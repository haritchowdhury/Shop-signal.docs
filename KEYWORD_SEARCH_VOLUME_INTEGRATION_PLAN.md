# KeywordSearchVolume Integration Plan

**Status:** superseded as an execution specification by the eight-artifact
keyword-intelligence package; retained as product-intent provenance only — no
implementation or deployment authority  
**Scope:** migrate the complete `KeywordSearchVolume` product into the existing
StoreSignal application without Python, SQLite, a separate service, or a second
dashboard.

Package index:

- `A1` `KEYWORD_INTELLIGENCE_PRODUCT_CONTRACT.md`
- `A2` `KEYWORD_INTELLIGENCE_DISCOVERY_DOSSIER.md`
- `A3` `KEYWORD_INTELLIGENCE_DECISION_LEDGER.md`
- `A4` `KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md`
- `A5` `ACTIVE_EXECUTION_STATE.md` (keyword package selected for documentation;
  implementation remains unassigned)
- `A6` `KEYWORD_INTELLIGENCE_EXECUTION_EVIDENCE.md`
- `A7` `KEYWORD_INTELLIGENCE_SPECIFICATION_CHANGELOG.md`
- `A8` `KEYWORD_INTELLIGENCE_TRACEABILITY_INDEX.md`

## 1. Required outcome

`KeywordSearchVolume` becomes the first step of the existing Email Scraper
workflow.

The complete target flow is:

```text
seed phrases
  -> US-only suggestions + related expansion (two calls per seed)
  -> one US overview screen of every candidate (maximum 300)
  -> deterministic metric-backed shortlist (maximum 200)
  -> overview research for the same shortlist in the other eight markets
     while reusing the US screen metrics
  -> KeywordSearchVolume calculation in Node.js
  -> complete KeywordSearchVolume dashboard in Next.js
  -> user keeps the recommended list or selects a different list
  -> duplicate and near-similarity review
  -> final retained list of 1–100 distinct keywords
  -> one intent-aware Shopify query per retained keyword
  -> Google Custom Search probe (up to 10 results per query)
  -> existing editable query review and explicit confirmation
  -> existing Email Scraper discovery, lead, and traffic workflow
```

There is no second research stage after query conversion. There is no
product-only restriction, no top-10 keyword reduction, and no automatic loss of
valid distinct keywords.

## 2. Non-negotiable scope

- Move the current SQLite response cache to the existing Prisma/Postgres
  database.
- Port the Python pipeline logic to Node.js inside `email_scraper/`.
- Port the entire `dashboard/index.html` experience to Next.js inside
  `frontend/`.
- Preserve the current KeywordSearchVolume calculations and dashboard behavior.
- Preserve the existing Email Scraper query review, revision-conflict, Google
  probing, explicit confirmation, and downstream discovery behavior.
- Keep product and non-product discovery queries.
- Keep a strict final limit of 100 retained keywords and therefore 100 queries.
- Do not add a Python runtime, Python subprocess, iframe, separate API service,
  separate database, Fargate service, or Step Functions workflow.
- Do not change the currently parked AWS deployment state while planning or
  porting locally. The keyword-research queue/Lambda deployment requires its
  own later execution window and explicit AWS approval.

## 3. What must be preserved from KeywordSearchVolume

### Research logic

The Node.js port must reproduce the current Python behavior for:

- seed expansion through DataForSEO keyword suggestions and related keywords,
  performed once per seed in the US anchor market rather than once per market;
- one uncapped-before-call US overview screen of the resulting 1–300 candidates;
- a deterministic US-metric shortlist of at most 200 candidates, researched as
  the same immutable list in the other eight markets with US metrics reused;
- multi-market research for US, GB, CA, AU, NZ, DE, FR, IN, and AE;
- market-specific language and location codes;
- one overview request per market stage (provider maximum 700; this plan sends
  at most 300 for the US anchor and at most 200 for every other market);
- cumulative and per-market metrics;
- search volume, CPC, competition, difficulty, intent, and monthly history;
- seasonality-aware trend slope;
- commercial-intent scoring and informational detection;
- token normalization and retail aliases;
- exact and near-variant grouping;
- canonical keyword selection;
- non-transitive clustering;
- lane classification and category/audience/channel/fit/modifier facets;
- raw, headline, adjusted, and distinct-variant cluster volumes;
- keyword and cluster opportunity scoring;
- flags and recommendation decisions; and
- CSV/JSON-equivalent exports.

The existing Python modules are the behavior reference while porting. They are
removed from the application path only after parity tests prove the Node output.
Python is not a runtime dependency of the finished main project.

The collection topology is the deliberate exception to statement-for-statement
Python parity: expansion is no longer repeated across nine markets, and only
the US-screened shortlist proceeds to the remaining eight. Post-collection
normalization, deduplication, clustering, scoring, recommendations, summaries,
and exports remain direct parity work.

