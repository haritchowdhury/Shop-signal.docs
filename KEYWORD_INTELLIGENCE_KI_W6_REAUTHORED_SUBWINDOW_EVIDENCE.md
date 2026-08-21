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

---

## `KI-W6-S101` file-subwindow execution certificate

```yaml
certificate: FILE-SUBWINDOW-EXECUTED
parent_window_id: KI-W6
subwindow_id: KI-W6-S101
assignment_id: ASG-KI-W6-S101
agent_identity: KI-W6-S101-LEAF-AGENT
writable_file: frontend/components/keyword-intelligence/research-dashboard.tsx
starting_file_digest: 19494a99a2be28683167908289176bf44ebb8d0bb1eb40f63cc6d1cd770c6337
ending_file_digest: 68a7ec84d77a955122dfb9ca1767ab1a52c2a2f2125db5c34581e5e9af8f5984
starting_repository_change_set_digest: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
attributable_changed_file_set: [frontend/components/keyword-intelligence/research-dashboard.tsx]
required_local_cases: [S101-C1, S101-C2, S101-C3, S101-C4]
registered_local_cases: [S101-C1, S101-C2, S101-C3, S101-C4]
executed_local_cases: [S101-C1, S101-C2, S101-C3, S101-C4]
skipped_local_cases: []
duplicate_case_ids: []
unexpected_case_ids: []
missing_activation_witnesses: []
negative_controls_expected: 0
negative_controls_falsified: 0
commands:
  - "grep -cF 'router.push(handoff.statusUrl)' frontend/components/keyword-intelligence/research-dashboard.tsx -> count 0 (exit 1) [S101-C1]"
  - "grep -cF 'router.push(`/runs/${encodeURIComponent(handoff.run.runId)}`)' frontend/components/keyword-intelligence/research-dashboard.tsx -> 2 [S101-C2]"
  - "wc -l frontend/components/keyword-intelligence/research-dashboard.tsx -> 529 [S101-C3]"
  - "git -C frontend diff --numstat -- components/keyword-intelligence/research-dashboard.tsx -> 2 inserted, 2 deleted [S101-C4]"
deferred_integration_checks: [V2 lint/tsc/build of the changed file, W6-NAV-01, W6-NAV-02, W6-NAV-03, W6-NC-01 (registered in S105)]
external_mutations: []
prohibited_actions_observed: []
successor_work_started: false
direct_parent_communication: false
status: AWAITING_WINDOW_REVIEW
```

Applied transformation: anchor A (line 266, `handleFinalize` success branch)
then anchor B (line 300, `handleRetryHandoff` success branch), each
`      router.push(handoff.statusUrl);` →
``      router.push(`/runs/${encodeURIComponent(handoff.run.runId)}`);``
with six-space indentation preserved; both replacements single-line for
single-line; all other 527 lines byte-identical (C3/C4 witnesses). No
import, state, prop, component, type, helper, fallback, route-probe, or
conditional change; `startKeywordResearchRun` return shape consumed
unchanged; no I/O of any kind added.

---

## `EV-KI-W6-R15` — S101 independent review disposition

- **Timestamp:** 2026-08-20T23:40:00+05:30
- **Actor/role:** `KI-W6-WINDOW-AGENT` (independent leaf review, standard §8
  13-point)
- **Independent inspection:** full `git -C frontend diff` read directly —
  exactly two single-line replacements inside the two pinned success
  branches, no other byte change; anchors verified pre-edit at lines
  266/300 against starting digest `19494a99…` (recomputed byte-equal before
  dispatch); `frontend` worktree was clean pre-dispatch (change-set digest
  `e3b0c442…` per §3.1).
- **P1–P2 baselines:** assignment identity, writable file, pinned starting
  digest, and clean baseline all matched. **T1/V1:** transformation and all
  four LOCAL_NOW witnesses exact (C1 0/exit 1, C2 2, C3 529, C4 2/2).
  **V2:** `git -C frontend status --porcelain` shows exactly
  ` M components/keyword-intelligence/research-dashboard.tsx` — the
  attributable changed-file set equals the writable file. **V3:** required =
  registered = executed = {C1..C4}, zero skips. **H2:** no prohibited
  action, second-file edit, successor work, external mutation, or parent
  communication.
- **Disposition:** `ACCEPTED_FOR_INTEGRATION`. Deferred V2 build/lint and
  V3 navigation gates (`W6-NAV-01..03`, `W6-NC-01`) remain registered in
  `S105`/`I101` per the approved decomposition.
- **State transition:** S2 records S101 EXECUTED → ACCEPTED;
  `next_subwindow: KI-W6-S102` (predecessor `KI-W6-S101` accepted).
- **External mutations/cost:** the single writable file only; `$0.00`.

---

## `KI-W6-S102` file-subwindow execution certificate

```yaml
certificate: FILE-SUBWINDOW-EXECUTED
parent_window_id: KI-W6
subwindow_id: KI-W6-S102
assignment_id: ASG-KI-W6-S102
agent_identity: KI-W6-S102-LEAF-AGENT
writable_file: frontend/test/browser/keyword-intelligence-dashboard.mjs
starting_file_digest: d30bed66cdc77ff53438515345be01baf2e1ad90ea2b9b8c8ab71c47f339c398
ending_file_digest: 17ae402882f64fd8da6aba61161343f119aa1b7a62edbed0cbf97d9bbe0896b7
starting_repository_change_set_digest: d1349d2efaeb4f235fdc62a01f529a7c4c861e814964c4a12c05eba5f27f0be2
attributable_changed_file_set: [frontend/test/browser/keyword-intelligence-dashboard.mjs]
required_local_cases: [S102-C1, S102-C2, S102-C3, S102-C4, S102-C5, S102-C6]
registered_local_cases: [S102-C1, S102-C2, S102-C3, S102-C4, S102-C5, S102-C6]
executed_local_cases: [S102-C1, S102-C2, S102-C3, S102-C4, S102-C5, S102-C6]
skipped_local_cases: []
duplicate_case_ids: []
unexpected_case_ids: []
missing_activation_witnesses: []
negative_controls_expected: 0
negative_controls_falsified: 0
commands:
  - "node --check frontend/test/browser/keyword-intelligence-dashboard.mjs -> exit 0 [S102-C1]"
  - "grep -c 'ki-r5-fin-nav-witness' ... -> 0 (exit 1) [S102-C2]"
  - "grep -cF 'run_kiw5_hostile_status_witness0001' ... -> 1 [S102-C3]"
  - "grep -cF 'encodeURIComponent(runHandoff.run.runId)' ... -> 1 [S102-C4]"
  - "grep -c 'runScenario(' ... -> 26 [S102-C5]"
  - "git -C frontend diff --numstat -- test/browser/keyword-intelligence-dashboard.mjs -> 8 inserted, 4 deleted [S102-C6]"
deferred_integration_checks: [V2 eslint of this file, W6-NAV-01, W6-NAV-02, W6-NAV-03, W6-NC-01 (executed in S105/V3)]
external_mutations: []
prohibited_actions_observed: []
successor_work_started: false
direct_parent_communication: false
status: AWAITING_WINDOW_REVIEW
```

Applied transformation: only the `R5-FIN-01` block — comments −2/+3;
`hostileStatusPath` const inserted before the `evaluate`; the fixture
assignment replaced with `${JSON.stringify(hostileStatusPath)}`;
`workspacePath` const inserted after the three `fin` assertions; the
pathname `waitFor` replaced with the
`location.pathname === ${JSON.stringify(workspacePath)}` /
`"finalize workspace navigation witness"` form; hostile-path non-visit
`assert` inserted after it; `capture("R5-FIN-01-finalize")` and every other
line byte-identical. Predecessor S101 accepted (`EV-KI-W6-R15`);
starting change-set digest `d1349d2e…` recomputed from the actual
changed-path set `{F-001}` under the sorted-member-plus-LF formula
(§3.1) — byte-equal.

---

## `EV-KI-W6-R16` — S102 independent review disposition

- **Timestamp:** 2026-08-20T23:55:00+05:30
- **Actor/role:** `KI-W6-WINDOW-AGENT` (independent leaf review)
- **Independent inspection:** full diff read directly — exactly 8 inserted /
  4 deleted, all inside the `R5-FIN-01` block; no other R5/W5 case,
  registration (26 unchanged), screenshot, capture, fetch-interception,
  presentation assertion, registry, output-path, helper, port, build, or
  browser-lifecycle line touched. Hostile literal occurs exactly once (its
  declaration); the assignment and assert reference the variable.
  `hostileStatusPath`/`workspacePath` counts (3/2) confirm block-local use
  only. `node --check` proves syntax.
- **P1–P2:** assignment identity, pinned starting digest `d30bed66…`
  (recomputed byte-equal), predecessor S101 accepted, and change-set digest
  `d1349d2e…` all matched. **T1/V1:** all six witnesses exact. **V2:**
  workspace delta since S101 = exactly this writable file. **V3:**
  required = registered = executed = {C1..C6}, zero skips. **H2:** no
  prohibited action, second-file edit, successor work, external mutation,
  or parent communication.
- **Disposition:** `ACCEPTED_FOR_INTEGRATION`.
- **State transition:** S2 records S102 EXECUTED → ACCEPTED;
  `next_subwindow: KI-W6-S103`.
