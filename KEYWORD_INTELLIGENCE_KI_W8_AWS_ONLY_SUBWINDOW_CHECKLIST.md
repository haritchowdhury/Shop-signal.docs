# KI-W8 AWS-Only Sub-Window Decomposition Checklist (`S1`)

**Decomposition ID:** `KI-W8-AWS-ONLY-DECOMP-5`
**Parent window:** `KI-W8`  
**Parent assignment:** `ASG-KI-W8-WA-02`  
**Window agent:** `/root/ki_w8_aws_decomposition`  
**Status:** `PARENT-DIRECT-ACTIVE-PREFLIGHT`

This is the revised subordinate decomposition authority for the AWS-only KI-W8
deployment with a disabled intermediate state and active terminal state. It
supersedes no bytes in the historical
`KEYWORD_INTELLIGENCE_KI_W8_SUBWINDOW_*` package and derives no authority from
that package. Live subordinate state exists only in
`KEYWORD_INTELLIGENCE_KI_W8_AWS_ONLY_SUBWINDOW_STATE.md` (`S2`); append-only
decomposition, execution, review and assessment evidence exists only in
`KEYWORD_INTELLIGENCE_KI_W8_AWS_ONLY_SUBWINDOW_EVIDENCE.md` (`S3`).

`KI-W8-AWS-ONLY-DECOMP-1` and `KI-W8-AWS-ONLY-DECOMP-2` remain rejected
authoring history in S3. `KI-W8-AWS-ONLY-DECOMP-3` is superseded only because
its lifecycle validator omitted AWS's accepted normalized empty filter
`{Prefix:""}`. `KI-W8-AWS-ONLY-DECOMP-4` is superseded by the
requester-directed ACT-02 active-terminal decision. None grants execution
authority. KI-W8 has no delegated implementation leaves; the parent made the
one-line deployment-guard action-label correction directly. After parent approval and
a new execution assignment, the same window agent personally executes the one
sequential assessment `KI-W8-I101`. No lower-level agent or subagent is used.

## 0. Inherited authority and revision pins

| Authority | Path | Lowercase SHA-256 |
|---|---|---|
| Parent standard | `PROJECT_AGNOSTIC_DECISION_COMPLETE_CHECKLIST_AUTHORING_STANDARD.md` | `cda352017e75c0d11f6797d9fbe108b4365508cd38b0e92365cfb523ede32848` |
| Sub-window standard | `PROJECT_AGNOSTIC_WINDOW_AGENT_SUBWINDOW_AUTHORING_STANDARD.md` | `842c29550c06c22d63e0a058a27cb8a9ff6b538b3168d2c83a384890b44247f0` |
| `A1` contract | `KEYWORD_INTELLIGENCE_PRODUCT_CONTRACT.md` | `8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c` |
| `A2` discovery | `KEYWORD_INTELLIGENCE_DISCOVERY_DOSSIER.md` | `3a6b294cc561556d0e3d92572121bc8cc529470866fba5bad8f78cf816310470` |
| `A3` decisions | `KEYWORD_INTELLIGENCE_DECISION_LEDGER.md` | `32ae437a3c755d370e6d78ff4ba33badec0fec504f2045339303c3c9e9ee044e` |
| `A4` checklist | `KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md` | `25c33528a7a2059aedb0ed850de8e83b49ca5a08b02ee8d2f64621090780e1a6` |
| `A5` state v205 | `ACTIVE_EXECUTION_STATE.md` | `61a795bd198c6e91e7b51bfe3d768c3a9f1cb0dec0065ca184876c6d041e2987` |
| `A6` evidence | `KEYWORD_INTELLIGENCE_EXECUTION_EVIDENCE.md` | `095dc473f1b14d65c7f2a14fbb0ce515eeb77cace9ae07ed33c89fcbfa0f1406` |
| `A7` changelog | `KEYWORD_INTELLIGENCE_SPECIFICATION_CHANGELOG.md` | `ba7d3831cf5737382fd32045b725dad718f65e7b79bfe0fa01dfa10a1bd7c6b2` |
| `A8` traceability | `KEYWORD_INTELLIGENCE_TRACEABILITY_INDEX.md` | `e89fe868823ba97a3c8877d79055bbc85d2593353add13c32b8a6c35a51e7d4b` |

The current assignment authorizes only creation of `S1`–`S3`, static/read-only
authoring checks and parent handoff. It authorizes no preflight command in
Section 6, no measurement, network, AWS, deployment, provider, database,
browser, local-server, paid, destructive, commit, push, leaf-dispatch or successor
action.

### 0.1 Mechanical interpretations fixed by this decomposition

1. The initial implementation-file set and initial sub-window set are both
   empty. Their set digest is the SHA-256 of zero bytes,
   `e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855`.
2. `KI-W8-I101` is an `INTEGRATION_ASSESSMENT`, is never delegated, and owns
   zero implementation-file writes. After approval S1 is immutable/read-only.
   I101 may update only the nine execution paths explicitly listed in Section
   1 after a later A5 assignment names them; S2/S3 occur once in that set and
   have no second subordinate owner.
3. Parent approval of this decomposition does not authorize I101. S2 remains a
   fail-closed `STOP` sentinel until the parent creates a later execution
   assignment. That assignment initially authorizes only P1–P6. ACT-01 and
   ACT-02 are separately requester-approved A5 states.
4. The controls count is eight. The phrase `four/two registry` in the
   `SCN-KI-049` activation-witness sentence is interpreted only as four cases
   and two action-ledger members; the authoritative control table, JSON schema,
   `DEC-KI-060`, A8 and digests all require eight controls.
5. The two measurement scripts deliberately overwrite only
   `email_scraper/dist/lambda/keyword-worker-measurements.json` and
   `email_scraper/dist/lambda/measurements.json`. `EV-KI-A-129` and A4 revision
   current A4 revision `5f056307…` explicitly authorize those generated
   outputs for execution.
6. Applied account, bucket/ARN/URL, object-version and change-set identities are
   observed facts and never executor choices. Exact values may exist only in
   process memory and the mode-0600 ignored deployment records. A5, A6 and S3
   store only `{present:true,sha256:<64hex>}`, presence/cardinality and account
   last four. Consumers re-hash the in-memory or private-record value before
   use. The packet `approvalToken` is the sole exact remote-action token kept in
   A5 because the accepted script requires it.
7. Raw AWS stdout/stderr never reaches retained terminal/evidence output. The
   frozen validator invokes AWS with captured pipes, parses raw JSON in process
   memory, emits only the sanitized projections frozen below, and hashes any
   diagnostic stderr. Exact raw identities written by the deployment script
   remain only in its three ignored mode-0600 records. Secret values are never
   read.
8. A remote mutation whose result cannot be reconciled exactly is a
   `PARENT_BLOCKED` result, not permission to retry, create a replacement,
   repair manually or continue.

### 0.2 Inherited execution-environment policy

Sandbox escalation is standing-authorized only for an already-authorized local
command. After a restricted attempt is proven invalidated solely by sandbox
denial or execution-channel loss, one identical escalated recovery is allowed
only after read-only postconditions prove no surviving process, workspace
mutation, AWS mutation, paid operation or usable result. Arguments,
environment, timeout, selection, oracle and action scope remain byte-identical.
An observable assertion/AWS failure or any surviving AWS effect is not an E8.1
invalidation. Escalation never grants AWS authority.

## 1. Parent scope copied without expansion

### 1.1 Objective, successor and exclusions

- **Objective:** preflight the exact production AWS target, deploy the accepted
  W7 keyword infrastructure and two ZIPs through a verified disabled
  intermediate state, apply the exact activation set, inspect the active stack,
  and stop without creating work.
- **Successor:** `STOP_KI-W8_COMPLETE`, reserved for the parent;
  `may_start_successor:false`.
- **Excluded:** hosted/local backend or frontend configuration, local server,
  authentication, secret-value read, research/API call, browser, Neon,
  provider/paid call, activation outside exact ACT-02, direct Lambda invocation, queue data-plane
  operation, DLQ action, rollback mutation, purge/delete/redrive/manual repair,
  source/test/schema/migration/package/lock/frontend edit other than the
  parent-approved deployment action-label correction, commit/push and any
  successor window.

### 1.2 Exact path scopes

The initial implementation-file set is empty. After parent approval S1 is
immutable/read-only. The parent-authorized W8 execution-write set is exactly:

```text
ACTIVE_EXECUTION_STATE.md
KEYWORD_INTELLIGENCE_EXECUTION_EVIDENCE.md
KEYWORD_INTELLIGENCE_KI_W8_AWS_ONLY_SUBWINDOW_EVIDENCE.md
KEYWORD_INTELLIGENCE_KI_W8_AWS_ONLY_SUBWINDOW_STATE.md
email_scraper/dist/aws-deployment/keyword-intelligence/artifacts.json
email_scraper/dist/aws-deployment/keyword-intelligence/activate-change-set.json
email_scraper/dist/aws-deployment/keyword-intelligence/full-change-set.json
email_scraper/dist/aws-deployment/keyword-intelligence/packet.json
email_scraper/dist/lambda/keyword-worker-measurements.json
email_scraper/dist/lambda/measurements.json
```

It has ten members and sorted-member-LF digest
`c0ae7c02ba529c538d22ae831637abbc199b53836428ec79f13fd844604057f9`.
S2 and S3 have exactly this one execution owner; they are not added again by a
subordinate scope. The current decomposition-authoring set remains exactly S1,
S2 and S3, digest
`92afa898a46252737c52e5be698ebc65c197cd5862294b59a5998c8fe46565b3`.
The union of the ten execution paths and immutable S1 has eleven members; its
digest is recomputed by the frozen scope oracle.
No other workspace path may be created, modified or deleted by I101. Temporary
validator material exists only below a `mktemp -d /tmp/ki-w8-i101.XXXXXX`
directory, mode 0700, contains no raw remote identity, and is removed after its
sanitized digest is retained.

The exact read-only source set is the two standards, A1–A8, immutable S1, S2/S3, the four
accepted W7 source/script files below, the accepted template and two ZIPs, and
the AWS read surfaces and returned identities enumerated in Section 6. No
directory/glob grants write authority.

### 1.3 External action scope

| Action | Authorized effect | Explicitly absent effect |
|---|---|---|
| `W8-ACT-01` | up to three exact content-addressed AES256/versioned `PutObject` operations and one exact disabled CloudFormation change-set create/review; never execute | activation, queue traffic, Lambda invocation, secret/provider/database access |
| `W8-ACT-02` | execute the exact ACT-01 full ID, require expected-disabled inspection, create/review/apply the deterministic exact activation set, then require expected-active inspection | manual repair, rollback mutation, unlisted change set, direct invocation, submitted queue traffic |

Read-only P1–P6 and post-action reconciliation are not mutations but still need
a later A5 execution assignment. ACT-01 and ACT-02 each require a new requester
approval reflected in A5. ACT-02 is one approval covering both exact
CloudFormation transactions in its sequence; it does not authorize application
work.

## 2. Starting working-tree and artifact inventory

Recorded in `EV-KI-W8-AWS-S007`:

- coordination root HEAD `8a235e858888cbd0ea21a26520493cda72ba1a23`;
  at DECOMP-2 entry exactly seven parent-owned modified authority paths plus
  the three DECOMP-1 S1–S3 paths, set digest
  `775f9083d0cfc21609f6c6f1c8ba3c6e99619916cf25afb4e9b340995faa482b`;
- backend HEAD `4f9d6ce079d7fcd93d8a034b0592d4cdc1522f02`, porcelain empty;
- frontend HEAD `5e441aae7e2f3a132b2c7fc85bf1bc525d3d5cb6`, porcelain empty;
- rejected DECOMP-1 baselines: S1 `a204d89a…3518d79`, S2
  `5da9d75b…f97a8c`, S3 `bfff7ee1…657279`; and
- the historical `KEYWORD_INTELLIGENCE_KI_W8_SUBWINDOW_*` files are protected
  read-only history.

| File | Entry digest/status | Execution rule |
|---|---|---|
| `email_scraper/dist/lambda/keyword-worker-measurements.json` | `f16657513db36c198bf87a383179a80d28070535aa9d84389af229c3754930c3`, 7,596 bytes | P4 may overwrite once |
| `email_scraper/dist/lambda/measurements.json` | `bd7a02cf1ae53ab68d19046da711bb115575237279e5b6fc622531d9df97c2b1`, 52,882 bytes | P4 may overwrite once |
| `email_scraper/dist/aws-deployment/keyword-intelligence/packet.json` | `ABSENT` | ACT-01 creates |
| `email_scraper/dist/aws-deployment/keyword-intelligence/artifacts.json` | `ABSENT` | ACT-01 creates |
| `email_scraper/dist/aws-deployment/keyword-intelligence/full-change-set.json` | `ABSENT` | ACT-01 creates |
| `email_scraper/dist/aws-deployment/keyword-intelligence/activate-change-set.json` | `ABSENT` | ACT-02 creates only after disabled inspection passes |

## 3. Frozen inputs, identities and boundary contracts

### 3.1 Accepted local bytes

| Member | Bytes | SHA-256 |
|---|---:|---|
| `email_scraper/infrastructure/aws/template.yaml` | `104582` | `2d87c28ad564842d13e42855aef676fb30b2f3aa357ef6eda73bc88f67cb8fa8` |
| `email_scraper/dist/lambda/keyword-worker.zip` | `32006605` | `47fda36e621bcb35a98fd1614854dadc0231e70871cf5488828610400d8460d4` |
| `email_scraper/dist/lambda/recovery.zip` | `31984076` | `cc5b6819d80c85a3ca74f05c9887b580aa8dd498f1f866ffc8e812ce89f2bb9c` |
| `email_scraper/scripts/measure-keyword-worker-package.js` | bytes pinned by adjacent SHA-256 | `e3c54db213b57af5a30d2475645186db9a138b00a1488f2299085aac4ce68494` |
| `email_scraper/scripts/measure-lambda-packages.js` | bytes pinned by adjacent SHA-256 | `b33318a78a6e6a0e25264fdc908c5185098d1188ef88e848e17fb9d85423f194` |
| `email_scraper/scripts/keyword-intelligence/create-change-set.js` | bytes pinned by adjacent SHA-256 | `54d82520988cae11edae7593ab2ad5ed1c5049be4601fb90282abdc23339342e` |
| `email_scraper/scripts/keyword-intelligence/inspect-stack.js` | bytes pinned by adjacent SHA-256 | `47ad3e90ac91f51d7d91292618828dd51e88d011bf53ce7625b8adb93c540496` |

Any byte/size drift before its consuming phase invalidates that phase and every
later phase. It does not authorize rebuilding or editing.

### 3.2 Packet and object identity

The exact target literals are profile `storesignal-dev`, region `ap-south-2`,
stack `storesignal-production-pipeline`, environment `production`, phase
`full`, and one P2-observed 12-digit `accountId`.

The packet is exactly:

```text
contractVersion = "storesignal-keyword-deployment-v1"
profile = "storesignal-dev"
accountId = the one P2-observed 12-digit account
region = "ap-south-2"
stack = "storesignal-production-pipeline"
environment = "production"
bucket = "storesignal-prod-pipeline-" + accountId + "-ap-south-2"
template = {basename:"cloudformation-template.json", source:"infrastructure/aws/template.yaml", bytes, sha256, key}
zips[0] = {logicalId:"KeywordWorker", basename:"keyword-worker.zip", source:"dist/lambda/keyword-worker.zip", bytes, sha256, key}
zips[1] = {logicalId:"Recovery", basename:"recovery.zip", source:"dist/lambda/recovery.zip", bytes, sha256, key}
key = "deployment/" + sha256 + "/" + basename
approvalToken = sha256(canonical(packet without approvalToken))
```

`canonical` recursively preserves array order, sorts object keys by the source
JavaScript ordering used by `Array.prototype.sort()`, renders object members as
`JSON.stringify(key)+":"+canonical(value)`, and uses `JSON.stringify` for
scalars. The change-set name is exactly
`ki-full-${approvalToken.slice(0,12)}`.

Every upload request computes and supplies the base64 SHA-256 checksum of the
exact source bytes and content type `application/json` for the template or
`application/zip` for a ZIP. Every confirmed object must have the exact key and
byte length above, metadata `sha256=<hex>`, `ServerSideEncryption:AES256`, and a
nonempty `VersionId`. An existing key is accepted only when the script's
head-object conflict guard confirms exact metadata/bytes/encryption/version; a
different member is `PARENT_BLOCKED_OBJECT_CONFLICT`.

The three private local records have these exact key sets and array order; no
extra/missing member is accepted:

```text
packet.json = {
  contractVersion, profile, accountId, region, stack, environment, bucket,
  template, zips:[KeywordWorker, Recovery], approvalToken
}
artifacts.json = {
  contractVersion:"storesignal-keyword-artifacts-v1", approvalToken,
  accountId, region, stack, bucket,
  template:{...packet.template,versionId},
  zips:[{...packet.zips[0],versionId},{...packet.zips[1],versionId}]
}
full-change-set.json = {
  contractVersion:"storesignal-keyword-change-set-v1", approvalToken,
  phase:"full", changeSetName, changeSetId,
  changes:[{action,logicalId,type,replacement}, ...] sorted by logicalId
}
```

