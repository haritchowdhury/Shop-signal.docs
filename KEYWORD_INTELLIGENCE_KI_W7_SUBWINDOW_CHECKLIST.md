# KI-W7 Sub-Window Decomposition Checklist (`S1`)

**Decomposition ID:** `KI-W7-DECOMP-1`  
**Parent window:** `KI-W7`  
**Parent assignment:** `ASG-KI-W7-WA-01`  
**Window agent:** `KI-W7-WINDOW-AGENT`

This is the frozen subordinate decomposition authority for `KI-W7`. It cannot
broaden `A1`-`A8` or `ACTIVE_EXECUTION_STATE.md`. Live subordinate assignment
exists only in `KEYWORD_INTELLIGENCE_KI_W7_SUBWINDOW_STATE.md` (`S2`); all
decomposition, execution, review, correction, and assessment evidence exists
only in `KEYWORD_INTELLIGENCE_KI_W7_SUBWINDOW_EVIDENCE.md` (`S3`).

No implementation leaf is assigned by this document. Parent decomposition
review is mandatory before `S2` may become `READY`.

## 0. Inherited authority and revision pins

| Authority | Path | Lowercase SHA-256 |
|---|---|---|
| Parent standard | `PROJECT_AGNOSTIC_DECISION_COMPLETE_CHECKLIST_AUTHORING_STANDARD.md` | `cda352017e75c0d11f6797d9fbe108b4365508cd38b0e92365cfb523ede32848` |
| Sub-window standard | `PROJECT_AGNOSTIC_WINDOW_AGENT_SUBWINDOW_AUTHORING_STANDARD.md` | `842c29550c06c22d63e0a058a27cb8a9ff6b538b3168d2c83a384890b44247f0` |
| `A1` contract | `KEYWORD_INTELLIGENCE_PRODUCT_CONTRACT.md` | `8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c` |
| `A2` discovery | `KEYWORD_INTELLIGENCE_DISCOVERY_DOSSIER.md` | `493192fc317c00ee43e277e85e00718985190cdd5c21e3d6824f67dd1d0b7c0c` |
| `A3` decisions | `KEYWORD_INTELLIGENCE_DECISION_LEDGER.md` | `6c0809225ba5336dc923786674b990f83c8db2496b88016f7655a770afb7e307` |
| `A4` checklist | `KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md` | `4a47d782223e372d2df7d653add494880eddf456ab3f4d63439fea2ed1c2374e` |
| `A5` state v195 | `ACTIVE_EXECUTION_STATE.md` | `3a63c9278ce68ae3a7c05e14a56f3ded4d3e3166bc0af7daea768e3b826dc7f1` |
| `A6` parent evidence | `KEYWORD_INTELLIGENCE_EXECUTION_EVIDENCE.md` | `48a5f5c7a23db49c61693c96f4f88ced5afb5231233c8bbc16e516f74f217510` |
| `A7` changelog | `KEYWORD_INTELLIGENCE_SPECIFICATION_CHANGELOG.md` | `48633eca3122fbdd8b7f616c79ecc8a228a784bba185a24b7929ea556592c6d0` |
| `A8` traceability | `KEYWORD_INTELLIGENCE_TRACEABILITY_INDEX.md` | `90c2f808426c4f1cf20ad885860e01b66763f3fc607e28c3b2dd9a2ef7391a5f` |

The assignment is exact: `current_window: KI-W7-DECOMPOSITION`, assignment
`ASG-KI-W7-WA-01`, agent `KI-W7-WINDOW-AGENT`, `current_status: READY`,
`accepted_through: KI-W6`, and write authority only over `S1`, `S2`, and `S3`.
Implementation, leaf dispatch, build, database/browser operation, AWS/provider/
paid action, `A1`-`A8` edit, commit, push, and every `KI-W8` action are
prohibited during this assignment.

### 0.1 Scope-relative mechanical interpretations

1. Initial leaf IDs are `KI-W7-S001` through `KI-W7-S013`; the first assessment
   is `KI-W7-I001`; corrective IDs start at `KI-W7-C001`; later assessments
   start at `KI-W7-I002`. IDs are never reused.
2. A4's three waves are retained as dependency strata: stratum 1 is S001-S006,
   stratum 2 is S007-S008, and stratum 3 is S009-S013. A5's
   `permitted_waves_after_parent_decomposition_approval: []` supplies no
   concurrent-dispatch authority. Therefore the executable schedule is the
   strict serial chain S001 -> ... -> S013 -> I001. A later parent authority
   change would require a revision delta audit; this decomposition itself does
   not activate parallel execution.
3. Private cross-file names not fixed as public product contracts are frozen
   here only to make the parent-decided behavior executable: recovery exports
   `recoverCombinedWork`; keyword deployment phases are `full` (disabled) and
   `activate`; the inspector uses the established mutually exclusive
   `--expected-disabled` and `--expected-active` flags; the measurement report
   is `dist/lambda/keyword-worker-measurements.json`. These are direct
   continuations of the current recovery and guarded-deployment conventions,
   not alternative behavior.
4. Every leaf runs from `email_scraper/`. Workspace-relative writable paths in
   leaf metadata retain the `email_scraper/` prefix. Commands use repository-
   relative paths because their working directory is fixed.
5. Before parent decomposition approval, S2 uses only values admitted by the
   Section 2.2 schema: `current_subwindow:STOP`,
   `current_assignment_id:WINDOW-AGENT`, `assigned_agent:WINDOW-AGENT`,
   `subwindow_type:INTEGRATION_ASSESSMENT`, `authorized_write_file:NONE`, and
   `current_status:COMPLETE`, with `blocker:null`. This is a completed
   decomposition-authoring sentinel at the normal parent-review boundary, not
   an assignment of I001 or authority to execute any check. The simultaneous
   `decomposition_status:AWAITING_PARENT_DECOMPOSITION_REVIEW`, `STOP`,
   `authorized_write_file:NONE`, empty accepted list, and prohibited leaf
   assignment make it fail closed without falsely classifying review as a
   blocker. On parent approval the window agent must replace the entire
   sentinel with the exact S001 assignment; it cannot begin from the sentinel.

### 0.2 Inherited execution-environment policy

Sandbox escalation is standing-authorized only for an already-authorized local
command. One identical escalated recovery is permitted after a restricted
attempt is proven invalidated solely by sandbox denial or execution-channel
loss and read-only postconditions prove no surviving process, workspace or
external mutation, paid operation, or usable result. Arguments, environment,
fixtures, timeout, selection, oracle, and write scope cannot change. Observable
test/product failure is not transport invalidation. This never authorizes AWS,
provider, paid, production, destructive, secret, commit, push, or successor
work.

## 1. Parent scope copied without expansion

- **Objective:** close production keyword repository/recovery/config seams and
  add one disabled-by-default keyword SQS/Lambda deployment slice with guarded
  local packaging; perform no AWS or paid action.
- **Delegable changed-file set:** exactly the 13 paths in Section 2, digest
  `04ce71235fe61103c071f859d6050d4f8fee2b56dc0e088b9d97f5111be57a9f`.
- **Authorized leaf actions:** one-file source or test edit; file-local static
  and focused checks; no other workspace write.
- **Window-agent-only final actions:** deterministic established/keyword/recovery
  builds and measurement, one frozen `npm test`, one frozen secret scan,
  complete static/template/coverage/diff assessment, and coordination-artifact
  updates after leaf execution is separately approved.
- **Read-only scope:** all other root/backend/frontend paths, accepted W6
  evidence, existing deployment source, and frozen authorities.
- **Prohibited:** AWS/API/CLI or provider/network/database call; credential or
  secret read; production/test database use; schema, migration, package, lock,
  frontend, or unlisted source/test edit; existing resource removal, rename,
  replacement, or disablement; direct `sam deploy`; destructive action;
  commit/push; `KI-W8`.
- **Successor:** `STOP_AWS_MUTATION_APPROVAL`, reserved for the parent.
  `may_start_successor:false`.

## 2. Starting working-tree inventory

Recorded read-only in `EV-KI-W7-S001`.

- Backend repository HEAD `a87e139c020712ef95c05d232b9548216b0658b8`; porcelain empty.
- Frontend repository HEAD `5e441aae7e2f3a132b2c7fc85bf1bc525d3d5cb6`; porcelain empty.
- Coordination root has seven parent-owned modified artifacts and no KI-W7
  subordinate artifact at baseline. The seven-path set digest is
  `6a8baa5680b1bc6f308c3778347ff3c9f24d17f9716c91abb361f1a1388d00cc`.
  Those files and their starting digests are the authority table in Section 0;
  they are protected from leaf edits.
- All six existing targets below are regular files, not symlinks. The parent
  directory of every new target is regular and workspace-contained; the new
  `scripts/keyword-intelligence/` directory does not exist at decomposition
  time and may be created only as the parent directory needed for S007's one
  file. S007 must prove no second file is created.

| File ID | Path | Operation | Start digest |
|---|---|---|---|
| `F-001` | `email_scraper/src/config.js` | MODIFY | `222daf3780cefa0f061cf486d978d84126fdee6d0a1adf358087b8db2bcc03f9` |
| `F-002` | `email_scraper/src/aws-pipeline/runtime-config.js` | MODIFY | `1801455db1e4c88c63e9d8215e4b1f3770990359518fe07877c3b0218f11576b` |
| `F-003` | `email_scraper/src/aws-pipeline/keyword-intelligence/handler.js` | MODIFY | `c6a38b0bb4adf19058b53b9e24b0ae3308f590a8d2eb387ca82d1bb0ab16c414` |
| `F-004` | `email_scraper/src/aws-pipeline/handlers/recovery.js` | MODIFY | `7a633679b7d0894c789bf01fb32bd056fdc50ac6a11d8080db52e8fefad81e78` |
| `F-005` | `email_scraper/infrastructure/aws/template.yaml` | MODIFY | `9e5366c95250d37caf0190611d14ca308b03ee20b9c4a0758c8e82b0233c058f` |
| `F-006` | `email_scraper/scripts/measure-keyword-worker-package.js` | CREATE | `ABSENT` |
| `F-007` | `email_scraper/scripts/keyword-intelligence/create-change-set.js` | CREATE | `ABSENT` |
| `F-008` | `email_scraper/scripts/keyword-intelligence/inspect-stack.js` | CREATE | `ABSENT` |
| `F-009` | `email_scraper/test/aws-pipeline-runtime-adapters.test.js` | MODIFY | `5131d1c7eb0df24516804c2801288b0dd323cd10b4e7933ffdefa52b40b573d6` |
| `F-010` | `email_scraper/test/keyword-intelligence-deployment-runtime.test.js` | CREATE | `ABSENT` |
| `F-011` | `email_scraper/test/keyword-intelligence-infrastructure.test.js` | CREATE | `ABSENT` |
| `F-012` | `email_scraper/test/keyword-intelligence-build.test.js` | CREATE | `ABSENT` |
| `F-013` | `email_scraper/test/keyword-intelligence-deployment-guard.test.js` | CREATE | `ABSENT` |

## 3. File graph, dependency order, and intermediate states

### 3.1 Mechanical file trace

| File | Parent requirements/invariants | Decisions/tasks | Produced interface | Coverage owner |
|---|---|---|---|---|
| F-001 | `REQ-KI-002/005`; `INV-KI-002/012` | `DEC-KI-027/059`; `KI-W7-T1` | IF-1 source config members | none; tested by F-009 |
| F-002 | same | same | IF-2 active/inactive runtime union | none; tested by F-009 |
| F-003 | `REQ-KI-002/005/022-024`; `INV-KI-004-007` | `DEC-KI-001/018/026/059`; `KI-W7-T2` | IF-3 production keyword runtime | none; tested by F-010 |
| F-004 | same | same | IF-4 combined recovery | none; tested by F-010 |
| F-005 | `REQ-KI-002/005/022-024`; `INV-KI-001/002/012`; `EXC-KI-008` | `DEC-KI-020/024/025/059`; `KI-W7-T3` | IF-5 disabled topology | none; tested by F-011/F-013 |
| F-006 | `INV-KI-012`; `REQ-KI-022-024` | `DEC-KI-024/059`; `KI-W7-T4` | IF-6 measurement report | none; tested by F-012 |
| F-007 | `AUTH-KI-005`; `EXC-KI-008`; `REQ-KI-022-024` | `DEC-KI-025/059`; `KI-W7-T5` | IF-7 packet/change-set guard | none; tested by F-013 |
| F-008 | same | same | IF-8 read-only stack inspection | none; tested by F-013 |
| F-009 | all T1 requirements | `KI-W7-T6`; `SCN-KI-047` | case registry runtime config | `W7-RUNTIME-01`; `W7-NC-01/02` |
| F-010 | all T2 requirements | `KI-W7-T6`; `SCN-KI-047` | case registry runtime composition | `W7-RUNTIME-02`; `W7-NC-03/04` |
| F-011 | all T3 requirements | `KI-W7-T6`; `SCN-KI-047` | infrastructure registry | `W7-INFRA-01-06`; `W7-NC-05-09` |
| F-012 | all T4 requirements | `KI-W7-T6`; `SCN-KI-047` | build registry | `W7-BUILD-01`; `W7-NC-10` |
| F-013 | all T5/T6 requirements | `KI-W7-T6`; `SCN-KI-047` | deployment/conformance registry plus accepted TAP parser/CLI | `W7-DEPLOY-01/02`; `W7-CONF-01`; `W7-NC-11/12`; CV4 execution certificate |

