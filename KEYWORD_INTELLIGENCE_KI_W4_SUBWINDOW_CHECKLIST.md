# KI-W4 Sub-Window Checklist (`S1`)

Authoritative decomposition of parent window `KI-W4` (assignment
`ASG-KI-W4-WA-01`, agent `KI-W4-WINDOW-AGENT`) under
`PROJECT_AGNOSTIC_WINDOW_AGENT_SUBWINDOW_AUTHORING_STANDARD.md` (revision
`1766f9107ce7d315877b75d4b0ea2b5521dff1c321e12f890b03787d66196ded`).

Authoring style (requester selection, 2026-08-18, `EV-KI-W4-S01` §0.4):
**contract + exact anchors**. Each leaf block fixes complete signatures,
defaults, invariants, verbatim insertion anchors, exact check commands, and
literal expected outcomes; verbatim implementation code is embedded only for
the one small pure addition (`I-F1`). Leaf subagents apply one bounded,
decision-complete block per file and never require global `S1` context.

---

## 0. Inherited authority and revision pins

### 0.1 Parent package

| Artifact | Path | Pinned revision (A5 state 100) | Observed revision (2026-08-18) |
|---|---|---|---|
| Parent standard | `PROJECT_AGNOSTIC_DECISION_COMPLETE_CHECKLIST_AUTHORING_STANDARD.md` | `3b7a4fd25156e1adfbc92abb835c5f82a0d18c686b1c1150feb202f2d944d2ac` | equal |
| Sub-window standard | `PROJECT_AGNOSTIC_WINDOW_AGENT_SUBWINDOW_AUTHORING_STANDARD.md` | `1766f9107ce7d315877b75d4b0ea2b5521dff1c321e12f890b03787d66196ded` | equal |
| A1 contract | `KEYWORD_INTELLIGENCE_PRODUCT_CONTRACT.md` | `8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c` | equal |
| A3 decision ledger | `KEYWORD_INTELLIGENCE_DECISION_LEDGER.md` | `5c42924c8ea6ad1ca43a00feff2b636d83bcd029b7b8a4eeb6777ac60a7f5ec6` | `c2dc635e5aa58f88c1ec465154663d314af68570fd4cbfdfca7b51c393c6f70f` (marker `KI-DL-10`) |
| A4 parent checklist | `KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md` | `8dce27da58ace35c605ee1f9d0b4ddc8a1e9358a282ec5bf8d7b461729eb999b` | `40f705a423da88b952af4e529566b5a5374d4c7c1d7a0a589642d5906f0744ee` (marker `KI-CL-12`) |

- **Delta audit (sub-window standard §0.4):** the A5 state 100 A3/A4 pins are
  stale byte copies from before `CHG-KI-016` (recorded in
  `KEYWORD_INTELLIGENCE_SPECIFICATION_CHANGELOG.md`, entry `CHG-KI-016`,
  2026-08-18T18:16:14+05:30). The observed A3/A4 files contain the complete
  W4 package: `DEC-KI-033` (A3 lines 1281–1565), the `KI-W4` window section
  with task blocks `KI-W4-T1`–`T4`, the literal 34-case matrix, controls
  `W4-NC01`–`NC18`, and gates `KI-W4-V1`–`V4` (A4 lines 1786–2214). Audit,
  hash recomputations, and the residual parent action (refresh A5 pins at the
  next A5 CAS) are recorded in `EV-KI-W4-S01`. This decomposition binds to the
  observed revisions above.
- **Assignment provenance:** requester performed the A5 CAS to state 100
  creating `ASG-KI-W4-WA-01` for `KI-W4-WINDOW-AGENT` with the three-artifact
  write scope of §1. No requester exception or waiver applies.

### 0.2 Authority precedence

A1 contract → parent standard → sub-window standard → A3 decision ledger →
A4 checklist (observed revisions) → A5 active state → this `S1` → `S2` →
`S3` (append-only facts only). `S1`/`S2`/`S3` cannot amend a parent decision,
task, ownership boundary, or authority.

---

## 1. Prohibitions (copied from A5 state 100, unexpanded)

- Window-agent edits to any implementation file: the window agent writes only
  `KEYWORD_INTELLIGENCE_KI_W4_SUBWINDOW_CHECKLIST.md`,
  `KEYWORD_INTELLIGENCE_KI_W4_SUBWINDOW_STATE.md`, and
  `KEYWORD_INTELLIGENCE_KI_W4_SUBWINDOW_EVIDENCE.md`.
- Parallel leaves: exactly one leaf is assigned and in flight at any time
  (sub-window standard §5.4).
- Direct parent–subagent communication: subagents report only to the window
  agent; the parent communicates only with the window agent (§1.4).
- Schema or Prisma migration edits; `package.json`/lockfile edits; config or
  runtime-config edits (`src/config.js`, environment variables); worker,
  recovery, or dispatcher service edits
  (`src/aws-pipeline/keyword-intelligence/*`); frontend or infrastructure
  edits; provider calls; AWS operations; production database writes; the full
  opted-in database integration suite; Prisma generate/validate as W4 gates.
- No purge of queues, buckets, prefixes, database rows, or stacks; no commits
  or staging; preserve the owner-controlled relocation state of the
  coordination root and all unrelated dirty worktree changes.
- Implementation of `G14`, `G15`, `KI-W5`, or any later window; no reuse of
  window IDs; corrections are append-only `KI-W4-C001`, `KI-W4-C002`, ….

---

## 2. Baseline (verified 2026-08-18, `EV-KI-W4-S01`/`S02`)

| Item | Value |
|---|---|
| Backend `email_scraper` HEAD | `d98ad53c02d8d8205d614043436164d85b84c6ce` ("Pre KI-W$ commit"), `git status --porcelain` empty |
| Frontend `frontend` HEAD | `0dfa1acac50fac3a86d02ec674c6d2bab645832d`, clean, read-only for `KI-W4` |
| Root change set | 33 paths, per-LF set digest `b33384c5ceb700902be88af820cbd0998699dbbdd2970e0d571c649107479ca5`, preserved unmodified |
| Planned ten-file set digest | `fe48d14ebec1dffa058cf91cfa9ec10982d4ceaa4c63e0cb9280cabf39a4a59b` (equals A4 `KI-W4` header `required_initial_file_set_digest`) |
| Manifest 34-ID digest | `86810ce87a79426bb972be2e2827abc3806835190135d17769b52c33e7bb2203` (normative sorted-member-plus-LF; recomputed from the A4 literal matrix) |

Starting file digests (before any `KI-W4` leaf):

| Path | Digest |
|---|---|
| `email_scraper/src/api-serializer.js` | `d1c6c579c150f1df17284c3c108d46710cf7e963dac5723de4b85f7a4e11fc56` |
| `email_scraper/src/keyword-intelligence/cluster.js` | `7dfbda3412c47eb28147cf80f4f05f368c946057f99e2f218a0287159701260b` |
| `email_scraper/src/keyword-intelligence/repository.js` | `e2cad9ea0d47adca3baeb28261da7a09ad775e5fc15c1ecde33f132d7387ee39` |
| `email_scraper/src/prisma-run-repository.js` | `c719ed27276cba78bbb140cf8a1241b19af426db82e5dedf40a99363a89da173` |
| `email_scraper/src/query-review.js` | `5cfbbe77aaa9dc94a5fe852d857f38bff52220518d510cc6eacd1b429f35d67a` |
| `email_scraper/src/server.js` | `73b2384ac85b36f4ae445d6a49fc00b0d03369b382eac278d944970c170fc2ec` |
| `email_scraper/src/keyword-intelligence/api.js` | ABSENT |
| `email_scraper/test/fixtures/keyword-intelligence/ki-w4-enforcement-manifest-v1.json` | ABSENT |
| `email_scraper/test/keyword-intelligence-api.test.js` | ABSENT |
| `email_scraper/test/keyword-intelligence-handoff.integration.test.js` | ABSENT |

Verified absent symbols in the six existing files (grep, zero matches):
`classifyKeywordForSelection`, `serializeKeywordResearch`,
`serializeSelectionItem`, `getOwnedApiView`, `RunHandoffAbort`,
`validateResearchBackedQueryList`, `validateResearchBackedConfirmedQueryRows`,
`newRunId`, `createKeywordResearchRun`, `createKeywordResearchQueries`,
`queryPlanSource`, `keywordResearchApi`, `requestedKeywordResearchId`.

---

## 3. Frozen formulas and interface freeze

### 3.1 Digest formula (parent standard, `F-D2`)

Set digest = `sha256` over the byte concatenation of each set member sorted by
unsigned UTF-8 byte order, each encoded UTF-8 followed by exactly one LF
(`\n`). Applied to: the ten planned paths (`fe48d14e…`), the 34 manifest IDs
(`86810ce8…`), each registry's `required`/`registered`/`executed` arrays in the
TAP certificates, and the assembled changed-file set at `KI-W4-V1`.

### 3.2 Interface freeze `I-F1`–`I-F11`

Every leaf consumes exactly these frozen forms; no leaf may alter a signature,
default, outcome union, error code, or key set defined here.

- **I-F1** `cluster.js` exports
  `classifyKeywordForSelection(keyword, { mainIntent = null, stripTokens = [] } = {})`
  returning exactly `{ lane, facets }` where `lane` is one of
  `local_discovery|brand_competitor|store_discovery|category_discovery` and
  `facets` is the existing five-key facet object of `cluster.js:51`. Verbatim
  implementation (embedded; the only verbatim block in this document):

  ```js
  export function classifyKeywordForSelection(keyword, { mainIntent = null, stripTokens = [] } = {}) {
    const toks = tokens(keyword, stripTokens);
    return { lane: lane({ keyword, mainIntent }, toks), facets: facets(toks, keyword) };
  }
  ```

- **I-F2** `api-serializer.js` exports `serializeSelectionItem(item)` and
  `serializeKeywordResearch(research)` emitting exactly the `DEC-KI-019`
  `ResearchView` key list; `serializeRun` adds
  `queryPlanSource:"keyword_research"`, `keywordResearchId`, and
  `keywordSelectionRevision` only for research-backed runs;
  `serializeRunQuery` adds `keywordResearchItemId` only when that column is
  non-null. Legacy serialized objects retain their exact prior key sets.
- **I-F3** `repository.js` adds
  `getOwnedApiView({ researchId, ownerId })` returning exactly
  `{ outcome: "found", research } | { outcome: "not_found" }`; one private
  `RunHandoffAbort` sentinel class beside `FinalPublicationAbort`; the
  `createRun` callback invocation exactly as A3 lines 1370–1375; post-write
  invalid callback output maps after rollback to
  `{ outcome: "conflict", code: "KEYWORD_RUN_HANDOFF_INVALID" }`.
- **I-F4** `query-review.js` exports
  `validateResearchBackedQueryList(queries, run)` returning exactly
  `{ valid, queries: [{ id, categoryIndex, query }], errors }` and
  `validateResearchBackedConfirmedQueryRows(rows, categories, config, status, options)`
  returning the `{ valid, errors, rows, queryPlans }` shape of
  `validateConfirmedQueryRows` with all-rows validity (never per-category
  exact counts).