The frozen runner's executable `records` mode checks those exact scalars, object-member sets,
two-element ZIP order, source-member equality, nonempty opaque version/ID
members and the normalized-change allowlist before use. File mode is exactly
0600.

### 3.3 Disabled change-set allowlist

The direct projection is exactly these 13 members (member-set digest
`f1200139c3ceae903f0443d7c2c2ca134ba44f1192d7d98be10fddc4a3422b90`):

| Action | Logical ID | Type | Replacement |
|---|---|---|---|
| Add | `KeywordResearchDlq` | `AWS::SQS::Queue` | `null` |
| Add | `KeywordResearchQueue` | `AWS::SQS::Queue` | `null` |
| Add | `KeywordWorkerLogGroup` | `AWS::Logs::LogGroup` | `null` |
| Add | `KeywordWorkerRole` | `AWS::IAM::Role` | `null` |
| Add | `KeywordWorker` | `AWS::Lambda::Function` | `null` |
| Add | `KeywordResearchMapping` | `AWS::Lambda::EventSourceMapping` | `null` |
| Add | `KeywordResearchDlqDepthAlarm` | `AWS::CloudWatch::Alarm` | `null` |
| Add | `KeywordResearchOldestMessageAlarm` | `AWS::CloudWatch::Alarm` | `null` |
| Add | `KeywordWorkerErrorsAlarm` | `AWS::CloudWatch::Alarm` | `null` |
| Add | `KeywordWorkerThrottlesAlarm` | `AWS::CloudWatch::Alarm` | `null` |
| Modify | `ControlPlanePolicy` | `AWS::IAM::ManagedPolicy` | `False` |
| Modify | `RecoveryRole` | `AWS::IAM::Role` | `False` |
| Modify | `Recovery` | `AWS::Lambda::Function` | `False` |

Zero or one of each optional dependency may additionally appear:

- `RecoveryInvokePermission`, Modify, `AWS::Lambda::Permission`, replacement
  `Conditional`, one dynamic `RecoverySchedule.Arn` → `SourceArn` detail with
  `RequiresRecreation:"Always"`;
- `RecoverySchedule`, Modify, `AWS::Events::Rule`, replacement `False`, one
  dynamic `Recovery.Arn` → `Targets` detail with
  `RequiresRecreation:"Never"`.

Any Remove, replacement `True`, duplicate, missing direct member, unlisted
member, incomplete projection or different optional detail rejects before
execute. The normalized projection sorts by `logicalId`; its SHA-256 is over
UTF-8 bytes of the recursive canonical representation defined in 3.2. Every
live `describe-change-set` observation retains the raw `Details` members in
process memory and passes the complete response to the accepted exported
`assertReviewedChanges("full", described)` before computing or retaining that
sanitized projection hash. The runner selftest proves the accepted optional
details pass and a wrong `RecoverySchedule` dependency detail rejects through
this same production guard.

### 3.4 Applied intermediate-disabled and terminal-active contracts

The accepted template has exactly 82 resources, 34 outputs, 19 parameters, 14
physical queues (seven source plus seven DLQ), eight functions, seven mappings
and 31 alarms. The intermediate `inspect-stack --expected-disabled` result
remains exactly:

```json
{
  "outcome": "EXPECTED_DISABLED_KEYWORD_STACK_VERIFIED",
  "identityVerified": true,
  "deployment": "production",
  "resources": 82,
  "queues": 7,
  "dlqs": 7,
  "functions": 8,
  "mappings": 7,
  "alarms": 31,
  "keywordActive": false,
  "keywordSourceMessages": 0,
  "keywordDlqMessages": 0
}
```

The inspector's activation witness also requires every template resource,
output, parameter, Lambda configuration/concurrency/environment, event mapping,
queue/DLQ attribute, log retention/activity, inline/managed IAM policy and alarm
to equal the template; no broad S3/SQS data-plane grant; all six established
mappings enabled; the one Recovery schedule remains enabled at `rate(5
minutes)`; `KeywordResearchMapping` disabled; KeywordWorker and Recovery
keyword flags `false`; keyword source/DLQ total visible+in-flight+delayed count
zero; and no KeywordWorker log stream.

The final `inspect-stack --expected-active` result must return exactly:

```json
{
  "outcome": "EXPECTED_ACTIVE_KEYWORD_STACK_VERIFIED",
  "identityVerified": true,
  "deployment": "production",
  "resources": 82,
  "queues": 7,
  "dlqs": 7,
  "functions": 8,
  "mappings": 7,
  "alarms": 31,
  "keywordActive": true,
  "keywordSourceMessages": 0,
  "keywordDlqMessages": 0
}
```

The active inspector requires `KeywordResearchMapping` enabled, KeywordWorker
and Recovery keyword flags `true`, every established mapping and the Recovery
schedule still enabled, and every other topology/IAM/configuration assertion
identical to the intermediate check. W8 submits no queue message and creates no
research. `forbiddenCounts.activation` therefore means activation outside the
single exact ACT-02 activation transaction and remains zero.

## 4. Approval and lifecycle state machine

| State | Entry predicate | Allowed next operation | Durable/output write | Replay/ambiguity result | Forbidden transition |
|---|---|---|---|---|---|
| `DECOMPOSITION_REVIEW` | current A5 v205 assignment | parent review only | S1–S3 | revision mismatch blocks | any P1/AWS action |
| `PREFLIGHT_ASSIGNED` | new A5 pins approved S1 and authorizes P1–P6 only | Section 6 gates P1–P6 | two measurement JSONs, S2/S3 | any pinned authority/source/package, root-scope, target identity, stable-stack or quota/capability drift invalidates | ACT-01/02 |
| `AWAITING_ACT01_APPROVAL` | P1–P6 and LIVE-01 pass | parent/requester approval | A5/S2/S3 only | re-read P1/P2 source/stack state before approval use | ACT-01 without token |
| `ACT01_ASSIGNED` | A5 authorizes only `W8-ACT-01`, pins exact packet token and Section 5.1 sanitized hashes/cardinalities | exact ACT-01 command | packet/artifacts/full-change-set plus AWS objects/change set | in-memory/private-record identity re-hashes to tracked pins; unequal blocks | execute change set |
| `AWAITING_ACT02_APPROVAL` | LIVE-02 pass; unexecuted reviewed-ID hash/presence exact | parent/requester approval | A5/S2/S3 only | private ID re-hash and live re-description projection re-hash; drift blocks | ACT-02 without approval |
| `ACT02_ASSIGNED` | A5 authorizes only `W8-ACT-02` and pins Section 5.2 sanitized hashes/cardinalities | exact apply then inspector | stack update plus A5/A6/S2/S3 | describe/wait/inspect private ID; retained evidence stays sanitized | replacement create/manual repair |
| `READY_FOR_PARENT_REVIEW` | LIVE-03, CONF-01, V1–V4, H1–H6 and expected-active pass | parent review | evidence/state only | none | unapproved application work |
| `PARENT_BLOCKED` | one exact blocker branch below | parent decision | evidence/state only | no retry beyond prescribed reconciliation | workaround/expanded action |

CloudFormation's own update transaction and automatic rollback are the only
deployment atomicity boundary. Objects are immutable/content-addressed. The
change set is a recovered boundary: an unexecuted change set has no stack
effect; apply ambiguity is reconciled from its ID, `ExecutionStatus`, stack
status/events and the final inspector. No manual repair or compensating delete
exists in W8.

## 5. Action-specific A5 pinning

### 5.1 ACT-01 state must pin

- `state_version`, approved S1 SHA-256 and `current_assignment_id`;
- `authorized_actions:[W8-ACT-01]` and no ACT-02/successor member;
- exact profile, region, stack and environment; account `{present:true,
  sha256:<64hex>,last4:<4digits>}`; bucket `{present:true,sha256:<64hex>}`;
- exact scalar fields `aws_target_account_present:true`,
  `aws_target_account_sha256`, `aws_target_account_last4`,
  `aws_artifact_bucket_present:true`, `aws_artifact_bucket_sha256`, and
  `p2_sanitized_projection_sha256` consumed by the frozen runner;
- exact three source paths, byte lengths, SHA-256 values and keys;
- exact packet `approvalToken` in `aws_mutation_approval`; and
- exact expected change-set name and direct/optional allowlist revision.

Immediately before the command, recompute all source bytes/token and re-run STS,
stack status and pending-change-set reads. Any mismatch consumes no AWS write and
returns `PARENT_BLOCKED_ACT01_PIN_DRIFT`.

### 5.2 ACT-02 state must pin

- every unchanged ACT-01 sanitized identity and exact packet token;
- `authorized_actions:[W8-ACT-02]` and no ACT-01/successor member;
- exact local `full-change-set.json` SHA-256;
- change-set ID `{present:true,sha256:<64hex>}`, deterministic name, status
  `CREATE_COMPLETE`, execution status `AVAILABLE`, normalized projection and
  projection SHA-256; three object-version
  `{present:true,sha256:<64hex>}` members in fixed packet order; and
- the same packet approval token in `aws_mutation_approval`.

The ACT-02 A5 spellings consumed literally are
`aws_object_version_count:3`, `aws_object_version_sha256s:[<hex>, <hex>,
<hex>]` in packet order, `aws_change_set_present:true`,
`aws_change_set_id_sha256`, `full_change_set_record_sha256`, and
`change_projection_sha256`. No raw counterpart field is permitted.

Immediately before execute, the private-record ID is re-hashed to the A5 pin;
`describe-change-set` by that ID must reproduce every sanitized pin. Any
mismatch performs zero execute and returns
`PARENT_BLOCKED_ACT02_PIN_DRIFT`.

## 6. `KI-W8-I101` — window-agent sequential assessment

```yaml
subwindow_id: KI-W8-I101
type: INTEGRATION_ASSESSMENT
parent_window_id: KI-W8
parent_assignment_id_at_authoring: ASG-KI-W8-WA-02
assigned_agent: WINDOW-AGENT_AFTER_PARENT_APPROVAL
predecessors: [parent_accepted_KI-W7, parent_approved_KI-W8-AWS-ONLY-DECOMP-4]
successor_reserved_for: parent
authorized_write_file: NONE
expected_implementation_changed_file_set: []
read_only_scope: [the exact Section 1 source/AWS surfaces]
authorized_actions: [P1-P6 only under initial execution assignment, W8-ACT-01 only under its separate A5 approval, W8-ACT-02 only under its separate A5 approval]
prohibited_actions: [every Section 1 exclusion]
may_start_successor: false
```

### 6.0 Frozen executor and output transport

At the start of each separately assigned phase (P1–P6, ACT-01, ACT-02), I101
runs these literal shell commands from workspace root in one durable shell with
xtrace disabled. `KIW8_ROOT` and `KIW8_TMP` are shell-local process state; the
directory contains sanitized projections and validator bytes only:

```text
set -euo pipefail
set +x
umask 077
export KIW8_ROOT="$PWD"
export KIW8_TMP="$(mktemp -d /tmp/ki-w8-i101.XXXXXX)"
test -n "$KIW8_TMP" && test "${KIW8_TMP#/tmp/ki-w8-i101.}" != "$KIW8_TMP" && test -d "$KIW8_TMP"
node --input-type=module -e 'import{readFileSync,writeFileSync,chmodSync}from"node:fs";const s=readFileSync("KEYWORD_INTELLIGENCE_KI_W8_AWS_ONLY_SUBWINDOW_CHECKLIST.md","utf8"),m=s.match(/<!-- KIW8_RUNNER_BEGIN -->\n```javascript\n([\s\S]*?)\n```\n<!-- KIW8_RUNNER_END -->/u);if(!m)throw new Error("KIW8_RUNNER_SOURCE_MISSING");writeFileSync(process.env.KIW8_TMP+"/kiw8-runner.mjs",m[1]+"\n",{mode:0o700});chmodSync(process.env.KIW8_TMP+"/kiw8-runner.mjs",0o700)'
export KIW8_RUNNER="$KIW8_TMP/kiw8-runner.mjs"
node "$KIW8_RUNNER" selftest
```

The prior phase runs `node "$KIW8_RUNNER" cleanup` only after its sanitized
projection hashes are appended to S3/A6 and S2 is updated. A resumed phase does
not rely on the prior shell or `/tmp` bytes. The extracted runner SHA-256 is
pinned by the parent-direct DECOMP-4 correction. No
executor edits it. Every AWS invocation below is made only by this runner or by
the three accepted deployment/inspection script pipelines stated literally in
6.4, 6.7 and 6.8. `spawnSync` captures raw output in process memory. The runner
writes only sanitized JSON below `KIW8_TMP`, emits safe fixed success tokens,
and hashes AWS stderr before any failure is surfaced. Each
`KIW8_EXPORTS="$(...)"`/`eval "$KIW8_EXPORTS"` stream contains shell exports and
is consumed then unset without display or retention;
they are the only raw-identity shell transport. Retained terminal/A6/S3 output
must be the runner's sanitized projection/digest, never raw command stdout.

