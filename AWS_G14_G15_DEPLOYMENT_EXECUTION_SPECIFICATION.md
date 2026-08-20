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
expectations, the guarded `lead-bounded-extraction` deployment phase, the
deterministically affected DiscoveryWorker and LeadWorker code references,
this specification, active state, and evidence.
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
5. Rebuild and measure all seven deterministic Node 24 packages. Every ZIP must
   cold-import and contain exactly the RHEL Prisma engine. Deterministic build
   evidence fixes the affected bundle set at `DiscoveryWorker` and
   `LeadWorker`; the other five ZIP hashes remain byte-identical. Publish only
   the two new content-addressed encrypted/versioned ZIPs and reconcile the
   five existing ZIP versions plus the existing content-addressed 512 MB
   template.
6. The `lead-bounded-extraction` change-set validator accepts exactly two
   non-replacing Lambda modifications: `DiscoveryWorker` with its existing
   three code details, and `LeadWorker` with those same three code details plus
   one static direct `MemorySize` detail requiring no recreation. No Recovery
   dependency reevaluation is expected because its package parameters and
   template resource are unchanged. Reject every other resource or detail.
7. Execute only the reviewed change set to `UPDATE_COMPLETE`. Require all seven
   functions Active with successful status and matching approved checksums,
   exact memory/reservations, and a passing full 72-resource active-stack
   inspection; only DiscoveryWorker and LeadWorker may have a new checksum.
8. Do not repair Neon or receive/purge/redrive/delete/change visibility for
   SQS. Let the enabled mapping and Recovery schedule resume the same durable
   task. Acceptance requires lead 78/78 terminal without another OOM and the
   same run to advance to `aws_traffic_crux` or a later terminal state. Stop on
   any different live failure that changes another ownership boundary.

## 18. G-R20 — bounded bulk pipeline execution correction

This section is an append-only correction specification. It contains no live
status; `ACTIVE_EXECUTION_STATE.md` alone authorizes and tracks execution.

### 18.1 Window header

ID: `G-R20`

Objective: remove the six observed unintended serial hot paths without
changing pipeline identity, provider economics, artifact/message contracts,
visibility, or the locked AWS architecture. The corrected implementation must
remain deterministic and recoverable at the 1,000-domain product bound.

Depends on: accepted `G-R19`; the current `traffic-enrichment-run-v1`,
`domain-stage-manifest-v1`, provider artifact protocols, PipelineTask fencing,
DataForSEO paid ledger, and final visibility transaction.

Consumes exact outputs:

- `PrismaRunRepository.claimAwsTrafficWorkBatch()` and
  `publishAwsFinalResults()` as they exist after G-R19;
- `finalizePersistedLeadScoresV3()`;
- `processTrafficBatch()`, `processDomainAggregation()`,
  `processLeadAggregation()`, and `processFinalAggregation()`;
- `SqsDispatcher.sendMany()`;
- `enrichDataForSeoSource()` and its durable repository callbacks; and
- the existing isolated-PostgreSQL harness, G-R9 recovery matrix, strict
  artifact parsers, and deterministic Lambda packaging toolchain.

Produces exact outputs:

- set-based traffic claims and final publication with no database operation in
  an item loop;
- one shared positional bounded-concurrency primitive;
- bounded and phase-ordered S3 reads/writes and task terminalization;
- one validated read per unique DataForSEO batch artifact;
- bounded parallel SQS `SendMessageBatch` calls;
- two-at-a-time DataForSEO scope execution while retaining bulk requests; and
- decisive maximum-size, concurrency, failure, replay, cost, packaging, and
  regression evidence.

Owned files/symbols:

- `email_scraper/src/prisma-run-repository.js`:
  `claimAwsTrafficWorkBatch()`, `publishAwsFinalResults()`,
  `finalizePersistedLeadScoresV3()`, and new private bulk helpers used only by
  those symbols. `completeTrafficEnrichment()` is a read-only caller boundary:
  its code and signature do not change, but its local-backend scoring path must
  pass the same bulk-score regression;
- new `email_scraper/src/aws-pipeline/core/bounded-concurrency.js`:
  `mapWithConcurrency()`;
- `email_scraper/src/enrichment/orchestrator.js`:
  removal of its private concurrency helper and the exact
  `enrichDataForSeoSource()` wave refactor;
- `email_scraper/src/aws-pipeline/services/traffic-worker.js`:
  bounded artifact reconciliation and fenced terminal fan-out only;
- `email_scraper/src/aws-pipeline/services/domain-aggregator.js`,
  `lead-aggregator.js`, and `final-aggregator.js`: bounded artifact operations
  and final DataForSEO batch memoization only;
- `email_scraper/src/aws-pipeline/adapters/queue-dispatcher.js`:
  `SqsDispatcher.sendMany()` only;
- focused tests in
  `email_scraper/test/aws-pipeline-bounded-concurrency.test.js` (new),
  `prisma-run-repository.test.js`,
  `aws-pipeline-traffic.integration.test.js`,
  `aws-pipeline-final.integration.test.js`,
  `aws-pipeline-traffic.test.js`, `aws-pipeline-domain.test.js`,
  `aws-pipeline-lead-aggregation.test.js`, `aws-pipeline-final.test.js`,
  `aws-pipeline-runtime-adapters.test.js`, and
  `dataforseo-enrichment.test.js`; the existing
  `progressive-persistence.integration.test.js` is a required unchanged-caller
  regression; and
- completion evidence in `AWS_PIPELINE_EXECUTION_EVIDENCE.md` and the one
  completion transition in `ACTIVE_EXECUTION_STATE.md`.

Shared-file permissions: the named source files already contain accepted dirty
G-R17-through-G-R19 work. Patch them in place and preserve every unrelated
change. Do not reset, restore, stage, commit, or rewrite history. The frozen
specification must not be edited by the implementing agent.

Non-goals/prohibited actions:

- no schema, migration, public API, message, artifact, fingerprint, timestamp,
  identity, ownership, lease-duration, provider timeout, cache-freshness,
  infrastructure, Lambda memory/timeout/reservation, frontend, or UI change;
- no per-domain DataForSEO request, no per-domain BigQuery query, no change to
  the CrUX REST concurrency snapshot, and no unbounded `Promise.all`;
- no AWS mutation, deployment, queue receive/purge/redrive/visibility change,
  provider call, Browserless call, BigQuery call, production-database write,
  destructive action, stage/commit, or live-run repair; and
- no timeout increase as a substitute for bulk work.

### 18.2 Locked constants and shared concurrency interface

Create and export exactly:

```js
export async function mapWithConcurrency(items, limit, mapper)
```

in `src/aws-pipeline/core/bounded-concurrency.js`.

The contract is:

1. `items` must be an array, `limit` an integer from 1 through 32, and `mapper`
   a function; otherwise throw `PipelineInvariantError("PIPELINE_INPUT_CONFLICT")`
   before invoking the mapper.
2. Return an array of exactly `items.length` entries in input-index order,
   independent of completion order. Empty input returns `[]` without invoking
   the mapper.
3. Start at most `min(limit, items.length)` mapper calls. Workers claim indexes
   monotonically. On the first rejection, stop assigning new indexes, await
   all already-started calls with no unhandled rejection, then throw the error
   belonging to the lowest failed input index. Already-started immutable writes
   may finish and are reconciled on retry.
4. No caller may pass a dynamic/environment-derived limit in this window.
   Define and use exactly:

```text
S3_IO_CONCURRENCY = 8
TASK_SETTLEMENT_CONCURRENCY = 4
SQS_BATCH_CONCURRENCY = 4
DATAFORSEO_SCOPE_CONCURRENCY = 2
```

The constants are private to their owning modules except the shared helper.
They are behavior constants, not environment configuration, and do not enter
the durable run snapshot because they change scheduling only—not output,
provider selection, request identity, or retry authority.

Remove the private `mapWithConcurrency()` from `enrichment/orchestrator.js` and
import the shared function. Existing CrUX REST execution continues to pass the
durable `policy.concurrency` value, which remains two for the deployed run.

Decisive helper tests must use deferred promises to prove positional results,
actual parallel progress above one, a maximum of exactly the supplied limit,
empty input, invalid arguments before side effects, lowest-index rejection,
no new work after rejection is observed, and no unhandled rejection from
already-started work.

### 18.3 T1 — set-based Neon traffic claims

The public signature and return union of
`PrismaRunRepository.claimAwsTrafficWorkBatch(input, now)` remain unchanged.
`claims` remains ordered, unique, and bounded by
`DATAFORSEO_TARGET_LIMIT` (1,000). Use one existing interactive transaction and
retain its default five-second timeout; do not add or raise a timeout.

Inside that transaction perform these ordered, constant-count operations:

1. Select the repository's validated schema with `selectBulkSchema()`.
2. Validate the AWS Run/generation/live run-lease and the `traffic_crux` stage
   exactly as today.
3. Load all referenced PipelineTasks in one query, index by ID, and require
   exact task count plus `task.itemKey === claim.shopId` for every input.
4. `createMany(..., {skipDuplicates:true})` all missing ShopWork rows once.
5. Lock all requested ShopWork rows in one schema-scoped
   `SELECT ... FOR UPDATE` joined to a `jsonb_to_recordset` input ordered by
   input ordinal. Require exact row equality; do not rely on returned database
   order.
6. In one query load every cache row needed by a currently `completed` work
   item using all five immutable selection fields. Group by the exact
   `source\0identity\0scopeKey\0metricSetKey\0contractVersion` key and preserve
   the existing requirements: exactly one row, valid dates, `fetchedAt <= now`;
   a fresh row returns `completed`, while an expired row becomes reclaimable.
7. In one query load every non-null `processingPipelineTaskId` owner including
   owner task state and owner Run state. In one additional query load every
   legacy non-null `processingRunId` owner needed for lease validation.
8. Classify every claim synchronously in original input order with the existing
   precedence: fresh completed cache -> `completed`; ambiguous -> `ambiguous`;
   same PipelineTask owner -> `owned`; different live task or live legacy Run
   owner -> `busy`; otherwise reclaimable. A PipelineTask owner is live only
   when its owning Run is `running` and the task is not `cancelled`. A legacy
   Run owner is live only when Run state, lease token, and unexpired lease all
   match the ShopWork row.
9. Submit every reclaimable row in one `UPDATE ... FROM
   jsonb_to_recordset(...)` statement. Its predicate must match the row ID,
   prior enum state, and all three prior owner fields with null-safe
   `IS NOT DISTINCT FROM`; its values set the same processing fields, timestamps,
   and cleared safe errors as the current per-row update. `RETURNING id` is the
   sole win certificate. A returned ID is `owned`; a missing returned ID is
   `busy`. Require no unknown/duplicate returned ID.
10. Return one result per input in original order. No database call, `await`, or
    repository call may occur inside the classification loop.

This is `SAME TRANSACTION`. It changes neither ShopWork identity nor recovery:
retry sees fresh cache, same-task ownership, a live competing owner, or a
reclaimable inactive owner exactly as before.

The real isolated-PostgreSQL test must create a 1,000-claim mixed corpus that
contains fresh completed, expired completed, ambiguous, failed, pending,
same-task processing, different live-task processing, cancelled-task owner,
inactive-Run task owner, live legacy-Run owner, and expired legacy-Run owner.
It must assert exact positional outcomes, exact cache rows, no ownership theft,
the set of updated IDs, same-task replay, stale run-lease rejection, and
completion inside the default transaction timeout. A one-claim corpus must
produce the same semantics. The test must use
`test/helpers/isolated-postgres.js`, a direct non-production database, a unique
disposable schema, verified `current_schema()`, schema-local migration history,
and `finally` cleanup; `public` must never be readied or cleaned.

### 18.4 T2 — set-based final publication

The public signature and return value of
`publishAwsFinalResults(input, now, {afterStep})` remain unchanged. Preserve
the existing `SAME TRANSACTION` ordering and every named `afterStep` boundary:
`cache_written`, `traffic_written`, `work_settled`, `profiles_settled`,
`diagnostics_written`, `scores_finalized`, `grants_written`, `stage_completed`,
and `before_run_visibility`. Replace `{maxWait:5000, timeout:90000}` with
exactly `{maxWait:5000, timeout:15000}` after the N+1 removals.

Before mutation, require uniqueness of `workOutcomes` by
`shopId\0workType\0scopeKey` and `leadProfileOutcomes` by `shopId`. Then:

1. Keep the aggregator fence, ledger lock/equality check, cache bulk upsert, and
   traffic bulk upsert unchanged.
2. Lock all referenced ShopWork rows once with `SELECT ... FOR UPDATE` joined to
   ordinal JSON input. Classify synchronously using the current state mapping:
   `available|no_coverage -> completed`, `ambiguous -> ambiguous`, `reused ->
   reused`, everything else -> failed. Reused requires an already-completed
   row. An already-target-state row is idempotent. Every other row must be
   `processing` and owned by the exact Run and PipelineTask. Update all mutable
   rows in one `UPDATE ... FROM jsonb_to_recordset` with the exact prior-state
   and owner CAS, existing safe codes/messages, `completedAt=now`, and returned
   ID set equality.
3. Load all referenced ShopLeadProfile rows and all non-`existing`
   `lead_discovery/current` ShopWork rows in two set queries, locking them.
   Parse/fingerprint every `new` profile before writes. Existing profile rows
   must be `completed` and fingerprint-equal. Bulk insert missing new profiles
   once, then reload and validate the complete required profile set.
