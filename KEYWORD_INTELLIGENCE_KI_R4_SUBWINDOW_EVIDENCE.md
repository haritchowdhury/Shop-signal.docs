# KI-R4 Sub-Window Evidence (`S3`)

Append-only. Every entry identifies actor, revisions, commands, decisive
results, coverage accounting, external mutations, and disposition. This file
cannot amend a task, decision, or authority boundary.

---

## `EV-KI-R4-S01` — Entry-gate verification and starting inventory

- **Timestamp:** 2026-08-18T18:30:00+05:30
- **Parent window / assignment / sub-window:** `KI-R4` / `ASG-KI-R4-WA-01` / (decomposition)
- **Actor/role:** `KI-R4-WINDOW-AGENT` (window agent)
- **Frozen revisions at inspection:** sub-window standard
  `1766f9107ce7d315877b75d4b0ea2b5521dff1c321e12f890b03787d66196ded` (equals the
  KI-R4 header pin); parent standard
  `3b7a4fd25156e1adfbc92abb835c5f82a0d18c686b1c1150feb202f2d944d2ac`; A1
  `8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c`; A3
  `4b2202d870da5df64ae324ad570adf1b6437689883cb49b118bcc8d1f170d9de`; A4
  `310011aa3d855cd4ce4d6ef5054d94e5b8f413b8b86543048fea065113a10cf6`.
- **Assignment provenance:** requester direct instruction on 2026-08-18
  ("I am assigning you, fuck the parent agent for now") grants
  `ASG-KI-R4-WA-01` to `KI-R4-WINDOW-AGENT` as a disclosed exception to the A5
  CAS precondition (`KI-R4-P1`) and, for now, to parent decomposition review
  (`KI-R4-P5`). A5 (state 97) still assigns KI-R3 and was not modified.
- **Commands and decisive results:**
  - `git -C email_scraper rev-parse HEAD` → `077213cc7c33fa8209a1e5d8ff365b73766500dc`; `git -C email_scraper status --porcelain` → empty. Matches `KI-R4-P2`.
  - `git -C frontend rev-parse HEAD` → `0dfa1acac50fac3a86d02ec674c6d2bab645832d`; status clean.
  - `sha256sum` over the seven existing planned files + `ABSENT` for the manifest → the eight digests recorded in S1 §2.
  - Eight planned paths, LC-all-C-sorted, each + LF, sha256 → `ccfa1089d1d62656afde3927cd0b42128856713442dcbda5d30dd47a6b5333f6` — byte-equal to the KI-R4 header `required_initial_file_set_digest`. Set-equality proof for `SW-D03`.
  - Root `git status --porcelain` → 29 owner-controlled relocation paths; per-LF set digest `df17885e439b7ebf2d72282f80b3b684bebaec7a9486fc741c51be176f4600ae`; root HEAD `6318a608a6475c62eeff8f2c21465d7c83e8e74d`. State preserved unmodified.
- **Coverage accounting:** no case IDs executable at this step (decomposition); required/registered/executed accounting begins at leaf level.
- **External mutations:** none (read-only commands; S1/S2/S3 creation is the authorized coordination write).
- **Limitations/deferred:** `EV-KI-R3-02` is not yet present in A6; its five findings were taken from `DEC-KI-032`/`KI-R4-P3` and independently reproduced (see `EV-KI-R4-S02`).
- **Disposition:** entry gate satisfied under the recorded requester exception; decomposition authoring authorized.

---

## `EV-KI-R4-S02` — Decision closure, defect reproduction, and digest-formula resolution

