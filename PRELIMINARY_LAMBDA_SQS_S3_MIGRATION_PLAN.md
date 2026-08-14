# Preliminary Lambda–SQS–S3 Migration Plan

## Status

Preliminary implementation plan, reconciled with the current code, completed
payload discovery, controlled provider probes, and the agreed target architecture
on **11 August 2026**. The pipeline boundaries, orchestration choice, provider
responsibilities, payload evidence, persistence order, and cutover direction are
now decided. Exact production resource sizes and implementation estimates remain
implementation-checklist acceptance items rather than discovery assumptions.

## Source of truth

- Frozen implementation specification:
  `FINAL_LAMBDA_SQS_S3_MIGRATION_EXECUTION_PLAN.md`; Section 10A defines
  corrective Windows G-R7 through G-R9.
- Live assignment/status authority: `ACTIVE_EXECUTION_STATE.md`.
- Append-only corrective evidence: `AWS_PIPELINE_EXECUTION_EVIDENCE.md`.
- Architectural guardrails: `AWS_ASYNC_DEPLOYMENT_DIRECTION.md`.
- Target execution flow: `TARGET_LAMBDA_SQS_S3_EXECUTION_FLOW.md`.
- Existing frontend authentication, ownership, query review, run history, results, and presentation flows remain in place.
- Existing Neon/Postgres remains the durable application database.
- Target execution services are Lambda, SQS, and S3.

The former hybrid Fargate/Step Functions/DynamoDB proposal has been replaced by
the current AWS direction. This plan implements the locked Lambda-SQS-S3-Neon
pipeline and does not introduce DynamoDB, Fargate, or Step Functions into its
execution path.

## Locked architecture decisions

1. **Neon/Postgres is the coordinator.** It owns expected task counts, idempotent
   terminal task records, conditional stage transitions, bounded stage leases,
   safe failure state, and run completion. S3 holds the potentially large
   artifacts; SQS supplies delivery and backpressure.
2. **No queue-emptiness inference or S3-event fan-in.** A stage completes only
   when Neon records one terminal outcome for every task declared in its immutable
   stage manifest.
3. **One discovery message processes one confirmed query.** Every query remains
   attached to the current `runId` and durable `RunQuery.id`.
4. **One lead message processes one unique domain.** Domain identity reuses the
   current deterministic `Shop.stableKey` and `shopIdForStableKey()` contract.
5. **One traffic-and-CrUX task/message represents one eligible domain.** The
   delivered SQS batch is only a trigger. One Neon-fenced stage-wide owner loads
   the complete immutable run work set so DataForSEO and CrUX BigQuery retain
   run-wide bulk-request economics despite split, delayed, or concurrent SQS
   delivery. The owner executes the required source subset and still writes and
   coordinates one combined terminal artifact per domain.
6. **Both CrUX sources are retained.** CrUX REST supplies origin Core Web Vitals
   used by score v3; CrUX BigQuery supplies monthly popularity rank and device
   distribution. They remain independently cached and independently terminal
   inside the single logical CrUX stage.
7. **Reuse is source-specific.** `needsTraffic` represents DataForSEO.
   `needsCrux` is true when either required CrUX source needs work, while the
   manifest also records `needsCruxRest` and `needsCruxBigQuery` so the combined
   worker does not repeat a fresh source.
8. **Current application semantics remain authoritative.** Query review,
   ownership, `RunStore`/`Lead` historical snapshots, reusable `ShopLeadProfile`,
   `UserShop` grants, traffic publication, score v3, public serializers, and the
   frontend contract must not regress.
9. **Browserless remains a bounded fallback inside lead enrichment.** Ordinary
   HTTP remains the first fetch path. Page discovery stays limited to the ranked
   store evidence set, currently five pages per domain. URLs that still require
   rendering form one logical domain render batch executed through one
   Browserless `/function` session, stop as soon as sufficient contact
   evidence exists, and never exceed a 45-second total Browserless session
   deadline. Initial lead-worker concurrency is two so neither configured
   Browserless ledger exceeds the verified account limit. Primary and fallback
   tokens remain sequential fallbacks with no overlapping sessions; independent
   usage ledgers do not authorize an assumed combined concurrency of four.

## Verified current-state evidence

The latest configured Neon run containing DataForSEO and CrUX persistence was
`run_DbYDEoIOLGOB1DuOATyRkyTV`, created on 6 August 2026. It provides a concrete
payload-discovery baseline:

- 61 leads were persisted and 52 were traffic-eligible.
- All 52 eligible leads have `dataforseo`, `crux_rest`, and `crux_bigquery`
  records; no eligible lead is missing either CrUX source record.
- 34 leads have both CrUX sources available.
- 17 have terminal `no_coverage` outcomes from both CrUX sources.
- One has CrUX REST available and a CrUX BigQuery `contract_mismatch`.
- The 52 eligible leads used 52 CrUX REST calls, one CrUX BigQuery table-list
  call and one BigQuery query, and 10 DataForSEO external tasks across the
  configured scopes. The distributed path must not turn those bulk provider
  operations into one billable bulk query per domain.
- The run later failed with `RUN_LEASE_EXPIRED`, after enrichment persistence,
  and did not expose results. Distributed coordination must therefore use
  bounded per-stage/task fencing rather than one long-lived whole-run lease.
- Both configured Browserless tokens were valid when checked on 11 August 2026
  and exposed independent free-plan usage ledgers: before controlled discovery
  the primary had used 290 of
  1,000 units and the fallback 258 of 1,000 units in billing periods beginning
  3 August 2026. The token usage API does not expose historical per-request
  success and failure counts. Three bounded `/function` probe sessions moved the
  primary counter to 293, proving one unit per opened session in these cases.
- The current Browserless path performs ordinary HTTP first, invokes `/content`
  only for an unusable or failed response, permits two concurrent page fetches
  per store, has no Browserless retry, and reduces a failed rendered fallback to
  the ordinary response when one exists. The target must retain the economical
  HTTP-first behavior while making rendered outcomes observable.

This evidence confirms that a terminal provider outcome is not synonymous with
available measurements. The target artifact and coordinator must preserve
`available`, `no_coverage`, `unavailable`, `ambiguous`, and `contract_mismatch`
semantics where the current source supports them.

## Behavioral invariants

- Scraping never starts before the complete query revision is confirmed and
  revalidated.
- Duplicate SQS delivery, Lambda retry, or aggregator retry must not repeat a
  completed external provider call or overwrite a conflicting artifact.
- A worker persists its artifact before recording its terminal task outcome.
- Rejected, failed, no-coverage, and contract-mismatch outcomes are explicit
  terminal records; they are not represented by missing files.
- A successfully committed store, lead, or provider checkpoint survives a later
  stage failure.
- Only qualified run leads are eligible for DataForSEO and CrUX enrichment.
- Existing global shop/profile/cache data never grants user access by itself.
  Run-specific lead snapshots and `UserShop`/`UserShopDiscovery` grants remain
  part of the final atomic publication; the private lead checkpoint creates no
  new public grant or globally linked profile.
- Historical run results remain immutable. Current master leads continue to use
  reusable shop/profile/cache state through owner-scoped reads.
- Large or provider-derived payloads travel through S3, not SQS or coordinator
  columns.
- Browserless does not crawl every discovered URL. Store-page discovery remains
  bounded and ranked, and a domain worker processes no more than the manifest's
  selected page set.
