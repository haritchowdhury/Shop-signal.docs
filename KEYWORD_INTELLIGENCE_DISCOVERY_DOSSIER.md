# Keyword Intelligence Discovery Dossier (`A2`)

**Revision:** `KI-DD-17`
**Observed at:** `2026-08-22`
**Environment:** local workspace `/home/harit/Email Scrapper`; no network,
provider, database, AWS, or production operation was performed.

This artifact is the sole authority for observed sources, inventories, payload
provenance, environmental facts, and unknowns. The other artifacts are `A1`
`KEYWORD_INTELLIGENCE_PRODUCT_CONTRACT.md`, `A3`
`KEYWORD_INTELLIGENCE_DECISION_LEDGER.md`, `A4`
`KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md`, `A5`
`ACTIVE_EXECUTION_STATE.md`, `A6`
`KEYWORD_INTELLIGENCE_EXECUTION_EVIDENCE.md`, `A7`
`KEYWORD_INTELLIGENCE_SPECIFICATION_CHANGELOG.md`, and `A8`
`KEYWORD_INTELLIGENCE_TRACEABILITY_INDEX.md`.

## 1. Repository and authority evidence

Each row is one dossier entry; the common environment and observation date are
those above.

| Evidence ID | Class | Precise claim | Exact source/revision | Limitations | Privacy |
|---|---|---|---|---|---|
| `SRC-KI-001` | OBSERVED | Workspace authority fixes Neon/S3/SQS/Lambda, existing control plane, worker fencing, privacy, test isolation, and AWS/provider gates. | user-supplied root `AGENTS.md`; `AWS_ASYNC_DEPLOYMENT_DIRECTION.md`; `TARGET_LAMBDA_SQS_S3_EXECUTION_FLOW.md`; `PRELIMINARY_LAMBDA_SQS_S3_MIGRATION_PLAN.md`; `FINAL_LAMBDA_SQS_S3_MIGRATION_EXECUTION_PLAN.md`; `PARENT_AGENT_CHECKLIST_INSTRUCTIONS.md` | Applies to this workspace; does not itself authorize keyword work. | No secrets read or reproduced. |
| `SRC-KI-002` | OBSERVED | Sole active state remains completed G-R31 and stops for deployment approval; keyword work is not assigned. | `ACTIVE_EXECUTION_STATE.md`, state version 64 | Mutable file already dirty before this authoring turn. | No private data. |
| `SRC-KI-003` | OBSERVED | Coordination root is in an owner-controlled dirty relocation state; backend is clean; KeywordSearchVolume is clean; frontend has three unrelated modified files. | `git status --short`; nested `git status --short`; backend `e63f55079acd29d5972cbba6651b9d9fc00df368`, frontend `ce513a7ab41dab8d0171a0dd2589cf7a0b83afde`, research `6ce7010aaa0d9b999cbf0a3f758f022c214681b3` | Status is a point-in-time observation. | Paths/status only. |
| `SRC-KI-004` | OBSERVED | The authoring standard requires eight distinct artifacts, checked evidence-bearing authoring items, D1–D13, lifecycle/scenario closure, mechanical lint, hashes, and independent falsification before `READY`. | `PROJECT_AGNOSTIC_DECISION_COMPLETE_CHECKLIST_AUTHORING_STANDARD.md` | The standard supplies process, not project facts. | No private data. |
| `SRC-KI-005` | OBSERVED | The product plan requires the entire dashboard, Python-to-Node port, SQLite-to-Postgres, durable worker, non-product queries, 1–100 retained items, one query each, and no implementation/deployment in the plan turn. | `KEYWORD_SEARCH_VOLUME_INTEGRATION_PLAN.md` | It is product prose, not an assignable checklist. | No private data. |

## 2. Standalone product evidence

| Evidence ID | Class | Precise claim | Exact source/revision | Limitations | Privacy |
|---|---|---|---|---|---|
| `SRC-KI-006` | OBSERVED | Configuration fixes nine markets, three v3 Labs endpoints, 120-second HTTP timeout, 30 requests/minute, four configured retries after the first attempt, 2/4/8/16 second exponential backoff plus 0–25% jitter, expansion 60 per seed, overview batches 250, seven-day cache, thresholds, and scoring weights. | `KeywordSearchVolume/config.yaml`; `pipeline/config.py`; `pipeline/client.py`; `pipeline/pipeline.py` at `6ce7010a…` | Provider/account applied limits were not queried. | Credentials not read. |
| `SRC-KI-007` | OBSERVED | SQLite contains only response cache; calculated outputs are files rather than database rows. Cache key is endpoint plus the first 24 hex SHA-256 characters of canonical JSON payload. | `KeywordSearchVolume/pipeline/cache.py`; `pipeline/output.py`; `run.py` | Historical files are not production storage contracts. | No raw bodies copied. |
| `SRC-KI-008` | OBSERVED | Exact Python behavior and formulas are implemented across normalization, intent, dedup, clustering, scoring, orchestration, models, and output modules. | `KeywordSearchVolume/pipeline/{normalize,intent,dedup,cluster,score,pipeline,models,output}.py` at `6ce7010a…` | Python implementation is a parity oracle, not a future runtime. | No provider bodies. |
| `SRC-KI-009` | OBSERVED | Existing tests exercise deterministic pipeline, cumulative markets, dashboard, live-client mocking, and store-discovery behavior. | `KeywordSearchVolume/tests/` at `6ce7010a…` | Coverage is not sufficient for the integrated durable workflow. | Synthetic test inputs only. |
| `SRC-KI-010` | OBSERVED | The 3,322-line dashboard implements all surfaces and interactions enumerated in `REQ-KI-014`, loads output JSON, and stores selection per market in `localStorage`. | `KeywordSearchVolume/dashboard/index.html`, symbols `state`, `renderAll`, `renderTable`, `renderClusters`, `drawClusterLandscape`, `exportCSV`, `changeMarket`, `loadData` | Browser integration must deliberately replace file/localStorage authority. | No private data. |
| `SRC-KI-011` | OBSERVED | Historical representative output has 144 keyword rows (~1.21 MB), two cluster rows, and one summary; current source can theoretically discover at most 2,700 unique phrases from 5 seeds × 9 markets × 60. | Git objects `9a82f7d3…`, `634414e4…`, `96eeb5fc…`; formula from `SRC-KI-006` | Historical output is one sample, not a maximum-size proof. | Raw values were not reproduced. |

## 3. Existing application evidence

