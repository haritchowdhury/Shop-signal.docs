# KI-W6 Reauthored Sub-Window State (`S2`)

Mechanical state file. Only `KI-W6-WINDOW-AGENT` writes it, only inside the
`ASG-KI-W6-WA-02` coordination scope (the three `REAUTHORED` artifacts).
Parent artifacts (`A1`–`A8`) are never modified here. This file records no
evidence and no history; see `S3`
(`KEYWORD_INTELLIGENCE_KI_W6_REAUTHORED_SUBWINDOW_EVIDENCE.md`). Decomposition
authority lives in `S1`
(`KEYWORD_INTELLIGENCE_KI_W6_REAUTHORED_SUBWINDOW_CHECKLIST.md`).

```yaml
state_version: 22
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-02
window_agent_identity: KI-W6-WINDOW-AGENT
parent_standard_path: PROJECT_AGNOSTIC_DECISION_COMPLETE_CHECKLIST_AUTHORING_STANDARD.md
parent_standard_revision: cda352017e75c0d11f6797d9fbe108b4365508cd38b0e92365cfb523ede32848
subwindow_standard_path: PROJECT_AGNOSTIC_WINDOW_AGENT_SUBWINDOW_AUTHORING_STANDARD.md
subwindow_standard_revision: 84e7590e74589f308c70dc9b0b67f7e9da395fafb1e5786202ecd1ca15be56e9
parent_contract_revision: 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c
parent_decision_revision: e59252cb3798fbdae805f43f33f69bf22de083c67d9a000632f5a1d2208e5a6c
parent_checklist_revision: bb823eca63520b6e0a8cd3b90b37fd9063813ee692c49d5c83bcc355cb1c0025
parent_state_path: ACTIVE_EXECUTION_STATE.md
parent_state_revision: 8e5624d405967500a14a1cf9c1384c70beaeba45bcc615efa37b416adc15bdad
decomposition_path: KEYWORD_INTELLIGENCE_KI_W6_REAUTHORED_SUBWINDOW_CHECKLIST.md
decomposition_revision: b99633447c17163f6e883d71388b0200a345d2c0ced51252b8d03a8fba3b6b38
evidence_path: KEYWORD_INTELLIGENCE_KI_W6_REAUTHORED_SUBWINDOW_EVIDENCE.md
decomposition_status: READY
integration: 'I102 CV1 remains superseded diagnostic evidence. A5 state 154 and KI-CL-22 / DEC-KI-040 prescribe the contract-valid C106 test substitute: five ordered seeds × 60 unique keywords and the exact anchor-stage shortlist-manifest fingerprint. C106 is dispatched; I103 CV7–CV12 follow only after independent C106 acceptance.'
current_subwindow: KI-W6-C106
current_assignment_id: ASG-KI-W6-C106
assigned_agent: KI-W6-C106-LEAF-AGENT
subwindow_type: CORRECTION
authorized_write_file: email_scraper/test/keyword-intelligence-worker-flow.test.js
authorized_read_scope: [KEYWORD_INTELLIGENCE_PRODUCT_CONTRACT.md, KEYWORD_INTELLIGENCE_DECISION_LEDGER.md §DEC-KI-040, KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md §KI-W6 second in-flight corrective amendment, ACTIVE_EXECUTION_STATE.md, email_scraper/src/aws-pipeline/keyword-intelligence/service.js::readManifest, email_scraper/src/aws-pipeline/keyword-intelligence/contracts.js::keywordExpansionManifestSchema, email_scraper/src/aws-pipeline/keyword-intelligence/keys.js::keywordStageInputFingerprint]
authorized_actions: [perform KI-W6-CT3 in the one writable file, run C106-C1 and C106-C2 once, return evidence only to the window agent]
prohibited_actions: [second-file edit, existing R3/R4 assertion or registration edit, production schema package config timeout provider database AWS commit push parent communication subdelegation successor or KI-W7 action, window-agent implementation-file edit, CV7-CV12 before C106 acceptance, edits to A1-A8 or parent artifacts]
execution_environment_policy:
  sandbox_escalation_for_authorized_local_actions: true
  automatic_identical_recovery_after_proven_environment_invalidation: true
  recovery_limit_per_invalidated_execution: 1
  external_authority_expansion: false
may_start_successor: false
current_status: READY
accepted_subwindows: [KI-W6-S101, KI-W6-S102, KI-W6-S103, KI-W6-S104, KI-W6-S105, KI-W6-C104, KI-W6-C105]
next_subwindow: KI-W6-I103 after independent C106 acceptance
blocker: null
last_updated: 2026-08-21T14:30:00+05:30
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
| `KI-W6-C106` | CORRECTION | `email_scraper/test/keyword-intelligence-worker-flow.test.js` | DISPATCHED | `KI-W6-C106-LEAF-AGENT` | `ASG-KI-W6-C106` (state-154 literal KI-CL-22 transcription; awaiting leaf evidence) |
| `KI-W6-I103` | INTEGRATION_ASSESSMENT | (none; CV7–CV12) | RESERVED | `KI-W6-WINDOW-AGENT` | `ASG-KI-W6-WA-02` (begins only after independent C106 acceptance) |

Counters: accepted initial file leaves 5/5; accepted corrective leaves 2/3;
integration assessments passed 0/3; C106 is the sole dispatched correction;
I102 is superseded diagnostic evidence. The accepted five-path history remains
`d28ae17864073639580d7650bb03c03474d5370a5034b632cf412e1e3cf3d0bb`.
The current authorized corrective plan is strictly sequential:
`C106 → window review → I103 → READY_FOR_PARENT_REVIEW`; parallel leaves are
prohibited.

Boundary: state 154 / `KI-CL-22` resolves I102's contract contradiction without
production or schema change. C106 may modify only its assigned test file and
must stop for independent window review. I103 may begin only after that
acceptance and stops `READY_FOR_PARENT_REVIEW`; KI-W7 remains prohibited.
