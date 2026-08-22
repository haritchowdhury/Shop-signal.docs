# Keyword Intelligence Decision-Complete Execution Checklist (`A4`)

**Checklist revision:** `KI-CL-32`
**Package status:** `AUTHORING-READY`; assignable only by a one-window `A5`
assignment  
**Execution status authority:** only `ACTIVE_EXECUTION_STATE.md`

This is the sole authority for ordered windows, implementation tasks, tests,
and acceptance. The other artifacts are `A1`
`KEYWORD_INTELLIGENCE_PRODUCT_CONTRACT.md`, `A2`
`KEYWORD_INTELLIGENCE_DISCOVERY_DOSSIER.md`, `A3`
`KEYWORD_INTELLIGENCE_DECISION_LEDGER.md`, `A5`
`ACTIVE_EXECUTION_STATE.md`, `A6`
`KEYWORD_INTELLIGENCE_EXECUTION_EVIDENCE.md`, `A7`
`KEYWORD_INTELLIGENCE_SPECIFICATION_CHANGELOG.md`, and `A8`
`KEYWORD_INTELLIGENCE_TRACEABILITY_INDEX.md`.

No box in an implementation window is checked by this authoring document.

## 1. Dependency DAG and gates

```text
GATE-KI-001 (CLOSED: requester authorized A5 switch)
GATE-KI-003 (CLOSED: requester fixed collection topology and $3 hard cap)
GATE-KI-002 (CLOSED: EV-KI-A-029 — exact installs, representative builds, fixtures)
    -> KI-W1 persistence
    -> KI-W2 pure Node parity
    -> KI-R1 corrective repository bridge
    -> KI-R2 corrective repository lease fences (requester-reopened proof gate)
    -> KI-W3 durable worker (both handoffs rejected; implementation retained as KI-R3 baseline)
    -> KI-R3 enforcement-complete worker correction (parent review rejected)
    -> KI-R4 commit-stable enforcement correction and cumulative W3 acceptance
    -> KI-W4 API + run handoff/query branch
    -> KI-W5 full Next.js dashboard
    -> KI-R5 W4/W5 functional boundary correction
    -> KI-W6 run-workspace correction and causal local acceptance
    -> STOP_LOCAL
    -> KI-W7 infrastructure source (separate authorization)
    -> STOP_AWS_MUTATION_APPROVAL
    -> KI-W8 deployment/live canary (action-by-action approvals)
    -> STOP_FINAL_INDEPENDENT_REVIEW
```

`GATE-KI-001`: requester authorizes replacing the parked G-R31 assignment with
the hash-pinned keyword package. Parent writes one-window `A5`; invalid or
absent approval leaves this checklist unassignable.

`GATE-KI-002`: after `GATE-KI-001`, parent may install only
`@noble/hashes@2.2.0` in backend and `chart.js@3.9.1` plus
`chartjs-chart-treemap@2.0.0` in frontend, build representative imports in the
actual Node/Next targets, inventory emitted dependencies, record compressed and
uncompressed sizes/startup, and update hashes. Any install/build incompatibility
causes an A7 correction; no alternative library is selected by an implementer.

`GATE-KI-003` is closed by `SRC-KI-030`: `maxCostPerResearchUsd=3.00`; expansion
uses the US anchor only and reserves `$0.012 + $0.00012×30 = $0.0156` for each
suggestions/related request; the US screening overview reserves
`$0.012 + $0.00012×candidateCount` for at most 300 candidates; each of the eight
remaining-market overview requests reserves
`$0.012 + $0.00012×shortlistCount` for at most 200 keywords. Thus first-pass
reservation is at most `$0.492`, five total attempts per logical task reserve at
most `$2.46`, and `$0.54` remains below the hard cap. The repository must deny
the next reservation before an HTTP call if cumulative actual plus held
reservations plus that reservation would exceed `$3.00`. Closing this gate made
no paid call and grants no implementation or provider-call authority.

## 2. Execution windows

### `KI-W1` — Durable schema and fenced repository

```yaml
window_id: KI-W1
objective: Persist one owner-scoped research, immutable task sets, cache/paid evidence, selection revisions, and atomic run lineage.
depends_on: [GATE-KI-002]
consumes: DEC-KI-002, DEC-KI-009, DEC-KI-017, DEC-KI-018, DEC-KI-021, DEC-KI-022
produces: forward Prisma migration, generated client, keyword repository, isolated database proofs
assigned_agent_policy: one_window
authorized_write_scope: email_scraper/prisma/schema.prisma; email_scraper/prisma/migrations/20260817000000_keyword_intelligence/migration.sql; email_scraper/src/keyword-intelligence/repository.js; email_scraper/test/keyword-intelligence-repository.test.js; email_scraper/test/keyword-intelligence-repository.integration.test.js
shared_file_scope: schema.prisma only for DEC-KI-021 models/relations/enums; no existing field alteration
read_only_scope: email_scraper/src/prisma-run-repository.js; email_scraper/src/aws-pipeline/repositories/pipeline-coordinator-repository.js; email_scraper/test/helpers/isolated-postgres.js
authorized_actions: [local_source_edits, prisma_generate, prisma_validate, local_unit_tests, isolated_test_database_writes, evidence_updates]
prohibited_actions: [provider_calls, AWS_operations, production_database_writes, frontend_edits, destructive_shared_cleanup, commits]
successor: KI-W2
successor_reserved_for: parent
may_start_successor: false
```

- [x] `KI-W1-P1` Active assignment ID, A1/A4 hashes, and state version match. Evidence: `EV-KI-W1-01` (A1 `8b17f85c…`, A4 `a12174f3…`, state 70).
- [x] `KI-W1-P2` Closed Gate 1/Gate 3 evidence, exact paid policy, and Gate 2 representative build proof exist. Evidence: `EV-KI-W1-01` (`EV-KI-A-025/026/027/029/030`).
- [x] `KI-W1-P3` A non-production isolated `TEST_DATABASE_URL` passes harness identity/schema checks. Evidence: `EV-KI-W1-01` (harness roundtrip on `ep-dry-fog-az4tir8h`).
- [x] `KI-W1-P4` Starting dirty worktrees and exact owned symbols are recorded. Evidence: `EV-KI-W1-01`.

#### Task block `KI-W1-T1`

1. **Task:** add exactly the enums, models, fields, relations, constraints, and
   indexes in `DEC-KI-021` with one forward migration; generate and validate the
   Prisma client.
2. **Requirements/decisions:** `REQ-KI-005`, `015`–`017`, `INV-KI-001`,
   `DEC-KI-017`, `021`.
3. **Source:** current `email_scraper/prisma/schema.prisma` Run/RunQuery and
   pipeline model symbols; `SRC-KI-012`.
4. **Target:** only the schema/migration paths in the window header.
5. **Interface/schema:** literal field/type/default/unique/index contract in
   `DEC-KI-021`; all new Run lineage fields nullable except discriminator
   default `legacy`; no backfill SQL beyond defaults.
6. **Algorithm:** append enums/models; add relations; generate migration;
   inspect SQL; require creation/addition only; generate/validate client.
7. **Operations:** schema edit → migration generation against isolated DB →
   inspect SQL → apply in disposable schema → assertions → cleanup in finally.
8. **Atomicity:** migration transaction as Prisma supports; runtime atomic
   sequences are implemented in T2; no destructive rewrite.
9. **Identities:** exact unique/index formulas are `DEC-KI-002`, `009`, `017`,
   `021`; DB timestamps are `now()`/`@updatedAt` as specified.
10. **Failure/replay:** migration failure rolls back/fails closed; rerun applies
    once through schema-local `_prisma_migrations`; no public cleanup.
11. **Dependencies/bounds:** existing Prisma 6.19.3; JSONB result ≤32 MiB;
    selection ≤200 enforced in repository, not SQL array length.
12. **Callers/obsolete behavior:** new repository only; preserve all existing
    Run/RunQuery callers and data; do not touch old cache/output files.
13. **Tests:** isolated migration from current schema; assert every table,
    column, enum, default, FK, unique/index; create a legacy Run without lineage;
    reject duplicate task/handoff/attempt; negative control removes one unique
    constraint and must fail catalog assertion.
14. **Output:** generated client/schema consumed by `KI-W1-T2` and all later
    backend windows.
15. **Non-goals:** no API, worker, algorithms, infrastructure, data import,
    production migration, or frontend.

- [x] `KI-W1-T1` Perform the fully specified schema/migration change above. Evidence: `EV-KI-W1-02`.

#### Task block `KI-W1-T2`

1. **Task:** implement `PrismaKeywordResearchRepository` with the exact
   transition, selection, cache, attempt, throttle, recovery, and handoff
   primitives used by later windows.
2. **Requirements/decisions:** `REQ-KI-002`, `005`, `015`–`017`, `022`,
   `INV-KI-005`–`008`, `DEC-KI-002`, `008`, `009`, `017`, `018`, `022`.
3. **Source:** existing coordinator repository/lease patterns in `SRC-KI-016`.
4. **Target:** `email_scraper/src/keyword-intelligence/repository.js` and its
   owned test files only.
5. **Interface/schema:** explicit `{outcome}` methods named in D1; inputs are
   frozen objects containing IDs/generation/fingerprints/tokens; outputs
   discriminate `created|found|claimed|terminal|lost|conflict|not_found|delayed`.
6. **Algorithm:** implement conditional update/CAS for each lifecycle row;
   first-terminal counter increments in same transaction; all-terminal compares
   immutable expected count; throttle uses DB time and atomic update; provider
   reservation atomically sums every known settled actual cost plus in-flight/ambiguous
   reservations against the exact `DEC-KI-009` snapshot and permits no call when
   the next reservation would exceed it; handoff transaction is `DEC-KI-017`
   but accepts a callback to construct Run rows.
7. **Operations:** no network inside transaction; exact S3/SQS recovered
   boundaries remain caller-owned; selection/run writes are one transaction.
8. **Atomicity:** D2 classification applies verbatim; every multi-row state
   transition uses one interactive transaction with bounded DB-only work.
9. **Identities:** formulas from `DEC-KI-002`, `009`, `017`; all time predicates
   use injected value or DB time as specified; tokens are random 24-byte
   base64url values supplied by caller.
10. **Failure/replay:** lease loss returns `lost`; duplicate terminal is no-op
    with original result; conflicting fingerprint is conflict; expired owner can
    be reclaimed; terminal research is immutable; cancellation unsupported.
11. **Dependencies/bounds:** Prisma only; 60/20 task and 120/40 aggregator
    lease/heartbeat; ≤19 logical tasks and ≤95 attempt rows as applicable;
    transactions contain
    no result traversal above one bounded record/task-set.
12. **Callers/obsolete behavior:** later worker/API are callers; existing
    repositories remain unchanged; do not expose cache to owner-facing reads.
13. **Tests:** migration-backed tests schedule every D4 competing pair,
    advance injected clock beyond full lease, duplicate/reorder task terminal,
    stale selection, identical/conflicting handoff retry, cache expiry, throttle
    collision, cost reservation/settlement/ambiguity/budget exhaustion, and
    zero-count advance; assert exact rows/counters and no external calls.
    Negative control removes token or budget predicate and race/budget test must
    fail.
14. **Output:** repository interface/behavior consumed by `KI-W3`/`KI-W4`.
15. **Non-goals:** no HTTP, S3/SQS, provider, pure algorithm, frontend, AWS.

- [x] `KI-W1-T2` Perform the fully specified repository change above. Evidence: `EV-KI-W1-03`.

- [x] `KI-W1-V1` Execute `SCN-KI-002`, `SCN-KI-008`, `SCN-KI-009`, `SCN-KI-012`, and `SCN-KI-015`; record activation/oracle/negative controls. Evidence: `EV-KI-W1-04`.
- [x] `KI-W1-V2` Run `npm run db:generate`, `npm run db:validate`, focused unit tests, and opted-in isolated integration tests; assert legacy-row compatibility. Evidence: `EV-KI-W1-05`.
- [x] `KI-W1-V3` Assert task/counter transaction statement growth is linear and selection comparison stays at the stated caps. Evidence: `EV-KI-W1-06`.
- [x] `KI-W1-V4` Run `npm run check:secrets`; assert owner IDs/results never enter cache/attempt log and no production/public schema was touched. Evidence: `EV-KI-W1-06`.
- [x] `KI-W1-H1` Record changed files/symbols and migration. Evidence: `EV-KI-W1-07`.
- [x] `KI-W1-H2` Record commands, outcomes, scenarios, and skipped checks. Evidence: `EV-KI-W1-02/03/04/05`.
- [x] `KI-W1-H3` Diff matches authorized scope. Evidence: `EV-KI-W1-07`.
- [x] `KI-W1-H4` No successor/prohibited action started. Evidence: `EV-KI-W1-07`.
- [x] `KI-W1-H5` Append evidence and set A5 to `AWAITING_REVIEW` by version CAS. Evidence: `EV-KI-W1-07`, A5 state 71.
- [x] `KI-W1-H6` Stop; do not assign or begin `KI-W2`. Evidence: `EV-KI-W1-07`.

Correction note (`CHG-KI-009`): the completed W1-T2 prose above abbreviated
held exposure as in-flight/ambiguous. `DEC-KI-009` and `DEC-KI-026` are the
current authority and include `planned|in_flight|ambiguous`; KI-R1 verifies the
accepted implementation and all future callers against that exact set without
rewriting W1 evidence.

### `KI-W2` — Exact Node calculation and selection engine

```yaml
window_id: KI-W2
objective: Produce Python-parity normalized research results, exports, default selections, and conflict analysis in pure Node.
depends_on: [KI-W1]
consumes: generated Prisma types only; SRC-KI-006 through SRC-KI-011; DEC-KI-003 through DEC-KI-016
produces: pure Node modules, strict domain schemas, golden parity fixtures/tests
assigned_agent_policy: one_window
authorized_write_scope: email_scraper/src/keyword-intelligence/config.js; email_scraper/src/keyword-intelligence/schemas.js; email_scraper/src/keyword-intelligence/normalize.js; email_scraper/src/keyword-intelligence/intent.js; email_scraper/src/keyword-intelligence/dedup.js; email_scraper/src/keyword-intelligence/cluster.js; email_scraper/src/keyword-intelligence/score.js; email_scraper/src/keyword-intelligence/pipeline.js; email_scraper/src/keyword-intelligence/selection.js; email_scraper/src/keyword-intelligence/query-mapper.js; email_scraper/src/keyword-intelligence/export.js; email_scraper/test/fixtures/keyword-intelligence/parity-input-v1.json; email_scraper/test/fixtures/keyword-intelligence/parity-output-v1.json; email_scraper/test/fixtures/keyword-intelligence/selection-cases-v1.json; email_scraper/test/keyword-intelligence-parity.test.js; email_scraper/test/keyword-intelligence-selection.test.js; email_scraper/test/keyword-intelligence-query-mapper.test.js
shared_file_scope: none
read_only_scope: KeywordSearchVolume/config.yaml; KeywordSearchVolume/pipeline/config.py; KeywordSearchVolume/pipeline/models.py; KeywordSearchVolume/pipeline/normalize.py; KeywordSearchVolume/pipeline/intent.py; KeywordSearchVolume/pipeline/dedup.py; KeywordSearchVolume/pipeline/cluster.py; KeywordSearchVolume/pipeline/score.py; KeywordSearchVolume/pipeline/pipeline.py; KeywordSearchVolume/pipeline/output.py; KeywordSearchVolume/tests/fixtures.py; KeywordSearchVolume/tests/test_normalize.py; KeywordSearchVolume/tests/test_intent.py; KeywordSearchVolume/tests/test_dedup.py; KeywordSearchVolume/tests/test_cluster.py; KeywordSearchVolume/tests/test_score.py; KeywordSearchVolume/tests/test_markets.py; KeywordSearchVolume/tests/test_seed_research.py; KeywordSearchVolume/dashboard/index.html
authorized_actions: [local_source_edits, local_node_tests, development_only_python_parity_oracle, evidence_updates]
prohibited_actions: [runtime_python_integration, provider_calls, database_writes, AWS_operations, frontend_edits, package_changes, commits]
successor: KI-R1
successor_reserved_for: parent
may_start_successor: false
```

- [x] `KI-W2-P1` Assignment/hashes/version match. Evidence: `EV-KI-W2-01`
- [x] `KI-W2-P2` `KI-W1` accepted and exact hash dependency exists. Evidence: `EV-KI-W2-01`
- [x] `KI-W2-P3` `@noble/hashes@2.2.0` representative build proof is present. Evidence: `EV-KI-W2-01`
- [x] `KI-W2-P4` Dirty state/scope and standalone source revision are recorded. Evidence: `EV-KI-W2-01`

#### Task block `KI-W2-T1`

1. **Task:** direct-port all configuration, models, normalization, intent,
   dedup, clustering, scoring, pipeline aggregation, and export functions.
2. **Requirements/decisions:** `REQ-KI-003`–`005`, `018`, `023`, `024`, `DEC-KI-004`,
   `010`–`012`, `024`.
3. **Source:** exact Python files/functions in `SRC-KI-008` and config in
   `SRC-KI-006`; historical normalized outputs `SRC-KI-011`.
4. **Target:** pure module files listed in header; no filesystem/network import.
5. **Interface/schema:** strict `keyword-research-config-v1` and
   `keyword-research-result-v1`; exact public fields in `DEC-KI-012`; functions
   accept/return plain immutable data and injected config.
6. **Algorithm:** statement-for-statement formulas/order/ties from Python;
   BLAKE2s IDs via decided dependency; delete raw_ref from output; no fallback
   field paths; exact cumulative/market/cluster passes.
7. **Operations:** pure memory only; CSV serializer returns string/bytes; no
   durable or external operation.
8. **Atomicity:** N/A pure functions (`SRC-KI-008` proves no required durable
   side effect in calculation).
9. **Identities:** exact stable-ID and result fingerprint formulas from
   `DEC-KI-002`, `009`, `012`.
10. **Failure/replay:** invalid config/result input throws typed contract error;
    same ordered input returns byte-identical result; no retry/concurrency/
    cancellation behavior in pure layer.
11. **Dependencies/bounds:** Node ESM, Zod 4.4.3, `@noble/hashes@2.2.0`;
    anchor k≤300 and final-shortlist k≤200; O(k²) loops must be explicit and
    instrumentable; result ≤32 MiB.
12. **Callers/obsolete:** worker finalizer and API exporter call these modules;
    Python remains development oracle only; no raw output/file writer port.
13. **Tests:** one fixture per function boundary; exact golden Node/Python
    equality under `DEC-KI-011`; shuffled/tie/boundary cases; 300-candidate
    anchor and 200-keyword final generated tests with deterministic seeds and
    operation counters. Negative
    control changes one weight/alias/tie-break and golden test must fail.
14. **Output:** normalized result/export engine consumed by `KI-W3` and `KI-W5`.
15. **Non-goals:** no algorithm redesign, provider parsing, DB/API/UI/worker.

- [x] `KI-W2-T1` Perform the fully specified pure port above. Evidence: `EV-KI-W2-02`, `EV-KI-W2-04`

#### Task block `KI-W2-T2`

1. **Task:** implement seed/selection parsers, default order, edits, full-list
   conflict components/canonical suggestions, and lane query mapper.
2. **Requirements/decisions:** `REQ-KI-001`, `006`–`011`, `DEC-KI-003`,
   `013`–`016`.
3. **Source:** Python dedup/lane symbols and dashboard selection behavior in
   `SRC-KI-008`, `SRC-KI-010`.
4. **Target:** `schemas.js`, `selection.js`, `query-mapper.js`, owned tests.
5. **Interface/schema:** exact SelectionItem in `DEC-KI-014`; functions
   `normalizeSeeds`, `createDefaultSelection`, `validateSelectionDraft`,
   `analyzeSelectionConflicts`, `mapSelectionToQueries`, and
   `validateResearchBackedQueries` return strict success/error unions.
6. **Algorithm:** exact normalization; deterministic default sort; all `n(n-1)/2`
   pair comparisons; conflict graph components in item input order; canonical
   rank; lane mapping; query grammar/relevance/set equality from `DEC-KI-016`.
7. **Operations:** pure memory; persistence/revision happens in W4.
8. **Atomicity:** N/A pure; repository later saves full replacement atomically.
9. **Identities:** item ID and selection fingerprint are canonical formulas in
   `DEC-KI-002`, `009`, `014`.
10. **Failure/replay:** invalid/over-200 rejected with stable field issues;
    conflicts block finalization but do not mutate; repeated analysis exact;
    cancellation N/A.
11. **Dependencies/bounds:** max seeds5, seed100, keyword160, draft200,
    retained/query100, 19,900 comparisons, query200/12 words.
12. **Callers/obsolete:** W4 API/review and W5 dashboard; bypass old candidate
    planner only for research-backed discriminator; preserve legacy functions.
13. **Tests:** boundaries 0/1/5/6 seeds, Unicode/control/duplicates; recommended
    0/1/100/101; exact/near/transitive conflicts; 200 unique; all four lanes;
    product/non-product grammar and malicious operators. Negative control skips
    one pair and maximum conflict fixture must fail.
14. **Output:** strict selection/query engine for W4/W5/W6.
15. **Non-goals:** no silent selection mutation, provider/UI/DB/AWS edits.

- [x] `KI-W2-T2` Perform the fully specified selection/query engine above. Evidence: `EV-KI-W2-03`

- [x] `KI-W2-V1` Execute `SCN-KI-003`, `SCN-KI-010`, `SCN-KI-011`, and `SCN-KI-014` with negative controls. Evidence: `EV-KI-W2-04`
- [x] `KI-W2-V2` Run focused Node tests and development-only Python golden oracle; prove no production script imports/invokes Python. Evidence: `EV-KI-W2-04`
- [x] `KI-W2-V3` Measure the 300-candidate anchor path, 200-keyword nine-market path, 200-item duplicate path, result bytes, and exact operation counters against `DEC-KI-024`. Evidence: `EV-KI-W2-04`
- [x] `KI-W2-V4` Assert fixtures/exports contain no raw reference/body/credential/private field and unknown payload fields fail. Evidence: `EV-KI-W2-05`
- [x] `KI-W2-H1` Record changed files/symbols. Evidence: `EV-KI-W2-06`
- [x] `KI-W2-H2` Record commands, outcomes, scenarios, skipped checks. Evidence: `EV-KI-W2-06`
- [x] `KI-W2-H3` Diff matches scope. Evidence: `EV-KI-W2-06`
- [x] `KI-W2-H4` No successor/prohibited action. Evidence: `EV-KI-W2-06`
- [x] `KI-W2-H5` Append evidence; A5 `AWAITING_REVIEW` by CAS. Evidence: `EV-KI-W2-07`
- [x] `KI-W2-H6` Stop; do not begin the successor window. Evidence: `EV-KI-W2-07`

### `KI-R1` — Corrective repository bridge for the durable worker

```yaml
window_id: KI-R1
objective: Repair the accepted W1 repository boundary so W3 receives one complete, fenced, recoverable interface without a schema change.
depends_on: [KI-W2]
consumes: accepted W1 schema/repository; accepted W2 selection identity; DEC-KI-002; DEC-KI-018; DEC-KI-022; DEC-KI-026; DEC-KI-027; EV-KI-A-031
produces: corrected repository interface and isolated integration evidence required by W3
assigned_agent_policy: one_window
authorized_write_scope: email_scraper/src/keyword-intelligence/repository.js; email_scraper/test/keyword-intelligence-repository.test.js; email_scraper/test/keyword-intelligence-repository.integration.test.js
shared_file_scope: repository.js only for the literal DEC-KI-026 interface and behavior; accepted unrelated W1/W2 behavior remains unchanged
read_only_scope: email_scraper/prisma/schema.prisma; email_scraper/prisma/migrations/20260817000000_keyword_intelligence/migration.sql; email_scraper/src/keyword-intelligence/selection.js; email_scraper/src/keyword-intelligence/dedup.js; email_scraper/src/aws-pipeline/repositories/pipeline-coordinator-repository.js; email_scraper/test/helpers/isolated-postgres.js
authorized_actions: [local_source_edits, prisma_generate, prisma_validate, local_unit_tests, isolated_test_database_writes, evidence_updates]
prohibited_actions: [schema_or_migration_edits, W3_worker_or_adapter_edits, provider_calls, AWS_operations, production_database_writes, API_or_frontend_edits, package_changes, commits]
successor: KI-W3
successor_reserved_for: parent
may_start_successor: false
```

- [x] `KI-R1-P1` Active assignment is exactly `KI-R1`; A1/A4 hashes and A5 state version match. Evidence: `EV-KI-R1-01` (A1 `8b17f85c…`, A4 `35f7236d…`, state 75).
- [x] `KI-R1-P2` `KI-W1` and `KI-W2` acceptance evidence exists and `EV-KI-A-031` findings reproduce against the accepted repository. Evidence: `EV-KI-R1-01`.
- [x] `KI-R1-P3` A non-production isolated `TEST_DATABASE_URL` passes the required identity/schema checks; no provider or AWS credentials are loaded. Evidence: `EV-KI-R1-01` (host `ep-dry-fog-az4tir8h…neon.tech`, distinct from production).
- [x] `KI-R1-P4` Starting dirty state and the three owned paths are recorded; all prohibited paths are byte-identical at handoff. Evidence: `EV-KI-R1-01`, `EV-KI-R1-07`.

#### Task block `KI-R1-T1`

1. **Task:** implement the literal corrective repository interface, transaction
   predicates, retry scheduling, atomic publication, and recovery projections
   in `DEC-KI-026`; use the one-queue/time mapping in `DEC-KI-027` only where a
   returned recovery row requires those values.
2. **Requirements/decisions:** `REQ-KI-002`, `005`, `015`–`017`, `022`,
   `INV-KI-002`, `004`–`008`, `014`, `DEC-KI-002`, `018`, `022`, `026`, `027`.
3. **Source:** accepted `PrismaKeywordResearchRepository` symbols and tests;
   exact contradictory implementation evidence `EV-KI-A-031`; W2
   `selectionItemId`; existing pipeline coordinator lease/recovery patterns.
4. **Target:** exactly the three paths in the window's
   `authorized_write_scope`; no Prisma schema or migration edit.
5. **Interface/schema:** implement exactly `getWorkerResearch`,
   `getTaskContext`, `getStageContext`, ownerless `initialize`, corrected
   `recordAttempt`, `settleAttempt`, `markAttemptAmbiguous`, `deferTask`, `scheduleRetry`,
   readiness-gated `claimAggregator`, atomic `publishCandidateManifest`,
   `publishShortlist`, fenced atomic `publishResearchResult`, and complete
   `recover` result unions from `DEC-KI-026`. Do not add an alternative public
   method, worker owner argument, callback transaction escape hatch, or schema.
6. **Algorithm:** replace repository item IDs with the six-byte BLAKE2s formula;
   return strict worker context projections; create an exact immutable initial
   task set ownerlessly; derive and reserve the next attempt under the current
   task token; settle known outcomes or durably mark ambiguity; schedule a
   pre-call throttle delay without an attempt; schedule a known retry at its
   derived due time with cleared lease; admit an
   aggregator only when ready or reclaiming expired aggregation; publish the
   expansion manifest plus US anchor stage/tasks atomically; publish the
   shortlist plus eight remaining-market tasks atomically; publish result,
   market manifest, revision-one default selection, and completed research in
   one fenced transaction; reconstruct recovery messages from returned rows
   alone.
7. **Operations:** DB-only work inside transactions; no HTTP, S3, SQS, provider,
   filesystem, or AWS call. Tests use mocked downstream seams only to prove
   zero calls at denied/early/ambiguous boundaries.
8. **Atomicity:** every method named atomic in `DEC-KI-026` is one Prisma
   interactive transaction with all stated predicates and writes inside it;
   no nested transaction and no caller-owned `repository.transaction(...)`.
   `scheduleRetry` performs task state, due time, and lease clearing together;
   candidate publication, shortlist publication, and final publication each
   have their literal all-or-none row sets.
9. **Identities:** use the exact six-byte `selectionItemId` and
   `stageInputFingerprint` formulas in `DEC-KI-002`/`026`; all fingerprints use
   canonical JSON; use durable `createdAt` values according to `DEC-KI-027` for
   replay-stable artifact-time projections; never derive identity from owner,
   mutable text index, or wall-clock time.
10. **Failure/replay:** stale generation/token returns `lost`; exact terminal or
     publication replay returns the existing outcome; conflicting fingerprint or
     immutable set returns `conflict`; early aggregator returns `not_ready`;
     attempt six and an over-budget reservation are denied before any external
     call; known retry crash before scheduling is recoverable without creating a
     new attempt; ambiguous exposure remains non-repeatable independent of a
     subsequently stale task lease.
11. **Dependencies/bounds:** accepted Prisma 6.19.3 schema only; five attempts
     maximum; task lease 60/20 seconds; aggregator lease 120/40 seconds; at most
     19 tasks, 95 attempts, 300 candidates, 200 shortlisted/selection rows, eight
     remaining-market task rows, and 32 MiB result JSON. Statement growth is
     linear in the bounded row set.
12. **Callers/obsolete behavior:** W3 is the sole new worker caller and must be
     able to use only the named public methods; W4 continues owner-scoped reads
     and selection edits. Remove the full-digest W1 item-ID behavior, ownerful
     worker initialization, collecting-stage early aggregator claim, split final
     publication, and incomplete recovery projection. Preserve legacy and all
     unrelated accepted repository behavior.
13. **Tests:** execute `SCN-KI-020`; assert W2/repository IDs agree for calculated
     and manual items; worker projections omit owner; initialize exact replay and
     mismatch; unclaimed/stale attempt denial; atomic attempt-count/reservation;
     duplicate pre-call marker becomes ambiguous with zero call; throttle delay
     consumes no attempt; successful cost settlement and normalized cache are
     all-or-none even after lease loss; known retry crash/reclaim/schedule/due
     sequence; attempt-five ceiling; ambiguity prevents a second call; early and
     competing aggregator schedules including expiry; rollback at each write of
     candidate/shortlist/final publication; stale final token leaves result,
     selection, manifest, and research status wholly unchanged; exact replay is
     idempotent; recovery constructs each strict message solely from returned
     data; durable producedAt values remain byte-stable. Negative controls remove
     one token/readiness/transaction predicate in turn and the corresponding
     schedule or partial-visibility assertion must fail.
14. **Output:** an accepted, versioned repository interface that makes
     `KI-W3-P2` mechanically satisfiable without W3 editing repository/schema or
     choosing an ownership, retry, transaction, identity, queue, or time policy.
15. **Non-goals:** no provider adapter, handler/service/contracts/keys/build
     implementation, API, frontend, infrastructure, schema/migration, package,
     live database, AWS, or paid call.

- [x] `KI-R1-T1` Perform the fully specified corrective repository change above. Evidence: `EV-KI-R1-02`.

- [x] `KI-R1-V1` Execute `SCN-KI-020` with every activation witness, schedule, atomic rollback, and negative control. Evidence: `EV-KI-R1-03`.
- [x] `KI-R1-V2` Run `npm run db:generate`, `npm run db:validate`, focused repository unit tests, and opted-in isolated repository integration tests. Evidence: `EV-KI-R1-04`, `EV-KI-R1-03`.
- [x] `KI-R1-V3` Assert the literal `DEC-KI-026` public interface exists, W3 can reconstruct every strict initialize/task/check message from its return values, and no direct transaction escape hatch is required. Evidence: `EV-KI-R1-05`.
- [x] `KI-R1-V4` Run `npm run check:secrets`; assert worker/recovery projections contain no owner, credential, raw provider body, private result, or unrestricted payload. Evidence: `EV-KI-R1-06`.
- [x] `KI-R1-V5` Run all accepted W1/W2 tests and prove schema/migration plus prohibited paths are byte-identical. Evidence: `EV-KI-R1-07`.
- [x] `KI-R1-H1` Record changed files/symbols and explicitly record no migration. Evidence: `EV-KI-R1-08`.
- [x] `KI-R1-H2` Record commands, outcomes, scenario schedules, negative controls, and skipped checks. Evidence: `EV-KI-R1-08`.
- [x] `KI-R1-H3` Diff matches the three-path scope and unrelated accepted code is unchanged. Evidence: `EV-KI-R1-08`.
- [x] `KI-R1-H4` No W3, provider, AWS, API, frontend, schema, package, or commit action occurred. Evidence: `EV-KI-R1-09`.
- [x] `KI-R1-H5` Append evidence and set A5 to `AWAITING_REVIEW` by state-version CAS. Evidence: `EV-KI-R1-09`, A5 state 78.
- [x] `KI-R1-H6` Stop; do not assign or begin `KI-W3`. Evidence: `EV-KI-R1-09`.

#### KI-R1 parent-review remediation (reopened at A5 state 80)

The first KI-R1 handoff remains append-only evidence, but it was **not
accepted**. `EV-KI-R1-10` falsified three `DEC-KI-026` claims that the original
23-case integration schedule did not exercise. This is an ordinary defect
whose behavior is already locked, so the existing unaccepted `KI-R1` window is
reopened; no `KI-R2`, schema choice, or new architecture is introduced.

1. **Attempt-five replay ordering:** in `recordAttempt`, load and reconcile the
   latest durable attempt before evaluating whether a new attempt would be
   number six. When `task.attemptCount===5` and latest attempt five is
   `planned|in_flight`, equal request fingerprint and reservation must
   return that attempt as `{outcome:"found",mayCall:false}`. It must create no
   row, change no counter, and authorize zero HTTP calls. Unequal fingerprint or
   reservation is `conflict`. `KEYWORD_PROVIDER_RETRY_EXHAUSTED` applies only
   when the repository would create a genuinely new attempt above five.
2. **Durable retry replay:** once `scheduleRetry` has atomically stored a
   pending task with a non-null `nextAttemptAt` and cleared lease fields, every
   exact replay for the same latest failed `attemptNumber` returns
   `{outcome:"delayed",retryAt:task.nextAttemptAt}` without recomputing it from
   the replay clock. This remains true before, at, and after the stored due
   time; only `claim` decides whether due work may be reclaimed. A different
   attempt number or non-failed latest attempt conflicts.
3. **Final-publication all-or-none result:** a `completed` market stage with a
   non-completed research is a conflicting partial state, never `found`.
   `publishResearchResult` must require exactly one conditional market-stage
   update and exactly one conditional research update. If either update affects
   zero rows, abort/roll back the interactive transaction through an internal
   private sentinel and map it outside the transaction: zero market-stage rows
   return `lost`; zero research rows return `conflict`. Returning normally from
   inside the transaction after the first write is forbidden. No result,
   selection, manifest, stage state, or research state may become visible on
   either zero-row schedule.
4. **Owned tests:** add the exact `SCN-KI-021` cases to
   `test/keyword-intelligence-repository.integration.test.js`; add any
   fail-closed input/surface assertion needed in the existing unit test. Do not
   weaken or delete the original KI-R1 tests.
5. **Regression and handoff:** rerun `SCN-KI-020` plus `SCN-KI-021`, focused
   tests, `npm run db:generate`, `npm run db:validate`, `npm run
   check:secrets`, and `npm test`; prove only the three KI-R1-owned paths differ
   from backend revision `2e477e9707afa6d6f4216ce99df58486f59f17b2` and that
   schema/migration/W3/provider/AWS/API/frontend/package paths remain unchanged.

- [x] `KI-R1-RP1` Verify A5 state 80 assigns only reopened KI-R1 and its A1/A4 hashes match. Evidence: `EV-KI-R1-11`, A5 state 80 pins `8b17f85c…`/`05deeaa7…` matched at start.
- [x] `KI-R1-RT1` Correct the three escaped `DEC-KI-026` behaviors exactly as specified above. Evidence: `EV-KI-R1-11` (`recordAttempt` replay-before-ceiling, `scheduleRetry` persisted-time replay, `publishResearchResult` partial-state conflict + `FinalPublicationAbort` zero-row mapping).
- [x] `KI-R1-RV1` Execute `SCN-KI-021` on an isolated non-public schema and preserve all original `SCN-KI-020` assertions. Evidence: `EV-KI-R1-11` (28/28 pass: 23 SCN-KI-020 + 5 SCN-KI-021; negative control fails 4/5 on the old source).
- [x] `KI-R1-RV2` Run the focused, Prisma validation/generation, secret, and full regression commands with exact outcomes. Evidence: `EV-KI-R1-11` (unit 10/10, db:generate/db:validate/check:secrets pass, `npm test` 502/0 fail).
- [x] `KI-R1-RH1` Append changed symbols, commands, scenario outcomes, skipped checks, and residual risks to A6. Evidence: `EV-KI-R1-11` (incl. two disposable leftover test schemas as the sole residual risk).
- [x] `KI-R1-RH2` CAS A5 back to `AWAITING_REVIEW` and stop without assigning or beginning KI-W3. Evidence: `EV-KI-R1-11`, `EV-KI-R1-12`, A5 state 83.

### `KI-W3` — Strict provider adapter and durable bounded worker

```yaml
window_id: KI-W3
objective: Complete research durably through bounded provider tasks and one fenced publication transaction.
depends_on: [KI-R2]
consumes: accepted KI-R1/KI-R2 repository at the P2 hashes; W2 schemas/calculation; PAY-KI-001 through PAY-KI-006; DEC-KI-026 through DEC-KI-030; unaccepted W3 source at backend 916b49d3929cef4a0100c2029c3951a54551b589
produces: final strict adapter; delayed SQS continuation; task and aggregation monitors; byte-stable recovery; isolated reproducible keyword package; frozen component/integration/build proof accepted directly by KI-W4
assigned_agent_policy: one_window
authorized_write_scope: email_scraper/src/aws-pipeline/keyword-intelligence/dataforseo-labs-adapter.js executeProviderAttempt/scheduleKnownRetry/settlementFence only; email_scraper/src/aws-pipeline/keyword-intelligence/contracts.js overviewRequestSchema only; email_scraper/src/aws-pipeline/keyword-intelligence/service.js processKeywordMessage/processTask/recoverClaimedTask/processAggregateCheck/readArtifact/readManifest/aggregateExpansion/aggregateAnchor/aggregateMarket/failStage/sendKeywordMessage/sendSameTaskMessage/createKeywordLeaseMonitor/withLeaseBoundary/prepareTerminalLease/stopReleasedLease only; email_scraper/src/aws-pipeline/adapters/queue-dispatcher.js SqsDispatcher.sendOne optional delay parameter only; email_scraper/scripts/build-keyword-worker.js buildKeywordWorkerPackage cleanup only; email_scraper/test/keyword-intelligence-adapter.test.js repository/attempt helpers plus replacement of the stale-settlement expectation and additive SCN-KI-024 test symbols only; email_scraper/test/keyword-intelligence-worker.test.js memoryS3/memoryDispatcher/runtimeFor/withIsolatedDb helpers plus additive SCN-KI-012/024/025 test symbols only; email_scraper/test/keyword-intelligence-worker-flow.test.js statefulRepository/memoryS3/memoryDispatcher/runtimeFor/drive helpers plus additive SCN-KI-025/026 test symbols only; email_scraper/test/aws-pipeline-runtime-adapters.test.js additive SCN-KI-025 SqsDispatcher.sendOne delay test symbols only; email_scraper/test/aws-pipeline-packaging.test.js additive SCN-KI-027 keyword-worker test symbols only
shared_file_scope: queue-dispatcher.js only the backwards-compatible sendOne fourth parameter because all existing callers omit it; aws-pipeline-runtime-adapters.test.js and aws-pipeline-packaging.test.js only the named additive cases; no existing assertion may be weakened or removed
read_only_scope: email_scraper/src/aws-pipeline/keyword-intelligence/keys.js; email_scraper/src/aws-pipeline/keyword-intelligence/handler.js; email_scraper/src/aws-pipeline/keyword-intelligence/recovery.js; email_scraper/test/keyword-intelligence-recovery.test.js; all keyword fixture files; email_scraper/src/aws-pipeline/adapters/artifact-store.js; email_scraper/src/aws-pipeline/adapters/sqs-batch.js; email_scraper/src/aws-pipeline/core/canonical.js; email_scraper/src/aws-pipeline/core/lease-monitor.js; email_scraper/src/keyword-intelligence/repository.js; email_scraper/prisma/**; all accepted W1/W2/KI-R1/KI-R2 output files; frontend/**; historical git blobs named in A2
authorized_actions: [named local source/test edits, focused static/unit diagnostics during editing, one frozen focused isolated-database gate after final edit, one frozen focused non-database gate, one frozen existing-handler build/measure plus two keyword builds, one frozen npm_test, one frozen secret_scan, append handoff evidence, one-version A5 CAS to AWAITING_REVIEW]
prohibited_actions: [provider_calls, AWS_operations, production_database_writes, full_database_integration_suite, repeated_acceptance_database_runs, prisma_generate_or_validate, raw_body_restore, repository_or_schema_or_migration_edits, API_or_frontend_or_package_edits, existing_test_weakening, commits_or_pushes, KI-W4_work]
successor: KI-W4
successor_reserved_for: parent
may_start_successor: false
```

Parent-review status (`EV-KI-W3-04`, `EV-KI-W3-05`): the initial W3 handoff is
rejected and remains unaccepted. KI-R2 is now accepted and tracked; this same
unaccepted W3 lifecycle is reopened under `DEC-KI-030`. The original T1/T2
capability boxes and every original oracle are cumulative final-state
obligations. `KI-W3-RT1`–`RT4` are unique remediation tasks for the actual
current source. This A4 block is the complete executable authority; the former
standalone W3 plan is historical and must not be consulted for choices.

- [ ] `KI-W3-P1` A5 has assignment `ASG-KI-W3-REOPEN-05`, state 94, only `KI-W3` authorized, A1/A4 hashes equal the files, `accepted_through:KI-R2`, `next_window:KI-W4`, `stop_after:KI-W3`, and `may_start_successor:false`. Evidence: ___
- [ ] `KI-W3-P2` Backend is clean at `916b49d3929cef4a0100c2029c3951a54551b589`; frontend is clean at `0dfa1acac50fac3a86d02ec674c6d2bab645832d`; repository/unit/integration hashes are respectively `e2cad9ea0d47adca3baeb28261da7a09ad775e5fc15c1ecde33f132d7387ee39`, `1a2168af81e97f9b0cd239d594362e8a0856754f6b0783efa8c2f134843a77a2`, and `e1572edeaac65612421fe4b6ae20e979f2aeed16ed94e0b8229b1a6f94856bcc`; accepted `EV-KI-R1-13` and `EV-KI-R2-04/06/07` exist. Reuse their database proof without rerunning it. Evidence: ___
- [ ] `KI-W3-P3` An isolated non-production `TEST_DATABASE_URL` is available through `test/helpers/isolated-postgres.js`; mocked HTTP/S3/SQS and deterministic monitor/clock seams load without live provider/AWS credentials; config snapshot fixes `$3.00000000`, nine markets, and all `DEC-KI-009` formulas. Evidence: ___
- [ ] `KI-W3-P4` Record root relocation state, the clean nested worktrees, and the fourteen P4 file hashes in `EV-KI-W3-05`; reproduce all eight `DEC-KI-030` findings by read-only inspection before editing. Evidence: ___

#### Task block `KI-W3-T1`

1. **Task:** implement strict three-endpoint adapter, normalized cache, attempt
   ledger, durable throttle, single-attempt retry scheduler, and safe errors.
2. **Requirements/decisions:** `REQ-KI-022`, `INV-KI-008`–`009`, `DEC-KI-007`–`009`,
   `026`, `PAY-KI-001`–`005`.
3. **Source:** `KeywordSearchVolume/pipeline/client.py` only as behavioral source;
   historical evidence blobs and certificates in A2; existing strict adapters.
4. **Target:** adapter/contracts/owned fixtures/tests only.
5. **Interface/schema:** exact request/response certificates; one
   `executeProviderAttempt({task,config,clock,http,repository})` union of
   cacheHit/succeeded/retryAt/failed/ambiguous/lost.
6. **Algorithm:** validate durable request → cache lookup → throttle claim →
   `recordAttempt` exposure check/reservation and pre-call attempt row → one timed POST →
   strict parse → classify → settle reported actual cost for every known
   response, cache only a normalized success, or retain the reservation only on
   ambiguity; never
   alternate paths. Budget denial performs zero HTTP calls and terminally fails
   with `KEYWORD_PROVIDER_BUDGET_EXHAUSTED`.
7. **Operations:** repository pre-call commit before HTTP; HTTP before result
   cache/attempt terminal transaction; response-loss is ambiguous.
8. **Atomicity:** provider boundary is `RECOVERED_BOUNDARY` exactly D2/D6;
   cache+attempt outcome is one DB transaction.
9. **Identities:** request/cache/attempt/jitter formulas `DEC-KI-007`–`009`;
   provider timestamp not trusted for durable ordering.
10. **Failure/replay:** exact classifications `PAY-KI-002`; ambiguous never
    repeats; a known retry calls `scheduleRetry` with the persisted failed
    attempt number and the repository derives/replays the durable due time; it
    is redelivered only when due; known retry ≤5; duplicate cache/terminal attempt reconstructs;
    lease loss prevents post-call publication and marks ambiguity if outcome
    cannot be committed.
11. **Dependencies/bounds:** native fetch/AbortController; 120s timeout; 30rpm;
    provider overview ceiling 700 but this design sends at most 300 in the
    anchor task and 200 in each remaining-market task; max five attempts;
    strict one-task envelope; exact `DEC-KI-009` USD policy.
12. **Callers/obsolete:** worker service caller; do not port raw writer,
    `items[].key`, single-market, or broad exception fallbacks.
13. **Tests:** every payload certificate positive/boundary/missing/malformed/
    unknown case; exact HTTP/body/header redaction; cache fresh/stale; throttle;
    each retry code and attempt5; timeout/response-loss/crash positions; exact
    reservation, settlement, ambiguous exposure, and budget denial with zero
    call. Negative control enabling alias/retry-after-ambiguity/over-budget call
    must fail.
14. **Output:** safe adapter used by `KI-W3-T2`.
15. **Non-goals:** no live call, pricing inference, worker orchestration/UI/API.

- [ ] `KI-W3-T1` Perform the fully specified adapter change above.

#### Task block `KI-W3-T2`

1. **Task:** implement strict message/artifact/key contracts and initialize,
   expansion-task, anchor-screen-task, market-overview-task, aggregate-check,
   and recovery service paths in one handler. In that handler construct a
   keyword-only `S3ArtifactStore` as
   `new S3ArtifactStore({client:runtime.s3Client,
   bucket:runtime.config.awsPipelineBucket,maxBytes:33554432})`; do not alter
   the existing runtime store or its 5,000,000-byte bound.
2. **Requirements/decisions:** `REQ-KI-002`–`005`, `023`, `024`, `INV-KI-002`–`008`,
   `DEC-KI-005`, `006`, `018`, `020`, `022`, `026`, `027`.
3. **Source:** existing AWS contract/handler/service/recovery patterns
   `SRC-KI-016`; repository from accepted KI-R1/KI-R2 and adapter/algorithms from
   W3-T1/W2.
4. **Target:** contracts/keys/service/handler/recovery/build script and tests.
5. **Interface/schema:** `PAY-KI-006`; exactly four message discriminators
   (`keyword.initialize.v1`, `keyword.expansion.task.v1`,
   `keyword.overview.task.v1`, `keyword.aggregate.check.v1`) and the artifact
   common header/types in `DEC-KI-020`; recovery emits those same initialize/task/check
   messages solely from `recover(now)` return rows; handler returns SQS partial
   batch failures. Every dispatch uses
   `runtime.config.awsPipelineKeywordResearchQueueUrl`.
6. **Algorithm:** parse record → load durable row/config → fingerprint check →
   claim/heartbeat → perform exactly discriminator work → validate/put immutable
   artifact → first-terminal DB transition → send check → acknowledge. Aggregate
   strictly follows lifecycle table and manifest algorithms.
7. **Operations:** ordered boundaries are contract load, claim, optional
   provider via T1, S3 put, terminal Neon, SQS check; recovery only reads
   dispatchable durable rows and sends identity messages.
8. **Atomicity:** every boundary classification is D2; final result written S3
   before one fenced Neon publication transaction; no S3/list completion.
9. **Identities:** `DEC-KI-002`, `005`, `006`, `009`, `020`, `026`, `027`;
   producedAt is projected from the exact durable `createdAt` source in
   `DEC-KI-027`; keys cannot be supplied by message.
10. **Failure/replay:** matrix in lifecycle table; duplicate/out-of-order/stale
    generation/token no-op or safe failure; artifact conflict terminal; SQS send
    failure recovered; tab/API irrelevant; no cancellation.
11. **Dependencies/bounds:** existing AWS SDK/Zod/Prisma adapters; leases
    `DEC-KI-022`; batch event supported but each record isolated; concurrency1;
    task/object/call limits `DEC-KI-024`; keyword-only artifact store
    maxBytes33554432; existing pipeline artifact store remains 5000000.
12. **Callers/obsolete:** dedicated Lambda and recovery schedule; no existing
    pipeline handler modified; no queueDrain/provider path.
13. **Tests:** `SCN-KI-001`, `004`–`007`, `012`, `013`; inject before/after
    every external/durable boundary; verify artifacts/counters/messages/calls;
    nonempty run must reach every message type. Negative controls bypass task
    table or S3 validation and must fail.
14. **Output:** built handler and durable service consumed by W4 and deployment.
15. **Non-goals:** API, frontend, SAM edits, live provider/AWS, whole-job call.

- [ ] `KI-W3-T2` Perform the fully specified worker change above.

#### Task block `KI-W3-RT1`

1. **Task:** make provider settlement, undecodable-response ambiguity, overview
   bounds, and SQS retry delay conform exactly to `DEC-KI-030`.
2. **Requirements/decisions:** `REQ-KI-002`, `004`, `021`–`024`,
   `INV-KI-002`, `007`–`009`, `012`, `DEC-KI-007`–`009`, `026`, `030`,
   `PAY-KI-001`–`005`.
3. **Source:** P4 hashes for `dataforseo-labs-adapter.js`, `contracts.js`, and
   `queue-dispatcher.js`; `EV-KI-W3-04/05`; literal repository settlement union
   in `DEC-KI-026`; current SQS adapter command at `SRC-KI-016`.
4. **Target:** only `executeProviderAttempt`, `scheduleKnownRetry`, private
   `settlementFence(settled,{attempt,providerCostUsd})`, `overviewRequestSchema`, and
   `SqsDispatcher.sendOne`, plus the exact additive test symbols in the window
   header.
5. **Interface/schema:** retain the five-argument
   `executeProviderAttempt({task,config,clock,http,repository})` union; add no
   adapter parameter. `overviewRequestSchema.keywords[*]` is string 1..160.
   `sendOne(queueUrl,message,schema,{delaySeconds}={})` is the exact optional
   interface and rejects extra option keys/noninteger/out-of-range values.
6. **Algorithm:** validate request/fingerprint → cache → throttle → durable
   attempt reservation → one HTTP call → decode/classify → settle known cost
   and optional cache → classify the returned task fence → only an active fence
   may schedule known retry or return known task outcome. On body decode failure
   other than HTTP 401, mark ambiguity once and return only after
   `terminal|found`. Apply the exact delay formula in `DEC-KI-030` after the
   service stops the voluntarily released monitor.
7. **Operations:** DB cache/throttle/attempt before HTTP; one HTTP; DB
   settlement before any adapter result; durable retry transition before SQS
   send. No S3 operation occurs in this task.
8. **Atomicity:** attempt+cache settlement and retry/defer remain the accepted
   DB transactions; HTTP and SQS are recovered boundaries. A failed delayed
   send leaves `nextAttemptAt` for recovery.
9. **Identities:** existing canonical request/cache/attempt fingerprints only;
   delay is `max(0,ceil((retryAt-now)/1000))`, maximum 900; cost strings remain
   fixed-eight-decimal; no provider timestamp is persisted.
10. **Failure/replay:** terminal/found active settlement continues; stale/missing
    settlement returns lost and makes zero schedule/S3/terminal calls;
    settlement conflict/invalid union fails closed; decode failure is ambiguous
    and never repeats; an identical known-response replay uses `fenceActive`;
    early delayed duplicate acknowledges without a call; cancellation remains
    unsupported.
11. **Dependencies/bounds:** native fetch, AbortSignal timeout 120s, one-element
    provider body, max five attempts, throttle 2000ms, SQS delay 0..900, seed
    strings 1..100, overview strings 1..160 and array 1..700, W3 work counts
    300/200.
12. **Callers/obsolete:** `runProviderAttempt` remains the only production
    caller; all old three-argument `sendOne` callers remain byte-compatible.
    Remove the lost-settlement-success test expectation and immediate retry
    dispatch; preserve every existing queue caller and payload fixture.
13. **Tests:** table all three endpoints and known failure classes across
    `terminal/active-found/lost/stale-found/conflict`; assert stale cases make
    zero `scheduleRetry`; table JSON decode failure at HTTP 200/429/500 and
    assert one ambiguity, zero settle/schedule; assert overview 160 reaches HTTP
    and 161 makes zero attempt/HTTP; assert exact `DelaySeconds` at 0/1/75/900
    and reject -1/901/fraction/extra key. Negative control maps a stale
    settlement to active and must falsify the no-publication/call-count oracle.
14. **Output:** strict adapter and delayed dispatcher consumed by RT2 and the
    final handler build.
15. **Non-goals:** no provider call, endpoint/version discovery, raw body/log,
    retry pricing change, queue topology, repository/schema/runtime-config/API/
    frontend/package edit.

- [ ] `KI-W3-RT1` Perform the fully specified final adapter/continuation change above. Evidence: ___

#### Task block `KI-W3-RT2`

1. **Task:** make ordinary task execution lease-aware across reconstruction,
   provider, S3, recovery, terminalization, and delayed/check dispatch.
2. **Requirements/decisions:** `REQ-KI-002`, `004`, `005`, `021`–`024`,
   `INV-KI-004`–`009`, `DEC-KI-018`, `020`, `022`, `026`–`030`.
3. **Source:** P4 service/worker test hashes; accepted R2 `heartbeat` and live
   `terminalize`; existing lease monitor; `EV-KI-W3-04/05`.
4. **Target:** only the task-side service symbols,
   `createKeywordLeaseMonitor`, `withLeaseBoundary`, `prepareTerminalLease`,
   `stopReleasedLease`, and exact worker/flow test symbols named in the window
   header; repository, monitor core, handler,
   recovery dispatcher, keys, fixtures, and artifact store are read-only.
5. **Interface/schema:** optional third `dependencies` argument on
   `processKeywordMessage` containing only `createLeaseMonitor`; default is the
   real monitor. `createKeywordLeaseMonitor({kind:"task",runtime,
   createLeaseMonitor,taskId,token})` constructs `{intervalMs:20000,
   now:()=>nowOf(runtime),
   renew(now)=>repository.heartbeat({taskId,token},now)}` and non-claimed renewal
   throws exact code `PIPELINE_LEASE_LOST`.
   `withLeaseBoundary`, `prepareTerminalLease`, and `stopReleasedLease` have the
   exact call orders and suppression rule in `DEC-KI-030`; no lease-context or
   alternative wrapper is added.
6. **Algorithm:** load/fingerprint → claim → construct monitor → assert around
   recovery/reconstruction → assert around provider → branch voluntary release
   or prepare terminal → for success assert around immutable S3 put →
   `renewNow/stop/assertActive` → terminalize → send check. Succeeded recovery
   validates reconstructed input/request and cache/attempt fingerprints and
   builds a succeeded artifact with the durable provider cost.
7. **Operations:** Neon claim → monitored DB/S3/provider work → S3 before Neon
   terminal → SQS check after terminal; retry/defer/ambiguity clears lease before
   delayed/no dispatch as `DEC-KI-030` specifies.
8. **Atomicity:** provider, S3, and SQS remain recovered boundaries;
   `terminalize` is the authoritative DB fence. A crash after S3 produces an
   immutable orphan that exact recovery matches; no partial Neon result becomes
   visible.
9. **Identities:** message/task/request fingerprints and deterministic artifact
   key unchanged; `producedAt=task.createdAt`; recovered cost is the exact
   fixed-eight-decimal `latestAttempt.providerCostUsd`; clock is runtime-injected.
10. **Failure/replay:** monitor loss before/after provider or S3 prevents later
    publication; strict response still settles global cache/cost; stale delivery
    returns lost; after-settle/after-S3 crash reclaims from cache with zero HTTP;
    retry SQS failure relies on recovery; post-terminal check failure relies on
    ready-stage recovery; duplicate terminal is immutable; no cancellation.
11. **Dependencies/bounds:** 60s task lease/20s monitor, operation continues for
    more than 120s in the fake-clock proof, one HTTP per invocation, max one task
    artifact, existing 32MiB keyword store, no new dependency.
12. **Callers/obsolete:** handler and component/integration tests call the same
    public function; preserve initialize and aggregate discrimination. Replace
    cacheHit-style succeeded recovery and unobserved monitor use; preserve
    ownerless messages and recovery projection.
13. **Tests:** execute boundary matrix before attempt, after marker/before send,
    after parse/before settle, after settle/before S3, after S3/before terminal,
    after terminal/before check; redeliver identical message and assert exact
    HTTP/S3/attempt/counter/check counts. Run a real-repository fake-clock case
    with renewals at T0+20/40/60/80/100/120s, B reclaim at exact last expiry,
    stale A loss, then recovery at B expiry; assert one paid call, settled cost,
    byte-identical artifact, one counter/check. Negative control suppresses
    `assertActive` and must falsify the zero-S3-after-loss oracle.
14. **Output:** durable task artifacts/counters/checks consumed by RT3 and W4
    status/result reads.
15. **Non-goals:** no repository/schema/fixture/key/handler/recovery/API/frontend/
    infrastructure edit, live call, owner field in worker data, or cancellation.

- [ ] `KI-W3-RT2` Perform the fully specified task-monitor/recovery change above. Evidence: ___

#### Task block `KI-W3-RT3`

1. **Task:** apply one exact aggregation monitor lifecycle to expansion,
   anchor, market, and failed-stage terminal paths.
2. **Requirements/decisions:** `REQ-KI-002`–`005`, `023`, `024`,
   `INV-KI-004`–`007`, `DEC-KI-005`, `006`, `018`, `020`, `022`,
   `026`–`030`.
3. **Source:** current aggregate service symbols at P4 hash; accepted R2
   `heartbeatAggregator` and live publish/fail methods; `EV-KI-W3-04/05`.
4. **Target:** only aggregate-side service, the same four exact private lease
   helpers owned by RT2, and component harness symbols named in the window
   header.
5. **Interface/schema:** `createKeywordLeaseMonitor({kind:"aggregation",
   runtime,createLeaseMonitor,researchId,stage,generation,token})` uses
   `{intervalMs:40000,now:()=>nowOf(runtime),renew(now)=>
   repository.heartbeatAggregator({researchId,stage,generation,token},now)}`;
   every aggregate helper receives the monitor and calls exact
   `withLeaseBoundary(monitor,operation)` and
   `prepareTerminalLease(monitor)` behavior fixed by `DEC-KI-030`.
6. **Algorithm:** claim aggregator → start monitor → load/validate context and
   stage fingerprint → fail a failed task or execute the exact stage aggregate;
   assert before/after each S3 get/put → build exact manifest/tasks/result →
   renew/stop/assert → invoke one matching fail/publish transaction → dispatch
   only on terminal/found publication. Always stop in finally.
7. **Operations:** Neon aggregator claim → monitored Neon reads/S3 reads → pure
   calculation → monitored S3 writes → one final fenced Neon transaction → SQS
   next tasks/check; final market has no successor dispatch.
8. **Atomicity:** S3-before-Neon is recovered and deterministic; publish/fail is
   one accepted R1/R2 transaction; local monitor is advisory and repository
   token+live expiry remains authoritative.
9. **Identities:** stage/task keys/fingerprints and `stage.createdAt` producedAt
   unchanged; exact one US task and eight ordered remaining-market task IDs;
   aggregation token is never messaged or persisted in artifacts.
10. **Failure/replay:** renewal loss blocks the next external/terminal action;
    stale final predicate returns lost and sends nothing; S3 orphan is
    byte-identical on reclaim; empty anchor or calculation failure calls the
    fenced fail path and reports stage_failed only on terminal/found; completed
    aggregate claim returns found without work; duplicate/reordered checks
    commute; no cancellation.
11. **Dependencies/bounds:** 120s aggregation lease/40s monitor, representative
    operation runs beyond 240s in fake time; candidate 1..300, shortlist 1..200,
    task counts 1/8, artifact max 32MiB, sequential S3 operations, no new package.
12. **Callers/obsolete:** aggregate-check discriminator remains sole caller;
    replace the unmonitored helpers and outcome-discarding `failStage`; preserve
    W2 calculation/ranking and accepted repository source.
13. **Tests:** cover expansion, anchor, market, failed-task, empty-anchor, and
    calculation-failure branches; make a representative S3 read span
    T0+40/80/120/160/200/240s; exercise loss before read, during read, before
    put, after put/before publication, and before failStage; assert no later
    S3/Neon/SQS, exact monitor intervals/calls, one publication/counter, and
    finally cleanup. Negative control makes `assertActive` a no-op after renewal
    loss and must falsify the zero-S3/publication-local-oracle while the durable
    repository fence still prevents Neon publication.
14. **Output:** three durable manifests, ordered next-stage work, and one fenced
    final result/default selection consumed by W4.
15. **Non-goals:** no ranking/scoring change, repository/monitor-core/artifact-
    store edit, parallel aggregation, S3 listing completion, API/frontend/AWS.

- [ ] `KI-W3-RT3` Perform the fully specified aggregation-monitor change above. Evidence: ___

#### Task block `KI-W3-RT4`

1. **Task:** isolate and prove the keyword Lambda build and reconcile W3 test
   ownership without changing runtime behavior.
2. **Requirements/decisions:** `REQ-KI-002`, `023`, `024`, `INV-KI-002`,
   `DEC-KI-001`, `024`, `027`, `029`, `030`, D9.
3. **Source:** current keyword build hash; existing seven-handler build/measure
   scripts and packaging suite; `EV-KI-W3-04/05`.
4. **Target:** `buildKeywordWorkerPackage` cleanup statements and additive
   keyword assertions in the packaging test only; retain the already tracked
   worker-flow test as an explicitly owned W3 component harness.
5. **Interface/schema:** retain `KEYWORD_LAMBDA_HANDLERS=["keyword-worker"]`,
   `REQUIRED_PRISMA_ENGINE`, ESM banner, exported
   `buildKeywordWorkerPackage()`, output `.lambda-build/keyword-worker` and
   `dist/lambda/keyword-worker.zip`.
6. **Algorithm:** assert dependencies → remove only own staging/archive → create
   roots → bundle → copy only Prisma client/one AL2023 engine → normalize times →
   sorted zip; repeat build and compare exact archive hash/inventory.
7. **Operations:** local filesystem/build only; no network, database, provider,
   AWS, Git staging, or package installation.
8. **Atomicity:** build output is disposable local output; failure may leave only
   the keyword-owned paths partial and must not alter sibling paths.
9. **Identities:** archive/staging names above; fixed 1980 ZIP timestamps;
   lexicographic file order; SHA-256 hashes for sibling and two-run comparison.
10. **Failure/replay:** rerun removes stale own members and is byte-reproducible;
    missing dependency/engine/zip failure fails closed; sibling sentinel/hash
    mismatch fails acceptance; cleanup removes only test sentinels/temp extract.
11. **Dependencies/bounds:** installed esbuild/zip/unzip/Node24/Prisma; exactly
    one `libquery_engine-rhel-openssl-3.0.x.so.node`; ZIP ≤45MiB, unzipped
    ≤200MiB, artifact store constant 33554432; no sourcemap/docs/tests/fixtures/
    env/credential paths.
12. **Callers/obsolete:** local W3 build and later W7 packaging consume it;
    remove shared-root deletion and stale-own-ZIP accumulation; preserve
    `build-lambda.js`, its seven handlers, measurements, and all existing
    packaging assertions.
13. **Tests:** seed/build/measure seven handlers, snapshot every non-keyword
    staging/archive/measurement hash, place an obsolete member in keyword-owned
    staging/archive, build twice, assert obsolete absent, siblings identical,
    two keyword ZIP hashes identical, inventory/engine/privacy/bounds valid,
    cold import has exported handler and performs no work. Negative control
    invokes an in-memory/source-mutated shared-root cleanup path and the sibling
    sentinel/hash oracle must fail; production source remains restored.
14. **Output:** reproducible keyword Lambda ZIP and inventory/startup evidence
    consumed by W7; explicit ownership of the retained flow harness.
15. **Non-goals:** no shared build/measure source edit, dependency/package
    change, infrastructure/deployment, commit/push, or deletion outside the two
    keyword-owned build paths and test-created sentinels/temp extraction.

- [ ] `KI-W3-RT4` Perform the fully specified build-isolation/test-ownership change above. Evidence: ___

- [ ] `KI-W3-V1` Execute `SCN-KI-001`, `004`–`007`, `012`, `013`, and `024`–`027`; record every listed activation witness, exact call/row/object/clock oracle, and negative control. Evidence: ___
- [ ] `KI-W3-V2` After the final source/test edit, run exactly once: `node --test --test-isolation=none test/keyword-intelligence-adapter.test.js test/keyword-intelligence-worker-flow.test.js test/keyword-intelligence-recovery.test.js test/aws-pipeline-runtime-adapters.test.js`; then run exactly once with isolated DB opt-in: `ALLOW_DATABASE_TESTS=true node --test --test-isolation=none --test-name-pattern='SCN-KI-001|SCN-KI-007|SCN-KI-012|SCN-KI-024' test/keyword-intelligence-worker.test.js`. All selected tests pass, every selected DB test executes (zero skip), and the run-created schemas are absent afterward. Evidence: ___
- [ ] `KI-W3-V3` Assert five seeds produce exactly ten US expansion tasks, one US anchor-screen task, and eight remaining-market tasks: 19 first-pass calls/task artifacts, three manifests, one final artifact, at most 95 attempt rows/calls across five attempts, and never more than one HTTP call per invocation.
- [ ] `KI-W3-V4` Assert messages/logs/errors/artifacts/cache exclude forbidden raw/private fields and owner access cannot be inferred from cache.
- [ ] `KI-W3-V5` Assert the keyword handler uses maxBytes 33554432 while an independently constructed existing pipeline runtime still uses maxBytes 5000000; neither store is shared with the other's handler.
- [ ] `KI-W3-V6` On the frozen tree, run `npm run build:lambda` once and `npm run measure:lambda` once; snapshot SHA-256 for all seven non-keyword staging trees/ZIPs and `dist/lambda/measurements.json`; run `node scripts/build-keyword-worker.js` twice and require identical keyword ZIP hashes, unchanged sibling hashes, no stale sentinel, one AL2023 engine, no forbidden files, ZIP ≤45MiB, unzipped ≤200MiB, and a cold import exporting `handler`. Then run `node --test --test-isolation=none test/aws-pipeline-packaging.test.js` once. Evidence: ___
- [ ] `KI-W3-V7` Against the same frozen tree and build outputs, run `npm test` exactly once and `npm run check:secrets` exactly once. Run neither Prisma command nor the full opted-in database suite. A later edit reruns only gates whose named inputs changed per `DEC-KI-029`. Evidence: ___
- [ ] `KI-W3-H1` Record files/symbols/build artifacts. Evidence: ___
- [ ] `KI-W3-H2` Record commands/scenarios/outcomes/skips. Evidence: ___
- [ ] `KI-W3-H3` Diff matches scope. Evidence: ___
- [ ] `KI-W3-H4` No successor/prohibited action. Evidence: ___
- [ ] `KI-W3-H5` Append evidence; A5 `AWAITING_REVIEW` by CAS. Evidence: ___
- [ ] `KI-W3-H6` Stop; do not begin `KI-W4`. Parent acceptance reruns only `SCN-KI-024`–`027` decisive oracles and, on success, assigns `KI-W4` directly; a further W3 correction is not a successful branch. Evidence: ___

Correction note (`CHG-KI-014`): `EV-KI-W3-07` rejects the second W3 handoff and
supersedes only the prospective acceptance/successor language in `KI-W3-H6` and
the W3 header. The unchecked W3 boxes remain historical and are not executable.
The sole live path is the unique `KI-R3` window below; its passing parent review
establishes cumulative W3 acceptance and may then assign KI-W4.

### `KI-R2` — Conditional keyword lease renewal and terminal fences

```yaml
window_id: KI-R2
objective: Supply the missing aggregation heartbeat and make every ordinary keyword task/aggregation renewal and terminal write require a live durable lease.
depends_on: [KI-R1]
consumes: accepted KI-R1 repository; EV-KI-W3-04; DEC-KI-022; DEC-KI-026; DEC-KI-028; existing Prisma keyword lease columns; existing isolated-postgres harness
produces: one corrected repository lease surface and SCN-KI-022 integration proof usable by reopened KI-W3
assigned_agent_policy: one_window
authorized_write_scope: email_scraper/src/keyword-intelligence/repository.js symbols PrismaKeywordResearchRepository.heartbeat, PrismaKeywordResearchRepository.heartbeatAggregator (new), PrismaKeywordResearchRepository.terminalize, PrismaKeywordResearchRepository.claimAggregator, PrismaKeywordResearchRepository._completeStageAndCreateNext, PrismaKeywordResearchRepository.publishResearchResult, PrismaKeywordResearchRepository.failStage only; email_scraper/test/keyword-intelligence-repository.test.js KI-R2 describe/cases only; email_scraper/test/keyword-intelligence-repository.integration.test.js SCN-KI-022 helpers/cases only
shared_file_scope: repository.js only the seven named methods; repository unit/integration files only additive KI-R2 cases and the exact public-surface list
read_only_scope: email_scraper/prisma/schema.prisma; email_scraper/prisma/migrations/**; email_scraper/src/aws-pipeline/core/lease-monitor.js; email_scraper/src/aws-pipeline/repositories/pipeline-coordinator-repository.js renewAggregator pattern; all W3 source/build/fixture/test files at f9457de; all accepted W1/W2/KI-R1 files outside the named symbols; A1-A8 and this execution plan
authorized_actions: [local_source_edits, local_mocked_tests, isolated_test_database_writes, documentation_and_evidence_updates]
prohibited_actions: [W3_source_build_fixture_or_test_edits, provider_calls, AWS_operations, production_database_writes, schema_or_migration_edits, package_or_frontend_or_API_edits, build_output_changes, commits]
successor: KI-W3
successor_reserved_for: parent
may_start_successor: false
```

- [x] `KI-R2-P1` A5 assigns only KI-R2, pins the current A1/A4 hashes, remains accepted only through KI-R1, and stops after KI-R2. Evidence: `EV-KI-R2-01`.
- [x] `KI-R2-P2` Baseline is backend clean at `f9457deaee19fdfa1f9c1e33152a143d69753c3c`; the three owned-file SHA-256 values are `c4d0a07713d24418fa49d89582da683449f87c188a13bdedfef3416063baec0b`, `0c2b28b9d77f0c85db296d4fb8149ad63365739998cb259b991d3d16733dd6ad`, and `7eafb0eb3700da59a29a761ea2a4ddbf1bd8d3fea7f2b87fef6ee6ddd40ba7bc`; frontend is clean at `0dfa1acac50fac3a86d02ec674c6d2bab645832d`; root relocation state is preserved. Evidence: `EV-KI-R2-01`.
- [x] `KI-R2-P3` An isolated `TEST_DATABASE_URL` distinct from production is available through `test/helpers/isolated-postgres.js`; no live credentials are printed and no public schema is used. Evidence: `EV-KI-R2-01`, `EV-KI-R2-04`.
- [x] `KI-R2-P4` Reproduce the gaps before editing: no `heartbeatAggregator`; task heartbeat update lacks `leaseExpiresAt:{gt:now}`; aggregator reclaim uses `{lt:now}`; and ordinary terminal/publication/failure update predicates lack live-expiry checks. Evidence: `EV-KI-R2-01`.

#### Task block `KI-R2-T1`

1. **Task:** correct only the repository-side lease interface and predicates
   enumerated by `DEC-KI-028`.
2. **Requirements/decisions:** `REQ-KI-002`, `INV-KI-005`–`007`,
   `DEC-KI-022`, `026`, `028`.
3. **Source:** accepted repository at the P2 hash; Prisma keyword lease columns;
   existing coordinator `renewAggregator` only as a read-only transaction
   pattern; `EV-KI-W3-04` contradiction evidence.
4. **Target:** the seven repository methods and additive cases in the two exact
   test files named in this window header; no other symbol or file.
5. **Interface/schema:** retain
   `heartbeat({taskId,token},now) -> {outcome:"claimed",leaseExpiresAt}|{outcome:"lost"}`;
   add
   `heartbeatAggregator({researchId,stage,generation,token},now) -> {outcome:"claimed",leaseExpiresAt}|{outcome:"lost"}`;
   keep every other public union and every Prisma column unchanged.
6. **Algorithm:** validate exact identity/token/time; derive aggregation stage
   ID; renew from injected `now` by 60/120 seconds only when the stored lease is
   strictly live; make exact-expiry aggregator reclaim eligible; require a
   strictly live lease both in the loaded-row guard and the terminal
   `updateMany` predicate for each ordinary terminal path.
7. **Operations:** task and aggregation heartbeat are each exactly one
   conditional `updateMany` and no read; existing publication transactions
   remain single transactions and add only the live-expiry predicate.
8. **Atomicity:** `SAME TRANSACTION` for terminal paths; count zero maps to
   `lost` and commits no counter, stage, manifest, task-set, result, selection,
   or research mutation. No process timer is authoritative.
9. **Identities:** existing task ID and `keywordStageId(researchId,stage,generation)`
   only; existing random tokens unchanged; `now+60000ms` and `now+120000ms`
   exactly, with no wall-clock call and no extension from old expiry.
10. **Failure/replay:** wrong/missing/terminal/expired renewal returns `lost`;
    same live token can renew repeatedly; at expiry the old token loses and a
    claimant may reclaim; after reclaim the old token cannot renew,
    terminalize, publish, or fail. Exact already-completed publication replay
    remains `found`; deliberately post-provider `settleAttempt` and
    `markAttemptAmbiguous` behavior is untouched.
11. **Dependencies/bounds:** Prisma client already installed; task lease 60s,
    task heartbeat 20s, aggregation lease 120s, aggregation heartbeat 40s;
    zero new dependencies, migrations, tables, indexes, queues, calls, or
    artifacts.
12. **Callers/obsolete:** reopened W3 service is the sole new caller of
    `heartbeatAggregator`; it will use the existing lease-monitor abstraction.
    Do not edit W3 now and do not add a second monitor or repository wrapper.
13. **Tests:** add fail-closed unit surface assertions and execute
    `SCN-KI-022` at `expiry-1ms`, exact expiry, and `expiry+1ms` for two owners;
    assert update/query counts and byte/row equality; preserve all
    `SCN-KI-020/021` tests. Negative controls separately remove the token,
    state, and live-expiry predicates and must make the matching stale-owner
    assertion fail. Implement the negative-control seam as the additive test
    helper `clientWithRemovedTaskHeartbeatPredicate(client,key)`, modelled on
    the existing Proxy wrappers: it intercepts only
    `keywordResearchTask.updateMany`, clones the argument, deletes exactly one
    of `leaseToken`, `state`, or `leaseExpiresAt` from `where`, and delegates
    every other path/argument unchanged. Do not patch production source for a
    negative control.
14. **Output:** accepted repository surface on which W3 can implement and prove
    both 20/40-second monitors without editing predecessor code.
15. **Non-goals:** no W3 adapter/service/build/test repair; no new lease
    duration/configuration; no schema/API/payload/artifact/provider/AWS/frontend
    change; no commit.

- [x] `KI-R2-T1` Perform the fully specified repository lease correction above. Evidence: `EV-KI-R2-01`, superseding verification `EV-KI-R2-04`.
- [x] `KI-R2-V1` Run `SCN-KI-022` in a disposable non-public schema and retain all `SCN-KI-020/021` cases unchanged and passing. Evidence: `EV-KI-R2-04` (33/33 final second-attempt integration result; original cases unchanged).
- [x] `KI-R2-V2` Run `node --test --test-isolation=none test/keyword-intelligence-repository.test.js`; run the isolated integration file with database opt-in; run `npm run db:generate`, `npm run db:validate`, and `npm run check:secrets`. Evidence: `EV-KI-R2-04` (unit 11/11, integration 33/33, Prisma and secret gates pass).
- [x] `KI-R2-V3` Run `npm test`; if localhost suites hit the documented sandbox `listen EPERM`, rerun those identical suites with sandbox approval and record both outcomes. Evidence: `EV-KI-R2-04` (482 pass / 0 fail / 61 skip).
- [x] `KI-R2-V4` Assert the exact public repository method set adds only `heartbeatAggregator`; assert schema/migrations/package/W3/frontend paths are byte-identical to P2 and `git diff --name-only` is exactly the three owned files. Evidence: `EV-KI-R2-04`.
- [x] `KI-R2-V5` With `clientWithRemovedTaskHeartbeatPredicate`, execute three independent task-heartbeat controls deleting `leaseToken`, `state`, then `leaseExpiresAt`; prove the wrong-token, terminal-row, and expired-owner assertions respectively fail while the production source remains byte-identical. Evidence: `EV-KI-R2-04`.
- [x] `KI-R2-H1` Record exact changed methods/files, commands, scenarios, row/call counts, skips, and negative-control failures in A6. Evidence: `EV-KI-R2-04`.
- [x] `KI-R2-H2` Drop only schemas created by this run and prove no run-specific disposable schema remains; never clean public. Evidence: `EV-KI-R2-04` (post-drop exact absence assertion and no `kir1%` leftovers).
- [x] `KI-R2-H3` Recompute the three owned-file hashes and prove every prohibited/read-only path remains unchanged. Evidence: `EV-KI-R2-04`.
- [x] `KI-R2-H4` No W3 remediation, provider call, AWS action, production write, schema/migration/package/frontend/build change, or commit occurred. Evidence: `EV-KI-R2-04` for the executor run; later requester-owned commits are recorded separately and do not alter this execution assertion.
- [x] `KI-R2-H5` Append evidence and CAS A5 to `AWAITING_REVIEW` with `accepted_through: KI-R1`, `next_on_pass: KI-W3`, and the current A1/A4 hashes. Evidence: `EV-KI-R2-04` (A5 state 90).
- [x] `KI-R2-H6` Stop; do not reopen or begin KI-W3. Evidence: `EV-KI-R2-04`.

#### Requester-reopened KI-R2 proof gate

This subsection supersedes only the unaccepted completion claim in
`EV-KI-R2-04`; it does not rewrite `KI-R2-T1`, `SCN-KI-022`, or their observed
historical results. The requester explicitly directed reuse of the still
unaccepted `KI-R2` window ID. That is a disclosed exception to the authoring
standard's unique-window-ID rule. The new task ID `KI-R2-RT2`, scenario ID
`SCN-KI-023`, assignment ID, evidence IDs, and state version remain unique; this
package does not claim strict conformance to `PT-007` for the window ID itself.

```yaml
window_id: KI-R2
objective: Close the two remaining lease-boundary activation-witness gaps without changing the already-correct repository implementation.
depends_on: [KI-R1, KI-R2-T1 implementation at dad2b41802e5b823d64d57fab67aea5a75712b25]
consumes: DEC-KI-028; DEC-KI-029; repository.js sha256 e2cad9ea0d47adca3baeb28261da7a09ad775e5fc15c1ecde33f132d7387ee39; EV-KI-R2-04 observed results; existing isolated-postgres harness
produces: SCN-KI-023 exact-expiry task-renewal denial and post-reclaim stale-aggregation-renewal denial, plus one frozen pre-handoff evidence set
assigned_agent_policy: one_window
authorized_write_scope: email_scraper/test/keyword-intelligence-repository.integration.test.js additive SCN-KI-023 helper/test symbols only; KEYWORD_INTELLIGENCE_EXECUTION_EVIDENCE.md append-only KI-R2 handoff entry; ACTIVE_EXECUTION_STATE.md CAS handoff update
shared_file_scope: integration test file only at new SCN-KI-023 symbols; existing SCN-KI-020 through SCN-KI-022 symbols are read-only
read_only_scope: email_scraper/src/keyword-intelligence/repository.js; email_scraper/test/keyword-intelligence-repository.test.js; email_scraper/prisma/schema.prisma; email_scraper/prisma/migrations/**; every W3/build/package/frontend file; A1-A4 and A7-A8 during execution
authorized_actions: [add_SCN-KI-023_test_only, fast_local_static_or_unit_diagnostics, one_focused_isolated_database_gate_after_final_edit, one_frozen_npm_test, one_frozen_secret_scan, append_evidence, CAS_A5_to_AWAITING_REVIEW]
prohibited_actions: [production_source_edits, existing_scenario_rewrites, full_database_integration_suite, repeated_acceptance_database_runs, Prisma_generate_or_validate, handler_build_or_measure, provider_calls, AWS_operations, production_database_writes, schema_or_migration_or_package_or_frontend_edits, commits_or_pushes, KI-W3_work]
successor: KI-W3
successor_reserved_for: parent
may_start_successor: false
```

- [x] `KI-R2-RP1` A5 has the unique assignment ID for this reopened proof gate,
  pins the current A1/A4 hashes, authorizes only KI-R2, remains accepted through
  KI-R1, and stops after KI-R2. Evidence: `EV-KI-A-034`, A5 state 91.
- [x] `KI-R2-RP2` Record the clean baseline: backend HEAD
  `dad2b41802e5b823d64d57fab67aea5a75712b25`; repository/unit/integration hashes
  `e2cad9ea0d47adca3baeb28261da7a09ad775e5fc15c1ecde33f132d7387ee39`,
  `1a2168af81e97f9b0cd239d594362e8a0856754f6b0783efa8c2f134843a77a2`, and
  `2cd38a59fc25616ec511738dffa3490f98c3886e93dd524afa217f524b7609d2`;
  frontend HEAD `0dfa1acac50fac3a86d02ec674c6d2bab645832d` clean; preserve the
  owner-controlled root relocation state. Evidence: `EV-KI-R2-05`.
- [x] `KI-R2-RP3` Confirm an isolated non-production `TEST_DATABASE_URL` is
  available through `test/helpers/isolated-postgres.js` without printing it;
  if absent, stop before editing because the final gate cannot be satisfied.
  Evidence: `EV-KI-R2-06`.
- [x] `KI-R2-RP4` By read-only inspection, reproduce exactly two missing
  witnesses: no same-token task heartbeat at original exact expiry, and no
  stale-A aggregation heartbeat plus row-equality assertion after B's renewed
  exact-expiry reclaim. Evidence: `EV-KI-R2-05`.

##### Task block `KI-R2-RT2`

1. **Task ID:** `KI-R2-RT2` adds only the two missing durable activation
   witnesses; it does not change application behavior.
2. **Requirements/decisions:** `REQ-KI-002`, `INV-KI-005`–`007`,
   `DEC-KI-022`, `DEC-KI-028`, `DEC-KI-029`.
3. **Source anchor:** the committed `SCN-KI-022` task and aggregation cases at
   the RP2 integration-test hash, plus the literal predicates in `DEC-KI-028`.
4. **Target anchor:** one new top-level Node test whose name begins exactly
   `SCN-KI-023:` in
   `email_scraper/test/keyword-intelligence-repository.integration.test.js`;
   helper additions, if any, are immediately adjacent and used only by it.
5. **Interface/schema:** invoke the existing `claim`, `heartbeat`,
   `claimAggregator`, and `heartbeatAggregator` unions unchanged; create no
   schema, fixture, exported helper, production interface, or mock envelope.
6. **Ordered algorithm:** call `setupRepo(t,"kir2_rt2")`; in that one disposable
   schema, first create/initialize a
   research and claim task A at `T0`; snapshot its full task and owning-stage
   rows; call A's same-token task heartbeat at exactly `T0+60,000ms`; assert
   `lost` and deep-equal rows. Separately create a ready stage, let aggregator A
   claim at `T0` and heartbeat at `T0+40,000ms` (renewed expiry
   `T0+160,000ms`), let B reclaim at exactly `T0+160,000ms`, snapshot the full
   stage and research rows, call stale A's `heartbeatAggregator` at that same
   instant, then assert `lost` and deep-equal rows.
7. **Durable/external order:** all setup and snapshots use Neon in the
   disposable schema; each tested heartbeat performs its existing single
   conditional update; no HTTP, S3, SQS, provider, AWS, filesystem artifact, or
   production-database operation occurs.
8. **Atomicity/recovery:** each heartbeat is one atomic `updateMany`; count zero
   is the `lost` outcome. The before/after deep equality is the no-visible-write
   recovery oracle; cleanup occurs in `t.after` even after assertion failure.
9. **Identity/time:** use generated valid research/task IDs and distinct valid
   32-character A/B tokens; use the existing fixed test `NOW` as `T0`; the only
   decisive times are exactly `T0+60,000ms`, `T0+40,000ms`, and
   `T0+160,000ms`. No wall clock, `setTimeout`, tolerance, or approximate time.
10. **Failure/replay/concurrency:** the task exact-expiry call proves the old
    owner cannot revive an expired lease; the aggregation schedule proves B is
    the exact-boundary winner and stale A cannot renew after reclaim. Missing,
    wrong-token, terminal, publication, duplicate, restart, cancellation, and
    `+1ms` branches are excluded because unchanged `SCN-KI-022` already covers
    them or because equality and greater-than-expiry take the same predicate
    branch with no other time-dependent code.
11. **Dependencies/bounds:** existing Node, Prisma client, and
    `isolated-postgres.js` only; one schema; zero new dependencies; task lease
    60 seconds; aggregation lease 120 seconds; exactly two decisive stale
    heartbeat calls; zero paid calls and `$0.00` cost.
12. **Callers/obsolete behavior:** tests call existing repository methods
    directly. Preserve every existing test and production caller. Remove or
    replace nothing.
13. **Exact tests/activation/oracles:** run only the focused name pattern
    `SCN-KI-023|SCN-KI-022 V5`. Activation is witnessed by task equality at
    original expiry, B's successful exact renewed-expiry aggregation claim,
    and stale-A aggregation equality after B owns. Reuse the unchanged
    `SCN-KI-022 V5` expiry-predicate Proxy as the representative negative
    control: removing `leaseExpiresAt` must falsify its unchanged `lost` oracle;
    no second negative-control helper is required because RT2 changes no
    production predicate.
14. **Output:** one passing `SCN-KI-023` result and frozen file hashes consumed
    by the KI-R2 handoff and independent parent review.
15. **Non-goals:** no production correction, broad refactor, historical-suite
    rewrite, full Neon suite, schema/client generation, build, W3 work, commit,
    push, provider/AWS action, or new behavior decision.

- [x] `KI-R2-RT2` Perform the fully specified proof-only change above. Evidence: `EV-KI-R2-06`.
- [x] `KI-R2-RV1` After the final local test edit, run exactly once with
  database opt-in in the isolated schema:
  `ALLOW_DATABASE_TESTS=true node --test --test-isolation=none --test-name-pattern='SCN-KI-023|SCN-KI-022 V5' test/keyword-intelligence-repository.integration.test.js`.
  Record individual pass/skip/fail counts and the negative-control assertion.
  Evidence: `EV-KI-R2-06` (2 pass / 0 fail / 0 skip).
- [x] `KI-R2-RV2` Against the same frozen tree, run exactly once
  `npm run check:secrets` and `npm test`. If only the documented localhost
  `listen EPERM` occurs, rerun only those identical failing localhost files with
  sandbox approval and record both outcomes. Evidence: `EV-KI-R2-06`.
- [x] `KI-R2-RV3` Do not run the full database integration suite,
  `db:generate`, `db:validate`, handler build/measure, or historical focused
  suites: their inputs/claims are unchanged and their accepted observations are
  reused under `DEC-KI-029`. Record any diagnostic exception and why it does
  not count as acceptance evidence. Evidence: `EV-KI-R2-06`.
- [x] `KI-R2-RV4` Recompute RP2 hashes; repository and unit hashes must be
  byte-identical, the integration hash may change only for additive
  `SCN-KI-023`, and `git diff dad2b418... --name-only` must name only that
  integration test before documentation handoff updates. Evidence: `EV-KI-R2-06`.
- [x] `KI-R2-RH1` Append one A6 entry containing the assignment/revisions,
  exact commands, frozen hashes, two activation witnesses, negative control,
  counts, cleanup, skips/reuse reasons, mutations, and `$0.00` cost. Evidence: `EV-KI-R2-06`.
- [x] `KI-R2-RH2` Prove the exact disposable schema is absent after the focused
  run and a read-only prefix query finds no run-created `kir2_` schema; never
  inspect, migrate, or clean `public`. Evidence: `EV-KI-R2-06`.
- [x] `KI-R2-RH3` CAS A5 by one state version to `AWAITING_REVIEW`, retain
  `accepted_through: KI-R1`, `next_window: KI-W3`,
  `may_start_successor:false`, and current A1/A4 hashes. Evidence: `EV-KI-R2-06`, A5 state 92.
- [x] `KI-R2-RH4` Stop. Do not accept KI-R2, assign/start KI-W3, edit production
  source, commit, push, or perform provider/AWS/production actions. Evidence: `EV-KI-R2-06`.

### `KI-R3` — Enforcement-complete durable-worker correction

```yaml
window_id: KI-R3
objective: Correct the four escaped W3 runtime defects and make cumulative W3 acceptance mechanically non-vacuous through a literal executable case manifest.
depends_on: [KI-R2, unaccepted KI-W3 source at backend 37a0e0203d265f539b566f1536642cd2f4eb2d99]
consumes: DEC-KI-026 through DEC-KI-031; EV-KI-W3-04/05/06/07; accepted R1/R2 hashes; current ten W3 file hashes in KI-R3-P2
produces: corrected adapter cost result, fully fenced task/recovery terminal and dispatch order, terminal-failure recovery classification, strict delayed-send options, executable case-set proof, and cumulative W3 handoff eligible for direct KI-W4 assignment
assigned_agent_policy: one_window
authorized_write_scope: email_scraper/src/aws-pipeline/keyword-intelligence/dataforseo-labs-adapter.js settlementFence only; email_scraper/src/aws-pipeline/keyword-intelligence/service.js processTask recoverClaimedTask runProviderAttempt only; email_scraper/src/aws-pipeline/adapters/queue-dispatcher.js SqsDispatcher.sendOne only; email_scraper/test/fixtures/keyword-intelligence/ki-r3-enforcement-manifest-v1.json new exact manifest only; email_scraper/test/keyword-intelligence-adapter.test.js additive SCN-KI-028 symbols only; email_scraper/test/aws-pipeline-runtime-adapters.test.js additive SCN-KI-028 symbols only; email_scraper/test/keyword-intelligence-worker.test.js additive SCN-KI-029/030 symbols and existing memoryS3 memoryDispatcher runtimeFor withIsolatedDb helpers only; email_scraper/test/keyword-intelligence-worker-flow.test.js additive SCN-KI-031 symbols and existing statefulRepository memoryS3 memoryDispatcher runtimeFor drive helpers only; email_scraper/test/keyword-intelligence-enforcement.test.js new SCN-KI-032 structural gate only; KEYWORD_INTELLIGENCE_EXECUTION_EVIDENCE.md append-only KI-R3 handoff; ACTIVE_EXECUTION_STATE.md one-version CAS handoff
shared_file_scope: production files only the four named symbols; existing test helpers only additive parameters/counters needed by named cases; existing assertions and SCN-KI-001 through SCN-KI-027 are immutable
read_only_scope: email_scraper/src/keyword-intelligence/repository.js; email_scraper/prisma/**; email_scraper/src/aws-pipeline/keyword-intelligence/contracts.js; email_scraper/src/aws-pipeline/keyword-intelligence/keys.js; email_scraper/src/aws-pipeline/keyword-intelligence/handler.js; email_scraper/src/aws-pipeline/keyword-intelligence/recovery.js; email_scraper/src/aws-pipeline/core/lease-monitor.js; email_scraper/scripts/build-keyword-worker.js; email_scraper/test/aws-pipeline-packaging.test.js; email_scraper/test/keyword-intelligence-repository.test.js; email_scraper/test/keyword-intelligence-repository.integration.test.js; email_scraper/test/keyword-intelligence-recovery.test.js; all pre-existing fixtures; frontend/**
authorized_actions: [read_only_preconditions, named_local_source_and_test_edits, smallest_static_or_unit_diagnostics_during_editing, one_final_non_database_gate, one_final_focused_isolated_database_gate, two_keyword_worker_builds, one_unchanged_packaging_test, one_frozen_npm_test, one_frozen_secret_scan, append_handoff_evidence, one_version_A5_CAS]
prohibited_actions: [provider_calls, AWS_operations, production_database_writes, full_database_integration_suite, repeated_acceptance_database_runs, prisma_generate_or_validate, seven_handler_build_or_measure, repository_or_schema_or_migration_or_contract_or_key_or_handler_or_recovery_or_build_script_edits, API_or_frontend_or_package_edits, existing_test_or_fixture_rewrite, source_mutation_negative_controls, commits_or_pushes, KI-W4_work]
successor: KI-W4
successor_reserved_for: parent
may_start_successor: false
```

`EV-KI-W3-06` is a historical execution report, not acceptance. KI-R3 is a new
unique corrective window by requester direction. It accepts W3 only if every
literal case below executes and all frozen gates pass; no broad statement such
as “matrix covered”, “monitor tested”, or “all scenarios pass” substitutes for
the case IDs, traces, counts, mutations, or set-equality certificates.

- [ ] `KI-R3-P1` A5 assigns exactly `ASG-KI-R3-01`, authorizes only `KI-R3`,
  pins current A1/A4 hashes, records `accepted_through:KI-R2`,
  `next_window:KI-W4`, `stop_after:KI-R3`, and
  `may_start_successor:false`. Evidence: ___
- [ ] `KI-R3-P2` Backend is clean at
  `37a0e0203d265f539b566f1536642cd2f4eb2d99`; frontend is clean at
  `0dfa1acac50fac3a86d02ec674c6d2bab645832d`. Record these current hashes in
  A6 before editing: adapter `9c47e815dfd21c6f406ee4c883de807466203965809908ad499434dc69077695`,
  contracts `e37b38d6129204127f9b2aa25779162ab6d8ea32e24be391fd04cac3ddcb7b29`,
  service `39e1caf49cfa440ff0bd3ad86ef81eada371085e16c5934bc78a5b25a5312cc8`,
  queue dispatcher `455eb9928d727ce005fa30d3a4731155634d0e916896036e0f623a37be4d1ae2`,
  build script `0667c6b40e9bc2d92759fe17d86ccfed51f9d1d0647aaeb5dbc91a66a3b1b935`,
  adapter test `d9f82b30fa210f63e03f518ea34a4f0e5aae173d2bc4af7f898fb5b9223de43b`,
  worker test `780e9194cb355d4ad2ac9e708fa8b7a1b10f7c21af9dcdf901b2b116fe0091bf`,
  worker-flow test `4742849582c1ae9fccc77379b98e3c33cbe7946946c9f3e9dde53832184e1ca4`,
  runtime-adapter test `270952329c7ea59c77a72ccc6b5fe8c25bf9e08a1f55d22d2fe85db4679909fb`,
  and packaging test `4ea3dbdd40b511002523c2e9b51a28bfedb2a3ef1d0c1f6edf2d3cf07329e6f3`.
  Evidence: ___
- [ ] `KI-R3-P3` Recompute and match the accepted read-only repository/unit/
  integration hashes `e2cad9ea0d47adca3baeb28261da7a09ad775e5fc15c1ecde33f132d7387ee39`,
  `1a2168af81e97f9b0cd239d594362e8a0856754f6b0783efa8c2f134843a77a2`,
  and `e1572edeaac65612421fe4b6ae20e979f2aeed16ed94e0b8229b1a6f94856bcc`;
  confirm one isolated non-production `TEST_DATABASE_URL` through
  `test/helpers/isolated-postgres.js` without printing it. Reuse R1/R2 database
  evidence; do not rerun it. Evidence: ___
- [ ] `KI-R3-P4` Reproduce R3-F1 through R3-F6 from `DEC-KI-031` with the exact
  counterexample operations in `EV-KI-W3-07`, record root relocation state,
  and confirm no run-created `kir1%|kir2%|kiw3%|kir3%` schema exists. Evidence: ___

#### Task block `KI-R3-T1`

1. **Task ID:** `KI-R3-T1` corrects settlement cost projection and delayed-send
   option strictness.
2. **Requirements/decisions:** `REQ-KI-021`–`023`, `INV-KI-002`,
   `INV-KI-008`–`009`, `DEC-KI-009`, `026`, `030`, `031`.
3. **Source anchor:** current `settlementFence` and `SqsDispatcher.sendOne` at
   the P2 hashes; current result/command expectations in the two named tests.
4. **Target anchor:** the same two production symbols; additive
   `SCN-KI-028` blocks in `keyword-intelligence-adapter.test.js` and
   `aws-pipeline-runtime-adapters.test.js`.
5. **Interface:** retain `executeProviderAttempt` unchanged; use the exact
   settlement union and exact `sendOne(...,options = {})` interface in
   `DEC-KI-031`; no export or error code is added.
6. **Ordered behavior:** classify settlement → preserve its supplied cost in
   both active/lost results → return/throw exact union; parse message → validate
   plain options/key/value → construct original or delayed command → send → map
   sent/failed IDs.
7. **Persistence contract:** no schema/write change; `settleAttempt` remains the
   only attempt/cache transaction and the dispatcher remains stateless.
8. **Boundary mapping:** fixed-eight-decimal strings are passed through without
   numeric conversion; options accept exactly `{}` or `{delaySeconds:int}`.
9. **Failure/retry semantics:** exact members from `DEC-KI-031`; invalid options
   throw `PIPELINE_MESSAGE_INVALID` before `client.send`; SQS client failure
   remains `{sentItemIds:[],failedItemIds:[logicalId]}`.
10. **Fixed configuration:** delay integer `0..900`; no dependency/config/env
    change.
11. **Call-site/removal map:** all existing three-argument dispatcher callers
    remain unchanged; remove no helper; `markAmbiguousOnce` remains the named
    private helper.
12. **Verification map:** execute the `adapter` and `dispatcher` groups of the
    exact manifest below; assert result deep equality, thrown safe code, and
    operation trace/call count for every ID.
13. **Output:** known outcomes expose their settled cost and null/non-plain
    delayed options cannot reach SQS.
14. **Non-goals:** provider parsing, repository logic, service lifecycle,
    contracts, build, live calls.
15. **Handoff:** record changed lines, every executed case ID, trace-set
    certificate, command result, and exact post-edit hashes.

#### Task block `KI-R3-T2`

1. **Task ID:** `KI-R3-T2` fences the ordinary provider/S3/terminal/check path.
2. **Requirements/decisions:** `REQ-KI-002`, `005`, `021`–`023`,
   `INV-KI-004`–`009`, `DEC-KI-022`, `026`, `028`, `030`, `031`.
3. **Source anchor:** `processTask` and `runProviderAttempt` at the P2 service
   hash; accepted `heartbeat`/`terminalize` contracts are read-only.
4. **Target anchor:** the same two service symbols; additive component members
   in `keyword-intelligence-worker.test.js`.
5. **Interface:** add required private `monitor` to `runProviderAttempt`; retain
   every public message/runtime/dependency/result interface; inline the exact
   monitored `{status,json}` HTTP view from `DEC-KI-031`.
6. **Ordered behavior:** context → claim → monitor → recovery T3 → reconstruct
   → adapter with monitored HTTP → voluntary-release result or monitored S3 put
   → renew-stop-assert → terminalize → gate exact outcome → optional check.
7. **Persistence contract:** no repository/schema edit; S3 remains before the
   live task terminal predicate; known settlement may durably store cost/cache
   after a post-send lease loss, but stale ownership cannot write S3 or terminal.
8. **Boundary mapping:** provider trace is
   `assert,http,assert,assert,json,assert`; S3 trace is
   `assert,s3.put,assert`; terminal trace is
   `renew,stop,assert,terminalize[,sendCheck]`.
9. **Failure/retry semantics:** pre-send loss makes zero HTTP; post-send/decode
   loss takes one ambiguity path; S3 loss stops before terminal; only
   `terminal|found` sends a check; exact public outcomes are in `DEC-KI-031`.
10. **Fixed configuration:** 20,000ms monitor, 60,000ms repository task lease,
    120-second provider timeout, at most one HTTP per invocation.
11. **Call-site/removal map:** `processTask` is the sole caller changed for the
    new private `monitor` argument; no named helper, export, or abstraction is
    added; aggregate paths are read-only.
12. **Verification map:** execute manifest group `task_component`; each case
    asserts its full ordered operation trace and zero forbidden suffix calls.
13. **Output:** ordinary task processing cannot send a check for a nonterminal
    fence and cannot cross a detected provider/S3 lease boundary.
14. **Non-goals:** repository, aggregation behavior, recovery scheduler,
    artifact schema, API/frontend/build changes.
15. **Handoff:** record exact source/test diff, case IDs/traces, negative-control
    failure, focused command result, and residual risk.

#### Task block `KI-R3-T3`

1. **Task ID:** `KI-R3-T3` makes claimed-task recovery use the same lease,
   terminal, release, and provider-failure classification rules as ordinary work.
2. **Requirements/decisions:** `REQ-KI-002`, `005`, `022`, `023`,
   `INV-KI-004`–`009`, `DEC-KI-007`, `009`, `020`, `022`, `026`, `028`,
   `030`, `031`.
3. **Source anchor:** current `recoverClaimedTask`; read-only repository
   projections/unions and existing artifact/request builders.
4. **Target anchor:** `recoverClaimedTask` only, plus additive component and
   isolated-database cases in `keyword-intelligence-worker.test.js`.
5. **Interface:** use the exact input and two-member internal return union in
   `DEC-KI-031`; no public export or repository callable changes.
6. **Ordered behavior:** classify latest durable attempt → validate exact
   identity/cache or exact failed safe code → choose ambiguity, byte-stable S3
   recovery, retry release, or terminal failure → apply monitored/fenced order
   → gate dispatch/result.
7. **Persistence contract:** existing atomic settle/cache and terminalize rows
   only; succeeded cache identity is triple-checked; immutable S3 put precedes
   terminal; terminal provider failures preserve the latest safe code and never
   call `scheduleRetry`.
8. **Boundary mapping:** the six recovery schedules in `DEC-KI-031` are
   exhaustive; any state/code/member outside them is
   `PIPELINE_INPUT_CONFLICT`.
9. **Failure/retry semantics:** exact no-repeat, retryable-only, attempt-five,
   missing-cache ambiguity, terminal outcome gate, delayed-send recovery, and
   stale-owner behavior in `DEC-KI-031`.
10. **Fixed configuration:** max five attempts; retry delay is the repository's
    persisted value; SQS delay `ceil((retryAt-now)/1000)` in `0..900`; no sleep.
11. **Call-site/removal map:** `processTask` passes its monitor; no change to
    `recoverKeywordWork`, repository, artifact builder, or message schema.
12. **Verification map:** execute manifest groups `recovery_component` and
    `task_database`; the database group is the sole KI-R3 database acceptance
    run and uses one generated non-public schema.
13. **Output:** a crash after any known response resumes without reclassifying a
    terminal failure as retryable or bypassing the lease fence.
14. **Non-goals:** new attempt states, cache TTL, schema/migration, live provider,
    general recovery redesign.
15. **Handoff:** record exact durable before/after rows, object/message/call
    counts, schema name/absence, manifest coverage, and `$0.00`.

#### Task block `KI-R3-T4`

1. **Task ID:** `KI-R3-T4` materializes and enforces the complete corrective
   case set and revalidates unchanged aggregation/build behavior required for
   cumulative W3 acceptance.
2. **Requirements/decisions:** `REQ-KI-002`–`005`, `023`, `024`,
   `INV-KI-002`, `INV-KI-004`–`007`, `DEC-KI-029`–`031`.
3. **Source anchor:** case tables below; current aggregation service is
   read-only; current `SCN-KI-027` and build script hashes are read-only.
4. **Target anchor:** new exact JSON manifest, additive `SCN-KI-031` in
   worker-flow tests, and new `keyword-intelligence-enforcement.test.js` for
   manifest/schema/scope/helper conformance.
5. **Interface:** manifest root is exactly
   `{contractVersion:"ki-r3-enforcement-manifest-v1",groups}`; `groups` has
   exactly `{adapter,dispatcher,task_component,recovery_component,
   task_database,aggregation,conformance}` and each value is the literal ordered
   case-ID array below.
6. **Ordered behavior:** parse strict manifest → assert key and ID set equality
   → run every ID once as a named subtest → record trace/result/count → assert
   expected equality → run injected mutation → prove the unchanged oracle fails
   → rerun production collaborator and pass.
7. **Persistence contract:** aggregation tests use stateful in-memory contracts;
   only T3's task database group writes one disposable schema; builds write only
   gitignored keyword staging/ZIP.
8. **Boundary mapping:** trace alphabets and expected traces are literal below;
   an unknown trace operation fails, not ignored.
9. **Failure/retry semantics:** duplicate, missing, skipped, `.todo`, or
   unexecuted manifest IDs; missing negative-control failure; source-helper
   additions; or changed read-only hashes fail the window.
10. **Fixed configuration:** exact case counts below; one non-DB gate, one DB
    gate, two keyword builds, one package test, one regression, one secret scan.
11. **Call-site/removal map:** existing SCN-KI-001–027 and package/build source
    are immutable; no general test framework or production dependency is added.
12. **Verification map:** `SCN-KI-031` exercises every aggregation publication/
    failure outcome and external boundary; `SCN-KI-032` proves manifest,
    changed-symbol, changed-file, private-helper, and prohibited-import sets.
13. **Output:** machine-readable proof that claimed corrective coverage equals
    executed coverage, with no trust in narrative handoff counts.
14. **Non-goals:** rerunning all predecessor database suites, changing build
    cleanup, generic instrumentation library, W4.
15. **Handoff:** A6 must embed the generated group counts, sorted executed-ID
    hashes, negative-control failures, source hashes, build hashes/sizes, exact
    commands/outcomes, skips/reuse, cleanup, mutations, cost, and stop statement.

#### Exact `ki-r3-enforcement-manifest-v1` case set

The JSON arrays contain these IDs in this order; no other ID is permitted:

| Group (count) | Literal case IDs |
|---|---|
| `adapter` (16) | `R3-A01-active-terminal-success-cost`, `R3-A02-active-found-success-cost`, `R3-A03-active-terminal-retry-cost`, `R3-A04-active-found-terminal-cost`, `R3-A05-lost-zero-schedule`, `R3-A06-not-found-zero-schedule`, `R3-A07-stale-found-zero-schedule`, `R3-A08-conflict-fails-closed`, `R3-A09-terminal-missing-fence-fails-closed`, `R3-A10-found-missing-fence-fails-closed`, `R3-A11-decode-200-ambiguous-once`, `R3-A12-decode-429-ambiguous-once`, `R3-A13-decode-500-ambiguous-once`, `R3-A14-ambiguity-terminal-accepted`, `R3-A15-ambiguity-found-accepted`, `R3-A16-ambiguity-other-fails-closed` |
| `dispatcher` (12) | `R3-Q01-omitted-no-delay-member`, `R3-Q02-empty-no-delay-member`, `R3-Q03-zero-delay`, `R3-Q04-nine-hundred-delay`, `R3-Q05-null-rejected`, `R3-Q06-array-rejected`, `R3-Q07-primitive-rejected`, `R3-Q08-fraction-rejected`, `R3-Q09-negative-rejected`, `R3-Q10-over-nine-hundred-rejected`, `R3-Q11-extra-key-rejected`, `R3-Q12-nonplain-rejected` |
| `task_component` (18) | `R3-T01-success-terminal-check`, `R3-T02-success-found-check`, `R3-T03-success-lost-no-check`, `R3-T04-success-conflict-no-check`, `R3-T05-success-not-found-no-check`, `R3-T06-failure-terminal-check`, `R3-T07-failure-found-check`, `R3-T08-failure-lost-no-check`, `R3-T09-failure-conflict-no-check`, `R3-T10-failure-not-found-no-check`, `R3-T11-loss-before-http-zero-call`, `R3-T12-loss-during-fetch-ambiguity`, `R3-T13-loss-during-json-ambiguity`, `R3-T14-loss-before-s3`, `R3-T15-loss-during-s3`, `R3-T16-loss-after-s3-before-terminal`, `R3-T17-six-renewals-over-120s`, `R3-T18-terminal-gate-negative-control` |
| `recovery_component` (18) | `R3-R01-success-terminal-check`, `R3-R02-success-found-check`, `R3-R03-success-lost-no-check`, `R3-R04-success-conflict-no-check`, `R3-R05-success-not-found-no-check`, `R3-R06-cache-missing-terminal-ambiguity`, `R3-R07-cache-expired-terminal-ambiguity`, `R3-R08-cache-fingerprint-mismatch-ambiguity`, `R3-R09-planned-attempt-ambiguity-check`, `R3-R10-auth-failure-no-retry`, `R3-R11-contract-failure-no-retry`, `R3-R12-task-failure-no-retry`, `R3-R13-retryable-delayed-send`, `R3-R14-attempt-five-exhausted-terminal`, `R3-R15-delayed-send-failure-durable`, `R3-R16-monitor-stopped-before-dispatch`, `R3-R17-unknown-failed-code-conflict`, `R3-R18-recovery-fence-negative-control` |
| `task_database` (5) | `R3-D01-after-settle-before-s3-recover`, `R3-D02-after-s3-before-terminal-recover`, `R3-D03-terminal-failure-crash-no-retry`, `R3-D04-retryable-crash-schedules-once`, `R3-D05-renewed-expiry-stale-owner-denied` |
| `aggregation` (24) | `R3-G01-expansion-terminal-dispatch`, `R3-G02-expansion-found-dispatch`, `R3-G03-expansion-lost-no-dispatch`, `R3-G04-expansion-conflict-no-dispatch`, `R3-G05-expansion-not-found-no-dispatch`, `R3-G06-anchor-terminal-dispatch`, `R3-G07-anchor-found-dispatch`, `R3-G08-anchor-lost-no-dispatch`, `R3-G09-anchor-conflict-no-dispatch`, `R3-G10-anchor-not-found-no-dispatch`, `R3-G11-market-terminal-publish`, `R3-G12-market-found-publish`, `R3-G13-market-lost-no-publish`, `R3-G14-market-conflict-no-publish`, `R3-G15-market-not-found-no-publish`, `R3-G16-fail-terminal-stage-failed`, `R3-G17-fail-found-stage-failed`, `R3-G18-fail-lost-propagated`, `R3-G19-fail-conflict-propagated`, `R3-G20-fail-not-found-propagated`, `R3-G21-loss-during-get-no-later-call`, `R3-G22-loss-during-put-orphan-only`, `R3-G23-six-renewals-over-240s`, `R3-G24-monitor-negative-control` |
| `conformance` (8) | `R3-C01-manifest-root-exact`, `R3-C02-group-set-exact`, `R3-C03-global-id-unique`, `R3-C04-private-helper-set-exact`, `R3-C05-production-symbol-diff-exact`, `R3-C06-write-file-set-exact`, `R3-C07-prohibited-import-set-empty`, `R3-C08-no-skip-todo-only` |

The manifest has exactly **101** globally unique IDs. Each scenario computes
`sha256(sortedExecutedIds.join("\n"))`; A6 records the seven group hashes and
the global hash. The conformance test recomputes all counts and hashes from the
manifest; hand-entered evidence counts are not accepted.

#### Exact operation traces and result oracles

Tests record only this alphabet:
`ctx,claim,renew,stop,assert,http,json,cache,markAmbiguous,scheduleRetry,
s3.get,s3.put,terminalize,publishCandidate,publishShortlist,publishResult,
failStage,sendTask,sendCheck`. Unknown operations fail.

- Adapter active cases A01–A04 assert the returned
  `providerCostUsd` is exactly the value supplied to `settleAttempt`; A03 trace
  ends `scheduleRetry`. A05–A07 contain no `scheduleRetry`; A08–A10 throw
  `PIPELINE_INPUT_CONFLICT`; A11–A13 trace one `http`, one `json`, one
  `markAmbiguous`, and zero settlement/schedule; A14–A15 return ambiguous;
  A16 throws. The injected control strips active cost and must falsify A01.
- Q01/Q02 send one command with no own `DelaySeconds`; Q03/Q04 send one command
  with exact `0/900`; Q05–Q12 send zero commands and throw
  `PIPELINE_MESSAGE_INVALID`. The injected control accepting null must falsify
  Q05.
- T01/T02 exact success suffix is
  `s3.put,renew,stop,assert,terminalize,sendCheck`; T03–T05 omit `sendCheck`.
  T06/T07 suffix is `renew,stop,assert,terminalize,sendCheck`; T08–T10 omit
  `sendCheck`. T11 has zero `http`; T12 has one `http`, one `markAmbiguous`, and
  no S3/ordinary terminal/check; T13 additionally has one `json`; T14–T16 allow
  at most one orphan `s3.put` and no terminal/check after the captured loss;
  T17 records six nonoverlapping `renew` operations; T18 makes the unchanged
  no-check assertion fail when the injected terminal gate treats `lost` as
  terminal.
- R01/R02 exact suffix is
  `cache,s3.put,renew,stop,assert,terminalize,sendCheck`; R03–R05 omit
  `sendCheck`. R06–R08 make zero HTTP/retry calls and use
  `renew,stop,assert,terminalize,sendCheck` only for a terminal/found fence;
  R09 is `markAmbiguous,stop,sendCheck`; R10–R12 make zero HTTP/retry calls and
  preserve their exact safe code; R13 is `scheduleRetry,stop,sendTask`; R14 is
  `renew,stop,assert,terminalize,sendCheck`; R15 records failed `sendTask` while
  durable delayed state remains; R16 asserts `stop` precedes `sendTask`; R17
  throws `PIPELINE_INPUT_CONFLICT`; R18's injected unfenced recovery must
  falsify the no-terminal/check assertion.
- D01/D02 each retain one provider attempt/cache, make zero recovery HTTP calls,
  store one immutable object, and expose one terminal counter/check with
  `costUsd:"0.01560000"`; D03 preserves the terminal failure safe code with
  zero schedule/HTTP; D04 creates one durable retry schedule and one due retry,
  never two simultaneous attempts; D05 uses T0 plus six 20-second renewals,
  lets B reclaim at exact renewed expiry, and proves stale A makes zero
  S3/terminal/check writes with task/stage rows deep-equal before/after.
- G01–G15 dispatch next tasks/checks only for `terminal|found`: expansion emits
  one anchor task plus one check, anchor emits eight ordered market tasks plus
  one check, market emits no successor message. G16/G17 report `stage_failed`;
  G18–G20 return the exact repository outcome. G21 loses during `s3.get` and
  has no later put/publication/dispatch; G22 may leave one immutable orphan but
  has no publication/dispatch; G23 records six nonoverlapping 40-second renewals
  across more than 240 seconds and one publication; G24's injected ignored loss
  must falsify the zero-later-call oracle.

- [ ] `KI-R3-T1` Perform the exact adapter/dispatcher task above. Evidence: ___
- [ ] `KI-R3-T2` Perform the exact ordinary task-fence task above. Evidence: ___
- [ ] `KI-R3-T3` Perform the exact recovery-classification task above. Evidence: ___
- [ ] `KI-R3-T4` Materialize the exact manifest and enforcement tasks above. Evidence: ___
- [ ] `KI-R3-V1` After the final non-database edit, run exactly once:
  `node --test --test-isolation=none --test-name-pattern='SCN-KI-028|SCN-KI-029|SCN-KI-031|SCN-KI-032' test/keyword-intelligence-adapter.test.js test/aws-pipeline-runtime-adapters.test.js test/keyword-intelligence-worker.test.js test/keyword-intelligence-worker-flow.test.js test/keyword-intelligence-enforcement.test.js`.
  Every 96 non-database manifest IDs executes exactly once, no selected test
  skips, and all group set/hash assertions and four negative controls pass.
  Evidence: ___
- [ ] `KI-R3-V2` Against the same frozen source/test tree, run exactly once with
  isolated DB opt-in:
  `ALLOW_DATABASE_TESTS=true node --test --test-isolation=none --test-name-pattern='SCN-KI-030' test/keyword-intelligence-worker.test.js`.
  All five database IDs execute with zero skip; exact rows/calls/objects/checks
  match; the generated schema is dropped and an exact-name absence query passes.
  Do not run another DB scenario or the full integration suite. Evidence: ___
- [ ] `KI-R3-V3` Because only keyword package inputs changed, reuse the seven
  sibling/measurements hashes recorded by `EV-KI-W3-06`; run
  `node scripts/build-keyword-worker.js` exactly twice and require identical ZIP
  hashes/inventories, sibling hashes unchanged, no stale member, one AL2023
  engine, ZIP ≤45MiB, unzipped ≤200MiB, and cold import exporting `handler`.
  Then run unchanged `node --test --test-isolation=none
  test/aws-pipeline-packaging.test.js` once. Do not run `build:lambda` or
  `measure:lambda`. Evidence: ___
- [ ] `KI-R3-V4` On the same frozen tree/output, run `npm test` exactly once and
  `npm run check:secrets` exactly once. If a documented sandbox-only localhost
  error occurs, rerun only that identical command with approval and record both
  outcomes. Evidence: ___
- [ ] `KI-R3-V5` Recompute hashes and assert production diff from P2 changes
  only the four authorized symbols; nested `git diff --name-only` equals the
  nine authorized backend paths (three production, five test files, one new
  manifest), except a test file with no needed additive change must be absent,
  never replaced by another path. All read-only hashes match. The service diff
  adds no named function/const/class helper; adapter private additions remain
  exactly the two and service W3-private additions exactly the six in
  `DEC-KI-031`. Evidence: ___
- [ ] `KI-R3-H1` Append `EV-KI-R3-01` containing assignment/revisions, P2/P3
  hashes, changed files/symbols, generated manifest counts/hashes, exact
  commands/outcomes, durable row/object/message/call counts, negative-control
  failures, skipped/reused gates with reasons, cleanup/absence, mutations,
  residual risks, user prerequisites, and `$0.00`. Evidence: ___
- [ ] `KI-R3-H2` Prove no `kir3%` schema remains, no provider/AWS/production/
  Prisma/seven-handler/frontend/package/commit/push action occurred, and root
  relocation state is preserved. Evidence: ___
- [ ] `KI-R3-H3` CAS A5 exactly one version to `AWAITING_REVIEW`, keep
  `accepted_through:KI-R2`, `next_window:KI-W4`,
  `may_start_successor:false`, and current A1/A4 hashes. Evidence: ___
- [ ] `KI-R3-H4` Stop. Do not accept W3/KI-R3, assign/start KI-W4, commit, push,
  or perform any prohibited action. Parent review uses the generated case-set
  certificate plus decisive R3 cases; only a passing review may assign KI-W4.
  Evidence: ___

Correction note (`CHG-KI-015`): `EV-KI-R3-02` rejects the KI-R3 handoff and
supersedes its prospective acceptance/successor language. The source at
`077213cc7c33fa8209a1e5d8ff365b73766500dc` is the immutable KI-R4 baseline;
KI-R3 execution observations remain history, not acceptance. The unique live
path is KI-R4. Only a passing window-agent assessment followed by independent
parent acceptance establishes cumulative W3 acceptance and permits KI-W4.

### `KI-R4` — Commit-stable enforcement and exhaustive worker correction

```yaml
window_id: KI-R4
objective: Close the remaining R3 production and enforcement gaps and produce commit-stable cumulative W3 acceptance evidence through recursive single-file execution.
depends_on: [KI-R2 accepted, unaccepted KI-R3 source at backend 077213cc7c33fa8209a1e5d8ff365b73766500dc]
consumes: DEC-KI-026 through DEC-KI-032; EV-KI-R3-01/02; exact R3 manifest and source hashes; parent and sub-window authoring standards
produces: exhaustive attempt/task identity fence, exact dispatcher own-key validation, durable case/digest enforcement, valid falsification controls, one-schema named DB cases, commit-stable conformance, and a window-agent integration certificate eligible for parent review
assigned_agent_policy: recursive_window_agent
window_agent_identity: KI-R4-WINDOW-AGENT
window_agent_coordination_write_scope: KEYWORD_INTELLIGENCE_KI_R4_SUBWINDOW_CHECKLIST.md; KEYWORD_INTELLIGENCE_KI_R4_SUBWINDOW_STATE.md; KEYWORD_INTELLIGENCE_KI_R4_SUBWINDOW_EVIDENCE.md
delegable_implementation_write_scope: email_scraper/src/aws-pipeline/keyword-intelligence/service.js recoverClaimedTask only; email_scraper/src/aws-pipeline/adapters/queue-dispatcher.js SqsDispatcher.sendOne only; email_scraper/test/fixtures/keyword-intelligence/ki-r4-enforcement-manifest-v1.json new exact manifest only; email_scraper/test/keyword-intelligence-adapter.test.js additive KI-R4 control and fixed R3 digest assertion only; email_scraper/test/aws-pipeline-runtime-adapters.test.js additive KI-R4 dispatcher cases and fixed R3 digest assertion only; email_scraper/test/keyword-intelligence-worker.test.js recovery fixtures/cases, T18/R18 controls, SCN-KI-030 registration/isolation structure, and fixed R3/R4 digest assertions only; email_scraper/test/keyword-intelligence-worker-flow.test.js G24 control and fixed R3/R4 digest assertions only; email_scraper/test/keyword-intelligence-enforcement.test.js SCN-KI-032 fixed-revision/hashes plus additive KI-R4 conformance only
required_initial_file_set: [email_scraper/src/aws-pipeline/keyword-intelligence/service.js, email_scraper/src/aws-pipeline/adapters/queue-dispatcher.js, email_scraper/test/fixtures/keyword-intelligence/ki-r4-enforcement-manifest-v1.json, email_scraper/test/keyword-intelligence-adapter.test.js, email_scraper/test/aws-pipeline-runtime-adapters.test.js, email_scraper/test/keyword-intelligence-worker.test.js, email_scraper/test/keyword-intelligence-worker-flow.test.js, email_scraper/test/keyword-intelligence-enforcement.test.js]
required_initial_file_set_digest: ccfa1089d1d62656afde3927cd0b42128856713442dcbda5d30dd47a6b5333f6
read_only_scope: email_scraper/src/aws-pipeline/keyword-intelligence/dataforseo-labs-adapter.js; email_scraper/src/keyword-intelligence/repository.js; email_scraper/src/aws-pipeline/core/lease-monitor.js; email_scraper/test/fixtures/keyword-intelligence/ki-r3-enforcement-manifest-v1.json; email_scraper/test/keyword-intelligence-repository.test.js; email_scraper/test/keyword-intelligence-repository.integration.test.js; email_scraper/test/keyword-intelligence-recovery.test.js; email_scraper/test/aws-pipeline-packaging.test.js; email_scraper/scripts/build-keyword-worker.js; email_scraper/prisma/**; frontend/**; A1-A8 except parent-only post-review updates
authorized_actions: [window_agent_create_and_update_only_three_subordinate_artifacts, parent_reviewed_sequential_single_file_delegation, file_local_static_or_unit_checks, one_final_non_database_gate, one_final_focused_isolated_database_gate, two_keyword_worker_builds, one_unchanged_packaging_test, one_frozen_npm_test, one_frozen_secret_scan, window_agent_integration_assessment_and_consolidated_handoff]
prohibited_actions: [window_agent_implementation_file_edits, leaf_multi_file_edits, parallel_leaf_execution, direct_parent_leaf_communication, leaf_subdelegation, parent_A5_or_A6_updates_by_window_agent, provider_calls, AWS_operations, production_database_writes, full_database_integration_suite, repeated_successful_database_gate_without_invalidation, Prisma_generate_or_validate, seven_handler_build_or_measure, repository_schema_migration_contract_key_handler_recovery_build_script_adapter_source_edits, API_frontend_package_edits, source_mutation_controls, commits_or_pushes, KI-W4_work]
subwindow_standard_path: PROJECT_AGNOSTIC_WINDOW_AGENT_SUBWINDOW_AUTHORING_STANDARD.md
subwindow_standard_revision: 1766f9107ce7d315877b75d4b0ea2b5521dff1c321e12f890b03787d66196ded
parent_decomposition_review_required: true
successor: KI-W4
successor_reserved_for: parent
may_start_successor: false
```

The `delegable_implementation_write_scope` is the complete parent-window
implementation boundary, not direct write authority for the window agent. The
window agent must create S1/S2/S3, compile exactly eight sequential one-file
initial sub-windows, and obtain parent decomposition approval before the first
leaf assignment. It may append one-file corrective sub-windows after diagnosed
failures but may never broaden the eight-file set or make a parent-level
decision. Parent and leaf agents communicate only through the window agent.

- [x] `KI-R4-P1` A5 pins both standards and the current A1/A3/A4 revisions,
  assigns only `ASG-KI-R4-WA-01` to `KI-R4-WINDOW-AGENT`, authorizes only
  subordinate-package authoring until decomposition review, retains
  `accepted_through:KI-R2`, names `next_window:KI-W4`, stops after KI-R4, and
  forbids successor start. Evidence: `EV-KI-A-037`, `EV-KI-R4-02`.
- [x] `KI-R4-P2` Backend is clean at
  `077213cc7c33fa8209a1e5d8ff365b73766500dc`; frontend is clean at
  `0dfa1acac50fac3a86d02ec674c6d2bab645832d`. Record exact SHA-256 for all
  eight planned files (`ABSENT` for the new manifest), all protected dirty root
  paths, and the starting repository change-set digest without modifying them.
  Evidence: `EV-KI-R4-S01`, `EV-KI-R4-02`.
- [x] `KI-R4-P3` Reproduce all `EV-KI-R3-02` findings: unequal failed identity
  reaches retry/terminal logic; symbol and non-enumerable extras each send;
  clean-checkout focused gate fails C06/C07 while C05 sees zero hunks; R3 hash
  assertions accept any 64-hex value; D01–D05 are not named subtests and create
  five schemas; A01/T18/R18/G24 controls alter inputs rather than the claimed
  defect. Evidence: `EV-KI-R4-S02`, `EV-KI-R4-02`.
- [x] `KI-R4-P4` The window agent creates exactly S1
  `KEYWORD_INTELLIGENCE_KI_R4_SUBWINDOW_CHECKLIST.md`, S2
  `KEYWORD_INTELLIGENCE_KI_R4_SUBWINDOW_STATE.md`, and S3
  `KEYWORD_INTELLIGENCE_KI_R4_SUBWINDOW_EVIDENCE.md`; copies and checks all 44
  `SW-*` readiness items; proves planned file-set equality/digest; fully authors
  the initial zero-write integration assessment; appends
  `SUBWINDOW-DECOMPOSITION-READY`; and stops at
  `AWAITING_PARENT_DECOMPOSITION_REVIEW`. Evidence: `EV-KI-R4-S03`, `EV-KI-R4-S04`.
- [x] `KI-R4-P5` Parent independently accepts the S1 decomposition before S2
  becomes `READY`; every initial or corrective leaf owns exactly one canonical
  file, and every leaf reports only to the window agent. Evidence: `EV-KI-R4-S04`, `EV-KI-R4-S18`.

#### Task block `KI-R4-T1`

1. **Task ID:** `KI-R4-T1` makes durable attempt/task request identity an
   exhaustive pre-classification fence.
2. **Requirements/decisions:** `REQ-KI-002`, `005`, `022`, `023`;
   `INV-KI-004`–`008`; `DEC-KI-026`, `030`–`032`.
3. **Source anchor:** `recoverClaimedTask` at KI-R4-P2; worker component
   fixtures/cases R09–R17.
4. **Target anchor:** only `recoverClaimedTask` in `service.js`; only the named
   recovery fixtures and additive R4 cases in `keyword-intelligence-worker.test.js`.
5. **Interface/schema:** no signature/export/repository/message/artifact change;
   retain the exact two-member internal return union from DEC-KI-031.
6. **Ordered algorithm:** load latest attempt; if absent proceed; compare exact
   request fingerprints; on inequality throw `PIPELINE_INPUT_CONFLICT`; only on
   equality enter planned/in-flight/succeeded/failed classification unchanged.
7. **Durable/external order:** mismatch performs zero cache, ambiguity, retry,
   HTTP, S3, terminal, task-send, and check-send operations and no durable write.
8. **Atomicity:** read-only fail-closed guard before all existing recovered
   boundaries; existing repository transactions remain unchanged.
9. **Identity/formulas:** byte-for-byte equality of the existing lowercase
   64-hex request fingerprints; null/undefined/different value is unequal.
10. **Failure/replay/concurrency:** every redelivery with unequal durable
    identity fails deterministically; equal replay follows the six accepted
    schedules; no lease or token behavior changes.
11. **Dependencies/bounds:** no new helper/import/dependency/configuration;
    five-attempt and lease bounds unchanged.
12. **Callers/removal/preservation:** `processTask` remains sole caller; remove
    null fingerprints from normal R09–R16 fixtures; preserve every equal-
    identity trace/result.
13. **Tests/cases:** R4-W01 uses planned mismatch and asserts zero
    `markAmbiguous`; W02 uses auth terminal failure mismatch and asserts zero
    terminal/check; W03 uses retryable mismatch and asserts zero schedule/task
    send; each asserts `PIPELINE_INPUT_CONFLICT` and zero forbidden operations.
14. **Output:** recovery cannot act on an attempt belonging to a different
    durable request identity.
15. **Non-goals:** repository validation, new attempt state, retry redesign,
    schema, provider, artifact, API, frontend, build, or helper extraction.

#### Task block `KI-R4-T2`

1. **Task ID:** `KI-R4-T2` enforces the complete own-key set of delayed-send
   options.
2. **Requirements/decisions:** `REQ-KI-021`–`023`, `INV-KI-002`, `008`, `009`,
   `DEC-KI-009`, `031`, `032`.
3. **Source anchor:** `SqsDispatcher.sendOne` at KI-R4-P2 and Q01–Q12.
4. **Target anchor:** only `sendOne` and additive R4 dispatcher cases in
   `aws-pipeline-runtime-adapters.test.js`.
5. **Interface/schema:** signature remains
   `sendOne(queueUrl,message,schema,options={})`; return/error unions unchanged.
6. **Ordered algorithm:** parse message; reject non-plain options; obtain
   `Reflect.ownKeys`; accept `[]` or `['delaySeconds']` only; validate integer
   `0..900`; construct/send the existing command.
7. **Durable/external order:** invalid own-key shape throws before construction
   reaches `client.send`; dispatcher remains stateless.
8. **Atomicity:** N/A, proven by zero durable state and zero client sends on
   rejected cases.
9. **Identity/formulas:** exact own-key identity includes strings and symbols;
   key order is irrelevant because only zero or one key is accepted.
10. **Failure/replay/concurrency:** symbol/non-enumerable extra rejects
    deterministically; valid send failure keeps the existing failed-item union.
11. **Dependencies/bounds:** built-in `Reflect.ownKeys`; no dependency/config.
12. **Callers/removal/preservation:** preserve every three/four-argument caller
    and Q01–Q12 result; replace only `Object.keys` key enumeration.
13. **Tests/cases:** R4-Q01 plain object with one symbol extra and R4-Q02 plain
    object with a non-enumerable `extra` each throw
    `PIPELINE_MESSAGE_INVALID` with zero commands.
14. **Output:** strict delayed options cannot smuggle unvalidated own keys.
15. **Non-goals:** message parsing, batch dispatch, queue configuration, AWS
    calls, retries, or new option fields.

#### Task block `KI-R4-T3`

1. **Task ID:** `KI-R4-T3` replaces vacuous controls and non-durable scope/hash
   assertions with exact commit-stable enforcement.
2. **Requirements/decisions:** `REQ-KI-002`, `021`–`024`;
   `INV-KI-002`, `004`–`009`; `DEC-KI-029`–`032`.
3. **Source anchor:** exact R3 manifest/hash list; existing A01/T18/R18/G24 and
   C01–C08 implementations; Git baseline/end revisions in DEC-KI-032.
4. **Target anchor:** the new R4 manifest and only the authorized test anchors
   in adapter/runtime-adapter/worker/worker-flow/enforcement test files.
5. **Interface/schema:** new strict JSON root is exactly
   `{contractVersion:'ki-r4-enforcement-manifest-v1',groups}` with exactly
   `adapter_control`, `dispatcher`, `worker_component`,
   `aggregation_control`, `conformance`; arrays equal the literal case list
   below in order.
6. **Ordered algorithm:** load strict manifests; compare literal groups/IDs;
   execute each named case; record ID only after activation/oracle; compare
   required=registered=executed; recompute fixed group/global digests; execute
   exact in-memory mutations and capture the expected `AssertionError`;
   inspect fixed Git revisions rather than live status.
7. **Durable/external order:** tests make no provider/AWS/production write;
   Git inspection is read-only; build/database are deferred to integration.
8. **Atomicity:** N/A for in-memory/static controls; the database boundary is
   owned separately by T4.
9. **Identity/formulas:** all path/ID digests use the sub-window-standard
   unsigned-UTF-8/LF/SHA-256 formula; R4 global digest is
   `6adc8ab132496c58608734549fbbc596577e1bd71c1e730349575eb96badc941`.
10. **Failure/replay/concurrency:** missing/extra/duplicate/skipped/unactivated
    case, wrong digest, empty historical production diff, live-status use, or a
    control that fails to produce `AssertionError` fails acceptance.
11. **Dependencies/bounds:** Node built-ins only; exactly 15 R4 IDs and the
    unchanged 101 R3 IDs; no new runtime export/helper/dependency.
12. **Callers/removal/preservation:** permanent SCN-KI-032 uses fixed
    `37a0e020...077213cc`; remove live `git status` and unstaged-only diff;
    replace regex-only digest checks; preserve every production oracle.
13. **Tests/cases:** execute all R4-A01/Q01/Q02/W01–W05/G01/C01–C06 below;
    A01 deletes output cost; W04 injects `sendCheck` into captured lost trace;
    W05 injects `terminalize,sendCheck`; G01 injects the first forbidden
    post-loss operation; each reruns the unchanged oracle and captures its
    assertion failure. C01–C06 enforce fixed nonempty diff, nine historical
    paths, imports, seven group digests, global digest, and worktree independence.
14. **Output:** portable enforcement that remains green after requester and
    successor commits while still proving the frozen R3 change.
15. **Non-goals:** production-source mutation, provider-body cost mutation,
    substituting a different valid terminal outcome, general test framework,
    W4 scope, or Git write.

#### Task block `KI-R4-T4`

1. **Task ID:** `KI-R4-T4` gives the five durable cases one shared isolated
   schema and five real named registrations.
2. **Requirements/decisions:** `REQ-KI-002`, `005`, `022`, `023`;
   `INV-KI-004`–`008`; `DEC-KI-026`, `028`–`032`.
3. **Source anchor:** SCN-KI-030, `t_scn030`, and `withIsolatedDb` at KI-R4-P2.
4. **Target anchor:** only SCN-KI-030/t_scn030 structure in
   `keyword-intelligence-worker.test.js`; production repository/harness read-only.
5. **Interface/schema:** SCN-KI-030 receives Node test context `t`; call
   `withIsolatedDb` once; `t_scn030(caseId,executed,{db,repo})` consumes the
   shared context and does not create/drop a schema.
6. **Ordered algorithm:** create one exact disposable schema; sequentially
   register/await five `t.test(caseId)` cases; append executed ID only after its
   activation/oracle; assert set/digest; outer helper disconnects/drops once and
   proves absence.
7. **Durable/external order:** migrations once before D01; D01–D05 sequential
   with case-local research/task cleanup inside the schema; one final schema
   drop; no public/production access.
8. **Atomicity/isolation:** existing repository transactions unchanged;
   `test/helpers/isolated-postgres.js` remains sole isolation authority.
9. **Identity/formulas:** one generated schema name with `kir4_` prefix for the
   gate; case IDs remain the exact R3 D01–D05 identities and fixed digest
   `9e8a3973d5430be70e26f68bb235b831b96f17162d30277a40b06942cc94e934`.
10. **Failure/replay/concurrency:** a failed subtest still reaches outer cleanup;
    cases are sequential and cannot share business IDs; zero skip required.
11. **Dependencies/bounds:** one migration deployment/schema, five cases, one
    focused database command; no Prisma generate/validate/full suite.
12. **Callers/removal/preservation:** remove five inner `withIsolatedDb` calls;
    preserve every D01–D05 assertion and existing helper implementation.
13. **Tests/cases:** runner output must expose D01–D05 as five named subtests;
    setup/cleanup counters equal one; executed set and fixed digest match; exact
    post-drop absence succeeds.
14. **Output:** observable, economical database enforcement at the required
    parity class.
15. **Non-goals:** new database scenario, repository/schema/migration edit,
    full integration run, parallel cases, public cleanup, or repeated gate.

#### Exact `ki-r4-enforcement-manifest-v1` case set

| Group | Literal ordered IDs |
|---|---|
| `adapter_control` (1) | `R4-A01-active-cost-output-omission-falsifies` |
| `dispatcher` (2) | `R4-Q01-symbol-extra-key-rejected`, `R4-Q02-nonenumerable-extra-key-rejected` |
| `worker_component` (5) | `R4-W01-planned-identity-mismatch-conflict`, `R4-W02-terminal-failure-identity-mismatch-conflict`, `R4-W03-retryable-failure-identity-mismatch-conflict`, `R4-W04-ordinary-lost-check-injection-falsifies`, `R4-W05-recovery-lost-write-injection-falsifies` |
| `aggregation_control` (1) | `R4-G01-post-loss-operation-injection-falsifies` |
| `conformance` (6) | `R4-C01-fixed-revision-diff-nonempty`, `R4-C02-fixed-revision-file-set-exact`, `R4-C03-fixed-revision-import-set-clean`, `R4-C04-r3-group-digests-exact`, `R4-C05-r3-global-digest-exact`, `R4-C06-live-worktree-independent` |

The exact 15-ID global digest is
`6adc8ab132496c58608734549fbbc596577e1bd71c1e730349575eb96badc941`.
The fixed R3 group digests are adapter
`b4ede4c2a1a32fddc1a1ac67e023a81f93c6863632cdff2be421f20d51080e4f`,
dispatcher `962ad70760c71a6fcf08b73d5edf0cdccad27dea9c3414c552c1d8e3e2b99226`,
task_component `d6773f3749e9f68c3b270df9ad63aba6297328b5578d1e5f3346ee2683518110`,
recovery_component `b6d8b7a1435b6a62da061980afd370290f16b899774bba32578e3df9cc5f2737`,
task_database `9e8a3973d5430be70e26f68bb235b831b96f17162d30277a40b06942cc94e934`,
aggregation `c017cd869b11a93e86070112ed626a3cd299e00a518ed3a568dd8f1331c27b14`,
conformance `43bbc0bd4dd296447b989ee2125fc0f991c2451f29e3f4ef87c05f8685a607f8`,
and global 101-ID digest
`70bd758e68cb32aff7dc418356d68e3ca07dadf282f76e7484858a7ec0c9470b`.

### KI-R4 scenarios

#### `SCN-KI-033` — Durable identity and strict own-key partitions

- **Cases:** R4-W01–W03 and R4-Q01–Q02.
- **Activation:** each mismatch reaches the new pre-classification comparison;
  each malformed options object reaches `Reflect.ownKeys` after the plain-
  prototype check.
- **Oracle:** exact safe error plus zero forbidden repository/S3/dispatch/client
  calls; required=registered=executed for these five IDs.
- **Parity:** component with the production service/dispatcher and faithful
  in-memory repository/client unions.

#### `SCN-KI-034` — Exact oracle falsification controls

- **Cases:** R4-A01, R4-W04, R4-W05, R4-G01.
- **Activation:** first run the real production path and unchanged oracle; then
  mutate only the captured result/trace as prescribed by DEC-KI-032 and rerun
  that identical oracle.
- **Oracle:** each of four controls captures `AssertionError`; replacing the
  defect with a different valid input is forbidden; production rerun remains
  passing.
- **Parity:** component oracle-sensitivity proof; it does not claim a second
  production execution path.

#### `SCN-KI-035` — Commit-stable case/diff conformance

- **Cases:** R4-C01–C06.
- **Activation:** fixed-revision Git diff is nonempty; all R3/R4 manifest sets
  and full digests are recomputed; no live-status command is called.
- **Oracle:** exact historical nine-file set and symbol/import boundaries;
  exact seven R3 group/global digests; exact R4 groups/15-ID digest; permanent
  test passes from the clean committed KI-R4 baseline and remains independent
  of unrelated successor paths.
- **Parity:** read-only static conformance.

- [x] `KI-R4-T1` Perform the exact identity-fence task through sequential
  single-file leaves. Evidence: `EV-KI-R4-S18`, `EV-KI-R4-02`.
- [x] `KI-R4-T2` Perform the exact dispatcher own-key task through sequential
  single-file leaves. Evidence: `EV-KI-R4-S18`, `EV-KI-R4-02`.
- [x] `KI-R4-T3` Perform the exact manifest/control/hash/conformance task through
  sequential single-file leaves. Evidence: `EV-KI-R4-S18`, `EV-KI-R4-02`.
- [x] `KI-R4-T4` Perform the exact single-schema named-registration task through
  the worker-test leaf. Evidence: `EV-KI-R4-S18`, `EV-KI-R4-02`.
- [x] `KI-R4-V1` Window agent independently accepts every one-file leaf and
  proves the assembled implementation changed-file set equals the exact eight
  paths and digest in the header; no leaf changed a second file. Evidence: `EV-KI-R4-S18`, `EV-KI-R4-02`.
- [x] `KI-R4-V2` On final frozen non-database inputs, run exactly once:
  `node --test --test-isolation=none --test-name-pattern='SCN-KI-028|SCN-KI-029|SCN-KI-031|SCN-KI-032|SCN-KI-033|SCN-KI-034|SCN-KI-035' test/keyword-intelligence-adapter.test.js test/aws-pipeline-runtime-adapters.test.js test/keyword-intelligence-worker.test.js test/keyword-intelligence-worker-flow.test.js test/keyword-intelligence-enforcement.test.js`.
  All selected top-level tests and named subtests pass with zero skip; all 96
  non-DB R3 IDs and 15 R4 IDs have exact required=registered=executed equality,
  full fixed digests, activation witnesses, and the four exact mutation
  failures. Evidence: `EV-KI-R4-S18`, `EV-KI-R4-02`.
- [x] `KI-R4-V3` Against the same frozen source/test tree and one isolated
  non-production database, run exactly once:
  `ALLOW_DATABASE_TESTS=true node --test --test-isolation=none --test-name-pattern='SCN-KI-030' test/keyword-intelligence-worker.test.js`.
  D01–D05 appear as five named subtests, each executes once with zero skip; one
  schema setup and one cleanup occur; all prior durable oracles and fixed digest
  pass; exact-name absence succeeds. Evidence: `EV-KI-R4-S15`, `EV-KI-R4-S18`, `EV-KI-R4-02`.
- [x] `KI-R4-V4` Run `node scripts/build-keyword-worker.js` exactly twice and
  require identical ZIP hashes, one AL2023 engine, no forbidden/stale member,
  ZIP ≤45MiB, unzipped ≤200MiB, cold import exporting `handler`, and unchanged
  sibling build hashes; then run unchanged
  `node --test --test-isolation=none test/aws-pipeline-packaging.test.js` once.
  Evidence: `EV-KI-R4-S15`, `EV-KI-R4-S18`, `EV-KI-R4-02`.
- [x] `KI-R4-V5` On the same frozen tree/output run `npm test` once and
  `npm run check:secrets` once. The permanent conformance suite must derive its
  R3 assertions only from the fixed revisions in `DEC-KI-032`; it must not
  require, create, or assume a requester commit and must not inspect live
  worktree cleanliness. The parent will independently rerun the same focused
  conformance gate after the requester later commits KI-R4; that later proof is
  an acceptance check, not work delegated to this window. Evidence: `EV-KI-R4-S18`, `EV-KI-R4-02`.
- [x] `KI-R4-V6` Window agent recomputes the cumulative required set (101 R3 +
  15 R4), registered set, and executed set using the normative UTF-8/LF digest
  formula; requires 116 unique IDs, zero skipped/duplicate/unexpected/
  unactivated IDs, four expected/falsified R4 controls, and no unresolved
  substitute-fidelity claim. Evidence: `EV-KI-R4-S18`, `EV-KI-R4-02`.
- [x] `KI-R4-H1` Window agent appends `WINDOW-AGENT-INTEGRATION-PASS` to S3,
  sets S2 to `READY_FOR_PARENT_REVIEW`, and returns only the consolidated
  Section 12.5 handoff; it does not edit A5/A6 or claim parent acceptance.
  Evidence: `EV-KI-R4-S18`.
- [x] `KI-R4-H2` Record exact initial/corrective/assessment IDs, file digests,
  commands/results, coverage sets/digests, controls, DB schema lifecycle, build
  artifacts, skips/reuse, external mutations/cost, and every superseded failed
  assessment. Evidence: `EV-KI-R4-S18`, `EV-KI-R4-02`.
- [x] `KI-R4-H3` Prove no provider/AWS/production/Prisma/full-DB/seven-handler/
  repository/schema/migration/adapter-source/API/frontend/package/commit/push/
  KI-W4 action and no direct parent-leaf communication occurred. Evidence: `EV-KI-R4-S18`, `EV-KI-R4-02`.
- [x] `KI-R4-H4` Stop. Only independent parent review may append parent A6
  acceptance, CAS A5, and assign KI-W4. Evidence: `EV-KI-R4-02`; KI-W4 remains unassigned.

### `KI-W4` — Owner API, durable selection, and direct run/query-review handoff

```yaml
window_id: KI-W4
objective: Expose truthful owner-scoped research control and atomically create an editable research-backed Run containing exactly one lineage-fenced query per retained keyword.
depends_on: [parent acceptance of KI-R4 and cumulative KI-W3]
consumes: accepted KI-R4 backend revision; DEC-KI-003/014/016/017/019/033; accepted W1 repository transaction; accepted W2 selectors/mapper/export; existing auth/probe/dispatch/run paths
produces: five strict backend routes; truthful research view; durable selection CAS; filtered CSV; atomic immutable handoff; research-only edit/confirm branch; 34-case enforcement certificate
assigned_agent_policy: one_window
delegation_policy: one named KI-W4 window agent authors and manages sequential single-file leaves under PROJECT_AGNOSTIC_WINDOW_AGENT_SUBWINDOW_AUTHORING_STANDARD.md
authorized_write_scope: KEYWORD_INTELLIGENCE_KI_W4_SUBWINDOW_CHECKLIST.md coordination only; KEYWORD_INTELLIGENCE_KI_W4_SUBWINDOW_STATE.md; KEYWORD_INTELLIGENCE_KI_W4_SUBWINDOW_EVIDENCE.md append-only
delegable_implementation_file_set: [email_scraper/src/api-serializer.js, email_scraper/src/keyword-intelligence/api.js, email_scraper/src/keyword-intelligence/cluster.js, email_scraper/src/keyword-intelligence/repository.js, email_scraper/src/prisma-run-repository.js, email_scraper/src/query-review.js, email_scraper/src/server.js, email_scraper/test/fixtures/keyword-intelligence/ki-w4-enforcement-manifest-v1.json, email_scraper/test/keyword-intelligence-api.test.js, email_scraper/test/keyword-intelligence-handoff.integration.test.js]
delegable_file_set_digest: fe48d14ebec1dffa058cf91cfa9ec10982d4ceaa4c63e0cb9280cabf39a4a59b
shared_file_scope: repository.js additive getOwnedApiView plus private RunHandoffAbort and createRun invalid-callback throw/catch mapping only; cluster.js additive classifyKeywordForSelection export only; api-serializer.js additive keyword serializers and conditional lineage keys only; prisma-run-repository.js exported newRunId, additive transaction-composable keyword methods, and the exact keyword_research branch inside replaceEditableQueries only; query-review.js additive research validators only; server.js exact imports, dependency injection, five routes, research edit/start/probe discriminators, and no legacy-branch semantic change; the two existing legacy query/server test files are read-only and exercised by npm test; new W4 test files own all W4 registries/negative controls
read_only_scope: A1-A3/A7-A8; accepted KI-R4 S1-S3/evidence; prisma/schema.prisma and migrations; keyword selection/query-mapper/export/config/schemas; api-errors/request-json; AWS keyword message/dispatcher/recovery contracts; existing probe artifacts/confirmed dispatcher; isolated-postgres helper; frontend/**
authorized_actions: [author parent-bounded S1/S2/S3 decomposition, sequentially delegate exactly one listed implementation file per leaf, window-agent independent leaf review, one final non-database gate, one final focused isolated-database gate, one final npm_test, one final secret_scan, one-file corrective leaves inside the same ten-file set, consolidated parent handoff]
prohibited_actions: [window-agent implementation-file edits, parallel leaves, direct parent-leaf communication, schema_or_migration_edits, package_or_lock_edits, config_or_runtime_config_edits, worker_or_recovery_or_dispatcher_edits, frontend_or_infrastructure_edits, provider_calls, AWS_operations, production_database_writes, full_database_integration_suite, Prisma_generate_or_validate, Lambda_build_or_measure, source_mutation_negative_controls, commits_or_pushes, KI-W5_work]
successor: KI-W5
successor_reserved_for: parent
may_start_successor: false
```

- [x] `KI-W4-P1` Active assignment identity, state version, parent/sub-window
  standard revisions, A1/A3/A4 hashes, and exact KI-W4 window-agent identity
  match. Evidence: `EV-KI-W4-S01` (delta-audited observed A3/A4; pins corrected
  by `EV-KI-A-039`/`CHG-KI-017` at A5 state 101).
- [x] `KI-W4-P2` Parent acceptance of KI-R4 and cumulative KI-W3 is recorded;
  backend starts clean at the accepted requester commit and frontend is
  read-only. Evidence: `EV-KI-A-038`, `EV-KI-W4-S01` (backend clean at
  `d98ad53c…`; ending `fac5bb0…` after requester-owned leaf commits), frontend
  `0dfa1aca…` clean throughout.
- [x] `KI-W4-P3` The isolated non-production `TEST_DATABASE_URL`, unchanged
  one-schema harness, mocked dispatcher, mocked probe, and auth request harness
  are available; no external credential is required. Evidence: `EV-KI-W4-I01`
  (`KI-W4-V3`).
- [x] `KI-W4-P4` Starting digests and dirty state for all ten delegable files
  plus protected root/frontend paths are recorded; the sorted-LF path digest is
  exactly `fe48d14e…`. Evidence: `EV-KI-W4-S01` §4–§5.
- [x] `KI-W4-P5` S1/S2/S3 exist; every mandatory `SW-*` item is checked with S3
  evidence; the exact 10-file/34-case decomposition is
  `AWAITING_PARENT_DECOMPOSITION_REVIEW`; no leaf is assigned. Evidence:
  `EV-KI-W4-S03` (44/44).
- [x] `KI-W4-P6` Parent approves the decomposition; only the window agent changes
  S2 to `READY` and assigns the first sequential one-file leaf. Evidence:
  `EV-KI-A-039`, `EV-KI-W4-S04`.

#### Task block `KI-W4-T1` — Owner projection, canonical selection, API service, and serializers

1. **Task:** implement the exact owner projection, additive selection
   classifier, five-method API service, and public serializers in
   `DEC-KI-033`.
2. **Requirements/decisions:** `REQ-KI-001`, `002`, `005`, `007`–`009`,
   `017`, `018`; `INV-KI-003`, `013`, `014`; `DEC-KI-002`–`004`,
   `012`–`015`, `019`, `021`, `033`.
3. **Source:** current `getOwned`, accepted W2 selection/cluster/export/config/
   result schemas, current API error/serializer patterns, and W3 initialize
   message schema.
4. **Target:** only `repository.js/getOwnedApiView` plus its private
   `RunHandoffAbort`/`createRun` invalid-callback rollback path,
   `cluster.js/classifyKeywordForSelection`, the complete new `api.js`, and
   `api-serializer.js` symbols named in the header.
5. **Interface/schema:** literal method signatures, strict inputs, ResearchView,
   selection canonicalization, conditional lineage fields, statuses and safe
   errors are `DEC-KI-019/033`; no child chooses a field or optionality.
6. **Algorithm:** owner-filtered DB projection → strict version/result parsing →
   canonical selection/conflict calculation → exact serialization; create is
   normalize/fingerprint/commit followed by initialize dispatch; export uses the
   exact conjunctive filter/projection/order in `DEC-KI-033`.
7. **Operation order:** rejected input has zero DB/send; accepted create has one
   repository create before one mocked `dispatchInitialize`; read/export have
   one owner projection and zero sends; selection has one owner projection then
   one repository CAS. No provider, S3 or Google operation exists.
8. **Atomicity:** research create and selection CAS remain the accepted
   `SAME_ATOMIC_BOUNDARY`; DB→SQS is the existing queued-row
   `RECOVERED_BOUNDARY`. The new projection is read-only. Invalid callback
   output now throws inside the accepted createRun transaction and is mapped
   only after rollback.
9. **Identities/formulas:** owner only from caller auth; research/item/config/
   selection fingerprints, timestamp and progress formulas are literal in
   `DEC-KI-002/003/033`.
10. **Failure/replay/concurrency:** missing and cross-owner collapse to 404;
    send failure preserves queued state; selection revision has one winner;
    terminal result is immutable; contract drift fails safe; no cancellation.
11. **Dependencies/bounds:** Zod already installed; 1–5 seeds, 0–200 draft,
    1–100 handoff, nine markets, 32-MiB stored result, ≤20 flags; no package or
    schema change.
12. **Callers/removals/preservation:** server routes are the only new caller;
    existing repository/cluster/serializer exports and all legacy serialized
    key sets remain unchanged; remove nothing.
13. **Tests/cases:** `W4-A01`–`A08`, `W4-S02`–`S04`, `W4-D02`, `W4-C04`; activation is the
    exact repository/parser/classifier/serializer/dispatch boundary in the case
    table. Controls `W4-NC01`–`NC04` and `NC11` must make their unchanged oracle
    fail.
14. **Output:** exact owner API functions/views consumed by T3 and W5.
15. **Non-goals/forbidden edits:** no createRun predicate/success/replay change
    beyond the exact rollback sentinel, no server route, query validator,
    worker/recovery/config/frontend/schema/package edit in this task.

- [x] `KI-W4-T1` Complete the four prescribed single-file transformations and
  their assigned local cases without changing a second file. Evidence:
  `EV-KI-W4-S05`, `EV-KI-W4-S06`, `EV-KI-W4-S07`, `EV-KI-W4-S10`.

#### Task block `KI-W4-T2` — Atomic Run and RunQuery construction

1. **Task:** add the exact transaction-composable Run/RunQuery constructors and
   immutable handoff integration in `DEC-KI-033`.
2. **Requirements/decisions:** `REQ-KI-010`, `011`, `015`–`017`, `019`;
   `INV-KI-010`, `011`, `015`; `DEC-KI-003`, `016`, `017`, `021`, `033`.
3. **Source:** accepted `runCreateData`, current query ID and repository
   transaction conventions, W1 `PrismaKeywordResearchRepository.createRun`,
   and accepted `mapSelectionToQueries`.
4. **Target:** only exported `newRunId`, `createKeywordResearchRun`, and
   `createKeywordResearchQueries`, their required private data builders, and
   the `queryPlanSource==="keyword_research"` branch inside
   `replaceEditableQueries` in `prisma-run-repository.js`; T4 separately owns
   the real-Prisma registrations.
5. **Interface/schema:** exact callback inputs, direct query-review Run state,
   normalized seed categories, snapshot object, RunQuery fields, and return
   arrays are literal in `DEC-KI-033`.
6. **Algorithm:** API validates/fingerprints snapshot → accepted keyword
   repository opens one transaction → run callback creates one Run → query
   callback maps and `createMany`s N rows → handoff row commits → route returns
   the created/found Run; no queue-planner action occurs.
7. **Operation order:** a new handoff performs exactly one each of research
   lookup, handoff lookup, Run create, RunQuery `createMany`, and handoff create;
   N is 1–100 but RunQuery insertion remains one repository bulk operation.
8. **Atomicity:** all five operations are `SAME_ATOMIC_BOUNDARY`; injected Run or
   query insertion failure rolls back Run, queries, handoff and lineage.
9. **Identities/formulas:** existing Run/RunQuery IDs; research/client request/
   selection fingerprint; primary-source-seed category index; one stable item
   ID to one query row. No stable-shop identity changes.
10. **Failure/replay/concurrency:** stale/non-owner/conflicted draft writes zero;
    identical handoff returns the original Run with zero writes; unequal
    fingerprint/revision under the key is 409; later selection edits cannot
    mutate the snapshot or RunQuery lineage; research edits atomically require
    the exact persisted query-ID set and preserve each non-null
    `keywordResearchItemId`, while the legacy replace branch is unchanged.
11. **Dependencies/bounds:** current Prisma client/schema only; N=1 and N=100
    are required; no per-query transaction and no N+1 read.
12. **Callers/removals/preservation:** only API service callbacks call the new
    methods; legacy `createRun`, planner, historical reads and null lineage are
    unchanged.
13. **Tests/cases:** `W4-D01`–`D06`, `W4-A05`, `W4-S05`; one real disposable
    schema, two rollback injection positions, owner/revision races, identical/
    conflicting replay, post-handoff edit, legacy negative control.
14. **Output:** immutable Run/snapshot/query plan consumed by T3 and downstream
    existing run routes.
15. **Non-goals/forbidden edits:** no schema/migration or further repository.js
    transaction change beyond T1's sentinel, no legacy replace behavior,
    planner rewrite, probe, dispatch, frontend, provider, AWS or package.

- [x] `KI-W4-T2` Complete the one prescribed production-file transformation;
  its six real-Prisma registrations remain allocated to T4. Evidence:
  `EV-KI-W4-S09`.

#### Task block `KI-W4-T3` — Research query editing, confirmation, probing, and routes

1. **Task:** add the exact research validators and server discriminators/routes
   while preserving every legacy path.
2. **Requirements/decisions:** `REQ-KI-001`, `002`, `010`–`013`, `015`, `019`;
   `INV-KI-003`, `010`, `011`, `013`, `015`; `DEC-KI-016`, `017`, `019`,
   `033`.
3. **Source:** `validateEditableQueryList`, `validateConfirmedQueryRows`,
   `validateResearchBackedQueries`, `requestedRunId`, `trustedUserId`,
   `awsProbeSearchPage`, existing start/edit/recovery/dispatch branches.
4. **Target:** only the two additive exports in `query-review.js` and the exact
   server imports, `keywordResearchApi`/`researchQueryValidationPipeline`
   injections, path parser, five routes, drain-to-execute context fields, and
   edit/start/local-confirm/AWS-confirm `queryPlanSource` branches named in the
   header.
5. **Interface/schema:** edit input stays strict
   `{revision,queries:[{id,categoryIndex,query}]}`; research validation recovers
   immutable item identity from persisted rows/snapshot; route bodies,
   responses, codes and CSV headers are `DEC-KI-019/033`.
6. **Algorithm:** route/auth/strict parse → T1 API method; research edit/start
   branch validates exact query/item sets and source relevance; explicit start
   queues scraping; drain passes discriminator/snapshot into `executeRun`;
   claimed research run revalidates with its immutable snapshot, probes each
   non-reusable valid row through the existing local/AWS seam, stores the
   evidence, returns weak/failure to review, otherwise invokes the unchanged
   downstream discovery/confirmed dispatcher.
7. **Operation order:** invalid edit/start makes zero probes/dispatches; valid
   confirmation commits before queue drain; worker uses existing marker→Google
   →result artifact sequence; at most one probe per row and dispatch only after
   all rows are valid.
8. **Atomicity:** existing query revision and confirmation transactions are
   unchanged; Google remains the existing recovered ambiguity boundary; this
   task adds no durable model or external operation.
9. **Identities/formulas:** query row ID and keyword item ID remain distinct;
   query revision fences edits/start; snapshot supplies source keyword/seeds;
   Run/stable shop/domain identities remain unchanged.
10. **Failure/replay/concurrency:** stale query revision 409; add/delete/swap
    lineage invalid; weak/failed probes persist and return editable; replay uses
    accepted probe fingerprint/freshness behavior; unknown discriminator fails
    closed; legacy behavior is exact.
11. **Dependencies/bounds:** 1–100 rows, query ≤200 code points, phrase ≤160,
    1–12 words, one supported prefix, ≤10 result occurrences each, ≤1,000
    total; no planner/repair call for research runs.
12. **Callers/removals/preservation:** existing `/api/runs/:id/queries` and
    `/start` gain a discriminator only; legacy validator/planner/probe/dispatch
    remain the default for `legacy`; no route is removed.
13. **Tests/cases:** `W4-Q01`–`Q08`, `W4-S01`–`S06`; product/non-product/all
    four lanes, 1/100 bounds, grammar/relevance/set partitions, weak/failure,
    1,000 occurrences, exact legacy regression. Controls `W4-NC07`–`NC10` make
    unchanged oracles fail.
14. **Output:** existing editable query UI/API receives a complete research
    plan and downstream flow receives confirmed probed rows.
15. **Non-goals/forbidden edits:** no query-validator/query-prober/pipeline/
    dispatcher/artifact/downstream/frontend/config/schema/package edit; no live
    Google/provider/AWS call.

- [x] `KI-W4-T3` Complete the two prescribed production-file transformations;
  their component registrations remain allocated to T4.
  Evidence: `EV-KI-W4-S08`, `EV-KI-W4-S12` (S007 accepted via `KI-W4-C001`).

#### Task block `KI-W4-T4` — Executable enforcement manifest and falsification

1. **Task:** create the exact manifest below and register every case once in its
   prescribed test file, including all critical falsification controls.
2. **Requirements/decisions:** every W4 requirement above; `DEC-KI-033`; parent
   standard E1/E6–E8 and Sections 8.4–8.5.
3. **Source:** literal matrix below; current Node test/subtest conventions;
   accepted isolated-schema helper and R4 executable-registry pattern.
4. **Target:** manifest plus the new non-DB component/enforcement test and the
   new DB handoff test in the delegable set; no production
   file is writable by this task.
5. **Interface/schema:** manifest root is exactly
   `{contractVersion:"ki-w4-enforcement-manifest-v1",groups}` and groups/IDs
   equal the literal block below; no metadata or inferred name registration.
6. **Algorithm:** `keyword-intelligence-api.test.js` enumerates and executes all
   28 non-DB IDs as one explicit registry; the handoff test enumerates and
   executes D01–D06 as its explicit registry. Each pushes an ID to `executed`
   only after its witness and oracle and asserts local exact equality. The
   non-DB conformance block combines its 28-ID certificate with the literal
   six-ID DB registry, while V6 combines the two executed certificates and
   independently asserts the 34-ID global union/digest. Each file emits exactly
   one TAP diagnostic beginning `KI_W4_EXECUTION_CERTIFICATE=` followed by
   compact JSON `{registry:"non_db"|"database",required:string[],
   registered:string[],executed:string[],skipped:string[],
   activationWitnesses:string[],oracleFailures:string[],digests:{required,
   registered,executed}}` with all arrays UTF-8 sorted and every digest using
   the normative member-plus-LF formula; the window
   assessment fails on a missing, duplicate or malformed certificate line.
7. **Operation order:** non-DB registries use only injected fakes/captured
   traces and run sequentially in manifest group/order
   `api_component→server_routes→query_review→conformance`; the DB registry
   calls the isolated harness once, registers D01–D06 in manifest order as
   sequential named subtests, and cleans that exact schema in `finally`.
8. **Atomicity:** test-only captured mutations are in-memory; real transaction
   claims come only from D01–D06; no source mutation control exists.
9. **Identities/formulas:** case grammar and sorted-member-plus-LF digest are
   the parent-standard formula; duplicate input fails before deduplication.
10. **Failure/replay/concurrency:** removal, skip/filter, duplicate/unexpected,
    absent activation, weakened forbidden-operation oracle, and divergent fake
    each make the unchanged acceptance assertion fail.
11. **Dependencies/bounds:** 34 IDs; counts 8/6/8/6/6; two executable registry
    files; one DB schema/run; no
    package, build, provider, AWS, production or second database run.
12. **Callers/removals/preservation:** test runner only; existing accepted tests
    may receive additive W4 blocks but no existing assertion/fixture is
    weakened, renamed, skipped or removed.
13. **Tests/cases:** all 34 literal cases; controls `W4-NC01`–`NC18`, with NC12
    individually exercises the seven enforcement-defect modes.
14. **Output:** exact WINDOW-ENFORCEMENT inputs for the window agent and parent.
15. **Non-goals/forbidden edits:** no production correction, future W5 test,
    live worktree/commit-dependent permanent oracle, or summary-only count.

- [x] `KI-W4-T4` Complete the three prescribed single-file manifest/test
  transformations and prove all controls falsify their unchanged oracles.
  Evidence: `EV-KI-W4-S13`, `EV-KI-W4-S14` (S009 accepted via `KI-W4-C002`),
  `EV-KI-W4-S15`.

##### Literal W4 enforcement manifest

```json
{
  "contractVersion": "ki-w4-enforcement-manifest-v1",
  "groups": {
    "api_component": [
      "W4-A01",
      "W4-A02",
      "W4-A03",
      "W4-A04",
      "W4-A05",
      "W4-A06",
      "W4-A07",
      "W4-A08"
    ],
    "server_routes": [
      "W4-S01",
      "W4-S02",
      "W4-S03",
      "W4-S04",
      "W4-S05",
      "W4-S06"
    ],
    "query_review": [
      "W4-Q01",
      "W4-Q02",
      "W4-Q03",
      "W4-Q04",
      "W4-Q05",
      "W4-Q06",
      "W4-Q07",
      "W4-Q08"
    ],
    "handoff_database": [
      "W4-D01",
      "W4-D02",
      "W4-D03",
      "W4-D04",
      "W4-D05",
      "W4-D06"
    ],
    "conformance": [
      "W4-C01",
      "W4-C02",
      "W4-C03",
      "W4-C04",
      "W4-C05",
      "W4-C06"
    ]
  }
}
```

Required count is 34, duplicate count zero, and normative digest is
`86810ce87a79426bb972be2e2827abc3806835190135d17769b52c33e7bb2203`.

##### Complete behavioral coverage matrix

Shared rules: all inputs are strict evidence-backed v1 objects; owner A owns the
fixture and owner B does not; external provider/AWS calls are forbidden; every
case uses its own case ID as `scenario_id` and records that ID only after the
stated witness and oracle. Component/unit/static cases discard only their
in-memory captures; D01–D06 share the one exact disposable schema and the DB
registry drops only that schema in `finally` and asserts exact-name absence.
`NC` references
the literal controls following the table. Within this matrix only, `/` repeats
the complete stable-ID prefix immediately to its left and an en-dash range is
inclusive; therefore `REQ-KI-001/002` resolves to `REQ-KI-001` plus
`REQ-KI-002`, and `W4-NC01/NC03` resolves to `W4-NC01` plus `W4-NC03`.
The reduction strategy is exhaustive for every listed boundary, owner/state/
version partition, failure position and N=1/N=100 limit; pairwise only across
independent filter parameters and independent valid selection-item kinds.
Omitted cross-products are equivalent because strict parsing occurs before the
same owner/service boundary and the filter predicate is a pure conjunction;
concurrency/rollback, legacy/research discrimination and external probe
outcomes are never reduced and have dedicated rows.

| Case | Requirements/decision | Production path, starting partition, input and actions | Activation witness and exact result | Operations, forbidden outcome and control | Parity / executable registration |
|---|---|---|---|---|---|
| `W4-A01` | `REQ-KI-001/002`; `DEC-KI-003/033` | `createResearch`; absent research; table partitions 0/1/5/6 seeds, 0/100/101 code points, NFKC/case duplicate, control and extra key; repeat one valid POST | strict parser and create commit run; only valid 1/5 persist and initialize after commit; repeated POST returns a distinct research ID | per valid call: 1 create+1 send; invalid: 0/0; automatic retry/send-before-commit forbidden; `W4-NC02` | component / `keyword-intelligence-api.test.js` API registry |
| `W4-A02` | `REQ-KI-002`; `INV-KI-003`; `DEC-KI-033` | `createResearch`; valid new row; dispatcher returns failed then throws | both return the same queued owner view and durable row is recoverable | 1 create, 1 attempted send, 0 provider; rollback/delete forbidden; `W4-NC02` | component / API registry |
| `W4-A03` | `REQ-KI-002/005/017`; `INV-KI-013/014`; `DEC-KI-033` | `getResearch`; missing, cross-owner, queued, each running stage, finalizing, completed, failed | owner predicate, stage projection and serializer run; exact progress/status/result visibility | one owner read; nonowner=missing 404; pre-complete result forbidden; `W4-NC01/NC03` | component / API registry |
| `W4-A04` | `REQ-KI-007`–`009`; `DEC-KI-014/015/033` | `saveSelection`; calculated/manual/edited, 0/200/201, extra/mutated lineage/metrics, conflict and stale revision | canonical classifier, conflict analyzer and CAS run; only exact canonical nonstale draft saves once | one read+one CAS; client authority/silent repair forbidden; `W4-NC04` | component / API registry |
| `W4-A05` | `REQ-KI-015/016`; `DEC-KI-017/033` | `createRun`; nonterminal, 0/1/100/101, conflict-free/conflicted, same/unequal retry | exact selection fingerprint/snapshot and transaction callbacks activate; exact outcome/code | invalid makes 0 callbacks; valid invokes both once; live-selection snapshot forbidden; `W4-NC05/NC06` | component / API registry |
| `W4-A06` | `REQ-KI-018`; `DEC-KI-019/033` | `exportCsv`; unknown/duplicate/boundary params then cumulative filters singly and conjunctively | strict query parser and every predicate execute; persisted order retained | one owner read, zero writes; ignored parameter/OR/re-sort forbidden; `W4-NC13` | component / API registry |
| `W4-A07` | `REQ-KI-018`; `INV-KI-009`; `DEC-KI-033` | `exportCsv`; each market plus null market and zero-match inputs | metric overlay and accepted CSV serializer execute; exact UTF-8 LF/header/data bytes | one read; raw/config/owner/lease/fingerprint/credential fields absent; `W4-NC11` | component / API registry |
| `W4-A08` | `REQ-KI-021`; `DEC-KI-033` | load/export/save/handoff with unsupported research/result/snapshot version | strict version parser activates and returns safe 409 `KEYWORD_RESEARCH_CONTRACT_MISMATCH` | zero mutation/send/probe; permissive upgrade forbidden; `W4-NC14` | component / API registry |
| `W4-S01` | `REQ-KI-001/019`; `DEC-KI-019/033` | all five routes; missing/duplicate user header, malformed encoded/shape ID, unknown body/query key | auth, path and strict body/query branches each execute with exact 401/400 | 0 API/service call for rejected requests; owner from body forbidden; `W4-NC15` | component / `keyword-intelligence-api.test.js` server section |
| `W4-S02` | `REQ-KI-001/002`; `DEC-KI-033` | POST base with valid owner/body and fake API event log | route returns 202, Location=statusUrl, create precedes dispatch | one service call; no queueDrain/provider; `W4-NC02` | component / server registry |
| `W4-S03` | `REQ-KI-002/005`; `DEC-KI-019` | GET ID for each owner/state plus notfound/internal safe error | exact API call and serializer response keys/status run | one service call; provider/internal fields forbidden; `W4-NC01/NC03` | component / server registry |
| `W4-S04` | `REQ-KI-007`–`009`; `DEC-KI-019` | PUT selection valid, malformed, stale, conflicting and nonowner | exact body parser/service/status mapping runs | one service call only for parsed requests; wrong 400/404/409 mapping forbidden; `W4-NC04` | component / server registry |
| `W4-S05` | `REQ-KI-015/016`; `DEC-KI-017/019` | POST runs new, identical retry, conflict, nonowner | 201 new/200 found and existing serialized Run/statusUrl activate | one API call; no planner/queueDrain; partial lineage forbidden; `W4-NC05/NC06` | component / server registry |
| `W4-S06` | `REQ-KI-018/019`; `DEC-KI-033` | export success/error then frozen legacy health/run/list/query requests | exact CSV headers/no-store and deep-equal legacy key/status fixtures | zero external call; additive legacy keys/behavior forbidden; `W4-NC10/NC11` | component / server registry |
| `W4-Q01` | `REQ-KI-010/011`; `DEC-KI-016` | mapper with category/store/local/brand and manual items | mapping executes and returns exactly one expected prefix/query per item | N input→N rows; products prefix on noncategory forbidden; `W4-NC16` | unit / `keyword-intelligence-api.test.js` query section |
| `W4-Q02` | `REQ-KI-010/013`; `DEC-KI-016/033` | research edit with mixed product/nonproduct/manual at 1 and 100; reorder/edit | research validator and ID recovery execute; exact set/order/text accepted | no add/delete and stable item lineage; `W4-NC07/NC08` | component / query registry |
| `W4-Q03` | `REQ-KI-010/013`; `DEC-KI-016` | quote/control/operator/colon/minus, 0/1/12/13 words, 160/161 phrase, 200/201 query, duplicate | each strict grammar partition activates exact issue code | zero probes; permissive grammar forbidden; `W4-NC17` | unit / query registry |
| `W4-Q04` | `REQ-KI-010/013`; `INV-KI-015`; `DEC-KI-016` | missing/extra/duplicate/swapped query or item IDs; relevant via keyword/seed and irrelevant text | exact two-set equality, category and relevance branches execute | invalid makes zero writes/probes; add/delete/identity substitution forbidden; `W4-NC08` | component / query registry |
| `W4-Q05` | `REQ-KI-012/013`; `INV-KI-010`; `DEC-KI-033` | confirmed valid 1 and 100 rows with ten-result mock pages | research confirmation validator and probe callback activate for every row | exactly N probes, ≤10N persisted occurrences, max 1,000, no planner; `W4-NC09` | component / query registry |
| `W4-Q06` | `REQ-KI-012/013`; `DEC-KI-033` | one weak and one thrown/failed probe | probe evidence serializer and return-to-review result activate | one probe/row; zero replacement/planner/dispatch; `W4-NC09` | component / query registry |
| `W4-Q07` | `REQ-KI-019`; `EXC-KI-005`; `DEC-KI-033` | frozen legacy editable/confirm fixtures | legacy validator/exact category count/product-only rules execute and deep-equal baseline | no research validator call; `W4-NC10` | component / query registry |
| `W4-Q08` | `REQ-KI-013`; `DEC-KI-016/033` | invalid research grammar/set/relevance and unknown discriminator | fail-closed branch activates before probe | zero probe/dispatch; fallback to legacy forbidden; `W4-NC07/NC08` | component / query registry |
| `W4-D01` | `REQ-KI-015/016`; `DEC-KI-017/033` | real Prisma new handoff with N=1 then N=100 in one schema | research/handoff lookups, Run create, bulk query insert and handoff create all activate | exactly five named repository operations per handoff; N queries; `W4-NC05/NC06` | integration / `keyword-intelligence-handoff.integration.test.js` DB registry |
| `W4-D02` | `REQ-KI-015`; `DEC-KI-017/033` | inject throw at Run create and RunQuery createMany; separately return invalid Run and invalid query callback outputs after their writes | rejection or mapped conflict and post-read activate only after rollback; no Run/query/handoff visible | 0 partial members at all four positions; normal-return-after-write forbidden; `W4-NC05` | integration / DB registry |
| `W4-D03` | `REQ-KI-015`; `INV-KI-013`; `DEC-KI-017` | owner B, stale revision and conflicted canonical draft | owner/revision/conflict predicates activate with exact outcome | 0 Run/query/handoff writes; `W4-NC01/NC04` | integration / DB registry |
| `W4-D04` | `REQ-KI-015`; `DEC-KI-017` | concurrent/equal client key+fingerprint then unequal revision/fingerprint | unique handoff/replay path executes; same Run found, conflict rejected | one Run total; no duplicate queries/handoff; `W4-NC18` | integration / DB registry |
| `W4-D05` | `REQ-KI-016/017`; `INV-KI-015`; `DEC-KI-017` | handoff, later selection CAS/edit, load run/history/queries | snapshot and item lineage reads execute and deep-equal pre-edit values | exactly N original query links; live research does not alter snapshot; `W4-NC06` | integration / DB registry |
| `W4-D06` | `REQ-KI-019`; `DEC-KI-021/033` | create/load/edit legacy Run and capture operation counts for 100-row research edit | null lineage/default discriminator and legacy repository paths execute | legacy key/behavior exact; one bulk handoff insert and bounded reads, no N+1; `W4-NC10` | integration / DB registry |
| `W4-C01` | `REQ-KI-001/002/005/007`–`013/015`–`019`; `DEC-KI-033` | parse literal manifest | exact root/groups/counts/unique IDs and digest recompute pass | 34 IDs; duplicate-before-dedup fails; `W4-NC12` | static / `keyword-intelligence-api.test.js` conformance registry |
| `W4-C02` | `REQ-KI-001/002/005/007`–`013/015`–`019`; `DEC-KI-033` | enumerate the literal 34 required IDs, both explicit registries, and the current 28 non-DB executed records | global required=registered exact; non-DB required=registered=executed and digest exact; V6 later merges DB execution | missing/duplicate/unexpected/filtered fails; `W4-NC12` | static/component registration certificate / conformance registry |
| `W4-C03` | `REQ-KI-001/002/005/007`–`013/015`–`019`; `DEC-KI-033` | inspect the 28 selected non-DB records; V3 separately emits the six DB records for V6 | local zero skip and every member has witness+oracle completion; V6 requires the same globally | skipped/unactivated/name-only execution fails; `W4-NC12` | component plus final window-agent certificate / conformance registry |
| `W4-C04` | `INV-KI-003/010/013`–`015`; `DEC-KI-033` | execute `W4-NC01`–`W4-NC18` against captured fakes/evidence | every unchanged positive oracle first passes, injected defect then throws, fresh positive passes | 18 expected/18 falsified; source mutation forbidden | component / conformance registry |
| `W4-C05` | `REQ-KI-002/012/013/015/019`; `DEC-KI-033` | compare fake repository/dispatcher/probe fields/order/failures with production contracts and D01–D06 | every substitute has exact supported claim and known difference | divergent fake cannot certify case; `W4-NC12` | component+integration / conformance registry |
| `W4-C06` | `REQ-KI-019`; `AUTH-KI-006`; `DEC-KI-033` | hash read-only accepted inputs; inspect final diff against 10-file set/symbols | legacy fixtures unchanged; actual changed set equals planned set; no W5/prohibited import | zero external/write during inspection; extra file/symbol fails; `W4-NC12` | static / conformance registry plus window-agent I001 |

Control definitions: `W4-NC01` removes the owner predicate from the fake/Proxy
read; `W4-NC02` places dispatch before the recorded commit; `W4-NC03` supplies a
running result to a serializer with result-exposure defect; `W4-NC04` removes the
revision predicate; `W4-NC05` replaces the post-write sentinel throw with a
normal conflict return, allowing a partial Run/query commit; `W4-NC06`
omits one snapshot/query item lineage field; `W4-NC07` invokes the legacy validator
for a valid non-product research row; `W4-NC08` permits one added/deleted row;
`W4-NC09` bypasses one required probe; `W4-NC10` invokes the research branch for the
frozen legacy fixture; `W4-NC11` adds one forbidden internal/raw field to the
captured response/export; `W4-NC12` independently injects missing registration,
skip/filter, duplicate, unexpected ID, absent activation, weakened forbidden-
operation assertion, and divergent substitute behavior; `W4-NC13` makes the
export parser ignore an unknown parameter and the filter use OR/re-sort;
`W4-NC14` accepts an unsupported persisted contract version; `W4-NC15` bypasses
auth/path strictness and trusts a body owner; `W4-NC16` maps every lane through
the products prefix; `W4-NC17` permits one forbidden query operator; and
`W4-NC18` removes the handoff replay uniqueness/fingerprint fence and attempts
to create a second Run. Each control first
passes its unchanged oracle, then the defect must throw `AssertionError`, then
a fresh unchanged witness passes.

##### Test-substitute fidelity and frozen gates

| Substitute | Reproduces | Cannot prove | Required higher-parity witness |
|---|---|---|---|
| API fake repository | exact method inputs/outcome unions, owner/status mapping and call order | SQL owner predicate, CAS, rollback, row persistence | `W4-D01`–`D06` real Prisma |
| Server fake API | strict route invocation, response status/headers/body and zero-call rejection | service canonicalization or DB semantics | `W4-A01`–`A08`, `W4-D01`–`D06` |
| Mock dispatcher | accepted `sendOne` input/result/throw and ordering event | AWS delivery/permissions | accepted R4 dispatcher contract; live remains W8 |
| Mock probe/artifact seam | one success/weak/failure result per query, saved occurrence and call counts | live Google quality/credentials/network | existing emitted probe contract; live remains separately gated |
| Injected clock/ID factories | exact deterministic timestamps/identities | wall-clock entropy | formula assertions and real Prisma persistence |

- [x] `KI-W4-V1` Window agent independently accepts every one-file leaf and
  proves the assembled changed-file set equals the ten literal paths and
  digest `fe48d14e…`; no leaf changed a second file. Evidence: `EV-KI-W4-S05`–
  `S15`, `EV-KI-W4-I01`.
- [x] `KI-W4-V2` On final frozen non-database inputs, run exactly once from
  `email_scraper/`:
  `node --test --test-isolation=none test/keyword-intelligence-api.test.js`.
  A01–A08, S01–S06, Q01–Q08 and C01–C06 pass; all 28
  non-DB W4 IDs have required=registered=executed equality, zero skips and
  activation witnesses; no localhost sandbox failure is silently accepted.
  Evidence: `EV-KI-W4-I01` (33/33); independently rerun by the parent
  (`EV-KI-A-040`).
- [x] `KI-W4-V3` Against one isolated non-production database, run exactly once:
  `ALLOW_DATABASE_TESTS=true node --test --test-isolation=none test/keyword-intelligence-handoff.integration.test.js`.
  One outer harness creates one schema, registers D01–D06 as six sequential
  named subtests, executes each once with zero skip, proves cleanup and exact
  schema-name absence, and makes no shared/public cleanup. Evidence:
  `EV-KI-W4-I01` (8/8); independently rerun by the parent (`EV-KI-A-040`).
- [x] `KI-W4-V4` On the same frozen source/tests, run `npm test` once and
  `npm run check:secrets` once. Existing legacy, keyword parity, selection,
  mapper, server, query-review and repository suites pass; guarded unrelated DB
  suites may skip only under their existing opt-in; secret scan is clean.
  Evidence: `EV-KI-W4-I01` (729/661/0 fail/68 guarded skips; secrets clean);
  independently rerun by the parent (`EV-KI-A-040`).
- [x] `KI-W4-V5` Prove scale/operation/privacy oracles: N=100 yields exactly 100
  RunQuery rows and at most 1,000 saved probe occurrences; handoff uses one bulk
  insert and no N+1 read; research path makes zero planner/repair calls; every
  owner response/export excludes the forbidden internal/raw/credential set.
  Evidence: `EV-KI-W4-I01`, `EV-KI-W4-S15` (oracles executed inside `W4-D01`/
  `D06`/`Q05`/`A07`/`C06` under V2/V3).
- [x] `KI-W4-V6` Independently recompute all 34 required, registered and executed
  IDs from the literal manifest and the two emitted
  `KI_W4_EXECUTION_CERTIFICATE` JSON objects and the normative digest
  `86810ce8…`; require exactly two certificate lines, exact equality, zero skip/
  duplicate/unexpected/filtered/unactivated/oracle failure, 18 expected and 18
  falsified controls, and zero unresolved substitute-fidelity or accepted-test
  invalidation. Evidence: `EV-KI-W4-I01`; merge digest independently reproduced
  by the parent (`EV-KI-A-040`).
- [x] `KI-W4-V7` Frozen-gate discipline: stateful V3 is not run during leaves or
  repeated after success unless a correction changes its source, harness,
  schema lifecycle or asserted path; V2/V4/V5/V6 rerun only when their inputs or
  asserted production path change. No Prisma/build/full-DB/live gate is run.
  Evidence: `EV-KI-W4-I01` (one run each); corrections C001/C002 preceded all
  gates (`EV-KI-W4-S12`, `EV-KI-W4-S14`).
- [x] `KI-W4-H1` Window agent appends `WINDOW-AGENT-INTEGRATION-PASS` to S3,
  sets S2 to `READY_FOR_PARENT_REVIEW`, and returns only the consolidated
  Section 12.5 handoff; it does not edit A4/A5/A6 or claim parent acceptance.
  Evidence: `EV-KI-W4-I01` (`WINDOW-INTEGRATION-COMPLETE`; A5 untouched at
  state 101 throughout execution).
- [x] `KI-W4-H2` Record every initial/corrective/assessment ID, starting/ending
  file digest, exact commands/results, required/registered/executed sets and
  digests, controls, schema lifecycle, skips/reuse, invalidated evidence,
  external mutations and `$0.00` provider/AWS cost. Evidence: `EV-KI-W4-S05`–
  `S15`, `EV-KI-W4-I01`.
- [x] `KI-W4-H3` Prove actual diff/symbol scope and no schema/migration/package/
  config/worker/recovery/dispatcher/probe/pipeline/frontend/infrastructure/W5/
  commit/push or direct parent-leaf action. Evidence: `EV-KI-W4-I01`; parent
  diff inspection in `EV-KI-A-040` (exactly ten paths, 6 `M`/4 `A`).
- [x] `KI-W4-H4` No corrective leaf remains unreviewed and every failed
  assessment is superseded by a later window-agent assessment. Evidence:
  `EV-KI-W4-S12` (C001 CLOSED), `EV-KI-W4-S14` (C002 CLOSED).
- [x] `KI-W4-H5` Parent independently verifies the current source/diff,
  enforcement certificate, decisive controls, DB transaction proof, legacy
  regression and active-state version before accepting. Evidence:
  `EV-KI-A-040`.
- [x] `KI-W4-H6` Stop. Only parent acceptance may append A6, CAS A5 and assign
  the separate KI-W5 window agent. Evidence: `EV-KI-A-040` (accepted; KI-W5
  remains unassigned pending requester direction).

### `KI-W5` — Complete Next.js dashboard

```yaml
window_id: KI-W5
objective: Deliver the complete standalone dashboard as owner-scoped Next.js UI backed by durable API state.
depends_on: [KI-W4]
consumes: W4 API; current dashboard inventory; existing Next/auth/proxy patterns
produces: keyword routes, strict frontend contracts/proxies, complete componentized dashboard, browser parity evidence
assigned_agent_policy: one_window
delegation_policy: one named KI-W5 window agent authors and manages sequential single-file leaves under PROJECT_AGNOSTIC_WINDOW_AGENT_SUBWINDOW_AUTHORING_STANDARD.md
window_agent_identity: KI-W5-WINDOW-AGENT
window_agent_coordination_write_scope: KEYWORD_INTELLIGENCE_KI_W5_SUBWINDOW_CHECKLIST.md; KEYWORD_INTELLIGENCE_KI_W5_SUBWINDOW_STATE.md; KEYWORD_INTELLIGENCE_KI_W5_SUBWINDOW_EVIDENCE.md
authorized_write_scope: KEYWORD_INTELLIGENCE_KI_W5_SUBWINDOW_CHECKLIST.md coordination only; KEYWORD_INTELLIGENCE_KI_W5_SUBWINDOW_STATE.md; KEYWORD_INTELLIGENCE_KI_W5_SUBWINDOW_EVIDENCE.md append-only
delegable_implementation_file_set: [frontend/app/keywords/page.tsx, frontend/app/keywords/[researchId]/page.tsx, frontend/app/api/keyword-research/route.ts, frontend/app/api/keyword-research/[researchId]/route.ts, frontend/app/api/keyword-research/[researchId]/selection/route.ts, frontend/app/api/keyword-research/[researchId]/runs/route.ts, frontend/app/api/keyword-research/[researchId]/export.csv/route.ts, frontend/components/keyword-intelligence/research-form.tsx, frontend/components/keyword-intelligence/research-dashboard.tsx, frontend/components/keyword-intelligence/research-status.tsx, frontend/components/keyword-intelligence/filter-bar.tsx, frontend/components/keyword-intelligence/summary-cards.tsx, frontend/components/keyword-intelligence/keyword-table.tsx, frontend/components/keyword-intelligence/selection-review.tsx, frontend/components/keyword-intelligence/chart-panels.tsx, frontend/components/keyword-intelligence/cluster-landscape.tsx, frontend/components/keyword-intelligence/keyword-dashboard.module.css, frontend/lib/keyword-intelligence-types.ts, frontend/lib/keyword-intelligence-validation.ts, frontend/lib/keyword-intelligence-view-model.ts, frontend/lib/api-types.ts additive keyword exports only, frontend/lib/api-validation.ts additive keyword parsers only, frontend/lib/client-api.ts additive keyword methods only, frontend/test/keyword-intelligence-api.test.ts, frontend/test/keyword-intelligence-components.test.ts, frontend/test/keyword-intelligence-inventory.test.ts, frontend/test/browser/keyword-intelligence-dashboard.mjs]
delegable_file_set_digest: a04dce13038a3d180ddab0c8412890af065e3f5ab5019540c87a5664485320e6
shared_file_scope: api-types/api-validation/client-api additive symbols only; existing modified run-presentation/stages/design-system-runtime are read-only
read_only_scope: KeywordSearchVolume/dashboard/index.html; frontend/AGENTS.md; installed Next docs; existing auth/proxy/run UI
authorized_actions: [author parent-bounded S1/S2/S3 decomposition, sequentially delegate exactly one listed implementation file per leaf, window-agent independent leaf review, leaf-level local_source_edits, local_frontend_check, local_next_server, local_Chrome_CDP, one final frozen npm run check from frontend/, one final frozen component/API/inventory test run, one final emitted production Next build with local server and Chrome CDP gates SCN-KI-016/017, one final 200-row scale and auth/privacy oracle run per KI-W5-V1-V4, one-file corrective leaves inside the same 27-file set, consolidated parent handoff]
prohibited_actions: [window-agent implementation-file edits, parallel leaves, direct parent-leaf communication, backend_edits, provider_calls, database_or_AWS_operations, iframe, runtime_CDN, unrelated_frontend_file_edits, package_or_lock_edits, commits, KI-W6_work]
successor: KI-W6
successor_reserved_for: parent
may_start_successor: false
```

- [ ] `KI-W5-P1` Assignment/hashes/version match. Evidence: ___
- [ ] `KI-W5-P2` W4 API contract accepted and local deterministic fixture server is available. Evidence: ___
- [ ] `KI-W5-P3` Exact Chart.js dependencies passed representative Next build and browser import. Evidence: ___
- [ ] `KI-W5-P4` Unrelated dirty frontend files and shared-symbol ownership recorded. Evidence: ___
- [ ] `KI-W5-P5` S1/S2/S3 exist; every mandatory `SW-*` readiness item is checked
  with S3 evidence; the exact 27-file decomposition covering `SCN-KI-016/017`
  and every `KI-W5-T1`–`T3` test obligation is
  `AWAITING_PARENT_DECOMPOSITION_REVIEW`; no leaf is assigned. Evidence: ___
- [ ] `KI-W5-P6` Parent approves the decomposition; only the window agent changes
  S2 to `READY` and assigns the first sequential one-file leaf. Evidence: ___

#### Task block `KI-W5-T1`

1. **Task:** add strict same-origin proxy routes, frontend types/parsers/client
   methods, and authenticated pages for all `DEC-KI-019` operations.
2. **Requirements/decisions:** `REQ-KI-001`, `002`, `005`–`009`, `018`,
   `DEC-KI-019`, `023`.
3. **Source:** existing frontend proxy/type/parser/client and auth page patterns
   `SRC-KI-015`, local Next documentation `SRC-KI-018`.
4. **Target:** exact page/api/lib symbols in window header.
5. **Interface/schema:** frontend strict mirror of `DEC-KI-019` and result/
   selection schemas; route params URL-encoded; auth forwarded only by existing
   server proxy; no client owner field.
6. **Algorithm:** server page authenticates → renders client shell; client
   creates/loads/saves/finalizes via same-origin API; queued/running polls with
   one active timer and capped 2s→10s interval; terminal stops; retry button only
   retries GET, never research.
7. **Operations:** browser→Next proxy→backend; export streams proxy response;
   no provider/browser calculation.
8. **Atomicity:** frontend performs expected-revision full save; backend remains
   authority; stale response reloads before user retries.
9. **Identities:** route research ID, revision, item IDs, clientRequestId generated
   once per handoff click and retained until response.
10. **Failure/replay:** tab close drops timers only; reload reads DB; duplicate
    click reuses client request; 401 routes sign-in; 404 generic; 409 shows stale
    conflict; terminal failure shows safe message.
11. **Dependencies/bounds:** Next16/React19; exact dependencies; request/result
    bounds from API; one poll timer; no localStorage except theme.
12. **Callers/obsolete:** new pages/components only; existing run pages receive
    returned URL; no static JSON/file loader or standalone dashboard script.
13. **Tests:** strict parser payload cases, proxy auth/error/no-store, polling
    lifecycle/tab remount/idempotent click; negative control bypasses parser and
    malformed backend response must fail.
14. **Output:** durable client boundary used by T2/T3.
15. **Non-goals:** visual port detail (T2), backend/API/provider edits.

- [ ] `KI-W5-T1` Perform the fully specified frontend boundary above.

#### Task block `KI-W5-T2`

1. **Task:** port every non-landscape dashboard surface and interaction in
   `REQ-KI-014` into focused components with exact filtering/sorting/export and
   durable cumulative selection.
2. **Requirements/decisions:** `REQ-KI-006`–`009`, `014`, `018`,
   `DEC-KI-013`–`015`, `023`.
3. **Source:** every reachable DOM/control/render function in
   `dashboard/index.html`, `SRC-KI-010`.
4. **Target:** component/view-model/test paths in header; one component per
   major surface, shared pure filter/sort selectors.
5. **Interface/schema:** components consume only parsed view model and emit
   typed selection/filter actions; filter state includes exact listed filters,
   market, page/pageSize, sort, selected history keyword; CSV columns/order
   mirror W2 export/filter result.
6. **Algorithm:** preserve standalone filter predicates/order/chart datasets;
   market changes project metrics only; edits/manual rows call W2-equivalent
   classifications returned by API state; selection save uses revision CAS;
   conflict review blocks handoff until 1–100 conflict-free.
7. **Operations:** render/filter pure client; saves/handoff through T1; export
   through backend route; no raw file/CDN calls.
8. **Atomicity:** UI applies saved selection only after backend success; stale
   mutation does not overwrite local display without explicit reload.
9. **Identities:** use itemId/clusterId, never keyword text or row index as React
   key/selection identity.
10. **Failure/replay:** empty/loading/error/over100/conflict/stale states are
    explicit; double-save disabled/reused; reload reconstructs exactly.
11. **Dependencies/bounds:** table pages bounded to standalone sizes; 200 draft;
    all chart data derived once per parsed revision/memoized; accessible controls.
12. **Callers/obsolete:** replaces static dashboard load/localStorage selection;
    preserves theme preference only; does not modify existing run editor.
13. **Tests:** component/runtime tests for every surface/control/filter/sort/
    selection/edit/pagination/theme/export; recommended≤100/>100/custom/conflict;
    market switch selection invariant. Negative control reintroduces per-market
    selection and invariant test fails.
14. **Output:** all complete-dashboard surfaces except 3D implementation consumed
    by T3/local E2E.
15. **Non-goals:** redesign, omitted charts, iframe, backend changes.

- [ ] `KI-W5-T2` Perform the fully specified dashboard port above.

#### Task block `KI-W5-T3`

1. **Task:** port custom 3D cluster landscape, local Chart.js/treemap charts,
   responsive styling, and real-browser interaction/visual assertions.
2. **Requirements/decisions:** `REQ-KI-014`, `DEC-KI-023`.
3. **Source:** standalone chart initialization and `drawClusterLandscape` plus
   CSS/DOM `SRC-KI-010`.
4. **Target:** owned components/styles/browser tests only.
5. **Interface/schema:** chart components accept parsed dataset/options; custom
   canvas accepts cluster points and exposes selected cluster callback; no
   global script variables.
6. **Algorithm:** preserve projection, depth order, radius/color, drag/pinch/
   wheel/zoom/reset/double-click, hit test, tooltip, inspector; destroy chart
   instances on dataset/unmount; use local imports.
7. **Operations:** browser canvas/DOM only; no network beyond app API.
8. **Atomicity:** N/A presentation; selection callback follows T2 save rules.
9. **Identities:** clusterId and itemId anchor interaction; device pointers keyed
   by pointerId.
10. **Failure/replay:** zero-size/empty dataset renders defined empty state;
    chart import/runtime error surfaces safe UI; remount creates one instance;
    no leaked listener/timer.
11. **Dependencies/bounds:** exact chart versions; desktop 1440×900 and mobile
    390×844; DPR-aware canvas; ≤200 final keyword points; no runtime CDN.
12. **Callers/obsolete:** dashboard T2 only; old loadScript/loadFirst removed from
    integrated path; existing unrelated visual system untouched.
13. **Tests:** CDP loads real Next page with nonempty fixture; assert every canvas
    exists/nonzero, controls change transform/selection, tooltips/inspector,
    mobile no horizontal page overflow, theme, no console/runtime errors. Pixel
    snapshots use stable fixture/browser and named tolerances. Negative control
    disables a required local dependency and build/runtime test fails.
14. **Output:** complete UI consumed by W6 end-to-end.
15. **Non-goals:** visual redesign, WebGL rewrite, chart-library substitution.

- [ ] `KI-W5-T3` Perform the fully specified visualization port above.

- [ ] `KI-W5-V1` Execute `SCN-KI-016` and `SCN-KI-017` in real Next/Chrome with nonempty fixture and all activation witnesses.
- [ ] `KI-W5-V2` Run `npm run check`, component/API tests, emitted production Next build/start, and browser console/network assertions.
- [ ] `KI-W5-V3` Render/filter 200 final keyword rows and 200 draft selections; assert one poll timer, bounded chart instances/listeners, and response/page-size ceilings.
- [ ] `KI-W5-V4` Assert auth isolation, no raw fields/CDNs/local result files, durable reload, accessible error/empty/loading states.
- [ ] `KI-W5-H1` Record files/symbols/dependencies. Evidence: ___
- [ ] `KI-W5-H2` Record commands/scenarios/outcomes/skips. Evidence: ___
- [ ] `KI-W5-H3` Diff matches scope and unrelated dirty files are byte-identical. Evidence: ___
- [ ] `KI-W5-H4` No successor/prohibited action. Evidence: ___
- [ ] `KI-W5-H5` Append evidence; A5 `AWAITING_REVIEW` by CAS. Evidence: ___
- [ ] `KI-W5-H6` Stop; do not begin `KI-W6`.

### Parent code review `KI-PR-W4-W5-01` — substantive implementation audit

```yaml
review_id: KI-PR-W4-W5-01
scope: [accepted KI-W4 production code and tests, accepted KI-W5 production code and tests]
purpose: Find real correctness, edge-case, conversion, integration, durability, privacy, performance, or test-coverage gaps before KI-W6 begins.
excluded: [documentation cleanup, evidence formatting, authoring-standard compliance without code impact, KI-W6 decomposition review, implementation changes]
authority_effect: none
status: COMPLETE_CORRECTION_REQUIRED
```

This is a parent-owned, read-only review record. It does not reopen acceptance,
assign work, authorize corrections, or change A5. Findings must identify an
observable code risk and cite exact source/test locations. Confirmed defects,
credible risks, and documentation-only observations remain distinct.

#### Review progress

- [x] Reconstruct the accepted KI-W4 implementation and behavioral contract.
- [x] Review KI-W4 production paths and meaningful adversarial coverage.
- [x] Reconstruct the accepted KI-W5 implementation and behavioral contract.
- [x] Review KI-W5 production paths and meaningful adversarial coverage.
- [x] Check the W4-to-W5 boundary and record the final disposition.

#### Findings

The following are confirmed implementation defects. They are ordered by
severity, not by window or file order.

1. **`KI-PR-F01` — critical — every real research response fails the W5
   parser.** W4 stores and serializes `contractVersion: 1`, and its result
   schema also requires literal number `1`
   (`email_scraper/src/api-serializer.js:1063-1069`,
   `email_scraper/src/keyword-intelligence/schemas.js:139-148`). W5 instead
   declares both versions as strings and calls `nonEmptyText`
   (`frontend/lib/keyword-intelligence-types.ts:175-176,210-215`,
   `frontend/lib/keyword-intelligence-validation.ts:516-523,728-734`). Its
   fixtures invented `"ki-research-v1"` rather than consuming a W4 response
   (`frontend/test/keyword-intelligence-api.test.ts:184-190,242-249`). Direct
   parser reproduction with a numeric W4 version returns `ApiPayloadError` at
   `research.contractVersion`. The real dashboard cannot create, load, poll,
   save, or finalize research successfully.
2. **`KI-PR-F02` — critical — all three W5 mutation calls are rejected with
   HTTP 415 by their own Next routes.** `apiRequest` sets only `Accept`; the
   create, save, and handoff calls pass JSON strings without a `Content-Type`
   header (`frontend/lib/client-api.ts:20-32,56-60,72-80,84-95`). Fetch assigns
   `text/plain;charset=UTF-8` to those requests, while each route requires
   `application/json` (for example
   `frontend/app/api/keyword-research/route.ts:10-16` and
   `frontend/app/api/keyword-research/[researchId]/selection/route.ts:10-19`).
   The browser harness replaced `globalThis.fetch` and returned fixtures before
   any Next route ran (`frontend/test/browser/keyword-intelligence-dashboard.mjs:647-697`),
   so its passing scenarios did not exercise this boundary.
3. **`KI-PR-F03` — high — W5 manual selections can never pass W4 canonical
   validation.** W5 creates `ksi_` IDs with a private salted FNV-like digest
   (`frontend/components/keyword-intelligence/selection-review.tsx:57-79`). W4
   recomputes the accepted six-byte BLAKE2s identity and rejects a mismatch
   (`email_scraper/src/keyword-intelligence/selection.js:12-20`,
   `email_scraper/src/keyword-intelligence/dedup.js:48-51`,
   `email_scraper/src/keyword-intelligence/api.js:236-247`). For normalized
   `womens dresses`, the implementations produce `ksi_866062defc09` and
   `ksi_efce01afca99` respectively. Every manual item therefore makes save
   return `KEYWORD_RESEARCH_INPUT_INVALID`.
4. **`KI-PR-F04` — critical — the selection payload ceilings cannot carry the
   supported selection cardinality.** The backend selection route uses the
   global 32 KiB reader (`email_scraper/src/server.js:1782-1789`,
   `email_scraper/src/request-json.js:3-5`); the Next route independently caps
   the body at 262,144 bytes
   (`frontend/app/api/keyword-research/[researchId]/selection/route.ts:8-24`).
   The accepted parity result's real 12-item default selection serializes to
   176,232 bytes, so even that accepted fixture cannot be saved through W4.
   A representative canonical calculated item with 15 months across all nine
   market snapshots measured 10,695 bytes; complete envelopes measured 32,021
   bytes for three items, 42,684 for four, 266,652 for 25, and 1,066,602 for
   100. The API advertises drafts up to 200 and handoff up to 100, but the
   backend rejects four representative items and the frontend rejects 25 before
   the canonical save logic runs.
5. **`KI-PR-F05` — high — Finalize can silently hand off an older persisted
   selection instead of the displayed draft.** Draft edits are local until
   `handleSave` (`frontend/components/keyword-intelligence/research-dashboard.tsx:205-238`).
   `handleFinalize` validates the local draft but sends only the current server
   revision and never saves or proves equality with `view.selection`
   (`frontend/components/keyword-intelligence/research-dashboard.tsx:240-255`);
   `canFinalizeSelection` has no dirty-draft condition
   (`frontend/lib/keyword-intelligence-view-model.ts:646-654`). A user can edit
   and immediately finalize, after which W4 correctly snapshots the old stored
   items (`email_scraper/src/keyword-intelligence/api.js:478-505`).
6. **`KI-PR-F06` — high — ambiguous handoff retries discard the idempotency
   key.** W5 clears `clientRequestIdRef` for every caught error, including a
   timeout, 502, or unreadable response after W4 may already have committed
   (`frontend/components/keyword-intelligence/research-dashboard.tsx:240-263`).
   The next click uses a new key and can create another run. W4 also does not
   reconcile a same-key unique race after its initial read
   (`email_scraper/src/keyword-intelligence/repository.js:1232-1275`); its DB
   test explicitly permits one concurrent equal-key call to reject by requiring
   only one fulfilled promise
   (`email_scraper/test/keyword-intelligence-handoff.integration.test.js:439-447`).
   Together, the browser and server do not provide reliable idempotent recovery
   at the network boundary.
7. **`KI-PR-F07` — medium — the visible table and downloaded CSV use different
   predicates.** W5 treats multiple flags as OR and searches `seed`,
   `mainIntent`, and the synthetic word `recommended`
   (`frontend/lib/keyword-intelligence-view-model.ts:185-216`). W4 export treats
   multiple flags as AND and its search corpus omits those extra fields
   (`email_scraper/src/keyword-intelligence/api.js:350-390`). The browser export
   scenario generated its expected CSV with the same frontend `getFiltered`
   helper instead of calling the W4 exporter
   (`frontend/test/browser/keyword-intelligence-dashboard.mjs:1093-1109`), so it
   could not detect the divergence.
8. **`KI-PR-F08` — medium — W4 persists an exact duplicate item that it later
   refuses to hand off.** `validateSelectionDraft` detects repeated IDs
   (`email_scraper/src/keyword-intelligence/selection.js:133-156`), but the W4
   save API never invokes it; conflict analysis silently deduplicates IDs
   (`email_scraper/src/keyword-intelligence/api.js:445-465`,
   `email_scraper/src/keyword-intelligence/selection.js:190-200`). The duplicate
   array is consequently saved with a new revision and no conflict, while
   `mapSelectionToQueries` rejects that same persisted array at handoff
   (`email_scraper/src/keyword-intelligence/query-mapper.js:32-46`). Direct
   reproduction returned zero conflicts at save analysis and
   `duplicate_item_id` at mapping.
9. **`KI-PR-F09` — medium security — keyword CSV export permits spreadsheet
   formula injection.** The keyword exporter only quotes comma/quote/newline
   characters and does not neutralize leading `=`, `+`, `-`, `@`, tab, or
   carriage return (`email_scraper/src/keyword-intelligence/export.js:3-10,188-208`).
   Direct export preserved an `=HYPERLINK(...)` keyword and `+cmd` seed as
   executable-looking spreadsheet cells. The repository's general CSV writer
   already neutralizes this class of value, but the W4 download path does not.

#### Verification and disposition

- Focused read-only reproductions confirmed: native Fetch assigns
  `text/plain;charset=UTF-8`; the W5 parser rejects W4 numeric version `1`; the
  two manual-ID algorithms disagree; representative selection envelope sizes
  cross both ceilings; duplicate save analysis returns no conflict while query
  mapping rejects the duplicate; and CSV formula prefixes remain intact.
- No production file, test, state file, evidence file, database, provider, AWS
  resource, or KI-W6 artifact was changed or invoked by this review.
- **Disposition:** KI-W4 and KI-W5 are not integration-safe as accepted. The
  four blocking boundary failures make KI-W6 incapable of proving the intended
  workflow. A corrective parent window is required before KI-W6, but this
  review record neither authors nor assigns it.

### `KI-R5` — W4/W5 functional boundary correction

```yaml
window_id: KI-R5
objective: Make the accepted W4 backend and W5 dashboard interoperable, capacity-correct, saved-selection faithful, retry-safe, filter-consistent, and CSV-safe before integrated acceptance.
depends_on: [KI-W5 accepted, KI-PR-W4-W5-01 complete]
consumes: DEC-KI-002/014/015/017/019/033; DEC-KI-034 through DEC-KI-037; SRC-KI-034 through SRC-KI-037; accepted W4/W5 source and tests
produces: corrected strict wire/mutation contract, canonical 200-item selection save, saved-only finalization, durable equal-key handoff recovery, filter/export parity, duplicate rejection, formula-safe CSV, 34-case enforcement certificate
assigned_agent_policy: one_window
delegation_policy: one named KI-R5 window agent authors and manages strictly sequential single-file leaves under PROJECT_AGNOSTIC_WINDOW_AGENT_SUBWINDOW_AUTHORING_STANDARD.md
window_agent_identity: KI-R5-WINDOW-AGENT
window_agent_coordination_write_scope: KEYWORD_INTELLIGENCE_KI_R5_SUBWINDOW_CHECKLIST.md; KEYWORD_INTELLIGENCE_KI_R5_SUBWINDOW_STATE.md; KEYWORD_INTELLIGENCE_KI_R5_SUBWINDOW_EVIDENCE.md
authorized_write_scope: KEYWORD_INTELLIGENCE_KI_R5_SUBWINDOW_CHECKLIST.md coordination only; KEYWORD_INTELLIGENCE_KI_R5_SUBWINDOW_STATE.md; KEYWORD_INTELLIGENCE_KI_R5_SUBWINDOW_EVIDENCE.md append-only
delegable_implementation_file_set: [email_scraper/src/keyword-intelligence/api.js, email_scraper/src/keyword-intelligence/repository.js, email_scraper/src/keyword-intelligence/export.js, email_scraper/src/server.js, email_scraper/test/keyword-intelligence-api.test.js, email_scraper/test/keyword-intelligence-handoff.integration.test.js, email_scraper/test/fixtures/keyword-intelligence/ki-r5-enforcement-manifest-v1.json, email_scraper/test/keyword-intelligence-r5-enforcement.test.js, frontend/lib/keyword-intelligence-types.ts, frontend/lib/keyword-intelligence-validation.ts, frontend/lib/client-api.ts, frontend/lib/keyword-intelligence-view-model.ts, frontend/components/keyword-intelligence/research-dashboard.tsx, frontend/components/keyword-intelligence/selection-review.tsx, frontend/test/keyword-intelligence-api.test.ts, frontend/test/keyword-intelligence-components.test.ts, frontend/test/keyword-intelligence-inventory.test.ts, frontend/test/browser/keyword-intelligence-dashboard.mjs]
delegable_file_set_digest: efc82a884d09561ed27be3513ca6898f0ab311dbe56cf46e9c2c241492560077
shared_file_scope: api.js saveSelection input/materialization/validation only; repository.js createRun unique-race catch/reconciliation only; export.js textual-cell safety only; server.js selection read limit only; client-api.ts three keyword mutation methods only; view-model.ts selection projection/saved gate and exact filter predicate only; research-dashboard/selection-review handoff state and control locking only; accepted tests may change only to supersede affected W4/W5 assertions and add R5 registries
read_only_scope: A1-A8 outside parent updates; email_scraper/prisma/**; email_scraper/src/request-json.js; email_scraper/src/keyword-intelligence/selection.js, schemas.js, query-mapper.js, pipeline.js, dedup.js, cluster.js; all worker/provider/S3/SQS/build/infrastructure code; frontend app route handlers; frontend auth/proxy code; installed Next route-handler docs; package/lock files; KI-W6 subordinate artifacts
authorized_actions: [author parent-bounded S1/S2/S3 decomposition, sequentially delegate exactly one listed implementation file per leaf, window-agent independent leaf review, leaf-level local source/test edits, file-local static or focused non-database diagnostics during editing, one final focused backend non-database gate, one final focused frontend test gate, one final focused isolated-database gate in one disposable schema, one final frontend npm run check, one emitted Next browser gate reusing that build, one final backend npm test, one final secret scan, one final 34-case enforcement merge, one-file corrective leaves inside the same 18-file set, consolidated parent handoff]
prohibited_actions: [window-agent implementation-file edits, parallel leaves, direct parent-leaf communication, package_or_lock_edits, schema_or_migration_edits, worker_provider_S3_SQS_build_or_infrastructure_edits, full_opted_in_database_suite, repeated_successful_stateful_or_build_gate_without_invalidation, auth_bypass, provider_calls, AWS_operations, production_database_writes, destructive_shared_cleanup, commits_or_pushes, KI-W6_leaf_or_integration_work, KI-W7_work]
successor: KI-W6
successor_reserved_for: parent
may_start_successor: false
```

The 18-path digest is SHA-256 over the unsigned-UTF-8-byte-sorted paths, each
followed by one LF. The window agent writes only S1/S2/S3; implementation is
performed only by sequential one-file leaves. It may add one-file corrective
leaves after a diagnosed failure but cannot broaden the 18-path set or decide a
parent-level behavior. The requester remains the only committer.

- [ ] `KI-R5-P1` A5 has a unique KI-R5 assignment, pins current standard/A1/A3/A4 hashes, authorizes only KI-R5 coordination until decomposition approval, records `accepted_through:KI-W5`, `next_window:KI-W6`, `stop_after:KI-R5`, and `may_start_successor:false`. Evidence: ___
- [ ] `KI-R5-P2` Backend is clean at `fac5bb0f0a4e9c04873c9d338794762d44e35f7f`; frontend is clean at `c85f93b4bc66e1c130401227e46b488c6fe13c94`; the exact starting hashes/ABSENT states for all 18 paths and protected root relocation state are recorded. Evidence: ___
- [ ] `KI-R5-P3` Reproduce `KI-PR-F01`–`F09`, verify `PAY-KI-008`, verify no KI-W6 leaf was assigned/executed, and verify the prior W6 decomposition is revision-invalidated rather than edited. Evidence: ___
- [ ] `KI-R5-P4` S1/S2/S3 exist; every mandatory `SW-*` readiness item is checked with S3 evidence; the exact 18-file one-file-leaf decomposition covers every T1–T5 field and all 34 cases; the window agent stops at `AWAITING_PARENT_DECOMPOSITION_REVIEW`. Evidence: ___
- [ ] `KI-R5-P5` Parent independently approves the decomposition; only the window agent changes S2 to `READY` and assigns the first sequential leaf. Evidence: ___

#### Task block `KI-R5-T1` — canonical bounded selection mutation

1. **Task:** replace the full-snapshot selection PUT input with `PAY-KI-008`,
   materialize canonical items in W4, reject duplicates before CAS, and raise
   only the backend selection reader to 262144 bytes.
2. **Requirements/decisions:** `REQ-KI-005`–`009`, `016`; `INV-KI-010`,
   `013`; `DEC-KI-002`, `014`, `015`, `034`, `036`.
3. **Source:** `api.js` strict schemas, `canonicalizeSelectionItem`,
   `saveSelection`; accepted `validateSelectionDraft`; `server.js` selection
   route; result row IDs/metrics in persisted owner view.
4. **Target:** only `api.js` selection input schema/materializer/save method,
   the selection-route `readJsonBody` argument in `server.js`, and additive R5
   API/server tests.
5. **Interface/schema:** exact strict union and request/envelope/limit in
   `DEC-KI-034/PAY-KI-008`; durable/full response `SelectionItem` unchanged.
6. **Ordered algorithm:** strict parse → owner view → v1 contract/fingerprint
   check → completed-state check → ordered union materialization from persisted
   result/first seed → `validateSelectionDraft` → conflict analysis → existing
   expected-revision repository CAS → serialize canonical owner response.
7. **Operations:** one existing owner read, in-memory lookup/materialization and
   at most 19,900 pair comparisons, then one existing save transaction; zero
   provider/S3/SQS/Google/worker call.
8. **Atomicity:** save remains `SAME_ATOMIC_BOUNDARY`; all parsing,
   materialization, duplicate and conflict rejection precede the write.
9. **Identities/formulas:** calculated source ID must match
   `^ksi_[a-f0-9]{12}$` and an exact result row; canonical calculated/manual ID
   is `DEC-KI-002`; normalized keyword and first seed are `DEC-KI-003/014`.
10. **Failure/replay:** unknown/old full keys, missing source, duplicate derived
    ID, malformed text, 201 items and noncanonical source reject 400/zero write;
    >262144 bytes rejects 413 before API; stale revision remains 409; exact
    retry after success is stale, not a second increment.
11. **Dependencies/bounds:** no new dependency/config; 0–200 items; 160 code
    points; 262144 bytes; 200 maximum four-byte keywords measure 143641 bytes.
12. **Callers/obsolete:** W5 PUT mapper changes in T4; remove acceptance of the
    old full request shape only; preserve response, repository, worker/default
    selection, handoff snapshot and legacy query behavior.
13. **Tests:** register `R5-SEL-01`–`08` exactly once; activation witnesses are
    the union branch, persisted-row lookup, manual ID derivation,
    `validateSelectionDraft`, body reader, and CAS; controls `R5-NC-03/04` make
    the unchanged rejection/write-count oracle fail.
14. **Output:** canonical saved response consumed by T4 saved-draft gate and T2
    run handoff.
15. **Non-goals:** no schema/result/durable item change, client identity trust,
    auto-dedup, conflict threshold change, package edit or W6 test.

- [ ] `KI-R5-T1` Perform the fully specified change in task block `KI-R5-T1`.

#### Task block `KI-R5-T2` — equal-key handoff race and retry truth

1. **Task:** make concurrent equal handoff calls both return the same durable
   Run and lock frontend retry semantics to the same attempt identity.
2. **Requirements/decisions:** `REQ-KI-015`, `016`; `INV-KI-010`, `015`;
   `DEC-KI-017`, `035`.
3. **Source:** `repository.js::createRun`, handoff unique
   `(researchId,clientRequestId)`, existing W4-D04, W5 handoff state.
4. **Target:** only the `createRun` unique-error catch/reconciliation and
   additive focused repository tests; frontend lifecycle is completed in T4.
5. **Interface/schema:** repository return union remains
   `created|found|conflict|not_found`; no public signature/schema change.
6. **Ordered algorithm:** attempt existing transaction; on recognized unique
   error start fresh read-only transaction → read exact handoff → if absent
   rethrow original → compare revision/fingerprint → read Run → equal+present
   `found`, otherwise conflict.
7. **Operations:** winning call performs one existing write transaction; loser
   rolls back then performs one handoff read and at most one Run read; no second
   write or external call.
8. **Atomicity:** original transaction is unchanged; reconciliation observes
   only committed durable evidence after rollback.
9. **Identities/formulas:** exact existing handoff key/fingerprint/revision and
   deterministic row identity; never compare caller-proposed Run ID for replay.
10. **Failure/replay:** equal concurrent calls fulfill `created+found`; unequal
    key payload conflicts; handoff-without-Run conflicts; unrelated unique or
    database error rethrows; later equal retry found.
11. **Dependencies/bounds:** existing Prisma client/isolated helper; two calls,
    one Run, 1–100 queries; no retry loop or sleep.
12. **Callers/obsolete:** API createRun and legacy runs unchanged; replace the
    W4-D04 `fulfilled>=1` oracle with exact two-fulfilled/one-Run proof.
13. **Tests:** `R5-FIN-07/08` in one isolated schema with exact row/call counts;
    `R5-NC-07` disables reconciliation through a test collaborator/proxy and
    makes the two-fulfilled oracle fail, then production passes.
14. **Output:** durable replay behavior consumed by T4 ambiguous retry.
15. **Non-goals:** no handoff schema/index/migration, distributed lock,
    client-side persistence or change to unequal replay semantics.

- [ ] `KI-R5-T2` Perform the fully specified change in task block `KI-R5-T2`.

#### Task block `KI-R5-T3` — filter/export parity and formula-safe CSV

1. **Task:** preserve W4 filter authority, make textual CSV cells spreadsheet
   safe, and supply independent literal filter/export oracles.
2. **Requirements/decisions:** `REQ-KI-014`, `018`; `INV-KI-009`;
   `DEC-KI-033`, `036`.
3. **Source:** W4 `matchesFilters`, `serializeKeywordsCsv`, general CSV writer
   neutralization precedent, W5 `getFiltered/buildExportQuery`.
4. **Target:** only `export.js` textual-cell preparation and additive backend
   tests; W5 predicate/test changes occur in T4.
5. **Interface/schema:** CSV columns/order/LF/headers/numeric formatting remain
   exact; textual neutralization is exactly `DEC-KI-036`.
6. **Ordered algorithm:** project/filter in persisted order → convert row →
   neutralize named textual cells once → existing CSV quote/escape → join LF.
7. **Operations:** one existing owner read and O(result rows) pure projection;
   no write/external call.
8. **Atomicity:** N/A pure on-demand response; no durable operation.
9. **Identities/formulas:** filter uses persisted item order/IDs; neutralization
   regex and named columns are literal in `DEC-KI-036`.
10. **Failure/replay:** repeated export byte-identical; empty filter header+LF;
    malformed filters remain 400; apostrophe-prefixed text is not double
    prefixed; negative numeric trend remains numeric.
11. **Dependencies/bounds:** result ≤200 shortlist rows; flag query ≤20; no new
    library, buffer, file or localStorage output.
12. **Callers/obsolete:** only W4 export route and W5 download; preserve Python
    parity except the explicitly superseded unsafe textual-cell behavior.
13. **Tests:** `R5-EXP-01`–`06`; independent literal item-ID/CSV expectations;
    `R5-NC-08/09/10` falsify AND/search/safety oracles without source mutation.
14. **Output:** authoritative CSV/filter semantics mirrored by T4.
15. **Non-goals:** no result re-sort, new filter, column change, CSV library or
    JSON export implementation.

- [ ] `KI-R5-T3` Perform the fully specified change in task block `KI-R5-T3`.

#### Task block `KI-R5-T4` — strict frontend wire, saved gate and retry UI

1. **Task:** correct numeric version parsing, explicit JSON requests, minimal
   selection projection, exact filter mirror, saved-only finalization and
   retry-required UI behavior.
2. **Requirements/decisions:** `REQ-KI-005`–`009`, `014`–`018`;
   `INV-KI-009`, `010`, `013`, `015`; `DEC-KI-034`–`036`.
3. **Source:** accepted W5 types/parser/client/view-model/dashboard/review,
   actual W4 serializer/result fixture, installed Next route-handler guide.
4. **Target:** exact frontend lib/component/test/browser paths in the header;
   no route/auth/proxy/style/package file.
5. **Interface/schema:** numeric literal `1`; `SelectionMutationItem` projection;
   `canFinalizeSelection` adds exact `unsaved`; handoff state adds exact
   `retry_required`; component prop/type changes are confined to the named
   dashboard/review pair.
6. **Ordered algorithm:** parse numeric response → keep full draft → project
   minimal PUT → canonical save response replaces view/draft → compare ordered
   projections → allocate handoff ID/revision → classify response definitive or
   ambiguous → retain/clear state exactly per `DEC-KI-035`.
7. **Operations:** one HTTP per user action; ambiguous retry one additional
   same-key POST; no auto-save, duplicate timer, provider or direct backend call.
8. **Atomicity:** browser has no durable authority; revision and backend
   transactions remain authoritative; ambiguous UI lock prevents mutation of
   the attempted revision.
9. **Identities/formulas:** client unsaved key is presentation-only; wire item
   identity is server-derived; request ID/revision pair remains byte-identical
   across ambiguous retries.
10. **Failure/replay:** 4xx definitive and existing UI mapping; network,
    unreadable or ≥500 retry-required; controls inert while retry-required;
    retry uses same ID; unsaved gate sends zero POST; reload performs GET only.
11. **Dependencies/bounds:** existing Next16/React19; 0–200 draft/1–100 final;
    one active handoff; no package/localStorage addition.
12. **Callers/obsolete:** update numeric fixtures and affected accepted W5
    assertions; remove browser manual ID authority and self-derived export
    oracle; preserve all unrelated dashboard surfaces, auth and legacy callers.
13. **Tests:** `R5-WIRE-01`–`06`, `R5-FIN-01`–`06`, and cross-side
    `R5-EXP-01`–`04`; actual serializer→parser witness; fetch-init witness;
    emitted Next pass-through 401-not-415 witness; controls
    `R5-NC-01/02/05/06/08/09/11`.
14. **Output:** functional corrected dashboard consumed by KI-W6.
15. **Non-goals:** no auth fixture/bypass, page redesign, chart change,
    persistence outside Neon, auto-save, service worker or W6 implementation.

- [ ] `KI-R5-T4` Perform the fully specified change in task block `KI-R5-T4`.

#### Task block `KI-R5-T5` — enforcement manifest and superseding proof

1. **Task:** implement the literal 34-case manifest/registries, enforcement
   lint, substitute boundaries, accepted-test supersession and frozen gates.
2. **Requirements/decisions:** all T1–T4 requirements; `DEC-KI-037`.
3. **Source:** accepted W4/W5 manifests/certificates, R5 matrix below,
   authoring-standard E6–E8/10.3/11.1.
4. **Target:** new R5 manifest/enforcement test plus additive registries in the
   exact six listed existing test/harness files.
5. **Interface/schema:** manifest root exactly
   `{contractVersion:"ki-r5-enforcement-manifest-v1",groups}` and only literal
   arrays below; certificate fields exactly standard Section 10.3.
6. **Ordered algorithm:** parse manifest → reject duplicate before set creation
   → compare literal groups/digests → enumerate registries → execute selected
   cases → record only after activation+oracle → merge exact sets → run controls
   → emit certificate.
7. **Operations:** 34 cases; one focused DB invocation; one frontend build and
   browser run; zero live/external mutation.
8. **Atomicity:** only DB cases use isolated transactions; certificate emitted
   after all case sets and controls succeed.
9. **Identities/formulas:** case-ID grammar and sorted-member-plus-LF digests
   below; no locale sorting or test-name inference.
10. **Failure/replay:** any missing/duplicate/skip/filter/unexpected/unactivated/
    weakened/divergent member fails; affected accepted evidence is explicitly
    superseded, unrelated accepted IDs must remain.
11. **Dependencies/bounds:** existing runners only; frozen gates exactly
    `DEC-KI-037`; no repeated successful DB/build gate.
12. **Callers/obsolete:** replace affected W4/W5 fixture assumptions and weak
    D04/browser intercept claims; do not rewrite unrelated accepted cases.
13. **Tests:** `R5-CONF-01`–`06`; `R5-NC-12` mutates only in-memory discovered
    sets/substitute evidence and proves execution/document lint fails.
14. **Output:** `WINDOW-ENFORCEMENT` certificate consumed by parent review.
15. **Non-goals:** no production mutation control, evidence deletion, W6 case,
    broad database suite or summary-only certificate.

- [ ] `KI-R5-T5` Perform the fully specified change in task block `KI-R5-T5`.

#### Literal enforcement manifest

| Group | Required IDs | Count | Per-member-LF SHA-256 |
|---|---|---:|---|
| `wire` | `R5-WIRE-01`, `R5-WIRE-02`, `R5-WIRE-03`, `R5-WIRE-04`, `R5-WIRE-05`, `R5-WIRE-06` | 6 | `64e53c38d37b28ebb8da1799fc5e1f2d75c3aa45b5ca78a79529fe1d0ec2c1c7` |
| `selection` | `R5-SEL-01`, `R5-SEL-02`, `R5-SEL-03`, `R5-SEL-04`, `R5-SEL-05`, `R5-SEL-06`, `R5-SEL-07`, `R5-SEL-08` | 8 | `a7fe88a15c03119d46e51bb3ccf9807440697c4d5381be7a0a0027b79f85bdf3` |
| `finalization` | `R5-FIN-01`, `R5-FIN-02`, `R5-FIN-03`, `R5-FIN-04`, `R5-FIN-05`, `R5-FIN-06`, `R5-FIN-07`, `R5-FIN-08` | 8 | `14330e67aa5a4bbb72869f68806dc88757de40fe65e1dc1767a67008647cd8e5` |
| `export` | `R5-EXP-01`, `R5-EXP-02`, `R5-EXP-03`, `R5-EXP-04`, `R5-EXP-05`, `R5-EXP-06` | 6 | `6d4ca77b8da2019bbfa4f3f1046c62d27d4c9fceb1b2d4c12105f13d8e87b340` |
| `conformance` | `R5-CONF-01`, `R5-CONF-02`, `R5-CONF-03`, `R5-CONF-04`, `R5-CONF-05`, `R5-CONF-06` | 6 | `5960be1734aed1a66b382de36e98723dcee41f4919299835963d01f818577c9a` |

The complete 34-ID digest is
`507186e7489a3f9eec18eb5de78692dbc55a8d1d2d106544aa4295a98ac9be60`.

#### Behavioral coverage matrix

Every registration named below is an explicit executable registry entry, not a
test-name search. `BAPI` = `R5_API_CASES` in backend API tests; `FDB` =
`R5_DB_CASES` in handoff integration; `FAPI` = `R5_FRONTEND_CASES` in frontend
API tests; `FCOMP` = `R5_COMPONENT_CASES` in frontend component tests; `BR` =
`R5_BROWSER_CASES` in the emitted browser harness; `CONF` =
`R5_CONFORMANCE_CASES` in the new enforcement test.

| Case | Scenario / production path and starting partition | Actions and activation witness | Exact result / operations / forbidden result | Control | Parity / registration |
|---|---|---|---|---|---|
| `R5-WIRE-01` | `SCN-KI-036`; queued W4 view→W5 parser | Parse exact numeric-v1 queued response | deep-equal pass; zero mutation; string absent | `NC-01` | component / `FAPI` |
| `R5-WIRE-02` | `SCN-KI-036`; completed actual W4 serializer→W5 parser | Serialize real parity-shaped completed research, parse envelope | numeric v1/result and all rows deep-equal; no invented field | `NC-01` | component / `FAPI` |
| `R5-WIRE-03` | `SCN-KI-036`; bad version partitions | Try string, 0, 2, null, missing in view/result | each `ApiPayloadError`; zero UI state | `NC-01` | unit / `FAPI` |
| `R5-WIRE-04` | `SCN-KI-038`; create client→emitted Next pre-auth route | Submit through real client with fixture interception disabled for this call | request JSON header/body; real route 401, never 415; one request | `NC-02/11` | emitted artifact / `BR` |
| `R5-WIRE-05` | `SCN-KI-036`; save client fetch boundary | Capture one 200-item request init | PUT, JSON header, strict minimal body ≤262144; no derived fields | `NC-02/03` | component / `FAPI` |
| `R5-WIRE-06` | `SCN-KI-036`; handoff client fetch boundary | Capture one handoff init | POST, JSON header, exact two-key body, one call | `NC-02` | component / `FAPI` |
| `R5-SEL-01` | `SCN-KI-036`; completed owner + one calculated input | Materialize by persisted source ID then save | exact full canonical item; one read/one CAS | `NC-03` | component / `BAPI` |
| `R5-SEL-02` | `SCN-KI-036`; completed owner + manual input | Normalize, derive ID/seed/classification then save | exact `DEC-KI-002` ID and null metrics/source; one CAS | `NC-03` | component / `BAPI` |
| `R5-SEL-03` | `SCN-KI-036`; legacy/unknown union members | Add itemId/metrics/lane/facets/owner or bad discriminator | 400; zero repository save | `NC-03` | component / `BAPI` |
| `R5-SEL-04` | `SCN-KI-036`; duplicate calculated source | Submit same calculated input twice | 400 duplicate; zero CAS; not a conflict component | `NC-04` | component / `BAPI` |
| `R5-SEL-05` | `SCN-KI-036`; two normalization-equal manual texts | Materialize then validate | 400 duplicate derived ID; zero CAS | `NC-04` | component / `BAPI` |
| `R5-SEL-06` | `SCN-KI-036`; 200 max-code-point calculated inputs | Send 143641-byte valid body through real W4 server route | 200; exactly 200 canonical items; one CAS; no 413 | `NC-03` | server component / `BAPI` |
| `R5-SEL-07` | `SCN-KI-036`; 201 minimal inputs | Parse API request | 400; zero owner read/save | `NC-03` | component / `BAPI` |
| `R5-SEL-08` | `SCN-KI-036`; body 262145 bytes | Send to real W4 selection route | 413 before API/owner read | `NC-03` | server component / `BAPI` |
| `R5-FIN-01` | `SCN-KI-038`; completed, saved 1–100 draft | Finalize once | one POST with current revision/one ID; navigate on success | `NC-05` | component / `FCOMP` |
| `R5-FIN-02` | `SCN-KI-038`; saved draft then add/remove | Exercise each mutation without save, attempt finalize | `unsaved`; zero POST for both partitions | `NC-05` | component / `FCOMP` |
| `R5-FIN-03` | `SCN-KI-038`; saved draft then edit/reorder/manual add | Exercise all three, attempt finalize | each `unsaved`; zero POST | `NC-05` | component / `FCOMP` |
| `R5-FIN-04` | `SCN-KI-038`; dirty draft then successful save | Save canonical response/revision, finalize | PUT once then POST once with incremented revision; exact saved items | `NC-05` | component / `FCOMP` |
| `R5-FIN-05` | `SCN-KI-038`; saved draft, network/unreadable/502/504 outcomes | For each, fail first POST then retry | retry-required; controls locked; second POST same ID/revision | `NC-06` | component / `FCOMP` |
| `R5-FIN-06` | `SCN-KI-038`; definitive 409 | Return parsed 409 then reload/save path | stale UI; attempt cleared; no automatic retry/run | `NC-06` | component / `FCOMP` |
| `R5-FIN-07` | `SCN-KI-037`; two concurrent equal requests | Release both against real Prisma unique | two fulfilled: one created/one found; one handoff/Run/query set | `NC-07` | isolated DB / `FDB` |
| `R5-FIN-08` | `SCN-KI-037`; same key unequal fingerprint/revision | Create then unequal replay | conflict; one handoff/Run; later equal replay found | `NC-07` | isolated DB / `FDB` |
| `R5-EXP-01` | `SCN-KI-039`; rows with A, B, A+B flags | Apply UI and W4 filters for flags A+B | both retain only A+B literal ID, persisted order | `NC-08` | cross-component / `FAPI` |
| `R5-EXP-02` | `SCN-KI-039`; each allowed search corpus field | Search keyword/source seed/cluster/lane/facet/flag | UI and W4 retain exact literal IDs for every field | `NC-09` | cross-component / `FAPI` |
| `R5-EXP-03` | `SCN-KI-039`; value exists only in intent or synthetic recommendation text | Search excluded words | zero rows on both sides unless also in allowed corpus | `NC-09` | cross-component / `FAPI` |
| `R5-EXP-04` | `SCN-KI-039`; cumulative and named-market projection | Apply same conjunctive filter/query | literal item IDs/order and CSV rows equal; null market excluded | `NC-08/09` | cross-component / `FAPI` |
| `R5-EXP-05` | `SCN-KI-039`; all dangerous textual prefixes + negative trend | Export once and parse cells | each dangerous text has one leading apostrophe; numeric negative unchanged | `NC-10` | unit / `BAPI` |
| `R5-EXP-06` | `SCN-KI-039`; zero match and forbidden internal fields | Export owner result | exact header+LF; no config/owner/raw/credential/fingerprint fields | `NC-10` | component / `BAPI` |
| `R5-CONF-01` | `SCN-KI-040`; final manifest | Parse root/groups/literals | exact five groups/counts/digests; duplicates fail first | `NC-12` | static / `CONF` |
| `R5-CONF-02` | `SCN-KI-040`; all final registries | Enumerate and merge after execution | required=registered=executed 34; zero skip/extra/duplicate/unactivated | `NC-12` | conformance / `CONF` |
| `R5-CONF-03` | `SCN-KI-040`; accepted W4/W5 tests changed | Compare the exact `DEC-KI-037` 6-W4/12-W5 mutable-oracle sets, all stable registrations, the 15 browser rerun set, and A7 invalidation | only the 18 listed oracles may change and cite R5 cases; all other IDs/registrations/witnesses/oracles unchanged | `NC-12` | static / `CONF` |
| `R5-CONF-04` | `SCN-KI-040`; final worktrees | Compare changed paths/symbol hunks to 18-path scope | exact subset, no package/schema/worker/route/auth/W6 edit | `NC-12` | static / `CONF` |
| `R5-CONF-05` | `SCN-KI-040`; three substitute classes | Assert serializer/parser, fetch capture, Next pass-through and DB fidelity | each claim limited per `DEC-KI-037`; intercept cannot satisfy route witness | `NC-11/12` | conformance / `CONF` |
| `R5-CONF-06` | `SCN-KI-040`; enforcement controls | Remove/skip/duplicate/add/bypass/weaken/diverge in memory | each execution/document lint fails, restored production passes | `NC-12` | conformance / `CONF` |

Control cells above abbreviate the exact IDs `R5-NC-01` through `R5-NC-12`.
Every control first runs the named production case and unchanged oracle to
PASS, applies only the listed test-boundary mutation/substitute, requires that
same oracle to throw `AssertionError` with the listed message, then discards
the mutation and reruns fresh production to PASS. A different valid input,
source edit, mutable global leak or a separate weaker assertion cannot satisfy
a control.

#### Literal falsification controls

| Control | Owning case/registry | Exact safe mutation or divergent substitute | Unchanged oracle and required failure |
|---|---|---|---|
| `R5-NC-01` | WIRE-01/02/03; `FAPI` | Deep-clone the actual W4-serialized object and replace only numeric `contractVersion:1` with string `"1"` before the actual W5 parser. | The same parse/deep-equality oracle throws `R5_NUMERIC_VERSION_REQUIRED`; fresh numeric object passes. |
| `R5-NC-02` | WIRE-04/05/06; `FAPI/BR` | Deep-clone the captured actual mutation `RequestInit` and delete only its case-insensitive content-type header. | The same exact-init oracle throws `R5_JSON_CONTENT_TYPE_REQUIRED`; fresh actual init contains exactly an application/json media type. |
| `R5-NC-03` | SEL-01/02/03/06/07/08; `BAPI` | Add forbidden `itemId` to one captured minimal item and separately replace the recorded accepted max-body result with a synthetic 413 event. | Strict-member/status/write-count oracle throws `R5_SELECTION_WIRE_OR_LIMIT_DIVERGED`; fresh minimal 143641-byte maximum passes and 262145 bytes fails. |
| `R5-NC-04` | SEL-04/05; `BAPI` | After actual duplicate rejection, append one synthetic `repository.saveSelection` event to a copied operation trace. | Unchanged 400-and-zero-CAS oracle throws `R5_DUPLICATE_WRITE_FORBIDDEN`; fresh production trace has zero save. |
| `R5-NC-05` | FIN-01/02/03/04; `FCOMP` | After an actual dirty-partition run, append one synthetic handoff POST to the copied request trace. | The same `unsaved` plus zero-POST oracle throws `R5_UNSAVED_HANDOFF_FORBIDDEN`; fresh dirty run passes. |
| `R5-NC-06` | FIN-05/06; `FCOMP` | Copy the two-request ambiguous trace and replace only the retry request ID, then separately its revision. | Same byte-equal ID/revision and locked-controls oracle throws `R5_AMBIGUOUS_RETRY_IDENTITY_DIVERGED`; fresh actual retry passes. |
| `R5-NC-07` | FIN-07/08; `FDB` | For the losing call only, use a non-mutating Prisma client Proxy that converts the fresh exact-handoff read after the recognized unique error to null; do not alter production source or the winning transaction. | Same `Promise.allSettled` two-fulfilled/one-Run oracle throws `R5_EQUAL_RACE_NOT_RECONCILED`; unwrapped client passes in a fresh fixture in the same schema. |
| `R5-NC-08` | EXP-01/04; `FAPI` | Feed the literal rows/filters to a test-only divergent predicate that uses `some` instead of `every` for selected flags. | Same literal ordered-ID oracle throws `R5_FLAG_AND_REQUIRED`; actual W4 and W5 predicates both pass. |
| `R5-NC-09` | EXP-02/03/04; `FAPI` | Feed the literal rows/search to a test-only divergent predicate adding `mainIntent` and synthetic `recommended` text to the allowed corpus. | Same literal ordered-ID oracle throws `R5_SEARCH_CORPUS_DIVERGED`; actual W4 and W5 predicates both pass. |
| `R5-NC-10` | EXP-05/06; `BAPI` | Copy actual CSV bytes and remove the single neutralizing apostrophe from the first dangerous textual data cell only. | Same parsed-cell/numeric-byte oracle throws `R5_CSV_TEXT_UNSAFE`; fresh export passes and negative numeric trend bytes remain unchanged. |
| `R5-NC-11` | WIRE-04/CONF-05; `BR/CONF` | Supply only an intercepted fixture-success record while omitting the emitted real-Next request activation record/status. | Same substitute-evidence validator throws `R5_REAL_NEXT_ROUTE_WITNESS_MISSING`; fresh pass-through reaches 401 and never 415. |
| `R5-NC-12` | CONF-01..06; `CONF` | In separate copied evidence values: remove one required registration; mark one required ID skipped/filtered; duplicate one ID; add one unexpected ID; clear one activation witness; replace one forbidden-operation count with no assertion; label intercepted presentation evidence as route evidence. | The same document/execution lint respectively throws `R5_REQUIRED_SET_MISMATCH`, `R5_REQUIRED_CASE_SKIPPED`, `R5_CASE_ID_INVALID` for each of duplicate and unexpected, `R5_ACTIVATION_WITNESS_MISSING`, `R5_ORACLE_WEAKENED`, and `R5_SUBSTITUTE_FIDELITY_DIVERGED`; untouched evidence passes after every variant. |

#### Scenario ledger

- **`SCN-KI-036` — wire and bounded canonical selection:** covers numeric
  response partitions, three mutation headers, strict union variants, 0/200/201
  items, 262144/262145 bytes, calculated/manual/duplicate inputs. Preconditions
  are completed owner views and actual serializers/parsers/server handlers;
  actions and witnesses are the WIRE/SEL rows. Oracle is exact parse/materialize/
  status/write counts with no raw field. Exhaustive over behavior-changing union,
  version and cardinality boundaries; text examples are equivalence classes.
  Cleanup is in-memory server close only.
- **`SCN-KI-037` — handoff uniqueness:** uses one verified disposable schema,
  two equal or unequal request schedules and real Prisma. Oracle is exactly one
  durable handoff/Run/query set and the FIN-07/08 outcomes. Control removes the
  reconciliation result through a test client/proxy. Finally disconnects and
  drops only the named schema, then asserts absence.
- **`SCN-KI-038` — saved and ambiguous frontend lifecycle:** crosses draft
  mutation `{none,add,remove,edit,reorder,manual}`, outcome
  `{success,4xx,network,unreadable,502,504}`, and retry `{none,same}` using
  pairwise coverage plus every ambiguous outcome. Activation is actual component
  state/request capture; one emitted case enters the real Next handler. Oracle
  is saved-only zero/one calls and same-key retry. No auth/backend success claim
  is made by interception; browser processes are killed in `finally`.
- **`SCN-KI-039` — filter and safe export parity:** exhausts every filter field,
  multi-flag AND, allowed/excluded search corpus, cumulative/named market,
  dangerous textual prefix and negative numeric partitions. Literal IDs/cells
  are the oracle; neither implementation generates the other's expected set.
  Pure/component cleanup only.
- **`SCN-KI-040` — enforcement/scope/substitute closure:** parses the literal
  manifest, enumerates registries, recomputes all digests, checks accepted-test
  supersession and 18-path symbol scope, then runs every enforcement
  falsification in memory. Zero network/database/provider/AWS operations.

#### Frozen verification

- [x] `KI-R5-V1` On final frozen non-DB inputs, execute only the named backend R5 API/export and enforcement registries; require all selected cases pass with zero skip/todo and no legacy W4 regression. Evidence: `EV-KI-R5-I001-01`; `EV-KI-R5-I004-02`.
- [x] `KI-R5-V2` Execute `node --experimental-strip-types --test test/keyword-intelligence-api.test.ts test/keyword-intelligence-components.test.ts test/keyword-intelligence-inventory.test.ts` once from `frontend/`; require all selected R5 and existing cases pass, no skip, and actual serializer→parser/fetch-init witnesses. Evidence: `EV-KI-R5-I001-03`; `EV-KI-R5-I004-02`.
- [x] `KI-R5-V3` With `ALLOW_DATABASE_TESTS=true` and an isolated non-production `TEST_DATABASE_URL`, execute only `R5-FIN-07/08` once in one disposable schema; require two fulfilled equal calls, one Run, unequal conflict, zero residual schema. Evidence: `EV-KI-R5-I001-08`–`11`; `EV-KI-R5-I004-02`.
- [x] `KI-R5-V4` Run `npm run check` once from `frontend/`, then run the emitted keyword browser harness once with `KI_W5_SKIP_BUILD=1`; require all prior presentation cases plus `R5-WIRE-04` pass, real route status 401 not 415, zero required skips/console errors/non-app URLs, and no intercepted-route substitution. Evidence: `EV-KI-R5-C005-02`; `EV-KI-R5-I002-01/02`; `EV-KI-R5-I004-02`.
- [x] `KI-R5-V5` Run backend `npm test` once and `npm run check:secrets` once; require zero failures and only the previously guarded database skips. No Prisma generate/validate or handler build is required. Evidence: `EV-KI-R5-I002-05`; `EV-KI-R5-I004-02`.
- [x] `KI-R5-V6` Independently recompute all five group digests and the global digest; require exact required=registered=executed 34-ID equality, zero skip/duplicate/unexpected/unactivated/oracle failure, and every `NC-01`–`NC-12` falsifies its unchanged acceptance oracle before restored production passes. Evidence: `EV-KI-R5-I004-01/02`.
- [x] `KI-R5-V7` Assert 0, 1, 100, and 200 valid selections, 201 rejection, 143641-byte maximum valid mutation, 262145-byte rejection, O(n²) comparisons bounded at 19900, one CAS, one Run under concurrency, CSV textual safety/numeric stability, owner privacy, and exact 18-path/symbol diff. Evidence: `EV-KI-R5-I004-01/02`.

#### Append-only KI-R5-V4 console classification (`EV-KI-A-072`)

- [x] `KI-R5-V4-A1` Supersede only the unqualified phrase “zero console
  errors” in `KI-R5-V4`: require zero application-generated console
  error/assert messages and zero unexpected browser console errors. Permit
  exactly one Chrome network-source diagnostic with exact text `Failed to load
  resource: the server responded with a status of 401 (Unauthorized)` only
  when the same execution proves the required browser-origin `R5-WIRE-04`
  request reached the emitted Next route, received the expected 401
  `AUTHENTICATION_REQUIRED` response, never received 415, and all other
  browser/error/network/certificate oracles pass. Zero entries, more than one
  entry, a different text/source/status, an application-generated error, or
  any entry without the passing WIRE-04 activation witness fails V4. This is
  an acceptance-classification correction only and authorizes no browser
  rerun or source/test edit. Evidence: `EV-KI-A-072`; `CHG-KI-047`.

#### Append-only KI-R5 CONF-04 scope correction and standards delta (`EV-KI-A-077`)

- [x] `KI-R5-CONF04-A1` Reproduce and classify the failure: the accepted E1
  recovery executed all six conformance registrations and failed only
  `R5-CONF-04` because `lintFinalWorktreeScope()` treats every nested-worktree
  status entry as an implementation edit. The rejected path is authorized
  browser-harness output, not product or test implementation. Evidence:
  `EV-KI-R5-I002-06`; `EV-KI-A-077`.
- [x] `KI-R5-CONF04-A2` Freeze the exact correction boundary. The one writable
  implementation file is
  `email_scraper/test/keyword-intelligence-r5-enforcement.test.js`, starting
  SHA-256
  `465b3d9fd5b43d2b5f34573a0ab392c58205ff4fce2b7f5b2b86abbdfed17bf4`.
  Keep `DELEGABLE_FILE_SET`, its 18 members and digest
  `efc82a884d09561ed27be3513ca6898f0ab311dbe56cf46e9c2c241492560077`
  unchanged.
  Add literal `ALLOWED_REVIEW_EVIDENCE_CHANGES` with these path/status pairs:
  four tracked modifications
  `frontend/review-evidence/keyword-intelligence/KI-W5/W5-R05-responsive.png`,
  `frontend/review-evidence/keyword-intelligence/KI-W5/artifact-index.json`,
  `frontend/review-evidence/keyword-intelligence/KI-W5/browser-checks.json`,
  and
  `frontend/review-evidence/keyword-intelligence/KI-W5/browser-server.log`; and
  one untracked create
  `frontend/review-evidence/keyword-intelligence/KI-W5/R5-FIN-03-unsaved.png`.
  Absence of an allowlisted evidence path is permitted; any observed allowlisted
  path must have its literal status. Every other observed nested-worktree path
  remains subject to the unchanged 18-path, create-status and forbidden-token
  checks. No directory or wildcard exemption is permitted. Evidence:
  `EV-KI-A-077`; `CHG-KI-052`.
- [x] `KI-R5-CONF04-A3` Freeze enforcement mechanics. Add pure
  `validateFinalWorktreeChanges(changes)` and let
  `lintFinalWorktreeScope(additionalChanges = [])` pass the real status entries
  plus test-only injected entries through it. The unchanged current status must
  pass. Injecting
  `frontend/review-evidence/keyword-intelligence/KI-W5/UNEXPECTED.png` must throw
  `R5_UNEXPECTED_REVIEW_EVIDENCE_PATH`; injecting an allowlisted path with the
  wrong tracked/untracked state must throw
  `R5_REVIEW_EVIDENCE_STATUS_MISMATCH`; a fresh unchanged invocation must pass.
  Preserve `R5-CONF-01`–`06`, all 34 IDs, registries, certificate shapes and
  digests. Evidence: `EV-KI-A-077`; `CHG-KI-052`.
- [x] `PA-008` A5 grants standing sandbox escalation only for already-authorized
  local actions and explicitly preserves external-authority gates. Evidence:
  `EV-KI-A-074`; `EV-KI-A-075`.
- [x] `PS-021` The frozen-gate protocol distinguishes proven environment
  invalidation from observable behavioral or invocation failure and permits
  only one identical escalated recovery under the former. Evidence:
  `EV-KI-A-073`–`076`; `CHG-KI-048`–`051`.
- [x] `PR-013` The current history mechanically falsifies both forbidden
  classifications: malformed E1 input and the observable CONF-04 assertion
  were stopped for parent adjudication rather than relabelled as sandbox
  invalidation, while the V5 channel-loss attempt alone used identical
  recovery. Changed commands and external authority remain prohibited.
  Evidence: `EV-KI-R5-I002-03`–`06`; `EV-KI-A-074`–`077`.

The window agent must first record the parent- and sub-window-standard revision
delta from
`3b7a4fd25156e1adfbc92abb835c5f82a0d18c686b1c1150feb202f2d944d2ac` /
`1766f9107ce7d315877b75d4b0ea2b5521dff1c321e12f890b03787d66196ded`
to
`cda352017e75c0d11f6797d9fbe108b4365508cd38b0e92365cfb523ede32848` /
`84e7590e74589f308c70dc9b0b67f7e9da395fafb1e5786202ecd1ca15be56e9`,
append and check `SW-A07`, `SW-V11`, and `SW-R11`, then author the
decision- and execution-complete single-file corrective sub-window
`KI-R5-C006`. It must also author window-agent integration assessment
`KI-R5-I003`, which runs corrected E1 once with the already-validated canonical
four-certificate transport, then the previously unexecuted V6 and V7. V1–V5
are reused only with recorded dependency proof; in particular, V5 reuse must
prove that its command does not set `KI_R5_EXECUTED_CERTIFICATES` and therefore
never activates the corrected CONF-04 branch. The window agent returns the
revised decomposition for parent review before assigning `KI-R5-C006`.

#### Append-only KI-R5 final corrective supersession and acceptance

- [x] `KI-R5-C007-A1` Supersede rejected `KI-R5-C006` and unstarted
  `KI-R5-I003` with the requester-directed `KI-R5-C007`/`KI-R5-I004`
  sequence. Because both enforcement paths were already requester-committed,
  the final status oracle requires `untracked:false` and rejects
  `untracked:true`; the implementation change is the single assertion added
  by requester commit `0083a42`, ending at SHA-256
  `f9a593fbb50ba4bc7d603e2c5fafe3129356cb758d022a5b83cef05f0ed3b954`.
  Both implementation-path status controls and both review-evidence controls
  pass, with no wildcard exemption or other oracle change. Evidence:
  `EV-KI-R5-C006-05`; `EV-KI-R5-C007-01`–`03`.
- [x] `KI-R5-I004-A1` Accept the requester-directed final assessment. The
  canonical 2,847-byte certificate transport hashes to `63eedf90…`; E1 passes
  `R5-CONF-01`–`06` 6/6 with required=registered=executed=activated 34 IDs
  and digest `507186e7…`; V6 and V7 pass; all twelve negative controls
  falsify; both nested repositories are clean; and no KI-W6 work began.
  Evidence: `EV-KI-R5-I004-01/02`.

This subsection supersedes only the stale C006/I003 continuation paragraph
above. It does not rewrite its historical diagnosis or evidence.

#### Handoff

- [x] `KI-R5-H1` Record changed files/symbols, starting/ending hashes, and confirm no schema/migration/package/generated file. Evidence: `EV-KI-R5-I004-02`.
- [x] `KI-R5-H2` Record exact commands, cases, activation witnesses, outcomes, skips, controls, frozen-gate invalidations/reruns, database schema and cleanup. Evidence: `EV-KI-R5-I001-01`–`14`; `EV-KI-R5-I002-01`–`06`; `EV-KI-R5-I004-01/02`.
- [x] `KI-R5-H3` Prove the actual diff is a subset of the 18 paths and exact shared-symbol scopes; unrelated accepted tests/fixtures and both repository baselines are accounted for. Evidence: `EV-KI-R5-I004-02`.
- [x] `KI-R5-H4` Record zero provider/AWS/production/destructive/agent-commit action and zero KI-W6 leaf/integration work; requester commits are disclosed separately. Evidence: `EV-KI-R5-C007-03`; `EV-KI-R5-I004-01/02`.
- [x] `KI-R5-H5` Window agent appends its consolidated S3 `WINDOW-AGENT-INTEGRATION-PASS` and stops at `READY_FOR_PARENT_REVIEW`; it does not edit A5/A6 or assign KI-W6. Evidence: `EV-KI-R5-I004-02`.
- [x] `KI-R5-H6` Parent-only transition completed; the invalidated KI-W6 decomposition remains unusable and no successor work begins. Evidence: `EV-KI-A-080`; `CHG-KI-055`.

### `KI-W6` — Causal local workflow proof and run-workspace correction

```yaml
window_id: KI-W6
objective: Correct successful dashboard navigation to the real run workspace and prove one causal maximum local workflow from authenticated seeds through durable keyword research, saved selection, immutable Run/RunQuery handoff, query confirmation, 100 Google probes, and the 1000-domain downstream lead-task boundary.
depends_on: [KI-R5]
consumes: accepted KI-R5 code/evidence; DEC-KI-038; existing Prisma, keyword worker, Next route/auth/proxy, query-review/Google parser, discovery and domain-aggregation implementations
produces: corrected workspace navigation; one 26-case causal local certificate; exact obsolete-runtime exclusion; no deployment artifact or cloud mutation
assigned_agent_policy: parent_assigns_one_window_agent_only
window_agent_role: KI-W6-WINDOW-AGENT
window_agent_coordination_scope: [KEYWORD_INTELLIGENCE_KI_W6_REAUTHORED_SUBWINDOW_CHECKLIST.md, KEYWORD_INTELLIGENCE_KI_W6_REAUTHORED_SUBWINDOW_STATE.md, KEYWORD_INTELLIGENCE_KI_W6_REAUTHORED_SUBWINDOW_EVIDENCE.md]
delegable_implementation_write_scope: [email_scraper/test/fixtures/keyword-intelligence/ki-w6-enforcement-manifest-v1.json, email_scraper/test/helpers/keyword-intelligence-e2e-harness.js, frontend/components/keyword-intelligence/research-dashboard.tsx, frontend/test/browser/keyword-intelligence-dashboard.mjs, frontend/test/browser/keyword-intelligence-e2e.mjs]
delegable_file_set_digest_sorted_member_lf_sha256: d28ae17864073639580d7650bb03c03474d5370a5034b632cf412e1e3cf3d0bb
starting_file_digests: [email_scraper/test/fixtures/keyword-intelligence/ki-w6-enforcement-manifest-v1.json=ABSENT, email_scraper/test/helpers/keyword-intelligence-e2e-harness.js=ABSENT, frontend/components/keyword-intelligence/research-dashboard.tsx=19494a99a2be28683167908289176bf44ebb8d0bb1eb40f63cc6d1cd770c6337, frontend/test/browser/keyword-intelligence-dashboard.mjs=d30bed66cdc77ff53438515345be01baf2e1ad90ea2b9b8c8ab71c47f339c398, frontend/test/browser/keyword-intelligence-e2e.mjs=ABSENT]
repository_baselines: [email_scraper=0083a42c5582aeb8d9d8998e8ce9e1cc1d52b43e, frontend=70fb5edfcfe092ca8d153bb025116b96cf1897b3]
shared_file_scope: frontend/components/keyword-intelligence/research-dashboard.tsx only the two successful router.push expressions; frontend/test/browser/keyword-intelligence-dashboard.mjs only the R5-FIN-01 handoff fixture/comment/navigation oracle; every other existing symbol/oracle is read-only
read_only_scope: every unlisted workspace path; all Prisma schema/migrations/packages; backend production source; frontend routes/auth/proxy/types/client/view-model/selection/run workspace; accepted W3/R4/R5 fixtures/tests/evidence; standalone KeywordSearchVolume repository
authorized_actions: [author fresh parent-bounded S1/S2/S3, sequentially delegate exactly one listed implementation file per leaf, window-agent independent leaf review, local source/test edits inside one leaf file, file-local diagnostics, one final frontend npm run check, one final emitted local Next start and Chrome CDP run against one isolated migrated test schema, one final backend npm test, one final backend secret scan, read-only negative searches, captured-data negative controls, window-agent consolidated handoff]
execution_environment_policy: sandbox escalation is standing-authorized for already-authorized local commands; a proven sandbox or execution-channel invalidation permits one identical escalated recovery after exact read-only postconditions; observable product/test failure is not an environment invalidation
prohibited_actions: [reuse/edit/cite state-108 KI-W6 decomposition as proof, multi-file leaf, leaf-to-parent communication, browser application-API response substitution or request short-circuit in SCN-KI-018, schema/migration/package/backend-production/route/auth/proxy/worker/adapter/infrastructure edits, full opted-in database suite, Prisma generate/validate, handler build, full W5 browser rerun, standalone-project edit/delete, provider calls, AWS operations, production database writes, destructive shared cleanup, commits/pushes, KI-W7 work]
successor: KI-W7
successor_reserved_for: parent
may_start_successor: false
stop_after: KI-W6
```

The old `KEYWORD_INTELLIGENCE_KI_W6_SUBWINDOW_{CHECKLIST,STATE,EVIDENCE}.md`
package is immutable invalidated history. The W6 window agent must create the
three exact `REAUTHORED` artifacts above from the pinned current sub-window
standard, use new sub-window/assignment/evidence IDs, and stop for parent
decomposition approval before dispatching any leaf. It may not copy the old
two-file proof topology, case IDs, interpretations, or certificates.

- [ ] `KI-W6-P1` Recompute A1–A5, both standard hashes, state version, both
  repository commits/statuses and the five starting states; require A5 to assign
  only `KI-W6-WINDOW-AGENT`, `accepted_through:KI-R5`, `may_start_successor:false`,
  and the exact coordination-only write scope. Evidence: ___
- [ ] `KI-W6-P2` Recompute the sorted-member-plus-LF five-file digest exactly as
  `d28ae17864073639580d7650bb03c03474d5370a5034b632cf412e1e3cf3d0bb`;
  require no duplicate/missing/unowned path and preserve unrelated dirty root
  relocation state. Evidence: ___
- [ ] `KI-W6-P3` Read the installed Next route-handler, environment-variable and
  testing guides; verify Node/Next/Chrome exist; resolve the configured
  `TEST_DATABASE_URL` through `test/helpers/isolated-postgres.js`, prove it is
  distinct from `DATABASE_URL`, and plan one non-`public` disposable schema.
  No database connection or build occurs during decomposition. Evidence: ___
- [ ] `KI-W6-P4` Reproduce `SRC-KI-038` at the pinned frontend/backend baselines:
  API `statusUrl` is `/api/runs/<id>`, both dashboard success branches navigate
  to it, and the UI workspace route is `/runs/[runId]`. Evidence: ___
- [ ] `KI-W6-P5` Author a complete sequential one-file-leaf DAG for exactly the
  five paths, the exact interfaces below, and one zero-implementation-write
  integration assessment. All mandatory `SW-*` boxes must be checked with
  evidence before parent decomposition review; no leaf is assigned yet. Evidence: ___
- [ ] `KI-W6-P6` Freeze one registration for every literal W6 case, all thirteen
  controls, certificate transport, cleanup ownership and invalidation-specific
  gate schedule; unresolved requirement/decision/task/case/interface/control/
  substitute/evidence counts must all be zero. Evidence: ___

#### Task block `KI-W6-T1` — Dashboard navigation correction

1. **Task:** change only the successful initial and retry navigation expressions
   so the browser opens the run workspace identified by the handoff Run.
2. **Requirements/decisions:** `REQ-KI-015`–`017`, `INV-KI-010`, `014`–`015`,
   `DEC-KI-035`, `038`; `SRC-KI-038`.
3. **Source:** `startKeywordResearchRun` returns a strict `RunHandoff` whose
   `run.runId` is the public workspace identity and whose `statusUrl` remains
   the API status resource.
4. **Target:** `frontend/components/keyword-intelligence/research-dashboard.tsx`
   only `handleFinalize` and `handleRetryHandoff` successful branches.
5. **Interface/schema:** keep the `RunHandoff` schema, API response and all state
   transitions unchanged; consume only existing validated `handoff.run.runId`.
6. **Algorithm:** replace each exact `router.push(handoff.statusUrl)` with
   ``router.push(`/runs/${encodeURIComponent(handoff.run.runId)}`)``; no helper,
   fallback, route probe or conditional branch is permitted.
7. **Operations:** two expression replacements; zero I/O, fetch, database,
   provider, queue or artifact operation is added.
8. **Atomicity:** unchanged handoff transaction remains authoritative; routing
   occurs only after the existing successful response and never changes durable
   state.
9. **Identities:** use the returned `RunStatus.runId` exactly once per branch;
   never derive a run ID from research ID, `statusUrl`, pathname or browser state.
10. **Failure/replay:** every existing definitive/ambiguous failure state is
    unchanged; successful same-key retry routes to the same encoded Run ID.
11. **Dependencies/bounds:** native `encodeURIComponent`; no import, package,
    state, prop, component or public type change.
12. **Callers/obsolete:** both dashboard branches are exhaustive owners; the
    backend API/status route and `/runs/[runId]` page are read-only.
13. **Tests:** `W6-NAV-01`–`03`; `W6-NC-01`. Source witness requires exactly two
    new workspace expressions and zero remaining `router.push(handoff.statusUrl)`.
14. **Output:** user lands on `/runs/<encoded handoff.run.runId>` after either
    success; `statusUrl` stays available to non-browser API clients.
15. **Non-goals:** backend change, new route, redirect, status polling change,
    handoff state-machine change, UI redesign.

- [ ] `KI-W6-T1` Apply exactly the two navigation replacements.

#### Task block `KI-W6-T2` — Accepted R5 navigation-oracle supersession

1. **Task:** align only `R5-FIN-01` with the W6 navigation contract while
   preserving the stable R5 registration and every unrelated browser oracle.
2. **Requirements/decisions:** `REQ-KI-015`–`017`; `DEC-KI-037/038`.
3. **Source:** accepted `R5-FIN-01` currently treats a mutable `statusUrl` as the
   browser destination; `W6-NAV-01`–`03` are its superseding evidence.
4. **Target:** `frontend/test/browser/keyword-intelligence-dashboard.mjs`, only
   the `R5-FIN-01` fixture assignment/comment/final pathname assertion.
5. **Interface/schema:** keep `runHandoff` valid and keep `statusUrl` present;
   set it to a hostile distinct same-origin API URL while `run.runId` remains
   the expected workspace identity.
6. **Algorithm:** change the scenario so the expected pathname is exactly
   ``/runs/${encodeURIComponent(runHandoff.run.runId)}``; assert the hostile
   `statusUrl` pathname is not visited. Do not add a W6 registration here.
7. **Operations:** existing one finalize POST and one router transition remain;
   zero extra request, retry, screenshot or fixture-interception behavior.
8. **Atomicity:** unchanged; the fixture proves navigation only and makes no SQL
   claim.
9. **Identities:** compare literal expected path derived independently from the
   fixture Run ID, not production routing code.
10. **Failure/replay:** unchanged R5 cases retain retry/definitive partitions;
    only the successful R5-FIN-01 destination oracle is superseded.
11. **Dependencies/bounds:** no registry, case-set, certificate, output path,
    helper, port, build or browser lifecycle change.
12. **Callers/obsolete:** every byte/semantic oracle outside R5-FIN-01 remains
    read-only; no full W5/R5 harness rerun is required because causal W6 cases
    supersede this one assertion.
13. **Tests:** syntax check plus manifest/source conformance; actual behavior is
    executed in `W6-NAV-01`–`03`. `W6-NC-01` mutates captured routing choice back
    to `statusUrl` and the same destination oracle must throw.
14. **Output:** historically accepted fixture no longer blesses JSON/API
    navigation; its stable R5 ID remains.
15. **Non-goals:** change any other R5/W5 case, registration, screenshot,
    certificate, fetch interception, or presentation assertion.

- [ ] `KI-W6-T2` Supersede only the accepted R5-FIN-01 destination oracle.

#### Task block `KI-W6-T3` — Causal local service harness

1. **Task:** add the one reusable Node harness that owns the disposable schema,
   local auth server/provider request substitutes, actual backend server, strict memory S3/SQS, and
   deterministic queue driving used by the emitted browser proof.
2. **Requirements/decisions:** `REQ-KI-001`–`013`, `015`–`017`, `019`–`024`;
   `INV-KI-001`–`009`, `011`–`015`; `DEC-KI-001`–`024`, `026`–`038`.
3. **Source:** exact patterns in `test/helpers/isolated-postgres.js`,
   `test/keyword-intelligence-worker.test.js`,
   `test/helpers/aws-pipeline-e2e-harness.js`, `src/server.js::createLeadServer`,
   and accepted strict fixtures; copy no standalone Python/runtime code.
4. **Target:** new
   `email_scraper/test/helpers/keyword-intelligence-e2e-harness.js` only.
5. **Interface/schema:** export exactly
   `createKeywordIntelligenceE2eHarness({testDatabaseUrl,testDirectDatabaseUrl,
   productionDatabaseUrl})`; return a frozen object exposing
   `{frontendEnv,ownerId,otherOwnerId,trace,setAuthOwner,drainKeywordWork,
   restartBackend,drainDownstream,readDurableState,injectCapturedDefect,close}`.
   `frontendEnv` contains exactly local `BACKEND_API_BASE_URL`,
   `BACKEND_API_TOKEN:"kiw6-backend-token"`, `NEON_AUTH_BASE_URL` and
   `NEON_AUTH_COOKIE_SECRET:"kiw6-local-e2e-cookie-secret-0000000000000000000000"`;
   the emitted Next
   child receives those four values plus only `PATH`, `HOME` and
   `NODE_ENV:"production"`. Neither test-only credential is logged or placed
   in a certificate. The backend uses the same literal token.
6. **Algorithm:** create one safe unique `kiw6_` schema, deploy migrations and
   assert schema locality; start a loopback auth server whose `GET /get-session`
   returns exactly `{user:{id:<selected nonempty owner>}}` with status 200 for
   owner mode and JSON `null` with status 200 for no-session mode; auth and
   backend servers bind only `127.0.0.1` with port `0` and publish their actual
   `server.address().port` through `frontendEnv`; create actual
   Prisma repositories and backend server with `executionBackend:"aws"`; supply
   DataForSEO only through the existing `runtime.http` function; inject the
   existing `researchQueryValidationPipeline` option as a thin wrapper that
   calls production `validateResearchBackedConfirmedQueryRows` with a
   deterministic `searchPage`, and require that search function to call
   production `parseGoogleSearchResponse` on the strict raw Google fixture for
   the received query; pass `createLeadServer.logger` as the callable no-op
   function `() => {}` (never an object), and inject
   `createLeadServer.schedule` as a FIFO callback
   queue so the harness, not wall-clock timing, deterministically starts each
   accepted queue-drain callback; start one fixed UTC clock and advance it by
   exactly 2,000 ms before each successive fresh keyword-provider claim so the
   base maximum trace satisfies the durable throttle without a deferral, while
   replay/fault cases advance only to their persisted due/expiry timestamp;
   raw task bodies report `0.01560000` for each of ten expansion calls,
   `0.04800000` for the 300-keyword anchor and `0.03600000` for each of eight
   200-keyword market calls, totalling `0.49200000`. Provider synthesis is
   literal: define `pad2(n)=String(n).padStart(2,"0")` and
   `pad3(n)=String(n).padStart(3,"0")`; for zero-based seed index `s` and
   one-based item index `i=1..30`,
   suggestions return `{keyword:` ``${seed} suggestion s${s}${pad2(i)}`` `}`
   and related returns `{keyword_data:{keyword:`
   ``${seed} related r${s}${pad2(i)}`` `},depth:2,related_keywords:[]}` in
   ascending `i`; the accepted per-seed cap therefore retains the seed, all 30
   suggestions and the first 29 related values, producing 300 distinct anchor
   inputs. Every overview item is produced in input order by the exact
   `overviewResponse` field/month formula at
   `test/keyword-intelligence-worker.test.js:93-122`; its response cost is
   `0.048` for 300 inputs and `0.036` for 200. Production aggregation must
   witness 300 active anchor candidates, the deterministic first 200 shortlist,
   and a 200-row final result/default-100 selection.

   For Google validation, deep-clone the accepted one-item fixture and replace
   `items` with ten one-based occurrences. With
   `queryProbeConcurrency:1`, received query ordinal `q` is exactly one plus
   the zero-based `searchPage` invocation index; for ordinal `q` and
   occurrence `r`, set exactly `title: receivedQuery`,
   `snippet: receivedQuery`, `displayLink: host`, and
   `link:` ``https://${host}/products/result-${pad2(r)}``, where `host` is
   ``w6-q${pad3(q)}-r${pad2(r)}.myshopify.com``; preserve all other top-level
   fixture members. Call `parseGoogleSearchResponse(payload, receivedQuery)`
   and pass its result through the production query-probe path. Each of all 100
   validations must witness ten usable distinct hosts, ten relevant results,
   relevance ratio `1`, and no rejection; parser success alone is not an
   acceptance oracle. The production discovery worker, not the harness, creates
   the 100 query artifacts from those persisted probe results. Drive only actual
   public worker/service functions until their durable readiness predicates
   settle.
7. **Operations:** record every auth, DataForSEO, Google, S3 and SQS operation as
   a privacy-safe typed tuple; strict artifact adapters parse schemas on put/get
   and reject unequal immutable replay; dispatch preserves each individual
   message and supports deliberate duplicate/reorder without batching identities.
8. **Atomicity:** use actual Prisma transactions for result publication,
   selection CAS, handoff and downstream coordinator. Fault hooks operate only
   before/after public calls; they never edit production source or directly
   fabricate a terminal database state.
9. **Identities:** deterministic five seeds, 100 retained keywords/queries,
   query IDs from the actual RunQuery creator, and hosts
   `w6-q<001..100>-r<01..10>.myshopify.com`; assert actual `stableShopIdentity`,
   `shopIdForStableKey` and `runStoreId` outputs rather than duplicating formulas.
10. **Failure/replay:** expose only the locked test operations: owner switch
    followed by emitted-Next restart so no auth-instance/cache state is reused;
    `duplicate-next-keyword-message`, `reorder-pending-keyword-messages`,
    `duplicate-next-discovery-message`, `reorder-pending-discovery-messages`,
    `duplicate-next-domain-check-message`, and
    `reorder-pending-domain-check-messages`; exactly two backend restarts,
    each retaining DB/S3/SQS: restart A immediately after the keyword
    duplicate/reorder operations and before expansion drain, and restart B
    immediately after the post-handoff research-selection mutation and before
    the immutable Run/RunQuery snapshot comparison; corrupt captured artifact
    before validated read; omit one Neon
    terminal while leaving its S3 object present; and replay the same client
    request ID. Each duplicate receives a fresh monotonic delivery ID without a
    dispatcher send trace; each reorder reverses the named queue's pending body
    order and reissues fresh increasing delivery IDs in that reversed order.
    Invoke the keyword duplicate/reorder immediately after initialization has
    queued expansion tasks/checks, invoke restart A, and then drain expansion.
    Invoke discovery duplicate/reorder immediately after confirmation dispatches
    the 100 discovery deliveries; after the first discovery emits a domain check,
    duplicate/reorder that check before completing downstream drain. Thus every
    partition operates on a nonempty queue and base dispatcher-send counts remain
    unchanged. The
    corrupt-artifact and missing-terminal partitions each use a separate
    one-seed research in the same schema: two expansion calls and two stored
    task objects; corrupt-artifact has two terminal tasks then mutates one memory
    object before the actual aggregate read, while missing-terminal throws only
    after the second immutable put so exactly one task is terminal. Both have
    zero next-stage rows/result visibility.
11. **Dependencies/bounds:** loopback only; one schema; 5 seeds; 19 keyword calls,
    exactly 23 keyword objects and 42 base keyword queue sends in the no-retry
    maximum trace; 100 Google calls/1,000 occurrences; 100 discovery tasks,
    1,000 stable domains/lead tasks; queue loop has an explicit step ceiling that
    throws with pending-message/state diagnostics rather than accepting partial work.
12. **Callers/obsolete:** only the new browser harness imports this helper. It
    may import existing backend test helpers and production exports but no
    Python, SQLite, output JSON, static dashboard, CDN or standalone project path.
13. **Tests:** supplies activation traces for `W6-FLOW-01`–`13` and
    `W6-RES-01`–`04`; negative controls `NC-02`–`09`, `12`. Every control mutates
    captured test state, not the production call path.
14. **Output:** frozen privacy-safe trace and durable projections sufficient for
    independent browser oracles and final certificate; no raw response/HTML,
    cookie, authorization header, credential-bearing URL or contact data.
15. **Non-goals:** generic framework, production test seam, live auth/provider/
    AWS call, Lambda emulation, lead scrape/enrichment, schema or package change.

- [ ] `KI-W6-T3` Add the exact causal local service harness.

#### Task block `KI-W6-T4` — Literal W6 enforcement manifest

1. **Task:** materialize the exact parent-owned case/control registry.
2. **Requirements/decisions:** all `DEC-KI-038` requirements; authoring standard
   E6–E8.
3. **Source:** the literal matrix and digests below; no discovered test list may
   generate required membership.
4. **Target:** new
   `email_scraper/test/fixtures/keyword-intelligence/ki-w6-enforcement-manifest-v1.json`.
5. **Interface/schema:** strict top-level keys only: `contractVersion`, `groups`,
   `groupDigests`, `globalDigest`, `negativeControls`; contract version exactly
   `ki-w6-enforcement-manifest-v1`; four exact group keys and thirteen exact
   control IDs.
6. **Algorithm:** encode the literal IDs in the matrix; arrays contain unique
   strings in ascending byte order; digests use sorted distinct UTF-8 member plus
   LF and equal the five parent literals in `DEC-KI-038`.
7. **Operations:** deterministic two-space JSON plus final LF; zero runtime I/O
   beyond fixture read.
8. **Atomicity:** N/A; whole-file strict parse is fail-closed.
9. **Identities:** case/control IDs are opaque stable identities and are not
   reused from the invalidated decomposition.
10. **Failure/replay:** missing/extra/duplicate/wrong-order/wrong-digest/wrong-
    group/unknown-key fixture fails conformance; identical replay is byte-equal.
11. **Dependencies/bounds:** exactly 26 cases and 13 controls; no wildcard,
    range expansion or dynamically generated required set in the fixture.
12. **Callers/obsolete:** consumed only by the new W6 browser harness; no earlier
    manifest/test is edited or treated as authority.
13. **Tests:** `W6-CONF-01/02`; `W6-NC-10` and manifest partitions.
14. **Output:** one literal non-secret JSON authority.
15. **Non-goals:** execution evidence, runtime config, provider fixture, old W6
    artifact repair.

- [ ] `KI-W6-T4` Add the literal manifest exactly as specified.

#### Task block `KI-W6-T5` — Emitted causal browser workflow and enforcement

1. **Task:** add the sole W6 executable registry, causal browser workflow,
   conformance engine and final certificate.
2. **Requirements/decisions:** all product requirements/invariants/exclusions
   and `DEC-KI-038`; `SCN-KI-018`.
3. **Source:** T1–T4 outputs; actual `/keywords` and `/runs/[runId]` pages;
   existing CDP process/readiness/cleanup patterns; installed Next docs.
4. **Target:** new `frontend/test/browser/keyword-intelligence-e2e.mjs` only.
5. **Interface/schema:** command supports normal execution and
   `KI_W6_SKIP_BUILD=1`; normal execution must refuse absent database opt-in;
   emit exactly one line `KI_W6_CERTIFICATE=<canonical JSON>` containing
   `{contractVersion,required,registered,executed,activated,skipped,duplicates,
   unexpected,unactivated,groupDigests,globalDigest,negativeControls,
   operationCounts,substituteClaims,obsoleteRuntimeHits}` and no secrets.
   `operationCounts` has exactly `baseMaximum`, `corruptArtifactFixture` and
   `missingTerminalFixture`. `baseMaximum` records the literal 19 calls/attempts,
   23 objects, 42 keyword sends, 100 selection/RunQueries/validation calls/
   discovery tasks, 1,000 occurrences/stable domains/lead tasks;
   `corruptArtifactFixture` records `2/2/2/0` for calls/objects/terminal tasks/
   next-stage rows; `missingTerminalFixture` records `2/2/1/0`.
6. **Algorithm:** import/strictly validate the manifest and helper; build unless
   explicitly skipped; start emitted Next with helper `frontendEnv`; use Chrome
   CDP with no application-API response substitution; for `W6-NAV-02` only,
   pause the first runs POST at CDP response stage, wait until the correlated
   backend trace and durable Run/100 RunQueries exist, then fail that response
   with zero supplied bytes so the UI enters `retry_required`; execute the 26 cases in manifest
   order, preserve an independent activation witness per case, run thirteen
   captured-data controls, recompute all sets/digests, emit the certificate only
   after every positive/control/scope/cleanup precondition passes.
7. **Operations:** all browser API calls must appear in Chrome network trace and
   matching auth/backend/helper traces; the sole response-stage abort described
   above must have a matching committed backend trace; only app-origin and loopback internal
   origins are allowed; screenshots/review files are forbidden; temporary logs
   live under one `mkdtemp` directory and are deleted after privacy-safe evidence
   has been emitted.
8. **Atomicity:** query durable rows before and after publication/handoff/fault
   partitions; require no partial result/selection/Run/RunQuery/domain terminal;
   queue/S3 state never substitutes for Neon readiness.
9. **Identities:** assert exact research, selection revision/fingerprint, Run,
   100 RunQuery, 100 discovery-task, 1,000 stable shop/run-store/lead-task sets;
   derive expected route from independently captured response `run.runId`.
10. **Failure/replay:** perform the exact owner/restart/duplicate/ambiguous/
    corrupt/missing-terminal partitions in the matrix; every retry uses durable
    identity and bounded step counters; no cancellation case.
11. **Dependencies/bounds:** Next binds only `127.0.0.1:4357`; fail preflight if
    occupied. One emitted build, one Chrome process at desktop and mobile
    viewport within the same run, one schema, no paid/cloud call;
    record wall time and peak child RSS without inventing a new acceptance ceiling.
12. **Callers/obsolete:** build the dependency inventory from exactly these
    roots: backend `package.json`, `scripts/build-keyword-worker.js`,
    `src/aws-pipeline/keyword-intelligence/handler.js`, `src/server.js`; frontend
    `package.json`, `app/keywords/page.tsx`,
    `app/keywords/[researchId]/page.tsx`, `app/runs/[runId]/page.tsx`,
    `app/api/keyword-research/route.ts`,
    `app/api/keyword-research/[researchId]/route.ts`,
    `app/api/keyword-research/[researchId]/selection/route.ts`,
    `app/api/keyword-research/[researchId]/runs/route.ts`, and
    `app/api/keyword-research/[researchId]/export.csv/route.ts`. Recursively
    resolve every literal relative or `@/` import/export/dynamic-import to
    `.js/.mjs/.ts/.tsx/.json/.css`; record bare package names from the two
    package files; fail any nonliteral local dynamic import or unresolved local
    edge. Scan that derived set for local `.py` references or Python spawn,
    SQLite imports/URLs, `KeywordSearchVolume`/standalone dashboard paths,
    `data/raw`, `data/output`, `output.json`, `file://`, and frontend runtime CDN
    hosts `cdn.jsdelivr.net`, `unpkg.com`, `cdnjs.cloudflare.com`. Provider URLs
    in backend adapters are not CDN hits. The standalone project itself is
    intentionally outside the roots and is never scanned as integrated code.
13. **Tests:** register/execute exactly the matrix; `NC-01`–`13`; zero skip,
    duplicate, unexpected, filtered, unactivated or oracle failure. Each positive
    passes before its mutation and again with a fresh witness afterward.
14. **Output:** one 26-case `local_e2e` certificate whose claims are bounded by
    the substitute ledger; parent handoff evidence references the actual line.
15. **Non-goals:** deploy/live parity, frontend/API feature expansion, full W5
    presentation rerun, Lambda build, lead fetching, infrastructure.

- [ ] `KI-W6-T5` Add and execute the sole causal W6 registry/certificate harness.

#### Authoritative `KI-W6` coverage matrix

Every row has exactly one planned registration in
`frontend/test/browser/keyword-intelligence-e2e.mjs`. “Forbidden” is an oracle,
not prose; its named control must falsify the same captured-data assertion.

| Case ID | Preconditions and action | Activation witness and exact oracle | Forbidden / control |
|---|---|---|---|
| `W6-NAV-01` | saved 100-item selection; successful first handoff | one runs POST; returned `run.runId`; browser reaches exact encoded `/runs/<runId>` and real workspace loads | navigation from `statusUrl`; `NC-01` |
| `W6-NAV-02` | first response made ambiguous after commit; retry same client key/revision | retry returns same Run; one durable Run; exact same workspace route | new key/Run or API route; `NC-01` |
| `W6-NAV-03` | handoff includes valid hostile distinct `statusUrl` | API field remains parseable/present; Chrome never requests/navigates to it | status URL browser authority; `NC-01` |
| `W6-FLOW-01` | owner-A browser creates research through emitted Next | Chrome→Next route→installed auth client→local session→proxy→actual backend chain has one correlated request; owner persisted | intercepted API response or injected owner header from browser; `NC-02/09` |
| `W6-FLOW-02` | submit exactly five distinct valid seeds, close tab, reopen URL | one queued g1 research; one initialize message; reopen reads durable queued/running state and causes no duplicate create | browser-owned job state; `NC-09` |
| `W6-FLOW-03` | drain expansion | exactly ten nonempty tasks/calls/attempts, five suggestion and five related; 300 unique capped candidates; locked reservation contribution | omitted/zero/bypassed expansion; `NC-03` |
| `W6-FLOW-04` | drain anchor screen | one 300-keyword US request/task/artifact; deterministic usable ordering yields exact 200 shortlist | pre-overview truncation or split anchor; `NC-03` |
| `W6-FLOW-05` | drain remaining markets and aggregate | eight 200-keyword calls; total 19 calls/attempts, 23 keyword objects, 42 base keyword queue sends, `$0.49200000`; one fenced 200-row result/default-100 selection becomes visible | unfenced/partial publication; `NC-04/05` |
| `W6-FLOW-06` | reload completed research at desktop/mobile | actual API result renders all accepted W5 surfaces, 200 rows and persisted 100-item selection; no fixture interception/CDN | static dashboard/fixture response; `NC-09/13` |
| `W6-FLOW-07` | exercise stale save, conflict resolution, then exact saved draft | numeric version `1`; minimal mutation only; stale 409/zero CAS; final one CAS at next revision with exactly 100 valid items | full/client-authoritative item or unsaved finalization; `NC-06` |
| `W6-FLOW-08` | hand off saved revision | one transaction exposes exactly one Run, 100 RunQueries and immutable selection snapshot or none; response uses same identities | split publication/missing query; `NC-06` |
| `W6-FLOW-09` | real run workspace edits and reorders all 100 queries | same 100 IDs; changed text/order persists; zero add/delete; keyword source lineage remains | regenerated/deleted identity; `NC-06` |
| `W6-FLOW-10` | confirm edited queries | exactly 100 production-validator searchPage calls, each passed through the strict Google parser with ten occurrences, 1,000 total; confirmation terminal only after all succeed | omitted/bypassed validation or product-only rewrite; `NC-07` |
| `W6-FLOW-11` | confirmation dispatches downstream | exactly 100 query-identity discovery tasks/messages/artifacts/terminal rows; duplicate/reorder adds no logical work | batched `itemIds` or queue-count completion; `NC-08` |
| `W6-FLOW-12` | actual domain aggregator consumes all terminal evidence | exactly 1,000 unique stable hosts, shops, run stores and lead tasks; one stable identity per occurrence host; stage completes once | raw URL identity/S3 count/queue empty; `NC-08` |
| `W6-FLOW-13` | edit research selection after handoff, invoke restart B, then reload and compare the durable run projection | original Run snapshot, 100 RunQueries, probe and downstream lineage remain byte/deep equal; research revision may advance independently | live research join mutates historical run or the post-handoff restart is omitted; `NC-06` |
| `W6-RES-01` | switch auth to owner B and restart emitted Next, then select no-session and restart again | research/run GET and mutations deny/not-found per accepted route contract; durable owner-A rows unchanged | owner leak, cached owner A or browser-supplied owner; `NC-02` |
| `W6-RES-02` | duplicate/reorder nonempty keyword queues across restart A, then duplicate/reorder nonempty discovery and domain-check queues at their frozen pre-drain points | provider counts, terminal counters, RunQueries and downstream logical work remain exact; recovery uses durable inputs | second paid/logical work, empty-queue no-op or memory-only recovery; `NC-03/08` |
| `W6-RES-03` | separate one-seed fixture completes two expansion calls/tasks, then corrupts one stored memory object before actual aggregate read | `2/2/2/0` calls/objects/terminal tasks/next-stage rows; typed contract failure and no result/selection/Run visibility | permissive parser/publication; `NC-04/05` |
| `W6-RES-04` | separate one-seed fixture stores both task objects but throws after the second put before Neon terminal; drain local queues then check | `2/2/1/0`; aggregator returns not-ready and produces zero next-stage/result visibility | S3/queue completion signal; `NC-08` |
| `W6-CONF-01` | strict manifest load | exact contract/keys, group counts `3/13/4/6`, 26 unique cases and 13 unique controls | manifest drift; `NC-10` |
| `W6-CONF-02` | after execution | required=registered=executed, independent group/global digests match | missing/duplicate/unexpected/filtered/skip; `NC-10` |
| `W6-CONF-03` | inspect case trace | 26 unique nonempty activation witnesses and zero unactivated/zero-work case | deleted/fabricated activation; `NC-11` |
| `W6-CONF-04` | inspect control trace | all 13 controls record pass→mutated-fail→fresh-pass against same oracle | vacuous/weakened control; `NC-11` |
| `W6-CONF-05` | compare calls to substitute ledger | every claim class is at or below its explicit fidelity; real app route has no fetch interception | divergent/broadened substitute; `NC-09/12` |
| `W6-CONF-06` | inspect exact five-file diff and literal integrated dependency inventory | only five owned files; old W6 docs/read-only paths unchanged; zero obsolete integrated runtime hit | wildcard scope or obsolete member; `NC-13` |

#### Critical falsification controls

| Control | Single captured-data mutation | Required failure |
|---|---|---|
| `W6-NC-01` | replace captured chosen route with handoff `statusUrl` | unchanged NAV destination assertion throws; fresh trace passes |
| `W6-NC-02` | remove auth-chain witness or substitute owner B as owner A | unchanged auth/ownership assertion throws; fresh trace passes |
| `W6-NC-03` | remove one expansion task/call/attempt tuple | unchanged exact topology/count assertion throws; fresh trace passes |
| `W6-NC-04` | mark a corrupted captured payload as parser-accepted | unchanged strict-contract assertion throws; fresh trace passes |
| `W6-NC-05` | add publication visibility without matching final fence | unchanged durable visibility assertion throws; fresh trace passes |
| `W6-NC-06` | remove one RunQuery or change snapshot/retry identity | unchanged atomicity/immutability assertion throws; fresh trace passes |
| `W6-NC-07` | remove one Google-call/ten-result tuple | unchanged 100/1,000 assertion throws; fresh trace passes |
| `W6-NC-08` | mark aggregation complete from S3/message counts with one Neon nonterminal | unchanged readiness/stable-merge assertion throws; fresh trace passes |
| `W6-NC-09` | label an intercepted browser API response as causal route evidence | unchanged request-chain/fidelity assertion throws; fresh trace passes |
| `W6-NC-10` | separately inject missing, duplicate, unexpected, skipped or filtered ID into synthetic sets | each unchanged set-equality assertion throws; fresh sets pass |
| `W6-NC-11` | remove one activation or change one control result to pass/pass/pass | unchanged activation/control assertion throws; fresh trace passes |
| `W6-NC-12` | broaden one substitute claim to live auth/AWS/provider/Lambda | unchanged fidelity assertion throws; fresh ledger passes |
| `W6-NC-13` | add a synthetic `.py`, SQLite, standalone dashboard, output-file or CDN member to discovered integrated dependencies | unchanged exclusion/scope assertion throws for each class; fresh inventory passes |

#### Substitute-fidelity ledger

| Boundary | Actual in W6 | May prove | Must not claim |
|---|---|---|---|
| Browser/frontend | production `next build` + `next start` + local Chrome CDP | emitted component, route-handler, client, navigation and UI behavior | deployed CDN/network/browser population |
| Authentication | installed Neon Auth server client against deterministic loopback `/get-session` | actual auth-client call and owner propagation/denial branches | live Neon Auth availability, cookie cryptography, external session security |
| Backend/database | actual backend server and Prisma repositories in one migrated isolated schema | strict API, SQL ownership/CAS/transactions, durable restart behavior | production database latency/permissions/transport |
| DataForSEO/Google | actual keyword adapter/parser via `runtime.http`; actual research validator and Google response parser via the existing injected validation dependency | keyword request shape, strict parsing, 19/100 call cardinality and causal downstream data | live provider pricing/quota/availability/transport, Google URL/request execution, or `awsProbeSearchPage` artifact-wrapper integration |
| S3/SQS | strict memory adapters calling actual service/message contracts | immutable-key conflict, schema validation, idempotent choreography and per-item identities | AWS IAM, encryption, transport, visibility, DLQ or Lambda event behavior |
| Lambda package | unchanged accepted W3/R4 build evidence | no W6 source invalidated the accepted worker package proof | new build, deployed execution or resource envelope measurement |

#### Frozen verification schedule

- [ ] `KI-W6-V1` After all five implementation files freeze, run file-local
  syntax/static manifest validation once: `node --check` for both new `.js/.mjs`
  harnesses and the existing browser harness, JSON strict parse, exact group/
  global digest recomputation, source-expression counts and exact five-path
  ownership. This gate performs zero database/build/browser/network/provider/AWS
  work. Evidence: ___
- [ ] `KI-W6-V2` From `frontend/`, run `npm run check` once. This is the sole
  production Next build. Preserve its `.next` output for V3; any edit to frontend
  source/config/package or either browser file invalidates V2, while backend
  helper/manifest-only edits do not. Evidence: ___
- [ ] `KI-W6-V3` With `ALLOW_DATABASE_TESTS=true`, the validated isolated test
  URLs and `KI_W6_SKIP_BUILD=1`, run
  `node test/browser/keyword-intelligence-e2e.mjs` once outside the sandbox when
  loopback/network permissions require it. Require 26/26, zero skips/duplicates/
  unexpected/unactivated, 13/13 falsifications, exact digests/counts, one schema
  created and absent after `finally`, and one privacy-safe certificate. Any edit
  to any five owned implementation files invalidates V3. A proven environment/
  channel invalidation follows the standing identical-recovery rule. Evidence: ___
- [ ] `KI-W6-V4` From `email_scraper/`, run `npm test` once and
  `npm run check:secrets` once after V3. Require zero failures and the guarded
  database suites to remain skipped without opt-in. Only a backend production/
  test/fixture/package change invalidates `npm test`; any owned-file change
  invalidates the secret scan. Evidence: ___
- [ ] `KI-W6-V5` Window agent independently recomputes the 26-ID/group/global
  certificate, five-path set/digest, starting→ending hashes, substitute-claim
  ceiling, exact operation counts and obsolete-runtime inventory from actual
  artifacts/traces; no command is rerun for this read-only assessment. Evidence: ___
- [ ] `KI-W6-V6` Prove by exact dependency hashes that accepted W3/R4 worker
  packaging, all R5 cases except the explicitly superseded R5-FIN-01 destination
  assertion, and downstream non-W6 source remain unchanged. No handler build,
  full W5 browser suite, full database integration, Prisma generate/validate or
  duplicate frontend build is permitted. Evidence: ___

- [ ] `KI-W6-H1` Record the fresh S1/S2/S3 revisions, every leaf assignment/
  review, five starting/ending file hashes, actual diff and generated/temp
  cleanup; identify the R5-FIN-01 supersession. Evidence: ___
- [ ] `KI-W6-H2` Record exact V1–V6 commands/outcomes, 26 required/registered/
  executed/activated IDs, zero exceptional sets, four group/global digests,
  13 control outcomes, operation counts, schema name/absence, skips, resource
  observations and any invalidated/recovered attempt. Evidence: ___
- [ ] `KI-W6-H3` Window agent appends `WINDOW-AGENT-INTEGRATION-PASS`, proves the
  final diff is exactly a subset of the five paths and personally reviews the
  causal chain/substitute limits; it stops `READY_FOR_PARENT_REVIEW` and does not
  edit A5/A6/A7/A8 or contact the parent through a leaf. Evidence: ___
- [ ] `KI-W6-H4` Record zero provider, AWS, production database, standalone-
  project, schema/migration/package, destructive, commit/push or KI-W7 action;
  cost is `$0.00`. Evidence: ___
- [ ] `KI-W6-H5` Parent independently reviews the window-agent certificate and
  actual source/diff. Only the parent may append A6/A7, CAS A5 to
  `AWAITING_REVIEW` or acceptance, and reserve/assign KI-W7. Evidence: ___
- [ ] `KI-W6-H6` Stop after KI-W6. Passing local evidence does not authorize
  infrastructure source, AWS mutation, provider call or KI-W7. Evidence: ___

#### `KI-W6` in-flight corrective amendment — final result shortlist projection

This `KI-CL-21` amendment supersedes only the affected `KI-W6` scope,
calculation, verification, packaging-reuse, and handoff statements above. The
five accepted initial files remain accepted history. The current W6 parent
scope is their exact set plus these two paths:

- `email_scraper/src/aws-pipeline/keyword-intelligence/service.js`
- `email_scraper/test/keyword-intelligence-worker-flow.test.js`

The complete seven-path sorted-member-plus-LF digest is
`c3bfe436aba49d52de26298ac74eb30e061d392144dfffbb6954ee792c908bdc`.
The two added starting SHA-256 values are respectively
`c37a038f189470ad1d2eca6626f515b9f0c45bd60de470d84c4b72fa497637b5`
and `f0e8be1a29d9ed5d85a657b8e73083f6c603ca30b18121701b3a33a7c1938510`.
The window agent must append two sequential single-file corrections,
`KI-W6-C104` then `KI-W6-C105`, and a zero-implementation-write reassessment
`KI-W6-I102`; it must return that decomposition for parent review before either
leaf is assigned. `KI-W6-C101`–`C103` remain used history and are not reused.

```yaml
window_id: KI-W6
correction_id: KI-W6-PCA-01
trigger: SRC-KI-041
governing_decision: DEC-KI-039
assigned_agent_policy: one_window_recursive
authorized_write_scope: [frontend/components/keyword-intelligence/research-dashboard.tsx, frontend/test/browser/keyword-intelligence-dashboard.mjs, email_scraper/test/helpers/keyword-intelligence-e2e-harness.js, email_scraper/test/fixtures/keyword-intelligence/ki-w6-enforcement-manifest-v1.json, frontend/test/browser/keyword-intelligence-e2e.mjs, email_scraper/src/aws-pipeline/keyword-intelligence/service.js aggregateMarket only, email_scraper/test/keyword-intelligence-worker-flow.test.js aggregationScaffold and additive SCN-KI-041 symbols only]
shared_file_scope: [service.js aggregateMarket only; worker-flow.test.js aggregationScaffold and additive SCN-KI-041 only; all unrelated symbols and accepted assertions remain byte/semantically preserved]
read_only_scope: [KEYWORD_INTELLIGENCE_PRODUCT_CONTRACT.md, KEYWORD_INTELLIGENCE_DISCOVERY_DOSSIER.md, KEYWORD_INTELLIGENCE_DECISION_LEDGER.md, KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md, ACTIVE_EXECUTION_STATE.md, KEYWORD_INTELLIGENCE_EXECUTION_EVIDENCE.md, KEYWORD_INTELLIGENCE_SPECIFICATION_CHANGELOG.md, KEYWORD_INTELLIGENCE_TRACEABILITY_INDEX.md, KEYWORD_INTELLIGENCE_KI_W6_REAUTHORED_SUBWINDOW_CHECKLIST.md, KEYWORD_INTELLIGENCE_KI_W6_REAUTHORED_SUBWINDOW_STATE.md, KEYWORD_INTELLIGENCE_KI_W6_REAUTHORED_SUBWINDOW_EVIDENCE.md, email_scraper/src/keyword-intelligence/pipeline.js, email_scraper/src/keyword-intelligence/config.js, email_scraper/src/aws-pipeline/keyword-intelligence/contracts.js, email_scraper/src/aws-pipeline/keyword-intelligence/keys.js, email_scraper/src/aws-pipeline/keyword-intelligence/handler.js, email_scraper/src/aws-pipeline/keyword-intelligence/recovery.js, email_scraper/src/keyword-intelligence/repository.js, email_scraper/test/aws-pipeline-packaging.test.js, email_scraper/scripts/build-keyword-worker.js, email_scraper/package.json, frontend/package.json]
authorized_actions: [window-agent S1/S2/S3 correction authoring, parent-reviewed sequential single-file leaf delegation, local static and focused component diagnostics, one corrected frozen V3 isolated-schema emitted-browser run, one backend npm test, one secret scan, exactly two keyword-worker builds, one unchanged packaging test, read-only dependency and coverage recomputation, consolidated parent handoff]
prohibited_actions: [window-agent implementation-file edits, leaf multi-file edits, parallel or out-of-order leaves, direct parent-leaf communication, leaf subdelegation, new or changed coverage IDs, manifest or frontend edits, schema migration package lock config handler recovery adapter repository pipeline or build-script edits, full opted-in database suite, Prisma generation or validation, seven-handler build or measure, provider calls, AWS operations, production database writes, destructive shared cleanup, commits or pushes, KI-W7 work]
successor: STOP_LOCAL
successor_reserved_for: parent
may_start_successor: false
```

##### Task block `KI-W6-CT1` — project final calculation from the durable shortlist

1. **Task:** correct only `aggregateMarket` so the final nine-market
   calculation uses the fingerprint-validated durable shortlist as its exact
   keyword universe.
2. **Requirements/decisions:** `REQ-KI-002/003/023/024`, `INV-KI-004/005/014`,
   `DEC-KI-006/024/038/039`.
3. **Source:** `SRC-KI-041`; current `aggregateMarket` reads the 300-row anchor
   artifact and expansion manifest but never reads the anchor shortlist
   manifest, then sends those unfiltered inputs to `computeResearchResult`.
4. **Target:** only
   `email_scraper/src/aws-pipeline/keyword-intelligence/service.js::aggregateMarket`;
   no export, signature, caller, handler, contract, key, or repository change.
5. **Interface/schema:** read `anchor_screen` through existing `readManifest`
   using `KEYWORD_ARTIFACT_SHORTLIST_MANIFEST` and
   `keywordShortlistManifestSchema`. Define the exact comparison key as
   `keyword.trim().toLowerCase()`. Public and artifact schemas remain unchanged.
6. **Algorithm:** after the existing validated expansion-manifest read and
   before `computeResearchResult`: (a) read the validated anchor shortlist;
   (b) build its ordered keyword array and distinct normalized-key set `K`;
   (c) map every `expansionManifest.bySeed` member to the same seed with its
   keywords filtered in original order to keys in `K`, retaining shared
   keywords under every original seed; (d) filter the US anchor metrics in
   original order to `K`; (e) compute the distinct normalized keys represented
   by each filtered input and call the existing invariant failure if either set
   is not exactly `K`; (f) call `computeResearchResult` with only that filtered
   expansion, filtered `US` metrics, and the unchanged eight market arrays.
7. **Operations:** existing aggregation claim/lease → validated anchor task
   read → eight validated market-task reads → validated expansion-manifest
   read → one validated shortlist-manifest read → in-memory projection →
   existing calculation → existing immutable market/result puts → existing
   fenced publication. No network/provider work occurs in aggregation.
8. **Atomicity/recovery:** the added read is inside the existing monitored
   aggregation boundary; publication and selection retain the existing final
   fenced transaction. A failure before publication leaves result/selection
   invisible and is recovered from the same immutable manifests.
9. **Identity/formulas:** use only the existing stage identity, generation,
   `keywordStageInputFingerprint`, manifest content fingerprint, and produced
   timestamp validation performed by `readManifest`; normalized membership is
   exactly `trim().toLowerCase()` and does not create a new durable identity.
10. **Failure/replay/concurrency:** missing/corrupt/mismatched shortlist or set
    inequality fails closed before any result put/publication. Duplicate,
    reordered, restarted, expired, or stale-owner aggregate checks retain the
    existing monitor/fence outcomes. Exact replay recomputes the identical
    result and fingerprint.
11. **Dependencies/bounds:** shortlist length `1..200`; anchor metrics `1..300`;
    final expansion/US universe exactly shortlist length; result rows exactly
    shortlist length and at most `200`; selection at most `100`; one added S3
    read; zero added provider calls, sends, attempts, writes, reservations, or
    database operations.
12. **Callers/obsolete behavior:** only market aggregation consumes the new
    projection. Remove the obsolete direct use of all expansion candidates and
    all US anchor metrics as the final calculation universe. Preserve the
    300-keyword anchor screen, 200-keyword market requests, full immutable
    anchor artifact, provider cost, ordering, provenance, and result schema.
13. **Tests/cases/controls:** `KI-W6-CT2` supplies the focused component
    regression. Existing sole W6 registration `W6-FLOW-05` must observe
    300 screened, 200 shortlisted, exactly 200 published and default 100;
    existing `W6-NC-05` must still falsify the unchanged durable-visibility
    oracle after a 201st/300th leaked row. No new W6 case/control ID or second
    registration is permitted.
14. **Output:** corrected production service consumed by `KI-W6-CT2`, V3, the
    keyword-worker build, and later W7 packaging.
15. **Non-goals:** no result post-truncation, rank change, shortlist-limit
    change, candidate pre-cap, seed-lineage collapse, artifact mutation,
    provider/API/frontend/schema/config/repository/handler/recovery/build edit,
    or live action.

- [ ] `KI-W6-CT1` Implement the exact `aggregateMarket` projection above in
  one `KI-W6-C104` leaf. Evidence: ___

##### Task block `KI-W6-CT2` — focused aggregation regression and substitute fidelity

1. **Task:** update only the existing non-database aggregation scaffold and add
   one focused regression proving a 300-candidate anchor plus durable
   200-keyword shortlist publishes exactly those 200 result rows.
2. **Requirements/decisions:** same as `KI-W6-CT1`; `SCN-KI-041`;
   `W6-FLOW-04/05/06`; `W6-NC-05`.
3. **Source:**
   `email_scraper/test/keyword-intelligence-worker-flow.test.js::aggregationScaffold`
   currently supplies no anchor shortlist manifest because the old production
   aggregator did not read one, and its three-candidate fixture cannot expose
   300→200 leakage.
4. **Target:** only that file's `aggregationScaffold` support symbols and one
   additive `SCN-KI-041` test; all R3/R4 registrations and assertions remain.
5. **Interface/schema:** extend the private scaffold options with exact
   `candidates` and `shortlist` arrays defaulting to the existing
   `AGG_CANDIDATES`; expose the exact `publishResearchResult` input through the
   returned private holder. No production or exported test interface changes.
6. **Algorithm:** use `candidates` for expansion manifest, anchor request, and
   anchor metrics; use `shortlist` for all eight market task request
   fingerprints and market metrics; create and store a strict
   `keyword-shortlist-manifest-v1` at the anchor manifest key with the existing
   anchor-stage input fingerprint/produced time, and assign its key,
   fingerprint, and produced time to the anchor stage; capture the final
   publication input without changing its return outcome.
7. **Operations:** all storage remains the existing in-memory strict
   `S3ArtifactStore`; no database, subprocess, HTTP, provider, AWS, or workspace
   artifact write is added by the test.
8. **Atomicity/recovery:** the scaffold continues to exercise the production
   aggregate message and repository publication seam; it makes no atomicity
   claim beyond the existing component parity ledger.
9. **Identity/formulas:** for `SCN-KI-041`, define candidates exactly as
   `Array.from({length:300},(_,index)=>` followed by the template literal
   `` `seed one candidate ${String(index + 1).padStart(3, "0")}` `` and `)`;
   define the durable shortlist as `candidates.slice(0, 200)` in original
   order, and compare normalized `trim().toLowerCase()` sets. Existing artifact
   keys/fingerprints remain the production formulas.
10. **Failure/replay/concurrency:** preserve every existing R3/R4 lease,
    lost-owner, terminal/found/conflict/not-found, and no-dispatch assertion.
    The new regression is a normal terminal market aggregation only; V3 retains
    restart/duplicate/fence proof.
11. **Dependencies/bounds:** exact input/output counts are 300/200/200/100;
    component execution is non-database and performs zero external calls.
12. **Callers/obsolete behavior:** existing scaffold callers receive byte-
    equivalent three-item defaults and continue to pass. The obsolete missing-
    shortlist substitute is removed because production now consumes that
    artifact.
13. **Tests/cases/controls:** the additive test must assert outcome
    `published`, captured final result length exactly `200`, normalized result
    keys exactly equal the durable shortlist keys, zero result key outside the
    shortlist, and default selection length exactly `100`. It is supplemental
    and must not register/activate `W6-FLOW-05`; the sole causal registration
    stays in S105. Existing `W6-NC-05` remains the enforcement control.
14. **Output:** component regression/fidelity evidence consumed by the
    corrected W6 assessment and backend regression.
15. **Non-goals:** no existing case-ID membership/digest change, no accepted
    R3/R4 oracle weakening, no DB fixture, timeout increase, retry, frontend,
    manifest, package, production, or second-file edit.

- [ ] `KI-W6-CT2` Implement the exact scaffold/regression update above in one
  `KI-W6-C105` leaf after C104 is accepted. Evidence: ___

##### Scenario `SCN-KI-041` — final result cannot escape the shortlist

```yaml
scenario_id: SCN-KI-041
requirements: [REQ-KI-002, REQ-KI-003, REQ-KI-023, REQ-KI-024]
decisions: [DEC-KI-024, DEC-KI-038, DEC-KI-039]
preconditions: market stage ready under a live aggregation token; immutable expansion manifest has 300 unique candidates; immutable anchor result has all 300 US metrics; immutable anchor shortlist has the first 200; eight market artifacts contain those same 200
inputs: strict in-memory artifact schemas and actual processKeywordMessage aggregate path
actions: process one market aggregate check; capture the publishResearchResult input; then rely on the existing W6-NC-05 mutation during V3
activation_witnesses: validated shortlist-manifest get occurs; computeResearchResult output reaches publishResearchResult; causal V3 later observes the fenced durable result
oracle: component result keys equal the 200 shortlist keys and exclude all other anchor keys; causal V3 observes rowCount 200 and defaultSelectionItemCount 100
call_and_operation_counts: one extra shortlist get; zero extra provider calls queue sends attempts writes reservations or database operations; existing maximum totals remain 19 calls 23 keyword objects 42 base sends and 0.49200000 USD
negative_control: W6-NC-05 mutates captured durable visibility with an escaped row and the unchanged oracle fails, then a fresh witness passes
parity_class: component plus existing local_e2e W6-FLOW-05
cleanup: component memory is discarded; V3 uses its existing schema/temp cleanup and absence witness
```

##### Corrected frozen assessment schedule

- [ ] `KI-W6-CV1` After C104/C105 acceptance, run once from `email_scraper/`:
  `node --check src/aws-pipeline/keyword-intelligence/service.js` and
  `node --test --test-isolation=none test/keyword-intelligence-worker-flow.test.js`.
  Require zero failures, `SCN-KI-041` activation and the exact
  300/200/200/100 assertions; existing R3/R4 cases remain green. Evidence: ___
- [ ] `KI-W6-CV2` Reuse the already-passing frontend `npm run check` only after
  `git -C frontend status --porcelain` is empty and
  `git -C frontend rev-parse HEAD` equals
  `a39663c8f99d9cc3c4aa1301ff088d5f4a24e7fd`, the committed tree containing
  the passed V2 inputs. Do not rebuild Next for backend-only C104/C105.
  Evidence: ___
- [ ] `KI-W6-CV3` Run the corrected V3 emitted-browser/isolated-schema command
  once with the standing sandbox policy. Require the unchanged 26-case/13-
  control certificate, exact 19/23/42/`$0.49200000` topology, 300 anchor,
  200 shortlist, 200 durable/UI rows, default 100, complete cleanup and zero
  residual schema. Earlier failed V3 attempts remain diagnostic and are not
  acceptance. Evidence: ___
- [ ] `KI-W6-CV4` From `email_scraper/`, run `npm test` once and
  `npm run check:secrets` once after the final backend freeze; require zero
  failures and a clean secret scan. Do not run the full opted-in DB suite.
  Evidence: ___
- [ ] `KI-W6-CV5` From `email_scraper/`, run
  `node scripts/build-keyword-worker.js` exactly twice. Require byte-identical
  keyword ZIP hashes, preserved sibling artifacts, no forbidden/stale members,
  ZIP at most 45 MiB, unzipped at most 200 MiB, and cold import exporting a
  function `handler`; then run
  `node --test --test-isolation=none test/aws-pipeline-packaging.test.js` once
  with zero failures. Do not run the seven-handler build or measure scripts.
  Evidence: ___
- [ ] `KI-W6-CV6` Recompute the seven-path scope digest, current file hashes,
  exact 26-ID/group/global equality, 13 controls, substitute limits, privacy,
  and W7 package/resource handoff. Require all non-C104/C105 accepted W6 files
  byte-identical to these accepted SHA-256 values: research dashboard
  `68a7ec84d77a955122dfb9ca1767ab1a52c2a2f2125db5c34581e5e9af8f5984`,
  dashboard browser test
  `17ae402882f64fd8da6aba61161343f119aa1b7a62edbed0cbf97d9bbe0896b7`,
  backend E2E helper
  `7571818027b54bc812d4395d0eb1eec65616b1b939c90baae27fefdb619867c6`,
  W6 manifest
  `ea3a5471e33f5dcc656a6b522e8d379f596caad158c0bd3ff2315e93d145e475`,
  and causal browser test
  `fc88c77ebb1bf8f62cafa600afbe5d789cd7a688899a552cff93a0ec0ada0a8f`;
  require no out-of-scope source change.
  Evidence: ___

Only CV1, CV3, CV4, CV5, and CV6 are invalidated by C104/C105. The previously
passing frontend build is not invalidated unless its complete inputs change.
An edit after any corrected gate reruns only that gate and its dependent gates;
sandbox/channel invalidation follows the standing identical-recovery rule.

- [ ] `KI-W6-CH1` Window agent records accepted C104/C105, the personally
  executed `KI-W6-I102`, exact seven-file final set/digest, corrected gates,
  reused frontend-build dependency proof, superseded failed V3 attempts, and
  a complete `WINDOW-AGENT-INTEGRATION-PASS`. Evidence: ___
- [ ] `KI-W6-CH2` Window agent stops `READY_FOR_PARENT_REVIEW`; no KI-W7,
  provider, AWS, production, destructive, commit, push, A1–A8, schema,
  migration, package, or frontend action occurs. Evidence: ___

### `KI-W7` — Infrastructure source only

```yaml
window_id: KI-W7
objective: Add deployable SAM source for one dedicated function, queue, DLQ, recovery schedule, permissions, alarms, and outputs without mutating AWS.
depends_on: [KI-W6, explicit_infrastructure_source_approval]
consumes: accepted emitted worker artifact and measured resource envelope
produces: validated infrastructure source/package inventory
assigned_agent_policy: one_window
authorized_write_scope: email_scraper/infrastructure/aws/template.yaml keyword resource logical IDs only; email_scraper/scripts/build-aws-handlers.js keyword handler entry only; email_scraper/src/config.js AWS_PIPELINE_KEYWORD_RESEARCH_QUEUE_URL mapping only; email_scraper/src/aws-pipeline/runtime-config.js awsPipelineKeywordResearchQueueUrl validation/projection only; email_scraper/test/aws-pipeline-runtime-adapters.test.js keyword queue config describe block only; email_scraper/test/keyword-intelligence-infrastructure.test.js; email_scraper/test/keyword-intelligence-build.test.js
shared_file_scope: template/build/config/runtime-config symbols are additive and limited to the one keyword queue; existing runtime configuration and resources remain unchanged
read_only_scope: all existing AWS resources/contracts; W6 measurements
authorized_actions: [local_source_edits, local_SAM_validation_if_installed, local_build, evidence_updates]
prohibited_actions: [AWS_mutation, AWS_deploy, secret_changes, provider_calls, frontend_or_schema_edits, existing_resource_topology_changes, commits]
successor: STOP_AWS_MUTATION_APPROVAL
successor_reserved_for: parent
may_start_successor: false
```

- [ ] `KI-W7-P1` Assignment/hashes/version and explicit source-edit approval match. Evidence: ___
- [ ] `KI-W7-P2` W6 accepted artifact/resource measurements exist. Evidence: ___
- [ ] `KI-W7-P3` Local SAM/build tools available or exact skip recorded; no AWS credential required. Evidence: ___
- [ ] `KI-W7-P4` Shared template/build symbols and dirty state recorded. Evidence: ___

#### Task block `KI-W7-T1`

1. **Task:** add exactly one standard SQS queue, one DLQ/redrive policy, one Node
   Lambda, batch-size-one event mapping without MaximumConcurrency=1, one
   recovery schedule, least-privilege IAM, log/alarm/output entries, and build
   inclusion.
2. **Requirements/decisions:** `INV-KI-001`–`007`, `012`, `AUTH-KI-005`,
   `DEC-KI-001`, `022`, `024`, `025`.
3. **Source:** existing SAM/build patterns `SRC-KI-016`; W6 emitted closure.
4. **Target:** exact shared symbols/owned tests in header, including only the
   `AWS_PIPELINE_KEYWORD_RESEARCH_QUEUE_URL` →
   `awsPipelineKeywordResearchQueueUrl` configuration seam locked by
   `DEC-KI-027`.
5. **Interface/schema:** handler `handler`; environment only existing secret/DB/
   bucket plus `AWS_PIPELINE_KEYWORD_RESEARCH_QUEUE_URL` and config version;
   runtime exposes that value only as `awsPipelineKeywordResearchQueueUrl`;
   outputs expose function/queue/DLQ
   names/ARNs without secret values.
6. **Algorithm:** additive resources/wiring; event mapping batch size 1 and
   function response types `ReportBatchItemFailures`; function reserved
   concurrency 1, timeout 180 seconds, memory 1024 MiB, ephemeral storage
   512 MiB; source queue visibility 360 seconds/retention 4 days, DLQ retention
   14 days, redrive maxReceiveCount 5; recovery schedule `rate(1 minute)` invokes
   the recovery discriminator.
7. **Operations:** template/build/validate only; no cloud command.
8. **Atomicity:** deployment atomicity deferred to approved stack action; runtime
   remains Neon-fenced.
9. **Identities:** deterministic SAM logical IDs; no production physical names
   guessed; S3 prefix/queue contract from decisions.
10. **Failure/replay:** DLQ/redrive/alarms declared; mapping disabled/enabled
    default follows existing safe deployment convention; no mutation now.
11. **Dependencies/bounds:** accepted artifact must fit existing Lambda package
    limits; no MaximumConcurrency setting; batch1; reserved1; timeout180;
    memory1024; ephemeral512; visibility360; 32MiB S3 artifact never enters SQS.
12. **Callers/obsolete:** add handler to build inventory; do not change existing
    discovery/lead/traffic resources.
13. **Tests:** template parse/assert all exact resources/properties/IAM/env;
    runtime config accepts one HTTPS queue URL, rejects missing/non-HTTPS with
    `KEYWORD_RUNTIME_CONFIG_INVALID`, and exposes the exact camel-case property;
    emitted inventory contains handler/dependencies once; startup mock invoke;
    negative control adds forbidden Step Functions/Fargate/MaxConcurrency1 and
    topology test fails.
14. **Output:** deployable source for separately approved W8.
15. **Non-goals:** AWS create/update, secrets, mapping enablement, provider call.

- [ ] `KI-W7-T1` Perform the fully specified infrastructure-source change above.

- [ ] `KI-W7-V1` Execute infrastructure topology/build/startup scenarios and negative controls.
- [ ] `KI-W7-V2` Run SAM validation if installed, handler build/inventory/size, backend regression/security tests.
- [ ] `KI-W7-V3` Assert measured timeout/memory/package/visibility/concurrency settings cover W6 bounds and do not mask growth.
- [ ] `KI-W7-V4` Assert no credential/value, broad IAM, existing topology change, or AWS mutation.
- [ ] `KI-W7-H1` Record files/symbols. Evidence: ___
- [ ] `KI-W7-H2` Record commands/outcomes/skips. Evidence: ___
- [ ] `KI-W7-H3` Diff matches additive scope. Evidence: ___
- [ ] `KI-W7-H4` No W8/live action. Evidence: ___
- [ ] `KI-W7-H5` Append evidence; A5 `AWAITING_REVIEW` by CAS. Evidence: ___
- [ ] `KI-W7-H6` Stop for exact AWS mutation/provider approval.

### `KI-W8` — Approved deployment and live canary

```yaml
window_id: KI-W8
objective: Read-only preflight, then only explicitly approved resource/secret/mapping/provider actions, followed by one bounded production-format canary.
depends_on: [KI-W7, explicit_action_by_action_approvals]
consumes: accepted template/artifacts; exact account/region/resource targets supplied or discovered read-only
produces: applied capability evidence, deployed resources, sanitized nonempty canary evidence, rollback/disable state
assigned_agent_policy: one_window
authorized_write_scope: KEYWORD_INTELLIGENCE_EXECUTION_EVIDENCE.md and ACTIVE_EXECUTION_STATE.md only; deployed targets exactly named in approval
shared_file_scope: A5/A6 versioned append/status only
read_only_scope: deployed stack/log/metric/config descriptions and owner-scoped canary result
authorized_actions: [approved_read_only_AWS_preflight, individually_approved_stack_mutation, individually_approved_secret_reference, individually_approved_event_mapping_enablement, one_approved_paid_canary, evidence_updates]
prohibited_actions: [unapproved_mutation, queue_receive_or_purge, DLQ_redrive, broad_S3_access, production_data_deletion, arbitrary_provider_calls, source_edits, commits]
successor: STOP_FINAL_INDEPENDENT_REVIEW
successor_reserved_for: parent
may_start_successor: false
```

- [ ] `KI-W8-P1` Assignment/hashes/version and exact approvals/resources/actions match. Evidence: ___
- [ ] `KI-W8-P2` W7 accepted artifact/template hashes exist. Evidence: ___
- [ ] `KI-W8-P3` Read-only applied quotas, region, permissions, DB transport, bucket/queue limits, and provider capability satisfy locked bounds. Evidence: ___
- [ ] `KI-W8-P4` Starting deployed state and exact mutation targets recorded without secrets. Evidence: ___

#### Task block `KI-W8-T1`

1. **Task:** execute only approved preflight/mutations, then one 1-seed
   production-format canary whose sanitized result reaches dashboard and run
   handoff; disable/rollback only by its preapproved branch.
2. **Requirements/decisions:** `AUTH-KI-005`, `INV-KI-001`–`015`,
   `DEC-KI-025`.
3. **Source:** accepted W7 artifacts and exact approved AWS/account/provider
   evidence; no published default substitutes.
4. **Target:** exact approved stack resources and evidence/state files only.
5. **Interface/schema:** deployed units must hash-match accepted artifacts;
   canary uses normal strict API/messages/artifacts, no admin shortcut.
6. **Algorithm:** read-only capability/config preflight → compare every applied
   value → stop if mismatch → disclose/execute each approved mutation → verify
   disabled state → approved secret reference → enable mapping → one seed canary
   → verify durable terminal/UI/handoff → observe alarms/DLQ → stop.
7. **Operations:** exact AWS/provider commands are recorded before execution;
   one canary may incur exactly two US expansion tasks, one US anchor-screen
   task, and eight remaining-market tasks when the shortlist is nonempty: 11
   first-pass logical calls and at most 55 attempts under the locked known retry
   rules. Its reservation is computed from actual candidate/shortlist lengths
   under `DEC-KI-009` and can never exceed the `$3.00` hard cap.
8. **Atomicity:** CloudFormation stack action plus runtime Neon/S3 recovered
   boundaries; failed deploy follows approved stack rollback, never manual purge.
9. **Identities:** exact account/region/stack/research/generation/artifact hashes
   recorded sanitized; no learning resource reused as production contract.
10. **Failure/replay:** any capability/permission/contract/ambiguity failure stops;
    no second paid canary; disable mapping only if preapproved; no queue purge.
11. **Dependencies/bounds:** applied values must meet W6/W7 measurements; one
    seed; reserved1/batch1; alarm/log/privacy policies.
12. **Callers/obsolete:** actual API→queue→Lambda path only; no local direct
    invocation as canary proof.
13. **Tests:** `SCN-KI-019`; activation witnesses: real API, SQS receive by
    mapping, each worker stage, Neon rows, S3 artifacts, completed owner UI and
    run snapshot; exact counts/cost; negative control is disabled mapping before
    enable and must leave queued/not completed without hidden processor.
14. **Output:** live evidence for independent final review only.
15. **Non-goals:** broad rollout, load test, second canary, purges/redrive,
    final completion declaration.

- [ ] `KI-W8-T1` Perform only the specifically approved deployment/canary actions above.

- [ ] `KI-W8-V1` Execute `SCN-KI-019` with real nonempty activation and negative control.
- [ ] `KI-W8-V2` Verify deployed hashes/config/IAM/event mapping/logs/alarms and exact durable/public state.
- [ ] `KI-W8-V3` Record actual calls/cost/duration/memory/artifact/message sizes against bounds.
- [ ] `KI-W8-V4` Confirm privacy, owner isolation, no DLQ/hidden retry, and no unapproved mutation.
- [ ] `KI-W8-H1` Record exact external mutations/resources and reversibility. Evidence: ___
- [ ] `KI-W8-H2` Record commands/outcomes/cost/skips sanitized. Evidence: ___
- [ ] `KI-W8-H3` Source/evidence diff and deployed hashes match scope. Evidence: ___
- [ ] `KI-W8-H4` No final-review work or extra canary. Evidence: ___
- [ ] `KI-W8-H5` Append evidence; A5 `AWAITING_REVIEW` by CAS. Evidence: ___
- [ ] `KI-W8-H6` Stop for independent parent final review.

## 3. Scenario ledger

Dimensions derive from D1–D13. Payload/input boundaries are exhaustive; each
external/durable failure boundary is exhaustive; owner/lease/revision schedules
are pairwise plus named adversarial cases; scale uses minimum, representative,
and hard maximum; runtime parity advances unit → component → integration →
local E2E → emitted artifact → approved canary. Cross-products not listed are
excluded only when the relevant functions are pure and their partitions do not
share state; stateful/external dimensions are never excluded on that basis.

Each scenario cleanup is limited to its disposable schema, mock state, spawned
local process, and `mktemp` artifacts in `finally`; live cleanup follows only an
explicit W8 approval.

### `SCN-KI-001` — Nonempty durable research

- **Requirements:** `REQ-KI-002`–`005`, `023`, `024`.
- **Decisions:** `DEC-KI-005`, `006`, `018`.
- **Preconditions:** owner A; queued generation-one research; fresh cache.
- **Inputs:** one valid seed and evidence-backed nonempty fixtures for all nine markets.
- **Actions:** initialize; process two US expansion tasks/check; process the US
  anchor screen/check; process eight remaining-market tasks/check; calculate;
  publish final result.
- **Activation witnesses:** every message discriminator, provider seam, S3 put,
  first-terminal counter, and final Neon transaction is reached.
- **Oracle:** completed fingerprint validates; revision one/default selection is
  durable; API exposes no partial result or raw field.
- **Call and operation counts:** exactly two expansion tasks, one anchor-screen
  task, and eight remaining-market tasks (11 first-pass tasks); one terminal
  transition per task.
- **Negative control:** bypass the anchor-screen worker or one remaining-market
  worker; completion remains false.
- **Parity class:** `integration`.
- **Cleanup:** drop only the disposable schema and clear created mock/S3/SQS state in `finally`.

### `SCN-KI-002` — Schema, identity, and migration

- **Requirements:** `INV-KI-001`.
- **Decisions:** `DEC-KI-002`, `021`.
- **Preconditions:** current migrations applied to one disposable non-public schema.
- **Inputs:** one legacy Run and two owners/researches with the same normalized seed.
- **Actions:** migrate; insert every model; exercise every unique; traverse
  relations; create and read the legacy row.
- **Activation witnesses:** migration SQL, Prisma client, every new table/FK,
  and owner-scoped repository read execute.
- **Oracle:** exact catalog/default/index/FK set; distinct research IDs; shared
  cache fingerprint allowed; owners remain isolated; public schema untouched.
- **Call and operation counts:** one forward migration; one collision assertion
  per declared unique; no production database call.
- **Negative control:** omit one unique/index from a test schema; catalog assertion fails.
- **Parity class:** `integration`.
- **Cleanup:** drop only the disposable schema in `finally`.

### `SCN-KI-003` — Seed/API partitions

- **Requirements:** `REQ-KI-001`.
- **Decisions:** `DEC-KI-003`, `019`.
- **Preconditions:** authenticated owner A and unauthenticated request contexts.
- **Inputs:** 0/1/5/6 seeds; 0/100/101 code points; whitespace, NFKC/case
  duplicate, control-character, and extra-key cases.
- **Actions:** call the actual POST parser/route, repository, and mock dispatcher.
- **Activation witnesses:** auth guard, strict body parser, normalization,
  transaction commit, and post-commit dispatch seam execute.
- **Oracle:** only valid normalized 1–5 persists; invalid/auth cases return exact
  400/401; no provider call occurs.
- **Call and operation counts:** one identity message after a successful commit;
  zero messages for rejected inputs.
- **Negative control:** accept a normalized duplicate silently; the test fails.
- **Parity class:** `component`.
- **Cleanup:** remove only created test rows and mock messages in `finally`.

### `SCN-KI-004` — Strict expansion payloads

- **Requirements:** `REQ-KI-004`.
- **Decisions:** `DEC-KI-005`; `PAY-KI-003`, `PAY-KI-004`.
- **Preconditions:** strict adapter and normalized fixture harness loaded.
- **Inputs:** observed suggestions/related shapes plus missing, alias, null,
  malformed, extra, empty, and ordered-duplicate fixtures.
- **Actions:** parse raw fixture; normalize; merge by seed and endpoint.
- **Activation witnesses:** both endpoint-specific consumed paths and every
  strict rejection partition execute.
- **Oracle:** only observed paths are accepted; order/dedup/cap-60 are exact;
  one failed endpoint leaves the seed and other endpoint output.
- **Call and operation counts:** zero network calls; at most 60 retained rows per endpoint.
- **Negative control:** enable `items[].key` or direct related keyword; rejection test fails.
- **Parity class:** `component`.
- **Cleanup:** clear only in-memory fixtures and temporary output in `finally`.

### `SCN-KI-005` — Anchor screening and nine-market result

- **Requirements:** `REQ-KI-003`, `REQ-KI-004`, `REQ-KI-024`.
- **Decisions:** `DEC-KI-004`, `006`.
- **Preconditions:** deterministic manifest builder and exact nine-market config loaded.
- **Inputs:** ordered candidate counts 1, 199, 200, 201, and 300; anchor metrics
  include ties, missing values, nonpositive values, and more than 200 usable
  active rows.
- **Actions:** build the candidate manifest and one anchor task; parse US
  metrics; rank/truncate to 200; build eight remaining-market tasks; combine US
  plus their results and calculate the cumulative result.
- **Activation witnesses:** anchor parser/ranker, 200 boundary, every remaining
  market key, every parser, US-metric reuse, and cumulative calculator execute.
- **Oracle:** no candidate is removed before the US request; shortlist ordering,
  market keys, and config fingerprint are exact; unusable rows are excluded;
  final scoring reruns over all nine markets.
- **Call and operation counts:** one anchor task and, for every nonempty
  shortlist fixture, exactly eight remaining-market tasks; never a second US
  overview task and never an overview split at 200/300.
- **Negative control:** swap one market/language; fingerprint and oracle fail.
- **Parity class:** `component`.
- **Cleanup:** clear only created manifests and mock task state in `finally`.

### `SCN-KI-006` — Paid-call failure boundaries

- **Requirements:** `REQ-KI-022`, `INV-KI-007`, `INV-KI-008`.
- **Decisions:** `DEC-KI-007`, `009`.
- **Preconditions:** exact task/cache states and immutable `DEC-KI-009` cost-policy snapshot.
- **Inputs:** crashes before marker, after marker/before send, after parse, after
  cache, after artifact, after terminal, and after check; known retry and response-loss cases.
- **Actions:** inject each failure, redeliver the same identity, and run recovery.
- **Activation witnesses:** budget reservation, durable pre-call row, HTTP seam,
  cache, S3, Neon terminal, and check-send boundaries execute.
- **Oracle:** ambiguous never calls again; cache hit calls zero; durable order is
  preserved; every known response replaces reservation with reported actual
  cost (including known retryable/terminal failures); ambiguity retains
  reservation; over-budget work makes zero calls; one terminal counter results.
- **Call and operation counts:** no call before marker; at most five known
  retries with exact delays; at most one call per Lambda invocation; at maximum
  scale first-pass reservation is exactly `$0.492`, five-attempt reservation is
  exactly `$2.46`, and the next reservation is denied if its addition would
  exceed `$3.00`.
- **Negative control:** remove the marker or repeat an ambiguous call; call-count oracle fails.
- **Parity class:** `integration`.
- **Cleanup:** drop only the disposable schema and clear mock HTTP/S3/SQS state in `finally`.

### `SCN-KI-007` — Throttle and retry schedules

- **Requirements:** `INV-KI-012`.
- **Decisions:** `DEC-KI-007`, `008`.
- **Preconditions:** concurrent workers and controllable DB clock at each boundary.
- **Inputs:** attempts one through five and deterministic task/request fingerprints.
- **Actions:** race throttle claims; redeliver before and at `nextAllowedAt`; schedule each retry.
- **Activation witnesses:** atomic throttle update, delayed task state, dispatcher,
  and retry claim execute.
- **Oracle:** early delivery performs no attempt/call; delays are deterministic
  whole seconds; no sixth attempt exists.
- **Call and operation counts:** exactly one throttle claim per 2,000 ms globally.
- **Negative control:** replace DB throttle with process-local state; collision test fails.
- **Parity class:** `integration`.
- **Cleanup:** remove only created throttle/task rows and mock messages in `finally`.

### `SCN-KI-008` — Owner/revision/handoff races

- **Requirements:** `REQ-KI-007`, `REQ-KI-015`.
- **Decisions:** `DEC-KI-014`, `017`, `019`.
- **Preconditions:** owner A has completed revision r; owner B has no grant.
- **Inputs:** concurrent saves and same/different handoff fingerprints/client IDs.
- **Actions:** race selection saves and handoffs; read as both owners.
- **Activation witnesses:** owner predicate, revision CAS, handoff unique keys,
  and Run/snapshot/query transaction execute.
- **Oracle:** one CAS winner; stale is 409; owner B is 404; identical handoff
  returns one Run; conflict is 409; Run+snapshot+N queries are all-or-none.
- **Call and operation counts:** one successful revision increment and one Run per idempotency key.
- **Negative control:** remove owner or revision predicate; race/isolation test fails.
- **Parity class:** `integration`.
- **Cleanup:** drop only the disposable schema and clear mock dispatch state in `finally`.

### `SCN-KI-009` — Cache and visibility

- **Requirements:** `REQ-KI-005`, `REQ-KI-017`, `INV-KI-013`, `INV-KI-014`.
- **Decisions:** `DEC-KI-009`.
- **Preconditions:** owners A/B and running/completed research rows exist.
- **Inputs:** fresh, exact-expiry, stale, and corrupt cache rows.
- **Actions:** perform worker lookups and owner API reads across the DB clock boundary.
- **Activation witnesses:** cache fingerprint/TTL parser, owner filter, running
  serializer, and completed serializer execute.
- **Oracle:** fresh hits; exact expiry misses; corruption fails; cache grants no
  owner access; running omits result; completed returns exact result.
- **Call and operation counts:** fresh hit makes zero provider calls; stale/expiry permits one planned attempt.
- **Negative control:** treat cache existence as access evidence; owner test fails.
- **Parity class:** `integration`.
- **Cleanup:** drop only the disposable schema and clear mock provider state in `finally`.

### `SCN-KI-010` — Python/Node parity

- **Requirements:** `REQ-KI-004`.
- **Decisions:** `DEC-KI-010`–`012`.
- **Preconditions:** development Python oracle and Node pure modules are available.
- **Inputs:** sanitized normalized fixtures covering every intent, alias, tie,
  cluster, market, missing metric, history, and seasonality partition.
- **Actions:** invoke each Python oracle and Node counterpart; run the full pure pipeline/export.
- **Activation witnesses:** every formula family, ranking branch, ID builder,
  and CSV serializer executes in both implementations.
- **Oracle:** public outputs are exact; intermediate numbers differ by at most
  1e-12; CSV bytes match; production build contains no Python.
- **Call and operation counts:** one paired oracle invocation per fixture/function family; zero provider calls.
- **Negative control:** perturb each formula family separately; its golden assertion fails.
- **Parity class:** `emitted_artifact`.
- **Cleanup:** remove only temporary oracle/export files in `finally`.

### `SCN-KI-011` — Selection/conflict boundaries

- **Requirements:** `REQ-KI-006`–`009`.
- **Decisions:** `DEC-KI-013`–`015`.
- **Preconditions:** completed research and revision-matched selection draft.
- **Inputs:** recommended counts 0/1/100/101; drafts 0/1/100/101/200/201;
  calculated/manual/edited and exact/near/transitive/unique pairs.
- **Actions:** build default; save draft; compare all pairs; canonical-rank conflicts; finalize.
- **Activation witnesses:** default cap, pairwise analyzer, revision CAS, conflict
  serializer, and final validator execute.
- **Oracle:** deterministic first 100; no silent removal; conflicts block; 100
  distinct pass; market switch does not mutate selection.
- **Call and operation counts:** exactly 19,900 pair comparisons at draft size 200.
- **Negative control:** skip the final pair; adversarial conflict fixture passes incorrectly and test fails.
- **Parity class:** `component`.
- **Cleanup:** remove only created selection rows and temporary fixtures in `finally`.

### `SCN-KI-012` — Lease/recovery competing owners

- **Requirements:** `INV-KI-006`.
- **Decisions:** `DEC-KI-018`, `022`.
- **Preconditions:** worker A/B, recovery, aggregator A/B, and injected DB clock.
- **Inputs:** times before/after the full 60-second task and 120-second
  aggregation leases; duplicate and reordered messages.
- **Actions:** execute every D4 pairwise schedule, heartbeat, reclaim, stale terminal, and check path.
- **Activation witnesses:** 20/40-second monitors, conditional renewals, recovery
  scan, task CAS, aggregator CAS, and publication fence execute.
- **Oracle:** one live fence; stale token changes zero rows; one counter and one
  publication; overdue pending work redelivers; terminal state is immutable.
- **Call and operation counts:** at most one active task owner and one active aggregator owner per row/stage.
- **Negative control:** omit token or generation predicate; overlap test fails.
- **Parity class:** `integration`.
- **Cleanup:** drop only the disposable schema and clear mock timers/messages in `finally`.

### `SCN-KI-013` — Maximum worker scale

- **Requirements:** `REQ-KI-003`–`005`, `REQ-KI-022`–`024`.
- **Decisions:** `DEC-KI-024`.
- **Preconditions:** no cache; all mocked provider tasks succeed on first attempt.
- **Inputs:** five seeds producing 300 distinct candidates; anchor metrics yield
  at least 201 active candidates so the deterministic shortlist is exactly 200;
  maximum normalized records for all nine markets.
- **Actions:** run the complete worker/component flow while recording operations,
  timers, memory, package, and artifact sizes.
- **Activation witnesses:** all ten expansion tasks, one anchor-screen task,
  eight remaining-market tasks, all three aggregators, calculator, final store,
  and emitted handler execute.
- **Oracle:** result is at most 32 MiB; O(k²) counters equal the formulas; no
  N+1 provider or DB behavior; emitted handler completes within measured bounds.
- **Call and operation counts:** 19 first-attempt calls/tasks, at most 95 calls
  across five attempts, at most 23 S3 objects, 19 work messages plus bounded
  checks, one HTTP call per invocation, `$0.492` first-pass reservation and
  `$2.46` five-attempt reservation.
- **Negative control:** generate 301 candidates, retain 201 shortlist rows, add
  a second US overview, or add one N+1 overview call; ceiling assertion fails.
- **Parity class:** `emitted_artifact`.
- **Cleanup:** clear only mock stores/queues and temporary emitted artifacts in `finally`.

### `SCN-KI-014` — Product and non-product query review

- **Requirements:** `REQ-KI-010`–`013`.
- **Decisions:** `DEC-KI-016`.
- **Preconditions:** research-backed review and legacy review harnesses exist.
- **Inputs:** all four lanes, manual/reclassified row, malicious operators,
  weak/failed/success probe fixtures, and one legacy Run.
- **Actions:** map; save/reorder/edit; confirm; invoke the existing probe service through its mock artifact seam.
- **Activation witnesses:** lane mapper, strict query parser, revision save,
  confirmation, probe marker/result, and legacy branch execute.
- **Oracle:** one row per item; exact prefixes; no add/delete; each valid row
  probes once; weak stays visible; legacy validation/count remains unchanged.
- **Call and operation counts:** one probe per valid research-backed row and zero extra probe for invalid rows.
- **Negative control:** route store lane to `/products`; expected-query assertion fails.
- **Parity class:** `integration`.
- **Cleanup:** drop only disposable rows and clear mock probe artifacts in `finally`.

### `SCN-KI-015` — Snapshot history

- **Requirements:** `REQ-KI-015`–`017`.
- **Decisions:** `DEC-KI-017`.
- **Preconditions:** completed research r and selection of N items.
- **Inputs:** later selection edits/saves and one completed Email Scraper Run.
- **Actions:** create Run transaction; mutate research selection; load Run/history/results.
- **Activation witnesses:** handoff uniqueness, snapshot serialization, N
  RunQuery inserts, later selection CAS, and historical reads execute.
- **Oracle:** snapshot/fingerprint/query lineage retain original N and fields;
  current research revision changes independently.
- **Call and operation counts:** exactly one handoff and N immutable lineage rows.
- **Negative control:** serialize historical Run from live research; history assertion fails.
- **Parity class:** `integration`.
- **Cleanup:** drop only the disposable schema in `finally`.

### `SCN-KI-016` — Complete dashboard interactions

- **Requirements:** `REQ-KI-014`, `REQ-KI-018`.
- **Decisions:** `DEC-KI-023`.
- **Preconditions:** authenticated owner session and real production Next build.
- **Inputs:** nonempty parsed result covering every lane, intent, flag, market, and chart.
- **Actions:** visit every surface and exercise controls, filters, sorting,
  pagination, edits, save/conflict, export, theme, charts, and canvas.
- **Activation witnesses:** each inventory component, API read/write, chart
  registration, canvas listener, and CSV exporter executes.
- **Oracle:** all surfaces are present/data-derived; CSV equals filtered table;
  no console/network/CDN/file/local-result error; one selection source exists.
- **Call and operation counts:** one mounted instance/listener set per component and one save request per action.
- **Negative control:** remove each surface registration; inventory set equality fails.
- **Parity class:** `emitted_artifact`.
- **Cleanup:** close spawned Next process and remove only its temporary build/test state in `finally`.

### `SCN-KI-017` — Responsive/reload/stale UI

- **Requirements:** `REQ-KI-002`, `REQ-KI-007`, `REQ-KI-014`.
- **Decisions:** `DEC-KI-019`, `023`.
- **Preconditions:** desktop/mobile viewports and restartable frontend/API mock.
- **Inputs:** queued, running, completed, failed, and stale-revision fixtures; tab close/remount.
- **Actions:** poll; close tab; restart client/API mock; reopen URL; race saves;
  resize and use pointer controls.
- **Activation witnesses:** polling timer, terminal cleanup, durable reload,
  revision conflict, responsive layout, and chart teardown execute.
- **Oracle:** tab closure does not change job; one timer exists and stops at
  terminal; durable state restores; stale UI cannot overwrite; no overflow/leak.
- **Call and operation counts:** one poll timer per mounted page and zero polls after terminal/unmount.
- **Negative control:** move completion state into the browser; reload test fails.
- **Parity class:** `local_e2e`.
- **Cleanup:** close spawned UI/API processes and clear timers/temp state in `finally`.

### `SCN-KI-018` — Full local maximum path

- **Requirements:** `REQ-KI-001`–`024`, `INV-KI-001`–`014`,
  `EXC-KI-001`–`008`, `AUTH-KI-001`–`004`, `AUTH-KI-006`, `AUTH-KI-007`.
- **Decisions:** `DEC-KI-001`–`025`, `026`–`038`.
- **Preconditions:** A5 assigns the reauthored W6 window agent; all five leaves
  are independently accepted; one direct isolated test URL distinct from
  production; emitted `.next` from the sole V2 build; loopback Chrome/auth/
  provider/backend ports available; manifest hashes match.
- **Inputs:** five deterministic seeds; expansion bodies whose exact union is
  300 candidates; US anchor metrics with at least 200 usable rows; eight
  remaining-market 200-row bodies; saved recommended 100; 100 independently
  editable queries; each Google body contains ten unique
  `w6-qNNN-rNN.myshopify.com` results.
- **Actions:** Chrome submits through emitted Next; actual auth client/proxy/
  backend create and execute durable research; close/reopen tab and restart
  Next/backend at named partitions; load actual result; save/resolve selection;
  initial and ambiguous-retry handoff; navigate to real run workspace; edit,
  reorder and confirm queries; the actual research validator and Google parser
  validate 100 deterministic search-page bodies;
  actual discovery workers and domain aggregator establish 1,000 lead tasks.
- **Activation witnesses:** one unique nonempty witness for every
  `W6-NAV-01`–`03`, `W6-FLOW-01`–`13`, `W6-RES-01`–`04` and
  `W6-CONF-01`–`06`; correlated Chrome/Next/auth/proxy/backend/SQL/worker/S3/SQS
  traces; no intercepted application API response.
- **Oracle:** required=registered=executed=activated is the literal 26-member
  set with global digest `d81bab26…`; all exceptional sets are empty; dashboard
  route is derived only from `run.runId`; numeric-v1/minimal-selection/saved-only/
  same-key/filter/CSV R5 contracts remain; exactly one immutable Run lineage
  survives later research mutation/restarts; owner B sees/mutates nothing;
  Neon terminal evidence alone advances stages.
- **Call and operation counts:** 10 expansion + 1 anchor + 8 remaining-market =
  19 first-pass keyword calls/attempts; exactly 23 keyword objects and 42 base
  keyword queue sends in the no-retry trace; 300/200/default-100;
  `$0.49200000`; 100 RunQueries; 100 Google calls × 10 results = 1,000
  occurrences; 100 discovery tasks; exactly 1,000 distinct stable shops,
  run stores and lead tasks; no lead fetch/enrichment.
- **Negative control:** execute all `W6-NC-01`–`13` as captured-data
  pass→single-mutation-fail→fresh-pass controls; production/source mutation is
  forbidden.
- **Parity class:** `local_e2e` with the exact `DEC-KI-038` substitute ledger;
  live provider/auth/AWS/Lambda/deployed parity is explicitly unclaimed.
- **Cleanup:** in `finally`, stop only spawned Chrome/Next/backend/auth/provider
  processes, disconnect clients, drop only the exact non-public disposable
  schema, verify its absence, remove only its `mkdtemp` directory, and preserve
  all source/accepted evidence. Cleanup failure fails the scenario.

### `SCN-KI-019` — Approved deployed canary

- **Requirements:** `AUTH-KI-005`.
- **Decisions:** `DEC-KI-025`.
- **Preconditions:** exact approved account, region, resources, actions, hashes,
  secrets, spend ceiling, and initially disabled event mapping.
- **Inputs:** one sanitized seed and approved canary identity.
- **Actions:** run read-only applied preflight; prove disabled mapping; perform
  only approved deploy/secret/mapping actions; use normal API through SQS,
  Lambda, Neon, S3, UI, and Run snapshot.
- **Activation witnesses:** applied IAM/config checks, disabled and enabled event
  paths, each worker stage, artifact writes, final UI, and handoff execute.
- **Oracle:** hashes/config/permissions match; result is nonempty and terminal;
  no DLQ/secret/raw log/unapproved mutation; actual calls/costs are recorded.
- **Call and operation counts:** exact live calls and mutations remain those in
  the approved W8 action manifest and must be recorded against planned ceilings.
- **Negative control:** disabled mapping leaves durable queued state and no hidden worker.
- **Parity class:** `production_canary`.
- **Cleanup:** perform only the exact separately approved live cleanup, or retain resources unchanged.

### `SCN-KI-020` — Corrected repository/worker schedules and atomic publication

- **Requirements:** `REQ-KI-002`, `005`, `015`–`017`, `022`; `INV-KI-002`,
  `004`–`008`, `014`.
- **Decisions:** `DEC-KI-002`, `018`, `022`, `026`, `027`.
- **Preconditions:** accepted W1 migration is applied to one disposable
  non-public schema; accepted W1 repository and W2 selection modules are loaded;
  injected clock/token/failure seams are deterministic; no external credential
  or live client is present.
- **Inputs:** calculated and manual selection items; queued researches with and
  without an expansion stage; one generation-one running research;
  exact expansion, anchor, and market task sets; attempts one through five;
  throttle delay, known success after fence loss, known-retry and ambiguous
  outcomes; early/ready/expired
  aggregator schedules;
  candidate/shortlist/result publication payloads and conflicting fingerprints.
- **Actions:** compare W2/repository IDs; load worker contexts; initialize and
  replay; race task claims and attempt reservation; crash after known settlement
  before retry scheduling, recover, schedule, deliver early, and deliver due;
  defer a throttled task without creating an attempt;
  settle a strict success after token loss and reclaim it from normalized cache;
  mark an exposed attempt ambiguous after lease loss; race early/ready/expired
  aggregators; inject rollback at each multi-row publication write; publish and
  replay the final result; call recovery and construct every strict W3 message
  without another repository lookup.
- **Activation witnesses:** six-byte item-ID helper, all context methods,
  ownerless initialize and lost-initialize recovery, token-fenced attempt
  counter/reservation, throttle defer, atomic known settlement plus cache,
  ambiguity marker, atomic retry scheduler, readiness predicate,
  expired aggregator reclaim, all three publication transactions, default
  selection revision one, complete recovery unions, and durable producedAt
  projection each execute.
- **Oracle:** exact initialization/publication replay is idempotent and a
  fingerprint mismatch conflicts; no worker/recovery value contains owner;
  attempt number and task count advance once; a lost-fence known success
  settles cost/cache but not task artifact and its reclaim makes zero HTTP
  calls; early retry/aggregator work makes
  zero downstream calls; no sixth attempt; ambiguity can never issue a second
  call; only one aggregator token wins; every injected publication failure
  leaves all members of its row set invisible; stale token publishes nothing;
  successful final publication exposes result, market manifest, selection
  revision one, and completed research together; recovery messages validate
  from returned data alone; replayed artifact metadata bytes are stable.
- **Call and operation counts:** zero real HTTP/S3/SQS/AWS calls; one logical
  attempt row per accepted attempt and at most five per task; one first-terminal
  count per task; exactly one anchor task after candidate publication and eight
  remaining-market tasks after shortlist publication; one selection revision
  and one final result publication.
- **Negative control:** separately remove the task-token predicate, aggregator
  readiness predicate, and final interactive transaction; the stale-worker,
  early-aggregation, and partial-visibility assertions respectively must fail.
- **Parity class:** `integration`.
- **Cleanup:** drop only the disposable schema and clear in-memory mocks in
  `finally`; never touch public or production data.

### `SCN-KI-021` — Escaped maximum-attempt replay, durable retry replay, and final-publication CAS

- **Requirements:** `REQ-KI-002`, `005`, `017`, `022`; `INV-KI-004`, `005`,
  `008`, `014`.
- **Decisions:** `DEC-KI-007`, `018`, `022`, `026`.
- **Preconditions:** reopened KI-R1 assignment; accepted schema in one
  disposable non-public schema; deterministic clock/token seams; the original
  `SCN-KI-020` suite remains present and passing; zero external clients.
- **Inputs:** (A) a processing task whose `attemptCount=5` and exact latest
  attempt five is `planned`, then separately `in_flight`; (B) a
  latest failed attempt scheduled once with persisted `nextAttemptAt`, replayed
  with clocks one millisecond before, exactly at, and sixty seconds after that
  value; (C) a ready market publication with injected conditional update counts
  of zero for the market-stage write and, separately, the research write; (D) a
  pre-existing `market_overview=completed` plus `research=running` partial row
  state.
- **Actions:** replay `recordAttempt` for each attempt-five state with equal and
  unequal inputs; schedule once and replay `scheduleRetry` at all three clocks;
  execute `publishResearchResult` under both zero-row failpoints and against the
  pre-existing partial state; reload every affected row after each operation.
- **Activation witnesses:** latest-attempt reconciliation executes before the
  new-attempt ceiling; pending retry replay reads its persisted due time;
  internal transaction-abort mapping executes for each zero-row publication
  write; partial completed-stage state takes the conflict branch.
- **Oracle:** every equal attempt-five replay is `found,mayCall:false`, retains
  exactly five attempt rows and `attemptCount=5`, and makes zero downstream
  calls; unequal replay conflicts; all retry replays return the byte-identical
  stored `retryAt` with no mutation; zero-row publication schedules leave
  market manifest/state, result, selection, revision, and research state wholly
  unchanged; the zero market-stage count returns `lost`, the zero research
  count returns `conflict`, and pre-existing partial state returns `conflict`
  with no write.
- **Call and operation counts:** zero HTTP/S3/SQS/AWS/provider calls; no new row
  on any replay; one initial retry scheduling mutation only; zero committed
  writes for each publication failpoint.
- **Negative control:** restore ceiling-before-replay, recompute retry from the
  later clock, or return normally after a zero-row research update; the
  corresponding attempt-five, durable-time, or partial-visibility assertion
  must fail.
- **Parity class:** `integration`.
- **Cleanup:** drop only the disposable schema in `finally`; never touch public
  or production data.

### `SCN-KI-022` — Conditional lease renewal, exact-expiry reclaim, and stale terminal denial

- **Requirements:** `REQ-KI-002`; `INV-KI-005`–`007`.
- **Decisions:** `DEC-KI-022`, `026`, `028`.
- **Preconditions:** A5 assigns KI-R2; accepted repository schema in one
  disposable non-public schema; repository A/B instances share that schema;
  deterministic `now` and 32-character task/aggregation token seams; no W3
  source is imported and no external client exists.
- **Inputs:** (A) one processing task claimed by A at `T0`, with clocks
  `T0+59,999ms`, `T0+60,000ms`, and `T0+60,001ms`; (B) one ready stage claimed
  by aggregator A at `T0`, heartbeat at `T0+40,000ms`, then clocks one
  millisecond before, exactly at, and one millisecond after its renewed
  `T0+160,000ms` expiry; (C) wrong tokens and terminal/missing identities; (D)
  ready expansion, anchor, and market stages capable of candidate, shortlist,
  final-result, and failure publication.
- **Actions:** task A renews once while live, then task B reclaims after the
  renewed expiry and A attempts heartbeat/terminalize; aggregator A claims and
  renews, aggregator B attempts claim before expiry, at exact expiry, and after
  expiry on isolated repetitions; after B owns, A attempts aggregation
  heartbeat, candidate publication, shortlist publication, final-result
  publication, and `failStage`; B performs the corresponding valid
  publication once. Reload every affected task, stage, research, selection,
  counter, manifest, and next-stage task set after each stale operation.
- **Activation witnesses:** task heartbeat `updateMany` includes state, token,
  and `leaseExpiresAt>now`; aggregation heartbeat includes deterministic
  identity, state, token, and `aggregationLeaseExpiresAt>now`; reclaim executes
  its `<=now` boundary; each ordinary terminal update executes its repeated
  live-expiry predicate; the completed-replay branch executes separately.
- **Oracle:** live renewals return `claimed` and exact expiries
  `now+60000ms`/`now+120000ms`; each heartbeat performs one update and zero
  reads; pre-expiry competing owner is `lost`; exact-expiry aggregator reclaim
  has one winner; expired/wrong/stale renewals and terminal operations are
  `lost` with zero durable changes; one live owner increments one task counter
  or publishes one manifest/result/selection exactly once; completed exact
  replay is `found`; no old owner can revive or publish after B's claim.
- **Call and operation counts:** zero HTTP/S3/SQS/AWS/provider calls; one
  conditional update per heartbeat; zero rows changed by every stale call;
  exactly one aggregation-attempt increment per successful claim/reclaim,
  exactly one terminal counter increment per task, and exactly one committed
  publication for each isolated valid-publication case.
- **Negative control:** use the additive
  `clientWithRemovedTaskHeartbeatPredicate(client,key)` Proxy helper described
  in `KI-R2-T1`; independently delete (1) `leaseToken`, (2) `state`, and (3)
  `leaseExpiresAt` only from the cloned task-heartbeat `updateMany.where`. The
  wrong-token, terminal-row, and expired-owner assertions respectively must
  fail. The unwrapped client with unchanged production source must make all
  three pass.
- **Parity class:** `integration`.
- **Cleanup:** in `finally`, disconnect clients and drop only the exact
  run-created disposable schema through `isolated-postgres.js`; query for its
  absence; never read, clean, or migrate `public`.

### `SCN-KI-023` — Original-expiry task denial and post-reclaim aggregation denial

- **Requirements:** `REQ-KI-002`; `INV-KI-005`–`007`.
- **Decisions:** `DEC-KI-022`, `DEC-KI-028`, `DEC-KI-029`.
- **Risk dimensions:** lease kind `{task,aggregation}`; decisive equality
  boundary `{original task expiry, renewed aggregation expiry}`; actor
  `{same old task token, old aggregation token after B reclaim}`; durable
  effect `{task/stage rows, stage/research rows}`. The two listed schedules are
  exhaustive for the escaped dimensions. `+1ms`, wrong-token, terminal,
  publication, duplicate, and missing-row combinations are excluded because
  unchanged `SCN-KI-022` covers them or they execute the identical strict
  greater-than false branch with no additional time-dependent operation.
- **Preconditions:** A5 assigns the reopened KI-R2 proof gate; backend begins at
  RP2; repository/unit files are byte-identical; one isolated non-public schema
  is created by `isolated-postgres.js`; fixed `T0` and valid distinct A/B tokens
  are available; no W3 or external client is imported.
- **Inputs:** one task claimed by A at `T0`; one all-terminal ready stage claimed
  by aggregator A at `T0`, renewed at `T0+40,000ms`, and eligible for reclaim
  at exactly `T0+160,000ms`.
- **Actions:** snapshot task plus owning stage, call same-token task heartbeat at
  exactly `T0+60,000ms`, reload; let B reclaim the aggregation stage at exactly
  `T0+160,000ms`, snapshot full stage plus research row, call stale A's
  aggregation heartbeat at the same instant, reload.
- **Activation witnesses:** the task call reaches the exact equality case of
  `leaseExpiresAt>now`; B's successful claim reaches the exact equality case of
  `aggregationLeaseExpiresAt<=now`; stale A's later call reaches the token and
  live-expiry fenced aggregation `updateMany` after ownership changed.
- **Oracle:** both stale heartbeats return `{outcome:"lost"}`; task/stage rows
  deep-equal around the task call; stage/research rows deep-equal around stale
  A's aggregation call; B owns the aggregation stage; zero provider/S3/SQS/AWS
  calls; no counter, token, expiry, owner, state, manifest, selection, result,
  task-set, or research field changes from either stale call.
- **Negative control:** in the same frozen test file/hash lineage, run unchanged
  `SCN-KI-022 V5`; its non-mutating Proxy removes the task heartbeat
  `leaseExpiresAt` predicate and must cause the unchanged `lost` assertion to
  throw, while the unwrapped repository passes. This is representative because
  RT2 changes no production predicate; duplicating the Proxy for aggregation
  would test the mock seam rather than a second implementation change.
- **Parity class:** isolated database integration.
- **Cleanup:** `t.after` disconnects and drops only the generated schema, then
  asserts that exact schema is absent. Handoff performs one read-only prefix
  absence query; neither action reads, migrates, or cleans `public`.

### `SCN-KI-024` — Known-response fence loss and byte-identical task recovery

- **Requirements:** `REQ-KI-002`, `004`, `005`, `021`–`024`;
  `INV-KI-004`–`009`.
- **Decisions:** `DEC-KI-007`, `009`, `020`, `022`, `026`, `028`–`030`.
- **Risk dimensions:** endpoint `{suggestions,related,overview}`; strict response
  `{success,retryable_failure,terminal_failure}`; settlement fence
  `{terminal_active,found_active,lost,found_stale}`; crash boundary
  `{after_settle_before_S3,after_S3_before_terminal}`; recovery
  `{same_owner_before_expiry,new_owner_at_expiry}`. Exhaustively cross every
  response with every fence in adapter component tests; exhaust both crash
  boundaries for one suggestions success through the real repository/S3 store.
  Related/overview crash repetitions are excluded because artifact construction
  is separately schema-tested and uses the identical recovery branch; malformed
  JSON is instead exhaustively tested at HTTP 200/429/500 because status
  previously changed behavior.
- **Preconditions:** accepted repository hashes match P2; one isolated schema;
  one initialized expansion task; deterministic T0/A/B tokens; strict synthetic
  response fixtures; in-memory encrypted-metadata-compatible S3 and dispatcher;
  no live credential/provider/AWS client.
- **Inputs:** provider cost `0.01560000`; fixed request/result fingerprints;
  latest succeeded attempt/cache; task expiry T0+60s; one S3 wrapper that throws
  before put and one that delegates the put then throws.
- **Actions:** run every adapter fence pair and record schedule/S3/terminal
  counts; for each crash case run A through the injected boundary, advance to
  exact lease expiry, redeliver as B, reconstruct from attempt+cache, write or
  exact-match the immutable artifact, terminalize, and send one check. Separately
  reject JSON decode at 200/429/500.
- **Activation witnesses:** every settlement-union branch; the no-schedule stale
  branch; ambiguity terminalization; attempt/cache fingerprint comparison;
  succeeded-cost artifact construction; S3 precondition exact-match; task live
  terminal predicate and recovery check execute.
- **Oracle:** strict known cost/cache is durable even when the task fence is
  lost; lost/stale settlement returns lost and performs zero retry/S3/terminal/
  check; undecodable response is ambiguous with zero settle/schedule; each crash
  replay performs zero additional HTTP calls and yields identical body,
  metadata, content fingerprint, and `costUsd:"0.01560000"`; exactly one task
  terminal/counter/check results.
- **Call and operation counts:** one HTTP and one attempt row per crash fixture;
  zero second HTTP; at most two immutable put attempts to one key, one stored
  object, one terminal counter, one check; stale retry settlement makes zero
  `scheduleRetry` calls.
- **Negative control:** in a non-mutating test wrapper, reinterpret
  `lost|found_stale` as active and build succeeded recovery as cacheHit. The
  unchanged zero-publication assertion and immutable byte/cost assertion must
  fail; rerunning the same inputs through production functions passes.
- **Parity class:** isolated database integration.
- **Cleanup:** disconnect/drop only the run-created schema and assert absence;
  clear in-memory S3/SQS/HTTP state in `finally`; no public/production cleanup.

### `SCN-KI-025` — Task monitor, voluntary release, and delayed redelivery

- **Requirements:** `REQ-KI-002`, `005`, `022`, `023`; `INV-KI-005`–`008`,
  `INV-KI-012`.
- **Decisions:** `DEC-KI-007`, `008`, `018`, `022`, `026`, `028`–`030`.
- **Risk dimensions:** duration `{short,greater_than_120s}`; monitor outcome
  `{live,lost}`; loss boundary `{before_provider,during_provider,before_S3,
  during_S3,before_terminal}`; release `{throttle,retry,ambiguity,stale}`;
  delayed send `{success,failure,early_duplicate,due_recovery}`. Required
  pairwise coverage combines every loss boundary with lost, every release with
  monitor stop, and every delayed-send state. Cross-product of provider endpoint
  and boundary is excluded because RT1 exhausts endpoint settlement and the
  service branch is endpoint-independent.
- **Preconditions:** deterministic clock/timer factory; task A claimed at T0;
  real repository for the decisive long/lost case and stateful component
  repository for boundary injection; controllable HTTP/S3 promises; dispatcher
  records fourth-argument options.
- **Inputs:** renew ticks at T0+20/40/60/80/100/120s; last expiry T0+180s; B
  reclaim exactly at T0+180s; retryAt values yielding 0/1/75 seconds; one failed
  SQS send and one early duplicate before due.
- **Actions:** hold provider/S3 promises while manually running monitor ticks;
  exercise long live completion; let B reclaim at the exact renewed expiry and
  make stale A finish a strict response; exercise every injected loss boundary;
  run throttle/retry/ambiguity release; inspect SQS command delay; redeliver
  early and invoke recovery at due time.
- **Activation witnesses:** real 20-second monitor configuration and six
  renewals; heartbeat live/lost paths; `assertActive` before/after external
  boundaries; renew-stop-assert terminal preparation; exact voluntary-loss
  suppression; `DelaySeconds`; claim delayed branch and recovery dispatch.
- **Oracle:** live work beyond two original leases retains one owner and
  terminalizes once; after B reclaim, A's settlement may record known global
  cost/cache but A writes no S3/task terminal/check; every detected loss stops
  later boundaries; voluntary release emits at most one correctly delayed
  message after monitor stop; send failure remains recoverable; early duplicate
  makes zero attempt/HTTP; due recovery dispatches once.
- **Call and operation counts:** heartbeat every 20,000ms with no overlap; one
  HTTP per invocation; zero sleep/poll; one SQS retry message per successful
  send, zero new attempt on throttle/early delivery, one recovered dispatch at
  due, one task counter at final success.
- **Negative control:** supply an otherwise identical monitor whose
  `assertActive` ignores its captured renewal failure; the no-S3-after-loss
  assertion must fail, while the production factory makes it pass and the
  durable terminal fence still rejects stale Neon mutation.
- **Parity class:** component. The decisive A/B settlement/recovery member is
  executed in the `SCN-KI-024` isolated-database scenario and is not a second
  parity claim for this scenario.
- **Cleanup:** stop every fake/real monitor in `finally`, reject outstanding
  promises, clear mock messages/objects, and drop only the named disposable
  schema used by the combined database member.

### `SCN-KI-026` — Aggregation monitor across all terminal paths

- **Requirements:** `REQ-KI-002`–`005`, `023`, `024`; `INV-KI-004`–`007`.
- **Decisions:** `DEC-KI-005`, `006`, `018`, `020`, `022`, `026`,
  `028`–`030`.
- **Risk dimensions:** stage `{expansion,anchor_screen,market_overview}`;
  terminal path `{publish,failed_task,empty_anchor,calculation_failure}`;
  duration `{short,greater_than_240s}`; lease outcome `{live,lost}`; loss boundary
  `{before_get,during_get,before_put,after_put_before_publication,
  before_failStage}`. Execute every stage publish path, every failure path, and
  every loss boundary; use the market publish for the >240s member. Other
  stage×duration repetitions are excluded because all stages use the same
  factory/wrappers and their distinct publication methods are separately
  activated.
- **Preconditions:** a stateful repository exposes exact R2 aggregation unions;
  each stage has its immutable ordered terminal task set and validated artifacts;
  deterministic clock/timer and controllable artifact promises; no live S3/SQS/
  provider/database client.
- **Inputs:** renew ticks T0+40/80/120/160/200/240s; competitor B at exact last
  renewed expiry; valid expansion/anchor/market artifacts; one failed task, one
  zero-metric anchor, and one calculation-throw fixture.
- **Actions:** process aggregate checks through every stage/path; hold one market
  S3 read through all six ticks; inject A renewal loss and B ownership at every
  listed boundary; release the held operation; record artifact, publication,
  failure, and dispatch calls.
- **Activation witnesses:** 40-second monitor/heartbeatAggregator; every
  before/after S3 assertion; all three manifest/result builders; all three
  publication methods; fenced failStage; finally stop; completed-stage replay.
- **Oracle:** live long aggregation publishes exactly once; detected loss makes
  no later S3/Neon/SQS call; a deterministic orphan written before loss is safe
  for B's replay; failStage reports stage_failed only for terminal/found and
  propagates lost/conflict/not_found; next tasks/checks dispatch only after a
  terminal/found publication; completed replay performs no external work.
- **Call and operation counts:** one monitor and nonoverlapping renewal stream per
  claim; expansion creates one US task, anchor creates eight ordered market
  tasks, market creates one manifest and one result; one publication or failure
  transaction; zero S3 listing/completion checks.
- **Negative control:** make only `assertActive` ignore the captured aggregation
  renewal loss. The local zero-later-S3/publication-call oracle must fail; the
  production monitor passes, and the R2 repository fence remains the independent
  zero-Neon-mutation control.
- **Parity class:** component; accepted `SCN-KI-022/023` supplies the unchanged
  repository integration half by exact source/test/schema hashes.
- **Cleanup:** stop monitors and clear all mock artifacts/messages/promises in
  `finally`; no database or external cleanup is used by this component scenario.

### `SCN-KI-027` — Isolated reproducible keyword Lambda package

- **Requirements:** `REQ-KI-002`, `023`, `024`; `INV-KI-002`.
- **Decisions:** `DEC-KI-001`, `024`, `027`, `029`, `030`; D9.
- **Risk dimensions:** path class `{keyword_staging,keyword_zip,
  sibling_staging,sibling_zip,measurements}`; build repetition `{first,second}`;
  inventory class `{entry,Prisma_client,engine,forbidden}`; runtime
  `{cold_import,empty_invocation}`. All listed members execute. Platform/runtime
  variants are excluded because D9 fixes Node24/AL2023 and live deployed parity
  belongs to W8.
- **Preconditions:** installed locked dependencies; `zip`/`unzip`; seven-handler
  baseline build and measurement succeed; test-created sibling/keyword sentinels
  and pre-build SHA-256 inventory are recorded.
- **Inputs:** current W3 entry point; one obsolete keyword-only archive member;
  one sibling sentinel; fixed 1980 timestamp and sorted file set.
- **Actions:** build/measure seven handlers; hash siblings; seed obsolete own
  member; build keyword twice; inspect/extract ZIP; cold-import index; compare
  hashes/inventories and invoke exported handler at its empty boundary.
- **Activation witnesses:** exact own-path removals, esbuild entry, Prisma copy
  filter, timestamp normalization, sorted zip, stale-own-member removal, sibling
  preservation, cold ESM import and handler export execute.
- **Oracle:** obsolete own member absent; every sibling and measurements hash is
  byte-identical; two keyword ZIP hashes/inventories match; exactly one required
  AL2023 engine; no env/test/fixture/doc/map/credential path; ZIP ≤45MiB,
  unzipped ≤200MiB; import succeeds without work and `handler` is a function;
  `KEYWORD_ARTIFACT_MAX_BYTES=33554432` while default store remains 5000000.
- **Call and operation counts:** one baseline build/measure, two keyword builds,
  one extraction/inventory and one cold import; zero network/database/provider/
  AWS/Git operations.
- **Negative control:** evaluate a test-only copy/mutation that removes the
  shared build root; the sibling sentinel/hash assertion must fail. The real
  source is neither edited for the control nor left mutated.
- **Parity class:** emitted artifact.
- **Cleanup:** remove only test-created sentinels and temporary extraction in
  `finally`; retain normal gitignored build output for handoff measurement; do
  not remove sibling builds or archives.

### `SCN-KI-028` — Settlement-cost and dispatcher strictness manifest

- **Requirements:** `REQ-KI-021`–`023`; `INV-KI-002`, `008`, `009`.
- **Decisions:** `DEC-KI-009`, `026`, `030`, `031`.
- **Risk dimensions:** exact manifest groups `adapter` (16) and `dispatcher`
  (12); no inferred combination or omitted member.
- **Preconditions:** P1–P4 pass; strict in-memory repository/SQS client; the
  versioned manifest parses and its two group arrays equal the A4 literals.
- **Inputs:** fixed attempt/cost `0.01560000`, every settlement/ambiguity member,
  decode statuses 200/429/500, and every options boundary in Q01–Q12.
- **Actions:** execute each case once as a named subtest; capture result/error,
  settlement/schedule/ambiguity/send counts, and command input.
- **Activation witnesses:** each settlement classification branch,
  `providerCostUsd` projection, ambiguity result gate, default-options branch,
  plain-object/key/value validators, and delayed/original command constructors.
- **Oracle:** every case satisfies the exact result/trace/count rule above;
  executed IDs equal both manifest groups and contain no duplicate/skip/todo.
- **Call and operation counts:** 28 cases; Q01–Q04 one send each, Q05–Q12 zero;
  A05–A07 zero schedule; A11–A13 one ambiguity each.
- **Negative control:** injected active fence omits cost and injected dispatcher
  accepts null; A01 and Q05 unchanged assertions fail, then production passes.
- **Parity class:** component.
- **Cleanup:** restore no source because controls mutate collaborators only;
  clear repository/client arrays in `finally`.

### `SCN-KI-029` — Ordinary and recovered task fence manifest

- **Requirements:** `REQ-KI-002`, `005`, `021`–`023`; `INV-KI-004`–`009`.
- **Decisions:** `DEC-KI-007`, `009`, `020`, `022`, `026`, `028`, `030`, `031`.
- **Risk dimensions:** exact manifest groups `task_component` (18) and
  `recovery_component` (18), including every terminal result member, every
  provider/S3 loss boundary, all durable attempt classifications, and both
  voluntary-release dispatch outcomes.
- **Preconditions:** deterministic monitor/clock; stateful repository, S3, HTTP,
  and dispatcher seams; valid research/stage/task/cache/artifact fixtures.
- **Inputs:** literal T01–T18/R01–R18 cases and trace rules above; six renewal
  ticks; known cost `0.01560000`; exact provider safe codes.
- **Actions:** run each case once; release controlled promises at the named
  boundary; record the complete operation trace and durable collaborator state.
- **Activation witnesses:** monitored fetch/json/S3 wrappers; renew-stop-assert;
  terminal result gate; cache triple fingerprint check; ambiguity/retry/
  terminal-failure classifiers; monitor-stop-before-dispatch.
- **Oracle:** the exact case traces/results/counters above; no operation after a
  forbidden suffix; executed IDs equal both manifest groups.
- **Call and operation counts:** 36 cases; at most one HTTP per invocation;
  terminal `lost|conflict|not_found` makes zero checks; known terminal recovery
  makes zero HTTP/schedule; six renewal ticks do not overlap.
- **Negative control:** T18 maps lost terminal to active and R18 omits recovery
  preparation; unchanged zero-check/zero-terminal assertions fail, then
  production passes.
- **Parity class:** component.
- **Cleanup:** stop monitors, settle/reject held promises, and clear mock state
  in `finally`; no database/external cleanup.

### `SCN-KI-030` — Durable crash and renewed-expiry task schedules

- **Requirements:** `REQ-KI-002`, `005`, `022`, `023`; `INV-KI-004`–`008`.
- **Decisions:** `DEC-KI-007`, `009`, `020`, `022`, `026`, `028`–`031`.
- **Risk dimensions:** exact `task_database` IDs D01–D05; success crash at both
  durable boundaries, terminal/retryable failure crash, and exact renewed-expiry
  competing owner.
- **Preconditions:** one generated non-public isolated schema, accepted Prisma
  schema/repository hashes, deterministic T0/A/B tokens, in-memory S3/HTTP/SQS.
- **Inputs:** one initialized suggestions task per fixture, cost `0.01560000`,
  fixed fingerprints, attempt states/safe codes, six 20-second renewals.
- **Actions:** inject the named crash, reclaim/redeliver, and drive recovery;
  for D05 let B claim at exact renewed expiry before stale A resumes.
- **Activation witnesses:** real settle/cache transaction, immutable put,
  terminal/counter transaction, schedule retry, heartbeat/live-expiry claim and
  stale terminal denial.
- **Oracle:** exact D01–D05 rows/objects/messages/calls above; sorted executed IDs
  equal the manifest group; no second paid call for D01–D03.
- **Call and operation counts:** five cases; one initial attempt per fixture;
  zero recovery HTTP in D01–D03/D05; one schedule in D04; one final terminal
  counter/check where specified.
- **Negative control:** the already-executed component T18/R18 controls apply to
  these production branches; no source/database mutation control is repeated in
  this risk-proportionate DB gate.
- **Parity class:** isolated database integration.
- **Cleanup:** `t.after` disconnects/drops only the generated schema, asserts its
  exact absence, and clears mock S3/SQS/HTTP; never inspect or clean `public`.

### `SCN-KI-031` — Aggregation outcome and lease-boundary manifest

- **Requirements:** `REQ-KI-002`–`005`, `023`, `024`; `INV-KI-004`–`007`.
- **Decisions:** `DEC-KI-005`, `006`, `018`, `020`, `022`, `026`, `028`–`031`.
- **Risk dimensions:** exact `aggregation` IDs G01–G24: every publication and
  failure result member, get/put loss, orphan replay safety, and >240-second
  live aggregation.
- **Preconditions:** deterministic monitor/clock, stateful repository outcomes,
  complete valid stage/task/artifact fixtures, controlled S3 promises.
- **Inputs:** literal G01–G24 cases, six 40-second ticks, one injected failed
  task, zero-metric anchor, and calculation failure.
- **Actions:** execute each case once and record the exact operation alphabet;
  release held get/put only after the selected renewal/loss.
- **Activation witnesses:** all three publication methods, failStage union,
  every monitored S3 boundary, six aggregation heartbeats, final monitor stop,
  and next-task/check dispatcher gates.
- **Oracle:** exact G01–G24 result/trace/count rules; one safe orphan at most;
  executed IDs equal the manifest group with no skip/todo.
- **Call and operation counts:** 24 cases; expansion terminal/found emits 1+1,
  anchor emits 8+1, market zero; loss outcomes emit zero; one publication or
  failure call per applicable case.
- **Negative control:** injected monitor ignores captured loss; G24's zero-later
  operation assertion fails, then production passes.
- **Parity class:** component.
- **Cleanup:** stop monitors, settle held promises, and clear in-memory state in
  `finally`; no database/external cleanup.

### `SCN-KI-032` — Corrective manifest and source-scope conformance

- **Requirements:** `REQ-KI-002`, `023`, `024`; `INV-KI-002`, `004`–`009`.
- **Decisions:** `DEC-KI-029`–`031`.
- **Risk dimensions:** exact `conformance` IDs C01–C08; manifest shape, group/
  global uniqueness, helper/symbol/file/import scope, and test activation.
- **Preconditions:** final local source/tests frozen; P2 hashes and A5 authorized
  scope available; manifest readable as UTF-8 JSON.
- **Inputs:** literal manifest, `git diff 37a0e020...`, production source, test
  registration metadata.
- **Actions:** parse and compare exact sets/counts/hashes; inspect only changed
  hunks for named production symbols/helpers/imports; inspect selected tests for
  skip/todo and executed-ID certificates.
- **Activation witnesses:** every C01–C08 assertion executes and the global
  101-ID hash is independently recomputed.
- **Oracle:** all exact sets equal; no duplicate/unowned file/symbol/helper/
  import/ID; selected scenario set contains no skipped or todo case.
- **Call and operation counts:** eight cases; zero network/database/provider/AWS
  calls and zero filesystem writes.
- **Negative control:** add a synthetic extra ID/helper/file only to the
  in-memory discovered set; the corresponding equality assertion fails, then
  the real discovered set passes.
- **Parity class:** static conformance.
- **Cleanup:** no source mutation; discard in-memory synthetic sets.

## 4. Mandatory parent authoring checklist

### 4.1 Authority and artifacts

- [x] `PA-001` All governing instructions and authorities are recorded. Evidence: `SRC-KI-001`, `EV-KI-A-001`
- [x] `PA-002` All eight package artifacts exist at named paths and name one another. Evidence: `EV-KI-A-025`; A5 state 66 names the keyword package.
- [x] `PA-003` Mutable status exists only in `A5`. Evidence: `EV-KI-A-002`
- [x] `PA-004` Execution and approval boundaries are explicit. Evidence: `AUTH-KI-001`–`006`, `DEC-KI-025`
- [x] `PA-005` Current working tree and repository boundaries were inspected. Evidence: `SRC-KI-003`, `SRC-KI-037`, `EV-KI-A-048`
- [x] `PA-006` Product scope, exclusions and compatibility policy are locked. Evidence: `REQ-KI-001`–`024`, `EXC-KI-001`–`008`
- [x] `PA-007` The canonical parent and recursive sub-window authoring-standard
  paths and SHA-256 revisions are pinned for the assignment. Evidence:
  `EV-KI-A-037`, `EV-KI-A-038`, `EV-KI-A-048`; KI-R5 assignment remains parent-reserved.

### 4.2 Evidence and payload safety

- [x] `PP-001` Every material fact has an allowed classification. Evidence: `EV-KI-A-003`
- [x] `PP-002` No inferred fact enters a locked contract or task. Evidence: `EV-KI-A-003`
- [x] `PP-003` Every material external or internal-boundary payload has provenance-labelled sanitized structural evidence. Evidence: `SRC-KI-019`–`022`, `034`–`036`, `PAY-KI-001`–`008`, `EV-KI-A-048`
- [x] `PP-004` Every consumed field has one exact evidence-backed path and type. Evidence: `PAY-KI-001`–`005`, `008`, `EV-KI-A-004`, `EV-KI-A-048`
- [x] `PP-005` Every payload has an exact strict parser and normalized internal result specified. Evidence: `PAY-KI-001`–`008`, `DEC-KI-019`, `020`, `034`, `EV-KI-A-048`
- [x] `PP-006` Missing, malformed, boundary and unknown-field fixture files exist. Evidence: `EV-KI-A-029`; all four fixture files exist under `email_scraper/test/fixtures/keyword-intelligence/` (42 synthetic cases total) covering positive/missing/malformed/boundary/unknown categories per `PAY-KI-002`–`006`, structurally validated for unique IDs, category coverage, and absence of secret markers; no provider body or customer data is reproduced.
- [x] `PP-007` Multiple supported shapes use explicit evidence-backed discrimination; N/A for provider variants because exactly one observed shape is supported. Evidence: `SRC-KI-019`–`021`, `PAY-KI-003`–`004`
- [x] `PP-008` No fallback probing, alias guessing, permissive cast, or synthetic evidence is permitted. Evidence: `SRC-KI-022`, `PAY-KI-002`–`005`
- [x] `PP-009` Raw secrets and unnecessary private payload data are excluded. Evidence: `INV-KI-009`, `EV-KI-A-005`
- [x] `PP-010` All unknown payload facts are blocking or safely parked; unknown consumed payload count is zero. Evidence: `SRC-KI-027`, `SRC-KI-034`–`036`, `EV-KI-A-004`, `EV-KI-A-048`

### 4.3 Discovery and lifecycle closure

- [x] `PD-001` All applicable Phase-B inventories are complete. Evidence: `SRC-KI-001`–`037`, `EV-KI-A-006`, `EV-KI-A-026`, `EV-KI-A-048`
- [x] `PD-002` Claimed absences have negative-search evidence. Evidence: `SRC-KI-012`, `023`, `024`
- [x] `PD-003` Every workflow has a complete state-transition table. Evidence: `DEC-KI-018`, `035`; A3 Sections 2 and 4; `EV-KI-A-048`
- [x] `PD-004` Every external and durable failure boundary is classified. Evidence: A3 D2/D6 and KI-R5 delta; `DEC-KI-030`, `034`–`037`; `SCN-KI-006`, `024`–`027`, `036`–`040`; `EV-KI-A-035`, `EV-KI-A-048`
- [x] `PD-005` Duplicate, reorder, retry, restart, stale-process, and cancellation behavior is locked. Evidence: `DEC-KI-007`, `015`, `018`, `022`, `028`, `030`, `035`, `036`; `EXC-KI-007`; `SCN-KI-022`, `024`–`026`, `036`–`038`; `EV-KI-A-048`
- [x] `PD-006` Every terminal and visibility boundary has durable evidence. Evidence: `INV-KI-005`, `014`; A3 Section 2

### 4.4 Decision closure

- [x] `PC-001` Every applicable D1–D13 ledger, including D2A, is complete. Evidence: A3 Sections 3–4, `EV-KI-A-007`, `EV-KI-A-048`
- [x] `PC-002` Every interface and payload schema is exact. Evidence: `PAY-KI-001`–`008`, `DEC-KI-019`–`021`, `026`–`030`, `034`–`037`; `EV-KI-A-032`, `EV-KI-A-033`, `EV-KI-A-035`, `EV-KI-A-048`
- [x] `PC-003` Every multi-write sequence is atomic or has an exact recovery protocol. Evidence: A3 D2 and KI-R5 delta; lifecycle tables; `DEC-KI-026`, `028`, `030`, `035`; `SCN-KI-020`–`027`, `037`; `EV-KI-A-033`, `EV-KI-A-035`, `EV-KI-A-048`
- [x] `PC-004` Every durable key, identity, fingerprint, and timestamp has an exact formula/source. Evidence: `DEC-KI-002`, `007`, `009`, `020`, `026`–`030`
- [x] `PC-005` Every identity cardinality and substitution rule is explicit. Evidence: A3 D3
- [x] `PC-006` Every competing-owner pair has atomic exclusion, fencing, or commutativity proof. Evidence: A3 D4 and KI-R5 delta; `DEC-KI-030`, `035`; `SCN-KI-008`, `012`, `020`, `022`, `024`–`026`, `037`; `EV-KI-A-048`
- [x] `PC-007` Every external operation has bounded cardinality, retry, ambiguity, and exact cost semantics. Evidence: `SRC-KI-030`–`032`; A3 D6; `DEC-KI-005`–`009`, `024`, `030`; `SCN-KI-005/006/013/024/025`.
- [x] `PC-008` Every permitted retry reconstructs all inputs from durable evidence. Evidence: `DEC-KI-005`–`009`, `020`, `022`, `026`–`030`; `SCN-KI-024/025`
- [x] `PC-009` Every replay-affecting configuration value has an exact durability/drift policy. Evidence: `DEC-KI-004`; A3 D7
- [x] `PC-010` Control-plane, status, and public-output paths are closed. Evidence: `DEC-KI-018`, `019`, `023`, `034`–`036`; A3 D8 and KI-R5 delta; `EV-KI-A-048`
- [x] `PC-011` Build/runtime/deployment dependency closure is proven. Evidence: `EV-KI-A-029`, `DEC-KI-030`, `SCN-KI-027`, `EV-KI-A-035`; exact versions installed and emitted closure proven — `@noble/hashes@2.2.0` in backend (zero runtime dependencies, ESM, sha256 import-verified, Node 24 startup 0.07–0.08 s, correct subpath `@noble/hashes/sha2.js`) and `chart.js@3.9.1` + `chartjs-chart-treemap@2.0.0` in frontend (peer satisfied, dual CJS/ESM load verified, startup 0.10–0.11 s); the existing Next 16.2.12 production build passes with both installed; only dependency manifests changed in either repo.
- [x] `PC-012` Applied environment capabilities and limits are measured or explicitly gated with complete branches. Evidence: `SRC-KI-025`, `DEC-KI-025`; A3 D10
- [x] `PC-013` Scale, operation growth, and resource ceilings are locked. Evidence: `DEC-KI-024`, `034`; A3 D11 and KI-R5 delta; `SRC-KI-035`, `EV-KI-A-048`
- [x] `PC-014` Historical/mixed-version policy is explicit. Evidence: `REQ-KI-019`–`021`; `DEC-KI-034/037`; A3 D12 and KI-R5 delta; `EV-KI-A-048`
- [x] `PC-015` No task leaves two materially different implementations possible. Evidence: `EV-KI-A-028`, `EV-KI-A-032`, `EV-KI-A-033`, `EV-KI-A-035`, `EV-KI-A-036`, `EV-KI-A-037`; `DEC-KI-021` enumerates schema literals, `DEC-KI-026`/`027` and `KI-R1-T1` lock the first corrective repository boundary, `DEC-KI-028`/`KI-R2-T1` lock renewal/exact-expiry/live-terminal predicates, and `DEC-KI-032` plus `KI-R4-T1`–`T4` lock the escaped KI-R3 behavior, fixed-revision enforcement, and exact recursive ownership.
- [x] `PC-016` Storage transport, namespace, migration history, and cleanup are specified fail-closed. Evidence: A3 D2A and KI-R5 delta; `KI-W1-T1`, `KI-R5-V3`; `EV-KI-A-048`

### 4.5 Scenario and acceptance closure

- [x] `PS-001` Scenario dimensions derive from current ledgers. Evidence: A4 Sections 2–3; `DEC-KI-037`, `EV-KI-A-048`
- [x] `PS-002` Combination strategy and exclusions are justified. Evidence: A4 Section 3 opening and KI-R5 scenario ledger; `EV-KI-A-048`
- [x] `PS-003` Every scenario has exact preconditions, actions, activation witnesses, and oracle. Evidence: `SCN-KI-001`–`040`; `EV-KI-A-036`, `EV-KI-A-048`
- [x] `PS-004` Representative nonempty end-to-end behavior is required. Evidence: `SCN-KI-001`, `018`, `019`
- [x] `PS-005` End-to-end acceptance cannot pass through a zero-work/bypass path. Evidence: `SCN-KI-001`, `018`
- [x] `PS-006` Negative controls prove required tests can fail. Evidence: `SCN-KI-001`–`040`; KI-R3 controls; KI-R5 `NC-01`–`NC-12`; `EV-KI-A-048`
- [x] `PS-007` Every durable/external failure boundary has injection coverage. Evidence: `SCN-KI-006`, `012`, `018`, `020`–`032`, `036`–`040`; `EV-KI-A-048`
- [x] `PS-008` Every competing-owner pair has a schedule-sensitive behavioral test. Evidence: A3 D4 and KI-R5 delta; `SCN-KI-008`, `012`, `020`, `022`, `024`–`026`, `030`, `037`; `EV-KI-A-048`
- [x] `PS-009` Generated tests use deterministic evidence-backed values and invariants. Evidence: `SCN-KI-010`, `013`, `018`, `021`–`032`
- [x] `PS-010` Representative and maximum workload tests assert operation/resource ceilings. Evidence: `SCN-KI-013`, `018`, `024`–`031`, `036`–`039`; `SRC-KI-035`, `EV-KI-A-048`
- [x] `PS-011` Evidence parity classes match every acceptance claim. Evidence: each scenario parity field; A3 D9/D10 and `DEC-KI-037` substitute limits; `EV-KI-A-048`
- [x] `PS-012` Final/public output is traced to the exercised path. Evidence: `SCN-KI-001`, `015`, `018`, `019`
- [x] `PS-013` Every applicable window has a complete behavioral coverage
  matrix derived from reachable paths and behavior-changing partitions.
  Evidence: `DEC-KI-032`, `037`; `SCN-KI-033`–`040`; `EV-KI-A-037`, `EV-KI-A-048`.
- [x] `PS-014` Every required coverage case has one unique ID and exactly one
  planned executable registration. Evidence: the existing manifests plus the
  literal 34-ID KI-R5 manifest and matrix; `EV-KI-A-037`, `EV-KI-A-048`.
- [x] `PS-015` Acceptance requires exact required/registered/executed case-set
  equality, zero required skips, and independently recomputed group/global
  digests. Evidence: `KI-R4-V2`, `V3`, `V6`; `KI-R5-V6`; `EV-KI-A-037`, `EV-KI-A-048`.
- [x] `PS-016` Every applicable critical invariant has a named falsification
  control. Evidence: existing controls plus KI-R5 `NC-01`–`NC-12`; `SCN-KI-034`, `036`–`040`; `EV-KI-A-048`.
- [x] `PS-017` Every test substitute has an exact fidelity boundary or a
  narrowed parity claim. Evidence: `SCN-KI-033`–`040`; `DEC-KI-032`, `037`; `EV-KI-A-048`.
- [x] `PS-018` Accepted tests and fixtures have explicit immutability and
  invalidation rules. Evidence: `DEC-KI-032`; `CHG-KI-015`; fixed revisions
  `37a0e020...077213cc`; KI-R5 affected-W4/W5 supersession and W6 invalidation
  are `DEC-KI-037`, `CHG-KI-025`, `EV-KI-A-048`.
- [x] `PS-019` Frozen final gates are exact, risk-proportionate, and bounded
  for stateful/costly suites. Evidence: `KI-R4-V2`–`V5`; database migration is
  one schema/one run and whole-window gates are not repeated per leaf; KI-R5
  gates are `KI-R5-V1`–`V7`, `DEC-KI-037`, `EV-KI-A-048`.
- [x] `PS-020` Handoff evidence must record counts, skips, duplicates,
  unexpected/unactivated IDs, negative-control outcomes, and independently
  recomputed digests. Evidence: `KI-R4-H2`, `KI-R4-V6`, `KI-R5-H2`, `KI-R5-V6`, `EV-KI-A-048`.

### 4.6 Window and agent-boundary closure

- [x] `PW-001` Dependency DAG is acyclic and complete. Evidence: A4 Section 1, `EV-KI-A-009`, `EV-KI-A-033`, `EV-KI-A-036`, `EV-KI-A-037`, `EV-KI-A-048`
- [x] `PW-002` Every window establishes one coherent capability. Evidence: all headers including `KI-R5`; `EV-KI-A-048`
- [x] `PW-003` Every task contains all fifteen F3 fields. Evidence: `EV-KI-A-010`, `EV-KI-A-033`, `EV-KI-A-035`, `EV-KI-A-036`, `EV-KI-A-037`, `EV-KI-A-048`
- [x] `PW-004` Every task has one complete mechanical trace. Evidence: A8; `EV-KI-A-010`, `EV-KI-A-033`, `EV-KI-A-035`, `EV-KI-A-036`, `EV-KI-A-037`, `EV-KI-A-048`
- [x] `PW-005` Every window has exact write/read/action/prohibition scope. Evidence: all window headers
- [x] `PW-006` Shared-file ownership is symbol-specific and ordered. Evidence: relevant headers including `KI-R5`; KI-R4/R5 require one canonical file per sequential leaf; `EV-KI-A-048`.
- [x] `PW-007` Default assignments authorize exactly one window. Evidence: all headers; `DEC-KI-025`
- [x] `PW-008` Successor reservation and `may_start_successor` are explicit. Evidence: all headers
- [x] `PW-009` Handoff verifies actual diff against scope. Evidence: every `H3`
- [x] `PW-010` No successor task is required for predecessor acceptance. Evidence: `EV-KI-A-009`
- [x] `PW-011` Every implementation, verification, and handoff action is a checkbox. Evidence: A4 Section 2
- [x] `PW-012` Every checked planning box cites resolvable evidence. Evidence: `EV-KI-A-011`, `EV-KI-A-048`

### 4.7 Traceability and change control

- [x] `PT-001` Every requirement has a complete A8 trace. Evidence: A8 through Section 7; `EV-KI-A-012`, `EV-KI-A-033`, `EV-KI-A-036`, `EV-KI-A-037`, `EV-KI-A-048`
- [x] `PT-002` Every source-set member has exactly one plan owner and assertion. Evidence: A8 source/target closure; `EV-KI-A-006`
- [x] `PT-003` Every planned member has a requirement and source/target anchor. Evidence: A8; task blocks
- [x] `PT-004` Evidence is append-only and cannot authorize behavior. Evidence: A6 authority statement
- [x] `PT-005` Revision/changelog and invalidation rules are present. Evidence: A7 through `CHG-KI-025`; `DEC-KI-037`; `EV-KI-A-048`
- [x] `PT-006` Active-state concurrency/version checks are specified. Evidence: all P1/H5; `AUTH-KI-002/003`
- [x] `PT-007` New task, scenario, assignment, evidence, state, and change IDs
  are unique. Evidence: A7 rules; `EV-KI-A-013`; `CHG-KI-012`, `025`; `EV-KI-A-048`. The requester
  explicitly resumed the same unaccepted KI-R2 lifecycle rather than allocating
  a new window; the disclosed exception is confined to that window label.

### 4.8 Audit and readiness

- [x] `PR-001` Forward simulation passed for normal and every specified failure boundary. Evidence: `EV-KI-A-014`, `EV-KI-A-032`, `EV-KI-A-035`, `EV-KI-A-036`, `EV-KI-A-037`, `EV-KI-A-048`
- [x] `PR-002` Backward simulation traced public/terminal fields to evidence/formulas. Evidence: `EV-KI-A-015`, `EV-KI-A-032`, `EV-KI-A-035`, `EV-KI-A-036`, `EV-KI-A-037`, `EV-KI-A-048`
- [x] `PR-003` Reachable-set audit passed at authoring/source parity. Evidence: `EV-KI-A-016`, `EV-KI-A-048`
- [x] `PR-004` Payload no-guessing audit passed for the supported one-shape contract. Evidence: `EV-KI-A-004`, `SRC-KI-034`–`036`, `PAY-KI-008`, `EV-KI-A-048`
- [x] `PR-005` Anti-vacuity and negative-control audit passed as a specification. Evidence: `EV-KI-A-017`, `EV-KI-R3-02`, `EV-KI-A-037`, KI-R5 `NC-01`–`NC-12`, `EV-KI-A-048`
- [x] `PR-006` Environment/runtime/deployment parity audit passed. Evidence: `EV-KI-A-029`; representative emitted backend (Node 24 ESM import of `@noble/hashes/sha2.js`, correctness, sizes 889,457 B uncompressed / 205,571 B gzipped-tree, startup) and frontend (Next 16.2.12 route-complete build plus chart dependency load, sizes 21,078,923 B + 64,697 B uncompressed / 3,118,028 B gzipped-tree, startup) proofs exist. Live deployed parity remains a later `KI-W8` acceptance claim per D10.
- [x] `PR-007` Scale and competing-owner falsification passed as a specification. Evidence: `EV-KI-A-018`, `EV-KI-A-032`, `EV-KI-A-033`, `EV-KI-A-035`, `EV-KI-A-036`, `EV-KI-A-037`, `EV-KI-A-048`; `SCN-KI-022`–`040` close exact-expiry, full-monitor, retry, recovery, enforcement, build-isolation, maximum-selection, and equal-key handoff schedules.
- [x] `PR-008` Mistake-derived conformance audit passed as a specification. Evidence: `EV-KI-A-019`, `EV-KI-A-032`, `EV-KI-A-035`, `EV-KI-A-036`, `EV-KI-R3-02`, `EV-KI-A-037`, `EV-KI-A-048`
- [x] `PR-009` Mechanical checklist lint has no missing IDs, links, evidence,
  scopes, and matching A5 hashes. Evidence: `EV-KI-A-032` for the base
  sequence; `EV-KI-A-033` for KI-R2; `EV-KI-A-035` for reopened W3;
  `EV-KI-A-036` for KI-R3; `EV-KI-A-037` for KI-R4 authoring;
  `EV-KI-R4-02`, `EV-KI-A-038`, and A5 state 99 for KI-R4 acceptance/W4
  authoring; `EV-KI-A-048`–`051` and A5 state 111 for KI-R5 readiness and W6 invalidation.
- [x] `PR-010` No implementation-affecting choice is delegated. Evidence: `EV-KI-A-008`, `EV-KI-A-032`, `EV-KI-A-033`, `EV-KI-A-035`, `EV-KI-A-036`, `EV-KI-A-037`, `EV-KI-A-048`
- [x] `PR-011` Enforcement lint rejects missing, duplicate, skipped, filtered,
  unactivated, or unexpected coverage cases. Evidence: `KI-R4-T3`,
  `KI-R4-V2`, `KI-R4-V3`, `KI-R4-V6`; KI-R5 literal manifest,
  `KI-R5-V6`; `EV-KI-A-037`, `EV-KI-A-048`.
- [x] `PR-012` Substitute-fidelity and accepted-test invalidation audits pass
  as a specification. Evidence: `DEC-KI-032`; `SCN-KI-033`–`035`;
  `CHG-KI-015`, `025`; `EV-KI-A-037`, `EV-KI-A-048`.

### 4.9 Recursive window-agent closure

- [x] `RW-001` The parent assigns one named window agent and no leaf agent.
  Evidence: `ASG-KI-R4-WA-01`; A5 state 98.
- [x] `RW-002` S1/S2/S3 paths and non-overlapping authorities are exact.
  Evidence: KI-R4 header; `DEC-KI-032`.
- [x] `RW-003` The delegable implementation set is exactly eight canonical
  files with a pinned sorted-LF digest; no wildcard or directory ownership is
  present. Evidence: KI-R4 header; `EV-KI-A-037`.
- [x] `RW-004` Initial decomposition requires exactly eight sequential
  single-file leaves and forbids a leaf from changing zero or two files.
  Evidence: KI-R4-P4/P5; sub-window standard Sections 3 and 7.
- [x] `RW-005` All 44 mandatory `SW-*` boxes must be copied and evidenced in
  S1/S3 before parent decomposition approval. Evidence: KI-R4-P4.
- [x] `RW-006` Parent decomposition review is a real pre-execution gate; S2
  cannot become `READY` and no leaf may be assigned before approval is recorded.
  Evidence: KI-R4-P4/P5; A5 state 98.
- [x] `RW-007` Parent↔window-agent↔leaf communication is strictly adjacent;
  leaf agents cannot update S1/S2/S3 or parent artifacts. Evidence: KI-R4
  header/H3; sub-window standard Sections 1.4 and 3.
- [x] `RW-008` The initial integration assessment is fully authored, owns zero
  implementation files, and runs costly/stateful gates once after leaf edits
  freeze. Evidence: KI-R4-V1–V6.
- [x] `RW-009` Any implementation correction is a new append-only sequential
  one-file corrective sub-window followed by a new window-agent assessment;
  the window agent may not repair files directly. Evidence: KI-R4 header;
  sub-window standard Sections 10 and 12.
- [x] `RW-010` Window-agent approval stops at `READY_FOR_PARENT_REVIEW`; only
  the parent may accept KI-R4 and assign KI-W4. Evidence: KI-R4-H1–H4.

### 4.10 KI-W4 recursive and enforcement closure

- [x] `RW4-001` KI-R4 and cumulative KI-W3 have an independent parent
  acceptance record at the requester-owned commit; W4 consumes no dirty
  implementation state. Evidence: `EV-KI-R4-02`.
- [x] `RW4-002` W4 is one coherent owner-API/query-review handoff capability,
  and every behavior choice is locked in `DEC-KI-033`. Evidence:
  `EV-KI-A-038`.
- [x] `RW4-003` The delegable set is exactly ten canonical files with no
  wildcard and the sorted-LF digest `fe48d14e…`. Evidence: W4 header;
  `EV-KI-A-038`.
- [x] `RW4-004` The set is partitioned without overlap across four complete
  15-field tasks: 4 + 1 + 2 + 3 files. Evidence: W4 T1–T4; A8 Section 6.
- [x] `RW4-005` The future window agent owns only the three named W4
  coordination artifacts and must delegate sequential one-file leaves; it may
  not edit implementation files. Evidence: W4 header/P5/P6/H1–H6.
- [x] `RW4-006` The literal enforcement manifest contains 34 unique IDs in
  exact 8/6/8/6/6 groups and has normative digest `86810ce8…`. Evidence: W4
  literal manifest; `EV-KI-A-038`.
- [x] `RW4-007` Every W4 case has exact input, action, activation witness,
  result, forbidden operation, control, parity and registration. Evidence: W4
  behavioral coverage matrix; A8 Section 6.
- [x] `RW4-008` All eighteen critical invariants have defect-injecting controls
  that first pass unchanged, then falsify, then pass fresh. Evidence:
  `W4-NC01`–`NC18`; `EV-KI-A-038`.
- [x] `RW4-009` Component substitutes have explicit fidelity limits and SQL
  ownership/CAS/rollback claims require D01–D06 real-Prisma evidence. Evidence:
  W4 substitute-fidelity table.
- [x] `RW4-010` Frozen gates are risk-proportionate: one non-DB run, one
  isolated-schema DB run, one full regression and one secret scan; no
  Prisma/build/full-DB/live repetition is authorized. Evidence: W4 V2–V7.
- [x] `RW4-011` Existing product-only query behavior remains the legacy branch;
  research-backed non-product queries use the separately specified validator,
  lineage and confirmation branch. Evidence: `DEC-KI-033`; W4 Q01–Q08.
- [x] `RW4-012` W4 remains unassigned until a later explicit A5 CAS; this
  authoring pass cannot create S1/S2/S3 or start a leaf. Evidence: A5 state 99;
  `EV-KI-A-038`.

### 4.11 KI-R5 corrective authoring closure

- [x] `RR5-001` The nine reproduced W4/W5 defects each have one observed
  source, one locked decision, one task owner, one executable case family and
  one frozen gate. Evidence: `SRC-KI-034`; `DEC-KI-034`–`037`; A8 Section 7;
  `EV-KI-A-048`.
- [x] `RR5-002` `PAY-KI-008` fixes one minimal selection input union, numeric
  contract version, strict unknown-key rejection and a 262144-byte ceiling;
  no implementer chooses a second wire shape. Evidence: `SRC-KI-035/036`;
  `DEC-KI-034`; `EV-KI-A-048`.
- [x] `RR5-003` The 18 canonical implementation/test paths are literal,
  non-wildcard, starting-hashed and protected by sorted-LF digest
  `efc82a884d09561ed27be3513ca6898f0ab311dbe56cf46e9c2c241492560077`.
  Evidence: KI-R5 header; `EV-KI-A-048`.
- [x] `RR5-004` T1–T5 each contain all fifteen task fields and assign every
  shared symbol, failure branch and test registration exactly once. Evidence:
  KI-R5 T1–T5; A8 Section 7; `EV-KI-A-048`.
- [x] `RR5-005` Saved-draft equality, ambiguous retry, definitive failure,
  reload, cancel and equal-key concurrent publication transitions are fully
  specified. Evidence: `DEC-KI-035`; `SCN-KI-037/038`; `EV-KI-A-048`.
- [x] `RR5-006` Filter and CSV rules name the exact field corpus, AND/every
  predicate, ordering, textual-cell neutralization and numeric preservation.
  Evidence: `DEC-KI-036`; `SCN-KI-039`; `EV-KI-A-048`.
- [x] `RR5-007` The literal 34-case manifest has exact five-group membership,
  exact registrations, exact per-group digests and global digest
  `507186e7489a3f9eec18eb5de78692dbc55a8d1d2d106544aa4295a98ac9be60`.
  Evidence: KI-R5 T5/matrix; `EV-KI-A-048`.
- [x] `RR5-008` Every critical R5 claim has a named pass-before/falsify/
  restore control, exact safe mutation, unchanged oracle/failure and explicit
  substitute-fidelity boundary. Evidence: literal `R5-NC-01`–`R5-NC-12`
  table; `DEC-KI-037`; `EV-KI-A-048`–`050`.
- [x] `RR5-009` Frozen gates run costly/stateful suites only once after the
  final edit freeze and require exact set equality, zero required skips and
  zero residual disposable schema. Evidence: KI-R5 V1–V7/H1–H6;
  `EV-KI-A-048`.
- [x] `RR5-010` The window-agent boundary owns only S1/S2/S3, requires
  sequential one-file leaves and reserves implementation corrections to new
  one-file corrective leaves. Evidence: KI-R5 header/P4/P5/H5/H6; sub-window
  standard; `EV-KI-A-048`.
- [x] `RR5-011` The exact 18 mutable accepted W4/W5 oracles, 15 browser reruns,
  stable registrations and immutable remainder are locked; the unexecuted
  state-108 KI-W6 decomposition is explicitly
  invalidated; W6 now depends on accepted KI-R5 and cannot reuse its prior
  S1/S2/S3. Evidence: `SRC-KI-037`; `DEC-KI-037`; `CHG-KI-025`–`027`; A8 Section 7; `EV-KI-A-051`.
- [x] `RR5-012` This parent pass authors and reserves KI-R5 only; it does not
  implement, decompose, assign a leaf or begin KI-W6. Evidence: A5 state 111;
  `EV-KI-A-048`–`051`.

### 4.12 KI-W6 reauthoring and enforcement closure

- [x] `RW6-001` The source contradiction has one observed record and one locked
  resolution: preserve API `statusUrl`, route the browser only from encoded
  `handoff.run.runId`, and supersede only R5-FIN-01's destination assertion.
  Evidence: `SRC-KI-038`; `DEC-KI-038`; `EV-KI-A-081`.
- [x] `RW6-002` The delegable set is exactly five canonical paths with three
  absence states, two starting hashes and sorted-LF digest
  `d28ae17864073639580d7650bb03c03474d5370a5034b632cf412e1e3cf3d0bb`;
  all unlisted source and history are read-only. Evidence: W6 header;
  `EV-KI-A-081`.
- [x] `RW6-003` T1–T5 each contain all fifteen fields and fix exact interfaces,
  expressions, exports, fixture schema, command surface, cleanup and non-goals;
  no implementation choice is left to decomposition. Evidence: W6 T1–T5;
  `DEC-KI-038`.
- [x] `RW6-004` The causal path is one connected browser→emitted Next→installed
  auth client→proxy→backend→Prisma/worker→run workspace→probe→downstream chain;
  browser API interception and disconnected-test relabelling are forbidden.
  Evidence: `SRC-KI-039`; `DEC-KI-038`; `SCN-KI-018`.
- [x] `RW6-005` The literal matrix contains 26 unique cases in exact 3/13/4/6
  groups with independently computed group/global digests and one registration
  owner; required/registered/executed/activated equality is mandatory. Evidence:
  `DEC-KI-038`; W6 matrix; `EV-KI-A-081`.
- [x] `RW6-006` Thirteen named captured-data controls cover navigation, auth,
  topology, parsing, fencing, handoff, probes, Neon readiness, causal routing,
  set defects, activation/control vacuity, substitute inflation and obsolete
  dependencies using pass→fail→fresh-pass. Evidence: W6 NC table;
  `DEC-KI-038`.
- [x] `RW6-007` Every substitute has an explicit maximum claim; isolated Prisma
  supplies SQL evidence, emitted Next/Chrome supplies frontend evidence, and
  local auth/provider/memory cloud boundaries cannot claim live/deployed parity.
  Evidence: W6 substitute ledger; `SRC-KI-039`; `DEC-KI-038`.
- [x] `RW6-008` The maximum-path counts are literal and causal: 19 keyword
  calls, 300/200/100, `$0.49200000`, 100 probes, 1,000 occurrences, 100
  discovery tasks and 1,000 stable downstream lead tasks; lead scraping is out
  of scope. Evidence: `DEC-KI-024/038`; `SCN-KI-018`.
- [x] `RW6-009` Frozen gates use one frontend check/build, one stateful emitted
  browser/schema run, one backend regression, one secret scan and read-only
  conformance; full DB suites, duplicate builds, handler builds and full W5
  browser reruns are prohibited. Evidence: W6 V1–V6; `DEC-KI-038`.
- [x] `RW6-010` Standing escalation and proven-environment recovery are explicit
  while behavioral failures remain failures; invalidation is file/gate-specific.
  Evidence: W6 header/V2–V4; parent standard E8.1; `EV-KI-A-081`.
- [x] `RW6-011` Recursive authority names three fresh `REAUTHORED` artifacts,
  requires sequential one-file leaves and one window-agent integration
  assessment, and keeps leaf↔parent communication and parent-artifact edits
  prohibited. Evidence: W6 header/P1/P5/H3/H5; `SRC-KI-040`.
- [x] `RW6-012` The state-108 decomposition remains immutable invalidated
  history; this parent pass changes only A2–A8/A5 documentation, assigns no
  agent, creates no S1/S2/S3 and performs no implementation/test/database/build/
  browser/provider/AWS action. Evidence: `SRC-KI-040`; `CHG-KI-056`;
  `EV-KI-A-081`.

### 4.13 KI-W6 in-flight shortlist correction readiness

- [x] `RW6C-001` The 300-row result is classified as a production aggregation
  defect against A1/DEC-KI-038, not a test-oracle defect. Evidence:
  `SRC-KI-041`; `DEC-KI-039`; `EV-KI-A-088`.
- [x] `RW6C-002` The remedy is mechanically fixed: read the immutable shortlist,
  project per-seed expansion and US metrics by exact normalized membership,
  require set equality, and preserve every provider/task/artifact/public
  contract. Evidence: `DEC-KI-039`; `KI-W6-CT1`; `EV-KI-A-088`.
- [x] `RW6C-003` The expanded W6 set is exactly seven paths with digest
  `c3bfe436aba49d52de26298ac74eb30e061d392144dfffbb6954ee792c908bdc`;
  C104 and C105 each own one added file and I102 owns no implementation file.
  Evidence: `KI-W6-PCA-01`; `EV-KI-A-088`.
- [x] `RW6C-004` Both corrective tasks contain all fifteen fields, exact
  intermediate order, preserved behavior, failure/replay outcomes, local
  checks, and successor boundaries. Evidence: `KI-W6-CT1/CT2`;
  `SCN-KI-041`; `EV-KI-A-088`.
- [x] `RW6C-005` Enforcement membership remains the existing 26 cases and 13
  controls: `W6-FLOW-05`/`W6-NC-05` own the final-row invariant and the focused
  component regression cannot create a duplicate registration. Evidence:
  `DEC-KI-039`; corrected gate schedule; `EV-KI-A-088`.
- [x] `RW6C-006` Gate invalidation is risk-proportionate: reuse the unchanged
  frontend build by full-input hashes; rerun the focused component, causal V3,
  backend regression/secrets, and worker package only after final backend
  freeze; never run the full DB or seven-handler build suites. Evidence:
  `KI-W6-CV1`–`CV6`; `EV-KI-A-088`.
- [x] `RW6C-007` The worker source change invalidates the old service hash, so
  W7 must consume the newly deterministic two-build package/size/startup proof
  rather than the unchanged-hash claim from original V6. Evidence:
  `KI-W6-CV5/CV6`; `DEC-KI-039`; `EV-KI-A-088`.
- [x] `RW6C-008` Recursive authority stops before leaf dispatch: only the
  window agent may append C104/C105/I102 to S1/S2/S3 and return them for parent
  decomposition review; KI-W7 remains prohibited. Evidence: A5 state 149;
  `CHG-KI-061`; `EV-KI-A-088`.

#### `KI-W6` second in-flight corrective amendment — contract-valid component fixture

This `KI-CL-22` amendment supersedes only C105's scaffold fingerprint and
one-seed SCN-KI-041 fixture shape plus failed I102/CV1. C104 production source,
the existing seven-path W6 scope/digest, 26 case IDs, 13 controls, frontend
build reuse, causal V3 oracle, provider economics, schemas, and every public
interface remain unchanged. `SRC-KI-042` and `DEC-KI-040` resolve the parent
choice: preserve the stage-manifest identity and 60-keyword-per-seed contract.

```yaml
window_id: KI-W6
correction_id: KI-W6-PCA-02
trigger: SRC-KI-042
governing_decision: DEC-KI-040
implementation_subwindow: KI-W6-C106
integration_assessment: KI-W6-I103
write_scope: [email_scraper/test/keyword-intelligence-worker-flow.test.js aggregationScaffold and SCN-KI-041 only]
starting_file_digest: f549f9ac16e2c31957dd3a03b11d54da15972f4af23ebcfecb6f8c16f8955d9f
starting_repository_change_set_digest: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
parent_scope_expansion: false
coverage_membership_change: false
production_change: false
successor: STOP_LOCAL
successor_reserved_for: parent
may_start_successor: false
```

The requester explicitly authorizes the window agent to append C106 and I103
to S1/S2/S3 from this literal parent block, dispatch C106, independently review
it, and continue through I103 without another parent-decomposition round. This
is not permission to reinterpret the block: before dispatch the window agent
must certify that its S1 copy has the same file, formulas, checks, order,
prohibitions and gates. Any divergence, new decision or scope expansion stops.

##### Task block `KI-W6-CT3` / sub-window `KI-W6-C106`

1. **Task:** correct only the existing component scaffold and SCN-KI-041 so
   their stored identities and maximum candidate shape satisfy the unchanged
   production schemas.
2. **Requirements/decisions:** `REQ-KI-001`, `REQ-KI-002`, `REQ-KI-003`,
   `REQ-KI-023`, `REQ-KI-024`, `INV-KI-004`, `INV-KI-005`, `INV-KI-014`,
   `DEC-KI-024`, `DEC-KI-038`, `DEC-KI-039`, `DEC-KI-040`, `SRC-KI-042`.
3. **Source:** current SHA-256
   `f549f9ac16e2c31957dd3a03b11d54da15972f4af23ebcfecb6f8c16f8955d9f`;
   R28 proves five R3 market cases fail on task-vs-stage fingerprint and
   SCN-KI-041 fails the strict 60-per-seed parser.
4. **Target:** only
   `email_scraper/test/keyword-intelligence-worker-flow.test.js`, limited to
   `aggregationScaffold` support statements and the one existing SCN-KI-041
   block. No other R3/R4 test, registration or assertion changes.
5. **Private interface:** add option `bySeed = null`. Define exactly
   `expansionBySeed = bySeed ?? [{ seed: "seed one", keywords: candidates }]`
   and `seeds = expansionBySeed.map((entry) => entry.seed)`. No export or
   production interface changes.
6. **Stage/task shape:** set expansion-stage expected/terminal/succeeded counts
   to `seeds.length * 2`. Construct exactly two ordered expansion tasks per seed
   in seed-index order, `suggestions` then `related`, using that seed in the
   request and task-input payload. Default callers therefore retain two tasks;
   the maximum fixture has ten.
7. **Expansion manifest:** retain its existing strict schema and stage
   fingerprint. Store `seeds`, `bySeed: expansionBySeed`, and the existing
   ordered `candidates`. Derive each candidate's `seeds` array by scanning
   `expansionBySeed` in seed order and retaining every entry whose exact
   `keywords` array contains that candidate; zero supplying seeds is invalid
   through the existing schema. Do not collapse all candidates to one seed.
8. **Shortlist manifest identity:** after `[anchorTask]` exists, compute exactly
   `anchorStageInputFingerprint = keywordStageInputFingerprint({ researchId,
   generation, stage: "anchor_screen", tasks: [anchorTask] })`. Use that value
   for both `shortlistManifest.inputFingerprint` and the shortlist
   `putImmutable.inputFingerprint`. Keep the anchor task artifact on
   `anchorTask.inputFingerprint`; these identities are deliberately different.
9. **Maximum fixture:** replace the one-seed candidate expression with exactly
   five seeds `seed 1`…`seed 5`. For each seed, its 60-keyword member is
   `[seed, ...59 strings]`, where string `n` is
   `` `${seed} candidate ${String(n + 1).padStart(2, "0")}` `` for zero-based
   `n=0..58`. `candidates = expansionBySeed.flatMap(entry => entry.keywords)`;
   assert five members, every member length 60, candidate length and distinct
   count 300; `shortlist = candidates.slice(0, 200)`.
10. **Scenario assertions:** call the actual production aggregate path with
    `{stage:"market_overview", candidates, shortlist, bySeed: expansionBySeed}`
    and preserve the existing `published`, result 200, default selection 100,
    normalized shortlist equality and zero escaped-key assertions.
11. **Failure/replay/concurrency:** existing R3/R4 outcome, lease, lost-owner,
    replay and no-dispatch cases remain unchanged and must all pass. A task
    fingerprint in the shortlist manifest, one `bySeed` member over 60, wrong
    stage counts, missing provenance, duplicate/leaked result key or changed
    existing assertion fails acceptance.
12. **Operations/bounds:** in-memory test only; five seeds, 60 each, 300
    candidates, 200 shortlist/result, 100 default. Zero database, subprocess,
    HTTP, provider, AWS, production, artifact-file, package or schema write.
13. **Checks:** from `email_scraper/`, run C106-C1
    `node --check test/keyword-intelligence-worker-flow.test.js`, then C106-C2
    `node --test --test-isolation=none test/keyword-intelligence-worker-flow.test.js`.
    Require exit 0, 37 tests pass, zero fail/skip, R3-G11–G15 pass, SCN-KI-041
    executes once, and exact 5/60/300/200/200/100 witnesses. Expected workspace
    write set is empty. The prior 30/7 result cannot be reused.
14. **Output:** corrected test substitute consumed by I103; C105's failed
    fingerprint/one-seed evidence is superseded, while its other accepted
    scaffold work remains.
15. **Non-goals:** no `service.js`, contract, key, config, repository, handler,
    frontend, browser harness, fixture manifest, case ID/digest, timeout,
    provider, database, AWS, commit, push or KI-W7 change.

```yaml
subwindow_id: KI-W6-C106
type: CORRECTION
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-02
assigned_agent: UNASSIGNED
predecessors: [KI-W6-I102 PARENT_BLOCKED]
successor_reserved_for: WINDOW-AGENT
writable_file: email_scraper/test/keyword-intelligence-worker-flow.test.js
file_operation: MODIFY
starting_file_digest: f549f9ac16e2c31957dd3a03b11d54da15972f4af23ebcfecb6f8c16f8955d9f
starting_repository_change_set_digest: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
read_only_scope: [KEYWORD_INTELLIGENCE_PRODUCT_CONTRACT.md, KEYWORD_INTELLIGENCE_DECISION_LEDGER.md §DEC-KI-040, KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md §KI-W6 second in-flight corrective amendment, ACTIVE_EXECUTION_STATE.md, email_scraper/src/aws-pipeline/keyword-intelligence/service.js::readManifest, email_scraper/src/aws-pipeline/keyword-intelligence/contracts.js::keywordExpansionManifestSchema, email_scraper/src/aws-pipeline/keyword-intelligence/keys.js::keywordStageInputFingerprint]
authorized_actions: [perform KI-W6-CT3 in the one writable file, run C106-C1 and C106-C2 once, return evidence only to the window agent]
prohibited_actions: [second-file edit, existing R3/R4 assertion or registration edit, production schema package config timeout provider database AWS commit push parent communication subdelegation successor or KI-W7 action]
may_start_successor: false
```

- [ ] `C106-P1` Pins, assignment, clean baseline and predecessor match.
- [ ] `C106-P2` The attributable changed-file set is exactly the writable file.
- [ ] `C106-T1` Apply all ordered CT3 transformations and no other edit.
- [ ] `C106-V1` Run C106-C1/C2 once with the exact witnesses and zero skips.
- [ ] `C106-H1` Return diff, ending digest, commands and outcomes to the window agent.
- [ ] `C106-H2` Confirm zero prohibited/external/successor action and stop for review.

##### Integration assessment `KI-W6-I103`

I103 is owned personally by the window agent, writes no implementation file,
and begins only after independent C106 acceptance. It supersedes failed I102
and uses these exact ordered gates:

- [ ] `KI-W6-CV7` From `email_scraper/`, once run
  `node --check src/aws-pipeline/keyword-intelligence/service.js` followed by
  `node --test --test-isolation=none test/keyword-intelligence-worker-flow.test.js`.
  Require 37 pass, zero fail/skip, R3/R4 green and exact SCN-KI-041
  5/60/300/200/200/100 activation.
- [ ] `KI-W6-CV8` Reuse the passed frontend build only if frontend porcelain is
  empty and HEAD remains `a39663c8f99d9cc3c4aa1301ff088d5f4a24e7fd`; otherwise stop for dependency
  adjudication. Do not rebuild.
- [ ] `KI-W6-CV9` From `frontend/`, once run
  `ALLOW_DATABASE_TESTS=true KI_W6_SKIP_BUILD=1 node test/browser/keyword-intelligence-e2e.mjs`
  with the existing isolated `TEST_DATABASE_URL` sourced without logging.
  Require the unchanged 26-case/13-control certificate, exact 19 calls, 23
  keyword objects, 42 sends, `$0.49200000`, five seeds, 300 anchor, 200
  shortlist/result/UI, default 100, complete cleanup and zero residual schema.
- [ ] `KI-W6-CV10` From `email_scraper/`, once run `npm test`, then
  `npm run check:secrets`; require zero failures and clean scan. Do not opt into
  the full database suite.
- [ ] `KI-W6-CV11` From `email_scraper/`, run
  `node scripts/build-keyword-worker.js` exactly twice; require identical ZIP
  hashes, preserved siblings, no forbidden/stale members, ZIP ≤45 MiB,
  unzipped ≤200 MiB and cold-imported function `handler`; then run once
  `node --test --test-isolation=none test/aws-pipeline-packaging.test.js` with
  zero failures. Do not run seven-handler build/measure.
- [ ] `KI-W6-CV12` Recompute the unchanged seven-path digest, current hashes,
  exact 26-ID/group/global equality, 13 controls, substitute limits, privacy,
  scope and W7 handoff. Require only C104 and the C105/C106-owned test file to
  differ from the five accepted initial hashes and no out-of-scope source.
- [ ] `KI-W6-CH3` Record C106 acceptance, I103 gates, superseded I102 failure,
  requester commit provenance, exact final files/digests and one
  `WINDOW-AGENT-INTEGRATION-PASS` certificate.
- [ ] `KI-W6-CH4` Stop `READY_FOR_PARENT_REVIEW`; do not begin KI-W7.

Sandbox or channel invalidation permits the standing one identical escalated
recovery. An observable product/test failure is not such an invalidation. If
C106 and all I103 gates pass, the window agent continues through CH3/CH4
without another parent prompt. A new decision, scope expansion or unresolved
contract contradiction stops; a mechanically determined same-scope defect
uses the standard's new one-file corrective-subwindow path.

##### Second-correction readiness

- [x] `RW6D-001` R28 activated both failures and stopped before later gates.
- [x] `RW6D-002` DEC-KI-040 preserves production contracts and fixes the test substitute.
- [x] `RW6D-003` C106 has one file, literal baseline, formulas and bounds.
- [x] `RW6D-004` Five × 60 is schema-valid and totals the required 300.
- [x] `RW6D-005` Stage and task fingerprints remain distinct and exact.
- [x] `RW6D-006` Coverage membership/digests remain unchanged.
- [x] `RW6D-007` I103 gates are ordered, bounded and invalidation-aware.
- [x] `RW6D-008` Authority stops before KI-W7 and grants no external action.

#### `KI-W6` third in-flight corrective amendment — page-aware selection swap

This `KI-CL-23` amendment supersedes only the accepted S105
`swapOneSelectionItemViaUi` helper and failed I103/CV9 result `EV-KI-W6-R33`.
It changes no product source, contract, payload, schema, package, case/control
membership, case digest, provider operation, database behavior, or production
build input. `SRC-KI-043` and `DEC-KI-041` classify the failure as a causal
browser-harness navigation defect: the real 200-row table renders 25 rows per
page and does not promise checked and unchecked rows on the same page.

```yaml
window_id: KI-W6
correction_id: KI-W6-PCA-03
trigger: SRC-KI-043
governing_decision: DEC-KI-041
implementation_subwindow: KI-W6-C107
integration_assessment: KI-W6-I104
write_scope: [frontend/test/browser/keyword-intelligence-e2e.mjs::swapOneSelectionItemViaUi only]
starting_file_digest: fc88c77ebb1bf8f62cafa600afbe5d789cd7a688899a552cff93a0ec0ada0a8f
starting_frontend_head: a39663c8f99d9cc3c4aa1301ff088d5f4a24e7fd
starting_frontend_change_set_digest: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
parent_scope_expansion: false
coverage_membership_change: false
production_or_build_input_change: false
successor: STOP_LOCAL
successor_reserved_for: parent
may_start_successor: false
```

The window agent may append the literal C107/I104 blocks to S1/S2/S3, certify
exact transcription, dispatch C107, independently review it, and personally
continue through I104 without another parent-decomposition review. A differing
algorithm, second file, new case/control, changed oracle, production edit, or
scope expansion stops for parent disposition. The window agent does not edit
A1–A8 and does not communicate with the leaf through the parent.

##### Task block `KI-W6-CT4` / sub-window `KI-W6-C107`

1. **Task:** repair only the private causal-harness selection-swap helper so it
   uses the real table pagination to replace one selected keyword with one
   different unselected keyword.
2. **Requirements/decisions:** `REQ-KI-007`, `REQ-KI-008`, `REQ-KI-009`,
   `REQ-KI-014`, `REQ-KI-015`, `INV-KI-010`, `DEC-KI-034`, `DEC-KI-035`,
   `DEC-KI-038`, `DEC-KI-041`, `SRC-KI-043`.
3. **Source:** current SHA-256
   `fc88c77ebb1bf8f62cafa600afbe5d789cd7a688899a552cff93a0ec0ada0a8f`;
   R33 proves the same-page `checkedRow && uncheckedRow` precondition fails
   after the real 200-row/default-100 result is visible.
4. **Target:** only
   `frontend/test/browser/keyword-intelligence-e2e.mjs`, limited to
   `swapOneSelectionItemViaUi`. Preserve both existing call sites and every
   registry, oracle, control, certificate, cleanup and diagnostic symbol.
5. **Private interface:** keep `swapOneSelectionItemViaUi` async with no
   parameters. It may return a private diagnostic object but neither caller may
   depend on it. Keep the exact existing checkbox selector. Define no export,
   product hook, route, payload, config, package or fixture interface.
6. **Ordered algorithm:** (a) wait for nonempty matching checkboxes; (b) read
   their ordered `{label,checked}` state on freshly mounted page 1, recording
   the first nonempty checked label and first different nonempty unchecked
   label with their integer page numbers; (c) if either is absent, capture the
   ordered newline-joined checkbox-label signature, require within the
   keyword-table surface an enabled `Next` button, click it, wait for the
   signature to change, increment the local page, and repeat through page 8;
   (d) require both recorded labels and different values; (e) navigate from the
   current page to the checked row's recorded page using the exact number of
   enabled `Prev` or `Next` clicks, requiring a changed checkbox signature after
   each; (f) click the checked row and wait until that same checkbox is
   unchecked; (g) navigate by the same direction/page-difference rule to the
   unchecked row's recorded page; (h) click the recorded distinct unchecked row
   and wait until it is checked; (i) wait until the selection-review surface
   contains the exact text `100 of 200 selected`.
7. **Operation order/boundary:** exactly two user-equivalent checkbox change
   events occur per invocation: one removal before one addition. Pagination
   clicks may occur only between them. Save/CAS/handoff remain in the existing
   callers after this helper returns. This test-only navigation changes no
   durable or external boundary and performs no direct API/database mutation.
8. **Identity:** checkbox labels locate rendered controls only; they do not
   become selection identity. The production checkbox handler continues to use
   the row's `itemId`; page signatures are ordered labels used only to observe
   a completed page transition. `addedLabel !== removedLabel` is mandatory.
9. **Failure behavior:** missing/empty/repeated candidate label, either state
   absent by page eight, absent or disabled required `Next`/`Prev`, unchanged
   page signature, failure to observe removal/addition, or final count other
   than 100 throws and prevents save/handoff/certificate.
   No retry, fallback filter, direct state edit, fetch mutation, or assertion
   weakening is permitted.
10. **Bounds/concurrency:** frozen 200 rows, 25 default rows per page, at most
    eight inventoried pages, at most 21 total pagination clicks, exactly two
    checkbox changes, one Chrome process and the existing waits/timeouts. Do
    not increase any timeout or add a browser/process/schema.
11. **Preserved callers:** the pre-handoff W6-FLOW-07 invocation must still
    produce one stale 409 then one successful revision-2 CAS with 100 strict
    items; the post-handoff W6-FLOW-13 invocation must still advance only the
    live research selection while the immutable Run snapshot stays equal.
12. **Forbidden alternatives:** no product component/view-model edit, page-size
    change, recommended filter, arbitrary DOM `checked` assignment, direct
    React state, API-side fabricated draft, removed-row re-addition, row-index
    identity, case/control/manifest edit, build, database, provider or AWS call.
13. **Local checks:** from `frontend/`, run exactly once
    `node --check test/browser/keyword-intelligence-e2e.mjs`, then
    `git diff --check -- test/browser/keyword-intelligence-e2e.mjs`. Require
    exit zero. The leaf runs no browser/build/database/full test command.
14. **Output:** one reviewed page-aware helper consumed by I104. Its final
    digest and exact one-symbol diff are recorded; accepted S105 helper evidence
    is explicitly superseded by C107 review and CV15.
15. **Non-goals:** no production behavior, response shape, persistent state,
    selection count/rank, paging UI, case ID/digest, substitute claim, timeout,
    package, schema, provider economics, commit, push or KI-W7 change.

```yaml
subwindow_id: KI-W6-C107
type: CORRECTION
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-02
assigned_agent: UNASSIGNED
predecessors: [KI-W6-I103 CV9 BLOCKED by EV-KI-W6-R33]
successor_reserved_for: WINDOW-AGENT
writable_file: frontend/test/browser/keyword-intelligence-e2e.mjs
writable_symbol: swapOneSelectionItemViaUi
file_operation: MODIFY
starting_file_digest: fc88c77ebb1bf8f62cafa600afbe5d789cd7a688899a552cff93a0ec0ada0a8f
starting_repository_change_set_digest: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
read_only_scope: [KEYWORD_INTELLIGENCE_PRODUCT_CONTRACT.md, KEYWORD_INTELLIGENCE_DECISION_LEDGER.md §DEC-KI-041, KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md §KI-W6 third in-flight corrective amendment, ACTIVE_EXECUTION_STATE.md, frontend/components/keyword-intelligence/keyword-table.tsx::KeywordTable, frontend/components/keyword-intelligence/research-dashboard.tsx::ResearchDashboard, frontend/lib/keyword-intelligence-view-model.ts::emptyKeywordFilterState/paginate, KEYWORD_INTELLIGENCE_KI_W6_REAUTHORED_SUBWINDOW_EVIDENCE.md::EV-KI-W6-R33]
authorized_actions: [perform KI-W6-CT4 in the one writable symbol, run the two C107 local commands once, return evidence only to the window agent]
prohibited_actions: [second-symbol or second-file edit, browser build database full-test provider AWS production commit push parent communication subdelegation successor or KI-W7 action]
may_start_successor: false
```

- [ ] `C107-P1` Pins, assignment, exact baseline, clean frontend and R33 predecessor match.
- [ ] `C107-P2` The attributable diff is exactly the writable symbol in the one file.
- [ ] `C107-T1` Apply all ordered CT4 behavior and no forbidden alternative.
- [ ] `C107-V1` Run the two local commands once with exit zero.
- [ ] `C107-H1` Return the diff, ending digest, commands and outcomes to the window agent.
- [ ] `C107-H2` Confirm zero prohibited/external/successor action and stop for independent review.

##### Integration assessment `KI-W6-I104`

I104 is owned personally by the window agent, writes no implementation file,
and begins only after independent C107 acceptance. It supersedes blocked I103
and preserves accepted C106/CV7/CV8 evidence.

- [ ] `KI-W6-CV13` Independently inspect the complete C107 diff, require only
  `swapOneSelectionItemViaUi` changed, recompute its ending file digest, rerun
  the two C107 local commands once, and verify both helper call sites and all
  26 case/13 control registrations remain byte-identical.
- [ ] `KI-W6-CV14` Reuse the accepted Next build only if `.next/BUILD_ID`
  exists and the changed-path set from frontend commit
  `a39663c8f99d9cc3c4aa1301ff088d5f4a24e7fd` to the current tree, excluding
  only `test/browser/keyword-intelligence-e2e.mjs`, is empty. From `frontend/`
  run exactly `test -f .next/BUILD_ID` and
  `git diff --name-only a39663c8f99d9cc3c4aa1301ff088d5f4a24e7fd -- . ':(exclude)test/browser/keyword-intelligence-e2e.mjs'`;
  require both exit zero and the second command to print no path. Do not run
  `npm run check` or another build.
- [ ] `KI-W6-CV15` From `frontend/`, run once
  `ALLOW_DATABASE_TESTS=true KI_W6_SKIP_BUILD=1 node test/browser/keyword-intelligence-e2e.mjs`
  with the existing isolated `TEST_DATABASE_URL` sourced without logging.
  Require exit zero; the unchanged 26 required/registered/executed/activated
  cases, 13 pass→fail→fresh-pass controls and all group/global digests; exact
  19 calls, 23 keyword objects, 42 sends, `$0.49200000`, five seeds,
  300/200/200/default-100, both successful page-aware selection swaps, complete
  cleanup and zero residual schema. An environment-only invalidation follows
  E8.1; an observable assertion failure is not recoverable under that rule.
- [ ] `KI-W6-CV16` Only after CV15 passes, from `email_scraper/` run `npm test`
  once and then `npm run check:secrets` once; require zero failures and clean
  scan without opting into the full database suite.
- [ ] `KI-W6-CV17` Then from `email_scraper/` run
  `node scripts/build-keyword-worker.js` exactly twice; require byte-identical
  ZIP hashes, preserved siblings, no forbidden/stale members, ZIP ≤45 MiB,
  unzipped ≤200 MiB and cold-imported function `handler`; run once
  `node --test --test-isolation=none test/aws-pipeline-packaging.test.js` with
  zero failures. Do not run the seven-handler build/measure.
- [ ] `KI-W6-CV18` Recompute the unchanged seven-path set/digest, current file
  hashes, exact 26-ID/group/global equality, 13 controls, substitute ceilings,
  privacy, obsolete-runtime inventory and W7 handoff. Require only the accepted
  C104, C106 and C107 changes against the respective frozen predecessors and no
  out-of-scope source/test member.
- [ ] `KI-W6-CH5` Append one consolidated integration certificate recording
  C107 acceptance, R33 supersession, preserved CV7/CV8, CV13–CV18, exact final
  files/digests, coverage sets, controls, cleanup, costs and requester commit
  provenance if the requester committed C107.
- [ ] `KI-W6-CH6` Stop `READY_FOR_PARENT_REVIEW`; do not begin KI-W7.

If C107 and all I104 gates pass, the window agent continues through CH5/CH6
without another parent prompt. A new implementation-affecting choice, second
file, changed case/control set, observable test failure or contract
contradiction stops. No further CV15 run is pre-authorized after an observable
failure.

##### Third-correction readiness

- [x] `RW6E-001` R33 is an observable failing result and is not relabelled as sandbox invalidation. Evidence: `SRC-KI-043`; `EV-KI-A-095`.
- [x] `RW6E-002` The causal defect is the helper's same-page assumption; production pagination and selection behavior remain correct. Evidence: `SRC-KI-043`; `DEC-KI-041`.
- [x] `RW6E-003` C107 owns one existing symbol in one existing W6 file with an exact baseline and ordered bounded algorithm. Evidence: `KI-W6-CT4`; `EV-KI-A-095`.
- [x] `RW6E-004` Exactly one removal precedes one distinct addition through real controls and returns to 100 items. Evidence: `DEC-KI-041`; `KI-W6-CT4`.
- [x] `RW6E-005` Existing W6-FLOW-07/FLOW-13 and NC-06 supply enforcement; membership and digests do not change. Evidence: `DEC-KI-041`; `EV-KI-A-095`.
- [x] `RW6E-006` CV15 is one fresh causal gate on the changed harness; unchanged backend component and production Next-build evidence are not repeated. Evidence: `KI-W6-I104`; parent standard E8.
- [x] `RW6E-007` Pending regression, secret, worker-package and closure gates remain ordered after causal success. Evidence: `KI-W6-CV16`–`CV18`.
- [x] `RW6E-008` Recursive authority permits transcription/execution but no parent-artifact, external, commit or KI-W7 action. Evidence: A5 state 156; `EV-KI-A-095`.

#### KI-W6 fourth in-flight corrective amendment — bounded final-publication transaction

```yaml
window_id: KI-W6
correction_sequence: [KI-W6-C108, KI-W6-C109, KI-W6-I105]
objective: preserve atomic maximum-cardinality final research publication while replacing Prisma's implicit five-second publication timeout with one publication-only 30-second safety ceiling
depends_on: [accepted KI-W6-C107, passed KI-W6-CV13, passed KI-W6-CV14, EV-KI-W6-R36]
consumes: [SRC-KI-044, DEC-KI-042, accepted C104/C106/C107 bytes, accepted CV7/CV8/CV13/CV14 evidence]
produces: [publication-only bounded transaction options, permanent deterministic rollback/success regression, fresh causal W6 certificate, conditional final regressions/package/scope closure]
assigned_agent_policy: one_window
authorized_write_scope: [email_scraper/src/keyword-intelligence/repository.js through C108 only, email_scraper/test/keyword-intelligence-repository.integration.test.js through C109 only, the three KI-W6 subordinate coordination artifacts by the window agent]
shared_file_scope: [repository.js only _transaction plus two private constants plus publishResearchResult call options; integration test only the SCN-KI-042 helper/registry/test symbols]
read_only_scope: [A1-A8, KI-W6 S1/S2/S3, email_scraper/src/aws-pipeline/keyword-intelligence/service.js createKeywordLeaseMonitor/prepareTerminalLease/aggregateMarket, existing repository unit/integration tests, isolated-postgres helper, keyword-worker build/packaging inputs, frontend emitted-browser harness and accepted Next build]
authorized_actions: [window-agent append-only C108/C109/I105 authoring, sequential single-file delegation, independent leaf review, local syntax/static checks, one focused isolated-database gate, one causal emitted-browser isolated-schema gate, one backend npm test, one secret scan, exactly two keyword-worker builds, one packaging test, read-only final closure]
prohibited_actions: [window-agent implementation edits, parallel leaves, direct parent-leaf communication, agent commit/push, any third implementation/test file, schema/migration/package/frontend/provider/AWS/production edit or call, global transaction timeout change, lease/heartbeat/retry/result/schema/case-or-browser-manifest change, full opted-in database suite, seven-handler build/measure, KI-W7]
successor: KI-W7
successor_reserved_for: parent
may_start_successor: false
```

This amendment supersedes only blocked I104/CV15 and the assumption that the
implicit Prisma timeout is sufficient. C107/CV13/CV14, C106/CV7/CV8 and all
earlier accepted W6 source/test evidence remain accepted unless their exact
inputs change. The current emitted-browser manifest remains 26 cases and 13
controls; the new transaction registry is separate and is merged only at I105.
The two implementation files have sorted-per-LF path-set digest
`0e9215fefca073914b7c198ef548b947b5325d323d7c39f39ffbfdf918009aa9`.

The window agent may append complete C108, C109 and I105 blocks to S1 and
certify exact parent-trace closure. It then assigns exactly C108, independently
reviews it, assigns exactly C109, independently reviews it, and personally
executes I105. No further parent decomposition review is required only when the
appended blocks preserve every literal behavior, file boundary, case/control
member, command, count, digest and stop rule below. A differing decomposition
returns for parent review before any leaf is assigned.

##### Preconditions

- [ ] `KI-W6-CP19` A5 assignment, all standard/A1/A3/A4 pins and the exact current S1 base revision match.
- [ ] `KI-W6-CP20` C107 is accepted; CV13/CV14 pass; R36 is preserved as a failed observable gate, not acceptance or sandbox invalidation.
- [ ] `KI-W6-CP21` Backend HEAD is `a411d4b967942228809e85c7a9780c4ad004bf3c`, its worktree is clean, and the two parent baselines below match.
- [ ] `KI-W6-CP22` `TEST_DATABASE_URL` resolves privately through the existing isolated-postgres helper and is proven distinct from production before behavioral writes.

##### Task block `KI-W6-CT5` / corrective sub-window `KI-W6-C108`

1. **Task/trace:** implement `DEC-KI-042` for `REQ-KI-002/005/024` and
   `INV-KI-004/005/006/014`; scenario `SCN-KI-042`; source evidence
   `SRC-KI-044`.
2. **Source anchor:**
   `email_scraper/src/keyword-intelligence/repository.js` SHA-256
   `be134a3fe039008a9509e940184337e14b276d6bd0e68b6c0830b03e2a68bf48`;
   private constants near `AGGREGATION_LEASE_MS`, method `_transaction(work)`,
   and `publishResearchResult()`'s sole `this._transaction(...)` call.
3. **Target anchor:** the same file only. Add exactly private numeric constants
   `FINAL_PUBLICATION_TRANSACTION_MAX_WAIT_MS = 5_000` and
   `FINAL_PUBLICATION_TRANSACTION_TIMEOUT_MS = 30_000` beside the lease/result
   bounds. Change the private helper signature to `_transaction(work, options)`.
4. **Exact helper algorithm:** construct the existing schema-setting callback
   without changing its body. When `options === undefined`, invoke
   `this.client.$transaction(callback)` with exactly one argument. Otherwise
   invoke `this.client.$transaction(callback, options)`. No other caller passes
   options.
5. **Publication call:** pass exactly
   `{ maxWait: FINAL_PUBLICATION_TRANSACTION_MAX_WAIT_MS, timeout: FINAL_PUBLICATION_TRANSACTION_TIMEOUT_MS }`
   as the second `_transaction` argument only in `publishResearchResult()`.
6. **Interface:** no export, constructor parameter, public option, environment
   read, return-union, error mapping, payload, schema, key or fingerprint
   changes. `_transaction` remains private-by-convention and every existing
   one-argument caller retains the one-argument Prisma invocation.
7. **Durable order/atomicity:** `SAME_ATOMIC_BOUNDARY`; preserve all existing
   reads, token/generation/live-expiry predicates, market-stage conditional
   completion, research result/default-selection conditional completion,
   rollback and `FinalPublicationAbort` handling byte-for-byte apart from the
   closing options argument.
8. **Identity/time:** preserve research, stage, generation and aggregation
   token identities and the injected `now`. The constants are wall-clock
   acquisition/transaction limits only; they do not supply durable timestamps.
9. **Failure/replay:** acquisition failure or timeout throws the existing
   Prisma error and commits nothing. Lost/conflict/found/terminal results,
   exact replay and stale owner behavior do not change. Add no automatic retry.
10. **Bounds:** `maxWait=5_000`, `timeout=30_000`; both are fixed. Preserve the
    120,000 ms aggregation lease, 40,000 ms heartbeat, result byte bound,
    200-row shortlist/final result and default 100 selection.
11. **Callers/obsolete behavior:** only `publishResearchResult()` opts into the
    bounded override. The obsolete behavior removed is reliance on Prisma's
    implicit timeout for final publication. All other `_transaction` callers
    and all direct client writes remain unchanged.
12. **Tests:** C108 runs only `node --check
    src/keyword-intelligence/repository.js` and `git diff --check --
    src/keyword-intelligence/repository.js` from `email_scraper/`. Behavioral
    proof is deliberately deferred to C109/I105; neither local command is
    publication acceptance.
13. **Output:** one reviewed production file consumed by C109 and I105.
14. **Non-goals:** no query/projection optimization, timeout configuration,
    global transaction policy, lease change, provider work, schema, test,
    fixture, manifest, build script or package change.
15. **Negative/forbidden:** a second timeout-bearing caller, direct
    `client.$transaction` duplicate inside publication, timeout ≥120,000,
    swallowed Prisma errors, partial commits, transaction retry or second file
    fails review.

```yaml
subwindow_id: KI-W6-C108
type: CORRECTION
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-03
assigned_agent: UNASSIGNED
predecessors: [KI-W6-C107 accepted, KI-W6-I104 CV13/CV14 passed, EV-KI-W6-R36]
successor_reserved_for: KI-W6-WINDOW-AGENT
writable_file: email_scraper/src/keyword-intelligence/repository.js
file_operation: MODIFY
starting_file_digest: be134a3fe039008a9509e940184337e14b276d6bd0e68b6c0830b03e2a68bf48
starting_repository_change_set_digest: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
read_only_scope: [A1-A8, KI-W6 S1/S2/S3, email_scraper/src/aws-pipeline/keyword-intelligence/service.js named lease/publication symbols, email_scraper/test/keyword-intelligence-repository.test.js, email_scraper/test/keyword-intelligence-repository.integration.test.js]
authorized_actions: [apply KI-W6-CT5 in the one writable file, run the two C108 local commands once, report only to the window agent]
prohibited_actions: [second-file edit, test/schema/migration/package/config/service change, database/build/browser/provider/AWS/production action, commit, push, successor, parent communication]
may_start_successor: false
```

- [ ] `C108-P1` Pins, assignment, clean backend, exact source baseline and R36 predecessor match.
- [ ] `C108-P2` The attributable changed-file set is exactly the writable source file.
- [ ] `C108-T1` Apply every CT5 transformation and no other behavior change.
- [ ] `C108-V1` Run both local commands once and record exit zero; defer behavioral proof to I105.
- [ ] `C108-H1` Return exact diff, ending digest, commands and outcomes to the window agent.
- [ ] `C108-H2` Confirm no prohibited/external/successor action and stop `AWAITING_WINDOW_REVIEW`.

##### Task block `KI-W6-CT6` / corrective sub-window `KI-W6-C109`

1. **Task/trace:** add the permanent `SCN-KI-042` enforcement for
   `DEC-KI-042`; cases `W6-TXN-01/02`; negative control `W6-NC-14`.
2. **Source anchor:**
   `email_scraper/test/keyword-intelligence-repository.integration.test.js`
   SHA-256
   `e1572edeaac65612421fe4b6ae20e979f2aeed16ed94e0b8229b1a6f94856bcc`;
   existing `advanceToMarketStage`, `makeKeywordRow`, `makeResult`,
   `defaultSelectionFor`, client-injection helpers and publication tests.
3. **Target anchor:** that test file only. Add one private transaction-probe
   helper and one top-level test whose name starts exactly `SCN-KI-042:`.
4. **Registry:** literal required/registered IDs are exactly
   `W6-TXN-01`, `W6-TXN-02`; fail on duplicate before execution; compute the
   sorted-unsigned-UTF8/per-member-LF digest and require
   `dd72e2292dac7c33d2250be7af0770401bde67695176d1b76c530b9c7bc10d39`.
   Add an ID to executed only after its activation witness and full oracle pass.
5. **Probe helper:** wrap only the supplied Prisma client's `$transaction` for
   the duration of one publication call; capture a structured clone of the
   options received from production; optionally replace only `timeout` for the
   negative run; wrap only final `keywordResearch.updateMany` and execute the
   literal `SELECT pg_sleep(21.000)` immediately before delegating its first
   `state:"completed"`/result-bearing call. Preserve method receivers and
   restore the original `$transaction` in `finally`. Expose observations only
   to this test.
6. **Maximum fixture:** create exactly 200 distinct `makeKeywordRow` rows and
   derive the exact default 100 using `createDefaultSelection`; use two
   distinct research identities, each advanced through the real repository to
   a fully terminal market stage with a live aggregation token.
7. **`W6-TXN-01` / `W6-NC-14`:** snapshot the complete research and market
   stage rows. Assert the production request options equal exactly
   `{maxWait:5_000, timeout:30_000}`; replace only the effective test timeout
   with 20,000 ms; require the 21,000 ms delay to activate after the stage update,
   Prisma code `P2028` with closed/expired transaction semantics, and deep-equal
   post-call rows proving result, selection, manifest, stage and research all
   rolled back. The control is falsified only when the insufficient timeout
   fails publication yet preserves atomicity; missing production options makes
   the same test fail before the override.
8. **`W6-TXN-02`:** use the same 21,000 ms delay with the production options unchanged;
   require `terminal`, research completed with exactly 200 result keywords,
   exactly 100 default selection items and revision one, market stage completed
   with the supplied manifest/fingerprint, and exact replay `found` without a
   second durable publication.
9. **Identity/fencing:** use only generated research and lease-token identities.
   Do not change clocks or lease rows. I105 reruns the existing SCN-KI-022 stale
   owner final-publication test beside SCN-KI-042.
10. **Isolation/cleanup:** use `setupRepo`/`createIsolatedTestSchema`; verify the
    schema before writes; disconnect and drop/absence-verify in existing
    `t.after`. Do not use or clean `public`; do not log either database URL.
11. **Failure/retry:** no test retries and no production retry. A missing delay,
    wrong options, non-P2028 failure, partial durable change, wrong cardinality,
    replay write, residual schema or unexecuted ID fails.
12. **Substitute fidelity:** the proxy proves option propagation and controlled
    rollback timing only. It cannot claim normal latency. The positive still
    uses the real Prisma interactive transaction and isolated Postgres; CV22
    owns the unmodified-client causal proof.
13. **Local checks:** from `email_scraper/`, run only `node --check
    test/keyword-intelligence-repository.integration.test.js` and `git diff
    --check -- test/keyword-intelligence-repository.integration.test.js`.
    Database execution is deferred to I105/CV21 and must not run in the leaf.
14. **Output:** one reviewed permanent regression file plus exact two-case/one-
    control registration consumed by I105.
15. **Forbidden:** modify an existing test/helper/oracle except additive reuse;
    depend on natural slowness; sleep outside the transaction; alter production
    options in the success path; edit the browser manifest; add provider/AWS/
    production behavior or another file.

C109 begins only after independent C108 acceptance. If the requester commits
the accepted C108 bytes before C109, the window agent records that provenance
and accepts either exact state: clean backend at the requester C108 commit, or
one uncommitted `repository.js` change whose digest equals the accepted C108
digest. Any other path/hunk or agent-authored commit blocks assignment.

```yaml
subwindow_id: KI-W6-C109
type: CORRECTION
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-03
assigned_agent: UNASSIGNED
predecessors: [KI-W6-C108 accepted]
successor_reserved_for: KI-W6-WINDOW-AGENT
writable_file: email_scraper/test/keyword-intelligence-repository.integration.test.js
file_operation: MODIFY
starting_file_digest: e1572edeaac65612421fe4b6ae20e979f2aeed16ed94e0b8229b1a6f94856bcc
starting_repository_change_set: [either accepted uncommitted email_scraper/src/keyword-intelligence/repository.js only, or clean after requester-owned exact C108 commit]
read_only_scope: [A1-A8, KI-W6 S1/S2/S3, accepted C108 source/diff/evidence, email_scraper/src/keyword-intelligence/repository.js, email_scraper/test/helpers/isolated-postgres.js, Prisma schema/migrations read-only]
authorized_actions: [apply KI-W6-CT6 in the one writable test file, run the two C109 local commands once, report only to the window agent]
prohibited_actions: [source/second-test/schema/migration/package/config edit, database execution in leaf, build/browser/provider/AWS/production action, commit, push, successor, parent communication]
may_start_successor: false
```

- [ ] `C109-P1` Pins, assignment, accepted C108 predecessor, exact test baseline and one permitted requester/uncommitted provenance branch match.
- [ ] `C109-P2` The attributable changed-file set is exactly the writable test file.
- [ ] `C109-T1` Apply every CT6 transformation and preserve all existing tests/oracles.
- [ ] `C109-V1` Run both local commands once and record exit zero; do not run the database gate.
- [ ] `C109-V2` Statically enumerate exactly two unique registered cases, one control and their pinned digest.
- [ ] `C109-H1` Return exact diff, ending digest, commands and outcomes to the window agent.
- [ ] `C109-H2` Confirm no prohibited/external/successor action and stop `AWAITING_WINDOW_REVIEW`.

##### Integration assessment `KI-W6-I105`

I105 is owned personally by the window agent, writes no implementation file,
begins only after independent C108 and C109 acceptance, and supersedes blocked
I104/CV15. It preserves accepted CV7/CV8/CV13/CV14 by exact dependency proof.

- [ ] `KI-W6-CV19` Independently inspect C108 against its parent baseline;
  require exactly the two private constants, optional private helper argument,
  preserved one-argument behavior for every non-publication caller and the one
  publication options object. Recompute its ending digest and rerun both C108
  local commands once.
- [ ] `KI-W6-CV20` Independently inspect C109 against its parent baseline;
  require only additive SCN-KI-042 helper/registry/test symbols, all existing
  tests byte-identical, exact case/control members/digest and deterministic
  delay/restore semantics. Recompute its ending digest and rerun both C109
  local commands once.
- [ ] `KI-W6-CV21` From `email_scraper/`, run once against one isolated test
  database:
  `ALLOW_DATABASE_TESTS=true node -r dotenv/config --test --test-isolation=none --test-concurrency=1 --test-name-pattern='publishResearchResult (requires|rollback)|SCN-KI-022: stale owners|SCN-KI-042' test/keyword-intelligence-repository.integration.test.js`.
  Require exactly four pass, zero fail and zero skip; `W6-TXN-01/02` required =
  registered = executed with digest
  `dd72e2292dac7c33d2250be7af0770401bde67695176d1b76c530b9c7bc10d39`;
  `W6-NC-14` falsified; exact 5,000/30,000 options observed; insufficient-
  timeout P2028 rollback leaves full rows equal; delayed maximum publication
  produces 200/default-100 and exact replay; existing atomic rollback and stale
  owner/fenced publication tests pass; every disposable schema is absent.
- [ ] `KI-W6-CV22` Only after CV21 passes, from `frontend/` run once
  `ALLOW_DATABASE_TESTS=true KI_W6_SKIP_BUILD=1 node test/browser/keyword-intelligence-e2e.mjs`
  with the isolated `TEST_DATABASE_URL` sourced without logging. Require exit
  zero; the unchanged 26 required/registered/executed/activated browser cases,
  13 pass→fail→fresh-pass browser controls and exact existing digests; 19 calls,
  23 keyword objects, 42 sends, `$0.49200000`, five seeds,
  300/200/200/default-100, both page-aware swaps, complete cleanup and zero
  residual schema. This is the sole fresh causal run after C108.
- [ ] `KI-W6-CV23` Only after CV22 passes, from `email_scraper/` run `npm test`
  once and `npm run check:secrets` once; require zero failures and clean scan,
  without the full opted-in database suite.
- [ ] `KI-W6-CV24` Then run `node scripts/build-keyword-worker.js` exactly
  twice from `email_scraper/`; require byte-identical ZIP hashes, siblings
  preserved, no forbidden/stale members, ZIP ≤45 MiB, unzipped ≤200 MiB and a
  cold-imported function `handler`; run once
  `node --test --test-isolation=none test/aws-pipeline-packaging.test.js` with
  zero failures. Finally recompute: the two-file correction set/digest; the
  unchanged seven-path assembled W6 history; browser 26 plus transaction 2 =
  exact combined 28 cases/digest
  `c1e4d65b0df7fd1fd86f71420e4ba5e9c6d12cc72b3f24885c71d5283dcf5c75`;
  browser 13 plus transaction control 1 = exact fourteen controls/digest
  `4f2c8489518c5845c52e9336a47f5cc0b90dcdd9dfa70db7614814d87c173af6`;
  zero missing/skip/duplicate/unexpected/unactivated/oracle/substitute/privacy/
  scope/obsolete-runtime failure; requester-only commit provenance; no KI-W7.
- [ ] `KI-W6-CH7` Append one consolidated integration certificate recording
  C108/C109 acceptance, I104 supersession, preserved prior gates, CV19–CV24,
  exact file/case/control sets and digests, P2028 rollback, causal success,
  cleanup, `$0.00` external cost and requester commit provenance if applicable.
- [ ] `KI-W6-CH8` Stop `READY_FOR_PARENT_REVIEW`; do not begin KI-W7.

CV21 and CV22 are separate one-run stateful gates. Each may start elevated.
Only a proven sandbox/channel invalidation permits one identical E8.1 recovery;
an observable assertion, Prisma, product or cleanup failure stops without
running later gates. A C108 or C109 correction invalidates CV21–CV24; a
C107-only change invalidates CV22–CV24. No successful stateful gate is repeated
without one of those exact invalidations.

##### Fourth-correction readiness

- [x] `RW6F-001` R36 is an observable final-publication transaction failure, not a harness assertion or sandbox invalidation. Evidence: `SRC-KI-044`; `EV-KI-A-096`.
- [x] `RW6F-002` Current source and prior W6 attempts isolate the implicit five-second interactive timeout at final `keywordResearch.updateMany`. Evidence: `SRC-KI-044`; `DEC-KI-042`.
- [x] `RW6F-003` The 5,000/30,000 publication-only bounds are mechanically below the freshly renewed 120,000 ms lease and change no other transaction. Evidence: `DEC-KI-042`; `KI-W6-CT5`.
- [x] `RW6F-004` C108 and C109 are sequential one-file corrections with exact baselines, symbols, intermediate state and requester-commit branches. Evidence: `KI-W6-CT5/CT6`; `EV-KI-A-096`.
- [x] `RW6F-005` SCN-KI-042 deterministically proves insufficient-timeout rollback and 30-second success without relying on natural slowness. Evidence: `DEC-KI-042`; `KI-W6-CT6`.
- [x] `RW6F-006` The transaction registry/control and combined case/control sets have literal members and independently recomputed digests. Evidence: `DEC-KI-042`; `EV-KI-A-096`.
- [x] `RW6F-007` Focused DB, causal E2E, regression, secret, package and final closure gates are ordered once and invalidation-aware. Evidence: `KI-W6-I105`; parent standard E8.
- [x] `RW6F-008` Test-proxy fidelity is bounded and the causal unmodified-client run remains mandatory. Evidence: `DEC-KI-042`; `KI-W6-CV21/CV22`.
- [x] `RW6F-009` Recursive authority lets the window agent author/review leaves and personally assess integration without parent implementation or leaf communication. Evidence: A5 state 157; sub-window standard §§1, 5, 9.
- [x] `RW6F-010` The assignment prohibits global timeout, lease, retry, schema, provider, AWS, production, commit and KI-W7 changes. Evidence: A5 state 157; `EV-KI-A-096`.

### KI-W6 fifth correction — supported delay result and parent takeover

The requester explicitly directed the parent to take over and finish KI-W6
after the window agent's terminal could not reliably observe the long-running
gate. `SRC-KI-045` then recovered the complete state-159 result: three passes,
one `SCN-KI-042` Prisma `P2010` failure, and exit one. This is an observable
test-probe defect. It is not eligible for another unchanged transport retry.

#### Task block `KI-W6-CT7` / corrective window `KI-W6-C110`

1. **Owner and writable file:** parent agent under requester override; only
   `email_scraper/test/keyword-intelligence-repository.integration.test.js`,
   starting SHA-256
   `9ba39e9cac703fc7df6d24268a4a1f8d870ce8d056e4556ee9218c80c698599d`.
2. **Exact edit:** inside `withPublicationTransactionProbe`, replace exactly
   `$queryRawUnsafe("SELECT pg_sleep(21.000)")` with
   `$queryRawUnsafe("SELECT ''::text AS slept FROM pg_sleep(21.000)")`.
   No other byte or symbol is owned.
3. **Intermediate state:** the helper still waits exactly 21 seconds immediately
   before delegating the first final result-bearing update. The query result is
   ignored. It now contains one deserializable text column and no `void` result.
4. **Local checks:** `node --check
   test/keyword-intelligence-repository.integration.test.js` and `git diff
   --check -- test/keyword-intelligence-repository.integration.test.js`.
5. **Non-goals:** no production, schema, migration, package, timeout, lease,
   retry, fixture, case/control, browser, provider, AWS or KI-W7 change; no
   commit or push.

#### Parent integration assessment `KI-W6-I106`

- [ ] `KI-W6-CV25` Verify the exact one-expression C110 diff, starting/ending
  digest and both local checks. Preserve C108/C109/CV19/CV20 and the three
  state-159 passing-case diagnostics without treating them as gate acceptance.
- [ ] `KI-W6-CV26` From `email_scraper/`, run the unchanged focused CV21 command
  once in the parent's persistent execution session:
  `ALLOW_DATABASE_TESTS=true node -r dotenv/config --test --test-isolation=none --test-concurrency=1 --test-name-pattern='publishResearchResult (requires|rollback)|SCN-KI-022: stale owners|SCN-KI-042' test/keyword-intelligence-repository.integration.test.js`.
  Require exactly four pass, zero fail, zero skip; exact transaction options,
  P2028 rollback with equal rows, 200/default-100 publication, exact replay,
  stale-owner fencing, `W6-TXN-01/02`, `W6-NC-14`, their unchanged digest, and
  zero residual selected-test schemas.
- [ ] `KI-W6-CV27` Only after CV26 passes, from `frontend/` run once
  `ALLOW_DATABASE_TESTS=true KI_W6_SKIP_BUILD=1 node test/browser/keyword-intelligence-e2e.mjs`.
  Require the unchanged 26 cases/13 controls, 19 calls, 23 keyword objects, 42
  sends, `$0.49200000`, five seeds, 300/200/200/default-100, both page-aware
  swaps, complete cleanup and zero residual schema.
- [ ] `KI-W6-CV28` Only after CV27 passes, run once from `email_scraper/`:
  `npm test`, then `npm run check:secrets`; require zero failures and a clean
  scan. Do not run the full opted-in database suite.
- [ ] `KI-W6-CV29` Then run `node scripts/build-keyword-worker.js` exactly twice
  from `email_scraper/`; require byte-identical ZIP hashes, sibling preservation,
  size ceilings and cold handler import. Run once
  `node --test --test-isolation=none test/aws-pipeline-packaging.test.js` with
  zero failures.
- [ ] `KI-W6-CV30` Recompute the unchanged browser 26 plus transaction 2 = 28
  cases/digest, browser 13 plus `W6-NC-14` = 14 controls/digest, exact W6
  implementation paths, privacy/scope/obsolete-runtime closure and requester-
  only commit provenance. Append consolidated evidence and stop
  `READY_FOR_PARENT_REVIEW`; do not begin KI-W7.

##### Fifth-correction readiness

- [x] `RW6G-001` The complete state-159 artifact supplies an observable P2010
  failure and real exit one; no transport ambiguity remains. Evidence:
  `SRC-KI-045`.
- [x] `RW6G-002` The exact failing expression and Prisma/Postgres type boundary
  are identified. Evidence: `SRC-KI-045`; `DEC-KI-043`.
- [x] `RW6G-003` C110 owns one expression in one test file with an exact baseline
  and replacement. Evidence: `KI-W6-CT7`.
- [x] `RW6G-004` The replacement preserves timing/injection semantics and changes
  only the ignored query result type. Evidence: `DEC-KI-043`.
- [x] `RW6G-005` CV26–CV30 are ordered and later gates cannot run after failure.
  Evidence: `KI-W6-I106`.
- [x] `RW6G-006` Case/control members and digests remain unchanged. Evidence:
  `DEC-KI-043`; `KI-W6-CV30`.
- [x] `RW6G-007` The requester override names the parent as executor and does not
  authorize commits, external actions or KI-W7. Evidence: A5 state 160.
- [x] `RW6G-008` No unresolved implementation or verification choice remains.
  Evidence: literal C110 and I106 blocks.

### KI-W6 sixth correction — causal selection-array consumer

I106 CV26 is accepted at four pass / zero fail / zero skip with zero residual
selected-test schemas. CV27 is an observable harness failure with complete
cleanup. `SRC-KI-046` and `DEC-KI-044` resolve its sole cause without changing
product code or the accepted repository gate.

#### Task block `KI-W6-CT8` / corrective window `KI-W6-C111`

1. **Owner and writable file:** parent agent under the requester's takeover;
   only `frontend/test/browser/keyword-intelligence-e2e.mjs`, starting SHA-256
   `aff4c6174decfc34189fd509cbea84c885cfbb433f061d606f7829c935d25b44`.
2. **Exact edit:** replace exactly
   `const items = (research.selection && research.selection.items) || [];` with
   `const items = Array.isArray(research.selection) ? research.selection : [];`.
   No other byte or symbol is owned.
3. **Local oracle:** the evaluated script must still require `mutation.length ===
   100`, alter only member 99, send the same numeric expected revision and
   minimal item union, and return its existing status/revision/itemCount witness.
4. **Local checks:** `node --check test/browser/keyword-intelligence-e2e.mjs` and
   `git diff --check -- test/browser/keyword-intelligence-e2e.mjs` from
   `frontend/`.
5. **Non-goals:** no Next build, component/library/backend/schema/package,
   timeout, fixture, registry/digest, provider, AWS, production, commit or KI-W7
   change.

#### Parent integration assessment `KI-W6-I107`

- [ ] `KI-W6-CV31` Verify the exact C111 hunk, baseline/ending digest and local
  checks. Preserve accepted CV26 by disjoint-path proof.
- [ ] `KI-W6-CV32` Run the unchanged causal command once from `frontend/`:
  `ALLOW_DATABASE_TESTS=true KI_W6_SKIP_BUILD=1 node test/browser/keyword-intelligence-e2e.mjs`.
  Require the exact existing 26 cases/13 controls and all frozen counts,
  selection/revision/page-aware, cleanup and schema-absence witnesses.
- [ ] `KI-W6-CV33` Only after CV32 passes, run `npm test` and then `npm run
  check:secrets` once from `email_scraper/`; require zero failures and a clean
  scan without opted-in full database integration.
- [ ] `KI-W6-CV34` Then run `node scripts/build-keyword-worker.js` exactly twice
  from `email_scraper/`, require byte-identical ZIP/package limits/cold import
  and sibling preservation, then run once `node --test --test-isolation=none
  test/aws-pipeline-packaging.test.js` with zero failures.
- [ ] `KI-W6-CV35` Recompute final 28-case/14-control equality and digests,
  implementation-path scope, privacy, obsolete-runtime, cleanup and requester-
  only commit closure. Append consolidated evidence, reconcile S2/S3 under the
  parent takeover, CAS A5 to `READY_FOR_PARENT_REVIEW`, and stop before KI-W7.

##### Sixth-correction readiness

- [x] `RW6H-001` CV26 is complete and disjoint from the browser-only correction.
- [x] `RW6H-002` CV27's exact failure and cleanup are observable.
- [x] `RW6H-003` Producer and consumer selection shapes are mechanically traced.
- [x] `RW6H-004` C111 owns one literal expression in one test file.
- [x] `RW6H-005` Revision, mutation-count, stale-conflict and page-swap behavior
  remain literal and unchanged.
- [x] `RW6H-006` CV32–CV35 are ordered with stop-on-failure semantics.
- [x] `RW6H-007` No successful stateful gate is unnecessarily repeated.
- [x] `RW6H-008` No product, registry, digest, external or successor authority is
  introduced.

### KI-W6 seventh correction — set-based repository transactions and bounded recovery

I107/CV32 is an observable production failure after complete cleanup. It
invalidates the earlier `DEC-KI-042` assumption that only final publication
needs a non-default transaction lifetime. `SRC-KI-047` inventories all 18 KI
transaction call sites and the independent unbounded recovery defect.
`DEC-KI-045` permits both boundary consolidation and workload-specific timeout
profiles; a timeout increase alone cannot satisfy this correction.

```yaml
window_id: KI-W6
correction_sequence: [KI-W6-C112, KI-W6-C113, KI-W6-C114, KI-W6-C115, KI-W6-C116, KI-W6-I108]
objective: remove avoidable KI repository round trips, make all 18 transaction budgets explicit, and bound one recovery invocation to 100 work items before resuming the causal W6 gate
depends_on: [accepted KI-W6-C110, passed KI-W6-CV26, accepted local KI-W6-C111, failed KI-W6-CV32, SRC-KI-047, DEC-KI-045]
consumes: [current C110-modified integration test, current C111 browser test, accepted W1 through R5 repository semantics, existing isolated-postgres helper]
produces: [two optimized production files, three focused enforcement test files, seven-case transaction/batching registry, three falsified controls, fresh causal/regression/package closure]
assigned_agent_policy: one_window_with_sequential_leaf_delegation
assigned_window_agent: KI-W6-WINDOW-AGENT
authorized_write_scope: [email_scraper/src/keyword-intelligence/repository.js, email_scraper/src/aws-pipeline/keyword-intelligence/recovery.js, email_scraper/test/keyword-intelligence-repository.test.js, email_scraper/test/keyword-intelligence-repository.integration.test.js, email_scraper/test/keyword-intelligence-recovery.test.js, the three existing KI-W6 reauthored subordinate coordination artifacts]
planned_changed_file_set_digest: dd66e44200514702c82ad06da4c93b3dda30596048a1f569d5779642119f8130
read_only_scope: [A1-A8, both authoring standards, email_scraper/prisma/schema.prisma, generated Prisma client capability, email_scraper/src/aws-pipeline/keyword-intelligence/service.js, email_scraper/src/aws-pipeline/keyword-intelligence/dataforseo-labs-adapter.js, email_scraper/src/keyword-intelligence/api.js, email_scraper/src/prisma-run-repository.js keyword handoff helpers, accepted KI tests and W6 manifest, frontend test harness, build/package inputs]
authorized_actions: [window-agent exact subordinate transcription, sequential leaf assignment and review, one final window-agent integration assessment, authorized local sandbox escalation, one focused isolated-database gate, one causal emitted-browser gate, one backend regression and secret scan, exactly two keyword-worker builds, one packaging test, append subordinate evidence and handoff]
prohibited_actions: [parallel leaves, window-agent implementation edits, direct parent-to-leaf communication, implicit transaction options, provider/S3/SQS work inside database transactions, DataForSEO task volume cost formula or HTTP payload change, schema migration package frontend product established-pipeline provider AWS production destructive commit push or KI-W7 action]
successor: KI-W7
successor_reserved_for: parent
may_start_successor: false
```

The window agent may append mechanically identical single-file `C112` through
`C116` blocks and `I108` to the existing KI-W6 subordinate artifacts, certify
exact equality with this parent trace, and launch its own sequential leaf
agents without another design review. Any changed file set, algorithm,
interface, profile membership, operation ceiling, case/control allocation,
gate or stop rule returns to the parent before a leaf is launched.

#### Preconditions

- [ ] `KI-W6-CP23` A5 assignment, parent/sub-window standard pins, A1/A3/A4
  pins and `ASG-KI-W6-WA-04` match. Evidence: ___
- [ ] `KI-W6-CP24` C110/CV26 and C111 local acceptance remain present; CV32 is
  preserved as failed diagnostic evidence and CV33–CV35 remain unexecuted.
  Evidence: ___
- [ ] `KI-W6-CP25` The five starting digests and exact planned path-set digest
  match; unrelated root relocation state is preserved. Evidence: ___
- [ ] `KI-W6-CP26` The isolated `TEST_DATABASE_URL` resolves privately through
  the existing helper, differs from production and no residual `kiw6_` schema
  exists before the single database gate. Evidence: ___

#### `KI-W6-CT9` / `KI-W6-C112` — repository consolidation and transaction policy

1. **Trace:** `REQ-KI-002/005/022/024`, `INV-KI-004/005/006/014`,
   `SRC-KI-047`, `DEC-KI-045`, `SCN-KI-043`, cases `W6-DB-01`–`05` and
   `W6-DB-07`, controls `W6-NC-15/16`.
2. **File/source:** only `email_scraper/src/keyword-intelligence/repository.js`,
   starting SHA-256
   `359a26f75ba7d605a1c13a5e969ef9ce0a49d0533eb6abe3fa1d6f5bd288c2b5`.
3. **Options interface:** replace the two publication-only numeric constants
   with private frozen `SHORT_TRANSACTION_OPTIONS={maxWait:5_000,timeout:15_000}`
   and `SCALE_TRANSACTION_OPTIONS={maxWait:5_000,timeout:30_000}`. Keep
   `_transaction(work,options)`, remove its undefined/one-argument branch and
   always call `client.$transaction(callback,options)`. Pass exactly the
   profile membership enumerated by `DEC-KI-045`; no nineteenth call and no
   call without options is permitted.
4. **Context reads:** `getTaskContext` uses one task read including
   `stage.research` and latest `attempts` ordered descending with `take:1`;
   `getStageContext` uses one stage read including `research` and ordered
   `tasks`. Preserve all current not-found/generation/stage checks and worker
   projections.
5. **Initialization/claim:** existing-stage initialization loads its tasks in
   the stage read. New initialization retains research validation, optional
   queued→running update, one stage create and one `createManyAndReturn` for
   tasks, sorting returned tasks by unsigned UTF-8 `itemKey`; remove final
   reloads. `claim` retains its classification read and uses
   `updateManyAndReturn`; exactly one returned row is `claimed`, zero is
   `lost`, and the returned row supplies `workerTask` without reread.
6. **Provider ledger:** `recordAttempt` loads task, stage and latest attempt in
   one relation-bearing read, then performs the one exposure aggregate, one
   attempt create and one task update. `settleAttempt` loads attempt plus task
   once, uses `updateManyAndReturn`, preserves immutable cache read/create
   conflict logic and returns that updated attempt without a final reread.
   `markAttemptAmbiguous` loads attempt→task→stage→research in one read and
   preserves its exact terminal counters/failure writes. No attempt or cache
   row crosses the paid HTTP boundary differently.
7. **Delay/terminal:** `deferTask` and `scheduleRetry` include the descending
   latest attempt in the task read. `terminalize` includes its stage, uses
   `updateManyAndReturn`, retains the live token/expiry predicate, increments
   exactly one terminal/categorical counter, performs the current conditional
   ready transition and returns the updated task without reread.
8. **Aggregation:** `claimAggregator` uses `updateManyAndReturn` on both ready
   and exact-expiry reclaim paths. `_completeStageAndCreateNext` loads completed
   replay's next stage with ordered tasks once; mutation uses returned stage,
   one next-stage create and one sorted `createManyAndReturn`, with no final
   reloads. `publishResearchResult` loads research with its three generation
   stages in one read before the unchanged two conditional writes.
9. **Handoff:** initial `createRun` loads research plus only the matching
   client-request handoff including its Run in one read; new handoff retains
   one Run create, one at-most-100 query `createMany` and one handoff create.
   P2002 reconciliation loads handoff including Run once. Return/error unions
   and fingerprint/revision equality remain unchanged.
10. **Throttle:** use the single CTE statement fixed in `DEC-KI-045`: an
    `inserted` CTE inserts `now()+gap` on absence; an `updated` CTE conditionally
    advances an existing due row only when `inserted` is empty; the final union
    emits inserted/updated as `claimed`, otherwise the existing row as
    `delayed`, with exactly one row and one database-clock-derived timestamp.
11. **Recovery:** change only repository signature/algorithm to
    `recover(now,{limit})`, require integer `1..100`, perform the three
    `take:limit` reads and deterministic merge/slice formula in `DEC-KI-045`.
    Preserve message projections and stage-input fingerprints.
12. **Callers/compatibility:** C113 changes the sole production recovery caller;
    C114–C116 change tests. All other public repository inputs/outputs and all
    established-pipeline source remain unchanged. The intermediate state is
    safe but recovery tests are expected to fail until C113/C116.
13. **Local proof:** run only `node --check
    src/keyword-intelligence/repository.js`, `git diff --check --
    src/keyword-intelligence/repository.js`, and a deterministic source
    extraction that reports exactly 18 profiled call sites with the exact
    8-short/10-scale partition. Database behavior is deferred to I108.
14. **Output:** one reviewed source file consumed by all later corrections and
    I108.
15. **Forbidden:** no schema/raw payload/cost/lease/retry/worker/service/API/
    established-pipeline change; no database call in a classification loop;
    no automatic transaction retry or implicit/global 30-second default.

```yaml
subwindow_id: KI-W6-C112
type: CORRECTION
predecessors: [failed KI-W6-CV32]
writable_file: email_scraper/src/keyword-intelligence/repository.js
assigned_agent: UNASSIGNED
successor_reserved_for: KI-W6-WINDOW-AGENT
may_start_successor: false
```

- [ ] `C112-P1` Verify assignment, pins, baseline, predecessor and one-file
  scope. Evidence: ___
- [ ] `C112-T1` Apply all CT9 transformations and no other edit. Evidence: ___
- [ ] `C112-V1` Run the three local proofs with exact 18/8/10 output. Evidence: ___
- [ ] `C112-H1` Return exact diff/digest/evidence to the window agent and stop
  `AWAITING_WINDOW_REVIEW`. Evidence: ___

#### `KI-W6-CT10` / `KI-W6-C113` — recovery caller bound

1. **Trace:** `REQ-KI-022/024`, `DEC-KI-045`, `W6-DB-06`, `W6-NC-17`.
2. **File/source:** only
   `email_scraper/src/aws-pipeline/keyword-intelligence/recovery.js`, starting
   SHA-256 `3fcf9b47c5def5ef2729fe7c844661fd17919978ec0f64156de29ac1050a14f0`.
3. **Transformation:** replace `repository.recover(now)` with exactly
   `repository.recover(now,{limit})`; after `outcome:"found"`, compute the sum
   of `initializations.length`, `taskDispatches.length` and
   `aggregateChecks.length`, require it be `<=limit`, and throw existing
   `PipelineInvariantError("PIPELINE_INPUT_CONFLICT")` before the first send
   otherwise. Preserve three list orders and sequential `sendOne` behavior.
4. **Interface/failure:** existing public `recoverKeywordWork({now,limit=100},
   runtime)` validation and return counts remain exact. A repository over-return
   makes zero sends. Duplicate/retry/fencing remains downstream-owned.
5. **Bound:** at most 100 total `sendOne` calls per invocation; no provider,
   S3, database write, cursor, second queue or concurrency change.
6. **Dependencies:** begins only after C112 acceptance; C116 owns its tests.
7. **Local proof:** `node --check` and file-scoped `git diff --check`; behavioral
   proof deferred to C116/I108.
8. **Preserve:** queue URL parser, four strict message shapes, fingerprint
   generation, return object and safe errors.
9. **Obsolete behavior removed:** validated-but-ignored recovery limit.
10. **Output:** bounded caller consumed by C116/I108.
11. **Forbidden:** no repository/test/handler/queue/config edit.
12. **Boundary:** database recovery completes before any queue send as today.
13. **Coverage:** activation is captured by `W6-DB-06`; over-return by
    `W6-NC-17`.
14. **Evidence:** exact hunk, digest, commands and zero second-file change.
15. **Stop:** report only to window agent; no successor.

- [ ] `C113-P1` Verify accepted C112, assignment and exact baseline. Evidence: ___
- [ ] `C113-T1` Apply CT10 in the one file. Evidence: ___
- [ ] `C113-V1` Run both local checks. Evidence: ___
- [ ] `C113-H1` Return evidence and stop `AWAITING_WINDOW_REVIEW`. Evidence: ___

#### `KI-W6-CT11` / `KI-W6-C114` — unit enforcement

1. **File:** only `email_scraper/test/keyword-intelligence-repository.test.js`,
   starting SHA-256
   `1a2168af81e97f9b0cd239d594362e8a0856754f6b0783efa8c2f134843a77a2`.
2. **Adds:** exact registered set `W6-DB-01/02`, control `W6-NC-15`, and one
   deterministic repository-source/profile parser plus fake-delegate operation
   spies. Preserve all existing tests byte-for-byte.
3. **`W6-DB-01`:** require the literal 18-method multiset, exact 8-short/
   10-scale partition and options `5000/15000` or `5000/30000`; require no
   undefined `_transaction` invocation and no transaction callback containing
   provider/S3/SQS symbols. Activation is successful parsing of every call.
4. **`W6-DB-02`:** execute `getTaskContext`, `getStageContext`, claim and
   aggregator claim against faithful fake delegates; assert one/one/two/two
   operation ceilings and returned projections/ordering.
5. **`W6-NC-15`:** make an in-memory source copy, remove one options argument,
   and require the unchanged profile oracle to fail; production bytes are not
   edited.
6. **Digest:** required local case digest for `W6-DB-01/02` uses the standard
   sorted-LF formula; registered/executed equality and zero skips are asserted.
7. **Checks:** `node --check`, file-scoped diff check, then one exact name-
   patterned non-DB test invocation. The added top-level test name is exactly
   `SCN-KI-043 unit: explicit transaction profiles and consolidated contexts`;
   run exactly:
   `node --test --test-isolation=none --test-name-pattern='SCN-KI-043 unit: explicit transaction profiles and consolidated contexts' test/keyword-intelligence-repository.test.js`.
   Require one pass, zero fail and zero skip; no database/build.
8. **Fidelity:** source parsing proves call-site structure only; dynamic fake
   delegates prove repository control flow only. Real SQL/atomicity remains
   C115/I108.
9. **Dependencies:** accepted C112; no C113 dependency.
10. **Preserve:** existing validation/surface tests and all accepted IDs.
11. **Failure:** missing/duplicate/unexpected ID, wrong profile, extra operation
    or absent activation fails.
12. **Output:** unit certificate consumed by I108.
13. **No fixture/manifest:** registries are additive constants in this file.
14. **Evidence:** exact sets, digest, assertions, negative-control failure.
15. **Forbidden:** no source/snapshot/fixture rewrite or source-text-only claim
    of SQL behavior.

- [ ] `C114-P1` Verify accepted C112 and exact test baseline. Evidence: ___
- [ ] `C114-T1` Add only CT11 symbols. Evidence: ___
- [ ] `C114-V1` Run exact local checks and prove two cases/one control. Evidence: ___
- [ ] `C114-H1` Return evidence and stop. Evidence: ___

#### `KI-W6-CT12` / `KI-W6-C115` — isolated repository integration enforcement

1. **File:** only
   `email_scraper/test/keyword-intelligence-repository.integration.test.js`,
   starting SHA-256
   `a278681ee25a2a955f010ceda54f6a3571f8aa782b5edc9aae20b27b7cb271a5`;
   preserve C110 and every existing test/oracle.
2. **Adds:** one `SCN-KI-043` registry for `W6-DB-03/04/05/06/07`, control
   `W6-NC-16`, delegate/transaction option counters and isolated fixtures.
3. **`W6-DB-03`:** real record/settle success, failure, fence loss, exact replay
   and rollback preserve attempt cost/cache semantics while enforcing at-most
   four operations per method and exact scale profile.
4. **`W6-DB-04`:** terminalize and both stage-publication paths preserve live
   expiry/token fencing, once-only counters, ready transition, stage/task sets,
   stale-owner zero visibility and operation ceilings.
5. **`W6-DB-05`:** maximum five-seed initialization creates ten ordered tasks;
   maximum saved 100-item handoff creates one Run, exactly 100 RunQuery rows and
   one handoff, with same-key replay and unequal conflict; enforce declared
   operation ceilings/profiles.
6. **`W6-DB-06`:** directly seed more than 100 eligible members across all
   three recovery classes in one disposable schema; `recover(now,{limit:100})`
   executes three bounded reads, returns exactly the deterministic first 100,
   never member 101, and a second smaller limit returns its exact prefix.
7. **`W6-DB-07`:** real concurrent throttle claims use one SQL statement per
   invocation, yield one claimant and delayed competitors with the same future
   boundary, and allow an exact-due subsequent claimant.
8. **`W6-NC-16`:** a non-mutating proxy reintroduces one removed delegate read;
   the unchanged operation ceiling must throw, then the unwrapped production
   path passes.
9. **Isolation:** existing helper only; verify distinct nonproduction identity,
   schema-local migrations/current schema before writes, exact finally drop and
   post-drop absence. No `public` cleanup.
10. **Coverage:** assert exact five registered/executed cases, zero skips,
    control falsified and local sorted-LF digest; I108 merges all seven.
11. **Checks:** leaf runs syntax and diff checks only; the single database
    execution belongs exclusively to I108.
12. **Accepted-test invalidation:** repository.js changes invalidate the prior
    CV26 runtime result but not C110 test bytes; I108 reruns the four CV26 cases
    in the same focused database invocation.
13. **Performance:** assert delegate/statement ceilings and cardinalities, not a
    flaky elapsed-time target; retain SCN-KI-042's deterministic 20/21-second
    safety proof.
14. **Evidence:** complete row equality, operation traces, options, sets,
    negative control and cleanup.
15. **Forbidden:** no production source, helper, fixture, timeout override,
    browser, full integration suite or shared cleanup.

- [ ] `C115-P1` Verify accepted C112 and current C110-bearing baseline. Evidence: ___
- [ ] `C115-T1` Add only CT12 symbols. Evidence: ___
- [ ] `C115-V1` Run syntax/diff checks only; defer DB to I108. Evidence: ___
- [ ] `C115-H1` Return exact registry/diff/digest and stop. Evidence: ___

#### `KI-W6-CT13` / `KI-W6-C116` — recovery caller enforcement

1. **File:** only `email_scraper/test/keyword-intelligence-recovery.test.js`,
   starting SHA-256
   `22d2bade7c316bed275057a5c20c78df516b64de99f6d960254a916283a27075`.
2. **Update:** every faithful repository mock accepts `(now,{limit})` and
   asserts the forwarded value. Preserve all existing message/order/error
   tests.
3. **Positive oracle:** return a mixed list totaling exactly 100; assert the
   repository saw `100`, exactly 100 ordered `sendOne` calls occur, and reported
   category/sent counts equal the fixture.
4. **Small-limit oracle:** `limit:1` forwards one and dispatches exactly the one
   returned candidate.
5. **`W6-NC-17`:** repository substitute returns `limit+1`; assert the caller
   throws `PIPELINE_INPUT_CONFLICT` before any send. This control is registered
   and falsified here; `W6-DB-06` remains registered only in C115.
6. **Invalid input:** existing zero/101/noninteger validation remains zero-call.
7. **Checks:** `node --check`, file diff check and exact focused recovery test;
   assert all existing plus new tests pass with zero skip. The added top-level
   test name is exactly
   `SCN-KI-043 recovery caller: forwards bound and rejects over-return`; run
   exactly:
   `node --test --test-isolation=none --test-name-pattern='SCN-KI-043 recovery caller: forwards bound and rejects over-return' test/keyword-intelligence-recovery.test.js`.
   Require one pass, zero fail and zero skip.
8. **Fidelity:** mock proves caller propagation/zero-send guard; real repository
   ordering/bounds are C115/I108.
9. **Dependencies:** accepted C113 and C115 registry ownership.
10. **Coverage:** no duplicate DB case ID; control set equality is asserted.
11. **Preserve:** queue/message schemas, URL, fingerprint and dispatch order.
12. **Output:** caller/control certificate consumed by I108.
13. **Failure:** any send before over-return rejection fails.
14. **Evidence:** exact trace, counts, commands, digest and one-file scope.
15. **Forbidden:** no recovery source, repository, fixture or manifest edit.

- [ ] `C116-P1` Verify C113/C115 acceptance and baseline. Evidence: ___
- [ ] `C116-T1` Apply CT13 only. Evidence: ___
- [ ] `C116-V1` Run focused recovery checks and falsify NC-17. Evidence: ___
- [ ] `C116-H1` Return evidence and stop. Evidence: ___

#### Window-agent assessment `KI-W6-I108`

The window agent personally executes I108 after independently accepting all
five leaves. It has zero implementation-file write authority.

- [ ] `KI-W6-CV36` Inspect all five diffs from their pinned baselines; require
  actual changed paths equal the five-path set and digest
  `dd66e44200514702c82ad06da4c93b3dda30596048a1f569d5779642119f8130`,
  exact 18/8/10 profiles, operation ceilings, recovery interface/bound and no
  established-pipeline/provider boundary change.
- [ ] `KI-W6-CV37` From `email_scraper/`, run exactly once:
  `node --test --test-isolation=none --test-name-pattern='SCN-KI-043 unit: explicit transaction profiles and consolidated contexts|SCN-KI-043 recovery caller: forwards bound and rejects over-return' test/keyword-intelligence-repository.test.js test/keyword-intelligence-recovery.test.js`.
  Require exactly two pass, zero fail and zero skip;
  all tests pass, `W6-DB-01/02` execute, `W6-NC-15/17` falsify acceptance, and
  no required skip/duplicate/unexpected ID.
- [ ] `KI-W6-CV38` From `email_scraper/`, run exactly once against the isolated
  database:
  `ALLOW_DATABASE_TESTS=true node -r dotenv/config --test --test-isolation=none --test-concurrency=1 --test-name-pattern='SCN-KI-043: set-based transaction ceilings and bounded recovery|publishResearchResult (requires|rollback)|SCN-KI-022: stale owners|SCN-KI-042' test/keyword-intelligence-repository.integration.test.js`.
  The added top-level `SCN-KI-043: set-based transaction ceilings and bounded
  recovery` owns DB-03 through DB-07 and includes provider settlement,
  exact-expiry ownership and maximum handoff/replay subtests. Require exactly
  five matching top-level tests pass with zero fail/skip; `W6-DB-03`–`07`
  execute;
  `W6-NC-16` falsifies; `W6-TXN-01/02` and `W6-NC-14` reexecute; exact rollback,
  operation counts, 18 options, 100-bound recovery and zero residual schemas.
  This is the sole new database gate.
- [ ] `KI-W6-CV39` Only after CV38 passes, run once from `frontend/`:
  `ALLOW_DATABASE_TESTS=true KI_W6_SKIP_BUILD=1 node
  test/browser/keyword-intelligence-e2e.mjs`. Require the unchanged 26 browser
  cases/13 controls, 19 provider-substitute calls, 23 keyword artifacts, 42
  sends, `$0.49200000`, five seeds, 300/200/200/default-100, revision advance,
  both page-aware swaps, complete process/tmp/schema cleanup and zero live
  provider/AWS activity.
- [ ] `KI-W6-CV40` Run once from `email_scraper/`: `npm test`, then `npm run
  check:secrets`; require zero failures and a clean scan. Do not run the full
  opted-in database integration suite.
- [ ] `KI-W6-CV41` Run `node scripts/build-keyword-worker.js` exactly twice;
  require byte-identical keyword ZIPs, sibling preservation, size/startup
  limits, then run once `node --test --test-isolation=none
  test/aws-pipeline-packaging.test.js` with zero failures.
- [ ] `KI-W6-CV42` Recompute new required=registered=executed cases exactly
  `W6-DB-01`–`07`, count 7, digest
  `073c0fa52135c9a271eea75264efc79fd6ebcb8d062ec73175dbb58a5333aa8f`;
  controls `W6-NC-15`–`17`, count 3, digest
  `86562d5c606dc8867b40ecd46b6604e2f5a66a2553c41a20a23696cb48cdbec0`.
  Merge with the unchanged browser 26 plus transaction 2 for exactly 35 cases,
  digest `c5ead2a638d7f5481178730958d83b582e42aeb265536696555eaf1a08b5d5f9`,
  and browser 13 plus transaction control plus three new controls for exactly
  17, digest `62566fd91c96579a60c9f512c27cf94afdabdbc000a967a3251b177f9710c2f5`.
- [ ] `KI-W6-CV43` Verify privacy, no transaction contains provider/S3/SQS work,
  no DataForSEO call/cost/cardinality change, no schema/migration/package/
  frontend product/established-pipeline/AWS/production/commit/KI-W7 action,
  and both nested worktrees contain only requester/authorized files.
- [ ] `KI-W6-CH9` Append the complete window-agent integration/enforcement
  certificate to S3, reconcile all earlier failed assessments as superseded but
  preserved, set S2 `READY_FOR_PARENT_REVIEW`, and return one consolidated
  handoff to the parent. Do not edit A1–A8 and do not begin KI-W7.

Stateful gates CV38/CV39 run only once after the last relevant edit. They may
start elevated. One identical recovery is allowed only after proven sandbox or
channel invalidation under E8.1; an observable assertion/Prisma/cleanup failure
requires diagnosis and the standard corrective-subwindow loop, not a retry.

##### Seventh-correction readiness

- [x] `RW6I-001` All 18 transaction paths and their exact profile memberships
  are enumerated. Evidence: `SRC-KI-047`; `DEC-KI-045`.
- [x] `RW6I-002` Timeout policy and set-based consolidation are separate but
  jointly required; a resource-only patch fails acceptance. Evidence:
  `DEC-KI-045`; `W6-DB-01`–`07`.
- [x] `RW6I-003` Provider, S3, SQS and task-fence boundaries remain fixed.
  Evidence: `DEC-KI-045`; CT9 items 6/7/10.
- [x] `RW6I-004` Recovery is deterministically bounded and the previously
  ignored limit has one exact caller/repository interface. Evidence:
  `DEC-KI-045`; CT9 item 11; CT10.
- [x] `RW6I-005` Five changed files have sequential single-file ownership and
  exact baselines; no leaf owns a second file. Evidence: CT9–CT13.
- [x] `RW6I-006` Seven cases and three controls have exact registrations,
  activation witnesses, digests and falsification mechanisms. Evidence:
  `SCN-KI-043`; CT11–CT13; CV42.
- [x] `RW6I-007` Expensive gates occur once at I108 with exact invalidation and
  sandbox-recovery rules. Evidence: CV38–CV43.
- [x] `RW6I-008` The window agent may launch only sequential child leaves,
  personally assess integration and stop before parent acceptance/KI-W7.
  Evidence: correction header; A5 state 163.
- [x] `RW6I-009` DataForSEO maximum remains `$0.49200000`; transport/database
  batching is not misrepresented as provider-cost reduction. Evidence:
  `SRC-KI-047`; `DEC-KI-045`.
- [x] `RW6I-010` No implementation-affecting choice or unknown payload remains.
  Evidence: CT9–CT13; `SRC-KI-047`; `DEC-KI-045`.

### KI-W6 eighth correction — revision-partitioned final-CAS witness

```yaml
window_id: KI-W6
correction_id: KI-W6-EIGHTH-CORRECTION
objective: Correct only the causal browser harness's structurally impossible final-CAS netlog oracle while preserving the real two-success revision sequence and every product/CAS invariant.
depends_on: [accepted KI-W6-C112, accepted KI-W6-C113, accepted KI-W6-C114, accepted KI-W6-C115, accepted KI-W6-C116, accepted KI-W6-C117, I109 CV36 pass, I109 CV37 pass, I109 CV38 pass, I109 CV39 diagnostic failure EV-KI-W6-R52]
consumes: [SRC-KI-048, DEC-KI-046, current browser harness digest f7f055e62f0e2c3c438bdaf739253f0cc917803a8a5115306773066b137fce6f]
produces: [one revision-partitioned browser oracle, one fresh complete causal certificate, pending final regression/build/coverage/privacy closure]
correction_sequence: [KI-W6-C118, KI-W6-I110]
assigned_agent_policy: one_window_with_recursive_single_file_leaves
delegable_implementation_file_set: [frontend/test/browser/keyword-intelligence-e2e.mjs]
delegable_implementation_file_set_digest: 3dd4230266485b5b217634b4558e3aa027264534ab8a13c52ddc2f227eca9867
delegable_implementation_baseline: frontend/test/browser/keyword-intelligence-e2e.mjs=f7f055e62f0e2c3c438bdaf739253f0cc917803a8a5115306773066b137fce6f
window_agent_coordination_scope: [KEYWORD_INTELLIGENCE_KI_W6_REAUTHORED_SUBWINDOW_CHECKLIST.md append/reconciliation only, KEYWORD_INTELLIGENCE_KI_W6_REAUTHORED_SUBWINDOW_STATE.md, KEYWORD_INTELLIGENCE_KI_W6_REAUTHORED_SUBWINDOW_EVIDENCE.md append-only]
read_only_scope: [KEYWORD_INTELLIGENCE_PRODUCT_CONTRACT.md, KEYWORD_INTELLIGENCE_DISCOVERY_DOSSIER.md, KEYWORD_INTELLIGENCE_DECISION_LEDGER.md, KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md, ACTIVE_EXECUTION_STATE.md, KEYWORD_INTELLIGENCE_EXECUTION_EVIDENCE.md, KEYWORD_INTELLIGENCE_SPECIFICATION_CHANGELOG.md, KEYWORD_INTELLIGENCE_TRACEABILITY_INDEX.md, KEYWORD_INTELLIGENCE_KI_W6_REAUTHORED_SUBWINDOW_CHECKLIST.md, KEYWORD_INTELLIGENCE_KI_W6_REAUTHORED_SUBWINDOW_STATE.md, KEYWORD_INTELLIGENCE_KI_W6_REAUTHORED_SUBWINDOW_EVIDENCE.md, email_scraper/src/keyword-intelligence/repository.js, email_scraper/src/aws-pipeline/keyword-intelligence/recovery.js, email_scraper/test/keyword-intelligence-repository.test.js, email_scraper/test/keyword-intelligence-repository.integration.test.js, email_scraper/test/keyword-intelligence-recovery.test.js, frontend/components/keyword-intelligence/, frontend/lib/client-api.ts, frontend/lib/keyword-intelligence-view-model.ts, "frontend/app/api/keyword-research/[researchId]/selection/route.ts", frontend/node_modules/next/dist/docs/, frontend/.next/]
authorized_actions: [window agent mechanically appends C118 and I110, launches and independently reviews one single-file C118 leaf, personally executes I110, starts authorized local commands elevated when required, uses one standards-defined identical recovery only after proven environment invalidation, records subordinate evidence and returns READY_FOR_PARENT_REVIEW]
prohibited_actions: [window-agent implementation edit, parallel leaf, second implementation file, clearing/truncating netlog, product/API/repository/database/provider/cost/queue/artifact/schema/package/build-input change, case/control ID or digest change, changed browser command, commit, push, provider/AWS/production/destructive action, KI-W7]
successor: KI-W7
successor_reserved_for: parent
may_start_successor: false
```

#### `KI-W6-CT14` / `KI-W6-C118` — truthful successful-selection request partition

1. **Task ID:** `KI-W6-CT14`; the window agent compiles it into exactly one
   corrective leaf `KI-W6-C118` with a new leaf assignment ID.
2. **Requirements/decision:** `REQ-KI-007`–`009`, `REQ-KI-014/015`,
   `INV-KI-010`, `DEC-KI-046`; trigger `SRC-KI-048` / `EV-KI-W6-R52`.
3. **Source anchor:** in
   `frontend/test/browser/keyword-intelligence-e2e.mjs`, immediately after the
   second `saveSelectionViaUi()` in the revision-conflict flow, the current
   `savedEntries` assignment filters all successful selection PUTs and the next
   line requires length one.
4. **Target anchor:** replace only that successful-save collection/assertion
   block before `const savedBody = savedEntries[0].requestBody || {};`;
   preserve the surrounding conflict,
   durable-state, capture, activation and finalization code byte-for-byte.
5. **Complete internal interface:** netlog entries retain fields `method`,
   `url`, `responseStatus`, and parsed `requestBody`; no producer/parser change.
   The block introduces only local arrays named `successfulSelectionEntries`,
   `advanceEntries`, and `savedEntries`; it exports nothing.
6. **Ordered algorithm:** (a) assign `successfulSelectionEntries` from exactly
   `(await netlogOf(cdp)).filter((entry) => entry.method === "PUT" && entry.url.endsWith("/selection") && entry.responseStatus === 200)`;
   (b) assert its length is exactly `2`;
   (c) derive `advanceEntries` from it with
   `entry.requestBody?.expectedRevision === 1` and assert length exactly `1`;
   (d) derive `savedEntries` from it with
   `entry.requestBody?.expectedRevision === 2` and assert length exactly `1`;
   (e) leave `const savedBody = savedEntries[0].requestBody || {};` and every
   following assertion unchanged. Each assertion message states its expected
   role and observed count; no `>=`, positional-last, fallback, log reset or
   unpartitioned success assertion is permitted.
7. **Operation order/boundary:** test observation only after the deliberate
   advance, stale 409, reload, page-aware swap and UI save; it performs no new
   request or durable operation and changes no transaction/recovery boundary.
8. **Identity/formula:** the exact request revision is the role discriminator:
   advance=`1`, final=`2`; total successful selection PUTs=`2`; final durable
   revision=`3`. Method/URL/status alone never identifies the final CAS.
9. **Failure/replay/concurrency:** zero, duplicate, extra, malformed-body,
   wrong-revision or mispartitioned success fails before handoff. The existing
   stale 409, retry, restart and later post-handoff mutation behavior is
   unchanged.
10. **Fixed bounds/configuration:** exactly 100 final items, one stale 409,
    two successful selection PUTs, one per revision partition, existing
    browser timeouts/environment and the literal CV45 command. No netlog
    lifetime, server configuration, page size or build input changes.
11. **Callers/obsolete behavior:** only the local selection assertion consumes
    the new arrays. Remove only the obsolete unpartitioned `savedEntries`
    assignment and its length-one assertion. Preserve C107's helper and C111's
    `Array.isArray(research.selection)` expression.
12. **Tests/enforcement:** no new case/control registration. Existing
    `W6-FLOW-07` executes the corrected witness; `W6-NC-06` remains its
    falsification control. Required browser set stays 26 IDs/digest
    `d81bab26bc5aadd19c162156c13890611b2fc5a6d0dcb917234453d568ffb4d4`;
    controls stay 13 IDs/digest
    `cfc5ff10479640aac3f43eaf1c2987ce2f2796335496f88ba82abeff3d56df72`.
    The observed old block is the negative counterexample and fails on the
    required two-success trace.
13. **Local-now checks:** from `frontend/`, run exactly `node --check
    test/browser/keyword-intelligence-e2e.mjs`; require exit zero. Then run the
    literal read-only source assertion below; require `KI_W6_C118_SOURCE_OK`.
    Do not run the browser gate in the leaf.

    ```bash
    node -e 'const fs=require("node:fs");const s=fs.readFileSync("test/browser/keyword-intelligence-e2e.mjs","utf8");const one=(x)=>((s.match(new RegExp(x,"g"))||[]).length===1);if(!one("const successfulSelectionEntries =")||!one("const advanceEntries = successfulSelectionEntries\\.filter")||!one("const savedEntries = successfulSelectionEntries\\.filter")||!s.includes("entry.requestBody?.expectedRevision === 1")||!s.includes("entry.requestBody?.expectedRevision === 2")||!s.includes("successfulSelectionEntries.length === 2")||!s.includes("advanceEntries.length === 1")||!s.includes("savedEntries.length === 1")||!s.includes("const items = Array.isArray(research.selection) ? research.selection : [];")||s.includes("const savedEntries = (await netlogOf(cdp)).filter"))throw new Error("KI_W6_C118_SOURCE_INVALID");console.log("KI_W6_C118_SOURCE_OK")'
    ```
14. **Output:** one syntax-valid harness whose final-CAS witness identifies the
    final request by expected revision and is consumed by `KI-W6-I110`.
15. **Non-goals/forbidden edits:** no production/component/route/server/
    repository/helper/netlog/certificate registry/case/control/fixture/build
    edit; no assertion deletion other than the named obsolete length-one
    assertion; no second file, test execution, commit or successor action.

- [ ] `C118-P1` Verify A5 assignment, all pins, predecessor evidence, exact
  baseline digest and the one-file scope. Evidence: ___
- [ ] `C118-T1` Apply exactly CT14's ordered block replacement and no other
  edit. Evidence: ___
- [ ] `C118-V1` Run both local-now checks and record the exact source witnesses.
  Evidence: ___
- [ ] `C118-H1` Return the one-file diff, ending digest, commands and deferred
  I110 obligation to the window agent, then stop `AWAITING_WINDOW_REVIEW`.
  Evidence: ___

#### Window-agent assessment `KI-W6-I110`

The window agent authors the exact subordinate C118/I110 blocks from CT14,
assigns and independently reviews C118, and personally executes I110. I110 has
zero implementation-file write authority.

- [ ] `KI-W6-CV44` Independently inspect C118 from baseline
  `f7f055e62f0e2c3c438bdaf739253f0cc917803a8a5115306773066b137fce6f`;
  require the attributable path set to equal the singleton with digest
  `3dd4230266485b5b217634b4558e3aa027264534ab8a13c52ddc2f227eca9867`,
  exactly the CT14 block change, both local commands passing, C107/C111
  witnesses still present, and zero case/control/registry/helper/netlog change.
- [ ] `KI-W6-CV45` Reuse I109 CV36–CV38 only after exact dependency/hash proof:
  C118 changes no backend input or asserted path, and all five accepted backend
  file digests remain those in `EV-KI-W6-R52`. Then run once from `frontend/`:
  `ALLOW_DATABASE_TESTS=true KI_W6_SKIP_BUILD=1 node
  test/browser/keyword-intelligence-e2e.mjs`. Require exit zero; all unchanged
  26 required/registered/executed/activated browser cases and 13
  pass→fail→fresh-pass controls; exactly two successful selection PUTs, one
  expected-revision-1 advance, one expected-revision-2 final CAS, one stale
  409, 100 final items and durable revision three; 19 provider-substitute calls,
  23 keyword artifacts, 42 sends, `$0.49200000`, five seeds,
  300/200/200/default-100, both page-aware swaps, complete process/temp/schema
  cleanup, zero residual schema and zero live provider/AWS activity.
- [ ] `KI-W6-CV46` Only after CV45 passes, run once from `email_scraper/`:
  `npm test`, then `npm run check:secrets`; require zero failures and a clean
  scan. Do not run the full opted-in database suite.
- [ ] `KI-W6-CV47` Run `node scripts/build-keyword-worker.js` exactly twice
  from `email_scraper/`; require byte-identical keyword ZIPs, sibling
  preservation, no forbidden/stale members, ZIP at most 45 MiB, unzipped at
  most 200 MiB and a cold import exporting a function named `handler`; then run once
  `node --test --test-isolation=none test/aws-pipeline-packaging.test.js` with
  zero failures.
- [ ] `KI-W6-CV48` Recompute browser 26/13 equality/digests unchanged; new DB
  cases `W6-DB-01`–`07` and controls `W6-NC-15`–`17` unchanged; final combined
  required=registered=executed cases exactly 35/digest
  `c5ead2a638d7f5481178730958d83b582e42aeb265536696555eaf1a08b5d5f9`
  and controls exactly 17/digest
  `62566fd91c96579a60c9f512c27cf94afdabdbc000a967a3251b177f9710c2f5`,
  with zero missing, skipped, duplicate, unexpected or unactivated member and
  every control falsified.
- [ ] `KI-W6-CV49` Verify privacy, substitute-fidelity limits, accepted evidence
  invalidation/supersession, exact current correction paths
  `email_scraper/src/keyword-intelligence/repository.js`,
  `email_scraper/src/aws-pipeline/keyword-intelligence/recovery.js`,
  `email_scraper/test/keyword-intelligence-repository.test.js`,
  `email_scraper/test/keyword-intelligence-repository.integration.test.js`,
  `email_scraper/test/keyword-intelligence-recovery.test.js`, and
  `frontend/test/browser/keyword-intelligence-e2e.mjs`,
  no transaction contains provider/S3/SQS work, no DataForSEO call/cost change,
  and no schema/migration/package/product/established-pipeline/AWS/production/
  destructive/commit/push/KI-W7 action.
- [ ] `KI-W6-CH10` Append the complete I110 integration/enforcement certificate
  to S3; preserve and supersede failed I109/CV39; set S2
  `READY_FOR_PARENT_REVIEW`; return one consolidated handoff to the parent and
  stop before KI-W7.

Stateful CV45 runs once only after C118's final edit. It may start elevated.
One identical recovery is permitted only for a proven sandbox/channel
invalidation under E8.1; an observable assertion, Prisma, cleanup or product
failure enters the standard correction loop and is not retried as transport.

##### Eighth-correction readiness

- [x] `RW6J-001` The observed failure is causally a harness-oracle partition,
  not a repository CAS defect. Evidence: `SRC-KI-048`; `EV-KI-W6-R52`.
- [x] `RW6J-002` The exact two successful operations and their revision roles
  are frozen; no alternative identification remains. Evidence: `DEC-KI-046`.
- [x] `RW6J-003` C118 owns exactly one file and one local block; all product and
  accepted helper behavior is read-only. Evidence: CT14.
- [x] `RW6J-004` Existing case/control membership and digests remain exact;
  `W6-FLOW-07`/`W6-NC-06` own the behavior. Evidence: `DEC-KI-046`; CT14.
- [x] `RW6J-005` The old broad filter is a captured falsifying counterexample,
  while CV45 must prove the corrected real route/UI/durable path. Evidence:
  `EV-KI-W6-R52`; CV45.
- [x] `RW6J-006` CV36–CV38 reuse is dependency-bounded; CV45 and all still
  pending final gates execute after the correction. Evidence: I110.
- [x] `RW6J-007` Sandbox recovery, costly-gate scheduling, cleanup and stop
  behavior are exact. Evidence: I110; pinned standards.
- [x] `RW6J-008` The window agent may manage only C118 then I110 and cannot
  implement, commit or begin KI-W7. Evidence: correction header; A5 state 164.

### KI-W6 ninth correction — protected workspace auth-substitute completion

```yaml
correction_id: KI-W6-CORRECTION-09
trigger: SRC-KI-049 / EV-KI-W6-R54
decision: DEC-KI-047
predecessor: KI-W6-C118 accepted; I110 CV44 and CV45 backend-reuse proof passed; fresh CV45 browser run failed only at protected workspace navigation
sequence: [KI-W6-C119, KI-W6-C120, KI-W6-I111]
delegable_file_set:
  - email_scraper/test/helpers/keyword-intelligence-e2e-harness.js
  - frontend/test/browser/keyword-intelligence-e2e.mjs
delegable_file_set_digest: 4f0d4befb9a6d1cdb039108cf271c25ed23265436fdf856866e93caeef179628
parallelism: forbidden; C120 depends on accepted C119; I111 begins only after both are accepted
window_agent_implementation_authority: none
window_agent_integration_authority: I111 only
successor_authority: false
```

The accepted C118 bytes are preserved. This correction changes only the local
authentication substitute needed to make the already-required `/runs/<id>`
route causally reachable through production `proxy.ts`. It does not modify or
bypass product auth. The window agent must transcribe these blocks into S1,
assign one single-file leaf at a time, independently review each leaf, execute
I111 personally, return `READY_FOR_PARENT_REVIEW`, and stop before KI-W7.

#### `KI-W6-CT15` / `KI-W6-C119` — complete deterministic loopback session

1. **Task ID and owner:** `KI-W6-CT15`; compile to exactly one leaf
   `KI-W6-C119` owning only
   `email_scraper/test/helpers/keyword-intelligence-e2e-harness.js`.
2. **Preconditions:** A5 assigns the ninth correction; C118 is accepted; the
   file exists with SHA-256
   `7571818027b54bc812d4395d0eb1eec65616b1b939c90baae27fefdb619867c6`;
   the singleton path-set digest is
   `7549f43fbf304b87491bb6d7758f09ea4b9d237153c7fe7ff2554fef5f125fe4`.
3. **Consumes:** `SRC-KI-049`, `DEC-KI-047`; no payload discovery or leaf
   choice remains.
4. **Exact constants:** immediately after existing
   `NEON_AUTH_COOKIE_SECRET_VALUE`, add exactly:
   `NEON_AUTH_SESSION_COOKIE_NAME = "__Secure-neon-auth.session_token"`,
   `NEON_AUTH_SESSION_COOKIE_VALUE = "kiw6-local-session-token"`,
   `AUTH_SESSION_CREATED_AT = "2026-08-21T00:00:00.000Z"`, and
   `AUTH_SESSION_EXPIRES_AT = "2099-01-01T00:00:00.000Z"` as `const` values.
5. **Exact envelope function:** immediately after `setAuthOwner`, add a local
   `authSessionBody` zero-argument function. It returns `null` for
   `authMode === "none"`. Otherwise derive `userId` from the existing
   owner-A/owner-B mapping and return exactly the session+user object frozen in
   `DEC-KI-047`; no additional key, alias, token validation or random/time
   dependency is permitted.
6. **Endpoint replacement:** in only the existing `GET /get-session` branch,
   replace the old ternary `{user:{id}}` body assignment with
   `const body = authSessionBody();`. Preserve the trace call, HTTP 200,
   content type, JSON serialization, 404 branch and server lifecycle exactly.
7. **Public test seam:** immediately before the harness return, create
   `browserSessionCookie = Object.freeze({name:NEON_AUTH_SESSION_COOKIE_NAME,value:NEON_AUTH_SESSION_COOKIE_VALUE})`;
   add exactly that property to the existing returned `Object.freeze(...)`.
   Do not expose the cookie secret, dates or session body.
8. **Behavior:** owner A/B still map to their existing durable owner IDs;
   `none` still produces JSON null. The token is an opaque local trigger only;
   the installed SDK remains the sole session-data signer and middleware
   decision maker. No production auth, database, provider, queue or artifact
   behavior changes.
9. **Local-now checks:** from `email_scraper/`, run exactly
   `node --check test/helpers/keyword-intelligence-e2e-harness.js`, then run:

   ```bash
   node -e 'const fs=require("node:fs");const s=fs.readFileSync("test/helpers/keyword-intelligence-e2e-harness.js","utf8");for(const x of ["const NEON_AUTH_SESSION_COOKIE_NAME = \"__Secure-neon-auth.session_token\"","const NEON_AUTH_SESSION_COOKIE_VALUE = \"kiw6-local-session-token\"","const AUTH_SESSION_CREATED_AT = \"2026-08-21T00:00:00.000Z\"","const AUTH_SESSION_EXPIRES_AT = \"2099-01-01T00:00:00.000Z\"","const authSessionBody = () =>","if (authMode === \"none\") return null","const body = authSessionBody();","const browserSessionCookie = Object.freeze({","browserSessionCookie, ownerId"]){if(!s.includes(x))throw new Error("KI_W6_C119_SOURCE_INVALID:"+x)}if(s.includes("const body = authMode === \"none\" ? null : { user:"))throw new Error("KI_W6_C119_OLD_ENVELOPE_PRESENT");console.log("KI_W6_C119_SOURCE_OK")'
   ```

   Require syntax exit zero and literal output `KI_W6_C119_SOURCE_OK`.
10. **Output/non-goals:** one syntax-valid helper with the exact seam/envelope.
    No browser/product/package/schema/fixture/registry/test execution, commit,
    push, provider, AWS, production or KI-W7 action.

- [ ] `C119-P1` Verify authority, predecessor, baseline and singleton scope.
  Evidence: ___
- [ ] `C119-T1` Apply CT15 items 4–7 exactly. Evidence: ___
- [ ] `C119-V1` Run both local-now checks and record results. Evidence: ___
- [ ] `C119-H1` Return the diff, ending digest and deferred C120 dependency to
  the window agent; stop `AWAITING_WINDOW_REVIEW`. Evidence: ___

#### `KI-W6-CT16` / `KI-W6-C120` — seed the opaque browser token and preserve claim limits

1. **Task ID and owner:** `KI-W6-CT16`; compile to exactly one leaf
   `KI-W6-C120` owning only
   `frontend/test/browser/keyword-intelligence-e2e.mjs`.
2. **Preconditions:** C119 is independently accepted; the browser file exists
   with post-C118 SHA-256
   `4fece32a44ab0276e71a813add6e75919453d9a46cb03f8a35c5d84f6fe146f3`;
   singleton path-set digest is
   `3dd4230266485b5b217634b4558e3aa027264534ab8a13c52ddc2f227eca9867`.
3. **Consumes:** `SRC-KI-049`, `DEC-KI-047`, accepted C119 interface. No
   alternative auth mechanism is delegable.
4. **Substitute entry:** replace only the authentication member's three text
   fields with the exact `actual`, `mayProve`, and `mustNotClaim` literals in
   `DEC-KI-047`. Preserve the member key/order and every other ledger entry.
5. **Cookie installation:** immediately after the existing `W6-FLOW-07`
   activation and before `const abortDone = armRunsResponseAbort()`, capture
   `const sessionAuthFloor = harness.trace().length;`, then add exactly one
   `Network.setCookie` call with the frozen seven fields in `DEC-KI-047`; assign its result to
   `sessionCookieResult` and assert `sessionCookieResult.success === true`.
   Then call `Network.getCookies` exactly once with `{urls:[baseUrl]}`, filter
   by `cookie.name === harness.browserSessionCookie.name`, and assert exactly
   one match with `secure === true` and `httpOnly === true`. Never compare or
   print its value. Keep the SDK cookies through the existing second
   `/runs/<id>` reload after restart. Immediately before the existing
   `harness.setAuthOwner(harness.otherOwnerId)` call, get `[baseUrl]` cookies,
   filter names beginning `__Secure-neon-auth.`, require the sorted names to
   deep-equal exactly
   `["__Secure-neon-auth.local.session_data","__Secure-neon-auth.session_token"]`,
   delete each through `Network.deleteCookies` with only its name and
   `url:baseUrl`, then get `[baseUrl]` cookies again and require zero remaining
   Neon-auth name. Immediately after the existing 100-query workspace wait,
   define `protectedWorkspaceAuthEvents` from
   `harness.trace().slice(sessionAuthFloor)` filtered to
   `kind === "auth"`, `op === "get-session"`, `mode === "owner-a"`, and
   `status === 200`; assert its length is greater than zero. Record no cookie
   or header value. Do not clear all browser cookies.
6. **Existing flow:** preserve C107 page-aware selection, C111 selection-array
   consumer, C118 revision partitions, accumulated netlog, automatic handoff
   navigation, expected `/runs/<runId>`, owner switches, no-session 401,
   restart/snapshot, owner-B/null partitions, cleanup, all 26 cases and 13
   controls. The explicit Neon-cookie deletion before the owner switch is
   required so the SDK's owner-A session-data cache cannot mask those
   partitions. Do not add a sign-in request, route exception, proxy edit, JWT
   implementation, header injection, all-cookie clear, log reset, case/control
   or certificate member.
7. **Enforcement:** the real proxy/middleware is not mocked. The existing
   `W6-NAV-01` workspace assertion is the positive witness; `W6-NC-02` and
   `W6-NC-12` remain negative controls. Missing cookie or old user-only
   envelope reproduces `EV-KI-W6-R54`; route-to-sign-in is always failure.
8. **Local-now checks:** from `frontend/`, run exactly
   `node --check test/browser/keyword-intelligence-e2e.mjs`, then:

   ```bash
   node -e 'const fs=require("node:fs");const s=fs.readFileSync("test/browser/keyword-intelligence-e2e.mjs","utf8");for(const x of ["installed Neon Auth server client and /runs middleware against deterministic loopback /get-session, with one CDP-seeded opaque local session token","actual auth-client and middleware calls, protected-workspace routing, cookie transport, and owner propagation/denial branches","live Neon Auth availability, external token issuance or validation, credential verification, cookie-cryptography assurance, or external session security","const sessionAuthFloor = harness.trace().length","const sessionCookieResult = await cdp.send(\"Network.setCookie\"","name: harness.browserSessionCookie.name","value: harness.browserSessionCookie.value","secure: true","httpOnly: true","sameSite: \"Lax\"","const installedSessionCookies = (await cdp.send(\"Network.getCookies\", { urls: [baseUrl] })).cookies.filter","installedSessionCookies.length === 1","const protectedWorkspaceAuthEvents = harness.trace().slice(sessionAuthFloor)","__Secure-neon-auth.local.session_data","await cdp.send(\"Network.deleteCookies\", { name: cookie.name, url: baseUrl })","harness.setAuthOwner(harness.otherOwnerId)"]){if(!s.includes(x))throw new Error("KI_W6_C120_SOURCE_INVALID:"+x)}if((s.match(/Network\.setCookie/g)||[]).length!==1||s.includes("Network.clearBrowserCookies"))throw new Error("KI_W6_C120_COOKIE_LIFECYCLE");console.log("KI_W6_C120_SOURCE_OK")'
   ```

   Require syntax exit zero and literal `KI_W6_C120_SOURCE_OK`. Do not run the
   causal browser gate in the leaf.
9. **Output/non-goals:** one syntax-valid causal browser harness. No helper,
   production auth/proxy/component/route/package/schema/fixture/manifest,
   provider/AWS/production/commit/push/KI-W7 action.

- [ ] `C120-P1` Verify C119 acceptance, baseline and singleton scope.
  Evidence: ___
- [ ] `C120-T1` Apply CT16 items 4–6 exactly. Evidence: ___
- [ ] `C120-V1` Run both local-now checks and record results. Evidence: ___
- [ ] `C120-H1` Return the diff, ending digest and I111 obligation to the
  window agent; stop `AWAITING_WINDOW_REVIEW`. Evidence: ___

#### Window-agent assessment `KI-W6-I111`

I111 has zero implementation-file write authority and begins only after C119
and C120 are independently accepted.

- [ ] `KI-W6-CV50` Review C119 from its pinned baseline: require only the exact
  constants, `authSessionBody`, endpoint replacement and frozen return seam;
  both local checks pass; mode A/B/null, trace and server behavior remain exact.
- [ ] `KI-W6-CV51` Review C120 from its pinned baseline: require only the exact
  ledger wording and cookie-installation block; both local checks pass; C107,
  C111 and C118 witnesses remain present; no product/proxy/auth-route or
  case/control/manifest edit.
- [ ] `KI-W6-CV52` Reuse I109 CV36–CV38 and I110 CV44 only after proving C119
  and C120 change none of their commands/imports/asserted production paths and
  the five backend correction files remain byte-identical to `EV-KI-W6-R52`.
  Preserve failed I110 CV45 as diagnostic; do not call it acceptance.
- [ ] `KI-W6-CV53` Run once from `frontend/`:
  `ALLOW_DATABASE_TESTS=true KI_W6_SKIP_BUILD=1 node test/browser/keyword-intelligence-e2e.mjs`.
  Require exit zero and the unchanged complete 26-case/13-control certificate;
  exact 19 provider-substitute calls, 23 keyword artifacts, 42 sends,
  `$0.49200000`, five seeds, 300/200/200/default-100, two successful selection
  PUTs partitioned 1/2, one 409, durable revision 3, same-key handoff retry,
  navigation through the real proxy to `/runs/<runId>` without `/sign-in`,
  100 workspace inputs, restart/snapshot proof, exact token+session-data cookie
  presence through the final owner-A protected reload, exact deletion before
  the owner switch, owner-B/no-session denial, complete cleanup and zero
  residual schema. Require at least one owner-A get-session auth trace at or
  after `sessionAuthFloor` and before workspace readiness, and zero cookie
  value or Cookie/Set-Cookie header in diagnostics/evidence.
- [ ] `KI-W6-CV54` Only after CV53 passes, run once from `email_scraper/`:
  `npm test`, then `npm run check:secrets`; require zero failures and clean scan.
- [ ] `KI-W6-CV55` Run `node scripts/build-keyword-worker.js` exactly twice
  from `email_scraper/`; require byte-identical ZIPs, sibling preservation, no
  forbidden/stale members, ZIP at most 45 MiB, unzipped at most 200 MiB and
  cold import exporting function `handler`; then run once
  `node --test --test-isolation=none test/aws-pipeline-packaging.test.js` with
  zero failures.
- [ ] `KI-W6-CV56` Recompute unchanged browser 26/13 and DB 7/3 registries and
  digests; final required=registered=executed cases exactly 35/digest
  `c5ead2a638d7f5481178730958d83b582e42aeb265536696555eaf1a08b5d5f9`
  and controls exactly 17/digest
  `62566fd91c96579a60c9f512c27cf94afdabdbc000a967a3251b177f9710c2f5`;
  zero missing, skipped, duplicate, unexpected or unactivated member and every
  control falsified.
- [ ] `KI-W6-CV57` Verify final scope/privacy/substitute claims: two correction
  files only for C119/C120; production `proxy.ts`, auth files and package bytes
  unchanged; no token value/header in evidence; no transaction contains
  provider/S3/SQS work; no provider cost/call, schema/migration/package/product/
  established-pipeline/AWS/production/destructive/commit/push/KI-W7 action.
- [ ] `KI-W6-CH11` Append the complete I111 certificate to S3, preserve and
  supersede failed I110/CV45, set S2 `READY_FOR_PARENT_REVIEW`, return one
  consolidated handoff to the parent, and stop before KI-W7.

CV53 is the sole fresh stateful browser/database gate. It may start elevated.
One identical recovery is allowed only for proven sandbox/channel invalidation
under E8.1; an observable auth, assertion, Prisma, cleanup or product failure
enters the correction loop and is not relabeled or retried as transport.

##### Ninth-correction readiness

- [x] `RW6K-001` The failure is a local auth-substitute setup gap, not a
  product proxy/navigation/repository defect. Evidence: `SRC-KI-049`.
- [x] `RW6K-002` The SDK-consumed cookie name, complete session envelope,
  deterministic values and ownership behavior are literal. Evidence:
  installed SDK source; `DEC-KI-047`.
- [x] `RW6K-003` C119 and C120 are sequential single-file leaves with exact
  baselines, interfaces, local checks and non-goals. Evidence: CT15/CT16.
- [x] `RW6K-004` Production auth remains read-only and the substitute claim is
  neither overstated nor vacuous. Evidence: `DEC-KI-047`; CV53/CV57.
- [x] `RW6K-005` Existing positive and falsification coverage owns the behavior;
  memberships/digests remain unchanged. Evidence: CV56.
- [x] `RW6K-006` Accepted database and C118 review evidence has exact reuse
  boundaries; the failed browser run remains diagnostic. Evidence: CV52.
- [x] `RW6K-007` Stateful/costly gates, invalidation, cleanup, sandbox recovery
  and stop behavior are frozen. Evidence: I111.
- [x] `RW6K-008` The window agent may manage C119→C120→I111 only, may not
  implement leaves, commit or start KI-W7. Evidence: A5 assignment.

### Tenth corrective sequence — `KI-W6-C121` then `KI-W6-I112`

This append-only correction supersedes only I111's failed CV53 badge oracle.
C119 and C120 remain accepted inputs subject to the same-file revalidation
below. It changes no product behavior and does not authorize KI-W7.

```yaml
finding: KI-W6-R57-F1
source: SRC-KI-050
decision: DEC-KI-048
violated_invariant: INV-KI-015 was misclassified as immutable source-label equality rather than stable row identity plus truthful edit provenance
sequence: [KI-W6-C121, KI-W6-I112]
changed_file_set: [frontend/test/browser/keyword-intelligence-e2e.mjs]
changed_file_set_digest_sorted_member_plus_lf_sha256: 3dd4230266485b5b217634b4558e3aa027264534ab8a13c52ddc2f227eca9867
browser_baseline_sha256: 72fe4f99420b854b537d82b769ffee71866203ff5872321538de6210faf97347
frontend_baseline_commit: a234a9eaf0e58e5ad4c74d49e8f861ae3516c7fd
backend_baseline_commit: 4d68993b13aeaab0b70ed544cfa575e2a73b0652
new_cases: 0
new_controls: 0
browser_cases_controls: 26/13 unchanged
final_cases_controls: 35/17 unchanged
provider_or_aws_cost_usd: 0.00
```

#### `KI-W6-CT17` / `KI-W6-C121` — exact edit-provenance transition oracle

1. **Owner:** compile into one leaf `KI-W6-C121`; the window agent reviews it.
2. **Writable file/baseline:** only
   `frontend/test/browser/keyword-intelligence-e2e.mjs`, SHA-256
   `72fe4f99420b854b537d82b769ffee71866203ff5872321538de6210faf97347`
   at frontend commit `a234a9eaf0e58e5ad4c74d49e8f861ae3516c7fd`.
   Singleton path digest is
   `3dd4230266485b5b217634b4558e3aa027264534ab8a13c52ddc2f227eca9867`.
3. **Consumes:** `SRC-KI-050`, `DEC-KI-048`, accepted C119/C120 and diagnostic
   `EV-KI-W6-R57`; no discovery or behavior choice remains.
4. **Exact edit:** immediately after
   `const beforeBadges = await queryRowBadges();`, insert:

   ```js
   assert(beforeBadges.length === 100 && beforeBadges.every((badge) => badge === "generated"), "keyword-research handoff rows must begin with generated provenance");
   ```

   Replace only the later assertion whose message is
   `"keyword source lineage must remain unchanged"` with:

   ```js
   const expectedEditedBadges = beforeBadges.map((badge) => badge === "generated" ? "user edited" : badge);
   const swappedExpectedBadges = [expectedEditedBadges[1], expectedEditedBadges[0], ...expectedEditedBadges.slice(2)];
   assert(arrayEqual(afterBadges, swappedExpectedBadges), "edited query provenance must change from generated to user edited and follow the persisted reorder");
   ```

   In the immediately following `captured.workspace`, replace only
   `badgesPreserved: true` with `provenanceTransitionVerified: true`.
5. **Preserve:** `queryRowBadges`, both value arrays, edit-all-100, first-row
   move, save/reload, `expectedOrder`, `swapped`, every count/text/order/
   persistence/zero-add-delete assertion, the `W6-FLOW-09` activation literal,
   C107/C111/C118/C120 blocks, auth/cookie lifecycle, registries, certificate,
   cleanup and all later phases.
6. **Enforcement:** zero/non-100 or any non-generated pre-edit badge fails;
   unchanged, wrong, missing, extra or wrongly reordered post-edit badges fail.
   Sorted/set/count/permissive alternatives are prohibited.
7. **Local-now checks:** from `frontend/`, run exactly:

   ```bash
   node --check test/browser/keyword-intelligence-e2e.mjs
   node -e 'const fs=require("node:fs"),a=require("node:assert/strict");const s=fs.readFileSync("test/browser/keyword-intelligence-e2e.mjs","utf8");for(const x of ["beforeBadges.length === 100 && beforeBadges.every((badge) => badge === \"generated\")","const expectedEditedBadges = beforeBadges.map((badge) => badge === \"generated\" ? \"user edited\" : badge);","const swappedExpectedBadges = [expectedEditedBadges[1], expectedEditedBadges[0], ...expectedEditedBadges.slice(2)];","arrayEqual(afterBadges, swappedExpectedBadges)","provenanceTransitionVerified: true"]){if(!s.includes(x))throw new Error("KI_W6_C121_SOURCE_INVALID:"+x)}for(const x of ["keyword source lineage must remain unchanged","badgesPreserved: true"]){if(s.includes(x))throw new Error("KI_W6_C121_STALE_ORACLE:"+x)}const before=["generated","user added","user edited"];const projected=before.map((badge)=>badge==="generated"?"user edited":badge);const expected=[projected[1],projected[0],...projected.slice(2)];a.deepEqual(expected,["user added","user edited","user edited"]);a.throws(()=>a.deepEqual(["user added","generated","user edited"],expected));console.log("KI_W6_C121_SOURCE_AND_NEGATIVE_CONTROL_OK")'
   ```

   Require both exits zero and the literal final marker. The leaf does not run
   the causal browser gate.
8. **Output/non-goals:** one corrected test oracle. No helper, production code,
   API, database, schema, fixture, manifest, registry, package, build input,
   provider, AWS, production, commit, push or KI-W7 action.

- [ ] `C121-P1` Verify assignment, accepted inputs, baseline and scope. Evidence: ___
- [ ] `C121-T1` Apply item 4 exactly and preserve item 5. Evidence: ___
- [ ] `C121-V1` Run both local-now checks. Evidence: ___
- [ ] `C121-H1` Return diff/digest/preservation proof; stop for window review. Evidence: ___

#### Window-agent assessment `KI-W6-I112`

I112 has zero implementation-file write authority and begins only after C121
is independently accepted.

- [ ] `KI-W6-CV58` Review C121 from its baseline, run its two checks and prove
  one-file scope. Re-run C120's CT16-item-8 source-preservation check and require
  all cookie/auth markers plus C107/C111/C118 witnesses. Verify no case/control/
  registry/manifest/certificate member changed. Supersede only C120's old
  whole-file digest/CV51 source review, not its accepted auth behavior.
- [ ] `KI-W6-CV59` Reuse I111 CV50/CV52 only after the C119 helper and five
  backend files rehash byte-equal to `EV-KI-W6-R55/R57`; keep failed CV53
  diagnostic. Run once from `frontend/`:
  `ALLOW_DATABASE_TESTS=true KI_W6_SKIP_BUILD=1 node test/browser/keyword-intelligence-e2e.mjs`.
  Require exit zero, unchanged 26-case/13-control certificate, every CV53 auth/
  cookie/navigation/provider/artifact/cost/cleanup witness, and W6-FLOW-09 with
  exactly 100 pre-edit `generated` badges, 100 post-edit `user edited` badges in
  persisted swapped order, all texts edited, zero add/delete and later restart/
  snapshot deep equality.
- [ ] `KI-W6-CV60` After CV59, run once from `email_scraper/`: `npm test`, then
  `npm run check:secrets`; require zero failures and clean scan.
- [ ] `KI-W6-CV61` From `email_scraper/`, run
  `node scripts/build-keyword-worker.js` exactly twice; require byte-identical
  ZIPs, sibling preservation, no forbidden/stale members, ZIP <=45 MiB,
  unzipped <=200 MiB and cold import exporting function `handler`; then run
  once `node --test --test-isolation=none test/aws-pipeline-packaging.test.js`
  with zero failures.
- [ ] `KI-W6-CV62` Recompute unchanged browser 26/13 and DB 7/3 registries and
  digests; final cases exactly 35/digest
  `c5ead2a638d7f5481178730958d83b582e42aeb265536696555eaf1a08b5d5f9`
  and controls exactly 17/digest
  `62566fd91c96579a60c9f512c27cf94afdabdbc000a967a3251b177f9710c2f5`;
  require exact required=registered=executed equality, zero skips/duplicates/
  unexpected/unactivated members and every control falsified.
- [ ] `KI-W6-CV63` Verify C121 changed only its browser test; C119 helper and
  all production/proxy/auth/API/repository/schema/package/build-input bytes
  retain accepted baselines; no token/header/private value in evidence and no
  provider/AWS/production/destructive/commit/push/KI-W7 action.
- [ ] `KI-W6-CH12` Append I112 certificate to S3, supersede failed I111 CV53
  and only C120's prior whole-file digest, set S2 `READY_FOR_PARENT_REVIEW`,
  return one consolidated handoff, and stop before KI-W7.

CV59 is the sole fresh stateful browser/database gate and may start elevated.
Only a proven sandbox/channel invalidation permits one identical E8.1 recovery;
an observable assertion, Prisma, cleanup or product failure is not retried.

##### Tenth-correction readiness

- [x] `RW6L-001` Impossible oracle, not product defect. Evidence: `SRC-KI-050`.
- [x] `RW6L-002` Identity/provenance distinction is exact. Evidence: `DEC-KI-048`.
- [x] `RW6L-003` One file, baseline, anchors and edit are exact. Evidence: CT17.
- [x] `RW6L-004` Oracle is non-vacuous/order-sensitive and falsified locally. Evidence: CT17.
- [x] `RW6L-005` Cases, controls and digests are unchanged. Evidence: CV62.
- [x] `RW6L-006` Invalidation/reuse boundaries are exact. Evidence: CV58/CV59.
- [x] `RW6L-007` Gates, recovery, cleanup and stop are frozen. Evidence: I112.
- [x] `RW6L-008` Window agent manages C121→I112 only; no commit/KI-W7. Evidence: A5 state 166.

### Eleventh corrective sequence — `KI-W6-C122`, `KI-W6-C123`, then `KI-W6-I113`

This append-only correction supersedes only I112's failed CV59 harness-
orchestration attempt. C121 remains accepted. It changes no production behavior,
case/control membership, provider economics or locked downstream fault schedule,
and does not authorize KI-W7.

```yaml
finding: KI-W6-R59-F1
source: SRC-KI-051
decision: DEC-KI-049
violated_invariant: the causal browser harness must execute the production run-start callback before measuring confirmation while preserving later discovery/domain fault partitions
sequence: [KI-W6-C122, KI-W6-C123, KI-W6-I113]
changed_file_set: [email_scraper/test/helpers/keyword-intelligence-e2e-harness.js, frontend/test/browser/keyword-intelligence-e2e.mjs]
changed_file_set_digest_sorted_member_plus_lf_sha256: 4f0d4befb9a6d1cdb039108cf271c25ed23265436fdf856866e93caeef179628
helper_baseline_sha256: cbcd304aea6657bef10d73644d81e253396fe3f4f3f112f9dc03e020f0c7db74
browser_baseline_sha256: 8d89bb198390c3f7baf431ccd3405693c5003eb8a9ee4f0e7ccd75c254d507d0
helper_expected_ending_sha256: d9a76cebad80650f5a601012eaaa4715e16a6b6ce334000c98a56470ab6fa6fe
browser_expected_ending_sha256: 448921c77cb0a1619e004d2c8587faa53e0598736605d95a0c7ff9fbf4e13b99
backend_baseline_commit: 4d68993b13aeaab0b70ed544cfa575e2a73b0652
frontend_baseline_commit: a234a9eaf0e58e5ad4c74d49e8f861ae3516c7fd
new_cases: 0
new_controls: 0
browser_cases_controls: 26/13 unchanged
final_cases_controls: 35/17 unchanged
provider_or_aws_cost_usd: 0.00
```

#### `KI-W6-CT18` / `KI-W6-C122` — one-shot run-start schedule seam

1. **Owner/order:** compile into one leaf `KI-W6-C122`; the window agent reviews
   and accepts it before assigning C123.
2. **Writable file/baseline:** only
   `email_scraper/test/helpers/keyword-intelligence-e2e-harness.js`, SHA-256
   `cbcd304aea6657bef10d73644d81e253396fe3f4f3f112f9dc03e020f0c7db74`
   at backend commit `4d68993b13aeaab0b70ed544cfa575e2a73b0652`. Singleton
   path digest is
   `7549f43fbf304b87491bb6d7758f09ea4b9d237153c7fe7ff2554fef5f125fe4`.
3. **Consumes:** `SRC-KI-051`, `DEC-KI-049`, the existing
   `scheduledCallbacks`, `schedule`, `flushSchedule`, `record`, `nowMs` and
   `HarnessPreflightError` symbols. Do not discover or select another seam.
4. **Exact edit:** immediately after the unchanged `flushSchedule` definition,
   add exactly:

   ```js
   const flushRunStartSchedule = () => {
     const pendingBefore = scheduledCallbacks.length;
     if (pendingBefore !== 1) {
       throw new preflightError(`expected exactly one parked run-start callback, saw ${pendingBefore}`);
     }
     const callback = scheduledCallbacks.shift();
     callback();
     const pendingAfter = scheduledCallbacks.length;
     if (pendingAfter !== 0) {
       throw new preflightError(`run-start flush left ${pendingAfter} parked callbacks`);
     }
     const witness = Object.freeze({ pendingBefore, flushedCallbacks: 1, pendingAfter });
     record({ kind: "harness", op: "flush-run-start-schedule", at: nowMs(), ...witness });
     return witness;
   };
   ```

   In the sole final `Object.freeze` return, insert only
   `flushRunStartSchedule` between `restartBackend` and `drainDownstream`.
5. **Interface/failure:** export exactly the synchronous signature and frozen
   return described by DEC-KI-049. Zero/multiple pending callbacks or a callback
   that synchronously parks another callback throws `HarnessPreflightError`.
   Invoke the callback once without awaiting it; the existing causal trace and
   durable waits own asynchronous completion and failure evidence.
6. **Preserve:** `schedule`, `flushSchedule`, `setIntervalFn`, `clearIntervalFn`,
   `drainKeywordWork`, `drainDownstream`, queue order/IDs, all fault injection,
   auth/session values, provider fixtures, cleanup, schema isolation and every
   production file. No new timer, poller or queue consumer.
7. **Local-now checks:** from `email_scraper/`, run exactly:

   ```bash
   node --check test/helpers/keyword-intelligence-e2e-harness.js
   node -e 'const fs=require("node:fs"),a=require("node:assert/strict"),{createHash}=require("node:crypto");const s=fs.readFileSync("test/helpers/keyword-intelligence-e2e-harness.js","utf8");const check=(x)=>{for(const v of ["const flushRunStartSchedule = () => {","if (pendingBefore !== 1)","const callback = scheduledCallbacks.shift();","callback();","if (pendingAfter !== 0)","op: \"flush-run-start-schedule\"","restartBackend, flushRunStartSchedule, drainDownstream"]){if(!x.includes(v))throw new Error("KI_W6_C122_SOURCE_INVALID:"+v)}if((x.match(/const flushRunStartSchedule =/g)||[]).length!==1)throw new Error("KI_W6_C122_DUPLICATE")};check(s);a.throws(()=>check(s.replace("    callback();","    void callback;")));const digest=createHash("sha256").update(s).digest("hex");a.equal(digest,"d9a76cebad80650f5a601012eaaa4715e16a6b6ce334000c98a56470ab6fa6fe");console.log("KI_W6_C122_SOURCE_AND_NEGATIVE_CONTROL_OK")'
   ```

8. **Output/non-goals:** exact ending SHA-256
   `d9a76cebad80650f5a601012eaaa4715e16a6b6ce334000c98a56470ab6fa6fe`.
   No browser, product, database schema, fixture, manifest, registry, package,
   provider, AWS, production, commit, push or KI-W7 action.

- [ ] `C122-P1` Verify assignment, baseline and one-file scope. Evidence: ___
- [ ] `C122-T1` Apply item 4 exactly and preserve item 6. Evidence: ___
- [ ] `C122-V1` Run both local-now checks and match the ending digest. Evidence: ___
- [ ] `C122-H1` Return diff/digest/preservation proof; stop for window review. Evidence: ___

#### `KI-W6-CT19` / `KI-W6-C123` — invoke the seam at the confirmation boundary

1. **Owner/order:** after C122 is independently accepted, compile into one leaf
   `KI-W6-C123`; the window agent reviews it before I113.
2. **Writable file/baseline:** only
   `frontend/test/browser/keyword-intelligence-e2e.mjs`, accepted C121 SHA-256
   `8d89bb198390c3f7baf431ccd3405693c5003eb8a9ee4f0e7ccd75c254d507d0`.
   Singleton path digest is
   `3dd4230266485b5b217634b4558e3aa027264534ab8a13c52ddc2f227eca9867`.
3. **Consumes:** the exact C122 frozen export and existing run-start,
   `googlePairsFloor`, confirmation, discovery, fault-injection and downstream
   symbols. C123 makes no orchestration choice.
4. **Exact edit:** immediately after
   `const googlePairsFloor = harness.trace().length;` and before
   `const confirmDeadline = Date.now() + 120000;`, add exactly:

   ```js
   const runStartSchedule = harness.flushRunStartSchedule();
   assert(
     runStartSchedule.pendingBefore === 1 &&
       runStartSchedule.flushedCallbacks === 1 &&
       runStartSchedule.pendingAfter === 0,
     "run start must flush exactly one parked queue-drain callback"
   );
   captured.confirmationDrain = structuredClone(runStartSchedule);
   ```

5. **Ordered behavior:** retain the observed run-start POST first; capture the
   Google trace floor; flush exactly once; validate/store the witness; then run
   the unchanged 100-call wait, confirmation terminal assertion, 100-delivery
   wait, duplicate/reorder discovery injection, later `drainDownstream`, partial
   domain-check sample, domain-check injections and 1,000-domain assertions.
6. **Preserve:** every C107/C111/C118/C120/C121 edit and oracle; the C121
   generated→user-edited order witness; all auth/cookie lifecycle; the existing
   `W6-FLOW-10`–`12` registrations, `W6-NC-07/08`, 26/13 registries, certificate,
   cleanup, browser command and downstream fault positions. Do not start
   `drainDownstream` earlier.
7. **Local-now checks:** from `frontend/`, run exactly:

   ```bash
   node --check test/browser/keyword-intelligence-e2e.mjs
   node -e 'const fs=require("node:fs"),a=require("node:assert/strict"),{createHash}=require("node:crypto");const s=fs.readFileSync("test/browser/keyword-intelligence-e2e.mjs","utf8");const check=(x)=>{for(const v of ["const googlePairsFloor = harness.trace().length;","const runStartSchedule = harness.flushRunStartSchedule();","runStartSchedule.pendingBefore === 1","runStartSchedule.flushedCallbacks === 1","runStartSchedule.pendingAfter === 0","captured.confirmationDrain = structuredClone(runStartSchedule);","const confirmDeadline = Date.now() + 120000;"]){if(!x.includes(v))throw new Error("KI_W6_C123_SOURCE_INVALID:"+v)}if((x.match(/harness\.flushRunStartSchedule\(\)/g)||[]).length!==1)throw new Error("KI_W6_C123_CALL_COUNT");const order=["run start request","const googlePairsFloor = harness.trace().length;","const runStartSchedule = harness.flushRunStartSchedule();","const confirmDeadline = Date.now() + 120000;","oracles.googleValidation(captured.confirmation);","const discoveryFloor = harness.trace().length;","await harness.injectCapturedDefect(\"duplicate-next-discovery-message\")","const downstreamPromise = harness.drainDownstream();"].map(v=>x.indexOf(v));if(order.some(v=>v<0)||order.some((v,i)=>i>0&&v<=order[i-1]))throw new Error("KI_W6_C123_ORDER")};check(s);a.throws(()=>check(s.replace("const runStartSchedule = harness.flushRunStartSchedule();","const runStartSchedule = { pendingBefore: 1, flushedCallbacks: 1, pendingAfter: 0 };")));const digest=createHash("sha256").update(s).digest("hex");a.equal(digest,"448921c77cb0a1619e004d2c8587faa53e0598736605d95a0c7ff9fbf4e13b99");console.log("KI_W6_C123_SOURCE_AND_NEGATIVE_CONTROL_OK")'
   ```

8. **Output/non-goals:** exact ending SHA-256
   `448921c77cb0a1619e004d2c8587faa53e0598736605d95a0c7ff9fbf4e13b99`.
   No helper/product/API/database/schema/fixture/manifest/registry/package/
   provider/AWS/production/commit/push/KI-W7 action.

- [ ] `C123-P1` Verify accepted C122, C121 baseline and one-file scope. Evidence: ___
- [ ] `C123-T1` Apply item 4 at the exact item-5 boundary. Evidence: ___
- [ ] `C123-V1` Run both local-now checks and match the ending digest. Evidence: ___
- [ ] `C123-H1` Return diff/digest/preservation proof; stop for window review. Evidence: ___

#### Window-agent assessment `KI-W6-I113`

I113 has zero implementation-file write authority and begins only after C122
and C123 are independently accepted.

- [ ] `KI-W6-CV64` Review C122 from helper baseline `cbcd304a…` and C123 from
  browser baseline `8d89bb19…`; require exact endings `d9a76ceb…` and
  `448921c7…`, the two-file path-set digest `4f0d4bef…`, both leaves' local
  checks, and no third implementation path. Revalidate every accepted C119
  auth/session marker and C120/C121 cookie/provenance marker. Prove no
  case/control/registry/manifest/certificate member changed. Supersede only
  C119's helper whole-file digest and C121's browser whole-file digest/source
  review, not their accepted behavior.
- [ ] `KI-W6-CV65` Preserve I112 CV58 and its five-production-file dependency
  proof after exact rehash; keep failed CV59 diagnostic. From `frontend/`, run
  once, elevated when needed:
  `ALLOW_DATABASE_TESTS=true KI_W6_SKIP_BUILD=1 node test/browser/keyword-intelligence-e2e.mjs`.
  Require exit zero and the unchanged 26-case/13-control certificate. Require
  the run-start POST precedes one safe `flush-run-start-schedule` trace with
  witness exactly `1/1/0`; then exactly 100 validator/parser calls, 1,000
  occurrences, terminal confirmation, 100 discovery deliveries/tasks, the
  unchanged duplicate/reorder fault points, 1,000 stable domains/lead tasks,
  all C119–C121 auth/navigation/provenance witnesses, and complete schema-
  absence cleanup. Zero, multiple, reordered or late flushes fail.
- [ ] `KI-W6-CV66` After CV65, run once from `email_scraper/`: `npm test`, then
  `npm run check:secrets`; require zero failures and a clean scan.
- [ ] `KI-W6-CV67` From `email_scraper/`, run
  `node scripts/build-keyword-worker.js` exactly twice; require byte-identical
  ZIPs, sibling preservation, no forbidden/stale members, ZIP <=45 MiB,
  unzipped <=200 MiB and cold import exporting function `handler`; then run
  once `node --test --test-isolation=none test/aws-pipeline-packaging.test.js`
  with zero failures.
- [ ] `KI-W6-CV68` Recompute unchanged browser 26/13 and DB 7/3 registries and
  digests; final cases exactly 35/digest
  `c5ead2a638d7f5481178730958d83b582e42aeb265536696555eaf1a08b5d5f9`
  and controls exactly 17/digest
  `62566fd91c96579a60c9f512c27cf94afdabdbc000a967a3251b177f9710c2f5`;
  require required=registered=executed equality, zero skips/duplicates/
  unexpected/unactivated members and every control falsified.
- [ ] `KI-W6-CV69` Verify exactly the two correction files differ from their
  parent baselines; all production/proxy/auth/API/repository/schema/package/
  build-input bytes retain accepted baselines; no token/cookie/header/private
  value in evidence and no provider/AWS/production/destructive/commit/push/
  KI-W7 action.
- [ ] `KI-W6-CH13` Append the I113 enforcement/integration certificate to S3,
  supersede failed I112 CV59 and only the two prior whole-file digest/source
  reviews named in CV64, set S2 `READY_FOR_PARENT_REVIEW`, return one
  consolidated handoff, and stop before KI-W7.

CV65 is the sole fresh stateful browser/database gate and may start elevated.
Only a proven sandbox/channel invalidation permits one identical E8.1 recovery;
an observable assertion, Prisma, cleanup or product failure is not retried.

##### Eleventh-correction readiness

- [x] `RW6M-001` The deadlock and sole callback path are source-proven. Evidence: `SRC-KI-051` / `EV-KI-W6-R59`.
- [x] `RW6M-002` Test-harness correction, not product behavior, is exact. Evidence: `DEC-KI-049`.
- [x] `RW6M-003` Two sequential single-file leaves have exact baselines, edits, interfaces and endings. Evidence: CT18/CT19.
- [x] `RW6M-004` The flush is one-shot, ordered after the start witness and before the Google floor's wait. Evidence: CT18/CT19.
- [x] `RW6M-005` Existing cases, controls, fault partitions and digests are unchanged and non-vacuous. Evidence: CV65/CV68.
- [x] `RW6M-006` Accepted-test invalidation and source-marker revalidation are exact. Evidence: CV64/CV65.
- [x] `RW6M-007` Stateful gate, recovery, cleanup, regressions and stop are frozen. Evidence: I113.
- [x] `RW6M-008` Window agent manages C122→C123→I113 only; no commit/KI-W7. Evidence: A5 state 167.

### Twelfth corrective sequence — parent-direct `KI-W6-C124`, then window-agent `KI-W6-I114`

This append-only correction supersedes only DEC-KI-049's unsatisfiable
one-callback witness and I113's failed CV65. The requester explicitly directed
the parent to ship the exact two-file test-harness fix and return the remaining
assessment to the window agent. No leaf or product implementation is involved.

```yaml
finding: KI-W6-R63-F1
source: SRC-KI-052
decision: DEC-KI-050
sequence: [KI-W6-C124-parent-direct, KI-W6-I114-window-agent]
changed_file_set: [email_scraper/test/helpers/keyword-intelligence-e2e-harness.js, frontend/test/browser/keyword-intelligence-e2e.mjs]
changed_file_set_digest_sorted_member_plus_lf_sha256: 4f0d4befb9a6d1cdb039108cf271c25ed23265436fdf856866e93caeef179628
helper_baseline_sha256: d9a76cebad80650f5a601012eaaa4715e16a6b6ce334000c98a56470ab6fa6fe
browser_baseline_sha256: 448921c77cb0a1619e004d2c8587faa53e0598736605d95a0c7ff9fbf4e13b99
helper_expected_ending_sha256: bc38c6320e4ceb4e14f0f781d08923ec2271388330f0dbb1bdf0761c7ec11557
browser_expected_ending_sha256: 8105d20460cdb09607e58f2a425063eeb39eae8585f621178fa9f8e036b8b231
backend_baseline_commit: 70af619814ec026e51dccb985b0fc0f732169309
frontend_baseline_commit: 3d97150f4736ce2ee3e6c754c67206d271479639
new_cases: 0
new_controls: 0
browser_cases_controls: 26/13 unchanged
final_cases_controls: 35/17 unchanged
provider_or_aws_cost_usd: 0.00
```

#### Parent-direct `KI-W6-C124` — restart-aware live-callback selection

1. **Authority/scope:** A5 state 168 plus the requester's direct instruction
   authorize the parent to change only the two paths in the YAML block above,
   then run syntax/source/digest/diff checks. No S1/S2/S3 edit, leaf dispatch,
   stateful gate or successor work belongs to C124.
2. **Helper edit:** starting from exact SHA `d9a76ceb…`, replace only the C122
   cardinality/removal/witness lines so `pendingBefore!==2` throws
   `expected one stale and one live run-start callback, saw <n>`; select the
   live callback with `scheduledCallbacks.pop()`; set
   `discardedStaleCallbacks=scheduledCallbacks.length`; clear the array; invoke
   `liveCallback()` once; preserve the zero-remain check; and freeze/record
   `{pendingBefore,discardedStaleCallbacks,flushedCallbacks:1,pendingAfter}`.
   Exact ending SHA is `bc38c632…`; exact diff is 7 insertions/5 deletions.
3. **Browser edit:** starting from exact SHA `448921c7…`, change only the C123
   witness assertion to require, in order, `pendingBefore===2`,
   `discardedStaleCallbacks===1`, `flushedCallbacks===1`, and
   `pendingAfter===0`, with message `run start must discard one stale callback
   and flush exactly one live callback`. Exact ending SHA is `8105d204…`;
   exact diff is 3 insertions/2 deletions.
4. **Preserve:** the seam/caller position, trace op, captured member, Google
   floor, confirmation/discovery waits, every later fault injection and drain,
   C119–C123 auth/provenance behavior, all cases/controls/registries/digests,
   cleanup and every production file. Do not invoke the stale callback.
5. **Local enforcement:** both `node --check` commands pass. The exact-source
   checker must find the `2/pop/discard/clear/live/2-1-1-0` members in their
   accepted order, fail after substituting `shift()` for `pop()`, fail after
   deleting the discarded-stale assertion, and match both ending hashes.
   `git diff --check` passes and each nested diff names only its owned file.

- [x] `C124-P1` Exact C122/C123 baselines and two-file scope verified. Evidence: `EV-KI-A-107`.
- [x] `C124-T1` Exact helper and browser replacements applied. Evidence: `EV-KI-A-107`.
- [x] `C124-V1` Syntax, source, two negative controls, hashes and diff scope passed. Evidence: `EV-KI-A-107`.
- [x] `C124-H1` No test/build/database/provider/AWS/production/commit/KI-W7 action occurred. Evidence: `EV-KI-A-107`.

#### Window-agent assessment `KI-W6-I114`

I114 has zero implementation-file write authority. The window agent first
transcribes/reconciles this exact parent correction in S1/S2/S3, independently
reviews the already-applied two-file patch, and then executes these gates in
order. No leaf is launched.

- [ ] `KI-W6-CV70` Recompute the exact two baselines/endings, two-path digest,
  source members, 7/5 and 3/2 diffs, syntax and both negative controls. Require
  exactly the helper and browser paths dirty relative to the pinned commits.
  Revalidate every accepted C119–C123 auth/cookie/provenance/scheduler marker
  and prove no case/control/registry/manifest/certificate member changed.
- [ ] `KI-W6-CV71` Preserve I113 CV64 and failed CV65 diagnostics. From
  `frontend/`, run once, elevated when needed:
  `ALLOW_DATABASE_TESTS=true KI_W6_SKIP_BUILD=1 node test/browser/keyword-intelligence-e2e.mjs`.
  Require exit zero, the unchanged 26-case/13-control certificate, exactly one
  `flush-run-start-schedule` trace with witness `2/1/1/0`, 100 validator/parser
  calls, 1,000 occurrences, terminal confirmation, 100 discovery tasks, the
  unchanged duplicate/reorder fault points, 1,000 stable domains/lead tasks,
  all auth/navigation/provenance/restart witnesses and schema-absence cleanup.
- [ ] `KI-W6-CV72` After CV71, run once from `email_scraper/`: `npm test`, then
  `npm run check:secrets`; require zero failures and a clean scan.
- [ ] `KI-W6-CV73` From `email_scraper/`, run
  `node scripts/build-keyword-worker.js` exactly twice; require byte-identical
  ZIPs, sibling preservation, no forbidden/stale members, ZIP <=45 MiB,
  unzipped <=200 MiB and cold import exporting function `handler`; then run
  once `node --test --test-isolation=none test/aws-pipeline-packaging.test.js`
  with zero failures.
- [ ] `KI-W6-CV74` Recompute unchanged browser 26/13 and DB 7/3 registries and
  digests; final cases exactly 35/digest
  `c5ead2a638d7f5481178730958d83b582e42aeb265536696555eaf1a08b5d5f9`
  and controls exactly 17/digest
  `62566fd91c96579a60c9f512c27cf94afdabdbc000a967a3251b177f9710c2f5`;
  require required=registered=executed equality and every control falsified.
- [ ] `KI-W6-CV75` Verify only the two C124 files differ from the pinned
  commits; all production/proxy/auth/API/repository/schema/package/build-input
  bytes retain accepted baselines; evidence contains no secret/private value;
  no provider/AWS/production/destructive/commit/push/KI-W7 action occurred.
- [ ] `KI-W6-CH14` Append the I114 certificate to S3, supersede only failed
  I113 CV65 and the C122/C123 whole-file digest/source reviews, set S2
  `READY_FOR_PARENT_REVIEW`, return one consolidated handoff and stop.

CV71 is the sole fresh stateful browser/database gate and may start elevated.
Only a proven sandbox/channel invalidation permits one identical E8.1 recovery;
an observable assertion, Prisma, cleanup or product failure is not retried.

##### Twelfth-correction readiness

- [x] `RW6N-001` The exact two-callback state and ordering are source/evidence proven. Evidence: `SRC-KI-052`.
- [x] `RW6N-002` The stale/live choice and failure semantics are parent-locked. Evidence: `DEC-KI-050`.
- [x] `RW6N-003` Exact baselines, replacements, endings and diff sizes are frozen. Evidence: C124 items 1–3.
- [x] `RW6N-004` Two independent negative controls reject FIFO invocation and a missing stale witness. Evidence: C124-V1.
- [x] `RW6N-005` Stateful causality, cleanup and existing coverage remain non-vacuous. Evidence: CV71/CV74.
- [x] `RW6N-006` Reuse/invalidation boundaries are exact. Evidence: CV70/CV71.
- [x] `RW6N-007` Expensive gates, recovery and stop are frozen. Evidence: I114.
- [x] `RW6N-008` The window agent owns reconciliation/review/assessment only; no leaf or KI-W7. Evidence: A5 state 169.

## 5. Final independent review (not assigned to implementation agents)

### Thirteenth corrective sequence — parent-direct `KI-W6-C125`/`C126`, then window-agent `KI-W6-I115`

This append-only sequence supersedes only failed I114 CV71. The requester
directed the parent to implement the diagnosed correction and hand the
remaining W6 assessment back to the window agent.

#### Parent-direct `KI-W6-C125` — one-file repository correction

- [x] `C125-P1` Verify `src/prisma-run-repository.js` starts at SHA-256
  `d4995ef9e177dbf9f0fad5c199b9c8f5e63fd37122919ba256aa1282f842db27`.
- [x] `C125-T1` In `saveQueryValidation` only, enforce an array of at most 100
  unique IDs; retain the live lease-fenced Run stage update; select the scoped
  schema; replace the per-row loop with one typed `jsonb_to_recordset` update;
  preserve nullable/omitted JSON semantics; set `updatedAt=now`; require exact
  returned-ID reconciliation; and pass exactly
  `{maxWait:5_000,timeout:30_000}` to this transaction only.
- [x] `C125-V1` `node --check src/prisma-run-repository.js` and a source oracle
  prove one bulk update, no per-row database loop, exact profile and exact
  reconciliation. Negative controls removing the returned-ID check and
  restoring a per-row update must falsify the oracle.
- [x] `C125-H1` No schema/package/provider/AWS/frontend/commit/KI-W7 action.

#### Parent-direct `KI-W6-C126` — one-file focused regression

- [x] `C126-P1` Verify `test/prisma-run-repository.integration.test.js` starts
  at SHA-256
  `f19d7c86127846b8f38c9d02f4eae7b6498357786bfec7afb8186b3117e08eb0`.
- [x] `C126-T1` Add one focused isolated-schema scenario proving 100 unique
  query rows persist with exact values; an unreconciled ID rolls back all row
  mutations and the Run stage; a lost lease mutates nothing; and cleanup drops
  and verifies absence of the disposable schema. Add a transaction-spy oracle
  proving the exact 30-second profile and one bulk mutation.
- [x] `C126-V1` Run syntax, the non-DB profile oracle, then the single named DB
  scenario once with the isolated test URL. Require zero skip/failure and
  schema absence. A sequential/default-timeout source substitute must fail the
  operation/profile oracle without depending on host timing.
- [x] `C126-H1` No full DB suite, provider/AWS/production/commit/KI-W7 action.

#### Window-agent assessment `KI-W6-I115`

The window agent reconciles and independently reviews C125/C126, then runs the
focused non-DB and single DB checks once, followed by one fresh causal browser
gate. If it passes, continue the previously frozen CV72–CV75/CH14 closure. A
proven environment invalidation permits the standards-defined identical
elevated recovery; an observable product/test failure is diagnosed and handled
under the existing correction rule. No leaf is required for the already
parent-applied files, no commit is permitted, and KI-W7 remains prohibited.

- [ ] `KI-W6-CV76` Independent two-file diff/source/profile/privacy review.
- [ ] `KI-W6-CV77` Focused non-DB profile oracle and one isolated-schema 100-row
  regression, with zero skips and verified schema absence.
- [ ] `KI-W6-CV78` One fresh unchanged causal browser command; require all
  existing 26 cases/13 controls, 100 validations, 100 discovery tasks, 1,000
  domains/leads, cleanup and schema absence.
- [ ] `KI-W6-CV79` On CV78 success, resume CV72–CV75 exactly and append the
  consolidated `READY_FOR_PARENT_REVIEW` handoff.

##### Thirteenth-correction readiness

- [x] `RW6O-001` Exact failure location and causal boundary are observed. Evidence: `SRC-KI-053`.
- [x] `RW6O-002` Transaction, batching, reconciliation and timeout choices are parent-locked. Evidence: `DEC-KI-051`.
- [x] `RW6O-003` Production and test ownership are two exact single-file units. Evidence: C125/C126.
- [x] `RW6O-004` Rollback, lost-fence, operation-count and timing-independent controls are mandatory. Evidence: C126.
- [x] `RW6O-005` Provider economics and established downstream behavior are unchanged. Evidence: `DEC-KI-051`.
- [x] `RW6O-006` Stateful reruns and stop boundaries are exact. Evidence: I115.
- [x] `RW6O-007` Parent implements; window agent independently reviews and assesses. Evidence: requester instruction/A5.
- [x] `RW6O-008` KI-W7 remains prohibited. Evidence: A5.

- [ ] `KI-FR-1` Independently inspect current source/diff, active hashes, every accepted window, and changed-file scope.
- [ ] `KI-FR-2` Re-run representative nonempty local E2E, maximum scale, payload negative controls, ownership/lease races, and emitted builds.
- [ ] `KI-FR-3` If W8 occurred, independently validate deployed hashes, applied capabilities, one canary trace, cost, privacy, and mutation scope.
- [ ] `KI-FR-4` Reconcile every implementation/verification/handoff box, A6 evidence, A7 invalidations, and A8 trace.
- [ ] `KI-FR-5` Confirm zero guessed payloads, delegated decisions, unaccepted required windows, or overstated parity claims.
- [ ] `KI-FR-6` Only the independent parent may mark the integration complete; otherwise append a uniquely identified corrective window and stop.

## 6. Current readiness result

Checked mandatory parent-standard items: **93**. Checked recursive KI-R4
items: **10**. Checked W4 authoring supplements: **12**. Checked KI-R5
corrective supplements: **12**. Checked KI-W6 reauthoring supplements: **12**.
Checked KI-W6 in-flight corrective supplements: **8**.
Checked KI-W6 second-correction supplements: **8**.
Checked KI-W6 third-correction supplements: **8**.
Checked KI-W6 fourth-correction supplements: **10**.
Checked KI-W6 fifth-correction supplements: **8**.
Checked KI-W6 sixth-correction supplements: **8**.
Checked KI-W6 seventh-correction supplements: **10**.
Checked KI-W6 eighth-correction supplements: **8**.
Checked KI-W6 ninth-correction supplements: **8**.
Checked KI-W6 tenth-correction supplements: **8**.
Checked KI-W6 eleventh-correction supplements: **8**.
Checked KI-W6 twelfth-correction supplements: **8**.
Checked KI-W6 thirteenth-correction supplements: **8**.
Unchecked required authoring items: **0**.

KI-R5 is accepted and closed by `EV-KI-A-080` / `CHG-KI-055`; A5 accepts
through KI-R5. The reauthored KI-W6 is decision-complete and
enforcement-complete as amended through the thirteenth correction:
`SRC-KI-038`–`053`, `DEC-KI-038`–`051`, the preserved accepted W6 history,
sequential one-file C112–C116 ownership plus C117, exact 18-path profile membership,
literal operation ceilings, bounded recovery, seven new cases, three
falsification controls and literal once-only assessment commands close the
observed provider-settlement timeout and previously ignored recovery bound
without changing product intent, public payloads or provider economics. CT14
adds the one-file C118 harness-oracle correction and I110 assessment without
changing the existing browser or combined case/control sets. CT15/CT16 add the
two-file local auth-substitute completion and I111 assessment without changing
production auth or the existing browser/combined case-control sets.
CT17 adds the one-file C121 exact generated-to-user-edited provenance oracle
and I112 assessment without changing product behavior or case/control sets.
CT18/CT19 add the two-file one-shot run-start schedule seam/caller and I113
assessment without changing production scheduling, downstream fault positions
or case/control sets.

Parent-direct C124 supersedes only DEC-KI-049's one-callback assumption after
the required backend restart: it discards the closed-server callback, invokes
only the live-server callback and freezes witness `2/1/1/0`. I114 owns the
fresh causal gate and remaining regression/build/coverage/scope closure without
changing product behavior, fault positions, cases, controls or digests.

Parent-direct C125/C126 replace only the maximum query-validation persistence
N+1 with one exactly reconciled set-based update and a path-specific 30-second
transaction budget. The lease fence, rollback boundary, public behavior,
provider economics, cases and controls remain unchanged. I115 independently
reviews this correction and resumes the causal and remaining closure gates.

A5 supplies the live authority. Its current state assigns the thirteenth-correction
assessment to the KI-W6 window agent, which may reconcile the already-applied
parent-direct C125/C126, independently review them, personally execute I115 and stop
`READY_FOR_PARENT_REVIEW`. The
window agent cannot edit implementation, launch a leaf, commit or begin KI-W7.

## KI-W6 fourteenth corrective sequence — observable and cleanup-safe downstream drain

```yaml
correction_sequence: [KI-W6-C127, KI-W6-C128, KI-W6-I116]
trigger: [SRC-KI-054, EV-KI-W6-R68]
decision: DEC-KI-052
objective: classify the first downstream stall without changing production behavior and make failure cleanup deterministic
assigned_agent_policy: window agent launches and independently reviews two sequential single-file leaves, then personally executes I116
authorized_write_scope:
  - email_scraper/test/helpers/keyword-intelligence-e2e-harness.js (C127 only)
  - frontend/test/browser/keyword-intelligence-e2e.mjs (C128 only)
  - KI-W6 S1/S2/S3 coordination artifacts
read_only_scope: [A1-A8, A5, EV-KI-W6-R68, accepted C119-C126 evidence, coordinator repository and discovery/domain services]
prohibited_actions: [production source edit, schema/migration/package/config edit, provider/AWS/production action, raw SQL/query/connection/secret logging, commit/push, KI-W7]
successor: STOP_FOR_PARENT_REVIEW
may_start_successor: false
```

### `KI-W6-C127` — single-file downstream lifecycle and cleanup seam

1. **Trace/owner:** `REQ-KI-010`–`015`, `INV-KI-004/005/010/015`,
   `SRC-KI-054`, `DEC-KI-052`; writable file only
   `email_scraper/test/helpers/keyword-intelligence-e2e-harness.js`, starting
   SHA-256 `c363fb61ac3ce2bd13a2551e56ba8e1aa8589931870ffb6627037b76ed7411e6`.
2. **Interface:** preserve every existing export and add only
   `readDownstreamDiagnostics`. `drainDownstream()` still returns a promise of
   the existing report on success and rejects with the original error on
   failure; a second concurrent call throws `HarnessPreflightError` before work.
3. **Algorithm:** wrap the existing drain body without changing queue choice,
   limits, processors, fault positions, counts or returned report. Track one
   active drain and active message. Emit the three DEC-KI-052 lifecycle events.
   Attach a rejection observer synchronously when the active promise is made.
4. **Diagnostics:** implement exactly the DEC-KI-052 safe projection. Direct
   durable reads use the already validated generated schema name and the admin
   connection. Activity rows expose only `state`, `wait_event_type`, and
   `wait_event`; they exclude the admin probe itself and never include query,
   PID, URL or connection fields. Sort all returned classifications
   lexicographically by their three nullable strings. Each failed diagnostic
   member is exactly `"unavailable"`.
5. **Cleanup order:** `close()` performs the bounded 5-second pre-drop outcome
   wait/diagnostic capture before `DROP SCHEMA`; it then performs the existing
   exact drop and absence proof, performs the bounded 5-second post-drop
   observation, and returns `downstreamCleanup` with the exact three-state
   settlement discriminator. It attaches no timer that can retain the process.
6. **Preserve/forbid:** preserve auth, backend, scheduler, provider substitutes,
   queue contents, database semantics and cleanup target. No production edit,
   retry, cancellation, timeout-policy or raw diagnostic payload.
7. **Local proof:** `node --check
   test/helpers/keyword-intelligence-e2e-harness.js`; `git diff --check --
   test/helpers/keyword-intelligence-e2e-harness.js`; deterministic source
   assertions must pass on the final file and fail after either removing the
   immediate rejection observer or moving `DROP SCHEMA` before the pre-drop
   settlement call.

```yaml
subwindow_id: KI-W6-C127
type: CORRECTION
assigned_agent: UNASSIGNED
predecessors: [KI-W6-I115 CV76/CV77 pass, CV78 diagnostic fail]
writable_file: email_scraper/test/helpers/keyword-intelligence-e2e-harness.js
starting_file_digest: c363fb61ac3ce2bd13a2551e56ba8e1aa8589931870ffb6627037b76ed7411e6
may_start_successor: false
```

- [ ] `C127-P1` Verify assignment, starting digest, predecessor and one-file scope. Evidence: ___
- [ ] `C127-T1` Apply all seven C127 fields exactly. Evidence: ___
- [ ] `C127-V1` Run the three local proofs and both falsification controls. Evidence: ___
- [ ] `C127-H1` Return to the window agent and stop for independent review. Evidence: ___

### `KI-W6-C128` — single-file causal wait and failure-safe promise ownership

1. **Trace/owner:** same requirement/decision set; writable file only
   `frontend/test/browser/keyword-intelligence-e2e.mjs`, starting SHA-256
   `0adfd85433fb8dca6c8f3988443e8b729edb7afca62717b0827b37970785d164`.
2. **Dependency:** accepted C127 interface. No fallback when the seam is absent.
3. **Promise ownership:** declare the downstream outcome holder before the main
   try. At the existing call site, synchronously map the drain promise to
   `{outcome:"fulfilled",value}` / `{outcome:"rejected",error}` and retain it
   through finally. Do not start a second drain.
4. **Wait:** replace only `waitForTrace(..."first domain-check emission"...)`
   with the DEC-KI-052 three-outcome loop and the same 120000 ms deadline. A
   rejection fails immediately with safe name/code/frame; a deadline captures
   and reports `readDownstreamDiagnostics()` once. Do not change the domain
   event predicate, later injections, counts, cases, controls or certificates.
5. **Success:** after the fault injections, require the retained outcome to be
   fulfilled before using its value as the existing downstream report.
6. **Finally:** before `harness.close`, make the retained outcome observable to
   cleanup; copy the helper's returned `downstreamCleanup` safe projection into
   `KI_W6_DIAGNOSTICS`. Never serialize an Error, SQL, query, PID, connection,
   URL, token, cookie, keyword or payload.
7. **Local proof:** `node --check test/browser/keyword-intelligence-e2e.mjs`;
   `git diff --check -- test/browser/keyword-intelligence-e2e.mjs`; exact-source
   assertions verify immediate outcome mapping, three-outcome wait, diagnostic
   capture and cleanup projection while preserving all 26 case IDs, 13 control
   IDs and their digests.

```yaml
subwindow_id: KI-W6-C128
type: CORRECTION
assigned_agent: UNASSIGNED
predecessors: [KI-W6-C127 accepted]
writable_file: frontend/test/browser/keyword-intelligence-e2e.mjs
starting_file_digest: 0adfd85433fb8dca6c8f3988443e8b729edb7afca62717b0827b37970785d164
may_start_successor: false
```

- [ ] `C128-P1` Verify accepted C127, starting digest and one-file scope. Evidence: ___
- [ ] `C128-T1` Apply all seven C128 fields exactly. Evidence: ___
- [ ] `C128-V1` Run the local proofs and prove registry/digest preservation. Evidence: ___
- [ ] `C128-H1` Return to the window agent and stop for independent review. Evidence: ___

### `KI-W6-I116` — window-agent integration assessment

`I116` has zero implementation-write authority. After independently accepting
C127 then C128, run in order:

- [ ] `CV80` Re-run both syntax/diff/source-falsification proofs; verify the
  combined changed set is exactly the two planned files and no production file
  differs from the committed C125/C126 baseline. Evidence: ___
- [ ] `CV81` From `frontend/`, run exactly once with authorized sandbox
  escalation: `ALLOW_DATABASE_TESTS=true KI_W6_SKIP_BUILD=1 node
  test/browser/keyword-intelligence-e2e.mjs`. A pass requires the existing
  26/13 certificate, 100 validators, 100 discovery tasks, 1,000 stable domains
  and cleanup/absence. A failure stops with every DEC-KI-052 diagnostic member;
  it grants no retry or production edit. Evidence: ___
- [ ] `CV82` Only after CV81 passes, run the previously unexecuted CV79 and
  resume CV72–CV75/CH14 exactly as frozen; reuse a prior passing gate only when
  its complete input hash set is byte-identical. Evidence: ___
- [ ] `CV83` Recompute required=registered=executed=activated equality, zero
  skips/duplicates/unexpected members, browser 26/13 and final 35/17 digests;
  verify privacy, scope, clean nested worktrees, zero provider/AWS cost and zero
  residual `kiw6_` schemas. Evidence: ___
- [ ] `I116-H1` Append one consolidated handoff, CAS A5 to
  `READY_FOR_PARENT_REVIEW`, and stop before KI-W7. Evidence: ___

### Fourteenth-correction readiness

- [x] `RW6O-001` Root cause is classified only to the evidence boundary; no
  production mitigation is guessed. Evidence: `SRC-KI-054`, `DEC-KI-052`.
- [x] `RW6O-002` Both implementation tasks are single-file, sequential and
  mechanically complete. Evidence: C127/C128 blocks above.
- [x] `RW6O-003` Promise ownership, failure, diagnostics, cleanup ordering,
  privacy and timeout bounds are exact. Evidence: `DEC-KI-052`.
- [x] `RW6O-004` Existing behavioral registrations, controls and digests are
  unchanged; the correction prevents vacuous teardown evidence. Evidence:
  `DEC-KI-052`, I116 CV81/CV83.
- [x] `RW6O-005` Stateful execution is once-only, escalatable, and a real
  observable failure cannot be relabelled as environment invalidation.
  Evidence: I116 CV81; parent standard E8/E8.1.
- [x] `RW6O-006` Authority is bounded to KI-W6 and stops before KI-W7.
  Evidence: window header and A5 assignment.