Every parent requirement, decision, task, scenario, case, and control allocated
to W7 terminates in this table and Sections 4-6. The planned set equals the 13
unique initial owners and recomputes to the parent digest. There are zero
unmapped or duplicate owners.

### 3.2 Exact serial DAG

```text
S001 -> S002 -> S003 -> S004 -> S005 -> S006
     -> S007 -> S008 -> S009 -> S010 -> S011 -> S012 -> S013 -> I001
```

The semantic strata remain:

- stratum 1: S001-S006 establishes IF-1 through IF-6;
- stratum 2: S007-S008 consumes accepted IF-5 and establishes IF-7/IF-8;
- stratum 3: S009-S013 consumes every production/script interface it tests.

Because execution is serial, each leaf's predecessor is the immediately prior
leaf and its expected starting backend changed-file-set digest is frozen in its
block. The semantic dependencies above remain mandatory even if a later parent
authorizes parallel scheduling.

### 3.3 Intermediate-state contract

After every production/script leaf S001-S008, its `node --check` or JSON parse,
file-local static assertions, and diff/write-set checks must pass. Focused or
whole tests that consume a not-yet-authored successor are `DEFERRED_TO_I001`,
not expected failures. No test command may be run merely to observe an expected
failure. These states are safe because no build, deployment, server, database,
AWS, provider, or externally visible action is allowed. S009-S013 successively
adds executable proof; required W7 case-set equality remains pending until S013.
Only I001 resolves all deferrals. During every intermediate state: no runtime
activation, packaging, AWS CLI, source consumer outside the assigned file,
successor edit, or A1-A8 edit is permitted. Any unexpected local failure stops
for diagnosis.

## 4. Frozen cross-file interfaces and exact transformations

### IF-1 / IF-2 configuration

- `loadConfig()` inserts exactly two members beside existing AWS settings:
  `awsPipelineKeywordResearchEnabled:
  strictBoolean("AWS_PIPELINE_KEYWORD_RESEARCH_ENABLED", false)` and
  `awsPipelineKeywordResearchQueueUrl:
  process.env.AWS_PIPELINE_KEYWORD_RESEARCH_QUEUE_URL || ""`.
- `loadAwsPipelineConfig(baseConfig)` preserves `QUEUE_KEYS` as the exact six
  established members and preserves all established local/AWS checks. Local
  mode returns both `awsPipelineActive:false` and
  `awsPipelineKeywordResearchActive:false`. Valid AWS mode first validates the
  established members. Keyword flag false then returns keyword inactive even
  with empty URL. Keyword flag true requires `validHttpsUrl` for the exact
  keyword URL; invalid active config throws
  `Object.assign(new Error("KEYWORD_RUNTIME_CONFIG_INVALID"),
  {code:"KEYWORD_RUNTIME_CONFIG_INVALID"})`; valid returns keyword active.
  Returned objects stay frozen. No alias or direct environment read is added.

### IF-3 keyword handler

- Add import `PrismaKeywordResearchRepository` from
  `../../keyword-intelligence/repository.js`.
- `handler(event = {}, runtime)` keeps injected `runtime.repository`
  authoritative. When `runtime` is absent, await `createPipelineRuntime()` and
  replace only `repository` with exactly
  `new PrismaKeywordResearchRepository(base.prisma)` using that same Prisma
  instance.
- Before `handleSqsBatch`, require active keyword config and an HTTPS queue URL;
  inactive/invalid activation throws the exact coded error from IF-2. Require
  repository, dispatcher, S3 client, base artifact store, Prisma for the
  uninjected branch, and bucket; missing non-config prerequisites retain
  `PIPELINE_INPUT_CONFLICT`.
- Construct exactly one `S3ArtifactStore` from `base.s3Client`, the shared
  bucket, and `KEYWORD_ARTIFACT_MAX_BYTES=33554432`; retain clock/http/secrets
  defaults and existing parse/process/partial-batch behavior. No environment,
  queue, provider, or repository algorithm is changed.

### IF-4 combined recovery

- Import `PipelineInvariantError`, `PrismaKeywordResearchRepository`, and
  `recoverKeywordWork`; export
  `recoverCombinedWork({now, limit = 100}, base)`.
- It awaits `recoverPipelineWork({now,limit},base)` first. When keyword active
  is not exactly true it returns
  `{pipeline,keyword:{outcome:"disabled"}}` and performs zero keyword
  construction/read/send. When active, require `base.prisma`, construct exactly
  one keyword repository from it, await
  `recoverKeywordWork({now,limit},{...base,repository:keywordRepository})`, and
  return `{pipeline,keyword}`. First failure propagates unchanged.
- `handler(event={})` creates the shared runtime once, retains current base
  prerequisite rejection, captures exactly one `new Date()`, uses
  `event.limit ?? 100`, and calls the exported composition. Existing recovery
  validation enforces valid Date and integer `1..100`. No second handler or
  schedule is introduced.

### IF-5 exact template delta

The JSON document remains valid SAM and every pre-existing member deep-equals
the baseline except these named extensions.

1. Add parameters:
   - `KeywordWorkerCodeKey`: `Type:"String"`,
     `AllowedPattern:"^deployment/[a-f0-9]{64}/keyword-worker\\.zip$"`;
   - `KeywordWorkerCodeVersion`: `Type:"String"`, `MinLength:1`,
     `MaxLength:1024`;
   - `KeywordResearchEnabled`: `Type:"String"`,
     `AllowedValues:["false","true"]`, `Default:"false"`.
2. Add `KeywordResearchEnabledCondition` as
   `{"Fn::Equals":[{"Ref":"KeywordResearchEnabled"},"true"]}`.
3. Add exactly ten resources:
   - `KeywordResearchDlq`: encrypted, 14-day retention, stack name suffix
     `keyword-research-dlq`, established project/environment/dead-letter tags;
   - `KeywordResearchQueue`: encrypted, stack suffix `keyword-research`,
     retention `345600`, visibility `1080`, maximum bytes `262144`, long poll
     `20`, redrive count `5` to the DLQ, established source tags;
   - `KeywordWorkerLogGroup`: retained on delete/replace, name
     `/aws/lambda/${AWS::StackName}-keyword-worker`, retention `30`;
   - `KeywordWorkerRole`: established Lambda trust/tags and one
     `PipelineAccess` policy. Exact statements are `WriteOwnLogs`
     (`logs:CreateLogStream`, `logs:PutLogEvents` to only the keyword log),
     `ReadPipelineSecret` (existing secret), `ConsumeAssignedQueues`
     (`ReceiveMessage/DeleteMessage/ChangeMessageVisibility/GetQueueAttributes`
     only keyword queue), `SendAssignedQueues` (`SendMessage` only keyword
     queue), `ListAssignedArtifactKeys` (`ListBucket` only existing bucket with
     `s3:prefix:["runs/keyword-research/*"]`), `ReadAssignedArtifacts`
     (`GetObject` only `.../runs/keyword-research/*`), and
     `WriteAssignedArtifacts` (`PutObject` only that prefix);
   - `KeywordWorker`: depends on log group; name/description suffix
     `keyword-worker`; code uses the two new parameters; handler `index.handler`,
     runtime `nodejs24.x`, architecture `x86_64`, memory `1024`, reserved `1`,
     timeout `180`, ephemeral `512`, keyword role, tracing `Disabled`, established
     tags. Environment preserves the current Recovery variable object and adds
     `AWS_PIPELINE_KEYWORD_RESEARCH_QUEUE_URL:{Ref:"KeywordResearchQueue"}` and
     `AWS_PIPELINE_KEYWORD_RESEARCH_ENABLED:{"Fn::If":["KeywordResearchEnabledCondition","true","false"]}`;
   - `KeywordResearchMapping`: event source keyword queue ARN, function keyword
     worker, batch `1`, window `0`, `ReportBatchItemFailures`, `Enabled` as
     `{"Fn::If":["KeywordResearchEnabledCondition",true,false]}`, with no
     `ScalingConfig` or provisioned poller member;
   - four no-action, `TreatMissingData:"notBreaching"` alarms named
     `KeywordResearchDlqDepthAlarm`, `KeywordResearchOldestMessageAlarm`,
     `KeywordWorkerErrorsAlarm`, `KeywordWorkerThrottlesAlarm`, structurally
     equal to the established corresponding queue/Lambda alarms with only
     keyword names/references substituted.
4. Extend only `RecoveryRole`'s `SendAssignedQueues.Resource` array and
   `ControlPlanePolicy`'s `StartDiscoveryOnly.Resource` array with
   `{"Fn::GetAtt":["KeywordResearchQueue","Arn"]}`. Extend only Recovery's
   environment with the two keyword members specified for KeywordWorker.
5. Add outputs `KeywordResearchQueueUrl:{Value:{Ref:"KeywordResearchQueue"}}`,
   `KeywordResearchQueueArn:{Value:{"Fn::GetAtt":["KeywordResearchQueue","Arn"]}}`,
   `KeywordResearchDlqArn:{Value:{"Fn::GetAtt":["KeywordResearchDlq","Arn"]}}`,
   and `KeywordWorkerFunctionArn:{Value:{"Fn::GetAtt":["KeywordWorker","Arn"]}}`.

No current resource, parameter, output, policy statement, schedule, mapping, or
environment member may be renamed, removed, disabled, reordered semantically,
or broadened beyond those extensions.

### IF-6 measurement

The new module imports `KEYWORD_LAMBDA_HANDLERS` and
`REQUIRED_PRISMA_ENGINE` from `build-keyword-worker.js`; the handler list must
equal `["keyword-worker"]`. It exports testable `validateInventory` and
`measureKeywordWorkerPackage`, and invokes the latter only when run as main.
It deterministically reads `dist/lambda/keyword-worker.zip`, sorts unsigned-UTF8
ZIP and extracted inventories, rejects absolute/`..`/symlink/unsupported or
forbidden `.env`, tests, fixtures, docs, maps, markdown, or credential-named
members, requires exactly one engine ending in the required engine literal,
checks ZIP <= `45*1024*1024` and expanded <= `200*1024*1024`, extracts only to
`mkdtemp(tmpdir())`, cold-imports `index.mjs`, and removes only that temporary
directory. It writes only `dist/lambda/keyword-worker-measurements.json`, after
all validation succeeds, and prints the same report. Report shape is
`{node,measurements:[{handler,zipBytes,unzippedBytes,fileListHash,
requiredEngine,enginePresent,coldImport:{durationMs,rssBytes,rssDeltaBytes},
files}]}`. Stable projections excluding the three measured cold-import values
must match across identical builds. It never removes or rewrites a ZIP.

### IF-7 guarded packet/change-set script

The new module is dedicated to the existing production stack and exports
`DEPLOYMENT`, `parseArguments`, `buildDeploymentPacket`,
`assertReviewedChanges`, and `main`. It reuses the established guarded script's
argument grammar and fixed identity: `storesignal-dev`, `ap-south-2`,
`storesignal-production-pipeline`, `production`, twelve-digit STS account,
phases only `full` and `activate`, plus `--execute` and
`--apply-reviewed-change-set`. Dry run is default and spawns no `aws` process.

The packet has contract `storesignal-keyword-deployment-v1`, canonical token,
exact template object and exactly two ZIP objects: `keyword-worker.zip` and a
fresh `recovery.zip`, each with byte count, SHA-256, and key
`deployment/<sha256>/<basename>`; template key is
`deployment/<sha256>/cloudformation-template.json`. Source bytes are reread and
hash-checked immediately before any upload or create.

Mutation branches require `--execute`, exact `aws_mutation_approval` in A5 equal
to the packet token, exact matching active W8 phase/action authority, SSE AES256
versioned object confirmation, and a separately recorded reviewed change-set
ID for application. `full` may add only the ten IF-5 resources and directly
modify only `ControlPlanePolicy`, `RecoveryRole`, `Recovery`, all replacement
`False`, plus zero-or-one exact dependent reevaluations
`RecoveryInvokePermission` (`Conditional`, caused by
`RecoverySchedule.Arn`/`SourceArn`) and `RecoverySchedule` (`False`, caused by
`Recovery.Arn`). `activate` may directly modify only
`KeywordResearchMapping`, `KeywordWorker`, `Recovery`, replacement `False`,
with static direct targets respectively `Enabled` and the two keyword
environment members, plus those same optional dependencies. Remove,
replacement `True`, wildcard/broad/unlisted/direct mutation, stale token/hash/
ID, or incomplete stack fails before execute. There is no `sam deploy`, queue
receive/purge/redrive, direct resource mutation, secret value operation, or
implicit execution.

