# KI-W8 Sub-Window Evidence (`S3`)

Append-only subordinate evidence for `KI-W8`. This file records decomposition,
execution and window-agent assessment facts; it cannot authorize an action or
amend A1-A8/S1.

Sibling artifacts:

- `S1`: `KEYWORD_INTELLIGENCE_KI_W8_SUBWINDOW_CHECKLIST.md`
- `S2`: `KEYWORD_INTELLIGENCE_KI_W8_SUBWINDOW_STATE.md`

## `EV-KI-W8-S001` — authority, revision and baseline certificate

```yaml
evidence_id: EV-KI-W8-S001
timestamp: 2026-08-24T15:35:00+05:30
phase: decomposition_authoring
parent_window_id: KI-W8
subwindow_id: KI-W8-DECOMPOSITION
assignment_id: ASG-KI-W8-WA-01
actor: KI-W8-WINDOW-AGENT
role: window_agent
commands:
  - cat ACTIVE_EXECUTION_STATE.md
  - sha256sum A1 A2 A3 A4 A5 A8 and both standards
  - git status --short and git rev-parse HEAD in root backend frontend
  - git diff -- A5 A6 A7
observed:
  a5_state: 200
  parent_assignment: ASG-KI-W8-WA-01
  parent_status: READY
  accepted_through: KI-W7
  root_head: 1d77166817830af0ba5acc4e6fa7fe61dd234795
  backend_head: c3ba835be446ba43e1a80be4f5ab4d28bae89497
  frontend_head: 5e441aae7e2f3a132b2c7fc85bf1bc525d3d5cb6
  backend_dirty_paths: []
  frontend_dirty_paths: []
  root_parent_owned_dirty_paths: [ACTIVE_EXECUTION_STATE.md, KEYWORD_INTELLIGENCE_EXECUTION_EVIDENCE.md, KEYWORD_INTELLIGENCE_SPECIFICATION_CHANGELOG.md]
  root_parent_owned_path_set_digest: de3724531095ca3c8d7ebbb1089b339c8f40927f7a23f8b4b6f6b43b33edc2ce
pins:
  parent_standard: cda352017e75c0d11f6797d9fbe108b4365508cd38b0e92365cfb523ede32848
  subwindow_standard: 842c29550c06c22d63e0a058a27cb8a9ff6b538b3168d2c83a384890b44247f0
  contract: 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c
  discovery: 493192fc317c00ee43e277e85e00718985190cdd5c21e3d6824f67dd1d0b7c0c
  decision: 6c0809225ba5336dc923786674b990f83c8db2496b88016f7655a770afb7e307
  checklist: 4f4b16bbe6ab20312e312db75506f9acfee7aaca67fbb66d1d951676f1f646e4
  traceability: 90c2f808426c4f1cf20ad885860e01b66763f3fc607e28c3b2dd9a2ef7391a5f
  parent_state: a4e08c31469b1c309a58ef52c457a65bcef3b9fe0561d9e60cabb802df4429b3
assertion: every A5 pin recomputed byte-equal; the only entry dirty paths are the parent's state-200 assignment records
sandbox_privilege: none
environment_invalidations: []
external_mutations: []
paid_cost_usd: "0.00"
privacy: no credential secret account value URL customer value or provider body inspected or recorded
status: PASS
```

## `EV-KI-W8-S002` — source, assessment, action and enforcement closure

