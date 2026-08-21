# Keyword Intelligence Append-Only Specification Changelog (`A7`)

This is the sole authority for specification revisions, causes, impact,
invalidation, compatibility, authorization, and resumption. Append entries;
never rewrite an assigned/completed revision and never reuse an ID.

The other artifacts are `A1` `KEYWORD_INTELLIGENCE_PRODUCT_CONTRACT.md`, `A2`
`KEYWORD_INTELLIGENCE_DISCOVERY_DOSSIER.md`, `A3`
`KEYWORD_INTELLIGENCE_DECISION_LEDGER.md`, `A4`
`KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md`, `A5`
`ACTIVE_EXECUTION_STATE.md`, `A6`
`KEYWORD_INTELLIGENCE_EXECUTION_EVIDENCE.md`, and `A8`
`KEYWORD_INTELLIGENCE_TRACEABILITY_INDEX.md`.

## Change records

```yaml
change_id: CHG-KI-001
timestamp: 2026-08-17T00:00:00+05:30
trigger_evidence: [SRC-KI-004, SRC-KI-005, EV-KI-A-001]
reason: Compile the product-level KeywordSearchVolume integration plan into the eight-artifact project-agnostic decision-complete format without authorizing implementation.
old_revision: KEYWORD_SEARCH_VOLUME_INTEGRATION_PLAN.md planning draft
new_revision: KI-PC-1 / KI-DD-1 / KI-DL-1 / KI-CL-1
changed_requirements: []
changed_decisions: [DEC-KI-001, DEC-KI-002, DEC-KI-003, DEC-KI-004, DEC-KI-005, DEC-KI-006, DEC-KI-007, DEC-KI-008, DEC-KI-009, DEC-KI-010, DEC-KI-011, DEC-KI-012, DEC-KI-013, DEC-KI-014, DEC-KI-015, DEC-KI-016, DEC-KI-017, DEC-KI-018, DEC-KI-019, DEC-KI-020, DEC-KI-021, DEC-KI-022, DEC-KI-023, DEC-KI-024, DEC-KI-025]
affected_windows: [KI-W1, KI-W2, KI-W3, KI-W4, KI-W5, KI-W6, KI-W7, KI-W8]
invalidated_evidence: []
compatibility_or_migration_effect: No implementation or data effect. The old plan remains product provenance but is superseded as an execution specification after activation.
authorization_effect: None. ACTIVE_EXECUTION_STATE.md remains at G-R31; all KI windows remain unassigned.
resumption_state: Close GATE-KI-001 and GATE-KI-002, rehash A1/A4, append AUTHORING-READY evidence, then create a new one-window A5 assignment for KI-W1.
```

```yaml
change_id: CHG-KI-002
timestamp: 2026-08-17T00:00:01+05:30
trigger_evidence: [SRC-KI-028, SRC-KI-029]
reason: The first audit preserved paid-call ambiguity but omitted the workspace-required pre-call cost reservation and requester-owned maximum research spend.
old_revision: A1 944dff30a7245d5ed9adfd1871251201e06f4a288a3ac8b03d66d5d7ef72aca7 / A4 bea0f48b0aeda1c4157db1996a3f9346376bfd24b88505060561e5da2599e39f
new_revision: A1 89e728c7c80c5edcc48d27665f3ccf383acaabf3226f4bfc7656c0999e75b867 / A4 9346c29887412c3fbeaf628f23f1c2b5674dd3d81cb4cda2ce3e1db7e360c5e1
changed_requirements: [REQ-KI-022, AUTH-KI-007]
changed_decisions: [DEC-KI-009, DEC-KI-021, DEC-KI-025]
affected_windows: [KI-W1, KI-W3, KI-W6, KI-W8]
invalidated_evidence: []
compatibility_or_migration_effect: Adds reservation/provider cost fields to the unimplemented forward schema plan; no existing data or code changed.
authorization_effect: Adds requester gate GATE-KI-003; no KI window can be assigned until exact values are approved and inserted.
resumption_state: Resolve GATE-KI-003, append its literal policy and tests, then close GATE-KI-001/GATE-KI-002 and rerun readiness.
```

```yaml
change_id: CHG-KI-003
timestamp: 2026-08-17T00:00:02+05:30
trigger_evidence: [EV-KI-A-021]
reason: Final frozen-plan cross-check found incompatible lease intervals and an ambiguous artifact-limit implementation.
old_revision: A1 89e728c7c80c5edcc48d27665f3ccf383acaabf3226f4bfc7656c0999e75b867 / A4 9346c29887412c3fbeaf628f23f1c2b5674dd3d81cb4cda2ce3e1db7e360c5e1
new_revision: A1 89e728c7c80c5edcc48d27665f3ccf383acaabf3226f4bfc7656c0999e75b867 / A4 ae876057c105c1dbe409f10ebf63ac500f8be9c0f57d58ed7201c47f57d2e1d8
changed_requirements: []
changed_decisions: [DEC-KI-022, DEC-KI-024]
affected_windows: [KI-W1, KI-W3]
invalidated_evidence: [EV-KI-A-020 A4 hash only]
compatibility_or_migration_effect: No implementation or data effect. The planned worker now uses the accepted coordinator lease constants and an isolated larger artifact-store instance; existing pipeline runtime behavior is unchanged.
authorization_effect: None; all KI windows remain unassigned and the same three gates remain open.
resumption_state: Resolve GATE-KI-003, close GATE-KI-001/GATE-KI-002, rerun readiness using the new A4 hash, and only then assign KI-W1.
```

```yaml
change_id: CHG-KI-004
timestamp: 2026-08-17T00:00:03+05:30
trigger_evidence: [EV-KI-A-022]
reason: Mechanical scenario lint showed that combined labels and one shared cleanup statement did not satisfy the standard's per-scenario field requirement.
old_revision: A1 89e728c7c80c5edcc48d27665f3ccf383acaabf3226f4bfc7656c0999e75b867 / A4 ae876057c105c1dbe409f10ebf63ac500f8be9c0f57d58ed7201c47f57d2e1d8
new_revision: A1 89e728c7c80c5edcc48d27665f3ccf383acaabf3226f4bfc7656c0999e75b867 / A4 d2169ea2a4c4eb93ac85cf5cd9169f668780a70947cb177403986a0066a1c746
changed_requirements: []
changed_decisions: []
affected_windows: [KI-W1, KI-W2, KI-W3, KI-W4, KI-W5, KI-W6, KI-W7, KI-W8]
invalidated_evidence: [EV-KI-A-020 A4 hash only, EV-KI-A-021 A4 hash only]
compatibility_or_migration_effect: None; scenario acceptance fields were decomposed without changing product behavior or implementation scope.
authorization_effect: None; all KI windows remain unassigned and the same three gates remain open.
resumption_state: Use the new A4 hash for subsequent lint/readiness and resolve the existing three gates before assignment.
```

```yaml
change_id: CHG-KI-005
timestamp: 2026-08-17T00:00:04+05:30
trigger_evidence: [EV-KI-A-023]
reason: The decomposed scenarios retained multi-layer parity labels; the standard requires one declared parity class per scenario.
old_revision: A1 89e728c7c80c5edcc48d27665f3ccf383acaabf3226f4bfc7656c0999e75b867 / A4 d2169ea2a4c4eb93ac85cf5cd9169f668780a70947cb177403986a0066a1c746
new_revision: A1 89e728c7c80c5edcc48d27665f3ccf383acaabf3226f4bfc7656c0999e75b867 / A4 2c5129f628d0a6dd9cf5f904b6fdaf918922f2f9c059f3aae1b5ef5be1a3eabe
changed_requirements: []
changed_decisions: []
affected_windows: [KI-W2, KI-W3, KI-W4, KI-W5, KI-W6, KI-W8]
invalidated_evidence: [EV-KI-A-020 A4 hash only, EV-KI-A-021 A4 hash only, EV-KI-A-022 A4 hash only]
compatibility_or_migration_effect: None; only evidence-class labels changed.
authorization_effect: None; all KI windows remain unassigned and the same three gates remain open.
resumption_state: Use the new A4 hash for subsequent lint/readiness and resolve the existing three gates before assignment.
```

```yaml
change_id: CHG-KI-006
timestamp: 2026-08-17T12:02:05+05:30
trigger_evidence: [SRC-KI-030, SRC-KI-031, SRC-KI-032, EV-KI-A-026, EV-KI-A-027]
reason: Requester replaced nine-market expansion with US-only expansion plus a US metric screen and fixed shortlist, approved exact reservation formulas, and fixed maxCostPerResearchUsd at $3 so implementers cannot reinterpret provider economics.
old_revision: A1 89e728c7c80c5edcc48d27665f3ccf383acaabf3226f4bfc7656c0999e75b867 / A4 2c5129f628d0a6dd9cf5f904b6fdaf918922f2f9c059f3aae1b5ef5be1a3eabe / A5 state 66
new_revision: KI-PC-2 / KI-DD-2 / KI-DL-2 / KI-CL-2 / KI-TR-2; A1 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c / A4 661a8158ef4bc587392c3af0127e560fb978bc06a84f66cd82106c21c5ec9297 / A5 state 67
changed_requirements: [REQ-KI-003, REQ-KI-004, REQ-KI-022, REQ-KI-023, REQ-KI-024, AUTH-KI-002, AUTH-KI-007]
changed_decisions: [DEC-KI-004, DEC-KI-005, DEC-KI-006, DEC-KI-009, DEC-KI-010, DEC-KI-018, DEC-KI-020, DEC-KI-021, DEC-KI-024, DEC-KI-025]
affected_windows: [KI-W1, KI-W2, KI-W3, KI-W5, KI-W6, KI-W8]
invalidated_evidence: [EV-KI-A-020 A1/A4 hash only, EV-KI-A-021 A4 hash only, EV-KI-A-022 A4 hash only, EV-KI-A-023 A4 hash only, EV-KI-A-024 A1/A4 hash and 72/7 count only, EV-KI-A-025 A1/A4 hash and open-gate list only]
compatibility_or_migration_effect: No implementation or data effect because no KI window was assigned. The future Node collection topology intentionally differs from the standalone Python market loop; post-collection calculation parity remains required.
authorization_effect: Closes GATE-KI-003 as a specification decision only. No paid call, dependency installation, implementation, AWS action, or production write is authorized. A5 retains documentation-only allowed actions and GATE-KI-002 remains open.
resumption_state: Correct the non-cost PC-015 placeholders, then obtain requester authorization for GATE-KI-002 dependency installation/build proof. Rerun readiness and assign KI-W1 only if every required item passes.
```

```yaml
change_id: CHG-KI-007
timestamp: 2026-08-17T13:20:00+05:30
trigger_evidence: [EV-KI-A-028]
reason: PC-015 named pre-existing non-cost placeholders; the three new state enums lacked enumerated values and DEC-KI-021 deferred two field sets to "current pipeline-stage/task field set" instead of literal contracts.
old_revision: A3 KI-DL-2 / A4 KI-CL-2 / A5 state 67 / A1 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c / A4 661a8158ef4bc587392c3af0127e560fb978bc06a84f66cd82106c21c5ec9297
new_revision: A3 KI-DL-3 / A4 KI-CL-3 / A5 state 68 / A1 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c / A4 e345305dc57c32acae3a529ae15d5d7cb4ef283b3d29885557cc7e875a4f85b8
changed_requirements: []
changed_decisions: [DEC-KI-021]
affected_windows: [KI-W1]
invalidated_evidence: [EV-KI-A-027 A4 hash and 75/4 count only]
compatibility_or_migration_effect: None on future generated SQL because no KI window ran; KI-W1-T1 now imports literal enum values and field lists instead of deriving them from the live schema at implementation time.
authorization_effect: None; closes readiness item PC-015 as documentation only. GATE-KI-002 remains stopped pending requester authorization and no implementation, install, provider call, or AWS action is granted.
resumption_state: Obtain requester authorization for GATE-KI-002 dependency installation and representative build proof; then materialize fixtures, rerun readiness for PP-006/PC-011/PR-006, append AUTHORING-READY if all pass, and assign KI-W1 by one-window A5.
```

```yaml
change_id: CHG-KI-008
timestamp: 2026-08-17T14:10:00+05:30
trigger_evidence: [SRC-KI-033, EV-KI-A-029, EV-KI-A-030]
reason: GATE-KI-002 executed: exact dependency installs, representative Node/Next build proof, emitted inventory/sizes/startup, fixture materialization/validation; readiness items PP-006/PC-011/PR-006 now pass and the package becomes AUTHORING-READY.
old_revision: A2 KI-DD-2 / A3 KI-DL-3 / A4 KI-CL-3 / A5 state 68 / A1 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c / A4 e345305dc57c32acae3a529ae15d5d7cb4ef283b3d29885557cc7e875a4f85b8
new_revision: A2 KI-DD-3 / A3 KI-DL-3 / A4 KI-CL-4 / A5 state 70 / A1 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c / A4 a12174f3ea692a896bb5b42031c09938bb7680474d5d2dd36682c63b3ac4b6f5
changed_requirements: []
changed_decisions: []
affected_windows: [KI-W1, KI-W2, KI-W3, KI-W5]
invalidated_evidence: []
compatibility_or_migration_effect: Dependency manifests gain @noble/hashes@2.2.0 (backend) and chart.js@3.9.1 + chartjs-chart-treemap@2.0.0 (frontend); note for W1/W2 that the correct ESM subpath is @noble/hashes/sha2.js. Four synthetic fixture files added under email_scraper/test/fixtures/keyword-intelligence/ (content hashes in EV-KI-A-029); KI-W3 consumes them unchanged unless a new change entry records otherwise.
authorization_effect: Closes GATE-KI-002 as local install/build/fixture proof only; AUTHORING-READY (EV-KI-A-030) plus A5 state 70 assign KI-W1 to execution. No provider call, AWS action, production write, frontend source edit, or commit is granted; KI-W7/KI-W8 gates unchanged.
resumption_state: Execute KI-W1 (durable schema + fenced repository) per its window contract; verify P1–P4 preconditions first; stop after KI-W1 acceptance for the requester review before any KI-W2 assignment.
```

```yaml
change_id: CHG-KI-009
timestamp: 2026-08-17T17:08:16+05:30
trigger_evidence: [EV-KI-A-031, EV-KI-A-032]
reason: Post-W2 review of the accepted repository against the drafted W3 caller exposed missing or contradictory worker context, retry/throttle, fencing, atomic publication, recovery, identity, queue-injection, and replay-time behavior. W3 could not implement safely inside its write scope without inventing those choices.
old_revision: A3 KI-DL-3 / A4 KI-CL-4 / A8 KI-TR-2 / A5 state 73 / A1 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c / A4 e4186011a7e1b5d4e3e7571ff3b979eedd5e11e4af4010bc434d4c324be613a9
new_revision: A3 KI-DL-4 / A4 KI-CL-5 / A8 KI-TR-3 / A5 state 74 / A1 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c / A4 35f7236d5213040ffc9dfd2cd8973bd460a5201ce7163aa46daeaf9249c1827e
changed_requirements: []
changed_decisions: [DEC-KI-009 clarification, DEC-KI-026, DEC-KI-027]
affected_windows: [KI-W2 successor edge only, KI-R1 new, KI-W3, KI-W7]
invalidated_evidence: [EV-KI-A-026 wording that omitted planned rows from held exposure only; EV-KI-A-030 as blanket authoring-readiness evidence for unstarted post-W2 windows; KI-W1 and KI-W2 execution evidence remains valid]
compatibility_or_migration_effect: No schema, migration, data, provider, AWS, package, frontend, or application-source change. KI-R1 is an append-only correction to accepted repository behavior using the existing schema; it preserves W1/W2 history and fixes repository selection IDs to the already accepted DEC-KI-002 six-byte formula.
authorization_effect: No implementation is assigned. A5 still stops at KI-W2 AWAITING_REVIEW and permits documentation/read-only review only. KI-R1 becomes the next candidate after that review; KI-W3 remains unassignable until KI-R1 is assigned, executed, evidenced, reviewed, and accepted.
resumption_state: Review KI-W2 and this correction package; if accepted, CAS A5 to a one-window KI-R1 assignment using the current A1/A4 hashes. Execute only KI-R1, stop at its review boundary, and assign KI-W3 only after SCN-KI-020 and all KI-R1 acceptance checks pass.
```

## Required correction protocol

When source or execution evidence contradicts A1–A4:

1. stop the affected assignment without beginning its successor;
2. append exact contradiction evidence to A6;
3. allocate the next `CHG-KI-*` ID and identify requirements, decisions,
   windows, evidence, compatibility, and authorization impact;
4. append corrected contract/decision/checklist text—do not rewrite completed
   evidence or reuse a task/window/scenario ID;
5. hash the corrected A1/A4;
6. create a new uniquely numbered corrective window when code changes are
   required after acceptance; an ordinary locked defect in the current
   unaccepted active window reopens that same window; and
7. version-CAS A5 to a new assignment only after the correction passes the
   authoring/readiness audits.

An ordinary defect whose required behavior is already locked is fixed inside
the active window and does not change this specification.

