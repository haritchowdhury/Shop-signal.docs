# My Runs Research Resume — Execution Checklist (A4)

Status: `READY / UNASSIGNED / PLAN-ONLY`

Companions: A1 `MY_RUNS_RESEARCH_RESUME_PRODUCT_CONTRACT.md`; A2
`MY_RUNS_RESEARCH_RESUME_DISCOVERY_DOSSIER.md`; A3
`MY_RUNS_RESEARCH_RESUME_DECISION_LEDGER.md`; A5
`MY_RUNS_RESEARCH_RESUME_ACTIVE_STATE.md`; A6
`MY_RUNS_RESEARCH_RESUME_EVIDENCE.md`; A7
`MY_RUNS_RESEARCH_RESUME_CHANGELOG.md`; A8
`MY_RUNS_RESEARCH_RESUME_TRACEABILITY.md`.

This checklist is future local execution authority only after A5 names an
assigned agent and pins unchanged hashes. It never authorizes deployment,
provider calls, AWS/production mutation, database migration, commit, or push.

## Dependency DAG and stop policy

`MRR-W1 → MRR-W2 → MRR-W3 → STOP / independent review`

The requester explicitly assigned the continuous `MRR-W1 → MRR-W2 → MRR-W3`
sequence before freeze. A5 names all three windows and the same root agent;
W1/W2 may start their named successor only after their complete acceptance and
evidence/state transition. No implementation box below is checked at authoring
time; mutable progress is recorded only in A5/A6.

## MRR-W1 — Owner-scoped research-list backend contract

```yaml
window_id: MRR-W1
objective: Expose a strict, lightweight, owner-scoped list of research with no Run.
depends_on: []
consumes: A1-A3 contracts; existing auth, serializer, API, repository and server seams
produces: keyword-research-history-v1 backend response and W1 enforcement certificate
assigned_agent_policy: explicit_multi_window
authorized_write_scope:
  - email_scraper/src/api-serializer.js: stage derivation helper and serializeKeywordResearchSummary
  - email_scraper/src/keyword-intelligence/repository.js: listOwnerWorkspaceResearch
  - email_scraper/src/keyword-intelligence/api.js: listResearch input/method
  - email_scraper/src/server.js: GET collection route and pagination parser
  - email_scraper/test/fixtures/keyword-research-history-v1.json: exact positive fixture
  - email_scraper/test/keyword-research-history.test.js: W1 registry/component tests
  - email_scraper/test/keyword-intelligence-repository.test.js: transaction inventory/hash enforcement only
shared_file_scope:
  - api-serializer.js: preserve serializeKeywordResearch output while sharing stage derivation
  - api.js: add listResearch only; preserve create/claim/get/save/handoff/export
  - server.js: add GET /api/keyword-research only; preserve POST and item routes
read_only_scope:
  - email_scraper/prisma/schema.prisma
  - email_scraper/src/prisma-run-repository.js
  - email_scraper/test/keyword-research-intent*.test.js
  - all AWS pipeline, provider and migration files
authorized_actions:
  - local source edits in exact scope
  - local unit/component tests, npm test, check:secrets, db:generate and db:validate
  - local sandbox escalation for identical localhost/toolchain commands
prohibited_actions:
  - schema/migration or database-row mutation
  - SQS/S3/provider/AWS/production/deployment/commit/push
  - frontend edits or W2/W3 work
successor: MRR-W2
successor_reserved_for: current root assignment
may_start_successor: true
```

### Preconditions

- [ ] `MRR-W1-P1` A5 assigns W1 and pinned standard/A1/A3/A4 hashes match. Evidence: ___
- [ ] `MRR-W1-P2` A1-A3 and the 23-member A8 coverage set are unchanged. Evidence: ___
- [ ] `MRR-W1-P3` Node/npm and installed Prisma dependencies are available; no database URL is required. Evidence: ___
- [ ] `MRR-W1-P4` Record nested-repository status and preserve all pre-existing changes. Evidence: ___

### Task blocks

#### `MRR-W1-T1` Repository projection and exclusion

1. Requirements/decisions: REQ-001,003-005,008,013; DEC-002-005,008,010.
2. Source anchor: `PrismaKeywordResearchRepository` and Prisma models in SRC-001/010/011.
3. Target anchor: add `listOwnerWorkspaceResearch({ownerId,page,pageSize})` beside owner-read methods.
4. Interface: strict object; nonempty `ownerId`; safe positive integer `page`; `pageSize` 1-100; returns `{totalItems,items}`.
5. Algorithm: validate before I/O; form exactly `{ownerId,runs:{none:{}}}`; in one short `$transaction`, count then bounded findMany; skip `(page-1)*pageSize`; order `createdAt desc,id desc`; select only A3 summary/stage fields.
6. Operation order: one transaction, one count, one findMany; zero writes/external calls.
7. Boundary class: short read transaction at READ COMMITTED; no recovery protocol or retry.
8. Identity/time: owner ID from authenticated caller; research ID/durable timestamps unchanged; no new key/fingerprint/clock.
9. Failure/concurrency: invalid input fails before transaction; Prisma failure propagates safely; concurrent handoff may cause transient count/list mismatch but never foreign/handed-off rows; duplicates/restarts/cancellation have no side effect.
10. Bounds/config: defaulting is caller-owned; repository max 100, exactly one page, no timeout/provider/batch.
11. Callers/preservation: only W1-T3 list API calls it; preserve every existing repository method and handoff transaction.
12. Tests: MRR-DB-01/02 and BE-04 in explicit registry; witnesses captured Prisma calls; assertions exact predicates/order/projection/counts; NC-01/02/03.
13. Output consumer: W1-T3.
14. Non-goals: no schema/index/migration, result read, worker/queue/artifact/provider access.
15. Mechanical output: method plus 20/10/10 transaction inventory and refreshed exact repository SHA.

- [ ] `MRR-W1-T1` Implement the repository method and enforcement update exactly above.

