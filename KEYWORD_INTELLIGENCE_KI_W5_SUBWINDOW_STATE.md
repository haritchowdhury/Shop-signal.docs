# KI-W5 Sub-Window State (`S2`)

Mechanical state file. Only the window agent writes it, only inside the
`ASG-KI-W5-WA-02` scope. Parent artifacts (`A1`–`A6`) are never modified
here. This file records no evidence; see `S3`.

```yaml
state_version: 1
artifact: KEYWORD_INTELLIGENCE_KI_W5_SUBWINDOW_STATE.md
parent_window_id: KI-W5
parent_assignment_id: ASG-KI-W5-WA-02
window_agent_identity: KI-W5-WINDOW-AGENT
decomposition_checklist: KEYWORD_INTELLIGENCE_KI_W5_SUBWINDOW_CHECKLIST.md
decomposition_revision: 740f84cfbc910782d501ac68c43f9fe24a58fbec55f242cb9595c1a36b92588d
decomposition_addendum_revision: 9c659a7876edf8e8e8b4a2a5db4e387cf4359bf77315d16c83ae5b33e8832b15
decomposition_addendum: §9 (leaf dispatch + P1 tracking protocol; requester-authorized 2026-08-19; §0–§8 byte-identical to decomposition_revision)
evidence_file: KEYWORD_INTELLIGENCE_KI_W5_SUBWINDOW_EVIDENCE.md
revisions:
  parent_standard: 3b7a4fd25156e1adfbc92abb835c5f82a0d18c686b1c1150feb202f2d944d2ac
  subwindow_standard: 1766f9107ce7d315877b75d4b0ea2b5521dff1c321e12f890b03787d66196ded
  contract: 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c
  decision: c2dc635e5aa58f88c1ec465154663d314af68570fd4cbfdfca7b51c393c6f70f
  parent_checklist: 324667cbe0d467ecf4f913c93e91087e75192bd463e0c05b033ee418754a362e
decomposition_status: READY
parent_review:
  evidence_entry: EV-KI-A-044/EV-KI-A-045 (decomposition approved; serialization correction closed)
  pin_correction: d1a974b3248df1764007f77b4d423fc9ff0e85fc7d6add16005058e5156495db (authoritative LC_ALL=C starting-inventory digest, per EV-KI-A-045)
  a5_state: 106 (DECOMPOSITION_APPROVED)
current_subwindow: NONE
current_subwindow_assignment_id: NONE
current_subwindow_assigned_agent: UNASSIGNED
next_subwindow: NONE
accepted_subwindows: [KI-W5-S001, KI-W5-S002, KI-W5-S003, KI-W5-S004, KI-W5-S005, KI-W5-S006, KI-W5-S007, KI-W5-S008, KI-W5-S009, KI-W5-S010, KI-W5-S011, KI-W5-S012, KI-W5-S013, KI-W5-S014, KI-W5-S015, KI-W5-S016, KI-W5-S017, KI-W5-S018, KI-W5-S019, KI-W5-S020, KI-W5-S021, KI-W5-S022, KI-W5-S023, KI-W5-S024, KI-W5-S025, KI-W5-S026, KI-W5-S027, KI-W5-I001]
corrective_subwindows: [KI-W5-C001 (closed: executed by window agent under requester authorization; EV-KI-W5-S19)]
integration_assessments: []
window_status: READY_FOR_PARENT_REVIEW
last_updated: 2026-08-20T04:35:00+05:30
```

## Sub-window registry