| Evidence ID | Class | Precise claim | Exact source/revision | Limitations | Privacy |
|---|---|---|---|---|---|
| `SRC-KI-012` | OBSERVED | Prisma already models owner-scoped runs, editable `RunQuery`, stages/tasks, paid DataForSEO ledger, stable shops, run stores, and durable leases/fencing. No keyword-research output table exists. | `email_scraper/prisma/schema.prisma` at `e63f5507…`; negative search `rg -n "KeywordResearch|keywordResearch" email_scraper/prisma email_scraper/src frontend` | Source state, not deployed-schema observation. | Schema only. |
| `SRC-KI-013` | OBSERVED | Existing query planning is product-only, enforces fixed per-category counts, and permits add/delete; the AWS Google probe persists an immutable attempt marker before one external call and a result artifact after it. | `email_scraper/src/query-{planner,validator,review}.js`; `pipeline.js`; `server.js::queryReviewPolicy`, `awsProbeSearchPage`; `prisma-run-repository.js` | Research-backed behavior needs an explicit branch; legacy must remain unchanged. | No result contents inspected. |
| `SRC-KI-014` | OBSERVED | Google probing is configured for ten results per query and downstream stable identity/domain aggregation is already bounded for 1,000 domains by G-R30 evidence. | `email_scraper/src/search.js`; AWS provider config/contracts; `AWS_PIPELINE_EXECUTION_EVIDENCE.md` G-R30 | Does not prove the new 100-query entry path. | Existing sanitized evidence only. |
| `SRC-KI-015` | OBSERVED | Backend exposes one HTTP server with authenticated owner-scoped run routes and queue-drain recovery; frontend uses Next.js App Router, same-origin proxy route handlers, strict API parsers, and `apiRequest`. | `email_scraper/src/server.js`; `frontend/app/api/**/route.ts`; `frontend/lib/{backend-proxy,api-validation,client-api,api-types}.ts` | New routes do not exist. | Auth secrets not inspected. |
| `SRC-KI-016` | OBSERVED | AWS pipeline already supplies strict message/artifact contracts, canonical fingerprints, immutable S3 storage, SQS dispatch, lease monitor, recovery, coordinator repository, handler build conventions, and SAM infrastructure. | `email_scraper/src/aws-pipeline/**`; `email_scraper/infrastructure/aws/{template,bootstrap-template}.yaml`; `email_scraper/scripts/build-aws-handlers.js` | Reuse still requires new keyword-specific contracts and build proof. | No AWS calls. |
| `SRC-KI-017` | OBSERVED | Backend lacks BLAKE2s support at a six-byte digest length through Node's built-in `createHash`; frontend/backend currently lack Chart.js/treemap and backend lacks `@noble/hashes`. | local Node digest experiment; `email_scraper/package.json`; `frontend/package.json` | A decided dependency must still be installed and built before assignment readiness. | No network call. |
| `SRC-KI-018` | OBSERVED | Frontend has an existing local Next.js plus Chrome/CDP browser-test pattern and is Next 16.2.12/React 19.2.4. | `frontend/package.json`; frontend browser/runtime tests; installed Next documentation required by `frontend/AGENTS.md` | Browser availability is local-environment dependent. | No browser launched. |

## 4. Historical DataForSEO payload evidence

The standalone repository previously committed live responses and later removed
them for safety. Inspection used `git show` piped directly to structural `jq`
queries. No raw body was restored, copied, logged, or added to this workspace.

| Evidence ID | Class | Precise claim | Exact source/revision | Limitations | Privacy |
|---|---|---|---|---|---|
| `SRC-KI-019` | OBSERVED | Keyword Overview v3 envelope/task/result/item shapes and all fields consumed by the Python normalizer were observed. | commit `013ed822109ca71f076090ec714205356ed96588`, blob `2b173410b7b484427bfcd68ddb6f2ca575bd3b31`, historical path `data/raw/keyword-overview/20260812T143909_c2c5bc24.json` | One observed provider version/shape; no alternate variants claimed. | Only keys and JSON types are reproduced below. |
| `SRC-KI-020` | OBSERVED | Keyword Suggestions v3 exposes the candidate at `tasks[].result[].items[].keyword`. | same commit, blob `7e03978aa5e3f09312f15660cd8b3a731e604729`, historical path `data/raw/keyword-suggestions/20260812T143906_5691735c.json` | One observed provider version/shape. | Values omitted. |
| `SRC-KI-021` | OBSERVED | Related Keywords v3 exposes the candidate at `tasks[].result[].items[].keyword_data.keyword`; `related_keywords` is an array of strings. | same commit, blob `40c4ff13339cd5a5b15ef0bae34dc2b11589fff6`, historical path `data/raw/related-keywords/20260812T143907_5691735c.json` | One observed provider version/shape. | Values omitted. |
| `SRC-KI-022` | OBSERVED | The old client guesses alternate candidate field `items[].key`, falls back across shape paths, and logs/stores raw response bodies; those behaviors violate the current contract and must not be ported. | `KeywordSearchVolume/pipeline/client.py::_extract_keywords`, `_store_raw`, error text | This is negative behavior evidence, not a supported payload variant. | Raw bodies excluded. |

### Payload certificates

#### `PAY-KI-001` — DataForSEO request task

- Provenance: `SRC-KI-006`, `SRC-KI-019`–`SRC-KI-021`.
- Producer/consumer: new `dataforseo-labs-adapter.js` produces one-element JSON
  arrays; DataForSEO Labs v3 consumes them.
- Discriminator: endpoint key is exactly `keyword_suggestions`,
  `related_keywords`, or `keyword_overview` and chooses one strict schema.
- Requests:
  - suggestion `{keyword:string(1..100),location_code:int,
    language_code:string,limit:30}`;
  - related adds `depth:2`;
  - overview `{keywords:string[1..700],location_code:int,
    language_code:string}`.
- Unknown-field policy: request objects are strict and reject extras.
- Errors: local invalid request → `KEYWORD_PROVIDER_REQUEST_INVALID` before any
  call.
- Privacy: the request fingerprint, not the request body or seed text, enters
  SQS/logs; normalized seed/keyword text is allowed only in owner-scoped Neon
  and encrypted S3 artifacts.
- Required tests: valid endpoints, every bound, missing/extra/wrong type,
  canonical request fingerprint, and endpoint discriminator.

#### `PAY-KI-002` — DataForSEO common response envelope

- Provenance: `SRC-KI-019`–`SRC-KI-021`.
- Producer/consumer: DataForSEO Labs v3 → strict endpoint parser.
- Required consumed paths/types: root `status_code:number`,
  `status_message:string`, `tasks:array`; first task `status_code:number`,
  `status_message:string`, `result:array`. Root/task observation also contains
  `version:string`, `time:string`, `cost:number`, counts, task `id`, `path`,
  `data`, and timing; they are validated then discarded except cost and safe
  status metadata.
- Success discriminator: HTTP 200, root `status_code===20000`, exactly one task,
  task `status_code===20000`.
- Unknown-field policy: endpoint-specific Zod objects enumerate and strictly
  validate every consumed/discriminator path, then strip every unconsumed key at
  each object boundary. Unknown fields therefore cannot affect normalized
  behavior; a later change may consume one only after it is catalogued and
  tested. Missing, moved, aliased, or wrong-typed consumed fields are contract
  mismatch.
