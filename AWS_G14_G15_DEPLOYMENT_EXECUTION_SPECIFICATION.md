# AWS G14/G15 Deployment Execution Specification

Status: **G14 ACCEPTED; G15 CURRENT-QUOTA ACTIVATION AUTHORIZED**

Created: 14 August 2026

This is the decision-complete deployment packet authorized after G-R10. It
supplements, but does not rewrite, the frozen architecture and implementation
plan. Progress belongs only in `ACTIVE_EXECUTION_STATE.md`; evidence belongs
only in `AWS_PIPELINE_EXECUTION_EVIDENCE.md`.

## 1. Authority and fixed inputs

The following are immutable inputs to this packet:

- `AWS_ASYNC_DEPLOYMENT_DIRECTION.md`, SHA-256
  `747cd5b398f3edd6d8c146187260f05c475abec006712d04a0df5301cd7c601f`;
- `FINAL_LAMBDA_SQS_S3_MIGRATION_EXECUTION_PLAN.md`, SHA-256
  `6fbbdaee89d20ceb6a9b369af43b79c0dfb17c36217d5dc33accd04e6caefdfe`;
- the accepted G-R9 evidence and accepted G-R10 correction in
  `AWS_PIPELINE_EXECUTION_EVIDENCE.md`;
- the seven deterministic Node 24 ZIPs emitted by
  `email_scraper/scripts/build-lambda.js`; and
- the v1 SQS/S3 contracts and strict secret schema already implemented under
  `email_scraper/src/aws-pipeline/`.

The architecture remains Neon + S3 + Standard SQS + bounded Lambda. G14 does
not enable dispatch. G15 does not redesign application behavior.

## 2. Discovery dossier and decisions

### 2.1 Observed deployment facts

- Runtime: `nodejs24.x`, x86-64, Amazon Linux 2023.
- Maximum measured package RSS: `104701952` bytes (traffic worker).
- Every ZIP is approximately 32 MB and therefore must be uploaded to S3 before
  CloudFormation can create Lambda resources from it.
- All handlers load the same strict Secrets Manager object because
  `createPipelineRuntime()` constructs Neon coordination for every handler.
- The existing HTTP backend performs confirmed-query validation, immutable
  query-manifest writes, and the first discovery/check dispatch. It therefore
  needs a separately scoped production AWS identity at G15 cutover.
- No SAM CLI is installed locally at packet creation. Installing it is a local
  tool prerequisite, not an AWS mutation.
- The configured `storesignal-dev` profile currently points at the learning
  account/resources. Its exact account identity and applicable quotas must be
  inspected read-only before an AWS mutation is proposed.

### 2.2 Locked deployment identity

| Field | Exact value |
|---|---|
| AWS CLI profile | `storesignal-dev` |
| Region | `ap-south-2` |
| Environment parameter | `production` |
| Stack | `storesignal-production-pipeline` |
| Artifact bucket | `storesignal-prod-pipeline-${AWS::AccountId}-${AWS::Region}` |
| Empty secret name | `/storesignal/production/aws-pipeline` |
| Deployment prefix | `deployment/<zip-sha256>/<handler>.zip` |
| Full-template object | `deployment/<template-sha256>/cloudformation-template.json` |
| Runtime artifact prefix | `runs/` |

The profile remains provisional until read-only STS proves the intended
account. Any different profile, Region, environment, stack, bucket formula, or
secret name requires a new append-only correction before mutation.

### 2.3 Two-phase materialization

CloudFormation cannot create the full Lambda change set from local 32 MB ZIPs.
G14 therefore uses this exact sequence:

1. validate a bootstrap template containing only the final retained S3 bucket
   and its bucket policy;
2. after exact user approval, create and execute the bootstrap CREATE change
   set for `storesignal-production-pipeline`;
3. upload the seven measured ZIPs and the 88,178-byte full template with
   `AES256`, SHA-256 checksums, and content-addressed keys under `deployment/`;
   record all returned object version IDs in an untracked deployment manifest;
4. validate the full template through its version-specific S3 URL, then create
   the full stack UPDATE change set from that URL using bucket, key, and version
   parameters for all seven functions; the S3 path is mandatory because the
   full template exceeds CloudFormation's 51,200-byte inline-body limit;
5. show and compare the actual CloudFormation change-set inventory to the
   locally approved inventory; refuse execute on any mismatch;
6. execute the full change set; and
7. inspect the deployed stack and prove all six SQS mappings and the recovery
   rule are disabled and all queues are empty.

The bootstrap bucket is the final production artifact bucket. The learning
bucket is never read or written. Failed full-stack materialization leaves only
the retained private bucket and immutable deployment ZIPs/template; no queue
trigger or schedule exists at that point.

### 2.4 Function, queue, and mapping ledger

All functions use 512 MB memory, 512 MB ephemeral storage, x86-64, Node 24,
active tracing disabled, and 30-day explicitly created log groups.

| Function | Source | Sends | Timeout | G14 deployed reserved | Required before enablement | Batch / window | Mapping maximum | Visibility |
|---|---|---|---:|---:|---:|---:|---:|---:|
| DiscoveryWorker | Discovery | DiscoveryCheck | 300 s | omitted | 1 | 1 / 0 s | omitted | 1800 s |
| DomainAggregator | DiscoveryCheck | Lead, LeadCheck | 300 s | omitted | 2 | 1 / 0 s | 2 | 1800 s |
| LeadWorker | Lead | LeadCheck | 90 s | omitted | 2 | 1 / 0 s | 2 | 540 s |
| LeadAggregator | LeadCheck | Traffic, TrafficCheck | 300 s | omitted | 2 | 1 / 0 s | 2 | 1800 s |
| TrafficWorker | Traffic | TrafficCheck | 900 s | omitted | 1 | 1000 / 10 s | omitted | 5410 s |
| FinalAggregator | TrafficCheck | none | 300 s | omitted | 2 | 1 / 0 s | 2 | 1800 s |
| Recovery | disabled 5-minute rule | all six queues | 300 s | omitted | 1 | n/a | n/a | n/a |

