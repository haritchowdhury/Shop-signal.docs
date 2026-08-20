# G-R22/G-R23 Deferred G-R20 Acceptance Corrections

## Status and authority

Status: **DECISION-COMPLETE / READY FOR FUTURE ASSIGNMENT / NOT CURRENTLY
AUTHORIZED**.

This file is the implementation specification for the two acceptance gaps left
by G-R20 and explicitly preserved by G-R21. It contains no live execution
status. `ACTIVE_EXECUTION_STATE.md` remains the sole authority for execution;
an agent must not edit source from this specification until that file names
this file by exact SHA-256, authorizes the applicable window, and permits the
required local source and test actions.

The four authority artifacts for a future assignment are:

1. product contract: `AWS_ASYNC_DEPLOYMENT_DIRECTION.md`;
2. implementation specification: this file;
3. live authority: `ACTIVE_EXECUTION_STATE.md`; and
4. evidence destination: `AWS_PIPELINE_EXECUTION_EVIDENCE.md`.

The intended future local sequence is `[G-R22, G-R23]`, in that order, with
continuous advancement after G-R22 passes and a stop after G-R23 for independent
review and a separate deployment decision. This sentence records the intended
packet; it grants no current execution or deployment authority.

## Source-grounded finding

G-R20 implemented the set-based and bounded-concurrency paths, but two
acceptance gaps remain:

1. The isolated PostgreSQL suite passed 37/38. The 1,000-domain,
   12,000-work-outcome final publication reached `before_run_visibility` at
   13.995 seconds and then exceeded the fixed 15-second interactive-transaction
   timeout. The same test passed alone, so the implementation has no reliable
   suite-level margin. The tail currently re-locks and rereads the stage through
   `completeAggregatorInTransaction()`, performs a count-only Run update, and
   then rereads both the Run and PipelineStage solely to construct the return
   object.
2. The production paths for G-R20 T3 through T6 exist, but their required
   decisive corpora do not. Current tests do not prove the 52-domain traffic
   phase barriers/concurrency, the aggregator max-eight and ten-GET
   memoization rule, 1,000-message SQS concurrency/contract behavior, or the
   two-wide ten-scope DataForSEO wave/cost/restart rules.

The product decisions remain unchanged: the final publication transaction has
`maxWait: 5_000` and `timeout: 15_000`; S3 concurrency is eight; task settlement
is four; SQS batch-call concurrency is four; DataForSEO scope concurrency is
two; DataForSEO remains at most ten bulk calls for a fully uncached run; and no
timeout, Lambda, provider, artifact, message, schema, or visibility contract is
changed.

---

## G-R22 — deterministic final-publication tail and transaction margin

### Window header

ID: `G-R22`

Objective: make the existing maximum final-publication corpus reliable under
the locked 15-second transaction timeout by removing redundant fenced
completion/tail database round trips. Do not reduce the corpus and do not raise
or bypass the timeout.

Depends on: completed G-R21; current G-R20 set-based publication code; Prisma
Client 6.19.3 support for `updateManyAndReturn()` on PostgreSQL; the unchanged
final-publication and coordinator contracts.

Consumes exact outputs:

- the `owned = assertCompleteAggregatorInTransaction(...)` result acquired at
  the start of `publishAwsFinalResults()`;
- the existing `resultFingerprint`, `leadSummary`, `trafficSummary`,
  `scoringVersion`, `now`, stage ID, generation, and aggregation token; and
- the existing G-R8 rollback corpus and G-R20 1,000-domain/12,000-outcome
  isolated-PostgreSQL corpus.

Produces exact outputs:

- the same `{ run, stage, resultFingerprint }` return shape populated from the
  two conditional update-return rows;
- the same final durable states and final visibility ordering;
- no stage/Run reread after the visibility write; and
- reliable maximum-corpus evidence with explicit timing headroom.

Owned files/symbols:

- `email_scraper/src/prisma-run-repository.js` — only the final stage-completion
  and Run-publication tail inside `PrismaRunRepository.publishAwsFinalResults()`;
- `email_scraper/test/aws-pipeline-final.integration.test.js` — only the G-R8
  rollback assertions and G-R20 maximum publication corpus; and
- completion records in `AWS_PIPELINE_EXECUTION_EVIDENCE.md` and, only when a
  future active state authorizes G-R22, the prescribed state transition in
  `ACTIVE_EXECUTION_STATE.md`.

Shared-file permissions: preserve all unrelated dirty changes. Do not modify
`completeAggregatorInTransaction()` or any of its other callers. Do not stage,
commit, restore, reset, or rewrite history.

