# KI-W6 Sub-Window Decomposition Checklist (`S1`)

Frozen decomposition authored by `KI-W6-WINDOW-AGENT` under assignment
`ASG-KI-W6-WA-01` (A5 state 108, `EV-KI-A-047`, `CHG-KI-024`). Once accepted
by the parent, the sub-window blocks in §5 are immutable; corrections are
appended under new `KI-W6-C***` IDs. This file records no execution status
(`S2`) and no evidence (`S3`).

## 0. Inherited authority and revision pins

```yaml
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-01
window_agent_identity: KI-W6-WINDOW-AGENT
parent_standard_path: PROJECT_AGNOSTIC_DECISION_COMPLETE_CHECKLIST_AUTHORING_STANDARD.md
parent_standard_revision: 3b7a4fd25156e1adfbc92abb835c5f82a0d18c686b1c1150feb202f2d944d2ac
subwindow_standard_path: PROJECT_AGNOSTIC_WINDOW_AGENT_SUBWINDOW_AUTHORING_STANDARD.md
subwindow_standard_revision: 1766f9107ce7d315877b75d4b0ea2b5521dff1c321e12f890b03787d66196ded
contract_path: KEYWORD_INTELLIGENCE_PRODUCT_CONTRACT.md
contract_revision: 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c
decision_path: KEYWORD_INTELLIGENCE_DECISION_LEDGER.md
decision_revision: c2dc635e5aa58f88c1ec465154663d314af68570fd4cbfdfca7b51c393c6f70f
parent_checklist_path: KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md
parent_checklist_revision: 324667cbe0d467ecf4f913c93e91087e75192bd463e0c05b033ee418754a362e
parent_active_state_path: ACTIVE_EXECUTION_STATE.md
parent_active_state_revision: A5 state 108 (assignment block; pins A1/A3/A4 byte-equal above)
```