4. Link every `new` or `existing` Lead to `shopLeadProfileId=shopId` in one
   schema-scoped set update restricted to `Lead.runId=input.runId`; assert that
   every requested shop maps to exactly one run Lead. Bulk settle new-profile
   work as completed and failed-profile work as failed in one CAS update, with
   exact returned-ID equality. Existing profiles do not settle a work row.
5. `finalizePersistedLeadScoresV3()` retains its two reads and exact V3 scoring
   function. Convert every computed lead through `leadRecordToCreate()` as
   today, then update every lead in one `UPDATE ... FROM
   jsonb_to_recordset(...)` restricted by both ID and Run ID. Preserve nullable
   `scoreBreakdown`; require returned-ID set equality and return scoring version
   three. No per-lead database call is allowed. The same helper remains the
   scoring primitive for both AWS `publishAwsFinalResults()` and local
   `completeTrafficEnrichment()`; both callers must retain their existing
   transaction and visibility behavior.
6. Keep diagnostic bulk upsert, owner grants, result-fingerprint inputs,
   aggregator completion, and the visibility-last conditional Run update in
   their existing order. `resultsAvailable=true` remains the final durable
   write. Any error or `afterStep` injection rolls back all writes.

The isolated final-publication integration corpus must prove:

- mixed new/existing/failed profiles and completed/failed/ambiguous/reused work;
- idempotent already-target-state rows and rejection of wrong Run/task owners;
- exact profile fingerprints, lead links, V3 scores, grants, terminal stage,
  result fingerprint, and no visibility before the last Run update;
- rollback at every retained `afterStep` boundary; and
- a maximum 1,000-domain run with ten DataForSEO scopes plus both CrUX sources
  (up to 12,000 work outcomes and 1,000 profile outcomes) finishes within the
  locked 15-second transaction timeout on the verified disposable test
  transport and leaves exact row cardinalities.

No SQL statement or Prisma call may be issued inside an outcome/profile/lead
loop. Serialization, parsing, scoring, maps, and validation may loop in memory.

### 18.5 T3 — bounded traffic-worker artifact and terminal phases

Retain `processTrafficBatch(records, runtime, dependencies={})`, its grouping,
single stage-wide Run lease, provider protocols, returned positional SQS
results, and provider-call cardinalities. Refactor only the serial per-task I/O
around them into these barriers:

1. Build and sort a deduplicated optional-read plan for every enabled source
   artifact and combined artifact. Execute `getOptionalValidated()` at
   `S3_IO_CONCURRENCY=8`; preserve each exact key, expected envelope, schema,
   missing/found/corrupt/conflict behavior, and place found values into the
   existing durable-source/combined maps only after validation.
2. Perform reuse validation, set-based traffic claims, DataForSEO, CrUX REST,
   and CrUX BigQuery through the unchanged durable provider seams. Provider
   execution does not overlap this window's S3 recovery-read phase.
3. Build all missing provider-source artifacts in deterministic task/source
   order without I/O. Write them with `putImmutable()` at concurrency eight.
   Every source write must settle before any combined-artifact write starts.
4. Build all eligible combined artifacts from validated durable or newly
   written source artifacts. Write combined artifacts at concurrency eight.
   Every combined write must settle before any task-terminal operation starts.
5. For each eligible task, execute the existing `claimTask()` followed, only
   when owned, by `recordTerminal()` as one indivisible mapper chain at
   `TASK_SETTLEMENT_CONCURRENCY=4`. Call `monitor.assertActive()` before each
   chain and immediately before `recordTerminal()`. Terminal replay remains
   terminal without another write. A busy task is nonterminal. Count results
   by input task, not completion order.
6. Renew/stop the Run lease, release it, and send exactly one final aggregation
   check only after the terminal phase, using the existing condition that at
   least one task was terminal. Preserve final sorted per-record results.

If a bounded phase rejects, no later phase begins. Work already started may
finish; immutable S3 and fenced Neon make it replayable. Retry rereads all
artifacts before provider work. Source-write failure therefore produces no
combined write; combined-write failure produces no terminal for that item;
terminal failure leaves its validated combined artifact for replay. None of
these failures authorizes another DataForSEO call after a succeeded/ambiguous
ledger or another CrUX call after an attempt marker with uncertain outcome.
Cancellation or lease loss stops new scheduling and forbids later fenced
terminal/publication writes.

Focused tests must use at least 52 nonempty domains and delayed fakes to prove
S3 maximum in-flight eight with actual overlap, terminal-chain maximum four
with actual overlap, strict read -> provider -> source-write -> combined-write
-> terminal -> aggregation-check barriers, deterministic outputs under reverse
completion, and each failure/retry boundary above. The existing real
PostgreSQL traffic test must exercise all 52 domains through the real
`claimAwsTrafficWorkBatch()` rather than a mocked repository.

### 18.6 T4 — bounded aggregators and batch-artifact memoization

Use `mapWithConcurrency(..., S3_IO_CONCURRENCY, ...)` for independent immutable
artifact operations while preserving deterministic assembly:

- Domain Aggregator: query-discovery artifact reads at eight; after all reads
  validate, candidate artifact writes at eight; only after all candidate
  writes complete may the domain manifest be written and Neon checkpoint be
  published.
- Lead Aggregator: lead-result artifact reads at eight; all profile/reuse and
  checkpoint logic remains after the read barrier.
- Final Aggregator: combined-traffic reads at eight; provider-source reads at
  eight; lead-result reads at eight. Do not publish until every required value
  is validated.

For final DataForSEO evidence, first collect all expected batch references by
`batchArtifactKey`. Before any batch GET, require duplicate references to agree
exactly on batch ID, scope, request fingerprint, target count, artifact
fingerprint, and expected envelope. A disagreement is
`PIPELINE_INPUT_CONFLICT`. Read each unique batch key exactly once at
concurrency eight, parse/validate it once, memoize it by key, and validate each
referencing domain's membership from that parsed value. A missing, corrupt, or
conflicting artifact keeps the current strict failure; it is never treated as
absent coverage.

All output arrays, fingerprints, summaries, cache rows, work outcomes, ledger
evidence, and dispatch messages must retain their existing deterministic sort
rules. Concurrency affects only scheduling.

Tests must prove the phase barriers, max-eight I/O, reverse-completion equality,
failure before checkpoint/publication, and exact GET cardinality. The decisive
final case is 52 domains across all ten scopes where each scope references one
shared DataForSEO batch: exactly ten provider-batch GETs occur, not 520, while
every domain membership and ledger-evidence assertion still runs.

### 18.7 T5 — bounded SQS batch dispatch

Keep `SqsDispatcher.sendMany(queueUrl, messages, schema)` and its return object
unchanged. Parse every message before any AWS SDK call. Build the same ordered
chunks of at most ten with the same deterministic entry IDs. Execute chunk
calls through `mapWithConcurrency(chunks, 4, mapper)`.

The mapper must retain current behavior: an SDK rejection marks every item in
that chunk failed; a response must account for every entry exactly once and
must reject duplicate, missing, or unknown IDs as
`PIPELINE_MESSAGE_INVALID`. After all chunks settle, flatten results by
original message index and derive `sentItemIds` and `failedItemIds` from that
positional array, never completion order. A malformed response can occur after
other chunks were sent; throw the contract error and rely on existing durable
dispatch recovery rather than pretending atomic multi-chunk delivery.

Tests must prove zero messages, 1, 10, 11, 40, 41, and 1,000 messages; maximum
four batch calls in flight with actual overlap; exact ten-entry chunks and IDs;
reverse completion; one SDK-rejected chunk with other chunks successful;
duplicate/missing/unknown response IDs; positional result equality; and no SDK
call when any input message fails strict parsing.

### 18.8 T6 — two-wide DataForSEO scope waves without cost regression

The cost unit remains the current bulk scope request—not a domain. The durable
run snapshot contains exactly ten ordered scopes: worldwide plus US, GB, CA,
AU, NZ, DE, FR, IN, and AE. Each nonempty scope retains one DataForSEO bulk
request of at most 1,000 unique canonical hostnames, the existing deterministic
request fingerprint, one paid ledger, one cost reservation, and one immutable
batch result artifact. Maximum provider calls for a fully uncached 1,000-domain
run remains ten. Never fan out by domain.

Refactor `enrichDataForSeoSource()` into ordered waves of two scopes:

1. For both scopes in a wave, in durable snapshot order, perform cache reads,
   ShopWork reservation/reconciliation, request construction, ledger planning,
   and ledger claim sequentially. A network descriptor exists only after
   `claimDataForSeoRequest().networkAllowed === true`. This is the durable
   pre-call evidence.
2. Execute only those descriptors with
   `mapWithConcurrency(descriptors, DATAFORSEO_SCOPE_CONCURRENCY, ...)`. Each
   descriptor still performs exactly one bulk fetch and its existing success
   settlement or failed/ambiguous ledger plus ShopWork settlement. Results are
   written to their scope slot, not completion order.
3. Wait for every descriptor in the wave to settle. Re-read authoritative
   `getDataForSeoRunCostUsd()` before planning the next wave. The existing
   estimated reservation is the pre-dispatch budget exposure; provider-reported
   cost replaces it on success. If the locked budget is exhausted, mark all
   remaining unclaimed scopes unavailable without a ledger claim or provider
   call.
4. A crash before claim permits normal planning. A crash after claim but before
   or during response leaves the existing in-flight/ambiguous recovery and
   forbids a second paid call. A crash after success settlement reuses cache and
   the succeeded ledger. One scope's zero-cost-proven/not-dispatched error may
   be failed safely; an uncertain outcome remains ambiguous. Concurrent peer
   completion does not change either rule.
5. Preserve exact diagnostics, summary, cache-hit/external-task counts,
   on-source-complete behavior, lease assertions, target sorting, batch
   request/response adapters, and the single latest-table plus single bounded
   multi-origin CrUX BigQuery flow.

Tests must drive all ten scopes with delayed provider fakes and durable fake
ledgers. Assert exactly ten calls, every call has the full scope target batch,
max provider concurrency two and greater than one, wave barrier before scopes
three/four, stable request fingerprints, cost reservations before calls,
authoritative cost reread between waves, budget stop without later claims,
success/zero-cost/ambiguous mixtures, crash/replay with no duplicate paid call,
reverse-completion-identical output, and the exact 52-domain provider-call
ceiling already required by G11. Existing CrUX REST concurrency and BigQuery
call ceilings must remain unchanged.

### 18.9 Interface, persistence, external-call, and recovery ledgers

| Surface | Locked contract | Durable/external order | Decisive assertion |
|---|---|---|---|
| `mapWithConcurrency(items,limit,mapper)` | New exported positional helper; no other public signature changes | Memory only; bounded started work drains on rejection | Deferred-promise unit corpus |
| `claimAwsTrafficWorkBatch()` | Existing input/return union; max 1,000; constant DB statements | One existing transaction; bulk lock/read/classify/CAS | Real 1/1,000 mixed PostgreSQL corpus under default timeout |
| `publishAwsFinalResults()` | Existing input/return/afterStep API; 15-second transaction | Existing visibility-last transaction; bulk work/profile/score SQL | 1,000-domain/12,000-work corpus and every rollback boundary |
| Traffic S3 operations | Existing keys, parsers, fingerprints, produced-at values | All reads -> provider -> all source writes -> all combined writes -> fenced terminals | 52-domain barrier/failure/replay test |
| Aggregator S3 operations | Existing immutable artifacts and strict missing/corrupt/conflict behavior | Read barriers before any checkpoint/publication | Reverse-completion and failed-read tests |
| DataForSEO batch evidence | One GET per exact batch key; duplicate metadata must agree | Collect/validate references -> unique GETs -> per-domain membership | Ten GETs for 52 domains x ten scopes |
| SQS dispatch | Existing messages and ten-entry AWS API chunks | Strict parse-all -> at most four concurrent chunk calls -> positional flatten | 1,000-message partial/reverse/malformed corpus |
| DataForSEO provider | One bulk request per nonempty scope, max ten per run, max two concurrent | ShopWork/cache -> plan -> paid claim -> provider -> cache/artifact/ledger settlement | Ten-scope cost/restart/cardinality corpus |

Persistence is `N/A` for schema changes: no model, enum, index, migration, key,
retention, or cleanup changes. Message/artifact shapes are `N/A` for contract
changes: only operation scheduling and duplicate read elimination change.
Identity/authorization is unchanged and is still fenced by the same Run,
PipelineStage, PipelineTask, ShopWork, aggregator token, and final Run CAS.

Database transport is fixed: only a non-production direct PostgreSQL URL may be
used for migration-backed verification. `test/helpers/isolated-postgres.js`
owns URL precedence, Neon pooler-to-direct derivation, unique schema grammar,
`search_path`, schema-local `_prisma_migrations`, and `finally` cleanup. Fail
closed for production identity, a remaining pooler, `public`, schema drift, or
cleanup failure. No migration is added.

Build/runtime closure is fixed: these shared source changes may enter any of
the seven Node 24 Lambda ZIPs. Rebuild all seven with the pinned existing
esbuild/AWS SDK/Prisma toolchain, measure and cold-import the emitted ZIPs in a
fresh process, verify exactly the RHEL Prisma engine, deterministic repeated
file-list hashes, existing size limits, and forbidden-file/secret rules. No
build script, dependency version, handler export, native asset, or
infrastructure template change is authorized. A packaging failure caused by
the prescribed source is an ordinary in-window defect; only an actually
missing decision or required ownership expansion is a blocker.

### 18.10 Mechanical traces and simulations

Mechanical traces:

```text
traffic SQS group -> processTrafficBatch -> claimAwsTrafficWorkBatch
-> set reads/classification/CAS -> 1,000-row PostgreSQL assertion
-> unchanged provider owner

terminal traffic artifacts -> processFinalAggregation
-> one batch-key read + per-domain validation -> publishAwsFinalResults
-> set work/profile/score writes -> final Run CAS -> visible results

ordered messages -> SqsDispatcher.sendMany -> ten-entry chunks
-> concurrency-four SDK calls -> positional results -> recordDispatch/recovery

ten durable scopes -> sequential durable reservations per two-scope wave
-> at-most-two bulk provider calls -> durable settlement -> cost reread
-> next wave or deterministic budget stop
```

Forward simulation passed at specification time: input parsing and all durable
claims precede external calls; provider recovery reads precede new calls;
source S3 precedes combined S3; combined S3 precedes PipelineTask terminal;
all traffic tasks precede aggregation; all final private writes precede the
single visibility CAS. Failure in any bounded phase starts no later phase.
Already-finished immutable or fenced work is reconciled on retry. Parallel
completion changes no positional output or fingerprint.

Backward simulation passed at specification time: every public final row still
traces to the same validated lead/provider artifacts and exact durable cache,
ledger, profile, work, task, stage, and Run rows. Every retry decision traces
to an immutable artifact, paid ledger, provider attempt marker, ShopWork owner,
PipelineTask token, or Run/aggregator lease. The new concurrency helper creates
no durable authority and cannot make results visible.

### 18.11 Required verification and acceptance

Run from `email_scraper/` in this order:

```text
node --test test/aws-pipeline-bounded-concurrency.test.js \
  test/dataforseo-enrichment.test.js \
  test/aws-pipeline-runtime-adapters.test.js \
  test/aws-pipeline-traffic.test.js \
  test/aws-pipeline-domain.test.js \
  test/aws-pipeline-lead-aggregation.test.js \
  test/aws-pipeline-final.test.js \
  test/prisma-run-repository.test.js

ALLOW_DATABASE_TESTS=true node -r dotenv/config --test --test-concurrency=1 \
  test/aws-pipeline-traffic.integration.test.js \
  test/aws-pipeline-final.integration.test.js \
  test/progressive-persistence.integration.test.js \
  test/aws-pipeline-end-to-end.integration.test.js

ALLOW_DATABASE_TESTS=true npm run test:integration
npm test
npm run build:lambda
npm run measure:lambda
node --test test/aws-pipeline-packaging.test.js
npm run check:secrets
git diff --check
```

The database command is executable only when the shared harness proves a
non-production direct connection and disposable non-`public` schema; otherwise
the implementing agent stops with the exact missing test prerequisite and does
not substitute production. A restricted-localhost failure is rerun with the
ordinary sandbox approval available to the executing agent.

Acceptance requires all of the following, not merely green commands:

1. every T1-through-T6 named behavioral and adversarial assertion passes;
2. real PostgreSQL proves both the exact 1,000-claim and maximum final
   publication corpora within their locked transaction timeouts;
3. no database/repository call remains inside the named per-item loops;
4. observed maximums are S3 eight, terminal four, SQS batch calls four,
   DataForSEO provider calls two, and all show actual overlap when work exists;
5. DataForSEO remains at most ten bulk provider calls and never becomes
   per-domain; CrUX BigQuery remains one latest-table lookup plus one bounded
   multi-origin query; CrUX REST remains at durable concurrency two;
6. immutable-write, paid-call, lease-loss, partial-SQS, reverse-order,
   duplicate, and final-publication recovery produce identical terminal
   results without premature visibility or repeated uncertain paid calls;
7. the full G-R9 16-boundary recovery matrix and full backend corpus have zero
   failures other than documented guarded skips;
8. all seven emitted Lambda packages build, measure, cold-import, contain only
   the required Prisma native engine, and pass deterministic/privacy checks;
9. no AWS/provider/production database/frontend/infrastructure action occurred;
   and
10. evidence records changed files, exact commands/results, statement and
    concurrency cardinalities, skipped checks/reasons, residual risks, external
    actions (`none`), and preserved dirty work. Then update only
    `ACTIVE_EXECUTION_STATE.md` to `current_status: COMPLETED` and
    `accepted_through: G-R20`, and stop at its declared parent-review boundary.

### 18.12 Decision-completeness audit and preflight gate report

The parent authoring audit searched every named source and its current tests for
`claimAwsTrafficWorkBatch`, `publishAwsFinalResults`,
`finalizePersistedLeadScoresV3`, `enrichDataForSeoSource`, `sendMany`,
`getOptionalValidated`, `putImmutable`, `claimTask`, `recordTerminal`, and
per-item `for`/`await` sites. The closed reachable set is exactly: traffic
claims; final work/profile/score settlement; traffic recovery/source/combined
artifact operations; domain/lead/final aggregator artifact operations; final
DataForSEO batch reads; SQS batch sends; and DataForSEO scope provider calls.
No schema writer, alternate dispatcher, provider adapter, identity function,
message/artifact parser, or visibility writer needs modification. The local
`completeTrafficEnrichment()` caller of the shared scoring helper is explicitly
covered by its existing unit and real-PostgreSQL regressions.

Counterexample audit decisions:

- cache, ownership, failure, and terminal semantics are copied from the current
  branches rather than reinterpreted;
- no nested transaction is introduced;
- artifact/message reconstruction is unchanged because keys, envelopes,
  fingerprints, and durable timestamps are unchanged;
- provider call cardinality is locked and failure-injected;
- Run/task/aggregator lease durations and renewal ownership are unchanged;
- no new environment read or nondurable behavior setting exists;
- final visibility remains the last Run CAS in the same transaction; and
- every changed packaged entry point is rebuilt from its final emitted ZIP.

Readiness classification:

```text
BLOCKERS BEFORE START: none
USER ACTIONS BEFORE START: none
PREDICTABLE FUTURE GATES: F-GR20-DEPLOY — after G-R20 completion and independent
  parent verification, compare each of the seven deterministic ZIP SHA-256
  values with the last approved deployment manifest. The changed set is exactly
  the functions whose hashes differ; unchanged functions retain their approved
  object versions. If verification fails, open a local append-only correction.
  If it passes, deployment still waits for A-GR20-DEPLOY and begins in a new
  guarded code-only corrective window preserving G-R20 evidence.
PAID/MUTATING APPROVALS NOT YET GRANTED: A-GR20-DEPLOY — explicit user approval
  is required before uploading changed content-addressed AES256/versioned ZIPs,
  creating/executing a guarded CloudFormation code-only change set, or allowing
  the deployed pipeline to resume provider work. No approval is required for
  this local implementation window.
PLANNED USER STOP: after G-R20 local acceptance, for independent parent review
  and the user's separate deployment decision
```

Readiness certificate: `READY / ASSIGNABLE`. The locked product contract is
`AWS_ASYNC_DEPLOYMENT_DIRECTION.md`; this implementation specification is the
plan; `ACTIVE_EXECUTION_STATE.md` is the sole live authority; and
`AWS_PIPELINE_EXECUTION_EVIDENCE.md` is the sole evidence destination. The
window has exact ownership, interfaces, algorithms, transaction and recovered
boundaries, fixed limits, failure behavior, tests, mechanical traces, forward
and backward simulations, a closed set-equality audit, and no delegated
implementation-affecting choice.

## 19. G-R21 — guarded G-R20 candidate deployment and existing-run recovery

This append-only deployment window records the user's 15 August 2026 decision
to defer the known G-R20 maximum-size acceptance gaps while testing the
implemented bounded-bulk correction against the existing production run
`run_KRnkR1jV7QInr2zXhHE-Hi9c` and a later user-created 100-domain run.

ID: `G-R21`

Objective: deploy the exact locally verified G-R20 candidate through the
existing content-addressed, versioned, AES256 CloudFormation path and allow the
already-enabled durable recovery path to resume only existing queued work. This
window does not accept G-R20's deferred 1,000-domain transaction or T3-through-
T6 proof gaps and does not authorize a new run.

Owned changes:

- add deployment phase `bounded-bulk` to
  `email_scraper/scripts/aws-pipeline/create-change-set.js` and its existing
  infrastructure test;
- upload all seven deterministic Lambda ZIPs and the byte-unchanged template to
  their content-addressed `deployment/` keys in the retained production bucket;
- create and inspect a CloudFormation update whose normalized inventory is
  exactly the seven `AWS::Lambda::Function` Code modifications plus the known
  `RecoveryInvokePermission` and `RecoverySchedule` dependency re-evaluations;
- execute only that reviewed change set and wait for `UPDATE_COMPLETE`; and
- observe the existing SQS mapping and scheduled Recovery resume
  `run_KRnkR1jV7QInr2zXhHE-Hi9c` until it becomes terminal or exposes a new
  concrete blocker.

Locked non-changes: no template topology, queue, DLQ, event-source enablement,
mapping batch/concurrency, Lambda memory/timeout/reserved concurrency, IAM,
secret, database schema/row, S3 `runs/` object, retention, frontend, or provider
policy change. Do not receive, purge, redrive, delete, or manually alter queue
messages. Do not repair coordinator rows. Existing immutable artifacts, paid
ledgers, attempt markers, task fencing, and scheduled recovery remain the sole
resume authority.

External authorization: the user's explicit request authorizes the seven
content-addressed uploads, creation/execution of the exact guarded code-only
change set, and provider work that the existing run's durable claims permit.
It does not authorize unrelated runs, destructive action, secret changes, or a
new run.

Required preflight and acceptance:

1. Verify the product/plan hashes, AWS SSO identity, stack
   `storesignal-production-pipeline` in `ap-south-2`, current stack state, exact
   target run state, mapping/rule enablement, queue counts, and no conflicting
   stack operation.
2. Rebuild and measure all seven ZIPs; pass packaging, infrastructure,
   secret-scan, and diff checks. Generate the approval token from those exact
   bytes and record it only in `ACTIVE_EXECUTION_STATE.md`.
3. Run `package --execute`; reconcile or write only content-addressed versioned
   objects. Run `bounded-bulk --execute` to create and guard the change set.
   Execute it only with `--apply-reviewed-change-set` after its normalized
   inventory passes.
4. Require stack `UPDATE_COMPLETE`; verify every deployed function's code hash
   equals its local ZIP, all six mappings and Recovery remain enabled, Traffic
   reserved concurrency remains one, and no infrastructure property drifted.
5. Observe the target coordinator stage and queue/log activity without manual
   queue or database mutation. Acceptance requires the target Run to reach a
   terminal state with truthful visibility, or a concise new blocker backed by
   live evidence. Append exact evidence and stop; the user owns the subsequent
   fresh 100-domain run.

Stop and escalate only for an unexpected change-set resource/detail, failed
stack update, deployment hash mismatch, missing AWS permission/session, a new
provider/contract ambiguity not governed by durable evidence, or the target
run reaching a stable new failure state. The known deferred G-R20 acceptance
gaps are not a blocker to this explicitly authorized guarded production test.

## 20. G-R24 — provider-version resilience and complete traffic publication

ID: `G-R24`

Objective: correct the two production defects proven by
`run_-hPWjmwusV7P7AS_QcxqTZlR` and deploy only the affected TrafficWorker and
FinalAggregator packages. The completed run remains immutable failure evidence;
the user creates a fresh run for the end-to-end production proof.

Locked decisions:

1. DataForSEO root versions matching `0.1.YYYYMMDD` are release metadata, not a
   business-contract discriminator. The adapter accepts that exact grammar while
   continuing to require every consumed status, cost, task, target, scope, count,
   item, and metric field. A major/minor or malformed version still fails closed.
   Current positive fixtures use the observed `0.1.20260806` value.
2. A paid response whose body fails the consumed contract may retain source state
   `contract_mismatch` while its paid ledger remains `ambiguous`; the provider
   source contract permits precisely that pairing. This prevents a DataForSEO
   parser failure from invalidating sibling CrUX artifacts.
3. A traffic task whose combined component is `skipped` solely because every
   source selection was a validated cache reuse still publishes exactly one
   `LeadTrafficEnrichment` for that lead/source. Final aggregation derives it from
   manifest-fingerprinted cache rows and the qualified run Lead for the same shop.
   It never invokes a provider and never grants access from cache existence alone.
4. DataForSEO reuse requires all ten frozen scopes and produces one `available`
   lead row containing ten normalized records in scope-key order with the newest
   fetched timestamp. CrUX reuse requires its exact selection and produces
   `available` with validated payload/timing or `no_coverage` without payload or
   timing. Missing, duplicate, mismatched, expired, post-snapshot, or non-qualified
   lead/cache evidence fails `PIPELINE_INPUT_CONFLICT`.
5. Deployment phase `traffic-publication-repair` uses previous values for the
   other five packages and may modify exactly `TrafficWorker` and
   `FinalAggregator`, both `AWS::Lambda::Function` resources with replacement
   `False`. It changes no topology, IAM, mappings, concurrency, queues, secrets,
   database rows/schema, S3 `runs/` objects, or frontend.

Owned files: DataForSEO request/contract and fixtures/tests; provider-source
artifact contract/tests; final aggregation service, Prisma reuse reader and
focused unit/integration tests; guarded deployment script and infrastructure
test; this specification, live state, and evidence log.

