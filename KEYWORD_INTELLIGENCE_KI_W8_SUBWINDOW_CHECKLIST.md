# KI-W8 Window-Agent Sequential Assessment Checklist (`S1`)

Status: **AWAITING_PARENT_DECOMPOSITION_REVIEW**  
Parent window: `KI-W8`  
Parent assignment: `ASG-KI-W8-WA-01`  
Window agent: `KI-W8-WINDOW-AGENT`

This is the frozen subordinate decomposition for `KI-W8`. It authorizes no
execution. It contains zero implementation/source leaves and exactly one
window-agent-personally-executed assessment, `KI-W8-I001`, as required by
`DEC-KI-059`, A4, A8 and A5 state 200. `KI-W8-I001` may start only after a
parent decomposition approval and a new A5 execution assignment.

Sibling artifacts:

- `S2`: `KEYWORD_INTELLIGENCE_KI_W8_SUBWINDOW_STATE.md`
- `S3`: `KEYWORD_INTELLIGENCE_KI_W8_SUBWINDOW_EVIDENCE.md`

Inherited parent package:

- `A1`: `KEYWORD_INTELLIGENCE_PRODUCT_CONTRACT.md`
- `A2`: `KEYWORD_INTELLIGENCE_DISCOVERY_DOSSIER.md`
- `A3`: `KEYWORD_INTELLIGENCE_DECISION_LEDGER.md`
- `A4`: `KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md`
- `A5`: `ACTIVE_EXECUTION_STATE.md`
- `A6`: `KEYWORD_INTELLIGENCE_EXECUTION_EVIDENCE.md`
- `A7`: `KEYWORD_INTELLIGENCE_SPECIFICATION_CHANGELOG.md`
- `A8`: `KEYWORD_INTELLIGENCE_TRACEABILITY_INDEX.md`

## 0. Frozen inheritance and zero-leaf exception

### 0.1 Revisions and baselines

| Authority/input | Frozen revision or state |
|---|---|
| Parent standard | `PROJECT_AGNOSTIC_DECISION_COMPLETE_CHECKLIST_AUTHORING_STANDARD.md` / `cda352017e75c0d11f6797d9fbe108b4365508cd38b0e92365cfb523ede32848` |
| Sub-window standard | `PROJECT_AGNOSTIC_WINDOW_AGENT_SUBWINDOW_AUTHORING_STANDARD.md` / `842c29550c06c22d63e0a058a27cb8a9ff6b538b3168d2c83a384890b44247f0` |
| A1 | `8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c` |
| A2 | `493192fc317c00ee43e277e85e00718985190cdd5c21e3d6824f67dd1d0b7c0c` |
| A3 | `6c0809225ba5336dc923786674b990f83c8db2496b88016f7655a770afb7e307` |
| A4 | `4f4b16bbe6ab20312e312db75506f9acfee7aaca67fbb66d1d951676f1f646e4` |
| A8 | `90c2f808426c4f1cf20ad885860e01b66763f3fc607e28c3b2dd9a2ef7391a5f` |
| A5 authoring state | state `200` / `a4e08c31469b1c309a58ef52c457a65bcef3b9fe0561d9e60cabb802df4429b3` |
| Coordination root | commit `1d77166817830af0ba5acc4e6fa7fe61dd234795`; only A5/A6/A7 contain the parent assignment delta |
| Backend | clean commit `c3ba835be446ba43e1a80be4f5ab4d28bae89497` |
| Frontend | clean commit `5e441aae7e2f3a132b2c7fc85bf1bc525d3d5cb6` |

The starting root changed-path set is exactly
`ACTIVE_EXECUTION_STATE.md`, `KEYWORD_INTELLIGENCE_EXECUTION_EVIDENCE.md`, and
`KEYWORD_INTELLIGENCE_SPECIFICATION_CHANGELOG.md`; its sorted-member-plus-LF
digest is `de3724531095ca3c8d7ebbb1089b339c8f40927f7a23f8b4b6f6b43b33edc2ce`.
Those are parent-owned assignment edits and must remain byte-identical during
this decomposition turn.

### 0.2 Parent scope copied without expansion

`KI-W8` proves applied capability, deploys the accepted keyword slice disabled,
creates exactly one one-seed research through the normal authenticated API,
activates the mapping/recovery, observes that same research to completion and
creates one run handoff, then stops before Run confirmation.

The assessment may write only:

1. append-only `KI-W8` entries in A6;
2. one-version A5 transitions;
3. the gitignored generated files produced by the accepted W7 deployment and
   measurement scripts under
   `email_scraper/dist/aws-deployment/keyword-intelligence/` and
   `email_scraper/dist/lambda/*measurements.json`.

It may make only the external mutations individually approved as
`W8-ACT-01` through `W8-ACT-07`. It must never edit source, tests, schemas,
migrations, packages, lockfiles, frontend files, A1-A4/A7/A8, or either
standard; commit/push; create a second research; confirm/start the downstream
Run; receive/delete/purge/redrive a queue; replay a DLQ; delete S3/database
evidence; expose secrets/private values; or claim final project completion.

### 0.3 Why there are no file leaves

A4 and A8 explicitly require `window_agent_personal_execution_no_leaf_delegation`.
Therefore:

- initial `FILE` sub-windows: `[]`;
- corrective `FILE` sub-windows preauthorized: `[]`;
- parallel waves: `[]`;
- planned implementation/source changed-file set: `[]`;
- empty-set digest:
  `e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855`;
- first and only subordinate execution unit: `KI-W8-I001`.

Sections 4, 6, 7 and 8 of the sub-window standard are `N/A` only for file-leaf
mechanics. Their authority, scope, one-file, correction and independent-review
protections remain enforced by prohibiting all leaf delegation and all
implementation writes. Any product/source defect, missing deployment mechanism,
or required new test is `PARENT_BLOCKED`; the window agent cannot repair it.

## 1. Frozen accepted inputs and derived identities

### 1.1 W7 packet inputs

| Member | Source | Bytes | SHA-256 | Content-addressed key |
|---|---|---:|---|---|
| template | `email_scraper/infrastructure/aws/template.yaml` | `104582` | `2d87c28ad564842d13e42855aef676fb30b2f3aa357ef6eda73bc88f67cb8fa8` | `deployment/2d87c28ad564842d13e42855aef676fb30b2f3aa357ef6eda73bc88f67cb8fa8/cloudformation-template.json` |
| KeywordWorker | `email_scraper/dist/lambda/keyword-worker.zip` | `32006605` | `47fda36e621bcb35a98fd1614854dadc0231e70871cf5488828610400d8460d4` | `deployment/47fda36e621bcb35a98fd1614854dadc0231e70871cf5488828610400d8460d4/keyword-worker.zip` |
| Recovery | `email_scraper/dist/lambda/recovery.zip` | `31984076` | `cc5b6819d80c85a3ca74f05c9887b580aa8dd498f1f866ffc8e812ce89f2bb9c` | `deployment/cc5b6819d80c85a3ca74f05c9887b580aa8dd498f1f866ffc8e812ce89f2bb9c/recovery.zip` |

The deployment identity is exactly:

```yaml
profile: storesignal-dev
region: ap-south-2
stack: storesignal-production-pipeline
environment: production
account_id: DEFERRED_P2_EXACT_12_DIGIT_STS_ACCOUNT
artifact_bucket_formula: storesignal-prod-pipeline-${account_id}-ap-south-2
packet_contract: storesignal-keyword-deployment-v1
```

`account_id` is an external fact, not a choice. P2 captures it from STS and
requires a 12-digit value. The packet approval token is then derived only by
the accepted `buildDeploymentPacket()` canonical SHA-256 formula. Any other
account/profile/region/stack/environment or packet hash stops before ACT-01.

### 1.2 Exact generated local paths

The accepted scripts may create/update only these gitignored paths:

```text
email_scraper/dist/lambda/keyword-worker-measurements.json
email_scraper/dist/lambda/measurements.json
email_scraper/dist/aws-deployment/keyword-intelligence/packet.json
email_scraper/dist/aws-deployment/keyword-intelligence/artifacts.json
email_scraper/dist/aws-deployment/keyword-intelligence/full-change-set.json
email_scraper/dist/aws-deployment/keyword-intelligence/activate-change-set.json
```

No generated file is authority. Its contract, hash, object versions and
change-set ID must be reconciled against current source, A5 and live read-only
AWS evidence before use.

### 1.3 Exact required case sets

```json
{
  "requiredCases": [
    "W8-CONF-01",
    "W8-LIVE-01",
    "W8-LIVE-02",
    "W8-LIVE-03",
    "W8-LIVE-04",
    "W8-LIVE-05",
    "W8-LIVE-06",
    "W8-LIVE-07",
    "W8-LIVE-08",
    "W8-LIVE-09"
  ],
  "requiredControls": [
    "W8-NC-01",
    "W8-NC-02",
    "W8-NC-03",
    "W8-NC-04",
    "W8-NC-05",
    "W8-NC-06"
  ]
}
```

The ten-case sorted-member-plus-LF digest is
`b716a609b2269f69d4e042503ad47dabb1eb397e17726af850f38ab09940431a`.
The six-control digest is
`1a2fd2fb71c94f297b27c5c6ad580c67d94ae807525b420996bd4382d46b7c6e`.
Duplicate IDs fail before digesting.

## 2. Approval state machine

### 2.1 Approval predicate

An action is approved only when all of these are simultaneously true:

1. the requester explicitly approved that exact `W8-ACT-nn` after receiving its
   action disclosure;
2. the parent appended the approval evidence to A6 and CAS-updated A5;
3. A5 names `KI-W8`, the current W8 execution assignment, the exact action ID
   in `authorized_actions`, the exact predecessor evidence and current S1
   revision;
4. A5 pins the action-specific target identities listed below;
5. source/packet/live facts used by the action remain byte/value equal; and
6. for ACT-01/02/05, A5 `aws_mutation_approval` equals the accepted packet's
   64-hex `approvalToken`, which the accepted deployment script verifies before
   its first AWS call.

Approval is action-specific, expires on any bound-value drift, and never
implies another action. Absence or staleness transitions S2 to the matching
`AWAITING_REQUESTER_APPROVAL_*` state and performs zero action.

### 2.2 Action-specific bound facts

| Action | Required A5/action evidence before execution |
|---|---|
| `W8-ACT-01` | account/profile/region/stack; three source hashes/bytes/keys; artifact bucket; packet token; `phase=full`; create-review only |
| `W8-ACT-02` | all ACT-01 facts; exact `full-change-set.json` SHA-256, `ChangeSetId`, normalized allowlisted change projection; execute existing reviewed ID only |
| `W8-ACT-03` | exact P2-observed host provider/service/revision/workload identity; exact `ControlPlanePolicyArn`; names `AWS_PIPELINE_KEYWORD_RESEARCH_QUEUE_URL` and `AWS_PIPELINE_KEYWORD_RESEARCH_ENABLED`; value hashes only, never values |
| `W8-ACT-04` | exact owner-A session identity hash, one normalized seed hash/length, `$3.00000000` disclosure, backend/UI origin, disabled-state evidence; create once through normal API |
| `W8-ACT-05` | packet token; exact `activate-change-set.json` SHA-256/ID/projection; same research ID hash; active mapping/recovery target |
| `W8-ACT-06` | same research ID hash; one-research ceiling; planned 11 first-pass calls, 55 attempts and `$3.00000000` cap; no downstream Run confirmation |
| `W8-ACT-07` | failure evidence; exact host target; exact rollback change-set ID/projection; disable-only order; no purge/redrive/delete/second canary |

ACT-05 is the physical operation that can release the queued message and incur
provider cost. Therefore the activation command is prohibited until **both**
independent ACT-05 and ACT-06 approvals are present together in current A5.
This coupling does not merge the approvals: either missing approval yields zero
activation. There is no state in which ACT-05 is executed while ACT-06 is
absent.

### 2.3 Exact sequential states

```text
AWAITING_PARENT_DECOMPOSITION_REVIEW
 -> READY_FOR_READ_ONLY_PREFLIGHT
 -> PREFLIGHT_RUNNING
 -> AWAITING_REQUESTER_APPROVAL_ACT01
 -> ACT01_RUNNING -> AWAITING_REQUESTER_APPROVAL_ACT02
 -> ACT02_RUNNING -> AWAITING_REQUESTER_APPROVAL_ACT03
 -> ACT03_RUNNING -> AWAITING_REQUESTER_APPROVAL_ACT04
 -> ACT04_RUNNING -> AWAITING_REQUESTER_APPROVAL_ACT05
 -> AWAITING_REQUESTER_APPROVAL_ACT06
 -> ACT05_ACT06_RUNNING
 -> LIVE_OBSERVATION_RUNNING
 -> READY_FOR_PARENT_REVIEW
```

Any pre-activation failure stops without mutation beyond already completed
approved actions. Any failure after ACT-05 begins transitions to
`AWAITING_REQUESTER_APPROVAL_ACT07`. ACT-07 approval runs disable-only rollback,
then stops `READY_FOR_PARENT_REVIEW_WITH_ROLLBACK`. Without ACT-07 approval the
agent records the live state and performs no rollback. It never purges, deletes,
redrives, manually invokes, or creates a second research.

## 3. Deferred applied facts and fail-closed branches

Only the following external facts are deferred to P1-P6. No other execution
choice may be made during assessment.

