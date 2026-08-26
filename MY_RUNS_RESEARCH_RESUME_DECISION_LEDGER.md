# My Runs Research Resume — Decision Ledger (A3)

Status: `LOCKED`

Companions: A1 `MY_RUNS_RESEARCH_RESUME_PRODUCT_CONTRACT.md`; A2
`MY_RUNS_RESEARCH_RESUME_DISCOVERY_DOSSIER.md`; A4
`MY_RUNS_RESEARCH_RESUME_EXECUTION_CHECKLIST.md`; A5
`MY_RUNS_RESEARCH_RESUME_ACTIVE_STATE.md`; A6
`MY_RUNS_RESEARCH_RESUME_EVIDENCE.md`; A7
`MY_RUNS_RESEARCH_RESUME_CHANGELOG.md`; A8
`MY_RUNS_RESEARCH_RESUME_TRACEABILITY.md`.

## Locked decisions

| ID | Requirements | Locked choice | Evidence | Rejected alternatives | Consequence |
|---|---|---|---|---|---|
| `MRR-DEC-001` | 001,004,007 | Keep `/api/runs` byte-compatible; add a separate research collection endpoint and compose both on `/runs`. | SRC-002,003,006,007 | mixed union response; cross-table cursor | Existing run consumers and pagination remain stable. |
| `MRR-DEC-002` | 001,004 | Backend research filter is exactly `{ ownerId, runs: { none: {} } }`. | SRC-001,010 | list all then client-dedupe; handoff flag | Foreign and handed-off research never enters response or total. |
| `MRR-DEC-003` | 003 | Add `serializeKeywordResearchSummary`; extract the existing stage derivation into one private helper used by full and summary serializers. | SRC-008,009 | full serializer/list response; duplicate derivation | Full research envelope remains byte-compatible; list never selects result/config/selection. |
| `MRR-DEC-004` | 003,009 | `GET /api/keyword-research?page=1&pageSize=20`, page max 100, only `page` and `pageSize`, decimal ASCII positive integers without signs/fractions/whitespace. | SRC-003,006 | cursor pagination; unbounded list | Mirrors existing run pagination while keeping independent state. |
| `MRR-DEC-005` | 005,010 | Auth identity is frontend session user → trusted backend `x-user-id` seam → repository `ownerId` predicate on count and rows. | SRC-003,006 | cookie-readable client identity; post-filtering | Foreign rows and totals are indistinguishable from absence. |
| `MRR-DEC-006` | 006,012 | Keep `RunHistory`; add two independent effects/controllers/state machines and two independently paginated sections. | SRC-007,013 | `Promise.all`; new page; merged page index | One failed list does not hide or refetch the other. |
| `MRR-DEC-007` | 002 | Client derives research links from strict IDs using fixed `/keywords/${encodeURIComponent(id)}`. | SRC-005 | backend URL/destination | Navigation cannot be redirected by payload data. |
| `MRR-DEC-008` | 008,013,014 | No schema, worker, queue, S3, provider, dashboard, auth, landing, or handoff edits. | SRC-001,005,010,015 | premature Run creation; dashboard rewrite | Change is read-only and resumes existing durable work. |
| `MRR-DEC-009` | 011 | Backend `sendJson` and BFF response remain `no-store`; no `use cache`, cache tags, or static route config. | SRC-012,014 | personalized cache | Every page visit sees current owner state. |
| `MRR-DEC-010` | 004,006 | Research and run sections have independent totals/pages; handed-off research disappears on the next research-list fetch and its run remains. | SRC-002,010 | atomic mixed snapshot | Transient cross-request movement is allowed; duplicate rows are forbidden within one rendered response. |
| `MRR-DEC-011` | 007,012 | Preserve existing run row markup/behavior; append narrowly scoped research history classes to `globals.css` and update page copy to “My searches”. | SRC-007,015 | redesign; new route | Existing responsive run layout remains recognizable. |
| `MRR-DEC-012` | 001-015 | Three sequential windows: backend contract/persistence, frontend composition/emitted-browser proof, then test-only stale-contract correction. | SRC-001-019 | single broad window; mixing unrelated stale tests into feature edits | W2 consumes W1; W3 runs only after feature files freeze and may edit tests only. |
| `MRR-DEC-013` | 015 | W3 changes exactly four test files: frontend `test/keyword-intelligence-api.test.ts`; backend `test/keyword-intelligence-api.test.js`, `test/keyword-intelligence-query-mapper.test.js`, and `test/keyword-intelligence-worker-flow.test.js`. | SRC-016-019 | weaken production parsers; restore removed product restrictions; edit production code | Existing registries/IDs remain; assertions and synthetic seams move to current contracts. |
| `MRR-DEC-014` | 015 | Frontend W5-A06 accepts history lengths 0, 14, and 103 while retaining strict point/date/numeric/unknown-key checks. Backend API/component tests inject a deterministic classifier returning exactly ordered `{itemId,product}` values, mapping tests drive `product` directly, editable-query tests retain only current rejection partitions, and worker `overviewResponse` nests `monthly_searches` inside `keyword_info`. | SRC-016-018 | remove tests; call OpenAI; invent provider aliases | Tests become deterministic and contract-faithful without production edits or external calls. |
| `MRR-DEC-015` | 015 | W3 first runs the four focused files, then full frontend/backend suites. Any remaining failure must be diagnosed: only a mechanically traced stale fixture/assertion may be corrected inside the four-file scope; a production defect or fifth-file requirement stops and escalates. | SRC-016-019 | make all failures pass by changing expectations; expand scope ad hoc | Test repair cannot conceal regressions. |

