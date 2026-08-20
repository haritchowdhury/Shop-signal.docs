# Decision-Complete Checklist Authoring Standard (Historical)

## Status and purpose

This file is retained as historical context and is not authoritative for new
checklist authoring. The sole current authority is
`PROJECT_AGNOSTIC_DECISION_COMPLETE_CHECKLIST_AUTHORING_STANDARD.md`. This file
previously superseded `PARENT_AGENT_CHECKLIST_INSTRUCTIONS.md`; neither
historical document overrides the project-agnostic standard.

Normative language below is preserved only to explain the historical design; it
does not govern a current assignment.

The standard exists to make a high-reasoning parent agent do all material
discovery and design work before implementation begins, so a default-reasoning
implementation agent can execute the resulting windows mechanically without
inventing architecture, contracts, data shapes, failure behavior, or execution
policy.

Success means all three of the following:

1. The implementation sequence can run through its authorized stop point
   without routine parent or user intervention.
2. An implementation agent stops and reports one precise blocker when reality
   contradicts the locked specification or a genuinely unavailable prerequisite
   is reached.
3. Before implementation starts, the parent tells the user every presently
   knowable account, approval, environment, live-evidence, and deliberately
   delayed decision gate, including exactly when it will occur and how execution
   will resume.

Passing tests after minor implementation debugging is expected. A successful
checklist eliminates product and architecture invention; it does not promise
that code will be written without ordinary defects.

## 1. Non-negotiable role boundary

### Parent planner

The parent planner owns every implementation-affecting decision:

- product behavior and exclusions;
- architecture and module boundaries;
- public and cross-module interfaces;
- schemas, migrations, indexes, uniqueness, and transaction boundaries;
- identity, ownership, authorization, visibility, and retention;
- idempotency, concurrency, leases, fencing, retry, recovery, and cancellation;
- provider selection, batching, cost controls, ambiguity, and rate limits;
- durable configuration, secrets validation, timeouts, and resource limits;
- external request/response contracts and strict parsing;
- window dependencies, ownership, acceptance, and execution policy; and
- all predictable prerequisites and decision gates.

The parent may not delegate a choice merely because either choice could be made
to work. If two materially different implementations could satisfy a task, the
task is not ready.

### Implementation agent

The implementation agent owns only:

- writing the prescribed code and migrations;
- private helper decomposition that cannot change a locked behavior or
  interface;
- local variable names and formatting;
- diagnosing and correcting ordinary implementation/test defects within the
  active window;
- running the prescribed verification;
- recording evidence; and
- advancing according to the active execution state.

It must not choose a missing product rule, durable formula, schema shape,
dependency, public signature, transaction protocol, retry policy, provider
behavior, or acceptance interpretation.

## 2. Required output package

The parent must produce four separate artifacts. A single large document that
mixes these responsibilities fails readiness regardless of its detail.

Authority is intentionally non-overlapping:

1. applicable `AGENTS.md` files govern repository conduct and authorization;
2. the locked product contract governs what the product must do;
3. the implementation specification governs how the named windows implement it;
4. the active execution state governs only what may execute now; and
5. the evidence log proves what happened but governs neither behavior nor live
   status.

When two artifacts speak to the same concern, the package is malformed; do not
invent a precedence rule to reconcile duplicated authority.

### A. Locked product contract

Contains the desired behavior, architecture, invariants, lifecycle definitions,
scope, exclusions, and supporting evidence. It changes only through an explicit
product decision or discovered contradiction.

### B. Decision-complete implementation specification

Contains the common technical contracts and ordered execution windows. It does
not contain mutable current status or accumulated implementation evidence.
Superseded task text must be moved to history, not left beside active task text.

### C. Active execution state

A short root-level file, normally `ACTIVE_EXECUTION_STATE.md`, is the sole
authority for what may run now. It must contain exactly one machine-scannable
state block and no historical narrative:

```yaml
state_version: 1
product_contract: ROOT_RELATIVE_CONTRACT_PATH
product_contract_revision: SHA256_OF_LOCKED_CONTRACT
plan: ROOT_RELATIVE_PLAN_PATH
plan_revision: SHA256_OF_FROZEN_IMPLEMENTATION_SPECIFICATION
mode: single_window | continuous_sequence
authorized_sequence: [G1, G2]
current_window: G1
current_status: READY | IN_PROGRESS | BLOCKED | COMPLETE
accepted_through: NONE
next_on_pass: G2 | STOP_FOR_REVIEW
stop_after: G2
blocker: null
allowed_actions: [local_source_edits, local_tests]
prohibited_actions: [deployment, paid_provider_calls]
user_gates: []
last_updated: ISO_8601_UTC
```

