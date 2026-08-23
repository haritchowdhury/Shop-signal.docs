# KI-W6 Reauthored Sub-Window State (`S2`)

Mechanical state file. Only `KI-W6-WINDOW-AGENT` writes it, only inside the
`ASG-KI-W6-WA-04` coordination scope (the three `REAUTHORED` artifacts).
Parent artifacts (`A1`–`A8`) are never modified here. This file records no
evidence and no history; see `S3`
(`KEYWORD_INTELLIGENCE_KI_W6_REAUTHORED_SUBWINDOW_EVIDENCE.md`). Decomposition
authority lives in `S1`
(`KEYWORD_INTELLIGENCE_KI_W6_REAUTHORED_SUBWINDOW_CHECKLIST.md`).

```yaml
state_version: 44
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-05
window_agent_identity: KI-W6-WINDOW-AGENT
parent_standard_path: PROJECT_AGNOSTIC_DECISION_COMPLETE_CHECKLIST_AUTHORING_STANDARD.md
parent_standard_revision: cda352017e75c0d11f6797d9fbe108b4365508cd38b0e92365cfb523ede32848
subwindow_standard_path: PROJECT_AGNOSTIC_WINDOW_AGENT_SUBWINDOW_AUTHORING_STANDARD.md
subwindow_standard_revision: 84e7590e74589f308c70dc9b0b67f7e9da395fafb1e5786202ecd1ca15be56e9
parent_contract_revision: 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c
parent_decision_revision: d6132eecb4ab8a1c6594aa2efb1a423567c798a11f658a2c7df078793b6c0912
parent_checklist_revision: 642025513288ae76dd448b7064e1d15fc6c57b688909206c96275ecca119463b
parent_state_path: ACTIVE_EXECUTION_STATE.md
parent_state_revision: 164
decomposition_path: KEYWORD_INTELLIGENCE_KI_W6_REAUTHORED_SUBWINDOW_CHECKLIST.md
decomposition_revision: 86b56ecaa579da2e4ec305c7c4800bbfb7b2666489dd9ceab72ca8ef0f11bc57
evidence_path: KEYWORD_INTELLIGENCE_KI_W6_REAUTHORED_SUBWINDOW_EVIDENCE.md
decomposition_status: READY
integration: 'Parent history preserved: C107-C111 and CV26/CV32 as recorded; seventh correction C112-C117 accepted with I109 CV36-CV38 pass and CV39 preserved as diagnostic evidence (EV-KI-W6-R52); parent SRC-KI-048/DEC-KI-046/KI-CL-28 resolve the harness-oracle defect. The eighth correction C118/I110 is transcribed into S1 under ASG-KI-W6-WA-05 and executes sequentially here.'
current_subwindow: STOP
current_assignment_id: ASG-KI-W6-WA-08
assigned_agent: KI-W6-WINDOW-AGENT
subwindow_type: INTEGRATION_ASSESSMENT
authorized_write_file: NONE
authorized_read_scope: [A1-A8, KI-W6 S1/S2/S3, accepted C112-C117 source/diff/evidence, KEYWORD_INTELLIGENCE_DECISION_LEDGER.md §DEC-KI-046, SRC-KI-048, EV-KI-W6-R52, email_scraper nested repository, frontend nested repository]
authorized_actions: [leaf applies exactly CT14 item-6 ordered block replacement with its two local-now checks; window agent then personally executes I110: CV44 inspection, CV45 dependency-proof reuse of I109 CV36-CV38 plus one fresh causal browser gate, CV46-CV49, CH10; append S3 evidence; set READY_FOR_PARENT_REVIEW and stop]
prohibited_actions: [window-agent implementation edits, parallel leaf execution, second implementation file, clearing or truncating the browser netlog, backend source or test edits, changed case/control/digest/browser command, provider/AWS/production/destructive action, full opted-in database suite, Prisma generate or validate, A1-A8 edit, commit, push, KI-W7 action]
execution_environment_policy:
  sandbox_escalation_for_authorized_local_actions: true
  automatic_identical_recovery_after_proven_environment_invalidation: true
  recovery_limit_per_invalidated_execution: 1
  external_authority_expansion: false
may_start_successor: false
current_status: BLOCKED
accepted_subwindows: [KI-W6-S101, KI-W6-S102, KI-W6-S103, KI-W6-S104, KI-W6-S105, KI-W6-C104, KI-W6-C105, KI-W6-C106, KI-W6-C107, KI-W6-C108, KI-W6-C109, KI-W6-C112, KI-W6-C113, KI-W6-C114, KI-W6-C115, KI-W6-C116, KI-W6-C117, KI-W6-C118]
next_subwindow: STOP
blocker: 'isolated TEST_DATABASE_URL provider (Neon) rejects all connections with 53000 data-transfer-quota-exceeded; integration regression and causal browser gate cannot execute until the quota is restored (plan upgrade, quota reset, or an alternate authorized isolated database). Correction itself is locally proven: C131-C135 accepted, syntax 5/5, unit 4/4.'
last_updated: 2026-08-23T18:20:00+05:30
```

