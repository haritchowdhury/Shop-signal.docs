# KI-W7 Sub-Window Evidence (`S3`)

Append-only evidence for parent window `KI-W7`. This file cannot authorize or
amend work. Decomposition authority is `S1`; live subordinate state is `S2`.

## `EV-KI-W7-S001` - authority, revision, environment, and baseline certificate

```yaml
evidence_id: EV-KI-W7-S001
timestamp: 2026-08-24T09:53:20+05:30
parent_window_id: KI-W7
subwindow_id: KI-W7-DECOMPOSITION
assignment_id: ASG-KI-W7-WA-01
actor: KI-W7-WINDOW-AGENT
role: window_agent_decomposition_author
frozen_revisions:
  parent_standard: cda352017e75c0d11f6797d9fbe108b4365508cd38b0e92365cfb523ede32848
  subwindow_standard: 842c29550c06c22d63e0a058a27cb8a9ff6b538b3168d2c83a384890b44247f0
  contract: 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c
  discovery: 493192fc317c00ee43e277e85e00718985190cdd5c21e3d6824f67dd1d0b7c0c
  decision: 6c0809225ba5336dc923786674b990f83c8db2496b88016f7655a770afb7e307
  parent_checklist: 4a47d782223e372d2df7d653add494880eddf456ab3f4d63439fea2ed1c2374e
  parent_state: 3a63c9278ce68ae3a7c05e14a56f3ded4d3e3166bc0af7daea768e3b826dc7f1
  traceability: 90c2f808426c4f1cf20ad885860e01b66763f3fc607e28c3b2dd9a2ef7391a5f
starting_subordinate_files: [S1 ABSENT, S2 ABSENT, S3 ABSENT]
backend_head: a87e139c020712ef95c05d232b9548216b0658b8
frontend_head: 5e441aae7e2f3a132b2c7fc85bf1bc525d3d5cb6
backend_starting_changed_files: []
backend_starting_change_set_digest: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
frontend_starting_changed_files: []
root_protected_changed_files: [ACTIVE_EXECUTION_STATE.md, KEYWORD_INTELLIGENCE_DECISION_LEDGER.md, KEYWORD_INTELLIGENCE_DISCOVERY_DOSSIER.md, KEYWORD_INTELLIGENCE_EXECUTION_EVIDENCE.md, KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md, KEYWORD_INTELLIGENCE_SPECIFICATION_CHANGELOG.md, KEYWORD_INTELLIGENCE_TRACEABILITY_INDEX.md]
root_protected_set_digest: 6a8baa5680b1bc6f308c3778347ff3c9f24d17f9716c91abb361f1a1388d00cc
```

Inspections/commands were read-only: SHA-256 recomputation of both standards and
all pinned parent artifacts; `git status --porcelain=v1 --untracked-files=all`
at root/backend/frontend; `git rev-parse HEAD` in both nested repositories;
`sha256sum` for all existing W7 targets; absence/non-symlink/parent-path checks
for new targets; `node --version`, `npm --version`, `zip -v`, `unzip -v`, SAM
presence, and installed-dependency presence.

Observed result: every pin and all six existing W7 file baselines match A5/A4;
seven new targets are absent; backend/frontend are clean; root dirty state is
the seven parent-owned files above. Node `v24.14.1`, npm `11.11.0`, Info-ZIP and
UnZip `6.00` are present, dependencies are installed, and SAM is absent as the
parent predicts. A5 names the exact window agent, allows only S1-S3 writes, and
records KI-W6 accepted. No sandbox escalation, process, workspace mutation,
external mutation, cost, credential read, database/browser/build/AWS/provider/
network action occurred during these inspections. Limit: this is source and
authority evidence, not implementation or applied-runtime evidence.

## `EV-KI-W7-S002` - source, file-set, and interface closure

```yaml
evidence_id: EV-KI-W7-S002
timestamp: 2026-08-24T09:53:20+05:30
parent_window_id: KI-W7
subwindow_id: KI-W7-DECOMPOSITION
assignment_id: ASG-KI-W7-WA-01
actor: KI-W7-WINDOW-AGENT
role: window_agent_decomposition_author
source_anchor: SRC-KI-060
governing_decision: DEC-KI-059
parent_tasks: [KI-W7-T1, KI-W7-T2, KI-W7-T3, KI-W7-T4, KI-W7-T5, KI-W7-T6]
parent_scenario: SCN-KI-047
planned_file_count: 13
planned_file_set_digest: 04ce71235fe61103c071f859d6050d4f8fee2b56dc0e088b9d97f5111be57a9f
initial_subwindow_count: 13
duplicate_initial_file_owners: []
multi_file_subwindows: []
unmapped_parent_requirements: []
unmapped_parent_decisions: []
unmapped_parent_tasks: []
unmapped_parent_scenarios: []
unresolved_interfaces: []
unresolved_execution_choices: []
```

The window agent directly inspected current `config.js`, runtime config,
keyword handler, scheduled recovery handler, runtime factory, keyword
repository/recovery, established recovery service, current JSON SAM template,
both accepted builders, established measurement/deployment/inspection scripts,
runtime-adapter tests, package commands, and W7 parent/traceability blocks.
Observed source reproduces every `SRC-KI-060` gap. The exact 13 sorted UTF-8
members plus LF recompute the parent digest. Each file has one initial owner;
production, script, template, and test changes are separate. IF-1 through IF-8
freeze all cross-file names, signatures, fields, ordering, failure branches,
limits, side effects, and preserved behavior before consumers. No payload or
external fact was guessed; applied account/quota/secret/provider/host facts stay
deferred to W8. No command changed source or generated output; external
mutations/costs are empty.

## `EV-KI-W7-S003` - DAG, coverage, intermediate-state, and assessment closure

```yaml
evidence_id: EV-KI-W7-S003
timestamp: 2026-08-24T09:53:20+05:30
parent_window_id: KI-W7
subwindow_id: KI-W7-DECOMPOSITION
assignment_id: ASG-KI-W7-WA-01
actor: KI-W7-WINDOW-AGENT
role: window_agent_decomposition_author
serial_order: [KI-W7-S001, KI-W7-S002, KI-W7-S003, KI-W7-S004, KI-W7-S005, KI-W7-S006, KI-W7-S007, KI-W7-S008, KI-W7-S009, KI-W7-S010, KI-W7-S011, KI-W7-S012, KI-W7-S013, KI-W7-I001]
dependency_strata:
  - [KI-W7-S001, KI-W7-S002, KI-W7-S003, KI-W7-S004, KI-W7-S005, KI-W7-S006]
  - [KI-W7-S007, KI-W7-S008]
  - [KI-W7-S009, KI-W7-S010, KI-W7-S011, KI-W7-S012, KI-W7-S013]
parallel_waves_currently_authorized: []
required_case_count: 12
required_case_set_digest: 6bacf5d9291362ee0d01f5d0d8e3e53f8f9e214a6ebbf5711497c80f3d74aa2e
required_control_count: 12
required_control_set_digest: 6950a20f91b666c03cf59c495576e72ad1501fcd58aa5f4378900bd473edafd7
unmapped_cases: []
unmapped_controls: []
duplicate_case_owners: []
unresolved_intermediate_states: []
integration_assessment_id: KI-W7-I001
```

The DAG is acyclic. A4's strata are preserved, while A5's empty permitted-wave
list is enforced by a serial schedule; no parallel authority is inferred. Each
intermediate state has exact passing local checks, explicit I001 deferrals,
safety, resolver, and prohibitions. Case/control registries, owner allocation,
activation/effect oracles, mutations, exact counts, and sorted-LF digests match
A4 and `DEC-KI-059`. I001 is fully authored with zero implementation write,
risk-proportionate build/regression scheduling, substitute limits, invalidation
rules, negative searches, and exact outcome oracles. No checks were executed as
implementation evidence in this decomposition turn; no external mutation or
cost occurred.

## `EV-KI-W7-S004` - reconciliation, structural lint, and adversarial audit