#### `MRR-W1-T2` Lightweight serializer

1. Requirements/decisions: REQ-001,003,007; DEC-003.
2. Source: `serializeKeywordResearch` stage logic in SRC-008/009.
3. Target: private shared stage helper plus exported `serializeKeywordResearchSummary` in `api-serializer.js`.
4. Interface: exact eight-key item schema in A3.
5. Algorithm: derive latest-generation stage using existing order; validate/emit seeds, state, revision and timestamps; force terminal stages; emit no other key.
6. Operations: pure CPU; zero durable/external operations.
7. Boundary: pure recovered-by-recompute function.
8. Identity/time: pass durable ID/timestamps without generation or fallback.
9. Failures: malformed required material fails closed; no retry/concurrency/restart/cancellation effect.
10. Bounds: seeds 1-5, 1-100 codepoints; stage/state/revision/timestamps per A3.
11. Callers: new list API; existing full serializer reuses helper and remains byte-compatible.
12. Tests: BE-01/02; exact fixture deep equality, full serializer parity; NC-03/06.
13. Output: W1-T3 payload items.
14. Non-goals: no full result/config/selection serialization change.
15. Mechanical output: one new export and one private helper.

- [ ] `MRR-W1-T2` Implement the summary serializer and full-serializer parity.

#### `MRR-W1-T3` API method and pagination

1. Requirements/decisions: REQ-001,003,005,009; DEC-004/005.
2. Source: `createKeywordResearchApi`, `parseRunListPagination` behavior.
3. Target: strict `listResearch` input schema/method in keyword API and research pagination parser in server.
4. Interface: `{ownerId,page?,pageSize?}` normalized to page 1/pageSize 20; exact A3 response.
5. Algorithm: reject unknown fields/non-ASCII-decimal/sign/fraction/whitespace/duplicate query values; call repository once; serialize each returned row; compute totalPages.
6. Operations: repository read once; zero writes/external calls.
7. Boundary: request-scoped read; safe error mapping, no retry.
8. Identity/time: owner passed unchanged; no client-provided owner.
9. Failures: invalid → exact 400; repository error → existing safe 500; repeat/restart idempotent; cancellation aborts request only.
10. Bounds: page safe positive integer; pageSize 1-100; default 1/20.
11. Callers: W1-T4; preserve every existing keyword API method.
12. Tests: BE-01/03/05; query partition table and strict response; NC-01/06.
13. Output: W1-T4 route response.
14. Non-goals: no POST/item-route/handoff changes.
15. Mechanical output: one API method and one parser.

- [ ] `MRR-W1-T3` Implement listResearch and exact pagination validation.

#### `MRR-W1-T4` Backend GET collection route and registry

1. Requirements/decisions: REQ-001,005,008-011; DEC-001/005/009.
2. Source: backend `/api/runs`, trustedUserId, sendJson and keyword route ordering.
3. Target: `GET /api/keyword-research` exact collection match before item routes.
4. Interface: page/pageSize query → A3 200 or A3 safe error.
5. Algorithm: authenticate; parse query; call `keywordResearchApi.listResearch`; send exact JSON/no-store.
6. Operations: one API call; zero writes/SQS/S3/provider.
7. Boundary: HTTP request; existing centralized safe-error recovery.
8. Identity/time: trusted header identity only; response durable timestamps only.
9. Failures: absent/invalid auth follows existing backend policy; invalid query 400; duplicate/replay read-only; disconnect makes no durable change.
10. Bounds: existing request/server bounds; no body.
11. Callers: frontend BFF in W2; preserve POST collection and all item routes.
12. Tests: BE-01/03/04/05 and REG-01; localhost component route witness; NC-01/06.
13. Output: frozen `keyword-research-history-v1` for W2.
14. Non-goals: no public anonymous list.
15. Mechanical output: one method/path branch and explicit registry certificate.

- [ ] `MRR-W1-T4` Add the authenticated GET route and executable W1 registry.

### W1 coverage matrix

| Case | Scenario / req / dec | Path and starting partition | Action and activation witness | Expected result / operations / forbidden | Control / parity / registration |
|---|---|---|---|---|---|
| `MRR-BE-01` | normal list; 001,011; 003,009 | GET collection; owner has queued/running/completed/failed unhanded rows | GET page 1; route/API/repository/serializer call counters | exact fixture, latest-stage labels, no-store; 1 txn/2 reads; no writes/external | NC-06; component; W1 registry `BE-01` |
| `MRR-BE-02` | privacy projection; 003; 003 | serializer/list with completed result/config/selection present durably | serialize selected projection; selected-key witness | exact eight item keys; result/config/selection/provider/artifact absent | NC-03; unit; W1 registry `BE-02` |
| `MRR-BE-03` | auth/owner; 005,010; 005 | anonymous, owner A, foreign B | anonymous GET then owner GET; trustedUserId/predicate witnesses | auth-safe error then only A rows/total; no B existence signal | NC-01; component; W1 registry `BE-03` |
| `MRR-BE-04` | read-only ceiling; 008; 008 | representative 20 and maximum 100 pages | invoke both; Prisma call/projection counters | exactly 1 transaction+2 reads/request; bounded take; zero create/update/delete/SQS/S3/provider | NC-03; component; W1 registry `BE-04` |
| `MRR-BE-05` | query partitions; 009; 004 | absent/default, boundaries, unknown/duplicate/sign/fraction/space/overflow | table-drive parser+route; per-member activation | valid normalize exactly; invalid exact 400 before repository | NC-06; unit/component; W1 registry `BE-05` |
| `MRR-DB-01` | owner totals; 005; 002,005 | fake Prisma contains conceptual A/B rows | inspect count/findMany args and returned partition | identical owner predicate in both; foreign absent from item and total | NC-01; component substitute; W1 registry `DB-01` |
| `MRR-DB-02` | handoff exclusion/concurrency; 004; 002,010 | one unhanded, one linked; injected count→find transition | capture where/order and simulate empty page/positive total | both reads include runs.none; transient mismatch accepted; no duplicate | NC-02; component substitute; W1 registry `DB-02` |

