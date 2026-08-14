# AWS Pipeline Corrective Execution Evidence

This is the append-only evidence log for corrective Windows G-R7 and later.
It records what occurred but never authorizes work or changes product behavior.
Live authority is `ACTIVE_EXECUTION_STATE.md`; the frozen specification is
Section 10A of `FINAL_LAMBDA_SQS_S3_MIGRATION_EXECUTION_PLAN.md`.

## Parent corrective authoring record — 13 August 2026

- Accepted implementation remains G10. G11-G13 acceptance was rescinded by the
  independent findings in Section 11.10A of the frozen specification.
- The parent inspected the current backend at commit
  `1380dca3eac1074738a4189f02ecd4fcf8c51492` and authored G-R7, G-R8, and G-R9.
- The committed implementing-agent statement that no commit occurred was
  false: local `HEAD` and `origin/main` both resolved to `1380dca` (`G11-14`).
- The correction requires no AWS, provider, production-database, frontend,
  infrastructure, deployment, staging, cutover, or destructive action.
- No implementation code, AWS resource, provider, or database was changed by
  corrective authoring.

Future window reports must append changed files, migrations, exact commands and
outcomes, behavioral assertions, PostgreSQL schema evidence, package
measurements, skipped checks/reasons, external actions, preserved dirty work,
residual risks, and the exact active-state transition.

## G-R7 acceptance evidence — 13 August 2026

- Changed backend files: `src/aws-pipeline/contracts/artifacts.js`,
  `src/aws-pipeline/handlers/traffic-worker.js`,
  `src/aws-pipeline/services/traffic-worker.js`,
  `src/aws-pipeline/traffic/durable-protocol.js`, deletion of the unreachable
  `src/aws-pipeline/traffic/source-executors.js`, and the named traffic,
  contract, final-regression, packaging, and PostgreSQL tests. No schema or
  migration changed.
- Real path: `processTrafficBatch` retains `enrichTraffic` and exposes only the
  seven frozen adapter seams. The one-domain service proof calls all adapters;
  the 52-domain proof calls DataForSEO 10 times, REST 52 times, and BigQuery
  table/dry/live once each regardless of trigger membership.
- Durable proof: strict per-scope `requestEvidence` links DataForSEO source
  artifacts to deterministic batches and ledgers. The disposable PostgreSQL
  test crashes after the first paid batch but before ledger success, expires the
  Run lease, restarts, reconciles the batch, completes all ten ledgers, and
  proves ten total paid calls rather than eleven; every evidence fingerprint
  equals its ledger `resultFingerprint` and the task is terminal.
- Recovery proof: REST attempt-marker replay makes a lost status-0 response
  ambiguous without a second adapter call; BigQuery dry-run transient work is
  nonterminal on early leases; marker month/bytes and 14:59.999/15:00.000 rules,
  batch replay, attempts 1-4, configuration drift, cancellation, competing
  owner, terminal replay, renew/release/check order, and every named artifact,
  terminal, release, and check boundary are covered. Exceptions emit only
  nonterminal `retryable`; the Lambda handler fails `busy|retryable` records.
- Additional corrections found by decisive tests: deterministic batch sorting
  now uses the strict artifact code-point order; REST errors use the locked
  status mapping; source publication reconciles the orchestrator's
  `stableLeadId()` rather than assuming the persisted row ID is identical.
- Commands/outcomes: focused traffic/runtime/contract suites passed; current
  provider/orchestrator regressions passed; the isolated PostgreSQL traffic
  test passed in a direct disposable schema; `npm test` passed 45 files with
  only the two documented restricted-listener failures, and their identical
  approved rerun passed 16/16; `npm run build:lambda`, `npm run
  measure:lambda`, `npm run check:secrets`, and `git diff --check` passed.
- Traffic package: Node `v24.14.1`, ZIP 32,070,823 bytes, unpacked 84,095,776
  bytes, Prisma engine present, cold import 370.993 ms, RSS 102,883,328 bytes,
  RSS delta 57,294,848 bytes, file-list hash
  `a27c435df9624ef6618e6318b5329296fa5380c536416a5e6d918cfed71338a1`.
- Skipped checks: none. The frozen command names
  `enrichment-orchestrator.test.js`, `dataforseo-adapter.test.js`, and
  `crux-adapter.test.js` do not exist; their current repository equivalents
  `traffic-orchestration.test.js`, `dataforseo-enrichment.test.js`, and
  `crux-enrichment.test.js` passed.
- External actions: no AWS read/mutation, live or paid provider call,
  production database, frontend, infrastructure, deployment, staging,
  cutover, destructive action, staging, or commit. Existing root relocation
  state was preserved.
- Acceptance: G-R7 passed. Active state advances from G-R7 `IN_PROGRESS` to
  G-R8 `READY`; accepted implementation advances from G10 to G-R7.

## G-R8 acceptance evidence — 13 August 2026

- Changed backend files: `src/aws-pipeline/services/final-aggregator.js`,
  `src/prisma-run-repository.js`, `test/aws-pipeline-final.test.js`, and
  `test/aws-pipeline-final.integration.test.js`; narrow G-R7 source-contract
  fixture support remains in the already recorded files. No schema/migration.
- Artifact proof: final aggregation directly validates every succeeded
  DataForSEO batch reference and its run/generation/scope/request/content/shop
  identity, collapses identical references, rejects conflicts, and supplies a
  sorted unique ledger-evidence set without S3 listing. Failed/ambiguous rows do
  not read a batch; reused/not-dispatched rows create no ledger input.
- Atomicity proof: `publishAwsFinalResults` locks the Run's paid ledgers with
  `FOR UPDATE`, requires exact evidence set/state/fingerprint equality, then
  performs all publication writes in the existing transaction. The nine exact
  `afterStep` hooks execute after their groups; stage completion precedes
  `before_run_visibility`, and Run visibility remains the last mutation.
- PostgreSQL proof: the retained zero-task case passes separately. The new
  nonempty disposable-schema case contains a qualified Lead, completed traffic
  task, reusable profile, three source publications, succeeded paid ledger and
  Run owner. Each of nine failpoints rolls back traffic, grants, stage state and
  visibility; success publishes three source rows, preserves the paid
  fingerprint, grants only the Run owner, completes the stage and exposes the
  Run. Independent result fingerprint checks remain in the zero-task regression.
- Commands/outcomes: final/traffic focused suites passed; serializer, CSV,
  score-v3 and Prisma repository suites passed; both isolated PostgreSQL final
  cases passed; `npm test` passed 45 files except the two documented restricted
  listeners, whose approved identical rerun passed 16/16; build, measurement,
  secret scan and diff hygiene passed.
- Final package: Node `v24.14.1`, ZIP 31,905,583 bytes, unpacked 83,245,787
  bytes, Prisma engine present, cold import 285.761 ms, RSS 99,545,088 bytes,
  RSS delta 53,964,800 bytes, file-list hash
  `a27c435df9624ef6618e6318b5329296fa5380c536416a5e6d918cfed71338a1`.
- External actions: no AWS/provider/production database/frontend/IaC/deploy/
  staging/cutover/commit action. Existing relocation state preserved.
- Acceptance: G-R8 passed. Active state advances to G-R9 `READY`; accepted
  implementation advances to G-R8.

