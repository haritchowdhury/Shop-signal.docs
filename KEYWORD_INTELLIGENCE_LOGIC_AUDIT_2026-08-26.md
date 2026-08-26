# Keyword Intelligence Logic Audit

**Date:** 2026-08-26  
**Scope:** Keyword-specific collection, normalization, deduplication, clustering,
scoring, recommendation, selection, query transformation, Google probing,
dashboard projection, and downstream Shopify acceptance.  
**Method:** Read-only source and contract inspection, comparison with the Python
reference, focused executable probes, focused test execution, and sanitized
read-only inspection of recent completed research results.  
**Code changes:** None.

## 1. Executive conclusion

The durable worker and pipeline engineering is mostly sound, but the keyword
intelligence itself is not a good general-purpose recommendation engine.

The Node.js implementation closely preserves the old Python implementation.
That implementation is apparel-specific and its scoring, clustering, lane, and
recommendation rules do not enforce concept diversity. Python parity therefore
preserved the source system's weaknesses; parity is not evidence that the
recommendations are useful.

There are also semantic discontinuities later in the flow:

- the Google probe now accepts a research-backed query with any usable
  MyShopify result regardless of semantic relevance;
- downstream storefront processing can reject that same verified Shopify store
  as the wrong category or as insufficient category evidence;
- the new AI product/non-product query classifier is outside the durable paid
  attempt and handoff identity protocols;
- the dashboard combines market-specific keyword metrics with cumulative
  cluster and summary metrics.

These problems can be corrected without redesigning the Lambda, SQS, S3,
database coordination, or transaction architecture.

## 2. Current implemented flow

```text
1-5 seeds
  -> US suggestions + related-keyword requests
  -> first-occurrence merge, max 60/seed and 300 total
  -> one US keyword-overview screen
  -> discard missing/zero-volume and informational candidates
  -> lexical deduplication
  -> clothing-specific lane/facet classification
  -> clothing-specific Jaccard clustering
  -> relative opportunity scoring
  -> recommended flag calculated independently per keyword
  -> top 200 US shortlist
  -> keyword overview in eight additional markets
  -> cumulative nine-market recomputation
  -> default-select every active recommended keyword, max 100
  -> pairwise duplicate/conflict analysis
  -> one batched AI product/non-product classification
  -> /products or root Shopify Google query
  -> Google Custom Search probe
  -> discovery and identity resolution
  -> storefront category-fit validation
  -> lead extraction and downstream enrichment
```

## 3. Live-result evidence

The most recent inspected completed research was:

- research ID: `kr_x3aSSK04BkMHrbsfBf8Yy4bO`
- seed: `Clothing`
- active keywords: 36
- clusters: 19
- recommended keywords: 8
- recommended clusters: 1

The eight recommended keywords were:

1. `clothing shopping near me`
2. `clothing shopping stores near me`
3. `clothing store close to me`
4. `clothing store closest to me`
5. `clothing store near me`
6. `walmart women's clothes clearance`
7. `walmart womens clothing new arrivals`
8. `women's walmart clothing`

They occupy three stored cluster IDs but represent essentially two semantic
concepts: local clothing stores and Walmart women's clothing.

Running the exact eight-row set through the production
`analyzeSelectionConflicts()` logic found zero conflicts.

The same result also contained obvious low-quality candidates such as:

- `4.12 4 clothing store`
- `clothing atore near.me`
- `supreme supreme clothing`

The earlier `online clothing` research recommended only
`cheap clothes under $5`, despite containing many more plausible online-store
phrases.

This demonstrates that the problem is present in the stored result, not merely
in dashboard rendering.

The saved selection on the latest inspected research still contained all 36
active rows. That research was published under the previous default-selection
behavior. The current source now selects recommended active rows only; existing
persisted selections are correctly not rewritten retroactively.

## 4. Critical findings

### 4.1 Classification and clustering are clothing-specific

`email_scraper/src/keyword-intelligence/cluster.js` hardcodes:

- clothing, fashion, and apparel vocabulary;
- women, men, kids, baby, and family audiences;
- activewear, streetwear, swimwear, outerwear, tops, bottoms, dresses,
  underwear, sleepwear, footwear, and apparel accessories;