Substitute fidelity: the W1 Prisma fake implements only `$transaction`,
`keywordResearch.count`, and `keywordResearch.findMany`, records order/args,
and returns injected rows. It proves call shape, ordering, projection and
read-only cardinality, not PostgreSQL isolation. Schema relation validity is
proved by `prisma validate`; the accepted concurrency claim is deliberately
limited to the documented READ COMMITTED transient mismatch.

### Verification and handoff

- [ ] `MRR-W1-V1` Run `node test/keyword-research-history.test.js`; all seven W1 cases register/execute with witnesses and NC-01/02/03/06 falsify.
- [ ] `MRR-W1-V2` Run `npm run db:generate`, `npm run db:validate`, `npm run check:secrets`, then `npm test`; no required MRR skip/failure and existing guarded integrations retain their declared skips.
- [ ] `MRR-W1-V3` Assert 20 total/10 short/10 scale repository transactions, new exact SHA, one transaction/two bounded reads, take <=100.
- [ ] `MRR-W1-V4` Assert owner/runs predicates and forbidden payload/operation sets.
- [ ] `MRR-W1-V5` Recompute required=registered=executed W1 case set, zero skips/duplicates/unexpected/unactivated, matching global digest subset record.
- [ ] `MRR-W1-H1` Append exact changed files/symbols and `migrations: []` to A6. Evidence: ___
- [ ] `MRR-W1-H2` Append commands/outcomes/cases/skips/controls. Evidence: ___
- [ ] `MRR-W1-H3` Diff matches W1 write scope. Evidence: ___
- [ ] `MRR-W1-H4` No W2/W3 or prohibited action started. Evidence: ___
- [ ] `MRR-W1-H5` Append certificates and atomically advance A5 to assigned W2. Evidence: ___
- [ ] `MRR-W1-H6` Begin W2 only after W1 acceptance and A5 transition.

## MRR-W2 — Authenticated My Searches composition and resume navigation

```yaml
window_id: MRR-W2
objective: Render independent research and run sections on /runs and resume research at /keywords/{id}.
depends_on: [MRR-W1 accepted]
consumes: frozen keyword-research-history-v1 backend contract
produces: authenticated two-section workspace and emitted-browser certificate
assigned_agent_policy: explicit_multi_window
authorized_write_scope:
  - frontend/app/api/keyword-research/route.ts: GET export only
  - frontend/lib/keyword-research-history.ts: new types/query/parser/presentation helpers
  - frontend/components/run-history.tsx: independent research and run state/rendering
  - frontend/app/runs/page.tsx: title/copy only
  - frontend/app/globals.css: narrowly prefixed research-history styles only
  - frontend/test/my-runs-research-resume.test.ts: W2 unit/component registry
  - frontend/test/design-system-shell.test.ts: exact My searches shell assertion only
  - frontend/test/browser/my-runs-research-resume.mjs: emitted browser registry
shared_file_scope:
  - keyword-research route: add GET; preserve POST landing/auth intent path byte-for-byte
  - run-history: preserve run functions/markup and add research controller/section
  - globals.css: append .research-history-* and required section layout only
read_only_scope:
  - frontend/app/api/runs/route.ts
  - frontend/components/keyword-intelligence/research-dashboard.tsx
  - frontend/app/keywords/[researchId]/page.tsx
  - all backend, auth, landing, pending-intent and worker files
authorized_actions:
  - local edits in scope; lint/unit/build; local Next server and headless Chrome
  - local sandbox escalation for identical build/localhost/headless commands
prohibited_actions:
  - backend/W1/W3 edits; auth/landing/dashboard/handoff edits
  - external network, provider, AWS, production, deployment, commit or push
successor: MRR-W3
successor_reserved_for: current root assignment
may_start_successor: true
```

### Preconditions

- [ ] `MRR-W2-P1` A5 assigns W2; pins match; W1 is independently accepted. Evidence: ___
- [ ] `MRR-W2-P2` W1 fixture and seven-case certificate are present and unchanged. Evidence: ___
- [ ] `MRR-W2-P3` Next dependencies and `/usr/bin/google-chrome` exist; ports are free. Evidence: ___
- [ ] `MRR-W2-P4` Record frontend status and preserve pre-existing changes. Evidence: ___

### Task blocks

#### `MRR-W2-T1` BFF GET and strict history parser

1. Requirements/decisions: REQ-003,005,009-011; DEC-004/005/009.
2. Source: POST-only keyword route and run GET proxy in SRC-006.
3. Target: GET export in route; new server/client-safe `keyword-research-history.ts`.
4. Interface: exact A3 query and payload; exported types, strict parser, fixed error behavior.
5. Algorithm: authenticate; reject unknown/duplicate query; forward only page/pageSize with userId/10s timeout; strict-parse exact keys/types/invariants in client.
6. Operations: one session read, one backend proxy GET; no body/write.
7. Boundary: request BFF; existing safe proxy errors; no retry/cache.
8. Identity/time: session user only; fixed research ID regex/ISO timestamps.
9. Failure: 401/503/query 400/upstream errors exact; malformed 2xx becomes research-only error; abort harmless.
10. Bounds: page 1+, pageSize 1-100, default browser request 20.
11. Callers: W2-T2; POST export and pending-auth cookies preserved exactly.
12. Tests: FE-01/06,E2E-03; GET/POST coexistence and strict mutations; NC-06.
13. Output: typed list consumed by RunHistory.
14. Non-goals: no POST/auth/cookie/landing modification.
15. Mechanical output: one GET export plus one new library.

- [ ] `MRR-W2-T1` Add the authenticated GET proxy and strict parser.

#### `MRR-W2-T2` Two independent list controllers