```yaml
change_id: CHG-KI-010
timestamp: 2026-08-17T19:12:50+05:30
trigger_evidence: [EV-KI-R1-10]
reason: Independent review falsified the first KI-R1 completeness claim with attempt-five marker replay, later-clock retry replay, and zero-row/partial-state final-publication schedules omitted by the original integration cases. The required behavior is already literal in DEC-KI-026, and KI-R1 was never accepted, so the requester directed the parent to reopen KI-R1 rather than invent KI-R2.
old_revision: A4 KI-CL-5 / A8 KI-TR-3 / A5 state 79 / A1 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c / A4 c8f4781a6c983e87756b414a9389c3dacd75ad83eba863e052b27a23075ee913
new_revision: A4 KI-CL-6 / A8 KI-TR-4 / A5 state 80 / A1 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c / A4 05deeaa7fc4ea78c2b48dc4840ebc9f542d7bd81ad180cc37a45b47cd5d23582
changed_requirements: []
changed_decisions: []
affected_windows: [KI-R1 reopened, KI-W3 remains blocked]
invalidated_evidence: [EV-KI-R1-03 completeness claim only; its observed 23/23 result remains historical fact, EV-KI-R1-09 readiness-to-accept implication only]
compatibility_or_migration_effect: No schema, migration, payload, API, provider, AWS, frontend, or package change. SCN-KI-021 adds missing adversarial schedules to the same three-file KI-R1 ownership boundary.
authorization_effect: Reopens only KI-R1 at A5 state 80 with its original source/test scope and isolated test-database authority. KI-W3, provider calls, AWS operations, production writes, schema/migrations, API/frontend, package changes, and commits remain prohibited.
resumption_state: The KI-R1 agent executes the six unchecked remediation items and SCN-KI-021, appends new evidence, CAS-returns A5 to AWAITING_REVIEW, and stops. Parent acceptance is required before any KI-W3 assignment.
```

```yaml
change_id: CHG-KI-011
timestamp: 2026-08-18T00:53:40+05:30
trigger_evidence: [EV-KI-W3-04, EV-KI-A-033]
reason: Independent parent review rejected the initial KI-W3 handoff. In addition to W3-owned defects, the review proved accepted predecessor repository code has no aggregation heartbeat, permits expired task heartbeat revival, excludes exact-expiry aggregation reclaim, and lacks live-expiry predicates on ordinary terminal/publication/failure writes. W3 cannot repair that accepted-file interface within its scope, so a narrow repository-only corrective window is required before W3 can be reopened safely.
old_revision: A3 KI-DL-4 / A4 KI-CL-6 / A8 KI-TR-4 / A5 state 86 / A1 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c / A4 e25e4ce69f1ef0cb619649bb5b15479246f74b66369e65d48d364b1ac93ff820
new_revision: A3 KI-DL-5 / A4 KI-CL-7 / A8 KI-TR-5 / A5 state 87 / A1 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c / A4 236a41cdad93883b6494d84beb2d859a6739f32dab0ec58a147bcebff76c8883
changed_requirements: []
changed_decisions: [DEC-KI-028 additive lease-boundary decision; DEC-KI-022 and DEC-KI-026 semantics unchanged]
affected_windows: [KI-W3 initial handoff rejected and paused, KI-R2 new and assigned, KI-W3 reopened only after KI-R2 acceptance, KI-W4 and later remain blocked]
invalidated_evidence: [EV-KI-W3-02 full-regression/no-regression claim and write-scope claim, EV-KI-W3-03 no-code-defects/completeness claim, A5 state 86 requester_stop acceptance implication; EV-KI-W3-01 remains valid historical precondition evidence]
compatibility_or_migration_effect: No schema, migration, payload, message, artifact, API, provider, AWS, package, frontend, or product behavior change. KI-R2 adds one repository callable and tightens only existing lease predicates in one production file; W3 output at backend f9457de is preserved read-only until W3 is reopened.
authorization_effect: A5 state 87 assigns only KI-R2. It authorizes seven named repository methods, additive cases in two repository test files, isolated disposable-schema writes, and evidence updates. W3 files, provider/AWS/production actions, schema/migrations, packages, frontend/API, build output, and commits are prohibited.
resumption_state: Execute and evidence KI-R2, CAS A5 to AWAITING_REVIEW, and stop. After independent parent acceptance, A5 may reopen the same unaccepted KI-W3 window for its separately enumerated W3-owned remediation; KI-W4 remains blocked until W3 eventually passes all original acceptance checks.
```

```yaml
change_id: CHG-KI-012
timestamp: 2026-08-18T10:56:44+05:30
trigger_evidence: [EV-KI-R2-05, EV-KI-A-034]
reason: Independent review of the KI-R2 second-attempt test source found two claimed schedules were not executed: same-token task heartbeat at its original exact expiry, and stale-A aggregation heartbeat plus row equality after B reclaims at the renewed exact expiry. The requester directed reopening the still-unaccepted KI-R2 window and rejected allocating KI-R3. The same review found the earlier verification policy repeated substantially more integration work than the risk required.
old_revision: A3 KI-DL-5 / A4 KI-CL-7 / A8 KI-TR-5 / A5 state 90 / A1 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c / A4 236a41cdad93883b6494d84beb2d859a6739f32dab0ec58a147bcebff76c8883
new_revision: A3 KI-DL-6 / A4 KI-CL-8 / A8 KI-TR-6 / A5 state 91 / A1 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c / A4 1da44b03d2726d1691b178b60dcc89a7f17de8ca6dc233359d94165628c6cd65
changed_requirements: []
changed_decisions: [DEC-KI-029 risk-proportionate frozen pre-handoff verification]
affected_windows: [KI-R2 requester-reopened proof gate, KI-W3 remains blocked]
invalidated_evidence: [EV-KI-R2-04 completeness claim and no-commit statement only; its observed source hash and executed test results remain historical facts]
compatibility_or_migration_effect: No product, schema, migration, API, payload, provider, AWS, package, frontend, build, or production-source change. KI-R2-RT2 owns one additive integration scenario only.
authorization_effect: By explicit requester exception, A5 state 91 resumes the same unaccepted KI-R2 window rather than allocating a unique corrective-window label. New task/scenario/assignment/evidence/state/change IDs remain unique. Only additive SCN-KI-023 test symbols, one focused isolated database acceptance run after final edit, one frozen npm test and secret scan, append-only evidence, and A5 handoff CAS are authorized. Repository/W3 source, full database integration, Prisma checks, build/measure, commits/pushes, provider/AWS/production actions, schema/migrations/packages/frontend remain prohibited.
resumption_state: The named KI-R2 remediation agent adds SCN-KI-023, runs the focused database pattern once after edits stop, runs the frozen workspace regression and secret scan once, records cleanup/hashes/evidence, CAS-updates A5 to AWAITING_REVIEW, and stops. Parent acceptance is required before KI-W3 may be assigned.
```

```yaml
change_id: CHG-KI-013
timestamp: 2026-08-18T12:00:33+05:30
trigger_evidence: [EV-KI-W3-04, EV-KI-R2-07, EV-KI-W3-05, EV-KI-A-035]
reason: KI-R2 is accepted, but the unaccepted W3 source and its original checklist still leave eight reachable W3-owned implementation choices or defects unresolved. The requester requires reopening W3 as a one-shot decision-complete window whose successful parent acceptance proceeds directly to W4.
old_revision: A3 KI-DL-6 / A4 KI-CL-8 / A8 KI-TR-6 / A5 state 93 / A1 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c / A4 1da44b03d2726d1691b178b60dcc89a7f17de8ca6dc233359d94165628c6cd65
new_revision: A3 KI-DL-7 / A4 KI-CL-9 / A8 KI-TR-7 / A5 state 94 / A1 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c / A4 f7f98d54df9f6b872edaf00c79cf59ea87d067fe0f63172bab97d56a9f988a93
changed_requirements: []
changed_decisions: [DEC-KI-030 additive final W3 settlement, ambiguity, recovery, monitoring, continuation, bound, and build decisions; DEC-KI-001 through DEC-KI-029 unchanged]
affected_windows: [KI-W3 reopened and assigned as the sole implementation window, KI-W4 remains next and is assignable only after successful parent acceptance of W3]
invalidated_evidence: [EV-KI-W3-01 through EV-KI-W3-03 as W3 completion/acceptance evidence; their observed commands and source history remain facts, EV-KI-W3-04 rejection remains authoritative]
compatibility_or_migration_effect: No product requirement, schema, migration, provider payload, pricing formula, API, frontend, package, AWS topology, or accepted repository behavior changes. The window corrects only the enumerated unaccepted W3 symbols and adds exact component/integration/build acceptance coverage.
authorization_effect: A5 state 94 authorizes only the exact KI-W3 F1 symbols, final focused tests, one frozen isolated-database gate, one frozen build/regression/secret sequence, append-only W3 handoff evidence, and a one-version A5 CAS to AWAITING_REVIEW. Provider/AWS/production actions, repository/schema/migration/API/frontend/package edits, full database integration, repeated acceptance runs, commits/pushes, and KI-W4 work remain prohibited.
resumption_state: Execute A4 KI-W3 cumulatively through T1/T2 and RT1-RT4, satisfy SCN-KI-001/004-007/012/013/024-027 on the final tree, append the handoff, CAS A5 to AWAITING_REVIEW, and stop. Parent review reruns only decisive W3 oracles and, on success, assigns KI-W4 directly; a correction window is not a successful branch.
```

```yaml
change_id: CHG-KI-014
timestamp: 2026-08-18T15:10:00+05:30
trigger_evidence: [EV-KI-W3-06, EV-KI-W3-07, EV-KI-A-036]
reason: Independent review of the second unaccepted W3 handoff proved its broad scenario labels were not enforcement-complete and found four reachable runtime defects plus two exact-interface/evidence contradictions. The requester explicitly requires a new decision-complete and enforcement-complete corrective window for a subagent, so a unique KI-R3 is allocated rather than reopening W3 again.
old_revision: A3 KI-DL-7 / A4 KI-CL-9 / A8 KI-TR-7 / A5 state 95 / A1 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c / A4 f7f98d54df9f6b872edaf00c79cf59ea87d067fe0f63172bab97d56a9f988a93
new_revision: A3 KI-DL-8 / A4 KI-CL-10 / A8 KI-TR-8 / A5 state 96 / A1 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c / A4 fd4a2fba8acbc0eb82f09fb76d5058796ab876e9f6afccc9987efdd6b061b6e1
changed_requirements: []
changed_decisions: [DEC-KI-031 additive settlement-result, provider-boundary, ordinary-terminal, recovery-classification, dispatcher-strictness, helper-inventory, and mechanical-enforcement decisions]
affected_windows: [KI-W3 second handoff rejected and retained as source baseline, KI-R3 new and assigned, KI-W4 remains blocked until parent acceptance of KI-R3]
invalidated_evidence: [EV-KI-W3-06 completion/readiness/no-defect claims; its observed file hashes, commands, package measurements, and zero-external-cost facts remain historical observations, EV-KI-A-035 readiness implication for W3 only]
compatibility_or_migration_effect: No product requirement, provider payload, pricing formula, schema, migration, repository, API, frontend, package dependency, AWS topology, or artifact/message contract changes. KI-R3 edits four existing private/runtime symbols, adds one test-only manifest and additive tests, and reuses accepted R1/R2/build evidence by hash.
authorization_effect: A5 state 96 authorizes only KI-R3's four named production symbols, literal additive manifest/test members, one final non-database gate, one focused isolated-database gate, two keyword builds, one unchanged packaging test, one npm test, one secret scan, append-only handoff evidence, and one A5 CAS. Provider/AWS/production/Prisma/seven-handler/repository/schema/migration/contract/key/handler/recovery/build-script/API/frontend/package/commit/push/KI-W4 actions remain prohibited.
resumption_state: Execute only A4 KI-R3-T1 through T4 and SCN-KI-028 through 032, run the frozen risk-proportionate gates once after edits stop, append EV-KI-R3-01, CAS A5 to AWAITING_REVIEW, and stop. Only a later parent review may accept cumulative W3/KI-R3 and assign KI-W4.
```

```yaml
change_id: CHG-KI-015
timestamp: 2026-08-18T20:00:00+05:30
trigger_evidence: [EV-KI-R3-01, EV-KI-R3-02, EV-KI-A-037, EV-KI-R4-S04]
reason: Parent review rejected KI-R3 enforcement completeness and allocated KI-R4; the recursive decomposition was then corrected to prohibit the window-agent leaf role and reconcile the already-exact R4 manifest.
old_revision: A3 KI-DL-8 / A4 KI-CL-10 / A5 state 97 / backend 077213cc7c33fa8209a1e5d8ff365b73766500dc
new_revision: A3 KI-DL-9 / A4 KI-CL-11 / A5 state 98 / S1 91b499cc2885937b23daa3186709ca2e0720c939435e4588b4050e2503abcd85
changed_requirements: []
changed_decisions: [DEC-KI-032]
affected_windows: [KI-R3 rejected, KI-R4 assigned, KI-W4 remains blocked pending KI-R4 acceptance]
invalidated_evidence: [EV-KI-R3-01 completion and successor-readiness claims only]
compatibility_or_migration_effect: No product, schema, migration, provider, API, frontend, package, or AWS contract change.
authorization_effect: A5 state 98 authorizes the KI-R4 window agent to coordinate sequential single-file leaves and personally assess integration; it does not authorize implementation edits by the window agent or KI-W4 work.
resumption_state: The KI-R4 window agent assigns S001 to a separate leaf agent, continues the remaining ordered leaves, performs I001, and returns READY_FOR_PARENT_REVIEW. Only parent acceptance may assign KI-W4.
```

```yaml
change_id: CHG-KI-016
timestamp: 2026-08-18T18:16:14+05:30
trigger_evidence: [EV-KI-R4-S18, EV-KI-R4-02, EV-KI-A-038]
reason: KI-R4 is now parent-accepted, but the earlier W4 prose predated the revised enforcement-completeness standard and left truthful stage-derived progress, research-backed non-product confirmation, durable keyword lineage across query edits, rollback on invalid post-write callback output, exact callback/worker discrimination, and executable coverage closure insufficiently specified. W4 is reauthored before assignment so its window agent can mechanically decompose it into sequential single-file leaves.
old_revision: A3 KI-DL-9 / A4 KI-CL-11 / A8 KI-TR-9 / A5 state 98 / backend 077213cc baseline named by the old active assignment
new_revision: A3 KI-DL-10 / A4 KI-CL-12 / A8 KI-TR-10 / A5 state 99 unassigned / accepted backend d98ad53c02d8d8205d614043436164d85b84c6ce
changed_requirements: []
changed_decisions: [DEC-KI-033 additive W4 owner API, immutable handoff, durable research edit, non-product confirmation, and enforcement closure]
affected_windows: [KI-R4 accepted, KI-W4 reauthored but unassigned, KI-W5 remains blocked]
invalidated_evidence: [EV-KI-A-037 current-readiness and assignment statements only; its KI-R4 authoring facts remain historical]
compatibility_or_migration_effect: No schema, migration, application source, provider payload/economics, AWS, package, frontend, or deployed behavior changed. W4 preserves the legacy product-only query branch and adds a separately discriminated research-backed branch when implemented.
authorization_effect: This is authoring and parent-acceptance bookkeeping only. A5 state 99 authorizes no window, agent, file, decomposition artifact, implementation, test, provider, AWS, production, commit, push, or successor action. W4 requires a separate future assignment CAS.
resumption_state: A future parent assignment may name one KI-W4 window agent, authorize only its three coordination artifacts, and require parent approval of the exact ten-file/34-case single-file decomposition before the first leaf. Stop before that assignment in the current turn.
```

```yaml
change_id: CHG-KI-017
timestamp: 2026-08-18T19:22:30+05:30
trigger_evidence: [EV-KI-W4-S01, EV-KI-W4-S03, EV-KI-A-039]
reason: A5 state 100 carried stale pre-CHG-KI-016 A3/A4 byte pins (and EV-KI-A-038 additionally pinned a stale A8 hash); the window agent's delta audit and the parent's independent digest authentication established that the observed KI-DL-10/KI-CL-12/KI-TR-10 files are the audited final package, and the KI-W4 decomposition now requires its parent review record.
old_revision: A5 state 100 / A3 pin 5c42924c8ea6ad1ca43a00feff2b636d83bcd029b7b8a4eeb6777ac60a7f5ec6 / A4 pin 8dce27da58ace35c605ee1f9d0b4ddc8a1e9358a282ec5bf8d7b461729eb999b / A8 pin (EV-KI-A-038) 0efb291ee92816422f3bf233a0011c66565b61c1b306c2f3b07a7a66da2d042a
new_revision: A5 state 101 / A3 c2dc635e5aa58f88c1ec465154663d314af68570fd4cbfdfca7b51c393c6f70f (KI-DL-10) / A4 40f705a423da88b952af4e529566b5a5374d4c7c1d7a0a589642d5906f0744ee (KI-CL-12) / A8 observed e9dc40a22e8b45c44c1c50adbdcabc65bc0c8f6efe6f5d4c7b0402995e31e3d4 (KI-TR-10)
changed_requirements: []
changed_decisions: []
affected_windows: [KI-W4 decomposition parent-accepted; KI-W4-S001..S010 + I001 leaves may begin sequentially; KI-W5 remains blocked]
invalidated_evidence: [A5 state 100 A3/A4 pin values and the EV-KI-A-038 A3/A4/A8 pin values only — metadata corrections; no artifact content, task, scenario, or execution evidence is invalidated]
compatibility_or_migration_effect: none — no A1/A3/A4/A8 content changed; the pins now equal the observed authenticated bytes.
authorization_effect: A5 state 101 keeps assignment ASG-KI-W4-WA-01, its write/action/prohibition scope, stop_after KI-W4, and may_start_successor false unchanged; it records current_status DECOMPOSITION_APPROVED. The window agent may set S2 to READY and assign the first one-file leaf.
resumption_state: The KI-W4 window agent sets S2 decomposition_status READY, assigns KI-W4-S001 through KI-W4-S010 strictly sequentially with per-leaf review, executes I001 gates V1-V4 exactly once each, appends the Section 12.5 consolidated handoff, and stops at READY_FOR_PARENT_REVIEW. Only parent acceptance may assign KI-W5.
```