- Error mapping: auth → `KEYWORD_PROVIDER_AUTH_FAILED`; retryable transport,
  HTTP, or configured API code → durable retry transition; exhausted retry →
  `KEYWORD_PROVIDER_RETRY_EXHAUSTED`; task failure →
  `KEYWORD_PROVIDER_TASK_FAILED`; malformed/missing/unknown →
  `KEYWORD_PROVIDER_CONTRACT_MISMATCH`; uncertain post-send outcome →
  `KEYWORD_PROVIDER_AMBIGUOUS`.
- Privacy: never persist/log the envelope. Persist only strict normalized output,
  safe codes, cost, and SHA-256 fingerprint.
- Required tests: observed success, empty result, each safe failure, missing,
  null, malformed, unknown key, second task, and secret/candidate redaction.

#### `PAY-KI-003` — Suggestions normalized response

- Provenance: `SRC-KI-020`.
- Exact consumed path: `tasks[0].result[].items[].keyword:string`; surrounding
  result requires `items:array`; observed unconsumed context is stripped and has
  no behavioral effect.
- Normalized output: `{keywords: string[]}` in provider order after trimming
  empty strings and exact case-insensitive first-occurrence deduplication.
- No `items[].key` alias is supported.
- Tests: `SCN-KI-004`, payload boundary matrix.

#### `PAY-KI-004` — Related normalized response

- Provenance: `SRC-KI-021`.
- Exact consumed path:
  `tasks[0].result[].items[].keyword_data.keyword:string`; `depth:number` and
  `related_keywords:string[]` are validated and have no behavioral effect.
- Normalized output and policies match `PAY-KI-003`.
- Tests: `SCN-KI-004`, including rejection of a direct `item.keyword` alias.

#### `PAY-KI-005` — Overview normalized response

- Provenance: `SRC-KI-019`.
- Consumed item fields across all 41 historical overview bodies:
  `keyword:string`; `keyword_info.search_volume:number`,
  `cpc:number|null`, `competition:number`,
  `competition_level:"LOW"|"MEDIUM"|"HIGH"`, `monthly_searches` array of
  `{year:number,month:number,search_volume:number}` (observed lengths 15–102);
  `keyword_properties.keyword_difficulty:number|null`; and
  `search_intent_info.main_intent:"transactional"|"commercial"|
  "informational"|"navigational"`. `keyword_info`, `keyword_properties`,
  `search_intent_info`, and `monthly_searches` were always objects/object/object/
  array respectively. No other nullability or intent/competition variant is
  supported without new sanitized evidence.
- Result context consumes `location_code:number`, `language_code:string`, and
  `items:array`; `items_count` and other observed context are stripped and have
  no behavioral effect.
- Normalized output is `KeywordMarketMetric[]`; missing keyword or nonpositive/
  null search volume yields no usable metric exactly as the Python source.
- Unknown nested fields cannot affect behavior and are validated/discarded as
  prescribed by `PAY-KI-002`.
- Tests: observed structural success plus missing/null/malformed/boundary/
  unknown fixtures and normalization parity.

#### `PAY-KI-006` — SQS messages

- Provenance: locked workspace pattern `SRC-KI-016`; produced shape is a product
  decision, not an external unknown.
- Discriminator `type` is exactly one of `keyword.initialize.v1`,
  `keyword.expansion.task.v1`, `keyword.overview.task.v1`, or
  `keyword.aggregate.check.v1`.
- Every shape is strict and contains only `contractVersion`, `type`,
  `researchId`, positive `generation`, task/stage identity when applicable, and
  a 64-lowercase-hex input fingerprint. No seed, keyword, provider body, result,
  credential, URL, or owner ID is permitted.
- Parser errors are per-record `KEYWORD_MESSAGE_CONTRACT_MISMATCH` and never
  cause a provider call.
- Tests: positive shape per discriminator; missing, wrong version/type, extra
  business field, malformed ID/fingerprint, mixed valid/invalid SQS batch.

#### `PAY-KI-007` — API and artifact payload family

- Provenance: existing patterns `SRC-KI-015`–`SRC-KI-016`; exact produced shapes
  are locked in `DEC-KI-019` and `DEC-KI-020`.
- Producers/consumers, schemas, fields, errors, privacy, and tests are fully
  enumerated in those decisions and their tasks. Unknown API fields are rejected;
  unknown artifact fields or contract versions are contract mismatch.

## 5. Negative searches and parked facts

| Evidence ID | Class | Precise claim | Exact source/operation | Limitations | Privacy |
|---|---|---|---|---|---|
| `SRC-KI-023` | OBSERVED | No current keyword research Prisma/API/worker/dashboard route exists in the integrated app. | `rg -n "KeywordResearch|keyword-intelligence|keywordResearch" email_scraper frontend` | Name-based absence check is paired with entry-point inventories above. | No private data. |
| `SRC-KI-024` | OBSERVED | No current output database table exists in standalone research; only files and response cache exist. | source inventory and `rg` over `KeywordSearchVolume` | Source state only. | No raw data. |
| `SRC-KI-025` | DEFERRED_GATE | Actual AWS account queue/Lambda quotas, installed secret references, event-source state, and deployment permissions are required only for the later infrastructure/live windows. | workspace AWS authorization rules | No local implementation depends on optimistic values; gate branches are in `DEC-KI-025`. | No AWS call made. |
| `SRC-KI-026` | DEFERRED_GATE | Final emitted worker artifact size/startup and frontend dependency build cannot be observed before decided dependencies are locally installed and representative code exists. | authoring standard D9; `SRC-KI-017` | This blocks package `READY`, not decision closure; closure action is `GATE-KI-002`. | No network/install performed. |
| `SRC-KI-027` | PARKED | Live provider error variants, alternate DataForSEO versions/shapes, and historical raw-body import are unsupported. | `REQ-KI-021`, `EXC-KI-006`; one-shape evidence `SRC-KI-019`–`021` | A later product change requires new sanitized evidence and changelog. | Prevents raw-data expansion. |
| `SRC-KI-028` | OBSERVED | Historical reported costs are nonzero and vary by endpoint/work size: at commit 013ed82, 41 overview bodies total $0.56484000 (largest task $0.01500000; largest observed per-keyword cost $0.00412000), 20 suggestion bodies total $0.31200000 (largest $0.01560000), and 20 related bodies total $0.28608000 (largest $0.01560000). Existing Email Scraper paid calls reserve estimated cost before network dispatch and enforce a run budget. | structural `git show 013ed82:<data/raw/...>` cost/count aggregation; `email_scraper/prisma/schema.prisma::DataForSeoRequestLedger`; `prisma-run-repository.js::claimDataForSeoRequest` | Historical reports do not prove current/provider-account prices or the requester's acceptable spend. | Aggregate cost/count facts only; no keyword/body/credential values reproduced. |
| `SRC-KI-029` | SUPERSEDED_UNKNOWN | The initial package lacked a maximum research exposure and reservation formula. | Initial authoring audit; superseded by `SRC-KI-030`. | Retained to explain `CHG-KI-002`; it is no longer blocking. | No paid call made. |
| `SRC-KI-030` | AUTHORIZED_CHOICE | The requester selected US-only expansion, accepted metric-backed shortlisting, fixed shortlist size 200 through acceptance of the `$3` calculation, and approved `maxCostPerResearchUsd=3.00000000`. | User decisions in this thread on 2026-08-17: “5 seeds × 1 market × 2 endpoints = 10 calls”, agreement with option 3, and “great lets settle for $3 then” followed by “do it” to the exact US/200 documentation change. | Authorization is specification-only; it grants no paid call, dependency install, implementation, or AWS action. | No provider call or private value. |
| `SRC-KI-031` | OBSERVED | Across all 41 historical overview, 20 suggestions, and 20 related bodies, provider-reported task cost equals `0.01200000 + 0.00012000 × returnedItemCount`; suggestions always returned 30 and cost `0.01560000`, while related varied with returned count. For safe pre-call reservation, substitute requested maximum count. | Structural `git show 013ed82:data/raw/...` plus `jq` over request counts, returned-item counts, root/task cost and status only; no keyword values emitted. | Historical/account pricing evidence; W8 must fail closed if applied pricing no longer fits the locked formula. | Aggregate counts/formula only. |
| `SRC-KI-032` | OBSERVED_CURRENT | DataForSEO's current official Google Keyword Overview Live documentation permits at most 700 keywords in one request and one task per Live call. | `https://docs.dataforseo.com/v3/dataforseo_labs-google-keyword_overview-live/`, checked 2026-08-17. | Published capability is not proof of applied account pricing or permission; W8 preflight remains required. | Public documentation only. |
| `SRC-KI-033` | AUTHORIZED_CHOICE | The requester authorized `GATE-KI-002`: install exactly `@noble/hashes@2.2.0` in `email_scraper/` and `chart.js@3.9.1` plus `chartjs-chart-treemap@2.0.0` in `frontend/`, run representative Node/Next builds, record emitted dependency inventory/sizes/startup, and materialize/validate the four strict payload fixture files. | User reply “continue” on 2026-08-17 directly to the assistant message naming exactly this package/version/action scope and closing with “Say the word when ready.” | Grants only the named local installs/builds/fixture materialization; no provider call, AWS action, production write, frontend source edit beyond dependency manifests, or alternative library selection. | No provider call or private value. |