1. Requirements/decisions: REQ-001,004,006,012; DEC-006/010.
2. Source: one-controller `RunHistory` in SRC-007.
3. Target: same component with `researchPage/data/error` and existing `runPage/data/error` states.
4. Interface: two `/api/...?...pageSize=20` requests; independent pagination callbacks.
5. Algorithm: two separate effects/AbortControllers; clear only changing section; render successful sibling during other loading/error; page empty only after both first pages successful/zero.
6. Operations: max two initial GETs, one per section; page action refetches one endpoint only.
7. Boundary: client request state; retry is user page/reload; unmount aborts both.
8. Identity/time: no identity in client; response IDs/timestamps only.
9. Failure/concurrency: either request may settle first/fail; stale effect aborted; handoff disappears on next research fetch; no merged snapshot promise.
10. Bounds: 20 rows/section/request; no polling added.
11. Callers: `/runs`; preserve run rendering/pagination/navigation.
12. Tests: FE-01/03/04/05; request counters and controlled resolution order; NC-02/05.
13. Output: W2-T3 render inputs.
14. Non-goals: no unified page/cursor, automatic polling, autosave.
15. Mechanical output: exactly two state machines/effects.

- [ ] `MRR-W2-T2` Split research and run loading/error/pagination state.

#### `MRR-W2-T3` Research rows, fixed resume link and page copy

1. Requirements/decisions: REQ-001,002,004,007,012; DEC-006/007/010/011.
2. Source: A1 visible policy, current run row/page shell, dashboard route SRC-005/007.
3. Target: research section above preserved run section; `/runs` title “My searches”.
4. Interface: research title/badge/activity/time functions exactly A1; link only fixed encoded ID.
5. Algorithm: title first two seeds +N; state/revision badge table; stage label map; render semantic headings/aria; preserve existing run rows; section/page empty policies.
6. Operations: pure render/navigation; zero mutation or dispatch.
7. Boundary: UI derived view; malformed payload blocked by parser.
8. Identity/time: encoded research ID only; locale date from durable timestamps.
9. Failure/retry/concurrency: render section error independently; no action on failed row except dashboard link; handoff duplicate impossible from payload partition.
10. Bounds: at most 20 visible research and 20 run rows per initial page.
11. Callers: page; preserve dashboard and run destinations.
12. Tests: FE-01/02/03,E2E-01/02; DOM href/text/row-count/duplicate oracles; NC-02/04.
13. Output: emitted browser surface.
14. Non-goals: no dashboard, landing, auth or run-row redesign.
15. Mechanical output: one new section and exact copy change.

- [ ] `MRR-W2-T3` Render research resume rows and update page copy.

#### `MRR-W2-T4` Scoped styles and emitted-browser enforcement

1. Requirements/decisions: REQ-006,007,012,014; DEC-006/011.
2. Source: current history CSS/shell tests and local CDP harness.
3. Target: prefixed styles, unit registry, shell assertion, new browser script.
4. Interface: browser registry emits exact case IDs, activation witnesses, control results and digest.
5. Algorithm: append responsive section/row styles; build production Next; start isolated local server/backend stubs; drive CDP; capture network/DOM/navigation at desktop/mobile.
6. Operations: local build/server/Chrome only; no external network.
7. Boundary: emitted artifact/browser; cleanup child processes/temp build state in finally.
8. Identity/time: synthetic authenticated session seam and deterministic fixture times.
9. Failure: port/build/browser failure reported distinctly; one identical escalated recovery only for proven sandbox denial.
10. Bounds: one final build and one browser run after frozen inputs; Chrome timeout 60s/case; no paid/stateful service.
11. Callers: verification only; preserve existing scripts/tests.
12. Tests: E2E-01/02/03, REG-01/03; NC-04/05/07.
13. Output: W2 certificate for review.
14. Non-goals: no screenshot baselines or visual redesign.
15. Mechanical output: scoped CSS and executable emitted registry.

- [ ] `MRR-W2-T4` Add scoped styles and emitted-browser enforcement.

### W2 coverage matrix

| Case | Scenario / req / dec | Path and starting partition | Action and activation witness | Expected result / operations / forbidden | Control / parity / registration |
|---|---|---|---|---|---|
| `MRR-FE-01` | normal two-list UI; 001,011,012; 006,009,011 | authenticated `/runs`, both first pages nonempty | resolve both requests; DOM headings/rows/network witnesses | both sections, exact copy/no-store path; 2 GETs; no mutations | NC-05; component; W2 registry `FE-01` |
| `MRR-FE-02` | fixed research navigation; 002; 007 | valid research ID | click row; observed href/navigation | exact encoded `/keywords/{id}`; never payload URL or `/runs/{researchId}` | NC-04; component; W2 registry `FE-02` |
| `MRR-FE-03` | handoff/no duplicate/run parity; 004,007; 001,010,011 | research response excludes linked ID; run response contains resulting run | render fixtures; DOM ID/link counters | one run row, zero research duplicate; old run text/href intact | NC-02; component; W2 registry `FE-03` |
| `MRR-FE-04` | partial failure schedules; 006; 006 | each list fails once while sibling succeeds | resolve/reject in both orders; independent state witnesses | successful sibling stays; one scoped alert; no sibling refetch/hide | NC-05; component; W2 registry `FE-04` |
| `MRR-FE-05` | pagination/empty partitions; 006,012; 006,010 | both zero; one zero; page transitions | click each pager and inspect requests/DOM | global empty only both zero page1; one pager changes one endpoint | NC-05; component; W2 registry `FE-05` |
| `MRR-FE-06` | strict BFF/parser; 009,010; 004,005 | auth missing/unavailable; bad query; malformed 2xx | table-drive route/parser; session/proxy/parser witnesses | exact errors; valid exact payload; bad never becomes UI state | NC-06; unit; W2 registry `FE-06` |
| `MRR-E2E-01` | representative emitted path; 001,006,012; 006,011 | production build, auth stub, 4 research states + 2 runs | CDP open `/runs`; network+DOM+CSS witnesses | nonempty two-section desktop/mobile surface, badges/title/times; no bypass | NC-05; emitted_artifact; browser registry `E2E-01` |
| `MRR-E2E-02` | emitted resume; 002; 007 | running and completed research rows | CDP click each; navigation event | `/keywords/{id}` for both, dashboard route loads durable GET | NC-04; emitted_artifact; browser registry `E2E-02` |
| `MRR-E2E-03` | emitted auth/proxy; 005,010; 005 | anonymous then authenticated session stub | request BFF and inspect backend stub headers/counts | anonymous 401/no backend call; auth sends one trusted owner header | NC-01; emitted_artifact; browser registry `E2E-03` |
| `MRR-REG-01` | run/route compatibility; 007,014; 001,008,011 | existing run fixture and POST keyword intent fixture | run old unit/auth tests plus DOM key assertions | `/api/runs`, POST auth, run rows/destination unchanged | NC-07; regression; existing + W2 registry `REG-01` |
| `MRR-REG-02` | schema invariant; 013; 008 | before/after Prisma schema/migration inventory | hash/inventory compare | byte-identical schema/migration list; no generated migration | NC-07; regression; W1 registry `REG-02` |
| `MRR-REG-03` | dashboard/worker/auth unchanged; 014; 008 | current dashboard/poll/auth/worker tests | execute focused existing suites; registration witnesses | all pass; production files outside scope byte-identical | NC-07; regression/emitted; W2 registry `REG-03` |