| Gate | Observed fact | Passing branch | Every nonpassing branch |
|---|---|---|---|
| `DG-W8-01` | STS account and stack status/inventory | 12-digit account; fixed profile/region/stack; complete stack | stop `PARENT_BLOCKED_TARGET_IDENTITY`; zero mutation |
| `DG-W8-02` | account Lambda/SQS/CloudFormation capability | all exact DEC-KI-059 sizes, timeout, memory, reservation and mapping/queue constraints possible | stop `PARENT_BLOCKED_APPLIED_CAPABILITY`; zero mutation |
| `DG-W8-03` | existing production secret shape | one current string version strictly parses; all required keys exact; DataForSEO login/password nonempty | stop `PARENT_BLOCKED_SECRET_VERSION`; secret mutation is outside this seven-action window |
| `DG-W8-04` | parent-supplied provider-capability protocol | current A5 contains the complete `KIW8_PROVIDER_CAPABILITY_PROTOCOL_V1` record in §3.3 and its command/output hashes match | stop `PARENT_BLOCKED_PROVIDER_CAPABILITY_PROTOCOL` before a provider request; the executor never selects an endpoint or contract |
| `DG-W8-05` | backend host target observed by the §3.2 admissible discovery request | current A5 contains the complete `KIW8_HOST_PROTOCOL_V1` record in §3.4 binding that observation to literal update/readback operations | stop `PARENT_BLOCKED_HOST_PROTOCOL` before ACT-03; the executor never selects a hosting mechanism |
| `DG-W8-06` | owner A/B authenticated sessions | distinct authenticated owners and normal browser/API origin are available without exposing tokens | stop `PARENT_BLOCKED_CANARY_IDENTITIES` |
| `DG-W8-07` | initial keyword durable/queue state | zero nonterminal research and zero source/DLQ messages | stop `PARENT_BLOCKED_DIRTY_CANARY_BASELINE`; never delete or drain |

The read-only preflight may discover exact values but may not mutate A1-A4/A7/A8,
resources, hosting, secrets, queues or application rows. Every passing value is
recorded sanitized in S3/A6 and pinned by the next parent A5 approval CAS.

### 3.1 Bound process inputs and output discipline

Every command in `KI-W8-I001` starts from its stated cwd with shell tracing
disabled. The execution assignment supplies exactly these process-only values:

```text
AWS_PROFILE=storesignal-dev
AWS_REGION=ap-south-2
KIW8_ORIGIN=<absolute HTTPS origin, no path/query/fragment/trailing slash>
KIW8_OWNER_A_COOKIE=<one complete Cookie request-header value>
KIW8_OWNER_B_COOKIE=<one complete Cookie request-header value>
KIW8_APPROVED_SEED=<one normalized 1..100-character seed>
KIW8_WINDOW_STARTED_AT=<ISO-8601 instant fixed before ACT-04>
KIW8_RESEARCH_ID=<exact A5 research ID after ACT-04 reconciliation>
```

The angle-bracket members above are named external values, not executor choices.
Before use, the runner requires current A5 fields
`kiw8_origin_sha256`, `kiw8_owner_a_cookie_sha256`,
`kiw8_owner_b_cookie_sha256`, `kiw8_seed_sha256`, and
`kiw8_window_started_at` to equal SHA-256 of the exact UTF-8 process value or
the exact timestamp. After ACT-04, A5 must additionally contain literal
`kiw8_research_id` plus its SHA-256 and every later process value must equal
both. Owner cookies, seed, database URL, provider credentials,
secret value, full account ID and raw response bodies never reach stdout,
stderr, S1/S2/S3/A6 or a generated file. A command emits one JSON object per
prescribed evidence line with only fields enumerated by its output schema; an
extra key or extra line is a privacy failure. The save-handoff command has the
two exact lines frozen in §3.7; all other commands have one.

All AWS CLI commands below have the literal suffix
`--profile storesignal-dev --region ap-south-2 --no-cli-pager --output json`.
All network commands have `AWS_MAX_ATTEMPTS=3`. All frontend requests use only
`KIW8_ORIGIN`, `Accept: application/json`, the named owner cookie and, for a
JSON body, `Content-Type: application/json`. Redirect mode is `error` and the
request ceiling is 20 seconds. The only evidence destination is the matching
append-only `EV-KI-W8-I001-*` entry in S3; the final sanitized aggregate is
copied to A6. No raw command response is an evidence artifact.

### 3.2 Exact admissible host discovery

P2 may obtain the host target only from current A5 field
`kiw8_host_discovery_request_v1`, whose schema is exact:

```json
{
  "method": "GET",
  "url": "https://<parent-approved-provider-host>/<parent-approved-path>",
  "headerEnvironmentNames": ["KIW8_HOST_READ_TOKEN"],
  "responseKeys": ["provider","serviceId","revisionId","workloadIdentity","configurationRevision"],
  "requestSha256": "<64-lower-hex>"
}
```

The parent replaces the shown value placeholders before execution and pins the
canonical-record SHA-256. The executor performs that one GET, substitutes only
the named token header defined by the same A5 record, rejects redirects and any
non-200 response, and strictly rejects a response with missing, empty or extra
keys. It emits only provider plus SHA-256 of the other four strings. If this
record is absent, still contains a placeholder, names another method/header, or
does not hash exactly, P2 stops `PARENT_BLOCKED_HOST_DISCOVERY_PROTOCOL` without
calling a hosting provider. Repository files, DNS inference, process listings
and remembered provider knowledge are not admissible discovery inputs.

### 3.3 Exact P5 prerequisite record

The current state-200 authority contains no proven zero-charge DataForSEO
capability operation. Therefore P5 has exactly one executable outcome under
state 200: emit
`{"gate":"P5","outcome":"PARENT_BLOCKED_PROVIDER_CAPABILITY_PROTOCOL"}`
and stop before a provider call. A later parent may unblock P5 only by adding
this complete literal record to A5 and re-pinning S1:

```json
{
  "contract": "KIW8_PROVIDER_CAPABILITY_PROTOCOL_V1",
  "officialSourceUrl": "<literal official HTTPS URL>",
  "officialSourceRetrievedAt": "<ISO-8601>",
  "officialSourceSha256": "<64-lower-hex>",
  "method": "GET",
  "requestUrl": "<literal documented zero-charge HTTPS endpoint>",
  "authorization": "basic-from-DATAFORSEO_LOGIN-and-DATAFORSEO_PASSWORD",
  "requestBody": null,
  "responseExactKeys": ["<literal ordered key set>"],
  "acceptedProjection": {
    "suggestionsEndpoint": "/v3/dataforseo_labs/google/keyword_suggestions/live",
    "relatedEndpoint": "/v3/dataforseo_labs/google/related_keywords/live",
    "overviewEndpoint": "/v3/dataforseo_labs/google/keywords_data/google_ads/search_volume/live",
    "requestsPerMinute": 30,
    "zeroCharge": true
  },
  "canonicalRecordSha256": "<64-lower-hex>"
}
```

The parent replaces every placeholder; a remaining placeholder is a failing
predicate. With a valid record, P5 retrieves the official source once with
method GET and no credentials, checks its SHA, then calls exactly the recorded
GET once using credentials loaded by P4. The strict parser accepts only the
recorded key set and projection. It emits only endpoint-name equality booleans,
`requestsPerMinute`, `zeroCharge`, source SHA and `$3.00000000`; raw provider
content/status text is discarded in memory. No suggestions, related or
overview endpoint is called by P5.

### 3.4 Exact ACT-03 prerequisite record

P2 observation does not authorize the executor to design host mutation. ACT-03
is executable only when its separate approval state contains this exact record:

```json
{
  "contract": "KIW8_HOST_PROTOCOL_V1",
  "provider": "<literal P2 provider>",
  "serviceIdSha256": "<64-lower-hex>",
  "startingRevisionSha256": "<64-lower-hex>",
  "workloadIdentitySha256": "<64-lower-hex>",
  "update": {
    "method": "<literal method>",
    "url": "<literal provider URL>",
    "headerEnvironmentNames": ["KIW8_HOST_WRITE_TOKEN"],
    "bodyExactKeys": ["policyArn","AWS_PIPELINE_KEYWORD_RESEARCH_QUEUE_URL","AWS_PIPELINE_KEYWORD_RESEARCH_ENABLED","expectedConfigurationRevision"],
    "bodyLiterals": {"AWS_PIPELINE_KEYWORD_RESEARCH_ENABLED":"true"}
  },
  "healthyReadback": {
    "method": "GET",
    "url": "<literal provider URL>",
    "pollSeconds": 10,
    "ceilingSeconds": 600,
    "responseExactKeys": ["serviceId","revisionId","health","policyArn","configurationRevision","environment"]
  },
  "canonicalRecordSha256": "<64-lower-hex>"
}
```

The parent replaces all placeholders and binds the canonical-record SHA in the
ACT-03 approval. The update body is constructed mechanically from the exact
stack outputs `ControlPlanePolicyArn` and `KeywordResearchQueueUrl`, literal
`"true"`, and P2's configuration revision. No other field is sent. Readback
must return the same service identity, a new healthy revision, exact policy ARN,
exact queue URL and literal true while every other configuration member's
canonical hash equals P2. Evidence contains hashes/booleans only. Absent,
incomplete or drifting protocol stops `PARENT_BLOCKED_HOST_PROTOCOL`; no host
request occurs.

### 3.5 Exact production Neon observer (`KIW8-DB-V1`)

All production database evidence uses one inline Node runner from
`email_scraper/`. It obtains `PipelineSecretArn` from the fixed stack via
`DescribeStacks`, loads only `AWSCURRENT` with `SecretsManagerClient`, parses it
through `loadPipelineSecrets`, and constructs `createPrismaClient` with the
returned `databaseUrl`. Each mode runs one interactive transaction whose first
statement is literal `SET TRANSACTION READ ONLY`; any failed read-only setting,
write attempt or non-`public` schema stops. The runner always disconnects and
never emits its connection string.

The runner has exactly five modes and these literal parameterized queries:

```sql
-- baseline
SELECT count(*)::int AS "nonterminalResearchCount"
FROM "KeywordResearch"
WHERE state::text IN ('queued','running');

-- resolveResearch($1 ownerId,$2 seedJson,$3 windowStartedAt)
SELECT id, state::text AS state, generation, "selectionRevision"
FROM "KeywordResearch"
WHERE "ownerId"=$1 AND seeds=$2::jsonb AND "createdAt">=$3::timestamptz
ORDER BY "createdAt" ASC;

-- progress($1 researchId)
SELECT kr.state::text, kr.generation, kr.progress, kr."resultFingerprint",
       kr."selectionRevision", kr."safeErrorCode",
       count(DISTINCT ks.id)::int AS "stageCount",
       count(DISTINCT kt.id)::int AS "taskCount",
       count(DISTINCT CASE WHEN kt.state::text IN ('succeeded','skipped','failed') THEN kt.id END)::int AS "terminalTaskCount",
       count(DISTINCT ka.id)::int AS "attemptCount",
       coalesce(sum(ka."providerCostUsd"),0)::text AS "providerCostUsd"
FROM "KeywordResearch" kr
LEFT JOIN "KeywordResearchStage" ks ON ks."researchId"=kr.id
LEFT JOIN "KeywordResearchTask" kt ON kt."stageId"=ks.id
LEFT JOIN "KeywordResearchProviderAttempt" ka ON ka."taskId"=kt.id
WHERE kr.id=$1
GROUP BY kr.id;

-- artifactRows($1 researchId)
SELECT kr."resultFingerprint", ks.stage::text, ks.generation, ks."createdAt" AS "stageCreatedAt", ks."manifestS3Key", ks."manifestFingerprint", ks."manifestProducedAt",
       kt.id, kt."itemKey", kt."inputFingerprint", kt."endpointKey", kt."requestFingerprint", kt.state::text,
       kt."artifactS3Key", kt."artifactFingerprint", kt."createdAt"
FROM "KeywordResearchStage" ks
JOIN "KeywordResearch" kr ON kr.id=ks."researchId"
LEFT JOIN "KeywordResearchTask" kt ON kt."stageId"=ks.id
WHERE ks."researchId"=$1
ORDER BY ks.stage::text, kt."itemKey";

-- handoff($1 researchId)
SELECT h."runId", h."selectionRevision", h."clientRequestId", h."selectionFingerprint",
       r.state::text AS "runState", r.phase::text AS "runPhase", r.stage AS "runStage",
       r."confirmedQueryRevision", r."queriesConfirmedAt", r."resultsAvailable",
       jsonb_array_length(kr.selection->'items')::int AS "selectedItemCount",
       count(DISTINCT q.id)::int AS "queryCount",
       count(DISTINCT CASE WHEN
         (q."keywordResearchItemId" IS NOT NULL AND NOT EXISTS (
           SELECT 1 FROM jsonb_array_elements(kr.selection->'items') s
           WHERE s->>'sourceKind'='calculated' AND s->>'itemId'=q."keywordResearchItemId" AND s->>'keyword'=q.query
         )) OR (q."keywordResearchItemId" IS NULL AND NOT EXISTS (
           SELECT 1 FROM jsonb_array_elements(kr.selection->'items') s
           WHERE s->>'sourceKind'='manual' AND s->>'keyword'=q.query
         )) THEN q.id END)::int AS "lineageMismatchCount",
       count(DISTINCT ps.id)::int AS "pipelineStageCount",
       count(DISTINCT pt.id)::int AS "pipelineTaskCount",
       count(DISTINCT d.id)::int AS "dataForSeoLedgerCount",
       count(DISTINCT l.id)::int AS "leadCount",
       count(DISTINCT rs.id)::int AS "runStoreCount"
FROM "KeywordResearchHandoff" h
JOIN "KeywordResearch" kr ON kr.id=h."researchId"
JOIN "Run" r ON r.id=h."runId"
LEFT JOIN "RunQuery" q ON q."runId"=r.id
LEFT JOIN "PipelineStage" ps ON ps."runId"=r.id
LEFT JOIN "PipelineTask" pt ON pt."stageId"=ps.id
LEFT JOIN "DataForSeoRequestLedger" d ON d."runId"=r.id
LEFT JOIN "Lead" l ON l."runId"=r.id
LEFT JOIN "RunStore" rs ON rs."runId"=r.id
WHERE h."researchId"=$1
GROUP BY h.id,r.id;
```