- petite, maternity, oversized, plus-size, and big-and-tall fits;
- clothing-specific generated cluster labels.

This is an accurate port of `KeywordSearchVolume/pipeline/cluster.py`, but the
reference implementation itself is not category-agnostic.

Executable classification examples from the current production function:

| Keyword | Current lane |
|---|---|
| `pickleball store` | `brand_competitor` |
| `best ceramic mugs online` | `brand_competitor` |
| `walmart women's clothes clearance` | `category_discovery` |
| `walmart womens clothing new arrivals` | `category_discovery` |

This produces errors in both directions:

- ordinary non-clothing store discovery is classified as branded demand;
- actual branded demand can pass as unbranded category discovery;
- arbitrary categories receive empty or misleading facets;
- clustering and generated labels remain apparel-shaped.

### 4.2 Recommendation is per keyword, not per concept

`email_scraper/src/keyword-intelligence/score.js` sets a keyword as recommended
when its opportunity score is at least 55 and it has no blocking flag.

`email_scraper/src/keyword-intelligence/selection.js` then selects every active
recommended keyword, up to 100. It does not consider:

- whether several recommendations belong to the same cluster;
- whether the cluster itself is recommended;
- whether another keyword expresses the same user intent;
- whether one representative already covers that concept;
- diversity across seeds, lanes, categories, or markets.

Consequently, multiple variations of one concept can all be recommended. A
keyword can also be recommended while its containing cluster is not.

### 4.3 Duplicate detection cannot detect the observed repetition

Deduplication and selection conflict analysis use:

- ASCII-oriented tokenization;
- a small alias table;
- singularization;
- compact punctuation-insensitive equality;
- token-set Jaccard similarity at `0.88`.

This is effective for extremely close lexical variants, but not semantic
equivalents such as:

- `clothing shopping near me`
- `clothing store close to me`
- `clothing store closest to me`

The correct product distinction is:

- retain all calculated rows and metrics;
- identify concept-equivalent alternatives;
- recommend one representative per concept;
- allow the user to deliberately select alternatives;
- never silently delete user selections.

Lowering the Jaccard threshold alone is not a sufficient fix because it would
also merge unrelated phrases that merely share common category words.

### 4.4 Opportunity scores are population-relative

Keyword volume is normalized against the maximum volume in the current result.
CPC is normalized against the maximum CPC in the current result.

Therefore, the score for one keyword changes when an unrelated keyword enters
or leaves the candidate population.

An executable probe used identical candidate metrics in two populations:

- against a weak peer: score `57`, recommended;
- against a strong peer: score `42`, not recommended.

Only the peer changed. The candidate did not.

Consequences:

- 55 is not an absolute quality threshold;
- scores are not comparable between research runs;
- a weak candidate can look strong in a weak candidate set;
- one extreme phrase can suppress otherwise unchanged candidates;
- low difficulty and competition can push low-quality phrases above the
  threshold.

### 4.5 Cluster scoring rewards variant repetition

The clusterer calculates an overlap-adjusted volume but cluster opportunity
scoring uses `rawVariantVolume`.

As a result, a cluster can receive more volume credit because it contains many
similar variants. The system recognizes possible volume overlap for display but
does not use the adjusted value for recommendation scoring.

### 4.6 Google-probe and downstream storefront semantics disagree

The research-backed query probe currently requires:

- at least one usable result;
- at least one distinct literal MyShopify host;
- zero relevant-result minimum;
- zero relevance-ratio minimum;
- zero query-score minimum.

This matches the recent rule that semantic relevance should not reject a query
when it finds Shopify stores.

Later, `email_scraper/src/storefront-validator.js` and
`email_scraper/src/pipeline.js` still apply category-fit semantics. A verified
Shopify store may be rejected as:

- `wrong_category`;
- `wrong_store_type`;
- `insufficient_store_evidence`.

The latest desired rule—accept any verified Shopify store—is therefore not
implemented end to end.

If that behavior is changed, it should be scoped to runs whose
`queryPlanSource` is `keyword_research`, so legacy discovery behavior need not
change unintentionally.

### 4.7 AI query classification is outside durable idempotency

`query-intent-classifier.js` performs one structured Luna call for 1-100
selected items. Its output shape and order validation are sensible.