Substitute fidelity: browser backend/session stubs reproduce only HTTP status,
exact JSON, trusted-owner header capture and deterministic failure ordering.
They do not prove Neon Auth internals or PostgreSQL; existing auth tests and W1
repository enforcement own those claims. CDP executes the emitted production
Next artifact and therefore supports DOM, request, navigation and responsive
claims.

### Verification and handoff

- [ ] `MRR-W2-V1` Run `node --experimental-strip-types --test test/my-runs-research-resume.test.ts` and exact existing auth/shell tests; all W2 unit cases execute.
- [ ] `MRR-W2-V2` Run `npm run check` once on frozen inputs; lint/test/build pass with zero required skips.
- [ ] `MRR-W2-V3` Run `node test/browser/my-runs-research-resume.mjs` once on frozen build; E2E-01–03 execute and controls falsify.
- [ ] `MRR-W2-V4` Assert two initial GETs, one GET per page action, zero POST/mutation, fixed links, owner header, scoped errors and forbidden data/navigation.
- [ ] `MRR-W2-V5` Assert required=registered=executed W2 cases, zero skips/duplicates/unexpected/unactivated and independently matching digest.
- [ ] `MRR-W2-H1` Record changed files/symbols and no migrations. Evidence: ___
- [ ] `MRR-W2-H2` Record commands/outcomes/cases/skips/controls/build/browser evidence. Evidence: ___
- [ ] `MRR-W2-H3` Diff matches W2 scope and read-only files hash unchanged. Evidence: ___
- [ ] `MRR-W2-H4` No W3/prohibited action started. Evidence: ___
- [ ] `MRR-W2-H5` Append certificates and atomically advance A5 to assigned W3. Evidence: ___
- [ ] `MRR-W2-H6` Begin W3 only after W2 acceptance and A5 transition.

## MRR-W3 — Test-only current-contract correction

```yaml
window_id: MRR-W3
objective: Correct four proven stale test surfaces without changing production code.
depends_on: [MRR-W2 accepted]
consumes: frozen feature implementation plus MRR-SRC-016-019
produces: focused and full-suite green evidence or one diagnosed product blocker
assigned_agent_policy: explicit_multi_window
authorized_write_scope:
  - frontend/test/keyword-intelligence-api.test.ts: W5-A06 history-length assertions only
  - email_scraper/test/keyword-intelligence-api.test.js: classifier seam and current mapping/validation assertions only
  - email_scraper/test/keyword-intelligence-query-mapper.test.js: product mapping and current validation partitions only
  - email_scraper/test/keyword-intelligence-worker-flow.test.js: overviewResponse monthly_searches nesting only
shared_file_scope: none with W1/W2 production files; test edits occur after those inputs freeze
read_only_scope:
  - current production sources cited by SRC-016-018
  - every other test, fixture, registry and certificate
authorized_actions:
  - exact four-file test edits and local focused/full test commands
  - local sandbox escalation for identical localhost tests
prohibited_actions:
  - every production, fixture outside four files, schema, migration, registry ID deletion or digest weakening
  - OpenAI/DataForSEO/provider/network/AWS/production/deployment/commit/push
successor: STOP
successor_reserved_for: independent review
may_start_successor: false
```

### Preconditions

- [ ] `MRR-W3-P1` A5 assigns W3; hashes match; W1/W2 are accepted. Evidence: ___
- [ ] `MRR-W3-P2` Record current four focused failures and verify each mechanical trace against SRC-016-018. Evidence: ___
- [ ] `MRR-W3-P3` No API/provider secret is present or required; localhost escalation is authorized. Evidence: ___
- [ ] `MRR-W3-P4` Record both nested worktrees and freeze every production file hash. Evidence: ___

### Task blocks

#### `MRR-W3-T1` Frontend history cardinality assertion

1. Req/dec: REQ-015; DEC-013-015. 2. Source: parser `monthlyHistory`; W5-A06. 3. Target: only W5-A06 history-length block. 4. Interface: array of strict points, no length bound. 5. Algorithm: assert lengths 0,14,103 parse; retain invalid month/negative volume/keys. 6. Ops: pure parser. 7. Boundary: unit. 8. Identity/time unchanged. 9. Failure: malformed points still throw; no retry/concurrency. 10. Bounds: array unbounded by parser, point bounds retained. 11. Preserve all W5/R5 IDs/certificate. 12. TEST-01/NC-08. 13. Output focused green. 14. No library/type edit. 15. One assertion block only.

