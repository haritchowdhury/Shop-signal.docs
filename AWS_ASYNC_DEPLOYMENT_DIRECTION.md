# AWS Async Deployment Direction

## Status and role

Current architectural direction, reconciled with the application and the agreed
target on **11 August 2026**.

This document is the architectural guardrail for the AWS migration. It explains
which services own which responsibilities and prevents implementation agents
from substituting a different orchestration or persistence model. It is not the
execution checklist.

Use the active documents as follows:

- `FINAL_LAMBDA_SQS_S3_MIGRATION_EXECUTION_PLAN.md` — frozen implementation
  specification; Section 10A defines corrective Windows G-R7 through G-R9.
- `ACTIVE_EXECUTION_STATE.md` — sole authority for the current assignment,
  sequence, status, and stop point.
- `AWS_PIPELINE_EXECUTION_EVIDENCE.md` — append-only evidence for new
  corrective execution.
- `TARGET_LAMBDA_SQS_S3_EXECUTION_FLOW.md` — target pipeline flow and fan-out.
- `PRELIMINARY_LAMBDA_SQS_S3_MIGRATION_PLAN.md` — discovery-gated migration
  phases, contracts, verification, and cutover requirements.
- `AWS_BEGINNER_SETUP_GUIDE.md` — completed learning-environment setup and
  resource names; its learning resources are not the production pipeline.
- `DECISION_COMPLETE_CHECKLIST_AUTHORING_STANDARD.md` — authoritative checklist
  authoring and execution-state rules. `PARENT_AGENT_CHECKLIST_INSTRUCTIONS.md`
  is retained as historical first-draft context.

If another document recommends Fargate, Step Functions, DynamoDB coordination,
queue-emptiness fan-in, S3-event fan-in, or removal of either CrUX source, that
recommendation is not part of the active target.

## Objective

Move the long-running backend work to an asynchronous AWS execution pipeline
while preserving the existing product behavior:

- the existing frontend, authentication, ownership, query review, run history,
  results, and CSV behavior remain authoritative;
- a user confirms the complete query revision before scraping begins;
- work continues after the initiating browser or HTTP request closes;
- individual work units are bounded and retry-safe;
- large intermediate results live in private S3 objects;
- SQS provides delivery, retries, dead-letter handling, and backpressure;
- Neon/Postgres remains the application database and durable coordinator; and
- the final result is exposed only after every required domain task has a
  reconciled terminal outcome.

## Locked service decisions

### Neon/Postgres

Neon is the durable application database and execution coordinator. It owns:

- users, ownership, runs, confirmed query revisions, shops, run stores, lead
  snapshots, reusable shop profiles, user-shop grants, traffic caches, traffic
  publication, scoring state, and public result visibility;
- immutable stage manifests and expected task counts;
- idempotent terminal task records and counters;
- bounded stage and task leases, fencing tokens, attempts, and safe failures;
- conditional stage advancement; and
- final atomic result publication.

Do not introduce DynamoDB as a second run-status or coordination authority.
Duplicating run state across Neon and DynamoDB would create reconciliation and
truthfulness failures without providing a needed capability.

### S3

S3 stores versioned, validated, potentially large pipeline artifacts. It is not
the completion coordinator. Every artifact has a deterministic key, versioned
envelope, input fingerprint, and content fingerprint.

Target keys begin with:

```text
runs/{runId}/queries/{queryId}/domains.json
runs/{runId}/domains-manifest.json
runs/{runId}/domains/{domainId}/lead.json
runs/{runId}/domains/{domainId}/traffic-crux.json
```

S3 objects must remain private and encrypted. Credentials, credential-bearing
URLs, unrestricted provider responses, raw HTML, and user-private fields that
are not required by the artifact contract must not be stored.

S3 object existence or object count never proves stage completion. A worker
writes and validates its artifact before recording the corresponding Neon task
as terminal.

### SQS

SQS provides at-least-once delivery and backpressure between bounded stages.
Production uses separate queues and dead-letter queues where workload,
concurrency, retry, or permission boundaries differ.

Workers must expect duplicate and delayed delivery. They use partial batch
failure responses when a Lambda receives an SQS batch. Queue visibility timeout
must exceed the corresponding Lambda timeout, and receive limits must route
poison messages to a DLQ instead of retrying forever.