```yaml
evidence_id: EV-KI-W8-S002
timestamp: 2026-08-24T15:38:00+05:30
phase: decomposition_authoring
parent_window_id: KI-W8
subwindow_id: KI-W8-DECOMPOSITION
assignment_id: ASG-KI-W8-WA-01
actor: KI-W8-WINDOW-AGENT
inspected_primary_sources:
  - KEYWORD_INTELLIGENCE_PRODUCT_CONTRACT.md REQ-KI-002/005/015-017/022-024 INV-KI-001-015 AUTH-KI-005/007 EXC-KI-008
  - KEYWORD_INTELLIGENCE_DECISION_LEDGER.md DEC-KI-059
  - KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md KI-W8 and SCN-KI-048
  - KEYWORD_INTELLIGENCE_TRACEABILITY_INDEX.md section 9
  - email_scraper/scripts/keyword-intelligence/create-change-set.js
  - email_scraper/scripts/keyword-intelligence/inspect-stack.js
  - email_scraper/scripts/measure-keyword-worker-package.js
  - email_scraper/scripts/measure-lambda-packages.js
  - email_scraper/infrastructure/aws/template.yaml
  - email_scraper/src/aws-pipeline/secrets.js
  - email_scraper/src/keyword-intelligence/api.js
  - email_scraper/src/server.js
  - frontend same-origin keyword routes and client-api/dashboard callers
derived_inventory:
  source_leaf_count: 0
  integration_assessment_ids: [KI-W8-I001]
  parallel_waves: []
  planned_implementation_changed_file_set: []
  planned_implementation_changed_file_set_digest: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
  action_ids: [W8-ACT-01, W8-ACT-02, W8-ACT-03, W8-ACT-04, W8-ACT-05, W8-ACT-06, W8-ACT-07]
  required_case_count: 10
  required_case_digest: b716a609b2269f69d4e042503ad47dabb1eb397e17726af850f38ab09940431a
  required_control_count: 6
  required_control_digest: 1a2fd2fb71c94f297b27c5c6ad580c67d94ae807525b420996bd4382d46b7c6e
accepted_packet_inputs:
  template: {bytes: 104582, sha256: 2d87c28ad564842d13e42855aef676fb30b2f3aa357ef6eda73bc88f67cb8fa8}
  keyword_zip: {bytes: 32006605, sha256: 47fda36e621bcb35a98fd1614854dadc0231e70871cf5488828610400d8460d4}
  recovery_zip: {bytes: 31984076, sha256: cc5b6819d80c85a3ca74f05c9887b580aa8dd498f1f866ffc8e812ce89f2bb9c}
closure:
  unmapped_requirements: []
  unmapped_decisions: []
  unmapped_tasks: []
  unmapped_scenarios: []
  unmapped_cases: []
  unresolved_non_deferred_interfaces: []
  unresolved_intermediate_states: []
  unresolved_execution_choices: []
  duplicate_initial_file_owners: []
  multi_file_subwindows: []
  substitutes_without_fidelity_disposition: []
  critical_invariants_without_control: []
decisive_assertions:
  - W8 has exactly one personally executed assessment and no delegable leaf.
  - P1-P6 own only exact external facts permitted as deferred applied preflight; each nonpassing result stops with zero guessed substitute.
  - ACT01-ACT07 each require their own requester approval and current A5 predicate.
  - ACT05 cannot execute until separate ACT05 and ACT06 approvals are both current because activation is the physical paid-call release.
  - The successful action ledger is exactly ACT01 through ACT06; ACT07 is failure-only.
  - The same ACT04 research is the sole ACT06 canary and the handoff Run is never confirmed.
  - Ten live cases and six controls have exact registrations activation witnesses oracles counts and recomputed digests.
sandbox_privilege: none
environment_invalidations: []
external_mutations: []
paid_cost_usd: "0.00"
status: PASS
```

## `EV-KI-W8-S003` — decomposition lint, adversarial audit and readiness

```yaml
evidence_id: EV-KI-W8-S003
timestamp: 2026-08-24T15:41:04+05:30
phase: decomposition_authoring
parent_window_id: KI-W8
subwindow_id: KI-W8-DECOMPOSITION
assignment_id: ASG-KI-W8-WA-01
actor: KI-W8-WINDOW-AGENT
decomposition_path: KEYWORD_INTELLIGENCE_KI_W8_SUBWINDOW_CHECKLIST.md
decomposition_revision: 19cfd226b4821e133951332b125f6ecc161a8f96f36e3a6a82e472eb794b5df1
commands:
  - count exact SW-A/D/E/V/R checkboxes and require 47/47 checked
  - extract and compare required case/control memberships and sorted-member-plus-LF SHA-256 digests
  - search assignable content for unresolved placeholders and broad alternative verbs
  - compare planned implementation file set to parent-authorized zero-source policy
  - validate every action appears in the exact approval/state sequence and no action is implied
  - validate all three subordinate artifact paths and cross references
  - git diff --check
results:
  mandatory_authoring_items_checked: 47
  mandatory_authoring_items_unchecked: 0
  initial_file_subwindow_count: 0
  assessment_count: 1
  required_case_count: 10
  required_case_digest: b716a609b2269f69d4e042503ad47dabb1eb397e17726af850f38ab09940431a
  required_control_count: 6
  required_control_digest: 1a2fd2fb71c94f297b27c5c6ad580c67d94ae807525b420996bd4382d46b7c6e
  unmapped_parent_requirements: 0
  unmapped_parent_decisions: 0
  unmapped_parent_tasks: 0
  unmapped_parent_scenarios: 0
  unmapped_coverage_cases: 0
  duplicate_initial_file_owners: 0
  multi_file_subwindows: 0
  unresolved_interfaces: 0
  unresolved_intermediate_states: 0
  unresolved_execution_choices: 0
  unresolved_evidence_references: 0
adversarial_results:
  leaf_or_source_write: rejected_by_zero_leaf_empty_set_oracle
  omitted_or_duplicate_case: rejected_by_set_equality_and_digest
  missing_activation: rejected_by_executed_after_activation_rule
  weakened_oracle_or_substitute: invalidates_evidence
  unapproved_or_combined_action: rejected_by_current_A5_predicate
  ACT05_without_ACT06: rejected_before_activation
  second_canary_or_Run_confirmation: rejected_by_NC06_and_CONF01
  sandbox_only_denial: one_identical_local_or_read_only_recovery
  real_failure_or_external_ambiguity: not_E8_1_and_stops
  window_agent_self_repair: prohibited_and_parent_blocked
external_mutations: []
paid_cost_usd: "0.00"
status: PASS
```