- **I-F5** `prisma-run-repository.js` exports `newRunId()`; instance methods
  `createKeywordResearchRun(tx, input)` and
  `createKeywordResearchQueries(tx, input)` with the exact input requirements,
  field overrides (`state="awaiting_query_confirmation"`,
  `phase="query_review"`, `stage="awaiting_query_confirmation"`,
  `queryRevision=1`, `queryPlanReadyAt=now`, `keywordResearchId`,
  `keywordSelectionRevision`, `keywordSelectionSnapshot`,
  `queryPlanSource="keyword_research"`), and the `replaceEditableQueries`
  research-branch invariants of A3 lines 1414–1429 including the
  `PIPELINE_INPUT_CONFLICT` unknown-discriminator throw before the CAS.
- **I-F6** `api.js` exports `createKeywordResearchApi({ keywordRepository,
  runRepository, dispatchInitialize, now = () => new Date(), researchIdFactory
  = newResearchId, runIdFactory = newRunId, configSnapshot =
  keywordResearchConfigV1() })` with methods `createResearch`, `getResearch`,
  `saveSelection`, `createRun`, `exportCsv` and the outcome unions of
  `DEC-KI-033` (A3 lines 1281–1310).
- **I-F7** `server.js` adds `requestedKeywordResearchId(pathname)` validating
  exactly `^kr_[A-Za-z0-9_-]{24}$`; exactly the five `DEC-KI-019` routes with
  statuses 202/200/200/201-or-200/200 and the nine keyword error codes of A3
  lines 1489–1506; CSV response headers
  `text/csv; charset=utf-8`,
  `Content-Disposition: attachment; filename="keyword-research-<researchId>.csv"`,
  `Cache-Control: no-store`.
- **I-F8** manifest root exactly
  `{ "contractVersion": "ki-w4-enforcement-manifest-v1", "groups": { api_component, server_routes, query_review, handoff_database, conformance } }`
  with the literal 34 IDs and per-LF digest `86810ce8…`; each registry file
  emits exactly one TAP diagnostic line beginning
  `KI_W4_EXECUTION_CERTIFICATE=` followed by the compact JSON of A4 `KI-W4-T4`
  item 6.
- **I-F9** registry composition: `keyword-intelligence-api.test.js` executes
  the 28 non-DB IDs in group order `api_component → server_routes →
  query_review → conformance`; `keyword-intelligence-handoff.integration.test.js`
  registers `W4-D01`–`D06` as six sequential named subtests in one isolated
  disposable schema; the two certificates merge at `KI-W4-V6` into the 34-ID
  global union and digest.
- **I-F10** `createLeadServer` accepts injected
  `researchQueryValidationPipeline` and optional `keywordResearchApi`; when the
  injection is absent it constructs exactly one
  `PrismaKeywordResearchRepository(repository.prisma)`-backed service per
  server with `now` and the lazy `dispatchInitialize` of A3 lines 1457–1469;
  no environment read and no new config key.
- **I-F11** `drainQueue` passes `queryPlanSource` and
  `keywordSelectionSnapshot` from the claimed run into `executeRun`; both
  confirmation branches select the research validators only for
  `keyword_research`; `legacy` keeps the existing validators and exact-count
  policy; any other discriminator throws `PIPELINE_INPUT_CONFLICT` before
  edit, confirmation, probe, or dispatch.

### 3.3 Error-code freeze (server routes)

`400 KEYWORD_RESEARCH_INPUT_INVALID`; `409 KEYWORD_RESEARCH_CONTRACT_MISMATCH`;
`404 KEYWORD_RESEARCH_NOT_FOUND`; `409 KEYWORD_RESEARCH_NOT_COMPLETED`;
`409 KEYWORD_SELECTION_HAS_CONFLICTS`; `409 KEYWORD_SELECTION_REVISION_CONFLICT`;
`409 KEYWORD_RUN_HANDOFF_CONFLICT`; research query edit/start retains
`422 QUERY_LIST_INVALID`, the existing 409 query-revision/lifecycle codes, and
`404 RUN_NOT_FOUND`; unexpected failures use the existing safe 500 mapper. No
response contains provider text.

---

## 4. Dependency graph (strictly sequential execution, §5.4)

| # | ID | File | Operation | Interface predecessors (named outputs) |
|---|---|---|---|---|
| 1 | `KI-W4-S001` | `email_scraper/src/keyword-intelligence/cluster.js` | MODIFY | none |
| 2 | `KI-W4-S002` | `email_scraper/src/api-serializer.js` | MODIFY | none |
| 3 | `KI-W4-S003` | `email_scraper/src/keyword-intelligence/repository.js` | MODIFY | none |
| 4 | `KI-W4-S004` | `email_scraper/src/query-review.js` | MODIFY | none (reads `query-mapper.js` read-only) |
| 5 | `KI-W4-S005` | `email_scraper/src/prisma-run-repository.js` | MODIFY | consumes `I-F3` callback contract |
| 6 | `KI-W4-S006` | `email_scraper/src/keyword-intelligence/api.js` | CREATE | `I-F2`, `I-F3`, `I-F5` exports |
| 7 | `KI-W4-S007` | `email_scraper/src/server.js` | MODIFY | `I-F4`, `I-F6`, `I-F2` |
| 8 | `KI-W4-S008` | `email_scraper/test/fixtures/keyword-intelligence/ki-w4-enforcement-manifest-v1.json` | CREATE | none (literal A4 matrix) |
| 9 | `KI-W4-S009` | `email_scraper/test/keyword-intelligence-api.test.js` | CREATE | `I-F6`, `I-F7`, `I-F8` |
| 10 | `KI-W4-S010` | `email_scraper/test/keyword-intelligence-handoff.integration.test.js` | CREATE | `I-F3`, `I-F5`, `I-F6`, `I-F8` |
| 11 | `KI-W4-I001` | (integration assessment, no file write) | ASSESS | all ten leaves |

Execution is strictly sequential `S001 → S010` then `I001` regardless of
interface independence: `predecessors` records the true interface
dependencies; the immediately preceding leaf is always also a predecessor
under §5.4. `may_start_successor` is `false` for every leaf; only the window
agent assigns the next leaf after an `ACCEPTED_FOR_INTEGRATION` review.

### 4.1 Intermediate states (§6.1)

| State | Exact condition | Permitted checks | Expected temporary failures | Resolver | Prohibitions |
|---|---|---|---|---|---|
| IS-1 (after S001–S005) | new exports exist, no production caller | `node --check`, per-leaf focused regression suites of §5 | none (all existing suites must pass) | S006/S007 wire callers | no caller edits inside these leaves |
| IS-2 (after S006) | `api.js` importable, unused by server | import smoke asserting the frozen export set | none | S007 | no route edits in S006 |
| IS-3 (after S007) | five routes live, zero tests reference them | `test/server.test.js`, `test/query-review-server.test.js` regressions | none | S009 | no test edits in S007 |
| IS-4 (after S008) | manifest fixture present, unreferenced | JSON parse + digest recompute | none | S009/S010 | no test edits in S008 |
| IS-5 (after S009) | 28 non-DB IDs green locally; D-registry absent | one `node --test` run of the new file | none | S010 + I001 `V3` | no DB execution at leaf level |
| IS-6 (after S010) | DB registry file present, syntax-checked only | `node --check` | none | I001 gates `V1`–`V4` | no DB run before I001 |


---

## 5. File sub-window blocks

Semantics common to every block below: the recorded
`starting_repository_change_set_digest` is the authoring-time root set; leaf
preflight (P2) instead proves both nested repositories clean at their §2
HEADs and the root change set equal to the §2 inventory plus exactly the
three `KI-W4` subordinate artifacts. V3 local coverage accounting:
production and fixture leaves carry zero local case IDs (all 34 IDs are
allocated by §6 and execute in `S009` or at `KI-W4-I001`); registry leaves
carry the §6 allocation.

### 5.1 `KI-W4-S001` — cluster classifier export

```yaml
subwindow_id: KI-W4-S001
type: FILE
parent_window_id: KI-W4
parent_assignment_id: ASG-KI-W4-WA-01
assigned_agent: UNASSIGNED
predecessors: []
successor_reserved_for: WINDOW-AGENT
writable_file: email_scraper/src/keyword-intelligence/cluster.js
file_operation: MODIFY
starting_file_digest: 7dfbda3412c47eb28147cf80f4f05f368c946057f99e2f218a0287159701260b
starting_repository_change_set_digest: b33384c5ceb700902be88af820cbd0998699dbbdd2970e0d571c649107479ca5
read_only_scope:
  - email_scraper/src/keyword-intelligence/cluster.js
  - email_scraper/src/keyword-intelligence/dedup.js
  - KEYWORD_INTELLIGENCE_DECISION_LEDGER.md lines 1281-1310 (DEC-KI-033 classifier clause)
  - KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md lines 1790-1870 (KI-W4-T1)
authorized_actions:
  - read every file listed in read_only_scope
  - apply the ordered transformation to exactly writable_file and no other file
  - run the exact LOCAL_NOW checks of this block
  - report the exact handoff to the window agent
prohibited_actions:
  - edit any second file
  - edit KEYWORD_INTELLIGENCE_KI_W4_SUBWINDOW_CHECKLIST.md, KEYWORD_INTELLIGENCE_KI_W4_SUBWINDOW_STATE.md, or KEYWORD_INTELLIGENCE_KI_W4_SUBWINDOW_EVIDENCE.md
  - start the successor or any later sub-window
  - communicate with the parent agent
  - mutate external state (providers, AWS, databases, queues, buckets)
  - weaken any existing test, fixture, or oracle
may_start_successor: false
```

Mechanical trace: `REQ-KI-007`–`009` (selection classification); `DEC-KI-033`;
`KI-W4-T1` item for `cluster.js`; consumed by `KI-W4-S009` case `W4-A04` and
`DEC-KI-014` conflict analysis through the accepted selection pipeline.

Exact transformation:

1. Anchor: the file currently ends at line 346 with the closing `}` of
   `attachVariants`. Append one blank line then the verbatim `I-F1` block of
   §3.2. No other edit.
2. The export calls the existing private `tokens` (line 47), `lane`
   (line 85), and `facets` (line 51) in that order; `mainIntent: null`
   deactivates the navigational branch through the existing
   `(record.mainIntent || "")` guard; the function is pure (no input
   mutation, no I/O, no new import).
3. Preserved: all existing exports (`AUDIENCE`, `CHANNEL`, `GENERIC`,
   `CATEGORY_TERMS`, `FIT_TERMS`, `MODIFIER_TERMS`, `clusterKeywords`,
   `attachVariants`) and every private helper byte-for-byte; `signature`/
   `stableId` imports unchanged.