Acceptance: focused DataForSEO, artifact-contract, traffic, final and deployment
tests; isolated PostgreSQL final-publication proof; complete backend suite; seven
deterministic Lambda builds, measurements and cold imports; secret scan and diff
hygiene. Then create, inspect and execute the exact two-function CloudFormation
change set, require `UPDATE_COMPLETE`, match deployed code hashes, and leave
mappings/recovery enabled and every other resource unchanged. No additional paid
call is required: the authorized diagnostic already proved HTTP 200, 21/21 items,
provider version `0.1.20260806`, parser-only rejection, and actual cost `$0.01452`
without retaining raw provider content.

## 21. G-R25 — preserve resolved CrUX month and recover final publication

ID: `G-R25`

Objective: complete existing Run `run_emuJITjaps8nvFyNiiA73UJH` after its first
post-G-R24 production execution proved six CrUX BigQuery `contract_mismatch`
artifacts lost their already-resolved `month:202607` identity by recording
`scopeKey=latest`. Traffic is otherwise terminal 61/61 and DataForSEO is
successful. Preserve all immutable artifacts and paid/provider evidence.

Locked decisions:

1. Once `fetchCruxLatestDatasetMonth` succeeds, TrafficWorker retains
   `month:<YYYYMM>` as the source scope for every later outcome, including
   `contract_mismatch`, `unavailable`, and `ambiguous`. It may use `latest` only
   when no month was resolved.
2. FinalAggregator treats a terminal CrUX BigQuery source artifact with
   `scopeKey=latest` and state `ambiguous`, `unavailable`, or
   `contract_mismatch` as requiring durable owner resolution. The repository
   must find exactly one task-fenced `crux_bigquery` ShopWork owned by this Run
   and PipelineTask whose scope is either `latest` or `month:20\d{4}`. It returns
   that exact scope; zero, duplicate, wrong-owner, wrong-task, or invalid scopes
   fail `PIPELINE_INPUT_CONFLICT`.
3. The resolved scope, not the artifact alias, is used only for ShopWork
   terminal settlement. S3 artifacts, source state, normalized traffic rows,
   cache identity, provider ledgers, and provider-call counts are unchanged.
4. The existing transaction remains visibility-last. A failed attempt rolls
   back all traffic writes and ShopWork changes; replay publishes exactly once.
5. Deployment updates exactly `TrafficWorker` and `FinalAggregator` code in
   place with replacement `False`. No queue/DLQ receive, purge, or redrive; no
   S3 `runs/` mutation; no production database repair; no provider call; and no
   topology, mapping, secret, IAM, concurrency, frontend, or schema change.

Acceptance: focused traffic/final/repository tests must reproduce post-month
contract mismatch and pre-month terminal scope resolution; isolated PostgreSQL
publication must prove exact task fencing, rollback and replay; backend,
integration, package/cold-import, secret and diff checks pass. Create and review
an exact two-function code-only change set, execute it to `UPDATE_COMPLETE`,
match deployed hashes, and observe this same Run naturally retry to
`completed` with `resultsAvailable=true` and independently published
DataForSEO, CrUX REST and CrUX BigQuery rows.

## 22. G-R26 — shared provider-identity ownership and cache fan-out correction

This is an append-only local corrective window. It contains no live status;
`ACTIVE_EXECUTION_STATE.md` alone authorizes execution. Deployment and live-run
recovery remain a separate approval gate after local acceptance.

### 22.1 Window header

ID: `G-R26`

Objective: make two or more distinct stable shops that share one canonical
provider hostname/origin execute as one provider/cache identity but retain one
fenced ShopWork owner and one published traffic result per shop/lead. Equivalent
cache rows are written once per global cache key; conflicting rows fail closed.

Depends on: completed `G-R25`; the current `traffic-enrichment-run-v1` snapshot,
`domain-stage-manifest-v1`, provider source/batch artifact contracts,
PipelineTask fencing, paid DataForSEO ledger, traffic cache uniqueness, and the
visibility-last final transaction.

Observed production finding consumed by this window:

- Run `run_tuMB4xTU8IAYrUCKlo44TjWo` reached 39/39 successful traffic tasks and
  final publication failed after `ledger_evidence_validated` but before
  `publication_input_validated`; therefore no final transaction or lease check
  caused the failure and no traffic row became visible.
- Privacy-safe local validation of its immutable artifacts found one pair of
  distinct shops with the same canonical CrUX identity. Their CrUX REST cache
  rows have the same five-field cache key and are normalized-equivalent; their
  CrUX BigQuery rows have the same five-field cache key and are also
  normalized-equivalent. No per-lead publication key collided.
- `eligibleTrafficIdentities()` already groups lead IDs by provider identity,
  so REST, BigQuery and DataForSEO network inputs are identity-deduplicated.
  It separately stores only one `shopId` per identity, however, causing later
  shops to overwrite earlier ShopWork owners. Final aggregation then rejects
  the repeated global cache rows before it can expose the missing per-shop
  ownership. The same defect class is reachable for DataForSEO hostname
  collisions and for duplicate reuse selections.

Consumes exact outputs:

- `eligibleTrafficIdentities()`, `reserveTrafficIdentities()`,
  `settleTrafficReservations()`, `workClaimsForIdentities()`,
  `enrichDataForSeoSource()`, `enrichCruxRestSource()`,
  `enrichCruxBigQuerySource()`, and `enrichTraffic()`;
- the AWS adapter repository and CrUX REST attempt-marker seam inside
  `processTrafficBatch()`;
- `PrismaRunRepository.readAwsFinalReuseRows()` and
  `publishAwsFinalResults()`;
- `materializeSkippedReuse()` and the existing provider source/batch artifact
  reconciliation in `processFinalAggregation()`; and
- the existing isolated-PostgreSQL harness, bounded-concurrency helper,
  recovery tests, strict artifact parsers, and deterministic Lambda packaging.

Produces exact outputs:

- one sorted, unique `shopId[]` owner set for every provider identity;
- one ShopWork claim/outcome per `(shopId, workType, scopeKey)` while provider
  calls remain one per unique identity and applicable batch/scope;
- deterministic fan-out of one provider result to every associated lead and
  per-shop source artifact;
- one cache write per exact global cache key after normalized-equivalence
  validation;
- duplicate reuse selections shared by several shops resolving to one cache
  read and several owner-scoped publications; and
- a guarded, local-only two-function deployment phase ready for a later
  explicit AWS approval.

Owned files/symbols:

- `email_scraper/src/enrichment/orchestrator.js`: the eight consumed symbols
  above and private helpers used only to construct/aggregate provider owner
  sets;
- `email_scraper/src/aws-pipeline/services/traffic-worker.js`: the adapter
  repository's `claimShopWorkBatch` implementation, shared-identity transient
  fencing, and deterministic CrUX REST attempt representative only;
- `email_scraper/src/prisma-run-repository.js`:
  `readAwsFinalReuseRows()`, `publishAwsFinalResults()`, and new private
  cache-coalescing/selection helpers used only by those methods;
- `email_scraper/scripts/aws-pipeline/create-change-set.js`: add only the
  `provider-identity-fan-in` code-only phase;
- focused tests in `email_scraper/test/traffic-orchestration.test.js`,
  `aws-pipeline-traffic.test.js`, `aws-pipeline-final.test.js`,
  `prisma-run-repository.test.js`,
  `aws-pipeline-final.integration.test.js`, and
  `aws-pipeline-infrastructure.test.js`; and
- completion evidence in `AWS_PIPELINE_EXECUTION_EVIDENCE.md` plus one state
  transition in `ACTIVE_EXECUTION_STATE.md`.

Shared-file permissions: patch the named symbols in place and preserve all
unrelated dirty work and accepted G-R20-through-G-R25 behavior. Do not reset,
restore, stage, commit, or rewrite completed evidence/specification history.

Non-goals/prohibited actions:

- no schema, migration, enum, index, cache key, Shop identity, Lead identity,
  message, artifact, fingerprint, produced-at, lease duration, provider
  timeout, freshness, scoring, visibility, frontend, or infrastructure
  topology change;
- no merging of distinct `Shop`, `RunStore`, `Lead`, PipelineTask, or ShopWork
  rows merely because a provider identity is shared;
- no per-shop DataForSEO request, per-shop CrUX REST call, or repeated origin in
  the BigQuery request; no change to ten-scope DataForSEO batching, REST
  concurrency two, or the single bounded BigQuery query;
- no acceptance of unequal rows under one cache key and no first/last-writer
  selection policy;
- no AWS mutation, deployment, provider call, production-database write,
  queue/DLQ receive/purge/redrive, S3 `runs/` mutation, secret change,
  destructive action, frontend edit, stage, or commit in G-R26; and
- no compatibility behavior for obsolete artifact formats. Only current strict
  contracts are supported.

### 22.2 T1 — retain every per-shop owner behind a provider identity

Change the exact return contract of `eligibleTrafficIdentities()` to:

```js
{
  byDataForSeo: Map<string, string[]>,
  byOrigin: Map<string, string[]>,
  dataForSeoShopIdsByIdentity: Map<string, string[]>,
  originShopIdsByIdentity: Map<string, string[]>
}
```

The first two maps remain provider identity to Lead IDs. The latter maps are
provider identity to all non-null `lead.shop_id` values. For every map, remove
duplicates and sort each value array lexicographically before returning. Map
keys are inserted/consumed in lexicographic order. A qualified lead may appear
under one DataForSEO hostname and one CrUX origin exactly as today; invalid
provider identities remain silently ineligible under the existing strict
normalizers. Do not derive or merge Shop identity here.

Rename the corresponding `enrichTraffic()` context fields exactly to
`dataForSeoShopIdsByIdentity` and `originShopIdsByIdentity`; update every
reachable reference and remove the two singular-map fields. No compatibility
alias remains because all callers are in the owned module.

Change the private helper contract to:

```js
workClaimsForIdentities(shopIdsByIdentity, identities, workType, scopeKey)
```

It returns one unique `{shopId, workType, scopeKey}` per identity/shop pair,
ordered first by sorted identity and then sorted shop ID. An identity with no
shop owner contributes no claim and retains the existing legacy/local behavior.

`reserveTrafficIdentities()` must submit the complete flattened claim list in
one repository batch, require exact positional count and exact claim-key
equality, then return one aggregate reservation per identity. Aggregate in this
fixed order:

1. No owner claims: `legacy`, `networkAllowed:true`.
2. More than one distinct terminal outcome among `completed` and `ambiguous`:
   throw `PipelineInvariantError("PIPELINE_INPUT_CONFLICT")`.
3. Any `ambiguous`: `ambiguous`, `networkAllowed:false`.
4. Any `completed`: `completed`, `networkAllowed:false`; this covers a durable
   or raced shared result and causes the existing cache reread/result fan-out.
5. Any `processing`: `processing`, `networkAllowed:false`.
6. Every claim is `won` with `networkAllowed:true`: `won`,
   `networkAllowed:true`.
7. Every other mixture or missing result: typed input conflict.

`settleTrafficReservations()` retains its existing wait count and duration. A
processing aggregate reclaims/rechecks all owners for that identity, not only
the single busy row. It never performs a provider call unless every owner is
network-authorized or there are no durable owners.

All DataForSEO success/failure `workClaims`, CrUX save claims and CrUX failed
claim settlement use the flattened helper. This changes only owner cardinality:
provider request targets remain the unique sorted keys of `byDataForSeo` or
`byOrigin`. Provider result fan-out remains one row for every Lead ID stored in
those maps.

Mechanical trace:

```text
qualified Leads -> eligibleTrafficIdentities -> identity -> sorted shopId[]
-> flattened claimAwsTrafficWorkBatch input -> aggregate identity reservation
-> one provider decision -> existing per-lead fan-out -> T2 AWS source artifacts
```

Decisive unit tests use two distinct `shopId` and Lead IDs that normalize to
the same hostname and origin. Assert one identity key, two sorted Lead IDs, two
sorted shop owners, two ShopWork claims per source/scope, one DataForSEO target
per scope, one REST call, one BigQuery origin, and two published rows per
source. Reverse lead order must produce identical owner/lead sets and request
identities. Add mixed claim tests for all-won, completed+won, ambiguous+won,
processing+won, contradictory completed+ambiguous, missing result, and a
no-Shop-ID legacy identity.

### 22.3 T2 — AWS shared-identity fencing and deterministic provider evidence

The AWS adapter `claimShopWorkBatch` continues to claim every input through
`claimAwsTrafficWorkBatch()` with the exact shop's PipelineTask and manifest
selection. Group claims by the immutable provider cache key:

```text
source\0identity\0scopeKey\0metricSetKey\0contractVersion
```

Derive the selection through the existing `sourceSelection()` and reject any
missing/mismatched task, plan or selection. If any result in a group is `busy`,
add `<shopId>:<workType>` to `transientSources` for every shop in that group,
not only the busy shop. Thus no sibling source/combined artifact or task
terminal is produced while one shared identity owner is unresolved. Same-task
owned replay remains network-authorized; terminal/raced evidence remains
non-network-authorized under T1.

For `fetchCruxOriginMetrics`, select all manifest plans whose CrUX REST identity
equals `input.origin`, require at least one, sort them by `shopId`, and use the
lowest shop ID and its PipelineTask as the sole representative for the existing
`provider-source-attempt-v1` key/body. Reverse manifest or SQS order must select
the same representative. The marker schema, key grammar and task fingerprint
remain unchanged. One uncertain REST call therefore creates one stable marker
and makes the shared outcome ambiguous for every associated lead without a
second call.

DataForSEO and BigQuery batch identities continue to include one item per shop,
sorted by shop ID, while the external request contains each hostname/origin
once. Per-shop provider source artifacts may consequently contain the same
normalized global cache row; that is intentional recovered evidence and is
coalesced only at T3's final database write. Source artifacts, combined
artifacts, PipelineTasks and work outcomes remain per shop.