Rules:

- Do not repeat live status in `AGENTS.md`, the implementation specification,
  or the evidence log. Those files link to this state file.
- Compute and record the contract/specification revisions after readiness and
  before assignment. The implementation agent verifies both hashes before its
  first edit and at every window boundary.
- The implementation specification is frozen during its authorized sequence.
  A genuine correction creates a new specification revision and an explicit
  state transition; do not silently rewrite instructions underneath an active
  agent.
- Increment `state_version` for every transition.
- `current_window` must be a member of `authorized_sequence` unless the state is
  complete.
- `next_on_pass` must equal the next sequence member or the declared stop.
- A blocker replaces `null` with one stable blocker ID referenced in the
  evidence log.
- Update the state only after the current window's required checks and evidence
  are complete, or when recording a genuine blocker.
- Read `state_version` immediately before writing a transition. If it changed
  since the agent began the window, do not overwrite it; reconcile the
  concurrent owner as a coordination blocker.
- Committed state and working-tree state must be checked separately. An agent
  may not ignore a newer uncommitted coordination file merely because nested
  application code is at a clean commit.

### D. Append-only execution evidence

Contains window reports, commands, results, corrective findings, and review
evidence. It never controls what may execute. Historical wording in this file
cannot block or authorize work.

The parent must name all four paths in its final authoring report.

## 3. Phase 0 — Capture execution policy before technical planning

Record the user's orchestration intent before discovery begins:

- single window or continuous sequence;
- authorized first and last window;
- whether implementation agents may advance themselves after passing checks;
- where independent parent review occurs;
- which actions are local/read-only, externally mutating, paid, destructive, or
  approval-gated;
- the exact planned user stop point; and
- what constitutes a genuine blocker.

Default for an explicitly authorized continuous sequence:

- the same implementation invocation advances through every named window;
- each window is verified and recorded before the next begins;
- no parent verification or reassignment occurs at routine boundaries;
- ordinary code/test defects are fixed inside the active window;
- execution stops only for a genuine blocker or the declared final stop; and
- independent parent review occurs once after the sequence.

Never infer authorization for paid calls, cloud mutations, production data,
secret installation, deployment, or destructive action from authorization to
write local code.

## 4. Phase 1 — Build a source-grounded discovery dossier

The parent must inspect the current working tree, not merely the last commit,
and record exact evidence locations. At minimum, inventory:

1. applicable agent instructions and document authority;
2. entry points and every reachable caller/callee on the planned path;
3. public and cross-module signatures;
4. database models, migrations, constraints, indexes, and all writers/readers;
5. queues, messages, artifacts, object keys, handlers, and dispatchers;
6. external/provider/network/SDK calls, including calls hidden by retained
   helpers;
7. configuration, environment, secret, clock, randomness, and account reads;
8. identities, ownership checks, grants, and public visibility paths;
9. leases, locks, tokens, generations, deduplication, retries, cancellation,
   recovery, and process-restart paths;
10. existing tests, fixtures, test seams, build/package scripts, and observable
    baselines;
11. dirty-worktree changes and nested repository boundaries; and
12. unavailable live evidence, credentials, services, permissions, or user
    decisions.

For every database-backed verification path, inventory the actual connection
topology rather than treating one URL as sufficient: runtime/pooler endpoint,
direct migration/DDL endpoint, database identity, schema/search-path mechanism,
driver or adapter behavior, session reuse, advisory-lock behavior, migration
configuration precedence, and cleanup authority. Verify these properties
against the real test transport before claiming an isolated database is ready.

For every packaged or deployed entry point, inventory its **planned production
dependency closure**, not only the imports present in an initial scaffold. This
includes the module format of the entry point and bundled dependencies,
dynamic/CommonJS loading, Node built-ins, native binaries, generated clients,
runtime-loaded assets, package exports, and platform/runtime target. If later
windows will add imports, the parent must trace those planned imports through
their installed dependency trees before treating packaging as proven.

Classify each material fact:

- `OBSERVED`: directly supported by current source, schema, fixture, installed
  dependency, controlled probe, or authoritative documentation;