## G-R9 acceptance evidence — 13 August 2026

- Changed backend files: `src/aws-pipeline/services/traffic-worker.js`,
  `src/aws-pipeline/services/final-aggregator.js`,
  `test/aws-pipeline-runtime-adapters.test.js`,
  `test/aws-pipeline-recovery.test.js`,
  `test/aws-pipeline-end-to-end.integration.test.js`,
  `test/helpers/aws-pipeline-e2e-harness.js`, and the narrow final regression
  assertion in `test/aws-pipeline-final.test.js`. No schema or migration.
- Positional recovery proof: dispatcher tests preserve duplicate logical IDs in
  positional results; recovery correlates two identical item IDs in different
  stages by returned index, records both or only the later success exactly, and
  rejects missing, out-of-range, duplicate-index, cardinality, and item-ID drift
  before recording dispatch.
- E2E proof: the test imports the v1 durable-failure matrix at runtime, asserts
  exact ordered set equality for all 16 boundary IDs, and executes 16 named
  subtests. Each subtest owns a separate direct disposable PostgreSQL schema and
  verifies schema-local Prisma migrations before running.
- Harness proof: one confirmed query enters the real G7-G12 service chain with
  a preloaded strict discovery artifact, nonempty lead/traffic work, strict
  immutable S3/message fakes, counted normalized provider fakes, controlled
  recovery time, and real `recoverPipelineWork`. Restart retains only
  PostgreSQL, immutable artifacts, queued messages, clock, fault state and
  provider counters while creating new repository/coordinator/service objects.
  Completion comes only from durable Run state and every scenario is bounded to
  100 queued records or recovery actions.
- Matrix proof: all 16 rows passed. Lost DataForSEO response becomes durable
  ambiguous with one paid call; conditional S3 conflict fails closed; generic
  S3 boundaries retain their declared durable nonterminal state; terminal and
  check response-loss rows recover; duplicate/reverse and partial batch operate
  on two distinct tasks; zero-query and all-reused both execute with zero
  provider calls; cancellation uses the atomic generation fence; DLQ retains a
  nonterminal traffic record without a paid call; before-visibility rollback
  and after-visibility response loss replay safely.
- Cross-window corrections required by the real harness: latest CrUX BigQuery
  source artifacts derive their terminal `month:YYYYMM` scope from captured
  normalized rows and fail closed without it; final publication does not settle
  nonexistent DataForSEO `ShopWork` for `not_dispatched` evidence. Focused G-R7
  traffic and G-R8 final component suites remained green.
- Commands/outcomes: `node --test test/aws-pipeline-runtime-adapters.test.js
  test/aws-pipeline-recovery.test.js` passed 2/2 files; the required unfiltered
  isolated matrix command passed 18/18 tests (16 matrix subtests plus the parent
  and cancellation proof); `ALLOW_DATABASE_TESTS=true npm run
  test:integration` passed 35/35; `npm test` initially had only the two expected
  restricted-listener failures and the identical approved rerun passed 369,
  failed 0, skipped 19; `npm run build:lambda`, `npm run measure:lambda`,
  `npm run check:secrets`, and `git diff --check` passed.
- Package proof: all seven handlers built and cold-imported under Node
  `v24.14.1`, with required Prisma engine present and common file-list hash
  `a27c435df9624ef6618e6318b5329296fa5380c536416a5e6d918cfed71338a1`.
  Representative final/recovery ZIP sizes were 31,905,735 and 31,898,802 bytes;
  cold imports were 279.657 ms and 257.241 ms respectively.
- Contract hashes were reverified exactly: product contract
  `747cd5b398f3edd6d8c146187260f05c475abec006712d04a0df5301cd7c601f` and
  frozen plan `6fbbdaee89d20ceb6a9b369af43b79c0dfb17c36217d5dc33accd04e6caefdfe`.
- External actions: no AWS read/mutation, live or paid provider call,
  production database, frontend, infrastructure, deployment, staging,
  cutover, destructive action, staging, or commit. Existing root relocation
  and unrelated dirty state were preserved.
- Residual risk/user prerequisite: local corrective acceptance is complete;
  G14/G15, AWS creation, secrets, provider smoke calls, deployment and cutover
  remain parked behind their independent review and explicit approval gates.
- Acceptance: G-R9 passed. Accepted implementation advances to G-R9. The
  authorized corrective sequence stops here for independent review.

## Post-G-R9 independent review and G-R10 acceptance evidence — 14 August 2026

- Review baseline: product-contract and frozen-plan hashes matched the values in
  active state; backend commit was
  `4019f9193972d0b07e2fd59eedefd79222708e6f`; the backend worktree was clean
  before the corrective edit. Focused final/traffic/recovery/runtime tests passed.
- Reproduced finding: the required real-PostgreSQL recovery matrix initially
  passed 16 tests and failed the parent plus
  `duplicate_delayed_or_reversed_delivery`. The subtest failed in
  `PrismaRunRepository.publishAwsFinalResults()` with Prisma's closed interactive
  transaction error. A second isolated run of only that boundary reproduced the
  same failure at the same final-publication call. The temporary test filter was
  removed byte-for-byte before implementation.
- Source cause: the sole final publication writer used Prisma's implicit
  five-second interactive transaction timeout even though it performs the
  complete atomic cache/traffic/work/profile/score/grant/stage/Run visibility
  commit over remote Neon. The Stage and Run are locked inside that transaction,
  and its aggregation lease is freshly renewed for exactly 120 seconds before
  publication.
- Corrective specification: root
  `PRE_G14_CORRECTIVE_EXECUTION_SPECIFICATION.md`, SHA-256
  `6773da016428b52aec35f7471d0a83b5f84d66cfe89e7fd9978ff913c4eaedbd`.
- Changed backend file: `src/prisma-run-repository.js` only. No schema,
  migration, fixture, public interface, transaction-body order, lease,
  provider, message, artifact, configuration, frontend, or infrastructure
  change.
- Exact correction: only `publishAwsFinalResults()` now invokes Prisma's
  interactive transaction with `{maxWait:5000, timeout:90000}`. This remains
  below the freshly renewed 120-second aggregation lease and preserves
  visibility-last atomic rollback and normal fenced retry.
- Decisive database verification: final focused unit test passed; the two-case
  final PostgreSQL corpus passed; the complete recovery matrix then passed
  18/18, including the repaired duplicate/reverse case in 84.4 seconds and both
  final-publication crash boundaries; the complete isolated PostgreSQL corpus
  passed 35/35 in 1,473,509.635 ms.
- Regression/package verification: `npm run build:lambda`, `npm run
  measure:lambda`, `npm run check:secrets`, approved `npm test`, and `git diff
  --check` passed. The backend suite reported 388 tests: 369 passed, 0 failed,
  19 guarded database skips. All seven Node 24 packages retained file-list hash
  `a27c435df9624ef6618e6318b5329296fa5380c536416a5e6d918cfed71338a1`,
  the sole required Prisma engine, and the size bounds. Maximum measured cold
  RSS was 104,701,952 bytes for traffic-worker; final-aggregator measured
  31,905,764 ZIP bytes, 83,246,563 unpacked bytes, 278.967446 ms cold import,
  and 99,155,968 RSS bytes.
