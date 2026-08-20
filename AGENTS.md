# StoreSignal Workspace Agent Instructions

These instructions apply to the entire workspace. A deeper `AGENTS.md` adds
directory-specific rules; it does not override the locked AWS architecture or
authorization boundaries here.

## Start here

The workspace contains a coordination root and two nested repositories:

- backend: `email_scraper/`
- frontend: `frontend/`

Before AWS-pipeline planning, implementation, review, or documentation work,
read these files in order:

1. `AWS_ASYNC_DEPLOYMENT_DIRECTION.md`
2. `TARGET_LAMBDA_SQS_S3_EXECUTION_FLOW.md`
3. `PRELIMINARY_LAMBDA_SQS_S3_MIGRATION_PLAN.md`
4. `FINAL_LAMBDA_SQS_S3_MIGRATION_EXECUTION_PLAN.md`
5. `email_scraper/docs/research/LAMBDA_SQS_S3_PAYLOAD_DISCOVERY_REPORT.md`
6. `PARENT_AGENT_CHECKLIST_INSTRUCTIONS.md`

For creation of a future execution checklist, read
`PROJECT_AGNOSTIC_DECISION_COMPLETE_CHECKLIST_AUTHORING_STANDARD.md`. It is the
sole authoritative authoring standard. `DECISION_COMPLETE_CHECKLIST_AUTHORING_STANDARD.md`
and `PARENT_AGENT_CHECKLIST_INSTRUCTIONS.md` are retained as historical context;
they do not override the project-agnostic standard.

The post-G13 review rescinded G11-G13 acceptance; G10 remains the last accepted
gate. Section 10A of `FINAL_LAMBDA_SQS_S3_MIGRATION_EXECUTION_PLAN.md` is the
frozen decision-complete correction specification: G-R7 corrects G11, G-R8
corrects G12, and G-R9 corrects G13. `ACTIVE_EXECUTION_STATE.md` is the sole
authority for the current assignment, sequence, status, and stop point.
`AWS_PIPELINE_EXECUTION_EVIDENCE.md` is the sole destination for new execution
evidence. Never edit the frozen specification to record progress.

Documents
under `email_scraper/docs/history/` are historical context and must not drive
implementation. `AWS_BEGINNER_SETUP_GUIDE.md` describes learning resources, not
the production contract.

For frontend work, also read `frontend/AGENTS.md` and the relevant installed
Next.js documentation it requires.

## Window execution is mandatory

The current window status and next assignable window are recorded only in
`ACTIVE_EXECUTION_STATE.md`; do not infer them from memory, conversation
history, Git history, the frozen plan, its historical evidence index, or this
file. Verify the product-contract and plan hashes in that state before editing.

The former G-R4-through-G13 standing assignment ended at G13 and grants no
authority to start G-R7 or any later window. Once a corrective window is
decision-complete and explicitly assigned:

- execute the windows sequentially from
  `FINAL_LAMBDA_SQS_S3_MIGRATION_EXECUTION_PLAN.md`;
- verify its dependencies before editing;
- stay inside its ownership and non-goal boundary;
- run its required adversarial and regression checks;
- append that window's report to `AWS_PIPELINE_EXECUTION_EVIDENCE.md` and update
  only `ACTIVE_EXECUTION_STATE.md` before advancing;
- record changed files/migrations, tests, exact commands/outcomes, evidence,
  skipped checks/reasons, residual risks and user prerequisites;
- if its acceptance checks pass, immediately begin the next window; and
- after the active state's `stop_after`, stop for the user's planned review. Do
  not begin G14, G15, or the
  final reliability review.

A window boundary is not a blocker. Passing checks do not require a separate
parent invocation, independent parent verification, explicit reassignment, or
user input. A failing check must first be diagnosed and corrected within the
active window when the locked specification already determines the fix. Stop
only when the remaining condition genuinely matches `Stop and escalate`.

Before a parent assigns a window from any future checklist, its eight-artifact
package must pass Sections 4 through 11 of
`PROJECT_AGNOSTIC_DECISION_COMPLETE_CHECKLIST_AUTHORING_STANDARD.md`.
Architectural prose,
wildcard ownership, fixture references without authoritative literal expected
members, or broad verbs are not executable task specifications. If any agent
would need to choose a dependency, schema, public
interface, transaction protocol, module boundary, configuration policy, failure
semantics, or acceptance behavior, the checklist remains `DRAFT / NOT
ASSIGNABLE`; the parent must resolve the choice and record its mechanical trace.