- `DECIDED`: the parent chose it within the user's product authority and records
  the reason and consequences;
- `DERIVED`: mechanically follows from observed inputs via a written formula;
- `UNKNOWN-BLOCKING`: implementation cannot safely begin until resolved;
- `DEFERRED-GATE`: cannot be known until a named earlier window produces exact
  evidence, but all possible branches and the owner are already specified; or
- `PARKED`: explicitly outside the authorized implementation sequence.

`INFERRED` is allowed in discovery notes but prohibited from the locked
implementation contract.

### Discovery closure rule

Discovery is not complete until negative searches are recorded for claimed
absence and the reachable sets are closed. Search for more than the expected
symbols: alternate writers, legacy callers, cancellation paths, configuration
reads, provider calls, and visibility paths are frequent sources of plan drift.

## 5. Phase 2 — Lock the product and lifecycle contract

Before creating windows, write the complete end-to-end lifecycle. For each
workflow state:

1. entry condition and trusted identity;
2. strict input parser and bounds;
3. ownership/authorization decision;
4. external calls and their cardinality;
5. durable pre-call evidence;
6. ordered durable writes and transaction boundaries;
7. artifact/message production and validation;
8. idempotency and deduplication key;
9. concurrency unit and owner;
10. lease/fence acquisition, renewal, expiry, and loss;
11. failure after each external or durable step;
12. duplicate, reverse-order, retry, and restart behavior;
13. terminal state and terminal evidence;
14. user-visible publication boundary; and
15. logging, redaction, metrics, and retention.

Write state-transition tables for durable state machines. For each transition,
name the actor, precondition/CAS predicate, writes, emitted work, replay result,
and forbidden transition.

If completion, visibility, authority, or retry behavior is described only in
prose and cannot be traced through these states, the contract is not locked.

## 6. Phase 3 — Close cross-cutting ledgers

Create only the ledgers applicable to the feature, but every reachable member
must appear exactly once in an applicable ledger.

### Interface ledger

For every new or changed callable, record the complete signature, argument
order, defaults, return union, safe thrown errors, caller, implementation file,
and consumer assertion.

### Persistence and atomicity ledger

For every durable field and write, record model/field/type/default/index,
migration behavior, writer, reader, visibility, and cleanup/retention. Every
multi-write sequence is either:

- `SAME TRANSACTION`, with the transaction-composable functions named; or
- `RECOVERED BOUNDARY`, with pre-boundary evidence, post-boundary evidence,
  exact retry action, and ambiguity behavior named.

### Database transport and isolation ledger

For every migration, DDL probe, integration test, and runtime database client,
record:

- exact database identity and proof it differs from production;
- pooled versus direct endpoint and which operation may use each;
- exact environment/config precedence for the migration CLI and runtime;
- database, namespace/schema, role, and session `search_path` selection;
- whether URL schema options are interpreted by the ORM, driver, server, or
  all three—never assume they are equivalent;
- preflight assertions made before migration or behavioral writes;
- proof that migration history, enums, tables, indexes, and columns were
  created only in the disposable namespace;
- sequential/concurrent execution policy and collision-free namespace grammar;
- cleanup target and `finally` behavior; and
- fail-closed behavior for a pooler, missing direct endpoint, `public` schema,
  schema/search-path mismatch, connection drift, or cleanup failure.

Migration-backed tests must use one named shared harness. A checklist may
permit an explicit test-direct URL or a deterministic provider-specific direct
derivation only when both branches and their validation are locked. It must
never repair isolation by deleting or rewriting shared/public objects.

### Message and artifact ledger

For every produced/read message or artifact, record:

- strict versioned schema/parser;
- deterministic key grammar;
- item identity;
- input-fingerprint formula;
- content-fingerprint formula;
- durable produced-at source;
- producer and consumer;
- missing, corrupt, conflicting, already-valid, and duplicate behavior; and
- exact recovery reconstruction using durable rows only.

### External-call ledger

For every network, paid, quota-limited, browser/session, provider, SDK, and
database call, record:

- exact caller and adapter;
- paid/mutating/rate-limited/read-only classification;
- durable pre-call state;
- request identity/idempotency support;
- timeout, SDK retries, application retries, concurrency, and batch limits;
- response validation and durable post-call write;
- crash-before-call, crash-after-call-before-write, and response-loss behavior;
- whether another live call is permitted; and
- decisive failure-injection test.