Scenario authority: `SCN-KI-018` (checklist §"SCN-KI-018 — Full local maximum
path", lines 2993–3012) is the sole remaining uncovered scenario;
`SCN-KI-001`–`017` are parity-complete through accepted windows W1–W5 (scenario
audit recorded in `EV-KI-A-047`), so this decomposition allocates exactly
`SCN-KI-018` plus the `KI-W6-T1` failure/restart/owner matrix, count ceilings
(`DEC-KI-024`), and negative-search obligations (`KI-W6-V4`).

### 0.1 Recorded interpretations (parent decomposition review required)

1. **UI-leg fidelity (`KI-W6-T1` items 1/6/13).** A real-session browser E2E is
   impossible locally without the external Neon Auth service: the server-side
   session cookie is validated upstream (`NEON_AUTH_BASE_URL`), every existing
   browser harness authenticates nothing, and `/runs/*` is proxy-protected.
   `KI-W6-S002` therefore freezes the accepted W5/G-R1 mechanism — real
   production Next build, real Chrome CDP, deterministic same-origin fetch
   interception — with fixtures that are path-derived (built by the same frozen
   deterministic generators that drive `KI-W6-S001`) and an aggregate
   `pathWitness` block in its certificate that `KI-W6-I001` compares byte-equal
   against `KI-W6-S001`'s executed-path certificate values. Real-API
   authenticity, real authentication (`x-user-id` over real HTTP), the real
   worker, the real probe, and the real merge are carried entirely by
   `KI-W6-S001`; `S002` proves the real UI operating on contract-real data plus
   the real unauthenticated gates (401 shapes; `/runs/*` → `/sign-in` redirect
   through the real middleware). No oracle is weakened: every W5-grade UI
   assertion class is re-proven on path-derived data.
2. **"Enter existing downstream merge" endpoint (`KI-W6-T1` item 6).** Frozen
   as the domain-aggregation boundary: `processDiscoveryMessage` ×100 →
   `processDomainAggregation` → `domain-candidate-v1` ×1,000 +
   `domain-stage-manifest-v1` + `publishAwsDomainCheckpoint` (1,000 `Shop`
   rows by `stableShopIdentity`/`shopIdForStableKey`/`runStoreId`, 1,000
   `RunStore` rows, lead stage with 1,000 tasks) + 1,000 `lead.domain`
   dispatches. Full lead/traffic processing is downstream of the named merge
   boundary and remains out of scope, consistent with the G10-accepted
   aggregation tests.
3. **Google probe mock.** `KI-W6-S001` keeps the default
   `researchQueryValidationPipeline` (so `awsProbeSearchPage` writes real
   `google-probe-attempt-v1`/`google-probe-result-v1` artifacts into the
   in-memory artifact store) and mocks only the wire: an in-process
   `globalThis.fetch` router that serves deterministic Custom Search JSON for
   `customsearch.googleapis.com` with an exact call log (100 calls, `num=10`,
   1,000 occurrences) and passes nothing else. DataForSEO is mocked at the
   worker's `runtime.http` seam (W3 pattern); it never touches global fetch.
4. **Harness composition.** `KI-W6-S001` composes three accepted patterns with
   no new product code: the W4 `withServer` injection recipe
   (`createLeadServer` overrides), the W3 worker runtime/message pump
   (`runtimeFor`/`drain`, worker.test.js:181–203), and the G-R9 AWS provider
   snapshot recipe (`awsProviderConfigSnapshot`, aws-pipeline-end-to-end
   integration test lines 42–54). The server-side AWS branch is entered by
   constructing `PrismaRunRepository(prisma, { runExecutionBackend: "aws",
   ...snapshotInputs })` so keyword runs are created with
   `executionBackend: "aws"` and the persisted provider snapshot
   (prisma-run-repository.js:942–975, 1440–1497).
5. **Path-derived handoff fixture.** `S002`'s intercepted `POST */runs`
   response mirrors the real backend contract (`statusUrl:
   "/api/runs/<runId>"`, api.js:520), and `U05` asserts the app navigates to
   exactly that URL. This is stricter than the W5 fixture
   (`/keywords/<id>`) and matches the shipped behavior.
6. **Browser port and artifacts.** `S002` uses port `4348` (W5 used 4347) and
   writes screenshots/logs under `frontend/review-evidence/keyword-intelligence/KI-W6/`
   (gitignored runner output at leaf level; committed only by the requester).
7. **Negative-search comment exclusion (`KI-W6-V4`).** The integrated trees
   contain exactly one non-binding provenance comment naming the standalone
   dashboard (`frontend/components/keyword-intelligence/keyword-dashboard.module.css:2`,
   authored by `KI-W5-S007`). The A4 obligation is "no integrated production
   dependency/script/import references" — a comment is none of these, and the
   file is outside this window's two-file write scope, so a zero-match-period
   gate would be unachievable without a scope violation. The frozen V4 rule
   therefore asserts zero matches on non-comment lines: matches are
   acceptable only on lines whose first non-whitespace token starts a
   comment (`//`, `/*`, `*`, or `#`); any non-comment match fails the gate.
   Pre-verified this session: with the exclusion, all five searches return
   zero non-comment matches.

## 1. Parent-window scope and exclusions (copied unexpanded)

- Write scope: exactly `email_scraper/test/keyword-intelligence-e2e.integration.test.js`
  (leaf `KI-W6-S001`) and `frontend/test/browser/keyword-intelligence-e2e.mjs`
  (leaf `KI-W6-S002`). No other workspace file may be created or edited by any
  leaf or by the window agent.
- Read-only scope: all application source in both repositories; the standalone
  `KeywordSearchVolume/` reference repository (never edited, never executed as
  an integrated runtime); all W1–W5 accepted outputs and existing
  fixtures/harnesses; parent artifacts A1–A7.
- Authorized actions: local test edits, local tests, isolated test-database
  writes (`test/helpers/isolated-postgres.js` only, D2A), local builds, local
  Chrome CDP, read-only negative searches, evidence updates.
- Prohibited: provider calls, AWS operations, production database writes,
  algorithm changes, feature changes, unrelated cleanup, deleting the standalone
  project, commits (requester-only), any `KI-W7` work.
- Successor: `STOP_LOCAL`; `may_start_successor: false` everywhere.

## 2. Starting working-tree inventory (authoring time, 2026-08-20)

- Backend repository clean at HEAD `fac5bb0` ("S010"); frontend repository
  clean at HEAD `c85f93b` ("Harness escape fit"); both verified by
  `git status --porcelain` = empty this session.
- Root: the 36-line owner-controlled relocation set is unchanged
  (authoritative `LC_ALL=C` porcelain digest
  `d1a974b3248df1764007f77b4d423fc9ff0e85fc7d6add16005058e5156495db`, per
  `EV-KI-A-045`); the only additional root changes are this window's three
  subordinate artifacts (S1/S2/S3) once created.
- Both planned writable files are `ABSENT` (verified).
- Baseline suites: backend 272 tests (265 pass, 7 DB-gated skips) and frontend
  `npm run check` exit 0 with 118/118 (`EV-KI-A-046`).

## 3. Planned file set (the complete required changed-file set)

| # | Path | Operation | Starting digest | Leaf |
|---|---|---|---|---|
| 1 | `email_scraper/test/keyword-intelligence-e2e.integration.test.js` | CREATE | `ABSENT` | `KI-W6-S001` |
| 2 | `frontend/test/browser/keyword-intelligence-e2e.mjs` | CREATE | `ABSENT` | `KI-W6-S002` |

Planned two-path per-LF `LC_ALL=C` set digest
`bb9f6381cc3b65d08b696fa1f62a2d75759289b4d4f0f44554ca44a2ebf56edc`.
Required changed-file set = planned set = files owned by initial sub-windows;
each file has exactly one initial owner.

## 4. Digest method (authoritative for every set digest in this window)

Lowercase SHA-256; members UTF-8-encoded; distinct; sorted by unsigned UTF-8
byte order (`LC_ALL=C`); each member followed by exactly one LF; hashed over
the concatenated bytes. Tool-default locale sorting is not authoritative. File
digests are over exact raw bytes; a missing path is the literal token `ABSENT`.
The 20-case required union
(`W6-E01`–`W6-E12`, `W6-U01`–`W6-U08`) has digest
`8d6d002cdf86a30459c2d140977fec3b72c30a8d1c4d612f512bd7c37ed4c523`.

## 5. File sub-window blocks

Semantics common to every block: the recorded
`starting_repository_change_set_digest` is the authoring-time root set
(`d1a974b3248df1764007f77b4d423fc9ff0e85fc7d6add16005058e5156495db`, computed
with the §4 method); leaf preflight (P2) instead proves both nested
repositories clean at their pinned HEADs (`fac5bb0`, `c85f93b`) or containing
exactly the accepted predecessor endings, and the root relocation set
unchanged. Every leaf reads the parent artifacts and installed guides named in
its block before editing. Every leaf reports the exact §7.5 handoff and stops
at `AWAITING_WINDOW_REVIEW`. The `prohibited_actions` list of every block is
exactly: edit any second file; edit the three coordination artifacts or any
parent artifact; start the successor or any later sub-window; communicate with
the parent agent; mutate external state (providers, AWS, databases other than
the prescribed disposable schema, queues, buckets); run any formatter,
installer, generator, or snapshot-update command; weaken any existing test,
fixture, or oracle; commit. It is not repeated per block.

### 5.1 `KI-W6-S001` — backend integrated E2E (`SCN-KI-018` spine)

```yaml
subwindow_id: KI-W6-S001
type: FILE
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-01
assigned_agent: LEAF (KI-W6-S001-AGENT)
predecessors: []
successor_reserved_for: WINDOW-AGENT
writable_file: email_scraper/test/keyword-intelligence-e2e.integration.test.js
file_operation: CREATE
starting_file_digest: ABSENT
starting_repository_change_set_digest: d1a974b3248df1764007f77b4d423fc9ff0e85fc7d6add16005058e5156495db
read_only_scope:
  - email_scraper/src/** (server.js, keyword-intelligence/*, aws-pipeline/**, prisma-run-repository.js, prisma-client.js, query-review.js, query-prober.js, search.js, http-client.js, config.js, api-errors.js, api-serializer.js, shop-persistence-contract.js)
  - email_scraper/test/keyword-intelligence-worker.test.js, keyword-intelligence-worker-flow.test.js, keyword-intelligence-handoff.integration.test.js, keyword-intelligence-repository.integration.test.js, keyword-intelligence-adapter.test.js, keyword-intelligence-api.test.js
  - email_scraper/test/helpers/isolated-postgres.js, aws-pipeline-e2e-harness.js
  - email_scraper/test/aws-pipeline-end-to-end.integration.test.js, aws-pipeline-domain.test.js, aws-pipeline-traffic.integration.test.js
  - email_scraper/prisma/schema.prisma, prisma.config.ts, package.json
  - parent artifacts A1–A7, this S1, S2, S3
authorized_actions: [create the one writable file, run node --check on it, run the file via npm run test:integration with ALLOW_DATABASE_TESTS=true and an isolated TEST_DATABASE_URL, run focused existing keyword suites, record S3 leaf evidence via the window agent]
prohibited_actions: (the common list; additionally) any edit under email_scraper/src, any test-database use other than a disposable schema created via test/helpers/isolated-postgres.js, any real network call
may_start_successor: false
```

**Mechanical trace (§7.2):** implements `KI-W6-T1` items 1–12 for the non-UI
surface; requirements `REQ-KI-001`–`022` (API/worker/selection/handoff/
probe/merge subset exercised end-to-end), invariants `INV-KI-001`–`015`
(S3-before-Neon, Neon-before-SQS, idempotent first-terminal, fenced
publication, paid ledger reservation, owner scoping), exclusions
`EXC-KI-001`–`008` (no cancel path; no raw provider retention), `D2`/`D2A`/`D3`
(asserted literally), `D11` counters, `D13` safe-error surfaces; scenario
`SCN-KI-018` (all non-UI activation witnesses); decisions `DEC-KI-002`,
`004`–`009`, `013`–`022`, `024`, `026`–`028`. Every allocated item terminates
in an executable assertion named below.

**Exact file transformation (§7.3).** Create exactly this Node ESM test file;
`node --check` must pass. Structure and content, in order:

1. **Imports (exactly):** `node:assert/strict`, `node:test`, `node:crypto`
   (`createHash`), `test/helpers/isolated-postgres.js`
   (`createIsolatedTestSchema`, `deployPrismaMigrations`,
   `assertMigrationStayedInSchema`), `src/prisma-client.js`
   (`createPrismaClient`), `src/prisma-run-repository.js`
   (`PrismaRunRepository`, `awsProviderConfigSnapshot`), `src/keyword-intelligence/repository.js`
   (`PrismaKeywordResearchRepository`), `src/aws-pipeline/keyword-intelligence/service.js`
   (`processKeywordMessage`, `processInitialize`), `src/aws-pipeline/keyword-intelligence/recovery.js`
   (`recoverKeywordWork`), `src/aws-pipeline/keyword-intelligence/keys.js`
   (`keywordResultKey`, `keywordManifestKey`), `src/aws-pipeline/keyword-intelligence/contracts.js`
   (`keywordMessageSchema`), `src/aws-pipeline/services/discovery-worker.js`
   (`processDiscoveryMessage`), `src/aws-pipeline/services/domain-aggregator.js`
   (`processDomainAggregation`), `src/aws-pipeline/repositories/pipeline-coordinator-repository.js`
   (`PipelineCoordinatorRepository`), `src/server.js` (`createLeadServer`).
2. **Skip gate:** `const enabled = process.env.ALLOW_DATABASE_TESTS === "true" && Boolean(process.env.TEST_DATABASE_URL);`
   every database test uses `{ skip: !enabled }`. A non-database final
   certificate test runs always (below).
3. **Constants:** `OWNER = "owner_kiw6"`, `OTHER = "owner_b_kiw6"`; fixed clock
   box `const clock = { nowMs: Date.parse("2026-08-20T00:00:00.000Z") }` and
   `now()` returning `new Date(clock.nowMs)`; `QUEUE_URL =
   "https://sqs.fixture/keyword-research"`, `LEAD_QUEUE_URL =
   "https://sqs.fixture/lead"`, `BUCKET = "kiw6-fixture-bucket"`;
   `AWS_INPUTS` = exactly the G-R9 snapshot inputs
   (`browserlessUrl: "https://fixture.example"`, `googleSearchEngineId:
   "fixture-cx"`, `googleResultsPerQuery: 10`, `requestTimeoutMs: 10000`,
   `maxPagesPerStore: 5`, `pageFetchConcurrency: 2`, `maxQueries: 200`,
   `generatedQueryCount: 10`, `queryProbeFreshnessMs: 60000`,
   `queryProbeConcurrency: 4`, `minQueryResults: 1`, `minQueryUniqueHosts: 1`,
   `minQueryRelevantResults: 1`, `minQueryRelevanceRatio: 0.1`,
   `minQueryBaseScore: 1`, `browserlessEnabled: false`,
   `enableAiNormalization: false`) plus `googleApiKey: "fixture-google-key"`,
   `dataForSeoLogin: "fixture-login"`, `dataForSeoPassword:
   "fixture-password"`; `SEEDS = ["seed one","seed two","seed three","seed
   four","seed five"]` (the SCN-KI-018 five-seed input); `REQUIRED` = the
   twelve case IDs `W6-E01..W6-E12`; registries `registered`/`executed`/
   `skipped`/`witnesses`/`failures` arrays.
4. **In-memory fakes (re-implement to this exact contract, single file):**
   `memoryS3()` — a `Map`-backed S3 client accepting `PutObjectCommand`
   (reject overwrite of an existing key with the stored body mismatch; store
   body/metadata), `GetObjectCommand` (throw `ObjectNotFoundError`-shaped
   error with name `"NoSuchKey"` for missing keys), returning
   `{ status: 200 }`/`{ status: 404 }`-free shapes consumed by
   `S3ArtifactStore` (copy the accepted shapes from
   `keyword-intelligence-worker-flow.test.js` `memoryS3`, lines 160–182);
   `memoryDispatcher()` — `{ sent: [], options: [], async sendOne(url,
   message, schema) { parse via schema; push; return { sentItemIds:[1],
   failedItemIds:[] }; }, async sendMany(url, messages, schema) { ...; return
   { sentItemIds: messages.map((_,i)=>i), failedItemIds: [] }; } }`;
   `keywordHttp(mode)` — the DataForSEO seam: `{ calls: [], http }` where
   `http(url, init)` records `{ url, body: init?.body }` and answers by URL
   substring (`keyword_suggestions`, `related_keywords`,
   `keyword_overview`) with envelope builders below; `mode` is one of
   `"full"` (default), `"parserDefect"`, `"ambiguousOnce"`.
5. **Deterministic provider envelope builders (frozen):** for seed index
   `s` (0–4), suggestions returns exactly 30 items with keyword
   `w${s}a${String(i).padStart(2,"0")}` and related returns exactly 30 items
   `w${s}b${String(i).padStart(2,"0")}` (300 distinct candidates total; the
   words carry a benign product noun, e.g. `w${s}a${i} coffee grinder`
   template — fixed literal strings); every item carries the valid metric
   shape accepted by the strict expansion parser (copy per-item fields from
   the accepted `expansionResponse`, worker-flow.test.js:222). The overview
   envelope echoes one metrics item for every requested keyword (valid
   `keyword_overview` shape from `overviewResponse`, worker-flow.test.js:199)
   with volume `1000 + (index % 7) * 111`, `monthly_searches` length 15.
   `parserDefect` mode: suggestions envelope omits the required `tasks`
   array member for one call. `ambiguousOnce` mode: the first overview call
   returns `{ status: 200, json: async () => { throw new SyntaxError("bad
   json"); } }` (the accepted SCN-KI-024 ambiguity trigger,
   adapter.test.js:359–369); later calls answer normally.
6. **Google fetch router (frozen):** before server creation, wrap
   `globalThis.fetch`: if `new URL(input).host ===
   "customsearch.googleapis.com"`, record `{ query: searchParams.get("q"),
   num: searchParams.get("num") }` and return `new Response(JSON.stringify(
   googleFixture(searchParams.get("q"))), { status: 200, headers: {
   "content-type": "application/json" } })`; otherwise delegate to the saved
   original fetch. `googleFixture(q)` returns the strict Custom Search shape
   (`kind: "customsearch#search"`, `searchInformation.totalResults: "10"`):
   for query index `qi` parsed from the frozen query text suffix (queries are
   `site:myshopify.com/products <keyword>`; `qi` = the RunQuery row order,
   recovered from a fixed map built when the run is created), ten items with
   `link: https://q${qi}s${j}.myshopify.com/products/p${j}`, title
   `Store q${qi}s${j}`, snippet `Fixture occurrence q${qi}s${j}` (j = 0..9) —
   1,000 distinct domains across the 100 queries. The wrapper is restored in
   the top-level `finally`.
7. **Harness construction (single recipe):** one top-level database test
   `"KI-W6 integrated local maximum path (SCN-KI-018) in one disposable
   schema"` with `{ skip: !enabled, timeout: 900000 }`; inside: `const schema
   = \`kiw6_e2e_${Date.now().toString(36)}_${process.pid}\``; isolated schema
   + `deployPrismaMigrations` + `assertMigrationStayedInSchema` (D2A);
   `prisma = createPrismaClient(scopedUrl)`; `runRepository = new
   PrismaRunRepository(prisma, { runExecutionBackend: "aws", ...AWS_INPUTS })`;
   `keywordRepo = new PrismaKeywordResearchRepository(prisma)`; `s3 =
   memoryS3()`; `store = new S3ArtifactStore({ client: s3, bucket: BUCKET,
   maxBytes: 33554432 })` (import from
   `src/aws-pipeline/adapters/artifact-store.js`); `keywordDispatcher =
   memoryDispatcher()`; `pipelineDispatcher = memoryDispatcher()`; keyword
   runtime `kwRuntime = { repository: keywordRepo, artifactStore: store,
   dispatcher: keywordDispatcher, config: { awsPipelineBucket: BUCKET,
   awsPipelineKeywordResearchQueueUrl: QUEUE_URL }, s3Client: s3, clock:
   now, http: keywordHttp().http, secrets: { dataForSeoLogin:
   AWS_INPUTS.dataForSeoLogin, dataForSeoPassword: AWS_INPUTS.dataForSeoPassword } }`;
   coordinator = `new PipelineCoordinatorRepository(prisma)`; downstream
   runtime `pipeRuntime = { coordinator, repository: runRepository,
   artifactStore: store, dispatcher: pipelineDispatcher, config: {
   awsPipelineBucket: BUCKET, awsPipelineLeadQueueUrl: LEAD_QUEUE_URL },
   s3Client: s3, clock: now, secrets: { googleApiKey:
   AWS_INPUTS.googleApiKey } }`; `server = createLeadServer({ ...
   AWS_INPUTS, runExecutionBackend: "aws", backendApiToken: undefined }, {
   repository: runRepository, pipelineRuntimeFactory: async () =>
   pipeRuntime, logger: () => {}, setIntervalFn: () => ({ unref() {} }),
   clearIntervalFn: () => {} })`; `server.listen(0, "127.0.0.1")`; `base` =
   the bound URL; `headers(owner)` = `{ "content-type": "application/json",
   "x-user-id": owner }`. Teardown in `finally`: close server, drop the
   schema (`DROP SCHEMA ... CASCADE` + absence assert + admin disconnect),
   restore fetch, assert `rss < 1536 MiB` via `process.memoryUsage().rss`.
   The message pump is the `drain` algorithm of worker.test.js:181–203
   (queue/seen/prevSent, throttle reset before each non-aggregate message,
   runaway guard 200), calling `processKeywordMessage(message, kwRuntime)`.
8. **Subtests (sequential `await context.test(...)` inside the schema; each
   registers + executes exactly its case ID and records at least one
   activation witness string):**
   - **`W6-E01` authenticated seed creation and owner isolation:** POST
     `/api/keyword-research` with `headers(OWNER)`, body `{"seeds": SEEDS}`
     → 202; response research `state: "queued"`, `statusUrl
     "/api/keyword-research/<id>"`; DB row owner-scoped to OWNER; exactly one
     `keyword.initialize.v1` message in `keywordDispatcher.sent`; POST with
     an invalid body (`{"seeds": []}`) → 400 `KEYWORD_RESEARCH_INPUT_INVALID`;
     six seeds → 400; GET the research with `headers(OTHER)` → 404
     `KEYWORD_RESEARCH_NOT_FOUND` and zero `OTHER` rows anywhere; duplicate
     `x-user-id` header → 401 `USER_CONTEXT_REQUIRED`; missing header → 401.
   - **`W6-E02` full worker flow with exact counters:** run the pump from the
     initialize message to quiescence; assert research `state: "completed"`,
     `selectionRevision: 1`, `result.keywords.length === 200`, default
     `selection.items.length === 100`; stages exactly
     `["expansion","anchor_screen","market_overview"]` all `completed`;
     tasks: 10 expansion + 1 anchor + 8 market = 19, all `succeeded`;
     expansion manifest candidates count `=== 300`; shortlist manifest
     keywords `=== 200`; provider `http.calls.length === 19` (2 per seed + 1
     anchor + 8 market); keyword S3 objects `=== 23` (19 task artifacts + 3
     manifests + 1 `keywordResultKey` result) with the result artifact
     validated through `S3ArtifactStore.getValidated` against
     `keywordResearchResultArtifactSchema`; attempt rows `=== 19` all
     `succeeded`; paid ledger: every attempt reserved USD before the call
     (assert reservation rows/`mayCall` ordering per `DEC-KI-009`); message
     types seen include all four (`initialize`, `expansion.task`,
     `overview.task`, `aggregate.check`).
   - **`W6-E03` overselect, conflict ceiling, resolution:** GET the research
     → completed view with `result`, `selection`, `selectionConflicts ===
     null`; PUT `/selection` with `expectedRevision: 1` and a 200-item draft
     built from all 200 keywords including two seeded near-similar pairs
     (choose keywords `w0a03`/`w0a04` and `w1b05`/`w1b06` with tokens crafted
     to be near-similar per `DEC-KI-015` — fixed literal keywords guarantee
     this) → 409 `KEYWORD_SELECTION_HAS_CONFLICTS` with both conflicts
     listed; conflict analysis pair comparisons at draft 200 equal the
     19,900 ceiling (assert `200*199/2`); PUT with the conflicts resolved
     (drop one of each pair, then trim to exactly 100 items: the first 98 by
     frozen order plus the two kept pair members) → 200 with
     `selectionRevision: 2`; PUT again with `expectedRevision: 1` → 409
     `KEYWORD_SELECTION_REVISION_CONFLICT`.
   - **`W6-E04` atomic handoff, replay, stale revision, snapshot
     immutability, owner isolation:** wrap `prisma` with the W4 operation-spy
     proxy (handoff.integration.test.js:73–94) around `createRun`; POST
     `/runs` `{ expectedSelectionRevision: 2, clientRequestId:
     "kiw6-client-request-0001" }` (matches `^[A-Za-z0-9_-]{16,80}$`) with
     `headers(OWNER)` → 201 `{ run, statusUrl }`; `statusUrl ===
     "/api/runs/" + run.id`; Run row `state:
     "awaiting_query_confirmation"`, `phase: "query_review"`,
     `queryPlanSource: "keyword_research"`, `keywordResearchId` set;
     exactly 100 `RunQuery` rows with `query === "site:myshopify.com/products
     <keyword>"`, `source: "generated"`, `validationState: "pending"`,
     `generationReason: "keyword_research"`, `keywordResearchItemId` set,
     `probeFingerprint: null`; the transaction performed exactly the five
     named ops (`keywordResearch.findUnique`,
     `keywordResearchHandoff.findUnique`, `run.create`,
     `runQuery.createMany`, `keywordResearchHandoff.create`); POST replay
     with the same `clientRequestId` → 200 with the same `run.id` and no new
     rows; POST with `expectedSelectionRevision: 1` → 409
     `KEYWORD_SELECTION_REVISION_CONFLICT`; edit the research selection
     (swap one item, `expectedRevision: 2`) → `selectionRevision: 3`; then
     GET `/runs/<id>/queries` and the persisted `keywordSelectionSnapshot`:
     snapshot still carries `selectionRevision: 2`, the original 100 items,
     and the original `selectionFingerprint` (immutability under later
     research edit); with `headers(OTHER)`: GET research → 404, GET
     `/api/runs/<id>` → 404, GET queries → 404, and `OTHER` has zero
     `UserShop`/`RunStore`/`Run` rows at every later checkpoint.
   - **`W6-E05` query review edits and revision conflicts:** GET
     `/api/runs/<id>/queries` → `revision: 1`, 100 editable rows; PUT with
     `revision: 1` and a mixed edit: 97 rows unchanged, 3 rows reworded
     within the keyword rules (prefix intact, ≤12 words, no operators;
     fixed replacement literals) → 200, `revision: 2`, lineage
     `keywordResearchItemId` preserved on every row; PUT with `revision: 1`
     again → 409 `QUERY_REVISION_CONFLICT`; PUT introducing an
     out-of-rules edit (operator `OR`) → 422 `QUERY_LIST_INVALID`.
   - **`W6-E06` confirm, real probe path, S3 probe artifacts, confirmed
     dispatch:** POST `/api/runs/<id>/start` `{ revision: 2 }` → 202, run
     `state: "queued"`, `phase: "scraping"`; await the in-process
     `executeRun` drain (poll the run row to `stage` beyond
     `queued_query_validation`, bounded wait 120 s); assert: exactly 100
     Google fetch calls, every call `num=10`, 100 distinct `q` values;
     1,000 occurrence URLs recorded; every `RunQuery` row
     `validationState: "valid"`, `probeContractVersion:
     "google-probe-v2"`, `probeFingerprint` matching
     `/^[a-f0-9]{64}$/`, `probeResults.length === 10`, `probedAt` set;
     probe S3 artifacts: exactly 200 keys matching
     `google-probe-attempt-v1`/`google-probe-result-v1` key patterns (100
     each); one `confirmed-query-manifest-v1` artifact; discovery stage
     registered with expected 100 tasks; exactly 100 `discovery.query`
     messages in `pipelineDispatcher.sent`; validation failure path is not
     taken (all rows valid — the frozen fixtures satisfy the thresholds in
     `AWS_INPUTS`).
   - **`W6-E07` downstream stable-domain merge at 1,000 scale:** drive
     `processDiscoveryMessage` for each of the 100 discovery messages with
     `pipeRuntime` → 100 per-query discovery artifacts; then
     `processDomainAggregation` for the discovery `aggregation.check` →
     assert: 1,000 `domain-candidate-v1` puts; one `domain-stage-manifest-v1`
     with `domains.length === 1000` sorted by `shopId`; `publishAwsDomainCheckpoint`
     effects in the DB: 1,000 `Shop` rows with `stableKey` matching
     `domain:q{i}s{j}.myshopify.com`-derived identity, `id` equal to
     `shopIdForStableKey(stableKey)`; 1,000 `RunStore` rows with `id ===
     runStoreId(runId, shopId)`; lead stage registered with 1,000 tasks; 1,000
     `lead.domain` messages sent to `LEAD_QUEUE_URL`; the manifest work-plan
     marks every domain `needsLead: true`; `duplicateCount === 0` (all
     domains distinct).
   - **`W6-E08` restart, duplicate/reorder/redelivery, full lease expiry
     (second research, 1 seed):** POST a second research (seed one only);
     before pumping, reorder: deliver `keyword.aggregate.check.v1` for the
     expansion stage first → outcome reflects `not_ready`/no premature
     advance (stage stays `collecting`, research `running`); deliver the
     initialize message twice → task set unchanged (11 tasks, no
     duplicates); expire leases: advance `clock.nowMs` by 61,000 and call
     `recoverKeywordWork({ now: now(), limit: 100 }, kwRuntime)` →
     re-dispatched work drains; simulate API restart: close the server,
     construct a fresh `createLeadServer` on the same `prisma` (same recipe),
     GET the research with `headers(OWNER)` → same durable state; complete
     the research via the pump → `completed` with 11 tasks; counters: 11
     provider calls for this research.
   - **`W6-E09` ambiguity is terminal (third research, 1 seed,
     `ambiguousOnce`):** pump with the ambiguous overview seam → the anchor
     task attempt is `ambiguous`, `safeErrorCode:
     "KEYWORD_PROVIDER_AMBIGUOUS"`, task/stage/research `failed` terminally;
     exactly one attempt row for the anchor task (no sixth-attempt storm);
     GET the research → safe error surface only (no raw provider body
     anywhere: assert the serialized `safeError.code` and that no response
     field contains `"tasks"` envelope bodies).
   - **`W6-E10` no-cancel and no-delete paths:** `DELETE
     /api/keyword-research/<id>` → 404 (no route); `POST
     /api/keyword-research/<id>/cancel` → 404; the three researches remain
     in terminal/durable states (`EXC-KI-007`).
   - **`W6-E11` negative controls (four, each: inject defect → assert the
     E2E oracle fails → restore; `negative_controls_falsified` increments
     only on a control that fails to fail):**
     1. *bypass worker:* create a fourth research, deliver initialize, do
        NOT deliver the anchor overview message, deliver the final
        `aggregate.check` → research is not `completed` (the W3
        worker-bypass oracle, worker.test.js:680–697).
     2. *bypass parser:* `parserDefect` http mode on a fifth research →
        the malformed suggestions call produces a failed attempt with a
        safe parse code, no S3 artifact for that task, task not terminal,
        retry scheduled (assert `nextAttemptAt` in the future).
     3. *bypass snapshot:* after the main run's handoff, tamper the run's
        `keywordSelectionSnapshot` in the DB (`selectionRevision: 99`) →
        POST `/start` → validation returns invalid snapshot → run returns
        to `awaiting_query_confirmation` with `confirmedQueryRevision:
        null`; restore the snapshot byte-exactly afterwards (the
        immutability assertions of `W6-E04` are re-asserted post-restore).
     4. *bypass stable merge:* inside `W6-E07`, before the 100th discovery
        message is delivered, run `processDomainAggregation` → aggregator
        refuses (`not_ready`), zero `Shop`/`RunStore` rows and zero
        `lead.domain` messages exist at that point; then deliver the final
        message, aggregate again → merge completes exactly as specified (no
        premature or partial merge possible). The control counts as
        falsified only if the premature aggregation produced a checkpoint.
   - **`W6-E12` resource ceilings and safe logging:** assert total S3
     object count `===` the frozen total (23 keyword objects for research 1
     + 11 for research 2 + 0 for research 3 + 0/… for NC researches + 200
     probe + 1 confirmed manifest + 100 per-query + 1,000 domain candidates
     + 1 domain manifest — computed from the case executions as a running
     counter asserted exactly); `process.memoryUsage().rss() < 1536 MiB`;
     the whole test's wall time recorded into `witnesses`; no log line or
     response body in the captured server log contains any seed keyword,
     provider body, or credential (assert by scanning the recorded
     logger output for `dataForSeoPassword`, `"tasks"`, and the literal
     seed strings).
9. **Certificates:** after the database test, a non-skipped test
   `"KI-W6 E2E execution certificate"` asserts `registered`, `executed`,
   `skipped`, `witnesses`, `failures` invariants (required = registered =
   executed when enabled; all twelve in `skipped` when disabled) and writes
   exactly one stdout line
   `KI_W6_E2E_EXECUTION_CERTIFICATE={"file":"keyword-intelligence-e2e.integration.test.js","required":[...],"registered":[...],"executed":[...],"skipped":[...],"activationWitnesses":[...],"oracleFailures":[...],"negativeControls":{"expected":4,"falsified":0},"pathWitness":{"candidateKeywords":300,"shortlistKeywords":200,"resultKeywords":200,"defaultSelectionItems":100,"finalSelectionItems":100,"runQueries":100,"probeCalls":100,"occurrences":1000,"uniqueDomains":1000},"digests":{"required":"<§4 digest>","registered":...,"executed":...}}`
   with §4 digests. `pathWitness` values are the literal frozen numbers;
   every corresponding subtest asserts its equal before registering its ID.

**Exact checks (§7.4).** C1 write-set proof: `git -C email_scraper status
--porcelain` attributable delta is exactly the one new untracked test file
(CREATE; the schema is disposable and dropped; no other path changes). C2
`node --check test/keyword-intelligence-e2e.integration.test.js` → exit 0
(LOCAL_NOW). C3 focused existing suites still pass: `node --test
test/keyword-intelligence-worker.test.js
test/keyword-intelligence-handoff.integration.test.js` with and without the
DB opt-in as applicable (LOCAL_NOW; no regression). C4 the file itself runs
green twice: once without opt-in (all twelve skipped, certificate emits
skipped set) and once with `ALLOW_DATABASE_TESTS=true npm run
test:integration` against an isolated `TEST_DATABASE_URL` distinct from
production (exit 0; certificate executed = required) — the leaf records both
runs; the official gate re-execution belongs to `KI-W6-I001` (DEFERRED).
C5 secrets: the file contains no real credential, token, production ID, or
provider body (grep the file for the fixture literals only). C6 the file
imports no module outside `email_scraper/src`, `email_scraper/test/helpers`,
`node:` builtins, and `zod` indirectly via src imports.

- [ ] P1 Revisions, assignment identity, writable file, baseline digest (`ABSENT`), and predecessor evidence match.
- [ ] P2 Starting repository status and protected dirty changes match the recorded baseline (both nested repos clean at `fac5bb0`/`c85f93b`; root relocation set unchanged; writable file `ABSENT`).
- [ ] T1 Apply every ordered transformation and no other edit to the writable file.
- [ ] V1 Run every LOCAL_NOW check and record its activation witnesses and exact assertions.
- [ ] V2 Prove the attributable workspace changed-file set is exactly the writable file.
- [ ] V3 Prove required local coverage IDs (`W6-E01`–`W6-E12`) equal registered and executed local IDs with zero skips (opt-in run).
- [ ] H1 Return the exact diff, ending digest, commands, outcomes, and residual integration obligations.
- [ ] H2 Confirm no prohibited action, second-file edit, successor work, external mutation, or parent communication occurred.
- [ ] H3 Stop at AWAITING_WINDOW_REVIEW.

### 5.2 `KI-W6-S002` — frontend browser integrated E2E (UI leg of `SCN-KI-018`)

```yaml
subwindow_id: KI-W6-S002
type: FILE
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-01
assigned_agent: LEAF (KI-W6-S002-AGENT)
predecessors: [KI-W6-S001]
successor_reserved_for: WINDOW-AGENT
writable_file: frontend/test/browser/keyword-intelligence-e2e.mjs
file_operation: CREATE
starting_file_digest: ABSENT
starting_repository_change_set_digest: d1a974b3248df1764007f77b4d423fc9ff0e85fc7d6add16005058e5156495db
read_only_scope:
  - frontend/test/browser/keyword-intelligence-dashboard.mjs (the W5 harness: Cdp class, fixture injection, phases, certificate)
  - frontend/scripts/g-r1-real-component-browser.mjs (redirect-probe precedent)
  - frontend/lib/keyword-intelligence-validation.ts, keyword-intelligence-view-model.ts, client-api.ts, api-types.ts
  - frontend/components/keyword-intelligence/** and frontend/app/keywords/**, frontend/app/runs/[runId]/**
  - frontend/lib/backend-proxy.ts, auth/server.ts, frontend/proxy.ts
  - frontend/package.json; installed Next.js documentation per workspace rules
  - parent artifacts A1–A7, this S1 (especially §0.1 interpretation 1/5), S2, S3, and the S001 leaf evidence for the path-derived fixture parity values
authorized_actions: [create the one writable file, run node --check on it, execute the harness once with full production build (K6_W6_SKIP_BUILD=1 escape only for intermediate fixes, never for the recorded official run), capture screenshots/logs under frontend/review-evidence/keyword-intelligence/KI-W6/, record S3 leaf evidence via the window agent]
prohibited_actions: (the common list; additionally) any edit under frontend/app, frontend/lib, frontend/components, frontend/scripts; any real backend/Neon Auth/provider network access; auth credential fabrication beyond the frozen fixture boundary
may_start_successor: false
```

**Mechanical trace (§7.2):** implements `KI-W6-T1` items 1/6/13 for the UI
surface — "operate real UI", "load all dashboard surfaces", overselect/
conflict resolve, finalize, edit-after-handoff reload durability, and the
`SCN-KI-018` UI/dashboard-canvases activation witnesses on path-derived
data (`REQ-KI-001`, `006`–`009`, `013`–`014`, `017`–`018`; `DEC-KI-013`–
`015`, `023`; the W5 surface inventory). Interface freeze: the intercepted
payload shapes are exactly the W4-accepted API contract envelopes validated
through `parseResearchEnvelope`/`parseRunHandoffEnvelope` before injection.

**Exact file transformation (§7.3).** Create exactly this Node ESM script by
cloning the W5 harness architecture (keyword-intelligence-dashboard.mjs) with
these frozen deltas — five phases, single `KI_W6_BROWSER_E2E_CERTIFICATE=`
stdout line, artifacts under
`frontend/review-evidence/keyword-intelligence/KI-W6/`:

1. **Constants:** port `4348`, `baseUrl = "http://127.0.0.1:4348"`; output
   dir as above; `REQUIRED = ["W6-U01".."W6-U08"]`; registries and
   `pathWitness = { candidateKeywords: 300, shortlistKeywords: 200,
   resultKeywords: 200, defaultSelectionItems: 100, finalSelectionItems: 100,
   runQueries: 100, probeCalls: 100, occurrences: 1000, uniqueDomains: 1000 }`
   (byte-equal to `S001`'s certificate `pathWitness` — the I001 comparison).
2. **Phase A (build/start):** identical to W5 lines 848–912 with the port
   delta; build refusal semantics identical (`K6_W6_SKIP_BUILD=1` explicit;
   skip mode refuses when `.next` is absent).
3. **Phase B (path-derived fixtures):** builders mirroring the S001 frozen
   generators — 300 candidate keywords (`w${s}a${i}` / `w${s}b${i}`,
   s = 0..4, i = 00..29), the completed `ResearchView` envelope carrying
   exactly the 200 shortlist-derived keyword rows (identical keyword
   literals and metric formula `1000 + (index % 7) * 111`), summary/clusters
   derived from those rows by the same fixed aggregation the W5 builders
   use, `selection` of the default 100, `selectionRevision: 2`,
   `selectionConflicts: null`; a queued view and a three-step running poll
   sequence for `POLL_ID` (queued → running/anchor_screen → running/
   market_overview → completed); a handoff envelope
   `{ run: { runId: "run_e2e_fixture_0001", statusUrl:
   "/api/runs/run_e2e_fixture_0001" }, statusUrl:
   "/api/runs/run_e2e_fixture_0001" }` (real backend shape, §0.1 item 5);
   every envelope validated through `parseResearchEnvelope` /
   `parseRunHandoffEnvelope` before use (W5 line 591 pattern). A
   `pathWitness` self-check runs at startup: the completed envelope's
   keyword-row count must equal `pathWitness.resultKeywords` and its
   candidate id pool must equal 300 distinct literals — a mismatch aborts
   before Chrome launches.
4. **Phase C (interception):** the W5 `fixtureInjection` wrapper (lines
   600–699) with the W6 deltas: `POST /api/keyword-research` returns
   `{ research: queuedView }`; `GET */` serves the poll sequence for
   `POLL_ID` then the completed view, 404 `RESEARCH_NOT_FOUND` otherwise;
   `PUT */selection` serves `state.conflictMode` (409
   `KEYWORD_SELECTION_REVISION_CONFLICT`) and a conflict-bearing 409
   `KEYWORD_SELECTION_HAS_CONFLICTS` variant for the overselect step;
   `POST */runs` records `clientRequestId`, serves the handoff envelope,
   supports `runsDelayMs` for the double-click window; all non-app URLs pass
   through and are recorded; requests log into `globalThis.__kiE2E.requests`.
5. **Phase D (subtests, sequential, each registers + executes its ID, zero
   console errors / zero uncaught exceptions / zero non-app network asserted
   globally after each):**
   - **`W6-U01` create → durable poll → completed:** on `/keywords`, fill
     five seed chips (the five S001 seed literals), submit → app navigates to
     `/keywords/<POLL_ID>`; the dashboard renders the research-status
     surface (`surface:research-status`) while polling; the real client poll
     ladder advances through the poll sequence (assert ≥3 GETs recorded
     before completion); terminal completed dashboard renders
     `surface:research-dashboard`.
   - **`W6-U02` all dashboard surfaces + canvases on path-derived data:**
     assert presence of all nine `surface:*` ids and all eleven `chart:*`
     canvases with nonzero size and a `$chartjs` instance each, plus
     `landscape:cluster-scene` with a nonzero landscape canvas; "200 rows"
     data-derived meta text.
   - **`W6-U03` overselect → conflicts → resolve → save:** select all 200,
     trigger the seeded near-similar pair selection → conflict review
     surface lists the conflicts and finalize is blocked; resolve (drop the
     fixed pair members, land on exactly 100) → PUT succeeds; revision
     advances to 3; the request log shows exactly one PUT with the resolved
     item set.
   - **`W6-U04` stale revision 409 recovery:** force `conflictMode` → save
     → 409 conflict surface rendered, no silent local-draft overwrite
     (assert the local draft rows unchanged after the 409); reload → fresh
     envelope revision, draft reset to server truth.
   - **`W6-U05` finalize + idempotent double-click + statusUrl:** click
     finalize twice within the `runsDelayMs` window → exactly one `POST
     */runs` in the log with one retained `clientRequestId` matching
     `^[A-Za-z0-9_-]{16,80}$`; the app navigates to
     `/api/runs/run_e2e_fixture_0001` (assert the final URL equals the
     statusUrl — the real backend behavior).
   - **`W6-U06` edit-after-handoff + reload durability:** navigate back to
     `/keywords/<POLL_ID>`, still editable (research completed); change one
     selection item (fixed literal), save → revision 4; full page reload →
     revision 4 durable, selection preserved, zero POST/PUT on reload
     (GET-only durability).
   - **`W6-U07` unauthenticated gates (real routes, no interception for
     these probes):** Node-side fetch `GET /api/keyword-research/kr_e2e_fixture`
     → 401 `AUTHENTICATION_REQUIRED` with `Cache-Control: no-store`; unknown
     query key → 400 `INVALID_QUERY_PARAMETERS`; bad id → 400
     `INVALID_RESEARCH_ID`; `localStorage` keys exactly `["ki-dashboard-theme"]`.
   - **`W6-U08` run-page auth gate:** browser navigate
     `/runs/run_e2e_fixture_0001` with no session → final URL
     `/sign-in` (the real proxy redirect, g-r1:293–295 precedent) and the
     sign-in surface renders.
   - **`NC-W6-05` fixture-divergence control (falsified only if undetected):**
     a second injection switches the completed envelope's row 0 volume to a
     diverged value → the harness envelope-consistency oracle (Phase B
     self-check re-run on the diverged copy) must flag divergence; the
     subtest asserts the oracle threw/flagged.
6. **Phase E (teardown/certificate):** W5 `finally` semantics — server log,
   CDP close, process-group SIGTERM for Chrome and Next, temp dir removal,
   and exactly one
   `KI_W6_BROWSER_E2E_CERTIFICATE={"file":"keyword-intelligence-e2e.mjs","required":[...8],"registered":[...],"executed":[...],"skipped":[],"oracleFailures":[],"negativeControls":{"expected":1,"falsified":0},"scenarios":{"SCN-KI-018":true},"pathWitness":{...},"digests":{...}}`
   line with §4 digests; screenshots for every subtest under the output dir.

**Exact checks (§7.4).** C1 write-set proof: `git -C frontend status
--porcelain` attributable delta is exactly the one new untracked harness file
(the `review-evidence/` runner output is gitignored at leaf level; if the
tree shows it, the leaf records the exact listing and the window agent
confirms the gitignore covers it). C2 `node --check` → 0. C3 `npm run
check` from `frontend/` → exit 0 (no source changed; 118/118). C4 the
official full-build execution `node test/browser/keyword-intelligence-e2e.mjs`
→ exit 0, certificate `executed === required`, `scenarios."SCN-KI-018" ===
true`, zero console errors, zero non-app network (LOCAL_NOW official run at
leaf level; I001 re-runs it as gate `KI-W6-V1`'s UI half — both runs are
recorded; the gate consumes the I001 re-run). C5 the file contains no
credential, token, production ID, or provider body. C6 no real backend,
Neon Auth, or provider URL appears in the network log of the official run
(allowlist: app origin only).

- [ ] P1 Revisions, assignment identity, writable file, baseline digest (`ABSENT`), and predecessor evidence match.
- [ ] P2 Starting repository status and protected dirty changes match the recorded baseline (frontend clean at `c85f93b` plus exactly the accepted S001 ending if committed, else containing exactly the S001 output; root relocation set unchanged; writable file `ABSENT`).
- [ ] T1 Apply every ordered transformation and no other edit to the writable file.
- [ ] V1 Run every LOCAL_NOW check and record its activation witnesses and exact assertions.
- [ ] V2 Prove the attributable workspace changed-file set is exactly the writable file.
- [ ] V3 Prove required local coverage IDs (`W6-U01`–`W6-U08`) equal registered and executed local IDs with zero skips.
- [ ] H1 Return the exact diff, ending digest, commands, outcomes, and residual integration obligations.
- [ ] H2 Confirm no prohibited action, second-file edit, successor work, external mutation, or parent communication occurred.
- [ ] H3 Stop at AWAITING_WINDOW_REVIEW.

### 5.3 `KI-W6-I001` — whole-window integration assessment

```yaml
subwindow_id: KI-W6-I001
type: INTEGRATION_ASSESSMENT (window-agent owned; not delegated)
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-01
assigned_agent: KI-W6-WINDOW-AGENT
predecessors: [KI-W6-S002]
successor_reserved_for: PARENT
writable_file: none
file_operation: none
starting_file_digest: N/A
starting_repository_change_set_digest: d1a974b3248df1764007f77b4d423fc9ff0e85fc7d6add16005058e5156495db
read_only_scope:
  - both leaf files plus S1/S2/S3; both repositories' complete diff; parent artifacts
authorized_actions:
  - independently review both leaf handoffs per sub-window standard section 8
  - execute gates KI-W6-V1 through KI-W6-V4 exactly once each on frozen final inputs
  - execute the KI-W6-I001-M case-union merge
  - append the section 12.4 integration certificate to S3 and set S2 to READY_FOR_PARENT_REVIEW
prohibited_actions:
  - any implementation-file write (a diagnosed defect opens KI-W6-C001+)
  - repeating a passed stateful gate without a documented invalidation
  - claiming parent acceptance or beginning KI-W7
may_start_successor: false
```

**Frozen gates (executed from the stated directories; each exactly once on
the frozen final tree):**

- **`KI-W6-V1` (scenario + matrix + controls):** (a) backend half —
  `ALLOW_DATABASE_TESTS=true npm run test:integration` from `email_scraper/`
  with an isolated `TEST_DATABASE_URL` distinct from production → exit 0;
  the `KI_W6_E2E_EXECUTION_CERTIFICATE` line shows
  `required = registered = executed` over the twelve `W6-E` IDs, zero
  skipped, `oracleFailures: []`, `negativeControls.falsified === 0`.
  (b) UI half — `node test/browser/keyword-intelligence-e2e.mjs` from
  `frontend/` (full production build performed by the script) → exit 0;
  certificate `executed === required` over the eight `W6-U` IDs,
  `scenarios."SCN-KI-018" === true`, zero console errors, zero non-app
  network. A documented sandbox `listen EPERM` failure is rerun under sandbox
  approval, never silently accepted.
- **`KI-W6-V2` (baselines + handler builds):** from `email_scraper/`:
  `node --test test/keyword-intelligence-worker.test.js
  test/keyword-intelligence-selection.test.js
  test/keyword-intelligence-query-mapper.test.js` → 0 failures;
  `npm run check:secrets` → exit 0; `npm test` → 272-test baseline intact
  (272 + 1 new file's counts recorded; zero pre-existing failures); `npm run
  build:lambda` → exit 0. From `frontend/`: `npm run check` → exit 0
  (lint 0 errors/1 pre-existing warning, 118/118, build compiles).
- **`KI-W6-V3` (ceilings):** from the V1 certificate and evidence: exact
  counters equal the frozen values (`pathWitness` byte-equal in both
  certificates); `rss < 1536 MiB`; recorded wall-clock for the database test
  ≤ 900 s and the browser run ≤ 600 s; DEC-KI-024 keyword maxima asserted
  inside the test (19 tasks / 19 calls / 23 keyword objects / result ≤
  32 MiB / draft 200 / final 100 / occurrences 1,000).
- **`KI-W6-V4` (obsolete-runtime negative searches + legacy preservation):**
  from `email_scraper/`: `rg -ni 'python|sqlite|KeywordSearchVolume' src/`
  → zero matches; `rg -n 'output/' src/` → zero matches. From `frontend/`:
  `rg -ni 'python|sqlite|KeywordSearchVolume|output/' app/ lib/ components/
  scripts/` → zero non-comment matches (§0.1 item 7: a match is acceptable
  only on a line whose first non-whitespace token starts a comment);
  `rg -ni 'unpkg\.com|jsdelivr\.net|cdnjs\.' app/ lib/ components/ scripts/`
  → zero matches. Legacy preservation: the `npm test` run in V2 includes the
  legacy run suites green (W1 migration baseline). `git -C
  KeywordSearchVolume status --porcelain` → unchanged (standalone
  read-only).
- **`KI-W6-I001-M` (case-union merge):** the union of the two certificates'
  `executed` sets equals exactly the 20-ID required set with per-LF §4
  digest `8d6d002cdf86a30459c2d140977fec3b72c30a8d1c4d612f512bd7c37ed4c523`;
  zero duplicates, zero unexpected IDs, zero skips; the two `pathWitness`
  objects byte-equal; `negativeControls` totals 5 expected / 0 falsified.
- Assembled write-set proof: `git -C email_scraper status --porcelain` and
  `git -C frontend status --porcelain` list exactly the two planned paths
  (per-LF set digest `bb9f6381cc3b65d08b696fa1f62a2d75759289b4d4f0f44554ca44a2ebf56edc`
  over the two workspace-prefixed paths) and nothing else; the root change
  set equals the 36-line relocation set plus the three subordinate
  artifacts; unrelated files byte-identical.

## 6. Case allocation and control mapping

| Case | Type | File | Scenario/requirement anchor |
|---|---|---|---|
| `W6-E01`–`W6-E12` | integration case | S001 | `SCN-KI-018` non-UI witnesses; `REQ-KI-001`–`022`; `INV-KI-001`–`015`; `D2`/`D3`/`D11`; `DEC-KI-024` counters |
| `W6-U01`–`W6-U08` | browser case | S002 | `SCN-KI-018` UI witnesses; `REQ-KI-006`–`009`, `013`–`014`, `017`–`018`; W5 surface inventory |
| `NC-W6-01` worker bypass | negative control | S001 (`W6-E11.1`) | worker-less completion impossible (W3 oracle) |
| `NC-W6-02` parser bypass | negative control | S001 (`W6-E11.2`) | strict-parser guard (`PAY-KI-006`) |
| `NC-W6-03` snapshot bypass | negative control | S001 (`W6-E11.3`) | `DEC-KI-017` snapshot immutability |
| `NC-W6-04` merge bypass | negative control | S001 (inside `W6-E07`) | terminal-evidence-only aggregation |
| `NC-W6-05` fixture divergence | negative control | S002 | path-derived fixture integrity |

Unmapped parent requirements/decisions/tasks/scenarios: none (every
`KI-W6-T1` item and every `KI-W6-P1`–`P4` prerequisite maps into §5 blocks or
§7; `SCN-KI-018` is wholly allocated; `SCN-KI-001`–`017` remain
parity-complete and are only regression-referenced by V2).

## 7. Correction and re-assessment rules

Corrections are append-only `KI-W6-C001+`, each owning exactly one of the two
planned files, each citing failed evidence, root cause, the governing parent
decision, corrected sub-window, invalidated evidence/gates, and a new
`KI-W6-I002+` assessment. Every correction invalidates all evidence whose
inputs include its file; unaffected costly gates may be reused only with a
recorded deterministic dependency comparison. No correction may touch
application source, the standalone repository, or parent artifacts — a defect
root-caused there is `PARENT_BLOCKED`.

## 8. Leaf dispatch protocol (requester-authorized, mirrors KI-W5 §9)

Every leaf dispatch includes the verbatim block text plus this file's path;
the leaf reads its block before editing; the handoff quotes
`subwindow_id`/`writable_file`/`starting_file_digest` unless the requester
waives the quote form. Leaves execute strictly sequentially: S001 → S002 →
I001. The requester performs all git commits; neither leaves nor the window
agent commit anything.

## 9. Mandatory decomposition-readiness checklist (standard §11)

- [ ] `SW-A01` Parent assignment `ASG-KI-W6-WA-01`, window-agent identity, and delegation authority are exact and current (A5 state 108; `EV-KI-A-047`). Evidence: S3 `EV-KI-W6-S01`.
- [ ] `SW-A02` Parent/sub-window standards plus contract, decision, checklist, and state revisions pinned and verified this session. Evidence: `EV-KI-W6-S01`.
- [ ] `SW-A03` Parent write/read/action/prohibition/stop boundaries copied unexpanded into §1 and every block. Evidence: `EV-KI-W6-S01`.
- [ ] `SW-A04` Repositories, dirty state, and owner-controlled changes inventoried (§2; both nested repos clean; both targets `ABSENT`). Evidence: `EV-KI-W6-S01`.
- [ ] `SW-A05` S1/S2/S3 exist with non-overlapping authorities. Evidence: `EV-KI-W6-S01`.
- [ ] `SW-A06` Strict adjacency enforced; no subagent delegation beyond one leaf at a time. Evidence: §5 blocks, §8.
- [ ] `SW-D01` Every KI-W6 requirement/invariant/decision/task/scenario/case allocated to exact files and assertions (§6). Evidence: `EV-KI-W6-S02`.
- [ ] `SW-D02` No missing parent decision remains (the six §0.1 interpretations are mechanical, each cites its governing decision; none changes product behavior). Evidence: `EV-KI-W6-S02`.
- [ ] `SW-D03` Required changed-file set equals planned initial file set (§3 digests). Evidence: `EV-KI-W6-S01`.
- [ ] `SW-D04` One initial sub-window per file; no multi-file sub-window. Evidence: §5.
- [ ] `SW-D05` Operations, starting digests, anchors, interfaces, preserved behavior, and forbidden edits exact per block. Evidence: §5.
- [ ] `SW-D06` DAG complete, sequential, acyclic (S001 → S002 → I001), edges justified (path-derived fixtures consume S001's frozen generators; I001 consumes both). Evidence: §5.
- [ ] `SW-D07` Cross-file interfaces frozen (API envelopes via W4 contract parsers; certificate shapes in §5.1/§5.2). Evidence: §5.
- [ ] `SW-D08` Intermediate states defined: after S001, the backend E2E exists and both repos otherwise unchanged (S002 depends only on S001's frozen generators, not its execution; safe because fixtures are literal-frozen in S1). Evidence: §5.
- [ ] `SW-D09` Production/test separation: both files are test files; no production file is editable. Evidence: §1.
- [ ] `SW-D10` No rename/generator/formatter/installer can violate the one-file rule (creates only; `node --check` writes nothing; builds emit to gitignored `.next`/`dist`). Evidence: `EV-KI-W6-S02`.
- [ ] `SW-E01`–`SW-E08` Every §7 field present; exact ordered edits; preflight/checks/witnesses/assertions/forbidden outcomes; single-file write-set proof; handoff/stop/successor rules; reporting line; no successor-dependent local acceptance; deferred checks name I001. Evidence: §5 blocks.
- [ ] `SW-V01`–`SW-V10` Coverage allocated to exact files/registrations/witnesses; set-equality and digest checks prescribed (§4, §5.3); five negative controls at the narrowest level; substitute fidelity = §0.1 interpretation 1 (aggregate `pathWitness` parity, recorded); I001 fully authored with zero write authority; frozen gates risk-proportionate at final assessment; correction rules complete; window-agent personal review/assessment; zero-work acceptance impossible (witnesses + certificates); handoff contents exact. Evidence: `EV-KI-W6-S02`.
- [ ] `SW-R01`–`SW-R10` IDs unique; no unresolved placeholders in assignable blocks; write-set lint semantics embedded in C1 checks; remove-one mappings fail readiness; case removal fails acceptance; oracle weakening invalidates; simulated second-file edit/parent communication rejected; window-agent repair requires a corrective sub-window; parent decomposition review precedes first assignment; document lint zero. Evidence: `EV-KI-W6-S02` (self-falsification pass).

## 10. Certificate templates

The §12.1 `SUBWINDOW-DECOMPOSITION-READY` certificate (S3) carries:
`initial_subwindow_ids: [KI-W6-S001, KI-W6-S002]`,
`initial_subwindow_count: 2`, `planned_file_set` = the two §3 paths,
`planned_file_set_digest:
bb9f6381cc3b65d08b696fa1f62a2d75759289b4d4f0f44554ca44a2ebf56edc`,
`unmapped_*` and `unresolved_*` arrays all empty,
`mandatory_authoring_items_checked: 44`, `mandatory_authoring_items_unchecked:
0`, `first_subwindow: KI-W6-S001`, `integration_assessment_id: KI-W6-I001`,
`parent_review_required: true`. Leaf execution certificates (§12.3) and the
window-agent integration certificate (§12.4) follow the sub-window standard
templates verbatim with the KI-W6 IDs and the 20-case required-set digest
`8d6d002cdf86a30459c2d140977fec3b72c30a8d1c4d612f512bd7c37ed4c523`.
