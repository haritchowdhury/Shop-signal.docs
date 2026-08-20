# Project-Agnostic Decision-Complete and Enforcement-Complete Checklist Authoring Standard

## 0. Status, scope, and conformance

This standard defines how a parent planner converts product-level requirements
and current-system evidence into implementation windows that another agent can
execute without inventing behavior.

It is project-agnostic. Project technologies, architectures, payloads, limits,
and historical practices are inputs to the process; none are defaults supplied
by this standard.

The key words `MUST`, `MUST NOT`, `REQUIRED`, `SHALL`, `SHALL NOT`, `SHOULD`,
and `MAY` are normative.

A checklist conforms only when:

1. every required artifact in Section 2 exists;
2. every applicable authoring checkbox is physically present and checked;
3. every checked box cites resolvable evidence IDs;
4. every requirement has a complete mechanical trace;
5. no payload, external contract, identity, failure outcome, or durable formula
   is guessed;
6. no implementation-affecting choice remains for an implementation agent;
7. every window has an enforceable assignment boundary;
8. every applicable window is enforcement-complete; and
9. the independent falsification audit passes.

Prose claiming that these conditions are satisfied is not conformance.

### 0.1 Governing principle

The parent acts as a compiler:

```text
product intent + observed system + authorized evidence
-> classified facts and unknowns
-> locked decisions and lifecycle models
-> risk-derived scenarios
-> bounded implementation windows
-> executable coverage cases, checkboxes and acceptance oracles
```

If any transformation is incomplete, the output is `DRAFT / NOT ASSIGNABLE`.

### 0.1.1 Decision completeness and enforcement completeness

`Decision-complete` means the implementation agent has no material behavior,
interface, dependency, persistence, failure, recovery, ownership, cost,
configuration, compatibility or acceptance choice left to make.

`Enforcement-complete` means the implementation cannot omit, bypass, weaken or
misclassify prescribed behavior while still satisfying the window's acceptance
gate. Every required behavioral partition has a stable coverage-case ID, an
executable oracle, an activation witness and a mechanically verified mapping to
an executed test registration. A passing command, aggregate test count or prose
summary is not enforcement evidence.

Enforcement closure is REQUIRED for a window that changes or establishes any
user-visible result, durable transition, external operation, asynchronous or
retry behavior, authorization or ownership rule, concurrency or time-bounded
lease, parser or boundary contract, artifact, build/runtime/deployment behavior,
or compatibility behavior. `N/A` is allowed only with evidence that none of
those concerns is reachable.

Enforcement completeness does not require exhaustive testing of combinations
that cannot change behavior. It requires the combination strategy and every
excluded combination to satisfy Phase E.

### 0.2 Priority order

When requirements compete, apply this order:

1. no guessed payload or contract;
2. no delegated implementation-affecting decision;
3. safety, authority, privacy, and durable correctness;
4. representative behavioral proof;
5. bounded cost, scale, and operational behavior;
6. execution efficiency and window ergonomics.

### 0.3 Non-normative material

Architecture examples and historical case studies SHALL NOT appear in the
normative sections of this standard. Blank schemas and abstract templates are
normative formats, not implementation examples.

If a separate case-study document exists:

- reading it is optional;
- it cannot establish a project fact;
- its technologies, shapes, thresholds, and remedies cannot be copied without
  current-project evidence; and
- the parent must derive the current design independently.

### 0.4 Standard revision and adoption

The canonical standard revision is the SHA-256 of this file. Every newly
assigned, reassigned, reopened, corrective or successor window MUST pin the
canonical standard path and revision in `A5` and in its readiness evidence.

Updating this standard does not silently rewrite an already `READY` or
`IN_PROGRESS` assignment. An assignment created before standard pinning may
finish only its currently authorized window under its frozen contract,
decision ledger, checklist and state. Before any later window is assigned, the
parent MUST apply the new standard, record a delta audit, add the standard pin
and resolve every newly applicable requirement. A status transition or adjacent
dependency is not an exemption.

## 1. Roles and authority

### 1.1 Requester

The requester owns product intent and approvals for actions outside the already
authorized boundary. The parent SHALL surface only concrete required decisions,
prerequisites, approvals, and deliberately delayed gates.

### 1.2 Parent planner

The parent owns:

- repository and runtime discovery;
- evidence acquisition within authorization;
- product interpretation and exclusions;
- all implementation-affecting decisions;
- payload and boundary contracts;
- identities, authority, ownership, and visibility;
- schemas, persistence, transactions, and recovery;
- external-operation economics, ambiguity, and retry rules;
- configuration, platform, build, deployment, and capacity decisions;
- lifecycle and state-machine definitions;
- scenario derivation, coverage-case compilation and acceptance oracles;
- window dependencies, ownership, sizing, and assignments;
- checklist, evidence, active-state, and changelog integrity; and
- independent verification and completion.

The parent MUST inspect primary evidence itself. Subagent summaries are
navigation aids, never proof.

### 1.3 Implementation agent

An implementation agent owns only the assignment recorded in the active state.
It MAY choose formatting, local names, and private decomposition only when that
choice cannot change a locked interface, dependency, behavior, durable state,
failure outcome, cost, authority, or acceptance result.

It MUST NOT:

- invent or select a missing contract;
- broaden its write or action scope;
- begin, prepare, partially implement, or pre-empt a successor window;
- change the product contract or active assignment;
- treat passing commands as behavioral proof without named assertions; or
- mark the overall project complete.

### 1.4 Parent executor and reviewer

The parent MAY orchestrate successive implementation agents without requester
intervention when authorization permits. Each subagent still stops at its own
assignment boundary. The parent verifies the handoff and assigns the next
window.

The final reviewer MUST inspect current source and evidence independently. A
review cannot consist of accepting implementation summaries.

## 2. Required authoring package

The parent MUST create or identify these eight distinct artifacts. Combining
their authorities in one narrative file is nonconforming.

| ID | Artifact | Sole authority |
|---|---|---|
| `A1` | Locked product contract | Required behavior, invariants, exclusions, compatibility and authorization |
| `A2` | Discovery dossier | Observed sources, probes, inventories, unknowns and environmental facts |
| `A3` | Decision ledger | Every implementation-affecting choice and deterministic derivation |
| `A4` | Checkbox execution checklist | Ordered windows, tasks, tests and acceptance criteria |
| `A5` | Active execution state | Current assignment, authorized actions and stop point |
| `A6` | Append-only evidence log | Proof of authoring, execution and verification claims |
| `A7` | Append-only specification changelog | Revisions, causes, impact and invalidation |
| `A8` | Traceability index | Requirement-to-evidence-to-decision-to-task-to-test closure |

Each artifact MUST name the paths of the other seven without duplicating their
authority.

### 2.1 Locked product contract (`A1`)

It MUST contain:

- stable requirement and invariant IDs;
- included behavior and explicit exclusions;
- user-visible outcomes and truthful intermediate states;
- trusted identities and authorization policy;
- retention, deletion, historical-compatibility and migration policy;
- supported external systems and deliberately unsupported variants;
- required nonfunctional behavior and limits;
- deployment/live boundary; and
- terms whose operational meaning could otherwise be ambiguous.

It MUST NOT contain live execution status or accumulated evidence.

### 2.2 Discovery dossier (`A2`)

Every entry MUST contain:

```yaml
evidence_id: SRC-0001
classification: OBSERVED | UNKNOWN_BLOCKING | DEFERRED_GATE | PARKED
claim: precise single claim
source: exact file/symbol, command, sanitized fixture, runtime probe, or authority
observed_at: timestamp or source revision
environment: relevant environment identity
limitations: explicit limitations
privacy: redaction/sanitization statement
```

`INFERRED` MAY appear in working notes but MUST NOT enter `A1`, `A3`, or `A4`.

### 2.3 Decision ledger (`A3`)

Every decision MUST contain:

```yaml
decision_id: DEC-0001
requirement_ids: [REQ-0001]
locked_choice: one exact choice
evidence_ids: [SRC-0001]
alternatives_rejected: complete materially different alternatives
reason: concise reason
consequences: exact interface, persistence, failure, cost, or operational effects
derived_values: exact formulas, inputs, normalization and edge behavior
implementing_tasks: [W1-T1]
verification_scenarios: [SCN-0001]
```

Two materially different implementations remaining possible means the decision
is not locked.

### 2.4 Checkbox execution checklist (`A4`)

The checklist MUST contain actual Markdown checkboxes for:

- authoring readiness;
- every implementation task;
- every window verification obligation;
- every window handoff obligation; and
- final independent review.

For every window requiring enforcement closure, `A4` MUST also contain or
resolve to the complete behavioral coverage matrix required by Section E6. A
fixture reference without the literal expected members, derivation and digest
in an authoritative artifact is not closure.

A checked authoring or acceptance box MUST cite evidence IDs on the same line or
immediately below it. A checkbox is not satisfied by intention.

### 2.5 Active execution state (`A5`)

The state MUST contain one machine-scannable block and no history:

```yaml
state_version: 1
standard_path: path
standard_revision: sha256
contract_path: path
contract_revision: sha256
decision_path: path
decision_revision: sha256
checklist_path: path
checklist_revision: sha256
current_window: W1
current_assignment_id: ASG-0001
assigned_agent: explicit identity or UNASSIGNED
authorized_windows: [W1]
authorized_write_scope: [exact paths or symbols]
authorized_actions: [exact actions]
prohibited_actions: [exact actions]
execution_environment_policy:
  sandbox_escalation_for_authorized_local_actions: true
  automatic_identical_recovery_after_proven_environment_invalidation: true
  recovery_limit_per_invalidated_execution: 1
  external_authority_expansion: false
may_start_successor: false
current_status: READY | IN_PROGRESS | AWAITING_REVIEW | BLOCKED | COMPLETE
accepted_through: NONE
next_window: W2 | STOP
stop_after: W1
blocker: null
user_gates: []
last_updated: ISO-8601
```

Default assignment scope is one window. `may_start_successor` defaults to
`false`. A multi-window assignment is valid only when every authorized window
is explicitly listed and none is reserved for another agent.

### 2.6 Append-only evidence log (`A6`)

Every entry MUST identify:

- evidence ID and timestamp;
- authoring, implementation, or review phase;
- claim being proven;
- environment and revision;
- exact operation or command;
- observed result and decisive assertion;
- sandbox privilege used, any environment-invalidated attempt, its read-only
  postcondition proof, and the identical recovery outcome;
- artifacts or sanitized output location;
- negative-control result when required;
- required, registered, executed, skipped, duplicate and unexpected coverage
  case counts plus the coverage-set digest when enforcement closure applies;
- limitations, skipped checks, and reason; and
- external mutations, costs, or confirmation that none occurred.

Evidence cannot authorize work or alter a contract.

### 2.7 Specification changelog (`A7`)

Every revision MUST append:

```yaml
change_id: CHG-0001
timestamp: ISO-8601
trigger_evidence: [EV-0001]
reason: concrete contradiction, decision, or requirement change
old_revision: sha256
new_revision: sha256
changed_requirements: []
changed_decisions: []
affected_windows: []
invalidated_evidence: []
compatibility_or_migration_effect: exact effect
authorization_effect: exact effect
resumption_state: exact active-state transition
```

Never silently rewrite an assigned or completed specification. Never reuse a
window, task, decision, scenario, evidence, or change ID.

### 2.8 Traceability index (`A8`)

For every requirement and invariant:

```text
requirement
-> observed evidence
-> locked decision
-> implementing task
-> verification scenario and coverage cases
-> executable registrations, activation witnesses and oracles
-> execution evidence
-> final-review assertion
```

Every arrow MUST resolve to a stable ID. Extra or missing members fail
readiness.

## 3. Fact classification and no-guessing rule

### 3.1 Allowed classifications

Every material fact SHALL be classified as:

- `OBSERVED`: directly established by current primary evidence;
- `DECIDED`: chosen by the parent within product authority;
- `DERIVED`: mechanically produced by a written deterministic formula;
- `UNKNOWN_BLOCKING`: unsafe to specify or implement without evidence;
- `DEFERRED_GATE`: knowable only after a named earlier output, with every branch
  already prescribed; or
- `PARKED`: outside the authorized result.

An `UNKNOWN_BLOCKING` fact cannot be converted to `DECIDED` when the fact is an
external reality rather than a product choice.

### 3.2 Payload scope

For this standard, `payload` includes any structured or unstructured data
crossing a boundary, including:

- request, response, error, callback and webhook bodies;
- event, message, job and command inputs;
- database rows and query results consumed across modules;
- files, artifacts, manifests and metadata;
- SDK and CLI results;
- browser, UI and server contracts; and
- imported historical records.

### 3.3 Payload evidence certificate

Every consumed or produced payload MUST have a ledger row containing:

| Field | Required content |
|---|---|
| Payload ID | Stable ID and boundary name |
| Provenance | Exact observed source and revision/version |
| Sanitized evidence | Fixture or controlled observation with secrets/private data removed |
| Producer | Exact source and symbol/system |
| Consumer | Exact source and symbol/system |
| Version/discriminator | Exact rule; absence is explicit |
| Parser | Exact strict parser and normalized output type |
| Consumed fields | Exact paths, types, required/optional/null rules and bounds |
| Produced fields | Exact paths, types and derivation formulas |
| Unknown-field policy | Reject or ignore without behavioral effect |
| Error mapping | Exact safe typed outcomes |
| Privacy policy | Fields forbidden from storage, fixtures, logs and telemetry |
| Tests | Positive, missing, malformed, boundary and unknown-field fixtures |

### 3.4 Absolute prohibitions

The parent and implementation agent MUST NOT:

- invent a field, envelope, alias, discriminator, error, metadata value or
  optionality rule;
- probe alternate shapes until one parses;
- use fallback field paths or credential branches;
- generalize one observation into undocumented variants;
- use a project example as payload evidence;
- replace missing evidence with a permissive parser, cast, optional chain or
  synthetic fixture;
- retain raw secret-bearing or unnecessarily private payloads; or
- claim compatibility with an unobserved version.

Multiple payload variants are supported only as a documented discriminated
union with separate evidence and tests for each variant.

### 3.5 Unknown payload outcome

If an implementation consumes an unobserved material payload field:

1. classify it `UNKNOWN_BLOCKING`;
2. identify the narrowest authorized evidence-acquisition action;
3. obtain sanitized evidence if authorized;
4. otherwise report one concrete prerequisite;
5. keep all affected implementation windows `DRAFT / NOT ASSIGNABLE`.

An evidence probe is not implementation acceptance.

## 4. Authoring lifecycle

The parent MUST execute Phases A through H in order. A failed gate returns to
the earliest affected phase.

### Phase A — Authority and execution policy

Record:

- governing instructions and authority order;
- authoritative product inputs and superseded material;
- current working-tree and repository boundaries;
- authorized actions and prohibited actions;
- paid, mutating, destructive, secret-bearing and production gates;
- sandbox/execution-environment privilege policy for already-authorized local
  actions, including automatic identical-recovery conditions;
- execution mode and agent-assignment policy;
- planned requester stop points; and
- exact blocker definition.

Do not infer cloud, provider, production, deployment, deletion, or payment
authority from permission to plan or edit local source.

### Phase B — Source-grounded discovery

Inventory applicable members of all these sets:

1. product entry points and user-visible outputs;
2. complete reachable caller/callee graph;
3. cross-module interfaces and payload boundaries;
4. durable models, fields, migrations, constraints, indexes, readers and writers;
5. identities, authorization checks, ownership claims and visibility gates;
6. external operations, callbacks and rate/cost limits;
7. asynchronous delivery, retries, deduplication and terminalization;
8. locks, leases, fencing, compare-and-swap and competing owners;
9. configuration, secrets, clocks, randomness and environment reads;
10. build, package, generated, native and runtime dependency closure;
11. infrastructure, target environment, permissions, quotas and service limits;
12. tests, fixtures, simulators, mocks and their bypasses;
13. monitoring, repair, cancellation and stale-process paths;
14. presentation/control-plane creation, update and status paths;
15. historical formats and explicit compatibility policy; and
16. scale-sensitive loops, queries, transactions and external calls.