Generated packet/change-set records exist only under the gitignored
`dist/aws-deployment/keyword-intelligence/` root with mode `0600`; they are W8
outputs, not leaf source writes or W7 external actions.

### IF-8 inspector and coverage registries

The inspector imports IF-7, keeps the exact fixed identity and mutually
exclusive expected-state flags, and exports `parseInspectArguments`, `inspect`,
and `main`. It performs read-only AWS commands only when explicitly invoked.
Using injected/spawn-stubbed responses, it verifies STS identity, complete
stack, exact resource inventory, all keyword queue/DLQ/function/mapping/log/
alarm/IAM/output/environment literals, no broad data-plane access, and all
pre-existing topology deep equality. Disabled requires mapping disabled and
both keyword environment projections false; active requires enabled/true. It
never reads a secret value, receives/purges/redrives a queue, or mutates AWS.

Every test owner contains exactly one single-line source registry and no
export. The line is the literal prefix
`const W7_OWNER_REGISTRY = Object.freeze(`, immediately followed by the
owner-specific canonical JSON frozen in S009-S013, then the literal suffix
`); // W7-REGISTRY`.
The JSON has exactly the ordered keys `owner`, `requiredCases`, and
`requiredControls`; arrays contain the exact owner members from Section 3.1 and
no duplicate. Owners are respectively `runtime_config`,
`runtime_composition`, `infrastructure`, `build`, and `deployment_guard` for
F-009 through F-013. Each owner test uses its own constant when recording
executed IDs.

S013 defines `readOwnerRegistry(filePath)`, reads each of the five literal
source files with `readFileSync(filePath,"utf8")`, requires exactly one line
matching
`/^const W7_OWNER_REGISTRY = Object\.freeze\((\{.*\})\); \/\/ W7-REGISTRY$/m`,
parses only the captured JSON, rejects extra/missing keys, wrong owner, duplicate
member, or a second marker, and merges the exact arrays. It never imports or
executes another owner module, so registry discovery cannot register or run a
test twice. Every control uses captured/synthetic data and performs positive ->
exactly one mutation -> failure -> fresh positive without writing production
source.

## 5. Shared leaf execution protocol

Every leaf block below inherits these exact requirements:

- Preflight recomputes all frozen revisions, writable-file digest, expected
  backend changed-file set/digest, root protected-file digests, regular/nonlink
  path safety, and predecessor `ACCEPTED_FOR_INTEGRATION` evidence. Mismatch
  stops before edit.
- Only `apply_patch` may manually edit/create the writable file. No formatter,
  installer, generator, build, snapshot update, or command with another
  workspace output is allowed.
- `git diff --check -- <file>` and the listed local checks must exit zero.
- Handoff records exact diff, ending digest, before/after backend changed-file
  sets, commands/output/assertions, cases, controls, activation witnesses,
  skips/duplicates/unexpected members, limitations, and confirmation of zero
  external mutation/cost.
- Attributable changed-file equality is exactly `{writable_file}`. The agent
  reports only to `KI-W7-WINDOW-AGENT`, starts no successor, edits no S1/S2/S3
  or A1-A8 artifact, and stops `AWAITING_WINDOW_REVIEW`.

Each leaf must complete:

- [ ] P1 Revisions, assignment, writable file, digest, predecessor, and expected changed-set digest match.
- [ ] P2 Starting status and protected root/backend/frontend state match.
- [ ] T1 Apply every ordered transformation and no other writable-file edit.
- [ ] V1 Run every `LOCAL_NOW` check with activation witnesses/assertions.
- [ ] V2 Prove attributable workspace changed-file set is exactly the writable file.
- [ ] V3 Prove required local coverage equals registered/executed local coverage, or record the exact I001 deferral.
- [ ] H1 Return diff, digest, commands, outcomes, cases, and residual I001 obligations.
- [ ] H2 Confirm zero prohibited action, second-file edit, successor work, external mutation, or parent communication.
- [ ] H3 Stop at `AWAITING_WINDOW_REVIEW`.

## 6. Initial single-file sub-windows

### `KI-W7-S001` - application config seam

```yaml
subwindow_id: KI-W7-S001
type: FILE
parent_window_id: KI-W7
parent_assignment_id: ASG-KI-W7-WA-01
assigned_agent: UNASSIGNED
predecessors: []
successor_reserved_for: WINDOW-AGENT
writable_file: email_scraper/src/config.js
file_operation: MODIFY
starting_file_digest: 222daf3780cefa0f061cf486d978d84126fdee6d0a1adf358087b8db2bcc03f9
starting_repository_change_set_digest: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
read_only_scope: [A1-A8 W7/DEC-KI-059/SRC-KI-060, email_scraper/src/aws-pipeline/runtime-config.js, email_scraper/test/aws-pipeline-runtime-adapters.test.js]
authorized_actions: [edit exactly the two IF-1 object members, run syntax/static config checks]
prohibited_actions: [any other member/helper/validation change, dotenv write, second-file edit, test/build/network/database/AWS action]
may_start_successor: false
```

Mechanical trace: `DEC-KI-027/059`, `KI-W7-T1`, IF-1. At the anchor
`runExecutionBackend/awsPipelineEnabled`, insert the two IF-1 members in that
order; change nothing else. Preserve `strictBoolean`, every default and every
post-object validation byte-equivalently. Result exposes exactly the two names
to IF-2.

Checks (`LOCAL_NOW`): `node --check src/config.js`; a no-dotenv ESM assertion
loads config once with both env vars absent and once with exact `true`/HTTPS,
asserting false/empty then true/exact URL; invalid strict boolean must reject;
`git diff --check -- src/config.js`. Expected runtime/write output: no workspace
write. W7 cases are deferred to S009/I001.

- [ ] P1 revisions, assignment, file, digest, and predecessor match.
- [ ] P2 starting and protected state match.
- [ ] T1 exact transformation and no other edit.
- [ ] V1 all local checks and activation witnesses pass.
- [ ] V2 attributable changed-file set equals the writable file.
- [ ] V3 local coverage equality or exact I001 deferral is recorded.
- [ ] H1 exact diff, digest, commands, outcomes, and obligations return.
- [ ] H2 zero prohibited action, second file, successor, external action, or parent contact.
- [ ] H3 stop at `AWAITING_WINDOW_REVIEW`.

### `KI-W7-S002` - runtime activation projection

```yaml
subwindow_id: KI-W7-S002
type: FILE
parent_window_id: KI-W7
parent_assignment_id: ASG-KI-W7-WA-01
assigned_agent: UNASSIGNED
predecessors: [KI-W7-S001]
successor_reserved_for: WINDOW-AGENT
writable_file: email_scraper/src/aws-pipeline/runtime-config.js
file_operation: MODIFY
starting_file_digest: 1801455db1e4c88c63e9d8215e4b1f3770990359518fe07877c3b0218f11576b
starting_repository_change_set_digest: b78c2a5d4444d756b8686f6e0c6af7e7a1c05c74580925bfa826574acca39a48
read_only_scope: [A1-A8 W7/DEC-KI-059, accepted S001, email_scraper/src/config.js, email_scraper/test/aws-pipeline-runtime-adapters.test.js]
authorized_actions: [implement IF-2 only, run syntax and pure config partition checks]
prohibited_actions: [change QUEUE_KEYS six-member set, change established activation/failure text, environment read, second-file edit]
may_start_successor: false
```

Apply IF-2 after the established mode and six-queue checks. Add one private
coded-error constructor only if it returns the literal IF-2 Error shape. No
alternate URL validator/error is allowed. `LOCAL_NOW`: syntax; pure ESM
assertions for local inactive, AWS keyword false+empty, AWS keyword true+HTTPS,
and coded empty/http rejection while the six established fields remain deep
equal; diff check. Cases/controls register only in S009.

- [ ] P1 revisions, assignment, file, digest, and predecessor match.
- [ ] P2 starting and protected state match.
- [ ] T1 exact transformation and no other edit.
- [ ] V1 all local checks and activation witnesses pass.
- [ ] V2 attributable changed-file set equals the writable file.
- [ ] V3 local coverage equality or exact I001 deferral is recorded.
- [ ] H1 exact diff, digest, commands, outcomes, and obligations return.
- [ ] H2 zero prohibited action, second file, successor, external action, or parent contact.
- [ ] H3 stop at `AWAITING_WINDOW_REVIEW`.

### `KI-W7-S003` - production keyword handler

```yaml
subwindow_id: KI-W7-S003
type: FILE
parent_window_id: KI-W7
parent_assignment_id: ASG-KI-W7-WA-01
assigned_agent: UNASSIGNED
predecessors: [KI-W7-S002]
successor_reserved_for: WINDOW-AGENT
writable_file: email_scraper/src/aws-pipeline/keyword-intelligence/handler.js
file_operation: MODIFY
starting_file_digest: c6a38b0bb4adf19058b53b9e24b0ae3308f590a8d2eb387ca82d1bb0ab16c414
starting_repository_change_set_digest: 4b540958b428c261ba41aff3522184cc23b682c05b6fbf810f86cdc500be3a63
read_only_scope: [A1-A8 W7/DEC-KI-059, accepted S001-S002, email_scraper/src/aws-pipeline/runtime.js, email_scraper/src/keyword-intelligence/repository.js, email_scraper/src/aws-pipeline/keyword-intelligence/contracts.js, email_scraper/test/keyword-intelligence-worker.test.js]
authorized_actions: [apply IF-3 imports and handler branch, run syntax/static interface checks]
prohibited_actions: [repository/service/contract/adapter change, direct env read, queue/provider call, second-file edit]
may_start_successor: false
```

Apply IF-3 in import order and within `handler`; preserve the exported constant,
parser, service call, and batch response. `LOCAL_NOW`: syntax; deterministic
source/AST-style assertions prove one repository import/construction, production
branch only, 33554432, and no `process.env`; diff check. The uninjected runtime
effect is deferred to S010/I001.

- [ ] P1 revisions, assignment, file, digest, and predecessor match.
- [ ] P2 starting and protected state match.
- [ ] T1 exact transformation and no other edit.
- [ ] V1 all local checks and activation witnesses pass.
- [ ] V2 attributable changed-file set equals the writable file.
- [ ] V3 local coverage equality or exact I001 deferral is recorded.
- [ ] H1 exact diff, digest, commands, outcomes, and obligations return.
- [ ] H2 zero prohibited action, second file, successor, external action, or parent contact.
- [ ] H3 stop at `AWAITING_WINDOW_REVIEW`.

### `KI-W7-S004` - combined recovery handler

```yaml
subwindow_id: KI-W7-S004
type: FILE
parent_window_id: KI-W7
parent_assignment_id: ASG-KI-W7-WA-01
assigned_agent: UNASSIGNED
predecessors: [KI-W7-S003]
successor_reserved_for: WINDOW-AGENT
writable_file: email_scraper/src/aws-pipeline/handlers/recovery.js
file_operation: MODIFY
starting_file_digest: 7a633679b7d0894c789bf01fb32bd056fdc50ac6a11d8080db52e8fefad81e78
starting_repository_change_set_digest: 979b0c975a5aa46b9f804619c9aa5ec629c0074afc4c3ab620ddb805ecfc5200
read_only_scope: [A1-A8 W7/DEC-KI-059, accepted S001-S003, email_scraper/src/aws-pipeline/runtime.js, email_scraper/src/aws-pipeline/services/recovery.js, email_scraper/src/aws-pipeline/keyword-intelligence/recovery.js, email_scraper/src/keyword-intelligence/repository.js]
authorized_actions: [apply IF-4 only, run syntax/static ordering checks]
prohibited_actions: [second handler/schedule, recovery algorithm or limit change, error relabel, second-file edit]
may_start_successor: false
```

Apply IF-4 exactly. The prerequisite rejection remains before composition;
`recoverCombinedWork` has no clock/environment read. `LOCAL_NOW`: syntax;
source assertion proves one call of each recovery function in pipeline-before-
keyword lexical/await order, inactive early return, one repository constructor,
one handler `new Date()`, and export names; diff check. Runtime effect defers to
S010/I001.

- [ ] P1 revisions, assignment, file, digest, and predecessor match.
- [ ] P2 starting and protected state match.
- [ ] T1 exact transformation and no other edit.
- [ ] V1 all local checks and activation witnesses pass.
- [ ] V2 attributable changed-file set equals the writable file.
- [ ] V3 local coverage equality or exact I001 deferral is recorded.
- [ ] H1 exact diff, digest, commands, outcomes, and obligations return.
- [ ] H2 zero prohibited action, second file, successor, external action, or parent contact.
- [ ] H3 stop at `AWAITING_WINDOW_REVIEW`.

### `KI-W7-S005` - disabled SAM topology