Non-goals/prohibited actions:

- no schema/migration, public signature, transaction boundary, `afterStep`
  name/order, fingerprint, identity, ownership, message/artifact, provider,
  cache, scoring, grant, diagnostic, result-visibility, or return-shape change;
- no timeout increase, corpus reduction, skipped timing assertion, retry around
  the transaction, nested transaction, unsafe SQL, or weaker CAS predicate;
- no frontend, infrastructure, Lambda setting, AWS, provider, production
  database, live-run, secret, destructive, staging, or commit action.

### G-R22-T1 — return the already-fenced stage update

Source: the call to `completeAggregatorInTransaction()` immediately after
`resultFingerprint` is computed in `publishAwsFinalResults()`.

Prescribed change:

1. Keep the initial `assertCompleteAggregatorInTransaction()` call exactly
   where it is. Its returned `owned.run` and `owned.stage` are selected and
   locked by the same interactive transaction before any final writes.
2. Keep every write and every `afterStep` before stage completion unchanged.
3. Replace only this function's final call to
   `completeAggregatorInTransaction()` with one
   `transaction.pipelineStage.updateManyAndReturn()` call.
4. Its `where` predicate is exactly:
   - `id === input.stageId`;
   - `runId === input.runId`;
   - `generation === input.generation`;
   - `state === "aggregating"`;
   - `aggregationLeaseToken === input.aggregationToken`; and
   - `aggregationLeaseExpiresAt > now`.
5. Its `data` is exactly the accepted completion write:
   `state="completed"`, `safeErrorCode=null`, `safeErrorMessage=null`, and
   `completedAt=now`. Do not clear the accepted aggregation audit fields.
6. Require the returned array length to be exactly one. Otherwise throw
   `PipelineInvariantError("PIPELINE_INPUT_CONFLICT")`.
7. Bind that sole row as `completedStage`; it is the stage returned to the
   caller after publication. Do not reread it.
8. Call `afterStep("stage_completed")` exactly after the update-return row is
   validated, followed by `afterStep("before_run_visibility")` exactly as now.

Why the reduced check is safe: the initial coordinator assertion has already
locked both Run and PipelineStage and proved the active AWS Run, generation,
terminal task set, aggregation token/expiry, and absence of a live traffic Run
lease. No code in this transaction changes those facts before this update. The
update repeats the mutable stage fence; a concurrent transaction cannot change
the locked rows before commit.

Failure/replay: an update returning zero/multiple rows aborts the entire
transaction. An exception at either retained `afterStep` rolls back the stage
update. Retry reacquires and reproves the complete fence through the unchanged
initial assertion.

Named assertion: extend the existing G-R8 rollback test to assert that every
failpoint still leaves the stage `aggregating`, the Run private/running, and no
grants/traffic publication. The successful pass must return the exact durable
completed stage row.

Mechanical trace:

```text
initial locked owned.stage -> conditional updateManyAndReturn
-> exactly one completedStage -> stage_completed failpoint
-> before_run_visibility failpoint -> G-R22-T2
```

### G-R22-T2 — make the visibility-last Run CAS return its row

Source: the final `transaction.run.updateMany()` plus the two following
`findUnique()` calls in `publishAwsFinalResults()`.

Prescribed change:

1. Replace the final `run.updateMany()` with
   `run.updateManyAndReturn()`.
2. Preserve its `where` predicate byte-for-behavior:
   `id=input.runId`, `state="running"`, `executionBackend="aws"`,
   `pipelineGeneration=input.generation`, and `resultsAvailable=false`.
3. Preserve the complete existing update data without additions or omissions:
   completed state/phase/stage/timestamp, `resultsAvailable=true`, lead and
   traffic summaries, pipeline/scoring versions, result fingerprint, cleared
   safe error, and cleared Run lease fields.
4. Require exactly one returned row; otherwise throw
   `PipelineInvariantError("PIPELINE_INPUT_CONFLICT")` so all prior writes roll
   back.
5. Return exactly
   `{ run: completedRuns[0], stage: completedStage, resultFingerprint }`.
6. Delete only the final Run and PipelineStage `findUnique()` calls. No database
   call may occur after the final Run update-return call.

Failure/replay: the Run update remains the last durable write and the only
public visibility transition. A failed CAS rolls back the stage and every
private write. A process loss after commit is reconciled by the existing
terminal/recovery path; this window adds no retry or alternate publication.

Named assertions in
`email_scraper/test/aws-pipeline-final.integration.test.js`:

- the returned Run has `state="completed"` and `resultsAvailable=true`;
- the returned stage has `state="completed"` and the same ID/token audit fields
  as the persisted row;
- `resultsAvailable` observed from the independent base client during
  `before_run_visibility` is false;
- every retained rollback failpoint leaves it false;
- the persisted Run and stage equal the returned terminal state after commit;
- all existing 12,000 traffic-work, 1,000 lead-work, scoring, grant, and
  fingerprint cardinalities remain exact; and
- the measured interval from immediately before `publishAwsFinalResults()` to
  its resolution is **less than 13,500 ms**. This supplies 1,500 ms of explicit
  headroom; do not weaken it to merely `<15000`.

Mechanical trace:

```text
before_run_visibility proves private -> conditional Run updateManyAndReturn
-> exactly one completed Run -> return completed Run + completedStage
-> existing owner-scoped result readers
```

### G-R22 transaction and interface ledger

| Category | Locked choice | Evidence | Decisive assertion |
|---|---|---|---|
| Interface | Existing `publishAwsFinalResults(input, now, {afterStep})` and return shape | Current callers/tests | Existing caller tests plus exact returned terminal rows |
| Persistence | No field/schema change | Prisma schema and current writes | No migration/diff outside owned files |
| Atomicity | One existing interactive transaction, `maxWait=5000`, `timeout=15000` | Current source | All failpoints roll back; visibility write remains last |
| Identity/authorization | Existing Run/generation/stage/token fences | Initial locked assertion plus repeated CAS fields | Wrong/stale fence returns no row and aborts |
| External calls | None | Repository path is database-only | No network/provider fake invoked |
| Configuration | No new read; fixed existing timeout | Current source | Literal 15,000 remains |
| Database isolation | Shared isolated-Postgres harness, direct non-production URL, disposable non-`public` schema | Existing G-R20 test | `current_schema()` and schema-local migration checks pass; `finally` cleanup |
| Visibility/privacy | Run update-return is final durable/public transition | Current order | independent read is false before it; true only after commit |
| Build/package | Source enters deployed Lambdas; no dependency closure change | Existing build pipeline | all seven emitted ZIP checks pass |

### G-R22 verification and acceptance

Run from `email_scraper/` with the already verified isolated test transport:

```text
ALLOW_DATABASE_TESTS=true node -r dotenv/config --test --test-concurrency=1 test/aws-pipeline-final.integration.test.js
ALLOW_DATABASE_TESTS=true node -r dotenv/config --test --test-concurrency=1 test/aws-pipeline-final.integration.test.js
ALLOW_DATABASE_TESTS=true node -r dotenv/config --test --test-concurrency=1 test/aws-pipeline-final.integration.test.js
ALLOW_DATABASE_TESTS=true npm run test:integration
npm test
npm run build:lambda
npm run measure:lambda
node --test test/aws-pipeline-packaging.test.js
npm run check:secrets
git diff --check
```

Acceptance requires all three consecutive focused executions and the full
integration suite to pass, every maximum-corpus duration to be below 13,500 ms,
all rollback/visibility/cardinality assertions to pass, no final tail read to
remain, all seven final emitted packages to pass, and no external action. On a
future authorized continuous sequence, append complete evidence and advance
directly to G-R23. A routine test defect is corrected inside G-R22. Stop only
if the verified direct isolated transport is unavailable or source evidence
contradicts a locked behavior not resolved above.

---

## G-R23 — complete G-R20 T3–T6 behavioral proof

### Window header

ID: `G-R23`

Objective: add the missing decisive tests for the already implemented G-R20
T3–T6 algorithms and correct only a test-proven scheduling deviation from
those locked algorithms. This window does not redesign them.

Depends on: accepted G-R22; G-R20 Sections 18.2 and 18.5–18.8; the current
shared `mapWithConcurrency()` implementation and its passing unit corpus.

Consumes exact outputs:

- `processTrafficBatch()` with S3 limit eight and terminal-chain limit four;
- `processDomainAggregation()`, `processLeadAggregation()`, and
  `processFinalAggregation()` with S3 limit eight and deterministic barriers;
- `SqsDispatcher.sendMany()` with ten-entry chunks and four concurrent batch
  sends;
- `enrichDataForSeoSource()` with the fixed ten-scope snapshot and two-scope
  waves; and
- the real isolated PostgreSQL `claimAwsTrafficWorkBatch()` implementation.

Produces exact outputs:

- one decisive T3 traffic corpus including a real 52-domain claim path;
- one decisive T4 corpus for all three aggregators and ten shared DataForSEO
  batch reads;
- one decisive T5 SQS size/concurrency/contract matrix through 1,000 messages;
- one decisive T6 ten-scope cost/restart/wave corpus; and
- full regression, database, recovery, package, and privacy evidence.

Owned production files/symbols, only when a new decisive test proves a mismatch:

- `email_scraper/src/aws-pipeline/services/traffic-worker.js` — only the T3
  read/source-write/combined-write/terminal phase scheduler;
- `email_scraper/src/aws-pipeline/services/domain-aggregator.js`,
  `lead-aggregator.js`, and `final-aggregator.js` — only T4 bounded artifact
  scheduling and DataForSEO batch-key memoization;
- `email_scraper/src/aws-pipeline/adapters/queue-dispatcher.js` — only
  `SqsDispatcher.sendMany()` T5 chunk scheduling/reconciliation;
- `email_scraper/src/enrichment/orchestrator.js` — only
  `enrichDataForSeoSource()` T6 two-scope waves; and
- `email_scraper/src/aws-pipeline/core/bounded-concurrency.js` only if its
  existing contract test itself exposes a helper defect. Its signature and
  contract may not change.

Owned tests:

- `email_scraper/test/aws-pipeline-traffic.test.js`;
- `email_scraper/test/aws-pipeline-traffic.integration.test.js`;
- `email_scraper/test/aws-pipeline-domain.test.js`;
- `email_scraper/test/aws-pipeline-lead-aggregation.test.js`;
- `email_scraper/test/aws-pipeline-final.test.js`;
- `email_scraper/test/aws-pipeline-runtime-adapters.test.js`;
- `email_scraper/test/traffic-orchestration.test.js`; and
- the existing bounded-concurrency test as a required unchanged-contract
  regression.

Non-goals/prohibited actions:

- no schema/migration, public/cross-module signature, message/artifact/key,
  fingerprint/timestamp, provider adapter/request, paid-ledger, cost formula,
  identity, lease/fence, timeout, config snapshot, infrastructure, or frontend
  change;
- no per-domain DataForSEO request, per-domain BigQuery query, unbounded
  `Promise.all`, sleep-based timing test, live provider call, or weaker failure
  assertion;
- no AWS, deployment, production database, live-run, secret, destructive,
  staging, or commit action.

### Shared deterministic delayed-fake protocol

Every concurrency test must use deferred promises controlled by the test, not
wall-clock sleeps. A private test helper records `started`, `inFlight`,
`maxInFlight`, `completed`, item index, and phase. It exposes one deferred gate
per operation. The test waits until the prescribed number of operations has
started, asserts the maximum and that no later-phase event exists, then releases
gates in forward or reverse index order. Each corpus must prove both
`maxInFlight === lockedLimit` and `maxInFlight > 1` when at least that many
items exist. Output comparison uses `canonicalJson()` or exact deep equality;
completion order must never alter bytes or positional results.

### G-R23-T3 — 52-domain traffic phase and recovery matrix

Target tests: `aws-pipeline-traffic.test.js` and
`aws-pipeline-traffic.integration.test.js`.

Build one deterministic 52-domain stage from the existing valid domain
manifest/work-plan/lead fixtures by replacing only stable identity, Shop ID,
RunStore ID, lead ID, task ID, and deterministic keys/fingerprints per ordinal.
Enable all ten DataForSEO scopes plus CrUX REST and BigQuery.

The unit-service corpus must execute these exact cases:

1. **Read barrier/concurrency:** make at least 52 optional artifact reads
   missing. Hold the first eight; assert eight and only eight are in flight and
   zero provider/source-write/combined-write/terminal/check events exist.
   Release all reads, including reverse completion, before provider events.
2. **Source-write barrier:** hold at least eight immutable source writes; assert
   max eight and zero combined writes/terminals/checks until every source write
   settles.
3. **Combined-write barrier:** hold at least eight combined writes; assert max
   eight and zero task-terminal/check events until every combined write
   settles.
4. **Settlement chains:** hold `recordTerminal()` for the first four owned
   tasks; assert exactly four claim/terminal chains are active, later chains
   have not started, and `monitor.assertActive()` occurred immediately before
   both claim-chain entry and terminal write. Release in reverse order and
   require 52 positional task results in input-task order.
5. **Final ordering:** require lease monitor stop/release after the terminal
   phase and exactly one aggregation check only when at least one task became
   terminal.
