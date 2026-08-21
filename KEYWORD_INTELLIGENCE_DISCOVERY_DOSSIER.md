# Keyword Intelligence Discovery Dossier (`A2`)

**Revision:** `KI-DD-7`
**Observed at:** `2026-08-21`
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

The corrective and W6 reauthoring reviews introduce **zero unknown consumed payload fields**. The
selection mutation payload is a parent-decided internal browser/API contract;
its strict produced and consumed fields are locked by `DEC-KI-034`.
