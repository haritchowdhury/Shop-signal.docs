# KI-W4 Sub-Window Evidence (`S3`)

Append-only. Every entry identifies actor, revisions, commands, decisive
results, coverage accounting, external mutations, and disposition. This file
cannot amend a task, decision, or authority boundary.

---

## `EV-KI-W4-S01` — Entry-gate verification, delta audit, and starting inventory

- **Timestamp:** 2026-08-18T19:07:46+05:30
- **Parent window / assignment / sub-window:** `KI-W4` / `ASG-KI-W4-WA-01` / (decomposition)
- **Actor/role:** `KI-W4-WINDOW-AGENT` (window agent)
- **Frozen revisions at inspection:** parent standard
  `3b7a4fd25156e1adfbc92abb835c5f82a0d18c686b1c1150feb202f2d944d2ac`;
  sub-window standard
  `1766f9107ce7d315877b75d4b0ea2b5521dff1c321e12f890b03787d66196ded`; A1
  `8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c`; A3
  observed `c2dc635e5aa58f88c1ec465154663d314af68570fd4cbfdfca7b51c393c6f70f`
  (A5 pin `5c42924c8ea6ad1ca43a00feff2b636d83bcd029b7b8a4eeb6777ac60a7f5ec6`
  — stale); A4 observed
  `40f705a423da88b952af4e529566b5a5374d4c7c1d7a0a589642d5906f0744ee` (A5 pin
  `8dce27da58ace35c605ee1f9d0b4ddc8a1e9358a282ec5bf8d7b461729eb999b` —
  stale).
- **§1 Assignment provenance:** requester performed the A5 CAS to state 100
  on 2026-08-18 creating `ASG-KI-W4-WA-01` for `KI-W4-WINDOW-AGENT` with
  `authorized_windows: [KI-W4]`, the three-artifact write scope, and the
  delegation action list recorded in the S1 §1 prohibitions copy. No
  requester exception or waiver applies.
- **§2 Delta audit (sub-window standard §0.4):** A5 state 100 pins A3/A4 at
  pre-`CHG-KI-016` byte copies. `CHG-KI-016`
  (`KEYWORD_INTELLIGENCE_SPECIFICATION_CHANGELOG.md`, 2026-08-18T18:16:14+05:30)
  records the W4 reauthoring to `KI-DL-10`/`KI-CL-12`/`KI-TR-10`; the
  observed A3 contains `DEC-KI-033` complete (lines 1281–1565) and the
  observed A4 contains the complete `KI-W4` window (lines 1786–2214) with
  task blocks `KI-W4-T1`–`T4`, gates `KI-W4-V1`–`V4`, the literal 34-case
  matrix, and controls `W4-NC01`–`NC18`. No contradictory authority found;
  the decomposition binds to the observed revisions. Residual parent action:
  refresh the A5 A3/A4 pins at the next A5 CAS. Both `KEYWORD_INTELLIGENCE_*`
  coordination documents are untracked in the root repository, so no
  byte-level git delta is recoverable; the audit rests on the changelog,
  the revision markers, and content presence.
- **§3 Boundary copy:** S1 §1 reproduces the A5 state 100 write/action/
  prohibition scope without expansion.
- **§4 Commands and decisive results:**
  - `git -C email_scraper rev-parse HEAD` →
    `d98ad53c02d8d8205d614043436164d85b84c6ce`; `git -C email_scraper status --porcelain`
    → empty. Matches `KI-W4-P2`.
  - `git -C frontend rev-parse HEAD` →
    `0dfa1acac50fac3a86d02ec674c6d2bab645832d`; status clean; read-only.
  - `sha256sum` over the six existing planned files + `ABSENT` markers for
    the four new paths → the digests recorded in S1 §2.
  - Ten planned paths, sorted, each + LF, sha256 →
    `fe48d14ebec1dffa058cf91cfa9ec10982d4ceaa4c63e0cb9280cabf39a4a59b` —
    byte-equal to the A4 `KI-W4` header `required_initial_file_set_digest`.
    Set-equality proof for `SW-D03`.
  - Root `git status --porcelain` → 33 owner-controlled relocation paths;
    per-LF set digest
    `b33384c5ceb700902be88af820cbd0998699dbbdd2970e0d571c649107479ca5`;
    state preserved unmodified.
  - Grep over the six existing files for every new W4 symbol
    (`classifyKeywordForSelection`, `serializeKeywordResearch`,
    `serializeSelectionItem`, `getOwnedApiView`, `RunHandoffAbort`,
    `validateResearchBackedQueryList`,
    `validateResearchBackedConfirmedQueryRows`, `newRunId`,
    `createKeywordResearchRun`, `createKeywordResearchQueries`,
    `queryPlanSource`, `keywordResearchApi`, `requestedKeywordResearchId`)
    → zero matches each: all `KI-W4` implementation work remains.
- **Coverage accounting:** no case IDs executable at this step
  (decomposition); required/registered/executed accounting begins at
  `S009`/`S010` and merges at `KI-W4-I001`.
- **External mutations:** none (read-only commands; S1/S2/S3 creation is the
  authorized coordination write).
- **Limitations/deferred:** A5 pin refresh is a parent action; no blocker for
  decomposition under §0.4 after this delta audit.
- **Disposition:** entry gate satisfied; decomposition authoring authorized.

---

## `EV-KI-W4-S02` — Dependency verification, anchors, and digest recomputation

- **Timestamp:** 2026-08-18T19:07:46+05:30
- **Parent window / assignment / sub-window:** `KI-W4` / `ASG-KI-W4-WA-01` / (decomposition)
- **Actor/role:** `KI-W4-WINDOW-AGENT`
- **§1 Decision closure:** every implementation-affecting `KI-W4` decision
  exists in `DEC-KI-033` (A3 lines 1281–1565) with the supporting accepted
  decisions `DEC-KI-003/012/014/015/016/017/019/021`; the A4 task blocks
  `KI-W4-T1`–`T4` are complete; no contradictory authority found
  (`SW-D02`).
- **§2–§5 Anchors and interfaces (verified by read/grep):**
  - `cluster.js` (346 lines): exports listed at S1 §5.1; private
    `tokens`(47)/`facets`(51)/`lane`(85); file-end insertion anchor.
  - `api-serializer.js` (1090 lines): `serializeRun`(928)/
    `serializeRunQuery`(980)/`serializeEditableQueries`(995–1006);
    insertion before `leadRecordToCreate`(1008).
  - `repository.js` (1372 lines): `FinalPublicationAbort`(42–48),
    `getOwned`(348–354), `createRun`(1206), `newResearchId`(132).
  - `query-review.js` (247 lines): `validateEditableQueryList`(56),
    `validateConfirmedQueryRows`(129–247); end-of-file insertion.
  - `prisma-run-repository.js` (4719 lines): `runId()`(71) formula,
    `stableLeadId`(169), `getEditableQueries`(1194),
    `replaceEditableQueries`(1202–1274), `confirmQueryRevision`(1276);
    `server.js:1698` is its only production caller.
  - `server.js` (2061 lines): imports(42), `executeRun`(927),
    `createLeadServer`(1388), `drainQueue`(1493), `handle`(1562), route
    blocks 1573–1654, PUT queries handler 1656–1714, parser helpers
    468–514.
  - Composed helpers exist and are read-only for W4:
    `validateResearchBackedQueries` (`query-mapper.js:55`),
    `mapSelectionToQueries` (`query-mapper.js:32`),
    `keywordResearchConfigV1` (`config.js:167`),
    `serializeKeywordsCsv` (`export.js:188`).
- **§6 Dependency verification:** `replaceEditableQueries` is validated
  upstream in `server.js` (which imports `query-review.js` validators), not
  inside `prisma-run-repository.js`; `api.js` composes
  `repository.js` + `prisma-run-repository.js` + `api-serializer.js`
  exports; `server.js` composes `api.js` + both validators; tests compose
  the manifest. The S1 §4 DAG order follows these named outputs
  (`SW-D06`).
- **§7 Interface freeze:** `I-F1`–`I-F11` (S1 §3.2) fix every cross-file
  signature, default, outcome union, error code, and key set before any
  dependent leaf executes (`SW-D07`).
- **Digest recomputations:** 34-ID manifest union extracted from the A4
  literal matrix (A4 lines 2107–2162), sorted, per-LF →
  `86810ce87a79426bb972be2e2827abc3806835190135d17769b52c33e7bb2203` —
  byte-equal to the `DEC-KI-033` normative digest. Deterministic fixture
  rendering (2-space JSON + trailing LF, 764 bytes) → sha256
  `417f25dd2ab68c30a5ccfe19d3209afb4386435ef852f75dcf87af9f075b8c51`.