```yaml
evidence_id: EV-KI-W7-S004
timestamp: 2026-08-24T10:38:33+05:30
parent_window_id: KI-W7
subwindow_id: KI-W7-DECOMPOSITION
assignment_id: ASG-KI-W7-WA-01
actor: KI-W7-WINDOW-AGENT
role: window_agent_decomposition_reviewer
reconciled_decomposition_revision: bc37e3d98533da7ff15102edb91143155f5d6d3f5010410a585bc4b00d9ec2c9
reconciled_state_revision: 9ff0668c40e2f1d6d70fd260c54a3dee5d706d11e6a740991511c2857f0cb4ed
initial_file_subwindows: 13
unique_subwindow_ids: 13
unique_writable_files: 13
mandatory_identity_fields_per_block: 15
mandatory_completion_boxes_per_block: 9
mandatory_authoring_items_checked: 47
mandatory_authoring_items_unchecked: 0
unresolved_placeholder_count: 0
unresolved_evidence_reference_count_after_this_entry: 0
multi_file_subwindow_count: 0
duplicate_file_owner_count: 0
unmapped_requirement_count: 0
unmapped_decision_count: 0
unmapped_task_count: 0
unmapped_scenario_count: 0
unmapped_case_count: 0
unmapped_control_count: 0
unresolved_interface_count: 0
unresolved_intermediate_state_count: 0
unresolved_execution_choice_count: 0
```

The requester stopped a separately dispatched overlapping decomposition agent
and returned sole responsibility to the assigned `KI-W7-WINDOW-AGENT`. The
overlap produced only untracked revisions of S1/S2 under the same A5 identity;
it produced no implementation/test/build output and no backend/frontend
change. The sole window agent preserved the valid expansion to thirteen
explicit nine-box leaf checklists, independently reread the complete live S1,
and reconciled S2 to that byte-exact S1. Superseded transient S1/S2 hashes are
not authority and are not execution evidence.

Read-only structural lint parsed all thirteen blocks and required each of the
fifteen Section 7 identity/authority fields plus the nine P1-P2/T1/V1-V3/H1-H3
completion boxes. It proved unique IDs/files, exact one-file ownership, no
unchecked `SW-*` item, and no `TODO`, `TBD`, blank evidence marker, or forbidden
assignable design verb. Removing a file/member changes the path digest;
duplicating/removing a case or control breaks set equality; a second writable
file, missing field/box, unresolved evidence reference, changed command,
observable test failure, or external action makes readiness fail. The inherited
one-identical-recovery rule applies only to proven sandbox/channel invalidation.

## `EV-KI-W7-S005` - `SUBWINDOW-DECOMPOSITION-READY` certificate

```yaml
certificate: SUBWINDOW-DECOMPOSITION-READY
evidence_id: EV-KI-W7-S005
timestamp: 2026-08-24T10:38:33+05:30
parent_window_id: KI-W7
parent_assignment_id: ASG-KI-W7-WA-01
window_agent: KI-W7-WINDOW-AGENT
decomposition_path: KEYWORD_INTELLIGENCE_KI_W7_SUBWINDOW_CHECKLIST.md
decomposition_revision: bc37e3d98533da7ff15102edb91143155f5d6d3f5010410a585bc4b00d9ec2c9
state_path: KEYWORD_INTELLIGENCE_KI_W7_SUBWINDOW_STATE.md
state_revision: 9ff0668c40e2f1d6d70fd260c54a3dee5d706d11e6a740991511c2857f0cb4ed
evidence_through: EV-KI-W7-S005
planned_file_count: 13
planned_file_set_digest: 04ce71235fe61103c071f859d6050d4f8fee2b56dc0e088b9d97f5111be57a9f
initial_subwindow_ids: [KI-W7-S001, KI-W7-S002, KI-W7-S003, KI-W7-S004, KI-W7-S005, KI-W7-S006, KI-W7-S007, KI-W7-S008, KI-W7-S009, KI-W7-S010, KI-W7-S011, KI-W7-S012, KI-W7-S013]
dependency_order: [KI-W7-S001, KI-W7-S002, KI-W7-S003, KI-W7-S004, KI-W7-S005, KI-W7-S006, KI-W7-S007, KI-W7-S008, KI-W7-S009, KI-W7-S010, KI-W7-S011, KI-W7-S012, KI-W7-S013, KI-W7-I001]
dependency_strata:
  - [KI-W7-S001, KI-W7-S002, KI-W7-S003, KI-W7-S004, KI-W7-S005, KI-W7-S006]
  - [KI-W7-S007, KI-W7-S008]
  - [KI-W7-S009, KI-W7-S010, KI-W7-S011, KI-W7-S012, KI-W7-S013]
parallel_waves_currently_authorized: []
integration_assessment_id: KI-W7-I001
required_case_count: 12
required_case_set_digest: 6bacf5d9291362ee0d01f5d0d8e3e53f8f9e214a6ebbf5711497c80f3d74aa2e
required_control_count: 12
required_control_set_digest: 6950a20f91b666c03cf59c495576e72ad1501fcd58aa5f4378900bd473edafd7
mandatory_authoring_checklist: 47/47
unmapped_counts: {requirements: 0, decisions: 0, tasks: 0, scenarios: 0, cases: 0, controls: 0}
unresolved_counts: {interfaces: 0, intermediate_states: 0, execution_choices: 0, evidence_references: 0}
multi_file_subwindows: 0
duplicate_file_owners: 0
backend_head: a87e139c020712ef95c05d232b9548216b0658b8
backend_changed_files: []
frontend_head: 5e441aae7e2f3a132b2c7fc85bf1bc525d3d5cb6
frontend_changed_files: []
implementation_started: false
leaf_dispatched: false
external_mutations: []
paid_cost_usd: 0.00
status: AWAITING_PARENT_DECOMPOSITION_REVIEW
blocker: null
```

This certificate proves decomposition readiness only. It grants no leaf
assignment, implementation, build, database/browser, network/provider/AWS,
commit/push, or KI-W8 authority. Parent decomposition approval and a live A5
transition are required before S001 may be assigned.

## `EV-KI-W7-S006` - parent-review correction and supersession audit

```yaml
evidence_id: EV-KI-W7-S006
timestamp: 2026-08-24T10:52:00+05:30
parent_window_id: KI-W7
parent_assignment_id: ASG-KI-W7-WA-01
actor: KI-W7-WINDOW-AGENT
supersedes_readiness_certificate: EV-KI-W7-S005
corrected_findings: [F1, F2, F3, F4, F5]
decomposition_revision: 9a802ceb3989cc74dac8ff7b64ce1f83446400227a3ea602b123e0b53eb07ea2
state_revision: 6a562c464cff7fff0eab3fd0e0e2cf177b606d031ea9e7f195e5c6d35bae3b95
initial_subwindow_count: 13
planned_file_set_changed: false
case_or_control_set_changed: false
leaf_assigned_or_dispatched: false
implementation_or_test_file_changed: false
build_or_external_action_run: false
```

F1 is closed by the strict `CV1 -> CV2 -> CV3 build/bridge -> CV4 focused
merge -> CV5 -> CV6 -> CV7` order. F2 is closed by the exact temporary path,
strict bridge schema, atomic producer, sole environment seam, strict S012
consumer/certificate, privacy bounds, and finally cleanup. F3 is closed by the
single `W7_OWNER_REGISTRY` source-marker grammar and S013 source parser, which
never imports another test module. F4 is closed by the exact superseding
Section 12.1 certificate below. F5 is closed by the schema-admitted fail-closed
`STOP/WINDOW-AGENT/INTEGRATION_ASSESSMENT/BLOCKED` preapproval sentinel. No
parent-level decision, file owner, case/control member, interface behavior, or
implementation scope changed.

## `EV-KI-W7-S007` - superseding decomposition readiness certificate

