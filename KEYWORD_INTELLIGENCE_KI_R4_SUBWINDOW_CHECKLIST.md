# KI-R4 Sub-Window Decomposition Checklist (`S1`)

**Artifact role:** Sole subordinate authority for KI-R4 sub-window DAG, exact file
assignments, task specifications, checks, and handoff requirements.
**Companion artifacts:** `S2` `KEYWORD_INTELLIGENCE_KI_R4_SUBWINDOW_STATE.md`
(live status), `S3` `KEYWORD_INTELLIGENCE_KI_R4_SUBWINDOW_EVIDENCE.md`
(append-only evidence).
**Document status:** parent-reviewed decomposition. Live execution status exists
only in S2.

## 0. Inherited authority and revision pins

### 0.1 Parent package

| Artifact | Path | Revision / value |
|---|---|---|
| Parent window | `KI-R4` in `KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md` (A4) | `310011aa3d855cd4ce4d6ef5054d94e5b8f413b8b86543048fea065113a10cf6` |
| Product contract (A1) | `KEYWORD_INTELLIGENCE_PRODUCT_CONTRACT.md` | `8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c` |
| Decision ledger (A3) | `KEYWORD_INTELLIGENCE_DECISION_LEDGER.md` | `4b2202d870da5df64ae324ad570adf1b6437689883cb49b118bcc8d1f170d9de` |
| Parent standard | `PROJECT_AGNOSTIC_DECISION_COMPLETE_CHECKLIST_AUTHORING_STANDARD.md` | `3b7a4fd25156e1adfbc92abb835c5f82a0d18c686b1c1150feb202f2d944d2ac` |
| Sub-window standard | `PROJECT_AGNOSTIC_WINDOW_AGENT_SUBWINDOW_AUTHORING_STANDARD.md` | `1766f9107ce7d315877b75d4b0ea2b5521dff1c321e12f890b03787d66196ded` (matches the KI-R4 header pin) |
| Parent window ID | `KI-R4` | — |
| Parent assignment ID | `ASG-KI-R4-WA-01` | A5 state 98 |
| Window agent identity | `KI-R4-WINDOW-AGENT` | — |
| Baseline backend revision | `email_scraper` HEAD, clean | `077213cc7c33fa8209a1e5d8ff365b73766500dc` |
| Baseline frontend revision | `frontend` HEAD, clean | `0dfa1acac50fac3a86d02ec674c6d2bab645832d` |
| Fixed R3 diff pair | `37a0e0203d265f539b566f1536642cd2f4eb2d99` → `077213cc7c33fa8209a1e5d8ff365b73766500dc` | per `DEC-KI-032` |

### 0.2 Governing decisions consumed

`DEC-KI-026` through `DEC-KI-032` (A3), in particular `DEC-KI-031` (recovery
schedules, dispatcher strictness, private-member sets) and `DEC-KI-032`
(durable identity gate, own-key gate, commit-stable conformance, falsification
controls, database registration, R4 case manifest, verification economy).
Parent task blocks: `KI-R4-T1`–`T4`; scenarios `SCN-KI-033`–`035` plus corrected
`SCN-KI-028`–`032`.

### 0.3 Assignment and bootstrap disposition

1. A5 state 98 assigns `ASG-KI-R4-WA-01` to `KI-R4-WINDOW-AGENT` and authorizes
   sequential delegation only; the window agent is not a leaf implementation
   agent.
2. `EV-KI-R3-02`, `CHG-KI-015`, and `EV-KI-A-037` are present in the parent
   package and resolve the KI-R4 correction and assignment references.
3. The exact R4 manifest was created during the aborted pre-review attempt. Its
   970-byte content and SHA-256 match I-F3, so parent review accepts only
   `KI-R4-S003` as completed bootstrap work. No other implementation leaf was
   accepted or started, and remaining leaves require separate leaf agents.
4. The window agent will not edit A5/A6. Parent acceptance, A5 CAS, and KI-W4
   assignment remain parent-only.

## 1. Parent-window scope and exclusions (copied, not expanded)

- **Delegable implementation write scope (the only files leaves may write):**
  1. `email_scraper/src/aws-pipeline/keyword-intelligence/service.js` — `recoverClaimedTask` only
  2. `email_scraper/src/aws-pipeline/adapters/queue-dispatcher.js` — `SqsDispatcher.sendOne` only
  3. `email_scraper/test/fixtures/keyword-intelligence/ki-r4-enforcement-manifest-v1.json` — new exact manifest only
  4. `email_scraper/test/keyword-intelligence-adapter.test.js` — additive KI-R4 control and fixed R3 digest assertion only
  5. `email_scraper/test/aws-pipeline-runtime-adapters.test.js` — additive KI-R4 dispatcher cases and fixed R3 digest assertion only
  6. `email_scraper/test/keyword-intelligence-worker.test.js` — recovery fixtures/cases, T18/R18 controls, SCN-KI-030 registration/isolation structure, fixed R3/R4 digest assertions only
  7. `email_scraper/test/keyword-intelligence-worker-flow.test.js` — G24 control replacement and fixed R3/R4 digest assertions only
  8. `email_scraper/test/keyword-intelligence-enforcement.test.js` — SCN-KI-032 fixed-revision/hashes plus additive KI-R4 conformance only
- **Window-agent coordination writes:** S1/S2/S3 paths in §0.1 only.
- **Read-only scope:** `dataforseo-labs-adapter.js`, `keyword-intelligence/repository.js`,
  `core/lease-monitor.js`, `ki-r3-enforcement-manifest-v1.json` fixture,
  repository unit/integration/recovery tests, `aws-pipeline-packaging.test.js`,
  `scripts/build-keyword-worker.js`, `email_scraper/prisma/**`, `frontend/**`,
  A1–A8 except parent-only post-review updates.
- **Prohibited (each leaf and the window agent):** window-agent implementation
  edits, leaf multi-file edits, parallel leaf execution, direct parent-leaf
  communication, leaf subdelegation, parent A5/A6 updates by the window agent,
  provider calls, AWS operations, production database writes, full database
  integration suite, repeated successful database gate without invalidation,
  Prisma generate/validate, seven-handler build/measure,
  repository/schema/migration/contract/key/handler/recovery/build-script/adapter-source
  edits, API/frontend/package edits, source-mutation controls, commits/pushes,
  KI-W4 work.
- **Successor:** `KI-W4`, reserved for parent; `may_start_successor:false` everywhere.

## 2. Starting working-tree inventory (frozen at authoring; `EV-KI-R4-S01`)

| # | Planned file | Operation | Starting digest |
|---|---|---|---|
| F-001 | `email_scraper/src/aws-pipeline/keyword-intelligence/service.js` | MODIFY | `a04be9ca96f6efb0a123c2e052df93c4bd92b0a1163d291d10e8052e3fae401f` |
| F-002 | `email_scraper/src/aws-pipeline/adapters/queue-dispatcher.js` | MODIFY | `453a323bd8929ea254f077b39bb5a62a82cc77490c8f5ac5f45485d730fef046` |
| F-003 | `email_scraper/test/fixtures/keyword-intelligence/ki-r4-enforcement-manifest-v1.json` | CREATE | `ABSENT` |
| F-004 | `email_scraper/test/keyword-intelligence-worker.test.js` | MODIFY | `4cdb622baa4a920ee6588ebcee278910ba08a7ab09f4591c18c7a756e86a3e2f` |
| F-005 | `email_scraper/test/keyword-intelligence-adapter.test.js` | MODIFY | `f48d0d2d348a86e0128b9ba3ec034648286ce4f2c4d5c20c99ee88cbfa779764` |
| F-006 | `email_scraper/test/aws-pipeline-runtime-adapters.test.js` | MODIFY | `4be47e21bddab690017ff18887ef284d9ab6781d825b5998aaec04da2a34722f` |
| F-007 | `email_scraper/test/keyword-intelligence-worker-flow.test.js` | MODIFY | `4fe1b890d3aa2b53001b4ea5da19bdf981b3780a2c2e24857a7e1184e6fe2856` |
| F-008 | `email_scraper/test/keyword-intelligence-enforcement.test.js` | MODIFY | `2d8f8cb5cd8c731052c112f1e979a60d09cf04230fff97252e7a4b8a1d795172` |

- Planned eight-path set digest (§4.7 formula): `ccfa1089d1d62656afde3927cd0b42128856713442dcbda5d30dd47a6b5333f6` — equals the KI-R4 header `required_initial_file_set_digest`. Verified `EV-KI-R4-S01`.
- `git -C email_scraper status --porcelain` = empty; `git -C frontend status --porcelain` = empty.
- Root coordination repo: owner-controlled relocation state preserved — 29
  dirty/untracked root paths (nested trees appear as `M email_scraper`/`M frontend`);
  starting root change-set digest `df17885e439b7ebf2d72282f80b3b684bebaec7a9486fc741c51be176f4600ae`.
  The only permitted root additions are the three S artifacts. Never stage,
  commit, move, or repair this state.