- A domain attempts ordinary HTTP before consuming Browserless capacity. When
  more than one selected page needs rendering, the target creates one logical
  domain render batch and uses no more than one active Browserless session. A
  fallback or retry must never overlap the previous session and must record why
  another session attempt was allowed.
- A Browserless session has a 45-second hard deadline across all navigations,
  not 45 seconds per page. Page-level deadlines and early stopping must leave
  time for response transfer, artifact persistence, and browser cleanup.
- Browserless diagnostics persist safe outcome categories and timing without
  tokens, raw authorization data, or unrestricted rendered documents.

## Current-to-target conversion

| Current responsibility | Current location | Target responsibility |
|---|---|---|
| Run admission and ownership | Frontend API routes and backend HTTP server | Keep current API and ownership flow |
| Query generation and review | `pipeline.js`, `server.js`, `RunQuery` persistence | Keep current flow; dispatch confirmed queries after confirmation |
| In-process run queue | `server.js` `queueDrain()` and `drainQueue()` | Replace scraping-stage dispatch with SQS |
| Full run execution | `server.js` `executeRun()` | Split into bounded Lambda handlers |
| Store discovery across all queries | `discoverStoresFromQueryPlans()` | One discovery Lambda per query |
| Store aggregation and deduplication | Pipeline in-memory aggregation | Domain-aggregator Lambda reading query S3 files |
| Progressive per-store lead discovery | `processPersistedRunStores()` and `discoverLeadForRunStore()` | One lead Lambda per unique domain, with bounded HTTP-first page discovery and at most one Browserless rendering session where practical |
| Lead persistence | Progressive repository writes and `saveLeadBatch()` | S3 lead files followed by one private RunStore/Lead bulk checkpoint; new profiles and owner grants wait for final publication |
| Traffic orchestration | `enrichTraffic()` | Per-domain SQS triggers activate one Neon-fenced stage-wide DataForSEO + CrUX owner; execute only missing sources |
| CrUX REST | Per-origin REST request, current-scope cache, score-v3 evidence | Retain inside the combined domain worker |
| CrUX BigQuery | Monthly batched popularity query and cache | Retain inside the same combined domain worker |
| Traffic persistence | `saveTrafficSourceResults()` | One combined S3 artifact per domain followed by one final bulk-write Lambda |
| Completion | `completeTrafficEnrichment()` | Final aggregator validates, writes, and completes the run |
| Whole-run lease | `Run.lease*` heartbeat across long execution | Replace for distributed stages with bounded Neon stage/task claims and fencing |

## Target execution outline

```text
current API/auth/query planning/review/confirmation
  -> validate confirmed queries through immutable Google probe attempt/result
     artifacts; discovery later consumes those results with zero Google calls
  -> register immutable discovery stage in Neon
  -> discovery SQS: one confirmed query per message
  -> query Lambda -> deterministic query domains artifact in S3
  -> Neon terminal task record -> domain-aggregation check message
  -> domain aggregator: validate all query outcomes, deduplicate domains,
     preserve query provenance, plan reusable/missing work
  -> cumulative domain manifest in S3
  -> lead SQS: one message for each domain needing lead work
  -> lead Lambda -> terminal lead outcome artifact in S3
  -> Neon terminal task record -> lead-aggregation check message
  -> lead aggregator: materialize reusable and new outcomes, bulk-persist a
     private RunStore/Lead/diagnostic checkpoint; keep new profiles/grants hidden
  -> traffic SQS: one message per qualified domain needing any provider work
  -> combined worker: load the complete registered task set and execute the
     required DataForSEO + CrUX REST + CrUX BigQuery subset stage-wide
  -> combined traffic-crux artifact in S3
  -> Neon terminal task record -> final-aggregation check message
  -> final aggregator: create/link profiles and grants, settle task-fenced
     global work, bulk-persist provider rows, finalize score v3 and summary,
     atomically expose results and complete the run
```

## Neon coordinator contract

This preliminary schema summary is subordinate to the exact Section 11 schema,
signatures, migrations, and transaction ledgers in the final checklist.

### Stage record

One record per `(runId, stage, generation)` for `discovery`, `lead`, and
`traffic_crux`:

```text
runId
stage
generation
state                  registering | collecting | aggregating | completed | failed | cancelled
manifestS3Key
manifestFingerprint
expectedCount
terminalCount
succeededCount
failedCount
version
leaseToken
leaseExpiresAt
createdAt
startedAt
completedAt
safeErrorCode
safeErrorMessage
```

### Task record

One record per `(runId, stage, generation, itemKey)` where `itemKey` is a
`queryId` or `domainId`:

```text
itemKey
state                  pending | processing | succeeded | skipped | failed | cancelled
artifactS3Key
artifactFingerprint
attemptCount
leaseToken
leaseExpiresAt
terminalAt
safeErrorCode
safeErrorMessage
```

Required transaction rules:

1. Register the immutable expected item set before dispatching any stage message.
2. Claim a task conditionally with a bounded lease. An expired claim may be
   reclaimed; the expired owner cannot publish afterward.
3. Record a terminal outcome idempotently. Increment stage counters only on the
   first nonterminal-to-terminal transition.
4. After recording a terminal outcome, send an aggregation-check message before
   acknowledging the worker's original SQS message. If that send fails, the
   original delivery retries and safely resends the check without repeating work.
5. An aggregator proceeds only when `terminalCount === expectedCount`, then
   conditionally claims `collecting -> aggregating` with its own bounded lease.
6. The aggregator validates the complete expected item set and every artifact or
   explicit skip/failure record; counts alone are insufficient.
7. Aggregator publication and the next-stage registration are replay-safe. A
   retry either observes the identical committed checkpoint or fails on a
   conflicting fingerprint.
8. No worker polls the database for queue completion. Coordinator reads are for
   task fencing and stage advancement, not repeated business-data reuse checks.
9. Registering a stage with `expectedCount = 0` immediately sends or performs an
   aggregation check. All-reused and no-eligible-lead runs must advance without
   waiting for a worker message that will never exist.

## Phase 1 — AWS access and environment preparation

1. Select one AWS account and Region for Lambda, SQS, and S3.
2. Configure local AWS access outside the repository using an AWS profile, SSO, or another approved credential mechanism.
3. Confirm permission to create or manage:
   - Lambda functions and execution roles;
   - SQS queues, queue policies, event-source mappings, and dead-letter queues;
   - one S3 bucket, bucket policy, encryption, lifecycle rules, and CORS only if required;
   - Lambda environment variables and secret references.
4. Keep all credentials and secrets out of Git and S3 payloads.
5. Keep Lambda functions and the S3 bucket in the same AWS Region.
6. Confirm that Lambda can reach Neon and the existing external providers.
7. Record resource names through environment configuration rather than embedding them in worker code.
8. Confirm Google authentication for both CrUX paths from Lambda:
   - CrUX REST API access;
   - BigQuery billing project, dataset location, dry-run, and maximum-bytes-billed guard.
9. Select SQS visibility timeouts and Lambda timeouts only after measuring the
   extracted query, lead, and combined enrichment units. Every unit must remain
   comfortably below Lambda's 15-minute platform limit.
10. For the initial lead queue, configure Lambda/event-source maximum concurrency
    at two. Set the lead Lambda timeout to a measured value in the 75–90 second
    range and its SQS visibility timeout above that value, while independently
    enforcing a 45-second maximum Browserless session deadline.