Its placement is not durable:

1. The selection fingerprint is calculated before classification.
2. The external AI call occurs before the handoff transaction.
3. `product` and `initialQuery` are not in the durable idempotency fingerprint.
4. Retrying the same `clientRequestId` calls the model again before discovering
   an existing handoff.
5. The generic HTTP client permits one automatic POST retry.
6. Model, prompt revision, output, cost, and attempt state are not represented
   in a paid-attempt ledger.

Concurrent or ambiguous retries can therefore classify the same selection more
than once, incur repeated cost, and let whichever transaction wins determine
the durable classification without recording why.

## 5. High-severity defects

### 5.1 Duplicate canonical selection chooses the worse calculated row

The intended canonical ranking is:

1. calculated before manual;
2. higher opportunity score;
3. higher volume;
4. shorter keyword;
5. deterministic lexical and ID tie-breaks.

The implementation sorts opportunity and volume ascending. An executable
example produced:

- `leather handbags`: score 10, volume 100;
- `leather handbag`: score 90, volume 1,000;
- current canonical suggestion: the score-10 row.

This is a direct implementation defect in
`email_scraper/src/keyword-intelligence/selection.js`.

### 5.2 Per-market cluster views are not per-market

The backend defines `marketClusterMetrics()` but does not call it when creating
the persisted result.

The result contains per-market keyword metrics but only cumulative cluster
metrics. The frontend's `currentClusterMetric()` ignores the selected market
and returns the cumulative cluster unchanged.

The dashboard therefore combines:

- market-specific keyword volume and CPC;
- cumulative cluster headline volume;
- cumulative cluster opportunity and trend;
- cumulative recommendation state;
- cumulative facets and lane counts.

The hero also retains cumulative active/recommended/cluster counts while the UI
says that a single market is being viewed.

### 5.3 No junk-quality filter exists

The only blocking flags are:

- volume below 100;
- one-word volume at least 200,000;
- declining trend;
- detected `brand_competitor` lane;
- informational intent.

There are no quality checks for:

- malformed numeric phrases;
- repeated tokens;
- likely typos;
- incomplete phrases;
- retailer and marketplace names missed by the lane classifier;
- boilerplate location variants;
- suspicious punctuation;
- navigational phrases missed by the provider intent field.

This allows candidates such as `4.12 4 clothing store` to reach a recommendation
score of 75.

### 5.4 Request and response keyword-length contracts conflict

Keyword overview requests permit keyword strings up to 160 characters. The
normalized `keywordMarketMetricSchema` permits only 100.

An executable probe confirmed:

- a 120-character overview request passes request validation;
- a successful response containing that same keyword fails normalized-result
  validation.

The paid provider response is then settled as
`KEYWORD_PROVIDER_CONTRACT_MISMATCH`.

### 5.5 Market coverage does not influence recommendation

Cumulative search volume sums the volumes available across markets, while CPC,
competition, difficulty, and commercial intent are volume-weighted.

The recommendation score does not consider:

- how many of the nine markets returned the keyword;
- whether it exists in only one market;
- whether its demand is broad or isolated;
- whether missing markets should reduce confidence.

A sparse one-market keyword can compete directly with a broadly supported
nine-market keyword.

### 5.6 Informational phrases are removed before full-market research

The US anchor screen removes informational candidates before creating the
200-keyword shortlist. Those candidates:

- are never researched in the other eight markets;
- never reach the final dashboard;
- cannot be selected manually later.

This was part of the frozen Python-parity behavior, but it must now be an
explicit decision if the product is intended to support arbitrary research and
arbitrary queries.

## 6. Medium findings

1. `minClusterSize` and `clusterLabelStrategy` exist in configuration but are
   unused by clustering.
2. `maxAttempts`, `backoffBaseSeconds`, and `backoffMaxSeconds` appear in the
   configuration, but repository retry behavior uses hardcoded values. The
   effective attempt ceiling is five.
3. Edited query duplicate detection is case-sensitive after NFKC and whitespace
   normalization. Google-equivalent case variants can pass.
4. The UI calls every calculated selected item “Recommended,” even when a user
   deliberately selects a non-recommended calculated keyword.