- Source-defect reproduction (`EV-KI-R4-S02`): `service.js:424-543` classifies
  `planned|succeeded|failed` attempts without any attempt/task request-fingerprint
  equality gate before schedules 2/4/5 (the `succeeded` schedule alone checks at
  line 446); `queue-dispatcher.js:34` enumerates options with `Object.keys`;
  `keyword-intelligence-enforcement.test.js:110-111,208,217` uses live
  `git diff`/`git status`; the five R3 group runners end in
  `assert.match(hash, /^[a-f0-9]{64}$/)`; R3-A01/T18/R18/G24 controls alter
  inputs rather than captured evidence; `SCN-KI-030` (worker test line 1358)
  takes no test context and `t_scn030` (line 1372) opens one schema per case.

## 3. Frozen cross-file interfaces and digest formulas (interface freeze)

| ID | Frozen fact |
|---|---|
| I-F1 | `recoverClaimedTask({taskId,token,current,message,kind,runtime,research,stage,config,monitor})` signature and its two-member return union `{outcome:"proceed"}|{outcome:"recovered",result}` are unchanged. New behavior: immediately after `const latestAttempt = current.latestAttempt; if (!latestAttempt) return { outcome: "proceed" };` and before the `now` binding or any state classification, execute `if (latestAttempt.requestFingerprint !== current.task.requestFingerprint) invariant();` where `invariant()` is the existing `service.js` helper defaulting to `PipelineInvariantError("PIPELINE_INPUT_CONFLICT")` (service.js line 57). Strict `!==` on the raw stored values: `null===null` passes; `undefined`, or any different 64-hex value, throws. Zero cache reads, ambiguity writes, retry schedules, S3 operations, terminal writes, and dispatches occur on mismatch. |
| I-F2 | `async sendOne(queueUrl, message, schema, options = {})` signature, return union, and existing predicates are unchanged. The single production edit replaces `const keys = Object.keys(options);` (queue-dispatcher.js line 34) with `const keys = Reflect.ownKeys(options);`. The existing length/key predicate at line 35 then rejects symbol keys and non-enumerable extras (a lone symbol key fails `keys[0] !== "delaySeconds"`; any second own key fails length). Validation still precedes command construction and `client.send`. |
| I-F3 | New fixture `ki-r4-enforcement-manifest-v1.json` byte-exact content: UTF-8, 2-space JSON indentation, one trailing LF, 970 bytes, sha256 `7700c1ebb02514cdf89ee2c4c729ef91c3c14aa6fec25d99161bf37e07f01702`, root exactly `{contractVersion:"ki-r4-enforcement-manifest-v1",groups}` with groups `adapter_control`(1), `dispatcher`(2), `worker_component`(5), `aggregation_control`(1), `conformance`(6) holding exactly the literal ordered IDs of `DEC-KI-032`/A4. Full literal content embedded in sub-window `KI-R4-S003`. |
| I-F4 | Digest formula F-D1 (R3 scenario digests; historical, matches the committed R3 fixture literals): `sha256(Buffer.from(sortedIds.join("\n"),"utf8"))` — no trailing LF. Fixed literals: adapter `b4ede4c2a1a32fddc1a1ac67e023a81f93c6863632cdff2be421f20d51080e4f`, dispatcher `962ad70760c71a6fcf08b73d5edf0cdccad27dea9c3414c552c1d8e3e2b99226`, task_component `d6773f3749e9f68c3b270df9ad63aba6297328b5578d1e5f3346ee2683518110`, recovery_component `b6d8b7a1435b6a62da061980afd370290f16b899774bba32578e3df9cc5f2737`, task_database `9e8a3973d5430be70e26f68bb235b831b96f17162d30277a40b06942cc94e934`, aggregation `c017cd869b11a93e86070112ed626a3cd299e00a518ed3a568dd8f1331c27b14`, conformance `43bbc0bd4dd296447b989ee2125fc0f991c2451f29e3f4ef87c05f8685a607f8`, global-101 `70bd758e68cb32aff7dc418356d68e3ca07dadf282f76e7484858a7ec0c9470b`. All eight verified against the R3 fixture in `EV-KI-R4-S02`. |
| I-F5 | Digest formula F-D2 (R4 manifest/path/ID sets; sub-window standard §4.7): sort distinct members by unsigned UTF-8 byte order, encode each member + one LF, concatenate, sha256. R4 15-ID global digest `6adc8ab132496c58608734549fbbc596577e1bd71c1e730349575eb96badc941` (verified `EV-KI-R4-S02`). F-D1 and F-D2 are not interchangeable; each assertion names its formula. |
| I-F6 | R4 case-runner conventions: each R4 group executes inside a labeled `test("SCN-KI-03x: …")` — worker/`SCN-KI-033` (R4-W01–W03), runtime-adapters/`SCN-KI-033` (R4-Q01–Q02), adapter/`SCN-KI-034` (R4-A01), worker/`SCN-KI-034` (R4-W04–W05), worker-flow/`SCN-KI-034` (R4-G01), enforcement/`SCN-KI-035` (R4-C01–C06). Every case runs as a named `t.test(<manifest ID>)` subtest; the runner pushes the ID to its executed array only after that subtest's oracle succeeds and finishes with sorted set equality and count equality against the R4 manifest group. No R4 group digest literal is asserted at file level (none is pinned by A4); the global R4 digest is asserted only in the enforcement runner preamble via F-D2. |
| I-F7 | R3 group runners keep their existing structure and replace only the final regex digest assertion with F-D1 literal equality for their group. The worker file splits its combined 36-ID hash into two per-group hashes (task_component and recovery_component executed arrays) against the two F-D1 literals. |
| I-F8 | Falsification-control convention (`DEC-KI-032`): run the real production path and unchanged oracle once (passing); copy the captured in-memory result/trace; apply exactly the prescribed mutation to the copy; rerun the identical oracle against the copy and require `AssertionError` (via `assert.throws(..., (e) => e instanceof assert.AssertionError)`); rerun the production path unchanged and require pass. Mutations: A01 `delete copy.providerCostUsd`; W04 `copy.trace.push("sendCheck")`; W05 `copy.trace.push("terminalize","sendCheck")`; G01 `copy.trace.push("s3.put")`. Production source is never mutated; a different valid input is never substituted. |
| I-F9 | Enforcement fixed-revision facts: permanent Git assertions use only `git diff 37a0e0203d265f539b566f1536642cd2f4eb2d99 077213cc7c33fa8209a1e5d8ff365b73766500dc -U0 -- <path>` and `git diff --name-only <same pair>`; C05 requires nonempty hunks for all three R3 production files before span checks (adapter spans `[[46,56]]`, dispatcher `[[28,50]]`, service spans `[[305,408],[410,488],[490,509]]` — unchanged constants, now against the fixed diff); C06 path set = the nine literal R3 paths already in `AUTHORIZED_WRITE_PATHS`; C07 prohibits added imports matching `/sqlite|python|subprocess|python-shell|node:worker/u` in the fixed diff. No live `git status` and no revision-less `git diff` remain anywhere in the five test files. |

## 4. Initial single-file dependency DAG

```text
KI-R4-S001 service.js ─────────────┐
KI-R4-S002 queue-dispatcher.js ────┤   (independent productions)
KI-R4-S003 R4 manifest fixture ────┤
                                   ▼
KI-R4-S004 worker.test.js  (consumes I-F1 fence, I-F3 manifest, I-F4/I-F7 digests, T4 restructure)
KI-R4-S005 adapter.test.js (consumes I-F3, I-F4, I-F8)
KI-R4-S006 runtime-adapters.test.js (consumes I-F2, I-F3, I-F4, I-F6)
KI-R4-S007 worker-flow.test.js (consumes I-F3, I-F4, I-F8)
KI-R4-S008 enforcement.test.js (consumes I-F3, I-F4, I-F5, I-F9; closure)
KI-R4-I001 integration assessment (window agent; zero implementation writes)
```

S003 is the accepted bootstrap leaf. Exactly one remaining leaf may be active
at a time; remaining execution order is S001→S002→S004→S005→S006→S007→S008.
Every edge names its frozen interface above. The graph is acyclic; every file
has exactly one initial owner; no sub-window owns more than one file.

### 4.1 Intermediate-state contracts