```yaml
subwindow_id: KI-W7-S005
type: FILE
parent_window_id: KI-W7
parent_assignment_id: ASG-KI-W7-WA-01
assigned_agent: UNASSIGNED
predecessors: [KI-W7-S004]
successor_reserved_for: WINDOW-AGENT
writable_file: email_scraper/infrastructure/aws/template.yaml
file_operation: MODIFY
starting_file_digest: 9e5366c95250d37caf0190611d14ca308b03ee20b9c4a0758c8e82b0233c058f
starting_repository_change_set_digest: 22b2424e64186fa124fa15a88f0a488b5e877a0b024d81c5837cddd302140baf
read_only_scope: [A1-A8 W7/DEC-KI-059/SRC-KI-060, accepted S001-S004, baseline template object, AWS architecture documents]
authorized_actions: [apply only IF-5 JSON members, parse and inspect exact delta]
prohibited_actions: [rename/remove/disable/replace existing member, second schedule, ScalingConfig, wildcard data-plane IAM, YAML generator, AWS/sam call, second-file edit]
may_start_successor: false
```

Use the existing JSON indentation/final LF. Apply IF-5 in parameter, condition,
resource, extension, output order. `LOCAL_NOW`: `node -e` JSON parse; a
deterministic inspection asserts exact three/one/ten/four added member sets,
all literal bounds, 1080=`6*180`, absent scaling, one recovery rule, narrow IAM,
and baseline deep equality after deleting only named additions/extensions; diff
check. Full cases/controls defer to S011/I001.

- [ ] P1 revisions, assignment, file, digest, and predecessor match.
- [ ] P2 starting and protected state match.
- [ ] T1 exact transformation and no other edit.
- [ ] V1 all local checks and activation witnesses pass.
- [ ] V2 attributable changed-file set equals the writable file.
- [ ] V3 local coverage equality or exact I001 deferral is recorded.
- [ ] H1 exact diff, digest, commands, outcomes, and obligations return.
- [ ] H2 zero prohibited action, second file, successor, external action, or parent contact.
- [ ] H3 stop at `AWAITING_WINDOW_REVIEW`.

### `KI-W7-S006` - keyword package measurement

```yaml
subwindow_id: KI-W7-S006
type: FILE
parent_window_id: KI-W7
parent_assignment_id: ASG-KI-W7-WA-01
assigned_agent: UNASSIGNED
predecessors: [KI-W7-S005]
successor_reserved_for: WINDOW-AGENT
writable_file: email_scraper/scripts/measure-keyword-worker-package.js
file_operation: CREATE
starting_file_digest: ABSENT
starting_repository_change_set_digest: 624be66e8e092aeba55d1a4dc4b9340c7d6d9119bdb2e500ecfa48965c0ca990
read_only_scope: [A1-A8 W7/DEC-KI-059, email_scraper/scripts/build-keyword-worker.js, email_scraper/scripts/measure-lambda-packages.js, accepted S005]
authorized_actions: [create exactly IF-6 module, run syntax/static no-main checks]
prohibited_actions: [run builder/measurement, alter or delete ZIP/report, create second workspace file, edit accepted builders]
may_start_successor: false
```

Implement IF-6 with unsigned-UTF8 `Buffer.compare`, not locale sorting. Main
guard must prevent work on import. `LOCAL_NOW`: syntax; import module and assert
two exports without invoking measurement; source inspection asserts exact
limits/report path/handler list/cleanup target and no sibling removal; diff
check. Build execution and `W7-BUILD-01/NC-10` defer to S012/I001.

- [ ] P1 revisions, assignment, file, digest, and predecessor match.
- [ ] P2 starting and protected state match.
- [ ] T1 exact transformation and no other edit.
- [ ] V1 all local checks and activation witnesses pass.
- [ ] V2 attributable changed-file set equals the writable file.
- [ ] V3 local coverage equality or exact I001 deferral is recorded.
- [ ] H1 exact diff, digest, commands, outcomes, and obligations return.
- [ ] H2 zero prohibited action, second file, successor, external action, or parent contact.
- [ ] H3 stop at `AWAITING_WINDOW_REVIEW`.

### `KI-W7-S007` - guarded keyword change-set packet

```yaml
subwindow_id: KI-W7-S007
type: FILE
parent_window_id: KI-W7
parent_assignment_id: ASG-KI-W7-WA-01
assigned_agent: UNASSIGNED
predecessors: [KI-W7-S006]
successor_reserved_for: WINDOW-AGENT
writable_file: email_scraper/scripts/keyword-intelligence/create-change-set.js
file_operation: CREATE
starting_file_digest: ABSENT
starting_repository_change_set_digest: ea25959403b3b8e94f7e39727d156e3f17d45d1e763a72a07d62b5251369c8a3
read_only_scope: [A1-A8 W7/DEC-KI-059, accepted S005-S006, email_scraper/scripts/aws-pipeline/create-change-set.js, email_scraper/infrastructure/aws/template.yaml, email_scraper/scripts/build-keyword-worker.js]
authorized_actions: [create parent directory if absent and exactly IF-7 file, run syntax/dry-run-static checks with no AWS]
prohibited_actions: [real AWS process, write generated packet, direct deploy, secret read, second source file, change established script]
may_start_successor: false
```

Create only the named file; directory creation is permitted but contains no
other new member. Implement IF-7. `LOCAL_NOW`: syntax; import and assert fixed
identity/phases/exports; parse-argument negative partitions; source inspection
proves default branch contains no spawned AWS call and all change allowlists;
diff check. Do not invoke `main` or build packet because ZIPs are integration
inputs. Deployment cases defer to S013/I001.

- [ ] P1 revisions, assignment, file, digest, and predecessor match.
- [ ] P2 starting and protected state match.
- [ ] T1 exact transformation and no other edit.
- [ ] V1 all local checks and activation witnesses pass.
- [ ] V2 attributable changed-file set equals the writable file.
- [ ] V3 local coverage equality or exact I001 deferral is recorded.
- [ ] H1 exact diff, digest, commands, outcomes, and obligations return.
- [ ] H2 zero prohibited action, second file, successor, external action, or parent contact.
- [ ] H3 stop at `AWAITING_WINDOW_REVIEW`.

### `KI-W7-S008` - read-only deployed-state inspector

```yaml
subwindow_id: KI-W7-S008
type: FILE
parent_window_id: KI-W7
parent_assignment_id: ASG-KI-W7-WA-01
assigned_agent: UNASSIGNED
predecessors: [KI-W7-S007]
successor_reserved_for: WINDOW-AGENT
writable_file: email_scraper/scripts/keyword-intelligence/inspect-stack.js
file_operation: CREATE
starting_file_digest: ABSENT
starting_repository_change_set_digest: 99917cf214eb955255440e57c6c2acd684f9c8b73857df18b3c5f099171927c7
read_only_scope: [A1-A8 W7/DEC-KI-059, accepted S005/S007, email_scraper/scripts/aws-pipeline/inspect-stack.js, email_scraper/infrastructure/aws/template.yaml]
authorized_actions: [create exactly IF-8 inspector, run syntax/argument/static read-only checks]
prohibited_actions: [invoke real AWS, secret-value/queue receive/purge/redrive, mutation command, second-file edit]
may_start_successor: false
```

Implement IF-8. The AWS command allowlist is limited to read-only STS,
CloudFormation describe/list, SQS attributes/get-url, Lambda configuration/
concurrency/mappings, Logs describe, IAM list/get policy, and CloudWatch
describe; `secretsmanager get-secret-value` is prohibited. `LOCAL_NOW`: syntax;
import/argument partitions; source command-token denylist; diff check. Stubbed
applied-state effects defer to S013/I001.

- [ ] P1 revisions, assignment, file, digest, and predecessor match.
- [ ] P2 starting and protected state match.
- [ ] T1 exact transformation and no other edit.
- [ ] V1 all local checks and activation witnesses pass.
- [ ] V2 attributable changed-file set equals the writable file.
- [ ] V3 local coverage equality or exact I001 deferral is recorded.
- [ ] H1 exact diff, digest, commands, outcomes, and obligations return.
- [ ] H2 zero prohibited action, second file, successor, external action, or parent contact.
- [ ] H3 stop at `AWAITING_WINDOW_REVIEW`.

### `KI-W7-S009` - runtime-config enforcement owner

```yaml
subwindow_id: KI-W7-S009
type: FILE
parent_window_id: KI-W7
parent_assignment_id: ASG-KI-W7-WA-01
assigned_agent: UNASSIGNED
predecessors: [KI-W7-S008]
successor_reserved_for: WINDOW-AGENT
writable_file: email_scraper/test/aws-pipeline-runtime-adapters.test.js
file_operation: MODIFY
starting_file_digest: 5131d1c7eb0df24516804c2801288b0dd323cd10b4e7933ffdefa52b40b573d6
starting_repository_change_set_digest: 916b03deca6b2189562fcc4e054c36ccd9156b5319e301a40b419358295af4da
read_only_scope: [A1-A8 W7 case matrix, accepted S001-S008, email_scraper/src/config.js, email_scraper/src/aws-pipeline/runtime-config.js]
authorized_actions: [extend only existing AWS config describe/test area with literal registry and W7 runtime partitions]
prohibited_actions: [weaken/delete existing test, edit unrelated adapter tests, production mutation, source-capture rewrite]
may_start_successor: false
```

Add exactly
`const W7_OWNER_REGISTRY = Object.freeze({"owner":"runtime_config","requiredCases":["W7-RUNTIME-01"],"requiredControls":["W7-NC-01","W7-NC-02"]}); // W7-REGISTRY`;
add named tests that exercise
IF-1/IF-2 inactive/active partitions, preserve the six established queue values,
assert exact coded error, and run each captured mutation positive->failure->
fresh-positive. Preserve all existing assertions. `LOCAL_NOW`: syntax; focused
`node --test --test-isolation=none --test-name-pattern='W7-RUNTIME-01|W7-NC-01|W7-NC-02' test/aws-pipeline-runtime-adapters.test.js` with exactly
the three W7 IDs activated and zero fail/skip; complete file test may be
deferred to I001; diff check.

- [ ] P1 revisions, assignment, file, digest, and predecessor match.
- [ ] P2 starting and protected state match.
- [ ] T1 exact transformation and no other edit.
- [ ] V1 all local checks and activation witnesses pass.
- [ ] V2 attributable changed-file set equals the writable file.
- [ ] V3 local coverage equality or exact I001 deferral is recorded.
- [ ] H1 exact diff, digest, commands, outcomes, and obligations return.
- [ ] H2 zero prohibited action, second file, successor, external action, or parent contact.
- [ ] H3 stop at `AWAITING_WINDOW_REVIEW`.

### `KI-W7-S010` - handler/recovery runtime enforcement

```yaml
subwindow_id: KI-W7-S010
type: FILE
parent_window_id: KI-W7
parent_assignment_id: ASG-KI-W7-WA-01
assigned_agent: UNASSIGNED
predecessors: [KI-W7-S009]
successor_reserved_for: WINDOW-AGENT
writable_file: email_scraper/test/keyword-intelligence-deployment-runtime.test.js
file_operation: CREATE
starting_file_digest: ABSENT
starting_repository_change_set_digest: f4489712034c0896bb8bbcb40661192f231d618677dac3e9b7521e60c2d7ddb2
read_only_scope: [A1-A8 W7 case matrix, accepted S001-S009, email_scraper/src/aws-pipeline/runtime.js, email_scraper/src/aws-pipeline/keyword-intelligence/handler.js, email_scraper/src/aws-pipeline/handlers/recovery.js, email_scraper/src/aws-pipeline/keyword-intelligence/recovery.js, email_scraper/src/keyword-intelligence/repository.js]
authorized_actions: [create isolated Node tests for IF-3/IF-4 with node:test module mocks and in-memory fakes]
prohibited_actions: [database/network/AWS/provider call, production source capture as sole positive proof, second-file edit]
may_start_successor: false
```

Add exactly
`const W7_OWNER_REGISTRY = Object.freeze({"owner":"runtime_composition","requiredCases":["W7-RUNTIME-02"],"requiredControls":["W7-NC-03","W7-NC-04"]}); // W7-REGISTRY`.
Use Node 24
`mock.module` before a cache-busted dynamic handler import so the uninjected
call reaches the real handler branch while `createPipelineRuntime` returns a
fully injected in-memory base; assert the repository is an actual
`PrismaKeywordResearchRepository` whose `.client` is the exact Prisma marker,
the keyword S3 store has 33554432, and the injected-handler path retains its
repository. Exercise exported combined recovery with event ordering log:
pipeline first, inactive zero keyword read/send, active one keyword repository
and one keyword call with same Date/limit, and unchanged first failure.
NC-03/04 use captured branch mutations, not production writes. `LOCAL_NOW`:
syntax and full focused file test, exact 1 case/2 controls, zero fail/skip;
diff check.

- [ ] P1 revisions, assignment, file, digest, and predecessor match.
- [ ] P2 starting and protected state match.
- [ ] T1 exact transformation and no other edit.
- [ ] V1 all local checks and activation witnesses pass.
- [ ] V2 attributable changed-file set equals the writable file.
- [ ] V3 local coverage equality or exact I001 deferral is recorded.
- [ ] H1 exact diff, digest, commands, outcomes, and obligations return.
- [ ] H2 zero prohibited action, second file, successor, external action, or parent contact.
- [ ] H3 stop at `AWAITING_WINDOW_REVIEW`.

