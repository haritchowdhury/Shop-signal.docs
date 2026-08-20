# KI-W6 Reauthored Sub-Window Evidence (`S3`)

Append-only evidence for `KI-W6` under assignment `ASG-KI-W6-WA-02`.
Entries never amend a task, decision, or authority boundary. Actor identities:
`KI-W6-WINDOW-AGENT` (decomposition author, reviewer, integration assessor)
and per-leaf agents `KI-W6-S101-AGENT` … `KI-W6-S105-AGENT` (none dispatched
yet). The invalidated state-108 package (`ASG-KI-W6-WA-01`,
`EV-KI-W6-S01/02`, `KI-W6-S001/S002/I001`) is immutable history; nothing here
reuses or cites it as proof.

Companion artifacts: `S1`
(`KEYWORD_INTELLIGENCE_KI_W6_REAUTHORED_SUBWINDOW_CHECKLIST.md`, final
authoring-session revision
`e7893e49930321c911def84082d6ce7a243a154e7bab644e2b73ee25bec12868`; see
`EV-KI-W6-R03`) and `S2`
(`KEYWORD_INTELLIGENCE_KI_W6_REAUTHORED_SUBWINDOW_STATE.md`).

---

## `EV-KI-W6-R01` — Decomposition authoring and entry-gate verification

- **Timestamp:** 2026-08-20T21:08:37+05:30
- **Parent window / assignment:** `KI-W6` / `ASG-KI-W6-WA-02`
- **Actor/role:** `KI-W6-WINDOW-AGENT` (decomposition author)
- **Frozen revisions at authoring (all recomputed on disk this session and
  byte-equal to `A5` state 142):** parent standard
  `cda352017e75c0d11f6797d9fbe108b4365508cd38b0e92365cfb523ede32848`;
  sub-window standard
  `84e7590e74589f308c70dc9b0b67f7e9da395fafb1e5786202ecd1ca15be56e9`;
  contract `8b17f85c…8522c`; decision ledger `ef415367…dbd31`; checklist
  `02352344…123e2`; `A5` file `5d082c2b…2363b`.
- **Entry-gate verification (sub-window standard §3):**
  1. **Assignment current and names this window agent.** Basis is the
     requester's explicit session instruction assigning `KI-W6-WINDOW-AGENT`
     to decompose `KI-W6` and create exactly the three `REAUTHORED`
     artifacts. On-disk `A5` v142 records `accepted_through: KI-R5`,
     `next_window: KI-W6`, `may_start_successor: false`,
     `current_status: READY`, `stop_after: KI-R5`. `CHG-KI-056`
     `authorization_effect` requires an explicit parent A5 CAS to record the
     assignment; that CAS is recorded in S1 §0.1 item 8 as a parent-owned
     prerequisite before `decomposition_status` may become `READY`. No leaf
     is assigned before parent decomposition review in any case.
  2. **Delegation authorized** (A4 `assigned_agent_policy:
     parent_assigns_one_window_agent_only`; `authorized_actions` includes
     sequential per-leaf delegation of exactly one listed file).
  3. **Revision pins match** (table above).
  4. **Parent window READY for decomposition** (`A5` `standard_adoption`
     line: KI-R5 accepted and KI-W6 parent-authored READY under the pinned
     standards; recomputation duty satisfied by the table above).
  5. **Exact scopes known and copied unexpanded** (S1 §1).
  6. **Every implementation-affecting decision exists:** `DEC-KI-038` (all
     nine paragraphs), A4 `KI-W6` header + `KI-W6-T1`–`T5` items 1–15 each,
     the authoritative 26-case coverage matrix, the 13-control table, the
     six-row substitute-fidelity ledger, the frozen V1–V6 schedule, H1–H6,
     and `SCN-KI-018` were all read and allocated; unmapped counts:
     requirements 0, invariants 0, exclusions 0, authority rules 0,
     decisions 0, tasks 0, scenarios 0, coverage cases 0, controls 0,
     interfaces 0, substitutes 0 (`REQ-KI-014/018`, `EXC-KI-001`–`008`,
     `AUTH-KI-001`–`004/006`–`007` allocated to `KI-W6-S105` per the
     "all product requirements/invariants/exclusions" scope of A4 `KI-W6-T5`
     item 2 and `DEC-KI-038`).
  7. **Expected changed files derived from current source and parent
     trace:** five A4-pinned paths; three verified `ABSENT`; the two existing
     files' digests recomputed byte-equal to the A4 pins
     (`19494a99…c6337` 529 lines; `d30bed66…9c398` 2220 lines); five-path
     sorted-member-plus-LF digest recomputed equal to
     `d28ae17864073639580d7650bb03c03474d5370a5034b632cf412e1e3cf3d0bb`.
  8. **Dirty tree inventoried without modification:** `email_scraper` clean
     at `0083a42c5582aeb8d9d8998e8ce9e1cc1d52b43e`; `frontend` clean at
     `70fb5edfcfe092ca8d153bb025116b96cf1897b3`; coordination root porcelain
     = 44 tracked-modified lines, zero untracked, digest
     `28522160bc6c3ffd5a7640dd85fa7d16bdf643b4b91842949934169e68742324`
     (owner-controlled relocation state preserved; this window adds only the
     three `REAUTHORED` artifacts).
  9. **No unrelated owner-controlled change will be overwritten** (all leaf
     writes target the five pinned paths; both nested repositories start
     clean).
  10. **No required action exceeds parent authority** (local-only; frozen
      gate schedule V1–V6 exactly as A4 `KI-W6-V1`–`V6`; E8.1 escalation
      copied into S1 §0.2 and S2).
- **Preflight coverage (A4 `KI-W6-P1`–`P6`):**
  - `KI-W6-P1` — hashes/version/status recomputed above; `A5` assigns only
    `KI-W6-WINDOW-AGENT` after the parent CAS recorded in S1 §0.1 item 8,
    with `accepted_through:KI-R5`, `may_start_successor:false`, and the exact
    coordination-only write scope (the three `REAUTHORED` artifacts).
  - `KI-W6-P2` — five-file digest recomputed exactly
    `d28ae17864073639580d7650bb03c03474d5370a5034b632cf412e1e3cf3d0bb`; no
    duplicate/missing/unowned path (one initial owner each); unrelated dirty
    root relocation state preserved (44-line digest above).
  - `KI-W6-P3` — installed Next route-handler/env/testing guides present
    under `frontend/node_modules/next/dist/docs/` (Next `16.2.12` installed);
    Node `v24.14.1`; Chrome `146.0.7680.164`;
    `resolveDirectTestDatabaseUrl()` from `test/helpers/isolated-postgres.js`
    ran successfully this session proving `TEST_DATABASE_URL` is set with a
    database identity distinct from `DATABASE_URL` (direct non-pooler host);
    planned schema is one non-`public` disposable `kiw6_` schema via
    `assertSafeDisposableSchema`. No database connection or build occurred
    during decomposition (the resolver is pure URL string logic).
  - `KI-W6-P4` — `SRC-KI-038` reproduced at the pinned baselines: backend
    `src/server.js:695` builds `` `/api/runs/${encodeURIComponent(run.id)}` ``;;
    both dashboard success branches currently navigate to
    `handoff.statusUrl` (`research-dashboard.tsx:266` and `:300`, exact two
    occurrences of `router.push(handoff.statusUrl)`, zero others); the UI
    workspace route is `app/runs/[runId]/page.tsx` (33 lines, validates
    `RUN_ID_PATTERN`, renders `<RunWorkspace runId>`).
  - `KI-W6-P5` — complete sequential one-file-leaf DAG authored for exactly
    the five paths (S1 §3), exact interfaces frozen (S1 §3.3), one
    zero-implementation-write integration assessment authored (S1 §5); all
    47 `SW-*` boxes checked with evidence (S1 §7); no leaf assigned.
  - `KI-W6-P6` — one registration per literal W6 case frozen (S1 §4 S105
    step 4; manifest literal in S104), all thirteen controls frozen (S1 §4
    S105 step 5 + A4 controls table), certificate transport frozen (IF-4),
    cleanup ownership frozen (harness `close()`; e2e `finally`;
    schema-absence assertion), invalidation-specific gate schedule frozen
    (S1 §5.1 invalidation column); unresolved requirement/decision/task/
    case/interface/control/substitute/evidence counts all zero.
- **Digest computations (sorted distinct UTF-8 members + LF, `LC_ALL=C`):**
  five-path planned set `d28ae178…3d0bb`; `navigation` 3-ID group
  `103df26205674ddd7f4e7548b3432ea7f5342096bd369991e067debf7f3bf6f2`;
  `flow` 13-ID group
  `14aa36ae942fc9eedef7d9fae9ae0a42775f6ab22c04e3dabb2cf1cbe9379461`;
  `resilience` 4-ID group
  `fc83e2c68fcd67e1849b955b3a9e48fe7a998aed1f1ac0ad6c0f943efeea354d`;
  `conformance` 6-ID group
  `b8180b2f2561d41298252db30b075d4184da3535af065a29f0273e12392c5646`;
  26-ID global
  `d81bab26bc5aadd19c162156c13890611b2fc5a6d0dcb917234453d568ffb4d4`;
  empty starting change set
  `e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855`.
  All group/global digests equal the `DEC-KI-038` literals.