Discovery MUST inspect the current working tree, not only a commit. Claimed
absence requires recorded negative searches. Every discovered member gets one
stable evidence ID.

### Phase C — Lifecycle and state closure

For every workflow state and transition, record:

1. actor and entry condition;
2. trusted identity and authorization predicate;
3. strict input parser and bounds;
4. durable precondition and ownership predicate;
5. external operation and call cardinality;
6. durable pre-call evidence;
7. ordered writes and transaction boundaries;
8. emitted payload/artifact and validation;
9. idempotency and deduplication identity;
10. concurrency unit and every competing actor;
11. claim, renewal, expiry, loss and fencing behavior;
12. failure before and after every external or durable boundary;
13. duplicate, reorder, retry, restart and stale-process behavior;
14. cancellation and supersession behavior;
15. terminal state and terminal evidence;
16. public visibility boundary; and
17. telemetry, privacy and retention.

Every transition MUST be represented in a table with precondition, atomic
predicate, writes, emitted action, replay result and forbidden transitions.

### Phase D — Cross-cutting decision ledgers

Create every applicable ledger below. `N/A` requires evidence proving the
concern is unreachable.

#### D1. Interface ledger

Record complete signatures, argument order, defaults, return unions, safe
errors, callers, implementations and consumer assertions.

#### D2. Persistence and atomicity ledger

Record every durable field, type, default, constraint, index, writer, reader,
visibility, retention, migration direction, data-preservation and rollback rule.
Classify each multi-write sequence as:

- `SAME_ATOMIC_BOUNDARY`, naming composable primitives and rollback proof; or
- `RECOVERED_BOUNDARY`, naming pre/post evidence, retry action and ambiguity.

#### D2A. Storage transport and test-isolation ledger

For every migration, schema change, destructive probe, integration test and
runtime storage client, record:

- exact storage/account/database identity and proof it is not production;
- administration/migration transport versus runtime transport;
- namespace, schema, partition or equivalent isolation mechanism;
- configuration precedence and the component interpreting each option;
- server/storage-side assertion of the selected isolation boundary;
- location and isolation of migration/history metadata;
- session, pool, cache and connection-reuse behavior;
- collision-free concurrent-test policy;
- exact cleanup target and `finally` behavior; and
- fail-closed behavior for identity, namespace, transport or cleanup mismatch.

Tests MUST verify isolation before behavioral writes. They MUST NOT obtain
isolation by deleting or rewriting shared or production-capable state.

#### D3. Identity and authority ledger

Separately enumerate user, tenant, run/process, task/work, resource, cache,
deduplication, external-call and publication identities. Record cardinality
between every pair and forbid accidental substitution of one identity for
another.

#### D4. Ownership and concurrency ledger

For every mutable/shared resource, record all claimers, renewers, reclaimers,
completers, cancellers, finalizers and legacy callers. Produce a pairwise
competing-owner matrix. Every pair that can overlap MUST have an atomic
mutual-exclusion, fencing or commutativity proof.

When time-bounded ownership exists, also record acquisition, renewal function,
renewal interval, injected clock/timer seam, expiry/loss transition, fence
predicate, ownership validation surrounding external and durable operations,
and a test that advances beyond one full ownership duration.

#### D5. Payload and artifact ledger

Apply Section 3 to every boundary. For durable artifacts also record key/name
grammar, item identity, input/content fingerprint formulas, durable timestamp
source, missing/corrupt/conflict/already-valid behavior and replay construction.

#### D6. External-operation ledger

For every network, SDK, subprocess, database, browser, paid, rate-limited or
mutating call, record:

- exact caller and adapter;
- authorization, cost and mutation class;
- request identity and provider-supported idempotency;
- batch/cardinality identity and ceiling;
- timeout and retry ownership at every layer;
- concurrency and rate limit;
- durable pre-call and post-call evidence;
- strict response and error parsing;
- crash-before-call, response-loss and crash-after-response behavior;
- whether a repeat call is allowed; and
- ambiguity state when exactly-once execution cannot be proven.

#### D7. Configuration ledger

Inventory every reachable environment, configuration, secret, clock, random,
feature, account and version read. Record source, durability, fingerprint,
consumer, drift behavior and validation. Replay-affecting non-secret behavior
MUST be durably snapshotted when later environment drift could change results.

#### D8. Control-plane and presentation ledger

Trace every creation, confirmation, start, status, cancellation, repair and
public-result path from its entry point to durable state and presentation.
Record configuration written by each path, status mapping, sort/order formulas,
process-version assumptions and stale-process behavior.

#### D9. Build, runtime and deployment ledger

For every deployable unit record source entry point, final module/runtime,
complete planned dependency closure, generated/native assets, build tool and
flags, target platform, inventory, size/resource bounds, startup/invocation
probe and delivery mechanism.

Determine deployment closure from emitted-artifact differences or equivalent
build evidence, not assumed call reachability.

A placeholder, no-op or incomplete entry point proves only build scaffolding.
Label it `PROVISIONAL`; it cannot certify final dependency compatibility,
startup, size, runtime resources or invocation. Before readiness, build and
invoke either the real production dependency closure or a disposable
representative closure containing every already-decided runtime dependency,
generated asset and native component. Repeat emitted-artifact validation when a
later window first adds a material dependency.

#### D10. Environment capability ledger

Measure or authoritatively establish permissions, quotas, platform restrictions,
transport limits, service constraints, regions/endpoints and account-specific
applied limits before locking a design that depends on them. Distinguish
published defaults from actually applied values.

Unknown capabilities become declared gates, never optimistic assumptions.

#### D11. Scale and complexity ledger

For each workload dimension, record minimum, representative, expected maximum
and hard maximum. At each bound record:

- database statements and rows touched;
- sequential critical-path operations;
- external calls and batches;
- durable object reads/writes;
- messages/jobs;
- transaction duration and lock scope;
- memory, package, payload and response size; and
- configured concurrency and backpressure.

State expected asymptotic growth and explicit ceilings. A timeout, memory or
capacity increase MUST NOT substitute for identifying and testing the causal
operation growth.

#### D12. Compatibility and lifecycle-policy ledger

Record whether historical formats, mixed versions, partially migrated data and
old processes are supported, rejected, migrated or deleted. A new project MUST
not inherit compatibility work without an explicit product requirement.

#### D13. Observability and privacy ledger

Record safe logs, metrics, traces, correlation identities, redaction, retention
and the observations required to distinguish waiting, retrying, stalled,
terminal and publicly visible states.

### Phase E — Scenario synthesis

Derive test dimensions from `A1` through `A3`; do not begin with a stock list of
examples. Classify each applicable dimension:

- input/payload partitions and boundaries;
- initial durable-state partitions;
- identity/cardinality relationships;
- external outcomes and ambiguity;
- delivery order, duplication and delay;
- ownership and concurrency schedules;
- failure positions;
- retry/restart/stale-process positions;
- cancellation and supersession;
- visibility and authorization;
- compatibility/version states;
- workload and resource bounds; and
- runtime/environment parity levels.

The scenario ledger MUST state whether combinations receive exhaustive,
pairwise, model-generated, randomized or deliberately excluded coverage.
Exclusions require a proof that the combination cannot affect behavior.

Every scenario MUST contain:

```yaml
scenario_id: SCN-0001
requirements: []
decisions: []
preconditions: exact durable and environmental state
inputs: evidence-backed payload fixtures and identities
actions: ordered operations and injected failures/schedule
activation_witnesses: execution units and boundaries that must be reached
oracle: exact durable, external, visible and forbidden outcomes
call_and_operation_counts: exact or bounded counts
negative_control: required behavior deliberately disabled or corrupted
parity_class: unit | component | integration | local_e2e | emitted_artifact | live_preflight | production_canary
cleanup: exact safe cleanup
```