```yaml
change_id: CHG-KI-018
timestamp: 2026-08-18T23:58:40+05:30
trigger_evidence: [EV-KI-W4-I01, EV-KI-A-040]
reason: The KI-W4 window agent completed all ten file leaves plus corrections KI-W4-C001/C002 and integration assessment I001 with gates V1-V4 and V6 PASS; the parent independently reran V2/V3/V4/V6 on the frozen tree, inspected the full diff and critical source paths, audited both corrections, and accepted the window. A4 KI-W4 boxes are checked with evidence citations.
old_revision: A4 KI-CL-12 / A5 state 101 (DECOMPOSITION_APPROVED, assignment ASG-KI-W4-WA-01) / backend accepted baseline d98ad53c
new_revision: A4 KI-CL-13 (KI-W4 boxes checked; no specification text changed) / A5 state 102 accepted unassigned / accepted backend fac5bb0f0a4e9c04873c9d338794762d44e35f7f
changed_requirements: []
changed_decisions: []
affected_windows: [KI-W4 accepted; KI-W5 becomes next assignable but remains blocked pending a separate requester-directed assignment CAS]
invalidated_evidence: []
compatibility_or_migration_effect: none — no A1/A3 content changed; A4 changes are completion box-checking plus the revision marker only.
authorization_effect: A5 state 102 ends ASG-KI-W4-WA-01 (window complete), sets accepted_through KI-W4, next_window KI-W5, and authorizes no window, file, provider, AWS, production, commit, or successor action. The three KI-W4 subordinate artifacts become historical records.
resumption_state: Unassigned. A future requester-directed parent assignment may name the KI-W5 window agent (frontend dashboard) from A4 KI-W5 at revision KI-CL-13; until then all work stops.
```

```yaml
change_id: CHG-KI-019
timestamp: 2026-08-19T11:31:00+05:30
trigger_evidence: [EV-KI-A-040, EV-KI-A-041]
reason: KI-W4 is parent-accepted (A5 state 102, accepted backend fac5bb0f) and the requester directed assignment of the KI-W5 window agent. The prior parent's 99->100 CAS development showed two metadata defects (stale A3/A4 pins transcribed from EV-KI-A-038 instead of recomputed at CAS time; missing A7/A6 transition records); this transition recomputes every pin from disk and records the assignment in both ledgers.
old_revision: A5 state 102 (ACCEPTED_UNASSIGNED, accepted_through KI-W4) / A4 KI-CL-13 c15b7a5989ecfa22db0bfc3ce6d161269895a8a9f04bc713d659b1690f656f2d / frontend clean 0dfa1acac50fac3a86d02ec674c6d2bab645832d
new_revision: A5 state 103 (READY, assignment ASG-KI-W5-WA-01 to KI-W5-WINDOW-AGENT) / pins A1 8b17f85c..., A3 c2dc635e... (KI-DL-10), A4 c15b7a59... (KI-CL-13), standards 3b7a4fd2.../1766f910... / delegable 27-file set digest a04dce13038a3d180ddab0c8412890af065e3f5ab5019540c87a5664485320e6
changed_requirements: []
changed_decisions: []
affected_windows: [KI-W5 assigned and READY; decomposition review by the parent required before the first leaf; KI-W6 remains blocked]
invalidated_evidence: []
compatibility_or_migration_effect: none — no A1/A3/A4 content changed; the 27-file delegable set and its digest are mechanical derivations from the A4 KI-W5 authorized_write_scope.
authorization_effect: A5 state 103 authorizes only the KI-W5 window agent; window-agent writes are limited to the three KEYWORD_INTELLIGENCE_KI_W5_SUBWINDOW_* coordination artifacts; implementation happens exclusively through strictly sequential single-file leaves over the 27 listed frontend paths under the subwindow standard, with parent decomposition approval before the first leaf. Backend edits, provider calls, database/AWS operations, iframe, runtime CDN, unrelated frontend file edits, package/lock edits, schema/migration edits, worker/recovery/dispatcher edits, commits/pushes, and KI-W6 work remain prohibited.
resumption_state: The requester directs the KI-W5 window agent to begin: author S1/S2/S3, decompose into sequential one-file leaves over the exact 27-path set (digest a04dce13...), stop at AWAITING_PARENT_DECOMPOSITION_REVIEW; the parent reviews and approves before any leaf is assigned. Gates KI-W5-V1-V4 run exactly once at the final integration assessment on the frozen tree; the window agent then returns the consolidated Section 12.5 handoff and stops at READY_FOR_PARENT_REVIEW.
```

```yaml
change_id: CHG-KI-020
timestamp: 2026-08-19T11:47:20+05:30
trigger_evidence: [EV-KI-A-041, EV-KI-A-042]
reason: The requester required the KI-W5 assignment CAS to conform to PROJECT_AGNOSTIC_DECISION_COMPLETE_CHECKLIST_AUTHORING_STANDARD.md so the workflow stays consistent with the rest of the checklist. Review found the state-103 CAS imposed a KI-W4-style delegation orchestration although A4 KI-W5 locks assigned_agent_policy one_window, added a non-schema A5 field, paraphrased A4's verbatim action/prohibition lists against Section 2.5, and routed the handoff through sub-window-standard vocabulary instead of the native Section 10.3 agent self-CAS to AWAITING_REVIEW.
old_revision: A5 state 103 (ASG-KI-W5-WA-01, delegating window-agent pattern; never started; no KI-W5 artifacts exist; both repositories clean)
new_revision: A5 state 104 (ASG-KI-W5-01 to KI-W5-AGENT, single implementation agent; Section 2.5 exact field schema; A4 KI-W5 verbatim 27-path write scope, actions, prohibitions; Section 10 execution semantics; agent self-CAS to AWAITING_REVIEW at handoff)
changed_requirements: []
changed_decisions: []
affected_windows: [KI-W5 assignment revised before any execution; KI-W6 remains blocked]
invalidated_evidence: [EV-KI-A-041 authorization_effect and resumption_state paragraphs describing the withdrawn delegation assignment only; its stale-pin analysis and pin recomputation facts remain historical observations]
compatibility_or_migration_effect: none — no A1/A3/A4 content changed; no agent accepted or began the withdrawn assignment; no code, test, or artifact was invalidated.
authorization_effect: A5 state 104 authorizes exactly one implementation agent (KI-W5-AGENT) to execute the whole KI-W5 window under Section 10 semantics: A4 verbatim write scope (27 paths), authorized actions [local_source_edits, local_frontend_check, local_next_server, local_Chrome_CDP, evidence_updates], prohibitions [backend_edits, provider_calls, database_or_AWS_operations, iframe, runtime_CDN, unrelated_frontend_file_edits, commits]; may_start_successor false; stop_after KI-W5; next_window KI-W6; accepted_through KI-W4.
resumption_state: The requester directs KI-W5-AGENT to begin: complete KI-W5-P1-P4 preflight with evidence, execute KI-W5-T1-T3 in order, run KI-W5-V1-V4 exactly as A4 specifies, complete KI-W5-H1-H6 including the self-CAS of current_status to AWAITING_REVIEW, and stop. The parent then performs the Section 10.4 independent verification and, on pass, creates the KI-W6 assignment.
```

```yaml
change_id: CHG-KI-021
timestamp: 2026-08-19T11:55:10+05:30
trigger_evidence: [EV-KI-A-042, EV-KI-A-043]
reason: The requester directed that KI-W5 execute through a window agent that decomposes the window into sequential single-file leaves per PROJECT_AGNOSTIC_WINDOW_AGENT_SUBWINDOW_AUTHORING_STANDARD.md, matching the accepted KI-W4 workflow. State 104's direct-agent assignment is therefore withdrawn unused; because that state had correctly objected to delegation being invented only in A5, the durable fix is to amend the A4 KI-W5 header to carry the delegation policy explicitly before assigning.
old_revision: A4 KI-CL-13 c15b7a5989ecfa22db0bfc3ce6d161269895a8a9f04bc713d659b1690f656f2d / A5 state 104 (ASG-KI-W5-01 to KI-W5-AGENT, direct execution; never begun)
new_revision: A4 KI-CL-14 324667cbe0d467ecf4f913c93e91087e75192bd463e0c05b033ee418754a362e (KI-W5 header gains delegation_policy, window_agent_identity KI-W5-WINDOW-AGENT, coordination write scope, delegable_implementation_file_set = the prior 27 paths verbatim with digest a04dce13038a3d180ddab0c8412890af065e3f5ab5019540c87a5664485320e6, delegation action/prohibition lists, and KI-W5-P5/P6 decomposition-review boxes) / A5 state 105 (ASG-KI-W5-WA-02 to KI-W5-WINDOW-AGENT)
changed_requirements: []
changed_decisions: []
affected_windows: [KI-W5 reassigned to the window-agent delegation pattern; KI-W6 remains blocked]
invalidated_evidence: [EV-KI-A-042 revised-assignment authorization_effect and resumption_state paragraphs describing ASG-KI-W5-01 only; its A5-schema conformance analysis and the state-103 defect findings remain historical]
compatibility_or_migration_effect: no requirement, decision, task, gate, scenario, or test text changed; the 27 implementation paths are byte-identical to the prior authorized_write_scope, only relocated into delegable_implementation_file_set.
authorization_effect: A5 state 105 authorizes only KI-W5-WINDOW-AGENT; window-agent writes are limited to the three KEYWORD_INTELLIGENCE_KI_W5_SUBWINDOW_* coordination artifacts; implementation happens exclusively through strictly sequential single-file leaves over the 27 listed paths; parent decomposition approval is required before the first leaf; window-agent implementation-file edits, parallel leaves, direct parent-leaf communication, backend edits, provider calls, database/AWS operations, iframe, runtime CDN, unrelated frontend file edits, package/lock edits, commits, and KI-W6 work are prohibited.
resumption_state: The requester directs KI-W5-WINDOW-AGENT to begin: author S1/S2/S3, decompose into sequential one-file leaves over the exact 27-path set (digest a04dce13...), stop at AWAITING_PARENT_DECOMPOSITION_REVIEW; the parent reviews and approves before any leaf is assigned. Final gates KI-W5-V1-V4 run exactly once at the integration assessment on the frozen tree; the window agent then returns the consolidated handoff and stops at READY_FOR_PARENT_REVIEW for Section 10.4-style parent verification.
```

```yaml
change_id: CHG-KI-022
timestamp: 2026-08-19T12:41:30+05:30
trigger_evidence: [EV-KI-W5-S01, EV-KI-W5-S03, EV-KI-A-044]
reason: The KI-W5 window agent completed the 27-leaf + I001 decomposition (43-case set, 12 controls, 44/44 readiness) and stopped at AWAITING_PARENT_DECOMPOSITION_REVIEW; the parent independently verified all digests, mappings, boundaries, and the four recorded interpretations and accepts the decomposition. One metadata defect was found and corrected by note: the starting-inventory digest used non-authoritative locale collation.
old_revision: A5 state 105 (assignment ASG-KI-W5-WA-02, status READY, decomposition pending)
new_revision: A5 state 106 (assignment ASG-KI-W5-WA-02, status DECOMPOSITION_APPROVED; A1/A3/A4 pins unchanged)
changed_requirements: []
changed_decisions: []
affected_windows: [KI-W5 decomposition parent-accepted; KI-W5-S001..S027 + I001 leaves may begin sequentially; KI-W6 remains blocked]
invalidated_evidence: []
compatibility_or_migration_effect: none — no A1/A3/A4 content changed; the authoritative byte-order value d1a974b3... of the unchanged 36-line inventory is recorded in EV-KI-A-044.
authorization_effect: A5 state 106 keeps ASG-KI-W5-WA-02, its write/action/prohibition scope, stop_after KI-W5, and may_start_successor false unchanged; the window agent may convert S2 to READY (appending the required serialization note) and assign the first one-file leaf.
resumption_state: The KI-W5 window agent appends the S3 serialization-correction note, sets S2 decomposition_status READY, assigns KI-W5-S001 through S027 strictly sequentially with per-leaf review, executes I001 gates KI-W5-V1-V4 plus the I001-M merge exactly once each on the frozen tree, appends the Section 12.5 consolidated handoff, and stops at READY_FOR_PARENT_REVIEW. Only parent acceptance may assign KI-W6.
```

```yaml
change_id: CHG-KI-023
timestamp: 2026-08-20T05:15:00+05:30
trigger_evidence: [EV-KI-W5-S36, EV-KI-A-046]
reason: The KI-W5 window agent completed all 27 file leaves, three single-file corrections, and the I001 integration assessment (gates KI-W5-V1-V4 and KI-W5-I001-M all PASS on frozen final inputs) and stopped at READY_FOR_PARENT_REVIEW; the parent independently verified every digest, set digest, gate artifact, certificate, and residual item and accepts the window.
old_revision: A5 state 106 (assignment ASG-KI-W5-WA-02, status DECOMPOSITION_APPROVED, accepted_through KI-W4)
new_revision: A5 state 107 (assignment ASG-KI-W5-WA-02 CLOSED/ACCEPTED, status KI-W5_ACCEPTED, accepted_through KI-W5; A1/A3/A4 pins unchanged)
changed_requirements: []
changed_decisions: []
affected_windows: [KI-W5 accepted and closed; KI-W6 (depends_on KI-W5) becomes assignable upon requester direction; STOP_LOCAL remains the terminal successor of KI-W6]
invalidated_evidence: []
compatibility_or_migration_effect: none — no A1/A3/A4 content changed; the accepted frontend surface is the 27-file set at digests recorded in the S2 registry (C001/C002/C003 supersessions included), committed by the requester through c85f93b.
authorization_effect: ASG-KI-W5-WA-02 is fulfilled and closed; no window agent holds a current assignment. KI-W6 work is NOT authorized by this change; it requires a new parent assignment (with decomposition passing the sub-window standard) once the requester directs it.
resumption_state: No active window. The requester decides whether to proceed with KI-W6 (integrated local proof and obsolete-runtime exclusion; two-file write scope; successor STOP_LOCAL) or pause. Both repositories are clean; the 36-line owner-controlled root relocation state is preserved.
```

```yaml
change_id: CHG-KI-024
timestamp: 2026-08-20T09:16:30+05:30
trigger_evidence: [EV-KI-A-046, EV-KI-A-047]
reason: The requester directed the KI-W6 window to begin under the current standards; the parent verified the W1-W5 acceptance chain, remaining-scenario closure (only SCN-KI-018 remains), and on-disk prerequisites, and assigns ASG-KI-W6-WA-01.
old_revision: A5 state 107 (no active window; KI-W5 accepted; KI-W6 pending requester direction)
new_revision: A5 state 108 (assignment ASG-KI-W6-WA-01 to KI-W6-WINDOW-AGENT, status READY, stop_after KI-W6; A1/A3/A4 pins unchanged)
changed_requirements: []
changed_decisions: []
affected_windows: [KI-W6 active; KI-W7 remains blocked pending KI-W6 acceptance plus explicit infrastructure-source approval]
invalidated_evidence: []
compatibility_or_migration_effect: none — no A1/A3/A4 content changed.
authorization_effect: KI-W6-WINDOW-AGENT may author S1/S2/S3, delegate exactly one listed file per sequential leaf, review leaves, execute frozen gates KI-W6-V1-V4 plus the I001-M merge once each on frozen final inputs, run one-file corrective leaves inside the same two-file set, and stop at READY_FOR_PARENT_REVIEW. No commits (requester-only), no provider/AWS/production action, no KI-W7 work, no standalone-repository edits.
resumption_state: Window agent authors the decomposition; parent decomposition review follows before any leaf starts; after acceptance the requester decides on KI-W7.
```