## Phase 2 — Payload discovery

### Runs and queries

1. Capture representative normalized category input.
2. Capture the persisted confirmed-query shape used by `loadConfirmedQueryPlans()`.
3. Capture query identifiers, category relationships, revisions, probe results, audit data, and diagnostics.
4. Measure the number and encoded size of queries for small, normal, and maximum runs.

### Query discovery output

1. Capture the exact output of one query passed through store discovery.
2. Identify every field needed for domain normalization, deduplication, evidence, ranking, diagnostics, and later lead processing.
3. Measure domain counts, duplicate rates, payload size, and worst-case query artifact size.
4. Verify which values can be regenerated and which must survive in S3.

### Domain manifest

1. Capture the existing stable domain identity rules from
   `parseShopIdentity()`, `Shop.stableKey`, and `shopIdForStableKey()`; do not
   introduce a second AWS-only domain identity.
2. Capture all query-to-domain provenance required by results and diagnostics.
3. Identify the database reads needed to determine:
   - reusable lead data;
   - reusable DataForSEO data;
   - reusable CrUX REST data;
   - reusable CrUX BigQuery data.
4. Encode `needsLead`, `needsTraffic`, `needsCrux`, `needsCruxRest`, and
   `needsCruxBigQuery`. The top-level `needsCrux` is the logical OR of its two
   source flags.
5. Measure normal and worst-case cumulative manifest size.
6. Preserve every associated confirmed `queryId`, representative discovery
   occurrence, category intent, and identity evidence required to materialize the
   current `RunStore` candidate and historical lead snapshot.

### Existing-data reuse matrix

Reuse means a current value satisfies the required identity, contract, scope,
metric, and freshness checks. Mere row existence is insufficient. Discovery
found a current-code drift: the progressive orchestrator prefers
`readReusableTrafficCache()` and `readReusableLatestCruxBigQueryCache()`, whose
queries do not currently filter `expiresAt`; the older fallback methods do.
The target contract below is authoritative, and Window G1 must correct and
regression-test this drift rather than reproducing it in Lambda.

| Work | Reusable when | Requires work when |
|---|---|---|
| Lead | A completed `ShopLeadProfile` parses successfully and matches `Shop.stableKey` | Missing, processing lease expired, failed, invalid, or contract-incompatible profile |
| DataForSEO | Every required configured scope has a matching unexpired cache row for the current contract and metric set; fresh `no_coverage` remains reusable | Any required scope is missing, stale, ambiguous, failed, or contract-incompatible |
| CrUX REST | Exact canonical origin has an unexpired `current` cache result for the required metric set and contract; fresh `no_coverage` remains reusable | Missing, stale, failed, or contract-incompatible REST result |
| CrUX BigQuery | Exact canonical origin has a result for the selected latest dataset month and current popularity contract; terminal no-coverage may be reused under its policy | Missing latest month, stale policy result, failed, or contract-incompatible BigQuery result |

The domain aggregator performs this business reuse check in bounded database
reads and records the decision and source identities in the immutable manifest.
Workers may still read Neon for task fencing and persisted lead input, but must
not silently recompute a different reuse plan.

### Lead output

1. Capture successful, rejected, failed, ambiguous, and reusable lead outcomes.
2. Capture `Lead`, `Shop`, `ShopLeadProfile`, `RunStore`, and diagnostic fields required by the lead bulk writer.
3. Identify which fields are domain-global and which are specific to a run or query.
4. Measure normal and maximum lead artifact sizes.
5. Define one explicit terminal artifact for every `needsLead=true` domain,
   including safe failed/rejected outcomes. Reusable domains remain explicit
   manifest entries and are materialized into the run checkpoint by the lead
   aggregator.
6. Capture safe Browserless diagnostics independently from the final lead
   outcome: render requested, render attempted, success or failure category,
   HTTP status class where safe, duration, rendered-page count, selected token
   label (`primary` or `fallback` only), early-stop reason, and session-budget
   exhaustion. Never persist the credential or a credential-bearing URL.
7. Record the bounded selected-page manifest and which pages were satisfied by
   ordinary HTTP, rendered in Browserless, skipped after early success, or
   failed. Do not retain unrestricted raw page bodies in the coordinator.

### Traffic and CrUX output

1. Capture DataForSEO, CrUX REST, and CrUX BigQuery output shapes.
2. Capture provider request IDs, cost, cache state, freshness, coverage, diagnostics, and scoring inputs.
3. Use one combined domain artifact containing independent `dataforseo`,
   `cruxRest`, and `cruxBigQuery` terminal components. A source not required by
   the manifest is recorded as reused or skipped with its durable reference.
4. Identify every field required by score finalization and run summaries.
5. Measure normal and maximum traffic artifact sizes.
6. Confirm that the artifact retains REST Core Web Vitals for score v3 and
   BigQuery popularity/device data for public presentation. One source must not
   masquerade as a replacement for the other.

### Completion and failure behavior

1. Capture current progress, stage, summary, lease, retry, and safe-error transitions.
2. Identify the terminal conditions for each query and domain.
3. Determine how partial query, lead, traffic, and provider failures must affect final run state.
4. Validate the agreed proof: immutable expected item set, Neon terminal task
   records, and matching S3 artifacts or explicit skipped/reused records.
5. Exercise the agreed retry-safe fan-in protocol using SQS delivery, S3
   artifacts, and Neon conditional task/stage transitions.
6. Preserve current optional-provider behavior: a terminal provider failure can
   produce a partial/unavailable enrichment outcome without discarding a valid
   lead checkpoint. Infrastructure or invariant failures remain run failures.

## Phase 3 — Payload contracts and S3 layout

1. Define and version the query-discovery S3 contract.
2. Define and version the cumulative domain-manifest contract.
3. Define and version the domain lead-result contract.
4. Define and version the combined domain traffic/CrUX-result contract with
   independent DataForSEO, CrUX REST, and CrUX BigQuery components.
5. Define and version SQS message contracts for every worker and aggregator.
6. Finalize deterministic S3 keys:

   ```text
   runs/{runId}/queries/{queryId}/domains.json
   runs/{runId}/domains-manifest.json
   runs/{runId}/domains/{domainId}/lead.json
   runs/{runId}/domains/{domainId}/traffic-crux.json
   ```

7. Define schema validation at every SQS and S3 boundary.
8. Define artifact versioning, conditional-write, replay, retention, and cleanup rules.
9. Define how terminal failures and skipped work are represented without missing artifacts.
10. Include `runId`, stage generation, `queryId` or `domainId`, input manifest
    fingerprint, contract version, produced-at time, and terminal outcome in every
    artifact envelope.
11. Keep credentials, raw authorization material, unrestricted provider
    responses, and user-private fields out of SQS messages and coordination rows.
12. Use conditional S3 writes. A replay may accept an existing object only after
    its version, identity, input fingerprint, and content fingerprint reconcile.

## Phase 4 — Extract bounded execution units

1. Preserve existing provider and pipeline logic while removing dependence on one long-lived `executeRun()` call.
2. Extract a query-scoped store-discovery operation from `discoverStoresFromQueryPlans()`.
3. Reuse `discoverLeadForRunStore()` behind a domain-scoped Lambda handler.
4. Extract domain-scoped DataForSEO, CrUX REST, and CrUX BigQuery operations from
   `enrichTraffic()` and compose them behind one combined domain handler.