- External actions: no AWS read/mutation, provider call, production database,
  secret, frontend, infrastructure, deployment, staging, cutover, destructive
  action, or commit. Root relocation and unrelated owner state were preserved.
- Acceptance: G-R10 passed. Accepted local implementation advances to G-R10.
  G14 remains unassigned until a separate decision-complete deployment packet
  is authored and its local pre-mutation phase is explicitly activated.

## G14 local preparation evidence — 14 August 2026

- Authority: the user explicitly assigned G14. The decision-complete deployment
  packet is `AWS_G14_G15_DEPLOYMENT_EXECUTION_SPECIFICATION.md`, SHA-256
  `256cd3d0d7de5286db15e19cbd1df89a3cb6307e966e1ea0e8bc750063109d26`.
  G14 is active; the exact AWS mutation gate remains unsatisfied.
- Local infrastructure: added the two-resource retained/private bucket
  bootstrap and the 72-resource full disabled SAM template, production SAM
  config, guarded change-set/package/inspection scripts, and adversarial IaC
  tests. The full topology contains one bucket/policy, 12 queues, seven
  functions/log groups/roles, six disabled mappings, one disabled recovery
  rule plus permission, one empty retained secret, one unattached control-plane
  managed policy, and 27 alarms.
- Template hashes: bootstrap
  `4d7535b1e3192aa825b4e4eec303538fbf0c0895f9dfb5e55605f43f18499cce`;
  full `0b1c9b86017660fdbb956a3e45e7be701d94186eccbfb5b543b70f6571b96d3c`.
- SAM validation: downloaded official SAM CLI `1.161.0` to `/tmp` only. Its ZIP
  SHA-256 `78d2c3679976373cd856ee113395e867eb1b9c8980d4fca1002203423a721b4a`
  and signature-file SHA-256
  `4b374a77bbb6e437b153901e453712b9ff4a89c0472dcb88abb703cb54501ed0`
  matched the official release record. SAM lint passed for bootstrap and full
  templates; SAM build passed and correctly retained the prebuilt versioned-S3
  code references. Its harmless metadata-write warning is caused by the
  read-only home filesystem and did not affect validation or build exit status.
- Local safety: the IaC suite passed, including mutations for public storage,
  absent encryption, completed-object expiry, embedded secret, enabled source,
  mapping concurrency one, missing partial failure, visibility drift, and
  wildcard IAM. Dry-run emitted the complete topology without an AWS call;
  forced execute without a matching live-state approval token refused before
  invoking AWS. Secret scan and `git diff --check` passed.
- Regression: all unrestricted backend files passed. The only sandbox failures
  were the two documented localhost server files; their identical approved
  rerun passed 16/16. No application source was changed by G14.
- Package proof: all seven deterministic Node 24 ZIPs rebuilt, measured, and
  cold-imported with the sole Prisma engine and common file-list hash
  `a27c435df9624ef6618e6318b5329296fa5380c536416a5e6d918cfed71338a1`.
  ZIPs range from 31,898,840 to 32,071,601 bytes; maximum measured RSS is
  104,566,784 bytes, preserving the locked 512 MB setting.
- AWS preflight attempt: the intended read-only STS/quota/name-collision calls
  made no successful AWS request because the `storesignal-dev` IAM Identity
  Center token had expired and refresh failed. No AWS identity, resource, or
  configuration data was returned. The configured local Region remains
  `ap-south-2`.
- External actions: no AWS read completed, no AWS mutation, S3 object write,
  stack/change set, secret value, provider call, production database access,
  frontend edit, deployment, staging, cutover, destructive action, or commit
  occurred. Learning resources were not contacted or changed.
- Current prerequisite: run `aws sso login --profile storesignal-dev`. After
  that, G14 resumes with read-only account/quota/collision inspection and then
  stops to show the exact mutation packet for user approval.

## G14 read-only AWS preflight and template transport correction — 14 August 2026

- Read-only identity succeeded for profile `storesignal-dev`: account
  `074209491031`, assumed-role ARN
  `arn:aws:sts::074209491031:assumed-role/AWSReservedSSO_AdministratorAccess_0ba914b1a641b121/7noteven`,
  configured/target Region `ap-south-2`.
- Collision proof: the production stack, bucket, and empty-secret name do not
  exist; no queue, Lambda, log group, EventBridge rule, or CloudWatch alarm
  begins with `storesignal-production-pipeline`. No existing production name
  would be adopted.
- Quota finding: Service Quotas and Lambda `GetAccountSettings` both report 10
  total and 10 unreserved concurrent executions in `ap-south-2`. The fixed
  function reservations total 11, and Lambda requires 100 executions to remain
  unreserved, so the exact deployment prerequisite is a regional concurrent-
  execution quota of at least 111. G14 stops before mutation at this external
  prerequisite.
- Learning-resource read-only baseline: bucket `signalshop-buk` remains in
  `ap-south-2` with only the seven-day incomplete-multipart abort under
  `learning/`; source queue `storesignal-dev-learning` has zero visible/inflight
  messages and its five-receive redrive/360-second visibility configuration;
  the DLQ has one visible and zero inflight message; Lambda
  `storesignal-dev-learning-worker` remains Active, last update Successful,
  Node 26, 256 MB, 60 seconds, with no reserved concurrency. No learning
  resource was changed.
- Remote validation exposed a deterministic local tooling defect before any
  mutation: the full 88,178-byte template exceeds CloudFormation's 51,200-byte
  inline `TemplateBody` limit. The deployment packet and script now include one
  additional content-addressed, AES256, checksummed, versioned template object
  and use its exact version-specific S3 `TemplateURL`. Current-object metadata,
  bytes, encryption, and version are reconciled before reuse; a conflicting
  current object is refused.
- Corrected local verification passed: focused IaC tests, bootstrap SAM lint,
  and full-template SAM lint. The real-account dry run contains 72 full
  resources, seven ZIPs, eight exact object writes, bootstrap hash
  `4d7535b1e3192aa825b4e4eec303538fbf0c0895f9dfb5e55605f43f18499cce`,
  full hash `0b1c9b86017660fdbb956a3e45e7be701d94186eccbfb5b543b70f6571b96d3c`,
  and approval token
  `692e95170ac2ba3e958b1b99f5620f427ba3bf9ee15f51bc8a2d578c98a82c7f`.
  The revised deployment specification hash is
  `fda65daf4c2ddc87ab76377fe0974d9c71a96fd390367541792a39d99ffabbd1`.
- External actions: read-only AWS calls only. No change set, stack, bucket,
  object, queue, Lambda, role, policy, log group, rule, alarm, secret, quota
  request, provider call, database action, deployment, staging, cutover,
  destructive action, stage, or commit occurred.

## G14 new-account Lambda quota request attempt — 14 August 2026

- User authorization was exact: request Lambda concurrent executions quota
  `L-B99A9384` in account `074209491031`, Region `ap-south-2`, from 10 to 250.
- The Service Quotas API rejected the request before creation with
  `IllegalArgumentException`: the desired value must be greater than AWS's
  published default value of 1,000. The authorized 250 request therefore made
  no quota change and created no request or Support case.
- Read-only reconciliation confirms the account-applied value remains 10, the
  AWS default value is 1,000, and request history for this quota is empty.
