# KI-R5 Sub-Window Decomposition Checklist (`S1`)

**Artifact:** `KEYWORD_INTELLIGENCE_KI_R5_SUBWINDOW_CHECKLIST.md`
**Role:** Frozen sub-window decomposition checklist — sole subordinate authority for
the sub-window DAG, exact file assignments, task specifications, checks, and
handoff requirements for parent window `KI-R5`.
**Status:** `AWAITING_PARENT_DECOMPOSITION_REVIEW` — no leaf may be assigned until
the parent approves this decomposition and the window agent sets `S2` to `READY`.

Sibling artifacts: `KEYWORD_INTELLIGENCE_KI_R5_SUBWINDOW_STATE.md` (`S2`, live
status), `KEYWORD_INTELLIGENCE_KI_R5_SUBWINDOW_EVIDENCE.md` (`S3`, append-only
evidence). Live status exists only in `S2`; execution evidence exists only in
`S3`. This file is coordination-only; it never authorizes an implementation edit
by the window agent.

## 0. Inherited authority and revision pins

| Artifact | Path | Revision (SHA-256) |
|---|---|---|
| Parent authoring standard | `PROJECT_AGNOSTIC_DECISION_COMPLETE_CHECKLIST_AUTHORING_STANDARD.md` | `3b7a4fd25156e1adfbc92abb835c5f82a0d18c686b1c1150feb202f2d944d2ac` |
| Sub-window authoring standard | `PROJECT_AGNOSTIC_WINDOW_AGENT_SUBWINDOW_AUTHORING_STANDARD.md` | `1766f9107ce7d315877b75d4b0ea2b5521dff1c321e12f890b03787d66196ded` |
| Parent contract (`A1`) | `KEYWORD_INTELLIGENCE_PRODUCT_CONTRACT.md` | `8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c` |
| Parent decision ledger (`A3`) | `KEYWORD_INTELLIGENCE_DECISION_LEDGER.md` | `e8ed580dd08b77540158340c47fae84c5d56b18cc7aba3149ccc2ab568493f5d` |
| Parent checklist (`A4`) | `KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md` | `d65c72d2c1441226dfd575495c5b2d8e8bb321b4c3a9cd9fe6c83ae2320d5084` |
| Parent active state (`A5`) | `ACTIVE_EXECUTION_STATE.md` | state_version `112` at decomposition start (content digest recorded in `S3` `EV-KI-R5-S01`) |
| Parent assignment | `ASG-KI-R5-WA-01` | window agent `KI-R5-WINDOW-AGENT`; only `KI-R5` authorized; `accepted_through:KI-W5`; `next_window:KI-W6`; `stop_after:KI-R5`; `may_start_successor:false` |

All five file revisions were recomputed and matched `A5` state 112 before
authoring (`EV-KI-R5-S01`). A revision mismatch blocks new sub-window assignment
and requires a delta audit; it does not rewrite this decomposition.

### 0.1 Recorded interpretations pending parent decomposition review

These are mechanical decomposition choices that do not change any locked parent
decision. The parent may reject any of them at decomposition review; a rejection
is returned to the window agent for re-authoring, never to a leaf.

1. **Registry/certificate mechanics (corrected by C002).** There are **five**
   execution registries: four case registries — `R5_API_CASES`, `R5_DB_CASES`,
   `R5_FRONTEND_CASES`, `R5_BROWSER_CASES` — each an explicit executable array
   literal in its owning
   test file that executes its IDs as named subtests and emits exactly one TAP
   diagnostic `KI_R5_EXECUTION_CERTIFICATE=` followed by compact JSON
   `{registry,required,registered,executed,skipped,activationWitnesses,
   oracleFailures,digests:{required,registered,executed}}` with UTF-8-sorted
   arrays and per-member-LF SHA-256 digests (the pattern the parent locked for
   W4), plus the conformance registry `R5_CONFORMANCE_CASES` in the new
   enforcement test. The **four** non-conformance certificates feed the
   conformance registry: they are captured once from the single V1 (api), V2
   (frontend_api), V3 (database), and V4 (browser) gate runs. C002 removes the
   invalid local component-model certificate; it must not be replaced by an
   empty or vacuous certificate.
   During `KI-R5-I001` the window agent then runs the enforcement test
   **exactly once** with `KI_R5_EXECUTED_CERTIFICATES` supplying all four
   certificates; that single run executes `R5-CONF-01`–`06`, statically derives
   the five `registered` sets from the registry files, validates the four
   executed certificates, merges all 34 IDs (required=registered=executed with
   exact digests and zero skip/duplicate/unexpected/unactivated), and emits the
   final merged certificate. The enforcement test is never run with a partial
   certificate set and never run twice — at leaf time `KI-R5-S018` receives
   only local syntax/static checks (§5 S018). `NC-12` mutates in-memory copies
   of registry/certificate values through the same lint functions, per the
   parent's control table ("in separate copied evidence values").
2. **Inventory-test allocation.** `frontend/test/keyword-intelligence-inventory.test.ts`
   (the sixth existing test/harness file named by `KI-R5-T5`) receives additive
   static registry-lint assertions that the literal `R5_*_CASES` arrays in the
   other frontend test files equal their A4-mandated ID sets. These additions
   are auxiliary: they carry no manifest case ID, emit no certificate, and are
   inputs consumed by `R5-CONF-03`'s stable-registration check.
3. **No new runtime lib exports (corrected per parent findings 3/4).**
   `W5-I01` asserts `Object.keys(types)` equals the empty `TYPES_SURFACE`, and
   `W5-I03` asserts the exact literal `VIEW_MODEL_SURFACE`; neither `W5-I01`
   nor `W5-I03` is in the `DEC-KI-037` supersession set, so
   `frontend/lib/keyword-intelligence-types.ts` additions are type-only, and
   the selection projection used by the unsaved gate (`view-model.ts`) and the
   minimal PUT body (`client-api.ts` `saveKeywordSelection`) are module-local
   functions, not new exports. `client-api.ts` keeps its public signature;
   `saveKeywordSelection` receives full `SelectionItem[]` and projects
   internally before PUT. Because `SelectionItem.sourceKeywordId` is
   `string | null`, both projections use the exact frozen guard: for
   `sourceKind === "calculated"`, a `sourceKeywordId` that is not a non-empty
   string throws `new Error("calculated selection item requires a source id")`
   (fail-closed contract corruption; server-derived calculated rows always
   carry a string) before `SelectionMutationItem` is constructed; manual items
   never read `sourceKeywordId`.
4. **Client-only manual draft key.** Unsaved manual draft rows use
   `itemId: "draft_" + n` with a per-mounted-session monotonic counter
   (collisions increment), `sourceKeywordId: null`, `metricsSnapshot: null`.
   The key has no wire, durable, or identity authority (DEC-KI-034) and is never
   projected.