There are **zero unknown consumed payload fields** in the supported one-shape
contract. `SRC-KI-025` and `SRC-KI-026` are predictable execution/readiness
gates, not payload discovery tasks. `SRC-KI-029` is resolved by
`SRC-KI-030`–`032`; no cost-policy decision remains open.

### `SRC-KI-050` — W6 workspace lineage witness contradicts the accepted edit-provenance contract

```yaml
evidence_id: SRC-KI-050
classification: OBSERVED
claim: The accepted keyword-research handoff creates every RunQuery with source="generated"; QuerySource admits generated, user_added and user_edited; QueryEditor changes a generated row to user_edited whenever its text is edited while preserving user_added/user_edited; I111 edits all 100 rows and swaps the first two. The current W6-FLOW-09 browser oracle nevertheless requires the sorted badge multiset to remain byte-equal, so it must fail after the correct 100 generated -> 100 user edited transition even though row count, text, reorder and durable persistence pass.
source: frontend commit a234a9eaf0e58e5ad4c74d49e8f861ae3516c7fd; frontend/lib/api-types.ts:13 SHA-256 e91b62a2ead26d6693c2ff47cd4dcc89778f287784620614d0296fb6a59fcec4; frontend/components/query-editor.tsx:68-78 SHA-256 f955737d19ba47c256a598aa118e2a1f07a8e70294911e4ed920d65a2bad4229; email_scraper/src/prisma-run-repository.js createRun handoff mapping; frontend/test/browser/keyword-intelligence-e2e.mjs:1127-1156 SHA-256 72fe4f99420b854b537d82b769ffee71866203ff5872321538de6210faf97347; EV-KI-W6-R57
observed_at: 2026-08-22
environment: local committed backend 4d68993b13aeaab0b70ed544cfa575e2a73b0652 and frontend a234a9eaf0e58e5ad4c74d49e8f861ae3516c7fd; no provider, AWS or production operation
limitations: The failed CV53 is diagnostic rather than acceptance. It reached the real workspace and observed the product transition, but later CV54-CV57 gates remain unexecuted.
privacy: Synthetic harness rows and source labels only; no cookie value, header, credential, provider body or user data inspected or recorded.
```

### `SRC-KI-051` — W6 run confirmation is parked behind an unflushed test scheduler

```yaml
evidence_id: SRC-KI-051
classification: OBSERVED
claim: The production run-start handler successfully calls queueDrain(), but the W6 harness injects a manual schedule(callback) implementation that only appends the drainQueue callback to scheduledCallbacks. Its setIntervalFn is also inert. The only current flushSchedule() caller is drainDownstream(), while the browser waits for all 100 validation calls and all 100 discovery dispatches before starting drainDownstream(). Consequently the callback that alone reaches executeRun(), validateResearchBackedConfirmedQueryRows(), and dispatchConfirmedQueries() is never invoked; the observable CV59 outcome is exactly zero validator calls after a successful POST /api/runs/<runId>/start.
source: email_scraper/src/server.js::queueDrain/drainQueue/executeRun and POST /api/runs/:id/start; email_scraper/test/helpers/keyword-intelligence-e2e-harness.js::schedule/flushSchedule/setIntervalFn/drainDownstream SHA-256 cbcd304aea6657bef10d73644d81e253396fe3f4f3f112f9dc03e020f0c7db74 at backend commit 4d68993b13aeaab0b70ed544cfa575e2a73b0652; frontend/test/browser/keyword-intelligence-e2e.mjs run-start-to-confirmation sequence SHA-256 8d89bb198390c3f7baf431ccd3405693c5003eb8a9ee4f0e7ccd75c254d507d0; EV-KI-W6-R59
observed_at: 2026-08-22
environment: local emitted Next/browser plus actual backend and isolated disposable schema; no live provider, AWS or production operation
limitations: CV59 is diagnostic rather than acceptance. It proves the test scheduler deadlock, not a product queueDrain defect. CV60-CV63 were not run.
privacy: Source control flow, synthetic event counts and disposable-schema cleanup only; no token, cookie value, header, provider body, keyword text or user data retained.
```

### `SRC-KI-052` — The required backend restart leaves one stale callback before the live run-start callback