| Edge | Permitted state / local checks | Exact expected temporary failure | Resolver | Prohibitions while state exists |
|---|---|---|---|---|
| IS-1 after S001 | service.js fenced; `node --check service.js` passes; adapter/flow/enforcement tests unaffected | `test/keyword-intelligence-worker.test.js` `SCN-KI-029` recovery_component group (R09, R10, R12–R16 fixtures with `requestFingerprint:null` attempts vs real `reqFp` tasks) throws `PIPELINE_INPUT_CONFLICT` at the new gate | S004 (fixtures adopt the real task fingerprint) | Running the worker test file or `npm test` as a leaf check; any production edit beyond line-34-class fence |
| IS-2 after S002 | dispatcher own-key strict; existing Q01–Q12 and all three/four-argument callers unaffected; `node --check` passes | none | — | — |
| IS-3 after S003 | fixture parses (`JSON.parse`) and hashes to I-F3; nothing consumes it yet | none | — | Editing the R3 fixture |
| IS-4 after S004 | worker file green non-DB: `SCN-KI-029` per-group digests green with real fingerprints; `SCN-KI-033/034` worker groups green; `SCN-KI-030` restructured and skipped without `ALLOW_DATABASE_TESTS` | `SCN-KI-030` durable oracles unexecuted locally (skip-guarded) | V3 database gate at I001 | Any database run before the frozen V3 gate |
| IS-5 after S005–S007 | each file self-green under its focused LOCAL_NOW pattern | none | — | Running other files' patterns |
| IS-6 after S008 | all five files green under the full V2 pattern; permanent conformance reads fixed revisions only | none | — | Any further edit without a corrective sub-window |

## 5. Sub-window blocks

### 5.1 `KI-R4-S001` — service.js durable identity fence

```yaml
subwindow_id: KI-R4-S001
type: FILE
parent_window_id: KI-R4
parent_assignment_id: ASG-KI-R4-WA-01
assigned_agent: UNASSIGNED
predecessors: []
successor_reserved_for: WINDOW-AGENT
writable_file: email_scraper/src/aws-pipeline/keyword-intelligence/service.js
file_operation: MODIFY
starting_file_digest: a04be9ca96f6efb0a123c2e052df93c4bd92b0a1163d291d10e8052e3fae401f
starting_repository_change_set_digest: df17885e439b7ebf2d72282f80b3b684bebaec7a9486fc741c51be176f4600ae
read_only_scope: [email_scraper/src/aws-pipeline/keyword-intelligence/service.js (pre-edit), email_scraper/src/keyword-intelligence/repository.js, email_scraper/test/keyword-intelligence-worker.test.js, KEYWORD_INTELLIGENCE_DECISION_LEDGER.md DEC-KI-032]
authorized_actions: [single_file_edit, node --check, focused non-database diagnostics on files other than the worker test file]
prohibited_actions: [edit of any symbol other than recoverClaimedTask, new imports/helpers/exports, worker test edits, database runs, every §1 prohibition]
may_start_successor: false
```

**Mechanical trace:** `KI-R4-T1`; `REQ-KI-002`,`005`,`022`,`023`; `INV-KI-004`–`008`;
`DEC-KI-026`,`030`–`032`; activation witness for `SCN-KI-033` cases R4-W01–W03.

**Exact file transformation:**
1. Source anchor: service.js lines 424–427 — current body loads `latestAttempt`,
   returns `proceed` when absent, then binds `now` and enters state classification
   (planned/in_flight at 429, succeeded at 445 with its own inline equality check
   at 446, failed at 500) with no attempt/task identity gate.
2. Target anchor: the gap between line 426 (`if (!latestAttempt) return { outcome: "proceed" };`)
   and line 427 (`const now = () => nowOf(runtime);`).
3. Ordered edits: insert exactly one statement after line 426:
   `if (latestAttempt.requestFingerprint !== current.task.requestFingerprint) invariant();`
   No other line is added, deleted, or modified.
4. Complete formulas: strict raw-value `!==` (byte-for-byte equality of the stored
   lowercase 64-hex strings; `null===null` passes; `undefined`/any other value throws);
   `invariant()` (line 57) throws `PipelineInvariantError("PIPELINE_INPUT_CONFLICT")`.
5. Imports/exports/callers: none change; `processTask` remains the sole caller;
   schedules 1–6 of `DEC-KI-031` are untouched, including the now-redundant
   succeeded-schedule check at line 446 (retained deliberately).
6. Operation order: the guard is a read-only fail-closed check before every
   durable or external operation in all six schedules.
7. Outcomes: every redelivery with unequal durable identity throws
   deterministically with zero forbidden operations; equal replay follows the six
   accepted schedules unchanged; lease/token behavior unchanged; no cancellation.
8. Preserved behavior: every other symbol and every equal-identity trace/result.
9. Obsolete behavior removed: none (the defect was an omission).
10. Resulting interface for successors: I-F1.
11. Forbidden edits within the file: every symbol other than `recoverClaimedTask`;
    any new helper/const/import.

**Exact checks (LOCAL_NOW unless noted):**
- C1 `node --check email_scraper/src/aws-pipeline/keyword-intelligence/service.js` exit 0.
- C2 `node --test --test-isolation=none --test-name-pattern='SCN-KI-028|SCN-KI-031|SCN-KI-032' test/keyword-intelligence-adapter.test.js test/keyword-intelligence-worker-flow.test.js test/keyword-intelligence-enforcement.test.js` (run from `email_scraper/`) — all pass, proving no non-worker regression. The worker test file is not run (IS-1).
- C3 Focused worker-file falsification expectation `DEFERRED_TO_INTEGRATION` (owned by S004 local checks and the I001 gates).
- V2 write-set proof: attributable changed-file set == exactly this file.

**Completion checklist (leaf must return each with evidence):**
- [ ] P1 Revisions, assignment identity, writable file, baseline digest match S1/S2.
- [ ] P2 Starting repository status matches §2 baseline (nested clean; root = inventory + three S artifacts).
- [ ] T1 Apply the one ordered insertion and no other edit.
- [ ] V1 Run C1–C2 and record outputs.
- [ ] V2 Prove attributable changed-file set is exactly `email_scraper/src/aws-pipeline/keyword-intelligence/service.js`.
- [ ] V3 Coverage: this leaf registers no case IDs; its activation witness is S004's R4-W01–W03.
- [ ] H1 Return exact diff, ending digest, commands, outcomes, deferred obligations.
- [ ] H2 Confirm no prohibited action, second-file edit, successor work, external mutation, or parent communication.
- [ ] H3 Stop at `AWAITING_WINDOW_REVIEW`.

### 5.2 `KI-R4-S002` — queue-dispatcher own-key enumeration

```yaml
subwindow_id: KI-R4-S002
type: FILE
parent_window_id: KI-R4
parent_assignment_id: ASG-KI-R4-WA-01
assigned_agent: UNASSIGNED
predecessors: []
successor_reserved_for: WINDOW-AGENT
writable_file: email_scraper/src/aws-pipeline/adapters/queue-dispatcher.js
file_operation: MODIFY
starting_file_digest: 453a323bd8929ea254f077b39bb5a62a82cc77490c8f5ac5f45485d730fef046
starting_repository_change_set_digest: df17885e439b7ebf2d72282f80b3b684bebaec7a9486fc741c51be176f4600ae
read_only_scope: [email_scraper/src/aws-pipeline/adapters/queue-dispatcher.js (pre-edit), KEYWORD_INTELLIGENCE_DECISION_LEDGER.md DEC-KI-031/032]
authorized_actions: [single_file_edit, node --check, focused dispatcher diagnostics on test/aws-pipeline-runtime-adapters.test.js]
prohibited_actions: [edit of any symbol other than SqsDispatcher.sendOne, message parsing or batch changes, every §1 prohibition]
may_start_successor: false
```

**Mechanical trace:** `KI-R4-T2`; `REQ-KI-021`–`023`; `INV-KI-002`,`008`,`009`;
`DEC-KI-009`,`031`,`032`; activation witness for `SCN-KI-033` cases R4-Q01–Q02.

**Exact file transformation:**
1. Source anchor: queue-dispatcher.js lines 28–39 — `sendOne` parses the message,
   computes `logicalId`, validates options with the non-null/non-array/plain-
   `Object.prototype` check (lines 32–33), then enumerates with
   `Object.keys(options)` (line 34) and validates the key set and integer range.
2. Target anchor: line 34 only.
3. Ordered edits: replace `const keys = Object.keys(options);` with
   `const keys = Reflect.ownKeys(options);`. No other line changes.
4. Formulas/bounds: accepted key lists are exactly `[]` or `["delaySeconds"]`
   (string); a symbol own key or non-enumerable extra appears in the list and is
   rejected by the unchanged line-35 predicate (`keys.length > 1` or
   `keys[0] !== "delaySeconds"`); integer `0..900` validation unchanged;
   key order is irrelevant because at most one key is accepted.
5. Callers: every existing three/four-argument caller is byte-compatible; Q01–Q12
   outcomes unchanged.
6. Operation order: rejection throws `PIPELINE_MESSAGE_INVALID` before command
   construction and `client.send`; the dispatcher remains stateless.
7. Outcomes: symbol/non-enumerable extras reject deterministically with zero
   sends; valid send failure keeps `{sentItemIds:[],failedItemIds:[logicalId]}`.
8. Preserved: everything else in the file, including `sendMany`.
9. Removed: the `Object.keys` enumeration only.
10. Resulting interface: I-F2.
11. Forbidden edits: any other line, symbol, or export.

