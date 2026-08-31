  The pipeline is doing its job. The recommendation engine is optimizing the wrong
  job. Below is a product review of that gap, grounded in the live Clothing result
  and the current scoring, clustering, and selection code.

  The actual product job

  A Shopify app developer is not buying keyword research. They are buying a short 
  list of Google queries that will surface independent Shopify merchants in their 
  niche, so downstream discovery, identity, traffic, and lead extraction can run.

  A good default selection therefore has to maximize:

  1. Merchant retrieval — site:myshopify.com actually returns real stores.
  2. Niche fidelity — those stores match the seed, not a drifted retailer or a
     local-maps intent.
  3. Independents — not Walmart, Amazon, Target, or marketplace names.
  4. New stores per query — each selected row should add merchants the others will
     not.
  5. Merchant quality — real businesses, not $5 junk and typos.

  The current engine was ported from KeywordSearchVolume: an apparel SEO opportunity 
  dashboard. It scores “would this phrase be a good keyword to rank for?” That is
  almost the inverse of “will this phrase find high-quality Shopify leads?”

  Python parity therefore preserved a source system that was never built for this
  buyer. The AWS/Neon/S3 machinery is not the problem. The locked contract even
  forbids a scoring redesign (EXC-KI-002). The live recommendations are what you get
  when that freeze is honored.

  What the live result proves

  Seed Clothing produced 36 active keywords, 19 clusters, and 8 recommended rows:

  • five local variants (clothing store near me, closest to me, shopping stores 
    near me, …)
  • three Walmart women’s variants

  analyzeSelectionConflicts() found zero conflicts. Those eight rows occupy three
  cluster IDs but only two user intents. Default selection then takes every
  recommended row.

  For this product that is a failure, not a ranking nit:

  ┌──────────────────────────────────┬──────────────────────────────────────────────┐
  │ Recommended phrase               │ What a Shopify-app buyer actually gets       │
  ├──────────────────────────────────┼──────────────────────────────────────────────┤
  │ clothing store near me and       │ Google Maps / local retail. Weak             │
  │ siblings                         │ site:myshopify.com yield. Highly overlapping │
  │                                  │ results.                                     │
  ├──────────────────────────────────┼──────────────────────────────────────────────┤
  │ walmart women's clothes …        │ A non-Shopify retailer. The brand flag       │
  │                                  │ missed it; the lane called it                │
  │                                  │ category_discovery.                          │
  ├──────────────────────────────────┼──────────────────────────────────────────────┤
  │ (not recommended) independent    │ The merchants the buyer actually wants.      │
  │ product/store phrases in the     │                                              │
  │ same 36                          │                                              │
  └──────────────────────────────────┴──────────────────────────────────────────────┘

  The earlier online clothing run recommending only cheap clothes under $5 is the
  same failure with the opposite flavor: the scorer preferred a low-competition
  bargain phrase, which is the worst lead cohort for an app developer (thin dropship,
  low willingness to pay).

  This is in the stored result. The dashboard is not inventing it.

  Where the logic disagrees with the buyer

  1. Opportunity score is an SEO formula

  Weights in config.js: volume 25%, commercial intent 25%, trend 20%, inverse
  difficulty 15%, inverse competition 10%, CPC 5%. Recommend if score ≥ 55 and no
  blocking flag.

  That rewards:

  • high volume relative to this run’s max
  • any commercial-ish modifier (near me is in the commercial-modifier list)
  • easy keywords (low difficulty, low competition)

  It does not reward:

  • likelihood of Shopify-hosted results
  • independence from big-box/marketplace names
  • distinctness from already-recommended concepts
  • merchant quality (luxury / specialist vs clearance / under $5)
  • niche match to the seeds

  Inverse competition is actively hostile here. The phrases that are easy in an SEO
  dataset are often local boilerplate, retailer navigational queries, and junk. The
  phrases that find real merchants (women's dresses online, organic cotton tee shop)
  look “harder” and lose.

  CPC is the one SEO metric that sometimes tracks merchant quality, and it is almost
  unused.

  Scores are also population-relative. The same keyword can be recommended in a weak
  set and rejected in a strong one. A user cannot learn what “55” means, and a weak
  seed like Clothing will systematically promote the least-bad junk in a bad
  candidate pool.

  2. Recommendation is per row, not per concept

  score.js flags each keyword independently. createDefaultSelection() then takes
  every recommended=true row, up to 100.

  Clusters exist, even compute recommendedForStoreDiscovery, and then do not 
  constrain recommendation or default selection. A keyword can be recommended while
  its cluster is not. Five “near me” paraphrases can all pass 55.

  That wastes the scarce resource. A research-backed run is capped at 100 queries × 
  10 Google results. Eight near-duplicate locals do not yield eight times the stores;
  they yield the same hosts with extra CSE spend and extra identity merge work. Most
  users will keep the default. Default selection is the product.

  3. Duplicate detection cannot see the repetition the buyer cares about

  Dedup and conflict analysis use compact signatures and token Jaccard at 0.88. That
  catches clothing store vs clothing stores. It does not catch:

  • clothing shopping near me
  • clothing store close to me
  • clothing store closest to me

  Those share intent (local clothing retail) but not a high token-set overlap once
  stopwords are stripped. Lowering 0.88 would also merge unrelated phrases that share
  clothing / store. Lexical similarity is the wrong tool for “same lead-finding
  job.”

  There is also a real bug in canonicalItem(): it sorts opportunity and volume
  ascending, so the conflict UI can suggest keeping the worse calculated row. Users
  who do try to clean duplicates can be steered toward the worse query.

  4. Classification is a clothing ontology pretending to be general

  cluster.js hardcodes apparel vocabulary, audiences, fits, and generated labels such
  as “women's clothing stores.” Anything outside that lexicon is an “unknown” token.

  The lane rule then does this:

  • unknown tokens + a channel word (store, shop, online) → brand_competitor
  • brand_competitor is a blocking flag → never recommended

  So pickleball store and best ceramic mugs online are branded demand and excluded.
  walmart women's clothes clearance stays category_discovery because walmart is
  unknown but the remaining tokens look like clothing category language.

  That is inverted for every non-apparel niche this product is supposed to serve, and
  it fails even inside apparel (Walmart is not a category). The four lanes
  (category_discovery, store_discovery, local_discovery, brand_competitor) are still
  a useful query-intent vocabulary. The problem is that membership is inferred from a
  clothing word list.

  5. Local and retailer demand are treated as commercial wins

  near me / closest correctly set local_discovery and a local channel facet. Then
  commercial-intent scoring boosts them because near me is a commercial modifier.
  Nothing blocks local from recommendation. Nothing has a retailer/marketplace
  denylist (walmart, amazon, target, etsy, ebay, costco, …).

  For SEO, local and big-box volume is real demand. For Shopify lead gen they are
  almost anti-signals: local is brick-and-mortar; Walmart is not a Shopify merchant.

  6. There is no junk filter

  Blocking flags are only: volume &lt; 100, one-word volume ≥ 200k, declining trend,
  brand_competitor, informational. Nothing flags 4.12 4 clothing store, clothing 
  atore near.me, or supreme supreme clothing. Those can still score in the 70s and
  become Google queries. Each one burns a slot in the 100-query budget.

  7. Informational drop happens too early, and for the wrong reason

  The US shortlist deletes informational candidates before the other eight markets.
  They never appear on the dashboard, so the user cannot rescue a useful best X / X 
  review phrase if DataForSEO labeled it informational.

  For lead gen, true how-to/wiki queries are usually correct to keep out of
  site:myshopify.com. Comparative commercial research (best ceramic mugs 2025) is
  often the opposite. The product currently has a blunt delete, not a visible “poor
  lead-finding intent” flag.

  8. Nine-market math is a dashboard cost, not a lead-quality signal

  Cumulative volume sums nine markets; recommendation ignores how many markets
  actually returned the keyword. A one-market fluke competes with a nine-market
  phrase. Cluster headlines stay cumulative while the UI implies a single-market
  view.

  Google probing is not nine-market. Lead finding is not nine-market. The $3 budget
  is spent producing an SEO-style international dashboard whose headline numbers then
  drive which queries get selected. If the buyer’s job is Shopify leads, that is the
  wrong place to spend both money and ranking influence.

  9. Probe acceptance and storefront rejection disagree — and “accept any Shopify 
  store” is not obviously the right fix

  Research-backed probes currently need one usable result and one MyShopify host.
  Relevance score is computed and ignored. Downstream, validateStorefront() can still
  reject wrong_category / wrong_store_type / insufficient_store_evidence from
  seed-derived vocabulary.

  That discontinuity is real. Blindly accepting every verified Shopify store for
  queryPlanSource=keyword_research would also be a product mistake if the buyer asked
  for a niche. Category-fit against the seeds is one of the few remaining niche
  filters. The better rule is:

  • do not reject a store because a single drifted keyword is a poor lexical match
  • do reject (or at least downrank) a store that does not match the research niche
  • keep category-fit as evidence even when it is not a hard reject

  Relaxing the probe made “we found a .myshopify.com URL” the success criterion. That
  is necessary but not sufficient for high-quality leads.

  10. Query mapping was patched with an AI boolean that is not part of the durable 
  product

  Lane-aware mapping (/products vs root) was replaced by one Luna call returning
  product: true/false per selected row. The prompt is reasonable. Placement is not:
  it sits outside the paid-attempt ledger and the handoff fingerprint, can be
  retried, and is invisible in query review unless the user notices the prefix.

  For this buyer both prefixes can find merchants. The important split is not product
  vs store. It is shoppable niche query vs local/retailer/junk. Spending a model
  call on /products vs / while defaulting eight near-me Walmart variants is
  optimizing the last mile of the wrong list.

  What is working and should not be reopened

  Keep the durable research worker, leases, fencing, S3-before-terminal, owner-scoped
  results, $3 cap, US-only expansion, 300/200/100 bounds, selection CAS, one
  selection item → one query, and the full dashboard as an inspectable artifact.

  Users must still be able to select non-recommended rows, add manual keywords, and
  edit queries. The system must never silently delete a selection. Those are the
  right control-plane rules. The defect is what the system proposes, not that the
  user can override it.

  Product decisions a redesign has to lock

  Do not start by retuning 55, Jaccard 0.88, or apparel word lists. Those are
  symptoms. The contract needs new recommendation semantics. The choices I would
  lock:

  1. What “recommended” means
  Not “SEO opportunity ≥ 55.”
  Recommended = the default query plan: one representative per distinct shoppable
  concept, ranked by predicted Shopify-merchant yield in the seed niche.

  2. What to optimize
  Predict lead-finding utility, not rankability:

  • shoppable / store / product intent (keep)
  • local / maps intent (penalize or block by default)
  • retailer / marketplace / giant-brand navigational (penalize or block)
  • junk / typo / numeric / repeated-token quality (flag, do not recommend)
  • niche overlap with seeds (require)
  • concept diversity (hard constraint on the default set)
  • volume only as a weak prior, on a stable scale, not vs max-in-run
  • drop or invert “easy keyword” rewards; if CPC is kept, treat it as
    willingness-to-pay, not a 5% afterthought

  3. How the default list is built
  Rank concepts, not rows. Default-select one representative per concept. Optionally
  allow a second member only when it is a materially different lane (product vs
  store), not a paraphrase. Cap remains 100; a good default is probably much smaller
  and diverse. Everything else stays visible for manual selection.

  4. What clustering is for
  Cluster by product/business concept + intent, with hard boundaries between local,
  store, product, brand, and informational. Use overlap-adjusted volume if clusters
  are scored at all. Do not generate apparel labels. Do not treat cluster
  recommendation as decoration.

  5. Informational and junk
  Do not delete metric-bearing rows at the US screen unless they cannot be
  researched. Flag them. Let the user see best X and rescue it. Never default-select
  junk.

  6. Downstream acceptance
  For research-backed runs, keep “must be a live Shopify store.” Use seed-niche fit
  as ranking/metadata or as a soft filter, not as a second incompatible grammar. Do
  not accept Walmart-query drift just because a .myshopify.com host appeared.

  7. Dashboard honesty
  If market views stay, label cluster/summary as cumulative or persist real
  per-market cluster metrics. Stop calling a manually selected non-recommended row
  “Recommended.” Opportunity score, if it remains, needs a stable meaning or it
  should be renamed so users do not treat 55 as quality.

  8. Versioning
  This is a new recommendation contract, not a silent v1 tweak. Existing completed
  researches keep their snapshots.

  Suggested correction order (product, not windows)

  1. Write the recommendation semantics from real completed researches (clothing,
     plus at least one non-apparel niche such as pickleball / ceramics / skincare).
     Define expected default sets by concept, not by score.
  2. Replace apparel classification with category-agnostic concept + intent +
     quality + retailer detection.
  3. Separate descriptive metrics from default-set construction (diversity-first).
  4. Fix conflict semantics and the canonical-order bug; distinguish duplicate vs
     equivalent vs related.
  5. Align probe vs storefront with the niche-lead rule above.
  6. Then durability of the Luna call, market UI labeling, and schema mismatches.

  Query transformation, Luna idempotency, and AWS fencing are real, but they are not
  why the clothing run recommended Walmart and “near me.” Fixing those first would
  polish a query planner that is still pointed at the wrong merchants.

  The honest summary: payloads and pipeline work; the recommendation layer is still a
  clothing SEO demo. Until default selection is a diverse set of shoppable,
  in-niche, independent-store queries, the rest of the lead scraper will keep doing
  expensive work on the wrong list.