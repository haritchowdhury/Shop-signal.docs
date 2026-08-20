# KI-W3 Execution Plan — Strict Provider Adapter and Durable Bounded Worker

> **HISTORICAL — DO NOT EXECUTE.** This supplemental plan is superseded in
> full by the `KI-CL-9` `KI-W3` window in
> `KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md` and `DEC-KI-030`. A4 is
> the sole executable task authority; A5 is the sole assignment authority.
> No executor may use this file to fill, narrow, merge, or reinterpret an A4
> requirement.

**Review disposition:** independent review rejected the initial W3 handoff
(`EV-KI-W3-04`). This historical disposition is not mutable assignment status;
only A5 records that. At this plan's current authoring snapshot, A5 state 91
assigns only the requester-reopened KI-R2 proof gate. W3 may resume only after KI-R2 is implemented, evidenced,
independently accepted, and A5 explicitly reopens this same unaccepted window.
**Package:** `KEYWORD_INTELLIGENCE`
**Window:** `KI-W3` (A4 `KI-CL-8`)
**Prepared:** 2026-08-17

This document is the execution plan for the `KI-W3` window of
`KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md` (A4). This document alone
does **not** authorize work. Its former state-85 assignment ended at the
state-86 review boundary and grants no current authority.

Authoritative references: A1 `KEYWORD_INTELLIGENCE_PRODUCT_CONTRACT.md`, A2
`KEYWORD_INTELLIGENCE_DISCOVERY_DOSSIER.md`, A3
`KEYWORD_INTELLIGENCE_DECISION_LEDGER.md`, A4
`KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md`, A5
`ACTIVE_EXECUTION_STATE.md`, A6 `KEYWORD_INTELLIGENCE_EXECUTION_EVIDENCE.md`,
A7 `KEYWORD_INTELLIGENCE_SPECIFICATION_CHANGELOG.md`, A8
`KEYWORD_INTELLIGENCE_TRACEABILITY_INDEX.md`.

---

## 1. Current execution state and gates

| Fact | Value |
|---|---|
| A5 state version | `91` |
| Current window | `KI-R2` |
| Current status | `READY` |
| Accepted through | `KI-R1` |
| `KI-W3` assignment | none; paused pending KI-R2 execution and parent acceptance |
| A1 hash | `8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c` |
| A4 hash | `1da44b03d2726d1691b178b60dcc89a7f17de8ca6dc233359d94165628c6cd65` |
| A1/A4 match A5? | yes at the reopened KI-R2 assignment |
| Backend worktree | clean at `dad2b41802e5b823d64d57fab67aea5a75712b25` (`R2 second attempt`); the three R2-owned files are committed and pushed despite the earlier no-commit claim |
| W2 output | accepted; pure Node modules at `src/keyword-intelligence/*`; parity/selection/query fixtures and tests present |
| W3 payload fixtures | already materialized under `GATE-KI-002` (`EV-KI-A-029`): `dataforseo-{overview,related,suggestions}-cases-v1.json`, `worker-message-cases-v1.json` |

The initial W3 implementation is historical, unaccepted output. Before W3 can
be reopened, KI-R2 must supply and prove `DEC-KI-028`. Reopened W3 must then,
within its original scope: handle lost settlement as lost; reconstruct
post-artifact recovery byte-identically; use task and aggregator lease monitors
with `assertActive` around S3/terminal boundaries; execute full `SCN-KI-012`;
make the keyword build preserve existing `.lambda-build` handlers; merge the
out-of-scope flow test into an owned test and remove that extra file; reconcile
file/path evidence; and rerun every original P/T/V/H oracle. Those repairs are
not authorized during KI-R2.

---

## 2. Window contract (from A4 `KI-CL-8`; dormant until A5 reopens W3)

- **objective:** Complete research durably through bounded provider tasks and
  one fenced publication transaction.
- **depends_on:** `[KI-R1]`
- **consumes:** corrected KI-R1/KI-R2 repository; W2 schemas/calculation;
  `PAY-KI-001`…`PAY-KI-006`; `DEC-KI-026`; `DEC-KI-027`; `DEC-KI-028`
