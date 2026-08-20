# KI-R4 Active Sub-Window State (`S2`)

```yaml
state_version: 12
parent_window_id: KI-R4
parent_assignment_id: ASG-KI-R4-WA-01
window_agent_identity: KI-R4-WINDOW-AGENT
parent_standard_path: PROJECT_AGNOSTIC_DECISION_COMPLETE_CHECKLIST_AUTHORING_STANDARD.md
parent_standard_revision: 3b7a4fd25156e1adfbc92abb835c5f82a0d18c686b1c1150feb202f2d944d2ac
subwindow_standard_path: PROJECT_AGNOSTIC_WINDOW_AGENT_SUBWINDOW_AUTHORING_STANDARD.md
subwindow_standard_revision: 1766f9107ce7d315877b75d4b0ea2b5521dff1c321e12f890b03787d66196ded
parent_contract_revision: 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c
parent_decision_revision: 4b2202d870da5df64ae324ad570adf1b6437689883cb49b118bcc8d1f170d9de
parent_checklist_revision: 310011aa3d855cd4ce4d6ef5054d94e5b8f413b8b86543048fea065113a10cf6
decomposition_path: KEYWORD_INTELLIGENCE_KI_R4_SUBWINDOW_CHECKLIST.md
decomposition_revision: 91b499cc2885937b23daa3186709ca2e0720c939435e4588b4050e2503abcd85
evidence_path: KEYWORD_INTELLIGENCE_KI_R4_SUBWINDOW_EVIDENCE.md
decomposition_status: READY
current_subwindow: KI-R4-I002
current_assignment_id: ASG-KI-R4-WA-01
assigned_agent: KI-R4-WINDOW-AGENT
subwindow_type: INTEGRATION_ASSESSMENT
authorized_write_file: NONE
authorized_read_scope: [KEYWORD_INTELLIGENCE_KI_R4_SUBWINDOW_CHECKLIST.md, KEYWORD_INTELLIGENCE_KI_R4_SUBWINDOW_EVIDENCE.md]
authorized_actions: [return READY_FOR_PARENT_REVIEW handoff]
prohibited_actions: [S1 section 1 prohibitions]
may_start_successor: false
current_status: READY_FOR_PARENT_REVIEW
accepted_subwindows: [KI-R4-S001, KI-R4-S002, KI-R4-S003, KI-R4-S004, KI-R4-S005, KI-R4-S006, KI-R4-S007, KI-R4-S008]
next_subwindow: STOP
blocker: null
last_updated: 2026-08-19T00:55:00+05:30
```

The decomposition is parent-approved (S1 `91b499cc…`). All eight leaves
accepted. `KI-R4-I001` PASS was superseded after parent review
`CORRECTION_REQUIRED` (`EV-KI-R4-S17`): under requester direct-fix
authorization the window agent applied the W05/G01 unchanged-oracle corrections
and corrected the 116-ID combined digest to
`203919cc95a56f664035a633e04bda72059e9d5b577bd3ec911e03be42bc740a` —
`EV-KI-R4-S18` records the superseding `KI-R4-I002` PASS (G-V2 124/0/0, G-V5
627/0/67 + secrets clean, G-V3/G-V4 reused with dependency proof). Two
corrected test files remain uncommitted for the requester; parent acceptance,
A5 CAS, A6 entry, and KI-W4 assignment are parent-only.