The invocation is literal
`KIW8_DB_MODE=<gate-prescribed-mode> node --input-type=module -e
'<KIW8-DB-V1 source below>'`; the mode at each call site is named by that gate
and is not selected interactively. The exact source algorithm is:

```javascript
import { createHash } from "node:crypto";
import { execFileSync } from "node:child_process";
import { SecretsManagerClient } from "@aws-sdk/client-secrets-manager";
import { loadPipelineSecrets } from "./src/aws-pipeline/secrets.js";
import { createPrismaClient } from "./src/prisma-client.js";

const mode = process.env.KIW8_DB_MODE;
if (!["baseline", "resolveResearch", "progress", "artifactRows", "handoff"].includes(mode))
  throw new Error("KIW8_DB_MODE_INVALID");
const region = "ap-south-2";
const stackName = "storesignal-production-pipeline";
const stack = JSON.parse(execFileSync("aws", ["cloudformation", "describe-stacks",
  "--stack-name", stackName, "--profile", "storesignal-dev", "--region", region,
  "--no-cli-pager", "--output", "json"], { encoding: "utf8", maxBuffer: 16777216 })).Stacks?.[0];
const outputs = Object.fromEntries((stack?.Outputs || []).map((x) => [x.OutputKey, x.OutputValue]));
if (typeof outputs.PipelineSecretArn !== "string") throw new Error("KIW8_SECRET_OUTPUT");
const secrets = await loadPipelineSecrets({
  client: new SecretsManagerClient({ region, maxAttempts: 3 }),
  secretId: outputs.PipelineSecretArn
});
const prisma = createPrismaClient(secrets.databaseUrl);
const h = (x) => createHash("sha256").update(String(x)).digest("hex");
const one = (rows, code) => {
  if (!Array.isArray(rows) || rows.length !== 1) throw new Error(code);
  return rows[0];
};
async function ownerId() {
  const response = await fetch(`${process.env.KIW8_ORIGIN}/api/auth/get-session`, {
    headers: { Accept: "application/json", Cookie: process.env.KIW8_OWNER_A_COOKIE },
    redirect: "error", signal: AbortSignal.timeout(20000)
  });
  const value = await response.json();
  if (response.status !== 200 || Object.keys(value).sort().join(",") !== "session,user" ||
      !value.user || typeof value.user.id !== "string" || !value.user.id)
    throw new Error("KIW8_OWNER_SESSION");
  return value.user.id;
}
let raw;
try {
  raw = await prisma.$transaction(async (tx) => {
    await tx.$executeRawUnsafe("SET TRANSACTION READ ONLY");
    const schema = one(await tx.$queryRawUnsafe("SELECT current_schema() AS schema"), "KIW8_SCHEMA");
    if (schema.schema !== "public") throw new Error("KIW8_PRODUCTION_SCHEMA");
    if (mode === "baseline") return tx.$queryRawUnsafe(
      `SELECT count(*)::int AS "nonterminalResearchCount" FROM "KeywordResearch" WHERE state::text IN ('queued','running')`
    );
    if (mode === "resolveResearch") return tx.$queryRawUnsafe(
      `SELECT id,state::text AS state,generation,"selectionRevision" FROM "KeywordResearch" WHERE "ownerId"=$1 AND seeds=$2::jsonb AND "createdAt">=$3::timestamptz ORDER BY "createdAt" ASC`,
      await ownerId(), JSON.stringify([process.env.KIW8_APPROVED_SEED]), process.env.KIW8_WINDOW_STARTED_AT
    );
    const id = process.env.KIW8_RESEARCH_ID;
    if (!/^kr_[A-Za-z0-9_-]{24}$/u.test(id || "")) throw new Error("KIW8_RESEARCH_ID");
    if (mode === "progress") return tx.$queryRawUnsafe(
      `SELECT kr.state::text,kr.generation,kr.progress,kr."resultFingerprint",kr."selectionRevision",kr."safeErrorCode",count(DISTINCT ks.id)::int AS "stageCount",count(DISTINCT kt.id)::int AS "taskCount",count(DISTINCT CASE WHEN kt.state::text IN ('succeeded','skipped','failed') THEN kt.id END)::int AS "terminalTaskCount",count(DISTINCT ka.id)::int AS "attemptCount",coalesce(sum(ka."providerCostUsd"),0)::text AS "providerCostUsd" FROM "KeywordResearch" kr LEFT JOIN "KeywordResearchStage" ks ON ks."researchId"=kr.id LEFT JOIN "KeywordResearchTask" kt ON kt."stageId"=ks.id LEFT JOIN "KeywordResearchProviderAttempt" ka ON ka."taskId"=kt.id WHERE kr.id=$1 GROUP BY kr.id`, id
    );
    if (mode === "artifactRows") return tx.$queryRawUnsafe(
      `SELECT kr."resultFingerprint",ks.stage::text,ks.generation,ks."createdAt" AS "stageCreatedAt",ks."manifestS3Key",ks."manifestFingerprint",ks."manifestProducedAt",kt.id,kt."itemKey",kt."inputFingerprint",kt."endpointKey",kt."requestFingerprint",kt.state::text,kt."artifactS3Key",kt."artifactFingerprint",kt."createdAt",kt."terminalAt" FROM "KeywordResearchStage" ks JOIN "KeywordResearch" kr ON kr.id=ks."researchId" LEFT JOIN "KeywordResearchTask" kt ON kt."stageId"=ks.id WHERE ks."researchId"=$1 ORDER BY ks.stage::text,kt."itemKey"`, id
    );
    return tx.$queryRawUnsafe(
      `SELECT h."runId",h."selectionRevision",h."clientRequestId",h."selectionFingerprint",r.state::text AS "runState",r.phase::text AS "runPhase",r.stage AS "runStage",r."confirmedQueryRevision",r."queriesConfirmedAt",r."resultsAvailable",jsonb_array_length(kr.selection->'items')::int AS "selectedItemCount",count(DISTINCT q.id)::int AS "queryCount",count(DISTINCT CASE WHEN (q."keywordResearchItemId" IS NOT NULL AND NOT EXISTS (SELECT 1 FROM jsonb_array_elements(kr.selection->'items') s WHERE s->>'sourceKind'='calculated' AND s->>'itemId'=q."keywordResearchItemId" AND s->>'keyword'=q.query)) OR (q."keywordResearchItemId" IS NULL AND NOT EXISTS (SELECT 1 FROM jsonb_array_elements(kr.selection->'items') s WHERE s->>'sourceKind'='manual' AND s->>'keyword'=q.query)) THEN q.id END)::int AS "lineageMismatchCount",count(DISTINCT ps.id)::int AS "pipelineStageCount",count(DISTINCT pt.id)::int AS "pipelineTaskCount",count(DISTINCT d.id)::int AS "dataForSeoLedgerCount",count(DISTINCT l.id)::int AS "leadCount",count(DISTINCT rs.id)::int AS "runStoreCount" FROM "KeywordResearchHandoff" h JOIN "KeywordResearch" kr ON kr.id=h."researchId" JOIN "Run" r ON r.id=h."runId" LEFT JOIN "RunQuery" q ON q."runId"=r.id LEFT JOIN "PipelineStage" ps ON ps."runId"=r.id LEFT JOIN "PipelineTask" pt ON pt."stageId"=ps.id LEFT JOIN "DataForSeoRequestLedger" d ON d."runId"=r.id LEFT JOIN "Lead" l ON l."runId"=r.id LEFT JOIN "RunStore" rs ON rs."runId"=r.id WHERE h."researchId"=$1 GROUP BY h.id,r.id,kr.id`, id
    );
  }, { maxWait: 5000, timeout: 30000 });
} finally {
  await prisma.$disconnect();
}
if (mode === "resolveResearch") {
  const row = one(raw, "KIW8_RESEARCH_CARDINALITY");
  process.stdout.write(`${JSON.stringify({mode,rowCount:1,nextStateResearchId:row.id,researchIdSha256:h(row.id),state:row.state,generation:row.generation,selectionRevision:row.selectionRevision})}\n`);
} else if (mode === "artifactRows") {
  process.stdout.write(`${JSON.stringify({mode,researchIdSha256:h(process.env.KIW8_RESEARCH_ID),rowCount:raw.length,rows:raw})}\n`);
} else {
  const row = one(raw, `KIW8_${mode.toUpperCase()}_CARDINALITY`);
  const safe = Object.fromEntries(Object.entries(row).map(([k,v]) =>
    [k, k === "runId" || k === "clientRequestId" || k === "selectionFingerprint" ? h(v) : v]));
  process.stdout.write(`${JSON.stringify({mode,researchIdSha256:mode === "baseline" ? null : h(process.env.KIW8_RESEARCH_ID),...safe})}\n`);
}
```

`artifactRows` raw keys/IDs are permitted only in the direct pipe to the §3.6
S3 observer and must not be appended to evidence. That observer replaces them
with hashes/counts before emitting. `resolveResearch.nextStateResearchId` is
permitted only in the parent A5 transition; S3/A6 retain only its hash. These
are the two explicit internal-channel exceptions to the safe evidence schema.

`ownerId` is obtained only by strict GET
`${KIW8_ORIGIN}/api/auth/get-session` with the named cookie; accepted response
keys are exactly `session` and `user`, and `user.id` must be nonempty. The
resolve query must return exactly one row; zero or multiple rows stops. The
runner's four evidence/internal schemas are exact:

```json
{"mode":"baseline","researchIdSha256":null,"nonterminalResearchCount":0}
{"mode":"resolveResearch","rowCount":1,"nextStateResearchId":"kr_<24 chars>","researchIdSha256":"64hex","state":"queued|running|completed|failed","generation":1,"selectionRevision":0}
{"mode":"progress","researchIdSha256":"64hex","state":"queued|running|completed|failed","generation":1,"progress":{"stage":"enum","expansion":{"expected":0,"terminal":0,"succeeded":0,"skipped":0,"failed":0},"anchorScreen":{"expected":0,"terminal":0,"succeeded":0,"skipped":0,"failed":0},"marketOverview":{"expected":0,"terminal":0,"succeeded":0,"skipped":0,"failed":0}},"resultFingerprint":"64hex-or-null","selectionRevision":0,"safeErrorCode":"string-or-null","stageCount":0,"taskCount":0,"terminalTaskCount":0,"attemptCount":0,"providerCostUsd":"decimal"}
{"mode":"handoff","researchIdSha256":"64hex","runId":"sha256","selectionRevision":0,"clientRequestId":"sha256","selectionFingerprint":"sha256","runState":"awaiting_query_confirmation","runPhase":"query_review","runStage":"string","confirmedQueryRevision":null,"queriesConfirmedAt":null,"resultsAvailable":false,"selectedItemCount":0,"queryCount":0,"lineageMismatchCount":0,"pipelineStageCount":0,"pipelineTaskCount":0,"dataForSeoLedgerCount":0,"leadCount":0,"runStoreCount":0}
```

`artifactRows` has the internal-only pipe schema frozen in the source above.
The parent copies the
reconciled literal ID into the next A5 action state; the executor does not
recover it by filename, history or a free-form query. Baseline requires `0`;
progress requires one row and monotonic task/attempt/stage/research changes;
handoff requires one row, `selectedItemCount=queryCount` in `1..100`,
`lineageMismatchCount=0`, `awaiting_query_confirmation/query_review`,
confirmation fields null, results false and every downstream count zero.

### 3.6 Exact AWS dynamic observers

Stack outputs are resolved only by
`aws cloudformation describe-stacks --stack-name storesignal-production-pipeline`
and exact `OutputKey`; no name guessing is allowed. The source queue is
`KeywordResearchQueueUrl`. The DLQ name is the last ARN segment of
`KeywordResearchDlqArn`, resolved to a URL only with `aws sqs get-queue-url`.
The downstream no-confirmation baseline uses exactly source/check output keys
`DiscoveryQueueUrl`, `DiscoveryCheckQueueUrl`, `LeadQueueUrl`,
`LeadCheckQueueUrl`, `TrafficQueueUrl`, `TrafficCheckQueueUrl` and DLQ ARN keys
`DiscoveryDlqArn`, `DiscoveryCheckDlqArn`, `LeadDlqArn`, `LeadCheckDlqArn`,
`TrafficDlqArn`, `TrafficCheckDlqArn`; every DLQ URL uses the same
last-ARN-segment plus `get-queue-url` formula. Capture all 12 projections once
immediately before handoff and once immediately after the durable handoff row;
their sorted canonical JSON must be byte-equal.
For each queue the only command is `aws sqs get-queue-attributes --attribute-names
ApproximateNumberOfMessages ApproximateNumberOfMessagesNotVisible
ApproximateNumberOfMessagesDelayed RedrivePolicy VisibilityTimeout
MessageRetentionPeriod`; the strict safe output is the six named numeric/string
members with queue URL replaced by SHA-256. Polling is every 5 seconds for at
most 120 seconds while disabled and every 15 seconds under the live watchdog.

The KeywordWorker identity is the final ARN segment of
`KeywordWorkerFunctionArn`. Lambda configuration is read only with
`aws lambda get-function-configuration --function-name <derived-name>` and
`aws lambda get-function-concurrency --function-name <derived-name>`; accepted
fields are `State`, `LastUpdateStatus`, `Timeout`, `MemorySize`, `EphemeralStorage.Size`
and reserved concurrency, with environment values reduced to exact key set plus
SHA-256 values. Mapping is read only with `aws lambda list-event-source-mappings
--function-name <derived-name> --event-source-arn <KeywordResearchQueueArn>`;
exact fields are `UUID`, `State`, `BatchSize`, `MaximumBatchingWindowInSeconds`,
`FunctionResponseTypes` and absence of `ScalingConfig.MaximumConcurrency`.
The zero-downstream metric set derives exactly six function identities from
`DiscoveryWorkerFunctionArn`, `DomainAggregatorFunctionArn`,
`LeadWorkerFunctionArn`, `LeadAggregatorFunctionArn`,
`TrafficWorkerFunctionArn`, and `FinalAggregatorFunctionArn`. It runs the same
metric query below for each and requires invocation/error/throttle deltas zero
from the pre-handoff instant through the post-handoff durable observation.