- **produces:** adapter, contracts, service/handler/recovery, artifacts, worker
  component/integration proof
- **assigned_agent_policy:** one_window
- **authorized_write_scope:**
  - `email_scraper/src/aws-pipeline/keyword-intelligence/dataforseo-labs-adapter.js`
  - `email_scraper/src/aws-pipeline/keyword-intelligence/contracts.js`
  - `email_scraper/src/aws-pipeline/keyword-intelligence/keys.js`
  - `email_scraper/src/aws-pipeline/keyword-intelligence/service.js`
  - `email_scraper/src/aws-pipeline/keyword-intelligence/handler.js`
  - `email_scraper/src/aws-pipeline/keyword-intelligence/recovery.js`
  - `email_scraper/test/keyword-intelligence-adapter.test.js`
  - `email_scraper/test/keyword-intelligence-worker.test.js`
  - `email_scraper/test/keyword-intelligence-recovery.test.js`
  - `email_scraper/test/fixtures/keyword-intelligence/dataforseo-overview-cases-v1.json`
  - `email_scraper/test/fixtures/keyword-intelligence/dataforseo-suggestions-cases-v1.json`
  - `email_scraper/test/fixtures/keyword-intelligence/dataforseo-related-cases-v1.json`
  - `email_scraper/test/fixtures/keyword-intelligence/worker-message-cases-v1.json`
  - `email_scraper/scripts/build-keyword-worker.js`
- **shared_file_scope:** fixture directory only for strict payload cases; no W2
  golden overwrite
- **read_only_scope:** existing `aws-pipeline` adapters/contracts/core/handler/
  repository files (full list in the A4 KI-W3 header); all accepted W1/W2/KI-R1/KI-R2 output files;
  historical git blobs named in A2
- **authorized_actions:** `[local_source_edits, local_mocked_tests,
  isolated_test_database_writes, local_build, evidence_updates]`
- **prohibited_actions:** `[provider_calls, AWS_operations,
  production_database_writes, raw_body_restore, API/frontend/schema edits,
  commits]`
- **successor:** `KI-W4` (reserved for parent; `may_start_successor: false`)

---

## 3. Preconditions (P1–P4)

| ID | Requirement | Current status / evidence needed |
|---|---|---|
| `KI-W3-P1` | Assignment/hashes/version match | NOT MET — A5 state 87 assigns KI-R2, not W3. Parent must create a later W3 assignment after KI-R2 acceptance. |
| `KI-W3-P2` | W1/W2/KI-R1 plus accepted KI-R2 outputs and exact revisions exist; `SCN-KI-020`–`022` pass | BLOCKED — KI-R2 is not implemented or accepted. |
| `KI-W3-P3` | Isolated DB, exact `DEC-KI-009` paid-policy snapshot, mocked S3/SQS/provider harnesses available; no live secrets loaded | MUST BE REVERIFIED on the future W3 assignment; no current authority to use it for W3 remediation. |
| `KI-W3-P4` | Dirty state/scope recorded | NOT MET for reopening — future parent assignment must baseline accepted KI-R2 plus committed W3 `f9457de` and its authorized remediation/deletion scope. |

---

## 4. Task T1 — Strict three-endpoint adapter (A4 `KI-W3-T1`)

**Task:** implement strict three-endpoint adapter, normalized cache, attempt
ledger, durable throttle, single-attempt retry scheduler, and safe errors.

**Requirements/decisions:** `REQ-KI-022`, `INV-KI-008`–`009`,
`DEC-KI-007`–`009`, `026`, `PAY-KI-001`–`005`.
**Source:** `KeywordSearchVolume/pipeline/client.py` **only** as behavioral
source; historical evidence blobs/certificates in A2; existing strict adapters
(`adapters/artifact-store.js`, `core/canonical.js`) as patterns.
**Target:** `dataforseo-labs-adapter.js` + `contracts.js` (strict Zod
request/response/normalized schemas) + owned adapter tests/fixtures only.