The 512 MB choice is the locked minimum after rounding twice the maximum
measured RSS upward in 128 MB units. Lead preserves the Browserless 45-second
session ceiling. Traffic receives a batch of reference messages but one
Neon-fenced stage-wide owner retains run-wide DataForSEO and BigQuery batches.
Every mapping declares `ReportBatchItemFailures`. G14 deployed them disabled;
the authorized G15 activation changes all six to enabled and enables recovery.
`MaximumConcurrency: 1` is forbidden. G14 deliberately omitted all seven
reserved-concurrency properties because the account then had a regional
concurrency quota of 10. AWS subsequently applied quota request
`ce33c0c396a04b7a8a2dbc11ed2004ecFAEyUfSM` at 1,000 concurrent executions.
G-R12 therefore ends that temporary bridge and restores the exact steady-state
function reservations `1/2/2/2/1/2/1` in the same guarded update as its
corrected Lambda code. The lead mapping maximum remains two; discovery and
traffic mappings continue to omit `MaximumConcurrency` because their function
reservations enforce one invocation.

Every source queue is Standard, SQS-managed encrypted, retained four days,
uses the table visibility value, and redrives after five receives to its
dedicated SQS-managed encrypted 14-day DLQ. No queue is purged by any script.

### 2.5 Non-secret environment ledger

Every Lambda receives exactly these configured non-secret values:

```text
RUN_EXECUTION_BACKEND=aws
AWS_PIPELINE_ENABLED=true
AWS_PIPELINE_BUCKET=<stack bucket>
AWS_PIPELINE_DISCOVERY_QUEUE_URL=<Discovery URL>
AWS_PIPELINE_DOMAIN_AGGREGATION_QUEUE_URL=<DiscoveryCheck URL>
AWS_PIPELINE_LEAD_QUEUE_URL=<Lead URL>
AWS_PIPELINE_LEAD_AGGREGATION_QUEUE_URL=<LeadCheck URL>
AWS_PIPELINE_TRAFFIC_QUEUE_URL=<Traffic URL>
AWS_PIPELINE_FINAL_AGGREGATION_QUEUE_URL=<TrafficCheck URL>
AWS_PIPELINE_SECRET_ID=<empty production secret ARN>
AWS_PIPELINE_TASK_LEASE_MS=60000
AWS_PIPELINE_AGGREGATOR_LEASE_MS=120000
AWS_PIPELINE_RECOVERY_AGE_MS=300000
AWS_PIPELINE_MAX_ARTIFACT_BYTES=5000000
```

Lambda supplies the reserved `AWS_REGION=ap-south-2` runtime variable. The
template must not attempt to configure that reserved key.

G14 creates an empty Secrets Manager secret: neither `SecretString` nor
`GenerateSecretString` appears in IaC. G15 alone may install its strict value.
No credential or secret value may occur in a template, parameter, change set,
output, environment variable, deployment manifest, log, or evidence record.

### 2.6 IAM ledger

Every Lambda role receives only log stream/write permission for its own log
group, `secretsmanager:GetSecretValue` for the one production secret, and the
following role-specific permissions:

| Role | SQS consume | SQS send | S3 access |
|---|---|---|---|
| DiscoveryWorker | Discovery | DiscoveryCheck | get/put `runs/*/queries/*` |
| DomainAggregator | DiscoveryCheck | Lead, LeadCheck | get `runs/*/queries/*`; get/put manifest and `runs/*/domains/*` |
| LeadWorker | Lead | LeadCheck | get manifest/candidates; get/put lead and lead-attempt objects under `runs/*/domains/*` |
| LeadAggregator | LeadCheck | Traffic, TrafficCheck | get manifest and `runs/*/domains/*` |
| TrafficWorker | Traffic | TrafficCheck | get manifest/domain objects; get/put `runs/*/domains/*` and `runs/*/traffic-batches/*` |
| FinalAggregator | TrafficCheck | none | get manifest, domain, traffic, and batch evidence |
| Recovery | none | all six source/check queues | none |

Consume means `sqs:ReceiveMessage`, `sqs:DeleteMessage`,
`sqs:ChangeMessageVisibility`, and `sqs:GetQueueAttributes` on the exact source
queue ARN. Send means `sqs:SendMessage` on exact destination ARNs. S3 means only
`s3:GetObject` and/or `s3:PutObject` on named `runs/*` patterns. There is no
`s3:ListBucket`, object delete, queue purge, `sqs:*`, `s3:*`, or resource `*`
for data-plane actions.

The stack also creates one unattached least-privilege managed policy for the
existing control plane: GetSecretValue on the production secret; get/put only
`runs/*/queries/*`; and send only to Discovery and DiscoveryCheck. G15 may
attach or translate it only after the backend hosting identity is explicitly
selected. G14 creates no IAM user, access key, trust relationship, or
credential.

### 2.7 Storage, retention, and encryption

The bucket has versioning, BucketOwnerEnforced ownership, all public-access
blocks, default `AES256`, retained deletion/update policies, TLS-only access,
and an explicit denial of `PutObject` without `AES256`. Its only lifecycle
action aborts incomplete multipart uploads after seven days. It never expires
completed `deployment/` or `runs/` objects.

### 2.8 Alarms and recurring-cost estimate

The full stack creates 27 standard one-metric alarms:

- six DLQ visible-message alarms;
- six source-queue oldest-message alarms;
- error and throttle alarms for each of seven Lambdas; and
- one EventBridge recovery-rule failed-invocation alarm.

They have no alarm action because no notification endpoint has been approved.
They remain inspectable in CloudWatch; adding SNS/email/PagerDuty is a separate
decision.

Disabled idle-stack estimate, before credits and regional variance:

| Item | Estimate/month |
|---|---:|
| 27 standard CloudWatch alarms at the public $0.10 example rate | $2.70 |
| One Secrets Manager secret | $0.40 |
| About 0.23 GB of versioned deployment ZIPs in S3 | less than $0.01 |
| Queues, disabled mappings/rule, Lambda, IAM, CloudFormation, empty logs | $0.00 fixed |
| **Estimated disabled total** | **about $3.11/month** |

This is a planning estimate, not an AWS quote. Runtime requests, log ingestion,
artifact storage, secret reads, Lambda duration, and provider costs are usage
based. SQS includes one million requests monthly under AWS's published free
tier, subject to the account's plan and eligibility.

## 3. Four-artifact package and state machine

The executable package is:

1. product contract: `AWS_ASYNC_DEPLOYMENT_DIRECTION.md`;
2. execution specification: this file;
3. live state: `ACTIVE_EXECUTION_STATE.md`; and
4. evidence log: `AWS_PIPELINE_EXECUTION_EVIDENCE.md`.

Only the live state may authorize a window. The frozen plan and this packet do
not record progress.

Exact G14 states are:

```text
G14_LOCAL -> G14_AWAITING_EXACT_MUTATION_APPROVAL
G14_AWAITING_EXACT_MUTATION_APPROVAL -> G14_BOOTSTRAP
G14_BOOTSTRAP -> G14_FULL_CHANGE_SET_REVIEW
G14_FULL_CHANGE_SET_REVIEW -> G14_FULL_EXECUTE
G14_FULL_EXECUTE -> G14_COMPLETE_DISABLED
```

Any failed validation stays in the current state. Any actual inventory drift,
wrong account/Region, missing permission, quota violation, or unapproved
replacement/deletion stops and escalates.

## 4. G14 — disabled production infrastructure

### G14 authority

The user's 14 August instruction authorizes the current-quota G14 template
change and deployment of the exact disabled packet. The generated approval
token is bound into live state before mutation. It authorizes no secret value,
provider call, event-source enablement, recovery-rule enablement, or cutover.

### G14 ownership

G14 may create or edit only:

- `email_scraper/infrastructure/aws/bootstrap-template.yaml`;
- `email_scraper/infrastructure/aws/template.yaml`;
- `email_scraper/infrastructure/aws/samconfig.toml`;
- `email_scraper/scripts/aws-pipeline/create-change-set.js`;
- `email_scraper/scripts/aws-pipeline/inspect-stack.js`;
- `email_scraper/test/aws-pipeline-infrastructure.test.js`;
- `email_scraper/package.json` only to add non-mutating test/validation scripts;
- this packet, live state, and evidence log.

It may not edit application behavior, Prisma, frontend, provider adapters,
contracts, existing migrations, production database data, or learning
resources.

### G14-T1 — local IaC

Implement the exact resources and settings in Section 2. Templates must use
parameters for the seven code keys and object versions and must never contain a
secret value. The bootstrap and full template must define byte-equivalent
bucket and bucket-policy resources.

Acceptance:

- templates parse and SAM/CloudFormation validation succeeds;
- policy tests reject public access, missing encryption/versioning/retention,
  a completed-object expiration, broad IAM, a secret value, an enabled event
  source/rule, a missing DLQ/partial-failure declaration, formula drift, an
  unscoped deployment/runtime S3 path, and mapping concurrency one;
- all resource and output logical IDs match the inventory emitted by the dry
  run; and
- full local backend, secret scan, package build, measurement, and diff hygiene
  pass.

### G14-T2 — guarded deployment and inspection scripts

`create-change-set.js` requires explicit `--profile`, `--region`, `--stack`,
`--environment`, and `--phase=bootstrap|package|full`. It defaults to dry-run.
`--execute` additionally requires a live-state approval token matching the
exact profile, account ID, Region, stack, template hashes, ZIP hashes, and
resource inventory hash. It refuses another account, Region, stack, enabled
source, template drift, ZIP drift, learning bucket, or secrets in arguments.

The script uses AWS CLI argument arrays without a shell and never prints
environment values. It creates named change sets, waits, describes them,
compares the normalized resource changes against the approved manifest, and
executes only after equality. The package phase performs only eight encrypted,
checksummed versioned `PutObject` operations—seven Lambda ZIPs and the full
CloudFormation template—and writes the sanitized returned keys/version IDs to
ignored `dist/aws-deployment/manifest.json`. The full change set uses the
recorded template version in `TemplateURL`; it never submits the oversized
template inline.

`inspect-stack.js` is read-only unless no mutation mode exists. It requires
`--expected-disabled`, checks every Section 2 setting, proves queue/DLQ counts
are zero, checks no Lambda invocation/log activity attributable to the new
stack, and prints no environment values or policy documents containing account
credentials.

### G14-T3 — read-only account preflight and user packet

Read-only preflight must prove:

- STS account and ARN for `storesignal-dev`;
- configured Region equals `ap-south-2`;
- no existing stack/bucket/secret/queue/function name collision;
- Lambda regional concurrent-execution quota is observed and recorded. For the
  current-quota G14 deployment it may remain 10 only because all reserved
  concurrency is omitted and all triggers are disabled. At least 111 remains a
  hard G15 prerequisite before restoring the 11 exact reservations;
- CloudFormation, IAM, Lambda, SQS, S3, Logs, Events, CloudWatch, and Secrets
  Manager permissions needed by the reviewed changes are available, using
  validation/change-set calls only where those calls do not mutate resources;
- learning resources are unchanged; and
- the exact bootstrap and full inventories, IAM summary, cost estimate,
  template hashes, ZIP hashes, and commands are ready for user review.

Before mutation, show the user:

1. exact account ID/ARN, profile, Region, and stack;
2. bootstrap resource list and mutation command;
3. exact eight S3 object writes: seven ZIPs and one full-template object;
4. full resource list/IAM summary and full change-set command;
5. disabled-state proof and estimated recurring cost; and
6. the rollback consequence: CloudFormation rollback may remove newly created
   non-retained resources, while the bucket and secret are retained and no
   script deletes them.

### G14-T4 — exact user gate and AWS mutation

No AWS mutation occurs until the user explicitly approves the complete packet
from G14-T3. Approval is bound into live state with the normalized inventory
hash and expires if any bound value changes. The authorized mutations are only:

- one bootstrap stack change-set create/execute;
- eight exact encrypted versioned object writes: seven ZIPs and the one
  full-template object;
- one full stack update change-set create/execute; and
- CloudFormation's creation of the approved disabled resources.

After execution, run the expected-disabled inspector and record safe evidence.
G14 is accepted only if actual resources equal Section 2, all queues/DLQs are
empty, mappings/rule are disabled, all functions have no reserved concurrency,
no function was dispatched, the secret has no current value, and learning
resources are unchanged. Stop before G15.

## 5. G15 — secret, bounded smoke, rollback, and cutover

G15 activation is assigned by the user's 14 August instruction to make the
deployed pipeline run. G14 is accepted. Remaining steady-state prerequisites
are:

- Lambda regional concurrency quota reaches at least 111 before the exact
  `1/2/2/2/1/2/1` steady-state reservations are applied;
- the production backend hosting environment and its AWS workload identity or
  approved credential-delivery mechanism;
- the operator-approved strict secret JSON source;
- one owner-controlled fixture of at most 52 domains;
- the BigQuery byte cap for that fixture; and
- the desired notification target, if alarms must notify rather than remain
  console-visible.

These are predictable gates, not reasons to halt G14.

### Separate G15 approvals

The user must separately approve:

1. installing/updating the named production secret;
2. direct-invoke paid/live provider smoke calls with stated ceilings;
3. enabling each named event-source mapping and the recovery rule; and
4. changing the production backend AWS identity/configuration and kill switch.

No one approval implies another.

### Fixed provider ceilings

The entire fixture may use at most ten DataForSEO tasks, 52 CrUX REST calls,
one BigQuery table-list, one dry run, one live query under the approved byte
cap, and two concurrent Browserless sessions. Both CrUX sources remain
independently present. Any unexplained Browserless unit or provider call stops
the smoke.

### G15 sequence

1. Implement guarded dry-run-first smoke, equivalence, and rollback scripts.
2. After secret approval, put one strict secret version and direct-invoke only
   with mappings and schedule disabled.
3. After paid-call approval, execute the bounded fixture and record provider,
   SQS, S3, Lambda, Neon, ownership, privacy, latency, and cost counters.
4. After mapping approval, enable one mapping at a time in pipeline order,
   verify it, then enable the next; enable recovery last.
5. Prove local/AWS lead, provenance, profile, grants, traffic, REST CrUX,
   BigQuery CrUX, score v3, API, CSV, and master-lead equivalence.
6. Rehearse rollback: kill switch false, new runs local, six mappings and
   recovery disabled, zero new AWS messages, one successful local fixture. Do
   not delete S3, Neon rows, queues, DLQs, secret, or stack.
7. Request the separate production cutover decision. Stop before independent
   final review.

Any application defect found by G15 opens a new append-only G-Rn. G15 never
patches application code or frontend code.

## 6. Mechanical trace and backward simulation

| Requirement | Mechanical implementation | Decisive proof |
|---|---|---|
| Private immutable artifacts | bucket policy/default encryption/versioning + conditional application puts | static policy tests + deployed bucket inspection |
| At-least-once bounded work | six Standard source queues with six DLQs | template assertions + queue attribute inspection |
| No premature execution | six mappings `Enabled:false`; rule `DISABLED`; empty secret | change-set scan + deployed state + zero queue/function activity |
| Provider batching | traffic reserved one, batch 1000/window 10, stage-wide Neon owner unchanged | template test + existing G-R9 matrix + G15 counters |
| Browserless ceiling | lead reserved/mapping maximum two | template/deployed concurrency inspection + G15 usage |
| Neon completion authority | no S3 events, Step Functions, DynamoDB, or queue-empty logic | negative template/source search |
| Least privilege | per-function exact SQS/S3/secret/log policies | normalized IAM action/resource test + deployed policy inspection |
| Privacy | empty secret in G14; no values in IaC/outputs/logs/evidence | secret scan + argument/output tests |
| Safe rollback | disabled sources first; no deletions in scripts; retained bucket/secret | script tests + G15 rehearsal |

Backward simulation:

1. final public visibility requires the final aggregator and fenced Neon
   transaction;
2. final aggregation requires terminal immutable traffic evidence;
3. traffic requires lead checkpoint and stage-wide provider batching;
4. lead requires the domain manifest and bounded per-domain work;
5. domain aggregation requires every registered discovery terminal;
6. discovery requires explicit confirmation and the control-plane manifest;
7. therefore disabled mappings/rule plus an empty secret make G14 incapable of
   advancing a production run, while preserving every resource needed for the
   separately approved G15 smoke.

## 7. Stop and escalate

Stop with one concise blocker if:

- STS identifies a different account than the user intends;
- any trigger is enabled before quota is at least 111 and the exact reserved
  concurrency values have been restored;
- an existing production name would be adopted, replaced, or deleted;
- bootstrap/full change-set inventory differs from the approved normalized
  inventory;
- a required permission cannot be validated;
- SAM/CloudFormation rejects a locked property;
- any mapping/rule is enabled, queue is nonempty, or Lambda executes during
  G14;
- the secret contains a value before the G15 secret gate;
- a template/script would log a secret or accept a wildcard data-plane policy;
  or
- completion requires any mutation not enumerated in G14-T4.

Ordinary fixable local syntax/test failures stay inside G14. A window boundary
is not a blocker.

## 8. Readiness certificate

```text
SPEC STATUS: G14 ACCEPTED; G15 CURRENT-QUOTA ACTIVATION AUTHORIZED
UNKNOWN IMPLEMENTATION DECISIONS IN G14: 0
PREDICTABLE USER GATE: exact G14 AWS mutation packet after read-only preflight
PREDICTABLE G15 PREREQUISITE: quota-backed steady-state reservations after AWS decision
PAID PROVIDER AUTHORIZATION: granted for live pipeline execution
AWS MUTATION AUTHORIZATION: granted for secret installation and exact activation update
FRONTEND AUTHORIZATION: none; frontend remains read-only
STOP AFTER G15 ACTIVATION: active pipeline independently inspected
```

## 9. G-R11 — persist the selected execution backend at run creation

Status: **ASSIGNED BY THE USER'S 14 AUGUST 2026 CORRECTION AUTHORIZATION**

Observed production evidence is decision-complete: run
`run_wkKmDLmvZpb3gfbPV_a_igJH` was created by an AWS-configured repository with
a valid `awsProviderConfig`, but `Run.executionBackend` remained Prisma's
default `local`. The confirmation invariant therefore rejected it before AWS
dispatch with `PIPELINE_INPUT_CONFLICT`.

G-R11 owns only `email_scraper/src/prisma-run-repository.js`, its focused unit
test, this specification, active state, and evidence. In `runCreateData()`, set
`executionBackend` mechanically to `aws` when the constructor produced an AWS
provider snapshot and to `local` otherwise. Preserve the existing snapshot,
identity, query-review, confirmation, coordinator, provider, artifact, and
visibility contracts. No schema, migration, Lambda package, infrastructure,
frontend, or provider change is permitted.