```yaml
certificate: SUBWINDOW-DECOMPOSITION-READY
parent_window_id: KI-W7
parent_assignment_id: ASG-KI-W7-WA-01
window_agent_identity: KI-W7-WINDOW-AGENT
revisions:
  parent_standard: cda352017e75c0d11f6797d9fbe108b4365508cd38b0e92365cfb523ede32848
  subwindow_standard: 842c29550c06c22d63e0a058a27cb8a9ff6b538b3168d2c83a384890b44247f0
  contract: 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c
  decision: 6c0809225ba5336dc923786674b990f83c8db2496b88016f7655a770afb7e307
  parent_checklist: 4a47d782223e372d2df7d653add494880eddf456ab3f4d63439fea2ed1c2374e
  decomposition: 9a802ceb3989cc74dac8ff7b64ce1f83446400227a3ea602b123e0b53eb07ea2
initial_subwindow_ids: [KI-W7-S001, KI-W7-S002, KI-W7-S003, KI-W7-S004, KI-W7-S005, KI-W7-S006, KI-W7-S007, KI-W7-S008, KI-W7-S009, KI-W7-S010, KI-W7-S011, KI-W7-S012, KI-W7-S013]
initial_subwindow_count: 13
planned_file_set: [email_scraper/src/config.js, email_scraper/src/aws-pipeline/runtime-config.js, email_scraper/src/aws-pipeline/keyword-intelligence/handler.js, email_scraper/src/aws-pipeline/handlers/recovery.js, email_scraper/infrastructure/aws/template.yaml, email_scraper/scripts/measure-keyword-worker-package.js, email_scraper/scripts/keyword-intelligence/create-change-set.js, email_scraper/scripts/keyword-intelligence/inspect-stack.js, email_scraper/test/aws-pipeline-runtime-adapters.test.js, email_scraper/test/keyword-intelligence-deployment-runtime.test.js, email_scraper/test/keyword-intelligence-infrastructure.test.js, email_scraper/test/keyword-intelligence-build.test.js, email_scraper/test/keyword-intelligence-deployment-guard.test.js]
planned_file_set_digest: 04ce71235fe61103c071f859d6050d4f8fee2b56dc0e088b9d97f5111be57a9f
unmapped_parent_requirements: []
unmapped_parent_decisions: []
unmapped_parent_tasks: []
unmapped_coverage_cases: []
duplicate_initial_file_owners: []
multi_file_subwindows: []
unresolved_interfaces: []
unresolved_intermediate_states: []
unresolved_execution_choices: []
unresolved_evidence_references: []
mandatory_authoring_items_checked: 47
mandatory_authoring_items_unchecked: 0
first_subwindow: KI-W7-S001
integration_assessment_id: KI-W7-I001
parent_review_required: true
```

`EV-KI-W7-S007` supersedes only the readiness claim in `EV-KI-W7-S005`;
S001-S006 history remains append-only. Decomposition status remains
`AWAITING_PARENT_DECOMPOSITION_REVIEW`, the preapproval sentinel carries no
execution authority, and S001 remains unassigned.

## `EV-KI-W7-S008` - final bridge-cleanup and pin reconciliation

```yaml
evidence_id: EV-KI-W7-S008
timestamp: 2026-08-24T11:00:00+05:30
parent_window_id: KI-W7
parent_assignment_id: ASG-KI-W7-WA-01
actor: KI-W7-WINDOW-AGENT
supersedes_readiness_certificate: EV-KI-W7-S007
decomposition_revision: a11d3548f07a10f77464680c09f68712d9afe812ca9d0691ad480c622d35f982
state_revision: eb33d3bc839c7ea4ad1cb0cc0b410345002b654550609b8d6ac9602f49dcbb6b
delta: bridge cleanup is one outer try/finally spanning CV3 and CV4, including pre-emission failure
planned_file_set_changed: false
case_or_control_set_changed: false
leaf_assigned_or_dispatched: false
implementation_or_test_file_changed: false
```

The final bridge clarification closes cleanup for CV3 failures occurring before
artifact emission. Structural lint again found 13 blocks, 15 mandatory fields
and nine boxes per block, 13 unique writable files, 47/47 authoring items,
zero unresolved placeholders, and zero stale vague bridge/registry phrases.

## `EV-KI-W7-S009` - final superseding decomposition readiness certificate

```yaml
certificate: SUBWINDOW-DECOMPOSITION-READY
parent_window_id: KI-W7
parent_assignment_id: ASG-KI-W7-WA-01
window_agent_identity: KI-W7-WINDOW-AGENT
revisions:
  parent_standard: cda352017e75c0d11f6797d9fbe108b4365508cd38b0e92365cfb523ede32848
  subwindow_standard: 842c29550c06c22d63e0a058a27cb8a9ff6b538b3168d2c83a384890b44247f0
  contract: 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c
  decision: 6c0809225ba5336dc923786674b990f83c8db2496b88016f7655a770afb7e307
  parent_checklist: 4a47d782223e372d2df7d653add494880eddf456ab3f4d63439fea2ed1c2374e
  decomposition: a11d3548f07a10f77464680c09f68712d9afe812ca9d0691ad480c622d35f982
initial_subwindow_ids: [KI-W7-S001, KI-W7-S002, KI-W7-S003, KI-W7-S004, KI-W7-S005, KI-W7-S006, KI-W7-S007, KI-W7-S008, KI-W7-S009, KI-W7-S010, KI-W7-S011, KI-W7-S012, KI-W7-S013]
initial_subwindow_count: 13
planned_file_set: [email_scraper/src/config.js, email_scraper/src/aws-pipeline/runtime-config.js, email_scraper/src/aws-pipeline/keyword-intelligence/handler.js, email_scraper/src/aws-pipeline/handlers/recovery.js, email_scraper/infrastructure/aws/template.yaml, email_scraper/scripts/measure-keyword-worker-package.js, email_scraper/scripts/keyword-intelligence/create-change-set.js, email_scraper/scripts/keyword-intelligence/inspect-stack.js, email_scraper/test/aws-pipeline-runtime-adapters.test.js, email_scraper/test/keyword-intelligence-deployment-runtime.test.js, email_scraper/test/keyword-intelligence-infrastructure.test.js, email_scraper/test/keyword-intelligence-build.test.js, email_scraper/test/keyword-intelligence-deployment-guard.test.js]
planned_file_set_digest: 04ce71235fe61103c071f859d6050d4f8fee2b56dc0e088b9d97f5111be57a9f
unmapped_parent_requirements: []
unmapped_parent_decisions: []
unmapped_parent_tasks: []
unmapped_coverage_cases: []
duplicate_initial_file_owners: []
multi_file_subwindows: []
unresolved_interfaces: []
unresolved_intermediate_states: []
unresolved_execution_choices: []
unresolved_evidence_references: []
mandatory_authoring_items_checked: 47
mandatory_authoring_items_unchecked: 0
first_subwindow: KI-W7-S001
integration_assessment_id: KI-W7-I001
parent_review_required: true
```

`EV-KI-W7-S009` is the operative readiness certificate. Earlier certificates
remain append-only history and grant no authority. S2 remains fail-closed at
`AWAITING_PARENT_DECOMPOSITION_REVIEW`; no implementation leaf is executable.

## `EV-KI-W7-S010` - runtime-accounting and boundary correction

```yaml
evidence_id: EV-KI-W7-S010
timestamp: 2026-08-24T11:18:00+05:30
parent_window_id: KI-W7
parent_assignment_id: ASG-KI-W7-WA-01
actor: KI-W7-WINDOW-AGENT
supersedes_readiness_certificate: EV-KI-W7-S009
corrected_findings: [F6, F7]
decomposition_revision: ec2d9bbcab27e3e88fbfa3f8b78be57cc701886c8f735ec619a7cbf6718a54de
state_revision: 052e83dd2424f40455ddd59aaab4e61cb62bcafeaa5c67da2184ef1444e426fe
planned_file_set_changed: false
case_or_control_set_changed: false
leaf_assigned_or_dispatched: false
implementation_or_test_file_changed: false
build_or_external_action_run: false
```

