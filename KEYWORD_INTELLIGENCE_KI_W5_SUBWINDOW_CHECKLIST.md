# KI-W5 Sub-Window Checklist (`S1`)

Authoritative decomposition of parent window `KI-W5` (assignment
`ASG-KI-W5-WA-02`, agent `KI-W5-WINDOW-AGENT`) under
`PROJECT_AGNOSTIC_WINDOW_AGENT_SUBWINDOW_AUTHORING_STANDARD.md` (revision
`1766f9107ce7d315877b75d4b0ea2b5521dff1c321e12f890b03787d66196ded`).

Authoring style (requester selection, carried from the accepted `KI-W4`
precedent `EV-KI-W4-S01` §0.4 and reaffirmed by the requester's 2026-08-19
delegation direction behind `CHG-KI-021`): **contract + exact anchors**.
Each leaf block fixes complete signatures, defaults, invariants, verbatim
insertion anchors, exact check commands, and literal expected outcomes.
Leaf subagents apply one bounded, decision-complete block per file and never
require global `S1` context.

---

## 0. Inherited authority and revision pins

### 0.1 Parent package

| Artifact | Path | Pinned revision (A5 state 105) | Observed revision (2026-08-19) |
|---|---|---|---|
| Parent standard | `PROJECT_AGNOSTIC_DECISION_COMPLETE_CHECKLIST_AUTHORING_STANDARD.md` | `3b7a4fd25156e1adfbc92abb835c5f82a0d18c686b1c1150feb202f2d944d2ac` | equal |
| Sub-window standard | `PROJECT_AGNOSTIC_WINDOW_AGENT_SUBWINDOW_AUTHORING_STANDARD.md` | `1766f9107ce7d315877b75d4b0ea2b5521dff1c321e12f890b03787d66196ded` | equal |
| A1 contract | `KEYWORD_INTELLIGENCE_PRODUCT_CONTRACT.md` | `8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c` | equal |
| A3 decision ledger | `KEYWORD_INTELLIGENCE_DECISION_LEDGER.md` | `c2dc635e5aa58f88c1ec465154663d314af68570fd4cbfdfca7b51c393c6f70f` | equal (marker `KI-DL-10`) |
| A4 parent checklist | `KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md` | `324667cbe0d467ecf4f913c93e91087e75192bd463e0c05b033ee418754a362e` | equal (marker `KI-CL-14`) |

- **Delta audit (sub-window standard §0.4):** all five A5 state 105 pins were
  recomputed from disk at authoring time (2026-08-19) and match
  byte-for-byte; no stale-pin condition exists. The A4 revision `KI-CL-14`
  is the `CHG-KI-021` amendment that added the `KI-W5` delegation header
  (A4 lines 2273–2295) and preconditions `KI-W5-P5`/`P6` (A4 lines
  2301–2306). This decomposition binds to the observed revisions above.
- **Assignment provenance:** requester-directed parent performed the A5 CAS
  to state 105 (2026-08-19T11:55:50+05:30) creating `ASG-KI-W5-WA-02` for
  `KI-W5-WINDOW-AGENT` with the three-artifact write scope of §1
  (`EV-KI-A-043`, `CHG-KI-021`). No requester exception or waiver applies.
- **`KI-W5-P2` fixture-server interpretation (recorded for parent
  review):** A4 `KI-W5-P2` requires "W4 API contract accepted and local
  deterministic fixture server is available". The W4 contract acceptance is
  `EV-KI-A-040`. No persisted standalone fixture-server artifact exists in
  either repository; the available deterministic mechanisms are (a) the
  accepted G-R1 pre-hydration fetch-interception precedent
  (`frontend/scripts/g-r1-real-component-browser.mjs:135-181,306`) and (b)
  the accepted W4 in-process server harness
  (`email_scraper/test/keyword-intelligence-api.test.js:679`). This
  decomposition freezes mechanism (a) for the browser gates: `KI-W5-S027`
  stands up the deterministic stand-in by intercepting same-origin
  `/api/keyword-research*` fetches with strict-parser-validated W4-contract
  fixture payloads, plus real unauthenticated route probes for the
  auth/no-store/400 oracles. The parent's decomposition review either
  accepts this reading or directs a correction before any leaf starts.

### 0.2 Authority precedence

A1 contract → parent standard → sub-window standard → A3 decision ledger →
A4 checklist (observed revisions) → A5 active state → this `S1` → `S2` →
`S3` (append-only facts only). `S1`/`S2`/`S3` cannot amend a parent
decision, task, ownership boundary, or authority.

---

## 1. Prohibitions (copied from A5 state 105 and A4 `KI-W5` header, unexpanded)

- Window-agent edits to any implementation file: the window agent writes
  only `KEYWORD_INTELLIGENCE_KI_W5_SUBWINDOW_CHECKLIST.md`,
  `KEYWORD_INTELLIGENCE_KI_W5_SUBWINDOW_STATE.md`, and
  `KEYWORD_INTELLIGENCE_KI_W5_SUBWINDOW_EVIDENCE.md`.
- Parallel leaves: exactly one leaf is assigned and in flight at any time
  (sub-window standard §5.4).
- Direct parent–subagent communication: subagents report only to the window
  agent; the parent communicates only with the window agent (§1.4).
- Backend edits; provider calls; database or AWS operations; iframes;
  runtime CDN loading; unrelated frontend file edits (everything outside
  the 27-path `delegable_implementation_file_set`, including the existing
  modified run-presentation/stages/design-system-runtime frontend files,
  which are read-only per A4 `shared_file_scope`); `package.json`/lockfile
  edits; commits or staging; `KI-W6` or any later window.
- No purge of queues, buckets, prefixes, database rows, or stacks; preserve
  the owner-controlled relocation state of the coordination root and all
  unrelated dirty worktree changes.
- No reuse of window/sub-window IDs; corrections are append-only
  `KI-W5-C001`, `KI-W5-C002`, ….
- Every implementation leaf MUST read the relevant installed Next.js guide
  under `frontend/node_modules/next/dist/docs/` before writing code
  (`frontend/AGENTS.md` mandate; `EV-KI-A-043` restates it).

---

## 2. Baseline (verified 2026-08-19, `EV-KI-W5-S01`)

| Item | Value |
|---|---|
| Frontend `frontend` HEAD | `0dfa1acac50fac3a86d02ec674c6d2bab645832d` ("package install"), `git status --porcelain` empty |
| Backend `email_scraper` HEAD | `fac5bb0f0a4e9c04873c9d338794762d44e35f7f`, clean, read-only for `KI-W5` |
| Root change set | 36 owner-controlled relocation paths, sorted-porcelain per-LF digest `f1d1d8e1ce5db60be7eca760ae2709954a824897ca40fb5e81ac6b36801a9a8b`, preserved unmodified |
| Planned 27-path set digest | `a04dce13038a3d180ddab0c8412890af065e3f5ab5019540c87a5664485320e6` (sorted by unsigned UTF-8 byte order, i.e. `LC_ALL=C sort`, each member + LF; recomputed 2026-08-19, byte-equal to A4 `delegable_file_set_digest`) |
| Required 43-case set digest | `cb8ef6d7cb87b5a451e438d11b0f037c8130f78d0c3e033b1304f78bfa1f6bdb` (§6.1 literal list, `LC_ALL=C sort`, each + LF) |
| Tooling baseline | Node `v24.14.1`; `npx tsc --noEmit` → exit 0; `npm run lint` → exit 0; `npm test` → green at baseline (existing suites); global `WebSocket` available (Node ≥22) |

Starting file digests (before any `KI-W5` leaf):

| Path | Digest | Lines |
|---|---|---|
| `frontend/lib/api-types.ts` | `25d6bd8e9ef371db2b9c1e9937a9991123675f397db5f9fcddae8822f6b6dd7d` | 532 |
| `frontend/lib/api-validation.ts` | `1522c8c46db5a1af33d8723140722ba1a8883a718a07ca5d5397355341829b55` | 1318 |
| `frontend/lib/client-api.ts` | `84f20e6ba5c3ca2bd17147f8ef46235cd9f6460ebcb49f1ec40228d4cd881046` | 52 |
| Read-only references | `frontend/lib/backend-proxy.ts` `20c3d5e5fc8bc587ebc359a63f1d905aa5658b62d7e91e8144cb5196d3a07707` (111 lines); `frontend/lib/auth/route.ts` (32); `frontend/lib/auth/server.ts` (32); `frontend/package.json` `65abf84236945fd89f973b5efc39031d3f9fb1a81d0608dd3647f50546b50d0d` | — |
| All other 24 planned paths | ABSENT (verified by `ls`: `app/keywords/`, `app/api/keyword-research/`, `components/keyword-intelligence/`, `lib/keyword-intelligence-*.ts`, `test/keyword-intelligence-*.test.ts`, `test/browser/` do not exist) | — |

Verified absent symbols in the three MODIFY files (grep, zero matches
each): `KeywordResearch`, `keyword-intelligence`, `parseResearchEnvelope`,
`parseRunHandoffEnvelope`, `validateSeedsInput`, `newClientRequestId`,
`KEYWORD_RESEARCH_ID_PATTERN`, `createKeywordResearch`,
`getKeywordResearch`, `saveKeywordSelection`, `startKeywordResearchRun`.
The only pre-existing `keyword` matches are the CrUX traffic field names
`organic_keyword_count`/`paid_keyword_count`/`featured_snippet_keyword_count`/`local_pack_keyword_count`
(api-types.ts:294-300, api-validation.ts:700-706), which are untouched.

Chart dependencies verified installed and pinned: `chart.js@3.9.1`
(`node_modules/chart.js/package.json`) and `chartjs-chart-treemap@2.0.0`
(peer `chart.js ^3.0.0`, satisfied, deduped). The standalone source loads
both from CDN (`KeywordSearchVolume/dashboard/index.html:10-11`); the port
MUST use local imports only (`KI-W5` prohibition `runtime_CDN`).

---

## 3. Frozen interfaces

Every leaf consumes exactly these frozen forms; no leaf may alter a
signature, default, outcome union, error code, or key set defined here.

### 3.1 Digest formula (parent standard `F-D2`)

Set digest = `sha256` over the byte concatenation of each set member sorted
by unsigned UTF-8 byte order (`LC_ALL=C sort`), each encoded UTF-8 followed
by exactly one LF (`\n`). Applied to: the 27 planned paths (`a04dce13…`),
the 43 required case IDs (`cb8ef6d7…`), each test file's
`required`/`registered`/`executed` arrays in the certificates, and the
assembled changed-file set at `KI-W5-V2`.

### 3.2 Module surface freeze `I-F1`–`I-F5` (frontend lib)

- **I-F1** `frontend/lib/keyword-intelligence-types.ts` exports exactly (all
  `export type`): `KeywordCompetitionLevel` (`"LOW"|"MEDIUM"|"HIGH"`),
  `KeywordMainIntent`
  (`"transactional"|"commercial"|"informational"|"navigational"`),
  `KeywordLane`
  (`"local_discovery"|"brand_competitor"|"store_discovery"|"category_discovery"`),
  `KeywordMarket`, `MonthlyHistoryPoint`, `MarketMetric`, `KeywordFacets`
  (exactly `{audience:string[];category:string[];channel:string[];fit:string[];modifier:string[]}`),
  `KeywordRow`, `ClusterRow`, `VariantGroup`, `ClusterLaneCounts`,
  `ResearchSummary`, `ResearchResult`, `KeywordMetricSnapshot`,
  `SelectionItem`, `SelectionConflictPair`, `SelectionConflict`,
  `ResearchProgressStage`
  (`"queued"|"expansion"|"anchor_screen"|"market_overview"|"finalizing"|"completed"|"failed"`),
  `StageCounts`, `ResearchProgress`, `ResearchSafeError`, `ResearchState`
  (`"queued"|"running"|"completed"|"failed"`), `ResearchView`,
  `KeywordResearchRunResponse` (exactly `{run: RunStatus; statusUrl: string}`
  importing `RunStatus` type-only from `@/lib/api-types`). Field lists
  mirror `DEC-KI-012/013/014/015/019` exactly (A3 lines 248-347, 404-445);
  every object field is required unless the ledger marks it nullable.
- **I-F2** `frontend/lib/keyword-intelligence-validation.ts` exports
  exactly: `KEYWORD_RESEARCH_ID_PATTERN` (`/^kr_[A-Za-z0-9_-]{24}$/u`),
  `validKeywordResearchId(id: string): boolean`,
  `CLIENT_REQUEST_ID_PATTERN` (`/^[A-Za-z0-9_-]{16,80}$/u`),
  `newClientRequestId(): string` (exactly
  `crypto.randomUUID().replace(/-/g, "")`; 32 hex chars; matches the
  pattern), `validateSeedsInput(input: unknown): {ok: true; seeds:
  string[]} | {ok: false; error: string}` (input must be an object with
  exactly the key `seeds`, an array of 1..5 strings, each
  NFKC-trim-collapsed, 1..100 code points, nonempty after trim; duplicates
  after normalization are rejected), `parseResearchEnvelope(payload:
  unknown): ResearchView` (payload is exactly `{research}`; unknown wrapper
  keys throw), `parseResearchView(payload: unknown): ResearchView`,
  `parseRunHandoffEnvelope(payload: unknown): KeywordResearchRunResponse`
  (payload exactly `{run,statusUrl}`; `run` parsed by importing the existing
  `parseRunStatus` from `./api-validation`). Parser strictness: every object
  rejects unknown keys; exact key sets per `DEC-KI-019`/`DEC-KI-012`;
  `monthlyHistory` length 15..102 with `month` 1..12 and nonnegative safe
  integer `searchVolume`; integer fields are safe integers with ledger
  bounds (`selectionRevision >= 1` post-publication, scores 0..100,
  `expectedRevision >= 1`); enums exact; dates ISO-8601 strings or `null`
  with `createdAt`/`updatedAt` non-null; `result` non-null only when
  `state === "completed"`; `selection` 0..200 items; failure throws
  `ApiPayloadError` imported (runtime) from `./api-validation`. The module's
  only imports are type-only from `./keyword-intelligence-types` and
  `@/lib/api-types`, plus the runtime imports `ApiPayloadError` and
  `parseRunStatus` from `./api-validation` (relative paths so Node test
  files can import this module).
- **I-F3** `frontend/lib/api-types.ts` additive edit is exactly one block
  appended at end of file (after current line 532, preceded by one blank
  line): the comment line
  `// Keyword intelligence re-exports (KI-W5; additive only).` followed by
  one `export type { … } from "./keyword-intelligence-types";` statement
  listing exactly the 24 I-F1 export names in alphabetical order. No other
  line changes.
- **I-F4** `frontend/lib/api-validation.ts` additive edit is exactly one
  block appended at end of file (after current line 1318, preceded by one
  blank line): the comment line
  `// Keyword intelligence parsers (KI-W5; additive only).` followed by
  `export { CLIENT_REQUEST_ID_PATTERN, KEYWORD_RESEARCH_ID_PATTERN, newClientRequestId, parseResearchEnvelope, parseResearchView, parseRunHandoffEnvelope, validKeywordResearchId, validateSeedsInput } from "./keyword-intelligence-validation";`.
  No other line changes.
- **I-F5** `frontend/lib/client-api.ts` additive edit appends exactly four
  functions at end of file (one blank line before the block) plus two
  import lines placed directly after the existing line-2 import: the
  runtime import
  `import { parseResearchEnvelope, parseRunHandoffEnvelope } from "./keyword-intelligence-validation";`
  and the type-only import
  `import type { KeywordResearchRunResponse, ResearchView, SelectionItem } from "./keyword-intelligence-types";`.
  The functions (all `export async function`):
  `createKeywordResearch(seeds: string[]): Promise<ResearchView>` — POST
  `/api/keyword-research` with body `JSON.stringify({ seeds })`;
  `getKeywordResearch(researchId: string): Promise<ResearchView>` — GET
  `/api/keyword-research/${encodeURIComponent(researchId)}`;
  `saveKeywordSelection(researchId: string, expectedRevision: number, items: SelectionItem[]): Promise<ResearchView>`
  — PUT `/api/keyword-research/${encodeURIComponent(researchId)}/selection`
  with body `JSON.stringify({ expectedRevision, items })`;
  `startKeywordResearchRun(researchId: string, expectedSelectionRevision: number, clientRequestId: string): Promise<KeywordResearchRunResponse>`
  — POST `/api/keyword-research/${encodeURIComponent(researchId)}/runs`
  with body
  `JSON.stringify({ expectedSelectionRevision, clientRequestId })`. All
  four call `apiRequest<T>(url, { method, body }, parseFn)` with `parseFn` =
  `parseResearchEnvelope` (JSON routes) or `parseRunHandoffEnvelope` (runs
  route). No other line changes.

### 3.3 Route contracts `I-F6`–`I-F10`

All five route files set `export const runtime = "nodejs";` and
`export const dynamic = "force-dynamic";`, import `jsonError`/`proxyBackend`
from `@/lib/backend-proxy` and `authenticatedRoute` from `@/lib/auth/route`,
and follow `frontend/app/api/runs/route.ts` and
`frontend/app/api/runs/[runId]/route.ts` patterns (each route leaf first
reads the installed guides
`node_modules/next/dist/docs/01-app/03-api-reference/03-file-conventions/route.md`
and `.../dynamic-routes.md`). Errors are always the existing `jsonError`
envelopes with `Cache-Control: no-store`.

- **I-F6** `app/api/keyword-research/route.ts` exports `POST` only. Guard
  order: Content-Type must start `application/json` (else 415
  `UNSUPPORTED_CONTENT_TYPE`); body ≤ 32768 bytes (else 413
  `REQUEST_TOO_LARGE`); must parse as JSON (else 400 `INVALID_JSON`); the
  parsed body must pass `validateSeedsInput` (else 400
  `KEYWORD_RESEARCH_INPUT_INVALID`, message "One to five research seed
  phrases are required."); then `auth = await authenticatedRoute()` (401
  passthrough of `auth.response`); then `proxyBackend({ path:
  "/api/keyword-research", method: "POST", body:
  JSON.stringify({ seeds }), timeoutMs: 15_000, userId: auth.userId })` —
  `seeds` is exactly the validated array.
- **I-F7** `app/api/keyword-research/[researchId]/route.ts` exports `GET`
  with signature
  `GET(_request: Request, context: RouteContext<"/api/keyword-research/[researchId]">)`;
  `const { researchId } = await context.params;` guard
  `validKeywordResearchId(researchId)` else 400 `INVALID_RESEARCH_ID`
  ("The research ID is invalid."); proxy GET
  `/api/keyword-research/${encodeURIComponent(researchId)}` timeout 10_000.