6. **Read failure:** reject one optional read; started reads may drain, but
   provider/source/combined/terminal/check counts remain zero. Replay after
   restoring the read succeeds.
7. **Source-write failure:** reject one source write; no combined write,
   terminal, or check starts. Replay revalidates completed immutable writes and
   does not repeat a succeeded/ambiguous DataForSEO ledger or uncertain CrUX
   attempt.
8. **Combined-write failure:** reject one combined write; no terminal starts
   for that item and no terminal phase begins until the entire combined phase
   has settled/rejected. Replay consumes the validated source artifacts.
9. **Terminal failure:** reject one fenced terminal write after its combined
   artifact exists; replay validates that combined artifact and performs no
   provider call or new S3 write for that item before terminalizing it.
10. **Reverse completion:** run the successful corpus with forward and reverse
    gate release and require byte-identical source/combined artifacts, identical
    sorted results, the same terminal cardinality, and the same provider-call
    ceilings: ten DataForSEO bulk calls, at most 52 REST calls, one table-list,
    one dry run, and one live bounded BigQuery query.

The real-PostgreSQL corpus must seed a live AWS Run/generation, traffic stage,
stage-wide Run lease, 52 PipelineTasks, 52 Shops, and every required ShopWork
row in one verified disposable schema. Invoke `processTrafficBatch()` with the
real bound `PrismaRunRepository.claimAwsTrafficWorkBatch()` method; other
network/S3/coordinator seams remain deterministic fakes. Assert all 52 domains
flow through that method, every returned claim is positional and owned or
reconciled as seeded, no row is stolen, replay is idempotent, and provider
ceilings remain run-wide. Using a mocked claim method in this case is forbidden.

Prescribed production correction if and only if a case fails: restore the
exact G-R20 order `all optional reads -> providers -> all source writes -> all
combined writes -> all owned claimTask/recordTerminal chains -> lease release
-> one check` with `mapWithConcurrency` limits 8/8/8/4. Do not change any
failure semantic, adapter, artifact, or provider protocol.

Mechanical trace:

```text
52 traffic triggers -> one stage-wide owner -> real/bounded claims
-> reads(8) -> unchanged run-wide providers -> source writes(8)
-> combined writes(8) -> fenced terminal chains(4) -> one check
```

### G-R23-T4 — aggregator barriers and ten-key memoization

Target tests: `aws-pipeline-domain.test.js`,
`aws-pipeline-lead-aggregation.test.js`, and `aws-pipeline-final.test.js`.

Add these exact delayed-fake cases:

1. **Domain aggregator:** 52 terminal query artifacts. Hold the first eight
   reads and prove max eight/overlap and zero candidate writes/checkpoint.
   After all reads validate, hold candidate writes and prove max eight and zero
   domain-manifest write/checkpoint. Only after every candidate write settles
   may the single domain manifest be written and the Neon checkpoint/dispatch
   occur. Reverse read/write completion must produce canonical-identical
   manifest, tasks, and dispatch items. One read or candidate-write rejection
   must prevent manifest/checkpoint/dispatch.
2. **Lead aggregator:** 52 terminal lead artifacts. Prove max-eight reads,
   actual overlap, no profile/reuse/checkpoint operation before all reads, and
   canonical-identical checkpoint input under reverse completion. Any read
   rejection prevents checkpoint and next-stage registration.
3. **Final aggregator:** 52 domains, each referencing all ten DataForSEO scopes
   and independent CrUX REST/BigQuery source artifacts. Create exactly ten
   shared DataForSEO batch keys—one key per scope—and make all 52 references to
   a scope identical in batch ID, scope, request fingerprint, target count,
   artifact fingerprint, and expected envelope. Prove max-eight combined,
   source, unique-batch, and lead reads; prove every read barrier completes
   before `publishAwsFinalResults()`; and assert exactly ten batch GETs, not
   520. Validate membership for every one of the 520 domain/scope references.
4. Mutate each duplicate-reference field one at a time; each mismatch must
   throw `PIPELINE_INPUT_CONFLICT` before any GET for that conflicting batch
   key and before publication. Missing/corrupt/conflicting GET outcomes retain
   their exact strict error and prevent publication.
5. Forward and reverse gate release must produce identical cache rows, traffic
   rows, work outcomes, ledger evidence, summaries, fingerprints, and
   publication input.

Prescribed production correction if and only if a case fails: use the existing
`mapWithConcurrency(..., 8, ...)` at the named phase, await the whole phase
before the next, assemble by original deterministic key order, and collect and
strictly compare all duplicate batch metadata before one memoized GET per key.
No parser or error mapping changes are permitted.

