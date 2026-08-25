# Jina, Browserless, Firecrawl, and Lambda Scaling Analysis

Status: decision support and experiment record; not an execution authority  
Prepared: 25 August 2026  
Scope: StoreSignal AWS lead pipeline, specifically the rendered-page fallback and multi-user capacity

## 1. Executive conclusion

The local experiment supports Jina Reader as a credible replacement for only the
Browserless rendering fallback. It does not support replacing domain discovery,
ordinary HTTP fetching, page ranking, lead extraction, scoring, persistence, or
aggregation.

The experiment processed 72 domains from a completed AWS run through the existing
lead pipeline with ordinary HTTP first and Jina substituted only at the renderer
dependency. It produced:

| Outcome | Original completed run | Local Jina experiment | Difference |
|---|---:|---:|---:|
| Qualified | 61 | 65 | +4 |
| Rejected | 5 | 6 | +1 |
| Failed | 6 | 1 | -5 |
| Total | 72 | 72 | 0 |

There was no observed lead-quality regression in this sample. Qualification rose
from 84.72% to 90.28%, and failure fell from 8.33% to 1.39%. This is encouraging,
but it is not proof that every site or future run will perform at least as well.
The live web changed between executions, and the experiment did not retain exact
Jina call counts, per-call token usage, cache state, or latency percentiles.

For multiple customers, the important limits are not all Lambda limits:

- AWS permits 1,000 concurrent executions in the Region, but at least 100 must
  remain unreserved. Therefore at most 900 can be assigned as reserved
  concurrency across every function in the Region.
- Jina's standard paid key is the rendered-fallback bottleneck at 50 concurrent
  requests and 500 requests per minute.
- Jina Premium raises that to 500 concurrent requests and 5,000 requests per
  minute.
- If CrUX is disabled for future runs, its 150-query-per-minute project quota no
  longer limits completed-run throughput.
- If DataForSEO remains enabled, its Labs limit and the current two-request
  internal scope concurrency imply approximately 12 concurrent Traffic Workers
  at an 80% provider-concurrency budget.
- Neon transaction latency and connection pressure must be measured before the
  highest proposed Lambda allocations are called production-safe.

The useful capacity envelopes are:

| Scenario | Proposed reserved concurrency | Principal ceiling |
|---|---:|---|
| Current local template, including the separate Keyword Worker | 12 | Frozen initial settings |
| Conservative first paid-Jina rollout with current CrUX path | 49 | CrUX and unproven global throttling |
| No CrUX, standard paid Jina, no shared Jina gate | 233 | Jina 50 concurrent |
| No CrUX, Jina Premium, no shared Jina gate | 593 | Jina 500 concurrent |
| No CrUX, Jina Premium, shared Jina gate | 843 | AWS/Neon and direct-HTTP mix |

The 843 allocation is an upper design target, not a setting to apply in one
deployment. It requires a distributed Jina concurrency/RPM gate, Neon load
evidence, SQS backlog monitoring, provider-cost alarms, and a staged ramp.

## 2. Authority and scenario boundary

The active AWS architecture still requires both CrUX REST and CrUX BigQuery and
locks the initial discovery, lead, and traffic concurrency. Removing CrUX or
changing provider economics is a future product/architecture decision and needs
a decision-complete corrective specification before production changes.

This document therefore separates:

1. **Observed current behavior:** repository source, production execution
   evidence, and the local Jina experiment.
2. **Provider-documented facts:** public pricing, concurrency, and rate limits
   retrieved on 25 August 2026.
3. **Calculated estimates:** throughput and cost derived from stated formulas.
4. **Future scenario:** CrUX disabled for new runs and Jina replacing only the
   renderer fallback.

Nothing in this document authorizes AWS mutation, provider cutover, CrUX removal,
secret installation, production dispatch, database writes, or concurrency
changes.

## 3. Exact lead-pipeline boundary

The existing domain lead path is:

```text
one stable domain task
  -> validate the candidate and same-store hostname set
  -> fetch the storefront over ordinary HTTP
  -> discover and rank at most five same-store pages
  -> fetch ranked pages over ordinary HTTP first
  -> classify each ordinary response as usable or render-required
  -> send only render-required page URLs to the renderer dependency
  -> merge ordinary and rendered documents in ranked order
  -> run the existing extraction, validation, qualification, scoring,
     lead-shape generation, and CSV serialization
```

The boundary owner is:

- `email_scraper/src/aws-pipeline/lead/domain-page-fetcher.js`
  - export: `fetchAwsDomainPages()`
  - fixed maximum: five ranked pages
  - ordinary HTTP before rendered fallback
  - fallback dependency name: `executeBrowserless`
- `email_scraper/src/aws-pipeline/services/lead-worker.js`
  - one stable domain per durable task/message
  - owns attempt markers, leases, S3 artifact production, and Neon terminal state
- `email_scraper/src/pipeline.js`
  - owns the retained lead discovery, extraction, qualification, and scoring

The local test does not fork or reimplement those business decisions. It injects
a Jina executor into the existing `executeBrowserless` seam.

### What is replaced

```text
executeBrowserlessDomainBatch(input)
            becomes, for the local test only
executeJinaDomainBatch(input)
```

Both accept the same narrow input concept:

```text
pages[]
allowedHostnames[]
taskContext
```

Both return renderer documents associated with the requested URL plus bounded
diagnostics and an early-stop reason.

### What is not replaced

- confirmed query generation or discovery;
- stable shop/domain identity;
- domain deduplication and provenance;
- sitemap/internal-page discovery;
- page ranking;
- ordinary HTTP fetching and usability assessment;
- lead extraction, contact validation, store-fit qualification, or scoring;
- RunStore/Lead/Profile behavior;
- SQS, S3, Neon, leases, fencing, recovery, or aggregation;
- CSV schema; or
- optional AI normalization.

That is the required preservation boundary for a future production substitution.

## 4. Local experiment implementation

### Source files

| File | Role |
|---|---|
| `email_scraper/scripts/run-leads-with-jina.js` | Loads a completed published AWS run, processes every discovered RunStore through the retained lead pipeline, and writes only qualified leads to CSV. |
| `email_scraper/scripts/lib/jina-render-fallback.js` | Jina Reader renderer adapter with the Browserless-compatible dependency shape. |
| `email_scraper/test/jina-fallback-test-script.test.js` | Deterministic tests for browser-rendered HTML and the HTTP-first boundary. |
| `email_scraper/package.json` | Defines `test:jina-leads`. |
| `email_scraper/data/jina-tests/<run-id>-qualified-leads.csv` | Default ignored experiment output; contains customer contact data and must not be committed. |

The implementation is present in backend commit `4f9d6ce` (`jona fallback
experiment`). The root analysis document does not duplicate the source so that
the runnable implementation and its tests remain the single source of truth.

### Preconditions

- `DATABASE_URL` points to the database containing the completed run.
- `JINA_API_KEY` is available only through the environment.
- The run must be an AWS run with `state=completed`, `stage=completed`, and
  `resultsAvailable=true`.
- The run's immutable provider snapshot must have AI normalization disabled;
  this isolated experiment never dispatches OpenAI normalization.

### Command

Run from `email_scraper/`:

```bash
npm run test:jina-leads -- <run-id>
```

Optional explicit output:

```bash
npm run test:jina-leads -- <run-id> data/jina-tests/result.csv
```

Focused deterministic verification:

```bash
node --test test/jina-fallback-test-script.test.js
```

Latest verification on 25 August 2026: exit 0, one test file passed, zero
failures, approximately 120 ms total.

### Preserved local limits

The experiment intentionally retains:

- domain concurrency two;
- at most five ranked pages per domain;
- sequential Jina rendering within one domain;
- 45-second total renderer ceiling;
- eight-second navigation hint per Jina request;
- 48-second outer client ceiling inherited conceptually from the production
  renderer margin;
- strict same-store final-URL attribution;
- public-URL/SSRF validation before and after rendering;
- maximum rendered HTML size of 1,000,000 UTF-8 bytes;
- no request retry in the Jina adapter;
- early stop after sufficient email/telephone evidence; and
- no storage or logging of the Jina credential.

The Jina request uses:

```text
GET https://r.jina.ai/<target-url>
Authorization: Bearer <JINA_API_KEY>
X-Engine: browser
X-Respond-With: html
X-Timeout: 8
X-No-Cache: true
```

The strict response projection consumes only successful Jina envelopes with a
validated final URL, rendered HTML, and a 2xx target HTTP status.

### What the local script deliberately does not do

- It does not enqueue or acknowledge SQS messages.
- It does not write AWS `runs/` artifacts.
- It does not mutate Neon lead, profile, traffic, ownership, or coordinator
  state.