#### E1. Anti-vacuity certificate

An integration or end-to-end claim is invalid unless evidence proves:

- representative nonempty work entered every claimed execution unit;
- required external and durable boundaries were reached;
- expected cardinalities and terminal states were observed;
- prohibited shortcut paths were absent;
- final output was derived from the exercised path; and
- every critical invariant exercised by the claim has a named negative control
  that makes the applicable oracle fail when that invariant is removed,
  bypassed or corrupted.

Zero-work scenarios remain necessary edge cases but cannot certify a nonempty
workflow.

For negative-control purposes, a `critical invariant` is any prescribed rule
whose violation can change authority or ownership, a durable or publicly
visible result, external-call/cost cardinality, retry/ambiguity classification,
atomicity or fencing, boundary parsing, artifact validity/order, dispatch, or
emitted runtime behavior. The parent MUST enumerate them; it cannot classify an
applicable member away merely because a positive test exists.

#### E2. Failure-boundary coverage

Inject failure before and after every non-atomic durable boundary and every
external operation. Assert exact retry, ambiguity, duplication, ownership and
visibility outcomes. A category name without a named boundary is insufficient.

#### E3. State-machine and generated testing

When concurrency, retry, asynchronous delivery, shared identity, partial
failure or combinatorial state exists, define:

- allowed model states and transitions;
- invariants checked after every generated action;
- generators constrained by observed contracts;
- deterministic seeds and replay commands;
- failure minimization/shrinking;
- trial/time budget and coverage counters; and
- promotion of each discovered failure to a permanent deterministic regression.

Random generation MUST NOT generate or legitimize unobserved payload shapes.
It may vary only evidence-backed values and modeled event schedules.

#### E4. Scale and performance proof

Tests MUST cover representative and required maximum cardinalities from D11.
Acceptance asserts operation counts, concurrency bounds and duration/resource
budgets, not only successful completion.

#### E5. Parity rules

Evidence proves only its declared parity class. Source tests do not prove an
emitted artifact; a simulated permission failure does not prove live
authorization semantics; published platform limits do not prove applied
account limits; a local end-to-end test does not prove production deployment.

#### E6. Behavioral coverage matrix and executable case closure

For every window requiring enforcement closure, derive coverage cases from the
Cartesian dimensions that can change behavior:

```text
reachable production paths
x applicable durable-state and identity partitions
x applicable input and external outcomes
x applicable ownership, retry, restart and failure schedules
```

The parent MUST reduce this set using the combination strategy declared under
Phase E. Every removed member requires an equivalence or unreachability proof.
Risk alone does not justify an undocumented omission.

Each retained member MUST have one stable, globally unique coverage-case ID and
this complete row:

```yaml
case_id: CASE-0001
scenario_id: SCN-0001
requirement_ids: []
decision_ids: []
production_path: exact entry point and required boundaries
state_partition: exact starting durable/ownership state
input_or_external_outcome: exact evidence-backed partition
actions: ordered actions, clock and injected schedule
activation_witness: runtime observation proving the intended path ran
expected_result: exact return, durable, visible and emitted result
expected_operations: exact or bounded operation sequence and counts
forbidden_operations: exact operations or visibility that must remain absent
negative_control_id: NC-0001 | N/A-with-evidence
parity_class: unit | component | integration | local_e2e | emitted_artifact | live_preflight | production_canary
test_registration: exact planned test anchor and runtime registration mechanism
```

The matrix MAY be represented as a table, a machine-readable fixture or code,
but the authoritative expected members, derivation and deterministic digest
MUST be resolvable before assignment. The standard does not prescribe a file
format, programming language, runner or case count.

Coverage-case IDs MUST match `[A-Z][A-Z0-9]*(?:[-_.:][A-Z0-9]+)+`. First fail
if an input contains a duplicate ID. Compute a case-set digest by sorting the
distinct IDs in ascending unsigned UTF-8 byte order, concatenating each UTF-8
ID followed by one LF byte, and encoding the SHA-256 result as lowercase
hexadecimal. The required, registered and executed sets each use this formula;
a declared count or stored digest is never trusted without recomputation from
the exact members.

The implementation acceptance mechanism MUST collect the IDs that actually
execute and assert exact set equality:

```text
required case IDs = registered case IDs = executed case IDs
```

Required cases have zero skips. Duplicate, missing, unexpected,
executed-without-activation and selected-but-filtered-out cases fail acceptance.
Group counts and the deterministic digest of the globally sorted case-ID set
MUST be independently recomputed rather than trusted from a reported total.

A test name containing a case ID is neither registration nor execution
evidence. The registered set comes from an executable registry enumeration that
does not infer IDs from names. The executed set records an ID only after that
case's activation witness and oracle have executed successfully.

#### E7. Test-substitute fidelity

For every mock, fake, stub, simulator, in-memory repository, clock, queue,
storage boundary, transport or external-operation substitute used to support a
behavioral claim, record:

```yaml
production_boundary: exact real boundary
test_substitute: exact test symbol
contract_fields: inputs, outputs, defaults and return unions reproduced
operation_order: reproduced call and durable ordering
failure_modes: reproduced failures and ambiguity
time_and_concurrency: reproduced clock, lease, retry and ownership behavior
fidelity_proof: conformance test or higher-parity witness
known_differences: exact differences
claims_not_supported: claims the substitute cannot prove
```

A substitute cannot support a production-path claim beyond its proved fidelity.
Where a difference can affect the claimed result, repeat that case at a parity
class containing the real boundary or narrow the claim.

#### E8. Risk-proportionate frozen gates

Before assignment, the parent MUST prescribe the smallest final gate set that
proves the window at the necessary parity classes. It MUST identify:

- the exact commands or runner selections;
- which coverage groups each command executes;
- required zero-skip and case-set results;
- the final source, test, fixture and generated/build inputs that are frozen for
  the gate;
- which diagnostics may run during editing;
- which stateful, costly, destructive or broad suites may run, how often and in
  what isolated environment; and
- which edit or environmental invalidation requires a gate to be rerun.

Broad integration, build, migration or live suites are not default obligations
for every window. Verification depth follows the changed risk and parity claim.
Diagnostic runs do not become handoff evidence unless they ran against the
frozen final inputs. A failed gate followed by a relevant edit requires a new
frozen gate; unchanged successful stateful gates MUST NOT be repeated merely to
accumulate evidence.

#### E8.1 Sandbox privilege and environment-invalidated executions

Sandbox escalation is an execution-environment privilege, not independent task
authority. A parent MUST authorize it by default for every otherwise-authorized
local command that may require additional local-process, localhost, headless-
browser, build-filesystem, toolchain, or isolated-test-service access.

An authorized local command MAY begin escalated. Merely requesting or using
that privilege MUST NOT require a requester gate, corrective window, parent
reassignment, new command, or expanded action scope.

When a restricted attempt is proven to have failed or become unobservable
solely because of sandbox denial or execution-channel loss, the same assigned
agent MUST be allowed one automatic recovery without returning to its parent.
The recovery MUST:

1. execute the identical command, arguments, selection, environment and
   behavioral oracle;
2. use only the escalation necessary for the already-authorized local action;
3. begin only after read-only postconditions prove that no matching process,
   workspace mutation, external mutation, paid operation or usable acceptance
   result remains from the invalidated attempt;
4. preserve the invalidated attempt as diagnostic history;
5. retain and report the recovery's final exit and complete decisive output;
   and
6. occur at most once for that invalidated execution unless a different,
   independently proven environmental invalidation occurs.

The invalidated attempt does not consume the one accepted frozen-gate
execution. An observable assertion failure, nonzero product/test result,
partial success with material side effects, changed input, resource exhaustion
caused by the implementation, or unexplained termination is not a sandbox
invalidation and MUST NOT use this rule.

Sandbox escalation never grants provider, paid, cloud, production, secret-
installation, destructive, deployment, commit, push or successor authority.
Those actions retain their explicit approval gates.

### Phase F — Compile execution windows