During an explicitly authorized continuous sequence, the executing agent owns
each window's implementation verification, evidence, status transition, and
move to the next dependency-satisfied window. The completed G-R4-through-G13
sequence supplies no current authorization because its post-G13 review failed.
Only a later independent parent review may perform G-FR or mark the migration
complete. Never reuse a window ID. Corrections are append-only `G-R1`, `G-R2`,
and so on; do not silently rewrite completed-window history.

Outside the standing G-R4-through-G13 assignment, do not infer authorization
for G14, G15, deployment, provider calls, or AWS mutations. Read-only
inspection and plan review remain allowed.

## Locked architecture

Do not substitute a different architecture.

- Neon/Postgres is the sole durable application database and coordinator.
- S3 stores private, encrypted, versioned, immutable artifacts.
- SQS provides at-least-once delivery, retries, DLQs, and backpressure.
- Lambda runs bounded workers and aggregators.
- The existing frontend/API/auth/query-review control plane remains.
- One discovery task/message corresponds to one confirmed `RunQuery.id`.
- One lead task/message corresponds to one stable domain needing lead work.
- One `traffic.domain` message corresponds to one eligible domain. Compatible
  messages are grouped only by Lambda event-source consumption; never create an
  SQS `itemIds` batch contract.
- A stage completes only from Neon terminal evidence for its immutable expected
  set. Queue emptiness, S3 counts, and S3 events are never completion signals.
- Every stage uses idempotent first-terminal transitions, bounded leases,
  generation/token fencing, deterministic fingerprints, explicit zero-count
  advancement, and one conditional aggregator owner.
- A worker writes and validates S3 before its terminal Neon result, then sends an
  aggregation check before acknowledging its SQS record.
- Results become visible only in the final fenced Neon transaction.

Do not introduce Fargate, Step Functions, DynamoDB coordination, S3-event
fan-in, queue-emptiness fan-in, a whole-run Lambda, a second shop identity
algorithm, or an API/auth/frontend rewrite.

## Behavior that must be preserved

- Query generation, probing, editable review, revision conflicts, and explicit
  confirmation remain authoritative.
- Use `stableShopIdentity()`, `Shop.stableKey`, `shopIdForStableKey()`, and
  `runStoreId()`; do not invent AWS-only identity.
- `RunStore` and `Lead` remain run-specific history. Global profile/cache
  existence never grants access.
- Preserve `UserShop` and `UserShopDiscovery` and owner-scoped reads.
- Reuse requires identity, scope, metric set, contract, and freshness/latest
  month—not row existence.
- Both CrUX REST and CrUX BigQuery remain independently required, cached,
  terminal, persisted, and observable inside one combined traffic worker.
- Preserve DataForSEO batching, paid ledger, cost reservation, and ambiguity.
  Do not create per-domain DataForSEO bulk tasks.
- Preserve one latest-table lookup and one bounded multi-origin BigQuery query;
  do not create one query per domain.
- Lead fetching remains HTTP-first with at most five ranked same-store pages.
- Browserless uses `/function`, one sequential session per domain, sequential
  primary/fallback tokens, a 45-second ceiling, and initial lead concurrency two.
- Initial discovery and traffic/CrUX Lambda reserved concurrency are each one;
  do not configure SQS event-source `MaximumConcurrency=1` because AWS permits
  that mapping value only from two upward.
- Traffic SQS records are triggers, not provider batch boundaries. One
  Neon-fenced stage-wide owner loads the immutable run work set and preserves
  run-wide DataForSEO/BigQuery batching before per-domain terminal fan-out.
- Completed production `runs/` artifacts do not automatically expire at launch.

## Contract and privacy rules

The v1 fixtures under `email_scraper/test/fixtures/aws-pipeline/v1/` and the
contract section of the final checklist are the internal boundary authority.
External provider shapes remain inside the existing strict adapters.

- Use strict deterministic Zod parsers.
- Do not probe alternate envelopes, aliases, fields, credential branches,
  cursors, or error shapes until something parses.