```yaml
change_id: CHG-KI-025
timestamp: 2026-08-20T10:10:00+05:30
trigger_evidence: [KI-PR-W4-W5-01, SRC-KI-034, SRC-KI-035, SRC-KI-036, SRC-KI-037, EV-KI-A-048]
reason: Independent code review reproduced nine functional and enforcement gaps across the accepted W4 backend and W5 frontend. Those gaps prevent KI-W6 from truthfully proving the intended integrated workflow. The requester directed one corrective window covering both accepted windows before W6.
old_revision: A2 KI-DD-3 / A3 KI-DL-10 c2dc635e5aa58f88c1ec465154663d314af68570fd4cbfdfca7b51c393c6f70f / A4 KI-CL-14 324667cbe0d467ecf4f913c93e91087e75192bd463e0c05b033ee418754a362e / A8 KI-TR-10 / A5 state 108 assigning unexecuted KI-W6 decomposition
new_revision: A2 KI-DD-4 301211500c5e243d6cdb0cefd758e2fbd560174dab148e7e75880dd5c7560ff6 / A3 KI-DL-11 c364f509aa60cbfaee50b42094f681d1c6f10d0be3540651dfd2552a9f2a205e / A4 KI-CL-15 d5b4ef6cc34bc666cad360943a3a50ce888e444781c2bc11fcc745c1873d6798 / A8 KI-TR-11 b4d21598cb1c7dafe7f7304a7a31c0efd655b846af21d6583464d3297d356ce4 / A5 state 109 unassigned with KI-R5 next
changed_requirements: []
changed_decisions: [DEC-KI-034 strict numeric/minimal wire and bounded selection, DEC-KI-035 saved-draft/finalization/idempotency lifecycle, DEC-KI-036 duplicate/filter/CSV semantics, DEC-KI-037 enforcement/substitute/gate/invalidation rules]
affected_windows: [KI-W4 and KI-W5 acceptance history retained but their nine affected boundary assertions are superseded pending KI-R5, KI-R5 newly authored and parent-reserved, KI-W6 blocked until KI-R5 acceptance and fresh decomposition]
invalidated_evidence: [EV-KI-A-046 claims that W5 plus W4 are integrated-boundary complete only; affected W4/W5 numeric wire, mutation media type, browser manual identity, full-snapshot capacity, unsaved finalization, ambiguous handoff retry, frontend filter parity, duplicate-selection acceptance, CSV-safety and W4-D04 weak concurrent-success assertions; EV-KI-A-047 authorization/readiness and the state-108 KI-W6 S1/S2/S3 decomposition. Unrelated observed hashes, commands, passing tests, UI behavior, W4/W5 implementation evidence and accepted case assertions remain historical and valid.]
compatibility_or_migration_effect: No A1 product requirement, Prisma schema/migration, package, provider payload/economics, AWS topology or deployed resource changes. KI-R5 replaces one internal browser-to-owner selection input with PAY-KI-008 while preserving the full owner response and durable SelectionItem shape; corrects frontend/backend behavior only inside the exact 18-file set.
authorization_effect: A5 state 109 terminates ASG-KI-W6-WA-01 before any leaf execution, authorizes no current window/agent/file/action, sets accepted_through KI-W5 and next_window KI-R5, and keeps may_start_successor false. This authoring change does not assign or decompose KI-R5 and does not permit KI-W6 work.
resumption_state: On separate requester direction, the parent may CAS A5 once to assign KI-R5-WINDOW-AGENT only its three coordination artifacts. The window agent authors a fresh exact 18-file sequential one-file decomposition under the sub-window standard and stops for parent decomposition review; after approved leaf execution and parent acceptance, KI-W6 must be decomposed afresh.
```

```yaml
change_id: CHG-KI-026
timestamp: 2026-08-20T10:18:00+05:30
trigger_evidence: [EV-KI-A-048, EV-KI-A-049, EV-KI-A-050]
reason: Final parent mechanical review found that DEC-KI-034 through DEC-KI-037 carried four stale implementing-task references and A4 named twelve controls without fixing each control's safe mutation, unchanged oracle and exact failure. Those authoring defects would leave the future window agent implementation choices, so they were corrected before assignment.
old_revision: A3 KI-DL-11 c364f509aa60cbfaee50b42094f681d1c6f10d0be3540651dfd2552a9f2a205e / A4 KI-CL-15 d5b4ef6cc34bc666cad360943a3a50ce888e444781c2bc11fcc745c1873d6798 / A5 state 109 unassigned
new_revision: A3 KI-DL-12 af32db3e74023be2e0e320da151419297e9d8db089752fafea1f58d3031e8457 / A4 KI-CL-16 d8bd3f20f93047722a14a80ee55d491b72a895e629cfd9f23791ff329c4e4dfc / A5 state 110 unassigned
changed_requirements: []
changed_decisions: [DEC-KI-034 task trace corrected to T1/T4/T5, DEC-KI-035 corrected to T2/T4/T5, DEC-KI-036 corrected to T1/T3/T4/T5, DEC-KI-037 corrected to enforcement owner T5]
affected_windows: [KI-R5 authoring package only; KI-W4/W5 historical acceptance and KI-W6 invalidation unchanged]
invalidated_evidence: [EV-KI-A-048 AUTHORING-READY certificate revision values and its assertion that naming NC-01 through NC-12 alone was complete; EV-KI-A-049 remains the authoritative starting-hash correction]
compatibility_or_migration_effect: none — no product/runtime/schema/package/provider/AWS decision or implementation path changed; the new literal control table removes implementation discretion and strengthens pre-assignment enforcement.
authorization_effect: none beyond advancing the unassigned A5 pin to state 110; no agent, window, file or action is authorized.
resumption_state: Use only the superseding EV-KI-A-050 AUTHORING-READY certificate. On requester direction the parent may assign KI-R5-WINDOW-AGENT to S1/S2/S3; all other KI-R5 and KI-W6 work remains prohibited until that CAS.
```

```yaml
change_id: CHG-KI-027
timestamp: 2026-08-20T10:24:00+05:30
trigger_evidence: [EV-KI-A-050, EV-KI-A-051]
reason: The final accepted-evidence audit found that “affected W4/W5 assertions” was not a literal executable set. KI-R5 now freezes the only 18 mutable prior oracles, the 15-member browser rerun set, the stable-registration rule and the immutable remainder. The NC-12 duplicate and unexpected-ID mutations are also explicitly separate.
old_revision: A3 KI-DL-12 af32db3e74023be2e0e320da151419297e9d8db089752fafea1f58d3031e8457 / A4 KI-CL-16 d8bd3f20f93047722a14a80ee55d491b72a895e629cfd9f23791ff329c4e4dfc / A5 state 110 unassigned
new_revision: A3 KI-DL-13 e8ed580dd08b77540158340c47fae84c5d56b18cc7aba3149ccc2ab568493f5d / A4 KI-CL-17 4f52bf764525927fd7b68c0795aec5cbbd15f1a8b9b73778d446cfd87e2b94b8 / A5 state 111 unassigned
changed_requirements: []
changed_decisions: [DEC-KI-037 exact accepted-assertion supersession and browser-rerun sets]
affected_windows: [KI-R5 authoring package only; W4/W5 history is now invalidated at literal-oracle granularity; KI-W6 remains blocked]
invalidated_evidence: [EV-KI-A-050 AUTHORING-READY revision values only; its task/control completeness observations remain valid]
compatibility_or_migration_effect: none — no implementation or external contract changed.
authorization_effect: none beyond advancing the unassigned A5 pins; no agent/window/file/action is authorized.
resumption_state: Use EV-KI-A-051 as the current AUTHORING-READY certificate. A requester-directed parent assignment is still required before KI-R5 decomposition.
```

```yaml
change_id: CHG-KI-028
timestamp: 2026-08-20T13:10:00+05:30
trigger_evidence: [EV-KI-A-052, EV-KI-R5-S06, EV-KI-R5-S17, EV-KI-A-053]
reason: After parent approval of KI-R5 S1 revision 6ff7830a..., the window agent appended only the approval record to S1 §11.3, producing live revision f38d0bfd..., but left the subordinate revision pin at 6ff7830a.... The mismatch was detected before S011 and requires explicit revision reconciliation rather than guessed continuation.
old_revision: A5 state 113; KI-R5 S1 approved/pinned 6ff7830adc72874a3c30a2000ec96f32a668fba230fe652260d83ad2cab9500f; S2 state 14 BLOCKED before S011
new_revision: A5 state 114; KI-R5 S1 reapproved/pin target f38d0bfd40dea50a11fb7473c0013d224f5b3e519c54d964553fc227c79b7319; window-agent S2/S3 reconciliation authorized
changed_requirements: []
changed_decisions: []
affected_windows: [KI-R5 coordination revision only; S001 through S010 remain accepted; S011 through S018 and I001 remain governed by unchanged task content; KI-W6 remains blocked]
invalidated_evidence: []
compatibility_or_migration_effect: none — mechanical deletion of the appended approval record plus one separator reproduces the approved 6ff7830a... bytes exactly; no implementation, interface, behavior, payload, schema, package, coverage, control, or gate changed.
authorization_effect: KI-R5-WINDOW-AGENT may update only S2/S3 to replace the subordinate decomposition pin with f38d0bfd..., cite EV-KI-A-053/CHG-KI-028, clear the S1-revision blocker, preserve accepted S001-S010 without hash-only reruns, and resume at unexecuted S011. Further S1 mutation, KI-W6, KI-W7, provider, AWS, production-database, commit, and push actions remain prohibited.
resumption_state: A5 state 114 IN_PROGRESS under existing ASG-KI-R5-WA-01. Window agent performs the S2/S3 CAS reconciliation, verifies live S1 still hashes f38d0bfd..., confirms S011 remains unexecuted, then assigns S011 and continues the already-approved sequential DAG through I001 and parent handoff.
```

```yaml
change_id: CHG-KI-029
timestamp: 2026-08-20T13:45:00+05:30
trigger_evidence: [EV-KI-R5-S16, EV-KI-R5-S20, EV-KI-R5-S21, EV-KI-A-054]
reason: Accepted S010 used view.selection.items although the frozen ResearchView contract makes view.selection the SelectionItem[]; S013 reproduced the resulting production TypeError and stopped without editing.
old_revision: A5 state 114; S1 f38d0bfd40dea50a11fb7473c0013d224f5b3e519c54d964553fc227c79b7319 with S1 section 11.1 empty; S2 state 18 BLOCKED before S013
new_revision: A5 state 115; one append-only KI-R5-C001 amendment authorized for S1 section 11.1; C001 execution and S013 resumption conditionally authorized
changed_requirements: []
changed_decisions: []
affected_windows: [KI-R5 only; corrective file frontend/lib/keyword-intelligence-view-model.ts; S013 remains next initial leaf after correction; KI-W6 remains blocked]
invalidated_evidence: [On the C001 implementation edit, EV-KI-R5-S16 resulting-file digest and canFinalizeSelection proof only are superseded; its unrelated filter/projection evidence remains valid. EV-KI-R5-S20 requires recorded dependency revalidation but no unchanged-file implementation rerun.]
compatibility_or_migration_effect: none — the exact one-expression correction conforms the implementation to the already-frozen ResearchView.selection array contract; no external shape, schema, package, architecture, or ownership boundary changes.
authorization_effect: KI-R5-WINDOW-AGENT may append one complete KI-R5-C001 block to S1 section 11.1, record the required certificate in S3/state in S2, assign one leaf owning only frontend/lib/keyword-intelligence-view-model.ts, apply only the exact view.selection.items to view.selection replacement, review the exact diff and frozen local oracles, record supersession/revalidation, and resume S013. No other S1 or implementation change is authorized.
resumption_state: A5 state 115 IN_PROGRESS under ASG-KI-R5-WA-01. C001 must be accepted and EV-KI-R5-S20 dependency revalidated before S013 may be reassigned; then the existing sequential DAG continues through I001 and parent handoff.
```

```yaml
change_id: CHG-KI-030
timestamp: 2026-08-20T13:52:00+05:30
trigger_evidence: [EV-KI-R5-S21, EV-KI-A-054, EV-KI-R5-S22, EV-KI-A-055]
reason: The authored C001 block and readiness certificate incorrectly made paused, unexecuted S013 a predecessor even though S013 cannot resume until C001 is accepted, creating a dependency cycle.
old_revision: A5 state 115; S1 0f3ef85771392d164ad1e44f044c1b71659b84d44176b47aed58c4afaca35657; C001 task and certificate predecessors both [KI-R5-S013]; S2 state 19 claimed READY
new_revision: A5 state 116; exact two-field S1 revision authorized so both C001 predecessor lists become [KI-R5-S010]; corrected C001 may execute without another parent review after mechanical verification
changed_requirements: []
changed_decisions: []
affected_windows: [KI-R5 C001 coordination only; S010 remains the accepted corrected predecessor; S013 remains the post-C001 successor; KI-W6 remains blocked]
invalidated_evidence: [EV-KI-R5-S22 CORRECTIVE-SUBWINDOW-READY claim and S1 revision pin only; its diagnosis, scope, transformation, starting file digest, and zero-implementation statement remain valid]
compatibility_or_migration_effect: none — dependency metadata correction only; no implementation or external contract changes.
authorization_effect: KI-R5-WINDOW-AGENT may replace exactly the two C001 predecessors [KI-R5-S013] fields with [KI-R5-S010], rehash/pin S1 in S2, append superseding readiness evidence in S3, and dispatch C001 without another parent review only if the two-field diff and accepted-S010/unexecuted-S013 state are proven. All EV-KI-A-054 implementation limits remain binding.
resumption_state: A5 state 116 IN_PROGRESS under ASG-KI-R5-WA-01. Correct C001 dependency metadata, execute/review C001, revalidate S012, then resume S013 and the approved DAG through I001; stop for parent handoff and do not begin KI-W6.
```

```yaml
change_id: CHG-KI-031
timestamp: 2026-08-20T14:45:00+05:30
trigger_evidence: [EV-KI-R5-S26, EV-KI-A-056]
reason: S014 assigned real dashboard finalization lifecycle cases to a plain Node test that implemented a substitute handoff state machine instead of activating the production components and request boundary; the resulting passing tests are not fidelity-valid.
old_revision: A5 state 116; S1 0743b17406ecc1643510a1f36a19c9c0a4ba20acc868ff12788896cc4b5782da; S014 owns R5-FIN-01..06 and NC-05/06; five non-conformance certificates expected; S2 state 23 BLOCKED
new_revision: A5 state 117 CORRECTIVE_AUTHORING_AUTHORIZED; C002 authoring and exact S014-to-S015 case/control ownership reallocation authorized; revised S1 must return for parent decomposition review before execution
changed_requirements: []
changed_decisions: []
affected_windows: [KI-R5 only; C002 corrects rejected S014; unexecuted S015 S016 S018 and I001 gate instructions are revised; S017 and all 34 manifest IDs/digests remain unchanged; KI-W6 remains blocked]
invalidated_evidence: [EV-KI-R5-S26 local passing result cannot support R5-FIN-01..06 or NC-05/06 activation and is superseded only after C002; no accepted S014 evidence or final gate exists]
compatibility_or_migration_effect: none — testing ownership and evidence fidelity only; no product behavior, external contract, schema, package, architecture, case membership, or manifest digest changes.
authorization_effect: KI-R5-WINDOW-AGENT may edit only S1/S2/S3 to author one-file C002, move R5-FIN-01..06 and NC-05/06 ownership to the unexecuted S015 emitted-browser harness, remove the components execution registry, revise S016/S018/I001 and V2/V4/V6 certificate expectations from five to four non-conformance certificates, mechanically prove S017 and all manifest IDs/digests unchanged, and return for parent decomposition review. No leaf execution is authorized.
resumption_state: A5 state 117 under ASG-KI-R5-WA-01. Stop at AWAITING_PARENT_DECOMPOSITION_REVIEW after the complete amendment; parent approval is required before C002 dispatch. KI-W6 and KI-W7 remain prohibited.
```

```yaml
change_id: CHG-KI-032
timestamp: 2026-08-20T15:00:00+05:30
trigger_evidence: [EV-KI-R5-S26, EV-KI-A-056, EV-KI-R5-S27, EV-KI-A-057]
reason: Parent review accepted the S014-to-S015 realignment structure but found five exact authoring defects: omitted removal of the rejected-model-only import, five-versus-six browser-oracle ambiguity, dual-owner shorthand, incomplete S018 read authority, and nonconforming readiness/invalidation fields.
old_revision: A5 state 117; S1 80c81cf2e71e3bff61a88dafdd71d8d579bb93e13e56b759ac663de60387d2e5; S2 state 24 AWAITING_PARENT_DECOMPOSITION_REVIEW
new_revision: A5 state 118 CORRECTIVE_REVISION_REQUIRED; exact S1/S2/S3 corrections authorized; decomposition remains unapproved
changed_requirements: []
changed_decisions: []
affected_windows: [KI-R5 decomposition only; C002 S015 S016 S018 I001 and their evidence wording; S017 and all product code/case IDs/digests remain unchanged; KI-W6 remains blocked]
invalidated_evidence: [EV-KI-R5-S27 readiness certificate only; its root-cause proof, no-execution claim, seven-ID ownership decision, four-certificate arithmetic, and S017 preservation proof remain valid]
compatibility_or_migration_effect: none — authoring precision and read authority only; no product behavior, test execution, external contract, schema, package, manifest, or digest change.
authorization_effect: KI-R5-WINDOW-AGENT may edit only S1/S2/S3 for the five literal corrections in EV-KI-A-057 and return for parent review. No corrective or initial leaf may be assigned or executed.
resumption_state: A5 state 118 under ASG-KI-R5-WA-01. Keep S2 at AWAITING_PARENT_DECOMPOSITION_REVIEW, rehash and pin the corrected S1, append S3 superseding readiness evidence, then stop for parent review; do not begin C002, S015, KI-W6, or KI-W7.
```