Mechanical trace:

```text
terminal artifact sets -> bounded validated reads(8)
-> deterministic in-memory assembly -> bounded immutable writes where applicable
-> one manifest/checkpoint/publication; ten shared batch keys -> ten GETs
```

### G-R23-T5 — SQS 0/1/10/11/40/41/1,000 matrix

Target test: `aws-pipeline-runtime-adapters.test.js`.

For each size `0, 1, 10, 11, 40, 41, 1000`, build strict valid messages with
unique deterministic logical IDs and call `SqsDispatcher.sendMany()`.

Required assertions:

- zero messages performs zero SDK calls and returns three empty arrays;
- every nonempty case uses `ceil(size/10)` calls, chunks of exactly ten except
  the final remainder, and entry IDs `m0000` through the last global ordinal;
- for 41 and 1,000, hold the first four SDK calls and prove maximum four and
  actual overlap; no fifth call starts until a gate is released;
- release chunk gates in reverse order and require `results`, `sentItemIds`, and
  `failedItemIds` in original message-index order;
- reject one SDK chunk and require every member of only that chunk to be
  failed while successful chunks remain sent;
- independently return duplicate, missing, and unknown response IDs and require
  `PipelineContractError("PIPELINE_MESSAGE_INVALID")` after already-started
  calls drain; do not synthesize success/failure for the malformed response;
- include duplicate logical item IDs in different positions and prove the
  positional array preserves both occurrences; and
- insert one invalid input message at the first, middle, and last positions;
  each call must fail strict parsing before any SDK call.

Prescribed production correction if and only if a case fails: retain parse-all
before I/O, ten-entry ordered chunks, `mapWithConcurrency(chunks,4,mapper)`,
exact response-ID set equality, per-chunk rejection mapping, and final sort by
original index. No message schema, return shape, or recovery behavior changes.

Mechanical trace:

```text
strict messages -> parse all -> ordered chunks of ten
-> at most four SDK calls -> exact response-ID reconciliation
-> original-index positional result -> durable dispatch recovery
```

### G-R23-T6 — ten-scope DataForSEO wave/cost/restart corpus

Target test: `traffic-orchestration.test.js`, using exported
`enrichDataForSeoSource()` or the existing `enrichTraffic()` caller without
changing a production signature.

Use 52 unique canonical hostnames and the exact durable scope order:
worldwide, US, GB, CA, AU, NZ, DE, FR, IN, AE. Every scope is nonempty and each
fake provider response contains all 52 targets.

Required cases and assertions:

1. **Successful waves:** record cache read, ShopWork reservation, ledger plan,
   ledger claim, provider start/finish, settlement, and cost read per scope.
   For each wave both claims precede either provider start; hold both provider
   calls and prove max concurrency exactly two and greater than one. Scope three
   must not be planned/claimed until scopes one and two settle and the
   authoritative cost is reread. Repeat for all five waves.
2. Require exactly ten provider calls, one per scope, each with all 52 sorted
   targets; exactly ten distinct stable request fingerprints; one ledger and
   one reservation per scope; results stored in durable scope order despite
   reverse provider completion; and identical normalized output for forward
   and reverse completion.
3. **Budget stop:** return provider-reported cost from the first wave such that
   the authoritative reread exhausts the locked budget. Assert later scopes are
   unavailable with no later ledger plan, claim, reservation, or provider call.
4. **Mixed outcomes:** in one wave let one descriptor succeed and the other
   throw a `zero_cost_proven`/`not_dispatched` error; require the exact failed
   ledger/work settlement only for the latter and continued next-wave planning
   after the cost reread. Repeat with an uncertain error and require ambiguous
   ledger/work settlement and no automatic second call.
5. **Crash/replay:** inject separately after plan-before-claim, after
   claim-before-provider result, and after success settlement. Replay permits
   normal planning only before claim, produces ambiguous/no second paid call
   after uncertain claimed execution, and reuses cache/succeeded ledger after
   settlement. Count calls by request fingerprint and require no fingerprint
   above one.
6. Preserve the 52-domain overall ceilings: DataForSEO exactly ten bulk calls,
   CrUX REST at most 52 with its durable concurrency two, and CrUX BigQuery one
   latest-table lookup, one dry run, and one bounded multi-origin live query.

Prescribed production correction if and only if a case fails: retain ordered
two-scope waves; perform each wave's durable planning/claims in snapshot order;
create a network descriptor only after `networkAllowed===true`; execute
descriptors at concurrency two; settle the entire wave; reread authoritative
cost; then plan the next wave or mark all remaining unclaimed scopes
unavailable. Do not change paid ambiguity or call granularity.