- **Verified source anchors used by the leaf specs** (read-only; captured for
  leaf mechanical trace): dashboard anchors `research-dashboard.tsx:266,300`
  and import block `:7-13`; R5-FIN-01 block
  `keyword-intelligence-dashboard.mjs:1769-1787` with fixture assignment
  `:1778` and pathname assertion `:1785`, fixture run
  `run_kiw5_finalize_000000000001` (`makeRunStatus` `:366`), exactly two
  occurrences of `ki-r5-fin-nav-witness` in the file, 26 `runScenario`
  registrations, symbols `hostileStatusPath`/`workspacePath` unused;
  `RunHandoff` envelope `parseRunHandoffEnvelope`
  (`lib/keyword-intelligence-validation.ts:775-782`, exact keys
  `["run","statusUrl"]`); `startKeywordResearchRun`
  (`lib/client-api.ts:99-113`); backend `statusUrl` (`src/server.js:695`);
  `createLeadServer(config, options)` (`src/server.js:1457`, `schedule`
  option `:1471`, consumption `:1654`, HTTP server `:2177-2206`);
  `isolated-postgres.js` exports (`:20,:25,:54,:62,:91,:123`);
  keyword worker exports (`processKeywordMessage`
  `service.js:247`, `processInitialize` `:255`, `handler.js:9`, keys module,
  adapter `executeProviderAttempt` `dataforseo-labs-adapter.js:170` with HTTP
  call `:245-250`); worker-test patterns (drain `:181-201`, `memoryS3`
  `:40-74`, `memoryDispatcher` `:76-91`, `keywordHttp` `:149-162`,
  `nowBox` fixed clock `:358`, `withIsolatedDb` `:270-282`);
  `aws-pipeline-e2e-harness.js` (artifact store `:68-114`, dispatcher
  `:115-137`, `preloadLead` `:199-218`, drain routing `:247-268`,
  `runUntilSettled` `:271-322`); downstream services
  (`processDiscoveryMessage` `discovery-worker.js:37`,
  `processDomainAggregation` `domain-aggregator.js:36`,
  `dispatchConfirmedQueries` `confirmed-query-dispatcher.js:8`);
  `validateResearchBackedConfirmedQueryRows` (`src/query-review.js:341`,
  `searchPage` option `:345-351`); `parseGoogleSearchResponse`
  (`src/search.js:50`); raw Google fixture
  `test/fixtures/providers/google/custom-search-v1-success.json`;
  identity helpers (`stableShopIdentity` `:175`, `shopIdForStableKey`
  `:308`, `runStoreId` `:313` of `src/shop-persistence-contract.js`);
  W5 browser-harness patterns (build/start `:1071-1087`, Chrome launch
  `:1089-1097`, `Cdp` `:829-870`, helpers `:872-1060`, cleanup
  `:2207-2220`); frontend env/auth (`lib/backend-proxy.ts:28-38`,
  `lib/auth/server.ts:15-32`, `NEON_AUTH_COOKIE_SECRET` ≥32 chars);
  frontend scripts (`check` = lint && test && build; `test` glob excludes
  `test/browser/**`); eslint config has no `test/browser` ignore (V2 lints
  all three browser files).
- **Artifacts authored:** S1 (1140 lines, revision
  `a74ebef90a84451d7ced65934a067073f71269c470b97ec4e92962dfb0611ad0`), S2
  (this state, `AWAITING_PARENT_DECOMPOSITION_REVIEW`), this S3.
- **External mutations/cost:** three coordination files created at the
  workspace root; nothing else; `$0.00`; no provider/AWS/production/
  database/destructive/commit action.
- **Disposition:** decomposition authored; readiness audit follows
  (`EV-KI-W6-R02`).

---

## `EV-KI-W6-R02` — Readiness completion and self-falsification

- **Timestamp:** 2026-08-20T21:08:37+05:30
- **Actor/role:** `KI-W6-WINDOW-AGENT` (readiness audit)
- **Checklist completion:** all 47 `SW-*` items in S1 §7 carry resolvable
  references to S1 sections or to `EV-KI-W6-R01/R02`; zero unchecked; zero
  `N/A`.
- **Structural document lint (SW-R10):** S1 contains exactly five initial
  file sub-window blocks, each with all standard §7 fields (identity/
  authority YAML, mechanical trace, 11-field transformation program, exact
  check table, P1–H3 completion checklist); one §5 integration assessment
  with I1–I10, V1–V6 gates and three-result oracle; §6 correction rules; §8
  handoff templates; §9 append-only amendments. No unresolved placeholder in
  any assignable block; ID references resolve (S101–S105, I101, C101+ series,
  IF-1..IF-4, F-001..F-005).
- **Self-falsification pass (standard §14 counterexamples):**
  1. two writable files in one sub-window — rejected: each §4 block names
     exactly one literal path (SW-R03).
  2. directory/wildcard writable scope — rejected: all five are regular-file
     literals; both existing targets verified regular files at pinned
     digests.
  3. command creates unplanned second workspace file — rejected: leaf
     commands are `node --check`/`grep`/read-only `git`/JSON parse only;
     builds/generators run solely at `I101` (SW-D10, §3.2).
  4. source and separate test file assigned together — rejected: production
     `.tsx` (S101) and its assertion surfaces (S102/S105) are separate
     sequential sub-windows (SW-D09).
  5. required parent file absent — rejected: §3 equality proof (required =
     planned = owned; digest `d28ae178…`); removing any path/file record
     breaks the closure statement.
  6. two initial sub-windows own the same file — rejected: F-001..F-005 map
     1:1 to S101..S105.
  7. dependent begins before interface freeze — rejected: IF-1..IF-4 frozen
     in S1 §3.3 before any dispatch; S102 consumes frozen IF-1, not S101
     execution state.
  8. intermediate state with unexplained failure — rejected: §3.2 defines
     the only permitted latent state (stale R5-FIN-01 oracle between S101
     and S102), why no gate can observe it, its resolver, and prohibitions.
  9. subagent starts successor — rejected: `may_start_successor: false`,
     `successor_reserved_for: WINDOW-AGENT` in every block; H2/H3 boxes;
     only the window agent updates S2 (standard §2.2/§5.5).
  10. subagent → parent communication — rejected: prohibited in every block;
      certificate field `direct_parent_communication: false`.
  11. window agent repairs implementation during review — rejected: §6
      correction loop requires new one-file corrective sub-windows; review
      dispositions are `ACCEPTED_FOR_INTEGRATION`/`CORRECTION_REQUIRED`/
      `PARENT_BLOCKED` only.
  12. integration failure without diagnosed one-file correction — rejected:
      §5.3 `CORRECTION_REQUIRED` → §6 loop with root-cause recording
      (standard §9.5 fields restated).
  13. correction silently rewrites completed sub-window — rejected: §9.1 is
      append-only; §6 rules 1–2.
  14. acceptance omits/skips/duplicates/filters/deactivates a required case —
      rejected: V3 oracle asserts required=registered=executed=activated
      byte-equality with group/global digests; `W6-NC-10` falsifies each
      defect class on synthetic sets; `W6-NC-11` falsifies absent activation.
  15. oracle weakened to fit current behavior — rejected: §6 rule 4;
      `W6-NC-11` rejects pass/pass/pass control results; A4 matrix oracles
      are copied as literal assertions, not derived from code.
  16. substitute over-claims — rejected: `substituteClaims` bounded literally
      by the A4 six-row ledger; `W6-NC-12` falsifies any broadened claim;
      S103 leaf explicitly claims zero behavioral parity.
  17. costly gate repeated without schedule/invalidation rule — rejected:
      §5.1 schedules V2/V3/V4 exactly once each with per-gate invalidation
      and post-correction rerun rules; reuse requires deterministic
      dependency proof.
  18. correction changes file but dependent evidence reused — rejected: §6
      rule 6 invalidates all evidence whose inputs include the corrected
      file.
  19. assembled set ≠ planned set or planned set exceeds parent scope —
      rejected: I2 compares actual diff to the five-path set with digest;
      planned set equals the A4-pinned delegable scope.
  20. window agent claims parent acceptance / starts next window — rejected:
      A4 `KI-W6-H5/H6`; §8.2 ends at `READY_FOR_PARENT_REVIEW`; KI-W7
      prohibited everywhere; S2 records `may_start_successor: false`.
  21. authorized local gate escalated to parent merely for sandbox
      privilege — rejected: S1 §0.2/S2 copy E8.1 standing authorization.
  22. changed command, observable failure, surviving process, or mutation
      accepted as sandbox recovery — rejected: §0.2 conditions; V3 recovery
      note requires read-only postcondition proof and identical command;
      observable product/test failures enter §5.5 correction, not recovery.
- **Predictable requester/parent gates:** parent decomposition review of this
  package (including the S1 §0.1 item 8 A5 CAS) before any leaf dispatch;
  V3 requires the requester-provided isolated `TEST_DATABASE_URL` opt-in
  (already resolving in this environment) and may run under sandbox
  escalation for loopback/network/Chrome per §0.2; commits remain
  requester-only; KI-W7 remains parent-reserved.
- **External mutations/cost:** none beyond the three coordination files;
  `$0.00`.