- **Coverage accounting:** decomposition-time only.
- **External mutations:** none.
- **Disposition:** anchors, dependencies, and formulas verified; contract +
  exact-anchors authoring style fixed by requester selection this session
  (recorded here as the authoring-style fact behind S1's preamble).

---

## `EV-KI-W4-S03` — Decomposition authoring, mechanical lint, counterexample audit, and readiness certificate

- **Timestamp:** 2026-08-18T19:07:46+05:30
- **Parent window / assignment / sub-window:** `KI-W4` / `ASG-KI-W4-WA-01` / (decomposition)
- **Actor/role:** `KI-W4-WINDOW-AGENT`
- **§1 Artifacts created:** S1
  (`KEYWORD_INTELLIGENCE_KI_W4_SUBWINDOW_CHECKLIST.md`, 1517 lines, sha256
  `f86b9a8c107dfa4281c25eda1fb759a1073c7207ae523ecf4c40d1e3724613e5`),
  S2 (`KEYWORD_INTELLIGENCE_KI_W4_SUBWINDOW_STATE.md`, state_version 1),
  S3 (this file). Authorities do not overlap: S1 decides, S2 records state,
  S3 records facts (`SW-A05`).
- **§2 Adjacency:** leaves report only to the window agent; the parent is
  addressed only through the S2 boundary and the consolidated handoff; no
  subagent may write S1/S2/S3 (`SW-A06`, `SW-E06`).
- **§3 Parent mapping:** S1 §6 allocates every requirement, decision, task,
  scenario, and the 34 cases + 18 controls to exact leaves/tests/gates;
  unmapped counts 0/0/0/0/0 (`SW-D01`).
- **§4 Structure:** ten initial FILE sub-windows (one file each, five
  MODIFY + one MODIFY-CREATE pair per A4 task split: S001–S007 production,
  S008 fixture, S009/S010 tests) plus `KI-W4-I001` ASSESS; zero multi-file
  sub-windows; zero duplicate file owners (`SW-D04`, `SW-D09`).
- **§5 Intermediate states:** S1 §4.1 defines IS-1 through IS-6 with exact
  permitted checks, expected temporary failures (none), resolvers, and
  prohibitions (`SW-D08`).
- **§6 Command safety:** every leaf check is `node --check`, `node --test`
  (focused), `node -e` digest/import scripts, or `grep -c`; none writes
  outside the runner's own outputs; no formatter/installer/generator is
  authorized (`SW-D10`).
- **§7 Block completeness:** mechanical lint over S1 verifies all 15 §7.1
  fields present in all 11 blocks; the §7.5 nine-box checklist appears once
  per FILE block (90 boxes); zero unresolved placeholders; banned-verb scan
  (`choose`, `decide`, `determine`, `as appropriate`, `as needed`,
  `similar to`, `etc.`) over transformation text → zero matches
  (`SW-E01`–`SW-E03`, `SW-R02`).
- **§8 File-local acceptance:** every leaf's V1/V2/V3 checks close inside
  its own file; deferred executions name `KI-W4-I001` gates (`W4-D01`–`D06`
  → `KI-W4-V3`; frozen-input registry re-run → `KI-W4-V2`) (`SW-E07`,
  `SW-E08`).
- **§9 Enforcement closure:** 34 cases allocated with registrations,
  witnesses, oracles, and forbidden-operation assertions (S1 §6.1); 18
  controls mapped to their narrowest cases (S1 §6.2); certificate equality
  and digest rules fixed (S1 §6.4); no zero-work, skipped, filtered,
  duplicate, unexpected, unactivated, or summary-only path can satisfy
  acceptance (`SW-V01`–`SW-V03`, `SW-V09`).
- **§10 Assessment authority:** `KI-W4-I001` carries zero implementation
  write authority, personally executed gates `KI-W4-V1`–`V4`, and the
  `KI-W4-V6` merge; gates are scheduled once at the final assessment per
  the A4 verification economy (`SW-V05`, `SW-V06`, `SW-V08`).
- **§11 Correction protocol:** append-only `KI-W4-C001`+ single-file
  corrections from the same ten-file set, §12.2 certificate before
  assignment, evidence invalidation per changed inputs (`SW-V07`).
- **§12 Boundary:** S2 set to `AWAITING_PARENT_DECOMPOSITION_REVIEW`;
  `next_subwindow KI-W4-S001` is not assignable until the parent records
  decomposition review and the window agent converts it to `READY`
  (`SW-V10`, `SW-R09`).
- **§13 Mechanical lint results:** sub-window IDs unique and ordered
  (`KI-W4-S001`–`S010`, `KI-W4-I001`); writable files equal the ten planned
  paths with per-LF set digest `fe48d14e…`; no path contains `..`, a glob,
  or a directory terminator; 90 unchecked boxes exactly inside the ten §7.5
  checklists; all referenced IDs and digests resolve (`SW-R01`–`SW-R03`,
  `SW-R10`).
- **§14 Counterexample audit (sub-window standard §14, twenty items):**
  (1,3,4) leaf P2/V2 single-file write-set proof + `SW-R03` lint; (2)
  `SW-R03` path grammar; (5) `SW-D03` set-digest equality; (6) S1 §4
  one-owner-per-file table; (7) §4 DAG + predecessors + `I-F1`–`I-F11`
  freeze; (8) §4.1 IS-1–IS-6 with named resolvers; (9)
  `may_start_successor:false` + S2 single `current_subwindow`; (10) §1
  prohibition + `SW-E06`; (11) §7 rule 6/window-agent review prohibition;
  (12) §8 corrective protocol; (13) append-only `KI-W4-Cxxx`; (14)
  `KI-W4-V6` required=registered=executed with witnesses; (15) literal
  manifest digests + control oracle order (unchanged → defect → fresh);
  (16) A4 fidelity table quoted into `S009`; (17) §5.11 gate scheduling and
  invalidation rules; (18) §8 evidence invalidation on correction; (19)
  `KI-W4-V1` assembled-set digest equality; (20) §8 terminal
  `READY_FOR_PARENT_REVIEW` boundary.
- **Coverage accounting (decomposition):** required parent items mapped —
  tasks `KI-W4-T1`–`T4` (4/4), scenarios `SCN-KI-003/008/009/014/015`
  (5/5), manifest IDs 34/34, controls 18/18; unmapped counts zero.
- **External mutations:** none beyond creation of the three subordinate
  artifacts.
- **Readiness counts:** mandatory authoring checklist checked 44 / unchecked
  0; initial sub-window count 10; planned file-set digest `fe48d14e…`;
  multi-file sub-windows 0; duplicate file owners 0; unresolved interfaces
  0; unresolved intermediate states 0; unresolved execution choices 0;
  unresolved evidence references 0.
- **Disposition:** decomposition complete; no leaf assigned; awaiting
  parent decomposition review.

### Certificate

```yaml
certificate: SUBWINDOW-DECOMPOSITION-READY
parent_window_id: KI-W4
parent_assignment_id: ASG-KI-W4-WA-01
window_agent_identity: KI-W4-WINDOW-AGENT
revisions:
  parent_standard: 3b7a4fd25156e1adfbc92abb835c5f82a0d18c686b1c1150feb202f2d944d2ac
  subwindow_standard: 1766f9107ce7d315877b75d4b0ea2b5521dff1c321e12f890b03787d66196ded
  contract: 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c
  decision: c2dc635e5aa58f88c1ec465154663d314af68570fd4cbfdfca7b51c393c6f70f
  parent_checklist: 40f705a423da88b952af4e529566b5a5374d4c7c1d7a0a589642d5906f0744ee
  decomposition: f86b9a8c107dfa4281c25eda1fb759a1073c7207ae523ecf4c40d1e3724613e5
initial_subwindow_ids: [KI-W4-S001, KI-W4-S002, KI-W4-S003, KI-W4-S004, KI-W4-S005, KI-W4-S006, KI-W4-S007, KI-W4-S008, KI-W4-S009, KI-W4-S010]
initial_subwindow_count: 10
planned_file_set: [email_scraper/src/api-serializer.js, email_scraper/src/keyword-intelligence/api.js, email_scraper/src/keyword-intelligence/cluster.js, email_scraper/src/keyword-intelligence/repository.js, email_scraper/src/prisma-run-repository.js, email_scraper/src/query-review.js, email_scraper/src/server.js, email_scraper/test/fixtures/keyword-intelligence/ki-w4-enforcement-manifest-v1.json, email_scraper/test/keyword-intelligence-api.test.js, email_scraper/test/keyword-intelligence-handoff.integration.test.js]
planned_file_set_digest: fe48d14ebec1dffa058cf91cfa9ec10982d4ceaa4c63e0cb9280cabf39a4a59b
unmapped_parent_requirements: []
unmapped_parent_decisions: []
unmapped_parent_tasks: []
unmapped_coverage_cases: []
duplicate_initial_file_owners: []
multi_file_subwindows: []
unresolved_interfaces: []
unresolved_intermediate_states: []
unresolved_execution_choices: []
unresolved_evidence_references: []
mandatory_authoring_items_checked: 44
mandatory_authoring_items_unchecked: 0
first_subwindow: KI-W4-S001
integration_assessment_id: KI-W4-I001
parent_review_required: true
```

Certificate notes: `decision` and `parent_checklist` record the observed
(post-`CHG-KI-016`) revisions per `EV-KI-W4-S01` §2; the stale A5 pins and
the residual parent refresh action are documented there.

---

## `EV-KI-W4-S04` — Parent decomposition approval converted to READY

- **Timestamp:** 2026-08-18T19:19:53+05:30
- **Parent window / assignment / sub-window:** `KI-W4` / `ASG-KI-W4-WA-01` / (state transition)
- **Actor/role:** `KI-W4-WINDOW-AGENT`
- **Parent actions verified:** `EV-KI-A-039` present in A6 at line 2886
  (decomposition acceptance; content authenticated through the
  `fe48d14e…`/`86810ce8…` digest reproductions recorded in
  `EV-KI-W4-S01`/`S02`, not the stale byte pins); `CHG-KI-017` present in
  A7 at line 294 (metadata-only pin correction); A5 at state 101 pins A3
  `c2dc635e…` and A4 `40f705a4…` — both recomputed equal to the observed
  files this session (`PINS-MATCH` confirmed); `current_status:
  DECOMPOSITION_APPROVED`; assignment `ASG-KI-W4-WA-01`, agent, authorized
  windows/actions unchanged.
- **Transition performed (sub-window standard §12.1):** S2 state_version
  1→2; `decomposition_status: AWAITING_PARENT_DECOMPOSITION_REVIEW` →
  `READY`; `window_status: EXECUTING`; residual parent action (pin refresh)
  cleared as completed by the parent; `next_subwindow: KI-W4-S001` now
  assignable. No S1 revision change (`f86b9a8c…` still current); no leaf
  assigned in this entry.
- **Coverage accounting:** unchanged (begins at `S009`/`S010`).
- **External mutations:** none (S2 edit + this S3 append are the authorized
  coordination writes).
- **Disposition:** first leaf `KI-W4-S001` assignable by the window agent
  under strict sequential execution (`SW-R09` satisfied).

---

## `EV-KI-W4-S05` — Window-agent review of `KI-W4-S001` (ACCEPTED_FOR_INTEGRATION)

- **Timestamp:** 2026-08-18T19:28:22+05:30
- **Parent window / assignment / sub-window:** `KI-W4` / `ASG-KI-W4-WA-01` / `KI-W4-S001`
- **Actor/role:** `KI-W4-WINDOW-AGENT` (independent review, sub-window standard §8)
- **Handoff under review:** `cluster.js` modification reported complete by the
  implementation side; requester committed the result as
  `0d207c058d20b6c7f4f6a3ec0d7aced93f32f35a` ("01") — requester-owned commit
  policy recorded in S2 (execution policy notes) before this review.
- **Verification battery (commands and decisive results):**
  1. Baseline: `git show d98ad53c…:src/keyword-intelligence/cluster.js | sha256sum`
     → `7dfbda3412c47eb28147cf80f4f05f368c946057f99e2f218a0287159701260b` —
     equals the frozen S1 §5.1 `starting_file_digest` (§8 item 1 ✓).
  2. Write set: `git diff --stat d98ad53c…0d207c0` → exactly
     `src/keyword-intelligence/cluster.js`, +5/−0; `git status --porcelain`
     in both nested repositories → empty (§8 items 2, 13 ✓); frontend clean;
     root change set = §2 inventory + the three subordinate artifacts only
     (§8 item 3 ✓).
  3. Transformation: appended block extracted and diffed against the S1 §3.2
     `I-F1` verbatim rendering → byte-equal on all four code lines and the
     preceding blank line; the single deviation is a missing trailing LF at
     end-of-file (§8 items 4–6: interface `classifyKeywordForSelection`
     byte-exact; EOF newline is non-behavioral formatting freedom under
     §7.3, recorded here so `KI-W4-V1`/`W4-C06` diff inspection is not
     surprised; no corrective window for one formatting byte).
  4. Checks: `node --check src/keyword-intelligence/cluster.js` → exit 0;
     `grep -c "export function classifyKeywordForSelection"` → `1`;
     `node --test test/keyword-intelligence-parity.test.js` → 11 tests,
     11 pass, 0 fail, 0 skipped — activation witness: the suite imports
     `keyword-intelligence/cluster.js` and passed unmodified (tree clean
     proves no suite edit; §8 items 7, 11 ✓).
  5. Coverage: zero local case IDs required by S1 §5.1 → 0 = 0 = 0
     (§8 item 8 ✓); `W4-A04` remains allocated to `S009`/I001.
  6. Intermediate state: IS-1 respected — no caller was wired, exactly as
     prescribed for `S001` (§8 item 12 ✓).
- **Ending digest:** `77ba9f6e2f210842b33e06a589e64d249bf1ad3f28655236e40c1fe9995fbd17`
  (recorded as the new `cluster.js` baseline for all successors; the ten-file
  set membership, not content, feeds `KI-W4-V1`).
- **Coverage accounting:** window totals unchanged (34 IDs pending in
  `S009`/`S010`/I001).
- **External mutations:** none attributable to the leaf; the commit is the
  requester's own action under the recorded policy.
- **Disposition:** `ACCEPTED_FOR_INTEGRATION` — `KI-W4-S001` closed;
  `KI-W4-S002` is the next assignable sub-window under strict sequential
  execution. No successor work has begun.

---

## `EV-KI-W4-S06` — Window-agent review of `KI-W4-S002` (ACCEPTED_FOR_INTEGRATION)

- **Timestamp:** 2026-08-18T20:04:16+05:30
- **Parent window / assignment / sub-window:** `KI-W4` / `ASG-KI-W4-WA-01` / `KI-W4-S002`
- **Actor/role:** `KI-W4-WINDOW-AGENT` (independent review, sub-window standard §8)
- **Handoff under review:** `api-serializer.js` modification; requester
  commit `a375849` ("S002") — the commit landed between review commands and
  the reviewed bytes are identical to the inspected working-tree bytes
  (digest `1003eb3b…` both before and after the commit).
- **Verification battery:**
  1. Baseline: `git show 0d207c0…:src/api-serializer.js | sha256sum` →
     `d1c6c579c150f1df17284c3c108d46710cf7e963dac5723de4b85f7a4e11fc56` —
     equals the frozen S1 §5.2 starting digest (§8 item 1 ✓).
  2. Write set: `git diff --stat 0d207c0…a375849` → exactly
     `src/api-serializer.js`, +87/−2; both nested repositories clean;
     frontend clean; root = inventory + three subordinate artifacts (§8
     items 2, 3 ✓).
  3. Transformation vs S1 §5.2: insertion of `serializeSelectionItem` and
     `serializeKeywordResearch` after `serializeEditableQueries` and before
     `leadRecordToCreate` ✓; `serializeSelectionItem` emits exactly the nine
     `DEC-KI-014` keys in order (`itemId,sourceKind,sourceKeywordId,
     originalKeyword,keyword,sourceSeeds,lane,facets,metricsSnapshot`) with
     no internal fields ✓; `serializeKeywordResearch` emits exactly the 17
     `DEC-KI-019` keys in order ✓; `statusUrl` template exact ✓; `progress`
     is `{stage,expansion,anchorScreen,marketOverview}` with `StageCounts`
     exactly `{expected,terminal,succeeded,skipped,failed}` ✓; stage
     derivation: terminal states map to `completed|failed`, zero stage rows
     → `queued`, otherwise first incomplete of
     `expansion→anchor_screen→market_overview`, all-complete → `finalizing`
     ✓; `result` non-null only for `state==="completed"` ✓; `selection`
     ordered via `serializeSelectionItem` with `[]` default ✓;
     `selectionConflicts` array-guarded ✓; `safeError` `{code,message}|null`
     ✓; dates ISO with non-null created/updated ✓.
  4. Stage-row column binding verified against `prisma/schema.prisma`
     `KeywordResearchStage` (lines 622–654): `expectedCount`, `terminalCount`,
     `succeededCount`, `skippedCount`, `failedCount`, `state` all exist and
     are read by exact name; `cancelledCount` correctly excluded from the
     five-key `StageCounts`.
  5. `serializeRun` trailing conditional spread adds exactly
     `queryPlanSource:"keyword_research"`, `keywordResearchId`,
     `keywordSelectionRevision` only when `run.queryPlanSource ===
     "keyword_research"`; `serializeRunQuery` adds exactly the S1-specified
     conditional `keywordResearchItemId` spread — byte-equal to the frozen
     interface text (§8 item 6 ✓).
  6. Checks: `node --check` → exit 0; symbol count → `2`;
     `node --test test/api-serializer.test.js` → 15 tests, 15 pass, 0 fail,
     0 skipped — legacy `serializeRun`/`serializeRunQuery` deep-equal key-set
     baselines pass unmodified (§8 items 7, 11 ✓).
  7. Coverage: zero local case IDs → 0 = 0 = 0 (§8 item 8 ✓); `W4-A03`,
     `W4-S03`, `W4-NC01/NC03/NC11` remain allocated to `S009`.
  8. Intermediate state IS-1 respected: no caller wired; the new exports
     await `S006`/`S007` (§8 item 12 ✓); no successor work begun (§8 item
     13 ✓).
- **Recorded interface note (non-defect):** `serializeKeywordResearch`
  derives per-stage rows via last-write-wins over the attached `stages`
  array; the production caller `S003.getOwnedApiView` supplies the frozen
  `orderBy: [{stage:"asc"},{generation:"asc"}]` include, making the last row
  per stage name the latest generation. Successors must preserve that
  include ordering.
- **Ending digest:** `1003eb3b236d7830a3ac9df56c4ac9a8df7e50cb784f454018691efa3aabd4c9`
  (new `api-serializer.js` baseline).
- **External mutations:** none attributable to the leaf; commit is the
  requester's own under the recorded policy.
- **Disposition:** `ACCEPTED_FOR_INTEGRATION` — `KI-W4-S002` closed;
  `KI-W4-S003` (`repository.js`) is the next assignable sub-window.

---

## `EV-KI-W4-S07` — Window-agent review of `KI-W4-S003` (ACCEPTED_FOR_INTEGRATION)

- **Timestamp:** 2026-08-18T20:16:09+05:30
- **Parent window / assignment / sub-window:** `KI-W4` / `ASG-KI-W4-WA-01` / `KI-W4-S003`
- **Actor/role:** `KI-W4-WINDOW-AGENT` (independent review, sub-window standard §8)
- **Handoff under review:** `repository.js` modification; requester commit
  `c4d1c25` ("S003").
- **Verification battery:**
  1. Baseline: `git show a375849…:src/keyword-intelligence/repository.js | sha256sum`
     → `e2cad9ea0d47adca3baeb28261da7a09ad775e5fc15c1ecde33f132d7387ee39` —
     equals the frozen S1 §5.3 starting digest (§8 item 1 ✓).
  2. Write set: `git diff --stat a375849…c4d1c25` → exactly
     `src/keyword-intelligence/repository.js`, +55/−34; backend and frontend
     clean; root = inventory + three subordinate artifacts (§8 items 2, 3 ✓).
  3. Transformation vs S1 §5.3: `class RunHandoffAbort extends Error {}`
     inserted immediately after `FinalPublicationAbort` (lines 42–48) with
     one blank line ✓; `getOwnedApiView` inserted after `getOwned` with the
     exact body — `requireResearchId`/`requireOwner`, owner-filtered
     `findFirst`, `include: { stages: { orderBy: [{ stage: "asc" }, {
     generation: "asc" }] } }` (preserves the S002-recorded serializer
     last-row-per-stage contract), `{outcome:"not_found"}|{outcome:"found",
     research}` ✓ (§8 item 4 ✓).
  4. `createRun` restructure audited line-by-line against DEC-KI-033
     (A3 lines 1404–1413): every pre-write path (`not_found`, handoff replay
     equality → `found`, unequal replay → `conflict`,
     `KEYWORD_RESEARCH_NOT_COMPLETED`, `KEYWORD_SELECTION_REVISION_CONFLICT`)
     remains a normal return before any write ✓; post-write validation now
     `throw new RunHandoffAbort()` inside the interactive transaction with
     Run identity checks extended to `run.ownerId === research.ownerId` ✓
     and per-index query lineage `query.keywordResearchItemId ===
     items[index].itemId` (order enforced through lineage) ✓; handoff-row
     create remains after both callbacks ✓; the outer catch maps
     `RunHandoffAbort` to `{outcome:"conflict",code:"KEYWORD_RUN_HANDOFF_INVALID"}`
     only after the transaction (and therefore rollback) has completed, and
     rethrows every other error ✓. This converts the prior normal-return
     defect (control `W4-NC05`) into the locked sentinel semantics.
  5. Preserved behavior: `_transaction` helper, all error codes, replay
     fencing, and every other method byte-identical outside the audited
     hunks (§8 items 5, 9 ✓).
  6. Checks: `node --check` → exit 0; `grep -c "getOwnedApiView\|
     RunHandoffAbort"` → `5` (≥2 declaration sites);
     `node --test test/keyword-intelligence-repository.test.js` → 11 tests,
     11 pass, 0 fail, 0 skipped (§8 items 7, 11 ✓).
  7. Coverage: zero local case IDs → 0 = 0 = 0 (§8 item 8 ✓); `W4-D01`–`D05`
     fencing executes at `S010`/I001 `KI-W4-V3`.
  8. Intermediate state IS-1 respected; no caller wired; no successor work
     begun (§8 items 12, 13 ✓).
- **Ending digest:** `fa249de27bc6d47c2480c342c5bf5760868328445e83dca9bb31be97fa2387c7`
  (new `repository.js` baseline).
- **External mutations:** none attributable to the leaf; commit is the
  requester's own under the recorded policy.
- **Disposition:** `ACCEPTED_FOR_INTEGRATION` — `KI-W4-S003` closed;
  `KI-W4-S004` (`query-review.js`) is the next assignable sub-window.

---

## `EV-KI-W4-S08` — Window-agent review of `KI-W4-S004` (ACCEPTED_FOR_INTEGRATION)

- **Timestamp:** 2026-08-18T20:28:41+05:30
- **Parent window / assignment / sub-window:** `KI-W4` / `ASG-KI-W4-WA-01` / `KI-W4-S004`
- **Actor/role:** `KI-W4-WINDOW-AGENT` (independent review, sub-window standard §8)
- **Handoff under review:** `query-review.js` modification; requester commit
  `3580413` ("S004").
- **Verification battery:**
  1. Baseline: `git show c4d1c25…:src/query-review.js | sha256sum` →
     `5cfbbe77aaa9dc94a5fe852d857f38bff52220518d510cc6eacd1b429f35d67a` —
     equals the frozen S1 §5.4 starting digest (§8 item 1 ✓).
  2. Write set: `git diff --stat c4d1c25…3580413` → exactly
     `src/query-review.js`, +213/−0 (one import line plus the appended
     block); backend and frontend clean; root = inventory + three
     subordinate artifacts (§8 items 2, 3 ✓). Legacy code untouched
     (additive-only diff; §8 item 9 ✓).
  3. Delegated-contract binding verified against
     `src/keyword-intelligence/query-mapper.js` (read-only, unchanged):
     `validateResearchBackedQueries({rows,persistedItemIds,sourceKeywords,
     stripTokens})` → `{ok:true,rows:[{itemId,sequence,phrase,lane}]}` |
     `{ok:false,error,issues:[{field,code,length?,missingIds?,extraIds?}]}`;
     the leaf consumes exactly these fields and enforces 1–100 rows
     (`rows_length`), grammar partitions, and the strict prefix set
     (`site:myshopify.com/products ` | `site:myshopify.com `).
  4. Edit validator audited against A3 lines 1430–1439: strict
     `{id,categoryIndex,query}` row grammar with unknown-field/row-shape/
     category errors in the existing public error-row shape ✓; item-ID
     recovery from `run.queries[].keywordResearchItemId` ✓; exact query-ID
     set equality (unknown id → per-row `query_id_set_mismatch`; missing
     persisted id → set-level error with `missingIds`) ✓; unchanged
     category index enforced against the persisted row ✓; order and
     query-text changes allowed ✓; delegation to
     `validateResearchBackedQueries` with snapshot-derived
     `sourceKeywords`/`dedupStripTokens` ✓; return exactly
     `{valid,queries:[{id,categoryIndex,query}],errors}` ✓.
  5. Confirmation validator audited against A3 lines 1440–1455: strict
     `options.snapshot` gate (`contractVersion:"keyword-run-snapshot-v1"`,
     fail-closed `invalid_snapshot` before any probe) ✓; `sourceKeywords`
     built from `snapshot.items` keyed by `itemId` ✓; durable rows mapped
     as `{itemId:row.keywordResearchItemId,sequence:row.query}` ✓;
     revalidation with `snapshot.dedupStripTokens` ✓; the mapper's
     normalized `phrase` feeds `product_phrase`/`product_family` while
     `query` stays the full mapped query ✓; remaining candidate fields
     exactly `market_signal:"user_confirmed"`, `seasonality:"unknown"`,
     persisted generation reason (`"keyword_research"` fallback equals the
     S005-persisted value)/source URLs, `confidence:1` ✓; the existing
     `freshReusableProbe`/`queryProbeFingerprint`/`normalizeProbeResults`
     seam used once per non-reusable valid row (single batched `probe`
     call) ✓; validity = all rows valid with no per-category exact-count
     rule ✓; `{valid,errors,rows,queryPlans}` return shape mirrors
     `validateConfirmedQueryRows` with `queryPlans` built from snapshot
     lineage fields ✓; probe summary block byte-mirrors the legacy
     serializer fields ✓.
  6. Checks: `node --check` → exit 0;
     `grep -c "export function validateResearchBacked"` → `2`;
     `node --test test/query-review.test.js test/query-review-server.test.js`
     → 7 tests, 7 pass, 0 fail, 0 skipped — legacy validator and server
     query-review behavior frozen green (§8 items 7, 11 ✓).
  7. Coverage: zero local case IDs → 0 = 0 = 0 (§8 item 8 ✓);
     `W4-Q01`–`Q08` execute in `S009`.
  8. Intermediate state IS-1 respected; no caller wired; no successor work
     begun (§8 items 12, 13 ✓).
- **Recorded interface notes (non-defects):**
  a. The edit validator's returned `queries[].query` carries the incoming
     raw text (normalization is applied by the mapper on every consumption
     path — confirmation reads, fingerprints, and probes all use
     `normalized.sequence`). `S007` and `S009` oracles must not assume
     normalized echo from the edit path.
  b. `validateResearchBackedConfirmedQueryRows` is a thin synchronous
     wrapper delegating to the private async
     `confirmResearchBackedQueryRows`; the public signature and defaults
     are exactly `I-F4` (options destructuring mirrors the legacy
     validator, including `snapshot`).
- **Ending digest:** `1b0c5460a96ea1857e78d0a6dd589f20ef218e4d9d911ebf4afd507c58b83a26`
  (new `query-review.js` baseline).
- **External mutations:** none attributable to the leaf; commit is the
  requester's own under the recorded policy.
- **Disposition:** `ACCEPTED_FOR_INTEGRATION` — `KI-W4-S004` closed;
  `KI-W4-S005` (`prisma-run-repository.js`) is the next assignable
  sub-window.

---

## `EV-KI-W4-S09` — Window-agent review of `KI-W4-S005` (ACCEPTED_FOR_INTEGRATION)

- **Timestamp:** 2026-08-18T20:40:42+05:30
- **Parent window / assignment / sub-window:** `KI-W4` / `ASG-KI-W4-WA-01` / `KI-W4-S005`
- **Actor/role:** `KI-W4-WINDOW-AGENT` (independent review, sub-window standard §8)
- **Handoff under review:** `prisma-run-repository.js` modification; requester
  commit `ff7081b` ("S005").
- **Verification battery:**
  1. Baseline: `git show 3580413…:src/prisma-run-repository.js | sha256sum`
     → `c719ed27276cba78bbb140cf8a1241b19af426db82e5dedf40a99363a89da173` —
     equals the frozen S1 §5.5 starting digest (§8 item 1 ✓).
  2. Write set: `git diff --stat 3580413…ff7081b` → exactly
     `src/prisma-run-repository.js`, +166/−2; backend and frontend clean;
     root = inventory + three subordinate artifacts (§8 items 2, 3 ✓).
  3. `newRunId()` exported immediately after `stableLeadId`, delegating to
     the existing private `runId()` formula — exact I-F5 ✓. Imports used
     (`mapSelectionToQueries`, `fingerprintJson` line 41,
     `PipelineInvariantError` line 44) all pre-existing; no new dependency
     (§8 item 5 ✓).
  4. `createKeywordResearchRun` audited against A3 lines 1365–1403: exact
     seven-key input requirement (fail-closed `PIPELINE_INPUT_CONFLICT`) ✓;
     categories = ordered seeds mapped to
     `{originalShopType,shopType,businessQualifier:"unspecified"}` ✓; one
     `tx.run.create` from `runCreateData(research.ownerId,categories,runId)`
     overriding exactly the ten frozen fields; lease fields and
     `confirmedQueryRevision`/`queriesConfirmedAt` remain null via the
     `runCreateData` defaults ✓; no queue/planner interaction ✓.
  5. `createKeywordResearchQueries` audited: exact four-key input ✓;
     `items` deep-equal `snapshot.items` via canonical `fingerprintJson`
     equality (JSON-canonical deep equality; both sides are plain JSON
     documents) ✓; one `mapSelectionToQueries` map ✓; rows carry the mapped
     query, `source:"generated"`, `validationState:"pending"`,
     `generationReason:"keyword_research"`, stable `keywordResearchItemId`,
     and `categoryIndex` from the first `sourceSeeds` member index in
     `snapshot.seeds` (missing membership throws) ✓; one
     `tx.runQuery.createMany` with count===N check ✓; returns constructed
     rows without a read ✓.
  6. `replaceEditableQueries` research branch audited against A3 lines
     1414–1429: `buildKeywordResearchReplacementRows` runs after the
     owner/state/revision read and before the CAS `updateMany` ✓; enforces
     duplicate-incoming rejection, unknown-ID rejection, exact set size
     equality, unique non-null `keywordResearchItemId` per persisted row,
     and per-row `categoryIndex` equality ✓; reorder-only rows are
     `{...existing, sequence, updatedAt}` preserving `source` and all probe
     evidence ✓; text-change rows set `source:"user_edited"`,
     `validationState:"pending"`, clear rejection/probe fields, preserve
     `id`/`keywordResearchItemId`/`createdAt`/`queryScore`/
     `generationReason`/`sourceUrls`/`categoryVocabulary` ✓; unknown
     discriminator throws `PIPELINE_INPUT_CONFLICT` before the CAS ✓; the
     `legacy` branch (including `user_added` rows) is unchanged inside its
     new guard ✓; delete+bulk-create stays inside the revision-CAS
     transaction ✓.
  7. Checks: `node --check` → exit 0; `export function newRunId` count →
     `1`; `node --test test/prisma-run-repository.test.js` → 53 tests, 53
     pass, 0 fail, 0 skipped — legacy suite including existing
     `replaceEditableQueries` coverage green (§8 items 7, 11 ✓).
  8. Coverage: zero local case IDs → 0 = 0 = 0 (§8 item 8 ✓);
     `W4-D01/D02/D06`, `W4-Q02/Q04` execute at `S009`/I001 `KI-W4-V3`.
  9. Intermediate state IS-1 respected; no caller wired; no successor work
     begun (§8 items 12, 13 ✓).
- **S1 check-literal correction (non-defect, recorded):** S1 §5.5 C3 asked
  for `grep -c "createKeywordResearchRun\|createKeywordResearchQueries"` ≥ 4
  ("declaration plus export/import sites"). The correct in-file shape is
  exactly `2` — the two instance-method declarations; the composer call
  sites belong to `S006`'s `api.js`, not this file. The S1 literal
  over-counted at authoring time; the observed `2` is the contract-correct
  value. No code defect; `S006` consumers must call both methods exactly as
  I-F3/I-F5 freeze them.
- **Ending digest:** `d4995ef9e177dbf9f0fad5c199b9c8f5e63fd37122919ba256aa1282f842db27`
  (new `prisma-run-repository.js` baseline).
- **External mutations:** none attributable to the leaf; commit is the
  requester's own under the recorded policy.
- **Disposition:** `ACCEPTED_FOR_INTEGRATION` — `KI-W4-S005` closed;
  `KI-W4-S006` (`api.js` CREATE) is the next assignable sub-window.

---

## `EV-KI-W4-S10` — Window-agent review of `KI-W4-S006` (ACCEPTED_FOR_INTEGRATION)

- **Timestamp:** 2026-08-18T21:38:35+05:30
- **Parent window / assignment / sub-window:** `KI-W4` / `ASG-KI-W4-WA-01` / `KI-W4-S006`
- **Actor/role:** `KI-W4-WINDOW-AGENT` (independent review, sub-window standard §8)
- **Handoff under review:** `api.js` creation; requester commit `22a8dd8`
  ("S006").
- **Verification battery:**
  1. Baseline: file ABSENT at `ff7081b…` per the frozen S1 §5.6
     `starting_file_digest: ABSENT`; `git diff --stat ff7081b…22a8dd8` →
     exactly one new file `src/keyword-intelligence/api.js`, +549/−0 (§8
     items 1, 2 ✓). The five previously accepted production baselines
     re-hashed unchanged (`77ba9f6e…`, `1003eb3b…`, `fa249de2…`,
     `1b0c5460…`, `d4995ef9…`); backend/frontend clean; root = inventory +
     three subordinate artifacts (§8 item 3 ✓).
  2. Composition bindings verified against the live exports:
     `newResearchId` (repository.js:132), `newRunId`
     (prisma-run-repository.js, S005), `keywordResearchConfigV1` +
     `keywordResearchConfigV1Schema` (config.js:167/171),
     `serializeKeywordsCsv` (export.js:188), `classifyKeywordForSelection`
     (cluster.js, S001), `mapSelectionToQueries` (query-mapper.js:32),
     `analyzeSelectionConflicts`/`normalizeSeeds`/`selectionItemId`
     (selection.js:190/30/12), `keywordResearchResultV1Schema`
     (schemas.js:160), `ApiError` (api-errors.js:1) — all exist; factory
     signature and defaults exactly `I-F6` (§8 items 4, 5 ✓).
  3. Method audit vs DEC-KI-033/019: `createResearch` strict-parses then
     `normalizeSeeds` before any repository call (invalid input → zero
     calls) ✓; one `keywordRepository.create`, `dispatchInitialize` only
     after the `created` commit, dispatcher failures swallowed with the
     durable queued row returned (rollback/delete forbidden; W4-A02/W4-NC02
     semantics) ✓. `getResearch` one `getOwnedApiView`, contract assertion
     (version 1 + config schema + config fingerprint + completed-result
     schema), `not_found` → 404 ✓. `saveSelection` canonicalizes every item
     through `classifyKeywordForSelection` with calculated/manual lineage
     checks (metrics/seed/lane/facet equality against the persisted result
     row; manual rows use first seed and stable id) ✓; conflict analyzer
     before the CAS; non-`created` repository outcome → 409 revision
     conflict ✓; updated view serialized without a second read ✓.
     `createRun` validates `clientRequestId` regex, completed state,
     expected revision, 1–100 items, zero conflicts; builds
     `keyword-run-snapshot-v1` with `selectionFingerprint`
     (`fingerprintJson` of the A3-specified object), `configFingerprint`,
     `dedupStripTokens`, `seeds`, and items with `initialQuery` from
     `mapSelectionToQueries` ✓; invokes `keywordRepository.createRun` with
     exactly the `I-F3` callback composition (`constructRun`/
     `constructQueries` spread into the S005 methods with
     `selectionRevision`/`selectionFingerprint`/`snapshot`) ✓; outcome
     mapping covers `not_found`, `KEYWORD_RESEARCH_NOT_COMPLETED`,
     `KEYWORD_SELECTION_REVISION_CONFLICT`, handoff conflict; returns
     `{created, run: serializeRun(run), statusUrl:"/api/runs/<id>"}` ✓;
     no `queueDrain`, no planner, no live-selection snapshot ✓.
     `exportCsv` parses exactly the DEC-KI-019 parameter contract (unknown
     name, duplicate singles, >20 flags, malformed numbers, empty/malformed
     bounds rejected; `minVolume` ≤ 2147483647, `minOpportunity` 0–100,
     lane enum, recommended bool, market enum) ✓; market overlay exactly
     the 12 frozen keys with null-market exclusion for named markets ✓;
     conjunctive filter predicate (seed membership under NFKC/trim/
     collapse/case-fold, exact cluster/intent/lane/facet membership,
     numeric minima with null-opportunity exclusion, recommendation,
     every flag present, case-folded haystack substring over keyword/
     seeds/cluster/lane/facets/flags) ✓; persisted result-keyword order
     preserved into `serializeKeywordsCsv` ✓; one read, zero writes ✓.
  4. Checks: `node --check` → exit 0; export-set import smoke → exactly
     `['createKeywordResearchApi']`, `OK` printed (activation witness: the
     module graph loads without a database connection) (§8 items 7, 11 ✓).
  5. Coverage: zero local case IDs → 0 = 0 = 0 (§8 item 8 ✓); `W4-A01`–
     `A08` execute in `S009`.
  6. Intermediate state IS-2 respected: module importable, unused by
     `server.js`; no successor work begun (§8 items 12, 13 ✓).
- **Recorded interface notes (binding for `KI-W4-S007`/`S009`):**
  a. The service surfaces typed failures by throwing
     `ApiError(status, code, message[, details])` — not by returning
     outcome objects. All seven frozen §3.3 codes are present with correct
     statuses (400 `KEYWORD_RESEARCH_INPUT_INVALID`, 409
     `KEYWORD_RESEARCH_CONTRACT_MISMATCH`, 404
     `KEYWORD_RESEARCH_NOT_FOUND`, 409 `KEYWORD_RESEARCH_NOT_COMPLETED`,
     409 `KEYWORD_SELECTION_HAS_CONFLICTS`, 409
     `KEYWORD_SELECTION_REVISION_CONFLICT`, 409
     `KEYWORD_RUN_HANDOFF_CONFLICT`). `S007` routes must let the existing
     `ApiError` mapper produce these responses and map `createRun`'s
     `created:true|false` to 201|200.
  b. `dispatchInitialize` receives the initialize message
     `{contractVersion:1, type:"keyword.initialize.v1", researchId,
     generation:1}`; the `S007` lazy wrapper forwards it through
     `sendOne(..., keywordMessageSchema)`.
  c. `exportCsv` returns the CSV body string (serializer output), not a
     wrapper object; `S007` sets the frozen CSV headers around it.
- **Ending digest:** `8c6e9845c0847e49f5eaa30f815e2fd4287db899a62c8aeb815adcdd730971fb`
  (new `api.js` baseline).
- **External mutations:** none attributable to the leaf; commit is the
  requester's own under the recorded policy.
- **Disposition:** `ACCEPTED_FOR_INTEGRATION` — `KI-W4-S006` closed;
  `KI-W4-S007` (`server.js`) is the next assignable sub-window.

---

## `EV-KI-W4-S11` — Window-agent review of `KI-W4-S007` (CORRECTION_REQUIRED) and `KI-W4-C001` readiness

- **Timestamp:** 2026-08-18T21:58:45+05:30
- **Parent window / assignment / sub-window:** `KI-W4` / `ASG-KI-W4-WA-01` / `KI-W4-S007`
- **Actor/role:** `KI-W4-WINDOW-AGENT` (independent review, sub-window standard §8)
- **Handoff under review:** `server.js` modification; requester commit `6e6cdf3`
  ("S007"); reviewed working-tree bytes identical to the committed blob
  (digest `77e364ca…` before and after the commit).
- **Conforming findings (verified):**
  1. Baseline: `git show 22a8dd8…:src/server.js | sha256sum` → `73b2384a…` —
     equals the frozen S1 §5.7 starting digest; write set exactly one file,
     +198/−32; backend/frontend clean; root = inventory + three artifacts.
  2. Imports: both research validators beside `validateEditableQueryList`;
     `createKeywordResearchApi`; `PrismaKeywordResearchRepository`;
     `keywordMessageSchema` verified exported at
     `aws-pipeline/keyword-intelligence/contracts.js:94`.
  3. `requestedKeywordResearchId` mirrors `requestedRunId` with the exact
     `^kr_[A-Za-z0-9_-]{24}$` pattern and 400
     `KEYWORD_RESEARCH_INPUT_INVALID` on decode/pattern failure.
  4. Five routes: 202 create / 200 get / 200 selection / 201-or-200 runs
     (via `handoff.created`) / CSV with the exact frozen headers
     (`text/csv; charset=utf-8`, attachment filename
     `keyword-research-<id>.csv`, `no-store`); owner only from
     `trustedUserId`; `exportCsv` result used as the raw body with
     `content-length`.
  5. `createLeadServer`: injected `keywordResearchApi` honored; default
     constructs exactly one service with `now: () => currentDate(now)` and
     the lazy `dispatchInitialize` (runtime → `sendOne(queueUrl, message,
     keywordMessageSchema)`); missing dispatcher or missing/invalid queue
     URL returns a failed-send result without an SQS call (no environment
     read, no new config key; https-strictness recorded as a non-weakening
     addition; the returned shape's empty `failedItemIds` is immaterial —
     no consumer reads it).
  6. `executeRun` both confirmation branches select
     `researchQueryValidationPipeline(rows, categories, config, status,
     {…, snapshot: keywordSelectionSnapshot})` only for
     `keyword_research`; `legacy`/null keep the injected legacy pipeline
     and exact-count policy; any other discriminator throws
     `PIPELINE_INPUT_CONFLICT` before validation/probe/dispatch. `drainQueue`
     passes `queryPlanSource` and `keywordSelectionSnapshot` from the
     claimed run.
  7. Edit and explicit-start paths select
     `validateResearchBackedQueryList` only for `keyword_research` with the
     same unknown-discriminator fence; legacy paths byte-preserved.
  8. Checks: `node --check` exit 0; `grep -c requestedKeywordResearchId` →
     5; `node --test test/server.test.js test/query-review-server.test.js`
     → 16 tests, 16 pass, 0 fail, 0 skipped (legacy frozen fixtures green).
- **Defect (the correction trigger):** the helper `keywordResearchBody`
  deletes `ownerId` and `researchId` from every keyword-research request
  body before strict parsing. DEC-KI-019 locks "unknown body/query keys
  reject 400"; `ownerId`/`researchId` are unknown keys in every frozen body
  contract. The helper converts a contract-mandated 400 into a silent
  accept (the discarded value never influences the owner — header identity
  always wins — so this is strictness drift, not an authorization bypass;
  control `W4-NC15` remains unfalsified). S1 §5.7 item 4 and the `W4-S01`
  oracle (unknown body key → exact 400) fail against these bytes.
- **Root cause:** defensive owner-injection guarding was implemented at the
  route layer by stripping instead of relying on the already-strict zod
  schemas, which are the locked rejection mechanism.
- **Remedy (single file, no scope expansion):** in `server.js`, delete
  `keywordResearchBody` and pass each `readJsonBody` payload straight into
  the service call (`{ ownerId, researchId?, ...payload }` for the
  path-parameter routes; `{ ownerId, ...payload }` for the collection
  route). The strict schemas then produce the mandated 400 for every
  unknown key including `ownerId`/`researchId`. No other line changes.
- **Corrective readiness certificate (sub-window standard §12.2):**

  ```yaml
  certificate: CORRECTIVE-SUBWINDOW-READY
  parent_window_id: KI-W4
  corrective_subwindow_id: KI-W4-C001
  window_agent_identity: KI-W4-WINDOW-AGENT
  trigger_evidence: [EV-KI-W4-S11]
  root_cause: route-layer body-key stripping bypassed the locked strict-schema 400 rejection for ownerId/researchId
  governing_parent_requirements: [REQ-KI-001, REQ-KI-002, REQ-KI-019]
  governing_parent_decisions: [DEC-KI-019, DEC-KI-033]
  corrected_prior_subwindows: [KI-W4-S007]
  writable_file: email_scraper/src/server.js
  starting_file_digest: 77e364ca93e1c6e4b1847c1a480b233915495a9299a5da777ca370526c3f685b
  predecessors: [KI-W4-S007]
  invalidated_evidence: []
  invalidated_gates: []  # no gate has run; V1-V4 unaffected
  unresolved_parent_decisions: []
  expanded_parent_scope_required: false
  section_7_fields_complete: true
  single_file_write_set: true
  unresolved_execution_choices: []
  next_integration_assessment_id: KI-W4-I001
  status: READY
  ```

- **Coverage accounting:** unchanged (all case IDs pending in
  `S009`/`S010`/I001).
- **External mutations:** none attributable to the leaf; commit is the
  requester's own under the recorded policy.
- **Disposition:** `CORRECTION_REQUIRED` — `KI-W4-S007` remains open;
  `KI-W4-C001` (single-file correction of `server.js`) is READY and is the
  next assignable sub-window. `KI-W4-S008` waits until the correction is
  accepted.

---

## `EV-KI-W4-S12` — Execution and acceptance of correction `KI-W4-C001`

- **Timestamp:** 2026-08-18T22:02:18+05:30
- **Parent window / assignment / sub-window:** `KI-W4` / `ASG-KI-W4-WA-01` / `KI-W4-C001` (corrects `KI-W4-S007`)
- **Actor/role:** `KI-W4-WINDOW-AGENT` — executed the correction directly
  under requester instruction ("please correct it yourself and make it
  ready for S008"). This is a disclosed requester exception to the
  window-agent implementation-edit prohibition, mirroring the
  `EV-KI-R4-S01` waiver pattern: the requester owns the A5 boundary and
  authorized this single-file edit; no subagent was involved; the
  corrective scope equaled the §12.2 certificate exactly.
- **Prescribed-remedy falsification (recorded before acceptance):** the
  `EV-KI-W4-S11` remedy (direct `{ ownerId, ...payload }` spread) was
  applied first and then falsified by a service-level probe: a body
  `ownerId` silently **overwrites** the header identity because the
  service schema legitimately accepts `ownerId` as a service parameter —
  an owner-spoofing regression (`W4-NC15` class). The bytes of that
  intermediate state were discarded; the final correction below was
  verified instead. S3 remains append-only; this entry supersedes the
  `EV-KI-W4-S11` remedy text, which is hereby marked falsified.
- **Executed correction (from starting digest `77e364ca…`):** replaced the
  stripping helper with a rejecting helper —
  `keywordResearchBody(payload, allowedKeys)` throws
  `400 KEYWORD_RESEARCH_INPUT_INVALID` (with `unknownKeys` details) for any
  body key outside the frozen per-route contract
  (`["seeds"]` create; `["expectedRevision","items"]` selection;
  `["expectedSelectionRevision","clientRequestId"]` runs) and for
  non-object bodies; the three route call sites pass the cleaned body with
  route-injected identity. Missing/invalid known keys still 400 through
  the service strict schemas. Diff vs `6e6cdf3`: +18/−9, `server.js` only.
- **Verification battery:**
  1. `grep -c "function keywordResearchBody"` → `1`; three call sites use
     the frozen key lists; `node --check` → exit 0.
  2. HTTP-level probes (real `createLeadServer`, injected fake API,
     ephemeral listener): body `ownerId` → `400
     KEYWORD_RESEARCH_INPUT_INVALID`; unknown key `extra` → `400`; valid
     `{seeds}` → `202` with the service receiving `ownerId:"user_alice"`
     from the header only. Route-layer rejection proven; owner spoof
     impossible.
  3. `node --test test/server.test.js test/query-review-server.test.js` →
     16 tests, 16 pass, 0 fail, 0 skipped (legacy frozen).
  4. Write set: `git diff --stat 6e6cdf3` → exactly `src/server.js`;
     backend otherwise clean; frontend clean; root = inventory + three
     subordinate artifacts.
- **File-subwindow execution certificate (§12.3):** status
  `ACCEPTED_FOR_INTEGRATION` (window-agent self-executed under the
  requester exception); `starting_file_digest 77e364ca…`; `ending_file_digest
  f9947000fe3edcd2d582979ad155fb732e0abd40726baa241e75d9ca9eb2e428`;
  `attributable_changed_file_set [email_scraper/src/server.js]`;
  `required/registered/executed local cases []`; `negative_controls
  expected/falsified 0/0` (route-level negative control executes in
  `S009` `W4-S01`/`W4-NC15`); `deferred_integration_checks
  [KI-W4-V1..V4]`; `external_mutations []`; `successor_work_started
  false`; `direct_parent_communication false`.
- **Invalidation accounting:** no gate had run, so no gate is invalidated;
  `EV-KI-W4-S11` defect findings stand; its remedy text is superseded per
  the falsification note above.
- **Ending digest:** `f9947000fe3edcd2d582979ad155fb732e0abd40726baa241e75d9ca9eb2e428`
  (new `server.js` baseline; NOT yet committed — requester commits under
  the recorded policy).
- **Disposition:** `KI-W4-C001` CLOSED; `KI-W4-S007`
  `ACCEPTED_FOR_INTEGRATION` with corrected bytes; `KI-W4-S008`
  (manifest fixture) is the next assignable sub-window.

---

## `EV-KI-W4-S13` — Window-agent review of `KI-W4-S008` (ACCEPTED_FOR_INTEGRATION)

- **Timestamp:** 2026-08-18T22:06:01+05:30
- **Parent window / assignment / sub-window:** `KI-W4` / `ASG-KI-W4-WA-01` / `KI-W4-S008`
- **Actor/role:** `KI-W4-WINDOW-AGENT` (independent review, sub-window standard §8)
- **Handoff under review:** manifest fixture creation; requester commits
  `97d8a40` ("S007 corrections") and `5f91be7` ("S008").
- **Preliminary verification — C001 commit closure:** `97d8a40` touches
  exactly `src/server.js` (+18/−9 vs `6e6cdf3`) and the working-tree blob
  hashes to `f9947000fe3edcd2d582979ad155fb732e0abd40726baa241e75d9ca9eb2e428`
  — byte-identical to the `EV-KI-W4-S12` accepted correction ending
  digest. The pending-commit residual in S2 is cleared.
- **Verification battery for the fixture:**
  1. Baseline: fixture ABSENT at `6e6cdf3…` per the frozen S1 §5.8
     `starting_file_digest: ABSENT`; `git show 5f91be7 --name-only` →
     exactly the fixture path, +49/−0 (§8 items 1, 2 ✓).
  2. Byte-identity: `cmp` against the frozen deterministic rendering
     (764 bytes, 2-space JSON + one trailing LF) → identical; sha256 →
     `417f25dd2ab68c30a5ccfe19d3209afb4386435ef852f75dcf87af9f075b8c51`
     — equals the S1 §5.8 frozen digest (§8 items 4–6 ✓).
  3. C1 digest recomputation executed verbatim from S1 §5.8 → prints `OK`,
     exit 0: root exactly
     `{contractVersion:"ki-w4-enforcement-manifest-v1",groups}`, five
     groups with counts 8/6/8/6/6, 34 unique IDs, union digest
     `86810ce87a79426bb972be2e2827abc3806835190135d17769b52c33e7bb2203`
     under the normative sorted-member-plus-LF formula, rendering
     canonical (`JSON.stringify(m,null,2)+'\n'`) — `W4-C01` registration
     half complete (execution half owned by `S009`).
  4. Repositories: backend clean at `5f91be7…`; frontend clean; root =
     inventory + three subordinate artifacts (§8 items 2, 3 ✓).
  5. Coverage: `W4-C01` registered (0 local executions required by S1
     §5.8; V3 local = registration half) (§8 item 8 ✓).
  6. Intermediate state IS-4 respected: fixture present, unreferenced; no
     test edit; no successor work begun (§8 items 12, 13 ✓).
- **Ending digest:** `417f25dd2ab68c30a5ccfe19d3209afb4386435ef852f75dcf87af9f075b8c51`
  (fixture baseline; content frozen — any future edit requires a
  corrective sub-window).
- **External mutations:** none attributable to the leaf; commits are the
  requester's own under the recorded policy.
- **Disposition:** `ACCEPTED_FOR_INTEGRATION` — `KI-W4-S008` closed;
  `KI-W4-S009` (`keyword-intelligence-api.test.js`, the 28-ID non-DB
  registry) is the next assignable sub-window.

---

## `EV-KI-W4-S14` — Review of `KI-W4-S009`, correction `KI-W4-C002`, and acceptance

- **Timestamp:** 2026-08-18T22:36:48+05:30
- **Parent window / assignment / sub-window:** `KI-W4` / `ASG-KI-W4-WA-01` / `KI-W4-S009` (+ `KI-W4-C002`)
- **Actor/role:** `KI-W4-WINDOW-AGENT` (independent review §8; correction executed directly under requester instruction "please correct it youself so S010 can proceed" — same disclosed requester-exception pattern as `EV-KI-W4-S12`; no subagent involved; scope equaled the §12.2 certificate exactly)
- **Handoff under review:** `test/keyword-intelligence-api.test.js` creation;
  requester commit `6f03dbd` ("S009").
- **Conforming findings (verified):**
  1. Baseline: file ABSENT at `5f91be7…` per S1 §5.9; write set exactly the
     one new file, +1967/−0; backend/frontend clean; root = inventory +
     three subordinate artifacts.
  2. C1 `node --check` → exit 0. C2
     `node --test --test-isolation=none test/keyword-intelligence-api.test.js`
     → 33 tests, 33 pass, 0 fail, 0 skipped; exactly one
     `KI_W4_EXECUTION_CERTIFICATE=` line; certificate shows 28 required =
     28 registered = 28 executed (UTF-8 sorted), `skipped: []`,
     `oracleFailures: []`, activation witnesses for all 28.
  3. Certificate honesty independently recomputed: fixture-derived 28-ID
     union (34 minus `handoff_database`) digest =
     `380fafb07d397522527ad24266c55ca185077b780ed9ef8052d7b000fd8dfaba` —
     equals the certificate's required/registered/executed digests; the
     34-ID global digest remains `86810ce8…`.
  4. Controls (`W4-C04`): harness runs each control as clean oracle →
     defective oracle must throw `AssertionError` → fresh clean oracle;
     defects are injected into fake collaborators/in-memory evidence only;
     `W4-NC01`–`W4-NC18` all present; completion asserts
     `controlsFalsified.size === 18` plus production-source digest
     invariance across the seven read-only production paths. `W4-NC05`
     proves the `RunHandoffAbort` sentinel requirement (partial-commit
     normal-return is rejected). `W4-NC15` covers auth/path/body-owner
     strictness including the corrected rejecting helper.
  5. Server group (`W4-S01`–`S06`): real `createLeadServer` with injected
     fake API and fake repository on an ephemeral `127.0.0.1` listener,
     `closeAllConnections` + close in `finally`; statuses/headers/bodies
     asserted per the A4 matrix; zero external calls.
  6. `W4-C05`/`W4-C06`: substitute fidelity assertions are exact-claim;
     prohibited-import regex over all imports passes; no external package
     imports; fixture byte-exactness and symbol presence re-verified.
  7. Group order `api_component → server_routes → query_review →
     conformance` per `I-F9`.
- **Defect found (correction trigger):** `W4-C06` ended with
  `assert.equal(absent, true, "DB handoff registry is not yet authored at
  this leaf")` — an absence assertion on
  `test/keyword-intelligence-handoff.integration.test.js`. True at this
  leaf, but `KI-W4-V2` re-runs this file at I001 on the final tree where
  the S010 file exists, so the gate would fail deterministically. The
  absence check was a leaf addition beyond S1 §5.9 (which requires only
  import/symbol inspection).
- **Root cause:** an intermediate-state condition (file not yet authored)
  was hardened into a permanent oracle instead of a state-robust check.
- **Corrective readiness certificate (§12.2):** certificate
  `CORRECTIVE-SUBWINDOW-READY`; `corrective_subwindow_id: KI-W4-C002`;
  `trigger_evidence [EV-KI-W4-S14]`; `root_cause` as above; governing
  `REQ-KI-019`/`DEC-KI-033`; `corrected_prior_subwindows [KI-W4-S009]`;
  `writable_file email_scraper/test/keyword-intelligence-api.test.js`;
  `starting_file_digest
  d4f91270d7b4d7c12c2de1433332d38e62823a9e9be3a47ccb0b08cc9a1f7b94`;
  `predecessors [KI-W4-S009]`; `invalidated_evidence []`;
  `invalidated_gates []` (V2 has not run; it will run on corrected bytes);
  `expanded_parent_scope_required false`; `section_7_fields_complete true`;
  `single_file_write_set true`; `next_integration_assessment_id KI-W4-I001`;
  `status READY`.
- **Executed correction:** replaced the absence assertion with a
  state-robust check — when the DB registry file exists it must contain
  `ALLOW_DATABASE_TESTS` and all six `W4-D01`–`W4-D06` registrations; when
  absent the check passes (intermediate state). Diff: +7/−1, one file.
- **Post-correction verification:** C1 exit 0; C2 → 33/33 pass, 0 skipped,
  certificate unchanged in content (28=28=28); working-tree write set
  exactly the one file; frontend clean; root = inventory + three
  subordinate artifacts.
- **File-subwindow execution certificate (§12.3, window-agent self-executed
  under the requester exception):** `starting_file_digest d4f91270…`;
  `ending_file_digest
  09e9235810a767bb4173a41a139b66f5cfe81c7a70ebddaf21773a78abc2aea0`;
  `attributable_changed_file_set
  [email_scraper/test/keyword-intelligence-api.test.js]`;
  `required/registered/executed local cases [28 non-DB IDs]`;
  `negative_controls expected/falsified 18/18`; `deferred_integration_checks
  [KI-W4-V2 re-run on final tree]`; `external_mutations []`;
  `successor_work_started false`; `direct_parent_communication false`.
- **Ending digest:** `09e9235810a767bb4173a41a139b66f5cfe81c7a70ebddaf21773a78abc2aea0`
  (NOT yet committed — requester commits under the recorded policy; S010
  may proceed against the corrected tree because its single-file invariant
  is unaffected).
- **Disposition:** `KI-W4-C002` CLOSED; `KI-W4-S009`
  `ACCEPTED_FOR_INTEGRATION`; `KI-W4-S010`
  (`keyword-intelligence-handoff.integration.test.js`) is the next
  assignable sub-window.

---

## `EV-KI-W4-S15` — Window-agent review of `KI-W4-S010` (ACCEPTED_FOR_INTEGRATION)

- **Timestamp:** 2026-08-18T23:06:31+05:30
- **Parent window / assignment / sub-window:** `KI-W4` / `ASG-KI-W4-WA-01` / `KI-W4-S010`
- **Actor/role:** `KI-W4-WINDOW-AGENT` (independent review, sub-window standard §8)
- **Handoff under review:** `keyword-intelligence-handoff.integration.test.js`
  creation; requester commits `1ec1ab8` ("S009 - correction") and
  `fac5bb0` ("S010").
- **Preliminary verification — C002 commit closure:** `1ec1ab8` touches
  exactly `test/keyword-intelligence-api.test.js` (+8/−1 vs `6f03dbd`);
  working-tree digest `09e92358…` equals the `EV-KI-W4-S14` accepted
  correction ending digest. Pending-commit residual cleared.
- **Verification battery:**
  1. Baseline: file ABSENT at `6f03dbd…` per S1 §5.10; `fac5bb0`
     adds exactly the one new file (+662/−0); backend clean at `fac5bb0`;
     frontend clean; root = inventory + three subordinate artifacts (§8
     items 1–3 ✓).
  2. C1 `node --check` → exit 0; C2 `grep -c "W4-D0"` → 7 line hits, six
     unique IDs `W4-D01`–`W4-D06` (2 occurrences each: registration list +
     case body) (§8 item 7 ✓).
  3. Harness structure audited against S1 §5.10/A4: one outer registry test
     creates exactly one disposable schema (`kiw4_handoff_<time>_<pid>`)
     through the accepted `createIsolatedTestSchema` +
     `deployPrismaMigrations` + `assertMigrationStayedInSchema` primitives
     (non-pooled scoped URL; never `public`); six sequential named subtests
     in manifest order via `await t.test(id, …)`; `finally` drops that
     exact schema with CASCADE, proves schema-name absence through a
     parameterized `information_schema` query, and disconnects; no shared
     or cross-test cleanup (§8 items 4, 5 ✓).
  4. Case bodies audited against A4 lines 2151–2156: `W4-D01` N=1 then
     N=100 with an operation spy proving exactly the five named
     transaction operations in order (`keywordResearch.findUnique`,
     `keywordResearchHandoff.findUnique`, `run.create`,
     `runQuery.createMany`, `keywordResearchHandoff.create`), full run-row
     field assertions (state/phase/stage/queryRevision=1/lease
     nulls/snapshot byte-deep-equal), query lineage and pending probe
     state; `W4-D02` injected throws at `run.create` and
     `runQuery.createMany` escape after rollback plus both invalid
     callback outputs map to `KEYWORD_RUN_HANDOFF_INVALID`, with
     `assertZeroPartial` (0 runs, 0 queries, 0 handoffs, research intact)
     at all four positions; `W4-D03` exercises all three pre-write
     conflict predicates — owner B → `not_found`, stale revision →
     `KEYWORD_SELECTION_REVISION_CONFLICT`, not-completed draft →
     `KEYWORD_RESEARCH_NOT_COMPLETED` — each with zero writes (the
     repository exposes exactly these three; recorded as the
     interpretation of "conflicted canonical draft"); `W4-D04` concurrent
     equal key+fingerprint via `Promise.allSettled` (unique fence
     tolerates the loser; exactly one Run/handoff survives), identical
     retry → `found` with the same Run, unequal fingerprint and unequal
     revision → conflicts, no second Run; `W4-D05` post-handoff
     `saveSelection` revision advance cannot alter the run snapshot
     (deep-equal pre-edit snapshot, frozen `keywordSelectionRevision`,
     unchanged item lineage, exactly N links, text-only change);
     `W4-D06` legacy create/load/edit with `user_added` row and null
     lineage, plus 100-row handoff (five named ops, one bulk insert) and
     100-row research edit with bounded-read accounting (zero per-row
     `runQuery.find*`, one `run.findFirst`, one terminal `run.findUnique`,
     one CAS `updateMany`, one `deleteMany`, one `createMany`) (§8 item 4
     ✓).
  5. Failure-capture design: subtest failures rethrow inside the subtest
     and are recorded in `oracleFailures`; the certificate test hard-fails
     on any failure/skip when enabled — no swallowable failure path.
  6. Opt-in gate: `ALLOW_DATABASE_TESTS === "true"`; disabled-mode run
     executed locally (safe, no database): registry test SKIPs, the
     certificate test passes and emits exactly one
     `KI_W4_EXECUTION_CERTIFICATE=` line with `registry:"database"`, all
     six IDs in `skipped`, and `required` digest
     `af09edaad950a39f35356708592fcd36f9bbad437cd50468a90d259220a9ae44`
     — independently recomputed equal to the F-D2 digest of the six-ID
     set (§8 items 7, 11 ✓).
  7. Coverage: `W4-D01`–`D06` registered (6/6); execution
     `DEFERRED_TO_INTEGRATION` to `KI-W4-I001` gate `KI-W4-V3` — the leaf
     did not run the database suite, exactly as prescribed (§8 item 8 ✓;
     intermediate state IS-6 respected).
  8. Imports: no external packages; no production mutation; one schema
     lifecycle; no second database; no cross-test schema reuse (§8 items
     5, 9 ✓). No successor work begun (§8 items 12, 13 ✓).
- **Ending digest:** `2a17aa562893c294a5f027ce074df17695cc4e6c156addcdc1af3522b6ada75c`
  (DB-registry baseline).
- **External mutations:** none attributable to the leaf; commits are the
  requester's own under the recorded policy.
- **Disposition:** `ACCEPTED_FOR_INTEGRATION` — `KI-W4-S010` closed. All
  ten file sub-windows are accepted; the next and final step inside the
  window is `KI-W4-I001` (window-agent integration assessment: gates
  `KI-W4-V1`, `V2`, `V3`, `V4`, then the `KI-W4-V6` merge; `V3` requires
  the requester's isolated non-production database opt-in).

---

## `EV-KI-W4-I01` — `KI-W4-I001` integration assessment (all gates PASS) and window closure

- **Timestamp:** 2026-08-18T23:10:52+05:30
- **Parent window / assignment / sub-window:** `KI-W4` / `ASG-KI-W4-WA-01` / `KI-W4-I001`
- **Actor/role:** `KI-W4-WINDOW-AGENT` (personally executed; sub-window standard §9, `SW-V08`)
- **Frozen inputs:** backend HEAD `fac5bb0f0a4e9c04873c9d338794762d44e35f7f`, tree
  clean; frontend `0dfa1acac50fac3a86d02ec674c6d2bab645832d`, clean; root =
  §2 inventory + the three subordinate artifacts (36 paths). No source
  change occurred between gates.
- **`KI-W4-V1` (assembled write-set) — PASS:**
  `git diff --name-status d98ad53c…fac5bb0` lists exactly the ten planned
  paths (6 `M`, 4 `A`, no other file); the sorted per-LF digest over the
  workspace-canonical paths (`email_scraper/` prefix) equals
  `fe48d14ebec1dffa058cf91cfa9ec10982d4ceaa4c63e0cb9280cabf39a4a59b`.
  Recording note: an intermediate digest `f0081f3f…` computed without the
  canonical prefix was rejected and recomputed — the frozen formula uses
  workspace-canonical paths (S1 §2 table).
- **`KI-W4-V2` (non-DB registry, once) — PASS:**
  `node --test --test-isolation=none test/keyword-intelligence-api.test.js`
  → 33 tests, 33 pass, 0 fail, 0 skipped. The `W4-C06` state-robust check
  passed against the now-existing S010 file, validating `KI-W4-C002` at
  gate level. The certificate line (deterministic; verified byte-identical
  in the `EV-KI-W4-S14` review runs and implied by the passing
  certificate test) carries 28 required = 28 registered = 28 executed,
  digests `380fafb07d397522527ad24266c55ca185077b780ed9ef8052d7b000fd8dfaba`.
- **`KI-W4-V3` (database registry, once, isolated opt-in) — PASS:** run
  with `ALLOW_DATABASE_TESTS=true` and the requester-provided
  `TEST_DATABASE_URL` from `email_scraper/.env` (loaded without printing;
  the accepted helper `resolveDirectTestDatabaseUrl` asserted the
  test-database identity differs from `DATABASE_URL` and the endpoint is
  not pooled; a benign `.env` line-25 shell notice about an unquoted value
  did not affect loading). Result: 8 tests, 8 pass, 0 fail, 0 skipped;
  `W4-D01`–`D06` executed sequentially in one disposable schema
  (`kiw4_handoff_<time>_<pid>`), migrations deployed inside the schema,
  `assertMigrationStayedInSchema` held, and the `finally` block dropped
  the schema and proved its absence. Certificate verbatim (captured to
  `v3-output.txt`): `registry:"database"`, 6 required = 6 registered =
  6 executed, `skipped: []`, `oracleFailures: []`, all digests
  `af09edaad950a39f35356708592fcd36f9bbad437cd50468a90d259220a9ae44`.
- **`KI-W4-V4` (regression + secrets, once each) — PASS:** `npm test` →
  729 tests, 661 pass, 0 fail, 68 skipped (every skip a guarded database
  opt-in in disabled mode, including the DB registry's disabled-mode run;
  no localhost sandbox failure occurred); `npm run check:secrets` →
  "Secret scan passed; no credential-shaped assignments found."
- **`KI-W4-V6` (global merge) — PASS:** union of the non-DB executed set
  (28) and the database executed set (6) equals the manifest's required
  set exactly (34 unique); sorted per-LF union digest equals
  `86810ce87a79426bb972be2e2827abc3806835190135d17769b52c33e7bb2203`;
  zero skips and zero oracle failures in both inputs; required =
  registered = executed globally.
- **Coverage accounting (final):** required 34 = registered 34 = executed
  34; controls 18/18 falsified (`W4-C04`); activation witnesses 34/34;
  zero skip/duplicate/unexpected/filtered/unactivated members.
- **External mutations:** exactly the authorized test-run footprint — one
  disposable PostgreSQL schema created and dropped inside the isolated
  non-production test database (absence proven); no provider, AWS, queue,
  bucket, or production-database action; no commit (requester-owned).
- **Residuals for parent review:** (1) A5 A3/A4 pins were refreshed by the
  parent at state 101 (`EV-KI-A-039`/`CHG-KI-017`) — closed;
  (2) `W4-D03` "conflicted canonical draft" maps to the repository's
  not-completed predicate (recorded in `EV-KI-W4-S15`); (3) `.env`
  line 25 contains an unquoted value with spaces (benign shell notice when
  sourcing; no product effect; flagged for the requester only).
- **Window-agent integration certificate (§12.4):**

  ```yaml
  certificate: WINDOW-INTEGRATION-COMPLETE
  parent_window_id: KI-W4
  parent_assignment_id: ASG-KI-W4-WA-01
  window_agent_identity: KI-W4-WINDOW-AGENT
  assessment_id: KI-W4-I001
  accepted_file_subwindows: 10
  corrective_subwindows: [KI-W4-C001, KI-W4-C002]
  gates:
    KI-W4-V1: PASS
    KI-W4-V2: PASS
    KI-W4-V3: PASS
    KI-W4-V4: PASS
    KI-W4-V6: PASS
  assembled_changed_file_set_digest: fe48d14ebec1dffa058cf91cfa9ec10982d4ceaa4c63e0cb9280cabf39a4a59b
  coverage_required: 34
  coverage_registered: 34
  coverage_executed: 34
  coverage_skipped: 0
  manifest_digest: 86810ce87a79426bb972be2e2827abc3806835190135d17769b52c33e7bb2203
  backend_head: fac5bb0f0a4e9c04873c9d338794762d44e35f7f
  frontend_head: 0dfa1acac50fac3a86d02ec674c6d2bab645832d
  unresolved_blockers: []
  expanded_parent_scope_required: false
  status: READY_FOR_PARENT_REVIEW
  ```

- **Disposition:** `KI-W4-I001` PASSED; all ten file sub-windows and both
  corrections accepted; the `KI-W4` window is complete from the window
  agent's side. S2 set to `READY_FOR_PARENT_REVIEW`. Per §12.5/§13 and the
  A5 boundary, the window agent claims no parent acceptance and begins no
  `KI-W5` work; the consolidated handoff accompanies this entry.