4. Forbidden within this file: exporting or modifying `tokens`/`facets`/
   `lane`, altering lane precedence, editing `dedup.js`.

Exact checks (`LOCAL_NOW`, from `email_scraper/`):

- C1 `node --check src/keyword-intelligence/cluster.js` → exit 0.
- C2 `grep -c "export function classifyKeywordForSelection" src/keyword-intelligence/cluster.js`
  → exactly `1`.
- C3 `node --test test/keyword-intelligence-parity.test.js` → exit 0, zero
  failing tests; activation witness: the suite imports
  `keyword-intelligence/cluster.js` (verified by the import graph) and
  completes without modification. Forbidden outcome: any modification of the
  parity suite.
- Coverage: zero local case IDs (`W4-A04` wiring executes in `S009`).
- Expected workspace write set: `M email_scraper/src/keyword-intelligence/cluster.js`
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

### 5.2 `KI-W4-S002` — public research serializers

```yaml
subwindow_id: KI-W4-S002
type: FILE
parent_window_id: KI-W4
parent_assignment_id: ASG-KI-W4-WA-01
assigned_agent: UNASSIGNED
predecessors: [KI-W4-S001]
successor_reserved_for: WINDOW-AGENT
writable_file: email_scraper/src/api-serializer.js
file_operation: MODIFY
starting_file_digest: d1c6c579c150f1df17284c3c108d46710cf7e963dac5723de4b85f7a4e11fc56
starting_repository_change_set_digest: b33384c5ceb700902be88af820cbd0998699dbbdd2970e0d571c649107479ca5
read_only_scope:
  - email_scraper/src/api-serializer.js
  - KEYWORD_INTELLIGENCE_DECISION_LEDGER.md lines 248-307 (DEC-KI-012), 308-348 (DEC-KI-014/015), 404-445 (DEC-KI-019), 1479-1488 (DEC-KI-033 serialization clause)
  - KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md lines 1790-1870 (KI-W4-T1)
authorized_actions:
  - read every file listed in read_only_scope
  - apply the ordered transformation to exactly writable_file and no other file
  - run the exact LOCAL_NOW checks of this block
  - report the exact handoff to the window agent
prohibited_actions:
  - edit any second file
  - edit KEYWORD_INTELLIGENCE_KI_W4_SUBWINDOW_CHECKLIST.md, KEYWORD_INTELLIGENCE_KI_W4_SUBWINDOW_STATE.md, or KEYWORD_INTELLIGENCE_KI_W4_SUBWINDOW_EVIDENCE.md
  - start the successor or any later sub-window
  - communicate with the parent agent
  - mutate external state (providers, AWS, databases, queues, buckets)
  - weaken any existing test, fixture, or oracle
may_start_successor: false
```

Mechanical trace: `REQ-KI-002/005/018`; `INV-KI-013`; `DEC-KI-012/014/015/
019/033`; `KI-W4-T1` serializer items; consumed by `S006` (`getResearch`,
`saveSelection`, `createResearch` responses) and `S007` route bodies;
exercised by `W4-A03`, `W4-S03`, `W4-NC01/NC03/NC11`.

Exact transformation:

1. Insert `serializeSelectionItem(item)` and `serializeKeywordResearch(research)`
   immediately after `serializeEditableQueries` (currently ending line 1006)
   and before `leadRecordToCreate` (line 1008), preserving one blank line on
   each side.
2. `serializeSelectionItem` emits exactly the public `SelectionItem` key list
   of `DEC-KI-014` (A3 lines 308–328) with the canonical id, keyword,
   lineage, market metric, flag, and score fields as defined there; absent
   internal fields (fingerprints, provider raw values, item keys) stay absent.
3. `serializeKeywordResearch` emits exactly the `DEC-KI-019` `ResearchView`
   keys: `id,statusUrl,state,generation,contractVersion,seeds,markets,
   progress,result,selection,selectionRevision,selectionConflicts,safeError,
   createdAt,startedAt,completedAt,updatedAt`; `statusUrl` is
   `` `/api/keyword-research/${encodeURIComponent(research.id)}` ``;
   `progress` is derived only from the attached stage rows as
   `{stage,expansion,anchorScreen,marketOverview}` with `StageCounts`
   exactly `{expected,terminal,succeeded,skipped,failed}` (nonnegative
   integers, `stage:"queued"` when no stage rows exist, terminal `stage`
   derived from research state in the order `expansion → anchor_screen →
   market_overview → finalizing → completed|failed`); `result` is `null`
   unless `state === "completed"`, then the persisted `DEC-KI-012` result
   document; `selection` is the ordered `serializeSelectionItem` array;
   `selectionConflicts` is the strict `DEC-KI-015` component-result array;
   `safeError` is `null` or `{code,message}`; dates are ISO strings or `null`
   with `createdAt`/`updatedAt` non-null.
4. Modify `serializeRun` (line 928): after the existing `error` key
   construction, when `run.queryPlanSource === "keyword_research"` add
   exactly `queryPlanSource: "keyword_research"`,
   `keywordResearchId: run.keywordResearchId`,
   `keywordSelectionRevision: run.keywordSelectionRevision`. Modify
   `serializeRunQuery` (line 980): add
   `...(row.keywordResearchItemId != null ? { keywordResearchItemId: row.keywordResearchItemId } : {})`
   as the final spread-free conditional key. Legacy runs and rows keep their
   exact prior key sets.
5. Preserved: every existing export and its byte behavior; `NORMALIZED_/
   PUBLISHED_PAYLOAD_SCHEMAS` untouched; no new import.
6. Forbidden: serializing config, owner, leases, S3 keys, task/attempt/cache
   rows, raw provider values, credentials, or internal fingerprints; probing
   alternate envelopes; changing `zod` schemas.

Exact checks (`LOCAL_NOW`, from `email_scraper/`):

- C1 `node --check src/api-serializer.js` → exit 0.
- C2 `node --test test/api-serializer.test.js` → exit 0; existing fixtures
  prove legacy `serializeRun`/`serializeRunQuery` key sets unchanged
  (deep-equal baselines). Forbidden: modifying the suite or fixtures.
- C3 `grep -c "export function serializeKeywordResearch\|export function serializeSelectionItem" src/api-serializer.js`
  → exactly `2`.
- Coverage: zero local case IDs (executed in `S009`).
- Expected workspace write set: `M email_scraper/src/api-serializer.js` only.

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

### 5.3 `KI-W4-S003` — repository API view and handoff fencing

```yaml
subwindow_id: KI-W4-S003
type: FILE
parent_window_id: KI-W4
parent_assignment_id: ASG-KI-W4-WA-01
assigned_agent: UNASSIGNED
predecessors: [KI-W4-S002]
successor_reserved_for: WINDOW-AGENT
writable_file: email_scraper/src/keyword-intelligence/repository.js
file_operation: MODIFY
starting_file_digest: e2cad9ea0d47adca3baeb28261da7a09ad775e5fc15c1ecde33f132d7387ee39
starting_repository_change_set_digest: b33384c5ceb700902be88af820cbd0998699dbbdd2970e0d571c649107479ca5
read_only_scope:
  - email_scraper/src/keyword-intelligence/repository.js
  - KEYWORD_INTELLIGENCE_DECISION_LEDGER.md lines 1281-1413 (DEC-KI-033 repository clauses)
  - KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md lines 1790-1930 (KI-W4-T1/T2 repository items)
authorized_actions:
  - read every file listed in read_only_scope
  - apply the ordered transformation to exactly writable_file and no other file
  - run the exact LOCAL_NOW checks of this block
  - report the exact handoff to the window agent
prohibited_actions:
  - edit any second file
  - edit KEYWORD_INTELLIGENCE_KI_W4_SUBWINDOW_CHECKLIST.md, KEYWORD_INTELLIGENCE_KI_W4_SUBWINDOW_STATE.md, or KEYWORD_INTELLIGENCE_KI_W4_SUBWINDOW_EVIDENCE.md
  - start the successor or any later sub-window
  - communicate with the parent agent
  - mutate external state (providers, AWS, databases, queues, buckets)
  - weaken any existing test, fixture, or oracle
may_start_successor: false
```

Mechanical trace: `REQ-KI-002/005/015/016`; `INV-KI-013`; `DEC-KI-033`;
`KI-W4-T1` repository item; consumed by `S006` (`getResearch`, `exportCsv`)
and fenced by `S010` cases `W4-D01`–`D05`.

Exact transformation:

1. Insert `async getOwnedApiView(input)` immediately after `getOwned`
   (currently ending line 354) and before `getWorkerResearch` (line 356).
   Body: `requireResearchId(input?.researchId)`; `requireOwner(input?.ownerId)`;
   one `this.client.keywordResearch.findFirst({ where: { id: researchId,
   ownerId }, include: { stages: { orderBy: [{ stage: "asc" }, {
   generation: "asc" }] } } })`; return `{ outcome: "not_found" }` for a
   null row, else `{ outcome: "found", research }`.
2. Insert `class RunHandoffAbort extends Error {}` immediately after the
   `FinalPublicationAbort` class (lines 42–48) with one blank line separation.
3. In `createRun` (line 1206), inside the accepted interactive transaction,
   after either `constructRun` or `constructQueries` has written: validate the
   returned Run identity (`id === input.runId`, `runId`/owner/research
   lineage), RunQuery array shape (N rows, ordered, ids/`keywordResearchItemId`
   lineage complete), and query count equality; on any invalid result throw
   `RunHandoffAbort`. Add one outer catch mirroring the accepted
   `FinalPublicationAbort` pattern that maps a caught `RunHandoffAbort` —
   only after the transaction has rolled back — to
   `{ outcome: "conflict", code: "KEYWORD_RUN_HANDOFF_INVALID" }`. Pre-write
   conflict returns, exact replay, and callback/database exception escape
   semantics remain exactly as accepted.
4. The callback invocation shape is frozen by `I-F3` (A3 lines 1370–1375);
   this file must accept and pass `{ researchId, ownerId,
   expectedSelectionRevision, clientRequestId, selectionFingerprint, runId,
   items, constructRun, constructQueries }` unchanged.
5. Preserved: every existing method, error code, lease/throttle/cache
   behavior, and export; `newResearchId` (line 132) untouched.
6. Forbidden: owner-scope relaxation, reading progress from S3/queue,
   returning normally after a post-write validation failure, adding public
   mutations, editing `FinalPublicationAbort` semantics.

Exact checks (`LOCAL_NOW`, from `email_scraper/`):

- C1 `node --check src/keyword-intelligence/repository.js` → exit 0.
- C2 `node --test test/keyword-intelligence-repository.test.js` → exit 0
  (accepted repository suite green, no fixture edit). Forbidden: weakening
  any assertion.
- C3 `grep -c "getOwnedApiView\|RunHandoffAbort" src/keyword-intelligence/repository.js`
  → at least `2` (declaration sites).
- Coverage: zero local case IDs (`W4-D01`–`D05` execute at I001 `V3`).
- Expected workspace write set: `M email_scraper/src/keyword-intelligence/repository.js`
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