### 4.1 Public interface (`executeProviderAttempt`)

```
executeProviderAttempt({ task, config, clock, http, repository })
  → { outcome: "cacheHit", normalized }                     // zero provider attempts
  | { outcome: "succeeded", normalized, attempt, providerCostUsd }
  | { outcome: "retryAt", retryAt, attempt, providerCostUsd } // known retryable ≤4
  | { outcome: "failed", code, attempt, providerCostUsd }      // terminal known
  | { outcome: "ambiguous", code }                             // never repeated
  | { outcome: "lost" }                                        // known settlement, stale task fence
```

- `task` is the strict `DEC-KI-026` `WorkerTask` projection, including the
  current `leaseToken`, endpoint/request fingerprints, attempt count, and
  durable createdAt.
- `config` is the immutable `keyword-research-config-v1` snapshot (W2
  `config.js`) carrying `api.baseUrl`, `timeoutSeconds=120`,
  `retry.maxAttempts=4`, `retry.retryableStatus`, `retry.retryableApiCodes`,
  `expansion.*`, `maxCostPerResearchUsd="3.00000000"`.
- `clock` injects `now()`/timeout seams for deterministic scheduling and test
  control; retry jitter is fingerprint-derived, not random.
- `http` injects the fetch/AbortController boundary (native fetch in prod;
  mocked in tests). Exactly **one** timed POST per invocation at most.
- `repository` is the accepted KI-R1 `PrismaKeywordResearchRepository` for
  `claimThrottle`, `deferTask`, `recordAttempt`, atomic `settleAttempt` plus
  success-cache write, `markAttemptAmbiguous`, `scheduleRetry`, and `cacheRead`.

### 4.2 Durable request contract (`PAY-KI-001`, `DEC-KI-009`)

- Request objects are strict Zod; one-element JSON arrays on the wire:
  - suggestion `{keyword:1..100, location_code:int, language_code:string,
    limit:30}`
  - related adds `depth:2`
  - overview `{keywords:string[1..700], location_code:int, language_code:string}`
    (anchor ≤300; remaining markets ≤200 per `DEC-KI-004/006`)
- `canonicalJson` (strict, finite scalars, sorted keys, preserved array order) →
  `requestFingerprint = SHA256(endpointKey + "\n" + canonicalJson)` and
  compatibility `cacheKey = endpointKey + ":" + first24hex(SHA256(canonicalJson))`.
- Reconstructing the request body from durable state (never from the message):
  expansion uses `seeds[itemKeyIndex]` + US anchor (`2840/en`); anchor overview
  uses the expansion-manifest candidate list (≤300); remaining markets use the
  shortlist (≤200). The adapter **verifies** the reconstructed request's
  fingerprint equals `task.requestFingerprint` before any HTTP.
- Local invalid request → `KEYWORD_PROVIDER_REQUEST_INVALID` **before any call**.
- Privacy: only the fingerprint/identity enters SQS/logs; seed/keyword text
  lives only in owner-scoped Neon and encrypted S3 artifacts (`PAY-KI-001`).

### 4.3 Response parsing and classification (`PAY-KI-002…005`)

- Envelope (`PAY-KI-002`): root `status_code`/`status_message`/`tasks`,
  first task `status_code`/`status_message`/`result`. Success discriminator:
  HTTP 200 + root `20000` + exactly one task + task `20000`. Cost is validated
  then consumed; every unconsumed key is stripped by strict Zod objects.
- Normalization:
  - suggestions/related (`PAY-KI-003/004`): `{keywords:string[]}` in provider
    order, trim empty, case-insensitive first-occurrence dedup. **No
    `items[].key` alias**, no direct related `item.keyword`.
  - overview (`PAY-KI-005`): strict `KeywordMarketMetric[]` per consumed item
    paths; missing keyword or nonpositive/null volume yields no usable metric
    exactly as the Python source.