**Exact checks (LOCAL_NOW):**
- C1 `node --check` exit 0.
- C2 `node --test --test-isolation=none --test-name-pattern='SCN-KI-028' test/aws-pipeline-runtime-adapters.test.js` — Q01–Q12 all pass unchanged.
- V2 write-set proof == exactly this file.

**Completion checklist:** P1/P2/T1/V1/V2/V3/H1/H2/H3 as in 5.1 (V3: activation
witness is S006's R4-Q01/Q02).

### 5.3 `KI-R4-S003` — R4 enforcement manifest fixture

```yaml
subwindow_id: KI-R4-S003
type: FILE
parent_window_id: KI-R4
parent_assignment_id: ASG-KI-R4-WA-01
assigned_agent: UNASSIGNED
predecessors: []
successor_reserved_for: WINDOW-AGENT
writable_file: email_scraper/test/fixtures/keyword-intelligence/ki-r4-enforcement-manifest-v1.json
file_operation: CREATE
starting_file_digest: ABSENT
starting_repository_change_set_digest: df17885e439b7ebf2d72282f80b3b684bebaec7a9486fc741c51be176f4600ae
read_only_scope: [email_scraper/test/fixtures/keyword-intelligence/ki-r3-enforcement-manifest-v1.json, KEYWORD_INTELLIGENCE_DECISION_LEDGER.md DEC-KI-032]
authorized_actions: [single_file_create, JSON parse + digest verification]
prohibited_actions: [edit of the R3 fixture, any other file, every §1 prohibition]
may_start_successor: false
```

**Mechanical trace:** `KI-R4-T3` interface item; `DEC-KI-032` R4 case manifest;
consumed by S004–S008 runners and the I001 cumulative coverage certificate.

**Exact file transformation:** create the file with exactly this byte content
(970 bytes, sha256 `7700c1ebb02514cdf89ee2c4c729ef91c3c14aa6fec25d99161bf37e07f01702`):

```json
{
  "contractVersion": "ki-r4-enforcement-manifest-v1",
  "groups": {
    "adapter_control": [
      "R4-A01-active-cost-output-omission-falsifies"
    ],
    "dispatcher": [
      "R4-Q01-symbol-extra-key-rejected",
      "R4-Q02-nonenumerable-extra-key-rejected"
    ],
    "worker_component": [
      "R4-W01-planned-identity-mismatch-conflict",
      "R4-W02-terminal-failure-identity-mismatch-conflict",
      "R4-W03-retryable-identity-mismatch-conflict",
      "R4-W04-ordinary-lost-check-injection-falsifies",
      "R4-W05-recovery-lost-write-injection-falsifies"
    ],
    "aggregation_control": [
      "R4-G01-post-loss-operation-injection-falsifies"
    ],
    "conformance": [
      "R4-C01-fixed-revision-diff-nonempty",
      "R4-C02-fixed-revision-file-set-exact",
      "R4-C03-fixed-revision-import-set-clean",
      "R4-C04-r3-group-digests-exact",
      "R4-C05-r3-global-digest-exact",
      "R4-C06-live-worktree-independent"
    ]
  }
}
```
(with a single trailing newline after the closing brace; 2-space indentation as shown).

**Exact checks (LOCAL_NOW):** C1 `JSON.parse` succeeds; C2 sha256 equals the
pinned digest; C3 F-D2 15-ID global digest computed from the parsed content
equals `6adc8ab132496c58608734549fbbc596577e1bd71c1e730349575eb96badc941`;
V2 write-set proof == exactly this new file.

**Completion checklist:** P1/P2/T1/V1/V2/V3/H1/H2/H3 as in 5.1 (V3: fixture IDs
are the registered set for all R4 groups; execution witnesses land in S004–S008).

### 5.4 `KI-R4-S004` — worker test: identity fixtures, R4 worker cases, per-group digests, single-schema SCN-KI-030

```yaml
subwindow_id: KI-R4-S004
type: FILE
parent_window_id: KI-R4
parent_assignment_id: ASG-KI-R4-WA-01
assigned_agent: UNASSIGNED
predecessors: [KI-R4-S001, KI-R4-S003]
successor_reserved_for: WINDOW-AGENT
writable_file: email_scraper/test/keyword-intelligence-worker.test.js
file_operation: MODIFY
starting_file_digest: 4cdb622baa4a920ee6588ebcee278910ba08a7ab09f4591c18c7a756e86a3e2f
starting_repository_change_set_digest: df17885e439b7ebf2d72282f80b3b684bebaec7a9486fc741c51be176f4600ae
read_only_scope: [email_scraper/src/aws-pipeline/keyword-intelligence/service.js, email_scraper/test/fixtures/keyword-intelligence/ki-r3-enforcement-manifest-v1.json, email_scraper/test/fixtures/keyword-intelligence/ki-r4-enforcement-manifest-v1.json, email_scraper/test/helpers/isolated-postgres.js, KEYWORD_INTELLIGENCE_DECISION_LEDGER.md DEC-KI-031/032]
authorized_actions: [single_file_edit, node --check, focused non-database worker-test runs, DEFERRED database structure preparation owned by the V3 gate]
prohibited_actions: [weakening or deleting any existing assertion or case, editing production files, running the database gate, every §1 prohibition]
may_start_successor: false
```

**Mechanical trace:** `KI-R4-T1` fixtures/cases R4-W01–W05; `KI-R4-T3` digest
assertions; `KI-R4-T4` entire task; `REQ-KI-002`,`005`,`022`,`023`;
`INV-KI-004`–`008`; `DEC-KI-026`,`028`–`032`; `SCN-KI-030`,`033`,`034`.

**Exact file transformation (ordered):**
1. **Fixtures (IS-1 resolver):** in the recovery_component fixtures for ordinary
   cases R3-R09 (planned), R3-R10 (auth failure), R3-R11 (contract failure),
   R3-R12 (task failure), R3-R13 (retryable), R3-R14 (attempt five), R3-R16
   (monitor stopped before dispatch), and the R3-T17 attempt-five task fixture
   where applicable, replace `requestFingerprint: null` on `latestAttempt` with
   the harness task's real fingerprint constant (the same value
   `componentHarness` assigns to `task.requestFingerprint`, i.e. `reqFp` — expose
   it by referencing the existing computation, not by introducing a new constant
   where one already exists). R3-R01–R08 already use `succeededAttempt()` with
   equal fingerprints and remain byte-identical.
2. **Digest split (I-F7):** in `SCN-KI-029` (line 1293), maintain two executed
   arrays — `executedTask` and `executedRecovery` — and replace the combined
   hash + regex (lines 1307–1312) with: sorted set-equality and count for each
   group (unchanged semantics, per array), then two F-D1 literal equalities:
   task_component `d6773f3749e9f68c3b270df9ad63aba6297328b5578d1e5f3346ee2683518110`
   and recovery_component `b6d8b7a1435b6a62da061980afd370290f16b899774bba32578e3df9cc5f2737`.
3. **R4 manifest load:** add `const R4_MANIFEST = JSON.parse(readFileSync(<URL to ki-r4-enforcement-manifest-v1.json>,"utf8"))` beside the existing R3 manifest load, using the file's existing import idiom.
4. **New `SCN-KI-033` worker runner:** `test("SCN-KI-033: durable attempt/task request identity fence rejects every unequal mismatch", async (t) => {...})` executing `R4_MANIFEST.groups.worker_component` IDs `R4-W01-…conflict`, `R4-W02-…conflict`, `R4-W03-…conflict` as named subtests:
   - W01: `componentHarness({ latestAttempt: { attemptNumber: 1, state: "planned", requestFingerprint: fp("r4-w01-other"), resultFingerprint: null, providerCostUsd: "0.01560000", safeErrorCode: null }, markAmbiguousOutcome: { outcome: "terminal" } })`; assert `processKeywordMessage` rejects with `error?.code === "PIPELINE_INPUT_CONFLICT"`; assert `countOp(h.trace,"markAmbiguous") === 0`, `countOp(h.trace,"sendCheck") === 0`, `countOp(h.trace,"http") === 0`.
   - W02: same with `state:"failed", safeErrorCode: KEYWORD_PROVIDER_AUTH_FAILED, terminalizeOutcome: "terminal"`; assert the same rejection and `countOp(h.trace,"terminalize") === 0`, `countOp(h.trace,"sendCheck") === 0`.
   - W03: same with `state:"failed", safeErrorCode: KEYWORD_PROVIDER_RETRYABLE, scheduleRetryOutcome: { outcome: "delayed", retryAt: new Date(COMPONENT_T0.getTime()+4000) }`; assert the same rejection and `countOp(h.trace,"scheduleRetry") === 0`, `countOp(h.trace,"sendTask") === 0`.
   Runner tail: sorted set equality + count equality vs the three manifest IDs (I-F6).
