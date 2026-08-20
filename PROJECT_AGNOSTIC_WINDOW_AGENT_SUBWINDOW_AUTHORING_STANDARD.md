# Project-Agnostic Window-Agent Sub-Window Authoring Standard

## 0. Status, purpose, and authority

This standard defines how a window agent converts one parent-authored,
decision-complete implementation window into sequential, single-file
sub-windows that lower-level implementation agents can execute mechanically.

It supplements, and does not replace,
`PROJECT_AGNOSTIC_DECISION_COMPLETE_CHECKLIST_AUTHORING_STANDARD.md`. The parent
standard controls the product contract, project decisions, parent-window
boundary, and parent acceptance. This standard controls decomposition and
execution below that boundary.

The key words `MUST`, `MUST NOT`, `REQUIRED`, `SHALL`, `SHALL NOT`, `SHOULD`,
and `MAY` are normative.

This standard does not authorize a window, file edit, test, external action, or
subagent. Authority must already exist in the parent assignment and must be
delegable by its terms.

Sandbox escalation required to execute an already-authorized local action is
not a new test or external action and does not broaden parent scope. It follows
the parent standard's E8.1 execution-environment policy.

### 0.1 Governing principle

Every managing agent is the complete author for its immediate lower level:

```text
parent agent
  -> authors a complete parent window
window agent
  -> authors complete single-file sub-windows
implementation subagent
  -> executes one single-file sub-window
window agent
  -> performs whole-window assessment
parent agent
  -> performs parent-window acceptance
```

No managing agent may delegate an unresolved decision, execution detail, or
acceptance ambiguity to its child.

### 0.2 Completeness definitions

A sub-window is `decision-complete` only when its implementation agent has no
material behavior, interface, dependency, algorithm, failure, compatibility,
or acceptance choice left to make.

A sub-window is `execution-complete` only when its implementation agent knows:

1. the one exact file it may write;
2. the exact starting state and required ending state;
3. the symbols, anchors, and ordered edits;
4. the predecessor state on which it depends;
5. the checks it must run and the assertions those checks must prove;
6. the evidence it must return;
7. the actions and files that remain prohibited; and
8. the exact conditions for completion, loss of authority, or escalation.

A sub-window is `enforcement-complete` only when omitted, bypassed, weakened,
duplicated, or incorrectly classified required behavior cannot still satisfy
its acceptance checks.

A decomposition is conforming only when every implementation and corrective
sub-window satisfies all three definitions and the final whole-window
assessment verifies their assembled behavior.

### 0.3 Scope-relative decisions

The parent agent owns product and parent-window decisions. The window agent may
decide only mechanical decomposition matters that cannot change those locked
decisions, including:

- the order in which already-required files are edited;
- the allocation of already-required coverage cases to exact test files;
- the point at which a frozen interface becomes available to a dependent file;
- file-local verification commands; and
- correction routing after a diagnosed failure.

The window agent MUST NOT change or fill a missing product behavior, public
interface, durable formula, ownership rule, transaction rule, failure outcome,
cost policy, external contract, or parent acceptance rule. A missing material
decision makes decomposition `BLOCKED`, not an opportunity to design.

### 0.4 Standard revision

The revision of this standard is the lowercase SHA-256 of this file. Every
sub-window decomposition MUST record:

- this standard's path and revision;
- the parent standard's path and revision;
- the parent window's contract, decision, checklist, and active-state
  revisions; and
- the exact parent assignment ID being decomposed.

A revision mismatch blocks new sub-window assignment. It does not invalidate an
already completed sub-window whose evidence pins its prior frozen revisions,
but the window agent must perform and record a delta audit before assigning the
next sub-window.

## 1. Roles and communication boundary

### 1.1 Parent agent

The parent agent:

- authors and assigns one complete parent window;
- freezes all product and cross-file decisions required by that window;
- authorizes or prohibits delegation;
- reviews the window agent's decomposition before leaf execution begins;
- communicates only with the window agent about that window;
- receives the window agent's consolidated handoff; and
- independently accepts, rejects, or revises the parent window.

The parent agent MUST NOT directly assign, correct, or accept a sub-window. If
the parent identifies a leaf-level issue, it returns the issue to the window
agent, which authors the appropriate sub-window.

### 1.2 Window agent

The window agent is both:

1. the implementation coordinator for the parent window; and
2. the parent author and reviewer for every sub-window beneath it.

The window agent:

- independently inspects the current working tree and primary source;
- verifies that the parent window is complete enough to decompose;
- compiles a sequential single-file dependency graph;
- authors every implementation and corrective sub-window;
- assigns exactly one active implementation sub-window at a time;
- reviews every returned file diff and its local evidence;
- personally performs every whole-window assessment sub-window;
- diagnoses integration failures before authoring corrections;
- consolidates leaf evidence without overstating it; and
- communicates upward only after decomposition review, a genuine parent-level
  blocker, or successful whole-window approval.

The window agent MUST NOT edit implementation files during decomposition,
leaf review, whole-window assessment, diagnosis, or handoff. Even a trivial
implementation correction requires a new single-file corrective sub-window.

The window agent MAY write only the exact coordination artifacts authorized for
the window agent itself. Those administrative writes do not grant authority to
modify implementation files.

### 1.3 Implementation subagent

An implementation subagent:

- receives exactly one sub-window;
- may write exactly one named file;
- may read only the named scope required by that sub-window;
- executes the specified edits and local checks;
- reports only to the window agent; and
- stops at `AWAITING_WINDOW_REVIEW`.

It MUST NOT:

- communicate or escalate directly to the parent agent;
- spawn or delegate to another implementation agent;
- edit decomposition, state, evidence, contract, decision, or parent-checklist
  artifacts;