- **I-F8** `app/api/keyword-research/[researchId]/selection/route.ts`
  exports `PUT` with the same param guard; Content-Type/JSON checks as I-F6;
  body ≤ 262144 bytes (413); the body must be an object with exactly the
  keys `expectedRevision` (safe integer ≥ 1) and `items` (array with length
  ≤ 200) else 400 `KEYWORD_SELECTION_INPUT_INVALID` ("The selection payload
  is invalid."); forward the original body string verbatim via
  `proxyBackend` PUT to
  `/api/keyword-research/${encodeURIComponent(researchId)}/selection`
  timeout 15_000.
- **I-F9** `app/api/keyword-research/[researchId]/runs/route.ts` exports
  `POST` with the same param guard; Content-Type/JSON checks; body ≤ 4096
  bytes; the body must be an object with exactly `expectedSelectionRevision`
  (safe integer ≥ 1) and `clientRequestId` (string matching
  `CLIENT_REQUEST_ID_PATTERN`) else 400 `KEYWORD_RUN_INPUT_INVALID` ("The
  research handoff payload is invalid."); forward verbatim via
  `proxyBackend` POST to
  `/api/keyword-research/${encodeURIComponent(researchId)}/runs` timeout
  15_000.
- **I-F10** `app/api/keyword-research/[researchId]/export.csv/route.ts`
  exports `GET` with the same param guard. It does NOT use `proxyBackend`
  (which JSON-parses every response; `backend-proxy.ts:74-84` would corrupt
  CSV). It performs a route-local backend fetch with the same environment
  contract: `BACKEND_API_BASE_URL` validated exactly as
  `backend-proxy.ts:28-38` (else 500 `FRONTEND_CONFIGURATION_ERROR`);
  headers `Accept: text/csv,application/json`,
  `Authorization: Bearer ${BACKEND_API_TOKEN}` when set, `X-User-Id` from
  `authenticatedRoute`; `AbortController` timeout 30_000 → 504
  `BACKEND_TIMEOUT`; network failure → 502 `BACKEND_UNAVAILABLE`. Query
  forwarding: only the allowlisted parameters, each at most once except
  `flag` (repeatable ≤ 20), validated exactly per `DEC-KI-019` (A3 lines
  420-425): `market` ∈ `all|US|GB|CA|AU|NZ|DE|FR|IN|AE`; `seed` ≤ 100;
  `clusterId`; `intent` nonempty ≤ 40; `lane` one of the four lanes;
  `category|audience|channel` nonempty ≤ 40; `minVolume` integer
  0..2147483647; `minOpportunity` integer 0..100; `recommended` ∈
  `true|false`; `flag` nonempty ≤ 40; `search` ≤ 160; unknown keys,
  duplicates of single-value keys, or bound violations → 400
  `INVALID_QUERY_PARAMETERS` ("One or more export query parameters are
  invalid."). On backend success (2xx) return `new Response(responseText, {
  status: 200, headers: { "Content-Type": <backend value or
  "text/csv; charset=utf-8">, "Content-Disposition": <backend value>,
  "Cache-Control": "no-store" } })`; on non-2xx attempt `JSON.parse` of the
  body and re-emit `Response.json(payload, { status: <backend status>,
  headers: { "Cache-Control": "no-store" } })`, unparsable → 502
  `BACKEND_INVALID_RESPONSE`.

### 3.4 Page contracts `I-F11`

- `app/keywords/page.tsx`: server component; `export const dynamic =
  "force-dynamic"`; `export const metadata: Metadata = { title: "Keyword
  research" }`; renders the app shell pattern of `app/runs/page.tsx`
  (`main.app-canvas` + `div.shell` + eyebrow/title/lede header row) with
  `ResearchForm` as the workspace body. No server-side session redirect
  (matches the existing app pattern; the client handles 401 with a sign-in
  CTA). `ResearchForm` is rendered without `onCreated`, so its built-in
  default navigates to `/keywords/${view.id}` (I-F14).
- `app/keywords/[researchId]/page.tsx`: server component;
  `export const dynamic = "force-dynamic"`; `export const metadata:
  Metadata = { title: "Keyword research dashboard" }`; typed via
  `PageProps<"/keywords/[researchId]">` per the installed
  `.../file-conventions/page.md` and `.../dynamic-routes.md`;
  `const { researchId } = await params;` renders the same shell with
  `<ResearchDashboard researchId={researchId} />`. The page does not
  validate the ID pattern (the client surfaces the API 400/404 safely).

### 3.5 View-model freeze `I-F12` (pure functions, no React)

`frontend/lib/keyword-intelligence-view-model.ts` exports exactly:

- `KEYWORD_INTELLIGENCE_SURFACE_INVENTORY: readonly string[]` — the literal
  frozen set (I-F15).
- `nextPollDelay(previousMs: number): number` — ladder 2000 → 3000 → 4500 →
  6750 → 10000 → 10000 (×1.5 capped at 10000; input < 2000 returns 2000).
- `isTerminalResearchState(state: ResearchState): boolean` — true for
  `completed|failed`.
- Projection: `activeRows(result: ResearchResult): KeywordRow[]` (rows with
  `mergedInto === null`; port of the standalone `activeRows`),
  `distinctKeywordRows(rows: KeywordRow[]): KeywordRow[]` (port),
  `projectMarketRow(row: KeywordRow, marketCode: string): KeywordRow` (port
  of index.html:962 — market metrics replace the top-level metric fields;
  absent market → null metrics), `marketKeywordKey(row: KeywordRow,
  marketCode: string): string` (port), `cumulativeVolume(rows:
  KeywordRow[]): number` (port), `currentSummary(result: ResearchResult,
  marketCode: string)` and `currentClusterMetric(cluster: ClusterRow,
  marketCode: string)` (ports of the standalone functions with market
  projection applied).
- Filtering/sorting: `KeywordFilterState` type (exactly `{ search: string;
  market: string; seed: string; clusterId: string; intent: string; lane:
  string; category: string; audience: string; channel: string; minVolume:
  number; minOpportunity: number; recommended: "" | "true" | "false";
  flags: string[]; sortKey: string; sortDir: "asc" | "desc"; page: number;
  pageSize: number }`), `emptyKeywordFilterState(): KeywordFilterState`
  (defaults `market: "all"`, `pageSize: 25`, `page: 1`, `sortKey`/`sortDir`
  = the standalone default sort), `getFiltered(rows: KeywordRow[], filter:
  KeywordFilterState): KeywordRow[]` (port of index.html:996 — same
  predicates and order), `sortKeywordRows(rows: KeywordRow[], sortKey:
  string, sortDir: "asc" | "desc"): KeywordRow[]` (port of the standalone
  comparator set with null-last rules), `paginate(rows: KeywordRow[], page:
  number, pageSize: number): KeywordRow[]` (bounds-clamped slice),
  `filterOptionSources(rows: KeywordRow[])` (port of
  `populateFilterOptions` outputs: distinct
  seeds/clusters/intents/lanes/categories/audiences/channels/flags).
- Aggregation: `aggregateByCluster(rows: KeywordRow[])` (port),
  `adjustedVolume(rows: KeywordRow[]): number` (port), `median(values:
  number[]): number`, `metricFingerprint(rows: KeywordRow[]): string` (port
  — deterministic join of item IDs), `discoveryLane(row: KeywordRow):
  KeywordLane` (port), `laneLabel(lane: KeywordLane): string` (port).
- Formatting: `fmtNum(n: number): string`, `fmtCpc(n: number | null):
  string`, `fmtPct(n: number): string`, `fmtSlope(n: number): string`
  (ports of the standalone formatters, identical outputs).
- Selection: `selectionDraftFromView(view: ResearchView): SelectionItem[]`,
  `toggleSelectedItem(draft: SelectionItem[], row: KeywordRow):
  SelectionItem[]` (adds at the DEC-KI-013 candidate-order position or
  removes; adding beyond the 200 cap is a no-op returning the input),
  `removeSelectedItem(draft: SelectionItem[], itemId: string):
  SelectionItem[]`, `editSelectedItemText(draft: SelectionItem[], itemId:
  string, text: string): { draft: SelectionItem[]; reclassified: { lane:
  KeywordLane; facets: KeywordFacets } }` (the edited text is reclassified
  by the same pure classifier port behind `discoveryLane`), 
  `addManualSelectedItem(draft: SelectionItem[], text: string, itemId:
  string, firstSeed: string): SelectionItem[]` (sourceKind "manual", null
  source/metrics, `firstSeed` as the single source seed),
  `selectionOverLimit(draft: SelectionItem[]): boolean` (> 100),
  `canFinalizeSelection(view: ResearchView, draft: SelectionItem[]):
  { ok: boolean; reason: "" | "not_completed" | "empty" | "over_limit" |
  "conflicts" }` (ok requires completed state, 1..100 items, zero
  `selectionConflicts`).
- Export: `buildExportQuery(filter: KeywordFilterState): URLSearchParams`
  (mirrors the `DEC-KI-019` parameter names/bounds; omits empty defaults;
  repeated `flag` entries ≤ 20), `EXPORT_CSV_COLUMNS: readonly string[]`
  (the W2 export column list mirrored from the accepted
  `email_scraper/src/keyword-intelligence/export.js` header order — the
  leaf reads that file read-only and copies the literal column names).
- Theme: `KEYWORD_THEME_STORAGE_KEY` = exactly `"ki-dashboard-theme"`,
  `nextTheme(current: "light" | "dark"): "light" | "dark"`.
- View state: `DashboardViewPhase = "loading" | "ready" | "error" |
  "empty"` and `dashboardPhase(view: ResearchView | null, error: unknown):
  DashboardViewPhase` (empty when completed with zero active rows).

Runtime imports allowed: none from React; type-only from
`./keyword-intelligence-types`; no `@/` runtime imports (Node-testable).

### 3.6 CSS module freeze `I-F13`

`frontend/components/keyword-intelligence/keyword-dashboard.module.css`
ports the standalone `<style>` block (index.html:12-467) into a CSS module:
class names camelCased (e.g. `tableScroll`, `chartWrap`,
`clusterSceneLayout`, `seedChipField`, `emptyState`, `errorBanner`,
`keywordDialog`, `selectionStatus`); the `:root` custom properties become
locals on a root class `.kiDashboard` with identical literal values; the
`[data-theme="dark"]` overrides become
`.kiDashboard[data-ki-theme="dark"]` (the wrapper element carries
`data-ki-theme`; the document root and the existing app design system are
never touched). No `id=` selectors; no selectors leaking outside the module
other than the scoped attribute selector above; media queries and
breakpoints preserved. No `!important` additions, no global element
resets, no `body`/`html`/`:root` selectors.

### 3.7 Component contracts `I-F14`

All components are `"use client"` under
`frontend/components/keyword-intelligence/`, import the CSS module as
`import styles from "./keyword-dashboard.module.css"`, and never read
`localStorage` except the theme key (I-F12). Props:

- `ResearchForm({ onCreated }: { onCreated?: (view: ResearchView) => void })`
  — seeds chip field (1..5 seeds, `validateSeedsInput` before submit),
  submit disabled while in flight; on success calls `onCreated` exactly
  once; when `onCreated` is undefined the built-in default is
  `router.push(`/keywords/${view.id}`)`; on 401 `ApiRequestError` renders
  the sign-in CTA linking `/sign-in`; on other errors renders
  `errorMessage` safely.
- `ResearchStatus({ researchId, initialView, onTerminal }: { researchId:
  string; initialView: ResearchView; onTerminal: (view: ResearchView) =>
  void })` — renders progress stage/counts surfaces; polls
  `getKeywordResearch` with exactly one pending `setTimeout` chain using
  `nextPollDelay`; stops at `isTerminalResearchState` then calls
  `onTerminal` exactly once; retry button performs GET only; unmount clears
  the pending timeout.
- `FilterBar({ filter, options, onChange, onReset }: { filter:
  KeywordFilterState; options: ReturnType<typeof filterOptionSources>;
  onChange: (patch: Partial<KeywordFilterState>) => void; onReset: () =>
  void })`.
- `SummaryCards({ result, marketCode }: { result: ResearchResult;
  marketCode: string })` — cards, collection funnel, discovery segments,
  overlap warnings (ports of `renderCards`, `renderFunnel`,
  `renderDiscoverySegments`, `renderOverlapWarnings`).
- `KeywordTable({ rows, filter, selectionItemIds, onToggleRow, onEditItem }:
  { rows: KeywordRow[]; filter: KeywordFilterState; selectionItemIds:
  ReadonlySet<string>; onToggleRow: (row: KeywordRow) => void; onEditItem:
  (itemId: string) => void })` — sorted/paginated table with page controls
  (ports of `renderTable`, `buildTableHead`, `compareRows`,
  `updateSortArrows`, `trendCell`, `flagsCell`); React keys are `itemId`
  values, never keyword text or row index.
- `SelectionReview({ view, draft, conflicts, saving, staleConflict,
  onSave, onFinalize, finalizeState }: { view: ResearchView; draft:
  SelectionItem[]; conflicts: SelectionConflict[]; saving: boolean;
  staleConflict: boolean; onSave: () => void; onFinalize: () => void;
  finalizeState: "idle" | "handing-off" })` — ordered selected list, manual
  add, edit dialog, remove, over-100 guard, conflict review blocking
  finalize, save button, finalize button (ports of `renderResearchPhrases`,
  `renderDecisionPanels` (index.html:1319), and the keyword-dialog flows).
- `ChartPanels({ result, marketCode, filter, rows }: { result:
  ResearchResult; marketCode: string; filter: KeywordFilterState; rows:
  KeywordRow[] })` — the eleven charts (I-F17).
- `ClusterLandscape({ clusters, selectedClusterId, onSelect }: { clusters:
  ClusterRow[]; selectedClusterId: string | null; onSelect: (clusterId:
  string | null) => void })` — canvas landscape (ports of `renderClusters`
  (index.html:2585) scene layout/pills/legend/inspector plus
  `drawClusterLandscape`: isometric projection, depth order, radius/color
  scales, drag, pinch (pointer events keyed by pointerId), wheel zoom,
  double-click reset, zoom buttons, hit test, tooltip, DPR-aware sizing).
- `ResearchDashboard({ researchId }: { researchId: string })` — the
  orchestrator: owns view/draft/filter/theme state; initial
  `getKeywordResearch`; `ResearchStatus` until terminal; failed → safe
  error surface with retry (GET only); completed → composes FilterBar,
  SummaryCards, KeywordTable, SelectionReview, ChartPanels,
  ClusterLandscape; save via `saveKeywordSelection(researchId,
  view.selectionRevision, draft)` applying the response only after backend
  success; 409 `KEYWORD_SELECTION_REVISION_CONFLICT` sets a stale-conflict
  surface requiring explicit reload before further saves; finalize via
  `startKeywordResearchRun` with a per-click retained `clientRequestId`
  (duplicate click reuses it), then navigates to the returned `statusUrl`;
  export anchor `/api/keyword-research/${researchId}/export.csv?${buildExportQuery(filter)}`;
  market switch projects metrics only (selection invariant); theme toggle
  writes only the I-F12 key; each composed surface carries
  `data-surface="<inventory id>"`.

### 3.8 Surface inventory freeze `I-F15`

`KEYWORD_INTELLIGENCE_SURFACE_INVENTORY` is exactly (order fixed, 21
entries):

```
surface:research-form, surface:research-status, surface:filter-bar,
surface:summary-cards, surface:keyword-table, surface:selection-review,
surface:chart-panels, surface:cluster-landscape, surface:research-dashboard,
chart:top-keywords, chart:cluster-volume, chart:bubble, chart:scatter,
chart:intent, chart:recommended, chart:seeds, chart:histogram, chart:treemap,
chart:flags, chart:history, landscape:cluster-scene
```

Recorded port note (for parent review): the standalone DOM contains
canvases for nine charts (chartTopKeywords, chartBubble, chartScatter,
chartIntent, chartRecommended, chartSeeds, chartHistogram, chartFlags,
chartHistory); `chartClusterVolume` (index.html:1459) and `chartTreemap`
(index.html:1826) target elements absent from the static DOM. A4
`KI-W5-T3` requires "local Chart.js/treemap charts" and the exact pinned
`chartjs-chart-treemap@2.0.0` dependency, so the port materializes both on
component-owned canvases with data/options ported verbatim from those
functions. No other chart is invented.

### 3.9 Poll and chart lifecycle `I-F16`–`I-F17`

- **I-F16** exactly one outstanding poll timer per mounted dashboard; delay
  sequence per `nextPollDelay`; zero polls after terminal or unmount; tab
  close drops timers only (no mutation beyond GET).
- **I-F17** `ChartPanels` imports `Chart` and registerables from
  `chart.js` and the treemap controller/elements from
  `chartjs-chart-treemap` locally; registers once at module scope; creates
  exactly one `Chart` instance per canvas ref; destroys every instance on
  dataset change and on unmount (`chart.destroy()`); the landscape uses
  the raw canvas 2D context (no Chart instance). No `loadScript`/CDN/
  fallback fetching (the standalone `SCRIPT_CANDIDATES`/`loadFirst` path is
  not ported).

### 3.10 Certificate formats `I-F18`

Each of `test/keyword-intelligence-api.test.ts`,
`test/keyword-intelligence-components.test.ts`, and
`test/keyword-intelligence-inventory.test.ts` emits exactly one TAP
diagnostic line `KI_W5_EXECUTION_CERTIFICATE=` followed by compact JSON
`{"file":<basename>,"required":[...],"registered":[...],"executed":[...],"skipped":[],"oracleFailures":[],"requiredDigest":"...","registeredDigest":"...","executedDigest":"..."}`
where each digest is the §3.1 set digest of the respective array.
`test/browser/keyword-intelligence-dashboard.mjs` emits exactly one
`KI_W5_BROWSER_CERTIFICATE=` line with the same schema over its B/R IDs
plus `"scenarios":{"SCN-KI-016":<bool>,"SCN-KI-017":<bool>}`.

---

## 4. Dependency graph (strictly sequential execution, §5.4)

| # | ID | File | Operation | Interface predecessors (named outputs) |
|---|---|---|---|---|
| 1 | `KI-W5-S001` | `frontend/lib/keyword-intelligence-types.ts` | CREATE | none |
| 2 | `KI-W5-S002` | `frontend/lib/keyword-intelligence-validation.ts` | CREATE | I-F1 |
| 3 | `KI-W5-S003` | `frontend/lib/api-types.ts` | MODIFY (additive) | I-F1 |
| 4 | `KI-W5-S004` | `frontend/lib/api-validation.ts` | MODIFY (additive) | I-F2 |
| 5 | `KI-W5-S005` | `frontend/lib/client-api.ts` | MODIFY (additive) | I-F2, I-F5 |
| 6 | `KI-W5-S006` | `frontend/lib/keyword-intelligence-view-model.ts` | CREATE | I-F1 |
| 7 | `KI-W5-S007` | `frontend/components/keyword-intelligence/keyword-dashboard.module.css` | CREATE | none (ports index.html:12-467) |
| 8 | `KI-W5-S008` | `frontend/components/keyword-intelligence/research-form.tsx` | CREATE | I-F5, I-F12, I-F13 |
| 9 | `KI-W5-S009` | `frontend/components/keyword-intelligence/research-status.tsx` | CREATE | I-F5, I-F12, I-F16 |
| 10 | `KI-W5-S010` | `frontend/components/keyword-intelligence/filter-bar.tsx` | CREATE | I-F12, I-F13 |
| 11 | `KI-W5-S011` | `frontend/components/keyword-intelligence/summary-cards.tsx` | CREATE | I-F12, I-F13 |
| 12 | `KI-W5-S012` | `frontend/components/keyword-intelligence/keyword-table.tsx` | CREATE | I-F12, I-F13 |
| 13 | `KI-W5-S013` | `frontend/components/keyword-intelligence/selection-review.tsx` | CREATE | I-F5, I-F12, I-F13 |
| 14 | `KI-W5-S014` | `frontend/components/keyword-intelligence/chart-panels.tsx` | CREATE | I-F12, I-F13, I-F17 |
| 15 | `KI-W5-S015` | `frontend/components/keyword-intelligence/cluster-landscape.tsx` | CREATE | I-F12, I-F13 |
| 16 | `KI-W5-S016` | `frontend/components/keyword-intelligence/research-dashboard.tsx` | CREATE | I-F5, I-F12, S008–S015 |
| 17 | `KI-W5-S017` | `frontend/app/api/keyword-research/route.ts` | CREATE | I-F2, I-F6 |
| 18 | `KI-W5-S018` | `frontend/app/api/keyword-research/[researchId]/route.ts` | CREATE | I-F2, I-F7 |
| 19 | `KI-W5-S019` | `frontend/app/api/keyword-research/[researchId]/selection/route.ts` | CREATE | I-F2, I-F8 |
| 20 | `KI-W5-S020` | `frontend/app/api/keyword-research/[researchId]/runs/route.ts` | CREATE | I-F2, I-F9 |
| 21 | `KI-W5-S021` | `frontend/app/api/keyword-research/[researchId]/export.csv/route.ts` | CREATE | I-F2, I-F10 |
| 22 | `KI-W5-S022` | `frontend/app/keywords/page.tsx` | CREATE | S008, I-F11 |
| 23 | `KI-W5-S023` | `frontend/app/keywords/[researchId]/page.tsx` | CREATE | S016, I-F11 |
| 24 | `KI-W5-S024` | `frontend/test/keyword-intelligence-api.test.ts` | CREATE | I-F2, I-F12 |
| 25 | `KI-W5-S025` | `frontend/test/keyword-intelligence-components.test.ts` | CREATE | I-F12 |
| 26 | `KI-W5-S026` | `frontend/test/keyword-intelligence-inventory.test.ts` | CREATE | I-F1, I-F2, I-F12, I-F15 |
| 27 | `KI-W5-S027` | `frontend/test/browser/keyword-intelligence-dashboard.mjs` | CREATE | all prior leaves |
| 28 | `KI-W5-I001` | (integration assessment, no file write) | ASSESS | all 27 leaves |

Execution is strictly sequential `S001 → S027` then `I001` regardless of
interface independence: `predecessors` records the true interface
dependencies; the immediately preceding leaf is always also a predecessor
under §5.4. `may_start_successor` is `false` for every leaf; only the
window agent assigns the next leaf after an `ACCEPTED_FOR_INTEGRATION`
review.

### 4.1 Intermediate states (§6.1)

| State | Exact condition | Permitted checks | Expected temporary failures | Resolver | Prohibitions |
|---|---|---|---|---|---|
| IS-1 (after S001–S005) | lib contracts exist; no route/component consumer | C1–C5 (common leaf checks) | none (tsc/lint/`npm test` must pass) | S006+ consume | no consumer edits inside these leaves |
| IS-2 (after S006–S007) | view model + CSS module exist, unreferenced | C1–C5 plus the S006 import-smoke | none | S008+ | no component edits |
| IS-3 (after S008–S016) | all components exist; routes/pages absent | C1–C5 | none | S017+ | no route/page/test edits |
| IS-4 (after S017–S023) | routes+pages exist; zero tests reference keyword paths | C1–C5; `npm run build` is NOT run at leaf level | none | S024+ | no test edits; no build runs |
| IS-5 (after S024–S026) | node tests green with certificates | one `node --experimental-strip-types --test test/keyword-intelligence-*.test.ts` run per test leaf | none | S027, I001 | browser script not yet executed |
| IS-6 (after S027) | browser harness authored, not executed | `node --check test/browser/keyword-intelligence-dashboard.mjs` | none | I001 gates V1–V4 | no Next production build before I001 |

Common leaf checks (`LOCAL_NOW`, executed from `frontend/`): C1
`git status --porcelain` lists exactly the cumulative planned set (accepted
leaf endings plus this leaf's writable file, nothing else within
`frontend/`; root relocation set unchanged); C2 `npx tsc --noEmit` → exit
0; C3 `npm run lint` → exit 0; C4 `npm test` → exit 0 with the baseline
suites green (keyword suites appear from S024 on); C5 the block-specific
grep/import smokes. No `next build`, no `next dev`, no browser, and no
backend process at leaf level — those run only inside `KI-W5-I001`.

---

## 5. File sub-window blocks

Semantics common to every block: the recorded
`starting_repository_change_set_digest` is the authoring-time root set;
leaf preflight (P2) instead proves the frontend repository clean at HEAD
`0dfa1aca…` (or, for later leaves, containing exactly the accepted
predecessor endings) and the root relocation set unchanged. Every leaf
reads the installed Next guides named in its block before editing. Every
leaf reports the exact §7.5 handoff and stops at `AWAITING_WINDOW_REVIEW`.
The prohibited_actions list of every block below is exactly the list of
`KI-W5-S001` (edit any second file; edit the three coordination artifacts;
start the successor or any later sub-window; communicate with the parent
agent; mutate external state — providers, AWS, databases, queues, buckets;
weaken any existing test, fixture, or oracle) and is not repeated per
block.

### 5.1 `KI-W5-S001` — keyword intelligence types

```yaml
subwindow_id: KI-W5-S001
type: FILE
parent_window_id: KI-W5
parent_assignment_id: ASG-KI-W5-WA-02
assigned_agent: UNASSIGNED
predecessors: []
successor_reserved_for: WINDOW-AGENT
writable_file: frontend/lib/keyword-intelligence-types.ts
file_operation: CREATE
starting_file_digest: ABSENT
starting_repository_change_set_digest: f1d1d8e1ce5db60be7eca760ae2709954a824897ca40fb5e81ac6b36801a9a8b
read_only_scope:
  - KEYWORD_INTELLIGENCE_DECISION_LEDGER.md lines 248-347 (DEC-KI-012/013/014/015), 404-445 (DEC-KI-019)
  - frontend/lib/api-types.ts (RunStatus import shape)
authorized_actions:
  - read every file listed in read_only_scope
  - create exactly writable_file with the I-F1 export surface
  - run the exact LOCAL_NOW checks of this block
  - report the exact handoff to the window agent
prohibited_actions:
  - edit any second file
  - edit KEYWORD_INTELLIGENCE_KI_W5_SUBWINDOW_CHECKLIST.md, KEYWORD_INTELLIGENCE_KI_W5_SUBWINDOW_STATE.md, or KEYWORD_INTELLIGENCE_KI_W5_SUBWINDOW_EVIDENCE.md
  - start the successor or any later sub-window
  - communicate with the parent agent
  - mutate external state (providers, AWS, databases, queues, buckets)
  - weaken any existing test, fixture, or oracle
may_start_successor: false
```

Mechanical trace: `REQ-KI-005/006/007/008/009/018`; `DEC-KI-012/013/014/015/019`;
`KI-W5-T1` interface/schema item; consumed by S002–S006, S008–S016,
S024–S026; exercised by `W5-A05/A06`, `W5-I01`.

Exact transformation:

1. Create `frontend/lib/keyword-intelligence-types.ts` containing exactly
   the I-F1 export surface. Every field name, nullability marker, enum
   member, and bound is transcribed from `DEC-KI-012/013/014/015/019`
   (A3 lines 248-347, 404-445); `marketMetrics` is the exact nine-key map
   `US|GB|CA|AU|NZ|DE|FR|IN|AE → MarketMetric | null`; `KeywordFacets` has
   exactly the five arrays; `KeywordMetricSnapshot` contains exactly the
   `KeywordRow` fields other than `itemId, keyword, seed, sourceSeeds,
   lane, facets`; `SelectionItem` is exactly the `DEC-KI-014` key list;
   `ResearchView` is exactly the 15-key `DEC-KI-019` list.
2. The only import is `import type { RunStatus } from "@/lib/api-types";`
   (type-only; used by `KeywordResearchRunResponse`).
3. No runtime code, no parsers, no defaults beyond type declarations.

Exact checks (`LOCAL_NOW`, from `frontend/`):

- C1 `git status --porcelain` → `?? lib/keyword-intelligence-types.ts`
  only (within `frontend/`; root relocation set unchanged).
- C2 `npx tsc --noEmit` → exit 0.
- C3 `npm run lint` → exit 0.
- C4 `npm test` → baseline green (no behavior change).
- C5 `grep -c "^export type " lib/keyword-intelligence-types.ts` →
  exactly `24` (the I-F1 count).
- Coverage: zero local case IDs (executed in S024/S026).
- Expected workspace write set: `A frontend/lib/keyword-intelligence-types.ts`
  only.

Completion checklist (sub-window standard §7.5):

- [ ] P1 Revisions, assignment identity, writable file, baseline digest, and predecessor evidence match.
- [ ] P2 Starting repository status and protected dirty changes match the recorded baseline.
- [ ] T1 Apply every ordered transformation and no other edit to the writable file.
- [ ] V1 Run every LOCAL_NOW check and record its activation witnesses and exact assertions.
- [ ] V2 Prove the attributable workspace changed-file set is exactly the writable file.
- [ ] V3 Prove required local coverage IDs equal registered and executed local IDs with zero skips.
- [ ] H1 Return the exact diff, ending digest, commands, outcomes, and residual integration obligations.
- [ ] H2 Confirm no prohibited action, second-file edit, successor work, external mutation, or parent communication occurred.
- [ ] H3 Stop at AWAITING_WINDOW_REVIEW.

### 5.2 `KI-W5-S002` — keyword intelligence validation

```yaml
subwindow_id: KI-W5-S002
type: FILE
parent_window_id: KI-W5
parent_assignment_id: ASG-KI-W5-WA-02
assigned_agent: UNASSIGNED
predecessors: [KI-W5-S001]
successor_reserved_for: WINDOW-AGENT
writable_file: frontend/lib/keyword-intelligence-validation.ts
file_operation: CREATE
starting_file_digest: ABSENT
starting_repository_change_set_digest: f1d1d8e1ce5db60be7eca760ae2709954a824897ca40fb5e81ac6b36801a9a8b
read_only_scope:
  - frontend/lib/keyword-intelligence-types.ts (accepted S001 output)
  - frontend/lib/api-validation.ts (ApiPayloadError at line 41; parseRunStatus export; helper style)
  - KEYWORD_INTELLIGENCE_DECISION_LEDGER.md lines 248-347, 404-445
authorized_actions:
  - read every file listed in read_only_scope
  - create exactly writable_file with the I-F2 export surface
  - run the exact LOCAL_NOW checks of this block
  - report the exact handoff to the window agent
prohibited_actions: [the KI-W5-S001 list]
may_start_successor: false
```

Mechanical trace: `REQ-KI-001/002/005-009/018`;
`DEC-KI-012/013/014/015/019`; `KI-W5-T1` interface item; consumed by S005,
S017–S021, S024, S026; exercised by `W5-A01`–`W5-A07`, `W5-NC01/NC07/NC12`.

Exact transformation:

1. Create `frontend/lib/keyword-intelligence-validation.ts` with exactly
   the I-F2 export surface. Parser helpers follow the `api-validation.ts`
   style (private `record`/`text`/`number`/`integer`/`oneOf` helpers
   throwing `ApiPayloadError(path)`), one `parseX` per public type,
   unknown-key rejection on every object via exact key-set comparison.
2. `parseResearchView` enforces the 15-key exact set; `progress` 4-key
   exact set with the seven-value stage enum and 5-key `StageCounts`
   (nonnegative safe integers); `result` null unless
   `state === "completed"`; `selection` 0..200 items with the `DEC-KI-014`
   exact key set and `sourceKind ∈ calculated|manual`;
   `selectionConflicts` items with the `DEC-KI-015` exact shapes
   (`conflictId`, sorted `itemIds`, `pairs` with
   `reason ∈ compact|similarity`, `canonicalItemId`); `selectionRevision`
   safe integer ≥ 0; `safeError` null or exactly `{code,message}`;
   ISO-or-null dates with `createdAt`/`updatedAt` non-null; `markets`
   nonempty array of exact 5-key market objects with unique codes from the
   nine-code set; `seeds` 1..5 strings; `generation` safe integer ≥ 1;
   `contractVersion` nonempty string; `statusUrl` string.
3. The result branch enforces the `DEC-KI-012` exact key sets: result
   header (`contractVersion,researchId,generation,configFingerprint,seeds,
   markets,summary,keywords,clusters`); market metric (all `DEC-KI-012`
   keys incl. `monthlyHistory` 15..102 entries with `month` 1..12 and
   nonnegative safe-integer `searchVolume`, `competitionLevel`/
   `mainIntent` enums, `opportunityScore` 0..100); keyword row (all
   `DEC-KI-012` keys incl. `facets` exact five arrays, `lane` four-enum,
   `marketMetrics` exact nine keys, nullable fields null-only); cluster
   row (`laneCounts` exact four lane keys, each present value a safe
   integer ≥ 1 per the ledger's "each present value a positive integer"
   clause); summary 15-key exact set with nonnegative integers.
4. `parseRunHandoffEnvelope` enforces exactly `{run,statusUrl}` with `run`
   via `parseRunStatus` and `statusUrl` nonempty string.
5. `validateSeedsInput`/`newClientRequestId`/pattern constants exactly per
   I-F2.
6. Forbidden: probing alternate envelopes; accepting unknown keys
   anywhere; zod or new dependencies; logging payloads.

Exact checks (`LOCAL_NOW`, from `frontend/`):

- C1 porcelain → exactly the cumulative two-file set
  (`?? lib/keyword-intelligence-types.ts`,
  `?? lib/keyword-intelligence-validation.ts`).
- C2 `npx tsc --noEmit` → 0. C3 `npm run lint` → 0. C4 `npm test` → green.
- C5 `node --experimental-strip-types -e "const m = await import('./lib/keyword-intelligence-validation.ts'); const keys = Object.keys(m).sort().join(); if (keys !== 'CLIENT_REQUEST_ID_PATTERN,KEYWORD_RESEARCH_ID_PATTERN,newClientRequestId,parseResearchEnvelope,parseResearchView,parseRunHandoffEnvelope,validKeywordResearchId,validateSeedsInput') process.exit(1);"`
  → exit 0 (Node-importable with the exact surface).
- Coverage: zero local case IDs (executed in S024).
- Expected workspace write set: the one file only.

Completion checklist (sub-window standard §7.5):

- [ ] P1 Revisions, assignment identity, writable file, baseline digest, and predecessor evidence match.
- [ ] P2 Starting repository status and protected dirty changes match the recorded baseline.
- [ ] T1 Apply every ordered transformation and no other edit to the writable file.
- [ ] V1 Run every LOCAL_NOW check and record its activation witnesses and exact assertions.
- [ ] V2 Prove the attributable workspace changed-file set is exactly the writable file.
- [ ] V3 Prove required local coverage IDs equal registered and executed local IDs with zero skips.
- [ ] H1 Return the exact diff, ending digest, commands, outcomes, and residual integration obligations.
- [ ] H2 Confirm no prohibited action, second-file edit, successor work, external mutation, or parent communication occurred.
- [ ] H3 Stop at AWAITING_WINDOW_REVIEW.

### 5.3 `KI-W5-S003` — api-types additive keyword exports

```yaml
subwindow_id: KI-W5-S003
type: FILE
parent_window_id: KI-W5
parent_assignment_id: ASG-KI-W5-WA-02
assigned_agent: UNASSIGNED
predecessors: [KI-W5-S002]
successor_reserved_for: WINDOW-AGENT
writable_file: frontend/lib/api-types.ts
file_operation: MODIFY
starting_file_digest: 25d6bd8e9ef371db2b9c1e9937a9991123675f397db5f9fcddae8822f6b6dd7d
starting_repository_change_set_digest: f1d1d8e1ce5db60be7eca760ae2709954a824897ca40fb5e81ac6b36801a9a8b
read_only_scope:
  - frontend/lib/api-types.ts
  - frontend/lib/keyword-intelligence-types.ts (accepted S001 output)
  - frontend/test/api-validation.test.ts (existing import behavior)
authorized_actions:
  - read every file listed in read_only_scope
  - append exactly the I-F3 block to writable_file
  - run the exact LOCAL_NOW checks of this block
  - report the exact handoff to the window agent
prohibited_actions: [the KI-W5-S001 list]
may_start_successor: false
```

Mechanical trace: `KI-W5-T1` boundary item; A4 `shared_file_scope`
"api-types/api-validation/client-api additive symbols only"; exercised by
`W5-I01`, regression by C4.

Exact transformation:

1. Append at end of file (after the current last line 532), preceded by
   one blank line, exactly:

   ```ts
   // Keyword intelligence re-exports (KI-W5; additive only).
   export type {
     ClusterLaneCounts,
     ClusterRow,
     KeywordCompetitionLevel,
     KeywordFacets,
     KeywordLane,
     KeywordMainIntent,
     KeywordMarket,
     KeywordMetricSnapshot,
     KeywordResearchRunResponse,
     KeywordRow,
     MarketMetric,
     MonthlyHistoryPoint,
     ResearchProgress,
     ResearchProgressStage,
     ResearchResult,
     ResearchSafeError,
     ResearchState,
     ResearchSummary,
     ResearchView,
     SelectionConflict,
     SelectionConflictPair,
     SelectionItem,
     StageCounts,
     VariantGroup,
   } from "./keyword-intelligence-types";
   ```

2. No other line changes; existing exports and their byte behavior
   preserved.

Exact checks: C1–C4 common; C5
`grep -c "keyword-intelligence-types" lib/api-types.ts` → exactly `1` and
`git diff --numstat lib/api-types.ts` → exactly `27 insertions, 0
deletions` (blank + comment + statement lines of the block above).
Coverage: zero local case IDs. Expected write set: this file only.

Completion checklist (sub-window standard §7.5):

- [ ] P1 Revisions, assignment identity, writable file, baseline digest, and predecessor evidence match.
- [ ] P2 Starting repository status and protected dirty changes match the recorded baseline.
- [ ] T1 Apply every ordered transformation and no other edit to the writable file.
- [ ] V1 Run every LOCAL_NOW check and record its activation witnesses and exact assertions.
- [ ] V2 Prove the attributable workspace changed-file set is exactly the writable file.
- [ ] V3 Prove required local coverage IDs equal registered and executed local IDs with zero skips.
- [ ] H1 Return the exact diff, ending digest, commands, outcomes, and residual integration obligations.
- [ ] H2 Confirm no prohibited action, second-file edit, successor work, external mutation, or parent communication occurred.
- [ ] H3 Stop at AWAITING_WINDOW_REVIEW.

### 5.4 `KI-W5-S004` — api-validation additive keyword parsers

```yaml
subwindow_id: KI-W5-S004
type: FILE
parent_window_id: KI-W5
parent_assignment_id: ASG-KI-W5-WA-02
assigned_agent: UNASSIGNED
predecessors: [KI-W5-S003]
successor_reserved_for: WINDOW-AGENT
writable_file: frontend/lib/api-validation.ts
file_operation: MODIFY
starting_file_digest: 1522c8c46db5a1af33d8723140722ba1a8883a718a07ca5d5397355341829b55
starting_repository_change_set_digest: f1d1d8e1ce5db60be7eca760ae2709954a824897ca40fb5e81ac6b36801a9a8b
read_only_scope:
  - frontend/lib/api-validation.ts
  - frontend/lib/keyword-intelligence-validation.ts (accepted S002 output)
  - frontend/test/api-validation.test.ts
authorized_actions:
  - read every file listed in read_only_scope
  - append exactly the I-F4 block to writable_file
  - run the exact LOCAL_NOW checks of this block
  - report the exact handoff to the window agent
prohibited_actions: [the KI-W5-S001 list]
may_start_successor: false
```

Mechanical trace: `KI-W5-T1` boundary item; A4 `shared_file_scope`
"additive parsers only"; exercised by `W5-I02`, `W5-NC12`; regression by
C4 (the relative re-export preserves Node importability of
`api-validation.ts`).

Exact transformation:

1. Append at end of file (after current line 1318), preceded by one blank
   line, exactly:

   ```ts
   // Keyword intelligence parsers (KI-W5; additive only).
   export {
     CLIENT_REQUEST_ID_PATTERN,
     KEYWORD_RESEARCH_ID_PATTERN,
     newClientRequestId,
     parseResearchEnvelope,
     parseResearchView,
     parseRunHandoffEnvelope,
     validKeywordResearchId,
     validateSeedsInput,
   } from "./keyword-intelligence-validation";
   ```

2. No other line changes.

Exact checks: C1–C4 common; C5
`grep -c "keyword-intelligence-validation" lib/api-validation.ts` → `1`
and `node --experimental-strip-types -e "const m = await import('./lib/api-validation.ts'); if (typeof m.parseResearchView !== 'function' || typeof m.parseRunStatus !== 'function') process.exit(1);"`
→ exit 0. Coverage: zero local case IDs. Expected write set: this file
only.

Completion checklist (sub-window standard §7.5):

- [ ] P1 Revisions, assignment identity, writable file, baseline digest, and predecessor evidence match.
- [ ] P2 Starting repository status and protected dirty changes match the recorded baseline.
- [ ] T1 Apply every ordered transformation and no other edit to the writable file.
- [ ] V1 Run every LOCAL_NOW check and record its activation witnesses and exact assertions.
- [ ] V2 Prove the attributable workspace changed-file set is exactly the writable file.
- [ ] V3 Prove required local coverage IDs equal registered and executed local IDs with zero skips.
- [ ] H1 Return the exact diff, ending digest, commands, outcomes, and residual integration obligations.
- [ ] H2 Confirm no prohibited action, second-file edit, successor work, external mutation, or parent communication occurred.
- [ ] H3 Stop at AWAITING_WINDOW_REVIEW.

### 5.5 `KI-W5-S005` — client-api additive keyword methods

```yaml
subwindow_id: KI-W5-S005
type: FILE
parent_window_id: KI-W5
parent_assignment_id: ASG-KI-W5-WA-02
assigned_agent: UNASSIGNED
predecessors: [KI-W5-S004]
successor_reserved_for: WINDOW-AGENT
writable_file: frontend/lib/client-api.ts
file_operation: MODIFY
starting_file_digest: 84f20e6ba5c3ca2bd17147f8ef46235cd9f6460ebcb49f1ec40228d4cd881046
starting_repository_change_set_digest: f1d1d8e1ce5db60be7eca760ae2709954a824897ca40fb5e81ac6b36801a9a8b
read_only_scope:
  - frontend/lib/client-api.ts
  - frontend/lib/keyword-intelligence-validation.ts (accepted S002 output)
  - frontend/lib/keyword-intelligence-types.ts (accepted S001 output)
authorized_actions:
  - read every file listed in read_only_scope
  - append exactly the I-F5 imports and functions to writable_file
  - run the exact LOCAL_NOW checks of this block
  - report the exact handoff to the window agent
prohibited_actions: [the KI-W5-S001 list]
may_start_successor: false
```

Mechanical trace: `REQ-KI-001/002/005-009/015`; `DEC-KI-019`; `KI-W5-T1`
algorithm item ("client creates/loads/saves/finalizes via same-origin
API"); consumed by S008/S009/S013/S016; behavioral oracle executed in S027
(`W5-B03`, `W5-R03`, `W5-R04` request-log assertions). Node import of this
file is impossible because its pre-existing line 2 uses the `@/` alias, so
no local Node case IDs are allocated here — recorded as a deliberate
allocation, not a skip.

Exact transformation:

1. Insert directly after the existing line-2 import the two I-F5 import
   lines (runtime re-export import from
   `./keyword-intelligence-validation`; type-only import from
   `./keyword-intelligence-types`), keeping import order stable.
2. Append at end of file, preceded by one blank line, the four I-F5
   functions exactly as specified (URLs, methods, bodies, parse
   functions). No other line changes; `ApiRequestError` mapping
   (401/404/409/4xx) flows through the untouched `apiRequest`.

Exact checks: C1–C4 common; C5
`grep -c "export async function createKeywordResearch\|export async function getKeywordResearch\|export async function saveKeywordSelection\|export async function startKeywordResearchRun" lib/client-api.ts`
→ exactly `4`. Coverage: zero local case IDs (allocation note above).
Expected write set: this file only.

Completion checklist (sub-window standard §7.5):

- [ ] P1 Revisions, assignment identity, writable file, baseline digest, and predecessor evidence match.
- [ ] P2 Starting repository status and protected dirty changes match the recorded baseline.
- [ ] T1 Apply every ordered transformation and no other edit to the writable file.
- [ ] V1 Run every LOCAL_NOW check and record its activation witnesses and exact assertions.
- [ ] V2 Prove the attributable workspace changed-file set is exactly the writable file.
- [ ] V3 Prove required local coverage IDs equal registered and executed local IDs with zero skips.
- [ ] H1 Return the exact diff, ending digest, commands, outcomes, and residual integration obligations.
- [ ] H2 Confirm no prohibited action, second-file edit, successor work, external mutation, or parent communication occurred.
- [ ] H3 Stop at AWAITING_WINDOW_REVIEW.

### 5.6 `KI-W5-S006` — keyword intelligence view model

```yaml
subwindow_id: KI-W5-S006
type: FILE
parent_window_id: KI-W5
parent_assignment_id: ASG-KI-W5-WA-02
assigned_agent: UNASSIGNED
predecessors: [KI-W5-S005]
successor_reserved_for: WINDOW-AGENT
writable_file: frontend/lib/keyword-intelligence-view-model.ts
file_operation: CREATE
starting_file_digest: ABSENT
starting_repository_change_set_digest: f1d1d8e1ce5db60be7eca760ae2709954a824897ca40fb5e81ac6b36801a9a8b
read_only_scope:
  - KeywordSearchVolume/dashboard/index.html (the I-F12-named functions with their line anchors)
  - email_scraper/src/keyword-intelligence/export.js (EXPORT_CSV_COLUMNS source; read-only)
  - KEYWORD_INTELLIGENCE_DECISION_LEDGER.md lines 294-347 (DEC-KI-013/014/015), 404-445 (DEC-KI-019)
  - frontend/lib/keyword-intelligence-types.ts (accepted S001 output)
authorized_actions:
  - read every file listed in read_only_scope
  - create exactly writable_file with the I-F12 export surface
  - run the exact LOCAL_NOW checks of this block
  - report the exact handoff to the window agent
prohibited_actions: [the KI-W5-S001 list]
may_start_successor: false
```

Mechanical trace: `REQ-KI-006/007/008/009/014/018`;
`DEC-KI-013/014/015/019/023`; `KI-W5-T2` items 5-11; consumed by S008–S016,
S024, S025, S026, S027; exercised by `W5-C01`–`W5-C12`, `W5-A08/A09/A10`,
`W5-I03/I05`, `W5-NC02/NC08/NC09`.

Exact transformation:

1. Create the file implementing exactly the I-F12 export surface. Each
   ported function preserves the standalone function's predicates, order,
   arithmetic, and outputs, transcribed from the named anchors:
   `activeRows`/`distinctKeywordRows`/`cumulativeVolume` (standalone
   utilities/projection block), `projectMarketRow` (index.html:962),
   `getFiltered` (index.html:996), the aggregation block
   (`aggregateByCluster`, `adjustedVolume`, `median`,
   `metricFingerprint`, `discoveryLane`, `laneLabel`), the formatters
   (`fmtNum`, `fmtCPC`, `fmtPct`, `fmtSlope`), `currentSummary`/
   `currentClusterMetric`, the sort-comparator semantics
   (`buildTableHead`/`compareRows`), pagination clamping, and
   `filterOptionSources` (the `populateFilterOptions` outputs).
2. Selection helpers implement the `DEC-KI-013/014/015` semantics exactly
   as I-F12 specifies (candidate-order insertion, 200-cap no-op, manual
   items, edit reclassification via the ported classifier,
   `canFinalizeSelection` gating).
3. `EXPORT_CSV_COLUMNS` is the literal header list copied from the
   accepted `email_scraper/src/keyword-intelligence/export.js` CSV header
   (read-only; byte-identical names and order).
4. `KEYWORD_INTELLIGENCE_SURFACE_INVENTORY` is the literal I-F15 list.
5. No React, no fetch, no `localStorage` access, no `@/` runtime imports.

Exact checks: C1–C4 common; C5
`node --experimental-strip-types -e "const m = await import('./lib/keyword-intelligence-view-model.ts'); if (m.KEYWORD_INTELLIGENCE_SURFACE_INVENTORY.length !== 21 || m.nextPollDelay(2000) !== 3000 || m.nextPollDelay(4500) !== 6750 || m.nextPollDelay(6750) !== 10000 || m.nextPollDelay(10000) !== 10000) process.exit(1);"`
→ exit 0. Coverage: zero local case IDs (executed in S025). Expected write
set: this file only.

Completion checklist (sub-window standard §7.5):

- [ ] P1 Revisions, assignment identity, writable file, baseline digest, and predecessor evidence match.
- [ ] P2 Starting repository status and protected dirty changes match the recorded baseline.
- [ ] T1 Apply every ordered transformation and no other edit to the writable file.
- [ ] V1 Run every LOCAL_NOW check and record its activation witnesses and exact assertions.
- [ ] V2 Prove the attributable workspace changed-file set is exactly the writable file.
- [ ] V3 Prove required local coverage IDs equal registered and executed local IDs with zero skips.
- [ ] H1 Return the exact diff, ending digest, commands, outcomes, and residual integration obligations.
- [ ] H2 Confirm no prohibited action, second-file edit, successor work, external mutation, or parent communication occurred.
- [ ] H3 Stop at AWAITING_WINDOW_REVIEW.

### 5.7 `KI-W5-S007` — dashboard CSS module

```yaml
subwindow_id: KI-W5-S007
type: FILE
parent_window_id: KI-W5
parent_assignment_id: ASG-KI-W5-WA-02
assigned_agent: UNASSIGNED
predecessors: [KI-W5-S006]
successor_reserved_for: WINDOW-AGENT
writable_file: frontend/components/keyword-intelligence/keyword-dashboard.module.css
file_operation: CREATE
starting_file_digest: ABSENT
starting_repository_change_set_digest: f1d1d8e1ce5db60be7eca760ae2709954a824897ca40fb5e81ac6b36801a9a8b
read_only_scope:
  - KeywordSearchVolume/dashboard/index.html lines 12-467 (style block) and the class attributes of the DOM markup
authorized_actions:
  - read every file listed in read_only_scope
  - create exactly writable_file per I-F13
  - run the exact LOCAL_NOW checks of this block
  - report the exact handoff to the window agent
prohibited_actions: [the KI-W5-S001 list]
may_start_successor: false
```

Mechanical trace: `REQ-KI-014`; `DEC-KI-023`; `KI-W5-T3` responsive
styling item; consumed by S008–S016; verified at I001 (`W5-R05`).

Exact transformation:

1. Create the CSS module porting every rule of the standalone `<style>`
   block into module scope: kebab-case class selectors become camelCase
   class exports with a documented exact mapping (e.g. `table-scroll` →
   `tableScroll`, `chart-wrap` → `chartWrap`, `cluster-scene-layout` →
   `clusterSceneLayout`, `seed-chip-field` → `seedChipField`,
   `empty-state` → `emptyState`, `error-banner` → `errorBanner`,
   `keyword-dialog` → `keywordDialog`, `selection-status` →
   `selectionStatus`); `:root` custom properties become `.kiDashboard`
   locals with identical values; `[data-theme="dark"]` overrides become
   `.kiDashboard[data-ki-theme="dark"]` with descendant selectors
   rewritten against module classes; element selectors from the standalone
   are scoped under `.kiDashboard`.
2. Media queries and responsive rules are preserved with the same
   breakpoints.

Exact checks: C1–C4 common; C5
`grep -c "^:root\|^body\|^html" components/keyword-intelligence/keyword-dashboard.module.css`
→ `0` and
`grep -c "kiDashboard" components/keyword-intelligence/keyword-dashboard.module.css`
→ ≥ `2`. Coverage: zero local case IDs. Expected write set: this file only
(plus the new directory).

Completion checklist (sub-window standard §7.5):

- [ ] P1 Revisions, assignment identity, writable file, baseline digest, and predecessor evidence match.
- [ ] P2 Starting repository status and protected dirty changes match the recorded baseline.
- [ ] T1 Apply every ordered transformation and no other edit to the writable file.
- [ ] V1 Run every LOCAL_NOW check and record its activation witnesses and exact assertions.
- [ ] V2 Prove the attributable workspace changed-file set is exactly the writable file.
- [ ] V3 Prove required local coverage IDs equal registered and executed local IDs with zero skips.
- [ ] H1 Return the exact diff, ending digest, commands, outcomes, and residual integration obligations.
- [ ] H2 Confirm no prohibited action, second-file edit, successor work, external mutation, or parent communication occurred.
- [ ] H3 Stop at AWAITING_WINDOW_REVIEW.

### 5.8 `KI-W5-S008` — research form component

```yaml
subwindow_id: KI-W5-S008
type: FILE
parent_window_id: KI-W5
parent_assignment_id: ASG-KI-W5-WA-02
assigned_agent: UNASSIGNED
predecessors: [KI-W5-S007]
successor_reserved_for: WINDOW-AGENT
writable_file: frontend/components/keyword-intelligence/research-form.tsx
file_operation: CREATE
starting_file_digest: ABSENT
starting_repository_change_set_digest: f1d1d8e1ce5db60be7eca760ae2709954a824897ca40fb5e81ac6b36801a9a8b
read_only_scope:
  - KeywordSearchVolume/dashboard/index.html seed phrase form block (seed-phrase-form, seed-chip-field, seed-chip-count, seed-market-note, keyword-submit)
  - frontend/components/run-form.tsx (existing client form pattern)
  - frontend/lib/client-api.ts, frontend/lib/keyword-intelligence-validation.ts, frontend/lib/keyword-intelligence-view-model.ts (accepted outputs)
  - node_modules/next/dist/docs/01-app/03-api-reference/03-file-conventions/page.md
authorized_actions:
  - read every file listed in read_only_scope
  - create exactly writable_file per I-F14 ResearchForm
  - run the exact LOCAL_NOW checks of this block
  - report the exact handoff to the window agent
prohibited_actions: [the KI-W5-S001 list]
may_start_successor: false
```

Mechanical trace: `REQ-KI-001/002`; `DEC-KI-019`; `KI-W5-T1` algorithm
item; `SRC-KI-010` seed form; exercised by `W5-B01`, `W5-R04` (no
re-create on retry).

Exact transformation:

1. Create the `"use client"` component with the exact I-F14 props. Chip
   field adds/removes seeds (Enter/comma split, the `parseKeywordLines`
   port: NFKC/trim/collapse), count display "1-5 seeds", market note text
   ported, submit button disabled while in flight or when
   `validateSeedsInput` fails; client-side validation error text under the
   field; on 401 `ApiRequestError` renders the sign-in CTA linking
   `/sign-in`; on success calls `onCreated(view)` exactly once (default
   navigation per I-F14); on other errors renders `errorMessage` safely.
2. Styling only via the S007 CSS module classes; accessible labels and
   `aria-*` matching the standalone markup.

Exact checks: C1–C4 common; C5
`grep -c '"use client"' components/keyword-intelligence/research-form.tsx`
→ `1`. Coverage: zero local case IDs. Expected write set: this file only.

Completion checklist (sub-window standard §7.5):

- [ ] P1 Revisions, assignment identity, writable file, baseline digest, and predecessor evidence match.
- [ ] P2 Starting repository status and protected dirty changes match the recorded baseline.
- [ ] T1 Apply every ordered transformation and no other edit to the writable file.
- [ ] V1 Run every LOCAL_NOW check and record its activation witnesses and exact assertions.
- [ ] V2 Prove the attributable workspace changed-file set is exactly the writable file.
- [ ] V3 Prove required local coverage IDs equal registered and executed local IDs with zero skips.
- [ ] H1 Return the exact diff, ending digest, commands, outcomes, and residual integration obligations.
- [ ] H2 Confirm no prohibited action, second-file edit, successor work, external mutation, or parent communication occurred.
- [ ] H3 Stop at AWAITING_WINDOW_REVIEW.

### 5.9 `KI-W5-S009` — research status component

```yaml
subwindow_id: KI-W5-S009
type: FILE
parent_window_id: KI-W5
parent_assignment_id: ASG-KI-W5-WA-02
assigned_agent: UNASSIGNED
predecessors: [KI-W5-S008]
successor_reserved_for: WINDOW-AGENT
writable_file: frontend/components/keyword-intelligence/research-status.tsx
file_operation: CREATE
starting_file_digest: ABSENT
starting_repository_change_set_digest: f1d1d8e1ce5db60be7eca760ae2709954a824897ca40fb5e81ac6b36801a9a8b
read_only_scope:
  - frontend/components/run-progress.tsx (existing progress surface pattern)
  - frontend/lib/client-api.ts, frontend/lib/keyword-intelligence-view-model.ts (accepted outputs)
  - KEYWORD_INTELLIGENCE_DECISION_LEDGER.md lines 428-439 (progress contract)
authorized_actions:
  - read every file listed in read_only_scope
  - create exactly writable_file per I-F14 ResearchStatus and I-F16
  - run the exact LOCAL_NOW checks of this block
  - report the exact handoff to the window agent
prohibited_actions: [the KI-W5-S001 list]
may_start_successor: false
```

Mechanical trace: `REQ-KI-002`; `DEC-KI-018/019`; `KI-W5-T1` algorithm
item (one timer, capped 2s→10s, terminal stop, retry GET only); exercised
by `W5-A08` (logic), `W5-R01/R02/R04`, `W5-NC05`.

Exact transformation:

1. Create the component per I-F14/I-F16: a `useRef` holds the pending
   timeout and an `aborted` flag; on mount a `setTimeout` chain schedules
   polls with `nextPollDelay` starting at 2000; each poll calls
   `getKeywordResearch`, replaces the view, and reschedules unless
   `isTerminalResearchState`; on terminal calls `onTerminal(view)` exactly
   once; cleanup clears the timeout and flag; retry button calls
   `getKeywordResearch` only; the progress surface renders the three
   `StageCounts` rows (expected/succeeded/skipped/failed) with stage label
   and the seven-stage order incl. `finalizing`; network/5xx errors keep
   polling on the ladder with a soft retry notice; a failed terminal
   renders `safeError.message` verbatim (backend-sanitized) with the code
   as `data-code`.

Exact checks: C1–C4 common; C5
`grep -c "setTimeout\|setInterval" components/keyword-intelligence/research-status.tsx`
→ exactly `1` (only `setTimeout`). Coverage: zero local case IDs.
Expected write set: this file only.

Completion checklist (sub-window standard §7.5):

- [ ] P1 Revisions, assignment identity, writable file, baseline digest, and predecessor evidence match.
- [ ] P2 Starting repository status and protected dirty changes match the recorded baseline.
- [ ] T1 Apply every ordered transformation and no other edit to the writable file.
- [ ] V1 Run every LOCAL_NOW check and record its activation witnesses and exact assertions.
- [ ] V2 Prove the attributable workspace changed-file set is exactly the writable file.
- [ ] V3 Prove required local coverage IDs equal registered and executed local IDs with zero skips.
- [ ] H1 Return the exact diff, ending digest, commands, outcomes, and residual integration obligations.
- [ ] H2 Confirm no prohibited action, second-file edit, successor work, external mutation, or parent communication occurred.
- [ ] H3 Stop at AWAITING_WINDOW_REVIEW.

### 5.10 `KI-W5-S010` — filter bar component

```yaml
subwindow_id: KI-W5-S010
type: FILE
parent_window_id: KI-W5
parent_assignment_id: ASG-KI-W5-WA-02
assigned_agent: UNASSIGNED
predecessors: [KI-W5-S009]
successor_reserved_for: WINDOW-AGENT
writable_file: frontend/components/keyword-intelligence/filter-bar.tsx
file_operation: CREATE
starting_file_digest: ABSENT
starting_repository_change_set_digest: f1d1d8e1ce5db60be7eca760ae2709954a824897ca40fb5e81ac6b36801a9a8b
read_only_scope:
  - KeywordSearchVolume/dashboard/index.html filter controls block (f-search, f-market, f-seed, f-cluster, f-intent, f-lane, f-category, f-audience, f-channel, f-minvol, f-minopp, f-rec, f-flags, f-reset) and readFilters/applyFilters/resetFilters
  - frontend/components/results-filters.tsx (existing filter pattern)
  - frontend/lib/keyword-intelligence-view-model.ts (accepted S006 output)
authorized_actions:
  - read every file listed in read_only_scope
  - create exactly writable_file per I-F14 FilterBar
  - run the exact LOCAL_NOW checks of this block
  - report the exact handoff to the window agent
prohibited_actions: [the KI-W5-S001 list]
may_start_successor: false
```

Mechanical trace: `REQ-KI-014`; `DEC-KI-023`; `KI-W5-T2` filter state
item; exercised by `W5-C05`, `W5-B02`.

Exact transformation:

1. Create the component per I-F14: one control per `KeywordFilterState`
   field (search text; market select with `all` plus the nine codes; seed,
   cluster, intent, lane, category, audience, channel selects;
   minVolume/minOpportunity numeric inputs; recommended tri-state; flags
   multi-select chips; reset button calling `onReset`); every change emits
   exactly one `onChange` patch; labels and option groups mirror the
   standalone filter markup including the per-market note text; each
   control carries `data-filter="<field>"`.

Exact checks: C1–C4 common; C5
`grep -c "data-filter" components/keyword-intelligence/filter-bar.tsx` →
`14` (one per filter field). Coverage: zero local case IDs. Expected
write set: this file only.

Completion checklist (sub-window standard §7.5):

- [ ] P1 Revisions, assignment identity, writable file, baseline digest, and predecessor evidence match.
- [ ] P2 Starting repository status and protected dirty changes match the recorded baseline.
- [ ] T1 Apply every ordered transformation and no other edit to the writable file.
- [ ] V1 Run every LOCAL_NOW check and record its activation witnesses and exact assertions.
- [ ] V2 Prove the attributable workspace changed-file set is exactly the writable file.
- [ ] V3 Prove required local coverage IDs equal registered and executed local IDs with zero skips.
- [ ] H1 Return the exact diff, ending digest, commands, outcomes, and residual integration obligations.
- [ ] H2 Confirm no prohibited action, second-file edit, successor work, external mutation, or parent communication occurred.
- [ ] H3 Stop at AWAITING_WINDOW_REVIEW.

### 5.11 `KI-W5-S011` — summary cards component

```yaml
subwindow_id: KI-W5-S011
type: FILE
parent_window_id: KI-W5
parent_assignment_id: ASG-KI-W5-WA-02
assigned_agent: UNASSIGNED
predecessors: [KI-W5-S010]
successor_reserved_for: WINDOW-AGENT
writable_file: frontend/components/keyword-intelligence/summary-cards.tsx
file_operation: CREATE
starting_file_digest: ABSENT
starting_repository_change_set_digest: f1d1d8e1ce5db60be7eca760ae2709954a824897ca40fb5e81ac6b36801a9a8b
read_only_scope:
  - KeywordSearchVolume/dashboard/index.html renderCards, renderFunnel, renderDiscoverySegments, renderOverlapWarnings blocks and their DOM (c-total, c-volume, c-cpc, c-rec, c-active, c-clusters, collection-funnel, discovery-segments, overlap-warnings, overlap-summary)
  - frontend/lib/keyword-intelligence-view-model.ts (accepted S006 output)
authorized_actions:
  - read every file listed in read_only_scope
  - create exactly writable_file per I-F14 SummaryCards
  - run the exact LOCAL_NOW checks of this block
  - report the exact handoff to the window agent
prohibited_actions: [the KI-W5-S001 list]
may_start_successor: false
```

Mechanical trace: `REQ-KI-014/018`; `DEC-KI-023`; `KI-W5-T2`; exercised
by `W5-B01`.

Exact transformation:

1. Create the component per I-F14: the summary cards driven by
   `currentSummary(result, marketCode)` with market-context text; funnel
   segments from summary counts; discovery segments by lane counts;
   overlap warnings from cluster variant-overlap data (port of
   `renderOverlapWarnings` inputs/outputs); all values formatted through
   the I-F12 formatters; no chart instances.

Exact checks: C1–C4 common; C5
`grep -c "new Chart" components/keyword-intelligence/summary-cards.tsx` →
`0`. Coverage: zero local case IDs. Expected write set: this file only.

Completion checklist (sub-window standard §7.5):

- [ ] P1 Revisions, assignment identity, writable file, baseline digest, and predecessor evidence match.
- [ ] P2 Starting repository status and protected dirty changes match the recorded baseline.
- [ ] T1 Apply every ordered transformation and no other edit to the writable file.
- [ ] V1 Run every LOCAL_NOW check and record its activation witnesses and exact assertions.
- [ ] V2 Prove the attributable workspace changed-file set is exactly the writable file.
- [ ] V3 Prove required local coverage IDs equal registered and executed local IDs with zero skips.
- [ ] H1 Return the exact diff, ending digest, commands, outcomes, and residual integration obligations.
- [ ] H2 Confirm no prohibited action, second-file edit, successor work, external mutation, or parent communication occurred.
- [ ] H3 Stop at AWAITING_WINDOW_REVIEW.

### 5.12 `KI-W5-S012` — keyword table component

```yaml
subwindow_id: KI-W5-S012
type: FILE
parent_window_id: KI-W5
parent_assignment_id: ASG-KI-W5-WA-02
assigned_agent: UNASSIGNED
predecessors: [KI-W5-S011]
successor_reserved_for: WINDOW-AGENT
writable_file: frontend/components/keyword-intelligence/keyword-table.tsx
file_operation: CREATE
starting_file_digest: ABSENT
starting_repository_change_set_digest: f1d1d8e1ce5db60be7eca760ae2709954a824897ca40fb5e81ac6b36801a9a8b
read_only_scope:
  - KeywordSearchVolume/dashboard/index.html renderTable (2465), buildTableHead, compareRows, updateSortArrows, trendCell, flagsCell and pagination controls (table-head, table-body, table-count, page-info, page-prev, page-next, page-size)
  - frontend/components/results-table.tsx (existing table pattern)
  - frontend/lib/keyword-intelligence-view-model.ts (accepted S006 output)
authorized_actions:
  - read every file listed in read_only_scope
  - create exactly writable_file per I-F14 KeywordTable
  - run the exact LOCAL_NOW checks of this block
  - report the exact handoff to the window agent
prohibited_actions: [the KI-W5-S001 list]
may_start_successor: false
```

Mechanical trace: `REQ-KI-006/014`; `DEC-KI-013/023`; `KI-W5-T2` items
5/9/11 (itemId keys, pagination bounds); exercised by `W5-C06`,
`W5-B02/B03`.

Exact transformation:

1. Create the component per I-F14: table head with sortable columns
   (`aria-sort` plus arrow indicators per `updateSortArrows`), body rows
   keyed by `row.itemId`, selection checkbox per row reflecting
   `selectionItemIds`, trend and flags cells ported, row count and page
   info, page prev/next and the page-size select with the standalone
   sizes, clamped via `paginate`; the edit control on managed rows emits
   `onEditItem(itemId)`; the empty filtered state renders the standalone
   empty row.

Exact checks: C1–C4 common; C5
`grep -c "key={row.itemId}" components/keyword-intelligence/keyword-table.tsx`
→ ≥ `1`. Coverage: zero local case IDs. Expected write set: this file
only.

Completion checklist (sub-window standard §7.5):

- [ ] P1 Revisions, assignment identity, writable file, baseline digest, and predecessor evidence match.
- [ ] P2 Starting repository status and protected dirty changes match the recorded baseline.
- [ ] T1 Apply every ordered transformation and no other edit to the writable file.
- [ ] V1 Run every LOCAL_NOW check and record its activation witnesses and exact assertions.
- [ ] V2 Prove the attributable workspace changed-file set is exactly the writable file.
- [ ] V3 Prove required local coverage IDs equal registered and executed local IDs with zero skips.
- [ ] H1 Return the exact diff, ending digest, commands, outcomes, and residual integration obligations.
- [ ] H2 Confirm no prohibited action, second-file edit, successor work, external mutation, or parent communication occurred.
- [ ] H3 Stop at AWAITING_WINDOW_REVIEW.

### 5.13 `KI-W5-S013` — selection review component

```yaml
subwindow_id: KI-W5-S013
type: FILE
parent_window_id: KI-W5
parent_assignment_id: ASG-KI-W5-WA-02
assigned_agent: UNASSIGNED
predecessors: [KI-W5-S012]
successor_reserved_for: WINDOW-AGENT
writable_file: frontend/components/keyword-intelligence/selection-review.tsx
file_operation: CREATE
starting_file_digest: ABSENT
starting_repository_change_set_digest: f1d1d8e1ce5db60be7eca760ae2709954a824897ca40fb5e81ac6b36801a9a8b
read_only_scope:
  - KeywordSearchVolume/dashboard/index.html renderResearchPhrases, renderDecisionPanels (1319), keyword dialog flows (keyword-dialog, keyword-input, keyword-line-count, manual-keyword-input, add/edit/cancel actions, keyword-toast, selection-status, clear-selection)
  - frontend/lib/keyword-intelligence-view-model.ts, frontend/lib/client-api.ts (accepted outputs)
  - KEYWORD_INTELLIGENCE_DECISION_LEDGER.md lines 294-347 (DEC-KI-013/014/015)
authorized_actions:
  - read every file listed in read_only_scope
  - create exactly writable_file per I-F14 SelectionReview
  - run the exact LOCAL_NOW checks of this block
  - report the exact handoff to the window agent
prohibited_actions: [the KI-W5-S001 list]
may_start_successor: false
```

Mechanical trace: `REQ-KI-007/008/009/015`; `DEC-KI-013/014/015/017`;
`KI-W5-T2` items 6/8/10; exercised by `W5-A09/A10` (logic), `W5-B03/B04`,
`W5-R03`, `W5-NC09`.

Exact transformation:

1. Create the component per I-F14: the ordered selected list (rank,
   keyword, calculated/manual source badge, lane/facet chips, remove); the
   manual add field with the `parseKeywordLines` port; the edit dialog for
   calculated items (original preserved; reclassified lane/facets shown
   before commit — the `beginPhraseEdit`/`commitManualPhrase` semantics
   through the I-F12 helpers); the over-100 warning banner; the
   `selectionConflicts` review list (pair keywords, reason, similarity,
   canonical suggestion per `DEC-KI-015`) blocking finalize until
   resolved; save disabled while `saving`; the stale-conflict surface
   (from the `staleConflict` prop) requiring explicit reload; finalize
   disabled unless `canFinalizeSelection(...).ok`; `finalizeState ===
   "handing-off"` disables double-click (the parent retains the
   `clientRequestId`).

Exact checks: C1–C4 common; C5
`grep -c "localStorage" components/keyword-intelligence/selection-review.tsx`
→ `0`. Coverage: zero local case IDs. Expected write set: this file only.

Completion checklist (sub-window standard §7.5):

- [ ] P1 Revisions, assignment identity, writable file, baseline digest, and predecessor evidence match.
- [ ] P2 Starting repository status and protected dirty changes match the recorded baseline.
- [ ] T1 Apply every ordered transformation and no other edit to the writable file.
- [ ] V1 Run every LOCAL_NOW check and record its activation witnesses and exact assertions.
- [ ] V2 Prove the attributable workspace changed-file set is exactly the writable file.
- [ ] V3 Prove required local coverage IDs equal registered and executed local IDs with zero skips.
- [ ] H1 Return the exact diff, ending digest, commands, outcomes, and residual integration obligations.
- [ ] H2 Confirm no prohibited action, second-file edit, successor work, external mutation, or parent communication occurred.
- [ ] H3 Stop at AWAITING_WINDOW_REVIEW.

### 5.14 `KI-W5-S014` — chart panels component

```yaml
subwindow_id: KI-W5-S014
type: FILE
parent_window_id: KI-W5
parent_assignment_id: ASG-KI-W5-WA-02
assigned_agent: UNASSIGNED
predecessors: [KI-W5-S013]
successor_reserved_for: WINDOW-AGENT
writable_file: frontend/components/keyword-intelligence/chart-panels.tsx
file_operation: CREATE
starting_file_digest: ABSENT
starting_repository_change_set_digest: f1d1d8e1ce5db60be7eca760ae2709954a824897ca40fb5e81ac6b36801a9a8b
read_only_scope:
  - KeywordSearchVolume/dashboard/index.html chart functions (baseScales, tooltipBase, chartTopKeywords 1345, chartClusterVolume 1459, chartBubble 1513, chartScatter 1571, doughnut/chartIntent 1621, chartRecommended, chartSeeds 1705, chartHistogram 1780, chartTreemap 1826, chartFlags 1935, chartHistory 2023, renderCharts)
  - frontend/package.json (chart.js 3.9.1, chartjs-chart-treemap 2.0.0)
  - relevant node_modules/next/dist/docs/ guides
authorized_actions:
  - read every file listed in read_only_scope
  - create exactly writable_file per I-F14 ChartPanels and I-F17
  - run the exact LOCAL_NOW checks of this block
  - report the exact handoff to the window agent
prohibited_actions: [the KI-W5-S001 list; additionally no CDN/loadScript/fallback fetching]
may_start_successor: false
```

Mechanical trace: `REQ-KI-014`; `DEC-KI-023`; `KI-W5-T3` local
Chart.js/treemap item; A4 `KI-W5-P3`; exercised by `W5-B07`, `W5-R06`,
`W5-I06`, `W5-NC04/NC06`.

Exact transformation:

1. Create the component per I-F14/I-F17 with local imports from
   `chart.js` and `chartjs-chart-treemap`; a module-scope `Chart.register`
   executes once with exactly the needed controllers/elements/scales plus
   the treemap controller.
2. Eleven chart subsections on component-owned `<canvas ref>` elements,
   each dataset/options ported verbatim from the named standalone
   function (scales, `tooltipBase` tooltips, color palettes, empty-state
   overlays); datasets are memoized once per parsed
   revision/filter/market via `useMemo` over the I-F12 outputs.
3. The effect creates exactly one `Chart` per canvas; dataset changes
   assign `chart.data` and call `chart.update()` (or destroy/recreate
   exactly as the standalone refresh path requires); unmount destroys
   every instance; each canvas carries
   `data-surface="chart:<name>"` per I-F15.
4. Zero-size/empty datasets render the `.chart-empty` overlay state;
   chart construction errors are caught and surface the safe error card.

Exact checks: C1–C4 common; C5
`grep -c "cdn.jsdelivr.net\|loadScript\|loadFirst" components/keyword-intelligence/chart-panels.tsx`
→ `0` and
`grep -c "from \"chart.js\"\|from 'chart.js'" components/keyword-intelligence/chart-panels.tsx`
→ ≥ `1` and
`grep -c "chartjs-chart-treemap" components/keyword-intelligence/chart-panels.tsx`
→ ≥ `1`. Coverage: zero local case IDs. Expected write set: this file
only.

Completion checklist (sub-window standard §7.5):

- [ ] P1 Revisions, assignment identity, writable file, baseline digest, and predecessor evidence match.
- [ ] P2 Starting repository status and protected dirty changes match the recorded baseline.
- [ ] T1 Apply every ordered transformation and no other edit to the writable file.
- [ ] V1 Run every LOCAL_NOW check and record its activation witnesses and exact assertions.
- [ ] V2 Prove the attributable workspace changed-file set is exactly the writable file.
- [ ] V3 Prove required local coverage IDs equal registered and executed local IDs with zero skips.
- [ ] H1 Return the exact diff, ending digest, commands, outcomes, and residual integration obligations.
- [ ] H2 Confirm no prohibited action, second-file edit, successor work, external mutation, or parent communication occurred.
- [ ] H3 Stop at AWAITING_WINDOW_REVIEW.

### 5.15 `KI-W5-S015` — cluster landscape component

```yaml
subwindow_id: KI-W5-S015
type: FILE
parent_window_id: KI-W5
parent_assignment_id: ASG-KI-W5-WA-02
assigned_agent: UNASSIGNED
predecessors: [KI-W5-S014]
successor_reserved_for: WINDOW-AGENT
writable_file: frontend/components/keyword-intelligence/cluster-landscape.tsx
file_operation: CREATE
starting_file_digest: ABSENT
starting_repository_change_set_digest: f1d1d8e1ce5db60be7eca760ae2709954a824897ca40fb5e81ac6b36801a9a8b
read_only_scope:
  - KeywordSearchVolume/dashboard/index.html renderClusters (2585), drawClusterLandscape, and the cluster scene DOM (cluster-landscape, cluster-scene-layout, cluster-scene-legend, cluster-inspector, cluster-view-reset, cluster-zoom-in, cluster-zoom-out, cluster-pill-tooltip)
  - frontend/lib/keyword-intelligence-view-model.ts (accepted S006 output)
authorized_actions:
  - read every file listed in read_only_scope
  - create exactly writable_file per I-F14 ClusterLandscape
  - run the exact LOCAL_NOW checks of this block
  - report the exact handoff to the window agent
prohibited_actions: [the KI-W5-S001 list; additionally no WebGL]
may_start_successor: false
```

Mechanical trace: `REQ-KI-014`; `DEC-KI-023`; `KI-W5-T3` landscape item;
exercised by `W5-B07`, `W5-R05/R06`.

Exact transformation:

1. Create the component per I-F14: a canvas 2D landscape with the ported
   isometric projection, depth-sorted cluster pillars (radius/color scales
   verbatim), pointer events keyed by `pointerId` (drag; two-pointer
   pinch), wheel zoom, double-click reset, zoom in/out buttons, hit test
   on pointerup selecting `clusterId`, hover tooltip and pill tooltip, the
   inspector panel for the selected cluster, the legend scroll area, the
   cluster count line, and the empty state when zero rows; DPR-aware
   canvas sizing via `devicePixelRatio` with a resize observer; selection
   emits `onSelect(clusterId | null)`; no Chart instance; all listeners
   removed on unmount; a zero-size canvas renders the defined empty
   state.

Exact checks: C1–C4 common; C5
`grep -c "addEventListener" components/keyword-intelligence/cluster-landscape.tsx`
→ ≥ `4` and
`grep -c "removeEventListener" components/keyword-intelligence/cluster-landscape.tsx`
→ ≥ `4`. Coverage: zero local case IDs. Expected write set: this file
only.

Completion checklist (sub-window standard §7.5):

- [ ] P1 Revisions, assignment identity, writable file, baseline digest, and predecessor evidence match.
- [ ] P2 Starting repository status and protected dirty changes match the recorded baseline.
- [ ] T1 Apply every ordered transformation and no other edit to the writable file.
- [ ] V1 Run every LOCAL_NOW check and record its activation witnesses and exact assertions.
- [ ] V2 Prove the attributable workspace changed-file set is exactly the writable file.
- [ ] V3 Prove required local coverage IDs equal registered and executed local IDs with zero skips.
- [ ] H1 Return the exact diff, ending digest, commands, outcomes, and residual integration obligations.
- [ ] H2 Confirm no prohibited action, second-file edit, successor work, external mutation, or parent communication occurred.
- [ ] H3 Stop at AWAITING_WINDOW_REVIEW.

### 5.16 `KI-W5-S016` — research dashboard orchestrator

```yaml
subwindow_id: KI-W5-S016
type: FILE
parent_window_id: KI-W5
parent_assignment_id: ASG-KI-W5-WA-02
assigned_agent: UNASSIGNED
predecessors: [KI-W5-S015]
successor_reserved_for: WINDOW-AGENT
writable_file: frontend/components/keyword-intelligence/research-dashboard.tsx
file_operation: CREATE
starting_file_digest: ABSENT
starting_repository_change_set_digest: f1d1d8e1ce5db60be7eca760ae2709954a824897ca40fb5e81ac6b36801a9a8b
read_only_scope:
  - the accepted S008-S015 component outputs and S005/S006 lib outputs
  - KeywordSearchVolume/dashboard/index.html renderAll, changeMarket, applySavedTheme/toggleTheme, exportCSV click
  - frontend/components/run-workspace.tsx (existing orchestrator pattern)
authorized_actions:
  - read every file listed in read_only_scope
  - create exactly writable_file per I-F14 ResearchDashboard
  - run the exact LOCAL_NOW checks of this block
  - report the exact handoff to the window agent
prohibited_actions: [the KI-W5-S001 list]
may_start_successor: false
```

Mechanical trace: `REQ-KI-002/005/006/007/008/009/014/015/018`;
`DEC-KI-013/014/015/017/019/023`; `KI-W5-T1` items 6-10 and `KI-W5-T2`
items 6-12; exercised by all B/R cases.

Exact transformation:

1. Create the orchestrator per I-F14 with state `{ view, draft, filter,
   theme, saving, staleConflict, finalizeState }`; the initial load runs
   once per mount (`getKeywordResearch`); `ResearchStatus` renders while
   non-terminal with `onTerminal` switching to the dashboard; a failed
   terminal renders the safe error surface with retry (GET only);
   completed renders the full composition (FilterBar, SummaryCards,
   KeywordTable, SelectionReview, ChartPanels, ClusterLandscape) with
   `useMemo` wiring of the I-F12 selectors.
2. Save flow: `saveKeywordResearch` selection per I-F14; success applies
   the returned `selection`/`selectionRevision` only after backend
   success; 409 `KEYWORD_SELECTION_REVISION_CONFLICT` sets
   `staleConflict` requiring an explicit reload
   (`getKeywordResearch`) before the next save — a stale response never
   silently overwrites the local display.
3. Finalize flow: `clientRequestId` generated once per click
   (`newClientRequestId()`) and retained in a ref until the response;
   double-click disabled; success navigates via `router.push(run.statusUrl)`;
   an idempotent duplicate click reuses the same id.
4. Market switch changes `filter.market` only (selection invariant);
   projection flows through the selectors; the theme toggle writes only
   the I-F12 key; the export anchor is built from `buildExportQuery(filter)`.
5. Each composed surface carries `data-surface="<inventory id>"` matching
   I-F15.

Exact checks: C1–C4 common; C5
`grep -c "localStorage" components/keyword-intelligence/research-dashboard.tsx`
→ ≥ `1` with
`grep -c "KEYWORD_THEME_STORAGE_KEY" components/keyword-intelligence/research-dashboard.tsx`
→ ≥ `1` (the only storage use) and
`grep -c "newClientRequestId" components/keyword-intelligence/research-dashboard.tsx`
→ ≥ `1`. Coverage: zero local case IDs. Expected write set: this file
only.

Completion checklist (sub-window standard §7.5):

- [ ] P1 Revisions, assignment identity, writable file, baseline digest, and predecessor evidence match.
- [ ] P2 Starting repository status and protected dirty changes match the recorded baseline.
- [ ] T1 Apply every ordered transformation and no other edit to the writable file.
- [ ] V1 Run every LOCAL_NOW check and record its activation witnesses and exact assertions.
- [ ] V2 Prove the attributable workspace changed-file set is exactly the writable file.
- [ ] V3 Prove required local coverage IDs equal registered and executed local IDs with zero skips.
- [ ] H1 Return the exact diff, ending digest, commands, outcomes, and residual integration obligations.
- [ ] H2 Confirm no prohibited action, second-file edit, successor work, external mutation, or parent communication occurred.
- [ ] H3 Stop at AWAITING_WINDOW_REVIEW.

### 5.17 `KI-W5-S017` — create research route

```yaml
subwindow_id: KI-W5-S017
type: FILE
parent_window_id: KI-W5
parent_assignment_id: ASG-KI-W5-WA-02
assigned_agent: UNASSIGNED
predecessors: [KI-W5-S016]
successor_reserved_for: WINDOW-AGENT
writable_file: frontend/app/api/keyword-research/route.ts
file_operation: CREATE
starting_file_digest: ABSENT
starting_repository_change_set_digest: f1d1d8e1ce5db60be7eca760ae2709954a824897ca40fb5e81ac6b36801a9a8b
read_only_scope:
  - frontend/app/api/runs/route.ts (POST pattern: content-type, size, JSON, auth ordering)
  - frontend/lib/backend-proxy.ts, frontend/lib/auth/route.ts, frontend/lib/keyword-intelligence-validation.ts
  - node_modules/next/dist/docs/01-app/03-api-reference/03-file-conventions/route.md
authorized_actions:
  - read every file listed in read_only_scope
  - create exactly writable_file per I-F6
  - run the exact LOCAL_NOW checks of this block
  - report the exact handoff to the window agent
prohibited_actions: [the KI-W5-S001 list]
may_start_successor: false
```

Mechanical trace: `REQ-KI-001/002`; `DEC-KI-019` POST clause; `KI-W5-T1`
operations item (browser→Next proxy→backend); exercised by `W5-A01/A02`
(validator), `W5-R07` (401/no-store probes).

Exact transformation:

1. Create the route per I-F6 with the exact guard order: content-type →
   size → JSON parse → `validateSeedsInput` → `authenticatedRoute` →
   `proxyBackend` POST with the re-serialized validated body
   `JSON.stringify({ seeds })`.

Exact checks: C1–C4 common; C5
`grep -c "export async function POST\|export async function GET" app/api/keyword-research/route.ts`
→ exactly `1` (POST). Coverage: zero local case IDs. Expected write set:
this file only (plus directory).

Completion checklist (sub-window standard §7.5):

- [ ] P1 Revisions, assignment identity, writable file, baseline digest, and predecessor evidence match.
- [ ] P2 Starting repository status and protected dirty changes match the recorded baseline.
- [ ] T1 Apply every ordered transformation and no other edit to the writable file.
- [ ] V1 Run every LOCAL_NOW check and record its activation witnesses and exact assertions.
- [ ] V2 Prove the attributable workspace changed-file set is exactly the writable file.
- [ ] V3 Prove required local coverage IDs equal registered and executed local IDs with zero skips.
- [ ] H1 Return the exact diff, ending digest, commands, outcomes, and residual integration obligations.
- [ ] H2 Confirm no prohibited action, second-file edit, successor work, external mutation, or parent communication occurred.
- [ ] H3 Stop at AWAITING_WINDOW_REVIEW.

### 5.18 `KI-W5-S018` — get research route

```yaml
subwindow_id: KI-W5-S018
type: FILE
parent_window_id: KI-W5
parent_assignment_id: ASG-KI-W5-WA-02
assigned_agent: UNASSIGNED
predecessors: [KI-W5-S017]
successor_reserved_for: WINDOW-AGENT
writable_file: frontend/app/api/keyword-research/[researchId]/route.ts
file_operation: CREATE
starting_file_digest: ABSENT
starting_repository_change_set_digest: f1d1d8e1ce5db60be7eca760ae2709954a824897ca40fb5e81ac6b36801a9a8b
read_only_scope:
  - frontend/app/api/runs/[runId]/route.ts (dynamic route pattern)
  - frontend/lib/backend-proxy.ts, frontend/lib/auth/route.ts, frontend/lib/keyword-intelligence-validation.ts
  - node_modules/next/dist/docs/01-app/03-api-reference/03-file-conventions/route.md and .../dynamic-routes.md
authorized_actions:
  - read every file listed in read_only_scope
  - create exactly writable_file per I-F7
  - run the exact LOCAL_NOW checks of this block
  - report the exact handoff to the window agent
prohibited_actions: [the KI-W5-S001 list]
may_start_successor: false
```

Mechanical trace: `REQ-KI-002/005`; `DEC-KI-019` GET clause; exercised by
`W5-A04` (pattern), `W5-R02/R04/R07`.

Exact transformation:

1. Create the route per I-F7 mirroring `runs/[runId]/route.ts` exactly
   (authenticatedRoute → awaited params → `validKeywordResearchId` guard →
   `proxyBackend` GET with `encodeURIComponent`).

Exact checks: C1–C4 common; C5
`grep -c "validKeywordResearchId" "app/api/keyword-research/[researchId]/route.ts"`
→ ≥ `1`. Coverage: zero local case IDs. Expected write set: this file
only.

Completion checklist (sub-window standard §7.5):

- [ ] P1 Revisions, assignment identity, writable file, baseline digest, and predecessor evidence match.
- [ ] P2 Starting repository status and protected dirty changes match the recorded baseline.
- [ ] T1 Apply every ordered transformation and no other edit to the writable file.
- [ ] V1 Run every LOCAL_NOW check and record its activation witnesses and exact assertions.
- [ ] V2 Prove the attributable workspace changed-file set is exactly the writable file.
- [ ] V3 Prove required local coverage IDs equal registered and executed local IDs with zero skips.
- [ ] H1 Return the exact diff, ending digest, commands, outcomes, and residual integration obligations.
- [ ] H2 Confirm no prohibited action, second-file edit, successor work, external mutation, or parent communication occurred.
- [ ] H3 Stop at AWAITING_WINDOW_REVIEW.

### 5.19 `KI-W5-S019` — save selection route

```yaml
subwindow_id: KI-W5-S019
type: FILE
parent_window_id: KI-W5
parent_assignment_id: ASG-KI-W5-WA-02
assigned_agent: UNASSIGNED
predecessors: [KI-W5-S018]
successor_reserved_for: WINDOW-AGENT
writable_file: frontend/app/api/keyword-research/[researchId]/selection/route.ts
file_operation: CREATE
starting_file_digest: ABSENT
starting_repository_change_set_digest: f1d1d8e1ce5db60be7eca760ae2709954a824897ca40fb5e81ac6b36801a9a8b
read_only_scope:
  - frontend/app/api/runs/route.ts (body guard pattern)
  - frontend/lib/backend-proxy.ts, frontend/lib/auth/route.ts, frontend/lib/keyword-intelligence-validation.ts
authorized_actions:
  - read every file listed in read_only_scope
  - create exactly writable_file per I-F8
  - run the exact LOCAL_NOW checks of this block
  - report the exact handoff to the window agent
prohibited_actions: [the KI-W5-S001 list]
may_start_successor: false
```

Mechanical trace: `REQ-KI-007/008`; `DEC-KI-014/019` PUT clause
(`expectedRevision` CAS); exercised by `W5-R03`, `W5-R07`.

Exact transformation:

1. Create the route per I-F8: content-type/size(262144)/JSON guards, the
   exact key-set + `expectedRevision` safe-integer ≥ 1 + `items` array ≤
   200 structural validation (400 `KEYWORD_SELECTION_INPUT_INVALID`
   otherwise; item-internal shape remains backend-authoritative), the
   param guard, then `proxyBackend` PUT forwarding the original body
   string verbatim.

Exact checks: C1–C4 common; C5
`grep -c "262144\|expectedRevision" "app/api/keyword-research/[researchId]/selection/route.ts"`
→ ≥ `2`. Coverage: zero local case IDs. Expected write set: this file
only.

Completion checklist (sub-window standard §7.5):

- [ ] P1 Revisions, assignment identity, writable file, baseline digest, and predecessor evidence match.
- [ ] P2 Starting repository status and protected dirty changes match the recorded baseline.
- [ ] T1 Apply every ordered transformation and no other edit to the writable file.
- [ ] V1 Run every LOCAL_NOW check and record its activation witnesses and exact assertions.
- [ ] V2 Prove the attributable workspace changed-file set is exactly the writable file.
- [ ] V3 Prove required local coverage IDs equal registered and executed local IDs with zero skips.
- [ ] H1 Return the exact diff, ending digest, commands, outcomes, and residual integration obligations.
- [ ] H2 Confirm no prohibited action, second-file edit, successor work, external mutation, or parent communication occurred.
- [ ] H3 Stop at AWAITING_WINDOW_REVIEW.

### 5.20 `KI-W5-S020` — create run route

```yaml
subwindow_id: KI-W5-S020
type: FILE
parent_window_id: KI-W5
parent_assignment_id: ASG-KI-W5-WA-02
assigned_agent: UNASSIGNED
predecessors: [KI-W5-S019]
successor_reserved_for: WINDOW-AGENT
writable_file: frontend/app/api/keyword-research/[researchId]/runs/route.ts
file_operation: CREATE
starting_file_digest: ABSENT
starting_repository_change_set_digest: f1d1d8e1ce5db60be7eca760ae2709954a824897ca40fb5e81ac6b36801a9a8b
read_only_scope:
  - frontend/app/api/runs/route.ts (POST pattern)
  - frontend/lib/backend-proxy.ts, frontend/lib/auth/route.ts, frontend/lib/keyword-intelligence-validation.ts
authorized_actions:
  - read every file listed in read_only_scope
  - create exactly writable_file per I-F9
  - run the exact LOCAL_NOW checks of this block
  - report the exact handoff to the window agent
prohibited_actions: [the KI-W5-S001 list]
may_start_successor: false
```

Mechanical trace: `REQ-KI-015/016`; `DEC-KI-017/019` runs clause;
exercised by `W5-R03` (duplicate-click idempotence in the S027 request
log).

Exact transformation:

1. Create the route per I-F9: content-type/size(4096)/JSON guards, the
   exact key-set + `expectedSelectionRevision` safe-integer ≥ 1 +
   `clientRequestId` matching `CLIENT_REQUEST_ID_PATTERN` (400
   `KEYWORD_RUN_INPUT_INVALID` otherwise), the param guard, `proxyBackend`
   POST forwarding the body verbatim.

Exact checks: C1–C4 common; C5
`grep -c "CLIENT_REQUEST_ID_PATTERN" "app/api/keyword-research/[researchId]/runs/route.ts"`
→ ≥ `1`. Coverage: zero local case IDs. Expected write set: this file
only.

Completion checklist (sub-window standard §7.5):

- [ ] P1 Revisions, assignment identity, writable file, baseline digest, and predecessor evidence match.
- [ ] P2 Starting repository status and protected dirty changes match the recorded baseline.
- [ ] T1 Apply every ordered transformation and no other edit to the writable file.
- [ ] V1 Run every LOCAL_NOW check and record its activation witnesses and exact assertions.
- [ ] V2 Prove the attributable workspace changed-file set is exactly the writable file.
- [ ] V3 Prove required local coverage IDs equal registered and executed local IDs with zero skips.
- [ ] H1 Return the exact diff, ending digest, commands, outcomes, and residual integration obligations.
- [ ] H2 Confirm no prohibited action, second-file edit, successor work, external mutation, or parent communication occurred.
- [ ] H3 Stop at AWAITING_WINDOW_REVIEW.

### 5.21 `KI-W5-S021` — export CSV route

```yaml
subwindow_id: KI-W5-S021
type: FILE
parent_window_id: KI-W5
parent_assignment_id: ASG-KI-W5-WA-02
assigned_agent: UNASSIGNED
predecessors: [KI-W5-S020]
successor_reserved_for: WINDOW-AGENT
writable_file: frontend/app/api/keyword-research/[researchId]/export.csv/route.ts
file_operation: CREATE
starting_file_digest: ABSENT
starting_repository_change_set_digest: f1d1d8e1ce5db60be7eca760ae2709954a824897ca40fb5e81ac6b36801a9a8b
read_only_scope:
  - frontend/lib/backend-proxy.ts (env validation semantics lines 28-38; error envelope style)
  - frontend/lib/auth/route.ts, frontend/lib/keyword-intelligence-validation.ts
  - KEYWORD_INTELLIGENCE_DECISION_LEDGER.md lines 420-427 (DEC-KI-019 export clause)
authorized_actions:
  - read every file listed in read_only_scope
  - create exactly writable_file per I-F10
  - run the exact LOCAL_NOW checks of this block
  - report the exact handoff to the window agent
prohibited_actions: [the KI-W5-S001 list]
may_start_successor: false
```

Mechanical trace: `REQ-KI-018`; `DEC-KI-019` export clause; `KI-W5-T1`
operations item ("export streams proxy response"); exercised by `W5-B05`,
`W5-NC08/NC11`, `W5-R07`.

Exact transformation:

1. Create the route per I-F10: the route-local backend fetch (never
   `proxyBackend`), the exact query allowlist/validation table, the param
   guard, `authenticatedRoute`, the timeout/availability/configuration
   error envelopes, and the CSV header passthrough with `no-store`.
2. Forbidden: parsing CSV content, logging body content, adding query
   keys, buffering beyond the single text read.

Exact checks: C1–C4 common; C5
`grep -c "proxyBackend" "app/api/keyword-research/[researchId]/export.csv/route.ts"`
→ `0` and
`grep -c "text/csv" "app/api/keyword-research/[researchId]/export.csv/route.ts"`
→ ≥ `1`. Coverage: zero local case IDs. Expected write set: this file
only.

Completion checklist (sub-window standard §7.5):

- [ ] P1 Revisions, assignment identity, writable file, baseline digest, and predecessor evidence match.
- [ ] P2 Starting repository status and protected dirty changes match the recorded baseline.
- [ ] T1 Apply every ordered transformation and no other edit to the writable file.
- [ ] V1 Run every LOCAL_NOW check and record its activation witnesses and exact assertions.
- [ ] V2 Prove the attributable workspace changed-file set is exactly the writable file.
- [ ] V3 Prove required local coverage IDs equal registered and executed local IDs with zero skips.
- [ ] H1 Return the exact diff, ending digest, commands, outcomes, and residual integration obligations.
- [ ] H2 Confirm no prohibited action, second-file edit, successor work, external mutation, or parent communication occurred.
- [ ] H3 Stop at AWAITING_WINDOW_REVIEW.

### 5.22 `KI-W5-S022` — keywords landing page

```yaml
subwindow_id: KI-W5-S022
type: FILE
parent_window_id: KI-W5
parent_assignment_id: ASG-KI-W5-WA-02
assigned_agent: UNASSIGNED
predecessors: [KI-W5-S021]
successor_reserved_for: WINDOW-AGENT
writable_file: frontend/app/keywords/page.tsx
file_operation: CREATE
starting_file_digest: ABSENT
starting_repository_change_set_digest: f1d1d8e1ce5db60be7eca760ae2709954a824897ca40fb5e81ac6b36801a9a8b
read_only_scope:
  - frontend/app/runs/page.tsx (shell pattern)
  - frontend/components/keyword-intelligence/research-form.tsx (accepted S008 output)
  - node_modules/next/dist/docs/01-app/03-api-reference/03-file-conventions/page.md
authorized_actions:
  - read every file listed in read_only_scope
  - create exactly writable_file per I-F11
  - run the exact LOCAL_NOW checks of this block
  - report the exact handoff to the window agent
prohibited_actions: [the KI-W5-S001 list]
may_start_successor: false
```

Mechanical trace: `REQ-KI-001`; `KI-W5-T1` server page item; exercised by
`W5-B01`.

Exact transformation:

1. Create the server page per I-F11: `metadata`, `force-dynamic`, the
   `app-canvas`/`shell` markup with an eyebrow, `h1` "Keyword research",
   a lede sentence, and `<ResearchForm />` (no `onCreated` — the
   component's built-in default navigates per I-F14).

Exact checks: C1–C4 common; C5
`grep -c "force-dynamic" app/keywords/page.tsx` → `1` and
`grep -c "use client" app/keywords/page.tsx` → `0`. Coverage: zero local
case IDs. Expected write set: this file only.

Completion checklist (sub-window standard §7.5):

- [ ] P1 Revisions, assignment identity, writable file, baseline digest, and predecessor evidence match.
- [ ] P2 Starting repository status and protected dirty changes match the recorded baseline.
- [ ] T1 Apply every ordered transformation and no other edit to the writable file.
- [ ] V1 Run every LOCAL_NOW check and record its activation witnesses and exact assertions.
- [ ] V2 Prove the attributable workspace changed-file set is exactly the writable file.
- [ ] V3 Prove required local coverage IDs equal registered and executed local IDs with zero skips.
- [ ] H1 Return the exact diff, ending digest, commands, outcomes, and residual integration obligations.
- [ ] H2 Confirm no prohibited action, second-file edit, successor work, external mutation, or parent communication occurred.
- [ ] H3 Stop at AWAITING_WINDOW_REVIEW.

### 5.23 `KI-W5-S023` — research dashboard page

```yaml
subwindow_id: KI-W5-S023
type: FILE
parent_window_id: KI-W5
parent_assignment_id: ASG-KI-W5-WA-02
assigned_agent: UNASSIGNED
predecessors: [KI-W5-S022]
successor_reserved_for: WINDOW-AGENT
writable_file: frontend/app/keywords/[researchId]/page.tsx
file_operation: CREATE
starting_file_digest: ABSENT
starting_repository_change_set_digest: f1d1d8e1ce5db60be7eca760ae2709954a824897ca40fb5e81ac6b36801a9a8b
read_only_scope:
  - frontend/app/runs/page.tsx (shell pattern)
  - frontend/components/keyword-intelligence/research-dashboard.tsx (accepted S016 output)
  - node_modules/next/dist/docs/01-app/03-api-reference/03-file-conventions/page.md and .../dynamic-routes.md
authorized_actions:
  - read every file listed in read_only_scope
  - create exactly writable_file per I-F11
  - run the exact LOCAL_NOW checks of this block
  - report the exact handoff to the window agent
prohibited_actions: [the KI-W5-S001 list]
may_start_successor: false
```

Mechanical trace: `REQ-KI-002/014`; `KI-W5-T1` server page item; exercised
by all B/R cases.

Exact transformation:

1. Create the server page per I-F11 with
   `PageProps<"/keywords/[researchId]">`, `const { researchId } = await
   params;`, rendering `<ResearchDashboard researchId={researchId} />`
   inside the standard shell.

Exact checks: C1–C4 common; C5
`grep -c "await params" "app/keywords/[researchId]/page.tsx"` → `1`.
Coverage: zero local case IDs. Expected write set: this file only.

Completion checklist (sub-window standard §7.5):

- [ ] P1 Revisions, assignment identity, writable file, baseline digest, and predecessor evidence match.
- [ ] P2 Starting repository status and protected dirty changes match the recorded baseline.
- [ ] T1 Apply every ordered transformation and no other edit to the writable file.
- [ ] V1 Run every LOCAL_NOW check and record its activation witnesses and exact assertions.
- [ ] V2 Prove the attributable workspace changed-file set is exactly the writable file.
- [ ] V3 Prove required local coverage IDs equal registered and executed local IDs with zero skips.
- [ ] H1 Return the exact diff, ending digest, commands, outcomes, and residual integration obligations.
- [ ] H2 Confirm no prohibited action, second-file edit, successor work, external mutation, or parent communication occurred.
- [ ] H3 Stop at AWAITING_WINDOW_REVIEW.

### 5.24 `KI-W5-S024` — API/parser test file

```yaml
subwindow_id: KI-W5-S024
type: FILE
parent_window_id: KI-W5
parent_assignment_id: ASG-KI-W5-WA-02
assigned_agent: UNASSIGNED
predecessors: [KI-W5-S023]
successor_reserved_for: WINDOW-AGENT
writable_file: frontend/test/keyword-intelligence-api.test.ts
file_operation: CREATE
starting_file_digest: ABSENT
starting_repository_change_set_digest: f1d1d8e1ce5db60be7eca760ae2709954a824897ca40fb5e81ac6b36801a9a8b
read_only_scope:
  - frontend/lib/keyword-intelligence-validation.ts, frontend/lib/keyword-intelligence-view-model.ts (accepted outputs)
  - frontend/test/api-validation.test.ts and frontend/test/query-treemap.test.ts (test style)
  - KEYWORD_INTELLIGENCE_KI_W5_SUBWINDOW_CHECKLIST.md sections 3 and 6 (this document)
authorized_actions:
  - read every file listed in read_only_scope
  - create exactly writable_file registering and executing W5-A01 through W5-A10
  - run the exact LOCAL_NOW checks of this block
  - report the exact handoff to the window agent
prohibited_actions: [the KI-W5-S001 list]
may_start_successor: false
```

Mechanical trace: `KI-W5-T1` item 13 (strict parser payload cases; negative
control bypasses parser); allocates `W5-A01`–`W5-A10` and controls
`W5-NC01/NC07/NC12` (§6.2).

Exact transformation:

1. Create the Node test file in the existing style (`node:test` +
   `node:assert/strict`, relative `.ts` imports) with ten named subtests
   `W5-A01`–`W5-A10` covering exactly the §6.1 W5-A definitions, plus the
   three controls executed as mutation-style assertions (defective copy →
   oracle throws → fresh copy passes).
2. A local literal fixture builder assembles a minimal valid
   `ResearchView` (the nine-market code set, ≥1 keyword/cluster rows,
   15-point histories, one conflict fixture) reused by subtests.
3. Emit exactly one `KI_W5_EXECUTION_CERTIFICATE=` TAP diagnostic line per
   I-F18 with `required = registered = executed =` the ten IDs and the
   §3.1 digests.

Exact checks: C1–C4 common; C5
`node --experimental-strip-types --test test/keyword-intelligence-api.test.ts`
→ all pass, 0 skipped, the certificate line present with
`requiredDigest == registeredDigest == executedDigest`. Expected write
set: this file only.

Completion checklist (sub-window standard §7.5):

- [ ] P1 Revisions, assignment identity, writable file, baseline digest, and predecessor evidence match.
- [ ] P2 Starting repository status and protected dirty changes match the recorded baseline.
- [ ] T1 Apply every ordered transformation and no other edit to the writable file.
- [ ] V1 Run every LOCAL_NOW check and record its activation witnesses and exact assertions.
- [ ] V2 Prove the attributable workspace changed-file set is exactly the writable file.
- [ ] V3 Prove required local coverage IDs equal registered and executed local IDs with zero skips.
- [ ] H1 Return the exact diff, ending digest, commands, outcomes, and residual integration obligations.
- [ ] H2 Confirm no prohibited action, second-file edit, successor work, external mutation, or parent communication occurred.
- [ ] H3 Stop at AWAITING_WINDOW_REVIEW.

### 5.25 `KI-W5-S025` — components/view-model test file

```yaml
subwindow_id: KI-W5-S025
type: FILE
parent_window_id: KI-W5
parent_assignment_id: ASG-KI-W5-WA-02
assigned_agent: UNASSIGNED
predecessors: [KI-W5-S024]
successor_reserved_for: WINDOW-AGENT
writable_file: frontend/test/keyword-intelligence-components.test.ts
file_operation: CREATE
starting_file_digest: ABSENT
starting_repository_change_set_digest: f1d1d8e1ce5db60be7eca760ae2709954a824897ca40fb5e81ac6b36801a9a8b
read_only_scope:
  - frontend/lib/keyword-intelligence-view-model.ts (accepted S006 output)
  - KeywordSearchVolume/dashboard/index.html (parity anchors for expected values)
  - frontend/test/query-treemap.test.ts (style)
  - KEYWORD_INTELLIGENCE_KI_W5_SUBWINDOW_CHECKLIST.md sections 3 and 6
authorized_actions:
  - read every file listed in read_only_scope
  - create exactly writable_file registering and executing W5-C01 through W5-C12
  - run the exact LOCAL_NOW checks of this block
  - report the exact handoff to the window agent
prohibited_actions: [the KI-W5-S001 list]
may_start_successor: false
```

Mechanical trace: `KI-W5-T2` item 13 (component/runtime tests for every
surface/control/filter/sort/selection/edit/pagination/theme/export) — the
React render surface itself is verified in S027 real Chrome; this file
owns the pure-logic oracle layer feeding those surfaces (recorded as the
test-substitute fidelity note for parent review); allocates
`W5-C01`–`W5-C12` and controls `W5-NC02/NC09` (§6.2).

Exact transformation:

1. Twelve named subtests `W5-C01`–`W5-C12` per §6.1: expected values are
   literal numbers/arrays transcribed from the standalone dashboard's
   behavior on a fixed fixture (the S024 builder style, extended to
   multiple markets/lanes/flags); the 200-row scale case (`W5-C12`)
   builds 200 distinct rows plus 200 draft items and asserts
   filter/sort/aggregate completeness and the page-size ceilings.
2. Controls: the per-market-selection mutation (market switch changes the
   selection → the invariant oracle fails) and the stale-overwrite
   mutation (last-write-wins overwrites → the stale-guard oracle fails).
3. One `KI_W5_EXECUTION_CERTIFICATE=` line per I-F18 over the twelve IDs.

Exact checks: C1–C4 common; C5
`node --experimental-strip-types --test test/keyword-intelligence-components.test.ts`
→ all pass + certificate equality. Expected write set: this file only.

Completion checklist (sub-window standard §7.5):

- [ ] P1 Revisions, assignment identity, writable file, baseline digest, and predecessor evidence match.
- [ ] P2 Starting repository status and protected dirty changes match the recorded baseline.
- [ ] T1 Apply every ordered transformation and no other edit to the writable file.
- [ ] V1 Run every LOCAL_NOW check and record its activation witnesses and exact assertions.
- [ ] V2 Prove the attributable workspace changed-file set is exactly the writable file.
- [ ] V3 Prove required local coverage IDs equal registered and executed local IDs with zero skips.
- [ ] H1 Return the exact diff, ending digest, commands, outcomes, and residual integration obligations.
- [ ] H2 Confirm no prohibited action, second-file edit, successor work, external mutation, or parent communication occurred.
- [ ] H3 Stop at AWAITING_WINDOW_REVIEW.

### 5.26 `KI-W5-S026` — inventory test file

```yaml
subwindow_id: KI-W5-S026
type: FILE
parent_window_id: KI-W5
parent_assignment_id: ASG-KI-W5-WA-02
assigned_agent: UNASSIGNED
predecessors: [KI-W5-S025]
successor_reserved_for: WINDOW-AGENT
writable_file: frontend/test/keyword-intelligence-inventory.test.ts
file_operation: CREATE
starting_file_digest: ABSENT
starting_repository_change_set_digest: f1d1d8e1ce5db60be7eca760ae2709954a824897ca40fb5e81ac6b36801a9a8b
read_only_scope:
  - all accepted lib/component/route/page outputs of S001-S023
  - frontend/package.json
  - KEYWORD_INTELLIGENCE_KI_W5_SUBWINDOW_CHECKLIST.md sections 2, 3, 6
authorized_actions:
  - read every file listed in read_only_scope
  - create exactly writable_file registering and executing W5-I01 through W5-I06
  - run the exact LOCAL_NOW checks of this block
  - report the exact handoff to the window agent
prohibited_actions: [the KI-W5-S001 list]
may_start_successor: false
```

Mechanical trace: `SCN-KI-016` negative control ("remove each surface
registration; inventory set equality fails"); `KI-W5-T3` item 13;
allocates `W5-I01`–`W5-I06` and controls `W5-NC03/NC04/NC06/NC10/NC12`
(§6.2).

Exact transformation:

1. Six named subtests per §6.1: exact export-surface equality for the
   three lib modules (`Object.keys(await import(...)).sort()` deep-equal
   literal arrays); recursive file-listing equality for the exact owned
   paths under `app/keywords/`, `app/api/keyword-research/`, and
   `components/keyword-intelligence/` (no extra file);
   `KEYWORD_INTELLIGENCE_SURFACE_INVENTORY` deep-equal the I-F15 literal;
   `data-surface`/`data-filter` registration greps over the component
   sources covering every inventory id; chart dependency assertions
   (chart.js version `"3.9.1"`, chartjs-chart-treemap `"2.0.0"`, read
   from `node_modules/*/package.json`) plus the no-CDN grep over all
   owned sources.
2. Controls: remove-one-registration equality failure; injected
   extra-path set failure; wrong-version literal failure; CDN-string
   injection failure; parser unknown-key weakening failure.
3. One `KI_W5_EXECUTION_CERTIFICATE=` line per I-F18 over the six IDs.

Exact checks: C1–C4 common; C5
`node --experimental-strip-types --test test/keyword-intelligence-inventory.test.ts`
→ all pass + certificate equality. Expected write set: this file only.

Completion checklist (sub-window standard §7.5):

- [ ] P1 Revisions, assignment identity, writable file, baseline digest, and predecessor evidence match.
- [ ] P2 Starting repository status and protected dirty changes match the recorded baseline.
- [ ] T1 Apply every ordered transformation and no other edit to the writable file.
- [ ] V1 Run every LOCAL_NOW check and record its activation witnesses and exact assertions.
- [ ] V2 Prove the attributable workspace changed-file set is exactly the writable file.
- [ ] V3 Prove required local coverage IDs equal registered and executed local IDs with zero skips.
- [ ] H1 Return the exact diff, ending digest, commands, outcomes, and residual integration obligations.
- [ ] H2 Confirm no prohibited action, second-file edit, successor work, external mutation, or parent communication occurred.
- [ ] H3 Stop at AWAITING_WINDOW_REVIEW.

### 5.27 `KI-W5-S027` — browser CDP harness

```yaml
subwindow_id: KI-W5-S027
type: FILE
parent_window_id: KI-W5
parent_assignment_id: ASG-KI-W5-WA-02
assigned_agent: UNASSIGNED
predecessors: [KI-W5-S026]
successor_reserved_for: WINDOW-AGENT
writable_file: frontend/test/browser/keyword-intelligence-dashboard.mjs
file_operation: CREATE
starting_file_digest: ABSENT
starting_repository_change_set_digest: f1d1d8e1ce5db60be7eca760ae2709954a824897ca40fb5e81ac6b36801a9a8b
read_only_scope:
  - frontend/scripts/g-r1-real-component-browser.mjs (Cdp class 183-201, fixtureInjection 135-181, spawn, capture patterns)
  - all accepted S001-S026 outputs
  - KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md lines 2959-2991 (SCN-KI-016/017)
authorized_actions:
  - read every file listed in read_only_scope
  - create exactly writable_file per the harness contract below
  - run the exact LOCAL_NOW checks of this block (node --check only; execution is I001-owned)
  - report the exact handoff to the window agent
prohibited_actions: [the KI-W5-S001 list; additionally no next build/dev/start execution at leaf level]
may_start_successor: false
```

Mechanical trace: `SCN-KI-016/017`; the `KI-W5-V1/V2/V3/V4` executor;
allocates `W5-B01`–`W5-B08` and `W5-R01`–`W5-R07` plus browser controls
`W5-NC05/NC11` (§6.2).

Exact transformation:

1. Create the harness (plain `.mjs`, Node ≥22 globals, the `Cdp` class
   copied from `g-r1-real-component-browser.mjs:183-201`), in five
   phases:
   - Phase A (build/start; I001 invocation only): spawn
     `next build` then `next start --hostname 127.0.0.1 --port 4347`,
     awaiting readiness; the script refuses to run when
     `process.env.KI_W5_SKIP_BUILD` is unset.
   - Phase B (fixture): build the fixture payloads in-file (queued,
     running ×3 stage views, completed, failed `ResearchView`s plus
     selection/runs/export responses) and validate each through
     `parseResearchEnvelope` (imported from
     `../../lib/keyword-intelligence-validation.ts` via strip-types)
     before injection.
   - Phase C (interception): `Page.addScriptToEvaluateOnNewDocument`
     installing a `window.fetch` wrapper for same-origin
     `/api/keyword-research*` requests serving the deterministic payloads,
     recording every request into `globalThis.__kiFixture.requests`
     (method, URL, body digest, `clientRequestId` when present),
     sequencing queued→running→completed per poll count, and serving the
     409 revision-conflict and handoff-conflict variants on demand; any
     non-app URL passes through untouched (and is captured by the network
     allowlist assertion).
   - Phase D (scenarios): the fifteen `W5-B*`/`W5-R*` subtests at
     1440×900 and 390×844 with console/error collection
     (`Runtime.consoleAPICalled`, `Log.entryAdded`,
     `Runtime.exceptionThrown`), a network allowlist (app-origin only,
     zero CDN), canvas and `Chart.getChart` presence, landscape
     transform mutation on drag/zoom, request-log oracles (one save per
     action, GET-only retry, single-poll cadence, idempotent duplicate
     finalize reuse), unauthenticated direct route probes (401 envelope +
     `Cache-Control: no-store` + 400 unknown query key + bad-id 400 +
     generic 404) hitting the real routes without interception, and CSV
     equality of the intercepted export response against
     `EXPORT_CSV_COLUMNS` plus the filtered fixture rows.
   - Phase E (teardown): kill Next, close CDP, remove temp directories in
     `finally`; emit exactly one `KI_W5_BROWSER_CERTIFICATE=` line per
     I-F18.
2. Determinism: fixed port 4347, fixed seeds, fixed date literals;
   screenshots under `review-evidence/keyword-intelligence/KI-W5/`
   (runner output, not a workspace source edit).

Exact checks (`LOCAL_NOW`, from `frontend/`): C1–C4 common; C5
`node --check test/browser/keyword-intelligence-dashboard.mjs` → exit 0.
Coverage: B/R IDs registered in the certificate; execution at I001.
Expected write set: this file only (plus the `test/browser/` directory).

Completion checklist (sub-window standard §7.5):

- [ ] P1 Revisions, assignment identity, writable file, baseline digest, and predecessor evidence match.
- [ ] P2 Starting repository status and protected dirty changes match the recorded baseline.
- [ ] T1 Apply every ordered transformation and no other edit to the writable file.
- [ ] V1 Run every LOCAL_NOW check and record its activation witnesses and exact assertions.
- [ ] V2 Prove the attributable workspace changed-file set is exactly the writable file.
- [ ] V3 Prove required local coverage IDs equal registered and executed local IDs with zero skips.
- [ ] H1 Return the exact diff, ending digest, commands, outcomes, and residual integration obligations.
- [ ] H2 Confirm no prohibited action, second-file edit, successor work, external mutation, or parent communication occurred.
- [ ] H3 Stop at AWAITING_WINDOW_REVIEW.

### 5.28 `KI-W5-I001` — whole-window integration assessment

```yaml
subwindow_id: KI-W5-I001
type: ASSESS
parent_window_id: KI-W5
parent_assignment_id: ASG-KI-W5-WA-02
assigned_agent: KI-W5-WINDOW-AGENT
predecessors: [KI-W5-S027]
successor_reserved_for: WINDOW-AGENT
writable_file: none
file_operation: none
starting_file_digest: N/A
starting_repository_change_set_digest: f1d1d8e1ce5db60be7eca760ae2709954a824897ca40fb5e81ac6b36801a9a8b
read_only_scope:
  - all 27 leaf files plus S1/S2/S3
  - KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md lines 2421-2430 (KI-W5-V1-V4)
authorized_actions:
  - independently review every leaf handoff per sub-window standard section 8
  - execute gates KI-W5-V1 through KI-W5-V4 exactly once each on frozen final inputs
  - append the section 12.4 integration certificate to S3
  - set S2 to READY_FOR_PARENT_REVIEW and produce the section 12.5 handoff
prohibited_actions:
  - any implementation-file write (a diagnosed defect opens KI-W5-C001+)
  - repeating a passed stateful gate without a documented invalidation
  - claiming parent acceptance or beginning KI-W6
may_start_successor: false
```

Frozen gates (A4 lines 2421-2424, executed from `frontend/`):

- **`KI-W5-V1`** `SCN-KI-016` + `SCN-KI-017` once via
  `node test/browser/keyword-intelligence-dashboard.mjs` on the emitted
  production build (the script performs the build itself); all 15 B/R IDs
  pass with activation witnesses; browser certificate equality holds;
  zero console errors; zero non-app network requests. A documented
  sandbox `listen EPERM` failure is rerun with the identical command under
  sandbox approval, never silently accepted.
- **`KI-W5-V2`** `npm run check` once (lint + all tests including the
  three keyword suites with certificate equality + `next build` emitting
  without error); assembled write-set proof: `git -C frontend status
  --porcelain` lists exactly the 27 planned paths and the per-LF
  `LC_ALL=C` set digest equals
  `a04dce13038a3d180ddab0c8412890af065e3f5ab5019540c87a5664485320e6`;
  the root change set equals the §2 inventory plus the three subordinate
  artifacts and nothing else; unrelated dirty files byte-identical.
- **`KI-W5-V3`** inside the V1 run: 200 final keyword rows and 200 draft
  selections rendered and filtered; exactly one poll timer; bounded chart
  instances/listeners; response/page-size ceilings asserted
  (`W5-C12` + `W5-B08` + `W5-R06`).
- **`KI-W5-V4`** auth isolation and privacy: the unauthenticated probes
  (`W5-R07`), no raw fields/CDNs/local result files (network allowlist +
  the `W5-I06` no-CDN grep + no `localStorage` beyond the theme key),
  durable reload (`W5-R02`), accessible error/empty/loading states
  (`W5-C11` + `W5-B01`).
- **`KI-W5-I001-M` (window-agent merge check)** the union of the four
  certificates (three node + one browser) equals the literal 43-ID
  required set with per-LF digest
  `cb8ef6d7cb87b5a451e438d11b0f037c8130f78d0c3e033b1304f78bfa1f6bdb`;
  zero skipped, zero oracle failures, zero duplicates, zero unexpected
  IDs.

Failure handling: any failing gate is diagnosed to exactly one owning
file; the window agent appends a corrective sub-window `KI-W5-C001`,
`KI-W5-C002`, … (single file from the same 27-file set, §12.2 certificate
first) and re-runs only the gates its invalidation rule marks stale
(§9.5, A4 verification economy).

---

## 6. Coverage allocation and accounting

### 6.1 Required case set (43 IDs, zero unallocated)

Global union digest
`cb8ef6d7cb87b5a451e438d11b0f037c8130f78d0c3e033b1304f78bfa1f6bdb`.

| Group | IDs (definitions) | Registered in | Executed in | Gate |
|---|---|---|---|---|
| api/parser | `W5-A01` seeds accept 1/5 boundaries; `W5-A02` seeds reject 0/6/non-array/unknown-key/non-string/empty/>100cp/duplicate; `W5-A03` clientRequestId format + uniqueness; `W5-A04` research-id pattern accept/reject; `W5-A05` envelope deep-equal valid fixture + wrapper unknown-key reject; `W5-A06` view strictness (unknown key, stage enum, StageCounts bounds, result-null rule, selection bounds/enums, conflict shapes, dates, markets, monthlyHistory 15..102); `W5-A07` run-handoff envelope + run-shape reuse; `W5-A08` poll ladder + terminal stop; `W5-A09` selection reducer add/remove/edit/manual + 200 cap + over-100 flag + CAS guard; `W5-A10` conflict gate blocks finalize + canonical suggestion shape | `S024` | `S024` | `KI-W5-V2` (I001 frozen re-run) |
| components/view-model | `W5-C01` activeRows/distinctKeywordRows; `W5-C02` market projection + selection invariant; `W5-C03` cumulativeVolume; `W5-C04` summary/cluster metrics; `W5-C05` every filter dimension + combined; `W5-C06` every sort column + null-last + pagination clamp; `W5-C07` aggregation/adjustedVolume/median/fingerprint/lane; `W5-C08` export query mirror + CSV column parity; `W5-C09` formatters; `W5-C10` theme key/next; `W5-C11` phase machine loading/ready/error/empty; `W5-C12` 200-row/200-draft scale + ceilings | `S025` | `S025` | `KI-W5-V2` |
| inventory | `W5-I01`–`W5-I03` exact lib export surfaces; `W5-I04` owned-path presence set equality; `W5-I05` surface inventory equality + registrations; `W5-I06` chart dependency versions + no-CDN | `S026` | `S026` | `KI-W5-V2` |
| browser SCN-KI-016 | `W5-B01` surfaces present/data-derived + empty/error states; `W5-B02` filters/sort/pagination/page-size; `W5-B03` selection save/conflict/over-100 one-request-per-action; `W5-B04` edit/manual dialog flows; `W5-B05` export CSV equals filtered table; `W5-B06` theme round-trip + single storage key; `W5-B07` canvases nonzero + landscape transform/hit/tooltip/inspector; `W5-B08` zero console errors, zero non-app network, one instance/listener set | `S027` | `S027` (I001 execution) | `KI-W5-V1` |
| browser SCN-KI-017 | `W5-R01` poll lifecycle single timer + ladder + terminal stop; `W5-R02` tab close/remount + durable reload; `W5-R03` stale 409 + no silent overwrite + idempotent finalize; `W5-R04` failed state + GET-only retry; `W5-R05` 1440×900/390×844 no overflow + DPR canvas; `W5-R06` chart teardown/no leaks; `W5-R07` unauthenticated 401/no-store/400 probes + generic 404 | `S027` | `S027` (I001 execution) | `KI-W5-V1`/`V4` |

### 6.2 Control-to-case allocation (`W5-NC01`–`W5-NC12`)

`W5-NC01`→`W5-A05`,`W5-A06` (parser-bypass mutation); `W5-NC02`→`W5-C02`
(per-market selection reintroduction); `W5-NC03`→`W5-I05`
(remove-one-registration); `W5-NC04`→`W5-I06` (CDN-string injection);
`W5-NC05`→`W5-R01` (forced second timer); `W5-NC06`→`W5-I06` (dependency
version divergence); `W5-NC07`→`W5-A02` (six-seed acceptance);
`W5-NC08`→`W5-C08` (flag-repeat cap removal); `W5-NC09`→`W5-C02`,`W5-R03`
(stale overwrite); `W5-NC10`→`W5-I04` (extra-path injection);
`W5-NC11`→`W5-B05` (CSV column divergence); `W5-NC12`→`W5-A06`,`W5-I02`
(unknown-key weakening). Each control proves: unchanged oracle passes →
injected defect makes the named assertion throw → fresh unchanged witness
passes. A4 `KI-W5-T3` item 13's "disables a required local dependency"
control is executed as the `W5-NC06` version-divergence mutation (a
wrong-version literal stands in for a disabled dependency because
mutating `node_modules` is a prohibited workspace mutation); the runtime
detector is `W5-B07`/`W5-B08` (unregistered or zero-size charts fail).
Recorded for parent review.

### 6.3 Parent-item mapping (unmapped counts all zero)

- Requirements: `REQ-KI-001/002` → S001–S005, S008, S009, S016–S023,
  S027; `REQ-KI-005`–`009` → S001, S002, S005, S006, S012, S013, S016,
  S019, S024, S025; `REQ-KI-014` → S006–S016, S025, S026, S027;
  `REQ-KI-015`–`017` → S013, S016, S020, S027; `REQ-KI-018` → S011,
  S021, S024, S026, S027.
- Decisions: `DEC-KI-012` (S001, S002, S024); `DEC-KI-013` (S006, S012,
  S013, S016, S025); `DEC-KI-014` (S001, S002, S006, S013, S019, S024);
  `DEC-KI-015` (S001, S002, S013, S024); `DEC-KI-017` (S016, S020,
  S027); `DEC-KI-018` (S009); `DEC-KI-019` (S001–S005, S017–S021, S024,
  S027); `DEC-KI-023` (S006–S016, S025, S027).
- Tasks: `KI-W5-T1` → S001–S005, S017–S023; `KI-W5-T2` → S006, S010–S013,
  S016, S025; `KI-W5-T3` → S007, S014, S015, S026, S027.
- Scenarios: `SCN-KI-016` → S026 (`W5-I*`), S027 (`W5-B*`);
  `SCN-KI-017` → S027 (`W5-R*`).
- Preconditions: `KI-W5-P1`–`P4` satisfied at entry (`EV-KI-W5-S01`);
  `KI-W5-P5` satisfied by this decomposition + S2/S3 (status
  `AWAITING_PARENT_DECOMPOSITION_REVIEW`); `KI-W5-P6` is the parent's
  decomposition-review action.

### 6.4 Coverage accounting rule (`KI-W5-I001-M`)

At I001, `required` = the literal 43-ID set of §6.1; `registered` = the
union of the four emitted certificates' `registered` arrays; `executed` =
the union of their `executed` arrays. Acceptance requires set equality of
all three, per-set §3.1 digests equal to
`cb8ef6d7cb87b5a451e438d11b0f037c8130f78d0c3e033b1304f78bfa1f6bdb` for
`required`, zero `skipped`, zero `oracleFailures`, and every executed ID
carrying an activation witness. Missing, duplicate, unexpected, filtered,
or unactivated members fail the assessment.

---

## 7. Mandatory decomposition-readiness checklist (sub-window standard §11)

All items are checked with `S3` evidence recorded in
`EV-KI-W5-S01`–`S03`.

- [x] `SW-A01` Assignment `ASG-KI-W5-WA-02`, agent `KI-W5-WINDOW-AGENT`, delegation authority exact and current. Evidence: `EV-KI-W5-S01` §1.
- [x] `SW-A02` Standards and contract/decision/checklist/state revisions pinned and verified with the §0.4 delta audit. Evidence: `EV-KI-W5-S01` §2.
- [x] `SW-A03` Parent write/read/action/prohibition/successor/stop boundaries copied without expansion. Evidence: `EV-KI-W5-S01` §3.
- [x] `SW-A04` Repositories, dirty state, and owner-controlled changes inventoried. Evidence: `EV-KI-W5-S01` §4.
- [x] `SW-A05` Three subordinate artifacts exist with non-overlapping authorities. Evidence: `EV-KI-W5-S03` §1.
- [x] `SW-A06` Strict adjacency and no subagent delegation enforced. Evidence: `EV-KI-W5-S03` §2.
- [x] `SW-D01` Every parent requirement, invariant, decision, task, scenario, and case allocated to exact files and assertions. Evidence: `EV-KI-W5-S03` §3 (§6 mapping).
- [x] `SW-D02` No missing parent-level decision or contradictory authority. Evidence: `EV-KI-W5-S02` §1.
- [x] `SW-D03` Required changed-file set equals the planned initial file set (digest `a04dce13…`). Evidence: `EV-KI-W5-S01` §5.
- [x] `SW-D04` One initial sub-window per file, one file per sub-window (27/27). Evidence: `EV-KI-W5-S03` §4.
- [x] `SW-D05` Every operation, starting digest, anchor, interface, preserved behavior, and forbidden edit exact. Evidence: `EV-KI-W5-S02` §2–§5.
- [x] `SW-D06` Dependency graph complete, sequential, acyclic, justified by named outputs. Evidence: `EV-KI-W5-S02` §6.
- [x] `SW-D07` Every cross-file interface frozen before dependent execution (`I-F1`–`I-F18`). Evidence: `EV-KI-W5-S02` §7.
- [x] `SW-D08` Every intermediate state has exact checks, expected failures, safety, resolver, prohibitions (§4.1). Evidence: `EV-KI-W5-S03` §5.
- [x] `SW-D09` Production, test, and coordination files have separate sub-windows (S001–S023 production, S024–S026 node tests, S027 browser test). Evidence: `EV-KI-W5-S03` §4.
- [x] `SW-D10` No rename, multi-output generator, formatter, installer, or command can violate the one-file invariant. Evidence: `EV-KI-W5-S03` §6.
- [x] `SW-E01` Every file sub-window contains every §7 field. Evidence: `EV-KI-W5-S03` §7.
- [x] `SW-E02` Every sub-window prescribes exact ordered edits, not alternatives or broad verbs. Evidence: `EV-KI-W5-S03` §7 (banned-verb lint zero).
- [x] `SW-E03` Every sub-window has exact preflight, checks, witnesses, assertions, forbidden outcomes. Evidence: `EV-KI-W5-S03` §7.
- [x] `SW-E04` Every sub-window mechanically proves its one-file changed set (V2 + I001 `KI-W5-V2`). Evidence: `EV-KI-W5-S03` §7.
- [x] `SW-E05` Exact evidence, handoff, stop, and successor-reservation rules per sub-window. Evidence: `EV-KI-W5-S03` §7.
- [x] `SW-E06` Subagents report only to the window agent and cannot update authority artifacts. Evidence: `EV-KI-W5-S03` §2.
- [x] `SW-E07` No sub-window requires successor work for file-local acceptance. Evidence: `EV-KI-W5-S03` §8.
- [x] `SW-E08` Deferred checks name the owning assessment (B/R execution and build → I001 gates). Evidence: `EV-KI-W5-S03` §8.
- [x] `SW-V01` Cases allocated to exact test files, registrations, witnesses, assertions (§6). Evidence: `EV-KI-W5-S03` §9.
- [x] `SW-V02` Local and whole-window set-equality and digest checks prescribed (per-file certificates + `KI-W5-I001-M`). Evidence: `EV-KI-W5-S03` §9.
- [x] `SW-V03` Every critical invariant has a negative control at the narrowest level (§6.2). Evidence: `EV-KI-W5-S03` §9.
- [x] `SW-V04` Substitute fidelity and invalidation rules exact (the S025 pure-logic layer and S027 interception substitute recorded; real Chrome remains the fidelity anchor). Evidence: `EV-KI-W5-S03` §9.
- [x] `SW-V05` I001 authored with zero implementation-file write authority. Evidence: `EV-KI-W5-S03` §10.
- [x] `SW-V06` Gates exact, risk-proportionate, scheduled at the final assessment only. Evidence: `EV-KI-W5-S03` §10.
- [x] `SW-V07` Correction diagnosis, one-file assignment, invalidation, reassessment rules complete. Evidence: `EV-KI-W5-S03` §11.
- [x] `SW-V08` Window agent independently inspects every handoff and personally executes the assessment. Evidence: `EV-KI-W5-S03` §10.
- [x] `SW-V09` Approval cannot pass through zero-work/skip/filter/duplicate/unexpected/unactivated/summary-only evidence. Evidence: `EV-KI-W5-S03` §9.
- [x] `SW-V10` Parent handoff contents and `READY_FOR_PARENT_REVIEW` boundary exact. Evidence: `EV-KI-W5-S03` §12.
- [x] `SW-R01` All IDs unique and all references resolve. Evidence: `EV-KI-W5-S03` §13.
- [x] `SW-R02` No unresolved placeholder in any checked item or assignable sub-window. Evidence: `EV-KI-W5-S03` §13.
- [x] `SW-R03` Single-file write-set lint rejects zero/two/wildcard/directory/rename/incidental outputs. Evidence: `EV-KI-W5-S03` §13.
- [x] `SW-R04` Removing one required file or mapping makes readiness fail. Evidence: `EV-KI-W5-S03` §14.
- [x] `SW-R05` Removing/skipping/filtering/bypassing one case makes acceptance fail. Evidence: `EV-KI-W5-S03` §14.
- [x] `SW-R06` Weakening an oracle or diverging a substitute invalidates evidence. Evidence: `EV-KI-W5-S03` §14.
- [x] `SW-R07` Simulated second-file edit and direct parent communication rejected. Evidence: `EV-KI-W5-S03` §14.
- [x] `SW-R08` Simulated integration failure cannot be repaired without a corrective sub-window. Evidence: `EV-KI-W5-S03` §14.
- [x] `SW-R09` Parent decomposition review recorded before the first implementation assignment. Evidence: `EV-KI-W5-S03` §12 (S2 boundary).
- [x] `SW-R10` Document lint reports zero missing fields, mappings, cases, evidence references, or authority conflicts. Evidence: `EV-KI-W5-S03` §13.

Counts: checked 44 / unchecked 0.

---

## 8. Correction protocol and terminal boundary

- Corrections are append-only `KI-W5-C001`, `KI-W5-C002`, …; each owns
  exactly one file from the same 27-file set; a §12.2 corrective readiness
  certificate is appended to `S3` before assignment; a completed
  sub-window's history is never rewritten; dependent evidence is
  invalidated per §10 of the sub-window standard (only gates whose inputs
  changed re-run).
- Terminal boundary: after `I001` succeeds, `S2.decomposition_status` is
  `READY_FOR_PARENT_REVIEW` and the window agent produces the §12.5
  consolidated handoff. The window agent does not claim parent
  acceptance, does not begin `KI-W6`, and does not assign any further
  leaf without a recorded parent review.
- `S2`/`S3` seeding: `S2` starts at `state_version: 1`,
  `decomposition_status: AWAITING_PARENT_DECOMPOSITION_REVIEW`,
  `current_subwindow: NONE`, `next_subwindow: KI-W5-S001`; `S3` opens
  with `EV-KI-W5-S01`–`S03` (entry gate and delta audit; dependency and
  digest verification; authoring lint and the §12.1 readiness
  certificate).
- Recorded interpretations awaiting parent decomposition review (all in
  this document): §0.1 `KI-W5-P2` fixture-server reading; §3.5/§3.8 the
  two materialized charts (`chart:cluster-volume`, `chart:treemap`) absent
  from the standalone DOM; §6.2 the `W5-NC06` dependency-control form;
  §5.25 the pure-logic test-substitute layer. None of these delegates a
  decision to a leaf; each is a fixed, reviewable authoring choice.

---

## 9. Addendum: leaf dispatch and block-consumption tracking (requester-authorized 2026-08-19)

This addendum is appended under explicit requester authorization ("can you
track them yourself until now, then keep tracking them as we go through
the next sub windows? or you can make them visible with a update in the
checklist", 2026-08-19). It changes no frozen block, interface, gate,
digest, or assignment; it adds dispatch-protocol requirements for all
not-yet-dispatched leaves (`KI-W5-S008` onward) and records the tracking
method applied retroactively to `KI-W5-S001`–`KI-W5-S007`. The reviewed
decomposition content (§0–§8) is byte-identical to revision
`740f84cfbc910782d501ac68c43f9fe24a58fbec55f242cb9595c1a36b92588d`.

### 9.1 Dispatch requirement (`KI-W5-S008` onward)

Every leaf dispatch MUST include:

1. the verbatim §5.x block text for the leaf's `subwindow_id`; and
2. the filesystem path of this checklist
   (`KEYWORD_INTELLIGENCE_KI_W5_SUBWINDOW_CHECKLIST.md`, workspace root).

The leaf MUST read its block from this file before any edit. The leaf
handoff MUST quote its `subwindow_id`, `writable_file`, and
`starting_file_digest` verbatim (P1 evidence). When the requester waives
the quote form for a dispatch, the window agent still records
block-consumption proof from artifact literals (`EV-KI-W5-S10` method).

### 9.2 Window-agent tracking (all leaves)

The window agent verifies and records block consumption for every leaf:

- retroactive evidence: `EV-KI-W5-S10` (S001–S006 method + verification)
  and the "P1 block consumption" line in `EV-KI-W5-S11` (S007);
- from `KI-W5-S008` onward: each window-review entry carries an explicit
  "P1 block consumption" line citing the handoff quotes (or the recorded
  waiver) plus at least one block-specific literal present in the output;
- the running table lives in S2 (mechanical state file), one row per
  leaf, updated at every acceptance.

### 9.3 Visibility note

This checklist is untracked in the root repository (owner-controlled
relocation state) and outside the `frontend/` repository boundary;
git-based discovery from inside `frontend/` cannot find it. Leaves reach
it only via the explicit path supplied at dispatch (§9.1). Committing
root coordination documents remains an owner action.