- Error mapping: HTTP 401/root `40100` → `KEYWORD_PROVIDER_AUTH_FAILED`;
  HTTP 429/500/502/503/504 or API `40601/40602/50001/50002/40107` →
  durable retry transition; retry exhausted →
  `KEYWORD_PROVIDER_RETRY_EXHAUSTED`; task failure →
  `KEYWORD_PROVIDER_TASK_FAILED`; malformed/missing/unknown →
  `KEYWORD_PROVIDER_CONTRACT_MISMATCH`; transport/timeout/malformed-after-send,
  or fence loss after the marker with no strict known response →
  `KEYWORD_PROVIDER_AMBIGUOUS`. A strict known response still settles under
  `DEC-KI-026`; fence loss only blocks task publication.
- Never log/persist the envelope; persist only strict normalized output, safe
  codes, cost, and fingerprints.

### 4.4 Cache, ledger, throttle, budget (`DEC-KI-009`, `DEC-KI-008`, `REQ-KI-022`)

- Cache: unique key = full `requestFingerprint`; logical label
  `dataforseo-labs-keyword-v1`, persisted `contractVersion=1`; expiry =
  successful DB time + 604800 s. Fresh
  hit returns `cacheHit` (zero provider attempts, zero new ledger rows). Stale
  misses (never destructively purged). Only a strict normalized success is
  cached through successful `settleAttempt`. Cache existence never grants owner access.
- Ledger: `recordAttempt` from `DEC-KI-026` (pre-call, state `planned`) commits
  the token-fenced attempt-number increment, reservation, and request
  fingerprint before HTTP; `settleAttempt` first-terminalizes known
  (`succeeded|failed`) outcomes after HTTP and **settles the reported
  provider cost for every known response** (success, retryable, terminal),
  replacing the reservation; a success writes/exact-matches the normalized
  cache in that same settlement transaction; ambiguous retains its reservation
  and is never repeated through `markAttemptAmbiguous`.
- Budget: before the pre-call attempt row,
  `sum(settled providerCostUsd) + sum(planned|in-flight|ambiguous reservation) +
  proposedReservation <= 3.00000000`. Otherwise create **no attempt row, zero
  HTTP calls**, terminal fail `KEYWORD_PROVIDER_BUDGET_EXHAUSTED`.
  Reservation formulas: suggestions/related `0.01560000`; overview
  `0.01200000 + 0.00012000×n`. First-pass max `$0.492`; five-attempt max
  `$2.46`; headroom `$0.54`.
- Throttle (`DEC-KI-008`): before any provider call, atomic singleton
  `KeywordProviderThrottle` claim (`provider="dataforseo_labs_keyword"`) with
  ≥2,000 ms DB-time gap. Early/failed claim requeues the same task for the
  whole-second delay through `deferTask` **without incrementing provider
  attempt count** and without HTTP.

### 4.5 Retry and ambiguity (`DEC-KI-007`)

- Max **five** HTTP attempts per logical task (initial + four). One Lambda
  invocation performs at most one attempt.
- Known retryable delay =
  `min(60, 2×2^(attempt-1)) + deterministicJitter`, where
  `deterministicJitter = baseDelay × ((uint32(first8hex(SHA256(taskId + ":" +
  attempt))) mod 2501)/10000)`; SQS delay = `ceil(delay)` whole seconds.
- Known retryable result → settle attempt `failed`, then call
  `scheduleRetry({taskId,token,attemptNumber},now)`; it derives the decided due
  time from the persisted attempt, makes the task pending, stores it, and
  clears the lease before the delayed same-task message is sent.
- Ambiguous → task and research terminal `failed` with the safe ambiguous code;
  **never** automatically repeated.
- A known response always settles its reported cost even after task-fence loss.
  If that lost response is a strict success, its settlement transaction writes
  only the normalized global cache and publishes no task artifact; recovery then completes the reclaimed
  task from cache with zero HTTP calls. A lost known failure is scheduled only
  after recovery reclaims the task.

### 4.6 Adapter deliverable tests (`keyword-intelligence-adapter.test.js`)

