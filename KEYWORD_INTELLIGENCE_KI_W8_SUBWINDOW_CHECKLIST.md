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
| Coordination root | requester commit `e4f315488cd80c567e035cc99ed0083b1c717a14`; clean before this superseding decomposition revision |
| Backend | clean commit `c3ba835be446ba43e1a80be4f5ab4d28bae89497` |
| Frontend | clean commit `5e441aae7e2f3a132b2c7fc85bf1bc525d3d5cb6` |

The requester committed the state-200 assignment and DECOMP-2 package as
`e4f315488cd80c567e035cc99ed0083b1c717a14` before this parent correction.
The starting root changed-path set for DECOMP-3 is empty; its
sorted-member-plus-LF digest is
`e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855`.
Only S1/S2/S3 may differ during this reconciliation.

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
 -> BROWSER_SELECTION_SAVE_RUNNING
 -> AWAITING_PARENT_SAVED_SELECTION_PIN
 -> HANDOFF_INITIAL_RUNNING
 -> OWNER_B_DENIAL_RUNNING
 -> READY_FOR_PARENT_REVIEW
```

The only resumable ambiguity branches are:

```text
BROWSER_SELECTION_SAVE_RUNNING
 -> AWAITING_PARENT_SELECTION_RECONCILIATION_PIN
 -> SELECTION_RECONCILIATION_RUNNING
 -> AWAITING_PARENT_SAVED_SELECTION_PIN        # saved only; rolled_back stops

HANDOFF_INITIAL_RUNNING
 -> AWAITING_PARENT_HANDOFF_RECONCILIATION_PIN
 -> HANDOFF_RECONCILIATION_RUNNING
 -> OWNER_B_DENIAL_RUNNING                     # exact same key/body; 200 only
 -> READY_FOR_PARENT_REVIEW

OWNER_B_DENIAL_RUNNING
 -> OWNER_B_DENIAL_READONLY_TRANSPORT_RECOVERY # only after zero usable response
 -> READY_FOR_PARENT_REVIEW
```

The parent pin transitions record only the safe fields enumerated in §3.7.
They do not authorize another save, research, or unequal handoff request.

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
KIW8_SELECTION_PRIOR_REVISION=<A5-pinned browser preflight integer, ambiguity only>
KIW8_SELECTION_COUNT=<A5-pinned browser preflight integer, ambiguity only>
KIW8_SELECTION_EXPECTED_SHA256=<A5-pinned browser preflight 64-lower-hex, ambiguity only>
KIW8_SELECTION_SAVED_REVISION=<A5-pinned successful saved revision>
KIW8_SELECTION_SAVED_SHA256=<A5-pinned successful saved-selection 64-lower-hex>
KIW8_HANDOFF_MODE=<literal initial or parent-authorized ambiguity-only reconcile>
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
extra key or extra line is a privacy failure. The browser-save command has the
two exact lines frozen in §3.7.1; every other command has one. The five
selection variables are unavailable before their preceding safe record has
been parent-pinned in A5; absence or drift stops before the next request.

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
encrypted:true,fingerprintMismatches:0,metadataMismatches:0}`. The existing
`GetObject` response for each key must show AES256 and a nonempty VersionId; no
separate `HeadObject` operation occurs. No raw object body/key is emitted.

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
// KIW8-MANIFEST-METADATA-V1-BEGIN
function manifestProducedAt(row) {
  if (typeof row.manifestProducedAt !== "string" || !row.manifestProducedAt)
    throw new Error("KIW8_MANIFEST_PRODUCED_AT");
  const value = new Date(row.manifestProducedAt);
  if (!Number.isFinite(value.getTime())) throw new Error("KIW8_MANIFEST_PRODUCED_AT");
  return value.toISOString();
}
// KIW8-MANIFEST-METADATA-V1-END
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
    contentFingerprint: row.manifestFingerprint, producedAt: manifestProducedAt(row) });
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

The manifest-metadata local-now oracle is the following exact documentation-
only command from root. It extracts and executes the function used by the
literal observer, gives `manifestProducedAt` and `stageCreatedAt` deliberately
different instants, and proves the persisted manifest instant wins. Its
in-memory negative control replaces only `row.manifestProducedAt` with
`row.stageCreatedAt`; that mutated function must fail the same semantic oracle.

```text
node -e 'const fs=require("node:fs"),s=fs.readFileSync("KEYWORD_INTELLIGENCE_KI_W8_SUBWINDOW_CHECKLIST.md","utf8"),start="// KIW8-MANIFEST-METADATA-V1-BEGIN",end="// KIW8-MANIFEST-METADATA-V1-END",body=s.slice(s.indexOf(start)+start.length,s.indexOf(end));if(!body||body.includes(start)||body.includes(end))throw Error("KIW8_MANIFEST_ORACLE_EXTRACT");const load=x=>Function(`${x};return manifestProducedAt`)(),row={manifestProducedAt:"2026-08-24T01:02:03.456Z",stageCreatedAt:"2026-08-20T04:05:06.789Z"},fn=load(body);if(fn(row)!=="2026-08-24T01:02:03.456Z")throw Error("KIW8_MANIFEST_PRODUCED_AT_MAPPING");const mutated=load(body.replaceAll("row.manifestProducedAt","row.stageCreatedAt"));let falsified=false;try{if(mutated(row)!=="2026-08-24T01:02:03.456Z")throw Error("KIW8_MANIFEST_PRODUCED_AT_MAPPING")}catch(e){falsified=e.message==="KIW8_MANIFEST_PRODUCED_AT_MAPPING"}if(!falsified)throw Error("KIW8_MANIFEST_NEGATIVE_CONTROL");console.log("KIW8_MANIFEST_METADATA_SEMANTIC_PASS")'
```

### 3.7 Exact production frontend/browser/API runners

