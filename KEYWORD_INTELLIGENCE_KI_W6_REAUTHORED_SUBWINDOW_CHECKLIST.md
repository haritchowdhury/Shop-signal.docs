# KI-W6 Reauthored Sub-Window Decomposition Checklist (`S1`)

**Decomposition ID:** `KI-W6-REAUTHORED-DECOMP-6` (supersedes the unapproved
`KI-W6-REAUTHORED-DECOMP-1` through `-5` drafts per `EV-KI-A-082` through
`EV-KI-A-086`; no leaf was ever assigned under any draft)
**Parent window:** `KI-W6` (A4 `KI-CL-20`, window block at
`KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md` §2 `KI-W6`)
**Parent assignment:** `ASG-KI-W6-WA-02` (A5 state 147;
`EV-KI-A-082`–`EV-KI-A-086`)
**Governing standard:** `PROJECT_AGNOSTIC_WINDOW_AGENT_SUBWINDOW_AUTHORING_STANDARD.md`
revision `84e7590e74589f308c70dc9b0b67f7e9da395fafb1e5786202ecd1ca15be56e9`

This is `S1`, the frozen sub-window decomposition checklist for `KI-W6`. It is
subordinate to the parent package (`A1`–`A8`) and cannot broaden it. The other
subordinate artifacts are `S2`
(`KEYWORD_INTELLIGENCE_KI_W6_REAUTHORED_SUBWINDOW_STATE.md`) and `S3`
(`KEYWORD_INTELLIGENCE_KI_W6_REAUTHORED_SUBWINDOW_EVIDENCE.md`).

The old `KEYWORD_INTELLIGENCE_KI_W6_SUBWINDOW_{CHECKLIST,STATE,EVIDENCE}.md`
package (assignment `ASG-KI-W6-WA-01`, state-108 decomposition) is immutable
invalidated history per `CHG-KI-056`. Nothing in this package reuses, cites,
edits, or baselines against its IDs, topology, case interpretations, or
certificates.

## 0. Inherited authority and revision pins

| Artifact | Path | Revision (sha256) |
|---|---|---|
| Parent standard | `PROJECT_AGNOSTIC_DECISION_COMPLETE_CHECKLIST_AUTHORING_STANDARD.md` | `cda352017e75c0d11f6797d9fbe108b4365508cd38b0e92365cfb523ede32848` |
| Sub-window standard | `PROJECT_AGNOSTIC_WINDOW_AGENT_SUBWINDOW_AUTHORING_STANDARD.md` | `84e7590e74589f308c70dc9b0b67f7e9da395fafb1e5786202ecd1ca15be56e9` |
| `A1` contract | `KEYWORD_INTELLIGENCE_PRODUCT_CONTRACT.md` | `8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c` |
| `A3` decision ledger | `KEYWORD_INTELLIGENCE_DECISION_LEDGER.md` | `ef4153677807c80dfa9a09c0ffe0ba5a5127681fe6706e17ff6cd48869fdbd31` |
| `A4` checklist (KI-CL-20) | `KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md` | `8fe18271bf368a283246d55807dcc4612e118c725e5aabeb6188962a7abf5f4e` |
| `A5` state (v147, fifth correction assignment) | `ACTIVE_EXECUTION_STATE.md` | `8954cf2e9414aab484735ffd67f094dce563219b4a431d3a4878dde786bbfcd7` |
| Parent correction authority | `EV-KI-A-082`–`EV-KI-A-086` in `KEYWORD_INTELLIGENCE_EXECUTION_EVIDENCE.md`; `CHG-KI-056`–`CHG-KI-059` | within A6/A7; findings `F1`–`F14` |
| Parent window | `KI-W6` in `A4` §2 | per `A4` revision above |

All pins were recomputed on disk this session and matched `A5` state 147 and
A4 `KI-CL-20` (`EV-KI-W6-R12`). Any later revision mismatch blocks new
sub-window assignment until a delta audit is recorded in `S3`.

### 0.1 Recorded mechanical interpretations and assignment history

Scope-relative mechanical decomposition matters under sub-window standard
§0.3. None delegates a decision to a leaf; each cites its governing parent
decision. Recorded for parent decomposition review.

1. **Fresh ID series.** The reauthored decomposition uses leaf IDs
   `KI-W6-S101`–`KI-W6-S105`, integration assessment `KI-W6-I101`, corrective
   series `KI-W6-C101+`, evidence IDs `EV-KI-W6-R01+`, and per-leaf assignment
   IDs `ASG-KI-W6-S101`–`ASG-KI-W6-S105`. The invalidated state-108 IDs
   (`KI-W6-S001`, `KI-W6-S002`, `KI-W6-I001`, `ASG-KI-W6-WA-01`,
   `EV-KI-W6-S01/02`) are never reused. Governing: `DEC-KI-038` "Recursive
   authority"; A4 `KI-W6` header paragraph.
2. **Leaf order equals A4 task order.** `S101`=T1, `S102`=T2, `S103`=T3,
   `S104`=T4, `S105`=T5. This is a valid topological order of the §3 DAG.
   Governing: A4 `KI-W6-T1`–`T5`.
3. **Manifest group keys.** The four manifest group keys are
   `navigation`, `flow`, `resilience`, `conformance` (counts `3/13/4/6`
   matching `W6-CONF-01`). Top-level key order is exactly
   `contractVersion`, `groups`, `groupDigests`, `globalDigest`,
   `negativeControls`; arrays are unique ascending-byte-order strings; file is
   two-space-indented JSON with one final LF. Governing: A4 `KI-W6-T4`
   items 5–6; `DEC-KI-038` "Executable case set".
4. **R5-FIN-01 supersession literals.** The hostile same-origin API
   `statusUrl` literal is `/api/runs/run_kiw5_hostile_status_witness0001`
   (distinct from the fixture run identity `run_kiw5_finalize_000000000001` and
   from the workspace route); the expected destination is derived in-file as
   `` `/runs/${encodeURIComponent(runHandoff.run.runId)}` `` via local symbols
   `hostileStatusPath` and `workspacePath` (both verified unused in the file).
   The literal `run_kiw5_hostile_status_witness0001` occurs exactly once (the
   `hostileStatusPath` declaration); the prescribed diff is exactly 8 inserted
   and 4 deleted lines. Governing: `DEC-KI-038` "Navigation choice"; A4
   `KI-W6-T2` items 5–6; `EV-KI-A-082` `F2`.
5. **Certificate and operation-count field names.** The `KI_W6_CERTIFICATE=`
   JSON field order is exactly the A4 T5 item 5 list; `operationCounts`
   sub-objects and field names are frozen in §4 `KI-W6-S105` step 8. The
   emission site is exactly one `console.log` line (§4 S105-C2; §5.1 V3
   single-line oracle). Governing: A4 `KI-W6-T5` item 5; `DEC-KI-038` "Frozen
   gates"; `EV-KI-A-082` `F5`.
6. **Transport choices in `S105`.** The manifest is read with
   `node:fs readFileSync` + strict `JSON.parse` resolved as
   `path.resolve(root, "../email_scraper/test/fixtures/keyword-intelligence/ki-w6-enforcement-manifest-v1.json")`
   (the e2e runs with `cwd` `frontend/`); the backend harness is imported via
   the explicit relative specifier
   `../../../email_scraper/test/helpers/keyword-intelligence-e2e-harness.js`.
   Governing: A4 `KI-W6-T5` item 6.
7. **Frontend `npm run check` coverage.** `frontend` eslint config has no
   ignore for `test/browser/**`, so `V2` lints all three `.mjs` browser/test
   files; `npm test` runs only `test/*.test.ts` and never executes browser
   files. Recorded so `S102`/`S105` leaves know `V2` is lint-relevant but not
   execution-relevant for their files. Governing: A4 `KI-W6-V2`.
8. **Entry-gate history and A5 reconciliation (`EV-KI-A-082` `F1`).** The
   first authoring pass treated the requester's session instruction as the
   assignment and checked `SW-A01` while A5 v142 still recorded
   `current_window:NONE` / `assigned_agent:UNASSIGNED` and prohibited
   decomposition. That claim was wrong: the requester instruction did not
   replace A5, the sole assignment authority. The pre-state-143 package was an
   unapproved draft; its entry-gate readiness claims and certificate are
   superseded by `EV-KI-W6-R04`/`EV-KI-W6-R05`, the DECOMP-2 package's
   claims by `EV-KI-W6-R06`/`EV-KI-W6-R07` after `EV-KI-A-083`, and the
   DECOMP-3 claims by `EV-KI-W6-R08`/`EV-KI-W6-R09` after `EV-KI-A-084`,
   the DECOMP-4 claims by `EV-KI-W6-R10`/`EV-KI-W6-R11` after
   `EV-KI-A-085`, and the DECOMP-5 claims by
   `EV-KI-W6-R12`/`EV-KI-W6-R13` after `EV-KI-A-086`.
   The operative assignment is **A5 state 147** (parent CAS 146→147 recorded
   in `EV-KI-A-086`; states 143/144 first recorded the
   `ASG-KI-W6-WA-02` / `KI-W6-WINDOW-AGENT` correction assignment in
   `EV-KI-A-082`/`EV-KI-A-083`):
   `ASG-KI-W6-WA-02` / `KI-W6-WINDOW-AGENT`, write scope limited to the three
   `REAUTHORED` coordination artifacts, actions limited to correcting findings
   (`F1`–`F5` under state 143; `F6`–`F9` under state 144; `F10`–`F12`
   under state 145; `F13` under state 146; `F14` strict predecessor-chain
   reconciliation under state 147) and returning
   `AWAITING_PARENT_DECOMPOSITION_REVIEW`; all
   implementation, leaf, gate, build, browser, and database work prohibited.
   This corrected package is authored under that state and asserts no
   implementation authority. `S2.decomposition_status` becomes `READY` only
   after the parent approves this corrected package; leaf dispatch remains
   prohibited until then.
9. **Dispatcher reality (`EV-KI-A-082` `F3`; `EV-KI-A-083` `F6` delivery
   model).** Production dispatches downstream work through
   `dispatcher.sendMany` at four call sites
   (`src/aws-pipeline/services/confirmed-query-dispatcher.js:43` discovery,
   `domain-aggregator.js:187` lead, `lead-aggregator.js:112` traffic,
   `services/recovery.js:39` recovery). The harness memory dispatcher
   therefore implements **both** `sendOne(queueUrl, message, schema)` and
   `sendMany(queueUrl, messages, schema)`, and `sendMany` expands into one
   individual pending delivery record per message with its own **monotonic
   harness delivery ID** (`deliveryId`, assigned from a single harness
   counter at enqueue time), preserving per-item messages without inventing
   an SQS `itemIds` batch message contract (each dispatched message body
   remains an individual schema-validated message). The drain model has **no
   body-derived deduplication**: `keyword.aggregate.check.v1` messages carry
   only `{contractVersion, type, researchId, generation, stage,
   stageInputFingerprint?}` (verified, `contracts.js:87-93`) — no task
   natural ID or input fingerprint — so body-dedupe would collapse required
   repeated aggregation checks and erase duplicate-delivery proof. The
   harness invokes the production handler exactly once for **every pending
   delivery record, including intentionally duplicated or reordered bodies**;
   production idempotency, not the harness, absorbs duplicates
   (`EV-KI-A-083` `F6`). It is a specification error to state that
   `sendMany` is never used; the earlier draft's statement to that effect is
   removed.
10. **Physical causal action order (`EV-KI-A-083` `F9`).** One physical
   causal sequence produces all durable state and provider work exactly once;
   the 26 manifest cases then assert against captured witnesses in manifest
   order without rerunning provider work. The frozen order is in §4
   `KI-W6-S105` step 12.
11. **Cleanup and schema-absence witness (`EV-KI-A-083` `F9`).** `close()`
   drops the disposable schema, verifies its absence **before** disconnecting
   Prisma, throws `HarnessCleanupError` on residual presence, and returns an
   exact positive absence witness; the e2e closes browser/server/auth
   resources, verifies schema removal, and deletes the temporary artifact
   root **before** the sole certificate emission and exit 0 (§4 S105
   step 13, `CLEANUP_ORDER`).
12. **A4 `KI-CL-20` literal provider/fault authority (`EV-KI-A-084`
   `F10`–`F12`).** The parent corrected its own W6 specification; S1 now
   takes the following from A4 `KI-CL-20` verbatim rather than from any
   earlier draft: `frontendEnv`'s fourth value
   `BACKEND_API_TOKEN:"kiw6-backend-token"` and the matching emitted-Next
   child allowlist (T3 item 5); the callable no-op `createLeadServer.logger`
   `() => {}` (T3 item 6); the literal 30+30 per-seed expansion strings, the
   `overviewResponse` formula anchor, the 300→200→default-100 aggregation
   witnesses, and the exact per-query Google item fields with
   production-probe-path acceptance (T3 item 6); and the six queue-specific
   duplicate/reorder fault IDs with their delivery-ID semantics and exact
   nonempty injection points (T3 item 10). Governing: A4 `KI-CL-20`;
   `CHG-KI-057`; `EV-KI-A-084`.
13. **Two backend restart points (`EV-KI-A-085` `F13`).** The same IF-2
   `restartBackend()` operation is invoked exactly twice by S105: restart A
   follows the nonempty keyword duplicate/reorder partition and precedes every
   expansion drain; restart B follows the post-handoff research-selection
   mutation and precedes reloading and deep-comparing the immutable Run and
   RunQuery projection. `W6-RES-02` owns restart A and `W6-FLOW-13` owns
   restart B. Governing: A4 `KI-CL-20` T3 item 10 and coverage matrix;
   `CHG-KI-058`; `EV-KI-A-085`.
14. **Strict predecessor chain (`EV-KI-A-086` `F14`).** Scheduling metadata
   equals the already-frozen sequential execution order: S101 has no
   predecessor; S102 names S101; S103 names S102; S104 names S103; S105 names
   S104; I101 retains all five accepted leaves. Semantic `depends_on_files`
   records remain interface facts and do not weaken this scheduling chain.
   Governing: A4 `authorized_actions` (`sequentially delegate`) and S1 §3;
   `CHG-KI-059`; `EV-KI-A-086`.

### 0.2 Execution-environment policy (inherited parent E8.1, copied)

Sandbox escalation is standing-authorized for already-authorized local
commands (local processes, localhost, headless Chrome, build output,
toolchains, isolated test services). A restricted attempt proven invalidated
solely by sandbox denial or execution-channel loss permits exactly one
identical escalated recovery by the same agent, only after read-only
postconditions prove no matching process, workspace mutation, external
mutation, paid operation, or usable acceptance result remains; the invalidated
attempt is preserved as diagnostic history and the recovery's final exit and
decisive output are retained. An observable assertion failure, nonzero
product/test result, partial success with material side effects, changed
input, implementation-caused resource exhaustion, or unexplained termination is
not a sandbox invalidation. Escalation never grants provider, paid, cloud,
production, secret-installation, destructive, deployment, commit, push, or
successor authority.

## 1. Parent-window scope and exclusions (copied unexpanded)

Source: A4 `KI-W6` header. This section is a copy, not a re-derivation.

- **Objective:** correct successful dashboard navigation to the real run
  workspace and prove one causal maximum local workflow from authenticated
  seeds through durable keyword research, saved selection, immutable
  Run/RunQuery handoff, query confirmation, 100 Google probes, and the
  1000-domain downstream lead-task boundary.
- **Delegable implementation write scope (exactly five paths, set digest
  `d28ae17864073639580d7650bb03c03474d5370a5034b632cf412e1e3cf3d0bb`):**
  1. `email_scraper/test/fixtures/keyword-intelligence/ki-w6-enforcement-manifest-v1.json`
  2. `email_scraper/test/helpers/keyword-intelligence-e2e-harness.js`
  3. `frontend/components/keyword-intelligence/research-dashboard.tsx`
  4. `frontend/test/browser/keyword-intelligence-dashboard.mjs`
  5. `frontend/test/browser/keyword-intelligence-e2e.mjs`
- **Shared file scope:** `research-dashboard.tsx` — only the two successful
  `router.push` expressions; `keyword-intelligence-dashboard.mjs` — only the
  `R5-FIN-01` handoff fixture/comment/navigation oracle; every other existing
  symbol/oracle is read-only.
- **Read-only scope:** every unlisted workspace path; all Prisma
  schema/migrations/packages; backend production source; frontend
  routes/auth/proxy/types/client/view-model/selection/run workspace; accepted
  W3/R4/R5 fixtures/tests/evidence; standalone `KeywordSearchVolume` repository.
- **Authorized actions (post-parent-approval, for the window):** author fresh
  parent-bounded S1/S2/S3; sequentially delegate exactly one listed
  implementation file per leaf; window-agent independent leaf review; local
  source/test edits inside one leaf file; file-local diagnostics; one final
  frontend `npm run check`; one final emitted local Next start and Chrome CDP
  run against one isolated migrated test schema; one final backend
  `npm test`; one final backend secret scan; read-only negative searches;
  captured-data negative controls; window-agent consolidated handoff.
- **Prohibited actions:** reuse/edit/cite state-108 KI-W6 decomposition as
  proof; multi-file leaf; leaf-to-parent communication; browser
  application-API response substitution or request short-circuit in
  `SCN-KI-018`; schema/migration/package/backend-production/route/auth/proxy/
  worker/adapter/infrastructure edits; full opted-in database suite; Prisma
  generate/validate; handler build; full W5 browser rerun; standalone-project
  edit/delete; provider calls; AWS operations; production database writes;
  destructive shared cleanup; commits/pushes; KI-W7 work.
- **Successor:** `KI-W7`, reserved for the parent. `may_start_successor:
  false`; `stop_after: KI-W6`.

## 2. Starting working-tree inventory (recorded without modification)

Recomputed this session under A5 state 147 and A4 `KI-CL-20`
(`EV-KI-W6-R12`; first recorded under state 143 in `EV-KI-W6-R04`, state 144
in `EV-KI-W6-R06`; five-path digests and both repository baselines are
unchanged in `KI-CL-20`):

- `email_scraper` @ `0083a42c5582aeb8d9d8998e8ce9e1cc1d52b43e` — `git status
  --porcelain` empty (clean).
- `frontend` @ `70fb5edfcfe092ca8d153bb025116b96cf1897b3` — clean.
- Coordination root: the requester committed the former 44-line dirty set in
  `72ad22a` (2026-08-20T21:06:43+05:30) and untracked the nested repositories
  in `03551f0` (2026-08-20T21:10:24+05:30); both are requester-owned actions
  recorded in `EV-KI-W6-R03`. Current coordination-root porcelain is exactly
  the three untracked `REAUTHORED` artifacts attributable to this window plus
  the four parent-owned modified authority files A4/A5/A6/A7; no other path is
  present (`EV-KI-W6-R12`).
- Starting file states (A4-pinned and verified):
  - `ki-w6-enforcement-manifest-v1.json` = `ABSENT`
  - `keyword-intelligence-e2e-harness.js` = `ABSENT`
  - `research-dashboard.tsx` =
    `19494a99a2be28683167908289176bf44ebb8d0bb1eb40f63cc6d1cd770c6337` (529 lines)
  - `keyword-intelligence-dashboard.mjs` =
    `d30bed66cdc77ff53438515345be01baf2e1ad90ea2b9b8c8ab71c47f339c398` (2220 lines)
  - `keyword-intelligence-e2e.mjs` = `ABSENT`
- Starting repository change set (both nested repositories, relative to their
  pinned HEADs): empty; digest of empty set
  `e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855`.
- Environment prerequisites verified read-only: Node `v24.14.1`; Chrome
  `146.0.7680.164` at `/usr/bin/google-chrome`; `next@16.2.12` installed in
  `frontend/node_modules`; backend `package.json` `"type": "module"`;
  `TEST_DATABASE_URL` set and resolving through
  `test/helpers/isolated-postgres.js::resolveDirectTestDatabaseUrl` with a
  database identity distinct from `DATABASE_URL` (direct, non-pooler host).
  No database connection or build occurred during decomposition or correction
  (the resolver is pure URL string logic).

## 3. Initial single-file dependency DAG

```text
KI-W6-S101  research-dashboard.tsx
  -> KI-W6-S102  keyword-intelligence-dashboard.mjs
  -> KI-W6-S103  keyword-intelligence-e2e-harness.js
  -> KI-W6-S104  ki-w6-enforcement-manifest-v1.json
  -> KI-W6-S105  keyword-intelligence-e2e.mjs
  -> KI-W6-I101  integration assessment (after all five accepted leaves;
                  WINDOW-AGENT; zero implementation writes)
```

Execution is strictly sequential in the order
`S101, S102, S103, S104, S105, I101`. Parallel sub-windows are prohibited.

### 3.1 File records

```yaml
file_id: F-001
path: frontend/components/keyword-intelligence/research-dashboard.tsx
operation: MODIFY
current_digest: 19494a99a2be28683167908289176bf44ebb8d0bb1eb40f63cc6d1cd770c6337
parent_requirement_ids: [REQ-KI-015, REQ-KI-016, REQ-KI-017]
parent_invariant_ids: [INV-KI-010, INV-KI-014, INV-KI-015]
parent_decision_ids: [DEC-KI-035, DEC-KI-038]
parent_task_ids: [KI-W6-T1]
source_research_ids: [SRC-KI-038]
owned_symbols_or_anchors: [handleFinalize success branch (line 266), handleRetryHandoff success branch (line 300)]
depends_on_files: []
consumed_interfaces: [RunHandoff via startKeywordResearchRun]
produced_interfaces: [IF-1 navigation expression contract]
coverage_case_ids: [W6-NAV-01, W6-NAV-02, W6-NAV-03]
reason_required: A4 KI-W6-T1 items 1-15; DEC-KI-038 "Navigation choice"
preserved_content: [every other line of the 529-line file byte-identical]
prohibited_changes: [imports, state, props, components, public types, helpers, fallbacks, route probes, conditionals]
```

