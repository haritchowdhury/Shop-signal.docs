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
next_subwindow: KI-W5-S008
accepted_subwindows: [KI-W5-S001, KI-W5-S002, KI-W5-S003, KI-W5-S004, KI-W5-S005, KI-W5-S006, KI-W5-S007]
corrective_subwindows: []
integration_assessments: []
window_status: EXECUTING
last_updated: 2026-08-19T16:55:00+05:30
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
| `KI-W5-S013` | FILE | `frontend/components/keyword-intelligence/selection-review.tsx` | NOT_STARTED | UNASSIGNED | NONE |
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

Counters: accepted 7/27 file leaves; corrections 0; integration
assessments 0/1; no leaf assigned. The 27 planned paths, per-LF
`LC_ALL=C` set digest
`a04dce13038a3d180ddab0c8412890af065e3f5ab5019540c87a5664485320e6`,
byte-equal the A4 `delegable_file_set_digest`.

Boundary: `KI-W5-S001`–`KI-W5-S007` are accepted (window reviews
`EV-KI-W5-S04` through `EV-KI-W5-S11`; leaf P1 tracking per
`EV-KI-W5-S10`); `KI-W5-S008` is next and assignable. Gates
`KI-W5-V1`–`V4` and merge `KI-W5-I001-M` remain reserved to
`KI-W5-I001`.

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
| `KI-W5-S008` | — | — | PENDING |
| `KI-W5-S009` | — | — | PENDING |
| `KI-W5-S010` | — | — | PENDING |
| `KI-W5-S011` | — | — | PENDING |
| `KI-W5-S012` | — | — | PENDING |
| `KI-W5-S013` | — | — | PENDING |
| `KI-W5-S014` | — | — | PENDING |
| `KI-W5-S015` | — | — | PENDING |
| `KI-W5-S016` | — | — | PENDING |
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