- No stack, change set, bucket, object, queue, Lambda, secret, provider call,
  deployment, or other AWS mutation occurred. The only attempted mutation was
  the rejected exact quota request.

## G14 Lambda quota request submitted — 14 August 2026

- With explicit user authorization, submitted exactly one account-level quota
  request in `ap-south-2`: AWS Lambda concurrent executions `L-B99A9384`,
  desired value 1,001.
- AWS accepted request ID
  `ce33c0c396a04b7a8a2dbc11ed2004ecFAEyUfSM` with status `PENDING` at
  `2026-08-14T11:21:37.281000+05:30`. The applied quota remains 10 until AWS
  approves and deploys the request.
- No production resource, stack, change set, object, Lambda, queue, secret,
  mapping, provider, database, staging, or cutover mutation occurred.
- Subsequent read-only Free Tier API inspection confirms the account plan is
  `PAID` and `ACTIVE`, with no plan expiration date. The applied Lambda quota
  of 10 is therefore a separate new-account service quota, not evidence that
  the account was enrolled in the Free account plan.

## G14 current-quota disabled production deployment — 14 August 2026

- Authority and scope: the user explicitly authorized the temporary
  current-quota infrastructure correction and G14 deployment. The deployed
  packet is bound to account `074209491031`, assumed administrator role
  `AWSReservedSSO_AdministratorAccess_0ba914b1a641b121`, profile
  `storesignal-dev`, Region `ap-south-2`, stack
  `storesignal-production-pipeline`, and approval token
  `f5cedea4d18e0c8c5273b2acda3ecd9c01936a16000ff8c9e17f84ce6b4c616e`.
- Decision-complete correction: the G14 template, IaC tests, deployed-state
  inspector, and deployment specification now omit reserved concurrency from
  all seven functions while all six SQS mappings and the recovery rule remain
  disabled. This is a deployment-only bridge for the applied account quota of
  10. Exact reservations `1/2/2/2/1/2/1` remain mandatory before any trigger
  is enabled. Deployment specification SHA-256 is
  `06a5801c28d53de4f3752370a280b06586114c7df33b195df43ecd752b99f1a8`;
  bootstrap template SHA-256 is
  `4d7535b1e3192aa825b4e4eec303538fbf0c0895f9dfb5e55605f43f18499cce`;
  full template SHA-256 is
  `fa7d9b15bb3a750eb1da701a201ddf68035bb9e7082704c0a44c2b818b29f2d9`.
- Pre-mutation proof: STS again returned account `074209491031`; Service
  Quotas returned applied Lambda concurrency 10; quota request
  `ce33c0c396a04b7a8a2dbc11ed2004ecFAEyUfSM` had advanced to `CASE_OPENED`
  for 1,001; and CloudFormation accepted the exact bootstrap template.
- Bootstrap: guarded command `create-change-set.js ... --phase=bootstrap
  --execute` created and executed change set
  `g14-bootstrap-f5cedea4d18e`. Its normalized inventory contained exactly
  two additions, `ArtifactBucket` and `ArtifactBucketPolicy`. The retained,
  versioned, private AES256 bucket is
  `storesignal-prod-pipeline-074209491031-ap-south-2`.
- Package publication: guarded command `create-change-set.js ...
  --phase=package --execute` wrote exactly eight content-addressed,
  checksummed, AES256, versioned objects. AWS validated the full template from
  its exact version-specific S3 URL. Durable object identities are:

| Object | Bytes | SHA-256 / key prefix | Version ID |
|---|---:|---|---|
| `discovery-worker.zip` | 31,943,518 | `fff6c386f3f991093cea242a83929fd6f0cfd4629a9566b1fa0530660dc60d45` | `5ffcmJqBrRapcIKjVtuUiCPtaAptB6M7` |
| `domain-aggregator.zip` | 31,907,609 | `bc11a6cb728d87b667651e1d65aa28c3518d017e957f69c7d6a9157a38044912` | `5DsNXzfWsOVH92K6eOSLIJIjfz7FXPgc` |
| `lead-worker.zip` | 31,948,513 | `c8c0591255492c918f2f25e3696153455118dd1729798fab882d6aad9caf2099` | `b7veGqzrqFPrLXCZGKYFLMzM8d91lnK_` |
| `lead-aggregator.zip` | 31,907,903 | `b9bbf9f7a27d574f1611c820a41fdb44e94da3b8291b239e25ad931ceedadd78` | `HquP5ftjpmKUrMqueGjCuw62e5uDSy86` |
| `traffic-worker.zip` | 32,071,601 | `19ce4789058ee9ece308ad959ca581af0779d3085d929cf78ccefe02393a8571` | `qaS14XsZ7RaoElRx7sQixq3GIzVgKwHE` |
| `final-aggregator.zip` | 31,905,764 | `c40f9852f12ed63566b4828243c640b8b6db7de9fe07a304dab60acee3a2785f` | `SanI3YsEyR3WQKMjZcjcvn7D2XQanuFW` |
| `recovery.zip` | 31,898,840 | `206e70224d1a58c312ef3d0693e6581d8909fbd4fc2979719a1f4faa79d50b0e` | `PHIbGBdZ8Lx_kAunAQY1aCX8514fBB9W` |
| `cloudformation-template.json` | 87,877 | `fa7d9b15bb3a750eb1da701a201ddf68035bb9e7082704c0a44c2b818b29f2d9` | `pAyV1q6MSAmv235KYBBiw51serK9oT6R` |

- Full deployment: guarded review created change set
  `g14-full-f5cedea4d18e`, ID
  `247fc3c2-76c8-43e9-8f00-2c04ddc91543`. Normalized review proved exactly
  70 additions on top of the two bootstrap resources, with zero removals,
  replacements, or unapproved modifications. The separately guarded
  `--apply-reviewed-change-set` execution reached `UPDATE_COMPLETE`.
- Independent deployed-state proof: `inspect-stack.js --expected-disabled`
  passed for all 72 resources: six empty source queues, six empty DLQs, seven
  Node 24 functions with no reserved concurrency, six disabled mappings, one
  disabled recovery rule, one empty secret with no version, 27 actionless
  alarms, zero new Lambda log streams, retained/versioned/private bucket
  controls, and least-privilege IAM. Source and DLQ message totals were both
  zero.
- Learning-resource comparison passed unchanged: `signalshop-buk` retains only
  the `learning/` incomplete-multipart abort rule; the learning source queue
  remains empty with visibility 360 and redrive count five; its DLQ remains at
  one visible message; and `storesignal-dev-learning-worker` remains Active,
  Node 26, 256 MB, 60 seconds, with no reserved concurrency.
- Local acceptance: the focused IaC file passed; all seven ZIPs rebuilt,
  measured, and cold-imported under Node 24 with the exact Prisma engine and
  common file-list hash
  `a27c435df9624ef6618e6318b5329296fa5380c536416a5e6d918cfed71338a1`;
  secret scan and diff hygiene passed; and the full backend corpus passed 394
  tests: 375 passed, zero failed, and 19 guarded integrations skipped.
