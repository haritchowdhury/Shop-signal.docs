# KI-W6 Sub-Window State (`S2`)

Mechanical state file. Only the window agent writes it, only inside the
`ASG-KI-W6-WA-01` scope. Parent artifacts (`A1`–`A7`) are never modified
here. This file records no evidence; see `S3`.

```yaml
state_version: 1
artifact: KEYWORD_INTELLIGENCE_KI_W6_SUBWINDOW_STATE.md
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-01
window_agent_identity: KI-W6-WINDOW-AGENT
decomposition_checklist: KEYWORD_INTELLIGENCE_KI_W6_SUBWINDOW_CHECKLIST.md
decomposition_revision: a0e3e28b7d9e272cfa6b1eec79f224d2b156725d7ebc86b729bfe3067dd42d87
evidence_file: KEYWORD_INTELLIGENCE_KI_W6_SUBWINDOW_EVIDENCE.md
revisions:
  parent_standard: 3b7a4fd25156e1adfbc92abb835c5f82a0d18c686b1c1150feb202f2d944d2ac
  subwindow_standard: 1766f9107ce7d315877b75d4b0ea2b5521dff1c321e12f890b03787d66196ded
  contract: 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c
  decision: c2dc635e5aa58f88c1ec465154663d314af68570fd4cbfdfca7b51c393c6f70f
  parent_checklist: 324667cbe0d467ecf4f913c93e91087e75192bd463e0c05b033ee418754a362e
decomposition_status: AWAITING_PARENT_DECOMPOSITION_REVIEW
current_subwindow: NONE
current_subwindow_assignment_id: NONE
current_subwindow_assigned_agent: UNASSIGNED
subwindow_type: NONE
authorized_write_file: NONE
authorized_read_scope: []
authorized_actions: []
prohibited_actions: []
may_start_successor: false
current_status: AWAITING_PARENT_DECOMPOSITION_REVIEW
accepted_subwindows: []
next_subwindow: KI-W6-S001
blocker: null
last_updated: 2026-08-20T09:40:00+05:30
```

## Sub-window registry

| ID | Type | File | Status | Assigned agent | Assignment ID |
|---|---|---|---|---|---|
| `KI-W6-S001` | FILE | `email_scraper/test/keyword-intelligence-e2e.integration.test.js` | NOT_STARTED | UNASSIGNED | NONE |
| `KI-W6-S002` | FILE | `frontend/test/browser/keyword-intelligence-e2e.mjs` | NOT_STARTED | UNASSIGNED | NONE |
| `KI-W6-I001` | ASSESS | (none) | NOT_STARTED | RESERVED (KI-W6-WINDOW-AGENT) | NONE |

Counters: accepted 0/2 file leaves; corrections 0; integration assessments
0/1; no leaf assigned. The two planned paths, per-LF `LC_ALL=C` set digest
`bb9f6381cc3b65d08b696fa1f62a2d75759289b4d4f0f44554ca44a2ebf56edc`.

Boundary: decomposition complete; awaiting parent decomposition review
before any leaf assignment. The seven recorded interpretations of S1 §0.1
are pending parent adjudication. The requester performs all git commits.

Execution policy notes:

- Leaf P2 preflight proves both nested repositories clean at their pinned
  HEADs (`email_scraper` `fac5bb0`, `frontend` `c85f93b`) or containing
  exactly the accepted predecessor endings, and the root 36-line
  owner-controlled relocation set (authoritative digest
  `d1a974b3248df1764007f77b4d423fc9ff0e85fc7d6add16005058e5156495db`, per
  `EV-KI-A-045`) unchanged; the three KI-W5 subordinate artifacts (tracked,
  modified) and this window's three subordinate artifacts are the only
  additional root entries.
- Leaf dispatch protocol per S1 §8: every dispatch includes the verbatim
  block text plus the checklist path; the leaf reads its block before
  editing; the handoff quotes `subwindow_id`/`writable_file`/
  `starting_file_digest` unless the requester waives the quote form.
- Recorded interpretations awaiting parent decomposition review are listed in
  S1 §0.1; none delegates a decision to a leaf.
- Database work only through `test/helpers/isolated-postgres.js` with
  `ALLOW_DATABASE_TESTS=true` and an isolated `TEST_DATABASE_URL` distinct
  from production (D2A); no `public`-schema use; `finally` cleanup mandatory.
