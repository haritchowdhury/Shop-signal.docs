# Parent-Agent Checklist Authoring Rules

Use this document when a parent agent must investigate a request, create an
implementation checklist, assign its windows to fresh agents, and independently
review the result.

The objective is a lean implementation with no guessed contracts, minimal
cross-window gaps, and evidence strong enough that checked boxes mean the
behavior actually works.

## 1. Parent-Agent Responsibility

The parent agent owns:

- discovery and safe probes,
- the authoritative product and technical contract,
- checklist structure, dependencies, and window sizing,
- subagent assignment and handoff quality,
- independent review of the completed source,
- corrective windows for concrete findings, and
- final completion.

Implementation agents own only their assigned window. They must not redefine
the product, start later windows, or mark overall verification complete.

The parent must inspect source, tests, migrations, and runtime evidence
directly. A subagent summary is a navigation aid, not proof.

## 2. Establish One Source Of Truth

Before planning, identify and record:

1. the authoritative product contract or knowledge base,
2. the active execution checklist,
3. applicable `AGENTS.md` files,
4. supporting research and evidence, and
5. superseded or parked documents.

Resolve contradictions before implementation. Conversation history and old
plans must not be required execution inputs. A fresh agent should be able to
execute a window using the current repository, the authoritative documents,
and that window alone.

Never reuse a window identifier. Preserve history with stable names such as
`G1`, `G2`, `G3`, followed by `G-R1` for a later correction.

## 3. Discover Before Dividing Work

The parent must inspect the current repository before writing implementation
windows. Use read-only probes by default.

Discovery must identify, as applicable:

- the current behavior and reproducible failure,
- relevant source, schema, migration, test, configuration, and documentation
  paths,
- trusted identity and authorization boundaries,
- external request, response, callback, webhook, and error contracts,
- repeated gates across APIs, workers, repositories, UI, configuration, and
  tests,
- durable writes, external calls, queues, cursors, leases, retries, and
  recovery paths,
- live data or migrations that must be preserved,
- existing dirty-worktree changes, and
- unavailable evidence or user prerequisites.

For every important discovery, distinguish:

- **observed** — supported by current source, schema, fixture, documentation, or
  controlled runtime evidence;
- **inferred** — plausible but not proven; it cannot become an implementation
  contract;
- **unknown** — must be resolved, explicitly deferred, or recorded as a
  blocker.

If an unknown affects parsing, ownership, authorization, data loss, historical
imports, transaction safety, or destructive behavior, stop and resolve it
before implementation.

## 4. Lock Scope And Behavior

The checklist must state:

- the exact user-visible outcome,
- included behavior,
- explicit exclusions,
- parked and deferred work,
- supported providers or platforms,
- ownership and authorization rules,
- historical-data and retention policy,
- deployment boundary, and
- definitions of ambiguous states such as connected, queued, synchronized,
  deleted, retryable, failed, and complete.

Do not ask implementation agents to make product decisions. If discovery
contradicts the locked contract in a scope-changing way, the agent must stop
and return the decision to the parent.

## 5. Model Complete Lifecycles

Define each end-to-end workflow before splitting it across windows. For every
applicable workflow, identify:

1. entry condition,
2. trusted identity,
3. validation and strict parsing,
4. external calls,
5. durable writes and transaction boundary,
6. idempotency or deduplication key,
7. concurrency unit,
8. lease, lock, generation, or compare-and-swap fence,
9. failure behavior between durable steps,
10. retry and process-restart recovery,
11. terminal state,
12. user-visible result, and
13. telemetry and privacy behavior.

Order is not atomicity. If several writes must succeed or fail together, require
one transaction or an explicitly tested recovery protocol. A job-level lock is
not a resource-level lock unless the job is the true concurrency unit.

Every cross-window invariant must have one named owning window.

## 6. No Fallback Probing

Treat all external provider data as `unknown` until a strict deterministic Zod
parser owned by the provider adapter accepts it.

Every consumed field must have one exact, versioned, evidence-backed path.
Never probe alternate:

- root/data/result/response envelopes,
- snake_case/camelCase aliases,
- credential or identity branches,
- cursor names,
- request bodies,
- error shapes, or
- tool/action slugs until one succeeds.

Do not write logic equivalent to:

```ts
payload.data ?? payload.result ?? payload.response ?? payload
```

If multiple shapes are genuinely supported, capture evidence for each, give
each an explicit version or discriminator, and parse them as a documented
union. Sequential guessing is not compatibility.

Requirements for every active external contract:

- pin the provider/API/tool version where possible,
- retain sanitized provenance-labelled schema or controlled fixtures,
- catalogue every consumed field and intentionally ignored available field,
- keep raw provider shapes inside the adapter,
- return normalized internal domain contracts,
- reject missing, moved, or malformed consumed fields with a typed,
  privacy-safe contract-drift error,
- add positive and negative parser fixtures, and
- fail verification if active code uses an undocumented, `REMOVE`, `PARKED`,
  or `UNDECLARED` mapping.

Unknown additive fields may be rejected or intentionally ignored under a
documented extension policy. They must never affect behavior before being
catalogued and tested.

Do not store raw provider bodies, secrets, tokens, signatures, credentials, or
sensitive content in fixtures, logs, telemetry, or tracking documents.

## 7. Define Safety Invariants

List the invariants that must remain true across all windows. Select only those
relevant to the project, including:

- tenant and ownership isolation,
- no client-supplied authority,
- no lost durable work,
- monotonic cursor or version movement,
- atomic multi-write transitions,
- correct resource-level serialization,
- duplicate and reverse-order safety,
- idempotent retry,
- lease-expiry and process-restart recovery,
- no unauthorized historical import,
- forward-only migration and data preservation,
- bounded pagination, retries, concurrency, and retention,
- privacy-safe logs, fixtures, and telemetry, and
- truthful UI state.

Each invariant must map to an owning window, deterministic tests, and the final
review.

## 8. Divide Work Into Execution-Sized Windows

A window should establish one coherent capability, contract, migration, or
reliability invariant. Split a window when it contains independently risky
transaction boundaries, unrelated subsystems, or both external-contract
discovery and broad implementation.

Every window must contain:

### ID, status, and objective

Use a stable unique ID and one concrete outcome.

### Dependencies and preconditions

Name completed windows, required fixtures, migrations, services, permissions,
and user inputs. If a prerequisite is absent, the agent records the exact
blocker and stops.

### Required reading and current-state evidence

Name the relevant contract sections, prior verification notes, source areas,
and reproducible starting behavior.

### Ownership and non-goals

Name files or areas the window owns, narrowly shared files it may touch, and
behavior it must preserve. Explicitly prohibit unrelated refactors and later
scope.

### Contracts and ordered tasks

State the invariant being established and list implementation steps in
dependency order.

### Adversarial verification

Cover applicable cases:

- happy path,
- missing, malformed, and boundary input,
- duplicate and reverse-order delivery,
- failure after every durable step,
- different concurrent operations on the same resource,
- lease loss, process death, retry, and restart,
- provider/network/database failure,
- authorization and cross-tenant attempts,
- migration replay and data preservation,
- resource-cap exhaustion,
- privacy/redaction, and
- stale or misleading UI state.

Sequential unit tests are not proof of concurrency safety. Source-text
assertions are not proof of runtime behavior.

### Required commands

List focused tests and applicable regression, type, lint, schema, migration,
build, browser, worker, security, privacy, and diff-hygiene checks.

### Acceptance

Every criterion must be observable and map to source plus test, migration,
database, controlled-provider, browser, or live evidence appropriate to the
claim. “Tests pass” or “all trackers agree” is not a behavioral acceptance
criterion.

### Handoff and stop condition

Require the agent to record:

- changed files and migrations,
- tests added,
- exact commands and outcomes,
- evidence locations,
- skipped checks and reasons,
- residual risks and user prerequisites, and
- confirmation that later windows were not started.

Then the agent stops.

## 9. Decision-Complete Implementation Specification