Build a dependency DAG. Each window establishes one coherent capability or
invariant and leaves deterministic evidence. Split unrelated ownership,
independently risky transitions and unbounded context.

Every window MUST contain the following exact sections.

#### F1. Window header

```yaml
window_id: W1
objective: one observable capability
depends_on: []
consumes: exact prior outputs
produces: exact outputs and guarantees
assigned_agent_policy: one_window | explicit_multi_window
authorized_write_scope: exact files and symbols
shared_file_scope: exact symbols and reason
read_only_scope: exact dependencies
authorized_actions: []
prohibited_actions: []
successor: W2 | STOP
successor_reserved_for: parent | named assignment | none
may_start_successor: false
```

Wildcard ownership without symbol/task mapping is prohibited. File overlap
between windows requires exact symbol ownership and dependency ordering.

#### F2. Preconditions

Use actual checkboxes:

```markdown
- [ ] W1-P1 Active assignment ID and pinned standard/contract/decision/checklist revisions match. Evidence: ___
- [ ] W1-P2 Required predecessor outputs exist and validate. Evidence: ___
- [ ] W1-P3 Required environment/permission/data prerequisites exist. Evidence: ___
- [ ] W1-P4 Starting dirty-worktree and ownership scope are recorded. Evidence: ___
```

#### F3. Task block

Every task MUST specify:

1. task ID;
2. requirement and decision IDs;
3. exact source anchor;
4. exact target anchor;
5. complete interface/schema;
6. exact ordered algorithm;
7. durable and external operation order;
8. transaction or recovered-boundary classification;
9. identity, key, fingerprint and timestamp formulas;
10. failure, retry, duplicate, concurrency, restart and cancellation behavior;
11. fixed dependencies, configuration, bounds, timeouts, batching and limits;
12. every caller and obsolete behavior to change/remove/preserve;
13. exact tests, coverage-case IDs, registrations, setup, actions, activation
    witnesses, assertions and negative controls;
14. output consumed by another task/window; and
15. non-goals and forbidden edits.

Each task is an unchecked box before implementation:

```markdown
- [ ] W1-T1 Perform the fully specified change in task block W1-T1.
```

Broad verbs do not satisfy a task unless all fifteen fields make execution
mechanical. `Choose`, `determine`, `as appropriate`, `as needed`, alternatives,
or an omitted formula make the window unassignable.

#### F4. Verification block

Every required scenario is an unchecked box with exact assertions:

```markdown
- [ ] W1-V1 Execute SCN-0001 and record activation, oracle and negative-control evidence.
- [ ] W1-V2 Execute the named regression and parity checks.
- [ ] W1-V3 Confirm operation/cardinality/resource ceilings.
- [ ] W1-V4 Confirm privacy, authorization and forbidden outcomes.
- [ ] W1-V5 Assert required = registered = executed coverage-case IDs, zero required skips and matching digest.
```

A command without behavioral assertions is not a verification specification.

#### F5. Handoff block

```markdown
- [ ] W1-H1 Record changed files/symbols and migrations. Evidence: ___
- [ ] W1-H2 Record commands, outcomes, scenarios and skipped checks. Evidence: ___
- [ ] W1-H3 Diff matches the authorized write scope. Evidence: ___
- [ ] W1-H4 No successor-window task or prohibited action was started. Evidence: ___
- [ ] W1-H5 Append the execution and enforcement certificates and set status to AWAITING_REVIEW. Evidence: ___
- [ ] W1-H6 Stop; do not assign or begin the successor.
```

### Phase G — Parent readiness and falsification

The parent MUST copy the checklist in Section 7 into `A4`, complete it with
evidence references, run the audits in Section 8 and issue the certificate in
Section 9.

### Phase H — Assignment

Only after readiness:

1. freeze and hash this standard plus `A1`, `A3`, and `A4`;
2. create one assignment ID;
3. set exact window/action/write scope in `A5`;
4. identify any successor reservation;
5. assign the implementation agent; and
6. require Section 10 execution semantics.

## 5. Mechanical closure certificates

The parent MUST mechanically compare actual discovered sets with planned sets.
At minimum, when applicable, inventory:

- requirements and invariants;
- entry points and public outputs;
- reachable callables;
- payload producers, consumers and parsers;
- durable fields, readers and writers;
- atomic/recovered boundaries;
- identities and authority checks;
- owners and competing-owner pairs;
- external operations;
- configuration/environment reads;
- deployable artifacts and dependency closure;
- control-plane/status mappings;
- workload loops and operation counts;
- terminal/publication transitions;
- tasks, scenarios and evidence assertions; and
- coverage-case IDs, executable registrations and negative controls;
- production boundaries and every test substitute used for acceptance; and
- authorized write symbols per window.

For every set:

1. every actual member has one evidence row, decision/task owner and assertion;
2. every planned member has a source/target anchor and requirement;
3. no member has conflicting owners;
4. no payload member lacks provenance and a strict parser;
5. no requirement lacks an end-to-end trace; and
6. no successor task appears in the predecessor write scope;
7. every required coverage case has exactly one planned registration and no
   registration lacks a required case; and
8. every acceptance substitute has a fidelity proof or an explicitly narrowed
   parity claim.

Record exact extraction/search commands and both set contents in `A6`.

## 6. Predictable gates and blockers

### 6.1 Resolve before assignment

Anything discoverable from current source, schemas, migrations, installed
dependencies, sanitized fixtures, repository history, authoritative
documentation or authorized read-only probes MUST be resolved by the parent.

### 6.2 Ask before assignment

Ask the requester when a product choice, authorization, cost, credential,
destructive action, production target or permission is required before the
sequence.

Sandbox privilege needed only to execute an already-authorized local action is
not such a requester gate. It MUST be handled by the standing E8.1 policy.

### 6.3 Deferred gate

A gate can be deferred only when its value genuinely depends on a named earlier
output. Record:

- gate ID and cause;
- producing window and exact evidence;
- complete bounded result space;
- deterministic action for every result;
- authority required for each action;
- automatic versus requester-controlled branches;
- invalid result behavior; and
- exact resumption state.

Unknown payload shape, parsing semantics, authorization meaning, destructive
scope or transaction behavior MUST NOT be a deferred implementation gate.

### 6.4 Genuine blocker

Stop only when:

- primary evidence contradicts the locked contract and no locked branch applies;
- an implementation-affecting decision or formula is absent;
- required sanitized payload/external evidence is unavailable;
- an exact required permission, environment, credential or approval is absent;
- safe completion requires exceeding the active assignment; or
- authoritative artifacts contradict after applying their declared authority.

A sandbox denial, localhost restriction, headless-browser restriction, build-
filesystem restriction or execution-channel loss is not a blocker when E8.1
permits identical escalated recovery. It becomes a blocker only when the
required escalation is unavailable, the invalidation preconditions cannot be
proved, or the escalated recovery itself produces an observable failing or
unobservable result.

Ordinary coding defects, failing tests with prescribed behavior, context-window
boundaries, completed handoffs and successful window boundaries are not
blockers.

## 7. Mandatory parent authoring checklist

The following boxes MUST be copied into `A4`. Remove none. Mark a concern `N/A`
only by checking it with evidence proving non-applicability.

### 7.1 Authority and artifacts

- [ ] `PA-001` All governing instructions and authorities are recorded. Evidence: ___
- [ ] `PA-002` All eight artifacts exist at named paths. Evidence: ___
- [ ] `PA-003` Mutable status exists only in `A5`. Evidence: ___
- [ ] `PA-004` Execution and approval boundaries are explicit. Evidence: ___
- [ ] `PA-005` Current working tree and repository boundaries were inspected. Evidence: ___
- [ ] `PA-006` Product scope, exclusions and compatibility policy are locked. Evidence: ___
- [ ] `PA-007` The canonical authoring-standard path and revision are pinned for the assignment. Evidence: ___
- [ ] `PA-008` A5 grants standing sandbox escalation for already-authorized local actions and forbids treating that privilege as expanded external authority. Evidence: ___