## Sub-window registry

| ID | Type | File | Status | Assigned agent | Assignment ID |
|---|---|---|---|---|---|
| `KI-W6-S101` | FILE | `frontend/components/keyword-intelligence/research-dashboard.tsx` | ACCEPTED | `KI-W6-S101-LEAF-AGENT` | `ASG-KI-W6-S101` (certificate + `EV-KI-W6-R15` in S3) |
| `KI-W6-S102` | FILE | `frontend/test/browser/keyword-intelligence-dashboard.mjs` | ACCEPTED | `KI-W6-S102-LEAF-AGENT` | `ASG-KI-W6-S102` (certificate + `EV-KI-W6-R16` in S3) |
| `KI-W6-S103` | FILE | `email_scraper/test/helpers/keyword-intelligence-e2e-harness.js` | ACCEPTED | `KI-W6-S103-LEAF-AGENT` | `ASG-KI-W6-S103` (certificate + `EV-KI-W6-R17` in S3) |
| `KI-W6-S104` | FILE | `email_scraper/test/fixtures/keyword-intelligence/ki-w6-enforcement-manifest-v1.json` | ACCEPTED | `KI-W6-S104-LEAF-AGENT` | `ASG-KI-W6-S104` (certificate + `EV-KI-W6-R18` in S3) |
| `KI-W6-S105` | FILE | `frontend/test/browser/keyword-intelligence-e2e.mjs` | ACCEPTED | `KI-W6-S105-LEAF-AGENT` | `ASG-KI-W6-S105` (certificate + `EV-KI-W6-R19` in S3) |
| `KI-W6-I101` | INTEGRATION_ASSESSMENT | (none) | SUPERSEDED | `KI-W6-WINDOW-AGENT` | `ASG-KI-W6-WA-02` (V3 publication witness; superseded by I102) |
| `KI-W6-C104` | CORRECTION | `email_scraper/src/aws-pipeline/keyword-intelligence/service.js` | ACCEPTED_FOR_INTEGRATION | `KI-W6-C104-LEAF-AGENT` | `ASG-KI-W6-C104` (EV-KI-W6-R26; requester-owned provenance) |
| `KI-W6-C105` | CORRECTION | `email_scraper/test/keyword-intelligence-worker-flow.test.js` | ACCEPTED_FOR_INTEGRATION | `KI-W6-C105-LEAF-AGENT` | `ASG-KI-W6-C105` |
| `KI-W6-I102` | INTEGRATION_ASSESSMENT | (none) | PARENT_BLOCKED | `KI-W6-WINDOW-AGENT` | `ASG-KI-W6-WA-02` (resolved by parent) |
| `KI-W6-C106` | CORRECTION | `email_scraper/test/keyword-intelligence-worker-flow.test.js` | ACCEPTED_FOR_INTEGRATION | `KI-W6-C106-LEAF-AGENT` | `ASG-KI-W6-C106` |
| `KI-W6-I103` | INTEGRATION_ASSESSMENT | (none) | SUPERSEDED | `KI-W6-WINDOW-AGENT` | `ASG-KI-W6-WA-02` (CV7/CV8 pass; superseded) |
| `KI-W6-C107` | CORRECTION | `frontend/test/browser/keyword-intelligence-e2e.mjs::swapOneSelectionItemViaUi` | ACCEPTED_FOR_INTEGRATION | `KI-W6-C107-LEAF-AGENT` | `ASG-KI-W6-C107` (requester-owned commit `6c1563e…`) |
| `KI-W6-I104` | INTEGRATION_ASSESSMENT | (none) | SUPERSEDED | `KI-W6-WINDOW-AGENT` | `ASG-KI-W6-WA-02` (CV13/CV14 pass; CV15 superseded by parent C108/C109) |
| `KI-W6-C108` | CORRECTION | `email_scraper/src/keyword-intelligence/repository.js` | ACCEPTED_FOR_INTEGRATION | `KI-W6-C108-LEAF-AGENT` | `ASG-KI-W6-C108` (requester-owned commit `21de6c9f…`) |
| `KI-W6-C109` | CORRECTION | `email_scraper/test/keyword-intelligence-repository.integration.test.js` | ACCEPTED_FOR_INTEGRATION | `KI-W6-C109-LEAF-AGENT` | `ASG-KI-W6-C109` (uncommitted; baseline of C115) |
| `KI-W6-I105` | INTEGRATION_ASSESSMENT | (none) | SUPERSEDED | `KI-W6-WINDOW-AGENT` | `ASG-KI-W6-WA-03` (CV21 unobservable here; resolved by parent takeover) |
| `KI-W6-C110` | CORRECTION (parent-executed) | `email_scraper/test/keyword-intelligence-repository.integration.test.js` | ACCEPTED (parent) | parent agent | requester takeover (EV-KI-A-100) |
| `KI-W6-I106` | INTEGRATION_ASSESSMENT (parent) | (none) | CV26 ACCEPTED / CV27 failed (parent) | parent agent | requester takeover (EV-KI-A-100) |
| `KI-W6-C111` | CORRECTION (parent-executed) | `frontend/test/browser/keyword-intelligence-e2e.mjs` | ACCEPTED locally (parent) | parent agent | requester takeover (EV-KI-A-100) |
| `KI-W6-I107` | INTEGRATION_ASSESSMENT (parent) | (none) | CV32 FAILED diagnostic (parent) | parent agent | requester takeover (EV-KI-A-101) |
| `KI-W6-C112` | CORRECTION | `email_scraper/src/keyword-intelligence/repository.js` | ACCEPTED_FOR_INTEGRATION | `KI-W6-C112-LEAF-AGENT` | `ASG-KI-W6-C112` (EV-KI-W6-R45; ending digest `17e55ed2…`) |
| `KI-W6-C113` | CORRECTION | `email_scraper/src/aws-pipeline/keyword-intelligence/recovery.js` | ACCEPTED_FOR_INTEGRATION | `KI-W6-C113-LEAF-AGENT` | `ASG-KI-W6-C113` (EV-KI-W6-R46; ending digest `714e40da…`) |
| `KI-W6-C114` | CORRECTION | `email_scraper/test/keyword-intelligence-repository.test.js` | ACCEPTED_FOR_INTEGRATION | `KI-W6-C114-LEAF-AGENT` | `ASG-KI-W6-C114` (EV-KI-W6-R47; ending digest `87c5fa81…`) |
| `KI-W6-C115` | CORRECTION | `email_scraper/test/keyword-intelligence-repository.integration.test.js` | ACCEPTED_FOR_INTEGRATION | `KI-W6-C115-LEAF-AGENT` | `ASG-KI-W6-C115` (EV-KI-W6-R48; ending digest `c50b1e70…`; DB execution deferred to I108/CV38) |
| `KI-W6-C116` | CORRECTION | `email_scraper/test/keyword-intelligence-recovery.test.js` | ACCEPTED_FOR_INTEGRATION | `KI-W6-C116-LEAF-AGENT` | `ASG-KI-W6-C116` (EV-KI-W6-R49; ending digest `41240b25…`) |
| `KI-W6-I108` | INTEGRATION_ASSESSMENT | (none; gates CV36–CV43/CH9) | CORRECTION_REQUIRED | `KI-W6-WINDOW-AGENT` | `ASG-KI-W6-WA-04` (CV36 pass, CV37 pass, CV38 observable failure EV-KI-W6-R50; superseded by I109) |
| `KI-W6-C117` | CORRECTION | `email_scraper/test/keyword-intelligence-repository.integration.test.js` | ACCEPTED_FOR_INTEGRATION | `KI-W6-C117-LEAF-AGENT` | `ASG-KI-W6-C117` (EV-KI-W6-R51; ending digest `91db4db5…`) |
| `KI-W6-I109` | INTEGRATION_ASSESSMENT | (none; reuses CV36/CV37 with dependency proof, reruns CV38, then CV39–CV43/CH9-equivalent) | PARENT_BLOCKED | `KI-W6-WINDOW-AGENT` | `ASG-KI-W6-WA-04` (CV36/37/38 pass; CV39 structural harness failure outside scope — EV-KI-W6-R52) |
| `KI-W6-C118` | CORRECTION | `frontend/test/browser/keyword-intelligence-e2e.mjs` | ACCEPTED_FOR_INTEGRATION | `KI-W6-C118-LEAF-AGENT` | `ASG-KI-W6-C118` (EV-KI-W6-R53; ending digest `4fece32a…`) |
| `KI-W6-I110` | INTEGRATION_ASSESSMENT | (none; CV44 inspection, CV45 reuse+fresh browser gate, CV46–CV49, CH10) | SUPERSEDED_BY_I111 | `KI-W6-WINDOW-AGENT` | `ASG-KI-W6-WA-05` (CV44 pass, CV45 dependency proof pass, CV45 browser run structural /runs/* proxy redirect — EV-KI-W6-R54; parent resolved via DEC-KI-047) |
| `KI-W6-C119` | CORRECTION | `email_scraper/test/helpers/keyword-intelligence-e2e-harness.js` | ACCEPTED_FOR_INTEGRATION | `KI-W6-C119-LEAF-AGENT` | `ASG-KI-W6-C119` (EV-KI-W6-R55; ending digest `cbcd304a…`) |
| `KI-W6-C120` | CORRECTION | `frontend/test/browser/keyword-intelligence-e2e.mjs` | ACCEPTED_FOR_INTEGRATION | `KI-W6-C120-LEAF-AGENT` | `ASG-KI-W6-C120` (EV-KI-W6-R56; ending digest `72fe4f99…`) |
| `KI-W6-I111` | INTEGRATION_ASSESSMENT | (none; CV50–CV57, CH11) | SUPERSEDED_BY_I112 | `KI-W6-WINDOW-AGENT` | `ASG-KI-W6-WA-06` (CV50–CV52 pass; failed CV53 diagnostic superseded by DEC-KI-048 tenth correction — EV-KI-W6-R57) |
| `KI-W6-C121` | CORRECTION | `frontend/test/browser/keyword-intelligence-e2e.mjs` | ACCEPTED_FOR_INTEGRATION | `KI-W6-C121-LEAF-AGENT` | `ASG-KI-W6-C121` (EV-KI-W6-R58; ending digest `8d89bb19…`) |
| `KI-W6-I112` | INTEGRATION_ASSESSMENT | (none; CV58–CV63, CH12) | SUPERSEDED_BY_I113 | `KI-W6-WINDOW-AGENT` | `ASG-KI-W6-WA-07` (CV58 pass; failed CV59 diagnostic superseded by DEC-KI-049 eleventh correction — EV-KI-W6-R59) |
| `KI-W6-C122` | CORRECTION | `email_scraper/test/helpers/keyword-intelligence-e2e-harness.js` | ACCEPTED_FOR_INTEGRATION | `KI-W6-C122-LEAF-AGENT` | `ASG-KI-W6-C122` (EV-KI-W6-R60; ending digest `d9a76ceb…`) |
| `KI-W6-C123` | CORRECTION | `frontend/test/browser/keyword-intelligence-e2e.mjs` | ACCEPTED_FOR_INTEGRATION | `KI-W6-C123-LEAF-AGENT` | `ASG-KI-W6-C123` (EV-KI-W6-R61; ending digest `448921c7…`) |
| `KI-W6-I113` | INTEGRATION_ASSESSMENT | (none; CV64–CV69, CH13) | PARENT_BLOCKED | `KI-W6-WINDOW-AGENT` | `ASG-KI-W6-WA-08` (CV64 pass; CV65 deterministic exactly-1-vs-2 seam contract failure — EV-KI-W6-R62/R63; superseded by twelfth correction DEC-KI-050/C124) |
| `KI-W6-I114` | INTEGRATION_ASSESSMENT | (none; CV70–CV75, CH14) | PARENT_BLOCKED | `KI-W6-WINDOW-AGENT` | `ASG-KI-W6-WA-09` (CV70 pass; CV71 failed — EV-KI-W6-R65/R66; superseded by thirteenth correction DEC-KI-051/C125/C126) |
| `KI-W6-I115` | INTEGRATION_ASSESSMENT | (none; CV76–CV79) | PARENT_BLOCKED | `KI-W6-WINDOW-AGENT` | `ASG-KI-W6-WA-10` (CV76/CV77 pass; CV78 failed at first domain-check emission — claimTask hang + teardown Prisma crash — EV-KI-W6-R68) |
| `KI-W6-C127` | CORRECTION | `email_scraper/test/helpers/keyword-intelligence-e2e-harness.js` | ACCEPTED | (delegated leaf) | `ASG-KI-W6-WA-11` (start `c363fb61…` → final `974376b6…`; independent review EV-KI-W6-R69) |
| `KI-W6-C128` | CORRECTION | `frontend/test/browser/keyword-intelligence-e2e.mjs` | ACCEPTED | (delegated leaf) | `ASG-KI-W6-WA-11` (start `0adfd854…` → final `1e7b0c10…`; independent review EV-KI-W6-R70) |
| `KI-W6-I116` | INTEGRATION_ASSESSMENT | (none; CV80–CV83) | PARENT_BLOCKED | `KI-W6-WINDOW-AGENT` | `ASG-KI-W6-WA-11` (CV80 pass; CV81 fail 504 -> E8.1 recovery fail at downstream deadline with complete DEC-KI-052 diagnostics — host CPU starvation, no DB lock — EV-KI-W6-R71) |
| `KI-W6-C129` | DIAGNOSTIC_CORRECTION | `email_scraper/test/helpers/keyword-intelligence-e2e-harness.js` | ACCEPTED | (delegated leaf) | `ASG-KI-W6-WA-12` (start `0b4de997…` → final `1dc83d7e…`; independent review EV-KI-W6-R72) |
| `KI-W6-C130` | DIAGNOSTIC_CORRECTION | `frontend/test/browser/keyword-intelligence-e2e.mjs` | ACCEPTED | (delegated leaf) | `ASG-KI-W6-WA-12` (start `69c13519…` → final `c035094b…`; independent review EV-KI-W6-R73) |
| `KI-W6-I117` | DIAGNOSTIC_ASSESSMENT | (none; I117-D1–D4) | COMPLETE | `KI-W6-WINDOW-AGENT` | `ASG-KI-W6-WA-12` (one causal run localized PIPELINE_LEASE_LOST to coordinator.getCompleteStage via operation seq 303 — EV-KI-W6-R74) |
| `KI-W6-C131` | CORRECTION | `email_scraper/src/aws-pipeline/repositories/pipeline-coordinator-repository.js` | ACCEPTED | (delegated leaf) | `ASG-KI-W6-WA-13` (start `531dc4cf…` → final `b010802e…`; independent review EV-KI-W6-R75) |
| `KI-W6-C132` | CORRECTION | `email_scraper/src/aws-pipeline/services/domain-aggregator.js` | ACCEPTED | (delegated leaf) | `ASG-KI-W6-WA-13` (start `14226be8…` → final `e873bb62…`; independent review EV-KI-W6-R76) |
| `KI-W6-C133` | CORRECTION | `email_scraper/src/aws-pipeline/services/lead-aggregator.js` | ACCEPTED | (delegated leaf) | `ASG-KI-W6-WA-13` (start `8885024d…` → final `c3f2fb24…`; independent review EV-KI-W6-R77) |
| `KI-W6-C134` | CORRECTION | `email_scraper/src/aws-pipeline/services/final-aggregator.js` | ACCEPTED | (delegated leaf) | `ASG-KI-W6-WA-13` (start `fead8c9b…` → final `416e36fe…`; independent review EV-KI-W6-R78) |
| `KI-W6-C135` | CORRECTION | `email_scraper/test/pipeline-coordinator-repository.integration.test.js` | ACCEPTED | (delegated leaf) | `ASG-KI-W6-WA-13` (start `083aa06c…` → final `9689ef9f…`; independent review EV-KI-W6-R79) |
| `KI-W6-I118` | INTEGRATION_ASSESSMENT | (none; R1–R4, H1) | PARENT_BLOCKED | `KI-W6-WINDOW-AGENT` | `ASG-KI-W6-WA-13` (R1 syntax 5/5 + unit 4/4 pass; integration 0/6 at provider quota 53000 in createIsolatedTestSchema — external prerequisite absent; R2–R4 not run — EV-KI-W6-R80) |

Counters: accepted initial file leaves 5/5; accepted window-agent corrective
leaves 6/6 plus parent-executed C110/C111 preserved. The eighth correction is
strictly sequential: `C118 → window review (CV44) → I110 (window-agent
personal: CV45–CV49, CH10) → READY_FOR_PARENT_REVIEW`; parallel leaves are
prohibited.

Boundary: A5 state 164 (`ASG-KI-W6-WA-05`) authorizes exactly this sequence
under the two pinned standards. The window agent performs no implementation
edit, no commit/push, no provider/AWS/production action, and does not begin
KI-W7. Final changed set after C118 (six paths): the five accepted backend
paths (sorted-LF digest
`dd66e44200514702c82ad06da4c93b3dda30596048a1f569d5779642119f8130`,
repository `17e55ed2…`, recovery `714e40da…`, unit test `87c5fa81…`,
integration test `91db4db5…`, recovery test `41240b25…`) plus
`frontend/test/browser/keyword-intelligence-e2e.mjs` (from baseline
`f7f055e6…` per CT14).