Failure/recovery rules:

- any busy owner fences all siblings before artifact writes or task terminal;
- immutable source/batch/attempt evidence is reread before a provider call;
- an already-valid provider/batch artifact fans out without another paid call;
- conflicting shared terminal evidence fails typed input conflict;
- cancellation or Run-lease loss starts no new claims/calls/artifacts and
  cannot publish; and
- retries reconstruct the same representative, batch identity, owner list and
  provider target set from the frozen manifest and durable tasks.

Mechanical trace:

```text
frozen per-shop manifest selections -> cache-key owner groups
-> all-owner claim fence -> unique provider target/origin
-> one attempt/batch protocol -> per-shop source artifacts/tasks
-> T3 cache coalescing plus per-shop settlement
```

Focused AWS tests must prove a two-shop shared-host/origin run performs ten
DataForSEO bulk scope requests rather than twenty, one REST call rather than
two, one BigQuery table lookup/dry-run/live query with one origin, two per-source
artifacts, two combined artifacts, and two terminal tasks. A busy claim for
either shop must produce neither sibling artifacts nor terminals. Reverse
manifest/task/SQS order must produce the same marker key, provider batch IDs,
artifacts and results. Crash/replay after attempt, batch, source and combined
artifact boundaries must not repeat an uncertain paid/provider call.

### 22.4 T3 — coalesce global cache writes and fan reused rows back out

In `publishAwsFinalResults()`, replace only the current unconditional uniqueness
rejection for cache rows. Normalize every input row first with the existing
`trafficCacheRecordToUpsert(cacheId(row), row)`. Group normalized rows by:

```text
source\0identity\0scopeKey\0metricSetKey\0contractVersion
```

For each group:

1. The first row establishes the deterministic cache ID and normalized
   fingerprint `fingerprintJson(row)`.
2. Every later row must have the same ID and fingerprint. Otherwise throw
   `PipelineInvariantError("PIPELINE_INPUT_CONFLICT")` before opening the final
   transaction.
3. Retain exactly one row and sort retained rows lexicographically by the group
   key before `bulkUpsertTrafficCache()`.

Do not compare raw JSON, choose newest/oldest, merge payloads, or permit an
unequal timestamp/state/payload. `writtenCache.length` is compared with the
coalesced unique count. `leadTrafficRows` remain unique by `leadId\0source` and
are never coalesced by provider identity. `workOutcomes` remain unique and
settled per `shopId\0workType\0scopeKey`. All existing after-step boundaries,
15-second transaction timeout, rollback behavior, result fingerprint inputs,
stage completion and visibility-last Run CAS remain unchanged.

In `readAwsFinalReuseRows()` accept repeated `cacheId` selections only across
different shops. Before the query:

- require uniqueness by `shopId\0source\0scopeKey`;
- group by `cacheId` and require every member to agree exactly on `source`,
  `identity`, `scopeKey`, `metricSetKey`, `contractVersion` and
  `cacheFingerprint`;
- sort by `cacheId` then `shopId`; and
- query each unique cache ID once.

Require returned row count to equal unique cache-ID count, validate each row
once against the shared selection contract, snapshot time and fingerprint, and
return unique `trafficRows`. Do not collapse the original per-shop selections:
`materializeSkippedReuse()` continues filtering them by `shopId` and fans the
one cached row into one `LeadTrafficEnrichment` per qualified Lead. Duplicate
selection metadata that disagrees, a missing/expired/post-snapshot row, a
non-qualified Lead, or unequal cache content fails typed input conflict.

This is unchanged atomicity: read-only reuse reconciliation occurs under the
aggregator fence; final cache, traffic, work, profile, diagnostic, score, grant,
stage and Run visibility writes remain one `SAME TRANSACTION`. No new durable
boundary, schema field or artifact is introduced.

Mechanical trace:

```text
per-shop source/reuse evidence -> normalized cache-key groups
-> exact-equivalence certificate -> one global cache upsert
-> unchanged per-lead rows + per-shop work outcomes
-> final visibility CAS -> owner-scoped API results
```

The decisive isolated-PostgreSQL corpus uses two shops and two qualified Leads
sharing one DataForSEO hostname and one CrUX origin. Supply duplicate-equivalent
rows for all ten DataForSEO scopes, REST current and one BigQuery month. Assert
exactly 12 global cache rows, six LeadTrafficEnrichment rows, 24 terminal
ShopWork rows, two linked profiles/Leads, one terminal stage and one visible
completed Run. Inject a different state, payload, fetched time and expiry into
separate duplicate cases; each must throw `PIPELINE_INPUT_CONFLICT`, roll back
all rows and leave `resultsAvailable=false`. Replay the equivalent case and
assert identical cardinalities/fingerprint.

Add the all-reuse variant: both shops select the same 12 cache IDs from the same
frozen evaluation time. Assert 12 cache reads/returned rows rather than 24,
six per-lead publications, no provider adapter call, exact snapshot/fingerprint
checks, and successful replay. Conflicting duplicate selection metadata must
fail before publication.

### 22.5 T4 — guarded deployment preparation, verification and evidence

Add `provider-identity-fan-in` to
`scripts/aws-pipeline/create-change-set.js`. It must use previous values for
DiscoveryWorker, DomainAggregator, LeadWorker, LeadAggregator and Recovery and
may change exactly TrafficWorker and FinalAggregator Code properties. Both are
in-place `AWS::Lambda::Function` modifications with replacement `False`.
Reject any template/IAM/mapping/queue/DLQ/schedule/secret/concurrency/timeout/
memory/environment/topology difference. Infrastructure tests must assert the
exact allowed/forbidden normalized change-set inventory. G-R26 only implements
and tests this guard; it does not invoke AWS.

Run from `email_scraper/` in this order:

```text
node --test test/traffic-orchestration.test.js \
  test/aws-pipeline-traffic.test.js \
  test/aws-pipeline-final.test.js \
  test/prisma-run-repository.test.js \
  test/aws-pipeline-infrastructure.test.js

ALLOW_DATABASE_TESTS=true node -r dotenv/config --test --test-concurrency=1 \
  test/aws-pipeline-final.integration.test.js \
  test/aws-pipeline-traffic.integration.test.js \
  test/aws-pipeline-end-to-end.integration.test.js

ALLOW_DATABASE_TESTS=true npm run test:integration
npm test
npm run build:lambda
npm run measure:lambda
node --test test/aws-pipeline-packaging.test.js
npm run check:secrets
git diff --check
```

Database tests must use `test/helpers/isolated-postgres.js`, a verified
non-production direct endpoint, unique disposable non-`public` schema,
schema-local migration history and `finally` cleanup. They may not use or clean
production/public. Restricted localhost tests are rerun identically with the
ordinary sandbox approval rather than waived.

Packaging acceptance rebuilds all seven Node 24 ZIPs, cold-imports the emitted
artifacts in fresh processes, verifies the exact RHEL Prisma engine,
deterministic repeated file-list hashes, size bounds and forbidden files. The
expected changed deployment closure is TrafficWorker (orchestrator, traffic
service and repository claim paths) and FinalAggregator (final service and
repository publication paths). Any additional changed package hash is a
specification contradiction and a genuine blocker; do not silently expand the
future deployment set.

Acceptance requires all of the following:

1. T1-through-T3 exact collision, fan-in, fan-out, ownership, conflict,
   transient, replay and rollback assertions pass for DataForSEO, REST,
   BigQuery, fresh and reuse paths.
2. Provider cardinality is based on unique provider identities: at most ten
   bulk DataForSEO calls per run, one REST call per unique origin at concurrency
   two, and one latest-table lookup plus one bounded multi-origin BigQuery
   query. Two shops sharing an identity never double a call or paid target.
3. Every current-format shop still has its own ShopWork and PipelineTask fence,
   provider source/combined artifact, LeadTrafficEnrichment and owner-scoped
   final visibility.
4. Equivalent global cache rows write once; unequal duplicates fail before the
   transaction with typed input conflict; reuse reads each cache ID once and
   fans it out without a provider call.
5. The full integration/backend/package/security/diff commands pass with only
   documented guarded skips and no AWS/provider/production/frontend action.
6. Evidence records changed files, exact commands/results, provider/claim/cache
   cardinalities, failure injections, skipped checks/reasons, residual risks,
   external actions (`none`) and preserved dirty work. Then transition only
   `ACTIVE_EXECUTION_STATE.md` to `COMPLETED` and stop at
   `STOP_FOR_DEPLOYMENT_APPROVAL`.

### 22.6 Cross-cutting ledgers and decision-completeness audit

Interface ledger:

| Interface | Locked change | Caller/consumer assertion |
|---|---|---|
| `eligibleTrafficIdentities()` | singular owner maps become sorted identity-to-`shopId[]` maps with the exact names in T1 | all three provider source tests prove two owners/one identity |
| `workClaimsForIdentities()` | flatten every identity/shop pair deterministically | repository fake receives exact per-shop claims |
| reservation aggregate | one identity result using T1's fixed precedence; network only when all owners permit | mixed-outcome matrix and no-call assertions |
| `readAwsFinalReuseRows()` | duplicate cache IDs allowed only for agreeing per-shop selections; returns unique cache rows | two-shop all-reuse PostgreSQL case |
| `publishAwsFinalResults()` | input cache rows coalesce only when normalized-equivalent | 12-cache/6-publication proof and conflict rollback |

Persistence/atomicity: no schema or migration. `TrafficEnrichmentCache` remains
unique by `(source, identity, scopeKey, metricSetKey, contractVersion)`;
`LeadTrafficEnrichment` remains unique by `(leadId, source)`; ShopWork remains
unique by `(shopId, workType, scopeKey)`. The only changed write cardinalities
are one global cache row per key and all per-shop ShopWork claims/outcomes. Final
publication remains one transaction and visibility last.

Message/artifact ledger: `N/A` for contract changes. Existing per-shop source
and combined artifacts, provider batch items, attempt markers, task messages,
keys, fingerprints and durable timestamps remain strict and unchanged.
Equivalent cache rows may occur in several valid per-shop artifacts; their
final coalescing is defined in T3. Missing/corrupt/conflicting immutable
artifacts retain existing typed behavior.

External-call ledger:

| Source | Durable pre-call evidence | External cardinality | Recovery |
|---|---|---|---|
| DataForSEO | every per-shop ShopWork claim plus one paid ledger/batch identity per unique target set/scope | one bulk request per nonempty scope, max ten; duplicate hostnames occur once in targets | succeeded/ambiguous ledger or valid batch artifact forbids another uncertain paid call |
| CrUX REST | every per-shop claim plus one lowest-shop attempt marker per unique origin | one call per unique origin, concurrency two | marker/valid cache or artifact determines replay; uncertain marker makes all sibling results ambiguous |
| CrUX BigQuery | every per-shop claim plus shared batch attempt/result | one table lookup, one dry run and one bounded unique-origin live query | stable request ID and batch artifact fan out to all shops without another query |

Identity/authorization: `Shop.stableKey`, `shopId`, per-run Lead and owner grants
remain distinct. Only provider hostname/origin and global cache keys fan in.
Cache existence still grants no access; each qualified Run Lead and per-shop
manifest selection is required before publication.

Configuration/build/privacy: no new environment read, secret, limit or durable
snapshot field. No raw provider body, credentials, unrestricted HTML, contact
data or customer identifiers may be logged. Tests and evidence report only
counts, source names, safe codes and fingerprints. The existing two-package
production dependency closure and code-only guard are revalidated by T4.

Set-equality certificate:

- reachable owner maps: DataForSEO hostname and CrUX origin, both owned by T1;
- reachable provider callers: DataForSEO bulk, REST and BigQuery, all covered by
  T1/T2 cardinality and recovery tests;
- reachable traffic cache writers: provider commits and final publication;
  provider shapes remain unchanged and final deduplication is owned by T3;
- reachable reuse readers: domain planning and final reuse reconciliation;
  planning already records per-shop selections and T3 owns shared cache IDs;
- reachable terminal/publication transitions: per-shop source/combined/task,
  final cache/traffic/work/stage/Run, all traced above; and
- packaged entry points affected: TrafficWorker and FinalAggregator only.

Forward simulation passed at authoring time: two qualified shops create two
tasks and two owners but one hostname/origin. All owner claims precede the one
provider call. Its one result is represented in each per-shop artifact, tasks
become terminal independently, final aggregation validates both, coalesces the
equivalent global row, settles both ShopWork rows, publishes both Leads and
makes the Run visible last. Busy/cancelled/lost ownership prevents sibling
artifact/terminal work. A crash at every existing durable boundary reuses the
same claim, marker, ledger, batch or immutable artifact without another
uncertain provider call.

Backward simulation passed at authoring time: each visible LeadTraffic row
traces to its qualified Lead, shop-specific manifest selection/task/artifact and
the validated shared provider/cache evidence. The one cache row traces to the
exact normalized provider result and five-field key. Every settled ShopWork row
traces to its own task-fenced claim. Cache reuse traces to one snapshot-valid
row plus each shop's manifest-fingerprinted selection; no shared row grants
cross-owner visibility by itself.

Independent counterexample audit searched the current owner maps, provider
identity grouping, all work-claim helper callers, AWS claim adapter, REST marker
selection, DataForSEO/BigQuery batch construction, provider source cache-row
fan-out, final cache uniqueness check, reuse selection query, cache and
publication unique constraints, and focused/integration tests. It falsified a
cache-only repair because the singular identity-to-shop map would leave sibling
ShopWork absent. T1 and T2 close that owner set before T3 coalesces rows. No
schema, artifact parser, queue contract, scoring function, visibility writer or
frontend caller requires modification.