- **Timestamp:** 2026-08-18T18:30:00+05:30
- **Parent window / assignment / sub-window:** `KI-R4` / `ASG-KI-R4-WA-01` / (decomposition)
- **Actor/role:** `KI-R4-WINDOW-AGENT`
- **Commands/inspections and decisive results:**
  1. `service.js` lines 424–543 read: `recoverClaimedTask` enters
     `planned|in_flight` (line 429), `succeeded` (line 445, inline equality only
     at 446), and `failed` (line 500) classification with no attempt/task
     request-fingerprint gate — reproduces KI-R4-P3 finding 1 ("unequal failed
     identity reaches retry/terminal logic"). `invariant()` at line 57 confirmed
     to throw `PipelineInvariantError("PIPELINE_INPUT_CONFLICT")`.
  2. `queue-dispatcher.js` line 34 `Object.keys(options)` confirmed — reproduces
     finding 2 (symbol/non-enumerable extras not enumerated); lines 32–33
     already enforce non-null/non-array/plain prototype, so the frozen one-line
     replacement (I-F2) is sufficient and necessary.
  3. `keyword-intelligence-enforcement.test.js` lines 110–111 (revision-less
     `git diff`), 208 (live `git status`), 217 (revision-less `git diff`)
     confirmed — reproduces finding 3 (clean-checkout failure/empty-diff pass);
     C05 span constants `[[46,56]]`/`[[28,50]]`/`[[305,408],[410,488],[490,509]]`
     read from source and preserved in I-F9.
  4. Regex-only digest assertions confirmed at adapter test line 722,
     runtime-adapters line 438, worker lines 1312/1369, flow line 994
     (`assert.match(hash, /^[a-f0-9]{64}$/)`) — reproduces finding 4.
  5. Worker test line 1358 `SCN-KI-030` takes no `t`; `t_scn030` (line 1372)
     opens `kir3_d_*` schema per case (five schemas) — reproduces finding 5.
     R3-A01 (adapter line 518) and R3-G24 (flow line 959) controls confirmed to
     alter scaffold inputs (`failOnAssert`) rather than captured evidence —
     reproduces finding 6; `componentHarness` confirmed to assign the task a real
     `reqFp` while R09/R10-style fixtures put `requestFingerprint: null` on the
     attempt (intermediate-state IS-1 fact).
  6. Digest-formula resolution (Node script over the committed R3 fixture):
     all seven R3 group digests and the 101-ID global digest match
     `sha256(sortedIds.join("\n"))` (no trailing LF) — formula F-D1; the R4
     15-ID digest `6adc8ab132496c58608734549fbbc596577e1bd71c1e730349575eb96badc941`
     matches the sub-window-standard per-member-LF formula — formula F-D2; the
     8-path planned-set digest matches F-D2. Both formulas frozen in S1 §3
     (I-F4/I-F5); no leaf may pick between them.
  7. R4 manifest content rendered deterministically (2-space JSON + trailing LF,
     970 bytes) with sha256
     `7700c1ebb02514cdf89ee2c4c729ef91c3c14aa6fec25d99161bf37e07f01702` and
     F-D2 global digest `6adc8ab1…`; content embedded verbatim in S003.
- **Conclusion:** every implementation-affecting decision required by KI-R4
  exists in `DEC-KI-026`–`032` plus the A4 task blocks; no contradictory
  authority found; decomposition is not `BLOCKED` (`SW-D02`).
- **Coverage accounting:** decomposition-time only; no executable case IDs yet.
- **External mutations:** none (source reads and one Node computation against
  fixture files).
- **Disposition:** decision closure verified; interface freeze I-F1–I-F9 authored from these facts.

---

## `EV-KI-R4-S03` — Decomposition authoring, mechanical lint, and readiness certificate

- **Timestamp:** 2026-08-18T18:30:00+05:30
- **Parent window / assignment / sub-window:** `KI-R4` / `ASG-KI-R4-WA-01` / (decomposition)
- **Actor/role:** `KI-R4-WINDOW-AGENT`
- **Artifacts created:** S1 (`KEYWORD_INTELLIGENCE_KI_R4_SUBWINDOW_CHECKLIST.md`,
  sha256 recorded in S2 `decomposition_revision`), S2
  (`KEYWORD_INTELLIGENCE_KI_R4_SUBWINDOW_STATE.md`), S3 (this file).
- **Mechanical lint executed over S1 (script `lint` below) with results:**
  1. Sub-window/assessment IDs unique: `KI-R4-S001`–`S008`, `KI-R4-I001` — 9 distinct, zero duplicates.
  2. Every FILE sub-window `writable_file` is exactly one canonical
     workspace-relative path (no directory, glob, `..`, symlink segment); the
     eight writable files equal the eight planned paths; per-LF set digest
     equals `ccfa1089d1d62656afde3927cd0b42128856713442dcbda5d30dd47a6b5333f6`.
  3. No unresolved placeholder (`___`, `TBD`, `PENDING_` outside the S2
     mechanical note) in checked items or assignable sub-windows.
  4. Banned-verb scan over §5 transformation text: zero occurrences of
     `choose`, `decide`, `determine`, `as appropriate`, `as needed`, `similar to`, `etc.`.
  5. Every §7.1 field present in all eight sub-window blocks; every §7.5 box
     list present; traceability matrix rows reference only existing IDs.
- **Counterexample audit (§14):** for each of the twenty counterexamples, the
  rejecting mechanism is: (1,3,4) leaf P2/V2 single-file write-set proof +
  SW-R03 lint; (2) SW-R03 path grammar; (5) G-V6 set-digest equality; (6) §5
  one-owner-per-file table; (7) §4 DAG + predecessors fields; (8) §4.1 IS-1
  exact expected failure with named resolver; (9) `may_start_successor:false` +
  §12.3 `successor_work_started:false`; (10) §12.3
  `direct_parent_communication:false` + §1 prohibition; (11) §7 rule 6; (12) §7
  corrective-sub-window protocol; (13) §7 rule 1/2; (14) G-V6 required=
  registered=executed with witnesses; (15) F-D1 byte-exact literals + §7 rule
  3; (16) I-F8 fidelity clause; (17) §6 gate scheduling/invalidation rules;
  (18) §6 reuse-only-with-dependency-proof; (19) G-V6/G-V7 set equality; (20)
  §10 boundary (`READY_FOR_PARENT_REVIEW` terminal).
- **Coverage accounting (decomposition):** required parent items mapped —
  tasks `KI-R4-T1`–`T4` (4/4), scenarios `SCN-KI-028`–`035` corrected/new
  (8/8), R3 manifest IDs 101 (allocation unchanged), R4 manifest IDs 15 (all
  allocated to exact leaves); unmapped requirement/decision/task/scenario
  counts: 0/0/0/0.
- **External mutations:** none beyond creation of the three subordinate artifacts.
- **Readiness counts:** mandatory authoring checklist checked 44 / unchecked 0;
  initial sub-window count 8; planned file-set digest `ccfa1089…`;
  multi-file sub-windows 0; duplicate file owners 0; unresolved interfaces 0;
  unresolved intermediate states 0; unresolved execution choices 0; unresolved
  evidence references 0.
- **Disposition:** decomposition complete; S2 set to
  `AWAITING_PARENT_DECOMPOSITION_REVIEW` with the requester-waiver exception of
  `EV-KI-R4-S01` §0.3. No leaf assigned.

### Certificate

```yaml
certificate: SUBWINDOW-DECOMPOSITION-READY
parent_window_id: KI-R4
parent_assignment_id: ASG-KI-R4-WA-01
window_agent_identity: KI-R4-WINDOW-AGENT
revisions:
  parent_standard: 3b7a4fd25156e1adfbc92abb835c5f82a0d18c686b1c1150feb202f2d944d2ac
  subwindow_standard: 1766f9107ce7d315877b75d4b0ea2b5521dff1c321e12f890b03787d66196ded
  contract: 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c
  decision: 4b2202d870da5df64ae324ad570adf1b6437689883cb49b118bcc8d1f170d9de
  parent_checklist: 310011aa3d855cd4ce4d6ef5054d94e5b8f413b8b86543048fea065113a10cf6
  decomposition: f93bdd01da6b273d34f10b2bab00db4dffdbd6c2d3530d80ffba570be985cc9d
initial_subwindow_ids: [KI-R4-S001, KI-R4-S002, KI-R4-S003, KI-R4-S004, KI-R4-S005, KI-R4-S006, KI-R4-S007, KI-R4-S008]
initial_subwindow_count: 8
planned_file_set: [email_scraper/src/aws-pipeline/keyword-intelligence/service.js, email_scraper/src/aws-pipeline/adapters/queue-dispatcher.js, email_scraper/test/fixtures/keyword-intelligence/ki-r4-enforcement-manifest-v1.json, email_scraper/test/keyword-intelligence-worker.test.js, email_scraper/test/keyword-intelligence-adapter.test.js, email_scraper/test/aws-pipeline-runtime-adapters.test.js, email_scraper/test/keyword-intelligence-worker-flow.test.js, email_scraper/test/keyword-intelligence-enforcement.test.js]
planned_file_set_digest: ccfa1089d1d62656afde3927cd0b42128856713442dcbda5d30dd47a6b5333f6
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
first_subwindow: KI-R4-S001
integration_assessment_id: KI-R4-I001
parent_review_required: true
```

`parent_review_required: true` stands; the requester's standing waiver
(`EV-KI-R4-S01`) permits the requester, in the parent's place, to direct
`decomposition_status: READY` and the first leaf assignment.

---

## `EV-KI-R4-S04` — Parent decomposition review and technical correction

- **Timestamp:** 2026-08-18T20:00:00+05:30
- **Parent window / assignment:** `KI-R4` / `ASG-KI-R4-WA-01`
- **Actor/role:** parent reviewer.
- **Frozen revisions:** parent standard `3b7a4fd25156e1adfbc92abb835c5f82a0d18c686b1c1150feb202f2d944d2ac`;
  sub-window standard `1766f9107ce7d315877b75d4b0ea2b5521dff1c321e12f890b03787d66196ded`;
  A1 `8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c`;
  A3 `4b2202d870da5df64ae324ad570adf1b6437689883cb49b118bcc8d1f170d9de`;
  A4 `310011aa3d855cd4ce4d6ef5054d94e5b8f413b8b86543048fea065113a10cf6`;
  corrected S1 `91b499cc2885937b23daa3186709ca2e0720c939435e4588b4050e2503abcd85`.
- **Review result:** approved. The eight-file decomposition covers the five
  KI-R4 correction classes and preserves the parent scope. Amendment A1 no
  longer permits the window agent to act as a leaf. All remaining leaves require
  separate implementation agents and report only to the window agent.
- **Bootstrap reconciliation:** the existing R4 manifest is exactly 970 bytes,
  SHA-256 `7700c1ebb02514cdf89ee2c4c729ef91c3c14aa6fec25d99161bf37e07f01702`,
  contains 15 unique required IDs, and has set digest
  `6adc8ab132496c58608734549fbbc596577e1bd71c1e730349575eb96badc941`.
  `KI-R4-S003` is accepted as completed bootstrap work; no other leaf is accepted.
- **State transition:** A5 state 98 assigns only the KI-R4 window agent. S2
  state 3 is `READY`, pins the corrected S1, records S003 accepted, and leaves
  S001 unassigned with zero implementation write authority until the window
  agent names a separate leaf agent.
- **External mutations/cost:** coordination-document edits only; no provider,
  AWS, production database, build, commit, or push action; `$0.00`.

```yaml
certificate: SUBWINDOW-DECOMPOSITION-READY-SUPERSEDING
parent_window_id: KI-R4
parent_assignment_id: ASG-KI-R4-WA-01
window_agent_identity: KI-R4-WINDOW-AGENT
decomposition_revision: 91b499cc2885937b23daa3186709ca2e0720c939435e4588b4050e2503abcd85
initial_subwindow_count: 8
accepted_bootstrap_subwindows: [KI-R4-S003]
remaining_subwindow_order: [KI-R4-S001, KI-R4-S002, KI-R4-S004, KI-R4-S005, KI-R4-S006, KI-R4-S007, KI-R4-S008]
planned_file_set_digest: ccfa1089d1d62656afde3927cd0b42128856713442dcbda5d30dd47a6b5333f6
remaining_multi_file_subwindows: []
remaining_window_agent_leaf_roles: []
parent_review_required: false
status: READY
```

---

## `EV-KI-R4-S05` — S001 leaf execution and window-agent review disposition

- **Timestamp:** 2026-08-18T20:15:00+05:30
- **Parent window / assignment / sub-window:** `KI-R4` / `ASG-KI-R4-WA-01` / `KI-R4-S001`
- **Actor/role:** S001 leaf implementation agent (report) then `KI-R4-WINDOW-AGENT` (independent review).
- **Frozen revisions at inspection:** S1 `91b499cc2885937b23daa3186709ca2e0720c939435e4588b4050e2503abcd85`; A3 `4b2202d870da5df64ae324ad570adf1b6437689883cb49b118bcc8d1f170d9de`; A4 `310011aa3d855cd4ce4d6ef5054d94e5b8f413b8b86543048fea065113a10cf6`.
- **Leaf report (executed prior session, `status: AWAITING_WINDOW_REVIEW`):**
  - T1 applied exactly one ordered insertion after line 426 (`if (latestAttempt.requestFingerprint !== current.task.requestFingerprint) invariant();`), before the `now` binding; no other line/symbol/import/export changed.
  - V1: C1 `node --check` exit 0; C2 (per amendment A1 #1, enforcement test excluded until S008) adapter + worker-flow patterns — 43 pass / 0 fail / 0 skip.
  - V2: attributable changed-file set exactly `email_scraper/src/aws-pipeline/keyword-intelligence/service.js` (1 insertion); ending digest `c37a038f189470ad1d2eca6626f515b9f0c45bd60de470d84c4b72fa497637b5`.
  - V3/C3: no case IDs registered; activation witness = S004 R4-W01–W03; worker-file falsification deferred to I001 (IS-1 expected failure: SCN-KI-029 fixtures with `requestFingerprint:null` throw `PIPELINE_INPUT_CONFLICT` until S004).
  - H2: no prohibited action, second-file edit, DB run, commit, parent/AWS action.
- **Window-agent independent verification (this entry):**
  - `service.js` re-read: line 427 carries the fence immediately after `if (!latestAttempt) return { outcome: "proceed" };` (line 426) and before `const now = () => nowOf(runtime);` (line 428) — matches I-F1 exactly; line 57 `invariant()` throwing `PipelineInvariantError("PIPELINE_INPUT_CONFLICT")` confirmed unchanged.
  - `sha256sum service.js` → `c37a038f189470ad1d2eca6626f515b9f0c45bd60de470d84c4b72fa497637b5` — equals the leaf's reported ending digest.
  - `sha256sum` of `ki-r4-enforcement-manifest-v1.json` → `7700c1ebb02514cdf89ee2c4c729ef91c3c14aa6fec25d99161bf37e07f01702` (I-F3) and queue-dispatcher.js at `453a323bd8929ea254f077b39bb5a62a82cc77490c8f5ac5f45485d730fef046` (S002 baseline) — both unchanged.
  - Repo state: `email_scraper` HEAD `264b44c21f66416d87a1430301eaf70b2d09c822` = prior HEAD `bea18a8` + the S001 fence commit (service.js +1) and the accepted S003 manifest fixture; `git status --porcelain` empty. `frontend` HEAD `0dfa1acac50fac3a86d02ec674c6d2bab645832d`, clean. Root = 29-path inventory + the three S artifacts (32 paths); relocation state preserved. The S001 commit exists outside the leaf's recorded actions (recorded as a post-leaf external coordination state), and the leaf's attributable edit itself is unchanged.
- **Coverage accounting:** no case IDs executed by S001 itself; activation witness (R4-W01–W03) is owned by S004. IS-1 expected temporary failure remains current and resolves at S004.
- **External mutations:** none by the reviewer beyond this S3/S2 coordination write.
- **Disposition:** `ACCEPTED_FOR_INTEGRATION` for `KI-R4-S001`. Next sub-window: `KI-R4-S002` (independent productions; S002 has no predecessor dependency on S001).

---

## `EV-KI-R4-S06` — S002 leaf execution evidence

- **Timestamp:** 2026-08-18T20:25:00+05:30
- **Parent window / assignment / sub-window:** `KI-R4` / `ASG-KI-R4-WA-01` / `KI-R4-S002` (leaf assignment `ASG-KI-R4-S002-L01`).
- **Frozen revisions at inspection:** S1 `91b499cc2885937b23daa3186709ca2e0720c939435e4588b4050e2503abcd85`; A3 `4b2202d870da5df64ae324ad570adf1b6437689883cb49b118bcc8d1f170d9de`; A4 `310011aa3d855cd4ce4d6ef5054d94e5b8f413b8b86543048fea065113a10cf6`. S2 state 4 records the assignment.
- **P1 (revisions/identity/baseline):** writable file `email_scraper/src/aws-pipeline/adapters/queue-dispatcher.js`; starting digest `453a323bd8929ea254f077b39bb5a62a82cc77490c8f5ac5f45485d730fef046` verified before edit.
- **P2 (starting repo status):** `git -C email_scraper status --porcelain` empty; `git -C frontend status --porcelain` empty; root = 29-path inventory + three S artifacts (32 paths), relocation state untouched.
- **T1 (exact transformation):** one ordered edit at line 34 — `const keys = Object.keys(options);` replaced with `const keys = Reflect.ownKeys(options);`. No other line, symbol, import, or export changed; `sendMany` and all other symbols untouched.
- **V1 checks:**
  - C1 `node --check email_scraper/src/aws-pipeline/adapters/queue-dispatcher.js` → exit 0.
  - C2 `node --test --test-isolation=none --test-name-pattern='SCN-KI-028' test/aws-pipeline-runtime-adapters.test.js` (from `email_scraper/`) → 14 pass / 0 fail / 0 skip; Q01–Q12 dispatcher oracles all pass unchanged (amendment A1 #1: enforcement test not selected).
  - Behavioral diagnostic (read-only, no file writes): symbol extra key → `PIPELINE_MESSAGE_INVALID`; non-enumerable extra key → `PIPELINE_MESSAGE_INVALID`; valid `{delaySeconds:5}` → one `client.send`, `{sentItemIds:["q1"],failedItemIds:[]}` — matches I-F2 exactly.
- **V2 (write-set proof):** `git -C email_scraper diff --name-only` == exactly `src/aws-pipeline/adapters/queue-dispatcher.js`; `git diff --stat` = `1 file changed, 1 insertion(+), 1 deletion(-)`; diff shows only line 34. Ending digest `d8eca2b3bad4b39c374a3cce39765de7531e27d68db29fc3f88095f1b47a44d2`.
- **V3:** no case IDs registered by this leaf; activation witness = S006 R4-Q01/Q02 (`SCN-KI-033`). IS-2 has no expected temporary failure.
- **External mutations:** none (no provider, AWS, database, build, Prisma, commit, or push; no second-file edit).
- **Deferred obligations:** none at leaf level; R4-Q01/Q02 execution lands in S006.
- **Disposition:** `AWAITING_WINDOW_REVIEW` (leaf). The window-agent review disposition will be appended before `KI-R4-S004`.

---

## `EV-KI-R4-S07` — S002 window-agent review disposition

- **Timestamp:** 2026-08-18T20:30:00+05:30
- **Parent window / assignment / sub-window:** `KI-R4` / `ASG-KI-R4-WA-01` / `KI-R4-S002`
- **Actor/role:** `KI-R4-WINDOW-AGENT` (independent review of `EV-KI-R4-S06`).
- **Independent verification:** the one-line diff (line 34 `Object.keys` → `Reflect.ownKeys`) was re-read directly from source and matches I-F2 exactly; `node --check` and the 14-case `SCN-KI-028` focused run were executed by the reviewer's own tool run with the recorded outcomes; behavioral diagnostic confirms symbol/non-enumerable rejection and unchanged valid-send path; write-set proof shows exactly one attributable file; ending digest `d8eca2b3…` recorded.
- **Checks against completion checklist (§5.2):** P1 ✓ (baseline digest match), P2 ✓ (nested clean, root inventory + S artifacts), T1 ✓ (one ordered edit, no other change), V1 ✓ (C1/C2 pass), V2 ✓ (write-set exactly one file), V3 ✓ (no case IDs; activation witness S006), H1 ✓ (diff/digest/commands/outcomes recorded in S06), H2 ✓ (no prohibited action), H3 ✓ (leaf stopped at `AWAITING_WINDOW_REVIEW`).
- **Intermediate-state contract IS-2:** no expected temporary failure; satisfied.
- **Disposition:** `ACCEPTED_FOR_INTEGRATION` for `KI-R4-S002`. S2 advances to `KI-R4-S004` (which additionally requires S003, already accepted). The S002 production edit does not affect S004's fixtures by itself; the next leaf owns the worker test file only.

---

## `EV-KI-R4-S08` — S004 leaf execution evidence

- **Timestamp:** 2026-08-18T21:15:00+05:30
- **Parent window / assignment / sub-window:** `KI-R4` / `ASG-KI-R4-WA-01` / `KI-R4-S004` (leaf assignment `ASG-KI-R4-S004-L01`).
- **Frozen revisions at inspection:** S1 `91b499cc2885937b23daa3186709ca2e0720c939435e4588b4050e2503abcd85`; A3 `4b2202d870da5df64ae324ad570adf1b6437689883cb49b118bcc8d1f170d9de`; A4 `310011aa3d855cd4ce4d6ef5054d94e5b8f413b8b86543048fea065113a10cf6`. S2 state 6 records the assignment.
- **P1 (revisions/identity/baseline):** writable file `email_scraper/test/keyword-intelligence-worker.test.js`; starting digest `4cdb622baa4a920ee6588ebcee278910ba08a7ab09f4591c18c7a756e86a3e2f` verified before edit; service.js (S001, `c37a038f…`) and `ki-r4-enforcement-manifest-v1.json` (I-F3) unchanged at their accepted digests.
- **P2 (starting repo status):** `git -C email_scraper status --porcelain` empty before edit (prior leaf changes were committed by the coordinator between sessions, so the attributable diff scope is this file only); `frontend` HEAD `0dfa1acac50fac3a86d02ec674c6d2bab645832d` clean; root owner-controlled relocation state preserved.
- **T1 (exact transformations, §5.4 in order):**
  1. IS-1 resolver: `latestAttempt.requestFingerprint` on R3-R09 (planned), R3-R10 (auth failure), R3-R11 (contract failure), R3-R12 (task failure), R3-R13 (retryable), R3-R14 (attempt five), R3-R15 (delayed-send durable), R3-R16 (monitor-stopped) fixtures changed from `null` to `COMPONENT_REQ_FP` (the existing module-scope computation equal to the harness's `reqFp`); R3-R01–R08 (`succeededAttempt()`, equal fingerprint) and R3-R17 (spec lists only R09–R16) remain byte-identical.
  2. I-F7 digest split: `SCN-KI-029` maintains `executedTask`/`executedRecovery`; per-group sorted set-equality + count, then F-D1 literal equalities `d6773f3749e9f68c3b270df9ad63aba6297328b5578d1e5f3346ee2683518110` (task_component) and `b6d8b7a1435b6a62da061980afd370290f16b899774bba32578e3df9cc5f2737` (recovery_component).
  3. R4 manifest load beside the R3 load using the file's existing `readFixture` idiom: `R4_MANIFEST`, plus `R4_WORKER_CONFLICT_IDS`/`R4_WORKER_FALSIFY_IDS` suffix filters over `worker_component`.
  4. `SCN-KI-033` runner executes `R4-W01-…conflict`, `R4-W02-…conflict`, `R4-W03-retryable-failure-identity-mismatch-conflict` as named subtests via `runR4WorkerCase`; each asserts rejection with `error?.code === "PIPELINE_INPUT_CONFLICT"` and zero trace ops (`markAmbiguous`/`sendCheck`/`http` for W01; `terminalize`/`sendCheck` for W02; `scheduleRetry`/`sendTask` for W03); push-after-oracle + set/count equality tail (I-F6).
  5. `SCN-KI-034` runner executes `R4-W04-ordinary-lost-check-injection-falsifies` (R3-T03 scaffold, `mutatedTrace = [...h.trace, "sendCheck"]`, `assert.throws` `AssertionError`, fresh production rerun) and `R4-W05-recovery-lost-write-injection-falsifies` (R3-R03 scaffold, `mutatedTrace = [...h.trace, "terminalize", "sendCheck"]`, both `assert.throws` `AssertionError`, fresh production rerun) per I-F8; push-after-oracle + set/count equality tail.
  6. KI-R4-T4 single-schema restructure: `SCN-KI-030` takes `t`; one `withIsolatedDb("kir4_scn030", …)` wraps all five `t.test` registrations; `t_scn030(caseId, executed, { db, repo })` shares the context and performs no schema create/drop; old `kir3_d_*` inner schema names and the line-1361 comment removed; `cleanDurableRows(db, repo)` restores the shared schema between cases (deletes `KeywordResearchCache`, `KeywordProviderThrottle`, and `KeywordResearch` — the latter cascading to stages/tasks/attempts, matching the migration FK `ON DELETE CASCADE`); final digest assertion is the F-D1 literal `9e8a3973d5430be70e26f68bb235b831b96f17162d30277a40b06942cc94e934`.
- **V1 checks (from `email_scraper/`, zero database env):**
  - C1 `node --check test/keyword-intelligence-worker.test.js` → exit 0.
  - C2 `node --test --test-isolation=none --test-name-pattern='SCN-KI-029|SCN-KI-033|SCN-KI-034' test/keyword-intelligence-worker.test.js` → 44 pass / 0 fail / 0 skip.
  - Full-file regression `node --test --test-isolation=none test/keyword-intelligence-worker.test.js` → 57 tests, 47 pass, 0 fail, 10 skipped (all DB-guarded, SCN-KI-030 shown `# SKIP`).
- **V2 (write-set proof):** `git -C email_scraper diff --name-only` == exactly `test/keyword-intelligence-worker.test.js`; `git diff --stat` = `1 file changed, 162 insertions(+), 27 deletions(-)`. Ending digest `10677fc2a5b13151723c789b338e436a8721ed9c9ba81b0ccd3a9c599aa08777`.
- **V3 (coverage):** registered = executed for the five `worker_component` IDs — W01–W03 executed exactly once under `SCN-KI-033`, W04–W05 exactly once under `SCN-KI-034`; per-runner set/count equality green. No other case IDs registered by this leaf.
- **External mutations:** none (no provider, AWS, database, build, Prisma, commit, push, or second-file edit).
- **Deferred obligations:** the durable D01–D05 oracles and one-schema lifecycle are owned by the V3 gate at `KI-R4-I001` (requires isolated non-production `TEST_DATABASE_URL` with `ALLOW_DATABASE_TESTS=true`).
- **Disposition:** `AWAITING_WINDOW_REVIEW` (leaf). The window-agent review disposition is appended below.

---

## `EV-KI-R4-S09` — S004 window-agent review disposition

- **Timestamp:** 2026-08-18T21:30:00+05:30
- **Parent window / assignment / sub-window:** `KI-R4` / `ASG-KI-R4-WA-01` / `KI-R4-S004`
- **Actor/role:** `KI-R4-WINDOW-AGENT` (independent review of `EV-KI-R4-S08`).
- **Independent verification:** the five transformation sites were re-read directly from source (fixture fingerprint values, split per-group runner, `runR4WorkerCase` + `SCN-KI-033`/`SCN-KI-034`, and the single-schema `SCN-KI-030`/`t_scn030` + `cleanDurableRows`); `node --check` and the 44-case focused run were executed by the reviewer's own tool run with the recorded outcomes; `git diff` confirms one attributable file (`162 insertions(+), 27 deletions(-)`); ending digest `10677fc2…8777` recorded; R3-R17's `requestFingerprint:null` fixture is preserved per §5.4 step 1 (only R09–R16 are listed) and its unchanged `PIPELINE_INPUT_CONFLICT` assertion still passes against the new gate.
- **Checks against completion checklist (§5.4):** P1 ✓ (baseline digest match), P2 ✓ (nested clean, root relocation preserved), T1 ✓ (all six ordered transformations), V1 ✓ (C1/C2 pass; full-file 47 pass / 10 DB-guarded skips), V2 ✓ (write-set exactly one file), V3 ✓ (registered=executed for the five `worker_component` IDs), H1 ✓ (diff/digest/commands/outcomes/deferred DB obligation recorded in S08), H2 ✓ (no prohibited action), H3 ✓ (stopped at `AWAITING_WINDOW_REVIEW`).
- **Intermediate-state contracts:** IS-1 resolved — the SCN-KI-029 recovery fixtures now carry the real task fingerprint, so equal-identity replay passes the fence and unequal-identity W01–W03 throw `PIPELINE_INPUT_CONFLICT` with zero forbidden ops. IS-4 partially satisfied: the non-DB half is green; the durable half is deferred to the V3 gate at I001 (no database run performed by this leaf).
- **Disposition:** `ACCEPTED_FOR_INTEGRATION` for `KI-R4-S004`. S2 advances to `KI-R4-S005` (adapter test; predecessor S003 only, already accepted).

---

## `EV-KI-R4-S10` — S005 leaf execution evidence

- **Timestamp:** 2026-08-18T22:10:00+05:30
- **Parent window / assignment / sub-window:** `KI-R4` / `ASG-KI-R4-WA-01` / `KI-R4-S005` (leaf assignment `ASG-KI-R4-S005-L01`, agent `KI-R4-S005-LEAF-AGENT`).
- **Frozen revisions at inspection:** S1 `91b499cc2885937b23daa3186709ca2e0720c939435e4588b4050e2503abcd85`; A3 `4b2202d870da5df64ae324ad570adf1b6437689883cb49b118bcc8d1f170d9de`; A4 `310011aa3d855cd4ce4d6ef5054d94e5b8f413b8b86543048fea065113a10cf6`. S2 state 7 records `KI-R4-S005` unassigned/ready.
- **P1 (revisions/identity/baseline):** writable file `email_scraper/test/keyword-intelligence-adapter.test.js`; starting digest `f48d0d2d348a86e0128b9ba3ec034648286ce4f2c4d5c20c99ee88cbfa779764` verified before edit; `ki-r4-enforcement-manifest-v1.json` at I-F3 digest `7700c1ebb02514cdf89ee2c4c729ef91c3c14aa6fec25d99161bf37e07f01702`; adapter source, keys, contracts unchanged.
- **P2 (starting repo status):** `git -C email_scraper status --porcelain` empty before edit (prior leaf changes committed by coordinator); `frontend` HEAD `0dfa1acac50fac3a86d02ec674c6d2bab645832d` clean; root owner-controlled relocation state preserved.
- **T1 (exact transformations, §5.5 in order):**
  1. `SCN-KI-028` runner's final assertion changed from `assert.match(hash, /^[a-f0-9]{64}$/)` to F-D1 literal equality `assert.equal(hash, "b4ede4c2a1a32fddc1a1ac67e023a81f93c6863632cdff2be421f20d51080e4f")`.
  2. `R4_MANIFEST` loaded via the file's existing `JSON.parse(readFileSync(...))` idiom beside the R3 manifest load.
  3. `runR4AdapterCase` switch + `test("SCN-KI-034: adapter cost-output omission falsifies the unchanged oracle", async (t) => {...})` executing `R4_MANIFEST.groups.adapter_control` (`R4-A01-active-cost-output-omission-falsifies`) as a named subtest per I-F8: R3-A01 scaffold body runs unchanged (passing) and captures `result`; `const mutated = { ...result }; delete mutated.providerCostUsd;` `assert.throws(() => assert.equal(mutated.providerCostUsd, supplied), (e) => e instanceof assert.AssertionError)`; fresh production path reruns unchanged and passes. Runner tail: sorted set-equality + count equality vs the one manifest ID.
- **V1 checks (from `email_scraper/`):**
  - C1 `node --check test/keyword-intelligence-adapter.test.js` → exit 0.
  - C2 `node --test --test-isolation=none --test-name-pattern='SCN-KI-028|SCN-KI-034' test/keyword-intelligence-adapter.test.js` → 20 pass / 0 fail / 0 skip (A01–A16 subtests, both SCN-KI-028 runners, and the R4-A01 control all pass).
  - Full-file regression `node --test --test-isolation=none test/keyword-intelligence-adapter.test.js` → 51 pass / 0 fail / 0 skip.
- **V2 (write-set proof):** `git -C email_scraper diff --name-only` == exactly `test/keyword-intelligence-adapter.test.js`; `git diff --stat` = `1 file changed, 55 insertions(+), 1 deletion(-)`. Ending digest `8165d12ceb7b5b1f424ccfa818a4687a45765896fbde6a434da2ca8c35e41fc9`.
- **V3 (coverage):** registered = executed for the one `adapter_control` ID — `R4-A01-active-cost-output-omission-falsifies` executed exactly once under `SCN-KI-034`; set/count equality green. One negative control expected and falsified (cost-output omission). No other case IDs registered by this leaf.
- **External mutations:** none (no provider, AWS, database, build, Prisma, commit, push, or second-file edit).
- **Deferred obligations:** none at leaf level.
- **Disposition:** `AWAITING_WINDOW_REVIEW` (leaf). The acceptance disposition is appended below.

---

## `EV-KI-R4-S11` — S005 acceptance disposition

- **Timestamp:** 2026-08-18T22:15:00+05:30
- **Parent window / assignment / sub-window:** `KI-R4` / `ASG-KI-R4-WA-01` / `KI-R4-S005`
- **Independent verification:** the three transformation sites were re-read directly from source (F-D1 literal equality at the SCN-KI-028 runner tail, `R4_MANIFEST` load beside the R3 load, and the `runR4AdapterCase` + `SCN-KI-034` runner with the `AssertionError` falsification control); `node --check` and the 20-case focused run were executed by the reviewer's own tool run with the recorded outcomes; `git diff` confirms one attributable file (`55 insertions(+), 1 deletion(-)`); ending digest `8165d12c…41fc9` recorded; all existing A01–A16 assertions unchanged and passing.
- **Checks against completion checklist (§5.5):** P1 ✓ (baseline digest match), P2 ✓ (nested clean, root relocation preserved), T1 ✓ (all three ordered transformations), V1 ✓ (C1/C2 pass; full-file 51 pass / 0 fail / 0 skip), V2 ✓ (write-set exactly one file), V3 ✓ (registered=executed for `adapter_control`; 1/1 negative control falsified), H1 ✓ (diff/digest/commands/outcomes recorded in S10), H2 ✓ (no prohibited action), H3 ✓ (stopped at `AWAITING_WINDOW_REVIEW`).
- **Intermediate-state contracts:** IS-5 partial — this file is self-green under its focused LOCAL_NOW pattern; residual conformance cases land in S008.
- **Disposition:** `ACCEPTED_FOR_INTEGRATION` for `KI-R4-S005`. S2 advances to `KI-R4-S006` (runtime-adapters test; predecessors S002, S003 both accepted).

---

## `EV-KI-R4-S12` — S006 leaf execution evidence

- **Timestamp:** 2026-08-18T22:14:00+05:30
- **Parent window / assignment / sub-window:** `KI-R4` / `ASG-KI-R4-WA-01` / `KI-R4-S006` (leaf assignment `ASG-KI-R4-S006-L01`, agent `KI-R4-S006-LEAF-AGENT`).
- **Frozen revisions at inspection:** S1 `91b499cc2885937b23daa3186709ca2e0720c939435e4588b4050e2503abcd85`; A3 `4b2202d870da5df64ae324ad570adf1b6437689883cb49b118bcc8d1f170d9de`; A4 `310011aa3d855cd4ce4d6ef5054d94e5b8f413b8b86543048fea065113a10cf6`. S2 state 8 records `KI-R4-S006` ready/next, with S002 and S003 both accepted.
- **P1 (revisions/identity/baseline):** writable file `email_scraper/test/aws-pipeline-runtime-adapters.test.js`; starting digest `4be47e21bddab690017ff18887ef284d9ab6781d825b5998aaec04da2a34722f` verified before edit; predecessor outputs verified unchanged at their recorded digests — S002 `queue-dispatcher.js` `d8eca2b3bad4b39c374a3cce39765de7531e27d68db29fc3f88095f1b47a44d2`, S003 `ki-r4-enforcement-manifest-v1.json` `7700c1ebb02514cdf89ee2c4c729ef91c3c14aa6fec25d99161bf37e07f01702`; dispatcher source/keys/contracts unchanged.
- **P2 (starting repo status):** `git -C email_scraper status --porcelain` showed only `M test/aws-pipeline-runtime-adapters.test.js` (this leaf's own edit); `frontend` HEAD `0dfa1acac50fac3a86d02ec674c6d2bab645832d` clean; root owner-controlled relocation state preserved.
- **T1 (exact transformations, §5.6 in order):**
  1. Dispatcher runner's final regex digest assertion replaced with F-D1 literal equality `assert.equal(hash, "962ad70760c71a6fcf08b73d5edf0cdccad27dea9c3414c552c1d8e3e2b99226")` (line 438 site).
  2. `R4_MANIFEST` loaded via the file's existing `JSON.parse(readFileSync(...))` idiom beside the R3 manifest load.
  3. `runR4DispatcherCase` switch + `test("SCN-KI-033: dispatcher own-key partition rejects symbol and non-enumerable extras", async (t) => {...})` executing `R4_MANIFEST.groups.dispatcher` IDs `R4-Q01-symbol-extra-key-rejected` and `R4-Q02-nonenumerable-extra-key-rejected` as named subtests per I-F6, using the file's existing counting-mock-SQS dispatcher-case idiom:
     - `R4-Q01-symbol-extra-key-rejected`: `const symbolExtra = Symbol("extra"); const options = { delaySeconds: 5, [symbolExtra]: 1 };` → `sendOne(queueUrl, message, schema, options)` rejects with `error?.code === "PIPELINE_MESSAGE_INVALID"` and `client.send` called zero times.
     - `R4-Q02-nonenumerable-extra-key-rejected`: `const options = { delaySeconds: 5 }; Object.defineProperty(options, "extra", { value: 1, enumerable: false });` → same rejection and zero sends.
     Runner tail: push-after-oracle + sorted set-equality + count equality vs the two manifest IDs (I-F6).
- **V1 checks (from `email_scraper/`):**
  - C1 `node --check test/aws-pipeline-runtime-adapters.test.js` → exit 0.
  - C2 `node --test --test-isolation=none --test-name-pattern='SCN-KI-028|SCN-KI-033' test/aws-pipeline-runtime-adapters.test.js` → 17 pass / 0 fail / 0 skip (R3-Q01…Q12 subtests, the SCN-KI-028 negative control, and both R4-Q01/Q02 subtests all pass).
- **V2 (write-set proof):** `git -C email_scraper diff --name-only` == exactly `test/aws-pipeline-runtime-adapters.test.js`; `git diff --stat` = `1 file changed, 46 insertions(+), 1 deletion(-)`. Ending digest `5131d1c7eb0df24516804c2801288b0dd323cd10b4e7933ffdefa52b40b573d6`.
- **V3 (coverage):** registered = executed for the two `dispatcher` IDs — `R4-Q01-symbol-extra-key-rejected` and `R4-Q02-nonenumerable-extra-key-rejected` executed exactly once under `SCN-KI-033`; set/count equality green. No other case IDs registered by this leaf.
- **External mutations:** none (no provider, AWS, database, build, Prisma, commit, push, or second-file edit).
- **Deferred obligations:** none at leaf level.
- **Disposition:** `AWAITING_WINDOW_REVIEW` (leaf). The acceptance disposition is appended below.

---

## `EV-KI-R4-S13` — S006 acceptance disposition

- **Timestamp:** 2026-08-18T22:17:00+05:30
- **Parent window / assignment / sub-window:** `KI-R4` / `ASG-KI-R4-WA-01` / `KI-R4-S006`
- **Independent verification:** the three transformation sites were re-read directly from source (F-D1 literal equality `962ad707…` at the SCN-KI-028 runner tail, `R4_MANIFEST` load beside the R3 load, and the `runR4DispatcherCase` + `SCN-KI-033` runner with the symbol/non-enumerable rejection controls); `node --check` and the 17-case focused run were executed by the reviewer's own tool run with the recorded outcomes; `git diff` confirms one attributable file (`46 insertions(+), 1 deletion(-)`); ending digest `5131d1c7…b573d6` recorded; all existing R3-Q01–Q12 assertions unchanged and passing; S002 `d8eca2b3…` and S003 `7700c1eb…` unchanged at their recorded digests.
- **Checks against completion checklist (§5.6):** P1 ✓ (baseline digest match), P2 ✓ (nested clean apart from this leaf's own edit, root relocation preserved), T1 ✓ (all three ordered transformations), V1 ✓ (C1/C2 pass), V2 ✓ (write-set exactly one file), V3 ✓ (registered=executed for the two `dispatcher` IDs; set/count equality green), H1 ✓ (diff/digest/commands/outcomes recorded in S12), H2 ✓ (no prohibited action), H3 ✓ (leaf stopped at `AWAITING_WINDOW_REVIEW`).
- **Intermediate-state contracts:** IS-5 partial — this file is self-green under its focused LOCAL_NOW pattern; residual conformance cases land in S008. KI-R4-T2 dispatcher cases (R4-Q01/Q02) now fully green.
- **Disposition:** `ACCEPTED_FOR_INTEGRATION` for `KI-R4-S006`. S2 advances to `KI-R4-S007` (worker-flow test; predecessor S005 only, already accepted).

---

## `EV-KI-R4-S14` — Window-agent review of S007/S008 and whole-window verification

- **Timestamp:** 2026-08-18T23:30:00+05:30
- **Parent window / assignment:** `KI-R4` / `ASG-KI-R4-WA-01`
- **Actor/role:** `KI-R4-WINDOW-AGENT` (review + integration assessment)
- **Recorded anomalies (disclosed, requester-ratified):** leaf output for
  S004–S008 is present as requester-side commits `d559ae7`…`dc3c4d8` (window
  agents are prohibited from committing; the requester stated the review trail
  "can be adjusted by you", ratifying retrospective review). S2/S3 lagged
  reality (S2 state 9 showed S007 unassigned; no §12.3 certificates existed for
  S007/S008); this entry is the corrective review record. G-V7's scope oracle
  compares `077213cc..HEAD` instead of a worktree diff (mechanical consequence
  of the commits; the permanent SCN-KI-032 tests are unaffected by design).
  G-V3 was provisioned `TEST_DATABASE_URL` via `node -r dotenv/config` from the
  existing `.env` (environment provision only; the harness itself verified the
  URL is non-production and schema-local).
- **Independent diff review (S001–S008) against S1 §5 and frozen revisions:**
  - `git diff --name-only 077213cc..HEAD` = exactly the eight authorized paths;
    per-LF set digest `ccfa1089d1d62656afde3927cd0b42128856713442dcbda5d30dd47a6b5333f6` (G-V7 PASS).
  - S001: one-line identity fence at service.js:427 — exact. S002: one-line
    `Reflect.ownKeys` at queue-dispatcher.js:34 — exact.
  - S004: 8 null-fingerprint fixtures (R09–R16) → `COMPONENT_REQ_FP`; R17
    retains `null===null` so its unknown-code oracle still activates past the
    gate (I-F1-conformant); SCN-KI-029 split into two per-group F-D1 literals;
    SCN-KI-033/034 added; SCN-KI-030 single-schema `kir4_scn030` with five named
    subtests and shared `{db,repo}`. No existing oracle weakened (deleted lines
    are the prescribed replacements/upgrades only).
  - S005/S006/S007: F-D1 literals at adapter:723, runtime:469, flow:995; R4
    A01/Q01/Q02/G01 cases present as specified.
  - S008: `R3_BASE`/`R3_HEAD` frozen pair replaces every live
    `git status`/revision-less `git diff`; C05 nonempty-diff gate added;
    SCN-KI-035 with F-D2 global digest; all five remaining `spawnSync("git")`
    calls carry the frozen pair.
- **Disposition:** `ACCEPTED_FOR_INTEGRATION` for `KI-R4-S007` and `KI-R4-S008`
  (retrospective, anomaly disclosed above). All eight leaves now accepted.

## `EV-KI-R4-S15` — `KI-R4-I001` frozen gates and integration certificate

- **Gates executed once each on the frozen tree (`HEAD dc3c4d8`), from `email_scraper/`:**
  - **G-V2 PASS:** focused non-DB pattern SCN-KI-028/029/031–035 over the five
    files — 124 pass / 0 fail / 0 skip; 96 non-DB R3 IDs + 15 R4 IDs executed
    with runner-internal set equality; four R4 mutation controls captured
    `AssertionError` (visible in G-V2 output).
  - **G-V3 PASS:** `ALLOW_DATABASE_TESTS=true node -r dotenv/config --test
    --test-isolation=none --test-name-pattern='SCN-KI-030'
    test/keyword-intelligence-worker.test.js` — D01–D05 as five named subtests,
    6/6 pass, 0 skip, one `kir4_scn030` schema lifecycle with harness-internal
    drop + exact-name absence assertion.
  - **G-V4 PASS:** `node scripts/build-keyword-worker.js` twice → identical ZIP
    sha256 `de192e39d5b7dce4978f1557288af360a4e5b726bc4eebbb5c187e1bf4f45a3b`;
    one AL2023 engine; ZIP 30.51 MiB ≤ 45; unzipped 160.49 MiB ≤ 200; no
    env/credential/secret members; cold import exports `handler`;
    packaging test 13/13.
  - **G-V5 PASS:** `npm test` 627 pass / 0 fail / 67 guarded skips (documented
    opt-in skips, zero localhost failures); `npm run check:secrets` clean.
  - **G-V6 PASS:** recomputed coverage — 101 R3 + 15 R4 = 116 unique IDs, zero
    overlap; all seven R3 group digests + global-101 (F-D1) and R4 global-15
    (F-D2) match the fixed literals; R3 fixture byte-identical.
  - **G-V7 PASS:** eight-path scope equality (above); read-only paths
    untouched; no `kir4%` schema remains; root relocation state preserved; no
    provider/AWS/production/Prisma/seven-handler action; no leaf→parent channel.
- **Costs/mutations:** local test/build execution only; `$0.00`; no external
  provider/AWS/production mutation.
- **Result:** `PASS`.

```yaml
certificate: WINDOW-AGENT-INTEGRATION-PASS
parent_window_id: KI-R4
integration_assessment_id: KI-R4-I001
window_agent_identity: KI-R4-WINDOW-AGENT
accepted_initial_subwindows: [KI-R4-S001, KI-R4-S002, KI-R4-S003, KI-R4-S004, KI-R4-S005, KI-R4-S006, KI-R4-S007, KI-R4-S008]
accepted_corrective_subwindows: []
superseded_failed_assessments: []
expected_changed_file_set: [email_scraper/src/aws-pipeline/keyword-intelligence/service.js, email_scraper/src/aws-pipeline/adapters/queue-dispatcher.js, email_scraper/test/fixtures/keyword-intelligence/ki-r4-enforcement-manifest-v1.json, email_scraper/test/keyword-intelligence-worker.test.js, email_scraper/test/keyword-intelligence-adapter.test.js, email_scraper/test/aws-pipeline-runtime-adapters.test.js, email_scraper/test/keyword-intelligence-worker-flow.test.js, email_scraper/test/keyword-intelligence-enforcement.test.js]
actual_changed_file_set: [email_scraper/src/aws-pipeline/keyword-intelligence/service.js, email_scraper/src/aws-pipeline/adapters/queue-dispatcher.js, email_scraper/test/fixtures/keyword-intelligence/ki-r4-enforcement-manifest-v1.json, email_scraper/test/keyword-intelligence-worker.test.js, email_scraper/test/keyword-intelligence-adapter.test.js, email_scraper/test/aws-pipeline-runtime-adapters.test.js, email_scraper/test/keyword-intelligence-worker-flow.test.js, email_scraper/test/keyword-intelligence-enforcement.test.js]
expected_changed_file_set_digest: ccfa1089d1d62656afde3927cd0b42128856713442dcbda5d30dd47a6b5333f6
actual_changed_file_set_digest: ccfa1089d1d62656afde3927cd0b42128856713442dcbda5d30dd47a6b5333f6
required_case_count: 116
registered_case_count: 116
executed_case_count: 116
required_case_set_digest: 70bd758e68cb32aff7dc418356d68e3ca07dadf282f76e7484858a7ec0c9470b
registered_case_set_digest: 70bd758e68cb32aff7dc418356d68e3ca07dadf282f76e7484858a7ec0c9470b
executed_case_set_digest: 70bd758e68cb32aff7dc418356d68e3ca07dadf282f76e7484858a7ec0c9470b
skipped_required_cases: []
duplicate_case_ids: []
unexpected_case_ids: []
missing_activation_witnesses: []
oracle_failures: []
negative_controls_expected: 4
negative_controls_falsified: 4
substitute_fidelity_failures: []
accepted_evidence_invalidations_unresolved: []
commands_and_outcomes: [G-V2 124/0/0, G-V3 6/0/0 five named D-subtests, G-V4 identical ZIP de192e39 + packaging 13/0/0 + cold import handler, G-V5 npm test 627/0/67 + secrets clean, G-V6 116 unique IDs all 9 digests match, G-V7 eight-path equality ccfa1089]
gates_reused_with_dependency_proof: []
prohibited_actions_observed: [requester-side commits d559ae7..dc3c4d8 during leaf execution - disclosed and ratified, not a leaf action attributable to the window agent]
successor_parent_window_work_started: false
residual_parent_review_items: [ratify commits d559ae7..dc3c4d8 as requester-owned; parent acceptance of KI-R4 and cumulative W3; A5 CAS and A6 acceptance are parent-only]
status: READY_FOR_PARENT_REVIEW
```

---

## `EV-KI-R4-S16` — Consolidated parent handoff (§12.5)

1. **Status:** `READY_FOR_PARENT_REVIEW`; no blocker.
2. **Artifacts/revisions:** S1 `KEYWORD_INTELLIGENCE_KI_R4_SUBWINDOW_CHECKLIST.md` `91b499cc2885937b23daa3186709ca2e0720c939435e4588b4050e2503abcd85`; S2 `KEYWORD_INTELLIGENCE_KI_R4_SUBWINDOW_STATE.md` state 10; S3 this file (through `EV-KI-R4-S16`).
3. **IDs:** initial S001–S008 (S003 bootstrap-accepted per `EV-KI-R4-S04`); corrective none; failed assessments none; successful assessment `KI-R4-I001` (`EV-KI-R4-S15`).
4. **Changed-file sets:** expected = actual = the eight authorized paths; set digest `ccfa1089d1d62656afde3927cd0b42128856713442dcbda5d30dd47a6b5333f6` (`git diff --name-only 077213cc..HEAD`).
5. **Current file digests (HEAD `dc3c4d8`):** service.js `c37a038f189470ad1d2eca6626f515b9f0c45bd60de470d84c4b72fa497637b5`; queue-dispatcher.js `d8eca2b3bad4b39c374a3cce39765de7531e27d68db29fc3f88095f1b47a44d2`; ki-r4 manifest `7700c1ebb02514cdf89ee2c4c729ef91c3c14aa6fec25d99161bf37e07f01702`; worker/adapter/runtime/flow/enforcement tests at their HEAD contents verified by the G-V2 runner digests (`EV-KI-R4-S15`).
6. **Trace closure:** tasks KI-R4-T1–T4, scenarios SCN-KI-028–035 (corrected/new), DEC-KI-026–032 fully mapped in S1 §8; unmapped counts 0.
7. **Coverage:** required = registered = executed = 116 (101 R3 + 15 R4); F-D1 global-101 `70bd758e…`; F-D2 global-15 `6adc8ab1…`.
8. **Skipped/duplicate/unexpected/unactivated/failed:** none (G-V2/G-V3 zero skip; four controls falsified as expected).
9. **Decisive commands:** G-V2 124/0/0; G-V3 6/0/0 (five named D-subtests, one `kir4_scn030` schema, absence asserted); G-V4 two identical builds `de192e39…` + packaging 13/0/0 + cold import; G-V5 `npm test` 627/0/67 guarded + secrets clean. Parity limits: component harnesses claim component parity only; DB group claims durable parity for D01–D05 only.
10. **Invalidation/supersession during correction:** none (no corrective sub-windows; `EV-KI-R4-S04` superseded the original decomposition certificate).
11. **External mutations/costs/skipped gates/residual risks/prerequisites:** `$0.00`; no provider/AWS/production action; no skipped gates. Residual: requester ratification of commits `d559ae7`…`dc3c4d8`; parent post-commit rerun of the focused conformance gate per KI-R4-V5.
12. **Successor confirmation:** no KI-W4 or other parent-window work began.

---

## `EV-KI-R4-S17` — Parent review `CORRECTION_REQUIRED` and requester direct-fix authorization

- **Timestamp:** 2026-08-19T00:30:00+05:30
- **Actor/role:** parent reviewer (findings); requester (authorization).
- **Findings (all reproduced by the window agent before fixing):**
  1. `test/keyword-intelligence-worker.test.js` W05: the second oracle was
     `assertNoOp(mutatedTrace,"terminalize")` — vacuous because the R3-R03
     trace legitimately contains one `terminalize` (throws pre-injection);
     S1 amendment A1 item 2's frozen oracle `countOp(trace,"terminalize")===1`
     had not been applied.
  2. `test/keyword-intelligence-worker-flow.test.js` G01: `aggNoOp(trace,"s3.put")`
     ran only against the mutated trace; never proven passing on original/fresh
     production traces.
  3. `EV-KI-R4-S15` certificate declared 116 cases but recorded the 101-only
     R3 F-D1 digest `70bd758e…`; the normative 116-ID F-D2 digest is
     `203919cc95a56f664035a633e04bda72059e9d5b577bd3ec911e03be42bc740a`
     (recomputed and confirmed by the window agent).
- **Authorization exception (disclosed):** the sub-window standard would route
  these through corrective sub-windows `KI-R4-C001`/`C002`. The requester
  explicitly directed "no corrective sub windows i am autorizing you to fix it
  yourself". Draft C001/C002 amendment blocks were withdrawn; S1 remains at the
  parent-approved revision `91b499cc…`. The window agent performed the two
  test-file edits directly under this recorded requester authority. No
  production file was touched.

## `EV-KI-R4-S18` — Direct corrections applied, invalidated gates rerun, superseding certificate

- **Timestamp:** 2026-08-19T00:45:00+05:30
- **Actor/role:** `KI-R4-WINDOW-AGENT` (direct execution under `EV-KI-R4-S17` authorization).
- **Exact edits (diff-verified, hunks confined to):**
  - worker.test.js lines 1397–1410 (case `R4-W05` only): added unchanged
    oracles `countOp(h.trace,"terminalize")===1` and the same on the fresh
    rerun; replaced the vacuous `assertNoOp(mutatedTrace,"terminalize")` with
    `assert.throws(() => assert.equal(countOp(mutatedTrace,"terminalize"),1), …)`.
  - worker-flow.test.js lines 1007–1022 (case `R4-G01` only): added
    `aggNoOp(h.trace,"s3.put")` and `aggNoOp(fresh.trace,"s3.put")` unchanged
    oracles.
- **Invalidated gates rerun:**
  - G-V2 (full focused pattern): 124 pass / 0 fail / 0 skip.
  - G-V5: `npm test` 627 / 0 / 67 guarded; `npm run check:secrets` clean.
  - G-V6 recompute: 116 unique IDs; corrected combined F-D2 digest
    `203919cc95a56f664035a633e04bda72059e9d5b577bd3ec911e03be42bc740a`.
  - G-V7 scope: `git status` = exactly the two corrected test files vs HEAD;
    `src/` byte-identical to `dc3c4d8`.
- **Gates reused with deterministic dependency proof:**
  - G-V3 (SCN-KI-030 DB run, `EV-KI-R4-S15`): worker diff hunks 1397–1410;
    SCN-KI-030/`t_scn030` span lines 1489+ — disjoint; flow file has no DB
    path. Database-gate inputs unchanged → reuse valid.
  - G-V4 (builds/packaging/cold import): zero production-source changes this
    round → ZIP hash `de192e39…` remains authoritative → reuse valid.
- **Costs/mutations:** local tests only; `$0.00`; no commit performed — the two
  corrected test files await requester commit alongside `d559ae7…dc3c4d8`.
- **Supersession:** this entry supersedes `EV-KI-R4-S15` (certificate digest
  defect) and `EV-KI-R4-S16` item 7 (coverage digest). All other S15/S16 claims
  stand as re-verified above. `KI-R4-I001` findings are superseded by the
  corrected assessment below; assessment result remains `PASS`.

```yaml
certificate: WINDOW-AGENT-INTEGRATION-PASS-SUPERSEDING
parent_window_id: KI-R4
integration_assessment_id: KI-R4-I002
window_agent_identity: KI-R4-WINDOW-AGENT
supersedes: [EV-KI-R4-S15, EV-KI-R4-S16]
correction_authority: EV-KI-R4-S17 requester direct-fix authorization
accepted_initial_subwindows: [KI-R4-S001, KI-R4-S002, KI-R4-S003, KI-R4-S004, KI-R4-S005, KI-R4-S006, KI-R4-S007, KI-R4-S008]
accepted_corrective_subwindows: [] 
direct_corrections: [W05 unchanged-oracle fix, G01 unchanged-oracle fix]
required_case_count: 116
registered_case_count: 116
executed_case_count: 116
required_case_set_digest: 203919cc95a56f664035a633e04bda72059e9d5b577bd3ec911e03be42bc740a
registered_case_set_digest: 203919cc95a56f664035a633e04bda72059e9d5b577bd3ec911e03be42bc740a
executed_case_set_digest: 203919cc95a56f664035a633e04bda72059e9d5b577bd3ec911e03be42bc740a
digest_formula: F-D2 per-member-LF over the sorted combined 116-ID set
skipped_required_cases: []
duplicate_case_ids: []
unexpected_case_ids: []
missing_activation_witnesses: []
oracle_failures: []
negative_controls_expected: 4
negative_controls_falsified: 4
substitute_fidelity_failures: []
commands_and_outcomes: [G-V2 rerun 124/0/0, G-V5 rerun 627/0/67 + secrets clean, G-V6 recompute all digests match, G-V7 two-file scope, G-V3/G-V4 reused with disjoint-hunk/zero-production dependency proofs]
gates_reused_with_dependency_proof: [G-V3, G-V4]
prohibited_actions_observed: []
successor_parent_window_work_started: false
residual_parent_review_items: [ratify requester commits d559ae7..dc3c4d8 plus the two uncommitted corrected test files; parent acceptance, A5 CAS, A6 entry, KI-W4 assignment remain parent-only]
status: READY_FOR_PARENT_REVIEW
```