5. Keep query generation, probing, review, and confirmation behavior unchanged initially.
6. Ensure every extracted operation accepts an explicit versioned payload and returns an explicit versioned result.
7. Remove process-local coordination from the extracted operations.
8. Preserve the present provider adapters, normalizers, request guards, cache
   contracts, cost ledger, score finalizer, and serializers rather than rewriting
   provider logic inside Lambda handlers.
9. Extract a domain-scoped rendering operation that accepts only the selected
   URLs still requiring Browserless after ordinary HTTP assessment. It creates
   one logical render batch, permits no more than one active Browserless session,
   enforces one 45-second total deadline per session attempt, applies shorter
   bounded page navigations, and stops early when sufficient direct or indirect
   contact evidence is available.
10. Keep the current five-page ranked discovery limit initially. Increasing it
    requires measured evidence that the additional contact yield justifies the
    latency and Browserless-unit cost.

## Phase 5 — Add infrastructure adapters

1. Add one S3 artifact adapter for validated reads, conditional writes, and deterministic keys.
2. Add one SQS dispatcher adapter for validated messages and batch dispatch.
3. Add one Neon execution-coordinator adapter for stage registration, task claims,
   terminal recording, aggregation claims, recovery, and fencing.
4. Add Lambda configuration loading and validation.
5. Add structured logging fields for `runId`, stage generation, `queryId`,
   `domainId`, source, attempt, lease token identifier, and artifact key.
6. Keep AWS-specific code outside the core discovery, lead, and enrichment logic.
7. Retain local adapters or fixtures so payloads can be tested without live AWS calls.

## Phase 6 — Implement target workers and aggregators

1. Confirmed-query dispatcher:
   - writes the immutable query manifest;
   - registers the discovery stage and expected `RunQuery.id` task set in Neon;
   - sends one discovery message per confirmed query.
2. Store-discovery Lambda:
   - processes one query;
   - writes one query-specific S3 artifact;
   - records a terminal discovery task and sends an aggregation-check message.
3. Domain-aggregator Lambda:
   - claims the ready discovery stage conditionally;
   - reads and reconciles all expected query artifacts;
   - merges and deduplicates domains;
   - assigns the deterministic current shop/domain identity;
   - retains all query and category provenance;
   - checks reusable lead, DataForSEO, CrUX REST, and CrUX BigQuery data;
   - writes the cumulative domain manifest;
   - bulk-checkpoints discovered `Shop`/`RunStore` state as required by the
     existing persistence contract;
   - registers and dispatches required lead jobs.
4. Lead-enrichment Lambda:
   - processes one domain;
   - discovers and ranks no more than the configured bounded page set, initially
     five pages;
   - fetches selected pages with ordinary HTTP first;
   - sends only pages with failed or unusable ordinary responses through one
     logical domain render batch with no overlapping Browserless sessions;
   - enforces a 45-second total Browserless budget with shorter per-page limits,
     stops early after sufficient contact evidence, and always closes the
     session;
   - treats the primary and fallback tokens as sequential alternatives rather
     than additive concurrency;
   - records safe rendering diagnostics in the terminal artifact;
   - writes one domain-specific terminal lead artifact;
   - records a terminal lead task and sends an aggregation-check message.
5. Lead S3-to-database aggregator Lambda:
   - claims the ready lead stage conditionally;
   - verifies every new, reusable, rejected, and failed lead outcome;
   - bulk-writes private run-specific lead snapshots and diagnostics;
   - leaves new profiles unlinked and creates no
     `UserShop`/`UserShopDiscovery` grant;
   - records the private lead checkpoint with `resultsAvailable=false`;
   - determines traffic eligibility from the persisted qualified lead set;
   - registers one `traffic_crux` task per eligible domain needing at least one
     source and dispatches it.
6. Combined traffic-and-CrUX Lambda:
   - treats a bounded SQS batch as a trigger, acquires the one Neon-fenced
     traffic execution lease for the run/generation, and loads the complete
     immutable registered work set rather than defining provider batches from
     the delivered records;
   - loads each persisted qualified lead and domain work plan;
   - processes only the required subset of DataForSEO, CrUX REST, and CrUX
     BigQuery for each domain;
   - preserves run-wide DataForSEO scope batching and CrUX BigQuery origin
     batching while keeping REST requests per origin at bounded concurrency;
   - writes immutable normalized provider-batch artifacts before per-domain
     fan-out, allowing durable successes to resume without another bulk call;
   - retains independent cache, cost, coverage, contract, and diagnostic states;
   - writes one domain-specific combined traffic/CrUX artifact and terminal task
     for every message in the batch;
   - uses partial batch failure responses and sends final-aggregation checks for
     terminal tasks.
7. Final S3-to-database aggregator Lambda:
   - claims the ready traffic stage conditionally;
   - verifies every required, reused, skipped, and failed provider component;
   - bulk-writes DataForSEO, CrUX REST, and CrUX BigQuery cache/publication rows;
   - finalizes scoring and summaries;
   - atomically publishes `resultsAvailable`, completes the run, and releases
     distributed stage claims.

## Phase 7 — Durable stage coordination

1. Replace the in-process `queueDrain()` trigger for scraping work with SQS dispatch.
2. Define expected work counts from immutable query and domain manifests.
3. Make every worker safe under duplicate SQS delivery.
4. Make every S3 output key deterministic and safe under retries.
5. Ensure only one successful aggregator advances each stage.
6. Ensure an aggregator can be retried after a timeout without repeating completed external work.
7. Ensure stale Lambda invocations cannot publish over a newer run stage or artifact version.
8. Configure queue visibility timeouts above the corresponding Lambda timeout.
9. Configure bounded receive counts and dead-letter queues.
10. Configure separate maximum concurrency for discovery, lead, and traffic
    workloads. Start lead concurrency at two to enforce the known Browserless
    limit across both sequential token paths. Raise it only after either
    separating ordinary-only work from rendered work or adding a proven
    distributed Browserless capacity gate.
11. Add the Neon stage/task records and transactional counter rules described in
    this plan.
12. Emit aggregation-check messages after durable terminal recording and before
    acknowledging the worker message; never infer completion from an empty SQS
    queue or an S3 object count alone.
13. Use partial batch responses if handlers receive SQS batches, so completed
    messages are not retried with a failed sibling.
14. Reconcile stuck task and aggregator leases on bounded scheduled recovery.
    Recovery may redispatch known nonterminal tasks but may not widen the
    immutable expected item set.
15. Cancellation stops new dispatch, marks pending tasks terminal-cancelled or
    skipped under the versioned contract, and fences late publishers. Already
    committed checkpoints remain durable.
16. Treat task granularity and provider-call granularity separately: task state
    and artifacts remain per domain, while safe same-run batching preserves the
    current DataForSEO and BigQuery bulk behavior.
17. Handle Browserless 429/capacity failures with short bounded exponential
    backoff and jitter while session budget remains. Do not immediately repeat a
    full navigation/session timeout in the same Lambda attempt; allow the fenced
    SQS task retry to recover it without overlapping a possibly live session.
18. Distinguish four deadlines in configuration and telemetry: page navigation,
    total Browserless session (maximum 45 seconds), Lambda invocation, and SQS
    visibility. No inner deadline may consume the cleanup and durable-publication
    allowance of its outer deadline.

## Phase 8 — Database adaptation