F6 is closed by exact top-level W7 names, per-owner diagnostic unions, one TAP
reporter destination, a deterministic no-import parser/filter, the strict
aggregate certificate, sole CV4 emission/acceptance, coexistence with the build
diagnostic, and four in-memory missing/duplicate/skip/unactivated parser
controls. Non-W7 focused-file tests are ignored only through the explicit
prefix rule and are counted. No global or import order is used. F7 is closed by
the schema-admitted `STOP/WINDOW-AGENT/INTEGRATION_ASSESSMENT/COMPLETE`
preapproval sentinel with `blocker:null`; `decomposition_status` still requires
parent review and no leaf authority exists.

## `EV-KI-W7-S011` - DECOMP-3 superseding decomposition readiness certificate

```yaml
certificate: SUBWINDOW-DECOMPOSITION-READY
parent_window_id: KI-W7
parent_assignment_id: ASG-KI-W7-WA-01
window_agent_identity: KI-W7-WINDOW-AGENT
revisions:
  parent_standard: cda352017e75c0d11f6797d9fbe108b4365508cd38b0e92365cfb523ede32848
  subwindow_standard: 842c29550c06c22d63e0a058a27cb8a9ff6b538b3168d2c83a384890b44247f0
  contract: 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c
  decision: 6c0809225ba5336dc923786674b990f83c8db2496b88016f7655a770afb7e307
  parent_checklist: 4a47d782223e372d2df7d653add494880eddf456ab3f4d63439fea2ed1c2374e
  decomposition: ec2d9bbcab27e3e88fbfa3f8b78be57cc701886c8f735ec619a7cbf6718a54de
initial_subwindow_ids: [KI-W7-S001, KI-W7-S002, KI-W7-S003, KI-W7-S004, KI-W7-S005, KI-W7-S006, KI-W7-S007, KI-W7-S008, KI-W7-S009, KI-W7-S010, KI-W7-S011, KI-W7-S012, KI-W7-S013]
initial_subwindow_count: 13
planned_file_set: [email_scraper/src/config.js, email_scraper/src/aws-pipeline/runtime-config.js, email_scraper/src/aws-pipeline/keyword-intelligence/handler.js, email_scraper/src/aws-pipeline/handlers/recovery.js, email_scraper/infrastructure/aws/template.yaml, email_scraper/scripts/measure-keyword-worker-package.js, email_scraper/scripts/keyword-intelligence/create-change-set.js, email_scraper/scripts/keyword-intelligence/inspect-stack.js, email_scraper/test/aws-pipeline-runtime-adapters.test.js, email_scraper/test/keyword-intelligence-deployment-runtime.test.js, email_scraper/test/keyword-intelligence-infrastructure.test.js, email_scraper/test/keyword-intelligence-build.test.js, email_scraper/test/keyword-intelligence-deployment-guard.test.js]
planned_file_set_digest: 04ce71235fe61103c071f859d6050d4f8fee2b56dc0e088b9d97f5111be57a9f
unmapped_parent_requirements: []
unmapped_parent_decisions: []
unmapped_parent_tasks: []
unmapped_coverage_cases: []
duplicate_initial_file_owners: []
multi_file_subwindows: []
unresolved_interfaces: []
unresolved_intermediate_states: []
unresolved_execution_choices: []
unresolved_evidence_references: []
mandatory_authoring_items_checked: 47
mandatory_authoring_items_unchecked: 0
first_subwindow: KI-W7-S001
integration_assessment_id: KI-W7-I001
parent_review_required: true
```

`EV-KI-W7-S011` is the operative readiness certificate. Earlier readiness
certificates remain append-only history and grant no authority. S2 is complete
only for decomposition authoring, remains
`AWAITING_PARENT_DECOMPOSITION_REVIEW`, and authorizes no implementation leaf.

## `EV-KI-W7-S012` - parser ownership and CLI execution-completeness correction

```yaml
evidence_id: EV-KI-W7-S012
timestamp: 2026-08-24T11:34:00+05:30
parent_window_id: KI-W7
parent_assignment_id: ASG-KI-W7-WA-01
actor: KI-W7-WINDOW-AGENT
supersedes_readiness_certificate: EV-KI-W7-S011
corrected_findings: [F8]
decomposition_revision: 44f8bc4a2a51858937ba1ebeff6df8d45fdd82ceb86fd226486be0d12b84d8f5
state_revision: 9218ae3faf5a8f6089f6a3b97ea1860cbf3806edeb5e9a88acf2ec455e9ba227
parser_owner: KI-W7-S013
parser_file: email_scraper/test/keyword-intelligence-deployment-guard.test.js
planned_file_set_changed: false
case_or_control_set_changed: false
leaf_assigned_or_dispatched: false
implementation_or_test_file_changed: false
build_or_external_action_run: false
```

F8 is closed without adding a file: S013 owns and exports
`parseFocusedTap(text,{buildEvidenceBytes})` and `runFocusedParserCli(argv)`,
owns the direct-main discriminator and private ordinary-test registrar, and
freezes exact arguments, paths, bounds, bridge input, atomic output, error/exit,
privacy, cleanup, and zero-test parser-mode oracles. S013 LOCAL_NOW runs the
accepted synthetic TAP plus four mutations through the real CLI and a final
unchanged replay. CV4 first produces TAP with the five-file command and then
invokes the accepted S013 CLI exactly once. I001 authors no parser code.

## `EV-KI-W7-S013` - DECOMP-4 superseding decomposition readiness certificate

```yaml
certificate: SUBWINDOW-DECOMPOSITION-READY
parent_window_id: KI-W7
parent_assignment_id: ASG-KI-W7-WA-01
window_agent_identity: KI-W7-WINDOW-AGENT
revisions:
  parent_standard: cda352017e75c0d11f6797d9fbe108b4365508cd38b0e92365cfb523ede32848
  subwindow_standard: 842c29550c06c22d63e0a058a27cb8a9ff6b538b3168d2c83a384890b44247f0
  contract: 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c
  decision: 6c0809225ba5336dc923786674b990f83c8db2496b88016f7655a770afb7e307
  parent_checklist: 4a47d782223e372d2df7d653add494880eddf456ab3f4d63439fea2ed1c2374e
  decomposition: 44f8bc4a2a51858937ba1ebeff6df8d45fdd82ceb86fd226486be0d12b84d8f5
initial_subwindow_ids: [KI-W7-S001, KI-W7-S002, KI-W7-S003, KI-W7-S004, KI-W7-S005, KI-W7-S006, KI-W7-S007, KI-W7-S008, KI-W7-S009, KI-W7-S010, KI-W7-S011, KI-W7-S012, KI-W7-S013]
initial_subwindow_count: 13
planned_file_set: [email_scraper/src/config.js, email_scraper/src/aws-pipeline/runtime-config.js, email_scraper/src/aws-pipeline/keyword-intelligence/handler.js, email_scraper/src/aws-pipeline/handlers/recovery.js, email_scraper/infrastructure/aws/template.yaml, email_scraper/scripts/measure-keyword-worker-package.js, email_scraper/scripts/keyword-intelligence/create-change-set.js, email_scraper/scripts/keyword-intelligence/inspect-stack.js, email_scraper/test/aws-pipeline-runtime-adapters.test.js, email_scraper/test/keyword-intelligence-deployment-runtime.test.js, email_scraper/test/keyword-intelligence-infrastructure.test.js, email_scraper/test/keyword-intelligence-build.test.js, email_scraper/test/keyword-intelligence-deployment-guard.test.js]
planned_file_set_digest: 04ce71235fe61103c071f859d6050d4f8fee2b56dc0e088b9d97f5111be57a9f
unmapped_parent_requirements: []
unmapped_parent_decisions: []
unmapped_parent_tasks: []
unmapped_coverage_cases: []
duplicate_initial_file_owners: []
multi_file_subwindows: []
unresolved_interfaces: []
unresolved_intermediate_states: []
unresolved_execution_choices: []
unresolved_evidence_references: []
mandatory_authoring_items_checked: 47
mandatory_authoring_items_unchecked: 0
first_subwindow: KI-W7-S001
integration_assessment_id: KI-W7-I001
parent_review_required: true
```

`EV-KI-W7-S013` is the operative readiness certificate. All previous readiness
certificates remain append-only history and grant no authority. S2 remains at
the normal completed-decomposition parent-review boundary; S001 is unassigned.

