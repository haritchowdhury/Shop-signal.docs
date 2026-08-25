# KI-W8 AWS-Only Sub-Window Evidence (`S3`)

Append-only evidence for `KI-W8-AWS-ONLY-DECOMP-1`. Authoring evidence does not
authorize or claim P1–P6, measurement, network, AWS, deployment, provider,
database, browser, local-server, paid or KI-W9 execution.

## `EV-KI-W8-AWS-S001` — authority, entry and parent correction

**Assignment:** `ASG-KI-W8-WA-02` under A5 state 204.  
**Window agent:** `/root/ki_w8_aws_decomposition`.  
**Outcome:** `PASS`.

Read-only SHA-256 preflight reproduced:

```text
parent standard  cda352017e75c0d11f6797d9fbe108b4365508cd38b0e92365cfb523ede32848
subwindow std    842c29550c06c22d63e0a058a27cb8a9ff6b538b3168d2c83a384890b44247f0
A1               8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c
A2               3a6b294cc561556d0e3d92572121bc8cc529470866fba5bad8f78cf816310470
A3               d65cd9b128170de778a2d1492ef8347c5d2a988b8c3c7737f4a36b740531515a
A4               b6cf79dd8fbe925101dd2c618c01ee1072f6df30c4653ea3c45c2660e6f0126b
A5               f2ebabb1285abd133fff07099fb67178ba133a38a03388a08ec9880c08f12de5
A6               116e49f031399fd1f4337bb161946c2ca07a1feb86b77c6732ce23dc99017f06
A7               f7e6cee213b5d109f3250536dfd00b825b0ef0d72b8ba3bf01a49aa84a2ce202
A8               76e5fbdab699f07fdabb85a381c6b7f400a8fcfa2619b517cdf0ab6304a4de89
```

The first authoring pass detected that P4's two accepted measurement commands
overwrite two generated JSON files absent from the then-current W8 write scope.
No command was executed. The window agent stopped and returned that precise
contradiction. Parent evidence `EV-KI-A-129` and change `CHG-KI-098` corrected
A4, producing the pinned A4 revision above and A5 state 204. This decomposition
therefore includes the two generated files and has no remaining P4 write-scope
contradiction.

Entry baselines were read-only verified:

```text
root HEAD      8a235e858888cbd0ea21a26520493cda72ba1a23
backend HEAD   4f9d6ce079d7fcd93d8a034b0592d4cdc1522f02 (porcelain empty)
frontend HEAD  5e441aae7e2f3a132b2c7fc85bf1bc525d3d5cb6 (porcelain empty)
```

The root entry delta was exactly seven parent authority files, sorted-member-LF
digest `6a8baa5680b1bc6f308c3778347ff3c9f24d17f9716c91abb361f1a1388d00cc`.
S1–S3 were absent. The three deployment-record JSON paths were absent. The two
measurement outputs existed at the starting hashes/bytes recorded in S1 §2.
The superseded `KEYWORD_INTELLIGENCE_KI_W8_SUBWINDOW_*` package was not edited.

No build, measurement, database, browser, local server, network, provider, AWS,
production, paid, destructive, commit, push, leaf, subagent or KI-W9 action ran;
external cost was `$0.00`.

## `EV-KI-W8-AWS-S002` — decision and execution closure

**Outcome:** `PASS`.

The fresh decomposition contains zero FILE/CORRECTION leaves and one
window-agent-owned sequential integration assessment, `KI-W8-I101`. Its exact
graph is:

```text
parent decomposition approval
  -> later P1-P6-only A5 assignment
  -> G-W8-01 / stop for ACT-01 approval
  -> separately pinned W8-ACT-01 / G-W8-02 / stop for ACT-02 approval
  -> separately pinned W8-ACT-02 / G-W8-03
  -> G-W8-04 / parent-review stop
```

S1 freezes the exact P1–P6 command sequence; exact ACT-01 and ACT-02 commands;
observed-identity pinning rules; packet/object/change-set schemas; direct and
optional allowlist; disabled applied-state oracle; action-specific A5 entry
predicates; success, rollback, partial, lost-output and ambiguity branches;
E8.1 transport recovery; action limits; substitutes; four-case/eight-control
certificate; and V1–V4/H1–H6 stop boundary. No step selects an account, path,
object, change set, interface, schema, transaction, retry, failure semantic,
activation behavior or acceptance rule at execution time.

Allocation audit:

```text
unmapped requirements:       0
unmapped decisions:          0
unmapped tasks:              0
unmapped scenarios:          0
unmapped cases:              0
unmapped controls:           0
unresolved interfaces:       0
unresolved intermediate states: 0
unresolved execution choices:   0
unresolved evidence references: 0
multi-file leaves:           0
duplicate file owners:       0
initial leaf count:          0
integration assessments:     1
```

The planned initial implementation path set is empty and hashes to
`e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855`.
The seven-path parent W8 coordination/generated set hashes to
`c7be57239e421128c087aa75b1d4a67305e86e1da530b70f894b274ffdb3587f`;
the S1–S3 administrative set hashes to
`92afa898a46252737c52e5be698ebc65c197cd5862294b59a5998c8fe46565b3`;
their ten-path union hashes to
`775f9083d0cfc21609f6c6f1c8ba3c6e99619916cf25afb4e9b340995faa482b`.

Required case membership is exactly four with digest
`3bd44b2c2c244b1dd29881dcfa249d9cdad5f9b1aecc981c56612d587283ca7e`.
Required control membership is exactly eight with digest
`9bd004917f960abb4842ea2f2da48ed60821fdedd55fcbc54dc7bdd271037ea6`.
The direct change-set member-ID set is exactly 13 with digest
`f1200139c3ceae903f0443d7c2c2ca134ba44f1192d7d98be10fddc4a3422b90`.

## `EV-KI-W8-AWS-S003` — mechanical and adversarial authoring audit

**Outcome:** `PASS`.

Read-only deterministic checks against S1 produced:

```text
mandatory SW-* checked:       47
mandatory SW-* unique:        47
mandatory SW-* unchecked:     0
implementation leaf blocks:   0
integration blocks:           1
initial implementation files: 0
unresolved TODO/TBD/___:       0
git diff --check:              PASS
backend porcelain:             EMPTY
frontend porcelain:            EMPTY
deployment record files:       ALL THREE ABSENT
```

The only unchecked boxes are the ten future I101 assessment members and the
ten inherited V1–V4/H1–H6 execution/handoff members. Every one has a literal
evidence destination; none is an authoring-readiness item or an execution
claim.

The lint independently recomputed all four path-set digests, both coverage
digests, the 13-member allowlist digest and the empty-set digest byte-equal to
S1. It found one unique `subwindow_id`, `KI-W8-I101`; no leaf write path,
wildcard owner, directory owner, second assessment, parallel wave, unresolved
ID or design choice exists.

Adversarial authoring controls passed:

1. adding any implementation member makes the empty-set oracle fail;
2. removing I101 or one P/T/V/H trace makes mapping closure fail;
3. removing, duplicating, skipping or failing to activate one required case
   makes the certificate validator fail before set conversion;
4. deleting one required forbidden-count member or substituting a fabricated
   LIVE-03 digest is rejected by NC-07/08;
5. granting a second workspace path, lower-level agent or direct leaf-parent
   channel fails scope/architecture lint; and
6. changing an ACT command, replaying after an observable AWS effect, or using
   sandbox escalation as AWS authority fails the frozen transition rules.

No execution gate or external operation was needed or performed to obtain this
authoring evidence.

## `SUBWINDOW-DECOMPOSITION-READY` — parent-review certificate

```yaml
certificate: SUBWINDOW-DECOMPOSITION-READY
parent_window_id: KI-W8
parent_assignment_id: ASG-KI-W8-WA-02
window_agent_identity: /root/ki_w8_aws_decomposition
revisions:
  parent_standard: cda352017e75c0d11f6797d9fbe108b4365508cd38b0e92365cfb523ede32848
  subwindow_standard: 842c29550c06c22d63e0a058a27cb8a9ff6b538b3168d2c83a384890b44247f0
  contract: 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c
  decision: d65cd9b128170de778a2d1492ef8347c5d2a988b8c3c7737f4a36b740531515a
  parent_checklist: b6cf79dd8fbe925101dd2c618c01ee1072f6df30c4653ea3c45c2660e6f0126b
  decomposition: a204d89a2909265392336d1cd78a89bdcfdf207fd5bc1f30a2a52c0543518d79
initial_subwindow_ids: []
initial_subwindow_count: 0
planned_file_set: []
planned_file_set_digest: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
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
first_subwindow: KI-W8-I101
integration_assessment_id: KI-W8-I101
parent_review_required: true
```

The window agent stops here. It has not assigned or executed I101, P1–P6,
ACT-01, ACT-02 or KI-W9.

## `EV-KI-W8-AWS-S004` — DECOMP-2 authority and parent-return reconciliation