### 5.4 `KI-W4-S004` — research-backed query validators

```yaml
subwindow_id: KI-W4-S004
type: FILE
parent_window_id: KI-W4
parent_assignment_id: ASG-KI-W4-WA-01
assigned_agent: UNASSIGNED
predecessors: [KI-W4-S003]
successor_reserved_for: WINDOW-AGENT
writable_file: email_scraper/src/query-review.js
file_operation: MODIFY
starting_file_digest: 5cfbbe77aaa9dc94a5fe852d857f38bff52220518d510cc6eacd1b429f35d67a
starting_repository_change_set_digest: b33384c5ceb700902be88af820cbd0998699dbbdd2970e0d571c649107479ca5
read_only_scope:
  - email_scraper/src/query-review.js
  - email_scraper/src/keyword-intelligence/query-mapper.js
  - KEYWORD_INTELLIGENCE_DECISION_LEDGER.md lines 349-366 (DEC-KI-016), 1430-1456 (DEC-KI-033 validator clauses)
  - KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md lines 1930-1991 (KI-W4-T3 validator items)
authorized_actions:
  - read every file listed in read_only_scope
  - apply the ordered transformation to exactly writable_file and no other file
  - run the exact LOCAL_NOW checks of this block
  - report the exact handoff to the window agent
prohibited_actions:
  - edit any second file
  - edit KEYWORD_INTELLIGENCE_KI_W4_SUBWINDOW_CHECKLIST.md, KEYWORD_INTELLIGENCE_KI_W4_SUBWINDOW_STATE.md, or KEYWORD_INTELLIGENCE_KI_W4_SUBWINDOW_EVIDENCE.md
  - start the successor or any later sub-window
  - communicate with the parent agent
  - mutate external state (providers, AWS, databases, queues, buckets)
  - weaken any existing test, fixture, or oracle
may_start_successor: false
```

Mechanical trace: `REQ-KI-010`–`013`; `INV-KI-015`; `DEC-KI-016/033`;
`KI-W4-T3`; consumed by `S007` (edit path and both confirmation branches);
exercised by `W4-Q01`–`Q08` and `W4-NC07`–`NC10/NC16/NC17`.

Exact transformation:

1. Append `validateResearchBackedQueryList(queries, run)` and
   `validateResearchBackedConfirmedQueryRows(rows, categories, config,
   status, options)` after `validateConfirmedQueryRows` (file currently ends
   at line 247 with its closing `}`), separated by one blank line, importing
   `validateResearchBackedQueries` from
   `./keyword-intelligence/query-mapper.js` (add the import beside the
   existing `query-validator.js` import at lines 3–6).
2. Edit validator (`I-F4`): accepts the existing strict
   `{id,categoryIndex,query}` row grammar (unknown keys →
   `unsupported_fields`, non-object rows → `invalid_query_row`, invalid
   category → `invalid_category`, reuse of the existing public error-row
   vocabulary); recovers each persisted `keywordResearchItemId` from
   `run.queries`; delegates grammar/relevance to
   `validateResearchBackedQueries` with `persistedItemIds` and
   `sourceKeywords` recovered from the run; requires the incoming query-ID
   set to equal the persisted query-ID set, the item-ID set to equal the
   persisted item-ID set, 1–100 rows, and each row's `categoryIndex` to equal
   its persisted row's `categoryIndex`; permits order and query-text changes;
   adds/deletes/swaps produce `valid: false` with a reason from the existing
   vocabulary; returns exactly
   `{ valid, queries: [{ id, categoryIndex, query }], errors }`.
3. Confirmation validator (`I-F4`): requires `options.snapshot` (strict
   immutable run snapshot, `keyword-run-snapshot-v1`); builds `sourceKeywords`
   from `snapshot.items` keyed by `itemId`; maps every durable row through
   the accepted `query-mapper.js` input contract (leaf binds the literal
   field names by reading `query-mapper.js:32–110`; `itemId` comes from
   `row.keywordResearchItemId`); revalidates with
   `validateResearchBackedQueries` and `snapshot.dedupStripTokens`; uses the
   returned normalized `phrase` (never either site prefix) for
   `product_phrase` and `product_family` while `query` stays the full mapped
   query; the remaining candidate fields are exactly
   `market_signal: "user_confirmed"`, `seasonality: "unknown"`, the persisted
   `generationReason`/`sourceUrls`, `confidence: 1`; uses the existing
   `freshReusableProbe`/`queryProbeFingerprint`/`normalizeProbeResults` seam
   once per non-reusable valid row with the injected `probe`; validity is
   all 1–100 rows valid with no per-category exact-count rule; returns the
   `{ valid, errors, rows, queryPlans }` shape with `queryPlans` built only
   from `snapshot` lineage fields.
4. Preserved: `validateEditableQueryList`, `validateConfirmedQueryRows`, all
   constants and exports byte-for-byte; legacy behavior untouched.
5. Forbidden: probing Google inside the edit validator, enforcing legacy
   per-category exact counts, accepting add/delete rows, inventing new error
   codes, editing `query-mapper.js` or `query-prober.js`.

Exact checks (`LOCAL_NOW`, from `email_scraper/`):

- C1 `node --check src/query-review.js` → exit 0.
- C2 `node --test test/query-review.test.js test/query-review-server.test.js`
  → exit 0 (legacy validator behavior frozen). Forbidden: weakening the
  suites.
- C3 `grep -c "export function validateResearchBacked" src/query-review.js`
  → exactly `2`.
- Coverage: zero local case IDs (`W4-Q01`–`Q08` execute in `S009`).
- Expected workspace write set: `M email_scraper/src/query-review.js` only.

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


### 5.5 `KI-W4-S005` — run repository handoff methods and research edit branch

```yaml
subwindow_id: KI-W4-S005
type: FILE
parent_window_id: KI-W4
parent_assignment_id: ASG-KI-W4-WA-01
assigned_agent: UNASSIGNED
predecessors: [KI-W4-S004]
successor_reserved_for: WINDOW-AGENT
writable_file: email_scraper/src/prisma-run-repository.js
file_operation: MODIFY
starting_file_digest: c719ed27276cba78bbb140cf8a1241b19af426db82e5dedf40a99363a89da173
starting_repository_change_set_digest: b33384c5ceb700902be88af820cbd0998699dbbdd2970e0d571c649107479ca5
read_only_scope:
  - email_scraper/src/prisma-run-repository.js
  - email_scraper/src/keyword-intelligence/query-mapper.js
  - email_scraper/src/prisma/schema.prisma
  - KEYWORD_INTELLIGENCE_DECISION_LEDGER.md lines 1365-1429 (DEC-KI-033 run-construction and edit clauses)
  - KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md lines 1900-1935 (KI-W4-T2)
authorized_actions:
  - read every file listed in read_only_scope
  - apply the ordered transformation to exactly writable_file and no other file
  - run the exact LOCAL_NOW checks of this block
  - report the exact handoff to the window agent
prohibited_actions:
  - edit any second file
  - edit KEYWORD_INTELLIGENCE_KI_W4_SUBWINDOW_CHECKLIST.md, KEYWORD_INTELLIGENCE_KI_W4_SUBWINDOW_STATE.md, or KEYWORD_INTELLIGENCE_KI_W4_SUBWINDOW_EVIDENCE.md
  - start the successor or any later sub-window
  - communicate with the parent agent
  - mutate external state (providers, AWS, databases, queues, buckets)
  - weaken any existing test, fixture, or oracle
may_start_successor: false
```

Mechanical trace: `REQ-KI-015/016`; `DEC-KI-017/033`; `KI-W4-T2`; consumed
by `S006` (`createRun` callback composition); fenced by `S010` `W4-D01`,
`D02`, `D06` and the edit path by `W4-Q02`/`W4-Q04`.

Exact transformation:

1. Export `newRunId()` immediately after `stableLeadId` (line 169): its body
   returns exactly the value of the existing private `runId()` formula
   (line 71, `` `run_${randomBytes(18).toString("base64url")}` ``) with no
   other effect.
2. Add instance methods `createKeywordResearchRun(tx, input)` and
   `createKeywordResearchQueries(tx, input)` to `PrismaRunRepository`
   immediately before `replaceEditableQueries` (line 1202), importing
   `mapSelectionToQueries` from `./keyword-intelligence/query-mapper.js`
   beside the existing serializer imports (lines 10–17).
3. `createKeywordResearchRun(tx, input)`: requires exactly
   `{ research, runId, now, items, selectionRevision, selectionFingerprint,
   snapshot }`; derives categories as the ordered normalized research seeds
   mapped to `{ originalShopType: seed, shopType: seed,
   businessQualifier: "unspecified" }`; calls the existing
   `runCreateData(research.ownerId, categories, runId)`; performs one
   `tx.run.create` overriding only: `state: "awaiting_query_confirmation"`,
   `phase: "query_review"`, `stage: "awaiting_query_confirmation"`,
   `queryRevision: 1`, `queryPlanReadyAt: now`, `keywordResearchId:
   research.id`, `keywordSelectionRevision: selectionRevision`,
   `keywordSelectionSnapshot: snapshot`, `queryPlanSource:
   "keyword_research"`; `confirmedQueryRevision`, `queriesConfirmedAt`, and
   every lease field remain null; returns the created row. It performs no
   queue/planner interaction.
4. `createKeywordResearchQueries(tx, input)`: requires exactly
   `{ run, items, now, snapshot }`; requires `items` deep-equal
   `snapshot.items`; maps once through `mapSelectionToQueries(items)`;
   performs one `tx.runQuery.createMany`; requires the count to equal N;
   returns the same constructed ordered rows without a read. Each row
   carries the mapped query, `source: "generated"`, `validationState:
   "pending"`, `generationReason: "keyword_research"`, its stable
   `keywordResearchItemId`, and `categoryIndex` equal to the index of its
   first `sourceSeeds` member in the research seed array; missing source
   membership throws.
5. `replaceEditableQueries` (lines 1202–1274): after the owner/state/revision
   read (line 1220) and before the revision CAS `updateMany` (line 1221),
   branch on `run.queryPlanSource`: for `"keyword_research"` require the
   incoming query-ID set to equal the persisted query-ID set, every persisted
   row to have a unique non-null `keywordResearchItemId`, every incoming
   `categoryIndex` to equal that row's persisted `categoryIndex`, and no
   incoming row without a matching ID; replacement rows preserve the exact
   persisted `id`, `keywordResearchItemId`, `createdAt`, `queryScore`,
   `generationReason`, `sourceUrls`, and `categoryVocabulary`; reorder-only
   changes update only `sequence`/`updatedAt` preserving `source` and probe
   evidence; a query-text change also sets `source: "user_edited"`,
   `validationState: "pending"`, clears rejection/probe fields, and updates
   `query`/`updatedAt`. For `"legacy"` the existing rows mapping
   (lines 1238–1266) is byte-for-byte unchanged, including `user_added`
   rows. Any other discriminator value throws
   `PipelineInvariantError("PIPELINE_INPUT_CONFLICT")` before the CAS. The
   delete+bulk-create stays inside the existing revision-CAS transaction.