### Complete dashboard

The Next.js version must retain the current dashboard, not replace it with a
small keyword picker. It includes:

- the research hero and editable phrase chips;
- manual keyword add/edit/remove behavior;
- cumulative and per-country market views;
- all seed, cluster, intent, lane, facet, volume, opportunity,
  recommendation, flag, and text filters;
- summary cards;
- seed-performance chart;
- interactive 3D cluster landscape, controls, legend, tooltips, and inspector;
- collection funnel and store-discovery mix;
- intent, recommendation, opportunity, and flag charts;
- volume-overlap analysis;
- monthly history selector and chart;
- recommended-keyword volume/trend chart;
- volume/difficulty bubble chart;
- competition/opportunity scatter chart;
- sortable, selectable, editable, paginated keyword table;
- light/dark themes, empty/error/loading states, and tooltips; and
- filtered CSV export.

The HTML/CSS/JavaScript is converted into normal Next.js components and CSS.
It is not embedded as the old HTML page. The current Chart.js 3.9.1,
chartjs-chart-treemap 2.0.0, and custom canvas behavior should be retained with
locally installed frontend dependencies rather than runtime CDN scripts.

## 4. Database move

Use the existing Neon/Postgres database and Prisma migration system.

The standalone KeywordSearchVolume project currently has no database table for
its calculated output. SQLite contains only the DataForSEO response cache; the
calculated keywords, clusters, market views, and summary are written to
`data/output/*.json` and CSV files. Those output files must be imported into a
durable application model rather than copied into the integrated runtime.

The minimum persistent data is:

- one owner-scoped keyword-research record containing its seeds, markets,
  status, configuration snapshot, summary, keyword results, cluster results,
  selected keywords, selection revision, worker lease/recovery state, and
  timestamps;
- one Postgres-backed DataForSEO response cache keyed by the same deterministic
  endpoint-and-payload fingerprint used by the SQLite cache, with the existing
  seven-day expiry behavior; and
- the minimal paid-request outcome metadata needed to prevent an unknown or
  ambiguous DataForSEO response from being charged again automatically.

The complete normalized dashboard result may be held in structured Postgres
JSON fields on the research record; this work does not require a table per
keyword merely to replace each output file. CSV and JSON exports are generated
from that persisted record on demand.

When an Email Scraper run is created, one transaction must:

- verify the expected owner and keyword-selection revision;
- link the run to its originating keyword-research record;
- copy an immutable run snapshot of the exact retained keywords and their
  source seeds, lane, cluster, market metrics, scores, flags, recommendation
  state, and initially mapped query; and
- create the corresponding persisted `RunQuery` rows.

The research record remains available after the Email Scraper run finishes,
and the run snapshot is never recalculated from a later research edit. This
preserves exactly what that run used even if the same research is edited or
reused later.

Only strictly parsed, normalized fields needed by the dashboard are retained.
The Python behavior that writes verbatim provider response bodies to
`data/raw/` is not copied because the main project forbids storing raw provider
bodies. Credentials remain in the existing secret/config path and never enter
Postgres, frontend responses, logs, or exports.

Research records and cache rows must be read through the existing owner and
database boundaries. No SQLite file or generated `data/output/*.json` file is a
production source of truth after the migration.

### Durable research execution

Keyword research is too long-running to execute in the API process. It must run
in one dedicated Node.js Lambda triggered by one dedicated keyword-research SQS
queue with a DLQ. It must not run inside the browser, Next.js, the API process,
or one Lambda invocation that attempts to finish the entire research job.

- Starting research creates a `queued` owner-scoped research record and returns
  its ID immediately; the backend sends only the initial identity/generation
  message to SQS.
- Each Lambda invocation claims the research generation in Neon, performs one
  bounded slice of provider work, persists its checkpoint, and sends the next
  continuation message when more work remains.
- SQS messages contain only the research ID, generation, checkpoint version,
  and deterministic fingerprint—not seeds, results, or provider bodies.
- Provider-batch outcomes and usable normalized checkpoints are persisted as
  work completes, so message redelivery or an expired lease can safely resume
  without blindly repeating a paid request.
- Completion publishes the full normalized research result and default
  selection in one fenced Neon transaction, then marks the research record
  `completed`; queue emptiness is never a completion signal.
- Closing the tab or signing out does not cancel the job. Reopening its saved
  research URL loads status and results from Postgres.
- If a Lambda stops or times out, SQS redelivery and Neon lease recovery resume
  from persisted checkpoints/cache.

The Lambda uses reserved concurrency one to preserve the existing conservative
DataForSEO call rate. Do not configure event-source `MaximumConcurrency=1`;
AWS does not allow that value. Neon remains the sole coordinator and durable
application database.