- start a successor or corrective sub-window;
- make a convenient edit in a second file;
- repair a discovered parent-window omission by inventing behavior; or
- claim that the assembled parent window works.

### 1.4 Strict adjacency

Permitted task communication is:

```text
implementation subagent <-> window agent <-> parent agent
```

The following are prohibited:

- implementation subagent -> parent agent;
- parent agent -> implementation subagent;
- implementation subagent -> another implementation subagent; and
- a whole-window verifier separate from the responsible window agent.

Raw subagent conversations are not parent handoff evidence. The window agent
must independently validate and consolidate material claims.

## 2. Required subordinate package

The window agent MUST create or identify these three subordinate artifacts for
the assigned parent window. They are subordinate to the parent package and
cannot broaden it.

| ID | Artifact | Sole subordinate authority |
|---|---|---|
| `S1` | Frozen sub-window decomposition checklist | Sub-window DAG, exact file assignments, task specifications, checks, and handoff requirements |
| `S2` | Active sub-window state | Current leaf or assessment assignment, identity, scope, status, and revision pins |
| `S3` | Append-only sub-window evidence | Decomposition, execution, review, correction, and whole-window assessment evidence |

Traceability is a mandatory section of `S1`; it does not require a fourth
artifact. Live status MUST exist only in `S2`. Execution evidence MUST exist
only in `S3`.

Each artifact MUST name the other two and the complete inherited parent
artifact package.

### 2.1 Frozen decomposition checklist (`S1`)

`S1` MUST contain:

1. inherited authority and revision pins;
2. exact parent-window scope and exclusions;
3. starting working-tree inventory;
4. the initial single-file dependency DAG;
5. every initial implementation sub-window;
6. exact allocation of requirements, decisions, interfaces, and coverage cases;
7. exact local and whole-window verification gates;
8. correction and re-assessment rules;
9. mandatory authoring-readiness checkboxes;
10. sub-window and whole-window handoff templates; and
11. append-only amendment sections for later corrective sub-windows.

Once the parent accepts the initial decomposition, its existing sub-window
blocks are immutable. Corrections are appended with new IDs; they do not rewrite
the original decomposition or evidence.

### 2.2 Active sub-window state (`S2`)

`S2` MUST contain one machine-scannable block and no history:

```yaml
state_version: 1
parent_window_id: W1
parent_assignment_id: ASG-W1
window_agent_identity: exact identity
parent_standard_path: path
parent_standard_revision: sha256
subwindow_standard_path: path
subwindow_standard_revision: sha256
parent_contract_revision: sha256
parent_decision_revision: sha256
parent_checklist_revision: sha256
decomposition_path: path
decomposition_revision: sha256
evidence_path: path
decomposition_status: DRAFT | AWAITING_PARENT_DECOMPOSITION_REVIEW | READY
current_subwindow: W1-S001 | W1-C001 | W1-I001 | STOP
current_assignment_id: ASG-W1-S001 | WINDOW-AGENT
assigned_agent: exact identity | WINDOW-AGENT | UNASSIGNED
subwindow_type: FILE | CORRECTION | INTEGRATION_ASSESSMENT
authorized_write_file: exact path | NONE
authorized_read_scope: [exact paths, directories, symbols, or artifacts]
authorized_actions: []
prohibited_actions: []
execution_environment_policy: exact inherited parent policy
may_start_successor: false
current_status: READY | IN_PROGRESS | AWAITING_WINDOW_REVIEW | BLOCKED | COMPLETE
accepted_subwindows: []
next_subwindow: exact ID | STOP
blocker: null
last_updated: ISO-8601
```

Only the window agent may update `S2`. A lower-level agent's completion report
does not itself change state or authorize a successor.

### 2.3 Append-only evidence (`S3`)

Every evidence entry MUST identify:

- stable evidence ID and timestamp;
- parent window, sub-window, and assignment IDs;
- actor and role;
- frozen revisions and starting file digest;
- exact command or inspection performed;
- sandbox privilege used, any environment-invalidated attempt, its read-only
  postcondition proof, and its identical recovery outcome;
- decisive observed result, assertion, and activation witness;
- ending file digest and exact changed path set;
- required, registered, executed, skipped, duplicate, and unexpected coverage
  cases applicable to that sub-window;
- negative-control result when required;
- limitations and deliberately deferred whole-window checks;
- external mutations, costs, or confirmation that none occurred; and
- review disposition by the window agent.

Evidence cannot amend a task, decision, or authority boundary.

## 3. Decomposition entry gate

Before authoring a sub-window, the window agent MUST independently verify:

1. the parent assignment is current and explicitly names the window agent;
2. delegation to lower-level agents is authorized;
3. parent standard, contract, decision, checklist, and state revisions match;
4. the parent window is `READY` or `IN_PROGRESS` for decomposition;
5. its exact write, read, action, and prohibition scopes are known;
6. every implementation-affecting decision required by the window exists;
7. every expected changed file can be derived from current source and the
   parent trace;
8. the current dirty working tree is inventoried without modifying it;
9. no unrelated owner-controlled change will be overwritten; and
10. no required action exceeds parent authority.

If any item fails, the window agent reports one concrete blocker to the parent.
It MUST NOT create speculative leaf work to discover what the parent meant.

## 4. Single-file invariant

### 4.1 Exact rule

Every `FILE` or `CORRECTION` sub-window MUST authorize exactly one canonical
workspace file path as writable.

For a sub-window with writable file `F`:

```text
workspace files changed by sub-window = {F}
```

This is exact set equality, not a maximum or recommendation. A directory,
glob, file class, generated group, or symbol spread across files is not a file
path and is prohibited.