### 7.2 Evidence and payload safety

- [ ] `PP-001` Every material fact has an allowed classification. Evidence: ___
- [ ] `PP-002` No inferred fact enters a locked contract or task. Evidence: ___
- [ ] `PP-003` Every payload has provenance-labelled sanitized evidence. Evidence: ___
- [ ] `PP-004` Every consumed field has one exact evidence-backed path and type. Evidence: ___
- [ ] `PP-005` Every payload has a strict parser and normalized internal result. Evidence: ___
- [ ] `PP-006` Missing, malformed, boundary and unknown-field fixtures exist. Evidence: ___
- [ ] `PP-007` Multiple supported shapes use explicit evidence-backed discrimination. Evidence: ___
- [ ] `PP-008` No fallback probing, alias guessing, permissive cast or synthetic evidence remains. Evidence: ___
- [ ] `PP-009` Raw secrets and unnecessary private payload data are excluded. Evidence: ___
- [ ] `PP-010` All unknown payload facts are blocking or safely parked. Evidence: ___

### 7.3 Discovery and lifecycle closure

- [ ] `PD-001` All applicable discovery inventories in Phase B are complete. Evidence: ___
- [ ] `PD-002` Claimed absences have negative-search evidence. Evidence: ___
- [ ] `PD-003` Every workflow has a complete state-transition table. Evidence: ___
- [ ] `PD-004` Every external and durable failure boundary is classified. Evidence: ___
- [ ] `PD-005` Duplicate, reorder, retry, restart, stale-process and cancellation behavior is locked. Evidence: ___
- [ ] `PD-006` Every terminal and visibility boundary has durable evidence. Evidence: ___

### 7.4 Decision closure

- [ ] `PC-001` Every applicable D1-D13 ledger, including D2A, is complete. Evidence: ___
- [ ] `PC-002` Every interface and payload schema is exact. Evidence: ___
- [ ] `PC-003` Every multi-write sequence is atomic or has an exact recovery protocol. Evidence: ___
- [ ] `PC-004` Every durable key, identity, fingerprint and timestamp has an exact formula/source. Evidence: ___
- [ ] `PC-005` Every identity cardinality and substitution rule is explicit. Evidence: ___
- [ ] `PC-006` Every competing-owner pair has atomic exclusion, fencing or commutativity proof. Evidence: ___
- [ ] `PC-007` Every external operation has bounded cardinality, cost, retry and ambiguity semantics. Evidence: ___
- [ ] `PC-008` Every permitted retry reconstructs all inputs from durable evidence. Evidence: ___
- [ ] `PC-009` Every replay-affecting configuration value has an exact durability/drift policy. Evidence: ___
- [ ] `PC-010` Control-plane, status and public-output paths are closed. Evidence: ___
- [ ] `PC-011` Build/runtime/deployment dependency closure is proven. Evidence: ___
- [ ] `PC-012` Applied environment capabilities and limits are measured or gated. Evidence: ___
- [ ] `PC-013` Scale, operation-growth and resource ceilings are locked. Evidence: ___
- [ ] `PC-014` Historical/mixed-version policy is an explicit product decision. Evidence: ___
- [ ] `PC-015` No task leaves two materially different implementations possible. Evidence: ___
- [ ] `PC-016` Storage transport, namespace, migration history and test cleanup are proven isolated. Evidence: ___

### 7.5 Scenario and acceptance closure

- [ ] `PS-001` Scenario dimensions derive from current ledgers. Evidence: ___
- [ ] `PS-002` Combination strategy and exclusions are justified. Evidence: ___
- [ ] `PS-003` Every scenario has exact preconditions, actions, activation witnesses and oracle. Evidence: ___
- [ ] `PS-004` Representative nonempty end-to-end behavior is required. Evidence: ___
- [ ] `PS-005` End-to-end acceptance cannot pass through a zero-work/bypass path. Evidence: ___
- [ ] `PS-006` Negative controls prove that required tests can fail. Evidence: ___
- [ ] `PS-007` Every durable/external failure boundary has injection coverage. Evidence: ___
- [ ] `PS-008` Every competing-owner pair has a schedule-sensitive behavioral test. Evidence: ___
- [ ] `PS-009` Generated tests use evidence-backed values, deterministic replay and invariants. Evidence: ___
- [ ] `PS-010` Representative and maximum workload tests assert operation/resource ceilings. Evidence: ___
- [ ] `PS-011` Evidence parity classes match every acceptance claim. Evidence: ___
- [ ] `PS-012` Final/public output is traced to the exercised path. Evidence: ___
- [ ] `PS-013` Every applicable window has a complete behavioral coverage matrix derived from reachable paths and behavior-changing partitions. Evidence: ___
- [ ] `PS-014` Every required coverage case has one unique ID and exactly one planned executable registration. Evidence: ___
- [ ] `PS-015` Acceptance requires exact required/registered/executed case-set equality, zero required skips and an independently recomputed digest. Evidence: ___
- [ ] `PS-016` Every critical invariant has a named falsification control. Evidence: ___
- [ ] `PS-017` Every test substitute has a fidelity proof or a narrowed parity claim. Evidence: ___
- [ ] `PS-018` Accepted tests and fixtures have explicit immutability and evidence-invalidation rules. Evidence: ___
- [ ] `PS-019` Frozen final gates are exact, risk-proportionate and bounded for stateful/costly suites. Evidence: ___
- [ ] `PS-020` Handoff evidence must record coverage counts, skips, duplicates, unexpected IDs, activation failures, negative-control results and digest. Evidence: ___
- [ ] `PS-021` Frozen gates distinguish behavioral failure from proven environment invalidation and prescribe one identical escalated recovery with exact postcondition evidence. Evidence: ___

### 7.6 Window and agent-boundary closure

- [ ] `PW-001` The dependency DAG is acyclic and complete. Evidence: ___
- [ ] `PW-002` Every window establishes one coherent capability. Evidence: ___
- [ ] `PW-003` Every task contains all fifteen F3 fields. Evidence: ___
- [ ] `PW-004` Every task has one complete mechanical trace. Evidence: ___
- [ ] `PW-005` Every window has exact write, read, action and prohibition scope. Evidence: ___
- [ ] `PW-006` Shared-file ownership is symbol-specific and ordered. Evidence: ___
- [ ] `PW-007` Default assignments authorize exactly one window. Evidence: ___
- [ ] `PW-008` Successor reservation and `may_start_successor` are explicit. Evidence: ___
- [ ] `PW-009` Handoff verifies the actual diff against authorized scope. Evidence: ___
- [ ] `PW-010` No successor task is required to satisfy predecessor acceptance. Evidence: ___
- [ ] `PW-011` Every implementation, verification and handoff action is an actual checkbox. Evidence: ___
- [ ] `PW-012` Every checked planning box cites resolvable evidence. Evidence: ___

### 7.7 Traceability and change control

- [ ] `PT-001` Every requirement has a complete A8 trace. Evidence: ___
- [ ] `PT-002` Every source-set member has exactly one plan owner and assertion. Evidence: ___
- [ ] `PT-003` Every planned member has a requirement and source/target anchor. Evidence: ___
- [ ] `PT-004` Evidence is append-only and cannot authorize behavior. Evidence: ___
- [ ] `PT-005` Revision/changelog and invalidation rules are present. Evidence: ___
- [ ] `PT-006` Active-state concurrency/version checks and standard/contract/decision/checklist revision pins are specified. Evidence: ___
- [ ] `PT-007` IDs are unique and never reused. Evidence: ___

### 7.8 Audit and readiness