6. Preserved: every other method, `queryId()`/`intentId()`/lease-token
   formulas, transaction and lease semantics, all exports.
7. Forbidden: schema edits, N+1 reads, recomputing the snapshot, queueing
   the run, relaxing CAS ordering, editing `runCreateData` for legacy runs.

Exact checks (`LOCAL_NOW`, from `email_scraper/`):

- C1 `node --check src/prisma-run-repository.js` → exit 0.
- C2 `node --test test/prisma-run-repository.test.js` → exit 0 (legacy
  repository suite green, including existing `replaceEditableQueries`
  coverage). Forbidden: weakening assertions.
- C3 `grep -c "createKeywordResearchRun\|createKeywordResearchQueries" src/prisma-run-repository.js`
  → at least `4` (declaration plus export/import sites) and
  `grep -c "export function newRunId" src/prisma-run-repository.js` → `1`.
- Coverage: zero local case IDs (`W4-D01/D02/D06`, `W4-Q02/Q04` execute at
  `S009`/I001 `V3`).
- Expected workspace write set: `M email_scraper/src/prisma-run-repository.js`
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

### 5.6 `KI-W4-S006` — keyword research API service (CREATE)

```yaml
subwindow_id: KI-W4-S006
type: FILE
parent_window_id: KI-W4
parent_assignment_id: ASG-KI-W4-WA-01
assigned_agent: UNASSIGNED
predecessors: [KI-W4-S002, KI-W4-S003, KI-W4-S005]
successor_reserved_for: WINDOW-AGENT
writable_file: email_scraper/src/keyword-intelligence/api.js
file_operation: CREATE
starting_file_digest: ABSENT
starting_repository_change_set_digest: b33384c5ceb700902be88af820cbd0998699dbbdd2970e0d571c649107479ca5
read_only_scope:
  - email_scraper/src/keyword-intelligence/repository.js
  - email_scraper/src/keyword-intelligence/config.js
  - email_scraper/src/keyword-intelligence/export.js
  - email_scraper/src/api-serializer.js
  - email_scraper/src/prisma-run-repository.js
  - KEYWORD_INTELLIGENCE_DECISION_LEDGER.md lines 1281-1364, 1479-1521 (DEC-KI-033 service, serialization, export clauses), 404-445 (DEC-KI-019)
  - KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md lines 1790-1900 (KI-W4-T1)
authorized_actions:
  - read every file listed in read_only_scope
  - apply the ordered transformation to exactly writable_file and no other file
  - run the exact LOCAL_NOW checks of this block
  - report the exact handoff to the window agent
prohibited_actions:
  - edit any second file
  - edit KEYWORD_INTELLIGENCE_KI_W4_SUBWINDOW_CHECKLIST.md, KEYWORD_INTELLIGENCE_KI_W4_SUBWINDOW_STATE.md, or KEYWORD_INTELLIGENCE_KI_W4_SUBWINDOW_EVIDENCE.md
  - start the successor or any later sub-window
  - communicate with the parent agent
  - mutate external state (providers, AWS, databases, queues, buckets)
  - weaken any existing test, fixture, or oracle
may_start_successor: false
```

Mechanical trace: `REQ-KI-001/002/005`–`009/015`–`018`; `DEC-KI-003/014/
015/017/019/033`; `KI-W4-T1`; consumed by `S007` (all five routes); exercised
by `W4-A01`–`A08` and `W4-S01`–`S06`.

Exact transformation:

1. Create `src/keyword-intelligence/api.js` exporting only
   `createKeywordResearchApi` with the frozen factory signature and defaults
   of `I-F6` (imports: `newResearchId` from `./repository.js`, `newRunId`
   from `../prisma-run-repository.js`, `keywordResearchConfigV1` from
   `./config.js`, `serializeKeywordResearch`/`serializeSelectionItem` from
   `../api-serializer.js`, `serializeKeywordsCsv` from `./export.js`).
2. `createResearch({ ownerId, seeds })`: strict seed validation — array of
   1–5 strings, each 1–100 code points after NFKC/trim/collapse, duplicate
   rejection under case folding; invalid input returns the typed invalid
   outcome with zero repository and zero dispatcher calls; valid input calls
   `keywordRepository.create` once and calls `dispatchInitialize` exactly
   once after the commit; a failed or throwing dispatcher returns the same
   queued serialized view (durable row recoverable); returns
   `{ outcome: "created", research }` with `serializeKeywordResearch` output.
3. `getResearch({ ownerId, researchId })`: one `getOwnedApiView` call;
   `not_found` maps to the typed not-found outcome; an unsupported persisted
   contract version maps to the typed contract-mismatch outcome; otherwise
   `{ outcome: "found", research }` with the serialized view.
4. `saveSelection({ ownerId, researchId, expectedRevision, items })`:
   canonicalizes each item with `classifyKeywordForSelection` and the
   accepted conflict analyzer (`DEC-KI-014/015` semantics as already
   implemented by the accepted `keywordRepository.saveSelection`), then
   performs one revision-CAS save; returns the updated serialized view or
   the typed stale/conflict/not-found outcomes; zero client-authority
   repair.
5. `createRun({ ownerId, researchId, expectedSelectionRevision,
   clientRequestId })`: validates `clientRequestId` against
   `/^[A-Za-z0-9_-]{16,80}$/`; reads the completed research; builds
   `selectionFingerprint` and the immutable `keyword-run-snapshot-v1`
   snapshot exactly as A3 lines 1355–1364; invokes
   `keywordRepository.createRun` once with the exact callback composition of
   `I-F3`; maps outcomes to `{ outcome: "created" | "replayed", run,
   statusUrl }` (serialized strict `SerializedRun` plus
   `/api/runs/<runId>`) or the typed not-completed/stale/conflict/handoff
   outcomes; no `queueDrain`, no planner, no live-selection snapshot.
6. `exportCsv({ ownerId, researchId, searchParams })`: parses exactly the
   `DEC-KI-019` parameter contract (unknown names, duplicate non-`flag`
   parameters, malformed bounds, empty normalized values rejected); applies
   the conjunctive pure filter predicate and persisted result-keyword order
   of A3 lines 1507–1520 (market overlay rules included); returns
   `{ outcome: "found", csv }` where `csv` is the `serializeKeywordsCsv`
   UTF-8 LF body, or the typed not-found/contract outcomes; zero writes.
7. No environment reads, no provider calls, no direct Prisma access, no
   logging of seeds beyond the accepted safe fields; the module keeps all
   repository outcomes opaque and typed.

Exact checks (`LOCAL_NOW`, from `email_scraper/`):

- C1 `node --check src/keyword-intelligence/api.js` → exit 0.
- C2 import smoke:
  `node --input-type=module -e "const m = await import('./src/keyword-intelligence/api.js'); const keys = Object.keys(m).sort(); if (JSON.stringify(keys) !== JSON.stringify(['createKeywordResearchApi'])) { throw new Error('export set: ' + keys); } if (typeof m.createKeywordResearchApi !== 'function') throw new Error('not a function'); console.log('OK');"`
  → prints `OK`, exit 0; activation witness: the module graph
  (`repository.js`, `prisma-run-repository.js`, `api-serializer.js`,
  `config.js`, `export.js`) imports cleanly without a database connection.
- Coverage: zero local case IDs (`W4-A01`–`A08` execute in `S009`).
- Expected workspace write set: `A email_scraper/src/keyword-intelligence/api.js`
  only (new file).

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

### 5.7 `KI-W4-S007` — server routes, injection, and dispatch branches

```yaml
subwindow_id: KI-W4-S007
type: FILE
parent_window_id: KI-W4
parent_assignment_id: ASG-KI-W4-WA-01
assigned_agent: UNASSIGNED
predecessors: [KI-W4-S004, KI-W4-S006]
successor_reserved_for: WINDOW-AGENT
writable_file: email_scraper/src/server.js
file_operation: MODIFY
starting_file_digest: 73b2384ac85b36f4ae445d6a49fc00b0d03369b382eac278d944970c170fc2ec
starting_repository_change_set_digest: b33384c5ceb700902be88af820cbd0998699dbbdd2970e0d571c649107479ca5
read_only_scope:
  - email_scraper/src/server.js
  - email_scraper/src/query-review.js
  - email_scraper/src/keyword-intelligence/api.js
  - email_scraper/src/keyword-intelligence/repository.js
  - email_scraper/src/aws-pipeline/services/confirmed-query-dispatcher.js
  - KEYWORD_INTELLIGENCE_DECISION_LEDGER.md lines 404-445 (DEC-KI-019), 1457-1506 (DEC-KI-033 server clauses)
  - KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md lines 1930-1991 (KI-W4-T3)
authorized_actions:
  - read every file listed in read_only_scope
  - apply the ordered transformation to exactly writable_file and no other file
  - run the exact LOCAL_NOW checks of this block
  - report the exact handoff to the window agent
prohibited_actions:
  - edit any second file
  - edit KEYWORD_INTELLIGENCE_KI_W4_SUBWINDOW_CHECKLIST.md, KEYWORD_INTELLIGENCE_KI_W4_SUBWINDOW_STATE.md, or KEYWORD_INTELLIGENCE_KI_W4_SUBWINDOW_EVIDENCE.md
  - start the successor or any later sub-window
  - communicate with the parent agent
  - mutate external state (providers, AWS, databases, queues, buckets)
  - weaken any existing test, fixture, or oracle
may_start_successor: false
```

Mechanical trace: `REQ-KI-001/002/019`; `EXC-KI-005`; `DEC-KI-016/019/033`;
`KI-W4-T3`; exercised by `W4-S01`–`S06`, `W4-Q02`, `W4-Q07`, `W4-NC02/NC10/
NC15`, and legacy regressions.

Exact transformation:

1. Imports: add `validateResearchBackedQueryList` and
   `validateResearchBackedConfirmedQueryRows` to the existing
   `./query-review.js` import (line 42); add
   `createKeywordResearchApi` from
   `./keyword-intelligence/api.js` and `PrismaKeywordResearchRepository`
   from `./keyword-intelligence/repository.js`.
2. Insert `requestedKeywordResearchId(pathname, suffix = "")` immediately
   after `requestedIntentId` (line 514): mirrors `requestedRunId`
   (lines 468–484) with pattern
   `^/api/keyword-research/([^/]+)(/<suffix>)?$`, decodes with the same
   try/catch, validates exactly `/^kr_[A-Za-z0-9_-]{24}$/u`, and throws
   `400 KEYWORD_RESEARCH_INPUT_INVALID` on decode or pattern failure.