After focused and full verification, repair only the observed unconfirmed row
with a conditional single-row update from `local` to `aws`. The update must
require the exact run ID, `awaiting_query_confirmation` state, `query_review`
phase, `awaiting_query_confirmation` stage, generation one, revision one, no
confirmed revision/timestamp, and a non-null AWS provider snapshot. A result
other than exactly one row is a blocker. Do not alter its queries or submit it;
the owner retries the existing confirmation.

Acceptance requires focused assertions for both local and AWS creation data,
the full backend suite, secret scan, diff hygiene, a safe read-back of the
repaired coordinator fields, and evidence that the discovery source queue did
not receive work from the repair. The user's currently running Node process is
not restarted or terminated by G-R11; it may finish this repaired run, but must
be restarted before creating another run so future creation uses the corrected
module.

## 10. G-R12 — collation-independent coordinator task reconciliation

Status: **ASSIGNED BY THE USER'S CONTINUING 14 AUGUST 2026 CORRECTION REQUEST**

The first live AWS run supplied the missing decisive evidence. Its strict query
manifest was written to S3, but Neon discovery registration rolled back before
queue dispatch. A forced-rollback reproduction proved that JavaScript
`localeCompare()` and PostgreSQL `ORDER BY itemKey` position the same mixed-case
base64url query IDs differently. `registerStageInTransaction()` incorrectly
compared those equal sets by array position and raised
`PIPELINE_INPUT_CONFLICT`.

G-R12 owns only the coordinator registration comparison, its unit and real-
PostgreSQL regression tests, the seven Lambda code references, the seven exact
reserved-concurrency properties, deployment/inspection guards, this
specification, active state, and evidence.
Replace positional reconciliation with an exact cardinality-and-itemKey map
comparison; every stored task must have exactly the expected fingerprint. Do
not change task identity, dispatch ordering, schemas, transactions, leases,
messages, artifacts, providers, infrastructure, or frontend behavior.

Because the coordinator module is bundled into the deployed workers, rebuild
and measure all seven deterministic packages. After showing the exact mutation
packet, the user must approve eight encrypted/versioned S3 writes (seven ZIPs
and the versioned template) and a guarded CloudFormation change set whose only
direct resource changes are the seven Lambda `Code` references plus these exact
`ReservedConcurrentExecutions` values: DiscoveryWorker 1, DomainAggregator 2,
LeadWorker 2, LeadAggregator 2, TrafficWorker 1, FinalAggregator 2, and Recovery
1. CloudFormation may additionally report exactly two dependency-only
reevaluations caused by the Recovery code reference: `RecoverySchedule.Targets`
from `Recovery.Arn` with no recreation, and
`RecoveryInvokePermission.SourceArn` from `RecoverySchedule.Arn` with its
conditional permission replacement. The schedule state, expression, target
identity, and recovery behavior must remain unchanged. No mapping, queue, IAM,
environment, schedule state/expression, secret, or other resource property may
change. Independently inspect the active stack after execution and require
those exact reservations.

After focused, real-PostgreSQL, full-suite, secret, and diff checks pass, stop
the currently running pre-correction local server before repairing the failed
run. Reconcile its existing immutable manifest by exact validated read. Then
conditionally restore only run `run_wkKmDLmvZpb3gfbPV_a_igJH` from its exact
failed/unpublished AWS state to `queued`/`scraping`/
`queued_query_validation`, preserving generation, confirmed revision,
`queriesConfirmedAt`, queries, provider snapshot, and artifact. Clear only the
failure and expired lease fields. The discovery stage/task tables and source
queue must still be empty before repair. A result other than one updated row is
a blocker. Do not start the server or submit provider work; the owner starts the
corrected server, which resumes the already-confirmed run and immutably
reconciles the existing manifest.

## 11. G-R13 — Amazon Linux Prisma engine correction

Status: **AUTHORIZED BY THE USER'S 14 AUGUST 2026 “DO FIRST 3” INSTRUCTION**

The first new live run proved the control-plane correction: it created one
discovery stage with ten registered tasks and delivered all ten SQS records.
Every Discovery invocation then failed before handler execution because the ZIP
contained `libquery_engine-debian-openssl-3.0.x.so.node`, while Lambda Node 24
on Amazon Linux 2023 selected `rhel-openssl-3.0.x`. No task was claimed and no
provider call occurred.

G-R13 owns only `prisma/schema.prisma`, Lambda build/measurement and packaging
tests, the guarded engine deployment phase, all seven Lambda code references,
the exact Discovery mapping containment/re-enable operation, this
specification, active state, and evidence. It must not alter schemas, migrations,
application logic, reservations, mapping batch/scaling settings, queues, IAM,
environment, secret, schedule state/expression, providers, frontend, or data.

The mechanical correction is:

1. disable only Discovery mapping UUID
   `20d9cdde-97f9-4f31-9116-da9870bc6122` while retaining every message;
2. configure Prisma binary targets exactly as `native` plus
   `rhel-openssl-3.0.x`;
3. package exactly one Prisma native engine per Lambda ZIP:
   `libquery_engine-rhel-openssl-3.0.x.so.node`, with no Debian engine;
4. regenerate Prisma, validate the schema, rebuild/measure all seven ZIPs, and
   require packaging tests to assert both the generator target and ZIP engine;
5. publish the seven content-addressed AES256 versioned ZIPs, reconcile the
   unchanged versioned template, and create an `engine` CloudFormation change
   set;
6. accept exactly seven in-place Lambda `Code` changes plus only
   `RecoverySchedule.Targets` from `Recovery.Arn` and the conditional
   `RecoveryInvokePermission.SourceArn` replacement from
   `RecoverySchedule.Arn`; reject concurrency or any other property/resource;
7. execute to `UPDATE_COMPLETE`, inspect all seven function code references and
   exact existing reservations, then re-enable only the same Discovery mapping;
   and
8. stop after confirming the mapping state is `Enabled`. Do not purge, redrive,
   change visibility, fabricate work, or perform the separate end-to-end
   advancement verification excluded by the user's “first 3” boundary.

## 12. G-R14 — scoped S3 optional-artifact existence correction