- [ ] `PR-001` Forward simulation passed for normal and every failure boundary. Evidence: ___
- [ ] `PR-002` Backward simulation traced every public/terminal field to evidence or formula. Evidence: ___
- [ ] `PR-003` Independent reachable-set audit passed. Evidence: ___
- [ ] `PR-004` Payload no-guessing audit passed. Evidence: ___
- [ ] `PR-005` Anti-vacuity and negative-control audit passed. Evidence: ___
- [ ] `PR-006` Environment/runtime/deployment parity audit passed. Evidence: ___
- [ ] `PR-007` Scale and competing-owner falsification passed. Evidence: ___
- [ ] `PR-008` Mistake-derived conformance audit in Section 12 passed. Evidence: ___
- [ ] `PR-009` Mechanical checklist lint has no missing IDs, links, evidence or scopes. Evidence: ___
- [ ] `PR-010` No implementation-affecting choice is delegated. Evidence: ___
- [ ] `PR-011` Enforcement lint rejects missing, duplicate, skipped, filtered, unactivated or unexpected coverage cases. Evidence: ___
- [ ] `PR-012` Substitute-fidelity and accepted-test invalidation audits passed. Evidence: ___
- [ ] `PR-013` Sandbox escalation and identical-recovery lint rejects parent round trips for privilege alone, changed-command retries, real-failure relabelling and external-authority expansion. Evidence: ___

## 8. Mandatory falsification audits

### 8.1 Forward simulation

From every entry point, simulate normal execution and failure at each external
or non-atomic durable boundary. At every step answer with IDs:

- exact existing data and owner;
- next authorized actor;
- duplicate/restart result;
- input reconstruction source;
- external-call permission and cardinality;
- visibility state; and
- next terminal or recoverable state.

### 8.2 Backward simulation

From every public output and terminal state, trace every field and decision to
one validated payload field, durable fact, authorized choice or deterministic
formula. Trace recovery actions backward to sufficient durable evidence.

### 8.3 Counterexample audit

Attempt to produce a conforming-looking plan where:

- a required payload field lacks evidence;
- a test passes without entering required work;
- an external result is lost between call and persistence;
- two identities are incorrectly collapsed;
- two owners overlap;
- an old process or entry point bypasses a new rule;
- maximum cardinality creates unbounded sequential work;
- local/source behavior differs from emitted/target runtime;
- a published platform default differs from an applied limit;
- a successor task is performed by the current agent;
- a resource increase masks an algorithmic defect; or
- a required coverage case is absent, duplicated, skipped, selected but filtered
  out, reported without activation or mapped only by a test name;
- a test substitute returns behavior the production boundary does not provide;
- an accepted test or fixture is weakened without invalidating its evidence; or
- compatibility work is invented without a requirement;
- an already-authorized local command is blocked only because it needs sandbox
  escalation; or
- a real assertion failure, changed command or external action is incorrectly
  admitted as an automatic sandbox recovery.

The authored package MUST reject every applicable counterexample mechanically
or with a decisive scenario. Otherwise it remains draft.

### 8.4 Mechanical lint

The parent MUST provide a reproducible lint operation that verifies at least:

- stable ID uniqueness;
- no unresolved placeholders in checked items;
- every checked item has evidence;
- every evidence reference resolves;
- every requirement trace is complete;
- every task has a window and ownership scope;
- every scenario has an oracle and activation witness;
- every applicable window has a complete coverage matrix;
- every required case ID is unique and has exactly one planned registration;
- every critical invariant has a negative-control mapping;
- every test substitute has a fidelity disposition;
- every window has a successor policy;
- no overlapping assignment exists; and
- standard/contract/decision/checklist hashes match active state.

If no reusable checker exists, the parent records exact deterministic searches
and set comparisons. A visual skim is insufficient.

Document lint and execution lint are separate gates. Document lint proves that
the prescribed sets and mappings are complete before assignment. Execution lint
proves after implementation that the registered and executed sets equal the
prescribed set, all activation witnesses ran, and required cases were not
skipped or filtered.

### 8.5 Enforcement falsification audit

For each applicable enforcement mechanism, prescribe safe deterministic
controls that demonstrate acceptance fails when:

1. one required case registration is removed;
2. one required case is skipped or filtered out;
3. one case ID is duplicated or an unexpected ID is reported;
4. the claimed production path is bypassed so its activation witness is absent;
5. one critical oracle is weakened or its forbidden-operation assertion is
   removed; and
6. one behavior-affecting test substitute difference is introduced.

The controls MAY use injected collaborators, boundary faults, isolated
controlled mutation, simulator behavior or another safe deterministic method.
The standard does not authorize production-source edits, destructive actions or
external mutations to perform them. Authoring readiness requires the controls
and their expected failures to be fully prescribed; execution handoff requires
the controls named for that window to have falsified acceptance.

## 9. Readiness certificate

The parent may set `READY` only after appending this certificate to `A6`:

```yaml
certificate: AUTHORING-READY
artifact_paths:
  A1: path
  A2: path
  A3: path
  A4: path
  A5: path
  A6: path
  A7: path
  A8: path
revisions:
  standard: sha256
  contract: sha256
  decision: sha256
  checklist: sha256
checked_authoring_items: exact count
unchecked_required_items: 0
unresolved_evidence_references: 0
unresolved_payload_contracts: 0
delegated_implementation_decisions: 0
unowned_source_members: 0
unowned_plan_members: 0
unproven_competing_owner_pairs: 0
anti_vacuity_failures: 0
mistake_conformance_failures: 0
planned_coverage_cases: exact count
unmapped_coverage_cases: 0
duplicate_coverage_case_ids: 0
critical_invariants_without_negative_control: 0
test_substitutes_without_fidelity_disposition: 0
unresolved_accepted_evidence_invalidations: 0
frozen_gate_ambiguities: 0
predictable_gates: []
requester_actions_before_start: []
authorized_first_window: W1
planned_stop: exact stop
audit_evidence: []
```

Any nonzero prohibited count makes the package `DRAFT / NOT ASSIGNABLE`.

## 10. Implementation and orchestration protocol

### 10.1 Agent preflight

Before editing, the assigned agent MUST:

1. read `A5`;
2. verify assignment ID, agent identity,
   standard/contract/decision/checklist hashes and state version;
3. verify its exact window and write/action scope;
4. inventory existing dirty changes;
5. check predecessor outputs; and
6. complete the window precondition boxes with evidence.

Mismatch is a coordination blocker. It does not authorize reconciliation by
guessing.

### 10.2 During execution

The agent:

- follows task order and locked decisions;
- checks a task only after implementation plus its named local proof;
- registers and reports coverage cases only after their activation witnesses and
  oracles execute;
- records evidence as work occurs;
- fixes ordinary defects within scope when behavior is prescribed;
- stops on a genuine blocker; and
- never begins successor work.

Discovering that a successor edit would be convenient is not authorization.

### 10.3 Handoff

The agent completes F5, appends evidence and moves only its current status to
`AWAITING_REVIEW` using state-version comparison. It MUST NOT assign the
successor or change `authorized_windows`.

When enforcement closure applies, the handoff evidence MUST include:

```yaml
enforcement_certificate: WINDOW-ENFORCEMENT
window_id: W1
frozen_source_revision: exact revision or deterministic file hashes
frozen_test_revision: exact revision or deterministic file hashes
required_case_count: exact count
registered_case_count: exact count
executed_case_count: exact count
required_case_set: exact inline set or resolvable immutable artifact plus digest
registered_case_set: exact inline set or resolvable immutable artifact plus digest
executed_case_set: exact inline set or resolvable immutable artifact plus digest
skipped_required_cases: []
duplicate_case_ids: []
unexpected_case_ids: []
missing_activation_witnesses: []
oracle_failures: []
negative_controls_expected: exact count
negative_controls_falsified: exact count
required_case_set_digest: lowercase SHA-256
registered_case_set_digest: lowercase SHA-256
executed_case_set_digest: lowercase SHA-256
commands: []
parity_classes_proven: []
accepted_tests_or_fixtures_changed: []
evidence_invalidated_or_superseded: []
```

Counts without the corresponding exact sets and digest are insufficient.

### 10.4 Parent transition

The parent independently verifies:

- behavioral assertions and negative controls;
- exact equality of required, registered and executed coverage cases;
- zero required skips, missing activation witnesses, duplicate IDs and
  unexpected IDs;