1. Preserve user ownership and existing public read filters.
2. Add the minimum coordinator schema for stage/task state, counts, artifact
   references, fingerprints, attempts, bounded leases, and safe errors.
3. Reuse stable shop, lead, and traffic identities where their contracts remain valid.
4. Add private bulk RunStore/Lead checkpointing from validated S3 artifacts.
5. Add bulk traffic/CrUX publication from validated S3 artifacts.
6. Keep the private lead checkpoint separate from final run completion and from
   new global-profile/owner-grant visibility.
7. Make new profile linking, owner grants, traffic rows, score, and final result
   visibility one atomic final publication.
8. Remove or retire only the repository operations made obsolete by the new flow.
9. Make raw SQL schema-aware before reusing bulk publication in Lambda. The
   guarded integration suite currently exposes unqualified `Run`, `UserShop`,
   and `UserShopDiscovery` SQL in `grantRunShopsToOwner()` when tests use an
   isolated schema.
10. Keep old `crux_rest` and `crux_bigquery` enum values, cache rows, historical
    enrichment rows, and serializers. This migration retains both sources and
    must not rewrite old run evidence.
11. Replace the long-lived run lease as the distributed execution fence without
    weakening current owner-scoped reads or query-revision conflict checks.

## Phase 9 — Verification

1. Unit-test every payload validator and deterministic S3 key builder.
2. Contract-test every SQS message and S3 artifact version.
3. Test duplicate delivery, duplicate invocation, conditional-write conflict, timeout, retry, and dead-letter behavior.
4. Test multiple queries discovering the same domain.
5. Test reuse combinations:
   - lead, DataForSEO, CrUX REST, and CrUX BigQuery all missing;
   - lead reusable and all enrichment missing;
   - lead and DataForSEO reusable but one or both CrUX sources missing;
   - CrUX REST reusable but CrUX BigQuery missing, and the inverse;
   - fresh no-coverage reuse for either CrUX source;
   - one CrUX source contract-mismatched while the other is available;
   - all work reusable.
6. Test partial provider failures and final aggregation retry.
7. Compare the distributed result with the current pipeline for the same fixed inputs and provider fixtures.
8. Run a live low-volume AWS smoke test.
9. Run a controlled multi-query and multi-domain test.
10. Verify that no individual Lambda approaches the configured timeout.
11. Replay a fixture shaped like the verified 52-eligible-lead Neon run and prove
    that both CrUX components are retained per eligible lead.
12. Test a worker crash after S3 write, after Neon terminal commit, and before the
    aggregation-check send. Each retry must converge without a repeated provider
    call or lost stage transition.
13. Test an aggregator crash before and after each bulk checkpoint and before
    next-stage dispatch.
14. Test expired task and aggregator leases and prove the stale owner cannot
    publish.
15. Run the full backend suite, guarded PostgreSQL integration suite, secret scan,
    frontend tests, lint, and production build before cutover.
16. Add a provider-call amplification gate. For the verified 52-domain shape,
    compare REST call count, DataForSEO task count, BigQuery query count, bytes
    processed/billed, and total cost with the current pipeline; unexplained
    per-domain BigQuery or DataForSEO multiplication blocks cutover.
17. Test Browserless behavior with zero, one, and several render-required pages:
    ordinary HTTP remains first, every domain creates at most one logical render
    batch, no domain holds overlapping sessions, any fallback/retry attempt has
    an explicit safe reason, successful evidence stops later navigations, and all
    branches close the session.
18. Test the 45-second Browserless hard deadline, shorter page deadlines, 429
    backoff, navigation timeout, token fallback, Lambda timeout margin, SQS
    redelivery, and stale-invocation fencing.
19. Prove under load that no more than two lead workers can hold Browserless
    sessions initially. Compare Browserless units before and after the controlled
    fixture and fail the cutover gate on unexplained session or unit
    amplification.
20. Verify safe diagnostics distinguish ordinary success, rendered success,
    capacity failure, navigation timeout, contract/redirect rejection, session
    budget exhaustion, and early stop without exposing credentials or raw page
    bodies.

## Phase 10 — Deployment and cutover

1. Deploy AWS resources without changing production dispatch.
2. Deploy worker code with live dispatch disabled.
3. Run fixture and isolated live test runs through the new path.
4. Add a configuration switch between the current in-process path and the Lambda–SQS–S3 path.
5. Enable the new path for controlled runs.
6. Compare output, cost, latency, retries, provider-call counts, Browserless
   session counts, and Browserless unit consumption.
7. Increase concurrency only after observing provider and database behavior.
8. Retain the current execution path for rollback during the validation window.
9. Remove the long-lived worker path only after the new path passes the agreed acceptance criteria.
10. During shadow comparison, verify exact query-to-domain provenance, lead
    qualification, both CrUX components, score state, user grants, current master
    leads, historical result snapshots, and frontend CSV output—not only row
    counts.

## Required outputs from payload discovery

- Versioned query-discovery payload fixture.
- Versioned domain-manifest fixture.
- Versioned lead-result payload fixtures.
- Versioned combined traffic/CrUX payload fixtures covering DataForSEO, CrUX
  REST, and CrUX BigQuery independently.
- Versioned SQS message fixtures.
- Measured payload-size report.
- Stable identity and deduplication report.
- Existing-data reuse and freshness matrix.
- Proven Neon stage-completion, fencing, recovery, and retry protocol plus its
  coordinator migration requirements.
- Queue and Lambda concurrency recommendations.
- Browserless page/session budget, unit-consumption, early-stop, and safe
  diagnostic report.
- Database migration requirements.
- Proper implementation plan with file-level tasks, test gates, deployment order, rollback steps, and estimates.

## Preliminary stop condition

The architecture no longer requires another product decision. Parent-owned
payload discovery may begin, including sanitized contract fixtures, read-only
runtime evidence, and isolated disposable database prototypes. Do not assign an
implementation window, apply the coordinator migration, enable live AWS dispatch,
or begin production cutover until:

1. AWS access and provider connectivity are verified;
2. payload discovery and size measurement are complete;
3. every boundary has a versioned validator and fixture;
4. the schema-aware raw SQL integration issue is fixed;
5. retry/fencing tests are green; and
6. the resulting file-level implementation checklist, concurrency limits,
   deployment order, and rollback gates are reviewed under
   `PARENT_AGENT_CHECKLIST_INSTRUCTIONS.md`.

## Required payload-discovery probes before the final implementation checklist

These probes are owned and reviewed by the parent agent under
`PARENT_AGENT_CHECKLIST_INSTRUCTIONS.md`. They are
evidence gathering, not implementation windows. Do not assign production
implementation to subagents until the probe outputs pass the readiness gate at
the end of this section.

### Probe execution and evidence policy

1. Preserve one evidence report at
   `email_scraper/docs/research/LAMBDA_SQS_S3_PAYLOAD_DISCOVERY_REPORT.md`.
2. Preserve sanitized positive and negative JSON fixtures under
   `email_scraper/test/fixtures/aws-pipeline/v1/`. Exact subdirectories and
   contract filenames are outputs of the probes, but every retained fixture must
   identify its provenance and contract version.
3. If repeatable extraction requires a script, place the bounded script at
   `email_scraper/scripts/lambda-payload-discovery-probe.js`. It must default to
   read-only/local-fixture behavior and require an explicit confirmation flag for
   every billable provider call or AWS sandbox mutation.