- Every payload certificate (`PAY-KI-001…005`) positive/boundary/missing/
  malformed/unknown case from the three already-materialized fixture files;
  exact HTTP/body/header redaction; cache fresh/stale; throttle; each retry code
  and attempt 5; timeout/response-loss/crash positions; exact reservation,
  settlement, ambiguous exposure, and **budget denial with zero calls**.
- **Negative control:** enabling an alias, retry-after-ambiguity, or
  over-budget call must fail.

---

## 5. Task T2 — Worker service/handler/recovery/build (A4 `KI-W3-T2`)

**Task:** strict message/artifact/key contracts and initialize, expansion-task,
anchor-screen-task, market-overview-task, aggregate-check, and recovery service
paths in one handler; a keyword-only `S3ArtifactStore`; a dedicated build
script.

**Requirements/decisions:** `REQ-KI-002`–`005`, `023`, `024`,
`INV-KI-002`–`008`, `DEC-KI-005`, `006`, `018`, `020`, `022`, `026`, `027`.
**Source:** existing AWS contract/handler/service/recovery patterns
(`SRC-KI-016`); repository/adapter/algorithms from W1/W2/T1.
**Target:** `contracts.js`, `keys.js`, `service.js`, `handler.js`,
`recovery.js`, `scripts/build-keyword-worker.js` + owned tests.

### 5.1 Contracts (`contracts.js` — `PAY-KI-006`, `DEC-KI-020`)

- Exactly four SQS discriminators, all strict:
  `keyword.initialize.v1`, `keyword.expansion.task.v1`,
  `keyword.overview.task.v1`, `keyword.aggregate.check.v1`.
- Every shape contains only `contractVersion`, `type`, `researchId`, positive
  `generation`, task/stage identity when applicable, and a 64-lowercase-hex
  input fingerprint. **No** seed, keyword, provider body, result, credential,
  URL, or owner ID.
- Parser errors are per-record `KEYWORD_MESSAGE_CONTRACT_MISMATCH`, never a
  provider call.
- Artifact contracts (`DEC-KI-020`): `keyword-expansion-result-v1`,
  `keyword-expansion-manifest-v1`, `keyword-anchor-screen-result-v1`,
  `keyword-shortlist-manifest-v1`, `keyword-market-overview-result-v1`,
  `keyword-market-overview-manifest-v1`, `keyword-research-result-v1`. Common
  header exactly `{contractVersion, researchId, generation, stage, itemId,
  inputFingerprint, producedAt}`; task artifacts add only normalized output and
  safe status/cost. Content fingerprint = SHA-256 canonical JSON.

### 5.2 Keys (`keys.js`)

- `runs/keyword-research/<researchId>/generation-<g>/<stage>/<itemId>.json`;
  manifests `manifest.json`; final `result.json` (DEC-KI-020).
- Keys are derived from Neon-held identity only — **never supplied by the
  message**. `producedAt` uses the exact `DEC-KI-027` durable source: task
  artifacts use task `createdAt`; candidate/shortlist/market manifests use the
  matching stage `createdAt`; final result uses market-stage `createdAt`.
- Input validation mirrors `core/keys.js` (no `..`, no forbidden substrings).

### 5.3 Service paths (`service.js`)

Ordered boundaries per A4 item 7: contract load → claim/heartbeat → optional
provider via T1 → S3 put → terminal Neon → SQS check → acknowledge. Each
boundary is one invocation; **never more than one HTTP call per invocation**.