```yaml
file_id: F-002
path: frontend/test/browser/keyword-intelligence-dashboard.mjs
operation: MODIFY
current_digest: d30bed66cdc77ff53438515345be01baf2e1ad90ea2b9b8c8ab71c47f339c398
parent_requirement_ids: [REQ-KI-015, REQ-KI-016, REQ-KI-017]
parent_decision_ids: [DEC-KI-037, DEC-KI-038]
parent_task_ids: [KI-W6-T2]
owned_symbols_or_anchors: [R5-FIN-01 scenario block lines 1769-1787 only]
depends_on_files: [F-001 (IF-1 frozen, not execution-dependent)]
consumed_interfaces: [IF-1]
produced_interfaces: []
coverage_case_ids: []   # registration set unchanged; no W6 registration added here
reason_required: A4 KI-W6-T2 items 1-15; supersession of the sole stale oracle
preserved_content: [all 25 other runScenario registrations and every byte outside the R5-FIN-01 block]
prohibited_changes: [any other R5/W5 case, registration, screenshot, certificate, fetch interception, presentation assertion, registry/case-set/output-path/helper/port/build/browser lifecycle changes]
```

```yaml
file_id: F-003
path: email_scraper/test/helpers/keyword-intelligence-e2e-harness.js
operation: CREATE
current_digest: ABSENT
parent_requirement_ids: [REQ-KI-001..013, REQ-KI-015..017, REQ-KI-019..024]
parent_invariant_ids: [INV-KI-001..009, INV-KI-011..015]
parent_decision_ids: [DEC-KI-001..024, DEC-KI-026..038]
parent_task_ids: [KI-W6-T3]
owned_symbols_or_anchors: [createKeywordIntelligenceE2eHarness (sole export)]
depends_on_files: []
consumed_interfaces: [isolated-postgres.js exports, createLeadServer, Prisma repositories, keyword worker/service exports, parseGoogleSearchResponse, validateResearchBackedConfirmedQueryRows, stableShopIdentity, shopIdForStableKey, runStoreId, accepted fixtures (exact list in S103 read_only_scope)]
produced_interfaces: [IF-2 harness export + returned frozen object + frontendEnv + trace/fault contracts]
coverage_case_ids: [W6-FLOW-01..13, W6-RES-01..04]   # activation-trace supplier; registration lives in F-005
reason_required: A4 KI-W6-T3 items 1-15
preserved_content: []
prohibited_changes: [production source edits, direct terminal-database fabrication, Python/SQLite/standalone-project imports, raw body/HTML/cookie/credential-bearing URL/contact-data logging, sendMany-never-used claims]
```

```yaml
file_id: F-004
path: email_scraper/test/fixtures/keyword-intelligence/ki-w6-enforcement-manifest-v1.json
operation: CREATE
current_digest: ABSENT
parent_requirement_ids: [all DEC-KI-038 requirements]
parent_decision_ids: [DEC-KI-038]
parent_task_ids: [KI-W6-T4]
owned_symbols_or_anchors: [whole file, literal content frozen in section 4 KI-W6-S104]
depends_on_files: []
consumed_interfaces: []
produced_interfaces: [IF-3 manifest schema + digests]
coverage_case_ids: []   # authority for required set; executed by F-005
reason_required: A4 KI-W6-T4 items 1-15
preserved_content: []
prohibited_changes: [wildcards, ranges, dynamic generation, extra keys, wrong digests/order]
```

```yaml
file_id: F-005
path: frontend/test/browser/keyword-intelligence-e2e.mjs
operation: CREATE
current_digest: ABSENT
parent_requirement_ids: [REQ-KI-001..024]   # incl. REQ-KI-014/018 (presentation/UX correctness asserted end-to-end here)
parent_invariant_ids: [INV-KI-001..015]
parent_exclusion_ids: [EXC-KI-001..008]
parent_authority_ids: [AUTH-KI-001..004, AUTH-KI-006..007]
parent_decision_ids: [DEC-KI-038]
parent_task_ids: [KI-W6-T5]
parent_scenario_ids: [SCN-KI-018]
owned_symbols_or_anchors: [whole file: CLI, registry, causal workflow, conformance engine, certificate]
depends_on_files: [F-001, F-003, F-004]
consumed_interfaces: [IF-1, IF-2, IF-3, /keywords and /runs/[runId] pages, installed Next docs patterns]
produced_interfaces: [IF-4 KI_W6_CERTIFICATE line]
coverage_case_ids: [W6-NAV-01..03, W6-FLOW-01..13, W6-RES-01..04, W6-CONF-01..06, W6-NC-01..13]
reason_required: A4 KI-W6-T5 items 1-15; authoritative coverage matrix
preserved_content: []
prohibited_changes: [browser API response substitution, screenshots/review files, second build, non-loopback binds, paid/cloud calls, KI-W7 work]
```

Required changed-file set (A4 header) = planned initial file set = files owned by
initial sub-windows = the five paths above; set digest
`d28ae17864073639580d7650bb03c03474d5370a5034b632cf412e1e3cf3d0bb`;
exactly one initial owner per path; the graph is acyclic.

**Assignment-time starting repository change-set digests** (per leaf; the
attributable set of W6-owned paths already changed by predecessor leaves;
sorted-member-plus-LF formula; both nested repositories combined; computed
under the clean pinned baselines in `EV-KI-W6-R04`, unchanged under states
144/145 in `EV-KI-W6-R06`/`R08`):

| Leaf | Starting changed set | Digest |
|---|---|---|
| `S101` | `{}` | `e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855` |
| `S102` | `{F-001}` | `d1349d2efaeb4f235fdc62a01f529a7c4c861e814964c4a12c05eba5f27f0be2` |
| `S103` | `{F-001, F-002}` | `fbfdac4a76ef0754ab3de904905a85b38b3777b2ad39926625f46ae4ae503954` |
| `S104` | `{F-001, F-002, F-003}` | `b94659a0de51b39e36e984c858ee4f0fa0effefaba27140ea29146fa947515e9` |
| `S105` | `{F-001, F-002, F-003, F-004}` | `dc48365f600adb2d36194745f5c6433ee34339626c03bf6f509245661ee2dbcc` |

At each dispatch the window agent verifies the actual repository status equals
the recorded starting set (any divergence stops dispatch for diagnosis).

### 3.2 Intermediate-state contract (per edge)

| After | Permitted local checks | Pending/expected temporary state | Safe because | Resolved by | Prohibited meanwhile |
|---|---|---|---|---|---|
| `S101` | grep/numstat counts only (no build) | Accepted `R5-FIN-01` oracle is latently stale (production now routes to `/runs/<runId>`; oracle still expects `/keywords/ki-r5-fin-nav-witness`) | No W6 gate runs the R5 browser suite; `npm run check` does not execute browser files; V2–V6 have not started | `S102` | Any R5/W5 browser rerun; any second frontend edit |
| `S102` | `node --check`, grep conformance | None (oracle aligned) | — | — | — |
| `S103` | `node --check`, structural greps | New helper exists but is imported by nothing; backend `npm test` does not match `test/helpers/*.js` | Helper is inert until imported | `S105` | Any backend production/package edit; DB connection during leaf |
| `S104` | strict JSON parse + digest recomputation scripts | Fixture exists, unconsumed | Inert data file | `S105` | Any manifest-driven test execution during leaf |
| `S105` | `node --check`, structural greps | Full assembly present; V1–V6 unexecuted | All frozen gates run only at `I101` | `I101` | Running V2/V3/V4 from a leaf; starting `I101` before window-agent review of all leaves |

Unexpected failures at any edge stop the sequence for diagnosis
(sub-window standard §6.1); "tests may fail until later" is not a license.

### 3.3 Interface freeze (before first dependent leaf)

#### IF-1 — navigation contract (producer F-001; consumers F-002, F-005)

The `RunHandoff` schema (`{run: RunStatus, statusUrl}` parsed by
`parseRunHandoffEnvelope`, exact keys `["run","statusUrl"]`), the API response,
and all state transitions are unchanged. Each of the two success branches calls
exactly ``router.push(`/runs/${encodeURIComponent(handoff.run.runId)}`)``. The
run ID is consumed exactly once per branch from `handoff.run.runId`; never
derived from research ID, `statusUrl`, pathname, or browser state. `statusUrl`
remains `/api/runs/<Run.id>` (backend `src/server.js:695`) and stays available
to non-browser API clients.

#### IF-2 — causal harness (producer F-003; consumer F-005)

**Sole export (exact signature):**

```js
export async function createKeywordIntelligenceE2eHarness({
  testDatabaseUrl = process.env.TEST_DATABASE_URL,
  testDirectDatabaseUrl = process.env.TEST_DIRECT_DATABASE_URL,
  productionDatabaseUrl = process.env.DATABASE_URL,
} = {})
```

**Returned frozen object (exact literal construction; the leaf writes this
exact `return` statement):**

```js
return Object.freeze({ frontendEnv, ownerId, otherOwnerId, trace, setAuthOwner, drainKeywordWork, restartBackend, drainDownstream, readDurableState, injectCapturedDefect, close });
```

**Member contracts (all frozen):**

1. `frontendEnv: Readonly<{ BACKEND_API_BASE_URL: string; BACKEND_API_TOKEN: string; NEON_AUTH_BASE_URL: string; NEON_AUTH_COOKIE_SECRET: string }>`
   — `BACKEND_API_BASE_URL` = `http://127.0.0.1:<backendPort>` and
   `NEON_AUTH_BASE_URL` = `http://127.0.0.1:<authPort>` where both ports are
   the actual `server.address().port` values of servers bound to `127.0.0.1:0`;
   `BACKEND_API_TOKEN` is the deterministic test-only literal
   `kiw6-backend-token` (the same literal the backend server config uses, so
   the frontend proxy's derived Authorization header is accepted —
   `EV-KI-A-084` `F10`); `NEON_AUTH_COOKIE_SECRET` is the deterministic
   test-only literal
   `kiw6-local-e2e-cookie-secret-0000000000000000000000` (51 characters).
   No secret value is logged or placed in a certificate.
2. `ownerId: "kiw6-owner-a"` and `otherOwnerId: "kiw6-owner-b"` (literal
   deterministic owner identities created through the actual repositories).
3. `trace(): TraceEvent[]` — returns a frozen copy of the accumulated
   privacy-safe typed event log. **Trace event union (discriminated by
   `kind`; no other fields are ever recorded):**

   ```ts
   type TraceEvent =
     | { kind: "http"; op: "request"; at: number; method: string; path: string; status: number }
     | { kind: "auth"; op: "get-session"; at: number; mode: "owner-a" | "owner-b" | "none"; status: 200 }
     | { kind: "dataforseo"; op: "request"; at: number; taskType: "expansion-suggestions" | "expansion-related" | "anchor-overview" | "market-overview"; attempt: number; costUsd: string; requestFingerprint: string }
     | { kind: "google"; op: "search-page"; at: number; runQueryId: string; occurrences: number }
     | { kind: "s3"; op: "put-immutable" | "get-validated" | "get-missing"; at: number; key: string; contentFingerprint: string; bytes: number }
     | { kind: "sqs"; op: "send-one" | "send-many"; at: number; count: number; messageTypes: string[] };
   ```

   `at` is the fixed-clock epoch milliseconds. Tuples never contain raw
   bodies, HTML, cookies, authorization headers, credential-bearing URLs, or
   contact data; identity is carried only by fingerprints, IDs, counts, and
   byte lengths.
4. `setAuthOwner(owner: "kiw6-owner-a" | "kiw6-owner-b" | null): void` —
   switches the loopback auth server's `GET /get-session` mode:
   owner modes return exactly `{user:{id:<owner>}}` with status 200; `null`
   returns JSON `null` with status 200.
5. `drainKeywordWork(stage: "expansion" | "anchor-screen" | "markets" | "settle"): Promise<KeywordStageReport>`
   — consumes pending keyword-queue **delivery records** (one production
   handler invocation per delivery, including duplicates/reorders; §0.1
   item 9) of exactly that stage, in `deliveryId` order, until the stage's
   stop condition: `"expansion"` consumes the initial
   `keyword.initialize.v1` delivery, every resulting
   `keyword.expansion.task.v1` delivery, and every
   `keyword.aggregate.check.v1` delivery the expansion tasks emit, then
   stops with the anchor `keyword.overview.task.v1` delivery queued and
   unconsumed (`EV-KI-A-083` `F6`); `"anchor-screen"` consumes the US
   anchor 300-candidate overview delivery and its aggregation checks, then
   stops with the first market overview delivery queued and unconsumed;
   `"markets"` consumes all remaining overview and aggregate-check
   deliveries until the keyword queue is empty; `"settle"` consumes every
   remaining keyword delivery. The exact task-input field names are read
   from the frozen message schema in
   `email_scraper/src/aws-pipeline/keyword-intelligence/contracts.js`
   (literals `keyword.initialize.v1`, `keyword.expansion.task.v1`,
   `keyword.overview.task.v1`, `keyword.aggregate.check.v1` at lines 14–17);
   the schema is the authority and introduces no choice. Returns
   `{ processedByType: Record<string, number>, providerCalls: number,
   providerAttempts: number, keywordObjects: number, keywordQueueSends: number }`
   computed from the trace and repository, never hardcoded.
6. `restartBackend(): Promise<void>` — closes the backend HTTP server,
   recreates the Prisma client, repositories, and `createLeadServer` with the
   identical injected dependencies and the same in-memory S3/SQS/clock
   instances, and listens on the same `127.0.0.1` port; resolves when
   listening; rejects if the same port cannot be rebound. The auth server,
   database schema, S3/SQS state, and clock are retained. S105 invokes this
   same method exactly twice: restart A at the pre-expansion point and restart
   B at the post-handoff-selection-mutation point frozen in §4 S105 step 12.
7. `drainDownstream(): Promise<{ processedByType: Record<string, number>, discoveryTasks: number, stableDomains: number, leadTasks: number }>`
   — processes pending downstream messages to completion of the domain-stage
   durable predicate via the drive table.
8. `readDurableState(): Promise<DurableStateSnapshot>` — exact schema, with
   `run` and `handoff` projected only from real Prisma fields
   (`prisma/schema.prisma` `model Run` at line 130 and `model
   KeywordResearchHandoff` at line 730; `Run.runIntentId` does not exist and
   must not be referenced — `EV-KI-A-083` `F7`):

   ```ts
   type DurableStateSnapshot = {
     research: { researchId: string; ownerId: string; state: string; selectionRevision: number; selectionFingerprint: string };
     keywordResult: { visible: boolean; rowCount: number; defaultSelectionItemCount: number };
     run: null | {
       runId: string;              // Run.id
       state: string;              // Run.state (RunState enum)
       phase: string;              // Run.phase (RunPhase enum)
       stage: string;              // Run.stage
       queryCount: number;         // Run.queries relation count
       confirmedQueryRevision: number | null;  // Run.confirmedQueryRevision
       queriesConfirmedAt: string | null;       // Run.queriesConfirmedAt (ISO)
       executionBackend: string;   // Run.executionBackend
       resultsAvailable: boolean   // Run.resultsAvailable
     };
     handoff: null | {
       handoffId: string;           // KeywordResearchHandoff.id
       clientRequestId: string;     // KeywordResearchHandoff.clientRequestId
       selectionRevision: number;   // KeywordResearchHandoff.selectionRevision
       selectionFingerprint: string; // KeywordResearchHandoff.selectionFingerprint
       createdAtIso: string         // KeywordResearchHandoff.createdAt (ISO)
     };
     discovery: { taskCount: number; terminalCount: number };
     domains: { stableHostCount: number; shopCount: number; runStoreCount: number; leadTaskCount: number; stageComplete: boolean };
     fixtures: null | {
       corruptArtifact: { calls: number; objects: number; terminalTasks: number; nextStageRows: number; rejected: boolean };
       missingTerminal: { calls: number; objects: number; terminalTasks: number; nextStageRows: number; notReady: boolean };
     };
   };
   ```

   The handoff state required by the W6 cases (`W6-NAV-02` same-client-key
   replay; `W6-FLOW-08` atomic handoff; `W6-FLOW-13` immutable snapshot) is
   proven by the `run` + `handoff` projection together: exactly one
   `KeywordResearchHandoff` row per `Run.id` (`runId @unique`) with the
   replay identity `@@unique([researchId, clientRequestId])`.

9. `injectCapturedDefect(faultId: FaultId): Promise<FaultOutcome>` — **fault
   union and outcomes (exact; six queue-specific delivery faults per A4
   `KI-CL-20` T3 item 10 plus the two captured-state faults):**

   ```ts
   type FaultId =
     | "duplicate-next-keyword-message"
     | "reorder-pending-keyword-messages"
     | "duplicate-next-discovery-message"
     | "reorder-pending-discovery-messages"
     | "duplicate-next-domain-check-message"
     | "reorder-pending-domain-check-messages"
     | "corrupt-stored-artifact"
     | "omit-neon-terminal";
   type FaultOutcome =
     | { faultId: "duplicate-next-keyword-message" | "duplicate-next-discovery-message" | "duplicate-next-domain-check-message"; deliveredType: string; deliveryId: number }
     | { faultId: "reorder-pending-keyword-messages" | "reorder-pending-discovery-messages" | "reorder-pending-domain-check-messages"; pendingCount: number }
     | { faultId: "corrupt-stored-artifact"; corruptedKey: string }
     | { faultId: "omit-neon-terminal"; omittedTaskNaturalId: string };
   ```

   Semantics: each `duplicate-next-<queue>-message` enqueues the named
   queue's next pending delivery a second time with identical body under a
   **fresh monotonic delivery ID without a dispatcher send trace** (the base
   dispatcher-send counts stay unchanged); each `reorder-pending-<queue>-messages`
   reverses the named queue's pending body order and reissues fresh
   increasing delivery IDs in that reversed order; `corrupt-stored-artifact`
   mutates the bytes of one stored memory-S3 object belonging to an
   already-terminal task before its next validated read (reports the key
   only); `omit-neon-terminal` suppresses the next task's Neon terminal write
   while leaving its S3 object present (reports the natural ID only).
   **Exact nonempty injection points (A4 `KI-CL-20` T3 item 10;
   `EV-KI-A-084` `F12`):** the keyword duplicate/reorder is invoked
   immediately after initialization has queued expansion tasks/checks, the
   backend restart A is then invoked (`restartBackend`), and only then is expansion
   drained; the discovery duplicate/reorder is invoked immediately after
   confirmation dispatches the 100 discovery deliveries; the domain-check
   duplicate/reorder is invoked after the first discovery emits a domain
   check, before completing the downstream drain. Every fault operates only
   on harness captured/test state before/after public calls and only on a
   nonempty queue (an empty named queue throws `HarnessPreflightError`);
   none edits production source, none fabricates a terminal database row
   directly.
10. `close(): Promise<{ droppedSchema: string; absenceWitness: { query: string; rowCount: 0 } }>`
    — in exact order: closes the backend and auth HTTP servers; drops the
    disposable schema `CASCADE`; **verifies the schema's absence before
    disconnecting Prisma** using the frozen literal
    `const SCHEMA_ABSENCE_QUERY = "SELECT schema_name FROM information_schema.schemata WHERE schema_name = $1";`
    with the schema name bound as the sole parameter; throws
    `HarnessCleanupError` (naming the residual schema) if the query returns
    any row; then disconnects Prisma; then resolves with
    `{ droppedSchema: <schema>, absenceWitness: { query: SCHEMA_ABSENCE_QUERY, rowCount: 0 } }`
    — the exact positive absence witness. Idempotent: a second call after a
    successful drop returns the memoized first result without reconnecting
    or error.

**Error names (exact):** the harness throws `HarnessPreflightError` for
invalid environment/URL preconditions (including a `TEST_DATABASE_URL` whose
database identity equals `DATABASE_URL`), `HarnessStallError` when a drain
loop exceeds its step ceiling (the error message lists pending message types
and a durable-state summary), and `HarnessCleanupError` when the disposable
schema survives the `close()` drop (the error names the residual schema).
Production typed errors from workers, services, parsers, and adapters
propagate unchanged; the harness never wraps or swallows them.

**Server, repository, and child-process configuration (exact literals;
`EV-KI-A-083` `F7`):**

- The harness **never calls `loadConfig()`** (it reads `.env` and ambient
  variables); it constructs the backend `config` object literally with
  exactly these keys and values (the only `config.*` members `src/server.js`
  touches): `{ port: 0, host: "127.0.0.1", backendApiToken:
  "kiw6-backend-token", runExecutionBackend: "aws",
  runRateLimitWindowMs: 60000, runRateLimitMax: 1000,
  queryConfirmRateLimitWindowMs: 60000, queryConfirmRateLimitMax: 1000,
  generatedQueryCount: 10, maxQueries: 20, maxShopTypes: 5 }`. `port: 0`
  is never used for listening (the harness binds the returned
  `http.Server` itself); no ambient provider or production configuration is
  read.