3. `createLeadServer` (line 1388): add optional injected parameters
   `keywordResearchApi` and `researchQueryValidationPipeline =
   validateResearchBackedConfirmedQueryRows`; when `keywordResearchApi` is
   absent construct exactly one service:
   `createKeywordResearchApi({ keywordRepository: new PrismaKeywordResearchRepository(repository.prisma), runRepository: repository, now: () => currentDate(now), dispatchInitialize: <lazy> })`
   where the lazy `dispatchInitialize` awaits
   `pipelineRuntimeFactory(...)`, then calls
   `runtime.dispatcher.sendOne(runtime.config.awsPipelineKeywordResearchQueueUrl,
   message, keywordMessageSchema)`; a missing dispatcher or missing/invalid
   queue URL returns a failed-send result without an SQS call. No
   environment variable read; no new config key.
4. Five route blocks in `handle()`, inserted after the existing
   `POST /api/runs` block (ending line 1654) and before the `PUT` block:
   `POST /api/keyword-research` (202, `Location` absent, body
   `{ research }`); `GET /api/keyword-research/:id` (200 `{ research }`);
   `PUT /api/keyword-research/:id/selection` (200 `{ research }`); `POST
   /api/keyword-research/:id/runs` (201 new / 200 identical replay, body
   `{ run, statusUrl }`); `GET /api/keyword-research/:id/export.csv` (CSV
   body with the frozen headers of `I-F7`). Owner identity comes only from
   `trustedUserId(request)`; bodies are read with `readJsonBody` and unknown
   keys map to `400 KEYWORD_RESEARCH_INPUT_INVALID`; the service outcome
   unions map to the frozen codes of §3.3 with the existing `ApiError`
   helper; unexpected failures use the existing safe 500 mapper.
5. Query edit/start discriminator: in the existing `PUT .../queries` handler
   (line 1656) select `validateResearchBackedQueryList` exactly when the
   loaded `run.queryPlanSource === "keyword_research"`, otherwise the
   existing `validateEditableQueryList` path unchanged; the same selection
   applies in the explicit-start handler (line 1715) and in both local and
   AWS confirmation branches inside `executeRun` (line 927), passing the
   run's `keywordSelectionSnapshot` as `options.snapshot`; any other
   discriminator throws `PipelineInvariantError("PIPELINE_INPUT_CONFLICT")`
   before edit, confirmation, probe, or dispatch.
6. `drainQueue` (line 1493) passes `queryPlanSource` and
   `keywordSelectionSnapshot` from the claimed run into `executeRun`.
7. Preserved: every existing route, status code, header, and legacy
   validator call; `serializeRun`/`serializeRunQuery` usage unchanged (the
   conditional keys come from `S002`); no route removed or renamed.
8. Forbidden: frontend edits, provider/AWS calls, reading stage progress
   from S3/queue, client-supplied owner identity, new config keys,
   `queueDrain` on the research run route.

Exact checks (`LOCAL_NOW`, from `email_scraper/`):

- C1 `node --check src/server.js` → exit 0.
- C2 `node --test test/server.test.js test/query-review-server.test.js` →
  exit 0 (legacy server behavior and frozen fixtures deep-equal; localhost
  `listen EPERM` in a restricted sandbox is re-run with sandbox approval,
  never silently accepted). Forbidden: weakening fixtures.
- C3 `grep -c "requestedKeywordResearchId" src/server.js` → at least `2`
  (definition plus route uses).
- Coverage: zero local case IDs (`W4-S01`–`S06` execute in `S009`).
- Expected workspace write set: `M email_scraper/src/server.js` only.

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


### 5.8 `KI-W4-S008` — enforcement manifest fixture (CREATE)

```yaml
subwindow_id: KI-W4-S008
type: FILE
parent_window_id: KI-W4
parent_assignment_id: ASG-KI-W4-WA-01
assigned_agent: UNASSIGNED
predecessors: [KI-W4-S007]
successor_reserved_for: WINDOW-AGENT
writable_file: email_scraper/test/fixtures/keyword-intelligence/ki-w4-enforcement-manifest-v1.json
file_operation: CREATE
starting_file_digest: ABSENT
starting_repository_change_set_digest: b33384c5ceb700902be88af820cbd0998699dbbdd2970e0d571c649107479ca5
read_only_scope:
  - KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md lines 1993-2060 (KI-W4-T4 manifest items), 2107-2162 (literal case matrix)
  - KEYWORD_INTELLIGENCE_DECISION_LEDGER.md lines 1521-1529 (DEC-KI-033 enforcement set)
authorized_actions:
  - read every file listed in read_only_scope
  - apply the ordered transformation to exactly writable_file and no other file
  - run the exact LOCAL_NOW checks of this block
  - report the exact handoff to the window agent
prohibited_actions:
  - edit any second file
  - edit KEYWORD_INTELLIGENCE_KI_W4_SUBWINDOW_CHECKLIST.md, KEYWORD_INTELLIGENCE_KI_W4_SUBWINDOW_STATE.md, or KEYWORD_INTELLIGENCE_KI_W4_SUBWINDOW_EVIDENCE.md
  - start the successor or any later sub-window
  - communicate with the parent agent
  - mutate external state (providers, AWS, databases, queues, buckets)
  - weaken any existing test, fixture, or oracle
may_start_successor: false
```

Mechanical trace: `DEC-KI-033` enforcement set; `KI-W4-T4` items 1/5/9;
consumed by `S009` (`W4-C01`) and `S010` (D-registry); frozen by the A4
header digest and `KI-W4-V6`.

Exact transformation:

1. Create the fixture with exactly this content (2-space JSON, one trailing
   LF, 764 bytes, sha256
   `417f25dd2ab68c30a5ccfe19d3209afb4386435ef852f75dcf87af9f075b8c51`):

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

2. No metadata, no other keys, no inferred-name registration; the ID union
   (34 unique) hashes under §3.1 to
   `86810ce87a79426bb972be2e2827abc3806835190135d17769b52c33e7bb2203`.

Exact checks (`LOCAL_NOW`, from `email_scraper/`):

- C1 `node -e "const t=require('fs').readFileSync('test/fixtures/keyword-intelligence/ki-w4-enforcement-manifest-v1.json','utf8'); const m=JSON.parse(t); const ids=Object.values(m.groups).flat(); const s=[...ids].sort(); if(s.length!==34||new Set(s).size!==34)throw new Error('bad set'); const d=require('crypto').createHash('sha256').update(s.map(x=>x+'\n').join('')).digest('hex'); if(d!=='86810ce87a79426bb972be2e2827abc3806835190135d17769b52c33e7bb2203')throw new Error('digest'); if(t!==JSON.stringify(m,null,2)+'\n')throw new Error('rendering'); console.log('OK');"`
  → prints `OK`, exit 0. Coverage: `W4-C01` registration half (execution in
  `S009`).
- Expected workspace write set: `A email_scraper/test/fixtures/keyword-intelligence/ki-w4-enforcement-manifest-v1.json`
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

### 5.9 `KI-W4-S009` — non-database enforcement registry (CREATE)

```yaml
subwindow_id: KI-W4-S009
type: FILE
parent_window_id: KI-W4
parent_assignment_id: ASG-KI-W4-WA-01
assigned_agent: UNASSIGNED
predecessors: [KI-W4-S006, KI-W4-S007, KI-W4-S008]
successor_reserved_for: WINDOW-AGENT
writable_file: email_scraper/test/keyword-intelligence-api.test.js
file_operation: CREATE
starting_file_digest: ABSENT
starting_repository_change_set_digest: b33384c5ceb700902be88af820cbd0998699dbbdd2970e0d571c649107479ca5
read_only_scope:
  - email_scraper/test/fixtures/keyword-intelligence/ki-w4-enforcement-manifest-v1.json
  - email_scraper/src/keyword-intelligence/api.js
  - email_scraper/src/server.js
  - email_scraper/src/query-review.js
  - email_scraper/src/api-serializer.js
  - email_scraper/src/keyword-intelligence/query-mapper.js
  - email_scraper/test/server.test.js
  - email_scraper/test/query-review-server.test.js
  - email_scraper/test/keyword-intelligence-repository.test.js
  - KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md lines 1993-2060 (KI-W4-T4), 2107-2183 (case matrix and control definitions), 2195-2204 (V2)
  - KEYWORD_INTELLIGENCE_DECISION_LEDGER.md lines 1521-1556 (DEC-KI-033 enforcement/fidelity clauses)
authorized_actions:
  - read every file listed in read_only_scope
  - apply the ordered transformation to exactly writable_file and no other file
  - run the exact LOCAL_NOW checks of this block
  - report the exact handoff to the window agent
prohibited_actions:
  - edit any second file
  - edit KEYWORD_INTELLIGENCE_KI_W4_SUBWINDOW_CHECKLIST.md, KEYWORD_INTELLIGENCE_KI_W4_SUBWINDOW_STATE.md, or KEYWORD_INTELLIGENCE_KI_W4_SUBWINDOW_EVIDENCE.md
  - start the successor or any later sub-window
  - communicate with the parent agent
  - mutate external state (providers, AWS, databases, queues, buckets)
  - weaken any existing test, fixture, or oracle
may_start_successor: false
```

Mechanical trace: `KI-W4-T4`; all 28 non-DB IDs `W4-A01`–`A08`, `W4-S01`–
`S06`, `W4-Q01`–`Q08`, `W4-C01`–`C06`; controls `W4-NC01`–`NC18`; scenarios
`SCN-KI-003/008/009/014/015`; gates `KI-W4-V2` (run once by I001 on frozen
inputs) — the leaf proves the file green once locally.

Exact transformation:

1. Create the test file using `node:test`; it parses the `S008` fixture,
   derives `required` as the 34-ID union minus `handoff_database` (28 IDs),
   and registers every ID exactly once in an explicit registry object.
2. Execution order is fixed: `api_component → server_routes → query_review →
   conformance`. Each case is one named subtest whose witness activates the
   production path (fake collaborators injected into
   `createKeywordResearchApi` for `api_component`; `createLeadServer` with an
   injected fake API and real `http` request/response doubles for
   `server_routes`; `validateResearchBackedQueryList`/
   `validateResearchBackedConfirmedQueryRows` with mock probe/seed snapshots
   for `query_review`) and whose oracle asserts the exact A4 matrix row
   (stimulus, expected behavior, and forbidden operations quoted from the
   matrix at A4 lines 2129–2162). An ID is pushed to `executed` only after
   its witness and oracle both hold; the file asserts
   `required = registered = executed` with zero skips before exiting.
3. The conformance group implements `W4-C01` (manifest parse + digest
   recompute), `W4-C02` (certificate enumeration), `W4-C03` (witness/oracle
   completeness over the 28 records), `W4-C04` (all 18 controls
   `W4-NC01`–`NC18` run against captured fakes/evidence: unchanged oracle
   passes → injected defect throws `AssertionError` → fresh witness passes;
   source mutation forbidden), `W4-C05` (substitute fidelity table asserts
   each fake's exact supported claim), and `W4-C06` (static import-set
   inspection proving no prohibited import).