## `EV-KI-W7-S014` - parent approval reconciliation and S001 assignment

```yaml
evidence_id: EV-KI-W7-S014
timestamp: 2026-08-24T13:08:00+05:30
parent_window_id: KI-W7
parent_assignment_id: ASG-KI-W7-WA-02
window_agent: KI-W7-WINDOW-AGENT
parent_state_version: 196
parent_state_revision: 078f9aa9a42447c2eea5d409dab4cfb68a97fd5d7e8583b2086bf4f1bdfebd8d
accepted_decomposition_revision: 44f8bc4a2a51858937ba1ebeff6df8d45fdd82ceb86fd226486be0d12b84d8f5
parent_acceptance_evidence: EV-KI-A-121
parent_change_log: CHG-KI-092
subwindow_state_version: 6
subwindow_state_revision: 16cd68db81a95a165190422e7095a62ecd8ba43a960662096b09f19e101f15b3
assigned_subwindow: KI-W7-S001
assignment_id: ASG-KI-W7-S001-01
assigned_agent: KI-W7-S001-AGENT
authorized_write_file: email_scraper/src/config.js
parallel_leaves: []
```

All parent and decomposition pins match. Backend and frontend remain clean at
the accepted heads. The serial schedule is active; only S001 is assigned.

## `EV-KI-W7-S015` - S001 independent acceptance and S002 assignment

```yaml
evidence_id: EV-KI-W7-S015
timestamp: 2026-08-24T13:18:00+05:30
parent_window_id: KI-W7
parent_assignment_id: ASG-KI-W7-WA-02
reviewed_subwindow: KI-W7-S001
reviewed_assignment: ASG-KI-W7-S001-01
disposition: ACCEPTED_FOR_INTEGRATION
writable_file: email_scraper/src/config.js
starting_digest: 222daf3780cefa0f061cf486d978d84126fdee6d0a1adf358087b8db2bcc03f9
ending_digest: 4f32f74b3cc38d91092427cf8fc0028ac535b4b3419900907a86eaf80a9edc9b
diff_numstat: {added: 6, deleted: 0}
actual_backend_changed_files: [src/config.js]
local_checks: [node_check_pass, absent_active_invalid_config_oracles_pass, exact_source_oracle_pass, diff_check_pass]
deferred_to: [KI-W7-S009, KI-W7-I001]
prohibited_actions_observed: []
next_subwindow: KI-W7-S002
next_assignment: ASG-KI-W7-S002-01
state_version: 7
state_revision: 58f90d16c4899f58e86215c09e4c212ab12cf580bc9842f6da04dc083e9fcce5
```

The window agent independently inspected the complete six-line diff, ending
hash, one-file porcelain, syntax result, IF-1 order/defaults, and preservation
of adjacent config behavior. S001 is accepted; only S002 is now assigned.

## `EV-KI-W7-S016` - S002 independent acceptance and S003 assignment

```yaml
evidence_id: EV-KI-W7-S016
timestamp: 2026-08-24T13:27:00+05:30
reviewed_subwindow: KI-W7-S002
reviewed_assignment: ASG-KI-W7-S002-01
disposition: ACCEPTED_FOR_INTEGRATION
writable_file: email_scraper/src/aws-pipeline/runtime-config.js
starting_digest: 1801455db1e4c88c63e9d8215e4b1f3770990359518fe07877c3b0218f11576b
ending_digest: 4acd12e06d435e2d1628f3a5db55ebeb929c25ac1bcbf8f5625524d026925fdf
diff_numstat: {added: 22, deleted: 2}
actual_backend_changed_files: [src/aws-pipeline/runtime-config.js, src/config.js]
local_checks: [node_check_pass, IF2_partition_and_frozen_oracles_pass, six_queue_preservation_pass, coded_error_order_pass, diff_check_pass]
deferred_to: [KI-W7-S009, KI-W7-I001]
prohibited_actions_observed: []
next_subwindow: KI-W7-S003
next_assignment: ASG-KI-W7-S003-01
state_version: 8
state_revision: d3ba540949a0e39b5b3652cb422cc660a2f2f4aff7e67a52dfcfde02e1a2289a
```

The window agent independently inspected the complete diff, exact error shape,
validation order, frozen results, ending hash, syntax, and two-file cumulative
porcelain. S002 is accepted; only S003 is assigned.

## `EV-KI-W7-S017` - S003 independent acceptance and S004 assignment

```yaml
evidence_id: EV-KI-W7-S017
timestamp: 2026-08-24T13:37:00+05:30
reviewed_subwindow: KI-W7-S003
reviewed_assignment: ASG-KI-W7-S003-01
disposition: ACCEPTED_FOR_INTEGRATION
writable_file: email_scraper/src/aws-pipeline/keyword-intelligence/handler.js
starting_digest: c6a38b0bb4adf19058b53b9e24b0ae3308f590a8d2eb387ca82d1bb0ab16c414
ending_digest: b17a1272e67a52216053f345d2c208d3d6d50df75883f45a14df71bb4730b947
diff_numstat: {added: 24, deleted: 3}
actual_backend_changed_files: [src/aws-pipeline/keyword-intelligence/handler.js, src/aws-pipeline/runtime-config.js, src/config.js]
local_checks: [node_check_pass, exact_IF3_source_interface_pass, diff_check_pass]
deferred_to: [KI-W7-S010, KI-W7-I001]
prohibited_actions_observed: []
next_subwindow: KI-W7-S004
next_assignment: ASG-KI-W7-S004-01
state_version: 9
state_revision: a2d26d0c78d9ceb0228807b445320671558ac1451ef29635c29332ec477dbfcf
```

The window agent independently verified the repository construction is limited
to the uninjected branch, activation is fail-closed, injected repository
authority and 32 MiB artifact store are preserved, no environment read exists,
and cumulative scope is exact. S003 is accepted; only S004 is assigned.

## `EV-KI-W7-S018` - S004 independent acceptance and S005 assignment

```yaml
evidence_id: EV-KI-W7-S018
timestamp: 2026-08-24T13:46:00+05:30
reviewed_subwindow: KI-W7-S004
reviewed_assignment: ASG-KI-W7-S004-01
disposition: ACCEPTED_FOR_INTEGRATION
writable_file: email_scraper/src/aws-pipeline/handlers/recovery.js
starting_digest: 7a633679b7d0894c789bf01fb32bd056fdc50ac6a11d8080db52e8fefad81e78
ending_digest: 0218bce551f7d3b65d80b76f3d81f1f37bfa56ef40d67e1105e48f2950e6bc7f
diff_numstat: {added: 19, deleted: 1}
local_checks: [node_check_pass, pipeline_first_and_single_clock_source_oracles_pass, disabled_zero_keyword_pass, active_composition_pass, diff_check_pass]
deferred_to: [KI-W7-S010, KI-W7-I001]
prohibited_actions_observed: []
next_subwindow: KI-W7-S005
next_assignment: ASG-KI-W7-S005-01
state_version: 10
state_revision: 99c5369667ed1ea8651d1c3a6f3be5d32385e7bc17d6ac2cec0a6cf41c5fd4de
```

The window agent independently inspected the full diff and verified pipeline-
first ordering, inactive zero keyword work, exact active repository injection,
one Date capture, preserved limit/error behavior, and exact cumulative scope.
S004 is accepted; only S005 is assigned.

## `EV-KI-W7-S019` - S005 independent acceptance and S006 assignment

```yaml
evidence_id: EV-KI-W7-S019
timestamp: 2026-08-24T14:05:00+05:30
reviewed_subwindow: KI-W7-S005
reviewed_assignment: ASG-KI-W7-S005-01
disposition: ACCEPTED_FOR_INTEGRATION
writable_file: email_scraper/infrastructure/aws/template.yaml
starting_digest: 9e5366c95250d37caf0190611d14ca308b03ee20b9c4a0758c8e82b0233c058f
ending_digest: 2d87c28ad564842d13e42855aef676fb30b2f3aa357ef6eda73bc88f67cb8fa8
diff_numstat: {added: 515, deleted: 1}
local_checks: [json_parse_pass, exact_3_1_10_4_sets_pass, baseline_deep_equality_pass, IAM_and_activation_oracles_pass, alarm_clone_and_single_schedule_pass, diff_check_pass]
deferred_to: [KI-W7-S011, KI-W7-I001]
environment_invalidations: [initial child-process git transport EPERM; read-only fd3 identical oracle passed]
prohibited_actions_observed: []
next_subwindow: KI-W7-S006
next_assignment: ASG-KI-W7-S006-01
state_version: 11
state_revision: 0622d167f7f14427ae610192aca1edec218396ecc3f1258eff6e6baf1de7a920
```