### `KI-W7-S011` - infrastructure enforcement

```yaml
subwindow_id: KI-W7-S011
type: FILE
parent_window_id: KI-W7
parent_assignment_id: ASG-KI-W7-WA-01
assigned_agent: UNASSIGNED
predecessors: [KI-W7-S010]
successor_reserved_for: WINDOW-AGENT
writable_file: email_scraper/test/keyword-intelligence-infrastructure.test.js
file_operation: CREATE
starting_file_digest: ABSENT
starting_repository_change_set_digest: 3035c0cff2e0cd55609c1d0cf8a61758d3e58d40ad82f778b2cf2648c86789e9
read_only_scope: [A1-A8 W7 case matrix, accepted S005/S010, email_scraper/infrastructure/aws/template.yaml, baseline template digest/object recorded in S3]
authorized_actions: [create exact JSON topology/property/IAM/deep-equality tests and captured mutations]
prohibited_actions: [sam/AWS call, template/source write, snapshot update, second-file edit]
may_start_successor: false
```

Add exactly
`const W7_OWNER_REGISTRY = Object.freeze({"owner":"infrastructure","requiredCases":["W7-INFRA-01","W7-INFRA-02","W7-INFRA-03","W7-INFRA-04","W7-INFRA-05","W7-INFRA-06"],"requiredControls":["W7-NC-05","W7-NC-06","W7-NC-07","W7-NC-08","W7-NC-09"]}); // W7-REGISTRY`.
Load the current template and an embedded/captured baseline projection of all
pre-existing members; assert the six unique oracles from A4 and IF-5. Each
control deep-clones parsed data, makes its one listed mutation, observes the
unchanged owning oracle fail, then reruns a fresh positive. `LOCAL_NOW`: syntax
and full file test; require 6 cases/5 controls activated, zero fail/skip; diff
check.

- [ ] P1 revisions, assignment, file, digest, and predecessor match.
- [ ] P2 starting and protected state match.
- [ ] T1 exact transformation and no other edit.
- [ ] V1 all local checks and activation witnesses pass.
- [ ] V2 attributable changed-file set equals the writable file.
- [ ] V3 local coverage equality or exact I001 deferral is recorded.
- [ ] H1 exact diff, digest, commands, outcomes, and obligations return.
- [ ] H2 zero prohibited action, second file, successor, external action, or parent contact.
- [ ] H3 stop at `AWAITING_WINDOW_REVIEW`.

### `KI-W7-S012` - deterministic build enforcement

```yaml
subwindow_id: KI-W7-S012
type: FILE
parent_window_id: KI-W7
parent_assignment_id: ASG-KI-W7-WA-01
assigned_agent: UNASSIGNED
predecessors: [KI-W7-S011]
successor_reserved_for: WINDOW-AGENT
writable_file: email_scraper/test/keyword-intelligence-build.test.js
file_operation: CREATE
starting_file_digest: ABSENT
starting_repository_change_set_digest: 0770413486470eb489c0835293bfd60862a3d4db11f83b5bdf39aabd736dfbee
read_only_scope: [A1-A8 W7 case matrix, accepted S006/S011, email_scraper/scripts/build-lambda.js, email_scraper/scripts/build-keyword-worker.js, email_scraper/scripts/measure-keyword-worker-package.js, email_scraper/test/aws-pipeline-packaging.test.js]
authorized_actions: [create registry, synthetic inventory control, final-build assertions]
prohibited_actions: [run build/measurement locally in leaf, source ZIP edit/delete, sibling removal, second-file edit]
may_start_successor: false
```

Add exactly
`const W7_OWNER_REGISTRY = Object.freeze({"owner":"build","requiredCases":["W7-BUILD-01"],"requiredControls":["W7-NC-10"]}); // W7-REGISTRY`.
The W7-BUILD-01 test requires
the exact `KI_W7_BUILD_EVIDENCE_PATH` bridge frozen in Section 7.2, validates
its strict schema, hashes, current ZIP/measurement correspondence, and all seven
boolean assertions, then emits exactly one diagnostic with prefix
`KI_W7_BUILD_CASE_CERTIFICATE_V1=` and the Section 7.2 canonical JSON suffix. That diagnostic
is the sole activation certificate for `W7-BUILD-01`; neither CV3 nor another
test may record that case as executed. The NC-10 test invokes IF-6 validation
only on a temporary synthetic inventory containing `.env` and performs the
positive->failure->fresh-positive sequence. Actual two-build/archive/cold-
import evidence production is `DEFERRED_TO_I001_CV3`. `LOCAL_NOW`: syntax;
static marker/test-definition inspection only; diff check. It must not execute
or claim `W7-BUILD-01` locally.

- [ ] P1 revisions, assignment, file, digest, and predecessor match.
- [ ] P2 starting and protected state match.
- [ ] T1 exact transformation and no other edit.
- [ ] V1 all local checks and activation witnesses pass.
- [ ] V2 attributable changed-file set equals the writable file.
- [ ] V3 local coverage equality or exact I001 deferral is recorded.
- [ ] H1 exact diff, digest, commands, outcomes, and obligations return.
- [ ] H2 zero prohibited action, second file, successor, external action, or parent contact.
- [ ] H3 stop at `AWAITING_WINDOW_REVIEW`.

### `KI-W7-S013` - deployment guard and conformance enforcement

```yaml
subwindow_id: KI-W7-S013
type: FILE
parent_window_id: KI-W7
parent_assignment_id: ASG-KI-W7-WA-01
assigned_agent: UNASSIGNED
predecessors: [KI-W7-S012]
successor_reserved_for: WINDOW-AGENT
writable_file: email_scraper/test/keyword-intelligence-deployment-guard.test.js
file_operation: CREATE
starting_file_digest: ABSENT
starting_repository_change_set_digest: 86493ecb44e9625f814ba577353e18ab9d2b5d2fade82fcceec0fbe0488eb231
read_only_scope: [A1-A8 W7 case matrix, accepted S007-S012, all five W7 test owners, email_scraper/scripts/keyword-intelligence/create-change-set.js, email_scraper/scripts/keyword-intelligence/inspect-stack.js, email_scraper/infrastructure/aws/template.yaml]
authorized_actions: [create AWS-stubbed packet/change-set/inspection tests, exact five-owner conformance merge, exported focused-TAP parser and fail-closed parser CLI, parser-mode local controls]
prohibited_actions: [real AWS/network/provider/database call, credential read, production/template/source write, second-file edit]
may_start_successor: false
```

Add exactly
`const W7_OWNER_REGISTRY = Object.freeze({"owner":"deployment_guard","requiredCases":["W7-DEPLOY-01","W7-DEPLOY-02","W7-CONF-01"],"requiredControls":["W7-NC-11","W7-NC-12"]}); // W7-REGISTRY`.
Spawn only a temporary executable named `aws` whose captured
argv and deterministic JSON responses prove no real CLI path. Validate exact
template/two-ZIP packet, source/hash equality, both allowlists, token/reviewed-ID
fail-closed behavior, and disabled/active inspector projections. Merge the five
literal owner registries once; compare sorted-LF memberships/digests to the
frozen 12/12 sets; require zero skip/duplicate/unexpected/external calls. Both
controls perform the exact A4 mutations and fresh-positive rerun. `LOCAL_NOW`:
syntax and full file test with 3 cases/2 controls, zero fail/skip, AWS stub
invocation count exact and real network zero; the Section 7.2.1 unchanged TAP
plus four mutation CLI tests all pass, parser-mode output proves zero registered
or executed tests, and only caller-provided temporary output exists before
finally cleanup; diff check. Export exactly `parseFocusedTap` and
`runFocusedParserCli`, retain private `registerOwnedTests`, and implement the
exact direct-main discriminator/error/output protocol. Its registry merge is
source-only through `readOwnerRegistry`; it must not import another test file.
Complete combined case activation remains I001 CV4 because S012's build case
consumes CV3 evidence there.

- [ ] P1 revisions, assignment, file, digest, and predecessor match.
- [ ] P2 starting and protected state match.
- [ ] T1 exact transformation and no other edit.
- [ ] V1 all local checks and activation witnesses pass.
- [ ] V2 attributable changed-file set equals the writable file.
- [ ] V3 local coverage equality or exact I001 deferral is recorded.
- [ ] H1 exact diff, digest, commands, outcomes, and obligations return.
- [ ] H2 zero prohibited action, second file, successor, external action, or parent contact.
- [ ] H3 stop at `AWAITING_WINDOW_REVIEW`.

## 7. Initial integration assessment `KI-W7-I001`

```yaml
subwindow_id: KI-W7-I001
type: INTEGRATION_ASSESSMENT
parent_window_id: KI-W7
parent_assignment_id: ASG-KI-W7-WA-01
assigned_agent: KI-W7-WINDOW-AGENT
predecessors: [KI-W7-S001, KI-W7-S002, KI-W7-S003, KI-W7-S004, KI-W7-S005, KI-W7-S006, KI-W7-S007, KI-W7-S008, KI-W7-S009, KI-W7-S010, KI-W7-S011, KI-W7-S012, KI-W7-S013]
authorized_write_file: NONE
authorized_read_scope: [A1-A8, S1-S3, complete backend/frontend/root status and diff, all 13 W7 files, accepted W6 build evidence]
authorized_actions: [independent diff/source review, frozen local syntax/tests/builds/measurement/regression/secret scan, invoke accepted S013 parser CLI exactly once on CV4 output, coordination evidence/state updates]
prohibited_actions: [implementation edit, AWS/network/provider/database/browser action, secret value read, schema/package/frontend/unlisted edit, commit, push, KI-W8]
may_start_successor: false
```

I001 is fully frozen now; accepted leaf IDs/digests and executed evidence IDs are
filled only after independent leaf review.

### 7.1 Expected sets

- Expected assembled changed files: exact Section 2 set, count 13, digest
  `04ce71235fe61103c071f859d6050d4f8fee2b56dc0e088b9d97f5111be57a9f`.
- Required cases have count 12 and digest
  `6bacf5d9291362ee0d01f5d0d8e3e53f8f9e214a6ebbf5711497c80f3d74aa2e`.
- Required controls have count 12 and digest
  `6950a20f91b666c03cf59c495576e72ad1501fcd58aa5f4378900bd473edafd7`.

```json
{
  "requiredCases": [
    "W7-BUILD-01", "W7-CONF-01", "W7-DEPLOY-01", "W7-DEPLOY-02",
    "W7-INFRA-01", "W7-INFRA-02", "W7-INFRA-03", "W7-INFRA-04",
    "W7-INFRA-05", "W7-INFRA-06", "W7-RUNTIME-01", "W7-RUNTIME-02"
  ],
  "requiredControls": [
    "W7-NC-01", "W7-NC-02", "W7-NC-03", "W7-NC-04",
    "W7-NC-05", "W7-NC-06", "W7-NC-07", "W7-NC-08",
    "W7-NC-09", "W7-NC-10", "W7-NC-11", "W7-NC-12"
  ]
}
```

### 7.2 Build-evidence bridge

I001 creates exactly one temporary directory before CV3 with
`mktemp -d "${TMPDIR:-/tmp}/ki-w7-i001.XXXXXX"`, records its canonical absolute
path as `KI_W7_EVIDENCE_DIR`, and derives the sole bridge path as
`${KI_W7_EVIDENCE_DIR}/build-evidence.json`. It passes that file to CV4 only as
the environment variable `KI_W7_BUILD_EVIDENCE_PATH`; no argument, alias,
fallback, glob, search, workspace evidence file, or inherited value is allowed.

After the second keyword build and second measurement have passed every CV3
oracle, CV3 writes the bridge once, with mode `0600`, by writing
`${KI_W7_EVIDENCE_DIR}/build-evidence.json.tmp`, fsyncing/closing it, and
renaming it to `build-evidence.json`. It is UTF-8 canonical JSON (two-space
indent, one final LF), has no unknown member, and has exactly this schema:

The root key order is exactly `schema`, `producerAssessmentId`,
`producerGateId`, `keyword`, `stableMeasurementSha256`,
`establishedZipHashes`, `assertions`. The first three values are the literals
`ki-w7-build-evidence-v1`, `KI-W7-I001`, and `KI-W7-CV3`. `keyword` has exactly
the ordered keys `path`, `firstSha256`, `secondSha256`, `zipBytes`,
`unzippedBytes`, `fileListHash`, `requiredEngine`, `enginePresent`, and
`coldImportHandlerType`: path is `dist/lambda/keyword-worker.zip`; all SHA
members are strings matching `^[a-f0-9]{64}$`; first/second hashes are equal;
sizes are JSON integers in `1..47185920` and `1..209715200`; required engine is
the literal `libquery_engine-rhel-openssl-3.0.x.so.node`; and the last two values
are literal `true` and `function`. `stableMeasurementSha256` has only `first`
and `second`, both lowercase SHA-256 strings and equal. `assertions` has exactly
the ordered keys `keywordByteIdentical`, `establishedSiblingsUnchanged`,
`inventorySafe`, `zipWithinLimit`, `expandedWithinLimit`, `exactEngine`, and
`coldImport`, each literal `true`.

