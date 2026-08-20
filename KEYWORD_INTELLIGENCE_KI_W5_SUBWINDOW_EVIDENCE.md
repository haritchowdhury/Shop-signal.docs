# KI-W5 Sub-Window Evidence (`S3`)

Append-only. Every entry identifies actor, revisions, commands, decisive
results, coverage accounting, external mutations, and disposition. This
file cannot amend a task, decision, or authority boundary.

---

## `EV-KI-W5-S01` — Entry-gate verification, delta audit, and starting inventory

- **Timestamp:** 2026-08-19T12:40:00+05:30
- **Parent window / assignment / sub-window:** `KI-W5` / `ASG-KI-W5-WA-02` / (decomposition)
- **Actor/role:** `KI-W5-WINDOW-AGENT` (window agent)
- **Frozen revisions at inspection:** parent standard
  `3b7a4fd25156e1adfbc92abb835c5f82a0d18c686b1c1150feb202f2d944d2ac`;
  sub-window standard
  `1766f9107ce7d315877b75d4b0ea2b5521dff1c321e12f890b03787d66196ded`; A1
  `8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c`; A3
  `c2dc635e5aa58f88c1ec465154663d314af68570fd4cbfdfca7b51c393c6f70f`;
  A4 `324667cbe0d467ecf4f913c93e91087e75192bd463e0c05b033ee418754a362e`.
- **§1 Assignment provenance:** requester-directed parent performed the
  A5 CAS to state 105 on 2026-08-19T11:55:50+05:30 creating
  `ASG-KI-W5-WA-02` for `KI-W5-WINDOW-AGENT` with
  `authorized_windows: [KI-W5]`, the three-artifact write scope, and the
  delegation action list copied unexpanded into S1 §1 (`EV-KI-A-043`,
  `CHG-KI-021`). The prior assignments `ASG-KI-W5-WA-01` (state 103) and
  `ASG-KI-W5-01` (state 104) were withdrawn unused before any execution;
  no work is invalidated. No requester exception or waiver applies.
- **§2 Delta audit (sub-window standard §0.4):** all five A5 state 105
  pins were recomputed from disk at authoring time via `sha256sum` and
  match byte-for-byte — no stale-pin condition exists (contrast: the
  KI-W4 `EV-KI-W4-S01` §2 stale-pin finding). The observed A4 contains
  the complete amended `KI-W5` window (A4 lines 2273–2430): delegation
  header with `delegation_policy`, `window_agent_identity`,
  `window_agent_coordination_write_scope`, the 27-path
  `delegable_implementation_file_set` with digest `a04dce13…`,
  `shared_file_scope`, `read_only_scope`, verbatim action/prohibition
  lists, preconditions `KI-W5-P1`–`P6`, task blocks `KI-W5-T1`–`T3`, and
  gates `KI-W5-V1`–`V4`. No contradictory authority found; the
  decomposition binds to the observed revisions.
- **§3 Boundary copy:** S1 §1 reproduces the A5 state 105 and A4 `KI-W5`
  write/action/prohibition/successor/stop scope without expansion.