Alarm names come only from the 31 physical `AWS::CloudWatch::Alarm` resources
returned by `list-stack-resources`. The sole alarm read is
`aws cloudwatch describe-alarms --alarm-names <sorted exact names>`; safe output
is sorted `{AlarmName,StateValue,StateUpdatedTimestamp}` and passes only for
`OK`, or `INSUFFICIENT_DATA` with no action and a pre-ACT05 timestamp. Lambda
metric reads use `aws cloudwatch get-metric-data` with exact one-minute Sum
queries for `Invocations`, `Errors`, `Throttles` and Maximum `Duration`,
dimension `FunctionName=<derived-name>`, bounded by `KIW8_WINDOW_STARTED_AT` and
the current observation instant. Output is counts/max duration only.

The literal `--metric-data-queries` JSON is
`[{"Id":"invocations","MetricStat":{"Metric":{"Namespace":"AWS/Lambda","MetricName":"Invocations","Dimensions":[{"Name":"FunctionName","Value":"<derived-name>"}]},"Period":60,"Stat":"Sum"},"ReturnData":true},{"Id":"errors","MetricStat":{"Metric":{"Namespace":"AWS/Lambda","MetricName":"Errors","Dimensions":[{"Name":"FunctionName","Value":"<derived-name>"}]},"Period":60,"Stat":"Sum"},"ReturnData":true},{"Id":"throttles","MetricStat":{"Metric":{"Namespace":"AWS/Lambda","MetricName":"Throttles","Dimensions":[{"Name":"FunctionName","Value":"<derived-name>"}]},"Period":60,"Stat":"Sum"},"ReturnData":true},{"Id":"duration","MetricStat":{"Metric":{"Namespace":"AWS/Lambda","MetricName":"Duration","Dimensions":[{"Name":"FunctionName","Value":"<derived-name>"}]},"Period":60,"Stat":"Maximum"},"ReturnData":true}]`.
The command also has literal `--scan-by TimestampAscending --query
'MetricDataResults[].{Id:Id,StatusCode:StatusCode,Timestamps:Timestamps,Values:Values}'`;
every StatusCode must be `Complete` and pagination is forbidden.

Log reads use `aws logs filter-log-events` on exact group
`/aws/lambda/<derived-name>`, start time `KIW8_WINDOW_STARTED_AT`, end time the
observation instant, `--limit 10000`; the JSON is piped directly to an in-memory
Node projector. It emits event count, safe error-code histogram and forbidden
match count only. Forbidden expressions are case-insensitive
`authorization|cookie|password|credential|private[_ -]?key|DATAFORSEO_(LOGIN|PASSWORD)|DATABASE_URL|SecretString|BEGIN (RSA|PRIVATE)`;
it never emits messages. A pagination token or 10000 events stops
`PARENT_BLOCKED_LOG_SCAN_INCOMPLETE` rather than silently truncating.

S3 bucket identity is exact `ArtifactBucketName`. The artifact observer receives
only the rows from `KIW8-DB-V1`, constructs `S3ArtifactStore` with max bytes
`33554432`, and calls `getValidated` for every succeeded task, every nonnull
stage manifest and deterministic `keywordResultKey(researchId,generation)`.
Schema mapping is exact: expansion task -> `keywordExpansionResultSchema`;
anchor task -> `keywordAnchorScreenResultSchema`; market task ->
`keywordMarketOverviewResultSchema`; stage manifests -> the corresponding
expansion/shortlist/market manifest schema; result ->
`keywordResearchResultArtifactSchema`. Expected metadata uses the DB
input/content fingerprints and produced-at fields exactly as service.js does.
The only output is `{validatedObjects,validatedBytes,versioned:true,
encrypted:true,fingerprintMismatches:0,metadataMismatches:0}`. `HeadObject` for
each key must additionally show AES256 and a nonempty VersionId. No raw object
body/key is emitted.

The artifact observer is the following exact inline Node source, invoked from
`email_scraper/` only as the direct stdin consumer of `KIW8-DB-V1 artifactRows`:

```javascript
import { execFileSync } from "node:child_process";
import { S3Client, GetObjectCommand } from "@aws-sdk/client-s3";
import { canonicalJson, sha256Hex } from "./src/aws-pipeline/core/canonical.js";
import { keywordResultKey, keywordStageInputFingerprint } from "./src/aws-pipeline/keyword-intelligence/keys.js";
import { resultFingerprint } from "./src/keyword-intelligence/pipeline.js";
import {
  keywordExpansionResultSchema, keywordExpansionManifestSchema,
  keywordAnchorScreenResultSchema, keywordShortlistManifestSchema,
  keywordMarketOverviewResultSchema, keywordMarketOverviewManifestSchema,
  keywordResearchResultArtifactSchema
} from "./src/aws-pipeline/keyword-intelligence/contracts.js";
let input = "";
for await (const chunk of process.stdin) input += chunk;
const envelope = JSON.parse(input);
if (envelope.mode !== "artifactRows" || !Array.isArray(envelope.rows)) throw new Error("KIW8_ARTIFACT_INPUT");
const researchId = process.env.KIW8_RESEARCH_ID;
const stack = JSON.parse(execFileSync("aws", ["cloudformation", "describe-stacks",
  "--stack-name", "storesignal-production-pipeline", "--profile", "storesignal-dev",
  "--region", "ap-south-2", "--no-cli-pager", "--output", "json"],
  { encoding: "utf8", maxBuffer: 16777216 })).Stacks?.[0];
const outputs = Object.fromEntries((stack?.Outputs || []).map((x) => [x.OutputKey, x.OutputValue]));
if (typeof outputs.ArtifactBucketName !== "string") throw new Error("KIW8_BUCKET_OUTPUT");
const s3 = new S3Client({ region: "ap-south-2", maxAttempts: 3 });
const taskSchema = { expansion: keywordExpansionResultSchema,
  anchor_screen: keywordAnchorScreenResultSchema, market_overview: keywordMarketOverviewResultSchema };
const manifestSchema = { expansion: keywordExpansionManifestSchema,
  anchor_screen: keywordShortlistManifestSchema, market_overview: keywordMarketOverviewManifestSchema };
let validatedObjects = 0, validatedBytes = 0;
async function validate(key, schema, expected) {
  const response = await s3.send(new GetObjectCommand({ Bucket: outputs.ArtifactBucketName, Key: key }));
  if (response.ServerSideEncryption !== "AES256" || typeof response.VersionId !== "string" || !response.VersionId)
    throw new Error("KIW8_ARTIFACT_STORAGE");
  const chunks = []; let bytes = 0;
  for await (const raw of response.Body) { const chunk = Buffer.from(raw); bytes += chunk.length;
    if (bytes > 33554432) throw new Error("KIW8_ARTIFACT_SIZE"); chunks.push(chunk); }
  if (Number.isFinite(response.ContentLength) && response.ContentLength !== bytes)
    throw new Error("KIW8_ARTIFACT_LENGTH");
  const text = Buffer.concat(chunks).toString("utf8"), value = schema.parse(JSON.parse(text));
  if (canonicalJson(value) !== text) throw new Error("KIW8_ARTIFACT_CANONICAL");
  const content = sha256Hex(text), metadata = Object.fromEntries(
    Object.entries(response.Metadata || {}).map(([k,v]) => [k.toLowerCase(), String(v)]));
  const wanted = { "contract-version": String(value.contractVersion), "run-id": researchId,
    stage: expected.stage, generation: String(expected.generation), "item-id": expected.itemId,
    "input-sha256": expected.inputFingerprint, "content-sha256": content,
    "produced-at": expected.producedAt };
  if (JSON.stringify(Object.keys(metadata).sort()) !== JSON.stringify(Object.keys(wanted).sort()) ||
      Object.entries(wanted).some(([k,v]) => metadata[k] !== String(v)) ||
      expected.contentFingerprint && expected.contentFingerprint !== content)
    throw new Error("KIW8_ARTIFACT_METADATA");
  validatedObjects++; validatedBytes += bytes;
  return { value, contentFingerprint: content };
}
for (const row of envelope.rows.filter((x) => x.state === "succeeded")) {
  if (!row.artifactS3Key || !row.artifactFingerprint) throw new Error("KIW8_TASK_ARTIFACT_MISSING");
  await validate(row.artifactS3Key, taskSchema[row.stage], { stage: row.stage,
    generation: row.generation, itemId: row.itemKey, inputFingerprint: row.inputFingerprint,
    contentFingerprint: row.artifactFingerprint, producedAt: new Date(row.createdAt).toISOString() });
}
const stages = [...new Map(envelope.rows.map((x) => [x.stage, x])).values()];
for (const row of stages) {
  if (!row.manifestS3Key || !row.manifestFingerprint || !row.manifestProducedAt)
    throw new Error("KIW8_MANIFEST_MISSING");
  const stageTasks=envelope.rows.filter((x)=>x.stage===row.stage).map((x)=>({itemKey:x.itemKey,
    inputFingerprint:x.inputFingerprint,endpointKey:x.endpointKey,requestFingerprint:x.requestFingerprint}));
  const stageInputFingerprint=keywordStageInputFingerprint({researchId,generation:row.generation,
    stage:row.stage,tasks:stageTasks});
  await validate(row.manifestS3Key, manifestSchema[row.stage], { stage: row.stage,
    generation: row.generation, itemId: "manifest", inputFingerprint: stageInputFingerprint,
    contentFingerprint: row.manifestFingerprint, producedAt: new Date(row.stageCreatedAt).toISOString() });
}
const market = stages.find((x) => x.stage === "market_overview");
if (!market) throw new Error("KIW8_MARKET_STAGE_MISSING");
const resultKey = keywordResultKey(researchId, market.generation);
const marketTasks=envelope.rows.filter((x)=>x.stage==="market_overview").map((x)=>({itemKey:x.itemKey,
  inputFingerprint:x.inputFingerprint,endpointKey:x.endpointKey,requestFingerprint:x.requestFingerprint}));
const resultInputFingerprint=keywordStageInputFingerprint({researchId,generation:market.generation,
  stage:"market_overview",tasks:marketTasks});
const storedResult=await validate(resultKey, keywordResearchResultArtifactSchema, { stage: "market_overview",
  generation: market.generation, itemId: "result", inputFingerprint: resultInputFingerprint,
  contentFingerprint: null, producedAt: new Date(market.stageCreatedAt).toISOString() });
if (resultFingerprint({...storedResult.value,contractVersion:1})!==market.resultFingerprint)
  throw new Error("KIW8_RESULT_FINGERPRINT");
process.stdout.write(`${JSON.stringify({validatedObjects,validatedBytes,versioned:true,
  encrypted:true,fingerprintMismatches:0,metadataMismatches:0})}\n`);
```

No ListObjects operation, prefix scan, alternate key, schema fallback or body
logging is permitted.

### 3.7 Exact production frontend/API runner (`KIW8-API-V1`)

Every positive HTTP operation is executed from `frontend/` by Node 20+ with
`--experimental-strip-types --input-type=module`. Each literal command imports
`parseResearchEnvelope`, `parseRunHandoffEnvelope` and
`CLIENT_REQUEST_ID_PATTERN` from
`./lib/keyword-intelligence-validation.ts`; no handwritten success parser is
permitted. These are the exact commands (whitespace-only shell reflow is the
only freedom):