An execution window is assignable only when its implementation specification is
**decision-complete**. Decision-complete means the implementation agent writes,
connects, and verifies code, but does not choose the architecture, data model,
dependency, module boundary, public interface, transaction protocol, failure
semantics, configuration policy, or acceptance behavior.

The parent owns those decisions. Repository inspection by an implementation
agent may locate an already named symbol or confirm starting behavior; it must
not be used to design an omitted part of the assignment.

### Required implementation map

For every task in every implementation window, the parent must specify all
applicable items below:

1. **Source anchor** — exact existing file and symbol being retained, modified,
   extracted, called, or replaced.
2. **Target anchor** — exact target file and new or changed symbol. Name exports,
   handler entry points, schemas, repository methods, scripts, and configuration
   keys rather than referring only to a directory or subsystem.
3. **Interface** — inputs, outputs, relevant types or schema versions, error
   result, and caller/callee relationship. New shared interfaces and error codes
   are chosen and named by the parent.
4. **Ordered behavior** — the required algorithm and durable-operation order,
   including validation, external calls, writes, transaction boundaries,
   dispatch, acknowledgement, and visibility.
5. **Persistence contract** — exact models/tables, fields, types, defaults,
   enums, relations, uniqueness, checks, indexes, compare-and-swap predicates,
   and migration behavior. If raw SQL is required, state the required predicate
   and atomic outcome even when the agent writes the final SQL syntax.
6. **Boundary mapping** — exact fixture/provider/artifact/message fields consumed
   and produced, required versus optional rules, bounds, discriminators,
   fingerprints, and key grammar. “Implement the fixture” is not sufficient.
7. **Failure and retry semantics** — typed outcome at every material failure
   point and the exact durable state expected after retry, duplicate delivery,
   lease loss, cancellation, and process death.
8. **Fixed configuration** — selected dependency and version policy, runtime,
   build mode, handler, environment keys, limits, timeouts, batch/concurrency
   settings, and deterministic derivation formula for values that depend on a
   measurement from an earlier window.
9. **Call-site and removal map** — exact callers to update and obsolete symbols,
   paths, feature branches, or contracts to remove or leave untouched.
10. **Verification map** — exact test file and named behavior to add or modify,
    fixture used, setup, operation, and observable assertions. Merely naming a
    test command or failure category is not enough.
11. **Window output** — exact files, exports, migrations, generated artifacts,
    evidence, and guarantees that become inputs to the next window.

Use a table or equally explicit task blocks. Repeating broad repository context
does not replace this map.

### Ambiguity is a failed gate

Words such as `implement`, `add`, `extract`, `reuse`, `wire`, `support`,
`preserve`, `derive`, `pin`, `configure`, `narrowly`, and `as needed` identify an
outcome, not an executable instruction. They may remain only when the same task
also names the exact anchors, interface, ordered behavior, and verification that
make the operation mechanical.

The following also make a window unassignable:

- wildcard-only ownership such as `src/example/**` without an exact file/symbol
  task map;
- alternatives such as “A or B”, “choose”, “determine”, or “where appropriate”
  that delegate an implementation-affecting choice;
- “match current behavior”, “use the fixture”, or “follow Section X” without an
  exact mapping to current symbols and required outputs;
- a new database model described only conceptually rather than field by field;
- a new module without its filename, exports, callers, and failure contract;
- a deferred value without a named owner, prerequisite measurement, formula or
  bounded selection rule, and verification;
- acceptance that can pass while two materially different implementations are
  still possible; or
- an instruction to discover information that the parent could have resolved
  from the repository or existing evidence before assignment.

Implementation agents retain discretion only over formatting, local variable
names, and private code organization that cannot change a named interface,
contract, invariant, behavior, dependency, durable state, or test outcome.

### Mandatory parent decision audit

Before marking the checklist ready, the parent must add a decision audit for
each window with these columns:

| Decision category | Locked choice | Source/evidence | Implementing task | Verification |
|---|---|---|---|---|
| Files and symbols | Exact anchors | Repository lines/contracts | Task ID | Test/assertion |
| Interfaces and dependencies | Exact names/signatures/selections | Existing API or parent decision | Task ID | Import/build/contract test |
| Data and transactions | Exact schema/order/fence | Schema and lifecycle evidence | Task ID | Migration/integration test |
| Failure, retry, and limits | Exact outcome/bounds | Locked lifecycle/provider evidence | Task ID | Adversarial test |
| Cross-window output | Exact produced contract | Dependency map | Task ID | Consumer test/precondition |