```yaml
change_id: CHG-KI-033
timestamp: 2026-08-20T15:08:00+05:30
trigger_evidence: [EV-KI-A-057, EV-KI-R5-S28, EV-KI-R5-S29, EV-KI-A-058]
reason: The corrected C002 block still hardcodes authoring A5 state 117 as an execution-time P1 match, but any parent approval necessarily advances A5, making the otherwise-correct leaf fail preflight deterministically.
old_revision: A5 state 118; S1 4cf412ce19daeb3c043d4d872223c8ad74a73587eb35f84d56a63413f7f53b00; C002 P1 requires parent state 117
new_revision: A5 state 119 CORRECTIVE_REVISION_REQUIRED; exact one-line live-dispatch P1 replacement authorized; decomposition remains unapproved
changed_requirements: []
changed_decisions: []
affected_windows: [KI-R5 C002 preflight wording only; every allocation case control certificate gate and S017 literal remains unchanged; KI-W6 remains blocked]
invalidated_evidence: [EV-KI-R5-S28 readiness claim only; its five correction proofs and EV-KI-R5-S29 preservation proof remain valid]
compatibility_or_migration_effect: none — coordination preflight wording only.
authorization_effect: KI-R5-WINDOW-AGENT may change only C002 completion item P1 to the exact live-assignment/live-approved-revision dispatch oracle in EV-KI-A-058, update S2/S3, and return for parent review. No leaf execution is authorized.
resumption_state: A5 state 119 under ASG-KI-R5-WA-01. Keep S2 AWAITING_PARENT_DECOMPOSITION_REVIEW, apply the one-line S1 correction with inverse proof, rehash/pin, append S3 evidence, and stop; do not begin C002, S015, KI-W6, or KI-W7.
```

```yaml
change_id: CHG-KI-034
timestamp: 2026-08-20T15:12:00+05:30
trigger_evidence: [EV-KI-A-058, EV-KI-R5-S30, EV-KI-A-059]
reason: The sole live-state P1 contradiction was corrected with an inverse one-line proof; the complete C002/browser realignment decomposition now satisfies parent decision- and enforcement-completeness review.
old_revision: A5 state 119; S1 4cf412ce19daeb3c043d4d872223c8ad74a73587eb35f84d56a63413f7f53b00 returned for one-line revision; S2 state 25 awaiting review
new_revision: A5 state 120 DECOMPOSITION_APPROVED; S1 65b91920edd84720f469d1bbbd57b0837fc0b1bfb11621f4a0f13f9f4ba4ef61 approved; S2 state 26 awaiting conversion to READY by the window agent
changed_requirements: []
changed_decisions: []
affected_windows: [KI-R5 C002 and revised S015 S016 S018 I001 execution sequence; S017 and all 34 IDs/digests unchanged; KI-W6 remains blocked]
invalidated_evidence: []
compatibility_or_migration_effect: none — approval of testing/evidence allocation only; no product behavior, external contract, schema, package, manifest, or digest change.
authorization_effect: KI-R5-WINDOW-AGENT may record approval in S2/S3, dispatch and independently review C002, then sequentially execute revised S015 through S018 and I001 under the approved single-file and frozen-gate rules. No KI-W6 work is authorized.
resumption_state: A5 state 120 DECOMPOSITION_APPROVED under ASG-KI-R5-WA-01. Window agent converts S2 to READY, assigns C002, and continues only through KI-R5 parent handoff; stop before KI-W6.
```

```yaml
change_id: CHG-KI-035
timestamp: 2026-08-20T15:14:43+05:30
trigger_evidence: [EV-KI-A-059, EV-KI-R5-S31, EV-KI-A-060]
reason: C002 copied C001's historical root change-set digest even though S1's authoritative 45-entry inventory and the live root status both equal c660d09a800e8a5fd446bd65039f55241d5d7bb4e4c7ef656fe4fc7dcc88417c; this stale literal made approved C002 fail P1 before dispatch.
old_revision: A5 state 120 DECOMPOSITION_APPROVED; S1 65b91920edd84720f469d1bbbd57b0837fc0b1bfb11621f4a0f13f9f4ba4ef61; C002 starting_repository_change_set_digest 02530e7cc6bba4e59291f1eba4cf5464b784bbabac4dfb2384c33fae90f54a74
new_revision: A5 state 121 DECOMPOSITION_APPROVED; exact C002-only digest substitution authorized; corrected S1 revision to be computed and pinned by the window agent
changed_requirements: []
changed_decisions: []
affected_windows: [KI-R5 C002 dispatch preflight only; all later approved KI-R5 leaves and KI-R5-I001 unchanged; KI-W6 remains blocked]
invalidated_evidence: [EV-KI-A-059 repository-digest subclaim only; its decision-completeness and enforcement-completeness approval remains valid]
compatibility_or_migration_effect: none — coordination digest correction only; no product code behavior interface allocation case control certificate gate or manifest change.
authorization_effect: KI-R5-WINDOW-AGENT may replace only C002's stale starting_repository_change_set_digest literal with c660d09a800e8a5fd446bd65039f55241d5d7bb4e4c7ef656fe4fc7dcc88417c, prove the single-literal S1 delta, repin S1 in S2/S3, rerun C002 P1, and on pass dispatch C002 immediately without another parent review.
resumption_state: A5 state 121 DECOMPOSITION_APPROVED under ASG-KI-R5-WA-01. Clear the EV-KI-R5-S31 blocker after the exact correction and successful preflight, then continue the already-approved sequence through KI-R5 handoff; stop before KI-W6.
```

```yaml
change_id: CHG-KI-036
timestamp: 2026-08-20T16:02:05+05:30
trigger_evidence: [EV-KI-R5-S34, EV-KI-A-061]
reason: S015 omitted the rendered Save selection action required to activate its FIN-04 PUT witness; the requester directly committed the mechanically determined four-line correction and directed that it be regularized without a new implementation leaf.
old_revision: A5 state 121 DECOMPOSITION_APPROVED; S2 state 30 PARENT_BLOCKED; rejected S015 commit d4763a771734dfe043d59e2a4ae5b0dc6e0371c9 and browser-harness digest ea7ab5ff8ac6368ff278520fa79876dcd30c8764fb3e8f6fb7a066cf3d95805d
new_revision: A5 state 122 DECOMPOSITION_APPROVED; requester-supplied review-only C003 authoring and review authorized for commit 4dd9b4f0357b7c118d6c8ea92af212c7ff0693ba and candidate digest 1c4cc5ae801f586398cf2e7a30c785f84868001d215fd85bd3d1bc0a920deb01
changed_requirements: []
changed_decisions: [C003 implementation is requester-supplied and already committed; the window agent performs documentation plus independent review only and must not dispatch an implementation leaf]
affected_windows: [KI-R5 C003 review and S015 corrected disposition; S016 S017 S018 I001 sequencing otherwise unchanged; KI-W6 remains blocked]
invalidated_evidence: [EV-KI-R5-S34 blocked disposition only; its defect diagnosis and rejected-S015 facts remain authoritative]
compatibility_or_migration_effect: none — the correction activates the already-required FIN-04 save path and changes no product interface architecture registry case control certificate or manifest.
authorization_effect: KI-R5-WINDOW-AGENT may append only the exact EV-KI-A-061 review-only C003 block to S1, pin it in S2/S3, review the existing requester commit without implementation edits or a leaf assignment, and on pass accept C003 and immediately resume at S016 without another parent review.
resumption_state: A5 state 122 DECOMPOSITION_APPROVED under ASG-KI-R5-WA-01. Review requester commit 4dd9b4f as C003, then continue the approved KI-R5 sequence through parent handoff; stop before KI-W6.
```

```yaml
change_id: CHG-KI-037
timestamp: 2026-08-20T16:28:38+05:30
trigger_evidence: [EV-KI-R5-S36, EV-KI-A-062]
reason: The inventory test's two W5-I02 fixtures retain the legacy string contract version, making its mandatory full-file pass incompatible with the accepted numeric-only S008 parser before S016's additive lint can execute.
old_revision: A5 state 122 DECOMPOSITION_APPROVED; S2 state 32 PARENT_BLOCKED; inventory test digest 67828152b71f9b05ec847d5fc0d3be238452d526aeffee8255e17b39a644f480 with two ki-research-v1 fixture literals
new_revision: A5 state 123 DECOMPOSITION_APPROVED; one-file two-literal C004 authoring dispatch review and fresh-baseline S016 resumption authorized
changed_requirements: []
changed_decisions: []
affected_windows: [KI-R5 C004 and S016 baseline only; S017 S018 I001 sequencing unchanged; KI-W6 remains blocked]
invalidated_evidence: [S016 state-31 dispatch baseline only; accepted S008 and C003 evidence remains valid]
compatibility_or_migration_effect: none — test fixtures are aligned to the already-accepted numeric wire contract; no production interface behavior registry case control certificate or manifest changes.
authorization_effect: KI-R5-WINDOW-AGENT may append only the exact EV-KI-A-062 C004 block to S1, dispatch and independently review its single inventory-test leaf, and on pass redispatch S016 using C004's resulting digest without another parent review.
resumption_state: A5 state 123 DECOMPOSITION_APPROVED under ASG-KI-R5-WA-01. Execute C004 then resume S016 and the approved KI-R5 sequence through parent handoff; stop before KI-W6.
```

```yaml
change_id: CHG-KI-038
timestamp: 2026-08-20T17:22:16+05:30
trigger_evidence: [EV-KI-R5-I001-01, EV-KI-A-063]
reason: KI-R5-I001 V2 passed its three selected frontend files but the frozen default-isolation invocation suppressed the nested diagnostic that is the sole runtime source of the required frontend_api certificate, preventing the four-certificate E1 input from being assembled.
old_revision: A5 state 123 DECOMPOSITION_APPROVED; S1 e73d80946af502c2e5d7225f0eeccdd5603535fdefbb05e19ccd2a13afb1a6b4; V2 command omitted --test-isolation=none; S2 state 36 PARENT_BLOCKED
new_revision: A5 state 124 DECOMPOSITION_APPROVED; exact V2 command-only evidence-protocol amendment authorized; corrected S1 revision to be computed and pinned by the window agent
changed_requirements: []
changed_decisions: [V2 executes the same three frontend test files under non-isolated Node test execution so its already-required nested frontend_api diagnostic is observable]
affected_windows: [KI-R5 I001 V2 evidence capture only; V1 remains valid; V3 V4 V5 E1 V6 V7 and all implementation leaves remain unchanged; KI-W6 remains blocked]
invalidated_evidence: [EV-KI-R5-I001-01 V2 acceptance disposition only; its passing three-file result and certificate-absence diagnosis remain diagnostic history]
compatibility_or_migration_effect: none — runner evidence-capture protocol only; no production code test oracle registry case control manifest digest schema package or external behavior changes.
authorization_effect: KI-R5-WINDOW-AGENT may apply only the exact EV-KI-A-063 S1 amendment, re-pin S1 in S2/S3, run the corrected V2 command exactly once, and on pass resume unchanged I001 at V3 without another parent review.
resumption_state: A5 state 124 DECOMPOSITION_APPROVED under ASG-KI-R5-WA-01. Preserve V1, recapture V2 once with --test-isolation=none, then complete unchanged V3 through V7 and E1 and return for parent handoff; stop before KI-W6.
```

```yaml
change_id: CHG-KI-039
timestamp: 2026-08-20T17:27:24+05:30
trigger_evidence: [EV-KI-R5-I001-03, EV-KI-A-064]
reason: The isolated test database URL already exists in email_scraper/.env, but KI-R5 V3's frozen direct Node command did not preload dotenv while the helper reads only process.env; the preflight therefore reported a false missing-prerequisite blocker before V3 started.
old_revision: A5 state 124 DECOMPOSITION_APPROVED; S1 c5411cb28ab806522ac28977b447ab91816f691a4bd4fe9209773f06b596571e; V3 command omitted dotenv/config preload; S2 state 38 PARENT_BLOCKED
new_revision: A5 state 125 DECOMPOSITION_APPROVED; exact V3 command-only environment-loading amendment authorized; corrected S1 revision to be computed and pinned by the window agent
changed_requirements: []
changed_decisions: [V3 preloads the repository-installed dotenv/config module so the existing local TEST_DATABASE_URL reaches the unchanged isolated-postgres helper]
affected_windows: [KI-R5 I001 V3 invocation only; accepted V1 and V2 evidence remains valid; V4 V5 E1 V6 V7 and all implementation leaves remain unchanged; KI-W6 remains blocked]
invalidated_evidence: [EV-KI-R5-I001-03 missing-user-prerequisite disposition only; its no-V3-execution and absent-process-variable observations remain diagnostic history]
compatibility_or_migration_effect: none — local test-runner environment loading only; no URL value production code test oracle schema migration registry case control certificate manifest digest package or external behavior changes.
authorization_effect: KI-R5-WINDOW-AGENT may apply only the exact EV-KI-A-064 S1 amendment, re-pin S1 in S2/S3, run corrected isolated V3 exactly once, and on pass resume unchanged I001 at V4 without another parent review.
resumption_state: A5 state 125 DECOMPOSITION_APPROVED under ASG-KI-R5-WA-01. Preserve V1 and V2, execute V3 once with dotenv preloaded and all isolation guards active, then complete unchanged V4 through V7 and E1 and return for parent handoff; stop before KI-W6.
```

```yaml
change_id: CHG-KI-040
timestamp: 2026-08-20T17:29:49+05:30
trigger_evidence: [EV-KI-R5-I001-04, EV-KI-A-065]
reason: V3's child-only name pattern excluded the differently named top-level database registry before its R5 children could register and also excluded the top-level R5 certificate test, producing deterministic zero-work with no database mutation.
old_revision: A5 state 125 DECOMPOSITION_APPROVED; S1 c5411cb28ab806522ac28977b447ab91816f691a4bd4fe9209773f06b596571e; V3 child-only pattern and no recorded dotenv preload; S2 state 39 PARENT_BLOCKED
new_revision: A5 state 126 DECOMPOSITION_APPROVED; consolidated dotenv-preload plus parent-child-certificate V3 command amendment authorized; corrected S1 revision to be computed and pinned by the window agent
changed_requirements: []
changed_decisions: [V3 selection explicitly includes the top-level registry both required nested R5 cases and the top-level R5 certificate while retaining dotenv preload and the unchanged isolated database helper]
affected_windows: [KI-R5 I001 V3 runner protocol only; accepted V1 and V2 evidence remains valid; V4 V5 E1 V6 V7 and all implementation leaves remain unchanged; KI-W6 remains blocked]
invalidated_evidence: [EV-KI-R5-I001-04 V3 acceptance disposition only; its zero-test zero-mutation diagnosis remains diagnostic history; EV-KI-A-064's unincorporated standalone S1 command instruction is superseded by the consolidated EV-KI-A-065 command]
compatibility_or_migration_effect: none — test-runner selection and local environment loading only; no production code test registration oracle schema migration registry case control certificate manifest digest package or external behavior change.
authorization_effect: KI-R5-WINDOW-AGENT may apply only the exact EV-KI-A-065 consolidated S1 amendment, re-pin S1 in S2/S3, run corrected V3 exactly once, and on pass resume unchanged I001 at V4 without another parent review.
resumption_state: A5 state 126 DECOMPOSITION_APPROVED under ASG-KI-R5-WA-01. Preserve V1 and V2, execute one corrected V3 selecting parent children and certificate under all isolation guards, then complete unchanged V4 through V7 and E1 and return for parent handoff; stop before KI-W6.
```

```yaml
change_id: CHG-KI-041
timestamp: 2026-08-20T17:35:35+05:30
trigger_evidence: [EV-KI-R5-I001-06, EV-KI-A-066]
reason: The corrected network-permitted V3 process ended but its execution channel returned no TAP payload exit disposition certificate or cleanup witness, making the attempt unobservable and neither acceptable nor diagnosable as a product failure.
old_revision: A5 state 126 DECOMPOSITION_APPROVED; S1 70377911c49c006c8a88de150753ef0d0fadd33ba84f8f9b955e58c867ba7b9e; S2 state 41 PARENT_BLOCKED after ambiguous V3 attempt
new_revision: A5 state 127 DECOMPOSITION_APPROVED; read-only orphan preflight plus one fixed-path durable-capture V3 recovery authorized; amended S1 revision to be computed and pinned by the window agent
changed_requirements: []
changed_decisions: [V3 recovery writes TAP and Node exit status to unique fixed /tmp artifacts so acceptance does not depend on the transient execution channel]
affected_windows: [KI-R5 I001 V3 evidence recovery only; accepted V1 and V2 remain valid; V4 V5 E1 V6 V7 and all implementation leaves remain unchanged; KI-W6 remains blocked]
invalidated_evidence: [EV-KI-R5-I001-06 V3 disposition only; its unobservable-attempt and no-running-process facts remain authoritative]
compatibility_or_migration_effect: none — execution evidence transport only; no production code test registration oracle schema migration registry case control certificate manifest digest package or external behavior change.
authorization_effect: KI-R5-WINDOW-AGENT may apply only the EV-KI-A-066 S1 recovery amendment, perform one read-only zero-residual-schema preflight, execute one durable-capture V3 recovery, and on pass resume unchanged I001 at V4 without another parent review.
resumption_state: A5 state 127 DECOMPOSITION_APPROVED under ASG-KI-R5-WA-01. Preserve V1/V2, require zero orphan schemas, recover V3 once through fixed /tmp TAP and exit artifacts, then on pass complete unchanged V4 through V7 and E1 and return for parent handoff; stop before KI-W6.
```