5. `informationalDropped` counts market occurrences rather than unique phrases,
   so it can be misread as the number of unique dropped keywords.
6. Expansion-manifest `candidates[].seeds` retains only the first seed that
   introduced a phrase. Final result reconstruction correctly rebuilds all
   source seeds from `bySeed`, but intermediate provenance is incomplete.
7. The clustering and duplicate tokenizers are ASCII-oriented despite the
   nine-market configuration including German and French language contexts.
8. A failed Google provider call marks its query invalid, and confirmation
   requires every row to be valid. Weak semantic probes are nonblocking, but a
   transient probe failure blocks the entire selected set.

## 7. Specification and test drift

The frozen product contract and decision ledger still require:

- direct Python parity;
- lane-based query mapping;
- strict query grammar and source relevance;
- no LLM query generation;
- no scoring or clustering redesign.

The current source instead contains:

- AI product/non-product classification;
- arbitrary editable query text;
- relaxed semantic probe acceptance;
- recommended-only default selection for new results.

Focused verification observed:

- Python parity suite: pass;
- selection suite: pass under the new recommended-only behavior;
- query-mapper suite: 5 pass, 4 fail.

The four mapper failures are stale tests expecting the old lane mapping, query
punctuation restrictions, and relevance rule.

There is no dedicated test suite for the new AI classifier, its prompt/output
contract, repeated-call behavior, idempotency, or cost ambiguity.

This demonstrates that Python parity can be green while recommendation quality
is poor, and that the current suite is not a trustworthy oracle for the newer
query behavior until the contract and tests are versioned together.

## 8. Logic that is sound and should be preserved

The following areas are comparatively strong:

- durable asynchronous research;
- task and aggregation leases;
- generation and token fencing;
- deterministic request and artifact fingerprints;
- S3-before-terminal publication;
- immutable validated artifacts;
- normalized provider cache;
- DataForSEO attempt and cost ledger;
- pre-call reservation and the $3 research cap;
- conservative ambiguity handling;
- US-only expansion and nine-market overview topology;
- owner-scoped persisted results;
- atomic result and default-selection publication;
- selection revision CAS;
- stable selection-item lineage;
- one retained selection item to one run query;
- bounded recovery;
- maximum limits of 5 seeds, 300 anchor candidates, 200 shortlisted keywords,
  200 draft items, and 100 final items.

The correction should avoid reopening the Lambda/SQS/S3/database state-machine
architecture unless a new defect is independently demonstrated there.

## 9. Selective-change map

### 9.1 Candidate retention

Current behavior:

- raw provider candidates without usable volume are removed;
- informational candidates are removed at the US anchor;
- active metric-bearing rows are retained after lexical deduplication.

Selectable change:

- retain informational metric-bearing rows for dashboard/manual selection;
- add explicit quality flags rather than deleting low-quality phrases;
- decide whether the 200-row multi-market cost cap continues to require a
  quality-based US shortlist.

### 9.2 General classification

Current behavior:

- apparel vocabulary determines facets, concepts, lanes, and labels.

Selectable change:

- replace it with category-agnostic classification of product concept,
  retailer/brand, store intent, local intent, informational intent, and quality;
- preserve seed-relative provenance independently of classifier output;
- version the new classifier rather than silently changing v1 results.

### 9.3 Clustering

Current behavior:

- lexical topic-token Jaccard;
- complete-link style membership check;
- only brand-vs-nonbrand compatibility boundary;
- apparel-specific labels.

Selectable change:

- cluster by semantic product/business concept plus intent;
- keep store, local, product, brand, and informational intent boundaries
  explicit;
- use one representative per concept for recommendation while retaining every
  row for inspection;
- do not attempt to fix this only by lowering the Jaccard threshold.

### 9.4 Scoring

Current behavior:

- score relative to maximum volume/CPC in the same run;
- weight volume, commercial intent, trend, inverse difficulty, inverse
  competition, and CPC;
- recommend at 55 with no blocking flag.

Selectable change:

- use stable/calibrated volume and CPC transforms;
- add data-quality and market-coverage confidence;
- decide explicitly whether lower competition should increase discovery value;
- score clusters using adjusted rather than raw repeated-variant volume;
- separate descriptive opportunity score from recommendation selection.