4. Label every finding `observed`, `inferred`, or `unknown`. Only observed
   findings may become exact external parsing contracts. An inferred internal
   design may become a proposed contract only after it receives a strict schema,
   deterministic fixture, and parent review.
5. Never retain credentials, authorization headers, credential-bearing URLs,
   raw HTML, unrestricted provider bodies, owner identifiers, emails, phone
   numbers, or other unnecessary user-private data. Use deterministic synthetic
   identities in committed fixtures.
6. Production Neon access is read-only during discovery. Database mutation tests
   use the existing isolated integration-schema mechanism. No probe changes
   production run, lead, cache, ledger, lease, or ownership rows.
7. AWS mutation is restricted to the learning source queue and the `learning/`
   S3 prefix described by `AWS_BEGINNER_SETUP_GUIDE.md`. Do not create production
   queues, functions, roles, policies, triggers, or `runs/` artifacts during
   discovery.
8. Do not run `email_scraper/scripts/traffic-discovery-probe.js` casually. It
   explicitly performs three paid DataForSEO calls. Existing sanitized provider
   fixtures and persisted run evidence are preferred; any new paid call requires
   a stated call count, maximum cost, purpose, and explicit approval.
9. Browserless render probes consume units. Capture the unit balance immediately
   before and after an approved controlled probe and enforce the known global
   concurrency ceiling of two.
10. A failed prerequisite produces one concise blocker with the missing evidence
    and the exact safe action needed. Do not replace unavailable live evidence
    with a guessed contract.

### Required outputs

The complete probe run must produce:

- a source-of-truth and repository-state inventory;
- a sanitized AWS learning-topology record;
- confirmed-query, per-query discovery, cumulative domain-manifest, lead-result,
  combined traffic/CrUX, and SQS message fixtures;
- strict field catalogues for each payload, including intentionally excluded
  fields;
- normal, verified-run, and boundary encoded-size measurements;
- stable identity, deduplication, and query-provenance evidence;
- a fixed-time existing-data reuse and freshness matrix;
- a provider-call, bytes, units, latency, and concurrency budget;
- Browserless interface and diagnostic evidence for the planned domain render
  batch;
- Neon transaction, publication, and coordinator migration requirements;
- a complete durable failure-boundary and recovery matrix;
- Lambda packaging/runtime/connectivity measurements; and
- an observed/inferred/unknown register with no hidden planning assumptions.

### PD-00 — Source of truth and repository baseline

**Purpose:** Make every later fixture reproducible against the exact repository
state and prevent old plans or the ongoing directory move from being treated as
active code.

**Probe:**

1. Record the active architectural documents and their roles:
   `AWS_ASYNC_DEPLOYMENT_DIRECTION.md`,
   `TARGET_LAMBDA_SQS_S3_EXECUTION_FLOW.md`, this preliminary plan,
   `AWS_BEGINNER_SETUP_GUIDE.md`, and the parent-agent checklist rules.
2. Record applicable `AGENTS.md` files by directory.
3. Capture `git status --short`, the current commit when available, Node/npm and
   Prisma versions, and the active backend root. Treat the old tracked
   `Email Scrapper/` deletion plus new root directories as user-owned relocation
   state; do not repair or stage it during probing.
4. Catalogue relevant source, schema, migration, contract, fixture, and test
   paths. Mark older plans under `docs/history/` as supporting history rather
   than execution inputs.

**Acceptance evidence:** The report allows a fresh agent to identify one active
backend and one contradiction-free AWS direction without conversation history.

### PD-01 — AWS learning topology and retry proof

**Purpose:** Verify the already-created AWS path and discover exact non-secret
resource settings before specifying production infrastructure.

**Read-only probe:** Using profile `storesignal-dev`, inspect caller identity,
Region, the `signalshop-buk` bucket, learning source queue and DLQ, learning
Lambda, execution role, event-source mapping, and recent relevant logs. Record:

- bucket Region, public-access block, ownership, encryption, versioning, and the
  `learning/` lifecycle scope;
- queue type, ARN/URL fingerprints, encryption, visibility, retention,
  redrive policy, receive count, and DLQ relationship;
- Lambda runtime, architecture, memory, timeout, environment-variable names,
  role/policy action-resource pairs, and code-package metadata;
- event-source enabled state, batch size, partial-batch response setting, and
  maximum concurrency; and
- whether the invalid-JSON learning message completed five receives and reached
  the DLQ.

Do not record temporary credentials, the SSO cache, environment values that may
contain secrets, or complete IAM identity documents when a safe summary is
sufficient.

**Controlled mutation only if the existing retry evidence is absent:** With
explicit approval, send one uniquely identified invalid learning message, observe
its retry/DLQ lifecycle, and leave it for inspection. Do not purge queues or
change resource settings.

**Acceptance evidence:** A sanitized topology fixture and a passed
`SQS -> Lambda -> S3` plus retry-to-DLQ record. A pending DLQ test is a blocker to
claiming the learning environment complete, but not to local payload extraction.

### PD-02 — Confirmed query contract

**Purpose:** Fix the immutable discovery task input instead of sending a loose
Prisma row or reconstructing query context inside Lambda.

**Probe:**

1. Trace query creation, editing, confirmation, revision fencing,
   `loadConfirmedQueryPlans()`, validation, and query-probe persistence.
2. Read one representative confirmed run from Neon without mutation and sanitize
   it to deterministic identifiers and category text.
3. Catalogue every consumed field: `RunQuery.id`, run/generation identity,
   category index, sequence, query, source, validation state, score, generation
   reason, source URLs, category vocabulary, probe contract/fingerprint/results,
   and confirmed revision as applicable.
4. Separate fields required in the SQS envelope from fields referenced through
   an immutable S3/query manifest.
5. Measure one-query, normal-run, and configured-boundary query manifest sizes.

**Fixtures:** Valid confirmed query, stale revision, missing query ID, malformed
category context, duplicate sequence, invalid validation state, and unknown
additive field under the chosen extension policy.

**Acceptance evidence:** One strict versioned confirmed-query/message contract
whose validation proves the exact confirmed revision and durable `RunQuery.id`.

### PD-03 — Per-query discovery output

**Purpose:** Determine the exact artifact produced when the existing all-query
discovery pipeline is extracted into one confirmed-query worker.

**Probe:**

1. Trace `discoverStoresFromQueryPlans()`, search, identity resolution,
   occurrence diagnostics, query audits, and `runStoreCandidateFromDiscovery()`.
2. Execute one query deterministically with current strict Google/provider
   fixtures and controlled dependency overrides; do not make a live search call.
3. Capture successful, empty-result, partial occurrence failure, duplicate
   result, rejected store, and complete query failure shapes.
4. Retain every field needed later for stable identity, deduplication,
   representative selection, category assessment, query provenance, diagnostics,
   and historical materialization.
5. Prove raw HTML and initial fetch documents do not cross the artifact boundary.

**Acceptance evidence:** A versioned per-query domain artifact with positive and
negative parser fixtures, deterministic ordering/fingerprint, and measured empty,
normal, and maximum sizes.

### PD-04 — Domain aggregation, identity, and provenance

**Purpose:** Fix how multiple query artifacts become one cumulative domain
manifest without losing evidence or inventing an AWS-specific shop identity.

**Probe:**

1. Replay several query artifacts that discover the same store through custom
   and `myshopify.com` URLs, redirects, different ranks, categories, and query
   orders.