- `createLeadServer` options (exact frozen values beyond the injected
  pipelines/factories already listed): `now: () => new Date(nowBox.current)`,
  `schedule` = the FIFO queue callback, `leaseOwner: "kiw6-lease-owner"`,
  `leaseDurationMs: 90000`, `heartbeatIntervalMs: 20000`,
  `recoveryIntervalMs: 15000`, `setIntervalFn` and `clearIntervalFn` =
  harness-controlled record/discrete-tick functions that never auto-fire
  real timers, and `logger` = the callable no-op function `() => {}`
  (A4 `KI-CL-20` T3 item 6: the server invokes the logger as a function;
  never an object — `EV-KI-A-084` `F10`; defaults `src/server.js:92-93,188`).
- `PrismaRunRepository` is constructed as
  `new PrismaRunRepository(scopedPrismaClient, { runExecutionBackend: "aws",
  browserlessUrl: "https://fixture.example", googleSearchEngineId: "fixture",
  googleResultsPerQuery: 10, requestTimeoutMs: 10000, maxPagesPerStore: 5,
  pageFetchConcurrency: 2, maxQueries: 20, generatedQueryCount: 10,
  queryProbeFreshnessMs: 60000, queryProbeConcurrency: 1, minQueryResults: 1,
  minQueryUniqueHosts: 1, minQueryRelevantResults: 1,
  minQueryRelevanceRatio: 0.1, minQueryBaseScore: 1, browserlessEnabled:
  false, enableAiNormalization: false, dataForSeoEnrichmentEnabled: true,
  cruxEnrichmentEnabled: true, cruxBigQueryProjectId: "fixture-project" })`
  — the exact accepted `awsProviderConfigSnapshot` recipe
  (`test/aws-pipeline-end-to-end.integration.test.js:67-74`;
  `awsProviderConfigSnapshot` validation at
  `src/prisma-run-repository.js:595-625`).
- Child-process environment allowlist (exact): the spawned `next start`
  child receives **exactly** `{ PATH: process.env.PATH, HOME:
  process.env.HOME, NODE_ENV: "production", BACKEND_API_BASE_URL:
  <frontendEnv value>, BACKEND_API_TOKEN: <frontendEnv value>,
  NEON_AUTH_BASE_URL: <frontendEnv value>, NEON_AUTH_COOKIE_SECRET:
  <frontendEnv value> }` — the four `frontendEnv` values plus only `PATH`,
  `HOME`, `NODE_ENV` (A4 `KI-CL-20` T3 item 5) — and nothing else (no
  ambient provider/production variables); the spawned `next build` child
  receives exactly `{ PATH: process.env.PATH, HOME: process.env.HOME }`;
  Chrome is spawned with inherited environment and no env override (the
  accepted harness pattern).

**Runtime, queue, and config contract (exact literals):** the injected
pipeline runtime carries `config` with exactly these keys and values:
`awsPipelineBucket: "kiw6-bucket"`,
`awsPipelineKeywordResearchQueueUrl: "https://sqs.kiw6.local/keyword-research"`,
`awsPipelineDiscoveryQueueUrl: "https://sqs.kiw6.local/discovery"`,
`awsPipelineDomainAggregationQueueUrl: "https://sqs.kiw6.local/domain-aggregation"`,
`awsPipelineLeadQueueUrl: "https://sqs.kiw6.local/lead"`,
`awsPipelineLeadAggregationQueueUrl: "https://sqs.kiw6.local/lead-aggregation"`,
`awsPipelineTrafficQueueUrl: "https://sqs.kiw6.local/traffic"`,
`awsPipelineFinalAggregationQueueUrl: "https://sqs.kiw6.local/final-aggregation"`,
`awsPipelineRecoveryAgeMs: 1`;
`secrets` carries only the DataForSEO fixture credentials
`{ dataForSeoLogin: "kiw6-login", dataForSeoPassword: "kiw6-password" }`
(test-only literals; never logged). The in-memory S3 adapter honors
`IfNoneMatch: "*"` puts (412 `PreconditionFailed` on conflicting rewrite),
`GetObjectCommand` (including `NoSuchKey`), parses strict artifact schemas on
put and get, and rejects an unequal immutable replay with the same error
discriminator as production (`PIPELINE_ARTIFACT_CONFLICT`). The in-memory
dispatcher (§0.1 item 9) implements `sendOne` and `sendMany`, validates every
message body individually through the supplied schema, preserves one delivery
identity per message, supports the duplicate/reorder faults, and records one
`{kind:"sqs"}` trace event per send call. A module-level frozen literal
`const DISPATCHER_METHODS = ["sendMany", "sendOne"];` is asserted against the
created dispatcher at harness creation (creation throws if either method is
missing).

**Clock contract (exact):** one fixed UTC clock starting at
`2026-01-01T00:00:00.000Z` (`nowBox` pattern); the drain loop advances it by
exactly `2000` ms before each successive fresh keyword-provider claim so the
base maximum trace satisfies the durable throttle without a deferral;
replay/fault cases advance only to their persisted due/expiry timestamps. All
repository date arguments are pinned to this clock (withClock proxy pattern,
`test/helpers/aws-pipeline-e2e-harness.js:37-38`).

**Deterministic data contract (exact literals):** five seed keywords
`["insulated water bottle", "stainless lunch box", "silicone baking mat",
"glass storage jar", "reusable straw set"]`; 100 retained keywords/queries;
query IDs from the actual RunQuery creator; occurrence hosts generated by the
exact template
`` `w6-q${String(q).padStart(3, "0")}-r${String(r).padStart(2, "0")}.myshopify.com` ``
with `q` in 1..100 and `r` in 1..10; provider cost literals in a frozen
`const TASK_COSTS = { expansion: "0.01560000", anchor: "0.04800000", market: "0.03600000", total: "0.49200000" };`
(ten expansion calls at `0.01560000`, one 300-keyword anchor at `0.04800000`,
eight 200-keyword market calls at `0.03600000`, total `0.49200000`); the
disposable schema name is generated with the frozen literal prefix
`const SCHEMA_PREFIX = "kiw6_";` plus a unique lowercase suffix, validated by
`assertSafeDisposableSchema`.

**Literal provider synthesis (exact; A4 `KI-CL-20` T3 item 6;
`EV-KI-A-084` `F11`):** the harness defines exactly
`const pad2 = (n) => String(n).padStart(2, "0");` and
`const pad3 = (n) => String(n).padStart(3, "0");`. For zero-based seed index
`s` and one-based item index `i` = 1..30, suggestions return
`{keyword: \`${seed} suggestion s${s}${pad2(i)}\`}` and related returns
`{keyword_data: {keyword: \`${seed} related r${s}${pad2(i)}\`}, depth: 2,
related_keywords: []}` in ascending `i`. The accepted per-seed cap therefore
retains the seed, all 30 suggestions, and the first 29 related values —
producing exactly 300 distinct anchor inputs. Every overview item is produced
in input order by the exact `overviewResponse` field/month formula at
`test/keyword-intelligence-worker.test.js:93-122` (verified anchor:
`search_volume: 1000 + index * 10`, monthly
`800 + index * 5 + m` over 15 months, cost `0.012 + 0.00012 * keywords.length`
— `0.048` for 300 inputs and `0.036` for 200). Production aggregation must
witness 300 active anchor candidates, the deterministic first-200 shortlist,
and a 200-row final result with the default-100 selection.

**Google per-query expansion contract (exact; A4 `KI-CL-20` T3 item 6;
`EV-KI-A-084` `F11`):** the pinned raw fixture
`test/fixtures/providers/google/custom-search-v1-success.json` contains
exactly one item (verified: `kind: "customsearch#search"`, item keys
`title/link/snippet/displayLink`). For each **received** query the harness
`searchPage` deep-clones that fixture and replaces `items` with ten one-based
occurrences. With `queryProbeConcurrency: 1`, the received query ordinal `q`
is exactly one plus the zero-based `searchPage` invocation index; for ordinal
`q` and occurrence `r` the item sets **exactly** `title: receivedQuery`,
`snippet: receivedQuery`, `displayLink: host`, and
``link: `https://${host}/products/result-${pad2(r)}` `` where
``host = `w6-q${pad3(q)}-r${pad2(r)}.myshopify.com` ``; all other top-level
fixture members are preserved. The wrapper calls production
`parseGoogleSearchResponse(payload, receivedQuery)` and passes its result
through the **production query-probe path**. Each of all 100 validations must
witness ten usable distinct hosts, ten relevant results, relevance ratio
exactly `1`, and no rejection — parser success alone is not an acceptance
oracle (`EV-KI-A-084` `F11`: the DECOMP-3 link-only recipe preserved the
fixture title/snippet and a production `summarizeProbe` check yielded zero
relevant results, ratio zero, `irrelevant_probe_results`). The harness
**never preloads fabricated query-discovery artifacts**: `preloadLead` is not
imported or replicated, and the production discovery worker creates the 100
query discovery artifacts from the persisted probe results
(`src/aws-pipeline/services/discovery-worker.js:84`) through the actual
`dispatchConfirmedQueries` → `processDiscoveryMessage` chain.

**Drive table (exact message-to-function routing; the only public functions
the harness calls to move work):**

| Pending message / source | Public function called |
|---|---|
| `keyword.initialize.v1` (first keyword-queue message, emitted by backend `dispatchInitialize`) | `processInitialize(message, runtime)` — `src/aws-pipeline/keyword-intelligence/service.js:255` |
| every other keyword-queue message (`keyword.expansion.task.v1`, `keyword.overview.task.v1`, `keyword.aggregate.check.v1`) | `processKeywordMessage(message, runtime)` — `service.js:247` |
| discovery-queue messages (emitted by production `dispatchConfirmedQueries` inside the backend) | `processDiscoveryMessage(message, runtime)` — `src/aws-pipeline/services/discovery-worker.js:37` |
| domain-aggregation-queue messages | `processDomainAggregation(message, runtime, options)` — `src/aws-pipeline/services/domain-aggregator.js:36`, with the same `createLeaseMonitorFn` option value used for domain aggregation in `test/helpers/aws-pipeline-e2e-harness.js` `drainOne` (copy that option value verbatim from the anchor; no choice) |

The harness never calls `recoverKeywordWork`, `recoverPipelineWork`,
`processLeadMessage`, `processLeadAggregation`, `processTrafficBatch`, or
`processFinalAggregation`; W6 stops at the lead-task boundary. The drain
loop consumes pending delivery records in `deliveryId` order — **no
body-derived deduplication exists anywhere in the harness** (§0.1 item 9) —
with step ceilings of exactly 500 production handler invocations for each
`drainKeywordWork` call and 3,000 for `drainDownstream`; exceeding a ceiling
throws `HarnessStallError` with the pending-delivery/state diagnostics rather
than accepting partial work.

#### IF-3 — enforcement manifest (producer F-004; consumers F-005, V1)

Strict top-level keys `contractVersion` (`ki-w6-enforcement-manifest-v1`),
`groups` (`navigation` 3, `flow` 13, `resilience` 4, `conformance` 6),
`groupDigests` (four parent literals), `globalDigest`
(`d81bab26bc5aadd19c162156c13890611b2fc5a6d0dcb917234453d568ffb4d4`),
`negativeControls` (13). Full literal bytes in §4 `KI-W6-S104`.

#### IF-4 — certificate (producer F-005; consumers I101/parent)

Exactly one stdout line `KI_W6_CERTIFICATE=<canonical JSON>` emitted by
exactly one `console.log` site, with field order exactly
`{contractVersion, required, registered, executed, activated, skipped,
duplicates, unexpected, unactivated, groupDigests, globalDigest,
negativeControls, operationCounts, substituteClaims, obsoleteRuntimeHits}`
and no secrets.

## 4. Initial implementation sub-windows

Every block below contains all sub-window standard §7 fields. A block is
`DRAFT / NOT ASSIGNABLE` if any field is unresolved; none is.

---

### `KI-W6-S101` — Dashboard navigation correction

```yaml
subwindow_id: KI-W6-S101
type: FILE
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-02
leaf_assignment_id: ASG-KI-W6-S101
assigned_agent: UNASSIGNED   # one named leaf agent at dispatch
predecessors: []
successor_reserved_for: WINDOW-AGENT
writable_file: frontend/components/keyword-intelligence/research-dashboard.tsx
file_operation: MODIFY
starting_file_digest: 19494a99a2be28683167908289176bf44ebb8d0bb1eb40f63cc6d1cd770c6337
starting_repository_change_set_digest: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
read_only_scope: [frontend/components/keyword-intelligence/research-dashboard.tsx, frontend/lib/client-api.ts, frontend/lib/keyword-intelligence-validation.ts, frontend/lib/api-validation.ts, "frontend/app/api/keyword-research/[researchId]/runs/route.ts", email_scraper/src/server.js, A4 KI-W6 block, DEC-KI-038]
authorized_actions: [edit only the writable file inside the two pinned expressions, run the S101 LOCAL_NOW checks]
prohibited_actions: [every other edit in the file, imports/state/props/type changes, helper/fallback/route-probe/conditional additions, builds, second-file edits, spawning or delegating to any other implementation agent, successor work, parent communication, external mutations]
may_start_successor: false
```

**Mechanical trace.** `KI-W6-T1` items 1–15; `REQ-KI-015`–`017`;
`INV-KI-010/014/015`; `DEC-KI-035/038`; `SRC-KI-038`; `SCN-KI-018` navigation
partition; coverage `W6-NAV-01`–`03` (production path) and `W6-NC-01`
(negative control in `S105` over the captured routing choice).

**Exact file transformation.**

1. Source anchor A: `handleFinalize` success branch, current line 266:
   `      router.push(handoff.statusUrl);`
2. Source anchor B: `handleRetryHandoff` success branch, current line 300:
   `      router.push(handoff.statusUrl);`
3. Replace each of the two exact lines (six-space indentation preserved,
   single-line for single-line, no other byte changes) with:
   ``      router.push(`/runs/${encodeURIComponent(handoff.run.runId)}`);``
4. Execution order: anchor A then anchor B. Two replacements total.
5. Complete signatures/constants: none added. `encodeURIComponent` is native;
   no import, package, state, prop, component, or public type change.
6. Imports/exports/callers affected: none. `startKeywordResearchRun` return
   shape (`KeywordResearchRunResponse = { run: RunStatus; statusUrl: string }`,
   `frontend/lib/keyword-intelligence-types.ts:91-94`) is consumed unchanged.
7. Operation ordering/atomicity: unchanged handoff transaction remains
   authoritative; routing occurs only after the existing successful response
   and never changes durable state.
8. Outcomes: every existing definitive/ambiguous failure state is unchanged;
   successful same-key retry routes to the same encoded Run ID; zero I/O,
   fetch, database, provider, queue, or artifact operations are added.
9. Preserved behavior: all other 527 lines byte-identical; line count stays
   529.
10. Obsolete behavior removed from this file: navigation to
    `handoff.statusUrl` in the browser (both branches).
11. Resulting interface for successors: IF-1 exactly.
12. Forbidden edits within the writable file: everything except the two lines.

**Exact checks (all `LOCAL_NOW`; no build/lint/tsc — deferred to V2).**

| ID | Exact command (from workspace root) | Expected result / activation witness |
|---|---|---|
| S101-C1 | `grep -cF 'router.push(handoff.statusUrl)' frontend/components/keyword-intelligence/research-dashboard.tsx` | exit 1 with count 0 (zero occurrences) |
| S101-C2 | `grep -cF 'router.push(`/runs/${encodeURIComponent(handoff.run.runId)}`)' frontend/components/keyword-intelligence/research-dashboard.tsx` | exactly `2` |
| S101-C3 | `wc -l frontend/components/keyword-intelligence/research-dashboard.tsx` | exactly `529` |
| S101-C4 | `git -C frontend diff --numstat -- components/keyword-intelligence/research-dashboard.tsx` | exactly `2 inserted, 2 deleted` in this file |

Expected workspace write set: exactly
`frontend/components/keyword-intelligence/research-dashboard.tsx`.
`DEFERRED_TO_INTEGRATION`: V2 lint/tsc/build of the changed file; V3 causal
navigation assertions `W6-NAV-01`–`03`; `W6-NC-01`.

**Completion checklist (leaf must return with checked boxes and `S3`-resolvable
citations):**

- [ ] P1 Revisions, assignment identity, writable file, baseline digest, and predecessor evidence match.
- [ ] P2 Starting repository status and protected dirty changes match the recorded baseline.
- [ ] T1 Apply every ordered transformation and no other edit to the writable file.
- [ ] V1 Run every LOCAL_NOW check and record its activation witnesses and exact assertions.
- [ ] V2 Prove the attributable workspace changed-file set is exactly the writable file.
- [ ] V3 Prove required local coverage IDs equal registered and executed local IDs with zero skips. (For S101: local coverage is the C1–C4 witness set; `W6-NAV-01`–`03` are registered in `S105` and deferred by design to V3.)
- [ ] H1 Return the exact diff, ending digest, commands, outcomes, and residual integration obligations.
- [ ] H2 Confirm no prohibited action, second-file edit, successor work, external mutation, or parent communication occurred.
- [ ] H3 Stop at AWAITING_WINDOW_REVIEW.

---

### `KI-W6-S102` — Accepted R5 navigation-oracle supersession

```yaml
subwindow_id: KI-W6-S102
type: FILE
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-02
leaf_assignment_id: ASG-KI-W6-S102
assigned_agent: UNASSIGNED
predecessors: [KI-W6-S101]
successor_reserved_for: WINDOW-AGENT
writable_file: frontend/test/browser/keyword-intelligence-dashboard.mjs
file_operation: MODIFY
starting_file_digest: d30bed66cdc77ff53438515345be01baf2e1ad90ea2b9b8c8ab71c47f339c398
starting_repository_change_set_digest: d1349d2efaeb4f235fdc62a01f529a7c4c861e814964c4a12c05eba5f27f0be2
read_only_scope: [frontend/test/browser/keyword-intelligence-dashboard.mjs, A4 KI-W6-T2 block, DEC-KI-038, frontend/components/keyword-intelligence/research-dashboard.tsx (post-S101)]
authorized_actions: [edit only the writable file inside the R5-FIN-01 fixture assignment/comment/final pathname assertion, run the S102 LOCAL_NOW checks]
prohibited_actions: [changes to any other R5/W5 case, registration, screenshot, certificate, fetch interception, presentation assertion, registry/case-set/output-path/helper/port/build/browser-lifecycle changes, adding any W6 registration here, builds, second-file edits, spawning or delegating to any other implementation agent, successor work, parent communication]
may_start_successor: false
```

**Mechanical trace.** `KI-W6-T2` items 1–15; `REQ-KI-015`–`017`;
`DEC-KI-037/038`; superseding evidence `W6-NAV-01`–`03`; control `W6-NC-01`
(executed in `S105`).

**Exact file transformation.** Scope: the `R5-FIN-01` scenario block only
(current lines 1769–1787). Ordered edits:

1. Replace the two comment lines (current 1774–1775)
   `    // Route the handoff to a distinct statusUrl so the router-push navigation`
   `    // is observable without depending on the current page's own path.`
   with exactly:
   `    // Superseded in KI-W6: the browser must open the run workspace derived`
   `    // from handoff.run.runId; a valid but hostile same-origin API statusUrl`
   `    // must never choose the browser destination (DEC-KI-038).`
2. Insert immediately before the `await evaluate(cdp, ...)` of this block:
   `    const hostileStatusPath = "/api/runs/run_kiw5_hostile_status_witness0001";`
3. Replace the fixture assignment line (current 1778)
   `      handoff.statusUrl = "/keywords/ki-r5-fin-nav-witness";`
   with exactly:
   `      handoff.statusUrl = ${JSON.stringify(hostileStatusPath)};`
   (inside the existing template literal; `runHandoff.run.runId` remains the
   expected workspace identity and `runHandoff` stays valid and
   `statusUrl`-present).
4. Insert immediately after the three existing `fin` assertions and before the
   navigation `waitFor`:
   ``    const workspacePath = `/runs/${encodeURIComponent(runHandoff.run.runId)}`;``
5. Replace the final pathname assertion (current 1785)
   `    await waitFor(cdp, "location.pathname === '/keywords/ki-r5-fin-nav-witness'", "finalize navigation witness");`
   with exactly:
   ``    await waitFor(cdp, `location.pathname === ${JSON.stringify(workspacePath)}`, "finalize workspace navigation witness");``
6. Insert immediately after that `waitFor`:
   ``    assert((await evaluate(cdp, `location.pathname === ${JSON.stringify(hostileStatusPath)}`)) === false, "hostile handoff statusUrl pathname must not be visited");``
7. Keep `await capture(cdp, "R5-FIN-01-finalize");` and every other line of the
   block and file byte-identical.