5. **New `SCN-KI-034` worker runner:** `test("SCN-KI-034: worker oracle falsification controls mutate only captured evidence", async (t) => {...})` executing `R4-W04-…falsifies` and `R4-W05-…falsifies` per I-F8:
   - W04: run the existing `R3-T03-success-lost-no-check` scaffold body unchanged (passing); `const mutatedTrace = [...h.trace, "sendCheck"]`; `assert.throws(() => assertNoOp(mutatedTrace, "sendCheck"), (e) => e instanceof assert.AssertionError)`; rerun the production path unchanged and require pass.
   - W05: run the existing `R3-R03-success-lost-no-check` scaffold body unchanged; `const mutatedTrace = [...h.trace, "terminalize", "sendCheck"]`; `assert.throws(() => assertNoOp(mutatedTrace, "terminalize"), (e) => e instanceof assert.AssertionError)` and the same for `assertNoOp(mutatedTrace, "sendCheck")`; rerun production unchanged and require pass.
   Runner tail: set/count equality vs the two manifest IDs.
6. **T4 single-schema restructure (KI-R4-T4):** change `SCN-KI-030` (line 1358) to
   `test("SCN-KI-030: task_database enforcement manifest executes every durable case exactly once", { skip: !enabled }, async (t) => { const executed = []; await withIsolatedDb("kir4_scn030", async ({ db, repo }) => { for (const caseId of DATABASE_IDS) { await t.test(caseId, async () => { await t_scn030(caseId, executed, { db, repo }); }); } }); const sortedExecuted = [...executed].sort(); ... });`
   — signature takes `t`; one `withIsolatedDb("kir4_scn030", ...)` call wraps all
   five registrations; `t_scn030(caseId, executed, { db, repo })` consumes the
   shared context and performs no schema create/drop; every D01–D05 assertion
   body is preserved verbatim, with case-local business-row cleanup inside the
   schema where the cases previously relied on schema disposal; the old
   `kir3_d_*` inner schema names and the comment at line 1361 are removed; the
   final digest assertion becomes F-D1 literal
   `9e8a3973d5430be70e26f68bb235b831b96f17162d30277a40b06942cc94e934`.
   `withIsolatedDb` itself (line 270) is not modified; the outer helper's
   disconnect/drop/absence proof remains the sole isolation authority.
7. Nothing else in the file changes; no existing assertion, helper
   (`memoryS3`, `memoryDispatcher`, `runtimeFor`, `withIsolatedDb`,
   `r3FailOnAssertMonitorFactory`, `componentHarness`), or R3 case body is
   weakened or deleted except the two fixture/digest lines explicitly replaced
   above and the SCN-KI-030 restructure.

**Exact checks:** LOCAL_NOW — C1 `node --check`; C2
`node --test --test-isolation=none --test-name-pattern='SCN-KI-029|SCN-KI-033|SCN-KI-034' test/keyword-intelligence-worker.test.js`
(zero database env; SCN-KI-030 skip-guarded and not selected) all pass with zero
fail and only the env-guarded skip. DEFERRED_TO_INTEGRATION — the durable
D01–D05 oracles and one-schema lifecycle (owned by the V3 gate at I001).

**Completion checklist:** P1/P2/T1/V1/V2/V3 (registered=executed equality for the
five worker_component IDs)/H1 (include the deferred DB obligation)/H2/H3.

### 5.5 `KI-R4-S005` — adapter test: fixed digest + R4-A01 control

```yaml
subwindow_id: KI-R4-S005
type: FILE
parent_window_id: KI-R4
parent_assignment_id: ASG-KI-R4-WA-01
assigned_agent: UNASSIGNED
predecessors: [KI-R4-S003]
successor_reserved_for: WINDOW-AGENT
writable_file: email_scraper/test/keyword-intelligence-adapter.test.js
file_operation: MODIFY
starting_file_digest: f48d0d2d348a86e0128b9ba3ec034648286ce4f2c4d5c20c99ee88cbfa779764
starting_repository_change_set_digest: df17885e439b7ebf2d72282f80b3b684bebaec7a9486fc741c51be176f4600ae
read_only_scope: [email_scraper/src/aws-pipeline/keyword-intelligence/dataforseo-labs-adapter.js, email_scraper/test/fixtures/keyword-intelligence/ki-r4-enforcement-manifest-v1.json, KEYWORD_INTELLIGENCE_DECISION_LEDGER.md DEC-KI-032]
authorized_actions: [single_file_edit, node --check, focused adapter-test runs]
prohibited_actions: [adapter source edits, weakening existing A01–A16 assertions, every §1 prohibition]
may_start_successor: false
```

**Mechanical trace:** `KI-R4-T3`; R4-A01; `SCN-KI-034`; `DEC-KI-032` falsification controls.

**Exact file transformation (ordered):**
1. Replace the `SCN-KI-028` runner's final `assert.match(hash, /^[a-f0-9]{64}$/)`
   (line 722) with F-D1 literal equality
   `assert.equal(hash, "b4ede4c2a1a32fddc1a1ac67e023a81f93c6863632cdff2be421f20d51080e4f")`.
2. Load `R4_MANIFEST` per the file's existing import idiom.
3. Add `test("SCN-KI-034: adapter cost-output omission falsifies the unchanged oracle", async (t) => {...})`
   executing `R4_MANIFEST.groups.adapter_control` (`R4-A01-active-cost-output-omission-falsifies`)
   as a named subtest per I-F8: run the existing `R3-A01-active-terminal-success-cost`
   scaffold body unchanged (passing); capture `result`; `const mutated = { ...result }; delete mutated.providerCostUsd;`
   `assert.throws(() => assert.equal(mutated.providerCostUsd, supplied), (e) => e instanceof assert.AssertionError)`;
   rerun the production path unchanged and require pass. Runner tail: set/count
   equality vs the one manifest ID.

**Exact checks (LOCAL_NOW):** C1 `node --check`; C2
`node --test --test-isolation=none --test-name-pattern='SCN-KI-028|SCN-KI-034' test/keyword-intelligence-adapter.test.js`
— A01–A16 and the new control pass; V2 write-set proof.

**Completion checklist:** as in 5.1 with V3 = registered=executed equality for `adapter_control`.

### 5.6 `KI-R4-S006` — runtime-adapters test: fixed digest + R4-Q01/Q02

```yaml
subwindow_id: KI-R4-S006
type: FILE
parent_window_id: KI-R4
parent_assignment_id: ASG-KI-R4-WA-01
assigned_agent: UNASSIGNED
predecessors: [KI-R4-S002, KI-R4-S003]
successor_reserved_for: WINDOW-AGENT
writable_file: email_scraper/test/aws-pipeline-runtime-adapters.test.js
file_operation: MODIFY
starting_file_digest: 4be47e21bddab690017ff18887ef284d9ab6781d825b5998aaec04da2a34722f
starting_repository_change_set_digest: df17885e439b7ebf2d72282f80b3b684bebaec7a9486fc741be176f4600ae
read_only_scope: [email_scraper/src/aws-pipeline/adapters/queue-dispatcher.js, email_scraper/test/fixtures/keyword-intelligence/ki-r4-enforcement-manifest-v1.json, KEYWORD_INTELLIGENCE_DECISION_LEDGER.md DEC-KI-031/032]
authorized_actions: [single_file_edit, node --check, focused runtime-adapter runs]
prohibited_actions: [production edits, weakening existing Q01–Q12 assertions, every §1 prohibition]
may_start_successor: false
```

**Mechanical trace:** `KI-R4-T2` cases; R4-Q01/Q02; `SCN-KI-033`; `DEC-KI-032` own-key gate.

**Exact file transformation (ordered):**
1. Replace the dispatcher runner's final regex digest assertion (line 438) with
   F-D1 literal equality
   `assert.equal(hash, "962ad70760c71a6fcf08b73d5edf0cdccad27dea9c3414c552c1d8e3e2b99226")`.