Queue emptiness is not a completion signal. SQS messages may be invisible,
delayed, duplicated, or in flight.

### Lambda

Lambda runs bounded worker and aggregator operations. No invocation owns the
whole run, waits for an entire queue to drain, or approaches Lambda's 15-minute
platform limit.

The target does not use one long-running Fargate worker and does not use Step
Functions as the orchestrator. Durable orchestration comes from SQS delivery,
S3 artifacts, and Neon conditional task/stage transitions.

### Existing application control plane

The existing frontend and backend HTTP control plane remain in place initially.
They continue to own:

- authentication and owner-scoped access;
- run creation and input validation;
- category normalization;
- query generation, probing, editable review, revision conflict handling, and
  explicit confirmation;
- status, history, master-lead, result, traffic, and CSV APIs; and
- cancellation requests and result presentation.

The AWS migration changes scraping execution after query confirmation. It does
not authorize a rewrite to API Gateway, Cognito, DynamoDB, or a separate frontend
contract. Hosting changes to the existing control plane are a separate decision.

## Target execution flow

```text
existing API/auth/query planning/review
        |
        | confirmed immutable query revision;
        | durable Google probe attempt/result reuse
        v
register discovery stage and query tasks in Neon
        |
        v
discovery SQS — one message per confirmed RunQuery
        |
        v
query Lambda — consumes confirmed probe results (zero Google/Browserless),
               deterministic per-query domain artifact in S3
        |
        v
Neon terminal record + aggregation-check message
        |
        v
domain aggregator — reconcile, deduplicate, preserve provenance,
                    plan reusable and missing work
        |
        v
cumulative domain manifest in S3 + lead-stage registration
        |
        v
lead SQS — one message per unique domain needing lead work
        |
        v
lead Lambda — HTTP-first bounded page discovery and enrichment,
              Browserless fallback when required,
              terminal per-domain lead artifact in S3
        |
        v
lead aggregator — reconcile all outcomes and bulk-persist private RunStore/Lead
                  checkpoint; no new profile/grant visibility
        |
        v
traffic SQS — one logical task per eligible domain needing provider work
        |
        v
combined traffic/CrUX Lambda — SQS-triggered, Neon-fenced stage-wide execution
                               preserving run-wide provider batching and one
                               logical terminal artifact per domain
        |
        v
final aggregator — reconcile all source components, create/link new profiles
                   and grants, bulk-persist traffic, score, atomically expose
                   results, complete run
```

## Work and artifact granularity

Task granularity and provider-call granularity are intentionally different.

| Stage | Durable task/artifact unit | Allowed execution grouping |
|---|---|---|
| Discovery | One confirmed `RunQuery.id` | One query per message |
| Domain aggregation | One run generation | One conditional aggregator claim |
| Lead enrichment | One unique stable domain | One domain per message |
| Lead publication | One run generation | One private bulk database checkpoint; public profile/grant visibility waits for final publication |
| Traffic and CrUX | One eligible domain | One Neon-fenced stage-wide run group; the received SQS batch is only a trigger |
| Final publication | One run generation | One conditional aggregator claim |

The combined traffic worker may execute a stage-wide group only when one live
Neon lease owns the exact run, generation, immutable work plan, registered task
set, and provider configuration. It loads that complete set after the lease is
won; it does not infer the set from records delivered together by SQS. It still
produces and coordinates one terminal artifact per logical domain task.
Global `ShopWork` ownership is additionally fenced by the registered domain
PipelineTask, not solely by the temporary Run lease, so the required lease
release before final aggregation does not open a cross-run reclaim window.

## Neon coordinator contract

The exact schema and transaction-composable callables are locked in Section 11
of the final checklist; the behavior summary here is subordinate to them.

Each stage records:

```text
runId
stage
generation
manifestS3Key
manifestFingerprint
expectedCount
terminalCount
succeededCount
failedCount
state
version
leaseToken
leaseExpiresAt
safeErrorCode
safeErrorMessage
```

Each expected task records:

```text
runId
stage
generation
itemKey
state
artifactS3Key
artifactFingerprint
attemptCount
leaseToken
leaseExpiresAt
terminalAt
safeErrorCode
safeErrorMessage
```

Required behavior:

1. Register the complete immutable expected set before dispatch.
2. Claim tasks and aggregators with bounded compare-and-swap leases.
3. Fence expired owners so they cannot publish late.
4. Write and validate S3 before the first terminal Neon transition.
5. Increment counters only on the first nonterminal-to-terminal transition.
6. Send an aggregation-check after durable terminal recording and before the
   original SQS message is acknowledged.
7. Aggregate only when `terminalCount === expectedCount`, then verify every
   expected item rather than trusting the count alone.
8. Handle `expectedCount = 0` explicitly so all-reused and empty stages advance.
9. Make publication and next-stage registration replay-safe.
10. Never poll Neon repeatedly to infer queue completion or silently recompute a
    different business reuse decision inside a worker.

## Identity, ownership, and historical data

The existing stable shop identity remains authoritative:

- `Shop.stableKey` and `shopIdForStableKey()` define global shop identity;
- `RunStore` and `Lead` remain run-specific historical snapshots;
- `ShopLeadProfile` may be reused only when its strict contract parses and its
  identity matches the durable shop;
- global shop/profile/cache existence never grants a user access;
- `UserShop` and `UserShopDiscovery` grants remain part of final atomic
  publication, never the private lead checkpoint;
- owner-scoped reads and query-revision conflicts must not weaken; and
- historical results remain immutable.

AWS workers must not introduce a second domain-normalization or ID algorithm.

## Page discovery and Browserless

Lead enrichment keeps the current economical shape and tightens its diagnostics:

1. Discover same-store evidence candidates from the homepage, verified result,
   initial internal links, and a bounded sitemap scan.
2. Rank the candidates and initially keep at most five pages per domain.
3. Attempt ordinary HTTP first.
4. Send only failed or unusable responses to Browserless.
5. Group render-required URLs into one logical domain render batch and execute
   them sequentially in one Browserless `/function` session.
6. Stop navigating as soon as sufficient contact evidence exists.
7. Enforce a 45-second total Browserless session deadline, with shorter page
   navigation deadlines and cleanup margin.
8. Use the primary and fallback tokens sequentially. They have independent
   usage ledgers, but the design must not assume additive concurrency.
9. Start the lead function and its event source at maximum concurrency two. A higher ordinary-HTTP
   concurrency requires separating rendered work or adding a proven distributed
   Browserless capacity gate.
10. Persist privacy-safe rendering diagnostics: attempt, outcome category,
    duration, page count, token label, early-stop reason, and budget exhaustion.

Browserless currently reports a free-plan maximum of two simultaneous sessions.
The controlled `/function` probe used exactly one unit for each of three opened
sessions, including one public-endpoint failure, and proved same-session early
stop plus cross-host redirect rejection. The checked tokens showed separate
free-plan unit ledgers. Historical success and failure counts are not available
through the token usage API, so the target must record its own safe outcomes.

The lead Lambda should initially use a measured 75–90 second timeout. Its SQS
visibility timeout must be higher, while the Browserless session remains capped
at 45 seconds. A 429/capacity response may receive short bounded backoff and
jitter. A full session/navigation timeout is not immediately repeated inside the
same Lambda attempt.

The AWS lead path writes one immutable Browserless attempt artifact immediately
before `/function` and one independent AI-normalization attempt artifact before
Chat Completions. A found marker with no lead result resolves safely without a
second paid request. Primary/fallback Browserless requests remain sequential;
fallback is permitted only for explicit 401, 403, or 429 before an accepted
provider envelope.

## Provider responsibilities and batching

### DataForSEO

DataForSEO supplies configured traffic-estimation scopes. Preserve its current
bulk request behavior, paid-request ledger, cost reservation, ambiguity handling,
strict normalized contract, and cache identity. Do not issue one paid bulk task
per domain.

### CrUX REST

CrUX REST remains enabled for per-origin Core Web Vitals used by score v3. It is
one REST request per required origin, subject to bounded concurrency and source-
specific cache reuse. Each missing origin has an immutable pre-call attempt
artifact, so all process restarts together permit only one adapter invocation
(the retained adapter may perform its bounded internal HTTP attempts).

### CrUX BigQuery

