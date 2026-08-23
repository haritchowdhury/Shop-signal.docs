state_version: 34
parent_window_id: KI-W6
parent_assignment_id: NONE
window_agent_identity: NONE
parent_standard_path: PROJECT_AGNOSTIC_DECISION_COMPLETE_CHECKLIST_AUTHORING_STANDARD.md
parent_standard_revision: cda352017e75c0d11f6797d9fbe108b4365508cd38b0e92365cfb523ede32848
subwindow_standard_path: PROJECT_AGNOSTIC_WINDOW_AGENT_SUBWINDOW_AUTHORING_STANDARD.md
subwindow_standard_revision: 842c29550c06c22d63e0a058a27cb8a9ff6b538b3168d2c83a384890b44247f0
parent_contract_revision: 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c
parent_discovery_revision: 022bd827f4827d3d543f48b502a6a5cbe5f74dbd54dd47b86b622463100a8d15
parent_decision_revision: 4c32d520e379347f32046aae735ebe012f9c421d65e9faa67127e70f72e74747
parent_checklist_revision: f177e81f1b40e4789fc7c0540685b15565e73145bc943ef4369629f8e59e5130
parent_traceability_revision: 36fe0aa2667f3cfa3091ddeca74c3d3c08720bd80a97d781d1c1b6c29d24f289
parent_active_state_version: 193
parent_active_state_revision: d7715931685f421adfdeb931d73a797a258d831dad606dafdb87fe6612dd230f
decomposition_path: KEYWORD_INTELLIGENCE_KI_W6_SUBWINDOW_CHECKLIST.md
approved_base_decomposition_revision: 1ab97a1a6bb66c400b31a5cc450ca94d515e96021588265789d26b2dea0b38cc
decomposition_revision: 7fc3a66648c7625f9843bcb10bc5ddad8625033125aeba39e1f0c70db04ca63f
protocol_supersession: DEC-KI-058 supersedes only I123 CV107's synthetic storefront 1000-domain assertion and parent-authors C152 C153 C154 I124; no decomposition or decomposition-review stop remains
evidence_path: KEYWORD_INTELLIGENCE_KI_W6_TRANSACTION_CLOCK_SUBWINDOW_EVIDENCE.md
decomposition_status: COMPLETE
parent_approval_state: 193
parent_approval_evidence: [requester direct closure instruction, KI-W6 section 19, EV-KI-W6-TC44, EV-KI-A-118]
current_subwindow: KI-W6-I126
current_assignment_id: NONE
assigned_agent: NONE
subwindow_type: INTEGRATION_ASSESSMENT
authorized_write_file: NONE
authorized_read_scope: []
authorized_actions: []
prohibited_actions: [all successor or mutation work without a new explicit parent assignment]
execution_environment_policy:
  sandbox_escalation_for_authorized_local_actions: true
  automatic_identical_recovery_after_proven_environment_invalidation: true
  recovery_limit_per_invalidated_execution: 1
  external_authority_expansion: false
parallel_execution_policy:
  permitted_wave: KI-W6-WAVE-4
  members: [KI-W6-C153, KI-W6-C154]
  requires: [KI-W6-C152 independently accepted]
  dependent_barrier: [KI-W6-C153 and KI-W6-C154 independently accepted before KI-W6-I124]
  integration_assessment_parallel: false
  implied_parallel_authority: false
may_start_successor: false
current_status: COMPLETE
accepted_subwindows: [KI-W6-C136, KI-W6-C137, KI-W6-C138, KI-W6-C139, KI-W6-C140, KI-W6-C141, KI-W6-C142, KI-W6-C143, KI-W6-C144, KI-W6-C145, KI-W6-C146, KI-W6-C147, KI-W6-C148, KI-W6-C149, KI-W6-C150, KI-W6-C151, KI-W6-C152, KI-W6-C153, KI-W6-C154, KI-W6-C155, KI-W6-C156, KI-W6-C157]
superseded_failed_assessments: [KI-W6-CV87 superseded by DEC-KI-054, KI-W6-CV94 superseded by C149, KI-W6-CV99 superseded by C150, KI-W6-CV103 superseded by C151, KI-W6-CV107 synthetic-storefront scale assertion superseded by DEC-KI-058 and pending SCN-KI-046]
preserved_assessment_results: [KI-W6-CV84 PASS, KI-W6-CV85 PASS, KI-W6-CV86 PASS, KI-W6-CV91 PASS, KI-W6-CV92 PASS, KI-W6-CV93 PASS, KI-W6-CV98 PASS, KI-W6-CV102 PASS, KI-W6-CV106 PASS, I123 browser causality through durable handoff 100 validation calls and 100 discovery dispatches, CV112 PASS 100 queries to 1000 domains, CV113 PASS compositional evidence]
failed_assessment_results: [KI-W6-CV107 diagnostic zero-domain result superseded by SRC-KI-059 and CV112, I125 CV114 four source-oracle failures superseded by C156 C157 and I126]
next_subwindow: NONE
blocker: null
planned_changed_files: [email_scraper/src/aws-pipeline/services/discovery-worker.js, email_scraper/test/aws-pipeline-discovery.test.js, email_scraper/test/aws-pipeline-domain.integration.test.js]
planned_file_set_digest: 36780bc47b3e5950c707525292655be1a10d8b39cbeff69ccea1023dcc5074e1
planned_cases: [W6-DB-13, W6-DB-14, W6-DB-15]
planned_controls: [W6-NC-22, W6-NC-23, W6-NC-24]
unmapped_requirements: 0
unmapped_decisions: 0
unmapped_tasks: 0
unmapped_cases: 0
unmapped_controls: 0
unresolved_interfaces: 0
unresolved_intermediate_states: 0
unresolved_execution_choices: 0
unresolved_evidence_references: 0
final_parent_corrective_files: [email_scraper/test/aws-pipeline-transaction-clock-enforcement.test.js, email_scraper/test/prisma-run-repository.integration.test.js]
final_parent_corrective_hashes: [aba0cf3697d13fcbf32f0abbe6271dd3929d7960583bf5ea001bf04391c8e8d6, cb92f1dfa11887e74b846f7b1f611e14487b69e5bd671c4053c53bd07bf5e897]
final_gates: [focused 11 pass 0 fail 2 guarded skips, npm test 697 pass 0 fail 73 guarded skips, check secrets PASS, build lambda PASS, cases 43 digest 5ef52fb9ed7a7cc182302cd2c2441712f5745f52948c4fb1f10b6e759c4dbe71, controls 24 digest 3bd895f41f3689c1c1d421d1ea0056c095e1d4cd57d3f90e3987f79104719707]
last_updated: 2026-08-24T04:15:00+05:30