The one-file rule includes:

- source files;
- test files;
- fixtures;
- schemas and migrations;
- configuration files;
- manifests and lock files;
- documentation;
- generated tracked files; and
- create, modify, or delete operations.

A production file and its separate test file therefore require separate,
ordered sub-windows.

### 4.2 Read scope

One-file write ownership does not mean one-file understanding. Each sub-window
MUST identify the exact read-only dependencies needed to implement and verify
the file. The subagent may inspect those dependencies but may not edit them.

### 4.3 Existing dirty state

Before assignment, the window agent records:

- whether the writable file exists;
- its complete content digest or `ABSENT`;
- its existing dirty status;
- the exact pre-existing hunks or owner-controlled portions that must remain;
  and
- the complete starting changed-file set for the repository.

The subagent must preserve unrelated existing changes. A file already modified
by another active owner is not assignable until ownership is reconciled by the
window agent without discarding either change.

### 4.4 Commands and incidental writes

A subagent MUST NOT run a command that can modify another workspace file.
Formatting, generation, migration, installation, build, snapshot-update, and
fix commands are allowed only when the sub-window proves that their workspace
write set is exactly the authorized file.

Disposable runtime output is permitted only outside the workspace or in an
exact parent-authorized disposable location, with its cleanup and residual
state prescribed. It never counts as authority to change a second tracked or
untracked workspace file.

### 4.5 Moves, renames, and multi-output generators

A rename or move changes two paths and is not one single-file sub-window. If
the parent decision requires the equivalent result, the window agent must
compile it into explicit ordered create, consumer-update, and delete
sub-windows, each owning one file and each defining the permitted intermediate
state.

A generator that necessarily changes multiple workspace files cannot be run by
a lower-level agent under this standard. Each resulting file must be handled by
its own exact sub-window using a parent-authorized deterministic method, or the
window agent must escalate the incompatibility to the parent.

### 4.6 Mechanical enforcement

Every file sub-window preflight and handoff MUST compare:

1. repository changed-file set before execution;
2. repository changed-file set after execution;
3. starting and ending digest of the writable file; and
4. starting and ending digests of any already-dirty protected files.

The delta attributable to the sub-window MUST contain exactly its writable
file and no other workspace path. Any unexplained second-file change fails the
sub-window even if tests pass.

### 4.7 Canonical paths, file digests, and set digests

A writable file path MUST be workspace-relative, use `/` separators, contain no
`.` or `..` path segment, and resolve lexically beneath the workspace root. An
existing writable target MUST be a regular file, not a symbolic link. A new
target must not traverse a symbolic-link parent. Platform-specific path aliases
must be normalized before comparison.

The file digest is lowercase SHA-256 over the exact raw file bytes. A missing
path is represented by the literal token `ABSENT`, not the digest of an empty
file.

For every path or ID set digest:

1. fail if any member is duplicated;
2. encode each member as UTF-8;
3. sort distinct members by unsigned UTF-8 byte order;
4. concatenate each member followed by one LF byte; and
5. compute lowercase SHA-256 over the resulting bytes.

An empty set is therefore the SHA-256 of zero bytes. Every subordinate artifact
must use this formula; tool-default locale sorting is not authoritative unless
it is proven to produce the same byte order.

## 5. Sub-window types and lifecycle

### 5.1 Initial file sub-window

An initial file sub-window has ID:

```text
<parent-window>-S<three-or-more digits>
```

Example grammar only: `W1-S001`. IDs are unique and never reused.

It implements the initially compiled change to one file.

### 5.2 Corrective file sub-window

A corrective sub-window has ID:

```text
<parent-window>-C<three-or-more digits>
```

It owns one file and cites:

- the failed review or integration evidence;
- the exact root cause;
- the original requirement and decision already determining the correction;
- the earlier sub-window whose result it corrects or completes; and
- the checks invalidated by the correction.

A correction may revisit a previously edited file, but it is always a new
sub-window with a new baseline digest and assignment ID. Reopening, rewriting,
or silently extending the old sub-window is prohibited.

If the correction requires a new parent-level decision or expanded parent
scope, no corrective sub-window may be authored; the window agent escalates.

### 5.3 Integration-assessment sub-window

An integration-assessment sub-window has ID:

```text
<parent-window>-I<three-or-more digits>
```

It is assigned to and personally executed by the window agent. It has:

- `authorized_write_file: NONE` for implementation files;
- the assembled current window state as input;
- exact frozen whole-window gates;
- exact diff, traceability, coverage, and prohibition checks; and
- a result of `PASS`, `CORRECTION_REQUIRED`, or `PARENT_BLOCKED`.

It is not delegated to a verifier subagent. It may update only the window
agent's authorized coordination artifacts.

### 5.4 Required sequential lifecycle

Only one sub-window may be active at a time:

```text
DRAFT DECOMPOSITION
  -> PARENT DECOMPOSITION REVIEW
  -> READY
  -> initial file sub-window
  -> window-agent file review
  -> next initial file sub-window
  -> ...
  -> integration assessment by window agent
       -> PASS -> parent handoff
       -> CORRECTION_REQUIRED
            -> one or more sequential single-file corrective sub-windows
            -> window-agent review after each
            -> new integration assessment by window agent
            -> repeat until PASS or PARENT_BLOCKED
```

Parallel implementation sub-windows are prohibited by this standard. Disjoint
files do not create implied parallel authority.

### 5.5 No automatic successor authority

A subagent never starts the next sub-window. After reviewing the returned work,
the window agent closes the current assignment, updates `S2`, and issues a new
assignment ID. Passing local tests or seeing an adjacent dependency does not
authorize continuation.