4. The file emits exactly one TAP diagnostic line beginning
   `KI_W4_EXECUTION_CERTIFICATE=` followed by compact JSON
   `{registry:"non_db",required,registered,executed,skipped,
   activationWitnesses,oracleFailures,digests:{required,registered,executed}}`
   with all arrays UTF-8-sorted and every digest using §3.1.
5. Test substitutes are bounded to the fidelity classes of A4 lines
   2185–2193; no production source mutation, no network, no database, no
   filesystem write outside the runner's own outputs.
6. Existing accepted tests receive no edits from this leaf; this file is
   additive only.

Exact checks (`LOCAL_NOW`, from `email_scraper/`):

- C1 `node --check test/keyword-intelligence-api.test.js` → exit 0.
- C2 `node --test --test-isolation=none test/keyword-intelligence-api.test.js`
  → exit 0, all subtests pass; activation witness: the emitted certificate
  line shows `required=registered=executed` = the sorted 28-ID set, `skipped:
  []`, `oracleFailures: []`, and digests over §3.1. Forbidden outcomes: any
  skip, filtered ID, duplicate registration, unexpected ID, or missing
  witness.
- Coverage (V3 local): 28 required = 28 registered = 28 executed, controls
  18/18 falsified; `W4-D01`–`D06` remain allocated to `S010`/I001 `KI-W4-V3`.
- Expected workspace write set: `A email_scraper/test/keyword-intelligence-api.test.js`
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

### 5.10 `KI-W4-S010` — database handoff registry (CREATE)

```yaml
subwindow_id: KI-W4-S010
type: FILE
parent_window_id: KI-W4
parent_assignment_id: ASG-KI-W4-WA-01
assigned_agent: UNASSIGNED
predecessors: [KI-W4-S006, KI-W4-S007, KI-W4-S008]
successor_reserved_for: WINDOW-AGENT
writable_file: email_scraper/test/keyword-intelligence-handoff.integration.test.js
file_operation: CREATE
starting_file_digest: ABSENT
starting_repository_change_set_digest: b33384c5ceb700902be88af820cbd0998699dbbdd2970e0d571c649107479ca5
read_only_scope:
  - email_scraper/test/helpers/isolated-postgres.js
  - email_scraper/test/keyword-intelligence-repository.integration.test.js
  - email_scraper/test/prisma-run-repository.integration.test.js
  - email_scraper/src/keyword-intelligence/repository.js
  - email_scraper/src/prisma-run-repository.js
  - KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md lines 2151-2156 (D-matrix), 2205-2209 (V3)
  - KEYWORD_INTELLIGENCE_DECISION_LEDGER.md lines 1365-1413 (DEC-KI-033 handoff clauses)
authorized_actions:
  - read every file listed in read_only_scope
  - apply the ordered transformation to exactly writable_file and no other file
  - run the exact LOCAL_NOW checks of this block
  - report the exact handoff to the window agent
prohibited_actions:
  - edit any second file
  - edit KEYWORD_INTELLIGENCE_KI_W4_SUBWINDOW_CHECKLIST.md, KEYWORD_INTELLIGENCE_KI_W4_SUBWINDOW_STATE.md, or KEYWORD_INTELLIGENCE_KI_W4_SUBWINDOW_EVIDENCE.md
  - start the successor or any later sub-window
  - communicate with the parent agent
  - mutate external state (providers, AWS, databases, queues, buckets)
  - weaken any existing test, fixture, or oracle
may_start_successor: false
```

Mechanical trace: `KI-W4-T4`; `W4-D01`–`D06`; guards
`ALLOW_DATABASE_TESTS`; isolated disposable schema via
`test/helpers/isolated-postgres.js` (non-pooled direct connection, explicit
`search_path`, `current_schema()` verification, never `public`); execution
owned by I001 `KI-W4-V3`.

Exact transformation:

1. Create the integration file: one outer harness creates one isolated
   disposable schema, registers `W4-D01`–`D06` as six sequential named
   subtests in manifest order, executes each exactly once with zero skip,
   and cleans that exact schema in `finally` (proving schema-name absence);
   no shared or `public` cleanup.
2. Case stimuli/oracles follow A4 lines 2151–2156 exactly: `D01` real Prisma
   new handoff N=1 then N=100 with exactly the five named repository
   operations per handoff; `D02` injected throws at Run create and
   RunQuery `createMany` plus invalid callback outputs after writes,
   proving rollback and the mapped conflict with zero partial members;
   `D03` owner-B/stale-revision/conflicted predicates with zero writes;
   `D04` concurrent equal client key+fingerprint replay (one Run) versus
   unequal revision/fingerprint conflict; `D05` post-handoff selection edit
   cannot alter the snapshot (deep-equal pre-edit values, exactly N query
   links); `D06` legacy run create/load/edit plus 100-row research edit with
   bounded reads (no N+1).
3. The file emits exactly one TAP diagnostic line
   `KI_W4_EXECUTION_CERTIFICATE=` with `registry:"database"` and the six-ID
   arrays/digests per `I-F8`. The file skips itself (zero subtests executed,
   certificate still emitted with `skipped` listing all six IDs) only when
   `ALLOW_DATABASE_TESTS` is unset — the I001 `KI-W4-V3` run sets it.
4. No production mutation, no second database, no cross-test schema reuse.

Exact checks (`LOCAL_NOW`, from `email_scraper/`):

- C1 `node --check test/keyword-intelligence-handoff.integration.test.js`
  → exit 0.
- C2 `grep -c "W4-D0" test/keyword-intelligence-handoff.integration.test.js`
  → at least `6` (registration sites).
- Coverage: `W4-D01`–`D06` registered here; execution is
  `DEFERRED_TO_INTEGRATION` to `KI-W4-I001` gate `V3` (leaf must not run the
  database suite).
- Expected workspace write set: `A email_scraper/test/keyword-intelligence-handoff.integration.test.js`
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

### 5.11 `KI-W4-I001` — whole-window integration assessment

```yaml
subwindow_id: KI-W4-I001
type: ASSESS
parent_window_id: KI-W4
parent_assignment_id: ASG-KI-W4-WA-01
assigned_agent: KI-W4-WINDOW-AGENT
predecessors: [KI-W4-S010]
successor_reserved_for: WINDOW-AGENT
writable_file: none
file_operation: none
starting_file_digest: N/A
starting_repository_change_set_digest: b33384c5ceb700902be88af820cbd0998699dbbdd2970e0d571c649107479ca5
read_only_scope:
  - all ten leaf files plus S1/S2/S3
  - KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md lines 2195-2214 (V1-V4)
authorized_actions:
  - independently review every leaf handoff per sub-window standard section 8
  - execute gates `KI-W4-V1`-`KI-W4-V4` exactly once each on frozen final inputs
  - append the section 12.4 integration certificate to S3
  - set S2 to READY_FOR_PARENT_REVIEW and produce the section 12.5 handoff
prohibited_actions:
  - any implementation-file write (a diagnosed defect opens KI-W4-C001+)
  - repeating a passed stateful gate without a documented invalidation
  - claiming parent acceptance or beginning KI-W5
may_start_successor: false
```

Frozen gates (A4 lines 2195–2214, executed from `email_scraper/`):

- **`KI-W4-V1`** assembled write-set proof: `git -C email_scraper status --porcelain`
  lists exactly the ten planned paths (six `M`, four `A`/untracked) and the
  per-LF set digest equals `fe48d14ebec1dffa058cf91cfa9ec10982d4ceaa4c63e0cb9280cabf39a4a59b`;
  root change set equals the §2 inventory plus the three subordinate
  artifacts and the ten backend paths; no second file changed.
- **`KI-W4-V2`** non-database registry, exactly once:
  `node --test --test-isolation=none test/keyword-intelligence-api.test.js`
  → all 28 IDs pass with required=registered=executed equality, zero skips,
  activation witnesses present; no localhost sandbox failure silently
  accepted.
- **`KI-W4-V3`** database registry, exactly once against one isolated
  non-production database:
  `ALLOW_DATABASE_TESTS=true node --test --test-isolation=none test/keyword-intelligence-handoff.integration.test.js`
  → six sequential subtests, zero skips, cleanup proven; `V6` merges both
  certificates and independently asserts the 34-ID global union and digest
  `86810ce8…`.
- **`KI-W4-V4`** on the same frozen source/tests: `npm test` once (existing legacy,
  keyword parity, selection, mapper, server, query-review, repository suites
  green; guarded unrelated DB suites may skip only under their existing
  opt-in) and `npm run check:secrets` once (clean).

Failure handling: any failing gate is diagnosed to exactly one owning file;
the window agent appends a corrective sub-window `KI-W4-C001`, `KI-W4-C002`,
… (single file from the same ten-file set, §12.2 certificate first) and
re-runs only the gates its invalidation rule marks stale (§9.5, A4
verification economy).


---

## 6. Coverage allocation and accounting

### 6.1 Case-to-leaf allocation (34 IDs, zero unallocated)

| Group | IDs | Registered in | Executed in | Gate |
|---|---|---|---|---|
| `api_component` | `W4-A01`–`A08` | `S009` | `S009` | `V2` (I001 re-run on frozen inputs) |
| `server_routes` | `W4-S01`–`S06` | `S009` | `S009` | `V2` |
| `query_review` | `W4-Q01`–`Q08` | `S009` | `S009` | `V2` |
| `conformance` | `W4-C01`–`C06` | `S009` | `S009` (`C06` also inspects the assembled set) | `KI-W4-V2` + `KI-W4-V1` |
| `handoff_database` | `W4-D01`–`D06` | `S010` | I001 `KI-W4-V3` only | `KI-W4-V3` + `KI-W4-V6` merge |

### 6.2 Control-to-case allocation (`W4-NC01`–`NC18`)

`W4-NC01`→`W4-A03`,`W4-S03`; `W4-NC03`→`W4-A03`,`W4-S03`;
`W4-NC02`→`W4-A01`,`W4-A02`,`W4-S02`; `W4-NC04`→`W4-A04`,`W4-S04`,`W4-D03`;
`W4-NC05`→`W4-A05`,`W4-D01`,`W4-D02`; `W4-NC06`→`W4-A05`,`W4-D05`;
`W4-NC07`→`W4-Q02`,`W4-Q08`; `W4-NC08`→`W4-Q02`,`W4-Q04`,`W4-Q08`;
`W4-NC09`→`W4-Q05`,`W4-Q06`; `W4-NC10`→`W4-Q07`,`W4-S06`,`W4-D06`;
`W4-NC11`→`W4-A07`,`W4-S06`; `W4-NC12`→`W4-C01`–`W4-C03`,`W4-C05`,`W4-C06`;
`W4-NC13`→`W4-A06`; `W4-NC14`→`W4-A08`; `W4-NC15`→`W4-S01`;
`W4-NC16`→`W4-Q01`; `W4-NC17`→`W4-Q03`; `W4-NC18`→`W4-D04`.
All 18 controls execute inside `S009` `W4-C04` against captured
fakes/evidence; the database-side controls re-verify at I001 `KI-W4-V3` through
their `D`-cases. Each control run proves: unchanged oracle passes → injected
defect throws `AssertionError` → fresh unchanged witness passes.