**Outcome:** `PASS`.  
**Supersedes:** the rejected DECOMP-1 readiness certificate above; its evidence
is retained unchanged as history and grants no execution authority.

Parent review `EV-KI-A-130` and `CHG-KI-099` were reproduced read-only. The
operative pins are A5 state 205, A3
`9dfbe47b16200a3dae4480068f86eb845543244c5e45b38ac42ee0cf4568c3f6`
and A4
`5f056307a779a413406f5a4f0e7e87dac8dc12703d5633ec7f00d077d6a036b6`.
Both authoring standards, A1/A2/A8 and the accepted W7 local source/package
pins remain byte-equal to DECOMP-1.

The corrected future execution write set has exactly nine members: A5, A6,
S2, S3 and the five generated measurement/deployment records. S2/S3 occur once
and have no second subordinate owner. Its sorted-member-LF digest is
`b19c0f7e5daae79e0d373432c4315aeff4e5236156b3b326ecc2d17174410ccb`.
The current S1–S3 authoring set remains digest
`92afa898a46252737c52e5be698ebc65c197cd5862294b59a5998c8fe46565b3`;
the union of the execution set and immutable/read-only S1 is ten members,
digest `775f9083d0cfc21609f6c6f1c8ba3c6e99619916cf25afb4e9b340995faa482b`.
The implementation changed-file set remains empty, digest
`e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855`.

DECOMP-2 entry had the seven parent-owned authority paths plus S1–S3, exact set
digest `775f9083…482b`; backend and frontend porcelains were empty. Rejected
DECOMP-1 baselines were S1 `a204d89a…3518d79`, S2 `5da9d75b…f97a8c`, S3
`bfff7ee1…657279`. No historical W8 package byte changed.

## `EV-KI-W8-AWS-S005` — DECOMP-2 decision/execution closure

**Outcome:** `PASS`.

The revised S1 resolves all seven parent-return requirements:

1. S1 is immutable/read-only after approval; the only future writable
   workspace set is the exact nine-member parent execution set.
2. Account, account-bearing bucket/ARN/URL, object VersionIds and ChangeSetId
   remain only in process memory or the mode-0600 ignored records. Tracked
   state/evidence use SHA-256, presence/cardinality and account last4; the exact
   packet approval token remains the action fence.
3. P2 has literal captured-pipe S3 reads and exact versioning, AES256,
   four-public-block, BucketOwnerEnforced and sole seven-day incomplete-
   multipart lifecycle oracles.
4. One byte-frozen executable runner replaces every prose-only projector,
   record validator, scope validator, certificate validator and control runner.
   Its source SHA-256 is
   `c11dccd82185384a36751585c77cc734341e38bab86cde4bf75761aed4384afc`.
5. Stack resources accept exactly `CREATE_COMPLETE|UPDATE_COMPLETE`; every
   other status rejects.
6. P1 invokes exact local `node --version`/`aws --version` checks for v24/v2.
   ACT ambiguity uses a pre-action event watermark, exactly 12 captured
   read-only polls at five-second intervals, zero-effect rules over all 12,
   last-two-identical partial continuation, wait-without-reexecute and
   fail-closed unequal/unclassified branches.
7. Every phase bootstraps the runner afresh, captures raw AWS JSON only in
   process memory, pipes raw script stdout directly into a sanitizer, records
   only sanitized digests and removes its exact `/tmp/ki-w8-i101.*` directory.

The frozen runner has literal modes for version, P2/bucket, quota, strict
private-record schemas/modes, state-hash pins, path scope, packet/action/
inspector sanitization, pre-controls, final certificate/controls, event
watermark/observations/classification/wait, post-inspection output hashing and
owned cleanup. NC-01–08 each use unchanged
positive→single-mutant-rejects→fresh-positive mechanics; NC-02 imports the real
production `assertReviewedChanges`. Certificate validation rejects raw
duplicates before set equality and recomputes both member-LF digests.

Graph/allocation remains zero leaves plus sequential window-agent assessment
`KI-W8-I101`. Unmapped requirements, decisions, tasks, scenarios, cases and
controls are `0/0/0/0/0/0`. Multi-file sub-windows and duplicate owners are
`0/0`. Unresolved interfaces, intermediate states, execution choices and
evidence references are `0/0/0/0`.

## `EV-KI-W8-AWS-S006` — DECOMP-2 executable/static/adversarial lint

**Outcome:** `PASS`.

Read-only authoring checks produced:

```text
S1 mandatory SW-* IDs equal the standard's exact set: 47/47
unchecked mandatory SW-* IDs: 0
duplicate mandatory SW-* IDs: 0
implementation FILE/CORRECTION blocks: 0
integration assessment blocks: 1 (KI-W8-I101)
unresolved TODO/TBD/___ placeholders: 0
runner extraction count: 1
runner node --check: PASS
runner selftest: KIW8_RUNNER_SELFTEST_OK
runner source SHA-256: c11dccd82185384a36751585c77cc734341e38bab86cde4bf75761aed4384afc
case digest: 3bd44b2c2c244b1dd29881dcfa249d9cdad5f9b1aecc981c56612d587283ca7e
control digest: 9bd004917f960abb4842ea2f2da48ed60821fdedd55fcbc54dc7bdd271037ea6
execution path digest: b19c0f7e5daae79e0d373432c4315aeff4e5236156b3b326ecc2d17174410ccb
authoring path digest: 92afa898a46252737c52e5be698ebc65c197cd5862294b59a5998c8fe46565b3
path union digest: 775f9083d0cfc21609f6c6f1c8ba3c6e99619916cf25afb4e9b340995faa482b
git diff --check: PASS
backend porcelain: EMPTY
frontend porcelain: EMPTY
```

Static falsification proves that removing one exact execution path, duplicating
S2/S3 ownership, changing one case/control member, weakening one all-zero
forbidden key, deleting the raw-duplicate check, accepting a third resource
status, removing one bucket-safety member, changing one poll count/interval,
retaining one raw identity, or changing one runner byte makes readiness fail.
No P1–P6, build, measurement, database, browser, local-server, network,
provider, AWS, production, paid, destructive, leaf, subagent, commit, push or
KI-W9 action ran; cost `$0.00`.

## `SUBWINDOW-DECOMPOSITION-READY` — DECOMP-2 superseding certificate

```yaml
certificate: SUBWINDOW-DECOMPOSITION-READY
parent_window_id: KI-W8
parent_assignment_id: ASG-KI-W8-WA-02
window_agent_identity: /root/ki_w8_aws_decomposition
revisions:
  parent_standard: cda352017e75c0d11f6797d9fbe108b4365508cd38b0e92365cfb523ede32848
  subwindow_standard: 842c29550c06c22d63e0a058a27cb8a9ff6b538b3168d2c83a384890b44247f0
  contract: 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c
  decision: 9dfbe47b16200a3dae4480068f86eb845543244c5e45b38ac42ee0cf4568c3f6
  parent_checklist: 5f056307a779a413406f5a4f0e7e87dac8dc12703d5633ec7f00d077d6a036b6
  decomposition: 7c191e21e5de02d07ab294692a32a594f71a8dcbc9fbea4af6156a64881282f7
initial_subwindow_ids: []
initial_subwindow_count: 0
planned_file_set: []
planned_file_set_digest: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
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
first_subwindow: KI-W8-I101
integration_assessment_id: KI-W8-I101
parent_review_required: true
```

DECOMP-2 stops at `AWAITING_PARENT_DECOMPOSITION_REVIEW`. I101, P1–P6,
ACT-01, ACT-02 and KI-W9 remain unassigned/unexecuted.

## `EV-KI-W8-AWS-S007` — DECOMP-3 authority and quota reconciliation

**Outcome:** `PASS`.  
**Supersedes:** rejected DECOMP-2 readiness claims for execution; DECOMP-1 and
DECOMP-2 remain immutable authoring history and grant no execution authority.

The parent returned DECOMP-2 with exactly F1–F3. The operative authority is
unchanged: A5 state 205 at
`61a795bd198c6e91e7b51bfe3d768c3a9f1cb0dec0065ca184876c6d041e2987`,
A3 at `9dfbe47b16200a3dae4480068f86eb845543244c5e45b38ac42ee0cf4568c3f6`
and A4 at `5f056307a779a413406f5a4f0e7e87dac8dc12703d5633ec7f00d077d6a036b6`.
The two standards and remaining A1–A8 pins remain unchanged from DECOMP-2.

F1 is resolved without expanding AWS reads. A4 literally enumerates
CloudFormation `list-service-quotas` but does not enumerate
`describe-account-limits` or define an account-applied concurrent-resource
threshold. The runner therefore retains the CloudFormation quota response only
as validated/sorted sanitized inventory. It no longer interprets Service
Quotas code `L-0485CB21` as a resource limit. Capability is proved by the exact
template counts against CloudFormation's fixed per-template limits: resources
`82 <= 500`, outputs `34 <= 200`, parameters `19 <= 200`. Lambda account/code
storage checks and SQS/template property checks remain unchanged.