Do not claim exactly-once external execution without a provider-supported
idempotency mechanism and durable use of it. Represent irreducible uncertainty
as an explicit `ambiguous` state.

### Configuration ledger

For every reachable configuration read, classify it as behavior, provider or
account identity, credential material, infrastructure address, or telemetry.
Behavior and non-secret identity affecting replay, cost, output, batching,
limits, or timeouts must come from a durable versioned snapshot. Credentials
remain secret but must be validated against the snapshot before calls.

### Build and package ledger

For every executable, bundle, archive, container, layer, or deployment unit,
record:

- source entry point and final runtime/module format;
- the complete planned production dependency closure and which dependencies
  are bundled, externalized, copied, generated, or native;
- build tool/version and exact flags, target platform/runtime, handler/export,
  and required runtime files;
- package inventory, deterministic-build rule, size/resource bounds, and
  forbidden files;
- a representative production-closure build used before readiness;
- fresh-process cold import/startup and invocation checks against the emitted
  artifact rather than the source tree;
- the later window that first wires each material dependency into each entry
  point and therefore must repeat the emitted-artifact checks; and
- the exact owner and prescribed correction branch for predictable module
  interop, missing asset, externalization, native-binary, or runtime-target
  failures.

A package containing a placeholder, no-op, or unimplemented handler proves
only the build scaffold. It must be labelled `PROVISIONAL PACKAGING`; it cannot
certify the final runtime package, dependency compatibility, cold-start
behavior, memory, or size. A source import test, successful compilation, ZIP
creation, or cold import of an empty shell is not a substitute for importing
the emitted artifact with its planned production dependency closure.

When the final handler does not yet exist, create a disposable or test-only
representative entry point that imports the same planned runtime adapters,
SDKs, generated clients, native modules, and runtime assets. Build and
cold-import it with the exact production toolchain. Do not ship that probe. If
the representative closure cannot be constructed from known source and locked
design, packaging compatibility is `UNKNOWN-BLOCKING`, not an implementation
detail to discover after several windows.

### Ownership and recovery ledger

For every globally shared work/cache/dedup row, record claim, renew, reclaim,
complete, fail, cancel, legacy callers, and final settlement. For every recovery
query, reconstruct every field needed for the exact retry message/action from
the returned row. An unstated lookup is a missing contract.

### Set-equality certificate

Mechanically inventory at least these sets when applicable:

- tasks;
- public/cross-module callables;
- durable fields and writers/readers;
- messages and artifacts;
- external calls;
- runtime configuration reads;
- packaged/deployed entry points and their planned production dependency
  closures;
- identities/authority checks; and
- terminal/publication transitions.

Every source member must have one plan owner, ledger row, mechanical trace, and
decisive assertion. Every planned member must have a source/target anchor and
test owner. Extra or missing members fail readiness.

## 7. Phase 4 — Resolve blockers and announce gates before windowing

The parent must produce a `Preflight Gate Report` before declaring the checklist
ready.

### Resolve now

Anything discoverable from source, installed dependencies, repository history,
existing fixtures, safe read-only inspection, or already authorized probes must
be resolved by the parent. It may not be deferred to an implementation agent.

### Ask now

Ask the user before implementation when a missing product decision, account
choice, cost authorization, destructive action, production target, credential,
or permission is required before the authorized sequence can start.

### Predictable future gate

A gate may occur after a window only when its value genuinely depends on that
window's output. The checklist must still specify before execution:

- gate ID and reason;
- earliest window at which it can be resolved;
- exact producing command/artifact/measurement;
- complete allowed range or branch table;
- deterministic formula or selection rule for every branch;
- who may decide/check it;
- whether execution can continue automatically under each branch;
- exact action requiring user input, if any; and
- restart window and preserved evidence after resolution.

“Decide later,” “measure and choose,” or “configure as needed” is not a future
gate; it is an incomplete plan.

### Required report format

```text
BLOCKERS BEFORE START: none | [B-...]
USER ACTIONS BEFORE START: none | [U-...]
PREDICTABLE FUTURE GATES: none | [F-... with trigger and exact branches]
PAID/MUTATING APPROVALS NOT YET GRANTED: none | [A-...]
PLANNED USER STOP: <after window / reason>
```