```text
node --experimental-strip-types --input-type=module -e 'import{createHash}from"node:crypto";import{parseResearchEnvelope}from"./lib/keyword-intelligence-validation.ts";const origin=process.env.KIW8_ORIGIN,cookie=process.env.KIW8_OWNER_A_COOKIE,seed=process.env.KIW8_APPROVED_SEED,r=await fetch(`${origin}/api/keyword-research`,{method:"POST",headers:{Accept:"application/json","Content-Type":"application/json",Cookie:cookie},body:JSON.stringify({seeds:[seed]}),redirect:"error",signal:AbortSignal.timeout(20000)}),body=await r.json();if(r.status!==202)throw Error("KIW8_CREATE_STATUS");const v=parseResearchEnvelope(body);if(!/^kr_[A-Za-z0-9_-]{24}$/u.test(v.id)||v.state!=="queued"||v.generation!==1||v.contractVersion!==1||v.selectionRevision!==0||v.result!==null||v.safeError!==null||v.seeds.length!==1||v.seeds[0]!==seed)throw Error("KIW8_CREATE_CONTRACT");console.log(JSON.stringify({mode:"create",status:r.status,researchIdSha256:createHash("sha256").update(v.id).digest("hex"),state:v.state,generation:v.generation,selectionRevision:v.selectionRevision}))'

node --experimental-strip-types --input-type=module -e 'import{createHash}from"node:crypto";import{parseResearchEnvelope}from"./lib/keyword-intelligence-validation.ts";const origin=process.env.KIW8_ORIGIN,cookie=process.env.KIW8_OWNER_A_COOKIE,id=process.env.KIW8_RESEARCH_ID,r=await fetch(`${origin}/api/keyword-research/${encodeURIComponent(id)}`,{headers:{Accept:"application/json",Cookie:cookie},redirect:"error",signal:AbortSignal.timeout(20000)}),body=await r.json();if(r.status!==200)throw Error("KIW8_POLL_STATUS");const v=parseResearchEnvelope(body);if(v.id!==id)throw Error("KIW8_POLL_ID");console.log(JSON.stringify({mode:"poll",researchIdSha256:createHash("sha256").update(id).digest("hex"),state:v.state,progress:v.progress,selectionCount:v.selection.length,selectionRevision:v.selectionRevision,resultKeywordCount:v.result?.keywords.length??0,safeErrorCode:v.safeError?.code??null}))'

node --experimental-strip-types --input-type=module -e 'import{createHash}from"node:crypto";import{parseResearchEnvelope,parseRunHandoffEnvelope}from"./lib/keyword-intelligence-validation.ts";const h=x=>createHash("sha256").update(x).digest("hex"),origin=process.env.KIW8_ORIGIN,cookie=process.env.KIW8_OWNER_A_COOKIE,other=process.env.KIW8_OWNER_B_COOKIE,id=process.env.KIW8_RESEARCH_ID,started=process.env.KIW8_WINDOW_STARTED_AT,request=async(path,init={})=>{const r=await fetch(`${origin}${path}`,{...init,headers:{Accept:"application/json",...init.headers,Cookie:cookie},redirect:"error",signal:AbortSignal.timeout(20000)});return{r,body:await r.json()}};const page=await fetch(`${origin}/keywords/${encodeURIComponent(id)}`,{headers:{Cookie:cookie},redirect:"error",signal:AbortSignal.timeout(20000)}),html=await page.text();if(page.status!==200||!String(page.headers.get("content-type")).startsWith("text/html")||page.url!==`${origin}/keywords/${encodeURIComponent(id)}`||!html.includes("Loading keyword research"))throw Error("KIW8_DASHBOARD_CONTRACT");let x=await request(`/api/keyword-research/${encodeURIComponent(id)}`);if(x.r.status!==200)throw Error("KIW8_RESEARCH_GET_STATUS");const before=parseResearchEnvelope(x.body);if(before.state!=="completed"||before.selection.length<1||before.selection.length>100||before.selectionRevision<1||before.selectionConflicts.length)throw Error("KIW8_SELECTION_PRECONDITION");process.stdout.write(`${JSON.stringify({mode:"selection-preflight",selectionRevision:before.selectionRevision,selectionCount:before.selection.length,selectionSha256:h(JSON.stringify(before.selection))})}\n`);const items=before.selection.map(v=>v.sourceKind==="calculated"?{sourceKind:"calculated",sourceKeywordId:v.sourceKeywordId,keyword:v.keyword}:{sourceKind:"manual",keyword:v.keyword});x=await request(`/api/keyword-research/${encodeURIComponent(id)}/selection`,{method:"PUT",headers:{"Content-Type":"application/json"},body:JSON.stringify({expectedRevision:before.selectionRevision,items})});if(x.r.status!==200)throw Error("KIW8_SELECTION_STATUS");const saved=parseResearchEnvelope(x.body);if(saved.selectionRevision!==before.selectionRevision+1||JSON.stringify(saved.selection)!==JSON.stringify(before.selection)||saved.selectionConflicts.length)throw Error("KIW8_SELECTION_SAVE_CONTRACT");const key=`kiw8_${h(`${id}\n${saved.selectionRevision}\n${started}`).slice(0,60)}`;x=await request(`/api/keyword-research/${encodeURIComponent(id)}/runs`,{method:"POST",headers:{"Content-Type":"application/json"},body:JSON.stringify({expectedSelectionRevision:saved.selectionRevision,clientRequestId:key})});if(x.r.status!==201)throw Error("KIW8_HANDOFF_STATUS");const handoff=parseRunHandoffEnvelope(x.body);if(handoff.statusUrl!==`/api/runs/${handoff.run.id}`)throw Error("KIW8_HANDOFF_CONTRACT");for(const [name,path,code]of[["research",`/api/keyword-research/${encodeURIComponent(id)}`,"KEYWORD_RESEARCH_NOT_FOUND"],["run",`/api/runs/${encodeURIComponent(handoff.run.id)}`,"RUN_NOT_FOUND"]]){const r=await fetch(`${origin}${path}`,{headers:{Accept:"application/json",Cookie:other},redirect:"error",signal:AbortSignal.timeout(20000)}),v=await r.json();if(r.status!==404||Object.keys(v).join(",")!=="error"||!v.error||Object.keys(v.error).sort().join(",")!=="code,message"||v.error.code!==code)throw Error(`KIW8_OWNER_B_${name.toUpperCase()}`)}console.log(JSON.stringify({mode:"save-handoff",dashboardStatus:page.status,dashboardBytes:Buffer.byteLength(html),dashboardSha256:h(html),selectionSaved:true,selectionRevision:saved.selectionRevision,selectionCount:saved.selection.length,selectionSha256:h(JSON.stringify(saved.selection)),runIdSha256:h(handoff.run.id),clientRequestIdSha256:h(key),handoffStatus:x.r.status,ownerBResearchStatus:404,ownerBRunStatus:404,privateProjectionCount:0}))'
```

The following rules are additional acceptance constraints on those literal
commands:

1. `create` sends exactly one `POST /api/keyword-research` with body
   `JSON.stringify({seeds:[process.env.KIW8_APPROVED_SEED]})`, owner-A cookie,
   the headers in §3.1, redirect `error` and a 20-second abort. It requires 202,
   parses with `parseResearchEnvelope`, and requires ID regex
   `^kr_[A-Za-z0-9_-]{24}$`, state `queued`, generation `1`, contractVersion
   `1`, selection revision `0`, null result, exactly the normalized seed and no
   safe error. Output is exactly
   `{mode:"create",status:202,researchIdSha256,state,generation,selectionRevision}`.
2. A create transport loss is never retried. `KIW8-DB-V1 resolveResearch`
   executes once with owner-A, seed and `KIW8_WINDOW_STARTED_AT`; exactly one
   row reconciles success, zero rows reconciles rollback, multiple rows stops
   `PARENT_BLOCKED_SECOND_CANARY`. This is the create ambiguity protocol; there
   is no invented idempotency key or second POST.
3. `poll` obtains the ID only from current A5 `kiw8_research_id`, sends exact
   `GET /api/keyword-research/${encodeURIComponent(id)}`, requires 200 and
   `parseResearchEnvelope`, and emits only state, progress counters, selection
   count/revision, result-keyword count, safe error code and SHA-256 IDs. It
   runs every 15 seconds, with a 15-minute no-durable-progress watchdog and a
   four-hour absolute ceiling. GET transport loss may be repeated once because
   it is read-only; a second loss stops.
4. `save-handoff` first sends exact owner-A `GET /keywords/${id}`, requires 200,
   `content-type` beginning `text/html`, final URL unchanged and body containing
   `Loading keyword research`; it records only byte length and SHA-256. It then
   GETs/parses the completed research and **always** sends one selection PUT;
   there is no conditional save branch. The PUT body is exactly
   `{expectedRevision:view.selectionRevision,items}` where calculated items are
   `{sourceKind:"calculated",sourceKeywordId,keyword}` and manual items are
   `{sourceKind:"manual",keyword}`. It requires 200, exact selection equality,
   revision `prior+1`, no conflicts and item count `1..100`.
5. Selection PUT ambiguity is reconciled once by owner-A GET. Exact saved items
   plus revision `prior+1` and the preflight `selectionSha256` is success;
   unchanged revision/items is rollback;
   every other state stops `PARENT_BLOCKED_SELECTION_AMBIGUITY`. The PUT is not
   repeated.
6. The run key is deterministic and reconstructible:
   `clientRequestId="kiw8_"+sha256(researchId+"\n"+savedRevision+"\n"+KIW8_WINDOW_STARTED_AT).slice(0,60)`.
   It must match `CLIENT_REQUEST_ID_PATTERN`. POST path is exact
   `/api/keyword-research/${encodeURIComponent(id)}/runs`; body is exactly
   `{expectedSelectionRevision:savedRevision,clientRequestId}`. Require 201 on
   first creation or 200 only during same-key ambiguity reconciliation, parse
   with `parseRunHandoffEnvelope`, and require status URL
   `/api/runs/${run.id}`. On lost response the same POST body/key may execute
   once; any unequal ID/fingerprint or second loss stops.
7. The final command sends only owner-B GETs for the exact research route and exact
   `/api/runs/${encodeURIComponent(runId)}`. Each must return the contract's
   authenticated 404/not-found response. The strict error parser accepts only
   `{error:{code,message}}`, code `KEYWORD_RESEARCH_NOT_FOUND` for research and
   `RUN_NOT_FOUND` for run; any private top-level member or
   200 is failure. Output is exactly
   Its safe output includes exactly `ownerBResearchStatus:404`,
   `ownerBRunStatus:404` and `privateProjectionCount:0`.

The module never logs cookies, seed, raw payloads, selection text, IDs, URLs or
error messages. Its first safe line is exactly
`{mode:"selection-preflight",selectionRevision,selectionCount,selectionSha256}`;
its second safe line is
`{mode:"save-handoff",dashboardStatus:200,dashboardBytes,dashboardSha256,
selectionSaved:true,selectionRevision,selectionCount,selectionSha256,runIdSha256,
clientRequestIdSha256,handoffStatus,ownerBResearchStatus,ownerBRunStatus,
privateProjectionCount}`.

## 4. Coverage and control matrix

| ID | Registration | Activation witness | Exact oracle / forbidden result |
|---|---|---|---|
| `W8-LIVE-01` | `I001-PREFLIGHT` | P1-P6 each produced sanitized PASS evidence | account/region/stack/quota/secret/provider/host/packet baseline exact; zero mutation/paid call |
| `W8-LIVE-02` | `I001-ACT01` | three versioned S3 objects plus reviewed full change-set ID | object hashes/bytes/metadata/AES256/version IDs equal W7; change projection equals allowlist; zero execute |
| `W8-LIVE-03` | `I001-ACT02` | stack update complete and expected-disabled inspector returns | 82 resources/34 outputs/19 parameters; keyword mapping disabled; recovery/worker flag false; established topology active; queue/DLQ zero |
| `W8-LIVE-04` | `I001-ACT03` | P2-observed host readback after approved update | only policy attachment plus two named values; enabled literal true and queue URL hash equals stack output; no value logged |
| `W8-LIVE-05` | `I001-ACT04` | normal authenticated POST 202 and durable/queue read | one research ID; state queued; exactly one visible source message; zero not-visible/delayed/DLQ/worker-log/provider-attempt/cost |
| `W8-LIVE-06` | `I001-ACT05-06` | expected-active inspector plus same research stage progress | reviewed activation consumed original message through event mapping/worker/recovery; no direct invoke/send |
| `W8-LIVE-07` | `I001-LIVE` | terminal attempt/task/stage rows for same research | nonempty-shortlist planned first-pass logical work is exactly `11`; actual first-pass network calls are `0..11` only through durable cache reuse; attempts `<=55`; durable USD `<=3.00000000`; exact observed call/attempt/throttle/retry counts recorded |
| `W8-LIVE-08` | `I001-LIVE` | every terminal task's S3 object reconciles to its Neon key/fingerprint and final result | private encrypted versioned immutable objects; nonempty fenced result/default selection; owner A visible only |
| `W8-LIVE-09` | `I001-HANDOFF` | dashboard selection save and one normal run-handoff POST | one immutable Run, `1..100` RunQueries, exact lineage; Run unconfirmed; zero PipelineStage/PipelineTask/downstream messages/calls |
| `W8-CONF-01` | `I001-CONFORMANCE` | final registry executed after all preceding witnesses | required=registered=executed=activated ten; six controls falsified; exact digests; action ledger is an allowed prefix of ACT01..06 plus failure-only ACT07 and contains no unapproved/extra/second-canary/confirm action |

| ID | Safe execution | Expected falsification witness |
|---|---|---|
| `W8-NC-01` | replace one in-memory packet SHA with 64 zeroes and run the preflight equality function; no file/AWS write | hash guard rejects before ACT-01 |
| `W8-NC-02` | call exported `assertReviewedChanges("full", syntheticDescription)` with exactly one extra unlisted Add member | throws allowlist error; zero execute/AWS call |
| `W8-NC-03` | real ACT-04 disabled observation | same research queued; visible=1; not-visible=0; provider attempts/cost/worker logs=0 |
| `W8-NC-04` | before ACT-05 approval exists, invoke the accepted activation command with `--execute`; `requireApproval` runs before `assertTarget` | exits nonzero `Exact KI-W8 phase/action approval is absent or stale`; mapping remains disabled; zero AWS call |
| `W8-NC-05` | owner B GETs owner A research and run through normal authenticated routes | exact 404/not-found or authenticated denial; no private field/result projection |
| `W8-NC-06` | add one synthetic second-canary or Run-confirm action to an in-memory action ledger and run conformance comparison | exact action-set/prefix validator rejects before action |

The execution registry is the literal 16-row matrix above. A case/control is
recorded as executed only after its activation witness and complete oracle pass.
A name in prose, a selected command, or an aggregate count is not execution.

## 5. Substitute fidelity and accepted-evidence policy

| Boundary | Substitute/control | Fidelity and claim limit |
|---|---|---|
| W7 source/packet | local `buildDeploymentPacket()` with P2 account | exact source bytes/key/token formula; proves packet identity, not AWS presence |
| change-set rejection | exported `assertReviewedChanges` synthetic description | exact production allowlist parser; proves rejection logic, not live CloudFormation semantics |
| action ledger controls | in-memory copies of exact case/action sets | exact set/prefix logic only; cannot prove live mutations |
| API/UI | none for positive canary | real authenticated production frontend/backend required |
| SQS/Lambda/S3/Neon | none for positive canary | real production boundaries required; queue attributes are observation only, never completion |
| provider | none for ACT-06 | real DataForSEO calls only after ACT-06 approval; P5 uses only an evidence-backed zero-charge capability boundary |

Accepted W7 source, template, ZIPs, tests and evidence are read-only. Any source,
test, fixture, template or ZIP change invalidates P1/P6 and all later action
evidence. A change after a stateful action stops for parent adjudication; no
repeat/second canary is permitted.

## 6. `KI-W8-I001` — personal sequential live assessment