Decision gate audit:

| Category | Locked choice | Evidence/task | Decisive assertion |
|---|---|---|---|
| Files and symbols | exact ownership in 22.1 | source reachability audit | negative diff outside owned symbols except evidence/state |
| Interfaces/dependencies | sorted identity-to-owner arrays and fixed aggregate | T1 | two-owner mixed matrix |
| Schema/persistence | no migration; global cache/per-lead/per-shop keys unchanged | T3 | 12 cache, 6 traffic, 24 work rows |
| Transactions/atomicity | existing final transaction, coalesce before open | T3 | every conflict/failpoint leaves visibility false |
| Identity/authorization | provider identity fans in; Shop/Lead/owner stays separate | T1-T3 | two owner-scoped Leads published |
| Messages/artifacts | unchanged per-shop contracts | T2 | strict parse and reverse-order fingerprints |
| External calls/cost | calls target unique identities only | T1/T2 | 10 DFS, 1 REST, 1 BQ origin path |
| Failure/retry/recovery | all siblings fence on busy; durable evidence prevents repeats | T2 | boundary replay/no-repeat corpus |
| Configuration/limits | unchanged snapshots, REST concurrency two | T1/T2 | config drift regressions |
| Database transport/isolation | shared isolated helper/direct disposable schema | T3/T4 | schema and cleanup preflight |
| Build/package/runtime | exact current toolchain; two changed package hashes | T4 | seven ZIP build/cold import/inventory |
| Visibility/privacy | visibility-last, counts/fingerprints only | T3/T4 | no partial rows/log leaks |
| Cross-window output | locally verified ZIPs and guarded phase | T4 | evidence plus deployment approval stop |

### 22.7 Preflight Gate Report and readiness certificate

```text
BLOCKERS BEFORE START: none
USER ACTIONS BEFORE START: none
PREDICTABLE FUTURE GATES: F-GR26-DEPLOY — after local G-R26 acceptance, bind the
  exact TrafficWorker and FinalAggregator ZIP SHA-256 values plus unchanged
  template hash into a new approval token. A later explicitly authorized
  deployment may upload only those content-addressed ZIPs outside `runs/`,
  create/inspect/execute only the `provider-identity-fan-in` code change set,
  require UPDATE_COMPLETE and deployed-hash equality, then observe existing Run
  `run_tuMB4xTU8IAYrUCKlo44TjWo` retry final publication. It must make no provider
  call because that Run's traffic tasks/artifacts are already terminal. Any
  third changed Lambda hash, non-Code resource difference, provider-call need,
  or unequal duplicate cache evidence stops as a genuine blocker.
PAID/MUTATING APPROVALS NOT YET GRANTED: A-GR26-DEPLOY — required for the exact
  content-addressed S3 uploads, CloudFormation change-set creation/execution and
  same-run production recovery observation. G-R26 grants none of these actions.
PLANNED USER STOP: after G-R26 local acceptance at STOP_FOR_DEPLOYMENT_APPROVAL
```

Readiness classification: `READY / ASSIGNABLE`. The four authority artifacts
are `AWS_ASYNC_DEPLOYMENT_DIRECTION.md` (locked product contract), this file
(implementation specification), `ACTIVE_EXECUTION_STATE.md` (sole live
assignment), and `AWS_PIPELINE_EXECUTION_EVIDENCE.md` (append-only evidence).
All choices affecting ownership cardinality, provider fan-in, result fan-out,
cache equality, reuse, transaction behavior, tests, package closure and the
future deployment gate are fixed above. The implementation agent chooses only
private helper decomposition and writes the prescribed code.

## 23. G-R27 — G-R26 complete Lambda package-closure correction

This append-only correction supersedes only G-R26 Section 22.5's two-package
assumption and every derivative two-package statement in Sections 22.6 and
22.7. It does not alter or reopen G-R26's provider, ownership, cache,
transaction, artifact, message, test, visibility, or privacy behavior.
`ACTIVE_EXECUTION_STATE.md` alone authorizes execution.

### 23.1 Window header

ID: `G-R27`

Objective: accept the observed emitted-package closure of the behaviorally
complete G-R26 implementation and make its guarded future deployment use all
seven byte-changed Lambda packages without changing any non-Code property.

Depends on: blocked G-R26 with `B-GR26-PACKAGE-CLOSURE`; its passing focused,
38/38 integration, 50-file/425-test backend, package, cold-import, Prisma
engine, secret and diff evidence; and the seven exact ZIP hashes recorded in
`AWS_PIPELINE_EXECUTION_EVIDENCE.md`.

Observed correction input: `PrismaRunRepository` is part of the emitted module
closure of all seven handlers. Required G-R26 repository changes therefore
changed all seven ZIP byte hashes even though only TrafficWorker and
FinalAggregator invoke the corrected business paths. Isolating the methods
would add module boundaries solely to manipulate package hashes and is rejected.
The user's selected decision is to deploy the complete verified closure.

Consumes exact outputs:

- the current G-R26 source and tests without behavioral modification;
- `provider-identity-fan-in` in
  `email_scraper/scripts/aws-pipeline/create-change-set.js`;
- `assertEngineChanges()` as the existing exact seven-function Code plus
  Recovery-dependency inventory validator;
- the deployment manifest containing all seven content-addressed ZIPs and the
  byte-unchanged template; and
- the current G-R26 emitted hashes:
  DiscoveryWorker `dd9fc2646f354000c2d1edd60071114006d85edd64bf4ad5c3ed8f0682c523b2`,
  DomainAggregator `60e7e2b06052ab68d2ec15a499c6084c173acd935015df5e42a1ebfbe4b030cb`,
  LeadWorker `444e546f73a8e31097cbbf0f89078b3172b5f0a1785307b2bff7431a4bb85fa3`,
  LeadAggregator `94b3665e6c2e8b4b9238cd018a41104d77f611b9db39bba81d872f20bf3857f0`,
  TrafficWorker `827248bd164bb1ae6ee5132671970b568a87ce574edd8ab49935886d704c0182`,
  FinalAggregator `3b15a54619bdfefc81db6d3c7fb65ca041ecbd09c0cdadab31dd0916f1a33891`,
  and Recovery `77c9c3027099e9a9c244779e060788fec840e17bea92ffe5a73fa12ac5d0fd4b`.

Produces exact outputs:

- `provider-identity-fan-in` requiring all seven current package key/version
  parameters rather than using five previous values;
- an exact guarded inventory of seven in-place Lambda Code modifications plus
  only the two known Recovery dependency re-evaluations;
- focused/full/package verification proving no G-R26 source or package drift;
  and
- G-R27 completion evidence and a stop for the separate AWS deployment gate.

Owned files/symbols:

- `email_scraper/scripts/aws-pipeline/create-change-set.js`:
  `assertActiveWindow()`, `parameterArguments()`, a new exported
  `assertProviderIdentityFanInChanges()` or an exact wrapper around
  `assertEngineChanges()`, and the `providerIdentityFanIn` guard/description
  branches only;
- `email_scraper/test/aws-pipeline-infrastructure.test.js`: replace the G-R26
  two-function guard case with exact seven-function/dependency cases;
- append-only evidence in `AWS_PIPELINE_EXECUTION_EVIDENCE.md`; and
- one completion transition in `ACTIVE_EXECUTION_STATE.md`.

Shared-file permissions: preserve every G-R26 application source/test change
and all unrelated dirty work. Do not edit `src/`, Prisma schema/migrations,
provider fixtures, Lambda handlers/template, frontend, frozen historical
evidence, or completed window text. Do not reset, restore, stage, commit, or
rewrite history.

Non-goals/prohibited actions:

- no business/source behavior change, refactor or repository-method isolation;
- no package dependency/version/build-tool/handler/native-engine change;
- no template, IAM, queue, DLQ, mapping, schedule state, secret, environment,
  timeout, memory, reserved concurrency, retention, frontend or schema change;
- no AWS mutation, deployment, provider call, production-database write,
  queue/DLQ receive/purge/redrive, S3 `runs/` mutation, destructive action or
  commit in G-R27; and
- no acceptance of fewer/more than the exact seven function Code changes and
  two dependency re-evaluations defined below.

### 23.2 Exact guard correction

`assertActiveWindow()` must permit phase `provider-identity-fan-in` only when
the single live state says `current_window: G-R27`. Remove its G-R26 check; no
dual-window compatibility branch remains.

In `parameterArguments()`, remove `provider-identity-fan-in` from the selective
two-function repair set. With a manifest, supply the current manifest key and
version for every handler in the existing `DEPLOYMENT.handlers` order. Continue
using previous values only for the older phases that already require them.

Create/export exactly:

```js
export function assertProviderIdentityFanInChanges(changes, description)
```

Its accepted normalized inventory is exactly:

| Logical IDs | Action/type/replacement |
|---|---|
| DiscoveryWorker, DomainAggregator, LeadWorker, LeadAggregator, TrafficWorker, FinalAggregator, Recovery | `Modify`, `AWS::Lambda::Function`, `False` |
| RecoveryInvokePermission | `Modify`, `AWS::Lambda::Permission`, `Conditional` |
| RecoverySchedule | `Modify`, `AWS::Events::Rule`, `False` |

For each function require exactly the same three Code details already enforced
by `assertEngineChanges()`: two static parameter references named
`<LogicalId>CodeKey` and `<LogicalId>CodeVersion`, plus one dynamic direct Code
modification, all `RequiresRecreation: Never`, and no other detail. Require the
existing exact dependency details:

- `RecoveryInvokePermission`: one dynamic `ResourceAttribute` detail caused by
  `RecoverySchedule.Arn`, target `SourceArn`, recreation `Always`;
- `RecoverySchedule`: one dynamic `ResourceAttribute` detail caused by
  `Recovery.Arn`, target `Targets`, recreation `Never`.

The implementation may call `assertEngineChanges(changes, description)` and
translate only its error prefix to `Provider-identity-fan-in`; it must not
weaken or duplicate that validator. Route only `providerIdentityFanIn` through
this new function. Update the CloudFormation description to
`Approved G-R27 complete provider identity fan-in package closure`.

The approval packet formula remains unchanged and binds the SHA-256/size/key/
version of all seven ZIPs and the template. The future change-set name remains
content-addressed through the existing helper. Creation and execution remain
impossible in G-R27 because active state has no AWS mutation approval.

Mechanical trace:

```text
observed seven emitted ZIP hashes -> package manifest with seven current values
-> provider-identity-fan-in parameterArguments -> CloudFormation normalized diff
-> exact seven Code + two dependency guard -> later reviewed change set
```

### 23.3 Decisive tests and acceptance

Replace the existing G-R24/G-R25/G-R26 combined two-function test label so
G-R24/G-R25 continue proving their two-function phases and G-R27 independently
proves the seven-package phase.

G-R27 focused cases must assert:

1. Phase parsing succeeds and active state G-R27 is required; G-R26 or any
   other window fails closed.
2. `parameterArguments()` uses current key/version values for all seven handler
   parameters; none uses `UsePreviousValue=true`.
3. The exact nine-resource inventory and details above pass independent of
   input order.
4. Removing any function/dependency, adding any resource, changing action/type/
   replacement, changing a parameter entity, or adding timeout/memory/
   concurrency/environment/IAM/mapping detail fails closed.
5. G-R24 `traffic-publication-repair` and G-R25 `crux-month-repair` remain exact
   two-function guards and their parameter behavior is unchanged.

Run from `email_scraper/`:

```text
node --test test/aws-pipeline-infrastructure.test.js
npm test
npm run build:lambda
npm run measure:lambda
node --test test/aws-pipeline-packaging.test.js
npm run check:secrets
git diff --check
```

Acceptance requires:

- the focused guard corpus and complete backend pass with only documented
  guarded skips;
- all seven ZIP SHA-256 values exactly equal the recorded G-R26 hashes above;
  any changed hash is a blocker because G-R27 owns no application/package code;
- all seven emitted packages cold-import under Node 24, contain exactly the
  required RHEL Prisma engine, retain the existing common file-list hash and
  pass size/forbidden-file checks;
- `git diff` contains no G-R27 change outside the two owned backend files,
  evidence and state;
- no AWS/provider/production/frontend action occurred; and
- append a G-R27 evidence record that incorporates the already-recorded G-R26
  behavioral proof by reference, records the guard/hash checks and changed
  files, then transition state to `COMPLETED`, `accepted_through: G-R27`, and
  `STOP_FOR_DEPLOYMENT_APPROVAL`.

### 23.4 Decision audit, simulations and gates

| Category | Locked choice | Evidence/task | Decisive assertion |
|---|---|---|---|
| Files/symbols | only deployment guard/test plus evidence/state | 23.1/23.2 | negative diff audit |
| Interface | new exact guard; existing phase name | 23.2 | focused exports/parser test |
| Persistence/transactions | N/A: no runtime or database change | G-R26 evidence retained | no `src`/schema diff |
| Identity/artifacts/messages | N/A: G-R26 behavior unchanged | G-R26 evidence retained | prior behavioral hashes/tests |
| External calls/cost | N/A locally; no provider call | active prohibition | external actions `none` |
| Failure/recovery | guard fails closed for any tenth/missing/drifted change | 23.2/23.3 | adversarial inventory cases |
| Configuration/limits | no runtime setting change | normalized diff guard | setting-detail rejection |
| Database isolation | N/A: no database test/write | no runtime edit | command inventory |
| Build/package | all seven current hashes are the deployment unit | observed package proof | exact seven hash equality |
| Visibility/privacy | unchanged; no production action | G-R26 proof | no source/log/evidence payload drift |
| Cross-window output | reviewed local seven-package guard | 23.3 | stop for deployment approval |