## 5. Node.js port

Create a focused `email_scraper/src/keyword-intelligence/` module set. Port the
current Python responsibilities directly:

| Current Python responsibility | Node.js responsibility |
|---|---|
| `pipeline/config.py` + `config.yaml` | strict application config and a versioned research snapshot |
| `pipeline/cache.py` | Prisma/Postgres cache repository |
| `pipeline/client.py` | strict DataForSEO Labs adapter with the same retry/rate bounds |
| `pipeline/models.py` | Zod schemas and plain Node domain objects |
| `pipeline/normalize.py` | metric normalization and trend calculation |
| `pipeline/intent.py` | intent classification and commercial-intent score |
| `pipeline/dedup.py` | token aliases, signatures, similarity, and canonical variants |
| `pipeline/cluster.py` | lanes, facets, non-transitive clusters, and aggregate volumes |
| `pipeline/score.py` | keyword/cluster flags, scores, and recommendations |
| `pipeline/pipeline.py` | seed expansion, market collection, batching, aggregation, and output assembly |
| `pipeline/output.py` | dashboard API serialization and CSV export |

Do not redesign the scoring or clustering during the language conversion.
First obtain output parity; later product changes must be separate work.

## 6. Dashboard-to-query handoff

### Selection rule

- When research completes, all active recommended keywords are selected by
  default, matching the current dashboard behavior.
- The user may remove recommended keywords and add active non-recommended or
  manual keywords.
- Before query conversion, run exact-duplicate and near-similarity analysis over
  the entire selected list, regardless of how the keywords were selected.
- Similar variants may not both enter query conversion. The review shows the
  conflict and the canonical suggestion; it does not silently choose for the
  user.
- After conflicts are resolved, the retained list must contain 1–100 keywords.
- If all 100 selections are genuinely distinct, all 100 are retained.

This selection check is separate from downstream domain deduplication. Keyword
similarity prevents repeated searches; the existing stable-shop merge prevents
the same Shopify store found by different queries from becoming duplicate
domains.

### One keyword becomes one query

Every retained keyword produces exactly one query. The mapper uses the lane
already calculated by KeywordSearchVolume:

| Keyword lane | Query form |
|---|---|
| `category_discovery` | `site:myshopify.com/products <keyword>` |
| `store_discovery` | `site:myshopify.com <keyword>` |
| `local_discovery` | `site:myshopify.com <keyword>` |
| `brand_competitor` | `site:myshopify.com <keyword>` |

Examples:

```text
linen midi dress          -> site:myshopify.com/products linen midi dress
women's clothing stores   -> site:myshopify.com women's clothing stores
sustainable clothing brands -> site:myshopify.com sustainable clothing brands
```

Manual keywords must pass through the same Node lane/facet classifier before
mapping. The query validator must accept both supported query forms, reject
extra operators/quotes/control characters, retain the 200-character bound, and
validate the keyword against its originating seed/category context.

The old candidate-generation, repair, product-only validation, and “select the
best 10/20 queries per category” path is bypassed for research-backed runs.
Google probing is retained for every mapped query. A failed or weak probe is
shown in the existing query review instead of causing a different keyword to be
generated automatically.

### Capacity contract

Keyword research itself has this fixed maximum topology for five seeds:

```text
10 US expansion calls
+ 1 US overview call for at most 300 candidates
+ 8 remaining-market overview calls for the same at-most-200 shortlist
= 19 first-pass logical provider calls
```

Each suggestions/related attempt reserves `$0.0156`. An overview attempt
reserves `$0.012 + $0.00012 × requestedKeywordCount`. Therefore the maximum
first pass reserves `$0.492`; five attempts for every logical task reserve at
most `$2.46`; and every research has the immutable hard cap
`maxCostPerResearchUsd=$3.00`. Before every provider call, the database must
atomically deny the call if actual cost from every known settled response plus
held in-flight/ambiguous reservations plus the new reservation would exceed
`$3.00`.

Google Custom Search currently returns at most 10 result occurrences per query.
Therefore:

```text
100 retained keywords
  = 100 queries
  x at most 10 Google results
  = at most 1,000 pre-dedup result occurrences
```

The number of unique domains can be anywhere from 0 to 1,000 because the same
domain can appear in several queries. The existing stable-domain aggregation
then deduplicates those occurrences. The current AWS manifest/final path is
bounded at 1,000 domains; G-R30 proves the 1,000-domain downstream publication
capacity, but a new end-to-end test must prove the new 100-query input path.

## 7. Implementation sequence

### Phase 1 — Lock parity fixtures

- Record representative current Python outputs for normalization, trend,
  intent, deduplication, clustering, scoring, cumulative markets, country
  markets, summaries, and exports.
- Record the current dashboard structure and interactions as browser parity
  cases.