| Path | Discriminator | Work |
|---|---|---|
| initialize | `keyword.initialize.v1` | load research row (queued/g1); `repository.initialize` (queued→running; create immutable expansion stage + 2–10 tasks with exact fingerprints); send one `keyword.expansion.task.v1` per task row, then `keyword.aggregate.check.v1` |
| expansion task | `keyword.expansion.task.v1` | load row/config; fingerprint check; `claim`/heartbeat (60 s/20 s); build suggestion/related request from seed + US anchor; T1 attempt; validate/put `keyword-expansion-result-v1` artifact; `terminalize` succeeded/skipped; send check; ack |
| expansion aggregate (check) | `keyword.aggregate.check.v1` stage=expansion | `claimAggregator`; `not_ready` performs no aggregation; validate exact 2–10 US task set + artifacts; build candidate manifest (DEC-KI-005 merge per seed, cap 60, global first-occurrence ≤300); put `keyword-expansion-manifest-v1`; one `publishCandidateManifest` transaction records/completes expansion and creates `anchor_screen` plus one `US:0` task; send task + check |
| anchor-screen task | `keyword.overview.task.v1` itemKey `US:0` | claim; build overview request from candidate manifest (≤300); T1; normalize US metrics, exclude unusable + informational; run preserved dedup/cluster/flag/score with US as sole metric; sort by recommended→opportunity→volume→keyword→itemID; keep `min(200, activeCount)`; validate/put `keyword-anchor-screen-result-v1`; `terminalize` |
| anchor aggregate (check) | `keyword.aggregate.check.v1` stage=anchor_screen | claim aggregator; validate anchor artifact; build shortlist manifest; put `keyword-shortlist-manifest-v1`; `publishShortlist` (complete anchor + atomically create the exact eight remaining-market tasks GB,CA,AU,NZ,DE,FR,IN,AE with shortlist ≤200 each); send eight task messages + check. **Zero usable anchor rows → `failStage` (anchor fails, research fails, no market tasks)** |
| market-overview task | `keyword.overview.task.v1` itemKey `<code>:0` | claim; build overview request from shortlist manifest (≤200); T1; validate/put `keyword-market-overview-result-v1`; `terminalize`; send check |
| market aggregate (check) | `keyword.aggregate.check.v1` stage=market_overview | claim aggregator; validate eight artifacts + reuse US metrics from anchor artifact; rerun nine-market `computeResearchResult` (W2 `pipeline.js`); put market manifest + final `keyword-research-result-v1` (`result.json`); one token-fenced `publishResearchResult` call publishes result, manifest, default selection revision 1, and completed research; send no further work |
| recovery | (recovery Lambda) | call `repository.recover(now)` once; construct initialize/task/check messages solely from returned `RecoveryInitialize`/`RecoveryTask`/`RecoveryCheck`; send all through `runtime.config.awsPipelineKeywordResearchQueueUrl`; **never** invokes a provider |

The service reads research/stage/task rows only through the exact
`DEC-KI-026` context methods and mutates them only through its named public
methods. It never calls a repository transaction escape hatch; owner-scoped
reads are API-only and never used here.

### 5.4 Handler (`handler.js`)

- Parses each SQS record with the strict message union; per-record
  `KEYWORD_MESSAGE_CONTRACT_MISMATCH` → that record fails, never a provider
  call.
- Constructs the keyword-only store exactly as specified:
  `new S3ArtifactStore({ client: runtime.s3Client, bucket:
  runtime.config.awsPipelineBucket, maxBytes: 33554432 })` — the existing
  runtime store (5,000,000) is neither reconfigured nor used for keyword
  artifacts, and the keyword store is not shared with the existing handlers.
- Returns SQS partial batch failures (`{ batchItemFailures }`); uses the
  `handleSqsBatch` pattern from `adapters/sqs-batch.js`.
- One Lambda invocation performs at most one provider attempt.

### 5.5 Recovery (`recovery.js`)

- Only reads dispatchable durable rows (`repository.recover(now)`): queued
  research without an expansion stage; expired
  nonterminal task leases and pending tasks with `nextAttemptAt <= DB now`;
  expired aggregation leases.
- Emits identity task/check messages using only returned fields and the one
  `DEC-KI-027` queue URL; **never** invokes a provider; duplicates commute
  (`DEC-KI-022`).

### 5.6 Build (`scripts/build-keyword-worker.js`)

- Dedicated build mirroring `scripts/build-lambda.js` conventions (esbuild
  bundle, Node ESM, `@prisma/client` external, ESM require banner, required
  Prisma engine copy, deterministic timestamps, zip) but for the keyword
  handler only. `build-lambda.js`'s frozen handler list is **not** modified
  (W7 scope). No new package dependency.