- [ ] `MRR-W3-T1` Replace only obsolete history-length rejection assertions.

#### `MRR-W3-T2` Backend deterministic classifier and API assertions

1. Req/dec: REQ-015; DEC-013-015. 2. Source: classifier/buildRunSnapshot/map/validator and W4 failures. 3. Target: `makeApi` classifier option/default plus W4-Q01/Q03/Q04/Q08 current assertions. 4. Interface: async fake returns ordered exact `{itemId,product}` for every item. 5. Algorithm: inject fake; choose product deterministically from test input/explicit overrides; assert product=true gets `/products`, false/absent gets store scope; assert current editable text acceptance while retaining row set/length/control/duplicate failures. 6. Ops: zero OpenAI/network. 7. Boundary: test seam. 8. IDs/order exact. 9. Fake omission/reorder must fail; conflicts/replays retained. 10. 1-100 items. 11. Preserve all W4/R5 registry IDs/certificates/server cases. 12. TEST-02/03 and NC-09. 13. Output focused green. 14. No production or manifest-fixture edit. 15. Exact seam/assertion sites only.

- [ ] `MRR-W3-T2` Inject the classifier fake and update only superseded API assertions.

#### `MRR-W3-T3` Query-mapper contract assertions

1. Req/dec: REQ-015; DEC-013-015. 2. Source: current query-mapper. 3. Target: mapping/default and validation tests. 4. Interface: `product===true` selects product prefix; otherwise store prefix; editable rows enforce current five partitions. 5. Algorithm: add explicit booleans, update defaults, split rejection/acceptance tables. 6. Ops: pure. 7. Boundary: unit. 8. item IDs unchanged. 9. duplicates/control/empty/oversize/cardinality remain failures; quotes/operators/no-prefix/irrelevance accepted. 10. 100 rows/200 codepoints. 11. Preserve unrelated tests. 12. TEST-02/03, NC-09. 13. Output focused green. 14. No mapper edit. 15. Exact assertions only.

- [ ] `MRR-W3-T3` Align mapper tests to product classification and current editable grammar.

#### `MRR-W3-T4` Worker provider fixture field path

1. Req/dec: REQ-015; DEC-013-015. 2. Source: adapter consumed path and overviewResponse. 3. Target: move generated `monthly_searches` into `keyword_info`. 4. Interface: current synthetic DataForSEO overview item. 5. Algorithm: keep 15 deterministic points/values; nest under keyword_info; remove obsolete top-level field; change no call/object oracle. 6. Ops: in-memory HTTP only. 7. Boundary: component substitute. 8. request/result IDs unchanged. 9. malformed old path must fail publication; no retry/concurrency changes. 10. same 11/19 calls and object ceilings. 11. Preserve all worker scenarios/controls. 12. TEST-04/NC-10. 13. Output three formerly failing worker cases green. 14. No adapter/service/schema edit. 15. One fixture constructor only.

- [ ] `MRR-W3-T4` Move the synthetic monthly-history field to its current nested path.

### W3 coverage matrix

| Case | Scenario / req / dec | Path and starting partition | Action and activation witness | Expected result / operations / forbidden | Control / parity / registration |
|---|---|---|---|---|---|
| `MRR-TEST-01` | variable history; 015; 013-015 | frontend parser, lengths 0/14/103 plus malformed points | execute W5-A06; each length and point guard witness | valid lengths parse; bad month/negative/key still throw; no parser edit | NC-08; unit; W5-A06 supplemental registry |
| `MRR-TEST-02` | classifier/product mapping; 015; 013-015 | API fake and mapper true/false/absent partitions | create handoff/map rows; fake-call/order and output witnesses | exact `/products` only true; zero OpenAI; IDs/certificates unchanged | NC-09; unit/component substitute; W3 registry in backend API/mapper tests |
| `MRR-TEST-03` | editable grammar; 015; 014 | quotes/operators/no-prefix/irrelevant valid; empty/control/duplicate/oversize/set mismatch invalid | table-drive validator; per-partition witnesses | exact current accept/reject sets; no production relaxation | NC-09; unit; W3 registry in API/mapper tests |
| `MRR-TEST-04` | current provider fixture; 015; 014 | worker component with nested monthly_searches | drive SCN-KI-001/013/026; adapter normalized-history/publication witnesses | all publish, numeric trend, old call/object/lease oracles unchanged; no external call | NC-10; component substitute; W3 registry in worker test |

Substitute fidelity: the classifier fake proves only ordered boolean plumbing;
production classifier transport/semantic quality remain covered elsewhere. The
worker HTTP fake matches the exact adapter-consumed nested field path and its
existing component flow; strict provider-shape fidelity remains in adapter
tests. Neither substitute authorizes or performs a provider call.

### Verification and handoff

- [ ] `MRR-W3-V1` Run the four focused files directly; TEST-01–04 execute and NC-08–10 falsify the obsolete behavior.
- [ ] `MRR-W3-V2` Run frontend `npm test`, backend focused API test with localhost escalation if needed, then backend `npm test`; all unguarded tests pass and only established opt-in integration skips remain.
- [ ] `MRR-W3-V3` Compare frozen production hashes and all registry ID/digest source sets; exact equality required.
- [ ] `MRR-W3-V4` Assert zero OpenAI/DataForSEO/network/AWS calls and no assertion outside the four traced surfaces was loosened.
- [ ] `MRR-W3-V5` Assert required=registered=executed TEST-01–04, zero skips/duplicates/unexpected/unactivated and matching digest.
- [ ] `MRR-W3-H1` Record exact four changed test files and `production_files: []`, `migrations: []`. Evidence: ___
- [ ] `MRR-W3-H2` Record focused/full commands, outcomes, cases and controls. Evidence: ___
- [ ] `MRR-W3-H3` Diff is test-only and matches exact anchors; production hashes match. Evidence: ___
- [ ] `MRR-W3-H4` No prohibited action or untraced fifth failure was changed around. Evidence: ___
- [ ] `MRR-W3-H5` Append final certificates and set A5 `AWAITING_REVIEW`. Evidence: ___
- [ ] `MRR-W3-H6` Stop for independent review.