```yaml
change_id: CHG-KI-042
timestamp: 2026-08-20T17:43:50+05:30
trigger_evidence: [EV-KI-R5-I001-08, EV-KI-A-067]
reason: State127 ultimately produced exit status zero and complete 10-of-10 TAP, but the Node reporter destination excludes the certificate test's direct process.stdout emission and the live stdout channel was not retained.
old_revision: A5 state 127 DECOMPOSITION_APPROVED; S1 82a267ec9bff5378dfd566288df5e3cb97cb3e4a3e6a363ecaf02cbee56cfcf5; state127 TAP and exit artifacts pass while database certificate transport remains absent; S2 state 43 PARENT_BLOCKED
new_revision: A5 state 128 DECOMPOSITION_APPROVED; one shell-launch direct-stdout combined-file V3 capture authorized; amended S1 revision to be computed and pinned by the window agent
changed_requirements: []
changed_decisions: [V3 final recovery captures TAP direct stdout and stderr in one pre-opened durable file and accepts complete zero-failure TAP instead of a separately written exit sidecar]
affected_windows: [KI-R5 I001 V3 evidence transport only; accepted V1 and V2 plus settled state127 behavior evidence remain valid; V4 V5 E1 V6 V7 and all implementation leaves remain unchanged; KI-W6 remains blocked]
invalidated_evidence: [EV-KI-R5-I001-08 claims that the state127 exit artifact is absent and TAP is only 750 bytes; its certificate-absence diagnosis remains valid]
compatibility_or_migration_effect: none — execution evidence transport only; no production code test registration oracle schema migration registry case control certificate manifest digest package or external behavior change.
authorization_effect: KI-R5-WINDOW-AGENT may apply only the EV-KI-A-067 capture amendment, perform one read-only zero-residual preflight, execute one combined-file V3 capture, and on pass resume unchanged I001 at V4 without another parent review.
resumption_state: A5 state 128 DECOMPOSITION_APPROVED under ASG-KI-R5-WA-01. Preserve V1/V2 and state127 artifacts, require zero orphan schemas, capture V3 once to the fixed state128 combined file, then on pass complete unchanged V4 through V7 and E1 and return for parent handoff; stop before KI-W6.
```

```yaml
change_id: CHG-KI-043
timestamp: 2026-08-20T17:51:38+05:30
trigger_evidence: [EV-KI-R5-I001-10, EV-KI-A-068]
reason: The state128 durable artifact uses Node's built-in spec reporter rather than TAP typography, but it contains complete equivalent totals plus the exact runtime database certificate; preserved state127 artifacts separately provide canonical TAP and exit zero on the same frozen V3 inputs.
old_revision: A5 state 128 DECOMPOSITION_APPROVED; S1 f8596179a5d93c049e6dce86afa02b44f100a89accf91b2828e7715a802c283b; S2 state 45 PARENT_BLOCKED solely because the state128 complete spec summary lacked TAP-specific markers
new_revision: A5 state 129 DECOMPOSITION_APPROVED; V3 accepted by parent from format-equivalent settled durable evidence; append-only S1 adjudication revision to be computed and pinned by the window agent
changed_requirements: []
changed_decisions: [A complete Node reporter result is accepted by semantic totals and runtime certificate rather than reporter-specific typography; state127 TAP and exit-zero evidence remains corroborating evidence]
affected_windows: [KI-R5 I001 V3 accepted; V4 V5 E1 V6 V7 resume unchanged; all implementation leaves unchanged; KI-W6 remains blocked]
invalidated_evidence: [EV-KI-R5-I001-10 failed-disposition and claim that complete TAP typography is mandatory for the state128 artifact only; its artifact facts and certificate validation remain authoritative]
compatibility_or_migration_effect: none — parent evidence-format adjudication only; no product code test registration oracle schema migration registry case control certificate manifest digest package or external behavior change.
authorization_effect: KI-R5-WINDOW-AGENT must record V3 PASS without another database action, preserve the three artifacts, resume I001 directly at V4, and complete unchanged V4 V5 E1 V6 V7 before returning for parent review.
resumption_state: A5 state 129 DECOMPOSITION_APPROVED under ASG-KI-R5-WA-01. V3 is accepted; run no more database commands; execute unchanged V4 through V7 and E1 once each, then return READY_FOR_PARENT_REVIEW; stop before KI-W6.
```

```yaml
change_id: CHG-KI-044
timestamp: 2026-08-20T17:58:54+05:30
trigger_evidence: [EV-KI-R5-I001-12, EV-KI-A-069]
reason: V4 lint and all 21 frontend tests passed, but the sandbox execution channel ended during next build without an exit result or BUILD_ID and no build process remains; only the build member lacks evidence and the browser member never started.
old_revision: A5 state 129 DECOMPOSITION_APPROVED; S2 state 47 PARENT_BLOCKED after unobservable V4 build portion
new_revision: A5 state 130 DECOMPOSITION_APPROVED; one sandbox-approved build-only recovery followed on pass by the original single browser execution authorized; amended S1 revision to be computed and pinned by the window agent
changed_requirements: []
changed_decisions: [V4 reuses its accepted lint and test members and reruns only the environmentally invalidated build member under required sandbox approval]
affected_windows: [KI-R5 I001 V4 only; V1 V2 V3 remain accepted; V5 E1 V6 V7 remain unchanged and pending; KI-W6 remains blocked]
invalidated_evidence: [EV-KI-R5-I001-12 build disposition only; its lint pass test pass absent BUILD_ID no-running-process and browser-not-started facts remain authoritative]
compatibility_or_migration_effect: none — execution-environment recovery only; no product code build configuration package test oracle registry case control certificate manifest digest or external behavior change.
authorization_effect: KI-R5-WINDOW-AGENT may record the adjudication, run one sandbox-approved build-only recovery, then on pass run the browser harness once and continue unchanged I001 at V5 without another parent review.
resumption_state: A5 state 130 DECOMPOSITION_APPROVED under ASG-KI-R5-WA-01. Preserve lint/tests, recover build once with sandbox approval, run browser once on the completed build, then finish unchanged V5 E1 V6 V7 and return READY_FOR_PARENT_REVIEW; stop before KI-W6.
```

```yaml
change_id: CHG-KI-045
timestamp: 2026-08-20T18:12:21+05:30
trigger_evidence: [EV-KI-R5-I001-14, EV-KI-A-070]
reason: The successful V4 build exposed two deterministic browser-harness false failures: W5-B02 counts its zero-result placeholder tr as a keyword row, and R5-FIN-03 tries to re-add low-volume row 1 while that row is outside the default 25-row page.
old_revision: A5 state 130 DECOMPOSITION_APPROVED; S2 state 49 PARENT_BLOCKED after browser exit 1; browser harness digest 1c4cc5ae801f586398cf2e7a30c785f84868001d215fd85bd3d1bc0a920deb01
new_revision: A5 state 131 DECOMPOSITION_APPROVED; one-file KI-R5-C005 plus fresh KI-R5-I002 browser-only reassessment authorized; amended S1 revision to be computed and pinned by the window agent
changed_requirements: []
changed_decisions: [W5-B02 counts rendered keyword-row checkboxes rather than the intentional empty-state placeholder; R5-FIN-03 exposes all 30 fixture rows by selecting page size 50 before the existing row-1 re-add]
affected_windows: [KI-R5 C005 and I002; V4 browser member only; accepted V1 V2 V3 lint frontend tests and build remain valid; V5 E1 V6 V7 remain pending; KI-W6 remains blocked]
invalidated_evidence: [EV-KI-R5-I001-14 V4 browser disposition only; its successful build failed-ID list generated-artifact inventory and no-valid-browser-certificate facts remain authoritative]
compatibility_or_migration_effect: none — browser acceptance-harness mechanics only; no product interface behavior component library API schema package registry case ID certificate digest manifest or external behavior changes.
authorization_effect: KI-R5-WINDOW-AGENT may append the exact EV-KI-A-070 C005 and I002 blocks to S1, dispatch and independently review one harness-file leaf, then rerun only the corrected browser member once and on pass complete unchanged V5 E1 V6 V7 without another parent review.
resumption_state: A5 state 131 DECOMPOSITION_APPROVED under ASG-KI-R5-WA-01. Preserve accepted prior gates and the successful build, execute C005, reassess through new I002, then return READY_FOR_PARENT_REVIEW; stop before KI-W6.
```

```yaml
change_id: CHG-KI-046
timestamp: 2026-08-20T18:14:13+05:30
trigger_evidence: [EV-KI-A-070, EV-KI-A-071]
reason: The requester committed the 12 previously dirty browser-evidence outputs while the C005 authorization was being verified, advancing the frontend repository from a dirty evidence baseline to clean commit a0477d5ae71b24f91826a5ceabf68d90aa66666b without changing the browser harness.
old_revision: A5 state 131 DECOMPOSITION_APPROVED; frontend at c80db6a with 12 dirty generated evidence paths; harness digest 1c4cc5ae801f586398cf2e7a30c785f84868001d215fd85bd3d1bc0a920deb01
new_revision: A5 state 132 DECOMPOSITION_APPROVED; frontend clean at requester commit a0477d5ae71b24f91826a5ceabf68d90aa66666b; unchanged harness digest and unchanged C005/I002 specification
changed_requirements: []
changed_decisions: []
affected_windows: [KI-R5 C005 repository baseline and I002 generated-evidence baseline only; all corrective transformations gates cases certificates and continuation remain unchanged; KI-W6 remains blocked]
invalidated_evidence: [EV-KI-A-070 statement that 12 evidence paths remain dirty/protected; its defect diagnosis C005 transformation and I002 reassessment specification remain authoritative]
compatibility_or_migration_effect: none — requester-only commit and coordination baseline update; no product code interface behavior test logic schema package registry certificate manifest or external behavior change.
authorization_effect: KI-R5-WINDOW-AGENT must author C005/I002 against clean frontend commit a0477d5 and may then proceed exactly as EV-KI-A-070 specifies without another parent review.
resumption_state: A5 state 132 DECOMPOSITION_APPROVED under ASG-KI-R5-WA-01. Execute unchanged C005 and I002 from the clean requester baseline, then complete pending KI-R5 gates and return for parent review; stop before KI-W6.
```

```yaml
change_id: CHG-KI-047
timestamp: 2026-08-20T18:27:00+05:30
trigger_evidence: [EV-KI-R5-I002-01, EV-KI-A-072]
reason: KI-R5-V4 simultaneously required an actual browser-origin emitted-route 401 witness and unqualified zero console errors, but Chrome necessarily records that expected failed resource response as one error-level network diagnostic even though all application and scenario oracles pass.
old_revision: A4 4f52bf764525927fd7b68c0795aec5cbbd15f1a8b9b73778d446cfd87e2b94b8; A5 state 132; S2 state 52 PARENT_BLOCKED after a zero-exit 25-of-25 browser run with one exact 401 console entry
new_revision: A4 d65c72d2c1441226dfd575495c5b2d8e8bb321b4c3a9cd9fe6c83ae2320d5084 with append-only KI-R5-V4-A1; A5 state 133 DECOMPOSITION_APPROVED; existing I002 browser execution accepted without rerun
changed_requirements: []
changed_decisions: [The zero-console V4 oracle means zero application-generated and zero unexpected browser errors; exactly one fixed Chrome 401 network diagnostic is allowed only with the passing required browser-origin R5-WIRE-04 witness and every other browser oracle]
affected_windows: [KI-R5 V4 acceptance and I002 continuation only; V5 E1 V6 V7 remain pending; all implementation leaves and prior gates remain accepted; KI-W6 remains blocked]
invalidated_evidence: [EV-KI-R5-I002-01 PARENT_BLOCKED disposition only; its complete execution results certificate and exact console-entry facts remain authoritative]
compatibility_or_migration_effect: none — acceptance classification for an expected browser network diagnostic only; no product behavior interface source test registry case certificate digest schema package or external effect changes.
authorization_effect: KI-R5-WINDOW-AGENT records V4 PASS from existing evidence without rerun, uses the captured browser certificate for E1, and completes V5 E1 V6 V7 once each before parent handoff.
resumption_state: A5 state 133 DECOMPOSITION_APPROVED under ASG-KI-R5-WA-01. Continue I002 directly at V5, then E1 V6 V7 and return READY_FOR_PARENT_REVIEW; stop before KI-W6.
```

```yaml
change_id: CHG-KI-048
timestamp: 2026-08-20T18:35:22+05:30
trigger_evidence: [EV-KI-R5-I002-03, EV-KI-A-073]
reason: V5's first npm test process ended after its transient execution channel closed without retaining final status or aggregate totals; no matching process or repository delta remained, so the result is environmentally unobservable rather than a pass or product failure.
old_revision: A5 state 133 DECOMPOSITION_APPROVED; S2 state 54 PARENT_BLOCKED after one unobservable npm test invocation; npm run check:secrets E1 V6 V7 unexecuted
new_revision: A5 state 134 DECOMPOSITION_APPROVED; one identical escalated npm test recovery through a persistent polled execution session authorized; all other gates unchanged
changed_requirements: []
changed_decisions: [The invalidated V5 process-result transport is recovered by rerunning the identical npm test command once outside the restricted sandbox and observing the same persistent session through final exit]
affected_windows: [KI-R5 V5 npm test member only; accepted V1 V2 V3 V4 remain valid; V5 secret scan E1 V6 V7 remain pending; KI-W6 remains blocked]
invalidated_evidence: [EV-KI-R5-I002-03 V5 run-budget and PARENT_BLOCKED disposition only; its partial-output no-process no-delta and no-external-action facts remain authoritative]
compatibility_or_migration_effect: none — execution environment and result transport only; no product code test selection oracle interface schema package registry certificate manifest or external behavior change.
authorization_effect: KI-R5-WINDOW-AGENT may run one identical escalated npm test recovery, then on pass run the still-unexecuted secret scan E1 V6 V7 once each and return for parent review.
resumption_state: A5 state 134 DECOMPOSITION_APPROVED under ASG-KI-R5-WA-01. Recover only npm test once through final exit, finish pending KI-R5 gates, and stop before KI-W6.
```

```yaml
change_id: CHG-KI-049
timestamp: 2026-08-20T18:37:00+05:30
trigger_evidence: [EV-KI-A-074]
reason: Treating sandbox permission for an already-authorized local command as new task authority caused unnecessary parent round trips and consumed execution time without improving product or acceptance safety.
old_revision: A5 state 134 required individually documented escalation recovery for V5
new_revision: A5 state 135 establishes standing sandbox escalation and one identical recovery for otherwise authorized local KI-R5 verification commands under exact invalidation preconditions
changed_requirements: []
changed_decisions: [Sandbox privilege may be used from the outset for an authorized local command; a purely sandbox-invalidated command may be repeated identically once under escalation without parent reauthorization]
affected_windows: [remaining KI-R5 local verification gates only; no successor or external gate]
invalidated_evidence: []
compatibility_or_migration_effect: none — execution permission policy only; no command behavior oracle product code interface schema package registry certificate manifest or external effect changes.
authorization_effect: KI-R5-WINDOW-AGENT no longer stops for sandbox permission alone and may apply the exact identical-recovery rule while completing V5 E1 V6 V7.
resumption_state: A5 state 135 DECOMPOSITION_APPROVED under ASG-KI-R5-WA-01. Complete the already-authorized V5 recovery and remaining gates; stop before KI-W6.
```

```yaml
change_id: CHG-KI-050
timestamp: 2026-08-20T18:42:43+05:30
trigger_evidence: [EV-KI-A-074, EV-KI-A-075]
reason: The standing sandbox rule must be part of both project-agnostic authoring standards so future parent and window agents do not treat execution privilege or a purely environment-invalidated local command as a new decision window.
old_revision: parent standard 3b7a4fd25156e1adfbc92abb835c5f82a0d18c686b1c1150feb202f2d944d2ac; window-agent standard 1766f9107ce7d315877b75d4b0ea2b5521dff1c321e12f890b03787d66196ded; A5 state 135
new_revision: parent standard cda352017e75c0d11f6797d9fbe108b4365508cd38b0e92365cfb523ede32848; window-agent standard 84e7590e74589f308c70dc9b0b67f7e9da395fafb1e5786202ecd1ca15be56e9; A5 state 136
changed_requirements: [Every future A5 grants standing sandbox escalation for already-authorized local actions, Every future S1 and S2 inherit that policy, One identical escalated recovery is permitted only after proven environment invalidation and exact read-only postconditions, Evidence and enforcement certificates report the invalidated attempt and recovery]
changed_decisions: [Sandbox privilege is not task authority, Proven sandbox or execution-channel invalidation does not consume the accepted gate run, Observable behavioral failure changed execution or external authority cannot be classified as environment recovery]
affected_windows: [already-active KI-R5-I002 may finish under its frozen standard revisions, every new KI-R5 sub-window or assessment is prohibited under those revisions, KI-W6 and successors require a parent delta audit and both new standard revisions]
invalidated_evidence: []
compatibility_or_migration_effect: none — authoring and execution-environment governance only; no product contract interface schema package test oracle registry certificate membership or runtime behavior changes.
authorization_effect: Finish the already-active KI-R5-I002 only. Do not assign another sub-window or KI-W6 until the live standard revisions are pinned through the required parent audit.
resumption_state: A5 state 136 DECOMPOSITION_APPROVED under ASG-KI-R5-WA-01. Complete V5 E1 V6 V7 and return for parent review; stop before KI-W6.
```