- Use sanitized fixtures only; make no live or paid provider call.

### Phase 2 — Move persistence to Prisma/Postgres

- Add forward-only Prisma models/migration for owner-scoped keyword research,
  the normalized response cache, and minimal paid-call outcome tracking.
- Add the immutable research-to-run linkage and exact run keyword snapshot.
- Add queued/running/completed/failed research state plus lease, heartbeat,
  generation fencing, progress, checkpoint, and recovery fields following the
  existing AWS worker invariants.
- Replace SQLite cache semantics with the Postgres repository and preserve the
  seven-day TTL and deterministic cache key.
- Add owner isolation, cache hit/miss/expiry, job recovery, run-snapshot, replay,
  and migration tests using the existing isolated Postgres harness.

### Phase 3 — Port Python logic to Node.js

- Port the modules in the mapping above without algorithm changes.
- Add strict DataForSEO request/response adapters for the three existing Labs
  endpoints.
- Run the same sanitized inputs through Python and Node during development and
  require matching normalized keyword, cluster, score, recommendation, market,
  summary, and export results.
- Remove Python from the runtime path only after parity passes.

### Phase 4 — Add the API and dedicated research-worker boundaries

- Add owner-scoped endpoints to queue/load a keyword research record, report its
  durable progress, save selections with a revision, and create the Email
  Scraper run and immutable keyword snapshot from the finalized selection.
- Add one bounded Node.js keyword-research Lambda, one SQS queue, and one DLQ.
  The Lambda advances the persisted research checkpoint and requeues a
  continuation until the job reaches its fenced terminal transaction.
- API handlers only create/read records or enqueue the initial message; they
  never execute provider research.
- Keep the work inside the existing backend, database, auth, and frontend proxy
  patterns.
- Package the worker with the existing Lambda build conventions. Resource
  creation, secret installation, event-source enablement, and paid smoke calls
  remain separately approval-gated.

### Phase 5 — Convert the full dashboard to Next.js

- Create a Next.js keyword-research route and component set from the complete
  HTML dashboard.
- Preserve its layout, CSS, charts, canvas interactions, filters, table,
  selection behavior, theme, errors, loading states, and CSV output.
- Replace `localStorage` as the source of truth for research results and final
  selections with the owner-scoped backend record; local storage may remain
  only for harmless UI preferences such as the theme.
- Connect the existing “Review my keywords” action to the duplicate/similarity
  review and finalized handoff.

### Phase 6 — Replace the first Email Scraper query-planning step

- Create one query per retained keyword using the lane mapping above.
- Update backend and frontend query validation to accept both product and
  non-product Shopify queries and a variable total of 1–100.
- Preserve editable query revision control, Google probing, saved probe results,
  explicit confirmation, AWS confirmed-query dispatch, and domain aggregation.
- Keep ordinary legacy runs readable; do not rewrite historical runs or query
  rows.

### Phase 7 — Verification and cleanup

- Prove full Python-to-Node calculation parity on fixtures.
- Prove full dashboard visual and interaction parity at desktop and mobile
  widths.
- Prove owner isolation and strict frontend/backend payload parsing.
- Prove recommended-default, custom-selection, exact-duplicate,
  near-similarity, and 100-distinct-keyword cases.
- Prove tab closure has no effect, completed research reloads from Postgres,
  SQS redelivery/worker timeout recovers from a fenced checkpoint without
  blindly duplicating paid work, and a finished Email Scraper run retains its
  immutable keyword snapshot after later research edits.
- Prove product and non-product query mapping and editing.
- Prove 100 queries produce no more than 1,000 probe occurrences and the
  existing stable-domain merge accepts up to 1,000 unique domains.
- Run backend unit/integration/security/full tests and `frontend/npm run check`.
- Remove the obsolete Python runtime entry points, SQLite dependency, static
  dashboard serving path, and old research-output loading only after all parity
  and end-to-end checks pass.

## 8. Explicitly not part of this plan

- changing KeywordSearchVolume scoring weights or thresholds;
- redesigning the dashboard;
- reducing results to a top 10;
- forcing every query to `/products`;
- silently deleting selected keywords;
- adding a storefront-verification step before query review;
- replacing the existing stable shop identity or downstream domain merge;
- deploying or mutating AWS resources;
- provider smoke calls without separate approval; or
- assigning implementation or changing any AWS deployment-approval stop.

## 9. Planning status

This document records the agreed product-level action plan but is not an
assignable execution checklist. It has now been compiled into the eight-artifact
package named at the top of this file. That package remains `DRAFT / NOT
ASSIGNABLE`. The requester has closed the active-state and paid-cost choices;
dependency/build proof and any remaining decision-completeness corrections
recorded in the package still must close before an implementation window can be
assigned.