## 6. Compiling the initial dependency graph

The window agent MUST derive the initial changed-file set mechanically from:

- parent requirements and decisions;
- parent task source and target anchors;
- the current reachable source graph;
- current interfaces, callers, consumers, tests, fixtures, and build closure;
- required coverage-case registrations and witnesses; and
- explicit removals and preserved behavior.

For every planned file, record:

```yaml
file_id: F-001
path: exact canonical workspace-relative path
operation: CREATE | MODIFY | DELETE
current_digest: sha256 | ABSENT
parent_requirement_ids: []
parent_decision_ids: []
parent_task_ids: []
owned_symbols_or_anchors: []
depends_on_files: []
consumed_interfaces: []
produced_interfaces: []
coverage_case_ids: []
reason_required: exact trace
preserved_content: []
prohibited_changes: []
```

Then mechanically prove:

```text
required changed-file set = planned initial file set
planned initial file set = files owned by initial sub-windows
```

Every file has exactly one initial owner. Every dependency edge names the
specific interface or evidence that requires the order. The graph must be
acyclic.

### 6.1 Intermediate-state contract

Because cross-file changes are sequential, each edge MUST define the permitted
intermediate state after its producer file changes and before its consumers do.
Record:

- which local checks must already pass;
- which whole-window checks are expected to remain pending or fail;
- the exact expected temporary failure, if any;
- why the state is safe and not externally visible;
- which later sub-window resolves it; and
- actions prohibited while the intermediate state exists.

“Tests may fail until later” is insufficient. Unexpected failures stop the
sequence for diagnosis.

### 6.2 Interface freeze

Before the first dependent sub-window begins, the window agent MUST specify the
complete cross-file interface, including applicable:

- exported and imported names;
- signatures and argument ordering;
- schemas and field rules;
- return and error unions;
- state transitions and transaction participation;
- configuration and defaults;
- identity and fingerprint formulas;
- call cardinality and side effects; and
- compatibility and removal behavior.

A subagent may not choose between interface alternatives. If current source
contradicts the parent decision, the window agent reports the contradiction
before assignment.

## 7. Mandatory exact sub-window block

Every `FILE` and `CORRECTION` sub-window in `S1` MUST contain all fields below.
Omitting one makes it `DRAFT / NOT ASSIGNABLE`.

### 7.1 Identity and authority

```yaml
subwindow_id: W1-S001
type: FILE | CORRECTION
parent_window_id: W1
parent_assignment_id: ASG-W1
assigned_agent: exact identity | UNASSIGNED
predecessors: []
successor_reserved_for: WINDOW-AGENT
writable_file: exact canonical path
file_operation: CREATE | MODIFY | DELETE
starting_file_digest: sha256 | ABSENT
starting_repository_change_set_digest: sha256
read_only_scope: []
authorized_actions: []
prohibited_actions: []
may_start_successor: false
```

### 7.2 Mechanical trace

Record exact parent requirement, invariant, decision, task, scenario, and
coverage-case IDs. Every requirement allocated to the sub-window must terminate
in a file anchor, an executable assertion, or a named output consumed by a
successor.

### 7.3 Exact file transformation

Specify:

1. exact source anchors and their current relevant behavior;
2. exact target anchors;
3. exact additions, modifications, and deletions in execution order;
4. complete signatures, schemas, constants, formulas, and bounds;
5. exact imports, exports, callers, and consumers affected by this file;
6. operation ordering and atomic/recovered-boundary classification;
7. success, failure, duplicate, retry, restart, concurrency, and cancellation
   outcomes applicable to this file;
8. preserved behavior and content;
9. obsolete behavior removed from this file;
10. the exact resulting interface exposed to successor sub-windows; and
11. forbidden edits within the writable file.

The verbs `choose`, `decide`, `determine`, `as appropriate`, `as needed`,
`similar`, `etc.`, and materially different alternatives make the sub-window
unassignable unless they describe non-behavioral formatting freedom.

### 7.4 Exact checks

Every check must identify:

- exact command or deterministic inspection;
- required setup and environment;
- required sandbox privilege class and the inherited identical-recovery rule;
- expected exit/result;
- exact activation witness;
- exact assertions and forbidden operations;
- coverage-case IDs registered and executed;
- negative control when applicable;
- expected workspace write set; and
- whether the check is `LOCAL_NOW` or `DEFERRED_TO_INTEGRATION`.

A command name or passing test count without behavioral assertions is not an
acceptance specification.

### 7.5 File-subwindow completion checklist

Each block MUST contain unchecked boxes equivalent to:

```markdown
- [ ] P1 Revisions, assignment identity, writable file, baseline digest, and predecessor evidence match.
- [ ] P2 Starting repository status and protected dirty changes match the recorded baseline.
- [ ] T1 Apply every ordered transformation and no other edit to the writable file.
- [ ] V1 Run every LOCAL_NOW check and record its activation witnesses and exact assertions.
- [ ] V2 Prove the attributable workspace changed-file set is exactly the writable file.
- [ ] V3 Prove required local coverage IDs equal registered and executed local IDs with zero skips.
- [ ] H1 Return the exact diff, ending digest, commands, outcomes, and residual integration obligations.
- [ ] H2 Confirm no prohibited action, second-file edit, successor work, external mutation, or parent communication occurred.
- [ ] H3 Stop at AWAITING_WINDOW_REVIEW.
```

Checked boxes must cite resolvable `S3` evidence.

## 8. Window-agent review of each file sub-window

The window agent MUST independently inspect, not merely accept the subagent's
summary. Before accepting a file sub-window, verify:

1. assignment and frozen revisions matched at execution;
2. exactly one authorized file changed attributable to the sub-window;
3. unrelated dirty state remained unchanged;
4. the actual diff implements every prescribed transformation;
5. no prescribed behavior was omitted or weakened;
6. public and cross-file interfaces match the frozen form byte-for-byte where
   applicable;
7. local checks exercised their claimed production path;
8. required local coverage cases equal registered and executed cases;
9. no required case was skipped, duplicated, filtered, unexpected, or reported
   without its activation witness;
10. test substitutes have only the prescribed parity claim;
11. no accepted test, fixture, or oracle was weakened without explicit
    invalidation and superseding proof;
12. the resulting intermediate state matches Section 6.1; and
13. no successor or prohibited action began.

The disposition is exactly one of:

- `ACCEPTED_FOR_INTEGRATION`: close the sub-window and assign its planned
  successor;
- `CORRECTION_REQUIRED`: diagnose and append one or more single-file corrective
  sub-windows; or
- `PARENT_BLOCKED`: stop and report a missing decision, contradiction, or scope
  expansion to the parent.

The window agent cannot directly repair the file during review.

## 9. Whole-window integration assessment

### 9.1 When it is authored

The initial integration assessment MUST be fully authored before initial leaf
execution begins, except that its frozen source revision and actual executed
evidence references are filled from completed sub-windows.

Every later assessment after correction is a new appended assessment sub-window
with a new ID. It reuses unchanged gates by exact reference and lists every gate
invalidated by the corrections.

### 9.2 Exact assessment contents

Every integration-assessment block MUST specify:

1. exact accepted sub-window IDs and resulting file digests;
2. exact assembled changed-file set expected by the parent window;
3. requirement -> decision -> file -> sub-window -> assertion trace;
4. complete required coverage-case set and digest;
5. exact integration, regression, stateful, build, privacy, performance, and
   parity gates applicable to the parent window;
6. exact setup, isolation, commands, run limits, expected counts, assertions,
   activation witnesses, and forbidden outcomes;
7. exact accepted-test and substitute-fidelity checks;
8. exact parent-scope and successor-work negative searches;
9. exact cost, external mutation, secret, destructive, and environment policy;
10. gate invalidation and rerun policy after any correction; and
11. exact `PASS`, `CORRECTION_REQUIRED`, and `PARENT_BLOCKED` oracles; and
12. the inherited sandbox-escalation and automatic identical-recovery policy.

### 9.3 Risk-proportionate execution

Costly, stateful, integration, migration, build, packaging, or live-equivalent
gates MUST be frozen before execution and run only at the prescribed final
assessment point. They are not repeated after every file sub-window.

After a correction, the next assessment MUST rerun:

- every gate whose inputs, production path, assertion, fixture, substitute, or
  emitted artifact changed;
- every gate explicitly required by the parent window as a final frozen gate;
  and
- the complete scope, coverage-set, secret/privacy, and regression closure
  checks.

Unaffected costly gates may reuse prior evidence only when a deterministic
dependency comparison proves their complete inputs and asserted path unchanged.
That proof is recorded in `S3`; convenience is not a reuse rule.

#### 9.3.1 Sandbox privilege and automatic identical recovery

The window agent MUST copy the parent standard E8.1 policy into `S1` and `S2`.
Every otherwise-authorized local leaf check or whole-window gate MAY start with
the sandbox escalation required for local processes, localhost, a headless
browser, build output, toolchains or isolated test services. The window agent
MUST NOT stop for parent approval merely to obtain that privilege.

If a restricted attempt is proven invalidated solely by sandbox denial or
execution-channel loss, the same leaf agent or window agent, as applicable,
MAY run the identical command once under escalation without a corrective sub-
window, new integration-assessment ID or parent escalation. Before recovery it
MUST prove read-only that no matching process, workspace mutation, external
mutation, paid operation or usable acceptance result remains. It MUST preserve
the first attempt as diagnostic history and capture the recovery through final
exit and decisive output.

This is gate-transport recovery, not a failed-assessment correction. It cannot
change command arguments, selection, environment, fixtures, timeouts,
resources, oracle or write scope, and it cannot follow an observable product or
test failure. It never authorizes providers, paid calls, cloud, production,
deployment, destructive operations, commits, pushes or successor work.

### 9.4 Mandatory integration checklist

Each integration assessment MUST contain unchecked boxes equivalent to:

```markdown
- [ ] I1 Verify all listed file and corrective sub-windows were independently accepted.
- [ ] I2 Verify actual assembled changed files equal the planned file set and the planned set is contained by parent-authorized scope.
- [ ] I3 Verify complete requirement and decision traceability to current source and assertions.
- [ ] I4 Execute all frozen applicable whole-window gates with activation witnesses.
- [ ] I5 Verify required = registered = executed coverage-case sets, matching digests, and zero skips/duplicates/unexpected IDs.
- [ ] I6 Execute required negative controls and verify acceptance fails under each prescribed defect.
- [ ] I7 Verify substitute fidelity and accepted-test/fixture integrity.
- [ ] I8 Verify no prohibited, successor, external, destructive, secret-bearing, or out-of-scope action occurred.
- [ ] I9 Independently inspect current source and complete diff; do not rely on leaf summaries.
- [ ] I10 Record PASS, CORRECTION_REQUIRED, or PARENT_BLOCKED with decisive evidence.
```

### 9.5 Failed assessment

For every failed assertion, the window agent must first record:

- exact observed failure;
- expected result;
- activation evidence;
- causal production path;
- root-cause file or unresolved cross-file decision;
- requirements and decisions governing the remedy;
- evidence and gates invalidated; and
- why the issue is correctable within parent scope or must be escalated.