<!-- KIW8_RUNNER_BEGIN -->
```javascript
import { createHash } from "node:crypto";
import { chmodSync, lstatSync, readFileSync, realpathSync, rmSync, writeFileSync } from "node:fs";
import { spawnSync } from "node:child_process";
import path from "node:path";
import { pathToFileURL } from "node:url";

const ROOT = process.env.KIW8_ROOT;
const TMP = process.env.KIW8_TMP;
const PROFILE = "storesignal-dev";
const REGION = "ap-south-2";
const STACK = "storesignal-production-pipeline";
const ACCEPTED_STACK_STATUSES = ["CREATE_COMPLETE", "UPDATE_COMPLETE"];
const CASES = ["W8-CONF-01", "W8-LIVE-01", "W8-LIVE-02", "W8-LIVE-03"];
const CONTROLS = Array.from({ length: 8 }, (_, index) => `W8-NC-${String(index + 1).padStart(2, "0")}`);
const FORBIDDEN = ["activation", "apiResearch", "browser", "database", "destructive", "lambdaDirectInvoke", "localServer", "paid", "provider", "queueDataPlane", "secretValueRead"];
const ROOT_ALLOWED = ["ACTIVE_EXECUTION_STATE.md", "KEYWORD_INTELLIGENCE_DECISION_LEDGER.md", "KEYWORD_INTELLIGENCE_DISCOVERY_DOSSIER.md", "KEYWORD_INTELLIGENCE_EXECUTION_EVIDENCE.md", "KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md", "KEYWORD_INTELLIGENCE_KI_W8_AWS_ONLY_SUBWINDOW_CHECKLIST.md", "KEYWORD_INTELLIGENCE_KI_W8_AWS_ONLY_SUBWINDOW_EVIDENCE.md", "KEYWORD_INTELLIGENCE_KI_W8_AWS_ONLY_SUBWINDOW_STATE.md", "KEYWORD_INTELLIGENCE_SPECIFICATION_CHANGELOG.md", "KEYWORD_INTELLIGENCE_TRACEABILITY_INDEX.md"];
const EXECUTION_PATHS = ["ACTIVE_EXECUTION_STATE.md", "KEYWORD_INTELLIGENCE_EXECUTION_EVIDENCE.md", "KEYWORD_INTELLIGENCE_KI_W8_AWS_ONLY_SUBWINDOW_EVIDENCE.md", "KEYWORD_INTELLIGENCE_KI_W8_AWS_ONLY_SUBWINDOW_STATE.md", "email_scraper/dist/aws-deployment/keyword-intelligence/activate-change-set.json", "email_scraper/dist/aws-deployment/keyword-intelligence/artifacts.json", "email_scraper/dist/aws-deployment/keyword-intelligence/full-change-set.json", "email_scraper/dist/aws-deployment/keyword-intelligence/packet.json", "email_scraper/dist/lambda/keyword-worker-measurements.json", "email_scraper/dist/lambda/measurements.json"];
const DIRECT = [
  ["Add", "KeywordResearchDlq", "AWS::SQS::Queue", null],
  ["Add", "KeywordResearchQueue", "AWS::SQS::Queue", null],
  ["Add", "KeywordWorkerLogGroup", "AWS::Logs::LogGroup", null],
  ["Add", "KeywordWorkerRole", "AWS::IAM::Role", null],
  ["Add", "KeywordWorker", "AWS::Lambda::Function", null],
  ["Add", "KeywordResearchMapping", "AWS::Lambda::EventSourceMapping", null],
  ["Add", "KeywordResearchDlqDepthAlarm", "AWS::CloudWatch::Alarm", null],
  ["Add", "KeywordResearchOldestMessageAlarm", "AWS::CloudWatch::Alarm", null],
  ["Add", "KeywordWorkerErrorsAlarm", "AWS::CloudWatch::Alarm", null],
  ["Add", "KeywordWorkerThrottlesAlarm", "AWS::CloudWatch::Alarm", null],
  ["Modify", "ControlPlanePolicy", "AWS::IAM::ManagedPolicy", "False"],
  ["Modify", "RecoveryRole", "AWS::IAM::Role", "False"],
  ["Modify", "Recovery", "AWS::Lambda::Function", "False"]
];
const ACTIVATE = [
  ["Modify", "KeywordResearchMapping", "AWS::Lambda::EventSourceMapping", "False"],
  ["Modify", "KeywordWorker", "AWS::Lambda::Function", "False"],
  ["Modify", "Recovery", "AWS::Lambda::Function", "False"]
];

function fail(code) { throw Object.assign(new Error(code), { code }); }
function ok(value, code) { if (!value) fail(code); }
function sha(value) { return createHash("sha256").update(value).digest("hex"); }
function canonical(value) {
  if (Array.isArray(value)) return `[${value.map(canonical).join(",")}]`;
  if (value && typeof value === "object") return `{${Object.keys(value).sort().map((key) => `${JSON.stringify(key)}:${canonical(value[key])}`).join(",")}}`;
  return JSON.stringify(value);
}
function digest(ids) { return sha([...ids].sort().map((id) => `${id}\n`).join("")); }
function exactKeys(value, keys, code) { ok(value && typeof value === "object" && !Array.isArray(value), code); ok(JSON.stringify(Object.keys(value).sort()) === JSON.stringify([...keys].sort()), code); }
function readJson(file) { return JSON.parse(readFileSync(file, "utf8")); }
function safeId(value) { ok(typeof value === "string" && value.length > 0, "KIW8_ID_MISSING"); return { present: true, sha256: sha(value) }; }
function safeWrite(name, value) {
  const base = realpathSync(TMP);
  ok(base.startsWith("/tmp/ki-w8-i101."), "KIW8_TMP_SCOPE_INVALID");
  const file = path.join(base, name);
  writeFileSync(file, `${JSON.stringify(value, null, 2)}\n`, { mode: 0o600 });
  chmodSync(file, 0o600);
  return { file: name, sha256: sha(readFileSync(file)) };
}
function command(binary, args, options = {}) {
  const result = spawnSync(binary, args, { cwd: options.cwd || ROOT, encoding: "utf8", maxBuffer: 32 * 1024 * 1024 });
  if (result.status !== 0) {
    if (options.allowFailure) return { failed: true, status: result.status, absent: /(?:404|Not Found|NoSuchKey|does not exist|ValidationError)/iu.test(result.stderr || ""), stderrSha256: sha(result.stderr || "") };
    fail(`${options.code || "KIW8_COMMAND_FAILED"}:${sha(result.stderr || "")}`);
  }
  const text = `${result.stdout || ""}${result.stderr || ""}`;
  return options.json === false ? (options.preserveWhitespace ? text : text.trim()) : JSON.parse(result.stdout || "{}");
}
function aws(args, options = {}) { return command("aws", [...args, "--profile", PROFILE, "--region", REGION, "--no-cli-pager", ...(options.json === false ? [] : ["--output", "json"])], options); }
function shellQuote(value) { return `'${String(value).replaceAll("'", `'"'"'`)}'`; }
function sourceDetails(source, basename, logicalId) {
  const body = readFileSync(path.join(ROOT, "email_scraper", source));
  const value = { ...(logicalId ? { logicalId } : {}), basename, source, bytes: body.byteLength, sha256: sha(body) };
  return { ...value, key: `deployment/${value.sha256}/${basename}` };
}
function packet(accountId) {
  ok(/^\d{12}$/u.test(accountId), "KIW8_ACCOUNT_INVALID");
  const value = { contractVersion: "storesignal-keyword-deployment-v1", profile: PROFILE, accountId, region: REGION, stack: STACK, environment: "production", bucket: `storesignal-prod-pipeline-${accountId}-${REGION}`, template: sourceDetails("infrastructure/aws/template.yaml", "cloudformation-template.json"), zips: [sourceDetails("dist/lambda/keyword-worker.zip", "keyword-worker.zip", "KeywordWorker"), sourceDetails("dist/lambda/recovery.zip", "recovery.zip", "Recovery")] };
  return { ...value, approvalToken: sha(canonical(value)) };
}
function projection(change) { return { action: change.action, logicalId: change.logicalId, type: change.type, replacement: change.replacement ?? null }; }
function validateChanges(changes) {
  ok(Array.isArray(changes) && changes.length >= 13 && changes.length <= 15, "KIW8_CHANGE_COUNT");
  const ids = changes.map((entry) => entry.logicalId);
  ok(ids.length === new Set(ids).size, "KIW8_CHANGE_DUPLICATE");
  const direct = changes.filter((entry) => !["RecoveryInvokePermission", "RecoverySchedule"].includes(entry.logicalId)).map(projection).sort((a, b) => a.logicalId.localeCompare(b.logicalId));
  const expected = DIRECT.map(([action, logicalId, type, replacement]) => ({ action, logicalId, type, replacement })).sort((a, b) => a.logicalId.localeCompare(b.logicalId));
  ok(canonical(direct) === canonical(expected), "KIW8_CHANGE_ALLOWLIST");
  const optional = changes.filter((item) => ["RecoveryInvokePermission", "RecoverySchedule"].includes(item.logicalId));
  for (const entry of optional) {
    const expectedOptional = entry.logicalId === "RecoveryInvokePermission"
      ? { action: "Modify", logicalId: "RecoveryInvokePermission", type: "AWS::Lambda::Permission", replacement: "Conditional" }
      : { action: "Modify", logicalId: "RecoverySchedule", type: "AWS::Events::Rule", replacement: "False" };
    ok(canonical(projection(entry)) === canonical(expectedOptional), "KIW8_CHANGE_OPTIONAL");
  }
  return changes.map(projection).sort((a, b) => a.logicalId.localeCompare(b.logicalId));
}
function validateActivationChanges(changes) {
  ok(Array.isArray(changes) && changes.length >= 3 && changes.length <= 5, "KIW8_ACTIVATION_CHANGE_COUNT");
  const ids = changes.map((entry) => entry.logicalId);
  ok(ids.length === new Set(ids).size, "KIW8_ACTIVATION_CHANGE_DUPLICATE");
  const direct = changes.filter((entry) => !["RecoveryInvokePermission", "RecoverySchedule"].includes(entry.logicalId)).map(projection).sort((a, b) => a.logicalId.localeCompare(b.logicalId));
  const expected = ACTIVATE.map(([action, logicalId, type, replacement]) => ({ action, logicalId, type, replacement })).sort((a, b) => a.logicalId.localeCompare(b.logicalId));
  ok(canonical(direct) === canonical(expected), "KIW8_ACTIVATION_CHANGE_ALLOWLIST");
  const optional = changes.filter((item) => ["RecoveryInvokePermission", "RecoverySchedule"].includes(item.logicalId));
  for (const entry of optional) {
    const expectedOptional = entry.logicalId === "RecoveryInvokePermission"
      ? { action: "Modify", logicalId: "RecoveryInvokePermission", type: "AWS::Lambda::Permission", replacement: "Conditional" }
      : { action: "Modify", logicalId: "RecoverySchedule", type: "AWS::Events::Rule", replacement: "False" };
    ok(canonical(projection(entry)) === canonical(expectedOptional), "KIW8_ACTIVATION_CHANGE_OPTIONAL");
  }
  return changes.map(projection).sort((a, b) => a.logicalId.localeCompare(b.logicalId));
}
function fullDescriptionWithDependencies() {
  const direct = DIRECT.map(([Action, LogicalResourceId, ResourceType, Replacement]) => ({ ResourceChange: { Action, LogicalResourceId, ResourceType, Replacement, Details: [] } }));
  const dependencies = [
    { ResourceChange: { Action: "Modify", LogicalResourceId: "RecoveryInvokePermission", ResourceType: "AWS::Lambda::Permission", Replacement: "Conditional", Details: [{ Evaluation: "Dynamic", ChangeSource: "ResourceAttribute", CausingEntity: "RecoverySchedule.Arn", Target: { Name: "SourceArn", RequiresRecreation: "Always" } }] } },
    { ResourceChange: { Action: "Modify", LogicalResourceId: "RecoverySchedule", ResourceType: "AWS::Events::Rule", Replacement: "False", Details: [{ Evaluation: "Dynamic", ChangeSource: "ResourceAttribute", CausingEntity: "Recovery.Arn", Target: { Name: "Targets", RequiresRecreation: "Never" } }] } }
  ];
  return { Changes: [...direct, ...dependencies] };
}
function activationDescriptionWithDependencies() {
  const targets = new Map([["KeywordResearchMapping", "Enabled"], ["KeywordWorker", "Environment"], ["Recovery", "Environment"]]);
  const direct = ACTIVATE.map(([Action, LogicalResourceId, ResourceType, Replacement]) => ({ ResourceChange: { Action, LogicalResourceId, ResourceType, Replacement, Details: [{ Evaluation: "Static", ChangeSource: "DirectModification", CausingEntity: null, Target: { Name: targets.get(LogicalResourceId), RequiresRecreation: "Never" } }] } }));
  const dependencies = [
    { ResourceChange: { Action: "Modify", LogicalResourceId: "RecoveryInvokePermission", ResourceType: "AWS::Lambda::Permission", Replacement: "Conditional", Details: [{ Evaluation: "Dynamic", ChangeSource: "ResourceAttribute", CausingEntity: "RecoverySchedule.Arn", Target: { Name: "SourceArn", RequiresRecreation: "Always" } }] } },
    { ResourceChange: { Action: "Modify", LogicalResourceId: "RecoverySchedule", ResourceType: "AWS::Events::Rule", Replacement: "False", Details: [{ Evaluation: "Dynamic", ChangeSource: "ResourceAttribute", CausingEntity: "Recovery.Arn", Target: { Name: "Targets", RequiresRecreation: "Never" } }] } }
  ];
  return { Changes: [...direct, ...dependencies] };
}
async function assertReviewedFull(description) {
  const deployment = await import(pathToFileURL(path.join(ROOT, "email_scraper/scripts/keyword-intelligence/create-change-set.js")));
  return deployment.assertReviewedChanges("full", description);
}
async function assertReviewedActivate(description) {
  const deployment = await import(pathToFileURL(path.join(ROOT, "email_scraper/scripts/keyword-intelligence/create-change-set.js")));
  return deployment.assertReviewedChanges("activate", description);
}
function validLifecycle(value) {
  const rules = value?.Rules;
  ok(Array.isArray(rules) && rules.length === 1, "KIW8_BUCKET_LIFECYCLE_COUNT");
  const rule = rules[0];
  ok(rule.ID === "AbortIncompleteMultipartUploads" && rule.Status === "Enabled", "KIW8_BUCKET_LIFECYCLE_ID");
  ok(rule.AbortIncompleteMultipartUpload?.DaysAfterInitiation === 7, "KIW8_BUCKET_LIFECYCLE_ABORT");
  ok(rule.Expiration == null && rule.NoncurrentVersionExpiration == null && rule.Transitions == null && rule.NoncurrentVersionTransitions == null, "KIW8_BUCKET_EXPIRATION_FORBIDDEN");
  ok(rule.Prefix == null || rule.Prefix === "", "KIW8_BUCKET_PREFIX");
  const filterKeys = rule.Filter && typeof rule.Filter === "object" && !Array.isArray(rule.Filter) ? Object.keys(rule.Filter) : null;
  ok(rule.Filter == null || (filterKeys && (filterKeys.length === 0 || (filterKeys.length === 1 && filterKeys[0] === "Prefix" && rule.Filter.Prefix === ""))), "KIW8_BUCKET_FILTER");
}
function p2(label) {
  ok(["initial", "recheck", "act02"].includes(label), "KIW8_P2_LABEL");
  const identity = aws(["sts", "get-caller-identity"]);
  const accountId = identity?.Account;
  ok(/^\d{12}$/u.test(accountId), "KIW8_STS_ACCOUNT");
  const stackResult = aws(["cloudformation", "describe-stacks", "--stack-name", STACK]);
  ok(Array.isArray(stackResult.Stacks) && stackResult.Stacks.length === 1, "KIW8_STACK_CARDINALITY");
  const stack = stackResult.Stacks[0];
  ok(ACCEPTED_STACK_STATUSES.includes(stack.StackStatus), "KIW8_STACK_STATUS");
  ok(typeof stack.StackId === "string" && stack.StackId.includes(`:${REGION}:${accountId}:stack/${STACK}/`), "KIW8_STACK_IDENTITY");
  const resourcesResult = aws(["cloudformation", "list-stack-resources", "--stack-name", STACK]);
  const resources = resourcesResult.StackResourceSummaries;
  ok(Array.isArray(resources) && resources.length > 0, "KIW8_RESOURCE_SET");
  for (const item of resources) ok(ACCEPTED_STACK_STATUSES.includes(item.ResourceStatus), "KIW8_RESOURCE_STATUS");
  const changeResult = aws(["cloudformation", "list-change-sets", "--stack-name", STACK]);
  const summaries = changeResult.Summaries || [];
  const active = summaries.filter((item) => ["CREATE_PENDING", "CREATE_IN_PROGRESS", "CREATE_COMPLETE"].includes(item.Status) && ["AVAILABLE", "EXECUTE_IN_PROGRESS"].includes(item.ExecutionStatus));
  let pendingChangeSet = null;
  if (label === "act02") {
    const record = readJson(path.join(ROOT, "email_scraper/dist/aws-deployment/keyword-intelligence/full-change-set.json"));
    ok(active.length === 1 && active[0].ChangeSetId === record.changeSetId && active[0].ChangeSetName === record.changeSetName && active[0].Status === "CREATE_COMPLETE" && active[0].ExecutionStatus === "AVAILABLE", "KIW8_REVIEWED_CHANGE_SET_PENDING");
    pendingChangeSet = safeId(record.changeSetId);
  } else ok(active.length === 0, "KIW8_PENDING_CHANGE_SET");
  const outputs = Object.fromEntries((stack.Outputs || []).map((item) => [item.OutputKey, item.OutputValue]));
  const bucket = `storesignal-prod-pipeline-${accountId}-${REGION}`;
  ok(outputs.ArtifactBucketName === bucket, "KIW8_BUCKET_IDENTITY");
  const versioning = aws(["s3api", "get-bucket-versioning", "--bucket", bucket]);
  const encryption = aws(["s3api", "get-bucket-encryption", "--bucket", bucket]);
  const access = aws(["s3api", "get-public-access-block", "--bucket", bucket]);
  const ownership = aws(["s3api", "get-bucket-ownership-controls", "--bucket", bucket]);
  const lifecycle = aws(["s3api", "get-bucket-lifecycle-configuration", "--bucket", bucket]);
  ok(versioning.Status === "Enabled", "KIW8_BUCKET_VERSIONING");
  const encryptionRules = encryption.ServerSideEncryptionConfiguration?.Rules;
  ok(Array.isArray(encryptionRules) && encryptionRules.length === 1 && encryptionRules[0].ApplyServerSideEncryptionByDefault?.SSEAlgorithm === "AES256" && encryptionRules[0].ApplyServerSideEncryptionByDefault?.KMSMasterKeyID == null && encryptionRules[0].BucketKeyEnabled === false, "KIW8_BUCKET_ENCRYPTION");
  const pab = access.PublicAccessBlockConfiguration;
  ok(pab?.BlockPublicAcls === true && pab.IgnorePublicAcls === true && pab.BlockPublicPolicy === true && pab.RestrictPublicBuckets === true, "KIW8_BUCKET_PUBLIC_ACCESS");
  ok(Array.isArray(ownership.OwnershipControls?.Rules) && ownership.OwnershipControls.Rules.length === 1 && ownership.OwnershipControls.Rules[0].ObjectOwnership === "BucketOwnerEnforced", "KIW8_BUCKET_OWNERSHIP");
  validLifecycle(lifecycle);
  const outputHashes = Object.fromEntries(Object.entries(outputs).sort(([left], [right]) => left.localeCompare(right)).map(([key, value]) => [key, safeId(value)]));
  const sanitized = { account: { ...safeId(accountId), last4: accountId.slice(-4) }, callerArn: safeId(identity.Arn), stackId: safeId(stack.StackId), stackStatus: stack.StackStatus, resourceCount: resources.length, outputCount: (stack.Outputs || []).length, parameterCount: (stack.Parameters || []).length, outputHashes, resourceStatuses: [...new Set(resources.map((item) => item.ResourceStatus))].sort(), pendingChangeSets: active.length, pendingChangeSet, bucket: safeId(bucket), bucketSafety: { versioning: "Enabled", encryption: "AES256", publicAccess: [true, true, true, true], ownership: "BucketOwnerEnforced", lifecycle: { id: "AbortIncompleteMultipartUploads", status: "Enabled", abortIncompleteMultipartDays: 7, expirationMembers: 0 } } };
  if (label === "recheck") ok(canonical(sanitized) === canonical(readJson(path.join(TMP, "p2-sanitized-initial.json"))), "KIW8_P2_RECHECK_DRIFT");
  const saved = safeWrite(`p2-sanitized-${label}.json`, sanitized);
  process.stdout.write(`export KIW8_ACCOUNT_ID=${shellQuote(accountId)};export KIW8_BUCKET=${shellQuote(bucket)};export KIW8_ACCOUNT_SHA256=${shellQuote(sanitized.account.sha256)};export KIW8_BUCKET_SHA256=${shellQuote(sanitized.bucket.sha256)};export KIW8_P2_SHA256=${shellQuote(saved.sha256)};`);
}
function quotas() {
  const settings = aws(["lambda", "get-account-settings"]);
  const lambdaQuotas = aws(["service-quotas", "list-service-quotas", "--service-code", "lambda"]);
  const sqsQuotas = aws(["service-quotas", "list-service-quotas", "--service-code", "sqs"]);
  const cfnQuotas = aws(["service-quotas", "list-service-quotas", "--service-code", "cloudformation"]);
  const all = { lambda: lambdaQuotas.Quotas || [], sqs: sqsQuotas.Quotas || [], cloudformation: cfnQuotas.Quotas || [] };
  for (const values of Object.values(all)) for (const item of values) ok(typeof item.QuotaCode === "string" && typeof item.QuotaName === "string" && Number.isFinite(item.Value) && item.Value >= 0, "KIW8_QUOTA_MEMBER");
  const limit = settings.AccountLimit, usage = settings.AccountUsage;
  for (const value of [limit?.ConcurrentExecutions, limit?.UnreservedConcurrentExecutions, limit?.TotalCodeSize, usage?.FunctionCount, usage?.TotalCodeSize]) ok(Number.isFinite(value) && value >= 0, "KIW8_LAMBDA_ACCOUNT_MEMBER");
  ok(limit.UnreservedConcurrentExecutions >= 101, "KIW8_LAMBDA_UNRESERVED");
  const keywordMeasure = readJson(path.join(ROOT, "email_scraper/dist/lambda/keyword-worker-measurements.json"));
  const establishedMeasure = readJson(path.join(ROOT, "email_scraper/dist/lambda/measurements.json"));
  const keywordEntry = keywordMeasure.measurements?.find((entry) => entry.handler === "keyword-worker");
  const recovery = establishedMeasure.measurements?.find((entry) => entry.handler === "recovery");
  const keywordExpanded = keywordEntry?.unzippedBytes;
  const recoveryExpanded = recovery?.unzippedBytes;
  ok(Number.isFinite(keywordExpanded) && Number.isFinite(recoveryExpanded), "KIW8_MEASUREMENT_MEMBER");
  ok(keywordEntry.zipBytes === 32006605 && keywordEntry.zipBytes <= 47185920 && keywordExpanded <= 209715200 && recoveryExpanded <= 209715200, "KIW8_PACKAGE_BOUNDS");
  ok(limit.TotalCodeSize - usage.TotalCodeSize >= keywordExpanded + recoveryExpanded, "KIW8_LAMBDA_CODE_STORAGE");
  const template = readJson(path.join(ROOT, "email_scraper/infrastructure/aws/template.yaml"));
  const templateCounts = { resources: Object.keys(template.Resources || {}).length, outputs: Object.keys(template.Outputs || {}).length, parameters: Object.keys(template.Parameters || {}).length };
  ok(templateCounts.resources === 82 && templateCounts.resources <= 500 && templateCounts.outputs === 34 && templateCounts.outputs <= 200 && templateCounts.parameters === 19 && templateCounts.parameters <= 200, "KIW8_TEMPLATE_COUNTS_AND_FIXED_LIMITS");
  const startingProjection = readJson(path.join(TMP, "p2-sanitized-initial.json"));
  ok(startingProjection.resourceCount + 10 === 82 && startingProjection.outputCount + 4 === 34 && startingProjection.parameterCount + 3 === 19, "KIW8_TEN_RESOURCE_ADDITION");
  const worker = template.Resources.KeywordWorker?.Properties;
  const mapping = template.Resources.KeywordResearchMapping?.Properties;
  const queue = template.Resources.KeywordResearchQueue?.Properties, dlq = template.Resources.KeywordResearchDlq?.Properties;
  ok(worker?.ReservedConcurrentExecutions === 1 && worker.Timeout === 180 && worker.MemorySize === 1024 && worker.EphemeralStorage?.Size === 512, "KIW8_WORKER_BOUNDS");
  ok(mapping?.BatchSize === 1 && mapping.MaximumBatchingWindowInSeconds === 0 && mapping.ScalingConfig == null && mapping.ProvisionedPollerConfig == null && canonical(mapping.FunctionResponseTypes) === canonical(["ReportBatchItemFailures"]), "KIW8_MAPPING_BOUNDS");
  ok(queue?.VisibilityTimeout === 1080 && queue.MessageRetentionPeriod === 345600 && queue.MaximumMessageSize === 262144 && queue.ReceiveMessageWaitTimeSeconds === 20 && queue.SqsManagedSseEnabled === true && queue.RedrivePolicy?.maxReceiveCount === 5, "KIW8_QUEUE_BOUNDS");
  ok(dlq?.MessageRetentionPeriod === 1209600 && dlq.SqsManagedSseEnabled === true, "KIW8_DLQ_BOUNDS");
  const project = Object.fromEntries(Object.entries(all).map(([service, values]) => [service, values.map(({ QuotaCode, QuotaName, Value, Unit }) => ({ quotaCode: QuotaCode, quotaName: QuotaName, value: Value, unit: Unit || null })).sort((a, b) => a.quotaCode.localeCompare(b.quotaCode))]));
  const sanitized = { lambdaAccount: { unreserved: limit.UnreservedConcurrentExecutions, existingFunctionCount: usage.FunctionCount, codeBytesRemaining: limit.TotalCodeSize - usage.TotalCodeSize, requiredExpandedBytes: keywordExpanded + recoveryExpanded }, template: { resources: 82, resourceLimit: 500, outputs: 34, outputLimit: 200, parameters: 19, parameterLimit: 200, timeout: 180, memory: 1024, ephemeral: 512, reservedConcurrency: 1, visibility: 1080, retention: 345600, maximumMessageSize: 262144, batch: 1, window: 0 }, quotaInventory: project };
  const result = safeWrite("p3-sanitized.json", sanitized);
  console.log(`KIW8_QUOTA_PROJECTION_OK ${result.sha256}`);
}
function privateMode(file) { ok((lstatSync(file).mode & 0o777) === 0o600, "KIW8_PRIVATE_MODE"); }
function records() {
  const base = path.join(ROOT, "email_scraper/dist/aws-deployment/keyword-intelligence");
  const files = ["packet.json", "artifacts.json", "full-change-set.json"].map((name) => path.join(base, name));
  files.forEach(privateMode);
  const packetRecord = readJson(files[0]), artifact = readJson(files[1]), change = readJson(files[2]);
  const expected = packet(packetRecord.accountId);
  exactKeys(packetRecord, ["contractVersion", "profile", "accountId", "region", "stack", "environment", "bucket", "template", "zips", "approvalToken"], "KIW8_PACKET_KEYS");
  ok(canonical(packetRecord) === canonical(expected), "KIW8_PACKET_DRIFT");
  exactKeys(artifact, ["contractVersion", "approvalToken", "accountId", "region", "stack", "bucket", "template", "zips"], "KIW8_ARTIFACT_KEYS");
  ok(artifact.contractVersion === "storesignal-keyword-artifacts-v1" && artifact.approvalToken === expected.approvalToken && artifact.accountId === expected.accountId && artifact.region === REGION && artifact.stack === STACK && artifact.bucket === expected.bucket, "KIW8_ARTIFACT_HEADER");
  ok(Array.isArray(artifact.zips) && artifact.zips.length === 2, "KIW8_ARTIFACT_ZIPS");
  const artifactMembers = [artifact.template, ...artifact.zips];
  const expectedMembers = [expected.template, ...expected.zips];
  expectedMembers.forEach((item, index) => { const actual = artifactMembers[index]; exactKeys(actual, [...Object.keys(item), "versionId"], "KIW8_ARTIFACT_MEMBER_KEYS"); ok(canonical(Object.fromEntries(Object.keys(item).map((key) => [key, actual[key]]))) === canonical(item), "KIW8_ARTIFACT_MEMBER"); safeId(actual.versionId); });
  exactKeys(change, ["contractVersion", "approvalToken", "phase", "changeSetName", "changeSetId", "changes"], "KIW8_CHANGE_RECORD_KEYS");
  ok(change.contractVersion === "storesignal-keyword-change-set-v1" && change.approvalToken === expected.approvalToken && change.phase === "full" && change.changeSetName === `ki-full-${expected.approvalToken.slice(0, 12)}`, "KIW8_CHANGE_RECORD_HEADER");
  const normalized = validateChanges(change.changes);
  const sanitized = { packetSha256: sha(readFileSync(files[0])), artifactRecordSha256: sha(readFileSync(files[1])), changeRecordSha256: sha(readFileSync(files[2])), approvalToken: expected.approvalToken, account: { ...safeId(expected.accountId), last4: expected.accountId.slice(-4) }, bucket: safeId(expected.bucket), objectVersions: artifactMembers.map((item) => safeId(item.versionId)), changeSet: safeId(change.changeSetId), changeSetName: change.changeSetName, projection: normalized, projectionSha256: sha(canonical(normalized)) };
  const result = safeWrite("records-sanitized.json", sanitized);
  console.log(`KIW8_PRIVATE_RECORDS_OK ${result.sha256}`);
  return { packetRecord, artifact, change, sanitized };
}
function activationRecord() {
  const file = path.join(ROOT, "email_scraper/dist/aws-deployment/keyword-intelligence/activate-change-set.json");
  privateMode(file);
  const value = readJson(file), base = records(), expectedName = `ki-activate-${base.packetRecord.approvalToken.slice(0, 12)}`;
  exactKeys(value, ["contractVersion", "approvalToken", "phase", "changeSetName", "changeSetId", "changes"], "KIW8_ACTIVATION_RECORD_KEYS");
  ok(value.contractVersion === "storesignal-keyword-change-set-v1" && value.approvalToken === base.packetRecord.approvalToken && value.phase === "activate" && value.changeSetName === expectedName, "KIW8_ACTIVATION_RECORD_HEADER");
  const normalized = validateActivationChanges(value.changes);
  const sanitized = { changeRecordSha256: sha(readFileSync(file)), changeSet: safeId(value.changeSetId), changeSetName: value.changeSetName, projection: normalized, projectionSha256: sha(canonical(normalized)) };
  safeWrite("activation-record-sanitized.json", sanitized);
  return { value, sanitized };
}
function porcelain(cwd) { return command("git", ["status", "--porcelain=v1", "-z"], { cwd, json: false, preserveWhitespace: true }).split("\0").filter(Boolean).map((line) => line.slice(3)).sort(); }
function scope() {
  const rootPaths = porcelain(ROOT), backend = porcelain(path.join(ROOT, "email_scraper")), frontend = porcelain(path.join(ROOT, "frontend"));
  ok(rootPaths.every((item) => ROOT_ALLOWED.includes(item)), "KIW8_ROOT_SCOPE");
  ok((backend.length === 0 || canonical(backend) === canonical(["scripts/keyword-intelligence/create-change-set.js"])) && frontend.length === 0, "KIW8_NESTED_SCOPE");
  ok(sha(readFileSync(path.join(ROOT, "email_scraper/scripts/keyword-intelligence/create-change-set.js"))) === "54d82520988cae11edae7593ab2ad5ed1c5049be4601fb90282abdc23339342e", "KIW8_DEPLOYMENT_GUARD_PIN");
  const state = readFileSync(path.join(ROOT, "ACTIVE_EXECUTION_STATE.md"), "utf8"), s1Hash = sha(readFileSync(path.join(ROOT, "KEYWORD_INTELLIGENCE_KI_W8_AWS_ONLY_SUBWINDOW_CHECKLIST.md")));
  ok(stateField(state, "decomposition_revision", "[a-f0-9]{64}") === s1Hash, "KIW8_IMMUTABLE_S1");
  const executionDigest = digest(EXECUTION_PATHS);
  ok(executionDigest === "c0ae7c02ba529c538d22ae831637abbc199b53836428ec79f13fd844604057f9", "KIW8_EXECUTION_SET");
  const result = safeWrite("scope-sanitized.json", { rootPaths, backendPaths: backend, frontendPaths: [], immutableS1Sha256: s1Hash, executionPaths: EXECUTION_PATHS, executionDigest });
  console.log(`KIW8_SCOPE_OK ${result.sha256}`);
}
function stateField(body, name, pattern) { const value = body.match(new RegExp(`^${name}:\\s*(${pattern})\\s*$`, "mu"))?.[1]; ok(value != null, `KIW8_STATE_FIELD_${name}`); return value; }
function statePins(action) {
  ok(["W8-ACT-01", "W8-ACT-02"].includes(action), "KIW8_STATE_ACTION");
  const body = readFileSync(path.join(ROOT, "ACTIVE_EXECUTION_STATE.md"), "utf8"), expected = packet(process.env.KIW8_ACCOUNT_ID);
  ok(/^current_window:\s*KI-W8\s*$/mu.test(body), "KIW8_STATE_WINDOW");
  ok(new RegExp(`^authorized_actions:\\s*\\[${action}\\]\\s*$`, "mu").test(body), "KIW8_STATE_ACTION_AUTHORITY");
  ok(stateField(body, "aws_target_account_present", "true|false") === "true" && stateField(body, "aws_target_account_sha256", "[a-f0-9]{64}") === sha(expected.accountId) && stateField(body, "aws_target_account_last4", "[0-9]{4}") === expected.accountId.slice(-4), "KIW8_STATE_ACCOUNT_PIN");
  ok(stateField(body, "aws_artifact_bucket_present", "true|false") === "true" && stateField(body, "aws_artifact_bucket_sha256", "[a-f0-9]{64}") === sha(expected.bucket), "KIW8_STATE_BUCKET_PIN");
  ok(stateField(body, "p2_sanitized_projection_sha256", "[a-f0-9]{64}") === process.env.KIW8_P2_SHA256, "KIW8_STATE_P2_PIN");
  ok(stateField(body, "aws_mutation_approval", "[a-f0-9]{64}") === expected.approvalToken, "KIW8_STATE_PACKET_TOKEN");
  const sanitized = { action, account: { present: true, sha256: sha(expected.accountId), last4: expected.accountId.slice(-4) }, bucket: safeId(expected.bucket), p2Sha256: process.env.KIW8_P2_SHA256, approvalToken: expected.approvalToken };
  if (action === "W8-ACT-02") {
    const record = records(), versions = record.sanitized.objectVersions.map((item) => item.sha256), pinnedVersions = stateField(body, "aws_object_version_sha256s", "\\[[a-f0-9, ]+\\]").slice(1, -1).split(",").map((item) => item.trim()).filter(Boolean);
    ok(stateField(body, "aws_object_version_count", "[0-9]+") === "3" && canonical(pinnedVersions) === canonical(versions), "KIW8_STATE_VERSION_PINS");
    ok(stateField(body, "aws_change_set_present", "true|false") === "true" && stateField(body, "aws_change_set_id_sha256", "[a-f0-9]{64}") === record.sanitized.changeSet.sha256, "KIW8_STATE_CHANGE_SET_PIN");
    ok(stateField(body, "full_change_set_record_sha256", "[a-f0-9]{64}") === record.sanitized.changeRecordSha256 && stateField(body, "change_projection_sha256", "[a-f0-9]{64}") === record.sanitized.projectionSha256, "KIW8_STATE_CHANGE_RECORD_PIN");
    Object.assign(sanitized, { objectVersions: record.sanitized.objectVersions, changeSet: record.sanitized.changeSet, changeRecordSha256: record.sanitized.changeRecordSha256, projectionSha256: record.sanitized.projectionSha256 });
  }
  const result = safeWrite(`${action.toLowerCase()}-state-pins.json`, sanitized); console.log(`KIW8_STATE_PINS_OK ${result.sha256}`);
}
function certificate(value, evidence) {
  exactKeys(value, ["certificate", "requiredCases", "registeredCases", "executedCases", "activatedCases", "skippedCases", "duplicateCaseIds", "unexpectedCaseIds", "requiredControls", "falsifiedControls", "caseDigest", "controlDigest", "liveEvidence", "actionLedger", "forbiddenCounts"], "KIW8_CERT_KEYS");
  ok(value.certificate === "KI-W8-EXECUTION-PASS", "KIW8_CERT_NAME");
  const exactRaw = (actual, expected, code) => { ok(Array.isArray(actual) && actual.length === new Set(actual).size, `${code}_DUPLICATE`); ok(canonical(actual) === canonical(expected), code); };
  exactRaw(value.requiredCases, CASES, "KIW8_REQUIRED_CASES"); exactRaw(value.registeredCases, CASES, "KIW8_REGISTERED_CASES"); exactRaw(value.executedCases, CASES, "KIW8_EXECUTED_CASES"); exactRaw(value.activatedCases, CASES, "KIW8_ACTIVATED_CASES");
  exactRaw(value.requiredControls, CONTROLS, "KIW8_REQUIRED_CONTROLS"); exactRaw(value.falsifiedControls, CONTROLS, "KIW8_FALSIFIED_CONTROLS");
  ok(canonical(value.skippedCases) === "[]" && canonical(value.duplicateCaseIds) === "[]" && canonical(value.unexpectedCaseIds) === "[]", "KIW8_CERT_EMPTY_SETS");
  ok(value.caseDigest === digest(CASES) && value.controlDigest === digest(CONTROLS), "KIW8_CERT_DIGEST");
  ok(canonical(value.liveEvidence) === canonical({ "W8-LIVE-01": "EV-KI-W8-L01", "W8-LIVE-02": "EV-KI-W8-L02", "W8-LIVE-03": "EV-KI-W8-L03" }), "KIW8_LIVE_EVIDENCE");
  ok(canonical(value.actionLedger) === canonical(["W8-ACT-01", "W8-ACT-02"]), "KIW8_ACTION_LEDGER");
  exactKeys(value.forbiddenCounts, FORBIDDEN, "KIW8_FORBIDDEN_KEYS"); ok(FORBIDDEN.every((key) => value.forbiddenCounts[key] === 0), "KIW8_FORBIDDEN_VALUE");
  exactKeys(evidence, ["W8-LIVE-01", "W8-LIVE-02", "W8-LIVE-03"], "KIW8_EVIDENCE_KEYS");
  for (const id of ["W8-LIVE-01", "W8-LIVE-02", "W8-LIVE-03"]) ok(evidence[id]?.entryId === value.liveEvidence[id] && /^[a-f0-9]{64}$/u.test(evidence[id]?.projectionSha256), "KIW8_EVIDENCE_FIDELITY");
  ok(canonical(evidence) === canonical(evidenceFromA6()), "KIW8_EVIDENCE_DIGEST_FIDELITY");
}
function evidenceFromA6() {
  const body = readFileSync(path.join(ROOT, "KEYWORD_INTELLIGENCE_EXECUTION_EVIDENCE.md"), "utf8"), result = {};
  for (const [id, entryId] of [["W8-LIVE-01", "EV-KI-W8-L01"], ["W8-LIVE-02", "EV-KI-W8-L02"], ["W8-LIVE-03", "EV-KI-W8-L03"]]) {
    const section = body.match(new RegExp(`^## ${entryId}[^\\n]*\\n([\\s\\S]*?)(?=^## |(?![\\s\\S]))`, "mu"))?.[1];
    const projectionSha256 = section?.match(/^sanitized_projection_sha256:\s*([a-f0-9]{64})\s*$/mu)?.[1];
    ok(projectionSha256, "KIW8_EVIDENCE_ENTRY_MISSING"); result[id] = { entryId, projectionSha256 };
  }
  return result;
}
function makeControlInput() {
  const zeros = Object.fromEntries(FORBIDDEN.map((key) => [key, 0]));
  const value = { certificate: "KI-W8-EXECUTION-PASS", requiredCases: CASES, registeredCases: CASES, executedCases: CASES, activatedCases: CASES, skippedCases: [], duplicateCaseIds: [], unexpectedCaseIds: [], requiredControls: CONTROLS, falsifiedControls: CONTROLS, caseDigest: digest(CASES), controlDigest: digest(CONTROLS), liveEvidence: { "W8-LIVE-01": "EV-KI-W8-L01", "W8-LIVE-02": "EV-KI-W8-L02", "W8-LIVE-03": "EV-KI-W8-L03" }, actionLedger: ["W8-ACT-01", "W8-ACT-02"], forbiddenCounts: zeros };
  const input = { certificate: value, evidence: evidenceFromA6() };
  certificate(input.certificate, input.evidence); safeWrite("control-input.json", input); console.log("KIW8_CONTROL_INPUT_OK");
}
async function controls() {
  const input = readJson(path.join(TMP, "control-input.json")); certificate(input.certificate, input.evidence);
  const a6 = readFileSync(path.join(ROOT, "KEYWORD_INTELLIGENCE_EXECUTION_EVIDENCE.md"), "utf8");
  const live02 = a6.match(/^## EV-KI-W8-L02[^\n]*\n([\s\S]*?)(?=^## |(?![\s\S]))/mu)?.[1];
  ok(/^falsified_controls:\s*\[W8-NC-01, W8-NC-02\]\s*$/mu.test(live02 || ""), "KIW8_PRE_CONTROL_EVIDENCE");
  const positiveCertificate = () => certificate(input.certificate, input.evidence);
  const tests = [
    { positive: positiveCertificate, mutate: () => { const value = structuredClone(input); value.certificate.registeredCases.splice(value.certificate.registeredCases.indexOf("W8-LIVE-02"), 1); certificate(value.certificate, value.evidence); } },
    { positive: positiveCertificate, mutate: () => { const value = structuredClone(input); value.certificate.skippedCases.push("W8-LIVE-03"); certificate(value.certificate, value.evidence); } },
    { positive: positiveCertificate, mutate: () => { const value = structuredClone(input); value.certificate.executedCases.push("W8-LIVE-02"); certificate(value.certificate, value.evidence); } },
    { positive: positiveCertificate, mutate: () => { const value = structuredClone(input); delete value.evidence["W8-LIVE-03"]; certificate(value.certificate, value.evidence); } },
    { positive: positiveCertificate, mutate: () => { const value = structuredClone(input); delete value.certificate.forbiddenCounts.provider; certificate(value.certificate, value.evidence); } },
    { positive: positiveCertificate, mutate: () => { const value = structuredClone(input); value.evidence["W8-LIVE-03"].projectionSha256 = "0".repeat(64); certificate(value.certificate, value.evidence); } }
  ];
  let rejected = 0;
  for (const test of tests) { await test.positive(); try { await test.mutate(); } catch { rejected += 1; } await test.positive(); }
  ok(rejected === 6, "KIW8_CONTROL_FALSIFICATION");
  const result = safeWrite("control-result.json", { requiredCases: CASES, requiredControls: CONTROLS, falsifiedControls: CONTROLS, preActionRejected: 2, finalRejected: rejected, caseDigest: digest(CASES), controlDigest: digest(CONTROLS) });
  console.log(`KIW8_CONTROLS_OK ${result.sha256}`);
}
async function preControls() {
  const deployment = await import(pathToFileURL(path.join(ROOT, "email_scraper/scripts/keyword-intelligence/create-change-set.js")));
  const validDescription = { Changes: DIRECT.map(([Action, LogicalResourceId, ResourceType, Replacement]) => ({ ResourceChange: { Action, LogicalResourceId, ResourceType, Replacement, Details: [] } })) };
  const record = records(), expectedPacket = packet(record.packetRecord.accountId);
  const packetGuard = (value) => ok(canonical(value) === canonical(expectedPacket), "KIW8_PACKET_CONTROL");
  const checks = [
    { positive: () => packetGuard(structuredClone(expectedPacket)), mutate: () => { const value = structuredClone(expectedPacket); value.template.sha256 = "0".repeat(64); packetGuard(value); } },
    { positive: () => deployment.assertReviewedChanges("full", structuredClone(validDescription)), mutate: () => { const value = structuredClone(validDescription); value.Changes.push({ ResourceChange: { Action: "Add", LogicalResourceId: "Unlisted", ResourceType: "AWS::SQS::Queue", Replacement: null, Details: [] } }); deployment.assertReviewedChanges("full", value); } }
  ];
  let rejected = 0; for (const check of checks) { await check.positive(); try { await check.mutate(); } catch { rejected += 1; } await check.positive(); }
  ok(rejected === 2, "KIW8_PRE_CONTROL_FALSIFICATION"); safeWrite("pre-control-result.json", { falsifiedControls: ["W8-NC-01", "W8-NC-02"], rejected }); console.log("KIW8_PRE_CONTROLS_OK");
}
function safePacket(value) { return { contractVersion: value.contractVersion, profile: value.profile, account: { ...safeId(value.accountId), last4: value.accountId.slice(-4) }, region: value.region, stack: value.stack, environment: value.environment, bucket: safeId(value.bucket), template: value.template, zips: value.zips, approvalToken: value.approvalToken }; }
function stdinJson() { return JSON.parse(readFileSync(0, "utf8")); }
function sanitize(mode) {
  const value = stdinJson(); let projected;
  if (mode === "sanitize-packet") { ok(value.mode === "DRY_RUN_NO_AWS" && value.phase === "full", "KIW8_DRY_RUN_MODE"); const { mode: _mode, phase: _phase, ...raw } = value; const expected = packet(raw.accountId); ok(canonical(raw) === canonical(expected), "KIW8_DRY_RUN_PACKET"); projected = { mode: value.mode, phase: value.phase, packet: safePacket(raw) }; }
  else if (mode === "sanitize-act01") { ok(value.outcome === "CHANGE_SET_REVIEWED", "KIW8_ACT01_OUTCOME"); const record = records(); ok(value.changeSetId === record.change.changeSetId, "KIW8_ACT01_ID"); projected = { outcome: value.outcome, contractVersion: value.contractVersion, approvalToken: value.approvalToken, phase: value.phase, changeSetName: value.changeSetName, changeSet: safeId(value.changeSetId), projectionSha256: record.sanitized.projectionSha256 }; }
  else if (mode === "sanitize-act02-full") { ok(value.outcome === "REVIEWED_CHANGE_SET_APPLIED" && value.phase === "full", "KIW8_ACT02_FULL_OUTCOME"); projected = { outcome: value.outcome, phase: value.phase, changeSet: safeId(value.changeSetId), projectionSha256: sha(canonical(validateChanges(value.changes))) }; }
  else if (mode === "sanitize-act02-activate-review") { ok(value.outcome === "CHANGE_SET_REVIEWED" && value.phase === "activate", "KIW8_ACT02_ACTIVATE_REVIEW_OUTCOME"); const record = activationRecord(); ok(value.changeSetId === record.value.changeSetId, "KIW8_ACTIVATION_REVIEW_ID"); projected = { outcome: value.outcome, phase: value.phase, changeSet: safeId(value.changeSetId), projectionSha256: record.sanitized.projectionSha256 }; }
  else if (mode === "sanitize-act02-activate-apply") { ok(value.outcome === "REVIEWED_CHANGE_SET_APPLIED" && value.phase === "activate", "KIW8_ACT02_ACTIVATE_APPLY_OUTCOME"); projected = { outcome: value.outcome, phase: value.phase, changeSet: safeId(value.changeSetId), projectionSha256: sha(canonical(validateActivationChanges(value.changes))) }; }
  else { const active = mode === "sanitize-inspector-active"; ok(mode === "sanitize-inspector-disabled" || active, "KIW8_INSPECT_MODE"); ok(value.outcome === (active ? "EXPECTED_ACTIVE_KEYWORD_STACK_VERIFIED" : "EXPECTED_DISABLED_KEYWORD_STACK_VERIFIED"), "KIW8_INSPECT_OUTCOME"); exactKeys(value, ["outcome", "identityVerified", "deployment", "resources", "queues", "dlqs", "functions", "mappings", "alarms", "keywordActive", "keywordSourceMessages", "keywordDlqMessages"], "KIW8_INSPECT_KEYS"); ok(value.identityVerified === true && value.deployment === "production" && value.resources === 82 && value.queues === 7 && value.dlqs === 7 && value.functions === 8 && value.mappings === 7 && value.alarms === 31 && value.keywordActive === active && value.keywordSourceMessages === 0 && value.keywordDlqMessages === 0, "KIW8_INSPECT_VALUE"); projected = value; }
  const result = safeWrite(`${mode}.json`, projected); console.log(`${mode.toUpperCase().replaceAll("-", "_")}_OK ${result.sha256}`);
}
function watermark(label) {
  ok(["act01", "act02"].includes(label), "KIW8_WATERMARK_LABEL");
  const events = aws(["cloudformation", "describe-stack-events", "--stack-name", STACK]).StackEvents || [];
  const latest = events[0]; safeWrite(`${label}-watermark.json`, { eventCount: events.length, latestTimestamp: latest?.Timestamp || null, latestEvent: latest?.EventId ? safeId(latest.EventId) : { present: false } }); console.log(`KIW8_${label.toUpperCase()}_WATERMARK_OK`);
}
function newEvent(events, watermarkValue) {
  const latest = events[0]; if (!latest) return false;
  if (!watermarkValue.latestTimestamp) return true;
  return String(latest.Timestamp) > String(watermarkValue.latestTimestamp) || (String(latest.Timestamp) === String(watermarkValue.latestTimestamp) && sha(latest.EventId || "") !== watermarkValue.latestEvent.sha256);
}
async function observe(label, index) {
  ok(Number.isInteger(index) && index >= 1 && index <= 12, "KIW8_POLL_INDEX");
  const mark = readJson(path.join(TMP, `${label}-watermark.json`));
  const eventsResult = aws(["cloudformation", "describe-stack-events", "--stack-name", STACK]);
  const stack = aws(["cloudformation", "describe-stacks", "--stack-name", STACK]).Stacks?.[0];
  const eventChanged = newEvent(eventsResult.StackEvents || [], mark);
  let value;
  if (label === "act01") {
    const expected = packet(process.env.KIW8_ACCOUNT_ID), objects = [expected.template, ...expected.zips].map((item) => { const result = aws(["s3api", "head-object", "--bucket", expected.bucket, "--key", item.key], { allowFailure: true }); if (result.failed) return { present: false, absent: result.absent, failure: result.stderrSha256 }; const exact = result.ContentLength === item.bytes && result.ServerSideEncryption === "AES256" && result.Metadata?.sha256 === item.sha256 && typeof result.VersionId === "string" && result.VersionId.length > 0; return { present: true, exact, bytes: result.ContentLength, encryption: result.ServerSideEncryption, metadataSha256: result.Metadata?.sha256 || null, version: result.VersionId ? safeId(result.VersionId) : { present: false } }; });
    const described = aws(["cloudformation", "describe-change-set", "--stack-name", STACK, "--change-set-name", `ki-full-${expected.approvalToken.slice(0, 12)}`], { allowFailure: true });
    let changeSet;
    if (described.failed) changeSet = { present: false, absent: described.absent, failure: described.stderrSha256 };
    else {
      const reviewed = await assertReviewedFull(described);
      changeSet = { present: true, id: safeId(described.ChangeSetId), status: described.Status, executionStatus: described.ExecutionStatus, projectionSha256: sha(canonical(reviewed)) };
    }
    value = { index, objects, changeSet, stackStatus: stack?.StackStatus, newEvent: eventChanged };
  } else {
    const record = readJson(path.join(ROOT, "email_scraper/dist/aws-deployment/keyword-intelligence/full-change-set.json"));
    const described = aws(["cloudformation", "describe-change-set", "--stack-name", STACK, "--change-set-name", record.changeSetId], { allowFailure: true });
    value = { index, changeSet: described.failed ? { present: false, failure: described.stderrSha256 } : { present: true, id: safeId(described.ChangeSetId), status: described.Status, executionStatus: described.ExecutionStatus }, stackStatus: stack?.StackStatus, newEvent: eventChanged };
  }
  safeWrite(`${label}-poll-${String(index).padStart(2, "0")}.json`, value); console.log(`KIW8_${label.toUpperCase()}_POLL_OK ${index}`);
}
function classifyAct01(values, loadLocalRecord = records) {
  const accepted = (item) => ACCEPTED_STACK_STATUSES.includes(item.stackStatus);
  const zero = values.every((item) => accepted(item) && item.objects.every((object) => object.present === false && object.absent === true) && item.changeSet.present === false && item.changeSet.absent === true && item.newEvent === false);
  const last = values.at(-1), prior = values.at(-2);
  const stable = canonical({ objects: last.objects, changeSet: last.changeSet, stackStatus: last.stackStatus, newEvent: last.newEvent }) === canonical({ objects: prior.objects, changeSet: prior.changeSet, stackStatus: prior.stackStatus, newEvent: prior.newEvent });
  const partialMember = (item) => accepted(item) && item.objects.some((object) => object.present) && item.objects.every((object) => object.present ? object.exact === true : object.absent === true) && item.changeSet.present === false && item.changeSet.absent === true && item.newEvent === false;
  const partial = partialMember(prior) && partialMember(last) && stable;
  let localExact = false;
  try { const local = loadLocalRecord(); localExact = last.changeSet.id.sha256 === local.sanitized.changeSet.sha256 && last.changeSet.projectionSha256 === local.sanitized.projectionSha256; } catch { localExact = false; }
  const complete = accepted(last) && last.newEvent === false && last.objects.every((item) => item.present && item.exact === true) && last.changeSet.present && last.changeSet.status === "CREATE_COMPLETE" && last.changeSet.executionStatus === "AVAILABLE" && localExact;
  return zero ? "ZERO_EFFECT_RECOVERY_ALLOWED" : partial ? "IDEMPOTENT_CONTINUATION_ALLOWED" : complete ? "RECONCILE_PRIVATE_RECORD" : "PARENT_BLOCKED_ACT01_AMBIGUOUS";
}
function classify(label) {
  const values = Array.from({ length: 12 }, (_, index) => readJson(path.join(TMP, `${label}-poll-${String(index + 1).padStart(2, "0")}.json`)));
  let outcome;
  if (label === "act01") outcome = classifyAct01(values);
  else {
    const available = values.every((item) => item.changeSet.present && item.changeSet.status === "CREATE_COMPLETE" && item.changeSet.executionStatus === "AVAILABLE" && item.newEvent === false && ["CREATE_COMPLETE", "UPDATE_COMPLETE"].includes(item.stackStatus));
    const latest = values.at(-1); outcome = available ? "ZERO_EFFECT_RECOVERY_ALLOWED" : latest.changeSet.executionStatus === "EXECUTE_IN_PROGRESS" || String(latest.stackStatus).endsWith("_IN_PROGRESS") ? "WAIT_WITHOUT_REEXECUTE" : latest.changeSet.executionStatus === "EXECUTE_COMPLETE" && latest.stackStatus === "UPDATE_COMPLETE" ? "INSPECT_WITHOUT_REEXECUTE" : String(latest.stackStatus).includes("ROLLBACK") || String(latest.stackStatus).includes("FAILED") ? "PARENT_BLOCKED_ACT02_ROLLBACK" : "PARENT_BLOCKED_ACT02_AMBIGUOUS";
  }
  safeWrite(`${label}-classification.json`, { polls: 12, intervalSeconds: 5, outcome }); console.log(`KIW8_${label.toUpperCase()}_CLASSIFICATION ${outcome}`);
}
function waitAct02() {
  aws(["cloudformation", "wait", "stack-update-complete", "--stack-name", STACK], { json: false });
  const stack = aws(["cloudformation", "describe-stacks", "--stack-name", STACK]).Stacks?.[0];
  const record = readJson(path.join(ROOT, "email_scraper/dist/aws-deployment/keyword-intelligence/full-change-set.json"));
  const described = aws(["cloudformation", "describe-change-set", "--stack-name", STACK, "--change-set-name", record.changeSetId]);
  ok(stack?.StackStatus === "UPDATE_COMPLETE" && described.ExecutionStatus === "EXECUTE_COMPLETE", "KIW8_ACT02_WAIT_TERMINAL");
  safeWrite("act02-wait.json", { stackStatus: stack.StackStatus, executionStatus: described.ExecutionStatus, changeSet: safeId(described.ChangeSetId) }); console.log("KIW8_ACT02_WAIT_OK");
}
function postInspect() {
  const stack = aws(["cloudformation", "describe-stacks", "--stack-name", STACK]).Stacks?.[0];
  ok(stack?.StackStatus === "UPDATE_COMPLETE", "KIW8_POST_STACK_STATUS");
  const template = readJson(path.join(ROOT, "email_scraper/infrastructure/aws/template.yaml")), expectedKeys = Object.keys(template.Outputs || {}).sort();
  const outputs = Object.fromEntries((stack.Outputs || []).map((item) => [item.OutputKey, item.OutputValue]));
  ok(canonical(Object.keys(outputs).sort()) === canonical(expectedKeys) && expectedKeys.length === 34, "KIW8_POST_OUTPUT_KEYS");
  const before = readJson(path.join(TMP, "p2-sanitized-act02.json")).outputHashes;
  for (const [key, value] of Object.entries(before)) ok(outputs[key] && sha(outputs[key]) === value.sha256, "KIW8_ESTABLISHED_OUTPUT_DRIFT");
  const added = expectedKeys.filter((key) => !(key in before));
  ok(canonical(added) === canonical(["KeywordResearchDlqArn", "KeywordResearchQueueArn", "KeywordResearchQueueUrl", "KeywordWorkerFunctionArn"]), "KIW8_KEYWORD_OUTPUT_SET");
  const outputHashes = Object.fromEntries(expectedKeys.map((key) => [key, safeId(outputs[key])]));
  const result = safeWrite("post-inspect.json", { stackStatus: stack.StackStatus, outputCount: 34, establishedOutputCount: Object.keys(before).length, addedOutputs: added, outputHashes }); console.log(`KIW8_POST_INSPECT_OK ${result.sha256}`);
}
function versions() {
  const nodeVersion = command("node", ["--version"], { json: false }); ok(/^v24\./u.test(nodeVersion), "KIW8_NODE_VERSION"); const awsVersion = command("aws", ["--version"], { json: false }); ok(/^aws-cli\/2\./u.test(awsVersion), "KIW8_AWS_CLI_VERSION"); safeWrite("versions.json", { nodeMajor: 24, awsCliMajor: 2 }); console.log("KIW8_VERSIONS_OK");
}
async function selftest() {
  ok(digest(CASES) === "3bd44b2c2c244b1dd29881dcfa249d9cdad5f9b1aecc981c56612d587283ca7e", "KIW8_CASE_DIGEST"); ok(digest(CONTROLS) === "9bd004917f960abb4842ea2f2da48ed60821fdedd55fcbc54dc7bdd271037ea6", "KIW8_CONTROL_DIGEST"); ok(digest(EXECUTION_PATHS) === "c0ae7c02ba529c538d22ae831637abbc199b53836428ec79f13fd844604057f9", "KIW8_PATH_DIGEST");
  const lifecycleRule = { ID: "AbortIncompleteMultipartUploads", Status: "Enabled", AbortIncompleteMultipartUpload: { DaysAfterInitiation: 7 } };
  for (const Filter of [undefined, {}, { Prefix: "" }]) validLifecycle({ Rules: [{ ...lifecycleRule, ...(Filter === undefined ? {} : { Filter }) }] });
  for (const Filter of [{ Prefix: "nonempty" }, { Prefix: "", Tag: { Key: "x", Value: "y" } }, []]) { let rejected = false; try { validLifecycle({ Rules: [{ ...lifecycleRule, Filter }] }); } catch { rejected = true; } ok(rejected, "KIW8_BUCKET_FILTER_CONTROL"); }
  const reviewed = fullDescriptionWithDependencies();
  await assertReviewedFull(structuredClone(reviewed));
  const wrongDependency = structuredClone(reviewed); wrongDependency.Changes.at(-1).ResourceChange.Details[0].CausingEntity = "RecoveryInvokePermission.Arn";
  let dependencyRejected = false; try { await assertReviewedFull(wrongDependency); } catch { dependencyRejected = true; } ok(dependencyRejected, "KIW8_OBSERVATION_DEPENDENCY_CONTROL");
  const activation = activationDescriptionWithDependencies();
  const activationProjection = await assertReviewedActivate(structuredClone(activation));
  validateActivationChanges(activationProjection.map((entry) => ({ action: entry.action, logicalId: entry.logicalId, type: entry.type, replacement: entry.replacement })));
  const wrongActivation = structuredClone(activation); wrongActivation.Changes[0].ResourceChange.Details[0].Target.Name = "BatchSize";
  let activationRejected = false; try { await assertReviewedActivate(wrongActivation); } catch { activationRejected = true; } ok(activationRejected, "KIW8_ACTIVATION_DETAIL_CONTROL");
  const deploymentSource = readFileSync(path.join(ROOT, "email_scraper/scripts/keyword-intelligence/create-change-set.js"), "utf8");
  ok(!deploymentSource.includes("W8-ACT-05") && /return "W8-ACT-02";/u.test(deploymentSource), "KIW8_ACT02_LABEL_CONTROL");
  const absentObject = { present: false, absent: true }, exactObject = { present: true, exact: true }, absentChange = { present: false, absent: true }, exactChange = { present: true, id: { present: true, sha256: "a".repeat(64) }, status: "CREATE_COMPLETE", executionStatus: "AVAILABLE", projectionSha256: "b".repeat(64) };
  const local = () => ({ sanitized: { changeSet: { present: true, sha256: "a".repeat(64) }, projectionSha256: "b".repeat(64) } });
  const zero = Array.from({ length: 12 }, (_, index) => ({ index: index + 1, objects: [absentObject, absentObject, absentObject], changeSet: absentChange, stackStatus: "CREATE_COMPLETE", newEvent: false }));
  const partial = Array.from({ length: 12 }, (_, index) => ({ index: index + 1, objects: [exactObject, absentObject, absentObject], changeSet: absentChange, stackStatus: "UPDATE_COMPLETE", newEvent: false }));
  const complete = Array.from({ length: 12 }, (_, index) => ({ index: index + 1, objects: [exactObject, exactObject, exactObject], changeSet: exactChange, stackStatus: "UPDATE_COMPLETE", newEvent: false }));
  ok(classifyAct01(zero, local) === "ZERO_EFFECT_RECOVERY_ALLOWED" && classifyAct01(partial, local) === "IDEMPOTENT_CONTINUATION_ALLOWED" && classifyAct01(complete, local) === "RECONCILE_PRIVATE_RECORD", "KIW8_ACT01_CLASSIFIER_POSITIVES");
  for (const [fixture, indexes] of [[zero, [0, 11]], [partial, [10, 11]], [complete, [11]]]) for (const status of ["UPDATE_IN_PROGRESS", "UPDATE_ROLLBACK_COMPLETE"]) { const mutant = structuredClone(fixture); for (const index of indexes) mutant[index].stackStatus = status; ok(classifyAct01(mutant, local) === "PARENT_BLOCKED_ACT01_AMBIGUOUS", "KIW8_ACT01_STACK_FENCE_CONTROL"); }
  console.log("KIW8_RUNNER_SELFTEST_OK");
}
function cleanup() { const base = realpathSync(TMP); ok(base.startsWith("/tmp/ki-w8-i101."), "KIW8_TMP_SCOPE_INVALID"); rmSync(base, { recursive: true, force: false }); console.log("KIW8_TMP_CLEANUP_OK"); }

const [mode, argument] = process.argv.slice(2);
try {
  if (mode === "selftest") await selftest(); else if (mode === "versions") versions(); else if (mode === "p2") p2(argument); else if (mode === "p3") quotas(); else if (mode === "records") records(); else if (mode === "activation-record") activationRecord(); else if (mode === "scope") scope(); else if (mode === "state-pins") statePins(argument); else if (mode === "pre-controls") await preControls(); else if (mode === "make-control-input") makeControlInput(); else if (mode === "controls") await controls(); else if (["sanitize-packet", "sanitize-act01", "sanitize-act02-full", "sanitize-act02-activate-review", "sanitize-act02-activate-apply", "sanitize-inspector-disabled", "sanitize-inspector-active"].includes(mode)) sanitize(mode); else if (mode === "watermark") watermark(argument); else if (mode === "observe") await observe(argument, Number(process.argv[4])); else if (mode === "classify") classify(argument); else if (mode === "wait-act02") waitAct02(); else if (mode === "post-inspect") postInspect(); else if (mode === "cleanup") cleanup(); else fail("KIW8_RUNNER_MODE");
} catch (error) { console.error(`KIW8_RUNNER_FAILED ${error?.code || error?.message || "UNKNOWN"}`); process.exitCode = 1; }
```
<!-- KIW8_RUNNER_END -->

Extracted runner bytes are exactly SHA-256
`4611115aa6c7fc3ae9448e44435051ad0e2abc6f85245f656613608bef5d47d0`.
P1 must reproduce this value before any AWS read.

The exact executable phase calls are frozen below. No prose-only projector,
private-record validator, certificate validator or control runner exists.

### 6.1 P1 — authority and immutable input preflight

From workspace root, run exactly:

```text
node "$KIW8_RUNNER" versions
sha256sum "$KIW8_RUNNER"
sha256sum PROJECT_AGNOSTIC_DECISION_COMPLETE_CHECKLIST_AUTHORING_STANDARD.md PROJECT_AGNOSTIC_WINDOW_AGENT_SUBWINDOW_AUTHORING_STANDARD.md KEYWORD_INTELLIGENCE_PRODUCT_CONTRACT.md KEYWORD_INTELLIGENCE_DISCOVERY_DOSSIER.md KEYWORD_INTELLIGENCE_DECISION_LEDGER.md KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md ACTIVE_EXECUTION_STATE.md KEYWORD_INTELLIGENCE_TRACEABILITY_INDEX.md KEYWORD_INTELLIGENCE_KI_W8_AWS_ONLY_SUBWINDOW_CHECKLIST.md
sha256sum email_scraper/infrastructure/aws/template.yaml email_scraper/dist/lambda/keyword-worker.zip email_scraper/dist/lambda/recovery.zip email_scraper/scripts/measure-keyword-worker-package.js email_scraper/scripts/measure-lambda-packages.js email_scraper/scripts/keyword-intelligence/create-change-set.js email_scraper/scripts/keyword-intelligence/inspect-stack.js
wc -c email_scraper/infrastructure/aws/template.yaml email_scraper/dist/lambda/keyword-worker.zip email_scraper/dist/lambda/recovery.zip
git status --short
git -C email_scraper status --short
git -C frontend status --short
```

Pass requires exact `KIW8_VERSIONS_OK`, Node `v24.x`, AWS CLI `v2.x`, the later
A5 execution assignment matching every inherited pin, exact Section 3
hashes/bytes, root changes consisting only of protected parent/subordinate
coordination paths, and empty nested porcelain. No build, measurement or AWS
network call runs in P1; `aws --version` is local process inspection.

### 6.2 P2 — exact target and stable starting stack

Run exactly:

```text
KIW8_EXPORTS="$(node "$KIW8_RUNNER" p2 initial)"
eval "$KIW8_EXPORTS"
unset KIW8_EXPORTS
```

The runner invokes, in this order, exact read-only CLI operations with literal
`--profile storesignal-dev --region ap-south-2 --no-cli-pager --output json`:
`sts get-caller-identity`; CloudFormation `describe-stacks`,
`list-stack-resources`, `list-change-sets`; then S3
`get-bucket-versioning`, `get-bucket-encryption`,
`get-public-access-block`, `get-bucket-ownership-controls`, and
`get-bucket-lifecycle-configuration`, each against the account-derived bucket.
The `eval` consumes five raw shell exports without displaying/retaining them;
the runner writes only `p2-sanitized-initial.json`.

In memory, require one 12-digit STS account; exactly one target stack whose
`StackId` account/region/stack agree; status `CREATE_COMPLETE` or
`UPDATE_COMPLETE`; every `StackResourceSummary.ResourceStatus` belongs exactly
to `{CREATE_COMPLETE,UPDATE_COMPLETE}` and every other value rejects;
`ArtifactBucketName` equals the derived bucket; and no change set in
`CREATE_PENDING|CREATE_IN_PROGRESS|CREATE_COMPLETE` with execution
`AVAILABLE|EXECUTE_IN_PROGRESS`. The derived bucket requires versioning
`Enabled`; exactly one AES256/default-encryption rule with bucket key false and
no KMS key; all four public-access booleans true; exactly one
`BucketOwnerEnforced` ownership rule; and exactly one lifecycle rule ID
`AbortIncompleteMultipartUploads`, status `Enabled`, seven-day incomplete
multipart abort, empty/absent filter/prefix, and zero expiration/transition
members. Any extra lifecycle rule or expiration rejects. The retained
projection is exactly the runner's `p2-sanitized-initial.json`: hashed account,
caller ARN, stack ID and bucket; account last4; status/count/status-set; zero
pending sets; and the literal normalized bucket-safety object.

The later action-resumption label `p2 act02` is the sole exception to the zero-
pending predicate: it requires exactly one `CREATE_COMPLETE/AVAILABLE` summary
whose raw ID/name equal the mode-0600 `full-change-set.json`, and retains only
its hash/presence. Any second or unequal active summary rejects.

### 6.3 P3 — account/service capability

Run exactly `node "$KIW8_RUNNER" p3`. The runner invokes exactly Lambda
`get-account-settings` followed by Service Quotas `list-service-quotas` for
`lambda`, `sqs`, and `cloudformation`, with the same literal CLI target flags.

The strict projector accepts only finite nonnegative numeric account/quota
members and emits sorted quota-name/value pairs plus these booleans, all true:

```text
unreservedConcurrentExecutions >= 101 before adding reserved concurrency 1
AccountUsage.FunctionCount is retained as informational usage; AWS Lambda's AccountLimit response has no FunctionCount member and no function-count capacity claim is made
remaining TotalCodeSize >= measured keyword-worker unzipped bytes + measured recovery unzipped bytes
keyword ZIP bytes = 32006605 <= 47185920; keyword/recovery expanded bytes each <= 209715200
template counts and fixed CloudFormation per-template limits = 82 resources <= 500, 34 outputs <= 200, 19 parameters <= 200
worker literals = timeout 180, memory 1024, ephemeral 512, reserved concurrency 1
source/DLQ literals = AES256 managed SSE true, 262144 message bytes, 1080 visibility, 345600/1209600 retention, redrive 5, long poll 20
mapping literals = batch 1, window 0, ReportBatchItemFailures
MaximumConcurrency is absent for the keyword mapping
```

The literal runner is the strict projector: it validates every returned Service
Quotas inventory member as a finite nonnegative value, performs the Lambda
account formulas above, validates the exact template counts/settings against
CloudFormation's fixed `500/200/200` limits, sorts
`{quotaCode,quotaName,value,unit}` by code and writes only
`p3-sanitized.json`. CloudFormation Service Quotas code `L-0485CB21` is stack
count, is retained only as part of the sanitized inventory, and is never used
as a resource-per-template or concurrent-resource proof. An absent/unreadable
inventory or insufficient Lambda account member is `PARENT_BLOCKED_CAPABILITY`;
no optimistic published default substitutes for it. A4 enumerates no
`describe-account-limits` read and requires no separate account-applied
concurrent-resource threshold, so I101 does not invent either.

### 6.4 P4 — accepted package and before projection

From `email_scraper/`, run exactly once each and do not rebuild:

```text
node scripts/measure-keyword-worker-package.js
node scripts/measure-lambda-packages.js
set -o pipefail
node scripts/keyword-intelligence/create-change-set.js --profile=storesignal-dev --region=ap-south-2 --stack=storesignal-production-pipeline --environment=production --phase=full --account-id=${KIW8_ACCOUNT_ID} | node "$KIW8_RUNNER" sanitize-packet
```

The first two commands may overwrite only the two authorized measurement JSONs.
Require Node 24; exact ZIP bytes/hashes; one
`libquery_engine-rhel-openssl-3.0.x.so.node`; safe inventory; ZIP ≤45 MiB;
expanded ≤200 MiB; exported cold-import handler function; and all seven
established ZIPs still present and within their accepted measurement rules. The
third command must emit `mode:"DRY_RUN_NO_AWS"`, perform zero AWS call/write,
and reproduce Section 3.2 exactly. P2's stack/resource/change-set projection is
the frozen before projection. Template/current established resource equality is
the accepted W7 evidence; live post-state equality is proved by the inspector.

### 6.5 P5 — zero pending/unapproved mutation

Recompute P1 source hashes and run exactly:

```text
KIW8_EXPORTS="$(node "$KIW8_RUNNER" p2 recheck)"
eval "$KIW8_EXPORTS"
unset KIW8_EXPORTS
```

The runner repeats the exact P2
read sequence and requires its complete sanitized projection byte-equal to the
initial projection. Prove no secret-value,
DataForSEO/provider, Neon, API, browser, local-server, Lambda-invoke or queue
data-plane operation occurred. Continue only to P6; LIVE-01 is not activated
before P6 passes.

### 6.6 P6 — write/action-scope closure

Run exactly `node "$KIW8_RUNNER" scope`. Recompute the parent-approved one-file
deployment-guard correction, ten-path execution-write set, zero additional
subordinate-write set, three-path authoring set and eleven-path union from Section 1 using the
sub-window standard's unsigned-UTF-8 sorted-member-LF formula. The runner
requires every root porcelain member in its literal protected list, frontend
porcelain empty, backend porcelain either clean after requester commit or the
one exact pinned deployment-guard path, and execution-set digest exact. Record exact
starting/ending digests of the two
measurement outputs and protected coordination paths. Then activate
`W8-LIVE-01`, append `EV-KI-W8-L01`, set S2 to
`AWAITING_REQUESTER_APPROVAL_ACT01`, run exactly
`node "$KIW8_RUNNER" cleanup`, and stop without ACT-01.

### 6.7 ACT-01 — upload and create/review only

After the requester approval and A5 pins Section 5.1, re-run the exact Section
6.0 bootstrap from workspace root, then run exactly:

```text
KIW8_EXPORTS="$(node "$KIW8_RUNNER" p2 initial)"
eval "$KIW8_EXPORTS"
unset KIW8_EXPORTS
node "$KIW8_RUNNER" state-pins W8-ACT-01
cd "$KIW8_ROOT/email_scraper"
node "$KIW8_RUNNER" watermark act01
set -o pipefail
node scripts/keyword-intelligence/create-change-set.js --profile=storesignal-dev --region=ap-south-2 --stack=storesignal-production-pipeline --environment=production --phase=full --account-id=${KIW8_ACCOUNT_ID} --execute | node "$KIW8_RUNNER" sanitize-act01
node "$KIW8_RUNNER" records
node "$KIW8_RUNNER" pre-controls
cd "$KIW8_ROOT"
KIW8_EXPORTS="$(node "$KIW8_RUNNER" p2 act02)"
eval "$KIW8_EXPORTS"
unset KIW8_EXPORTS
```

Activation witness: exit zero and output `outcome:"CHANGE_SET_REVIEWED"`; three
object records each reconcile exact bytes/hash/key/metadata/encryption/version;
`packet.json`, `artifacts.json` and `full-change-set.json` are mode 0600 and
strict exact-key schemas; the stable change-set ID is unexecuted and its direct
plus optional projection passes Section 3.3. `pre-controls` runs the literal
NC-01/02 positive→mutant-rejects→fresh-positive oracles. Then append
`EV-KI-W8-L02` using only `sanitize-act01.json`, `records-sanitized.json` and
`pre-control-result.json`; pin the resulting `p2-sanitized-act02.json` digest
for the separate ACT-02 approval; activate
`W8-LIVE-02`, run exactly `node "$KIW8_RUNNER" cleanup`, and stop for ACT-02
approval.

If action output/transport is lost, first prove no matching local process, then
run exactly this observation schedule from workspace root (the watermark was
captured immediately before the action):

```text
for KIW8_POLL_INDEX in 1 2 3 4 5 6 7 8 9 10 11 12; do node "$KIW8_RUNNER" observe act01 "$KIW8_POLL_INDEX"; if test "$KIW8_POLL_INDEX" != 12; then sleep 5; fi; done
node "$KIW8_RUNNER" classify act01
```

This performs 12 read-only observations at five-second intervals. Each polls
the three exact head-object keys, deterministic change-set name, stack status
and stack events, retaining only hashes/cardinalities/status and comparison to
the pre-action event watermark. Apply this exclusive classifier result:

1. `ZERO_EFFECT_RECOVERY_ALLOWED` occurs only when all 12 polls show stack
   status exactly `CREATE_COMPLETE` or `UPDATE_COMPLETE`, all three keys absent
   through classified not-found responses, the deterministic change set absent,
   and no post-watermark event; it permits the one identical E8.1 recovery;
2. one-to-three matching objects, every present object passing the exact
   script conflict guard, no unequal/latest version and no deterministic change
   set, both final observations have stack status exactly `CREATE_COMPLETE` or
   `UPDATE_COMPLETE` and no post-watermark event, and those final two sanitized
   observations are byte-identical permits one identical idempotent ACT-01
   continuation; it reuses present
   content-addressed objects and completes missing members, and remains the
   original action-ledger member rather than a second action;
3. `RECONCILE_PRIVATE_RECORD` requires final stack status exactly
   `CREATE_COMPLETE` or `UPDATE_COMPLETE`, no post-watermark event, three exact
   objects, byte-valid local packet/artifact/change-set records and one exact
   remote `CREATE_COMPLETE/AVAILABLE` reviewed change set; only then is it
   accepted without another write;
4. an exact remote change set with no byte-valid exact local change-set record,
   multiple/unequal object or change-set identity, any failed/in-progress stack
   status in an otherwise zero/partial/complete branch, failed change-set
   creation, or any unclassified partial state is
   `PARENT_BLOCKED_ACT01_AMBIGUOUS`.

For only `IDEMPOTENT_CONTINUATION_ALLOWED`, preserve the original watermark and
run exactly the deployment-pipe, `records`, `pre-controls`, and post-ACT-01
`p2 act02` commands already printed in the primary block; do not rerun
`watermark act01`. For only `ZERO_EFFECT_RECOVERY_ALLOWED`, the one E8.1
recovery reruns the complete primary block with a new pre-action watermark.
Never create a second change set or manually synthesize a missing record.

### 6.8 ACT-02 — apply the reviewed full ID, then review/apply activation

After the requester approval and A5 pins Section 5.2, re-run the exact Section
6.0 bootstrap from workspace root, then run:

```text
KIW8_EXPORTS="$(node "$KIW8_RUNNER" p2 act02)"
eval "$KIW8_EXPORTS"
unset KIW8_EXPORTS
node "$KIW8_RUNNER" state-pins W8-ACT-02
cd "$KIW8_ROOT/email_scraper"
node "$KIW8_RUNNER" watermark act02
set -o pipefail
node scripts/keyword-intelligence/create-change-set.js --profile=storesignal-dev --region=ap-south-2 --stack=storesignal-production-pipeline --environment=production --phase=full --account-id=${KIW8_ACCOUNT_ID} --execute --apply-reviewed-change-set | node "$KIW8_RUNNER" sanitize-act02-full
node scripts/keyword-intelligence/inspect-stack.js --profile=storesignal-dev --region=ap-south-2 --stack=storesignal-production-pipeline --account-id=${KIW8_ACCOUNT_ID} --expected-disabled | node "$KIW8_RUNNER" sanitize-inspector-disabled
node scripts/keyword-intelligence/create-change-set.js --profile=storesignal-dev --region=ap-south-2 --stack=storesignal-production-pipeline --environment=production --phase=activate --account-id=${KIW8_ACCOUNT_ID} --execute | node "$KIW8_RUNNER" sanitize-act02-activate-review
node "$KIW8_RUNNER" activation-record
node scripts/keyword-intelligence/create-change-set.js --profile=storesignal-dev --region=ap-south-2 --stack=storesignal-production-pipeline --environment=production --phase=activate --account-id=${KIW8_ACCOUNT_ID} --execute --apply-reviewed-change-set | node "$KIW8_RUNNER" sanitize-act02-activate-apply
node scripts/keyword-intelligence/inspect-stack.js --profile=storesignal-dev --region=ap-south-2 --stack=storesignal-production-pipeline --account-id=${KIW8_ACCOUNT_ID} --expected-active | node "$KIW8_RUNNER" sanitize-inspector-active
node "$KIW8_RUNNER" post-inspect
```

The first command may execute only the recorded full ID after source, A5 and
live-description equality. The disabled inspector must pass before activation
creation. The deterministic activation set must pass the production
`assertReviewedChanges("activate", ...)` guard and the private-record validator;
only that recorded ID may then execute. The final active inspector must emit the
exact Section 3.4 active object and its internal complete-topology assertions
must pass. `post-inspect` hashes all 34
output values, proves every established output hash unchanged and the exact
four keyword outputs added; no raw ARN/URL is retained. Append `EV-KI-W8-L03`,
activate `W8-LIVE-03`, then run the conformance gate.

An observable full-apply failure stops before activation. An observable
activation-create failure leaves the verified disabled stack and stops. An
observable activation-apply failure is reconciled read-only and must leave the
stack disabled or in CloudFormation's automatic rollback state; it stops. Loss
of transport at either activation boundary is
`PARENT_BLOCKED_ACT02_AMBIGUOUS` unless one exact deterministic remote/local ID
and terminal stack status can be proven without another create or execute. No
replacement change set, manual repair, direct Lambda invocation, queue action
or application request is permitted.

For lost execute response, after proving no matching local process run exactly:

```text
for KIW8_POLL_INDEX in 1 2 3 4 5 6 7 8 9 10 11 12; do node "$KIW8_RUNNER" observe act02 "$KIW8_POLL_INDEX"; if test "$KIW8_POLL_INDEX" != 12; then sleep 5; fi; done
node "$KIW8_RUNNER" classify act02
```

The runner makes 12 read-only `describe-change-set`, `describe-stacks`, and
`describe-stack-events` observations at five-second intervals against the
private-record ID, retaining only status, hashed ID and pre-action-watermark
comparison. `ZERO_EFFECT_RECOVERY_ALLOWED` requires all 12 remain
`CREATE_COMPLETE/AVAILABLE`, the stack remain accepted-complete, and zero new
event; only then may the identical original ACT-02 pipeline run once.
`WAIT_WITHOUT_REEXECUTE` runs exactly `node "$KIW8_RUNNER" wait-act02` and never
executes again, then runs the inspector pipeline plus `post-inspect`.
`INSPECT_WITHOUT_REEXECUTE` runs only the inspector pipeline plus
`post-inspect`.
A rollback/failure classification is `PARENT_BLOCKED_ACT02_ROLLBACK`; an
unequal/unclassified state is `PARENT_BLOCKED_ACT02_AMBIGUOUS`. No second
execute, change set, manual repair, rollback mutation or deletion is permitted.

## 7. Enforcement coverage, controls and substitute fidelity

### 7.1 Required sets

Required cases are exactly:

```text
W8-CONF-01
W8-LIVE-01
W8-LIVE-02
W8-LIVE-03
```

Count 4; digest
`3bd44b2c2c244b1dd29881dcfa249d9cdad5f9b1aecc981c56612d587283ca7e`.

Required controls are exactly `W8-NC-01` through `W8-NC-08`, count 8; digest
`9bd004917f960abb4842ea2f2da48ed60821fdedd55fcbc54dc7bdd271037ea6`.
Each case registers exactly once before its phase but enters `executed` and
`activated` only after its unique witness and oracle pass.

| ID | Registration and activation witness | Exact oracle |
|---|---|---|
| `W8-LIVE-01` | I101 P1–P6, final P5 stable read | all pins/target/capability/package/before/scope checks pass; zero mutation |
| `W8-LIVE-02` | ACT-01 exit/reconciled record | exact three object versions and one allowlisted unexecuted change set |
| `W8-LIVE-03` | ACT-02 final inspector | exact full and activation IDs applied and Section 3.4 expected-active state |
| `W8-CONF-01` | frozen runner `make-control-input` then `controls` | case equality 4, controls 8, exact digests/action ledger, every forbidden count zero |

| Control | One in-memory captured mutation | Unchanged guard that must throw/reject |
|---|---|---|
| `W8-NC-01` | replace template SHA in a deep-cloned dry-run packet with 64 zeroes | Section 3.1/3.2 packet equality before AWS write |
| `W8-NC-02` | append `{Action:"Add",LogicalResourceId:"Unlisted",ResourceType:"AWS::SQS::Queue",Replacement:null}` to a deep-cloned valid full description | exported `assertReviewedChanges("full", value)` allowlist |
| `W8-NC-03` | remove `W8-LIVE-02` from registered cases | required/registered exact equality |
| `W8-NC-04` | add `W8-LIVE-03` to skipped cases | zero required skips |
| `W8-NC-05` | append a second `W8-LIVE-02` execution record | duplicate-ID rejection before set conversion |
| `W8-NC-06` | remove `EV-KI-W8-L03` from live evidence while retaining executed LIVE-03 | executed/activated/evidence equality |
| `W8-NC-07` | delete `forbiddenCounts.provider` from a deep clone | exact certificate-key/schema and all-zero forbidden map |
| `W8-NC-08` | replace LIVE-03 projection digest with a fabricated digest not equal to retained inspector output | live-evidence digest/fidelity equality |

Controls run positive → one mutation must reject → fresh positive. They mutate
only memory or `/tmp`; they perform zero AWS write and never alter production or
workspace source.

### 7.2 Final certificate schema

The final `KI-W8-EXECUTION-PASS` object is exactly the JSON schema printed in
A4: sorted required/registered/executed/activated arrays all equal the four
members; empty skipped/duplicate/unexpected arrays; sorted required/falsified
controls equal all eight; exact two digests; liveEvidence exactly maps the
three LIVE IDs to `EV-KI-W8-L01/L02/L03`; actionLedger exactly
`["W8-ACT-01","W8-ACT-02"]`; and forbiddenCounts has exactly the eleven A4
keys, all numeric zero. Extra, missing, wrong-type, reordered ledger or
unresolved evidence members reject. The validator first rejects duplicate raw
IDs, then recomputes sets and digests from raw members, never from stored
counts/digests.

### 7.3 Substitute fidelity

| Production boundary | Assessment mechanism | Proven claim | Claim not supported |
|---|---|---|---|
| local packet/source bytes | real `buildDeploymentPacket` dry run and measurement scripts | accepted bytes, identities, inventory, handler import | AWS object or deployment state |
| change-set allowlist | real exported `assertReviewedChanges` plus live described change set | accepted normalized change inventory and rejection | CloudFormation apply success before ACT-02 |
| AWS identity/quota/stack | real AWS CLI read calls | applied account facts returned at execution time | secret/provider/database capability |
| deployed topology | real disabled-intermediate and active-final inspector modes | read-only current AWS resource/config/IAM/alarm/empty-queue equality and exact active flag/mapping | research, provider or local control plane |
| CloudFormation transaction | real reviewed-ID execute, wait/status/events | applied or automatic-rollback state of that exact update | future activation or rollback mutation |

No fake supports a live claim. A fabricated summary is rejected by NC-08.
W7 source/tests/template/ZIPs are immutable inputs; changing any invalidates P1
and all later gates.

### 7.4 Literal conformance and cleanup commands

Each live evidence entry appended to A6 and S3 has exactly these safe scalar
lines in addition to its sanitized command/outcome narrative:

```text
sanitized_projection_sha256: <64 lowercase hex>
```

`EV-KI-W8-L02` additionally has exactly:

```text
falsified_controls: [W8-NC-01, W8-NC-02]
```

After LIVE-03 evidence exists, run exactly from workspace root:

```text
cd "$KIW8_ROOT"
node "$KIW8_RUNNER" make-control-input
node "$KIW8_RUNNER" controls
node "$KIW8_RUNNER" scope
```

`make-control-input` constructs the fixed certificate data and reads the three
literal A6 evidence members; the executor authors no test logic. `controls`
requires the ACT-01 control evidence, executes NC-03–08 as
positive→one-mutant-rejects→fresh-positive, reuses the real production
`assertReviewedChanges` for NC-02 fidelity, and emits only the sanitized
four-case/eight-control result. Retain only the printed safe projection hashes,
run exactly `node "$KIW8_RUNNER" cleanup`, and only after cleanup succeeds
append `EV-KI-W8-C01`, the exact final certificate and handoff evidence to
A6/S3. A cleanup failure is `PARENT_BLOCKED`; it never permits deleting any
workspace or AWS member.

## 8. Frozen gate schedule and run limits

| Gate | Exact content | Limit | Invalidation | Evidence |
|---|---|---:|---|---|
| `G-W8-01` | P1 then P2/P3 then P4 then P5/P6; LIVE-01 | once after execution assignment | any authority/source/package/stack/quota/scope drift | `EV-KI-W8-L01` |
| `G-W8-02` | ACT-01 plus NC-01/02; LIVE-02 | one approved action; no repeat after observable effect | no edit allowed; ambiguity uses 6.7 | `EV-KI-W8-L02` |
| `G-W8-03` | ACT-02 full apply → disabled inspector → activation review/apply → active inspector; LIVE-03 | one approved sequence; no repeated create/execute after observable effect | no edit allowed; ambiguity uses 6.8 | `EV-KI-W8-L03` |
| `G-W8-04` | NC-03–08, certificate set/digest/action/privacy/scope checks; CONF-01 | once after LIVE-03 | any evidence/certificate/state change | `EV-KI-W8-C01` |

Measurement, stateful AWS and broad inspection gates do not run per leaf because
there are no leaves. A source or authority edit invalidates all four. A
measurement-output-only rewrite by the prescribed P4 scripts invalidates no
source pin. An external AWS change after LIVE-03 invalidates LIVE-03 and blocks
handoff; W8 does not repair it.

## 9. I101 completion, correction and handoff

### 9.1 Assessment checkboxes

- [ ] `I101-I1` Verify zero file/corrective leaves exist and the parent approved this exact decomposition revision. Evidence destination: next append-only I101 entry in S3.
- [ ] `I101-I2` Verify the empty implementation set and all parent/subordinate write/action scopes. Evidence destination: next append-only I101 entry in S3.
- [ ] `I101-I3` Execute P1–P6 in exact order under a preflight-only A5 assignment and activate LIVE-01. Evidence destination: `EV-KI-W8-L01` in A6 and the corresponding I101 entry in S3.
- [ ] `I101-I4` Stop, obtain ACT-01 approval/pins, execute only G-W8-02, then stop for ACT-02. Evidence destination: `EV-KI-W8-L02` in A6 and the corresponding I101 entry in S3.
- [ ] `I101-I5` Obtain ACT-02 approval/pins, execute only G-W8-03, and require the complete applied-disabled oracle. Evidence destination: `EV-KI-W8-L03` in A6 and the corresponding I101 entry in S3.
- [ ] `I101-I6` Execute all eight negative controls and prove each unchanged acceptance guard rejects its one mutation. Evidence destination: `EV-KI-W8-C01` in A6 and the corresponding I101 entry in S3.
- [ ] `I101-I7` Verify required=registered=executed=activated cases, required=falsified controls, zero skips/duplicates/unexpected/unactivated and both digests. Evidence destination: final I101 integration certificate in S3.
- [ ] `I101-I8` Verify substitute fidelity, W7 input immutability, exact action ledger, zero forbidden operations and no accepted-evidence invalidation. Evidence destination: final I101 integration certificate in S3.
- [ ] `I101-I9` Independently inspect all retained projections and complete workspace/AWS action diff; do not rely on command summaries. Evidence destination: final I101 integration certificate in S3.
- [ ] `I101-I10` Record exactly `PASS`, `CORRECTION_REQUIRED`, or `PARENT_BLOCKED` with decisive evidence. Evidence destination: final I101 integration certificate in S3.

### 9.2 Parent A4 verification and handoff checkboxes

- [ ] `KI-W8-V1` P1–P5 pass with exact source/package/target/quota/before-state evidence and zero mutation. Evidence destination: `EV-KI-W8-L01` in A6.
- [ ] `KI-W8-V2` ACT-01 produces/reconciles exactly three accepted object versions and one reviewed, unexecuted, allowlisted disabled change set. Evidence destination: `EV-KI-W8-L02` in A6.
- [ ] `KI-W8-V3` ACT-02 applies the exact full ID, passes expected-disabled inspection, applies the exact reviewed activation ID, and passes expected-active inventory/config/IAM/output/queue/DLQ inspection. Evidence destination: `EV-KI-W8-L03` in A6.
- [ ] `KI-W8-V4` Four-case/eight-control equality/digests, exact ACT-01→ACT-02 ledger and all-zero forbidden counts pass. Evidence destination: `EV-KI-W8-C01` in A6.
- [ ] `KI-W8-H1` Record exact changed/generated paths and prove no source/test/schema/migration/package-lock/frontend path changed. Evidence destination: KI-W8 handoff entry in A6.
- [ ] `KI-W8-H2` Append sanitized commands, approvals, identities, projections, outcomes, rollback status, residuals, coverage/digests and W9 prerequisites to A6. Evidence destination: KI-W8 handoff entry in A6.
- [ ] `KI-W8-H3` Prove workspace diff/status and AWS action ledger equal the exact authorized scopes. Evidence destination: KI-W8 handoff entry in A6.
- [ ] `KI-W8-H4` Prove no secret read, provider/database/API/browser/local-server/paid/destructive or unapproved activation action. Evidence destination: KI-W8 handoff entry in A6.
- [ ] `KI-W8-H5` Append execution/enforcement certificates and CAS A5 one version to `AWAITING_REVIEW`, retaining `accepted_through:KI-W7`, `next_window:null`, `may_start_successor:false`. Evidence destination: KI-W8 handoff entry in A6 and one-version A5 CAS.
- [ ] `KI-W8-H6` Stop with active AWS keyword infrastructure and no successor window. Evidence destination: final I101 integration certificate in S3.

### 9.3 Result classification

- `PASS`: every I101, V1–V4 and H1–H6 box passes; certificate exact; S2 becomes
  `READY_FOR_PARENT_REVIEW`.
- `CORRECTION_REQUIRED`: only an append-only S2/S3/A6 transcription defect
  whose exact corrected bytes are already dictated by this S1 and require no
  command/action rerun. The window agent appends a superseding evidence/state
  entry within existing I101; S1 remains byte-identical. Any validator,
  schedule, command, action or scope change is instead `PARENT_BLOCKED`.
- `PARENT_BLOCKED`: source/A4 contradiction, capability/identity absence,
  object/change-set conflict, observable AWS failure/rollback, unexplained
  ambiguity, expanded scope/decision or any needed implementation/AWS action
  outside ACT-01/02. Stop with one blocker.

## 10. Requirement and decision trace closure

| Parent trace | I101 owner | Executable closure |
|---|---|---|
| `REQ-KI-002/005/022`–`024`; `INV-KI-001/002/012`; `AUTH-KI-005`; `EXC-KI-008` | P1–P6, ACT-01/02 | `SCN-KI-049`; LIVE-01–03; zero active/provider/database behavior |
| `DEC-KI-059` packet, disabled allowlist, topology/IAM and inspector | Sections 3, 6.4, 6.7, 6.8 | LIVE-02/03; NC-01/02/08 |
| `DEC-KI-060` two-action AWS-first boundary | Sections 1, 4, 5, 8 | action ledger exactly ACT-01→ACT-02; NC-07; H4/H6 |
| A4 P1–P6 | G-W8-01 | LIVE-01/V1 |
| A4 T1 | G-W8-02 | LIVE-02/V2 |
| A4 T2 | G-W8-03 | LIVE-03/V3 |
| A4 V4/H1–H6 | G-W8-04 | CONF-01, NC-03–08, parent handoff |

Unmapped requirements: 0. Unmapped decisions: 0. Unmapped tasks: 0. Unmapped
scenario members: 0. Unmapped cases: 0. Unmapped controls: 0. Unknown consumed
payload fields: 0. No durable database, provider payload, owner identity,
browser substitute or application workflow is reachable in W8.

## 11. Mandatory decomposition-readiness checklist

### 11.1 Authority and inheritance

- [x] `SW-A01` Parent assignment, window agent identity and zero-leaf authority are exact/current. Evidence: `EV-KI-W8-AWS-S007`.
- [x] `SW-A02` Both standards and A1/A3/A4/A5 revisions are pinned/recomputed. Evidence: `EV-KI-W8-AWS-S007`.
- [x] `SW-A03` Parent write/read/action/prohibition/successor boundaries are copied without expansion. Evidence: `EV-KI-W8-AWS-S008`.
- [x] `SW-A04` Root/backend/frontend dirty state and protected parent changes are inventoried. Evidence: `EV-KI-W8-AWS-S007`.
- [x] `SW-A05` S1/S2/S3 authorities are distinct and all paths exist after authoring. Evidence: `EV-KI-W8-AWS-S009`.
- [x] `SW-A06` No implementation subagent, delegation or direct leaf-parent communication exists. Evidence: `EV-KI-W8-AWS-S008`.
- [x] `SW-A07` E8.1 is inherited without external-authority expansion. Evidence: `EV-KI-W8-AWS-S008`.

### 11.2 Decision and file-set closure

- [x] `SW-D01` Every parent requirement/decision/task/scenario/case/control is allocated to I101 assertions. Evidence: `EV-KI-W8-AWS-S008`.
- [x] `SW-D02` The P4 output-scope contradiction was parent-corrected by EV-KI-A-129; no missing parent decision remains. Evidence: `EV-KI-W8-AWS-S007`.
- [x] `SW-D03` Required implementation changed-file set equals the empty planned initial set. Evidence: `EV-KI-W8-AWS-S008`.
- [x] `SW-D04` Zero planned files have zero initial owners; no multi-file leaf exists. Evidence: `EV-KI-W8-AWS-S008`.
- [x] `SW-D05` Generated/admin files, baselines, operations and prohibited edits are exact. Evidence: `EV-KI-W8-AWS-S007`.
- [x] `SW-D06` The graph is the acyclic singleton I101; every phase is strictly sequential. Evidence: `EV-KI-W8-AWS-S008`.
- [x] `SW-D07` Packet/change-set/inspector interfaces are frozen before execution. Evidence: `EV-KI-W8-AWS-S008`.
- [x] `SW-D08` Every approval pause/intermediate state and failure branch is exact. Evidence: `EV-KI-W8-AWS-S008`.
- [x] `SW-D09` N/A: no production/test/fixture/schema/config/manifest implementation file is changed. Evidence: `EV-KI-W8-AWS-S008`.
- [x] `SW-D10` Commands write only the nine execution paths with S2/S3 owned once; S1 is immutable and `/tmp` validator output is sanitized/owned. Evidence: `EV-KI-W8-AWS-S009`.

### 11.3 Sub-window execution completeness

- [x] `SW-E01` N/A: no FILE/CORRECTION leaf; I101 contains all Section 9.2 assessment fields. Evidence: `EV-KI-W8-AWS-S008`.
- [x] `SW-E02` I101 uses exact commands/branches and delegates no design alternative. Evidence: `EV-KI-W8-AWS-S008`.
- [x] `SW-E03` P1–P6/T1/T2 have exact setup, activation witnesses, oracles and forbidden outcomes. Evidence: `EV-KI-W8-AWS-S008`.
- [x] `SW-E04` N/A for leaves; I101 separately proves empty implementation and exact admin/generated write sets. Evidence: `EV-KI-W8-AWS-S008`.
- [x] `SW-E05` I101 evidence, approval pauses, stop and parent successor reservation are exact. Evidence: `EV-KI-W8-AWS-S008`.
- [x] `SW-E06` No subagent exists; only window agent updates S1–S3 and reports to parent. Evidence: `EV-KI-W8-AWS-S008`.
- [x] `SW-E07` No successor work satisfies W8 acceptance. Evidence: `EV-KI-W8-AWS-S008`.
- [x] `SW-E08` No successor-window facts are required; active W8 facts have exact fail-closed branches. Evidence: parent DECOMP-5 audit.

### 11.4 Enforcement and integration closure

- [x] `SW-V01` All four cases/eight controls map to I101 registrations/witnesses/assertions. Evidence: `EV-KI-W8-AWS-S008`.
- [x] `SW-V02` Exact set equality, raw duplicate checks and both digests are frozen. Evidence: `EV-KI-W8-AWS-S009`.
- [x] `SW-V03` Every W8 critical invariant has one named NC-01–08 control. Evidence: `EV-KI-W8-AWS-S008`.
- [x] `SW-V04` Packet/allowlist/AWS/inspector substitutes and W7 invalidation rules are exact. Evidence: `EV-KI-W8-AWS-S008`.
- [x] `SW-V05` I101 is fully authored with zero implementation-file write authority. Evidence: `EV-KI-W8-AWS-S008`.
- [x] `SW-V06` Four final gates are sequential, bounded and invalidation-aware. Evidence: `EV-KI-W8-AWS-S008`.
- [x] `SW-V07` Coordination correction versus parent blocker routing is exact. Evidence: `EV-KI-W8-AWS-S008`.
- [x] `SW-V08` The same window agent personally executes/inspects I101. Evidence: `EV-KI-W8-AWS-S008`.
- [x] `SW-V09` Zero-work/bypass/skips/duplicates/unactivated/summary-only evidence cannot pass. Evidence: `EV-KI-W8-AWS-S009`.
- [x] `SW-V10` Parent handoff and READY_FOR_PARENT_REVIEW boundary are exact. Evidence: `EV-KI-W8-AWS-S008`.
- [x] `SW-V11` E8.1 permits one identical local transport recovery and rejects real/external failures. Evidence: `EV-KI-W8-AWS-S009`.

### 11.5 Mechanical and adversarial audit

- [x] `SW-R01` All subordinate IDs are unique and all references resolve. Evidence: `EV-KI-W8-AWS-S009`.
- [x] `SW-R02` No unresolved placeholder exists in checked/assignable content; `${...}` values are explicitly observed/pinned identities. Evidence: `EV-KI-W8-AWS-S009`.
- [x] `SW-R03` No FILE sub-window exists; a synthetic FILE sub-window with zero, two, wildcard, directory, rename or incidental-output write members fails lint. Evidence: `EV-KI-W8-AWS-S009`.
- [x] `SW-R04` Removing I101 or one parent trace makes readiness fail. Evidence: `EV-KI-W8-AWS-S009`.
- [x] `SW-R05` Removing/duplicating/skipping/filtering/unactivating any required case fails certificate validation. Evidence: `EV-KI-W8-AWS-S009`.
- [x] `SW-R06` Weakening forbidden counts or fabricating inspector evidence fails NC-07/08. Evidence: `EV-KI-W8-AWS-S009`.
- [x] `SW-R07` A second workspace path or direct leaf-parent communication is rejected. Evidence: `EV-KI-W8-AWS-S009`.
- [x] `SW-R08` I101 cannot repair implementation; scope/decision failure returns PARENT_BLOCKED. Evidence: `EV-KI-W8-AWS-S009`.
- [x] `SW-R09` S2 cannot leave STOP until parent decomposition approval is recorded. Evidence: `EV-KI-W8-AWS-S009`.
- [x] `SW-R10` Deterministic document lint reports zero missing fields/mappings/cases/evidence/authority conflicts. Evidence: `EV-KI-W8-AWS-S009`.
- [x] `SW-R11` Sandbox-only invalidation permits one identical recovery; changed commands, real failures and AWS effects reject. Evidence: `EV-KI-W8-AWS-S009`.

DECOMP-4 adversarial lint additionally mutates the optional dependency detail
and each zero-effect/partial/complete ACT-01 fixture to both in-progress and
failed stack statuses. The unchanged production guard/classifier rejects every
mutant before a recovery, continuation or reconciliation result can be emitted.

Checked mandatory authoring items: 47. Unchecked: 0.

## 12. Append-only amendments

No amendment exists. After parent approval, the original decomposition above is
immutable and S1 is read-only. Any genuine coordination, validator, action or
scope defect returns `PARENT_BLOCKED` for a parent-authored superseding
decomposition revision; the window agent does not append a corrective block to
S1. No supersession can authorize application work or an implementation edit implicitly.