Mechanical trace:

```text
ten durable scopes -> five ordered waves -> sequential durable claims per wave
-> at most two full-batch provider calls -> durable settlement
-> authoritative cost reread -> next wave or deterministic budget stop
```

### G-R23 decision audit

| Category | Locked choice | Evidence | Decisive assertion |
|---|---|---|---|
| Files/symbols | Exact seven source symbols and seven test files named above | Current reachable call set | Diff contains no other production symbol |
| Interfaces/dependencies | No public signature/dependency change | G-R20 interface ledger | Existing callers and strict return assertions pass |
| Schema/persistence | No schema/migration; existing ledgers/work/tasks only | Prisma schema/current source | No migration; real 52-domain claim rows reconcile |
| Transactions | Existing repository transactions unchanged | G-R20 | Real claim test and full integration pass |
| Identity/authorization | Existing Run/stage/task/ShopWork fences | Current services | wrong/busy/replay cases retain outcomes |
| Messages/artifacts | Existing strict schemas, keys, fingerprints, timestamps | v1 fixtures/current code | reverse bytes equal; malformed/missing/conflict fail closed |
| External calls/cost | Fake only; bulk DFS max ten/two concurrent; REST 52/two; BQ 1/1/1 | Locked contract | exact fake call counters and request contents |
| Failure/recovery | Phase rejection stops later phases; immutable/durable replay | G-R20 T3–T6 | named failure/replay cases make no duplicate uncertain call |
| Configuration/limits | Literal 8/4/4/2; fixed durable scopes | Current code | actual-overlap maximum assertions |
| DB isolation | shared direct disposable-schema harness | existing helper | non-production/current-schema/migration/cleanup checks |
| Build/package | unchanged Node 24 production closure | existing seven-package build | build, measure, cold import, engine, deterministic checks |
| Visibility/privacy | no publication until reads validate; no raw/private fixture material | final aggregator/log rules | failed reads never publish; secret scan passes |
| Cross-window output | G-R22 stable transaction is prerequisite; G-R23 yields complete G-R20 local evidence | this sequence | full DB/recovery/backend/package corpus passes |

### G-R23 adversarial verification and acceptance

Run from `email_scraper/`:

```text
node --test test/aws-pipeline-bounded-concurrency.test.js test/aws-pipeline-traffic.test.js test/aws-pipeline-domain.test.js test/aws-pipeline-lead-aggregation.test.js test/aws-pipeline-final.test.js test/aws-pipeline-runtime-adapters.test.js test/traffic-orchestration.test.js
ALLOW_DATABASE_TESTS=true node -r dotenv/config --test --test-concurrency=1 test/aws-pipeline-traffic.integration.test.js test/aws-pipeline-final.integration.test.js
ALLOW_DATABASE_TESTS=true npm run test:integration
npm test
npm run build:lambda
npm run measure:lambda
node --test test/aws-pipeline-packaging.test.js
npm run check:secrets
git diff --check
```

Also rerun the existing 16-boundary G-R9 recovery command named in the frozen
execution specification/evidence; record its exact command and outcome rather
than replacing it with a summary.

Acceptance requires every named T3–T6 case above, not merely green commands;
real 52-domain traffic claims; actual observed maxima S3=8, terminal=4,
SQS=4, DataForSEO=2; exact final batch GET count 10; exact 1,000-message chunk
cardinality 100; DataForSEO max ten non-domain calls; preserved REST/BigQuery
ceilings; deterministic reverse completion; strict failure barriers and replay;
full G-R22 maximum publication; full DB/backend/recovery/package/privacy checks;
and zero AWS/provider/production/frontend/infrastructure action.

On a future authorized sequence, append evidence including changed files,
commands/results, maximum concurrency observations, exact call/GET/chunk
counts, skipped checks/reasons, residual risks, external actions (`none`), and
preserved dirty work. Then transition the active state to completed through
G-R23 and stop for independent review. Do not deploy automatically.

---

## Forward/backward simulation and set closure

Forward simulation:

```text
G-R22 initial locked Run/stage
-> all existing private writes
-> conditional returned stage completion
-> rollback-capable stage_completed/before_visibility hooks
-> conditional returned final Run visibility write
-> completed return with no tail read

G-R23 traffic/aggregator inputs
-> strict validation and durable fences
-> bounded phase work with deterministic barriers
-> immutable artifacts before terminal tasks
-> all validated artifacts before final publication
-> no scheduling change to provider identity, cost, or terminal result
```