If no items exist, say `none` explicitly. The parent must give this report to
the user immediately after authoring, not wait for an implementation agent to
discover a predictable gate.

## 8. Phase 5 — Compile execution windows

A window establishes one coherent capability or invariant and leaves the
repository in a deterministically verifiable state. Window boundaries are for
context management, not mandatory user/parent scheduling.

Split a window when it combines unrelated ownership, multiple independently
risky lifecycle transitions, or a contract discovery task with broad
implementation. Do not split merely to force handoffs. A continuous sequence
can contain several windows within one implementation invocation.

Every window must use this exact structure.

### Window header

```text
ID:
Objective:
Depends on:
Consumes exact outputs:
Produces exact outputs:
Owned files/symbols:
Shared-file permissions:
Non-goals/prohibited actions:
```

### Task specification

For each task, state:

1. source file and symbol;
2. target file and symbol;
3. complete interface/signature/schema;
4. exact ordered algorithm;
5. durable operation and external-call order;
6. transaction/recovered-boundary classification;
7. identity, key, fingerprint, and timestamp formulas;
8. failure/retry/duplicate/restart/cancellation behavior;
9. fixed config, bounds, timeouts, batching, and concurrency;
10. exact callers to change;
11. exact obsolete behavior to remove or preserve; and
12. named tests, setup, operation, and observable assertions.

Broad verbs such as `implement`, `wire`, `support`, `reuse`, `derive`, or
`preserve` are permitted only after all twelve mechanical details are supplied.

### Mechanical trace

Every task includes:

```text
observed source -> prescribed change -> target symbol -> exact caller ->
durable/external effect -> named assertion -> next-window consumer
```

If any arrow requires “the agent can determine it,” the task fails readiness.

### Adversarial verification

Specify applicable tests for happy path, strict invalid input, duplicates,
reverse order, failure after every durable/external boundary, concurrency,
lease expiry/loss, process death, retry/restart, authorization, migration replay,
partial dispatch, resource exhaustion, privacy, and premature visibility.

Name exact test files and assertions. A test command alone is insufficient.

For a window that adds or changes a packaged entry point's material import
closure, acceptance must rebuild the emitted deployment artifact and run its
fresh-process import/startup, inventory, native/runtime-file, deterministic,
size, and invocation checks. It must not rely on measurements from a prior
shell/scaffold window. The task must explicitly own any build/package files
needed by its already-prescribed correction branch, or name a corrective
window that the active state may insert and execute automatically without a
user/parent scheduling gate.

### Acceptance and handoff

Acceptance must describe observable behavior and exact evidence, not “tests
pass.” The window evidence record must include changed files, migrations, tests,
commands/outcomes, skipped checks/reasons, residual risks, user prerequisites,
external actions, and dirty work preserved.

At a passing boundary, the agent follows `ACTIVE_EXECUTION_STATE.md`; the
window must not contain its own contradictory stop/assignment instruction.

## 9. Decision-completeness gate

For each window, the parent must answer all applicable rows with an exact choice,
evidence, task, and assertion:

| Category | Locked choice | Evidence | Task | Decisive assertion |
|---|---|---|---|---|
| Files and symbols | | | | |
| Interfaces/dependencies | | | | |
| Schema/persistence | | | | |
| Transactions/atomicity | | | | |
| Identity/authorization | | | | |
| Messages/artifacts | | | | |
| External calls/cost | | | | |
| Failure/retry/recovery | | | | |
| Configuration/limits | | | | |
| Database transport/isolation | | | | |
| Build/package/runtime closure | | | | |
| Visibility/privacy | | | | |
| Cross-window output | | | | |

`N/A` requires a reason proving the category cannot be affected. An applicable
empty or vague cell fails the entire checklist.

The parent must then run two simulations.

### Forward simulation

Start at the product entry point and simulate normal execution plus failure
after every external call and durable write. At each step answer:

- What exact data exists?
- Who owns the next operation?
- What happens on duplicate/restart?
- Can the next message/action be reconstructed?
- Can anything become visible too early?

### Backward simulation

Start from each final/public output and terminal state. Trace every field and
decision backward to one validated input, durable write, or deterministic
formula. Then trace recovery actions backward to sufficient durable evidence.

Any missing edge returns the checklist to draft. It does not become an
implementation-agent discovery task.

## 10. Independent authoring audit

