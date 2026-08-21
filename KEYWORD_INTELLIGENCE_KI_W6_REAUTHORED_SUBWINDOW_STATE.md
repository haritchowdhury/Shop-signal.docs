# KI-W6 Reauthored Sub-Window State (`S2`)

Mechanical state file. Only `KI-W6-WINDOW-AGENT` writes it, only inside the
`ASG-KI-W6-WA-02` coordination scope (the three `REAUTHORED` artifacts).
Parent artifacts (`A1`–`A8`) are never modified here. This file records no
evidence and no history; see `S3`
(`KEYWORD_INTELLIGENCE_KI_W6_REAUTHORED_SUBWINDOW_EVIDENCE.md`). Decomposition
authority lives in `S1`
(`KEYWORD_INTELLIGENCE_KI_W6_REAUTHORED_SUBWINDOW_CHECKLIST.md`).

```yaml
state_version: 27
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-02
window_agent_identity: KI-W6-WINDOW-AGENT
parent_standard_path: PROJECT_AGNOSTIC_DECISION_COMPLETE_CHECKLIST_AUTHORING_STANDARD.md
parent_standard_revision: cda352017e75c0d11f6797d9fbe108b4365508cd38b0e92365cfb523ede32848
subwindow_standard_path: PROJECT_AGNOSTIC_WINDOW_AGENT_SUBWINDOW_AUTHORING_STANDARD.md
subwindow_standard_revision: 84e7590e74589f308c70dc9b0b67f7e9da395fafb1e5786202ecd1ca15be56e9
parent_contract_revision: 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c
parent_decision_revision: 4d7e4aa311286d997b2498f7af46fa0a32426d1cbace5e1d1f3db340009168b7
parent_checklist_revision: d47d0dd73b7efd357a7fc196ee64bfba2c2e5b0e4f818ea6e8180054e1f36eae
parent_state_path: ACTIVE_EXECUTION_STATE.md
parent_state_revision: 199870af4d0dbf03153316abb29acbd4d68151da87a9368517aa54270aad5123
decomposition_path: KEYWORD_INTELLIGENCE_KI_W6_REAUTHORED_SUBWINDOW_CHECKLIST.md
decomposition_revision: b99633447c17163f6e883d71388b0200a345d2c0ced51252b8d03a8fba3b6b38
evidence_path: KEYWORD_INTELLIGENCE_KI_W6_REAUTHORED_SUBWINDOW_EVIDENCE.md
decomposition_status: READY
integration: 'I103 CV7/CV8 remain accepted. R33 is an observable causal browser-flow failure, superseded only by state-156 C107: one page-aware helper correction followed by I104. C107 is dispatched; I104 remains reserved until independent C107 acceptance.'
current_subwindow: KI-W6-C107
current_assignment_id: ASG-KI-W6-C107
assigned_agent: KI-W6-C107-LEAF-AGENT
subwindow_type: CORRECTION
authorized_write_file: frontend/test/browser/keyword-intelligence-e2e.mjs::swapOneSelectionItemViaUi
authorized_read_scope: [KEYWORD_INTELLIGENCE_PRODUCT_CONTRACT.md, KEYWORD_INTELLIGENCE_DECISION_LEDGER.md §DEC-KI-041, KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md §KI-W6 third in-flight corrective amendment, ACTIVE_EXECUTION_STATE.md, frontend/components/keyword-intelligence/keyword-table.tsx::KeywordTable, frontend/components/keyword-intelligence/research-dashboard.tsx::ResearchDashboard, frontend/lib/keyword-intelligence-view-model.ts::emptyKeywordFilterState/paginate, KEYWORD_INTELLIGENCE_KI_W6_REAUTHORED_SUBWINDOW_EVIDENCE.md::EV-KI-W6-R33]
authorized_actions: [perform KI-W6-CT4 in the one writable symbol, run node --check test/browser/keyword-intelligence-e2e.mjs once from frontend, run git diff --check -- test/browser/keyword-intelligence-e2e.mjs once from frontend, return evidence only to the window agent, stop for independent review]
prohibited_actions: [second-symbol or second-file edit, browser build database full-test provider AWS production commit push parent communication subdelegation successor or KI-W7 action]
execution_environment_policy:
  sandbox_escalation_for_authorized_local_actions: true
  automatic_identical_recovery_after_proven_environment_invalidation: true
  recovery_limit_per_invalidated_execution: 1
  external_authority_expansion: false
may_start_successor: false
current_status: DISPATCHED
accepted_subwindows: [KI-W6-S101, KI-W6-S102, KI-W6-S103, KI-W6-S104, KI-W6-S105, KI-W6-C104, KI-W6-C105, KI-W6-C106]
next_subwindow: KI-W6-I104 after independent C107 acceptance only
blocker: null
last_updated: 2026-08-21T15:09:13+05:30
```