An applicable empty cell is a failed gate. Mark a category `N/A` only with a
one-sentence reason demonstrating that the window cannot affect it.

The parent must then perform and record a mechanical trace for every task:

```text
source symbol -> prescribed change -> target symbol -> caller -> test assertion
```

If the trace requires the parent to say “the agent can figure that out,” the
specification is incomplete. The parent must resolve it before assignment.

An implementation agent that encounters an omitted implementation-affecting
decision stops without choosing. The parent updates the unstarted window and
reruns its decision audit. Missing checklist detail is not a reason to start a
discovery window when the answer already exists in source or recorded evidence.

### Hard readiness enforcement

- The active checklist remains `DRAFT / NOT ASSIGNABLE` until every window has a
  complete decision audit and mechanical trace.
- The parent may not check the planning-readiness gate from architectural prose,
  section references, or intended behavior alone.
- “No unknown contracts” and “architecture is locked” do not prove that coding
  instructions are decision-complete.
- A readiness claim must cite the decision-audit location for every window and
  explicitly state that no implementation-affecting choice is delegated.
- If later review finds a delegated decision that the audit marked complete,
  treat it as a parent-plan defect: stop assignment, correct every affected
  unstarted window, and record the defect rather than asking the implementation
  agent to improvise.

### Required source-grounded proof packet

A completed decision-audit table is a claim, not evidence. Before the parent
may change `DRAFT / NOT ASSIGNABLE`, the checklist must also contain a proof
packet for every unstarted window. The parent must build the packet from the
current source, schema, migrations, fixtures, installed dependency contracts,
and authoritative provider documentation. It must contain all of the following:

1. **Exact signature ledger.** Spell every new or changed callable as a complete
   signature, including argument order, defaults, return union, thrown safe
   errors, and every caller to change. Descriptions such as “publication
   method”, “repository helper”, or “dispatcher input” do not count.
2. **Atomicity ledger.** For every task that mentions two durable writes, mark
   them either `SAME TRANSACTION` and name the transaction-composable functions,
   or `RECOVERED BOUNDARY` and name the durable evidence and exact retry action.
   A repository method that opens its own transaction cannot be listed inside
   another transaction unless an exact transaction-parameterized primitive is
   specified.
3. **Recovery reconstruction ledger.** Starting only from each recovery query's
   returned row, mechanically construct the exact queue URL, message type,
   message body, manifest identity, produced-at value, fingerprint, and
   generation. If any field requires an unstated lookup or an unavailable row,
   the producer/repository contract is incomplete.
4. **Artifact reachability ledger.** For every S3 key written or read, name its
   strict schema/parser, metadata identity, input-fingerprint formula,
   content-fingerprint source, producing task, consuming task, and behavior for
   missing, conflicting, corrupt, and already-valid material. A named key with
   no schema or no replay rule fails readiness.
5. **Persistence materialization ledger.** Map every artifact field to the exact
   Neon model/field writer and map every downstream read back to the persisted
   field. Include global-profile preservation, owner grants, intermediate
   visibility, summaries, scoring inputs, and final fingerprint inputs.
6. **Lease-duration proof.** Name the renewal function, renewal interval,
   injected clock/timer seam, ownership check immediately before and after each
   external or durable operation, and the test that advances beyond one lease
   duration. Merely naming a lease duration is incomplete.
7. **External-call ambiguity ledger.** For each paid or rate-limited call, name
   the durable pre-call state, post-response write, crash-before-write outcome,
   retry permission, batching key, cardinality bound, and source-artifact
   reconciliation rule. Do not promise that a pre-durable unknown response can
   never repeat unless the provider supplies an idempotency contract that is
   actually used.