- **Disposition:** readiness complete; certificate appended below.

---

## Decomposition readiness certificate (sub-window standard §12.1)

```yaml
certificate: SUBWINDOW-DECOMPOSITION-READY
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-02
window_agent_identity: KI-W6-WINDOW-AGENT
revisions:
  parent_standard: cda352017e75c0d11f6797d9fbe108b4365508cd38b0e92365cfb523ede32848
  subwindow_standard: 84e7590e74589f308c70dc9b0b67f7e9da395fafb1e5786202ecd1ca15be56e9
  contract: 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c
  decision: ef4153677807c80dfa9a09c0ffe0ba5a5127681fe6706e17ff6cd48869fdbd31
  parent_checklist: 02352344d5ba940f640463f89bc3011339d6e9f175ca35343abe4e63412523e2
  decomposition: e7893e49930321c911def84082d6ce7a243a154e7bab644e2b73ee25bec12868
initial_subwindow_ids: [KI-W6-S101, KI-W6-S102, KI-W6-S103, KI-W6-S104, KI-W6-S105]
initial_subwindow_count: 5
planned_file_set:
  - email_scraper/test/fixtures/keyword-intelligence/ki-w6-enforcement-manifest-v1.json
  - email_scraper/test/helpers/keyword-intelligence-e2e-harness.js
  - frontend/components/keyword-intelligence/research-dashboard.tsx
  - frontend/test/browser/keyword-intelligence-dashboard.mjs
  - frontend/test/browser/keyword-intelligence-e2e.mjs
planned_file_set_digest: d28ae17864073639580d7650bb03c03474d5370a5034b632cf412e1e3cf3d0bb
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
mandatory_authoring_items_checked: 47
mandatory_authoring_items_unchecked: 0
first_subwindow: KI-W6-S101
integration_assessment_id: KI-W6-I101
parent_review_required: true
```

The window agent stops here. No leaf begins before the parent's decomposition
review (including the parent-owned A5 CAS recorded in S1 §0.1 item 8) and the
window agent's resulting `S2.decomposition_status: READY` transition.

---

## `EV-KI-W6-R03` — Authoring-session environment delta and final revision pins

- **Timestamp:** 2026-08-20T21:16:00+05:30
- **Actor/role:** `KI-W6-WINDOW-AGENT` (authoring-session close-out)
- **Mid-session requester-owned repository actions (outside this window's
  write scope; no window-agent action):** during decomposition authoring the
  requester committed the previously dirty coordination-root artifacts
  (`72ad22a` "docs com", 2026-08-20T21:06:43+05:30) and untracked the nested
  repositories from the coordination root (`03551f0` "Untrack nested
  repositories", 2026-08-20T21:10:24+05:30). Consequently the coordination
  root's owner-controlled 44-line dirty set recorded in `EV-KI-W6-R01` (digest
  `28522160…742324`, captured at inventory time before these commits) is now
  committed history. The current coordination-root porcelain is exactly the
  three untracked `REAUTHORED` artifacts of this window and nothing else;
  `email_scraper` remains at `0083a42c5582aeb8d9d8998e8ce9e1cc1d52b43e` and
  `frontend` at `70fb5edfcfe092ca8d153bb025116b96cf1897b3` (both still clean;
  the untracking commit does not change the nested repositories' own
  baselines). No parent artifact (A1–A8) content changed by these commits
  relative to the pins in `EV-KI-W6-R01`: the pinned artifact revisions were
  recomputed after the commits and remain byte-equal.
- **S1 final authoring revision:** one in-session wording fix to the SW-R02
  evidence line produced the final S1 revision
  `e7893e49930321c911def84082d6ce7a243a154e7bab644e2b73ee25bec12868`
  (superseding the initial `a74ebef90a84451d7ced65934a067073f71269c470b97ec4e92962dfb0611ad0`
  write recorded in `EV-KI-W6-R01`; same authoring session, pre-parent-review,
  no specification change). `S2.decomposition_revision` and the §12.1
  certificate above carry the final revision.
- **External mutations/cost:** none by this window beyond the three
  coordination files; `$0.00`.
- **Disposition:** decomposition package finalized;
  `AWAITING_PARENT_DECOMPOSITION_REVIEW` stands.

---

## `EV-KI-W6-R04` — Parent correction execution (`EV-KI-A-082` `F1`–`F5`)

- **Timestamp:** 2026-08-20T22:05:00+05:30
- **Parent window / assignment:** `KI-W6` / `ASG-KI-W6-WA-02` (A5 state 143,
  CAS 142→143 recorded by the parent in `EV-KI-A-082`)
- **Actor/role:** `KI-W6-WINDOW-AGENT` (correction author)
- **Operative authority:** A5 v143
  (`ACTIVE_EXECUTION_STATE.md` sha256
  `4f3545eafd46353ee39bcafbaf3e2da8c51e777a32526d11938a27267ac17d38`,
  recomputed and byte-equal on disk this session): `KI-W6-WINDOW-AGENT`
  assigned to revise only the three `REAUTHORED` coordination artifacts to
  resolve findings `F1`–`F5`, perform read-only source/standard
  verification, recompute affected pins and readiness claims, append a
  superseding decomposition certificate, and return
  `AWAITING_PARENT_DECOMPOSITION_REVIEW`. All other pins (parent standard
  `cda35201…`, sub-window standard `84e7590e…`, contract `8b17f85c…`,
  decision `ef415367…`, checklist `02352344…`) were recomputed and remain
  byte-equal.
- **F1 resolution (entry authority and pins):** S1 §0 table now pins A5 state
  143 and cites `EV-KI-A-082` as correction authority; S1 §0.1 item 8 records
  the full supersession: the pre-state-143 entry-gate claims and
  `SUBWINDOW-DECOMPOSITION-READY` certificate (in the earlier section of this
  file) were authored while A5 v142 still said `current_window:NONE` /
  `assigned_agent:UNASSIGNED` and are **superseded unapproved-draft claims**,
  not authority. S1 §2 was recomputed under state 143 (both nested
  repositories clean at `0083a42c…`/`70fb5edf…`; coordination root carries
  only the three untracked `REAUTHORED` artifacts after the requester's
  `72ad22a`/`03551f0` commits recorded in `EV-KI-W6-R03`). `SW-A01` evidence
  now cites state 143. S2 carries `parent_state_revision` and states the
  correction boundary.
- **F2 resolution (S102 arithmetic):** recounted the prescribed
  transformation hunk by hunk: comments −2/+3, +1 `const hostileStatusPath`,
  assignment line −1/+1, +1 `const workspacePath`, `waitFor` line −1/+1,
  +1 `assert` ⇒ exactly **8 inserted / 4 deleted**; the hostile literal
  `run_kiw5_hostile_status_witness0001` appears exactly **once** (the
  declaration; the added assertion references the variable). S102-C3 now
  expects exactly `1`; S102-C6 now expects exactly `8 inserted, 4 deleted`;
  the same corrected values are encoded in V1-8 and V6-3. Transformation and
  one-oracle-only ownership unchanged.
- **F3 resolution (harness interface/execution completeness and sendMany):**
  S1 §3.3 IF-2 is now fully frozen: exact export signature with defaults;
  exact `return Object.freeze({…})` literal; per-member contracts for all 11
  members (frontendEnv keys and secret literal, owner literals, `trace()`
  with the complete discriminated `TraceEvent` union, `setAuthOwner` modes,
  `drainKeywordWork(stage)` with literal stage filters and report schema,
  `restartBackend` same-port rebinding, `drainDownstream`, `readDurableState`
  with the exact `DurableStateSnapshot` schema, `injectCapturedDefect` with
  the exact `FaultId`/`FaultOutcome` unions and semantics, `close` with
  `{droppedSchema}`); exact error names (`HarnessPreflightError`,
  `HarnessStallError`); exact runtime config/queue/secret literals; clock
  start/advance rules; deterministic seeds/host template/`TASK_COSTS`/
  `SCHEMA_PREFIX`; and the exact message-type-to-public-function drive table
  with step ceilings (500 keyword / 3,000 downstream) and the named functions
  the harness must never call. "as needed" is removed. The production
  contradiction is corrected: verified this session that production calls
  `dispatcher.sendMany` at `src/aws-pipeline/services/confirmed-query-dispatcher.js:43`,
  `domain-aggregator.js:187`, `lead-aggregator.js:112`, and
  `services/recovery.js:39`; S1 §0.1 item 9 and IF-2 now require the memory
  dispatcher to implement **both** `sendOne` and `sendMany`, with `sendMany`
  expanding into one individual delivery record per message (no `itemIds`
  batch contract), enforced at creation via the frozen
  `const DISPATCHER_METHODS = ["sendMany", "sendOne"];` assertion (S103-C8).