`establishedZipHashes` contains exactly seven objects, each with only ordered
keys `path` and `sha256`, sorted by unsigned UTF-8 path. Paths are exactly
`dist/lambda/discovery-worker.zip`, `dist/lambda/domain-aggregator.zip`,
`dist/lambda/lead-worker.zip`, `dist/lambda/lead-aggregator.zip`,
`dist/lambda/traffic-worker.zip`, `dist/lambda/final-aggregator.zip`, and
`dist/lambda/recovery.zip`; hashes match `^[a-f0-9]{64}$` and equal both the
pre-CV3 snapshot and post-second-keyword-build files.
`stableMeasurementSha256.first/second`
hash canonical stable projections of the respective measurement reports after
removing only `durationMs`, `rssBytes`, and `rssDeltaBytes`; they must equal.
The bridge contains no absolute path, environment value, credential, provider
body, account identifier, or measured RSS/duration.

S012 is the only consumer and the only source of the W7-BUILD-01 activation
certificate. It requires the environment variable to be one canonical absolute
regular nonsymlink file named `build-evidence.json` inside the live directory
whose basename matches `^ki-w7-i001\.[A-Za-z0-9]{6}$`; reads at most 65536 bytes;
strictly checks every key/type/bound/equality above; recomputes the current
keyword ZIP, seven sibling ZIP, and current stable measurement hashes; and
fails before recording execution on missing, malformed, stale, extra, unequal,
or privacy-unsafe data. On success it emits exactly one diagnostic prefixed
`KI_W7_BUILD_CASE_CERTIFICATE_V1=`. The suffix is canonical JSON with exactly
ordered keys `schema`, `caseId`, `evidenceSha256`, `activated`, `assertions`;
values are respectively `ki-w7-build-case-certificate-v1`, `W7-BUILD-01`, the
lowercase SHA-256 of the exact bridge bytes, literal `true`, and the exact array
`["keywordByteIdentical","establishedSiblingsUnchanged","inventorySafe","zipWithinLimit","expandedWithinLimit","exactEngine","coldImport"]`.
I001 accepts exactly one such diagnostic and rejects zero, two, malformed, or
different members. One outer `try/finally` begins immediately after `mktemp`
and encloses CV3 plus CV4. Its `finally` always validates the canonical temp
directory still matches the derived path, removes only that directory with
`fs.rm(...,{recursive:true,force:false})`, and asserts it is absent, including
CV3 failure before bridge emission and CV4 failure. S3 retains only
privacy-safe hashes/assertions.

#### 7.2.1 Runtime execution-accounting protocol

Every W7 case is one top-level `node:test` whose exact name matches
`^\[W7 CASE (W7-(?:RUNTIME|INFRA|BUILD|DEPLOY|CONF)-[0-9]{2})\] [^\r\n]+$`.
Every W7 control is one top-level test whose name matches
`^\[W7 CONTROL (W7-NC-[0-9]{2})\] [^\r\n]+$`. Non-W7 tests in the focused files
retain their names and are ignored only when neither their test name nor any
diagnostic line begins with a W7 prefix. Any malformed line containing
`[W7 `, `KI_W7_EXECUTION_RECORD_V1=`, or
`KI_W7_BUILD_CASE_CERTIFICATE_V1=` fails closed.

After the final owning oracle passes, each case emits once through
`t.diagnostic` the prefix `KI_W7_EXECUTION_RECORD_V1=` followed by canonical
JSON with exactly ordered keys `schema`, `id`, `kind`, `owner`, `executed`,
`activated`, `oraclePassed`, `skipped`. Values are
`ki-w7-execution-record-v1`, the test ID, `case`, its exact IF-8 owner, three
literal `true` values, and literal `false`. After its unchanged positive,
injected failure, and fresh-positive rerun all pass, each control emits once
through `t.diagnostic` the same prefix plus canonical JSON with exactly ordered
keys `schema`, `id`, `kind`, `owner`, `executed`, `activated`,
`positivePassed`, `mutationFalsified`, `freshPositivePassed`, `skipped`; values
are the same schema/ID/owner, `control`, five literal `true` values, and final
literal `false`. No record is emitted in `before`, `after`, module load, a
nested test, or a failure/skip path. W7-BUILD-01 emits this execution record
only after its separate Section 7.2 build diagnostic; the two prefixes remain
distinct.

CV4 uses the exact reporter additions
`--test-reporter=tap --test-reporter-destination="$KI_W7_EVIDENCE_DIR/focused.tap"`.
The destination must be absent before the process, a regular nonsymlink file
after it, no larger than 4194304 bytes, and remain inside the canonical evidence
directory. Process exit must be zero. The accepted S013 export
`parseFocusedTap(text,{buildEvidenceBytes})` then operates on UTF-8
LF-normalized lines without importing any test module. `text` must be a string
whose UTF-8 encoding is at most 4194304 bytes; `buildEvidenceBytes` must be a
Buffer of 1..65536 bytes containing the strict Section 7.2 bridge:

1. collect only top-level lines matching
   `^# Subtest: \[W7 (CASE|CONTROL) ([A-Z0-9-]+)\] ([^\r\n]+)$` and their
   corresponding top-level result lines matching
   `^(ok|not ok) [0-9]+ - \[W7 (CASE|CONTROL) ([A-Z0-9-]+)\] ([^\r\n]+)(?: # (SKIP|TODO).*)?$`;
2. reject missing result, `not ok`, `SKIP`, `TODO`, kind/ID/title mismatch,
   duplicate test ID, malformed W7-prefixed line, or a registered ID absent
   from the top-level names;
3. collect diagnostic lines matching
   `^[ ]*# KI_W7_EXECUTION_RECORD_V1=(\{.*\})$`, strict-parse the applicable
   case/control union above, and reject an extra key, wrong type/owner/kind,
   duplicate/unexpected ID, false activation/oracle/control phase, or skip;
4. separately collect exactly one line matching
   `^[ ]*# KI_W7_BUILD_CASE_CERTIFICATE_V1=(\{.*\})$`, validate Section 7.2,
   and require its evidence hash to equal the exact bridge bytes;
5. parse the five IF-8 source markers without module import, require
   required=registered top-level names=execution-record IDs, and require exact
   12-case/12-control members and frozen digests; and
6. ignore a non-W7 test only after proving its name/diagnostics contain no W7
   prefix; record the ignored non-W7 top-level count without treating it as a
   required, skipped, duplicate, or unexpected W7 member.

S013 also exports `runFocusedParserCli(argv)`. Its exact argv is
`["--parse-w7-focused-tap","--tap",tapAbsolute,"--build-evidence",buildAbsolute,"--output",outputAbsolute]`;
no omission, reordering, repeated flag, relative path, extra argument, alias, or
environment fallback is accepted. All three paths must be canonical absolute,
regular/nonsymlink where inputs, absent where output, and have exact basenames
`focused.tap`, `build-evidence.json`, and `focused-certificate.json` inside the
same live directory whose basename matches
`^ki-w7-i001\.[A-Za-z0-9]{6}$`. Input bounds are 4194304 and 65536 bytes.
Output and sibling `focused-certificate.json.tmp` must both be absent before
parsing.

The S013 CLI is the sole aggregate-certificate emitter and I001 CV4 is the sole
acceptance site. After parsing succeeds, the CLI writes canonical JSON to the
`.tmp` sibling with mode `0600`, fsyncs/closes, renames it atomically to
`${KI_W7_EVIDENCE_DIR}/focused-certificate.json`, and prints only
`KI_W7_FOCUSED_CERTIFICATE_WRITTEN ` followed by the lowercase output SHA-256
and LF. Canonical JSON has exactly ordered root keys
`schema`, `producerAssessmentId`, `producerGateId`, `requiredCases`,
`registeredCases`, `executedCases`, `activatedCases`, `requiredControls`,
`registeredControls`, `executedControls`, `activatedControls`,
`falsifiedControls`, `freshPositiveControls`, `skippedIds`, `duplicateIds`,
`unexpectedIds`, `unactivatedIds`, `buildCaseCertificate`,
`ignoredNonW7TopLevelCount`, `result`. The first three values are literals
`ki-w7-focused-certificate-v1`, `KI-W7-I001`, `KI-W7-CV4`; every case array is
the exact sorted twelve-case set; every control array is the exact sorted
twelve-control set; the four exception arrays are empty; `buildCaseCertificate`
is the strict Section 7.2 object; ignored count is a nonnegative integer; and
result is `PASS`. CV4 rereads and strict-validates those bytes once and matches
the stdout hash; no test
file, diagnostic, summary count, console narrative, or S013 assertion can
substitute for this certificate.

The S013 direct-main discriminator is exact: direct invocation means
`pathToFileURL(path.resolve(process.argv[1])).href === import.meta.url`; parser
mode additionally requires `process.argv[2] === "--parse-w7-focused-tap"`.
Parser mode calls only `runFocusedParserCli(process.argv.slice(2))` and
registers/runs zero `node:test` tests. Non-parser mode calls the private
`registerOwnedTests()` exactly once, preserving ordinary `node --test`
behavior. A parser/CLI failure uses only
`Object.assign(new Error("W7_EXECUTION_CERTIFICATE_INVALID"),{code:"W7_EXECUTION_CERTIFICATE_INVALID"})`;
direct CLI catches it, removes only its own `.tmp` if created, leaves output
absent, writes exactly `W7_EXECUTION_CERTIFICATE_INVALID` plus LF to stderr,
sets exit code 1, and prints no stack, input, JSON, path, or credential.

S013 `LOCAL_NOW` constructs one complete synthetic accepted TAP/build bridge
and invokes the real CLI in six directories, each created only by
`mktemp -d "${TMPDIR:-/tmp}/ki-w7-i001.XXXXXX"`: initial unchanged, one
execution record removed, one record duplicated, ` # SKIP` appended to one W7
result, one record's `activated:true` changed to false, and final unchanged.
Unchanged exits 0, emits the exact stdout hash, creates only its caller-provided
temporary output, contains 12/12 exact sets, and stdout/TAP prove zero nested
test execution by parser mode. Each mutation exits 1 with the exact safe error,
no output, and the expected missing/duplicate/skipped/unactivated rejection;
then unchanged succeeds again byte-identically. S013 removes only those temp
directories in `finally` and asserts absence. The same four controls are
`LOCAL_NOW` proof and need not be reinvented by I001; CV4 invokes the accepted
CLI once on real TAP. These parser controls are not new W7 coverage IDs. The
outer Section 7.2 `finally` removes the TAP, bridge, aggregate certificate, and
their sole containing directory.

### 7.3 Frozen gates, in exact order

1. **CV1 authority/diff:** recompute every pin and current file digest; require
   all 13 leaves independently `ACCEPTED_FOR_INTEGRATION`; backend actual
   changed set equals expected, frontend remains clean, protected root files
   equal their post-decomposition recorded digests except S1-S3; inspect every
   complete diff and interface IF-1-IF-8.
2. **CV2 static:** from `email_scraper/`, run `node --check` once for the seven
   JS production/scripts plus the five test files (12 JS files; template is the
   thirteenth path), parse template JSON once, and run `git diff --check` for
   all 13 paths. Require all zero.
3. **CV3 build/measurement and bridge production (costly, once):** snapshot SHA-256 of all existing
   `dist/lambda/*.zip`; run `node scripts/build-lambda.js` once; record the
   seven established ZIP hashes. Run `node scripts/build-keyword-worker.js`,
   hash keyword ZIP and all seven siblings, run
   `node scripts/measure-keyword-worker-package.js` and retain its stable
   projection in memory. Run the keyword
   builder a second and final time, require the same keyword ZIP hash and all
   seven sibling hashes unchanged, rerun measurement, and require equal stable
   projections excluding only duration/RSS values. Require one safe inventory,
   one required engine, ZIP <=45 MiB, expanded <=200 MiB, importable
   `index.mjs` exporting function `handler`, and no forbidden/stale member.
   Only after those assertions pass, emit the Section 7.2 bridge. CV3 does not
   register, execute, or certify `W7-BUILD-01`. Build output is authorized
   gitignored output; no source path may change.