Forward simulation passed: the unchanged G-R26 code builds the same seven
packages; a later approved package upload records all seven versions; the phase
passes all seven values to CloudFormation; only seven Code properties and the
two deterministic Recovery dependencies may appear; any other diff is rejected
before execution.

Backward simulation passed: every future deployed function hash traces to one
recorded local ZIP and manifest object version; both dependency re-evaluations
trace only to the changed Recovery ARN. No business behavior, provider call,
database write or infrastructure setting is introduced by this correction.

Independent audit searched the package manifest, handler list, phase parser,
active-window checks, parameter selection, normalized change guards, Recovery
dependency rules, infrastructure tests and recorded emitted hashes. The seven
packages are the closed changed set. Method isolation was rejected because it
adds implementation risk without changing deployed behavior or reducing the
required verification.

```text
BLOCKERS BEFORE START: none
USER ACTIONS BEFORE START: none
PREDICTABLE FUTURE GATES: F-GR27-DEPLOY — after local acceptance, generate the
  approval token from the exact seven recorded ZIP hashes and current unchanged
  template. On later explicit authorization, upload only those content-addressed
  objects outside `runs/`, create/review the exact nine-resource change set,
  execute it, require UPDATE_COMPLETE and seven deployed-hash matches, then
  observe existing terminal-artifact Run `run_tuMB4xTU8IAYrUCKlo44TjWo` retry
  final publication without a provider call. Any other resource/detail, hash
  drift or provider-call requirement stops.
PAID/MUTATING APPROVALS NOT YET GRANTED: A-GR27-DEPLOY — this user decision
  selected the seven-package design but did not authorize AWS uploads,
  change-set creation/execution or production recovery.
PLANNED USER STOP: after G-R27 local acceptance at STOP_FOR_DEPLOYMENT_APPROVAL
```

Readiness: `READY / ASSIGNABLE`. G-R27 resolves
`B-GR26-PACKAGE-CLOSURE` without delegating any package, guard, inventory,
dependency, verification or deployment choice.

## 24. G-R28 — run-isolated provider work and guarded deployment

### 24.1 Objective and locked decisions

G-R28 removes cross-run execution ownership from the globally unique
`ShopWork(shopId, workType, scopeKey)` row without a schema change. `ShopWork`
remains non-authoritative, last-writer bookkeeping and a global cache/profile
locator. The current run's `PipelineTask`, stage/run lease, immutable S3 keys,
provider ledgers and fenced publication are the only execution authorities.

Locked behavior:

- A valid compatible completed global profile/cache remains reusable.
- Otherwise every current run owns and completes its own provider work; another
  run's `ShopWork` owner/state never returns `busy`, inherited `ambiguous`, or a
  terminal result to the current run.
- DataForSEO paid-ledger request fingerprints include exactly `runId`,
  `generation`, and the existing provider request fingerprint. The provider
  request body and run-wide batching remain unchanged.
- Final publication requires each outcome's `pipelineTaskId` to belong to the
  publishing run. It settles `ShopWork` only when that row still names the
  current task; a missing or foreign bookkeeping row cannot block publication.
- Concurrent newly discovered lead profiles use first-completed-writer
  semantics for the global reusable profile; every run still publishes its own
  private `Lead` and run history from its own fenced artifacts.
- Concurrent cache misses may repeat one provider execution per run. No
  cross-run paid-call deduplication is claimed. Compatible global cache rows may
  be last-writer-wins, while private run artifacts/results remain separate.
- Discovery and all aggregators already use run-scoped tasks/stages/artifacts;
  they receive no ownership change.

### 24.2 Exact ownership

Application files:

- `src/aws-pipeline/core/canonical.js`: export
  `awsDataForSeoRequestFingerprint({ runId, generation,
  providerRequestFingerprint })` using contract
  `aws-dataforseo-run-request-v1` and deterministic canonical fingerprinting.
- `src/aws-pipeline/services/traffic-worker.js`: replace only the DataForSEO
  descriptor fingerprint passed to paid-ledger operations with that run-scoped
  fingerprint.
- `src/aws-pipeline/services/final-aggregator.js`: reconstruct the identical
  run-scoped fingerprint for ambiguous DataForSEO ledger reconciliation.
- `src/prisma-run-repository.js`: apply the lead/traffic claim and final
  publication rules in 24.1; retain task/stage/run validation and transaction
  fences; do not add a migration.

Exact behavioral tests are owned in
`test/aws-pipeline-contracts.test.js`,
`test/aws-pipeline-lead.integration.test.js`,
`test/aws-pipeline-traffic.integration.test.js`, and
`test/aws-pipeline-final.integration.test.js`. They must prove fingerprint
stability and run separation, two running runs independently owning the same
lead identity, 1,000 mixed traffic claims ignoring foreign bookkeeping owners,
and final publication succeeding after a competing run replaces the global
bookkeeping owner.

Deployment files are limited to
`scripts/aws-pipeline/create-change-set.js` and
`test/aws-pipeline-infrastructure.test.js`. Phase `run-isolation-repair` requires
`current_window: G-R28`, supplies all seven current Lambda package versions,
and accepts exactly seven in-place `AWS::Lambda::Function` Code modifications
plus the deterministic `RecoveryInvokePermission` and `RecoverySchedule`
dependency re-evaluations already enforced by `assertEngineChanges()`. Any
other resource, property, replacement or detail fails closed.

Non-goals: no schema/migration, provider request shape, batch size, cache
freshness, queue/mapping/concurrency, IAM, environment, secret, timeout, memory,
frontend, S3 retention, production data, topology or historical compatibility
change. Do not receive/purge/redrive queues, mutate `runs/`, call providers,
write production Neon rows, or create a run.

### 24.3 Verification, deployment and stop

Required local acceptance:

```text
node --test --test-concurrency=1 test/aws-pipeline-contracts.test.js test/aws-pipeline-traffic.test.js test/aws-pipeline-final.test.js test/prisma-run-repository.test.js
ALLOW_DATABASE_TESTS=true node -r dotenv/config --test --test-concurrency=1 test/aws-pipeline-lead.integration.test.js test/aws-pipeline-traffic.integration.test.js test/aws-pipeline-final.integration.test.js
ALLOW_DATABASE_TESTS=true npm run test:integration
node --test test/aws-pipeline-infrastructure.test.js
npm test
npm run build:lambda
npm run measure:lambda
node --test test/aws-pipeline-packaging.test.js
npm run check:secrets
git diff --check
```

Database commands require the existing isolated disposable-schema helper and
must never target production or `public`. Acceptance requires all assertions,
the complete recovery corpus, package cold imports/native-engine checks,
security checks and exact diff hygiene to pass.

The user explicitly authorized the exact G-R28 deployment on 15 August 2026.
After local acceptance, generate the content-addressed approval token from the
seven ZIPs and unchanged template; upload only those deployment objects outside
`runs/`; create and review the `run-isolation-repair` change set; execute only
if its normalized inventory is the exact nine resources above; require stack
`storesignal-production-pipeline` in `ap-south-2` to reach `UPDATE_COMPLETE`;
and compare all seven deployed `CodeSha256` values with the local packages.
No provider smoke call or agent-created production run is authorized.

Record local and deployment evidence append-only in
`AWS_PIPELINE_EXECUTION_EVIDENCE.md`, update only
`ACTIVE_EXECUTION_STATE.md`, then stop at
`STOP_AFTER_DEPLOYMENT_VERIFICATION`.

```text
BLOCKERS BEFORE START: none
USER ACTIONS BEFORE START: none
PREDICTABLE FUTURE GATES: none inside the exact approved deployment
PAID/MUTATING APPROVAL: G-R28 exact code-only AWS deployment granted
PLANNED USER STOP: after verified deployment
```

Readiness: `READY / ASSIGNABLE`.


## 25. G-R29 — atomic traffic/final lease exclusion

### 25.1 Objective and locked behavior

G-R29 closes the remaining race between the Traffic Worker run-wide lease and
the Final Aggregator lease for the same `traffic_crux` stage. Both claims must
lock the deterministic traffic `PipelineStage` row first and the `Run` row
second in one PostgreSQL transaction. Exactly one side may own a live lease:

- a live Traffic Worker run lease makes `claimAggregator()` return `busy`;
- a live Final Aggregator stage lease makes `claimAwsRunLease()` return `busy`;
- an expired lease does not block the other side; and
- simultaneous claims cannot deadlock and produce exactly one `owned` result
  and one `busy` result.

The existing 60-second Traffic Worker and 120-second Final Aggregator lease
durations, recovery behavior, task/provider protocols, batching, S3 artifacts,
publication transaction, and error contracts remain unchanged. No schema,
migration, provider, queue, mapping, concurrency, IAM, secret, frontend,
retention, or topology change is permitted.

### 25.2 Exact implementation and proof

Application ownership is limited to `email_scraper/src/prisma-run-repository.js`:

1. Import and derive `pipelineStageId(runId, "traffic_crux", generation)`.
2. Inside `claimAwsRunLease()`, after selecting the isolated schema, acquire
   `FOR UPDATE` on that exact `PipelineStage` row, then acquire `FOR UPDATE` on
   the exact `Run` row. Missing rows or identity/generation mismatch remain
   `PIPELINE_INPUT_CONFLICT`.
3. Before acquiring or replaying a Traffic Worker lease, return `{ outcome:
   "busy" }` when the traffic stage is `aggregating` and its aggregator lease
   expiry is later than `now`.
4. Preserve all existing run-lease validation, idempotent same-token replay,
   attempt increment, renewal, and release behavior.

`email_scraper/test/aws-pipeline-traffic.integration.test.js` must use two
independent Prisma clients against one disposable isolated schema to prove:

- Final Aggregator owned first -> Traffic Worker claim is `busy`.
- Traffic Worker owned first -> Final Aggregator claim is `busy`; after release,
  the Final Aggregator can own the lease.
- Truly simultaneous Traffic Worker and Final Aggregator claims settle without
  deadlock as exactly one `owned` and one `busy`.

No production database write or provider call is part of acceptance.

### 25.3 Verification, deployment, and stop

Run the focused traffic/coordinator unit and isolated PostgreSQL integration
tests, then the complete database integration suite, full backend suite, all
seven Lambda builds/measurements/cold imports, packaging check, secret scan,
and `git diff --check`.

Because `PrismaRunRepository` is bundled into every handler, deployment must
publish all seven Lambda packages even though only the Traffic Worker invokes
the changed method. Add a fail-closed `traffic-final-lease-exclusion` deployment
phase that is valid only for `current_window: G-R29`; it must accept exactly the
same seven in-place Lambda `Code` updates plus only the deterministic
`RecoveryInvokePermission` and `RecoverySchedule` dependency re-evaluations
allowed by G-R28. Any other resource, property, replacement, or detail blocks
execution.

The user's 15 August 2026 instruction "alright do it" authorizes this exact
implementation and code-only deployment. Before mutation, disclose the seven
Lambda code updates and the two possible dependency re-evaluations. Upload only
content-addressed deployment objects outside `runs/`, create and inspect the
guarded change set, execute only the exact normalized inventory, require
`UPDATE_COMPLETE`, compare all seven deployed `CodeSha256` values with local
packages, append evidence, update `ACTIVE_EXECUTION_STATE.md`, and stop. No
provider smoke call or agent-created run is authorized.

```text
BLOCKERS BEFORE START: none
USER ACTIONS BEFORE START: none
PAID/MUTATING APPROVAL: G-R29 exact code-only AWS deployment granted
PLANNED USER STOP: after verified deployment
```

Readiness: `READY / ASSIGNABLE`.

## 26. G-R30 — maximum-cardinality final-publication reliability

### 26.1 Finding, objective, and authority boundary

The 16 August 2026 parent verification reran the required four-file isolated
PostgreSQL corpus. Twenty-eight of twenty-nine tests passed. The existing
1,000-domain/12,000-work-outcome publication case reached
`scores_finalized` after 14,291 ms and `grants_written` after 14,414 ms, then
Prisma closed the interactive transaction before stage completion under the
current 15,000 ms hard timeout. The identical maximum case passed when rerun
alone. This proves timing-sensitive maximum-cardinality acceptance rather than
a deterministic data or ownership conflict.

G-R30 makes final publication reliable at the already-supported maximum without
adding any workload-specific production branch. It reduces unnecessary row
projection and score-mapping work, retains the 15-second performance target,
and separates that target from a 30-second transaction safety deadline so a
temporary latency excursion does not roll back otherwise valid publication.

This is a local implementation and verification window only. It authorizes no
AWS mutation, package upload, deployment, provider call, production database
write, queue action, S3 mutation, secret/configuration change, frontend edit,
schema migration, destructive action, staging, or commit. Because the changed
repository module is bundled into every handler, a later deployment requires
all seven newly measured Lambda packages and a separate explicit approval.

### 26.2 Locked implementation

Owned application file:

- `email_scraper/src/prisma-run-repository.js`

Owned test files:

- `email_scraper/test/prisma-run-repository.test.js`
- `email_scraper/test/aws-pipeline-final.integration.test.js`

No other application, test, schema, migration, infrastructure, frontend, or
provider file is owned. If implementation requires another file, stop at the
ownership boundary and report the exact contradiction.

#### G-R30-T1 — explicit generic work-row projections