```yaml
subwindow_id: KI-W8-I001
type: INTEGRATION_ASSESSMENT
parent_window_id: KI-W8
parent_assignment_id: ASG-KI-W8-WA-EXEC-PENDING
assigned_agent: WINDOW-AGENT
predecessors: [parent_approved_decomposition, accepted_KI-W7]
successor_reserved_for: parent
authorized_write_file: NONE_FOR_IMPLEMENTATION
planned_implementation_changed_file_set: []
planned_implementation_changed_file_set_digest: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
read_only_scope: [A1-A8, both standards, accepted W7 source/tests/build artifacts/evidence, P1-P6 approved production read surfaces, owner-scoped API/UI and canary rows/artifacts]
authorized_actions: [P1-P6 only at initial execution assignment; later action only when current A5 grants its exact W8-ACT ID]
prohibited_actions: [leaf delegation, implementation edit, unapproved external action, second canary, downstream confirmation, destructive cleanup, commit, push, final acceptance]
may_start_successor: false
```

### 6.1 Entry preflight (`P1`)

Before any network command:

1. read A5 and require a new execution assignment naming this S1 SHA, this
   window agent, `KI-W8`, accepted-through W7 and only read-only P1-P6 actions;
2. recompute both standards and A1-A4/A8 hashes;
3. require backend/frontend clean at the parent-pinned committed revisions and
   record the root coordination-only status;
4. hash/stat the three W7 packet inputs and compare §1.1 exactly;
5. validate local template JSON is 82 resources, 34 outputs, 19 parameters;
6. require zero source/test/schema/package/frontend diff from the accepted W7
   baselines; and
7. register P1 but do not execute `W8-LIVE-01` until P2-P6 all pass.

Any mismatch stops `PARENT_BLOCKED_PREFLIGHT_DRIFT`, performs no external call
after the mismatch, and records exact changed path/hash only.

### 6.2 Read-only applied preflight (`P2`–`P6`)

All AWS reads use §3.1's suffix and sanitization. They may run with network
sandbox escalation after the execution assignment; escalation is not action
authority.

`P2` executes exactly these seven CLI operations in order:

```text
aws sts get-caller-identity --query '{Account:Account,Arn:Arn}'
aws cloudformation describe-stacks --stack-name storesignal-production-pipeline --query 'Stacks[0].{StackId:StackId,StackStatus:StackStatus,EnableTerminationProtection:EnableTerminationProtection,Parameters:Parameters,Outputs:Outputs}'
aws cloudformation list-stack-resources --stack-name storesignal-production-pipeline --query 'StackResourceSummaries[].{LogicalResourceId:LogicalResourceId,PhysicalResourceId:PhysicalResourceId,ResourceType:ResourceType,ResourceStatus:ResourceStatus}'
aws cloudformation list-change-sets --stack-name storesignal-production-pipeline --query 'Summaries[].{ChangeSetId:ChangeSetId,Status:Status,ExecutionStatus:ExecutionStatus}'
aws lambda list-event-source-mappings --query 'EventSourceMappings[].{UUID:UUID,EventSourceArn:EventSourceArn,FunctionArn:FunctionArn,State:State,BatchSize:BatchSize,MaximumBatchingWindowInSeconds:MaximumBatchingWindowInSeconds,FunctionResponseTypes:FunctionResponseTypes,ScalingConfig:ScalingConfig}'
aws events list-rules --name-prefix storesignal-production-pipeline --query 'Rules[].{Name:Name,Arn:Arn,State:State,ScheduleExpression:ScheduleExpression}'
aws logs describe-log-groups --log-group-name-prefix /aws/lambda/storesignal-production-pipeline- --query 'logGroups[].{logGroupName:logGroupName,retentionInDays:retentionInDays,storedBytes:storedBytes}'
```

The stdout of each is piped to a strict in-memory projector. Its exact output is
`{accountSha256,accountLast4,callerArnSha256,stackIdSha256,stackStatus,
terminationProtection,parameterKeys,outputKeys,resourceTypeCounts,
pendingChangeSetCount,mappingCount,ruleCount,logGroupCount}`. Parameter/output
values, physical IDs and ARNs become SHA-256 before emission. Pass requires a
12-digit account, `CREATE_COMPLETE|UPDATE_COMPLETE`, zero change sets whose
status is `CREATE_PENDING|CREATE_IN_PROGRESS|CREATE_COMPLETE` with execution
`AVAILABLE|EXECUTE_IN_PROGRESS`, and every existing resource status complete.
Then execute only §3.2 host discovery. Missing/invalid host observation records
the named DG-W8-05 block; it does not authorize ACT-03.

`P3` executes exactly:

```text
aws lambda get-account-settings --query '{AccountLimit:AccountLimit,AccountUsage:AccountUsage}'
aws service-quotas list-service-quotas --service-code lambda --query 'Quotas[].{QuotaName:QuotaName,Value:Value,Adjustable:Adjustable}'
aws service-quotas list-service-quotas --service-code sqs --query 'Quotas[].{QuotaName:QuotaName,Value:Value,Adjustable:Adjustable}'
aws service-quotas list-service-quotas --service-code cloudformation --query 'Quotas[].{QuotaName:QuotaName,Value:Value,Adjustable:Adjustable}'
```

The projector emits only sorted quota-name/value pairs and these booleans:
`reservedConcurrency1`, `timeout180`, `memory1024`, `ephemeral512`,
`zip47185920`, `expanded209715200`, `message262144`, `visibility1080`,
`retention345600`, `dlqRetention1209600`, `redrive5`, `batch1`, `window0`,
`maximumConcurrencyAbsent`. Every boolean must be true; an absent/unreadable
quota or capacity below the applied request takes `DG-W8-02`.

`P4` derives `PipelineSecretArn` only from the P2 stack output, then executes:

```text
aws secretsmanager describe-secret --secret-id "$KIW8_PIPELINE_SECRET_ARN" --query '{ARN:ARN,RotationEnabled:RotationEnabled,VersionIdsToStages:VersionIdsToStages}'
aws secretsmanager list-secret-version-ids --secret-id "$KIW8_PIPELINE_SECRET_ARN" --include-deprecated --query 'Versions[].{VersionId:VersionId,VersionStages:VersionStages}'
aws secretsmanager get-secret-value --secret-id "$KIW8_PIPELINE_SECRET_ARN" --version-stage AWSCURRENT --query '{SecretString:SecretString}' | node --input-type=module -e 'import{loadPipelineSecrets}from"./src/aws-pipeline/secrets.js";let b="";for await(const c of process.stdin)b+=c;const x=JSON.parse(b),s=await loadPipelineSecrets({client:{send:async()=>({SecretString:x.SecretString})},secretId:"AWSCURRENT"});console.log(JSON.stringify({strictSchema:true,databaseUrlPresent:!!s.databaseUrl,dataForSeoCredentialsNonempty:!!s.dataForSeoLogin&&!!s.dataForSeoPassword}))'
```

The first two responses must identify exactly one version carrying
`AWSCURRENT`. The pipeline prints only
`{"strictSchema":true,"databaseUrlPresent":true,"dataForSeoCredentialsNonempty":true}`.
The raw value exists only between the AWS process and parser. Any failure takes
`DG-W8-03`; another version/key/alias is forbidden.

`P5` follows §3.3. Under state 200 it stops with the exact parent blocker and
makes zero provider calls. Only a later parent-repinned literal protocol can
activate its one official-source GET plus one documented zero-charge GET.

`P6` executes, in order:

1. from `email_scraper/`, `node scripts/measure-keyword-worker-package.js` then
   `node scripts/measure-lambda-packages.js`; no builder; exact W7 ZIP hashes,
   byte limits and cold-imported handler functions must pass;
2. `KIW8-DB-V1 baseline`; exact output has `nonterminalResearchCount:0`;
3. §3.6 queue observer when outputs exist; otherwise exact P2 output proves
   both keyword logical resources absent; when present, both queues have
   visible/not-visible/delayed `0`;
4. rerun P1 hashes and the P2 change-set query; require no drift and no pending
   change set; and
5. execute the literal decomposition lint in §7.2; require zero findings.

P1-P6 passing executes `W8-LIVE-01`. Then stop at
`AWAITING_REQUESTER_APPROVAL_ACT01`; do not prepare or call ACT-01 before the
parent records its exact approval state.

### 6.3 ACT-01 — upload and create/review disabled change set

After exact ACT-01 approval, run from `email_scraper/`:

```text
node scripts/keyword-intelligence/create-change-set.js --profile=storesignal-dev --region=ap-south-2 --stack=storesignal-production-pipeline --environment=production --phase=full --account-id=${KIW8_ACCOUNT_ID} --execute
```

The accepted command alone may upload the three versioned AES256 objects and
create the disabled change set. Require `CHANGE_SET_REVIEWED`, exact object
hashes/bytes/keys/nonempty version IDs, and the exact full allowlist: ten Adds;
direct Modify/False only for `ControlPlanePolicy`, `RecoveryRole`, `Recovery`;
zero-or-one exact `RecoveryInvokePermission` and `RecoverySchedule` dependency
members; no Remove/replacement True/unlisted/detail drift. Record the generated
record SHA and stable ID. Execute `W8-LIVE-02`, `W8-NC-01`, and `W8-NC-02`.
Stop `AWAITING_REQUESTER_APPROVAL_ACT02`; zero change-set execution.

### 6.4 ACT-02 — apply and inspect disabled deployment

After exact ACT-02 approval, run:

```text
node scripts/keyword-intelligence/create-change-set.js --profile=storesignal-dev --region=ap-south-2 --stack=storesignal-production-pipeline --environment=production --phase=full --account-id=${KIW8_ACCOUNT_ID} --execute --apply-reviewed-change-set
node scripts/keyword-intelligence/inspect-stack.js --profile=storesignal-dev --region=ap-south-2 --stack=storesignal-production-pipeline --account-id=${KIW8_ACCOUNT_ID} --expected-disabled
```

Require `REVIEWED_CHANGE_SET_APPLIED`, then
`EXPECTED_DISABLED_KEYWORD_STACK_VERIFIED` with 82 resources, 7 queues/DLQs,
8 functions, 7 mappings, 31 alarms, keyword inactive and source/DLQ counts
zero. Verify the recovery schedule and established six mappings remain enabled,
while KeywordResearchMapping is disabled and KeywordWorker/Recovery keyword
flags are false. Execute `W8-LIVE-03`. Stop
`AWAITING_REQUESTER_APPROVAL_ACT03`.

### 6.5 ACT-03 — host attachment/configuration

After exact ACT-03 approval, require §3.4's complete record and execute its
single literal update request once. The request body is mechanically constructed
from the two exact stack outputs, literal true and the P2 configuration revision;
the strict before/after canonical comparison must show no other configuration
member changed. Poll only the record's GET every 10 seconds for at most 600
seconds. The first healthy matching revision passes; provider failure, timeout,
extra response member, wrong policy/queue/flag, or any unrelated configuration
hash change stops `PARENT_BLOCKED_HOST_APPLY` and makes no second update.

Execute `W8-LIVE-04`. Run the exact expected-disabled stack inspector command in
§6.4, the §3.6 Lambda metric query and log-group query. Require the stack still
disabled and KeywordWorker invocation/event/log-stream deltas all zero. Stop
`AWAITING_REQUESTER_APPROVAL_ACT04`.

### 6.6 ACT-04 — create the sole disabled research

After exact ACT-04 approval, execute only the first literal `KIW8-API-V1`
command in §3.7. The seed/cookies remain process-only. Require its exact safe
202 projection. On transport ambiguity execute only `KIW8-DB-V1
resolveResearch`; apply §3.7 rule 2 and never repeat POST. The parent records the
single reconciled literal ID and hash in the subsequent ACT-05/06 A5 state.

Poll only §3.6's two queue projections every 5 seconds for at most 120 seconds.
Require source visible=`1`, not-visible=`0`, delayed=`0`, DLQ three counts zero.
Execute `KIW8-DB-V1 progress` and the exact §3.6 Lambda metric/log projections:
same research queued, stage/task/attempt counts zero, provider cost
`0.00000000`, result fingerprint absent, selection revision 0, KeywordWorker
invocation/log-event deltas zero. No ReceiveMessage/DeleteMessage is allowed.
Execute `W8-LIVE-05` and the real `W8-NC-03`. Execute `W8-NC-04` before any
ACT-05 approval and prove the activation command fails locally at approval
checking with zero AWS call. Stop `AWAITING_REQUESTER_APPROVAL_ACT05`.

### 6.7 ACT-05 plus ACT-06 — activate and allow the same paid research

The window agent obtains and records ACT-05 approval, then stops again if the
independent ACT-06 approval is absent. Only when current A5 contains both may it
run:

```text
node scripts/keyword-intelligence/create-change-set.js --profile=storesignal-dev --region=ap-south-2 --stack=storesignal-production-pipeline --environment=production --phase=activate --account-id=${KIW8_ACCOUNT_ID} --execute
```

Require `CHANGE_SET_REVIEWED`; exact direct Modify/False members only
`KeywordResearchMapping.Enabled`, `KeywordWorker.Environment`,
`Recovery.Environment`, plus the same optional exact Recovery dependencies.
The window agent records the ID/projection and, because ACT-05 and ACT-06 are
both current, runs:

```text
node scripts/keyword-intelligence/create-change-set.js --profile=storesignal-dev --region=ap-south-2 --stack=storesignal-production-pipeline --environment=production --phase=activate --account-id=${KIW8_ACCOUNT_ID} --execute --apply-reviewed-change-set
node scripts/keyword-intelligence/inspect-stack.js --profile=storesignal-dev --region=ap-south-2 --stack=storesignal-production-pipeline --account-id=${KIW8_ACCOUNT_ID} --expected-active
```

Require expected-active inspection, the original visible message becoming
not-visible/consumed through the event mapping, and the same research entering
running. No direct Lambda invoke or SQS Send/Receive/Delete is permitted.
Execute `W8-LIVE-06`.