4. **CV4 focused enforcement and sole build-case activation:** run exactly
   `KI_W7_BUILD_EVIDENCE_PATH="$KI_W7_EVIDENCE_DIR/build-evidence.json" node --test --test-isolation=none --test-reporter=tap --test-reporter-destination="$KI_W7_EVIDENCE_DIR/focused.tap" test/aws-pipeline-runtime-adapters.test.js test/keyword-intelligence-deployment-runtime.test.js test/keyword-intelligence-infrastructure.test.js test/keyword-intelligence-build.test.js test/keyword-intelligence-deployment-guard.test.js`.
   After exit zero, run exactly
   `node test/keyword-intelligence-deployment-guard.test.js --parse-w7-focused-tap --tap "$KI_W7_EVIDENCE_DIR/focused.tap" --build-evidence "$KI_W7_EVIDENCE_DIR/build-evidence.json" --output "$KI_W7_EVIDENCE_DIR/focused-certificate.json"`.
   Require parser exit zero, the sole safe stdout hash line, empty stderr, and
   zero TAP/test output from parser mode.
   Require required=registered=executed for 12 cases, all 12 controls falsified,
   zero fail/skip/duplicate/unexpected/unactivated, exact digests, zero real
   external call, exactly one valid Section 7.2 build-case diagnostic, and the
   exact Section 7.2.1 aggregate certificate. Reconfirm by S013 ending digest
   that its accepted LOCAL_NOW missing/duplicate/skip/unactivated controls are
   uninvalidated; do not rerun or reimplement them in I001.
   Remove the bridge directory in the mandatory `finally` after capturing its
   SHA and assert absence.
5. **CV5 full regression (once after final edit/build):** `npm test`; require
   exit 0, no failing test, and only the seven established guarded integration
   skips when database opt-in is absent. If localhost/sandbox denial alone
   invalidates it, apply the one identical E8.1 recovery. No changed filter or
   timeout is permitted.
6. **CV6 secrets (once):** `npm run check:secrets`; require exit 0 and no
   credential/private value. Do not inspect secret values.
7. **CV7 independent closure:** recompute the path/case/control digests plus the
   exact logical parameter/condition/resource/output and IAM/property sets;
   verify every control positive->mutation failure->fresh positive; scan for
   `sam deploy`, `ScalingConfig` in keyword mapping, second recovery schedule,
   wildcard keyword data-plane resource/action, direct environment reads in
   consumers, real AWS/provider/network/database calls, source package/schema/
   migration/frontend changes, commit/push, and KI-W8 actions. Every forbidden
   count is zero.

No AWS, provider, database, browser, requester approval, or paid gate is needed
for I001. Predictable expensive operations are exactly seven established builds
within one `build-lambda` invocation, two keyword builds, two keyword
measurements, one full npm regression, and one secret scan. No `sam` binary is
required.

### 7.4 Substitute and accepted-test policy

AWS spawn stubs prove only command/guard behavior; parsed template proves only
local emitted infrastructure; in-memory Prisma/S3/SQS markers prove constructor
identity/call ordering only; synthetic ZIP inventory proves rejection logic,
while the real local ZIP gate proves packaging. None proves applied AWS,
credentials, quotas, Neon, providers, pricing, or production runtime. Existing
tests/fixtures cannot be deleted or weakened. A correction to any source, test,
fixture, script, template, builder, measurement output, bridge producer/schema/
consumer, registry parser, W7 test name/diagnostic, reporter destination,
execution parser, or aggregate-certificate schema invalidates CV1-CV4, CV6-CV7 and every parent-final
gate. CV3 evidence cannot be reused after any such input changes because CV4 is
cryptographically bound to it. CV5 may be reused only with a recorded exact
input/path dependency proof; otherwise it reruns once after the final edit.

### 7.5 Result oracle and checklist

- `PASS`: all gates pass, exact sets/digests/counts match, no unresolved
  invalidation/prohibition, and the Section 12.4 certificate is complete;
  result is `READY_FOR_PARENT_REVIEW` only.
- `CORRECTION_REQUIRED`: a diagnosed file-local defect governed by current
  parent decisions; append minimum one-file correction(s) and `I002`.
- `PARENT_BLOCKED`: missing/contradictory decision, expanded scope/authority,
  unknown external contract, or unavailable required prerequisite.

- [ ] I1 Verify all 13 leaves were independently accepted.
- [ ] I2 Verify actual assembled files equal planned set within parent scope.
- [ ] I3 Verify complete requirement/decision trace to current source/assertions.
- [ ] I4 Execute all frozen gates with activation witnesses.
- [ ] I5 Verify required=registered=executed cases/controls, digests, zero exceptions.
- [ ] I6 Execute every required negative control and observe the prescribed failure.
- [ ] I7 Verify substitute fidelity and accepted test/fixture integrity.
- [ ] I8 Verify zero prohibited/successor/external/destructive/secret/out-of-scope action.
- [ ] I9 Independently inspect source and complete diff; do not rely on leaf summaries.
- [ ] I10 Record exact PASS, CORRECTION_REQUIRED, or PARENT_BLOCKED evidence.

## 8. Correction and reassessment protocol

A failed local or integration assertion is first recorded with observed result,
expected result, activation path, root-cause file, governing parent decision,
and invalidated evidence/gates. A file-local remedy gets the next unused
`KI-W7-C###`, one exact file/current digest, one new assignment, and every
Section 7 field/check. A cross-file or missing-decision remedy is returned to
the parent. The window agent never edits implementation. Completed blocks and
failed evidence stay immutable. After corrections, the window agent appends the
next `KI-W7-I###`; leaf success never substitutes for reassessment.

## 9. Traceability and enforcement closure

| Parent task | Files/sub-windows | Executable assertions |
|---|---|---|
| `KI-W7-T1` | F-001/S001, F-002/S002, F-009/S009 | `W7-RUNTIME-01`, `W7-NC-01/02`, IF-1/2 |
| `KI-W7-T2` | F-003/S003, F-004/S004, F-010/S010 | `W7-RUNTIME-02`, `W7-NC-03/04`, IF-3/4 |
| `KI-W7-T3` | F-005/S005, F-011/S011 | `W7-INFRA-01-06`, `W7-NC-05-09`, IF-5 |
| `KI-W7-T4` | F-006/S006, F-012/S012 | `W7-BUILD-01`, `W7-NC-10`, IF-6, CV3/CV4 bridge |
| `KI-W7-T5` | F-007/S007, F-008/S008, F-013/S013 | `W7-DEPLOY-01/02`, `W7-NC-11/12`, IF-7/8 |
| `KI-W7-T6` | F-009-F-013/S009-S013, I001 | `W7-CONF-01`, exact merged sets/digests, all controls, S013 parser/CLI and CV4 aggregate certificate |

`SCN-KI-047` is activated only by the assembled I001 physical schedule. No
single leaf claims whole-window parity. `KI-W7-V1-V6` map respectively to
CV1/CV7, CV2/CV4, CV3, CV5/CV6, CV7, and CV7; `KI-W7-H1/H2` remain the
window-agent handoff boundary after execution authority exists.

## 10. Mandatory decomposition-readiness checklist

### Authority and inheritance

- [x] `SW-A01` Assignment, identity, and delegation are exact/current. Evidence: `EV-KI-W7-S001`.
- [x] `SW-A02` Standards and A1-A5/A8 revisions match. Evidence: `EV-KI-W7-S001`.
- [x] `SW-A03` Parent scopes/boundaries copied without expansion. Evidence: `EV-KI-W7-S001`.
- [x] `SW-A04` Repositories/dirty state/owner changes inventoried. Evidence: `EV-KI-W7-S001`.
- [x] `SW-A05` S1/S2/S3 exist with non-overlapping authority. Evidence: `EV-KI-W7-S013`.
- [x] `SW-A06` Strict adjacency/no leaf delegation enforced. Evidence: `EV-KI-W7-S004`.
- [x] `SW-A07` E8.1 policy copied without external expansion. Evidence: `EV-KI-W7-S004`.

### Decision and file-set closure

- [x] `SW-D01` Every parent member maps to files/assertions. Evidence: `EV-KI-W7-S002`.
- [x] `SW-D02` No missing/contradictory parent decision remains. Evidence: `EV-KI-W7-S002`.
- [x] `SW-D03` Required changed set equals planned set. Evidence: `EV-KI-W7-S002`.
- [x] `SW-D04` Thirteen files have thirteen unique initial owners. Evidence: `EV-KI-W7-S002`.
- [x] `SW-D05` Operations/digests/anchors/interfaces/preservation are exact. Evidence: `EV-KI-W7-S002`.
- [x] `SW-D06` Serial DAG is complete/acyclic; no parallel dispatch inferred. Evidence: `EV-KI-W7-S003`.
- [x] `SW-D07` IF-1 through IF-8 are frozen before consumers. Evidence: `EV-KI-W7-S003`.
- [x] `SW-D08` Intermediate states/deferrals/safety/resolvers exact. Evidence: `EV-KI-W7-S003`.
- [x] `SW-D09` Production/test/config/template/script files have separate leaves. Evidence: `EV-KI-W7-S002`.
- [x] `SW-D10` No rename/multi-output/generator/incidental leaf write. Evidence: `EV-KI-W7-S004`.

### Sub-window execution completeness

- [x] `SW-E01` Every file block contains Section 7 fields. Evidence: `EV-KI-W7-S004`.
- [x] `SW-E02` Ordered edits are exact; no material alternatives. Evidence: `EV-KI-W7-S004`.
- [x] `SW-E03` Preflight/local checks/witnesses/forbidden outcomes exact. Evidence: `EV-KI-W7-S004`.
- [x] `SW-E04` Every leaf requires attributable one-file equality. Evidence: `EV-KI-W7-S004`.
- [x] `SW-E05` Evidence/handoff/stop/successor reservation exact. Evidence: `EV-KI-W7-S004`.
- [x] `SW-E06` Leaves report only to window agent and cannot edit authority. Evidence: `EV-KI-W7-S004`.
- [x] `SW-E07` File-local acceptance does not require successor work. Evidence: `EV-KI-W7-S004`.
- [x] `SW-E08` Deferred checks name I001. Evidence: `EV-KI-W7-S003`.

### Enforcement and integration closure

- [x] `SW-V01` Cases/controls allocated to exact owners/witnesses. Evidence: `EV-KI-W7-S003`.
- [x] `SW-V02` Local/whole set equality and digests prescribed. Evidence: `EV-KI-W7-S003`.
- [x] `SW-V03` Every critical invariant has its narrow control. Evidence: `EV-KI-W7-S003`.
- [x] `SW-V04` Substitute/accepted-test fidelity and invalidation exact. Evidence: `EV-KI-W7-S003`.
- [x] `SW-V05` I001 is fully authored with zero implementation write. Evidence: `EV-KI-W7-S003`.
- [x] `SW-V06` Gates are exact/risk-proportionate/finally scheduled. Evidence: `EV-KI-W7-S003`.
- [x] `SW-V07` Diagnosis/correction/invalidation/reassessment complete. Evidence: `EV-KI-W7-S004`.
- [x] `SW-V08` Independent leaf review/personal assessment mandatory. Evidence: `EV-KI-W7-S004`.
- [x] `SW-V09` Zero-work/skip/filter/duplicate/unactivated/summary evidence cannot pass. Evidence: `EV-KI-W7-S004`.
- [x] `SW-V10` Parent handoff and review boundary exact. Evidence: `EV-KI-W7-S004`.
- [x] `SW-V11` Sandbox invalidation vs real failure and one recovery exact. Evidence: `EV-KI-W7-S004`.

### Mechanical and adversarial audit

- [x] `SW-R01` IDs unique/references resolve. Evidence: `EV-KI-W7-S004`.
- [x] `SW-R02` No unresolved assignable placeholder. Evidence: `EV-KI-W7-S004`.
- [x] `SW-R03` Write-set lint rejects zero/two/wildcard/directory/rename/output. Evidence: `EV-KI-W7-S004`.
- [x] `SW-R04` Removing a file/mapping fails readiness. Evidence: `EV-KI-W7-S004`.
- [x] `SW-R05` Missing/duplicate/skip/filter/bypass case fails acceptance. Evidence: `EV-KI-W7-S004`.
- [x] `SW-R06` Weakened oracle/divergent substitute invalidates evidence. Evidence: `EV-KI-W7-S004`.
- [x] `SW-R07` Second-file edit/direct parent communication rejected. Evidence: `EV-KI-W7-S004`.
- [x] `SW-R08` Integration failure requires new correction. Evidence: `EV-KI-W7-S004`.
- [x] `SW-R09` Parent review required before first assignment. Evidence: `EV-KI-W7-S013`.
- [x] `SW-R10` Document lint reports zero structural omissions/conflicts. Evidence: `EV-KI-W7-S004`.
- [x] `SW-R11` Identical sandbox recovery accepted; changed/failing/external recovery rejected. Evidence: `EV-KI-W7-S004`.

Checked authoring items: 47. Unchecked authoring items: 0.

## 11. Handoff templates and append-only amendments

### 11.1 Leaf certificate

Every leaf returns the exact Section 12.3 `FILE-SUBWINDOW-EXECUTED`
certificate from the sub-window standard, with this parent/assignment, its
current digests, exact case/control arrays, commands, deferrals, zero external
mutations, `successor_work_started:false`, `direct_parent_communication:false`,
and `status:AWAITING_WINDOW_REVIEW`. The window agent appends a distinct review
disposition in S3.

### 11.2 Integration and parent handoff