A proven environment-invalidated attempt governed by Section 9.3.1 is not a
failed assertion and does not enter this correction path. Record it and perform
the one identical recovery instead.

If correctable, create the minimum ordered set of one-file corrective
sub-windows. “Fix integration,” “make tests pass,” or assigning multiple files
to one agent is prohibited.

### 9.6 Successful assessment

The window agent may approve the assembled window only when:

- the latest integration assessment is `PASS`;
- no corrective sub-window remains unreviewed;
- every earlier failed assessment is explicitly superseded, not erased;
- current source and evidence match the latest file digests;
- parent-window acceptance requirements are all satisfied;
- no parent-level decision or authorization was invented; and
- the window handoff certificate in Section 12 is complete.

Window-agent approval means `READY_FOR_PARENT_REVIEW`, not parent acceptance or
project completion.

## 10. Correction loop

The correction loop is append-only:

```text
failed evidence
  -> diagnosis
  -> one-file corrective sub-window(s)
  -> independent window-agent review of each
  -> new whole-window integration assessment
  -> pass or repeat
```

Rules:

1. Never reuse an initial, correction, assessment, assignment, or evidence ID.
2. Never edit a completed sub-window specification to match later code.
3. Never allow a corrective agent to edit the test and production file
   together.
4. Never weaken an accepted oracle merely because current code fails it.
5. Never replace root-cause diagnosis with a timeout, retry, resource, fixture,
   or mock change unless the parent decision already prescribes that remedy and
   evidence proves the cause.
   This does not prohibit the unchanged identical sandbox recovery in Section
   9.3.1, which changes none of those inputs.
6. Every corrective edit invalidates all evidence whose inputs or asserted path
   include that file.
7. Every correction records a new baseline and ending file digest.
8. The window agent always performs a new integration assessment after the last
   correction; leaf test results cannot substitute for it.
9. There is no limit on corrective sub-window count, but unresolved repetition
   of the same parent-level ambiguity is a blocker, not permission to guess.

## 11. Mandatory decomposition-readiness checklist

These checkboxes MUST be copied into `S1` and completed with resolvable `S3`
evidence before the parent may approve leaf execution. `N/A` requires evidence
proving non-applicability.

### 11.1 Authority and inheritance

- [ ] `SW-A01` Parent assignment, window agent identity, and delegation authority are exact and current. Evidence: ___
- [ ] `SW-A02` Parent and sub-window standards plus contract, decision, checklist, and state revisions are pinned and verified. Evidence: ___
- [ ] `SW-A03` Parent write, read, action, prohibition, successor, and stop boundaries are copied without expansion. Evidence: ___
- [ ] `SW-A04` Current repositories, dirty state, and owner-controlled changes are inventoried. Evidence: ___
- [ ] `SW-A05` All three subordinate artifacts exist and their authorities do not overlap. Evidence: ___
- [ ] `SW-A06` Strict adjacent communication and no subagent delegation are enforced. Evidence: ___
- [ ] `SW-A07` The inherited execution-environment policy permits sandbox escalation for authorized local actions without expanding parent authority. Evidence: ___

### 11.2 Decision and file-set closure

- [ ] `SW-D01` Every parent requirement, invariant, decision, task, scenario, and coverage case is allocated to exact files and assertions. Evidence: ___
- [ ] `SW-D02` No missing parent-level decision or contradictory authority remains. Evidence: ___
- [ ] `SW-D03` Required changed-file set equals planned initial file set. Evidence: ___
- [ ] `SW-D04` Every planned file has one initial sub-window and no initial sub-window owns more than one file. Evidence: ___
- [ ] `SW-D05` Every file operation, starting digest, anchor, interface, preserved behavior, and forbidden edit is exact. Evidence: ___
- [ ] `SW-D06` The dependency graph is complete, sequential, acyclic, and justified by named outputs. Evidence: ___
- [ ] `SW-D07` Every cross-file interface is frozen before dependent execution. Evidence: ___
- [ ] `SW-D08` Every intermediate state has exact permitted checks, expected temporary failures, safety, resolver, and prohibitions. Evidence: ___
- [ ] `SW-D09` Separate production, test, fixture, schema, configuration, manifest, and generated files have separate sub-windows. Evidence: ___
- [ ] `SW-D10` No rename, multi-output generator, formatter, installer, or command can violate the one-file write invariant. Evidence: ___

### 11.3 Sub-window execution completeness

- [ ] `SW-E01` Every file sub-window contains every field in Section 7. Evidence: ___
- [ ] `SW-E02` Every sub-window prescribes exact ordered edits rather than design alternatives or broad verbs. Evidence: ___
- [ ] `SW-E03` Every sub-window has exact preflight, local checks, activation witnesses, assertions, and forbidden outcomes. Evidence: ___
- [ ] `SW-E04` Every sub-window mechanically proves its attributable changed-file set is exactly one file. Evidence: ___
- [ ] `SW-E05` Every sub-window has exact evidence, handoff, stop, and successor-reservation rules. Evidence: ___
- [ ] `SW-E06` Each subagent may report only to the window agent and cannot update subordinate or parent authority artifacts. Evidence: ___
- [ ] `SW-E07` No sub-window requires successor work to satisfy its file-local acceptance. Evidence: ___
- [ ] `SW-E08` Deliberately deferred checks name the exact integration assessment that owns them. Evidence: ___

### 11.4 Enforcement and integration closure

