# My Runs Research Resume — Locked Product Contract (A1)

Status: `LOCKED / PLAN-ONLY / NOT YET ASSIGNED`

Companion authorities:

- A2: `MY_RUNS_RESEARCH_RESUME_DISCOVERY_DOSSIER.md`
- A3: `MY_RUNS_RESEARCH_RESUME_DECISION_LEDGER.md`
- A4: `MY_RUNS_RESEARCH_RESUME_EXECUTION_CHECKLIST.md`
- A5: `MY_RUNS_RESEARCH_RESUME_ACTIVE_STATE.md`
- A6: `MY_RUNS_RESEARCH_RESUME_EVIDENCE.md`
- A7: `MY_RUNS_RESEARCH_RESUME_CHANGELOG.md`
- A8: `MY_RUNS_RESEARCH_RESUME_TRACEABILITY.md`

## Product outcome

The existing authenticated `/runs` page becomes the single resume surface for
two mutually exclusive work phases:

1. keyword research that has not produced a discovery `Run`; and
2. existing discovery `Run` rows.

Selecting a keyword-research row opens the fixed local route
`/keywords/{researchId}`. That dashboard reloads durable state, resumes polling
for queued/running research, presents persisted results for completed research,
and permits the existing save/finalize workflow. Selecting a discovery-run row
continues to open `/runs/{runId}`.

## Locked requirements

- `MRR-REQ-001` `/runs` MUST show every owner-visible `KeywordResearch` whose
  `runs` relation is empty, including `queued`, `running`, `completed`, and
  `failed` states.
- `MRR-REQ-002` Each research row MUST link only to
  `/keywords/${encodeURIComponent(researchId)}`; backend-provided destinations
  and arbitrary URLs are forbidden.
- `MRR-REQ-003` The research summary MUST expose only the exact lightweight
  contract in A3. Completed result documents, selections, config snapshots,
  provider material, and artifacts MUST NOT enter the list query or response.
- `MRR-REQ-004` Research with any related `Run` MUST be absent from the
  research section. Its resulting run remains in the existing discovery-run
  section, so a handoff never creates duplicate workspace rows.
- `MRR-REQ-005` Both count and item queries MUST include the authenticated
  `ownerId`. Foreign research MUST affect neither items nor pagination totals.
- `MRR-REQ-006` Research and run lists MUST have independent page state,
  pagination, loading, error, and retry behavior. Failure of one list MUST NOT
  hide a successfully loaded other list.
- `MRR-REQ-007` Existing `/api/runs`, `RunListResponse`, run ordering, run-row
  rendering, run pagination, and `/runs/{runId}` navigation MUST remain
  compatible.
- `MRR-REQ-008` The new list is a read-only control-plane feature. It MUST NOT
  create or mutate research/runs, send SQS messages, drain workers, call
  providers, alter leases, or read S3 artifacts.
- `MRR-REQ-009` The new backend and BFF `GET /api/keyword-research` endpoints
  MUST reject unknown, duplicate, non-positive, non-integer, or over-limit
  pagination parameters with the safe contract in A3.
- `MRR-REQ-010` The BFF MUST preserve the existing Neon-auth session flow and
  pass only the authenticated user ID through the trusted backend header seam.
  Anonymous requests return the existing safe authentication-required result.
- `MRR-REQ-011` Personalized list responses MUST remain uncached and carry
  `Cache-Control: no-store` through the existing backend/BFF behavior.
- `MRR-REQ-012` `/runs` MUST retain the current page shell and responsive run
  history design, adding explicit “Keyword research” and “Discovery runs”
  sections with accessible labels and independently announced loading/errors.
- `MRR-REQ-013` No Prisma schema or migration is permitted. Existing
  `KeywordResearch.ownerId`, `KeywordResearch.runs`, stage rows, and indexes are
  sufficient.
- `MRR-REQ-014` Existing keyword dashboard polling, selection persistence,
  handoff atomicity, landing/auth flow, worker contracts, and AWS pipeline
  behavior MUST remain unchanged.
- `MRR-REQ-015` After the resume feature is complete, repair the four proven
  stale keyword-intelligence test surfaces named in A3. Test expectations and
  fixtures MUST match the already-committed current contracts without changing
  production behavior, deleting coverage IDs, weakening strict fields that
  remain authoritative, or relabelling a product failure as expectation drift.

## Exact user-visible policy

Research title is derived from normalized durable seeds: show the first two
joined by ` · `; when more exist append ` +N more`. Empty/malformed seeds fail
strict response parsing and show the research-section safe error; the client
does not invent a fallback title.

Research badges map exactly:

| Durable state | Badge | Activity |
|---|---|---|
| `queued` | `Queued` | `Waiting to start keyword research` |
| `running` | `Running` | stage label from A3 |
| `completed`, revision `0` | `Ready to review` | `Keyword results are ready to review` |
| `completed`, revision `>=1` | `Selection saved` | `Your saved shortlist is ready to continue` |
| `failed` | `Failed` | `Keyword research stopped before completion` |

The page-level empty card appears only after both first pages load successfully
and both totals are zero. If only research is empty, its section shows a compact
empty message while runs remain visible; the inverse applies to runs.

## Retention and compatibility

This feature neither changes retention nor deletes data. Historical research
without a run becomes visible. Historical research with a run remains reachable
through that run and is deliberately excluded from the research section.

## Authorization and deployment boundary

This package authorizes planning and future local implementation/testing only.
It does not authorize deployment, database migration, AWS mutation, provider
calls, production data access, commit, push, or modification of the workspace's
AWS coordination state.

## Explicit exclusions

- No unified cross-table cursor or single mixed pagination stream.
- No research cancellation, deletion, archival, retry button, or worker repair.
- No autosave for unsaved browser selection drafts.
- No change to `/keywords/{researchId}` or `/runs/{runId}` behavior.
- No change to auth pages, landing page, workers, queues, artifacts, or schema.
- No production-code change is permitted in the stale-test correction window;
  a failure not explained by the four source-grounded contract changes in A3
  stops that window for diagnosis and correction planning.