- `local_build` proof: emit `dist/lambda/keyword-worker.zip`, verify startup of
  the bundled handler with mocked boundaries.

### 5.7 Worker deliverable tests

- `keyword-intelligence-worker.test.js` + `keyword-intelligence-recovery.test.js`
  with mocked S3/SQS/provider/http boundaries and (for integration cases) the
  isolated DB harness.
- Execute `SCN-KI-001`, `004`–`007`, `012`, `013` (see §6); inject before/after
  every external/durable boundary; verify artifacts/counters/messages/calls;
  nonempty run must reach every message type.
- **Negative controls:** bypass the task table or S3 validation → must fail;
  bypass anchor or one market worker → completion stays false; 301 candidates/
  201 shortlist/second US overview/N+1 overview call → ceiling assertion fails.

---

## 6. Verification (V1–V5)

| ID | Action |
|---|---|
| `KI-W3-V1` | Execute `SCN-KI-001` (nonempty durable research), `SCN-KI-004` (strict expansion payloads), `SCN-KI-005` (anchor screen + nine-market result), `SCN-KI-006` (paid-call failure boundaries), `SCN-KI-007` (throttle/retry schedules), `SCN-KI-012` (lease/recovery competing owners), `SCN-KI-013` (maximum worker scale); include every failure boundary and activation witness |
| `KI-W3-V2` | Run focused/unit/integration tests and the emitted handler build/startup with mocked boundaries (`node --test test/keyword-intelligence-adapter.test.js test/keyword-intelligence-worker.test.js test/keyword-intelligence-recovery.test.js`; `node scripts/build-keyword-worker.js`; smoke import/startup) |
| `KI-W3-V3` | Assert five seeds → exactly ten US expansion tasks, one US anchor-screen task, and eight remaining-market tasks: 19 first-pass calls/task artifacts, three manifests, one final artifact, at most 95 attempt rows/calls across five attempts, and **never more than one HTTP call per invocation** |
| `KI-W3-V4` | Assert messages/logs/errors/artifacts/cache exclude forbidden raw/private fields and owner access cannot be inferred from cache; `npm run check:secrets`; strict `unrecognized_keys` rejection |
| `KI-W3-V5` | Assert the keyword handler uses `maxBytes 33554432` while an independently constructed existing pipeline runtime still uses `maxBytes 5000000`; neither store is shared with the other's handler |

`V3` oracles: `$0.492` first-pass reservation, `$2.46` five-attempt exposure,
`$3.00` over-budget zero-call denial, ≤23 S3 objects, 19 work messages plus
bounded checks.

---

## 7. Read-only sources consulted (for the implementer)

- `email_scraper/src/aws-pipeline/adapters/{artifact-store,queue-dispatcher,sqs-batch}.js`
- `email_scraper/src/aws-pipeline/contracts/{artifacts,messages,errors}.js`
- `email_scraper/src/aws-pipeline/core/{canonical,keys,lease-monitor}.js`
- `email_scraper/src/aws-pipeline/handlers/{traffic-worker,recovery}.js`
- `email_scraper/src/aws-pipeline/services/{discovery-worker,lead-worker,domain-aggregator,recovery}.js`
- `email_scraper/src/aws-pipeline/repositories/pipeline-coordinator-repository.js`
- `email_scraper/src/aws-pipeline/{runtime,runtime-config,pipeline-log}.js`
- `email_scraper/src/keyword-intelligence/{repository,schemas,config,pipeline,selection,query-mapper,normalize,intent,dedup,cluster,score}.js`
- `email_scraper/scripts/build-lambda.js`; `email_scraper/test/aws-pipeline-runtime-adapters.test.js`
- `KeywordSearchVolume/pipeline/client.py` (behavioral source only)
- `KeywordSearchVolume/pipeline/{normalize,dedup,cluster,score,pipeline,models}.py` (behavioral references)

No file outside the `authorized_write_scope` may be modified. No file in
`KeywordSearchVolume/` may be imported by runtime or copied in.

---

## 8. Handoff (H1–H6)

