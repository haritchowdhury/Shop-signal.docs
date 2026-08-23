# KI-W6 Sub-Window Decomposition Checklist (`S1`, superseding revision)

This file supersedes, in full and by replacement, the state-108 decomposition
(authored under `ASG-KI-W6-WA-01`, starting revision
`a0e3e28b7d9e272cfa6b1eec79f224d2b156725d7ebc86b729bfe3067dd42d87`) under
assignment `ASG-KI-W6-WA-14` (authored at A5 state 184 and approved for
dispatch at A5 state 185). The superseded two-leaf
`KI-W6-S001/S002` decomposition never became executable authority: its parent
acceptance is absent and A5 state 183's continuation was itself superseded by
`SRC-KI-055` and `DEC-KI-053`. Nothing in the superseded text grants authority
here. This replacement is the fifteenth KI-W6 corrective sequence
(`KI-W6-CLOCK-TXN-CLOSURE`): nine one-file leaves `KI-W6-C136`–`KI-W6-C144`
in two explicitly authorized parallel waves, then window-agent-only
integration assessment `KI-W6-I119`, decomposing parent tasks `KI-W6-CT20`
through `KI-W6-CT23`. The historical reauthored decomposition
(`KEYWORD_INTELLIGENCE_KI_W6_REAUTHORED_SUBWINDOW_CHECKLIST.md`, revision
`86b56ecaa579da2e4ec305c7c4800bbfb7b2666489dd9ceab72ca8ef0f11bc57`) remains
read-only history. This file records no execution status (`S2`) and no
evidence (`S3`); those are
`KEYWORD_INTELLIGENCE_KI_W6_TRANSACTION_CLOCK_SUBWINDOW_STATE.md` and
`KEYWORD_INTELLIGENCE_KI_W6_TRANSACTION_CLOCK_SUBWINDOW_EVIDENCE.md`.

Once the parent accepts this decomposition, its sub-window blocks are
immutable; corrections are appended under new `KI-W6-C145+` IDs.

## 0. Inherited authority and revision pins

```yaml
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-14
window_agent_identity: KI-W6-WINDOW-AGENT
parent_standard_path: PROJECT_AGNOSTIC_DECISION_COMPLETE_CHECKLIST_AUTHORING_STANDARD.md
parent_standard_revision: cda352017e75c0d11f6797d9fbe108b4365508cd38b0e92365cfb523ede32848
subwindow_standard_path: PROJECT_AGNOSTIC_WINDOW_AGENT_SUBWINDOW_AUTHORING_STANDARD.md
subwindow_standard_revision: 842c29550c06c22d63e0a058a27cb8a9ff6b538b3168d2c83a384890b44247f0
contract_path: KEYWORD_INTELLIGENCE_PRODUCT_CONTRACT.md
contract_revision: 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c
decision_path: KEYWORD_INTELLIGENCE_DECISION_LEDGER.md
decision_revision: 2b2d75b9ebb94ae80d3cc7241ce69a2aa92a22efa755b1497887018950ccf406
parent_checklist_path: KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md
parent_checklist_revision: 679e9a7d986775d60fa9f2a9b7cd9568084652534c857f7109482426653b1d36
parent_active_state_path: ACTIVE_EXECUTION_STATE.md
parent_active_state_revision: state 185 (parent decomposition-approval block; pins above verified byte-equal)
superseded_s1_starting_revision: a0e3e28b7d9e272cfa6b1eec79f224d2b156725d7ebc86b729bfe3067dd42d87
trigger_evidence: [SRC-KI-055, EV-KI-A-110]
governing_decisions: [DEC-KI-051, DEC-KI-052, DEC-KI-053]
```

All six authoring pins were recomputed and verified byte-equal against A5
state 184 before authoring (recorded in S3 `EV-KI-W6-TC01`). The corrected S1
was independently approved and pinned by the parent at A5 state 185
(`EV-KI-W6-TC03`). A revision mismatch at dispatch time blocks assignment.

Scenario authority: this sequence implements the parent's supplemental
`SCN-KI-044` (complete clock/profile/round-trip closure) and preserves
`SCN-KI-018` as the unchanged causal flow executed by `KI-W6-I119`'s
`KI-W6-CV87` gate.

### 0.1 Recorded mechanical interpretations (all cite locked decisions; none delegates a choice)

1. **Statement-ceiling baseline.** CT20 item 5 requires that claim/renew/
   terminal/aggregation database statement ceilings "not increase from the
   post-consolidation baseline recorded by `C141`". `C141`'s dynamic spies
   therefore record per-method transaction-internal operation counts
   (raw-query locks, delegate reads, writes) into their activation witnesses;
   `KI-W6-CV86` enforces the frozen ceilings. This allocates the parent's
   recording duty to `C141` and its enforcement duty to `I119`; it changes no
   behavior. Governing text: CT20 items 5/7.
2. **Occurrence-count arithmetic for the frozen constants.** After `C136`, the
   coordinator file contains exactly twelve `PIPELINE_TRANSACTION_OPTIONS`
   tokens (one definition plus eleven usages). After `C137`, the run
   repository contains exactly twenty-two `AWS_PIPELINE_TRANSACTION_OPTIONS`
   tokens (one definition plus twenty-one usages) and exactly one surviving
   inline `{ maxWait: 5_000, timeout: 30_000 }` — the `DEC-KI-051`
   `saveQueryValidation` profile, which CT21 item 4 forbids modifying.
   `C142` asserts these exact counts. Governing text: DEC-KI-053 transaction
   profile; CT21 item 4.
3. **Five-method integration coverage shape.** CT23 item 5's "five-method
   final/lead/domain contract through direct or service activation" is
   implemented by one new disposable-schema test in `C144` that registers
   three zero-task stages (discovery, lead, traffic_crux), claims each
   aggregator at a controlled inside-lease instant, and drives the five
   instrumented readers with zero-candidate inputs (`domains: []`,
   `selections: []`, `candidates: []`), asserting missing/invalid-now
   pre-transaction rejection with zero writes, expired-lease
   `PIPELINE_LEASE_LOST`, and inside-lease success. Zero-candidate inputs are
   the minimal members already accepted by each method's strict input
   validation (the existing `G10`/`G12` tests use the same shapes). Governing
   text: CT23 item 5; DEC-KI-053 clock interface.
4. **`C143` reuse-input refactor.** The existing direct
   `readAwsReusableProfiles` call's input object is extracted verbatim into a
   `reuseInput` const so the new rejection assertions reuse identical
   literals; no existing assertion is weakened or removed. Governing text:
   CT23 item 4.
5. **Line anchors.** Line numbers cited below are authoring-time witnesses
   into the pinned starting digests. Where a line number and the pinned digest
   disagree, the digest governs and the leaf stops for re-verification.
6. **`readAwsReuseInputs` `evaluatedAt` coupling.** The domain reader rejects
   unless `input.evaluatedAt` equals the locked stage row's `createdAt`
   (prisma-run-repository.js:1549–1550). The `C144` discovery-leg uses the
   registered stage's returned `createdAt` as `evaluatedAt`. This is existing
   locked behavior, not a new decision.

## 1. Parent-window scope and exclusions (copied unexpanded)

- Write scope: exactly the nine files of §3, each owned by exactly one leaf.
  The window agent writes only the three coordination artifacts named in the
  header. No other workspace file may be created or edited by any leaf or by
  the window agent during this sequence.
- Read-only scope: all application source and tests in `email_scraper/`; the
  accepted W1–W6 outputs, fixtures, and harnesses; parent artifacts A1–A8;
  the historical reauthored S1–S3; the superseded S1.
- Authorized actions: local source/test edits, `node --check`, focused
  `node --test` runs, isolated test-database writes
  (`test/helpers/isolated-postgres.js` only, D2A) behind
  `ALLOW_DATABASE_TESTS=true` with a non-production `TEST_DATABASE_URL`, the
  one causal browser command of `KI-W6-CV87`, local builds, read-only source
  audits, evidence updates, sandbox escalation for these local actions with
  the inherited E8.1 identical-recovery rule (recovery limit 1 per invalidated
  execution).
- Prohibited: provider calls, AWS operations, production database writes,
  schema/migration changes, package/config changes, algorithm or feature
  changes, lease-duration/heartbeat/retry/batching changes, unrelated cleanup,
  commits or pushes (requester-only), any `KI-W7` work, any edit to the
  historical reauthored or superseded decompositions, any edit to A1–A8 by a
  leaf.
- Successor: `STOP_FOR_PARENT_REVIEW`; `may_start_successor: false` everywhere.

## 2. Starting working-tree inventory (recorded without modification, 2026-08-23)

- Backend repository clean at HEAD `173a015`; frontend repository clean at
  HEAD `f981b34`; both verified by empty `git status --porcelain` this
  session.
- Root: `git status --porcelain | LC_ALL=C sort` lists exactly the eight
  owner-controlled coordination documents (`ACTIVE_EXECUTION_STATE.md`,
  `KEYWORD_INTELLIGENCE_DECISION_LEDGER.md`,
  `KEYWORD_INTELLIGENCE_DISCOVERY_DOSSIER.md`,
  `KEYWORD_INTELLIGENCE_EXECUTION_EVIDENCE.md`,
  `KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md`,
  `KEYWORD_INTELLIGENCE_SPECIFICATION_CHANGELOG.md`,
  `KEYWORD_INTELLIGENCE_TRACEABILITY_INDEX.md`,
  `PROJECT_AGNOSTIC_WINDOW_AGENT_SUBWINDOW_AUTHORING_STANDARD.md`); the
  authoritative per-LF sorted-porcelain digest is
  `565d9fb141c12fc6c056f259745965c450c65088acb62ade9c81d0193c022860`.
  The only additional root changes during this sequence are this window's
  three subordinate artifacts (this S1, S2, S3).
- All nine planned files exist with the pinned §3 digests except
  `email_scraper/test/aws-pipeline-transaction-clock-enforcement.test.js`,
  which is `ABSENT` (verified).
- The five production starting digests equal the accepted finals of
  `KI-W6-C131`–`KI-W6-C134` and the post-I118 coordinator state recorded by
  `SRC-KI-055` (coordinator `e285557a…`).

## 3. Planned file set, DAG, waves, intermediate states, interface freeze

### 3.1 Planned file set (the complete required changed-file set)

| # | Path | Operation | Starting SHA-256 | Leaf | Wave |
|---|---|---|---|---|---|
| 1 | `email_scraper/src/aws-pipeline/repositories/pipeline-coordinator-repository.js` | MODIFY | `e285557a5dc854d0021bb71e19076d8bff6ce4e161b9ce8621acda9c24e549c4` | `KI-W6-C136` | 1 |
| 2 | `email_scraper/src/prisma-run-repository.js` | MODIFY | `54d5f422431ec1914855b2ae5cc07ff30e9ab428f11601a7703d589ee21cef13` | `KI-W6-C137` | 1 |
| 3 | `email_scraper/src/aws-pipeline/services/domain-aggregator.js` | MODIFY | `e873bb622c085ea34e69e3658f21dacd36d068765f821782dfc613009f3199ce` | `KI-W6-C138` | 1 |
| 4 | `email_scraper/src/aws-pipeline/services/lead-aggregator.js` | MODIFY | `c3f2fb24576f43e6c046a87573e6e0942b9263d39c2002eec152280365cde38c` | `KI-W6-C139` | 1 |
| 5 | `email_scraper/src/aws-pipeline/services/final-aggregator.js` | MODIFY | `416e36feeb35aedd571ae8863a413550215263a157a99ed8cf519722446f9683` | `KI-W6-C140` | 1 |
| 6 | `email_scraper/test/pipeline-coordinator-repository.test.js` | MODIFY | `ee2f14da06e171d876c926cf2fde0f259a62dcf477f0d6873e8294d49bdb5533` | `KI-W6-C141` | 2 |
| 7 | `email_scraper/test/aws-pipeline-transaction-clock-enforcement.test.js` | CREATE | `ABSENT` | `KI-W6-C142` | 2 |
| 8 | `email_scraper/test/aws-pipeline-lead-aggregation.integration.test.js` | MODIFY | `102cac9694251ea5dedb40bcf44a07b771f26440202b5c81a3c5f33b98630238` | `KI-W6-C143` | 2 |
| 9 | `email_scraper/test/aws-pipeline-final.integration.test.js` | MODIFY | `22b70d3111ea65d0e24fe9d5e82d4c03e8fe84c6b80e076335e919edd0e0e664` | `KI-W6-C144` | 2 |

Sorted-member-plus-LF nine-path digest (§4 method):
`ba4ccba7b65016b486dc2e1160bcc11a2cb08d306aff4945fad0022e3f19ad92`
(recomputed this session; matches the parent pin). Required changed-file set =
planned set = files owned by this sequence's leaves; each file has exactly one
owner; no tenth file is authorized.

### 3.2 DAG and parallel waves

```text
KI-W6-WAVE-1 (parallel, five production leaves, disjoint files/commands/resources):
  KI-W6-C136  KI-W6-C137  KI-W6-C138  KI-W6-C139  KI-W6-C140
      | (barrier: every wave-1 member independently ACCEPTED by the window agent)
KI-W6-WAVE-2 (parallel, four test leaves, disjoint files/commands/resources):
  KI-W6-C141  KI-W6-C142  KI-W6-C143  KI-W6-C144
      | (barrier: every wave-2 member independently ACCEPTED)
KI-W6-I119 (window-agent-only, sequential, zero implementation-write authority)
      -> READY_FOR_PARENT_REVIEW -> stop before KI-W7
```

Wave conformance proofs (sub-window standard §5.4): every member owns one
distinct canonical file and assignment ID; no member consumes an output,
interface, generated artifact, fixture, database schema, port, or process
owned by another member (wave 1 edits five disjoint production files whose
consumed interfaces are already frozen by §3.4; wave 2 edits four disjoint
test files, each reading only frozen wave-1 outputs plus existing fixtures);
every cross-file interface consumed by either wave is frozen in §3.4 before
dispatch; each member's commands write only its own file plus authorized
disposable runtime state (per-leaf uniquely-named disposable schemas for
`C143`/`C144`, `/tmp` scratch for `C142` if needed); `S2.active_subwindows`
records the whole wave before any member begins; each member reports only to
the window agent and stops at `AWAITING_WINDOW_REVIEW`; a failed or blocked
member prevents the next wave. File disjointness alone creates no parallel
authority beyond these two named waves (DEC-KI-053; revised sub-window
standard).

### 3.3 Intermediate-state contract