| ID | Type | File | Status | Assigned agent | Assignment ID |
|---|---|---|---|---|---|
| `KI-W5-S001` | FILE | `frontend/lib/keyword-intelligence-types.ts` | ACCEPTED (ending digest `1619572d…`; commit `ad87f9b4`) | LEAF | ASG-KI-W5-S001 |
| `KI-W5-S002` | FILE | `frontend/lib/keyword-intelligence-validation.ts` | ACCEPTED (ending digest `8275def2…`; commit `69e5e3a`) | LEAF | ASG-KI-W5-S002 |
| `KI-W5-S003` | FILE | `frontend/lib/api-types.ts` | ACCEPTED (ending digest `e91b62a2…`; commit `3953bb7`) | LEAF | ASG-KI-W5-S003 |
| `KI-W5-S004` | FILE | `frontend/lib/api-validation.ts` | ACCEPTED (ending digest `6b2999fc…`; commit `e5b7aa3`) | LEAF | ASG-KI-W5-S004 |
| `KI-W5-S005` | FILE | `frontend/lib/client-api.ts` | ACCEPTED (ending digest `b57d7b86…`; commit `9730806`) | LEAF | ASG-KI-W5-S005 |
| `KI-W5-S006` | FILE | `frontend/lib/keyword-intelligence-view-model.ts` | ACCEPTED (ending digest `b91f0f5e…`; commit `d6ca5aa`) | LEAF | ASG-KI-W5-S006 |
| `KI-W5-S007` | FILE | `frontend/components/keyword-intelligence/keyword-dashboard.module.css` | ACCEPTED (ending digest `c8d8cebb…`; commit `1a51f6e`) | LEAF | ASG-KI-W5-S007 |
| `KI-W5-S008` | FILE | `frontend/components/keyword-intelligence/research-form.tsx` | ACCEPTED (ending digest `9583f663…`; commit `82197b1`) | LEAF | ASG-KI-W5-S008 |
| `KI-W5-S009` | FILE | `frontend/components/keyword-intelligence/research-status.tsx` | ACCEPTED (ending digest `9a28bcf1…`; commit `71eab6b`) | LEAF | ASG-KI-W5-S009 |
| `KI-W5-S010` | FILE | `frontend/components/keyword-intelligence/filter-bar.tsx` | ACCEPTED (ending digest `a5d8cc98…`; commit `6626baf`) | LEAF | ASG-KI-W5-S010 |
| `KI-W5-S011` | FILE | `frontend/components/keyword-intelligence/summary-cards.tsx` | ACCEPTED (ending digest `3690e3f1…`; commit `1bbf069`) | LEAF | ASG-KI-W5-S011 |
| `KI-W5-S012` | FILE | `frontend/components/keyword-intelligence/keyword-table.tsx` | ACCEPTED (ending digest `f7686ead…`; commit `83cf7dc`) | LEAF | ASG-KI-W5-S012 |
| `KI-W5-S003` | FILE | `frontend/lib/api-types.ts` | NOT_STARTED | UNASSIGNED | NONE |
| `KI-W5-S004` | FILE | `frontend/lib/api-validation.ts` | NOT_STARTED | UNASSIGNED | NONE |
| `KI-W5-S005` | FILE | `frontend/lib/client-api.ts` | NOT_STARTED | UNASSIGNED | NONE |
| `KI-W5-S006` | FILE | `frontend/lib/keyword-intelligence-view-model.ts` | NOT_STARTED | UNASSIGNED | NONE |
| `KI-W5-S007` | FILE | `frontend/components/keyword-intelligence/keyword-dashboard.module.css` | NOT_STARTED | UNASSIGNED | NONE |
| `KI-W5-S008` | FILE | `frontend/components/keyword-intelligence/research-form.tsx` | NOT_STARTED | UNASSIGNED | NONE |
| `KI-W5-S009` | FILE | `frontend/components/keyword-intelligence/research-status.tsx` | NOT_STARTED | UNASSIGNED | NONE |
| `KI-W5-S010` | FILE | `frontend/components/keyword-intelligence/filter-bar.tsx` | NOT_STARTED | UNASSIGNED | NONE |
| `KI-W5-S011` | FILE | `frontend/components/keyword-intelligence/summary-cards.tsx` | NOT_STARTED | UNASSIGNED | NONE |
| `KI-W5-S012` | FILE | `frontend/components/keyword-intelligence/keyword-table.tsx` | NOT_STARTED | UNASSIGNED | NONE |
| `KI-W5-S013` | FILE | `frontend/components/keyword-intelligence/selection-review.tsx` | ACCEPTED via `KI-W5-C001` (superseding digest `5d127c19…`; commits `6f99357`+`9eec30e`) | LEAF + WINDOW-AGENT CORRECTION | ASG-KI-W5-S013 |
| `KI-W5-S014` | FILE | `frontend/components/keyword-intelligence/chart-panels.tsx` | ACCEPTED (ending digest `0297f218…`; commit `006301c`) | LEAF | ASG-KI-W5-S014 |
| `KI-W5-S015` | FILE | `frontend/components/keyword-intelligence/cluster-landscape.tsx` | ACCEPTED (ending digest `2304b0c8…`; commit `2841151`) | LEAF | ASG-KI-W5-S015 |
| `KI-W5-S016` | FILE | `frontend/components/keyword-intelligence/research-dashboard.tsx` | ACCEPTED (ending digest `94ba68ee…`; commit `9606cfd`) | LEAF | ASG-KI-W5-S016 |
| `KI-W5-S017` | FILE | `frontend/app/api/keyword-research/route.ts` | ACCEPTED (ending digest `259bdfb4…`; commit `1168e7a`) | LEAF | ASG-KI-W5-S017 |
| `KI-W5-S018` | FILE | `frontend/app/api/keyword-research/[researchId]/route.ts` | ACCEPTED (ending digest `fbc9e75d…`; commit `a07fe65`; C2 unblocked by requester-authorized window-level `next typegen`, `EV-KI-W5-S24`) | LEAF | ASG-KI-W5-S018 |
| `KI-W5-S019` | FILE | `frontend/app/api/keyword-research/[researchId]/selection/route.ts` | ACCEPTED (ending digest `3c44ed2f…`; commit `a6d4c52`) | LEAF | ASG-KI-W5-S019 |
| `KI-W5-S020` | FILE | `frontend/app/api/keyword-research/[researchId]/runs/route.ts` | ACCEPTED (ending digest `270c0e64…`; commit `e13ba00`) | LEAF | ASG-KI-W5-S020 |
| `KI-W5-S021` | FILE | `frontend/app/api/keyword-research/[researchId]/export.csv/route.ts` | ACCEPTED (ending digest `fde0b5c4…`; commit `cad36c4`; one accepted stricter-than-contract deviation — nonempty `seed`/`search`/`clusterId`, `EV-KI-W5-S27`) | LEAF | ASG-KI-W5-S021 |
| `KI-W5-S022` | FILE | `frontend/app/keywords/page.tsx` | ACCEPTED (ending digest `07a82664…`; commit `32f6aaf`) | LEAF | ASG-KI-W5-S022 |
| `KI-W5-S023` | FILE | `frontend/app/keywords/[researchId]/page.tsx` | ACCEPTED (ending digest `a82eb39c…`; commit `71ca03c`) | LEAF | ASG-KI-W5-S023 |
| `KI-W5-S024` | FILE | `frontend/test/keyword-intelligence-api.test.ts` | ACCEPTED (ending digest `a2f40c62…`; commit `1c8062f`; certificate digests independently recomputed, `EV-KI-W5-S30`) | LEAF | ASG-KI-W5-S024 |
| `KI-W5-S025` | FILE | `frontend/test/keyword-intelligence-components.test.ts` | ACCEPTED (ending digest `6e14ecc8…`; commit `cfde28c`; certificate digests independently recomputed, `EV-KI-W5-S31`) | LEAF | ASG-KI-W5-S025 |
| `KI-W5-S026` | FILE | `frontend/test/keyword-intelligence-inventory.test.ts` | ACCEPTED (ending digest `67828152…`; commit `0aa5ff9` with C002; certificate digests independently recomputed, `EV-KI-W5-S33`) | LEAF | ASG-KI-W5-S026 |
| `KI-W5-S027` | FILE | `frontend/test/browser/keyword-intelligence-dashboard.mjs` | ACCEPTED (ending digest `6a531ca8…`; commit `983d3ed`; not executed at leaf level per contract, `EV-KI-W5-S34`; superseded by `KI-W5-C003` → `d28cc1b5…` at `c85f93b`, `EV-KI-W5-S35`) | LEAF | ASG-KI-W5-S027 |
| `KI-W5-I001` | ASSESS | none | PASS (gates `KI-W5-V1`–`V4` + `KI-W5-I001-M` all green on frozen final inputs; §12.4 certificate `WINDOW-AGENT-INTEGRATION-PASS`, `EV-KI-W5-S36`) | WINDOW-AGENT | ASG-KI-W5-WA-02 |
| `KI-W5-S014` | FILE | `frontend/components/keyword-intelligence/chart-panels.tsx` | NOT_STARTED | UNASSIGNED | NONE |
| `KI-W5-S015` | FILE | `frontend/components/keyword-intelligence/cluster-landscape.tsx` | NOT_STARTED | UNASSIGNED | NONE |
| `KI-W5-S016` | FILE | `frontend/components/keyword-intelligence/research-dashboard.tsx` | NOT_STARTED | UNASSIGNED | NONE |
| `KI-W5-S017` | FILE | `frontend/app/api/keyword-research/route.ts` | NOT_STARTED | UNASSIGNED | NONE |
| `KI-W5-S018` | FILE | `frontend/app/api/keyword-research/[researchId]/route.ts` | NOT_STARTED | UNASSIGNED | NONE |
| `KI-W5-S019` | FILE | `frontend/app/api/keyword-research/[researchId]/selection/route.ts` | NOT_STARTED | UNASSIGNED | NONE |
| `KI-W5-S020` | FILE | `frontend/app/api/keyword-research/[researchId]/runs/route.ts` | NOT_STARTED | UNASSIGNED | NONE |
| `KI-W5-S021` | FILE | `frontend/app/api/keyword-research/[researchId]/export.csv/route.ts` | NOT_STARTED | UNASSIGNED | NONE |
| `KI-W5-S022` | FILE | `frontend/app/keywords/page.tsx` | NOT_STARTED | UNASSIGNED | NONE |
| `KI-W5-S023` | FILE | `frontend/app/keywords/[researchId]/page.tsx` | NOT_STARTED | UNASSIGNED | NONE |
| `KI-W5-S024` | FILE | `frontend/test/keyword-intelligence-api.test.ts` | NOT_STARTED | UNASSIGNED | NONE |
| `KI-W5-S025` | FILE | `frontend/test/keyword-intelligence-components.test.ts` | NOT_STARTED | UNASSIGNED | NONE |
| `KI-W5-S026` | FILE | `frontend/test/keyword-intelligence-inventory.test.ts` | NOT_STARTED | UNASSIGNED | NONE |
| `KI-W5-S027` | FILE | `frontend/test/browser/keyword-intelligence-dashboard.mjs` | NOT_STARTED | UNASSIGNED | NONE |
| `KI-W5-I001` | ASSESS | (none) | NOT_STARTED | RESERVED (KI-W5-WINDOW-AGENT) | NONE |