```yaml
change_id: CHG-KI-051
timestamp: 2026-08-20T18:46:51+05:30
trigger_evidence: [EV-KI-R5-I002-05, EV-KI-A-076]
reason: The first E1 invocation supplied malformed certificate JSON and exited before registering or executing any conformance case; V1 through V5 and the four accepted certificate semantics are unaffected.
old_revision: A5 state 136; V5 PASS; E1 one malformed-input invocation with 0 conformance cases; V6 and V7 unexecuted
new_revision: A5 state 137; one canonical parse-preflighted E1 recovery authorized using the exact four accepted certificate objects and pinned 2847-byte SHA-256 transport
changed_requirements: []
changed_decisions: [Canonicalize the four accepted certificates as one sorted JSON array with digest 63eedf904a3eb40729e5dc393085341ca7bf97105bc5a920ddedb106a4d70412 before the sole recovery, A parse-only preflight does not consume E1 because it does not import register or execute the enforcement test, The malformed zero-conformance invocation is diagnostic history and not acceptance evidence]
affected_windows: [KI-R5 E1 transport only; V1 through V5 remain accepted; V6 and V7 remain pending; KI-W6 remains blocked]
invalidated_evidence: [EV-KI-R5-I002-05 E1 run-budget and PARENT_BLOCKED disposition only; its malformed-input zero-conformance and no-write facts remain authoritative]
compatibility_or_migration_effect: none — certificate serialization and command transport only; no case membership digest oracle production code test source manifest fixture schema package or runtime behavior change.
authorization_effect: KI-R5-WINDOW-AGENT may record the adjudication in S1/S2/S3, perform one parse-only canonical-input preflight, run one corrected E1, then on pass execute V6 and V7 once and return for parent review.
resumption_state: A5 state 137 DECOMPOSITION_APPROVED under ASG-KI-R5-WA-01. Recover E1 once and stop on observable failure; otherwise finish V6/V7 and stop before KI-W6.
```

```yaml
change_id: CHG-KI-052
timestamp: 2026-08-20T18:55:06+05:30
trigger_evidence: [EV-KI-R5-I002-06, EV-KI-A-077]
reason: CONF-04 confuses exact browser-harness runtime evidence with implementation edits and therefore rejects an A5-authorized preserved output outside the correct 18-file implementation set.
old_revision: A4 d65c72d2c1441226dfd575495c5b2d8e8bb321b4c3a9cd9fe6c83ae2320d5084; A5 state 137; old standards frozen for active I002; E1 5/6 with CONF-04 failed
new_revision: A4 ecafe206e767d508089a8f8e772ab62444767fa4886feaad6b2a13013c6a0ada; A5 state 138; parent standard cda352017e75c0d11f6797d9fbe108b4365508cd38b0e92365cfb523ede32848; sub-window standard 84e7590e74589f308c70dc9b0b67f7e9da395fafb1e5786202ecd1ca15be56e9
changed_requirements: [CONF-04 classifies only five literal browser-harness review-evidence path and status pairs outside the unchanged implementation allowlist, Any other evidence path or wrong status fails, The window-agent decomposition satisfies the newly applicable sandbox-policy checks before a new leaf is assigned]
changed_decisions: [Runtime review evidence and implementation changes are separate exact classes, Absence of an allowlisted evidence output is permitted but an observed output must match its literal path and status, No wildcard evidence exemption is allowed, Corrected E1 plus V6 and V7 form the new assessment while V1 through V5 require explicit reuse proof]
affected_windows: [KI-R5 corrective decomposition and replacement integration assessment only; KI-W6 remains blocked]
invalidated_evidence: [EV-KI-R5-I002-06 E1 acceptance and CONF-04 result only; its canonical transport five passing conformance cases and root-cause facts remain diagnostic evidence]
compatibility_or_migration_effect: none — test-oracle status classification only; no product runtime interface schema package certificate membership digest or browser behavior change.
authorization_effect: KI-R5-WINDOW-AGENT may update S1/S2/S3 with the standards delta, single-file corrective block KI-R5-C006 and replacement assessment KI-R5-I003, then must stop for parent decomposition review without dispatching a leaf.
resumption_state: A5 state 138 CORRECTIVE_DECOMPOSITION_AUTHORIZED under ASG-KI-R5-WA-01. Author documentation only and return AWAITING_PARENT_DECOMPOSITION_REVIEW; stop before implementation or KI-W6.
```

```yaml
change_id: CHG-KI-053
timestamp: 2026-08-20T19:10:59+05:30
trigger_evidence: [EV-KI-R5-C006-01, EV-KI-R5-C006-02, EV-KI-R5-C006-03, EV-KI-A-078]
reason: Parent review found decomposition-only inaccuracies and the requester directed the parent to correct them directly without executing a leaf.
old_revision: S1 a8d888915d2db01bd44e8537627b89995b23632198737df0e45e8a0b4b78f810; S2 state 59; readiness count 3; noncanonical one-path digest in the latest certificate; nonliteral local helper invocation; incorrect claim that npm test did not import enforcement; V6/V7 incorrectly listed as invalidated
new_revision: S1 950a0cbb91a373c8075b1e3e5f1c2aee8e5b036871e7c751566e5d88309e4f26; S2 state 60; readiness 47/47; planned-file digest 2b272324c43a1f4120f0ece14c4579fac819c8702fc0feb94b4f1db61661b5de; literal commands and corrected reuse/gate classifications; A5 state 139 DECOMPOSITION_APPROVED
changed_requirements: []
changed_decisions: [C006 local verification uses the literal approved commands and does not claim CONF execution, I003 E1 owns actual CONF-04 and NC-12 execution, V5 npm test import is acknowledged and reused through the absent-environment guard plus final module-load proof, V5 secret-scan reuse requires exact non-secret diff proof, E1 alone is invalidated while V6 and V7 remain pending]
affected_windows: [KI-R5-C006 and KI-R5-I003 authoring and assignment only; KI-W6 remains blocked]
invalidated_evidence: [EV-KI-R5-C006-01 readiness certificate superseded by EV-KI-R5-C006-03; EV-KI-R5-C006-02 remains historical digest correction]
compatibility_or_migration_effect: none — decomposition accuracy only; no product test implementation manifest certificate schema package or runtime behavior changed.
authorization_effect: KI-R5-WINDOW-AGENT may record approval, assign one C006 leaf, independently accept it, execute I003, and return READY_FOR_PARENT_REVIEW. No parent or requester leaf execution is authorized.
resumption_state: A5 state 139 DECOMPOSITION_APPROVED under ASG-KI-R5-WA-01. Window agent manages C006 then I003 and stops before KI-W6.
```

```yaml
change_id: CHG-KI-054
timestamp: 2026-08-20T19:33:47+05:30
trigger_evidence: [EV-KI-R5-C006-05, EV-KI-R5-C007-01, EV-KI-A-079]
reason: C006's controls failed to enforce its written requirement that both original implementation-create paths remain untracked-only, allowing a weakened unconditional continue to pass local acceptance.
old_revision: S1 cc603020b65343f71d48457b275afbff526a179592805bf6a7c337a9b48d3b83; S2 state 63 PARENT_BLOCKED; C006 rejected; I003 unstarted; A5 state 139
new_revision: S1 9b78ce7945231cb031a78a6c4fec6ac6d7047d4faae21a5e110c2eb7b4a5f597; S2 state 64 AWAITING_PARENT_DECOMPOSITION_REVIEW; exact C007 and I004 authored; A5 state 140 DECOMPOSITION_APPROVED
changed_requirements: []
changed_decisions: [Restore exactly the original untracked-true assertion for both implementation-create paths, Require pass wrong-status-fail fresh-pass for each create path in addition to both review-evidence controls, Supersede unstarted I003 with I004 after C007]
affected_windows: [KI-R5-C007 and KI-R5-I004 only; C006 remains rejected; KI-W6 remains blocked]
invalidated_evidence: [C006 local-command pass as evidence of CONF-04 preservation; EV-KI-R5-C006-05 remains authoritative rejection evidence]
compatibility_or_migration_effect: none — enforcement-test oracle restoration only; no product runtime interface schema package case registry certificate digest or browser behavior change.
authorization_effect: KI-R5-WINDOW-AGENT may record approval, assign one C007 leaf, independently accept it, execute I004, and return READY_FOR_PARENT_REVIEW. No parent or requester leaf execution is authorized.
resumption_state: A5 state 140 DECOMPOSITION_APPROVED under ASG-KI-R5-WA-01. Window agent manages C007 then I004 and stops before KI-W6.
```

```yaml
change_id: CHG-KI-055
timestamp: 2026-08-20T20:18:30+05:30
trigger_evidence: [EV-KI-R5-C007-03, EV-KI-R5-I004-01, EV-KI-R5-I004-02, EV-KI-A-080]
reason: The requester-directed C007 status correction and I004 assessment completed the rejected C006 enforcement invariant, passed corrected E1 and the remaining V6/V7 gates, and supplied the mandatory window-agent integration certificate and consolidated handoff.
old_revision: A4 ecafe206e767d508089a8f8e772ab62444767fa4886feaad6b2a13013c6a0ada; A5 state 140 DECOMPOSITION_APPROVED under ASG-KI-R5-WA-01; accepted_through KI-W5; S2 state 68 READY_FOR_PARENT_REVIEW
new_revision: A4 2ea1f07a88d8064b20e8ea72a21c2894c941825c6db193f892a82c1398cf8ab7 with KI-R5 V1-V7 and H1-H6 evidenced plus append-only C007/I004 supersession; A5 state 141 ACCEPTED_UNASSIGNED; accepted_through KI-R5
changed_requirements: []
changed_decisions: [For the two already committed enforcement paths the final status invariant is tracked modification rather than untracked creation; the exact opposite status remains a falsifying control]
affected_windows: [KI-R5 accepted and closed; KI-W6 remains unassigned and its invalidated earlier decomposition remains unusable]
invalidated_evidence: [C006 local-pass sufficiency and untracked-create status assumption remain rejected/superseded; I001/I002 blocked dispositions and unstarted I003 are historical, with I004 the accepted final assessment]
compatibility_or_migration_effect: none — enforcement status classification and parent closeout only; no product runtime interface schema migration package case registry certificate digest provider AWS or production behavior change.
authorization_effect: ASG-KI-R5-WA-01 is fulfilled and closed; no agent holds an assignment. This change does not assign, decompose or start KI-W6.
resumption_state: A5 state 141 has no active window, accepts through KI-R5, names KI-W6 only as the next unassigned window, and keeps may_start_successor false. Any future KI-W6 work requires a fresh parent assignment and fresh decomposition; the state-108 decomposition cannot be reused.
```

```yaml
change_id: CHG-KI-056
timestamp: 2026-08-20T20:55:19+05:30
trigger_evidence: [SRC-KI-038, SRC-KI-039, SRC-KI-040, EV-KI-A-081]
reason: The old W6 specification delegated coverage and proof-topology choices, omitted post-R5 contracts and enforcement, and would accept dashboard navigation to the backend JSON status endpoint rather than the real run workspace.
old_revision: A2 KI-DD-4; A3 KI-DL-13 / e8ed580dd08b77540158340c47fae84c5d56b18cc7aba3149ccc2ab568493f5d; A4 KI-CL-17 / 2ea1f07a88d8064b20e8ea72a21c2894c941825c6db193f892a82c1398cf8ab7; A8 KI-TR-11; A5 state 141 ACCEPTED_UNASSIGNED
new_revision: A2 KI-DD-5 / 9f311515564da6db4411a22295d9543651a0bac2ee53839a796ec8d3f4a52134; A3 KI-DL-14 / ef4153677807c80dfa9a09c0ffe0ba5a5127681fe6706e17ff6cd48869fdbd31; A4 KI-CL-18 / 02352344d5ba940f640463f89bc3011339d6e9f175ca35343abe4e63412523e2; A8 KI-TR-12 / 2f42684c9bc41e6390c9fc53cdead403189090391b7f7a34b3167355a915df83; A5 state 142 READY and unassigned
changed_requirements: [Successful browser handoff opens the encoded /runs/<runId> workspace while API statusUrl remains unchanged, W6 proves one connected authenticated emitted local workflow through the 1000-domain lead-task boundary, W6 acceptance uses literal 26-case coverage and 13 falsification controls under explicit substitute limits]
changed_decisions: [DEC-KI-038, Five exact W6 implementation paths and path digest, Fresh REAUTHORED recursive coordination artifacts, One frontend build and one isolated-schema causal browser gate, R5-FIN-01 destination assertion alone superseded]
affected_windows: [KI-W6 reauthored and authoring-ready but unassigned, KI-W7 remains prohibited and parent-reserved]
invalidated_evidence: [The state-108 KI-W6 decomposition and all of its unexecuted planned IDs/topology/certificates remain unusable, R5-FIN-01 destination assertion will be superseded only when W6 implementation is accepted; all other accepted R5 evidence remains valid]
compatibility_or_migration_effect: no schema migration package backend API route auth proxy worker adapter infrastructure or standalone-project change; statusUrl remains the API resource and browser routing changes only after successful handoff.
authorization_effect: This change authorizes no implementation or decomposition. A future explicit parent A5 CAS may assign one KI-W6-WINDOW-AGENT to create only the three fresh REAUTHORED coordination artifacts and return for parent decomposition review; leaf and integration work remain prohibited until that review.
resumption_state: A5 state 142 is READY with no current window/assignment, accepted through KI-R5, next KI-W6, stop_after KI-R5 and may_start_successor false.
```

```yaml
change_id: CHG-KI-057
timestamp: 2026-08-20T23:05:00+05:30
trigger_evidence: [EV-KI-A-084]
reason: DECOMP-3 faithfully exposed runnable-harness gaps in the parent W6 authority: missing frontend backend-token propagation, a non-callable server logger, unfrozen DataForSEO synthesis, Google results that parse but fail production relevance, and duplicate/reorder operations scheduled against empty or unidentified queues.
old_revision: A4 KI-CL-18 / 02352344d5ba940f640463f89bc3011339d6e9f175ca35343abe4e63412523e2; A5 state 144; S1 DECOMP-3 2ea48e27d47ddc0824285471877e4897b3740c16516f0b1abea81cb79b77bb4c
new_revision: A4 KI-CL-19 / 8fa54dd445dda3ad3bda8a4b0434bbbc8f93ad75469f782015ab4631eed9bcb3; A5 state 145; DECOMP-3 rejected pending S1/S2/S3 reconciliation
changed_requirements: []
changed_decisions: [Emitted Next receives the exact matching backend token privately, createLeadServer logger is callable, deterministic expansion and overview synthesis proves 300/200/default-100, every Google occurrence carries received-query relevance and passes the production probe, queue-specific duplicate/reorder faults run only at frozen nonempty points]
affected_windows: [KI-W6 decomposition only; KI-W7 remains prohibited]
invalidated_evidence: [KI-W6-R07 decomposition-readiness certificate and DECOMP-3 assignability claim; its F6-F9 source findings remain valid inputs]
compatibility_or_migration_effect: none — local W6 harness specification only; no product runtime API schema migration package provider AWS or production behavior change.
authorization_effect: KI-W6-WINDOW-AGENT may revise only the three REAUTHORED coordination artifacts to reconcile A4 KI-CL-19 and EV-KI-A-084 F10-F12, then return for parent review; no leaf or gate execution is authorized.
resumption_state: A5 state 145 READY under ASG-KI-W6-WA-02; stop before leaf dispatch, implementation or KI-W7.
```

```yaml
change_id: CHG-KI-058
timestamp: 2026-08-20T22:38:27+05:30
trigger_evidence: [EV-KI-A-085]
reason: KI-CL-19 assigned one backend restart to both the pre-expansion resilience partition and the post-handoff immutable-snapshot partition, two mutually exclusive causal positions.
old_revision: A4 KI-CL-19 / 8fa54dd445dda3ad3bda8a4b0434bbbc8f93ad75469f782015ab4631eed9bcb3; A5 state 145; S1 DECOMP-4 c197af8640cce52e9224c35aa41159754c271b99d5a5222765bf20feb0665831
new_revision: A4 KI-CL-20 / 8fe18271bf368a283246d55807dcc4612e118c725e5aabeb6188962a7abf5f4e; A5 state 146; DECOMP-4 rejected pending narrow S1/S2/S3 reconciliation
changed_requirements: []
changed_decisions: [Invoke restart A after keyword duplicate/reorder and before expansion drain, Invoke restart B after post-handoff research-selection mutation and before immutable Run projection comparison, Reuse the existing restartBackend harness operation for both invocations]
affected_windows: [KI-W6 decomposition only; KI-W7 remains prohibited]
invalidated_evidence: [KI-W6-R09 decomposition-readiness certificate and DECOMP-4 assignability claim; its F10-F12 reconciliation remains valid]
compatibility_or_migration_effect: none — local W6 harness causal ordering only; no product runtime API schema migration package provider AWS or production behavior change.
authorization_effect: KI-W6-WINDOW-AGENT may revise only the three REAUTHORED coordination artifacts to reconcile A4 KI-CL-20 and EV-KI-A-085 F13, then return for parent review; no leaf or gate execution is authorized.
resumption_state: A5 state 146 READY under ASG-KI-W6-WA-02; stop before leaf dispatch, implementation or KI-W7.
```

```yaml
change_id: CHG-KI-059
timestamp: 2026-08-20T22:50:00+05:30
trigger_evidence: [EV-KI-A-086]
reason: DECOMP-5's predecessor declarations permitted out-of-order dispatch even though the parent and the same S1 froze strict sequential execution and predecessor-based starting change-set digests.
old_revision: A5 state 146; S1 DECOMP-5 dedb5a2b3339856d6eeafb6f34ea4460a4de7dd3da298cb9ee9f515fd48ebe2e; mixed predecessor graph
new_revision: A5 state 147; narrow F14 correction assigned; exact chain S101 to S102 to S103 to S104 to S105 to I101 required
changed_requirements: []
changed_decisions: [Each initial leaf after S101 names the immediately preceding leaf as its sole predecessor, I101 retains all five accepted leaves as predecessors, Semantic file dependency records remain unchanged]
affected_windows: [KI-W6 decomposition only; KI-W7 remains prohibited]
invalidated_evidence: [EV-KI-W6-R11 readiness certificate and DECOMP-5 assignability claim; its F13 reconciliation remains valid]
compatibility_or_migration_effect: none — recursive scheduling metadata only; no implementation file interface behavior case registry digest or gate changes.
authorization_effect: KI-W6-WINDOW-AGENT may revise only S1/S2/S3 for F14 and return for parent review; no leaf or gate execution.
resumption_state: A5 state 147 READY under ASG-KI-W6-WA-02; stop before leaf dispatch, implementation or KI-W7.
```