CrUX BigQuery remains enabled for monthly popularity rank and device
distribution. Preserve one latest-table lookup and a bounded origin batch query,
including dry-run and maximum-bytes-billed guards. Do not replace it with REST or
turn it into one BigQuery query per domain.
The live-query attempt artifact retains the resolved month, accepted dry-run
bytes, stable request ID, and dispatch time. An unexpired retry can therefore
repeat only the identical live request without repeating preflight; later
unknown outcomes become explicit ambiguity.

For discovery and traffic, “initial concurrency one” means Lambda reserved
concurrency one. Do not set an SQS event-source `MaximumConcurrency` of one:
AWS permits that mapping property only from two upward. Lead uses reserved
concurrency two and event-source maximum concurrency two. Check queues use their
separately measured bounds.

### Combined artifact

Each domain's traffic artifact contains independent terminal components:

```text
dataforseo
cruxRest
cruxBigQuery
```

Each component records whether it was required, reused, skipped, available,
partial, no-coverage, unavailable, ambiguous, or contract-mismatched as
supported by its source. DataForSEO `partial` is material and references its
validated source artifact. One source never masquerades as another.

The verified 52-eligible-domain run used 10 DataForSEO external tasks, 52 CrUX
REST calls, one CrUX BigQuery table-list call, and one BigQuery query. Equivalent
provider-call amplification blocks cutover.

## Payload and external-contract policy

Every SQS message and S3 artifact requires a strict versioned validator and
positive and negative fixtures before live dispatch.

External provider responses remain inside their adapters. Consumed fields must
come from one observed, provenance-labelled contract. Do not probe alternate
envelopes or aliases until one happens to parse. Missing or moved consumed fields
produce typed, privacy-safe contract-drift failures.

SQS messages carry identity, generation, fingerprints, and S3 references—not
large provider or lead documents. S3 artifacts carry only fields required by a
downstream contract. Neon coordination rows carry state and references, not raw
artifacts.

Payload discovery must measure normal and boundary JSON byte sizes before queue,
Lambda, and database settings are finalized.

## Secrets, IAM, and networking

Production credentials use approved secret references and never enter Git, SQS,
S3 artifacts, coordinator rows, logs, or frontend responses. This includes AWS
credentials, Neon credentials, OpenAI, Google Custom Search, Browserless,
DataForSEO, CrUX API, and Google/BigQuery authorization material.

Use temporary AWS SSO credentials for operators and least-privilege execution
roles for each worker class. S3, SQS, Lambda, and production artifacts use one
project Region unless a documented service constraint requires otherwise.

Workers require outbound TLS access to Neon and the configured providers. Do not
place Lambdas in a VPC unless access to a private resource requires it; otherwise
NAT cost and failure modes are introduced without benefit.

## Learning AWS resources

The resources created by `AWS_BEGINNER_SETUP_GUIDE.md` are a sandbox proof of:

```text
SQS -> Lambda -> S3
```

Current recorded learning values include:

```text
Project Region: ap-south-2
AWS profile: storesignal-dev
S3 bucket: signalshop-buk
Source queue: storesignal-dev-learning
DLQ: storesignal-dev-learning-dlq
Lambda: storesignal-dev-learning-worker
```

They are not production queue, function, IAM, artifact-layout, or retention
contracts. Sandbox writes stay under `learning/`. Its current lifecycle rule
only aborts incomplete multipart uploads after seven days and does not expire
completed objects; no production `runs/` retention policy may be inferred from
it. The recorded learning retry test passed: the same invalid message failed
five receives and is present in the DLQ.

## Reliability and observability requirements

- At-least-once delivery cannot duplicate durable results.
- Conflicting replays fail instead of overwriting prior artifacts or rows.
- A successfully committed query, lead, or provider checkpoint survives a later
  stage failure.
- Rejected, failed, skipped, reused, no-coverage, ambiguous, and contract-
  mismatch outcomes are explicit rather than missing.
- Cancellation fences late publishers and prevents new dispatch without erasing
  committed checkpoints.
- Scheduled recovery may reclaim expired known tasks but cannot widen an
  immutable manifest.
- Structured logs include run, stage, generation, task identity, attempt, safe
  outcome, duration, and artifact key; they exclude raw payloads and secrets.
- CloudWatch alarms cover DLQ depth, terminal infrastructure failures, stuck
  leases, throttles, error rate, and unexpected provider-call or cost growth.