2. Load `R4_MANIFEST`.
3. Add `test("SCN-KI-033: dispatcher own-key partition rejects symbol and non-enumerable extras", async (t) => {...})`
   executing `R4_MANIFEST.groups.dispatcher` as named subtests with a counting
   mock SQS client (the file's existing dispatcher-case idiom):
   - `R4-Q01-symbol-extra-key-rejected`: `const symbolExtra = Symbol("extra"); const options = { delaySeconds: 5, [symbolExtra]: 1 };`
     assert `sendOne(queueUrl, message, schema, options)` rejects with
     `error?.code === "PIPELINE_MESSAGE_INVALID"` (or the file's existing
     rejection idiom for Q05–Q12) and `client.send` was called zero times.
   - `R4-Q02-nonenumerable-extra-key-rejected`: `const options = { delaySeconds: 5 }; Object.defineProperty(options, "extra", { value: 1, enumerable: false });`
     same rejection and zero sends.
   Runner tail: set/count equality vs the two manifest IDs.

**Exact checks (LOCAL_NOW):** C1 `node --check`; C2
`node --test --test-isolation=none --test-name-pattern='SCN-KI-028|SCN-KI-033' test/aws-pipeline-runtime-adapters.test.js`
— Q01–Q12 and both new cases pass; V2 write-set proof.

**Completion checklist:** as in 5.1 with V3 = registered=executed equality for `dispatcher`.

### 5.7 `KI-R4-S007` — worker-flow test: fixed digest + R4-G01 control

```yaml
subwindow_id: KI-R4-S007
type: FILE
parent_window_id: KI-R4
parent_assignment_id: ASG-KI-R4-WA-01
assigned_agent: UNASSIGNED
predecessors: [KI-R4-S003]
successor_reserved_for: WINDOW-AGENT
writable_file: email_scraper/test/keyword-intelligence-worker-flow.test.js
file_operation: MODIFY
starting_file_digest: 4fe1b890d3aa2b53001b4ea5da19bdf981b3780a2c2e24857a7e1184e6fe2856
starting_repository_change_set_digest: df17885e439b7ebf2d72282f80b3b684bebaec7a9486fc741be176f4600ae
read_only_scope: [email_scraper/src/aws-pipeline/keyword-intelligence/service.js, email_scraper/test/fixtures/keyword-intelligence/ki-r4-enforcement-manifest-v1.json, KEYWORD_INTELLIGENCE_DECISION_LEDGER.md DEC-KI-032]
authorized_actions: [single_file_edit, node --check, focused worker-flow runs]
prohibited_actions: [production edits, weakening existing G-case assertions except the G24 replacement prescribed below, every §1 prohibition]
may_start_successor: false
```

**Mechanical trace:** `KI-R4-T3` aggregation_control; R4-G01; `SCN-KI-034`; `DEC-KI-032`.

**Exact file transformation (ordered):**
1. Replace the `SCN-KI-031` runner's final regex digest assertion (line 994) with
   F-D1 literal equality
   `assert.equal(hash, "c017cd869b11a93e86070112ed626a3cd299e00a518ed3a568dd8f1331c27b14")`.
2. Load `R4_MANIFEST`.
3. Add `test("SCN-KI-034: aggregation post-loss operation injection falsifies the zero-later-call oracle", async (t) => {...})`
   executing `R4_MANIFEST.groups.aggregation_control`
   (`R4-G01-post-loss-operation-injection-falsifies`) as a named subtest per I-F8:
   run the existing `R3-G21-loss-during-get-no-later-call` scaffold body unchanged
   (passing); `const mutatedTrace = [...h.trace, "s3.put"];`
   `assert.throws(() => aggNoOp(mutatedTrace, "s3.put"), (e) => e instanceof assert.AssertionError)`;
   rerun the production path unchanged and require pass.
4. The existing `R3-G24-monitor-negative-control` case body (lines 959–971)
   remains in the R3 manifest set and continues to execute as the R3 oracle; its
   input-altering mutation no longer carries the falsification claim, which now
   lives solely in R4-G01 per `DEC-KI-032` (the R3 manifest is byte-identical, so
   the G24 ID and body stay; no R3 assertion is weakened).

**Exact checks (LOCAL_NOW):** C1 `node --check`; C2
`node --test --test-isolation=none --test-name-pattern='SCN-KI-031|SCN-KI-034' test/keyword-intelligence-worker-flow.test.js`
— G01–G24 and the new control pass; V2 write-set proof.

**Completion checklist:** as in 5.1 with V3 = registered=executed equality for `aggregation_control`.

### 5.8 `KI-R4-S008` — enforcement test: fixed-revision conformance + R4 conformance

```yaml
subwindow_id: KI-R4-S008
type: FILE
parent_window_id: KI-R4
parent_assignment_id: ASG-KI-R4-WA-01
assigned_agent: UNASSIGNED
predecessors: [KI-R4-S003]
successor_reserved_for: WINDOW-AGENT
writable_file: email_scraper/test/keyword-intelligence-enforcement.test.js
file_operation: MODIFY
starting_file_digest: 2d8f8cb5cd8c731052c112f1e979a60d09cf04230fff97252e7a4b8a1d795172
starting_repository_change_set_digest: df17885e439b7ebf2d72282f80b3b684bebaec7a9486fc741be176f4600ae
read_only_scope: [email_scraper/test/fixtures/keyword-intelligence/ki-r3-enforcement-manifest-v1.json, email_scraper/test/fixtures/keyword-intelligence/ki-r4-enforcement-manifest-v1.json, email_scraper/test/keyword-intelligence-adapter.test.js, email_scraper/test/aws-pipeline-runtime-adapters.test.js, email_scraper/test/keyword-intelligence-worker.test.js, email_scraper/test/keyword-intelligence-worker-flow.test.js, KEYWORD_INTELLIGENCE_DECISION_LEDGER.md DEC-KI-032]
authorized_actions: [single_file_edit, node --check, focused enforcement runs]
prohibited_actions: [live git status or revision-less git diff usage, weakening any R3-C oracle except the C05/C06/C07 body corrections prescribed below, every §1 prohibition]
may_start_successor: false
```

**Mechanical trace:** `KI-R4-T3` conformance; R4-C01–C06; `SCN-KI-035`;
corrected `SCN-KI-032`; `DEC-KI-032` commit-stable conformance.

**Exact file transformation (ordered):**
1. Add `const R4_MANIFEST = JSON.parse(readFileSync(\`${fixtureDir}/ki-r4-enforcement-manifest-v1.json\`, "utf8"));`
   and `const R3_BASE = "37a0e0203d265f539b566f1536642cd2f4eb2d99"; const R3_HEAD = "077213cc7c33fa8209a1e5d8ff365b73766500dc";`
2. `gitDiffHunks(path)` (line 110): change the spawned command to
   `["diff", "-U0", R3_BASE, R3_HEAD, "--", path]`. No other change to the parser.
3. `R3-C05-production-symbol-diff-exact` body: before span checks, require
   `hunks.length > 0` for each of the three production files (adapter, dispatcher,
   service); keep the existing span constants and helper-inventory assertions
   unchanged (they now evaluate against the fixed diff).
4. `R3-C06-write-file-set-exact` body: replace the live `git status --porcelain`
   block (lines 208–212) with `git diff --name-only R3_BASE R3_HEAD` output
   compared to `AUTHORIZED_WRITE_PATHS` (the same nine literal paths), keeping
   sorted deep equality.
5. `R3-C07-prohibited-import-set-empty` body: replace the revision-less
   `git diff` (line 217) with `git diff --no-color R3_BASE R3_HEAD`; keep the
   nonempty-added-imports requirement and the prohibited-import regex; keep the
   new-file source scan extended to also scan this file and the R4 fixture for
   prohibited imports (JSON fixture trivially has none).
6. Add `test("SCN-KI-035: commit-stable R4 manifest and fixed-revision conformance", async (t) => {...})`:
   preamble asserts R4 manifest root keys exactly `["contractVersion","groups"]`,
   `contractVersion === "ki-r4-enforcement-manifest-v1"`, the five group names,
   per-group counts `1/2/5/1/6`, 15 total unique IDs, and the F-D2 global digest
   `6adc8ab132496c58608734549fbbc596577e1bd71c1e730349575eb96badc941`; then
   executes `R4_MANIFEST.groups.conformance` as named subtests:
   - `R4-C01-fixed-revision-diff-nonempty`: `git diff -U0 R3_BASE R3_HEAD -- <each of the three R3 production files>` yields at least one hunk each.
   - `R4-C02-fixed-revision-file-set-exact`: `git diff --name-only R3_BASE R3_HEAD` equals the nine literal R3 paths.
   - `R4-C03-fixed-revision-import-set-clean`: added imports in that fixed diff contain no `/sqlite|python|subprocess|python-shell|node:worker/u` match.
   - `R4-C04-r3-group-digests-exact`: recompute F-D1 for all seven R3 manifest groups and compare to the seven I-F4 literals.
   - `R4-C05-r3-global-digest-exact`: recompute F-D1 over the 101 R3 IDs and compare to `70bd758e68cb32aff7dc418356d68e3ca07dadf282f76e7484858a7ec0c9470b`.
   - `R4-C06-live-worktree-independent`: read this file's own source and the four other R4-runner test files' sources and require neither `["status"` nor a revision-less `["diff"` spawn argument appears (the only permitted `diff` spawns carry both `R3_BASE` and `R3_HEAD`); additionally assert the suite makes no assertion on live worktree state.
   Runner tail: set/count equality vs the six manifest IDs.

**Exact checks (LOCAL_NOW):** C1 `node --check`; C2
`node --test --test-isolation=none --test-name-pattern='SCN-KI-032|SCN-KI-035' test/keyword-intelligence-enforcement.test.js`
— C01–C08 (corrected bodies) and the six R4 conformance cases pass; V2 write-set proof.

**Completion checklist:** as in 5.1 with V3 = registered=executed equality for `conformance`.

## 6. Integration assessment `KI-R4-I001` (window agent; zero implementation writes)

```yaml
integration_assessment_id: KI-R4-I001
type: INTEGRATION_ASSESSMENT
assigned_agent: WINDOW-AGENT
authorized_write_file: NONE
preconditions: [S001..S008 individually accepted by the window agent]
```

**Gates (frozen; each runs exactly once after the last leaf edit, per `DEC-KI-032` verification economy):**

| Gate | Exact command (from `email_scraper/`) | Required outcome |
|---|---|---|
| G-V2 | `node --test --test-isolation=none --test-name-pattern='SCN-KI-028|SCN-KI-029|SCN-KI-031|SCN-KI-032|SCN-KI-033|SCN-KI-034|SCN-KI-035' test/keyword-intelligence-adapter.test.js test/aws-pipeline-runtime-adapters.test.js test/keyword-intelligence-worker.test.js test/keyword-intelligence-worker-flow.test.js test/keyword-intelligence-enforcement.test.js` | all selected top-level tests and named subtests pass, zero skip; 96 non-DB R3 IDs + 15 R4 IDs executed exactly once; four R4 mutation controls each capture `AssertionError`; all fixed F-D1/F-D2 digests equal |
| G-V3 | `ALLOW_DATABASE_TESTS=true node --test --test-isolation=none --test-name-pattern='SCN-KI-030' test/keyword-intelligence-worker.test.js` with an isolated non-production `TEST_DATABASE_URL` | D01–D05 appear as five named subtests, each executes once, zero skip; exactly one schema setup/cleanup (`kir4_scn030`); all durable oracles and the F-D1 task_database digest pass; exact-name absence after drop |
| G-V4 | `node scripts/build-keyword-worker.js` twice; then `node --test --test-isolation=none test/aws-pipeline-packaging.test.js` once | identical keyword ZIP hashes, one AL2023 engine, no forbidden/stale member, ZIP ≤45MiB, unzipped ≤200MiB, cold import exports `handler`, sibling build hashes unchanged, packaging test passes |
| G-V5 | `npm test` once; `npm run check:secrets` once | full suite green (documented sandbox `listen EPERM` handled by identical rerun with approval, both outcomes recorded); secret scan clean |
| G-V6 | Window-agent recomputation | cumulative required set = 101 R3 + 15 R4 = 116 unique IDs; required = registered = executed; zero skipped/duplicate/unexpected/unactivated IDs; four expected/falsified controls; no unresolved substitute-fidelity claim; assembled changed-file set equals the eight planned paths with set digest `ccfa1089d1d62656afde3927cd0b42128856713442dcbda5d30dd47a6b5333f6` |
| G-V7 | Read-only scope sweep | `git -C email_scraper diff --name-only` == exactly the eight paths; read-only paths byte-identical to §2 digests; no `kir4%` schema remains; root relocation state preserved; no provider/AWS/production/Prisma/seven-handler/commit/push action; no direct parent-leaf communication |

**Oracles:** `PASS` only when G-V2..G-V7 all hold and every leaf was
independently accepted. `CORRECTION_REQUIRED` when any gate fails — the window
agent records the failure per §9.5 and appends one-file corrective sub-windows.
`PARENT_BLOCKED` when the remedy needs a missing parent decision or expanded
scope. Gate invalidation after any correction: rerun every gate whose named
inputs changed, plus the mandatory scope/case/secret/regression closure
(G-V5/G-V6/G-V7); the database gate G-V3 reruns only if its source, harness,
schema lifecycle, or asserted production path changed after its successful run.
Costly-gate reuse requires the deterministic dependency proof recorded in S3.

**Mandatory integration checklist (§9.4):**

- [ ] I1 All listed file sub-windows independently accepted (S001–S008 dispositions recorded).
- [ ] I2 Actual assembled changed files equal the eight planned paths; planned set within parent scope; set digest `ccfa1089…`.
- [ ] I3 Requirement → decision → file → sub-window → assertion trace complete (§8 table).
- [ ] I4 G-V2/G-V3/G-V4 executed with activation witnesses recorded in S3.
- [ ] I5 Required = registered = executed coverage sets; 116 unique IDs; per-formula digests match; zero skips/duplicates/unexpected.
- [ ] I6 Four R4 mutation controls falsified as prescribed; negative-control failures recorded.
- [ ] I7 Substitute fidelity: component harnesses claim only component parity; accepted R3 tests untouched except the six prescribed digest-line replacements, fixture fingerprint fixes, and the SCN-KI-030 restructure.
- [ ] I8 No prohibited, successor, external, destructive, secret-bearing, or out-of-scope action (G-V7).
- [ ] I9 Window agent independently inspected current source and the complete diff, not leaf summaries.
- [ ] I10 `PASS`/`CORRECTION_REQUIRED`/`PARENT_BLOCKED` recorded with decisive evidence; on PASS append `WINDOW-AGENT-INTEGRATION-PASS` and hand off per §12.5 without touching A5/A6.

## 7. Correction and re-assessment rules

Append-only, per sub-window standard §10:
1. Never reuse any sub-window, assignment, or evidence ID; corrections are `KI-R4-C001+`.
2. A correction owns exactly one file, cites the failed evidence, root cause,
   governing parent decision, corrected prior sub-window, and invalidated
   evidence/gates, and carries a `CORRECTIVE-SUBWINDOW-READY` certificate before
   assignment.
3. A correction may not weaken an accepted oracle; if current code fails an
   oracle, the code is corrected, not the oracle.
4. Every corrective edit invalidates all evidence whose inputs or asserted path
   include that file; the next integration assessment reruns invalidated gates
   per §6 rules.
5. Same failure twice without a parent-decidable remedy = `PARENT_BLOCKED`, not
   a guess.
6. The window agent never edits an implementation file directly.

## 8. Traceability matrix

| Parent item | Sub-window(s) | Terminal assertion |
|---|---|---|
| `KI-R4-T1` identity fence | S001 (production), S004 (W01–W03 + fixtures) | `PIPELINE_INPUT_CONFLICT` with zero forbidden ops; equal-identity schedules unchanged |
| `KI-R4-T2` own-key gate | S002 (production), S006 (Q01–Q02) | symbol/non-enumerable extras throw with zero commands |
| `KI-R4-T3` manifest/digests/controls/conformance | S003, S005, S006, S007, S008 | fixed F-D1 literals; four I-F8 mutation `AssertionError` captures; R4 manifest structure + F-D2 global digest; fixed-revision Git gates |
| `KI-R4-T4` single-schema DB registration | S004 item 6 | five named subtests; one `kir4_scn030` schema; outer drop + absence |
| `SCN-KI-033` | S004, S006 | five partition cases; set equality |
| `SCN-KI-034` | S004, S005, S007 | four falsification controls; `AssertionError` captures |
| `SCN-KI-035` | S008 | six conformance cases + manifest preamble |
| Corrected `SCN-KI-028` | S005 | F-D1 adapter literal |
| Corrected `SCN-KI-029` | S004 | two per-group F-D1 literals + real-fingerprint fixtures |
| Corrected `SCN-KI-030` | S004 + G-V3 | single-schema five-subtest structure |
| Corrected `SCN-KI-031` | S007 | F-D1 aggregation literal |
| Corrected `SCN-KI-032` | S008 | fixed-revision C05/C06/C07 |
| `REQ-KI-002/005/021–024`, `INV-KI-002/004–009`, `DEC-KI-026–032` | allocated above per sub-window mechanical-trace fields | every ID terminates in a file anchor or executable assertion |
| Unmapped parent requirements/decisions/tasks/scenarios | none | §10 `SW-D01` certificate fields are all empty |

## 9. Mandatory decomposition-readiness checklist (44 items)

### 9.1 Authority and inheritance

- [x] `SW-A01` Parent assignment, window agent identity, and delegation authority are exact and current. Evidence: A5 state 98; `EV-KI-A-037`.
- [x] `SW-A02` Parent and sub-window standards plus contract, decision, checklist, and state revisions pinned and verified (§0.1; sub-window standard hash equals the KI-R4 header pin). Evidence: `EV-KI-R4-S01`.
- [x] `SW-A03` Parent write/read/action/prohibition/successor/stop boundaries copied without expansion (§1). Evidence: `EV-KI-R4-S01`.
- [x] `SW-A04` Current repositories, dirty state, and owner-controlled changes inventoried (§2). Evidence: `EV-KI-R4-S01`.
- [x] `SW-A05` All three subordinate artifacts exist with non-overlapping authorities. Evidence: `EV-KI-R4-S03`.
- [x] `SW-A06` Strict adjacent communication and no subagent delegation enforced (§1 prohibitions; leaf §7.5 H2 boxes). Evidence: `EV-KI-R4-S03`.

### 9.2 Decision and file-set closure

- [x] `SW-D01` Every parent requirement, invariant, decision, task, scenario, and coverage case allocated to exact files and assertions (§8). Evidence: `EV-KI-R4-S03`.
- [x] `SW-D02` No missing parent-level decision or contradictory authority remains (DEC-KI-026–032 complete; digest-formula ambiguity resolved mechanically in I-F4/I-F5). Evidence: `EV-KI-R4-S02`.
- [x] `SW-D03` Required changed-file set equals planned initial file set (eight paths; digest `ccfa1089…` verified). Evidence: `EV-KI-R4-S01`.
- [x] `SW-D04` Every planned file has one initial sub-window; none owns more than one file (§5.1–5.8). Evidence: `EV-KI-R4-S03`.
- [x] `SW-D05` Every file operation, starting digest, anchor, interface, preserved behavior, and forbidden edit is exact (§2, §3, §5). Evidence: `EV-KI-R4-S02`.
- [x] `SW-D06` Dependency graph complete, sequential, acyclic, justified by named outputs (§4). Evidence: `EV-KI-R4-S03`.
- [x] `SW-D07` Every cross-file interface frozen before dependent execution (§3 I-F1–I-F9). Evidence: `EV-KI-R4-S02`.
- [x] `SW-D08` Every intermediate state has exact permitted checks, expected failures, safety, resolver, prohibitions (§4.1). Evidence: `EV-KI-R4-S02` (IS-1 verified against fixture source).
- [x] `SW-D09` Separate production/test/fixture files have separate sub-windows (S001–S008). Evidence: `EV-KI-R4-S03`.
- [x] `SW-D10` No rename, multi-output generator, formatter, installer, or command can violate the one-file invariant (leaf commands are `node --check`, focused `node --test`, `JSON.parse`, sha256, fixed-revision read-only `git diff`; none writes workspace files). Evidence: `EV-KI-R4-S03`.

### 9.3 Sub-window execution completeness

- [x] `SW-E01` Every file sub-window contains every §7 field (§5.1–5.8). Evidence: `EV-KI-R4-S03` lint.
- [x] `SW-E02` Every sub-window prescribes exact ordered edits, not alternatives or broad verbs. Evidence: `EV-KI-R4-S03` lint (banned-verb scan).
- [x] `SW-E03` Every sub-window has exact preflight, local checks, activation witnesses, assertions, forbidden outcomes. Evidence: `EV-KI-R4-S03` lint.
- [x] `SW-E04` Every sub-window mechanically proves its attributable changed-file set is exactly one file (P2/V2 digest comparisons in every leaf). Evidence: `EV-KI-R4-S03`.
- [x] `SW-E05` Every sub-window has exact evidence, handoff, stop, and successor-reservation rules (§7.5 boxes, §12.3 certificate). Evidence: `EV-KI-R4-S03`.
- [x] `SW-E06` Each subagent reports only to the window agent and cannot update authority artifacts (§1; leaf prohibited actions). Evidence: `EV-KI-R4-S03`.
- [x] `SW-E07` No sub-window requires successor work to satisfy its file-local acceptance (each leaf's LOCAL_NOW set is self-contained; DB deferral is integration-owned, not leaf-owned). Evidence: `EV-KI-R4-S03`.
- [x] `SW-E08` Deliberately deferred checks name the exact integration assessment owning them (S004 → G-V3; S001 C3 → S004/I001). Evidence: `EV-KI-R4-S03`.

### 9.4 Enforcement and integration closure

- [x] `SW-V01` Coverage cases allocated to exact test files, registrations, activation witnesses, assertions (§5, §8). Evidence: `EV-KI-R4-S03`.
- [x] `SW-V02` Required local and whole-window case-set equality and digest checks prescribed (I-F4–I-F7; G-V2/G-V6). Evidence: `EV-KI-R4-S02`.
- [x] `SW-V03` Every critical invariant has a negative control at the narrowest effective level (four R4 mutation controls replace the defective R3 controls; R3 negative-control oracles preserved). Evidence: `EV-KI-R4-S02`.
- [x] `SW-V04` Test substitutes and accepted tests/fixtures have exact fidelity and invalidation rules (I-F8; §6 I7; §7 rule 3). Evidence: `EV-KI-R4-S03`.
- [x] `SW-V05` Initial integration assessment fully authored with zero implementation-file write authority (§6). Evidence: `EV-KI-R4-S03`.
- [x] `SW-V06` Frozen gates exact, risk-proportionate, scheduled at final assessment (§6 gates; database/build run once). Evidence: `EV-KI-R4-S03`.
- [x] `SW-V07` Correction diagnosis, one-file corrective assignment, invalidation, and reassessment rules complete (§7). Evidence: `EV-KI-R4-S03`.
- [x] `SW-V08` Window agent independently inspects every file handoff and personally executes every integration assessment (§6 preconditions; §8 disposition rules). Evidence: `EV-KI-R4-S03`.
- [x] `SW-V09` Whole-window approval cannot pass through zero-work, skipped, filtered, duplicate, unexpected, unactivated, or summary-only evidence (G-V6 counts/digests; §6 oracles). Evidence: `EV-KI-R4-S03`.
- [x] `SW-V10` Parent handoff contents and `READY_FOR_PARENT_REVIEW` boundary exact (§10.2). Evidence: `EV-KI-R4-S03`.

### 9.5 Mechanical and adversarial audit

- [x] `SW-R01` All IDs unique; all references resolve (lint: 8 sub-window IDs, 1 assessment ID, 8 file IDs, distinct manifest IDs 15+101). Evidence: `EV-KI-R4-S03` lint.
- [x] `SW-R02` No unresolved placeholder in a checked item or assignable sub-window. Evidence: `EV-KI-R4-S03` lint.
- [x] `SW-R03` Single-file write-set lint rejects zero/two/wildcard/directory/rename/incidental outputs (each `writable_file` is one canonical relative path; commands enumerated in SW-D10). Evidence: `EV-KI-R4-S03` lint.
- [x] `SW-R04` Removing one required file or requirement-to-file mapping makes readiness fail (G-V6 set-digest equality; §8 matrix rows map 1:1 to leaves). Evidence: `EV-KI-R4-S03`.
- [x] `SW-R05` Removing/duplicating/skipping/filtering/bypassing one required coverage case makes acceptance fail (runner set-equality + fixed digests + G-V6). Evidence: `EV-KI-R4-S03`.
- [x] `SW-R06` Weakening an oracle or diverging a substitute invalidates acceptance evidence (F-D1 literals are byte-exact; I-F8 forbids input substitution; §7 rule 3). Evidence: `EV-KI-R4-S02`.
- [x] `SW-R07` Simulated second-file edit and direct parent communication rejected (leaf V2 write-set proof; §12.3 certificate fields `attributable_changed_file_set`, `direct_parent_communication`). Evidence: `EV-KI-R4-S03`.
- [x] `SW-R08` Simulated integration failure cannot be repaired by the window agent without a new corrective sub-window (§7 rule 6). Evidence: `EV-KI-R4-S03`.
- [x] `SW-R09` Parent decomposition review is recorded before assignment of any remaining implementation leaf. Evidence: `EV-KI-R4-S04`.
- [x] `SW-R10` Document lint reports zero missing fields, mappings, cases, evidence references, or authority conflicts. Evidence: `EV-KI-R4-S03` lint.

## 10. Handoff templates and boundary

- Leaf execution certificate: sub-window standard §12.3, returned to the window
  agent with `status: AWAITING_WINDOW_REVIEW`; window agent appends a separate
  review disposition (`ACCEPTED_FOR_INTEGRATION` / `CORRECTION_REQUIRED` /
  `PARENT_BLOCKED`).
- Corrective readiness certificate: §12.2 before any corrective assignment.
- Integration certificate: §12.4 appended to S3 only on a PASS assessment.
- Consolidated parent handoff: §12.5 contents only; `READY_FOR_PARENT_REVIEW`
  is the terminal status of this window agent's authority. The window agent does
  not edit A5/A6, does not claim parent acceptance, and does not begin KI-W4.

## 11. Append-only amendments

Corrections are appended below as `KI-R4-C###` blocks with their §12.2
certificates; the blocks in §5 are immutable once decomposition review passes.

(No amendments yet.)

### Amendment `KI-R4-A1` — pre-S008 local-check scope, W05 oracle precision, bootstrap disposition

Recorded by the window agent before leaf execution; corrects decomposition
details without rewriting any §5 block:

1. S001/S002/S005–S007 LOCAL_NOW patterns exclude
   `test/keyword-intelligence-enforcement.test.js` until S008 lands: its live
   `git status`/revision-less `git diff` oracles (R3-C06/C07) fail on any
   partial worktree. That dependency is exactly `EV-KI-R4-S02` finding 3 and is
   repaired by S008; the final G-V2 gate proves the assembled state. These are
   the named expected temporary failures of IS-6's precursor, not regressions.
2. KI-R4-S004 `R4-W05` mutation oracles are R3-R03's two actual oracles
   (`assert.equal(countOp(trace,"terminalize"),1)` and
   `assertNoOp(trace,"sendCheck")`); appending `terminalize,sendCheck` must make
   both throw `AssertionError` while both pass on the unmutated capture (the
   R03 trace legitimately contains exactly one `terminalize`).
3. The exact manifest already present at the I-F3 hash is accepted as completed
   `KI-R4-S003` bootstrap work. Every remaining leaf is assigned to a separate
   implementation agent; `KI-R4-WINDOW-AGENT` only assigns and reviews those
   leaves and performs `KI-R4-I001`.