```yaml
change_id: CHG-KI-060
timestamp: 2026-08-20T23:00:00+05:30
trigger_evidence: [EV-KI-W6-R12, EV-KI-W6-R13, EV-KI-A-087]
reason: DECOMP-6 resolves all parent findings and passes the standards-mandated independent parent review with exact file set baselines sequence interfaces gates controls and readiness closure.
old_revision: A5 state 147 correction assignment; S1 DECOMP-6 awaiting parent review
new_revision: A5 state 148 DECOMPOSITION_APPROVED; approved S1 revision bf92d2515a3dde37e7e577308ee69b224fe21498434ef831612536a841475134
changed_requirements: []
changed_decisions: [The approved leaf order is S101 then S102 then S103 then S104 then S105, I101 begins only after all five are independently accepted, Window agent may create one-file corrections only inside the same five-file parent scope for already-decided implementation defects]
affected_windows: [KI-W6 only; KI-W7 remains prohibited and parent-reserved]
invalidated_evidence: []
compatibility_or_migration_effect: none — decomposition approval and recursive execution authority only; no product runtime interface schema package or provider behavior change.
authorization_effect: KI-W6-WINDOW-AGENT may acknowledge approval in S2/S3 and manage the approved sequential leaves and I101; no leaf is assigned by this parent transition.
resumption_state: A5 state 148 DECOMPOSITION_APPROVED under ASG-KI-W6-WA-02; S2 must record approval and become READY before S101 dispatch.
```

```yaml
change_id: CHG-KI-061
timestamp: 2026-08-21T12:56:40+05:30
trigger_evidence: [SRC-KI-041, EV-KI-A-088]
reason: The causal maximum W6 run proved that production market aggregation bypassed the durable 200-keyword shortlist during final calculation and therefore published 300 rows despite the accepted 300-screen to 200-shortlist to 200-final contract.
old_revision: A2 KI-DD-5; A3 KI-DL-14 / ef4153677807c80dfa9a09c0ffe0ba5a5127681fe6706e17ff6cd48869fdbd31; A4 KI-CL-20 / 8fe18271bf368a283246d55807dcc4612e118c725e5aabeb6188962a7abf5f4e; A8 KI-TR-12; A5 state 148; five-path W6 parent scope; unchanged-worker-hash V6 premise
new_revision: A2 KI-DD-6 / cd0aca4b66e52f7953e2e411d0415df408ab5ccbbda4f83c9f9267c7c64db8ca; A3 KI-DL-15 / 4bb1201594bc4a33bf868f19dd73c6777d046cdbb8ae70ef2cc8972dd6c342ad; A4 KI-CL-21 / a499afe117ee9b9dba07ab1a420d8a9bae824d6d5d7419374427f9cc0687fa63; A8 KI-TR-13 / 2d0987b1ff7014d4561a9edd4ac5cec711b7893f420ea0de448c8bb564c909ed; A5 state 149; seven-path W6 parent scope; corrected worker-package proof required
changed_requirements: []
changed_decisions: [DEC-KI-039 projects per-seed expansion and reused US metrics from the immutable validated shortlist before final calculation, final rows equal shortlist cardinality at most 200, one extra validated S3 read and no other operation count changes, old worker hash evidence is replaced by a new deterministic package proof]
affected_windows: [KI-W6 remains active and unaccepted; KI-W7 remains prohibited and parent-reserved]
invalidated_evidence: [all failed W6 V3 attempts remain diagnostic; original W6 V6 unchanged-service-hash premise is invalidated when C104 edits service.js; the passed frontend V2 build remains reusable only under the exact committed-input proof]
compatibility_or_migration_effect: no product-contract schema migration API provider queue task artifact format key cost selection or historical compatibility change; this corrects current v1 calculation to the already accepted shortlist contract.
authorization_effect: KI-W6-WINDOW-AGENT may edit only S1/S2/S3 to append decision-complete and execution-complete C104 then C105 and zero-write I102 and return for parent decomposition review; no leaf dispatch or implementation action is yet authorized.
resumption_state: A5 state 149 READY under ASG-KI-W6-WA-02; stop at AWAITING_PARENT_DECOMPOSITION_REVIEW before C104 assignment.
```

```yaml
change_id: CHG-KI-062
timestamp: 2026-08-21T13:15:38+05:30
trigger_evidence: [EV-KI-W6-R22, EV-KI-A-089]
reason: The state-149 C104/C105/I102 package is substantively correct but its two leaf authority blocks contain non-literal repository baselines, shorthand read scopes, one inherited-ID reference, and non-executable inspection checks, so it does not yet satisfy mandatory sub-window Sections 7.1 through 7.4.
old_revision: A5 state 149; S1 corrective appendix c305f7eb42dcef07ba19d7044d52b85bdc4e629458b7b363c49ce90e9cd1c69e; C104/C105 marked readiness-complete
new_revision: A5 state 150 READY for F15-F18 documentation-only reconciliation
changed_requirements: []
changed_decisions: []
affected_windows: [KI-W6 corrective decomposition only; KI-W7 remains prohibited]
invalidated_evidence: [EV-KI-W6-R22 C104/C105 section_7_fields_complete and status READY claims; its root-cause diagnosis, correction algorithm, scope, sequence and gate plan remain valid]
compatibility_or_migration_effect: none — recursive execution-authority precision only; no product runtime interface schema package provider case registry or gate behavior changes.
authorization_effect: KI-W6-WINDOW-AGENT may edit only S1/S2/S3 to correct F15-F18 and return for parent review; no leaf assignment, implementation, gate, external action, commit or push is authorized.
resumption_state: A5 state 150 READY under ASG-KI-W6-WA-02 for documentation correction only; stop again at AWAITING_PARENT_DECOMPOSITION_REVIEW before C104 dispatch.
```

```yaml
change_id: CHG-KI-063
timestamp: 2026-08-21T13:27:48+05:30
trigger_evidence: [EV-KI-W6-R23, EV-KI-A-090]
reason: The state-150 correction fixed baselines scopes and trace IDs, but its C104-C2 count can be satisfied by one pre-existing unrelated invariant plus one new guard, while C105-C2 does not witness the claimed default-100 or no-leak assertions and can match unrelated later source.
old_revision: A5 state 150; S1 corrective appendix 6b7e90944a9167b24d42c61fcb26b3d7e692bae6b7319b48d94c86503b4b93b2; EV-KI-W6-R23 readiness claim
new_revision: A5 state 151 READY for F19-F20 documentation-only anti-vacuity correction
changed_requirements: []
changed_decisions: []
affected_windows: [KI-W6 corrective decomposition only; KI-W7 remains prohibited]
invalidated_evidence: [EV-KI-W6-R23 F18 and section_7_fields_complete claims only; F15-F17 and every substantive correction decision remain valid]
compatibility_or_migration_effect: none — local inspection enforcement only; no product runtime interface schema package provider case registry scope sequence or gate behavior change.
authorization_effect: KI-W6-WINDOW-AGENT may edit only S1/S2/S3 to make C104-C2 and C105-C2 non-vacuous and return for parent review; no leaf assignment implementation gate external action commit or push is authorized.
resumption_state: A5 state 151 READY under ASG-KI-W6-WA-02 for documentation correction only; stop again at AWAITING_PARENT_DECOMPOSITION_REVIEW before C104 dispatch.
```

```yaml
change_id: CHG-KI-064
timestamp: 2026-08-21T13:37:44+05:30
trigger_evidence: [EV-KI-W6-R24, EV-KI-A-091]
reason: The state-151 package closes the final two anti-vacuity gaps by independently witnessing both projection-specific production guards and bounding the focused regression before requiring its exact default-100 and no-leak assertions.
old_revision: A5 state 151 documentation correction; S1 b99633447c17163f6e883d71388b0200a345d2c0ced51252b8d03a8fba3b6b38 awaiting renewed parent review
new_revision: A5 state 152 DECOMPOSITION_APPROVED / 84e35abf369bfcaf11069b0a21e17744b160da48329f53dde5cb3c52ea4f8b00; approved S1 b99633447c17163f6e883d71388b0200a345d2c0ced51252b8d03a8fba3b6b38
changed_requirements: []
changed_decisions: []
affected_windows: [KI-W6 only; KI-W7 remains prohibited and parent-reserved]
invalidated_evidence: []
compatibility_or_migration_effect: none — recursive decomposition approval only; no product runtime interface schema package provider case registry scope sequence or gate behavior change.
authorization_effect: KI-W6-WINDOW-AGENT may acknowledge approval in S2/S3, dispatch only C104 first, independently review it, then dispatch C105, independently review it, and personally execute I102; no leaf is assigned by this parent transition.
resumption_state: A5 state 152 DECOMPOSITION_APPROVED under ASG-KI-W6-WA-02; S2 must record approval and become READY before C104 dispatch; stop READY_FOR_PARENT_REVIEW before KI-W7.
```

```yaml
change_id: CHG-KI-065
timestamp: 2026-08-21T13:52:46+05:30
trigger_evidence: [EV-KI-W6-R26, EV-KI-A-092]
reason: C104's reviewed bytes were committed by the requester between leaf execution and window review; the generic no-commit prohibition applies to agents and must not misclassify the requester's owner-controlled commit as a leaf violation.
old_revision: A5 state 152 DECOMPOSITION_APPROVED; S2 state 18 PARENT_BLOCKED on unresolved actor attribution for backend commit 9eff81490d15f6c001bf30121133f538addb81bf
new_revision: A5 state 153 READY / 7b4f43dd62b3262303921878d525908a09689a842cfcf5150d13c3427d772cd8; requester-owned provenance adjudicated
changed_requirements: []
changed_decisions: []
affected_windows: [KI-W6 only; KI-W7 remains prohibited and parent-reserved]
invalidated_evidence: [EV-KI-W6-R26 PARENT_BLOCKED disposition only; its source review local checks digests scope findings and negative results remain valid]
compatibility_or_migration_effect: none — execution-provenance classification only; no product runtime interface schema package provider case registry scope sequence or gate behavior change.
authorization_effect: KI-W6-WINDOW-AGENT may record the requester attribution, accept C104 from its existing independent review if no other defect exists, and then dispatch C105; no source/history rewrite rerun or direct parent leaf acceptance is authorized.
resumption_state: A5 state 153 READY under ASG-KI-W6-WA-02; C105 remains unassigned until the window agent records C104 ACCEPTED_FOR_INTEGRATION; stop READY_FOR_PARENT_REVIEW before KI-W7.
```

```yaml
change_id: CHG-KI-066
timestamp: 2026-08-21T14:20:05+05:30
trigger_evidence: [EV-KI-W6-R28, SRC-KI-042, EV-KI-A-093]
reason: I102 exposed that the accepted component scaffold used a task fingerprint for a stage manifest and encoded the 300-candidate maximum as one seed despite the immutable 60-per-seed contract.
old_revision: A2 KI-DD-6; A3 KI-DL-15 / 4bb1201594bc4a33bf868f19dd73c6777d046cdbb8ae70ef2cc8972dd6c342ad; A4 KI-CL-21 / a499afe117ee9b9dba07ab1a420d8a9bae824d6d5d7419374427f9cc0687fa63; A8 KI-TR-13; A5 state 153; I102 PARENT_BLOCKED
new_revision: A2 KI-DD-7 / 8095243aa7482b49e0991a8cafae0235cf87894d39d1a9e2007f3c234978e9e2; A3 KI-DL-16 / e59252cb3798fbdae805f43f33f69bf22de083c67d9a000632f5a1d2208e5a6c; A4 KI-CL-22 / bb823eca63520b6e0a8cd3b90b37fd9063813ee692c49d5c83bcc355cb1c0025; A8 KI-TR-14 / 31bd8df4912b2cf7d569316c08398d993d60b486ff7b175ad96362f220be28b5; A5 state 154 / 8e5624d405967500a14a1cf9c1384c70beaeba45bcc615efa37b416adc15bdad
changed_requirements: []
changed_decisions: [DEC-KI-040 preserves stage-manifest fingerprint identity, preserves the 60-per-seed schema, represents the 300 maximum as five seeds times 60, and assigns one test-file correction plus a fresh assessment]
affected_windows: [KI-W6 remains active; KI-W7 remains prohibited and parent-reserved]
invalidated_evidence: [I102 CV1 failure remains diagnostic; C105 shortlist-fingerprint and one-seed-SCN assertions are superseded; C104 production evidence and all other C105 work remain valid]
compatibility_or_migration_effect: none — test substitute correction only; no production runtime interface artifact schema package provider queue cost or persistent behavior change.
authorization_effect: KI-W6-WINDOW-AGENT may copy the literal C106/I103 blocks into S1/S2/S3, certify identity, dispatch/review C106, then execute I103 and continue to handoff without another parent prompt if all gates pass.
resumption_state: A5 state 154 READY under ASG-KI-W6-WA-02; stop READY_FOR_PARENT_REVIEW after I103 and before KI-W7.
```

```yaml
change_id: CHG-KI-067
timestamp: 2026-08-21T14:50:00+05:30
trigger_evidence: [EV-KI-W6-R31, EV-KI-A-094]
reason: I103 CV9's restricted attempt was environment-invalidated before any case and its one elevated recovery returned no output certificate diagnostics or exit metadata, leaving no usable acceptance result or observable product failure.
old_revision: A5 state 154 READY; I103 BLOCKED after CV7/CV8 with the automatic identical-recovery allowance exhausted
new_revision: A5 state 155 READY; one final observable elevated CV9 transport recovery authorized
changed_requirements: []
changed_decisions: []
affected_windows: [KI-W6 only; KI-W7 remains prohibited and parent-reserved]
invalidated_evidence: []
compatibility_or_migration_effect: none — gate transport and evidence retention only; the CV9 command environment selection fixtures oracle cases controls and acceptance values are unchanged.
authorization_effect: KI-W6-WINDOW-AGENT may record the disposition in S2/S3 and make exactly one final elevated CV9 attempt using persistent or transparent stdout stderr and exit capture; on pass it continues CV10-CV12 and CH3/CH4, while an observable failure or renewed unobservability stops with no further CV9 retry.
resumption_state: A5 state 155 READY under ASG-KI-W6-WA-02; preserve C106/CV7/CV8; stop READY_FOR_PARENT_REVIEW after I103 and before KI-W7.
```

```yaml
change_id: CHG-KI-068
timestamp: 2026-08-21T15:05:00+05:30
trigger_evidence: [EV-KI-W6-R33, SRC-KI-043, EV-KI-A-095]
reason: The final observable CV9 recovery exposed a causal-harness same-page assumption: its selection helper requires checked and unchecked rows in one 25-row DOM page although the accepted result has 200 paginated rows and a 100-item selection.
old_revision: A2 KI-DD-7 / 8095243aa7482b49e0991a8cafae0235cf87894d39d1a9e2007f3c234978e9e2; A3 KI-DL-16 / e59252cb3798fbdae805f43f33f69bf22de083c67d9a000632f5a1d2208e5a6c; A4 KI-CL-22 / bb823eca63520b6e0a8cd3b90b37fd9063813ee692c49d5c83bcc355cb1c0025; A8 KI-TR-14 / 31bd8df4912b2cf7d569316c08398d993d60b486ff7b175ad96362f220be28b5; A5 state 155; I103 CV9 failed
new_revision: A2 KI-DD-8 / 66a85fa6918193635e438dac1dd21986d0fd75fbfba791386a7f140470a9bd68; A3 KI-DL-17 / 4d7e4aa311286d997b2498f7af46fa0a32426d1cbace5e1d1f3db340009168b7; A4 KI-CL-23 / d47d0dd73b7efd357a7fc196ee64bfba2c2e5b0e4f818ea6e8180054e1f36eae; A8 KI-TR-15 / e4fb208e39e60f41f87f0b398b5979aa1702fce7e6124a7f2260c2a7d844a9bc; A5 state 156 READY
changed_requirements: []
changed_decisions: [DEC-KI-041 locks a real-pagination two-checkbox swap in the causal harness]
affected_windows: [KI-W6 remains active; KI-W7 remains prohibited and parent-reserved]
invalidated_evidence: [accepted S105 swapOneSelectionItemViaUi implementation evidence is superseded only for that helper; EV-KI-W6-R33 remains diagnostic and cannot satisfy CV15; C106/CV7/CV8 and all other S105 cases controls and oracles remain valid]
compatibility_or_migration_effect: none — one test-harness symbol only; no product runtime payload schema persistence package provider cost case registry or build input changes.
authorization_effect: KI-W6-WINDOW-AGENT may transcribe C107/I104 into S1/S2/S3, dispatch and review one C107 leaf, then execute I104 and continue to READY_FOR_PARENT_REVIEW only if every frozen gate passes; no parent artifact edit by the window agent and no KI-W7 action.
resumption_state: A5 state 156 READY under ASG-KI-W6-WA-02; preserve C106/CV7/CV8, execute C107 then I104, stop before KI-W7.
```