8. **Infrastructure validity evidence.** Validate every selected runtime,
   timeout, batch, concurrency, visibility, retention, and IAM setting against
   the installed tool schema or current official service contract. Account
   concurrency and Lambda reserved concurrency must be distinguished from an
   event-source mapping's allowed scaling values.
9. **Negative source searches.** Record searches for every claimed existing
   caller, cancellation path, writer, parser, and adapter. A statement such as
   “existing cancellation calls X” is prohibited unless the exact caller exists
   in current source.
10. **Independent contradiction pass.** After authoring, reread the proof packet
    from the final consumer backwards to the entry point. Any contradiction,
    missing field, impossible transaction nesting, or unreconstructable retry
    returns the entire checklist to `DRAFT / NOT ASSIGNABLE`; it is not deferred
    to the implementation agent.
11. **External-call-site closure.** Search the current source for every network,
    SDK, provider-client, browser/session, webhook, queue, object-store, and
    model invocation reachable from the planned path, including calls hidden
    behind retained pipeline helpers. Record each exact caller and classify it
    as paid, quota/rate-limited, mutating, free read-only, or unreachable. For
    every reachable call, map it to one external-call ambiguity row and one
    failure-injection test. The discovered call-site set and ledger set must be
    equal; “the main providers are covered” fails readiness.
12. **Durable-configuration closure.** Search every reachable call path for
    environment/config/secret reads. Classify each consumed value as behavior,
    identity/account selection, credential material, or telemetry-only.
    Behavior and non-secret provider identity that can affect replay,
    idempotency scope, cost, output, timeout, limits, or batching must come from
    a named durable versioned snapshot and fingerprint. Credential material
    stays secret but must be validated against the durable non-secret contract
    before dispatch. Record the producer, persisted field/artifact, parser,
    consumer, drift outcome, and test for every value. The reachable config-read
    set and classification ledger must be equal.
13. **Set-equality certificate.** List the mechanically extracted sets for
    (a) implementation tasks, (b) new/changed public callables, (c) durable
    fields and writers/readers, (d) S3 keys, (e) queue message producers and
    consumers, (f) external call sites, and (g) runtime configuration reads.
    For each set, prove every member has exactly one applicable decision-audit
    task, proof-ledger row, mechanical trace, and decisive assertion. Extra
    undocumented source members and planned members with no source/test owner
    both fail the gate.
14. **Durable global-work ownership closure.** For every work/dedup/cache row
    shared across runs, enumerate every claim, reclaim, completion, failure,
    cancellation, and legacy caller. If ownership crosses a Run-lease release
    or stage transition, persist the true task/resource owner and require every
    old and new claim path to honor it. Prove terminal-state behavior,
    same-run/different-run races, local-versus-distributed races, and the final
    settlement writer. A new owner field checked only by the new worker fails
    readiness.
15. **Retry-input reconstructability.** For every permitted retry of a retained
    adapter, start only from durable pre-call evidence and construct every
    required adapter input. Persist prerequisite evidence such as accepted
    preflight output, account/project identity, request ID, and dispatch time
    when the adapter requires it. A plan that says “retry the same call” while
    requiring an unstored argument fails readiness.

The proof packet must use code-like signatures and formulas where applicable.
Section references and prose summaries may explain a choice but cannot replace
these ledgers. The planning-readiness boxes remain unchecked until every ledger
has been mechanically traced and its referenced symbol has been inspected.
The parent must include the seven set inventories and their equality result in
the active checklist; a sentence asserting completeness is not the certificate.

## 10. Planning Readiness Gate

The parent must review the checklist before assigning the first implementation
window. Do not begin until all applicable answers are yes:

- Is there one authoritative, contradiction-free contract?
- Can a fresh agent work without conversation history?
- Are all high-risk external contracts proven rather than guessed?
- Are complete lifecycles and transaction boundaries defined?
- Are concurrency, idempotency, fencing, and recovery defined?
- Does every invariant have an owning window?
- Are dependencies and file ownership explicit?
- Is every acceptance criterion deterministically verifiable?
- Are partial failure, concurrency, and restart cases assigned?
- Are live/user prerequisites separated from local deterministic acceptance?
- Does every window pass the Section 9 decision audit and mechanical trace?
- Are all dependencies, filenames, symbols, interfaces, data definitions,
  ordered durable operations, bounds, and test assertions fixed by the parent?