The file graph and authority are unchanged: zero implementation leaves, one
window-agent-owned sequential I101, exact nine-path future execution set digest
`b19c0f7e5daae79e0d373432c4315aeff4e5236156b3b326ecc2d17174410ccb`,
empty implementation set digest
`e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855`,
and no duplicate owner.

## `EV-KI-W8-AWS-S008` — DECOMP-3 ACT-01 fidelity and stack fences

**Outcome:** `PASS`.

F2 is resolved by calling the accepted exported production
`assertReviewedChanges("full", described)` on the unprojected live
`describe-change-set` response. `ResourceChange.Details` remains in process
memory through that call. Only its accepted normalized projection hash is then
retained. Runner selftest passes the exact two optional dependency-detail
contracts and proves a wrong `RecoverySchedule` causing entity rejects through
the same production guard. The prior projection-before-validation path no
longer exists.

F3 is resolved in one pure ACT-01 classifier used by execution and selftest:

- zero effect requires all 12 observations to have stack status exactly
  `CREATE_COMPLETE|UPDATE_COMPLETE`, three classified-absent objects, absent
  deterministic change set and no post-watermark event;
- partial continuation requires the final two byte-identical observations both
  have accepted-complete stack status, exact-or-absent object classification,
  at least one exact present object, absent change set and no event;
- complete reconciliation requires the final accepted-complete stack status,
  no event, three exact objects, `CREATE_COMPLETE/AVAILABLE` remotely reviewed
  change set, and exact mode-0600 local record ID/projection reconciliation.

Any failed/in-progress status in the applicable observations yields only
`PARENT_BLOCKED_ACT01_AMBIGUOUS`. Selftest separately changes the zero,
partial, and complete fixtures to `UPDATE_IN_PROGRESS` and
`UPDATE_ROLLBACK_COMPLETE`; all six branch/status mutants reject. Existing
ACT-02 fail-closed behavior remains unchanged.

Unmapped requirements, decisions, tasks, scenarios, cases and controls remain
`0/0/0/0/0/0`. Unresolved interfaces, intermediate states, execution choices
and evidence references remain `0/0/0/0`.

## `EV-KI-W8-AWS-S009` — DECOMP-3 executable/static/adversarial lint

**Outcome:** `PASS`.

Read-only authoring checks produced:

```text
S1 SHA-256: d68d8f72e3e830481ace6aa9f489abcb57dad79a7ab503a7d11d3970a5b9fba9
S2 state 3 SHA-256 before this append: 4c871820110e4042735ef54064e145490274b59fe4ad434bf021bb3c4dcab770
runner extraction count: 1
runner SHA-256: 70b636fb06af162c1325247110fdc52beb122d54a7abba327a7f6ce02fedea03
runner node --check: PASS
runner selftest: KIW8_RUNNER_SELFTEST_OK
mandatory SW-* IDs: 47/47 unique
unchecked mandatory SW-* IDs: 0
DECOMP3_STATIC_LINT_PASS
DECOMP3_ADVERSARIAL_LINT_PASS positive=1 negative=8
git diff --check: PASS
backend porcelain: EMPTY
frontend porcelain: EMPTY
```

The eight authoring mutants reintroduce the false quota, weaken one fixed
limit, bypass the exported live guard, remove the optional-detail negative
control, or remove the zero/partial/complete stack fences/status controls. Each
causes readiness lint to fail. The runner itself also executes the dependency
detail and six stack-status negative controls during selftest.

No P1–P6, I101, build, measurement, database, browser, local-server, network,
provider, AWS, production, paid, destructive, leaf, subagent, commit, push or
KI-W9 action ran; cost `$0.00`.

## `SUBWINDOW-DECOMPOSITION-READY` — DECOMP-3 superseding certificate