```yaml
certificate: SUBWINDOW-DECOMPOSITION-READY
parent_window_id: KI-W8
parent_assignment_id: ASG-KI-W8-WA-01
window_agent_identity: KI-W8-WINDOW-AGENT
revisions:
  parent_standard: cda352017e75c0d11f6797d9fbe108b4365508cd38b0e92365cfb523ede32848
  subwindow_standard: 842c29550c06c22d63e0a058a27cb8a9ff6b538b3168d2c83a384890b44247f0
  contract: 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c
  decision: 6c0809225ba5336dc923786674b990f83c8db2496b88016f7655a770afb7e307
  parent_checklist: 4f4b16bbe6ab20312e312db75506f9acfee7aaca67fbb66d1d951676f1f646e4
  decomposition: 19cfd226b4821e133951332b125f6ecc161a8f96f36e3a6a82e472eb794b5df1
initial_subwindow_ids: []
initial_subwindow_count: 0
planned_file_set: []
planned_file_set_digest: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
unmapped_parent_requirements: []
unmapped_parent_decisions: []
unmapped_parent_tasks: []
unmapped_parent_scenarios: []
unmapped_coverage_cases: []
duplicate_initial_file_owners: []
multi_file_subwindows: []
unresolved_interfaces: []
unresolved_intermediate_states: []
unresolved_execution_choices: []
unresolved_evidence_references: []
mandatory_authoring_items_checked: 47
mandatory_authoring_items_unchecked: 0
first_subwindow: KI-W8-I001
integration_assessment_id: KI-W8-I001
parent_review_required: true
status: AWAITING_PARENT_DECOMPOSITION_REVIEW
```

No implementation, preflight, build, database, browser, network, provider,
AWS, host, production, paid, destructive, commit, push or final-review action
occurred. No leaf was dispatched. `KI-W8-I001` remains unexecuted.

## `EV-KI-W8-S004` — parent finding reconciliation and superseding readiness