### 9.5 Recommendation-set construction

Current behavior:

- every individually passing keyword is recommended;
- cluster recommendation is informational only;
- default selection uses all recommended rows, max 100.

Selectable change:

- rank representatives within each concept;
- select one representative per concept first;
- optionally add a second member only when it represents a materially distinct
  lane, market, audience, or product intent;
- retain all other rows as non-default alternatives;
- preserve the maximum of 100 final rows.

### 9.6 Duplicate/conflict review

Current behavior:

- exact/compact/Jaccard conflicts only;
- conflict blocks finalization;
- canonical suggestion currently contains an ascending-score defect.

Selectable change:

- correct canonical score/volume ordering immediately;
- distinguish lexical duplicate, semantic equivalent, and merely related;
- block only actual duplicate/equivalent final selections;
- show related alternatives without forcing deletion if desired.

### 9.7 AI product-query classification

Current behavior:

- one Luna call returns `product:boolean` for every selected keyword;
- product true uses `site:myshopify.com/products`;
- false uses `site:myshopify.com`.

Selectable change:

- preserve the one-call batch design;
- make classification durable and replayable;
- include model, prompt/schema revision, classification output, and its
  fingerprint in the handoff identity;
- prevent automatic duplicate POST calls after ambiguous transport failures;
- optionally expose the product/root decision in query review for user edits.

### 9.8 Query review and Google probing

Current behavior:

- exactly one row per selection item;
- arbitrary nonempty text up to 200 characters is accepted;
- rows may be edited/reordered but not added/deleted;
- every row is probed;
- one MyShopify host is enough regardless of semantic title/snippet relevance.

Selectable change:

- preserve arbitrary query editing;
- make duplicate sequences case-insensitive;
- decide whether probe transport failure blocks all confirmation or remains
  visible with an explicit user retry/override path;
- retain probe evidence even when semantic relevance is nonblocking.

### 9.9 Downstream Shopify acceptance

Current behavior:

- query probing is relaxed;
- lead processing still enforces seed/category fit.

Selectable change:

- for `queryPlanSource=keyword_research`, accept a verified active Shopify store
  independent of seed/category text;
- retain category-fit evidence as descriptive metadata rather than a rejection
  reason;
- preserve stricter legacy semantics for legacy query-planner runs if desired.

### 9.10 Dashboard and exports

Current behavior:

- keyword rows have per-market metrics;
- cluster rows and summary are cumulative;
- market filters mix both types.

Selectable change:

- persist exact per-market cluster and summary metrics; or
- explicitly label cluster and summary sections cumulative while market keyword
  metrics change;
- correct misleading “Recommended” labels on manually selected
  non-recommended calculated rows.

## 10. Coupling boundaries

Changes that can be implemented independently:

- canonical duplicate suggestion ordering;
- 100-vs-160 keyword contract mismatch;
- case-insensitive edited-query duplicate detection;
- truthful selection labels;
- cumulative-vs-market UI labeling.

Changes that should be designed together:

1. taxonomy, lane classification, clustering, scoring, recommendation, and
   semantic duplicate analysis;
2. AI classification, paid-call semantics, snapshot versioning, and handoff
   idempotency;
3. Google-probe acceptance and downstream storefront acceptance;
4. per-market cluster persistence, summary calculation, exports, and dashboard
   presentation;
5. source behavior, product contract, decision ledger, focused tests, and
   deployment version.

## 11. Recommended correction order

1. Decide the desired recommendation semantics using real examples from the
   completed research results.
2. Replace the clothing-specific classification boundary with a general
   concept/intent model.
3. Separate scoring from recommendation-set diversity.
4. Correct duplicate/conflict semantics and the canonical-order defect.
5. Align Google probing and downstream Shopify acceptance.
6. Make the Luna classification durable and idempotent.
7. Correct market-specific dashboard semantics.
8. Resolve bounded schema and UI defects.
9. Version the contract and rewrite focused behavioral tests.
10. Run sanitized real-seed acceptance cases before redeployment.

The first redesign should focus on classification, clustering, scoring,
recommendation, and duplicate semantics. Those are the components producing the
observed poor recommendations. Query transformation and AWS durability are
separate concerns and should not be mixed into that redesign unnecessarily.