- Boundary: G14 is accepted in its disabled current-quota state. No secret
  value, provider call, production database action, frontend edit, trigger
  enablement, recovery-rule enablement, cutover, destructive action, stage, or
  commit occurred. G15 remains parked. After AWS applies at least 111 Lambda
  concurrency, an independently reviewed stack update must restore exact
  reservations `1/2/2/2/1/2/1` before any G15 trigger enablement.

## G15 current-quota production activation — 14 August 2026

- Authority and scope: the user explicitly authorized the production pipeline
  to run under the currently applied regional Lambda concurrency quota of 10,
  including secret installation, production Neon migrations, all six event
  source mappings, the recovery schedule, and live provider execution. The
  activation packet was bound to account `074209491031`, profile
  `storesignal-dev`, Region `ap-south-2`, stack
  `storesignal-production-pipeline`, and approval token
  `4ccc266d0b8bd9c5a1a63c553ba1e215d84b344ac6a8bee66be14000394aa1d3`.
- Google prerequisite: enabled `iam.googleapis.com` and
  `cloudresourcemanager.googleapis.com` in project `voice-assistant-471909`;
  created or reconciled service account
  `storesignal-aws-pipeline@voice-assistant-471909.iam.gserviceaccount.com` with
  only `roles/bigquery.jobUser`; and created key ID
  `a6c8926709835bd5f84421e1cc87ae6258997cb1`. The key was handled in memory and
  was not written to the workspace.
- Secret installation: installed the strict production value at
  `/storesignal/production/aws-pipeline`. The initial full Google key envelope
  was rejected by the runtime's strict contract and was replaced using the
  same key with exactly `client_email`, `private_key`, and `project_id`.
  `AWSCURRENT` is version `0e4cdc9d-efee-4af8-8da4-93fc17447aba`; no secret
  value was printed, committed, or placed in Lambda environment variables.
  Runtime validation proved the AWS pipeline active, the secret loaded, the
  BigQuery service account authenticated, and all bucket/queue configuration
  present.
- Production database: read-only migration status found exactly the two
  reviewed AWS coordinator migrations pending. `npm run db:migrate:deploy`
  applied `20260811120000_aws_pipeline_coordinator` and
  `20260812120000_aws_pipeline_remainder_foundations`; subsequent status was up
  to date. The pre-activation coordinator read found no queued/running work:
  four local runs awaited query confirmation, ten were completed, and three
  were failed. No historical run was automatically submitted to AWS.
- Control plane: the ignored backend `.env` now selects the AWS execution
  backend and names the production bucket, six queue URLs, Region, profile, and
  secret ID. The local backend was started on `127.0.0.1:3000`; an authenticated
  `/api/health` request returned HTTP 200 with `{"status":"ok"}`. New explicit
  query confirmations therefore enter the deployed AWS pipeline.
- Activation package: the exact full-template SHA-256 is
  `e34d9f80dc9d875aed970c8b18cca1598bb52f77564abfa021c6673397994a00`
  (87,870 bytes), stored as version
  `s_bhg41QYkJL2FPHRT7iS.Gqqqd1Tf0J`. Guarded change set
  `g15-activate-4ccc266d0b8b` contained only six event-source mapping
  modifications, the recovery-rule state modification, and CloudFormation's
  dependent recovery-permission update; it executed to `UPDATE_COMPLETE`.
- Independent deployed-state proof: the final expected-active inspector passed
  against all 72 resources: six source queues, six DLQs, seven Node 24
  functions, six enabled mappings, enabled recovery, a current secret version,
  27 alarms, and zero source/DLQ messages. No reserved concurrency is installed
  during this temporary posture; the regional quota of 10, Neon fencing, and
  the lead mapping maximum of two bound execution until the quota decision.
- Local acceptance: corrected the Lambda cold-invocation packaging test to
  explicitly force its child process into inert local mode instead of inheriting
  the newly active `.env`. The focused packaging test passed; the full backend
  reported 394 tests, 375 passed, zero failed, and 19 guarded integration skips.
  Secret scan and `git diff --check` passed.
- Boundary: the production pipeline is active and awaiting its first new,
  owner-confirmed run. No fabricated business run, direct provider smoke
  fixture, queue purge, object deletion, frontend edit, destructive action,
  stage, or commit occurred. Quota request
  `ce33c0c396a04b7a8a2dbc11ed2004ecFAEyUfSM` remains the prerequisite for the
  later reviewed steady-state reservations `1/2/2/2/1/2/1`; it does not block
  the currently active pipeline.

## G-R11 AWS run-creation backend correction — 14 August 2026

- Production observation: run `run_wkKmDLmvZpb3gfbPV_a_igJH` reached durable
  query review with ten selected queries and a present AWS provider snapshot,
  but retained `executionBackend=local`. Confirmation failed before dispatch
  with `PIPELINE_INPUT_CONFLICT`. The row remained unconfirmed, and the
  discovery queue contained no visible, in-flight, or delayed message.
- Cause: `PrismaRunRepository.runCreateData()` persisted the AWS provider
  snapshot but omitted `executionBackend`; Prisma consequently applied the
  schema default `local`. The confirmation transaction correctly rejected the
  contradictory snapshot/backend pair.
- Correction: new runs now persist `executionBackend=aws` exactly when the
  repository constructor produced an AWS provider snapshot, otherwise
  `executionBackend=local`. No schema, migration, provider, artifact, queue,
  Lambda, infrastructure, frontend, or public-interface behavior changed.
- Regression proof: focused repository tests assert both creation branches.
  The complete backend suite reported 395 tests: 376 passed, zero failed, and
  19 guarded integration skips. Secret scan and diff hygiene passed.
- Conditional production repair: exactly one row was changed for the observed
  run, from `local` to `aws`, requiring its exact ID, query-review state/phase/
  stage, generation one, revision one, absent confirmation revision/timestamp,
  and a present AWS provider snapshot. Safe read-back proved every predicate
  remained intact except the corrected backend. The repair did not confirm,
  submit, edit queries, or enqueue work; the discovery queue remained zero for
  visible, in-flight, and delayed messages.
- Operational note: the owner may retry confirmation for this existing run
  immediately. The currently running Node process loaded the previous module;
  restart it before creating a different run so future creation uses the
  corrected code.

## G-R12 collation-safe coordinator deployment and failed-run repair — 14 August 2026

- Live failure diagnosis: the confirmed run wrote its immutable query manifest
  successfully but Neon discovery registration rolled back with
  `PIPELINE_INPUT_CONFLICT`. Forced-rollback production-Neon diagnostics proved
  the same ten task identities and fingerprints were ordered differently by
  JavaScript `localeCompare()` and PostgreSQL collation. No stage, task, or
  discovery message survived the failed transaction.
- Correction: `registerStageInTransaction()` now reconciles the exact task set
  by `itemKey` and fingerprint rather than comparing two collation-dependent
  arrays positionally. Unit coverage reverses stored order; the isolated real-
  PostgreSQL corpus passed all five coordinator cases, including the exact
  mixed-case/base64url shape from the live run.
- Quota and proper topology: read-only Service Quotas inspection returned an
  applied regional Lambda concurrency quota of 1,000. The temporary quota-10
  bridge ended. The full template SHA-256 is
  `4794d56a9dad5bc56c5a541800467e06fd9b63301d5964689b25de6cc48cd857`
  (88,171 bytes) and installs exact function reservations
  `1/2/2/2/1/2/1` for DiscoveryWorker, DomainAggregator, LeadWorker,
  LeadAggregator, TrafficWorker, FinalAggregator, and Recovery.