```yaml
evidence_id: EV-KI-W8-S004
timestamp: 2026-08-24T17:28:00+05:30
phase: decomposition_parent_finding_reconciliation
parent_window_id: KI-W8
subwindow_id: KI-W8-DECOMPOSITION
assignment_id: ASG-KI-W8-WA-01
actor: KI-W8-WINDOW-AGENT
supersedes_readiness_claims: [EV-KI-W8-S003, SUBWINDOW-DECOMPOSITION-READY at decomposition 19cfd226b4821e133951332b125f6ecc161a8f96f36e3a6a82e472eb794b5df1]
parent_finding: KI-W8-I001 was decision-safe but delegated positive-gate execution mechanisms, contradicting Section 9.2 item 6 and unresolved_execution_choices zero
revised_decomposition_revision: 7019451217532974865c440a14c87fa7698d125877897bd5aac98d686b450fe2
corrections:
  act04:
    mechanism: exact production same-origin API commands using accepted frontend strict parsers
    route: POST /api/keyword-research
    save_is_mandatory: true
    create_ambiguity: zero_retry_and_exact_read_only_DB_reconciliation
    handoff_ambiguity: one_same_key_reconciliation_only
  neon:
    runner: KIW8-DB-V1
    transaction_guard: SET TRANSACTION READ ONLY and public schema
    literal_query_modes: [baseline, resolveResearch, progress, artifactRows, handoff]
    safe_output_schema: exact
  aws:
    mechanics: exact STS CloudFormation quota SecretsManager SQS Lambda CloudWatch Logs S3 IAM inspector commands and projections
    identities: derived_only_from_exact_stack_outputs
    polling: {disabled_seconds: 5, disabled_ceiling_seconds: 120, live_seconds: 15, no_progress_seconds: 900, absolute_seconds: 14400}
  host:
    discovery: exact A5 KIW8_HOST_DISCOVERY_REQUEST_V1 or fail closed
    mutation: exact separately approved A5 KIW8_HOST_PROTOCOL_V1 or fail closed
    rollback: exact separately approved A5 KIW8_HOST_ROLLBACK_PROTOCOL_V1 or fail closed
  provider_capability:
    state_200_outcome: PARENT_BLOCKED_PROVIDER_CAPABILITY_PROTOCOL
    later_unblock: complete literal A5 KIW8_PROVIDER_CAPABILITY_PROTOCOL_V1 plus S1 re-pin only
    executor_endpoint_choice: prohibited
  handoff:
    exact_order: [dashboard_HTML_GET, owner_A_research_GET, mandatory_selection_PUT, deterministic_same_key_run_POST, owner_B_research_GET, owner_B_run_GET, DB_handoff_zero_downstream, queue_metric_log_alarm_S3_closure]
  gate_manifest:
    gates: [G1, G2, G3, G4, G5, G6, G7]
    columns: [command_or_runner, cwd, environment_allowlist, expected_exit_output, activation_witness, maximum_runs, external_side_effect, cost_ceiling, ambiguity_reconciliation, evidence_artifact]
  execution_choice_lint:
    positive_result: KIW8_EXECUTION_CHOICES_ZERO
    falsifications: 4
closure:
  initial_file_subwindows: []
  implementation_source_leaves: 0
  leaf_delegation: prohibited
  action_ids_preserved: [W8-ACT-01, W8-ACT-02, W8-ACT-03, W8-ACT-04, W8-ACT-05, W8-ACT-06, W8-ACT-07]
  required_cases_preserved: 10
  required_case_digest: b716a609b2269f69d4e042503ad47dabb1eb397e17726af850f38ab09940431a
  required_controls_preserved: 6
  required_control_digest: 1a2fd2fb71c94f297b27c5c6ad580c67d94ae807525b420996bd4382d46b7c6e
  unresolved_interfaces: []
  unresolved_intermediate_states: []
  unresolved_execution_choices: []
  unresolved_evidence_references: []
  explicit_parent_prerequisites_not_executor_choices:
    - KIW8_PROVIDER_CAPABILITY_PROTOCOL_V1
    - KIW8_HOST_DISCOVERY_REQUEST_V1
    - KIW8_HOST_PROTOCOL_V1
    - exact origin owner-cookie seed hashes
commands:
  - documentation-only rg/source inspection
  - exact assignable-content execution-choice lint
  - case/control membership and digest recomputation
  - 47-item authoring-checklist count
  - git diff --check
external_mutations: []
paid_cost_usd: "0.00"
status: PASS
```

```yaml
certificate: SUBWINDOW-DECOMPOSITION-READY-SUPERSEDING
parent_window_id: KI-W8
parent_assignment_id: ASG-KI-W8-WA-01
window_agent_identity: KI-W8-WINDOW-AGENT
decomposition_revision: 7019451217532974865c440a14c87fa7698d125877897bd5aac98d686b450fe2
state_version: 2
decomposition_status: AWAITING_PARENT_DECOMPOSITION_REVIEW
initial_subwindow_ids: []
initial_subwindow_count: 0
integration_assessment_id: KI-W8-I001
planned_file_set: []
planned_file_set_digest: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
unmapped_parent_requirements: []
unmapped_parent_decisions: []
unmapped_parent_tasks: []
unmapped_parent_scenarios: []
unmapped_coverage_cases: []
duplicate_initial_file_owners: []
multi_file_subwindows: []
unresolved_interfaces: []
unresolved_intermediate_states: []
unresolved_execution_choices: []
unresolved_evidence_references: []
mandatory_authoring_items_checked: 47
mandatory_authoring_items_unchecked: 0
execution_prerequisites_are_fail_closed_parent_records: true
parent_review_required: true
status: AWAITING_PARENT_DECOMPOSITION_REVIEW
```

No W8 preflight, network, AWS, host, provider, paid, database, browser, build,
source/test edit, leaf dispatch, commit, push, action or assessment execution
occurred during this reconciliation.