The window agent independently parsed and inspected the topology, exact named
sets, 1080/180/1024/1 bounds, condition, absent scaling, ending digest and
cumulative scope. The leaf's deep-equality oracle proves no unlisted baseline
change. S005 is accepted; only S006 is assigned.

## `EV-KI-W7-S020` - S006 independent acceptance and S007 assignment

```yaml
evidence_id: EV-KI-W7-S020
timestamp: 2026-08-24T14:18:00+05:30
reviewed_subwindow: KI-W7-S006
reviewed_assignment: ASG-KI-W7-S006-01
disposition: ACCEPTED_FOR_INTEGRATION
writable_file: email_scraper/scripts/measure-keyword-worker-package.js
starting_digest: ABSENT
ending_digest: e3c54db213b57af5a30d2475645186db9a138b00a1488f2299085aac4ce68494
diff_numstat: {added: 136, deleted: 0}
local_checks: [node_check_pass, no_main_import_and_exact_exports_pass, IF6_static_contract_pass, no_build_or_output_pass, diff_check_pass]
deferred_to: [KI-W7-S012, KI-W7-I001-CV3]
prohibited_actions_observed: []
next_subwindow: KI-W7-S007
next_assignment: ASG-KI-W7-S007-01
state_version: 12
state_revision: 4a07d8cc3b8708249e56f993800f15c885d363e50b281e0bd54fba287eab5dd0
```

The window agent independently inspected all 136 lines, exact constants,
unsigned sorting, inventory/engine/size/cold-import/report behavior, main guard,
tmp-only cleanup, no ZIP removal and one-file scope. S006 is accepted; only
S007 is assigned.

## `EV-KI-W7-S021` - S007 independent acceptance and S008 assignment

```yaml
evidence_id: EV-KI-W7-S021
timestamp: 2026-08-24T14:38:00+05:30
reviewed_subwindow: KI-W7-S007
reviewed_assignment: ASG-KI-W7-S007-01
disposition: ACCEPTED_FOR_INTEGRATION
writable_file: email_scraper/scripts/keyword-intelligence/create-change-set.js
starting_digest: ABSENT
ending_digest: b2cac13d5457c3f565f1d385ef09578d6efbc36f3dcfaff03e03493423f05c83
diff_numstat: {added: 513, deleted: 0}
local_checks: [node_check_pass, exact_exports_identity_and_arguments_pass, full_activate_allowlists_pass, mutation_guards_and_negative_controls_pass, dry_run_no_AWS_static_pass, diff_check_pass]
deferred_to: [KI-W7-S013, KI-W7-I001]
prohibited_actions_observed: []
next_subwindow: KI-W7-S008
next_assignment: ASG-KI-W7-S008-01
state_version: 13
state_revision: ba108b53221af70df1f1af11f3039e9ab9bae2e51da8279b368636fd0385e9e0
```

The window agent independently inspected the complete module in two source
segments and verified fixed identity, packet/hash/key formula, default no-AWS
branch, A5/W8 gates, encrypted versioned artifact confirmation, exact change
allowlists/details and reviewed-ID reconciliation. S007 is accepted; only S008
is assigned.

## `EV-KI-W7-S022` - S008 independent acceptance and S009 assignment

```yaml
evidence_id: EV-KI-W7-S022
timestamp: 2026-08-24T15:08:00+05:30
reviewed_subwindow: KI-W7-S008
reviewed_assignment: ASG-KI-W7-S008-01
disposition: ACCEPTED_FOR_INTEGRATION
writable_file: email_scraper/scripts/keyword-intelligence/inspect-stack.js
starting_digest: ABSENT
ending_digest: 47ad3e90ac91f51d7d91292618828dd51e88d011bf53ce7625b8adb93c540496
diff_numstat: {added: 490, deleted: 0}
local_checks: [node_check_pass, exact_exports_and_argument_partitions_pass, exact_15_operation_read_only_allowlist_pass, forbidden_operation_and_single_spawn_seam_pass, diff_check_pass]
deferred_to: [KI-W7-S013, KI-W7-I001]
prohibited_actions_observed: []
next_subwindow: KI-W7-S009
next_assignment: ASG-KI-W7-S009-01
state_version: 14
state_revision: 1a90d6c63309ed328ffd32330a183d312f253b7778a002dceb60224e2e8c17ef
```

The window agent independently inspected the complete inspector and verified
the fixed identity, mutually exclusive states, exact exported surface, all
fifteen read-only AWS operations, forbidden-operation fail-closed guard,
privacy-safe return projection, ending digest, and exact cumulative scope.
S008 is accepted; only S009 is assigned.

## `EV-KI-W7-S023` - S009 independent acceptance and S010 assignment

```yaml
evidence_id: EV-KI-W7-S023
timestamp: 2026-08-24T15:18:00+05:30
reviewed_subwindow: KI-W7-S009
reviewed_assignment: ASG-KI-W7-S009-01
disposition: ACCEPTED_FOR_INTEGRATION
writable_file: email_scraper/test/aws-pipeline-runtime-adapters.test.js
starting_digest: 5131d1c7eb0df24516804c2801288b0dd323cd10b4e7933ffdefa52b40b573d6
ending_digest: d4792636a8e551e73bf86b6ec5d90563160040e037cfb147968ef3262321e0ca
diff_numstat: {added: 162, deleted: 0}
local_checks: [node_check_pass, exact_registry_pass, three_ID_activation_pass, focused_3_pass_0_fail_0_skip, queue_preservation_and_error_oracles_pass, two_controls_falsified_and_fresh_positive_pass, diff_check_pass]
deferred_to: [KI-W7-I001]
prohibited_actions_observed: []
next_subwindow: KI-W7-S010
next_assignment: ASG-KI-W7-S010-01
state_version: 15
state_revision: 35f3c4bcde64edc3efbfb3544a8488d57264ebb3387d8630d0238d463cbfa8fe
```

The window agent independently inspected and reran the focused suite. The exact
registry, inactive/active/fail-closed partitions, six established queue values,
coded error and both captured mutation controls pass with exactly three
activated IDs and no skip. S009 is accepted; only S010 is assigned.

## `EV-KI-W7-S024` - S010 recovered, independently accepted and S011 assigned

```yaml
evidence_id: EV-KI-W7-S024
timestamp: 2026-08-24T15:42:00+05:30
reviewed_subwindow: KI-W7-S010
reviewed_assignment: ASG-KI-W7-S010-01
disposition: ACCEPTED_FOR_INTEGRATION
writable_file: email_scraper/test/keyword-intelligence-deployment-runtime.test.js
starting_digest: ABSENT
ending_digest: 69ab1157c82ca70e4eca0d46764064f2b699cfe23b1ccb25aff23704ba807f68
diff_numstat: {added: 325, deleted: 0}
local_checks: [node_check_pass, exact_registry_pass, focused_3_pass_0_fail_0_skip, handler_repository_and_32MiB_oracles_pass, combined_recovery_order_clock_limit_and_failure_oracles_pass, controls_falsified_and_fresh_positive_pass, diff_check_pass]
environment_invalidations: [sandbox child_process spawnSync node EPERM; identical elevated focused run used]
file_local_correction: [NC_03 callback parameter t added before acceptance]
deferred_to: [KI-W7-I001]
prohibited_actions_observed: []
next_subwindow: KI-W7-S011
next_assignment: ASG-KI-W7-S011-01
state_version: 16
state_revision: 41bd25de027ddbd15e03f6e7ec46ac302fb62459810cfea9ccbdadf96c9878f7
```

