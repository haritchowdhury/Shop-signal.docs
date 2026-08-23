state_version: 185
standard_path: PROJECT_AGNOSTIC_DECISION_COMPLETE_CHECKLIST_AUTHORING_STANDARD.md
standard_revision: cda352017e75c0d11f6797d9fbe108b4365508cd38b0e92365cfb523ede32848
subwindow_standard_path: PROJECT_AGNOSTIC_WINDOW_AGENT_SUBWINDOW_AUTHORING_STANDARD.md
subwindow_standard_revision: 842c29550c06c22d63e0a058a27cb8a9ff6b538b3168d2c83a384890b44247f0
standard_adoption: KI-R5 is accepted; KI-W6 remains active; the parent-corrected transaction-clock decomposition revision eda1bd4f is approved for the two exact waves and sequential I119 assessment under DEC-KI-053; KI-W7 remains prohibited
contract_path: KEYWORD_INTELLIGENCE_PRODUCT_CONTRACT.md
contract_revision: 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c
decision_path: KEYWORD_INTELLIGENCE_DECISION_LEDGER.md
decision_revision: 2b2d75b9ebb94ae80d3cc7241ce69a2aa92a22efa755b1497887018950ccf406
checklist_path: KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md
checklist_revision: 679e9a7d986775d60fa9f2a9b7cd9568084652534c857f7109482426653b1d36
current_window: KI-W6
current_assignment_id: ASG-KI-W6-WA-14
assigned_agent: KI-W6-WINDOW-AGENT
authorized_windows: [KI-W6]
decomposition_target_path: KEYWORD_INTELLIGENCE_KI_W6_SUBWINDOW_CHECKLIST.md
decomposition_target_starting_revision: a0e3e28b7d9e272cfa6b1eec79f224d2b156725d7ebc86b729bfe3067dd42d87
subwindow_state_target_path: KEYWORD_INTELLIGENCE_KI_W6_TRANSACTION_CLOCK_SUBWINDOW_STATE.md
subwindow_evidence_target_path: KEYWORD_INTELLIGENCE_KI_W6_TRANSACTION_CLOCK_SUBWINDOW_EVIDENCE.md
historical_decomposition_read_only: KEYWORD_INTELLIGENCE_KI_W6_REAUTHORED_SUBWINDOW_CHECKLIST.md@86b56ecaa579da2e4ec305c7c4800bbfb7b2666489dd9ceab72ca8ef0f11bc57
approved_decomposition_revision: eda1bd4ff887780f00f6aa7721f308b738505bed8dbcf9d6cb5d13cedaa6ef40
approved_subwindow_state_revision: f288b11036e8d462a7c1025c1f2a122d8b7d29baaa88fefc99a08c1618e716ee
approval_evidence: [EV-KI-W6-TC03, EV-KI-A-111]
authorized_write_scope: [email_scraper/src/aws-pipeline/repositories/pipeline-coordinator-repository.js through KI-W6-C136 only, email_scraper/src/prisma-run-repository.js through KI-W6-C137 only, email_scraper/src/aws-pipeline/services/domain-aggregator.js through KI-W6-C138 only, email_scraper/src/aws-pipeline/services/lead-aggregator.js through KI-W6-C139 only, email_scraper/src/aws-pipeline/services/final-aggregator.js through KI-W6-C140 only, email_scraper/test/pipeline-coordinator-repository.test.js through KI-W6-C141 only, email_scraper/test/aws-pipeline-transaction-clock-enforcement.test.js through KI-W6-C142 only, email_scraper/test/aws-pipeline-lead-aggregation.integration.test.js through KI-W6-C143 only, email_scraper/test/aws-pipeline-final.integration.test.js through KI-W6-C144 only, KEYWORD_INTELLIGENCE_KI_W6_SUBWINDOW_CHECKLIST.md append-only corrective blocks C145+ if required, KEYWORD_INTELLIGENCE_KI_W6_TRANSACTION_CLOCK_SUBWINDOW_STATE.md window-agent state transitions, KEYWORD_INTELLIGENCE_KI_W6_TRANSACTION_CLOCK_SUBWINDOW_EVIDENCE.md append-only execution/review/integration evidence]
authorized_actions: [window agent records and dispatches all five KI-W6-WAVE-1 leaves in parallel, leaf agents implement only their literal one-file blocks and return only to the window agent, window agent independently reviews every wave-1 leaf and accepts all five before dispatching wave 2, window agent records and dispatches all four KI-W6-WAVE-2 leaves in parallel, leaf agents execute only their literal one-file blocks including the two isolated-schema local gates, window agent independently reviews every wave-2 leaf, diagnose any in-scope defect and append decision-complete execution-complete one-file C145+ corrections plus I120+ reassessment without parent return when DEC-KI-053 already determines the remedy, execute KI-W6-I119 sequentially after all nine leaves are accepted, run CV84 through CV90 and CH15 in exact order with one identical E8.1 recovery only after proven environment invalidation, update S2 and append S3 evidence, stop at READY_FOR_PARENT_REVIEW]
prohibited_actions: [any file outside the exact nine implementation/test paths and three subordinate coordination artifacts, any leaf edit to S1 S2 S3 A1-A8 or A5, any window-agent implementation edit, any overlapping or dependency-violating parallel assignment, wave 2 before all wave-1 leaves are independently accepted, integration assessment in parallel or before all wave-2 leaves are independently accepted, provider calls, AWS operations, production database writes, schema or migration changes, package or configuration changes, frontend edits, paid or destructive actions, raw secret token cookie connection SQL provider body keyword or user-data evidence, commits or pushes, parent acceptance claims, KI-W7 work]
execution_environment_policy:
  sandbox_escalation_for_authorized_local_actions: true
  automatic_identical_recovery_after_proven_environment_invalidation: true
  recovery_limit_per_invalidated_execution: 1
  external_authority_expansion: false
parallel_execution_policy:
  permitted_waves: [KI-W6-WAVE-1, KI-W6-WAVE-2]
  wave_1_members: [KI-W6-C136, KI-W6-C137, KI-W6-C138, KI-W6-C139, KI-W6-C140]
  wave_2_members: [KI-W6-C141, KI-W6-C142, KI-W6-C143, KI-W6-C144]
  wave_2_requires: [every wave-1 leaf independently accepted by window agent]
  integration_assessment_parallel: false
  implied_parallel_authority: false
may_start_successor: false
current_status: READY
accepted_through: KI-R5
next_window: KI-W6
stop_after: KI-W6-WINDOW-AGENT-HANDOFF
blocker: null
user_gates: []
last_updated: 2026-08-23T19:30:00+05:30