- [ ] `SW-V01` Coverage cases are allocated to exact test files, registrations, activation witnesses, and assertions. Evidence: ___
- [ ] `SW-V02` Required local and whole-window case-set equality and digest checks are prescribed. Evidence: ___
- [ ] `SW-V03` Every critical invariant has a negative control assigned at the narrowest effective level. Evidence: ___
- [ ] `SW-V04` Test substitutes and accepted tests/fixtures have exact fidelity and invalidation rules. Evidence: ___
- [ ] `SW-V05` The initial integration assessment is fully authored with zero implementation-file write authority. Evidence: ___
- [ ] `SW-V06` Frozen gates are exact, risk-proportionate, and scheduled at the final assessment rather than every leaf. Evidence: ___
- [ ] `SW-V07` Correction diagnosis, one-file corrective assignment, invalidation, and reassessment rules are complete. Evidence: ___
- [ ] `SW-V08` The window agent must independently inspect every file handoff and personally execute every integration assessment. Evidence: ___
- [ ] `SW-V09` Whole-window approval cannot pass through zero-work, skipped, filtered, duplicate, unexpected, unactivated, or summary-only evidence. Evidence: ___
- [ ] `SW-V10` Parent handoff contents and `READY_FOR_PARENT_REVIEW` boundary are exact. Evidence: ___
- [ ] `SW-V11` Every local gate distinguishes real failure from proven sandbox/channel invalidation and permits one identical escalated recovery without parent round trip. Evidence: ___

### 11.5 Mechanical and adversarial audit

- [ ] `SW-R01` All IDs are unique and all references resolve. Evidence: ___
- [ ] `SW-R02` No unresolved placeholder exists in a checked item or assignable sub-window. Evidence: ___
- [ ] `SW-R03` Single-file write-set lint rejects zero, two, wildcard, directory, rename, and incidental workspace outputs for file sub-windows. Evidence: ___
- [ ] `SW-R04` Removing one required file or requirement-to-file mapping makes readiness fail. Evidence: ___
- [ ] `SW-R05` Removing, duplicating, skipping, filtering, or bypassing one required coverage case makes acceptance fail. Evidence: ___
- [ ] `SW-R06` Weakening an oracle or diverging a substitute invalidates acceptance evidence. Evidence: ___
- [ ] `SW-R07` Simulated second-file edit and direct parent communication are rejected. Evidence: ___
- [ ] `SW-R08` Simulated integration failure cannot be repaired by the window agent without a new corrective sub-window. Evidence: ___
- [ ] `SW-R09` Parent decomposition review is recorded before the first implementation assignment. Evidence: ___
- [ ] `SW-R10` Document lint reports zero missing fields, mappings, cases, evidence references, or authority conflicts. Evidence: ___
- [ ] `SW-R11` Simulated sandbox denial proceeds to one identical escalated recovery, while a changed command, observable test failure or external action is rejected. Evidence: ___

## 12. Certificates and handoff

### 12.1 Decomposition readiness certificate

After completing Section 11, the window agent appends this certificate to `S3`
and sets `S2.decomposition_status` to
`AWAITING_PARENT_DECOMPOSITION_REVIEW`:

```yaml
certificate: SUBWINDOW-DECOMPOSITION-READY
parent_window_id: W1
parent_assignment_id: ASG-W1
window_agent_identity: exact identity
revisions:
  parent_standard: sha256
  subwindow_standard: sha256
  contract: sha256
  decision: sha256
  parent_checklist: sha256
  decomposition: sha256
initial_subwindow_ids: []
initial_subwindow_count: exact integer
planned_file_set: []
planned_file_set_digest: sha256
unmapped_parent_requirements: []
unmapped_parent_decisions: []
unmapped_parent_tasks: []
unmapped_coverage_cases: []
duplicate_initial_file_owners: []
multi_file_subwindows: []
unresolved_interfaces: []
unresolved_intermediate_states: []
unresolved_execution_choices: []
unresolved_evidence_references: []
mandatory_authoring_items_checked: exact integer
mandatory_authoring_items_unchecked: 0
first_subwindow: exact ID
integration_assessment_id: exact ID
parent_review_required: true
```

The parent reviews the decomposition against the parent window. Only the window
agent may convert a parent approval into `S2.decomposition_status: READY` and
assign the first sub-window. Parent approval does not authorize the parent to
communicate directly with subagents.

### 12.2 Corrective-subwindow readiness certificate

Before assigning any corrective sub-window, the window agent appends:

```yaml
certificate: CORRECTIVE-SUBWINDOW-READY
parent_window_id: W1
corrective_subwindow_id: W1-C001
window_agent_identity: exact identity
trigger_evidence: []
root_cause: exact causal claim
governing_parent_requirements: []
governing_parent_decisions: []
corrected_prior_subwindows: []
writable_file: exact path
starting_file_digest: sha256 | ABSENT
predecessors: []
invalidated_evidence: []
invalidated_gates: []
unresolved_parent_decisions: []
expanded_parent_scope_required: false
section_7_fields_complete: true
single_file_write_set: true
unresolved_execution_choices: []
next_integration_assessment_id: exact ID
status: READY
```

Any unresolved parent decision, required scope expansion, incomplete Section 7
field, or non-single-file remedy prohibits assignment and requires parent
escalation.

### 12.3 File-subwindow execution certificate

Every implementation subagent returns:

```yaml
certificate: FILE-SUBWINDOW-EXECUTED
parent_window_id: W1
subwindow_id: W1-S001
assignment_id: ASG-W1-S001
agent_identity: exact identity
writable_file: exact path
starting_file_digest: sha256 | ABSENT
ending_file_digest: sha256 | ABSENT
starting_repository_change_set_digest: sha256
attributable_changed_file_set: [exact path]
required_local_cases: []
registered_local_cases: []
executed_local_cases: []
skipped_local_cases: []
duplicate_case_ids: []
unexpected_case_ids: []
missing_activation_witnesses: []
negative_controls_expected: exact integer
negative_controls_falsified: exact integer
commands: []
deferred_integration_checks: []
external_mutations: []
prohibited_actions_observed: []
successor_work_started: false
direct_parent_communication: false
status: AWAITING_WINDOW_REVIEW
```

