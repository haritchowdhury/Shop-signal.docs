# Pre-G14 Corrective Execution Specification

## Status and authority

Status: **READY / ASSIGNABLE**

- Product contract: `AWS_ASYNC_DEPLOYMENT_DIRECTION.md`, SHA-256
  `747cd5b398f3edd6d8c146187260f05c475abec006712d04a0df5301cd7c601f`.
- Prior frozen implementation specification:
  `FINAL_LAMBDA_SQS_S3_MIGRATION_EXECUTION_PLAN.md`, SHA-256
  `6fbbdaee89d20ceb6a9b369af43b79c0dfb17c36217d5dc33accd04e6caefdfe`.
- This specification owns only corrective Window G-R10. It does not authorize
  G14, infrastructure edits, AWS access, provider calls, production database
  access, secrets, deployment, staging, frontend changes, or cutover.
- Live authority remains `ACTIVE_EXECUTION_STATE.md`. Evidence is appended only
  to `AWS_PIPELINE_EXECUTION_EVIDENCE.md`.

## Source-grounded finding

The mandatory post-G-R9 review ran the exact disposable-PostgreSQL recovery
matrix against the current clean backend commit `4019f9193972d0b07e2fd59eedefd79222708e6f`.
Sixteen tests passed. The
`duplicate_delayed_or_reversed_delivery` subtest reached the real final
publication path and failed twice with Prisma `Transaction API error:
Transaction not found` at
`PrismaRunRepository.publishAwsFinalResults()`.

Observed closure:

- `publishAwsFinalResults()` is the sole final atomic publication writer.
- It performs the complete cache, per-run traffic, global work, profile, score,
  grant, stage, fingerprint, and Run-visibility transition inside one Prisma
  interactive transaction.
- It supplies no transaction options, so Prisma's five-second interactive
  transaction timeout controls the production path.
- The transaction locks the PipelineStage and Run before publication through
  `assertCompleteAggregatorInTransaction()`. Competing aggregation/recovery
  owners must acquire those same row locks.
- The aggregation lease is exactly 120 seconds. The final service renews the
  lease immediately before stopping its monitor and entering publication.
- A temporary boundary filter used only to isolate the reproduction was removed;
  the backend worktree returned to its pre-review state.

Classification: **OBSERVED correctness/deployment blocker**. A remote Neon
transaction budget shorter than the bounded publication operation can reject a
correct run after all provider work. G14 cannot safely deploy that behavior.

## Locked corrective decision

The final publication transaction uses exactly:

```text
maxWait: 5_000 ms
timeout: 90_000 ms
```

The options apply only to `publishAwsFinalResults()`. They do not change its
signature, transaction body, isolation level, ordering, lease duration, retry
policy, or any other repository transaction. Ninety seconds remains below the
120-second freshly renewed aggregation lease and leaves 25 seconds for
transaction acquisition and Lambda/service overhead. The locked Stage and Run
rows continue to fence competing owners for the transaction's lifetime.

A timeout remains a retryable invocation failure: PostgreSQL rolls back the
entire publication transaction, `resultsAvailable` remains false, the SQS
record is retried, and the normal fenced aggregator path reclaims after lease
expiry. No partial visibility or provider replay is introduced.

## Window G-R10 — Final-publication transaction budget

**Objective:** Make the already-atomic final Neon publication executable over
the deployed remote transport while retaining rollback, lease fencing, replay,
and visibility-last behavior.

**Depends on:** G-R9 completed; the reproducible review finding above.

**Consumes exact outputs:** current `publishAwsFinalResults()`, corrected G-R8
rollback tests, corrected G-R9 matrix, direct disposable-schema helper.

**Produces exact outputs:** explicit final transaction budget and a passing
duplicate/reverse boundary under the real isolated transport.

**Owned files/symbols:**

- `email_scraper/src/prisma-run-repository.js::publishAwsFinalResults`
- `email_scraper/test/aws-pipeline-final.integration.test.js`
- `email_scraper/test/aws-pipeline-end-to-end.integration.test.js` only if a
  permanent assertion is necessary; its 16-row set and default full execution
  may not be weakened or filtered
- packaging expectation only if the repository edit changes the emitted file
  inventory

**Non-goals/prohibited actions:** no schema/migration, transaction-body reorder,
new retry, lease change, batch/provider change, frontend/API/IaC/AWS/provider/
production action, fixture reduction, or acceptance based on a partial matrix.

### G-R10-T1 — Exact transaction option

Change the existing final `$transaction(async transaction => { ... })` call to
pass `{ maxWait: 5_000, timeout: 90_000 }` as its second argument. Do not apply
those values globally and do not change any callback statement.

Mechanical trace:

```text
fresh 120-second aggregator lease -> publishAwsFinalResults -> Prisma waits at
most 5 seconds -> one atomic transaction runs at most 90 seconds -> locked
stage/Run and visibility-last commit -> duplicate/reverse assertion
```