- **§4 Commands and decisive results:**
  - `sha256sum` over the five parent artifacts → the pins above (all
    equal).
  - `git -C frontend rev-parse HEAD` →
    `0dfa1acac50fac3a86d02ec674c6d2bab645832d`;
    `git -C frontend status --porcelain` → empty. Frontend is the W5
    write target and starts clean.
  - `git -C email_scraper rev-parse HEAD` →
    `fac5bb0f0a4e9c04873c9d338794762d44e35f7f`; status clean; read-only
    for `KI-W5`.
  - Root `git status --porcelain` → 36 owner-controlled relocation
    paths; sorted-porcelain per-LF digest
    `f1d1d8e1ce5db60be7eca760ae2709954a824897ca40fb5e81ac6b36801a9a8b`;
    state preserved unmodified.
  - The 27 planned paths, `LC_ALL=C sort`, each + LF, `sha256sum` →
    `a04dce13038a3d180ddab0c8412890af065e3f5ab5019540c87a5664485320e6`
    — byte-equal to the A4 `delegable_file_set_digest` and to the
    `EV-KI-A-041`/`EV-KI-A-043` derivations. Set-equality proof for
    `SW-D03`. (Method note: unsigned-byte-order sorting requires
    `LC_ALL=C`; a locale-collation `sort` produces a different, wrong
    digest — recorded so leaf/gate recomputations use the frozen method.)
  - `sha256sum` over the three MODIFY files → the S1 §2 starting digests;
    `ls` proves the other 24 paths ABSENT (directories
    `app/keywords/`, `app/api/keyword-research/`,
    `components/keyword-intelligence/`, `test/browser/` and the lib/test
    files do not exist).
  - Grep over the three MODIFY files for every planned keyword symbol
    (`KeywordResearch`, `parseResearchEnvelope`,
    `parseRunHandoffEnvelope`, `validateSeedsInput`,
    `newClientRequestId`, `KEYWORD_RESEARCH_ID_PATTERN`,
    `createKeywordResearch`, `getKeywordResearch`,
    `saveKeywordSelection`, `startKeywordResearchRun`,
    `keyword-intelligence`) → zero matches each; the only pre-existing
    `keyword` occurrences are the four CrUX traffic field names
    (api-types.ts:294-300, api-validation.ts:700-706), untouched. All
    `KI-W5` implementation work remains.
  - Tooling baselines: Node `v24.14.1` (`node --version`); global
    `WebSocket` available (Node ≥22; required by the S027 `Cdp` client);
    `npx tsc --noEmit` → exit 0; `npm run lint` → exit 0 (both from
    `frontend/`). Chart dependencies verified:
    `node_modules/chart.js/package.json` version `3.9.1`;
    `node_modules/chartjs-chart-treemap/package.json` version `2.0.0`
    (`KI-W5-P3` evidence: the exact pinned versions are installed and
    imported only by future W5 code; the representative-build proof runs
    at `KI-W5-V2` on the frozen tree).
  - `KI-W5-P2` reading: W4 API contract acceptance is `EV-KI-A-040`
    (parent verification, 34-case enforcement certificate, owner API,
    durable selection, atomic handoff). No persisted standalone
    fixture-server artifact exists in either repository (grep over
    `KEYWORD_INTELLIGENCE_KI_W4_SUBWINDOW_*` and
    `KEYWORD_INTELLIGENCE_EXECUTION_EVIDENCE.md` for "fixture
    server|fixture-server|mock server" → zero matches). The available
    deterministic mechanisms are the accepted G-R1 pre-hydration
    interception precedent
    (`frontend/scripts/g-r1-real-component-browser.mjs:135-181,306`) and
    the accepted W4 in-process server harness
    (`email_scraper/test/keyword-intelligence-api.test.js:679`). S1 §0.1
    freezes the interception mechanism plus real unauthenticated route
    probes for the browser gates; recorded for parent decomposition
    review.
- **Coverage accounting:** no case IDs executable at this step
  (decomposition); required/registered/executed accounting begins at
  `S024`–`S027` and merges at `KI-W5-I001-M`.
- **External mutations:** none (read-only commands; S1/S2/S3 creation is
  the authorized coordination write).
- **Limitations/deferred:** the representative production build and
  browser import proof of the chart dependencies execute once at
  `KI-W5-V2`/`KI-W5-V1` on the frozen final tree per the A4 gate
  economy; no blocker for decomposition.
- **Disposition:** entry gate satisfied; decomposition authoring
  authorized.

---

## `EV-KI-W5-S02` — Dependency verification, anchors, and digest recomputation

- **Timestamp:** 2026-08-19T12:40:00+05:30
- **Parent window / assignment / sub-window:** `KI-W5` / `ASG-KI-W5-WA-02` / (decomposition)
- **Actor/role:** `KI-W5-WINDOW-AGENT`
- **§1 Decision closure:** every implementation-affecting parent decision
  for `KI-W5` exists and is accepted: `DEC-KI-019` (backend API contract;
  A3 lines 404-445), `DEC-KI-012/013/014/015` (result, default selection,
  selection items, duplicate review; A3 lines 248-347), `DEC-KI-017`
  (run handoff), `DEC-KI-018` (state machines incl. the seven-stage
  order), `DEC-KI-023` (dashboard implementation), `DEC-KI-024/025`
  (bounds); the A4 task blocks `KI-W5-T1`–`T3` are complete with all 15
  items each; no contradictory authority found (`SW-D02`).
- **§2–§5 Anchors and interfaces (verified by read/grep):**
  - `frontend/lib/api-types.ts` (532 lines): end-of-file additive anchor
    after line 532; no `Keyword*` export exists.
  - `frontend/lib/api-validation.ts` (1318 lines): `ApiPayloadError`
    class at line 41; helper style lines 50-101; `parseRunStatus`
    exported (existing); end-of-file additive anchor after line 1318.
  - `frontend/lib/client-api.ts` (52 lines): `apiRequest`/`ApiRequestError`/
    `errorMessage`; existing runtime import at line 2 uses the `@/` alias
    (Node-import impossible — allocation consequence recorded in S1 §5.5).
  - `frontend/lib/backend-proxy.ts` (111 lines): `jsonError` (13),
    `backendBaseUrl` validation (28-38), `proxyBackend` JSON-parses every
    response (74-84) — the CSV route therefore cannot use it (S1 I-F10);
    `RUN_ID_PATTERN`/`validRunId` (107-110).
  - `frontend/app/api/runs/route.ts` (142 lines): POST guard order
    (content-type 55, size 63, JSON 67, auth 73, proxy 84-99).
  - `frontend/app/api/runs/[runId]/route.ts` (26 lines): dynamic-route
    pattern (`authenticatedRoute` → awaited params → guard →
    `encodeURIComponent` proxy).
  - `frontend/lib/auth/route.ts` (32 lines): `authenticatedRoute()`
    outcome union; `frontend/lib/auth/server.ts` (32 lines):
    `sessionUserId`.
  - `frontend/app/runs/page.tsx` (25 lines): server-page shell pattern
    (no session redirect — the app's 401 handling is client-side).
  - `frontend/test/query-treemap.test.ts` (29 lines): the Node test style
    for pure lib modules (relative `.ts` imports); existing suites never
    node-import modules with runtime `@/` imports.
  - `frontend/scripts/g-r1-real-component-browser.mjs` (514 lines):
    `fixtureInjection` (135-181), `Cdp` class (183-201), `next dev` spawn
    (283), Chrome headless spawn with `--remote-debugging-port=0` (297),
    `evaluate`/`waitFor`/`navigate`/`setViewport`/`capture`/`click`
    helpers (204-281) — the S027 harness patterns.
  - `KeywordSearchVolume/dashboard/index.html` (3322 lines): style block
    12-467; script 758-3320; CDN scripts 10-11 (not portable); the
    I-F12/I-F14-named function anchors (`projectMarketRow` 962,
    `getFiltered` 996, `renderDecisionPanels` 1319, `chartTopKeywords`
    1345, `chartClusterVolume` 1459, `chartTreemap` 1826, `renderTable`
    2465, `renderClusters` 2585); DOM inventory of 89 `id="…"` elements
    incl. the nine static chart canvases and the landscape canvas (593);
    `chartClusterVolume`/`chartTreemap` target elements absent from the
    static DOM (grep count 0) — S1 §3.8 records the materialization
    decision for parent review.
  - `frontend/package.json`: `chart.js` `3.9.1`, `chartjs-chart-treemap`
    `2.0.0`, `next` `16.2.12`, `react` `19.2.4`; scripts `test`
    (`node --experimental-strip-types --test test/*.test.ts`), `lint`
    (`eslint`), `check` (`npm run lint && npm run test && npm run
    build`); `engines.node >=20`; `tsconfig.json` paths `@/*` → `./*`.
- **§6 Dependency verification:** components consume only lib outputs
  (S005 client methods, S006 selectors, S007 CSS module); the orchestrator
  S016 composes S008–S015; routes consume only S002 validators and the
  existing proxy/auth modules; pages consume S008/S016; tests consume
  lib/component/route outputs and never import route/page modules in Node
  (they import `server-only`-free lib modules only). The S1 §4 DAG order
  follows these named outputs (`SW-D06`).
- **§7 Interface freeze:** `I-F1`–`I-F18` (S1 §3) fix every cross-file
  signature, default, outcome union, error code, key set, poll ladder,
  chart lifecycle, inventory literal, and certificate format before any
  dependent leaf executes (`SW-D07`).
- **Digest recomputations:** the 43-ID required case set (S1 §6.1
  literals), `LC_ALL=C sort`, each + LF →
  `cb8ef6d7cb87b5a451e438d11b0f037c8130f78d0c3e033b1304f78bfa1f6bdb`.
  The 12 control IDs (`W5-NC01`–`W5-NC12`) are tracked by allocation
  (S1 §6.2) outside the case-set digest, mirroring the accepted KI-W4
  convention.
- **Coverage accounting:** decomposition-time only.
- **External mutations:** none.
- **Disposition:** anchors, dependencies, and formulas verified; contract
  + exact-anchors authoring style fixed by requester selection (carried
  from the accepted `EV-KI-W4-S01` §0.4 precedent and the 2026-08-19
  delegation direction; recorded here as the authoring-style fact behind
  S1's preamble).

---

## `EV-KI-W5-S03` — Decomposition authoring, mechanical lint, counterexample audit, and readiness certificate

- **Timestamp:** 2026-08-19T12:40:00+05:30
- **Parent window / assignment / sub-window:** `KI-W5` / `ASG-KI-W5-WA-02` / (decomposition)
- **Actor/role:** `KI-W5-WINDOW-AGENT`
- **§1 Artifacts created:** S1
  (`KEYWORD_INTELLIGENCE_KI_W5_SUBWINDOW_CHECKLIST.md`, 2596 lines,
  sha256
  `740f84cfbc910782d501ac68c43f9fe24a58fbec55f242cb9595c1a36b92588d`),
  after one authoring-time self-falsification correction: the §7.5
  nine-box checklist was initially rendered only in `KI-W5-S001` with
  verbatim references in the other 26 FILE blocks; per `SW-E01`
  ("contains every §7 field") all 27 FILE blocks now render the boxes
  explicitly (243 boxes total). Correction made before any parent review;
  no completed-window history existed.
  S2 (`KEYWORD_INTELLIGENCE_KI_W5_SUBWINDOW_STATE.md`, state_version 1),
  S3 (this file). Authorities do not overlap: S1 decides, S2 records
  state, S3 records facts (`SW-A05`).
- **§2 Adjacency:** leaves report only to the window agent; the parent is
  addressed only through the S2 boundary and the consolidated handoff; no
  subagent may write S1/S2/S3 (`SW-A06`, `SW-E06`).
- **§3 Parent mapping:** S1 §6 allocates every requirement, decision,
  task, scenario, and the 43 cases + 12 controls to exact leaves/tests/
  gates; unmapped counts 0/0/0/0/0 (`SW-D01`).
- **§4 Structure:** 27 initial FILE sub-windows (one file each: 24 CREATE
  + 3 MODIFY-additive) plus `KI-W5-I001` ASSESS; zero multi-file
  sub-windows; zero duplicate file owners (`SW-D04`, `SW-D09`).
- **§5 Intermediate states:** S1 §4.1 defines IS-1 through IS-6 with
  exact permitted checks, expected temporary failures (none), resolvers,
  and prohibitions (`SW-D08`).
- **§6 Command safety:** every leaf check is `git status --porcelain`,
  `npx tsc --noEmit`, `npm run lint`, `npm test`, `grep -c`, `node
  --check`, or a `node --experimental-strip-types` import smoke; none
  writes outside the runner's own outputs; no formatter, installer, or
  generator is authorized; `next build`/`next dev`/browser/CDP execute
  only inside I001 (`SW-D10`).
- **§7 Block completeness:** mechanical lint over S1 verifies all 15 §7.1
  yaml fields present in all 28 blocks (27 FILE + 1 ASSESS; S001 carries
  the full prohibited_actions list and every later block references it
  explicitly); the §7.5 nine-box checklist is rendered inside every FILE
  block (27 × 9 = 243 boxes, verified by grep counts 27/27); zero
  unresolved placeholders; banned-verb scan over transformation text
  (`choose`, `decide`, `determine`, `as appropriate`, `as needed`,
  `similar to`, `etc.`) → zero matches (`SW-E01`–`SW-E03`, `SW-R02`).
- **§8 File-local acceptance:** every leaf's V1/V2/V3 checks close inside
  its own file; deferred executions name `KI-W5-I001` gates (B/R
  execution → `KI-W5-V1`; production build + browser → `KI-W5-V2`/`V1`)
  (`SW-E07`, `SW-E08`).
- **§9 Enforcement closure:** 43 cases allocated with registrations,
  witnesses, oracles, and forbidden-outcome assertions (S1 §6.1); 12
  controls mapped to their narrowest cases (S1 §6.2); certificate
  equality and digest rules fixed (S1 §6.4, I-F18); no zero-work,
  skipped, filtered, duplicate, unexpected, unactivated, or summary-only
  path can satisfy acceptance (`SW-V01`–`SW-V03`, `SW-V09`).
- **§10 Assessment authority:** `KI-W5-I001` carries zero implementation
  write authority, personally executed gates `KI-W5-V1`–`V4` and the
  `KI-W5-I001-M` merge; gates run once at the final assessment per the
  A4 verification economy (`SW-V05`, `SW-V06`, `SW-V08`).
- **§11 Correction protocol:** append-only `KI-W5-C001`+ single-file
  corrections from the same 27-file set, §12.2 certificate before
  assignment, evidence invalidation per changed inputs (`SW-V07`).
- **§12 Boundary:** S2 set to `AWAITING_PARENT_DECOMPOSITION_REVIEW`;
  `next_subwindow KI-W5-S001` is not assignable until the parent records
  decomposition review and the window agent converts S2 to `READY`
  (`SW-V10`, `SW-R09`).
- **§13 Mechanical lint results:** sub-window IDs unique and ordered
  (`KI-W5-S001`–`S027`, `KI-W5-I001`); writable files equal the 27
  planned paths with per-LF `LC_ALL=C` set digest `a04dce13…`; no path
  contains `..`, a glob, or a trailing directory terminator; all
  referenced IDs, digests, anchors, and evidence entries resolve
  (`SW-R01`–`SW-R03`, `SW-R10`).
- **§14 Counterexample audit (sub-window standard §14, twenty items):**
  (1,3,4) leaf P2/V2 single-file write-set proof + C1 porcelain +
  `SW-R03` lint; (2) `SW-R03` path grammar; (5) `SW-D03` set-digest
  equality; (6) S1 §4 one-owner-per-file table; (7) §4 DAG +
  predecessors + `I-F1`–`I-F18` freeze; (8) §4.1 IS-1–IS-6 with named
  resolvers; (9) `may_start_successor:false` + S2 single
  `current_subwindow`; (10) §1 prohibition + `SW-E06`; (11) §5 common
  semantics + window-agent review prohibition; (12) §8 corrective
  protocol; (13) append-only `KI-W5-Cxxx`; (14) `KI-W5-I001-M`
  required=registered=executed with witnesses; (15) literal case/control
  digests + control oracle order (unchanged → defect → fresh); (16)
  test-substitute fidelity recorded (S025 pure-logic layer; S027
  interception with strict-parser-validated payloads; real Chrome as the
  fidelity anchor); (17) §5.28 gate scheduling and invalidation rules;
  (18) §8 evidence invalidation on correction; (19) `KI-W5-V2`
  assembled-set digest equality; (20) §8 terminal
  `READY_FOR_PARENT_REVIEW` boundary.
- **Coverage accounting (decomposition):** required parent items mapped —
  tasks `KI-W5-T1`–`T3` (3/3), scenarios `SCN-KI-016/017` (2/2), case IDs
  43/43, controls 12/12; unmapped counts zero.
- **External mutations:** none beyond creation of the three subordinate
  artifacts.
- **Readiness counts:** mandatory authoring checklist checked 44 /
  unchecked 0; initial sub-window count 27; planned file-set digest
  `a04dce13…`; multi-file sub-windows 0; duplicate file owners 0;
  unresolved interfaces 0; unresolved intermediate states 0; unresolved
  execution choices 0; unresolved evidence references 0.
- **Disposition:** decomposition complete; no leaf assigned; awaiting
  parent decomposition review.

### Certificate

```yaml
certificate: SUBWINDOW-DECOMPOSITION-READY
parent_window_id: KI-W5
parent_assignment_id: ASG-KI-W5-WA-02
window_agent_identity: KI-W5-WINDOW-AGENT
revisions:
  parent_standard: 3b7a4fd25156e1adfbc92abb835c5f82a0d18c686b1c1150feb202f2d944d2ac
  subwindow_standard: 1766f9107ce7d315877b75d4b0ea2b5521dff1c321e12f890b03787d66196ded
  contract: 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c
  decision: c2dc635e5aa58f88c1ec465154663d314af68570fd4cbfdfca7b51c393c6f70f
  parent_checklist: 324667cbe0d467ecf4f913c93e91087e75192bd463e0c05b033ee418754a362e
  decomposition: 740f84cfbc910782d501ac68c43f9fe24a58fbec55f242cb9595c1a36b92588d
initial_subwindow_ids: [KI-W5-S001, KI-W5-S002, KI-W5-S003, KI-W5-S004, KI-W5-S005, KI-W5-S006, KI-W5-S007, KI-W5-S008, KI-W5-S009, KI-W5-S010, KI-W5-S011, KI-W5-S012, KI-W5-S013, KI-W5-S014, KI-W5-S015, KI-W5-S016, KI-W5-S017, KI-W5-S018, KI-W5-S019, KI-W5-S020, KI-W5-S021, KI-W5-S022, KI-W5-S023, KI-W5-S024, KI-W5-S025, KI-W5-S026, KI-W5-S027]
initial_subwindow_count: 27
planned_file_set: [frontend/app/keywords/page.tsx, frontend/app/keywords/[researchId]/page.tsx, frontend/app/api/keyword-research/route.ts, frontend/app/api/keyword-research/[researchId]/route.ts, frontend/app/api/keyword-research/[researchId]/selection/route.ts, frontend/app/api/keyword-research/[researchId]/runs/route.ts, frontend/app/api/keyword-research/[researchId]/export.csv/route.ts, frontend/components/keyword-intelligence/chart-panels.tsx, frontend/components/keyword-intelligence/cluster-landscape.tsx, frontend/components/keyword-intelligence/filter-bar.tsx, frontend/components/keyword-intelligence/keyword-dashboard.module.css, frontend/components/keyword-intelligence/keyword-table.tsx, frontend/components/keyword-intelligence/research-dashboard.tsx, frontend/components/keyword-intelligence/research-form.tsx, frontend/components/keyword-intelligence/research-status.tsx, frontend/components/keyword-intelligence/selection-review.tsx, frontend/components/keyword-intelligence/summary-cards.tsx, frontend/lib/api-types.ts, frontend/lib/api-validation.ts, frontend/lib/client-api.ts, frontend/lib/keyword-intelligence-types.ts, frontend/lib/keyword-intelligence-validation.ts, frontend/lib/keyword-intelligence-view-model.ts, frontend/test/browser/keyword-intelligence-dashboard.mjs, frontend/test/keyword-intelligence-api.test.ts, frontend/test/keyword-intelligence-components.test.ts, frontend/test/keyword-intelligence-inventory.test.ts]
planned_file_set_digest: a04dce13038a3d180ddab0c8412890af065e3f5ab5019540c87a5664485320e6
required_case_set_digest: cb8ef6d7cb87b5a451e438d11b0f037c8130f78d0c3e033b1304f78bfa1f6bdb
required_case_count: 43
control_count: 12
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
mandatory_authoring_items_checked: 44
mandatory_authoring_items_unchecked: 0
first_subwindow: KI-W5-S001
integration_assessment_id: KI-W5-I001
parent_review_required: true
```

Certificate notes: all parent pins matched at authoring time (no stale-pin
condition); the four recorded interpretations awaiting parent
decomposition review are enumerated in S1 §8 (P2 fixture-server reading;
two materialized charts; `W5-NC06` control form; S025 test-substitute
layer). None delegates a decision to a leaf.

---

## Parent-executed serialization-correction note (per `EV-KI-A-044`; requester-approved)

- **Timestamp:** 2026-08-19T12:43:00+05:30
- **Actor/role:** parent agent — S3 append executed directly under explicit
  requester approval ("approving you to do the lightweight correction so
  window agent can start dispatching leaf agents", 2026-08-19), a disclosed
  exception to the window-agent-only S3 write rule mirroring the accepted
  `EV-KI-W4-S12`/`EV-KI-W4-S14` requester-exception pattern. Scope is
  exactly the correction prescribed in `EV-KI-A-044`; no other S3/S2/S1
  content is touched.
- **Correction:** the `starting_repository_change_set_digest`
  `f1d1d8e1ce5db60be7eca760ae2709954a824897ca40fb5e81ac6b36801a9a8b`
  recorded in S1 §2 and all 28 block headers was computed under default
  locale collation (`en_US.UTF-8 sort`), which the sub-window standard §4
  declares non-authoritative. The authoritative unsigned-byte-order
  (`LC_ALL=C`) digest of the identical unchanged 36-line starting
  inventory (33 owner-controlled relocation paths + the three KI-W4
  subordinate artifacts, each porcelain line + LF) is
  `d1a974b3248df1764007f77b4d423fc9ff0e85fc7d6add16005058e5156495db`.
  Both values identify the same member set; membership and count are
  exact.
- **No executable impact:** leaf P2 proves the frontend repository clean
  at HEAD `0dfa1aca…` (or containing exactly the accepted predecessor
  endings) plus the root relocation set unchanged per the S1 §5 common
  semantics and consumes no digest; every executable digest computation
  in this decomposition — the 27-path set `a04dce13…`, the `KI-W5-V2`
  write-set proof, and the 43-case set `cb8ef6d7…` — already uses the
  authoritative `LC_ALL=C` member+LF formula. The authoritative method
  note in `EV-KI-W5-S01` §4 stands.
- **Append-only discipline:** S1 remains frozen at
  `740f84cfbc910782d501ac68c43f9fe24a58fbec55f242cb9595c1a36b92588d`
  and S2 at
  `6d99aea682544121838e14e5b65a678f1cd5a7d4130de931d4405d8cb0ff506c`;
  this note is the sole authoritative correction record for the locale
  collation of the starting-inventory digest and supersedes only that
  value's method, not any member, count, or executable check.
- **Disposition:** the correction prescribed by `EV-KI-A-044` is closed by
  the parent. The window agent's next append is the S2→`READY` transition
  (no serialization note required there); `KI-W5-S001` becomes assignable
  immediately after that transition per `KI-W5-P6` and A5 state 106
  (`DECOMPOSITION_APPROVED`).

---

## `EV-KI-W5-S04` — Window review of `KI-W5-S001` (keyword intelligence types)

- **Timestamp:** 2026-08-19T13:39:20+05:30
- **Parent window / assignment / sub-window:** `KI-W5` / `ASG-KI-W5-WA-02` / `KI-W5-S001`
- **Actor/role:** `KI-W5-WINDOW-AGENT` (window review)
- **Leaf handoff summary:** CREATE `frontend/lib/keyword-intelligence-types.ts`,
  270 lines, committed by the requester as `ad87f9b4` (parent commit
  `0dfa1aca`); single-file diff (270 insertions, no other file).
- **Contract verification:** all 24 `export type` declarations match
  `I-F1` exactly — verified field-by-field against `DEC-KI-012/013/014/015/019`
  (A3 lines 248-347, 404-445): `ResearchView` 17 keys; `ResearchSummary`
  13 keys incl. literal `schemaVersion: 3`; `MarketMetric.opportunityScore`
  non-null vs `KeywordRow`/snapshot nullable; `KeywordMetricSnapshot` =
  keyword row minus `itemId,keyword,seed,sourceSeeds,lane,facets` (19
  fields); `marketMetrics` exact nine-key map; `KeywordFacets` exact five
  arrays; enums and `SelectionItem`/conflict shapes per ledger; sole
  import is type-only `RunStatus` from `@/lib/api-types`; zero runtime
  code.
- **Checks:** C1 write-set = the one file (`git show ad87f9b4 --name-only`
  → exactly `lib/keyword-intelligence-types.ts`; tree clean after commit);
  root relocation subset digest `d1a974b3…` unchanged (39 porcelain
  lines = 36 relocation/inventory + 3 coordination artifacts); C2
  `npx tsc --noEmit` → 0; C3 `npm run lint` → 0; C4 `npm test` → 90/90
  pass, 0 skipped; C5 `grep -c "^export type "` → 24, `grep -c "^import "`
  → 1.
- **Ending digest:** `1619572d606af3b43a7bbf9945ef3f208e01f99c01ced29e2666a84c244b1f19`.
- **Coverage accounting:** zero local case IDs at this leaf (cases
  `W5-A05/A06`, `W5-I01` execute in S024/S026 per the frozen allocation);
  no skips.
- **External mutations:** none.
- **Limitations/deferred:** none.
- **Disposition:** `KI-W5-S001` ACCEPTED.

---

## `EV-KI-W5-S05` — Window review of `KI-W5-S002` (keyword intelligence validation)

- **Timestamp:** 2026-08-19T13:39:20+05:30
- **Parent window / assignment / sub-window:** `KI-W5` / `ASG-KI-W5-WA-02` / `KI-W5-S002`
- **Actor/role:** `KI-W5-WINDOW-AGENT` (window review)
- **Leaf handoff summary:** CREATE `frontend/lib/keyword-intelligence-validation.ts`,
  818 lines, committed by the requester as `69e5e3a` (parent `ad87f9b4`);
  single-file diff (818 insertions, no other file).
- **Contract verification (I-F2):** export surface exactly the eight
  names (C5 Node import: sorted keys string equal; `KEYWORD_RESEARCH_ID_PATTERN`
  `^kr_[A-Za-z0-9_-]{24}$/u`; `CLIENT_REQUEST_ID_PATTERN`
  `^[A-Za-z0-9_-]{16,80}$/u`; `newClientRequestId()` =
  `crypto.randomUUID().replace(/-/g, "")` → 32 chars, pattern-match true).
  `parseResearchView` enforces the 17-key `DEC-KI-019` set, 4-key
  `progress` with seven-value stage enum, 5-key nonnegative `StageCounts`,
  `result` null unless completed (and required when completed), selection
  0..200 with the `DEC-KI-014` key set, `DEC-KI-015` conflict shapes with
  ascending `itemIds` and `(leftItemId,rightItemId)` pair ordering,
  `safeError` exact `{code,message}`, ISO-or-null dates with
  created/updated non-null, nonempty unique-code markets from the
  nine-code set, seeds 1..5, generation ≥ 1. Result branch enforces the
  `DEC-KI-012` sets: market metric (16 keys, `monthlyHistory` 15..102,
  `month` 1..12, nonnegative safe-integer volumes, enums, score bounds),
  keyword row (25 keys, facets, lane, nine-key marketMetrics, null-only
  nullables), cluster row (16 keys; `laneCounts` lane-key-subset with
  present values positive integers per the ledger absence-means-zero
  clause), 13-key summary with `schemaVersion` 3. `parseRunHandoffEnvelope`
  exact `{run,statusUrl}` with `parseRunStatus`; `validateSeedsInput`
  exact-key object, 1..5 strings, NFKC/whitespace-collapse/trim, 1..100
  code points, duplicate rejection — verified byte-for-byte against the
  authoritative backend `normalizeSeeds`
  (`email_scraper/src/keyword-intelligence/selection.js:23-58`,
  identical algorithm incl. `toLocaleLowerCase("en-US")` duplicate key,
  `MAX_SEEDS=5`, `MAX_SEED_LENGTH=100`).
- **Adversarial probes (Node, `--experimental-strip-types`):** 12-probe
  batch on the view/envelope/handoff paths — accepted baseline; rejected
  unknown top-level key, `result` on queued, empty markets, duplicate
  market codes, 6 seeds, negative revision, bad timestamp, envelope extra
  key, bare-view envelope, handoff extra key, empty handoff `statusUrl`;
  duplicate seed rejected, whitespace seed normalized; id-pattern checks
  true/false. 5-probe completed-result batch — accepted full valid
  result; rejected 14-point history, bogus lane key, zero lane count,
  completed-without-result. All 17 outcomes as specified; all failures
  were `ApiPayloadError`.
- **Checks:** C1 write-set = the one file (single-file commit); C2
  `npx tsc --noEmit` → 0; C3 `npm run lint` → 0; C4 `npm test` → 90/90
  pass, 0 skipped; C5 surface check → exit 0.
- **Ending digest:** `8275def2a60c2cac443f1ca6e0a6f2d64cf31df9d467513be6cf0eaba34a6464`.
- **Accepted deviations (recorded, no executable impact):**
  1. Import specifier `"./api-validation.ts"` (with extension) instead of
     I-F2's literal `"./api-validation"` — required for Node
     strip-types resolution, enabled by `allowImportingTsExtensions:
     true`, and the established codebase convention (existing tests
     import `"../lib/api-validation.ts"`); `api-validation.ts` itself has
     zero runtime imports, so Node importability holds.
  2. `validateSeedsInput` omits the backend's control-character check
     (`CONTROL_RE` `\u0000-\u001f\u007f`, selection.js:10) — the frontend
     pre-validation is a deliberate subset; the backend remains
     authoritative and its 400 surfaces through the routes.
- **S1 erratum (prose-only, frozen S1 untouched):** S1 §5.2 step 2 says
  "15-key exact set" for `ResearchView` (authoritative count: 17 per
  `DEC-KI-019`) and step 3 says "summary 15-key exact set" (authoritative
  count: 13 per `DEC-KI-012`). The leaf transcribed the authoritative
  ledger key lists correctly; no executable check depends on those prose
  counts; S1 remains frozen at `740f84cf…`.
- **Coverage accounting:** zero local case IDs at this leaf (cases
  `W5-A01`–`W5-A07`, `W5-NC01/NC07/NC12` execute in S024 per the frozen
  allocation); no skips.
- **External mutations:** none.
- **Limitations/deferred:** deep behavioral coverage (all 43 cases) runs
  at S024 with the test file; this review's probes are window-review
  verification, not a substitute.
- **Disposition:** `KI-W5-S002` ACCEPTED. Next assignable: `KI-W5-S003`.

---

## `EV-KI-W5-S06` — Window review of `KI-W5-S003` (api-types additive re-exports) and requester-authorized harness repair

- **Timestamp:** 2026-08-19T14:06:24+05:30
- **Parent window / assignment / sub-window:** `KI-W5` / `ASG-KI-W5-WA-02` / `KI-W5-S003`
- **Actor/role:** `KI-W5-WINDOW-AGENT` (window review; harness repair executed by the window agent under explicit requester authorization)
- **Leaf handoff summary:** MODIFY `frontend/lib/api-types.ts`, additive append
  of the I-F3 re-export block, committed by the requester as `3953bb7`
  (parent `69e5e3a`); single-file diff; starting digest verified
  `25d6bd8e…` (= S1 §2 baseline; parent commit blob recomputed), ending
  digest
  `e91b62a2ead26d6693c2ff47cd4dcc89778f287784620614d0296fb6a59fcec4`;
  file now 560 lines.
- **Contract verification (I-F3):** appended block byte-equal to the I-F3
  literal — one blank line, the exact comment line, one `export type { … }`
  statement listing exactly the 24 I-F1 names in alphabetical order with
  the relative specifier `"./keyword-intelligence-types"`; no other line
  changed (`git diff --numstat` → `28 insertions, 0 deletions`; the S1
  §5.3 C5 expectation of `27 insertions` is the known authoring-session
  off-by-one — blank line + 27-line block = 28; S1 frozen, erratum
  recorded here); `grep -c "keyword-intelligence-types" lib/api-types.ts`
  → `1`.
- **C4 initial failure and diagnosis:** `npm test` failed 11 tests in
  `test/lead-details-component.test.ts` — each with
  `lib/keyword-intelligence-types.ts(1,32): error TS2307: Cannot find
  module '@/lib/api-types'`. Root cause is a pre-existing harness defect,
  not a leaf defect: the harness (`compiledComponents`,
  test/lead-details-component.test.ts:41-65 original) compiled
  `components/lead-details.tsx` and `components/results-table.tsx` with a
  bare programmatic `tsc` CLI invocation (`--moduleResolution Node`, no
  project config). A bare invocation never loads `tsconfig.json`, so the
  `@/*` path alias could not resolve; the harness only ever passed
  because every transitive import of those two files happened to be
  relative. S003's re-export legitimately pulled
  `keyword-intelligence-types.ts` (whose line-1 type-only
  `import … from "@/lib/api-types"` is mandated by the frozen I-F1
  interface) into the compile graph, exposing the defect. `npx tsc
  --noEmit` (real project config) was and remains exit 0; product code
  was never broken.
- **Requester exception:** the harness file is outside the frozen
  27-path writable set, so the correction protocol could not authorize
  the fix. The requester explicitly authorized the window agent to fix
  the harness and document the change (2026-08-19: "i am authorizing you
  to fix it and document the changes you made so S004 can proceed and
  S003 is accepted") — the same disclosed requester-exception pattern as
  `EV-KI-A-045`/`EV-KI-W4-S12`/`EV-KI-W4-S14`. Scope of the exception:
  exactly `frontend/test/lead-details-component.test.ts`; no other file
  and no specification change.
- **Fix applied (single file, minimal):** the bare CLI invocation in
  `compiledComponents()` was replaced by a generated
  `tsconfig.harness.json` (written to the existing temp output directory)
  invoked via `tsc -p`. The config preserves every prior compiler option
  verbatim (`module CommonJS`, `moduleResolution Node`, `target ES2022`,
  `jsx react-jsx`, `strict`, `skipLibCheck`, `esModuleInterop`,
  `resolveJsonModule`, `rootDir` = frontend root, outDir = the same temp
  directory, and the same two component entry files) and adds exactly the
  two alias options the harness lacked: `baseUrl` = frontend root and
  `paths: { "@/*": ["*"] }` — identical semantics to the project
  `tsconfig.json`. Emitted layout (`<outDir>/components/*.js`) and all
  `require` paths are unchanged; no assertion, test case, or oracle was
  weakened (11 previously failing tests now pass against the same
  assertions; the 79 previously passing tests are unchanged). Net diff:
  22 insertions / 12 deletions; ending digest
  `8f7f611b3866b1cfd108ebb2acb0c06c8a06da74035ab4e5dd433a4fd8431412`.
- **Verification after fix:** `npx tsc --noEmit` → 0; `npm run lint` → 0;
  `npm test` → 90/90 pass, 0 fail, 0 skipped; root relocation-inventory
  porcelain digest `d1a974b3…` unchanged (exception write is inside
  `frontend/`, not the root set).
- **Checks (S003):** C1 write-set = the one file (single-file commit
  `3953bb7`); C2 tsc → 0; C3 lint → 0; C4 tests → 90/90 after the
  harness repair (initially 79/90 with the pre-existing harness defect);
  C5 grep → 1; numstat → 28/0 with the erratum note above.
- **Coverage accounting:** zero local case IDs at this leaf (`W5-I01`
  and regression execute at S026/I001); no skips.
- **External mutations:** none beyond the authorized single-file harness
  repair (uncommitted; requester commits per policy).
- **Limitations/deferred:** none.
- **Disposition:** harness defect closed; `KI-W5-S003` ACCEPTED. Next
  assignable: `KI-W5-S004`.

---

## `EV-KI-W5-S07` — Window review of `KI-W5-S004` (api-validation additive parser re-exports)

- **Timestamp:** 2026-08-19T14:24:00+05:30
- **Parent window / assignment / sub-window:** `KI-W5` / `ASG-KI-W5-WA-02` / `KI-W5-S004`
- **Actor/role:** `KI-W5-WINDOW-AGENT` (window review)
- **Leaf handoff summary:** MODIFY `frontend/lib/api-validation.ts`, additive
  append of the I-F4 re-export block, committed by the requester as
  `e5b7aa3` (parent `379d05d`, the committed harness correction from
  `EV-KI-W5-S06`: +22/−12, single file); single-file diff (+12, 0
  deletions); starting digest verified
  `1522c8c46db5a1af33d8723140722ba1a8883a718a07ca5d5397355341829b55`
  (= S1 §2 baseline; parent commit blob recomputed), ending digest
  `6b2999fc0203bab85b042a00395afe56e34fb7dc5efdbd6e760c4d576b9a44db`;
  file now 1330 lines.
- **Contract verification (I-F4):** appended block byte-equal to the I-F4
  literal except the import specifier reads
  `"./keyword-intelligence-validation.ts"` (with extension) instead of
  I-F4's extensionless `"./keyword-intelligence-validation"` — the exact
  deviation class accepted as `EV-KI-W5-S05` deviation #1: required for
  Node strip-types resolution (the block's own C5 imports
  `./lib/api-validation.ts` at runtime, and extensionless would fail),
  enabled by `allowImportingTsExtensions: true`, established codebase
  convention. Eight names in the exact I-F4 order; one blank line before
  the comment; no other line changed.
- **Alias-safety of the re-export chain (harness regression):**
  `api-validation.ts` is imported (type-only) by `components/lead-details.tsx`
  and compiled by the repaired harness; the new runtime re-export pulls
  `keyword-intelligence-validation.ts`, which imports only relative
  modules and `@/lib/api-types` type-only (erased at runtime). The full
  `npm test` (including the harness-compiled component tests) passed
  90/90 — chain confirmed alias-safe at runtime and alias-resolved under
  the harness config.
- **Checks:** C1 write-set = the one file (single-file commit; tree clean
  after); C2 `npx tsc --noEmit` → 0; C3 `npm run lint` → 0; C4 `npm test`
  → 90/90 pass, 0 fail, 0 skipped; C5
  `grep -c "keyword-intelligence-validation" lib/api-validation.ts` → `1`
  and the Node import probe → exit 0 with all eight re-exports present
  (`parseResearchView`/`parseRunStatus` functions verified, plus
  `parseResearchEnvelope`, `validateSeedsInput`, `newClientRequestId`,
  `validKeywordResearchId`, both pattern objects).
- **Ending digest:** `6b2999fc0203bab85b042a00395afe56e34fb7dc5efdbd6e760c4d576b9a44db`.
- **Coverage accounting:** zero local case IDs at this leaf (`W5-I02`,
  `W5-NC12` execute at S024; regression via C4); no skips.
- **External mutations:** none.
- **Limitations/deferred:** none.
- **Disposition:** `KI-W5-S004` ACCEPTED. Next assignable: `KI-W5-S005`.

---

## `EV-KI-W5-S08` — Window review of `KI-W5-S005` (client-api additive keyword methods)

- **Timestamp:** 2026-08-19T14:32:00+05:30
- **Parent window / assignment / sub-window:** `KI-W5` / `ASG-KI-W5-WA-02` / `KI-W5-S005`
- **Actor/role:** `KI-W5-WINDOW-AGENT` (window review)
- **Leaf handoff summary:** MODIFY `frontend/lib/client-api.ts`, additive
  edit per I-F5, committed by the requester as `9730806` (parent
  `e5b7aa3`); single-file diff (+45, 0 deletions); starting digest
  verified `84f20e6ba5c3ca2bd17147f8ef46235cd9f6460ebcb49f1ec40228d4cd881046`
  (= S1 §2 baseline; parent commit blob recomputed), ending digest
  `b57d7b8609387243b8413a084303acf89c2fc4943ec170077321a01a3608c936`;
  file now 97 lines.
- **Contract verification (I-F5):** the two import lines sit directly
  after the existing line-2 import with order stable — runtime
  `import { parseResearchEnvelope, parseRunHandoffEnvelope } from
  "./keyword-intelligence-validation";` and type-only
  `import type { KeywordResearchRunResponse, ResearchView, SelectionItem }
  from "./keyword-intelligence-types";`, both byte-equal to the I-F5
  literals (extensionless specifiers are exactly as specified and correct
  here: the file is browser-bundled only — its pre-existing line 2 uses
  the `@/` alias so Node import is impossible by design per the S1 §5.5
  allocation note; webpack/Next resolves extensionless relative TS).
  The four appended functions are byte-equal to I-F5: POST
  `/api/keyword-research` body `{seeds}`; GET
  `` `/api/keyword-research/${encodeURIComponent(researchId)}` ``; PUT
  `…/selection` body `{expectedRevision, items}`; POST `…/runs` body
  `{expectedSelectionRevision, clientRequestId}`; `parseResearchEnvelope`
  on the three JSON routes and `parseRunHandoffEnvelope` on the runs
  route; all via `apiRequest<T>(url, { method, body }, parseFn)`;
  401/404/409/4xx error mapping flows through the untouched `apiRequest`/
  `ApiRequestError`. No other line changed.
- **Checks:** C1 write-set = the one file (single-file commit; tree clean
  after); C2 `npx tsc --noEmit` → 0; C3 `npm run lint` → 0; C4 `npm test`
  → 90/90 pass, 0 fail, 0 skipped; C5 the four-function grep → exactly
  `4`.
- **Ending digest:** `b57d7b8609387243b8413a084303acf89c2fc4943ec170077321a01a3608c936`.
- **Coverage accounting:** zero local case IDs at this leaf — deliberate
  allocation (behavioral oracles `W5-B03`, `W5-R03`, `W5-R04` execute in
  S027 via browser request-log assertions because the file cannot be
  Node-imported); not a skip. No skips.
- **External mutations:** none.
- **Limitations/deferred:** none.
- **Disposition:** `KI-W5-S005` ACCEPTED (zero deviations). Next
  assignable: `KI-W5-S006`.

---

## `EV-KI-W5-S09` — Window review of `KI-W5-S006` (keyword intelligence view model)

- **Timestamp:** 2026-08-19T14:50:00+05:30
- **Parent window / assignment / sub-window:** `KI-W5` / `ASG-KI-W5-WA-02` / `KI-W5-S006`
- **Actor/role:** `KI-W5-WINDOW-AGENT` (window review)
- **Leaf handoff summary:** CREATE
  `frontend/lib/keyword-intelligence-view-model.ts`, 708 lines, committed
  by the requester as `d6ca5aa` (parent `9730806`); single-file diff
  (+708); ending digest
  `b91f0f5e7fd9f692e5f9086f1be0f511af1f0b6b755d117924497a52f89ce9d5`.
- **Contract verification (I-F12):** full I-F12 export surface present
  and behaviorally probed (see below). `KEYWORD_INTELLIGENCE_SURFACE_INVENTORY`
  is the exact 21-entry I-F15 literal. `EXPORT_CSV_COLUMNS` is
  byte-identical (23 names, order) to the accepted backend
  `KEYWORD_CSV_COLS` (`email_scraper/src/keyword-intelligence/export.js:179-187`,
  verified side-by-side). `nextPollDelay` ladder exact (2000→3000→4500→
  6750→10000→10000; <2000→2000). Type-only import from
  `./keyword-intelligence-types.ts`; no React, no fetch, no
  `localStorage`, no `@/` runtime imports — Node-importable.
- **Port fidelity spot-checks against the standalone source:**
  `getFiltered` predicate order matches index.html:996-1019 (market
  projection → `_marketMissing` → seed/cluster/intent/lane/category/
  audience/channel/minVolume/minOpportunity/recommended/flags/search);
  `projectMarketRow` matches index.html:962-977 (metric-field overwrite
  set, `flags→[]`/`recommended→false`/others→null on absent market);
  `aggregateByCluster`/`adjustedVolume`/`metricFingerprint` match the
  standalone aggregation block (index.html:1021-1040); `paginate` clamp
  matches `renderTable` (index.html:2469-2471); `fmtCPC` matches
  index.html:889 (`toFixed(2)`, `—` on non-number); the selection
  classifier (`classifyTokens`/`facetsForSelection`/`laneForSelection`)
  is the ported pure classifier behind `discoveryLane` used for
  `DEC-KI-014` edit reclassification.
- **Behavioral probes (Node, 41 assertions across two batches):** poll
  ladder; terminal states; `fmtNum`/`fmtCpc`/`fmtPct`/`fmtSlope` outputs
  (incl. `fmtCpc(1.005)`→`$1.00` = `toFixed` binary-float rounding,
  identical to standalone); `median` odd/even/empty; `laneLabel`;
  `discoveryLane` three lanes; `nextTheme`; theme key; `paginate`
  clamping (page 99 of 3 pages → last page `[5]`, matching standalone);
  filter defaults; `buildExportQuery` (omits empty defaults, repeated
  `flag` appends, `market/seed/...` names per DEC-KI-019); CSV columns
  equality with backend; selection helpers — DEC-KI-013 candidate order
  (recommended desc → opportunity desc → volume desc → keyword → itemId)
  verified via toggle insertion sequence, toggle-off, remove, 200-cap
  no-op, `selectionOverLimit` boundary 100/101, manual item shape
  (sourceKind manual, null source/metrics, firstSeed single source seed,
  local_discovery reclassification of "… near me"), `canFinalizeSelection`
  all four failure reasons plus ok; `editSelectedItemText` reclassification
  ("plus size dresses near me" → local_discovery, fit `plus size`,
  category `dresses`); `selectionDraftFromView` cloning; market
  projection identity/all/absent; `cumulativeVolume` dedup;
  `aggregateByCluster`; `adjustedVolume` fingerprint dedup;
  `metricFingerprint`; `getFiltered`; `filterOptionSources`; and
  `dashboardPhase` all six outcomes (loading/error×2/empty×2/ready).
  Three initial probe "failures" were verified as probe-author errors,
  not leaf defects: `fmtCpc(1.005)` expectation ignored `toFixed` float
  rounding; `paginate` expected `[4,5]` where the standalone clamp
  semantics (correctly ported) yield `[5]`; `dashboardPhase` probe
  passed a truthy `[]` as the error argument. Corrected probes pass
  41/41.
- **Checks:** C1 write-set = the one file (single-file commit; tree clean
  after); C2 `npx tsc --noEmit` → 0; C3 `npm run lint` → 0; C4 `npm test`
  → 90/90 pass, 0 fail, 0 skipped; C5 the S1 §5.6 Node probe (inventory
  length 21 + poll ladder) → exit 0.
- **Ending digest:** `b91f0f5e7fd9f692e5f9086f1be0f511af1f0b6b755d117924497a52f89ce9d5`.
- **Accepted deviations:** import specifier
  `"./keyword-intelligence-types.ts"` (with extension) instead of I-F12's
  extensionless literal — the `EV-KI-W5-S05` deviation #1 class (Node
  strip-types resolution; required for this block's own C5 Node import;
  `allowImportingTsExtensions` enabled). Type-only, so no runtime impact
  beyond loadability.
- **Coverage accounting:** zero local case IDs at this leaf (cases
  `W5-C01`–`W5-C12`, `W5-A08/A09/A10`, `W5-I03/I05`, `W5-NC02/NC08/NC09`
  execute in S025/S024/S026 per the frozen allocation); no skips.
- **External mutations:** none.
- **Limitations/deferred:** deep behavioral coverage runs at S025; these
  probes are window-review verification, not a substitute.
- **Disposition:** `KI-W5-S006` ACCEPTED. Next assignable: `KI-W5-S007`.

---

## `EV-KI-W5-S10` — Window-agent leaf P1 tracking (block-consumption verification discipline)

- **Timestamp:** 2026-08-19T14:58:00+05:30
- **Parent window / assignment:** `KI-W5` / `ASG-KI-W5-WA-02`
- **Actor/role:** `KI-W5-WINDOW-AGENT`
- **Context:** the requester observed that leaf consumption of S1
  (`KEYWORD_INTELLIGENCE_KI_W5_SUBWINDOW_CHECKLIST.md`) was not being
  explicitly tracked. Correct: leaf P1 attestation ("Revisions,
  assignment identity, writable file, baseline digest, and predecessor
  evidence match", §7.5) was not being verified as a distinct review
  step. This entry establishes the discipline retroactively for
  S001–S006 and binds it into every later window review.
- **Method:** the window agent cannot observe leaf prompts (dispatch is
  requester-relayed), so P1 is verified per leaf by block-specific
  consumption evidence — literals/anchors that exist only in the leaf's
  S1 §5.x block (or its named `read_only_scope` anchors) and are not
  derivable from sibling accepted files. For future leaves the window
  agent additionally requires the leaf handoff to quote its
  `subwindow_id`, `writable_file`, and `starting_file_digest`.
- **Retroactive P1 verification (S001–S006):**
  - **S001** — output contains the exact I-F1 24-type surface with
    `MarketMetric.opportunityScore` non-null vs `KeywordRow` nullable and
    the six-field snapshot exclusion set; these distinctions exist only
    in S1 §3.2 I-F1 + the ledger anchors named in the block. P1 verified.
  - **S002** — output matches I-F2's exact eight-export surface and both
    pattern literals with `u` flags; the leaf followed the block's
    `read_only_scope` to `DEC-KI-019`/`DEC-KI-012` and transcribed the
    authoritative 17-key/13-key sets where S1 §5.2's prose counts were
    wrong (erratum recorded in `EV-KI-W5-S05`) — impossible without
    reading both the block and its anchors. P1 verified.
  - **S003** — output is byte-equal to the I-F3 block including the
    exact comment line `// Keyword intelligence re-exports (KI-W5; additive only).`
    and 24 names in alphabetical order; the comment string exists only
    in S1 §5.3. P1 verified.
  - **S004** — output is byte-equal to the I-F4 block including the
    exact comment `// Keyword intelligence parsers (KI-W5; additive only).`
    and the eight names in the exact I-F4 order. P1 verified.
  - **S005** — output is byte-equal to I-F5's function bodies/URLs/bodies
    and import placement ("directly after the existing line-2 import"),
    including the deliberate extensionless specifiers that exist only in
    the I-F5 literal. P1 verified.
  - **S006** — output contains the exact 21-entry I-F15 inventory in
    fixed order, the poll-ladder constants, the theme key
    `ki-dashboard-theme`, and the C5-specified probe surface; the
    inventory order exists only in S1 §3.8. P1 verified.
- **Protocol change (S007 onward):** each window review entry records an
  explicit "P1 block consumption" line citing (a) the leaf handoff's
  quoted `subwindow_id`/`writable_file`/`starting_file_digest` and (b)
  at least one block-specific literal/anchor present in the output.
  Acceptance without this line is invalid.
- **Disposition:** tracking gap closed retroactively for the six accepted
  leaves; discipline bound into all later reviews. No accepted result
  changes; no S1/S2 authority changes.
- **External mutations:** none.

---

## `EV-KI-W5-S11` — Window review of `KI-W5-S007` (dashboard CSS module)

- **Timestamp:** 2026-08-19T15:12:00+05:30
- **Parent window / assignment / sub-window:** `KI-W5` / `ASG-KI-W5-WA-02` / `KI-W5-S007`
- **Actor/role:** `KI-W5-WINDOW-AGENT` (window review)
- **P1 block consumption:** the module's header comment (lines 1-13)
  documents the exact kebab→camel mapping list including the four
  id→class conversions (`last-updated`, `manual-keyword-input`,
  `select-all-keywords`, `keyword-input`) and the "no rule escapes
  module scope" discipline — that exact conversion list exists only in
  S1 §5.7/I-F13. Requester waived the handoff-quote form ("not
  required"); consumption verified from artifact literals.
- **Leaf handoff summary:** CREATE
  `frontend/components/keyword-intelligence/keyword-dashboard.module.css`,
  716 lines, committed by the requester as `1a51f6e` (parent `d6ca5aa`);
  single-file diff (+716; new directory); ending digest
  `c8d8cebb81fd69bcef568664f91211883b44330946ec6d7a400ffa93c7e420e8`.
- **Contract verification (I-F13), mechanical rule comparison:** a
  selector-normalizing comparator (kebab→camel, `#id`→`.camelClass`,
  `:root`→`.kiDashboard`, `[data-theme="dark"]`→`.kiDashboard[data-ki-theme="dark"]`,
  bare element selectors scoped under `.kiDashboard`) compared all
  standalone `<style>` rules (index.html:12-467) against the module:
  **287/287 non-global rules matched with byte-identical declaration
  blocks** after the mandated conversions. The 13 comparator flags were
  all verified as correct conversions (`#last-updated`→`.lastUpdated`:84,
  `#manual-keyword-input(:focus)`→`.manualKeywordInput`:167/169,
  `section.filters`:191 — decls identical, leak-safe because `.filters`
  is module-hashed, `#select-all-keywords` grouped into
  `.rowCheck, .selectAllKeywords`:422, `tbody tr.is-selected(:hover)`→
  `.kiDashboard tbody tr.isSelected(:hover)`:426/428,
  `#keyword-input(:focus/::placeholder)`→`.keywordInput`:474/479/481,
  `tbody tr.hl-vol*`→`.kiDashboard tbody tr.hlVol*`:530-534).
  `:root`/dark custom-property blocks ported with identical literal
  values (verified against index.html:13-70). Global resets (`*`,
  `html, body`, `body`) correctly NOT ported (I-F13 prohibition).
  Media queries preserved at identical breakpoints (640px, 980px) with
  identical contents (module:688-716 vs index.html:439-467). The two
  `!important`s (module:189,424) are ports of standalone
  `!important`s (index.html:146,279) — no additions. All 98 real
  standalone DOM classes covered; `overlap-panel` (index.html:645),
  `empty-state`, and `error-banner` are dead names with zero standalone
  rules — correctly absent from the module (documented in the mapping
  comment only). Eight I-F13-named classes: six with rules
  (`tableScroll`, `chartWrap`, `clusterSceneLayout`, `seedChipField`,
  `keywordDialog`, `selectionStatus`), two dead in standalone
  (`emptyState`, `errorBanner`).
- **Checks:** C1 write-set = the one file (single-file commit; tree clean
  after); C2 `npx tsc --noEmit` → 0; C3 `npm run lint` → 0; C4 `npm test`
  → 90/90 pass, 0 fail, 0 skipped; C5 root/body/html grep → `0`,
  `kiDashboard` grep → `26` (≥ 2).
- **Ending digest:** `c8d8cebb81fd69bcef568664f91211883b44330946ec6d7a400ffa93c7e420e8`.
- **Accepted deviations:** none.
- **Coverage accounting:** zero local case IDs at this leaf (visual
  regression `W5-R05` executes at I001); no skips.
- **External mutations:** none.
- **Limitations/deferred:** rendered-appearance verification (dark theme,
  responsive breakpoints) executes in the S027 browser harness and
  `KI-W5-V1`.
- **Disposition:** `KI-W5-S007` ACCEPTED. Next assignable: `KI-W5-S008`.

---

## `EV-KI-W5-S12` — Requester-authorized S1 §9 addendum and standing P1 tracking table

- **Timestamp:** 2026-08-19T16:55:00+05:30
- **Parent window / assignment:** `KI-W5` / `ASG-KI-W5-WA-02`
- **Actor/role:** `KI-W5-WINDOW-AGENT` (addendum authored by the window
  agent under explicit requester authorization)
- **Requester authorization:** "can you track them yourself until now,
  then keep tracking them as we go through the next sub windows? or you
  can make them visible with a update in the checklist" (2026-08-19).
- **Context:** `EV-KI-W5-S10` established retroactive P1 verification
  and a forward discipline; the requester asked for standing, visible
  tracking plus a checklist-level protocol update.
- **Actions:**
  1. Appended S1 §9 (addendum; dispatch requirement for S008 onward —
     verbatim block text + checklist path in every dispatch, leaf reads
     its block before editing, handoff quotes
     `subwindow_id`/`writable_file`/`starting_file_digest` with a
     recorded waiver path; window-agent tracking method; visibility note
     documenting why git discovery cannot find the checklist from inside
     `frontend/`). S1 §0–§8 remain byte-identical to the reviewed
     revision `740f84cf…`; S1 digest becomes
     `9c659a7876edf8e8e8b4a2a5db4e387cf4359bf77315d16c83ae5b33e8832b15`
     (pinned in S2 as `decomposition_addendum_revision`; the frozen
     `decomposition_revision` pin is unchanged).
  2. Added the standing "P1 block-consumption tracking" table to S2 —
     one row per leaf, retroactively filled TRACKED for S001–S007 with
     their commits and evidence pointers (`EV-KI-W5-S10`/`S11`), PENDING
     for S008–S027 and I001; updated at every acceptance.
- **No changes:** no frozen block, interface, gate, digest, file-set
  membership, assignment, or authority boundary altered; no corrective
  sub-window consumed; already-accepted leaf results unchanged.
- **External mutations:** none beyond the two coordination writes above.
- **Disposition:** tracking request satisfied — retroactive through
  `KI-W5-S007`, standing table live in S2, dispatch protocol visible in
  S1 §9. Next assignable: `KI-W5-S008`.

---

## `EV-KI-W5-S13` — Window review of `KI-W5-S008` (research form component)

- **Timestamp:** 2026-08-19T17:20:00+05:30
- **Parent window / assignment / sub-window:** `KI-W5` / `ASG-KI-W5-WA-02` / `KI-W5-S008`
- **Actor/role:** `KI-W5-WINDOW-AGENT` (window review)
- **P1 block consumption (S1 §9.2):** output carries the four block
  `read_only_scope` DOM ids (`seed-phrase-form`, `seed-chip-field`,
  `seed-chip-count`, `seed-market-note`) plus the I-F14 behavioral set —
  `validateSeedsInput` gating, 401 CTA to `/sign-in`, `onCreated`-once
  with `router.push(`/keywords/${view.id}`)` default, the
  `parseKeywordLines` NFKC/trim/collapse port — all specified only in
  S1 §5.8/I-F14. Quote form not supplied in handoff; waiver recorded
  (requester relay), consumption proven from artifact literals.
- **Leaf handoff summary:** CREATE
  `frontend/components/keyword-intelligence/research-form.tsx`, 215
  lines, committed by the requester as `82197b1` (parent `1a51f6e`);
  single-file diff (+215); ending digest
  `9583f663db36d57cf4f4782aed5727a2aba471b75f9cb1fec48ce23b1f777336`.
- **Contract verification (I-F14):** `"use client"` (line 1); exact
  props signature `onCreated?: (view: ResearchView) => void`; chip field
  adds/removes seeds with Enter/comma split via the ported
  `parseKeywordLines` (NFKC → whitespace-collapse → trim, case-fold
  dedup — algorithm-identical to the standalone/backend normalization);
  count display `{seeds.length}/5 seeds` with `seed-chip-count` id;
  market note ported (`seed-market-note`); submit disabled while in
  flight or when `validateSeedsInput` fails (`disabled={isSubmitting ||
  !canSubmit}`); re-entrancy guard (`if (isSubmitting) return`);
  `validateSeedsInput` re-checked at submit; success path calls
  `onCreated(view)` exactly once or defaults to
  `router.push(`/keywords/${view.id}`)`; 401 `ApiRequestError` renders
  the sign-in CTA linking `/sign-in` (`role="alert"` banner); other
  errors render `errorMessage(requestError)` safely; accessible
  markup (`aria-busy`, `aria-live="polite"` chip field, labeled input
  with `aria-describedby`, `aria-label` removes, `role="alert"`
  errors). Styling exclusively via 15 S007 CSS-module classes — all
  verified present in the module (zero missing); no inline styles; no
  `localStorage`. `keyword-submit` (block read anchor) is not an S1
  output requirement (grep: sole occurrence is the §5.8 read_only_scope
  line) — correctly absent.
- **Checks:** C1 write-set = the one file (single-file commit; tree clean
  after); C2 `npx tsc --noEmit` → 0; C3 `npm run lint` → 0; C4 `npm test`
  → 90/90 pass, 0 fail, 0 skipped; C5 `"use client"` grep → `1`.
- **Ending digest:** `9583f663db36d57cf4f4782aed5727a2aba471b75f9cb1fec48ce23b1f777336`.
- **Accepted deviations:** none (imports use the app-standard `@/` alias
  — correct for a browser-bundled component).
- **Coverage accounting:** zero local case IDs at this leaf (`W5-B01`,
  `W5-R04` execute in S027 browser harness); no skips.
- **External mutations:** none.
- **Limitations/deferred:** rendered behavior (chip add/remove, 401 CTA,
  in-flight disabling) verified at S027/I001 against real Chrome.
- **Disposition:** `KI-W5-S008` ACCEPTED. Next assignable: `KI-W5-S009`.

---

## `EV-KI-W5-S14` — Window review of `KI-W5-S009` (research status component)

- **Timestamp:** 2026-08-19T17:45:00+05:30
- **Parent window / assignment / sub-window:** `KI-W5` / `ASG-KI-W5-WA-02` / `KI-W5-S009`
- **Actor/role:** `KI-W5-WINDOW-AGENT` (window review)
- **P1 block consumption (S1 §9.2):** leaf handoff supplied the full §9.1
  quote form — `subwindow_id: KI-W5-S009`, `writable_file:
  frontend/components/keyword-intelligence/research-status.tsx`,
  `starting_file_digest: ABSENT`, block-read attestation — plus a
  §12.3 `FILE-SUBWINDOW-EXECUTED` certificate. All quotes verified
  against disk and S1 §5.9.
- **What S009 achieved (verified from disk, independent of the report):**
  - I-F14 props exact (`researchId`/`initialView`/`onTerminal`);
    `"use client"`; module import with `styles.kiDashboard` applied to
    the section (scopes the S007 custom properties).
  - I-F16 single-timer invariant: exactly one `setTimeout` (C5 → 1; no
    `setInterval`), one `timeoutRef`; ladder verified in code — mount
    schedules 2000, then `scheduleNext(nextPollDelay(delayMs))` on both
    success and network-failure paths (2000→3000→4500→6750→10000→10000).
  - `onTerminal` exactly once: `terminalDoneRef` guard shared by poll and
    retry paths; `stopTimer()` at terminal; zero polls after terminal.
  - Unmount safety: `abortedRef` set + `clearTimeout` in cleanup; all
    in-flight `.then`/`.catch` results checked against `aborted`.
  - Retry is GET-only and never touches the timer (invariant preserved;
    poll ladder continues independently — matches I-F14 "retry button
    performs GET only").
  - Progress surface: seven-stage ordered list incl. `finalizing`
    (`STAGE_ORDER`), stage label map, three `StageCounts` groups
    (expansion/anchorScreen/marketOverview) each rendering
    expected/succeeded/skipped/failed, `aria-live="polite"`,
    `aria-busy`, `aria-current="step"`.
  - Network/5xx: `retryNotice` + continued ladder ("Still checking —
    connection issue." + Check again).
  - Failed terminal: `safeError.message` verbatim with
    `data-code={view.safeError.code}` (`role="alert"`).
  - Stale-closure safety: `onTerminalRef` kept current via effect.
- **Styling design note:** visual classes come from the existing app
  design system (`progress-card ds-card state-*`, `progress-head`,
  `progress-stage`, `state-indicator`, `eyebrow`, `progress-metrics`,
  `progress-count`, `inline-error`, `ds-notice--danger` — all verified
  present in `app/globals.css`, 94 rule matches), mirroring
  `components/run-progress.tsx` — the exact pattern named in the block's
  `read_only_scope`. S009's block (unlike S008's) contains no
  module-only styling mandate; `styles.kiDashboard` satisfies the I-F14
  module-import contract. No violation.
- **Literal-conformance observation (no action):** if `initialView` is
  already terminal at mount, the first scheduled GET still runs and
  `onTerminal` fires one poll later. The block's literal transformation
  specifies onTerminal on poll-observed terminal with no
  initial-terminal shortcut; I-F16's "zero polls after terminal" governs
  post-observation. S016 owns mount-context decisions.
- **Checks (independently re-run):** C1 porcelain → exactly
  `?? components/keyword-intelligence/research-status.tsx` (file
  uncommitted at review; requester commits); C2 `npx tsc --noEmit` → 0;
  C3 `npm run lint` → 0 errors, 1 warning — verified pre-existing by
  stash-isolation (lint without the file shows the identical
  traffic-globe.tsx warning); C4 `npm test` → 90/90 pass, 0 fail,
  0 skipped; C5 timer grep → exactly `1`; `localStorage` grep → 0.
- **Digest:** 204 lines; ending digest
  `9a28bcf137990b635f1386139ae4b44b5c7d43902a0812b43e4fcb12f12f2637`
  (matches the certificate).
- **What S009 deferred (verified against the frozen allocation):** all
  rendered-behavior oracles — `W5-R01`/`W5-R02` (poll lifecycle),
  `W5-NC05` (timer-invariant negative control), `W5-R04` (GET-only
  retry, shared with S008), `W5-R05` (visual regression), and the
  `W5-A08` logic case — execute in S024/S025/S027 and gates at I001 per
  S1 §6. Deferral is by allocation, not skip: zero local case IDs is
  the frozen design for this leaf.
- **External mutations:** none.
- **Disposition:** `KI-W5-S009` ACCEPTED (zero deviations; one
  design-note observation). Next assignable: `KI-W5-S010`. Requester to
  commit the file.

---

## `EV-KI-W5-S15` — Window review of `KI-W5-S010` (filter bar component)

- **Timestamp:** 2026-08-19T18:05:00+05:30
- **Parent window / assignment / sub-window:** `KI-W5` / `ASG-KI-W5-WA-02` / `KI-W5-S010`
- **Actor/role:** `KI-W5-WINDOW-AGENT` (window review)
- **P1 block consumption (S1 §9.2):** no handoff quote form was relayed;
  waiver recorded. Consumption proven from artifact literals: the
  `data-filter` attribute convention + exact 14-field set exists only in
  S1 §5.10 step 1; the Market tip text
  "Switch every metric, chart, score, and recommendation between
  cumulative demand and one country" is byte-equal to the standalone
  filter markup (index.html:532) named in `read_only_scope`; the
  options prop is typed `ReturnType<typeof filterOptionSources>` —
  S006's named output per the block's predecessor chain.
- **Leaf handoff summary:** CREATE
  `frontend/components/keyword-intelligence/filter-bar.tsx`, 342 lines,
  committed by the requester as `6626baf` (parent `71eab6b` = S009,
  confirming the prior commit); single-file diff (+342); ending digest
  `a5d8cc9814e817459e95cc595a5063125180af9bed8703a2eba582befa08d641`.
- **Contract verification (I-F14 FilterBar):** exact props
  (`filter`/`options`/`onChange`/`onReset`); one control per
  `KeywordFilterState` field — search text, market select (`all` +
  nine codes `US|GB|CA|AU|NZ|DE|FR|IN|AE`), seed/cluster/intent/lane/
  category/audience/channel selects, minVolume/minOpportunity numeric
  inputs (min/max/step bounds, 0 shown as empty placeholder),
  recommended tri-state (""/true/false), flags multi-select chips with
  tooltips, reset button calling `onReset`. Every change emits exactly
  one `onChange` patch and resets `page: 1` (pagination-consistent
  filtering). Labels/tips mirror the standalone markup (tip texts
  ported with `data-tip` + the `.tip`/`.tip::after` hover mechanics
  from the S007 module); `laneLabel` reuse for lane options;
  `intentLabel` capitalization. C5: `data-filter` grep → exactly `14`
  with the exact field set (13 fields + reset), unique values
  verified. All 13 CSS classes used (`filters`, `filterRow`,
  `filter`, `tip`, `flagGroup`, `seedEmpty`, `grow`, `btn`) present in
  the S007 module. `"use client"`; no `localStorage`; no fetch.
- **Checks (independently re-run):** C1 write-set = the one file
  (single-file commit `6626baf`; tree clean after); C2 `npx tsc
  --noEmit` → 0; C3 `npm run lint` → 0 errors (1 pre-existing
  traffic-globe.tsx warning, already recorded in `EV-KI-W5-S14`); C4
  `npm test` → 90/90 pass, 0 fail, 0 skipped; C5 → `14`.
- **Ending digest:** `a5d8cc9814e817459e95cc595a5063125180af9bed8703a2eba582befa08d641`.
- **Accepted deviations:** none.
- **Coverage accounting:** zero local case IDs at this leaf (`W5-C05`,
  `W5-B02` execute in S025/S027 per the frozen allocation); no skips.
- **External mutations:** none.
- **Limitations/deferred:** rendered interaction (option population,
  patch emission, reset) verified at S025 substitute layer and S027
  browser harness.
- **Disposition:** `KI-W5-S010` ACCEPTED. Next assignable: `KI-W5-S011`.

---

## `EV-KI-W5-S16` — Window review of `KI-W5-S011` (summary cards component)

- **Timestamp:** 2026-08-19T18:30:00+05:30
- **Parent window / assignment / sub-window:** `KI-W5` / `ASG-KI-W5-WA-02` / `KI-W5-S011`
- **Actor/role:** `KI-W5-WINDOW-AGENT` (window review)
- **P1 block consumption (S1 §9.2):** no handoff quote form relayed;
  waiver recorded. Consumption proven from artifact literals: the
  summary-driven card mandate ("driven by `currentSummary(result,
  marketCode)`") exists only in S1 §5.11 — the standalone `renderCards`
  (index.html:1302-1317) computes from filtered rows, so a leaf that had
  NOT read the block would have ported the standalone behavior instead;
  the funnel stage notes ("API rows", "usable volume data", "X
  informational removed", "cross-seed repeats combined", "X rows
  organised into canonicals", "non-transitive market topics", "passed
  score + flags") are byte-equal to `renderFunnel`
  (index.html:1067-1093), a named `read_only_scope` anchor.
- **Leaf handoff summary:** CREATE
  `frontend/components/keyword-intelligence/summary-cards.tsx`, 395
  lines, committed by the requester as `1bbf069` (parent `6626baf` =
  S010); single-file diff (+395); ending digest
  `3690e3f1436a036a5660b8ad3d3ae37cf7ad0032da532d35fd9570411ec9c559`.
- **Contract verification (I-F14 SummaryCards) with port-fidelity
  comparison against the named standalone anchors:**
  - Cards (renderCards port, summary-driven per the S1 mandate): six
    cards — Total (`summary.rawItemsCollected`), Active
    (`summary.activeKeywords`), Recommended
    (`summary.recommendedKeywords`), Clusters (`summary.clusters`),
    Volume (`cumulativeVolume(marketRows)`), AvgCPC (mean over active
    CPCs, `fmtCpc` null-safe) — with market-context labels matching the
    standalone `updateMarketContext` ("Cumulative search volume" /
    "{country} search volume", "Average CPC · {country}") and accessible
    tooltips.
  - Funnel (renderFunnel port): seven stages with identical
    labels/notes and arrows; `variantGroups || active.length` fallback
    preserved; the standalone's missing-summary fallbacks are correctly
    dropped because the S002 strict parser guarantees all summary
    fields (nonnegative integers).
  - Discovery segments (renderDiscoverySegments port): identical
    lane-label grouping over active rows, fixed four-segment order
    ("Store / online", "Local store", "Product / category",
    "Brand / competitor"), `fmtNum` volume + "N keywords".
  - Overlap warnings (renderOverlapWarnings port): grouping key
    `clusterId|metricFingerprint` else `seed|searchVolume` with the
    identical per-row fingerprint (volume, monthly-history join, cpc,
    competition, keyword difficulty); in-group keyword dedup; ≥2 filter;
    sort by `volume×(len-1)` desc; shared/reported/overlap/variantCount
    arithmetic identical; total-track and per-item bar widths identical;
    empty state byte-equal ("No identical-volume variant groups in the
    filtered data.").
  - All values formatted through the I-F12 formatters (`fmtNum`,
    `fmtCpc`); zero `new Chart` instances (C5 → 0); all 44 CSS classes
    used are present in the S007 module (verified by exhaustive grep);
    `"use client"`; no fetch/localStorage.
- **Checks (independently re-run):** C1 write-set = the one file
  (single-file commit; tree clean after); C2 `npx tsc --noEmit` → 0; C3
  `npm run lint` → 0 errors (1 pre-existing traffic-globe.tsx warning);
  C4 `npm test` → 90/90 pass, 0 fail, 0 skipped; C5 `new Chart` → `0`.
- **Ending digest:** `3690e3f1436a036a5660b8ad3d3ae37cf7ad0032da532d35fd9570411ec9c559`.
- **Accepted deviations:** none.
- **Coverage accounting:** zero local case IDs at this leaf (`W5-B01`
  executes in S027 per the frozen allocation); no skips.
- **External mutations:** none.
- **Limitations/deferred:** rendered card/funnel/segment/overlap output
  verified at S025 substitute layer and the S027 browser harness.
- **Disposition:** `KI-W5-S011` ACCEPTED. Next assignable: `KI-W5-S012`.

---

## `EV-KI-W5-S17` — Window review of `KI-W5-S012` (keyword table component)

- **Timestamp:** 2026-08-19T18:55:00+05:30
- **Parent window / assignment / sub-window:** `KI-W5` / `ASG-KI-W5-WA-02` / `KI-W5-S012`
- **Actor/role:** `KI-W5-WINDOW-AGENT` (window review)
- **P1 block consumption (S1 §9.2):** no handoff quote form relayed;
  waiver recorded. Consumption proven from artifact literals: the
  fourteen `TABLE_COLS` definitions with byte-equal labels/tips/types to
  index.html:2347-2363 (a named `read_only_scope` anchor); the
  `aria-sort` requirement (an I-F14/§5.12 mandate absent from the
  standalone, which only mutates arrow text at
  index.html:2414-2426); the camelCase `itemId` row-key mandate (S1
  "KI-W5-T2 item 5" — the standalone uses `keywordId(row)`).
- **Leaf handoff summary:** CREATE
  `frontend/components/keyword-intelligence/keyword-table.tsx`, 380
  lines, committed by the requester as `83cf7dc` (parent `1bbf069` =
  S011); single-file diff (+380); ending digest
  `f7686eadc39500c4850a54b904cbe370ee11575fdbd4196c5fbdb0d5d110ce69`.
- **Contract verification (I-F14 KeywordTable) with port-fidelity
  comparison:**
  - Table head: sortable columns with `aria-sort` (ascending/descending/
    none) plus ▼/▲ arrows and the `.sorted` class — the
    `updateSortArrows` port (index.html:2414-2426) with the mandated
    accessibility addition; sort click semantics identical to
    `buildTableHead` (toggle direction on same key; new key: number
    columns default desc, string asc — index.html:2401-2412);
    sort logic delegated to S006's `sortKeywordRows` (the `compareRows`
    port verified at S006 review).
  - Body: rows keyed by `row.itemId` (C5 → 1); selection checkbox per
    row reflecting `selectionItemIds` with `.isSelected` row class and
    `aria-label`; `hl-vol` highlight ported with the standalone
    constants (`HVOL=500000`, `HCI=0.8`, `isHighVolumeCommercial` at
    index.html:932-935); trend cell port (`trendCell` — mono class,
    ▲/▼/• glyph, `fmtSlope`, identical title text); flags cell port
    (`flagsCell` — badge classes `flagDeclining`/`flagBroad`/
    `flagLow` + identical flag metadata labels/tips); per-column cell
    rendering with `fmtNum`/`fmtCpc`/`fmtPct`, "—" null markers,
    capitalized intent, lane labels; keyword-cell title attribute.
  - Edit control: emits `onEditItem(itemId)`; the not-selected branch
    first calls `onToggleRow` then `onEditItem` (add-then-edit); label
    "In form ✓"/"Add to form →" with accessible aria-labels.
  - Pagination: "Page X of Y" info, Prev/Next with the standalone's
    disabled bounds (`page <= 1`, `page >= pageCount`,
    index.html:2559-2560), page-size select with the standalone sizes
    10/25/50/100 (index.html:705-710) resetting to page 1; counting via
    `paginate` clamping; row count "{n} row(s)" matching `table-count`
    (index.html:2557).
  - Empty state: "No keywords match the current filters." byte-equal to
    index.html:2478 (the `renderTable` empty row, not the hero variant
    at :563).
  - Deliberate divergence (recorded, not a defect): the standalone's
    `select-all-keywords` checkbox (index.html:2371-2376) is not
    ported — I-F14 defines no `onToggleAll` prop; selection state is
    owned by the S016 orchestrator per the frozen props contract. The
    header select column remains.
  - Hygiene: `styles.kiDashboard` scoping on the section; all 30 CSS
    classes verified present in the S007 module (incl.
    `.badge.flagDeclining/flagBroad/flagLow` at module:559-563 and
    `th .arrow`/`th.sorted .arrow` at :522-524); zero `new Chart`;
    `"use client"`; no fetch/localStorage. A few inline styles port
    standalone inline styling (flags wrap, empty cell, pagination row)
    — visually necessary, values identical to the standalone markup.
- **Checks (independently re-run):** C1 write-set = the one file
  (single-file commit; tree clean after); C2 `npx tsc --noEmit` → 0; C3
  `npm run lint` → 0 errors (1 pre-existing traffic-globe.tsx warning);
  C4 `npm test` → 90/90 pass, 0 fail, 0 skipped; C5 `key={row.itemId}`
  → `1`.
- **Ending digest:** `f7686eadc39500c4850a54b904cbe370ee11575fdbd4196c5fbdb0d5d110ce69`.
- **Accepted deviations:** none beyond the recorded select-all design
  note.
- **Coverage accounting:** zero local case IDs at this leaf (`W5-C06`,
  `W5-B02/B03` execute in S025/S027 per the frozen allocation); no
  skips.
- **External mutations:** none.
- **Limitations/deferred:** rendered interaction (sort clicks,
  pagination, selection sync) verified at S025 substitute layer and S027
  browser harness.
- **Disposition:** `KI-W5-S012` ACCEPTED. Next assignable: `KI-W5-S013`.

---

## `EV-KI-W5-S18` — Window review of `KI-W5-S013` (selection review component) — CORRECTION REQUIRED

- **Timestamp:** 2026-08-19T19:25:00+05:30
- **Parent window / assignment / sub-window:** `KI-W5` / `ASG-KI-W5-WA-02` / `KI-W5-S013`
- **Actor/role:** `KI-W5-WINDOW-AGENT` (window review)
- **P1 block consumption:** proven — the component implements the full
  §5.13 feature list (ordered list with rank/source/lane/facet chips,
  manual add via the `parseKeywordLines` port, edit dialog with
  original-keyword preservation and pre-commit reclassification preview
  through the I-F12 helpers, over-100 banner, `DEC-KI-015` conflict list
  with pair keywords/reason/similarity/canonical suggestion, save gated
  on `saving || staleConflict`, finalize gated on
  `canFinalizeSelection(...).ok`, `finalizeState === "handing-off"`
  double-click guard with `clientRequestId` correctly left to the
  parent).
- **Leaf handoff summary:** CREATE, 464 lines, commit `6f99357`
  (parent `83cf7dc` = S012); single-file diff (+464); digest
  `2aec2619962e8de100f68f829f3bf5db5114dd3267636ecbad520ac030e5517e`.
- **Passing checks:** C2 `npx tsc --noEmit` → 0; C3 `npm run lint` → 0
  errors (1 pre-existing warning); C4 `npm test` → 90/90; C5
  `localStorage` grep → `0`; all 38 CSS classes present in the S007
  module; toast timer cleaned up on unmount; accessible dialog
  (`role="dialog"`, `aria-modal`, labels); 160-code-point bound and
  duplicate detection on manual add and edit; empty-state texts; C1
  single-file write set.
- **Defect 1 (leaf defect, fix determined):** manual item IDs are
  generated by `newClientRequestId()` (selection-review.tsx:175) — 32
  bare hex chars. The authoritative backend PUT validator requires
  `itemId` to match `/^ksi_[a-f0-9]{12}$/u`
  (`email_scraper/src/keyword-intelligence/selection.js:151`,
  `invalid_item_id` otherwise), per `DEC-KI-014` "a new stable item ID"
  in this block's own `read_only_scope`. Every manual keyword would be
  rejected with 400 on save. Fix: deterministic `ksi_`-prefixed 12-hex
  IDs (stable per normalized text, deduped within the draft).
- **Defect 2 (frozen-interface defect — I-F14 `SelectionReview` props
  incomplete; decomposition authoring error, not a leaf error):** the
  component owns a private `workingDraft` (resynced on prop identity
  change), but the frozen props provide only `onSave: () => void` — no
  upward draft channel. `KI-W5-S016` step 2 saves
  `saveKeywordSelection(researchId, view.selectionRevision, draft)`
  with the parent's own draft, so all manual adds/removes/edits made in
  `SelectionReview` are silently lost on save, and the finalize gate
  evaluates a working copy the parent never persists. The block's
  feature list and its props contract are mutually unsatisfiable as
  frozen. Fix direction is determined (lift draft changes up), but it
  amends frozen `I-F14` and therefore requires requester authorization
  and an append-only erratum before the corrective leaf executes.
- **Disposition:** `KI-W5-S013` NOT accepted as-is. Corrective
  sub-window `KI-W5-C001` (same writable file,
  `frontend/components/keyword-intelligence/selection-review.tsx`, same
  27-file set) authorized workflow: fix Defect 1; fix Defect 2 pending
  requester authorization of the I-F14 amendment (add
  `onDraftChange: (draft: SelectionItem[]) => void` to the frozen
  props; S016 composes it; erratum recorded here and in S1 §9-style
  addendum if the requester prefers S1 visibility). Evidence
  invalidation: none of S001–S012 consumes this component; no accepted
  evidence changes.
- **External mutations:** none.

---

## `EV-KI-W5-S19` — `KI-W5-C001` corrective execution (window agent as corrective leaf, requester-authorized) and I-F14 amendment

- **Timestamp:** 2026-08-19T19:55:00+05:30
- **Parent window / assignment / sub-window:** `KI-W5` / `ASG-KI-W5-WA-02` / `KI-W5-C001` (corrective; fixes `KI-W5-S013`)
- **Actor/role:** `KI-W5-WINDOW-AGENT` executing the corrective leaf directly under requester authorization ("let's not make another leaf for now, you can act as a corrective leaf and fix it, also i am authorizing this one dicision to alter the frozen contract", 2026-08-19).
- **Contract amendment (Defect 2):** appended S1 §10 (requester-authorized; S1 digest becomes
  `cad439e085655a3e404ac2eedda1377eb9215ec4019df931dcb54617f160d0e7`;
  frozen §0–§9 byte-identical). `SelectionReview` props amended to add
  `onDraftChange: (draft: SelectionItem[]) => void`; the component is
  fully controlled (every mutation computes the next draft and calls
  exactly `onDraftChange(next)`; the parent owns the single draft and
  saves that copy per S016 step 2).
- **Code corrections applied to
  `frontend/components/keyword-intelligence/selection-review.tsx`:**
  1. Defect 2: removed the private `workingDraft`/`prevDraft` state and
     the identity-resync branch; all reads (`gate`, `overLimit`,
     `editingItem`, `reclassified`, `keywordById`, render) now use the
     `draft` prop; `commitEdit`/`addManualKeywords`/`removeItem` now end
     in `onDraftChange(next)` (5 call sites incl. the props signature).
     No other behavioral change.
  2. Defect 1: removed the `newClientRequestId` import and usage (grep →
     0); added `manualItemDigest` (three FNV-1a 32-bit lanes seeded
     `0x811c9dc5`/`0x9e3779b9`/`0x85ebca6b` over `salt\ntext`, each lane
     contributing 4 hex chars via `Math.imul` with `>>> 0`) and
     `stableManualItemId(text, draft)` producing `ksi_` + exactly 12
     lowercase hex, deterministically, with in-draft collision salting —
     matching the authoritative backend PUT validation
     `/^ksi_[a-f0-9]{12}$/u` (`selection.js:151`).
- **Verification:** C2 `npx tsc --noEmit` → 0; C3 `npm run lint` → 0
  errors (1 pre-existing traffic-globe.tsx warning); C4 `npm test` →
  90/90 pass; C5 `localStorage` grep → 0. ID-algorithm probes
  (identical algorithm re-implemented in the probe): format basic and
  unicode, exactly 12 hex, deterministic, salt-sensitive,
  text-sensitive — 6/6 pass. `newClientRequestId` grep → 0.
- **Resulting file:** 483 lines; ending digest
  `5d127c195a2553cc077b4b1a3f592add08a184b9761cfce658fbb810b248f992`
  (supersedes S013's `2aec2619…`; commit `6f99357` stands as the
  pre-correction history; requester commits the correction).
- **Deferred:** browser-harness exercise of the manual-add/edit/remove →
  save round trip (`W5-B03/B04`, `W5-A09/A10`, `W5-R03`, `W5-NC09`)
  remains allocated to S024/S025/S027 per the frozen allocation; S016
  must compose `onDraftChange` per the amended I-F14 (its block step 2
  already saves the parent-owned draft — no S016 block change needed).
- **External mutations:** none beyond the authorized S1 §10 append and
  the single-file code correction.
- **Disposition:** both `EV-KI-W5-S18` defects closed;
  `KI-W5-S013` ACCEPTED (superseding digest `5d127c19…`);
  `KI-W5-C001` closed. `KI-W5-S014` is next and assignable.

---

## `EV-KI-W5-S20` — Window review of `KI-W5-S014` (chart panels component)

- **Timestamp:** 2026-08-19T20:35:00+05:30
- **Parent window / assignment / sub-window:** `KI-W5` / `ASG-KI-W5-WA-02` / `KI-W5-S014`
- **Actor/role:** `KI-W5-WINDOW-AGENT` (window review)
- **P1 block consumption:** proven — the eleven `data-surface="chart:…"`
  canvas ids are the exact I-F15 literals (S1 §3.8); the destroy/recreate
  refresh path and "exactly one Chart per canvas" mandate are §5.14/I-F17
  text absent from the standalone; the no-CDN prohibition is the block's
  additional prohibited action. Quote form not relayed; waiver recorded.
- **Leaf handoff summary:** CREATE
  `frontend/components/keyword-intelligence/chart-panels.tsx`, 1295
  lines, committed by the requester as `006301c` (parent `9eec30e` =
  the S013 correction — verified byte-identical to the `KI-W5-C001`
  output, digest `5d127c19…`); single-file diff (+1295); ending digest
  `0297f218dfe4cdfa08c644434c9475b0ab62570efb6f7de96bf56477e01c8835`.
- **Contract verification (I-F14/I-F17):**
  - Local imports only: `chart.js` named controllers/elements/scales +
    `chartjs-chart-treemap` (`TreemapController`, `TreemapElement`);
    module-scope `Chart.register(...)` executes exactly once with the
    needed set (Arc/Bar/Bubble/Doughnut/Line/Scatter controllers and
    elements, Category/Linear scales, Filler, Legend, Tooltip, treemap
    controller+element).
  - Eleven component-owned `<canvas ref>` elements, each with the exact
    I-F15 id — including the two materialized charts
    (`chart:cluster-volume`, `chart:treemap`) whose standalone canvases
    were absent from the static DOM (S1 §8 recorded interpretation,
    satisfied); the wrapper carries `data-surface="surface:chart-panels"`.
  - Dataset preparation memoized once per inputs via one `useMemo` over
    the I-F12 outputs (`getFiltered` with market override, `activeRows`,
    `aggregateByCluster`, seeds/funnel aggregations, 10-bin histogram
    with null exclusion, flag counts, history eligibility) — deps
    `[rows, filter, marketCode, result]`.
  - Lifecycle: one `Chart` per canvas created in a single effect; every
    dataset/theme/market change re-runs the effect whose prior cleanup
    destroys every instance (destroy/recreate — the standalone
    `renderCharts` refresh path, explicitly sanctioned by the block);
    unmount destroys all; construction errors are caught, partial
    instances destroyed, and the safe error banner surfaced.
  - Chart configs port the named standalone functions: top-keywords
    bar+line dual-axis (yVolume/yTrend, truncated labels, CPC/CI tooltip
    details), cluster-volume horizontal bars with
    `lerpColor(primary→amber)` share shading, bubble (difficulty×volume,
    sqrt(CPC) radius, CI color), scatter (competition×opportunity with
    -0.04/1.04 axis padding and 0..100 clamp), two doughnuts (intent
    mix, recommended/rejected, 62% cutout), seeds stacked horizontal
    three-dataset (recommended/declining/remaining with afterBody stats
    incl. `median`), histogram (10-point bins, precision-0 ticks),
    treemap (`tree`/`key: value`, per-node lerp color, centered bold
    labels, share tooltips), flags (per-flag colors + tips), history
    (all-combined or per-keyword monthly line, sorted chronologically,
    fill). `tooltipBase`/`baseScales` ports present with the standalone
    fallback literals.
  - Empty states: `.chartEmpty` overlays per chart with `hidden`
    toggling and chart-specific texts; zero-size datasets return `null`
    configs (no Chart created).
  - Theme reactivity: `MutationObserver` on `data-ki-theme` bumps a tick
    that re-runs the effect → palette recomputed from CSS variables —
    supports the S016 theme toggle without touching document root.
  - History keyword select with "all" fallback when the selected keyword
    filters out; top-chart `minWidth` scaling ported.
- **Checks (independently re-run):** C1 write-set = the one file
  (single-file commit `006301c`; tree clean after); C2 `npx tsc
  --noEmit` → 0; C3 `npm run lint` → 0 errors (1 pre-existing
  traffic-globe.tsx warning); C4 `npm test` → 90/90 pass, 0 fail,
  0 skipped; C5 CDN/loadScript/loadFirst grep → `0`; chart.js import
  grep → ≥1; treemap import grep → ≥1; all 16 CSS classes used present
  in the S007 module.
- **Ending digest:** `0297f218dfe4cdfa08c644434c9475b0ab62570efb6f7de96bf56477e01c8835`.
- **Accepted deviations (recorded, cosmetic):** seven of eleven charts
  call `tooltipBase(null)`, so their tooltip colors use the universal
  fallback literals rather than live theme variables (dark-theme tooltip
  chrome differs from the standalone's themed tooltips); no data,
  oracle, or inventory impact.
- **Coverage accounting:** zero local case IDs at this leaf (`W5-B07`,
  `W5-R06`, `W5-I06`, `W5-NC04/NC06` execute in S026/S027 per the
  frozen allocation); no skips.
- **External mutations:** none.
- **Limitations/deferred:** rendered chart output, destroy-on-unmount,
  and no-CDN behavior verified at S027 browser harness (`KI-W5-V1`).
- **Disposition:** `KI-W5-S014` ACCEPTED. Next assignable: `KI-W5-S015`.

---

## `EV-KI-W5-S21` — Window review of `KI-W5-S015` (cluster landscape component)

- **Timestamp:** 2026-08-19T20:55:00+05:30
- **Parent window / assignment / sub-window:** `KI-W5` / `ASG-KI-W5-WA-02` / `KI-W5-S015`
- **Actor/role:** `KI-W5-WINDOW-AGENT` (window review)
- **Numbering note:** the requester wrote "S016"; disk truth is commit
  `2841151` "S15" containing exactly
  `frontend/components/keyword-intelligence/cluster-landscape.tsx`
  (+727) — this is `KI-W5-S015`. `research-dashboard.tsx` (S016) does
  not exist yet; S016 remains to be dispatched.
- **P1 block consumption:** proven — the ported constants
  (azimuth `-0.45`, zoom clamp `0.55–1.8`, wheel
  `Math.exp(-event.deltaY * 0.0012)`, `volumeNorm = log(v+1)/log(max+1)`
  with `nz = norm × 0.86`, radius `3 + norm × 6`, ground plane
  `0.68/0.31/0.46` factors, DPR clamp 2) are byte-equal to
  `drawClusterLandscape` (index.html:2880+ and anchors 780/2886/2912-13/
  2917/3104); the pointerId-keyed pinch/drag model, the no-Chart/no-WebGL
  mandates, and the DPR+ResizeObserver requirements are §5.15/I-F14 text
  absent from the standalone. Quote form not relayed; waiver recorded.
- **Leaf handoff summary:** CREATE, 727 lines, commit `2841151` (parent
  `006301c` = S014); single-file diff (+727); ending digest
  `2304b0c8c9d40b89a364a2ad1badd6ba871767a7bad49fdf30f2257675409e6a`.
- **Contract verification (I-F14 ClusterLandscape):** exact props
  (`clusters`/`selectedClusterId`/`onSelect`); raw canvas 2D context
  (zero `new Chart`/WebGL — grep 0); isometric projection ported
  verbatim (save/translate/scale camera scaffold, `viewDepth`,
  `project`, gradient ground plane with 5×5 grid lines at identical
  alpha/width steps); depth-sorted pillar rendering (stem lines, ground
  ellipses `0.9/0.22` factors, radial-gradient glow spheres with white
  core → color → 0.42 fade, `recommendedForStoreDiscovery` green ring);
  axis triad (Opportunity/Trend/Volume arrows at `width-142,height-34`);
  hit-test radius `max(8, r+3)` top-most-first (reverse find); pointer
  events keyed by `pointerId` in `pointersRef` with `setPointerCapture`,
  single-pointer azimuth drag (`dx/max(320,width)×2π`), two-pointer
  pinch zoom with `pinchZoom` anchor and >2px move threshold; pointerup
  hit test suppressed after drag (`moved` flag) selecting
  `onSelect(clusterId|null)`; `pointercancel` releases cleanly; wheel
  zoom `preventDefault` with `{passive:false}`; double-click + Reset
  button restore `-0.45`/`1`; zoom ± buttons ×1.2 clamped; hover
  tooltip (escaped HTML, identical field set + "N keywords · volume ·
  Opportunity · Trend · CPC · Recommended") with edge clamping;
  mouseleave hides; DPR-aware sizing via `devicePixelRatio` clamped to
  2 with ResizeObserver on the scene; all 11 listeners added and
  removed in cleanup plus observer disconnect; `onSelectRef` avoids
  stale closures. Legend: scroll area with per-cluster buttons
  (color dot, rank, truncate-28 name, volume/share/opp/trend stats,
  `data-cluster-detail` + accessible aria-label/aria-describedby),
  hover/focus pill tooltip positioned with viewport clamping, scroll
  hides it; cluster count line ("N clusters · M keyword points");
  inspector for the selected cluster (shared-token analysis with the
  standalone stop-token list and half-membership threshold, lane-count
  line via `laneLabel`, overlap note, keyword chips, variant groups
  canonical → variants); empty state ("No clusters match the current
  filters."); surfaces `data-surface="surface:cluster-landscape"` and
  `landscape:cluster-scene` per I-F15; 12-color palette ported.
- **Checks (independently re-run):** C1 write-set = the one file
  (single-file commit; tree clean after); C2 `npx tsc --noEmit` → 0; C3
  `npm run lint` → 0 errors (1 pre-existing traffic-globe.tsx warning);
  C4 `npm test` → 90/90 pass, 0 fail, 0 skipped; C5 addEventListener →
  `11` (≥4), removeEventListener → `11` (≥4); all 29 CSS classes used
  present in the S007 module.
- **Ending digest:** `2304b0c8c9d40b89a364a2ad1badd6ba871767a7bad49fdf30f2257675409e6a`.
- **Accepted deviations:** none.
- **Coverage accounting:** zero local case IDs at this leaf (`W5-B07`,
  `W5-R05/R06` execute in S027 per the frozen allocation); no skips.
- **External mutations:** none.
- **Limitations/deferred:** rendered interaction (drag/pinch/wheel/hit
  test/inspector) verified at the S027 browser harness (`KI-W5-V1`).
- **Disposition:** `KI-W5-S015` ACCEPTED. Next assignable: `KI-W5-S016`
  (research dashboard orchestrator).

---

## `EV-KI-W5-S22` — Window review of `KI-W5-S016` (research dashboard orchestrator)

- **Timestamp:** 2026-08-19T21:35:00+05:30
- **Parent window / assignment / sub-window:** `KI-W5` / `ASG-KI-W5-WA-02` / `KI-W5-S016`
- **Actor/role:** `KI-W5-WINDOW-AGENT` (window review)
- **P1 block consumption:** proven — the amended `onDraftChange`
  composition (S1 §10 / I-F14 after `KI-W5-C001`), the
  `finalizeState` ref-retained `clientRequestId` idempotency, the
  409-code-specific `KEYWORD_SELECTION_REVISION_CONFLICT` branch, the
  GET-only retry semantics, and the I-F15 surface-wrapper split
  (children without own surfaces get wrapper divs; ChartPanels/
  ClusterLandscape carry their own) are §5.16/I-F14/I-F15 text with no
  standalone counterpart (the standalone has no revision-conflict,
  client-request-id, or surface-inventory concepts). Quote form not
  relayed; waiver recorded.
- **Leaf handoff summary:** CREATE, 479 lines, commit `9606cfd`
  "S016" (parent `2841151` = S015); single-file diff (+479); tree
  clean after; ending digest
  `94ba68eec79302352bdd6ac387bd8f27586ba0bb078d80b7b1390c56518ef023`.
- **Contract verification (I-F14 ResearchDashboard / §5.16):**
  required state set present (`view, draft, filter, theme, saving,
  staleConflict, finalizeState`) plus supporting load/auth/reload/
  saveError/selectedClusterId states; initial load once per mount via
  `getKeywordResearch` with a `disposed` guard and explicit-retry
  `reloadVersion` (GET only); `ResearchStatus` renders for
  queued/running with `onTerminal={setView}`; failed terminal renders
  `view.safeError` (code + message) with GET-only retry; completed
  composes FilterBar/SummaryCards/KeywordTable/SelectionReview/
  ChartPanels/ClusterLandscape with `useMemo` wiring of the I-F12
  selectors (`getFiltered`, `activeRows`, `filterOptionSources`,
  `distinctKeywordRows`, `aggregateByCluster`, `cumulativeVolume`,
  `adjustedVolume`, `currentClusterMetric` per `filter.market`);
  save calls `saveKeywordSelection(researchId,
  view.selectionRevision, draft)` (block "saveKeywordResearch" typo
  resolved to the S005 export) and applies the returned
  view/selection/selectionRevision only after `await` success via
  `setView(next)` + revision-gated draft sync; 409 with
  `code === "KEYWORD_SELECTION_REVISION_CONFLICT"` sets
  `staleConflict`, `handleSave` refuses while stale, explicit
  "Reload dashboard" performs the GET-only reload — a stale response
  never overwrites local display; finalize gates on
  `canFinalizeSelection`, generates `newClientRequestId()` once into a
  ref, reuses it for duplicate clicks (idempotent), disables via
  `finalizeState === "handing-off"`, navigates
  `router.push(handoff.statusUrl)` on success, resets id + state on
  failure, 409 → staleConflict; market switch changes `filter.market`
  only (draft/selection untouched); theme toggle writes only the
  I-F12 key `ki-dashboard-theme` (getItem+setItem both keyed) and
  drives `data-ki-theme` on the root (S014 MutationObserver contract);
  export anchor
  `/api/keyword-research/${researchId}/export.csv?${buildExportQuery(filter)}`;
  `data-ki-theme` + `data-surface="surface:research-dashboard"` on
  every render branch (auth, load-error, loading, status, failed,
  completed); surface wrappers for the five children lacking own
  surfaces; `dashboardPhase(view, null)` empty-state guard. Child prop
  signatures cross-checked against accepted S008–S015 outputs.
- **Checks (independently re-run):** C1 write-set = the one file
  (commit `9606cfd`, +479); C2 `npx tsc --noEmit` → 0; C3
  `npm run lint` → 0 errors (1 pre-existing traffic-globe.tsx
  warning); C4 `npm test` → 90/90 pass, 0 fail; C5 `localStorage` →
  `2` (≥1; both uses keyed), `KEYWORD_THEME_STORAGE_KEY` → `3` (≥1;
  the only storage key), `newClientRequestId` → `2` (≥1);
  `data-surface` → 12.
- **Ending digest:** `94ba68eec79302352bdd6ac387bd8f27586ba0bb078d80b7b1390c56518ef023`.
- **Accepted deviations:** one cosmetic — `encodeURIComponent(researchId)`
  in the export path segment (I-F14 literal uses bare `${researchId}`);
  matches the S005 client-api convention and is a no-op for `res_…`
  ids; no behavioral difference.
- **Observation (no action):** `setSelectedClusterId(null)` during
  render at lines 181-183 is the guarded React derived-state-adjust
  pattern (prunes a selected cluster that filters removed); legal,
  idempotent, re-render-only.
- **Coverage accounting:** zero local case IDs at this leaf (all B/R
  cases execute in S024–S027 per the frozen allocation); no skips.
- **External mutations:** none.
- **Limitations/deferred:** end-to-end interaction (save/409/finalize/
  navigation/theme/export) verified at the S024–S027 test leaves and
  the `KI-W5-V1` browser gate.
- **Disposition:** `KI-W5-S016` ACCEPTED. Next assignable: `KI-W5-S017`
  (API route leaf).

---

## `EV-KI-W5-S23` — Window review of `KI-W5-S017` (create research route)

- **Timestamp:** 2026-08-19T22:10:00+05:30
- **Parent window / assignment / sub-window:** `KI-W5` / `ASG-KI-W5-WA-02` / `KI-W5-S017`
- **Actor/role:** `KI-W5-WINDOW-AGENT` (window review)
- **P1 block consumption:** proven — the I-F6 guard order
  (415 `UNSUPPORTED_CONTENT_TYPE` → 413 `REQUEST_TOO_LARGE` → 400
  `INVALID_JSON` → 400 `KEYWORD_RESEARCH_INPUT_INVALID` → 401
  passthrough → `proxyBackend` POST), the re-serialized
  `JSON.stringify({ seeds })` forwarding rule, the 32768-byte cap, the
  15_000 timeout, and the verbatim message "One to five research seed
  phrases are required." are §3.3/I-F6 + §5.17 contract text; the
  `runs/route.ts` reference pattern is honored (content-type lowercase
  prefix check, `TextEncoder().encode(body).byteLength` sizing,
  nodejs/force-dynamic exports). Quote form not relayed; waiver
  recorded.
- **Leaf handoff summary:** CREATE, 49 lines, commit `1168e7a` "S017"
  (parent `9606cfd` = S016); single-file diff (+49, plus directory);
  tree clean after; ending digest
  `259bdfb4460cb5b4f3a34c55cc25fa7dbecfcbc6db6075938c5d9d424d23ca41`.
- **Contract verification (I-F6):** exports `POST` only; `runtime =
  "nodejs"` + `dynamic = "force-dynamic"`; imports `jsonError`/
  `proxyBackend` from `@/lib/backend-proxy` and `authenticatedRoute`
  from `@/lib/auth/route`; guard order exactly: Content-Type
  `application/json` prefix (415) → body ≤ `MAX_BODY_BYTES = 32 *
  1024` (413) → `JSON.parse` (400 `INVALID_JSON`) →
  `validateSeedsInput(parsed)` else 400
  `KEYWORD_RESEARCH_INPUT_INVALID` with the verbatim message →
  `auth = await authenticatedRoute()` with 401 passthrough of
  `auth.response` → `proxyBackend({ path: "/api/keyword-research",
  method: "POST", body: JSON.stringify({ seeds: validated.seeds }),
  timeoutMs: 15_000, userId: auth.userId })` — `seeds` is exactly the
  validated array (re-serialization, not raw forward). Helper shapes
  cross-checked: `validateSeedsInput` returns
  `{ ok: true; seeds: string[] } | { ok: false; error }` (S002
  output), `authenticatedRoute` returns `{ response }` 401 envelope or
  `{ userId }` (`lib/auth/route.ts:10`).
- **Checks (independently re-run):** C1 write-set = the one file
  (commit `1168e7a`, +49); C2 `npx tsc --noEmit` → 0; C3
  `npm run lint` → 0 errors (1 pre-existing traffic-globe.tsx
  warning); C4 `npm test` → 90/90 pass, 0 fail; C5
  `export async function POST|GET` count → `1` (exactly POST).
- **Ending digest:** `259bdfb4460cb5b4f3a34c55cc25fa7dbecfcbc6db6075938c5d9d424d23ca41`.
- **Accepted deviations:** none.
- **Coverage accounting:** zero local case IDs at this leaf
  (`W5-A01/A02`, `W5-R07` execute in S024–S027 per the frozen
  allocation); no skips.
- **External mutations:** none.
- **Limitations/deferred:** route behavior (415/413/400/401 ordering,
  proxy forwarding) verified at the S024–S026 route test leaves.
- **Disposition:** `KI-W5-S017` ACCEPTED. Next assignable: `KI-W5-S018`
  (get research route).

---

## `EV-KI-W5-S24` — Window-level environmental fix + review of `KI-W5-S018` (get research route)

- **Timestamp:** 2026-08-19T23:05:00+05:30
- **Parent window / assignment / sub-window:** `KI-W5` / `ASG-KI-W5-WA-02` / `KI-W5-S018`
- **Actor/role:** `KI-W5-WINDOW-AGENT` (environmental fix under requester authorization; window review)
- **Blocker diagnosis (leaf escalation, confirmed on disk):** C2 failed with
  exactly two errors — TS2344 on
  `RouteContext<"/api/keyword-research/[researchId]">` and its TS2339
  cascade — caused solely by the stale gitignored
  `.next/types/routes.d.ts` (mtime Aug 17 12:20, zero
  `keyword-research` entries; predates the entire W5 route tree),
  imported via `next-env.d.ts`. Root cause is structural: I-F7–I-F10
  freeze typed `RouteContext` literals that only typecheck against
  the generated `AppRouteHandlerRoutes` union, which regenerates only
  via `next dev`/`next build`/`next typegen` — all reserved for
  `KI-W5-I001` by S1 §4.1 — while C2 is a leaf-level check. Every
  `[researchId]` route leaf (S018–S021) hits the same wall; S017
  passed only because it is a static route with a plain `Request`
  signature. The leaf stopped correctly (no signature weakening, no
  generator run).
- **Environmental fix (requester-authorized this date, option "Authorize
  next typegen"):** window agent ran `npx next typegen` once from
  `frontend/`. Outcome: "Types generated successfully"; regenerated
  `.next/types/routes.d.ts` now lists `/api/keyword-research` and
  `/api/keyword-research/[researchId]` in `AppRouteHandlerRoutes` and
  the params map. Write set verified gitignored-only (`git status`
  clean before and after; `.next/types/routes.d.ts` confirmed inside
  `.gitignore` via `git check-ignore`) — zero tracked files touched,
  no network, no external mutation, complying with root AGENTS "keep
  generated/build output out of Git". This refresh is a standing
  window-level environmental baseline for the remaining route leaves;
  it does not authorize leaf-level generators and does not alter S1.
- **P1 block consumption:** proven — the I-F7 ordering
  (`authenticatedRoute` → 401 passthrough → awaited params →
  `validKeywordResearchId` guard → proxy GET), the verbatim 400
  `INVALID_RESEARCH_ID` "The research ID is invalid." message, the
  `RouteContext<"/api/keyword-research/[researchId]">` signature
  literal, `encodeURIComponent`, and `timeoutMs: 10_000` are §3.3/I-F7
  + §5.18 contract text mirrored from `runs/[runId]/route.ts:13`.
  Quote form not relayed; waiver recorded.
- **Leaf handoff summary:** CREATE, 27 lines, commit `a07fe65` "S018"
  (parent `1168e7a` = S017); single-file diff (+27, plus directory);
  tree clean after; ending digest
  `fbc9e75dc69448387323655a1c3ca2ee5152aeefe5dc5351e4a0368369beb064`
  (matches leaf handoff).
- **Contract verification (I-F7):** exports `GET` only; `runtime =
  "nodejs"` + `dynamic = "force-dynamic"`; imports
  `authenticatedRoute`/`jsonError`+`proxyBackend`/
  `validKeywordResearchId`; signature
  `GET(_request: Request, context: RouteContext<"/api/keyword-research/[researchId]">)`;
  order: auth 401 passthrough → `const { researchId } = await
  context.params;` → guard else 400 `INVALID_RESEARCH_ID` with the
  verbatim message → `proxyBackend({ path:
  \`/api/keyword-research/${encodeURIComponent(researchId)}\`,
  timeoutMs: 10_000, userId: auth.userId })`. Helper shape
  cross-checked: `validKeywordResearchId` exported from the S002
  validation module.
- **Checks (independently re-run after typegen):** C1 write-set = the
  one file (commit `a07fe65`, +27); C2 `npx tsc --noEmit` → **0**
  (both errors resolved by the regenerated union — sole-cause
  confirmed); C3 `npm run lint` → 0 errors (1 pre-existing
  traffic-globe.tsx warning); C4 `npm test` → 90/90 pass, 0 fail; C5
  `grep -c "validKeywordResearchId"` → `2` (≥ 1).
- **Ending digest:** `fbc9e75dc69448387323655a1c3ca2ee5152aeefe5dc5351e4a0368369beb064`.
- **Accepted deviations:** none.
- **Coverage accounting:** zero local case IDs at this leaf (`W5-A04`,
  `W5-R02/R04/R07` execute in S024–S027 per the frozen allocation);
  no skips.
- **External mutations:** none (typegen writes gitignored build
  output only; requester-authorized).
- **Limitations/deferred:** route behavior (401/400 ordering, proxy
  forwarding, no-store) verified at the S024–S026 route test leaves;
  the `KI-W5-I001` build re-verifies C2 with freshly generated types.
- **Disposition:** `KI-W5-S018` ACCEPTED (blocker resolved at window
  level, no file correction needed). Next assignable: `KI-W5-S019`
  (selection PUT route).

---

## `EV-KI-W5-S25` — Window review of `KI-W5-S019` (save selection route)

- **Timestamp:** 2026-08-19T23:40:00+05:30
- **Parent window / assignment / sub-window:** `KI-W5` / `ASG-KI-W5-WA-02` / `KI-W5-S019`
- **Actor/role:** `KI-W5-WINDOW-AGENT` (window review)
- **P1 block consumption:** proven — the I-F8 mandates prove block reads:
  the 262144-byte cap, the exact key-set + `expectedRevision` safe
  integer ≥ 1 + `items` ≤ 200 structural validation with the verbatim
  400 `KEYWORD_SELECTION_INPUT_INVALID` "The selection payload is
  invalid." message, the same param guard as I-F7 (400
  `INVALID_RESEARCH_ID` "The research ID is invalid."), the
  **verbatim original-body-string** forwarding rule (explicitly
  contrasted with I-F6's re-serialization), the PUT method, the
  `encodeURIComponent(researchId)/selection` path, and `timeoutMs:
  15_000` are §3.3/I-F8 + §5.19 contract text. Quote form not
  relayed; waiver recorded.
- **Leaf handoff summary:** CREATE, 74 lines, commit `a6d4c52` "S019"
  (full `a6d4c522b72744b35e364119312038807c381cfc`; parent `a07fe65`
  = S018); single-file diff (+74, plus directory); tree clean after;
  ending digest
  `3c44ed2f3c54d949582f0a0779168487584a28908f7d8387efc32e06cfc7af29`.
- **Contract verification (I-F8):** exports `PUT` only; `runtime =
  "nodejs"` + `dynamic = "force-dynamic"`; signature
  `PUT(_request: Request, context: RouteContext<"/api/keyword-research/[researchId]/selection">)`;
  guard order exactly: Content-Type prefix (415
  `UNSUPPORTED_CONTENT_TYPE`) → body ≤ `MAX_BODY_BYTES = 262144`
  (413 `REQUEST_TOO_LARGE`) → `JSON.parse` (400 `INVALID_JSON`) →
  structural validation: object-not-array/null, `keys.length !== 2`,
  `Number.isSafeInteger(record.expectedRevision)` with `>= 1`,
  `Array.isArray(record.items)` with `length <= 200`, else 400
  `KEYWORD_SELECTION_INPUT_INVALID` verbatim message (wrong key names
  necessarily fail the type checks — exact key-set enforced) →
  `authenticatedRoute()` 401 passthrough → awaited params →
  `validKeywordResearchId` guard else 400 `INVALID_RESEARCH_ID`
  verbatim message → `proxyBackend({ path, method: "PUT", body,
  timeoutMs: 15_000, userId })` forwarding the original body string
  verbatim (no re-serialization). Item-internal shape correctly left
  backend-authoritative per the frozen block.
- **Checks (independently re-run):** C1 write-set = the one file
  (commit `a6d4c52`, +74); C2 `npx tsc --noEmit` → **0** after a
  standing-baseline typegen refresh (this leaf introduces a new route
  literal `/api/keyword-research/[researchId]/selection`; gitignored
  `.next/` writes only, git tree clean before/after); C3 `npm run
  lint` → 0 errors (1 pre-existing traffic-globe.tsx warning); C4
  `npm test` → 90/90 pass, 0 fail; C5
  `grep -c "262144\|expectedRevision"` → `3` (≥ 2).
- **Ending digest:** `3c44ed2f3c54d949582f0a0779168487584a28908f7d8387efc32e06cfc7af29`.
- **Accepted deviations:** none.
- **Coverage accounting:** zero local case IDs at this leaf (`W5-R03`,
  `W5-R07` execute in S024–S027 per the frozen allocation); no skips.
- **External mutations:** none (typegen writes gitignored build output
  only, under the standing `EV-KI-W5-S24` baseline).
- **Limitations/deferred:** route behavior (guard ordering, verbatim
  forwarding, CAS semantics) verified at the S024–S026 route test
  leaves; `KI-W5-I001` re-verifies C2 with freshly built types.
- **Disposition:** `KI-W5-S019` ACCEPTED. Next assignable: `KI-W5-S020`
  (create run route).

---

## `EV-KI-W5-S26` — Window review of `KI-W5-S020` (create run route)

- **Timestamp:** 2026-08-19T23:59:00+05:30
- **Parent window / assignment / sub-window:** `KI-W5` / `ASG-KI-W5-WA-02` / `KI-W5-S020`
- **Actor/role:** `KI-W5-WINDOW-AGENT` (window review)
- **P1 block consumption:** proven — the I-F9 mandates prove block reads:
  the 4096-byte cap, the exact key-set + `expectedSelectionRevision`
  safe-integer ≥ 1 + `clientRequestId` matching
  `CLIENT_REQUEST_ID_PATTERN` structural validation with the verbatim
  400 `KEYWORD_RUN_INPUT_INVALID` "The research handoff payload is
  invalid." message, the same param guard (400 `INVALID_RESEARCH_ID`
  "The research ID is invalid."), the verbatim body-string forwarding
  rule, the POST method, the `encodeURIComponent(researchId)/runs`
  path, and `timeoutMs: 15_000` are §3.3/I-F9 + §5.20 contract text.
  Quote form not relayed; waiver recorded.
- **Leaf handoff summary:** CREATE, 77 lines, commit `e13ba00` "S020"
  (full `e13ba00c4a749555a29721e928df0d85e5d34905`; parent `a6d4c52`
  = S019); single-file diff (+77, plus directory); tree clean after;
  ending digest
  `270c0e64ea6f7f410f75fd6349f3ac2b27cc88ddaaea0c4418d288b3483f54c5`.
- **Contract verification (I-F9):** exports `POST` only; `runtime =
  "nodejs"` + `dynamic = "force-dynamic"`; signature
  `POST(_request: Request, context: RouteContext<"/api/keyword-research/[researchId]/runs">)`;
  guard order exactly: Content-Type prefix (415) → body ≤
  `MAX_BODY_BYTES = 4096` (413) → `JSON.parse` (400 `INVALID_JSON`)
  → structural validation: object-not-array/null, `keys.length !== 2`,
  `Number.isSafeInteger(record.expectedSelectionRevision)` with
  `>= 1`, `typeof record.clientRequestId === "string"` and
  `CLIENT_REQUEST_ID_PATTERN.test(...)` else 400
  `KEYWORD_RUN_INPUT_INVALID` verbatim message (wrong key names
  necessarily fail the type checks — exact key-set enforced) →
  `authenticatedRoute()` 401 passthrough → awaited params →
  `validKeywordResearchId` guard else 400 `INVALID_RESEARCH_ID`
  verbatim message → `proxyBackend({ path, method: "POST", body,
  timeoutMs: 15_000, userId })` forwarding the original body string
  verbatim. Import cross-checked: `CLIENT_REQUEST_ID_PATTERN`
  exported at `lib/keyword-intelligence-validation.ts:30`
  (`/^[A-Za-z0-9_-]{16,80}$/u`).
- **Checks (independently re-run):** C1 write-set = the one file
  (commit `e13ba00`, +77); C2 `npx tsc --noEmit` → **0** after a
  standing-baseline typegen refresh (new route literal
  `/api/keyword-research/[researchId]/runs`; gitignored `.next/`
  writes only, git tree clean before/after); C3 `npm run lint` →
  0 errors (1 pre-existing traffic-globe.tsx warning); C4 `npm test`
  → 90/90 pass, 0 fail; C5
  `grep -c "CLIENT_REQUEST_ID_PATTERN"` → `2` (≥ 1).
- **Ending digest:** `270c0e64ea6f7f410f75fd6349f3ac2b27cc88ddaaea0c4418d288b3483f54c5`.
- **Accepted deviations:** none.
- **Coverage accounting:** zero local case IDs at this leaf
  (`W5-R03` duplicate-click idempotence executes in S027 per the
  frozen allocation); no skips.
- **External mutations:** none (typegen writes gitignored build output
  only, under the standing `EV-KI-W5-S24` baseline).
- **Limitations/deferred:** route behavior (guard ordering, verbatim
  forwarding, idempotence) verified at the S024–S027 test leaves;
  `KI-W5-I001` re-verifies C2 with freshly built types.
- **Disposition:** `KI-W5-S020` ACCEPTED. Next assignable: `KI-W5-S021`
  (export CSV route).

---

## `EV-KI-W5-S27` — Window review of `KI-W5-S021` (export CSV route)

- **Timestamp:** 2026-08-20T00:25:00+05:30
- **Parent window / assignment / sub-window:** `KI-W5` / `ASG-KI-W5-WA-02` / `KI-W5-S021`
- **Actor/role:** `KI-W5-WINDOW-AGENT` (window review)
- **P1 block consumption:** proven — the I-F10 mandates prove block reads:
  the no-`proxyBackend` rule (route-local fetch because
  `backend-proxy.ts:74-84` JSON-parses every response and would
  corrupt CSV), the env-validation parity with `backend-proxy.ts:28-38`
  (empty/trailing-slash/non-http(s)/unparseable → null) else 500
  `FRONTEND_CONFIGURATION_ERROR`, the `Accept: text/csv,application/json`
  header, conditional `Authorization: Bearer ${BACKEND_API_TOKEN}`,
  `X-User-Id`, `AbortController` 30_000 → 504 `BACKEND_TIMEOUT`,
  network failure → 502 `BACKEND_UNAVAILABLE`, the full DEC-KI-019
  query allowlist table, the verbatim 400
  `INVALID_QUERY_PARAMETERS` "One or more export query parameters are
  invalid." message, and the 2xx CSV passthrough / non-2xx
  JSON re-emit with `no-store` are §3.3/I-F10 + §5.21 + ledger
  lines 420-427 contract text. Quote form not relayed; waiver
  recorded.
- **Leaf handoff summary:** CREATE, 217 lines, commit `cad36c4` "S021"
  (full `cad36c4b9282e3fe763e4201ef9647ac84247527`; parent `e13ba00`
  = S020); single-file diff (+217, plus directory); tree clean after;
  ending digest
  `fde0b5c48c626afa82410404ea7b1dafdd03e24fead4a893b806ea0a331d1e07`.
- **Contract verification (I-F10):** exports `GET` only;
  `runtime = "nodejs"` + `dynamic = "force-dynamic"`; signature with
  exact `RouteContext<"/api/keyword-research/[researchId]/export.csv">`
  literal; order: param guard (400 `INVALID_RESEARCH_ID` verbatim) →
  query validation → `authenticatedRoute()` 401 passthrough → env
  check → fetch. `exportBackendBaseUrl()` is a semantic copy of
  `backendBaseUrl()` (`backend-proxy.ts:28-38`): rejects empty,
  trailing `/`, non-`http(s)` protocol, unparseable URL. Query
  validation: unknown keys rejected; single-value keys
  (`market|seed|clusterId|intent|lane|category|audience|channel|
  minVolume|minOpportunity|recommended|search`) at most once;
  `flag` repeatable ≤ 20 (`MAX_FLAG_COUNT = 20`); `market` ∈
  {all,US,GB,CA,AU,NZ,DE,FR,IN,AE}; `lane` ∈ the exact four-lane
  `KeywordLane` union (types.ts:39-43 — verified byte-equal);
  `minVolume` `/^\d+$/` ≤ 2147483647; `minOpportunity` `/^\d+$/`
  ≤ 100; `recommended` ∈ {true,false}; violations → 400
  `INVALID_QUERY_PARAMETERS` verbatim message. Fetch headers:
  `Accept: text/csv,application/json`, conditional `Authorization:
  Bearer ${BACKEND_API_TOKEN}`, `X-User-Id: auth.userId`; timeout
  30_000 → 504 `BACKEND_TIMEOUT`; network failure → 502
  `BACKEND_UNAVAILABLE`; both messages match the established
  proxy vocabulary. Success path: single `response.text()` read,
  `new Response(responseText, { status: 200, headers:
  { "Content-Type": backend value ?? "text/csv; charset=utf-8",
  "Cache-Control": "no-store", "Content-Disposition": backend value
  when present } })` — CSV content never parsed, no logging, no
  added query keys, no buffering beyond the single text read
  (all §5.21 forbidden items honored). Non-2xx: `JSON.parse` attempt
  → `Response.json(payload, { status: <backend status>, headers:
  { "Cache-Control": "no-store" } })`; unparsable → 502
  `BACKEND_INVALID_RESPONSE`. Message parity verified:
  `FRONTEND_CONFIGURATION_ERROR` → "The frontend is not connected to
  the lead service." (`backend-proxy.ts:51-52` byte-identical).
- **Checks (independently re-run):** C1 write-set = the one file
  (commit `cad36c4`, +217); C2 `npx tsc --noEmit` → **0** after a
  standing-baseline typegen refresh (new route literal `export.csv`;
  gitignored `.next/` writes only, git tree clean before/after); C3
  `npm run lint` → 0 errors (1 pre-existing traffic-globe.tsx
  warning); C4 `npm test` → 90/90 pass, 0 fail; C5
  `grep -c "proxyBackend"` → **0** (exactly as required) and
  `grep -c "text/csv"` → `2` (≥ 1).
- **Ending digest:** `fde0b5c48c626afa82410404ea7b1dafdd03e24fead4a893b806ea0a331d1e07`.
- **Accepted deviations:** one, stricter-than-contract only. I-F10
  lists `seed` "≤ 100", `search` "≤ 160", and bare `clusterId`
  without nonempty constraints (contrast the explicit "nonempty" on
  `intent|category|audience|channel|flag`). The leaf enforces
  nonempty for `seed` (code-point ≤ 100), `search` (≤ 160), and
  `clusterId` (≥ 1), so empty-value requests receive 400 rather than
  being forwarded. Accepted because: degenerate-input class only;
  the ledger's "normalized string" semantics make empty filters
  meaningless; the delta only rejects (never accepts more than
  contract); no privacy/cost/atomicity impact. Residual risk: if the
  backend later defines empty `seed`/`search`/`clusterId` as valid
  filters, a corrective window is required.
- **Coverage accounting:** zero local case IDs at this leaf (`W5-B05`,
  `W5-NC08/NC11`, `W5-R07` execute in S024–S027 per the frozen
  allocation); no skips.
- **External mutations:** none (typegen writes gitignored build output
  only, under the standing `EV-KI-W5-S24` baseline).
- **Limitations/deferred:** route behavior (query allowlist edges,
  CSV passthrough, error envelopes) verified at the S024–S027 test
  leaves; `KI-W5-I001` re-verifies C2 with freshly built types.
- **Disposition:** `KI-W5-S021` ACCEPTED. Next assignable: `KI-W5-S022`
  (keywords landing page).

---

## `EV-KI-W5-S28` — Window review of `KI-W5-S022` (keywords landing page)

- **Timestamp:** 2026-08-20T00:55:00+05:30
- **Parent window / assignment / sub-window:** `KI-W5` / `ASG-KI-W5-WA-02` / `KI-W5-S022`
- **Actor/role:** `KI-W5-WINDOW-AGENT` (window review)
- **P1 block consumption:** proven — the I-F11 mandates prove block reads:
  the exact `metadata` object `{ title: "Keyword research" }`,
  `force-dynamic`, the `app/runs/page.tsx` shell pattern
  (`main.app-canvas` + `div.shell` + eyebrow/title/lede header row),
  `<ResearchForm />` rendered without `onCreated` (I-F14 built-in
  navigation), and the explicit no-server-side-session-redirect rule
  are §3.4/I-F11 + §5.22 contract text; the markup mirrors
  `app/runs/page.tsx:10-18` class-for-class (`app-canvas
  history-page`, `shell`, `run-title-row app-page-header`, `eyebrow`,
  `h1`, lede `p`). Quote form not relayed; waiver recorded.
- **Leaf handoff summary:** CREATE, 23 lines, commit `32f6aaf` "S022"
  (full `32f6aaf214b462cb9234d4547f5e2f8dacfbef09`; parent `cad36c4`
  = S021); single-file diff (+23); tree clean after; ending digest
  `07a826646454bb2612b992d2e2d5f77a302e3272ce11d5ee21e3bd950e3de1fd`.
- **Contract verification (I-F11):** server component (no
  `"use client"`); `import type { Metadata }` + `export const
  metadata: Metadata = { title: "Keyword research" }` byte-exact;
  `export const dynamic = "force-dynamic"`; shell markup mirrors the
  runs reference exactly — `main.app-canvas history-page`, `div.shell`,
  `div.run-title-row.app-page-header`, eyebrow "Keyword research",
  `h1` "Keyword research", lede sentence; `<ResearchForm />` with no
  props (no `onCreated` — the S008 component's built-in default
  navigates to `/keywords/${view.id}` per I-F14); no session redirect
  in the server component (client handles 401 with sign-in CTA).
- **Checks (independently re-run):** C1 write-set = the one file
  (commit `32f6aaf`, +23); C2 `npx tsc --noEmit` → **0** after a
  standing-baseline typegen refresh (new `/keywords` page literal;
  gitignored `.next/` writes only, tree clean before/after); C3
  `npm run lint` → 0 errors (1 pre-existing traffic-globe.tsx
  warning); C4 `npm test` → 90/90 pass, 0 fail; C5
  `grep -c "force-dynamic"` → `1` (exact) and
  `grep -c "use client"` → `0` (no match, exit 1).
- **Ending digest:** `07a826646454bb2612b992d2e2d5f77a302e3272ce11d5ee21e3bd950e3de1fd`.
- **Accepted deviations:** none. (The runs page's `New discovery`
  header link is intentionally absent — the frozen pattern mandates
  the eyebrow/title/lede row, and I-F11 names no header action.)
- **Coverage accounting:** zero local case IDs at this leaf (`W5-B01`
  executes in S027 per the frozen allocation); no skips.
- **External mutations:** none (typegen writes gitignored build output
  only, under the standing `EV-KI-W5-S24` baseline).
- **Limitations/deferred:** page rendering and 401 client CTA verified
  at the S027 browser leaf; `KI-W5-I001` re-verifies with a real
  build.
- **Disposition:** `KI-W5-S022` ACCEPTED. Next assignable:
  `KI-W5-S023` (research dashboard page).

---

## `EV-KI-W5-S29` — Window review of `KI-W5-S023` (research dashboard page)

- **Timestamp:** 2026-08-20T01:25:00+05:30
- **Parent window / assignment / sub-window:** `KI-W5` / `ASG-KI-W5-WA-02` / `KI-W5-S023`
- **Actor/role:** `KI-W5-WINDOW-AGENT` (window review)
- **P1 block consumption:** proven — the I-F11 mandates prove block reads:
  the exact `metadata` object `{ title: "Keyword research dashboard" }`,
  `force-dynamic`, the `PageProps<"/keywords/[researchId]">` typing per
  the installed file-conventions docs, `const { researchId } = await
  params;`, the standard shell with
  `<ResearchDashboard researchId={researchId} />`, and the explicit
  no-ID-pattern-validation rule (client surfaces API 400/404) are
  §3.4/I-F11 + §5.23 contract text. Quote form not relayed; waiver
  recorded.
- **Leaf handoff summary:** CREATE, 27 lines, commit `71ca03c` "S023"
  (full `71ca03c893015d22634a775af1cf0eec33de80e6`; parent `32f6aaf`
  = S022); single-file diff (+27, plus directory); tree clean after;
  ending digest
  `a82eb39ce9373d91410d301e11bdcc4ead8ce9e948601ee7d167ba3e74fbb58a`.
- **Contract verification (I-F11):** async server component (no
  `"use client"`); signature
  `({ params }: PageProps<"/keywords/[researchId]">)`; `export const
  metadata: Metadata = { title: "Keyword research dashboard" }`
  byte-exact; `export const dynamic = "force-dynamic"`; awaited
  params destructure; standard shell markup mirrors the runs
  reference (`app-canvas history-page`, `shell`,
  `run-title-row app-page-header`, eyebrow, `h1`, lede);
  `<ResearchDashboard researchId={researchId} />` as the only body;
  no ID-pattern validation in the page (the S016 client surfaces the
  API 400/404 safely).
- **Checks (independently re-run):** C1 write-set = the one file
  (commit `71ca03c`, +27); C2 `npx tsc --noEmit` → **0** after a
  standing-baseline typegen refresh (new `/keywords/[researchId]`
  page literal; gitignored `.next/` writes only, tree clean
  before/after); C3 `npm run lint` → 0 errors (1 pre-existing
  traffic-globe.tsx warning); C4 `npm test` → 90/90 pass, 0 fail; C5
  `grep -c "await params"` → `1` (exact).
- **Ending digest:** `a82eb39ce9373d91410d301e11bdcc4ead8ce9e948601ee7d167ba3e74fbb58a`.
- **Accepted deviations:** none.
- **Coverage accounting:** zero local case IDs at this leaf (all B/R
  cases execute in S024–S027 per the frozen allocation); no skips.
- **External mutations:** none (typegen writes gitignored build output
  only, under the standing `EV-KI-W5-S24` baseline).
- **Limitations/deferred:** page rendering verified at the S027
  browser leaf; `KI-W5-I001` re-verifies with a real build.
- **Disposition:** `KI-W5-S023` ACCEPTED. All page leaves complete.
  Next assignable: `KI-W5-S024` (API/parser test file).

---

## `EV-KI-W5-S30` — Window review of `KI-W5-S024` (API/parser test file)

- **Timestamp:** 2026-08-20T01:55:00+05:30
- **Parent window / assignment / sub-window:** `KI-W5` / `ASG-KI-W5-WA-02` / `KI-W5-S024`
- **Actor/role:** `KI-W5-WINDOW-AGENT` (window review)
- **P1 block consumption:** proven — the §5.24 transformation mandates
  prove block reads: `node:test` + `node:assert/strict` with relative
  `.ts` imports; ten named subtests whose titles match the §6.1
  W5-A definitions verbatim; the three §6.2 controls
  (`W5-NC01`→A05/A06 parser-bypass, `W5-NC07`→A02 six-seed,
  `W5-NC12` A06-half unknown-key weakening) embedded as
  defective-copy→throws→fresh-passes mutation assertions; the local
  literal fixture builder (nine-market code set, ≥1 keyword/cluster
  rows, 15-point histories, one conflict fixture); and exactly one
  `KI_W5_EXECUTION_CERTIFICATE=` TAP diagnostic per I-F18 with
  §3.1 set digests. Quote form not relayed; waiver recorded.
- **Leaf handoff summary:** CREATE, 632 lines, commit `1c8062f` "S024"
  (full `1c8062f0db6aa3247bb93df6db7dd1b54911caba`; parent `71ca03c`
  = S023); single-file diff (+632); tree clean after; ending digest
  `a2f40c62bdf6d34136c2d6a318c8aef24e426581182a2d5edf0ef6fc950cd5c5`.
- **Contract verification (§6.1 W5-A01–A10):** A01 accept boundaries
  (1, 5, 100 cp, full-width-space normalization); A02 all eight
  reject classes (0/6/non-array/unknown-key/non-string/empty/>
  100cp/duplicate-after-normalization); A03 32-hex format + pattern +
  uniqueness + pattern rejects; A04 `kr_`+24 accept and five reject
  classes; A05 envelope deep-equal + wrapper unknown-key throw;
  A06 all enumerated strictness dimensions — unknown key, stage
  enum, StageCounts bounds (negative expected), state/result
  pairing (running with result), result-null rule, selection
  bounds (201) and enums (sourceKind), conflict shapes (itemIds
  order, pair order, reason enum, similarity bound), date format,
  markets (empty/duplicate/bad code), monthlyHistory 15..102
  (14 and 103 rejected, month 13, negative volume); A07 run-handoff
  deep-equal + bad run state + wrapper unknown-key; A08 poll ladder
  2000→3000→4500→6750→10000 with 10000 ceiling + terminal stops;
  A09 toggle add/remove identity, append order, edit with lane/
  facet reclassification deep-equal, manual add (sourceKind
  "manual", metricsSnapshot null), 200 cap returning the identical
  array reference (strictEqual), over-100 flag (100 false, 101
  true), finalize guards (not_completed/empty/over_limit); A10
  conflict gate blocks finalize, clean view passes, canonical
  conflict shape deep-equal. Certificate emitted inside A10 after
  digest-equality asserts (lines 629-631).
- **Certificate verification (I-F18/§3.1):** TAP output contains
  exactly one `KI_W5_EXECUTION_CERTIFICATE=` line; compact JSON key
  order matches I-F18 byte-for-byte (file/required/registered/
  executed/skipped/oracleFailures/three digests); required =
  registered = executed = the ten W5-A IDs; skipped and
  oracleFailures empty; `requiredDigest == registeredDigest ==
  executedDigest` asserted in-test and true in output; the window
  agent independently recomputed the §3.1 set digest (sorted
  UTF-8 byte order, member+LF, sha256) over the ten IDs and it
  matches the certificate value.
- **Checks (independently re-run):** C1 write-set = the one file
  (commit `1c8062f`, +632); C2 `npx tsc --noEmit` → **0**; C3
  `npm run lint` → 0 errors (1 pre-existing traffic-globe.tsx
  warning); C4 `npm test` → **100/100 pass, 0 fail, 0 skipped**
  (baseline grew 90 → 100 exactly by the ten new subtests); C5
  `node --experimental-strip-types --test --test-reporter=tap
  test/keyword-intelligence-api.test.ts` → `# tests 10`,
  `# pass 10`, `# fail 0`, `# skipped 0`, certificate line count
  exactly 1 with equal digests.
- **Ending digest:** `a2f40c62bdf6d34136c2d6a318c8aef24e426581182a2d5edf0ef6fc950cd5c5`.
- **Accepted deviations:** none. (Interpretation note: A09's "CAS
  guard" is exercised as the `canFinalizeSelection` state/
  emptiness/limit preconditions — the view-model half of the CAS
  save; the 409 wire behavior is exercised in S027 per allocation.)
- **Coverage accounting:** ten local case IDs registered = executed
  (`W5-A01`–`W5-A10`); three controls executed (`W5-NC01`,
  `W5-NC07`, `W5-NC12` A06-half; the NC12 I02-half executes in its
  allocated file per §6.2); zero skips.
- **External mutations:** none.
- **Limitations/deferred:** wire-level route/proxy behavior remains
  with S026/S027; `KI-W5-V2` frozen re-run belongs to `KI-W5-I001`.
- **Disposition:** `KI-W5-S024` ACCEPTED. Next assignable:
  `KI-W5-S025` (components/view-model test file).

---

## `EV-KI-W5-S31` — Window review of `KI-W5-S025` (components/view-model test file)

- **Timestamp:** 2026-08-20T02:25:00+05:30
- **Parent window / assignment / sub-window:** `KI-W5` / `ASG-KI-W5-WA-02` / `KI-W5-S025`
- **Actor/role:** `KI-W5-WINDOW-AGENT` (window review)
- **P1 block consumption:** proven — the §5.25 transformation mandates
  prove block reads: twelve named subtests whose titles match §6.1
  W5-C verbatim; literal expected values on a fixed multi-market/
  multi-lane/multi-flag fixture (four lanes, US/GB market metrics,
  four flags, six rows) in the S024 builder style; the 200-row scale
  case with 200 distinct rows plus a 200-item draft; the two named
  controls (per-market-selection mutation; stale-overwrite mutation);
  and one `KI_W5_EXECUTION_CERTIFICATE=` line per I-F18 over the
  twelve IDs. Quote form not relayed; waiver recorded.
- **Leaf handoff summary:** CREATE, 915 lines, commit `cfde28c` "S25"
  (full `cfde28c1cbd6fd8de2766430a2f5207fd6ba772c`; parent `1c8062f`
  = S024; commit subject "S25" abbreviates the established "S0NN"
  pattern — cosmetic registry observation, not a file deviation);
  single-file diff (+915); tree clean after; ending digest
  `6e14ecc8eed297a6ca608ec365799b6cb2da2914d231944cb6be3047e24fe168`.
- **Contract verification (§6.1 W5-C01–C12):** C01 activeRows (merged
  excluded) + distinctKeywordRows (case-insensitive dedupe keeping
  higher volume, merged rows ineligible); C02 `projectMarketRow`
  all-identity (strictEqual) + US/GB projected literals + absent
  market `_marketMissing` null-out + the selection invariant oracle
  (projected IDs superset of draft IDs across market switch); C03
  cumulativeVolume (21400 literal; merged dup excluded; projected
  null excluded); C04 currentSummary/currentClusterMetric identity;
  C05 every filter dimension individually (search case-insensitive,
  seed, clusterId, intent, lane, category, audience, channel,
  minVolume, minOpportunity, recommended true/false, single+multi
  flag, market) plus three combined cases plus empty result plus
  projected-value assertion plus `filterOptionSources` sorted
  literals; C06 all fifteen sort columns both directions + null-last
  in both directions + pagination clamp (page 4→3, page 0→1, empty,
  size 0→1, fractional size→floor); C07 aggregateByCluster literal
  sums, adjustedVolume (distinct-only, 400 literal), median (odd/
  even/empty/single), metricFingerprint join, discoveryLane for all
  four lanes, laneLabel display literals; C08 empty-filter empty
  query, full-mirror query string with ordered repeated `flag`
  params, 20-flag cap, `EXPORT_CSV_COLUMNS` 23-column literal parity
  lock; C09 formatter literals (K/M/B, $cpc 2dp, pct rounding, signed
  slope, "—" NaN); C10 theme key `ki-dashboard-theme` + toggle
  round-trip; C11 phase machine (loading/error priority/ready/empty
  all-merged); C12 200-row/200-draft scale (200 active+distinct,
  199000 volume, filter counts, sort ends, 10×20 aggregation, page
  ceilings 25/200 with clamp, 200-draft over-limit, finalize gates,
  capped toggle/manual identity strictEqual, remove→199).
- **Controls verification (§6.2):** `W5-NC02` per-market selection
  reintroduction mutant (`itemId: ${m}:${id}`) throws the invariant
  oracle, fresh passes; `W5-NC08` uncapped-flag mutant throws the
  cap oracle, fresh passes; `W5-NC09` C02-half stale-overwrite
  `lastWriteWins` mutant throws the stale-guard oracle,
  guarded-apply passes (the R03-half executes in S027 per §6.2
  allocation). All follow unchanged-passes → defect-throws →
  fresh-passes.
- **Certificate verification (I-F18/§3.1):** exactly one
  `KI_W5_EXECUTION_CERTIFICATE=` TAP line; JSON key order matches
  I-F18; twelve `W5-C` IDs; skipped/oracleFailures empty;
  `requiredDigest == registeredDigest == executedDigest` asserted
  in-test and true; the window agent independently recomputed the
  §3.1 set digest over the twelve IDs and it matches.
- **Checks (independently re-run):** C1 write-set = the one file
  (commit `cfde28c`, +915); C2 `npx tsc --noEmit` → **0**; C3
  `npm run lint` → 0 errors (1 pre-existing traffic-globe.tsx
  warning); C4 `npm test` → **112/112 pass, 0 fail, 0 skipped**
  (grew exactly by the twelve new subtests); C5
  `node --experimental-strip-types --test --test-reporter=tap
  test/keyword-intelligence-components.test.ts` → 12/12 pass,
  0 skipped, certificate count 1 with equal digests.
- **Ending digest:** `6e14ecc8eed297a6ca608ec365799b6cb2da2914d231944cb6be3047e24fe168`.
- **Accepted deviations:** none.
- **Coverage accounting:** twelve local case IDs registered =
  executed (`W5-C01`–`W5-C12`); three controls executed (`W5-NC02`,
  `W5-NC08`, `W5-NC09` C02-half); zero skips.
- **External mutations:** none.
- **Limitations/deferred:** the React render surface itself is
  verified in S027 real Chrome (test-substitute fidelity recorded
  for parent review per the §5.25 mechanical trace); `KI-W5-V2`
  frozen re-run belongs to `KI-W5-I001`.
- **Disposition:** `KI-W5-S025` ACCEPTED. Next assignable:
  `KI-W5-S026` (inventory test file).

---

## `EV-KI-W5-S32` — Correction `KI-W5-C002` (S008 defect: missing surface registration)

- **Timestamp:** 2026-08-20T03:10:00+05:30
- **Parent window / assignment:** `KI-W5` / `ASG-KI-W5-WA-02`
- **Actor/role:** `KI-W5-WINDOW-AGENT` (correction executed by the window agent under explicit requester authorization, per the `KI-W5-C001` precedent)
- **Defect:** the S008 output
  `frontend/components/keyword-intelligence/research-form.tsx`
  (accepted in `EV-KI-W5-S09`, then-digest `9583f663…`) lacked the
  `data-surface="surface:research-form"` registration mandated by
  §3.7 ("each composed surface carries `data-surface=\"<inventory
  id>\"`") and I-F15 (21-entry inventory). Surfaced by the S026 leaf's
  frozen W5-I05 registration check: 5/6 pass, `W5-I05` failed with
  actual missing `surface:research-form` (the other 20 ids were
  registered). Root cause: the §5.8 block did not restate the
  registration rule and its C5 only counted `"use client"`, so both
  the leaf and the S008 window review missed it — a cross-leaf
  consistency miss that the inventory negative-control design exists
  to catch (mechanical trace §5.26: SCN-KI-016 negative control).
- **Fix (spec-determined, minimal):** one line added at
  `research-form.tsx:116` — `data-surface="surface:research-form"` on
  the root `<form id="seed-phrase-form">` element, mirroring the
  registration pattern of the other eight surfaces. No other line
  changed; the S026 test file was NOT modified to accommodate.
- **Verification after fix:** `npx tsc --noEmit` → 0; `npm run lint`
  → 0 errors (1 pre-existing traffic-globe.tsx warning);
  `npm test` → **118/118 pass, 0 skipped** (was 117/118 with the
  W5-I05 failure); single-file S026 TAP run → **6/6 pass**, one
  certificate line, digests equal. Ending digests:
  `research-form.tsx`
  `b66c6f976aa428d2a17416233c322a2c0be09e046ee2cf5116d05533acdbf948`
  (corrected from `9583f663…`);
  `keyword-intelligence-inventory.test.ts` unchanged
  `67828152b71f9b05ec847d5fc0d3be238452d526aeffee8255e17b39a644f480`.
- **Commit:** requester committed the correction together with the
  S026 leaf output as `0aa5ff9` "S25-fix" (full
  `0aa5ff96799af7319108f3e1ef829e0a540be285`, parent `cfde28c`);
  stat: research-form.tsx +1, inventory test +507; tree clean after.
- **Disposition:** `KI-W5-C002` CLOSED. The S008 registry entry is
  superseded by ending digest `b66c6f97…` at commit `0aa5ff9`.

---

## `EV-KI-W5-S33` — Window review of `KI-W5-S026` (inventory test file)

- **Timestamp:** 2026-08-20T03:10:00+05:30
- **Parent window / assignment / sub-window:** `KI-W5` / `ASG-KI-W5-WA-02` / `KI-W5-S026`
- **Actor/role:** `KI-W5-WINDOW-AGENT` (window review)
- **P1 block consumption:** proven — the §5.26 transformation mandates
  prove block reads: exact export-surface equality via
  `Object.keys(await import(...)).sort()` deep-equal for the three lib
  modules; recursive file-listing equality for the exact owned paths
  under `app/keywords/`, `app/api/keyword-research/`, and
  `components/keyword-intelligence/` (17 files, no extra);
  `KEYWORD_INTELLIGENCE_SURFACE_INVENTORY` deep-equal the 21-entry
  I-F15 literal; `data-surface`/`data-filter` registration greps
  covering every inventory id (9 surfaces + 11 charts + 1 landscape)
  and the 14 filter fields including `reset`; chart dependency
  assertions reading `node_modules/*/package.json` (chart.js
  `"3.9.1"`, chartjs-chart-treemap `"2.0.0"`); the no-CDN grep
  (`https?://`, `cdn.`, `unpkg`, `jsdelivr`, `cdnjs`, `loadScript`,
  `SCRIPT_CANDIDATES`, `loadFirst`) over all 20 owned sources. Quote
  form not relayed; waiver recorded.
- **Leaf handoff summary:** CREATE, 507 lines, committed with the
  C002 correction in `0aa5ff9` (see `EV-KI-W5-S32`); single-file
  diff (+507); tree clean after; ending digest
  `67828152b71f9b05ec847d5fc0d3be238452d526aeffee8255e17b39a644f480`.
- **Contract verification (§6.1 W5-I01–I06):** I01 types module
  export surface = `[]` (type-only module — correct); I02 validation
  module = the exact 8 runtime exports; I03 view-model module = the
  exact 37 runtime exports; I04 owned-path set equality with the
  17-file literal (recursive walk, byte-order sort); I05 inventory
  deep-equal + registration grep equality (21/21 after C002) +
  filter-field grep equality (14/14) + the remove-one negative
  control loop over all 21 entries; I06 installed-version equality
  (chart.js 3.9.1, chartjs-chart-treemap 2.0.0, read from
  `node_modules/*/package.json`) + no-CDN grep over all owned
  sources.
- **Controls verification (§6.2):** `W5-NC03` remove-one-registration
  loop (each of 21 removals throws); `W5-NC04` CDN-string injection
  throws; `W5-NC06` wrong-version literals (3.9.0 / 2.0.1) throw;
  `W5-NC10` extra-path injection throws; `W5-NC12` I02-half
  weakened-envelope mutant parses (proving the strict parser is the
  guard) while the strict oracle throws. All follow
  unchanged-passes → defect-throws → fresh-passes.
- **Certificate verification (I-F18/§3.1):** exactly one
  `KI_W5_EXECUTION_CERTIFICATE=` TAP line; JSON key order matches
  I-F18; six `W5-I` IDs; skipped/oracleFailures empty; digests equal
  asserted in-test and true; window agent independently recomputed
  the §3.1 set digest over the six IDs — matches.
- **Checks (independently re-run, after C002):** C1 write-set = the
  one test file (in commit `0aa5ff9`, +507; the sibling +1 line is
  the separately recorded C002 correction); C2 `npx tsc --noEmit` →
  **0**; C3 `npm run lint` → 0 errors (1 pre-existing warning); C4
  `npm test` → **118/118 pass, 0 fail, 0 skipped** (grew exactly by
  the six new subtests); C5 single-file TAP run → 6/6 pass, 0
  skipped, certificate count 1 with equal digests.
- **Ending digest:** `67828152b71f9b05ec847d5fc0d3be238452d526aeffee8255e17b39a644f480`.
- **Accepted deviations:** none.
- **Coverage accounting:** six local case IDs registered = executed
  (`W5-I01`–`W5-I06`); five controls executed (`W5-NC03/NC04/NC06/
  NC10/NC12` I02-half); zero skips.
- **External mutations:** none.
- **Limitations/deferred:** `KI-W5-V2` frozen re-run belongs to
  `KI-W5-I001`; the browser registrations are DOM-verified in S027.
- **Disposition:** `KI-W5-S026` ACCEPTED. Next assignable:
  `KI-W5-S027` (browser CDP harness).

---

## `EV-KI-W5-S34` — Window review of `KI-W5-S027` (browser CDP harness)

- **Timestamp:** 2026-08-20T03:45:00+05:30
- **Parent window / assignment / sub-window:** `KI-W5` / `ASG-KI-W5-WA-02` / `KI-W5-S027`
- **Actor/role:** `KI-W5-WINDOW-AGENT` (window review)
- **P1 block consumption:** proven — the five-phase §5.27 transformation
  is implemented contract-for-contract: Phase A spawns `next build`
  then `next start --hostname 127.0.0.1 --port 4347` with readiness
  wait, build mandatory unless `KI_W5_SKIP_BUILD=1` explicitly set
  (skip mode additionally refuses when `.next` is absent); Phase B
  builds the queued / running×3 (expansion, anchor_screen,
  market_overview) / completed / failed / empty / scale / poll-sequence
  fixtures in-file, each validated through `parseResearchEnvelope` and
  the handoff through `parseRunHandoffEnvelope` before injection;
  Phase C installs `Page.addScriptToEvaluateOnNewDocument` wrapping
  same-origin `/api/keyword-research*` fetches with deterministic
  payloads, recording `{method,url,at,bodyDigest,clientRequestId}`
  into `globalThis.__kiFixture.requests`, poll sequencing by count,
  on-demand 409 selection/handoff conflict modes, non-app URLs passed
  through untouched; Phase D runs the fifteen `W5-B*`/`W5-R*`
  scenarios at 1440×900 and 390×844 (DPR 2 canvas assertions) with
  console/exception collection, the network allowlist
  (app-origin only, zero CDN, asserted lines 1450-1456),
  canvas/`$chartjs` presence (11 charts), landscape transform
  mutation on CDP drag, request-log oracles, unauthenticated direct
  route probes against the real routes, and CSV equality against
  `EXPORT_CSV_COLUMNS` + filtered fixture rows; Phase E tears down in
  `finally` (process-group SIGTERM for Next and Chrome, CDP close,
  temp-dir removal) and emits exactly one
  `KI_W5_BROWSER_CERTIFICATE=` line. The `Cdp` class matches
  `g-r1-real-component-browser.mjs:183-201`. Determinism: fixed port
  4347, fixed seeds, fixed date literals; screenshots under
  `review-evidence/keyword-intelligence/KI-W5/` (gitignored runner
  output; verified absent at leaf level — the harness was NOT
  executed, matching the leaf prohibition and I001 ownership).
  Quote form not relayed; waiver recorded.
- **Leaf handoff summary:** CREATE, 1495 lines, commit `983d3ed`
  "S027" (full `983d3ede3cb7e5abb92992cf576e8abdfa5a4041`; parent
  `0aa5ff9` = S026/C002); single-file diff (+1495, plus the
  `test/browser/` directory); tree clean after; ending digest
  `6a531ca8078c4fce49189f4d1053e59c6affd01fd9c8bfc440c9a47b5126d649`.
- **Scenario-to-§6.1 verification:** B01 surface presence incl. the
  C002-restored `surface:research-form`, "N rows" data-derived meta,
  empty state, 404 error state with retry; B02 seed/search filters,
  reset to 25-row default page, `aria-sort` header state, page-size
  select, pagination advance; B03 exactly-one-PUT-per-save with body
  digests, 409 `KEYWORD_SELECTION_REVISION_CONFLICT` conflict surface,
  over-100 banner + disabled finalize on the 200-draft scale view;
  B04 edit dialog (reclassified text commit + toast) and manual add
  (badge + toast); B05 export anchor `buildExportQuery` mirror +
  intercepted CSV equality + NC11 divergence control; B06 theme
  round-trip with exactly one storage key `ki-dashboard-theme` and
  reload persistence; B07 11 nonzero chart canvases each with a
  `$chartjs` instance, DPR-aware landscape canvas (±4px), drag
  transform mutation via before/after `toDataURL`, cluster
  hit/tooltip/inspector; B08 scale render + filter, zero console
  errors, zero uncaught exceptions, exactly one chart instance set;
  R01 five-GET lifecycle with ladder-gap assertions
  (2000/3000/4500/6750 ±60%), terminal stop (no polls after
  completed), NC05 forced-second-timer defect control + restoration;
  R02 close/remount durable reload with zero POST/PUT mutations;
  R03 stale 409 with no silent local-draft overwrite, fresh reload
  reset, idempotent duplicate finalize (single `/runs` POST with one
  retained `clientRequestId` matching the 16-80 pattern); R04 failed
  state `data-code="KI_WORKER_FAILED"` + GET-only retry; R05 both
  viewports with no horizontal overflow + DPR 2 at 390×844; R06
  chart teardown/recreate on market filter change with 11 canvases
  and no new console errors; R07 unauthenticated probes — 401
  `AUTHENTICATION_REQUIRED` with `Cache-Control: no-store`, 400
  `INVALID_QUERY_PARAMETERS` unknown query key, 400
  `INVALID_RESEARCH_ID` bad id, generic 404 — via Node-side fetches
  against the real routes without interception.
- **Certificate verification (I-F18):** emitted in `finally`
  (available even on failure); schema `file/required/registered/
  executed/skipped/oracleFailures/requiredDigest/registeredDigest/
  executedDigest` plus `scenarios:{"SCN-KI-016":<all B pass>,
  "SCN-KI-017":<all R pass>}` over the fifteen `W5-B/R` IDs; digests
  via the §3.1 set-digest algorithm (sort + member+LF + sha256,
  byte-order comparator); `oracleFailures` carries any failed IDs and
  the script then throws (honest reporting).
- **Checks (independently re-run):** C1 write-set = the one file
  (commit `983d3ed`, +1495); C2 `npx tsc --noEmit` → **0** (the
  `.mjs` is outside tsconfig scope); C3 `npm run lint` → 0 errors (1
  pre-existing traffic-globe.tsx warning); C4 `npm test` →
  **118/118 pass, 0 skipped** (glob `test/*.test.ts` does not pick
  up `test/browser/*.mjs` — verified); C5 `node --check
  test/browser/keyword-intelligence-dashboard.mjs` → exit 0.
- **Ending digest:** `6a531ca8078c4fce49189f4d1053e59c6affd01fd9c8bfc440c9a47b5126d649`.
- **Accepted deviations/interpretations:** two, both recorded by the
  leaf. (1) The frozen line "the script refuses to run when
  `KI_W5_SKIP_BUILD` is unset" is implemented as "refuses to run in
  skip-build mode unless the var is explicitly set" — the only parse
  consistent with V1 "the script performs the build itself"; the
  interpretation is documented in the file header (lines 5-12).
  (2) NC11 executes as an explicit divergence-detection assertion
  (diverged header fails the equality/header oracle) rather than
  `assert.throws` — oracle semantics preserved.
- **Coverage accounting:** fifteen B/R IDs registered in the
  certificate (`W5-B01`–`B08`, `W5-R01`–`R07`); browser controls
  `W5-NC05` (R01) and `W5-NC11` (B05) embedded with restoration; the
  NC09 R03-half is the no-silent-overwrite browser assertion;
  execution deferred to `KI-W5-I001` per the frozen allocation.
- **External mutations:** none (harness not executed; no
  build/dev/start at leaf level).
- **Limitations/deferred:** actual execution — build, server, Chrome,
  screenshots, certificate values, and gates V1–V4 — belongs to
  `KI-W5-I001`.
- **Disposition:** `KI-W5-S027` ACCEPTED. All 27 file leaves are
  complete. Next: `KI-W5-I001` (whole-window integration assessment,
  window-agent owned).

---

## `EV-KI-W5-S35` — Correction `KI-W5-C003` (S027 harness defects exposed by V1)

- **Timestamp:** 2026-08-20T04:35:00+05:30
- **Parent window / assignment:** `KI-W5` / `ASG-KI-W5-WA-02`
- **Actor/role:** `KI-W5-WINDOW-AGENT` (correction executed by the window agent under explicit requester authorization, per the `KI-W5-C001`/`C002` precedent; owning file `frontend/test/browser/keyword-intelligence-dashboard.mjs` from the 27-file set)
- **Defects (all harness-side; zero product defects found):**
  1. **Template-escape defect (line 662):** `url.search.replace(/^\?/, "")`
     inside the `fixtureInjection` template literal emitted the invalid
     regex `/^?/` into the page (`SyntaxError: Nothing to repeat` at
     parse time), so the fetch wrapper never installed → real 401s →
     14/15 scenarios failed on the first V1 execution. Fix: `\?` → `\\?`.
  2. **W5-B06 readiness signal:** waited for
     `surface:research-dashboard`, which exists in loading/auth layouts
     too; the theme button renders only in ready. Fix: wait for the
     keyword-table surface (ready layout).
  3. **W5-B06 initial-theme assumption:** assumed `light`, but the
     dashboard falls back to `prefers-color-scheme` and headless Chrome
     prefers dark. Fix: drive the round-trip from the OBSERVED theme
     (flip → persist → flip back); assertions unchanged in strength.
  4. **W5-B07 drag:** CDP mouse coordinates are viewport-relative; the
     landscape canvas sat below the fold and `scrollIntoView` was
     defeated by an `overflow: hidden` ancestor. Fix: instant
     `window.scrollTo`, viewport-bounds pre-assertion, plus a DOM
     PointerEvent fallback (identical pixel-change assertion).
  5. **W5-R01 premature oracle:** the ladder assertion ran while the
     first (queued) poll was still pending (got 1 GET). Fix: wait for
     the terminal ready layout before the 5-GET oracle (all three
     passes).
  6. **W5-R03 duplicate-click selector:** the in-flight button reads
     "Handing off…" — precisely the idempotence guard under test — so
     the duplicate-click finder threw. Fix: match either label; the
     one-POST/retained-`clientRequestId` assertions unchanged.
  7. **W5-R06 over-assertion:** under the US projection the fixture's
     market metrics all carry `flags: []`, so `buildFlagsConfig`
     legitimately returns `null` and the flags canvas stays
     uninstanced. Fix: assert the data reality — exactly 11 canvases
     (no duplicates/leaks), only `chart:flags` uninstanced, 10
     data-backed charts recreated, zero new console errors.
- **Verification:** intermediate skip-build iteration → 10/15 then
  progressive fixes; final FULL-build official V1 execution
  (`node test/browser/keyword-intelligence-dashboard.mjs`, exit 0):
  15/15 pass, `oracleFailures: []`, both scenario flags true,
  zero console errors, zero uncaught exceptions, zero non-app/CDN
  network. `node --check` exit 0. Ending digest
  `d28cc1b5411d412edeba139f715da69ab5c09a8d67c543be4cc69719ef5e68a7`.
- **Commit:** requester committed as `c85f93b` "Harness escape fit"
  (full `c85f93b4bc66e1c130401227e46b488c6fe13c94`, parent `983d3ed`);
  the commit also includes the 17 gate-evidence runner artifacts under
  `review-evidence/keyword-intelligence/KI-W5/` (14 screenshots +
  browser-checks.json + artifact-index.json + browser-server.log) —
  runner output retained for parent review per the §5.27 determinism
  clause, consistent with the workspace's existing tracked
  `review-evidence/` convention. Tree clean after.
- **Disposition:** `KI-W5-C003` CLOSED. The S027 registry entry is
  superseded by ending digest `d28cc1b5…` at commit `c85f93b`.

---

## `EV-KI-W5-S36` — `KI-W5-I001` whole-window integration assessment (§12.4)

- **Timestamp:** 2026-08-20T04:35:00+05:30
- **Parent window / assignment / sub-window:** `KI-W5` / `ASG-KI-W5-WA-02` / `KI-W5-I001`
- **Actor/role:** `KI-W5-WINDOW-AGENT` (integration assessment owner)

### Gate outcomes (each executed exactly once on frozen final inputs; the pre-C003 V1 failure was corrected within this assessment per §8 before the official executions recorded here)

- **`KI-W5-V1` PASS** — official execution
  `node test/browser/keyword-intelligence-dashboard.mjs` (full
  `next build` performed by the script; exit 0). All 15 B/R IDs pass
  with activation witnesses; browser certificate
  `required = registered = executed` over the 15 IDs with digest
  `0070889385681c847bc41e0c98a190f7e4b2e97c5d4fe57887b114e00da09b74`
  (independently recomputed by the window agent — matches);
  `scenarios: {SCN-KI-016: true, SCN-KI-017: true}`; zero console
  errors; zero uncaught exceptions; zero non-app network requests;
  zero CDN. Fourteen scenario screenshots retained under
  `review-evidence/keyword-intelligence/KI-W5/` (committed by the
  requester in `c85f93b`).
- **`KI-W5-V2` PASS** — `npm run check` (exit 0): eslint 0 errors (1
  pre-existing unrelated traffic-globe.tsx warning), 118/118 tests
  0 skipped, `next build` compiled successfully. Write-set proofs:
  all 27 planned paths are tracked; the per-LF `LC_ALL=C` set digest
  over the 27 `frontend/`-prefixed paths is byte-equal to the frozen
  `a04dce13038a3d180ddab0c8412890af065e3f5ab5019540c87a5664485320e6`;
  the root porcelain change set is exactly the 36-line owner-controlled
  relocation set (digest byte-equal to the A5-authoritative
  `d1a974b3248df1764007f77b4d423fc9ff0e85fc7d6add16005058e5156495db`,
  unchanged across the entire window) plus the three subordinate
  coordination artifacts (S1/S2/S3) and nothing else; the frontend
  tree is clean after `c85f93b`. Observation recorded for parent
  review: §2's `f1d1d8e1…` literal is a stale pre-A5 capture of the
  36-line relocation set (A5 at state 106 fixed the authoritative
  digest to `d1a974b3…`; every leaf review verified the set unchanged
  against it).
- **`KI-W5-V3` PASS** (inside V1) — `W5-B08` rendered and filtered the
  200-row/200-draft scale fixture ("200 rows", "200 of 200 selected",
  search filter); `W5-R01` proved the single poll timer (exactly five
  GETs, ladder gaps within 2000/3000/4500/6750 tolerance, terminal
  stop); `W5-R06` proved bounded chart instances/listener sets (11
  canvases, no duplicates, controlled teardown/recreate); ceilings via
  `W5-C12` (page-size/pagination/200-draft caps) + `W5-B08` + `W5-R06`.
- **`KI-W5-V4` PASS** — `W5-R07` unauthenticated probes (401
  `AUTHENTICATION_REQUIRED` + `Cache-Control: no-store`; 400
  `INVALID_QUERY_PARAMETERS` unknown key; 400 `INVALID_RESEARCH_ID`;
  generic 404); no-CDN via `W5-I06` grep + the V1 network allowlist
  (zero non-app, zero CDN); `localStorage` limited to
  `ki-dashboard-theme` (`W5-B06`); durable GET-only reload (`W5-R02`);
  accessible error/empty/loading states (`W5-C11` + `W5-B01`).
- **`KI-W5-I001-M` PASS** — union of the four certificates (three node
  + one browser) = exactly the 43-ID required set; per-LF digest
  byte-equal to the frozen
  `cb8ef6d7cb87b5a451e438d11b0f037c8130f78d0c3e033b1304f78bfa1f6bdb`;
  zero skipped, zero oracle failures, zero duplicates, zero
  unexpected IDs (all independently recomputed by the window agent).

### §12.4 integration certificate

```yaml
certificate: WINDOW-AGENT-INTEGRATION-PASS
parent_window_id: KI-W5
integration_assessment_id: KI-W5-I001
window_agent_identity: KI-W5-WINDOW-AGENT (assignment ASG-KI-W5-WA-02)
accepted_initial_subwindows: [KI-W5-S001 … KI-W5-S027 (all 27)]
accepted_corrective_subwindows: [KI-W5-C001 (selection-review.tsx, EV-KI-W5-S19), KI-W5-C002 (research-form.tsx, EV-KI-W5-S32), KI-W5-C003 (browser harness, EV-KI-W5-S35)]
superseded_failed_assessments: []
expected_changed_file_set: [the 27 planned paths of §2]
actual_changed_file_set: [the 27 planned paths; plus 17 runner-output evidence artifacts under frontend/review-evidence/keyword-intelligence/KI-W5/ committed by the requester in c85f93b]
expected_changed_file_set_digest: a04dce13038a3d180ddab0c8412890af065e3f5ab5019540c87a5664485320e6
actual_changed_file_set_digest: a04dce13038a3d180ddab0c8412890af065e3f5ab5019540c87a5664485320e6 (over the 27-path planned set; the evidence artifacts are non-source runner output outside the planned set)
required_case_count: 43
registered_case_count: 43
executed_case_count: 43
required_case_set_digest: cb8ef6d7cb87b5a451e438d11b0f037c8130f78d0c3e033b1304f78bfa1f6bdb
registered_case_set_digest: cb8ef6d7cb87b5a451e438d11b0f037c8130f78d0c3e033b1304f78bfa1f6bdb
executed_case_set_digest: cb8ef6d7cb87b5a451e438d11b0f037c8130f78d0c3e033b1304f78bfa1f6bdb
skipped_required_cases: []
duplicate_case_ids: []
unexpected_case_ids: []
missing_activation_witnesses: []
oracle_failures: []
negative_controls_expected: 12
negative_controls_falsified: 0
substitute_fidelity_failures: []
accepted_evidence_invalidations_unresolved: []
commands_and_outcomes:
  - "node test/browser/keyword-intelligence-dashboard.mjs (full build) → exit 0, 15/15, certificate digest 00708893…, scenarios both true"
  - "npm run check → exit 0 (eslint 0 errors/1 pre-existing warning; 118/118 tests; build compiled)"
  - "root porcelain → 36 relocation lines (digest d1a974b3…, byte-equal A5) + 3 subordinate artifacts"
gates_reused_with_dependency_proof: []
prohibited_actions_observed: []
successor_parent_window_work_started: false
residual_parent_review_items:
  - S1 recorded interpretations: §0.1 KI-W5-P2 fixture-server reading; §3.5/§3.8 two materialized charts; §6.2 W5-NC06 control form; §5.25 pure-logic test-substitute layer
  - KI-W5-C002 stricter-than-contract nonempty seed/search/clusterId export validation (EV-KI-W5-S27)
  - §2 stale pre-A5 literal f1d1d8e1… superseded by the A5-authoritative d1a974b3… relocation digest
  - requester commit c85f93b additionally contains the 17 runner-output evidence artifacts (deviation from the "harness only" intent recorded here factually)
  - environmental baseline: requester-authorized window-level `npx next typegen` refreshes (EV-KI-W5-S24 et al.) — gitignored-only writes, no leaf generator authority
status: READY_FOR_PARENT_REVIEW
```

- **Disposition:** `KI-W5-I001` PASS. S2 transitions to
  `READY_FOR_PARENT_REVIEW`; §12.5 consolidated handoff produced. The
  window agent claims no parent acceptance and does not begin KI-W6.