1. `H1` Record changed files/symbols/build artifacts (must equal the A4 write
   scope plus generated `dist/lambda/keyword-worker.zip`).
2. `H2` Record commands, outcomes, scenarios, skipped checks.
3. `H3` `git diff` matches authorized scope exactly.
4. `H4` No successor (`KI-W4`) or prohibited action started.
5. `H5` Append evidence to A6 (`EV-KI-W3-01..07`); CAS A5 to `AWAITING_REVIEW`.
6. `H6` Stop; do not begin `KI-W4`.

---

## 9. Environment prerequisites and resolved predecessor decisions

1. **Predecessor and A5 assignment:** the reopened `KI-R1` must pass its six
   remediation checks plus `SCN-KI-020`/`021` and be accepted; the parent then
   rehashes A1/A4 and records a one-window `KI-W3` assignment before any W3
   edit.
2. **Isolated database:** `TEST_DATABASE_URL` and `ALLOW_DATABASE_TESTS=true`
   must be provided (as in W1); the isolated harness
   (`test/helpers/isolated-postgres.js`) is used for migration-backed
   integration cases in `finally`-dropped disposable schemas.
3. **Mock harnesses:** S3/SQS/provider/http/clock seams are injected per the
   existing `runtime-adapters` and worker-service test patterns; no live
   secret, provider call, or AWS call occurs.
4. **Fixture state:** the four W3 payload fixture files are already materialized
   under `GATE-KI-002` (`EV-KI-A-029`); the implementer may only extend the
   shared fixture directory for strict payload cases and must **not** overwrite
   W2 golden fixtures.
5. **Resolved repository decisions:** `DEC-KI-026` selects one corrective
   implementation: `scheduleRetry`; worker-safe context reads and ownerless
   initialization; attempt-count/token fencing; readiness-gated aggregation;
   atomic candidate/shortlist/final publication; complete recovery projections;
   and the canonical six-byte BLAKE2s selection ID. `KI-R1` owns and must prove
   these choices through `SCN-KI-020` and reopened `SCN-KI-021`; W3 only
   consumes them.
6. **Resolved queue/time decisions:** `DEC-KI-027` selects one dedicated queue,
   the runtime property `awsPipelineKeywordResearchQueueUrl`, environment key
   `AWS_PIPELINE_KEYWORD_RESEARCH_QUEUE_URL`, and exact durable createdAt sources
   for every artifact `producedAt`. W3 consumes the property in mocked/local
   runtime objects; W7 later owns application/runtime-config and SAM wiring.
7. **No remaining W3 design choice:** if accepted KI-R1 output lacks any literal
   `DEC-KI-026` method/predicate/return field, or runtime construction cannot
   inject the `DEC-KI-027` property without leaving W3 scope, stop and report a
   predecessor/specification mismatch. Do not implement an alternative inside
   W3.

---

## 10. Execution sequence (only after accepted KI-R1 and W3 assignment)

1. Verify accepted `KI-R1`/`SCN-KI-020`/`SCN-KI-021`, then record `KI-W3-P1…P4` evidence
   (`EV-KI-W3-01`).
2. Implement `contracts.js` (strict message/artifact schemas) then `keys.js`
   (artifact key builders) — consumed by everything else.
3. Implement `dataforseo-labs-adapter.js` (T1): strict request builders +
   fingerprint verification → cache → throttle → budget reservation →
   single timed POST → strict parse/classify → settle → retry/ambiguity.
4. Implement `service.js` paths (initialize, expansion task, anchor task,
   market task, aggregate checks, final publication) composing repository +
   adapter + artifacts.
5. Implement `handler.js` (keyword-only `S3ArtifactStore` 33554432; partial
   batch failures) and `recovery.js`.
6. Implement `scripts/build-keyword-worker.js`; emit and smoke the handler.
7. Write the three owned test files; run adapter + worker + recovery suites.
8. Run V1–V5 incl. `SCN-KI-001/004–007/012/013`, negative controls,
   `check:secrets`, and the V3/V5 byte/count/budget oracles.
9. Hand off (H1–H6), stop.