The window agent appends a separate review disposition to `S3`. The subagent
cannot self-accept.

### 12.4 Window-agent integration certificate

After a successful integration assessment, the window agent appends:

```yaml
certificate: WINDOW-AGENT-INTEGRATION-PASS
parent_window_id: W1
integration_assessment_id: W1-I001
window_agent_identity: exact identity
accepted_initial_subwindows: []
accepted_corrective_subwindows: []
superseded_failed_assessments: []
expected_changed_file_set: []
actual_changed_file_set: []
expected_changed_file_set_digest: sha256
actual_changed_file_set_digest: sha256
required_case_count: exact integer
registered_case_count: exact integer
executed_case_count: exact integer
required_case_set_digest: sha256
registered_case_set_digest: sha256
executed_case_set_digest: sha256
skipped_required_cases: []
duplicate_case_ids: []
unexpected_case_ids: []
missing_activation_witnesses: []
oracle_failures: []
negative_controls_expected: exact integer
negative_controls_falsified: exact integer
substitute_fidelity_failures: []
accepted_evidence_invalidations_unresolved: []
commands_and_outcomes: []
environment_invalidations_and_identical_recoveries: []
gates_reused_with_dependency_proof: []
prohibited_actions_observed: []
successor_parent_window_work_started: false
residual_parent_review_items: []
status: READY_FOR_PARENT_REVIEW
```

### 12.5 Consolidated parent handoff

The window agent sends the parent only a consolidated report containing:

1. `READY_FOR_PARENT_REVIEW` or one exact blocker;
2. `S1`, `S2`, and `S3` paths and revisions;
3. initial, corrective, failed-assessment, and successful-assessment IDs;
4. expected and actual changed-file sets and digests;
5. current file digests;
6. requirement, decision, task, scenario, and coverage trace closure;
7. exact required, registered, and executed coverage counts and digests;
8. skipped, duplicate, unexpected, unactivated, and failed cases;
9. exact commands, decisive outcomes, negative controls, and parity limits;
10. evidence invalidated and superseded during correction;
11. external mutations, costs, skipped gates, residual risks, and user
    prerequisites; and
12. confirmation that no successor parent window began.

Subagent summaries are not forwarded as proof. Their certificates remain
resolvable in `S3`, and the window agent's independent review and integration
certificate are the handoff claims.

## 13. Parent review boundary

The parent independently verifies the parent-window contract, current source,
complete diff, window-agent integration certificate, enforcement evidence, and
scope closure. It may return findings only to the window agent.

If the finding is governed by an existing parent decision and remains within
the same parent-window scope, the window agent appends new one-file corrective
sub-windows and a new integration assessment. The parent does not author those
sub-windows.

If the finding exposes a missing or changed parent decision, contract revision,
or expanded authority, the parent applies the parent standard's correction
protocol before reassigning the window agent.

Only parent acceptance permits movement to the next parent window. Window-agent
approval alone does not authorize it.

## 14. Mandatory self-falsification

Before declaring a decomposition ready, the window agent MUST demonstrate that
its document and state rules reject each applicable counterexample:

1. a sub-window names two writable files;
2. a sub-window names a directory or wildcard;
3. a command creates an unplanned second workspace file;
4. a source and separate test file are assigned together;
5. a required parent file is absent from the decomposition;
6. two initial sub-windows own the same file;
7. a dependent file begins before its interface is frozen;
8. an intermediate state has an unexplained test failure;
9. a subagent starts its successor;
10. a subagent communicates directly with the parent;
11. the window agent repairs implementation during review;
12. an integration failure produces no diagnosed one-file correction;
13. a correction silently rewrites a completed sub-window;
14. integration acceptance omits, skips, duplicates, filters, or fails to
    activate a required coverage case;
15. an oracle is weakened to accommodate current behavior;
16. a test substitute proves more parity than its fidelity supports;
17. a costly gate is repeated without its prescribed scheduling or invalidation
    rule;
18. a correction changes a file but dependent evidence is reused without proof;
19. the assembled changed-file set differs from the planned set or the planned
    set exceeds parent-authorized scope; or
20. the window agent claims parent acceptance or begins the next parent window;
21. an already-authorized local gate is escalated to the parent merely because
    sandbox privilege is required; or
22. a changed command, observable assertion failure, surviving process,
    workspace/external mutation or external action is accepted as automatic
    sandbox recovery.

If any counterexample can still produce a passing readiness or handoff
certificate, the standard has not been applied correctly and the decomposition
remains `DRAFT / NOT ASSIGNABLE`.

## 15. Mandatory window-agent authoring report

After authoring, report only:

1. `AWAITING_PARENT_DECOMPOSITION_REVIEW` or `BLOCKED`;
2. the three subordinate artifact paths and revisions;
3. parent window and assignment IDs;
4. initial sub-window count and exact ordered IDs;
5. exact planned changed-file set and digest;
6. unmapped requirement, decision, task, scenario, and coverage counts;
7. multi-file sub-window and duplicate-file-owner counts;
8. unresolved interface, intermediate-state, execution-choice, and evidence
   counts;
9. mandatory authoring checklist checked and unchecked counts;
10. initial integration-assessment ID and frozen gate summary;
11. predictable external, stateful, costly, or requester gates; and
12. one concrete blocker when status is `BLOCKED`.

Do not begin implementation while decomposition awaits parent review. Do not
replace these exact closure results with a narrative confidence claim.