Counters: accepted 12/27 file leaves; corrections 0; integration
assessments 0/1; no leaf assigned. The 27 planned paths, per-LF
`LC_ALL=C` set digest
`a04dce13038a3d180ddab0c8412890af065e3f5ab5019540c87a5664485320e6`,
byte-equal the A4 `delegable_file_set_digest`.

Counters: accepted 27/27 file leaves; corrections 3 closed
(`KI-W5-C001`, `EV-KI-W5-S19`; `KI-W5-C002`, `EV-KI-W5-S32`;
`KI-W5-C003`, `EV-KI-W5-S35` — each a single file from the 27-file
set, each executed by the window agent under explicit requester
authorization); integration assessments 1/1 PASS (`KI-W5-I001`,
`EV-KI-W5-S36`); no leaf assigned, no next sub-window. The 27 planned
paths, per-LF `LC_ALL=C` set digest
`a04dce13038a3d180ddab0c8412890af065e3f5ab5019540c87a5664485320e6`,
byte-equal the A4 `delegable_file_set_digest`; the 43-case union
digest is byte-equal the frozen `cb8ef6d7…` (I001-M).

Boundary: TERMINAL. All 27 file leaves accepted (`EV-KI-W5-S04`
through `EV-KI-W5-S34`), three corrections closed, gates
`KI-W5-V1`–`V4` and `KI-W5-I001-M` PASS on frozen final inputs, §12.4
integration certificate appended (`WINDOW-AGENT-INTEGRATION-PASS`).
The window is `READY_FOR_PARENT_REVIEW`; the window agent claims no
parent acceptance, assigns no further leaf, and does not begin
`KI-W6` without a recorded parent review. Residual parent-review
items are enumerated in `EV-KI-W5-S36` (S1 recorded interpretations,
C002 stricter-export deviation, §2 stale `f1d1d8e1…` literal
superseded by the A5-authoritative `d1a974b3…`, the evidence-artifact
inclusion in `c85f93b`, and the typegen environmental baseline).