- **F4 resolution (placeholders, non-executable checks, delegation):** all
  wildcard (`**`) read scopes replaced with exact file and named-directory
  lists (S103/S105 `read_only_scope`); every
  `starting_repository_change_set_digest: computed at dispatch` replaced with
  the assignment-time computed digests recorded in the S1 §3.1 table
  (`d1349d2e…`, `fbfdac4a…`, `b94659a0…`, `dc48365f…`; formula verified by
  recomputation this session); S104-C2/C3/C4 are now exact executable
  `node -e` scripts with printed `OK` markers; all `≥1` expectations replaced
  with exact counts (S103-C2..C9, S105-C2..C8); the S105 pseudo-checks are
  now exact single greps with expected `1`/`0`; the host-template check uses
  the exact frozen generator literal (S103-C5); the V3 command is literal
  with no `<validated isolated URL>` placeholder (the harness performs the
  URL resolution/assertion itself, so no credential is embedded); the
  certificate emission site is exactly one (S105-C2, V3 single-line oracle);
  every leaf block's `prohibited_actions` now explicitly includes "spawning
  or delegating to any other implementation agent"; §8.1 now enumerates the
  five exact certificate IDs (no `S1xx` placeholders).
- **F5 resolution (frozen V1/V6 and control mechanisms):** V1 is now ten
  exact commands with exact expected outputs (V1-1..V1-10), including the
  exact expected `git status --porcelain` line sets for both repositories;
  V6 is now four exact commands with expected outputs: non-W6 diff-empty
  proofs for both repositories against the pinned commits with literal
  pathspec exclusions (V6-1/V6-2), the superseded-oracle-only numstat `8 4`
  (V6-3), and a literal seven-file `sha256sum` command over the accepted
  W3/R4 worker-packaging closure with the pinned hash table (V6-4; hashes
  computed this session under A5 state 143 and recorded in S1 §5.1). The
  phrases "accepted W3/R4 worker packaging inputs", "all R5 evidence", and
  "all downstream non-W6 source" are replaced by those executable proofs.
  Each of the thirteen controls is allocated to exactly one mutation
  mechanism in the frozen S105 control-allocation table (captured-data
  substitution/removal/flip/addition, synthetic-record injection, synthetic-
  set injections with per-class sub-injections for `W6-NC-10/13`); the
  remaining alternative "or" was removed (the A4 `W6-NC-02` "or" resolved to
  the single auth-witness-removal mechanism; `W6-NC-11` to the single
  activation-witness removal). Exactly one `KI_W6_CERTIFICATE=` emission site
  is required before the V3 runtime single-line oracle.
- **Digest recomputations this session (sorted distinct UTF-8 members + LF,
  `LC_ALL=C`):** five-path set `d28ae178…3d0bb` (unchanged); per-leaf
  starting change sets as in the S1 §3.1 table; all four group digests and
  the global digest re-verified equal to the `DEC-KI-038` literals; empty set
  `e3b0c442…`; V6-4 closure hashes computed and pinned.
- **Artifacts produced:** corrected S1 (1506 lines, revision
  `c1771d1e994e520202cf165c27ff8586a69fd9dea48393568cbc2e6753c7e372`,
  recorded in S2), S2 state v2, this S3 entry.
- **External mutations/cost:** none beyond the three coordination files;
  `$0.00`; no implementation, leaf, test, build, browser, database, provider,
  AWS, destructive, commit/push, or KI-W7 action (per A5 v143 prohibitions).
- **Disposition:** corrections applied; superseding readiness audit follows
  (`EV-KI-W6-R05`).

---

## `EV-KI-W6-R05` — Superseding readiness completion and self-falsification

- **Timestamp:** 2026-08-20T22:05:00+05:30
- **Actor/role:** `KI-W6-WINDOW-AGENT` (superseding readiness audit)
- **Supersession scope:** this entry and the certificate below supersede the
  readiness claims of `EV-KI-W6-R01` (item 1's entry-gate basis and item 4's
  `SW-A01` basis) and all of `EV-KI-W6-R02`'s `SW-A06`, `SW-D05`, `SW-D07`,
  `SW-E02`, `SW-E03`, `SW-R02`, `SW-R10` citations against the superseded
  draft, together with the earlier `SUBWINDOW-DECOMPOSITION-READY`
  certificate in this file (decomposition revision `a74ebef9…`, later
  re-pinned `e7893e49…`). Those remain as unapproved-draft history.
- **Checklist completion against the corrected package (S1 revision
  `c1771d1e994e520202cf165c27ff8586a69fd9dea48393568cbc2e6753c7e372` per S2):** all 47
  `SW-*` items in S1 §7 carry resolvable references to corrected S1 sections
  or to `EV-KI-W6-R04`/`R05`; zero unchecked; zero `N/A`. The eight items the
  parent named (`SW-A06`, `SW-D05`, `SW-D07`, `SW-E02`, `SW-E03`, `SW-R02`,
  `SW-R10`, plus `SW-A01`) are re-justified: `SW-A06` by the per-leaf
  spawning/delegation prohibitions; `SW-D05` by exact anchors plus the
  assignment-time digest table; `SW-D07` by the fully frozen IF-2 (literal
  member schemas, unions, drive table); `SW-E02`/`SW-E03` by exact-count
  executable checks; `SW-R02`/`SW-R10` by the structural lint below.
- **Structural document lint (re-run on the corrected S1):** five initial
  file sub-window blocks, each with all standard §7 fields plus
  `leaf_assignment_id`; one §5 assessment with I1–I10, V1–V6 exact commands
  and three-result oracle; §6 correction rules; §8.1 five exact certificate
  IDs; §9 append-only amendments. Machine grep confirms: zero `**` wildcard
  in any read/write scope (remaining `**` are markdown emphasis), zero
  `computed at dispatch`, zero `≥1`, zero `as needed`, zero `(or …)`
  alternative in assignable content (the only matches are the SW-R02/SW-E02
  evidence lines quoting the banned patterns as absent), zero `___`, zero
  `S1xx`, zero `sendMany`-never-used claim. All ID references resolve.
- **Self-falsification re-run (standard §14 counterexamples):** the corrected
  package rejects all 22 counterexamples previously recorded in
  `EV-KI-W6-R02` with these strengthened rejections — counterexample 3
  (unplanned second file): leaf commands are now fully enumerated exact
  commands with no workspace write; counterexample 7 (dependent before
  freeze): IF-2 is now literally complete including the drive table;
  counterexample 14 (case-set defects): `W6-NC-10` now has its five exact
  sub-injection mechanisms; counterexample 16 (substitute divergence):
  `W6-NC-12`'s single mechanism is frozen; counterexample 17 (costly gate
  repetition): V6-1..V6-4 are exact commands with per-gate invalidation;
  counterexamples 21–22 unchanged from §0.2.
- **Predictable parent gates:** parent decomposition review of this corrected
  package and an A5 CAS recording approval before `S2.decomposition_status:
  READY` and any leaf dispatch; V3 later requires the environment
  `TEST_DATABASE_URL` opt-in (present) and sandbox escalation per §0.2;
  commits remain requester-only; KI-W7 remains parent-reserved.
- **External mutations/cost:** none beyond the three coordination files;
  `$0.00`.
- **Disposition:** superseding readiness complete; certificate appended
  below.

---

## Superseding decomposition readiness certificate (sub-window standard §12.1)

This certificate supersedes the earlier `SUBWINDOW-DECOMPOSITION-READY`
certificate in this file (draft revision `a74ebef9…`, re-pinned
`e7893e49…`), which was authored before the A5 state-143 assignment existed
and is retained above as unapproved-draft history only.

```yaml
certificate: SUBWINDOW-DECOMPOSITION-READY
supersedes: initial certificate at draft revisions a74ebef90a84451d7ced65934a067073f71269c470b97ec4e92962dfb0611ad0 and e7893e49930321c911def84082d6ce7a243a154e7bab644e2b73ee25bec12868
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-02
window_agent_identity: KI-W6-WINDOW-AGENT
correction_authority: EV-KI-A-082 (A5 state 143)
revisions:
  parent_standard: cda352017e75c0d11f6797d9fbe108b4365508cd38b0e92365cfb523ede32848
  subwindow_standard: 84e7590e74589f308c70dc9b0b67f7e9da395fafb1e5786202ecd1ca15be56e9
  contract: 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c
  decision: ef4153677807c80dfa9a09c0ffe0ba5a5127681fe6706e17ff6cd48869fdbd31
  parent_checklist: 02352344d5ba940f640463f89bc3011339d6e9f175ca35343abe4e63412523e2
  parent_state: 4f3545eafd46353ee39bcafbaf3e2da8c51e777a32526d11938a27267ac17d38
  decomposition: c1771d1e994e520202cf165c27ff8586a69fd9dea48393568cbc2e6753c7e372
initial_subwindow_ids: [KI-W6-S101, KI-W6-S102, KI-W6-S103, KI-W6-S104, KI-W6-S105]
initial_subwindow_count: 5
planned_file_set:
  - email_scraper/test/fixtures/keyword-intelligence/ki-w6-enforcement-manifest-v1.json
  - email_scraper/test/helpers/keyword-intelligence-e2e-harness.js
  - frontend/components/keyword-intelligence/research-dashboard.tsx
  - frontend/test/browser/keyword-intelligence-dashboard.mjs
  - frontend/test/browser/keyword-intelligence-e2e.mjs
planned_file_set_digest: d28ae17864073639580d7650bb03c03474d5370a5034b632cf412e1e3cf3d0bb
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
parent_findings_unresolved: []
mandatory_authoring_items_checked: 47
mandatory_authoring_items_unchecked: 0
first_subwindow: KI-W6-S101
integration_assessment_id: KI-W6-I101
parent_review_required: true
```