Complete constants: hostile literal
`/api/runs/run_kiw5_hostile_status_witness0001` (matches `RUN_ID_PATTERN`
shape, distinct from fixture run `run_kiw5_finalize_000000000001` and from the
workspace route); `workspacePath` derived independently from the fixture Run
ID, not from production routing code. The hostile literal occurs exactly once
in the resulting file (the `hostileStatusPath` declaration; the added
assertion references the variable). Operations: the existing one finalize POST
and one router transition remain; zero extra request, retry, screenshot, or
fixture-interception behavior. Atomicity unchanged; the fixture proves
navigation only and makes no SQL claim. Failure/replay partitions of other R5
cases are untouched; only the successful `R5-FIN-01` destination oracle is
superseded. No W6 registration is added here. Symbols `hostileStatusPath` and
`workspacePath` are verified unused elsewhere in the file. Resulting
interface: none new; the stable `R5-FIN-01` registration remains. Exact diff
arithmetic: 8 inserted lines, 4 deleted lines (comments −2/+3, +1 const
`hostileStatusPath`, assignment line replaced −1/+1, +1 const
`workspacePath`, `waitFor` line replaced −1/+1, +1 `assert`).

**Exact checks (`LOCAL_NOW`; behavior intentionally not executed here — it is
superseded by the causal `W6-NAV-01`–`03`).**

| ID | Exact command (from workspace root) | Expected result |
|---|---|---|
| S102-C1 | `node --check frontend/test/browser/keyword-intelligence-dashboard.mjs` | exit 0 |
| S102-C2 | `grep -c 'ki-r5-fin-nav-witness' frontend/test/browser/keyword-intelligence-dashboard.mjs` | 0 occurrences (exit 1) |
| S102-C3 | `grep -cF 'run_kiw5_hostile_status_witness0001' frontend/test/browser/keyword-intelligence-dashboard.mjs` | exactly `1` |
| S102-C4 | `grep -cF 'encodeURIComponent(runHandoff.run.runId)' frontend/test/browser/keyword-intelligence-dashboard.mjs` | exactly `1` |
| S102-C5 | `grep -c 'runScenario(' frontend/test/browser/keyword-intelligence-dashboard.mjs` | exactly `26` (registration set unchanged) |
| S102-C6 | `git -C frontend diff --numstat -- test/browser/keyword-intelligence-dashboard.mjs` | exactly `8 inserted, 4 deleted` in this file |

Expected workspace write set: exactly
`frontend/test/browser/keyword-intelligence-dashboard.mjs`.
`DEFERRED_TO_INTEGRATION`: V2 eslint of this file; the superseded behavior is
executed only as `W6-NAV-01`–`03`/`W6-NC-01` in V3.

**Completion checklist:** identical P1–H3 list as `KI-W6-S101`, with "writable
file" read as this file and local coverage = C1–C6 witnesses.

---

### `KI-W6-S103` — Causal local service harness

```yaml
subwindow_id: KI-W6-S103
type: FILE
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-02
leaf_assignment_id: ASG-KI-W6-S103
assigned_agent: UNASSIGNED
predecessors: [KI-W6-S102]
successor_reserved_for: WINDOW-AGENT
writable_file: email_scraper/test/helpers/keyword-intelligence-e2e-harness.js
file_operation: CREATE
starting_file_digest: ABSENT
starting_repository_change_set_digest: fbfdac4a76ef0754ab3de904905a85b38b3777b2ad39926625f46ae4ae503954
read_only_scope: [email_scraper/test/helpers/isolated-postgres.js, email_scraper/test/keyword-intelligence-worker.test.js, email_scraper/test/keyword-intelligence-worker-flow.test.js, email_scraper/test/helpers/aws-pipeline-e2e-harness.js, email_scraper/test/aws-pipeline-end-to-end.integration.test.js, email_scraper/test/fixtures/providers/google/custom-search-v1-success.json, email_scraper/test/fixtures/keyword-intelligence/dataforseo-suggestions-cases-v1.json, email_scraper/test/fixtures/keyword-intelligence/dataforseo-related-cases-v1.json, email_scraper/test/fixtures/keyword-intelligence/dataforseo-overview-cases-v1.json, email_scraper/src/server.js, email_scraper/src/config.js, email_scraper/src/log.js, email_scraper/src/query-review.js, email_scraper/src/search.js, email_scraper/src/shop-persistence-contract.js, email_scraper/src/prisma-run-repository.js, email_scraper/src/keyword-intelligence/api.js, email_scraper/src/keyword-intelligence/repository.js, email_scraper/src/aws-pipeline/runtime.js, email_scraper/src/aws-pipeline/keyword-intelligence/contracts.js, email_scraper/src/aws-pipeline/keyword-intelligence/dataforseo-labs-adapter.js, email_scraper/src/aws-pipeline/keyword-intelligence/handler.js, email_scraper/src/aws-pipeline/keyword-intelligence/keys.js, email_scraper/src/aws-pipeline/keyword-intelligence/recovery.js, email_scraper/src/aws-pipeline/keyword-intelligence/service.js, email_scraper/src/aws-pipeline/services/confirmed-query-dispatcher.js, email_scraper/src/aws-pipeline/services/discovery-worker.js, email_scraper/src/aws-pipeline/services/domain-aggregator.js, email_scraper/src/aws-pipeline/services/final-aggregator.js, email_scraper/src/aws-pipeline/services/lead-aggregator.js, email_scraper/src/aws-pipeline/services/lead-worker.js, email_scraper/src/aws-pipeline/services/recovery.js, email_scraper/src/aws-pipeline/services/traffic-worker.js, A4 KI-W6-T3 block, DEC-KI-038]
authorized_actions: [create the writable file, run the S103 LOCAL_NOW checks (no database connection during the leaf)]
prohibited_actions: [production-source edits, package/schema changes, direct terminal-database fabrication, Python/SQLite/standalone-project imports or output.json/data-dir paths, raw provider body/HTML/cookie/authorization/credential-bearing URL/contact-data logging, live auth/provider/AWS calls, Lambda emulation, lead scrape/enrichment, builds, second-file edits, spawning or delegating to any other implementation agent, successor work, parent communication]
may_start_successor: false
```

**Mechanical trace.** `KI-W6-T3` items 1–15; `REQ-KI-001`–`013`,
`015`–`017`, `019`–`024`; `INV-KI-001`–`009`, `011`–`015`;
`DEC-KI-001`–`024`, `026`–`038`; activation-trace supplier for
`W6-FLOW-01`–`13` and `W6-RES-01`–`04`; negative controls `NC-02`–`09`, `12`
(mutate captured test state only, via `injectCapturedDefect` and the frozen
trace).

**Exact file transformation.** Create one ESM module (backend is
`"type": "module"`) implementing IF-2 exactly (signatures, frozen-object
literal, trace union, fault union, error names, config/queue literals, clock,
seeds, host template, `TASK_COSTS`, `SCHEMA_PREFIX`, `DISPATCHER_METHODS`
assertion, drive table, step ceilings). The implementation recipe, with
verified source anchors, in construction order:

1. **Schema.** `resolveDirectTestDatabaseUrl({testDatabaseUrl,
   testDirectDatabaseUrl, productionDatabaseUrl})` → unique `kiw6_`-prefixed
   schema via `assertSafeDisposableSchema`, `createIsolatedTestSchema`,
   `deployPrismaMigrations`, `assertMigrationStayedInSchema` exactly as
   `test/keyword-intelligence-worker.test.js::withIsolatedDb` (lines 270–282)
   does, with `scopedTestDatabaseUrl`; `close()` drops the schema CASCADE and
   disconnects.
2. **Auth server.** Loopback HTTP server bound `127.0.0.1:0`;
   `GET /get-session` returns exactly the IF-2 mode payloads with status 200;
   `setAuthOwner` switches modes; the actual port is published through
   `frontendEnv`.
3. **Backend server.** Actual Prisma repositories
   (`PrismaKeywordResearchRepository` from
   `src/keyword-intelligence/repository.js`, `PrismaRunRepository` with the
   exact IF-2 frozen `awsProviderConfigSnapshot` recipe options from
   `src/prisma-run-repository.js`) and `createLeadServer(config, options)`
   (`src/server.js:1457`) with the literal IF-2 server config object (including
   `backendApiToken: "kiw6-backend-token"`, the same literal `frontendEnv`
   publishes) and the frozen options (clock, FIFO `schedule`,
   lease/interval literals, and the callable no-op logger `() => {}`);
   the returned `http.Server` is bound by the harness to `127.0.0.1:0`;
   actual port published via `frontendEnv`. The harness never calls
   `loadConfig()`. Inject exactly: `pipelineRuntimeFactory` returning a
   runtime carrying the IF-2 config/queue literals, the in-memory S3
   artifact store and dispatcher, `runtime.http` as the sole DataForSEO
   transport (the adapter reaches HTTP only through it,
   `dataforseo-labs-adapter.js:245-250`), `researchQueryValidationPipeline` as
   a thin wrapper calling production `validateResearchBackedConfirmedQueryRows`
   (`src/query-review.js:341`) with the deterministic IF-2 Google-expansion
   `searchPage` (production `parseGoogleSearchResponse` on the ten-item
   expanded fixture payload for the received query), and
   `createLeadServer.schedule` as a FIFO callback queue so the harness
   deterministically starts each accepted queue-drain callback (consumption
   point `src/server.js:1654`).
4. **Provider substitutes (literal; A4 `KI-CL-20` T3 item 6).** Raw task
   bodies report the frozen `TASK_COSTS` literals (ten expansion calls
   `0.01560000`, 300-keyword anchor `0.04800000`, eight 200-keyword markets
   `0.03600000`, total `0.49200000`). Keyword synthesis uses exactly the
   IF-2 "Literal provider synthesis" contract: the `pad2`/`pad3` literals,
   the per-seed 30 suggestion and 30 related strings in ascending `i`, the
   seed + 30 suggestions + first 29 related per-seed retention (300 distinct
   anchor inputs), and every overview item from the exact
   `overviewResponse` formula at
   `keyword-intelligence-worker.test.js:93-122` (cost `0.048` for 300
   inputs, `0.036` for 200); production aggregation must witness 300 active
   anchor candidates, the deterministic first-200 shortlist, and a 200-row
   final result with the default-100 selection. Google responses use the
   exact IF-2 Google per-query expansion contract (title/snippet =
   `receivedQuery`, `displayLink` = host,
   ``link: `https://${host}/products/result-${pad2(r)}` ``; ordinal `q` =
   1 + zero-based `searchPage` invocation index) and are accepted only
   through the production query-probe path (ten usable distinct hosts, ten
   relevant results, ratio `1`, no rejection per validation);
   **no query-discovery artifacts are preloaded** (`preloadLead` never
   imported; the production discovery worker creates the 100 artifacts from
   the persisted probe results, `discovery-worker.js:84`).
5. **Work driving.** Only the public functions in the IF-2 drive table; the
   dispatcher implements `sendOne` and `sendMany`, assigns one monotonic
   `deliveryId` per enqueued delivery, and the drain invokes the production
   handler exactly once per pending delivery — including intentionally
   duplicated or reordered bodies — in `deliveryId` order, with no
   body-derived deduplication anywhere (§0.1 item 9).
6. **Trace.** Every auth, DataForSEO, Google, S3, SQS, and backend HTTP
   operation is recorded as exactly one IF-2 trace-union tuple. Strict
   artifact adapters parse schemas on put/get and reject unequal immutable
   replay with the `PIPELINE_ARTIFACT_CONFLICT` discriminator
   (`aws-pipeline-e2e-harness.js:82-85` parity).
7. **Atomicity.** Actual Prisma transactions for result publication,
   selection CAS, handoff, and downstream coordinator. Fault hooks
   (`injectCapturedDefect`) operate only before/after public calls; they never
   edit production source or directly fabricate a terminal database state.
8. **Identities.** Deterministic five seeds (IF-2 literals); 100 retained
   keywords/queries; query IDs from the actual RunQuery creator; hosts per the
   IF-2 template; assert actual `stableShopIdentity`, `shopIdForStableKey`,
   and `runStoreId` outputs (`src/shop-persistence-contract.js:175/308/313`)
   rather than duplicating formulas.
9. **Locked test operations (A4 `KI-CL-20` T3 item 10).** Owner switch
   (`setAuthOwner`) followed by emitted-Next restart (driven by `S105`);
   the six queue-specific duplicate/reorder faults exactly as frozen in
   IF-2 member 9, invoked at their exact nonempty injection points (keyword
   duplicate/reorder immediately after initialization queues expansion
   tasks/checks, then restart A via `restartBackend()` retaining DB/S3/SQS,
   then the
   expansion drain; discovery duplicate/reorder immediately after
   confirmation dispatches the 100 discovery deliveries; domain-check
   duplicate/reorder after the first discovery emits a domain check, before
   the downstream drain completes) with each duplicate under a fresh
   monotonic delivery ID and no dispatcher send trace so base send counts
   stay unchanged; corrupt captured artifact before validated read (fault
   `corrupt-stored-artifact`); omit one Neon terminal while leaving its S3
   object (fault `omit-neon-terminal`); replay the same client request ID
   (driven by `S105` in `W6-NAV-02`). After the post-handoff research-selection
   mutation, S105 invokes restart B through the same `restartBackend()` method,
   reloads the durable run projection, and performs the `W6-FLOW-13` immutable
   snapshot comparison before any owner switch. The corrupt-artifact and missing-terminal
   partitions each use a separate one-seed research in the same schema: two
   expansion calls and two stored task objects; corrupt-artifact has two
   terminal tasks then mutates one memory object before the actual aggregate
   read (`2/2/2/0` calls/objects/terminal tasks/next-stage rows);
   missing-terminal throws only after the second immutable put so exactly one
   task is terminal (`2/2/1/0`). Both have zero next-stage rows and zero
   result visibility, reported through `readDurableState().fixtures`.
10. **Imports.** Only the read-scope backend test helpers and production
    exports; no Python, SQLite, output JSON, static dashboard, CDN, or
    standalone project path (`KeywordSearchVolume` never referenced).

Resulting interface: IF-2 exactly; the sole importer is `S105`'s file.

**Exact checks (`LOCAL_NOW`; no database connection, no build).**

| ID | Exact command (from workspace root) | Expected result |
|---|---|---|
| S103-C1 | `node --check email_scraper/test/helpers/keyword-intelligence-e2e-harness.js` | exit 0 |
| S103-C2 | `grep -cF 'export async function createKeywordIntelligenceE2eHarness({' email_scraper/test/helpers/keyword-intelligence-e2e-harness.js` | exactly `1` |
| S103-C3 | `grep -cF 'return Object.freeze({ frontendEnv, ownerId, otherOwnerId, trace, setAuthOwner, drainKeywordWork, restartBackend, drainDownstream, readDurableState, injectCapturedDefect, close });' email_scraper/test/helpers/keyword-intelligence-e2e-harness.js` | exactly `1` |
| S103-C4 | `grep -cE 'KeywordSearchVolume|data/output|output\.json|sqlite|\.py\b|python' email_scraper/test/helpers/keyword-intelligence-e2e-harness.js` | 0 occurrences (exit 1) |
| S103-C5 | `grep -cF 'w6-q${String(q).padStart(3, "0")}-r${String(r).padStart(2, "0")}.myshopify.com' email_scraper/test/helpers/keyword-intelligence-e2e-harness.js` | exactly `1` |
| S103-C6 | `grep -cF 'const TASK_COSTS = { expansion: "0.01560000", anchor: "0.04800000", market: "0.03600000", total: "0.49200000" };' email_scraper/test/helpers/keyword-intelligence-e2e-harness.js` | exactly `1` |
| S103-C7 | `grep -cF 'const SCHEMA_PREFIX = "kiw6_";' email_scraper/test/helpers/keyword-intelligence-e2e-harness.js` | exactly `1` |
| S103-C8 | `grep -cF 'const DISPATCHER_METHODS = ["sendMany", "sendOne"];' email_scraper/test/helpers/keyword-intelligence-e2e-harness.js` | exactly `1` |
| S103-C9 | `grep -cF 'duplicate-next-keyword-message' email_scraper/test/helpers/keyword-intelligence-e2e-harness.js`; likewise separate `grep -cF` runs for `reorder-pending-keyword-messages`, `duplicate-next-discovery-message`, `reorder-pending-discovery-messages`, `duplicate-next-domain-check-message`, `reorder-pending-domain-check-messages`, `corrupt-stored-artifact`, `omit-neon-terminal` | exactly `1` each (eight fault IDs) |
| S103-C10 | `grep -c 'preloadLead' email_scraper/test/helpers/keyword-intelligence-e2e-harness.js` | 0 occurrences (exit 1; no fabricated discovery artifacts) |
| S103-C11 | `grep -cF 'const SCHEMA_ABSENCE_QUERY = "SELECT schema_name FROM information_schema.schemata WHERE schema_name = $1";' email_scraper/test/helpers/keyword-intelligence-e2e-harness.js` | exactly `1` |
| S103-C12 | `grep -cF 'HarnessCleanupError' email_scraper/test/helpers/keyword-intelligence-e2e-harness.js` | exactly `1` |
| S103-C13 | `grep -cF 'BACKEND_API_TOKEN: "kiw6-backend-token"' email_scraper/test/helpers/keyword-intelligence-e2e-harness.js` | exactly `1` |
| S103-C14 | `grep -cF 'const pad2 = (n) => String(n).padStart(2, "0");' email_scraper/test/helpers/keyword-intelligence-e2e-harness.js` and `grep -cF 'const pad3 = (n) => String(n).padStart(3, "0");' email_scraper/test/helpers/keyword-intelligence-e2e-harness.js` | exactly `1` each |
| S103-C15 | `grep -cF 'suggestion s${s}${pad2(i)}' email_scraper/test/helpers/keyword-intelligence-e2e-harness.js` and `grep -cF 'related r${s}${pad2(i)}' email_scraper/test/helpers/keyword-intelligence-e2e-harness.js` and `grep -cF '/products/result-${pad2(r)}' email_scraper/test/helpers/keyword-intelligence-e2e-harness.js` | exactly `1` each |
| S103-C16 | `grep -cF 'logger: () => {}' email_scraper/test/helpers/keyword-intelligence-e2e-harness.js` | exactly `1` |

`DEFERRED_TO_INTEGRATION`: every behavioral claim (`W6-FLOW-*`, `W6-RES-*`,
`NC-02`–`09`, `12`, operation counts, schema lifecycle) executes only in V3.

**Completion checklist:** identical P1–H3 list, local coverage = C1–C16
witnesses; the leaf proves syntax/structure only and claims zero behavioral
parity (substitute ledger bounds its claims at V3).

---

### `KI-W6-S104` — Literal W6 enforcement manifest

```yaml
subwindow_id: KI-W6-S104
type: FILE
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-02
leaf_assignment_id: ASG-KI-W6-S104
assigned_agent: UNASSIGNED
predecessors: [KI-W6-S103]
successor_reserved_for: WINDOW-AGENT
writable_file: email_scraper/test/fixtures/keyword-intelligence/ki-w6-enforcement-manifest-v1.json
file_operation: CREATE
starting_file_digest: ABSENT
starting_repository_change_set_digest: b94659a0de51b39e36e984c858ee4f0fa0effefaba27140ea29146fa947515e9
read_only_scope: [A4 KI-W6 coverage matrix + KI-W6-T4 block, DEC-KI-038 "Executable case set", this S1 block]
authorized_actions: [create the writable file with exactly the literal bytes below, run the S104 LOCAL_NOW checks]
prohibited_actions: [wildcards, ranges, dynamic generation, extra/missing keys, wrong order or digests, execution evidence, runtime config, provider fixture content, old W6 artifact repair, second-file edits, spawning or delegating to any other implementation agent, successor work, parent communication]
may_start_successor: false
```

**Mechanical trace.** `KI-W6-T4` items 1–15; all `DEC-KI-038` requirements;
authoring standard E6–E8; authority for the required set consumed by `S105`
(`W6-CONF-01`, `W6-NC-10`).

**Exact file transformation.** Create the file with exactly these bytes
(two-space indent, one final LF, no trailing spaces):

```json
{
  "contractVersion": "ki-w6-enforcement-manifest-v1",
  "groups": {
    "navigation": [
      "W6-NAV-01",
      "W6-NAV-02",
      "W6-NAV-03"
    ],
    "flow": [
      "W6-FLOW-01",
      "W6-FLOW-02",
      "W6-FLOW-03",
      "W6-FLOW-04",
      "W6-FLOW-05",
      "W6-FLOW-06",
      "W6-FLOW-07",
      "W6-FLOW-08",
      "W6-FLOW-09",
      "W6-FLOW-10",
      "W6-FLOW-11",
      "W6-FLOW-12",
      "W6-FLOW-13"
    ],
    "resilience": [
      "W6-RES-01",
      "W6-RES-02",
      "W6-RES-03",
      "W6-RES-04"
    ],
    "conformance": [
      "W6-CONF-01",
      "W6-CONF-02",
      "W6-CONF-03",
      "W6-CONF-04",
      "W6-CONF-05",
      "W6-CONF-06"
    ]
  },
  "groupDigests": {
    "navigation": "103df26205674ddd7f4e7548b3432ea7f5342096bd369991e067debf7f3bf6f2",
    "flow": "14aa36ae942fc9eedef7d9fae9ae0a42775f6ab22c04e3dabb2cf1cbe9379461",
    "resilience": "fc83e2c68fcd67e1849b955b3a9e48fe7a998aed1f1ac0ad6c0f943efeea354d",
    "conformance": "b8180b2f2561d41298252db30b075d4184da3535af065a29f0273e12392c5646"
  },
  "globalDigest": "d81bab26bc5aadd19c162156c13890611b2fc5a6d0dcb917234453d568ffb4d4",
  "negativeControls": [
    "W6-NC-01",
    "W6-NC-02",
    "W6-NC-03",
    "W6-NC-04",
    "W6-NC-05",
    "W6-NC-06",
    "W6-NC-07",
    "W6-NC-08",
    "W6-NC-09",
    "W6-NC-10",
    "W6-NC-11",
    "W6-NC-12",
    "W6-NC-13"
  ]
}
```