```yaml
certificate: SUBWINDOW-DECOMPOSITION-READY
package: KI-W8-AWS-ONLY-DECOMP-3
supersedes_package: KI-W8-AWS-ONLY-DECOMP-2
parent_window_id: KI-W8
parent_assignment_id: ASG-KI-W8-WA-02
window_agent_identity: /root/ki_w8_aws_decomposition
revisions:
  parent_standard: cda352017e75c0d11f6797d9fbe108b4365508cd38b0e92365cfb523ede32848
  subwindow_standard: 842c29550c06c22d63e0a058a27cb8a9ff6b538b3168d2c83a384890b44247f0
  contract: 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c
  decision: 9dfbe47b16200a3dae4480068f86eb845543244c5e45b38ac42ee0cf4568c3f6
  parent_checklist: 5f056307a779a413406f5a4f0e7e87dac8dc12703d5633ec7f00d077d6a036b6
  decomposition: d68d8f72e3e830481ace6aa9f489abcb57dad79a7ab503a7d11d3970a5b9fba9
  runner: 70b636fb06af162c1325247110fdc52beb122d54a7abba327a7f6ce02fedea03
initial_subwindow_ids: []
initial_subwindow_count: 0
planned_file_set: []
planned_file_set_digest: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
future_execution_path_count: 9
future_execution_path_digest: b19c0f7e5daae79e0d373432c4315aeff4e5236156b3b326ecc2d17174410ccb
unmapped_parent_requirements: []
unmapped_parent_decisions: []
unmapped_parent_tasks: []
unmapped_parent_scenarios: []
unmapped_coverage_cases: []
unmapped_controls: []
duplicate_initial_file_owners: []
multi_file_subwindows: []
unresolved_interfaces: []
unresolved_intermediate_states: []
unresolved_execution_choices: []
unresolved_evidence_references: []
mandatory_authoring_items_checked: 47
mandatory_authoring_items_unchecked: 0
first_subwindow: KI-W8-I101
integration_assessment_id: KI-W8-I101
parent_review_required: true
```

DECOMP-3 stops at `AWAITING_PARENT_DECOMPOSITION_REVIEW`. I101, P1–P6,
ACT-01, ACT-02 and KI-W9 remain unassigned and unexecuted.

## `EV-KI-W8-AWS-S010` — parent acceptance and P1–P6 assignment

**Outcome:** `READY`.

The parent accepted immutable DECOMP-3 revision
`d68d8f72e3e830481ace6aa9f489abcb57dad79a7ab503a7d11d3970a5b9fba9`
and runner revision
`70b636fb06af162c1325247110fdc52beb122d54a7abba327a7f6ce02fedea03`.
A5 state 206, SHA-256
`0d494f2698133b84c636e8a238a7c10656b19a8f971c04e9a7840b6845cd650e`,
assigns `ASG-KI-W8-I101-01` only for P1–P6/G-W8-01. S2 advanced to state 4
`READY`. ACT-01/ACT-02, every AWS mutation and KI-W9 remain prohibited.

## `EV-KI-W8-AWS-S011` — I101 P1 pass; P2 external-prerequisite blocker

**Outcome:** `PARENT_BLOCKED`.

P1 passed before any AWS network read:

- frozen runner selftest and local version checks passed; Node is v24 and AWS
  CLI is v2;
- runner SHA-256 is
  `70b636fb06af162c1325247110fdc52beb122d54a7abba327a7f6ce02fedea03`;
- A5 state 206, A1/A2/A3/A4/A8, both standards, immutable S1, template, both
  ZIPs and all four accepted scripts matched their frozen hashes;
- template/ZIP bytes matched `104582/32006605/31984076`;
- root status contained only the ten protected coordination paths and both
  nested porcelains were empty.

The restricted P2 `sts get-caller-identity` transport failed before yielding a
usable result. Its one elevated recovery was itself environment-invalidated by
a login-shell home change; a non-login elevated transport restored the original
home and repeated the identical read-only P2 command. That attempt failed with
the same observable external prerequisite as a sanitized direct STS
classification:

```yaml
status: 255
profile_missing: false
expired_credentials: true
connectivity_failure: false
access_denied: false
stderr_sha256: 73c866bcbd5383b9013eff2236e8a5d55ed51bd7b1f472d1b620e1db4299b552
```

The first restricted stderr hash was
`d163746340e5e4100272392ffb5b88023dfe0db5eefcbe1ed26caf37e54ba530`;
no raw stderr, account, ARN, URL or credential was retained. P2 obtained no
identity/projection, so P3–P6 did not run and `W8-LIVE-01` was not activated.
Both measurement files remain at their entry hashes
`f16657513db36c198bf87a383179a80d28070535aa9d84389af229c3754930c3`
and `bd7a02cf1ae53ab68d19046da711bb115575237279e5b6fc622531d9df97c2b1`.
All three exact temporary directories were removed; no process remains.

No AWS mutation, object/change-set creation, provider/paid/database/API/browser/
local-server action, implementation edit, commit/push or KI-W9 action occurred;
cost `$0.00`. Resume requires refreshed valid credentials for the existing
`storesignal-dev` profile and a parent state returning I101 P1–P6 to READY.

## `EV-KI-W8-AWS-S012` — refreshed-credential P1–P6 reassignment