- **External mutations/cost:** the single writable file only; `$0.00`.

---

## `KI-W6-S103` file-subwindow execution certificate

```yaml
certificate: FILE-SUBWINDOW-EXECUTED
parent_window_id: KI-W6
subwindow_id: KI-W6-S103
assignment_id: ASG-KI-W6-S103
agent_identity: KI-W6-S103-LEAF-AGENT
writable_file: email_scraper/test/helpers/keyword-intelligence-e2e-harness.js
starting_file_digest: ABSENT
ending_file_digest: 93ee3a3b31275a84babe27e3b37519bb4b86e3bd1571485f3bf3486c3b8c5a26
starting_repository_change_set_digest: fbfdac4a76ef0754ab3de904905a85b38b3777b2ad39926625f46ae4ae503954
attributable_changed_file_set: [email_scraper/test/helpers/keyword-intelligence-e2e-harness.js]
required_local_cases: [S103-C1, S103-C2, S103-C3, S103-C4, S103-C5, S103-C6, S103-C7, S103-C8, S103-C9, S103-C10, S103-C11, S103-C12, S103-C13, S103-C14, S103-C15, S103-C16]
registered_local_cases: [S103-C1, S103-C2, S103-C3, S103-C4, S103-C5, S103-C6, S103-C7, S103-C8, S103-C9, S103-C10, S103-C11, S103-C12, S103-C13, S103-C14, S103-C15, S103-C16]
executed_local_cases: [S103-C1, S103-C2, S103-C3, S103-C4, S103-C5, S103-C6, S103-C7, S103-C8, S103-C9, S103-C10, S103-C11, S103-C12, S103-C13, S103-C14, S103-C15, S103-C16]
skipped_local_cases: []
duplicate_case_ids: []
unexpected_case_ids: []
missing_activation_witnesses: []
negative_controls_expected: 0
negative_controls_falsified: 0
commands:
  - "node --check email_scraper/test/helpers/keyword-intelligence-e2e-harness.js -> exit 0 [S103-C1]"
  - "grep -cF structural witnesses C2..C16 -> exactly 1 each (C9: eight fault IDs each 1) [S103-C2..C16]"
  - "grep -cE 'KeywordSearchVolume|data/output|output\\.json|sqlite|\\.py\\b|python' -> 0 (exit 1) [S103-C4]"
  - "grep -c 'preloadLead' -> 0 (exit 1) [S103-C10]"
deferred_integration_checks: [all behavioral claims: W6-FLOW-*, W6-RES-*, NC-02..09, NC-12, operation counts, schema lifecycle — V3 only]
external_mutations: []
prohibited_actions_observed: []
successor_work_started: false
direct_parent_communication: false
status: AWAITING_WINDOW_REVIEW
```

Construction followed the S1 §4 S103 recipe steps 1–10 against verified
source anchors; no database connection, build, or test execution occurred
during the leaf. Leaf-agent-reported source divergences (all resolved by
following real source, none a structural-check failure): (1) frozen 12-key
config literal omits `googleApiKey`/`googleSearchEngineId`/`openaiApiKey`
required only by direct `POST /api/runs` config assertion paths the W6 flow
never touches; (2) `research.selectionFingerprint` projected from the
linked handoff row (no Prisma column on `KeywordResearch`); (3) keyword
provider throttle compares against the PostgreSQL clock, so the harness
uses the exact `resetThrottle` anchor from
`keyword-intelligence-worker.test.js:177-179` alongside the mandated
+2000 ms clock advance; (4) **integration risk flagged for S105/V3:**
production discovery identity resolution
(`processDiscoveryMessage` → `resolveStoreIdentity` → `requestText` →
`globalThis.fetch` + `dns.lookup`) exposes no runtime injection seam; the
leaf fabricated none (correct per contract rules) and claims zero
behavioral parity; (5) Google trace `runQueryId` records the received
query text — the only identity the `searchPage` seam receives.

---

## `EV-KI-W6-R17` — S103 independent review disposition

- **Timestamp:** 2026-08-21T00:20:00+05:30
- **Actor/role:** `KI-W6-WINDOW-AGENT` (independent leaf review)
- **Independent inspection:** all C1–C16 commands re-executed directly by
  the window agent — every count exact (frozen signature/return statement,
  `pad2`/`pad3`, three synthesis templates, host template, `TASK_COSTS`,
  `SCHEMA_PREFIX`, `DISPATCHER_METHODS`, `SCHEMA_ABSENCE_QUERY`,
  `HarnessCleanupError`, `BACKEND_API_TOKEN` literal, `logger: () => {}`,
  eight fault IDs each once; zero forbidden tokens).
- **P1–P2:** assignment identity, ABSENT starting file, and starting
  change-set digest `fbfdac4a…` (changed set `{F-001, F-002}` recomputed
  under the §3.1 formula — S101/S102 frontend changes only) matched;
  backend worktree was clean pre-dispatch. **V2:** backend delta = exactly
  the one new untracked helper. **V3:** required = registered = executed =
  {C1..C16}, zero skips. **H2:** no prohibited action, production/package
  edit, database connection, second-file edit, successor work, external
  mutation, or parent communication.
- **Divergence ruling:** all five leaf-reported divergences follow real
  source within the frozen literals; divergence (4) is recorded as a V3
  integration risk for `S105`/`I101` (discovery identity seam), not an
  S103 defect — the leaf's acceptance basis is structural with zero
  behavioral parity claims by design.
- **Disposition:** `ACCEPTED_FOR_INTEGRATION`.
- **State transition:** S2 records S103 EXECUTED → ACCEPTED;
  `next_subwindow: KI-W6-S104`.
- **External mutations/cost:** the single writable file only; `$0.00`.

---

## `KI-W6-S104` file-subwindow execution certificate

```yaml
certificate: FILE-SUBWINDOW-EXECUTED
parent_window_id: KI-W6
subwindow_id: KI-W6-S104
assignment_id: ASG-KI-W6-S104
agent_identity: KI-W6-S104-LEAF-AGENT
writable_file: email_scraper/test/fixtures/keyword-intelligence/ki-w6-enforcement-manifest-v1.json
starting_file_digest: ABSENT
ending_file_digest: ea3a5471e33f5dcc656a6b522e8d379f596caad158c0bd3ff2315e93d145e475
starting_repository_change_set_digest: b94659a0de51b39e36e984c858ee4f0fa0effefaba27140ea29146fa947515e9
attributable_changed_file_set: [email_scraper/test/fixtures/keyword-intelligence/ki-w6-enforcement-manifest-v1.json]
required_local_cases: [S104-C1, S104-C2, S104-C3, S104-C4]
registered_local_cases: [S104-C1, S104-C2, S104-C3, S104-C4]
executed_local_cases: [S104-C1, S104-C2, S104-C3, S104-C4]
skipped_local_cases: []
duplicate_case_ids: []
unexpected_case_ids: []
missing_activation_witnesses: []
negative_controls_expected: 0
negative_controls_falsified: 0
commands:
  - "node -e strict JSON.parse -> S104-C1 OK, exit 0 [S104-C1]"
  - "node -e keys/groups/counts/uniqueness/order script -> S104-C2 OK, exit 0 [S104-C2]"
  - "node -e sha256 member-plus-LF digest script -> S104-C3 OK (all four group digests + global digest recompute), exit 0 [S104-C3]"
  - "node -e final-LF/no-BOM byte script -> S104-C4 OK, exit 0 [S104-C4]"
deferred_integration_checks: [manifest conformance execution (W6-CONF-01, W6-NC-10) in V3]
external_mutations: []
prohibited_actions_observed: []
successor_work_started: false
direct_parent_communication: false
status: AWAITING_WINDOW_REVIEW
```

File created with exactly the S1 §4 literal bytes (two-space indent, one
final LF, no BOM, no trailing spaces): 26 unique case IDs in groups 3/13/4/6
and 13 negative controls, all ascending; the five `DEC-KI-038` digest
literals verified against independent recomputation.

---

## `EV-KI-W6-R18` — S104 independent review disposition

- **Timestamp:** 2026-08-21T00:35:00+05:30
- **Actor/role:** `KI-W6-WINDOW-AGENT` (independent leaf review)
- **Independent inspection:** all four exact check scripts re-executed by
  the window agent — C1 strict parse OK, C2 top-level/group keys,
  3/13/4/6 counts, 26 unique cases, 13 controls, ascending orders all OK,
  C3 all four group digests and the global digest recompute equal to the
  manifest literals, C4 final LF present and no BOM.
- **P1–P2:** assignment identity, ABSENT starting file, and starting
  change-set digest `b94659a0…` (changed set `{F-001, F-002, F-003}`
  recomputed under the §3.1 formula) matched. **V2:** backend delta since
  S103 = exactly the one new fixture. **V3:** required = registered =
  executed = {C1..C4}, zero skips. **H2:** no prohibited action, manifest
  execution, second-file edit, successor work, external mutation, or
  parent communication.
- **Disposition:** `ACCEPTED_FOR_INTEGRATION`.
- **State transition:** S2 records S104 EXECUTED → ACCEPTED;
  `next_subwindow: KI-W6-S105`.
- **External mutations/cost:** the single writable file only; `$0.00`.

---

## `KI-W6-S105` file-subwindow execution certificate