```yaml
evidence_id: SRC-KI-052
classification: OBSERVED
claim: C122 and C123 correctly exposed the manual run-start scheduler, but I113 CV65 proved its exact one-callback precondition cannot hold in the accepted causal flow. createLeadServer calls queueDrain once at construction. The browser's required W6-RES-01 restart closes server A and constructs server B before confirmation, while the shared manual scheduler retains server A's callback and appends server B's callback. Request-driven queueDrain calls on server B do not append another callback because its drainScheduled guard is already true. Thus the confirmation boundary contains exactly two FIFO callbacks: the first belongs to closed server A and its disconnected repository; the last belongs to live server B and is the only callback that can claim the queued run.
source: email_scraper/src/server.js::createLeadServer/queueDrain/drainQueue; email_scraper/test/helpers/keyword-intelligence-e2e-harness.js::schedule/buildBackendServer/restartBackend/flushRunStartSchedule SHA-256 d9a76cebad80650f5a601012eaaa4715e16a6b6ce334000c98a56470ab6fa6fe at backend commit 70af619814ec026e51dccb985b0fc0f732169309; frontend/test/browser/keyword-intelligence-e2e.mjs::W6-RES-01 restart and confirmation boundary SHA-256 448921c77cb0a1619e004d2c8587faa53e0598736605d95a0c7ff9fbf4e13b99 at frontend commit 3d97150f4736ce2ee3e6c754c67206d271479639; EV-KI-W6-R60-R63
observed_at: 2026-08-22
environment: local emitted Next/browser plus actual backend and isolated disposable schemas; no live provider, AWS or production operation
limitations: CV65 attempt one was environment-invalidated by an unrelated fixed proxy timeout after traversing FLOW-10 through FLOW-13. Its authorized recovery passed that phase and failed deterministically at pendingBefore=2 before invoking the live callback. Later I113 gates did not run.
privacy: Callback counts, source control flow and synthetic cleanup evidence only; no token, cookie value, header, provider body, keyword text or user data retained.
```

### `SRC-KI-053` — Maximum query validation expires in sequential persistence

```yaml
evidence_id: SRC-KI-053
classification: OBSERVED
claim: After the local harness reached a confirmed 202/202 run start and completed all 100 production validator calls, executeRun failed before discovery dispatch with Prisma P2028 at prisma-run-repository.js:1822. saveQueryValidation holds the live Run lease fence inside Prisma's default interactive-transaction timeout and then performs one RunQuery.updateMany per row; at the accepted 100-query bound this is 101 sequential mutations and the transaction expires before dispatchConfirmedQueries. The stable failure reproduced after the internet-invalidated attempt; the interrupted disposable schema was dropped by exact name and verified absent.
source: email_scraper/src/prisma-run-repository.js::saveQueryValidation at SHA-256 d4995ef9e177dbf9f0fad5c199b9c8f5e63fd37122919ba256aa1282f842db27; local W6 causal-browser diagnostics on 2026-08-22
observed_at: 2026-08-22
environment: local emitted Next/browser, actual backend and isolated disposable Neon test schema; synthetic provider substitutes only
limitations: The failure proves the 100-row persistence defect, not live provider, AWS or production behavior. The interrupted network run is invalidated; the later stable P2028 run is authoritative.
privacy: Only safe error name/code/repository-relative frame, row counts and schema-absence evidence were retained; no raw error, SQL, URL, header, token, cookie, body, keyword or user data.
```

### `SRC-KI-054` — CV78 teardown masks the first downstream operation

```yaml
evidence_id: SRC-KI-054
classification: OBSERVED
claim: I115 CV78 started drainDownstream without retaining a failure-safe cleanup handle, waited 120 seconds for the first domain delivery, then dropped the disposable schema while the first discovery message was still pending. The resulting Prisma "Response from the Engine was empty" appeared only after schema destruction. This proves an unsettled downstream operation and a cleanup race; it does not prove that PostgreSQL was waiting on a row lock, identify a blocking transaction, or justify changing production coordinator timeouts.
source: EV-KI-W6-R68; email_scraper/test/helpers/keyword-intelligence-e2e-harness.js::drainDownstream/close SHA-256 c363fb61ac3ce2bd13a2551e56ba8e1aa8589931870ffb6627037b76ed7411e6; frontend/test/browser/keyword-intelligence-e2e.mjs downstream wait/finally SHA-256 0adfd85433fb8dca6c8f3988443e8b729edb7afca62717b0827b37970785d164; email_scraper/src/aws-pipeline/repositories/pipeline-coordinator-repository.js::claimTask read-only inspection
observed_at: 2026-08-22
environment: local causal browser harness with isolated disposable Neon schema; no provider, AWS or production operation
limitations: The underlying 120-second stall is not yet classified. Production lock_timeout, statement_timeout, retry, or coordinator transaction changes remain unsupported until a diagnostic run distinguishes lock wait, connection/engine failure, harness scheduling, or another failure.
privacy: Only synthetic task identity classes, safe error name, operation phase, counts, wait classification and repository-relative frames may be recorded; no SQL text, connection URL, token, cookie, header, provider body, keyword text or user data.
```

### `SRC-KI-055` — W6 clock and transaction-boundary inventory after the first complete discovery aggregation

```yaml
evidence_id: SRC-KI-055
classification: OBSERVED
claim: The accepted clock correction lets all 100 discovery tasks complete, but the next repository operation fails PIPELINE_LEASE_LOST because five PrismaRunRepository aggregation readers create real time internally while the causal harness pins service-level Date construction. The same W6-reachable graph contains exactly 32 interactive Prisma transactions: eleven PipelineCoordinatorRepository methods and twenty-one PrismaRunRepository methods. Only claimTask, renewTask, and publishAwsFinalResults currently carry the required explicit 5-second acquisition/30-second execution profile, leaving twenty-nine implicit defaults. Coordinator lockedTask, lockedStage, and lockedRun each perform SELECT id FOR UPDATE followed by a redundant findUnique, and recordDispatch reloads rows already locked.
source: local causal-browser run ending at run-repository.readAwsReuseInputs operation sequence 304 after 100/100 discovery tasks; email_scraper/src/aws-pipeline/repositories/pipeline-coordinator-repository.js SHA-256 e285557a5dc854d0021bb71e19076d8bff6ce4e161b9ce8621acda9c24e549c4; email_scraper/src/prisma-run-repository.js SHA-256 54d5f422431ec1914855b2ae5cc07ff30e9ab428f11601a7703d589ee21cef13; domain/lead/final service SHAs e873bb622c085ea34e69e3658f21dacd36d068765f821782dfc613009f3199ce, c3f2fb24576f43e6c046a87573e6e0942b9263d39c2002eec152280365cde38c, 416e36feeb35aedd571ae8863a413550215263a157a99ed8cf519722446f9683; mechanical method/call-site inventory recorded by EV-KI-A-110
observed_at: 2026-08-23
environment: local emitted Next/browser, actual backend and isolated disposable Neon test schema; synthetic local provider substitutes only
limitations: This evidence proves the local W6-reachable source set and causal clock failure. It does not claim a production incident, authorize a global Prisma default change, or establish provider/AWS behavior.
privacy: Method names, counts, safe error code, source hashes and schema-absence result only; no SQL values, connection URL, credential, token, cookie, provider body, keyword text or user data retained.
```

## 6. Post-W5 corrective discovery