The window agent stops here. No leaf begins before the parent approves this
corrected package (including any parent A5 CAS recording that approval) and
the window agent's resulting `S2.decomposition_status: READY` transition.

---

## `EV-KI-W6-R06` — Second parent correction execution (`EV-KI-A-083` `F6`–`F9`)

- **Timestamp:** 2026-08-20T22:40:00+05:30
- **Parent window / assignment:** `KI-W6` / `ASG-KI-W6-WA-02` (A5 state 144,
  CAS 143→144 recorded by the parent in `EV-KI-A-083`)
- **Actor/role:** `KI-W6-WINDOW-AGENT` (second correction author)
- **Operative authority:** A5 v144
  (`ACTIVE_EXECUTION_STATE.md` sha256
  `55454efafe549dae352a015d2ec7b4528085888f0ff31d9854405dbd7e5583b9`,
  recomputed and byte-equal on disk this session): revise only the three
  `REAUTHORED` artifacts to resolve `F6`–`F9`, read-only verification,
  recompute pins, append superseding certificate, return
  `AWAITING_PARENT_DECOMPOSITION_REVIEW`. All other parent pins (standards,
  contract, decision, checklist) recomputed byte-equal. Both nested
  repositories re-verified clean at `0083a42c…`/`70fb5edf…`.
- **F6 resolution (queue progression and duplicate delivery):** verified the
  aggregate-check schema at
  `src/aws-pipeline/keyword-intelligence/contracts.js:87-93` —
  `{contractVersion, type, researchId, generation, stage,
  stageInputFingerprint?}` with no task natural ID/input fingerprint —
  confirming body-dedupe would collapse repeated aggregation checks. S1
  §0.1 item 9 now freezes the monotonic `deliveryId` model (single harness
  counter at enqueue; `sendMany` expands to one delivery record per message);
  IF-2 member 5 now defines each stage's exact stop condition
  (`"expansion"` consumes initialize + expansion tasks + their aggregation
  checks and stops with the anchor overview delivery queued and unconsumed);
  the drive paragraph removes the dedupe key entirely and invokes the
  production handler exactly once per pending delivery, including
  intentionally duplicated/reordered bodies — production idempotency absorbs
  duplicates. Ceilings restated as handler invocations (500/3,000).
- **F7 resolution (source-real configuration and projection):** verified
  `prisma/schema.prisma` — `model Run` (line 130) has no `runIntentId`;
  the replay identity lives on `model KeywordResearchHandoff` (line 730:
  `runId @unique`, `clientRequestId`, `selectionRevision`,
  `selectionFingerprint`, `@@unique([researchId, clientRequestId])`).
  `DurableStateSnapshot.run` now projects only real fields
  (`id/state/phase/stage/queries count/confirmedQueryRevision/
  queriesConfirmedAt/executionBackend/resultsAvailable`) plus a separate
  `handoff` projection. IF-2 adds the exact literal server config object
  (never `loadConfig()`; the only `config.*` members `src/server.js`
  touches), frozen `createLeadServer` options (`now` pinned to the fixed
  clock, FIFO `schedule`, `leaseOwner: "kiw6-lease-owner"`,
  `leaseDurationMs: 90000`, `heartbeatIntervalMs: 20000`,
  `recoveryIntervalMs: 15000` (default verified `src/server.js:188`),
  harness-controlled `setIntervalFn`/`clearIntervalFn` that never auto-fire,
  no-op frozen logger), the exact `PrismaRunRepository` construction with the
  accepted `awsProviderConfigSnapshot` recipe literals
  (`aws-pipeline-end-to-end.integration.test.js:67-74`; validation verified
  at `src/prisma-run-repository.js:595-625`), and the exact child-process
  env allowlists (`next start`: PATH/HOME/NODE_ENV=production + the three
  `frontendEnv` values only; `next build`: PATH/HOME only; Chrome:
  inherited). Cookie-secret length corrected to 51 characters (recounted).
- **F8 resolution (Google expansion and discovery causality):** verified the
  fixture contains exactly one item (`kind: "customsearch#search"`, item
  keys `title/link/snippet/displayLink`) and executed the frozen per-query
  transformation read-only through production `parseGoogleSearchResponse`:
  clone payload, replace `items` with ten items whose `link` is
  `https://w6-q<q pad3>-r<r pad2>.myshopify.com/` (all other fields cloned),
  call the parser with the received query — observed ten results, zero
  rejections, host `w6-q001-r01.myshopify.com`. The transformation is frozen
  in IF-2 ("Google per-query expansion contract"); S103 step 4 now forbids
  preloading (`preloadLead` never imported; S103-C10 greps zero) because the
  production discovery worker creates the 100 query artifacts from parsed
  `probeResults` (`src/aws-pipeline/services/discovery-worker.js:84`)
  through the actual dispatch chain.
- **F9 resolution (causal order, cleanup proof, exact dependencies):** S105
  step 12 freezes the eleven-step physical causal action order (harness →
  build/start/Chrome → browser research create → keyword drains → reload/
  selection → handoff/navigation → workspace edit/confirm → downstream
  drain → resilience partitions → controls → conformance) with the 26 case
  assertions executing in manifest order against captured witnesses without
  rerunning provider work. IF-2 member 10 and S105 step 13 freeze the
  cleanup contracts: `close()` drops the schema, verifies absence **before**
  disconnecting via the frozen `SCHEMA_ABSENCE_QUERY` (S103-C11), throws
  `HarnessCleanupError` (S103-C12) on residual presence, and returns the
  positive `{droppedSchema, absenceWitness:{query, rowCount: 0}}` witness;
  the e2e executes the frozen `CLEANUP_ORDER` (browser → next-server →
  auth-server → backend-server → schema-absence → temp-root; S105-C9) before
  the sole certificate emission, asserts the absence witness (S105-C10), and
  a cleanup failure prevents certificate emission and exits nonzero. V3's
  oracle now requires the certificate as the last substantive stdout line
  emitted only after cleanup, with the absence witness in the final
  diagnostics. All directory-level read scopes replaced with literal files:
  S103 lists the three DataForSEO case fixtures individually plus every
  named service/module file; S105 lists the ten
  `components/keyword-intelligence/*` files, `run-workspace.tsx`,
  `query-editor.tsx`, and the exact Next doc files
  (`01-app/01-getting-started/15-route-handlers.md`,
  `01-app/02-guides/environment-variables.md`, `docs/index.md`).
  V1 gains rows V1-11 (S103-C1..C12) and V1-12 (S105-C1..C10).
- **Digest recomputations:** five-path set `d28ae178…3d0bb` unchanged;
  per-leaf starting change-set digests unchanged (both repositories still
  clean at the pinned baselines); manifest group/global digests re-verified
  equal to the `DEC-KI-038` literals.
- **Artifacts produced:** corrected S1 (1710 lines, revision
  `2ea48e27d47ddc0824285471877e4897b3740c16516f0b1abea81cb79b77bb4c`,
  recorded in S2 state v3), this S3 entry.
- **External mutations/cost:** none beyond the three coordination files;
  `$0.00`; no implementation, leaf, test, build, browser, database,
  provider, AWS, destructive, commit/push, or KI-W7 action (per A5 v144
  prohibitions).
- **Disposition:** corrections applied; superseding readiness audit follows
  (`EV-KI-W6-R07`).

---

## `EV-KI-W6-R07` — Second superseding readiness completion and self-falsification

- **Timestamp:** 2026-08-20T22:40:00+05:30
- **Actor/role:** `KI-W6-WINDOW-AGENT` (second superseding readiness audit)
- **Supersession scope:** this entry and the certificate below supersede the
  DECOMP-2 readiness claims of `EV-KI-W6-R05` and its certificate
  (decomposition revision `c1771d1e…`), which remain as unapproved-draft
  history together with all DECOMP-1 claims.
- **Checklist completion against DECOMP-3 (S1 revision
  `2ea48e27d47ddc0824285471877e4897b3740c16516f0b1abea81cb79b77bb4c` per
  S2 state v3):** all 47 `SW-*` items in S1 §7 carry resolvable references
  to the corrected S1 sections or to `EV-KI-W6-R06`/`R07`; zero unchecked;
  zero `N/A`.
- **Structural document lint (re-run on DECOMP-3):** five initial blocks
  with all standard §7 fields; V1–V6 exact commands (V1 now twelve rows);
  §8.1 five exact certificate IDs; append-only §9. Machine grep confirms:
  zero directory-level read scopes, zero `computed at dispatch`, zero `≥1`,
  zero `as needed`, zero `___`, zero `S1xx`, zero `55 characters`, zero
  `runIntentId` outside its explicit prohibition note, zero dedupe-key
  sentence, zero `preloadLead` instruction outside its prohibition and
  zero-occurrence check. All ID references resolve; the F6–F9-relevant
  literals (`deliveryId`, `SCHEMA_ABSENCE_QUERY`, `CLEANUP_ORDER`,
  `absenceWitness`, `HarnessCleanupError`, `51 characters`) each appear in
  both the frozen interface and a leaf check or gate.