```yaml
certificate: FILE-SUBWINDOW-EXECUTED
parent_window_id: KI-W6
subwindow_id: KI-W6-S105
assignment_id: ASG-KI-W6-S105
agent_identity: KI-W6-S105-LEAF-AGENT
writable_file: frontend/test/browser/keyword-intelligence-e2e.mjs
starting_file_digest: ABSENT
ending_file_digest: 25b30bba733e4d77e3912ae1079448065e035e1e9f58b91887d874430595e7b0
starting_repository_change_set_digest: dc48365f600adb2d36194745f5c6433ee34339626c03bf6f509245661ee2dbcc
attributable_changed_file_set: [frontend/test/browser/keyword-intelligence-e2e.mjs]
required_local_cases: [S105-C1, S105-C2, S105-C3, S105-C4, S105-C5, S105-C6, S105-C7, S105-C8, S105-C9, S105-C10, S105-C11]
registered_local_cases: [S105-C1, S105-C2, S105-C3, S105-C4, S105-C5, S105-C6, S105-C7, S105-C8, S105-C9, S105-C10, S105-C11]
executed_local_cases: [S105-C1, S105-C2, S105-C3, S105-C4, S105-C5, S105-C6, S105-C7, S105-C8, S105-C9, S105-C10, S105-C11]
skipped_local_cases: []
duplicate_case_ids: []
unexpected_case_ids: []
missing_activation_witnesses: []
negative_controls_expected: 0
negative_controls_falsified: 0
commands:
  - "node --check frontend/test/browser/keyword-intelligence-e2e.mjs -> exit 0 [S105-C1]"
  - "grep -cF structural witnesses C2..C5, C7, C9..C11 -> exactly the expected counts (C11: exactly 2 restart sites) [S105-C2..C5, C7, C9..C11]"
  - "grep -cE 'Page.captureScreenshot|review-evidence' -> 0 (exit 1) [S105-C6]"
  - "grep -cF 'kiw6-local-e2e-cookie-secret-0000000000000000000000' -> 0 (exit 1; secret never copied into the emitter) [S105-C8]"
deferred_integration_checks: [execution of all 26 cases, 13 controls, digest recomputation, certificate emission, schema lifecycle assertions — V3 only]
external_mutations: []
prohibited_actions_observed: []
successor_work_started: false
direct_parent_communication: false
status: AWAITING_WINDOW_REVIEW
```

Construction followed S1 §4 S105 steps 1–13 with the accepted
dashboard.mjs CDP/spawn patterns and the A4 authoritative coverage
matrix/substitute-fidelity ledger copied as literal case/control
assertions. Leaf-agent-reported divergences (all resolved in S1's favor;
none weakens an oracle): (1) conformance activations ordered before the
controls so `NC-11` mutates the literal 26-witness map, with `CONF-02/04`
live oracles re-asserted after the controls and in the final manifest-order
pass; (2) A4 `NC-02/NC-11` alternatives not taken — S1's frozen
single-mechanism allocation followed; (3) `W6-NAV-03` hostility realized
via the real backend's valid-but-distinct `/api/runs/<id>` statusUrl (no
response substitution), asserting zero document navigations to it;
(4) RunQuery identity set captured as the 100 unique workspace query texts
cross-checked against durable `queryCount === 100` (frozen snapshot exposes
only the count); (5) `W6-RES-03` corrupt injection after the full expansion
drain with the typed rejection surfacing at the anchor-screen artifact read
(`2/2/2/0`). The known V3 integration risk from `EV-KI-W6-R17` (discovery
identity seam) remains flagged for `I101`.

---

## `EV-KI-W6-R19` — S105 independent review disposition

- **Timestamp:** 2026-08-21T01:05:00+05:30
- **Actor/role:** `KI-W6-WINDOW-AGENT` (independent leaf review)
- **Independent inspection:** all C1–C11 commands re-executed directly by
  the window agent — syntax valid; sole certificate emission site; port
  literal; both frozen exclusion lists; harness/manifest specifiers each
  exactly once; skip-build and database opt-in literals each exactly once
  (the opt-in name is message-built without a second literal occurrence);
  zero screenshot/review tokens; zero cookie-secret copies; cleanup-order
  literal; single absence-witness assertion; exactly two
  `await harness.restartBackend();` sites (restart A post-keyword-faults,
  restart B post-selection-mutation).
- **P1–P2:** assignment identity, ABSENT starting file, and starting
  change-set digest `dc48365f…` (changed set `{F-001..F-004}` recomputed
  under the §3.1 formula) matched. **V2:** frontend delta = exactly the one
  new e2e file beside the two accepted S101/S102 modifications. **V3:**
  required = registered = executed = {C1..C11}, zero skips. **H2:** no
  prohibited action, build/browser/database execution, second-file edit,
  successor work, external mutation, or parent communication.
- **Divergence ruling:** all five divergences stay within S1's frozen
  mechanism allocations; the `W6-NAV-03` realization and the RunQuery
  identity-set capture are recorded for the parent's V3 attention but are
  not S105 defects — the leaf's acceptance basis is structural with zero
  executed behavioral evidence by design.
- **Disposition:** `ACCEPTED_FOR_INTEGRATION`.
- **State transition:** S2 records S105 EXECUTED → ACCEPTED; all five
  leaves accepted; `next: I101` (integration assessment, window agent).
- **External mutations/cost:** the single writable file only; `$0.00`.

---

## `EV-KI-W6-R20` — Integration assessment `KI-W6-I101` (executed by the window agent)

- **Timestamp:** 2026-08-21T01:35:00+05:30
- **Actor/role:** `KI-W6-WINDOW-AGENT` (integration assessment, personally
  executed)
- **Inputs:** assembled window state (S2 v12), actual diffs and ending
  digests of all five files, leaf certificates `KI-W6-S101..S105`,
  review dispositions `EV-KI-W6-R15..R19`.

### Checklist I1–I10

- [x] I1 All five file sub-windows independently accepted
  (`ACCEPTED_FOR_INTEGRATION` in `EV-KI-W6-R15..R19`).
- [x] I2 Assembled changed-file set equals the planned five-path set
  (backend: two untracked W6 paths, V1-9 exact; frontend: two modified W6
  paths + one untracked W6 path, V1-10 exact; five-path set digest
  `d28ae178…` re-verified; set contained by parent-authorized scope).
- [x] I3 Requirement/decision traceability intact (A4 T1–T5 → S101–S105 →
  matrix rows → witnesses; no owned file changed since acceptance).
- [x] I4 Gates executed with witnesses: **V1 PASS** (all 12 rows exact —
  node checks, S104 scripts, S101/S102/S103/S105 command sets, both
  porcelain sets byte-exact); **V2 PASS** (`npm run check` from `frontend/`
  exit 0, fail 0, compiled, `.next` preserved); **V4 PASS** (backend
  `npm test` exit 0 — 677 pass / 0 fail / guarded skips;
  `npm run check:secrets` clean); **V6 PASS** (V6-1/V6-2 empty, V6-3
  exactly `8\t4`, V6-4 all seven pinned hashes byte-equal). **V3 FAIL**
  (deterministic conformance failure; detail below). **V5 not runnable**
  (recomputes the V3 certificate, which was correctly never emitted).
- [ ] I5 Not satisfiable until V3 passes (no certificate to compare).
- [ ] I6 Not satisfiable until V3 passes (controls never executed:
  `controlsExecuted: 0`).
- [x] I7 Substitute-fidelity claims are bounded by the A4 ledger in the
  emitter (structural); R5 integrity proven by V6-2/V6-3; W3/R4 packaging
  unchanged by V6-4. Final behavioral confirmation pending V3.
- [x] I8 No prohibited, successor, external, destructive, secret-bearing,
  or out-of-scope action occurred; no commit/push; production trees outside
  the five paths byte-identical (V6-1/V6-2).
- [x] I9 Current source and complete diffs independently inspected at
  `EV-KI-W6-R15..R19`; gate failures reproduced from the real tree, not
  leaf summaries.
- [x] I10 **PARENT_BLOCKED** — exact blocker below.

### V3 execution record (single run, `KI_W6_SKIP_BUILD=1`)

Command (from `frontend/`): `ALLOW_DATABASE_TESTS=true
KI_W6_SKIP_BUILD=1 node test/browser/keyword-intelligence-e2e.mjs` with the
workspace-provided `TEST_DATABASE_URL` (distinct endpoint from
`DATABASE_URL`; sourced from `email_scraper/.env` without logging).
Outcome: exit 1 in 75 ms; zero cases/controls executed; **no certificate
emitted** (correct per step 13); diagnostics
`KI_W6_OBSOLETE_RUNTIME_MEMBER:[{"path":"components/keyword-intelligence/keyword-dashboard.module.css","pattern":"KeywordSearchVolume","kind":"local"}]`.

### The exact blocker (one)

The frozen A4/S1 obsolete-runtime exclusion oracle, applied exactly as
specified to the real production dependency inventory, fails:
`frontend/components/keyword-intelligence/keyword-dashboard.module.css`
line 2 carries the historical provenance comment "Ports
KeywordSearchVolume/dashboard/index.html:12-467 into module scope.", and
that CSS module is imported by all nine shipped keyword-intelligence
components (including `research-dashboard.tsx`), so it is legitimately
reachable from the A4 T5 item 12 roots. The obsolete standalone runtime is
**not** wired in — this is a naming artifact — but the frozen scan has no
comment exemption, and §6 rule 4 forbids weakening the oracle because
current code fails it. Resolution requires exactly one parent decision:
(a) authorize a scope expansion adding the CSS file (comment removal) as a
corrective sub-window outside the current five-file set; or (b) amend the
A4 `KI-CL-20` oracle definition (e.g., a frozen comment-stripping rule) and
re-freeze the affected S105 assertions; or (c) another parent-chosen
mechanism. Until then V3 can never pass and the window cannot reach
`READY_FOR_PARENT_REVIEW`.