Before marking the checklist assignable, perform a fresh audit pass that does
not rely on the checklist's conclusions. Re-run source searches and compare the
actual reachable sets with the ledgers and window tasks.

The audit must explicitly attempt to falsify:

- interface completeness;
- nested-transaction feasibility;
- artifact/message reconstructability;
- provider call cardinality and retry claims;
- lease duration and renewal claims;
- shared-work ownership across run/stage transitions;
- durable configuration closure;
- migration/runtime connection separation, actual server `search_path`, and
  namespace-local migration history;
- final visibility and publication fencing;
- cancellation and legacy caller behavior;
- package/runtime/infrastructure setting validity;
- real emitted-artifact compatibility with the complete planned production
  dependency closure, including dependencies absent from early scaffolds; and
- execution-state consistency.

The same parent may perform this audit, but it must record fresh commands and
counterexample searches. Merely rereading its own prose is not an audit.

## 11. Readiness certificate

The checklist remains `DRAFT / NOT ASSIGNABLE` until the parent records all of
the following:

- product contract locked and contradiction-free;
- every fact classified and every blocking unknown resolved;
- all applicable lifecycle and cross-cutting ledgers closed;
- every database-backed acceptance path has passed its real transport,
  direct/pooler, schema/search-path, migration-history, and cleanup preflight;
- every deployable entry point has either passed representative
  production-closure packaging proof or is `UNKNOWN-BLOCKING`; no scaffold is
  presented as final package evidence;
- set-equality certificate passed;
- every window has a complete task map, decision audit, and mechanical trace;
- forward and backward simulations passed;
- independent authoring audit passed;
- preflight gate report delivered to the user;
- execution mode and authorization boundary recorded;
- active-state file contains exactly one valid current state; and
- no implementation-affecting choice is delegated.

The certificate lists exact section/file locations and commands used. A summary
claim such as “architecture is complete” or “no unknown contracts remain” does
not satisfy it.

## 12. Execution semantics

For a continuous sequence, the assignment is exactly:

```text
Read ACTIVE_EXECUTION_STATE.md first and use it as the sole authority for live
status. Execute its authorized sequence from current_window through stop_after.
For each window, implement only the locked specification, run its required
checks, append evidence, and update the active state. If checks pass, continue
immediately to next_on_pass without requesting parent verification,
reassignment, scheduling, or user input. Diagnose and fix ordinary code/test
failures inside the current window when the locked specification determines the
behavior. Stop only for a genuine blocker. Do not cross the declared action or
authorization boundary.
```

### Genuine blockers — stop and report

Stop only when at least one is true:

1. Current source or runtime evidence contradicts a locked requirement and the
   specification does not determine the resolution.
2. A required implementation-affecting decision or formula is absent.
3. Required sanitized external evidence cannot be obtained within authorization.
4. A required database, credential, permission, account setting, approved paid
   call, cloud mutation, or live environment is unavailable.
5. The required fix crosses the active window's ownership or the user's action
   authorization.
6. A prescribed operation is unsafe, destructive, or impossible on the actual
   platform.
7. Required verification remains impossible after documented safe attempts and
   no equivalent decisive check exists.

### Not blockers — continue working

These do not justify returning to the user:

- reaching a window boundary;
- completing a handoff/evidence record;
- absence of a separate parent invocation;
- a normal compile, lint, type, unit, integration, or packaging failure;
- an implementation bug whose correct behavior is locked;
- a test fixture that must be updated according to the locked schema;
- a restricted-sandbox failure that can be rerun with available approval;
- discovering a named symbol at a nearby source location without changing the
  contract; or
- needing ordinary private helper decomposition.

A normal packaging failure remains non-blocking only when the locked
specification determines the correction and the active window or its
preauthorized corrective branch owns the required files. It becomes a genuine
blocker under item 1, 2, 5, 6, or 7 above when the checklist omitted the final
dependency closure, omitted the correction decision, or denied the active
sequence authority to apply it.

### Blocker report

```text
Blocker ID:
Active window/task:
Observed evidence and reproduction:
Locked requirement:
Why the specification cannot decide the fix:
Work completed and checks run:
Partial edits retained or removed:
Exact parent/user decision, evidence, permission, or ownership expansion needed:
Later windows not started:
```

A report that says only “parent verification required” or “handoff complete” is
invalid unless the active state explicitly declares that stop.

## 13. Corrections and completion