I001 PASS returns the exact Section 12.4
`WINDOW-AGENT-INTEGRATION-PASS` certificate and a consolidated Section 12.5
report. It names all accepted/corrective/failed/superseding IDs, exact file and
case sets/digests, commands/outcomes, negative controls, substitute limits,
invalidations, external mutations/costs (none), skipped gates, residual W8
prerequisites, and confirms `successor_parent_window_work_started:false`.

### 11.3 Append-only correction area

No corrective sub-window exists at decomposition time. Append future diagnosed
`KI-W7-C###` and `KI-W7-I###` blocks below this line; never rewrite Sections
0-11 or completed evidence.

### `KI-W7-C001` - make the build owner inert in ordinary regression mode

```yaml
subwindow_id: KI-W7-C001
type: FILE_CORRECTION
parent_window_id: KI-W7
parent_assignment_id: ASG-KI-W7-WA-02
assigned_agent: UNASSIGNED
predecessors: [KI-W7-I001-CV5-FAIL]
successor_reserved_for: KI-W7-WINDOW-AGENT
writable_file: email_scraper/test/keyword-intelligence-build.test.js
file_operation: MODIFY
starting_file_digest: 18dcf90026119d2aa98a6b4e1e06ab47647f596adc5033c24d3941f13f0e2731
read_only_scope: [I001 CV5 failure EV-KI-W7-S028, accepted S012, Section 7.2 and 7.2.1]
authorized_actions: [add the exact ordinary-regression nonactivation branch to W7-BUILD-01, run correction-local syntax absent-environment and static checks]
prohibited_actions: [change bridge schema consumer certificate execution record NC-10 or test name, build or measurement, second-file edit, external action]
may_start_successor: false
```

Diagnosis: CV4 necessarily supplies `KI_W7_BUILD_EVIDENCE_PATH`, but frozen CV5
is the ordinary `npm test` process and supplies no bridge. The accepted S012
therefore fails at `readStrictBuildEvidence()` before regression can run. This
is a test-mode integration defect, not a product/build failure.

Apply exactly one guarded branch at the beginning of the existing
`W7-BUILD-01` callback, before `readStrictBuildEvidence()`:

```js
if (process.env.KI_W7_BUILD_EVIDENCE_PATH === undefined) {
  assert.equal(Object.hasOwn(process.env, "KI_W7_BUILD_EVIDENCE_PATH"), false);
  return;
}
```

No other byte changes. This branch is ordinary-regression nonactivation: the
top-level test passes but emits neither the build-case certificate nor the
W7-BUILD-01 execution record. An empty, relative, stale, malformed, or present
bridge still enters the strict accepted S012 path and fails closed. CV4 still
supplies the exact absolute bridge and remains the sole W7-BUILD-01 activation
and certificate source.

`LOCAL_NOW`: `node --check`; with only
`KI_W7_BUILD_EVIDENCE_PATH` removed, run the complete build-owner file and
require 2 pass/0 fail/0 skip, exactly one NC-10 execution diagnostic and zero
W7-BUILD-01 execution/build-certificate diagnostics; exact-source assertion
requires one guard before one `readStrictBuildEvidence()` call and proves the
strict present-value path is otherwise byte-identical; `git diff --check`.

### `KI-W7-I002` - post-C001 full reassessment

```yaml
subwindow_id: KI-W7-I002
type: INTEGRATION_REASSESSMENT
parent_window_id: KI-W7
parent_assignment_id: ASG-KI-W7-WA-02
assigned_agent: KI-W7-WINDOW-AGENT
predecessors: [KI-W7-C001]
authorized_write_file: NONE
authorized_read_scope: [A1-A8, S1-S3, all thirteen W7 paths and build outputs]
authorized_actions: [repeat invalidated CV1-CV4 once after accepted C001, run CV5 once after final correction with E8.1 identical elevated recovery only for proven sandbox denial, then CV6-CV7]
prohibited_actions: [implementation edit, database browser network provider AWS paid action, credential read, commit push KI-W8]
may_start_successor: false
```

I002 reruns CV1-CV4 because C001 changes an enforcement owner and invalidates
the bridge/certificate closure. It then runs the frozen CV5 `npm test`, CV6
secret scan, and CV7 closure exactly as Sections 7.3-7.5 specify. The C001
ordinary-regression branch is additionally rejected if it emits a build case
record/certificate without the bridge, skips the test, accepts a present bad
path, changes NC-10, or changes the CV4 certificate/digests. PASS returns only
`READY_FOR_PARENT_REVIEW`; KI-W8 remains prohibited.

### `KI-W7-C002` - register S013 under multi-file nonisolated node:test

```yaml
subwindow_id: KI-W7-C002
type: FILE_CORRECTION
parent_window_id: KI-W7
parent_assignment_id: ASG-KI-W7-WA-02
assigned_agent: UNASSIGNED
predecessors: [KI-W7-I002-CV4-FAIL]
successor_reserved_for: KI-W7-WINDOW-AGENT
writable_file: email_scraper/test/keyword-intelligence-deployment-guard.test.js
file_operation: MODIFY
starting_file_digest: 91b6bd11f5b56da5fe07c26d67395b15573a26a87d2b39df61eaa2c2f7e3f79a
read_only_scope: [I002 CV4 TAP failure EV-KI-W7-S030, accepted S013, Section 7.2.1]
authorized_actions: [add exact node:test process discriminator and broaden only the ordinary registration condition, run local combined-registration and parser-zero-test checks]
prohibited_actions: [change parser CLI registry cases controls diagnostics schemas or owner tests, second-file edit, build external action]
may_start_successor: false
```

Diagnosis: with `--test-isolation=none` and five input files, Node sets
`process.argv[1]` to the first file. S013 is imported later, so its current
`directInvocation` is false and none of its five owned tests register. The real
TAP contains only 9 cases and 10 controls; the strict parser correctly rejects
it. Node exposes the unambiguous ordinary-test signal as
`process.execArgv.includes("--test")`; the accepted parser wrapper/direct CLI
do not carry that argument.

Immediately before the existing final direct-mode conditional, add exactly:

```js
const nodeTestMode = process.execArgv.includes("--test");
```

Change only the final ordinary registration condition from
`else if (directInvocation)` to
`else if (directInvocation || nodeTestMode)`. Preserve the exact direct parser
branch first. Thus direct parser mode still registers zero tests; imported
parser-wrapper mode has neither signal and registers zero; direct ordinary and
multi-file node:test modes each call `registerOwnedTests()` exactly once.

`LOCAL_NOW`: syntax; exact-source/inverse-start-digest check; a two-file
`--test-isolation=none` run with runtime adapters first must activate S013's
exact 3 cases/2 controls once; direct parser mode on a valid synthetic fixture
must emit only its safe hash line and zero TAP; importing S013 from a plain
non-test ESM process must register/run zero tests; `git diff --check`.

### `KI-W7-I003` - post-C002 final reassessment

```yaml
subwindow_id: KI-W7-I003
type: INTEGRATION_REASSESSMENT
parent_window_id: KI-W7
parent_assignment_id: ASG-KI-W7-WA-02
assigned_agent: KI-W7-WINDOW-AGENT
predecessors: [KI-W7-C002]
authorized_write_file: NONE
authorized_read_scope: [A1-A8, S1-S3, all thirteen W7 paths and build outputs]
authorized_actions: [repeat invalidated CV1-CV4 after accepted C002, then execute CV5-CV7 and final handoff]
prohibited_actions: [implementation edit, database browser network provider AWS paid action, credential read, commit push KI-W8]
may_start_successor: false
```

I003 repeats CV1-CV4 under the frozen invalidation rule, including fresh builds
and the aggregate certificate. It then runs CV5 once, using only one identical
elevated recovery if the sandbox alone invalidates it, followed by CV6/CV7.
PASS requires all 12 cases, all 12 controls, zero exceptions, ordinary npm
regression closure, no external call/cost and only `READY_FOR_PARENT_REVIEW`.

### `KI-W7-C003` - reconcile preserved infrastructure topology totals

```yaml
subwindow_id: KI-W7-C003
type: FILE_CORRECTION
parent_window_id: KI-W7
parent_assignment_id: ASG-KI-W7-WA-03
assigned_agent: UNASSIGNED
predecessors: [KI-W7-I003-CV5-FAIL]
successor_reserved_for: KI-W7-WINDOW-AGENT
writable_file: email_scraper/test/aws-pipeline-infrastructure.test.js
file_operation: MODIFY
starting_file_digest: 3bfa45fab2beb2613be395e2a903fa87cdfef2a3b8c558073483acd504da13f8
read_only_scope: [EV-KI-W7-S032, accepted S005 template topology, email_scraper/infrastructure/aws/template.yaml, email_scraper/scripts/measure-lambda-packages.js, Sections 7.3-7.5]
authorized_actions: [apply exactly four frozen assertion-literal replacements, run correction-local syntax exact-source inverse-digest focused-test and diff checks, return for independent window-agent review]
prohibited_actions: [production template script package fixture or second-file edit, build measurement database browser network provider AWS paid credential commit push KI-W8 action, successor dispatch]
may_start_successor: false
```

The accepted W7 template adds exactly ten resources: `KeywordResearchDlq`,
`KeywordResearchQueue`, `KeywordWorkerLogGroup`, `KeywordWorkerRole`,
`KeywordWorker`, `KeywordResearchMapping`, and the four keyword alarm resources.
The role count therefore changes by one and the alarm count by four. Modify only
these four complete assertion lines, each exactly once:

```text
assert.equal(roles.length, 7);                         -> assert.equal(roles.length, 8);
assert.equal(alarms.length, 27);                       -> assert.equal(alarms.length, 31);
assert.equal(Object.keys(template.Resources).length, 72); -> assert.equal(Object.keys(template.Resources).length, 82);
assert.equal(packet.full.resources.length, 72);        -> assert.equal(packet.full.resources.length, 82);
```

No other count, topology assertion, expected set, production byte, or test
behavior may change. `LOCAL_NOW`, from `email_scraper/`: `node --check
test/aws-pipeline-infrastructure.test.js`; an exact-source script must require
each new complete line once, each superseded complete line zero times, reverse
only the four replacements in memory and reproduce starting digest
`3bfa45fab2beb2613be395e2a903fa87cdfef2a3b8c558073483acd504da13f8`;
`node --test test/aws-pipeline-infrastructure.test.js` must exit zero with zero
fail/skip; `git diff --check`; and the file diff must be exactly four additions
and four deletions. These are compatibility-count corrections only and create
no new W7 case/control ID.

### `KI-W7-I004` - corrected final reassessment and handoff

```yaml
subwindow_id: KI-W7-I004
type: INTEGRATION_REASSESSMENT
parent_window_id: KI-W7
parent_assignment_id: ASG-KI-W7-WA-03
assigned_agent: KI-W7-WINDOW-AGENT
predecessors: [KI-W7-C003]
authorized_write_file: NONE
authorized_read_scope: [A1-A8, KI-W7 S1-S3, all fourteen final W7 paths, email_scraper/scripts/build-lambda.js, email_scraper/scripts/measure-lambda-packages.js, email_scraper/scripts/build-keyword-worker.js, email_scraper/scripts/measure-keyword-worker-package.js, gitignored dist/lambda build outputs]
authorized_actions: [repeat CV1-CV4 once with corrected CV3 order, execute CV5 once, execute CV6 once, execute CV7 once, append final W7 evidence and CAS handoff only after every gate passes]
prohibited_actions: [implementation edit, changed test filter or timeout, database browser real network provider AWS paid action, credential value read, package schema migration frontend edit, commit push KI-W8]
may_start_successor: false
```

I004 supersedes only I003's failed assessment schedule. Run CV1-CV7 in the
unchanged Sections 7.3-7.5 order, with these exact corrections:

1. CV1 expects the original thirteen W7 paths plus
   `email_scraper/test/aws-pipeline-infrastructure.test.js`; the exact fourteen-
   path digest is
   `dd30a08f7f9bfa66d224c2b8f72758557d0823bf392e1f59c7a4ca2f26640836`.
2. In CV3, immediately after the sole `node scripts/build-lambda.js`, run the
   existing `node scripts/measure-lambda-packages.js` exactly once. Require exit
   zero and `dist/lambda/measurements.json` before recording the seven sibling
   hashes/snapshot or running the first keyword build. The rest of CV3,
   including two keyword builds, two keyword measurements and bridge emission,
   remains byte-for-byte the frozen sequence.
3. CV4 must again certify exactly 12 cases and 12 controls with the frozen
   digests and no exception. CV5 is one fresh `npm test`; CV6 is one fresh
   `npm run check:secrets`; CV7 recomputes the expanded fourteen-path set and
   all original topology/privacy/prohibition oracles.

Only a proven sandbox denial permits the one identical E8.1 recovery already
frozen by A5. A passing I004 returns `READY_FOR_PARENT_REVIEW`, records the exact
commands/results and final file/case/control digests, and confirms zero external
action and `$0.00` cost. It must not begin KI-W8. Any genuinely new failing
oracle is diagnosed and handled under the existing mechanically-governed
one-file correction rule; an out-of-scope decision returns one exact blocker.