- Packages: all seven Node 24 ZIPs rebuilt, measured, cold-imported, retained
  the exact Prisma engine, and shared file-list hash
  `a27c435df9624ef6618e6318b5329296fa5380c536416a5e6d918cfed71338a1`.
  The approved content-addressed package identities are:

| Object | Bytes | SHA-256 / key prefix | Version ID |
|---|---:|---|---|
| `discovery-worker.zip` | 31,943,570 | `ec1b247d0e5bff58f5ff5c87b0ddc4caa225addc3ee72fbb4a0234932b069638` | `H0FJmda9lAejPKIhwRLidcYbuBOJLAh6` |
| `domain-aggregator.zip` | 31,907,663 | `0a8687b3f742bdb2d38de7a1d4a983c22e11f7142c8cae26b1337db47c6affbc` | `bwddUdcWWjXZPWdsMpBxZ.o.9XgkMzp3` |
| `lead-worker.zip` | 31,948,569 | `313bd8869dc7babfce0210a851afe45a0714bcd78845989c2f0b233c67e1484b` | `hAYLLmA1PyVyjmrL1lh9IeHv06zv.UTI` |
| `lead-aggregator.zip` | 31,907,955 | `95033d5883c2129efd146d90cc70325c05c553a66edd78487b077f7182c05b06` | `5GC5I9xkBEUblAjTAJXzjxbJCCtCdS6R` |
| `traffic-worker.zip` | 32,071,661 | `8596ed066a2b4650d1f7f77d20db318a4d48de4d3b7450bb1ccc10923c65e730` | `jxOpVjbEMbziSBZddyAlKXR9WqSvMS4r` |
| `final-aggregator.zip` | 31,905,816 | `e1cde3e5ae8163f69462f53a2e5d7a8a61a5abc906784021d571b74f02b5edad` | `aIxiyozXhnZuMo5ENT0QEOW.VB6ySBxT` |
| `recovery.zip` | 31,898,895 | `8d4d55d5a8aa06f8ac7054bb771604f8e2f22978e33ee53e3c20ad33b2bb790b` | `oDqhCBycXq74bjO6w8y3eFA5.fkNCSeD` |
| `cloudformation-template.json` | 88,171 | `4794d56a9dad5bc56c5a541800467e06fd9b63301d5964689b25de6cc48cd857` | `MokY4wV9OZ..iNHg1OvZDuhBnPArbpYB` |

- Deployment guard: the first proposed change set was refused and never
  executed because CloudFormation also reported two dependency
  reevaluations. The corrected approval token
  `062ab08bad3bbfd278e8fc72cf4ccd88ac82275c8f428576bbcf801a81b34b67`
  and guard permit exactly seven in-place Lambda code/concurrency updates,
  `RecoverySchedule.Targets` from `Recovery.Arn`, and the conditional
  `RecoveryInvokePermission.SourceArn` replacement from
  `RecoverySchedule.Arn`. No schedule state/expression, mapping, queue, IAM,
  environment, secret, or other property is permitted.
- Deployment execution: reviewed change set `gr12-code-062ab08bad3b` matched
  the exact nine-resource guard and reached `UPDATE_COMPLETE`. The independent
  expected-active inspector then passed all 72 resources: seven functions with
  exact reservations, six enabled mappings, enabled recovery, six source
  queues, six DLQs, current secret, least-privilege IAM, and 27 alarms. Source
  and DLQ message totals were both zero.
- Immutable repair proof: before the database write, the run remained exactly
  `failed/finished/failed`, AWS generation one, query and confirmed revision
  one, ten strict valid `google-probe-v2` rows, unpublished, with zero
  PipelineStage/PipelineTask rows. S3 validation reconstructed the manifest
  from Neon and proved fingerprint
  `e1e373d30eae001978c7f691e6b0165eb29937bc5f8116f7e86e8b7182778c71`,
  60,170 canonical bytes, ten queries, and produced-at
  `2026-08-14T10:17:58.965Z`.
- Conditional production repair: exactly run
  `run_wkKmDLmvZpb3gfbPV_a_igJH` changed to
  `queued/scraping/queued_query_validation`. The transaction required every
  observed failed-state, revision, timestamp, validation, absent-stage/task,
  AWS-backend, unpublished, and expired-lease predicate. It preserved the
  queries, confirmation, provider snapshot, generation, manifest, and result
  visibility, and cleared only completion, safe failure, and expired lease
  fields. No server was running, so the repair dispatched no message or
  provider work.
- Final verification: focused infrastructure and coordinator tests, package
  build/measurement, secret scan, and diff hygiene passed. The complete backend
  suite passed 398 tests: 378 passed, zero failed, and 20 guarded integration
  skips. No frontend edit, queue purge, object deletion, stack deletion,
  provider call, commit, or destructive action occurred.
- Boundary: G-R12 is complete. The repaired run is intentionally queued and
  inert until the owner starts the corrected local backend. Startup recovery
  will claim the already-confirmed run, reconcile the immutable manifest, and
  begin the real end-to-end AWS/provider execution.

### G-R12 live-resume correction

- The preceding boundary claim was premature. After the first conditional
  repair, the same pre-correction worker identity from the original failure
  reclaimed the run at `2026-08-14T11:29:39Z` and failed it again at
  `2026-08-14T11:29:48.345Z`, still with zero PipelineStage/PipelineTask rows.
  The owner therefore never observed a durable resumed state.
- A later corrected backend process was confirmed listening, but the owner
  elected not to repair the historical run again and will test with a new run.
  The interrupted second repair did not commit: read-back still showed the
  exact second `failed/finished/failed` state. The old run remains unpublished
  and no second-repair helper or process remains.
- G-R12 acceptance is reopened until a new live run proves advancement beyond
  discovery registration. The deployed Lambda code, exact reservations, and
  independently verified 72-resource stack remain unchanged.

## G-R13 Amazon Linux Prisma engine correction — 14 August 2026

- Live failure and containment: the new AWS-backed run advanced through query
  confirmation and registered one discovery stage with ten pending tasks, but
  every Discovery invocation failed during module initialization before the
  handler, task claim, or provider call. CloudWatch identified the exact cause:
  the ZIP contained Prisma's Debian OpenSSL 3 engine while Lambda Node 24 on
  Amazon Linux 2023 required
  `libquery_engine-rhel-openssl-3.0.x.so.node`. Only Discovery mapping
  `20d9cdde-97f9-4f31-9116-da9870bc6122` was disabled; AWS confirmed
  `Disabled` with `USER_INITIATED`. Messages were not purged, deleted, or
  manually redriven.
- Packaging correction: Prisma now generates both `native` and
  `rhel-openssl-3.0.x` targets for local generation plus production packaging.
  The Lambda builder includes exactly the RHEL engine and rejects the Debian
  engine. Packaging tests mechanically assert the schema target and required
  engine filename. `npm run db:generate`, `npm run db:validate`, the focused
  packaging/infrastructure tests, `npm run check:secrets`, `git diff --check`,
  and `node --test --test-reporter=dot` all exited successfully. All seven ZIPs
  built, measured, and cold-imported locally; local import is not claimed as an
  Amazon Linux runtime proof. Their common file-list hash is
  `eed2b39bc940fe20c2070ecc64953c74c21b7ddded3e92a64f98a98dd5ba0ff2`.
