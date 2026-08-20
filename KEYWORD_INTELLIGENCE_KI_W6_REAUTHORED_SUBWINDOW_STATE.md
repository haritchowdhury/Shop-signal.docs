# KI-W6 Reauthored Sub-Window State (`S2`)

Mechanical state file. Only `KI-W6-WINDOW-AGENT` writes it, only inside the
`ASG-KI-W6-WA-02` coordination scope (the three `REAUTHORED` artifacts).
Parent artifacts (`A1`–`A8`) are never modified here. This file records no
evidence and no history; see `S3`
(`KEYWORD_INTELLIGENCE_KI_W6_REAUTHORED_SUBWINDOW_EVIDENCE.md`). Decomposition
authority lives in `S1`
(`KEYWORD_INTELLIGENCE_KI_W6_REAUTHORED_SUBWINDOW_CHECKLIST.md`).

```yaml
state_version: 7
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-02
window_agent_identity: KI-W6-WINDOW-AGENT
parent_standard_path: PROJECT_AGNOSTIC_DECISION_COMPLETE_CHECKLIST_AUTHORING_STANDARD.md
parent_standard_revision: cda352017e75c0d11f6797d9fbe108b4365508cd38b0e92365cfb523ede32848
subwindow_standard_path: PROJECT_AGNOSTIC_WINDOW_AGENT_SUBWINDOW_AUTHORING_STANDARD.md
subwindow_standard_revision: 84e7590e74589f308c70dc9b0b67f7e9da395fafb1e5786202ecd1ca15be56e9
parent_contract_revision: 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c
parent_decision_revision: ef4153677807c80dfa9a09c0ffe0ba5a5127681fe6706e17ff6cd48869fdbd31
parent_checklist_revision: 8fe18271bf368a283246d55807dcc4612e118c725e5aabeb6188962a7abf5f4e
parent_state_path: ACTIVE_EXECUTION_STATE.md
parent_state_revision: 162221c05be37ac06bb8cf742dffb39bb6e3bbae124a2b25dbcc4ab2e39a4046
decomposition_path: KEYWORD_INTELLIGENCE_KI_W6_REAUTHORED_SUBWINDOW_CHECKLIST.md
decomposition_revision: bf92d2515a3dde37e7e577308ee69b224fe21498434ef831612536a841475134
evidence_path: KEYWORD_INTELLIGENCE_KI_W6_REAUTHORED_SUBWINDOW_EVIDENCE.md
decomposition_status: READY
current_subwindow: NONE
current_assignment_id: NONE
assigned_agent: UNASSIGNED
subwindow_type: NONE
authorized_write_file: NONE
authorized_read_scope: []
authorized_actions: [assign KI-W6-S101 to one named leaf agent, then manage only the approved strict sequence and independent reviews defined by S1, author one-file corrective leaves only inside the parent five-file scope for already-decided implementation defects, execute I101 only after all five leaves are accepted, return READY_FOR_PARENT_REVIEW]
prohibited_actions: [window-agent implementation-file edits, parallel or out-of-order leaves, multi-file leaves, direct parent-leaf communication, leaf subdelegation, edits to A1-A8 or any parent artifact, reuse or citation of the invalidated state-108 KI-W6 decomposition, KI-W7 work, provider calls, AWS operations, production database writes, destructive shared cleanup, commits/pushes, gate repetition outside approved invalidation and sandbox-recovery rules]
execution_environment_policy:
  sandbox_escalation_for_authorized_local_actions: true
  automatic_identical_recovery_after_proven_environment_invalidation: true
  recovery_limit_per_invalidated_execution: 1
  external_authority_expansion: false
may_start_successor: false
current_status: READY
accepted_subwindows: []
next_subwindow: KI-W6-S101
blocker: null
last_updated: 2026-08-20T23:00:00+05:30
```

## Sub-window registry

| ID | Type | File | Status | Assigned agent | Assignment ID |
|---|---|---|---|---|---|
| `KI-W6-S101` | FILE | `frontend/components/keyword-intelligence/research-dashboard.tsx` | NOT_STARTED | UNASSIGNED | `ASG-KI-W6-S101` (reserved) |
| `KI-W6-S102` | FILE | `frontend/test/browser/keyword-intelligence-dashboard.mjs` | NOT_STARTED | UNASSIGNED | `ASG-KI-W6-S102` (reserved) |
| `KI-W6-S103` | FILE | `email_scraper/test/helpers/keyword-intelligence-e2e-harness.js` | NOT_STARTED | UNASSIGNED | `ASG-KI-W6-S103` (reserved) |
| `KI-W6-S104` | FILE | `email_scraper/test/fixtures/keyword-intelligence/ki-w6-enforcement-manifest-v1.json` | NOT_STARTED | UNASSIGNED | `ASG-KI-W6-S104` (reserved) |
| `KI-W6-S105` | FILE | `frontend/test/browser/keyword-intelligence-e2e.mjs` | NOT_STARTED | UNASSIGNED | `ASG-KI-W6-S105` (reserved) |
| `KI-W6-I101` | INTEGRATION_ASSESSMENT | (none; gates V1–V6) | NOT_STARTED | RESERVED (`KI-W6-WINDOW-AGENT`) | NONE |

Counters: accepted 0/5 file leaves; corrections 0; integration assessments
0/1; no leaf assigned. Planned five-path set digest
`d28ae17864073639580d7650bb03c03474d5370a5034b632cf412e1e3cf3d0bb`;
execution order `S101 → S102 → S103 → S104 → S105 → I101` (strictly
sequential; parallel leaves prohibited).

Boundary: this is the parent-approved fifth-corrected decomposition package
(`KI-W6-REAUTHORED-DECOMP-6`) reconciled under A5 state 147 to A4
`KI-CL-20` after `EV-KI-A-082` `F1`–`F5`, `EV-KI-A-083` `F6`–`F9`,
`EV-KI-A-084` `F10`–`F12`, `EV-KI-A-085` `F13`, and `EV-KI-A-086` `F14`;
it supersedes the unapproved DECOMP-1/2/3/4/5 drafts, whose claims and
certificates are historical only. The package
was approved by `EV-KI-A-087` and A5 state 148. `decomposition_status: READY`;
the next permitted action is window-agent assignment of S101 to one named leaf
agent. No implementation leaf has yet been assigned or dispatched. Only the
parent performs git commits. The
requester provides/validates the isolated `TEST_DATABASE_URL` opt-in for V3;
sandbox escalation for already-authorized local commands is standing per the
inherited E8.1 policy above.