### G-R10-T2 — Decisive verification

Run, in order:

```text
node --test test/aws-pipeline-final.test.js
ALLOW_DATABASE_TESTS=true node -r dotenv/config --test --test-concurrency=1 test/aws-pipeline-final.integration.test.js
ALLOW_DATABASE_TESTS=true node -r dotenv/config --test --test-concurrency=1 test/aws-pipeline-end-to-end.integration.test.js
ALLOW_DATABASE_TESTS=true npm run test:integration
npm run build:lambda
npm run measure:lambda
npm run check:secrets
npm test
git diff --check
```

The full 16-boundary matrix must execute; a boundary filter is not acceptance
evidence. Restricted localhost failures use the existing identical approved
rerun procedure. The evidence records the original two failures, the corrected
duplicate/reverse outcome, full matrix count, integration count, package
measurements, full regression count, and absence of external actions.

## Ledgers

### Interface and persistence

No callable, argument, return value, schema, field, index, migration, message,
artifact, key, fingerprint, timestamp, configuration environment variable, or
public response changes. The only changed interface to an installed dependency
is Prisma `$transaction(callback, options)` at the named call site.

### Atomicity, failure, and recovery

| Boundary | Durable state | Required result |
|---|---|---|
| Before transaction acquisition | completed traffic tasks; aggregating stage | wait at most 5 seconds; failure writes nothing |
| During transaction before visibility | locked Stage/Run; uncommitted writes | timeout rolls back every write |
| After stage update before Run visibility | same transaction | timeout rolls back stage and all publication writes |
| Commit response lost | completed Run/fingerprint | existing identical replay observes terminal state; no duplicate provider call |

### External calls and privacy

No external/provider call is added or moved. No new value is logged or stored.
The correction changes only a Prisma client control option containing two
public integers.

### Database transport and package closure

Verification uses `test/helpers/isolated-postgres.js`, the non-pooled direct
migration endpoint, explicit disposable `search_path`, schema-local migration
history, and the existing cleanup guard. The final handler must be rebuilt,
cold-imported, inventoried, and remain within existing package limits.

## Decision-completeness audit

| Category | Locked choice | Evidence | Task | Decisive assertion |
|---|---|---|---|---|
| Files/symbols | one final transaction call | source trace | T1 | diff inspection |
| Interfaces/dependencies | Prisma callback options only | installed Prisma 6.19.3 | T1 | integration reaches commit |
| Schema/persistence | unchanged | schema/diff search | T1 | no migration |
| Transactions/atomicity | 5s wait, 90s execution, unchanged body | repeated timeout | T1/T2 | failpoint rollback corpus |
| Identity/authorization | unchanged locked Run/Stage | coordinator helpers | T2 | duplicate/reverse E2E |
| Messages/artifacts | unchanged | G-R9 schemas | T2 | full 16-row matrix |
| External calls/cost | none | call graph | T1/T2 | provider counters unchanged |
| Failure/recovery | rollback then normal SQS/lease recovery | existing service | T2 | boundary convergence |
| Configuration/limits | constants at call site | 120s lease | T1 | exact source values |
| Database transport | direct disposable schema | isolation helper | T2 | migration-locality checks |
| Build/runtime | final handler rebuilt | build scripts | T2 | cold import/inventory |
| Visibility/privacy | visibility remains last | transaction body | T2 | failpoints/resultsAvailable |
| Cross-window output | safe G14 prerequisite | post-G-R9 review | T2 | G14 remains unassigned until pass |

## Simulations and independent audit

Forward simulation: a duplicate/reversed trigger reaches the one final owner,
renews its lease, acquires locked Stage/Run rows, performs the unchanged atomic
writes, and commits within the explicit budget. A failure before commit rolls
back and later retry follows durable coordinator evidence.

Backward simulation: `resultsAvailable=true` still traces to the final Run
update, completed Stage, grants/profiles/scores/traffic, validated artifacts and
terminal task set inside one committed transaction. No timeout branch can
produce a visible partial result.

Fresh searches found no other final-publication writer and no configured Prisma
transaction options. The correction touches no external call, configuration
snapshot, package dependency, or AWS boundary.

```text
BLOCKERS BEFORE START: none
USER ACTIONS BEFORE START: none
PREDICTABLE FUTURE GATES: G14 remains behind the post-G-R10 deployment packet and exact AWS mutation approval
PAID/MUTATING APPROVALS NOT YET GRANTED: all AWS/provider/secret/deployment actions
PLANNED USER STOP: after local G-R10 acceptance, before any AWS mutation
```

Readiness certificate: **READY**. The finding, exact code change, dependency
interface, transaction/failure behavior, ownership, verification, transport,
package rerun, evidence destination, and stop point are fixed. No
implementation-affecting choice is delegated.