- **After wave 1, before wave 2:** the five production files carry the frozen
  §3.4 interfaces; behavior is closed under the existing harness `pinDates`
  seam (services now pass real boundary clocks that `pinDates` substitution
  controls). Local checks that must already pass: each leaf's `node --check`
  and diff proof. Whole-window checks expected pending: every test assertion
  of wave 2 (not yet authored/executed) and all `I119` gates. One expected
  temporary state is exact and safe: `test/pipeline-coordinator-repository.test.js`
  still passes unchanged (its unit fakes bypass raw SQL delegates only where
  `registerStageInTransaction` is driven directly; the locked-row
  consolidation does not alter that test's transaction fakes), while the
  integration suites are not yet re-run — nothing is externally visible, no
  provider/AWS/production surface exists, and wave 2 plus `I119` resolve the
  pending proof. While this state exists: no commit, no `npm test` claim, no
  parent handoff, no KI-W7 work.
- **After `C141`, before `C142`/`C143`/`C144`:** coordinator unit coverage
  (profiles, locked-row consolidation, no-reload) is green locally; the
  remaining three test files are still pending. Same prohibitions.
- **After each wave-2 member:** its local suite is green; the other members
  may still be pending; only `I119` assembles the window.
- **After `I119` PASS:** state is `READY_FOR_PARENT_REVIEW`; no successor
  work; requester performs any commit.

### 3.4 Interface freeze (before first dependent execution)

1. **Coordinator constant (C136 output):** module-private
   `const PIPELINE_TRANSACTION_OPTIONS = Object.freeze({ maxWait: 5_000, timeout: 30_000 });`
   — byte-equivalent literal; passed as the second `$transaction` argument in
   exactly the eleven methods of §5.1.
2. **Run-repository constant (C137 output):** module-private
   `const AWS_PIPELINE_TRANSACTION_OPTIONS = Object.freeze({ maxWait: 5_000, timeout: 30_000 });`
   — passed as the second `$transaction` argument in exactly the twenty-one
   methods of §5.2; `saveQueryValidation`'s existing inline equal object
   (`DEC-KI-051`) is untouched; `renewAwsRunLease` remains one atomic
   `updateMany` (never a `$transaction`).
3. **Clock validator (C137 output):** module-private
   `requireAwsPipelineNow(now)` returning `now` only when
   `now instanceof Date && Number.isFinite(now.getTime())`, otherwise
   throwing `PipelineInvariantError("PIPELINE_INPUT_CONFLICT")`.
4. **Five reader signatures (C137 output):** `readAwsReuseInputs(input, now)`,
   `readAwsReusableProfiles(input, now)`, `readAwsFinalReuseRows(input, now)`,
   `readAwsAmbiguousDataForSeoTargets(input, now)`,
   `readAwsTerminalCruxBigQueryWork(input, now)` — required second argument,
   no default, validated before the transaction opens, validated value passed
   to `assertCompleteAggregatorInTransaction`; `evaluatedAt` remains a
   distinct durable manifest timestamp (never substituted for lease time).
5. **Five service callers (C138–C140 output):** exactly one
   `readAwsReuseInputs` call in `domain-aggregator.js`, one
   `readAwsReusableProfiles` call in `lead-aggregator.js`, and
   `readAwsAmbiguousDataForSeoTargets`, `readAwsTerminalCruxBigQueryWork`,
   `readAwsFinalReuseRows` calls in `final-aggregator.js`, each appending
   `new Date()` as the second argument with argument one byte-equivalent;
   call position relative to artifact reads, ownership, materialization,
   ledger construction, and publication unchanged.
6. **Locked-row helpers (C136 output):** `lockedTask`, `lockedStage`,
   `lockedRun` each execute one schema-scoped `SELECT * ... FOR UPDATE`,
   require exactly one row, and return that raw row; no follow-up
   `findUnique`. `recordDispatch` locks all stage tasks once with one ordered
   `SELECT * ... FOR UPDATE`, proves cardinality and requested-item existence
   from those rows, then performs its existing single `updateMany` returning
   `{ count }`; lock order (tasks then stage), state predicates, fencing,
   public return shapes, and write cardinalities unchanged.
7. **Public surface:** no exported symbol, schema, payload, queue, artifact,
   cost, lease-duration, heartbeat, retry, or provider-facing interface
   changes anywhere in the nine files.

## 4. Digest method (authoritative for every set digest in this window)

Lowercase SHA-256; members UTF-8-encoded; distinct; sorted by unsigned UTF-8
byte order (`LC_ALL=C`); each member followed by exactly one LF; hashed over
the concatenated bytes. File digests are over exact raw bytes; a missing path
is the literal token `ABSENT`. Frozen sets for this sequence:

- nine-path planned set: `ba4ccba7b65016b486dc2e1160bcc11a2cb08d306aff4945fad0022e3f19ad92`
- new required cases `[W6-DB-08, W6-DB-09, W6-DB-10, W6-DB-11]`:
  `e8bd1b4a3b3deb8f853eac0e8bcea5609278177945389f292b1b12a7309bf030`
- new controls `[W6-NC-18, W6-NC-19, W6-NC-20]`:
  `89e40c02b11dd426c8445de018a9d85fa2c110b6da9728cee8dff4e3cc31db1b`
- final W6 39-case union:
  `f8137d25f5994cc83e4ec1deaa672656d50f19692a5907b10e47399a78c6dd80`
- final W6 20-control union:
  `0cbaad071c1bc474102394ddc0082d61f0c366d67768dcab0eafa7b5f6a3fc88`

All four were recomputed this session and match `DEC-KI-053`/the parent
checklist (S3 `EV-KI-W6-TC01`).

## 5. Sub-window blocks

Semantics common to every block: the recorded
`starting_repository_change_set_digest` is the authoring-time root porcelain
set digest
`565d9fb141c12fc6c056f259745965c450c65088acb62ade9c81d0193c022860` (§4
method over sorted porcelain lines); leaf preflight (P2) instead proves both
nested repositories clean at their pinned HEADs (`173a015`, `f981b34`) or
containing exactly the accepted same-wave-independent predecessor endings,
and the eight-line owner-controlled root core set unchanged (the three
subordinate artifacts of this window may additionally appear). Every leaf
reads the parent artifacts and its named read scope before editing. Every
leaf reports the exact §12.3 certificate and stops at
`AWAITING_WINDOW_REVIEW`. The `prohibited_actions` list of every block is
exactly: edit any second file; edit the three coordination artifacts or any
parent artifact; start the successor, another leaf, or any later sub-window;
communicate with the parent agent; mutate external state (providers, AWS,
databases other than the prescribed disposable schema, queues, buckets); run
any formatter, installer, generator, or snapshot-update command; weaken any
existing test, fixture, or oracle; commit. It is not repeated per block.

### 5.1 `KI-W6-C136` — coordinator transaction profile and locked-row consolidation

```yaml
subwindow_id: KI-W6-C136
type: CORRECTION
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-14
assigned_agent: LEAF (KI-W6-C136-AGENT)
predecessors: [KI-W6-WAVE-1 dispatch]
successor_reserved_for: WINDOW-AGENT
writable_file: email_scraper/src/aws-pipeline/repositories/pipeline-coordinator-repository.js
file_operation: MODIFY
starting_file_digest: e285557a5dc854d0021bb71e19076d8bff6ce4e161b9ce8621acda9c24e549c4
starting_repository_change_set_digest: 565d9fb141c12fc6c056f259745965c450c65088acb62ade9c81d0193c022860
read_only_scope:
  - the writable file; prisma/schema.prisma (PipelineStage/PipelineTask/Run column names)
  - email_scraper/test/pipeline-coordinator-repository.test.js, test/pipeline-coordinator-repository.integration.test.js
  - DEC-KI-053; SRC-KI-055; parent checklist CT20/CT23; this S1 §3.4/§5.1; S2; S3
authorized_actions: [apply the exact transformation below to the one writable file, run node --check, run node --test test/pipeline-coordinator-repository.test.js, run a leaf-local assertion script over the resulting file and record its output, record S3 leaf evidence via the window agent]
prohibited_actions: (the common list)
may_start_successor: false
```

**Mechanical trace (§7.2).** Implements `KI-W6-CT20` items 2–6 end-to-end.
Requirements `REQ-KI-010`–`015/024`; invariants `INV-KI-004`–`006`,
`INV-KI-010/011/015`; decisions `DEC-KI-053` (profile set, read
consolidation), `DEC-KI-051` (unaffected), `DEC-KI-052` (timeout/retry
prohibition respected — no retry added); trigger `SRC-KI-055`. Verified by
`C141`/`C142`; cases `W6-DB-08`/`W6-DB-10`; controls `W6-NC-18`/`W6-NC-20`.

**Exact file transformation (§7.3).** Starting from the pinned digest
(authoring-time anchors: `requireNow` :15–18; `lockedTask` :68–74;
`lockedStage` :76–82; `lockedRun` :84–88; the eleven `$transaction` methods
`registerStage` :185, `recordDispatch` :194, `claimTask` :214 (options :242),
`renewTask` :245 (options :262), `recordTerminal` :265, `claimAggregator`
:305, `renewAggregator` :334, `getCompleteStage` :353, `completeAggregator`
:361, `listRecoverable` :371, `cancelRunGeneration` :394):

1. **Constant.** Immediately after the `UUID` const (line 9), insert exactly:
   `const PIPELINE_TRANSACTION_OPTIONS = Object.freeze({ maxWait: 5_000, timeout: 30_000 });`
2. **`lockedTask`.** Replace the whole helper with exactly:
   `async function lockedTask(transaction, taskId) {` / ``   const rows = await transaction.$queryRaw` `` +
   `    SELECT * FROM "PipelineTask" WHERE "id" = ${taskId} FOR UPDATE` /
   ``   `; `` / `  if (rows.length !== 1) conflict();` / `  return rows[0];` / `}`.
3. **`lockedStage`.** Same shape with table `"PipelineStage"` and parameter
   `stageId`.
4. **`lockedRun`.** Same shape with table `"Run"` and parameter `runId`
   (preserving the existing single-line template style is not required; the
   statement content is exactly `SELECT * FROM "Run" WHERE "id" = ${runId} FOR UPDATE`).
5. **`recordDispatch`.** Inside its transaction callback, replace the body
   from the task-lock statement through the cardinality check with exactly:
   lock all stage tasks once —
   `` const lockedTasks = await transaction.$queryRaw`SELECT * FROM "PipelineTask" WHERE "stageId" = ${stageId} ORDER BY "id" FOR UPDATE`; ``
   (multi-line template formatting as the file style); then
   `const stage = await lockedStage(transaction, stageId);`; then the
   unchanged `if (["failed", "cancelled"].includes(stage.state)) conflict("PIPELINE_CANCELLED");`;
   then `if (lockedTasks.length !== stage.expectedCount) conflict();`; then
   `const requestedItemKeys = new Set(itemKeys);` / `const requested = lockedTasks.filter((task) => requestedItemKeys.has(task.itemKey));` /
   `if (requested.length !== itemKeys.length) conflict();`; then retain the
   existing single `pipelineTask.updateMany({ where: { stageId, itemKey: { in: itemKeys } }, data: { dispatchCount: { increment: 1 }, lastDispatchedAt: now } })`
   and `return { count: updated.count };`. The existing
   `pipelineTask.findMany` line is deleted. Lock ordering (tasks before stage)
   is unchanged.
6. **Eleven transaction arguments.** In `registerStage`, `recordDispatch`,
   `recordTerminal`, `claimAggregator`, `renewAggregator`, `getCompleteStage`,
   `completeAggregator`, `listRecoverable`, and `cancelRunGeneration`, the
   closing `});` of `this.prisma.$transaction(async (transaction) => { … })`
   becomes `}, PIPELINE_TRANSACTION_OPTIONS);`. In `claimTask` (:242) and
   `renewTask` (:262), the literal second argument
   `{ maxWait: 5_000, timeout: 30_000 }` becomes `PIPELINE_TRANSACTION_OPTIONS`.
7. **Everything else byte-identical:** no schema, predicate, lease duration,
   heartbeat, return union, cancellation rule, export, validation, or
   non-inventory transaction change; `requireNow`, fencing, counters, and
   rollback untouched; no retry or external action inside any transaction.

**Exact checks (§7.4).** C1 write-set: `git -C email_scraper status
--porcelain` attributable delta is exactly the one modified file. C2
`node --check src/aws-pipeline/repositories/pipeline-coordinator-repository.js`
→ exit 0 (LOCAL_NOW). C3 `node --test test/pipeline-coordinator-repository.test.js`
→ zero failures (existing five tests unaffected by this file's edits; LOCAL_NOW).
C4 leaf-local assertion script (Node, `/tmp` scratch permitted) verifies on the
resulting file: exactly one `PIPELINE_TRANSACTION_OPTIONS` definition with the
byte-exact frozen literal; exactly eleven usages (total twelve tokens); zero
remaining inline `{ maxWait: 5_000, timeout: 30_000 }`; each of the eleven
method bodies contains `$transaction` and the constant; `lockedTask`/
`lockedStage`/`lockedRun` bodies contain `SELECT *` and `FOR UPDATE`, contain
`rows[0]`, and contain no `findUnique`; the `recordDispatch` body contains
`SELECT *`, contains no `findMany`, and retains exactly one `updateMany`;
every other top-level helper and method is byte-identical to the starting
digest's parsed form except the enumerated edits (diff-hunk audit). Controls
(on in-memory copies): (A) deleting the constant argument from `listRecoverable`
makes the eleven-usage assertion fail; (B) restoring `findUnique` inside
`lockedStage` makes the no-delegate assertion fail. C5 secrets: no credential,
token, production ID, or provider body appears or changes (file diff contains
only the enumerated hunks). All checks LOCAL_NOW except the integration
re-verification owned by `I119` (DEFERRED: `CV85`/`CV86`).

- [ ] P1 Revisions, assignment identity, writable file, baseline digest, and wave-1 dispatch evidence match.
- [ ] P2 Starting repository status and protected dirty changes match §2.
- [ ] T1 Apply every ordered transformation and no other edit to the writable file.
- [ ] V1 Run every LOCAL_NOW check and record its activation witnesses and exact assertions.
- [ ] V2 Prove the attributable workspace changed-file set is exactly the writable file.
- [ ] V3 Prove required local coverage (`W6-DB-08`/`W6-DB-10` static half) via the C4 script witnesses; registrations execute in `C142`.
- [ ] H1 Return the exact diff, ending digest, commands, outcomes, and residual integration obligations.
- [ ] H2 Confirm no prohibited action, second-file edit, successor work, external mutation, or parent communication occurred.
- [ ] H3 Stop at AWAITING_WINDOW_REVIEW.

### 5.2 `KI-W6-C137` — run-repository clock and transaction inventory

```yaml
subwindow_id: KI-W6-C137
type: CORRECTION
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-14
assigned_agent: LEAF (KI-W6-C137-AGENT)
predecessors: [KI-W6-WAVE-1 dispatch]
successor_reserved_for: WINDOW-AGENT
writable_file: email_scraper/src/prisma-run-repository.js
file_operation: MODIFY
starting_file_digest: 54d5f422431ec1914855b2ae5cc07ff30e9ab428f11601a7703d589ee21cef13
starting_repository_change_set_digest: 565d9fb141c12fc6c056f259745965c450c65088acb62ade9c81d0193c022860
read_only_scope:
  - the writable file; src/aws-pipeline/repositories/pipeline-coordinator-repository.js (assertCompleteAggregatorInTransaction import, read-only)
  - email_scraper/test/aws-pipeline-lead-aggregation.integration.test.js, test/aws-pipeline-final.integration.test.js, test/pipeline-coordinator-repository.integration.test.js
  - DEC-KI-051/052/053; SRC-KI-055; parent checklist CT21/CT22/CT23; this S1 §3.4/§5.2; S2; S3
authorized_actions: [apply the exact transformation below to the one writable file, run node --check, run a leaf-local assertion script over the resulting file and record its output, record S3 leaf evidence via the window agent]
prohibited_actions: (the common list)
may_start_successor: false
```

**Mechanical trace (§7.2).** Implements `KI-W6-CT21` items 2–7 and the
repository half of `CT22`'s frozen interface. Same requirements/invariants as
C136; decisions `DEC-KI-053` (validator, five signatures, twenty-one set),
`DEC-KI-051` (saveQueryValidation untouched), `DEC-KI-052` (no retry).
Verified by `C142`–`C144` and `I119`; cases `W6-DB-08`/`W6-DB-09`/`W6-DB-11`;
controls `W6-NC-18`/`W6-NC-19`.

**Exact file transformation (§7.3).** Authoring-time anchors: module
constants `ACTIVE_STATES` :69 / `BULK_CHECKPOINT_LIMIT` :70; class
declaration :941; the five readers :1545 (`readAwsReuseInputs`), :1595
(`readAwsReusableProfiles`), :2462 (`readAwsFinalReuseRows`), :2511
(`readAwsAmbiguousDataForSeoTargets`), :2530
(`readAwsTerminalCruxBigQueryWork`); the twenty-one `$transaction` sites
:1513, :1546, :1596, :1631, :1710, :2177, :2224, :2274, :2286, :2326, :2432,
:2465, :2519, :2538, :2603, :3808, :3829, :4133, :4204, :4461, :4512;
`publishAwsFinalResults` inline profile :2838; `saveQueryValidation` inline
profile :1873; `renewAwsRunLease` :2261.

1. **Validator and constant.** Immediately after `const BULK_CHECKPOINT_LIMIT = 500;`
   (line 70), insert exactly:
   `function requireAwsPipelineNow(now) {` /
   `  if (!(now instanceof Date) || !Number.isFinite(now.getTime())) {` /
   `    throw new PipelineInvariantError("PIPELINE_INPUT_CONFLICT");` /
   `  }` /
   `  return now;` /
   `}` and
   `const AWS_PIPELINE_TRANSACTION_OPTIONS = Object.freeze({ maxWait: 5_000, timeout: 30_000 });`
   (`PipelineInvariantError` is already imported and used in this file).
2. **Five signatures.** `async readAwsReuseInputs(input) {` becomes
   `async readAwsReuseInputs(input, now) {`; likewise
   `readAwsReusableProfiles`, `readAwsFinalReuseRows`,
   `readAwsAmbiguousDataForSeoTargets`, `readAwsTerminalCruxBigQueryWork`.
   No default value. In each: insert `requireAwsPipelineNow(now);` as the
   first statement — before the existing input validation for
   `readAwsFinalReuseRows`/`readAwsAmbiguousDataForSeoTargets`/
   `readAwsTerminalCruxBigQueryWork` is acceptable only in the exact position
   "first statement of the method body"; the frozen rule is: the validator
   runs before `this.prisma.$transaction` opens and before any database
   access. In each of the five `assertCompleteAggregatorInTransaction(transaction, { … }, new Date())`
   calls, the third argument `new Date()` becomes `now`.
3. **Twenty-one transaction arguments.** Each `$transaction` call belonging
   to `publishAwsDiscoveryStage`, `readAwsReuseInputs`,
   `readAwsReusableProfiles`, `publishAwsDomainCheckpoint`,
   `publishAwsLeadCheckpoint`, `claimAwsLeadWork`, `claimAwsRunLease`,
   `releaseAwsRunLease`, `loadAwsTrafficStage`, `claimAwsTrafficWorkBatch`,
   `recordAwsDataForSeoOutcome`, `readAwsFinalReuseRows`,
   `readAwsAmbiguousDataForSeoTargets`, `readAwsTerminalCruxBigQueryWork`,
   `publishAwsFinalResults`, `readReusableTrafficCache`,
   `readReusableLatestCruxBigQueryCache`, `planDataForSeoRequest`,
   `claimDataForSeoRequest`, `getDataForSeoRunCostUsd`,
   `markStaleDataForSeoRequestsAmbiguous` gains
   `AWS_PIPELINE_TRANSACTION_OPTIONS` as its second argument. The inline
   `{ maxWait: 5_000, timeout: 30_000 }` at :2838
   (`publishAwsFinalResults`) becomes the constant. The inline profile at
   :1873 (`saveQueryValidation`, `DEC-KI-051`) is not modified. No other
   transaction — and no atomic non-transactional `updateMany` such as
   `renewAwsRunLease` — is modified.
4. **Everything else byte-identical:** callbacks, locks, fences, rollback,
   paid-ledger and publication boundaries, `evaluatedAt` durable timestamps,
   error codes (`PIPELINE_LEASE_LOST` retained for stale clocks), and every
   non-enumerated method.

**Exact checks (§7.4).** C1 write-set as C136 (this file). C2 `node --check`
→ 0. C3 leaf-local assertion script verifies: one `requireAwsPipelineNow`
definition with the exact body; five signatures read
`(input, now)` with no default and each body contains
`requireAwsPipelineNow(now)` positioned before its `$transaction`; five
`assertCompleteAggregatorInTransaction` third arguments changed to `now`
(zero zero-argument `new Date()` remains at those five sites); one
`AWS_PIPELINE_TRANSACTION_OPTIONS` definition with the byte-exact literal;
twenty-one usages (twenty-two tokens); each of the twenty-one method bodies
contains both `$transaction` and the constant; exactly one inline
`{ maxWait: 5_000, timeout: 30_000 }` remains and lies inside
`saveQueryValidation`'s body; `renewAwsRunLease`'s body contains `updateMany`
and no `$transaction`; every other method byte-identical (diff-hunk audit).
Controls on in-memory copies: (A) removing the constant from
`markStaleDataForSeoRequestsAmbiguous` makes the twenty-one-usage assertion
fail; (B) reverting one reader's third argument to `new Date()` makes the
clock assertion fail. C4 secrets unchanged. DEFERRED to integration: real
transaction/lease behavior (`C143`/`C144`/`CV86`).

- [ ] P1 Revisions, assignment identity, writable file, baseline digest, and wave-1 dispatch evidence match.
- [ ] P2 Starting repository status and protected dirty changes match §2.
- [ ] T1 Apply every ordered transformation and no other edit to the writable file.
- [ ] V1 Run every LOCAL_NOW check and record its activation witnesses and exact assertions.
- [ ] V2 Prove the attributable workspace changed-file set is exactly the writable file.
- [ ] V3 Prove the `W6-DB-08`/`W6-DB-09`/`W6-DB-11` static witnesses; registrations execute in C142.
- [ ] H1 Return the exact diff, ending digest, commands, outcomes, and residual integration obligations.
- [ ] H2 Confirm no prohibited action, second-file edit, successor work, external mutation, or parent communication occurred.
- [ ] H3 Stop at AWAITING_WINDOW_REVIEW.

### 5.3 `KI-W6-C138` — domain-aggregator caller clock

```yaml
subwindow_id: KI-W6-C138
type: CORRECTION
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-14
assigned_agent: LEAF (KI-W6-C138-AGENT)
predecessors: [KI-W6-WAVE-1 dispatch]
successor_reserved_for: WINDOW-AGENT
writable_file: email_scraper/src/aws-pipeline/services/domain-aggregator.js
file_operation: MODIFY
starting_file_digest: e873bb622c085ea34e69e3658f21dacd36d068765f821782dfc613009f3199ce
starting_repository_change_set_digest: 565d9fb141c12fc6c056f259745965c450c65088acb62ade9c81d0193c022860
read_only_scope: [the writable file; src/prisma-run-repository.js (read-only); DEC-KI-053; CT22; this S1 §3.4; S2; S3]
authorized_actions: [apply the exact one-line transformation, run node --check, run the leaf-local assertion script, record S3 leaf evidence via the window agent]
prohibited_actions: (the common list)
may_start_successor: false
```

**Mechanical trace (§7.2).** `KI-W6-T22A` / `KI-W6-CT22` item 2 (domain
member): the sole domain call. Decision `DEC-KI-053` clock callers. Verified
by `C142` (caller audit) and `CV86`/`CV87`.

**Exact file transformation (§7.3).** The sole
`runtime.repository.readAwsReuseInputs({ runId: message.runId, … domains, evaluatedAt });`
call (authoring-time anchor :87–89) becomes the same call with `, new Date()`
inserted after the closing `}` of its first argument — ending
`… domains, evaluatedAt }, new Date());`. Argument one is byte-equivalent
otherwise; nothing else in the file changes; the call is not moved relative
to artifact reads, ownership, materialization, or publication.

**Exact checks (§7.4).** C1 write-set (this file). C2 `node --check` → 0. C3
leaf script: exactly one `readAwsReuseInputs(` occurrence in the file; its
call now ends `}, new Date());`; `git diff` is exactly one line changed.
Controls: (A) reverting the argument fails the second-argument assertion;
(B) adding `new Date()` to any other repository call fails the one-change
assertion.

- [ ] P1 Revisions, assignment identity, writable file, baseline digest, and wave-1 dispatch evidence match.
- [ ] P2 Starting repository status and protected dirty changes match §2.
- [ ] T1 Apply the exact one-call transformation and no other edit.
- [ ] V1 Run every LOCAL_NOW check and record its activation witnesses and exact assertions.
- [ ] V2 Prove the attributable workspace changed-file set is exactly the writable file.
- [ ] V3 Record the domain caller-audit witness consumed by C142.
- [ ] H1 Return the exact diff, ending digest, commands, outcomes, and residual integration obligations.
- [ ] H2 Confirm no prohibited action, second-file edit, successor work, external mutation, or parent communication occurred.
- [ ] H3 Stop at AWAITING_WINDOW_REVIEW.

### 5.4 `KI-W6-C139` — lead-aggregator caller clock

```yaml
subwindow_id: KI-W6-C139
type: CORRECTION
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-14
assigned_agent: LEAF (KI-W6-C139-AGENT)
predecessors: [KI-W6-WAVE-1 dispatch]
successor_reserved_for: WINDOW-AGENT
writable_file: email_scraper/src/aws-pipeline/services/lead-aggregator.js
file_operation: MODIFY
starting_file_digest: c3f2fb24576f43e6c046a87573e6e0942b9263d39c2002eec152280365cde38c
starting_repository_change_set_digest: 565d9fb141c12fc6c056f259745965c450c65088acb62ade9c81d0193c022860
read_only_scope:
  - the writable file; src/prisma-run-repository.js (frozen wave-1 output, read-only)
  - DEC-KI-053; KI-W6-CT22; this S1 §3.4; S2; S3
authorized_actions: [apply the exact one-line transformation, run node --check, run the leaf-local assertion script, record S3 leaf evidence via the window agent]
prohibited_actions: (the common list)
may_start_successor: false
```

**Mechanical trace (§7.2).** `KI-W6-T22B` / `KI-W6-CT22` item 2 (lead
member): the sole lead call. Decision `DEC-KI-053` clock callers. Verified by
`C142` (caller audit) and `CV86`/`CV87`.

**Exact file transformation (§7.3).** The sole
`runtime.repository.readAwsReusableProfiles({ runId: message.runId, … selections: reusableSelections, evaluatedAt: new Date(manifest.workPlan.evaluatedAt) });`
call (authoring-time anchor :71–73) ends `… evaluatedAt: new Date(manifest.workPlan.evaluatedAt) }, new Date());`.
Argument one is byte-equivalent; nothing else in the file changes; the call
is not moved.

**Exact checks (§7.4).** C1 write-set (this file). C2 `node --check` → 0. C3
leaf script: exactly one `readAwsReusableProfiles(` occurrence in the file;
its call ends `}, new Date());`; `git diff` is exactly one line changed.
Controls: (A) reverting the argument fails the second-argument assertion;
(B) adding `new Date()` to any other repository call fails the one-change
assertion.

- [ ] P1 Revisions, assignment identity, writable file, baseline digest, and wave-1 dispatch evidence match.
- [ ] P2 Starting repository status and protected dirty changes match §2.
- [ ] T1 Apply the exact one-call transformation and no other edit.
- [ ] V1 Run every LOCAL_NOW check and record its activation witnesses and exact assertions.
- [ ] V2 Prove the attributable workspace changed-file set is exactly the writable file.
- [ ] V3 Record the lead caller-audit witness consumed by C142.
- [ ] H1 Return the exact diff, ending digest, commands, outcomes, and residual integration obligations.
- [ ] H2 Confirm no prohibited action, second-file edit, successor work, external mutation, or parent communication occurred.
- [ ] H3 Stop at AWAITING_WINDOW_REVIEW.

### 5.5 `KI-W6-C140` — final-aggregator caller clocks

```yaml
subwindow_id: KI-W6-C140
type: CORRECTION
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-14
assigned_agent: LEAF (KI-W6-C140-AGENT)
predecessors: [KI-W6-WAVE-1 dispatch]
successor_reserved_for: WINDOW-AGENT
writable_file: email_scraper/src/aws-pipeline/services/final-aggregator.js
file_operation: MODIFY
starting_file_digest: 416e36feeb35aedd571ae8863a413550215263a157a99ed8cf519722446f9683
starting_repository_change_set_digest: 565d9fb141c12fc6c056f259745965c450c65088acb62ade9c81d0193c022860
read_only_scope:
  - the writable file; src/prisma-run-repository.js (frozen wave-1 output, read-only)
  - DEC-KI-053; KI-W6-CT22; this S1 §3.4; S2; S3
authorized_actions: [apply the exact three-line transformation, run node --check, run the leaf-local assertion script, record S3 leaf evidence via the window agent]
prohibited_actions: (the common list)
may_start_successor: false
```

**Mechanical trace (§7.2).** `KI-W6-T22C` / `KI-W6-CT22` item 2 (final
member): the three final calls. Decision `DEC-KI-053` clock callers.
Verified by `C142` (caller audit) and `CV86`/`CV87`.

**Exact file transformation (§7.3).** Exactly three calls gain `, new Date()`
as the second argument — `readAwsAmbiguousDataForSeoTargets({ … })` (anchor
:294–296), `readAwsTerminalCruxBigQueryWork({ … })` (anchor :324–326), and
`readAwsFinalReuseRows({ … selections: reuseSelections, evaluatedAt: new Date(manifest.workPlan.evaluatedAt) })`
(anchor :334–336). Each argument one is byte-equivalent; call order and all
other lines unchanged.

**Exact checks (§7.4).** C1 write-set (this file). C2 `node --check` → 0. C3
leaf script: exactly one occurrence each of the three call names; each ends
`}, new Date());`; `git diff` shows exactly three changed lines. Controls:
(A) reverting one argument fails the second-argument assertion; (B) adding a
fourth `new Date()` call argument fails the three-change assertion.

- [ ] P1 Revisions, assignment identity, writable file, baseline digest, and wave-1 dispatch evidence match.
- [ ] P2 Starting repository status and protected dirty changes match §2.
- [ ] T1 Apply the exact three-call transformation and no other edit.
- [ ] V1 Run every LOCAL_NOW check and record its activation witnesses and exact assertions.
- [ ] V2 Prove the attributable workspace changed-file set is exactly the writable file.
- [ ] V3 Record the three final caller-audit witnesses consumed by C142.
- [ ] H1 Return the exact diff, ending digest, commands, outcomes, and residual integration obligations.
- [ ] H2 Confirm no prohibited action, second-file edit, successor work, external mutation, or parent communication occurred.
- [ ] H3 Stop at AWAITING_WINDOW_REVIEW.

### 5.6 `KI-W6-C141` — coordinator unit regression for profile and consolidation

```yaml
subwindow_id: KI-W6-C141
type: CORRECTION
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-14
assigned_agent: LEAF (KI-W6-C141-AGENT)
predecessors: [KI-W6-WAVE-1 fully accepted]
successor_reserved_for: WINDOW-AGENT
writable_file: email_scraper/test/pipeline-coordinator-repository.test.js
file_operation: MODIFY
starting_file_digest: ee2f14da06e171d876c926cf2fde0f259a62dcf477f0d6873e8294d49bdb5533
starting_repository_change_set_digest: 565d9fb141c12fc6c056f259745965c450c65088acb62ade9c81d0193c022860
read_only_scope:
  - the writable file; src/aws-pipeline/repositories/pipeline-coordinator-repository.js (frozen wave-1 output)
  - DEC-KI-053; CT23 item 2; this S1 §3.4; S2; S3
authorized_actions: [modify only the writable file per the transformation, run node --check, run node --test test/pipeline-coordinator-repository.test.js, record S3 leaf evidence via the window agent]
prohibited_actions: (the common list; additionally) no production-source edit, no database use (unit fakes only)
may_start_successor: false
```

**Mechanical trace (§7.2).** `KI-W6-T23A` / `CT23` item 2. Decisions
`DEC-KI-053` (eleven-method set, consolidation), CT20 item 5 (baseline
recording, §0.1 item 1). Cases `W6-DB-08`/`W6-DB-10` (dynamic half);
supports `W6-NC-18`/`W6-NC-20` falsification surface.

**Exact file transformation (§7.3).** Preserve all five existing tests and
every accepted assertion byte-for-byte (migration/schema/exports/preflight
tests :12–67, the focused `renewTask` profile oracle :69–86, the collation
test :88–125). Append exactly three new tests:

1. **"all eleven coordinator transactions receive the frozen profile"** — a
   fake `prisma` whose `$transaction(operation, options)` records `options`
   and throws a distinct sentinel without invoking `operation`; for each of
   the eleven methods, call it with these preflight-passing literal inputs
   (`registerStage`: `{ runId: "run_profile_fixture", stage: "discovery",
   generation: 1,
   manifestS3Key: "runs/run_profile_fixture/domains-manifest.json",
   manifestFingerprint: "a".repeat(64), manifestProducedAt: now, tasks: [] }`;
   `recordDispatch`:
   `{ stageId: "stage_profile_fixture", itemKeys: ["k1"] }`; `claimTask`:
   `{ runId: "run_profile_fixture", stage: "discovery", generation: 1,
   itemKey: "k1", inputFingerprint: "a".repeat(64), owner: "spy",
   token: "00000000-0000-4000-8000-000000000001", leaseDurationMs: 60000 }`;
   `renewTask`: `{ taskId: "task_profile_fixture",
   token: "00000000-0000-4000-8000-000000000001",
   leaseDurationMs: 60000 }`; `recordTerminal`:
   `{ taskId: "task_profile_fixture",
   token: "00000000-0000-4000-8000-000000000001",
   inputFingerprint: "a".repeat(64), state: "succeeded",
   artifactS3Key: "runs/profile/result.json",
   artifactFingerprint: "b".repeat(64) }`; `claimAggregator`:
   `{ runId: "run_profile_fixture", stage: "discovery", generation: 1,
   owner: "spy", token: "00000000-0000-4000-8000-000000000002",
   leaseDurationMs: 120000 }`; `renewAggregator`:
   `{ stageId: "stage_profile_fixture",
   token: "00000000-0000-4000-8000-000000000002",
   leaseDurationMs: 120000 }`; `getCompleteStage`:
   `{ runId: "run_profile_fixture", stage: "discovery", generation: 1,
   token: "00000000-0000-4000-8000-000000000002" }`;
   `completeAggregator`: `{ stageId: "stage_profile_fixture",
   token: "00000000-0000-4000-8000-000000000002",
   state: "completed" }`; `listRecoverable`:
   `{ olderThan: now, limit: 100 }`; `cancelRunGeneration`:
   `{ runId: "run_profile_fixture", generation: 1 }`; every method receives
   the same fixed `new Date("2026-08-23T00:00:00.000Z")`) and assert the
   rejection is the sentinel (proving `$transaction` was reached) and
   `assert.deepEqual(recordedOptions, { maxWait: 5_000, timeout: 30_000 })`
   for all eleven, with exactly eleven records.
2. **"locked helpers return complete raw rows without delegate reads and the
   coordinator ceilings are exact"** — drive the maximal successful branch
   of each of `claimTask`, `renewTask`, `recordTerminal`, `claimAggregator`,
   `renewAggregator`, `getCompleteStage`, and `completeAggregator` through a
   method-local fake transaction. Every fake serves `selectSchema` first and
   then returns complete camelCase task/stage/run rows from `$queryRaw` in the
   production lock order. The common run row is exactly
   `{ id: runId, state: "running", executionBackend: "aws",
   pipelineGeneration: 1, leaseExpiresAt: null }`; collecting task/stage rows
   carry the method's exact IDs/fingerprints/tokens, live expiry
   `new Date(now.getTime() + 60000)` or
   `new Date(now.getTime() + 120000)`, `expectedCount: 1`, and matching
   terminal counters. The `recordTerminal` fixture is the final expected task,
   so it executes both stage writes and reaches `state: "ready"`.
   `pipelineTask.update` and `pipelineStage.update` return separately named
   expected updated rows; `claimTask` must return the task row returned by
   `pipelineTask.update` (not the pre-update raw locked row). Every
   `pipelineTask.findUnique`, `pipelineStage.findUnique`, and `run.findUnique`
   records and throws `"delegate read must not occur"`; the one deliberate
   `pipelineTask.findMany` inside `getCompleteStage` returns its single
   terminal task and is recorded separately from forbidden helper reloads.
   Assert the exact maximal statement ceilings below, counting `selectSchema`
   and every raw/delegate/write operation:

   | Method | Raw queries | Deliberate delegate reads | Writes | Total statements |
   |---|---:|---:|---:|---:|
   | `claimTask` | 4 | 0 | 1 | 5 |
   | `renewTask` | 4 | 0 | 1 | 5 |
   | `recordTerminal` | 4 | 0 | 3 | 7 |
   | `claimAggregator` | 3 | 0 | 1 | 4 |
   | `renewAggregator` | 3 | 0 | 1 | 4 |
   | `getCompleteStage` | 3 | 1 | 0 | 4 |
   | `completeAggregator` | 3 | 0 | 1 | 4 |

   Emit this literal table as `context.diagnostic` and assert deep equality;
   any additional raw query, delegate read, or write fails the test. This is
   the frozen CT20-item-5 post-consolidation baseline consumed by CV86.
3. **"recordDispatch locks complete rows once and never reloads tasks"** —
   fake transaction whose `$queryRaw` returns: for the ordered task lock, two
   complete task rows (`itemKey` `"k1"`, `"k2"`); for the stage lock, a
   complete stage row with `expectedCount: 2`, `state: "collecting"`;
   `pipelineTask.findMany` records and throws `"task reload must not occur"`;
   `pipelineTask.updateMany` returns `{ count: 1 }`. Call
   `recordDispatch({ stageId, itemKeys: ["k1"] }, now)` → `{ count: 1 }`,
   zero `findMany`; then a cardinality-control call with a stage row whose
   `expectedCount: 3` rejects with `PIPELINE_INPUT_CONFLICT`.

**Exact checks (§7.4).** C1 write-set (this file). C2 `node --check` → 0. C3
`node --test test/pipeline-coordinator-repository.test.js` → exit 0, eight
tests, zero failures/skips (LOCAL_NOW). C4 diff-hunk audit: only the three
appended tests; existing five byte-identical. DEFERRED: statement-ceiling
enforcement (`CV86`).

- [ ] P1 Revisions, assignment identity, writable file, baseline digest, and wave-2 dispatch evidence match.
- [ ] P2 Starting repository status contains only accepted wave-1 endings plus protected root coordination state.
- [ ] T1 Append exactly the three prescribed tests and preserve the existing five tests byte-identically.
- [ ] V1 Run every LOCAL_NOW check and record eight passing tests and the literal seven-method ceiling table.
- [ ] V2 Prove the attributable workspace changed-file set is exactly the writable file.
- [ ] V3 Record the dynamic `W6-DB-08`/`W6-DB-10` witnesses with zero skips.
- [ ] H1 Return the exact diff, ending digest, commands, outcomes, and residual integration obligations.
- [ ] H2 Confirm no prohibited action, second-file edit, successor work, external mutation, or parent communication occurred.
- [ ] H3 Stop at AWAITING_WINDOW_REVIEW.

### 5.7 `KI-W6-C142` — transaction-clock enforcement suite (CREATE)

```yaml
subwindow_id: KI-W6-C142
type: CORRECTION
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-14
assigned_agent: LEAF (KI-W6-C142-AGENT)
predecessors: [KI-W6-WAVE-1 fully accepted]
successor_reserved_for: WINDOW-AGENT
writable_file: email_scraper/test/aws-pipeline-transaction-clock-enforcement.test.js
file_operation: CREATE
starting_file_digest: ABSENT
starting_repository_change_set_digest: 565d9fb141c12fc6c056f259745965c450c65088acb62ade9c81d0193c022860
read_only_scope:
  - src/aws-pipeline/repositories/pipeline-coordinator-repository.js, src/prisma-run-repository.js,
    src/aws-pipeline/services/domain-aggregator.js, src/aws-pipeline/services/lead-aggregator.js,
    src/aws-pipeline/services/final-aggregator.js (frozen wave-1 outputs, read via node:fs)
  - email_scraper/test/keyword-intelligence-enforcement.test.js (registration/certificate precedent, read-only)
  - DEC-KI-053; SRC-KI-055; CT23 item 3; SCN-KI-044; this S1 §3.4/§4; S2; S3
authorized_actions: [create only the writable file, run node --check, run node --test on it (no database required), record S3 leaf evidence via the window agent]
prohibited_actions: (the common list; additionally) no database use, no production-source edit, no dynamic import or execution of production modules except pure functions named below)
may_start_successor: false
```

**Mechanical trace (§7.2).** `KI-W6-T23B` / `CT23` item 3. Registers and
executes exactly `W6-DB-08`, `W6-DB-09`, `W6-DB-10`, `W6-DB-11` (unit half)
and the three controls `W6-NC-18`–`20`. Decisions `DEC-KI-053` (all four
enforcement clauses); scenario `SCN-KI-044` activation witnesses (32/32
transaction members, 9/9 explicit clocks). Zero database, zero network.

**Exact file transformation (§7.3).** Create exactly this Node ESM test file.
Structure, in order:

1. **Imports (exactly):** `node:assert/strict`, `node:test`, `node:fs/promises`
   (`readFile`), `node:crypto` (`createHash`), `node:url` (`pathToFileURL` not
   required — resolve sources relative to `import.meta.url`), and
   `src/prisma-run-repository.js` (`PrismaRunRepository`) for the
   `W6-DB-11` rejection half (pure construction with a fake prisma; no
   connection).
2. **Constants:** `REQUIRED = ["W6-DB-08","W6-DB-09","W6-DB-10","W6-DB-11"]`;
   `CONTROLS = ["W6-NC-18","W6-NC-19","W6-NC-20"]`; the eleven coordinator
   method names and twenty-one run-repository method names as literal arrays
   (copied from DEC-KI-053 verbatim); the five clock-method names; the five
   caller signatures (file + call name + count); registries
   `registered`/`executed`/`witnesses`/`failures`.
3. **Source loader:** read the five wave-1 files once into strings; a helper
   slices a class body into per-method text on `^  async <name>(` boundaries;
   a helper slices module functions (`lockedTask` etc.) on
   `^async function <name>(` boundaries.
4. **`W6-DB-08` (transaction memberships and frozen constants):** compute the
   coordinator's `$transaction`-containing method set from source and assert
   set equality with the literal eleven (recomputed from source, not
   trusted from counts); assert each of the eleven bodies contains
   `PIPELINE_TRANSACTION_OPTIONS`; assert exactly one definition of the
   constant with the byte-exact frozen literal; assert zero inline
   `{ maxWait: 5_000, timeout: 30_000 }` in the coordinator file. For the run
   repository: assert each of the literal twenty-one bodies contains both
   `$transaction` and `AWS_PIPELINE_TRANSACTION_OPTIONS`; assert exactly
   twenty-one usages (twenty-two tokens including the one definition); one
   definition with the byte-exact literal; exactly one surviving inline
   profile and it is inside `saveQueryValidation`; `renewAwsRunLease` has no
   `$transaction` and retains `updateMany`.
5. **`W6-DB-09` (nine-clock inventory):** count
   `assertCompleteAggregatorInTransaction(` call sites across the two
   repository files — exactly nine (one coordinator, eight run-repository);
   none of the nine passes `new Date()`; the five clock methods have
   `(input, now)` signatures with no `= new Date()` default, contain
   `requireAwsPipelineNow(now)` before `$transaction`, and forward `now`;
   exactly one `requireAwsPipelineNow` definition; the five service callers:
   in `domain-aggregator.js` exactly one `readAwsReuseInputs(` occurrence
   ending `}, new Date())`; in `lead-aggregator.js` exactly one
   `readAwsReusableProfiles(` occurrence ending `}, new Date())`; in
   `final-aggregator.js` exactly one occurrence each of
   `readAwsAmbiguousDataForSeoTargets(`, `readAwsTerminalCruxBigQueryWork(`,
   `readAwsFinalReuseRows(`, each ending `}, new Date())`.
6. **`W6-DB-10` (lock/read ceilings, static half):** `lockedTask`/
   `lockedStage`/`lockedRun` bodies each contain `SELECT *` and `FOR UPDATE`
   and `rows[0]` and no `findUnique`; the `recordDispatch` body contains
   `SELECT *`, no `findMany`, exactly one `updateMany`; the dynamic
   operation-count baseline itself is the `C141` witness (referenced by
   evidence ID, not re-derived here).
7. **`W6-DB-11` (required-now rejection, unit half):** with
   `const prisma = { $transaction: async () => { throw new Error("transaction must not start"); } }`
   and `new PrismaRunRepository(prisma, {})`: for each of the five clock
   methods, `assert.rejects` with a missing second argument and with an
   invalid second argument (`new Date("invalid")` and `42`) proving
   `error.code === "PIPELINE_INPUT_CONFLICT"` and — via a recording fake
   whose `$transaction` counts invocations — zero transaction attempts; then
   with a valid `new Date("2026-08-23T00:00:00.000Z")` and a recording fake
   whose `$transaction` throws a distinct sentinel, assert the sentinel
   (validation passed, transport reached) for all five methods.
8. **Controls (each: apply the mutation to an in-memory copy → rerun only the
   targeted oracle function against the copy → assert it throws; record the
   control only after the throw; then a fresh positive pass on the real
   source):**
   - `W6-NC-18`: in the coordinator copy, remove the constant argument from
     `listRecoverable` (`}, PIPELINE_TRANSACTION_OPTIONS);`
     → `});`) — the unchanged `W6-DB-08` membership/profile oracle must
     throw.
   - `W6-NC-19`: in the run-repository copy, replace one forwarded `now`
     third argument at an `assertCompleteAggregatorInTransaction` site with
     `new Date()` — the unchanged `W6-DB-09` oracle must throw.
   - `W6-NC-20`: in the coordinator copy, restore one follow-up reload
     (insert `await transaction.pipelineStage.findUnique({ where: { id: stageId } });`
     into `lockedStage`) — the unchanged `W6-DB-10` oracle must throw.
9. **Certificate:** a final always-run test asserts `registered = executed =
   REQUIRED` (zero skips — no database gate exists), `failures` empty, and
   `falsifiedControls = CONTROLS`. It writes exactly one stdout line whose JSON
   value is the following complete member set (JSON key order is fixed as
   shown; the three digests are recomputed at runtime and must equal the
   literals):

   `KI_W6_TXN_CLOCK_ENFORCEMENT_CERTIFICATE={"file":"aws-pipeline-transaction-clock-enforcement.test.js","required":["W6-DB-08","W6-DB-09","W6-DB-10","W6-DB-11"],"registered":["W6-DB-08","W6-DB-09","W6-DB-10","W6-DB-11"],"executed":["W6-DB-08","W6-DB-09","W6-DB-10","W6-DB-11"],"skipped":[],"activationWitnesses":{"coordinatorTransactions":11,"runRepositoryTransactions":21,"assertionClockSites":9,"serviceCallers":5},"oracleFailures":[],"negativeControls":{"expected":3,"falsified":3,"ids":["W6-NC-18","W6-NC-19","W6-NC-20"]},"digests":{"required":"e8bd1b4a3b3deb8f853eac0e8bcea5609278177945389f292b1b12a7309bf030","registered":"e8bd1b4a3b3deb8f853eac0e8bcea5609278177945389f292b1b12a7309bf030","executed":"e8bd1b4a3b3deb8f853eac0e8bcea5609278177945389f292b1b12a7309bf030","controls":"89e40c02b11dd426c8445de018a9d85fa2c110b6da9728cee8dff4e3cc31db1b"}}`

**Exact checks (§7.4).** C1 write-set (this one new untracked file). C2
`node --check` → 0. C3 `node --test
test/aws-pipeline-transaction-clock-enforcement.test.js` → exit 0, all tests
pass, certificate line present with `executed === required`,
`negativeControls.falsified === 3`, and the exact three control IDs
(LOCAL_NOW; no env vars). C4 the file
imports nothing outside `node:` builtins and the one named `src/` module; no
credentials, tokens, production IDs, or provider bodies (only method names,
counts, hashes). DEFERRED: integration halves (`C143`/`C144`, `CV86`).

- [ ] P1 Revisions, assignment identity, writable CREATE file, ABSENT baseline, and wave-2 dispatch evidence match.
- [ ] P2 Starting repository status contains only accepted wave-1 endings plus protected root coordination state.
- [ ] T1 Create exactly the prescribed enforcement suite and no other file.
- [ ] V1 Run every LOCAL_NOW check and capture the exact certificate with four executed cases and three falsified controls.
- [ ] V2 Prove the attributable workspace changed-file set is exactly the writable file.
- [ ] V3 Prove required=registered=executed `W6-DB-08`–`11`, zero skips, and expected=falsified `W6-NC-18`–`20`.
- [ ] H1 Return the exact file, ending digest, commands, outcomes, and residual integration obligations.
- [ ] H2 Confirm no prohibited action, second-file edit, successor work, external mutation, or parent communication occurred.
- [ ] H3 Stop at AWAITING_WINDOW_REVIEW.

### 5.8 `KI-W6-C143` — lead integration controlled-clock coverage

```yaml
subwindow_id: KI-W6-C143
type: CORRECTION
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-14
assigned_agent: LEAF (KI-W6-C143-AGENT)
predecessors: [KI-W6-WAVE-1 fully accepted, C141 and C142 dispatch-parallel peers]
successor_reserved_for: WINDOW-AGENT
writable_file: email_scraper/test/aws-pipeline-lead-aggregation.integration.test.js
file_operation: MODIFY
starting_file_digest: 102cac9694251ea5dedb40bcf44a07b771f26440202b5c81a3c5f33b98630238
starting_repository_change_set_digest: 565d9fb141c12fc6c056f259745965c450c65088acb62ade9c81d0193c022860
read_only_scope:
  - the writable file; src/prisma-run-repository.js (frozen wave-1 output, read-only); src/aws-pipeline/repositories/pipeline-coordinator-repository.js (read-only)
  - test/fixtures/aws-pipeline/v1/** (read-only); test/helpers/isolated-postgres.js (read-only)
  - DEC-KI-053; CT23 item 4; this S1 §3.4; S2; S3
authorized_actions: [modify only the writable file per the transformation, run node --check test/aws-pipeline-lead-aggregation.integration.test.js, run exactly once ALLOW_DATABASE_TESTS=true node -r dotenv/config --test --test-isolation=none --test-concurrency=1 test/aws-pipeline-lead-aggregation.integration.test.js against an isolated non-production TEST_DATABASE_URL with sandbox escalation permitted, record S3 leaf evidence via the window agent]
prohibited_actions: (the common list; additionally) any production-database use, any test-database use other than one disposable schema named g10_lead_* created via test/helpers/isolated-postgres.js)
may_start_successor: false
```

**Mechanical trace (§7.2).** `KI-W6-T23C` / `CT23` item 4. Case `W6-DB-11`
(lead integration half). Decision `DEC-KI-053` clock interface.

**Exact file transformation (§7.3).** In the single existing test, at the
"reusable profile read" step (anchor :49–53): extract the existing input
object verbatim into `const reuseInput = { runId: manifest.runId, generation: 1,
stageId: lead.stage.id, aggregationToken: token, evaluatedAt: now,
selections: [{ shopId: domain.shopId, profileShopId: domain.shopId, profileFingerprint,
stableIdentity: domain.identity.stableKey }] };` and change the call to
`const selected = await repository.readAwsReusableProfiles(reuseInput, new Date(now.getTime() + 2));`
(the aggregator claim is at `+1` with a 120000 ms lease; `+2` is
inside-lease). Retain `assert.equal(selected.profiles.length, 1);`. Then
insert immediately after it exactly this block:

```js
step = "reusable profile clock rejection";
await assert.rejects(repository.readAwsReusableProfiles(reuseInput),
  (error) => error.code === "PIPELINE_INPUT_CONFLICT");
await assert.rejects(repository.readAwsReusableProfiles(reuseInput, new Date("invalid")),
  (error) => error.code === "PIPELINE_INPUT_CONFLICT");
await assert.rejects(repository.readAwsReusableProfiles(reuseInput,
  new Date(now.getTime() + 120001)), (error) => error.code === "PIPELINE_LEASE_LOST");
assert.equal((await prisma.pipelineStage.findUnique({ where: { id: lead.stage.id } })).state,
  "aggregating");
```

(expiry = claim `+1` + 120000 = `+120001` boundary past expiry; the claim at
`+1` used `leaseDurationMs: 120000`; the three rejections mutate nothing, so
every later existing assertion — publication at `+2`, post-commit checks —
still passes unchanged). The existing `publishAwsLeadCheckpoint(…, new Date(now.getTime() + 2))`
and every other line remain byte-identical.

**Exact checks (§7.4).** C1 write-set (this file). C2 `node --check` → 0. C3
one isolated-database run → exit 0, one test passing, `step` progression
witnessed; disposable schema `g10_lead_*` dropped with
`DROP SCHEMA IF EXISTS … CASCADE` in the unchanged `finally`. C4 diff-hunk
audit: input extraction, clock argument, inserted rejection block only.
DEFERRED: full-suite `CV86`.

- [ ] P1 Revisions, assignment identity, writable file, baseline digest, and wave-2 dispatch evidence match.
- [ ] P2 Starting repository status contains only accepted wave-1 endings plus protected root coordination state; TEST_DATABASE_URL is isolated and non-production.
- [ ] T1 Apply the exact reuse-input extraction, controlled clock, and rejection block only.
- [ ] V1 Run syntax and the one authorized isolated-file test command; require one pass and zero skips.
- [ ] V2 Prove the attributable workspace changed-file set is exactly the writable file and the disposable schema is absent after exit.
- [ ] V3 Prove the `W6-DB-11` lead half: missing/invalid/expired rejection and inside-lease success on the same input.
- [ ] H1 Return the exact diff, ending digest, commands, outcomes, cleanup witness, and residual integration obligations.
- [ ] H2 Confirm no prohibited action, second-file edit, successor work, external mutation, or parent communication occurred.
- [ ] H3 Stop at AWAITING_WINDOW_REVIEW.

### 5.9 `KI-W6-C144` — final integration controlled-clock coverage

```yaml
subwindow_id: KI-W6-C144
type: CORRECTION
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-14
assigned_agent: LEAF (KI-W6-C144-AGENT)
predecessors: [KI-W6-WAVE-1 fully accepted, C141/C142/C143 dispatch-parallel peers]
successor_reserved_for: WINDOW-AGENT
writable_file: email_scraper/test/aws-pipeline-final.integration.test.js
file_operation: MODIFY
starting_file_digest: 22b70d3111ea65d0e24fe9d5e82d4c03e8fe84c6b80e076335e919edd0e0e664
starting_repository_change_set_digest: 565d9fb141c12fc6c056f259745965c450c65088acb62ade9c81d0193c022860
read_only_scope:
  - the writable file; src/prisma-run-repository.js and src/aws-pipeline/repositories/pipeline-coordinator-repository.js (frozen wave-1 outputs, read-only)
  - test/fixtures/aws-pipeline/v1/** (read-only); test/helpers/isolated-postgres.js (read-only)
  - DEC-KI-053; CT23 item 5; this S1 §0.1 item 3/§3.4; S2; S3
authorized_actions: [modify only the writable file per the transformation, run node --check test/aws-pipeline-final.integration.test.js, run exactly once ALLOW_DATABASE_TESTS=true node -r dotenv/config --test --test-isolation=none --test-concurrency=1 test/aws-pipeline-final.integration.test.js against an isolated non-production TEST_DATABASE_URL with sandbox escalation permitted, record S3 leaf evidence via the window agent]
prohibited_actions: (the common list; additionally) any production-database use, any test-database use other than disposable schemas named g12_final_*/gr8_final_*/gr30_final_*/w6clk_final_* created via test/helpers/isolated-postgres.js)
may_start_successor: false
```

**Mechanical trace (§7.2).** `KI-W6-T23D` / `CT23` item 5. Case `W6-DB-11`
(final/domain/lead integration half). Decision `DEC-KI-053`; §0.1 item 3
coverage shape.

**Exact file transformation (§7.3).** Three edits; everything else
byte-identical:

1. **G12 test, `readAwsFinalReuseRows` (anchor :52–53):** the call gains
   `, new Date(now.getTime() + 2)` as its second argument (claim at `+1`,
   lease 120000 ms; the later `publishAwsFinalResults` remains at `+2`).
2. **G-R8 test, `readAwsTerminalCruxBigQueryWork` (anchor :129–132):** the
   call gains `, new Date(now.getTime() + 2)` as its second argument (the
   fixed clock `2026-08-13` precedes the `:121–123` real-clock lease
   extension; `+2` is inside the lease).
3. **Append one new test
   `"W6-DB-11 five aggregation readers reject, expire, and succeed under explicit controlled clocks"`
   (`{ skip: !enabled, timeout: 180000 }`):** schema
   `` `w6clk_final_${Date.now()}_${process.pid}` ``; one `Run` row
   (`state: "running"`, `executionBackend: "aws"`, `pipelineGeneration: 1`,
   `stage: "aws_traffic_crux"`). Its `trafficEnrichmentConfig` is exactly
   `trafficEnrichmentConfigSnapshot({})`. Its `awsProviderConfig` is exactly
   the valid G12 fixture produced by
   `awsProviderConfigSnapshot({ browserlessUrl: "https://fixture.example",
   googleSearchEngineId: "fixture", googleResultsPerQuery: 10,
   requestTimeoutMs: 10000, maxPagesPerStore: 5, pageFetchConcurrency: 2,
   maxQueries: 20, generatedQueryCount: 10, queryProbeFreshnessMs: 60000,
   queryProbeConcurrency: 1, minQueryResults: 1, minQueryUniqueHosts: 1,
   minQueryRelevantResults: 1, minQueryRelevanceRatio: 0.1,
   minQueryBaseScore: 1, browserlessEnabled: false,
   enableAiNormalization: false })`; raw `{}` snapshots are forbidden because
   `readAwsReuseInputs` parses both contracts.
   `now = new Date("2026-08-23T00:00:00.000Z")`; register three zero-task
   stages via `coordinator.registerStage({ runId, stage: "discovery" |
   "lead" | "traffic_crux", generation: 1, manifestS3Key:
   `runs/${runId}/domains-manifest.json`, manifestFingerprint: "a".repeat(64),
   manifestProducedAt: now, tasks: [] }, now)`; claim each stage's aggregator
   at `new Date(now.getTime() + 1)` with its own UUID token and
   `leaseDurationMs: 120000`, asserting `outcome: "owned"`. Then for the five
   readers, each with its zero-candidate input — domain:
   `{ runId, generation: 1, stageId: discoveryStage.stage.id,
   aggregationToken: discoveryToken, domains: [], evaluatedAt:
   discoveryStage.stage.createdAt }` (§0.1 item 6); lead:
   `{ runId, generation: 1, stageId: leadStage.stage.id, aggregationToken:
   leadToken, evaluatedAt: now, selections: [] }`; final-reuse:
   `{ runId, generation: 1, stageId: trafficStage.stage.id,
   aggregationToken: trafficToken, selections: [], evaluatedAt: now }`;
   ambiguous/targets and terminal-work: `{ runId, generation: 1,
   aggregationToken: trafficToken, candidates: [] }` — execute and assert in
   order: (i) missing second argument → `PIPELINE_INPUT_CONFLICT`; (ii)
   `new Date("invalid")` → `PIPELINE_INPUT_CONFLICT`; (iii) after (i)/(ii)
   each stage row still reads `state: "aggregating"` and the run row is
   unchanged (zero writes on rejection); (iv) expired
   `new Date(now.getTime() + 120001)` → `PIPELINE_LEASE_LOST`; these injected
   expiry probes are nonmutating and therefore do not prevent the following
   inside-lease probes at earlier controlled instants. (v) call the domain and
   lead readers at `new Date(now.getTime() + 2)` and assert domain
   `awsProviderConfig`/traffic snapshot members are present and lead
   `profiles.length === 0`; (vi) complete the lead stage exactly once with
   `coordinator.completeAggregator({ stageId: leadStage.stage.id,
   token: leadToken, state: "completed" }, new Date(now.getTime() + 3))` and
   assert its returned stage and durable row are `completed`; this transition
   is mandatory because `readAwsFinalReuseRows` rejects a non-completed lead
   stage; (vii) call the three traffic-stage readers at
   `new Date(now.getTime() + 4)` and assert final-reuse
   `trafficRows/leadTasks/leads` are all empty arrays, ambiguous is an empty
   array, and terminal-work is an empty array. The discovery stage remains
   `aggregating`, the lead stage alone becomes `completed`, the traffic stage
   remains `aggregating`, and the run remains byte-deep-equal to its captured
   pre-reader row throughout except for no field (the stage completion does
   not update `Run`). Teardown `finally`: drop the schema with
   `DROP SCHEMA IF EXISTS … CASCADE`, then the exact absence witness
   `const [absent] = await base.$queryRawUnsafe(\`SELECT EXISTS (SELECT 1 FROM pg_namespace WHERE nspname = '${schema}') AS present\`);`
   `assert.equal(absent.present, false);` then disconnects.

**Exact checks (§7.4).** C1 write-set (this file). C2 `node --check` → 0. C3
one isolated-database run → exit 0, four tests passing (the three existing
tests plus the new one), zero skips, schema-absence witnesses recorded. C4 diff-hunk audit: two
argument additions plus the one appended test; existing assertions
byte-identical. DEFERRED: `CV86`/`CV87`.

- [ ] P1 Revisions, assignment identity, writable file, baseline digest, and wave-2 dispatch evidence match.
- [ ] P2 Starting repository status contains only accepted wave-1 endings plus protected root coordination state; TEST_DATABASE_URL is isolated and non-production.
- [ ] T1 Apply exactly two existing-call arguments plus the fully specified new controlled-clock test.
- [ ] V1 Run syntax and the one authorized isolated-file test command; require four passes and zero skips.
- [ ] V2 Prove the attributable workspace changed-file set is exactly the writable file and every disposable schema is absent after exit.
- [ ] V3 Prove the `W6-DB-11` five-reader missing/invalid/expired/inside outcomes, lead completion prerequisite, zero rejected-path writes, and schema absence.
- [ ] H1 Return the exact diff, ending digest, commands, outcomes, cleanup witnesses, and residual integration obligations.
- [ ] H2 Confirm no prohibited action, second-file edit, successor work, external mutation, or parent communication occurred.
- [ ] H3 Stop at AWAITING_WINDOW_REVIEW.

### 5.10 `KI-W6-I119` — window-agent integration assessment

```yaml
subwindow_id: KI-W6-I119
type: INTEGRATION_ASSESSMENT (window-agent owned; not delegated)
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-14
assigned_agent: KI-W6-WINDOW-AGENT
predecessors: [KI-W6-C136..KI-W6-C144 all independently accepted]
successor_reserved_for: PARENT
writable_file: none
file_operation: none
starting_file_digest: N/A
starting_repository_change_set_digest: 565d9fb141c12fc6c056f259745965c450c65088acb62ade9c81d0193c022860
read_only_scope: [all nine leaf files plus S1/S2/S3; both repositories' complete diff; parent artifacts A1–A8]
authorized_actions:
  - independently review all nine leaf handoffs per the sub-window standard section 8
  - execute gates KI-W6-CV84 through KI-W6-CV90 exactly once each on frozen final inputs, in order
  - execute the W6 case/control union merge
  - append the section 12.4 integration certificate to S3 and set S2 to READY_FOR_PARENT_REVIEW
prohibited_actions:
  - any implementation-file write (a diagnosed defect opens KI-W6-C145+)
  - repeating a passed stateful gate without a documented invalidation
  - claiming parent acceptance or beginning KI-W7
may_start_successor: false
```

**Frozen gates (copied from the parent checklist's `KI-W6-I119` section; each
exactly once, in order, on the frozen final tree; stop on an observable
behavioral failure):**

- **`KI-W6-CV84`** — recompute every starting/ending digest; prove the actual
  implementation/test changed-file set equals exactly the nine-path set and
  digest `ba4ccba7…`; independently inspect all diffs; prove no accepted
  unrelated hunk was weakened.
- **`KI-W6-CV85`** — `node --check` on the five production and four test
  files; then from `email_scraper/`:
  `node --test test/pipeline-coordinator-repository.test.js
  test/aws-pipeline-transaction-clock-enforcement.test.js
  test/aws-pipeline-domain.test.js
  test/aws-pipeline-lead-aggregation.test.js
  test/aws-pipeline-final.test.js` → exit 0, zero failures/skips for the four
  new cases, exact executed set `W6-DB-08`–`11`, all three controls
  falsified-then-fresh-positive.
- **`KI-W6-CV86`** — once, with the authorized isolated test database, from
  `email_scraper/`:
  `ALLOW_DATABASE_TESTS=true node -r dotenv/config --test
  --test-isolation=none --test-concurrency=1
  test/pipeline-coordinator-repository.integration.test.js
  test/aws-pipeline-domain.integration.test.js
  test/aws-pipeline-lead-aggregation.integration.test.js
  test/aws-pipeline-traffic.integration.test.js
  test/aws-pipeline-final.integration.test.js` → exit 0, zero guarded skips,
  controlled-time lease assertions, rollback assertions, operation ceilings
  (C141 baseline), exact test-schema isolation, zero residual disposable
  schemas.
- **`KI-W6-CV87`** — after CV86 passes, exactly one durable causal command
  from `email_scraper/` with local substitutes and the authorized test
  database: `ALLOW_DATABASE_TESTS=true KI_W6_SKIP_BUILD=1 node
  test/browser/keyword-intelligence-e2e.mjs`. Transport retains complete
  stdout/stderr and exit status in the preflight-empty files
  `/tmp/ki-w6-i119-state184.browser.log` and
  `/tmp/ki-w6-i119-state184.browser.status`, uses an executor allowance of at
  least 75 minutes, and remains attached/durable independently of a chat
  turn. Require exit 0; existing browser required=registered=executed 26/26
  with 13 controls; 100 validators; 100 discovery tasks; 1,000
  domains/leads; the five clock-correct aggregation readers; no transaction
  timeout/lease error; cleanup/schema absence. One identical escalated
  recovery only after the exact E8.1 invalidation/postcondition proof.
- **`KI-W6-CV88`** — only after CV87 passes, run once from `email_scraper/`:
  `npm test`, `npm run check:secrets`, `npm run build:lambda`; from
  `frontend/`: `npm run check`. Require zero failures, clean secret/privacy
  scan, successful handler build/startup inventory, frontend
  lint/test/build success. Do not repeat a successful unchanged expensive
  gate.
- **`KI-W6-CV89`** — recompute the final W6 case union as exactly 39 members
  with digest `f8137d25…` and control union as exactly 20 members with
  digest `0cbaad07…`; required=registered=executed; zero
  skips/duplicates/unexpected IDs; every activation witness; 20/20
  falsified controls.
- **`KI-W6-CV90`** — verify no provider/AWS/production/paid action, schema or
  migration, package/config, frontend product, global Prisma default, lease,
  retry, cost, payload, S3/SQS, commit/push, or KI-W7 change occurred; paid
  cost `$0.00`; exact disposable schema/process/output cleanup; privacy-safe
  evidence.
- **`KI-W6-CH15`** — append the complete window-agent
  integration/enforcement certificate (§12.4 form), set the subordinate
  state to `READY_FOR_PARENT_REVIEW`, return only the consolidated handoff
  to the parent, and stop before KI-W7.

**Mandatory integration checklist (sub-window standard §9.4), executed
personally:** I1 all nine leaves independently accepted (list IDs and ending
digests); I2 actual assembled changed files equal the nine-path set within
parent scope; I3 complete requirement→decision→file→sub-window→assertion
trace; I4 all frozen gates executed with activation witnesses; I5
required=registered=executed case/control sets with matching digests and
zero skips/duplicates/unexpected; I6 negative controls executed and
acceptance fails under each prescribed defect; I7 substitute fidelity and
accepted-test integrity (no weakened oracle); I8 no prohibited, successor,
external, destructive, secret-bearing, or out-of-scope action; I9 independent
source/diff inspection, not leaf summaries; I10 `PASS` /
`CORRECTION_REQUIRED` / `PARENT_BLOCKED` recorded with decisive evidence.
Result oracles: `PASS` only when CV84–CV90 all pass and CH15 completes;
`CORRECTION_REQUIRED` opens `KI-W6-C145+` single-file corrections and a new
`KI-W6-I120+`; `PARENT_BLOCKED` on any missing decision, contradiction, or
scope expansion.

## 6. Case allocation and control mapping (complete W6 closure)

New members owned by this sequence:

| Case | Type | Leaf | Assertion anchor |
|---|---|---|---|
| `W6-DB-08` | enforcement case | C142 (registration/execution), C141 (dynamic profile spies), C136/C137 (implementation) | 11/21 literal memberships; two frozen constants; usage-count arithmetic (§0.1 item 2) |
| `W6-DB-09` | enforcement case | C142, C137/C138/C139/C140 (implementation) | nine `assertCompleteAggregatorInTransaction` sites with explicit clocks; five `(input, now)` signatures; five service callers; zero internal zero-argument `new Date()` |
| `W6-DB-10` | enforcement case | C142 (static), C141 (dynamic baseline), C136 (implementation) | locked helpers return raw rows with zero delegate reads; `recordDispatch` zero task reload; CV86 ceiling enforcement |
| `W6-DB-11` | enforcement case | C142 (unit rejection half), C143 (lead half), C144 (five-method half), C137 (implementation) | missing/invalid-now pre-transaction `PIPELINE_INPUT_CONFLICT` with zero writes; expired `PIPELINE_LEASE_LOST`; inside-lease success |
| `W6-NC-18` | negative control | C142 | remove one profile argument → unchanged `W6-DB-08` oracle throws |
| `W6-NC-19` | negative control | C142 | restore one hidden clock / drop caller argument → unchanged `W6-DB-09` oracle throws |
| `W6-NC-20` | negative control | C142 | restore one follow-up reload → unchanged `W6-DB-10` oracle throws |

Existing 32 members (`W6-NAV-01`–`03`, `W6-CONF-01`–`06`, `W6-FLOW-01`–`13`,
`W6-RES-01`–`04`, `W6-TXN-01`/`02`, `W6-DB-01`–`07`, and controls
`W6-NC-01`–`17`) were registered, executed, and accepted by their prior
W6 leaves and assessments; they are regression-referenced here by
`KI-W6-CV87` (browser 26/13) and recomputed into the 39/20 unions by
`KI-W6-CV89`. Unmapped parent requirements/decisions/tasks/scenarios/cases:
none — every `KI-W6-CT20`–`CT23` item and `SCN-KI-044` clause maps into §5
blocks; `SCN-KI-018` is executed unchanged by `CV87`; the parent readiness
items `RW6O-001`–`006` and `RW6P-001`–`012` are already checked by the
parent and are not re-owned here.

## 7. Correction and re-assessment rules (append-only)

Corrections are append-only `KI-W6-C145+`, each owning exactly one of the
nine files (or a parent-authorized tenth file only after explicit scope
expansion), each citing failed evidence, root cause, the governing parent
decision, corrected sub-window, invalidated evidence/gates, and a new
`KI-W6-I120+` assessment. Every correction invalidates all evidence whose
inputs include its file; unaffected costly gates may be reused only with a
recorded deterministic dependency comparison. A defect root-caused outside
the nine files or outside `DEC-KI-053`'s locked remedies is `PARENT_BLOCKED`.
No correction may weaken an accepted oracle; E8.1 identical recovery is not a
correction.

## 8. Leaf dispatch protocol (two authorized waves)

Every dispatch includes the verbatim block text plus this file's path and
digest; the leaf reads its block and pinned revisions before editing; the
handoff quotes `subwindow_id`/`writable_file`/`starting_file_digest`.
`S2.active_subwindows` records the whole wave before any member begins. Wave
1 members are mutually independent and dispatch together; wave 2 dispatches
only after every wave-1 member is independently `ACCEPTED_FOR_INTEGRATION`;
`I119` runs only after every wave-2 member is accepted. No leaf communicates
with the parent, starts another leaf, or edits S1/S2/S3. The requester
performs all git commits; nothing here commits anything.

## 9. Mandatory decomposition-readiness checklist (standard §11)

### 9.1 Authority and inheritance

- [x] `SW-A01` Parent assignment `ASG-KI-W6-WA-14`, window-agent identity, and the two-wave delegation authority are exact and current (A5 state 184). Evidence: `EV-KI-W6-TC01`.
- [x] `SW-A02` Parent/sub-window standards plus contract, decision, checklist, and state revisions pinned and verified byte-equal this session. Evidence: `EV-KI-W6-TC01`.
- [x] `SW-A03` Parent write/read/action/prohibition/successor/stop boundaries copied without expansion into §1 and every block. Evidence: `EV-KI-W6-TC01`.
- [x] `SW-A04` Repositories, dirty state, and owner-controlled changes inventoried (§2; both nested repos clean; nine baselines + `ABSENT` verified). Evidence: `EV-KI-W6-TC01`.
- [x] `SW-A05` S1/S2/S3 exist with non-overlapping authorities. Evidence: `EV-KI-W6-TC02`.
- [x] `SW-A06` Strict adjacency enforced; parallel waves carry no subagent-to-subagent or subagent-to-parent channel; integration assessment is window-agent-only. Evidence: §3.2/§8.
- [x] `SW-A07` The inherited E8.1 sandbox-escalation and identical-recovery policy (limit 1) is copied into S1 §1 and S2 without expanding parent authority. Evidence: §1; `EV-KI-W6-TC01`.

### 9.2 Decision and file-set closure

- [x] `SW-D01` Every allocated requirement, invariant, decision, task, scenario, and case maps to exact files and assertions (§5 traces; §6 closure). Evidence: `EV-KI-W6-TC02`.
- [x] `SW-D02` No missing parent decision or contradictory authority remains (the six §0.1 interpretations are mechanical and cite governing text; `SRC-KI-055`'s inventory was independently reproduced this session). Evidence: `EV-KI-W6-TC01`.
- [x] `SW-D03` Required changed-file set equals planned initial file set (nine-path digest recomputed). Evidence: `EV-KI-W6-TC01`.
- [x] `SW-D04` Every planned file has exactly one leaf; no leaf owns more than one file. Evidence: `EV-KI-W6-TC02` (lint).
- [x] `SW-D05` Every file operation, starting digest, anchor, interface, preserved behavior, and forbidden edit is exact. Evidence: §3/§5.
- [x] `SW-D06` The graph is complete and acyclic; the two waves are justified by frozen §3.4 interfaces plus disjoint files/commands/resources; the wave-2 barrier and sequential `I119` are frozen. Evidence: §3.2/§3.3.
- [x] `SW-D07` Every cross-file interface is frozen before dependent execution (§3.4). Evidence: §3.4.
- [x] `SW-D08` Every intermediate state has exact permitted checks, expected temporary states, safety, resolver, and prohibitions (§3.3). Evidence: §3.3.
- [x] `SW-D09` Production and test files have separate leaves in separate waves (§3.1). Evidence: §3.1.
- [x] `SW-D10` No rename, multi-output generator, formatter, installer, or command can violate the one-file invariant (`node --check` writes nothing; `node --test` writes only disposable schemas in leaf-unique namespaces; `prisma migrate` is never run by a leaf — migrations already exist). Evidence: `EV-KI-W6-TC02`.

### 9.3 Sub-window execution completeness

- [x] `SW-E01` Every file sub-window contains every §7 field. Evidence: `EV-KI-W6-TC02` (lint).
- [x] `SW-E02` Every sub-window prescribes exact ordered edits; no broad verbs or alternatives remain. Evidence: §5.
- [x] `SW-E03` Every sub-window has exact preflight, local checks, activation witnesses, assertions, and forbidden outcomes. Evidence: §5.
- [x] `SW-E04` Every sub-window mechanically proves its attributable changed-file set is exactly one file. Evidence: §5 C1s.
- [x] `SW-E05` Every sub-window has exact evidence, handoff, stop, and successor-reservation rules. Evidence: §5 P/T/V/H; §8.
- [x] `SW-E06` Each subagent reports only to the window agent and cannot update subordinate or parent authority artifacts. Evidence: §1/§8.
- [x] `SW-E07` No sub-window requires successor work to satisfy its file-local acceptance. Evidence: §5.
- [x] `SW-E08` Deliberately deferred checks name the exact owning assessment (`I119` gates). Evidence: §5 DEFERRED notes.

### 9.4 Enforcement and integration closure

- [x] `SW-V01` Coverage cases are allocated to exact test files, registrations, activation witnesses, and assertions. Evidence: §6.
- [x] `SW-V02` Required local and whole-window case-set equality and digest checks are prescribed (§4; C142 certificate; CV89). Evidence: §4/§5.7/§5.10.
- [x] `SW-V03` Every critical invariant has a negative control at the narrowest effective level (`W6-NC-18`–`20` in C142, the sole suite that recomputes membership from source). Evidence: §5.7/§6.
- [x] `SW-V04` Test substitutes and accepted tests/fixtures have exact fidelity and invalidation rules (unit fakes claim only unit parity; isolated-Prisma tests claim real transaction behavior; the causal browser claims the assembled path — no lower level claims more). Evidence: CT23 item 7 copied at §5 heads; §5.7 read scope.
- [x] `SW-V05` The initial integration assessment is fully authored with zero implementation-file write authority. Evidence: §5.10.
- [x] `SW-V06` Frozen gates are exact, risk-proportionate, and scheduled once at the final assessment (CV84→CV90 ordering; CV87 only after CV86; CV88 only after CV87). Evidence: §5.10.
- [x] `SW-V07` Correction diagnosis, one-file corrective assignment, invalidation, and reassessment rules are complete. Evidence: §7.
- [x] `SW-V08` The window agent independently inspects every file handoff and personally executes every integration assessment. Evidence: §5.10; §8.
- [x] `SW-V09` Whole-window approval cannot pass through zero-work, skipped, filtered, duplicate, unexpected, unactivated, or summary-only evidence. Evidence: §5.10 I5/I9; CV89.
- [x] `SW-V10` Parent handoff contents and `READY_FOR_PARENT_REVIEW` boundary are exact. Evidence: §5.10 CH15.
- [x] `SW-V11` Every local gate distinguishes real failure from proven sandbox/channel invalidation and permits one identical escalated recovery without a parent round trip. Evidence: §1; CV87 clause.

### 9.5 Mechanical and adversarial audit

- [x] `SW-R01` All IDs (`C136`–`C144`, `I119`, `W6-DB-08`–`11`, `W6-NC-18`–`20`) are unique and all references resolve. Evidence: `EV-KI-W6-TC02` (lint).
- [x] `SW-R02` No unresolved placeholder exists in an assignable sub-window. Evidence: `EV-KI-W6-TC02` (lint).
- [x] `SW-R03` Single-file write-set lint rejects zero/two/wildcard/directory/rename/incidental outputs for every file sub-window. Evidence: `EV-KI-W6-TC02`.
- [x] `SW-R04` Removing one required file or requirement-to-file mapping makes readiness fail (nine-path digest and §6 closure break). Evidence: `EV-KI-W6-TC02` (falsification pass).
- [x] `SW-R05` Removing, duplicating, skipping, filtering, or bypassing one required coverage case makes acceptance fail (C142 set-equality; CV89 union digest). Evidence: §5.7/§5.10.
- [x] `SW-R06` Weakening an oracle or diverging a substitute invalidates acceptance evidence (controls `W6-NC-18`–`20`; §7 no-weakening rule). Evidence: §5.7/§7.
- [x] `SW-R07` Simulated second-file edit and direct parent communication are rejected (C1 checks; §8 prohibitions). Evidence: `EV-KI-W6-TC02` (falsification pass).
- [x] `SW-R08` Simulated integration failure cannot be repaired by the window agent without a new corrective sub-window (§7; §5.10 zero-write authority). Evidence: §7.
- [x] `SW-R09` Parent decomposition review is recorded before the first implementation assignment (S2 `AWAITING_PARENT_DECOMPOSITION_REVIEW`; this checklist gates dispatch). Evidence: §8; S2.
- [x] `SW-R10` Document lint reports zero missing fields, mappings, cases, evidence references, or authority conflicts. Evidence: `EV-KI-W6-TC02`.
- [x] `SW-R11` Simulated sandbox denial proceeds to one identical escalated recovery, while a changed command, observable test failure, or external action is rejected. Evidence: §1; `EV-KI-W6-TC02` (falsification pass).

## 10. Certificate templates

The §12.1 `SUBWINDOW-DECOMPOSITION-READY` certificate (S3) carries
`initial_subwindow_ids: [KI-W6-C136 … KI-W6-C144]` (nine, in ID order),
`initial_subwindow_count: 9`, `planned_file_set` = the nine §3.1 paths,
`planned_file_set_digest:
ba4ccba7b65016b486dc2e1160bcc11a2cb08d306aff4945fad0022e3f19ad92`,
`unmapped_*` and `unresolved_*` arrays all empty,
`mandatory_authoring_items_checked: 47`,
`mandatory_authoring_items_unchecked: 0`, `first_subwindow: KI-W6-WAVE-1`
(all five members; no intra-wave order), `integration_assessment_id:
KI-W6-I119`, `parent_review_required: true`. Leaf execution certificates
(§12.3) and the window-agent integration certificate (§12.4) follow the
sub-window standard templates verbatim with the KI-W6 IDs and the §4 case
digests.

## 11. Amendment sections (initially empty; append-only)

### 11.1 Corrective sub-windows

(none)

### 11.2 Later integration assessments

(none)

## 12. State-186 append-only amendment — terminal lease-monitor lifecycle

This section is append-only under parent assignment `ASG-KI-W6-WA-15` and
mechanically decomposes `DEC-KI-054`, parent tasks `KI-W6-CT24`–`CT27`,
scenario `SCN-KI-045`, case `W6-DB-12`, control `W6-NC-21`, and assessment
`KI-W6-I120`. It does not rewrite or reopen accepted `C136`–`C144`; it
supersedes only `I119`'s blocked continuation after `CV87` through the new
assessment `I120`. No leaf may begin until the parent approves this exact S1
revision and the window agent records that approval in S2/S3.

### 12.1 Inherited authority, package, and exact boundary

```yaml
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-15
window_agent_identity: KI-W6-WINDOW-AGENT
parent_standard_path: PROJECT_AGNOSTIC_DECISION_COMPLETE_CHECKLIST_AUTHORING_STANDARD.md
parent_standard_revision: cda352017e75c0d11f6797d9fbe108b4365508cd38b0e92365cfb523ede32848
subwindow_standard_path: PROJECT_AGNOSTIC_WINDOW_AGENT_SUBWINDOW_AUTHORING_STANDARD.md
subwindow_standard_revision: 842c29550c06c22d63e0a058a27cb8a9ff6b538b3168d2c83a384890b44247f0
A1: KEYWORD_INTELLIGENCE_PRODUCT_CONTRACT.md
A1_revision: 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c
A2: KEYWORD_INTELLIGENCE_DISCOVERY_DOSSIER.md
A2_revision: 425bedd9a7f429e2b145559d6d408fd161260a025382e047900f2112355316e0
A3: KEYWORD_INTELLIGENCE_DECISION_LEDGER.md
A3_revision: 412e58dffc326e43a6c3efaae5e2b18a9a1fd65841bcd66e34c0b7fcc161d183
A4: KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md
A4_revision: aaa15feedebe70d93284a87c4eb480593992481a51ce00ea7f838eb9e802dabc
A5: ACTIVE_EXECUTION_STATE.md
A5_state: 186
A6: KEYWORD_INTELLIGENCE_EXECUTION_EVIDENCE.md
A7: KEYWORD_INTELLIGENCE_SPECIFICATION_CHANGELOG.md
A8: KEYWORD_INTELLIGENCE_TRACEABILITY_INDEX.md
A8_revision: ac7165d143a786b65ee20681feb8be07009911113a29a34cc6e329dcfb605399
S1: KEYWORD_INTELLIGENCE_KI_W6_SUBWINDOW_CHECKLIST.md
S2: KEYWORD_INTELLIGENCE_KI_W6_TRANSACTION_CLOCK_SUBWINDOW_STATE.md
S3: KEYWORD_INTELLIGENCE_KI_W6_TRANSACTION_CLOCK_SUBWINDOW_EVIDENCE.md
trigger_evidence: [SRC-KI-056, EV-KI-W6-TC06]
governing_decision: DEC-KI-054
parent_tasks: [KI-W6-CT24, KI-W6-CT25, KI-W6-CT26, KI-W6-CT27]
scenario: SCN-KI-045
coverage_case: W6-DB-12
negative_control: W6-NC-21
accepted_predecessors: [KI-W6-C136, KI-W6-C137, KI-W6-C138, KI-W6-C139, KI-W6-C140, KI-W6-C141, KI-W6-C142, KI-W6-C143, KI-W6-C144]
preserved_assessment_evidence: [KI-W6-CV84, KI-W6-CV85, KI-W6-CV86]
failed_assessment_evidence: KI-W6-CV87
successor_parent_window: PROHIBITED
may_start_successor: false
```

Parent scope is exactly four implementation/test paths plus S1/S2/S3
coordination. It prohibits schema/migration, repository fence/transaction,
lease duration/heartbeat interval, retry, queue, provider, AWS, production,
paid, frontend, package/configuration, build-script, commit/push, and KI-W7
changes. Local syntax/tests, one dependency-gated isolated-database reuse or
rerun, one durable causal browser gate, regression/build/privacy/scope gates,
and sandbox escalation for those already-authorized local actions are allowed.
An attempt invalidated solely by sandbox or channel transport may receive one
identical escalated recovery only after the inherited E8.1 read-only
postcondition proof; an observable assertion/product failure is never such a
recovery.

State-186 entry was independently reproduced: all pinned revisions above
match; backend is clean at
`8694b949bc4e308a7605074047cc330e2a2d8b44`; frontend is clean at
`f981b34eeb79764a2e9e7ee96779f99907228a3f`; the four writable targets are
regular non-symlink files with the exact baselines in §12.2; root porcelain
contains only the seven owner-controlled parent artifacts present before this
amendment, with sorted-line digest
`84ed43672dd873536e36a2903cc9950bb1efbad22c453dfb46f39ea75b1e8f49`.
The only window-agent writes authorized during decomposition are S1/S2/S3.

### 12.2 Complete four-file set, DAG, and intermediate states

| Path | Operation | Starting SHA-256 | Owner |
|---|---|---|---|
| `email_scraper/src/aws-pipeline/core/lease-monitor.js` | MODIFY | `cb0332470928fb33d59529544ac6a6c0b1adbcaa1d5a5a69cd80ee8fd55398be` | `KI-W6-C145` |
| `email_scraper/src/aws-pipeline/services/discovery-worker.js` | MODIFY | `5ff0bd6c727da335422abccd336e87ae441c453e2bf63ef20c6189b278c60874` | `KI-W6-C146` |
| `email_scraper/src/aws-pipeline/services/lead-worker.js` | MODIFY | `db616bccbd283c3f5488fd3458e6d86a1b57f945ac722cdf0935c95ccfb20d26` | `KI-W6-C147` |
| `email_scraper/test/aws-pipeline-transaction-clock-enforcement.test.js` | MODIFY | `606d8e90e7a8045ddf0ae9bb374e6b2390a80491770a252c75d44b725e1b0448` | `KI-W6-C148` |

Required changed-file set = planned set = the four rows above. The sorted
distinct workspace-relative path plus LF digest is
`e556d60d1253045b8193f683f86e9622118cf00f52a076011d2917c6da416fe4`.
There are zero duplicate owners and zero multi-file leaves.

```text
KI-W6-C145
    |
    +-- KI-W6-WAVE-3 (parallel only after C145 is independently accepted)
    |      KI-W6-C146       KI-W6-C147
    |          \             /
    +----------- barrier: both independently accepted
                         |
                     KI-W6-C148
                         |
                     KI-W6-I120 (window agent, sequential, no implementation writes)
                         |
                 READY_FOR_PARENT_REVIEW; stop before KI-W7
```

Wave 3 is the sole authorized parallel wave. C146 and C147 own disjoint files,
consume the already accepted C145 export, run read-only syntax/source checks,
share no writable fixture/schema/port/process/build output, and do not consume
one another's output. S2 must record both assignments before either starts.
The window agent must independently accept both before C148 starts.

Intermediate-state contract:

- After C145: the new export has zero callers. Only C145's syntax and exact
  helper-byte checks are required to pass; worker behavior remains unchanged.
  This is local/uncommitted and externally invisible. Wave 3 resolves the
  temporary zero-caller state. No integration, provider/AWS, parent handoff,
  commit, or KI-W7 action is allowed.
- After one Wave-3 member returns: the sibling may still be running; no
  dependent leaf or integration gate starts. Each changed worker consumes the
  same frozen helper interface independently. The window agent accepts or
  rejects each file separately.
- After both Wave-3 members are accepted: production ordering is present, but
  `W6-DB-12/W6-NC-21` are not registered until C148. Syntax/source checks must
  pass; enforcement and all causal claims remain pending. C148 resolves this.
- After C148: the four-file implementation is assembled. Only I120 may execute
  whole-window gates. Leaves cannot claim causal browser, regression, build,
  privacy, database, or parent acceptance.

Frozen interface consumed by C146/C147 and enforced by C148:

```js
export async function preparePipelineTerminalLease(monitor) {
  await monitor.renewNow();
  await monitor.stop();
  monitor.assertActive();
}
```

It accepts exactly one `monitor`, resolves `undefined`, and adds no default,
return object, catch, suppression, retry, timeout, timer/clock mutation,
validation branch, or export. It runs outside transactions. Renewal/prior
failure aborts before terminalization; successful return means the explicit
renewal and any previously queued renewal settled, the timer was cleared, and
stored failure was rethrown if present. Existing terminal token/fingerprint/
state/live-expiry fences and recovery semantics remain unchanged.

### 12.3 `KI-W6-C145` — shared terminal lease boundary

```yaml
subwindow_id: KI-W6-C145
type: CORRECTION
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-15
assigned_agent: UNASSIGNED
predecessors: [KI-W6-I119 PARENT_BLOCKED at CV87, DEC-KI-054]
successor_reserved_for: KI-W6-WINDOW-AGENT
writable_file: email_scraper/src/aws-pipeline/core/lease-monitor.js
file_operation: MODIFY
starting_file_digest: cb0332470928fb33d59529544ac6a6c0b1adbcaa1d5a5a69cd80ee8fd55398be
starting_repository_change_set: []
starting_repository_change_set_digest: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
read_only_scope:
  - ACTIVE_EXECUTION_STATE.md state 186
  - KEYWORD_INTELLIGENCE_DECISION_LEDGER.md DEC-KI-054
  - KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md KI-W6-CT24/I120
  - email_scraper/src/aws-pipeline/core/lease-monitor.js
  - email_scraper/src/aws-pipeline/services/discovery-worker.js
  - email_scraper/src/aws-pipeline/services/lead-worker.js
  - email_scraper/test/aws-pipeline-contracts.test.js lease-monitor tests
authorized_actions: [edit the one writable file, read-only syntax/diff/source inspections, return evidence to the window agent]
prohibited_actions: [second-file edit, worker caller edit, test execution that writes workspace state, external/database/provider/AWS action, commit, push, direct parent communication, successor work]
may_start_successor: false
```

Mechanical trace: `REQ-KI-010`–`REQ-KI-015`, `REQ-KI-024`;
`INV-KI-004`–`INV-KI-006`, `INV-KI-010`, `INV-KI-011`, `INV-KI-015`;
`SRC-KI-056`, `EV-KI-W6-TC06`, `DEC-KI-054`, `KI-W6-CT24`,
`SCN-KI-045`, `W6-DB-12`, `W6-NC-21` -> exact export above -> C146/C147
call sites -> C148 dynamic/source assertions.

Ordered transformation:

1. Preserve the complete existing `createPipelineLeaseMonitor` export
   byte-for-byte.
2. Immediately after it, add exactly the five-line exported helper shown in
   §12.2, including the three statements in that order.
3. Add no import, validation, default, return, catch, suppression, retry,
   timeout, timer/clock change, extra export, or other edit.

LOCAL_NOW checks, from `email_scraper/`, write set empty:

1. `node --check src/aws-pipeline/core/lease-monitor.js` -> exit 0.
2. `git diff --check -- src/aws-pipeline/core/lease-monitor.js` -> exit 0.
3. Deterministic source inspection must read the file as UTF-8, require the
   exact helper literal in §12.2 exactly once, require its index after
   `createPipelineLeaseMonitor`, require total occurrences of
   `preparePipelineTerminalLease` = 1, and prove deletion of that literal
   makes the inspection fail. Activation witness: exact helper bytes and
   ordering. Forbidden outcomes: a changed existing monitor byte or any extra
   helper behavior.
4. Compare backend porcelain before/after and file digests: attributable
   workspace path set is exactly `{email_scraper/src/aws-pipeline/core/lease-monitor.js}`;
   all previously clean non-owned paths remain clean.

Coverage registration is deferred to C148; causal proof is deferred to I120.

- [ ] `P1` Revisions, `ASG-KI-W6-C145`, writable file, baseline digest, and predecessor evidence match.
- [ ] `P2` Backend starts clean at `8694b949…`; root owner-controlled state is preserved.
- [ ] `T1` Apply all three ordered transformation steps and no other edit.
- [ ] `V1` Run all four LOCAL_NOW checks and record activation witnesses/assertions.
- [ ] `V2` Prove the attributable workspace changed-file set is exactly the writable file.
- [ ] `V3` Record local coverage as none and the exact C148/I120 deferred obligations; zero invented registration.
- [ ] `H1` Return exact diff, ending digest, commands/outcomes, and deferred obligations.
- [ ] `H2` Confirm no prohibited action, second-file edit, successor work, external mutation, or parent communication.
- [ ] `H3` Stop at `AWAITING_WINDOW_REVIEW` and report only to the window agent.

### 12.4 `KI-W6-C146` — discovery terminal ordering

```yaml
subwindow_id: KI-W6-C146
type: CORRECTION
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-15
assigned_agent: UNASSIGNED
predecessors: [KI-W6-C145 independently accepted]
parallel_wave: KI-W6-WAVE-3
successor_reserved_for: KI-W6-WINDOW-AGENT
writable_file: email_scraper/src/aws-pipeline/services/discovery-worker.js
file_operation: MODIFY
starting_file_digest: 5ff0bd6c727da335422abccd336e87ae441c453e2bf63ef20c6189b278c60874
starting_repository_change_set: [src/aws-pipeline/core/lease-monitor.js]
starting_repository_change_set_digest: e1304b502505ff5503e382d7a144d17bf6ae810f65a160ee600b1e675888cf10
read_only_scope:
  - ACTIVE_EXECUTION_STATE.md state 186
  - KEYWORD_INTELLIGENCE_DECISION_LEDGER.md DEC-KI-054
  - KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md KI-W6-CT25/I120
  - email_scraper/src/aws-pipeline/core/lease-monitor.js accepted C145 export
  - email_scraper/src/aws-pipeline/services/discovery-worker.js
  - email_scraper/test/aws-pipeline-discovery.test.js
  - email_scraper/test/aws-pipeline-transaction-clock-enforcement.test.js
authorized_actions: [edit the one writable file, read-only syntax/diff/source inspections, return evidence to the window agent]
prohibited_actions: [lease-monitor edit, lead-worker edit, test edit, second-file edit, provider/AWS/database action, commit, push, direct parent communication, successor work]
may_start_successor: false
```

Mechanical trace: `REQ-KI-010`–`REQ-KI-015`, `REQ-KI-024`;
`INV-KI-004`–`INV-KI-006`, `INV-KI-010`, `INV-KI-011`, `INV-KI-015`;
`SRC-KI-056`, `EV-KI-W6-TC06`, `DEC-KI-054`, `KI-W6-CT25`,
`SCN-KI-045`, `W6-DB-12`, `W6-NC-21` -> exact discovery import/call/order
anchors -> C148's source and dynamic assertions -> I120 causal proof.

Ordered transformation inside the exact exported
`processDiscoveryMessage(message, runtime)` function:

1. Add `preparePipelineTerminalLease` beside
   `createPipelineLeaseMonitor` in the existing import from
   `../core/lease-monitor.js`; no second lease-monitor import.
2. Replace the sole success-path `await monitor.renewNow();` immediately before
   the existing `recordTerminal` call with
   `await preparePipelineTerminalLease(monitor);`.
3. Delete only the success-path `await monitor.stop();` immediately after that
   `recordTerminal` call.
4. Preserve manifest/artifact/provider logic, terminal token/fingerprint/state
   and `new Date()` arguments, busy/cancelled/terminal early returns,
   dispatcher payload/order, return union, catch cleanup, 20-second/60-second
   values, repository behavior, and every other byte.

Resulting order is artifact validated/written -> helper renew/stop/drain/assert
-> fenced terminal transaction -> existing aggregation-check `sendOne` ->
acknowledge. Helper failure prevents terminal/check; terminal failure follows
unchanged catch cleanup; after a recorded terminal no live heartbeat exists.

LOCAL_NOW checks, from `email_scraper/`, write set empty:

1. `node --check src/aws-pipeline/services/discovery-worker.js` -> exit 0.
2. `git diff --check -- src/aws-pipeline/services/discovery-worker.js` -> exit 0.
3. Deterministic inspection of the exact exported-function span requires:
   import occurrence = 1, helper invocation occurrence = 1, direct
   `monitor.renewNow()` occurrence = 0, helper index < `recordTerminal` index <
   domain-aggregation dispatcher `sendOne` index, and the slice from
   `recordTerminal` through that send contains zero `monitor.stop()`. It also
   requires the unchanged catch cleanup stop. Replacing the helper call with
   direct renewal plus a post-terminal stop must make the inspection fail;
   the real source must pass immediately afterward.
4. Attributable workspace path set is exactly the writable file; C145's file
   digest is protected and the Wave-3 sibling's attributable edit is ignored
   only as its separately recorded ownership, never attributed to C146.

Runtime/certificate proof is deferred to C148/I120.

- [ ] `P1` Revisions, `ASG-KI-W6-C146`, writable file, baseline, C145 acceptance, and Wave-3 state match.
- [ ] `P2` Starting repository set is exactly the recorded C145 path; protected/sibling changes are preserved.
- [ ] `T1` Apply the four ordered transformations and no other edit.
- [ ] `V1` Run all four LOCAL_NOW checks with exact source-order witnesses.
- [ ] `V2` Prove the attributable changed-file set is exactly the writable file.
- [ ] `V3` Record no local case registration; preserve exact C148/I120 deferred proof.
- [ ] `H1` Return exact diff, ending digest, commands/outcomes, and deferred obligations.
- [ ] `H2` Confirm no prohibited action, second-file edit, successor work, external mutation, sibling communication, or parent communication.
- [ ] `H3` Stop at `AWAITING_WINDOW_REVIEW` and report only to the window agent.

### 12.5 `KI-W6-C147` — lead terminal ordering

```yaml
subwindow_id: KI-W6-C147
type: CORRECTION
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-15
assigned_agent: UNASSIGNED
predecessors: [KI-W6-C145 independently accepted]
parallel_wave: KI-W6-WAVE-3
successor_reserved_for: KI-W6-WINDOW-AGENT
writable_file: email_scraper/src/aws-pipeline/services/lead-worker.js
file_operation: MODIFY
starting_file_digest: db616bccbd283c3f5488fd3458e6d86a1b57f945ac722cdf0935c95ccfb20d26
starting_repository_change_set: [src/aws-pipeline/core/lease-monitor.js]
starting_repository_change_set_digest: e1304b502505ff5503e382d7a144d17bf6ae810f65a160ee600b1e675888cf10
read_only_scope:
  - ACTIVE_EXECUTION_STATE.md state 186
  - KEYWORD_INTELLIGENCE_DECISION_LEDGER.md DEC-KI-054
  - KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md KI-W6-CT26/I120
  - email_scraper/src/aws-pipeline/core/lease-monitor.js accepted C145 export
  - email_scraper/src/aws-pipeline/services/lead-worker.js
  - email_scraper/test/aws-pipeline-transaction-clock-enforcement.test.js
authorized_actions: [edit the one writable file, read-only syntax/diff/source inspections, return evidence to the window agent]
prohibited_actions: [lease-monitor edit, discovery-worker edit, test edit, second-file edit, provider/AWS/database action, commit, push, direct parent communication, successor work]
may_start_successor: false
```

Mechanical trace: `REQ-KI-010`–`REQ-KI-015`, `REQ-KI-024`;
`INV-KI-004`–`INV-KI-006`, `INV-KI-010`, `INV-KI-011`, `INV-KI-015`;
`SRC-KI-056`, `EV-KI-W6-TC06`, `DEC-KI-054`, `KI-W6-CT26`,
`SCN-KI-045`, `W6-DB-12`, `W6-NC-21` -> exact lead import/call/order anchors
-> C148's source and dynamic assertions -> I120 causal proof.

Ordered transformation inside exact exported
`processLeadMessage(message, runtime)`:

1. Add `preparePipelineTerminalLease` beside
   `createPipelineLeaseMonitor` in the existing lease-monitor import; no second
   import.
2. Replace the sole success-path `await monitor.renewNow();` immediately before
   terminal-state derivation and `recordTerminal` with
   `await preparePipelineTerminalLease(monitor);`.
3. Delete only the success-path `await monitor.stop();` immediately after
   `recordTerminal`.
4. Preserve manifest/candidate/artifact/provider/marker logic, token/
   fingerprint/terminal state/safe-error/`new Date()` arguments, busy/
   cancelled/terminal early returns, dispatcher payload/order, return union,
   catch cleanup, timing and repository behavior. No Browserless, AI,
   page-fetch, artifact, cost, or ambiguity rule changes.

Resulting success/failure/replay semantics and order are identical to C146,
with the existing lead aggregation-check destination preserved.

LOCAL_NOW checks, from `email_scraper/`, write set empty:

1. `node --check src/aws-pipeline/services/lead-worker.js` -> exit 0.
2. `git diff --check -- src/aws-pipeline/services/lead-worker.js` -> exit 0.
3. Deterministic inspection of `processLeadMessage` requires: helper import =
   1, helper invocation = 1, direct `monitor.renewNow()` = 0, helper index <
   terminal-state derivation < `recordTerminal` < lead-aggregation `sendOne`,
   and zero `monitor.stop()` from `recordTerminal` through send. Existing
   early-return/catch cleanup stops remain. The same renew->terminal->stop
   in-memory mutation must fail; fresh real source must pass.
4. Attributable workspace path set is exactly the writable file; C145 and the
   separately owned C146 path are protected from attribution.

Runtime/certificate proof is deferred to C148/I120.

- [ ] `P1` Revisions, `ASG-KI-W6-C147`, writable file, baseline, C145 acceptance, and Wave-3 state match.
- [ ] `P2` Starting repository set is exactly the recorded C145 path; protected/sibling changes are preserved.
- [ ] `T1` Apply the four ordered transformations and no other edit.
- [ ] `V1` Run all four LOCAL_NOW checks with exact source-order witnesses.
- [ ] `V2` Prove the attributable changed-file set is exactly the writable file.
- [ ] `V3` Record no local case registration; preserve exact C148/I120 deferred proof.
- [ ] `H1` Return exact diff, ending digest, commands/outcomes, and deferred obligations.
- [ ] `H2` Confirm no prohibited action, second-file edit, successor work, external mutation, sibling communication, or parent communication.
- [ ] `H3` Stop at `AWAITING_WINDOW_REVIEW` and report only to the window agent.

### 12.6 `KI-W6-C148` — lifecycle enforcement

```yaml
subwindow_id: KI-W6-C148
type: CORRECTION
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-15
assigned_agent: UNASSIGNED
predecessors: [KI-W6-C145, KI-W6-C146, KI-W6-C147 independently accepted]
successor_reserved_for: KI-W6-WINDOW-AGENT
writable_file: email_scraper/test/aws-pipeline-transaction-clock-enforcement.test.js
file_operation: MODIFY
starting_file_digest: 606d8e90e7a8045ddf0ae9bb374e6b2390a80491770a252c75d44b725e1b0448
starting_repository_change_set:
  - src/aws-pipeline/core/lease-monitor.js
  - src/aws-pipeline/services/discovery-worker.js
  - src/aws-pipeline/services/lead-worker.js
starting_repository_change_set_digest: f2e8606cb5be884ffc116fedde48a0addfaa45535f9a0bfcb86b4ca498e4dd5f
read_only_scope:
  - ACTIVE_EXECUTION_STATE.md state 186
  - KEYWORD_INTELLIGENCE_DECISION_LEDGER.md DEC-KI-054
  - KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md KI-W6-CT27/I120
  - email_scraper/src/aws-pipeline/core/lease-monitor.js accepted C145 output
  - email_scraper/src/aws-pipeline/services/discovery-worker.js accepted C146 output
  - email_scraper/src/aws-pipeline/services/lead-worker.js accepted C147 output
  - email_scraper/test/aws-pipeline-transaction-clock-enforcement.test.js
authorized_actions: [edit the one writable test file, run its read-only syntax and focused Node test, use only in-memory fake timer/deferred state, return evidence to the window agent]
prohibited_actions: [production edit, second-file edit, real timer wait, database/provider/AWS action, fixture write, snapshot update, commit, push, direct parent communication, successor work]
may_start_successor: false
```

Mechanical trace: `REQ-KI-010`–`REQ-KI-015`, `REQ-KI-024`;
`INV-KI-004`–`INV-KI-006`, `INV-KI-010`, `INV-KI-011`, `INV-KI-015`;
`SRC-KI-056`, `EV-KI-W6-TC06`, `DEC-KI-054`, `KI-W6-CT27`,
`SCN-KI-045`, `W6-DB-12`, `W6-NC-21` -> exact test registrations,
activation witnesses, negative control, certificate -> I120's 40/21 closure.

Ordered transformation:

1. Import `createPipelineLeaseMonitor` and
   `preparePipelineTerminalLease` from the exact lease-monitor source.
2. Add exact constants for
   `../src/aws-pipeline/core/lease-monitor.js`,
   `../src/aws-pipeline/services/discovery-worker.js`, and
   `../src/aws-pipeline/services/lead-worker.js`; load all three in the existing
   top-level `Promise.all` inventory and expose them in `REAL` without removing
   existing source members.
3. Set `REQUIRED` exactly to
   `['W6-DB-08','W6-DB-09','W6-DB-10','W6-DB-11','W6-DB-12']` and `CONTROLS`
   exactly to
   `['W6-NC-18','W6-NC-19','W6-NC-20','W6-NC-21']` in that order. Replace the
   required digest with
   `1aba569c8f08f9ca3ee240a10c4ddb4fbb0e6ec0bb00608b74aa414faefaaf39`
   and control digest with
   `3068f94cf9c935bfdec5f0374182c5261fc0acaf7e5d8bf80d6b278cfa5b981c`.
4. Extend witnesses with exact initial numeric members
   `terminalLeaseWorkers: 0`, `terminalLeaseRenewals: 0`, and
   `terminalLeaseTimerClears: 0`; preserve prior witness members.
5. Add one reusable source oracle for the exact exported
   `processDiscoveryMessage` and `processLeadMessage` spans. For each, require
   one helper import, one helper call, zero direct `monitor.renewNow()`, helper
   call index < `recordTerminal` index < the existing aggregation dispatcher
   `sendOne` index, and zero `monitor.stop()` between terminal and send; allow
   only existing cleanup stops outside that interval. It sets
   `terminalLeaseWorkers` to exactly 2 only after both pass.
6. Register `W6-DB-12` through `runRequired`. Use the real monitor/helper with
   a controlled valid Date clock, fake `setIntervalFn` capturing exactly one
   callback/token, fake `clearIntervalFn` asserting and counting that token,
   and a renewal function whose first invocation appends start then waits on a
   deferred release and whose second invocation appends start/completion.
   Invoke the captured timer to queue renewal 1; start without awaiting the
   helper to queue explicit renewal 2; release renewal 1; await the helper.
   Assert serialized ordered completion of exactly two renewals, exactly one
   clear, final `monitor.assertActive()` success, and source oracle success.
   Invoke the captured stale callback after the simulated terminal boundary,
   await exactly two `Promise.resolve()` microtasks, and assert renewal count
   remains 2. Set witnesses to workers=2, renewals=2, clears=1.
7. Register `W6-NC-21`. Mutate only an in-memory copy of discovery source by
   replacing its helper call with direct `await monitor.renewNow();` and
   inserting `await monitor.stop();` between terminalization and check send.
   Assert the unchanged W6-DB-12 source oracle throws; append the control ID;
   run the unmodified REAL source oracle immediately and require pass. Never
   write the mutated bytes.
8. Update the certificate to require 5 required/registered/executed cases,
   zero skips/failures/duplicates/unexpected IDs; 4 expected/falsified controls
   with the exact IDs; activation witnesses exactly
   `{coordinatorTransactions:11, runRepositoryTransactions:21,
   assertionClockSites:9, serviceCallers:5, terminalLeaseWorkers:2,
   terminalLeaseRenewals:2, terminalLeaseTimerClears:1}`; and the two new
   group digests for required/registered/executed/control sets. Preserve every
   earlier oracle and test. File total is exactly 10 tests: five cases, four
   controls, one certificate.

LOCAL_NOW checks from `email_scraper/`, expected workspace write set empty:

1. `node --check test/aws-pipeline-transaction-clock-enforcement.test.js` ->
   exit 0.
2. `node --test test/aws-pipeline-transaction-clock-enforcement.test.js` ->
   exactly 10 pass, 0 fail, 0 skip; exact five-case/four-control certificate;
   2/2/1 new witnesses; W6-NC-21 falsifies then fresh REAL passes.
3. `git diff --check -- test/aws-pipeline-transaction-clock-enforcement.test.js`
   -> exit 0; attributable workspace path set exactly the writable test file;
   accepted C145–C147 digests protected.

- [ ] `P1` Revisions, `ASG-KI-W6-C148`, writable file, baseline, and all three accepted predecessor digests match.
- [ ] `P2` Starting repository set is exactly the recorded three production paths.
- [ ] `T1` Apply all eight ordered transformations and preserve every prior case/control/oracle.
- [ ] `V1` Run all three LOCAL_NOW checks and capture exact activation/certificate output.
- [ ] `V2` Prove the attributable changed-file set is exactly the writable test file.
- [ ] `V3` Prove local required=registered=executed exact five IDs, zero skips/duplicates/unexpected, and four/four controls falsified.
- [ ] `H1` Return exact diff, ending digest, command outcomes, certificate, and I120 obligations.
- [ ] `H2` Confirm no prohibited action, second-file edit, production mutation, successor work, external mutation, or parent communication.
- [ ] `H3` Stop at `AWAITING_WINDOW_REVIEW` and report only to the window agent.

### 12.7 Coverage, controls, fidelity, and immutable accepted evidence

This correction adds exactly `W6-DB-12` and `W6-NC-21`. The enforcement group
is exactly `W6-DB-08`–`W6-DB-12`, digest
`1aba569c8f08f9ca3ee240a10c4ddb4fbb0e6ec0bb00608b74aa414faefaaf39`.
Its controls are exactly `W6-NC-18`–`W6-NC-21`, digest
`3068f94cf9c935bfdec5f0374182c5261fc0acaf7e5d8bf80d6b278cfa5b981c`.

Final W6 required cases are exactly:

```text
W6-NAV-01 W6-NAV-02 W6-NAV-03
W6-CONF-01 W6-CONF-02 W6-CONF-03 W6-CONF-04 W6-CONF-05 W6-CONF-06
W6-FLOW-01 W6-FLOW-02 W6-FLOW-03 W6-FLOW-04 W6-FLOW-05 W6-FLOW-06 W6-FLOW-07 W6-FLOW-08 W6-FLOW-09 W6-FLOW-10 W6-FLOW-11 W6-FLOW-12 W6-FLOW-13
W6-RES-01 W6-RES-02 W6-RES-03 W6-RES-04
W6-TXN-01 W6-TXN-02
W6-DB-01 W6-DB-02 W6-DB-03 W6-DB-04 W6-DB-05 W6-DB-06 W6-DB-07 W6-DB-08 W6-DB-09 W6-DB-10 W6-DB-11 W6-DB-12
```

Count = 40; sorted-member-plus-LF digest =
`334999de9923c0af40fa46b1c99eb92b03efce978585a71ff6b031092d105b71`.
Final controls are exactly `W6-NC-01` through `W6-NC-21`; count = 21;
digest =
`66921e9aae67f455bc35678da9b6ba659165dd037856d437b91c11b3c07fde80`.
I120 must prove required=registered=executed and every control falsified with a
fresh positive. Removing, skipping, filtering, duplicating, adding, or failing
to activate any member makes closure fail.

Fake timer/deferred behavior in C148 proves only monitor scheduling and source
ordering; it cannot claim Prisma, browser, provider, or deployment parity.
Existing accepted C142 cases/oracles are immutable except the additive
registries/digests/witness members and exact new W6-DB-12/W6-NC-21 blocks.
The unchanged causal browser supplies assembled local parity. No fixture,
substitute, existing browser registration, or accepted database test changes.

### 12.8 `KI-W6-I120` — corrective integration assessment and automatic continuation

```yaml
subwindow_id: KI-W6-I120
type: INTEGRATION_ASSESSMENT
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-15
assigned_agent: KI-W6-WINDOW-AGENT
predecessors: [KI-W6-C145, KI-W6-C146, KI-W6-C147, KI-W6-C148 independently accepted]
authorized_write_file: NONE
coordination_writes: [KEYWORD_INTELLIGENCE_KI_W6_TRANSACTION_CLOCK_SUBWINDOW_STATE.md, KEYWORD_INTELLIGENCE_KI_W6_TRANSACTION_CLOCK_SUBWINDOW_EVIDENCE.md]
expected_changed_file_set:
  - email_scraper/src/aws-pipeline/core/lease-monitor.js
  - email_scraper/src/aws-pipeline/services/discovery-worker.js
  - email_scraper/src/aws-pipeline/services/lead-worker.js
  - email_scraper/test/aws-pipeline-transaction-clock-enforcement.test.js
expected_changed_file_set_digest: e556d60d1253045b8193f683f86e9622118cf00f52a076011d2917c6da416fe4
required_case_count: 40
required_case_digest: 334999de9923c0af40fa46b1c99eb92b03efce978585a71ff6b031092d105b71
negative_control_count: 21
negative_control_digest: 66921e9aae67f455bc35678da9b6ba659165dd037856d437b91c11b3c07fde80
may_start_successor: false
```

Execute personally and sequentially; successful boundaries are not stop
points:

- [ ] `KI-W6-CV91` Independently review and accept C145–C148; recompute their
  ending digests; inspect complete diffs; prove attributable paths equal the
  exact four-path set/digest above; prove accepted C136–C144 inputs are
  byte-identical to backend HEAD `8694b949bc4e308a7605074047cc330e2a2d8b44`.
- [ ] `KI-W6-CV92` From `email_scraper/`, run `node --check` separately on
  `src/aws-pipeline/core/lease-monitor.js`,
  `src/aws-pipeline/services/discovery-worker.js`,
  `src/aws-pipeline/services/lead-worker.js`, and
  `test/aws-pipeline-transaction-clock-enforcement.test.js`; then run exactly
  `node --test test/aws-pipeline-transaction-clock-enforcement.test.js`.
  Require 10/10/0, exact five-case/four-control certificate, 2/2/1 lifecycle
  witnesses, W6-NC-21 failure on mutated source, and immediate fresh REAL pass.
- [ ] `KI-W6-CV93` From `email_scraper/`, run exactly
  `node --test test/aws-pipeline-contracts.test.js test/aws-pipeline-discovery.test.js test/aws-pipeline-transaction-clock-enforcement.test.js`.
  Require 26 pass, 0 fail, 0 skip after C148 (11 contracts + 5 discovery + 10
  enforcement), W6-DB-12 active, existing monitor serialization/loss and
  discovery terminal behavior unchanged. Reuse I119 CV86 only when all seven
  complete input hashes remain exact:
  `pipeline-coordinator-repository.integration.test.js=9689ef9f5acbe7a68de1b224553c5dcf753fb618fe1dcfbfed3711046ea8b559`,
  `aws-pipeline-domain.integration.test.js=e1f10225fb301c9b798032e70fa2bc57c38de5e7374f8c419b7b3928104f3779`,
  `aws-pipeline-lead-aggregation.integration.test.js=020cafb8684a9cb9d7cd6bcb307a896f5ef363ee478b4a12be781cada609ac71`,
  `aws-pipeline-traffic.integration.test.js=3f8af953c1bee9150cea9be422ac867c7a39737c3a4e8a4b6dcd4a737b78cdfd`,
  `aws-pipeline-final.integration.test.js=8ed2a61a5b272e2f3f8c8c937000056ab5f41dceda56c2b398791e8a70b30638`,
  `pipeline-coordinator-repository.js=abcf23786d069a18584d33af1f21d9e507f68b2625fac517599d21ece2d8cd60`,
  `prisma-run-repository.js=1d5814084778c23b5af306ebe93996c481a19d63aa3dcebefd78ae00b628a962`,
  with backend HEAD `8694b949…` and frontend HEAD `f981b34…`. If any differs,
  run exactly once with the isolated helper and non-production URL:
  `ALLOW_DATABASE_TESTS=true node -r dotenv/config --test --test-isolation=none --test-concurrency=1 test/pipeline-coordinator-repository.integration.test.js test/aws-pipeline-domain.integration.test.js test/aws-pipeline-lead-aggregation.integration.test.js test/aws-pipeline-traffic.integration.test.js test/aws-pipeline-final.integration.test.js`;
  require 14 pass, 0 fail/skip, exact isolation, cleanup, and zero residual
  disposable schemas.
- [ ] `KI-W6-CV94` From `frontend/`, run exactly one durable child command
  `ALLOW_DATABASE_TESTS=true KI_W6_SKIP_BUILD=1 node test/browser/keyword-intelligence-e2e.mjs`
  with executor allowance at least 75 minutes and complete retained stdout,
  stderr, and exit status in preflight-empty `/tmp/ki-w6-i120-cv94.browser.log`
  and `/tmp/ki-w6-i120-cv94.browser.status`. Require exit 0; browser 26/26,
  controls 13/13; 100 validators and discovery tasks; 1,000 domains/leads;
  both discovery and lead terminal/check progression; zero
  heartbeat-after-terminal `PIPELINE_LEASE_LOST`; and complete browser,
  server, process, schema-drop/absence, and temporary-output cleanup. One
  identical elevated recovery is allowed only after the exact inherited E8.1
  environment-invalidated-attempt proof.
- [ ] `KI-W6-CV95` Only after CV94 passes, run once from `email_scraper/`:
  `npm test`, `npm run check:secrets`, `npm run build:lambda`; and from
  `frontend/`: `npm run check`. Require every command exit 0, zero test/lint/
  secret failures, successful handler build/startup inventories, and no
  unplanned tracked/untracked workspace output. Do not repeat a successful
  unchanged expensive gate.
- [ ] `KI-W6-CV96` Recompute the literal §12.7 sets: required=registered=
  executed exactly 40 with digest `334999de9923c0af40fa46b1c99eb92b03efce978585a71ff6b031092d105b71`;
  zero skips/duplicates/unexpected/unactivated/oracle failures; controls
  exactly 21 with digest
  `66921e9aae67f455bc35678da9b6ba659165dd037856d437b91c11b3c07fde80`,
  all falsified with fresh positives.
- [ ] `KI-W6-CV97` Verify exact four-file correction scope and protected
  accepted evidence; no schema, migration, repository transaction/fence,
  lease duration/interval, queue, retry, provider, AWS, production, paid,
  frontend product, package/config, commit/push, or KI-W7 action; cost `$0.00`;
  privacy-safe evidence and complete cleanup.
- [ ] `KI-W6-CH16` Append the complete `WINDOW-AGENT-INTEGRATION-PASS`
  certificate, set S2 `READY_FOR_PARENT_REVIEW`, send the standard §12.5
  consolidated handoff only to the parent, and stop before KI-W7.

Mandatory I120 checklist:

- [ ] `I1` Independently accept C145–C148 and record ending digests.
- [ ] `I2` Prove actual four-file set equals planned set within parent scope.
- [ ] `I3` Verify complete requirement/decision/task/scenario/file/assertion trace.
- [ ] `I4` Execute CV91–CV97/CH16 in order with activation witnesses.
- [ ] `I5` Verify exact required=registered=executed case/control sets/digests and zero skips/duplicates/unexpected.
- [ ] `I6` Execute all prescribed controls and prove each falsifies unchanged acceptance with a fresh positive.
- [ ] `I7` Verify substitute fidelity and accepted-test/fixture integrity.
- [ ] `I8` Verify no prohibited, successor, external, destructive, secret-bearing, or out-of-scope action.
- [ ] `I9` Independently inspect current source/diffs; do not rely on leaf summaries.
- [ ] `I10` Record exactly `PASS`, `CORRECTION_REQUIRED`, or `PARENT_BLOCKED` with decisive evidence.

`PASS` requires every CV91–CV97/CH16 item. A coding omission mechanically
governed by DEC-KI-054 and confined to these four files is
`CORRECTION_REQUIRED`: diagnose it, append one-file C149+ leaves and a new
I121+ assessment, then continue without parent return. A new observable
failure whose root cause is outside these four files, missing decision,
authority expansion, unavailable isolated database, or authoritative
contradiction is `PARENT_BLOCKED`. No successful leaf or gate boundary causes
a stop; after parent decomposition approval, execution continues until PASS or
one such new failure.

### 12.9 State-186 mandatory decomposition-readiness checklist (47/47)

#### Authority and inheritance

- [x] `SW-A01` State 186 names `ASG-KI-W6-WA-15`, this window agent, and exact delegable correction scope. Evidence: `EV-KI-W6-TC07`.
- [x] `SW-A02` Parent/subwindow standards and A1/A2/A3/A4/A5/A8 revisions are pinned and recomputed. Evidence: `EV-KI-W6-TC07`.
- [x] `SW-A03` Write/read/action/prohibition/successor/stop boundaries are copied without expansion. Evidence: §12.1; `EV-KI-W6-TC07`.
- [x] `SW-A04` Backend/frontend cleanliness, commits, four baselines, and owner-controlled root state are inventoried. Evidence: §12.1/§12.2; `EV-KI-W6-TC07`.
- [x] `SW-A05` S1/S2/S3 exist with nonoverlapping authorities. Evidence: §12.1; `EV-KI-W6-TC07`.
- [x] `SW-A06` Strict leaf↔window↔parent adjacency, no leaf delegation, and window-agent-only I120 are frozen. Evidence: §12.3–§12.8.
- [x] `SW-A07` E8.1 sandbox escalation/one-identical-recovery policy is copied without external expansion. Evidence: §12.1/§12.8.

#### Decision and file-set closure

- [x] `SW-D01` Every parent requirement/invariant/decision/task/scenario/case/control maps to exact files/assertions. Evidence: §12.3–§12.8; `EV-KI-W6-TC07`.
- [x] `SW-D02` DEC-KI-054 and CT24–CT27 leave no material choice or contradiction. Evidence: §12.1/§12.2.
- [x] `SW-D03` Required changed-file set equals the four-path planned set and pinned digest. Evidence: §12.2.
- [x] `SW-D04` Every planned file has one correction owner; no leaf owns multiple files. Evidence: §12.2.
- [x] `SW-D05` Every operation, baseline, anchor, interface, preservation, and forbidden edit is exact. Evidence: §12.3–§12.6.
- [x] `SW-D06` C145→Wave3{C146,C147}→C148→I120 is complete/acyclic with disjoint-resource proof. Evidence: §12.2.
- [x] `SW-D07` The exact helper interface is frozen before Wave 3. Evidence: §12.2/§12.3.
- [x] `SW-D08` Every intermediate state, pending check, safety rule, resolver, and prohibition is exact. Evidence: §12.2.
- [x] `SW-D09` Three production files and one test file have four separate leaves. Evidence: §12.2.
- [x] `SW-D10` No rename/generator/formatter/installer or local command can create an authorized second workspace edit. Evidence: §12.3–§12.6.

#### Sub-window execution completeness

- [x] `SW-E01` C145–C148 contain all Section 7 fields and literal nine-box checklists. Evidence: §12.3–§12.6; `EV-KI-W6-TC07`.
- [x] `SW-E02` Every leaf has one ordered exact transformation with no alternatives. Evidence: §12.3–§12.6.
- [x] `SW-E03` Every leaf freezes preflight, local activation/assertions, controls, and forbidden outcomes. Evidence: §12.3–§12.6.
- [x] `SW-E04` Every leaf proves its attributable changed-file set is exactly one file. Evidence: §12.3–§12.6 V2.
- [x] `SW-E05` Every leaf has exact evidence/handoff/stop/successor-reservation rules. Evidence: §12.3–§12.6 P/H boxes.
- [x] `SW-E06` Leaves report only to the window agent and cannot edit S1/S2/S3 or parent artifacts. Evidence: §12.3–§12.6 prohibitions.
- [x] `SW-E07` No leaf needs successor work for its LOCAL_NOW acceptance. Evidence: §12.3–§12.6.
- [x] `SW-E08` All deferred checks name C148 or I120 exactly. Evidence: §12.3–§12.8.

#### Enforcement and integration closure

- [x] `SW-V01` W6-DB-12/W6-NC-21 registration, activation, assertions, and source ownership are exact. Evidence: §12.6/§12.7.
- [x] `SW-V02` Local 5/4 and final 40/21 set equality/digests are literal. Evidence: §12.6–§12.8.
- [x] `SW-V03` W6-NC-21 falsifies the narrow terminal-order invariant and requires a fresh positive. Evidence: §12.6.
- [x] `SW-V04` Fake-timer/source parity is bounded and accepted C142/browser/database evidence invalidation rules are exact. Evidence: §12.7/§12.8.
- [x] `SW-V05` I120 is fully authored with zero implementation-write authority. Evidence: §12.8.
- [x] `SW-V06` Focused/reuse-or-rerun/browser/regression/build/privacy/scope gates are exact and scheduled once at I120. Evidence: §12.8.
- [x] `SW-V07` C149+/I121+ routing is complete for in-scope omissions; outside-scope failures stop. Evidence: §12.8.
- [x] `SW-V08` Window agent independently reviews every leaf and personally executes I120. Evidence: §12.2/§12.8.
- [x] `SW-V09` Zero-work/skipped/filtered/duplicate/unexpected/unactivated/summary-only acceptance fails. Evidence: §12.6–§12.8.
- [x] `SW-V10` `READY_FOR_PARENT_REVIEW`, consolidated handoff, and KI-W7 stop are exact. Evidence: §12.8 CH16.
- [x] `SW-V11` Sandbox/channel invalidation is separated from observable failure with one identical recovery. Evidence: §12.1/§12.8 CV94.

#### Mechanical and adversarial audit

- [x] `SW-R01` C145–C148/I120/W6-DB-12/W6-NC-21 IDs are unique and references resolve. Evidence: `EV-KI-W6-TC07`.
- [x] `SW-R02` No unresolved placeholder or implementation alternative occurs in assignable content. Evidence: `EV-KI-W6-TC07`.
- [x] `SW-R03` One-file lint rejects zero/two/wildcard/directory/rename/incidental outputs. Evidence: §12.2–§12.6; `EV-KI-W6-TC07`.
- [x] `SW-R04` Removing any required path or mapping changes the four-path digest/trace and fails readiness. Evidence: §12.2/§12.3–§12.6.
- [x] `SW-R05` Removing/duplicating/skipping/filtering/bypassing any case fails local/final exact-set acceptance. Evidence: §12.6–§12.8.
- [x] `SW-R06` Weakening the order oracle or diverging fake-timer behavior invalidates W6-DB-12/W6-NC-21 evidence. Evidence: §12.6/§12.7.
- [x] `SW-R07` A second-file edit, sibling communication, or direct parent communication is rejected. Evidence: §12.3–§12.6.
- [x] `SW-R08` Window-agent implementation repair is prohibited; a diagnosed omission requires C149+ then I121+. Evidence: §12.8.
- [x] `SW-R09` Parent approval of this exact amended S1 revision is required before C145 assignment. Evidence: §12 opening; S2.
- [x] `SW-R10` Document lint has zero missing fields/mappings/cases/evidence/authority conflicts. Evidence: `EV-KI-W6-TC07`.
- [x] `SW-R11` Sandbox denial permits one identical escalated recovery; changed command, observable failure, surviving process/mutation, or external action does not. Evidence: §12.1/§12.8.

## 13. State-188 append-only command-protocol supersession

`DEC-KI-055`, A5 state 188, `EV-KI-A-114`, and `CHG-KI-086` supersede only
the following three command literals; they require no new decomposition review
and change no source/test bytes, registration, case/control membership, digest,
expected total, assertion, later gate, or recovery allowance:

1. C148 §12.6 LOCAL_NOW check 2 and I120 `KI-W6-CV92` use exactly:
   `node --test --test-isolation=none test/aws-pipeline-transaction-clock-enforcement.test.js`.
   Required result remains 10 pass, 0 fail, 0 skip; exact five-case/
   four-control certificate; witnesses `11/21/9/5/2/2/1`; exact group
   digests; W6-NC-21 falsification and fresh REAL positive.
2. I120 `KI-W6-CV93` uses exactly:
   `node --test --test-isolation=none test/aws-pipeline-contracts.test.js test/aws-pipeline-discovery.test.js test/aws-pipeline-transaction-clock-enforcement.test.js`.
   Required result remains 26 pass, 0 fail, 0 skip with every previously frozen
   activation oracle.
3. The default-isolation 1/1 file wrapper is diagnostic evidence only. It is
   neither an acceptance failure nor activation evidence and must not be used
   in any required/registered/executed count.

All other C148 and I120 text remains authoritative and unchanged. C148 remains
the same one-file leaf with the same candidate bytes; the window agent now
finishes its independent review under command 1 and, on acceptance, continues
I120 automatically.

## 14. State-189 seventeenth corrective sequence — domain-aggregation trace predicate

`DEC-KI-056`, A5 state 189, `EV-KI-A-115`, and `CHG-KI-087` authorize this
append-only parent-direct correction and assessment without another decomposition
review. Accepted C145-C148 are committed at backend commit
`9fc714ad9c96a396aa31426fc0d3c1e08da07050`; their implementation and evidence
remain unchanged.

### 14.1 `KI-W6-C149` — one-file parent-direct correction

```yaml
subwindow_id: KI-W6-C149
type: CORRECTION
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-16
implementation_owner: REQUESTER_AUTHORIZED_PARENT_DIRECT
review_owner: KI-W6-WINDOW-AGENT
predecessors: [KI-W6-C145, KI-W6-C146, KI-W6-C147, KI-W6-C148 independently accepted and requester committed]
writable_file: frontend/test/browser/keyword-intelligence-e2e.mjs
starting_digest: c035094b1276161c6d69e4aa87b25a02c4aa360e8a0aea606f72d2385650d55f
baseline_commit: f981b34eeb79764a2e9e7ee96779f99907228a3f
expected_ending_digest: 8a9cffc39e33689a69b0c89200b4cfae1af31ff410270dc1a867205acb4ce0b6
expected_diff_stat: 1 insertion / 1 deletion
planned_file_set_digest: 3dd4230266485b5b217634b4558e3aa027264534ab8a13c52ddc2f227eca9867
may_start_successor: false
```

1. **Trace:** `REQ-KI-010`-`REQ-KI-015`; `INV-KI-010/015`;
   `SRC-KI-057`; `DEC-KI-056`; existing `SCN-KI-018`, `W6-FLOW-11/12`,
   `W6-NC-08`.
2. **Exact edit:** replace exactly once
   `(event.messageTypes || []).some((type) => String(type).startsWith("domain"))`
   with `(event.messageTypes || []).includes("aggregation.check")`.
3. **Preserve:** every other byte, including the SQS-kind guard,
   `downstreamFloor`, promise/error handling, progress watchdog, absolute
   ceiling, diagnostics, cleanup, all 26 browser cases, all 13 browser
   controls, combined 40/21 closure, and every production file.
4. **Local review:** from `frontend/`, run `node --check
   test/browser/keyword-intelligence-e2e.mjs`; require the exact old occurrence
   count `0` and new occurrence count `1`; reconstruct the candidate from the
   baseline with only the exact replacement and require byte equality; invert
   the replacement in memory and require the unchanged source oracle to fail,
   then require the fresh real source to pass; run `git diff --check`; require
   the attributable frontend path set to equal the one writable file and its
   workspace-relative sorted-LF digest to equal the pinned digest.

- [x] `P1` State 189, assignment, baseline commit/digest, candidate digest, and requester-direct authority match. Evidence: `EV-KI-W6-TC20`.
- [x] `P2` Backend is clean at committed C145-C148 commit and frontend has exactly this one attributable test-file edit. Evidence: `EV-KI-W6-TC20`.
- [x] `T1` Independently reconstruct the exact one-expression candidate; do not modify it. Evidence: baseline transform byte-equal in `EV-KI-W6-TC20`.
- [x] `V1` Execute every local review oracle and require exact source/inverse/fresh activation. Evidence: `EV-KI-W6-TC20`.
- [x] `V2` Prove ending digest, 1/1 diff and exact one-path digest. Evidence: `EV-KI-W6-TC20`.
- [x] `V3` Prove the preserved event-kind guard, watchdog, diagnostics, cases, controls and closure literals remain byte-identical. Evidence: exact one-expression reconstruction in `EV-KI-W6-TC20`.
- [x] `H1` Append independent review evidence and accept or reject the actual bytes. Evidence: accepted in `EV-KI-W6-TC20`.
- [x] `H2` Confirm no second file, product, provider, AWS, database, schema, package, commit/push or KI-W7 action. Evidence: `EV-KI-W6-TC20`.
- [x] `H3` On acceptance continue directly to I121; successful review is not a stop boundary. Evidence: I121 started in `EV-KI-W6-TC20`.

### 14.2 `KI-W6-I121` — fresh causal continuation and final closure

```yaml
subwindow_id: KI-W6-I121
type: INTEGRATION_ASSESSMENT
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-16
assigned_agent: KI-W6-WINDOW-AGENT
predecessors: [KI-W6-C149 independently accepted]
authorized_write_file: NONE
coordination_writes: [KEYWORD_INTELLIGENCE_KI_W6_TRANSACTION_CLOCK_SUBWINDOW_STATE.md, KEYWORD_INTELLIGENCE_KI_W6_TRANSACTION_CLOCK_SUBWINDOW_EVIDENCE.md]
expected_backend_commit: 9fc714ad9c96a396aa31426fc0d3c1e08da07050
expected_frontend_baseline_commit: f981b34eeb79764a2e9e7ee96779f99907228a3f
expected_frontend_changed_file: frontend/test/browser/keyword-intelligence-e2e.mjs
expected_frontend_changed_file_digest: 8a9cffc39e33689a69b0c89200b4cfae1af31ff410270dc1a867205acb4ce0b6
planned_file_set_digest: 3dd4230266485b5b217634b4558e3aa027264534ab8a13c52ddc2f227eca9867
required_case_count: 40
required_case_digest: 334999de9923c0af40fa46b1c99eb92b03efce978585a71ff6b031092d105b71
negative_control_count: 21
negative_control_digest: 66921e9aae67f455bc35678da9b6ba659165dd037856d437b91c11b3c07fde80
may_start_successor: false
```

Execute personally and sequentially. A passing gate is not a stop boundary:

- [x] `KI-W6-CV98` Verify backend clean at committed C145-C148 commit
  `9fc714ad9c96a396aa31426fc0d3c1e08da07050`, frontend baseline commit
  `f981b34eeb79764a2e9e7ee96779f99907228a3f`, and exactly one attributable
  frontend test-file edit with planned one-path sorted-LF digest
  `3dd4230266485b5b217634b4558e3aa027264534ab8a13c52ddc2f227eca9867`.
- [ ] `KI-W6-CV99` Run the unchanged durable causal command once with at least
  75 minutes attached and complete stdout/stderr/status retention. Require
  browser 26/26, controls 13/13, 100 discovery tasks, observed
  `aggregation.check` domain trigger, 1,000 domains/leads, no terminal-heartbeat
  lease loss, and complete process/schema/temp cleanup. One identical E8.1
  recovery remains available only for a newly proven environment-invalidated
  attempt; observable failure is not recoverable.
- [ ] `KI-W6-CV100` Only after CV99 passes, execute the unchanged CV95 commands
  exactly once: backend `npm test`, `npm run check:secrets`, `npm run
  build:lambda`; frontend `npm run check`; require zero failures and no
  unplanned output.
- [ ] `KI-W6-CV101` Execute unchanged CV96 40-case/21-control equality/digest
  closure and unchanged CV97 scope/privacy/cost/cleanup audit.
- [ ] `KI-W6-CH17` Append the complete integration certificate, set subordinate
  status `READY_FOR_PARENT_REVIEW`, return to parent and stop before KI-W7.

`PASS` requires CV98-CV101 and CH17. A coding omission mechanically governed
by `DEC-KI-056` and confined to the C149 file may use append-only C150+/I122+
and continue without parent return. Any new observable failure outside that
decision or one-file scope is `PARENT_BLOCKED`.

## 15. State-190 eighteenth corrective sequence — durable-only handoff observation

`DEC-KI-057`, A5 state 190, `EV-KI-A-116`, and `CHG-KI-088` authorize this
append-only parent-direct correction and assessment without another decomposition
review. C150 is layered on accepted C149 in the same single browser-test file.

### 15.1 `KI-W6-C150` — parent-direct one-file waiter correction

```yaml
subwindow_id: KI-W6-C150
type: CORRECTION
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-17
implementation_owner: REQUESTER_AUTHORIZED_PARENT_DIRECT
review_owner: KI-W6-WINDOW-AGENT
predecessors: [KI-W6-C149 independently accepted]
writable_file: frontend/test/browser/keyword-intelligence-e2e.mjs
starting_digest: 8a9cffc39e33689a69b0c89200b4cfae1af31ff410270dc1a867205acb4ce0b6
baseline_commit_before_C149_and_C150: f981b34eeb79764a2e9e7ee96779f99907228a3f
candidate_commit: 9f0c4c53da4cc0268f5165d51c89a8a151237fdb
expected_ending_digest: 6de55e92cfe25c8caed683cacb5ba1ae9eee5f7696874e7e372cf7f50ec3767e
expected_combined_diff_stat_from_baseline: 40 insertions / 12 deletions
planned_file_set_digest: 3dd4230266485b5b217634b4558e3aa027264534ab8a13c52ddc2f227eca9867
may_start_successor: false
```

1. **Trace:** `REQ-KI-015`-`REQ-KI-017`; `INV-KI-010/011/015`;
   `SRC-KI-058`; `DEC-KI-035/038/057`; existing `W6-NAV-02`,
   `W6-FLOW-08`, `W6-NC-06`.
2. **Authoritative waiter:** `waitForDurableHandoffCommit` accepts exactly
   `{clientRequestId,expectedSelectionRevision}`, reads
   `harness.readDurableState()` unconditionally on every cycle, and returns
   only for exact durable handoff client ID, exact selection revision and its
   associated Run with `queryCount === 100`. It has zero `harness.trace()` or
   HTTP-gate dependency.
3. **Interception:** retain numeric `responseStatusCode` for diagnostics; parse
   the intercepted POST body; require string `clientRequestId` and safe-integer
   `expectedSelectionRevision`; retain that identity and the returned durable
   snapshot before `Fetch.failRequest`.
4. **Post-abort proof:** require netlog request identity equal to intercepted
   identity; require stored durable handoff ID/revision and 100-query Run.
   Response-finish trace is diagnostic boolean only. Preserve C149's exact
   `aggregation.check` predicate.
5. **No alternatives:** preserve the 30-second waiter, 90-second pause guard,
   15-second product proxy, request/retry key, repository, route, helper,
   response bytes, cases, controls, all other timeouts and product behavior.
6. **Local review:** syntax/diff pass; exact source oracle proves all fields and
   ordering above; restoring the former trace-gated waiter in memory falsifies
   it, then fresh source passes; ending digest, combined sole-file diff and
   C149 predicate match exactly.

- [x] `P1` State 190, assignment, parent revisions, commits and starting/ending digests match. Evidence: `EV-KI-W6-TC22`.
- [x] `P2` Backend is clean at `9fc714ad…`; frontend candidate is clean at `9f0c4c53…`; only the sole test path differs from baseline `f981b34…`. Evidence: `EV-KI-W6-TC22`.
- [x] `T1` Independently reconstruct/review every DEC-KI-057 transformation; do not modify the candidate. Evidence: byte-exact baseline reconstruction in `EV-KI-W6-TC22`.
- [x] `V1` Run syntax, diff, exact source/inverse/fresh and C149-preservation oracles. Evidence: `EV-KI-W6-TC22`.
- [x] `V2` Prove ending digest, 40/12 combined diff and exact one-path digest. Evidence: `EV-KI-W6-TC22`.
- [x] `V3` Prove all product/helper/timeouts/cases/controls and nonowned bytes unchanged. Evidence: sole-file exact reconstruction in `EV-KI-W6-TC22`.
- [x] `H1` Append independent review evidence and accept or reject actual bytes. Evidence: accepted in `EV-KI-W6-TC22`.
- [x] `H2` Confirm no second file, provider/AWS/database/schema/package/commit/push/KI-W7 action. Evidence: `EV-KI-W6-TC22`.
- [x] `H3` On acceptance continue directly to I122; successful review is not a stop boundary. Evidence: I122 started in `EV-KI-W6-TC22`.

### 15.2 `KI-W6-I122` — fresh causal continuation and final closure

```yaml
subwindow_id: KI-W6-I122
type: INTEGRATION_ASSESSMENT
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-17
assigned_agent: KI-W6-WINDOW-AGENT
predecessors: [KI-W6-C150 independently accepted]
authorized_write_file: NONE
coordination_writes: [KEYWORD_INTELLIGENCE_KI_W6_TRANSACTION_CLOCK_SUBWINDOW_STATE.md, KEYWORD_INTELLIGENCE_KI_W6_TRANSACTION_CLOCK_SUBWINDOW_EVIDENCE.md]
expected_backend_commit: 9fc714ad9c96a396aa31426fc0d3c1e08da07050
expected_frontend_commit: 9f0c4c53da4cc0268f5165d51c89a8a151237fdb
expected_frontend_changed_file: frontend/test/browser/keyword-intelligence-e2e.mjs
expected_frontend_changed_file_digest: 6de55e92cfe25c8caed683cacb5ba1ae9eee5f7696874e7e372cf7f50ec3767e
planned_file_set_digest: 3dd4230266485b5b217634b4558e3aa027264534ab8a13c52ddc2f227eca9867
required_case_count: 40
required_case_digest: 334999de9923c0af40fa46b1c99eb92b03efce978585a71ff6b031092d105b71
negative_control_count: 21
negative_control_digest: 66921e9aae67f455bc35678da9b6ba659165dd037856d437b91c11b3c07fde80
may_start_successor: false
```

- [x] `KI-W6-CV102` Verify backend commit `9fc714ad…`, frontend baseline commit
  `f981b34…`, exact C149+C150 sole-file diff, ending digest `6de55e92…`, C149
  predicate preserved, and C150 source/inverse/fresh oracles.
- [ ] `KI-W6-CV103` Run one fresh durable causal browser command with at least
  75 minutes attached and retained stdout/stderr/status. Require 26/26 cases,
  13/13 controls, exact durable handoff identity/100 queries independent of
  HTTP trace, exact aggregation.check observation, 100 discovery tasks, 1,000
  domains/leads, no terminal-heartbeat loss, and complete cleanup. One identical
  E8.1 recovery is allowed only for a newly proven environmental invalidation.
- [ ] `KI-W6-CV104` After CV103 passes, run unchanged backend `npm test`,
  `npm run check:secrets`, `npm run build:lambda` and frontend `npm run check`
  once; require zero failures/unplanned output.
- [ ] `KI-W6-CV105` Run unchanged 40-case/21-control equality/digests and final
  scope/privacy/cost/cleanup audit.
- [ ] `KI-W6-CH18` Record integration pass, set `READY_FOR_PARENT_REVIEW`, hand
  off to parent and stop before KI-W7.

Only a mechanically governed omission confined to this browser test may open
C151+/I123+ without parent return. A new observable failure outside
`DEC-KI-057` or this file is `PARENT_BLOCKED`.

## 16. State-190 in-scope C151/I123 — progress-aware downstream settlement

I122 CV103 proved C149 and C150, then failed only because the post-first-check
settlement block retained a separate fixed 120-second deadline while the frozen
causal workload was still making valid sequential progress. This is the exact
mechanically governed, same-file omission authorized by A5 state 190.

### 16.1 `KI-W6-C151` — one-file settle-watchdog correction

```yaml
subwindow_id: KI-W6-C151
type: CORRECTION
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-17
assignment_id: ASG-KI-W6-C151
assigned_agent: KI-W6-LEAF-C151
predecessors: [KI-W6-C150 independently accepted, KI-W6-CV102 PASS, KI-W6-CV103 observable in-scope failure]
writable_file: frontend/test/browser/keyword-intelligence-e2e.mjs
starting_digest: 6de55e92cfe25c8caed683cacb5ba1ae9eee5f7696874e7e372cf7f50ec3767e
expected_ending_digest: 2a07612d9f58c7b882573a3f3f8d7dbc99cc8a35ff3fdaea60ee10b7935601f6
planned_file_set_digest: 3dd4230266485b5b217634b4558e3aa027264534ab8a13c52ddc2f227eca9867
may_start_successor: false
```

Replace exactly the seven-line block beginning
`const downstreamSettleDeadline = Date.now() + 120000;` and ending at its
`while (!downstreamOutcome.settled)` closing brace with one 31-line settle loop
that:

1. retains the same `while (!downstreamOutcome.settled)` and 50 ms poll;
2. reads `harness.trace().slice(downstreamFloor)` every cycle;
3. immediately throws a sanitized `message-failed after first domain-check
   emission` error for the first downstream `message-failed` event;
4. recomputes lifecycle start/complete events, updates the existing
   `downstreamLifecycleCount`, `downstreamCompletedCount`, and
   `downstreamLastProgressAt`, and writes the same four-field
   `diagnostics.downstreamProgress` projection;
5. fails after the existing `downstreamNoProgressLimitMs` only when lifecycle
   progress has stopped, with exactly one `readDownstreamDiagnostics()` safe
   projection;
6. fails after the existing `downstreamAbsoluteLimitMs`, measured from the
   unchanged `downstreamWaitStartedAt`, with exactly one safe diagnostics
   projection; and
7. contains no new duration literal, no reset of the absolute start, and no
   fixed settle deadline.

The exact source strings and expressions are those already used by the
immediately preceding first-check watchdog: `downstream-message`,
`message-start`, `message-complete`, `message-failed`, the four progress fields,
the `120000` no-progress constant and `(100 * 30000) + 600000` absolute ceiling.
Preserve C149, C150, the domain-check fault injections, downstream result
assertions, all 26 cases/13 controls, cleanup and every other byte.

The replacement block is literally:

```js
  while (!downstreamOutcome.settled) {
    const downstreamEvents = harness.trace().slice(downstreamFloor);
    const downstreamFailureEvent = downstreamEvents.find((event) => event.kind === "downstream-message" && event.op === "message-failed");
    if (downstreamFailureEvent) {
      throw new Error(`KI downstream drain message-failed after first domain-check emission: ${JSON.stringify({ name: downstreamFailureEvent.errorName, code: downstreamFailureEvent.errorCode, frame: downstreamFailureEvent.errorFrame })}`);
    }
    const lifecycleEvents = downstreamEvents.filter((event) => event.kind === "downstream-message" && (event.op === "message-start" || event.op === "message-complete"));
    if (lifecycleEvents.length > downstreamLifecycleCount) {
      downstreamLifecycleCount = lifecycleEvents.length;
      downstreamCompletedCount = lifecycleEvents.filter((event) => event.op === "message-complete").length;
      downstreamLastProgressAt = Date.now();
    }
    const downstreamElapsedMs = Date.now() - downstreamWaitStartedAt;
    diagnostics.downstreamProgress = {
      elapsedMs: downstreamElapsedMs,
      lifecycleEvents: downstreamLifecycleCount,
      completedMessages: downstreamCompletedCount,
      completedMessagesPerSecond: downstreamElapsedMs > 0
        ? Number((downstreamCompletedCount * 1000 / downstreamElapsedMs).toFixed(4))
        : 0,
    };
    if (Date.now() - downstreamLastProgressAt > downstreamNoProgressLimitMs) {
      const downstreamStallDiagnostics = await harness.readDownstreamDiagnostics();
      throw new Error(`KI downstream made no lifecycle progress for ${downstreamNoProgressLimitMs} ms after first domain-check emission: ${JSON.stringify({ progress: diagnostics.downstreamProgress, diagnostics: downstreamStallDiagnostics })}`);
    }
    if (downstreamElapsedMs > downstreamAbsoluteLimitMs) {
      const downstreamCeilingDiagnostics = await harness.readDownstreamDiagnostics();
      throw new Error(`KI downstream exceeded the ${downstreamAbsoluteLimitMs} ms absolute safety ceiling after first domain-check emission: ${JSON.stringify({ progress: diagnostics.downstreamProgress, diagnostics: downstreamCeilingDiagnostics })}`);
    }
    await wait(50);
  }
```

LOCAL_NOW from `frontend/`:

1. `node --check test/browser/keyword-intelligence-e2e.mjs` and
   `git diff --check` pass.
2. SHA-256 equals the pinned ending digest; attributable path set is exactly
   the writable file and its sorted-LF digest is pinned above.
3. Source oracle requires zero `downstreamSettleDeadline`, two occurrences each
   of lifecycle filtering/progress projection/no-progress/absolute-ceiling
   guards (before and after first check), and C149/C150 exact markers.
4. In-memory restoration of the seven-line fixed-deadline block falsifies the
   unchanged oracle; fresh real source passes.

- [x] `P1` State 190 authority, C150 baseline and exact one-file assignment match. Evidence: `EV-KI-W6-TC24`.
- [x] `P2` Starting file digest and clean backend/frontend commits match. Evidence: `EV-KI-W6-TC24`.
- [x] `T1` Apply exactly the frozen seven-line-to-31-line block replacement. Evidence: byte-exact reconstruction in `EV-KI-W6-TC24`.
- [x] `V1` Execute syntax/diff/source/inverse/fresh checks with activation output. Evidence: `EV-KI-W6-TC24`.
- [x] `V2` Prove exact ending digest and one attributable path/digest. Evidence: `EV-KI-W6-TC24`.
- [x] `V3` Prove C149/C150, cases/controls/faults/cleanup and every sibling byte preserved. Evidence: `EV-KI-W6-TC24`.
- [x] `H1` Return exact diff, ending digest, checks and I123 obligations only to window agent. Evidence: leaf handoff and independent review in `EV-KI-W6-TC24`.
- [x] `H2` Confirm no second file, parent artifact, external action, commit/push or KI-W7 work. Evidence: `EV-KI-W6-TC24`.
- [x] `H3` Stop at AWAITING_WINDOW_REVIEW; do not run browser/database/build/regression gates. Evidence: leaf stopped and window agent accepted in `EV-KI-W6-TC24`.

### 16.2 `KI-W6-I123` — fresh causal continuation and final closure

- [x] `KI-W6-CV106` Independently reconstruct/review C151; require exact
  one-file digest, source/inverse/fresh activation, C149/C150 preservation and
  clean backend commit `9fc714ad…`.
- [ ] `KI-W6-CV107` Run one fresh durable causal browser command with at least
  75 minutes and retained stdout/stderr/status. Require the complete CV103
  contract plus a progress-aware settle: 26/26 cases, 13/13 controls, durable
  handoff identity/100 queries, aggregation.check observation, 100 discovery
  tasks, 1,000 domains/leads, no lease loss, no fixed-deadline failure, and
  complete cleanup. One identical E8.1 recovery only follows newly proven
  environment invalidation.
- [ ] `KI-W6-CV108` After CV107 passes, run unchanged backend `npm test`,
  `npm run check:secrets`, `npm run build:lambda`, and frontend `npm run check`
  exactly once; require zero failures or unplanned output.
- [ ] `KI-W6-CV109` Run unchanged 40-case/21-control equality/digests and final
  scope/privacy/cost/cleanup audit.
- [ ] `KI-W6-CH19` Record integration pass, set `READY_FOR_PARENT_REVIEW`, hand
  off to parent and stop before KI-W7.

I123 is window-agent-only with zero implementation-write authority. A further
same-file mechanically governed omission may use C152+/I124+; a new failure
outside this file or the frozen semantics is `PARENT_BLOCKED`.

## 17. Parent-authored compositional 1,000-domain bridge package

### 17.0 Operative authority and requester exception

This section supersedes only the stopped I123/CV107 synthetic-storefront
assertion. It implements `SRC-KI-059`, `DEC-KI-058` and the nineteenth KI-W6
corrective sequence in A4. At the requester's explicit direction, the parent
agent authored this complete subordinate package directly. This is a recorded
exception only to the subwindow standard's role allocation: all single-file,
decision-complete, execution-complete, enforcement-complete, evidence,
independent-review and integration-assessment requirements remain binding.

The receiving window agent does **not** decompose or return for decomposition
review. It must:

1. verify A5 state 191 and every pin/baseline below;
2. reserve and dispatch C152 alone;
3. independently review C152;
4. after C152 acceptance, reserve/dispatch C153 and C154 in parallel or
   sequentially at its discretion, without changing either contract;
5. independently review both leaves;
6. personally run I124; and
7. stop only at `READY_FOR_PARENT_REVIEW` or one genuinely new parent-level
   blocker. It must not communicate leaf results directly to the parent.

The exact initial path set is:

```text
email_scraper/src/aws-pipeline/services/discovery-worker.js
email_scraper/test/aws-pipeline-discovery.test.js
email_scraper/test/aws-pipeline-domain.integration.test.js
```

Sorted-member-LF digest:
`36780bc47b3e5950c707525292655be1a10d8b39cbeff69ccea1023dcc5074e1`.
Backend baseline commit:
`9fc714ad9c96a396aa31426fc0d3c1e08da07050`. Frontend unchanged commit:
`5e441aae7e2f3a132b2c7fc85bf1bc525d3d5cb6`; unchanged browser file digest:
`2a07612d9f58c7b882573a3f3f8d7dbc99cc8a35ff3fdaea60ee10b7935601f6`.

New exact coverage registries:

```text
cases = [W6-DB-13, W6-DB-14, W6-DB-15]
controls = [W6-NC-22, W6-NC-23, W6-NC-24]
case_digest = 5342728a461b927afe37050b5f4e8df6df30f42698e3b75144f5872334e19600
control_digest = 97b186a9948a3fbb4077f1d6f4d39b2d635ad1325e37fb82cdb095661bfbe4ee
final_case_count = 43
final_case_digest = 5ef52fb9ed7a7cc182302cd2c2441712f5745f52948c4fb1f10b6e759c4dbe71
final_control_count = 24
final_control_digest = 3bd895f41f3689c1c1d421d1ea0056c095e1d4cd57d3f90e3987f79104719707
```

No live storefront, Google, DataForSEO, CrUX, Browserless, AWS or production
operation is permitted. Paid cost is `$0.00`. Requester alone commits.

### 17.1 `KI-W6-C152` — one-file production resolver dependency

```yaml
subwindow_id: KI-W6-C152
assignment_id: ASG-KI-W6-C152
type: CORRECTION
status_at_authoring: READY
predecessors: [KI-W6-C151 accepted, KI-W6-I123 stopped PARENT_BLOCKED, A5 state 191]
writable_file: email_scraper/src/aws-pipeline/services/discovery-worker.js
starting_sha256: 34013f07b18b5040d848eda6eff5abb53b5db0daf174dfea375fd6002bd9c212
read_scope: [the writable file, email_scraper/src/domain-resolver.js resolveStoreIdentity signature, DEC-KI-058, this block]
prohibited: [second file, runtime/config/env seam, domain-resolver edit, payload/schema/queue/lease/retry behavior, network/provider/AWS/database/build/browser, commit/push, parent artifacts, KI-W7]
```

Exact transformation:

1. Change the declaration to
   `export async function processDiscoveryMessage(message, runtime, dependencies = {})`.
2. As the first statements in the function, before `artifactStore.getValidated`,
   require `dependencies !== null`, `typeof dependencies === "object"`,
   `Object.getPrototypeOf(dependencies) === Object.prototype`, every member of
   `Object.keys(dependencies)` equals `"resolveStoreIdentityFn"`, and
   `dependencies.resolveStoreIdentityFn === undefined || typeof dependencies.resolveStoreIdentityFn === "function"`.
   A failed predicate throws
   `new PipelineInvariantError("PIPELINE_INPUT_CONFLICT")`.
3. Immediately select
   `const resolveStoreIdentityFn = dependencies.resolveStoreIdentityFn ?? resolveStoreIdentity;`.
4. Replace exactly the existing callback body
   `resolveStoreIdentity(result, identityConfig)` with
   `resolveStoreIdentityFn(result, identityConfig)`.
5. Preserve imports, all two-argument production callers and every other byte.

Required intermediate states:

- before edit: hard-coded real resolver, no dependency object;
- after edit: invalid dependency fails before artifact/DB/external work;
- production/default: selected function is the imported real resolver;
- test override: only the selected resolver function changes; identityConfig,
  scoring, artifact and terminal paths remain real;
- terminal: exact ending digest is recorded by the leaf, not pre-guessed.

LOCAL_NOW from backend:

1. `node --check src/aws-pipeline/services/discovery-worker.js` passes.
2. `git diff --check` passes and the leaf diff contains exactly the writable
   file.
3. A source oracle requires the exact signature, validation, fallback and
   selected call, plus zero production call-site third arguments.
4. A runtime preflight passes `null`, `[]`, `Object.create(null)`, an unknown
   key and a non-function resolver; each must throw `PIPELINE_INPUT_CONFLICT`
   before a manifest-read counter changes from zero.
5. Non-mutating negative controls remove the fallback expression and allow an
   unknown key; the unchanged oracle fails for each, then fresh source passes.

- [ ] `P1` Verify authority, baseline commit/digest and clean attributable path.
- [ ] `T1` Apply only steps 1–4 above.
- [ ] `V1` Run all five LOCAL_NOW checks and record activation outputs.
- [ ] `V2` Record exact ending digest, diff stat and prohibited-action audit.
- [ ] `H1` Return diff/digest/checks only to the window agent.
- [ ] `H2` Stop at `AWAITING_WINDOW_REVIEW`; do not start C153/C154/I124.

Window-agent acceptance requires byte-level inspection, independent recreation
from the starting blob, all LOCAL_NOW proofs, and exact one-file attribution.

### 17.2 `KI-W6-C153` — focused resolver/default/injection enforcement

```yaml
subwindow_id: KI-W6-C153
assignment_id: ASG-KI-W6-C153
type: CORRECTION
status_at_authoring: WAITING_FOR_C152_ACCEPTANCE
predecessors: [KI-W6-C152 independently accepted]
writable_file: email_scraper/test/aws-pipeline-discovery.test.js
starting_sha256: f76f1f35cc07843ec634bd464fffb16b7ab298f3646a657d70fee13be561d7f2
owned_cases: [W6-DB-13]
owned_controls: [W6-NC-22]
read_scope: [accepted C152, email_scraper/src/domain-resolver.js, strict discovery artifacts, existing test helpers/fixture, DEC-KI-058, this block]
prohibited: [second file, production edit, global fetch monkeypatch, live network/provider/AWS/database/browser/build, commit/push, parent artifacts, KI-W7]
```

Exact fixture and oracle:

1. Preserve the five existing top-level tests unchanged. Import
   `resolveStoreIdentity` and add exactly two top-level tests, `W6-DB-13` and
   `W6-NC-22`.
2. Clone the accepted confirmed manifest, retain one query, and replace its
   accepted results with ranks 1–10. For `NN = String(rank).padStart(2,"0")`,
   each URL/title/snippet is respectively
   `https://w6-bridge-q001-r${NN}.myshopify.com/products/result-${NN}`,
   the query text, and the query text; rejectionReason is absent/empty exactly
   as required by the strict manifest parser.
3. Supply the C152 seam with
   `(result, config) => resolveStoreIdentity(result, config, { fetch: deterministicFetch })`.
   `deterministicFetch(url, config, options)` rejects unless URL equals one of
   the ten inputs, `options.purpose === "storefront"`, and
   `options.allowedHostnames` deep-equals `[new URL(url).hostname]`. It returns
   `{status:200, finalUrl:url, contentType:"text/html", rendered:false,
   renderAttempted:false, renderContractVersion:"", fetchAssessment:null}` and
   exact body
   `<!doctype html><html><head><link rel="canonical" href="${url}"><meta name="generator" content="Shopify"></head><body><script>Shopify.theme={};</script><main><h1>${query}</h1><a href="/products/result-${NN}">${query}</a><img src="https://cdn.shopify.com/w6-fixture.png"></main></body></html>`.
   It neither calls nor replaces global fetch.
4. Use the real discovery runtime path. Require exactly ten resolver/fetch
   calls, ten strict stores, ten distinct stable keys and myshopify domains,
   one immutable artifact write, one succeeded terminal, one aggregation check,
   no live network/provider/AWS call and the normal recorded return.
5. Also assert C152's invalid shapes fail before manifest reads and the source
   default expression names imported `resolveStoreIdentity`.
6. `W6-NC-22`: on a fresh fixture, use a sentinel injected resolver/fetch that
   prevents the ten-store result; the unchanged W6-DB-13 oracle must throw.
   Then rerun the untouched actual positive fixture and require pass. The
   control may not attempt live network.
7. Emit exactly one privacy-safe certificate with
   `required/registered/executed/activated = 1/1/1/1`,
   `controlExpected/controlFalsified/freshPositive = 1/1/1`, and the exact
   one-member registry/digests from §17.0.

LOCAL_NOW from backend:

`node --test --test-isolation=none test/aws-pipeline-discovery.test.js`
must report exactly 7 pass, 0 fail, 0 skip and the certificate above.
`node --check test/aws-pipeline-discovery.test.js` and `git diff --check` pass;
the leaf diff is exactly its writable file.

- [ ] `P1` Verify C152 acceptance and the exact starting blob.
- [ ] `T1` Add only the two frozen tests/import/helper code in this file.
- [ ] `V1` Run LOCAL_NOW once after the final edit; record full totals and
  certificate.
- [ ] `V2` Prove W6-NC-22 falsification and fresh positive are non-vacuous.
- [ ] `H1` Return exact diff/digest/certificate only to the window agent.
- [ ] `H2` Stop at `AWAITING_WINDOW_REVIEW`; do not run C154/I124.

### 17.3 `KI-W6-C154` — isolated 100-query/1,000-domain bridge

```yaml
subwindow_id: KI-W6-C154
assignment_id: ASG-KI-W6-C154
type: CORRECTION
status_at_authoring: WAITING_FOR_C152_ACCEPTANCE
predecessors: [KI-W6-C152 independently accepted]
writable_file: email_scraper/test/aws-pipeline-domain.integration.test.js
starting_sha256: e1f10225fb301c9b798032e70fa2bc57c38de5e7374f8c419b7b3928104f3779
owned_cases: [W6-DB-14, W6-DB-15]
owned_controls: [W6-NC-23, W6-NC-24]
read_scope: [accepted C152, domain aggregator, coordinator/run repositories, strict artifact schemas, isolated-postgres helper, accepted discovery/provider fixtures, DEC-KI-058, this block]
prohibited: [second file, production/schema/migration/package edit, live network/provider/AWS/browser/build, public-schema write/cleanup, commit/push, parent artifacts, KI-W7]
```

The leaf preserves the existing G8 top-level test byte-for-byte and adds one
top-level `SCN-KI-046` test with these exact phases:

1. Create `schema` by the exact expression
   ``const schema = `kiw6_bridge_${Date.now()}_${process.pid}`;``, pass that exact
   generated name to `createIsolatedTestSchema`, deploy migrations once,
   instantiate real Prisma/coordinator/run repositories, and assert
   `current_schema()` plus schema-local migration history before writes.
2. Create one running AWS Run and one strict confirmed manifest with 100 ordered
   queries `query_001`…`query_100`, sequence 0…99. Register one discovery stage
   with those exact 100 tasks. Test setup then updates those registered tasks to
   `succeeded` with their exact artifact keys/fingerprints and updates that
   stage to ready with expected/terminal/succeeded counts all 100. It must not
   call production terminal APIs to manufacture this precondition.
3. A validating in-memory artifact store holds the strict manifest and 100
   strict query-discovery artifacts. Starting from the accepted discovery
   fixture, for `QQQ=001..100` and `RR=01..10`, replace consistently in
   `identity`, `candidatePayload`, representative, occurrence, allowed hosts and
   identity evidence every stable/myshopify/resolved hostname and URL with
   `w6-bridge-q${QQQ}-r${RR}.myshopify.com` and
   `https://w6-bridge-q${QQQ}-r${RR}.myshopify.com/products/result-${RR}`.
   Parse every artifact before storing it.
   Assert the pre-invocation union contains exactly 1,000 distinct stable keys.
4. Invoke real `processDomainAggregation` once. The only service dependency is
   `createLeaseMonitorFn`, returning a deterministic monitor whose
   `renewNow/stop` resolve and whose `assertActive` passes; this substitutes
   timer transport only, not fencing/repository semantics. Memory S3 validates
   expected metadata/schema. Memory SQS validates `workMessageSchema` and
   records the single batch.
5. Require exactly 100 query-artifact reads, 1,000 domain-candidate writes, one
   domain-manifest write, one `readAwsReuseInputs`, one
   `publishAwsDomainCheckpoint`, one `sendMany` containing exactly 1,000 unique
   `lead.domain` messages and one `recordDispatch` containing the same 1,000
   IDs. No provider/network/AWS call is available.
6. Query the real database: exactly 1,000 Shops matching production
   `stableShopIdentity/shopIdForStableKey`, exactly 1,000 run-specific RunStores
   matching `runStoreId`, one completed discovery stage, one collecting lead
   stage with expected count 1,000, exactly 1,000 lead tasks, Run stage
   `aws_lead`, `resultsAvailable:false`, and no duplicate identity/task/message.
7. For W6-DB-15 create a second maximum run/stage/artifact set whose 1,000
   otherwise-identical identities use the distinct prefix
   `w6-rollback-q${QQQ}-r${RR}.myshopify.com`, and preinsert a `RunDiagnostic`
   at sequence 100000 whose values conflict with the incoming
   first diagnostic. Real aggregation must throw `PIPELINE_INPUT_CONFLICT`.
   Afterwards require zero run-specific RunStores, lead stage, lead tasks and
   rollback-only Shops; discovery remains `aggregating`; Run remains
   `aws_discovery`, unavailable. A third wrong-token maximum publication call
   must reject before any durable visibility.
8. W6-NC-23 non-mutatingly changes the captured success witness to 999 members
   by duplicating one identity; the unchanged exact cardinality/uniqueness
   assertion must fail, then the fresh database success projection passes.
   W6-NC-24 non-mutatingly changes the captured rollback projection to expose
   one RunStore/lead member; the unchanged zero-visibility assertion must fail,
   then a fresh actual rollback projection passes.
9. In `finally`, disconnect scoped Prisma, drop only the exact generated schema,
   run an administrator query for that exact name and require rowCount zero,
   then disconnect administrator. Cleanup failure fails the test.
10. Emit one privacy-safe certificate:
   new cases required/registered/executed/activated `2/2/2/2`, controls
   expected/falsified/fresh-positive `2/2/2`, counts `100/1000/1000/1000`,
   rollback visibility zero, schema rowCount zero, paid cost `$0.00`.

LOCAL_NOW is deliberately non-stateful. From backend run `node --check
test/aws-pipeline-domain.integration.test.js`, `git diff --check`, and a
file-local/source oracle requiring the exact SCN/case/control registries,
100/1,000 literals, real service/repository/helper imports, rollback/stale-fence
assertions and cleanup/absence query. Non-mutating in-memory source controls
remove one registry ID and one cleanup absence assertion; the unchanged oracle
must fail, then fresh source passes. Neither the leaf nor its independent review
may connect to a database. I124/CV112 is the sole post-edit database execution.

- [ ] `P1` Verify C152 acceptance, isolated URL distinct from production and
  the exact starting blob.
- [ ] `T1` Add only SCN-KI-046 and file-local helpers/imports.
- [ ] `V1` Run only the frozen syntax/diff/source/falsification checks.
- [ ] `V2` Prove the executable test text contains the exact cardinality,
  rollback/fence, control and schema-absence oracles; do not claim runtime pass.
- [ ] `H1` Return diff/digest/certificate only to the window agent.
- [ ] `H2` Stop at `AWAITING_WINDOW_REVIEW`; do not run I124.

### 17.4 `KI-W6-I124` — window-agent-only compositional closure

```yaml
subwindow_id: KI-W6-I124
assignment_id: ASG-KI-W6-I124
type: INTEGRATION_ASSESSMENT
actor: KI-W6-WINDOW-AGENT
writable_implementation_files: []
predecessors: [KI-W6-C152, KI-W6-C153, KI-W6-C154 independently accepted]
state_evidence_writes: [KEYWORD_INTELLIGENCE_KI_W6_TRANSACTION_CLOCK_SUBWINDOW_STATE.md, KEYWORD_INTELLIGENCE_KI_W6_TRANSACTION_CLOCK_SUBWINDOW_EVIDENCE.md append-only]
prohibited: [implementation/test edit, browser rerun, live network/provider/AWS/production, commit/push, KI-W7]
```

Execute once, sequentially:

1. `CV110` independently reconstruct all three leaves from their starting
   blobs; require exact one-file ownership, no duplicate owner, changed set
   exactly the three §17.0 paths/digest, syntax/diff pass, and every leaf-local
   positive/negative-control oracle. If implementation differs from this frozen
   algorithm, reject the leaf; do not repair during I124.
2. `CV111` reuse the accepted C153 7/0/0 and exact `1/1/1/1` case plus
   `1/1/1` control certificate only after proving C152/C153 ending hashes and
   dependencies unchanged after C154. If and only if an input changed, invalidate
   that certificate and run its identical focused command once.
3. `CV112` run exactly once from backend:
   `ALLOW_DATABASE_TESTS=true node -r dotenv/config --test --test-concurrency=1 --test-isolation=none test/aws-pipeline-domain.integration.test.js`.
   Require 2/0/0, the exact case/control/cardinality/rollback/schema certificate
   and administrator rowCount zero for the exact generated `schema` name. One
   identical E8.1 recovery is allowed
   only for proven environment invalidation; behavioral failure is not
   recoverable.
4. `CV113` do not run Chrome. Verify frontend commit and browser digest pinned
   in §17.0. Retain earlier W6 browser evidence only for authenticated workspace,
   durable handoff/100 associated RunQueries, run start, 100 validation/parser
   calls and 100 discovery dispatches. Mark only the old synthetic-fetch
   1,000-domain assertion superseded by SCN-KI-046. Verify the accepted
   1,000-domain traffic corpus and 1,000-domain/12,000-outcome final corpus test
   files/production dependencies are unchanged; record these as compositional
   evidence, never as one monolithic 1,000-domain E2E.
5. `CV114` from backend run once each: `npm test`, `npm run check:secrets`,
   `npm run build:lambda`. Require zero failures/unplanned output, only expected
   guarded DB skips, no secret finding, successful handler packaging and clean
   tracked status. Reuse frontend check/build only after the exact unchanged
   commit/path proof.
6. `CV115` require new case/control registries equal the exact §17.0 sets and
   digests. Merge with the accepted 40/21 sets and require exact 43/24 counts and
   final digests. Every ID must register, execute and activate exactly once; no
   unknown ID. Recompute exact three-file diff, privacy, `$0.00`, no external
   operation, no residual schema/build output and no prohibited path.
7. `CH20` append `WINDOW-AGENT-INTEGRATION-PASS`, set S2
   `READY_FOR_PARENT_REVIEW`, return to parent and stop before KI-W7.

A mechanically determined defect confined to one of the three paths and already
dictated by `DEC-KI-058` may be decomposed by the window agent as C155+/I125+.
Any behavior choice, fourth path, absent isolated database or external
prerequisite is one concise `PARENT_BLOCKED` return.

### 17.5 Dispatch-readiness audit

- [x] One production leaf and two test leaves each own exactly one file.
- [x] The DAG and parallel barrier are exact; I124 has zero implementation write
  authority.
- [x] Starting blobs, path-set digest, interfaces, algorithms, intermediates,
  failure semantics and no-op boundaries are literal.
- [x] Coverage registries, membership digests, counts, activation and three
  independent falsification controls are exact.
- [x] Stateful/build gates are once-only, environment-invalidated recovery is
  bounded, and cleanup/absence witnesses are mandatory.
- [x] Substitute fidelity and claim limits are explicit; no live resolver or
  paid provider is used and no browser-scale simulation remains.
- [x] Unmapped requirements/decisions/tasks/cases/controls and unresolved
  interfaces/intermediates/execution choices/evidence references are all zero.
- [x] Parent-direct authoring exception is requester-authorized; no subordinate
  decomposition or parent decomposition-review stop remains.

## 18. Requester-resumed cleanup-query correction after I124/CV112

### 18.0 Trigger, diagnosis, and authority

The requester supplied a fresh isolated database URL and explicitly authorized
another I124 attempt after `EV-KI-W6-TC34`. That attempt passed the preserved G8
test and reached `SCN-KI-046`, but the cleanup absence query selected PostgreSQL
`pg_namespace.nspname` with internal type `name`. Prisma 6.19.3 rejected that
column before returning the result with `P2010` / unsupported `name` type. The
preceding exact-schema `DROP SCHEMA` completed. This is a test-oracle transport
defect in the already-authorized C154 file; it changes no production behavior,
database contract, schema, migration, or cleanup target.

The current A5 authority explicitly permits `C155+` / `I125+` without parent
return when a mechanically determined correction is confined to one of the
three authorized files and dictated by `DEC-KI-058`. The required administrator
absence proof already fixes the semantic query; PostgreSQL-to-Prisma type
compatibility mechanically requires casting only the selected witness column to
text.

### 18.1 `KI-W6-C155` — serializable exact-schema absence witness

```yaml
subwindow_id: KI-W6-C155
assignment_id: ASG-KI-W6-C155
type: CORRECTION
predecessors: [KI-W6-C154 accepted, I124 resumed CV112 failed after bridge execution at cleanup absence deserialization]
writable_file: email_scraper/test/aws-pipeline-domain.integration.test.js
starting_sha256: 2860a2315d2267bf61028ade7a8101aaa2c89f89d92ef92138609b1495b803f4
read_scope: [the writable file cleanup finally block, Prisma P2010 unsupported-name failure, isolated-postgres text-cast precedent, DEC-KI-058, this block]
prohibited: [second file, production/schema/migration/package change, database execution, browser/build/network/provider/AWS, commit/push, parent artifacts, KI-W7]
```

Exact transformation:

1. In the single administrator absence query after the exact generated-schema
   drop, replace only
   `SELECT nspname FROM pg_namespace WHERE nspname = $1`
   with
   `SELECT nspname::text AS "nspname" FROM pg_namespace WHERE nspname = $1`.
2. Preserve the parameterized exact-name predicate, `residual.length`, the
   zero-row assertion, both disconnects, every scenario/case/control registry,
   every production-path assertion, and every other byte.
3. Do not connect to a database. `KI-W6-I125` exclusively owns the next
   stateful execution.

LOCAL_NOW from backend:

- `node --check test/aws-pipeline-domain.integration.test.js` passes.
- `git diff --check` passes and the attributable diff is exactly the writable
  file with one replacement line.
- A source oracle requires the exact text cast/alias, parameterized predicate,
  `schema` argument, `residual.length`, and `assert.equal(schemaRowCount, 0)`.
- A non-mutating negative control removes `::text AS "nspname"`; the unchanged
  oracle fails, then fresh source passes.

- [ ] `P1` Verify requester resumption, C154 accepted digest, current clean
  backend commit and exact starting blob.
- [ ] `T1` Apply only the one frozen query-string replacement.
- [ ] `V1` Run the syntax, diff, source and falsification LOCAL_NOW gates without
  a database connection.
- [ ] `V2` Prove exact one-file attribution and every C154 registry/oracle remains
  byte-identical outside the query string.
- [ ] `H1` Return exact diff/digest/checks only to the window agent.
- [ ] `H2` Stop at `AWAITING_WINDOW_REVIEW`; do not run I125.

### 18.2 `KI-W6-I125` — post-C155 whole-window reassessment

```yaml
subwindow_id: KI-W6-I125
assignment_id: ASG-KI-W6-I125
type: INTEGRATION_ASSESSMENT
actor: KI-W6-WINDOW-AGENT
writable_implementation_files: []
predecessors: [KI-W6-C152, KI-W6-C153, KI-W6-C154, KI-W6-C155 independently accepted]
state_evidence_writes: [KEYWORD_INTELLIGENCE_KI_W6_TRANSACTION_CLOCK_SUBWINDOW_STATE.md, KEYWORD_INTELLIGENCE_KI_W6_TRANSACTION_CLOCK_SUBWINDOW_EVIDENCE.md append-only]
prohibited: [implementation/test edit, browser rerun, live network/provider/AWS/production, commit/push, KI-W7]
```

`I125` must:

1. Reperform CV110 for the four current file results, prove C155 changed only
   the exact cleanup query string, and prove the assembled implementation/test
   changed-file set remains the exact three §17.0 paths/digest.
2. Reuse CV111 only after unchanged C152/C153 hashes and dependency closure.
3. Run the exact CV112 database command once against the requester-supplied
   isolated URL. Require 2/0/0, the exact `SCN-KI-046` certificate, and schema
   row-count zero. A behavioral failure is not an identical recovery.
4. If CV112 passes, execute CV113 through CV115 and CH20 exactly as §17.4.
5. Record `READY_FOR_PARENT_REVIEW` only after every gate passes. A new failure
   outside the three-file scope or not mechanically determined by DEC-KI-058 is
   `PARENT_BLOCKED`.