Environmental baseline: requester-authorized window-level
`npx next typegen` (`EV-KI-W5-S24`, 2026-08-19) regenerated the
gitignored `.next/types/routes.d.ts` so the frozen I-F7–I-F10
`RouteContext`/`PageProps` literals typecheck at leaf C2; the window
agent refreshes it whenever a leaf introduces a new route literal
(re-applied at S019–S023, `EV-KI-W5-S25`–`S29`). It grants no
leaf-level generator authority.

Execution policy notes:

- The requester performs all git commits; leaves and the window agent
  never commit.
- Leaf P2 preflight proves the frontend tree clean at HEAD
  `0dfa1acac50fac3a86d02ec674c6d2bab645832d` (or containing exactly the
  accepted predecessor endings for later leaves); unstarted-leaf starting
  digests remain the frozen S1 §2 content baselines.
- Recorded interpretations awaiting parent decomposition review are listed
  in S1 §8; none delegates a decision to a leaf.
- Dispatch protocol per S1 §9 (requester-authorized addendum): every leaf
  dispatch from `KI-W5-S008` onward includes the verbatim block text plus
  the checklist path; the leaf reads its block before editing; the
  handoff quotes `subwindow_id`/`writable_file`/`starting_file_digest`
  unless the requester waives the quote form.