### 6.3 Parent-item mapping (unmapped counts all zero)

- Requirements: `REQ-KI-001/002` → `S002`,`S003`,`S006`,`S007`,`S009`;
  `REQ-KI-005`–`009` → `S001`–`S004`,`S006`,`S009`; `REQ-KI-010`–`013` →
  `S004`,`S007`,`S009`; `REQ-KI-015/016` → `S003`,`S005`,`S006`,`S010`;
  `REQ-KI-017`–`019` → `S002`,`S006`,`S007`,`S009`; `REQ-KI-021` → `S006`,
  `S009` (`A08`).
- Decisions: `DEC-KI-003` (`S006`); `DEC-KI-012` (`S002`); `DEC-KI-014/015`
  (`S001`,`S002`,`S006`); `DEC-KI-016` (`S004`,`S005`,`S007`); `DEC-KI-017`
  (`S003`,`S005`,`S006`,`S010`); `DEC-KI-019` (`S002`,`S006`,`S007`,`S009`);
  `DEC-KI-021` (`S010` `D06`); `DEC-KI-033` (every leaf).
- Tasks: `KI-W4-T1` → `S001`,`S002`,`S003`,`S006`; `KI-W4-T2` → `S005`;
  `KI-W4-T3` → `S004`,`S007`; `KI-W4-T4` → `S008`,`S009`,`S010` (+`I001`
  gates).
- Scenarios: `SCN-KI-003` → `S006`/`S009` (`A*`,`S*`); `SCN-KI-008` →
  `S006`/`S009`/`S010` handoff cases; `SCN-KI-009` → `S009`; `SCN-KI-014` →
  `S004`/`S009` (`Q*`); `SCN-KI-015` → `S006`/`S010` (`D*`).
- Preconditions: `KI-W4-P1` (A5 assignment) satisfied at entry
  (`EV-KI-W4-S01`); `KI-W4-P2` (backend clean at `d98ad53c…`) verified at
  entry and at every leaf preflight (P2).

### 6.4 Coverage accounting rule (`KI-W4-V6`; A4 names this merge check `V6`)

At I001, `required` = the literal 34-ID manifest set; `registered` = the
union of the two emitted certificates' `registered` arrays; `executed` = the
union of their `executed` arrays. Acceptance requires set equality of all
three, per-set §3.1 digests equal to the manifest digest
`86810ce87a79426bb972be2e2827abc3806835190135d17769b52c33e7bb2203` for
`required`, zero `skipped`, zero `oracleFailures`, and every executed ID
carrying an activation witness. Missing, duplicate, unexpected, filtered, or
unactivated members fail the assessment.

---

## 7. Mandatory decomposition-readiness checklist (sub-window standard §11)

All items are checked with `S3` evidence recorded in `EV-KI-W4-S01`–`S03`.

- [x] `SW-A01` Assignment `ASG-KI-W4-WA-01`, agent `KI-W4-WINDOW-AGENT`, delegation authority exact and current. Evidence: `EV-KI-W4-S01` §1.
- [x] `SW-A02` Standards and contract/decision/checklist/state revisions pinned and verified with the §0.4 delta audit. Evidence: `EV-KI-W4-S01` §2.
- [x] `SW-A03` Parent write/read/action/prohibition/successor/stop boundaries copied without expansion. Evidence: `EV-KI-W4-S01` §3.
- [x] `SW-A04` Repositories, dirty state, and owner-controlled changes inventoried. Evidence: `EV-KI-W4-S01` §4.
- [x] `SW-A05` Three subordinate artifacts exist with non-overlapping authorities. Evidence: `EV-KI-W4-S03` §1.
- [x] `SW-A06` Strict adjacency and no subagent delegation enforced. Evidence: `EV-KI-W4-S03` §2.
- [x] `SW-D01` Every parent requirement, invariant, decision, task, scenario, and case allocated to exact files and assertions. Evidence: `EV-KI-W4-S03` §3 (§6 mapping).
- [x] `SW-D02` No missing parent-level decision or contradictory authority. Evidence: `EV-KI-W4-S02` §1.
- [x] `SW-D03` Required changed-file set equals the planned initial file set (digest `fe48d14e…`). Evidence: `EV-KI-W4-S01` §5.
- [x] `SW-D04` One initial sub-window per file, one file per sub-window (10/10). Evidence: `EV-KI-W4-S03` §4.
- [x] `SW-D05` Every operation, starting digest, anchor, interface, preserved behavior, and forbidden edit exact. Evidence: `EV-KI-W4-S02` §2–§5.
- [x] `SW-D06` Dependency graph complete, sequential, acyclic, justified by named outputs. Evidence: `EV-KI-W4-S02` §6.
- [x] `SW-D07` Every cross-file interface frozen before dependent execution (`I-F1`–`I-F11`). Evidence: `EV-KI-W4-S02` §7.
- [x] `SW-D08` Every intermediate state has exact checks, expected failures, safety, resolver, prohibitions (§4.1). Evidence: `EV-KI-W4-S03` §5.
- [x] `SW-D09` Production, test, and fixture files have separate sub-windows (`S001`–`S007` production, `S008` fixture, `S009`/`S010` tests). Evidence: `EV-KI-W4-S03` §4.
- [x] `SW-D10` No rename, multi-output generator, formatter, installer, or command can violate the one-file invariant. Evidence: `EV-KI-W4-S03` §6.
- [x] `SW-E01` Every file sub-window contains every §7 field. Evidence: `EV-KI-W4-S03` §7.
- [x] `SW-E02` Every sub-window prescribes exact ordered edits, not alternatives or broad verbs. Evidence: `EV-KI-W4-S03` §7 (banned-verb lint zero).
- [x] `SW-E03` Every sub-window has exact preflight, checks, witnesses, assertions, forbidden outcomes. Evidence: `EV-KI-W4-S03` §7.
- [x] `SW-E04` Every sub-window mechanically proves its one-file changed set (V2 + I001 `V1`). Evidence: `EV-KI-W4-S03` §7.
- [x] `SW-E05` Exact evidence, handoff, stop, and successor-reservation rules per sub-window. Evidence: `EV-KI-W4-S03` §7.
- [x] `SW-E06` Subagents report only to the window agent and cannot update authority artifacts. Evidence: `EV-KI-W4-S03` §2.
- [x] `SW-E07` No sub-window requires successor work for file-local acceptance. Evidence: `EV-KI-W4-S03` §8.
- [x] `SW-E08` Deferred checks name the owning assessment (`W4-D*`→I001 `KI-W4-V3`; leaf-level registry runs→`KI-W4-V2`). Evidence: `EV-KI-W4-S03` §8.
- [x] `SW-V01` Cases allocated to exact test files, registrations, witnesses, assertions (§6). Evidence: `EV-KI-W4-S03` §9.
- [x] `SW-V02` Local and whole-window set-equality and digest checks prescribed (`KI-W4-V2`,`KI-W4-V3`,`KI-W4-V6`). Evidence: `EV-KI-W4-S03` §9.
- [x] `SW-V03` Every critical invariant has a negative control at the narrowest level (§6.2). Evidence: `EV-KI-W4-S03` §9.
- [x] `SW-V04` Substitute fidelity and invalidation rules exact (A4 fidelity table quoted in `S009`). Evidence: `EV-KI-W4-S03` §9.
- [x] `SW-V05` I001 authored with zero implementation-file write authority. Evidence: `EV-KI-W4-S03` §10.
- [x] `SW-V06` Gates exact, risk-proportionate, scheduled at the final assessment only. Evidence: `EV-KI-W4-S03` §10.
- [x] `SW-V07` Correction diagnosis, one-file assignment, invalidation, reassessment rules complete. Evidence: `EV-KI-W4-S03` §11.
- [x] `SW-V08` Window agent independently inspects every handoff and personally executes the assessment. Evidence: `EV-KI-W4-S03` §10.
- [x] `SW-V09` Approval cannot pass through zero-work/skip/filter/duplicate/unexpected/unactivated/summary-only evidence. Evidence: `EV-KI-W4-S03` §9.
- [x] `SW-V10` Parent handoff contents and `READY_FOR_PARENT_REVIEW` boundary exact. Evidence: `EV-KI-W4-S03` §12.
- [x] `SW-R01` All IDs unique and all references resolve. Evidence: `EV-KI-W4-S03` §13.
- [x] `SW-R02` No unresolved placeholder in any checked item or assignable sub-window. Evidence: `EV-KI-W4-S03` §13.
- [x] `SW-R03` Single-file write-set lint rejects zero/two/wildcard/directory/rename/incidental outputs. Evidence: `EV-KI-W4-S03` §13.
- [x] `SW-R04` Removing one required file or mapping makes readiness fail. Evidence: `EV-KI-W4-S03` §14.
- [x] `SW-R05` Removing/skipping/filtering/bypassing one case makes acceptance fail. Evidence: `EV-KI-W4-S03` §14.
- [x] `SW-R06` Weakening an oracle or diverging a substitute invalidates evidence. Evidence: `EV-KI-W4-S03` §14.
- [x] `SW-R07` Simulated second-file edit and direct parent communication rejected. Evidence: `EV-KI-W4-S03` §14.
- [x] `SW-R08` Simulated integration failure cannot be repaired without a corrective sub-window. Evidence: `EV-KI-W4-S03` §14.
- [x] `SW-R09` Parent decomposition review recorded before the first implementation assignment. Evidence: `EV-KI-W4-S03` §12 (S2 boundary).
- [x] `SW-R10` Document lint reports zero missing fields, mappings, cases, evidence references, or authority conflicts. Evidence: `EV-KI-W4-S03` §13.

Counts: checked 44 / unchecked 0.

---

## 8. Correction protocol and terminal boundary

- Corrections are append-only `KI-W4-C001`, `KI-W4-C002`, …; each owns
  exactly one file from the same ten-file set; a §12.2 corrective readiness
  certificate is appended to `S3` before assignment; a completed sub-window's
  history is never rewritten; dependent evidence is invalidated per §10 of
  the sub-window standard (only gates whose inputs changed re-run).
- Terminal boundary: after `I001` succeeds, `S2.decomposition_status` is
  `READY_FOR_PARENT_REVIEW` and the window agent produces the §12.5
  consolidated handoff. The window agent does not claim parent acceptance,
  does not begin `KI-W5`, and does not assign any further leaf without a
  recorded parent review.
- `S2`/`S3` seeding: `S2` starts at `state_version: 1`,
  `decomposition_status: AWAITING_PARENT_DECOMPOSITION_REVIEW`,
  `current_subwindow: NONE`, `next_subwindow: KI-W4-S001`; `S3` opens with
  `EV-KI-W4-S01`–`S03` (entry gate and delta audit, dependency and digest
  verification, authoring lint and the §12.1 readiness certificate).