Status: **AUTHORIZED BY THE USER'S 14 AUGUST 2026 “CAN YOU DO IT?” INSTRUCTION**

Post-G-R13 live evidence is decision-complete. The corrected Discovery Lambda
now initializes successfully, but the run remains at discovery with ten
`processing` tasks, zero terminal tasks, and no per-query artifacts. Recovery
has dispatched each task three times, producing 30 in-flight source records and
zero DLQ records. The deployed Discovery role is allowed `s3:GetObject` and
`s3:PutObject` for its query artifacts but is implicitly denied
`s3:ListBucket`. For an absent object, S3 consequently returns 403 rather than
the modeled `NoSuchKey`; every task fails immediately after its Neon claim at
`getOptionalValidated()` and before HTTP discovery or S3 write.

G-R14 owns only `src/aws-pipeline/adapters/artifact-store.js`, its focused
adapter test, the exact four scoped ListBucket policy statements and their
infrastructure tests, the guarded `artifact-access` deployment phase, all seven
Lambda code references required by the shared bundle, this specification,
active state, and evidence. It must not change artifact keys or schemas,
provider behavior/economics, coordinator state, queue properties, concurrency,
mappings, schedules, secrets, other IAM actions/resources, frontend, database
rows, or existing objects/messages.

The mechanical correction is:

1. `getOptionalValidated()` must issue `ListObjectsV2` with the exact requested
   key as `Prefix` and `MaxKeys:1`; only an exact returned key is present. Empty
   or non-exact contents are missing. A list error remains
   `PIPELINE_ARTIFACT_INVALID`; it is never treated as missing. A present key is
   then read and validated by the unchanged strict `GetObject` path. A
   `NoSuchKey` race after listing remains missing.
2. Grant bucket-level `s3:ListBucket` only with `StringLike` `s3:prefix`
   conditions matching each caller's existing object-read scope:
   DiscoveryWorkerRole `runs/*/queries/*`; LeadWorkerRole
   `runs/*/domains/*`; TrafficWorkerRole `runs/*/domains/*` and
   `runs/*/traffic-batches/*`; unattached ControlPlanePolicy
   `runs/*/queries/*` and `runs/*/query-probes/*`. No other role receives
   ListBucket, and no statement uses a wildcard resource.
3. Focused tests must prove exact list inputs, exact-key present/missing
   behavior, list denial rejection, strict subsequent validation, exact policy
   resources/prefixes, and rejection when a prefix condition is removed.
4. Regenerate no schema and apply no migration. Rebuild and measure all seven
   deterministic Node 24 packages because the adapter is shared. Each ZIP must
   retain exactly the RHEL Prisma engine.
5. Publish the seven content-addressed AES256 versioned ZIPs and the versioned
   template, then create an `artifact-access` change set. Accept only seven
   in-place Lambda `Code` changes, `ControlPlanePolicy.PolicyDocument`, the
   inline `Policies` of DiscoveryWorkerRole, LeadWorkerRole, and
   TrafficWorkerRole, the dependent `Role`-ARN reevaluation on exactly
   DiscoveryWorker, LeadWorker, and TrafficWorker, plus the two known Recovery
   code-reference dependency reevaluations. Reject every other
   resource/property.
6. Execute to `UPDATE_COMPLETE`; verify all seven functions are Active with
   successful updates and reservations `1/2/2/2/1/2/1`. IAM simulation must
   allow the exact four prefix sets and deny an unrelated deployment prefix.
7. Do not purge, receive, redrive, delete, or change visibility for any message.
   Leave the enabled mapping and five-minute Recovery rule in place. Observe
   recovery re-dispatch against Neon and require the existing run to produce
   per-query artifacts and terminal discovery evidence, then advance beyond
   discovery. Existing duplicate records must reconcile as terminal replays.
8. Append decisive evidence and stop if any new failure changes architecture,
   authorization, privacy, provider economics, or another ownership boundary.

## 13. G-R15 — verified-host provider identity fallback

Status: **AUTHORIZED BY THE USER'S 14 AUGUST 2026 REQUEST TO MAKE THE STALLED RUN PROGRESS**

G-R14 succeeded: every one of the ten discovery tasks became a validated
`succeeded` terminal and all ten immutable query artifacts exist. The first
real Domain Aggregator input then exposed a separate deterministic defect. Of
78 merged stable shops, `rbxactive.myshopify.com` has a verified stable and
resolved hostname but no canonical URL. The domain aggregator and reuse reader
called `new URL(identity.canonicalUrl)` unconditionally, so the complete
discovery stage was claimed repeatedly and failed before any domain candidate
or manifest was written. The Run consequently remained visibly at
`aws_discovery`; the frontend was accurately reflecting Neon.

G-R15 owns only the shared stable-identity provider-key helper,
`src/aws-pipeline/services/domain-aggregator.js`, the matching reuse lookup and
combined-manifest validation paths, their focused tests, the guarded
`provider-identity` code-only deployment phase, the seven Lambda code
references required by the shared bundle, this specification, active state,
and evidence. It must not change stable shop identity, schemas, migrations,
artifact/message shapes or keys, cache policy, provider batching/economics,
queues, IAM, concurrency, mappings, schedules, secrets, frontend code, or
existing durable rows/objects.

The mechanical correction is:

1. Add `trafficProviderIdentities(identity)`. It must first parse the existing
   strict stable identity. Its DataForSEO hostname is exactly
   `resolvedDomain || stableKey`. Its CrUX origin is the origin of
   `canonicalUrl` only when that URL is HTTPS; otherwise it is exactly
   `https://${resolvedDomain || stableKey}`. Both fallbacks therefore use an
   already verified lower-case ASCII hostname and never invent a second shop
   identity.
2. Domain plan creation, the three fenced reuse reads, and strict
   `domain-stage-manifest-v1` source-key reconciliation must all call that one
   helper. No consumer may retain an independent canonical-URL-only formula.
3. Focused tests must prove canonical URL behavior, missing-canonical fallback
   to resolved hostname, missing-resolved fallback to stable key, exact
   DataForSEO/CrUX source keys, and strict combined-manifest parsing. Replay the
   78-domain live discovery payloads read-only and require every provider key
   to derive without an exception.