- test-substitute fidelity at every claimed parity class;
- accepted-test/fixture immutability or explicit evidence invalidation;
- actual diff/write-scope closure;
- no successor work;
- evidence completeness;
- regression and parity claims; and
- current active-state version.

On pass, the parent records acceptance and creates a new assignment ID for the
successor. This orchestration MAY continue automatically without requester
intervention when authorization already covers it.

### 10.5 Explicit multi-window exception

One agent may cross a window boundary only when `A5` explicitly lists every
authorized window, `may_start_successor: true`, no listed successor is reserved
for another agent, and the requester/parent execution policy selected this mode
before assignment. Adjacency, dependency, passing tests or available context
never implies permission.

## 11. Corrections and completion

### 11.1 Correction protocol

When evidence contradicts a locked specification:

1. stop affected assignment;
2. append evidence;
3. identify violated requirement/decision and root cause;
4. append `A7` impact analysis;
5. invalidate affected unaccepted tasks/evidence explicitly;
6. revise and rehash the specification;
7. create a uniquely identified corrective window when implementation is
   required; and
8. issue a new assignment.

Do not rewrite completed evidence or reuse IDs.

Any modification, weakening, deletion, renaming, filtering or replacement of a
test, fixture, substitute or enforcement manifest that supports accepted
evidence invalidates that evidence unless the active window explicitly owns the
change and supplies a named superseding proof. Formatting-only claims require a
mechanical proof that registrations, activation witnesses and oracles are
unchanged.

### 11.2 Diagnostic discipline

Do not prescribe a resource, timeout, retry or compatibility expansion before
reproducing and isolating the causal failure when safe evidence can do so.
Mitigations require an explicit causal claim, falsification attempt and
regression test.

### 11.3 Final review

The parent MUST independently:

- inspect current source and full diff;
- rerun risk-proportionate scenarios and negative controls;
- verify required/registered/executed coverage-case equality and the independent
  digest;
- verify required cases have zero skips and every reported case has its
  activation witness;
- verify substitute fidelity and accepted-test/fixture integrity;
- inspect payload parsers and evidence provenance;
- trace full current-format representative nonempty execution;
- verify ownership, concurrency, retry and visibility invariants;
- verify scale ceilings and target-runtime artifacts;
- review live claims only at their proven parity class;
- reconcile all checklist boxes, evidence and changelog revisions; and
- report concrete residual blockers only.

Completion requires no unresolved contradiction with `A1`, no guessed payload,
no delegated decision, no unaccepted required window and no overstated evidence.

## 12. Mistake-derived conformance audit

This section validates the standard against the failure classes recorded in
`mistakes.md`. It is not an architecture catalogue and supplies no project
defaults.

For each row, a future parent MUST identify the current-project evidence and
applicable implementation. The prevention rule alone is not project evidence.

| Failure ID | Abstract failure class | Mandatory prevention chain | Falsification required |
|---|---|---|---|
| `M-01` | Exact formulas, artifacts, timestamps, transactions, packaging or test isolation omitted | Sections 2.3, 3, D1-D5 including D2A, D9, F3, `PC-002`-`PC-004`, `PC-016`, `PW-003`-`PW-004` | Remove one formula or transaction classification; lint/readiness must fail |
| `M-02` | Component or zero-work tests falsely accepted as end-to-end proof | E1, E2, `PS-003`-`PS-006`, Sections 8.2-8.3 | Bypass a required execution unit; negative control must fail the scenario |
| `M-03` | Applied account/platform quotas and deployment transport limits discovered after design | D9-D10, E5, `PC-011`-`PC-012`, `PR-006` | Substitute a published/default value for measured applied capability; readiness must fail or gate it |
| `M-04` | Control-plane creation/configuration/status paths or stale processes bypassed the implementation | Phase B items 13-14, D7-D8, `PC-009`-`PC-010`, `PD-005` | Add an alternate writer/caller or old process; set-equality and lifecycle audit must expose it |
| `M-05` | Local/source tests did not represent target runtime, native closure or authorization semantics | D9-D10, E5, `PC-011`-`PC-012`, `PS-011` | Make emitted artifact or live authorization behavior differ from local simulation; parity claim must be rejected |
| `M-06` | Happy-path inputs/recovery/presentation passed while malformed values, self-retry, stale state or UI mapping failed; resources were raised before cause | D4, D8, D13, Phase E, Section 11.2, `PD-005`, `PS-007`-`PS-008` | Inject malformed/boundary input, same-owner retry and stale state; remove causal proof for mitigation and require failure |
| `M-07` | Sequential/N+1 behavior and transaction limits appeared only at realistic scale; unnecessary historical compatibility was designed | D11-D12, E4, `PC-013`-`PC-014`, `PS-010` | Increase cardinality and compare operation growth; delete compatibility requirement and ensure compatibility tasks become unowned/invalid |
| `M-08` | External-source terminal states, cache-only paths, version resolution, identity fan-in/fan-out or emitted deployment closure were modeled incorrectly | D3, D5-D6, D9, `PC-005`, `PC-007`, `PC-011`, Phase E | Exercise every identity-cardinality and terminal-state partition; compare all emitted units after shared-source change |
| `M-09` | Execution authority was generalized across independent runs/resources and competing worker/finalizer claims were not atomically exclusive | D3-D4, C transition tables, E3, `PC-005`-`PC-006`, `PS-008` | Schedule every competing-owner pair across independent execution identities; invariant must reject overlap and preserve independence |
| `M-10` | Broad scenario names and passing commands concealed omitted paths, outcomes, assertions or divergent test substitutes | E6-E8, `PS-013`-`PS-020`, Sections 8.4-8.5 and the handoff enforcement certificate | Remove, skip, filter or duplicate one case; bypass its activation witness; weaken one oracle; or diverge one substitute. Document or execution acceptance must fail |

The standard fails its own conformance if any `mistakes.md` failure cannot be
mapped to:

```text
generic rule -> mandatory checkbox -> evidence type -> scenario/oracle ->
counterexample -> readiness failure
```

## 13. Prior-standard preservation audit

The new standard MUST preserve the enforceable strengths of both predecessor
standards without inheriting project-specific architecture.

| Prior requirement class | Preserved in |
|---|---|
| Parent owns discovery, decisions and final review | Sections 1, 4 and 11 |
| One source of truth and stable IDs | Sections 2 and 11 |
| Observed/inferred/unknown classification | Section 3 |
| No fallback payload probing | Section 3 and `PP-*` |
| Complete lifecycle and durable-boundary reasoning | Phase C and D2-D6 |
| Exact task anchors, signatures, algorithms and callers | F3 and `PW-*` |
| Atomicity and recovery reconstruction | D2, D5-D6 and `PC-*` |
| External-call ambiguity and configuration closure | D6-D7 |
| Packaging and production dependency closure | D9 and E5 |
| Database/environment isolation as an observed transport property | D2A, D10 and E5 |
| Ownership across transitions and legacy callers | D3-D4 and Phase C |
| Set equality and negative source searches | Phase B and Section 5 |
| Executable behavioral coverage, test-substitute fidelity and frozen risk-proportionate gates | E6-E8, Sections 8.4-8.5 and 10.3-10.4 |
| Predictable gates reported before execution | Section 6 |
| Independent contradiction/reliability review | Sections 8 and 11 |
| Append-only corrective history | A7 and Section 11 |
| Continuous orchestration without routine requester gates | Sections 1.4 and 10.4 |

Preservation is valid only when the current-project checklist supplies evidence
and checked items; this table does not satisfy readiness itself.

## 14. Mandatory parent handoff

After authoring, report only:

1. `READY` or `DRAFT / NOT ASSIGNABLE`;
2. the eight artifact paths;
3. authorized assignment and planned stop;
4. checked/unchecked authoring counts;
5. payload unknown count;
6. planned coverage-case count, unmapped-case count, critical-invariant
   negative-control count and unresolved substitute-fidelity count;
7. mistake-conformance and falsification results;
8. predictable gates and requester actions; and
9. concrete remaining blockers.

Do not replace verification with a long risk list. Resolve what evidence can
resolve, classify what cannot, and fail closed.
