state_version: 15
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-15
window_agent_identity: KI-W6-WINDOW-AGENT
parent_standard_path: PROJECT_AGNOSTIC_DECISION_COMPLETE_CHECKLIST_AUTHORING_STANDARD.md
parent_standard_revision: cda352017e75c0d11f6797d9fbe108b4365508cd38b0e92365cfb523ede32848
subwindow_standard_path: PROJECT_AGNOSTIC_WINDOW_AGENT_SUBWINDOW_AUTHORING_STANDARD.md
subwindow_standard_revision: 842c29550c06c22d63e0a058a27cb8a9ff6b538b3168d2c83a384890b44247f0
parent_contract_revision: 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c
parent_discovery_revision: 425bedd9a7f429e2b145559d6d408fd161260a025382e047900f2112355316e0
parent_decision_revision: b8a5190b614967be2369e75c3a4e5aa49cfc8f21d9112fc984ab7387b1aca60f
parent_checklist_revision: 86914c48562e69fe08007930ab3973dc5dfa28f743bef3d98eb89a1ebc2d7e5d
parent_traceability_revision: 6e0b8fe0cc56917a3d4397fd6b3260b869a8045a3f39906e8aafcead0d17f5f2
parent_active_state_version: 188
parent_active_state_revision: 4bf0e6adbe159a89086c99e285be75ebbb45d046ef0ed270f0165c264f6bda01
decomposition_path: KEYWORD_INTELLIGENCE_KI_W6_SUBWINDOW_CHECKLIST.md
approved_base_decomposition_revision: 1ab97a1a6bb66c400b31a5cc450ca94d515e96021588265789d26b2dea0b38cc
decomposition_revision: 8f95bafc5f2965ae384a181b42d585dfc85f57c2a23ecf987554a2423ba47141
protocol_supersession: DEC-KI-055 under A5 state 188; no new decomposition review required
evidence_path: KEYWORD_INTELLIGENCE_KI_W6_TRANSACTION_CLOCK_SUBWINDOW_EVIDENCE.md
decomposition_status: BLOCKED
parent_approval_state: 188
parent_approval_evidence: [EV-KI-A-113, CHG-KI-085, EV-KI-A-114, CHG-KI-086]
current_subwindow: KI-W6-I120
current_assignment_id: ASG-KI-W6-I120
assigned_agent: KI-W6-WINDOW-AGENT
subwindow_type: INTEGRATION_ASSESSMENT
authorized_write_file: NONE
authorized_read_scope: [ACTIVE_EXECUTION_STATE.md state 188, KEYWORD_INTELLIGENCE_KI_W6_SUBWINDOW_CHECKLIST.md sections 12.8 and 13, accepted C145-C148 files, exact CV93 dependency inputs, backend and frontend regression/build/browser inputs]
authorized_actions: [personally execute CV91 through CV97 and CH16 sequentially, write only S2/S3 evidence and state, use exact E8.1 policy]
prohibited_actions: [implementation/test/frontend/parent-artifact edit, provider AWS production non-isolated-database paid destructive action, commit or push, successor work, KI-W7]
execution_environment_policy:
  sandbox_escalation_for_authorized_local_actions: true
  automatic_identical_recovery_after_proven_environment_invalidation: true
  recovery_limit_per_invalidated_execution: 1
  external_authority_expansion: false
parallel_execution_policy:
  permitted_wave: KI-W6-WAVE-3
  members: [KI-W6-C146, KI-W6-C147]
  requires: [KI-W6-C145 independently accepted]
  dependent_barrier: [KI-W6-C146 and KI-W6-C147 independently accepted before KI-W6-C148]
  integration_assessment_parallel: false
  implied_parallel_authority: false
may_start_successor: false
current_status: PARENT_BLOCKED
accepted_subwindows: [KI-W6-C136, KI-W6-C137, KI-W6-C138, KI-W6-C139, KI-W6-C140, KI-W6-C141, KI-W6-C142, KI-W6-C143, KI-W6-C144, KI-W6-C145, KI-W6-C146, KI-W6-C147, KI-W6-C148]
superseded_failed_assessments: [KI-W6-CV87 superseded by DEC-KI-054 implementation and CV91-CV93]
preserved_assessment_results: [KI-W6-CV84 PASS, KI-W6-CV85 PASS, KI-W6-CV86 PASS, KI-W6-CV91 PASS, KI-W6-CV92 PASS, KI-W6-CV93 PASS]
failed_assessment_results: [KI-W6-CV94 PARENT_BLOCKED after one sandbox-invalid attempt and one observable elevated recovery]
next_subwindow: NONE
blocker: CV94's first-domain-check witness searches SQS message type prefix "domain", but the frozen production contract emits the discovery aggregation check as type "aggregation.check"; the recovery completed 100 discovery tasks plus 100 checks and fulfilled the drain, yet the impossible predicate never matched. Correcting frontend/test/browser/keyword-intelligence-e2e.mjs is outside DEC-KI-054's four-file scope and I120's zero-write authority.
last_updated: 2026-08-23T20:53:04+05:30