## Global coverage-set enforcement

The authoritative 23 IDs are listed only in A8. Every window registry must
enumerate its owned IDs explicitly; execution is recorded only after the named
activation witness and oracle pass. The global digest in A6 is computed from
the sorted LF-terminated IDs. Missing, duplicate, unexpected, skipped,
selected-but-filtered, or executed-without-activation members fail.

## Frozen gates and environment-invalidated recovery

- W1 final inputs: its seven source/test/fixture files; gates W1-V1–V5.
- W2 final inputs: its eight files plus accepted W1 fixture; gates W2-V1–V5.
- W3 final inputs: four test files plus frozen production hashes; gates W3-V1–V5.
- Diagnostics may be repeated while editing. A successful final build/browser
  or full suite is rerun only after a relevant edit invalidates it.
- If a localhost/build/headless command fails solely from sandbox denial, prove
  no surviving process/material mutation/result, then retry the identical
  command once with local escalation. Assertion failures are never relabelled.
- No gate uses a database, provider, external network, AWS or production data.

## Mandatory parent authoring checklist

### Authority and artifacts

- [x] `PA-001` All governing instructions and authorities are recorded. Evidence: MRR-AUTH-001
- [x] `PA-002` All eight artifacts exist at named paths. Evidence: MRR-AUTH-001
- [x] `PA-003` Mutable status exists only in A5. Evidence: MRR-AUTH-001
- [x] `PA-004` Execution and approval boundaries are explicit. Evidence: MRR-AUTH-001
- [x] `PA-005` Current working tree and repository boundaries were inspected. Evidence: MRR-AUTH-001
- [x] `PA-006` Product scope, exclusions and compatibility policy are locked. Evidence: MRR-AUTH-001
- [x] `PA-007` Canonical authoring-standard path and revision are pinned. Evidence: MRR-AUTH-001
- [x] `PA-008` A5 grants local sandbox escalation without external authority. Evidence: MRR-AUTH-001

### Evidence and payload safety

- [x] `PP-001` Every material fact has an allowed classification. Evidence: MRR-AUTH-002
- [x] `PP-002` No inferred fact enters a locked contract or task. Evidence: MRR-AUTH-002
- [x] `PP-003` Every payload has provenance-labelled sanitized evidence. Evidence: MRR-AUTH-002
- [x] `PP-004` Every consumed field has one exact evidence-backed path and type. Evidence: MRR-AUTH-002
- [x] `PP-005` Every payload has a strict parser and normalized internal result. Evidence: MRR-AUTH-002
- [x] `PP-006` Missing, malformed, boundary and unknown-field fixtures exist. Evidence: MRR-AUTH-002
- [x] `PP-007` Multiple supported shapes are N/A; one exact shape per payload. Evidence: MRR-AUTH-002
- [x] `PP-008` No fallback probing, alias guessing, permissive cast or synthetic evidence remains. Evidence: MRR-AUTH-002
- [x] `PP-009` Raw secrets and unnecessary private payload data are excluded. Evidence: MRR-AUTH-002
- [x] `PP-010` Unknown payload facts are zero. Evidence: MRR-AUTH-002

### Discovery and lifecycle closure

- [x] `PD-001` Applicable discovery inventories are complete. Evidence: MRR-AUTH-003
- [x] `PD-002` Claimed absences have negative-search evidence. Evidence: MRR-AUTH-003
- [x] `PD-003` Every workflow has complete state behavior. Evidence: MRR-AUTH-003
- [x] `PD-004` Every external/durable failure boundary is classified. Evidence: MRR-AUTH-003
- [x] `PD-005` Duplicate/reorder/retry/restart/stale/cancellation behavior is locked or N/A. Evidence: MRR-AUTH-003
- [x] `PD-006` Terminal/visibility boundaries use durable research/run evidence. Evidence: MRR-AUTH-003

### Decision closure

- [x] `PC-001` Applicable D1-D13 ledgers, including D2A, are complete or evidenced N/A. Evidence: MRR-AUTH-004
- [x] `PC-002` Every interface and payload schema is exact. Evidence: MRR-AUTH-004
- [x] `PC-003` No new multi-write exists; existing atomic handoff is preserved. Evidence: MRR-AUTH-004
- [x] `PC-004` Identities/timestamps are exact; no new key/fingerprint. Evidence: MRR-AUTH-004
- [x] `PC-005` Identity cardinality/substitution rules are explicit. Evidence: MRR-AUTH-004
- [x] `PC-006` Owner isolation and concurrent handoff behavior are explicit. Evidence: MRR-AUTH-004
- [x] `PC-007` New external operations are zero; read cardinality bounded. Evidence: MRR-AUTH-004
- [x] `PC-008` Durable retry reconstruction is N/A to read-only list. Evidence: MRR-AUTH-004
- [x] `PC-009` Replay configuration is N/A; pagination is request-local. Evidence: MRR-AUTH-004
- [x] `PC-010` Control-plane/status/public-output paths are closed. Evidence: MRR-AUTH-004
- [x] `PC-011` Build/runtime/dependency closure is proven. Evidence: MRR-AUTH-004
- [x] `PC-012` Environment capabilities are local and gated. Evidence: MRR-AUTH-004
- [x] `PC-013` Scale/operation/resource ceilings are locked. Evidence: MRR-AUTH-004
- [x] `PC-014` Historical/mixed-version visibility is explicit. Evidence: MRR-AUTH-004
- [x] `PC-015` No task delegates a material implementation choice. Evidence: MRR-AUTH-004
- [x] `PC-016` No storage/migration/test-cleanup mutation exists. Evidence: MRR-AUTH-004