- Corrected immutable packages:

| Object | Bytes | SHA-256 / key prefix | Version ID |
|---|---:|---|---|
| `discovery-worker.zip` | 31,943,704 | `3966e4befa7ae0f599afaf11457f2a07ded3364fbe7e815c18856d500deed37d` | `nxlZZTCxOpKCLrOW7mcyb.XCjg1nEP7S` |
| `domain-aggregator.zip` | 31,907,797 | `361fd8e96661ca248c6cdfe617eb8a1c0acb2f7c41aec1bef36d9365ebcb082e` | `IhcbhUCF3uG_IPUDlRggyr5Sh5J3Ddt4` |
| `lead-worker.zip` | 31,948,703 | `8cf11303876beb1bb620ff1e59f3745a5f80cf4c045a8f6d401ef90b565c33e6` | `7GofEIBa9zW_vI0GuJ.3aEtbU8Ax6wBV` |
| `lead-aggregator.zip` | 31,908,089 | `283ad841d564ab239054d6bfd2600a4e1d21d6addaa79de61b327b9c7c8625f0` | `fTdeyUVT0xPY91FDnBaoAKcIBE09EUQV` |
| `traffic-worker.zip` | 32,071,795 | `3cb1d9fc57913d6abdbb6d3537f67028e70dc8f1990c611b5ce4df025bd47520` | `5i5S1.vbx7HMZHRB.dHValhXLCf1SNXi` |
| `final-aggregator.zip` | 31,905,950 | `162db58759a0c5a2caf85551cdc53f2c0664e1c9eea6f19bbb41076476637129` | `ZGiH4zGNHP1qtryNa_LiHKuFSh8S9NH7` |
| `recovery.zip` | 31,899,029 | `7440adcc2c5720e4784679257bef7b65405ce07c2c2f2583eb0e3fd424511cb5` | `dpBDPjYE118Bm6AUhG9LlB5efvmBgnMc` |

- Guarded deployment: approval token
  `86698ee68bf5a78cf20bba728ac2f9ede4e44c142bc5cdfed9ad224f19851828`
  bound the exact artifacts and unchanged 88,171-byte template. Reviewed change
  set `gr13-engine-86698ee68bf5` contained exactly seven in-place Lambda `Code`
  modifications plus the expected `RecoveryInvokePermission` and
  `RecoverySchedule` dependency reevaluations. It reached `UPDATE_COMPLETE`.
  No concurrency, mapping, queue, IAM, environment, secret, schedule-state, or
  database property was present.
- Post-deployment proof: all seven functions reported Node 24, `Active`, and
  `LastUpdateStatus=Successful`; their deployed code checksums matched the
  uploaded objects. Reserved concurrency remained exactly `1/2/2/2/1/2/1`.
  Discovery remained disabled throughout those checks.
- Authorized resume and stop: only the same Discovery mapping was re-enabled;
  AWS reported `Enabled`, `USER_INITIATED`, and batch size one. This is the
  owner's requested stop point. No subsequent run-state, queue, provider,
  artifact, log, or database inspection was performed, so G-R13 does not claim
  that the resumed business run has advanced or completed.

## G-R14 scoped optional-artifact access correction — 14 August 2026

- Live diagnosis: run `run_KRnkR1jV7QInr2zXhHE-Hi9c` had ten discovery tasks
  repeatedly claimed but no terminal results or query artifacts. IAM simulation
  proved the Discovery role's exact query-object Get/Put permissions while
  `s3:ListBucket` was implicitly denied. S3 therefore returned an ambiguous 403
  for an absent optional attempt/result object, which the strict artifact store
  correctly refused to treat as missing.
- Correction and local proof: optional reads now perform `ListObjectsV2` with
  the exact key as `Prefix` and `MaxKeys:1`, require an exact returned key, and
  preserve strict GetObject validation. Four bucket-level ListBucket grants are
  scoped by the callers' existing prefixes only. Focused adapter/IaC tests,
  the full backend corpus, secret scan, diff hygiene, seven package builds,
  measurements, Node 24 cold imports, and exact RHEL Prisma-engine inspection
  passed. The common package file-list hash was
  `eed2b39bc940fe20c2070ecc64953c74c21b7ddded3e92a64f98a98dd5ba0ff2`.
- Guarded deployment: approval token
  `0cd6807efba1a54939c594ee142de5e665f542018a32ff635e961c9050a2c504`
  bound the seven packages and 90,453-byte template SHA-256
  `9e5366c9f6ca41bdc75ce6ea6f1749b50bc274b14bd8859ea7c89e9fd1693e2`.
  Reviewed change set `gr14-artifact-access-0cd6807efba1` contained only the
  seven Lambda code updates, the four exact policy updates, the three resulting
  worker Role-ARN reevaluations, and the two known Recovery dependencies. It
  reached `UPDATE_COMPLETE`. All functions were Active with successful updates
  and reservations remained `1/2/2/2/1/2/1`; IAM simulation allowed only the
  approved query/domain/traffic-batch prefixes and denied `deployment/*`.
- Live result: the unchanged queues and Recovery rule advanced all ten discovery
  tasks to `succeeded`; the discovery stage reached 10/10 terminal, and all ten
  strict per-query artifacts plus the confirmed manifest validated. No queue
  was purged, received manually, redriven, deleted, or given altered visibility.
- Newly isolated downstream defect: the Domain Aggregator then claimed the
  complete stage five times and failed immediately. Read-only replay proved the
  manifest and all ten artifacts valid, 81 candidates merging deterministically
  into 78 domains, and exactly one verified shop with no canonical URL.
  Canonical-URL-only provider-key derivation threw before any domain artifact or
  checkpoint. This is assigned separately as G-R15; G-R14's S3 access correction
  is accepted and did not cause the downstream identity defect.

## G-R15 verified-host provider identity fallback — 14 August 2026

- Correction: one strict helper now derives the DataForSEO hostname as
  `resolvedDomain || stableKey` and the CrUX origin from an HTTPS canonical URL
  or `https://${resolvedDomain || stableKey}`. Domain planning, fenced reuse
  reads, and combined-manifest validation all consume the same formula. This
  preserves the existing verified shop identity and provider batching.
- Verification: focused identity/domain/artifact/infrastructure tests passed.
  Read-only replay of the live artifacts derived 78 unique valid hostnames and
  78 unique HTTPS CrUX origins without exception. Prisma generation/validation,
  the complete backend corpus outside the restricted localhost sandbox, secret
  scan, and diff hygiene passed. All seven Node 24 ZIPs built, measured, and
  cold-imported with exactly the RHEL Prisma engine and common file-list hash
  `eed2b39bc940fe20c2070ecc64953c74c21b7ddded3e92a64f98a98dd5ba0ff2`.