5. **`canFinalizeSelection` reason order.** `not_completed`, `empty`,
   `over_limit`, `unsaved`, `conflicts` — `unsaved` is evaluated after the
   cardinality gates and before conflict success (DEC-KI-035 "adds reason
   `unsaved` before conflict success").
6. **Cross-repo serializer witness (path corrected per parent finding 2).**
   `R5-WIRE-02` imports the actual W4 serializer into the frontend API test via
   `import { serializeKeywordResearch } from "../../email_scraper/src/api-serializer.js"`
   — from `frontend/test/`, `../..` resolves to the coordination root, then
   `email_scraper/src/api-serializer.js` — and feeds its output to the actual
   W5 parser, per DEC-KI-034's conformance-case requirement.

**Parent adjudication (2026-08-20, recorded in §11.3 and `EV-KI-R5-S04`):**
items 2, 4, and 5 accepted as written; item 1 rejected as written and revised
above (finding 7); items 3 and 6 accepted with the corrections above
(findings 3/4 and 2). Findings 1 and 5 are applied in §2/§5 S001 and §5
S011/S012 respectively.

## 1. Parent-window scope and exclusions

Objective (A4 `KI-R5`): make the accepted W4 backend and W5 dashboard
interoperable, capacity-correct, saved-selection faithful, retry-safe,
filter-consistent, and CSV-safe before integrated acceptance, through strictly
sequential single-file leaves.

Implementation boundary — the exact 18-path `delegable_implementation_file_set`
with per-member-LF `LC_ALL=C` sorted set digest
`efc82a884d09561ed27be3513ca6898f0ab311dbe56cf46e9c2c241492560077` (§2). The
window agent writes only `S1`/`S2`/`S3`; implementation is performed only by
one-file leaves; corrective leaves stay inside the same 18-path set.

Shared-symbol scopes (verbatim from A4): `api.js` selection
input/materialization/validation only; `repository.js` `createRun`
unique-race catch/reconciliation only; `export.js` textual-cell safety only;
`server.js` selection read limit only; `client-api.ts` three keyword mutation
methods only; `view-model.ts` selection projection/saved gate and exact filter
predicate only; `research-dashboard.tsx`/`selection-review.tsx` handoff state
and control locking only; accepted tests change only to supersede affected
W4/W5 assertions and add R5 registries.

Read-only scope (verbatim from A4): `A1`–`A8` outside parent updates;
`email_scraper/prisma/**`; `email_scraper/src/request-json.js`;
`email_scraper/src/keyword-intelligence/{selection,schemas,query-mapper,pipeline,dedup,cluster}.js`;
all worker/provider/S3/SQS/build/infrastructure code; frontend app route
handlers; frontend auth/proxy code; installed Next route-handler docs;
package/lock files; KI-W6 subordinate artifacts.

Prohibitions (verbatim from A4 `prohibited_actions`):
window-agent implementation-file edits; parallel leaves; direct parent-leaf
communication; package_or_lock_edits; schema_or_migration_edits;
worker_provider_S3_SQS_build_or_infrastructure_edits;
full_opted_in_database_suite; repeated_successful_stateful_or_build_gate_
without_invalidation; auth_bypass; provider_calls; AWS_operations;
production_database_writes; destructive_shared_cleanup; commits_or_pushes;
KI-W6_leaf_or_integration_work; KI-W7_work. Frozen-gate discipline
(DEC-KI-037): DB/build/browser/check/npm-test/secret gates each run once on
final frozen inputs; a later relevant edit invalidates and reruns only the
affected gate. The requester remains the only committer.

## 2. Starting working-tree inventory

Recorded without modification (`EV-KI-R5-S01`, revised `EV-KI-R5-S04`).
Nested repositories clean at the A4 `KI-R5-P2` baselines: backend
(email_scraper) HEAD `fac5bb0f0a4e9c04873c9d338794762d44e35f7f`; frontend HEAD
`c85f93b4bc66e1c130401227e46b488c6fe13c94`. Coordination root remains in the
owner-controlled relocation state: **45** `git status --porcelain` entries —
the pre-authoring 42 owner-controlled entries plus this window's three
subordinate artifacts — with `LC_ALL=C` sorted per-line-LF digest
`c660d09a800e8a5fd446bd65039f55241d5d7bb4e4c7ef656fe4fc7dcc88417c`
(recomputed after subordinate-artifact creation; content edits to S1/S2/S3 do
not change this path-set digest, and the window agent recomputes and records
the authoritative value in each leaf assignment at dispatch). No unrelated
owner-controlled change exists inside the 18 paths (all 16 existing paths are
clean at the recorded digests; two are `ABSENT`).

| # | Canonical path | Operation | Starting digest / state |
|---|---|---|---|
| F-001 | `email_scraper/src/keyword-intelligence/api.js` | MODIFY | `8c6e9845c0847e49f5eaa30f815e2fd4287db899a62c8aeb815adcdd730971fb` |
| F-002 | `email_scraper/src/server.js` | MODIFY | `f9947000fe3edcd2d582979ad155fb732e0abd40726baa241e75d9ca9eb2e428` |
| F-003 | `email_scraper/src/keyword-intelligence/export.js` | MODIFY | `03284102ee94ae11073e81d4dd331faa64dd4ee99ed1adadee1cd34366300d19` |
| F-004 | `email_scraper/src/keyword-intelligence/repository.js` | MODIFY | `fa249de27bc6d47c2480c342c5bf5760868328445e83dca9bb31be97fa2387c7` |
| F-005 | `email_scraper/test/keyword-intelligence-api.test.js` | MODIFY | `09e9235810a767bb4173a41a139b66f5cfe81c7a70ebddaf21773a78abc2aea0` |
| F-006 | `email_scraper/test/keyword-intelligence-handoff.integration.test.js` | MODIFY | `2a17aa562893c294a5f027ce074df17695cc4e6c156addcdc1af3522b6ada75c` |
| F-007 | `email_scraper/test/fixtures/keyword-intelligence/ki-r5-enforcement-manifest-v1.json` | CREATE | `ABSENT` |
| F-008 | `email_scraper/test/keyword-intelligence-r5-enforcement.test.js` | CREATE | `ABSENT` |
| F-009 | `frontend/lib/keyword-intelligence-types.ts` | MODIFY | `1619572d606af3b43a7bbf9945ef3f208e01f99c01ced29e2666a84c244b1f19` |
| F-010 | `frontend/lib/keyword-intelligence-validation.ts` | MODIFY | `8275def2a60c2cac443f1ca6e0a6f2d64cf31df9d467513be6cf0eaba34a6464` |
| F-011 | `frontend/lib/client-api.ts` | MODIFY | `b57d7b8609387243b8413a084303acf89c2fc4943ec170077321a01a3608c936` |
| F-012 | `frontend/lib/keyword-intelligence-view-model.ts` | MODIFY | `b91f0f5e7fd9f692e5f9086f1be0f511af1f0b6b755d117924497a52f89ce9d5` |
| F-013 | `frontend/components/keyword-intelligence/selection-review.tsx` | MODIFY | `5d127c195a2553cc077b4b1a3f592add08a184b9761cfce658fbb810b248f992` |
| F-014 | `frontend/components/keyword-intelligence/research-dashboard.tsx` | MODIFY | `94ba68eec79302352bdd6ac387bd8f27586ba0bb078d80b7b1390c56518ef023` |
| F-015 | `frontend/test/keyword-intelligence-api.test.ts` | MODIFY | `a2f40c62bdf6d34136c2d6a318c8aef24e426581182a2d5edf0ef6fc950cd5c5` |
| F-016 | `frontend/test/keyword-intelligence-components.test.ts` | MODIFY | `6e14ecc8eed297a6ca608ec365799b6cb2da2914d231944cb6be3047e24fe168` |
| F-017 | `frontend/test/keyword-intelligence-inventory.test.ts` | MODIFY | `67828152b71f9b05ec847d5fc0d3be238452d526aeffee8255e17b39a644f480` |
| F-018 | `frontend/test/browser/keyword-intelligence-dashboard.mjs` | MODIFY | `d28cc1b5411d412edeba139f715da69ab5c09a8d67c543be4cc69719ef5e68a7` |

Planned initial file set = required changed-file set = the 18 paths above;
each has exactly one initial owner (§3, §5). The set digest over the sorted
paths each followed by one LF is
`efc82a884d09561ed27be3513ca6898f0ab311dbe56cf46e9c2c241492560077`, equal to
the A4 `delegable_file_set_digest` (recomputed, `EV-KI-R5-S01`).

## 3. Initial single-file dependency DAG

Sequential order with named dependency edges; acyclic; one active sub-window at
a time. `S0xx` identifiers are never reused; corrective sub-windows append
`KI-R5-C<nnn>`.

```text
S001 api.js
S002 server.js                 <- S001 (selection route must serve the new PAY-KI-008 input contract)
S003 export.js
S004 repository.js
S005 test/keyword-intelligence-api.test.js        <- S001,S002,S003 (BAPI cases exercise all three)
S006 test/keyword-intelligence-handoff.integration.test.js <- S004 (FDB cases exercise createRun reconciliation)
S007 types.ts
S008 validation.ts             <- S007 (numeric literal type)
S009 client-api.ts             <- S007 (SelectionMutationItem types; module-local projection)
S010 view-model.ts             <- S007 (projection output types; saved gate)
S011 selection-review.tsx      <- S007 (draft item types)
S012 research-dashboard.tsx    <- S009,S010,S011 (mutation methods, saved gate, review props)
S013 frontend test/keyword-intelligence-api.test.ts      <- S008,S009,S010 (parser, init capture, predicate)
S014 frontend test/keyword-intelligence-components.test.ts <- S010,S011,S012
C002 frontend test/keyword-intelligence-components.test.ts <- S014 (remove rejected local lifecycle model; preserve W5 corrections)
S015 frontend test/browser/keyword-intelligence-dashboard.mjs <- S012,C002 (numeric fixtures, literal export oracle, actual lifecycle UI/request capture)
S016 frontend test/keyword-intelligence-inventory.test.ts <- S013,S015 (static registry lint)
S017 fixtures/ki-r5-enforcement-manifest-v1.json  <- (literal A4 case set; no source dependency)
S018 test/keyword-intelligence-r5-enforcement.test.js <- S005,S006,S013,S015,S016,S017
KI-R5-I001 integration assessment (window agent)  <- S001..S018
```

### 3.1 Interface freeze (before first dependent leaf)

Frozen cross-file interfaces (leaf agents may not choose alternatives):

- **WIRE (A4/DEC-KI-034):** persisted/worker/API/frontend research
  `contractVersion` is JSON number literal `1`. W5 `ResearchResult`/`ResearchView`
  types become `contractVersion: 1`; both strict parsers require exact finite
  integer `1`; string/other-number/null/missing/unknown-key is `ApiPayloadError`.
- **SelectionMutationItem (PAY-KI-008):**
  `CalculatedSelectionMutation = {sourceKind:"calculated", sourceKeywordId:string matching /^ksi_[a-f0-9]{12}$/, keyword:string}`;
  `ManualSelectionMutation = {sourceKind:"manual", keyword:string}`;
  request `{expectedRevision:int>=1, items:SelectionMutationItem[0..200]}` (plus
  service-injected `ownerId`/`researchId`); strict — unknown keys, calculated
  null/missing source ID, any manual source ID, item ID, metrics, lane, facets,
  seed or original text reject 400. Response/durable `SelectionItem` unchanged.
- **Materializer (W4 `api.js`):** calculated → find exact persisted result row
  by `sourceKeywordId`, item ID is the persisted row's canonical ID, retain
  original keyword/source seeds/metrics, normalize supplied editable keyword
  (1–160 code points, DEC-KI-014), reclassify lane/facets with persisted
  intent; manual → six-byte DEC-KI-002 ID via existing
  `selectionItemId("manual", keyword)`, first research seed, null
  source/metrics, lane/facets with `mainIntent:null`.
- **Duplicate fence (DEC-KI-036):** `saveSelection` calls accepted
  `validateSelectionDraft(draft)` after materialization and before
  `analyzeSelectionConflicts`/repository CAS; any invalid draft is 400 with
  zero write.
- **Body limit:** backend selection route `readJsonBody(request, 262144)`;
  Next selection route already `262144`; both 413 above; measured hard maximum
  of the strict union is 143,641 bytes for 200 calculated items.
- **createRun race recovery (DEC-KI-035):** public union stays
  `created|found|conflict|not_found`; on recognized unique-constraint error on
  the handoff key, one fresh read-only transaction reads the exact
  `(researchId,clientRequestId)` handoff, compares revision+fingerprint, reads
  its Run — equal+present `found`, unequal or missing Run `conflict`
  (`KEYWORD_RUN_HANDOFF_CONFLICT`), absent handoff rethrows the original error;
  no second write.
- **CSV safety (DEC-KI-036):** one ASCII apostrophe prefixed to textual cells
  starting with tab/CR or matching `/^\s*[=+\-@]/u`, once only, before existing
  escaping; numeric cells never neutralized.
- **Frontend saved gate/attempt lifecycle (DEC-KI-035; frozen per parent
  finding 5):** `canFinalizeSelection` reason adds `"unsaved"`; handoff state
  literals are exactly `"idle" | "handing-off" | "succeeded" |
  "definitive_failure" | "retry_required"` (the existing `"handing-off"`
  literal is retained; three members added). Parsed HTTP `<500` is definitive
  — success sets `"succeeded"` then navigates; `4xx` applies the existing safe
  UI mapping (409 → stale banner, else save error) and clears the attempt
  while `"definitive_failure"` leaves controls enabled for a fresh attempt.
  Network failure, unreadable response, or `>=500` is ambiguous — retain the
  exact `clientRequestId`+revision, enter `"retry_required"`, controls inert,
  retry byte-identical; another ambiguous outcome stays `"retry_required"`.
  The `SelectionReview` prop contract (`S011` owns the type/rendering, `S012`
  owns the state machine and wiring): `finalizeState` uses the expanded union;
  new prop `onRetryHandoff: () => void`; while `finalizeState` is
  `"handing-off"` or `"retry_required"` the manual add input/button, edit,
  remove, save, and finalize controls are disabled, a literal retry notice is
  rendered, and a retry button is rendered enabled only in
  `"retry_required"`; `"succeeded"` disables everything (navigation unmounts);
  `"definitive_failure"` renders with idle-equivalent enablement plus the
  mapped error — it adds **no** state-based control lock of its own, while the
  existing accepted-W5 409 `staleConflict` lock (which already disables
  draft/save/finalize controls when a 409 sets the stale banner) continues to
  apply unchanged.
- **Selection projection guard (frozen per parent finding 4):** the exact
  module-local mapping used by both S009 and S010 is
  `items.map((item) => { if (item.sourceKind === "calculated") { if (typeof
  item.sourceKeywordId !== "string" || item.sourceKeywordId.length === 0)
  throw new Error("calculated selection item requires a source id"); return
  { sourceKind: "calculated", sourceKeywordId: item.sourceKeywordId, keyword:
  item.keyword }; } return { sourceKind: "manual", keyword: item.keyword }; })`
  — the validated string is returned before `SelectionMutationItem` is
  constructed; manual items never read `sourceKeywordId`.
- **Registry/certificate shape:** §0.1 item 1 (five registries; four
  non-conformance certificates captured at V1/V2/V3/V4; the enforcement test
  runs exactly once during `KI-R5-I001` with all four and emits the merged
  34-ID certificate; S018 leaf checks are syntax/static only).

### 3.2 Intermediate-state contracts

Unexpected failures stop the sequence for diagnosis; only the listed temporary
failures are permitted.

| After | Passing now | Expected temporary failure | Resolver | Prohibited while state exists |
|---|---|---|---|---|
| S001 | `node --check api.js`; anchor inspection; unrelated create/get/export paths unchanged | Old full-snapshot PUT assertions in `test/keyword-intelligence-api.test.js` (W4-A04/W4-S04 members) fail until superseded | S005 | Running `npm test` or the full api test file |
| S002 | syntax + anchors; all existing small-body cases unaffected | none new | — | — |
| S003 | parity/export golden tests must still pass (accepted fixtures contain no dangerous textual cells) | none | — | Editing any fixture outside the 18 paths; a parity failure here is a blocker, not a todo |
| S004 | syntax + anchors; old W4-D04 `>=1` oracle remains semantically true | none (DB cases are not run mid-sequence) | S006/V3 | Any DB run before V3 |
| S005 | full `node --test --test-isolation=none test/keyword-intelligence-api.test.js` passes (superseded six + new BAPI cases green) | none | — | — |
| S006 | syntax + structure; file skips without `ALLOW_DATABASE_TESTS` (registration-only) | DB execution deferred to V3 | V3 | Any DB run before V3 |
| S007–S012 | per-leaf anchor/strip-types checks; lib-level runtime surfaces unchanged | `npm run check` (frontend) may fail on superseded fixtures until S013/S015/S016; deferred to V4 | S013/S015/S016, V4 | Running `npm run check` or frontend suites before their owning leaf |
| C002/S013–S016 | C002 focused component regression passes without an R5 certificate; S013 focused registry passes; S015 structural checks only; S016 follows S013/S015 | browser execution deferred to V4 | V4 | Browser/Next build before V4 |
| S017 | JSON parse + digest recompute vs literals | none | — | — |
| S018 | `node --check`; manifest-fixture parse; static registry enumeration (five `registered` sets == required, exact digests); NC-12 lint falsifications on synthetic in-memory copies — **no certificate input, no CONF execution, no test run requiring certificates** | the six CONF cases and the 34-ID merge are deferred to the single `KI-R5-I001` enforcement run with all four captured certificates | I001 | Running the enforcement test at leaf time; running it with a partial certificate set; running it twice |

## 4. Allocation maps

### 4.1 Requirements/decisions/tasks → files

| Parent task | Locked decisions | Production files | Test/registry files |
|---|---|---|---|
| `KI-R5-T1` canonical bounded selection mutation | DEC-KI-002/014/015/034/036; PAY-KI-008 | S001 api.js; S002 server.js | S005 (BAPI) |
| `KI-R5-T2` equal-key handoff race | DEC-KI-017/035 | S004 repository.js | S006 (FDB) |
| `KI-R5-T3` filter/export parity + CSV safety | DEC-KI-033/036 | S003 export.js | S005 (BAPI), S013 (FAPI cross-side) |
| `KI-R5-T4` frontend wire/saved gate/retry | DEC-KI-034/035/036 | S007–S012 | S013 (FAPI), S014 W5 regression preservation, S015 browser execution registry alone (BR + A4 FCOMP lifecycle evidence; NC-05/06 only) |
| `KI-R5-T5` enforcement manifest | DEC-KI-037 | — | S017 manifest, S018 CONF, execution registries in S005/S006/S013/S015, and S016 registry lint |

Requirement IDs consumed verbatim from the A4 task blocks (REQ-KI-005–009,
014–018, 021; INV-KI-009/010/013/015). No parent requirement, invariant,
decision, task, scenario, or coverage case in the A4 `KI-R5` window remains
unallocated (`SW-D01`).

### 4.2 Coverage cases → registries (34 manifest IDs)

| Registry (file) | Manifest group | IDs |
|---|---|---|
| `R5_API_CASES` (S005 `email_scraper/test/keyword-intelligence-api.test.js`) | `selection` (8) + export backend members | `R5-SEL-01`–`08`, `R5-EXP-05`, `R5-EXP-06` |
| `R5_DB_CASES` (S006 `email_scraper/test/keyword-intelligence-handoff.integration.test.js`) | `finalization` DB members | `R5-FIN-07`, `R5-FIN-08` |
| `R5_FRONTEND_CASES` (S013 `frontend/test/keyword-intelligence-api.test.ts`) | `wire` (except 04) + export cross-side | `R5-WIRE-01`,`-02`,`-03`,`-05`,`-06`, `R5-EXP-01`–`04` |
| `R5_BROWSER_CASES` (S015 `frontend/test/browser/keyword-intelligence-dashboard.mjs`) | browser execution registry alone for wire browser + A4 `FCOMP` finalization lifecycle evidence; NC-05/06 execute only here | `R5-WIRE-04`, `R5-FIN-01`–`06` |
| `R5_CONFORMANCE_CASES` (S018 `email_scraper/test/keyword-intelligence-r5-enforcement.test.js`) | `conformance` | `R5-CONF-01`–`06` |

Five execution registries total: the four case registries above emit
`KI_R5_EXECUTION_CERTIFICATE` lines captured at V1/V2/V3/V4; the
conformance registry executes only inside the single `KI-R5-I001` enforcement
run that merges all 34 IDs.

Per-group per-member-LF digests and the 34-ID global digest
`507186e7489a3f9eec18eb5de78692dbc55a8d1d2d106544aa4295a98ac9be60` are the A4
literals; S017 embeds them; S018 and V6 recompute them.

Controls `R5-NC-01`–`NC-12` are executed inside their owning registries per the
A4 control table (NC-01 FAPI; NC-02 FAPI/BR; NC-03/04/10 BAPI; NC-05/06
browser registry only carrying A4 FCOMP lifecycle evidence; NC-07 FDB;
NC-08/09 FAPI; NC-11 BR/CONF; NC-12 CONF). Controls are
falsification executions, not manifest members; each first runs the named
production case and unchanged oracle to PASS, applies only the listed
test-boundary mutation, requires that same oracle to throw `AssertionError`
with the listed message, then discards the mutation and reruns fresh production
to PASS.

### 4.3 Accepted-test supersession (DEC-KI-037, exhaustive)

- W4 mutable oracles (six): `W4-A04`, `W4-A06`, `W4-A07`, `W4-S04`, `W4-S06`
  (S005), `W4-D04` (S006). Stable IDs/registrations remain; each change cites
  its R5 case(s).
- W5 mutable oracles (twelve): `W5-A05`, `W5-A06`, `W5-A09`, `W5-A10` (S013),
  `W5-C05`, `W5-C08`, `W5-C12` (S014), `W5-B02`–`B05`, `W5-R03` (S015).
- Browser rerun set under V4 (15): `W5-B01`–`B08`, `W5-R01`–`R07`; no browser
  oracle outside B02–B05/R03 may change.
- Every other accepted W4/W5 case ID, registration, activation witness, and
  oracle is byte/semantic read-only. `R5-CONF-03` enforces this; A7
  (`KEYWORD_INTELLIGENCE_SPECIFICATION_CHANGELOG.md`) already records the
  invalidation; the unexecuted KI-W6 decomposition is invalidated wholesale by
  the predecessor/revision change and must be re-authored after R5.

## 5. Initial sub-window blocks

Every block below contains the complete Section 7 field set of the sub-window
standard. All leaves: `parent_window_id: KI-R5`, `parent_assignment_id:
ASG-KI-R5-WA-01`, `successor_reserved_for: WINDOW-AGENT`, `may_start_successor:
false`, assigned agent identity issued at dispatch, `assigned_agent_policy`
per-leaf UNASSIGNED until the window agent dispatches after parent approval.
Common prohibitions for every leaf: no second-file edit; no command whose
workspace write set exceeds the writable file; no provider/AWS/production DB
call; no schema/migration/package/config/worker/route-handler/auth edit; no
commit/push; no parent communication; no successor start; no KI-W6/W7 work;
preserve unrelated dirty state; stop at `AWAITING_WINDOW_REVIEW`. Common
preflight/handoff mechanics: compare repository changed-file sets before/after,
starting/ending digest of the writable file, and digests of protected dirty
root paths; the attributable delta must be exactly the writable file.

---

### KI-R5-S001 — W4 selection mutation contract (api.js)

```yaml
subwindow_id: KI-R5-S001
type: FILE
assignment_id: ASG-KI-R5-S001
assigned_agent: UNASSIGNED
predecessors: []
writable_file: email_scraper/src/keyword-intelligence/api.js
file_operation: MODIFY
starting_file_digest: 8c6e9845c0847e49f5eaa30f815e2fd4287db899a62c8aeb815adcdd730971fb
starting_repository_change_set_digest: c660d09a800e8a5fd446bd65039f55241d5d7bb4e4c7ef656fe4fc7dcc88417c
read_only_scope: [email_scraper/src/keyword-intelligence/selection.js, email_scraper/src/keyword-intelligence/cluster.js, email_scraper/src/keyword-intelligence/schemas.js, email_scraper/src/api-serializer.js, email_scraper/src/keyword-intelligence/query-mapper.js, KEYWORD_INTELLIGENCE_DECISION_LEDGER.md::DEC-KI-002/014/034/036, KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md::KI-R5-T1]
authorized_actions: [apply the ordered transformations to the writable file, node --check, deterministic anchor inspection, focused non-database diagnostics]
prohibited_actions: [common prohibitions, editing any schema/repository/serializer file, removing any existing export]
```

Dispatch note (finding 1): the recorded change-set digest is the current
45-entry value; because S1/S2/S3 content revisions do not alter the root
path-set digest, it remains valid until a leaf edits an implementation file —
the window agent recomputes and records the authoritative digest in the
assignment at dispatch and the leaf preflight compares against that value.

**Mechanical trace:** `KI-R5-T1` items 1–15; `REQ-KI-005`–`009`, `016`;
`INV-KI-010`, `013`; `DEC-KI-002`, `014`, `015`, `034`, `036`; `PAY-KI-008`;
cases `R5-SEL-01`–`08` (behavioral proof in S005).

**Exact file transformation (ordered):**
1. Replace the items element of `saveSelectionInputSchema` (anchor: line 59,
   `z.strictObject({ ownerId: ... })` block) with a strict discriminated union
   on `sourceKind`:
   `z.discriminatedUnion("sourceKind", [z.strictObject({sourceKind: z.literal("calculated"), sourceKeywordId: z.string().regex(/^ksi_[a-f0-9]{12}$/u), keyword: z.string()}), z.strictObject({sourceKind: z.literal("manual"), keyword: z.string()})])`.
   Change `expectedRevision` from `z.number().int().nonnegative()` (its
   current form at line 61) to `z.number().int().min(1)` (finding 3). The
   request keeps exactly `{ownerId, researchId, expectedRevision, items}` with
   `items` array `0..200`; `strictObject` rejects unknown keys.
2. Rewrite `canonicalizeSelectionItem(research, item)` (anchor: line 205) to
   the DEC-KI-034 materializer. Calculated: `findResultRow` by
   `item.sourceKeywordId` (400 `inputInvalid` when absent); `keyword =
   normalizeKeyword(item.keyword)` (1–160 code points); `itemId = row.itemId`;
   retain `originalKeyword`/`sourceSeeds`/`metricsSnapshot` from the row;
   `classifyKeywordForSelection(keyword, {mainIntent: row.mainIntent,
   stripTokens})`. Manual: `itemId = selectionItemId("manual", keyword)`; 400
   when `research.seeds[0]` is absent/empty; `sourceSeeds=[firstSeed]`;
   `sourceKeywordId: null`, `metricsSnapshot: null`; `originalKeyword =
   keyword`; classify with `{mainIntent: null, stripTokens}`. No client-supplied
   itemId/metrics/lane/facets/originalKeyword is read or compared on input.
3. In `saveSelection` (anchor: line 444): keep `parseStrict` and the
   `MAX_SELECTION_ITEMS` guard; after `const draft = parsed.items.map(...)`
   insert `const validity = validateSelectionDraft(draft); if (!validity.ok)
   throw inputInvalid({ issues: validity.issues });` (add
   `validateSelectionDraft` to the existing `./selection.js` import) — strictly
   before `analyzeSelectionConflicts` and the repository CAS.
4. Preserve byte-for-byte behavior of `createResearch`, `getResearch`,
   `createRun`, `exportCsv`, error codes, `serializeKeywordResearch` output,
   and the repository call sequence (one owner read + one CAS).

**Exact checks (LOCAL_NOW):** `node --check src/keyword-intelligence/api.js`
(exit 0); anchor inspection asserting (a) `discriminatedUnion("sourceKind"`
present in `saveSelectionInputSchema`; (b) `validateSelectionDraft(` appears
exactly once and textually before `analyzeSelectionConflicts(` inside
`saveSelection`; (c) no `item.metricsSnapshot`/`item.itemId` comparison remains
inside `canonicalizeSelectionItem`. **DEFERRED_TO_INTEGRATION:** S005 BAPI
cases; V1; V5. Expected intermediate state: §3.2 row S001.

```markdown
- [ ] P1 Revisions, assignment identity, writable file, baseline digest, and predecessor evidence match.
- [ ] P2 Starting repository status and protected dirty changes match the recorded baseline.
- [ ] T1 Apply every ordered transformation and no other edit to the writable file.
- [ ] V1 Run every LOCAL_NOW check and record its activation witnesses and exact assertions.
- [ ] V2 Prove the attributable workspace changed-file set is exactly the writable file.
- [ ] V3 Prove required local coverage IDs equal registered and executed local IDs with zero skips.
- [ ] H1 Return the exact diff, ending digest, commands, outcomes, and residual integration obligations.
- [ ] H2 Confirm no prohibited action, second-file edit, successor work, external mutation, or parent communication occurred.
- [ ] H3 Stop at AWAITING_WINDOW_REVIEW.
```

---

### KI-R5-S002 — backend selection body limit (server.js)

```yaml
subwindow_id: KI-R5-S002
type: FILE
assignment_id: ASG-KI-R5-S002
assigned_agent: UNASSIGNED
predecessors: [KI-R5-S001]
writable_file: email_scraper/src/server.js
file_operation: MODIFY
starting_file_digest: f9947000fe3edcd2d582979ad155fb732e0abd40726baa241e75d9ca9eb2e428
starting_repository_change_set_digest: recorded at dispatch (post-S001 tree)
read_only_scope: [email_scraper/src/request-json.js, KEYWORD_INTELLIGENCE_DECISION_LEDGER.md::DEC-KI-034]
authorized_actions: [single-argument edit, node --check, anchor inspection]
prohibited_actions: [common prohibitions, any other server route/branch change]
```

**Mechanical trace:** `KI-R5-T1` item 1 ("raise only the backend selection
reader to 262144 bytes"); DEC-KI-034 locked size; cases `R5-SEL-06`, `R5-SEL-08`.

**Exact file transformation:** in the selection PUT route (anchor: line 1786,
`const payload = await readJsonBody(request);` inside the
`requestedKeywordResearchId(requestUrl.pathname, "selection")` block) change to
`const payload = await readJsonBody(request, 262144);`. No other edit;
`readJsonBody` already accepts a limit parameter and returns the existing 413
error above it.

**Exact checks (LOCAL_NOW):** `node --check src/server.js`; anchor inspection
asserting the selection route passes literal `262144` and no other
`readJsonBody` call site changed (all other call sites keep default 32 KiB).
**DEFERRED_TO_INTEGRATION:** `R5-SEL-06`/`R5-SEL-08` (S005); V1; V5.
Completion checklist: as S001.

---

### KI-R5-S003 — spreadsheet-safe textual CSV cells (export.js)

```yaml
subwindow_id: KI-R5-S003
type: FILE
assignment_id: ASG-KI-R5-S003
assigned_agent: UNASSIGNED
predecessors: []
writable_file: email_scraper/src/keyword-intelligence/export.js
file_operation: MODIFY
starting_file_digest: 03284102ee94ae11073e81d4dd331faa64dd4ee99ed1adadee1cd34366300d19
starting_repository_change_set_digest: recorded at dispatch
read_only_scope: [KEYWORD_INTELLIGENCE_DECISION_LEDGER.md::DEC-KI-036, email_scraper/test/keyword-intelligence-parity.test.js, email_scraper/test/fixtures/keyword-intelligence/parity-output-v1.json]
authorized_actions: [ordered edit, node --check, focused parity test run]
prohibited_actions: [common prohibitions, changing column order/headers/numeric formatting]
```

**Mechanical trace:** `KI-R5-T3` items 1–15; `REQ-KI-014`, `018`;
`INV-KI-009`; DEC-KI-036 locked CSV safety; cases `R5-EXP-05`, `R5-EXP-06`;
finding `KI-PR-F09`.

**Exact file transformation (ordered):**
1. Add module-local
   `function neutralizeTextCell(value) { if (typeof value !== "string") return value; if (/^[\t\r]/u.test(value) || /^\s*[=+\-@]/u.test(value)) return value.startsWith("'") ? value : "'" + value; return value; }`
   — exactly one apostrophe, applied once, before existing quote/escape.
2. In `serializeKeywordsCsv` (anchor: line 190), wrap exactly the textual cells
   of each data row before `csvRow`: `d.keyword`, `d.seed`,
   `d.source_seeds.join("|")`, `d.competition_level`, `d.main_intent`,
   `d.cluster`, `d.cluster_id`, `d.lane`, `pyDumps(d.facets, true)`,
   `d.variant_group_id`, `d.variant_canonical`, `(d.flags||[]).join(";")`,
   `d.merged_into`, `pyDumps(d.monthly_history, true)`,
   `d.available_markets.join("|")`. Numeric cells (`intStr`/`pyFloatStr`/
   `pyBoolStr` outputs, including negative `trend_slope`) are never wrapped.
   Header row, column order, LF joining, and all other formatting remain
   byte-identical for safe values.

**Exact checks (LOCAL_NOW):** `node --check src/keyword-intelligence/export.js`;
`node --test --test-isolation=none test/keyword-intelligence-parity.test.js`
must PASS (accepted parity fixtures contain no dangerous textual cells; any
failure is an unexpected failure → stop for diagnosis, not a fixture edit);
anchor inspection: `neutralizeTextCell` defined once and applied to the named
cells; `csvEscape` unchanged. **DEFERRED_TO_INTEGRATION:** `R5-EXP-05/06`
(S005); V1; V5. Completion checklist: as S001.

---

### KI-R5-S004 — equal-key handoff race reconciliation (repository.js)

```yaml
subwindow_id: KI-R5-S004
type: FILE
assignment_id: ASG-KI-R5-S004
assigned_agent: UNASSIGNED
predecessors: []
writable_file: email_scraper/src/keyword-intelligence/repository.js
file_operation: MODIFY
starting_file_digest: fa249de27bc6d47c2480c342c5bf5760868328445e83dca9bb31be97fa2387c7
starting_repository_change_set_digest: recorded at dispatch
read_only_scope: [KEYWORD_INTELLIGENCE_DECISION_LEDGER.md::DEC-KI-035, email_scraper/prisma/schema.prisma, email_scraper/test/keyword-intelligence-handoff.integration.test.js]
authorized_actions: [ordered edit, node --check, anchor inspection]
prohibited_actions: [common prohibitions, schema/migration edit, retry loop/sleep, distributed lock, changing the winning transaction]
```

**Mechanical trace:** `KI-R5-T2` items 1–15; `REQ-KI-015`, `016`;
`INV-KI-010`, `015`; DEC-KI-017/035; finding `KI-PR-F06`; cases
`R5-FIN-07`, `R5-FIN-08`.

**Exact file transformation:** in `PrismaKeywordResearchRepository.createRun`
(anchors: transaction body lines 1233–1269, catch at 1270–1275) keep the first
transaction and its `RunHandoffAbort` mapping unchanged. In the `catch`, before
rethrowing: if the error is a recognized Prisma unique-constraint violation
(code `P2002`) on the keyword-research handoff, run
`return await this._transaction(async (tx) => { const handoff = await
tx.keywordResearchHandoff.findUnique({ where: { researchId_clientRequestId: {
researchId, clientRequestId: input.clientRequestId } } }); if (!handoff) throw
originalError; if (handoff.selectionFingerprint !== input.selectionFingerprint
|| handoff.selectionRevision !== input.expectedSelectionRevision) return
{ outcome: "conflict", code: "KEYWORD_RUN_HANDOFF_CONFLICT" }; const run = await
tx.run.findUnique({ where: { id: handoff.runId } }); return run ? { outcome:
"found", run } : { outcome: "conflict", code: "KEYWORD_RUN_HANDOFF_CONFLICT" };
})`. The reconciliation is read-only (no Run/RunQuery/handoff write), observes
only committed evidence after the winner's rollback, compares durable
identity/revision/fingerprint only (never a caller-proposed Run ID), and
rethrows the original error when the handoff is absent. Every other exception
still escapes; public signature and all outcome unions unchanged.

**Exact checks (LOCAL_NOW):** `node --check src/keyword-intelligence/repository.js`;
anchor inspection: exactly one `P2002` branch; reconciliation transaction
performs exactly `findUnique` ×2 and zero creates/updates; winner path
untouched. **DEFERRED_TO_INTEGRATION:** `R5-FIN-07/08` + `NC-07` (V3);
`W4-D04` supersession (S006); V5. DB runs prohibited before V3.
Completion checklist: as S001.

---

### KI-R5-S005 — backend API/export registry and W4 supersession (api.test.js)

```yaml
subwindow_id: KI-R5-S005
type: FILE
assignment_id: ASG-KI-R5-S005
assigned_agent: UNASSIGNED
predecessors: [KI-R5-S001, KI-R5-S002, KI-R5-S003]
writable_file: email_scraper/test/keyword-intelligence-api.test.js
file_operation: MODIFY
starting_file_digest: 09e9235810a767bb4173a41a139b66f5cfe81c7a70ebddaf21773a78abc2aea0
starting_repository_change_set_digest: recorded at dispatch
read_only_scope: [email_scraper/src/keyword-intelligence/api.js, email_scraper/src/keyword-intelligence/export.js, email_scraper/src/server.js, KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md::R5-SEL/R5-EXP rows, KEYWORD_INTELLIGENCE_DECISION_LEDGER.md::DEC-KI-037]
authorized_actions: [additive registry/case edits, supersede exactly the six listed W4 oracles, run the focused file once, emit certificate]
prohibited_actions: [common prohibitions, weakening/renaming/removing any unlisted W4 assertion, editing production files]
```

**Mechanical trace:** `KI-R5-T1`/`T3`/`T5` test obligations; `R5-SEL-01`–`08`,
`R5-EXP-05/06`; controls `R5-NC-03`, `R5-NC-04`, `R5-NC-10`; supersession set
`{W4-A04, W4-A06, W4-A07, W4-S04, W4-S06}`; DEC-KI-036/037.

**Exact file transformation (ordered):**
1. Add literal `const R5_API_CASES = ["R5-SEL-01","R5-SEL-02","R5-SEL-03","R5-SEL-04","R5-SEL-05","R5-SEL-06","R5-SEL-07","R5-SEL-08","R5-EXP-05","R5-EXP-06"];`
   and an executable case map implementing each A4 row exactly:
   SEL-01 calculated materialization (persisted source ID → exact full
   canonical item; one read + one CAS); SEL-02 manual derivation (exact
   DEC-KI-002 ID, null metrics/source; one CAS); SEL-03 unknown/legacy union
   members (itemId/metrics/lane/facets/owner or bad discriminator → 400, zero
   repository save); SEL-04 duplicate calculated source (400 duplicate, zero
   CAS, not a conflict); SEL-05 two normalization-equal manual texts (400
   duplicate derived ID, zero CAS); SEL-06 200 max-code-point calculated items
   through the real W4 server route (143641-byte body → 200, exactly 200
   canonical items, one CAS, no 413); SEL-07 201 minimal inputs (400, zero
   owner read/save); SEL-08 262145-byte body to the real route (413 before
   API/owner read); EXP-05 all dangerous textual prefixes + negative trend
   (parse exported CSV cells: each dangerous text has exactly one leading
   apostrophe; negative numeric cell unchanged); EXP-06 zero-match export +
   forbidden internal fields (exact header+LF; no config/owner/raw/credential/
   fingerprint fields). Each case pushes its ID only after its activation
   witness and oracle.
2. Implement controls NC-03/04/10 exactly per the A4 control table (forbidden
   `itemId` added to a captured minimal item and synthetic 413 substitution →
   `R5_SELECTION_WIRE_OR_LIMIT_DIVERGED`; synthetic save event appended after
   duplicate rejection → `R5_DUPLICATE_WRITE_FORBIDDEN`; removed neutralizing
   apostrophe from a copied dangerous cell → `R5_CSV_TEXT_UNSAFE`), each with
   the pass–mutate–fail–restore pattern.
3. Supersede exactly `W4-A04`, `W4-A06`, `W4-A07`, `W4-S04`, `W4-S06` to the
   corrected contract (minimal-union PUT inputs; dangerous-cell CSV
   expectations), keeping their IDs/registrations and citing the corresponding
   R5 case(s) in a comment; every other W4 case byte-identical; the existing
   `KI_W4_EXECUTION_CERTIFICATE` emission remains structurally unchanged.
4. Emit exactly one `KI_R5_EXECUTION_CERTIFICATE=` TAP diagnostic for registry
   `"api"` with sorted arrays and per-member-LF digests (§0.1 item 1).

**Exact checks (LOCAL_NOW):** run exactly
`node --test --test-isolation=none test/keyword-intelligence-api.test.js` from
`email_scraper/` — every test passes (superseded six + new cases + unrelated
W4), zero skip/todo; certificate line present and well-formed.
**DEFERRED_TO_INTEGRATION:** V1 (frozen rerun), V5. Completion checklist: as
S001.

---

### KI-R5-S006 — handoff DB registry and D04 supersession (integration test)

```yaml
subwindow_id: KI-R5-S006
type: FILE
assignment_id: ASG-KI-R5-S006
assigned_agent: UNASSIGNED
predecessors: [KI-R5-S004]
writable_file: email_scraper/test/keyword-intelligence-handoff.integration.test.js
file_operation: MODIFY
starting_file_digest: 2a17aa562893c294a5f027ce074df17695cc4e6c156addcdc1af3522b6ada75c
starting_repository_change_set_digest: recorded at dispatch
read_only_scope: [email_scraper/src/keyword-intelligence/repository.js, email_scraper/test/helpers/isolated-postgres.js, KEYWORD_INTELLIGENCE_DECISION_LEDGER.md::DEC-KI-035/037]
authorized_actions: [additive registry/case edits, supersede W4-D04 oracle, node --check, no-database registration run]
prohibited_actions: [common prohibitions, any database execution (V3 owns it), editing W4-D01..D03/D05/D06 oracles]
```

**Mechanical trace:** `KI-R5-T2` item 13; cases `R5-FIN-07`, `R5-FIN-08`;
control `R5-NC-07`; supersession `W4-D04`; DEC-KI-035; `SCN-KI-037`.

**Exact file transformation (ordered):**
1. Add literal `const R5_DB_CASES = ["R5-FIN-07", "R5-FIN-08"];` and the two
   cases as sequential named subtests inside the existing single-harness
   disposable-schema lifecycle (one `withIsolatedDb`-equivalent outer setup;
   case-local research/task cleanup inside the schema; one final drop +
   exact-name absence assertion): FIN-07 two concurrent equal requests
   released against the real Prisma unique — `Promise.allSettled` yields two
   fulfilled (one `created`, one `found`), exactly one handoff/Run/query set;
   FIN-08 same key unequal fingerprint/revision — conflict; one handoff/Run;
   later equal replay `found`.
2. Supersede the `W4-D04` oracle (anchor: line 439,
   `assert.ok(fulfilled.length >= 1, ...)`) to the exact two-fulfilled/one-Run
   proof, citing `R5-FIN-07`; keep the ID/registration and every other W4-D
   case byte-identical.
3. Implement `R5-NC-07`: a non-mutating Prisma client `Proxy` used only for the
   losing call that converts the fresh exact-handoff read after the recognized
   unique error to `null`; the unchanged two-fulfilled oracle must throw
   `R5_EQUAL_RACE_NOT_RECONCILED`; the unwrapped client passes in a fresh
   fixture in the same schema. No production source edit.
4. Emit the registry `"database"` certificate line (§0.1 item 1). DB execution
   itself is DEFERRED to V3.

**Exact checks (LOCAL_NOW):** `node --check`; a no-database invocation of the
file (skips as designed, zero failures) proving registration/structure;
anchor inspection: `R5_DB_CASES` literal matches the two IDs; old `>=1`
assertion absent. **DEFERRED_TO_INTEGRATION:** V3 (single frozen DB gate);
V5. Completion checklist: as S001.

---

### KI-R5-S007 — numeric wire types (types.ts)

```yaml
subwindow_id: KI-R5-S007
type: FILE
assignment_id: ASG-KI-R5-S007
assigned_agent: UNASSIGNED
predecessors: []
writable_file: frontend/lib/keyword-intelligence-types.ts
file_operation: MODIFY
starting_file_digest: 1619572d606af3b43a7bbf9945ef3f208e01f99c01ced29e2666a84c244b1f19
starting_repository_change_set_digest: recorded at dispatch
read_only_scope: [KEYWORD_INTELLIGENCE_DECISION_LEDGER.md::DEC-KI-034, frontend/test/keyword-intelligence-inventory.test.ts (TYPES_SURFACE context)]
authorized_actions: [type-only edits, strip-types import smoke, anchor inspection]
prohibited_actions: [common prohibitions, any runtime export (W5-I01 oracle is byte-read-only)]
```

**Mechanical trace:** `KI-R5-T4` item 5; DEC-KI-034 locked response version +
selection input; finding `KI-PR-F01`; cases `R5-WIRE-01`–`03`.

**Exact file transformation (ordered):** (1) `ResearchResult.contractVersion:
string` → `contractVersion: 1` (anchor: line 175). (2)
`ResearchView.contractVersion: string` → `contractVersion: 1` (anchor: line
210). (3) Append type-only exports
`export type CalculatedSelectionMutation = { sourceKind: "calculated"; sourceKeywordId: string; keyword: string };`
`export type ManualSelectionMutation = { sourceKind: "manual"; keyword: string };`
`export type SelectionMutationItem = CalculatedSelectionMutation |
ManualSelectionMutation;`. No runtime export is added or removed.

**Exact checks (LOCAL_NOW):** anchor inspection (two `contractVersion: 1`
literals; three type exports; zero new `export const/function`); strip-types
load smoke `node --experimental-strip-types --input-type=module -e "await
import('./lib/keyword-intelligence-types.ts')"` exits 0 from `frontend/`.
**DEFERRED_TO_INTEGRATION:** S008/S009 consumers; V2/V4. Completion checklist:
as S001.

---

### KI-R5-S008 — strict numeric version parsing (validation.ts)

```yaml
subwindow_id: KI-R5-S008
type: FILE
assignment_id: ASG-KI-R5-S008
assigned_agent: UNASSIGNED
predecessors: [KI-R5-S007]
writable_file: frontend/lib/keyword-intelligence-validation.ts
file_operation: MODIFY
starting_file_digest: 8275def2a60c2cac443f1ca6e0a6f2d64cf31df9d467513be6cf0eaba34a6464
starting_repository_change_set_digest: recorded at dispatch
read_only_scope: [frontend/lib/keyword-intelligence-types.ts, KEYWORD_INTELLIGENCE_DECISION_LEDGER.md::DEC-KI-034]
authorized_actions: [ordered edits, strip-types smoke, anchor inspection]
prohibited_actions: [common prohibitions, new runtime exports (W5-I02 oracle byte-read-only), dual-version parser]
```

**Mechanical trace:** `KI-R5-T4` item 6; DEC-KI-034 locked response version;
finding `KI-PR-F01`; cases `R5-WIRE-01`–`03`.

**Exact file transformation (ordered):** in `result()` (anchor: line 518) and
in `parseResearchView()` (anchor: line 731) replace
`contractVersion: nonEmptyText(source.contractVersion, \`${path}.contractVersion\`)`
with `contractVersion: source.contractVersion === 1 ? 1 : (() => { throw new
ApiPayloadError(\`${path}.contractVersion\`); })()` — equivalently an exact
`=== 1` guard that throws `ApiPayloadError` for any string, other number,
null, undefined, or non-integer. `nonEmptyText` remains used by unrelated
fields; no other parser behavior changes; export surface unchanged.

**Exact checks (LOCAL_NOW):** anchor inspection (two `contractVersion === 1`
guards; no remaining `nonEmptyText(source.contractVersion` occurrence);
strip-types load smoke. **DEFERRED_TO_INTEGRATION:** `R5-WIRE-01`–`03`
(S013); V2/V4. Completion checklist: as S001.

---

### KI-R5-S009 — explicit JSON mutation requests (client-api.ts)

```yaml
subwindow_id: KI-R5-S009
type: FILE
assignment_id: ASG-KI-R5-S009
assigned_agent: UNASSIGNED
predecessors: [KI-R5-S007]
writable_file: frontend/lib/client-api.ts
file_operation: MODIFY
starting_file_digest: b57d7b8609387243b8413a084303acf89c2fc4943ec170077321a01a3608c936
starting_repository_change_set_digest: recorded at dispatch
read_only_scope: [frontend/lib/keyword-intelligence-types.ts, KEYWORD_INTELLIGENCE_DECISION_LEDGER.md::DEC-KI-034/PAY-KI-008]
authorized_actions: [three-method edits + module-local projection, strip-types smoke, anchor inspection]
prohibited_actions: [common prohibitions, changing apiRequest shared behavior or any legacy caller]
```

**Mechanical trace:** `KI-R5-T4` items 5–7; DEC-KI-034 locked browser request
headers + locked selection input; findings `KI-PR-F02`, `KI-PR-F03`; cases
`R5-WIRE-05`, `R5-WIRE-06`.

**Exact file transformation (ordered):**
1. `createKeywordResearch` (anchor: line 56): add
   `headers: { "Content-Type": "application/json" }` to its init.
2. `saveKeywordSelection` (anchor: line 72): add the same header; add
   module-local `toSelectionMutation` using the exact frozen §3.1 guard and
   mapping (`sourceKind === "calculated"` requires a non-empty string
   `sourceKeywordId` and throws `new Error("calculated selection item
   requires a source id")` otherwise, returning the validated string before
   constructing `{ sourceKind: "calculated", sourceKeywordId, keyword }`;
   manual returns `{ sourceKind: "manual", keyword }`) and send
   `{ expectedRevision, items: toSelectionMutation(items) }` — no
   snapshot/derived field, no client identity authority; public signature
   unchanged (`items: SelectionItem[]`).
3. `startKeywordResearchRun` (anchor: line 84): add the same header; body
   stays exactly `{ expectedSelectionRevision, clientRequestId }`.
4. `apiRequest` (anchor: line 20) and every GET remain unchanged.

**Exact checks (LOCAL_NOW):** anchor inspection (three literal
`"Content-Type": "application/json"` additions; `toSelectionMutation` module-
local, not exported; body of PUT built from the projection); strip-types load
smoke. **DEFERRED_TO_INTEGRATION:** `R5-WIRE-05/06` init capture (S013);
`R5-WIRE-04` route boundary (S015/V4); V2/V4. Completion checklist: as S001.

---

### KI-R5-S010 — saved gate, projection, filter parity (view-model.ts)

```yaml
subwindow_id: KI-R5-S010
type: FILE
assignment_id: ASG-KI-R5-S010
assigned_agent: UNASSIGNED
predecessors: [KI-R5-S007]
writable_file: frontend/lib/keyword-intelligence-view-model.ts
file_operation: MODIFY
starting_file_digest: b91f0f5e7fd9f692e5f9086f1be0f511af1f0b6b755d117924497a52f89ce9d5
starting_repository_change_set_digest: recorded at dispatch
read_only_scope: [frontend/lib/keyword-intelligence-types.ts, KEYWORD_INTELLIGENCE_DECISION_LEDGER.md::DEC-KI-035/036]
authorized_actions: [module-local projection + gate/predicate edits, strip-types smoke, literal predicate spot-check]
prohibited_actions: [common prohibitions, new runtime exports (W5-I03 oracle byte-read-only), re-sorting persisted order]
```

**Mechanical trace:** `KI-R5-T4` items 5–6; DEC-KI-035 locked saved predicate;
DEC-KI-036 locked filter parity; findings `KI-PR-F05`, `KI-PR-F07`; cases
`R5-FIN-01`–`04`, `R5-EXP-01`–`04`.

**Exact file transformation (ordered):**
1. Add module-local `selectionSaveProjection(items: SelectionItem[])` using
   the exact frozen §3.1 guard and mapping — identical to S009
   `toSelectionMutation` byte-for-byte in behavior (calculated → validated
   non-empty string `sourceKeywordId`, throwing
   `"calculated selection item requires a source id"` on a null/non-string
   value before constructing the member; manual → `{sourceKind, keyword}`;
   manual items never read `sourceKeywordId`).
2. `canFinalizeSelection` (anchor: line 646): add reason `"unsaved"` to the
   union and insert, after the `over_limit` check and before the `conflicts`
   check, the saved predicate — draft is saved iff
   `selectionSaveProjection(draft)` deep-equals
   `selectionSaveProjection(view.selection.items)` by length, order,
   discriminator, source-ID presence/value, and exact keyword; unsaved returns
   `{ ok: false, reason: "unsaved" }`.
3. `haystack()` (anchor: line 185): remove the `r.mainIntent` and
   `(r.recommended ? "recommended" : "")` members.
4. `getFiltered()` (anchor: line 199): flags check
   `filter.flags.some(...)` → `filter.flags.every((fl) => (r.flags ||
   []).indexOf(fl) !== -1)`. No other predicate changes; persisted order
   preserved.

**Exact checks (LOCAL_NOW):** strip-types load smoke; anchor inspection; a
deterministic literal spot-check executed via
`node --experimental-strip-types --input-type=module -e` constructing literal
rows with flags `["a"]`, `["a","b"]`, `["b"]` and filter flags `["a","b"]`,
asserting `getFiltered` retains only the `["a","b"]` row, and asserting a
search for a `mainIntent`-only token returns zero rows.
**DEFERRED_TO_INTEGRATION:** `R5-EXP-01`–`04` literal oracles (S013);
`R5-FIN-02`–`04` actual dashboard gate (S015/V4); V2/V4. Completion checklist: as S001.

---

### KI-R5-S011 — remove browser manual-ID authority (selection-review.tsx)

```yaml
subwindow_id: KI-R5-S011
type: FILE
assignment_id: ASG-KI-R5-S011
assigned_agent: UNASSIGNED
predecessors: [KI-R5-S007]
writable_file: frontend/components/keyword-intelligence/selection-review.tsx
file_operation: MODIFY
starting_file_digest: 5d127c195a2553cc077b4b1a3f592add08a184b9761cfce658fbb810b248f992
starting_repository_change_set_digest: recorded at dispatch
read_only_scope: [frontend/lib/keyword-intelligence-types.ts, frontend/lib/keyword-intelligence-view-model.ts, KEYWORD_INTELLIGENCE_DECISION_LEDGER.md::DEC-KI-034]
authorized_actions: [ordered edits, anchor inspection]
prohibited_actions: [common prohibitions, any ksi_ derivation in browser code, prop/type changes outside the dashboard/review pair]
```

**Mechanical trace:** `KI-R5-T4` item 12 ("remove browser manual ID
authority"); DEC-KI-034 materialization; finding `KI-PR-F03`; case
`R5-SEL-02` (server-side counterpart), `R5-WIRE-05`.

**Exact file transformation (ordered):**
1. Expand the `SelectionReviewProps` type (anchor: line 26,
   `type SelectionReviewProps = { ... }`) to the frozen §3.1 contract
   (finding 5): `finalizeState: "idle" | "handing-off" | "succeeded" |
   "definitive_failure" | "retry_required"` (existing `"handing-off"` literal
   retained, three members added) and the new prop
   `onRetryHandoff: () => void`. No other prop is added, renamed, or removed;
   component prop/type changes remain confined to the dashboard/review pair.
2. Implement control inertness per §3.1: while `finalizeState` is
   `"handing-off"` or `"retry_required"`, the manual-add input and button,
   edit controls, remove controls, save button, and finalize button are
   disabled (`disabled`/`aria-disabled` per existing conventions); in
   `"retry_required"` render the literal retry notice
   `"The run request didn't complete. Retry the same run."` and an enabled
   retry button invoking `onRetryHandoff`; in `"succeeded"` all controls are
   disabled (navigation unmounts the surface); `"definitive_failure"` renders
   with idle-equivalent enablement while the dashboard shows the mapped
   error/stale banner — it adds no state-based control lock of its own, and
   the existing accepted-W5 409 `staleConflict` lock continues to apply
   unchanged.
3. Delete `MANUAL_ID_LANES`, `manualItemDigest`, and `stableManualItemId`
   (anchors: lines 57–79). The manual-add path now creates the draft row with
   the client-only key of §0.1 item 4 (`itemId: "draft_" + n`, monotonic per
   mounted session, collision increments; `sourceKind: "manual"`;
   `sourceKeywordId: null`; `metricsSnapshot: null`); displayed text and edit
   flows unchanged; no `ksi_` string is generated in this file.

**Exact checks (LOCAL_NOW):** anchor inspection (`manualItemDigest`/
`stableManualItemId`/`MANUAL_ID_LANES` absent; `"draft_"` key generation
present; zero `ksi_` literals; expanded `finalizeState` union and
`onRetryHandoff` prop present; the disabled logic is verified for **all
three** disabling states — `"handing-off"`, `"retry_required"`, and
`"succeeded"` each disable the manual-add/edit/remove/save/finalize controls
(with `"succeeded"` disabling everything) — and `"definitive_failure"`
introduces no state-based lock while the existing 409 `staleConflict` lock
remains present and unchanged).
**DEFERRED_TO_INTEGRATION:** actual component behavior
(S015/V4); V2/V4. Completion checklist: as S001.

---

### KI-R5-S012 — saved-only finalization and retry-required handoff (research-dashboard.tsx)

```yaml
subwindow_id: KI-R5-S012
type: FILE
assignment_id: ASG-KI-R5-S012
assigned_agent: UNASSIGNED
predecessors: [KI-R5-S009, KI-R5-S010, KI-R5-S011]
writable_file: frontend/components/keyword-intelligence/research-dashboard.tsx
file_operation: MODIFY
starting_file_digest: 94ba68eec79302352bdd6ac387bd8f27586ba0bb078d80b7b1390c56518ef023
starting_repository_change_set_digest: recorded at dispatch
read_only_scope: [frontend/lib/client-api.ts, frontend/lib/keyword-intelligence-view-model.ts, frontend/components/keyword-intelligence/selection-review.tsx, KEYWORD_INTELLIGENCE_DECISION_LEDGER.md::DEC-KI-035]
authorized_actions: [ordered edits, anchor inspection]
prohibited_actions: [common prohibitions, auto-save, browser persistence, clearing idempotency key on ambiguous outcomes]
```

**Mechanical trace:** `KI-R5-T4` items 6–10; DEC-KI-035 locked client attempt
lifecycle + saved predicate; findings `KI-PR-F05`, `KI-PR-F06`; cases
`R5-FIN-01`–`06`.

**Mechanical trace:** `KI-R5-T4` items 6–10; DEC-KI-035 locked client attempt
lifecycle + saved predicate; findings `KI-PR-F05`, `KI-PR-F06`; parent
finding 5 (state/prop wiring); cases `R5-FIN-01`–`06`.

**Exact file transformation (ordered):**
1. `handleSave` (anchor: line 213): on success keep replacing `view` with the
   canonical response and resetting the draft to its saved items (server is
   authority); retry/stale handling unchanged.
2. `handleFinalize` (anchor: line 240): gate stays `canFinalizeSelection`
   (now unsaved-aware); allocate `clientRequestId` once when entering from
   `idle` and pair it with the current saved `view.selectionRevision`; the
   state literals are exactly the frozen §3.1 union (`"idle"`, the existing
   `"handing-off"`, plus `"succeeded"`, `"definitive_failure"`,
   `"retry_required"`).
3. Classification: parsed HTTP `<500` is definitive — success sets
   `"succeeded"` and navigates (`router.push(handoff.statusUrl)`); `4xx`
   applies the existing safe UI mapping (409 → stale banner, else save
   error), clears `clientRequestIdRef`, and sets `"definitive_failure"`
   (controls remain enabled for a fresh attempt with a new ID); network
   failure, unreadable response, or `>=500` is ambiguous — retain the exact
   ID/revision, set `"retry_required"`, make draft/save/finalize controls
   inert (rendered by S011), and permit only retry of the same handoff with
   byte-identical ID and revision; another ambiguous outcome stays
   `"retry_required"`. The catch block no longer clears
   `clientRequestIdRef.current` on ambiguous outcomes.
4. Add `handleRetryHandoff` (wired to the S011 `onRetryHandoff` prop;
   enabled only in `"retry_required"`): re-enter `"handing-off"` and resend
   the byte-identical `{expectedSelectionRevision, clientRequestId}` pair
   through `startKeywordResearchRun`, with the same classification as step 3.
5. Reload semantics: only durable server state (GET) reconstructs the view;
   no unobserved result is claimed after reload; no browser persistence is
   added.

**Exact checks (LOCAL_NOW):** anchor inspection (`"retry_required"` and
`"definitive_failure"` and `"succeeded"` members; retry path sends the
retained ref with no re-allocation; no `clientRequestIdRef.current = null` on
the ambiguous path; `onRetryHandoff` wired; save replaces draft from
response). **DEFERRED_TO_INTEGRATION:** `R5-FIN-01`–`06` (S015/V4);
`R5-WIRE-06`; V2/V4. Completion checklist: as S001.

---

### KI-R5-S013 — frontend API registry: wire parsers, init capture, cross-side filters (api.test.ts)

```yaml
subwindow_id: KI-R5-S013
type: FILE
assignment_id: ASG-KI-R5-S013
assigned_agent: UNASSIGNED
predecessors: [KI-R5-S008, KI-R5-S009, KI-R5-S010]
writable_file: frontend/test/keyword-intelligence-api.test.ts
file_operation: MODIFY
starting_file_digest: a2f40c62bdf6d34136c2d6a318c8aef24e426581182a2d5edf0ef6fc950cd5c5
starting_repository_change_set_digest: recorded at dispatch
read_only_scope: [frontend/lib/keyword-intelligence-types.ts, frontend/lib/keyword-intelligence-validation.ts, frontend/lib/client-api.ts, frontend/lib/keyword-intelligence-view-model.ts, ../../email_scraper/src/api-serializer.js (imported from the test as "../../email_scraper/src/api-serializer.js"), KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md::R5-WIRE/R5-EXP rows]
authorized_actions: [numeric fixture corrections, additive registry/cases, supersede the four listed W5 oracles, run the focused file once, emit certificate]
prohibited_actions: [common prohibitions, weakening unrelated W5 cases, intercepted fixture presented as route evidence]
```

**Mechanical trace:** `KI-R5-T4` item 13 + `KI-R5-T5`; cases `R5-WIRE-01`,
`-02`, `-03`, `-05`, `-06`, `R5-EXP-01`–`04`; controls `R5-NC-01`, `R5-NC-02`,
`R5-NC-08`, `R5-NC-09`; supersession `{W5-A05, W5-A06, W5-A09, W5-A10}`;
DEC-KI-034/036/037; `SCN-KI-036`, `SCN-KI-039`.

**Exact file transformation (ordered):**
1. Correct every fixture to numeric `contractVersion: 1` (replace
   `"ki-research-v1"` strings at anchors 184–190, 242–249 and any remaining
   occurrence); supersede `W5-A05`, `W5-A06`, `W5-A09`, `W5-A10` oracles to the
   numeric contract, minimal PUT projection inputs, and draft-key manual rows,
   citing the R5 cases; every other W5 case byte-identical.
2. Add literal `const R5_FRONTEND_CASES = ["R5-WIRE-01","R5-WIRE-02","R5-WIRE-03","R5-WIRE-05","R5-WIRE-06","R5-EXP-01","R5-EXP-02","R5-EXP-03","R5-EXP-04"];`
   and implement each A4 row exactly: WIRE-01 parse an exact numeric-v1 queued
   response deep-equal; WIRE-02 serialize a parity-shaped completed research
   through the actual W4 `serializeKeywordResearch` (cross-repo import §0.1
   item 6) and parse the envelope through the actual W5 parser (numeric v1,
   all rows deep-equal, no invented field); WIRE-03 string/0/2/null/missing
   version partitions each `ApiPayloadError` with zero UI state; WIRE-05
   capture one 200-item request init (PUT, JSON header, strict minimal body
   ≤262144 bytes, no derived fields); WIRE-06 capture one handoff init (POST,
   JSON header, exact two-key body, one call); EXP-01 flags AND (rows with A,
   B, A+B → both sides retain only the A+B literal ID in persisted order);
   EXP-02 each allowed search corpus field (keyword/source seed/cluster/lane/
   facet/flag — exact literal IDs for every field); EXP-03 intent-only and
   synthetic `recommended` text excluded (zero rows on both sides unless also
   in allowed corpus); EXP-04 cumulative and named-market projection with null
   market excluded (literal item IDs/order and CSV rows equal). Expected sets
   are literals — neither implementation generates the other's oracle.
3. Implement controls NC-01 (cloned serialized object with `contractVersion`
   replaced by string `"1"` → `R5_NUMERIC_VERSION_REQUIRED`), NC-02 (cloned
   captured init with content-type header deleted →
   `R5_JSON_CONTENT_TYPE_REQUIRED`), NC-08 (divergent `some` predicate →
   `R5_FLAG_AND_REQUIRED`), NC-09 (corpus with `mainIntent`+`recommended`
   added → `R5_SEARCH_CORPUS_DIVERGED`) with the pass–mutate–fail–restore
   pattern.
4. Emit the registry `"frontend_api"` certificate line.

**Exact checks (LOCAL_NOW):** run exactly
`node --experimental-strip-types --test test/keyword-intelligence-api.test.ts`
from `frontend/` — every test passes, zero skip; certificate well-formed.
**DEFERRED_TO_INTEGRATION:** V2; V6 merge. Completion checklist: as S001.

---

### KI-R5-S014 — component registry: saved gate and retry lifecycle (components.test.ts) — SUPERSEDED BY C002

```yaml
subwindow_id: KI-R5-S014
type: FILE
assignment_id: ASG-KI-R5-S014
assigned_agent: UNASSIGNED
predecessors: [KI-R5-S010, KI-R5-S011, KI-R5-S012]
writable_file: frontend/test/keyword-intelligence-components.test.ts
file_operation: MODIFY
starting_file_digest: 6e14ecc8eed297a6ca608ec365799b6cb2da2914d231944cb6be3047e24fe168
starting_repository_change_set_digest: recorded at dispatch
read_only_scope: [frontend/lib/keyword-intelligence-view-model.ts, frontend/components/keyword-intelligence/research-dashboard.tsx, frontend/components/keyword-intelligence/selection-review.tsx, KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md::R5-FIN rows]
authorized_actions: [additive registry/cases, supersede the three listed W5 oracles, run the focused file once, emit certificate]
prohibited_actions: [common prohibitions, weakening unrelated W5 cases]
```

**Historical defective allocation:** this block must never be dispatched. Its
`R5-FIN-01`–`06` / `R5-NC-05` / `R5-NC-06` local model is superseded by C002;
the valid `W5-C05`, `W5-C08`, and `W5-C12` corrections remain in the file.
Current component-lifecycle ownership is S015/V4 under C002.

**Exact file transformation (ordered):**
1. Add literal `const R5_COMPONENT_CASES = ["R5-FIN-01","R5-FIN-02","R5-FIN-03","R5-FIN-04","R5-FIN-05","R5-FIN-06"];`
   implementing the A4 rows exactly: FIN-01 completed saved 1–100 draft → one
   POST with current revision/one ID, navigate on success; FIN-02 saved then
   add/remove without save → `unsaved`, zero POST for both partitions; FIN-03
   saved then edit/reorder/manual add → each `unsaved`, zero POST; FIN-04
   dirty draft then successful save → PUT once then POST once with incremented
   revision and exact saved items; FIN-05 network/unreadable/502/504 →
   retry-required, controls locked, second POST same ID/revision; FIN-06
   definitive parsed 409 → stale UI, attempt cleared, no automatic retry/run.
2. Implement NC-05 (synthetic handoff POST appended to a copied dirty-partition
   request trace → `R5_UNSAVED_HANDOFF_FORBIDDEN`) and NC-06 (copied ambiguous
   two-request trace with retry request ID replaced, then separately its
   revision → `R5_AMBIGUOUS_RETRY_IDENTITY_DIVERGED`).
3. Supersede `W5-C05`, `W5-C08`, `W5-C12` citing the R5 cases (filter
   every-flag semantics, export query mirror without self-derived CSV oracle
   divergence, scale ceilings under the new draft-key/projection rules); all
   other W5 cases byte-identical.
4. Emit the registry `"components"` certificate line.

**Exact checks (LOCAL_NOW):** run exactly
`node --experimental-strip-types --test test/keyword-intelligence-components.test.ts`
— full pass, zero skip. **DEFERRED_TO_INTEGRATION:** V2; V6. Completion
checklist: as S001.

---

### KI-R5-S015 — browser harness: real route witness and actual lifecycle capture (browser mjs)

```yaml
subwindow_id: KI-R5-S015
type: FILE
assignment_id: ASG-KI-R5-S015
assigned_agent: UNASSIGNED
predecessors: [KI-R5-S012, KI-R5-C002]
writable_file: frontend/test/browser/keyword-intelligence-dashboard.mjs
file_operation: MODIFY
starting_file_digest: d28cc1b5411d412edeba139f715da69ab5c09a8d67c543be4cc69719ef5e68a7
starting_repository_change_set_digest: recorded at dispatch
read_only_scope: [frontend/lib/client-api.ts, frontend/components/keyword-intelligence/research-dashboard.tsx, frontend/components/keyword-intelligence/selection-review.tsx, KEYWORD_INTELLIGENCE_DISCOVERY_DOSSIER.md::SRC-KI-036, KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md::R5-WIRE-04/R5-FIN rows]
authorized_actions: [replace/add browser registry/case edits, fixture corrections, supersede exactly the five listed browser oracles W5-B02/W5-B03/W5-B04/W5-B05/W5-R03, structural inspection only (execution deferred to V4)]
prohibited_actions: [common prohibitions, running the browser/build gate before V4, presenting intercepted fixtures as route evidence]
```

**Mechanical trace:** cases `R5-WIRE-04`, `R5-FIN-01`–`06`; controls
`R5-NC-05`, `R5-NC-06`, `R5-NC-11`; supersession
`{W5-B02, W5-B03, W5-B04, W5-B05, W5-R03}`; rerun set `W5-B01`–`B08`,
`W5-R01`–`R07` under V4; findings `KI-PR-F01`, `KI-PR-F02`, `KI-PR-F07`;
`SCN-KI-038`; DEC-KI-034/036/037.

**Exact file transformation (ordered):**
1. Correct all payload fixtures to numeric `contractVersion: 1`.
2. Replace the literal registry with exactly
   `const R5_BROWSER_CASES = ["R5-WIRE-04","R5-FIN-01","R5-FIN-02","R5-FIN-03","R5-FIN-04","R5-FIN-05","R5-FIN-06"];`.
   Implement `R5-WIRE-04` as before:
   with fixture interception disabled for that one call, submit the real
   client create request to the emitted Next pre-auth route and record the
   activation (request JSON header/body; real route responds 401, never 415;
   exactly one request).
3. Add the six FIN cases through the emitted, hydrated dashboard only: use CDP
   to operate rendered table/review controls and capture the intercepted
   production `fetch` requests; never call `startKeywordResearchRun`,
   `saveKeywordSelection`, a React callback, or a local handoff model directly.
   FIN-01 uses a completed saved one-to-100 selection and one rendered
   Finalize click: exactly one POST has the current revision and one generated
   ID, then the router navigation witness succeeds. FIN-02 changes a saved
   draft by actual table add and review remove controls; each rendered Finalize
   attempt is disabled/unsaved and records zero POST. FIN-03 uses the rendered
   edit dialog, actual remove-and-readd of a calculated row (the UI's real
   reorder path), and the manual-input/Add controls; each partition is unsaved
   with zero POST. FIN-04 makes a real dirty manual addition, clicks Save
   selection, observes exactly one PUT, canonical returned items and incremented
   revision, then Finalize records exactly one POST at that incremented revision.
   FIN-05 injects exactly network, unreadable JSON, 502, and 504 outcomes for
   the first real `/runs` POST; each must render retry-required with all
   draft/save/finalize controls disabled, and a rendered Retry makes a second
   POST with byte-equal request ID and revision. FIN-06 injects parsed 409 for
   the real POST; it must render stale UI, clear the attempt, make no automatic
   retry/run request, and leave only the documented reload/save recovery path.
4. Implement NC-05 by appending a synthetic POST only to a copied dirty actual
   request trace and requiring `R5_UNSAVED_HANDOFF_FORBIDDEN`; fresh dirty
   actual traces pass. Implement NC-06 by replacing only retry ID, then only
   retry revision, in copied ambiguous actual two-POST traces and requiring
   `R5_AMBIGUOUS_RETRY_IDENTITY_DIVERGED`; a fresh actual retry passes.
5. Replace the self-derived export oracle (the scenario that generated
   expected CSV via the frontend `getFiltered` helper, anchor ~1093–1109) with
   a literal expected CSV fixture tied to the exported query; supersede
   `W5-B02`–`B05`/`W5-R03` oracles (filter parity AND/corpus, numeric
   versions, mutation headers, retry-required presentation) citing the R5
   cases; every other browser scenario and capture name unchanged.
6. Implement NC-11: supply only an intercepted fixture-success record while
   omitting the emitted real-Next request activation record/status → the
   substitute-evidence validator throws `R5_REAL_NEXT_ROUTE_WITNESS_MISSING`;
   fresh pass-through reaches 401 and never 415.
7. Emit the seven-ID registry `"browser"` certificate line when the harness
   runs (V4), with all seven actual activation witnesses and zero skip.

**Exact checks (LOCAL_NOW):** `node --check`; anchor inspection
(`R5_BROWSER_CASES` seven-ID literal; numeric fixture versions; all FIN cases
use CDP-rendered controls/request capture; `getFiltered` no longer generates
the export oracle; pass-through case present). Execution is
**DEFERRED_TO_INTEGRATION:** V4 (single frozen browser gate with
`KI_W5_SKIP_BUILD=1` reusing the V4 `npm run check` build); V6 merge.
Completion checklist: as S001.

---

### KI-R5-S016 — inventory registry lint (inventory.test.ts)

```yaml
subwindow_id: KI-R5-S016
type: FILE
assignment_id: ASG-KI-R5-S016
assigned_agent: UNASSIGNED
predecessors: [KI-R5-S013, KI-R5-S015]
writable_file: frontend/test/keyword-intelligence-inventory.test.ts
file_operation: MODIFY
starting_file_digest: 67828152b71f9b05ec847d5fc0d3be238452d526aeffee8255e17b39a644f480
starting_repository_change_set_digest: recorded at dispatch
read_only_scope: [frontend/test/keyword-intelligence-api.test.ts, frontend/test/keyword-intelligence-components.test.ts, frontend/test/browser/keyword-intelligence-dashboard.mjs, KEYWORD_INTELLIGENCE_DECISION_LEDGER.md::DEC-KI-037]
authorized_actions: [additive static registry-lint assertions, run the focused file once]
prohibited_actions: [common prohibitions, changing any W5-I oracle, adding manifest case IDs or a certificate line]
```

**Mechanical trace:** `KI-R5-T5` additive registry obligation for the sixth
existing test/harness file (§0.1 item 2); input to `R5-CONF-03`
stable-registration evidence.

**Exact file transformation:** append one additive block that statically reads
the three sibling frontend test files and asserts (a) there is no
`R5_COMPONENT_CASES` literal or `registry: "components"` certificate;
`R5_FRONTEND_CASES` and the seven-ID `R5_BROWSER_CASES` arrays equal exactly
the amended A4-mandated ownership sets (sorted deep-equal), and (b) — corrected
per parent finding 6 — every `R5-*` case-ID reference discovered anywhere in
those files belongs to the exact owning registry for that ID (e.g.
`R5-FIN-01`–`06` and `R5-WIRE-04` only inside `R5_BROWSER_CASES` and their own
browser implementations; supersession comments citing an R5 ID are permitted
because the cited owner matches), and no undeclared R5 ID exists that is absent
from the two arrays and the manifest groups. No existing `W5-I0x` oracle, the
`KI_W5_EXECUTION_CERTIFICATE` emission, or any registration changes; no
manifest case ID or certificate is added here.

**Exact checks (LOCAL_NOW):** run exactly
`node --experimental-strip-types --test test/keyword-intelligence-inventory.test.ts`
— full pass, zero skip. **DEFERRED_TO_INTEGRATION:** V2. Completion checklist:
as S001.

---

### KI-R5-S017 — enforcement manifest fixture (new JSON)

```yaml
subwindow_id: KI-R5-S017
type: FILE
assignment_id: ASG-KI-R5-S017
assigned_agent: UNASSIGNED
predecessors: []
writable_file: email_scraper/test/fixtures/keyword-intelligence/ki-r5-enforcement-manifest-v1.json
file_operation: CREATE
starting_file_digest: ABSENT
starting_repository_change_set_digest: recorded at dispatch
read_only_scope: [KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md::Literal enforcement manifest]
authorized_actions: [create exactly the literal file, digest recompute]
prohibited_actions: [common prohibitions, any extra key/metadata/ID/order deviation]
```

**Mechanical trace:** DEC-KI-037 locked case set; A4 literal manifest table.

**Exact file transformation:** create the file with root exactly
`{"contractVersion":"ki-r5-enforcement-manifest-v1","groups":{...}}` and
groups/IDs exactly: `wire` `R5-WIRE-01`..`R5-WIRE-06`; `selection`
`R5-SEL-01`..`R5-SEL-08`; `finalization` `R5-FIN-01`..`R5-FIN-08`; `export`
`R5-EXP-01`..`R5-EXP-06`; `conformance` `R5-CONF-01`..`R5-CONF-06` — in the A4
order, no other key or ID.

**Exact checks (LOCAL_NOW):** `node -e` JSON parse; recompute the five
per-member-LF group digests and the 34-ID global digest and require the exact
A4 literals: wire
`64e53c38d37b28ebb8da1799fc5e1f2d75c3aa45b5ca78a79529fe1d0ec2c1c7`, selection
`a7fe88a15c03119d46e51bb3ccf9807440697c4d5381be7a0a0027b79f85bdf3`,
finalization
`14330e67aa5a4bbb72869f68806dc88757de40fe65e1dc1767a67008647cd8e5`, export
`6d4ca77b8da2019bbfa4f3f1046c62d27d4c9fceb1b2d4c12105f13d8e87b340`,
conformance
`5960be1734aed1a66b382de36e98723dcee41f4919299835963d01f818577c9a`, global
`507186e7489a3f9eec18eb5de78692dbc55a8d1d2d106544aa4295a98ac9be60`.
**DEFERRED_TO_INTEGRATION:** S018 consumption; V1/V6. Completion checklist:
as S001.

---

### KI-R5-S018 — enforcement test (new file)

```yaml
subwindow_id: KI-R5-S018
type: FILE
assignment_id: ASG-KI-R5-S018
assigned_agent: UNASSIGNED
predecessors: [KI-R5-S005, KI-R5-S006, KI-R5-S013, KI-R5-S015, KI-R5-S016, KI-R5-S017]
writable_file: email_scraper/test/keyword-intelligence-r5-enforcement.test.js
file_operation: CREATE
starting_file_digest: ABSENT
starting_repository_change_set_digest: recorded at dispatch
read_only_scope: [email_scraper/test/fixtures/keyword-intelligence/ki-r5-enforcement-manifest-v1.json, email_scraper/test/keyword-intelligence-api.test.js, email_scraper/test/keyword-intelligence-handoff.integration.test.js, frontend/test/keyword-intelligence-api.test.ts, frontend/test/browser/keyword-intelligence-dashboard.mjs, frontend/test/keyword-intelligence-components.test.ts, frontend/test/keyword-intelligence-inventory.test.ts, KEYWORD_INTELLIGENCE_SPECIFICATION_CHANGELOG.md, KEYWORD_INTELLIGENCE_DECISION_LEDGER.md::DEC-KI-037, git metadata of both nested repositories (read-only status/diff)]
authorized_actions: [create the enforcement test, local syntax/static checks only at leaf time (node --check, manifest parse, static five-registry enumeration with exact digests, NC-12 lint falsifications on synthetic in-memory copies), single execution during KI-R5-I001 with all four captured certificates]
prohibited_actions: [common prohibitions, executing the six CONF cases or the 34-ID merge at leaf time, running the enforcement test with a partial certificate set, running the enforcement test twice, executing DB/browser/build inside this test, mutating evidence or production source]
```

**Mechanical trace:** `KI-R5-T5` items 1–15; cases `R5-CONF-01`–`06`; control
`R5-NC-12`; DEC-KI-037; `SCN-KI-040`; standard Sections E6–E8, 10.3, 11.1;
parent finding 7 (single-run enforcement flow).

**Exact file transformation:** create the file containing the literal
`R5_CONFORMANCE_CASES = ["R5-CONF-01","R5-CONF-02","R5-CONF-03","R5-CONF-04","R5-CONF-05","R5-CONF-06"]`
and six cases, all gated on `KI_R5_EXECUTED_CERTIFICATES` supplying exactly
the four non-conformance certificates (`api`, `database`, `frontend_api`,
`browser`): CONF-01 manifest parse (exact root/groups/counts/
literals/digests; duplicates rejected before set creation); CONF-02 registry
enumeration and merge — statically derive the five `registered` sets by
parsing the registry files, require registered==required for all five with
exact digests and zero duplicate/unexpected ID, validate the four executed
certificates (registry identity, sorted arrays, per-registry digests, zero
skip), merge the 28 executed non-conformance IDs (wire 6 + selection 8 +
finalization 8 + export 6) with the six executed
conformance IDs, and assert the exact 34-ID required=registered=executed
equality with the global digest; CONF-03 accepted-test supersession lint —
the exact DEC-KI-037 sets: six W4 and twelve W5 mutable oracles, all stable
registrations, the 15-ID browser rerun set, and A7 invalidation presence,
with every changed oracle citing an R5 case and every unrelated accepted
ID/registration/witness/oracle unchanged; CONF-04 final-worktree scope lint —
nested `git -C email_scraper status --porcelain` and `git -C frontend status
--porcelain` changed sets are exact subsets of the 18 paths (F-007/F-008 as
untracked creates; the other 16 as modifications) with no
package/schema/worker/route-handler/auth/W6 path; CONF-05 substitute-fidelity
boundaries per DEC-KI-037 (backend fakes prove parsing/materialization/call
order not SQL; real-Prisma FIN-07/08; frontend fetch capture proves exact
init; Next pass-through proves the real handler 401-not-415 boundary;
intercepted dashboard fixture proves presentation only and is forbidden as
route evidence); CONF-06 enforcement controls NC-12 — in separate copied
evidence values, remove one required registration
(`R5_REQUIRED_SET_MISMATCH`), mark one ID skipped/filtered
(`R5_REQUIRED_CASE_SKIPPED`), duplicate one ID and add one unexpected ID
(`R5_CASE_ID_INVALID` each), clear one activation witness
(`R5_ACTIVATION_WITNESS_MISSING`), replace one forbidden-operation count with
no assertion (`R5_ORACLE_WEAKENED`), label intercepted presentation evidence
as route evidence (`R5_SUBSTITUTE_FIDELITY_DIVERGED`); untouched evidence
passes after every variant. On the single successful merge the test emits the
final merged `KI_R5_EXECUTION_CERTIFICATE` (registry `"merged"`, all 34 IDs,
global digest).

**Exact checks (LOCAL_NOW at leaf time — syntax/static only):** `node --check
test/keyword-intelligence-r5-enforcement.test.js` exits 0; the manifest
fixture parses with exact digests; the static registry-enumeration helper
resolves all five `registered` sets equal to required with exact digests
(read-only parse of the four case-registry files plus the local conformance
literal); each NC-12 lint function, fed synthetic in-memory copies, produces
its exact error for its mutation and passes untouched input — no certificate
input, no CONF-case execution, no test run requiring certificates.
**DEFERRED_TO_INTEGRATION:** the single `KI-R5-I001` enforcement run with all
four captured certificates; V6 independent recompute. Completion checklist:
as S001.

---

## 6. Verification gates

Leaf-local checks are listed per block (§5). Frozen whole-window gates
(DEC-KI-037; A4 `KI-R5-V1`–`V7`); each runs once on final frozen inputs after
all leaves are accepted; a later relevant edit invalidates and reruns only
affected gates; no Prisma generate/validate, worker build, full opted-in DB
suite, provider, AWS, or production operation:

| Gate | Exact command (cwd) | Required outcome |
|---|---|---|
| V1 backend non-DB | `node --test --test-isolation=none test/keyword-intelligence-api.test.js` (from `email_scraper/`); capture its `KI_R5_EXECUTION_CERTIFICATE` line | all selected cases pass, zero skip/todo, no legacy W4 regression; the `api` certificate is captured for I001 |
| V2 frontend focused | `node --experimental-strip-types --test --test-isolation=none test/keyword-intelligence-api.test.ts test/keyword-intelligence-components.test.ts test/keyword-intelligence-inventory.test.ts` (from `frontend/`); capture only the `frontend_api` certificate line | all selected R5 + existing component regression cases pass, no skip; actual serializer→parser and fetch-init witnesses present; no component R5 certificate exists or is accepted |
| V3 isolated DB (single run) | `DOTENV_CONFIG_QUIET=true ALLOW_DATABASE_TESTS=true node --require dotenv/config --test --test-isolation=none --test-name-pattern='^(?:KI-W4 database handoff registry \(D01-D06 in one disposable schema\)|.*R5-FIN-(?:07|08)|KI-R5 database execution certificate)$' test/keyword-intelligence-handoff.integration.test.js > /tmp/ki-r5-v3-state128.combined 2>&1` (from `email_scraper/`) with isolated non-production `TEST_DATABASE_URL` via `test/helpers/isolated-postgres.js`; capture the `database` certificate line from the fixed combined artifact | two fulfilled equal calls, one Run, unequal conflict, NC-07 falsified then production passes, zero residual schema; certificate captured for I001 |
| V4 frontend check + browser | `npm run check` (from `frontend/`), then the emitted keyword browser harness once with `KI_W5_SKIP_BUILD=1`; capture the seven-ID `browser` certificate line | check clean; all prior presentation cases plus `R5-WIRE-04` and actual-control `R5-FIN-01`–`06` pass; real route status 401 not 415; zero required skips/console errors/non-app URLs; no intercepted-route substitution; certificate captured for I001 |
| V5 backend regression | `npm test` then `npm run check:secrets` (from `email_scraper/`) | zero failures; only the previously guarded database skips; secrets clean |
| E1 enforcement (single, during I001) | `KI_R5_EXECUTED_CERTIFICATES='<all four captured certificates>' node --test --test-isolation=none test/keyword-intelligence-r5-enforcement.test.js` (from `email_scraper/`), executed exactly once by the window agent inside `KI-R5-I001` | CONF-01–06 pass with zero skip; five registered sets == required with exact digests; four certificates validated; merged 34-ID required=registered=executed equality with global digest; final merged certificate emitted |
| V6 window-agent merge verification | window agent recomputes all five manifest group digests and the global digest from the four captured certificates and the E1 merged certificate | exact required=registered=executed 34-ID equality; zero skip/duplicate/unexpected/unactivated/oracle failure; NC-01–NC-12 each falsified its unchanged oracle before restored production passed |
| V7 scale/privacy/scope oracles | window-agent verification from case evidence | 0/1/100/200 valid selections, 201 rejection, 143641-byte maximum, 19900 comparison bound, one CAS, one Run under concurrency, CSV textual safety/numeric stability, owner privacy, exact 18-path/symbol diff |

The enforcement test runs exactly once (E1, inside `KI-R5-I001`, after V1–V4
have captured all four non-conformance certificates); it is never run with a
partial certificate set and never repeated (`S1` §3.2/S018 prohibitions).

## 7. Correction and re-assessment rules

Append-only, per standard Sections 5.2, 10, 12.2: a diagnosed leaf or gate
failure yields `KI-R5-C<nnn>` owning exactly one file inside the 18-path set,
with a `CORRECTIVE-SUBWINDOW-READY` certificate (root cause, governing
decisions, corrected prior sub-window, invalidated evidence/gates, new
baseline digest); completed sub-window specifications are never rewritten;
every correction invalidates evidence whose inputs or asserted path include
that file; after the last correction the window agent executes a new
integration assessment `KI-R5-I<nnn>` reusing unchanged gates by exact
reference and rerunning every invalidated or parent-mandated final gate.
Unresolved repetition of the same parent-level ambiguity is a blocker. The
window agent never edits implementation files.

## 8. Authoring-readiness checklist (standard Section 11)

All 44 items checked with `S3` evidence; `N/A` is not used. Items cite
`EV-KI-R5-S01`–`S03`; the parent-review revision applying findings 1–7
(digest/import/schema-guard/projection/prop-contract/lint/enforcement-flow)
is recorded in `EV-KI-R5-S04` and §11.3, and the checks below remain true of
this revised document.

### 8.1 Authority and inheritance

- [x] `SW-A01` Parent assignment, window agent identity, and delegation authority are exact and current. Evidence: `EV-KI-R5-S01` (A5 state 112 = `ASG-KI-R5-WA-01`, `KI-R5-WINDOW-AGENT`, only KI-R5, delegation_policy names this standard).
- [x] `SW-A02` Parent and sub-window standards plus contract, decision, checklist, and state revisions are pinned and verified. Evidence: `EV-KI-R5-S01` (five recomputed SHA-256 equal A5 pins).
- [x] `SW-A03` Parent write, read, action, prohibition, successor, and stop boundaries are copied without expansion. Evidence: §1 (verbatim A4 scopes); `EV-KI-R5-S01`.
- [x] `SW-A04` Current repositories, dirty state, and owner-controlled changes are inventoried. Evidence: `EV-KI-R5-S01`, revised `EV-KI-R5-S04` (clean nested HEADs; 45-entry root set digest `c660d09a…` including this window's three subordinate artifacts; dispatch-time recompute authoritative).
- [x] `SW-A05` All three subordinate artifacts exist and their authorities do not overlap. Evidence: `EV-KI-R5-S03` (S1/S2/S3 created; status only in S2, evidence only in S3).
- [x] `SW-A06` Strict adjacent communication and no subagent delegation are enforced. Evidence: §1 prohibitions; §5 common prohibitions; §9 templates.

### 8.2 Decision and file-set closure

- [x] `SW-D01` Every parent requirement, invariant, decision, task, scenario, and coverage case is allocated to exact files and assertions. Evidence: §4 maps; A4 `KI-R5` T1–T5 fully allocated; unmapped counts zero (`EV-KI-R5-S03`).
- [x] `SW-D02` No missing parent-level decision or contradictory authority remains. Evidence: `EV-KI-R5-S02` (DEC-KI-034–037 + PAY-KI-008 complete; the W5-I01/I03 surface constraint resolved by §0.1 item 3 within existing decisions).
- [x] `SW-D03` Required changed-file set equals planned initial file set. Evidence: §2 (18/18; set digest recomputed = A4 literal).
- [x] `SW-D04` Every planned file has one initial sub-window and no initial sub-window owns more than one file. Evidence: §3/§5 (S001–S018 ↔ F-001–F-018 bijection).
- [x] `SW-D05` Every file operation, starting digest, anchor, interface, preserved behavior, and forbidden edit is exact. Evidence: §2 digests; §5 anchors/transformations; §3.1 interface freeze.
- [x] `SW-D06` The dependency graph is complete, sequential, acyclic, and justified by named outputs. Evidence: §3 edges name the consumed interface/registry per edge.
- [x] `SW-D07` Every cross-file interface is frozen before dependent execution. Evidence: §3.1 (frozen before S002/S009/S012/S013/S018).
- [x] `SW-D08` Every intermediate state has exact permitted checks, expected temporary failures, safety, resolver, and prohibitions. Evidence: §3.2 table.
- [x] `SW-D09` Separate production, test, fixture, schema, configuration, manifest, and generated files have separate sub-windows. Evidence: §3/§5 (e.g. api.js vs api.test.js; manifest JSON vs enforcement test).
- [x] `SW-D10` No rename, multi-output generator, formatter, installer, or command can violate the one-file write invariant. Evidence: §5 checks (every command is parse/check/test with write sets verified in V2 per leaf); no generator/formatter/installer is authorized.

### 8.3 Sub-window execution completeness

- [x] `SW-E01` Every file sub-window contains every field in Section 7. Evidence: §5 blocks (7.1 identity/authority YAML, 7.2 trace, 7.3 transformation, 7.4 checks, 7.5 checklist).
- [x] `SW-E02` Every sub-window prescribes exact ordered edits rather than design alternatives or broad verbs. Evidence: §5 numbered transformations with anchors and literals.
- [x] `SW-E03` Every sub-window has exact preflight, local checks, activation witnesses, assertions, and forbidden outcomes. Evidence: §5 per-block checks; §4.2 witness definitions.
- [x] `SW-E04` Every sub-window mechanically proves its attributable changed-file set is exactly one file. Evidence: §5 common preflight/handoff mechanics (V2 box per leaf).
- [x] `SW-E05` Every sub-window has exact evidence, handoff, stop, and successor-reservation rules. Evidence: §5 common prohibitions; §9 certificate template.
- [x] `SW-E06` Each subagent may report only to the window agent and cannot update subordinate or parent authority artifacts. Evidence: §1/§5 prohibitions (no state/evidence/contract edits by leaves).
- [x] `SW-E07` No sub-window requires successor work to satisfy its file-local acceptance. Evidence: §5 LOCAL_NOW checks complete per leaf; deferrals are explicit and owned by §6 gates.
- [x] `SW-E08` Deliberately deferred checks name the exact integration assessment that owns them. Evidence: §5 DEFERRED markers → `KI-R5-I001`/§6.

### 8.4 Enforcement and integration closure

- [x] `SW-V01` Coverage cases are allocated to exact test files, registrations, activation witnesses, and assertions. Evidence: §4.2 registry table.
- [x] `SW-V02` Required local and whole-window case-set equality and digest checks are prescribed. Evidence: S017/S018/V6 digest machinery.
- [x] `SW-V03` Every critical invariant has a negative control assigned at the narrowest effective level. Evidence: §4.2 NC-01–NC-12 ownership per A4 control table.
- [x] `SW-V04` Test substitutes and accepted tests/fixtures have exact fidelity and invalidation rules. Evidence: CONF-05 (DEC-KI-037 verbatim); §4.3 supersession sets.
- [x] `SW-V05` The initial integration assessment is fully authored with zero implementation-file write authority. Evidence: §10 `KI-R5-I001`.
- [x] `SW-V06` Frozen gates are exact, risk-proportionate, and scheduled at the final assessment rather than every leaf. Evidence: §6; DEC-KI-037 frozen-gate list 1:1.
- [x] `SW-V07` Correction diagnosis, one-file corrective assignment, invalidation, and reassessment rules are complete. Evidence: §7.
- [x] `SW-V08` The window agent must independently inspect every file handoff and personally execute every integration assessment. Evidence: §1; §10; standard Section 8 obligations restated in §9.
- [x] `SW-V09` Whole-window approval cannot pass through zero-work, skipped, filtered, duplicate, unexpected, unactivated, or summary-only evidence. Evidence: V6 oracle; CONF-02/06; NC-12.
- [x] `SW-V10` Parent handoff contents and `READY_FOR_PARENT_REVIEW` boundary are exact. Evidence: §9.3; §10 stop rule.

### 8.5 Mechanical and adversarial audit

- [x] `SW-R01` All IDs are unique and all references resolve. Evidence: `EV-KI-R5-S03` lint (S001–S018, F-001–F-018, 34 case IDs, 12 controls, 6 supersession+rerun sets; zero duplicate/unresolved).
- [x] `SW-R02` No unresolved placeholder exists in a checked item or assignable sub-window. Evidence: `EV-KI-R5-S03` (zero `___`/TBD in §5 blocks; assignment IDs issue at dispatch).
- [x] `SW-R03` Single-file write-set lint rejects zero, two, wildcard, directory, rename, and incidental workspace outputs for file sub-windows. Evidence: §11 counterexamples 1–3, 19.
- [x] `SW-R04` Removing one required file or requirement-to-file mapping makes readiness fail. Evidence: §11 counterexample 5; §4.1 complete allocation with zero unmapped.
- [x] `SW-R05` Removing, duplicating, skipping, filtering, or bypassing one required coverage case makes acceptance fail. Evidence: CONF-02/06 + NC-12 oracles; §11 counterexample 14.
- [x] `SW-R06` Weakening an oracle or diverging a substitute invalidates acceptance evidence. Evidence: NC-10/11/12 (`R5_ORACLE_WEAKENED`, `R5_SUBSTITUTE_FIDELITY_DIVERGED`); §11 counterexamples 15–16.
- [x] `SW-R07` Simulated second-file edit and direct parent communication are rejected. Evidence: §5 common preflight (changed-set equality) and prohibitions; §11 counterexamples 9–10.
- [x] `SW-R08` Simulated integration failure cannot be repaired by the window agent without a new corrective sub-window. Evidence: §7; §11 counterexamples 11–13.
- [x] `SW-R09` Parent decomposition review is recorded before the first implementation assignment. Evidence: S2 `AWAITING_PARENT_DECOMPOSITION_REVIEW`; no leaf assigned (`EV-KI-R5-S03`).
- [x] `SW-R10` Document lint reports zero missing fields, mappings, cases, evidence references, or authority conflicts. Evidence: `EV-KI-R5-S03`.

## 9. Handoff templates

### 9.1 Leaf execution certificate (returned by every implementation subagent)

```yaml
certificate: FILE-SUBWINDOW-EXECUTED
parent_window_id: KI-R5
subwindow_id: KI-R5-S0xx
assignment_id: ASG-KI-R5-S0xx
agent_identity: exact identity
writable_file: exact path
starting_file_digest: sha256 | ABSENT
ending_file_digest: sha256
starting_repository_change_set_digest: sha256
attributable_changed_file_set: [exact path]
required_local_cases: []
registered_local_cases: []
executed_local_cases: []
skipped_local_cases: []
duplicate_case_ids: []
unexpected_case_ids: []
missing_activation_witnesses: []
negative_controls_expected: exact integer
negative_controls_falsified: exact integer
commands: []
deferred_integration_checks: []
external_mutations: []
prohibited_actions_observed: []
successor_work_started: false
direct_parent_communication: false
status: AWAITING_WINDOW_REVIEW
```

The window agent independently inspects the diff and evidence (standard
Section 8: 13 checks) and appends exactly one disposition to `S3`:
`ACCEPTED_FOR_INTEGRATION`, `CORRECTION_REQUIRED`, or `PARENT_BLOCKED`.

### 9.2 Window-agent integration certificate (standard Section 12.4)

Appended to `S3` after a `PASS` assessment, with the exact field set of the
sub-window standard (`WINDOW-AGENT-INTEGRATION-PASS`, expected/actual changed
sets and digests, case counts/digests, control results, invalidations,
commands, `successor_parent_window_work_started: false`, `status:
READY_FOR_PARENT_REVIEW`).

### 9.3 Consolidated parent handoff (standard Section 12.5)

The window agent sends the parent only the consolidated report:
`READY_FOR_PARENT_REVIEW` or one exact blocker; S1/S2/S3 paths and revisions;
initial/corrective/failed/successful assessment IDs; expected/actual changed
sets and digests; current file digests; requirement/decision/task/scenario/
coverage trace closure; required/registered/executed counts and digests;
skipped/duplicate/unexpected/unactivated/failed cases; exact commands,
decisive outcomes, negative controls, parity limits; invalidated/superseded
evidence; external mutations, costs, skipped gates, residual risks, user
prerequisites; confirmation that no successor parent window began. Subagent
summaries are not forwarded as proof.

## 10. Integration assessment `KI-R5-I001` (fully authored before leaf execution)

```yaml
integration_assessment_id: KI-R5-I001
parent_window_id: KI-R5
assigned_to: KI-R5-WINDOW-AGENT
authorized_write_file: NONE (implementation files)
input: accepted S001..S018 dispositions, ending file digests, assembled tree, the four non-conformance certificates captured at V1 (api), V2 (frontend_api), V3 (database), and V4 (seven-ID browser)
gates: V1, V2, V3, V4, V5, E1 (single enforcement run with all four certificates), V6, V7 (Section 6)
result_oracle: PASS | CORRECTION_REQUIRED | PARENT_BLOCKED
```

**Contents (standard Section 9.2):**
1. Exact accepted sub-window IDs `KI-R5-S001`–`S018` (+ any `KI-R5-C<nnn>`)
   and their ending file digests.
2. Expected assembled changed-file set = the exact 18 paths with digest
   `efc82a88…`; actual set from nested git status must equal it exactly.
3. Requirement → decision → file → sub-window → assertion trace: A4 `KI-R5`
   T1–T5 rows mapped through §4 to §5 blocks and case oracles.
4. Complete required coverage set: the 34 manifest IDs; per-group and global
   digests per §4.2; required=registered=executed equality with zero
   skip/duplicate/unexpected/unactivated.
5. Gates: §6 V1–V7 with the exact commands, run limits, expected counts
   (34 IDs; NC-01–NC-12 falsified before production passes; W4/W5 supersession
   exact; 15 browser rerun IDs), assertions, activation witnesses, and
   forbidden outcomes (no provider/AWS/production/DB-outside-V3/build-outside-
   V4/commit action; no KI-W6/W7 work).
6. Negative controls: each NC executes its unchanged oracle PASS → mutation →
   `AssertionError` with the exact A4 message → restored production PASS.
7. Substitute fidelity: CONF-05 boundaries; intercepted presentation evidence
   is never route evidence.
8. Negative searches: no `ksi_` derivation in browser code; no string
   `contractVersion` in W5 fixtures; no `mainIntent`/synthetic `recommended`
   in either search corpus; no `.some` flag predicate; no apostrophe-free
   dangerous CSV cell; no package/schema/worker/route-handler/auth/W6 diff
   path; no direct parent-leaf communication.
9. Cost/privacy: `$0.00`; zero external mutations; no owner/raw/credential
   field in any response/export/certificate.
10. Invalidation policy: a correction to file F invalidates the gates whose
    inputs or asserted paths include F and reruns them plus the complete
    scope/coverage/secret/regression closure; unaffected costly gates are
    reused only with a recorded deterministic dependency proof.
11. Oracles: `PASS` only when every gate passes with witnesses and §9 of
    standard holds; any failed assertion is first recorded per standard
    Section 9.5 (observed/expected/activation/causal path/root cause/
    governing decisions/invalidations/correctability) before minimum ordered
    one-file corrections; parent-level ambiguity → `PARENT_BLOCKED`.

Assessment checklist (standard Section 9.4): I1–I10, unchecked until executed.

## 11. Amendment sections (append-only)

### 11.1 Corrective sub-windows

#### KI-R5-C001 — repair saved-selection projection source (view-model.ts)

```yaml
subwindow_id: KI-R5-C001
type: CORRECTION
parent_window_id: KI-R5
parent_assignment_id: ASG-KI-R5-WA-01
assigned_agent: UNASSIGNED
predecessors: [KI-R5-S010]
successor_reserved_for: KI-R5-WINDOW-AGENT
writable_file: frontend/lib/keyword-intelligence-view-model.ts
file_operation: MODIFY
starting_file_digest: 5a193f82981d865b44e082a39a374cdf77d7ec3300bbfc3659246709a8ed3df5
starting_repository_change_set_digest: 02530e7cc6bba4e59291f1eba4cf5464b784bbabac4dfb2384c33fae90f54a74
read_only_scope: [frontend/lib/keyword-intelligence-types.ts, frontend/components/keyword-intelligence/research-dashboard.tsx, frontend/components/keyword-intelligence/selection-review.tsx, KEYWORD_INTELLIGENCE_DECISION_LEDGER.md::DEC-KI-035]
authorized_actions: [replace exactly selectionSaveProjection(view.selection.items) with selectionSaveProjection(view.selection) at canFinalizeSelection]
prohibited_actions: [all common S1 §5 prohibitions, any second-file edit, any other source change, any test/fixture/oracle change, any export/interface change, any formatting or reorder, any S013 work, provider/AWS/DB operation, commit/push]
may_start_successor: false
```

Correction authority and diagnosis: EV-KI-R5-S21 recorded the live TypeError
and root cause. EV-KI-A-054 and CHG-KI-029 authorize exactly this one-file
correction; the frozen ResearchView contract makes view.selection the
SelectionItem[] authority. The correction is governed by DEC-KI-035 and the
existing S010 projection/saved-gate requirement; it introduces no new
decision or interface.

Exact transformation (one expression only):

1. At canFinalizeSelection, line 663 in the accepted S010 ending source,
   replace the exact expression
   selectionSaveProjection(view.selection.items) with
   selectionSaveProjection(view.selection).
2. Preserve every other byte, including the proposed-draft projection,
   ordering comparison, conflict ordering, filter implementation, exports,
   error literal, and all unrelated S010 behavior.

Exact LOCAL_NOW checks:

- P1: verify the live starting digest and repository change-set digest above;
  the writable file is the only attributable target.
- T1: git diff proves the exact one-expression replacement and no other hunk;
  no second workspace path changes.
- V1: run node --experimental-strip-types --input-type=module -e from
  frontend/ importing ./lib/keyword-intelligence-view-model.ts, construct a
  completed view with selection as a SelectionItem[] and no conflicts, and
  assert canFinalizeSelection(view, equalDraft) returns {ok:true,reason:""};
  assert a keyword-different draft returns {ok:false,reason:"unsaved"}; assert
  neither call throws a TypeError.
- V2: compare repository changed-file sets before/after and require the
  attributable set to equal exactly
  [frontend/lib/keyword-intelligence-view-model.ts].
- V3: no local coverage IDs are registered or executed; integration cases
  remain deferred to their existing owners.
- H1/H2: return the exact diff, ending digest, commands/outcomes, and
  residual obligations; stop at AWAITING_WINDOW_REVIEW; do not start S013 or
  any successor.

DEFERRED_TO_INTEGRATION: only the affected canFinalizeSelection portion of
EV-KI-R5-S16 is superseded by C001; S16's filter/projection proof remains
valid. EV-KI-R5-S20's unchanged S012 implementation is dependency-revalidated
after C001 acceptance without an implementation rerun. S013 remains unexecuted
until C001 is accepted. Final V2/V4 and the complete integration gates remain
owned by KI-R5-I001.

Corrective-subwindow completion checklist:

- [ ] P1 assignment, revisions, predecessor, writable file, baseline digest, and root change-set digest match.
- [ ] P2 starting repository status and protected dirty state match.
- [ ] T1 exact one-expression replacement and no other edit.
- [ ] V1 both direct saved/unsaved oracles pass without TypeError.
- [ ] V2 attributable changed-file set is exactly the writable file.
- [ ] V3 no unowned local coverage is registered or executed.
- [ ] H1 exact certificate, diff, digest, commands, and residual obligations returned.
- [ ] H2 no prohibited action, successor work, external mutation, or parent communication.
- [ ] H3 stop at AWAITING_WINDOW_REVIEW.

CORRECTIVE-SUBWINDOW-READY certificate:

```yaml
certificate: CORRECTIVE-SUBWINDOW-READY
parent_window_id: KI-R5
corrective_subwindow_id: KI-R5-C001
window_agent_identity: KI-R5-WINDOW-AGENT
trigger_evidence: [EV-KI-R5-S21, EV-KI-A-054, CHG-KI-029]
root_cause: canFinalizeSelection passes view.selection.items although ResearchView.selection is SelectionItem[]
governing_parent_requirements: [KI-R5-T4, DEC-KI-035]
governing_parent_decisions: [DEC-KI-035]
corrected_prior_subwindows: [KI-R5-S010]
writable_file: frontend/lib/keyword-intelligence-view-model.ts
starting_file_digest: 5a193f82981d865b44e082a39a374cdf77d7ec3300bbfc3659246709a8ed3df5
predecessors: [KI-R5-S010]
invalidated_evidence: [EV-KI-R5-S16 canFinalizeSelection proof and resulting-file digest only]
invalidated_gates: [S013 local supersession and any gate consuming the erroneous canFinalizeSelection path]
unresolved_parent_decisions: []
expanded_parent_scope_required: false
section_7_fields_complete: true
single_file_write_set: true
unresolved_execution_choices: []
next_integration_assessment_id: KI-R5-I001
status: READY
```

#### KI-R5-C002 — remove invalid local lifecycle model (components.test.ts)

```yaml
subwindow_id: KI-R5-C002
type: CORRECTION
parent_window_id: KI-R5
parent_assignment_id: ASG-KI-R5-WA-01
assigned_agent: UNASSIGNED
predecessors: [KI-R5-S014]
successor_reserved_for: KI-R5-WINDOW-AGENT
writable_file: frontend/test/keyword-intelligence-components.test.ts
file_operation: MODIFY
starting_file_digest: 2fcb1c88df97f2471ed78a94d7e8aa70a91d89f206632213a75a4c4ebc3d6ba4
starting_repository_change_set_digest: c660d09a800e8a5fd446bd65039f55241d5d7bb4e4c7ef656fe4fc7dcc88417c
read_only_scope: [frontend/components/keyword-intelligence/research-dashboard.tsx, frontend/components/keyword-intelligence/selection-review.tsx, frontend/test/browser/keyword-intelligence-dashboard.mjs, KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md::R5-FIN rows]
authorized_actions: [remove the rejected-model-only editSelectedItemText import and invented R5_COMPONENT_CASES local handoff/retry model, remove R5-FIN-01 through R5-FIN-06 and R5-NC-05/R5-NC-06 subtests, remove the components R5 execution certificate, preserve the W5-C05/W5-C08/W5-C12 corrections and every unrelated W5 assertion, run the focused component regression file once]
prohibited_actions: [all common S1 §5 prohibitions, any second-file edit, adding or retaining a replacement R5 registry/certificate/model, changing W5-C05/W5-C08/W5-C12 or any other W5 oracle, browser/build/enforcement/DB execution, provider/AWS/production operation, commit/push]
may_start_successor: false
```

Correction authority and diagnosis: `EV-KI-R5-S26` proves that S014's
handoff()/retryHandoff() trace is a newly invented local state machine and
cannot satisfy `SCN-KI-038` actual component state/request capture.
`EV-KI-A-056` / `CHG-KI-031` / A5 state 117 authorize this exact C002 and
reallocate the seven real lifecycle witnesses to revised S015; no case ID,
manifest group, per-group digest, global digest, source interface, or W5
assertion changes here.

Exact transformation (ordered):

1. Delete the contiguous S014-added local-model region beginning with literal
   `const R5_COMPONENT_CASES = ["R5-FIN-01","R5-FIN-02","R5-FIN-03","R5-FIN-04","R5-FIN-05","R5-FIN-06"];`
   and ending with `runR5ComponentCase`, including only its supporting
   `ComponentRequest`, `HandoffOutcome`, `HandoffResult`,
   `R5_CLIENT_REQUEST_ID`, `savedView`, `handoff`, `retryHandoff`,
   `assertUnsavedHandoffForbidden`, and `assertRetryIdentity` declarations.
2. Remove `editSelectedItemText` from the named
   `../lib/keyword-intelligence-view-model.ts` import: it is used only by the
   rejected local model and no retained W5 assertion consumes it.
3. Delete the entire test named `R5 component finalization registry`, including
   its six FIN subtests, NC-05/NC-06 subtests, digest assertion, and emitted
   `registry: "components"` execution certificate.
4. Preserve byte/semantic behavior of `REGISTERED_CASE_IDS`, its accepted W5
   certificate, and all existing W5 tests. No empty R5 array, no placeholder
   certificate, no local replacement trace, and no R5-FIN/R5-NC-05/R5-NC-06
   reference may remain in this file.

Exact LOCAL_NOW checks:

- P1: verify the live file/root digests above and that the frontend/backend
  nested worktrees are otherwise clean.
- T1: the attributable diff names exactly this one file; it removes the two
  specified contiguous S014 additions and the rejected-model-only
  `editSelectedItemText` import, with no additions except whitespace required
  by their removal.
- V1: run exactly `node --experimental-strip-types --test
  test/keyword-intelligence-components.test.ts` from `frontend/`; all retained
  W5 component regressions pass, zero skip, and its existing W5 certificate is
  unchanged.
- V2: static absence checks find no `editSelectedItemText`,
  `R5_COMPONENT_CASES`, `registry: "components"`, `handoff(`,
  `retryHandoff(`, `R5-FIN-`, `R5-NC-05`, or `R5-NC-06` in this file; the
  S015 browser registry alone owns all transferred A4 FCOMP IDs/controls.
- V3: no R5 execution certificate is emitted and no browser/build/enforcement
  gate is run. C002 acceptance is a mandatory predecessor of S015; S015 is
  not started by the C002 leaf.
- H1/H2: return exact diff/digest/command outcome and stop at
  `AWAITING_WINDOW_REVIEW` with no successor, external mutation, or commit.

DEFERRED_TO_INTEGRATION: S014 was rejected and no final gate ran, so C002
invalidates no accepted evidence or executed gate. This amendment supersedes
the planned V2/V4/E1/V6 certificate specification only: the S015 browser
registry alone produces `R5-FIN-01`–`06` / `R5-NC-05` / `R5-NC-06` A4 FCOMP
lifecycle evidence at V4 after C002 is accepted. V2 runs the retained component
regression but captures only `frontend_api`; V4/V6/E1 consume the four-
certificate allocation in §0.1/§6.

Corrective-subwindow completion checklist:

- [ ] P1 live A5 assignment `ASG-KI-R5-WA-01` and parent-approved decomposition revision recorded at dispatch, predecessor evidence, writable file, and both starting digests match (authoring authority historically traces to A5 state 117).
- [ ] P2 only the assigned file is attributable; nested repositories/protected root state match.
- [ ] T1 exact local model, rejected-model-only editSelectedItemText import, and R5 component-registry test are removed.
- [ ] T2 valid W5-C05/W5-C08/W5-C12 corrections and all other W5 assertions remain unchanged.
- [ ] V1 retained focused component regression passes with zero skip.
- [ ] V2 all forbidden local-model/registry/certificate references are absent.
- [ ] V3 no R5 certificate, browser/build/enforcement/DB, successor, external action, or commit occurs.
- [ ] H1 exact certificate/diff/digest/commands/residual obligations returned at AWAITING_WINDOW_REVIEW.

CORRECTIVE-SUBWINDOW-READY certificate:

```yaml
certificate: CORRECTIVE-SUBWINDOW-READY
parent_window_id: KI-R5
corrective_subwindow_id: KI-R5-C002
window_agent_identity: KI-R5-WINDOW-AGENT
trigger_evidence: [EV-KI-R5-S26, EV-KI-A-056, CHG-KI-031]
root_cause: S014 proved FIN lifecycle outcomes through an invented local handoff/retry model instead of SCN-KI-038 actual component state/request capture
governing_parent_requirements: [KI-R5-T4, KI-R5-T5, SCN-KI-038, DEC-KI-035, DEC-KI-037]
governing_parent_decisions: [DEC-KI-035, DEC-KI-037]
corrected_prior_subwindows: [KI-R5-S014]
writable_file: frontend/test/keyword-intelligence-components.test.ts
starting_file_digest: 2fcb1c88df97f2471ed78a94d7e8aa70a91d89f206632213a75a4c4ebc3d6ba4
predecessors: [KI-R5-S014]
successor_dependency: KI-R5-S015
invalidated_evidence: []
invalidated_gates: []
unresolved_parent_decisions: []
expanded_parent_scope_required: false
section_7_fields_complete: true
single_file_write_set: true
unresolved_execution_choices: []
next_integration_assessment_id: KI-R5-I001
status: READY
```

#### KI-R5-C003 — requester-supplied FIN-04 rendered-save correction (review only)

```yaml
subwindow_id: KI-R5-C003
type: CORRECTION
parent_window_id: KI-R5
parent_assignment_id: ASG-KI-R5-WA-01
implementation_origin: REQUESTER_DIRECT_COMMIT
requester_commit: 4dd9b4f0357b7c118d6c8ea92af212c7ff0693ba
requester_commit_parent: d4763a771734dfe043d59e2a4ae5b0dc6e0371c9
assigned_agent: KI-R5-WINDOW-AGENT
predecessors: [KI-R5-S015]
successor_reserved_for: KI-R5-WINDOW-AGENT
writable_file: NONE
review_target: frontend/test/browser/keyword-intelligence-dashboard.mjs
file_operation: REVIEW_ONLY
starting_file_digest: ea7ab5ff8ac6368ff278520fa79876dcd30c8764fb3e8f6fb7a066cf3d95805d
candidate_file_digest: 1c4cc5ae801f586398cf2e7a30c785f84868001d215fd85bd3d1bc0a920deb01
starting_repository_change_set_digest: c660d09a800e8a5fd446bd65039f55241d5d7bb4e4c7ef656fe4fc7dcc88417c
read_only_scope: [frontend/test/browser/keyword-intelligence-dashboard.mjs, KEYWORD_INTELLIGENCE_KI_R5_SUBWINDOW_CHECKLIST.md::KI-R5-S015, ACTIVE_EXECUTION_STATE.md, KEYWORD_INTELLIGENCE_EXECUTION_EVIDENCE.md::EV-KI-A-061]
authorized_actions: [review only the supplied requester commit, prove exact ancestry and one-file four-insertion diff, run node --check and complete S015 structural LOCAL_NOW inspection, accept or reject without implementation edit or leaf assignment]
prohibited_actions: [all implementation-file edits, assigning a C003 leaf, amending/replacing requester commit, browser/build/enforcement/database/full-regression execution, changing registries/cases/controls/certificates/S017/W5 oracles, successor work before acceptance, provider/AWS/production operation, commit/push]
may_start_successor: false
```

Correction authority: A5 state 122, `EV-KI-A-061`, and `CHG-KI-036` accept
the diagnosed `EV-KI-R5-S34` defect and authorize this requester exception.
The requester-supplied commit is not implementation authority for the window
agent and does not bypass independent review. It corrects only the omitted
rendered Save selection activation in `R5-FIN-04`; no parent-level behavior
decision, registry/case/control allocation, certificate topology, manifest
literal, or frozen V4 timing changes.

Exact review oracle:

1. Prove commit `4dd9b4f0357b7c118d6c8ea92af212c7ff0693ba` has exactly parent
   `d4763a771734dfe043d59e2a4ae5b0dc6e0371c9`, changes only the review target,
   and has exactly four insertions: three explanatory comment lines and one
   rendered Save selection click immediately between the dirty-three-item
   readiness wait and the `waitForInPage` FIN-04 PUT witness.
2. Prove the recorded pre-fix/candidate/root digests and clean nested worktrees
   match. Run exactly `node --check test/browser/keyword-intelligence-dashboard.mjs`
   from `frontend/`.
3. Repeat S015 LOCAL_NOW structural inspection without V4: the numeric fixture
   versions remain exact; `R5_BROWSER_CASES` remains exactly the seven owned
   IDs; every FIN case activates rendered CDP controls/request capture; the
   seed-dresses export oracle remains the literal CSV rather than runtime
   `getFiltered` derivation; real-route pass-through/NC-11 remains present;
   the browser certificate remains deferred to harness execution at V4.
4. Prove the four-line diff changes no other R5/W5 assertion, registry,
   certificate, control, S017 literal, or scope path. Do not run browser,
   build, enforcement, database, full regression, provider, AWS, production,
   or successor work.

Review-only completion checklist:

- [ ] P1 A5 state 122, EV-KI-A-061/CHG-KI-036, exact ancestry, target, and all three digests match.
- [ ] T1 Exactly three explanatory comment lines plus one rendered Save selection click occur at the frozen FIN-04 placement.
- [ ] V1 `node --check` passes; the complete S015 structural LOCAL_NOW inspection passes without V4.
- [ ] V2 All unaffected registry/case/control/certificate/S017/W5 structures remain unchanged; no prohibited action or successor work occurred.
- [ ] H1 Window agent appends the independent disposition with exact diff/digest/command evidence to S3.

REVIEW-ONLY-CORRECTIVE-SUBWINDOW-READY certificate:

```yaml
certificate: REVIEW-ONLY-CORRECTIVE-SUBWINDOW-READY
parent_window_id: KI-R5
corrective_subwindow_id: KI-R5-C003
implementation_origin: REQUESTER_DIRECT_COMMIT
requester_commit: 4dd9b4f0357b7c118d6c8ea92af212c7ff0693ba
requester_commit_parent: d4763a771734dfe043d59e2a4ae5b0dc6e0371c9
window_agent_identity: KI-R5-WINDOW-AGENT
trigger_evidence: [EV-KI-R5-S34, EV-KI-A-061, CHG-KI-036]
root_cause: S015 R5-FIN-04 waited for a selection PUT without clicking the rendered Save selection control that activates it
corrected_prior_subwindows: [KI-R5-S015]
writable_file: NONE
review_target: frontend/test/browser/keyword-intelligence-dashboard.mjs
starting_file_digest: ea7ab5ff8ac6368ff278520fa79876dcd30c8764fb3e8f6fb7a066cf3d95805d
candidate_file_digest: 1c4cc5ae801f586398cf2e7a30c785f84868001d215fd85bd3d1bc0a920deb01
predecessors: [KI-R5-S015]
successor_dependency: KI-R5-S016
invalidated_evidence: [EV-KI-R5-S34 blocked disposition only]
invalidated_gates: []
unresolved_parent_decisions: []
expanded_parent_scope_required: false
section_7_fields_complete: true
single_file_write_set: true
unresolved_execution_choices: []
next_integration_assessment_id: KI-R5-I001
status: READY
```

#### KI-R5-C004 — align frozen inventory fixtures to the accepted numeric contract

```yaml
subwindow_id: KI-R5-C004
type: CORRECTION
parent_window_id: KI-R5
parent_assignment_id: ASG-KI-R5-WA-01
assigned_agent: KI-R5-C004-LEAF
predecessors: [KI-R5-S008]
successor_dependency: KI-R5-S016
writable_file: frontend/test/keyword-intelligence-inventory.test.ts
file_operation: MODIFY
starting_file_digest: 67828152b71f9b05ec847d5fc0d3be238452d526aeffee8255e17b39a644f480
starting_repository_change_set_digest: c660d09a800e8a5fd446bd65039f55241d5d7bb4e4c7ef656fe4fc7dcc88417c
read_only_scope: [frontend/lib/keyword-intelligence-validation.ts, KEYWORD_INTELLIGENCE_DECISION_LEDGER.md::DEC-KI-037, KEYWORD_INTELLIGENCE_KI_R5_SUBWINDOW_CHECKLIST.md::KI-R5-S016]
authorized_actions: [replace only the two legacy contractVersion fixture strings in result and minimalView with numeric literal 1, run the focused inventory test once]
prohibited_actions: [all common S1 §5 prohibitions, any second-file edit, changing any W5-I02 assertion/control/export-surface oracle/negative control, any registry/certificate/S016 addition, any other inventory-test byte change, browser/build/enforcement/database/full-regression execution, provider/AWS/production operation, commit/push]
may_start_successor: false
```

Correction authority and diagnosis: A5 state 123, `EV-KI-A-062`, and
`CHG-KI-037` authorize this one-file corrective leaf after `EV-KI-R5-S36`
proved that the frozen W5-I02 fixture cannot pass accepted S008's numeric-only
parser. The correction restores the already-accepted wire contract; it creates
no product-interface, registry, case, certificate, or parser decision.

Exact transformation:

1. In `result()`, replace only `contractVersion: "ki-research-v1"` with
   `contractVersion: 1`.
2. In `minimalView()`, make the same replacement.
3. Preserve every other byte, including W5-I02's `assert.doesNotThrow`, its
   export-surface assertion, its negative controls, every other W5-I oracle,
   and the deferred S016 registry-lint block.

Exact LOCAL_NOW checks:

- P1: verify the predecessor, both starting digests, clean nested worktrees,
  and one writable file at dispatch.
- T1: prove the attributable diff is exactly the inventory test with exactly
  two string-to-numeric replacements and no other hunk.
- V1: from `frontend/`, run exactly `node --experimental-strip-types --test
  test/keyword-intelligence-inventory.test.ts`; require full pass and zero
  skip.
- V2: prove there are zero remaining `contractVersion: "ki-research-v1"`
  occurrences and exactly two `contractVersion: 1` fixture occurrences; no
  registry, certificate, manifest case ID, V2/V4/build/browser/database/full
  regression, or integration gate runs.
- H1/H2: return the exact diff, ending digest, command outcome, and residual
  obligation to resume S016 under C004's ending digest; stop at
  `AWAITING_WINDOW_REVIEW` without successor work or commit.

Corrective-subwindow completion checklist:

- [ ] P1 parent authority, predecessor, writable file, both starting digests, and clean worktrees match.
- [ ] T1 exactly the two frozen fixture literals changed in exactly one file.
- [ ] V1 focused inventory test passes in full with zero skip.
- [ ] V2 no legacy fixture literal remains; exactly two numeric fixture literals remain; W5-I02 and every other W5-I oracle are unchanged.
- [ ] V3 no registry/certificate/S016 addition or deferred integration gate ran.
- [ ] H1 exact certificate/diff/digest/command/residual obligation returned at AWAITING_WINDOW_REVIEW.

CORRECTIVE-SUBWINDOW-READY certificate:

```yaml
certificate: CORRECTIVE-SUBWINDOW-READY
parent_window_id: KI-R5
corrective_subwindow_id: KI-R5-C004
window_agent_identity: KI-R5-WINDOW-AGENT
trigger_evidence: [EV-KI-R5-S36, EV-KI-A-062, CHG-KI-037]
root_cause: W5-I02 result and minimalView fixtures retained string ki-research-v1 while accepted S008 parseResearchView accepts only numeric contractVersion 1
governing_parent_requirements: [KI-R5-T5, DEC-KI-037]
governing_parent_decisions: [DEC-KI-037]
corrected_prior_subwindows: [KI-R5-S008]
writable_file: frontend/test/keyword-intelligence-inventory.test.ts
starting_file_digest: 67828152b71f9b05ec847d5fc0d3be238452d526aeffee8255e17b39a644f480
predecessors: [KI-R5-S008]
successor_dependency: KI-R5-S016
invalidated_evidence: [EV-KI-R5-S36 blocked S016 baseline disposition only]
invalidated_gates: []
unresolved_parent_decisions: []
expanded_parent_scope_required: false
section_7_fields_complete: true
single_file_write_set: true
unresolved_execution_choices: []
next_integration_assessment_id: KI-R5-I001
status: READY
```

#### KI-R5-C005 — correct browser-harness empty-row counting and reorder visibility

```yaml
subwindow_id: KI-R5-C005
type: CORRECTION
parent_window_id: KI-R5
parent_assignment_id: ASG-KI-R5-WA-01
assignment_id: ASG-KI-R5-C005
assigned_agent: KI-R5-C005-LEAF
predecessors: [KI-R5-S015, KI-R5-C003]
successor_reserved_for: KI-R5-WINDOW-AGENT
writable_file: frontend/test/browser/keyword-intelligence-dashboard.mjs
file_operation: MODIFY
starting_file_digest: 1c4cc5ae801f586398cf2e7a30c785f84868001d215fd85bd3d1bc0a920deb01
starting_repository_commit: a0477d5ae71b24f91826a5ceabf68d90aa66666b
starting_repository_change_set_digest: c660d09a800e8a5fd446bd65039f55241d5d7bb4e4c7ef656fe4fc7dcc88417c
read_only_scope: [frontend/components/keyword-intelligence/keyword-table.tsx, frontend/components/keyword-intelligence/research-dashboard.tsx, KEYWORD_INTELLIGENCE_EXECUTION_EVIDENCE.md::EV-KI-A-070, KEYWORD_INTELLIGENCE_EXECUTION_EVIDENCE.md::EV-KI-A-071]
authorized_actions: [change only W5-B02 uiFlagRows from tbody tr to tbody tr input[type=checkbox], immediately after the R5-FIN-03 one-item post-remove witness select keyword-table page size 50 and wait 250 ms before the existing keyword-1 lookup, run only node --check test/browser/keyword-intelligence-dashboard.mjs]
prohibited_actions: [all common S1 §5 prohibitions, any second-file edit, browser/build/database/enforcement/full-regression execution, changing any fixture/registry/case ID/certificate digest/control/product oracle, changing W5-B02 beyond the uiFlagRows selector count, changing R5-FIN-03 beyond the page-size-50 visibility step, manual generated-evidence manipulation, provider/AWS/production operation, commit/push]
may_start_successor: false
```

Correction authority and diagnosis: A5 state 132, `EV-KI-A-070`, `EV-KI-A-071`,
`CHG-KI-045`, and `CHG-KI-046` authorize exactly this corrective leaf from the
clean requester commit baseline. The failed V4 browser member identified two
harness mechanics only: a zero-result placeholder row is not a keyword row,
and low-volume row 1 is outside the default 25-row page. No product behavior,
fixture, registry, certificate formula, control, or expected oracle changes.

Exact transformation:

1. In W5-B02, replace only the DOM-count selector for `uiFlagRows` from all
   keyword-table `tbody tr` elements to keyword-table
   `tbody tr input[type=checkbox]` elements. The existing comparison against
   zero stays unchanged.
2. In R5-FIN-03, immediately after the existing one-item `draft after remove`
   witness and before the existing `keyword 1` row lookup, call
   `setSelectValue(cdp, '[data-surface="surface:keyword-table"] select', '50')`
   and wait exactly 250 milliseconds. Preserve the existing remove, row-1
   lookup, re-add, order, unsaved, and zero-POST assertions byte-for-byte.

Exact LOCAL_NOW checks:

- P1: verify A5 state 132 authority, both predecessors accepted, frontend
  clean at commit `a0477d5ae71b24f91826a5ceabf68d90aa66666b`, the starting
  file digest, and the protected 45-entry root change-set digest.
- T1: prove the attributable diff is exactly this one file and exactly the two
  transformations above; no registry/case/control/certificate/fixture or
  product assertion changes.
- V1: from `frontend/`, run exactly `node --check
  test/browser/keyword-intelligence-dashboard.mjs`; require exit zero.
- V2: browser/build/database/enforcement/full-regression execution is
  deferred to I002. Do not alter or manually clean generated evidence paths.
- H1/H2: return the exact diff, ending digest, clean/changed-path inventory,
  command outcome, and residual I002 obligation at `AWAITING_WINDOW_REVIEW`;
  do not start I002 or a successor.

Corrective-subwindow completion checklist:

- [ ] P1 authority, predecessors, clean requester baseline, file digest, and root change-set digest match.
- [ ] T1 exactly the W5-B02 checkbox-row selector and R5-FIN-03 page-size-50/wait mechanics changed in one file.
- [ ] V1 the sole `node --check` command exits zero.
- [ ] V2 no browser/build/database/enforcement/full-regression gate or generated-evidence manual action occurred.
- [ ] H1 exact leaf certificate/diff/digest/command/residual I002 obligation returned.
- [ ] H2 leaf stopped at `AWAITING_WINDOW_REVIEW` without commit, parent communication, or successor work.

CORRECTIVE-SUBWINDOW-READY certificate:

```yaml
certificate: CORRECTIVE-SUBWINDOW-READY
parent_window_id: KI-R5
corrective_subwindow_id: KI-R5-C005
window_agent_identity: KI-R5-WINDOW-AGENT
trigger_evidence: [EV-KI-R5-I001-14, EV-KI-A-070, EV-KI-A-071, CHG-KI-045, CHG-KI-046]
root_cause: W5-B02 counted an intentional zero-result placeholder tr as a keyword row and R5-FIN-03 looked for low-volume row 1 outside the default 25-row page
governing_parent_requirements: [KI-R5-T4, KI-R5-T5, DEC-KI-037]
governing_parent_decisions: [DEC-KI-034, DEC-KI-035, DEC-KI-036, DEC-KI-037]
corrected_prior_subwindows: [KI-R5-S015, KI-R5-C003]
writable_file: frontend/test/browser/keyword-intelligence-dashboard.mjs
starting_file_digest: 1c4cc5ae801f586398cf2e7a30c785f84868001d215fd85bd3d1bc0a920deb01
predecessors: [KI-R5-S015, KI-R5-C003]
invalidated_evidence: [EV-KI-R5-I001-14 V4 browser disposition only]
invalidated_gates: [V4 browser member only]
unresolved_parent_decisions: []
expanded_parent_scope_required: false
section_7_fields_complete: true
single_file_write_set: true
unresolved_execution_choices: []
next_integration_assessment_id: KI-R5-I002
status: READY
```

### 11.2 Later integration assessments

#### KI-R5-I002 — browser-only reassessment after C005

```yaml
integration_assessment_id: KI-R5-I002
parent_window_id: KI-R5
assigned_to: KI-R5-WINDOW-AGENT
predecessors: [KI-R5-C005]
implementation_write_authority: NONE
reused_accepted_evidence: [V1 api certificate, V2 frontend_api certificate, V3 database certificate, V4 lint zero-error result, V4 21-of-21 frontend-test result, V4 successful production-build result]
invalidated_gate_member: V4 browser harness only
single_command: KI_W5_SKIP_BUILD=1 node test/browser/keyword-intelligence-dashboard.mjs
required_outcome: all W5-B01..B08 and W5-R01..R07 plus R5-WIRE-04 and R5-FIN-01..R5-FIN-06 pass; zero required skip, console error, uncaught exception, non-app URL, or CDN; exactly one valid browser certificate with the seven sorted R5 IDs, equal required/registered/executed digests, empty skipped/oracleFailures, and all seven activation witnesses
generated_evidence_authority: the harness invocation alone may overwrite/create only the literal A5-state-132 evidence paths; no manual evidence action
continuation_on_pass: V5, E1, V6, V7 exactly once under unchanged Section 6 instructions
result_oracle: PASS | CORRECTION_REQUIRED | PARENT_BLOCKED
```

I002 does not reopen or relabel failed I001. It reuses only the listed accepted
evidence and executes only the invalidated browser member exactly once with
required localhost/headless-browser approval. A browser failure stops for a
new decision-complete correction; a browser pass resumes V5, E1, V6, and V7
in frozen order. KI-W6 remains prohibited.

### 11.3 Parent adjudications of §0.1 interpretations

**First review (2026-08-20, `EV-KI-R5-S04`): decomposition not approved for
leaf execution; seven executable defects returned. Disposition of all seven:
applied in this revision.**

1. Stale S001 preflight digest (42-entry `3631850a…`) — fixed: §2 and §5 S001
   now record the current 45-entry digest
   `c660d09a800e8a5fd446bd65039f55241d5d7bb4e4c7ef656fe4fc7dcc88417c`, with
   an authoritative dispatch-time recompute note.
2. Nonexistent `../../../email_scraper/...` import — fixed in §0.1 item 6 and
   §5 S013 `read_only_scope` to
   `../../email_scraper/src/api-serializer.js`.
3. `expectedRevision` ".nonnegative() vs stays positive" — fixed: §5 S001
   step 1 now explicitly prescribes changing line 61 from
   `z.number().int().nonnegative()` to `z.number().int().min(1)`.
4. Untyped S009/S010 projection — fixed: §0.1 item 3, §3.1, §5 S009 step 2,
   and §5 S010 step 1 freeze the exact calculated-item guard returning a
   validated non-empty string (throwing
   `"calculated selection item requires a source id"` on null/non-string)
   before `SelectionMutationItem` is constructed.
5. Unallocated S011/S012 finalization contract — fixed: §3.1 freezes the
   expanded prop/state contract; §5 S011 owns the prop type, inert/disabled
   rendering, retry notice/control; §5 S012 owns the exact state machine,
   `handleRetryHandoff`, and succeeded/definitive_failure transitions.
6. Unsatisfiable S016 "no R5 ID outside arrays" lint — fixed: every discovered
   R5 reference must belong to the exact owning registry; no undeclared ID.
7. Contradictory enforcement flow — fixed: §0.1 item 1, §4.2, §3.2, §5 S018,
   §6, and §10 now define six registries, five non-conformance certificates
   captured at V1/V2/V3/V4, S018 leaf checks limited to syntax/static +
   synthetic NC-12, and a single E1 enforcement run inside `KI-R5-I001` that
   executes CONF-01–06, merges all 34 IDs, and emits the final merged
   certificate.

Interpretation adjudication: items 2, 4, 5 accepted; item 1 rejected as
written and revised per finding 7; items 3 and 6 corrected per findings 3/4
and 2. Status remains `AWAITING_PARENT_DECOMPOSITION_REVIEW`; no leaf
assigned; A5 unchanged.

**Second review (2026-08-20, `EV-KI-R5-S05`): seven findings confirmed
resolved; two residual defects returned; both applied.**

1. S018 arithmetic — "29 executed non-conformance IDs" corrected to **28**
   (wire 6 + selection 8 + finalization 8 + export 6) merged with the six
   conformance IDs = 34 (§5 S018).
2. S011 oracle gap — the S011 LOCAL_NOW anchor inspection now verifies the
   disabled logic for all three disabling states (`"handing-off"`,
   `"retry_required"`, `"succeeded"`), and §3.1 plus S011 step 2 clarify that
   `"definitive_failure"` adds no state-based control lock while the existing
   accepted-W5 409 `staleConflict` lock still applies unchanged.

Status remains `AWAITING_PARENT_DECOMPOSITION_REVIEW`; no leaf assigned; no
A5 change.

**Approval (2026-08-20, `EV-KI-R5-S06`):** the parent approved the revised
decomposition (`S1` rev `6ff7830a…`, including the two second-round
corrections). The window agent converted the approval into
`S2.decomposition_status: READY` and staged `KI-R5-S001` /
`ASG-KI-R5-S001` as the first dispatchable leaf. §5 blocks are immutable
from this point; corrections append `KI-R5-C<nnn>` only.

**Corrective authoring (2026-08-20, `EV-KI-A-056` / `CHG-KI-031`, A5 state
117):** the parent authorized reauthoring, but not execution, for the
`EV-KI-R5-S26` substitute-fidelity failure. C002 removes the invalid S014
local model; revised S015 exclusively owns `R5-WIRE-04` plus
`R5-FIN-01`–`06` through actual emitted dashboard state/request capture.
The current certificate topology is four non-conformance registries
(`api`, `database`, `frontend_api`, `browser`) plus conformance — not the
historical six/five topology recorded in the first-review finding above.
S017 bytes, the 34 IDs, all manifest groups, and every digest remain unchanged.
This amended decomposition is `AWAITING_PARENT_DECOMPOSITION_REVIEW`; C002 and
S015 remain unassigned and unexecuted until a new parent approval.

**I001 V2 evidence-protocol adjudication (2026-08-20, `EV-KI-A-063` /
`CHG-KI-038`, A5 state 124):** the original V2 invocation passed the same
three selected frontend files but, under default per-file isolation, did not
surface the nested `frontend_api` `t.diagnostic()` certificate. That result is
retained as diagnostic history only and is not V2 acceptance evidence. In §6,
the V2 command adds exactly `--test-isolation=none` after `--test`; every
selected file, cwd, expected count, registry, case, control, digest,
certificate payload, and outcome remains unchanged. This invalidates only V2
acceptance evidence, authorizes exactly one corrected V2 execution, preserves
the accepted V1 `api` certificate, and permits V3–V7/E1 continuation only
after the corrected command captures exactly one `frontend_api` certificate.

**I001 V3 runner-protocol adjudication (2026-08-20, `EV-KI-A-065` /
`CHG-KI-040`, A5 state 126):** the prior V3 invocation is diagnostic history
only: it preloaded the local environment but its child-only name pattern
excluded the top-level database registry and certificate test, so it executed
zero tests and made no database mutation. In §6, V3 is replaced once by the
consolidated command that preloads `dotenv/config` and selects the top-level
registry, both `R5-FIN-07`/`R5-FIN-08` nested cases, and the `KI-R5 database
execution certificate` test. The helper, isolated-schema requirements, two
R5 case IDs, certificate payload and digests, controls, and every other gate
remain unchanged. This authorizes exactly one corrected V3 execution; V1/V2
remain accepted, unrelated runner-filtered W4 TAP skips are not R5 evidence,
and continuation to V4 requires the complete database certificate.

**I001 V3 durable-capture recovery adjudication (2026-08-20, `EV-KI-A-066` /
`CHG-KI-041`, A5 state 127):** the state-126 network-permitted V3 attempt has
no observable exit, TAP, certificate, or cleanup witness and is neither a pass
nor a product failure. Before one recovery execution, the window agent must
use the unchanged direct-test resolver for the single read-only
`kiw4_handoff_%` residual-schema count and require zero; it may not clean any
schema. Both fixed `/tmp/ki-r5-v3-state127.{tap,exit}` artifacts must be absent
before execution. The §6 V3 wrapper then writes TAP and always records the
Node exit status to those unique paths. Acceptance requires an exact `0` status,
complete non-secret TAP, both R5 child cases, and one complete database
certificate; absent/truncated/partial output stops assessment. This authorizes
one recovery only, preserves V1/V2, and leaves all implementation behavior,
V4–V7, E1, and KI-W6 boundaries unchanged.

**I001 V3 direct-stdout durable-capture adjudication (2026-08-20,
`EV-KI-A-067` / `CHG-KI-042`, A5 state 128):** settled state127 artifacts now
prove exit status zero and a complete 10-test/10-pass TAP result, including
both R5 cases and the certificate test; they remain preserved historical
evidence. The only missing member is the test's direct-stdout database
certificate, which the TAP reporter destination cannot carry. Before the one
final capture execution, repeat the unchanged read-only direct-test resolver
count for `kiw4_handoff_%` and require zero, and require the fixed
`/tmp/ki-r5-v3-state128.combined` destination to be absent. In §6, V3 is
replaced only by the shell-redirection command that pre-opens that combined
file for TAP, direct stdout, and stderr; no wrapper, reporter destination,
pipe, `tee`, sidecar, helper, selected pattern, case, registry, certificate
formula, or behavior oracle changes. Acceptance requires exactly one complete,
non-secret TAP result with 10 tests/10 pass/zero fail-cancel-skip-todo, both
R5 cases, and the certificate test, plus exactly one parseable `database`
certificate with the frozen two-ID required=registered=executed=
activationWitnesses sets, empty skipped/oracleFailures, and equal digests.
On pass V3 is accepted and I001 resumes once at V4; on failure no further V3
run is authorized. V1/V2 remain accepted, and V4–V7, E1, and KI-W6 boundaries
remain unchanged.

**I001 V3 format-neutral evidence adjudication (2026-08-20,
`EV-KI-A-068` / `CHG-KI-043`, A5 state 129):** V3 is accepted without another
database command. The preserved state127 TAP artifact (SHA-256
`8018558b68a529967035525304bff998cd4ae1676596ffb9d394389359125775`) supplies
the canonical 10-test/10-pass/zero-total TAP result and the preserved state127
exit artifact (SHA-256
`9a271f2a916b0b6ee6cecb2426f0b3206ef074578be55d9bc94f6f3fe3ab86aa`) supplies
exit zero. The preserved state128 combined artifact (1,064 bytes; SHA-256
`ead5e611dcc33e35d11a769c350d0c394b471d92eb4642855b4c32fed9a3979d`) is a
complete Node spec-reporter summary with the same semantic totals and exactly
one valid `database` certificate. That certificate is the sole accepted V3
certificate for E1: registry `database`; required = registered = executed =
activationWitnesses = `R5-FIN-07`, `R5-FIN-08`; empty skipped/oracleFailures;
and equal digests
`0cc6cab7b86d187e8db4edcd44d68a6752a2375e6bdc7eaeba7d051e470a09b5`.
Reporter typography is format-neutral evidence transport, not a behavioral
oracle. All three artifacts remain byte-identical; no further V3 command,
database preflight/query/mutation, or evidence reconstruction is authorized.
I001 resumes directly at unchanged V4; V1 and V2 remain accepted.

**I001 V4 sandbox-recovery adjudication (2026-08-20, `EV-KI-A-069` /
`CHG-KI-044`, A5 state 130):** the completed V4 lint result (zero errors) and
completed 21-of-21 frontend test result (zero fail/cancel/skip/todo) remain
accepted and must not rerun. Only the prior unobservable `next build` portion
is environmentally invalidated. From `frontend/`, run exactly `npm run build`
once with required sandbox approval and wait for final exit; require exit zero,
normal completed production-build output, and a nonempty `.next/BUILD_ID`.
Do not clean or edit `.next`. Only then run exactly once, with required
localhost/headless-browser approval, `KI_W5_SKIP_BUILD=1 node
test/browser/keyword-intelligence-dashboard.mjs`; require every frozen V4
browser oracle and exactly one valid seven-ID `browser` certificate. On V4
pass, continue directly to V5. A nonzero/missing-build-marker result stops;
neither build nor browser harness may otherwise repeat.

**KI-R5-V4-A1 (2026-08-20, `EV-KI-A-072` / `CHG-KI-047`, A5 state 133):**
the existing I002 browser execution is V4 **PASS** without a rerun. This
classification supersedes only V4's unqualified zero-console phrase: exactly
one Chrome diagnostic, `Failed to load resource: the server responded with a
status of 401 (Unauthorized)`, is permitted only when the required
browser-origin `R5-WIRE-04` activation witness passed and every other browser
oracle passed. It does not permit an application-generated assertion or error,
an unexpected/different/additional console entry, uncaught exception, skip,
oracle failure, non-app/CDN URL, invalid certificate, 415 response, or missing
WIRE-04 witness. The existing seven-ID `browser` certificate is the sole
browser input to E1. V5, E1, V6, and V7 remain exactly-once gates in that
order; no browser/build rerun, source/test correction, KI-W6 work, provider,
AWS, database, production, commit, or push action is authorized.

**KI-R5-V5-A1 (2026-08-20, `EV-KI-A-073` / `CHG-KI-048`, A5 state 134):**
the first V5 `npm test` invocation is environmentally invalidated: its execution
channel closed without a final exit status or complete Node aggregate summary,
and subsequent read-only checks found no matching process, repository delta, or
external action. From `email_scraper/`, execute exactly `npm test` once with
required escalated sandbox permission in one persistent execution session; poll
that same session through final exit and retain the complete output. No filter,
environment override, reporter, wrapper, redirect, pipe, or changed command is
permitted. Accept only observable exit zero, a complete aggregate summary with
zero failures, and only the previously guarded integration skips. A partial
result, missing totals or exit, truncated final result, or nonzero exit stops
recovery and authorizes no further V5 rerun. On pass, run exactly `npm run
check:secrets` once; then execute E1, V6, and V7 once each in order.

**KI-R5-SBX-A1 (2026-08-20, `EV-KI-A-074` / `CHG-KI-049`, A5 state 135):**
sandbox escalation is execution-environment permission, not new task authority.
Any otherwise authorized local KI-R5 verification command may begin with the
required escalated permission. If a restricted attempt is proven invalidated
solely by sandbox denial or execution-channel loss, with no matching process,
workspace mutation, external action, or acceptable result remaining, the window
agent may run that identical already-authorized command once under escalation
and record both attempts. Escalation cannot alter the command, environment,
selection, oracle, write scope, or run budget, and never authorizes provider,
AWS, production, destructive, commit, push, or successor work.

## 12. Self-falsification record (standard Section 14)

Demonstrated against this document's rules (`EV-KI-R5-S03`):

1. Two writable files in one sub-window — every §5 block YAML lists exactly
   one `writable_file`; a second path fails the block lint and the leaf V2
   changed-set check.
2. Directory/wildcard writable target — all 18 paths are canonical
   workspace-relative file paths (§2 rules); no glob/directory appears.
3. Command creating an unplanned second workspace file — §5 checks are
   parse/check/focused-test only; the per-leaf changed-set comparison fails
   any second-file delta; certificates/temp output stay outside the workspace.
4. Source + test file assigned together — S001/S005, S004/S006, S010/S014 etc.
   are separate sequential blocks.
5. Required parent file absent — §2/§4 prove 18/18 allocation with digest
   equality; removing any file breaks SW-D03/D04 and the I001 I2 check.
6. Two initial sub-windows owning the same file — S001–S018 ↔ F-001–F-018 is a
   bijection; a duplicate owner breaks the §8.2 lint.
7. Dependent file beginning before its interface is frozen — §3.1 freezes all
   cross-file interfaces before S002/S009/S012/S013/S018; edges in §3 name the
   consumed interface.
8. Intermediate state with unexplained test failure — §3.2 lists every
   permitted temporary failure with its resolver; anything else stops the
   sequence.
9. Subagent starting its successor — `may_start_successor: false`,
   `successor_reserved_for: WINDOW-AGENT`, common prohibitions, S2 transition
   only by the window agent.
10. Subagent → parent communication — prohibited in every block and §9; the
    leaf certificate reports only to the window agent.
11. Window agent repairing implementation during review — §1/§7 forbid it;
    every fix is a corrective leaf.
12. Integration failure without a diagnosed one-file correction — §7 requires
    the Section 9.5 record and minimum ordered corrections.
13. Correction silently rewriting a completed sub-window — §7/§11 append-only
    rule; new IDs and baseline digests only.
14. Coverage omission/skip/duplicate/filter/bypass — CONF-02 equality oracles
    plus NC-12 mutation modes make each fail acceptance.
15. Oracle weakened to accommodate behavior — NC-10/NC-12
    (`R5_ORACLE_WEAKENED`) and the immutable A4 oracles forbid it.
16. Substitute proving more parity than supported — CONF-05 boundaries + NC-11
    (`R5_SUBSTITUTE_FIDELITY_DIVERGED`, `R5_REAL_NEXT_ROUTE_WITNESS_MISSING`).
17. Costly gate repeated without scheduling/invalidation rule — §6 single-run
    discipline with invalidation-only reruns; A5 prohibits repeated
    successful stateful/build gates.
18. Correction with reused dependent evidence — §7 invalidation rule requires
    dependency proof for any reuse.
19. Assembled changed set ≠ planned set or planned set exceeding parent scope
    — I001 I2 and CONF-04 compare against the exact 18-path digest and forbid
    any extra path.
20. Window agent claiming parent acceptance or starting the next parent window
    — §9.3/§10 stop at `READY_FOR_PARENT_REVIEW`; A5 CAS and KI-W6 assignment
    are parent-only.

---

**End of `S1`.** Decomposition status: `AWAITING_PARENT_DECOMPOSITION_REVIEW`.
No leaf is assigned. Implementation begins only after parent approval and the
window agent's `S2` transition to `READY`.

**KI-R5-E1-A1 (2026-08-20, `EV-KI-A-076` / `CHG-KI-051`, A5 state 137):**
the prior E1 process is invalid only as certificate transport: it exited before
registering a conformance test because its environment value was malformed
JSON. V1–V5 and their four runtime certificate objects remain accepted and
must not rerun or change. In registry order `api`, `frontend_api`, `database`,
`browser`, serialize those accepted objects with sorted member arrays, equal
required/registered/executed/activationWitnesses arrays, empty skipped and
oracleFailures arrays, and their accepted per-registry digests. The resulting
JSON array must be exactly 2,847 bytes with SHA-256
`63eedf904a3eb40729e5dc393085341ca7bf97105bc5a920ddedb106a4d70412`.
Before E1, perform one read-only JSON parse preflight that verifies those
registry names and exact accepted member/failure sets plus the pinned byte
count and digest, without importing or executing the enforcement test. On a
passing preflight, run exactly once from `email_scraper/`:
`KI_R5_EXECUTED_CERTIFICATES='<that canonical JSON array>' node --test
--test-isolation=none test/keyword-intelligence-r5-enforcement.test.js` with
required sandbox escalation. Only observable exit zero, six passing
`R5-CONF-01`–`06` cases, zero fail/skip/todo, and exactly one valid merged
34-ID certificate permit V6 then V7 once each. Any observable E1 failure
stops I002 without another rerun. KI-W6 remains prohibited.

## 13. State-138 standards delta and corrective decomposition

**Standards delta audit.** The completed leaves and accepted V1–V5 retain the
frozen parent/sub-window revisions
`3b7a4fd25156e1adfbc92abb835c5f82a0d18c686b1c1150feb202f2d944d2ac` /
`1766f9107ce7d315877b75d4b0ea2b5521dff1c321e12f890b03787d66196ded`.
This new corrective decomposition pins the current revisions
`cda352017e75c0d11f6797d9fbe108b4365508cd38b0e92365cfb523ede32848` /
`84e7590e74589f308c70dc9b0b67f7e9da395fafb1e5786202ecd1ca15be56e9` as
required by both standards' §0.4. The newly applicable requirements are the
inherited authorized-local sandbox policy and its identical-recovery boundary:
they add no implementation scope, certificate-member change, evidence wildcard,
or automatic recovery for an observable assertion failure. `PA-008`, `PS-021`,
and `PR-013` are recorded in A4; `EV-KI-A-074`–`077` and
`EV-KI-R5-I002-03`–`06` mechanically demonstrate the distinction.

- [x] `SW-A07` The inherited execution-environment policy permits required
  sandbox escalation only for already-authorized local actions, without
  expanding provider, AWS, production, destructive, commit, or successor
  authority. Evidence: `KI-R5-SBX-A1`; `EV-KI-A-074`; A5-138.
- [x] `SW-V11` Local gates distinguish proven sandbox/channel invalidation from
  observable failure and allow exactly one identical escalated recovery only in
  the former class. Evidence: `EV-KI-R5-I002-03`–`06`; `PS-021`; A5-138.
- [x] `SW-R11` A sandbox-denial simulation is recoverable only after its
  required no-process/no-mutation proof; changed command, observable assertion
  failure, surviving process, workspace/external mutation, or external action
  is rejected. Evidence: state-137 malformed-input stop and state-138 CONF-04
  correction; `PR-013`; A5-138.

The 44 previously checked authoring items remain supported by their frozen
evidence, and the three checks above close the only newly added standard
items: current-standard readiness is therefore 47/47 checked and 0 unchecked.

#### KI-R5-C006 — classify exact browser-harness runtime evidence in CONF-04

```yaml
subwindow_id: KI-R5-C006
type: CORRECTION
parent_window_id: KI-R5
parent_assignment_id: ASG-KI-R5-WA-01
assigned_agent: UNASSIGNED
predecessors: [KI-R5-S018, KI-R5-I002]
successor_reserved_for: KI-R5-WINDOW-AGENT
writable_file: email_scraper/test/keyword-intelligence-r5-enforcement.test.js
file_operation: MODIFY
starting_file_digest: 465b3d9fd5b43d2b5f34573a0ab392c58205ff4fce2b7f5b2b86abbdfed17bf4
starting_repository_change_set_digest: c660d09a800e8a5fd446bd65039f55241d5d7bb4e4c7ef656fe4fc7dcc88417c
read_only_scope: [KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md::KI-R5-CONF04-A1..A3, KEYWORD_INTELLIGENCE_EXECUTION_EVIDENCE.md::EV-KI-A-077, KEYWORD_INTELLIGENCE_SPECIFICATION_CHANGELOG.md::CHG-KI-052, email_scraper/test/fixtures/keyword-intelligence/ki-r5-enforcement-manifest-v1.json, git metadata of email_scraper and frontend]
authorized_actions: [implement only KI-R5-CONF04-A2 and KI-R5-CONF04-A3, validate exact status classification with the two prescribed injected negative controls, run only the specified local syntax/pure-helper checks]
prohibited_actions: [edit any other file, alter DELEGABLE_FILE_SET or its 18 members/digest, change any R5 ID/registry/certificate/digest/oracle other than CONF-04 classification, wildcard/directory/prefix evidence exemption, execute E1/V1-V7/browser/build/database/full regression, manual review-evidence action, provider/AWS/production/database operation, commit/push, successor work, parent communication, KI-W6/W7]
may_start_successor: false
```

**Mechanical trace:** `KI-R5-CONF04-A1` diagnoses `EV-KI-R5-I002-06`:
CONF-04 rejects the A5-authorized browser output
`frontend/review-evidence/keyword-intelligence/KI-W5/W5-R05-responsive.png`
because it classifies every nested status path as an implementation edit.
`KI-R5-CONF04-A2` and `A3`, `DEC-KI-037`, `EV-KI-A-077`, and `CHG-KI-052`
determine the remedy. It corrects S018's failed enforcement helper and
invalidates only I002's E1/CONF-04 disposition; V1–V5 remain accepted.

**Exact transformation:** immediately before `lintFinalWorktreeScope`, add
literal `ALLOWED_REVIEW_EVIDENCE_CHANGES` as exactly these five `{ path,
untracked }` pairs: `{path:"frontend/review-evidence/keyword-intelligence/KI-W5/W5-R05-responsive.png",untracked:false}`,
`{path:"frontend/review-evidence/keyword-intelligence/KI-W5/artifact-index.json",untracked:false}`,
`{path:"frontend/review-evidence/keyword-intelligence/KI-W5/browser-checks.json",untracked:false}`,
`{path:"frontend/review-evidence/keyword-intelligence/KI-W5/browser-server.log",untracked:false}`,
and `{path:"frontend/review-evidence/keyword-intelligence/KI-W5/R5-FIN-03-unsaved.png",untracked:true}`.
Add pure exported `validateFinalWorktreeChanges(changes)`: for each observed
entry, an exact allowlist pair passes; an allowlisted path at the wrong
`untracked` value throws `R5_REVIEW_EVIDENCE_STATUS_MISMATCH`; an observed path
under `frontend/review-evidence/keyword-intelligence/KI-W5/` that is not one
of the five literals throws `R5_UNEXPECTED_REVIEW_EVIDENCE_PATH`; every other
entry retains the existing exact 18-path membership, forbidden-token, and
create-versus-modification checks. Absence of an allowlisted path passes.
Change the helper signature to `lintFinalWorktreeScope(additionalChanges = [])`
and pass real nested status entries plus `additionalChanges` through that pure
validator. Preserve final expected-file existence and 18-path digest checks.
No broad path match, directory exception, or changed implementation boundary
is allowed.

**Exact checks (LOCAL_NOW):** from `email_scraper/`, first run exactly
`node --check test/keyword-intelligence-r5-enforcement.test.js` and require
exit 0. Then run exactly this one pure-helper command:

```sh
node --input-type=module -e '
import assert from "node:assert/strict";
delete process.env.KI_R5_EXECUTED_CERTIFICATES;
const { lintFinalWorktreeScope, validateFinalWorktreeChanges } = await import("./test/keyword-intelligence-r5-enforcement.test.js");
assert.equal(typeof validateFinalWorktreeChanges, "function");
assert.equal(lintFinalWorktreeScope(), true);
assert.throws(
  () => lintFinalWorktreeScope([{ path: "frontend/review-evidence/keyword-intelligence/KI-W5/UNEXPECTED.png", untracked: false }]),
  (error) => error?.message === "R5_UNEXPECTED_REVIEW_EVIDENCE_PATH"
);
assert.throws(
  () => lintFinalWorktreeScope([{ path: "frontend/review-evidence/keyword-intelligence/KI-W5/W5-R05-responsive.png", untracked: true }]),
  (error) => error?.message === "R5_REVIEW_EVIDENCE_STATUS_MISMATCH"
);
assert.equal(lintFinalWorktreeScope(), true);
'
```

The command explicitly removes the certificate environment before importing
the module, so it registers and executes no CONF test. Its four local oracles
are current-status pass, unexpected-path fail with the exact first error,
wrong-status fail with the exact second error, and fresh current-status pass.
Actual `R5-CONF-04` / `R5-NC-12` execution remains deferred to I003 E1. The
attributable changed-file set is exactly the writable file.

- [ ] P1 A5-138, both current standard pins, C006 identity, predecessors,
  baseline file/root digests, and protected five evidence paths match.
- [ ] P2 Nested status matches the protected dirty baseline; no sixth evidence
  path or wrong status is accepted.
- [ ] T1 Only the literal allowlist and pure CONF-04 classification mechanics
  above change in the one writable file.
- [ ] V1 The syntax and pure-helper current/negative-control checks pass with
  the exact two error strings.
- [ ] V2 The attributable changed-file set is exactly the enforcement test.
- [ ] V3 Static comparison proves the 34-ID registry, accepted certificate
  sets and digests unchanged; actual R5-CONF-04/control execution remains
  deferred to I003 E1.
- [ ] H1 Return diff, ending digest, command output, activation witnesses, and
  I003 deferred-gate obligations.
- [ ] H2 Confirm no prohibited action, second-file edit, successor work,
  external mutation, or parent communication.
- [ ] H3 Stop at AWAITING_WINDOW_REVIEW.

```yaml
certificate: CORRECTIVE-SUBWINDOW-READY
parent_window_id: KI-R5
corrective_subwindow_id: KI-R5-C006
window_agent_identity: KI-R5-WINDOW-AGENT
trigger_evidence: [EV-KI-R5-I002-06, EV-KI-A-077, CHG-KI-052]
root_cause: CONF-04 applies the 18-path implementation set before classifying five exact A5-authorized browser-harness evidence paths and statuses.
governing_parent_requirements: [KI-R5-CONF04-A1, KI-R5-CONF04-A2, KI-R5-CONF04-A3, PA-008, PS-021, PR-013]
governing_parent_decisions: [DEC-KI-037]
corrected_prior_subwindows: [KI-R5-S018]
writable_file: email_scraper/test/keyword-intelligence-r5-enforcement.test.js
starting_file_digest: 465b3d9fd5b43d2b5f34573a0ab392c58205ff4fce2b7f5b2b86abbdfed17bf4
predecessors: [KI-R5-S018, KI-R5-I002]
invalidated_evidence: [EV-KI-R5-I002-06 E1 acceptance and CONF-04 disposition only]
invalidated_gates: [E1]
pending_unexecuted_gates: [V6, V7]
unresolved_parent_decisions: []
expanded_parent_scope_required: false
section_7_fields_complete: true
single_file_write_set: true
unresolved_execution_choices: []
next_integration_assessment_id: KI-R5-I003
status: READY
```

#### KI-R5-I003 — corrected enforcement and final unexecuted gate assessment

```yaml
integration_assessment_id: KI-R5-I003
parent_window_id: KI-R5
assigned_to: KI-R5-WINDOW-AGENT
predecessors: [KI-R5-C006]
implementation_write_authority: NONE
reused_accepted_evidence: [V1 api certificate, V2 frontend_api certificate, V3 database certificate, V4 lint/frontend-test/build/browser results, V5 npm-test and secrets results]
invalidated_gates: [I002 E1/CONF-04 only]
gates_in_order: [corrected E1 once, V6 once, V7 once]
result_oracle: PASS | CORRECTION_REQUIRED | PARENT_BLOCKED
```

I003 first proves C006 was independently accepted and preserves the four
canonical accepted runtime certificate objects in registry order `api`,
`frontend_api`, `database`, `browser` (2,847 bytes; SHA-256
`63eedf904a3eb40729e5dc393085341ca7bf97105bc5a920ddedb106a4d70412`).
V1–V4 reuse is branch-disjoint because C006 changes only CONF-04 and none of
their commands import or execute the enforcement test. V5's `npm test` does
discover and import the enforcement test, but it does not set
`KI_R5_EXECUTED_CERTIFICATES`; the module-level guard therefore registers zero
CONF cases and never invokes the changed classifier. C006's exact syntax and
pure-helper import checks prove that the final module still parses and loads
with that environment absent. Every other V5 test path is byte-identical.
`npm run check:secrets` is reused only after the C006 diff is inspected and
shown to contain exactly the five public review-evidence paths, two public
error identifiers, status booleans, and helper/control mechanics prescribed
above, with no credential-shaped assignment or secret-bearing value. This
complete dependency proof is recorded in S3 before E1; V5 must not rerun.

E1 runs once with the canonical four-certificate JSON and required sandbox
escalation; it requires exit 0, `R5-CONF-01`–`06` six pass/zero fail-skip-todo,
all five registry sets equal their required sets with accepted digests, and one
merged 34-ID certificate with global digest
`507186e7489a3f9eec18eb5de78692dbc55a8d1d2d106544aa4295a98ac9be60`.
V6 then recomputes all five group digests and the global digest from the four
certificates and merged certificate; it requires required=registered=executed
34-ID equality, no skipped/duplicate/unexpected/unactivated/oracle-failure ID,
and the unchanged NC-01–NC-12 falsification record. V7 then verifies case
evidence for valid 0/1/100/200 selections, 201 rejection, 143641-byte maximum,
19900 comparison bound, one CAS, one Run under concurrency, CSV textual
safety/numeric stability, owner privacy, and the exact 18-path/symbol diff
plus only the five literal evidence/status exceptions. Any observable failure
stops; no E1/V6/V7 rerun is automatic. KI-W6 remains prohibited.

**KI-R5-C006 approval and dispatch (2026-08-20, `EV-KI-A-078` /
`CHG-KI-053`, A5 state 139):** the parent approved revision
`950a0cbb91a373c8075b1e3e5f1c2aee8e5b036871e7c751566e5d88309e4f26`.
The window agent dispatches only `KI-R5-C006` to `KI-R5-C006-LEAF` under
`ASG-KI-R5-C006`; its writable file, baseline, literal commands, two negative
controls, V5 reuse proof, and I003 E1-only invalidation remain exactly as
above. The leaf must stop at `AWAITING_WINDOW_REVIEW`; I003 cannot start until
independent C006 acceptance. KI-W6 remains prohibited.

## 14. Requester-authorized direct C007/I004 corrective decomposition

C006 is rejected by `EV-KI-R5-C006-05`: its new
`validateFinalWorktreeChanges()` changed the two implementation-status paths
from a required status assertion to an unconditional `continue`. The prior
prose required preservation, but its local controls did not exercise that
invariant. C007 restores status enforcement and makes its omission unpassable.

#### KI-R5-C007 — restore implementation-create status enforcement

```yaml
subwindow_id: KI-R5-C007
type: CORRECTION
parent_window_id: KI-R5
parent_assignment_id: ASG-KI-R5-WA-01
assigned_agent: UNASSIGNED
predecessors: [KI-R5-C006]
successor_reserved_for: KI-R5-WINDOW-AGENT
writable_file: email_scraper/test/keyword-intelligence-r5-enforcement.test.js
file_operation: MODIFY
starting_file_digest: f9fcb58e47b179f0a120f8c1aaf9bf17836dcdf1bc764de00643788f2036aee3
starting_repository_change_set_digest: c660d09a800e8a5fd446bd65039f55241d5d7bb4e4c7ef656fe4fc7dcc88417c
authorized_actions: [replace only the createPaths unconditional continue with the literal tracked-modification assertion plus continue, run only the two exact LOCAL_NOW commands below]
prohibited_actions: [edit any other file or hunk, alter the five review-evidence pairs or their checks, alter DELEGABLE_FILE_SET createPaths forbiddenTokens IDs registries certificates digests or non-CONF04 behavior, wildcard evidence exception, E1 V1-V7 browser build database full regression, manual review-evidence action, provider AWS production database operation, commit push successor or KI-W6 work, parent communication]
may_start_successor: false
```

**Exact transformation:** inside `validateFinalWorktreeChanges(changes)`,
replace exactly:

```js
if (createPaths.includes(change.path)) {
  continue;
}
```

with exactly:

```js
if (createPaths.includes(change.path)) {
  assert.equal(change.untracked, false, `${change.path} present as a modification, not an untracked create`);
  continue;
}
```

No other line changes. The two paths governed by this branch remain exactly:

- `email_scraper/test/fixtures/keyword-intelligence/ki-r5-enforcement-manifest-v1.json`
- `email_scraper/test/keyword-intelligence-r5-enforcement.test.js`

**Exact checks (LOCAL_NOW):** from `email_scraper/`, first run exactly
`node --check test/keyword-intelligence-r5-enforcement.test.js` and require
exit 0. Then run exactly:

```sh
node --input-type=module -e '
import assert from "node:assert/strict";
delete process.env.KI_R5_EXECUTED_CERTIFICATES;
const { lintFinalWorktreeScope, validateFinalWorktreeChanges } = await import("./test/keyword-intelligence-r5-enforcement.test.js");
const createPaths = [
  "email_scraper/test/fixtures/keyword-intelligence/ki-r5-enforcement-manifest-v1.json",
  "email_scraper/test/keyword-intelligence-r5-enforcement.test.js",
];
assert.equal(lintFinalWorktreeScope(), true);
assert.throws(
  () => lintFinalWorktreeScope([{ path: "frontend/review-evidence/keyword-intelligence/KI-W5/UNEXPECTED.png", untracked: false }]),
  (error) => error?.message === "R5_UNEXPECTED_REVIEW_EVIDENCE_PATH"
);
assert.throws(
  () => lintFinalWorktreeScope([{ path: "frontend/review-evidence/keyword-intelligence/KI-W5/W5-R05-responsive.png", untracked: true }]),
  (error) => error?.message === "R5_REVIEW_EVIDENCE_STATUS_MISMATCH"
);
for (const path of createPaths) {
  assert.equal(validateFinalWorktreeChanges([{ path, untracked: false }]), true);
  assert.throws(
    () => validateFinalWorktreeChanges([{ path, untracked: true }]),
    (error) => error?.message?.startsWith(`${path} present as a modification, not an untracked create`)
  );
  assert.equal(validateFinalWorktreeChanges([{ path, untracked: false }]), true);
}
assert.equal(lintFinalWorktreeScope(), true);
'
```

The command removes the certificate environment before import, so no CONF case
registers. It proves unchanged current status, both review-evidence controls,
and pass→wrong-status-fail→fresh-pass for each current tracked implementation
path. Actual CONF-04/NC-12 execution remains deferred to I004 E1.

- [ ] P1 Verify A5 authority, C007 identity, predecessor, one writable file,
  starting file digest and protected root/evidence state.
- [ ] T1 Verify the attributable diff is exactly the one literal replacement.
- [ ] V1 Require both exact local commands to exit zero and every prescribed
  local control phase to activate with its exact message.
- [ ] V2 Verify the five review-evidence pairs, both create-path literals,
  18-path digest, IDs, registries, certificates and all other oracles unchanged.
- [ ] H1 Return exact diff, ending digest, command outputs and I004 obligation.
- [ ] H2 Confirm no second-file, external, commit, successor or KI-W6 action.
- [ ] H3 Stop at `AWAITING_WINDOW_REVIEW`.

```yaml
certificate: CORRECTIVE-SUBWINDOW-READY
parent_window_id: KI-R5
corrective_subwindow_id: KI-R5-C007
window_agent_identity: KI-R5-WINDOW-AGENT
trigger_evidence: [EV-KI-R5-C006-05]
root_cause: C006 replaced the two committed implementation paths' status assertion with an unconditional continue, and its local controls omitted that invariant.
governing_parent_requirements: [KI-R5-CONF04-A2, KI-R5-CONF04-A3]
governing_parent_decisions: [DEC-KI-037]
corrected_prior_subwindows: [KI-R5-C006]
writable_file: email_scraper/test/keyword-intelligence-r5-enforcement.test.js
starting_file_digest: f9fcb58e47b179f0a120f8c1aaf9bf17836dcdf1bc764de00643788f2036aee3
predecessors: [KI-R5-C006]
invalidated_evidence: [EV-KI-R5-C006-05 supersedes C006 local-pass sufficiency]
invalidated_gates: [E1]
pending_unexecuted_gates: [V6, V7]
unresolved_parent_decisions: []
expanded_parent_scope_required: false
section_7_fields_complete: true
single_file_write_set: true
unresolved_execution_choices: []
next_integration_assessment_id: KI-R5-I004
status: READY
```

#### KI-R5-I004 — corrected enforcement and remaining final gates

```yaml
integration_assessment_id: KI-R5-I004
parent_window_id: KI-R5
assigned_to: KI-R5-WINDOW-AGENT
predecessors: [KI-R5-C007]
implementation_write_authority: NONE
reused_accepted_evidence: [V1 api certificate, V2 frontend_api certificate, V3 database certificate, V4 lint frontend-test build browser results, V5 npm-test and secrets results]
superseded_unstarted_assessment: KI-R5-I003
invalidated_gates: [E1]
pending_unexecuted_gates: [V6, V7]
gates_in_order: [corrected E1 once, V6 once, V7 once]
result_oracle: PASS | CORRECTION_REQUIRED | PARENT_BLOCKED
```

I004 begins only after independent C007 acceptance. It records the same V1–V5
reuse proof as I003 against the final C007 diff: V1–V4 never import enforcement;
V5 `npm test` imports it with the certificate environment absent, C007's syntax
and pure import checks prove module loading, zero CONF cases register, and no
changed classifier runs; secret-scan reuse requires the exact diff to contain
no credential-shaped assignment or secret-bearing value. It then uses the
already validated 2,847-byte canonical four-certificate transport to execute
E1 exactly once. Acceptance requires six CONF passes, zero fail/skip/todo and
the exact merged 34-ID digest
`507186e7489a3f9eec18eb5de78692dbc55a8d1d2d106544aa4295a98ac9be60`.
Only on pass does it execute the unchanged V6 once and V7 once. Any observable
failure stops; KI-W6 remains prohibited.

**KI-R5-C007 approval and dispatch (2026-08-20, `EV-KI-A-079` /
`CHG-KI-054`, A5 state 140):** the parent approved S1 revision
`9b78ce7945231cb031a78a6c4fec6ac6d7047d4faae21a5e110c2eb7b4a5f597`.
The window agent dispatches only `KI-R5-C007` to `KI-R5-C007-LEAF` under
`ASG-KI-R5-C007`. Its sole writable file, starting digest, literal one-hunk
replacement, and two LOCAL_NOW commands remain exactly as specified above.
The leaf must stop at `AWAITING_WINDOW_REVIEW`; I004 cannot start until
independent C007 acceptance. V1–V5 remain accepted, E1 remains invalidated,
V6/V7 remain pending, and KI-W6 remains prohibited.

**Requester-directed C007 status correction (2026-08-20):** the two paths in
`createPaths` were committed by S017/S018/C006 before C007 began. A current
C007 edit therefore appears in nested-repository status as `untracked: false`.
The requester directed this local documentation correction without a parent
state transition: C007's literal assertion and local control now require a
tracked modification and reject an untracked status. This is a local override
of the A5-state-140 C007 mechanics; A5 is intentionally unchanged. I004 may
start only after the corrected C007 helper and independent review pass. The
negative-control matcher uses `startsWith` because Node appends its
`true !== false` comparison detail to `AssertionError.message`.

**Requester-directed C007 verification (2026-08-20):** the resulting one-hunk
diff has enforcement-test SHA-256
`f9a593fbb50ba4bc7d603e2c5fafe3129356cb758d022a5b83cef05f0ed3b954`.
`node --check`, the revised exact pure-helper command, and
`node --test test/keyword-intelligence-r5-enforcement.test.js` all pass. The
five review-evidence controls remain unchanged and the revised two-path
controls pass for `untracked: false` and reject `untracked: true`. At the
requester's direction, C007 is locally accepted for the purpose of beginning
I004; this is not a parent-A5 acceptance or a claim that A5 state 140 changed.