4. Apply no migration and make no infrastructure-policy change. Rebuild and
   measure all seven deterministic Node 24 packages because the shared
   repository/contracts are bundled. Every ZIP must retain exactly the RHEL
   Prisma engine. Run focused tests, the full backend corpus, secret scan, and
   diff hygiene.
5. Publish only the seven content-addressed AES256 versioned ZIPs and reconcile
   the unchanged versioned template. The `provider-identity` change-set guard
   accepts exactly seven in-place Lambda `Code` modifications plus only the
   known `RecoverySchedule.Targets` and conditional
   `RecoveryInvokePermission.SourceArn` dependency reevaluations. It rejects
   every IAM, concurrency, mapping, queue, environment, secret, schedule-state,
   or other resource/property change.
6. Execute to `UPDATE_COMPLETE`; verify all seven functions are Active with
   successful updates, their code checksums match the approved artifacts, and
   reservations remain `1/2/2/2/1/2/1`.
7. Do not repair, purge, receive, redrive, delete, or change visibility for any
   live message or coordinator row. Let the enabled mapping and Recovery rule
   reclaim the expired discovery aggregation lease. Acceptance requires the
   same Run to leave `aws_discovery`, create its strict domain manifest and
   domain checkpoint, and register the lead stage. Later lead/traffic work may
   proceed normally under the user's existing live-pipeline/provider
   authorization; it is observation evidence, not permission to alter another
   contract.

## 14. G-R16 — frontend AWS-stage presentation

Status: **AUTHORIZED BY THE USER'S 14 AUGUST 2026 CLARIFICATION THAT THE MISSING PROGRESS IS IN THE FRONTEND**

G-R15 advanced the durable Run to `aws_lead`, but the polling frontend still
renders the generic `Processing your run` fallback and an 8% bar. The API
already returns the current stage every three seconds; its parser intentionally
accepts stage text. The presentation table and traffic-state helper simply do
not recognize the three AWS execution-stage names.

G-R16 owns only `frontend/lib/stages.ts`,
`frontend/lib/run-presentation.ts`, their focused presentation tests, this
specification, active state, and evidence. It must not change API polling,
backend serialization or progress rows, AWS resources, pipeline execution,
results visibility, frontend data contracts, components, styling, or provider
behavior.

The mechanical correction is:

1. Treat `aws_discovery` as the presentation alias of `discovering_stores`,
   `aws_lead` as `discovering_leads`, and `aws_traffic_crux` as
   `enriching_traffic` for both label and percentage. Retain the existing human
   labels and progress order; unknown stages must still use the generic label
   and 8% fallback.
2. `trafficProgressState()` must report `Analyzing/active` for both
   `enriching_traffic` and `aws_traffic_crux`. Its stopped and completed rules
   remain unchanged.
3. Focused tests must prove every alias label, its exact legacy-equivalent
   percentage, AWS traffic state, and unchanged unknown fallback. Run the full
   authorized frontend `npm run check` verification.
4. No AWS, provider, database, backend, deployment, or live-data mutation is
   permitted. A running development frontend may hot reload; a production
   frontend process requires an ordinary rebuild/restart by its operator.

## 15. G-R17 — same-task durable lead-work recovery

Status: **AUTHORIZED BY THE USER'S 14 AUGUST 2026 REQUEST TO MAKE THE STALLED LIVE RUN PROGRESS**

After G-R15, 77 of 78 lead tasks became terminal. The remaining task was
reclaimed six times but `ShopWork` stayed `processing`. Read-only Neon evidence
proved `ShopWork.processingPipelineTaskId` already equals that same durable
`PipelineTask.id`. `claimAwsLeadWork()` validates the caller's current fenced
task token, then incorrectly treats any processing task ID—including the
caller's identical ID—as a competing active owner and returns `busy` forever.

G-R17 owns only the same-task branch of
`PrismaRunRepository.claimAwsLeadWork()`, its isolated PostgreSQL regression,
the guarded `lead-work-resume` code-only deployment phase, all seven shared
Lambda code references, this specification, active state, and evidence. It must
not change ShopWork/PipelineTask identity, schema, migrations, leases, attempt
markers, provider calls/economics, artifacts/messages, queues, IAM,
concurrency, mappings, schedules, secrets, frontend, or existing rows.

The mechanical correction is:

1. Keep the existing current-task token, item, stage, run, generation, state,
   and Run-state validation at the start of `claimAwsLeadWork()` unchanged.
2. After completed/ambiguous/failed terminal handling, when a processing
   `ShopWork.processingPipelineTaskId` exactly equals the validated caller's
   `taskId`, return `{outcome:"owned"}`. The current token validation proves
   this invocation owns the latest attempt of that durable task. An invocation
   with an older token fails before this branch.
3. A different live task owner remains `busy`; a non-live different owner still
   follows the existing conditional replacement. Do not clear or rewrite
   attempt markers. The resumed lead worker must therefore reconcile any
   existing Browserless/AI marker and must not repeat an uncertain paid call.
4. The isolated PostgreSQL test must prove initial ownership, idempotent
   same-task resume, stale-token rejection, and a different live task remaining
   busy. Run focused tests, the isolated migration-backed case, the full backend
   corpus, package build/measurement, secret scan, and diff hygiene.
5. After AWS SSO is valid, publish only the seven content-addressed encrypted
   and versioned ZIPs and reconcile the unchanged template. The
   `lead-work-resume` change-set guard accepts exactly seven Lambda Code changes
   plus only the two known Recovery dependency reevaluations and rejects every
   other resource/property.
6. Execute to `UPDATE_COMPLETE`, verify all functions/checksums/reservations,
   and let Recovery resume the existing task without queue/Neon repair.
   Acceptance requires lead 78/78 terminal and advancement to
   `aws_traffic_crux` or a later terminal Run state.

## 16. G-R18 — lead-worker live memory correction

Status: **AUTHORIZED BY THE USER'S 14 AUGUST 2026 “DO IT” INSTRUCTION**

G-R17's ownership correction deployed successfully and changed the formerly
self-blocked task from repeated `busy` outcomes into real lead execution. The
first three post-correction invocations were then terminated by Lambda with
`Runtime.OutOfMemory`; each reported the configured 512 MB fully consumed. The
task has no Browserless attempt marker or lead result artifact, locating the
failure before paid Browserless dispatch. The other six functions have no
observed memory failure and retain their existing settings.