| Evidence ID | Class | Precise claim | Exact source/revision | Limitations | Privacy |
|---|---|---|---|---|---|
| `SRC-KI-034` | OBSERVED | Parent review `KI-PR-W4-W5-01` reproduced nine current implementation defects: numeric-vs-string research contract versions; missing JSON content type on three browser mutations; noncanonical browser manual IDs; selection bodies exceeding the backend/Next ceilings; finalization of an unsaved local draft; loss of a handoff idempotency key after ambiguous response; frontend/export filter divergence; duplicate selection persistence followed by handoff rejection; and spreadsheet-formula-capable CSV text cells. | `KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md::KI-PR-W4-W5-01`; backend `fac5bb0f0a4e9c04873c9d338794762d44e35f7f`; frontend `c85f93b4bc66e1c130401227e46b488c6fe13c94`; exact symbols and focused reproductions cited in `KI-PR-F01`–`F09`. | Local source/component evidence; it proves the defects and interface mismatch, not a corrected end-to-end workflow. | Synthetic keywords only; no user/provider body, credential, database, network, provider, or AWS access. |
| `SRC-KI-035` | OBSERVED | The accepted parity result produces a real 12-item default-selection request of 176,232 UTF-8 bytes under the old full-snapshot request contract; a strict minimal request containing only `{sourceKind,sourceKeywordId,keyword}` for calculated items or `{sourceKind,keyword}` for manual items is at most 143,641 bytes for 200 calculated items whose keywords are each 160 four-byte Unicode code points. | `parity-output-v1.json` plus `createDefaultSelection`; deterministic `Buffer.byteLength(JSON.stringify(...))` measurements recorded during `KI-PR-W4-W5-01` and KI-R5 authoring. | The 143,641-byte value is the maximum for the newly decided fixed-key input union; it is not a bound for arbitrary unknown fields, which remain rejected. | Synthetic/parity fixtures only. |
| `SRC-KI-036` | OBSERVED | Native Fetch assigns `text/plain;charset=UTF-8` to a string body without an explicit type; all three Next mutation handlers reject non-JSON before authentication. The emitted W5 browser harness replaces `globalThis.fetch` for every keyword route, so its authenticated-looking success paths never enter those Next handlers. A pass-through unauthenticated request can nevertheless prove the real emitted handler received JSON by reaching the existing 401 boundary instead of the 415 boundary. | Native Node Fetch reproduction; `frontend/lib/client-api.ts`; the three Next route handlers; `frontend/test/browser/keyword-intelligence-dashboard.mjs:647-697`; installed Next 16 route-handler guide. | No deterministic local Neon-authenticated session fixture exists; full authenticated Next-to-backend workflow proof remains `KI-W6`, while KI-R5 must prove each real wire endpoint at its highest available parity without claiming the interception as route proof. | No cookie, secret, auth service, or network call used. |
| `SRC-KI-037` | OBSERVED | A5 state 108 assigns only KI-W6 decomposition, but the parent review changed A4 and therefore invalidated its pinned checklist revision. The KI-W6 subordinate state is `AWAITING_PARENT_DECOMPOSITION_REVIEW`; S001/S002/I001 are all `NOT_STARTED`, no leaf is assigned, and accepted count is zero. | `ACTIVE_EXECUTION_STATE.md` state 108; `KEYWORD_INTELLIGENCE_KI_W6_SUBWINDOW_STATE.md` state 1; current A4 SHA-256. | The three KI-W6 subordinate artifacts remain historical unexecuted decomposition evidence and must be regenerated after KI-R5 acceptance; this observation does not authorize either window. | Paths, hashes, and status only. |
| `SRC-KI-038` | OBSERVED | The accepted backend handoff response deliberately exposes the API status resource as `statusUrl:"/api/runs/<Run.id>"`, while both dashboard handoff-success branches pass that API URL directly to `router.push`; the actual run workspace is the Next route `/runs/[runId]`. The current emitted-browser `R5-FIN-01` fixture changes `statusUrl` and asserts navigation to it, so that accepted assertion can pass while routing the user to JSON instead of the workspace. | `email_scraper/src/keyword-intelligence/api.js::startRun` return at lines 509–514; `frontend/components/keyword-intelligence/research-dashboard.tsx::handleFinalize/handleRetryHandoff`; `frontend/app/runs/[runId]/page.tsx`; `frontend/test/browser/keyword-intelligence-dashboard.mjs::R5-FIN-01`; backend `0083a42c…`, frontend `70fb5edf…`. | Source-level observation only. It does not authorize changing the API resource URL or any implementation file. | Synthetic paths and identifiers only. |
| `SRC-KI-039` | OBSERVED | A causal authenticated local proof can use existing seams without production auth/provider/cloud changes: emitted Next route handlers call installed Neon Auth and the actual backend proxy; the backend server constructs the real Prisma keyword API and accepts an injected pipeline runtime; existing keyword-worker and AWS E2E harnesses demonstrate isolated-schema migrations, strict provider substitutes, immutable artifact stores, in-memory queue dispatch, and real discovery/domain services. | `frontend/lib/auth/server.ts`; `frontend/lib/auth/route.ts`; `frontend/lib/backend-proxy.ts`; installed Next route-handler/testing guides; `email_scraper/src/server.js::createLeadServer`; `email_scraper/test/helpers/isolated-postgres.js`; `email_scraper/test/keyword-intelligence-worker.test.js`; `email_scraper/test/helpers/aws-pipeline-e2e-harness.js`. | A local auth server, provider HTTP fixture, and in-memory S3/SQS prove only the explicit substitute claims in `DEC-KI-038`; they do not prove live Neon Auth, provider, S3, SQS, Lambda, pricing, quota, IAM, or deployment behavior. | Test-only identities and deterministic synthetic provider data; no live cookie, credential, provider body, or customer data. |
| `SRC-KI-040` | OBSERVED | The current parent standard requires exact case registrations/digests, captured-evidence falsification, substitute-fidelity limits, invalidation-aware one-time gates, standing escalation for already-authorized local operations, and recursive parent→window-agent→single-file-leaf authority. The state-108 W6 decomposition has none of the post-R5 contracts and chose two disconnected substitutes as an end-to-end proof; it remains unexecuted and cannot be amended into the new authority chain. | `PROJECT_AGNOSTIC_DECISION_COMPLETE_CHECKLIST_AUTHORING_STANDARD.md` SHA-256 `cda35201…`; `PROJECT_AGNOSTIC_WINDOW_AGENT_SUBWINDOW_AUTHORING_STANDARD.md` SHA-256 `84e7590e…`; historical `KEYWORD_INTELLIGENCE_KI_W6_SUBWINDOW_{CHECKLIST,STATE,EVIDENCE}.md`; A5 state 141. | Governance and current-artifact observation; it does not assign KI-W6. | Paths, hashes and structural facts only. |
| `SRC-KI-041` | OBSERVED | The maximum causal W6 run reaches the real final market aggregator with 300 valid anchor candidates and a durable 200-keyword shortlist, but publishes 300 result rows. `aggregateMarket` reads the complete expansion manifest and all 300 US anchor metrics, never reads the durable shortlist manifest, and passes the unfiltered expansion/US set to `computeResearchResult`; that function retains every discovered anchor-backed row. This contradicts the locked 300-screen→200-shortlist→200-final contract rather than exposing a harness-only error. | `email_scraper/src/aws-pipeline/keyword-intelligence/service.js::aggregateMarket` at source SHA-256 `c37a038f189470ad1d2eca6626f515b9f0c45bd60de470d84c4b72fa497637b5`; `email_scraper/src/keyword-intelligence/pipeline.js::computeResearchResult`; `KEYWORD_INTELLIGENCE_KI_W6_REAUTHORED_SUBWINDOW_EVIDENCE.md` continued V3 Attempt B (`publishedSnapshot.keywordResult={visible:true,rowCount:300,defaultSelectionItemCount:100}`); A1 `REQ-KI-024`; A3 `DEC-KI-038`. | Local emitted-browser/isolated-schema evidence. Provider/AWS/production behavior was not invoked. The failed V3 run emitted no W6 acceptance certificate and therefore remains diagnostic evidence only. | Deterministic synthetic keywords/counts and source paths only; no credentials, provider bodies, owner data, or production rows. |
| `SRC-KI-042` | OBSERVED | I102 CV1 proved two defects in the accepted C105 test scaffold, not in the C104 production correction: the shortlist manifest was stored with `anchorTask.inputFingerprint` although production `readManifest` requires `keywordStageInputFingerprint({researchId,generation,stage:"anchor_screen",tasks:[anchorTask]})`; and SCN-KI-041 put 300 candidates in one `bySeed` member although `keywordExpansionManifestSchema` permits at most five seeds and at most 60 keywords per seed. Five seeds with 60 unique ordered keywords each are the contract-valid 300-candidate maximum. | `KEYWORD_INTELLIGENCE_KI_W6_REAUTHORED_SUBWINDOW_EVIDENCE.md::EV-KI-W6-R28`; `email_scraper/src/aws-pipeline/keyword-intelligence/service.js::readManifest`; `email_scraper/src/aws-pipeline/keyword-intelligence/contracts.js::keywordExpansionManifestSchema`; `email_scraper/test/keyword-intelligence-worker-flow.test.js::aggregationScaffold/SCN-KI-041`; backend HEAD `adf416662e3aae581328478b70dfe828d3191e8b`. | Local component evidence only. CV1 stopped with 30 pass / 7 fail; CV2–CV6 did not run. It requires no payload discovery, schema change, provider call, database, AWS, or production action. | Synthetic keywords, fingerprints, counts and source paths only. |
| `SRC-KI-043` | OBSERVED | I103 CV9 reached the completed 200-row/default-100 dashboard but failed before selection save because `swapOneSelectionItemViaUi` searches only the currently rendered keyword-table page for both a checked and an unchecked checkbox. The production table renders `paginate(..., pageSize)` with default `pageSize:25` and exposes `Prev`/`Next`; it does not promise either selection state on page 1 or both states on one page. The frozen workflow deliberately starts with 100 selected of 200, so the harness must discover one checked and one different unchecked row across the real pages, navigate to their recorded pages, remove then add, and restore exactly 100 selected. | `KEYWORD_INTELLIGENCE_KI_W6_REAUTHORED_SUBWINDOW_EVIDENCE.md::EV-KI-W6-R33`; `frontend/test/browser/keyword-intelligence-e2e.mjs::swapOneSelectionItemViaUi` at SHA-256 `fc88c77ebb1bf8f62cafa600afbe5d789cd7a688899a552cff93a0ec0ada0a8f`; `frontend/components/keyword-intelligence/keyword-table.tsx::KeywordTable`; `frontend/lib/keyword-intelligence-view-model.ts::emptyKeywordFilterState/paginate`; frontend HEAD `a39663c8f99d9cc3c4aa1301ff088d5f4a24e7fd`. | Local emitted-browser/isolated-schema diagnostic evidence. The final recovery exited 1 after an observable assertion and therefore is not acceptance evidence or an environment invalidation. It proves a test-navigation defect, not a product, payload, schema, provider, database, or AWS defect. | Deterministic synthetic row labels/counts only; the database URL and private values were not logged. |
| `SRC-KI-044` | OBSERVED | I104 CV15's elevated causal run reached 66 requests and then failed inside Prisma with `Transaction API error: Transaction not found`; the isolated schema and every process cleaned up. The same W6 causal harness had previously localized two five-second interactive-transaction expiries to final publication's `keywordResearch.updateMany`. Current `PrismaKeywordResearchRepository.publishResearchResult()` calls the generic `_transaction()` without options, so Prisma's default interactive timeout governs a transaction that performs the fenced stage reads, stage completion and the maximum 200-row result/default-100 selection write. Immediately before that call, `aggregateMarket()` renews the aggregation lease and stops its 40-second monitor; the repository renewal is exactly 120 seconds. The accepted G-R30/G-R31 precedent separately proves a publication-only 30,000 ms hard timeout with `maxWait:5,000` as a safety ceiling without relaxing its performance contract. | `KEYWORD_INTELLIGENCE_KI_W6_REAUTHORED_SUBWINDOW_EVIDENCE.md` section `Continued V3 attempts after EV-KI-W6-R21` and `EV-KI-W6-R36`; `email_scraper/src/keyword-intelligence/repository.js::_transaction/publishResearchResult` at SHA-256 `be134a3fe039008a9509e940184337e14b276d6bd0e68b6c0830b03e2a68bf48`; `email_scraper/src/aws-pipeline/keyword-intelligence/service.js::createKeywordLeaseMonitor/prepareTerminalLease/aggregateMarket`; `AWS_G14_G15_DEPLOYMENT_EXECUTION_SPECIFICATION.md::G-R30-T3`; `AWS_PIPELINE_EXECUTION_EVIDENCE.md::G-R30/G-R31`; backend HEAD `a411d4b967942228809e85c7a9780c4ad004bf3c`. | Local isolated-Neon and source evidence. R36 identifies the production transaction class but emitted no W6 acceptance certificate. A 30-second ceiling is a rollback deadline, not a claim that publication should normally take 30 seconds. | Only safe error text, counts, timing, source paths and hashes; no database URL, credential, owner value, keyword body or production row. |
| `SRC-KI-045` | OBSERVED | The completed state-159 CV21 capture is an observable `3 pass / 1 fail`, not a transport blocker. `SCN-KI-042` failed with Prisma `P2010` because `$queryRawUnsafe("SELECT pg_sleep(21.000)")` asks Prisma to deserialize PostgreSQL's `void` result. The two pre-existing publication tests and the stale-owner test passed; stderr was empty; the final summary and exit status were durably captured. Returning a supported text column from the same `pg_sleep(21.000)` relation preserves the exact delay and injection boundary while removing only the invalid result decoding. | `/tmp/kiw6-cv21-state159.JPCZ5y/{stdout.log,stderr.log,exit-status}`; `KEYWORD_INTELLIGENCE_KI_W6_REAUTHORED_SUBWINDOW_EVIDENCE.md::EV-KI-W6-R43`; `email_scraper/test/keyword-intelligence-repository.integration.test.js::withPublicationTransactionProbe` at SHA-256 `9ba39e9cac703fc7df6d24268a4a1f8d870ce8d056e4556ee9218c80c698599d`. | Local isolated-test evidence. It proves a test-probe result-shape defect, not a production repository failure; the failed run cannot satisfy CV21. | Safe error code/message, timings, paths and hashes only; no database URL, credential, keyword body or row content. |
| `SRC-KI-046` | OBSERVED | Parent-run I106 CV26 passed 4/4 with zero residual schemas. CV27 then failed after full cleanup because the causal script could not find both checked and unchecked table rows. The script's deliberate server-side revision advance reads `(research.selection && research.selection.items) || []`, but `serializeKeywordResearch()` exposes `selection` as the array itself. It therefore saved an empty selection, reloaded a dashboard with all rows unchecked, and made C107's two-state inventory impossible. | Parent CV26/CV27 terminal output; `frontend/test/browser/keyword-intelligence-e2e.mjs` lines 983–1001 and `swapOneSelectionItemViaUi`; `email_scraper/src/api-serializer.js::serializeKeywordResearch`; browser file SHA-256 `aff4c6174decfc34189fd509cbea84c885cfbb433f061d606f7829c935d25b44`. | Local causal-harness evidence. Cleanup passed and zero cases/controls were accepted. This is a harness consumer-shape defect, not a product selection or pagination failure. | Synthetic counts/status only; no database URL, credential, selection contents or private row data. |
| `SRC-KI-047` | OBSERVED | The new `PrismaKeywordResearchRepository` has exactly 18 `this._transaction(...)` call sites. Only `publishResearchResult` supplies explicit Prisma transaction options; the other 17 inherit the approximately five-second default. The failed I107/CV32 run expired inside `settleAttempt` before its first provider-attempt lookup. Source tracing also shows avoidable sequential operations: task context is loaded before claim and again after claim; task/stage/latest-attempt rows are fetched separately in several methods; successful claim, settlement, terminalization and stage transitions reread rows after conditional writes; throttle uses up to three sequential SQL statements; and `recoverKeywordWork({limit})` validates `limit` but calls unbounded `repository.recover(now)`. The 18 transaction boundaries are `initialize`, `claim`, `recordAttempt`, `settleAttempt`, `markAttemptAmbiguous`, `deferTask`, `scheduleRetry`, `terminalize`, `claimAggregator`, `publishCandidateManifest`, `publishShortlist`, `publishResearchResult`, `failStage`, `saveSelection`, `createRun` initial, `createRun` uniqueness reconciliation, `recover`, and `claimThrottle`. Prisma 6.19.3 exposes `updateManyAndReturn` and `createManyAndReturn` on the generated KeywordResearchTask delegate. | Current working tree at backend source digests `repository.js=359a26f75ba7d605a1c13a5e969ef9ce0a49d0533eb6abe3fa1d6f5bd288c2b5`, `recovery.js=3fcf9b47c5def5ef2729fe7c844661fd17919978ec0f64156de29ac1050a14f0`; `rg -n "this\\._transaction\\("`; direct source inspection of all 18 callbacks and `service.js`/`dataforseo-labs-adapter.js`; generated-client capability inspection; `EV-KI-A-101`. | Local source and isolated-Neon failure evidence. Operation counts describe reachable worst branches before correction; they do not claim live provider, AWS or production timing. Transport batching alone does not change the evidenced per-task DataForSEO cost formula. | Paths, method names, counts, safe Prisma error and aggregate bounds only; no URL, credential, keyword, provider body or production row was read or emitted. |
| `SRC-KI-048` | OBSERVED | I109 CV39 reached the causal selection phase after C112 removed the earlier provider-settlement timeout, then failed because the browser harness's accumulated fetch netlog contains two legitimate successful `PUT .../selection` entries before finalization: the harness-authored revision advance with request `expectedRevision:1`, and the UI-authored final CAS with request `expectedRevision:2`. The current line-1011 filter selects every successful selection PUT, asserts the resulting length is one, and then reads index zero as the final save; it therefore necessarily sees two and would select the advance request even if the length assertion were removed. The surrounding durable witnesses remain coherent: starting revision 1, exactly one stale 409, ending revision 3. | `KEYWORD_INTELLIGENCE_KI_W6_REAUTHORED_SUBWINDOW_EVIDENCE.md::EV-KI-W6-R52`; `frontend/test/browser/keyword-intelligence-e2e.mjs` lines 337–369 and 982–1025 at SHA-256 `f7f055e62f0e2c3c438bdaf739253f0cc917803a8a5115306773066b137fce6f`; I109 CV38 11/11/0 and CV39 diagnostics. | Local emitted-browser/isolated-schema diagnostic evidence. It identifies a harness-oracle partition defect, not a repository CAS, product API, UI, provider, or database defect. CV39 emitted no case/control acceptance certificate. | Synthetic revision numbers, counts, safe paths and status codes only; no URL secret, credential, keyword, request contents, database identity or private row was reproduced. |
| `SRC-KI-049` | OBSERVED | I110 CV45 passed the corrected selection witness and reached the successful same-key handoff retry, but the automatic document navigation to `/runs/<Run.id>` was redirected to `/sign-in`. `frontend/proxy.ts` protects `/runs/:path*` with the installed Neon Auth middleware. That middleware first requires the browser cookie named `__Secure-neon-auth.session_token`; when present it calls the configured `/get-session` endpoint and permits the route only when the returned envelope contains a non-null `session`. The W6 browser carries no session-token cookie, while the current loopback returns only `{user:{id}}`, so the protected workspace is deterministically unreachable even though server-side `/api/*` authentication succeeds. The installed SDK owns session-cache signing; the harness need only seed one opaque non-live token and return the complete deterministic session+user envelope. | `KEYWORD_INTELLIGENCE_KI_W6_REAUTHORED_SUBWINDOW_EVIDENCE.md::EV-KI-W6-R54`; `frontend/proxy.ts`; `frontend/lib/auth/server.ts`; installed `@neondatabase/auth@0.4.2-beta` `dist/next/server/index.mjs::processAuthMiddleware/checkSessionRequired/parseSessionData`; `email_scraper/test/helpers/keyword-intelligence-e2e-harness.js` SHA-256 `7571818027b54bc812d4395d0eb1eec65616b1b939c90baae27fefdb619867c6`; `frontend/test/browser/keyword-intelligence-e2e.mjs` SHA-256 `4fece32a44ab0276e71a813add6e75919453d9a46cb03f8a35c5d84f6fe146f3`. | Local SDK/source and emitted-browser diagnostic evidence. It proves a substitute-auth setup gap, not a production proxy, session, handoff, navigation, API, repository or database defect. It does not prove live Neon Auth, token issuance, cookie cryptographic security or external identity verification. | The proposed token and identities are deterministic test-only values; no live cookie, secret, credential, customer identity or external auth request is used or recorded. |

The corrective and W6 reauthoring reviews introduce **zero unknown consumed payload fields**. The
selection mutation payload is a parent-decided internal browser/API contract;
its strict produced and consumed fields are locked by `DEC-KI-034`.