- **Self-falsification re-run (standard §14):** all 22 counterexamples
  remain rejected; strengthened for DECOMP-3 — counterexample 8
  (unexplained intermediate failure): the anchor-queued stop condition makes
  the `"expansion"` drain's terminal state observable and asserted;
  counterexample 16 (substitute divergence): the Google expansion was proven
  against the production parser read-only before freezing; counterexample 17
  (costly gate repetition): V1-11/V1-12 enumerate the new leaf checks
  exactly; counterexample 19 (assembled-set divergence): unchanged digests
  re-verified under state 144.
- **Predictable parent gates:** parent decomposition review of DECOMP-3 and
  an A5 CAS recording approval before `S2.decomposition_status: READY` and
  any leaf dispatch; V3 later requires the environment `TEST_DATABASE_URL`
  opt-in (present) and sandbox escalation per §0.2; commits remain
  requester-only; KI-W7 remains parent-reserved.
- **External mutations/cost:** none beyond the three coordination files;
  `$0.00`.
- **Disposition:** second superseding readiness complete; certificate
  appended below.

---

## Second superseding decomposition readiness certificate (sub-window standard §12.1)

This certificate supersedes both earlier `SUBWINDOW-DECOMPOSITION-READY`
certificates in this file (DECOMP-1 at revisions `a74ebef9…`/`e7893e49…` and
DECOMP-2 at `c1771d1e…`), which are retained above as unapproved-draft
history only.

```yaml
certificate: SUBWINDOW-DECOMPOSITION-READY
supersedes: certificates at draft revisions a74ebef90a84451d7ced65934a067073f71269c470b97ec4e92962dfb0611ad0, e7893e49930321c911def84082d6ce7a243a154e7bab644e2b73ee25bec12868, and c1771d1e994e520202cf165c27ff8586a69fd9dea48393568cbc2e6753c7e372
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-02
window_agent_identity: KI-W6-WINDOW-AGENT
correction_authority: [EV-KI-A-082 (A5 state 143), EV-KI-A-083 (A5 state 144)]
revisions:
  parent_standard: cda352017e75c0d11f6797d9fbe108b4365508cd38b0e92365cfb523ede32848
  subwindow_standard: 84e7590e74589f308c70dc9b0b67f7e9da395fafb1e5786202ecd1ca15be56e9
  contract: 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c
  decision: ef4153677807c80dfa9a09c0ffe0ba5a5127681fe6706e17ff6cd48869fdbd31
  parent_checklist: 02352344d5ba940f640463f89bc3011339d6e9f175ca35343abe4e63412523e2
  parent_state: 55454efafe549dae352a015d2ec7b4528085888f0ff31d9854405dbd7e5583b9
  decomposition: 2ea48e27d47ddc0824285471877e4897b3740c16516f0b1abea81cb79b77bb4c
initial_subwindow_ids: [KI-W6-S101, KI-W6-S102, KI-W6-S103, KI-W6-S104, KI-W6-S105]
initial_subwindow_count: 5
planned_file_set:
  - email_scraper/test/fixtures/keyword-intelligence/ki-w6-enforcement-manifest-v1.json
  - email_scraper/test/helpers/keyword-intelligence-e2e-harness.js
  - frontend/components/keyword-intelligence/research-dashboard.tsx
  - frontend/test/browser/keyword-intelligence-dashboard.mjs
  - frontend/test/browser/keyword-intelligence-e2e.mjs
planned_file_set_digest: d28ae17864073639580d7650bb03c03474d5370a5034b632cf412e1e3cf3d0bb
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
parent_findings_unresolved: []
mandatory_authoring_items_checked: 47
mandatory_authoring_items_unchecked: 0
first_subwindow: KI-W6-S101
integration_assessment_id: KI-W6-I101
parent_review_required: true
```

The window agent stops here. No leaf begins before the parent approves this
DECOMP-3 package (including any parent A5 CAS recording that approval) and
the window agent's resulting `S2.decomposition_status: READY` transition.

---

## `EV-KI-W6-R08` — Third parent reconciliation to A4 `KI-CL-19` (`EV-KI-A-084` `F10`–`F12`)

- **Timestamp:** 2026-08-20T23:20:00+05:30
- **Parent window / assignment:** `KI-W6` / `ASG-KI-W6-WA-02` (A5 state 145,
  CAS 144→145 recorded by the parent in `EV-KI-A-084`; parent corrected A4
  `KI-CL-18`→`KI-CL-19` and recorded `CHG-KI-057`)
- **Actor/role:** `KI-W6-WINDOW-AGENT` (reconciliation author)
- **Operative authority:** A5 v145
  (`ACTIVE_EXECUTION_STATE.md` sha256
  `726888a434115defc9e120e30e36703a5498610acca356434553ca9e2367f36d`) and
  A4 `KI-CL-19`
  (`KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md` sha256
  `8fa54dd445dda3ad3bda8a4b0434bbbc8f93ad75469f782015ab4631eed9bcb3`),
  both recomputed and byte-equal on disk this session with the standards,
  contract, and decision pins unchanged. Both nested repositories
  re-verified clean at `0083a42c…`/`70fb5edf…`; the `KI-CL-19` KI-W6 header
  pins the same five starting digests, path-set digest `d28ae178…3d0bb`,
  and repository baselines.
- **F10 resolution (emitted-server bootstrap):** verified against source —
  `lib/backend-proxy.ts:67-69` derives the Authorization header from
  `BACKEND_API_TOKEN`, so its absence would 401 every proxied request
  against the backend's `kiw6-backend-token`. S1 now freezes the fourth
  `frontendEnv` value `BACKEND_API_TOKEN: "kiw6-backend-token"` (IF-2
  member 1; S103-C13), the four-value `next start` child allowlist (IF-2
  child-env contract; S105 step 2), and the callable no-op
  `createLeadServer.logger: () => {}` (server invokes the logger as a
  function; never an object) in the IF-2 server options and S103 step 3
  (S103-C16).
- **F11 resolution (provider data topology):** S1 replaces "adapt the
  shapes" with the A4-frozen literal synthesis (§0.1 item 12; IF-2 "Literal
  provider synthesis"): exact `pad2`/`pad3` definitions (S103-C14), the
  per-seed 30 suggestion/30 related string literals in ascending `i`
  (S103-C15), seed + 30 suggestions + first-29-related retention = 300
  distinct anchor inputs, every overview item from the verified
  `overviewResponse` formula at
  `test/keyword-intelligence-worker.test.js:93-122` (costs `0.048`/300,
  `0.036`/200), and the required aggregation witnesses (300 active anchor
  candidates → deterministic first-200 shortlist → 200-row final result /
  default-100 selection). The Google contract now freezes the exact item
  fields (`title: receivedQuery`, `snippet: receivedQuery`,
  `displayLink: host`, `link: https://${host}/products/result-${pad2(r)}`,
  host `w6-q${pad3(q)}-r${pad2(r)}.myshopify.com`, ordinal `q` = 1 +
  zero-based `searchPage` invocation index under `queryProbeConcurrency: 1`)
  and requires acceptance through the **production query-probe path** — ten
  usable distinct hosts, ten relevant results, ratio `1`, no rejection per
  validation — recording the parent's falsification (link-only cloning
  preserved fixture title/snippet → `summarizeProbe` gave zero relevant
  results, ratio zero, `irrelevant_probe_results`). Discovery artifacts
  remain production-created (`preloadLead` prohibited; S103-C10).
- **F12 resolution (nonempty fault injection):** the IF-2 fault union is now
  the eight-ID union with the six A4 queue-specific duplicate/reorder IDs
  (`duplicate/reorder-pending-{keyword,discovery,domain-check}-messages`;
  S103-C9 asserts each exactly once) plus the two captured-state faults;
  duplicates take a fresh monotonic delivery ID with **no dispatcher send
  trace** (base send counts unchanged) and reorders reverse the named
  queue's pending body order with fresh increasing delivery IDs. Exact
  nonempty injection points are frozen in IF-2 member 9 and embedded in the
  S105 step-12 causal order: keyword duplicate/reorder immediately after
  initialization queues expansion tasks/checks, then the one
  `restartBackend()`, then the expansion drain; discovery duplicate/reorder
  immediately after confirmation dispatches the 100 discovery deliveries;
  domain-check duplicate/reorder after the first discovery emits a check,
  before the downstream drain completes. An empty-queue fault invocation
  throws `HarnessPreflightError` and is an oracle failure
  (`W6-RES-02` forbidden column: empty-queue no-op — A4 `KI-CL-19` matrix).
- **Digest recomputations:** five-path set `d28ae178…3d0bb` unchanged;
  per-leaf starting change-set digests unchanged (repositories clean);
  manifest group/global digests re-verified equal to the `DEC-KI-038`
  literals; the decision-ledger pin `ef415367…` re-verified unchanged
  (`CHG-KI-057` touched A4/A5/A6/A7 only).
- **Artifacts produced:** reconciled S1 (1827 lines, revision
  `c197af8640cce52e9224c35aa41159754c271b99d5a5222765bf20feb0665831`,
  recorded in S2 state v4), this S3 entry.
- **External mutations/cost:** none beyond the three coordination files;
  `$0.00`; no implementation, leaf, test, build, browser, database,
  provider, AWS, destructive, commit/push, or KI-W7 action (per A5 v145
  prohibitions).
- **Disposition:** reconciliation applied; superseding readiness audit
  follows (`EV-KI-W6-R09`).