2. Verify `stableShopIdentity()`, `shopIdForStableKey()`, `runStoreId()`, current
   merge ordering, representative occurrence, duplicate count, assessments, and
   all query/category provenance.
3. Test unsafe cross-host canonical URLs, identity conflicts, missing observed
   host evidence, duplicated messages, and reversed artifact order.
4. Prove the same expected inputs create the same domain IDs, ordering, manifest
   fingerprint, and selected representative.

**Acceptance evidence:** A stable identity/deduplication report and cumulative
domain-manifest fixtures for single-query, multi-query duplicate, conflict,
empty, and boundary cases.

### PD-05 — Existing-data reuse and work planning

**Purpose:** Produce the immutable per-domain work plan once, before dispatch,
using current cache/profile contracts rather than row-existence checks.

**Probe:**

1. At a fixed recorded `evaluatedAt`, perform bounded read-only Neon queries for
   reusable `ShopLeadProfile`, DataForSEO scope caches, CrUX REST current caches,
   and latest-month CrUX BigQuery caches.
2. Exercise missing, fresh available, fresh no-coverage, stale, processing,
   failed, ambiguous, invalid payload, identity mismatch, metric mismatch,
   contract mismatch, partial DataForSEO scope, and one-CrUX-source-only cases.
3. Record exact source identities, scope/metric/contract keys, freshness evidence,
   and durable references without copying unrestricted normalized payloads into
   SQS.
4. Derive and validate `needsLead`, `needsTraffic`, `needsCruxRest`,
   `needsCruxBigQuery`, and logical-OR `needsCrux`.
5. Measure the query count and rows read for the verified 52-domain shape to
   prevent an N+1 coordinator design.

**Acceptance evidence:** A fixed-time reuse matrix, versioned work-plan fixture,
and proof that all-reused and no-eligible-work manifests advance with an explicit
zero-count stage.

### PD-06 — Lead input, output, and page diagnostics

**Purpose:** Fix the domain lead worker, private checkpoint, and final-publication inputs while
preserving current qualification, history, profile reuse, and ownership.

**Probe:**

1. Trace `runStoreCandidateSchema`, `discoverLeadForRunStore()`,
   `shopLeadProfileSchema`, `materializeLeadFromProfile()`, failed outcomes,
   `saveLeadBatch()`, grants, and public serialization.
2. Capture new qualified, new rejected, safe failed, reusable qualified,
   reusable rejected, and profile-contract failure outcomes.
3. Catalogue run-specific versus domain-global fields and every field needed for
   the private `RunStore`/`Lead`/diagnostic checkpoint and later atomic
   `ShopLeadProfile`/`UserShop`/`UserShopDiscovery` publication.
4. Record the selected five-page maximum, page ordering, ordinary/rendered/skipped
   disposition, safe error type, contact-evidence source, early-stop reason, and
   timing required by the target artifact.
5. Prove the artifact rejects raw HTML, provider bodies, credential fields,
   mismatched shop identities, and unbounded diagnostic arrays.

**Acceptance evidence:** Strict terminal lead fixtures for success, rejection,
failure, and reuse; normal and maximum byte sizes; and a field-level publication
map into the current schema.

### PD-07 — Browserless domain-render contract and budget

**Purpose:** Replace separate `/content` sessions with one observed, strictly
parsed logical domain render batch without guessing the chosen Browserless
interface.

**Local/read-only portion:**

1. Catalogue the current `/content` request, response-header adapter, ordinary-
   HTTP assessment, primary/fallback order, timeout, redirect guard, and silent
   rendered-failure behavior from source and existing fixtures.
2. Record current account usage through the read-only usage API, the verified
   concurrency ceiling of two, the 45-second total session ceiling, and the fact
   that historical success/failure counts are not token-accessible.
3. Compare `/function` and BaaS only from official contracts and current runtime
   needs. Select one interface before the controlled live probe.

**Controlled live portion requiring explicit unit approval:**

1. Use deterministic public pages and one logical batch containing several URLs.
2. Cap total Browserless time at 45 seconds, keep active concurrency at one for
   the probe, forbid proxies/CAPTCHA options, and set an explicit maximum unit
   budget.
3. Capture sanitized success metadata, response envelope/headers, page-level
   outcomes, navigation timeout, redirect rejection behavior, session cleanup,
   duration, early stop, and before/after units. Do not force queue saturation or
   store page bodies.
4. A 429 implementation contract consumes only the HTTP status and safe category
   unless a naturally observed, sanitized provider error shape is retained.
   Never create load merely to discover an error body.

**Acceptance evidence:** Strict positive and negative parser fixtures for the
selected interface, proof of one active session, a measured page/session budget,
and exact privacy-safe diagnostic fields. Until this probe is observed, the
multi-page Browserless external response is `unknown` and cannot be delegated as
an implementation contract.

### PD-08 — Combined traffic and CrUX work/result contract

**Purpose:** Fix one logical domain artifact with independent DataForSEO, CrUX
REST, and CrUX BigQuery outcomes.

**Probe:**

1. Trace `enrichTraffic()`, immutable run snapshot, eligibility normalization,
   source callbacks, normalized provider contracts, publication serializers,
   `saveTrafficSourceResults()`, score v3 finalization, and summary composition.
2. Replay existing strict provider fixtures and the latest persisted 52-eligible-
   domain run without new paid calls.
3. Capture available, no-coverage, unavailable, ambiguous, contract-mismatch,
   reused, and skipped component states where supported.
4. Map each source's request identity, scope, metric set, contract, freshness,
   cost/bytes telemetry, normalized payload, publication fields, score inputs,
   and public fields.
5. Prove CrUX REST Core Web Vitals and CrUX BigQuery popularity/device data
   remain independent and both survive partial failure of the other.

**Acceptance evidence:** Versioned combined traffic/CrUX fixtures covering every
reuse combination and terminal state, plus exact mappings to cache, run-specific
publication, summary, and score records.

### PD-09 — Provider batching and amplification budget

**Purpose:** Prevent per-domain task decomposition from multiplying paid or
large provider requests.

**Probe:**

1. Replay the verified 52-domain input and measure logical tasks, SQS batch
   grouping, DataForSEO scopes/tasks/targets, CrUX REST requests, BigQuery table
   lookups/queries, dry-run bytes, billed bytes, cache hits, and normalized
   outputs.
2. Exercise batch boundaries, one missing source, all sources reused, partial
   provider failure, and a failed sibling in an SQS batch.
3. Use request builders and fixtures for DataForSEO; do not run the existing
   three-paid-call probe without separate approval.
4. Permit a BigQuery dry run only after confirming credentials, billing project,
   location, and a zero-query-cost contract. Any executing query retains an
   explicit maximum-bytes-billed guard and approval.

**Acceptance evidence:** A provider-call budget whose verified-run baseline is
10 DataForSEO tasks, 52 CrUX REST calls, one BigQuery table-list call, and one
BigQuery query, with an explicit cutover failure threshold for amplification.

### PD-10 — SQS envelope, S3 object, and encoded-size boundaries

**Purpose:** Prove that queues carry small references while S3 carries validated
artifacts, and select settings from measured bytes rather than estimates.

**Probe:**

1. Define provisional versioned envelopes for each worker and aggregator with
   run, stage, generation, item identity, manifest/artifact key, fingerprint,
   attempt context, and no business payload that belongs in S3.