G-R18 owns only `LeadWorker.Properties.MemorySize`, the corresponding
infrastructure and deployed-stack expectations, a guarded `lead-memory`
deployment phase, this specification, active state, and evidence. It must not
change Lambda code, ZIP bytes or keys, any other function's memory, reserved or
event-source concurrency, timeouts, ephemeral storage, queues, IAM, mappings,
schedules, secrets, provider behavior/economics, frontend, database rows, or
existing messages/artifacts.

The mechanical correction is:

1. Set exactly `LeadWorker.Properties.MemorySize` from 512 to 1024 MB. Keep its
   timeout at 90 seconds, ephemeral storage at 512 MB, and reserved concurrency
   at two. Every other function remains at 512 MB with its existing timeout and
   reservation.
2. Update the template test and active-stack inspector to require 1024 MB only
   for `LeadWorker` and 512 MB for all six other functions. Add a guarded
   `lead-memory` phase that is executable only while `current_window: G-R18` and
   whose change-set validator accepts exactly one non-replacing
   `AWS::Lambda::Function` modification for `LeadWorker`, with one static direct
   `MemorySize` detail requiring no recreation. Reject every additional change
   or detail.
3. Do not rebuild or alter Lambda ZIPs. Reconcile their already-approved
   content-addressed object versions, publish only the newly content-addressed
   encrypted/versioned CloudFormation template, and bind all exact versions to
   a new approval token and manifest. Run focused infrastructure/deployment
   tests, secret scan, and diff hygiene before AWS mutation.
4. Create the `lead-memory` change set and inspect it before execution. Execute
   only if it contains the single exact `LeadWorker` in-place memory change.
   Require `UPDATE_COMPLETE`, `Active`, `LastUpdateStatus=Successful`, 1024 MB,
   reserved concurrency two, unchanged code checksum, and a passing full
   72-resource active-stack inspection.
5. Do not repair Neon, receive/purge/redrive/delete/change visibility for SQS,
   or invoke the Lambda manually. Let the enabled mapping and five-minute
   Recovery schedule resume the same task. Existing provider authorization
   remains limited to the pipeline's normal execution path.
6. Acceptance requires the same run
   `run_KRnkR1jV7QInr2zXhHE-Hi9c` to reach lead 78/78 terminal without another
   memory termination and advance to `aws_traffic_crux` or a later terminal Run
   state. If 1024 MB is also exhausted, or any different live failure prevents
   that transition, stop with the exact new evidence; do not choose another
   memory size or alter provider behavior inside G-R18.

## 17. G-R19 — bounded invalid-mailto extraction correction

Status: **AUTHORIZED BY THE USER'S 14 AUGUST 2026 “YOU ARE AUTHORIZED” INSTRUCTION**

G-R18 proved that increasing memory cannot correct the live failure: the first
1024 MB invocation also exhausted its allocation. A local reproduction using
the affected store's five actual public pages at the locked extraction
concurrency of two reached approximately 2,021,256 KB RSS and failed at
`contact-extractor.js:250`. An invalid `mailto:` normalizes to `""`;
`rawValueIndexes(html, "")` then repeatedly receives the unchanged `start`
from `indexOf("", start)` and grows its result array without bound. Page fetch
alone and single-page valid extraction remained bounded.

G-R19 owns only the empty-value guard in `rawValueIndexes()`, the invalid-email
guard in `associatedMailtoEvidence()`, focused extraction tests, restoration of
`LeadWorker.Properties.MemorySize` to 512 MB, corresponding template/inspector
expectations, the guarded `lead-bounded-extraction` deployment phase, all seven
shared Lambda code references, this specification, active state, and evidence.
It must not change valid email normalization/evidence, page ranking/fetching,
Browserless/AI behavior or markers, schemas, artifacts/messages, queues, IAM,
concurrency, timeouts, schedules, secrets, frontend, database rows, or existing
messages/artifacts.

The mechanical correction is:

1. In `rawValueIndexes(html, value)`, normalize the candidate value once and
   return `[]` immediately when it is empty; for nonempty values retain the
   existing left-to-right non-overlapping occurrence scan exactly.
2. In `associatedMailtoEvidence()`, after `normalizeEmail(href)`, skip the
   candidate immediately when the normalized email is empty. Valid mailto
   evidence continues through the unchanged association and confidence logic.
3. Focused tests must prove bare `mailto:`, query-only mailto, and invalid
   addresses return no email evidence and terminate; a valid associated mailto
   must still produce the same normalized value, method, confidence, and
   validation reason. Run the affected extraction/pipeline tests, full backend
   corpus, secret scan, and diff hygiene.
4. Reproduce the affected five-page, concurrency-two extraction locally with
   Browserless and paid providers disabled under a 512 MB V8 heap ceiling. It
   must complete successfully, preserve a valid evidence result, and report
   maximum RSS below 512 MB. Then restore only
   `LeadWorker.Properties.MemorySize` from 1024 to 512 MB; every Lambda is again
   512 MB, while the lead timeout remains 90 seconds, ephemeral storage 512 MB,
   and reserved concurrency two.
5. Rebuild and measure all seven deterministic Node 24 packages because the
   extractor is shared. Every ZIP must cold-import and contain exactly the RHEL
   Prisma engine. Publish only their content-addressed encrypted/versioned
   objects and the content-addressed template.
6. The `lead-bounded-extraction` change-set validator accepts exactly the seven
   non-replacing Lambda code modifications, the direct non-replacing
   `LeadWorker.MemorySize` change, and only the two known Recovery dependency
   reevaluations. For the six non-lead functions accept exactly the existing
   three code details; for `LeadWorker` require those three plus one static
   direct `MemorySize` detail requiring no recreation. Reject every other
   resource or detail.
7. Execute only the reviewed change set to `UPDATE_COMPLETE`. Require all seven
   functions Active with successful updates and matching approved checksums,
   exact memory/reservations, and a passing full 72-resource active-stack
   inspection.
8. Do not repair Neon or receive/purge/redrive/delete/change visibility for
   SQS. Let the enabled mapping and Recovery schedule resume the same durable
   task. Acceptance requires lead 78/78 terminal without another OOM and the
   same run to advance to `aws_traffic_crux` or a later terminal state. Stop on
   any different live failure that changes another ownership boundary.