The sandbox could not create the Node module-mock child process. The window
agent used the authorized identical elevated execution, which exposed one
mechanical test-local missing callback parameter; that byte was corrected
before acceptance. The rerun passed all three IDs and exact runtime/recovery
oracles. S010 is accepted; only S011 is assigned.

## `EV-KI-W7-S025` - S011 independent acceptance and S012 assignment

```yaml
evidence_id: EV-KI-W7-S025
timestamp: 2026-08-24T15:50:00+05:30
reviewed_subwindow: KI-W7-S011
reviewed_assignment: ASG-KI-W7-S011-01
disposition: ACCEPTED_FOR_INTEGRATION
writable_file: email_scraper/test/keyword-intelligence-infrastructure.test.js
starting_digest: ABSENT
ending_digest: 48ead8e7dde4563342c5a5bc9b66ffe822f6e9a4792129290be7c32f349f5636
diff_numstat: {added: 534, deleted: 0}
local_checks: [node_check_pass, exact_registry_pass, focused_11_pass_0_fail_0_skip, six_infrastructure_oracles_pass, five_controls_falsified_and_fresh_positive_pass, baseline_projection_digest_pass, diff_check_pass]
deferred_to: [KI-W7-I001]
prohibited_actions_observed: []
next_subwindow: KI-W7-S012
next_assignment: ASG-KI-W7-S012-01
state_version: 17
state_revision: 941b9f400d156e526a977058f25ff44970504e0c683a6ab09cb256baf4b6aaab
```

The window agent independently reran the complete focused file and inspected
the exact registry, topology, 1080/180 timing relation, activation condition,
least-privilege IAM, single schedule, deep baseline projection and five
mutation controls. All eleven IDs activate once with no skip. S011 is accepted;
only S012 is assigned.

## `EV-KI-W7-S026` - S012 independent acceptance and S013 assignment

```yaml
evidence_id: EV-KI-W7-S026
timestamp: 2026-08-24T16:02:00+05:30
reviewed_subwindow: KI-W7-S012
reviewed_assignment: ASG-KI-W7-S012-01
disposition: ACCEPTED_FOR_INTEGRATION
writable_file: email_scraper/test/keyword-intelligence-build.test.js
starting_digest: ABSENT
ending_digest: 18dcf90026119d2aa98a6b4e1e06ab47647f596adc5033c24d3941f13f0e2731
diff_numstat: {added: 257, deleted: 0}
local_checks: [node_check_pass, exact_registry_and_two_test_definitions_pass, strict_bridge_and_certificate_static_contract_pass, NC10_single_mutation_static_contract_pass, diff_check_pass]
execution_deferred: [W7-BUILD-01, W7-NC-10]
deferred_to: [KI-W7-I001-CV3, KI-W7-I001-CV4]
prohibited_actions_observed: []
next_subwindow: KI-W7-S013
next_assignment: ASG-KI-W7-S013-01
state_version: 18
state_revision: 859d189362b698a637c509b205936bc06694b5cbee0d7cfe753f2f2212de8fcb
```

The window agent independently inspected the complete build owner, strict
bridge schema and current-artifact checks, sole build certificate emission,
and synthetic NC-10 sequence. No build or build-case execution occurred in the
leaf, as required. S012 is accepted; only S013 is assigned.

## `EV-KI-W7-S027` - S013 elevated recovery, independent acceptance and I001 assignment

```yaml
evidence_id: EV-KI-W7-S027
timestamp: 2026-08-24T16:42:00+05:30
reviewed_subwindow: KI-W7-S013
reviewed_assignment: ASG-KI-W7-S013-01
disposition: ACCEPTED_FOR_INTEGRATION
writable_file: email_scraper/test/keyword-intelligence-deployment-guard.test.js
starting_digest: ABSENT
ending_digest: 91b6bd11f5b56da5fe07c26d67395b15573a26a87d2b39df61eaa2c2f7e3f79a
diff_numstat: {added: 905, deleted: 0}
local_checks: [node_check_pass, exact_registry_and_exports_pass, focused_5_pass_0_fail_0_skip, packet_change_set_inspector_stub_oracles_pass, registry_case_control_digests_pass, parser_unchanged_four_mutations_final_unchanged_pass, parser_mode_zero_tests_atomic_safe_output_pass, diff_check_pass]
environment_invalidations: [sandbox nested Node and temporary executable spawn unobservable; identical elevated focused run used]
deferred_to: [KI-W7-I001-CV4]
prohibited_actions_observed: []
next_subwindow: KI-W7-I001
next_assignment: ASG-KI-W7-I001-01
state_version: 19
state_revision: 4f47d9e0444924971b51054be586ea3396b0698207d80e3d3ac7ab5fec95b6c2
```

The accepted elevated focused run passed all five owner IDs and the real
source-only registry/parser protocol, including unchanged, missing, duplicate,
skip, unactivated and fresh-unchanged executions. The window agent inspected
the direct-main zero-test branch, safe failure, atomic output, exact case and
control digests, ending digest and scope. All thirteen leaves are accepted;
only the zero-write I001 assessment is active.

## `EV-KI-W7-S028` - I001 CV5 failure and mechanically governed C001 assignment

```yaml
evidence_id: EV-KI-W7-S028
timestamp: 2026-08-24T17:05:00+05:30
assessment: KI-W7-I001
CV1: PASS
CV2: PASS
CV3: PASS
CV4: PASS
CV3_keyword_sha256: 47fda36e621bcb35a98fd1614854dadc0231e70871cf5488828610400d8460d4
CV3_stable_measurement_sha256: 919e0d086d8206025ca0669798b20bbb879f6b1fbeeb2ca56af02d369d6b8fcc
CV3_bridge_sha256: 9f6ffe010ea714ec78c86080942a7d02d5aec70f727099538fe167e511051be6
CV4_focused_certificate_sha256: b68985a23ccd5d9509151035249b094498f6d2e04e15b17a41d49a91c2f577dd
CV4_counts: {cases: 12, controls: 12, exceptions: 0, ignored_non_W7: 17}
CV5: FAIL
CV5_outer_totals: {files_passed: 61, files_failed: 8}
deterministic_failure: test/keyword-intelligence-build.test.js absent KI_W7_BUILD_EVIDENCE_PATH
focused_reproduction: {pass: 1, fail: 1, skip: 0, error: KI_W7_BUILD_EVIDENCE_PATH is required}
environment_probable_outer_failures: [aws-pipeline-infrastructure.test.js, aws-pipeline-packaging.test.js, keyword-intelligence-api.test.js, keyword-intelligence-deployment-guard.test.js, keyword-intelligence-deployment-runtime.test.js, query-review-server.test.js, server.test.js]
CV6: NOT_RUN
CV7: NOT_RUN
disposition: CORRECTION_REQUIRED
correction: KI-W7-C001
reassessment: KI-W7-I002
superseding_decomposition_revision: 4ab8aff30a8f05dc0a89f50c76c97493a6b0dff6dc599a45974934959db904df
state_version: 20
state_revision: 92f83083738e3a86ee739e317313b79124d1d1d444a22b8334619f8164f42aea
```

CV1/CV2 proved the exact thirteen-path set and static closure. The frozen CV3
and CV4 command completed under one fail-fast wrapper; privacy-safe hashes were
recomputed from the retained deterministic outputs after the wrapper removed
its sole evidence directory. CV5 then exposed that the build owner cannot run
under ordinary `npm test` without the intentionally CV4-only bridge. The
focused absent-environment reproduction isolates this one mechanically governed
test-mode defect. C001 owns only that file and preserves strict CV4 behavior.

## `EV-KI-W7-S029` - C001 independent acceptance and I002 assignment