- It does not dispatch Browserless.
- It does not dispatch OpenAI normalization.
- It exports only qualified leads.
- It does not retain raw provider response bodies.

The local script also does not exercise the production Lead Worker's durable
renderer-attempt marker. A production Jina change must preserve or version that
pre-call ambiguity barrier rather than bypassing it.

## 5. Experiment results

### Input and output

| Measurement | Result |
|---|---:|
| Completed AWS run selected | One published run with the most useful lead count |
| Discovered RunStore domains | 72 |
| Local domain concurrency | 2 |
| Qualified CSV rows | 65 |
| CSV physical lines | 66, including header |
| Rejected | 6 |
| Failed | 1 |
| Approximate wall time | 4.5 minutes |

No production identifier, domain list, email address, telephone number, or raw
HTML is copied into this document.

### Derived experiment throughput

```text
wall throughput = 72 domains / 4.5 min = 16 domains/min

slot service estimate
  = 270 seconds * 2 slots / 72 domains
  = 7.5 slot-seconds/domain
```

The corresponding rough lead-stage estimates are:

| Lead Lambda concurrency | Domains/min at 7.5 s | 72-domain run-equivalents/min |
|---:|---:|---:|
| 2 | 16 | 0.22 |
| 10 | 80 | 1.11 |
| 20 | 160 | 2.22 |
| 40 | 320 | 4.44 |
| 400 | 3,200 | 44.44 |

Production evidence also contains one corrected Lead Worker completion at 10.79
seconds. It is one invocation, not a population average. Using 7.5–10.79 seconds
as a planning band produces:

| Lead concurrency | Estimated domains/min | 72-domain run-equivalents/min |
|---:|---:|---:|
| 20 | 111–160 | 1.54–2.22 |
| 40 | 222–320 | 3.09–4.44 |
| 400 | 2,224–3,200 | 30.89–44.44 |
| 650 | 3,615–5,200 theoretical | 50.21–72.22 theoretical |

The 650 row is attainable only when enough domains finish through ordinary HTTP
while a shared gate prevents more than the allowed Jina requests. If every
domain needs rendering, provider throughput remains capped at the Jina gate.

### What the experiment proves

- The existing HTTP-first function can inject Jina only for failed or unusable
  pages.
- Jina can return browser-rendered HTML in the internal document shape needed by
  the retained extraction pipeline.
- The unchanged CSV writer produced 65 qualified records with the same output
  structure.
- The tested run did not show a qualification or failure regression.
- Jina is viable enough to justify a controlled production-shadow design.

### What the experiment does not prove

- statistical equivalence across categories, regions, bot defenses, or time;
- exact Jina cost per domain;
- exact Jina calls per domain or fallback incidence;
- p50, p95, or p99 latency;
- behavior at 50 or 500 concurrent requests;
- production crash/retry ambiguity safety;
- a guarantee of no performance drop;
- DataForSEO, Neon, S3, SQS, or final-publication capacity; or
- that CrUX can be removed without a score/product-contract decision.

## 6. Provider comparison

Provider facts in this section were retrieved from official public pages on
25 August 2026. Prices shown by providers using annual billing are normalized
only where the arithmetic is explicit. Taxes and custom enterprise pricing are
excluded.

### Concurrency and pricing summary

| Provider | Free/dev | Entry paid | Higher self-serve | Concurrency ceiling | Billing unit |
|---|---|---|---|---:|---|
| Browserless | 1,000 units, 2 browsers | $25/month annual, 20k units, 10 browsers | $140/180k/40; $350/500k/100 | 100 self-serve | One unit per started 30 seconds of browser connection; proxy/CAPTCHA extra |
| Firecrawl | 1,000 credits, 2 concurrent requests | $16/month annual, 5k credits, 5 concurrent | $83/100k/25; $333/500k/50; $599/1m/100 | 100 self-serve | Normally one credit per successfully scraped page; enhanced mode can cost five |
| Jina Reader | Free development tokens; Reader limits depend on key | $50 for 1 billion tokens, 50 concurrent, 500 RPM | $500 for 11 billion tokens, 500 concurrent, 5,000 RPM | 500 Premium | Output tokens returned by Reader |

Official sources:

- [Browserless pricing](https://cloud.browserless.io/pricing)
- [Browserless unit consumption](https://docs.browserless.io/overview/unit-consumption)
- [Firecrawl pricing](https://www.firecrawl.dev/pricing)
- [Firecrawl billing and credits](https://github.com/firecrawl/firecrawl-docs/blob/main/billing.mdx)
- [Firecrawl scrape API](https://docs.firecrawl.dev/api-reference/endpoint/scrape)
- [Jina Reader limits and pricing](https://jina.ai/reader/)
- [Jina API rate limits](https://api.jina.ai/docs)

Firecrawl's billing documentation and live pricing page currently disagree on
some plan concurrency values. This analysis uses the lower live pricing-page
values—25 Standard, 50 Growth, and 100 Scale—rather than assuming the larger
documentation values.

### Jina development allowance

Jina currently advertises a free 10-million-token toy/development allocation.
The pricing page marks it for non-commercial use. Reader without a key is also
available at a much smaller request allowance, while an authenticated free key
has account-level limits below the paid tiers. This is suitable for development
and bounded comparison runs, not for serving production customers.

At illustrative output sizes, 10 million tokens covers approximately:

| Average Reader output/page | Approximate pages covered |
|---:|---:|
| 10,000 tokens | 1,000 |
| 25,000 tokens | 400 |
| 50,000 tokens | 200 |

The experiment did not retain Jina's returned usage field, so its actual token
consumption cannot be reconstructed from the qualified CSV.

### Capability fit for this pipeline

#### Browserless

Advantages:

- exact programmable browser/session control;
- one `/function` request can visit several ranked pages sequentially;
- explicit early-stop behavior inside the session;
- strong fit for custom navigation, cookies, redirects, and browser automation.

Disadvantages:

- self-serve concurrency tops out at 100;
- each started 30-second interval consumes another unit;
- proxy bandwidth and CAPTCHA solving add units;
- a large multi-user fallback population needs Scale or Enterprise;
- the current architecture originally had only two-account concurrency.

#### Firecrawl

Advantages:

- known-URL `/scrape` is straightforward;
- normal scrape is one credit per successful page;
- rendering, proxy escalation, markdown/HTML, and extraction options are
  available;
- subscription page allowances are easy to model.

Disadvantages:

- billing is per page, while the current Browserless contract groups several
  pages into one domain session;
- enhanced mode can multiply cost to five credits per page;
- self-serve concurrency is below Jina Premium;
- its response and redirect/evidence contract would require a separate strict
  adapter and equivalence experiment;
- advanced JSON/LLM extraction is unnecessary because StoreSignal already owns
  extraction and scoring.

#### Jina Reader

Advantages:

- accepts the exact direct page URL already produced by StoreSignal;
- browser rendering can be requested while returning HTML;
- standard paid concurrency matches or exceeds mid-tier scraping plans;
- Premium concurrency of 500 is the best self-serve fit for many customers;
- the local adapter can occupy only the existing rendered-fallback seam;
- no separate discovery or extraction feature is required.

Disadvantages:

- one Reader request represents one URL, not a multi-page domain session;
- billing depends on output size, so returning full rendered HTML can be more
  expensive than short markdown;
- RPM and concurrency are shared key/account concerns and need a distributed
  gate at high Lambda concurrency;
- exact cost was not retained by the experiment;
- strict final-URL, response, retry, and ambiguity handling remain application
  responsibilities.

### Normalized cost estimates

#### Browserless

Subscription allowance cost per 1,000 one-unit sessions:

| Plan | Arithmetic | Effective included cost/1,000 units |
|---|---:|---:|
| Prototyping | $25 / 20,000 | $1.25 |
| Starter | $140 / 180,000 | $0.78 |
| Scale | $350 / 500,000 | $0.70 |

A session lasting 31–45 seconds consumes two units. The current design can render
up to five pages sequentially in one domain session, so Browserless cost is
session-time based rather than simply pages multiplied by unit price.

#### Firecrawl

Basic successful scrape cost per 1,000 pages using the headline annual plans:

| Plan | Arithmetic | Effective included cost/1,000 basic pages |
|---|---:|---:|
| Hobby | $16 / 5,000 | $3.20 |
| Standard | $83 / 100,000 | $0.83 |
| Growth | $333 / 500,000 | $0.67 |
| Scale | $599 / 1,000,000 | $0.60 |

Enhanced mode can consume five credits per page, making the corresponding
effective cost approximately five times larger.

#### Jina Reader

Headline token prices:

```text
standard: $50 / 1,000,000,000 tokens = $0.050 per 1M output tokens
premium:  $500 / 11,000,000,000 tokens = $0.04545 per 1M output tokens
```

Estimated standard-key cost per 1,000 rendered pages:

| Average output/page | Total output | Estimated cost |
|---:|---:|---:|
| 10,000 tokens | 10 million | $0.50 |
| 25,000 tokens | 25 million | $1.25 |
| 50,000 tokens | 50 million | $2.50 |
| 100,000 tokens | 100 million | $5.00 |

Therefore Jina is not automatically cheapest for every rendered HTML page. It
is especially attractive when output is compact or only a small fraction of
ranked pages reaches fallback. Full raw rendered HTML and several Jina requests
per domain can cost more than one Browserless session or a high-volume
Firecrawl basic scrape. Production telemetry must retain Jina output tokens and
requests per domain before selecting a cost winner.

### Practical provider choice

For this exact boundary:

1. **Jina is the strongest candidate** because StoreSignal already has direct
   ranked URLs and wants rendered HTML only.
2. **Browserless remains the strongest control option** for complicated
   multi-page browser behavior and can be economical when several pages fit in
   one short session.
3. **Firecrawl is viable but less boundary-aligned** unless its proxy success or
   operational reliability materially outperforms Jina in a direct equivalence
   test.

The provider decision should be made from a larger shadow corpus using success,
evidence fidelity, output tokens/credits/units, latency, and 429/5xx rates—not
headline price alone.

## 7. Lambda concurrency analysis

### AWS account rules

AWS documents a regional account concurrency pool of 1,000. Reserved concurrency
both reserves capacity for a function and caps that function. AWS requires at
least 100 executions to remain unreserved, so the maximum total reserved
concurrency is:

```text
1,000 regional limit - 100 mandatory unreserved = 900 maximum reserved
```

Sources:

- [AWS Lambda concurrency](https://docs.aws.amazon.com/lambda/latest/dg/lambda-concurrency.html)
- [AWS PutFunctionConcurrency rule](https://docs.aws.amazon.com/lambda/latest/api/API_PutFunctionConcurrency.html)
- [AWS SQS scaling](https://docs.aws.amazon.com/lambda/latest/dg/services-sqs-scaling.html)

SQS event-source `MaximumConcurrency` is independent of function reserved
concurrency and must not exceed it. AWS accepts mapping maximums from two
upward, so a function intentionally capped at one must omit the mapping maximum
and rely on reserved concurrency one.

The exact remaining regional allocation is unknown because the read-only AWS
inventory could not refresh an expired `storesignal-dev` SSO token. The figures
below assume no other reserved functions beyond those represented in the
current template. That assumption must be verified before deployment.

### Current local template settings

| Function | Memory | Timeout | Reserved concurrency | SQS mapping maximum |
|---|---:|---:|---:|---:|
| Discovery Worker | 512 MiB | 300 s | 1 | omitted |
| Domain Aggregator | 512 MiB | 300 s | 2 | 2 |
| Lead Worker | 512 MiB | 90 s | 2 | 2 |
| Lead Aggregator | 512 MiB | 300 s | 2 | 2 |
| Traffic Worker | 512 MiB | 900 s | 1 | omitted |
| Final Aggregator | 512 MiB | 300 s | 2 | 2 |
| Recovery | 512 MiB | 300 s | 1 | scheduled singleton |
| Keyword Worker | 1,024 MiB | 180 s | 1 | omitted |
| **Total** |  |  | **12** |  |

The infrastructure source is
`email_scraper/infrastructure/aws/template.yaml`.

The seven core lead/traffic-pipeline functions total 11. The separate Keyword
Worker makes the consolidated local-template total 12. A live-account inventory
is still required to prove whether every template function and any unrelated
Lambda currently share the same regional reserved-concurrency pool.

### Why the earlier recommendation was 49

The earlier 49 allocation was a first safe rollout under three assumptions:

1. CrUX remained part of the active pipeline.
2. Jina was on the standard paid tier without a distributed RPM gate.
3. Aggregator/Neon behavior had not been load-tested at larger multi-run
   concurrency.

The allocation was:

```text
Discovery 10
Domain Aggregator 5
Lead 20
Lead Aggregator 5
Traffic 1
Final Aggregator 5
Recovery 1
Keyword 2
Total 49
```

This was intentionally a canary/ramp target, not a claim that the 1,000 Lambda
quota should remain unused forever.

### CrUX as the earlier end-to-end ceiling

CrUX REST allows 150 queries per minute per Google Cloud project, and Google
states that the quota cannot be purchased higher.

The successful production run had 61 traffic-eligible leads. At an 80% operating
budget:

```text
150 RPM * 80% = 120 safe CrUX requests/min
120 / 61 = 1.97 comparable runs/min
```

At 100 eligible domains, the same calculation is 1.2 runs/min. Increasing Lead
Lambda far beyond the downstream CrUX rate would drain the lead queue faster but
would not raise sustained completed-run throughput.

Source: [CrUX API quota](https://developer.chrome.com/docs/crux/api).

### No-CrUX standard paid Jina envelope

Without a shared Jina gate, preserve 20% headroom under the provider's 50
concurrent-request limit:

| Worker | Proposed reserved concurrency | Reason |
|---|---:|---|
| Discovery | 100 | Parallel confirmed-query tasks; no Google or renderer call in the AWS discovery worker |
| Domain Aggregator | 25 | One fenced aggregation per completed run; bounded S3 work |
| Lead | 40 | 80% of Jina standard paid concurrency 50 |
| Lead Aggregator | 25 | More run-level capacity than the Lead stage can sustainably complete |
| Traffic/DataForSEO | 12 | 24/30 provider-concurrency budget divided by two internal calls |
| Final Aggregator | 25 | Run-level publication capacity with Neon protection |
| Recovery | 1 | Prevent overlapping recovery sweeps |
| Keyword | 5 | Existing provider throttle controls paid dispatch |
| **Total** | **233** |  |

Raising non-lead workers above these values would reserve more AWS capacity but
would not materially improve throughput while Lead remains capped at 40.

### No-CrUX Jina Premium envelope without a shared gate

| Worker | Proposed reserved concurrency | Reason |
|---|---:|---|
| Discovery | 100 | Feeds high-volume lead work |
| Domain Aggregator | 25 | Run-scoped aggregation |
| Lead | 400 | 80% of Jina Premium concurrency 500 |
| Lead Aggregator | 25 | Supports more run completions than the estimated Lead stage |
| Traffic/DataForSEO | 12 | DataForSEO provider-concurrency budget |
| Final Aggregator | 25 | Bounded final publication |
| Recovery | 1 | Singleton |
| Keyword | 5 | Separate throttled pipeline |
| **Total** | **593** |  |

At the published 7.9-second Jina average, 400 continuously occupied renderer
requests imply approximately 3,038 requests/minute, below an 80% Premium RPM
budget of 4,000. Faster responses can still breach RPM, so concurrency alone is
not a complete rate limiter.

### High-capacity no-CrUX envelope with a shared Jina gate

The Lead Lambda can exceed the renderer concurrency only if the application has
an account-wide gate that ensures no more than 400 simultaneous Jina requests
and approximately 4,000 requests/minute. Additional Lead Lambdas can perform
ordinary HTTP while renderer capacity is occupied.

| Worker | Proposed reserved concurrency |
|---|---:|
| Discovery | 100 |
| Domain Aggregator | 25 |
| Lead | 650 |
| Lead Aggregator | 25 |
| Traffic/DataForSEO | 12 |
| Final Aggregator | 25 |
| Recovery | 1 |
| Keyword | 5 |
| **Total** | **843** |

Account arithmetic:

```text
1,000 regional concurrency
- 100 mandatory unreserved
- 843 proposed reserved
= 57 additional reservable capacity
```

This is the largest useful allocation discussed, not the largest number AWS
will syntactically accept. It depends on these conditions:

- Jina Premium is active and its dashboard confirms the documented limits.
- A distributed limiter, not a per-process counter, gates concurrent and RPM
  usage across all warm Lambda environments.
- Waiting for the Jina gate cannot push the 90-second Lead Lambda beyond its
  task/renderer deadlines.
- The fallback remains sequential within each domain.
- Neon pooled connections, transaction latency, locks, and timeouts pass staged
  multi-run load tests.
- SQS mappings match function concurrency and produce no sustained throttles.
- Direct target sites are distributed enough that 650 HTTP-first workers do not
  create abusive per-host traffic.
- Provider cost and output-token alarms are active.

### DataForSEO after CrUX removal

The Traffic Worker currently executes DataForSEO scope waves with internal
concurrency two. DataForSEO documents 30 simultaneous requests for Labs APIs
and a general limit of 2,000 requests per minute.

```text
30 concurrent * 80% = 24 provider requests
24 / 2 requests per Traffic Worker = 12 Traffic Workers
```

Source: [DataForSEO rate and request limits](https://dataforseo.com/help-center/rate-limits-and-request-limits).

The last successful production run recorded ten external DataForSEO tasks and
actual cost of $0.1908. At continuous comparable completion rates, before cache
savings:

| Runs/min | DataForSEO cost/min | Cost/hour |
|---:|---:|---:|
| 10 | $1.908 | $114.48 |
| 25 | $4.770 | $286.20 |
| 40 | $7.632 | $457.92 |

Therefore provider economics may become the real customer-capacity limit after
CrUX is removed. If DataForSEO is also disabled, the traffic stage should
zero-count advance; Traffic concurrency can remain one and its 11 extra slots
can be reassigned.

### Aggregator and Neon caveat

The domain, lead, and final aggregators perform bounded S3 reads at internal
concurrency eight, while final publication contains substantial Neon work. The
maximum-cardinality tests prove correctness for 1,000 domains and 12,000 traffic
outcomes, but remote Neon latency has occasionally approached or exceeded
transaction targets during integration evidence.

Reserved concurrency 25 for each aggregator is therefore a capacity estimate,
not a proven database ceiling. Before increasing beyond it, collect:

- Prisma/Neon connection acquisition time and timeout counts;
- active/queued pooled connections;
- transaction p50/p95/p99;
- row-lock and serialization conflicts;
- stage lease renewals/losses;
- S3 request latency and throttling;
- final-publication retries; and
- Lambda maximum duration/memory.

## 8. Required production design for a Jina cutover

A production change should preserve the existing fallback seam and add only the
following renderer-specific pieces:

1. **Strict Jina snapshot configuration**
   - enabled flag;
   - endpoint identity;
   - response contract version;
   - browser engine and HTML-output mode;
   - per-request and per-domain deadlines;
   - maximum response bytes;
   - concurrency and RPM policy identifiers.

2. **Durable pre-call attempt marker**
   - written before the first Jina network request;
   - keyed by run, generation, stable shop/task, task input fingerprint, and
     page-plan fingerprint;
   - prevents a process restart from blindly repeating an unknown paid call;
   - contains no raw HTML, credential, or contact data.

3. **Distributed capacity gate**
   - account-wide, not one in-memory counter per Lambda;
   - enforces both concurrent requests and rolling RPM;
   - has bounded waiting compatible with the existing 45/90-second limits;
   - records privacy-safe 429, wait, and saturation metrics.

4. **Strict adapter and attribution**
   - exact observed Jina envelope only;
   - final URL must remain in the verified store hostname set;
   - 2xx target status and rendered HTML required;
   - raw provider bodies never leave the adapter.

5. **Cost telemetry**
   - Jina requests per domain;
   - output tokens per request/domain;
   - fallback incidence;
   - direct-versus-rendered document counts;
   - latency percentiles;
   - 429/5xx/timeout/contract-drift counts;
   - early-stop reason;
   - cost estimate attached to the provider attempt, without storing customer
     content.

6. **Shadow and rollback**
   - deterministic fixtures first;
   - a sanitized multi-category corpus;
   - controlled low-volume live shadow comparison;
   - no simultaneous Browserless and Jina charge for the same production task
     unless explicitly authorized as a bounded comparison;
   - configuration rollback to the prior renderer;
   - provider-call and output-equivalence gates before concurrency increases.

## 9. Recommended staged rollout

The following sequence maximizes eventual customer capacity without treating
the 843 design target as already proven:

### Stage A — Instrumented low-volume shadow

- Keep Lead concurrency at two to ten.
- Record exact fallback incidence, Jina calls, output tokens, latency, and
  outcomes.
- Compare a sanitized corpus with the existing renderer contract.
- Confirm the durable attempt marker and retry behavior.

### Stage B — Standard paid key

- Raise Lead concurrency through 10, 20, and 40.
- Do not exceed 40 without a shared gate or Premium.
- Alarm on Jina 429s, token rate, Lambda duration, failed leads, and SQS age.

### Stage C — Premium provider gate

- Enable the distributed 400-concurrent/4,000-RPM policy.
- Raise Lead concurrency through 100, 250, and 400.
- Prove Neon and aggregators with multiple simultaneous runs.
- If CrUX is disabled by a separate approved contract change, raise
  Traffic/DataForSEO gradually toward 12.

### Stage D — Direct-HTTP overlap

- Raise Lead concurrency from 400 toward 650 only after measuring what fraction
  completes without Jina.
- Prove gate wait time stays within task deadlines.
- Stop increasing if Jina saturation, Neon latency, provider cost, SQS retries,
  or target-site errors rise materially.

### Stage E — Account allocation review

- Refresh AWS SSO and inventory every regional function's reserved and
  provisioned concurrency.
- Confirm total reserved concurrency remains at or below 900.
- Preserve the mandatory unreserved pool and explicit headroom for the control
  plane and deployments.

## 10. Decision summary

- **Does Jina fit the task?** Yes. Direct ranked page URLs are already known,
  and the local experiment proved browser-rendered HTML can enter only the
  existing fallback seam.
- **Did the experiment show a quality drop?** No observed drop in this 72-domain
  run; it produced four more qualified leads and five fewer failures. This is
  not a universal guarantee.
- **Is Jina definitely cheaper?** Not for every page. It is token-priced, and
  full HTML can be large. It is likely attractive when fallback incidence and
  output size are controlled, but exact experiment cost was not captured.
- **Does Jina allow more concurrency?** Yes. Standard paid supports 50 and
  Premium 500, versus Browserless self-serve up to 100 and Firecrawl self-serve
  up to 100 on the current live pricing page.
- **Why was 49 proposed earlier?** It was a conservative first rollout while
  CrUX and unproven provider/Neon limits remained in scope, not the AWS maximum.
- **What is the high-throughput no-CrUX target?** Approximately 593 reserved
  concurrency without a shared Jina gate, or 843 with Premium, a shared gate,
  sufficient direct-HTTP work, and proven Neon capacity.
- **Can all 1,000 be reserved?** No. AWS requires at least 100 unreserved, so
  900 is the regional reserved-concurrency ceiling before subtracting other
  functions.
- **What limits the business after CrUX?** Jina tier, Neon behavior,
  DataForSEO cost/concurrency, and actual fallback/output-token distributions.

## 11. Evidence and references

Repository evidence:

- `AWS_ASYNC_DEPLOYMENT_DIRECTION.md`
- `TARGET_LAMBDA_SQS_S3_EXECUTION_FLOW.md`
- `PRELIMINARY_LAMBDA_SQS_S3_MIGRATION_PLAN.md`
- `FINAL_LAMBDA_SQS_S3_MIGRATION_EXECUTION_PLAN.md`
- `AWS_PIPELINE_EXECUTION_EVIDENCE.md`
- `email_scraper/docs/research/LAMBDA_SQS_S3_PAYLOAD_DISCOVERY_REPORT.md`
- `email_scraper/infrastructure/aws/template.yaml`
- `email_scraper/src/aws-pipeline/lead/domain-page-fetcher.js`
- `email_scraper/src/aws-pipeline/services/lead-worker.js`
- `email_scraper/src/aws-pipeline/services/traffic-worker.js`
- `email_scraper/src/enrichment/orchestrator.js`
- `email_scraper/src/aws-pipeline/keyword-intelligence/dataforseo-labs-adapter.js`
- `email_scraper/scripts/run-leads-with-jina.js`
- `email_scraper/scripts/lib/jina-render-fallback.js`
- `email_scraper/test/jina-fallback-test-script.test.js`

External references, retrieved 25 August 2026:

- [AWS Lambda concurrency](https://docs.aws.amazon.com/lambda/latest/dg/lambda-concurrency.html)
- [AWS reserved-concurrency API](https://docs.aws.amazon.com/lambda/latest/api/API_PutFunctionConcurrency.html)
- [AWS SQS event-source scaling](https://docs.aws.amazon.com/lambda/latest/dg/services-sqs-scaling.html)
- [Jina Reader](https://jina.ai/reader/)
- [Jina Search Foundation API limits](https://api.jina.ai/docs)
- [Browserless pricing](https://cloud.browserless.io/pricing)
- [Browserless unit consumption](https://docs.browserless.io/overview/unit-consumption)
- [Firecrawl pricing](https://www.firecrawl.dev/pricing)
- [Firecrawl billing documentation](https://github.com/firecrawl/firecrawl-docs/blob/main/billing.mdx)
- [Firecrawl scrape endpoint](https://docs.firecrawl.dev/api-reference/endpoint/scrape)
- [DataForSEO rate limits](https://dataforseo.com/help-center/rate-limits-and-request-limits)
- [CrUX API quota](https://developer.chrome.com/docs/crux/api)