## Sub-window registry

| ID | Type | File | Status | Assigned agent | Assignment ID |
|---|---|---|---|---|---|
| `KI-W6-S101` | FILE | `frontend/components/keyword-intelligence/research-dashboard.tsx` | ACCEPTED | `KI-W6-S101-LEAF-AGENT` | `ASG-KI-W6-S101` (executed; certificate + `EV-KI-W6-R15` in S3) |
| `KI-W6-S102` | FILE | `frontend/test/browser/keyword-intelligence-dashboard.mjs` | ACCEPTED | `KI-W6-S102-LEAF-AGENT` | `ASG-KI-W6-S102` (executed; certificate + `EV-KI-W6-R16` in S3) |
| `KI-W6-S103` | FILE | `email_scraper/test/helpers/keyword-intelligence-e2e-harness.js` | ACCEPTED | `KI-W6-S103-LEAF-AGENT` | `ASG-KI-W6-S103` (executed; certificate + `EV-KI-W6-R17` in S3) |
| `KI-W6-S104` | FILE | `email_scraper/test/fixtures/keyword-intelligence/ki-w6-enforcement-manifest-v1.json` | ACCEPTED | `KI-W6-S104-LEAF-AGENT` | `ASG-KI-W6-S104` (executed; certificate + `EV-KI-W6-R18` in S3) |
| `KI-W6-S105` | FILE | `frontend/test/browser/keyword-intelligence-e2e.mjs` | ACCEPTED | `KI-W6-S105-LEAF-AGENT` | `ASG-KI-W6-S105` (executed; certificate + `EV-KI-W6-R19` in S3) |
| `KI-W6-I101` | INTEGRATION_ASSESSMENT | (none; gates V1–V6) | CORRECTION_REQUIRED | `KI-W6-WINDOW-AGENT` | `ASG-KI-W6-WA-02` (V3 publication witness; superseded by I102) |
| `KI-W6-C104` | CORRECTION | `email_scraper/src/aws-pipeline/keyword-intelligence/service.js` | ACCEPTED_FOR_INTEGRATION | `KI-W6-C104-LEAF-AGENT` | `ASG-KI-W6-C104` (accepted via EV-KI-W6-R26 and state-153 requester-owned provenance disposition) |
| `KI-W6-C105` | CORRECTION | `email_scraper/test/keyword-intelligence-worker-flow.test.js` | ACCEPTED_FOR_INTEGRATION | `KI-W6-C105-LEAF-AGENT` | `ASG-KI-W6-C105` (accepted via independent review; C105-C1/C105-C2 PASS) |
| `KI-W6-I102` | INTEGRATION_ASSESSMENT | (none; CV1–CV6) | PARENT_BLOCKED | `KI-W6-WINDOW-AGENT` | `ASG-KI-W6-WA-02` (CV1 failed; R28 records the parent-level C105 contract contradiction) |
| `KI-W6-C106` | CORRECTION | `email_scraper/test/keyword-intelligence-worker-flow.test.js` | ACCEPTED_FOR_INTEGRATION | `KI-W6-C106-LEAF-AGENT` | `ASG-KI-W6-C106` (C106-C1/C106-C2 pass; independent review in EV-KI-W6-R30) |
| `KI-W6-I103` | INTEGRATION_ASSESSMENT | (none; CV7–CV12) | BLOCKED | `KI-W6-WINDOW-AGENT` | `ASG-KI-W6-WA-02` (CV7/CV8 pass; CV9 execution-channel certificate unavailable) |
| `KI-W6-C107` | CORRECTION | `frontend/test/browser/keyword-intelligence-e2e.mjs::swapOneSelectionItemViaUi` | DISPATCHED | `KI-W6-C107-LEAF-AGENT` | `ASG-KI-W6-C107` (state-156 only; I104 awaits independent review) |
| `KI-W6-I104` | INTEGRATION_ASSESSMENT | (none; CV13–CV18) | RESERVED | `KI-W6-WINDOW-AGENT` | `ASG-KI-W6-WA-02` (starts only after accepted C107) |

Counters: accepted initial file leaves 5/5; accepted corrective leaves 3/4;
integration assessments passed 0/4; C107 is dispatched; I103/CV9 is superseded
diagnostic evidence and I104 is reserved. The accepted five-path history remains
`d28ae17864073639580d7650bb03c03474d5370a5034b632cf412e1e3cf3d0bb`.
The current authorized corrective plan is strictly sequential:
`C107 → independent window review → I104 → READY_FOR_PARENT_REVIEW`; parallel
leaves are prohibited.

Boundary: state 156 / `KI-CL-23` authorizes only C107's page-aware harness
correction and I104. C106/CV7/CV8 remain accepted; no production, schema,
coverage, digest, provider, AWS, commit, push, or KI-W7 action is authorized.