---

## `EV-KI-W6-R09` — Third superseding readiness completion and self-falsification

- **Timestamp:** 2026-08-20T23:20:00+05:30
- **Actor/role:** `KI-W6-WINDOW-AGENT` (third superseding readiness audit)
- **Supersession scope:** this entry and the certificate below supersede the
  DECOMP-3 readiness claims of `EV-KI-W6-R07` and its certificate
  (decomposition revision `2ea48e27…`), which remain as unapproved-draft
  history together with all DECOMP-1/2 claims.
- **Checklist completion against DECOMP-4 (S1 revision
  `c197af8640cce52e9224c35aa41159754c271b99d5a5222765bf20feb0665831` per
  S2 state v4):** all 47 `SW-*` items in S1 §7 carry resolvable references
  to the reconciled S1 sections or to `EV-KI-W6-R08`/`R09`; zero unchecked;
  zero `N/A`.
- **Structural document lint (re-run on DECOMP-4):** five initial blocks
  with all standard §7 fields; V1 now twelve rows with the C13–C16
  expectations; §8.1 five exact certificate IDs; append-only §9. Machine
  grep confirms: zero occurrences of the retired fault ID
  `reorder-pending-messages`, zero "three `frontendEnv` values", zero
  "55 characters", zero object-form logger, zero "adapt the shapes"
  delegation in the provider recipe; the F10–F12 literals
  (`BACKEND_API_TOKEN: "kiw6-backend-token"`, `logger: () => {}`,
  `pad2`/`pad3`, `suggestion s${s}${pad2(i)}`,
  `/products/result-${pad2(r)}`, all six queue fault IDs) each appear in
  the frozen interface and in an executable leaf check. All ID references
  resolve.
- **Self-falsification re-run (standard §14):** all 22 counterexamples
  remain rejected; strengthened for DECOMP-4 — an emitted-Next run without
  the token cannot pass V3 (401 on the first proxied request); a provider
  recipe preserving fixture title/snippet cannot pass `W6-FLOW-10`
  (production probe rejects with ratio zero); a fault invoked on an empty
  queue cannot pass `W6-RES-02` (the `HarnessPreflightError` and the
  empty-queue-no-op forbidden column both fail it); a fault delivery
  counted as a dispatcher send cannot pass the 42/100 base-send assertions.
- **Predictable parent gates:** parent decomposition review of DECOMP-4 and
  an A5 CAS recording approval before `S2.decomposition_status: READY` and
  any leaf dispatch; V3 later requires the environment `TEST_DATABASE_URL`
  opt-in (present) and sandbox escalation per §0.2; commits remain
  requester-only; KI-W7 remains parent-reserved.
- **External mutations/cost:** none beyond the three coordination files;
  `$0.00`.
- **Disposition:** third superseding readiness complete; certificate
  appended below.

---

## Third superseding decomposition readiness certificate (sub-window standard §12.1)

This certificate supersedes every earlier `SUBWINDOW-DECOMPOSITION-READY`
certificate in this file (DECOMP-1 at `a74ebef9…`/`e7893e49…`, DECOMP-2 at
`c1771d1e…`, DECOMP-3 at `2ea48e27…`), which are retained above as
unapproved-draft history only.

```yaml
certificate: SUBWINDOW-DECOMPOSITION-READY
supersedes: certificates at draft revisions a74ebef90a84451d7ced65934a067073f71269c470b97ec4e92962dfb0611ad0, e7893e49930321c911def84082d6ce7a243a154e7bab644e2b73ee25bec12868, c1771d1e994e520202cf165c27ff8586a69fd9dea48393568cbc2e6753c7e372, and 2ea48e27d47ddc0824285471877e4897b3740c16516f0b1abea81cb79b77bb4c
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-02
window_agent_identity: KI-W6-WINDOW-AGENT
correction_authority: [EV-KI-A-082 (A5 state 143), EV-KI-A-083 (A5 state 144), EV-KI-A-084 (A5 state 145; A4 KI-CL-19; CHG-KI-057)]
revisions:
  parent_standard: cda352017e75c0d11f6797d9fbe108b4365508cd38b0e92365cfb523ede32848
  subwindow_standard: 84e7590e74589f308c70dc9b0b67f7e9da395fafb1e5786202ecd1ca15be56e9
  contract: 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c
  decision: ef4153677807c80dfa9a09c0ffe0ba5a5127681fe6706e17ff6cd48869fdbd31
  parent_checklist: 8fa54dd445dda3ad3bda8a4b0434bbbc8f93ad75469f782015ab4631eed9bcb3
  parent_state: 726888a434115defc9e120e30e36703a5498610acca356434553ca9e2367f36d
  decomposition: c197af8640cce52e9224c35aa41159754c271b99d5a5222765bf20feb0665831
initial_subwindow_ids: [KI-W6-S101, KI-W6-S102, KI-W6-S103, KI-W6-S104, KI-W6-S105]
initial_subwindow_count: 5
planned_file_set:
  - email_scraper/test/fixtures/keyword-intelligence/ki-w6-enforcement-manifest-v1.json
  - email_scraper/test/helpers/keyword-intelligence-e2e-harness.js
  - frontend/components/keyword-intelligence/research-dashboard.tsx
  - frontend/test/browser/keyword-intelligence-dashboard.mjs
  - frontend/test/browser/keyword-intelligence-e2e.mjs
planned_file_set_digest: d28ae17864073639580d7650bb03c03474d5370a5034b632cf412e1e3cf3d0bb
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
parent_findings_unresolved: []
mandatory_authoring_items_checked: 47
mandatory_authoring_items_unchecked: 0
first_subwindow: KI-W6-S101
integration_assessment_id: KI-W6-I101
parent_review_required: true
```

The window agent stops here. No leaf begins before the parent approves this
DECOMP-4 package (including any parent A5 CAS recording that approval) and
the window agent's resulting `S2.decomposition_status: READY` transition.

---

## `EV-KI-W6-R10` — Fourth parent-authority reconciliation (`F13`)

- **Timestamp:** 2026-08-20T22:38:27+05:30
- **Actor/role:** `KI-W6-WINDOW-AGENT` (temporary parent-requested
  reconciliation role; no implementation authority exercised).
- **Operative authority:** A4 `KI-CL-20`
  `8fe18271bf368a283246d55807dcc4612e118c725e5aabeb6188962a7abf5f4e`;
  A5 state 146
  `464f10ad68f4df3c2dd7c84e0202a129fa3ec0742569ab9791c2372ae97ca462`;
  `EV-KI-A-085` / `CHG-KI-058`. All contract, decision, parent-standard and
  sub-window-standard pins remain byte-equal to the S1 §0 table.
- **F13 resolution:** IF-2 retains one `restartBackend()` method but S105 now
  invokes it at exactly two noninterchangeable causal points. Restart A is
  after the nonempty keyword duplicate/reorder partition and before any
  expansion drain (`W6-RES-02`). Restart B is after the post-handoff live
  research-selection mutation and before the durable Run/100-RunQuery reload
  and byte/deep equality comparison (`W6-FLOW-13`). S105-C11 and V1-12 require
  exactly two literal invocations; one omitted or merged invocation fails.
- **Mechanical closure:** S1 is now `KI-W6-REAUTHORED-DECOMP-5`, 1856 lines,
  revision `dedb5a2b3339856d6eeafb6f34ea4460a4de7dd3da298cb9ee9f515fd48ebe2e`;
  47/47 `SW-*` items checked, zero unchecked. The five planned implementation
  paths, their digest `d28ae178…3d0bb`, leaf DAG, manifest membership/digests,
  provider recipes, fault IDs, and all F1–F12 resolutions are unchanged.
- **Working trees:** backend and frontend remain clean. Coordination-root
  porcelain is exactly the three untracked REAUTHORED artifacts plus the four
  parent-owned modified authority files A4/A5/A6/A7; no other path is present.
- **No execution:** no leaf assignment, implementation edit, test, build,
  browser, database, provider, AWS, production, destructive, commit, push, or
  KI-W7 action; cost `$0.00`.

---

## `EV-KI-W6-R11` — Fourth superseding readiness completion and self-falsification

- **Timestamp:** 2026-08-20T22:38:27+05:30
- **Actor/role:** `KI-W6-WINDOW-AGENT`.
- **Supersession:** this readiness audit and certificate supersede the
  DECOMP-4 audit/certificate at `EV-KI-W6-R09`; all earlier draft certificates
  remain historical and non-authorizing.
- **Readiness:** all 47 mandatory `SW-*` items resolve to current S1 sections
  or R10/R11 evidence; zero unchecked, zero `N/A`; requirements, decisions,
  tasks, scenarios, cases, controls, interfaces, intermediate states,
  execution choices, and evidence references each have zero unmapped or
  unresolved members. Five initial leaves remain single-file, uniquely owned,
  and strictly sequential; I101 retains zero implementation-write authority.
- **Structural/adversarial audit:** removing either restart invocation fails
  S105-C11/V1-12 and its owning coverage row; moving restart A after expansion
  makes W6-RES-02's recovery witness false; moving restart B before the
  selection mutation makes W6-FLOW-13's persistence witness false. The prior
  22 self-falsification counterexamples remain rejected. No unresolved broad
  verb, wildcard scope, computed-at-dispatch decision, alternative, or
  authority conflict remains in assignable content.