Inside `PrismaRunRepository.publishAwsFinalResults()` replace the two broad raw
SQL projections without changing their predicates, order, locks, cardinality,
or reconciliation:

1. The traffic `lockedWork` query must return only:
   `id`, `shopId`, `workType`, `scopeKey`, `state`, `processingRunId`,
   `processingPipelineTaskId`, and input `ordinal`.
2. The lead `profileWorkRows` query must return only:
   `id`, `shopId`, `state`, `processingRunId`,
   `processingPipelineTaskId`, and input `ordinal`.

The projection applies identically at every cardinality. Do not add a domain,
row-count, chunk-size, or threshold branch. Preserve `FOR UPDATE`, exact input
ordinal ordering, run/task fencing, enum comparisons, target-state mapping,
duplicate behavior, and row-count reconciliation.

#### G-R30-T2 — narrow score preparation inside the atomic transaction

Keep `finalizePersistedLeadScoresV3()` inside the final publication transaction.
Do not move scoring or lead reads outside the transaction: current `Lead` rows
have no mutation version or scoring-input fingerprint with which to reject a
stale precomputed result.

Within `finalizePersistedLeadScoresV3()`:

1. Retain one ordered `Lead.findMany({ where: { runId }, orderBy: { id:
   "asc" } })` because the complete stored rows are still required by the
   unchanged final result fingerprint and owner-grant path.
2. Restrict the scoring `LeadTrafficEnrichment.findMany()` to sources
   `dataforseo` and `crux_rest`, ordered by `leadId` then `source`, and select
   only `leadId`, `source`, `state`, `contractVersion`, and
   `normalizedPayload`. CrUX BigQuery is independently published but is not a
   v3 scoring input.
3. Replace full `serializeLead()` conversion for scoring with one private
   deterministic mapper that returns exactly:
   `id`, `status`, `resolved_domain`, `relevance_score`,
   `shopify_confidence`, `identity_confidence`, `email`, `phone`, and
   `contact_url` from the corresponding stored fields.
4. Before scoring, validate each stored row's existing score state with
   `assertLeadScoreState()` using its exact stored `status`, `pipelineVersion`,
   `scoringVersion`, `leadScore`, and `scoreBreakdown`.
5. Preserve `finalizeLeadScoresV3()` as the sole scoring algorithm. Require its
   output length, order, ID, and status to match the ordered stored rows.
6. Replace the full `leadRecordToCreate()` round trip for score updates with
   direct construction of only `id`, `pipelineVersion`, `scoringVersion`,
   `leadScore`, and `scoreBreakdown`. Require pipeline version `2`, scoring
   version `3`, and validate every resulting score tuple with
   `assertLeadScoreState()` before the existing set-based update.
7. Preserve the existing set-based `UPDATE`, exact updated-ID/cardinality
   reconciliation, `captureLeads` merge, score semantics, and final result
   fingerprint input.

No score formula, score evidence, public lead field, ordering, traffic-source
contract, visibility boundary, or persisted output may change.

#### G-R30-T3 — separate safety timeout from performance acceptance

Change only the hard interactive-transaction timeout of
`publishAwsFinalResults()` from `15_000` to `30_000` ms. Keep `maxWait: 5_000`.
Do not make either value configurable and do not change Lambda timeout, lease
duration, queue visibility, retry, memory, concurrency, batching, or any other
transaction timeout.

The maximum-publication behavioral test retains a strict elapsed publication
requirement below 15,000 ms. The 30,000 ms value is a rollback safety ceiling,
not a relaxed performance claim.

#### G-R30-T4 — deterministic repeated maximum proof

Refactor only the existing test beginning at
`test/aws-pipeline-final.integration.test.js`'s
`G-R20 publishes 1,000 domains and 12,000 work outcomes...` case into a local
trial helper and execute three consecutive trials. Each trial must:

- create and verify its own disposable isolated schema;
- use a unique run, stage, task, work, lead, and schema identity;
- construct exactly 1,000 domains, 1,000 terminal traffic tasks, 12 external
  work outcomes per domain, 1,000 lead-work outcomes, and the existing mixed
  terminal-state distribution;
- start timing immediately before `publishAwsFinalResults()`;
- record every existing `afterStep` timestamp;
- require publication elapsed time below 15,000 ms;
- require `resultsAvailable` to remain false before the final visibility write;
- retain every existing 12,000-work, 1,000-profile, score-version, owner-grant,
  terminal-stage, result-fingerprint, state-count, and cleanup assertion; and
- on failure report the trial ordinal and complete step timing array without
  payload or credential data.

The existing nonempty rollback/failpoint test remains unchanged and must pass.
Add or update focused repository assertions proving the exact score output and
score-state validation remain unchanged. A source-text-only assertion is not
acceptance proof.

### 26.3 Invariants and non-goals

G-R30 must preserve:

- one atomic final publication transaction;
- task/stage/run and aggregation-token fencing;
- all-or-nothing work settlement, scoring, grants, stage completion, result
  fingerprint, and visibility;
- first-terminal and replay behavior;
- current-run execution authority and G-R29 lease exclusion;
- provider call cardinality and cost behavior;
- exact public results and score semantics; and
- rollback at every existing injected failpoint.

Do not add volume-specific logic, partial publication, chunk commits,
pre-publication visibility, a new durable field/table, a migration, an external
cache, a background finalization stage, or historical-format compatibility.

### 26.4 Required checkboxes and verification

Implementation:

- [ ] `G-R30-P1` Revisions, G-R29 acceptance, ownership, dirty work, isolated
  test database, and non-production identity are verified and recorded.
- [ ] `G-R30-T1` Both work-row projections contain only the locked columns and
  preserve their predicates, locks, order, and reconciliation.
- [ ] `G-R30-T2` Narrow scoring preparation preserves exact v3 outputs and stays
  inside the atomic transaction.
- [ ] `G-R30-T3` Only the final-publication hard timeout becomes 30,000 ms; the
  15,000 ms performance target remains.
- [ ] `G-R30-T4` Three maximum-cardinality trials and the unchanged rollback
  corpus pass with exact activation and cardinality evidence.

Run from `email_scraper/`:

```text
node --test --test-concurrency=1 test/prisma-run-repository.test.js
ALLOW_DATABASE_TESTS=true node -r dotenv/config --test --test-concurrency=1 test/aws-pipeline-final.integration.test.js
ALLOW_DATABASE_TESTS=true node -r dotenv/config --test --test-concurrency=1 test/aws-pipeline-end-to-end.integration.test.js test/aws-pipeline-final.integration.test.js test/aws-pipeline-traffic.integration.test.js test/pipeline-coordinator-repository.integration.test.js
ALLOW_DATABASE_TESTS=true npm run test:integration
npm test
npm run build:lambda
npm run measure:lambda
node --test test/aws-pipeline-packaging.test.js
npm run check:secrets
git diff --check
```

Database tests MUST use the existing isolated disposable-schema harness with a
test URL proven distinct from production. Restricted localhost test failures
must be rerun identically under the approved sandbox procedure.

Acceptance:

- [ ] `G-R30-V1` Focused repository behavior and score semantics pass.
- [ ] `G-R30-V2` Three consecutive 1,000-domain/12,000-outcome trials each
  publish below 15,000 ms with no transaction expiry.
- [ ] `G-R30-V3` The complete four-file 29-test corpus passes in one invocation,
  including all 16 recovery boundaries, rollback, collation, 1,000 claims, and
  G-R29 mutual exclusion.
- [ ] `G-R30-V4` The complete isolated integration and backend regression suites
  pass with only documented guarded skips/reruns.
- [ ] `G-R30-V5` All seven packages build, measure, cold-import, contain the
  required native runtime material, and receive newly recorded hashes.
- [ ] `G-R30-V6` Secret scan, package inspection, diff hygiene, privacy, and
  authorized-write-scope checks pass.
- [ ] `G-R30-V7` No AWS, provider, production database, frontend,
  infrastructure, deployment, secret, destructive, stage, or commit action
  occurred.
- [ ] `G-R30-H1` Append exact commands/results, step timings, changed symbols,
  seven package hashes, skips, residual risks, and external-action boundary to
  `AWS_PIPELINE_EXECUTION_EVIDENCE.md`.
- [ ] `G-R30-H2` Update `ACTIVE_EXECUTION_STATE.md` only to local completion and
  stop at `STOP_FOR_DEPLOYMENT_APPROVAL`; do not begin or deploy a successor.

### 26.5 Decision audit and readiness

| Category | Locked choice | Evidence | Task | Decisive assertion |
|---|---|---|---|---|
| Files/symbols | Repository final publication/finalizer plus two named tests | Current source and failure trace | T1-T4 | Scope/diff closure |
| Interfaces | No public signature or payload change | Existing callers and artifacts | T1-T3 | Existing contract suites unchanged |
| Persistence/atomicity | One transaction; no schema; identical durable outputs | Publication and rollback tests | T1-T3 | Rollback and visibility proof |
| Identity/authority | Existing run/task/stage/token fences | G-R28/G-R29 | T1-T4 | Existing concurrency corpus |
| External calls/cost | No change and none during acceptance | Final publication has no provider call | All | Provider regressions/full suite |
| Failure/recovery | 30-second safety timeout; 15-second target; retry remains atomic | Fresh 28/29 trace and isolated pass | T3-T4 | Repeated maximum and recovery corpus |
| Scale | Generic projections; three exact maximum trials | 1,000/12,000 observed failure | T1-T4 | V2-V4 |
| Runtime/package | Shared repository changes all seven bundles | G-R27 package closure | T2-T3 | V5 |
| Cross-window output | Seven local package hashes and local acceptance only | This section | H1-H2 | Stop for deployment approval |

Forward simulation: every cardinality uses the same projections and score
algorithm. At maximum scale, final publication validates ownership, locks and
settles the complete work set, validates and updates all scores, writes grants,
completes the stage, fingerprints the complete durable result, and flips
visibility in one transaction. A latency excursion above the 15-second target
is observable but has up to 30 seconds before rollback; acceptance still fails
the target until optimization proves all three trials below it.

Backward simulation: every published score traces to the unchanged pure v3
scorer and evidence-backed traffic rows; every final fingerprint member traces
to the same complete stored lead/traffic/audit/diagnostic arrays; every settled
work row traces to an exact current-run task; and public visibility traces to
the final fenced update after stage completion.

No payload shape, schema, provider result, identity, formula, transaction
boundary, or deployment action is unknown. G-R30 is decision-complete and
`READY / NOT ASSIGNED`. Assignment requires a separate active-state transition;
this authoring change alone grants no implementation or deployment authority.

## 27. G-R31 — maximum-publication performance-contract correction

### 27.1 Decision and authority

Parent verification of G-R30 reproduced a safe, atomic maximum-cardinality
publication whose third trial reached `before_run_visibility` after 18,473 ms.
The user explicitly selected a 25,000 ms performance acceptance target on
16 August 2026. The 30,000 ms Prisma interactive-transaction timeout remains
the hard rollback ceiling. This preserves at least 5,000 ms of safety margin
between acceptance and forced rollback.

G-R31 changes no production code, payload, schema, persistence behavior,
transaction boundary, provider behavior, package bytes, or AWS resource. It
owns only:

- `email_scraper/test/aws-pipeline-final.integration.test.js`;
- this append-only specification section;
- `AWS_PIPELINE_EXECUTION_EVIDENCE.md`; and
- `ACTIVE_EXECUTION_STATE.md`.

No AWS mutation, deployment, provider call, production database write, queue
action, S3 mutation, secret/configuration change, frontend edit,
infrastructure edit, destructive action, staging, or commit is authorized.

### 27.2 Exact implementation and proof

- [ ] `G-R31-T1` In the existing three-trial maximum-publication test, change
  only its displayed/tested performance target from 15,000 ms to 25,000 ms.
  Retain three consecutive trials, exact 1,000-domain/12,000-work cardinality,
  independently isolated schemas, all existing atomicity/cardinality/cleanup
  assertions, complete failure timings, and the 30,000 ms production hard
  transaction timeout.
- [ ] `G-R31-V1` The complete four-file 29-test PostgreSQL corpus passes in one
  unchanged invocation, and all three maximum trials are below 25,000 ms.
- [ ] `G-R31-V2` `npm test`, `npm run check:secrets`, backend/root
  `git diff --check`, and exact changed-file scope pass. Database-guarded skips
  remain expected because V1 executes the required isolated database cases.
- [ ] `G-R31-V3` The seven already rebuilt G-R30 package SHA-256 values remain
  unchanged because G-R31 modifies no bundled source. Rebuilding is not
  required; hash the existing packages and compare them to G-R30 evidence.
- [ ] `G-R31-H1` Append exact commands, results, all three elapsed times, changed
  files, skips, residual risk, and the no-external-action boundary to the
  evidence log.
- [ ] `G-R31-H2` On pass, record `G-R31` as completed and accepted-through in
  the active state, then stop at `STOP_FOR_DEPLOYMENT_APPROVAL`. On any trial at
  or above 25,000 ms, keep G-R31 unaccepted and stop with the timing trace.

Run from `email_scraper/`:

```text
ALLOW_DATABASE_TESTS=true node -r dotenv/config --test --test-concurrency=1 test/aws-pipeline-end-to-end.integration.test.js test/aws-pipeline-final.integration.test.js test/aws-pipeline-traffic.integration.test.js test/pipeline-coordinator-repository.integration.test.js
npm test
npm run check:secrets
sha256sum dist/lambda/*.zip
git diff --check
```

G-R31 is decision-complete and authorized only by an active-state assignment.
