# KI-W7 Sub-Window State (`S2`)

Only `KI-W7-WINDOW-AGENT` may update this machine-scannable state. It contains
no history or evidence. `S1` is the decomposition authority and `S3` is the
append-only evidence authority.

```yaml
state_version: 24
parent_window_id: KI-W7
parent_assignment_id: ASG-KI-W7-WA-02
window_agent_identity: KI-W7-WINDOW-AGENT
parent_standard_path: PROJECT_AGNOSTIC_DECISION_COMPLETE_CHECKLIST_AUTHORING_STANDARD.md
parent_standard_revision: cda352017e75c0d11f6797d9fbe108b4365508cd38b0e92365cfb523ede32848
subwindow_standard_path: PROJECT_AGNOSTIC_WINDOW_AGENT_SUBWINDOW_AUTHORING_STANDARD.md
subwindow_standard_revision: 842c29550c06c22d63e0a058a27cb8a9ff6b538b3168d2c83a384890b44247f0
parent_contract_revision: 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c
parent_decision_revision: 6c0809225ba5336dc923786674b990f83c8db2496b88016f7655a770afb7e307
parent_checklist_revision: 4a47d782223e372d2df7d653add494880eddf456ab3f4d63439fea2ed1c2374e
parent_state_path: ACTIVE_EXECUTION_STATE.md
parent_state_version: 196
parent_state_revision: 078f9aa9a42447c2eea5d409dab4cfb68a97fd5d7e8583b2086bf4f1bdfebd8d
decomposition_path: KEYWORD_INTELLIGENCE_KI_W7_SUBWINDOW_CHECKLIST.md
decomposition_revision: ad88ab2430f6d3046f1a41271f93a8f5435669d12cfe071f84f47dcc6c55802e
evidence_path: KEYWORD_INTELLIGENCE_KI_W7_SUBWINDOW_EVIDENCE.md
decomposition_status: READY
current_subwindow: KI-W7-I003
current_assignment_id: ASG-KI-W7-I003-01
assigned_agent: KI-W7-WINDOW-AGENT
subwindow_type: INTEGRATION_REASSESSMENT
authorized_write_file: NONE
authorized_read_scope: [A1-A8, KI-W7 S1-S3, all thirteen W7 paths and build outputs, email_scraper/test/aws-pipeline-infrastructure.test.js, email_scraper/test/aws-pipeline-packaging.test.js, email_scraper/scripts/measure-lambda-packages.js]
authorized_actions: [record the I003 blocker and stop for parent scope and gate adjudication]
prohibited_actions: [implementation edit, database browser network provider AWS paid action, credential value read, schema package frontend or unlisted edit, commit, push, KI-W8]
execution_environment_policy:
  sandbox_escalation_for_authorized_local_actions: true
  automatic_identical_recovery_after_proven_environment_invalidation: true
  recovery_limit_per_invalidated_execution: 1
  external_authority_expansion: false
parallel_execution_policy:
  dependency_strata: [[KI-W7-S001, KI-W7-S002, KI-W7-S003, KI-W7-S004, KI-W7-S005, KI-W7-S006], [KI-W7-S007, KI-W7-S008], [KI-W7-S009, KI-W7-S010, KI-W7-S011, KI-W7-S012, KI-W7-S013]]
  concurrently_authorized_waves: []
  executable_schedule: SERIAL
may_start_successor: false
current_status: BLOCKED
accepted_subwindows: [KI-W7-S001, KI-W7-S002, KI-W7-S003, KI-W7-S004, KI-W7-S005, KI-W7-S006, KI-W7-S007, KI-W7-S008, KI-W7-S009, KI-W7-S010, KI-W7-S011, KI-W7-S012, KI-W7-S013]
next_subwindow: STOP_PARENT_DECISION
blocker: "CV5 exposed one parent-scope regression-compatibility omission: the preserved infrastructure test retains four pre-W7 topology counts, and CV3 omitted the established measurement producer required by the preserved packaging tests. Parent authorization is required for one exact-file C003 plus a corrected I004 gate schedule."
last_updated: 2026-08-24T18:00:00+05:30
```