**Outcome:** `READY`.

The requester reported the existing `storesignal-dev` credentials refreshed.
The parent created A5 state 208, SHA-256
`bd8fe16cfc57f2bed883f25f4ef3dfe696e5c018338b001719eb1defd22c1b2d`,
and assignment `ASG-KI-W8-I101-02` for the identical immutable P1–P6/G-W8-01
sequence only. S2 advanced to state 6 `READY`. P2 must independently prove the
STS identity; the requester statement is not evidence. ACT-01/ACT-02, every AWS
mutation and KI-W9 remain prohibited.

## `EV-KI-W8-AWS-S013` — refreshed P2 reaches target; lifecycle normalization blocker

**Outcome:** `PARENT_BLOCKED`.

P1 passed again under assignment `ASG-KI-W8-I101-02`. P2 independently reached
the refreshed STS/CloudFormation/S3 target and advanced through the bucket
versioning, AES256 encryption, public-access and ownership checks. It then
failed at frozen code `KIW8_BUCKET_FILTER`.

One authorized sanitized read-only lifecycle query proved the exact existing
shape without retaining account/bucket identity:

```json
{"ruleCount":1,"rules":[{"id":"AbortIncompleteMultipartUploads","status":"Enabled","topLevelPrefix":null,"filterType":"object","filterKeys":["Prefix"],"filterPrefix":"","abortDays":7,"expirationPresent":false,"transitionsPresent":false,"noncurrentExpirationPresent":false,"noncurrentTransitionsPresent":false}]}
```

This is the accepted empty-prefix lifecycle normalized by AWS as
`Filter:{Prefix:""}`. DECOMP-3's immutable `validLifecycle` accepts only absent
filter or `{}` and therefore contradicts its own prose/A4 requirement to accept
an empty/absent filter/prefix. The mechanically exact correction is to accept
only these three filter forms: absent, `{}`, or exactly `{Prefix:""}`; all
other filter keys/nonempty prefixes still reject. No current authority permits
editing immutable S1, so P3–P6 did not run and `W8-LIVE-01` was not activated.

The exact temporary directory was removed. Measurement outputs remain
unchanged. No AWS mutation, ACT-01/02, provider/paid/database/API/browser/
local-server, implementation, commit/push or KI-W9 action occurred; cost
`$0.00`.

## `EV-KI-W8-AWS-S014` — requester-authorized parent takeover clears P1–P5

**Outcome:** `PASS_THROUGH_P5`.

The requester authorized `/root` to take over directly and clear P5. The
parent superseded only the faulty executor members:

- lifecycle validation now accepts absent filter, `{}`, or exactly
  `{Prefix:""}` and rejects nonempty prefixes, extra keys and arrays;
- Lambda account validation no longer invents nonexistent
  `AccountLimit.FunctionCount`; `AccountUsage.FunctionCount` is retained only
  as informational usage.

The corrected S1 and extracted runner revisions are respectively
`0f99913d69f573ce9df7a89bf1b05962f2fbd5cceb68ca3f5dbeb1f4d784e62d`
and `f2d21cdd9a9ff7c6dd2d0d4d26ec70592cecb8aaf44dab335241a2a383fb960e`.
Runner syntax and self-test passed, including all accepted/rejected lifecycle
representations.

P1–P5 then passed in exact order:

```yaml
p1: PASS
p2_projection_sha256: 4419b32a71c1993a839a13595c6fd8444389affa78c2c28e95534b03dba2755e
p3_projection_sha256: ef9748a94435ffefb0b2d41ceec23ed1b8d6883d1a42849f2a0656195ac54349
p4_packet_projection_sha256: dade137fe8274b48ed32441bf1e32be10f5f44673a8084174e59ca21a2c39bba
p5_projection_sha256: 4419b32a71c1993a839a13595c6fd8444389affa78c2c28e95534b03dba2755e
p2_p5_byte_equal: true
keyword_measurement_sha256: fd0c6232cee16ce3a43370928e06702412e70e2b73db9bec07e59297943c366c
established_measurement_sha256: 6168ddc070b96880d6793db7749bd2f497e177d553543710cd7fd21287d0c0b6
temp_cleanup: PASS
aws_mutations: 0
paid_cost_usd: 0.00
```

P2 verified the target stack and bucket safety; P3 verified applicable Lambda
account capacity, returned quota inventories and fixed template/package
bounds; P4 measured accepted packages and reproduced the dry-run packet; P5
repeated the complete read-only P2 projection byte-identically. No secret,
provider, database, API, browser, local-server, Lambda invoke, queue data-plane
or AWS mutation occurred. P6 was intentionally not run because the requester
corrected W8's terminal intent: there is no KI-W9, and W8 must be reauthored to
finish with active AWS infrastructure usable by the local application.