- Final status and `resultsAvailable` remain truthful and atomic.

## Concurrency direction

Use separate concurrency controls for discovery, lead, traffic/CrUX, and
aggregators. Begin conservatively:

- lead Lambda maximum concurrency: two, because it can consume Browserless;
- aggregation: one conditional lease owner per run-stage-generation;
- CrUX REST: bounded to the documented provider quota and measured latency;
- DataForSEO and BigQuery: preserve batches instead of scaling per-domain calls;
- database writes: bounded bulk publication, not an unbounded connection fan-out.

The final execution checklist locks conservative initial function settings:
discovery and traffic/CrUX use reserved concurrency one (their SQS mappings omit
`MaximumConcurrency`, because AWS does not accept a value of one), with traffic
consuming a measured bounded reference batch so provider grouping is preserved.
These are not implementation-agent choices. Increase any limit
only after observing provider, Neon, SQS, Lambda, and cost behavior and receiving
parent review.

## Deployment sequence

1. Complete and record the learning AWS retry/DLQ test.
2. Run the required parent-owned payload discovery probes.
3. Produce strict payload contracts, sanitized fixtures, size measurements,
   provider-call budgets, and the Neon coordinator migration requirements.
4. Execute `FINAL_LAMBDA_SQS_S3_MIGRATION_EXECUTION_PLAN.md`, the reviewed
   file-level checklist authored under the parent-agent rules.
5. Implement locally with deterministic fixtures and isolated database tests.
6. Deploy production AWS resources with dispatch disabled.
7. Run isolated low-volume AWS smoke tests.
8. Add a configuration switch and shadow comparison against the current path.
9. Enable controlled production runs and observe cost, retries, provider calls,
   output equivalence, ownership, and frontend behavior.
10. Retain the current execution path for rollback until every cutover gate is
    satisfied.

## Explicit exclusions

Implementation agents must not introduce the following without a new parent-
owned architecture decision:

- Fargate as the primary pipeline worker;
- Step Functions as the pipeline orchestrator;
- DynamoDB as run state or fan-in coordination;
- S3 events or queue emptiness as completion proof;
- one Lambda invocation for a complete run;
- per-domain DataForSEO tasks or BigQuery queries that destroy bulk economics;
- removal or substitution of either CrUX REST or CrUX BigQuery;
- a second shop identity algorithm;
- an API/auth/frontend rewrite;
- Browserless concurrency above two without a proven capacity gate; or
- production AWS dispatch before payload contracts and retry/fencing tests pass.

## Definition of ready for implementation

The final implementation checklist may be assigned only when:

1. the AWS learning path, including DLQ retry, is verified;
2. payload discovery has captured exact query, domain, lead, traffic, message,
   artifact, and database-publication shapes;
3. every external contract consumed by new code has sanitized evidence and a
   strict parser fixture;
4. normal and boundary payload sizes are measured;
5. identity, ownership, reuse, transaction, idempotency, fencing, recovery,
   cancellation, and terminal-state rules are assigned to owning windows;
6. Browserless batching, concurrency, deadlines, and diagnostics are fixed;
7. DataForSEO and BigQuery amplification gates are quantified;
8. AWS and Neon prerequisites are separated from deterministic local
   acceptance; and
9. a fresh implementation agent can execute its window without relying on
   conversation history or choosing an architecture.

## Definition of migration complete

The migration is complete only when:

1. a confirmed query revision dispatches the exact immutable discovery set;
2. each stage advances from complete Neon terminal evidence rather than queue or
   object-store heuristics;
3. duplicate, delayed, reversed, and retried deliveries converge safely;
4. stale workers and aggregators cannot publish;
5. every qualified lead retains independent DataForSEO, CrUX REST, and CrUX
   BigQuery outcomes required by the run configuration;
6. Browserless stays within concurrency and session budgets without unexplained
   unit amplification;
7. bulk provider economics match or improve on the verified current run;
8. user ownership, historical snapshots, current master leads, scoring, traffic,
   CSV, and frontend contracts remain correct;
9. private artifacts, least-privilege IAM, secret redaction, alarms, DLQs,
   retention, rollback, and recovery are verified; and
10. the parent agent independently reviews the final source and evidence under
    `PARENT_AGENT_CHECKLIST_INSTRUCTIONS.md`.