All runners in this section execute from `frontend/` with Node 20+ and shell
tracing disabled. The create and poll commands remain exactly:
Together these two read/create commands are `KIW8-API-V1`; the browser save,
selection reconciliation and handoff runners below are separate resumable
operations and are never collapsed back into `KIW8-API-V1`.

```text
node --experimental-strip-types --input-type=module -e 'import{createHash}from"node:crypto";import{parseResearchEnvelope}from"./lib/keyword-intelligence-validation.ts";const origin=process.env.KIW8_ORIGIN,cookie=process.env.KIW8_OWNER_A_COOKIE,seed=process.env.KIW8_APPROVED_SEED,r=await fetch(`${origin}/api/keyword-research`,{method:"POST",headers:{Accept:"application/json","Content-Type":"application/json",Cookie:cookie},body:JSON.stringify({seeds:[seed]}),redirect:"error",signal:AbortSignal.timeout(20000)}),body=await r.json();if(r.status!==202)throw Error("KIW8_CREATE_STATUS");const v=parseResearchEnvelope(body);if(!/^kr_[A-Za-z0-9_-]{24}$/u.test(v.id)||v.state!=="queued"||v.generation!==1||v.contractVersion!==1||v.selectionRevision!==0||v.result!==null||v.safeError!==null||v.seeds.length!==1||v.seeds[0]!==seed)throw Error("KIW8_CREATE_CONTRACT");console.log(JSON.stringify({mode:"create",status:r.status,researchIdSha256:createHash("sha256").update(v.id).digest("hex"),state:v.state,generation:v.generation,selectionRevision:v.selectionRevision}))'

node --experimental-strip-types --input-type=module -e 'import{createHash}from"node:crypto";import{parseResearchEnvelope}from"./lib/keyword-intelligence-validation.ts";const origin=process.env.KIW8_ORIGIN,cookie=process.env.KIW8_OWNER_A_COOKIE,id=process.env.KIW8_RESEARCH_ID,r=await fetch(`${origin}/api/keyword-research/${encodeURIComponent(id)}`,{headers:{Accept:"application/json",Cookie:cookie},redirect:"error",signal:AbortSignal.timeout(20000)}),body=await r.json();if(r.status!==200)throw Error("KIW8_POLL_STATUS");const v=parseResearchEnvelope(body);if(v.id!==id)throw Error("KIW8_POLL_ID");console.log(JSON.stringify({mode:"poll",researchIdSha256:createHash("sha256").update(id).digest("hex"),state:v.state,progress:v.progress,selectionCount:v.selection.length,selectionRevision:v.selectionRevision,resultKeywordCount:v.result?.keywords.length??0,safeErrorCode:v.safeError?.code??null}))'
```

Create sends one POST only. A lost create response is never retried:
`KIW8-DB-V1 resolveResearch` runs once, with exactly one row proving creation,
zero rows proving rollback, and multiple rows stopping
`PARENT_BLOCKED_SECOND_CANARY`. Poll runs every 15 seconds, with one read-only
transport recovery, a 15-minute no-durable-progress watchdog and four-hour
absolute ceiling.

#### 3.7.1 Real rendered dashboard selection save (`KIW8-BROWSER-SAVE-V1`)

The selection state transition uses `/usr/bin/google-chrome` headless through
Chrome DevTools Protocol. It does not use an HTML fetch as a UI substitute.
Execute this literal heredoc once:

```bash
node --experimental-strip-types --input-type=module - <<'KIW8_BROWSER_SAVE_V1'
import { spawn } from "node:child_process";
import { createHash } from "node:crypto";
import { mkdtemp, readFile, rm } from "node:fs/promises";
import { tmpdir } from "node:os";
import { join } from "node:path";
import { parseResearchEnvelope } from "./lib/keyword-intelligence-validation.ts";
const h=(x)=>createHash("sha256").update(String(x)).digest("hex"), wait=(ms)=>new Promise(r=>setTimeout(r,ms));
const origin=process.env.KIW8_ORIGIN,cookieHeader=process.env.KIW8_OWNER_A_COOKIE,id=process.env.KIW8_RESEARCH_ID;
if(!/^https:\/\/[^/?#]+$/u.test(origin||"")||!/^kr_[A-Za-z0-9_-]{24}$/u.test(id||"")||!cookieHeader)throw Error("KIW8_BROWSER_INPUT");
if(typeof WebSocket!=="function")throw Error("KIW8_BROWSER_WEBSOCKET");
const profile=await mkdtemp(join(tmpdir(),"kiw8-live-browser-"));let chrome,cdp;
class Cdp{constructor(url){this.ws=new WebSocket(url);this.n=1;this.pending=new Map();this.listeners=[]}async open(){await new Promise((r,j)=>{this.ws.addEventListener("open",r,{once:true});this.ws.addEventListener("error",j,{once:true})});this.ws.addEventListener("message",({data})=>{const m=JSON.parse(String(data));if(m.id!==undefined){const p=this.pending.get(m.id);if(!p)return;this.pending.delete(m.id);m.error?p.j(Error("KIW8_CDP_PROTOCOL")):p.r(m.result);return}for(const x of this.listeners)if(x.method===m.method)x.fn(m.params)})}send(method,params={}){const id=this.n++;this.ws.send(JSON.stringify({id,method,params}));return new Promise((r,j)=>this.pending.set(id,{r,j}))}on(method,fn){this.listeners.push({method,fn})}close(){this.ws.close()}}
const evaluate=async(expression)=>{const x=await cdp.send("Runtime.evaluate",{expression,awaitPromise:true,returnByValue:true});if(x.exceptionDetails)throw Error("KIW8_BROWSER_EVALUATE");return x.result.value};
const until=async(fn,ms,code)=>{const start=Date.now();while(Date.now()-start<ms){const v=await fn();if(v)return v;await wait(100)}throw Error(code)};
const requests=[],responses=new Map(),finished=new Set();
try{
  chrome=spawn("/usr/bin/google-chrome",["--headless=new","--no-sandbox","--disable-gpu","--disable-dev-shm-usage",`--user-data-dir=${profile}`,"--remote-debugging-port=0","about:blank"],{detached:true,stdio:"ignore"});
  const port=await until(async()=>{try{return (await readFile(join(profile,"DevToolsActivePort"),"utf8")).trim().split(/\r?\n/u)[0]}catch{return null}},20000,"KIW8_BROWSER_PORT");
  const targets=await(await fetch(`http://127.0.0.1:${port}/json/list`,{signal:AbortSignal.timeout(20000)})).json(),target=targets.find(x=>x.type==="page");if(!target)throw Error("KIW8_BROWSER_TARGET");
  cdp=new Cdp(target.webSocketDebuggerUrl);await cdp.open();await cdp.send("Page.enable");await cdp.send("Runtime.enable");await cdp.send("Network.enable");
  cdp.on("Network.requestWillBeSent",p=>requests.push({requestId:p.requestId,method:p.request?.method,url:p.request?.url,postData:p.request?.postData??null}));
  cdp.on("Network.responseReceived",p=>responses.set(p.requestId,p.response?.status));cdp.on("Network.loadingFinished",p=>finished.add(p.requestId));
  const cookies=cookieHeader.split(";").map(x=>x.trim()).filter(Boolean).map(x=>{const i=x.indexOf("=");if(i<1)throw Error("KIW8_BROWSER_COOKIE");return{name:x.slice(0,i),value:x.slice(i+1)}});
  for(const entry of cookies){const set=await cdp.send("Network.setCookie",{...entry,url:origin,secure:true,httpOnly:true,sameSite:"Lax"});if(set.success!==true)throw Error("KIW8_BROWSER_COOKIE")}
  await cdp.send("Page.navigate",{url:`${origin}/keywords/${encodeURIComponent(id)}`});
  await until(()=>evaluate(`document.readyState==="complete"&&location.href===${JSON.stringify(`${origin}/keywords/${encodeURIComponent(id)}`)}`),60000,"KIW8_BROWSER_NAVIGATION");
  const completed=await until(()=>evaluate(`(()=>{const d=document.querySelector('[aria-label="Keyword research dashboard"]'),t=document.querySelector('[data-surface="surface:keyword-table"] tbody tr'),r=document.querySelector('[data-surface="surface:selection-review"]'),b=[...document.querySelectorAll('[data-surface="surface:selection-review"] button')].find(x=>x.textContent.trim()==="Save selection"),c=document.querySelector('[data-surface="surface:keyword-table"] input[type="checkbox"][aria-label^="Select "]');return d&&t&&r&&b&&!b.disabled&&c?{dashboard:true,table:true,review:true,save:true,checkbox:true}:null})()`),60000,"KIW8_BROWSER_COMPLETED_UI");
  const beforeRaw=await evaluate(`fetch(${JSON.stringify(`/api/keyword-research/${encodeURIComponent(id)}`)},{headers:{Accept:"application/json"},redirect:"error",signal:AbortSignal.timeout(20000)}).then(async r=>({status:r.status,body:await r.json()}))`),before=parseResearchEnvelope(beforeRaw.body);
  if(beforeRaw.status!==200||before.id!==id||before.state!=="completed"||before.selection.length<1||before.selection.length>100||before.selectionRevision<1||before.selectionConflicts.length)throw Error("KIW8_SELECTION_PREFLIGHT");
  const selectionSha256=h(JSON.stringify(before.selection));
  process.stdout.write(`${JSON.stringify({mode:"selection-preflight",researchIdSha256:h(id),selectionRevision:before.selectionRevision,selectionCount:before.selection.length,selectionSha256,rendered:completed})}\n`);
  const clicked=await evaluate(`(()=>{const b=[...document.querySelectorAll('[data-surface="surface:selection-review"] button')].find(x=>x.textContent.trim()==="Save selection");if(!b||b.disabled)return false;b.click();return true})()`);if(!clicked)throw Error("KIW8_SELECTION_CLICK");
  let req;try{req=await until(async()=>requests.find(x=>x.method==="PUT"&&new URL(x.url).pathname===`/api/keyword-research/${encodeURIComponent(id)}/selection`),20000,"KIW8_SELECTION_REQUEST_TIMEOUT")}catch{process.stdout.write(`${JSON.stringify({mode:"selection-save-ambiguous",researchIdSha256:h(id),priorRevision:before.selectionRevision,selectionCount:before.selection.length,selectionSha256,requestObserved:false})}\n`);process.exitCode=75}
  let status=null;if(req){const posted=JSON.parse(req.postData),projected=before.selection.map(v=>v.sourceKind==="calculated"?{sourceKind:"calculated",sourceKeywordId:v.sourceKeywordId,keyword:v.keyword}:{sourceKind:"manual",keyword:v.keyword});
  if(posted.expectedRevision!==before.selectionRevision||JSON.stringify(posted.items)!==JSON.stringify(projected))throw Error("KIW8_SELECTION_REQUEST_BODY");
  try{status=await until(async()=>responses.get(req.requestId)||null,20000,"KIW8_SELECTION_RESPONSE_TIMEOUT")}catch{process.stdout.write(`${JSON.stringify({mode:"selection-save-ambiguous",researchIdSha256:h(id),priorRevision:before.selectionRevision,selectionCount:before.selection.length,selectionSha256,requestObserved:true})}\n`);process.exitCode=75}}
  if(status!==null){if(status!==200)throw Error("KIW8_SELECTION_STATUS");await until(async()=>finished.has(req.requestId),20000,"KIW8_SELECTION_BODY_TIMEOUT");const body=JSON.parse((await cdp.send("Network.getResponseBody",{requestId:req.requestId})).body),saved=parseResearchEnvelope(body);if(saved.id!==id||saved.selectionRevision!==before.selectionRevision+1||JSON.stringify(saved.selection)!==JSON.stringify(before.selection)||saved.selectionConflicts.length)throw Error("KIW8_SELECTION_SAVE_CONTRACT");const ui=await until(()=>evaluate(`(()=>{const b=[...document.querySelectorAll('[data-surface="surface:selection-review"] button')].find(x=>x.textContent.trim()==="Save selection"),a=document.querySelector('[aria-label="Keyword research dashboard"] [role="alert"]');return b&&!b.disabled&&b.getAttribute("aria-busy")!=="true"&&!a?{saveSettled:true,noErrorAlert:true}:null})()`),20000,"KIW8_SELECTION_UI_SETTLE");if(requests.some(x=>x.method==="POST"&&(/\/runs$/u.test(new URL(x.url).pathname)||/\/start$/u.test(new URL(x.url).pathname))))throw Error("KIW8_FORBIDDEN_CONFIRM_START");process.stdout.write(`${JSON.stringify({mode:"browser-save",researchIdSha256:h(id),selectionSaved:true,priorRevision:before.selectionRevision,selectionRevision:saved.selectionRevision,selectionCount:saved.selection.length,selectionSha256:h(JSON.stringify(saved.selection)),saveRequestStatus:status,ui,forbiddenRunOrStartRequests:0})}\n`)}
}finally{try{cdp?.close()}catch{}if(chrome?.pid&&chrome.exitCode===null)try{process.kill(-chrome.pid,"SIGTERM")}catch{}await rm(profile,{recursive:true,force:true})}
KIW8_BROWSER_SAVE_V1
```

The runner proves the real owner-A page rendered the completed dashboard,
keyword table, at least one real checkbox, selection review and enabled `Save
selection` control before it clicks that exact button. It observes and parses
the resulting real PUT, proves the UI returned to an enabled non-error settled
state, and proves no `/runs` or `/start` POST occurred. It emits the preflight
line before the click and exactly one success or ambiguity line afterward.
Cookies, raw IDs, keywords, request/response bodies, URLs and Chrome output are
never emitted. Chrome and its temporary profile are always terminated/removed.

#### 3.7.2 Selection ambiguity reconciliation (`KIW8-SELECTION-READ-V1`)

This command is permitted exactly once only after the browser emitted
`selection-save-ambiguous` or its execution channel lost the terminal line
after preserving `selection-preflight`. A5 must pin the preflight revision,
count and hash as `KIW8_SELECTION_PRIOR_REVISION`,
`KIW8_SELECTION_COUNT`, and `KIW8_SELECTION_EXPECTED_SHA256`. It performs one
read-only GET and never sends another PUT:

```text
node --experimental-strip-types --input-type=module -e 'import{createHash}from"node:crypto";import{parseResearchEnvelope}from"./lib/keyword-intelligence-validation.ts";const h=x=>createHash("sha256").update(String(x)).digest("hex"),origin=process.env.KIW8_ORIGIN,cookie=process.env.KIW8_OWNER_A_COOKIE,id=process.env.KIW8_RESEARCH_ID,prior=Number(process.env.KIW8_SELECTION_PRIOR_REVISION),count=Number(process.env.KIW8_SELECTION_COUNT),expected=process.env.KIW8_SELECTION_EXPECTED_SHA256;if(!Number.isSafeInteger(prior)||prior<1||!Number.isSafeInteger(count)||count<1||count>100||!/^[0-9a-f]{64}$/u.test(expected||""))throw Error("KIW8_SELECTION_RECONCILE_INPUT");const r=await fetch(`${origin}/api/keyword-research/${encodeURIComponent(id)}`,{headers:{Accept:"application/json",Cookie:cookie},redirect:"error",signal:AbortSignal.timeout(20000)}),body=await r.json();if(r.status!==200)throw Error("KIW8_SELECTION_RECONCILE_STATUS");const v=parseResearchEnvelope(body),actual=h(JSON.stringify(v.selection));let outcome;if(v.id===id&&v.selection.length===count&&actual===expected&&v.selectionRevision===prior+1&&!v.selectionConflicts.length)outcome="saved";else if(v.id===id&&v.selection.length===count&&actual===expected&&v.selectionRevision===prior&&!v.selectionConflicts.length)outcome="rolled_back";else throw Error("PARENT_BLOCKED_SELECTION_AMBIGUITY");console.log(JSON.stringify({mode:"selection-reconcile",researchIdSha256:h(id),outcome,priorRevision:prior,selectionRevision:v.selectionRevision,selectionCount:v.selection.length,selectionSha256:actual}))'
```

Only outcome `saved` may advance. `rolled_back` is a definitive stopped outcome;
the save is not repeated. The successful browser line or reconciliation line is
pinned in A5 as literal saved revision/count/hash before handoff.

#### 3.7.3 Independently resumable same-key handoff (`KIW8-HANDOFF-V1`)

The initial and ambiguity-reconciliation invocations use the same literal
source and differ only in `KIW8_HANDOFF_MODE=initial|reconcile`. A5 must pin
`KIW8_SELECTION_SAVED_REVISION` and `KIW8_SELECTION_SAVED_SHA256`; the source
imports and enforces `CLIENT_REQUEST_ID_PATTERN`. Execute `initial` once. Only
after its `handoff-ambiguous` line or a proven lost terminal response may the
same source execute once as `reconcile`; it does not load or save selection.

```bash
KIW8_HANDOFF_MODE=initial node --experimental-strip-types --input-type=module - <<'KIW8_HANDOFF_V1'
import { createHash } from "node:crypto";
import { CLIENT_REQUEST_ID_PATTERN, parseRunHandoffEnvelope } from "./lib/keyword-intelligence-validation.ts";
const h=x=>createHash("sha256").update(String(x)).digest("hex"),origin=process.env.KIW8_ORIGIN,cookie=process.env.KIW8_OWNER_A_COOKIE,id=process.env.KIW8_RESEARCH_ID,started=process.env.KIW8_WINDOW_STARTED_AT,revision=Number(process.env.KIW8_SELECTION_SAVED_REVISION),selectionSha256=process.env.KIW8_SELECTION_SAVED_SHA256,mode=process.env.KIW8_HANDOFF_MODE;
if(!["initial","reconcile"].includes(mode)||!Number.isSafeInteger(revision)||revision<2||!/^[0-9a-f]{64}$/u.test(selectionSha256||""))throw Error("KIW8_HANDOFF_INPUT");
const key=`kiw8_${h(`${id}\n${revision}\n${started}`).slice(0,60)}`;if(!CLIENT_REQUEST_ID_PATTERN.test(key))throw Error("KIW8_HANDOFF_KEY");const requestBody={expectedSelectionRevision:revision,clientRequestId:key};let r;
try{r=await fetch(`${origin}/api/keyword-research/${encodeURIComponent(id)}/runs`,{method:"POST",headers:{Accept:"application/json","Content-Type":"application/json",Cookie:cookie},body:JSON.stringify(requestBody),redirect:"error",signal:AbortSignal.timeout(20000)})}catch{console.log(JSON.stringify({mode:"handoff-ambiguous",attempt:mode,researchIdSha256:h(id),selectionRevision:revision,selectionSha256,clientRequestIdSha256:h(key)}));process.exit(75)}
const body=await r.json(),expectedStatus=mode==="initial"?201:200;if(r.status!==expectedStatus)throw Error(mode==="initial"?"KIW8_HANDOFF_INITIAL_STATUS":"KIW8_HANDOFF_RECONCILE_STATUS");const handoff=parseRunHandoffEnvelope(body);if(handoff.statusUrl!==`/api/runs/${handoff.run.id}`)throw Error("KIW8_HANDOFF_CONTRACT");
console.log(JSON.stringify({mode:"handoff",attempt:mode,handoffStatus:r.status,researchIdSha256:h(id),selectionRevision:revision,selectionSha256,runIdSha256:h(handoff.run.id),clientRequestIdSha256:h(key)}))
KIW8_HANDOFF_V1
```

For the sole reconciliation invocation, replace only the command prefix with
`KIW8_HANDOFF_MODE=reconcile`; the heredoc body is byte-identical. Status `201`
is accepted only by `initial`; status `200` is accepted only by `reconcile`.
A second lost response, a mismatching strict envelope, any other status, or an
unequal identity stops. There is at most one selection PUT, one initial handoff
POST, one ambiguity-only same-key POST, zero second research POSTs and zero
Confirm/Start requests.

#### 3.7.4 Independently resumable owner-B denial (`KIW8-OWNER-DENIAL-V1`)

After either handoff success record, run the following exact source once from
`email_scraper/`. It resolves the sole run ID inside one read-only production
transaction and uses it in memory for the owner-B requests. The raw run ID,
database URL and cookie never cross the process boundary or enter evidence.

```bash
node --input-type=module - <<'KIW8_OWNER_DENIAL_V1'
import { createHash } from "node:crypto";
import { execFileSync } from "node:child_process";
import { SecretsManagerClient } from "@aws-sdk/client-secrets-manager";
import { loadPipelineSecrets } from "./src/aws-pipeline/secrets.js";
import { createPrismaClient } from "./src/prisma-client.js";
const h=x=>createHash("sha256").update(String(x)).digest("hex"),origin=process.env.KIW8_ORIGIN,cookie=process.env.KIW8_OWNER_B_COOKIE,id=process.env.KIW8_RESEARCH_ID;
if(!/^https:\/\/[^/?#]+$/u.test(origin||"")||!/^kr_[A-Za-z0-9_-]{24}$/u.test(id||"")||!cookie)throw Error("KIW8_OWNER_DENIAL_INPUT");
const stack=JSON.parse(execFileSync("aws",["cloudformation","describe-stacks","--stack-name","storesignal-production-pipeline","--profile","storesignal-dev","--region","ap-south-2","--no-cli-pager","--output","json"],{encoding:"utf8",maxBuffer:16777216})).Stacks?.[0],outputs=Object.fromEntries((stack?.Outputs||[]).map(x=>[x.OutputKey,x.OutputValue]));if(typeof outputs.PipelineSecretArn!=="string")throw Error("KIW8_OWNER_DENIAL_SECRET_OUTPUT");
const secrets=await loadPipelineSecrets({client:new SecretsManagerClient({region:"ap-south-2",maxAttempts:3}),secretId:outputs.PipelineSecretArn}),prisma=createPrismaClient(secrets.databaseUrl);let runId;
try{runId=await prisma.$transaction(async tx=>{await tx.$executeRawUnsafe("SET TRANSACTION READ ONLY");const schemas=await tx.$queryRawUnsafe("SELECT current_schema() AS schema");if(schemas.length!==1||schemas[0].schema!=="public")throw Error("KIW8_OWNER_DENIAL_SCHEMA");const rows=await tx.$queryRawUnsafe(`SELECT "runId" FROM "KeywordResearchHandoff" WHERE "researchId"=$1`,id);if(rows.length!==1||typeof rows[0].runId!=="string"||!rows[0].runId)throw Error("KIW8_OWNER_DENIAL_CARDINALITY");return rows[0].runId},{maxWait:5000,timeout:30000})}finally{await prisma.$disconnect()}
for(const [name,path,code]of[["research",`/api/keyword-research/${encodeURIComponent(id)}`,"KEYWORD_RESEARCH_NOT_FOUND"],["run",`/api/runs/${encodeURIComponent(runId)}`,"RUN_NOT_FOUND"]]){const r=await fetch(`${origin}${path}`,{headers:{Accept:"application/json",Cookie:cookie},redirect:"error",signal:AbortSignal.timeout(20000)}),v=await r.json();if(r.status!==404||Object.keys(v).join(",")!=="error"||!v.error||Object.keys(v.error).sort().join(",")!=="code,message"||v.error.code!==code)throw Error(`KIW8_OWNER_B_${name.toUpperCase()}`)}
console.log(JSON.stringify({mode:"owner-denial",researchIdSha256:h(id),runIdSha256:h(runId),ownerBResearchStatus:404,ownerBRunStatus:404,privateProjectionCount:0}))
KIW8_OWNER_DENIAL_V1
```

The denial runner is read-only and independently resumable once after a proven
transport-only failure because the handoff is already durable and it creates no
state. A contract/status failure is not retried. It accepts only exact
`{error:{code,message}}`, with `KEYWORD_RESEARCH_NOT_FOUND` and `RUN_NOT_FOUND`
respectively; any 200, extra key or private projection fails.

The exact safe transition records are: browser `selection-preflight` followed
by `browser-save` or `selection-save-ambiguous`; optional
`selection-reconcile`; then `handoff` or `handoff-ambiguous`; then
`owner-denial`. Raw/private state never crosses a process boundary. A5/S2 advance only from the recorded safe
revision/count/hash and action-attempt discriminator; S3/A6 retain only hashes,
counts, booleans and statuses.

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
| `W8-LIVE-09` | `I001-HANDOFF` | owner-A real rendered completed dashboard exposes table checkbox plus enabled save control; its mandatory click settles after one selection PUT; one initial or ambiguity-only same-key run-handoff succeeds | saved revision/hash reconcile; one immutable Run, `1..100` RunQueries, exact lineage; owner B gets two exact denials; Run unconfirmed; zero Confirm/Start, PipelineStage/PipelineTask/downstream messages/calls |
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

Execute `KIW8-BROWSER-SAVE-V1` once. Require the rendered completed dashboard,
real table checkbox, selection review and enabled save control witnesses, then
the mandatory click-generated PUT, status 200, revision `prior+1`, exact
selection hash/count preservation, settled enabled UI, zero error alert, and
zero `/runs` or `/start` POST. A terminally missing response permits only the
one read-only `KIW8-SELECTION-READ-V1` invocation after A5 pins the browser's
preflight record; require outcome `saved`. Outcome `rolled_back` or ambiguity
stops, and no second browser/save invocation occurs.

After A5 pins the saved revision/hash, execute `KIW8-HANDOFF-V1` in `initial`
mode exactly once. Require status 201 and strict handoff parsing. A terminally
lost response permits only one byte-identical invocation in `reconcile` mode,
with the same deterministic pattern-validated key and selection revision;
require status 200. The successful invocation performs the exact strict handoff
contract checks and emits only hashes/status. Then execute
`KIW8-OWNER-DENIAL-V1` once; its read-only transaction resolves the durable run
inside the process and its two owner-B GETs must emit exact 404 statuses and
`privateProjectionCount:0`. Execute `W8-NC-05`. A transport-only failure of the
denial runner permits one identical read-only retry; no command reloads or
resaves selection, creates another research, generates a new handoff key, or
clicks Finalize/Confirm/Start.

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
| `G1` | root: `sha256sum` the two standards/A1-A5/A8/S1; `git status --short`, `git rev-parse HEAD`, packet `sha256sum`/`wc -c`; execute §3.6 `KIW8_MANIFEST_METADATA_SEMANTIC_PASS`; backend: the two measurement commands in §6.2 P6 | none | exit 0; all pinned hashes/bytes/counts/cold imports exact; semantic persisted-manifest-produced-at oracle passes and its stage-created-at control falsifies; W7 commits clean | 1 | gitignored measurement refresh only; `$0` | local read/build transport only: E8.1 one identical recovery after zero surviving process/write proof | `EV-KI-W8-I001-G1.json` in S3 entry |
| `G2` | backend: exact P2/P3/P4/P5/P6 commands and `KIW8-DB-V1 baseline`; §3.6 queue observer; §3.2 discovery | `AWS_PROFILE,AWS_REGION,KIW8_HOST_READ_TOKEN`; P4 credentials remain in memory | exit 0; exact safe schemas; every DG passing; `W8-LIVE-01` activated | 1 | read-only AWS/host/provider/Neon; `$0` | GET/read transport may recover once under E8.1 only after zero mutation/cost/result; missing host/P5 record is a blocker, not recovery | `EV-KI-W8-I001-G2.json` |
| `G3` | backend: exact §6.3 create-change-set command | `KIW8_ACCOUNT_ID` equal current A5 | exit 0 `CHANGE_SET_REVIEWED`; three object versions and reviewed projection exact; NC01/02 activated | 1 | three versioned AES256 S3 writes plus one unexecuted change set; `$0` | stable object keys and change-set name/ID reconcile any lost response; never recreate if identity exists | `EV-KI-W8-I001-G3.json` |
| `G4` | backend: exact two §6.4 commands | `KIW8_ACCOUNT_ID` | exit 0 `REVIEWED_CHANGE_SET_APPLIED` then `EXPECTED_DISABLED_KEYWORD_STACK_VERIFIED`; LIVE03 | 1 | execute one reviewed disabled stack update; `$0` | describe exact A5 change-set ID and stack events; if final state cannot be proven, stop without second execute | `EV-KI-W8-I001-G4.json` |
| `G5` | §3.4 exact host update/readback, then frontend first `KIW8-API-V1` command, `KIW8-DB-V1 resolveResearch/progress`, §3.6 observers | G2 allowlist plus `KIW8_HOST_WRITE_TOKEN,KIW8_ORIGIN,KIW8_OWNER_A_COOKIE,KIW8_APPROVED_SEED,KIW8_WINDOW_STARTED_AT` | host exact; POST 202 or exact DB reconciliation; one queued row/message; zero work/cost; LIVE04/05 and NC03/04 | host 1; create POST 1 | one host config update and one research/message; provider `$0` | host readback by configuration revision; create uses §3.7 no-retry DB reconciliation | `EV-KI-W8-I001-G5.json` |
| `G6` | backend: exact three §6.7 activation commands; frontend second `KIW8-API-V1`; backend `KIW8-DB-V1 progress/artifactRows` plus §3.6 queue/Lambda/alarm/log/S3 observers | `KIW8_ACCOUNT_ID,KIW8_ORIGIN,KIW8_OWNER_A_COOKIE,KIW8_RESEARCH_ID` plus AWS fixed values | active inspector; same ID progresses/completes; artifacts validated; LIVE06/07/08 | activation 1; canary 1; bounded polls only | one activation stack update; same research may make provider calls; total `<=3.00000000` | activation reconciled by exact change-set/stack/mapping state; paid ambiguity uses durable attempt rows only; never repeat activation/research | `EV-KI-W8-I001-G6.json` |
| `G7` | frontend: `KIW8-BROWSER-SAVE-V1`; ambiguity-only `KIW8-SELECTION-READ-V1`; `KIW8-HANDOFF-V1` initial and ambiguity-only reconcile; backend: `KIW8-OWNER-DENIAL-V1`, `KIW8-DB-V1 handoff/progress/artifactRows`, §3.6 queue/Lambda/alarm/log/S3 observers, literal registry/digest command | browser: `KIW8_ORIGIN,KIW8_OWNER_A_COOKIE,KIW8_RESEARCH_ID`; reconcile adds `KIW8_SELECTION_PRIOR_REVISION,KIW8_SELECTION_COUNT,KIW8_SELECTION_EXPECTED_SHA256`; handoff adds `KIW8_WINDOW_STARTED_AT,KIW8_SELECTION_SAVED_REVISION,KIW8_SELECTION_SAVED_SHA256,KIW8_HANDOFF_MODE`; denial adds `KIW8_OWNER_B_COOKIE` plus AWS fixed values; observers use AWS fixed values | real rendered completed dashboard and save control; mandatory click save and UI settle; one strict handoff; independently resumable owner-B two-404 denial; zero confirm/start/downstream/private projection; 10/6 sets and digests; LIVE09/CONF01/NC05/06 | browser/save 1; selection reconcile 0..1 only after ambiguity; handoff initial 1; same-key reconcile 0..1 only after ambiguity; owner denial 1 plus one transport-only read recovery; final reads 1 | one selection revision and one unconfirmed Run; `$0` additional | browser preflight safe record is the selection reconciliation identity; no second PUT; deterministic `CLIENT_REQUEST_ID_PATTERN` key is the handoff identity; initial accepts 201 only, reconcile accepts 200 only; denial resolves run identity inside its read-only process; DB handoff row is final authority | `EV-KI-W8-I001-G7.json` |

All `EV-KI-W8-I001-G*.json` names identify exact JSON blocks appended to S3;
they are not workspace files. Every row's action requires its separate current
A5 approval predicate. G6 additionally requires ACT-05 and ACT-06 together.

### 7.2 Mechanical execution-choice lint and falsification

Before parent review and again at P6, run from root:

```text
node <<'KIW8_EXECUTION_CHOICE_LINT'
const fs = require("node:fs");
const original = fs.readFileSync("KEYWORD_INTELLIGENCE_KI_W8_SUBWINDOW_CHECKLIST.md", "utf8");
const between = (source, start, end) => source.slice(source.indexOf(start), source.indexOf(end, source.indexOf(start)));
const replaceIn = (source, start, end, before, after) => {
  const section = between(source, start, end);
  if (!section.includes(before)) throw new Error("KIW8_CONTROL_MEMBER");
  return source.replace(section, section.replace(before, after));
};
function lint(source) {
  const assignable = between(source, "## 6. `KI-W8-I001`", "## 7. Frozen gates");
  const p5 = between(source, "### 3.3 Exact P5 prerequisite record", "### 3.4 Exact ACT-03 prerequisite record");
  const db = between(source, "### 3.5 Exact production Neon observer", "### 3.6 Exact AWS dynamic observers");
  const browser = between(source, "#### 3.7.1", "#### 3.7.2");
  const selection = between(source, "#### 3.7.2", "#### 3.7.3");
  const handoff = between(source, "#### 3.7.3", "#### 3.7.4");
  const denial = between(source, "#### 3.7.4", "## 4. Coverage");
  const operations = between(source, "### 7.1 Literal per-gate operation manifest", "### 7.2 Mechanical execution-choice lint");
  const broad = ["dashboard form or same-origin route", "if required", "normal authenticated GETs", "read-only durable inspection", "Search exact inspected projections", "execute only the P2-recorded host operation", "may use only a current official provider", "inspect only", "read Neon", "as appropriate", "as needed", "choose", "decide", "determine", " etc.", "Loading keyword research", "third literal KIW8-API-V1"];
  const hits = broad.filter((value) => assignable.includes(value));
  if (hits.length) throw new Error(`KIW8_EXECUTION_CHOICE:${hits.join("|")}`);
  if (p5.includes("select endpoint") || !p5.includes("PARENT_BLOCKED_PROVIDER_CAPABILITY_PROTOCOL")) throw new Error("KIW8_P5_EXECUTOR_CHOICE");
  for (const heading of ["### 3.2 Exact admissible host discovery", "### 3.3 Exact P5 prerequisite record", "### 3.4 Exact ACT-03 prerequisite record", "### 3.5 Exact production Neon observer", "### 3.6 Exact AWS dynamic observers", "### 3.7 Exact production frontend/browser/API runners", "### 7.1 Literal per-gate operation manifest"]) if (!source.includes(heading)) throw new Error(`KIW8_MECHANISM_MISSING:${heading}`);
  if ((db.match(/SELECT count\(\*\)::int AS "nonterminalResearchCount"/g) || []).length !== 2) throw new Error("KIW8_DB_BASELINE_QUERY_COUNT");
  for (const value of ["/usr/bin/google-chrome", "Network.setCookie", "surface:keyword-table", "surface:selection-review", "b.click()", "Network.responseReceived", "mode:\"browser-save\"", "forbiddenRunOrStartRequests:0"]) if (!browser.includes(value)) throw new Error(`KIW8_BROWSER_UI_ACTIVATION:${value}`);
  if (browser.includes("fetch(`/api/keyword-research/${encodeURIComponent(id)}/selection`")) throw new Error("KIW8_BROWSER_DIRECT_API_SAVE");
  for (const value of ["mode:\"selection-reconcile\"", "v.selectionRevision===prior+1", "v.selectionRevision===prior", "outcome=\"rolled_back\"", "the save is not repeated"]) if (!selection.includes(value)) throw new Error(`KIW8_SELECTION_AMBIGUITY_CODE:${value}`);
  if (selection.includes("method:\"PUT\"") || selection.includes("/runs`")) throw new Error("KIW8_SELECTION_RECONCILE_MUTATION");
  for (const value of ["CLIENT_REQUEST_ID_PATTERN.test(key)", "expectedStatus=mode===\"initial\"?201:200", "KIW8_HANDOFF_MODE=initial", "KIW8_HANDOFF_MODE=reconcile", "mode:\"handoff-ambiguous\""]) if (!handoff.includes(value)) throw new Error(`KIW8_HANDOFF_AMBIGUITY_CODE:${value}`);
  for (const value of ["SET TRANSACTION READ ONLY", "KeywordResearchHandoff", "KEYWORD_RESEARCH_NOT_FOUND", "RUN_NOT_FOUND", "privateProjectionCount:0"]) if (!denial.includes(value)) throw new Error(`KIW8_OWNER_DENIAL_CODE:${value}`);
  if (!operations.includes("| Gate | Exact command/runner and cwd | Environment allowlist |")) throw new Error("KIW8_GATE_ENV_ALLOWLIST");
  for (let number = 1; number <= 7; number += 1) if (!operations.includes(`| \`G${number}\` |`) || !operations.includes(`\`EV-KI-W8-I001-G${number}.json\``)) throw new Error(`KIW8_GATE_ROW:${number}`);
}
lint(original);
const controls = [
  replaceIn(original, "## 6. `KI-W8-I001`", "## 7. Frozen gates", "Execute `KIW8-BROWSER-SAVE-V1` once", "dashboard form or same-origin route"),
  replaceIn(original, "### 3.5 Exact production Neon observer", "### 3.6 Exact AWS dynamic observers", "SELECT count(*)::int AS \"nonterminalResearchCount\"", "SELECT 0 AS \"removedBaseline\""),
  replaceIn(original, "### 7.1 Literal per-gate operation manifest", "### 7.2 Mechanical execution-choice lint", "| Gate | Exact command/runner and cwd | Environment allowlist |", "| Gate | Exact command/runner and cwd | removed |"),
  replaceIn(original, "### 3.3 Exact P5 prerequisite record", "### 3.4 Exact ACT-03 prerequisite record", "PARENT_BLOCKED_PROVIDER_CAPABILITY_PROTOCOL", "select endpoint"),
  replaceIn(original, "#### 3.7.1", "#### 3.7.2", "b.click();return true", "fetch(`/api/keyword-research/${encodeURIComponent(id)}/selection`,{method:\"PUT\"});return true"),
  replaceIn(original, "#### 3.7.3", "#### 3.7.4", "expectedStatus=mode===\"initial\"?201:200", "expectedStatus=mode===\"initial\"?201:201")
];
for (const [index, control] of controls.entries()) {
  let falsified = false;
  try { lint(control); } catch { falsified = true; }
  if (!falsified) throw new Error(`KIW8_EXECUTION_CONTROL_${index + 1}`);
}
console.log("KIW8_EXECUTION_CHOICES_ZERO controls=6");
KIW8_EXECUTION_CHOICE_LINT
```

Self-falsification runs on an in-memory copy only. Replace the exact ACT-04
command with the former `dashboard form or same-origin route`, delete one SQL
query, delete one operation-table environment allowlist, and change P5's
fail-closed state to `select endpoint`. Then separately replace the browser's
`b.click()` with a direct API PUT and replace handoff
`expectedStatus=mode==="initial"?201:200` with
`expectedStatus=mode==="initial"?201:201`. Each of the six separate in-memory
mutations must make the lint exit nonzero. It emits only the failing rule name.
Required outcome is six falsifications plus the unmodified
`KIW8_EXECUTION_CHOICES_ZERO` pass. The manifest-produced-at semantic control
in §3.6 is a seventh independent falsification and must also pass at G1.

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
- [ ] `I8` Execute one real rendered browser save; use only the frozen read-only selection reconciliation if its terminal response is ambiguous; parent-pin the saved revision/hash; execute one initial handoff and only its same-key reconcile mode after ambiguity; prove owner-B denial, privacy, cost and zero downstream/Confirm/Start; execute no second save/research. Evidence: ___
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