## Exact payload contract: `keyword-research-history-v1`

Success response has exact keys and no discriminator aliases:

```json
{
  "pagination": {
    "page": 1,
    "pageSize": 20,
    "totalItems": 1,
    "totalPages": 1
  },
  "items": [
    {
      "researchId": "kr_abcdefghijklmnopqrstuvwx",
      "seeds": ["independent eyewear"],
      "state": "running",
      "stage": "anchor_screen",
      "selectionRevision": 0,
      "createdAt": "2026-08-26T12:00:00.000Z",
      "updatedAt": "2026-08-26T12:05:00.000Z",
      "completedAt": null
    }
  ]
}
```

Exact bounds:

- `researchId`: `^kr_[A-Za-z0-9_-]{24}$`.
- `seeds`: array length 1–5; each normalized string 1–100 Unicode code points.
- `state`: `queued | running | completed | failed`.
- `stage`: `queued | expansion | anchor_screen | market_overview | finalizing | completed | failed`.
- `selectionRevision`: safe integer `>=0`.
- timestamps: ISO timestamps; `completedAt` is ISO or `null`.
- pagination fields: safe nonnegative integers, with page/pageSize positive;
  `totalPages = ceil(totalItems/pageSize)`, including `0` when total is zero.
- Top-level, pagination, and item unknown keys are rejected.

Summary serialization uses the existing latest-generation stage map. State
`completed` forces stage `completed`; `failed` forces `failed`; no stages means
`queued`; otherwise the first incomplete stage in
`expansion → anchor_screen → market_overview` is returned, or `finalizing`.

## Repository algorithm

`listOwnerWorkspaceResearch({ownerId,page,pageSize})` validates all inputs and
executes one short interactive transaction:

1. `where = { ownerId, runs: { none: {} } }`;
2. count with exactly that `where`;
3. find at `skip=(page-1)*pageSize`, `take=pageSize`;
4. order `createdAt DESC`, then `id DESC`;
5. select only ID, seeds, state, selectionRevision, created/updated/completed
   timestamps, and stage fields needed by the shared stage derivation;
6. return `{totalItems,items}`.

At PostgreSQL `READ COMMITTED`, a concurrent atomic handoff may make the count
temporarily greater than the returned item count, but cannot expose a foreign
row or a handed-off item. The next independent fetch converges. The UI MUST use
the returned values without inventing rows and MUST tolerate an empty page with
a positive transient total.

## Failure contract

- Invalid query: HTTP 400, code `INVALID_QUERY_PARAMETERS`, message
  `One or more keyword-research list query parameters are invalid.`
- Anonymous BFF: existing HTTP 401 `AUTHENTICATION_REQUIRED`.
- Auth unavailable: existing HTTP 503 `AUTH_UNAVAILABLE`.
- Backend/upstream failure: existing safe proxy result; other section remains.
- Malformed 2xx: strict client parser raises existing invalid-data error for
  the research section only.

## Enforcement decisions

Adding the repository transaction changes the pinned repository inventory from
19/9/10 to exactly 20 total, 10 short, 10 scale; add
`listOwnerWorkspaceResearch` to the short partition and mechanically replace
the full-file SHA after W1 freezes. Preserve all historical cases and mutation
controls.

## Accepted-test invalidation rules

W3 supersedes only assertions contradicted by `MRR-SRC-016` through
`MRR-SRC-018`. It MUST preserve all existing case IDs, registry membership,
execution certificates, negative controls, strict unknown-key and scalar
validation, row-set identity enforcement, maximum row/query bounds, and worker
call/object-count oracles. The deterministic classifier fake reproduces the
production classifier's ordered one-result-per-item surface but supports no
claim about OpenAI transport or semantic model quality. The synthetic
DataForSEO response reproduces the current consumed nested field path; provider
contract fidelity remains owned by the existing adapter fixture tests.