At every injected failure, already-started bounded work may settle but no later
phase begins; retry reconstructs from the existing Neon/S3 evidence. The final
Run remains private until the one G-R22 CAS commits.

Backward simulation:

- each returned final Run comes from the exact visibility CAS row;
- each returned stage comes from the exact fenced completion update row;
- each terminal traffic task traces to its validated combined artifact, whose
  source components trace to validated reused/attempt/batch evidence;
- each DataForSEO result traces to one durable scope claim and at most one bulk
  provider call;
- each dispatch result traces to one strict input position and one exact AWS
  batch response ID; and
- each public result traces through the unchanged final fingerprint and atomic
  visibility transaction.

Closed affected set:

```text
final publication tail
traffic S3 read/source-write/combined-write/task-terminal scheduling
domain/lead/final aggregator S3 scheduling and DFS batch memoization
SQS SendMessageBatch scheduling/reconciliation
DataForSEO scope-wave scheduling/cost reconciliation
```

Negative searches found no required schema writer, alternate SQS bulk
dispatcher, alternate final visibility writer, per-domain DataForSEO production
path, alternate BigQuery fan-out, or second affected public interface. Existing
local `completeTrafficEnrichment()` continues to consume the shared scoring
helper but is not touched by either window and remains a regression boundary.

## Preflight Gate Report

```text
BLOCKERS BEFORE START: none
USER ACTIONS BEFORE START: none for the local G-R22/G-R23 sequence
PREDICTABLE FUTURE GATES: F-GR23-DEPLOY — after G-R23 and independent review,
  rebuild and compare all seven content-addressed Lambda ZIP hashes with the
  deployed manifest. Only changed hashes are eligible for a guarded code-only
  deployment; any topology/template/resource change requires a new specification.
PAID/MUTATING APPROVALS NOT YET GRANTED: A-GR23-DEPLOY — separate explicit user
  approval is required for S3 deployment-object upload, CloudFormation change
  set creation/execution, event-source changes, provider calls, or live-run work.
PLANNED USER STOP: after G-R23 local acceptance for independent review and a
  separate deployment decision
```

The local sequence requires the already configured non-production direct
`TEST_DATABASE_URL`. The shared isolation helper must fail closed if it resolves
to production, a pooler, `public`, a mismatched `search_path`, or nonlocal
migration history. This is an environment preflight, not permission to use or
clean production data.

## Assignment packet for a future active state

When the user later authorizes implementation, the parent must first compute
this file's SHA-256 and atomically replace the completed G-R21 state with one
machine-scannable state naming this file and revision, using:

```text
mode: continuous_sequence
authorized_sequence: [G-R22, G-R23]
current_window: G-R22
current_status: READY
accepted_through: G-R19
next_on_pass: G-R23
stop_after: G-R23
allowed_actions: [local_source_edits, local_tests, isolated_test_database_writes, local_documentation]
prohibited_actions: [aws_mutations, deployment, paid_provider_calls, production_database_writes, frontend_edits, infrastructure_changes, destructive_actions, commits]
```

On G-R22 pass, transition to `current_window: G-R23`, `current_status: READY`,
and keep `accepted_through: G-R19` because the T3–T6 half of G-R20 acceptance
is still open. On G-R23 pass, record `current_window: G-R23`,
`current_status: COMPLETED`, `accepted_through: G-R23`, and the declared stop.
G-R21 remains a completed deployment/recovery window in its existing evidence;
these state values do not retroactively claim that its deferred G-R20 gaps were
accepted.

The implementing agent must verify the product-contract and specification
hashes before editing, execute both windows continuously, correct ordinary
implementation/test defects inside the active window when this specification
dictates the behavior, append evidence and transition state at each passing
boundary, and stop only for a genuine blocker or after G-R23. A window boundary
or passing handoff is not a blocker.

## Readiness certificate

Classification: **DECISION-COMPLETE / READY FOR FUTURE ASSIGNMENT**, but **not
active** until the assignment packet above is installed in
`ACTIVE_EXECUTION_STATE.md` under explicit user authorization.

The two windows lock exact files/symbols, interfaces, algorithms, transaction
and recovered boundaries, limits, failure semantics, deterministic tests,
database isolation, package verification, mechanical traces, acceptance, and
the later external gate. No implementation agent must choose architecture,
schema, public API, transaction policy, concurrency, cost behavior, retry
semantics, or acceptance interpretation.