2. Serialize every discovered artifact and message using the real JSON encoder.
   Measure empty, one-item, latest-run, normal synthetic, and configured-boundary
   bytes.
3. Compare measurements against current AWS service quotas retrieved from
   authoritative documentation or the configured account; do not hard-code a
   remembered quota into the final checklist.
4. With approval, write sanitized objects only under
   `learning/payload-probe/{probeId}/`, read them back, inspect metadata, and test
   deterministic conditional-write success plus conflict. Send only a synthetic
   reference message through the learning queue.
5. Verify compression is unnecessary for SQS envelopes and document whether any
   S3 artifact benefits from compression without weakening direct validation.

**Acceptance evidence:** Versioned message fixtures, an encoded-size table,
conditional-write observations, and production queue/object size alarms and
rejection thresholds.

### PD-11 — Neon publication and coordinator requirements

**Purpose:** Discover the exact database changes and transaction boundaries
required without treating write order as atomicity.

**Probe:**

1. Trace migrations and current repository transactions for query validation,
   `Shop`/`RunStore` checkpoints, profile claims/reuse, `saveLeadBatch()`, user
   grants, traffic caches/publication, score finalization, completion, leases,
   cancellation, and safe failure.
2. Run the guarded integration suite in an isolated schema and reproduce the
   known unqualified raw-SQL issue in `grantRunShopsToOwner()` if still present.
3. Measure current bulk operations at the verified 61-lead/52-eligible shape and
   identify database parameter, statement, transaction-duration, and connection
   requirements.
4. Specify the minimal coordinator migration, uniqueness constraints, indexes,
   stage/task compare-and-swap statements, first-terminal counter update,
   zero-count advancement, artifact fingerprint reconciliation, and stale-owner
   fence.
5. Prove proposed transaction semantics with an isolated disposable schema or
   database-level prototype before making them an implementation-window
   acceptance contract. Do not apply a production migration during discovery.

**Acceptance evidence:** A schema/migration requirement report, transaction
boundary map, measured bulk limits, and deterministic database proofs for
duplicate terminal recording, conflicting replay, lease expiry, stale publish,
and one aggregation owner.

### PD-12 — Durable failure and recovery lifecycle

**Purpose:** Ensure the final checklist assigns every failure gap between SQS,
S3, Neon, and the next dispatch instead of assuming the happy-path order is
atomic.

**Probe:** Build a lifecycle table for every worker and aggregator covering:

- failure before external work;
- external success with lost response or local timeout;
- failure before S3 write, during write, and after successful write;
- conditional S3 conflict;
- failure before and after the first Neon terminal commit;
- failure before aggregation-check send and before SQS acknowledgement;
- duplicate, delayed, and reversed delivery;
- Lambda timeout, process death, task lease expiry, and aggregator lease expiry;
- partial SQS batch failure;
- zero expected tasks and all-reused work;
- cancellation during every stage;
- DLQ arrival and operator recovery; and
- final publication failure before and after `resultsAvailable` changes.

For each boundary, record durable state, safe retry action, deduplication key,
fence, whether an external call may repeat, terminal/user-visible state, alarm,
and owning future implementation window.

**Acceptance evidence:** No state transition relies on queue emptiness, S3 event
count, process memory, or an unfenced late writer. Any unavoidable provider
ambiguity is explicit rather than reported as success.

### PD-13 — Lambda runtime, package, and connectivity probe

**Purpose:** Prevent a correct local contract from failing because of Lambda
runtime, bundle, credential, or network assumptions.

**Local probe:**

1. Inventory the transitive runtime dependencies for query, lead, traffic, and
   aggregator handlers; exclude dev/test files and credentials.
2. Measure uncompressed and packaged sizes, module initialization time, peak
   memory on representative fixtures, temporary storage needs, and each bounded
   unit's duration.
3. Verify Node.js 24 compatibility, Prisma generation/runtime requirements,
   Neon serverless adapter behavior, Google auth material loading, and absence of
   filesystem persistence assumptions.

**Controlled AWS sandbox probe requiring approval:** Deploy or temporarily adapt
only a learning-scoped function to process sanitized fixtures, write under
`learning/payload-probe/`, and establish outbound DNS/TLS connectivity. Do not
install production secrets or call paid endpoints. Record cold/warm duration,
memory, logs, SQS event shape, partial-batch response, and cleanup, then restore
the learning trigger/code if it was changed.

**Acceptance evidence:** Runtime/package measurements and a list of exact Lambda
layers, environment names, secret references, IAM actions, network access, timeouts,
and memory settings that the final checklist must implement or validate.

### PD-14 — Probe consolidation and planning-readiness gate

**Purpose:** Convert probe evidence into one contradiction-free basis for the
file-level subagent checklist.

**Probe consolidation:**

1. Validate every retained fixture through its strict parser and every negative
   fixture through the expected typed failure.
2. Run the backend focused/full tests appropriate to inspected contracts,
   database integration tests when configured, secret scan, and diff hygiene.
3. Reconcile the report with the target-flow, AWS-direction, and preliminary-plan
   documents. Correct contradictions before writing implementation windows.
4. List all remaining unknowns, distinguish deferred live acceptance from local
   deterministic acceptance, and identify the exact owner of each future
   invariant.

The final implementation checklist is ready only when all applicable answers are
yes:

- Is every task/message/artifact/database-publication boundary exact and
  versioned?
- Can every external consumed field be traced to sanitized observed evidence?
- Are identity, ownership, history, reuse, and privacy rules preserved?
- Are normal and boundary payload sizes measured?
- Are Browserless interface, concurrency, time, retry, unit, and diagnostic
  contracts fixed?
- Are DataForSEO and BigQuery batch/cost gates fixed?
- Are transaction, idempotency, fencing, cancellation, and recovery lifecycles
  complete?
- Are AWS live prerequisites separated from local deterministic tests?
- Can every implementation invariant be assigned to one stable execution window
  with exact file ownership and acceptance evidence?
- Could all future boxes be checked while an end-to-end invariant still fails?

If the answer to the last question is yes, or any earlier required answer is no,
the parent revises the evidence or contract before assigning Window G1.

## Payload discovery completion record

PD-00 through PD-14 completed on 11 August 2026. The sanitized evidence report is
`email_scraper/docs/research/LAMBDA_SQS_S3_PAYLOAD_DISCOVERY_REPORT.md`; versioned
fixtures are under `email_scraper/test/fixtures/aws-pipeline/v1/`.

The evidence was sufficient to create the final file-level parent-agent checklist.
That checklist now exists at
`FINAL_LAMBDA_SQS_S3_MIGRATION_EXECUTION_PLAN.md` and is the only document from
which implementation windows may be assigned.

The final checklist splits the three discovered readiness blockers across
coherent Windows G1–G3, as required by the parent-agent window-sizing rule:

1. restore `expiresAt` enforcement in the progressive DataForSEO and both-CrUX
   reuse path;
2. select the configured Neon schema before `grantRunShopsToOwner()` raw SQL and
   make the guarded integration suite fully green; and
3. establish independent Node 24 packaging in G3, remeasure every completed
   handler in its owning window, and prohibit G14 from choosing ZIP/layer,
   memory, or timeout settings until the final measurements pass.

The completed probe does not authorize production AWS resources, a production
database migration, or deployment secrets. The learning Lambda was temporarily
adapted for one credential-free egress check and restored byte-for-byte to its
original 598-byte ZIP.