### Secondary recorded defect (non-blocking, in-scope correctable)

On the V3 failure path the S105 cleanup diagnostics labeled step
`schema-absence:failed` although no harness schema had been created (run
aborted at 75 ms pre-harness; `droppedSchema: null`). Independent database
verification: **zero residual `kiw6_` schemas** in the test database (query
`information_schema.schemata` via the isolated test endpoint). The
failure-path labeling should treat "harness never created" distinctly from
"schema survived drop"; reserved for the next corrective window per §6.

### Disposition

`PARENT_BLOCKED` per §5.3 ("missing parent decision, contradiction, or
required scope expansion → stop and report one exact blocker to the
parent"). No corrective sub-window is assigned (§6 rule 7: unresolved
parent decision requires escalation). Gate evidence V1/V2/V4/V6 remains
valid; V3/V5 must rerun after the parent decision. External mutations
beyond the five owned files: none. Cost: `$0.00` (one local gate run; no
paid provider, AWS, or production action).

---

## `EV-KI-W6-R21` — Parent decision (b) recorded; S1 oracle re-frozen

- **Timestamp:** 2026-08-21T01:50:00+05:30
- **Actor/role:** `KI-W6-WINDOW-AGENT` (recording parent decision resolving the
  `EV-KI-W6-R20` blocker)
- **Parent decision (user, parent authority):** option **(b)** — amend the
  obsolete-runtime oracle definition with a frozen comment-stripping rule
  and re-freeze the affected S105 assertions. The A4 `KI-CL-20`-side
  mirroring of this decision (A4 text, A5 CAS, A6 evidence, A7 changelog)
  belongs to the parent session; the window agent does not edit A-artifacts
  and records the decision's window-side mechanical trace here.
- **Frozen comment-stripping rule (now part of the S1 S105 step 9 oracle):**
  before `FORBIDDEN_LOCAL_PATH_PATTERNS` / `FORBIDDEN_RUNTIME_HOSTS` are
  applied to a resolved inventory member's contents, strip comments —
  `.css`: non-greedy `/* … */` block comments; `.js/.mjs/.ts/.tsx`: the
  same block comments plus full-line `//` line comments (optional leading
  whitespace; `^`-anchored per line so protocol separators inside strings
  are never touched); all other files (including `.json`) are scanned
  verbatim; member **paths** are matched unstripped. The rule is
  deterministic, fail-closed toward real code (trailing same-line comments
  remain scanned), and applies identically to the S105 implementation and
  the `I101`/`I102` gate rerun.
- **Rationale preserved for review:** the sole real-tree hit was the
  provenance *comment* "Ports KeywordSearchVolume/dashboard/index.html…"
  at `frontend/components/keyword-intelligence/keyword-dashboard.module.css:2`;
  the shipped module does not wire the obsolete standalone runtime.
- **Scope of the corrective window `KI-W6-C101` (one file, inside the
  parent five-file scope):** (A) implement the frozen stripping rule at the
  `obsoleteExclusion` content checks; (B) fix the already-diagnosed
  `EV-KI-W6-R20` failure-path diagnostics defect so the `schema-absence`
  cleanup step reports `ok` when no harness schema was ever created and
  `failed` only when a created schema survives its drop verification.
- **S1 amendments applied with this decision:** S105 step 9 oracle text;
  new check `S105-C12`; `V1-12` row extended to C12. New S1 revision is
  recorded in S2 state v14.
- **External mutations/cost:** coordination files only; `$0.00`.

---

## Corrective sub-window readiness certificate — `KI-W6-C101`

```yaml
certificate: CORRECTIVE-SUBWINDOW-READY
parent_window_id: KI-W6
subwindow_id: KI-W6-C101
type: FILE
corrects: [EV-KI-W6-R20 blocker (parent decision (b) recorded in EV-KI-W6-R21), EV-KI-W6-R20 secondary failure-path diagnostics defect]
writable_file: frontend/test/browser/keyword-intelligence-e2e.mjs
file_operation: MODIFY
predecessors: [KI-W6-S105]
starting_file_digest: 25b30bba733e4d77e3912ae1079448065e035e1e9f58b91887d874430595e7b0
decomposition_revision: 3487d71a761f990adc23e2b0c1221fd33f0dd6c7c943a96fea6452fded6b7533
authorized_actions:
  - "insert the frozen helper after the two FORBIDDEN list literals: const stripComments = (filePath, text) => { if (filePath.endsWith(\".css\")) return text.replace(/\\/\\*[\\s\\S]*?\\*\\//g, \"\"); if (/\\.(js|mjs|ts|tsx)$/u.test(filePath)) return text.replace(/\\/\\*[\\s\\S]*?\\*\\//g, \"\").replace(/^[ \\t]*\\/\\/[^\\n]*/gm, \"\"); return text; };"
  - "inside obsoleteExclusion, replace the two content checks with const content = stripComments(member.path, member.content || \"\"); then member.path.includes(pattern) || content.includes(pattern) and content.includes(host)"
  - "schema-absence cleanup step: return ok when no harness schema was ever created (harness === null and harnessCloseState.result === null); otherwise keep the existing zero-row absence assertion"
prohibited_actions: [every other edit, oracle weakening beyond the frozen stripping rule, pattern-list changes, build/browser/database execution during the leaf]
parent_findings_unresolved: []
status: READY_FOR_DISPATCH
```

Dispatch follows immediately (single corrective leaf, window-agent managed).

---

## Corrective sub-window readiness certificates — `KI-W6-C102` and `KI-W6-C103`