```yaml
evidence_id: EV-KI-W7-S029
timestamp: 2026-08-24T17:14:00+05:30
reviewed_subwindow: KI-W7-C001
reviewed_assignment: ASG-KI-W7-C001-01
disposition: ACCEPTED_FOR_INTEGRATION
writable_file: email_scraper/test/keyword-intelligence-build.test.js
starting_digest: 18dcf90026119d2aa98a6b4e1e06ab47647f596adc5033c24d3941f13f0e2731
ending_digest: f5adf4065adf9e2970034f94d10c0a8b70b2c443677966933b5faa980055cd32
diff_numstat: {added: 4, deleted: 0}
local_checks: [node_check_pass, absent_environment_2_pass_0_fail_0_skip, exactly_one_NC10_record, zero_build_case_record_or_certificate, inverse_start_digest_pass, diff_check_pass]
invalidated_gates: [CV1, CV2, CV3, CV4, CV5, CV6, CV7]
prohibited_actions_observed: []
next_subwindow: KI-W7-I002
next_assignment: ASG-KI-W7-I002-01
state_version: 21
state_revision: 4c523d9bc3b24b13e32ee1c0d8b7b0cd78751748a47dc68c2af882be335c40ee
```

The window agent independently reran the absent-environment owner file and
verified the correction is exactly the frozen four-line nonactivation guard.
Ordinary regression now passes without inventing a build certificate, while
every present bridge still enters the unchanged strict path. C001 is accepted;
I002 owns the complete invalidated reassessment.

## `EV-KI-W7-S030` - I002 CV4 registration failure and C002 assignment

```yaml
evidence_id: EV-KI-W7-S030
timestamp: 2026-08-24T17:38:00+05:30
assessment: KI-W7-I002
CV1: PASS
CV2: PASS
CV3: PASS
CV3_bridge: {bytes: 2108, sha256: 9f6ffe010ea714ec78c86080942a7d02d5aec70f727099538fe167e511051be6}
CV4_focused_process: PASS
CV4_parser: FAIL
observed_registered: {cases: 9, controls: 10}
missing_owner: deployment_guard
missing_ids: [W7-CONF-01, W7-DEPLOY-01, W7-DEPLOY-02, W7-NC-11, W7-NC-12]
root_cause: S013 directInvocation false when imported after first file under test-isolation=none
diagnostic_TAP_cleanup: PASS
CV5: NOT_RUN
CV6: NOT_RUN
CV7: NOT_RUN
disposition: CORRECTION_REQUIRED
correction: KI-W7-C002
reassessment: KI-W7-I003
superseding_decomposition_revision: ad88ab2430f6d3046f1a41271f93a8f5435669d12cfe071f84f47dcc6c55802e
state_version: 22
state_revision: 5af8c93809c10dd9664d474819063813f708d59b830e119ad9f6fc9cfe29c279
```

The strict parser correctly rejected the real 51-test TAP. Inspection proved
the five S013 IDs were wholly absent while all other owners were present. Under
the frozen nonisolated command, `process.argv[1]` remains the first test file;
`process.execArgv` contains the exact `--test` signal while plain parser imports
do not. C002 owns only this deterministic registration seam.

## `EV-KI-W7-S031` - C002 elevated recovery, independent acceptance and I003 assignment

```yaml
evidence_id: EV-KI-W7-S031
timestamp: 2026-08-24T17:48:00+05:30
reviewed_subwindow: KI-W7-C002
reviewed_assignment: ASG-KI-W7-C002-01
disposition: ACCEPTED_FOR_INTEGRATION
writable_file: email_scraper/test/keyword-intelligence-deployment-guard.test.js
starting_digest: 91b6bd11f5b56da5fe07c26d67395b15573a26a87d2b39df61eaa2c2f7e3f79a
ending_digest: 08d26a2478fa7c83ba83d27b3bdd3a903cbbfe11ec8fd89cbce7beda5362875f
diff_numstat: {added: 2, deleted: 1}
local_checks: [node_check_pass, exact_inverse_start_digest_pass, plain_ESM_import_zero_tests, elevated_two_file_39_pass_0_fail_0_skip, exact_S013_3_cases_2_controls_once, parser_child_controls_pass, diff_check_pass]
environment_invalidations: [sandbox nested child stdout empty; identical elevated two-file recovery passed]
invalidated_gates: [CV1, CV2, CV3, CV4, CV5, CV6, CV7]
prohibited_actions_observed: []
next_subwindow: KI-W7-I003
next_assignment: ASG-KI-W7-I003-01
state_version: 23
state_revision: aae07b35f6ca1bad15f08f71cb9e1d8bfd3716939cd706b0faa02b785e4bcb67
```

The window agent independently ran the corrected two-file nonisolated path
outside the sandbox. All 39 tests passed and S013 contributed its exact five
IDs once; its parser controls also passed. The two-line correction preserves
zero-test plain imports and direct parser behavior. C002 is accepted; I003 owns
the final full reassessment.

## `EV-KI-W7-S032` - I003 CV5 preserved-regression compatibility blocker

```yaml
evidence_id: EV-KI-W7-S032
timestamp: 2026-08-24T18:00:00+05:30
assessment: KI-W7-I003
CV1: PASS
CV1_path_count: 13
CV1_path_digest: 04ce71235fe61103c071f859d6050d4f8fee2b56dc0e088b9d97f5111be57a9f
CV2: PASS
CV3: PASS
CV3_bridge_sha256: 9f6ffe010ea714ec78c86080942a7d02d5aec70f727099538fe167e511051be6
CV3_keyword_zip_bytes: 32006605
CV3_keyword_unzipped_bytes: 84224692
CV4: PASS
CV4_focused_certificate_sha256: b68985a23ccd5d9509151035249b094498f6d2e04e15b17a41d49a91c2f577dd
CV4_required_cases: 12
CV4_required_controls: 12
CV4_ignored_non_w7_tests: 17
CV4_exceptions: 0
CV5: FAIL
CV5_totals: {tests: 794, pass: 717, fail: 4, skip: 73}
CV5_failures:
  - {file: email_scraper/test/aws-pipeline-infrastructure.test.js, oracle: exact resource count, expected: 72, actual: 82}
  - {file: email_scraper/test/aws-pipeline-infrastructure.test.js, oracle: deployment-packet full resource count, expected: 72, actual: 82}
  - {file: email_scraper/test/aws-pipeline-packaging.test.js, oracle: established measurements report exists, missing: dist/lambda/measurements.json}
  - {file: email_scraper/test/aws-pipeline-packaging.test.js, oracle: SCN-KI-027 sibling-preservation baseline exists, missing: dist/lambda/measurements.json}
diagnosis:
  infrastructure_test_starting_digest: 3bfa45fab2beb2613be395e2a903fa87cdfef2a3b8c558073483acd504da13f8
  infrastructure_exact_literal_updates: [roles.length 7_to_8, alarms.length 27_to_31, template.Resources 72_to_82, packet.full.resources 72_to_82]
  packaging_source_change_required: false
  omitted_established_command: node scripts/measure-lambda-packages.js
  corrected_schedule_position: immediately_after_node_scripts_build-lambda.js_and_before_the_established_sibling_snapshot
  corrected_planned_path_count: 14
  corrected_planned_path_digest: dd30a08f7f9bfa66d224c2b8f72758557d0823bf392e1f59c7a4ca2f26640836
CV6: NOT_RUN
CV7: NOT_RUN
external_actions: []
paid_cost_usd: "0.00"
disposition: PARENT_BLOCKED
parent_decision_required:
  - authorize one-file KI-W7-C003 owning only email_scraper/test/aws-pipeline-infrastructure.test.js and the four literal count updates above
  - authorize KI-W7-I004 to rerun invalidated CV1-CV4 with the corrected CV3 measurement order, then CV5-CV7
state_version: 24
```

The four failures reduce to one omitted compatibility decision, not four
product defects. W7 legitimately adds ten resources, four alarms, and one IAM
role, so the preserved infrastructure test's four old totals cannot remain
true. Separately, the preserved packaging suite consumes the established
`measurements.json`; `build-lambda.js` recreates the build root but does not
produce that report. The already-existing `measure-lambda-packages.js` is its
sole producer and requires no source edit. Because the preserved test file is
outside A5's exact 13-file scope and I003 has zero implementation-write
authority, CV6/CV7 were not run and KI-W8 was not begun.
