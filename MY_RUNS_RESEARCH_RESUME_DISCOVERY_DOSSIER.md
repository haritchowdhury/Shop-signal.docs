# My Runs Research Resume — Discovery Dossier (A2)

Status: `OBSERVED / 2026-08-26`

Companions: A1 `MY_RUNS_RESEARCH_RESUME_PRODUCT_CONTRACT.md`; A3
`MY_RUNS_RESEARCH_RESUME_DECISION_LEDGER.md`; A4
`MY_RUNS_RESEARCH_RESUME_EXECUTION_CHECKLIST.md`; A5
`MY_RUNS_RESEARCH_RESUME_ACTIVE_STATE.md`; A6
`MY_RUNS_RESEARCH_RESUME_EVIDENCE.md`; A7
`MY_RUNS_RESEARCH_RESUME_CHANGELOG.md`; A8
`MY_RUNS_RESEARCH_RESUME_TRACEABILITY.md`.

Every source below is current working-tree evidence. No live, production,
provider, AWS, secret, or customer-data probe was performed.

```yaml
- evidence_id: MRR-SRC-001
  classification: OBSERVED
  claim: KeywordResearch has ownerId and a Run[] relation; Run has nullable keywordResearchId.
  source: email_scraper/prisma/schema.prisma models Run and KeywordResearch
  observed_at: 2026-08-26
  environment: local workspace
  limitations: source schema only; no production row claim
  privacy: no row data read

- evidence_id: MRR-SRC-002
  classification: OBSERVED
  claim: Existing run history is owner-scoped, sorted createdAt DESC then id DESC, and paginated with count plus findMany.
  source: email_scraper/src/prisma-run-repository.js PrismaRunRepository.listRuns
  observed_at: 2026-08-26
  environment: local workspace
  limitations: no latency measurement
  privacy: source only

- evidence_id: MRR-SRC-003
  classification: OBSERVED
  claim: Backend GET /api/runs authenticates with trustedUserId, parses page/pageSize, and serializes Run rows.
  source: email_scraper/src/server.js parseRunListPagination and GET /api/runs
  observed_at: 2026-08-26
  environment: local workspace
  limitations: local contract inspection
  privacy: source only

- evidence_id: MRR-SRC-004
  classification: OBSERVED
  claim: No owner-scoped keyword-research collection/list method or GET collection route currently exists.
  source: negative rg searches for keywordResearch.findMany, listResearch, and GET /api/keyword-research
  observed_at: 2026-08-26
  environment: local workspace
  limitations: current working tree only
  privacy: source only

- evidence_id: MRR-SRC-005
  classification: OBSERVED
  claim: The keyword dashboard GETs durable research on mount, polls queued/running state, and restores persisted selection revision.
  source: frontend/components/keyword-intelligence/research-dashboard.tsx and research-status.tsx
  observed_at: 2026-08-26
  environment: local workspace
  limitations: browser population not measured
  privacy: source only

- evidence_id: MRR-SRC-006
  classification: OBSERVED
  claim: Frontend /api/keyword-research currently owns POST only; /api/runs GET shows the established auth/query forwarding pattern.
  source: frontend/app/api/keyword-research/route.ts and frontend/app/api/runs/route.ts
  observed_at: 2026-08-26
  environment: Next.js 16.2.12 local source
  limitations: emitted artifact covered only by planned build/browser gate
  privacy: source only

- evidence_id: MRR-SRC-007
  classification: OBSERVED
  claim: RunHistory is a client component with one run page state, one fetch effect, strict parser, existing rows, and run pagination.
  source: frontend/components/run-history.tsx
  observed_at: 2026-08-26
  environment: local workspace
  limitations: current responsive behavior inferred only where existing tests assert it
  privacy: source only

- evidence_id: MRR-SRC-008
  classification: OBSERVED
  claim: Keyword full serialization includes completed result and selection material and is therefore unsuitable as a list response.
  source: email_scraper/src/api-serializer.js serializeKeywordResearch
  observed_at: 2026-08-26
  environment: local workspace
  limitations: no production payload-size measurement
  privacy: source only

- evidence_id: MRR-SRC-009
  classification: OBSERVED
  claim: Keyword stage display is deterministically derived from durable state and latest stage generations in serializeKeywordResearch.
  source: email_scraper/src/api-serializer.js serializeKeywordResearch
  observed_at: 2026-08-26
  environment: local workspace
  limitations: source derivation only
  privacy: source only

- evidence_id: MRR-SRC-010
  classification: OBSERVED
  claim: Keyword-to-run handoff creates the Run and handoff inside one repository transaction and links keywordResearchId.
  source: email_scraper/src/keyword-intelligence/repository.js PrismaKeywordResearchRepository.createRun
  observed_at: 2026-08-26
  environment: local workspace
  limitations: integration proof is an execution-window obligation
  privacy: source only

- evidence_id: MRR-SRC-011
  classification: OBSERVED
  claim: Repository enforcement pins keyword repository bytes and exactly 19 _transaction sites, nine short and ten scale.
  source: email_scraper/test/keyword-intelligence-repository.test.js SCN_KI_043
  observed_at: 2026-08-26
  environment: local test source
  limitations: future repository edit mechanically changes the hash and inventory
  privacy: source only

- evidence_id: MRR-SRC-012
  classification: OBSERVED
  claim: Next Route Handlers are uncached by default, GET and POST may coexist, and request/cookie access makes the handler request-time dynamic.
  source: frontend/node_modules/next/dist/docs/01-app/01-getting-started/15-route-handlers.md sha256 b2cffc8116b25978f5ec03ea18577550b2a6dc11a49b9dc68892bfa42464cfd0
  observed_at: 2026-08-26
  environment: installed Next.js 16.2.12 docs
  limitations: documentation, not emitted proof
  privacy: N/A

- evidence_id: MRR-SRC-013
  classification: OBSERVED
  claim: Independent client fetches should start independently; Promise.all failure would couple them, while separate effects preserve partial success.
  source: installed fetching-data and server/client component docs plus current RunHistory client pattern
  observed_at: 2026-08-26
  environment: installed Next.js 16.2.12 docs
  limitations: design evidence; behavioral proof remains planned
  privacy: N/A

- evidence_id: MRR-SRC-014
  classification: OBSERVED
  claim: Cache Components are not enabled in frontend/next.config.ts.
  source: frontend/next.config.ts
  observed_at: 2026-08-26
  environment: local workspace
  limitations: current config only
  privacy: N/A

- evidence_id: MRR-SRC-015
  classification: OBSERVED
  claim: Both nested repositories were clean at plan freeze; the coordination root retains its owner-controlled relocation state and the new plan documents are unstaged.
  source: git status --short in root, email_scraper, and frontend
  observed_at: 2026-08-26
  environment: local workspace
  limitations: status can change before assignment and must be re-recorded
  privacy: filenames only

- evidence_id: MRR-SRC-016
  classification: OBSERVED
  claim: Frontend W5-A06 still rejects 0-14 and greater-than-102 monthly-history rows although the current parser accepts any array length and still validates every point strictly.
  source: frontend/lib/keyword-intelligence-validation.ts monthlyHistory; frontend/test/keyword-intelligence-api.test.ts W5-A06; focused test output 2026-08-26
  observed_at: 2026-08-26
  environment: local workspace
  limitations: test-only contract drift; no browser claim
  privacy: source and synthetic fixture only

- evidence_id: MRR-SRC-017
  classification: OBSERVED
  claim: Query mapping now uses AI-produced item.product, defaults absent product to false/store scope, and intentionally permits arbitrary nonempty edited text subject only to row identity, 200-codepoint, control-character, duplicate, and cardinality checks; old lane, grammar, and relevance assertions fail.
  source: email_scraper/src/keyword-intelligence/query-intent-classifier.js; src/keyword-intelligence/query-mapper.js; test/keyword-intelligence-api.test.js; test/keyword-intelligence-query-mapper.test.js; focused test output 2026-08-26
  observed_at: 2026-08-26
  environment: local workspace and localhost rerun
  limitations: AI transport is replaced by a deterministic contract-faithful test seam; no provider call
  privacy: source and synthetic fixture only

- evidence_id: MRR-SRC-018
  classification: OBSERVED
  claim: The current DataForSEO adapter reads monthly_searches from keyword_info, while the worker-flow fixture still emits it at the obsolete item top level, producing empty history and a downstream null trendSlope rejection.
  source: email_scraper/src/aws-pipeline/keyword-intelligence/dataforseo-labs-adapter.js normalizeOverviewMetrics; test/keyword-intelligence-worker-flow.test.js overviewResponse; focused test output 2026-08-26
  observed_at: 2026-08-26
  environment: local component test
  limitations: synthetic provider response only; no paid call
  privacy: synthetic fixture only

- evidence_id: MRR-SRC-019
  classification: OBSERVED
  claim: Current full-suite baseline is frontend 21/22 files with only keyword-intelligence-api failing; backend exits nonzero with stale API/query-mapper/worker-flow failures, while localhost-only cases pass when the identical focused API suite is rerun with local sandbox escalation.
  source: npm test in frontend; npm test and escalated node test/keyword-intelligence-api.test.js in email_scraper, 2026-08-26
  observed_at: 2026-08-26
  environment: local workspace
  limitations: diagnostic pre-change run, not acceptance evidence
  privacy: no secrets or external calls
```

## Payload evidence certificate

| Payload ID | Producer → consumer | Exact shape authority | Unknown fields | Privacy |
|---|---|---|---|---|
| `MRR-PAY-001` backend research-list success | backend server → frontend BFF → client parser | A3 §Payload contract | reject at client; backend produces exact keys | summary only; forbids result/config/selection/artifacts |
| `MRR-PAY-002` pagination query | browser → BFF → backend | A3 §Pagination | reject unknown/duplicate | no private data |
| `MRR-PAY-003` safe error | backend/BFF → browser | existing `jsonError`/ApiError envelope | existing strict client error path | no owner IDs or foreign counts |

There are zero blocking payload unknowns. All new fields are product-owned
outputs derived from existing durable fields; no external payload is consumed.

## Scale inventory

Hard page size is 100; default is 20. Each research-list request performs one
count and one bounded `findMany`, selects at most 100 summary rows and stage
counters, reads no result JSON, and performs zero external calls. Initial
`/runs` page load performs two independent BFF GETs; no sequential dependency
exists between them.