Arrays are unique strings in ascending byte order; digests use
sorted-distinct-UTF-8-member-plus-LF and equal the five `DEC-KI-038` literals
(all recomputed and verified in `EV-KI-W6-R01`, re-verified in
`EV-KI-W6-R04`, `EV-KI-W6-R06`, under state 145 in `EV-KI-W6-R08`, under
state 146 in `EV-KI-W6-R10`, and under state 147 in `EV-KI-W6-R12`).
Deterministic whole-file strict parse is fail-closed;
identical replay is byte-equal. Case/control IDs are opaque stable
identities, not reused from the invalidated decomposition.

**Exact checks (`LOCAL_NOW`; exact commands, no prose oracles).**

| ID | Exact command (from workspace root) | Expected result |
|---|---|---|
| S104-C1 | `node -e 'JSON.parse(require("fs").readFileSync("email_scraper/test/fixtures/keyword-intelligence/ki-w6-enforcement-manifest-v1.json","utf8"));console.log("S104-C1 OK")'` | prints `S104-C1 OK`, exit 0 |
| S104-C2 | `node -e 'const m=JSON.parse(require("fs").readFileSync("email_scraper/test/fixtures/keyword-intelligence/ki-w6-enforcement-manifest-v1.json","utf8"));const eq=(a,b)=>JSON.stringify(a)===JSON.stringify(b);if(!eq(Object.keys(m),["contractVersion","groups","groupDigests","globalDigest","negativeControls"]))throw new Error("top-level keys");if(!eq(Object.keys(m.groups),["navigation","flow","resilience","conformance"]))throw new Error("group keys");if(!eq(Object.keys(m.groups).map(k=>m.groups[k].length),[3,13,4,6]))throw new Error("group counts");const all=Object.values(m.groups).flat();if(new Set(all).size!==26)throw new Error("26 unique cases");if(new Set(m.negativeControls).size!==13||m.negativeControls.length!==13)throw new Error("13 controls");for(const k of Object.keys(m.groups)){const a=m.groups[k];if(!eq(a,[...a].sort()))throw new Error("order "+k)}if(!eq(m.negativeControls,[...m.negativeControls].sort()))throw new Error("control order");console.log("S104-C2 OK")'` | prints `S104-C2 OK`, exit 0 |
| S104-C3 | `node -e 'const c=require("crypto");const m=JSON.parse(require("fs").readFileSync("email_scraper/test/fixtures/keyword-intelligence/ki-w6-enforcement-manifest-v1.json","utf8"));const d=a=>c.createHash("sha256").update([...new Set(a)].sort().map(s=>s+"\n").join("")).digest("hex");for(const k of Object.keys(m.groups)){if(d(m.groups[k])!==m.groupDigests[k])throw new Error("group digest "+k)}if(d(Object.values(m.groups).flat())!==m.globalDigest)throw new Error("global digest");console.log("S104-C3 OK")'` | prints `S104-C3 OK`, exit 0 |
| S104-C4 | `node -e 'const b=require("fs").readFileSync("email_scraper/test/fixtures/keyword-intelligence/ki-w6-enforcement-manifest-v1.json");if(b[b.length-1]!==10)throw new Error("final LF");if(b[0]===0xef)throw new Error("BOM");console.log("S104-C4 OK")'` | prints `S104-C4 OK`, exit 0 |

(JS `.sort()` equals unsigned UTF-8 byte order for this pure-ASCII ID set;
the digest script implements the standard's member-plus-LF formula.)

`DEFERRED_TO_INTEGRATION`: manifest conformance execution (`W6-CONF-01`,
`W6-NC-10`) in V3.

**Completion checklist:** identical P1–H3 list, local coverage = C1–C4.

---

### `KI-W6-S105` — Emitted causal browser workflow and enforcement

```yaml
subwindow_id: KI-W6-S105
type: FILE
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-02
leaf_assignment_id: ASG-KI-W6-S105
assigned_agent: UNASSIGNED
predecessors: [KI-W6-S104]
successor_reserved_for: WINDOW-AGENT
writable_file: frontend/test/browser/keyword-intelligence-e2e.mjs
file_operation: CREATE
starting_file_digest: ABSENT
starting_repository_change_set_digest: dc48365f600adb2d36194745f5c6433ee34339626c03bf6f509245661ee2dbcc
read_only_scope: [frontend/test/browser/keyword-intelligence-dashboard.mjs (CDP process/readiness/cleanup patterns), email_scraper/test/helpers/keyword-intelligence-e2e-harness.js, email_scraper/test/fixtures/keyword-intelligence/ki-w6-enforcement-manifest-v1.json, frontend/app/keywords/page.tsx, "frontend/app/keywords/[researchId]/page.tsx", "frontend/app/runs/[runId]/page.tsx", frontend/app/api/keyword-research/route.ts, "frontend/app/api/keyword-research/[researchId]/route.ts", "frontend/app/api/keyword-research/[researchId]/selection/route.ts", "frontend/app/api/keyword-research/[researchId]/runs/route.ts", "frontend/app/api/keyword-research/[researchId]/export.csv/route.ts", frontend/lib/client-api.ts, frontend/lib/keyword-intelligence-validation.ts, frontend/lib/keyword-intelligence-types.ts, frontend/lib/api-validation.ts, frontend/lib/api-types.ts, frontend/lib/backend-proxy.ts, frontend/lib/auth/server.ts, frontend/lib/auth/client.ts, frontend/lib/auth/route.ts, frontend/components/keyword-intelligence/research-dashboard.tsx, frontend/components/keyword-intelligence/research-form.tsx, frontend/components/keyword-intelligence/research-status.tsx, frontend/components/keyword-intelligence/selection-review.tsx, frontend/components/keyword-intelligence/keyword-table.tsx, frontend/components/keyword-intelligence/filter-bar.tsx, frontend/components/keyword-intelligence/summary-cards.tsx, frontend/components/keyword-intelligence/chart-panels.tsx, frontend/components/keyword-intelligence/cluster-landscape.tsx, frontend/components/run-workspace.tsx, frontend/components/query-editor.tsx, frontend/package.json, "frontend/node_modules/next/dist/docs/01-app/01-getting-started/15-route-handlers.md", "frontend/node_modules/next/dist/docs/01-app/02-guides/environment-variables.md", frontend/node_modules/next/dist/docs/index.md, email_scraper/package.json, email_scraper/scripts/build-keyword-worker.js, email_scraper/src/aws-pipeline/keyword-intelligence/handler.js, email_scraper/src/server.js, A4 KI-W6-T5 block + coverage matrix + controls + substitute ledger, DEC-KI-038, SCN-KI-018]
authorized_actions: [create the writable file, run the S105 LOCAL_NOW checks (no build, no browser, no database during the leaf)]
prohibited_actions: [browser application-API response substitution or request short-circuit except the single prescribed W6-NAV-02 response-stage abort, screenshots/review files, second Chrome process or build, non-loopback binds, paid/cloud/provider/AWS calls, KI-W7 work, schema/migration/package/production edits, second-file edits, spawning or delegating to any other implementation agent, successor work, parent communication]
may_start_successor: false
```

**Mechanical trace.** `KI-W6-T5` items 1–15; all product
requirements/invariants/exclusions (`REQ-KI-001`–`024`,
`INV-KI-001`–`015`, `EXC-KI-001`–`008`, `AUTH-KI-001`–`004`, `006`–`007`);
`DEC-KI-038`; `SCN-KI-018`; registers/executes the authoritative matrix —
`W6-NAV-01`–`03`, `W6-FLOW-01`–`13`, `W6-RES-01`–`04`, `W6-CONF-01`–`06`,
`W6-NC-01`–`13` — exactly as specified in the A4 "Authoritative `KI-W6`
coverage matrix" and "Critical falsification controls" tables (each row's
preconditions, activation witness, exact oracle, and forbidden/control column
is copied into the file's case engine as literal assertions; the matrix tables
are the authority and are not restated here).

**Exact file transformation.** Create the sole W6 executable registry, causal
browser workflow, conformance engine, and final certificate, per A4 `KI-W6-T5`
items 1–15 verbatim. Frozen recipe with verified anchors:

1. **CLI.** `node test/browser/keyword-intelligence-e2e.mjs` from `frontend/`.
   Supports normal execution and `KI_W6_SKIP_BUILD=1` (frozen literal
   `const skipBuild = process.env.KI_W6_SKIP_BUILD === "1";`); normal
   execution must refuse absent database opt-in (`ALLOW_DATABASE_TESTS=true`
   plus harness preflight resolution of `TEST_DATABASE_URL`) with a clear
   preflight error. Preflight fails if `127.0.0.1:4357` is occupied (frozen
   literal `const port = 4357;`).
2. **Assembly.** Import IF-2 via
   `../../../email_scraper/test/helpers/keyword-intelligence-e2e-harness.js`;
   read IF-3 with `node:fs readFileSync` + strict `JSON.parse` resolved as
   `path.resolve(root, "../email_scraper/test/fixtures/keyword-intelligence/ki-w6-enforcement-manifest-v1.json")`.
   Build with `next build` unless explicitly skipped (reuse the accepted
   `keyword-intelligence-dashboard.mjs` build/start/CDP patterns: `nextBin`
   spawn lines 1071–1087, Chrome spawn lines 1089–1097, `Cdp` class 829–870,
   `waitFor/navigate/setViewport/evaluate/assert/runScenario` helpers). Next
   binds only `127.0.0.1:4357`; the `next start` child receives exactly the
   IF-2 allowlisted environment (PATH, HOME, NODE_ENV=production, and the
   four `frontendEnv` values including `BACKEND_API_TOKEN`) and nothing
   else; the `next build` child receives exactly `{ PATH, HOME }`; Chrome
   inherits the environment unchanged.
3. **No interception.** No application-API response substitution or request
   short-circuit. Sole permitted CDP intervention, for `W6-NAV-02` only:
   enable `Fetch` for the runs POST URL at stage `Response`; when paused, wait
   until the correlated backend trace and durable Run plus 100 RunQueries
   exist (harness `trace`/`readDurableState`), then `Fetch.failRequest` with
   zero supplied bytes so the UI enters `retry_required`; disable `Fetch`
   immediately after. The aborted request must have a matching committed
   backend trace.
4. **Cases.** Execute the 26 cases in manifest order with one independent
   activation witness per case (witness identity = case ID + captured
   evidence reference; `W6-CONF-03` requires 26 unique nonempty witnesses).
   Every browser API call must appear in the Chrome network trace and matching
   auth/backend/helper traces; only app-origin and loopback internal origins
   are allowed.
5. **Controls.** Run all thirteen captured-data controls in the frozen
   allocation below. Each control performs: unchanged oracle passes → exactly
   one injected defect on captured/synthetic test state → the same unchanged
   oracle throws → fresh unchanged witness passes. (`W6-NC-10` and `W6-NC-13`
   run the pass→fail→fresh-pass cycle once per enumerated sub-injection.) No
   control touches production code or production call paths.

   **Frozen control allocation (one exact mechanism per control; no
   alternatives):**

   | Control | Exact mutation mechanism (single) | Unchanged oracle that must throw |
   |---|---|---|
   | `W6-NC-01` | S105 captured-data substitution: in the captured `W6-NAV-01` navigation witness, replace the captured `location.pathname` value with the handoff `statusUrl` pathname | NAV destination assertion (expected encoded `/runs/<runId>`) |
   | `W6-NC-02` | S105 captured-data removal: delete the `auth` trace event correlated with the `W6-FLOW-01` create request from the captured correlation tuple | auth-chain/ownership assertion |
   | `W6-NC-03` | S105 captured-data removal: delete one expansion task/call/attempt tuple from the captured `W6-FLOW-03` arrays | exact-topology assertion (10/10/10; five suggestion + five related) |
   | `W6-NC-04` | S105 captured-data flip: mark the captured corrupt-artifact read outcome as parser-accepted | strict-contract rejection assertion |
   | `W6-NC-05` | S105 captured-data addition: append a result-visibility record without its matching final-fence event to the captured `W6-FLOW-05` publication set | durable-visibility assertion |
   | `W6-NC-06` | S105 captured-data removal: delete one RunQuery from the captured `W6-FLOW-08` handoff set | atomicity/immutability assertion (exactly 100, immutable snapshot) |
   | `W6-NC-07` | S105 captured-data removal: delete one (Google `search-page` event, ten-occurrence result) pair from the captured `W6-FLOW-10` set | 100-calls/1,000-occurrences assertion |
   | `W6-NC-08` | S105 captured-data flip: set the captured domain-stage completion flag to `true` derived from S3/message counts while one captured Neon terminal is absent | readiness/stable-merge assertion |
   | `W6-NC-09` | S105 synthetic-record injection: insert one synthetic response record labeled `source:"fetch-interception"` into the captured causal request chain | request-chain/fidelity assertion (every causal route event must originate from Chrome network + correlated traces) |
   | `W6-NC-10` | S105 synthetic-set injections on copies of the required/registered/executed ID sets: remove one member; duplicate one member; add one unexpected member; mark one member skipped; filter one member — five sub-injections, each falsifying its own unchanged set-equality assertion | required=registered=executed set equality per sub-injection |
   | `W6-NC-11` | S105 captured-data removal: delete one activation-witness entry from the captured 26-witness map | 26-unique-nonempty-activation assertion |
   | `W6-NC-12` | S105 captured-data broadening: rewrite the captured S3/SQS `substituteClaims` entry from the memory-adapter claim to a live-AWS-transport claim | substitute-fidelity assertion (claims within the frozen ledger) |
   | `W6-NC-13` | S105 synthetic-set injections into the discovered integrated dependency inventory, one per class: `kiw6-synthetic.py` (`.py`), `sqlite://kiw6` (SQLite), `KeywordSearchVolume/app.py` (standalone), `data/output/output.json` (output file), `file://kiw6` (`file://` URL), `https://cdn.jsdelivr.net/kiw6` (CDN host) — six class injections, each falsifying the exclusion assertion for its class | obsolete-runtime exclusion assertion per class |

6. **Atomicity/durability assertions.** Query durable rows before and after
   publication/handoff/fault partitions; require no partial
   result/selection/Run/RunQuery/domain terminal; queue/S3 state never
   substitutes for Neon readiness; every retry uses durable identity and
   bounded step counters; no cancellation case.
7. **Identities.** Assert exact research, selection revision/fingerprint, Run,
   100 RunQuery, 100 discovery-task, 1,000 stable shop/run-store/lead-task
   sets; derive the expected route from an independently captured response
   `run.runId`.
8. **Certificate.** After every positive/control/scope/cleanup precondition
   passes, emit exactly one line via exactly one emission site
   ``console.log(`KI_W6_CERTIFICATE=${JSON.stringify(certificate)}`);`` with
   IF-4 field order and no secrets. Freeze `operationCounts` as:
   `baseMaximum = {providerCalls:19, providerAttempts:19, keywordObjects:23,
   keywordQueueSends:42, selectedItems:100, runQueries:100,
   googleValidationCalls:100, discoveryTasks:100, googleOccurrences:1000,
   stableDomains:1000, leadTasks:1000}`;
   `corruptArtifactFixture = {providerCalls:2, keywordObjects:2,
   terminalTasks:2, nextStageRows:0}`;
   `missingTerminalFixture = {providerCalls:2, keywordObjects:2,
   terminalTasks:1, nextStageRows:0}`.
   `substituteClaims` is bounded exactly by the A4 "Substitute-fidelity
   ledger" (copy its six boundary rows as literal claims; claim nothing
   beyond).
9. **Obsolete-runtime exclusion.** Build the dependency inventory from exactly
   the A4 T5 item 12 roots (backend: `package.json`,
   `scripts/build-keyword-worker.js`,
   `src/aws-pipeline/keyword-intelligence/handler.js`, `src/server.js`;
   frontend: `package.json`, `app/keywords/page.tsx`,
   `app/keywords/[researchId]/page.tsx`, `app/runs/[runId]/page.tsx`,
   `app/api/keyword-research/route.ts`,
   `app/api/keyword-research/[researchId]/route.ts`,
   `app/api/keyword-research/[researchId]/selection/route.ts`,
   `app/api/keyword-research/[researchId]/runs/route.ts`, and
   `app/api/keyword-research/[researchId]/export.csv/route.ts`). Recursively
   resolve every literal relative or `@/` import/export/dynamic import to
   `.js/.mjs/.ts/.tsx/.json/.css`; record bare package names from the two
   package files; fail any nonliteral local dynamic import or unresolved
   local edge. Scan that derived set with the frozen literal pattern lists
   `const FORBIDDEN_RUNTIME_HOSTS = ["cdn.jsdelivr.net", "unpkg.com", "cdnjs.cloudflare.com"];`
   and
   `const FORBIDDEN_LOCAL_PATH_PATTERNS = [".py", "sqlite", "KeywordSearchVolume", "data/raw", "data/output", "output.json", "file://"];`
   Provider URLs in backend adapters are not CDN hits. The standalone project
   is outside the roots and never scanned. **Frozen comment-stripping rule
   (parent decision (b) recorded in `EV-KI-W6-R21`; applies to this scan
   only):** before either pattern list is applied to a resolved member's
   contents, strip comments — `.css` members lose non-greedy `/* … */`
   block comments; `.js/.mjs/.ts/.tsx` members lose the same block
   comments plus full-line `//` line comments (optional leading
   whitespace, line-anchored, so protocol separators inside strings are
   never touched); every other file (including `.json`) is scanned
   verbatim; member paths are matched unstripped. The rule is implemented
   by the single helper
   `const stripComments = (filePath, text) => …` applied at both content
   checks inside `obsoleteExclusion` (`S105-C12`).
10. **Privacy.** Screenshots and review files are forbidden
    (`Page.captureScreenshot` never sent; no `review-evidence` writes).
    Temporary logs live under one `mkdtemp` directory and are deleted only by
    the step-13 cleanup order (before certificate emission). Record wall time
    and peak child RSS without inventing a new acceptance ceiling.
11. **Viewports.** One Chrome process, one desktop and one mobile viewport
    within the same run (`setViewport` pattern). One schema for the whole run;
    created by the harness and verified absent through the `close()` positive
    absence witness.
12. **Physical causal action order (frozen; `EV-KI-A-083` `F9`;
    injection points per A4 `KI-CL-20` T3 item 10 / `EV-KI-A-084` `F12` /
    `EV-KI-A-085` `F13`).**
    The run executes exactly this physical sequence; all durable state and
    provider work is produced here exactly once:
    1. harness creation (schema, auth server, backend server, owners A/B);
    2. Next build (unless skipped) and `next start`; Chrome launch; owner-A
       session;
    3. browser: create research with the five seeds through `/keywords`
       (`W6-FLOW-01/02` witnesses captured here); initialization queues the
       expansion tasks/checks;
    4. **keyword fault partition (`W6-RES-02` keyword half):** immediately
       after initialization has queued expansion tasks/checks, apply
       `duplicate-next-keyword-message` then
       `reorder-pending-keyword-messages` on the nonempty keyword queue,
       then `await harness.restartBackend();` (restart A, retaining
       DB/S3/SQS);
    5. harness: `drainKeywordWork("expansion")`, then `("anchor-screen")`,
       then `("markets")` — the 19 provider calls, 23 keyword objects, and
       42 base keyword queue sends happen exactly once here despite the
       duplicated/reordered deliveries (production idempotency absorbs
       them; fault deliveries add no dispatcher send traces);
    6. browser: reload completed research desktop+mobile (`W6-FLOW-06`);
       stale save, conflict resolution, exact saved 100-item draft
       (`W6-FLOW-07`);
    7. browser: handoff (`W6-FLOW-08`, `W6-NAV-01`; the `W6-NAV-02`
       response-stage abort/retry and `W6-NAV-03` hostile-`statusUrl`
       assertions use this same single handoff partition);
    8. browser: run-workspace edit/reorder of all 100 queries
       (`W6-FLOW-09`) and confirmation (`W6-FLOW-10`: the 100 Google
       validations happen exactly once here through the injected validator
       and the production probe path);
    9. **discovery fault partition (`W6-RES-02` discovery half):**
       immediately after confirmation dispatches the 100 discovery
       deliveries, apply `duplicate-next-discovery-message` then
       `reorder-pending-discovery-messages` on the nonempty discovery
       queue;
    10. harness: `drainDownstream()` begins (`W6-FLOW-11/12`: 100 discovery
        tasks, 1,000 stable domains/lead tasks exactly once); **domain-check
        fault partition (`W6-RES-02` domain-check half):** after the first
        discovery emits a domain check, apply
        `duplicate-next-domain-check-message` then
        `reorder-pending-domain-check-messages` on the nonempty check queue
        before completing the drain;
    11. **post-handoff snapshot partition (`W6-FLOW-13`):** while owner A is
        still active, capture the immutable Run/100-RunQuery projection,
        mutate the live research selection, invoke
        `await harness.restartBackend();` (restart B, retaining DB/S3/SQS),
        reload the durable run projection, and require it byte/deep equal to
        the captured snapshot while the research revision may advance;
        only after that comparison run the remaining resilience partitions:
        owner-B switch + emitted-Next restart and no-session restart
        (`W6-RES-01`), then the two separate one-seed fixtures
        (`W6-RES-03/04`);
    12. thirteen captured-data controls on the frozen captured state
        (§4 S105 step 5 allocation);
    13. conformance checks (`W6-CONF-01..06`) and certificate assembly.
    The 26 case assertions and certificate registration then execute in
    manifest order against the captured witnesses **without rerunning any
    provider work**; each case's activation witness references its captured
    evidence from the step above that produced it. Every fault partition
    operates on a nonempty queue at its frozen point; an empty-queue fault
    invocation is an oracle failure (`W6-RES-02` forbidden column:
    empty-queue no-op).