- Can the implementation agent finish without selecting among two materially
  different contract-compliant designs?
- Does the external-call inventory exactly equal the ambiguity ledger and its
  failure-injection tests?
- Does every reachable runtime configuration read have one durable-snapshot or
  credential-validation classification and drift test?
- Do all seven proof-packet set inventories have exact task/ledger/trace/test
  coverage with no extra or missing member?
- Does every cross-run global-work owner remain fenced across lease release,
  stage completion, legacy callers, and final settlement?
- Can every permitted retry reconstruct all adapter inputs from durable evidence
  without repeating a forbidden prerequisite call?
- Could every box be checked while an end-to-end invariant still fails?

If the last answer is yes, revise the plan.

## 11. Subagent Execution Rules

Assign windows sequentially when later work consumes earlier contracts,
migrations, schemas, fixtures, or shared state machinery. Parallelize only
independent read-only discovery, non-overlapping tests, or clearly disjoint
implementation ownership.

When the user authorizes a continuous sequence, assign the whole named sequence
to one implementation agent. Do not turn routine window boundaries into parent
or user scheduling gates. The assignment must say:

```text
Execute Windows <FIRST> through <LAST> sequentially.
For each window, verify its dependencies before editing, stay inside its
ownership boundary, implement the locked specification, run every required
test, and complete its evidence record.
If that window passes, mark its implementation acceptance and immediately
continue to the next window without requesting parent verification,
reassignment, scheduling, or user input.
If a check fails, diagnose and correct it inside the active window when the
locked specification determines the fix. Stop only for one concrete blocker:
an authoritative contradiction or missing implementation decision; absent
required sanitized external evidence; unavailable required isolated database,
permission, secret, approval, or live prerequisite; or a required action that
would cross an authorization/ownership boundary.
Do not continue past a genuine blocker. Do not begin any window after <LAST>.
```

Checked boxes require executed evidence, not intent or source inspection alone.
Independent parent reliability review occurs once after the authorized sequence,
not between its windows. A completed handoff, passing test suite, or dependency
boundary is never itself a blocker.

## 12. Parent Reliability Review

After all implementation windows, the parent must independently:

- inspect the complete diff and current source,
- compare behavior with the locked contract and exclusions,
- trace every end-to-end lifecycle and durable failure point,
- review transaction, concurrency, lease, fence, retry, and recovery behavior,
- search for fallback probing, permissive parsing, unsafe casts, duplicate
  authority, raw-payload leakage, and parked functionality,
- inspect test quality and confirm mocks do not bypass the claimed behavior,
- rerun focused and risk-proportionate full verification,
- review migrations and preserved live data safely, and
- record unavailable live checks as gaps rather than replacing them with
  synthetic evidence.

The reviewer should reproduce failures before prescribing corrections whenever
practical.

## 13. Corrective Windows And Completion

Do not rewrite completed windows or silently fix findings during independent
review. Open append-only corrective windows.

Each corrective window must name:

- the finding and severity,
- violated contract or invariant,
- exact reproduction,
- root cause and owning files,
- bounded fix,
- required regression test,
- migration implications,
- dependencies, and
- stop condition.

Group findings only when they share one root cause and implementation boundary.
After corrections, rerun their focused tests, the original affected-window
tests unchanged, the relevant full regression corpus, and the parent review.

The parent may mark the plan complete only when:

- implementation and corrective windows are complete,
- acceptance claims have appropriate evidence,
- migrations and preserved data are safe,
- no external contract is guessed,
- no fallback probing remains,
- no unresolved finding contradicts a locked invariant, and
- deployment or live claims are limited to what was actually verified.

## Lean-Plan Rule

Use only the sections and checks relevant to the task, but never remove
source-of-truth control, evidence classification, lifecycle reasoning,
ownership, acceptance, handoff, or independent review.

Small work may fit one implementation window plus review. High-risk provider,
data, concurrency, migration, or authorization work should be split until each
window has one clear invariant and decisive verification.