- Guarded deployment: approval token
  `3a2c4a398572b72b105533507f0b0e67868c728b6074d4c2b356b18116b4e03b`
  bound seven encrypted/versioned package writes and the unchanged 90,453-byte
  template. Change set `gr15-provider-identity-3a2c4a398572` contained exactly
  the seven Lambda Code modifications plus the two known Recovery dependency
  reevaluations and reached `UPDATE_COMPLETE`. The independent active-stack
  inspector passed all 72 resources, seven functions, six mappings, six source
  queues, six DLQs, current secret, and 27 alarms; DLQ depth remained zero.
- Live acceptance: without queue or Neon repair, Recovery reclaimed the expired
  aggregation lease. Run `run_KRnkR1jV7QInr2zXhHE-Hi9c` completed discovery
  10/10, persisted 78 stable stores, completed the domain checkpoint, registered
  78 lead tasks, and changed its durable stage to `aws_lead`. At the acceptance
  observation, 77 lead tasks were terminal: 69 succeeded and eight failed
  safely; one bounded task remained processing. This satisfies G-R15's exact
  beyond-discovery acceptance condition.
- Frontend finding: the API-backed Run stage advanced correctly, but the
  frontend stage table lacked AWS-stage aliases and therefore continued showing
  its generic label/percentage. That separate UI-only correction is G-R16.

## G-R16 frontend AWS-stage presentation — 14 August 2026

- Cause and correction: the client already polls the Run API every three
  seconds and accepts arbitrary stage text, but its presentation layer had no
  entries for `aws_discovery`, `aws_lead`, or `aws_traffic_crux`. These now map
  exactly to the existing `discovering_stores`, `discovering_leads`, and
  `enriching_traffic` labels and percentages. AWS traffic also maps to the
  existing `Analyzing/active` traffic state. Unknown stages retain their
  generic label and 8% fallback.
- Verification: the focused presentation assertions passed; all 18 frontend
  test files passed; ESLint reported zero errors and one unrelated pre-existing
  `traffic-globe.tsx` hook warning; and the Next.js 16.2.12 production build
  completed successfully outside the restricted sandbox. Its existing
  Neon-auth dynamic-route notices remained informational and did not fail the
  build.
- Boundary: only `frontend/lib/stages.ts`,
  `frontend/lib/run-presentation.ts`, and the focused presentation test changed.
  No component, polling, API, backend, AWS, provider, database, deployment,
  style, or results-visibility behavior changed. No frontend process was
  running at verification time; the operator must start or restart it to load
  the new bundle.

## G-R17 same-task lead-work recovery — 14 August 2026

- Cause and correction: a retried `PipelineTask` received a new fenced lease
  token but retained the same durable task ID. `ShopWork` treated that same
  task ID as a competing live owner and returned `busy` forever. The lead-work
  claim now returns `owned` only when the current, token-validated task is
  already the recorded processing task. A stale token still fails before that
  branch, and a different live task remains busy.
- Local proof: focused unit and real isolated-PostgreSQL ownership tests proved
  same-task resume, stale-token rejection, and different-task exclusion.
  Prisma generation/validation, the complete backend corpus, secret scan, diff
  hygiene, and all seven Node 24 package builds, measurements, cold imports,
  and exact RHEL-engine checks passed. The common file-list hash remained
  `eed2b39bc940fe20c2070ecc64953c74c21b7ddded3e92a64f98a98dd5ba0ff2`.
- Guarded deployment: approval token
  `2d7d58d5169f67b36df7965df01044078fcb93b3ebbd3ed75e043841a2edfe70`
  bound the seven immutable package versions and unchanged 90,453-byte
  template. Reviewed change set `gr17-lead-work-resume-2d7d58d5169f`
  contained exactly seven in-place Lambda code modifications plus the two
  known Recovery dependency reevaluations and reached `UPDATE_COMPLETE`. The
  independent active-stack inspector passed all 72 resources, seven functions,
  six mappings, six queues, six DLQs, current secret, and 27 alarms; the stack
  was active and DLQ depth remained zero.
- Live result and blocker: the formerly self-blocked lead task advanced from
  lease attempt 6 to 15, proving the ownership correction is active. The lead
  worker then reached real page fetching and was terminated on three consecutive
  invocations with `Runtime.OutOfMemory`; CloudWatch reported the configured
  512 MB fully consumed. No Browserless attempt marker or lead result artifact
  was written, locating the failure before paid Browserless dispatch. The run
  remains safely unpublished at `aws_lead`, with 77/78 terminal tasks (69
  succeeded, eight failed, one processing), zero DLQ messages, and no manual
  queue or database intervention.
- Boundary: G-R17 remains unaccepted because its live advancement criterion did
  not pass. Raising `LeadWorker` memory would change the deployed resource and
  execution economics outside the authorized code-only G-R17 mutation, so it
  requires an explicit decision-complete corrective window and AWS mutation
  approval.

## G-R18 lead-worker live memory correction — 14 August 2026

- Guarded change: the production template and active-stack inspector now
  require 1024 MB only for `LeadWorker`; the other six functions remain at 512
  MB. Focused infrastructure/packaging tests, secret scan, and diff hygiene
  passed. The seven Lambda ZIPs and their version IDs were unchanged; only the
  new 90,454-byte template (SHA-256
  `14ca22d34a2b46393462758ef21481fc1a91e351ebd657c6436c9a46ab003d26`,
  version `ZK2q6kkdgUUtXUWGAR.lkakvWAI_nb.T`) was added.
- Approval and deployment: token
  `25455ac948eaa4e70a93b901bdcd029dc6e2e8746052bb41da640293346c78c9`
  bound the unchanged packages and new template. Reviewed change set
  `gr18-lead-memory-25455ac948ea` contained exactly one non-replacing
  `LeadWorker` modification and reached `UPDATE_COMPLETE`. The function was
  Active with successful update, 1024 MB memory, 90-second timeout, 512 MB
  ephemeral storage, reserved concurrency two, and unchanged code checksum
  `lMalemTvUbMGPCWZmAV02ofalXML4m9bYCyomMKF13k=`. The complete 72-resource
  active-stack inspection passed.
- Failed acceptance: the first 1024 MB execution was also terminated with
  `Runtime.OutOfMemory`, reporting all 1024 MB consumed. Lead remains 77/78
  terminal and unpublished. Three records produced by the preceding repeated
  OOM deliveries were visible in the lead DLQ; no queue record was received,
  purged, redriven, deleted, or altered.
- Exact local diagnosis: the affected sanitized candidate reproduced its real
  five-page, concurrency-two extraction without Browserless or another paid
  provider. It failed at `src/contact-extractor.js:250` with
  `RangeError: Invalid array length` after reaching approximately 2,021,256 KB
  maximum RSS. An invalid empty `mailto:` normalizes to the empty string;
  `rawValueIndexes()` then calls `indexOf("", start)` and assigns
  `start = index + 0`, so the loop never advances and grows `indexes` until
  exhaustion. One-page and page-fetch-only controls remained bounded, and the
  live prefix still had neither a Browserless attempt marker nor a lead result
  artifact. The temporary candidate copy was removed after diagnosis.
- Boundary: G-R18 remains unaccepted. Its specification expressly forbids
  choosing another memory size after a 1024 MB failure. The next correction
  must guard empty normalized values before occurrence scanning, prove invalid
  `mailto:` inputs terminate under the real concurrent page shape, restore the
  intended 512 MB LeadWorker memory after bounded-memory proof, and deploy as a
  new append-only window.