- Missing or moved consumed fields produce typed privacy-safe contract drift.
- Unknown fields affect behavior only after they are catalogued and tested.
- Never store or log raw provider bodies, unrestricted HTML, credentials,
  tokens, authorization headers, credential-bearing URLs, customer contact data,
  or unnecessary private fields.
- SQS carries identity, generation, fingerprints, and S3 references—not business
  documents.
- Do not commit `.env`, credentials, production IDs, or private live evidence.

## AWS and paid-provider authorization

Do not treat prior probe approvals as standing authorization for a new task.

- Tell the user before any AWS mutation and state the exact resources/actions.
- Production AWS creation requires the explicit approval gate in G14.
- Secret installation, event-source enablement, paid/provider smoke calls, and
  cutover require the separate approvals in G15.
- Default AWS work is read-only. Do not mutate learning resources unless the
  current request authorizes the exact learning operation.
- Never create production resources or `runs/` artifacts during local windows.
- Never purge a queue, DLQ, bucket, prefix, database rows, or stack for
  convenience. Destructive actions require exact targets and explicit approval.
- Keep credentials out of Git, SQS, S3, Neon coordinator rows, logs, frontend
  responses, command output, and evidence.

Configured learning resources are in `ap-south-2` under profile
`storesignal-dev`: bucket `signalshop-buk`, source queue
`storesignal-dev-learning`, DLQ `storesignal-dev-learning-dlq`, and Lambda
`storesignal-dev-learning-worker`. They are not production contracts. Its
lifecycle aborts incomplete multipart uploads after seven days; completed
objects do not expire.

## Repository and editing boundaries

The coordination root is in an owner-controlled relocation state: the former
tracked nested tree appears deleted while active root documents and nested
repositories appear untracked. Preserve that state. Do not stage, commit,
repair, move, or reverse it unless explicitly requested.

- Preserve unrelated dirty-worktree changes.
- Do not edit `frontend/` during backend migration windows unless the assigned
  window explicitly owns it. G15 treats frontend as read-only; a needed change
  opens a corrective window.
- Put AWS pipeline code under `email_scraper/src/aws-pipeline/` and
  infrastructure under `email_scraper/infrastructure/aws/`.
- Use forward-only Prisma migrations. Never rewrite/delete historical rows,
  CrUX enum values, migration history, or live evidence.
- Use `apply_patch` for manual edits and keep generated/build output out of Git.
- Do not stage or commit unless explicitly requested.

## Verification baseline

Run commands from `email_scraper/` unless a window states otherwise.

- focused tests named in the window;
- `npm run db:generate` and `npm run db:validate` for schema work;
- `ALLOW_DATABASE_TESTS=true npm run test:integration` only with an isolated
  `TEST_DATABASE_URL` different from production;
- migration-backed integration tests must use
  `test/helpers/isolated-postgres.js`: Prisma Migrate uses a non-pooled direct
  test connection with an explicit disposable `search_path`, verifies
  `current_schema()` and the schema-local `_prisma_migrations`, and never uses
  or cleans `public` for test isolation;
- `npm run check:secrets`;
- `npm test`; and
- handler build/measurement commands after G3.

The backend baseline is 272 tests: 265 pass and seven guarded integrations skip
without database opt-in. Localhost suites may fail in a restricted sandbox;
rerun the identical suite with required sandbox approval rather than treating
`listen EPERM` as a product failure.

For authorized frontend verification, run `npm run check` from `frontend/`.
Passing tests alone is insufficient: acceptance must demonstrate the window's
behavior, concurrency, transaction, privacy, recovery, cost, and ownership
invariant with the evidence named in the checklist.

## Stop and escalate

Stop the assigned window and report one concise blocker when:

- authoritative documents still contradict after applying their authority;
- an external consumed field lacks observed sanitized evidence;
- a decision changes parsing, ownership, authorization, transaction atomicity,
  history, retention, deletion, provider economics, or locked architecture;
- a required isolated database, permission, secret reference, approval, or live
  prerequisite is absent; or
- completing the task would cross the assigned ownership boundary.

Do not replace unavailable evidence with a guessed contract. Do not continue
into a later window to work around a blocker.