### Scenario and acceptance closure

- [x] `PS-001` Scenario dimensions derive from current ledgers. Evidence: MRR-AUTH-005
- [x] `PS-002` Combination strategy/exclusions are justified. Evidence: MRR-AUTH-005
- [x] `PS-003` Every scenario has preconditions/actions/witness/oracle. Evidence: MRR-AUTH-005
- [x] `PS-004` Representative nonempty end-to-end behavior is required. Evidence: MRR-AUTH-005
- [x] `PS-005` E2E cannot pass through zero-work/bypass. Evidence: MRR-AUTH-005
- [x] `PS-006` Negative controls prove required tests fail. Evidence: MRR-AUTH-005
- [x] `PS-007` Every applicable durable/external failure has injection; external mutations are N/A. Evidence: MRR-AUTH-005
- [x] `PS-008` Owner/handoff schedule-sensitive behavior is tested. Evidence: MRR-AUTH-005
- [x] `PS-009` Generated values are deterministic/evidence-backed. Evidence: MRR-AUTH-005
- [x] `PS-010` Representative/max workload ceilings are asserted. Evidence: MRR-AUTH-005
- [x] `PS-011` Evidence parity matches each claim. Evidence: MRR-AUTH-005
- [x] `PS-012` Public output is traced to exercised paths. Evidence: MRR-AUTH-005
- [x] `PS-013` Every window has a complete behavioral coverage matrix. Evidence: MRR-AUTH-005
- [x] `PS-014` Every required case has one ID and registration. Evidence: MRR-AUTH-005
- [x] `PS-015` Exact set equality/zero skips/digest are required. Evidence: MRR-AUTH-005
- [x] `PS-016` Every critical invariant has a falsification control. Evidence: MRR-AUTH-005
- [x] `PS-017` Every substitute has a fidelity disposition. Evidence: MRR-AUTH-005
- [x] `PS-018` Accepted-test invalidation rules are explicit. Evidence: MRR-AUTH-005
- [x] `PS-019` Final gates are exact/risk-proportionate/bounded. Evidence: MRR-AUTH-005
- [x] `PS-020` Handoff records full enforcement counts/results/digest. Evidence: MRR-AUTH-005
- [x] `PS-021` Environment invalidation uses one identical escalated recovery. Evidence: MRR-AUTH-005

### Window and agent-boundary closure

- [x] `PW-001` Dependency DAG is acyclic and complete. Evidence: MRR-AUTH-006
- [x] `PW-002` Every window establishes one coherent capability. Evidence: MRR-AUTH-006
- [x] `PW-003` Every task contains all fifteen F3 fields. Evidence: MRR-AUTH-006
- [x] `PW-004` Every task has a complete mechanical trace. Evidence: MRR-AUTH-006
- [x] `PW-005` Every window has exact write/read/action/prohibition scope. Evidence: MRR-AUTH-006
- [x] `PW-006` Shared-file ownership is symbol-specific and ordered. Evidence: MRR-AUTH-006
- [x] `PW-007` Default assignments authorize exactly one window. Evidence: MRR-AUTH-006
- [x] `PW-008` Successor reservation/may_start_successor are explicit. Evidence: MRR-AUTH-006
- [x] `PW-009` Handoff verifies actual diff against scope. Evidence: MRR-AUTH-006
- [x] `PW-010` No successor satisfies predecessor acceptance. Evidence: MRR-AUTH-006
- [x] `PW-011` Implementation/verification/handoff actions are boxes. Evidence: MRR-AUTH-006
- [x] `PW-012` Every checked planning box cites evidence. Evidence: MRR-AUTH-006

### Traceability and change control

- [x] `PT-001` Every requirement has complete A8 trace. Evidence: MRR-AUTH-007
- [x] `PT-002` Every source member has one owner/assertion. Evidence: MRR-AUTH-007
- [x] `PT-003` Every plan member has requirement and anchors. Evidence: MRR-AUTH-007
- [x] `PT-004` A6 is append-only and non-authorizing. Evidence: MRR-AUTH-007
- [x] `PT-005` Changelog/invalidation rules are present. Evidence: MRR-AUTH-007
- [x] `PT-006` A5 concurrency/version/hash pins are specified. Evidence: MRR-AUTH-007
- [x] `PT-007` IDs are unique and never reused. Evidence: MRR-AUTH-007

### Audit and readiness

- [x] `PR-001` Forward simulation passed normal/failure boundaries. Evidence: MRR-AUTH-008
- [x] `PR-002` Backward simulation traced public/terminal fields. Evidence: MRR-AUTH-008
- [x] `PR-003` Independent reachable-set audit passed. Evidence: MRR-AUTH-008
- [x] `PR-004` Payload no-guessing audit passed. Evidence: MRR-AUTH-008
- [x] `PR-005` Anti-vacuity/negative-control audit passed. Evidence: MRR-AUTH-008
- [x] `PR-006` Environment/runtime/deployment parity audit passed. Evidence: MRR-AUTH-008
- [x] `PR-007` Scale/competing-owner falsification passed. Evidence: MRR-AUTH-008
- [x] `PR-008` Mistake-derived conformance audit passed. Evidence: MRR-AUTH-008
- [x] `PR-009` Mechanical checklist lint has no missing IDs/links/evidence/scopes. Evidence: MRR-AUTH-008
- [x] `PR-010` No implementation choice is delegated. Evidence: MRR-AUTH-008
- [x] `PR-011` Enforcement lint rejects missing/duplicate/skipped/filtered/unactivated/unexpected cases. Evidence: MRR-AUTH-008
- [x] `PR-012` Substitute-fidelity/accepted-test invalidation audits passed. Evidence: MRR-AUTH-008
- [x] `PR-013` Sandbox identical-recovery/external-authority lint passed. Evidence: MRR-AUTH-008