## P1 block-consumption tracking (S1 §9.2; updated at every acceptance)

| Leaf | Commit | P1 evidence | Status |
|---|---|---|---|
| `KI-W5-S001` | `ad87f9b4` | `EV-KI-W5-S10` — I-F1 surface distinctions (24 types, nullability split, 6-field snapshot exclusion) | TRACKED |
| `KI-W5-S002` | `69e5e3a` | `EV-KI-W5-S10` — eight-export I-F2 surface, pattern literals, block-anchored ledger transcription (17/13-key erratum path) | TRACKED |
| `KI-W5-S003` | `3953bb7` | `EV-KI-W5-S10` — byte-equal I-F3 block incl. comment literal + alphabetical 24 names | TRACKED |
| `KI-W5-S004` | `e5b7aa3` | `EV-KI-W5-S10` — byte-equal I-F4 block incl. comment literal + exact name order | TRACKED |
| `KI-W5-S005` | `9730806` | `EV-KI-W5-S10` — byte-equal I-F5 bodies/URLs/bodies + line-2 import placement | TRACKED |
| `KI-W5-S006` | `d6ca5aa` | `EV-KI-W5-S10` — exact 21-entry I-F15 inventory in fixed order + poll-ladder constants | TRACKED |
| `KI-W5-S007` | `1a51f6e` | `EV-KI-W5-S11` P1 line — header conversion-list literal exists only in S1 §5.7/I-F13 (quote form waived by requester) | TRACKED |
| `KI-W5-S008` | `82197b1` | `EV-KI-W5-S13` P1 line — four block read_only_scope ids + I-F14 behavioral set (quote form waived; artifact-literal proof) | TRACKED |
| `KI-W5-S009` | `71eab6b` | `EV-KI-W5-S14` — full §9.1 quote form + §12.3 certificate supplied; verified against disk | TRACKED |
| `KI-W5-S010` | `6626baf` | `EV-KI-W5-S15` — 14-field `data-filter` set + byte-equal standalone tip text (quote form waived; artifact-literal proof) | TRACKED |
| `KI-W5-S011` | `1bbf069` | `EV-KI-W5-S16` — summary-driven mandate + byte-equal funnel notes prove block + anchor reads (quote form waived) | TRACKED |
| `KI-W5-S012` | `83cf7dc` | `EV-KI-W5-S17` — byte-equal TABLE_COLS tips + `aria-sort` mandate + `itemId` key mandate prove block + anchor reads (quote form waived) | TRACKED |
| `KI-W5-S013` | `6f99357` + `9eec30e` | `EV-KI-W5-S18` (defects) + `EV-KI-W5-S19` (correction verified byte-identical in `9eec30e`) | TRACKED |
| `KI-W5-S014` | `006301c` | `EV-KI-W5-S20` — eleven exact I-F15 chart ids + I-F17 lifecycle/no-CDN mandates prove block reads (quote form waived) | TRACKED |
| `KI-W5-S015` | `2841151` | `EV-KI-W5-S21` — byte-equal projection/interaction constants + pointerId/no-Chart mandates prove block + anchor reads (quote form waived) | TRACKED |
| `KI-W5-S016` | `9606cfd` | `EV-KI-W5-S22` — amended §10 `onDraftChange` composition + 409-code/ref-idempotency/GET-only-retry/I-F15-wrapper mandates prove block reads (quote form waived) | TRACKED |
| `KI-W5-S017` | `1168e7a` | `EV-KI-W5-S23` — exact I-F6 guard order + verbatim error codes/messages + re-serialized-seeds forwarding rule prove block reads (quote form waived) | TRACKED |
| `KI-W5-S018` | `a07fe65` | `EV-KI-W5-S24` — exact I-F7 ordering + RouteContext literal + verbatim message prove block reads; C2 blocker root-caused to stale gitignored generated route types, resolved by requester-authorized window-level `next typegen` (standing baseline for S019–S021) (quote form waived) | TRACKED |
| `KI-W5-S019` | `a6d4c52` | `EV-KI-W5-S25` — 262144 cap + exact key-set/safe-integer/items-≤200 mandates + verbatim-body-string forwarding rule prove block reads; typegen refresh under standing baseline (quote form waived) | TRACKED |
| `KI-W5-S020` | `e13ba00` | `EV-KI-W5-S26` — 4096 cap + exact key-set/expectedSelectionRevision/CLIENT_REQUEST_ID_PATTERN mandates + verbatim forwarding rule prove block reads; typegen refresh under standing baseline (quote form waived) | TRACKED |
| `KI-W5-S021` | `cad36c4` | `EV-KI-W5-S27` — no-proxyBackend rule + env-parity + full DEC-KI-019 allowlist table + CSV passthrough/no-store mandates prove block reads; typegen refresh under standing baseline; one accepted stricter deviation (nonempty seed/search/clusterId) (quote form waived) | TRACKED |
| `KI-W5-S022` | `32f6aaf` | `EV-KI-W5-S28` — exact metadata/force-dynamic + runs-page shell class-for-class mirror + prop-less `<ResearchForm />` prove block reads; typegen refresh under standing baseline (quote form waived) | TRACKED |
| `KI-W5-S023` | `71ca03c` | `EV-KI-W5-S29` — PageProps typing + awaited params + `<ResearchDashboard researchId>` + no-ID-validation rule prove block reads; typegen refresh under standing baseline (quote form waived) | TRACKED |
| `KI-W5-S024` | `1c8062f` | `EV-KI-W5-S30` — ten §6.1-matching subtest titles + three §6.2 mutation controls + literal fixture builder + I-F18 certificate with §3.1 digests prove block reads (quote form waived) | TRACKED |
| `KI-W5-S025` | `cfde28c` | `EV-KI-W5-S31` — twelve §6.1-matching subtest titles + NC02/NC08/NC09 mutation oracles + literal parity values + I-F18 certificate with §3.1 digests prove block reads (quote form waived) | TRACKED |
| `KI-W5-S026` | `0aa5ff9` | `EV-KI-W5-S33` — six §6.1-matching subtests + five controls (NC03/NC04/NC06/NC10/NC12-I02) + I-F15/owned-path literals + no-CDN grep + I-F18 certificate prove block reads; its W5-I05 check exposed and closed correction `KI-W5-C002` (`EV-KI-W5-S32`; S008 registry superseded: research-form.tsx digest `9583f663…` → `b66c6f97…` at `0aa5ff9`) (quote form waived) | TRACKED |
| `KI-W5-S027` | `983d3ed` | `EV-KI-W5-S34` — five-phase harness contract implemented clause-for-clause (build-refusal/skip-build, envelope-validated fixtures, fetch interception with request log, fifteen B/R scenarios + NC05/NC11 controls with restoration, finally-teardown + I-F18 browser certificate) (quote form waived) | TRACKED (superseded by C003: `c85f93b`, digest `d28cc1b5…`) |
| `KI-W5-I001` | `c85f93b` (C003 harness correction; the assessment itself writes no files) | `EV-KI-W5-S36` — V1 15/15 full-build browser run (certificate `00708893…`, zero console/network violations), V2 `npm run check` exit 0 + 27-path set digest byte-equal `a04dce13…` + root set = 36 relocation lines (`d1a974b3…`) + 3 subordinates, V3 scale/poll/chart-bounding inside V1, V4 auth/privacy probes, I001-M 43-ID union digest byte-equal `cb8ef6d7…`; §12.4 `WINDOW-AGENT-INTEGRATION-PASS` | TRACKED |
| `KI-W5-S017` | — | — | PENDING |
| `KI-W5-S018` | — | — | PENDING |
| `KI-W5-S019` | — | — | PENDING |
| `KI-W5-S020` | — | — | PENDING |
| `KI-W5-S021` | — | — | PENDING |
| `KI-W5-S022` | — | — | PENDING |
| `KI-W5-S023` | — | — | PENDING |
| `KI-W5-S024` | — | — | PENDING |
| `KI-W5-S025` | — | — | PENDING |
| `KI-W5-S026` | — | — | PENDING |
| `KI-W5-S027` | — | — | PENDING |
| `KI-W5-I001` | — | — | PENDING |