Before implementation begins, correct the draft in place and rerun readiness.
After a window has been accepted, preserve its evidence and use an append-only
corrective window for a concrete source/runtime finding. A corrective window is
not automatically a user gate; if its behavior is already dictated by the
locked product contract and lies within authorization, insert it into the active
continuous sequence and proceed after its checks pass.

Stop for parent/user resolution only when the corrective finding is a genuine
blocker under Section 12.

Independent parent reliability review occurs at the user-declared sequence
boundary. It inspects actual source and reruns risk-proportionate checks. It
opens bounded corrective windows for concrete findings and never silently
rewrites accepted history.

## 14. Mandatory authoring handoff to the user

After creating the checklist, the parent must report concisely:

1. whether it is `READY` or `DRAFT / NOT ASSIGNABLE`;
2. the four authoritative artifact paths;
3. the authorized execution sequence and planned stop;
4. the complete Preflight Gate Report;
5. the validation/audit performed; and
6. only unresolved genuine blockers.

Do not bury gates in the checklist. Do not return a long list of speculative
risks. Verify what can be verified, resolve what can be resolved, and report
only concrete remaining user obligations or blockers.

## Appendix A — Failure tests this standard must prevent

A new checklist is not ready unless the parent can show how its artifacts would
prevent each failure below:

| Historical failure class | Mandatory prevention |
|---|---|
| Missing distinction between absent and corrupt immutable artifacts | Artifact ledger requires separate missing/corrupt/conflict/already-valid behavior and tests. |
| Missing manifest identity, fingerprint, or durable timestamp | Message/artifact ledger requires exact formulas and produced-at source before window assignment. |
| Retry could not reconstruct the original message/input | Recovery ledger reconstructs every field from returned durable rows only. |
| Public repository method could not participate in a larger transaction | Atomicity ledger names transaction-composable primitives and rollback tests. |
| Shared work owner was lost across a lease/stage transition | Ownership ledger covers every old/new claim path through final settlement. |
| Provider retry/cardinality was asserted without durable evidence | External-call ledger requires pre/post artifacts, ambiguity, and crash tests. |
| Behavior changed when current environment drifted after dispatch | Configuration ledger requires durable versioned snapshots and drift tests. |
| Parent claimed readiness while reachable calls/config/writers were omitted | Set-equality certificate and negative source searches fail closed. |
| Implementation stopped at every successful window | Active state and continuous execution semantics make routine boundaries non-blocking. |
| Fresh agent read stale status from a large plan or Git commit | One short active-state authority; status is prohibited elsewhere; working tree and nested repositories are inspected separately. |
| Predictable account/approval/measurement gate surprised the user mid-run | Preflight Gate Report requires trigger, branches, owner, and resumption before implementation. |
| Placeholder handlers falsely certified final Lambda/package compatibility | Build/package ledger labels scaffold proof provisional, requires a representative production dependency closure before readiness, repeats emitted-artifact cold import when real imports are wired, and preauthorizes the prescribed correction owner. |
| A schema URL parameter falsely certified migration isolation while pooled/raw SQL reached `public` | Database transport/isolation ledger separates direct migration and pooled runtime endpoints, verifies server `current_schema()` plus namespace-local migration history before behavioral writes, centralizes disposable-schema setup, and forbids cleanup of shared/public objects. |
| Several shop/task owners shared one provider/cache identity, but planning retained only one owner or rejected equivalent cache fan-out | Identity, ownership, external-call, and persistence ledgers must separately enumerate global provider/cache keys and every per-shop owner. Require deterministic identity fan-in, all-owner claim/fencing, one provider call per unique identity, per-owner result fan-out, exact-equivalent global cache coalescing, conflicting-duplicate rejection, shared-reuse tests, and a two-owner/one-identity forward/backward simulation. |
| A shared repository module changed every emitted Lambda ZIP although the edited methods had only two runtime callers | Package closure is determined by emitted byte hashes, not business-call reachability. Before locking a selective deployment, build every deployable artifact after representative source edits or use bundler metadata proving exclusion; define the exact branch for either module isolation or expansion to the complete changed-hash set. |

For current authoring, a newly found planning failure is handled under the
change rules in
`PROJECT_AGNOSTIC_DECISION_COMPLETE_CHECKLIST_AUTHORING_STANDARD.md`; this
historical file is not updated as the governing standard.