- **Disposition:** `AWAITING_PARENT_DECOMPOSITION_REVIEW`; no leaf assigned.

---

## Fourth superseding decomposition readiness certificate (sub-window standard §12.1)

This certificate supersedes every earlier `SUBWINDOW-DECOMPOSITION-READY`
certificate in this file, including DECOMP-4 revision `c197af8640…`.

```yaml
certificate: SUBWINDOW-DECOMPOSITION-READY
supersedes: all DECOMP-1/2/3/4 draft certificates, latest superseded revision c197af8640cce52e9224c35aa41159754c271b99d5a5222765bf20feb0665831
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-02
window_agent_identity: KI-W6-WINDOW-AGENT
correction_authority: [EV-KI-A-082 (F1-F5), EV-KI-A-083 (F6-F9), EV-KI-A-084 (F10-F12), EV-KI-A-085 (F13; A5 state 146; A4 KI-CL-20; CHG-KI-058)]
revisions:
  parent_standard: cda352017e75c0d11f6797d9fbe108b4365508cd38b0e92365cfb523ede32848
  subwindow_standard: 84e7590e74589f308c70dc9b0b67f7e9da395fafb1e5786202ecd1ca15be56e9
  contract: 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c
  decision: ef4153677807c80dfa9a09c0ffe0ba5a5127681fe6706e17ff6cd48869fdbd31
  parent_checklist: 8fe18271bf368a283246d55807dcc4612e118c725e5aabeb6188962a7abf5f4e
  parent_state: 464f10ad68f4df3c2dd7c84e0202a129fa3ec0742569ab9791c2372ae97ca462
  decomposition: dedb5a2b3339856d6eeafb6f34ea4460a4de7dd3da298cb9ee9f515fd48ebe2e
initial_subwindow_ids: [KI-W6-S101, KI-W6-S102, KI-W6-S103, KI-W6-S104, KI-W6-S105]
initial_subwindow_count: 5
planned_file_set:
  - email_scraper/test/fixtures/keyword-intelligence/ki-w6-enforcement-manifest-v1.json
  - email_scraper/test/helpers/keyword-intelligence-e2e-harness.js
  - frontend/components/keyword-intelligence/research-dashboard.tsx
  - frontend/test/browser/keyword-intelligence-dashboard.mjs
  - frontend/test/browser/keyword-intelligence-e2e.mjs
planned_file_set_digest: d28ae17864073639580d7650bb03c03474d5370a5034b632cf412e1e3cf3d0bb
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
parent_findings_unresolved: []
mandatory_authoring_items_checked: 47
mandatory_authoring_items_unchecked: 0
first_subwindow: KI-W6-S101
integration_assessment_id: KI-W6-I101
parent_review_required: true
```

The window agent stops here. No implementation leaf or gate began.

---

## `EV-KI-W6-R12` — Strict predecessor-chain reconciliation (`F14`)

- **Timestamp:** 2026-08-20T22:50:00+05:30
- **Actor/role:** `KI-W6-WINDOW-AGENT`.
- **Authority:** A5 state 147
  `8954cf2e9414aab484735ffd67f094dce563219b4a431d3a4878dde786bbfcd7`;
  A4 remains `KI-CL-20` `8fe18271…`; `EV-KI-A-086` / `CHG-KI-059`.
- **F14 resolution:** the §3 DAG and all five file-subwindow `predecessors`
  fields now encode exactly S101 `[]`, S102 `[S101]`, S103 `[S102]`, S104
  `[S103]`, S105 `[S104]`; I101 remains after all five. This equals the frozen
  execution order and the predecessor-based starting changed-set table. No
  semantic `depends_on_files`, interface, file scope, case, control, digest,
  gate, or implementation instruction changed.
- **Artifacts:** S1 `KI-W6-REAUTHORED-DECOMP-6`, 1864 lines, revision
  `bf92d2515a3dde37e7e577308ee69b224fe21498434ef831612536a841475134`;
  S2 state 6. Backend/frontend remain clean; coordination-root ownership set is
  unchanged.
- **No execution:** no leaf assignment, implementation edit, gate, provider,
  AWS, database, build, browser, commit, push, or KI-W7 work; `$0.00`.

---

## `EV-KI-W6-R13` — Fifth superseding readiness completion

- **Timestamp:** 2026-08-20T22:50:00+05:30
- **Actor/role:** `KI-W6-WINDOW-AGENT`.
- **Supersession:** DECOMP-6 and this audit supersede DECOMP-5 R10/R11
  readiness while retaining its valid F13 facts.
- **Closure:** 47/47 `SW-*` checked, zero unchecked/N/A; five unique single-file
  leaves; exact strict predecessor chain; zero unmapped requirements,
  decisions, tasks, cases, or controls; zero unresolved interfaces,
  intermediate states, execution choices, evidence references, or parent
  findings. Removing or changing any predecessor now breaks both the declared
  chain and its starting changed-set witness.
- **Disposition:** `AWAITING_PARENT_DECOMPOSITION_REVIEW`; no leaf assigned.

---

## Fifth superseding decomposition readiness certificate (sub-window standard §12.1)

```yaml
certificate: SUBWINDOW-DECOMPOSITION-READY
supersedes: all DECOMP-1/2/3/4/5 draft certificates, latest superseded revision dedb5a2b3339856d6eeafb6f34ea4460a4de7dd3da298cb9ee9f515fd48ebe2e
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-02
window_agent_identity: KI-W6-WINDOW-AGENT
correction_authority: [EV-KI-A-082 (F1-F5), EV-KI-A-083 (F6-F9), EV-KI-A-084 (F10-F12), EV-KI-A-085 (F13), EV-KI-A-086 (F14; A5 state 147; CHG-KI-059)]
revisions:
  parent_standard: cda352017e75c0d11f6797d9fbe108b4365508cd38b0e92365cfb523ede32848
  subwindow_standard: 84e7590e74589f308c70dc9b0b67f7e9da395fafb1e5786202ecd1ca15be56e9
  contract: 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c
  decision: ef4153677807c80dfa9a09c0ffe0ba5a5127681fe6706e17ff6cd48869fdbd31
  parent_checklist: 8fe18271bf368a283246d55807dcc4612e118c725e5aabeb6188962a7abf5f4e
  parent_state: 8954cf2e9414aab484735ffd67f094dce563219b4a431d3a4878dde786bbfcd7
  decomposition: bf92d2515a3dde37e7e577308ee69b224fe21498434ef831612536a841475134
initial_subwindow_ids: [KI-W6-S101, KI-W6-S102, KI-W6-S103, KI-W6-S104, KI-W6-S105]
initial_subwindow_count: 5
initial_predecessors:
  KI-W6-S101: []
  KI-W6-S102: [KI-W6-S101]
  KI-W6-S103: [KI-W6-S102]
  KI-W6-S104: [KI-W6-S103]
  KI-W6-S105: [KI-W6-S104]
planned_file_set:
  - email_scraper/test/fixtures/keyword-intelligence/ki-w6-enforcement-manifest-v1.json
  - email_scraper/test/helpers/keyword-intelligence-e2e-harness.js
  - frontend/components/keyword-intelligence/research-dashboard.tsx
  - frontend/test/browser/keyword-intelligence-dashboard.mjs
  - frontend/test/browser/keyword-intelligence-e2e.mjs
planned_file_set_digest: d28ae17864073639580d7650bb03c03474d5370a5034b632cf412e1e3cf3d0bb
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
parent_findings_unresolved: []
mandatory_authoring_items_checked: 47
mandatory_authoring_items_unchecked: 0
first_subwindow: KI-W6-S101
integration_assessment_id: KI-W6-I101
parent_review_required: true
```

The window agent stops here. No implementation leaf or gate began.

---

## `EV-KI-W6-R14` — Parent approval acknowledged; decomposition READY

- **Timestamp:** 2026-08-20T23:00:00+05:30
- **Actor/role:** `KI-W6-WINDOW-AGENT` (coordination transition only).
- **Parent approval:** `EV-KI-A-087`; A5 state 148 revision
  `162221c05be37ac06bb8cf742dffb39bb6e3bbae124a2b25dbcc4ab2e39a4046`
  explicitly approves S1 revision
  `bf92d2515a3dde37e7e577308ee69b224fe21498434ef831612536a841475134`.
  This is the required post-pin delta audit: A4, standards, contract, decision,
  S1, five-file set, baselines, interfaces, cases, controls and gates are
  unchanged; the A5 delta is approval/recursive execution authority only.
- **State transition:** S2 state 7 sets `decomposition_status: READY` and
  `current_status: READY`; all leaves remain `NOT_STARTED`/`UNASSIGNED`,
  `current_subwindow:NONE`, and `next_subwindow:KI-W6-S101`.
- **Dispatch boundary:** the window agent may next assign S101 to one named
  leaf agent. S102–S105 and I101 remain prohibited until their exact
  predecessors are accepted. No leaf was assigned or dispatched by this
  transition.
- **External mutations/cost:** none; `$0.00`; no implementation, test, build,
  browser, database, provider, AWS, production, destructive, commit, push, or
  KI-W7 action.