Run the second literal `KIW8-API-V1` command plus `KIW8-DB-V1 progress`, §3.6
queue, metric, alarm and sanitized-log commands every 15 seconds. Fail
immediately on research failed, DLQ count >0, alarm `ALARM`, forbidden log
match, durable cost >3, attempt count >55, a second resolveResearch row, or any
downstream durable count. A 15-minute interval with no changed DB state/task/
attempt/stage terminal count fails; a four-hour absolute ceiling fails. Queue
emptiness and log text are not progress.

At completion require nonempty result and default selection; planned first-pass
logical work exactly `11` (2 expansion, 1 anchor, 8 markets), actual first-pass
network calls `0..11` only through durable cache reuse, total attempts at most
`55`, durable cost at most `3.00000000`, and record actual
duration/peak memory/artifact/message/task/attempt/throttle/retry values.
Run `KIW8-DB-V1 artifactRows` and §3.6's exact S3 observer; require all success
fields, nonempty result/default selection and every succeeded task/manifest/result
object validated. S3-before-Neon is witnessed by nonnull matching fingerprints
on every succeeded terminal row and produced-at metadata no later than its
terminal timestamp. Execute
`W8-LIVE-07` and `W8-LIVE-08`.

### 6.8 Owner visibility, denial and run handoff

Execute only the third literal `KIW8-API-V1` command in §3.7. It performs the
exact HTML GET, completed research GET, mandatory same-selection PUT, one
same-key run POST and both owner-B denial GETs in that order. Apply the frozen
selection and handoff ambiguity branches; no alternate request or click is
allowed. Require its exact safe output and `privateProjectionCount:0`; execute
`W8-NC-05`.

Immediately execute `KIW8-DB-V1 handoff`. Require one handoff, selection revision
equal to the PUT result, `1..100` queries, exact selection fingerprint, every
query's `keywordResearchItemId` equal to one saved calculated item (manual items
use null), Run `awaiting_query_confirmation/query_review`, confirmation fields
null, results false and all six downstream durable counts zero. Repeat the six
established non-keyword source/check/DLQ §3.6 queue projections captured before
the handoff and require byte-equal count projections. Query exact downstream
Lambda metrics over the handoff interval and require invocation deltas zero.
The runner never requests `POST /api/runs/${runId}/start`, query confirmation,
Google, lead, Browserless, traffic DataForSEO or CrUX. Execute `W8-LIVE-09`.

### 6.9 Operational/privacy closure and conformance

Execute the exact expected-active inspector, §3.6 source/DLQ, 31-alarm, Lambda
metric, log and S3 projections, and final `KIW8-DB-V1 progress/artifactRows/
handoff` sequence. Require keyword DLQ zero, source counts consistent with
terminal completion, every alarm accepted by §3.6, inspector equality, all
artifact validations, and all durable handoff predicates. Concatenate only the
safe JSON projections in memory and test the forbidden regex in §3.6 plus
`https?://|@[A-Za-z0-9.-]+|\b\d{12}\b`; `forbiddenMatchCount` must be zero.

Execute `W8-NC-06`, then recompute the required/registered/executed/activated
case and control sets. Require 10/10/10/10 cases, 6/6 controls falsified, zero
skip/duplicate/unexpected/unactivated/oracle failures and both pinned digests.
Require the external action ledger to equal exactly `[ACT01,ACT02,ACT03,ACT04,
ACT05,ACT06]` on success; ACT07 must be absent. Execute `W8-CONF-01` and
`KI-W8-V1`–`V7`.

Append the complete sanitized handoff to A6, CAS A5 one version to
`AWAITING_REVIEW`, retain `accepted_through: KI-W7`, set
`next_window: STOP_FINAL_INDEPENDENT_REVIEW`, `may_start_successor:false`, and
stop. The window agent does not mark KI-W8 accepted.

### 6.10 Failure-only ACT-07 rollback

ACT-07 is unavailable on success. After an activated-path failure, disclose the
failure, current mapping/host/queue/DLQ state and exact disable plan. Without a
separate ACT-07 approval, stop without mutation.

With ACT-07 approval:

1. require A5 `KIW8_HOST_ROLLBACK_PROTOCOL_V1`, which is byte-identical to the
   accepted §3.4 update/readback record except: its starting revision is the
   ACT-03 healthy revision, its update body retains the same policy ARN and
   queue URL and sets only `AWS_PIPELINE_KEYWORD_RESEARCH_ENABLED` to literal
   `"false"`, and its canonical SHA is separately pinned by ACT-07. Execute its
   one update and 10-second/600-second readback; every unrelated configuration
   hash must remain equal;
2. derive `KIW8_ROLLBACK_NAME` as
   `ki-rollback-${acceptedPacketApprovalToken.slice(0,12)}` and create exactly
   this CloudFormation UPDATE change set (the command suffix always remains
   `--profile storesignal-dev --region ap-south-2 --no-cli-pager`):

```text
aws cloudformation create-change-set --stack-name storesignal-production-pipeline --change-set-name ${KIW8_ROLLBACK_NAME} --change-set-type UPDATE --use-previous-template --parameters ParameterKey=Environment,UsePreviousValue=true ParameterKey=ArtifactBucketName,UsePreviousValue=true ParameterKey=DiscoveryWorkerCodeKey,UsePreviousValue=true ParameterKey=DiscoveryWorkerCodeVersion,UsePreviousValue=true ParameterKey=DomainAggregatorCodeKey,UsePreviousValue=true ParameterKey=DomainAggregatorCodeVersion,UsePreviousValue=true ParameterKey=LeadWorkerCodeKey,UsePreviousValue=true ParameterKey=LeadWorkerCodeVersion,UsePreviousValue=true ParameterKey=LeadAggregatorCodeKey,UsePreviousValue=true ParameterKey=LeadAggregatorCodeVersion,UsePreviousValue=true ParameterKey=TrafficWorkerCodeKey,UsePreviousValue=true ParameterKey=TrafficWorkerCodeVersion,UsePreviousValue=true ParameterKey=FinalAggregatorCodeKey,UsePreviousValue=true ParameterKey=FinalAggregatorCodeVersion,UsePreviousValue=true ParameterKey=RecoveryCodeKey,UsePreviousValue=true ParameterKey=RecoveryCodeVersion,UsePreviousValue=true ParameterKey=KeywordWorkerCodeKey,UsePreviousValue=true ParameterKey=KeywordWorkerCodeVersion,UsePreviousValue=true ParameterKey=KeywordResearchEnabled,ParameterValue=false --capabilities CAPABILITY_IAM --description "Approved keyword-intelligence failure rollback" --profile storesignal-dev --region ap-south-2 --no-cli-pager --output json
aws cloudformation wait change-set-create-complete --stack-name storesignal-production-pipeline --change-set-name ${KIW8_ROLLBACK_NAME} --profile storesignal-dev --region ap-south-2 --no-cli-pager
aws cloudformation describe-change-set --stack-name storesignal-production-pipeline --change-set-name ${KIW8_ROLLBACK_NAME} --profile storesignal-dev --region ap-south-2 --no-cli-pager --output json
```

   Capture the exact returned `ChangeSetId` and normalized projection in memory;
3. normalize and require the activation allowlist in §6.7 (same three direct
   Modify/False members plus only the two optional exact dependencies), no
   Remove/replacement/unlisted/detail drift;
4. CAS A5 one version retaining the current ACT-07 approval and adding only the
   exact `rollback_change_set_id` and normalized-projection SHA-256, then run:

```text
aws cloudformation describe-change-set --stack-name storesignal-production-pipeline --change-set-name ${KIW8_ROLLBACK_ID} --profile storesignal-dev --region ap-south-2 --no-cli-pager --output json
aws cloudformation execute-change-set --stack-name storesignal-production-pipeline --change-set-name ${KIW8_ROLLBACK_ID} --profile storesignal-dev --region ap-south-2 --no-cli-pager --output json
aws cloudformation wait stack-update-complete --stack-name storesignal-production-pipeline --profile storesignal-dev --region ap-south-2 --no-cli-pager
```

   The first describe must reproduce the A5-pinned ID/projection before execute;
5. run the expected-disabled inspector; require mapping disabled and both
   keyword flags false; and
6. retain all rows, messages, artifacts and logs. Never purge, redrive, delete,
   direct-invoke, or create another research.

The rollback change-set ID/projection must be pinned in current A5 before its
execute call. If the host or stack disable step fails, stop and report the exact
applied state; do not manually repair. ACT-07 is the sole additional action in
the ledger and does not make the failed canary pass.

## 7. Frozen gates, run counts and invalidation

### 7.1 Literal per-gate operation manifest

| Gate | Exact command/runner and cwd | Environment allowlist | Exit/output and activation witness | Maximum runs | External side effect / cost | Ambiguity and reconciliation | Evidence artifact |
|---|---|---|---|---:|---|---|---|
| `G1` | root: `sha256sum` the two standards/A1-A5/A8/S1; `git status --short`, `git rev-parse HEAD`, packet `sha256sum`/`wc -c`; backend: the two measurement commands in §6.2 P6 | none | exit 0; all pinned hashes/bytes/counts/cold imports exact; W7 commits clean | 1 | gitignored measurement refresh only; `$0` | local read/build transport only: E8.1 one identical recovery after zero surviving process/write proof | `EV-KI-W8-I001-G1.json` in S3 entry |
| `G2` | backend: exact P2/P3/P4/P5/P6 commands and `KIW8-DB-V1 baseline`; §3.6 queue observer; §3.2 discovery | `AWS_PROFILE,AWS_REGION,KIW8_HOST_READ_TOKEN`; P4 credentials remain in memory | exit 0; exact safe schemas; every DG passing; `W8-LIVE-01` activated | 1 | read-only AWS/host/provider/Neon; `$0` | GET/read transport may recover once under E8.1 only after zero mutation/cost/result; missing host/P5 record is a blocker, not recovery | `EV-KI-W8-I001-G2.json` |
| `G3` | backend: exact §6.3 create-change-set command | `KIW8_ACCOUNT_ID` equal current A5 | exit 0 `CHANGE_SET_REVIEWED`; three object versions and reviewed projection exact; NC01/02 activated | 1 | three versioned AES256 S3 writes plus one unexecuted change set; `$0` | stable object keys and change-set name/ID reconcile any lost response; never recreate if identity exists | `EV-KI-W8-I001-G3.json` |
| `G4` | backend: exact two §6.4 commands | `KIW8_ACCOUNT_ID` | exit 0 `REVIEWED_CHANGE_SET_APPLIED` then `EXPECTED_DISABLED_KEYWORD_STACK_VERIFIED`; LIVE03 | 1 | execute one reviewed disabled stack update; `$0` | describe exact A5 change-set ID and stack events; if final state cannot be proven, stop without second execute | `EV-KI-W8-I001-G4.json` |
| `G5` | §3.4 exact host update/readback, then frontend first `KIW8-API-V1` command, `KIW8-DB-V1 resolveResearch/progress`, §3.6 observers | G2 allowlist plus `KIW8_HOST_WRITE_TOKEN,KIW8_ORIGIN,KIW8_OWNER_A_COOKIE,KIW8_APPROVED_SEED,KIW8_WINDOW_STARTED_AT` | host exact; POST 202 or exact DB reconciliation; one queued row/message; zero work/cost; LIVE04/05 and NC03/04 | host 1; create POST 1 | one host config update and one research/message; provider `$0` | host readback by configuration revision; create uses §3.7 no-retry DB reconciliation | `EV-KI-W8-I001-G5.json` |
| `G6` | backend: exact three §6.7 activation commands; frontend second `KIW8-API-V1`; backend `KIW8-DB-V1 progress/artifactRows` plus §3.6 queue/Lambda/alarm/log/S3 observers | `KIW8_ACCOUNT_ID,KIW8_ORIGIN,KIW8_OWNER_A_COOKIE,KIW8_RESEARCH_ID` plus AWS fixed values | active inspector; same ID progresses/completes; artifacts validated; LIVE06/07/08 | activation 1; canary 1; bounded polls only | one activation stack update; same research may make provider calls; total `<=3.00000000` | activation reconciled by exact change-set/stack/mapping state; paid ambiguity uses durable attempt rows only; never repeat activation/research | `EV-KI-W8-I001-G6.json` |
| `G7` | frontend third `KIW8-API-V1`; backend `KIW8-DB-V1 handoff/progress/artifactRows`, §3.6 queue/Lambda/alarm/log/S3 observers, literal registry/digest command | `KIW8_ORIGIN,KIW8_OWNER_A_COOKIE,KIW8_OWNER_B_COOKIE,KIW8_RESEARCH_ID,KIW8_WINDOW_STARTED_AT` plus AWS fixed values | dashboard 200, mandatory save, one handoff, owner B two 404s, zero downstream, privacy zero, 10/6 sets and digests; LIVE09/CONF01/NC05/06 | save 1; handoff 1; final reads 1 | one selection revision and one unconfirmed Run; `$0` additional | selection read-after-timeout; handoff same-key one retry; DB handoff row is final authority; never confirm/start | `EV-KI-W8-I001-G7.json` |

All `EV-KI-W8-I001-G*.json` names identify exact JSON blocks appended to S3;
they are not workspace files. Every row's action requires its separate current
A5 approval predicate. G6 additionally requires ACT-05 and ACT-06 together.

### 7.2 Mechanical execution-choice lint and falsification

Before parent review and again at P6, run from root:

```text
node -e 'const fs=require("node:fs"),s=fs.readFileSync("KEYWORD_INTELLIGENCE_KI_W8_SUBWINDOW_CHECKLIST.md","utf8"),a=s.slice(s.indexOf("## 6. `KI-W8-I001`"),s.indexOf("## 7. Frozen gates")),db=s.slice(s.indexOf("### 3.5 Exact production Neon observer"),s.indexOf("### 3.6 Exact AWS dynamic observers")),ops=s.slice(s.indexOf("### 7.1 Literal per-gate operation manifest"),s.indexOf("### 7.2 Mechanical execution-choice lint")),bad=["dashboard form or same-origin route","if required","normal authenticated GETs","read-only durable inspection","Search exact inspected projections","execute only the P2-recorded host operation","may use only a current official provider","inspect only","read Neon","as appropriate","as needed","choose","decide","determine"," etc."];const hit=bad.filter(x=>a.includes(x));if(hit.length)throw Error(`KIW8_EXECUTION_CHOICE:${hit.join("|")}`);for(const x of["### 3.2 Exact admissible host discovery","### 3.3 Exact P5 prerequisite record","### 3.4 Exact ACT-03 prerequisite record","### 3.5 Exact production Neon observer","### 3.6 Exact AWS dynamic observers","### 3.7 Exact production frontend/API runner","### 7.1 Literal per-gate operation manifest"]){if(!s.includes(x))throw Error(`KIW8_MECHANISM_MISSING:${x}`)}if((db.match(/SELECT count\(\*\)::int AS \"nonterminalResearchCount\"/g)||[]).length!==2)throw Error("KIW8_DB_BASELINE_QUERY_COUNT");if(!ops.includes("| Gate | Exact command/runner and cwd | Environment allowlist |"))throw Error("KIW8_GATE_ENV_ALLOWLIST");for(let n=1;n<=7;n++)if(!ops.includes(`| \`G${n}\` |`)||!ops.includes(`\`EV-KI-W8-I001-G${n}.json\``))throw Error(`KIW8_GATE_ROW:${n}`);console.log("KIW8_EXECUTION_CHOICES_ZERO")'
```

Self-falsification runs on an in-memory copy only. Replace the exact ACT-04
command with the former `dashboard form or same-origin route`, delete one SQL
query, delete one operation-table environment allowlist, and change P5's
fail-closed state to `select endpoint`; each separate mutation must make the
lint exit nonzero. It emits only the failing rule name. Required outcome is four
falsifications plus the unmodified `KIW8_EXECUTION_CHOICES_ZERO` pass.

No stateful, AWS, host, provider, paid, database or browser gate may be repeated
to accumulate evidence. The one E8.1 identical recovery applies only to a
proven sandbox/channel invalidation with no surviving process, mutation, paid
operation or usable result. It cannot repeat an AWS mutation, API creation,
activation, paid canary or handoff after any material side effect. Such an
unobservable or ambiguous external action is reconciled read-only by its stable
identity; if not provable, stop. Observable assertion failure is never E8.1.

Any source/template/ZIP/test/fixture change invalidates G1 onward. Host changes
invalidate G5 onward. Full change-set drift invalidates G3 onward. Activation
change-set drift invalidates G6 onward. A corrected implementation requires
parent correction authority and a new decomposition; the window agent cannot
open a source corrective leaf.

## 8. Assessment checklist and handoff

- [ ] `I1` Verify parent decomposition approval, new execution assignment, A5 pins and no implementation leaf. Evidence: ___
- [ ] `I2` Execute P1-P6 in order; record every deferred-gate value/branch sanitized. Evidence: ___
- [ ] `I3` Obtain/verify ACT-01 approval, execute G3 only, then stop for ACT-02. Evidence: ___
- [ ] `I4` Obtain/verify ACT-02 approval, execute G4 only, then stop for ACT-03. Evidence: ___
- [ ] `I5` Obtain/verify ACT-03 approval, execute host update/readback, then stop for ACT-04. Evidence: ___
- [ ] `I6` Obtain/verify ACT-04 approval, create exactly one disabled research and execute NC03/04, then stop for ACT-05. Evidence: ___
- [ ] `I7` Obtain ACT-05 and ACT-06 independently; execute activation only when both are current; observe the same research. Evidence: ___
- [ ] `I8` Execute owner/UI/handoff, privacy, operation, cost and no-downstream oracles; execute no second canary. Evidence: ___
- [ ] `I9` Verify required=registered=executed=activated case sets and all six controls/digests with zero exceptions. Evidence: ___
- [ ] `I10` Verify current source diff is empty, only authorized coordination/generated paths changed, and no prohibited/successor action occurred. Evidence: ___
- [ ] `I11` On success append the window certificate, CAS A5 to AWAITING_REVIEW and stop; on failure use ACT-07 only after its separate approval and still stop failed. Evidence: ___

Successful handoff must include the Section 12.4 certificate adapted to the
zero-source live assessment plus: exact sanitized approval ledger, AWS action
ledger, mutation IDs, packet/object/change-set hashes, actual provider attempts
and cost, duration/memory/artifact/message counts, owner/run lineage hashes,
rollback status, queue/DLQ/alarm state, forbidden-output count, residual risks
and prerequisites. Status is `READY_FOR_PARENT_REVIEW`, never parent acceptance.

## 9. Correction and escalation rule

`KI-W8-I001` may diagnose but may not edit implementation. A failure is:

- `CORRECTION_REQUIRED` only after the parent authorizes a new parent-level
  correction and returns a revised/delegable scope; or
- `PARENT_BLOCKED` for authority contradiction, missing applied capability,
  secret/provider/host prerequisite, unapproved action, external ambiguity,
  source defect, privacy issue, cost breach, DLQ/alarm, or required scope growth.

The window agent records exact expected/observed behavior, activation, causal
path, root file/system, governing IDs and invalidated gates, then stops. It does
not invent a local fix, weaken an oracle, raise a timeout, repeat the canary, or
forward a lower-agent summary.

## 10. Mandatory decomposition-readiness checklist

### 10.1 Authority and inheritance

- [x] `SW-A01` Parent assignment and window-agent identity are exact; delegation is explicitly prohibited. Evidence: `EV-KI-W8-S001`.
- [x] `SW-A02` Both standards and A1/A2/A3/A4/A5/A8 revisions are pinned and recomputed. Evidence: `EV-KI-W8-S001`.
- [x] `SW-A03` Parent write/read/action/prohibition/successor/stop boundaries are copied without expansion. Evidence: `EV-KI-W8-S001`.
- [x] `SW-A04` Root/backend/frontend baselines and parent-owned dirty paths are inventoried. Evidence: `EV-KI-W8-S001`.
- [x] `SW-A05` S1/S2/S3 exist with nonoverlapping authority. Evidence: `EV-KI-W8-S003`.
- [x] `SW-A06` Strict adjacency is vacuous below W8 and no subagent/leaf delegation can occur. Evidence: `EV-KI-W8-S002`.
- [x] `SW-A07` E8.1 is inherited for authorized local/read-only transport only and cannot expand external authority. Evidence: `EV-KI-W8-S002`.

### 10.2 Decision and file-set closure

- [x] `SW-D01` Every W8 requirement/decision/task/scenario/case/control maps to I001 phases and assertions. Evidence: `EV-KI-W8-S002`.
- [x] `SW-D02` No non-deferred parent decision is missing; exact deferred facts and fail-closed branches are enumerated. Evidence: `EV-KI-W8-S002`.
- [x] `SW-D03` Required and planned implementation changed-file sets are both empty. Evidence: `EV-KI-W8-S002`.
- [x] `SW-D04` Initial file-owner count is zero by the parent-authorized no-leaf policy. Evidence: `EV-KI-W8-S002`.
- [x] `SW-D05` File transformation fields are N/A because source writes are prohibited; current input/generated-path identities are exact. Evidence: `EV-KI-W8-S002`.
- [x] `SW-D06` DAG is the single sequential I001 assessment with no parallel wave. Evidence: `EV-KI-W8-S002`.
- [x] `SW-D07` All consumed interfaces are frozen by DEC-KI-059/current source or explicit deferred applied facts. Evidence: `EV-KI-W8-S002`.
- [x] `SW-D08` Every approval/intermediate state has exact permitted actions, stop branch and resolver. Evidence: `EV-KI-W8-S002`.
- [x] `SW-D09` No production/test/fixture/schema/config/manifest/generated tracked file is assigned. Evidence: `EV-KI-W8-S002`.
- [x] `SW-D10` No generator/formatter/installer/rename/move can change a workspace source file. Evidence: `EV-KI-W8-S002`.

### 10.3 Sub-window execution completeness

- [x] `SW-E01` No FILE/CORRECTION block is applicable; I001 contains every Section 9.2 field. Evidence: `EV-KI-W8-S002`.
- [x] `SW-E02` I001 has one exact ordered state/action algorithm and no implementation alternatives. Evidence: `EV-KI-W8-S002`.
- [x] `SW-E03` Every phase has exact entry, activation, result and forbidden outcomes. Evidence: `EV-KI-W8-S002`.
- [x] `SW-E04` Source changed-file equality is exact empty-set equality. Evidence: `EV-KI-W8-S002`.
- [x] `SW-E05` I001 evidence, handoff, stop and parent-successor reservation are exact. Evidence: `EV-KI-W8-S002`.
- [x] `SW-E06` No subordinate implementation agent exists or can update authority artifacts. Evidence: `EV-KI-W8-S002`.
- [x] `SW-E07` I001 requires no successor implementation to satisfy W8. Evidence: `EV-KI-W8-S002`.
- [x] `SW-E08` Deferred facts are owned only by P1-P6; final review remains parent-owned. Evidence: `EV-KI-W8-S002`.

### 10.4 Enforcement and integration closure

- [x] `SW-V01` Ten cases/six controls map to exact I001 registrations/activation/oracles. Evidence: `EV-KI-W8-S002`.
- [x] `SW-V02` Exact set equality, counts and both digests are prescribed. Evidence: `EV-KI-W8-S002`.
- [x] `SW-V03` Every critical W8 invariant maps to NC01-NC06 at the narrowest safe boundary. Evidence: `EV-KI-W8-S002`.
- [x] `SW-V04` Every local substitute has an explicit fidelity limit and accepted W7 evidence invalidation rule. Evidence: `EV-KI-W8-S002`.
- [x] `SW-V05` I001 is fully authored with zero implementation-write authority. Evidence: `EV-KI-W8-S002`.
- [x] `SW-V06` P1-P6/G1-G7 are exact, sequential and once-only. Evidence: `EV-KI-W8-S002`.
- [x] `SW-V07` Diagnosis, parent correction and reassessment rules prohibit self-repair. Evidence: `EV-KI-W8-S002`.
- [x] `SW-V08` The window agent personally executes/reviews every I001 phase. Evidence: `EV-KI-W8-S002`.
- [x] `SW-V09` Live acceptance cannot pass via local substitute, zero work, skip, duplicate, unexpected or missing activation. Evidence: `EV-KI-W8-S002`.
- [x] `SW-V10` Consolidated handoff and READY_FOR_PARENT_REVIEW boundary are exact. Evidence: `EV-KI-W8-S002`.
- [x] `SW-V11` E8.1 permits only one identical no-side-effect transport recovery and rejects real/external ambiguity. Evidence: `EV-KI-W8-S002`.

### 10.5 Mechanical and adversarial audit

- [x] `SW-R01` IDs are unique and references resolve. Evidence: `EV-KI-W8-S003`.
- [x] `SW-R02` No unresolved assignable placeholder exists; deferred values use named gates. Evidence: `EV-KI-W8-S003`.
- [x] `SW-R03` Any FILE/CORRECTION assignment or implementation write fails the zero-leaf/empty-set oracle. Evidence: `EV-KI-W8-S003`.
- [x] `SW-R04` Removing I001 or any mapped parent task/case fails traceability. Evidence: `EV-KI-W8-S003`.
- [x] `SW-R05` Removing/duplicating/skipping/filtering/bypassing a case/control fails exact set/activation closure. Evidence: `EV-KI-W8-S003`.
- [x] `SW-R06` Weakening an oracle or overstating a substitute invalidates evidence. Evidence: `EV-KI-W8-S003`.
- [x] `SW-R07` Simulated leaf dispatch, source edit or direct lower-agent communication is rejected. Evidence: `EV-KI-W8-S003`.
- [x] `SW-R08` Simulated live failure cannot be repaired by the window agent. Evidence: `EV-KI-W8-S003`.
- [x] `SW-R09` Parent decomposition approval is required before I001 receives execution authority. Evidence: `EV-KI-W8-S003`.
- [x] `SW-R10` Document lint reports zero missing mappings/cases/evidence/authority conflicts. Evidence: `EV-KI-W8-S003`.
- [x] `SW-R11` Sandbox denial permits one identical local/read-only recovery; changed commands, live side effects and external actions do not. Evidence: `EV-KI-W8-S003`.

## 11. Trace closure

| Parent set | I001 ownership |
|---|---|
| `REQ-KI-002/005/022`–`024`, `INV-KI-001`–`009/012`–`014`, `AUTH-KI-005/007`, `EXC-KI-008` | P1-P6, ACT01-ACT06, LIVE01-LIVE08, NC01-NC04 |
| `REQ-KI-015`–`017/022`–`024`, `INV-KI-005`–`011/013`–`015` | LIVE06-LIVE09, CONF01, NC05/NC06 |
| `DEC-KI-009/017/025/059` | approval state machine, cost/attempt bounds, atomic handoff, failure-only rollback |
| `KI-W8-T1` | ACT01/02; LIVE01-LIVE03; NC01/02 |
| `KI-W8-T2` | ACT03/04/05; LIVE04-LIVE06; NC03/04 |
| `KI-W8-T3` | ACT06 and conditional ACT07; LIVE07-LIVE09/CONF01; NC05/06 |
| `SCN-KI-048` | complete I001 assessment |
| `KI-W8-V1`–`V7`, `H1/H2` | §§6.2-6.10 and §8 |

Unmapped parent requirements: `0`. Unmapped decisions: `0`. Unmapped tasks:
`0`. Unmapped scenarios: `0`. Unmapped cases/controls: `0`.

## 12. Append-only amendments

No amendment or correction is authorized by state 200. Later parent-approved
changes append here with new IDs; existing content and evidence are not
silently rewritten.