S2 state 8 and A5 state 212 stop at parent reauthoring with no external action
authority.

## `EV-KI-W8-AWS-S015` — DECOMP-5 P1–P6 pass; ACT-01 approval boundary

**Outcome:** `PASS_THROUGH_P6`.

The requester retained ACT-01 and changed only ACT-02's terminal behavior:
after the exact disabled intermediate update and inspection, ACT-02 reviews and
applies the already-supported exact activation set and requires expected-active
inspection. The parent recorded `DEC-KI-061`, retired the legacy ACT-05 label,
and assigned only read-only P1–P6 under A5 state 213.

The extracted runner revision
`4611115aa6c7fc3ae9448e44435051ad0e2abc6f85245f656613608bef5d47d0`
passed syntax/self-test. P1–P6 passed with projections:

```yaml
p2_initial_sha256: 4419b32a71c1993a839a13595c6fd8444389affa78c2c28e95534b03dba2755e
p3_sha256: ef9748a94435ffefb0b2d41ceec23ed1b8d6883d1a42849f2a0656195ac54349
p4_packet_sha256: dade137fe8274b48ed32441bf1e32be10f5f44673a8084174e59ca21a2c39bba
p5_recheck_sha256: 4419b32a71c1993a839a13595c6fd8444389affa78c2c28e95534b03dba2755e
p6_scope_sha256: 2f5e7d55ce5a18de0f9d5ada2a37da5a07843aa18df21bb31e41a0c3c0d6e442
p2_p5_byte_equal: true
keyword_measurement_sha256: 07217b5a05418c9790559c24b5cb07281e6edd9fa28dc6e4d5ac2d0237043447
established_measurement_sha256: 5286e288717283027316c43c5fe4ddc66471790b6bf3c4c230a91ad02c4572a6
aws_mutations: 0
paid_cost_usd: 0.00
```

No deployment, activation, Lambda invocation, queue data-plane, secret-value,
database, API, browser, local-server or provider action occurred. LIVE-01 is
accepted. The sole next operation is requester approval of unchanged ACT-01.

## `EV-KI-W8-AWS-S016` — requester-approved ACT-01 completed

**Outcome:** `PASS_AWAITING_ACT02_APPROVAL`.

Under A5 state 215 and assignment `ASG-KI-W8-ACT01-PARENT-01`, the frozen
runner revalidated the exact state pins and target before any write. The exact
three content-addressed artifact members reconciled to versioned AES256 S3
objects. Sanitized version hashes, in packet order, are:

```yaml
object_version_sha256s:
  - 73a3b542888e36bf77dc9bc38738ef60811e9733a50d46097951a99364ec1b6f
  - a7ddf54cca1ed60516a2017ed6d73afc3df222df8b68957f9985abd7e7c4ccd8
  - b57038b574321c2a467dd77344448b15b9f7d129c660dd9bc64b2bee07d7c859
```

The exact full-phase change set `ki-full-a62298d72baf` was created and reviewed
but not executed. Sanitized change-set ID hash is
`5a4e7c1d0c4dc456a59640a25753f68cea2bf39b3e47c7f5971d2f14d6f9127a`;
the exact normalized 15-change projection hash is
`55a6dcf69ca72fb4004facc422c5677723aa50a0e8daecd6d1300a1eaac19649`.
The sanitizer, strict private-record reconciliation and both ACT-01 negative
controls passed. Sanitized output hashes are:

```yaml
sanitize_act01_sha256: 05a273ff878addc3e8238a2411efc93dd7d389753424761413732ab978b73e1e
records_sanitized_sha256: 2a6c0a26bb0bdaea94c0faafb6eefac382de9e8e83d572e62f1e0a4b53930ff6
pre_control_result_sha256: dc271ffd74845b46a8c86e4430c181fdf261a1ee2573a9ebaad6deb5eab1cd03
p2_act02_sha256: 2292fb4a3079ae29b3fe00e7a4bb835168dae09bd5efce123aec988d9a433619
falsified_controls: [W8-NC-01, W8-NC-02]
```

No CloudFormation execution, stack update, activation, Lambda invocation,
queue data-plane operation, secret-value read, provider/paid call, database,
API, browser, local-server, commit, push or successor action occurred. Cost was
`$0.00`. LIVE-02 is accepted; ACT-02 still requires separate requester approval.