```yaml
certificate: CORRECTIVE-SUBWINDOW-READY
parent_window_id: KI-W6
subwindow_id: KI-W6-C102
type: FILE
corrects: "V3 run 2 cleanup failure: Prisma raw queries cannot deserialize the information_schema `name`/`sql_identifier` column type on the DIRECT (non-pooler) connection, regardless of row count (empirically reproduced this session: direct zero-row uncast THROWS; direct one-row uncast THROWS; ::text cast OK both) — the accepted isolated-postgres.js helper itself casts every catalog select ::text (current_schema()::text at line 71) for this exact reason"
writable_file: email_scraper/test/helpers/keyword-intelligence-e2e-harness.js
file_operation: MODIFY
starting_file_digest: 93ee3a3b31275a84babe27e3b37519bb4b86e3bd1571485f3bf3486c3b8c5a26
authorized_actions:
  - "in close(), replace the absence-query EXECUTION with the ::text-cast wrapper subquery selecting from the frozen SCHEMA_ABSENCE_QUERY constant: const rows = await admin.$queryRawUnsafe(`SELECT schema_name::text AS schema_name FROM (${SCHEMA_ABSENCE_QUERY.replace(/;\\s*$/, \"\")}) kiw6_absence_probe`, schema);"
  - "the frozen constant literal (S103-C11) and the absenceWitness { query: SCHEMA_ABSENCE_QUERY, rowCount: 0 } contract stay byte-identical; the wrapper selects exactly the frozen query's rows with only the Prisma-safe column cast"
prohibited_actions: [every other edit, constant changes, witness changes, new raw queries]
```

```yaml
certificate: CORRECTIVE-SUBWINDOW-READY
parent_window_id: KI-W6
subwindow_id: KI-W6-C103
type: FILE
corrects: "V3 run 2 main failure: first-seed Add lost to the React hydration race — the e2e used a fixed 150ms wait instead of the accepted dashboard.mjs pattern, which confirms every Add with a chip-count waitFor (dashboard.mjs:1131-1133: setInputValue -> click Add -> waitFor '1/5')"
writable_file: frontend/test/browser/keyword-intelligence-e2e.mjs
file_operation: MODIFY
starting_file_digest: 7976b705eb44d7e9b75cd8fa5b475e86224e687ecd281ad041194f98ddbe7822
authorized_actions:
  - "replace the seed loop's fixed await wait(150) with the accepted per-seed confirmation: await waitFor(cdp, `document.querySelector('#seed-chip-count')?.textContent.includes('${seedIndex + 1}/5')`, `seed chip ${seedIndex + 1}/5`) via for (const [seedIndex, seed] of SEEDS.entries())"
prohibited_actions: [every other edit, oracle changes, selector changes]
```

Environmental note recorded with these certificates: the user (parent/requester
authority) committed the five-file W6 work as frontend `0bb0376` and backend
`ecc1a71` ("KI-W6"); the pinned V6 baseline commits still resolve and the
V6-1/V6-2/V6-3 diffs remain exact with the five W6 paths excluded. The
window agent commits nothing.

---

## `KI-W6-C103` amendment 1 — bounded re-attempt drive mechanism

V3 run 3 (post-C103) failed deterministically at seed 1/5: the per-seed
waitFor correctly converted the hydration race into a deterministic
failure. Root cause at component level confirmed: `research-form.tsx` is a
controlled input (`manualInput` state via `addManualSeeds()`); an
InputEvent dispatched before React hydration completes never reaches React
state, so Add is a no-op. `dashboard.mjs` uses the same immediate sequence
(its R5 pass predates current build state and is not re-executed in W6).
Authorized amendment (drive mechanism only; no oracle change — the final
`5/5` waitFor, the exactly-one-create-POST assertion, and all case oracles
are unchanged): wrap each seed's setInputValue+Add in up to three attempts,
each confirmed by the short-timeout (1500 ms) chip-count waitFor; throw if
unconfirmed after the third attempt. Component-level duplicate-seed
skipping makes a redundant attempt a no-op.

---

## `KI-W6-C103` amendment 2 — controlled-input state settle

The isolated browser probe reproduced the form behavior: the exact native
setter/InputEvent plus JS click succeeds when a short settle occurs between
input dispatch and click; the e2e clicked immediately after dispatch. The
controlled `manualInput` state therefore had not committed before
`addManualSeeds()` read it. Add exactly `await wait(100);` between
`setInputValue` and the Add click in the bounded per-seed attempt loop.
This changes only the browser drive timing; per-seed chip confirmation,
final 5/5 oracle, one-create-POST oracle, and all coverage/control semantics
remain unchanged.

---

## Continued V3 attempts after `EV-KI-W6-R21` (records preserved)

These records are append-only continuation evidence. They do not replace
`EV-KI-W6-R20` or `EV-KI-W6-R21`, and no certificate was emitted.

### Attempt A — anchor behavior reached

- **Command:** from `frontend/`, `ALLOW_DATABASE_TESTS=true
  KI_W6_SKIP_BUILD=1 node --env-file=../email_scraper/.env
  test/browser/keyword-intelligence-e2e.mjs`
- **Outcome:** seed creation passed after the bounded trusted-input drive;
  browser/auth/startup and isolated-schema cleanup passed; failure was
  `anchor drain must make one request and store one artifact`.
- **Diagnostics:** `wallTimeMs=177577`, `casesExecuted=0`,
  `controlsExecuted=0`, `droppedSchema` was removed successfully,
  cleanup steps were `browser:ok`, `next-server:ok`, `auth-server:ok`,
  `backend-server:ok`, `schema-absence:ok`, `temp-root:ok`.
- **Interpretation:** the anchor provider call was reached; the harness
  report counted the anchor task artifact together with the required
  anchor-stage shortlist manifest.

### Attempt B — corrected artifact and queue accounting

- **Changes exercised:** task-result artifact reports exclude aggregate
  `manifest.json`/`result.json` objects; the overall immutable-put oracle
  still counts the complete trace and remains `23`; the keyword fault driver
  prepares initialization before applying duplicate/reorder faults; the
  expansion report retains the pre-drain initialization sends.
- **Intermediate outcomes:** anchor artifact assertion passed and the frozen
  `42` queue-send assertion passed. Two retries independently hit the known
  isolated-DB Prisma interactive-transaction timeout
  (`keywordResearch.updateMany`, 5-second timeout); cleanup was successful in
  both cases. One retry reached publication and failed the next assertion.
- **Decisive outcome:** `publishedSnapshot.keywordResult` was
  `{visible:true,rowCount:300,defaultSelectionItemCount:100}` while the frozen
  S105 oracle requires `rowCount=200`; no certificate was emitted.
- **Diagnostics:** decisive run `wallTimeMs=153284`,
  `casesExecuted=0`, `controlsExecuted=0`, cleanup fully successful, and the
  disposable schema was dropped and absence-verified.

### Current blocker

The production provider formula frozen by S1/A4 is the same formula used by
the authoritative worker fixtures: overview items use
`main_intent = index % 3 === 0 ? "transactional" : "commercial"`. It therefore
does not create informational rows. The production aggregator receives 300
US anchor metrics, applies the 200-item shortlist only to the subsequent
market-task fan-out, and the final `computeResearchResult` retains the 300
anchor-backed rows. The current S105 oracle simultaneously requires 200 final
rows. This is an authoritative contract/acceptance contradiction outside the
two-file corrective mechanism; V3 remains blocked pending a parent decision.

---

## `EV-KI-W6-R22` — State-149 shortlist-correction decomposition readiness

- **Timestamp:** 2026-08-21T13:25:00+05:30
- **Actor/role:** `KI-W6-WINDOW-AGENT`; coordination authoring only.
- **Authority:** state 149 / `ASG-KI-W6-WA-02` authorizes S1/S2/S3 reconciliation,
  C104→C105→I102 authoring, and return for parent review only. Its pins were
  rechecked: contract `8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c`,
  decision `4bb1201594bc4a33bf868f19dd73c6777d046cdbb8ae70ef2cc8972dd6c342ad`,
  checklist `a499afe117ee9b9dba07ab1a420d8a9bae824d6d5d7419374427f9cc0687fa63`,
  and active state `49795fe367d86347b27bdf7aee8e7b730e18c7ecbbd136e3acf5be7de69d2620`.
- **Diagnosis:** V3 reached fenced publication with `rowCount:300`; DEC-KI-039
  fixes this as an `aggregateMarket` production defect, not an oracle defect.
- **Authored artifacts:** S1 revision
  `c305f7eb42dcef07ba19d7044d52b85bdc4e629458b7b363c49ce90e9cd1c69e`
  contains C104, C105, and I102. S2 state 14 revision
  `32a162502cee6e30643451909f3acc1a1b8afa5453d8b399e37e36067e50ade7`
  is `AWAITING_PARENT_DECOMPOSITION_REVIEW`. The 26 existing cases and 13
  existing controls are unchanged. C104/C105 baselines equal parent-pinned
  hashes `c37a038f189470ad1d2eca6626f515b9f0c45bd60de470d84c4b72fa497637b5`
  and `f0e8be1a29d9ed5d85a657b8e73083f6c603ca30b18121701b3a33a7c1938510`.
- **Verification:** `git diff --check` exits 0. Only the three authorized
  coordination artifacts (S1/S2 and this S3 entry) changed; no
  implementation/test/build/browser/database/provider/AWS/production/
  destructive/commit/push/KI-W7 action occurred. Cost `$0.00`.

### Corrective readiness certificate — `KI-W6-C104`

```yaml
certificate: CORRECTIVE-SUBWINDOW-READY
parent_window_id: KI-W6
corrective_subwindow_id: KI-W6-C104
window_agent_identity: KI-W6-WINDOW-AGENT
trigger_evidence: [EV-KI-W6-R20, continued V3 Attempt B, EV-KI-W6-R22]
root_cause: aggregateMarket supplies all expansion candidates and US anchor metrics to computeResearchResult without reading/projecting the immutable shortlist.
governing_parent_requirements: [REQ-KI-002, REQ-KI-003, REQ-KI-023, REQ-KI-024, INV-KI-004, INV-KI-005, INV-KI-014]
governing_parent_decisions: [DEC-KI-006, DEC-KI-024, DEC-KI-038, DEC-KI-039]
corrected_prior_subwindows: [KI-W6-I101]
writable_file: email_scraper/src/aws-pipeline/keyword-intelligence/service.js
starting_file_digest: c37a038f189470ad1d2eca6626f515b9f0c45bd60de470d84c4b72fa497637b5
predecessors: [KI-W6-I101]
invalidated_evidence: [failed V3 acceptance attempts, old service-hash proof, original V6 unchanged-service claim]
invalidated_gates: [CV1, CV3, CV4, CV5, CV6]
unresolved_parent_decisions: []
expanded_parent_scope_required: false
section_7_fields_complete: true
single_file_write_set: true
unresolved_execution_choices: []
next_integration_assessment_id: KI-W6-I102
status: READY
```

### Corrective readiness certificate — `KI-W6-C105`

```yaml
certificate: CORRECTIVE-SUBWINDOW-READY
parent_window_id: KI-W6
corrective_subwindow_id: KI-W6-C105
window_agent_identity: KI-W6-WINDOW-AGENT
trigger_evidence: [EV-KI-W6-R22, KI-W6-C104]
root_cause: aggregationScaffold lacks the shortlist manifest newly consumed by aggregateMarket and its three-item fixture cannot prove the 300-to-200 boundary.
governing_parent_requirements: [REQ-KI-002, REQ-KI-003, REQ-KI-023, REQ-KI-024, INV-KI-004, INV-KI-005, INV-KI-014]
governing_parent_decisions: [DEC-KI-024, DEC-KI-038, DEC-KI-039]
corrected_prior_subwindows: [KI-W6-I101]
writable_file: email_scraper/test/keyword-intelligence-worker-flow.test.js
starting_file_digest: f0e8be1a29d9ed5d85a657b8e73083f6c603ca30b18121701b3a33a7c1938510
predecessors: [KI-W6-C104 ACCEPTED_FOR_INTEGRATION]
invalidated_evidence: [old aggregation-scaffold substitute-fidelity evidence]
invalidated_gates: [CV1, CV3, CV4, CV5, CV6]
unresolved_parent_decisions: []
expanded_parent_scope_required: false
section_7_fields_complete: true
single_file_write_set: true
unresolved_execution_choices: []
next_integration_assessment_id: KI-W6-I102
status: READY
```

### I102 readiness and disposition

I102 has no implementation write authority. It reruns CV1/CV3/CV4/CV5/CV6;
CV2 remains reusable only with the exact clean-frontend/committed-HEAD proof.
The causal V3 oracle remains 19 calls, 23 immutable objects, 42 sends,
`$0.49200000`, 300 anchor, 200 shortlist, 200 durable/UI rows, default 100,
complete cleanup, and the unchanged 26 cases/13 controls. Full DB suites,
Prisma generate/validate, seven-handler builds, and duplicate frontend builds
remain prohibited.

**Disposition:** `AWAITING_PARENT_DECOMPOSITION_REVIEW`. No C104/C105
assignment, execution, test, gate, or successor work is authorized. KI-W7
remains prohibited.

---

## `EV-KI-W6-R23` — State-150 superseding corrective-decomposition readiness

- **Timestamp:** 2026-08-21T13:35:00+05:30
- **Actor/role:** `KI-W6-WINDOW-AGENT`; documentation-only reconciliation.
- **Authority:** A5 state 150 / `ASG-KI-W6-WA-02`, `EV-KI-A-089` F15–F18,
  and `CHG-KI-062`. No product decision, implementation design, scope,
  coverage membership, or gate changed.
- **F15 corrected:** C104's literal clean combined-repository baseline is
  `e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855`;
  C105's literal one-member post-C104 baseline is
  `55d5f0b43f8cc3466478169f48d23cb546f829f4f597c393c326621f9d7be9e0`.
- **F16 corrected:** both leaf `read_only_scope` arrays now name only canonical
  workspace-relative paths or exact, resolvable parent-document sections.
- **F17 corrected:** C105 now explicitly lists `REQ-KI-002/003/023/024`,
  `INV-KI-004/005/014`, `DEC-KI-006/024/038/039`, `KI-W6-CT2`,
  `SCN-KI-041`, `W6-FLOW-04/05/06`, and `W6-NC-05`.
- **F18 corrected:** C104-C2 and C105-C2 now contain exact `node
  --input-type=module -e` commands, working directories, source bounds,
  activation assertions, fail conditions, exit result, read-only write set,
  and explicit forbidden operations. They are LOCAL_NOW inspections only.
- **Revisions:** S1 is
  `6b7e90944a9167b24d42c61fcb26b3d7e692bae6b7319b48d94c86503b4b93b2`;
  S2 state 15 is
  `1659b93c6a716ffcc611c414ddc98cc62dc83eda1ae13d2399dfb662537dae59`.
  R22's readiness claims are superseded only to the F15–F18 extent named by
  `CHG-KI-062`; its diagnosis, algorithm, seven-path scope, sequence, case/
  control registry, and gate plan remain valid.
- **Verification:** `git diff --check` exits 0; both nested repositories are
  clean. No implementation/test/build/browser/database/provider/AWS/
  production/destructive/commit/push/KI-W7 action occurred. Cost `$0.00`.

```yaml
certificate: CORRECTIVE-DECOMPOSITION-READY
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-02
window_agent_identity: KI-W6-WINDOW-AGENT
trigger_evidence: [EV-KI-A-089, CHG-KI-062]
supersedes: [EV-KI-W6-R22 C104/C105 section_7_fields_complete and READY claims]
corrective_subwindows: [KI-W6-C104, KI-W6-C105]
next_integration_assessment_id: KI-W6-I102
governing_trace:
  KI-W6-C104:
    requirements: [REQ-KI-002, REQ-KI-003, REQ-KI-023, REQ-KI-024]
    invariants: [INV-KI-004, INV-KI-005, INV-KI-014]
    decisions: [DEC-KI-006, DEC-KI-024, DEC-KI-038, DEC-KI-039]
    task_scenario_case_control: [KI-W6-CT1, SCN-KI-041, W6-FLOW-05, W6-NC-05]
  KI-W6-C105:
    requirements: [REQ-KI-002, REQ-KI-003, REQ-KI-023, REQ-KI-024]
    invariants: [INV-KI-004, INV-KI-005, INV-KI-014]
    decisions: [DEC-KI-006, DEC-KI-024, DEC-KI-038, DEC-KI-039]
    task_scenario_case_control: [KI-W6-CT2, SCN-KI-041, W6-FLOW-04, W6-FLOW-05, W6-FLOW-06, W6-NC-05]
repository_change_set_digests:
  KI-W6-C104: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
  KI-W6-C105: 55d5f0b43f8cc3466478169f48d23cb546f829f4f597c393c326621f9d7be9e0
section_7_fields_complete: true
single_file_write_sets: true
unresolved_parent_decisions: []
expanded_parent_scope_required: false
unresolved_execution_choices: []
leaf_dispatch_authorized: false
integration_gate_execution_authorized: false
may_start_successor: false
status: AWAITING_PARENT_DECOMPOSITION_REVIEW
```

**Disposition:** the corrected C104→C105→I102 package is returned for renewed
parent decomposition review. C104/C105 remain `UNASSIGNED`; I102 remains
unstarted; KI-W7 remains prohibited.

---

## `EV-KI-W6-R24` — State-151 anti-vacuity corrective-decomposition readiness

- **Timestamp:** 2026-08-21T13:35:09+05:30
- **Actor/role:** `KI-W6-WINDOW-AGENT`; documentation-only reconciliation.
- **Authority:** A5 state 151 / `ASG-KI-W6-WA-02`, `EV-KI-A-090` F19–F20,
  and `CHG-KI-063`. Only C104-C2, C105-C2, and dependent readiness records
  changed. The product correction, test design, canonical scopes, explicit
  governing IDs, digests, sequence, case/control membership, and I102 schedule
  remain unchanged.
- **F19 corrected:** C104-C2 now locates one guarded `invariant()` witness for
  `projectedExpansion` and a different guarded witness for
  `projectedUsMetrics`. Each witness requires its projection and
  `shortlistKeys` in the guard condition, follows that projection's normalized
  `new Set`/`keywordKey` construction, and occurs before
  `computeResearchResult`. The unrelated anchor-context invariant cannot
  satisfy either witness.
- **F20 corrected:** C105-C2 now bounds the one `SCN-KI-041` source block from
  its `test("SCN-KI-041:...")` declaration to the next test or EOF. Inside
  that block it requires literal 300/200 output witnesses, the exact captured
  default-selection oracle `holder.publishedInput.selectionItems.length ===
  100`, normalized result/shortlist set equality, and the exact zero-result-key
  outside-shortlist assertion. Later source cannot satisfy an SCN-KI-041
  witness.
- **Revisions:** S1 is
  `b99633447c17163f6e883d71388b0200a345d2c0ced51252b8d03a8fba3b6b38`;
  S2 state 16 is
  `6abda9af61c54653c5de0e3abaea4fa279c5b9bdf08dc3f41b42a359b1eb6bed`.
  R23's F18 and `section_7_fields_complete` readiness claims are superseded
  only to the F19/F20 extent defined by `CHG-KI-063`; F15–F17 and all
  substantive correction decisions remain valid.
- **Verification:** `git diff --check` exits 0; both nested repositories are
  clean. No implementation/test/build/browser/database/provider/AWS/
  production/destructive/commit/push/KI-W7 action occurred. Cost `$0.00`.

```yaml
certificate: CORRECTIVE-DECOMPOSITION-READY
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-02
window_agent_identity: KI-W6-WINDOW-AGENT
trigger_evidence: [EV-KI-A-090, CHG-KI-063]
supersedes: [EV-KI-W6-R23 F18 and section_7_fields_complete readiness claims]
corrective_subwindows: [KI-W6-C104, KI-W6-C105]
next_integration_assessment_id: KI-W6-I102
repository_change_set_digests:
  KI-W6-C104: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
  KI-W6-C105: 55d5f0b43f8cc3466478169f48d23cb546f829f4f597c393c326621f9d7be9e0
f19_c104_c2_independent_guards: [projectedExpansion, projectedUsMetrics]
f20_c105_c2_bounded_oracles: [default_selection_length_100, zero_result_key_outside_shortlist]
section_7_fields_complete: true
single_file_write_sets: true
unresolved_parent_decisions: []
expanded_parent_scope_required: false
unresolved_execution_choices: []
leaf_dispatch_authorized: false
integration_gate_execution_authorized: false
may_start_successor: false
status: AWAITING_PARENT_DECOMPOSITION_REVIEW
```

**Disposition:** the state-151-corrected C104→C105→I102 package is returned
for renewed parent decomposition review. C104/C105 remain `UNASSIGNED`; I102
remains unstarted; KI-W7 remains prohibited.

---

## `EV-KI-W6-R25` — State-152 approval acknowledgement and C104 dispatch

- **Timestamp:** 2026-08-21T13:41:36+05:30
- **Parent/window authority:** A5 state 152 `DECOMPOSITION_APPROVED`,
  `ASG-KI-W6-WA-02`, `EV-KI-A-091`, and `CHG-KI-064`. The approved S1 revision
  is exactly `b99633447c17163f6e883d71388b0200a345d2c0ced51252b8d03a8fba3b6b38`.
- **Dispatch:** S2 state 17 records `KI-W6-C104` as the sole active assignment:
  `ASG-KI-W6-C104` to `KI-W6-C104-LEAF-AGENT`. Its sole writable file is
  `email_scraper/src/aws-pipeline/keyword-intelligence/service.js`; its frozen
  baseline is `c37a038f189470ad1d2eca6626f515b9f0c45bd60de470d84c4b72fa497637b5`
  and its repository change-set baseline is
  `e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855`.
- **Frozen local acceptance:** C104 may perform only C104-C1 and C104-C2 and
  return one certificate to the window agent at `AWAITING_WINDOW_REVIEW`.
  C104-C2 includes both independent projection-specific equality-guard
  witnesses before `computeResearchResult`; no C105 test execution is allowed
  during the prescribed intermediate state.
- **Sequence hold:** C105 remains `UNASSIGNED` pending independent C104
  acceptance; I102 remains unstarted pending acceptance of both C104 and C105.
  No implementation, local check, gate, external operation, or leaf evidence
  has occurred under `ASG-KI-W6-C104` at dispatch time.
- **State revision:** S2 state 17 is
  `39c654caf8c1d62b3897af1558e40f3d343614621fa0679dbca240c6550faee2`.
  This record changes no product decision, coverage ID, manifest membership,
  S1 task, or authority outside the approved dispatch.

```yaml
certificate: CORRECTIVE-SUBWINDOW-DISPATCHED
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-02
subwindow_id: KI-W6-C104
assignment_id: ASG-KI-W6-C104
assigned_agent: KI-W6-C104-LEAF-AGENT
writable_file: email_scraper/src/aws-pipeline/keyword-intelligence/service.js
starting_file_digest: c37a038f189470ad1d2eca6626f515b9f0c45bd60de470d84c4b72fa497637b5
starting_repository_change_set_digest: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
required_local_checks: [C104-C1, C104-C2]
predecessors: [KI-W6-I101]
successor_reservation: C105 after independent C104 acceptance only
integration_assessment_reservation: I102 after C104 and C105 acceptance only
external_mutations: []
prohibited_actions_observed: []
status: READY
```

**Disposition:** C104 is dispatched and awaits its leaf evidence. C105,
I102, and KI-W7 remain prohibited from starting.

---

## `EV-KI-W6-R26` — C104 independent window review: parent-blocked provenance

- **Timestamp:** 2026-08-21T13:50:18+05:30
- **Window/sub-window/assignment:** `KI-W6` / `KI-W6-C104` /
  `ASG-KI-W6-C104`; reviewer `KI-W6-WINDOW-AGENT` under A5 state 152.
- **Frozen revisions:** parent state
  `84e35abf369bfcaf11069b0a21e17744b160da48329f53dde5cb3c52ea4f8b00`;
  contract `8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c`;
  decision `4bb1201594bc4a33bf868f19dd73c6777d046cdbb8ae70ef2cc8972dd6c342ad`;
  parent checklist `a499afe117ee9b9dba07ab1a420d8a9bae824d6d5d7419374427f9cc0687fa63`;
  S1 `b99633447c17163f6e883d71388b0200a345d2c0ced51252b8d03a8fba3b6b38`;
  and S2 state 18
  `8b70d60feed1e3680441bdfec231b6b6dcf61af62ce8c96eae84d9297a4fd3eb`.
- **Reported leaf result:** the received C104 completion report identifies only
  `email_scraper/src/aws-pipeline/keyword-intelligence/service.js`, reports
  C104-C1/C104-C2 and `git diff --check` passing, ending SHA-256
  `b85ce80098792faf7c781effe648d86452f61b857a8cd737b037940fdce12b02`,
  and claims no commit.
- **Independent source/digest review:** current `aggregateMarket` reads the
  strict shortlist manifest, creates normalized shortlist keys, projects
  expansion and US metrics, applies distinct guards before
  `computeResearchResult`, and supplies the projected expansion/overview.
  `sha256sum email_scraper/src/aws-pipeline/keyword-intelligence/service.js`
  returned exactly the reported ending digest.
- **Independent local checks:** from `email_scraper/`, C104-C1
  `node --check src/aws-pipeline/keyword-intelligence/service.js` passed.
  The byte-for-byte frozen C104-C2 `node --input-type=module -e` inspection in
  S1 passed: it activated the bounded `aggregateMarket` extraction, exact one
  shortlist contract/schema references, both distinct projection-specific
  equality guards, normalized-set witnesses, and pre-calculation ordering.
  `git diff --check` passed at both root and backend scope. A compound status
  command ended after those successful checks because `git -C frontend` was
  resolved relative to `email_scraper/`; the immediate corrected root-relative
  status query completed successfully and both nested worktrees were clean.
- **Provenance conflict:** read-only Git inspection reports backend `HEAD`
  `9eff81490d15f6c001bf30121133f538addb81bf`, author `Harit`, subject `C104`,
  with exactly one file changed (`service.js`, 26 insertions, 3 deletions).
  `HEAD:service.js` has the same ending digest, while the frozen C104 baseline
  was `c37a038f189470ad1d2eca6626f515b9f0c45bd60de470d84c4b72fa497637b5`.
  This directly conflicts with the submitted no-commit claim and prevents the
  required no-prohibited-action evidence from being established. The review
  does not attribute that commit to a particular actor.
- **Scope/negative result:** current backend and frontend porcelain are clean;
  the observed commit contains only the C104 writable file. No C105/I102,
  provider, AWS, database, destructive, or KI-W7 action was observed during
  review. No external mutation or cost occurred during review.
- **Disposition:** `PARENT_BLOCKED`. S2 state 18 preserves the source and
  evidence, stops successor work, and awaits parent disposition of the
  commit-provenance conflict. C104 is not accepted; C105 remains unassigned;
  I102 remains unstarted.

```yaml
certificate: WINDOW-AGENT-FILE-REVIEW
parent_window_id: KI-W6
subwindow_id: KI-W6-C104
assignment_id: ASG-KI-W6-C104
reviewer: KI-W6-WINDOW-AGENT
starting_file_digest: c37a038f189470ad1d2eca6626f515b9f0c45bd60de470d84c4b72fa497637b5
ending_file_digest: b85ce80098792faf7c781effe648d86452f61b857a8cd737b037940fdce12b02
starting_repository_change_set_digest: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
observed_head: 9eff81490d15f6c001bf30121133f538addb81bf
observed_head_changed_files: [email_scraper/src/aws-pipeline/keyword-intelligence/service.js]
local_checks: [C104-C1 PASS, C104-C2 PASS, git-diff-check PASS]
required_local_cases: [C104-C1, C104-C2]
registered_local_cases: [C104-C1, C104-C2]
executed_local_cases: [C104-C1, C104-C2]
skipped_local_cases: []
duplicate_case_ids: []
unexpected_case_ids: []
missing_activation_witnesses: []
prohibited_actions_observed: [backend committed HEAD C104 9eff81490d15f6c001bf30121133f538addb81bf; actor attribution unresolved]
external_mutations: []
cost_usd: '0.00'
successor_work_started: false
status: PARENT_BLOCKED
```

**Parent action required:** determine whether the committed backend `HEAD`
`C104` revision is authorized parent-owned provenance or an impermissible leaf
commit. Until that disposition, no C104 acceptance, C105 dispatch, I102 gate,
or KI-W7 action may begin.

---

## `EV-KI-W6-R27` — State-153 C104 acceptance and C105 dispatch

- **Timestamp:** 2026-08-21T13:54:41+05:30
- **Authority/disposition:** A5 state 153, `EV-KI-A-092`, and `CHG-KI-065`
  classify backend commit `9eff81490d15f6c001bf30121133f538addb81bf` as
  requester-owned provenance. It contains exactly C104's reviewed file and
  matches R26's accepted ending digest; it is neither a prohibited leaf action
  nor a window-agent action. No source, Git history, local check, or gate rerun
  is authorized or required by this disposition.
- **C104 acceptance:** R26's independent source inspection, ending digest
  `b85ce80098792faf7c781effe648d86452f61b857a8cd737b037940fdce12b02`,
  C104-C1 pass, C104-C2 pass, exact one-file commit scope, zero skipped/
  duplicate/unexpected local IDs, and no external mutation/cost are accepted
  unchanged. `KI-W6-C104` is `ACCEPTED_FOR_INTEGRATION`.
- **C105 dispatch:** S2 state 19 assigns only `KI-W6-C105` /
  `ASG-KI-W6-C105` to `KI-W6-C105-LEAF-AGENT`. Its sole writable file is
  `email_scraper/test/keyword-intelligence-worker-flow.test.js`; frozen starting
  file digest is `f0e8be1a29d9ed5d85a657b8e73083f6c603ca30b18121701b3a33a7c1938510`
  and repository change-set digest is
  `55d5f0b43f8cc3466478169f48d23cb546f829f4f597c393c326621f9d7be9e0`.
  It may run only C105-C1/C105-C2 and must stop at `AWAITING_WINDOW_REVIEW`.
- **Sequence hold:** I102 remains unstarted until independent C105 acceptance.
  No C105 implementation, local check, gate, provider, AWS, database,
  destructive, commit, push, or KI-W7 action occurred at dispatch time.
- **State revision:** S2 state 19 is
  `927fbec7ee3e77ac79d433e5acbd1d46f86bc5a2d1faecd2dce1cd212ed7242b`.

```yaml
certificate: WINDOW-AGENT-FILE-ACCEPTED
parent_window_id: KI-W6
subwindow_id: KI-W6-C104
assignment_id: ASG-KI-W6-C104
reviewer: KI-W6-WINDOW-AGENT
ending_file_digest: b85ce80098792faf7c781effe648d86452f61b857a8cd737b037940fdce12b02
local_checks: [C104-C1 PASS, C104-C2 PASS, git-diff-check PASS]
provenance_disposition: requester-owned commit 9eff81490d15f6c001bf30121133f538addb81bf accepted by EV-KI-A-092
status: ACCEPTED_FOR_INTEGRATION
```

```yaml
certificate: CORRECTIVE-SUBWINDOW-DISPATCHED
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-02
subwindow_id: KI-W6-C105
assignment_id: ASG-KI-W6-C105
assigned_agent: KI-W6-C105-LEAF-AGENT
writable_file: email_scraper/test/keyword-intelligence-worker-flow.test.js
starting_file_digest: f0e8be1a29d9ed5d85a657b8e73083f6c603ca30b18121701b3a33a7c1938510
starting_repository_change_set_digest: 55d5f0b43f8cc3466478169f48d23cb546f829f4f597c393c326621f9d7be9e0
required_local_checks: [C105-C1, C105-C2]
predecessors: [KI-W6-C104 ACCEPTED_FOR_INTEGRATION]
integration_assessment_reservation: I102 after independent C105 acceptance only
external_mutations: []
prohibited_actions_observed: []
status: READY
```

**Disposition:** C104 is accepted. C105 is dispatched and awaits leaf
evidence; I102 and KI-W7 remain prohibited from starting.

---

## `EV-KI-W6-R27` — C105 independent window-agent acceptance

- **Timestamp:** 2026-08-21T14:10:00+05:30
- **Actor/role:** `KI-W6-WINDOW-AGENT` (independent leaf review)
- **Predecessor:** `KI-W6-C104` accepted; C105 assignment, writable path,
  starting digest, and change-set digest matched S2/S1.
- **Ending digest:** `f549f9ac16e2c31957dd3a03b11d54da15972f4af23ebcfecb6f8c16f8955d9f`.
- **Independent checks:** C105-C1 `node --check` passed; C105-C2 exact
  bounded-source inspection passed. Required = registered = executed
  `[C105-C1, C105-C2]`; zero skips, duplicates, unexpected IDs, or local
  controls.
- **Independent diff/scope review:** the only changed path relative to the
  C104 commit is `test/keyword-intelligence-worker-flow.test.js`; diff is
  `42` additions / `11` deletions; whitespace check passed. The scaffold
  separates candidates from the shortlist, captures strict shortlist
  metadata/publication input, and adds only `SCN-KI-041` with the required
  300/200/200/100 assertions.
- **Commit provenance:** repository history contains requester-authored
  commit `adf416662e3aae581328478b70dfe828d3191e8b` (`C105`). No history
  repair, reset, amend, push, or additional agent commit was performed by
  the window agent; this is recorded as requester-owned provenance rather
  than a leaf action.
- **Disposition:** `ACCEPTED_FOR_INTEGRATION`.
- **State transition:** S2 state 20; `KI-W6-I102` is now reserved for the
  window-agent's independent integration assessment. No I102 execution is
  included in this acceptance.
- **External actions/cost:** none; `$0.00`.

---

## `EV-KI-W6-R28` — I102 CV1 failure and parent-level specification blocker

- **Timestamp:** 2026-08-21T14:22:00+05:30
- **Actor/role:** `KI-W6-WINDOW-AGENT` (independent integration assessment)
- **Authority:** A5 state 153 / `ASG-KI-W6-WA-02`; C104 and C105 were already
  accepted (`R26`/state-153 disposition and `R27` C105 review). I102 has no
  implementation-write authority.
- **Exact CV1 command:** from `email_scraper/`,
  `node --check src/aws-pipeline/keyword-intelligence/service.js && node --test --test-isolation=none test/keyword-intelligence-worker-flow.test.js`.
  The syntax check passed; the component test exited `1` with `37` tests,
  `30` pass, `7` fail, `0` skipped.
- **Decisive failures:** `R3-G11` through `R3-G15` each throw
  `PIPELINE_ARTIFACT_CONFLICT` from `readManifest()` at
  `service.js:998`; `SCN-KI-041` throws `PIPELINE_ARTIFACT_INVALID` while
  storing the expansion manifest at the scaffold's line 605. Thus R3/R4 are
  not green and the required 300/200/200/100 runtime activation is not
  established.
- **Independent source diagnosis:** C105 stores the anchor shortlist manifest
  with `anchorTask.inputFingerprint` (`worker-flow.test.js:632,639`), while
  `readManifest()` mechanically derives and requires
  `keywordStageInputFingerprint({ researchId, generation, stage:
  "anchor_screen", tasks: manifestContext.tasks })` (`service.js:772-789`).
  This fingerprint mismatch produces the five R3 artifact conflicts.
  Separately, the required `SCN-KI-041` passes 300 candidates through the
  scaffold's one `expansionManifest.bySeed[0].keywords` list
  (`worker-flow.test.js:601`), but the frozen
  `keywordExpansionManifestSchema` caps that list at `60`
  (`contracts.js:238`). This produces the invalid artifact before C104 can
  execute its shortlist projection.
- **Why this stops rather than opens C106:** changing the task fingerprint to
  the already-defined stage fingerprint is mechanical, but making the required
  *one-seed / 300-keyword* scenario valid requires a parent choice that either
  changes the frozen scenario shape or the frozen manifest contract. The
  window agent cannot choose between those materially different contract/test
  designs. No corrective leaf is authored.
- **Scope/provenance checks:** current raw SHA-256 digests are
  `service.js = b85ce80098792faf7c781effe648d86452f61b857a8cd737b037940fdce12b02`
  and `worker-flow.test.js = f549f9ac16e2c31957dd3a03b11d54da15972f4af23ebcfecb6f8c16f8955d9f`.
  The C104→C105 diff names only `test/keyword-intelligence-worker-flow.test.js`;
  that diff and the root worktree pass `git diff --check`. Both nested
  repositories are clean. No provider, AWS, production-database,
  destructive, secret, history, commit, or KI-W7 action occurred.
- **Coverage/controls:** CV1 executed once and failed; no CV2-CV6 command was
  executed, no control was rerun, and no coverage membership/digest changed.
  This is not a sandbox or channel invalidation, so no identical recovery is
  permitted.
- **Disposition:** `PARENT_BLOCKED`. S2 state 21 records `STOP` and the exact
  parent decision needed. KI-W7 remains prohibited.

---

## `EV-KI-W6-R29` — State-154 C106/I103 literal transcription and C106 dispatch

- **Timestamp / role:** 2026-08-21T14:30:00+05:30 / `KI-W6-WINDOW-AGENT`
  decomposition and dispatch.
- **Authority:** A5 state 154 / `ASG-KI-W6-WA-02`, A4 `KI-CL-22`,
  `DEC-KI-040`, `KI-DD-7`, `KI-DL-16`, and `KI-TR-14`. The parent explicitly
  authorizes literal transcription into S1/S2/S3, one C106 dispatch, independent
  review, then I103 CV7–CV12. KI-W7 remains prohibited.
- **Exact-transcription certificate:** S1 §9.3 contains the C106 task block,
  one-file assignment, checks, non-goals, and I103 CV7–CV12/CH3/CH4 in the
  same order, with the same formulas, bounds, prohibitions, gates, starting
  file digest, and empty repository change-set digest as A4. The only
  assignment completion is replacing A4's `UNASSIGNED` leaf placeholder with
  `KI-W6-C106-LEAF-AGENT`; no implementation-affecting content changed.
- **C106 dispatch:** `ASG-KI-W6-C106` assigns only
  `email_scraper/test/keyword-intelligence-worker-flow.test.js` to
  `KI-W6-C106-LEAF-AGENT`. Starting digest is
  `f549f9ac16e2c31957dd3a03b11d54da15972f4af23ebcfecb6f8c16f8955d9f`;
  starting backend change-set digest is
  `e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855`.
  C106-C1 and C106-C2 each run once; C106 must stop at
  `AWAITING_WINDOW_REVIEW` for independent review.
- **Current baseline:** before dispatch, the assigned file matched its frozen
  digest, both nested repositories had empty porcelain, and `git diff --check`
  passed. S1/S2/S3 were the only coordination writes. No source/test leaf edit,
  command gate, provider, AWS, production/database, destructive, commit, push,
  secret, cost, or KI-W7 action occurred in this dispatch record.
- **Disposition:** `CORRECTIVE-SUBWINDOW-DISPATCHED`; S2 state 22 is `READY`
  for C106. I103 is reserved and unstarted.

```yaml
certificate: CORRECTIVE-SUBWINDOW-DISPATCHED
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-02
subwindow_id: KI-W6-C106
assignment_id: ASG-KI-W6-C106
assigned_agent: KI-W6-C106-LEAF-AGENT
writable_file: email_scraper/test/keyword-intelligence-worker-flow.test.js
starting_file_digest: f549f9ac16e2c31957dd3a03b11d54da15972f4af23ebcfecb6f8c16f8955d9f
starting_repository_change_set_digest: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
required_local_cases: [C106-C1, C106-C2]
predecessors: [KI-W6-I102 PARENT_BLOCKED]
integration_assessment_reservation: KI-W6-I103 after independent C106 acceptance only
external_mutations: []
prohibited_actions_observed: []
status: READY
```
