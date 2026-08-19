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