13. **Cleanup order (frozen; `EV-KI-A-083` `F9`).** The file freezes the
    literal `const CLEANUP_ORDER = ["browser", "next-server", "auth-server", "backend-server", "schema-absence", "temp-root"];`
    and executes exactly that order in `finally`: close the CDP/Chrome
    browser; terminate the Next child; close the auth and backend servers
    (harness `close()` does servers → schema drop → absence verification →
    Prisma disconnect, returning the positive absence witness); delete the
    `mkdtemp` temporary artifact root; and only after every cleanup step
    succeeded (or an error is being propagated) emit the sole
    `KI_W6_CERTIFICATE=` line and exit 0. A cleanup failure (including
    `HarnessCleanupError`) prevents certificate emission and exits nonzero
    with the failure recorded in the final diagnostics line.

**Exact checks (`LOCAL_NOW`; build/browser/database all deferred).**

| ID | Exact command (from workspace root) | Expected result |
|---|---|---|
| S105-C1 | `node --check frontend/test/browser/keyword-intelligence-e2e.mjs` | exit 0 |
| S105-C2 | `grep -cF 'KI_W6_CERTIFICATE=' frontend/test/browser/keyword-intelligence-e2e.mjs` | exactly `1` (sole emission site; the literal appears only inside the single `console.log` line) |
| S105-C3 | `grep -cF 'const port = 4357;' frontend/test/browser/keyword-intelligence-e2e.mjs` | exactly `1` |
| S105-C4 | `grep -cF 'const FORBIDDEN_RUNTIME_HOSTS = ["cdn.jsdelivr.net", "unpkg.com", "cdnjs.cloudflare.com"];' frontend/test/browser/keyword-intelligence-e2e.mjs` and `grep -cF 'const FORBIDDEN_LOCAL_PATH_PATTERNS = [".py", "sqlite", "KeywordSearchVolume", "data/raw", "data/output", "output.json", "file://"];' frontend/test/browser/keyword-intelligence-e2e.mjs` | exactly `1` each |
| S105-C5 | `grep -cF '../../../email_scraper/test/helpers/keyword-intelligence-e2e-harness.js' frontend/test/browser/keyword-intelligence-e2e.mjs` and `grep -cF 'ki-w6-enforcement-manifest-v1.json' frontend/test/browser/keyword-intelligence-e2e.mjs` | exactly `1` each |
| S105-C6 | `grep -cE 'Page.captureScreenshot|review-evidence' frontend/test/browser/keyword-intelligence-e2e.mjs` | 0 occurrences (exit 1) |
| S105-C7 | `grep -cF 'KI_W6_SKIP_BUILD' frontend/test/browser/keyword-intelligence-e2e.mjs` and `grep -cF 'ALLOW_DATABASE_TESTS' frontend/test/browser/keyword-intelligence-e2e.mjs` | exactly `1` each |
| S105-C8 | `grep -cF 'kiw6-local-e2e-cookie-secret-0000000000000000000000' frontend/test/browser/keyword-intelligence-e2e.mjs` | 0 occurrences (exit 1; the secret literal exists only in the harness and must never be copied into the certificate emitter) |
| S105-C9 | `grep -cF 'const CLEANUP_ORDER = ["browser", "next-server", "auth-server", "backend-server", "schema-absence", "temp-root"];' frontend/test/browser/keyword-intelligence-e2e.mjs` | exactly `1` |
| S105-C10 | `grep -cF 'absenceWitness' frontend/test/browser/keyword-intelligence-e2e.mjs` | exactly `1` (the e2e asserts the harness positive absence witness) |
| S105-C11 | `grep -cF 'await harness.restartBackend();' frontend/test/browser/keyword-intelligence-e2e.mjs` | exactly `2` (restart A and restart B; neither causal point may be omitted or merged) |
| S105-C12 | `grep -cF 'const stripComments = (filePath, text) =>' frontend/test/browser/keyword-intelligence-e2e.mjs` and `grep -cF 'const content = stripComments(member.path, member.content || "");' frontend/test/browser/keyword-intelligence-e2e.mjs` | exactly `1` each (frozen comment-stripping rule; `EV-KI-W6-R21`) |

`DEFERRED_TO_INTEGRATION`: execution of all 26 cases, 13 controls, digest
recomputation, certificate emission, schema lifecycle assertions — V3 only.

**Completion checklist:** identical P1–H3 list, local coverage = C1–C11; the
leaf claims zero executed behavioral evidence.

---

## 5. Integration assessment `KI-W6-I101` (authored before leaf execution)

```yaml
subwindow_id: KI-W6-I101
type: INTEGRATION_ASSESSMENT
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-02
assigned_agent: KI-W6-WINDOW-AGENT
authorized_write_file: NONE
predecessors: [KI-W6-S101, KI-W6-S102, KI-W6-S103, KI-W6-S104, KI-W6-S105]
```

Personally executed by the window agent after all five leaves are
`ACCEPTED_FOR_INTEGRATION`. Inputs: assembled current window state, actual
diffs, ending digests, leaf evidence. Result: exactly one of `PASS`,
`CORRECTION_REQUIRED`, `PARENT_BLOCKED`.

### 5.1 Frozen gates (exact commands, oracles, witnesses, invalidations)

**V1 — static/manifest conformance and ownership (zero database/build/
browser/network/provider/AWS work).** Run every command from the workspace
root; each must produce exactly its expected result:

| # | Exact command | Expected result |
|---|---|---|
| V1-1 | `node --check email_scraper/test/helpers/keyword-intelligence-e2e-harness.js` | exit 0 |
| V1-2 | `node --check frontend/test/browser/keyword-intelligence-dashboard.mjs` | exit 0 |
| V1-3 | `node --check frontend/test/browser/keyword-intelligence-e2e.mjs` | exit 0 |
| V1-4 | S104-C1 exact command | prints `S104-C1 OK` |
| V1-5 | S104-C2 exact command | prints `S104-C2 OK` |
| V1-6 | S104-C3 exact command | prints `S104-C3 OK` |
| V1-7 | S101-C1, S101-C2, S101-C3, S101-C4 exact commands | 0 / `2` / `529` / `2 inserted, 2 deleted` |
| V1-8 | S102-C1 through S102-C6 exact commands | exit 0 / 0 / `1` / `1` / `26` / `8 inserted, 4 deleted` |
| V1-9 | `git -C email_scraper status --porcelain` | exactly two lines: `?? test/fixtures/keyword-intelligence/ki-w6-enforcement-manifest-v1.json` and `?? test/helpers/keyword-intelligence-e2e-harness.js` |
| V1-10 | `git -C frontend status --porcelain` | exactly three lines: ` M components/keyword-intelligence/research-dashboard.tsx`, ` M test/browser/keyword-intelligence-dashboard.mjs`, `?? test/browser/keyword-intelligence-e2e.mjs` |
| V1-11 | S103-C1 through S103-C16 exact commands | `1`/`1`/`1`/0/`1`/`1`/`1`/`1`/`1` each/0/`1`/`1`/`1`/`1` each/`1` each/`1` each/`1` per the S103 table |
| V1-12 | S105-C1 through S105-C12 exact commands | exit 0 / `1` / `1` / `1` each / `1` each / 0 / `1` each / 0 / `1` / `1` / `2` / `1` each per the S105 table |

Invalidation: any edit to any of the five owned files.

**V2 — sole production Next build.** From `frontend/`: `npm run check` once
(lint && test && build). Expected exit 0; `.next` output preserved for V3.
Invalidation: any edit to frontend source/config/package or either frontend
browser file; backend helper/manifest-only edits do not invalidate.

**V3 — single emitted causal browser/isolated-schema gate.** From `frontend/`:

```text
ALLOW_DATABASE_TESTS=true KI_W6_SKIP_BUILD=1 node test/browser/keyword-intelligence-e2e.mjs
```

run once with the environment-provided `TEST_DATABASE_URL` (present and
validated in this workspace; the harness itself resolves it through
`resolveDirectTestDatabaseUrl` and refuses a URL whose database identity
equals `DATABASE_URL`, so no URL is embedded in this command). Sandbox
escalation per §0.2 when loopback/network/Chrome privilege requires it.
Expected: exit 0; stdout contains exactly one `KI_W6_CERTIFICATE=` line whose
JSON shows required=registered=executed=activated 26-ID equality, zero
skipped/duplicates/unexpected/unactivated, 13/13 controls with
pass→mutated-fail→fresh-pass, four group digests and the global digest equal
to the `DEC-KI-038` literals, `operationCounts` equal to the §4 S105 step 8
literals, `obsoleteRuntimeHits` empty, and no secrets. The certificate line
must be the **last** substantive stdout line, emitted only after the full
`CLEANUP_ORDER` succeeded (§4 S105 step 13): the run's final diagnostics
record the harness `close()` positive absence witness
`{ droppedSchema: <kiw6_ schema>, absenceWitness: { query:
SCHEMA_ABSENCE_QUERY, rowCount: 0 } }` proving exactly one `kiw6_` schema
was created and is absent, and the temporary artifact root deletion.
Invalidation: any edit to any of the five owned files; proven
environment/channel invalidation follows the standing identical-recovery rule
(§0.2).

**V4 — backend regression and secret scan.** From `email_scraper/`:
`npm test` once and `npm run check:secrets` once. Expected: zero failures;
guarded database suites remain skipped without opt-in; secret scan clean.
Invalidation: backend production/test/fixture/package change invalidates
`npm test`; any owned-file change invalidates the secret scan.

**V5 — window-agent read-only recomputation.** No command rerun: recompute
from actual artifacts/traces the 26-ID/group/global certificate values,
five-path set/digest, starting→ending hashes, substitute-claim ceiling vs the
A4 ledger, exact operation counts, and obsolete-runtime inventory; require
byte-equality with the V3 certificate and the frozen literals.

**V6 — unchanged-dependency proof (exact hashes and path sets).** Run every
command from the workspace root; each must produce exactly its expected
result:

| # | Exact command | Expected result |
|---|---|---|
| V6-1 | `git -C email_scraper diff --name-only 0083a42c5582aeb8d9d8998e8ce9e1cc1d52b43e -- . ':(exclude)test/helpers/keyword-intelligence-e2e-harness.js' ':(exclude)test/fixtures/keyword-intelligence/ki-w6-enforcement-manifest-v1.json'` | empty output (no tracked backend file outside the two W6 paths changed; untracked files never appear in diff) |
| V6-2 | `git -C frontend diff --name-only 70fb5edfcfe092ca8d153bb025116b96cf1897b3 -- . ':(exclude)components/keyword-intelligence/research-dashboard.tsx' ':(exclude)test/browser/keyword-intelligence-dashboard.mjs'` | empty output |
| V6-3 | `git -C frontend diff --numstat 70fb5edfcfe092ca8d153bb025116b96cf1897b3 -- test/browser/keyword-intelligence-dashboard.mjs` | exactly `8	4	test/browser/keyword-intelligence-dashboard.mjs` (all R5 evidence unchanged except the one superseded R5-FIN-01 destination oracle, whose exact diff is S102's) |
| V6-4 | `sha256sum email_scraper/src/aws-pipeline/keyword-intelligence/contracts.js email_scraper/src/aws-pipeline/keyword-intelligence/dataforseo-labs-adapter.js email_scraper/src/aws-pipeline/keyword-intelligence/handler.js email_scraper/src/aws-pipeline/keyword-intelligence/keys.js email_scraper/src/aws-pipeline/keyword-intelligence/recovery.js email_scraper/src/aws-pipeline/keyword-intelligence/service.js email_scraper/scripts/build-keyword-worker.js` | all seven hashes equal the pinned table below, line for line |

V6-4 pinned worker-packaging closure (accepted W3/R4 packaging inputs; hashes
recorded under A5 state 143 in `EV-KI-W6-R04` and re-verified unchanged under states 144/145 in `EV-KI-W6-R06`/`R08`):

| Path (relative to `email_scraper/`) | Pinned sha256 |
|---|---|
| `src/aws-pipeline/keyword-intelligence/contracts.js` | `e37b38d6129204127f9b2aa25779162ab6d8ea32e24be391fd04cac3ddcb7b29` |
| `src/aws-pipeline/keyword-intelligence/dataforseo-labs-adapter.js` | `dcdac7f40e7775bd5cb80b6fc4f513e482a6f79207fba20af4c4a213c486ccd1` |
| `src/aws-pipeline/keyword-intelligence/handler.js` | `c6a38b0bb4adf19058b53b9e24b0ae3308f590a8d2eb387ca82d1bb0ab16c414` |
| `src/aws-pipeline/keyword-intelligence/keys.js` | `8327f0b116f5092011485c1fb29854b201a965382ede380fae9f191fb47b4c46` |
| `src/aws-pipeline/keyword-intelligence/recovery.js` | `3fcf9b47c5def5ef2729fe7c844661fd17919978ec0f64156de29ac1050a14f0` |
| `src/aws-pipeline/keyword-intelligence/service.js` | `c37a038f189470ad1d2eca6626f515b9f0c45bd60de470d84c4b72fa497637b5` |
| `scripts/build-keyword-worker.js` | `0667c6b40e9bc2d92759fe17d86ccfed51f9d1d0647aaeb5dbc91a66a3b1b935` |

V6 prohibits: handler build, full W5 browser suite, full database integration,
Prisma generate/validate, duplicate frontend build. Invalidation: any diff in
a compared path.

Gate scheduling is risk-proportionate: V1 after all leaves freeze; V2 once;
V3 once against V2's `.next`; V4 after V3; V5/V6 read-only. After any
correction, rerun every gate whose inputs/paths/fixtures/substitutes/artifacts
changed, every final-frozen gate (V2, V3, V4), and the complete scope,
coverage-set, secret/privacy, and regression closure; unaffected costly gates
may reuse prior evidence only with a recorded deterministic dependency proof.

### 5.2 Mandatory integration checklist

- [ ] I1 Verify all listed file and corrective sub-windows were independently accepted.
- [ ] I2 Verify actual assembled changed files equal the planned five-path set (digest `d28ae178…`) and the planned set is contained by parent-authorized scope.
- [ ] I3 Verify complete requirement and decision traceability to current source and assertions (A4 T1–T5 items → S101–S105 → matrix rows → witnesses).
- [ ] I4 Execute all frozen applicable whole-window gates V1–V6 with activation witnesses.
- [ ] I5 Verify required = registered = executed = activated coverage sets (26 IDs), matching group/global digests, zero skips/duplicates/unexpected/unactivated.
- [ ] I6 Execute all thirteen negative controls and verify acceptance fails under each prescribed defect before the fresh pass.
- [ ] I7 Verify substitute fidelity (claims within the A4 ledger) and accepted-test/fixture integrity (R5 set unchanged except the one superseded oracle, proven by V6-2/V6-3; W3/R4 packaging evidence reused only by the V6-4 unchanged-hash proof).
- [ ] I8 Verify no prohibited, successor, external, destructive, secret-bearing, or out-of-scope action occurred; the R5-FIN-01 supersession is the only earlier-evidence change.
- [ ] I9 Independently inspect current source and complete diff; do not rely on leaf summaries.
- [ ] I10 Record PASS, CORRECTION_REQUIRED, or PARENT_BLOCKED with decisive evidence.

### 5.3 Oracles

- **PASS:** I1–I10 all satisfied; V1–V6 exact; certificate digests/counts equal
  the frozen literals; diff = subset of the five paths; unrelated dirty state
  byte-identical; `WINDOW-AGENT-INTEGRATION-PASS` appended to `S3`; status
  `READY_FOR_PARENT_REVIEW`; A5/A6/A7/A8 untouched by the window agent.
- **CORRECTION_REQUIRED:** any failed assertion → §6 correction loop (one-file
  corrective sub-windows + new assessment `KI-W6-I102+`).
- **PARENT_BLOCKED:** missing parent decision, contradiction, or required
  scope expansion → stop and report one exact blocker to the parent.

## 6. Correction and re-assessment rules (append-only)

1. Never reuse any initial, correction, assessment, assignment, or evidence ID;
   corrective IDs are `KI-W6-C101+`, next assessments `KI-W6-I102+`.
2. Never edit a completed sub-window specification to match later code.
3. Never let one corrective agent edit a test and production file together.
4. Never weaken an accepted oracle because current code fails it.
5. Never replace root-cause diagnosis with a timeout/retry/resource/fixture/
   mock change unless the parent decision already prescribes that remedy and
   evidence proves the cause (the unchanged identical sandbox recovery of
   §0.2 is not such a change).
6. Every corrective edit invalidates all evidence whose inputs or asserted
   path include that file; every correction records a new baseline and ending
   digest; the window agent always performs a new integration assessment after
   the last correction.
7. Before assigning any corrective sub-window, append the
   `CORRECTIVE-SUBWINDOW-READY` certificate (sub-window standard §12.2) to
   `S3`; unresolved parent decision or scope expansion requires escalation.

## 7. Mandatory decomposition-readiness checklist

All 47 `SW-*` items are checked with resolvable evidence against this
corrected package (revision recorded in `S2`). `N/A` items: none.

### 7.1 Authority and inheritance

- [x] `SW-A01` Parent assignment, window agent identity, and delegation authority are exact and current. Evidence: A5 state 147 and A4 `KI-CL-20` pins verified on disk (`EV-KI-W6-R12` item 1); `EV-KI-A-082`–`EV-KI-A-086` correction assignments; all pre-state-147 `SW-A01` claims are superseded (§0.1 item 8); delegation authority activates only after parent approval of this package.
- [x] `SW-A02` Parent and sub-window standards plus contract, decision, checklist, and state revisions are pinned and verified. Evidence: §0 table; `EV-KI-W6-R12` item 2 (all recomputed byte-equal against A5 v147 and A4 `8fe18271…`).
- [x] `SW-A03` Parent write, read, action, prohibition, successor, and stop boundaries are copied without expansion. Evidence: §1 (verbatim A4 `KI-CL-20` copy); `EV-KI-W6-R12` item 3.
- [x] `SW-A04` Current repositories, dirty state, and owner-controlled changes are inventoried. Evidence: §2; `EV-KI-W6-R08` item 4.
- [x] `SW-A05` All three subordinate artifacts exist and their authorities do not overlap. Evidence: S1 (DAG/specs), S2 (live status only), S3 (evidence only); cross-references in each header.
- [x] `SW-A06` Strict adjacent communication and no subagent delegation are enforced. Evidence: §4 prohibited lists in every leaf block name both "parent communication" and "spawning or delegating to any other implementation agent"; §8.1 certificate fields (`direct_parent_communication: false`, `successor_work_started: false`); `EV-KI-W6-R13`.
- [x] `SW-A07` The inherited execution-environment policy permits sandbox escalation for authorized local actions without expanding parent authority. Evidence: §0.2 (E8.1 copy); A4 `execution_environment_policy`; `EV-KI-W6-R08` item 5.

### 7.2 Decision and file-set closure

- [x] `SW-D01` Every parent requirement, invariant, decision, task, scenario, and coverage case is allocated to exact files and assertions. Evidence: §3.1 file records; §4 mechanical traces; allocation closure in `EV-KI-W6-R08` item 6 (unmapped counts all zero, including `REQ-KI-014/018`, `EXC-*`, `AUTH-*` → `S105`).
- [x] `SW-D02` No missing parent-level decision or contradictory authority remains. Evidence: `EV-KI-W6-R12` item 6; F3/F6–F13 remain resolved; F14 is resolved by §0.1 item 14, §3 DAG, and every §4 `predecessors` field.
- [x] `SW-D03` Required changed-file set equals planned initial file set. Evidence: §3 closure statement; digest `d28ae178…` recomputed in `EV-KI-W6-R12` item 7 (unchanged in `KI-CL-20`).
- [x] `SW-D04` Every planned file has one initial sub-window and no initial sub-window owns more than one file. Evidence: §3.1/§4 one-to-one mapping F-001..F-005 → S101..S105.
- [x] `SW-D05` Every file operation, starting digest, anchor, interface, preserved behavior, and forbidden edit is exact. Evidence: §3.1 records + §4 blocks; IF-1..IF-4 fully frozen with literal signatures, schemas, unions, drive table, error names, source-real durable projection, provider synthesis, four-value `frontendEnv`, callable logger, eight-fault union, and the exact restart-A/restart-B call sites (F6–F13).
- [x] `SW-D06` The dependency graph is complete, sequential, acyclic, and justified by named outputs. Evidence: §3 DAG + named interfaces IF-1..IF-4 on every edge.
- [x] `SW-D07` Every cross-file interface is frozen before dependent execution. Evidence: §3.3 (IF-1..IF-4 frozen in this S1 before any leaf runs; IF-2 contains literal member signatures, trace/fault unions, server/repository/child-env literals, config/queue/clock/data contracts, the Google per-query expansion contract with production-probe acceptance, the literal provider synthesis, the monotonic-delivery drive table, the eight-fault union with exact nonempty injection points, and the cleanup/absence-witness contract).
- [x] `SW-D08` Every intermediate state has exact permitted checks, expected temporary failures, safety, resolver, and prohibitions. Evidence: §3.2 table.
- [x] `SW-D09` Separate production, test, fixture, schema, configuration, manifest, and generated files have separate sub-windows. Evidence: production `.tsx` (S101) vs browser test (S102) vs backend helper (S103) vs JSON fixture (S104) vs new browser harness (S105) — five separate sub-windows.
- [x] `SW-D10` No rename, multi-output generator, formatter, installer, or command can violate the one-file write invariant. Evidence: §4 blocks run only `node --check`/`grep`/read-only `git`/`node -e` parse-and-print scripts (no workspace writes beyond the writable file); `npm run check`/V2–V4 run only at `I101` by the window agent; `EV-KI-W6-R08` item 8.

### 7.3 Sub-window execution completeness

- [x] `SW-E01` Every file sub-window contains every field in Section 7 of the standard. Evidence: §4 blocks (identity/authority YAML incl. `leaf_assignment_id`, mechanical trace, transformation items 1–12, checks with witnesses, P1–H3 completion checklist; S105 additionally freezes the physical causal order with its fault-injection points (step 12) and cleanup order (step 13)).
- [x] `SW-E02` Every sub-window prescribes exact ordered edits rather than design alternatives or broad verbs. Evidence: §4 (exact bytes, line anchors, ordered steps; exact grep/numstat expected values; no `choose`/`decide`/`as appropriate`/`as needed`/`(or …)` alternatives in any assignable block; `EV-KI-W6-R13` lint).
- [x] `SW-E03` Every sub-window has exact preflight, local checks, activation witnesses, assertions, and forbidden outcomes. Evidence: §4 check tables C1..C9 per leaf with exact commands and expected results; §3.1 dispatch-time starting-set verification.
- [x] `SW-E04` Every sub-window mechanically proves its attributable changed-file set is exactly one file. Evidence: P2/V2 boxes + per-leaf starting change-set digests (§3.1 table) re-verified at dispatch and at handoff.
- [x] `SW-E05` Every sub-window has exact evidence, handoff, stop, and successor-reservation rules. Evidence: H1–H3 boxes; `successor_reserved_for: WINDOW-AGENT` in every block.
- [x] `SW-E06` Each subagent may report only to the window agent and cannot update subordinate or parent authority artifacts. Evidence: §4 prohibited lists (parent communication; spawning/delegation); §8.1 certificate; S2 written only by the window agent.
- [x] `SW-E07` No sub-window requires successor work to satisfy its file-local acceptance. Evidence: §4 local checks are self-contained; deferred items are named per leaf with their integration owner (`I101`).
- [x] `SW-E08` Deliberately deferred checks name the exact integration assessment that owns them. Evidence: `DEFERRED_TO_INTEGRATION` lines in §4; §5.1 gates.

### 7.4 Enforcement and integration closure

- [x] `SW-V01` Coverage cases are allocated to exact test files, registrations, activation witnesses, and assertions. Evidence: §3.1 `coverage_case_ids`; §4 S105 step 4 (26 registrations in manifest order, one witness per case); A4 matrix rows are the literal assertion authority.
- [x] `SW-V02` Required local and whole-window case-set equality and digest checks are prescribed. Evidence: S104-C3 digest scripts; V1-4..V1-6; V3 certificate oracle; I5.
- [x] `SW-V03` Every critical invariant has a negative control assigned at the narrowest effective level. Evidence: §4 S105 frozen control-allocation table (13 controls ↔ 13 invariant classes, one exact mechanism each); `NC-01` targets the S101 routing choice specifically.
- [x] `SW-V04` Test substitutes and accepted tests/fixtures have exact fidelity and invalidation rules. Evidence: A4 substitute ledger copied literally into S105 step 8 `substituteClaims`; I7 invalidation rule for the single superseded R5-FIN-01 oracle, proven by V6-2/V6-3.
- [x] `SW-V05` The initial integration assessment is fully authored with zero implementation-file write authority. Evidence: §5 (`authorized_write_file: NONE`).
- [x] `SW-V06` Frozen gates are exact, risk-proportionate, and scheduled at the final assessment rather than every leaf. Evidence: §5.1 V1–V6 with exact commands, expected outputs, and per-gate invalidation/scheduling rules.
- [x] `SW-V07` Correction diagnosis, one-file corrective assignment, invalidation, and reassessment rules are complete. Evidence: §6.
- [x] `SW-V08` The window agent must independently inspect every file handoff and personally execute every integration assessment. Evidence: §5 header; standard §8/§9 duties restated in §6; leaf certificates cannot self-accept (§8.1).
- [x] `SW-V09` Whole-window approval cannot pass through zero-work, skipped, filtered, duplicate, unexpected, unactivated, or summary-only evidence. Evidence: V3 oracle (set equality + witnesses + exactly one certificate line), I5/I6, §6 rule 6.
- [x] `SW-V10` Parent handoff contents and `READY_FOR_PARENT_REVIEW` boundary are exact. Evidence: §8.2 (12-item consolidated handoff); A4 `KI-W6-H5/H6`.
- [x] `SW-V11` Every local gate distinguishes real failure from proven sandbox/channel invalidation and permits one identical escalated recovery without parent round trip. Evidence: §0.2; V3 note; standard §9.3.1 copied.

### 7.5 Mechanical and adversarial audit

- [x] `SW-R01` All IDs are unique and all references resolve. Evidence: fresh ID series (§0.1 item 1); `EV-KI-W6-R13` audit.
- [x] `SW-R02` No unresolved placeholder exists in a checked item or assignable sub-window. Evidence: `EV-KI-W6-R13` structural audit — no unresolved blank, computed-at-dispatch choice, inequality oracle, ellipsis command, or wildcard read/write scope in assignable content.
- [x] `SW-R03` Single-file write-set lint rejects zero, two, wildcard, directory, rename, and incidental workspace outputs for file sub-windows. Evidence: every §4 block names exactly one literal regular-file path; §4 commands have no workspace write beyond it; §3.2 prohibits builds/generators at leaf level.
- [x] `SW-R04` Removing one required file or requirement-to-file mapping makes readiness fail. Evidence: §3 closure proof breaks if any file/mapping is removed; `EV-KI-W6-R13` counterexample 5.
- [x] `SW-R05` Removing, duplicating, skipping, filtering, or bypassing one required coverage case makes acceptance fail. Evidence: V3 set-equality + digest oracle; `W6-NC-10` falsifies each defect class; `W6-NC-11` falsifies absent activation.
- [x] `SW-R06` Weakening an oracle or diverging a substitute invalidates acceptance evidence. Evidence: `W6-NC-11` (pass/pass/pass control result rejected), `W6-NC-12` (divergent substitute rejected), §6 rule 4.
- [x] `SW-R07` Simulated second-file edit and direct parent communication are rejected. Evidence: per-leaf starting change-set digest verification at dispatch and handoff (§3.1 table, P2/V2); `attributable_changed_file_set` certificate field; `direct_parent_communication: false`; H2 boxes.
- [x] `SW-R08` Simulated integration failure cannot be repaired by the window agent without a new corrective sub-window. Evidence: §5.3 `CORRECTION_REQUIRED` → §6 loop; standard §8 bar on window-agent implementation edits restated in §6.
- [x] `SW-R09` Parent decomposition review is recorded before the first implementation assignment. Evidence: `EV-KI-A-082` (first review, `CORRECTION_REQUIRED`); S2 `decomposition_status: AWAITING_PARENT_DECOMPOSITION_REVIEW` for this corrected package; certificate `parent_review_required: true` in S3.
- [x] `SW-R10` Document lint reports zero missing fields, mappings, cases, evidence references, or authority conflicts. Evidence: `EV-KI-W6-R13` structural audit of this corrected S1.
- [x] `SW-R11` Simulated sandbox denial proceeds to one identical escalated recovery, while a changed command, observable test failure or external action is rejected. Evidence: §0.2 copied E8.1 conditions; V3 recovery note; `EV-KI-W6-R13` counterexamples 21–22.

## 8. Handoff templates

### 8.1 File-subwindow execution certificate (returned by every leaf)

Each leaf returns one certificate with its exact literal IDs. The five
certificates are identified by exactly these fields:

| Leaf | `subwindow_id` | `assignment_id` | `writable_file` |
|---|---|---|---|
| 1 | `KI-W6-S101` | `ASG-KI-W6-S101` | `frontend/components/keyword-intelligence/research-dashboard.tsx` |
| 2 | `KI-W6-S102` | `ASG-KI-W6-S102` | `frontend/test/browser/keyword-intelligence-dashboard.mjs` |
| 3 | `KI-W6-S103` | `ASG-KI-W6-S103` | `email_scraper/test/helpers/keyword-intelligence-e2e-harness.js` |
| 4 | `KI-W6-S104` | `ASG-KI-W6-S104` | `email_scraper/test/fixtures/keyword-intelligence/ki-w6-enforcement-manifest-v1.json` |
| 5 | `KI-W6-S105` | `ASG-KI-W6-S105` | `frontend/test/browser/keyword-intelligence-e2e.mjs` |

Certificate body (fields per sub-window standard §12.3; `agent_identity` is
filled at dispatch with the leaf agent identity the window agent names in S2;
digest and case fields are filled from the leaf's actual execution):

```yaml
certificate: FILE-SUBWINDOW-EXECUTED
parent_window_id: KI-W6
subwindow_id: <one exact ID from the table above>
assignment_id: <one exact ID from the table above>
agent_identity: <assigned leaf agent identity>
writable_file: <one exact path from the table above>
starting_file_digest: <pinned sha256 or ABSENT>
ending_file_digest: <sha256>
starting_repository_change_set_digest: <the leaf's §3.1 table digest>
attributable_changed_file_set: [<the writable path>]
required_local_cases: [<leaf's LOCAL_NOW check IDs>]
registered_local_cases: [<same>]
executed_local_cases: [<same>]
skipped_local_cases: []
duplicate_case_ids: []
unexpected_case_ids: []
missing_activation_witnesses: []
negative_controls_expected: 0        # leaves execute none; controls run at V3
negative_controls_falsified: 0
commands: [<exact commands run, with outcomes>]
deferred_integration_checks: [<per §4 DEFERRED_TO_INTEGRATION>]
external_mutations: []
prohibited_actions_observed: []
successor_work_started: false
direct_parent_communication: false
status: AWAITING_WINDOW_REVIEW
```

The window agent appends a separate review disposition
(`ACCEPTED_FOR_INTEGRATION` / `CORRECTION_REQUIRED` / `PARENT_BLOCKED`) to
`S3` after independently inspecting the diff and evidence (standard §8's
13-point review).

### 8.2 Consolidated parent handoff (window agent → parent, after I-PASS)

Exactly the 12 items of sub-window standard §12.5: `READY_FOR_PARENT_REVIEW`
or one exact blocker; S1/S2/S3 paths and revisions; initial/corrective/
failed-assessment/successful-assessment IDs; expected vs actual changed-file
sets and digests; current file digests; requirement/decision/task/scenario/
coverage trace closure; required/registered/executed coverage counts and
digests; skipped/duplicate/unexpected/unactivated/failed cases; exact
commands, decisive outcomes, negative controls, parity limits; invalidated and
superseded evidence (the R5-FIN-01 destination oracle); external mutations,
costs (`$0.00`), skipped gates, residual risks, user prerequisites; and
confirmation that no successor parent window (KI-W7) began. Subagent summaries
are not forwarded as proof.

## 9. Append-only amendments

### 9.1 Corrective sub-windows

(Reserved. Each future correction appends a `KI-W6-C1xx` block with all §7
fields, its `CORRECTIVE-SUBWINDOW-READY` certificate reference, invalidated
evidence/gates, and new baseline digests. The §4 blocks above are immutable
once this package is parent-approved.)

### 9.2 Later integration assessments

(Reserved. Each future assessment appends a `KI-W6-I1xx` block reusing
unchanged §5.1 gates by exact reference and listing every gate invalidated by
the intervening corrections.)

### 9.3 State-154 literal second-correction transcription (`KI-CL-22`)

This block is a literal operational transcription of A4 `KI-CL-22`'s second
in-flight corrective amendment. It supersedes only C105's scaffold fingerprint
and one-seed SCN-KI-041 fixture shape plus failed I102/CV1. C104 production
source, the existing seven-path W6 scope/digest, 26 case IDs, 13 controls,
frontend-build reuse, causal V3 oracle, provider economics, schemas, and every
public interface remain unchanged. Before dispatch, the window agent certified
same writable file, formulas, checks, order, prohibitions, and gates against
the A4 literal; any divergence, new decision, or scope expansion stops.

#### Task block `KI-W6-CT3` / sub-window `KI-W6-C106`

1. **Task:** correct only the existing component scaffold and SCN-KI-041 so
   their stored identities and maximum candidate shape satisfy the unchanged
   production schemas.
2. **Requirements/decisions:** `REQ-KI-001`, `REQ-KI-002`, `REQ-KI-003`,
   `REQ-KI-023`, `REQ-KI-024`, `INV-KI-004`, `INV-KI-005`, `INV-KI-014`,
   `DEC-KI-024`, `DEC-KI-038`, `DEC-KI-039`, `DEC-KI-040`, `SRC-KI-042`.
3. **Source:** current SHA-256
   `f549f9ac16e2c31957dd3a03b11d54da15972f4af23ebcfecb6f8c16f8955d9f`;
   R28 proves five R3 market cases fail on task-vs-stage fingerprint and
   SCN-KI-041 fails the strict 60-per-seed parser.
4. **Target:** only
   `email_scraper/test/keyword-intelligence-worker-flow.test.js`, limited to
   `aggregationScaffold` support statements and the one existing SCN-KI-041
   block. No other R3/R4 test, registration or assertion changes.
5. **Private interface:** add option `bySeed = null`. Define exactly
   `expansionBySeed = bySeed ?? [{ seed: "seed one", keywords: candidates }]`
   and `seeds = expansionBySeed.map((entry) => entry.seed)`. No export or
   production interface changes.
6. **Stage/task shape:** set expansion-stage expected/terminal/succeeded counts
   to `seeds.length * 2`. Construct exactly two ordered expansion tasks per seed
   in seed-index order, `suggestions` then `related`, using that seed in the
   request and task-input payload. Default callers therefore retain two tasks;
   the maximum fixture has ten.
7. **Expansion manifest:** retain its existing strict schema and stage
   fingerprint. Store `seeds`, `bySeed: expansionBySeed`, and the existing
   ordered `candidates`. Derive each candidate's `seeds` array by scanning
   `expansionBySeed` in seed order and retaining every entry whose exact
   `keywords` array contains that candidate; zero supplying seeds is invalid
   through the existing schema. Do not collapse all candidates to one seed.
8. **Shortlist manifest identity:** after `[anchorTask]` exists, compute exactly
   `anchorStageInputFingerprint = keywordStageInputFingerprint({ researchId,
   generation, stage: "anchor_screen", tasks: [anchorTask] })`. Use that value
   for both `shortlistManifest.inputFingerprint` and the shortlist
   `putImmutable.inputFingerprint`. Keep the anchor task artifact on
   `anchorTask.inputFingerprint`; these identities are deliberately different.
9. **Maximum fixture:** replace the one-seed candidate expression with exactly
   five seeds `seed 1`…`seed 5`. For each seed, its 60-keyword member is
   `[seed, ...59 strings]`, where string `n` is
   `` `${seed} candidate ${String(n + 1).padStart(2, "0")}` `` for zero-based
   `n=0..58`. `candidates = expansionBySeed.flatMap(entry => entry.keywords)`;
   assert five members, every member length 60, candidate length and distinct
   count 300; `shortlist = candidates.slice(0, 200)`.
10. **Scenario assertions:** call the actual production aggregate path with
    `{stage:"market_overview", candidates, shortlist, bySeed: expansionBySeed}`
    and preserve the existing `published`, result 200, default selection 100,
    normalized shortlist equality and zero escaped-key assertions.
11. **Failure/replay/concurrency:** existing R3/R4 outcome, lease, lost-owner,
    replay and no-dispatch cases remain unchanged and must all pass. A task
    fingerprint in the shortlist manifest, one `bySeed` member over 60, wrong
    stage counts, missing provenance, duplicate/leaked result key or changed
    existing assertion fails acceptance.
12. **Operations/bounds:** in-memory test only; five seeds, 60 each, 300
    candidates, 200 shortlist/result, 100 default. Zero database, subprocess,
    HTTP, provider, AWS, production, artifact-file, package or schema write.
13. **Checks:** from `email_scraper/`, run C106-C1
    `node --check test/keyword-intelligence-worker-flow.test.js`, then C106-C2
    `node --test --test-isolation=none test/keyword-intelligence-worker-flow.test.js`.
    Require exit 0, 37 tests pass, zero fail/skip, R3-G11–G15 pass, SCN-KI-041
    executes once, and exact 5/60/300/200/200/100 witnesses. Expected workspace
    write set is empty. The prior 30/7 result cannot be reused.
14. **Output:** corrected test substitute consumed by I103; C105's failed
    fingerprint/one-seed evidence is superseded, while its other accepted
    scaffold work remains.
15. **Non-goals:** no `service.js`, contract, key, config, repository, handler,
    frontend, browser harness, fixture manifest, case ID/digest, timeout,
    provider, database, AWS, commit, push or KI-W7 change.

```yaml
subwindow_id: KI-W6-C106
type: CORRECTION
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-02
assigned_agent: KI-W6-C106-LEAF-AGENT
predecessors: [KI-W6-I102 PARENT_BLOCKED]
successor_reserved_for: WINDOW-AGENT
writable_file: email_scraper/test/keyword-intelligence-worker-flow.test.js
file_operation: MODIFY
starting_file_digest: f549f9ac16e2c31957dd3a03b11d54da15972f4af23ebcfecb6f8c16f8955d9f
starting_repository_change_set_digest: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
read_only_scope: [KEYWORD_INTELLIGENCE_PRODUCT_CONTRACT.md, KEYWORD_INTELLIGENCE_DECISION_LEDGER.md §DEC-KI-040, KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md §KI-W6 second in-flight corrective amendment, ACTIVE_EXECUTION_STATE.md, email_scraper/src/aws-pipeline/keyword-intelligence/service.js::readManifest, email_scraper/src/aws-pipeline/keyword-intelligence/contracts.js::keywordExpansionManifestSchema, email_scraper/src/aws-pipeline/keyword-intelligence/keys.js::keywordStageInputFingerprint]
authorized_actions: [perform KI-W6-CT3 in the one writable file, run C106-C1 and C106-C2 once, return evidence only to the window agent]
prohibited_actions: [second-file edit, existing R3/R4 assertion or registration edit, production schema package config timeout provider database AWS commit push parent communication subdelegation successor or KI-W7 action]
may_start_successor: false
```

- [ ] `C106-P1` Pins, assignment, clean baseline and predecessor match.
- [ ] `C106-P2` The attributable changed-file set is exactly the writable file.
- [ ] `C106-T1` Apply all ordered CT3 transformations and no other edit.
- [ ] `C106-V1` Run C106-C1/C2 once with the exact witnesses and zero skips.
- [ ] `C106-H1` Return diff, ending digest, commands and outcomes to the window agent.
- [ ] `C106-H2` Confirm zero prohibited/external/successor action and stop for review.

#### Integration assessment `KI-W6-I103`

I103 is owned personally by the window agent, writes no implementation file,
and begins only after independent C106 acceptance. It supersedes failed I102
and uses these exact ordered gates:

- [ ] `KI-W6-CV7` From `email_scraper/`, once run
  `node --check src/aws-pipeline/keyword-intelligence/service.js` followed by
  `node --test --test-isolation=none test/keyword-intelligence-worker-flow.test.js`.
  Require 37 pass, zero fail/skip, R3/R4 green and exact SCN-KI-041
  5/60/300/200/200/100 activation.
- [ ] `KI-W6-CV8` Reuse the passed frontend build only if frontend porcelain is
  empty and HEAD remains `a39663c8f99d9cc3c4aa1301ff088d5f4a24e7fd`; otherwise stop for dependency adjudication. Do not rebuild.
- [ ] `KI-W6-CV9` From `frontend/`, once run
  `ALLOW_DATABASE_TESTS=true KI_W6_SKIP_BUILD=1 node test/browser/keyword-intelligence-e2e.mjs`
  with the existing isolated `TEST_DATABASE_URL` sourced without logging.
  Require the unchanged 26-case/13-control certificate, exact 19 calls, 23
  keyword objects, 42 sends, `$0.49200000`, five seeds, 300 anchor, 200
  shortlist/result/UI, default 100, complete cleanup and zero residual schema.
- [ ] `KI-W6-CV10` From `email_scraper/`, once run `npm test`, then
  `npm run check:secrets`; require zero failures and clean scan. Do not opt into
  the full database suite.
- [ ] `KI-W6-CV11` From `email_scraper/`, run
  `node scripts/build-keyword-worker.js` exactly twice; require identical ZIP
  hashes, preserved siblings, no forbidden/stale members, ZIP ≤45 MiB,
  unzipped ≤200 MiB and cold-imported function `handler`; then run once
  `node --test --test-isolation=none test/aws-pipeline-packaging.test.js` with
  zero failures. Do not run seven-handler build/measure.
- [ ] `KI-W6-CV12` Recompute the unchanged seven-path digest, current hashes,
  exact 26-ID/group/global equality, 13 controls, substitute limits, privacy,
  scope and W7 handoff. Require only C104 and the C105/C106-owned test file to
  differ from the five accepted initial hashes and no out-of-scope source.
- [ ] `KI-W6-CH3` Record C106 acceptance, I103 gates, superseded I102 failure,
  requester commit provenance, exact final files/digests and one
  `WINDOW-AGENT-INTEGRATION-PASS` certificate.
- [ ] `KI-W6-CH4` Stop `READY_FOR_PARENT_REVIEW`; do not begin KI-W7.

Sandbox or channel invalidation permits the standing one identical escalated
recovery. An observable product/test failure is not such an invalidation. If
C106 and all I103 gates pass, the window agent continues through CH3/CH4
without another parent prompt. A new decision, scope expansion or unresolved
contract contradiction stops; a mechanically determined same-scope defect uses
the standard's new one-file corrective-subwindow path.

---

End of `S1` (corrected per `EV-KI-A-082`–`EV-KI-A-086`, `F1`–`F14`). Decomposition status and
live assignment state live only in `S2`; execution evidence lives only in
`S3`.

---

## 10. State-149 corrective decomposition (awaiting parent review)

This appendix is authorized solely by A5 state 149 and the pinned
`KI-DD-6` / `KI-DL-15` / `KI-CL-21` / `KI-TR-13` package. It preserves the
accepted five-file history, the exact 26 W6 cases, and all 13 controls. The
only additional parent-scope files are `service.js` and `worker-flow.test.js`;
the seven-path sorted-member-plus-LF digest is
`c3bfe436aba49d52de26298ac74eb30e061d392144dfffbb6954ee792c908bdc`.
No leaf may be assigned until renewed parent decomposition approval.

### `KI-W6-C104` — durable-shortlist final calculation projection

```yaml
subwindow_id: KI-W6-C104
type: CORRECTION
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-02
assigned_agent: UNASSIGNED
predecessors: [KI-W6-I101]
successor_reserved_for: WINDOW-AGENT
writable_file: email_scraper/src/aws-pipeline/keyword-intelligence/service.js
file_operation: MODIFY
starting_file_digest: c37a038f189470ad1d2eca6626f515b9f0c45bd60de470d84c4b72fa497637b5
starting_repository_change_set_digest: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
read_only_scope: [KEYWORD_INTELLIGENCE_PRODUCT_CONTRACT.md, KEYWORD_INTELLIGENCE_DECISION_LEDGER.md §DEC-KI-039, KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md §KI-W6 in-flight corrective amendment — final result shortlist projection, ACTIVE_EXECUTION_STATE.md, email_scraper/src/keyword-intelligence/pipeline.js, email_scraper/src/keyword-intelligence/config.js, email_scraper/src/aws-pipeline/keyword-intelligence/contracts.js, email_scraper/src/aws-pipeline/keyword-intelligence/keys.js, email_scraper/src/aws-pipeline/keyword-intelligence/handler.js, email_scraper/src/aws-pipeline/keyword-intelligence/recovery.js, email_scraper/src/keyword-intelligence/repository.js, email_scraper/test/keyword-intelligence-worker-flow.test.js]
authorized_actions: [modify aggregateMarket only as specified below, run C104 LOCAL_NOW checks, return one certificate to the window agent]
prohibited_actions: [all other service symbols, exports, signatures, callers, contracts, keys, repository, handler, recovery, build, test, fixture, manifest, frontend, schema, config, provider, AWS, production, destructive action, commit, push, parent communication, subdelegation, successor work]
may_start_successor: false
```

**Trace and root cause.** `EV-KI-W6-R20` and the later V3 witness prove that
`aggregateMarket` reads the 300-member expansion manifest and US anchor
artifact, but not the durable shortlist, before `computeResearchResult`.
`REQ-KI-002/003/023/024`, `INV-KI-004/005/014`,
`DEC-KI-006/024/038/039`, `KI-W6-CT1`, `SCN-KI-041`, `W6-FLOW-05`, and
`W6-NC-05` determine the correction; no earlier accepted leaf is rewritten.

**Exact ordered transformation.** At `service.js:979` in `aggregateMarket`,
after the existing validated expansion-manifest read and before the unchanged
calculation: (1) read `anchor_screen` with existing `readManifest`,
`KEYWORD_ARTIFACT_SHORTLIST_MANIFEST`, and
`keywordShortlistManifestSchema`; (2) create the ordered shortlist and
distinct `K` using exactly `keyword.trim().toLowerCase()`; (3) filter every
`bySeed` keyword in original seed/order, retaining shared members under every
original seed; (4) filter US metrics in original order; (5) compute each
filtered input's distinct normalized keys and invoke the existing invariant
failure unless each equals `K`; (6) call the existing calculation with the
projected expansion, projected US metrics, and unchanged eight market arrays.
Keep the existing claim/lease, artifact reads, immutable writes and fenced
publication. The added read remains inside the monitored boundary. Missing,
corrupt, mismatched, or unequal input fails closed before publication; replay,
duplicate, reorder, restart, expired lease and stale-owner behavior remains.
Bounds are shortlist `1..200`, anchor `1..300`, final expansion/US/result
equal to shortlist and at most `200`, selection at most `100`. It adds one S3
read and zero provider calls, sends, attempts, writes, reservations, database
operations, cost, or public/artifact-schema changes. It must not post-truncate,
re-rank, pre-cap, collapse lineage, mutate artifacts, or alter provenance.

For C104-C2's reproducible inspection, the implementation uses these exact
local names: `keywordKey`, `shortlistManifest`, `shortlistKeys`,
`projectedExpansion`, `projectedUsMetrics`, and `projectedOverview`. The
calculation call has the literal members `expansion: projectedExpansion` and
`overview: projectedOverview`; equality failures call `invariant()` before
that call. These names are private to `aggregateMarket` and add no export.

**Intermediate state and checks.** C104 makes production correct but causes
the old scaffold (which supplies no shortlist manifest) to remain incomplete;
only C104 static checks may run before C105. This is local-only and resolved
solely by C105. `C104-C1` (`LOCAL_NOW`): from `email_scraper/`,
`node --check src/aws-pipeline/keyword-intelligence/service.js`, exit 0.
`C104-C2` (`LOCAL_NOW`): from `email_scraper/`, after C104's edit and before
any C105 edit, run exactly:

```sh
node --input-type=module -e 'import { readFileSync } from "node:fs"; import assert from "node:assert/strict"; const s=readFileSync("src/aws-pipeline/keyword-intelligence/service.js","utf8"); const a=s.indexOf("async function aggregateMarket("); const b=s.indexOf("\nasync function failStage(",a); assert.ok(a>=0&&b>a,"aggregateMarket bounds"); const f=s.slice(a,b); const once=(x)=>assert.equal(f.split(x).length-1,1,x); once("KEYWORD_ARTIFACT_SHORTLIST_MANIFEST"); once("keywordShortlistManifestSchema"); for(const x of ["const keywordKey = (keyword) => keyword.trim().toLowerCase();","shortlistManifest","shortlistKeys","projectedExpansion","projectedUsMetrics","projectedOverview","expansion: projectedExpansion","overview: projectedOverview"]) assert.ok(f.includes(x),x); const calc=f.indexOf("computeResearchResult({"); assert.ok(calc>=0,"calculation"); assert.ok(f.indexOf("KEYWORD_ARTIFACT_SHORTLIST_MANIFEST")<calc,"shortlist before calculation"); const guardFor=(projection)=>{ const declaration=f.indexOf(`const ${projection}`); assert.ok(declaration>=0,`${projection} declaration`); const re=new RegExp(`if\\s*\\((?=[^{};]*${projection})(?=[^{};]*shortlistKeys)[^{};]*\\)\\s*\\{?\\s*invariant\\(\\);?\\s*\\}?`,"g"); const matches=[...f.matchAll(re)]; assert.equal(matches.length,1,`${projection} one equality guard`); const guard=matches[0].index; assert.ok(guard>declaration&&guard<calc,`${projection} guard before calculation`); const pre=f.slice(declaration,guard); assert.ok(pre.includes("new Set("),`${projection} normalized set`); assert.ok(pre.includes("keywordKey"),`${projection} normalized key`); return guard; }; const expansionGuard=guardFor("projectedExpansion"); const usMetricsGuard=guardFor("projectedUsMetrics"); assert.notEqual(expansionGuard,usMetricsGuard,"independent equality guards");'
```

Expected result is exit `0`; stdout/stderr is not asserted. Activation is the
bounded function extraction, exactly one shortlist contract/schema member, all
eight required projection members, shortlist-before-calculation order, and two
distinct projection-specific `if (...) invariant()` equality guards. Each guard
must name its own projected input and `shortlistKeys`, follow that projected
input's normalized `new Set`/`keywordKey` construction, and precede
`computeResearchResult`; the pre-existing anchor-context invariant cannot match
either witness. Missing/duplicate members, missing projection, wrong order,
missing/duplicated projection guard, shared guard, or an unnormalized guard
fails. The command is
read-only with expected workspace write set `[]`; it must not run tests,
providers, queues, artifact storage, databases, or builds.
Required=registered=executed IDs `[C104-C1, C104-C2]`; no local control;
`W6-NC-05` is deferred to I102. The inherited one-identical-command sandbox
recovery is allowed only for proven sandbox/channel invalidation.

- [ ] P1 Pins, identity, writable file, baseline, and predecessor evidence match.
- [ ] P2 Protected dirty state matches baseline.
- [ ] T1 Apply the six ordered transformations and no other service edit.
- [ ] V1 Execute C104-C1/C104-C2 with witnesses.
- [ ] V2 Prove the attributable changed set is only `service.js`.
- [ ] V3 Prove local-ID equality with zero skips/duplicates/unexpected IDs.
- [ ] H1 Return diff, ending digest, commands, outcomes, and C105 obligation.
- [ ] H2 Confirm no prohibited/second-file/successor/external/parent action.
- [ ] H3 Stop at `AWAITING_WINDOW_REVIEW`.

### `KI-W6-C105` — aggregation-scaffold shortlist regression

```yaml
subwindow_id: KI-W6-C105
type: CORRECTION
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-02
assigned_agent: UNASSIGNED
predecessors: [KI-W6-C104 ACCEPTED_FOR_INTEGRATION]
successor_reserved_for: WINDOW-AGENT
writable_file: email_scraper/test/keyword-intelligence-worker-flow.test.js
file_operation: MODIFY
starting_file_digest: f0e8be1a29d9ed5d85a657b8e73083f6c603ca30b18121701b3a33a7c1938510
starting_repository_change_set_digest: 55d5f0b43f8cc3466478169f48d23cb546f829f4f597c393c326621f9d7be9e0
read_only_scope: [KEYWORD_INTELLIGENCE_PRODUCT_CONTRACT.md, KEYWORD_INTELLIGENCE_DECISION_LEDGER.md §DEC-KI-039, KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md §KI-W6 in-flight corrective amendment — final result shortlist projection, ACTIVE_EXECUTION_STATE.md, email_scraper/src/aws-pipeline/keyword-intelligence/service.js::aggregateMarket post-C104, email_scraper/src/aws-pipeline/keyword-intelligence/contracts.js, email_scraper/src/aws-pipeline/keyword-intelligence/keys.js]
authorized_actions: [modify aggregationScaffold support symbols and add SCN-KI-041 only, run C105 LOCAL_NOW checks, return one certificate to the window agent]
prohibited_actions: [R3/R4 registration or assertion changes, production edits, existing case-ID membership/digest changes, database fixture, timeout/retry change, frontend, manifest, package, provider, AWS, production, destructive action, commit, push, parent communication, subdelegation, successor work]
may_start_successor: false
```

**Trace and exact transformation.** This sequentially implements
`KI-W6-CT2` / `SCN-KI-041` under `REQ-KI-002/003/023/024`,
`INV-KI-004/005/014`, and `DEC-KI-006/024/038/039`. Its explicit affected
W6 cases are `W6-FLOW-04`, `W6-FLOW-05`, and `W6-FLOW-06`; its explicit
control is `W6-NC-05`. It is supplemental to, never a duplicate registration
of, S105's `W6-FLOW-05`, while `W6-NC-05` remains unchanged. At
`aggregationScaffold` (current line 529), add private `candidates` and
`shortlist` options defaulting to `AGG_CANDIDATES`. Use candidates for the
expansion manifest, anchor request and anchor metrics; use shortlist for all
eight market-task fingerprints and metrics. Store strict
`keyword-shortlist-manifest-v1` at the anchor manifest key with existing
anchor input fingerprint/produced time, assign its key/fingerprint/time to the
anchor stage, and return a private holder of the exact
`publishResearchResult` input without changing the outcome.

For C105-C2's reproducible inspection, the private holder assignment is
exactly `holder.publishedInput = input`; the one additive test contains the
literal identifier `SCN-KI-041`. These names do not change an exported or
production interface.

Add only `SCN-KI-041`: construct
`Array.from({length:300},(_,index)=>` with
`` `seed one candidate ${String(index + 1).padStart(3, "0")}` ``, take
`candidates.slice(0, 200)`, drive actual production aggregation, and assert
`published`, captured result length `200`, normalized
`trim().toLowerCase()` set equality with shortlist, no escaped result key, and
default selection `100`. Existing three-item defaults and R3/R4 lease,
lost-owner, outcome, and no-dispatch assertions remain byte/semantically
preserved. This is in-memory only: zero database, subprocess, HTTP, provider,
AWS, or workspace-artifact write. C105 closes C104's temporary scaffold gap;
the first component execution is CV1 at I102.

**Checks.** `C105-C1` (`LOCAL_NOW`): from `email_scraper/`,
`node --check test/keyword-intelligence-worker-flow.test.js`, exit 0.
`C105-C2` (`LOCAL_NOW`): from `email_scraper/`, after C105's edit, run exactly:

```sh
node --input-type=module -e 'import { readFileSync } from "node:fs"; import assert from "node:assert/strict"; const s=readFileSync("test/keyword-intelligence-worker-flow.test.js","utf8"); const a=s.indexOf("async function aggregationScaffold("); const b=s.indexOf("\nasync function runAggregationCase(",a); assert.ok(a>=0&&b>a,"aggregationScaffold bounds"); const f=s.slice(a,b); for(const x of ["candidates = AGG_CANDIDATES","shortlist = AGG_CANDIDATES","KEYWORD_ARTIFACT_SHORTLIST_MANIFEST","keywordShortlistManifestSchema","anchorStage.manifestS3Key","anchorStage.manifestFingerprint","anchorStage.manifestProducedAt","holder.publishedInput = input"]) assert.ok(f.includes(x),x); assert.equal((s.match(/SCN-KI-041/g)??[]).length,1,"one SCN-KI-041"); const start=s.indexOf("test(\"SCN-KI-041:"); const next=s.indexOf("\ntest(",start+1); const end=next<0?s.length:next; assert.ok(start>=0&&end>start,"SCN-KI-041 test block bounds"); const q=s.slice(start,end); const c=q.replace(/\\s+/g,""); for(const x of ["Array.from({length:300}","candidates.slice(0,200)","assert.equal(holder.publishedInput.result.keywords.length,200)","assert.equal(holder.publishedInput.selectionItems.length,100)","constresultKeys=newSet(holder.publishedInput.result.keywords.map((entry)=>entry.keyword.trim().toLowerCase()))","constshortlistKeys=newSet(shortlist.map((keyword)=>keyword.trim().toLowerCase()))","assert.deepEqual([...resultKeys].sort(),[...shortlistKeys].sort())","assert.equal([...resultKeys].filter((key)=>!shortlistKeys.has(key)).length,0)"]) assert.ok(c.includes(x),x);'
```

Expected result is exit `0`; stdout/stderr is not asserted. Activation is the
bounded scaffold and the one complete `test("SCN-KI-041:...")` block, exactly
one SCN-KI-041, both defaults, strict shortlist manifest, all three anchor-stage
metadata assignments, captured publication input, and literal 300/200/200/100
assertions. Within that one block it requires the exact
`holder.publishedInput.selectionItems.length === 100` assertion and both the
normalized result/shortlist set-equality assertion and the exact zero
`[...resultKeys].filter((key) => !shortlistKeys.has(key)).length` assertion.
Missing members, duplicate scenario, an unbounded/later witness, non-strict
manifest, missing capture, wrong cardinality/default oracle, or a missing
escaped-result-key rejection fails. The command is read-only with expected workspace write set
`[]`; it must not run tests, databases, subprocesses, HTTP, providers, AWS, or
builds. Required=registered=executed `[C105-C1, C105-C2]`, zero
skips/duplicates/unexpected, no local control; I102 owns the suite and
controls. The identical sandbox-recovery policy applies.

- [ ] P1 Pins, identity, writable file, baseline, and C104 acceptance match.
- [ ] P2 Protected dirty state matches the recorded post-C104 baseline.
- [ ] T1 Apply only the scaffold and SCN-KI-041 transformation.
- [ ] V1 Execute C105-C1/C105-C2 with witnesses.
- [ ] V2 Prove the attributable changed set is only `worker-flow.test.js`.
- [ ] V3 Prove local-ID equality with zero skips/duplicates/unexpected IDs.
- [ ] H1 Return diff, ending digest, commands, outcomes, and I102 obligation.
- [ ] H2 Confirm no prohibited/second-file/successor/external/parent action.
- [ ] H3 Stop at `AWAITING_WINDOW_REVIEW`.

### `KI-W6-I102` — corrected integration assessment

```yaml
subwindow_id: KI-W6-I102
type: INTEGRATION_ASSESSMENT
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-02
assigned_agent: KI-W6-WINDOW-AGENT
predecessors: [KI-W6-C104 ACCEPTED_FOR_INTEGRATION, KI-W6-C105 ACCEPTED_FOR_INTEGRATION]
authorized_write_file: NONE
assembled_set_digest: c3bfe436aba49d52de26298ac74eb30e061d392144dfffbb6954ee792c908bdc
invalidated_gates: [CV1, CV3, CV4, CV5, CV6]
reusable_gate: CV2 only with its complete-input proof
prohibited_actions: [implementation edit, leaf delegation, KI-W7, provider, AWS, production, destructive action, commit, push, full opted-in DB suite, Prisma generate/validate, seven-handler build/measure, duplicate frontend build]
may_start_successor: false
```

I102 personally accepts C104/C105, verifies the seven-file scope,
requirement→decision→file→subwindow→assertion trace, exact unchanged
26-case/13-control membership, substitute fidelity, privacy and all
prohibitions. It then executes the frozen `KI-CL-21` schedule exactly:

- CV1: once from `email_scraper/`, `node --check src/aws-pipeline/keyword-intelligence/service.js` and `node --test --test-isolation=none test/keyword-intelligence-worker-flow.test.js`; zero failures, SCN-KI-041 activation, exact 300/200/200/100, R3/R4 green.
- CV2: reuse passed frontend `npm run check` only with empty frontend porcelain and HEAD `a39663c8f99d9cc3c4aa1301ff088d5f4a24e7fd`; do not rebuild.
- CV3: one corrected frozen V3 emitted-browser/isolated-schema run: unchanged 26/13 certificate, 19/23/42/`$0.49200000`, 300 anchor, 200 shortlist, 200 durable/UI rows, default 100, complete cleanup, zero residual schema.
- CV4: once each from `email_scraper/`, `npm test` and `npm run check:secrets`; zero failures and clean scan.
- CV5: exactly two `node scripts/build-keyword-worker.js` runs; identical ZIP hashes, preserved siblings, no forbidden/stale members, ZIP <=45 MiB, unzipped <=200 MiB, cold import exports `handler`; then one `node --test --test-isolation=none test/aws-pipeline-packaging.test.js` with zero failures.
- CV6: recompute seven-path digest/current hashes, exact 26-ID group/global equality, 13 controls, substitute limits, privacy and W7 handoff; five non-C104/C105 hashes equal the five KI-CL-21 literals and no out-of-scope source differs.

Every gate requires witnesses; the thirteen controls include W6-NC-05
pass→fail→fresh-pass. Later edits rerun only affected/dependent gates. One
identical escalated recovery is permitted solely for proven sandbox/channel
invalidation. `PASS` requires I1–I10 and ends `READY_FOR_PARENT_REVIEW`;
failed behavior is `CORRECTION_REQUIRED`; missing decision/scope is
`PARENT_BLOCKED`.

- [ ] I1 Independently accept all listed leaf/corrective evidence.
- [ ] I2 Verify actual assembled set equals the parent-authorized seven paths.
- [ ] I3 Verify complete traceability to current source and assertions.
- [ ] I4 Execute CV1–CV6 with exact witnesses/outcomes.
- [ ] I5 Verify required=registered=executed coverage with zero defects.
- [ ] I6 Execute all controls and verify their required falsifications.
- [ ] I7 Verify substitute/accepted-test integrity and CV2 reuse proof.
- [ ] I8 Verify no prohibited, successor, external, destructive, secret, or scope action.
- [ ] I9 Independently inspect source and complete diff.
- [ ] I10 Record PASS, CORRECTION_REQUIRED, or PARENT_BLOCKED in S3.
