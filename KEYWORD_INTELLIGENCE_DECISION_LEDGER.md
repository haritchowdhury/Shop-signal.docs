# Keyword Intelligence Decision Ledger (`A3`)

**Revision:** `KI-DL-27`
**Status:** locked decisions; not an assignment

This is the sole authority for implementation-affecting choices and
deterministic derivations. The other artifacts are `A1`
`KEYWORD_INTELLIGENCE_PRODUCT_CONTRACT.md`, `A2`
`KEYWORD_INTELLIGENCE_DISCOVERY_DOSSIER.md`, `A4`
`KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md`, `A5`
`ACTIVE_EXECUTION_STATE.md`, `A6`
`KEYWORD_INTELLIGENCE_EXECUTION_EVIDENCE.md`, `A7`
`KEYWORD_INTELLIGENCE_SPECIFICATION_CHANGELOG.md`, and `A8`
`KEYWORD_INTELLIGENCE_TRACEABILITY_INDEX.md`.

## 1. Locked decision records

### `DEC-KI-001` — Runtime and module boundary

- **Requirements:** `REQ-KI-002`, `REQ-KI-004`, `INV-KI-001`–`007`,
  `EXC-KI-001`.
- **Locked choice:** port pure/domain/API behavior to ESM Node.js under
  `email_scraper/src/keyword-intelligence/`; place message, artifact, provider,
  worker, handler, and recovery code under
  `email_scraper/src/aws-pipeline/keyword-intelligence/` as required by the
  workspace boundary. Use the existing backend process, Prisma/Neon, S3/SQS
  adapters, and one dedicated Node Lambda entry point. Use no Python or SQLite
  in any integrated runtime or build artifact.
- **Evidence:** `SRC-KI-001`, `SRC-KI-007`, `SRC-KI-008`, `SRC-KI-016`.
- **Rejected:** Python subprocess/service; iframe/static dashboard; whole-job
  Lambda; Fargate; Step Functions; second database.
- **Consequences:** modules are directly unit-testable; the Lambda handles only
  bounded message units; API and browser never call DataForSEO.
- **Tasks/scenarios:** `KI-W2-T1`, `KI-W4-T1`, `SCN-KI-001`, `SCN-KI-012`.

### `DEC-KI-002` — Research identity and generation

- **Requirements:** `REQ-KI-002`, `INV-KI-005`–`008`, `INV-KI-013`.
- **Locked choice:** research ID is `kr_` plus 24 base64url characters from
  `randomBytes(18)`; generation starts at 1 and is immutable in this scope.
  Task identity is `(researchId,stage,generation,itemKey)`. Selection item
  identity is `ksi_` plus the 12 lowercase hex BLAKE2s digest of
  `sourceKind + "\n" + originalNormalizedKeyword`.
- **Evidence:** `SRC-KI-012`, `SRC-KI-016`; Python stable IDs `SRC-KI-008`.
- **Rejected:** seed text as identity; owner ID as work identity; random task
  IDs; mutable generation; cache key as access identity.
- **Consequences:** duplicate messages commute; manual edits retain lineage;
  research access still requires owner equality.
- **Derived values:** BLAKE2s digest is six bytes using `@noble/hashes` 2.2.0;
  hex is exactly 12 lowercase characters.
- **Tasks/scenarios:** `KI-W1-T2`, `KI-W2-T2`, `SCN-KI-002`, `SCN-KI-008`.

### `DEC-KI-003` — Seed normalization and source attribution

- **Requirements:** `REQ-KI-001`, `REQ-KI-016`.
- **Locked choice:** parse an array length 1–5; for each string apply NFKC,
  trim, and replace every Unicode whitespace run with one ASCII space; require
  1–100 Unicode code points; reject control characters and duplicates under
  locale-independent lowercase. Preserve normalized input order. Each keyword's
  `sourceSeeds` is the normalized seed set sorted by original seed index; its
  primary `seed` is the first member.
- **Evidence:** `SRC-KI-005`, `SRC-KI-006`, `SRC-KI-008`.
- **Rejected:** comma parsing; silent duplicate removal; arbitrary 5+ seeds;
  alphabetic primary seed.
- **Consequences:** category index for a run query is the zero-based index of
  the primary seed.
- **Tasks/scenarios:** `KI-W2-T2`, `KI-W4-T2`, `SCN-KI-003`.

### `DEC-KI-004` — Markets and immutable config snapshot

- **Requirements:** `REQ-KI-003`, `REQ-KI-004`, `INV-KI-014`.
- **Locked choice:** snapshot `keyword-research-config-v1` with all values in
  `KeywordSearchVolume/config.yaml`, except obsolete paths/offline mode. Market
  order and tuple is: US/2840/en/English, GB/2826/en/English,
  CA/2124/en/English, AU/2036/en/English, NZ/2554/en/English,
  DE/2276/de/German, FR/2250/fr/French, IN/2356/en/English,
  AE/2784/en/English. The same snapshot additionally fixes
  `expansionAnchor={code:"US",locationCode:2840,languageCode:"en",
  languageName:"English"}`, `expansionPerSeedLimit=60`,
  `screenCandidateLimit=300`, `shortlistLimit=200`,
  `overviewBatchLimit=700`, `maxCostPerResearchUsd="3.00000000"`, and the
  reservation formulas in `DEC-KI-009`. Snapshot is written at creation and all
  replays use it.
- **Evidence:** `SRC-KI-006`.
- **Rejected:** user-selected subset; environment reread during a run; legacy
  single-market fallback.
- **Consequences:** market views are analytical filters; there is one cumulative
  selection, not nine independent lists.
- **Tasks/scenarios:** `KI-W2-T1`, `KI-W3-T1`, `SCN-KI-005`.

### `DEC-KI-005` — US-only expansion manifest

- **Requirements:** `REQ-KI-004`, `INV-KI-004`–`007`.
- **Locked choice:** expansion uses only the immutable US anchor from
  `DEC-KI-004`. It has exactly `seeds × 2` tasks (2–10). Item key is
  `<zeroBasedSeedIndex>:suggestions|related`. Suggestions and related are
  separate provider calls/artifacts, each requesting at most 30 rows. The
  aggregator combines each seed as `[seed,...suggestions,...related]`, preserves
  endpoint then provider order, applies case-insensitive first-occurrence
  uniqueness, truncates to 60 including the seed, then forms one global
  first-occurrence list in seed order. Empty/known-failed endpoint output
  contributes no candidates; the seed always remains. No non-US expansion call
  exists.
- **Evidence:** `SRC-KI-006`, `SRC-KI-008`, `PAY-KI-003`, `PAY-KI-004`.
- **Rejected:** one invocation per seed doing two calls; depth-two recursive
  client traversal; alphabetical ordering; abort on one endpoint failure.
- **Consequences:** expected expansion count is known at creation (2–10);
  maximum global candidate list is 300.
- **Tasks/scenarios:** `KI-W3-T1`, `KI-W3-T2`, `SCN-KI-004`, `SCN-KI-006`.

### `DEC-KI-006` — Anchor screen, deterministic shortlist, and remaining markets

- **Requirements:** `REQ-KI-004`, `INV-KI-004`–`007`.
- **Locked choice:** expansion aggregation writes one immutable candidate
  manifest and atomically creates one `anchor_screen` task with item key
  `US:0`. Its one overview request contains the complete 1–300 candidate list;
  no candidate is capped before this call. The anchor aggregator strictly
  normalizes US metrics, excludes provider-omitted/unusable rows and rows
  rejected by the preserved informational rule, then runs the existing variant
  deduplication, clustering, flagging, recommendation, and scoring algorithms
  with US as the sole metric. It sorts active canonical rows by recommended
  descending, opportunity score descending, search volume descending,
  normalized keyword ascending, then stable item ID ascending, and retains the
  first `min(200,activeCount)`. It writes an immutable shortlist manifest.

  In the same fenced transaction it creates one `market_overview` task for each
  non-anchor market in this exact order: GB, CA, AU, NZ, DE, FR, IN, AE. Item
  key is `<marketCode>:0`; each request contains the complete ordered shortlist
  and therefore at most 200 keywords. US metrics are reused from the validated
  anchor artifact and are never requested again. After all eight tasks are
  terminal, final aggregation combines US plus the eight results and reruns the
  preserved nine-market normalization/dedup/clustering/scoring pipeline; the
  anchor ranking does not remain the final score/order.
- **Evidence:** `SRC-KI-006`, `SRC-KI-008`.
- **Rejected:** one call per keyword; a provider batch across markets; dynamic
  expected set after task creation.
- **Consequences:** maximum overview work is one anchor plus eight remaining
  markets, so maximum first-pass provider work is 10 expansion + 1 anchor + 8
  remaining-market calls. A zero usable anchor set fails before creating market
  tasks; shortlist size 1–200 makes each remaining task nonempty.
- **Tasks/scenarios:** `KI-W3-T2`, `SCN-KI-005`, `SCN-KI-013`.

### `DEC-KI-007` — Provider retry and ambiguity

- **Requirements:** `INV-KI-006`–`009`.
- **Locked choice:** maximum five HTTP attempts per logical task (initial plus
  four). One Lambda invocation performs at most one attempt. Known HTTP
  429/500/502/503/504 or root API code 40601/40602/50001/50002/40107 schedules
  a continuation after `min(60,2×2^(attempt-1)) + deterministicJitter`, where
  `deterministicJitter = baseDelay × ((uint32(first8hex(SHA256(taskId+":"+attempt)))
  mod 2501)/10000)`; SQS delay is `ceil(delay)` seconds. HTTP 401/root 40100 is
  terminal auth failure. Other known failures are terminal. A transport error,
  timeout, malformed body after send, or lease loss after the durable pre-call
  marker **when no strict known response is available** is `ambiguous` and is
  never automatically repeated. When a strict response is available, its
  outcome and cost remain known: `DEC-KI-026` settles it (and a success cache)
  before reporting the lost task fence. Cache hit performs zero provider
  attempts.
- **Evidence:** `SRC-KI-006`, `SRC-KI-022`, workspace paid-call invariant.
- **Rejected:** in-memory sleeps across retries; blind transport retry; random
  nondeterministic jitter; provider-shape probing.
- **Consequences:** safety is stricter than old Python for unknowable transport
  outcomes while preserving attempt/backoff ceilings for known responses.
- **Tasks/scenarios:** `KI-W3-T1`, `KI-W3-T2`, `SCN-KI-006`, `SCN-KI-007`.

### `DEC-KI-008` — Rate control

- **Requirements:** `INV-KI-012`.
- **Locked choice:** research worker reserved concurrency is one; before any
  provider call it atomically claims the singleton Postgres throttle row
  `provider="dataforseo_labs_keyword"`. Claims are at least 2,000 ms apart
  using database time. A failed early claim requeues the same task for the
  calculated whole-second delay without incrementing provider attempt count.
- **Evidence:** `SRC-KI-006`, `SRC-KI-016`.
- **Rejected:** event-source maximum concurrency one; per-process timestamp;
  sleeping while holding a lease; assuming account-wide limits.
- **Consequences:** research is bounded to 30 attempts/minute even across cold
  starts; interaction with other DataForSEO products is validated at deployment
  gate, not guessed.
- **Tasks/scenarios:** `KI-W1-T2`, `KI-W3-T1`, `SCN-KI-007`.

### `DEC-KI-009` — Cache and paid-call ledger

- **Requirements:** `REQ-KI-017`, `REQ-KI-022`, `INV-KI-008`, `INV-KI-009`.
- **Locked choice:** canonical request JSON recursively sorts object keys,
  preserves array order, uses UTF-8 JSON without whitespace, and permits only
  finite JSON scalars. `requestFingerprint=SHA256(endpointKey+"\n"+canonicalJson)`;
  compatibility `cacheKey=endpointKey+":"+first24hex(SHA256(canonicalJson))`.
  Cache unique key is full request fingerprint, logical adapter contract label
  is `dataforseo-labs-keyword-v1`, its existing persisted
  `KeywordResearchCache.contractVersion` value is integer `1`, and expiry is
  successful DB time + 604800 seconds.
  Each actual attempt has a unique `(taskId,attemptNumber)` ledger row and a
  first-terminal state. Immutable `maxCostPerResearchUsd` is
  `3.00000000`. Suggestions and related reserve `0.01560000` per attempt.
  Overview reserves `0.01200000 + 0.00012000*n`, where `n` is the strict
  requested keyword-array length (1–300 for anchor; 1–200 for other markets).
  In one transaction before network dispatch, require
  `sum(providerCostUsd for every known settled response)
  +sum(planned|in_flight|ambiguous.reservationCostUsd)
  +proposedReservation <= 3.00000000`; otherwise create no attempt row, make
  no HTTP call, and fail safely with `KEYWORD_PROVIDER_BUDGET_EXHAUSTED`.
  Every strict known response, whether success, retryable failure, or terminal
  failure, settles its reported provider cost and replaces that attempt's
  reservation; ambiguous outcome retains its reservation. Only a strict
  normalized success is cached. At maximum scale the
  first pass reserves `0.49200000`, five fully charged attempts per logical
  task reserve `2.46000000`, and budget headroom is `0.54000000`.
- **Evidence:** `SRC-KI-007`, `SRC-KI-012`, `SRC-KI-022`, `SRC-KI-028`–`032`.
- **Rejected:** raw-response cache; TTL refresh on read; cache existence as
  owner authorization; retry without a ledger row.
- **Consequences:** stale entries miss but are not destructively purged in this
  scope; cache/result fingerprints detect corruption and conflicts.
- **Tasks/scenarios:** `KI-W1-T2`, `KI-W3-T1`, `SCN-KI-006`, `SCN-KI-009`.

### `DEC-KI-010` — Algorithm port authority

- **Requirements:** `REQ-KI-004`, `EXC-KI-002`.
- **Locked choice:** each pure Python function in `SRC-KI-008` is ported directly;
  same constants, input order, tie-breaks, rounding sites, field names, and
  formulas. `KeywordPipeline.run` collection loops are intentionally replaced
  only by `DEC-KI-005`–`006`; its post-collection normalization, deduplication,
  clustering, scoring, summaries, and output assembly remain parity authority.
  Remove only raw file references, compatibility fallbacks, disk
  writes, and Python-specific object plumbing. Use `@noble/hashes` 2.2.0 for
  six-byte BLAKE2s stable IDs.
- **Evidence:** `SRC-KI-008`, `SRC-KI-017`.
- **Rejected:** rewrite with a new ML/LLM classifier; transitive clustering;
  new weights; built-in variable-length BLAKE2s approximation.
- **Consequences:** function-by-function golden parity is possible.
- **Tasks/scenarios:** `KI-W2-T1`, `SCN-KI-010`.

### `DEC-KI-011` — Parity oracle

- **Requirements:** `REQ-KI-004`.
- **Locked choice:** for the same sanitized normalized overview fixture and
  config snapshot, Node and Python must produce exact equality for strings,
  booleans, nulls, arrays, membership, IDs, ordering, integer scores, rounded
  public numbers, flags, and recommendations. Intermediate unrounded IEEE-754
  values compare at absolute error ≤`1e-12`; exported CSV compares exact UTF-8
  bytes with LF line endings after both oracles use the same required column
  order. No Python invocation remains in production scripts or artifacts.
- **Evidence:** `SRC-KI-008`, `SRC-KI-009`.
- **Rejected:** screenshot-only parity; approximate output-object equality;
  retaining Python as production fallback.
- **Tasks/scenarios:** `KI-W2-T1`, `KI-W6-T5`, `SCN-KI-010`, `SCN-KI-018`.

### `DEC-KI-012` — Final normalized result schema

- **Requirements:** `REQ-KI-005`, `REQ-KI-014`, `REQ-KI-018`.
- **Locked choice:** persist one strict `keyword-research-result-v1` JSON object:
  `{contractVersion,researchId,generation,configFingerprint,seeds,markets,
  summary,keywords,clusters}`. A market is strict `{code,name,locationCode,
  languageCode,languageName}`. A market metric is strict `{countryCode,
  locationCode,locationName,languageName,searchVolume:int,cpc:number|null,
  competition:number,competitionLevel:"LOW"|"MEDIUM"|"HIGH",
  keywordDifficulty:int|null,mainIntent:"transactional"|"commercial"|
  "informational"|"navigational",commercialIntent:number,
  monthlyHistory:{year:int,month:int(1..12),searchVolume:int}[15..102],
  trendSlope:number,flags:string[],opportunityScore:int,
  recommended:boolean}`. A keyword row is strict `{itemId,keyword,seed,
  sourceSeeds,searchVolume:int,cpc:number|null,competition:number,
  competitionLevel:"LOW"|"MEDIUM"|"HIGH",keywordDifficulty:int|null,
  mainIntent:"transactional"|"commercial"|"informational"|"navigational",
  commercialIntent:number,monthlyHistory,trendSlope:number,
  cluster:string|null,clusterId:string|null,lane,facets:{audience:string[],
  category:string[],channel:string[],fit:string[],modifier:string[]},
  variantGroupId:string|null,variantCanonical:string|null,flags:string[],
  opportunityScore:int|null,recommended:boolean,mergedInto:string|null,
  availableMarkets:string[],marketMetrics:<exact nine market-code keys to
  MarketMetric|null>}`. A cluster row is strict `{cluster,clusterId,keywords,
  combinedVolume:int,headlineVolume:int,adjustedClusterVolume:int,
  rawVariantVolume:int,variantGroups:{variantGroupId,canonical,variants,
  volume:int,sourceSeeds}[],sourceSeeds,laneCounts:<four-lane integer object>,
  facets,avgCpc:number,commercialIntent:number,trendScore:number,
  opportunityScore:int,recommendedForStoreDiscovery:boolean}`. Summary is strict
  `{schemaVersion:3,markets,seeds,rawItemsCollected:int,itemsWithMetrics:int,
  informationalDropped:int,uniquePhrases:int,dedupMerged:int,
  activeKeywords:int,variantGroups:int,clusters:int,recommendedKeywords:int,
  recommendedClusters:int}`. All counts/volumes are nonnegative, scores are
  0..100, bounded normalized numbers are 0..1 or -1..1 as their source formula
  specifies, and all arrays use port output order. Store fingerprint is SHA-256
  of canonical JSON. `raw_ref` and output paths are absent.
  `laneCounts` permits only the four lane keys, each present value a positive
  integer (absence means zero); cluster `facets` is the same exact five-array
  facets object as a keyword row.
- **Evidence:** `SRC-KI-008`, `SRC-KI-010`, `SRC-KI-011`.
- **Rejected:** table per metric; output files as authority; raw response field;
  browser recomputation.
- **Consequences:** one JSONB can reproduce every dashboard/export view and is
  immutable after completion.
- **Tasks/scenarios:** `KI-W1-T1`, `KI-W2-T1`, `KI-W3-T2`, `SCN-KI-010`.

### `DEC-KI-013` — Default selection and over-selection

- **Requirements:** `REQ-KI-006`–`REQ-KI-009`.
- **Locked choice:** candidate order is active rows sorted by recommended
  descending, opportunity score descending (null last), search volume descending
  (null last), normalized keyword ascending, item ID ascending. Default is all
  recommended candidates, truncated to first 100 only if necessary. A selection
  draft is one ordered array of 0–200 items and starts at revision 1 in the same
  final publication transaction. Market switching never changes it.
- **Evidence:** `SRC-KI-005`, `SRC-KI-010`.
- **Rejected:** top 10; per-market localStorage selection; arbitrary database
  order; silently removing over-limit entries.
- **Tasks/scenarios:** `KI-W2-T2`, `KI-W4-T1`, `KI-W5-T2`, `SCN-KI-011`.

### `DEC-KI-014` — Selection item and edit semantics

- **Requirements:** `REQ-KI-007`–`REQ-KI-009`, `REQ-KI-016`.
- **Locked choice:** a strict selection item is
  `{itemId,sourceKind:"calculated"|"manual",sourceKeywordId:string|null,
  originalKeyword:string,keyword:string,sourceSeeds:string[],lane,facets,
  metricsSnapshot:KeywordMetricSnapshot|null}`. `KeywordMetricSnapshot` contains
  exactly the keyword row fields in `DEC-KI-012` other than `itemId`, `keyword`,
  `seed`, `sourceSeeds`, `lane`, and `facets`; its nested schemas and bounds are
  unchanged. Calculated edits preserve original metrics and
  source identity; the edited text is reclassified for lane/facets. Manual rows
  have null source/metrics, a new stable item ID, and use the first research seed
  as source seed. Keyword text uses seed normalization rules and max 160 code
  points. PUT replaces the complete ordered draft only when `expectedRevision`
  equals current; success increments revision once.
- **Evidence:** `SRC-KI-005`, `SRC-KI-010`, existing revision pattern
  `SRC-KI-013`.
- **Rejected:** patch-by-index; metrics recomputation after edits; local-only
  manual rows; last-write-wins.
- **Tasks/scenarios:** `KI-W2-T2`, `KI-W4-T1`, `KI-W5-T2`, `SCN-KI-008`.

### `DEC-KI-015` — Duplicate review

- **Requirements:** `REQ-KI-009`, `EXC-KI-004`.
- **Locked choice:** compare every selected pair with Python-equivalent
  `compact_signature`, token aliases, singularization, stop-token stripping,
  and Jaccard threshold 0.88. Each connected conflict component is returned;
  finalization rejects any pairwise conflict, even if the component is
  transitive. Canonical suggestion ranks calculated source canonical first,
  then opportunity, volume, shortest keyword, lowercase keyword, item ID.
  A strict conflict is `{conflictId,itemIds,pairs,canonicalItemId}` where item IDs
  are sorted ascending, `conflictId="ksc_"+first16hex(SHA256(itemIds joined by
  "\n"))`, and each pair is sorted by `(leftItemId,rightItemId)` with strict
  `{leftItemId,rightItemId,reason:"compact"|"similarity",similarity:number}`;
  compact equality uses similarity `1`, otherwise the unrounded Jaccard value.
- **Evidence:** `SRC-KI-006`, `SRC-KI-008`.
- **Rejected:** automatic union-find deletion; only exact duplicates; first row
  always wins; comparison only within recommended items.
- **Consequences:** maximum 19,900 pair comparisons at draft cap 200.
- **Tasks/scenarios:** `KI-W2-T2`, `KI-W4-T1`, `KI-W5-T2`, `SCN-KI-011`.

### `DEC-KI-016` — Keyword-to-query mapping and validation

- **Requirements:** `REQ-KI-010`–`REQ-KI-013`, `INV-KI-015`.
- **Locked choice:** mapping is exactly `REQ-KI-011`. Research-backed query
  phrase is NFKC/trim/collapse, 1–160 code points, 1–12 alphanumeric-token words,
  no control, quote, newline, or operator punctuation. Full query is ≤200 code
  points and contains exactly one leading supported lowercase site prefix and
  no other `site:`, colon operator, quote, `OR`, or unary minus token. Editable
  review contains exactly the persisted selection item ID set, 1–100 rows,
  unique sequences, and may edit/reorder but not add/delete. Relevance requires
  at least one normalized non-stop token shared with the source keyword or any
  source seed. Legacy validator is unchanged and dispatch branches by
  `queryPlanSource`.
- **Evidence:** `SRC-KI-013`, `SRC-KI-014`, product mapping `SRC-KI-005`.
- **Rejected:** products-only validator; LLM query generation; arbitrary row
  additions; replacement after weak probe.
- **Tasks/scenarios:** `KI-W2-T2`, `KI-W4-T2/T3`, `KI-W6-T3/T5`,
  `SCN-KI-014`, `SCN-KI-018`.

### `DEC-KI-017` — Research-to-run atomic snapshot

- **Requirements:** `REQ-KI-015`, `REQ-KI-016`.
- **Locked choice:** authenticated `POST /api/keyword-research/:id/runs` invokes
  one Prisma transaction. Predicate: owner equality, research completed,
  expected revision equality, 1–100 items, zero conflicts. Writes: Run with
  `queryPlanSource=keyword_research`, research ID/revision, immutable snapshot;
  ordered RunQuery rows with `source=generated` and `keywordResearchItemId`;
  relation link. Any failure rolls back all writes. Identical retry with the
  same `(researchId,revision,clientRequestId)` returns the same run through a
  unique handoff row; differing payload under that key is conflict.
- **Evidence:** `SRC-KI-012`, `SRC-KI-013`.
- **Rejected:** create then copy in separate transactions; recompute snapshot;
  one research usable for only one run; browser-created query rows.
- **Tasks/scenarios:** `KI-W1-T1`, `KI-W1-T2`, `KI-W4-T2`, `SCN-KI-008`, `SCN-KI-015`.

### `DEC-KI-018` — Durable state machines

- **Requirements:** `REQ-KI-002`, `INV-KI-005`–`008`, `INV-KI-014`.
- **Locked choice:** research: `queued→running→completed|failed`; no transition
  leaves terminal. Stage: `collecting→ready→aggregating→completed|failed`;
  task: `pending→processing→succeeded|skipped|failed`, with expired processing
  reclaimed to processing under a new lease token. Final research completion
  stage names and order are
  `expansion→anchor_screen→market_overview`; final research completion requires
  all three stages completed and one live final aggregation owner. Provider
  ambiguity makes its task and then research failed with safe error. Endpoint
  known failure may be `skipped` for expansion; anchor failure or zero usable
  rows fails research; remaining-market known failure is `failed`, and final
  research fails when any required market has zero usable metrics. Provider-
  omitted individual shortlist items remain null for that market and do not
  alter the immutable shortlist.
- **Evidence:** `SRC-KI-008`, `SRC-KI-016`.
- **Rejected:** queue emptiness; S3 event fan-in; user cancellation; publish
  partial dashboard.
- **Tasks/scenarios:** `KI-W1-T2`, `KI-W3-T2`, `SCN-KI-001`, `SCN-KI-006`, `SCN-KI-012`.

### `DEC-KI-019` — Backend API contract

- **Requirements:** `REQ-KI-001`–`002`, `005`–`009`, `015`, `018`,
  `INV-KI-013`.
- **Locked choice:** add strict owner-scoped routes:
  - `POST /api/keyword-research` body `{seeds:string[1..5]}` → 202
    `{research:ResearchView}`;
  - `GET /api/keyword-research/:id` → 200 `{research:ResearchView}`;
  - `PUT /api/keyword-research/:id/selection` body
    `{expectedRevision:int>=1,items:SelectionItem[0..200]}` → 200
    `{research:ResearchView}`; stale revision 409
    `KEYWORD_SELECTION_REVISION_CONFLICT`;
  - `POST /api/keyword-research/:id/runs` body
    `{expectedSelectionRevision:int>=1,clientRequestId:string matching
    /^[A-Za-z0-9_-]{16,80}$/}` → 201
    `{run:<existing strict SerializedRun>,statusUrl:string}`;
  - `GET /api/keyword-research/:id/export.csv` accepts each parameter at most
    once except repeated `flag` (≤20): `market=all|US|GB|CA|AU|NZ|DE|FR|IN|AE`,
    `seed` normalized string≤100, `clusterId` stable ID, `intent` nonempty≤40,
    `lane` one of four lanes, `category|audience|channel` nonempty≤40,
    `minVolume` integer 0..2147483647, `minOpportunity` integer 0..100,
    `recommended=true|false`, `flag` nonempty≤40, and normalized `search`≤160.
    It applies the same pure filter predicate/order as the dashboard and returns
    UTF-8 LF CSV, attachment, no-store.
  `ResearchView` is exactly `{id,statusUrl,state,generation,contractVersion,
  seeds,markets,progress,result,selection,selectionRevision,selectionConflicts,
  safeError,createdAt,startedAt,completedAt,updatedAt}`. `progress` is
  `{stage:"queued"|"expansion"|"anchor_screen"|"market_overview"|
  "finalizing"|"completed"|"failed",expansion:StageCounts,
  anchorScreen:StageCounts,marketOverview:StageCounts}` and `StageCounts` is exactly
  `{expected,terminal,succeeded,skipped,failed}` with nonnegative integers.
  `result` is `null` except completed, then `DEC-KI-012`; `selection` is ordered
  `SelectionItem[]` (empty/revision0 before publication); conflicts are the
  strict component results from `DEC-KI-015`; `safeError` is null or
  `{code:string,message:string}`; dates are ISO strings or null except non-null
  created/updated; all objects reject unknown keys.
  Unknown body/query keys reject 400. Invalid state is 409; unauthenticated is
  existing 401; contract/internal safe errors never expose provider bodies.
- **Evidence:** `SRC-KI-015`, `PAY-KI-007`.
- **Rejected:** generic RPC; server-sent ephemeral-only status; frontend direct
  backend/provider calls; client-provided owner ID.
- **Tasks/scenarios:** `KI-W4-T1/T2/T3`, `KI-W5-T1`, `SCN-KI-003`, `008`, `009`.

### `DEC-KI-020` — Artifact contracts and keys

- **Requirements:** `INV-KI-002`, `INV-KI-005`–`009`.
- **Locked choice:** strict artifacts are
  `keyword-expansion-result-v1`, `keyword-expansion-manifest-v1`,
  `keyword-anchor-screen-result-v1`, `keyword-shortlist-manifest-v1`,
  `keyword-market-overview-result-v1`, `keyword-market-overview-manifest-v1`,
  and `keyword-research-result-v1`. Common header is exactly
  `{contractVersion,researchId,generation,stage,itemId,inputFingerprint,
  producedAt}`. Task artifacts add only normalized output and safe status/cost.
  Keys are `runs/keyword-research/<researchId>/generation-<g>/<stage>/`
  plus `<itemId>.json`; manifests use `manifest.json`; final uses
  `result.json`. `producedAt` is the durable stage/task timestamp chosen once in
  Neon before put. Content fingerprint is SHA-256 canonical JSON. Existing
  valid+matching artifact reconstructs terminalization; missing permits work;
  corrupt/conflicting is terminal contract/conflict failure.
- **Evidence:** `SRC-KI-016`, `PAY-KI-006`.
- **Rejected:** raw provider artifact; timestamp from each replay; mutable key;
  S3 listing as work discovery.
- **Tasks/scenarios:** `KI-W3-T1`, `KI-W3-T2`, `SCN-KI-006`, `SCN-KI-012`.

### `DEC-KI-021` — Prisma schema

- **Requirements:** `REQ-KI-005`, `015`–`017`, `INV-KI-001`, `006`, `008`.
- **Locked choice:** one forward migration adds enums
  `KeywordResearchState { queued, running, completed, failed }`,
  `KeywordResearchStageName
  { expansion, anchor_screen, market_overview }`,
  `KeywordResearchStageState
  { collecting, ready, aggregating, completed, failed }`,
  `KeywordResearchTaskState
  { pending, processing, succeeded, skipped, failed }`, and
  `RunQueryPlanSource { legacy, keyword_research }`; the state-machine values
  are exactly the `DEC-KI-018` transitions and omit `cancelled` because no
  cancellation path is in scope; models:
  - `KeywordResearch`: `id`, `ownerId`, `state`, `generation`, `contractVersion`,
    `configSnapshot Json`, `configFingerprint`, `seeds Json`, `markets Json`,
    `progress Json`, `result Json?`, `resultFingerprint?`, `selection Json?`,
    `selectionRevision default 0`, `safeErrorCode?`, `safeErrorMessage?`,
    `createdAt`, `startedAt?`, `completedAt?`, `updatedAt`; indexes owner/time,
    state/time; relations stages, runs, handoffs.
  - `KeywordResearchStage`: literal mirror of the accepted `PipelineStage`
    model (`SRC-KI-012`, `email_scraper/prisma/schema.prisma` lines 180–212)
    with exactly: `id String @id`; `researchId String` with `research
    KeywordResearch` relation; `stage KeywordResearchStageName`;
    `generation Int`; `manifestS3Key String?`, `manifestFingerprint String?`,
    `manifestProducedAt DateTime?` nullable until ready; `expectedCount Int`;
    `terminalCount Int @default(0)`, `succeededCount Int @default(0)`,
    `skippedCount Int @default(0)`, `failedCount Int @default(0)`,
    `cancelledCount Int @default(0)` retained verbatim from the accepted
    pattern though cancellation is out of scope; `state
    KeywordResearchStageState @default(collecting)`; `version Int
    @default(1)`; `aggregationOwner String?`, `aggregationLeaseToken String?
    @unique`, `aggregationLeaseAcquiredAt DateTime?`,
    `aggregationLeaseExpiresAt DateTime?`, `aggregationAttempt Int
    @default(0)`; `safeErrorCode String?`, `safeErrorMessage String?`;
    `createdAt DateTime @default(now())`, `updatedAt DateTime @updatedAt`,
    `completedAt DateTime?`; `tasks KeywordResearchTask[]`;
    `@@unique([researchId,stage,generation])`, `@@index([researchId,
    generation])`, `@@index([state,aggregationLeaseExpiresAt])`.
  - `KeywordResearchTask`: literal mirror of the accepted `PipelineTask`
    model (`email_scraper/prisma/schema.prisma` lines 214–241) plus the three
    keyword fields, with exactly: `id String @id`; `stageId String` with
    `stage KeywordResearchStage` relation; `itemKey String`;
    `inputFingerprint String`; `endpointKey String`; `requestFingerprint
    String`; `nextAttemptAt DateTime?`; `state KeywordResearchTaskState
    @default(pending)`; `attemptCount Int @default(0)`, `dispatchCount Int
    @default(0)`, `lastDispatchedAt DateTime?`; `leaseOwner String?`,
    `leaseToken String? @unique`, `leaseAcquiredAt DateTime?`,
    `leaseExpiresAt DateTime?`, `leaseAttempt Int @default(0)`;
    `artifactS3Key String?`, `artifactFingerprint String?`; `terminalAt
    DateTime?`; `safeErrorCode String?`, `safeErrorMessage String?`;
    `createdAt DateTime @default(now())`, `updatedAt DateTime @updatedAt`;
    `@@unique([stageId,itemKey])`, `@@index([stageId,state])`,
    `@@index([state,leaseExpiresAt])`, `@@index([stageId,lastDispatchedAt])`,
    and `@@index([state,nextAttemptAt])` for the `DEC-KI-022` recovery
    predicate.
  - `KeywordResearchCache`: `requestFingerprint @id`, `cacheKey`, `endpointKey`,
    `contractVersion`, `normalizedResponse Json`, `resultFingerprint`,
    `createdAt`, `expiresAt`; indexes cacheKey and expiry.
  - `KeywordResearchProviderAttempt`: `id`, `taskId`, `attemptNumber`, state
    using existing `DataForSeoRequestState`, `requestFingerprint`, timestamps,
    `reservationCostUsd Decimal(18,8)?`, `providerCostUsd Decimal(18,8)?`,
    `safeErrorCode?`, `resultFingerprint?`; unique task/attempt.
  - `KeywordProviderThrottle`: `provider @id`, `nextAllowedAt`, `updatedAt`.
  - `KeywordResearchHandoff`: `id`, `researchId`, `selectionRevision`,
    `clientRequestId`, `selectionFingerprint`, `runId @unique`, `createdAt`;
    unique research/clientRequestId.
  Extend `Run` with nullable research relation/ID, selection revision, snapshot
  JSON, and `queryPlanSource default legacy`; extend `RunQuery` with nullable
  `keywordResearchItemId`; index both lineage fields.
- **Evidence:** `SRC-KI-012`.
- **Rejected:** JSON-only state with no task rows; table per keyword/metric;
  reuse Run pipeline stages for pre-run research; destructive backfill.
- **Tasks/scenarios:** `KI-W1-T1`, `KI-W1-T2`, `SCN-KI-002`, `SCN-KI-015`.

### `DEC-KI-022` — Lease, fence, and recovery

- **Requirements:** `INV-KI-005`–`008`.
- **Locked choice:** reuse the accepted coordinator and lease-monitor constants:
  task lease duration 60 seconds with heartbeat every 20 seconds; aggregation
  lease duration 120 seconds with heartbeat every 40 seconds. Claim sets random
  24-byte base64url token and increments lease attempt. Every durable write is
  conditioned on row ID, generation, processing/aggregating state, and live
  token. Loss stops work and prevents terminalization. Recovery scans expired
  nonterminal leases and pending tasks whose `nextAttemptAt<=DB now`, then
  dispatches identity messages; it never invokes a provider. Same-owner retry
  is valid only with the same current token. One check owner transitions stage.
- **Evidence:** `SRC-KI-016`.
- **Rejected:** Lambda request ID as fence; heartbeat without conditional write;
  API process as sole recovery; two aggregation owners.
- **Tasks/scenarios:** `KI-W1-T2`, `KI-W3-T2`, `SCN-KI-012`.

### `DEC-KI-023` — Dashboard implementation

- **Requirements:** `REQ-KI-014`, `REQ-KI-018`.
- **Locked choice:** add App Router pages `/keywords` (new/start/history) and
  `/keywords/[researchId]` (status/dashboard), server-auth guarded using existing
  patterns. Port dashboard into focused client components under
  `frontend/components/keyword-intelligence/`, CSS under an owned module, and
  pure view-model modules. Use local exact dependencies `chart.js@3.9.1` and
  `chartjs-chart-treemap@2.0.0`; preserve custom canvas landscape without a
  replacement chart library. Backend is source of truth; localStorage stores
  only theme. Existing unrelated modified frontend symbols are read-only until
  their owner clears or explicitly transfers them.
- **Evidence:** `SRC-KI-010`, `SRC-KI-015`, `SRC-KI-018`.
- **Rejected:** redesign; iframe; one monolithic component; local output files;
  Recharts substitution for specified charts.
- **Tasks/scenarios:** `KI-W5-T1`, `KI-W5-T2`, `KI-W5-T3`, `SCN-KI-016`, `SCN-KI-017`.

### `DEC-KI-024` — Capacity and resource ceilings

- **Requirements:** `INV-KI-010`, `REQ-KI-008`.
- **Locked choice:** bounds are 1–5 seeds; 2–10 US expansion tasks; 1–300 global
  candidates; exactly one anchor-screen task; shortlist 1–200; exactly eight
  remaining-market tasks only after a nonempty anchor shortlist. A research can
  therefore create 3–19 logical provider tasks; a successful nonempty research
  creates 11–19. At most five attempts per task means at most 95 HTTP attempts
  before cache reduction; at most 23 S3 objects at
  maximum (19 task artifacts, three manifests, one final); result artifact/JSONB
  maximum 32 MiB; selection draft 200; pair comparisons 19,900; final/query
  rows 100; Google occurrences 1,000. Pure pairwise port algorithms are
  `O(k²)` at `k<=300` for anchor screening and `k<=200` for final calculation;
  tests must measure and cap their representative runtime
  and memory rather than increase Lambda resources blindly. The 32 MiB bound is
  implemented by constructing a keyword-worker-only `S3ArtifactStore` with
  `maxBytes:33554432` from the already-created runtime S3 client and bucket.
  The existing pipeline runtime store remains exactly 5,000,000 bytes and is
  neither reconfigured nor passed to keyword result reads/writes.
- **Evidence:** `SRC-KI-006`, `SRC-KI-011`, `SRC-KI-014`.
- **Rejected:** unbounded candidates; 1 query/provider call; assumed historical
  sample size as max; timeout increase as scale proof.
- **Tasks/scenarios:** `KI-W2-T1`, `KI-W3-T2`, `KI-W6-T3/T5`,
  `SCN-KI-013`, `SCN-KI-018`.

### `DEC-KI-025` — Deployment and predictable gates

- **Requirements:** `REQ-KI-022`–`024`, `AUTH-KI-002`–`005`, `AUTH-KI-007`,
  `EXC-KI-008`.
- **Locked choice:** local windows `KI-W1`–`KI-W6` require a new A5 assignment.
  `GATE-KI-001` and `GATE-KI-002` are parent-only activation/readiness gates:
  resolve unrelated
  frontend ownership, install decided exact dependencies, build representative
  backend/frontend closures, record sizes/startup, hash A1/A4, and replace A5
  only with requester authorization. `KI-W7` may edit SAM source only after
  local acceptance and explicit infrastructure-source authorization. `KI-W8`
  covers AWS creation/config discovery, secrets, event-source enablement, one
  paid sanitized canary, and production enablement; each mutation/call is
  separately disclosed and approved. Failed applied quota/capability preflight
  stops without substitution.
- **Evidence:** `SRC-KI-001`–`003`, `SRC-KI-017`, `SRC-KI-025`, `SRC-KI-026`.
- **Rejected:** treating plan approval as deployment/provider approval; editing
  A5 now; optimistic account limits; hidden dependency installation.
- **Tasks/scenarios:** `GATE-KI-001`, `GATE-KI-002`, `KI-W7-T1`, `KI-W8-T1`, `SCN-KI-019`.

The former `GATE-KI-003` is closed by `SRC-KI-030`: the exact budget and
formulas are `DEC-KI-004`/`009`, and no implementation agent chooses or
estimates them. This specification decision is not paid-call authorization.

### `DEC-KI-026` — Corrective worker/repository boundary

- **Requirements:** `REQ-KI-002`, `005`, `015`–`017`, `022`–`024`,
  `INV-KI-004`–`008`, `014`.
- **Finding:** accepted W1 source does not supply the transaction-complete
  worker boundary promised to W3. `initialize` requires an owner ID unavailable
  to identity-only worker messages; attempt creation is not lease-fenced and
  does not advance `attemptCount`; no throttle defer or retry transition exists;
  aggregator claim accepts `collecting`; recovery omits lost initialize
  dispatch and cannot reconstruct strict messages; expansion
  publication is split; final publication omits the default selection and live
  aggregator token; the logical cache label is not mapped to its integer schema
  value; and W1/W2 compute unequal selection IDs.
- **Locked interfaces:** `PrismaKeywordResearchRepository` is corrected in
  `KI-R1` and exposes the following exact worker callables in addition to the
  owner API/handoff callables already accepted:
  - `getWorkerResearch({researchId,generation})` returns
    `{outcome:"found",research:WorkerResearch}|{outcome:"not_found"}|
    {outcome:"conflict"}`. `WorkerResearch` is exactly `{id,state,generation,
    contractVersion,configSnapshot,configFingerprint,seeds,markets}`; it never
    contains `ownerId`.
  - `getTaskContext({taskId})` returns `{outcome:"found",research:
    WorkerResearch,stage:WorkerStage,task:WorkerTask,latestAttempt:
    WorkerAttempt|null}|{outcome:"not_found"}`. `WorkerStage` is exactly
    `{id,researchId,stage,generation,state,expectedCount,terminalCount,
    succeededCount,skippedCount,failedCount,manifestS3Key,
    manifestFingerprint,manifestProducedAt,createdAt}`. `WorkerTask` is exactly
    `{id,stageId,itemKey,inputFingerprint,endpointKey,requestFingerprint,
    nextAttemptAt,state,attemptCount,leaseToken,leaseExpiresAt,createdAt,
    artifactS3Key,artifactFingerprint,terminalAt,safeErrorCode}`.
    `WorkerAttempt` is exactly `{attemptNumber,state,requestFingerprint,
    reservationCostUsd,providerCostUsd,safeErrorCode,resultFingerprint,
    plannedAt,completedAt,ambiguousAfter}`; money values are fixed-eight-decimal
    strings or null and dates are `Date|null`.
  - `getStageContext({researchId,stage,generation})` returns
    `{outcome:"found",research:WorkerResearch,stage:WorkerStage,tasks:
    WorkerTask[]}|{outcome:"not_found"}|{outcome:"conflict"}`; tasks are ordered
    by `itemKey` ascending and generation/stage mismatch is `conflict`.
  - `initialize({researchId,generation,stage:"expansion",tasks},now)` no longer
    accepts `ownerId`. It loads the research by identity/generation, requires
    `queued|running`, validates exactly two tasks per persisted seed
    (`<index>:suggestions`, `<index>:related`) and the endpoint/fingerprint
    fields, and atomically performs queued→running plus immutable stage/task-set
    creation. Its exact union is
    `{outcome:"created"|"found",stage:WorkerStage,tasks:WorkerTask[]}|`
    `{outcome:"not_found"|"conflict"}`; existing equal rows return `found` and
    unequal rows return `conflict`.
  - `recordAttempt({taskId,token,requestFingerprint,reservationCostUsd,
    maxCostPerResearchUsd},now)` requires a `processing` task with the same
    lease token and request fingerprint. In the budget transaction it derives
    `attemptNumber=task.attemptCount+1`, requires `1..5`, applies `DEC-KI-009`,
    inserts the `planned` attempt, increments `task.attemptCount`, and clears a
    due `nextAttemptAt`. A matching existing nonterminal/ambiguous/latest
    attempt returns `{outcome:"found",attempt,mayCall:false}` and authorizes
    zero HTTP calls; the caller marks a matching `planned|in_flight` attempt
    ambiguous before acknowledgement. A new row returns
    `{outcome:"created",attempt,mayCall:true}`. An earlier failed
    attempt without a persisted retry schedule returns `conflict` with
    `KEYWORD_PROVIDER_RETRY_NOT_SCHEDULED`; other union members are
    `{outcome:"not_found"|"lost"|"conflict",code?:string}` and never authorize
    HTTP.
  - `settleAttempt({taskId,token,attemptNumber,state:"succeeded"|"failed",
    providerCostUsd,safeErrorCode,resultFingerprint,cacheEntry},now)` requires
    the exact
    latest attempt and a fixed-eight-decimal provider cost for every known
    response. `cacheEntry` is required only for success and is exactly
    `{cacheKey,endpointKey,contractVersion:1,
    normalizedResponse,resultFingerprint,ttlSeconds:604800}`; failure requires
    `cacheEntry:null`. The same transaction first-terminalizes the attempt,
    settles that known cost, and inserts or exact-matches the normalized cache
    row with `expiresAt=now+604800s`
    even if the task lease was lost, then evaluates the task token. Identical
    replay returns `{outcome:"found",attempt,fenceActive:boolean}`, unequal
    replay `conflict`; a newly settled active fence returns
    `{outcome:"terminal",attempt,fenceActive:true}`, and a stale fence returns
    `{outcome:"lost",attempt,fenceActive:false}`. A lost successful response
    has populated only the strict global normalized cache; it cannot write a
    task artifact or terminal task result. Recovery reclaims the task and
    completes from that cache with zero HTTP calls. A lost known failure is
    recovered from the durable failed attempt and scheduled without a new
    attempt row.
  - `markAttemptAmbiguous({taskId,attemptNumber,requestFingerprint,
    safeErrorCode:"KEYWORD_PROVIDER_AMBIGUOUS"},now)` conditionally changes the
    matching `planned|in_flight` attempt to `ambiguous`, leaves provider cost
    null and its reservation held, and does not require a stale task token. In
    that same transaction it first-terminalizes any still-nonterminal task as
    failed, increments its stage terminal/failed counters exactly once, marks
    that stage and research failed with the same safe code, and clears their
    live leases. This is the sole post-send lease-loss/transport-uncertainty
    write; identical replay is `{outcome:"found"}`, a new transition is
    `{outcome:"terminal"}`, mismatch is `conflict`, and it never authorizes
    another call.
  - `deferTask({taskId,token,nextAttemptAt,
    safeErrorCode:"KEYWORD_PROVIDER_THROTTLED"},now)` requires the current
    processing token, `nextAttemptAt>now`, and no provider attempt created in
    that claim. One transaction sets task pending, stores the due time/code,
    and clears all four lease fields without changing attempt or terminal
    counters. Equal replay is `{outcome:"delayed",retryAt}`, token loss is
    `lost`, missing is `not_found`, and mismatch is `conflict`. This is the only pre-call
    throttle-delay transition.
  - `scheduleRetry({taskId,token,attemptNumber},now)`
    requires the current processing token, the exact latest `failed` attempt,
    and `attemptNumber<5`. It derives the whole-second delay only from
    `DEC-KI-007` and stores `retryAt=max(attempt.completedAt + delay, now)`; the
    caller supplies neither a due time nor a code. One transaction sets task
    `pending`, stores `retryAt` as `nextAttemptAt`, and nulls
    `leaseOwner`, `leaseToken`, `leaseAcquiredAt`, and `leaseExpiresAt`; it does
    not change terminal counters or attempt count. Equal pending replay returns
    `{outcome:"delayed",retryAt}`; mismatch is `conflict` and token loss is
    `lost`; missing is `not_found`.
  - `claimAggregator({researchId,stage,generation,owner,token},now)` returns
    `not_ready` without mutation for `collecting`; claims only `ready` with
    `terminalCount===expectedCount` and
    `succeededCount+skippedCount+failedCount===expectedCount`, or reclaims an
    expired `aggregating` lease. A live unequal token returns `lost`; completed
    equal stage returns `found`; failed returns `conflict`. The exact union is
    `{outcome:"claimed"|"found",stage:WorkerStage}|`
    `{outcome:"not_ready",stage:WorkerStage}|`
    `{outcome:"not_found"|"lost"|"conflict"}`.
  - `publishCandidateManifest({researchId,generation,token,manifestS3Key,
    manifestFingerprint,nextStageTasks},now)` requires exactly the one `US:0`
    overview task and, in one transaction, records the expansion manifest,
    completes expansion, and creates the anchor stage/task. Its exact success
    union is `{outcome:"terminal"|"found",stage:WorkerStage,nextStage:
    WorkerStage,tasks:WorkerTask[]}`; other outcomes are
    `not_found|lost|conflict`. `publishShortlist({researchId,generation,token,
    manifestS3Key,manifestFingerprint,marketTasks},now)` analogously requires
    exactly `GB:0,CA:0,AU:0,NZ:0,DE:0,FR:0,IN:0,AE:0` once each and returns the
    same union; both exact replays return the persisted next-stage rows.
  - `publishResearchResult({researchId,generation,token,manifestS3Key,
    manifestFingerprint,result,resultFingerprint,selectionItems},now)` requires
    0–100 default-selection items conforming to `DEC-KI-014`, the live
    `market_overview` aggregation token,
    exact terminal counters, completed expansion/anchor stages, and running
    matching-generation research. Before writing, it requires `selectionItems`
    to deep-equal W2 `createDefaultSelection(result)` including order and item
    IDs; caller-supplied alternative defaults conflict. One transaction records the market manifest,
    completes the market stage, writes result/fingerprint and
    `selection={items:selectionItems}`, sets `selectionRevision=1`, and completes
    research. A new publication returns `{outcome:"terminal"}`; exact completed
    replay returns `{outcome:"found"}`; missing is `not_found`, token loss is
    `lost`, and any result, manifest, or selection mismatch returns `conflict`.
  - `recover(now)` returns
    `{outcome:"found",initializations:RecoveryInitialize[],taskDispatches:
    RecoveryTask[],aggregateChecks:RecoveryCheck[]}`.
    `RecoveryInitialize` is exactly `{researchId,generation}` for every queued
    research without an expansion stage. `RecoveryTask` is exactly
    `{researchId,generation,stage,stageId,taskId,itemKey,inputFingerprint,
    endpointKey,requestFingerprint}`. `RecoveryCheck` is exactly
    `{researchId,generation,stage,stageId,stageInputFingerprint}` for every
    ready stage and expired aggregating stage; its fingerprint is derived from
    that stage's persisted ordered tasks. Rows in every array are ordered by
    their primary identity fields. No later database lookup is permitted to
    construct a recovery message.
- **Identities/formulas:** the repository selection helper uses exactly
  `blake2s(UTF8(sourceKind+"\n"+normalizedKeyword),{dkLen:6})`, matching W2 and
  `DEC-KI-002`. `stageInputFingerprint=SHA256(canonicalJson({researchId,
  generation,stage,tasks:[{itemKey,inputFingerprint,endpointKey,
  requestFingerprint}] ordered by itemKey ascending}))`.
- **Boundaries:** all methods above are DB-only `SAME TRANSACTION` operations.
  The later W3 S3-before-Neon and Neon-before-SQS seams remain recovered
  boundaries. No schema change, provider call, S3/SQS operation, or owner-facing
  API change occurs in `KI-R1`.
- **Tasks/scenarios:** `KI-R1-T1`, `SCN-KI-020`; W3 consumes the accepted output.

### `DEC-KI-027` — One keyword queue and replay-stable artifact time

- **Requirements:** `REQ-KI-002`, `005`, `023`, `024`, `INV-KI-002`, `005`–`007`.
- **Locked choice:** all four keyword message discriminators use one dedicated
  standard queue. The application configuration property is exactly
  `awsPipelineKeywordResearchQueueUrl`, sourced from environment key
  `AWS_PIPELINE_KEYWORD_RESEARCH_QUEUE_URL`; W3 service reads only
  `runtime.config.awsPipelineKeywordResearchQueueUrl`, and local tests inject
  that property. W7 owns adding that key to `src/config.js`, strict HTTPS
  validation in `src/aws-pipeline/runtime-config.js`, infrastructure
  environment wiring, and the existing runtime-adapter configuration test.
- **Produced-at mapping:** task artifact `producedAt` is exactly the durable
  `KeywordResearchTask.createdAt`; candidate/shortlist/market manifests use the
  corresponding `KeywordResearchStage.createdAt`; final result uses the
  `market_overview` stage `createdAt`. Replays reuse these values byte-for-byte;
  wall-clock time at S3 write is forbidden.
- **Recovery:** W3 maps every `RecoveryTask` to the expansion or overview
  discriminator from its persisted stage/endpoint and every `RecoveryCheck` to
  `keyword.aggregate.check.v1`; every send uses the one URL above. Missing or
  non-HTTPS runtime URL is `KEYWORD_RUNTIME_CONFIG_INVALID` before dispatch.
- **Tasks/scenarios:** `KI-R1-T1` proves reconstruction inputs;
  `KI-W3-T2` consumes them; `KI-W7-T1` wires deployment configuration;
  `SCN-KI-012`, `020` prove replay stability.

### `DEC-KI-028` — Conditional lease renewal and live terminal fences

- **Requirements:** `REQ-KI-002`, `INV-KI-005`–`007`.
- **Finding:** independent review of the unaccepted W3 handoff found that the
  accepted keyword repository has no aggregation-renewal callable, task
  heartbeat can revive an expired lease, aggregator reclaim excludes the exact
  expiry instant, and task/aggregation terminal writes check token/state but
  not lease liveness. W3 therefore cannot implement the locked 20/40-second
  monitors or prove `SCN-KI-012` without changing an accepted predecessor file.
- **Locked task renewal:** `heartbeat({taskId,token},now)` keeps its existing
  input and success shape, but its one conditional `updateMany` must require
  exact task ID, `state:"processing"`, exact token, and
  `leaseExpiresAt:{gt:now}`. Count one sets
  `leaseExpiresAt=now+60000ms`, sets `updatedAt=now`, and returns
  `{outcome:"claimed",leaseExpiresAt}`. Count zero returns
  `{outcome:"lost"}` and performs no read or write. An expired, missing,
  terminal, or wrong-token row can never be revived.
- **Locked aggregation renewal:** add
  `heartbeatAggregator({researchId,stage,generation,token},now)`. Validate the
  same research/stage/token grammar as `claimAggregator` and use
  `requireGeneration(input?.generation ?? 1)` exactly; derive the
  stage ID with `keywordStageId(researchId,stage,generation)`. Its one
  conditional `updateMany` requires that ID plus exact research ID, stage,
  generation, `state:"aggregating"`, exact token, and
  `aggregationLeaseExpiresAt:{gt:now}`. Count one sets
  `aggregationLeaseExpiresAt=now+120000ms`, sets `updatedAt=now`, and returns
  `{outcome:"claimed",leaseExpiresAt}`. Count zero returns
  `{outcome:"lost"}` without a second query or mutation. It never changes the
  owner, token, acquired-at time, attempt number, counters, manifest, task set,
  or research row.
- **Expiry boundary and reclaim:** a lease is live only while its durable
  expiry is strictly greater than the injected `now`. `claimAggregator` may
  reclaim an aggregating stage when `aggregationLeaseExpiresAt<=now`; at the
  exact expiry instant the old token loses and one claimant may acquire.
  Renewal always extends from injected `now`, never from the old expiry or wall
  clock.
- **Live terminal fences:** `terminalize`, `_completeStageAndCreateNext`,
  `publishResearchResult`, and `failStage` must reject an expired token as
  `{outcome:"lost"}` before mutation and repeat the strict
  `leaseExpiresAt:{gt:now}` or `aggregationLeaseExpiresAt:{gt:now}` predicate
  in the conditional terminal update. Exact completed replay behavior remains
  unchanged and does not require a live lease. `settleAttempt` and
  `markAttemptAmbiguous` retain their deliberate `DEC-KI-026` post-provider
  recovery semantics and are not changed.
- **Concurrency/atomicity:** all renewal and terminal predicates execute in
  Neon using the caller's injected `now`; a stale token changes zero rows. No
  process-local timer establishes ownership. The W3 monitor calls renewal at
  20/40 seconds and calls its local `assertActive` immediately before every S3
  put and terminal repository call; repository fencing remains authoritative
  if the process pauses after that assertion.
- **Public interface effect:** the only additive repository callable is
  `heartbeatAggregator`; `heartbeat` retains its existing union. No
  `WorkerStage` projection, schema, migration, payload, message, API, artifact,
  or owner-facing contract changes.
- **Tasks/scenarios:** `KI-R2-T1`, `SCN-KI-022`; reopened `KI-W3-T2` consumes
  both heartbeat callables and remains responsible for monitor lifecycle.

### `DEC-KI-029` — Risk-proportionate verification and frozen pre-handoff gate

- **Requirements:** `REQ-KI-002`, `INV-KI-005`–`007`, `AUTH-KI-002`,
  `AUTH-KI-006`.
- **Locked choice:** implementation iterations use the smallest deterministic
  unit/static check that exercises the edited symbol. Database integration is
  an acceptance gate, not an edit-loop gate: run the current window's focused
  integration scenario exactly once after the final local implementation edit
  and before handoff. A diagnostic database run before that point is permitted,
  but is not acceptance evidence. Reuse accepted predecessor database evidence
  when its production source, test, schema, and migration hashes are unchanged.
  Run `npm test` and `npm run check:secrets` once against the same frozen
  pre-handoff tree. Run Prisma generate/validate only when schema, migration, or
  generated-client inputs changed; run handler build/size/startup only when a
  build/runtime input changed. Parent review reruns only the corrected
  risk-proportionate scenario, not the complete integration suite by default.
- **Invalidation rule:** any edit after a passing gate invalidates only checks
  whose source, test, schema, fixture, configuration, or build input changed.
  Rerun the focused database scenario only when one of its inputs changed;
  rerun the full default suite only when application/test inputs changed.
- **Evidence:** workspace verification policy `SRC-KI-001`; project-agnostic
  standard Phases E/F and final-review parity rules; requester direction
  recorded by `EV-KI-R2-05`.
- **Rejected:** rerunning every historical database scenario at each window or
  each edit; treating a diagnostic run as final evidence; omitting integration
  proof for a durable concurrency boundary; running schema/build gates whose
  inputs are byte-identical.
- **Consequences:** reopened KI-R2 adds one focused durable-boundary scenario;
  it does not repeat the 33-case Neon suite, Prisma generation/validation, or
  Lambda build. The handoff states the frozen hashes used by every result.
- **Tasks/scenarios:** `KI-R2-RT2`, `SCN-KI-023`; future window V/H blocks apply
  the same invalidation rule unless a stricter window-specific gate is written.

### `DEC-KI-030` — Reopened W3 final worker, continuation, and build boundary

- **Requirements:** `REQ-KI-002`–`005`, `REQ-KI-021`–`024`,
  `INV-KI-002`, `INV-KI-004`–`009`, `INV-KI-012`, `AUTH-KI-002`,
  `AUTH-KI-006`.
- **Finding:** inspection of the unaccepted W3 implementation at backend
  revision `916b49d3929cef4a0100c2029c3951a54551b589` confirms all W3-owned
  defects in `EV-KI-W3-04` and two additional reachable contradictions. The
  eight finding classes are: (F1) the adapter treats a stale `settleAttempt`
  fence as success; (F2) undecodable HTTP 429/500 bodies become guessed
  zero-cost retries; (F3) succeeded-attempt recovery writes `costUsd:null`;
  (F4) the task monitor is never consulted; (F5) no aggregation monitor exists
  and aggregation failure hides its repository fence outcome; (F6) delayed
  tasks are dispatched immediately because `sendOne` has no delay option;
  (F7) `overviewRequestSchema` caps each keyword at 100 although the locked
  research keyword bound is 160; and (F8) the keyword build deletes sibling
  staging and can retain stale entries in its own ZIP. W3 remains unaccepted,
  so this decision completes that same window rather than allocating a
  corrective successor.
- **Known-response settlement:** after every strict known response,
  `executeProviderAttempt` still settles cost/cache exactly as `DEC-KI-026`
  requires. It may return the known `succeeded|failed|retryAt` outcome only when
  settlement is `{outcome:"terminal",fenceActive:true}` or the identical replay
  is `{outcome:"found",fenceActive:true}`. Settlement `lost`, `not_found`, or
  `found` with `fenceActive:false` returns `{outcome:"lost",attempt,
  providerCostUsd}` and performs no retry scheduling. `conflict`, a missing
  `fenceActive` member on `terminal|found`, or any other union member is
  `PIPELINE_INPUT_CONFLICT`. A JSON-body decode failure after send is ambiguous
  for every HTTP status except the separately classified HTTP 401; it calls
  `markAttemptAmbiguous` once, never settles zero as a guessed cost, and never
  schedules a retry. `markAttemptAmbiguous` must return `terminal|found`; every
  other result fails closed.
- **Exact private helpers:** adapter-private
  `settlementFence(settled,{attempt,providerCostUsd})` returns
  `{outcome:"active",attempt}` only for the two active settlement members,
  returns the locked lost union for the three stale/missing members, and throws
  `PipelineInvariantError("PIPELINE_INPUT_CONFLICT")` otherwise. Service-private
  `createKeywordLeaseMonitor` accepts exactly the task/aggregation tagged inputs
  in A4 and constructs the corresponding monitor;
  `withLeaseBoundary(monitor,operation)` executes
  `assertActive()` → `await operation()` → `assertActive()`;
  `prepareTerminalLease(monitor)` executes
  `await renewNow()` → `await stop()` → `assertActive()`; and
  `stopReleasedLease(monitor)` awaits `stop()` and suppresses only an error with
  `code==="PIPELINE_LEASE_LOST"`. These four service helpers and the one adapter
  helper are the complete new private-helper set; no alternative wrapper or
  lease-context abstraction is authorized.
- **Succeeded-attempt recovery:** a reclaimed task whose latest attempt is
  `succeeded` must reconstruct and validate the exact input/request
  fingerprints, read the normalized cache by the task request fingerprint,
  require the cache result fingerprint to equal the attempt result fingerprint,
  and call `buildTaskArtifact` with
  `{outcome:"succeeded",normalized:cache.normalizedResponse,
  providerCostUsd:latestAttempt.providerCostUsd}`. Thus a crash after a first S3
  write replays byte-identical `costUsd`, body, metadata, and content fingerprint
  with zero HTTP calls. Missing/expired/mismatched cache is terminal ambiguity;
  it is never a second paid call.
- **Monitor construction and lifecycle:** `processKeywordMessage(message,
  runtime,dependencies={})` accepts only the optional internal test dependency
  `dependencies.createLeaseMonitor`, defaulting to
  `createPipelineLeaseMonitor`; every nested task/aggregate path receives that
  same factory. Task monitors use exactly `intervalMs:20000`; aggregation
  monitors use exactly `intervalMs:40000`; both pass `now:()=>nowOf(runtime)`.
  A renewal result other than `claimed` throws an error whose exact safe code is
  `PIPELINE_LEASE_LOST`. The monitor is consulted immediately before and after
  every provider call and S3 get/put. Before any ordinary terminal,
  publication, or failure repository call, the service executes
  `renewNow()` then `stop()` then `assertActive()` and immediately invokes the
  repository with the same token; the repository's live-expiry predicate is
  the authoritative final fence. A detected monitor loss permits no later S3,
  terminal, publication, or check send.
- **Voluntary release:** `deferTask`, `scheduleRetry`, and
  `markAttemptAmbiguous` deliberately clear/terminalize the current lease. Once
  one returns the exact successful delayed/terminal/found outcome, the service
  stops the monitor before dispatch and may suppress only that monitor's exact
  `PIPELINE_LEASE_LOST` error; no artifact/publication follows. A returned
  `lost` similarly stops and acknowledges the stale delivery with no write.
  Every other monitor error is propagated.
- **Aggregation outcomes:** the expansion, anchor, market, and failed-task
  aggregation paths share the 40-second monitor and the same S3 wrappers.
  `failStage` returns the repository outcome; callers report `stage_failed` only
  for `terminal|found` and propagate `lost|conflict|not_found`. A publication
  result other than `terminal|found` sends no next task/check. All monitor stops
  occur in `finally`, and a successful terminal preparation stops it before the
  fence-clearing repository transaction.
- **Delayed continuation:** add only the backwards-compatible optional fourth
  parameter to `SqsDispatcher.sendOne`:
  `sendOne(queueUrl,message,schema,{delaySeconds}={})`. When supplied it must be
  a strict object containing only integer `delaySeconds` in `0..900`, and the
  command includes that exact `DelaySeconds`; omitted options preserve every
  existing command byte-for-byte. W3 computes
  `delaySeconds=max(0,ceil((retryAt-nowOf(runtime))/1000))`, fails closed above
  900, stops the voluntarily released task monitor, then sends the same strict
  task message. A failed send is recovered from durable `nextAttemptAt`; early
  duplicate delivery is acknowledged as `delayed` and recovery redispatches
  only when due.
- **Request bound:** suggestion/related seed requests remain 1–100 code points.
  Each member of an overview `keywords` array is 1–160 code points, array length
  remains 1–700, anchor count remains 1–300, and remaining-market count remains
  1–200. A 160-code-point candidate reaches the mocked HTTP seam; 161 is
  `KEYWORD_PROVIDER_REQUEST_INVALID` with zero HTTP/attempt calls.
- **Build isolation:** `buildKeywordWorkerPackage` removes only
  `.lambda-build/keyword-worker` and `dist/lambda/keyword-worker.zip`, recreates
  those exact paths, and never removes or rewrites a sibling staging directory,
  sibling archive, or `measurements.json`. Removing the own ZIP before `zip -X`
  prevents stale archive members. The final gate first builds/measures the seven
  existing handlers, snapshots every sibling hash, builds keyword worker twice,
  and proves sibling byte equality plus identical two-run keyword ZIP hash,
  inventory, size, cold import, and exported handler.
- **Verification economy and successor:** implementation uses only focused
  static/unit checks until edits stop. The frozen final tree receives one
  focused isolated-database command, one focused non-DB command, one existing
  handler baseline build/measure followed by two keyword builds, one `npm test`,
  and one secret scan. Unchanged R1/R2 repository/schema evidence is reused by
  hash per `DEC-KI-029`; Prisma generation/validation and the full database suite
  are prohibited. Any final edit invalidates only its affected frozen gates.
  Successful W3 handoff stops at `AWAITING_REVIEW`; the parent reruns only the
  decisive W3 scenarios and, if they pass, assigns `KI-W4` directly. No W3
  correction window is an allowed successful branch.
- **Evidence:** current source inspection and hashes recorded by
  `EV-KI-W3-05`; predecessor acceptance `EV-KI-R2-04/06/07`; original rejection
  `EV-KI-W3-04`; payload and architecture evidence `SRC-KI-016`,
  `SRC-KI-019`–`022`, `SRC-KI-030`–`032`.
- **Rejected:** accepting stale settlement; guessing zero cost after undecodable
  bodies; cache-hit recovery bytes; process-local ownership; continuing after a
  monitor loss; immediate retry messages; polling/sleeping inside Lambda;
  changing repository/schema; deleting shared build roots; relying on the
  supplemental W3 plan; another correction window after this assignment.
- **Tasks/scenarios:** `KI-W3-RT1`–`KI-W3-RT4`, `SCN-KI-024`–`027`; original
  `KI-W3-T1/T2` and `SCN-KI-001/004`–`007/012/013` remain cumulative final-state
  obligations.

### `DEC-KI-031` — Enforcement-complete W3 correction and acceptance boundary

- **Requirements:** `REQ-KI-002`–`005`, `REQ-KI-021`–`024`, `INV-KI-002`,
  `INV-KI-004`–`009`, `INV-KI-012`, `AUTH-KI-002`, `AUTH-KI-006`.
- **Finding and authority:** independent inspection of the W3 handoff at backend
  revision `37a0e0203d265f539b566f1536642cd2f4eb2d99` rejects
  `EV-KI-W3-06` as completion evidence. The current ten-file implementation
  closes the originally enumerated F1–F8 examples, but its acceptance suite does
  not instantiate the required branch sets. Four reachable source defects
  remain: (R3-F1) active `settlementFence` drops `providerCostUsd`, so known
  failed results expose `undefined`; (R3-F2) ordinary task paths send an
  aggregation check after `terminalize` returns `lost|conflict|not_found`;
  (R3-F3) `recoverClaimedTask` performs S3, terminal, voluntary-release, and
  dispatch operations outside the task monitor/final fence; and (R3-F4) every
  recovered failed provider attempt is treated as retryable, so a crash after a
  known auth/contract/task failure can cause another paid call. Two exact
  interface defects also remain: (R3-F5) `sendOne(..., null)` is accepted even
  though supplied options must be strict, and (R3-F6) the W3 evidence claimed a
  complete private-helper set that omitted the present `markAmbiguousOnce`,
  `LEASE_LOST_CODE`, and `leaseLostError`. The helper implementations are not
  themselves unsafe; this decision names and accepts them so source and contract
  cannot disagree.
- **Unique corrective window:** requester direction allocates `KI-R3` rather
  than reopening W3 again. W3 remains unaccepted; accepted history remains
  through `KI-R2`. `KI-R3` owns only the literal symbols and additive tests in
  A4. Passing KI-R3 accepts the cumulative W3 capability and makes `KI-W4` the
  next candidate; it does not authorize KI-W4. This decision supersedes only
  `DEC-KI-030`'s incomplete private-helper-set sentence and its prospective
  direct-W3-successor/no-correction branch; all other `DEC-KI-030` behavior and
  accepted predecessor decisions remain cumulative.
- **Settlement result:**
  `settlementFence(settled,{attempt,providerCostUsd})` returns exactly
  `{outcome:"active",attempt,providerCostUsd}` for
  `terminal|found` with `fenceActive:true`; returns exactly
  `{outcome:"lost",attempt,providerCostUsd}` for `lost`, `not_found`, or
  `found/fenceActive:false`; and throws
  `PipelineInvariantError("PIPELINE_INPUT_CONFLICT")` for `conflict`, missing
  `fenceActive` on `terminal|found`, or any other member. Every known
  succeeded/failed/retry result carries the fixed-eight-decimal value supplied
  to settlement. No guessed or recomputed cost is permitted.
- **Provider-call lease boundary:** retain the five-argument public adapter
  interface. `runProviderAttempt({task,research,config,runtime,request,monitor})`
  passes an inline monitored HTTP function to `executeProviderAttempt`. That
  function asserts the task monitor immediately before fetch, in a `finally`
  immediately after fetch settles, immediately before `response.json()`, and in
  a `finally` immediately after JSON decode settles. It returns only the
  adapter-consumed `{status,json}` view. Loss before send produces zero HTTP;
  loss after send or during decode follows the existing one-call ambiguity path
  and may call `markAttemptAmbiguous`, but permits no S3, ordinary terminal, or
  check dispatch. The repository token/expiry fence remains authoritative if a
  process pauses after the last assertion.
- **Ordinary terminal gate:** after `prepareTerminalLease`, call
  `terminalize` once. Only `terminal|found` may call `sendCheckForStage`.
  For a successful artifact, `terminal` returns public outcome `succeeded` and
  `found` returns `found`; for a known failed attempt, `terminal` returns
  `terminal` and `found` returns `found`. `lost|conflict|not_found` is returned
  unchanged with zero check send. Any other member is
  `PIPELINE_INPUT_CONFLICT`. Check-send failure is acknowledged only because the
  durable terminal row makes `repository.recover().aggregateChecks` redispatch
  it; no second terminal write is made.
- **Recovery classification and order:**
  `recoverClaimedTask({taskId,token,current,message,kind,runtime,research,stage,
  config,monitor})` returns only `{outcome:"proceed"}` or
  `{outcome:"recovered",result}` where `result` is one of
  `terminal|found|lost|conflict|not_found|delayed|ambiguous`. It uses these
  literal schedules:
  1. no latest attempt, or a failed retryable attempt whose durable
     `nextAttemptAt` survived the due claim: `proceed`;
  2. `planned|in_flight`: call `markAttemptAmbiguous`, require
     `terminal|found` to send one check after `stopReleasedLease`; return
     `lost|conflict|not_found` unchanged after stop and without a check; reject
     any other member;
  3. `succeeded`: require latest/task request fingerprint equality, a fresh
     normalized cache, equality of attempt/cache/result fingerprints, and
     equality of `fingerprintJson(cache.normalizedResponse)` to that fingerprint;
     otherwise terminalize the task once as `failed/KEYWORD_PROVIDER_AMBIGUOUS`
     through `prepareTerminalLease`, with zero HTTP. On equality, reconstruct
     input, perform the S3 put through `withLeaseBoundary`, prepare the terminal
     lease, terminalize as succeeded, then apply the ordinary terminal gate;
  4. `failed/KEYWORD_PROVIDER_RETRYABLE` with no durable `nextAttemptAt`:
     attempt 1–4 calls `scheduleRetry`; `delayed` stops the released monitor
     before delayed dispatch, `lost|conflict|not_found` stops and returns with
     zero dispatch, and only the exact retry-exhausted conflict or attempt five
     proceeds through terminal preparation to
     `failed/KEYWORD_PROVIDER_RETRY_EXHAUSTED`;
  5. failed with safe code `KEYWORD_PROVIDER_AUTH_FAILED`,
     `KEYWORD_PROVIDER_CONTRACT_MISMATCH`, or `KEYWORD_PROVIDER_TASK_FAILED`:
     make zero HTTP/retry calls and terminalize once using that same code and
     the ordinary expansion `skipped` versus overview `failed` mapping;
  6. `ambiguous`, a failed attempt with null/unknown safe code, unequal durable
     identity, or any unlisted state is `PIPELINE_INPUT_CONFLICT`.
  Every S3 get/put in recovery is inside a before/after monitor boundary; every
  ordinary terminal uses renew-stop-assert; every voluntary release stops the
  monitor before dispatch. A `lost|conflict|not_found` repository result sends
  neither task nor check.
- **Dispatcher strictness:** the exact signature is
  `async sendOne(queueUrl,message,schema,options = {})`. `options` must be a
  non-null, non-array object whose prototype is exactly `Object.prototype`,
  with key set `{}` or `{delaySeconds}`. The value, when present, is an integer
  `0..900`. Null, arrays, primitives, non-plain objects, extra keys, fractions,
  and out-of-range values throw `PIPELINE_MESSAGE_INVALID`. Omitted/empty
  options emit the original command without a `DelaySeconds` member.
- **Exact private-member decision:** adapter-private additions are exactly
  `{settlementFence,markAmbiguousOnce}`. Service-private W3 additions are
  exactly `{LEASE_LOST_CODE,leaseLostError,createKeywordLeaseMonitor,
  withLeaseBoundary,prepareTerminalLease,stopReleasedLease}`. No further named
  helper or abstraction is added in KI-R3; monitored HTTP remains inline in
  `runProviderAttempt`.
- **Mechanical enforcement:** A4 defines one versioned case manifest with
  literal IDs, expected operation traces, result shapes, call counts, and
  mutation controls. The implementation materializes it at
  `test/fixtures/keyword-intelligence/ki-r3-enforcement-manifest-v1.json`.
  Each `SCN-KI-028`–`032` test loads its own group, executes every member as a
  named subtest, records every operation at the mocked boundary, and finishes
  with sorted set equality between expected IDs and executed IDs. Unknown,
  duplicate, skipped, or unexecuted case IDs fail. Negative controls mutate
  only injected collaborators and must make the unchanged production oracle
  fail; editing production source for a control is forbidden.
- **Verification economy:** edits use static/unit checks only. After the final
  code/test edit, run one non-database command containing only
  `SCN-KI-028/029/031/032`, one isolated-database command containing only
  `SCN-KI-030`, two keyword builds plus the unchanged `SCN-KI-027` package test,
  one `npm test`, and one secret scan. Reuse accepted R1/R2 integration and W3
  sibling-build baselines by exact hash. Do not run the full opted-in database
  suite, Prisma commands, seven-handler rebuild/measure, provider/AWS calls, or
  production writes. A post-gate edit reruns only the gate whose named input
  changed.
- **Evidence:** `EV-KI-W3-06` historical handoff; rejection
  `EV-KI-W3-07`; authoring certificate `EV-KI-A-036`; source hashes and observed
  counterexamples in those entries.
- **Rejected:** accepting broad scenario prose as proof; check dispatch after a
  nonterminal fence result; recovery outside the monitor; retrying a known
  terminal failure; silently accepting null options; hidden helper additions;
  repeated historical integration suites; W4 work in this window.
- **Tasks/scenarios:** `KI-R3-T1`–`T4`, `SCN-KI-028`–`032`, and unchanged
  package scenario `SCN-KI-027`.

### `DEC-KI-032` — Commit-stable enforcement and exhaustive R3 correction closure

- **Requirements:** `REQ-KI-002`, `REQ-KI-005`, `REQ-KI-021`–`024`,
  `INV-KI-002`, `INV-KI-004`–`009`.
- **Finding and authority:** independent parent review in `EV-KI-R3-02`
  rejects `EV-KI-R3-01` as cumulative W3 acceptance. The nine implementation
  hashes and the observed handoff-time commands remain historical facts, but
  five acceptance classes are unresolved: failed-attempt recovery does not
  reject unequal durable request identity; dispatcher own-key validation
  ignores symbol and non-enumerable extras; permanent conformance tests depend
  on uncommitted worktree state and allow an empty diff to pass one scope gate;
  case digests and database case registrations are not independently enforced;
  and four stated mutation controls do not inject the defect they claim to
  falsify. `KI-R4` is the unique corrective parent window. KI-W4 remains
  blocked until KI-R4 and cumulative W3 pass parent review.
- **Recursive execution boundary:** KI-R4 is assigned to one window agent under
  `PROJECT_AGNOSTIC_WINDOW_AGENT_SUBWINDOW_AUTHORING_STANDARD.md`. The window
  agent may write only the three named subordinate coordination artifacts. It
  must obtain parent approval of an initial sequential decomposition before
  assigning leaves, and each implementation/correction leaf may write exactly
  one of the eight implementation files named by KI-R4. The window agent
  personally performs the final integration assessment and may report only
  `READY_FOR_PARENT_REVIEW` or one parent-level blocker. It cannot edit an
  implementation file, update A5/A6, accept KI-R4, or begin KI-W4.
- **Durable identity gate:** immediately after `latestAttempt` is found and
  before any state/code classification, cache read, ambiguity write, retry
  schedule, S3 operation, terminal write, or dispatch,
  `recoverClaimedTask` compares
  `latestAttempt.requestFingerprint` with `current.task.requestFingerprint`.
  Unequal values, including null/undefined or a different 64-hex fingerprint,
  throw `PipelineInvariantError("PIPELINE_INPUT_CONFLICT")`. Equal values
  continue through the existing six schedules unchanged. All ordinary planned,
  in-flight, failed-terminal, failed-retryable, and attempt-five fixtures use
  the real task request fingerprint; three explicit mismatch cases prove the
  guard precedes `markAttemptAmbiguous`, `scheduleRetry`, `terminalize`, S3,
  and both dispatch types.
- **Dispatcher own-key gate:** after the existing non-null/non-array/plain-
  prototype check, enumerate own keys with `Reflect.ownKeys(options)`. Accept
  only an empty list or the one string key `delaySeconds`; any symbol key,
  non-enumerable extra string key, or second own key throws
  `PIPELINE_MESSAGE_INVALID` before `client.send`. The existing integer
  `0..900`, omitted/empty command, and client-failure behavior is unchanged.
- **Commit-stable historical conformance:** permanent SCN-KI-032 Git checks use
  the immutable pair baseline
  `37a0e0203d265f539b566f1536642cd2f4eb2d99` and accepted handoff candidate
  `077213cc7c33fa8209a1e5d8ff365b73766500dc`; they never use live `git status`
  or an unstaged-only `git diff`. C05 requires nonempty hunks for all three R3
  production files before checking symbol spans. C06 compares the fixed-revision
  changed-path set to the literal nine R3 paths. C07 inspects added imports from
  that same fixed diff. These permanent tests therefore pass on clean committed
  checkouts and after successor commits. KI-R4's own exact eight-file scope is
  a handoff-only window-agent integration oracle comparing the KI-R4 baseline
  commit to the assembled worktree; it is not encoded as a permanent global
  worktree-status assertion.
- **Case-set and digest enforcement:** the existing R3 manifest remains
  byte-identical. Every R3 group test compares its recomputed digest to the
  full fixed digest recorded in KI-R4; matching `/^[a-f0-9]{64}$/` alone is
  forbidden. SCN-KI-032 independently recomputes all seven R3 group digests and
  the global 101-ID digest and compares them to the fixed values. A new strict
  `ki-r4-enforcement-manifest-v1` contains exactly the fifteen IDs in KI-R4,
  divided into the five literal groups there; its root, group sets, case sets,
  counts, required/registered/executed equality, and global digest
  `6adc8ab132496c58608734549fbbc596577e1bd71c1e730349575eb96badc941`
  are independently asserted. The cumulative required set at KI-R4 handoff is
  the union of the 101 R3 IDs and 15 R4 IDs, with no duplicate.
- **Falsification controls:** controls mutate captured in-memory result/trace
  evidence while rerunning the same production oracle. A01 deletes
  `providerCostUsd` from a successful active result and the exact deep-equality
  oracle must throw `AssertionError`; W04 appends `sendCheck` after an ordinary
  lost terminal result and the unchanged zero-check oracle must throw; W05
  appends `terminalize,sendCheck` to a recovery lost trace and both unchanged
  forbidden-operation oracles must throw; G01 appends the first forbidden
  post-loss operation to the captured aggregation trace and the unchanged
  zero-later-operation oracle must throw. Comparing different repository
  outcomes, removing provider input cost, or running a no-loss path is not a
  mutation control and cannot satisfy these cases.
- **Database registration and isolation:** SCN-KI-030 creates exactly one
  disposable non-public schema by calling `withIsolatedDb` once. Inside that
  callback, the Node test context registers D01–D05 as five named `t.test`
  subtests; `t_scn030` receives the shared `{db,repo}` rather than creating a
  schema. The five cases remain sequential, independently named, and retain
  their existing row/call/object oracles. One outer cleanup drops that exact
  schema and proves exact-name absence. No full opted-in suite or second
  database acceptance run is permitted.
- **R4 case manifest:** groups and IDs are exactly:
  `adapter_control=[R4-A01-active-cost-output-omission-falsifies]`;
  `dispatcher=[R4-Q01-symbol-extra-key-rejected,R4-Q02-nonenumerable-extra-key-rejected]`;
  `worker_component=[R4-W01-planned-identity-mismatch-conflict,R4-W02-terminal-failure-identity-mismatch-conflict,R4-W03-retryable-failure-identity-mismatch-conflict,R4-W04-ordinary-lost-check-injection-falsifies,R4-W05-recovery-lost-write-injection-falsifies]`;
  `aggregation_control=[R4-G01-post-loss-operation-injection-falsifies]`;
  `conformance=[R4-C01-fixed-revision-diff-nonempty,R4-C02-fixed-revision-file-set-exact,R4-C03-fixed-revision-import-set-clean,R4-C04-r3-group-digests-exact,R4-C05-r3-global-digest-exact,R4-C06-live-worktree-independent]`.
- **Verification economy:** leaf agents run only file-local static/unit checks
  that cannot write another workspace file. The window agent runs, once after
  all leaf edits: one non-database focused gate for SCN-KI-028/029/031–035; one
  focused SCN-KI-030 isolated-database gate; two keyword-only builds plus the
  unchanged packaging test; one `npm test`; and one secret scan. A correction
  reruns only invalidated gates plus mandatory scope/case/secret/regression
  closure; the database gate is repeated only if its source, harness, schema
  lifecycle, or asserted production path changed after its successful run.
- **Rejected:** reopening KI-R3; accepting live-worktree Git tests as permanent
  regression tests; counting a switch branch without named registration;
  regex-only digest assertions; symbol/non-enumerable option extras; unequal
  attempt/task identity; controls that merely choose a different valid input;
  one schema per database case; direct parent-to-leaf communication; parallel
  leaves; a window-agent implementation edit; and KI-W4 work before acceptance.
- **Tasks/scenarios:** `KI-R4-T1`–`T4`, `SCN-KI-033`–`035`, corrected
  `SCN-KI-028`–`032`, and the KI-R4 subordinate decomposition/assessment
  package.

### `DEC-KI-033` — W4 owner API, direct query-review handoff, and enforcement closure

- **Requirements:** `REQ-KI-001`, `002`, `005`, `007`–`013`, `015`–`019`;
  `INV-KI-003`, `010`, `013`–`015`; `EXC-KI-003`, `005`, `007`, `008`.
- **Locked owner projection:** add
  `PrismaKeywordResearchRepository.getOwnedApiView({researchId,ownerId})`.
  It validates the canonical IDs, performs one owner-filtered `findFirst`, and
  includes the research's three stage rows ordered by
  `stage asc,generation asc`. It returns only
  `{outcome:"found",research}|{outcome:"not_found"}`. The accepted worker
  projections and `getOwned` remain byte-for-byte behaviorally unchanged.
  `ResearchView.progress` is derived from these stage rows, never from queue
  state or S3: absent rows are zero counts; a nonterminal research reports the
  first incomplete stage in fixed order `expansion,anchor_screen,
  market_overview`; all three completed while the research transaction is not
  yet completed reports `finalizing`; terminal research reports `completed` or
  `failed`. `result` is non-null only for `state=completed`.
- **Locked service interface:** create
  `createKeywordResearchApi({keywordRepository,runRepository,
  dispatchInitialize,now,researchIdFactory,runIdFactory,configSnapshot})` in
  `src/keyword-intelligence/api.js`. It returns the five methods
  `createResearch({ownerId,body})`, `getResearch({ownerId,researchId})`,
  `saveSelection({ownerId,researchId,body})`,
  `createRun({ownerId,researchId,body})`, and
  `exportCsv({ownerId,researchId,searchParams})`. Defaults are
  `now=()=>new Date()`, `researchIdFactory=newResearchId`,
  `runIdFactory=newRunId`, and `configSnapshot=keywordResearchConfigV1()`.
  The config fingerprint is `fingerprintJson(configSnapshot)`. All request,
  result, selection, snapshot, filter, and return objects use strict Zod
  parsing; unknown keys fail before a durable or external operation. Successful
  method results are exactly `{research}`, `{research}`, `{research}`,
  `{created:boolean,run,statusUrl:"/api/runs/"+run.id}`, and the CSV string in
  that order; methods throw only privacy-safe `ApiError` instances described
  below. The server injects this service as `keywordResearchApi`; no route calls
  the keyword repository directly.
  Every owner read also requires the persisted v1 config to parse and
  `fingerprintJson(research.configSnapshot)===research.configFingerprint`;
  mismatch is contract drift, never a fallback to the current code default.
- **Locked create/recovery boundary:** `createResearch` normalizes with
  `normalizeSeeds`, writes the exact v1 snapshot, nine markets and fingerprint
  through `keywordRepository.create`, then and only then calls
  `dispatchInitialize({contractVersion:1,type:"keyword.initialize.v1",
  researchId,generation:1})`. A send failure or thrown dispatcher error is
  swallowed only after the durable create and returns the same 202 owner view;
  queued-row recovery remains the only retry authority. A rejected request
  writes nothing and sends nothing. The API performs no DataForSEO, S3, Google,
  or worker operation. The create contract has no idempotency key: the server
  never automatically retries POST, and a second accepted POST intentionally
  allocates a distinct research with its own `$3.00` cap. Only initialize
  delivery for an already-created research is recovered/idempotent; clients
  must retain the first successful 202 response rather than replaying creation.
- **Locked selection materialization:** add the pure export
  `classifyKeywordForSelection(keyword,{mainIntent,stripTokens})` to
  `cluster.js`; it calls the already-accepted token, facet, and lane functions
  in that order and returns exactly `{lane,facets}`; `stripTokens` is the
  persisted config array and `mainIntent` is a valid intent or null. It changes
  none of their existing callers. `saveSelection` accepts the
  exact `DEC-KI-014` shape and materializes a canonical draft before the
  repository CAS. Calculated items must name a result keyword through
  `sourceKeywordId`, use its deterministic calculated `itemId`, preserve its
  `originalKeyword`, `sourceSeeds`, and exact metrics snapshot, and may change
  only normalized `keyword`; edited text is reclassified with the source
  `mainIntent`. Manual items require `sourceKeywordId:null`,
  `metricsSnapshot:null`, `originalKeyword===keyword` after normalization,
  deterministic manual `itemId`, the research's first seed as the sole source
  seed, and classification with `mainIntent:null`. Client-supplied lane,
  facets, source, ID, or metrics that differs from this canonical value is a
  400 error; nothing is silently repaired. `analyzeSelectionConflicts` runs on
  the canonical draft. Revision mismatch is the sole
  `KEYWORD_SELECTION_REVISION_CONFLICT` 409.
- **Locked handoff:** finalization reads the owner projection, requires
  `state=completed`, exact expected selection revision, 1–100 canonical items,
  and zero conflicts. The selection fingerprint is exactly
  `fingerprintJson({contractVersion:"keyword-selection-v1",researchId,
  selectionRevision,items})` (the lowercase SHA-256 emitted by that accepted
  helper). The immutable snapshot is exactly
  `{contractVersion:"keyword-run-snapshot-v1",researchId,selectionRevision,
  selectionFingerprint,configFingerprint,dedupStripTokens,seeds,items}`, where
  `configFingerprint` is the research's persisted fingerprint,
  `dedupStripTokens` is a copied ordered array from its persisted
  `configSnapshot.dedup.stripTokens`, and every snapshot item is the full
  canonical `SelectionItem` plus `initialQuery`. The API supplies that snapshot
  and the run repository's two transaction-composable callbacks to the accepted
  keyword repository `createRun` transaction.
- **Locked Run construction:** export `newRunId()` from
  `prisma-run-repository.js` using the existing Run ID formula, and add
  instance methods `createKeywordResearchRun(tx,input)` and
  `createKeywordResearchQueries(tx,input)`. The API calls the accepted
  repository exactly as
  `keywordRepository.createRun({researchId,ownerId,
  expectedSelectionRevision,clientRequestId,selectionFingerprint,runId,
  items:snapshot.items,constructRun:(tx,context)=>runRepository.
  createKeywordResearchRun(tx,{...context,selectionRevision,
  selectionFingerprint,snapshot}),constructQueries:(tx,context)=>
  runRepository.createKeywordResearchQueries(tx,{...context,snapshot})},now)`;
  no other callback input or outer write is permitted. The run method requires
  `{research,runId,now,items,selectionRevision,selectionFingerprint,snapshot}`;
  it derives categories from `research.seeds`, calls existing
  `runCreateData(research.ownerId,categories,runId)`, and overrides only the
  exact keyword fields below in one `tx.run.create`. The query method requires
  `{run,items,now,snapshot}`, requires `items` deep-equal `snapshot.items`, maps
  once with `mapSelectionToQueries(items)`, performs one
  `tx.runQuery.createMany`, requires its count to equal N, and returns the same
  constructed ordered rows without a read. The run starts directly in
  `state="awaiting_query_confirmation"`, `phase="query_review"`,
  `stage="awaiting_query_confirmation"`, `queryRevision=1`, and
  `queryPlanReadyAt=now`; it also stores `keywordResearchId=research.id`,
  `keywordSelectionRevision=selectionRevision`,
  `keywordSelectionSnapshot=snapshot`, and
  `queryPlanSource="keyword_research"`; `confirmedQueryRevision`,
  `queriesConfirmedAt`, and every lease field remain null. It is not queued for
  query planning. Its categories
  are the ordered normalized research seeds mapped to
  `{originalShopType:seed,shopType:seed,businessQualifier:"unspecified"}`;
  all other run configuration comes from the existing `runCreateData` snapshot.
  Each selection item creates one ordered `RunQuery` with the mapped query,
  `source="generated"`, `validationState="pending"`,
  `generationReason="keyword_research"`, its stable
  `keywordResearchItemId`, and `categoryIndex` equal to the index of its first
  `sourceSeeds` member in the research seed array. Missing source membership,
  unequal callback output, or any write failure aborts the complete handoff.
  The run route does not call `queueDrain`; the existing start route does so
  only after explicit query confirmation.
- **Locked invalid-callback rollback:** in
  `PrismaKeywordResearchRepository.createRun`, add one private
  `RunHandoffAbort` sentinel and an outer catch matching the accepted
  `FinalPublicationAbort` pattern. After either callback has written, an
  invalid Run identity/lineage result or invalid query array/count/run ID must
  throw that sentinel inside the interactive transaction; the outer catch maps
  it to `{outcome:"conflict",code:"KEYWORD_RUN_HANDOFF_INVALID"}` only after
  rollback. Pre-write conflict returns and exact replay remain unchanged;
  callback/database exceptions still escape after rollback. Returning a
  conflict normally after a callback write is forbidden.
- **Locked durable research edit:** the only existing run-repository mutation
  changed is `replaceEditableQueries`. After its owner/state/revision read and
  before its revision CAS, a `keyword_research` run requires the incoming query
  IDs to equal the persisted query-ID set, every persisted row to have a unique
  non-null `keywordResearchItemId`, every incoming category index to equal that
  row's persisted category index, and no incoming row without a matching ID.
  Its replacement rows preserve the exact persisted `id`,
  `keywordResearchItemId`, `createdAt`, `queryScore`, `generationReason`,
  `sourceUrls`, and `categoryVocabulary`. Reorder-only changes update only
  `sequence`/`updatedAt` and preserve `source` and probe evidence; a query-text
  change also sets `source="user_edited"`, `validationState="pending"`, clears
  rejection/probe fields, and updates `query`/`updatedAt`. The
  delete+bulk-create remains inside the existing revision-CAS transaction.
  The `legacy` branch, including user-added rows, is byte-for-byte behaviorally
  unchanged; an unknown discriminator throws `PIPELINE_INPUT_CONFLICT` before
  the CAS.
- **Locked edit and confirmation branch:** add
  `validateResearchBackedQueryList(queries,run)` and
  `validateResearchBackedConfirmedQueryRows(rows,categories,config,status,
  options)` in `query-review.js`. The edit validator accepts the existing
  strict `{id,categoryIndex,query}` rows, recovers each immutable item ID from
  the persisted RunQuery, and delegates grammar/relevance to
  `validateResearchBackedQueries`; it requires exactly the persisted query-ID
  and item-ID sets, 1–100 rows, unchanged category index and stable lineage,
  while allowing order and query text changes. Its return is exactly
  `{valid:boolean,queries:[{id,categoryIndex,query}],errors:[]}` using the
  existing public error-row vocabulary. The confirmation validator requires
  `options.snapshot` to be the strict immutable run snapshot; creates the
  `sourceKeywords` map from its items keyed by `itemId`; maps every durable row
  to `{itemId:row.keywordResearchItemId,sequence:row.query}`; revalidates with
  `validateResearchBackedQueries` and `snapshot.dedupStripTokens`; and then uses
  its returned normalized `phrase` (never either site prefix) for both legacy-
  named probe-candidate fields `product_phrase` and `product_family`, while
  `query` remains the full mapped query. The other candidate fields are exactly
  `market_signal:"user_confirmed"`, `seasonality:"unknown"`, the persisted
  generation reason/source URLs, and `confidence:1`. It then uses the existing
  freshness/fingerprint/probe normalization seam once per non-reusable valid
  row. It returns the same
  `{valid,errors,rows,queryPlans}` shape as `validateConfirmedQueryRows`, except
  validity is all 1–100 rows valid and never an exact per-category count. Weak
  and failed probes return the run to editable review with their saved evidence
  and no replacement generation.

  `createLeadServer` adds injected
  `researchQueryValidationPipeline=validateResearchBackedConfirmedQueryRows`
  and optional `keywordResearchApi`. When that injection is absent it constructs
  exactly one service per server from
  `new PrismaKeywordResearchRepository(repository.prisma)`, the existing
  `repository` as run repository, `now:()=>currentDate(now)`, and a lazy
  `dispatchInitialize` that calls the existing `pipelineRuntimeFactory`, then
  `runtime.dispatcher.sendOne(runtime.config.
  awsPipelineKeywordResearchQueueUrl,message,keywordMessageSchema)`. Missing
  dispatcher or missing/invalid keyword queue URL returns a failed-send result
  without an SQS call; the already-committed queued research remains for the
  accepted recovery path. W4 does not read environment variables or add the
  queue config key; `DEC-KI-027`/W7 remain the sole config/infrastructure owner.
  `drainQueue` passes `queryPlanSource` and
  `keywordSelectionSnapshot` from the claimed Run into `executeRun`. Both the
  edit and explicit-start request paths select the research edit validator only
  for `keyword_research`. Both local and AWS confirmed-query branches inside
  `executeRun` select `researchQueryValidationPipeline` only for that same
  discriminator and supply the immutable snapshot; `legacy` continues through
  the existing validators, exact-count policy and injected
  `queryValidationPipeline`. Any other discriminator is
  `PIPELINE_INPUT_CONFLICT` before edit, confirmation, probe or dispatch.
- **Locked public serialization:** add `serializeSelectionItem` and
  `serializeKeywordResearch` to `api-serializer.js`. They emit exactly
  `DEC-KI-019`; config, owner, stage leases, S3 keys, task/attempt/cache rows,
  raw provider values, credentials, and every internal fingerprint are absent.
  `serializeRun` conditionally adds
  `queryPlanSource:"keyword_research"`, `keywordResearchId`, and
  `keywordSelectionRevision` only for research-backed runs;
  `serializeRunQuery` conditionally adds `keywordResearchItemId` only when
  non-null. Legacy serialized objects therefore retain their exact prior key
  set.
- **Locked routes and errors:** `server.js` adds only the five `DEC-KI-019`
  routes and an exact `requestedKeywordResearchId` parser for
  `^kr_[A-Za-z0-9_-]{24}$`. Owner identity comes only from `trustedUserId`.
  Success is 202 create, 200 load/save/export, and 201 new or 200 identical
  handoff retry. Exact keyword errors are: malformed path/body/query or
  noncanonical selection → 400 `KEYWORD_RESEARCH_INPUT_INVALID`; unsupported
  persisted research/result/selection/snapshot contract → 409
  `KEYWORD_RESEARCH_CONTRACT_MISMATCH`; missing/cross-owner → 404
  `KEYWORD_RESEARCH_NOT_FOUND`; not completed → 409
  `KEYWORD_RESEARCH_NOT_COMPLETED`; nonempty selection conflicts → 409
  `KEYWORD_SELECTION_HAS_CONFLICTS`; stale selection revision → 409
  `KEYWORD_SELECTION_REVISION_CONFLICT`; unequal handoff replay or invalid
  callback output → 409 `KEYWORD_RUN_HANDOFF_CONFLICT`. Research query
  edit/start retains existing 422 `QUERY_LIST_INVALID`, 409 query-revision/
  lifecycle codes, and 404 `RUN_NOT_FOUND`; unexpected failures use the
  existing safe 500 mapper. No response contains provider text. CSV is
  `text/csv; charset=utf-8`, `Content-Disposition: attachment;
  filename="keyword-research-<researchId>.csv"`, and `Cache-Control: no-store`.
- **Locked export predicate/order:** parse exactly the `DEC-KI-019` query
  parameters, rejecting unknown names, duplicates other than at most 20
  `flag` values, malformed bounds, and empty normalized values. `market=all`
  uses cumulative row metrics; a named market excludes null market rows and
  overlays exactly `searchVolume,cpc,competition,competitionLevel,
  keywordDifficulty,mainIntent,commercialIntent,monthlyHistory,trendSlope,
  flags,opportunityScore,recommended` from that market metric. Filters are
  conjunctive: seed membership under NFKC/trim/collapse/case-fold; exact
  cluster ID, effective intent, lane, and facet membership; effective numeric
  minima; effective recommendation; every requested flag present; and
  case-folded substring search over keyword, source seeds, cluster text, lane,
  facets and effective flags. Preserve the persisted result-keyword order and
  pass the projected rows to the accepted `serializeKeywordsCsv`; zero matches
  returns its header plus LF.
- **Enforcement set:** the literal `ki-w4-enforcement-manifest-v1` contains 34
  globally unique IDs in groups `api_component=8`, `server_routes=6`,
  `query_review=8`, `handoff_database=6`, and `conformance=6`. Its normative
  sorted-member-plus-LF SHA-256 is
  `86810ce87a79426bb972be2e2827abc3806835190135d17769b52c33e7bb2203`.
  Every group is an executable registry; an ID becomes executed only after its
  activation witness and oracle pass. Required, registered, and executed sets
  must be equal with zero skip, duplicate, unexpected, filtered, or
  unactivated member.
- **Critical falsification controls:** the final assessment must demonstrate
  failure for removal of the owner predicate; dispatch-before-commit; result
  exposure before completion; removal of selection revision CAS; split run/
  query writes; omitted query lineage; routing a research run through the
  legacy validator; permitting add/delete; bypassing one probe; routing a
  legacy run through the research validator; adding a raw/internal response
  field; ignoring/reordering export filters; accepting unsupported persisted
  versions; bypassing auth/path strictness; mapping every lane as a product
  query; permitting forbidden query grammar; removing handoff replay
  uniqueness/fingerprint fencing; and each missing/duplicate/skipped/
  unexpected/unactivated/weakened-oracle/divergent-substitute enforcement
  defect. Controls mutate injected
  test collaborators or in-memory captured evidence only, never production
  source or external state.
- **Verification economy:** leaf agents run only one-file static or focused
  non-database checks. The window agent runs once on frozen final inputs: the
  complete non-database W4 registry, one six-case integration test inside one
  isolated disposable schema, the existing keyword parity/query/legacy
  regressions, one `npm test`, and one secret scan. No Prisma generate/validate,
  worker/Lambda build, full opted-in database suite, provider call, AWS action,
  or repeat of an unchanged successful stateful gate is required.
- **Substitute fidelity:** API/server fakes prove strict call order, status and
  redaction but not SQL atomicity; the six real-Prisma cases prove durable
  owner/CAS/rollback/lineage behavior. The mock dispatcher is bounded to the
  already accepted `sendOne` contract; the mock probe reproduces one result or
  failure per query and proves call counts but not live Google behavior. No W4
  acceptance claim exceeds these parity classes.
- **Rejected:** reading stage progress from S3/queue; API access through cache;
  trusting client metrics/lane/facets/owner; queuing a research run through the
  legacy planner; product-only validation for research rows; adding or deleting
  research-backed query rows; recomputing a historical snapshot from live
  research; live provider/AWS proof; broad repeated integration/build gates;
  and summary-only coverage evidence.
- **Tasks/scenarios:** `KI-W4-T1`–`T4`; `SCN-KI-003`, `008`, `009`, `014`,
  `015`; W4 cases `W4-A01`–`A08`, `W4-S01`–`S06`, `W4-Q01`–`Q08`,
  `W4-D01`–`D06`, and `W4-C01`–`C06`.

### `DEC-KI-034` — Corrected W4/W5 wire and selection-mutation contract

- **Requirements:** `REQ-KI-005`–`009`, `014`, `018`, `021`;
  `INV-KI-009`, `010`, `013`; findings `KI-PR-F01`–`F04`.
- **Locked response version:** the persisted, worker-result, backend API and
  frontend value is the JSON number literal `1`. Frontend `ResearchView` and
  `ResearchResult` types are `contractVersion:1`; both strict parsers require
  exact finite integer `1`. A string, other number, null, missing value or
  unknown key is `ApiPayloadError`. All W5 fixtures use numeric `1`; at least
  one conformance case constructs the response through the actual W4
  `serializeKeywordResearch` and passes that object to the actual W5 parser.
  No persisted row, result artifact, response serializer or backend version is
  changed or migrated.
- **Locked browser request headers:** each of
  `createKeywordResearch`, `saveKeywordSelection`, and
  `startKeywordResearchRun` supplies explicit
  `Content-Type: application/json` in its own request init. `apiRequest`'s
  shared behavior and every legacy caller remain unchanged. GET has no content
  type. An emitted Next pass-through control must reach the existing
  unauthenticated 401 branch, not the pre-authentication 415 branch; intercepted
  browser fixture success is not route-handler evidence.
- **Locked selection input:** replace only the PUT request-item shape with the
  strict discriminated union `SelectionMutationItem`:
  `CalculatedSelectionMutation={sourceKind:"calculated",
  sourceKeywordId:string matching /^ksi_[a-f0-9]{12}$/,
  keyword:string}` and
  `ManualSelectionMutation={sourceKind:"manual",keyword:string}`. The request
  remains exactly `{expectedRevision:int>=1,items:SelectionMutationItem[0..200]}`;
  unknown keys, a calculated null/missing source ID, or any manual source ID,
  item ID, metrics, lane, facets, seed or original text reject 400. Keyword
  normalization and 1–160-code-point bounds remain `DEC-KI-014`.
- **Locked materialization:** frontend drafts and responses remain full
  `SelectionItem[]`. Before PUT, the client maps each item in order to the union
  above and sends no snapshot/derived field. For a calculated input, W4 finds
  the exact persisted result row by `sourceKeywordId`, recomputes its
  deterministic calculated item ID, retains its original keyword/source seeds/
  metrics, normalizes the supplied editable keyword, and reclassifies lane and
  facets with its persisted intent. For a manual input, W4 derives the six-byte
  `DEC-KI-002` ID, first research seed, null source/metrics, original normalized
  text, lane and facets. Client-only unsaved row keys have no wire, durable or
  identity authority and are replaced by the canonical response after save.
- **Locked size:** both the emitted Next selection route and W4 selection route
  accept at most `262144` UTF-8 bytes and return 413 above it. The fixed strict
  union's measured hard maximum is 143,641 bytes for 200 calculated items with
  160 four-byte-code-point keywords, so every valid 0–200 request fits. Body
  length never authorizes an unknown key. Create remains 32 KiB and handoff
  remains 4 KiB/32 KiB as currently implemented.
- **Payload certificate `PAY-KI-008`:** producer is W5
  `saveKeywordSelection`; consumers are the emitted Next selection route and
  W4 `saveSelection`; discriminator is `sourceKind`; strict fields/types/bounds
  are the union above; normalized output is the existing canonical full
  `SelectionItem[]`; unknowns reject 400; oversize rejects 413; safe errors and
  owner/revision rules remain `DEC-KI-019/033`; no owner, raw body, credential,
  provider field or contact data is logged/stored as request evidence.
- **Evidence:** `SRC-KI-034`–`036`, `PAY-KI-007`, current W4/W5 source.
- **Rejected:** string version; dual-version parser; browser-side BLAKE2s
  dependency; trusting browser metrics/IDs/classification; raising the limit to
  carry full snapshots; permissive old/new request union; changing durable
  selection/result schemas.
- **Consequences:** one bounded request supports the full 200-item draft; W4
  remains sole canonical identity/metrics authority; legacy full-snapshot PUT
  clients receive 400 and must use the corrected internal v1 request.
- **Tasks/scenarios:** `KI-R5-T1`, `KI-R5-T4`, `KI-R5-T5`; `SCN-KI-036`, `SCN-KI-038`;
  cases `R5-WIRE-01`–`06`, `R5-SEL-01`–`08`.

### `DEC-KI-035` — Saved-draft finalization and durable handoff retry

- **Requirements:** `REQ-KI-007`–`009`, `015`, `016`; `INV-KI-010`, `013`,
  `015`; findings `KI-PR-F05`, `F06`.
- **Locked saved predicate:** define the ordered mutation projection from
  `DEC-KI-034`. A draft is saved iff its projected array is deeply equal by
  length, order, discriminator, source ID presence/value and exact keyword to
  the projection of `view.selection`. `canFinalizeSelection` adds reason
  `unsaved` before conflict success. Add/remove/edit/reorder/manual changes all
  block handoff with zero POST until a successful save response replaces the
  view/draft at the incremented revision. Finalize never auto-saves and never
  uses the visible draft as an unpersisted snapshot.
- **Locked client attempt lifecycle:** state is
  `idle -> handing_off -> succeeded | definitive_failure | retry_required`.
  Allocate one `clientRequestId` with the existing formula when entering from
  idle and pair it with the current saved selection revision. A parsed HTTP
  response below 500 is definitive: success navigates; 4xx applies existing
  safe UI handling and clears the attempt. Network failure, unreadable response
  or HTTP `>=500` is ambiguous: retain the exact ID/revision, enter
  `retry_required`, show a truthful retry message, make draft/save controls
  inert, and permit only a retry of the same handoff. Retry uses byte-identical
  ID and revision. It remains retry-required on another ambiguous outcome.
  Reload may reconstruct only durable server state; because the ID is not
  durable in the browser, the UI must not claim an unobserved result after a
  reload, and this scope adds no browser persistence.
- **Locked repository race recovery:** `createRun` keeps its current first
  transaction. If that transaction throws a recognized unique-constraint
  error, run one fresh repository transaction that reads the exact
  `(researchId,clientRequestId)` handoff, compares selection revision and
  fingerprint, then reads its Run. Equal+present returns `found`; unequal or
  missing Run returns conflict; absence of the handoff rethrows the original
  error. No second Run/RunQuery/handoff write occurs. Other exceptions still
  escape. Two concurrent equal requests therefore both fulfill as one
  `created` and one `found`, point to one Run, and exact later replay is found;
  unequal same-key input remains conflict.
- **Atomicity:** all writes remain the existing single handoff transaction;
  race reconciliation is a read-only post-rollback transaction and cannot make
  partial writes visible.
- **Evidence:** `SRC-KI-034`, existing handoff unique and W4-D04 behavior.
- **Rejected:** clearing every error; new ID after timeout; auto-saving before
  finalize; localStorage idempotency; treating a unique error as success
  without reading/validating the durable handoff; weakening one-Run atomicity.
- **Tasks/scenarios:** `KI-R5-T2`, `KI-R5-T4`, `KI-R5-T5`; `SCN-KI-037`, `SCN-KI-038`;
  cases `R5-FIN-01`–`08`.

### `DEC-KI-036` — Selection validity, filter parity and safe CSV cells

- **Requirements:** `REQ-KI-008`–`010`, `014`, `018`; `INV-KI-009`, `010`;
  findings `KI-PR-F07`–`F09`.
- **Locked duplicate boundary:** after all mutation inputs materialize to full
  canonical items and before conflict analysis or repository CAS, W4 must call
  the existing `validateSelectionDraft`. Any duplicate derived item ID or other
  draft-invalid result is 400 with zero repository write. Conflict analysis
  remains for distinct exact/near-similar items and never substitutes for input
  uniqueness.
- **Locked filter parity:** W4 `matchesFilters` is authoritative. W5's visible
  table uses its exact effective market overlay and conjunctive predicate:
  normalized case-insensitive source-seed membership; exact cluster, intent,
  lane and facet membership; numeric minima; exact recommendation; **every**
  selected flag present; and case-folded substring search only over keyword,
  source seeds, cluster text, lane, facet values and effective flags. Do not add
  standalone primary seed, main intent or synthetic `recommended` text to the
  search corpus. Persisted result order is preserved before independent UI
  sorting/pagination; export receives the filter query and preserves backend
  filtered order. Tests use literal expected item-ID sets/CSV, never one side's
  predicate as the other side's oracle.
- **Locked CSV safety:** before RFC4180-style comma/quote/newline escaping,
  prefix exactly one ASCII apostrophe to every **textual** keyword export cell
  whose raw string starts with tab/CR or matches `/^\s*[=+\-@]/u`. Apply to
  keyword, seed, joined source seeds, competition level, intent, cluster,
  cluster ID, lane, serialized facets, variant IDs/text, joined flags,
  merged-into, serialized monthly history and joined markets. Numeric columns,
  including a negative trend slope, retain their accepted formatting and never
  receive an apostrophe. Apply once only; an already apostrophe-prefixed value
  is unchanged. Header/order/LF and all other Python-parity formatting remain.
- **Evidence:** `SRC-KI-034`; existing W4 predicate and general CSV safety
  precedent.
- **Rejected:** frontend OR/backend AND; self-derived export fixtures; silently
  dropping duplicates; formula stripping; neutralizing negative numeric cells;
  replacing the accepted keyword CSV formatter wholesale.
- **Tasks/scenarios:** `KI-R5-T1`, `KI-R5-T3`, `KI-R5-T4`, `KI-R5-T5`; `SCN-KI-036`,
  `SCN-KI-039`; cases `R5-SEL-04`–`05`, `R5-EXP-01`–`06`.

### `DEC-KI-037` — KI-R5 enforcement and accepted-evidence supersession

- **Requirements:** all requirements and invariants named by `DEC-KI-034`–`036`.
- **Locked case set:** `ki-r5-enforcement-manifest-v1` contains exactly the five
  literal groups in A4: `wire` 6, `selection` 8, `finalization` 8, `export` 6,
  `conformance` 6. The 34-ID per-member-LF digest is
  `507186e7489a3f9eec18eb5de78692dbc55a8d1d2d106544aa4295a98ac9be60`.
  Required, registered and executed sets must be byte-equal with zero skip,
  duplicate, unexpected, filtered or unactivated ID.
- **Accepted-test policy:** KI-R5 explicitly owns only the listed W4/W5 tests
  and browser fixture whose previous evidence supported the defective
  boundaries. Changing them invalidates only their affected W4/W5 assertions;
  KI-R5 cases and evidence must supersede those assertions while preserving
  every unrelated accepted registration/oracle. Static deep-equality of
  unrelated case sets plus the frozen legacy/backend/frontend suites is
  required. The unexecuted KI-W6 decomposition is invalidated wholesale by the
  predecessor/dependency and revision change and must be reauthored after R5.
- **Exact accepted-assertion supersession:** the only existing case oracles
  authorized to change are W4
  `{W4-A04,W4-A06,W4-A07,W4-S04,W4-S06,W4-D04}` and W5
  `{W5-A05,W5-A06,W5-A09,W5-A10,W5-C05,W5-C08,W5-C12,W5-B02,W5-B03,
  W5-B04,W5-B05,W5-R03}`. Their stable IDs and registrations remain; each
  changed oracle must cite the corresponding R5 case(s). Numeric-version and
  request-seam fixture corrections cause all W5 browser IDs `W5-B01`–`B08`
  and `W5-R01`–`R07` to rerun under V4, but no browser oracle outside the five
  listed B02–B05/R03 members may change. Every other accepted W4/W5 case ID,
  registration, activation witness and oracle is byte/semantic read-only.
- **Substitute fidelity:** backend API fakes prove parsing/materialization/call
  order but not SQL; `R5-FIN-07/08` use real Prisma in one isolated schema for
  unique-race/atomicity. Frontend fetch capture proves exact client request
  init; emitted Next pass-through proves the real handler's pre-auth media-type
  boundary by 401-not-415; actual W4 serializer-to-W5 parser conformance proves
  the wire object. The intercepted dashboard fixture proves presentation only
  and is forbidden as Next/backend route evidence. Full authenticated local
  workflow remains `KI-W6` and is not claimed by R5.
- **Critical controls:** old string version; missing content type; legacy full
  selection item; omitted duplicate validation; dirty-gate bypass; ambiguous
  key reset; unique-race reconciliation removal; OR flag semantics; extra
  search corpus; missing text neutralization; intercepted route substituted for
  pass-through; and each missing/duplicate/skipped/unexpected/unactivated/
  weakened-oracle/divergent-substitute enforcement defect must make its
  unchanged oracle or execution lint fail before production passes.
- **Frozen gates:** editing uses only file-local/static/focused non-DB
  diagnostics. On final frozen inputs run once: focused backend non-DB cases;
  focused frontend API/component/inventory cases; one focused isolated-schema
  handoff integration; one frontend `npm run check`; one emitted Next browser
  harness reusing that build; one backend `npm test`; one secret scan; and one
  conformance/set-equality merge. A relevant later edit invalidates and reruns
  only the affected gate. No Prisma generation/validation, full opted-in DB
  suite, worker build, provider, AWS or production operation is permitted.
- **Evidence:** `SRC-KI-034`–`037`; authoring standard Sections E6–E8 and 11.
- **Tasks/scenarios:** `KI-R5-T5`; `SCN-KI-036`–`040`; all `R5-*` cases.

### `DEC-KI-038` — KI-W6 workspace navigation and causal local-proof contract

- **Requirements:** `REQ-KI-001`–`024`, `INV-KI-001`–`015`,
  `EXC-KI-001`–`008`, `AUTH-KI-001`–`004`, `AUTH-KI-006`–`007`.
- **Navigation choice:** keep the accepted backend response
  `statusUrl:"/api/runs/<Run.id>"` unchanged because it names the owner-scoped
  API status resource. On either successful initial handoff or successful
  same-key retry, the dashboard must instead call exactly
  ``router.push(`/runs/${encodeURIComponent(handoff.run.runId)}`)``. A supplied
  `statusUrl`—including a valid but different same-origin URL—must never choose
  the browser destination. The accepted `R5-FIN-01` fixture/oracle is the only
  earlier browser assertion superseded by this choice; its registration and all
  other R5 registrations/oracles remain unchanged.
- **Causal proof topology:** one emitted Next 16 build and one local Chrome CDP
  workflow must traverse the real `/keywords`, same-origin Next route handlers,
  installed Neon Auth server client, backend proxy, actual backend HTTP server,
  actual Prisma repositories in one disposable migrated schema, actual keyword
  worker/service/parser/publication code, actual dashboard/run-workspace/query-
  review UI, actual research-backed query validator and strict Google response
  parser, and actual discovery/domain services. Test
  boundaries are limited to a deterministic local Neon-Auth HTTP response,
  the existing injected DataForSEO `runtime.http`, the existing
  `researchQueryValidationPipeline` server dependency supplied as a wrapper
  around the production validator with a deterministic `searchPage` that parses
  the strict raw Google fixture through `parseGoogleSearchResponse`, and strict
  in-memory S3/SQS adapters. No browser fetch interception may answer or replace
  an application API response. The sole permitted CDP interception is a
  response-stage abort of the first handoff after the correlated backend trace
  and durable Run are observed, solely to create the ambiguous retry partition;
  it supplies no response bytes. The production `awsProbeSearchPage`
  transport/artifact wrapper is not invoked or claimed by this local substitute.
- **Maximum path:** create exactly five seeds. The keyword phase executes ten US
  expansion tasks, one 300-keyword US anchor task and eight 200-keyword market
  tasks: 19 first-pass provider calls, 19 attempt rows, exactly 23 immutable
  keyword objects and 42 base keyword queue sends in this no-retry maximum
  fixture, 300 candidates, 200 final rows and the locked `$0.49200000`
  reservation. Save exactly 100 recommended items, atomically create one Run
  plus 100 immutable RunQueries, edit/reorder but do not add/delete the queries,
  confirm them, perform exactly 100 Google probes returning ten distinct
  occurrences each, dispatch exactly 100 discovery tasks, and merge exactly
  1,000 distinct stable Shopify hosts into 1,000 run-specific domain/lead work
  entries. Stop at that established downstream lead-task boundary; W6 does not
  scrape or enrich the 1,000 leads.
- **Durability/security partitions:** the same causal run covers tab close and
  reopen during research, emitted Next restart, backend API restart, duplicate
  keyword and downstream messages, the same handoff request after an ambiguous
  response, owner-B/no-session denial, later research-selection mutation after
  handoff, strict corrupted-artifact rejection, and an all-S3/all-queue-empty but
  missing-Neon-terminal aggregation check. No cancellation behavior is added.
- **Executable case set:** the authoritative manifest contains exactly `3`
  `W6-NAV-*`, `13` `W6-FLOW-*`, `4` `W6-RES-*`, and `6` `W6-CONF-*` cases. The
  sorted-distinct-UTF-8-member-plus-LF group digests are respectively
  `103df26205674ddd7f4e7548b3432ea7f5342096bd369991e067debf7f3bf6f2`,
  `14aa36ae942fc9eedef7d9fae9ae0a42775f6ab22c04e3dabb2cf1cbe9379461`,
  `fc83e2c68fcd67e1849b955b3a9e48fe7a998aed1f1ac0ad6c0f943efeea354d`,
  and `b8180b2f2561d41298252db30b075d4184da3535af065a29f0273e12392c5646`.
  The global 26-ID digest is
  `d81bab26bc5aadd19c162156c13890611b2fc5a6d0dcb917234453d568ffb4d4`.
  Required, registered, executed and activated sets must be byte-equal, with
  zero skip, duplicate, unexpected, filtered or unactivated member.
- **Falsification:** `W6-NC-01`–`W6-NC-13` each operate on captured trace/data or
  an isolated synthetic discovered set: first the unchanged oracle passes, then
  exactly one defect is injected and that same oracle throws, then a fresh
  unchanged witness passes. Controls must cover API-URL navigation, auth bypass,
  an omitted expansion call, parser bypass, unfenced publication, split handoff,
  omitted Google probe, S3/queue completion, intercepted frontend data, each
  case-set defect, absent activation, divergent substitute, and an obsolete
  runtime member. No production/source mutation is a control.
- **Substitute limits:** the local auth server proves the installed client and
  owner/session consumption, not live auth/cookie cryptography; deterministic
  provider request substitutes prove exact keyword requests and Google
  validation/parser inputs, strict parsing and call counts; they do not prove
  the live Google request or `awsProbeSearchPage` artifact wrapper in the causal
  run. Those unchanged boundaries retain only their accepted focused evidence.
  The substitutes do not prove live pricing/quota/availability. Memory S3/SQS
  prove contract serialization, immutable-key/idempotency and service choreography,
  not AWS transport/IAM/DLQ/Lambda; isolated Postgres proves real Prisma SQL,
  transactions, ownership and restart durability only in one disposable schema;
  emitted Next plus local Chrome proves the production frontend artifact and
  real route/UI chain, not deployed networking. Accepted W3/R4 package/adaptor
  evidence is reused by exact unchanged-file proof and is not re-created.
- **Exact ownership:** W6 owns only the five paths and hashes/absence states in
  its A4 header. The sorted-member-plus-LF path digest is
  `d28ae17864073639580d7650bb03c03474d5370a5034b632cf412e1e3cf3d0bb`.
  No schema, migration, package, backend production source, route, auth, adapter,
  worker, queue, infrastructure or standalone KeywordSearchVolume file changes.
- **Recursive authority:** the parent assigns only one W6 window agent. That
  agent authors fresh coordination artifacts with the `REAUTHORED` names in A4,
  delegates sequential single-file leaves from the five-path set, independently
  reviews each leaf, and personally executes the final integration assessment.
  The state-108 W6 artifacts and their IDs are historical and cannot be reused,
  edited, cited as proof, or used as a baseline.
- **Frozen gates:** file-local diagnostics may run during leaves. After all
  implementation inputs freeze, run once: frontend `npm run check` (the sole
  build), the single emitted causal browser/isolated-schema gate using that
  build, backend `npm test`, backend secret scan, and final manifest/scope
  conformance. Do not run the full opted-in database suite, Prisma generation or
  validation, a handler build, the entire accepted W5 browser suite, provider or
  AWS operations. Only a relevant file change invalidates its named gate; proven
  sandbox/execution-channel failure permits one identical escalated recovery
  under the pinned standards and is not a product rerun.
- **Evidence:** `SRC-KI-038`–`040`; accepted `DEC-KI-024`, `034`–`037`; current
  source at backend `0083a42c…` and frontend `70fb5edf…`; installed Next route-
  handler/testing documentation.
- **Rejected:** changing the backend API `statusUrl`; adding an auth bypass or
  production test seam; browser fetch interception as end-to-end evidence;
  disconnected backend/UI tests relabelled E2E; a second database or browser
  build; processing 1,000 leads; wildcard source searches or test ownership;
  reuse of the invalidated decomposition.
- **Tasks/scenarios:** `KI-W6-T1`–`T5`; `SCN-KI-018`; all `W6-*` cases and
  `W6-NC-01`–`13`.

### `DEC-KI-039` — Final calculation is projected from the durable shortlist

- **Requirements:** `REQ-KI-002`, `REQ-KI-003`, `REQ-KI-023`,
  `REQ-KI-024`, `INV-KI-004`, `INV-KI-005`, `INV-KI-014`.
- **Locked choice:** the anchor stage continues to screen and persist all
  `1..300` US candidates. The market aggregator must additionally read the
  validated immutable `keyword-shortlist-manifest-v1` produced by the
  `anchor_screen` stage and must project both the per-seed expansion input and
  the reused US metrics to exactly that manifest's `1..200` keywords before
  calling `computeResearchResult`. The remaining eight market artifacts are
  already requested from that same shortlist. The published result therefore
  contains exactly the shortlist cardinality, at most `200`, while the default
  selection remains at most `100`.
- **Normalization/formula:** define
  `key(keyword)=keyword.trim().toLowerCase()`. Define `S` as the unique ordered
  `shortlistManifest.keywords` and `K={key(x)|x in S}`. For each expansion
  `bySeed` member, retain its original seed and original keyword order but keep
  only keywords whose key is in `K`; retain a keyword under every original seed
  that supplied it. Filter the US anchor metrics in original provider order by
  the same `K`. Before calculation, the distinct keys represented by the
  filtered expansion and the distinct keys represented by the filtered US
  metrics must each equal `K`; mismatch fails through the existing invariant/
  artifact-contract path and publishes nothing. Pass only the filtered
  expansion and filtered US metrics, plus the unchanged eight market metrics,
  to `computeResearchResult`.
- **Durability and operations:** the shortlist is reconstructed only from its
  existing fingerprint-validated S3 manifest through `readManifest`; no queue
  body, task request, array truncation, S3 listing, in-memory prior-stage value,
  or result post-truncation is authoritative. The change adds one validated S3
  read during market aggregation and adds no provider call, queue send,
  attempt, task, artifact write, database write, reservation, transaction, key,
  timestamp, retry, lease, or public interface.
- **Failure/replay/concurrency:** missing, corrupt, fingerprint-mismatched, or
  incomplete shortlist evidence fails before result/selection publication
  under the existing aggregation lease monitor. Duplicate/reordered aggregate
  checks and stale owners retain the existing fencing/idempotency behavior; an
  exact replay reads the same immutable shortlist and computes the same result
  fingerprint.
- **Rejected:** accepting 300 final rows; changing `shortlistLimit`; capping
  before the US overview; taking the first 200 expansion entries independently
  of the ranked manifest; truncating `result.keywords` after calculation;
  collapsing all shortlist keywords onto one seed; mutating any accepted
  artifact; or changing provider economics.
- **Evidence:** `SRC-KI-030`, `SRC-KI-041`; A1 `REQ-KI-024`; `DEC-KI-006`,
  `DEC-KI-024`, `DEC-KI-038`.
- **Tasks/scenarios:** `KI-W6-CT1`, `KI-W6-CT2`; `SCN-KI-041`;
  existing `W6-FLOW-04`, `W6-FLOW-05`, `W6-FLOW-06`, and `W6-NC-05`.

### `DEC-KI-040` — Maximum component fixture preserves stage identity and per-seed bounds

- **Requirements:** `REQ-KI-001`, `REQ-KI-002`, `REQ-KI-003`, `REQ-KI-023`,
  `REQ-KI-024`, `INV-KI-004`, `INV-KI-005`, `INV-KI-014`; correction evidence
  `SRC-KI-042`.
- **Locked choice:** production contracts and C104 remain unchanged. The
  component scaffold must store `keyword-shortlist-manifest-v1` with the exact
  anchor-stage fingerprint
  `keywordStageInputFingerprint({researchId,generation,stage:"anchor_screen",tasks:[anchorTask]})`
  in both the manifest header and `putImmutable.inputFingerprint`. A task
  fingerprint is never a stage-manifest identity.
- **Maximum fixture:** SCN-KI-041 uses exactly five ordered seeds named
  `seed 1` through `seed 5`. Each `bySeed` member contains exactly 60 ordered,
  unique strings: its seed itself followed by 59 strings
  `<seed> candidate <NN>` where `NN` is `01` through `59`. Flattening the five
  members in seed/order produces exactly 300 distinct candidates. The durable
  shortlist is exactly `candidates.slice(0,200)`.
- **Scaffold parity:** its private seed-aware option defaults to the existing
  one-seed three-candidate behavior. Under the five-seed fixture it constructs
  ten ordered expansion tasks (suggestions then related for each seed), stage
  counters equal ten, preserves each candidate's exact supplying-seed list in
  the expansion manifest, and changes no production/exported interface.
- **Acceptance:** the complete non-database worker-flow file must pass, including
  R3-G11–G15 and SCN-KI-041's exact 5/60/300/200/200/100 witnesses. The earlier
  30-pass/7-fail CV1 is diagnostic and superseded only by a fresh complete pass.
- **Rejected:** raising/removing the 60-per-seed schema bound; one seed with 300
  keywords; changing C104 to expect a task fingerprint; weakening `readManifest`;
  changing product source, case IDs, manifest membership, provider economics,
  or the causal V3 oracle.
- **Tasks/scenarios:** `KI-W6-CT3`; corrected `SCN-KI-041`; existing
  `W6-FLOW-04/05/06` and `W6-NC-05`; `KI-W6-CV7`–`CV12`.

### `DEC-KI-041` — Selection swap traverses the real paginated table

- **Requirements:** `REQ-KI-007`, `REQ-KI-008`, `REQ-KI-009`,
  `REQ-KI-014`, `REQ-KI-015`, `INV-KI-010`; correction evidence
  `SRC-KI-043`.
- **Locked choice:** preserve the production dashboard and the existing
  200-row/default-100 selection contract. Correct only
  `swapOneSelectionItemViaUi` in the causal browser harness. Starting at the
  freshly mounted page 1, it must inventory successive real table pages until
  it records one checked row and one differently labelled unchecked row plus
  each row's page number. It then navigates to the checked row, removes it,
  navigates to the recorded unchecked row, adds it, and waits until the
  selection-review surface reports exactly `100 of 200 selected`.
- **Exact traversal:** the checkbox selector remains
  `[data-surface="surface:keyword-table"] tbody tr input[type=checkbox][aria-label^="Select"]`.
  Scan page 1 before advancing. At most eight pages may be inventoried because
  the frozen result is 200 rows and the unchanged default page size is 25.
  Every `Next` or `Prev` navigation captures the ordered newline-joined
  checkbox-label signature before the click, requires an enabled
  keyword-table button with that exact trimmed text, clicks it, and waits for
  the signature to change. Track the current page locally from 1; do not infer
  it from a CSS-module class. Stop inventory once both distinct rows exist.
  Move to each recorded page using the direction implied by the integer page
  difference. The complete helper permits at most 21 pagination clicks
  (seven inventory, seven repositioning, seven between rows). Missing either
  state by page 8, a repeated label, an unavailable required direction, or an
  unchanged signature fails closed. Do not select before removing: the
  100-item cap would correctly reject that attempted addition.
- **Mutation semantics:** perform exactly two checkbox changes per helper
  invocation—one checked→unchecked removal and one different
  unchecked→checked addition. Do not use fetch, direct React state, DOM property
  assignment, test-only product hooks, filters, row text as an item identity,
  or a fabricated selection. The existing save request, numeric-revision CAS,
  strict minimal payload, 100-item assertion, stale-conflict path and immutable
  handoff assertions remain unchanged.
- **Acceptance/invalidation:** this changes no W6 case/control membership or
  digest. It supersedes only the accepted S105 helper implementation and the
  failed R33 CV9 result. A fresh emitted-browser/isolated-schema run must execute
  the unchanged 26 cases and 13 controls and prove both helper invocations,
  including `W6-FLOW-07` and the post-handoff `W6-FLOW-13` selection mutation.
  C106/CV7 and the clean committed frontend build/CV8 remain valid; the test
  file is not a Next build input. CV10–CV12 remain pending and run only after
  the fresh causal gate passes.
- **Rejected:** changing pagination or selection product code; requiring both
  states on one page; increasing page size; changing default selection rank or
  count; using the removed row as the addition; weakening the exact saved-100
  or case/control certificate; adding a case ID; rebuilding unchanged Next
  output; or relabelling R33 as an environment failure.
- **Tasks/scenarios:** `KI-W6-CT4`; existing `W6-FLOW-07`, `W6-FLOW-13`,
  `W6-NC-06`; `KI-W6-CV13`–`CV18`.

### `DEC-KI-042` — Final research publication has a publication-only 30-second transaction ceiling

- **Requirements:** `REQ-KI-002`, `REQ-KI-005`, `REQ-KI-024`;
  `INV-KI-004`, `INV-KI-005`, `INV-KI-006`, `INV-KI-014`; correction
  evidence `SRC-KI-044`.
- **Locked choice:** preserve one atomic, generation/token/lease-fenced
  `publishResearchResult()` transaction. Extend the private `_transaction`
  seam to accept an optional Prisma interactive-transaction options object,
  preserving the current one-argument call for every other repository
  operation. Only `publishResearchResult()` supplies
  `{maxWait:5_000, timeout:30_000}`. Both values are private fixed constants;
  neither is configurable or exported.
- **Bound derivation:** the aggregation owner renews immediately before final
  publication to `now + 120_000 ms`, then stops the 40,000 ms heartbeat. A
  maximum 5,000 ms acquisition wait plus 30,000 ms transaction ceiling remains
  strictly below the renewed lease duration. The 30,000 ms value is a rollback
  safety deadline for the existing maximum 200-row result/default-100 write,
  not permission for provider/network work inside the transaction, a changed
  lease, a retry, or a relaxed performance claim.
- **Atomic ordering:** retain the existing ordered reads and predicates;
  conditionally complete the market stage first, then conditionally complete
  research with result, fingerprint, default selection and revision one in the
  same transaction. Any expiry/error after the stage write rolls back every
  member. `FinalPublicationAbort` mappings, completed replay, stale-token loss,
  visibility and immutable result semantics remain unchanged.
- **Deterministic proof:** one permanent isolated-database scenario uses the
  real repository and maximum 200-row/default-100 payload. Its transaction
  proxy must first observe the production request options exactly. For
  `W6-TXN-01`/`W6-NC-14`, it substitutes only the test transaction timeout with
  20,000 ms and injects one literal `SELECT pg_sleep(21.000)` immediately before the
  first final `keywordResearch.updateMany`, after the market-stage update; the
  expected Prisma `P2028`/closed-transaction failure must leave the complete
  research and market-stage rows deep-equal to their pre-call snapshots. For
  `W6-TXN-02`, the same 21,000 ms delay with the unmodified production options
  must publish exactly 200 result rows/default 100, complete both rows once,
  and return `found` on exact replay. Existing stale-owner publication proof is
  rerun in the same focused gate.
- **Coverage:** the existing emitted-browser manifest remains exactly 26 cases
  and thirteen controls. The separate transaction registry is exactly
  `W6-TXN-01`, `W6-TXN-02`, digest
  `dd72e2292dac7c33d2250be7af0770401bde67695176d1b76c530b9c7bc10d39`,
  with control `W6-NC-14`. I105 merges the two registries to 28 cases, digest
  `c1e4d65b0df7fd1fd86f71420e4ba5e9c6d12cc72b3f24885c71d5283dcf5c75`,
  and fourteen controls, digest
  `4f2c8489518c5845c52e9336a47f5cc0b90dcdd9dfa70db7614814d87c173af6`.
- **Substitute fidelity:** overriding the timeout and injecting `pg_sleep` is
  an isolated negative-control seam proving rollback and option propagation;
  it does not prove normal production latency. The positive uses the real
  Prisma transaction and real isolated Postgres with only the fixed delay; the
  subsequent causal emitted-browser run exercises the unmodified production
  client and supplies local-E2E parity.
- **Rejected:** a global timeout increase; changing the lease/heartbeat;
  retrying publication inside the repository; moving writes outside the
  transaction; chunk/partial publication; changing result/selection bounds;
  relying on naturally slow infrastructure; weakening CV15; another browser,
  schema, provider, AWS or production change.
- **Tasks/scenarios:** `KI-W6-CT5`, `KI-W6-CT6`; `SCN-KI-042`;
  `W6-TXN-01/02`, `W6-NC-14`; `KI-W6-CV19`–`CV24`.

### `DEC-KI-043` — The deterministic sleep probe returns a Prisma-supported column

- **Requirements:** unchanged `REQ-KI-002`, `REQ-KI-005`, `REQ-KI-024` and
  `INV-KI-004`, `INV-KI-005`, `INV-KI-006`, `INV-KI-014`; evidence
  `SRC-KI-045`.
- **Locked correction:** in `withPublicationTransactionProbe`, replace only
  `$queryRawUnsafe("SELECT pg_sleep(21.000)")` with
  `$queryRawUnsafe("SELECT ''::text AS slept FROM pg_sleep(21.000)")`.
  PostgreSQL still executes the same 21-second sleep at the same first final
  result-bearing `keywordResearch.updateMany` boundary, but Prisma receives one
  supported text column rather than an unsupported `void` column.
- **Preserved behavior:** the 20,000 ms negative timeout, production
  5,000/30,000 ms options, transaction wrapper/restoration, post-stage-write
  injection point, P2028 rollback oracle, 200/default-100 positive publication,
  exact replay, case/control membership and every digest remain unchanged.
- **Invalidation:** the state-159 `3/1` result is diagnostic and invalidates
  only the old probe expression and CV21. C108 production evidence, C109's other
  assertions, CV19/CV20 and the three passing focused cases remain valid. A
  fresh complete focused gate and causal emitted-browser gate remain mandatory.
- **Rejected:** changing the delay, timeout, production source, transaction
  boundary, registry, case IDs, database helper, fixture or acceptance count;
  relabelling P2010 as a production failure; accepting partial prior output.
- **Tasks/scenarios:** `KI-W6-CT7` / `KI-W6-C110`; unchanged `SCN-KI-042`,
  `W6-TXN-01/02`, `W6-NC-14`; `KI-W6-I106`.

### `DEC-KI-044` — The causal revision advance consumes the serialized selection array

- **Requirements:** `REQ-KI-007`, `REQ-KI-008`, `REQ-KI-009`,
  `REQ-KI-014`, `REQ-KI-015`; `INV-KI-010`; evidence `SRC-KI-046`.
- **Locked correction:** in the one browser-evaluated revision-advance script,
  replace exactly
  `const items = (research.selection && research.selection.items) || [];` with
  `const items = Array.isArray(research.selection) ? research.selection : [];`.
  This consumes the already-locked numeric-v1 API representation and rejects a
  non-array substitute by producing the existing empty-list fail-closed path.
- **Preserved behavior:** retain the 100-item precondition, mutate only item 99's
  keyword with the existing ` curated` suffix, PUT the same minimal mutation at
  the same expected revision, cause exactly one stale 409 in the open page,
  reload, then exercise C107's page-aware checked/unchecked swap and final
  100-item CAS. No API, component, selection, case/control or digest changes.
- **Invalidation:** CV26 remains accepted because a browser-test-only hunk cannot
  affect repository.js or the integration test. CV27 is invalid and must run
  once fresh; its complete cleanup remains diagnostic evidence.
- **Rejected:** accepting zero items, reading an `.items` alias, changing the
  serializer, product UI, default selection, page size, pagination helper,
  selection cap, revision sequence, cases, controls or build inputs.
- **Tasks/scenarios:** `KI-W6-CT8` / `KI-W6-C111`; existing `W6-FLOW-07`,
  `W6-FLOW-13`, `W6-NC-06`; `KI-W6-I107`.

### `DEC-KI-045` — KI repository set-based transaction policy and bounded recovery

- **Requirements:** `REQ-KI-002`, `REQ-KI-005`, `REQ-KI-022`,
  `REQ-KI-024`; `INV-KI-004`, `INV-KI-005`, `INV-KI-006`,
  `INV-KI-014`; evidence `SRC-KI-047` and `EV-KI-A-101`.
- **Scope:** this decision applies only to the new Keyword Intelligence
  repository and recovery caller. The established discovery, lead, traffic,
  CrUX and final-publication repositories remain byte-read-only. There is no
  schema, migration, payload, provider, queue, artifact, cost, lease-duration,
  retry, result, selection, frontend or AWS behavior change.
- **Boundary rule:** preserve separate durable boundaries for task claim,
  cache/throttle/reservation, paid HTTP, attempt settlement, immutable S3 put,
  task terminalization and aggregation publication. No provider, S3 or SQS
  operation may enter a database transaction. Database-only reads and writes
  inside one existing logical transition may be joined, returned from the
  conditional write, or set-loaded without changing its return union,
  idempotency, fencing, rollback or visibility semantics.
- **Complete transaction-policy set:** all 18 `_transaction` invocations pass
  one explicit frozen options object and no implicit-options branch remains.
  `maxWait` is `5_000` ms for both profiles. The short constant-count profile
  has `timeout:15_000`; it is used exactly by `claim`, `deferTask`,
  `scheduleRetry`, `claimAggregator`, `failStage`, `saveSelection`, the
  `createRun` uniqueness-reconciliation transaction and `claimThrottle`. The
  scale-bearing profile has `timeout:30_000`; it is used exactly by
  `initialize`, `recordAttempt`, `settleAttempt`, `markAttemptAmbiguous`,
  `terminalize`, `publishCandidateManifest`, `publishShortlist`,
  `publishResearchResult`, the initial `createRun` transaction and `recover`.
  Acquisition plus transaction ceilings are respectively 20 seconds and 35
  seconds, strictly below the 60-second task and 120-second aggregation leases.
  These are rollback safety ceilings, not performance targets or retry
  authority.
- **Repository consolidation:** use one relation-bearing read wherever the
  same immutable graph was previously loaded separately: task plus stage plus
  research plus latest attempt; stage plus research plus ordered tasks; attempt
  plus task; and handoff plus run. Use `updateManyAndReturn` for conditional
  task/stage updates whose row was immediately reread, require exactly one
  returned row, and use that returned row. Use `createManyAndReturn` for new
  stage tasks, sort returned rows by unsigned UTF-8 `itemKey`, and remove the
  post-create task reload. `recordAttempt` retains one research-wide exposure
  aggregate and atomic attempt/task writes; `settleAttempt` retains immutable
  cache conflict detection and atomic cost/cache settlement; `terminalize`
  retains the live token/expiry predicate and exact once-only stage counters.
  Final publication keeps the already-proven 30-second profile and all-or-none
  stage/research writes. Run handoff keeps one `Run`, one `createMany` of at
  most 100 `RunQuery` rows and one handoff row in the same transaction.
- **Throttle:** replace the update/insert/select sequence with one
  schema-selected SQL statement composed of data-modifying CTEs. It returns
  exactly one row tagged `claimed` with the newly reserved `nextAllowedAt`, or
  `delayed` with the existing future value. The two-second provider gap,
  database clock authority and no-attempt-on-delay behavior are unchanged.
- **Recovery interface and bound:** repository signature becomes exactly
  `recover(now, {limit})`; `limit` is required integer `1..100`.
  `recoverKeywordWork({now,limit=100},runtime)` passes that exact value and
  rejects any repository result whose three list lengths sum above `limit`
  before dispatch. The repository performs exactly three bounded set reads,
  each with `take:limit`: queued initializations; due/expired tasks including
  stage; ready/expired aggregation stages including ordered tasks. Candidate
  eligibility time is research `createdAt`; pending-task
  `nextAttemptAt ?? updatedAt`; processing-task `leaseExpiresAt`; ready-stage
  `updatedAt`; aggregating-stage `aggregationLeaseExpiresAt`. Sort candidates
  by ascending eligibility time, then type rank `task=0`, `stage=1`,
  `initialization=2`, then unsigned UTF-8 candidate ID; return the first
  `limit`. Duplicate delivery remains harmless through existing claims and
  fences. No cursor, durable recovery marker or deletion is introduced.
- **Operation ceilings:** after correction, `getTaskContext` and
  `getStageContext` each issue one Prisma delegate operation; `claim` at most
  two; `recordAttempt` at most four; `settleAttempt` at most four;
  `deferTask` and `scheduleRetry` at most two each; `terminalize` at most four;
  `claimAggregator` at most two; each stage publication at most four on its
  mutation branch; `claimThrottle` exactly one SQL statement; and recovery
  exactly three bounded delegate reads with at most 300 inspected top-level
  candidates and at most 100 returned/dispatchable members. No database call
  is permitted inside an input/task/result classification loop.
- **Enforcement:** `SCN-KI-043` owns cases `W6-DB-01`–`W6-DB-07`, sorted-LF
  digest `073c0fa52135c9a271eea75264efc79fd6ebcb8d062ec73175dbb58a5333aa8f`,
  and controls `W6-NC-15`–`W6-NC-17`, digest
  `86562d5c606dc8867b40ecd46b6604e2f5a66a2553c41a20a23696cb48cdbec0`.
  Acceptance fails when one transaction lacks its exact profile, one removed
  redundant operation returns, or recovery returns/dispatches member 101.
  Existing attempt replay, settlement rollback, exact-expiry ownership,
  publication rollback, 100-item handoff and causal 26-case browser evidence
  remain required.
- **Alternatives rejected:** a repository-global implicit 30-second default;
  changing the established pipeline; combining paid HTTP/S3/SQS with database
  work; batching distinct provider task identities into one ledger row;
  changing the evidenced `$0.49200000` maximum; unbounded recovery; raising
  Lambda/lease/queue limits; retrying timed-out transactions automatically; or
  accepting elapsed-time success without operation-count enforcement.
- **Tasks/scenarios:** `KI-W6-CT9`–`CT13`, corrections `KI-W6-C112`–`C116`,
  `SCN-KI-043`, and parent assessment `KI-W6-I108`.

### `DEC-KI-046` — The causal final-CAS witness is partitioned by expected revision

- **Requirements:** `REQ-KI-007`, `REQ-KI-008`, `REQ-KI-009`,
  `REQ-KI-014`, `REQ-KI-015`; `INV-KI-010`; evidence `SRC-KI-048` and
  `EV-KI-W6-R52`.
- **Locked correction:** preserve both successful selection mutations and
  distinguish their roles from their already-captured strict request bodies.
  At the existing final-save assertion in
  `frontend/test/browser/keyword-intelligence-e2e.mjs`, first collect
  `successfulSelectionEntries` using the existing method, URL suffix and HTTP
  200 predicates. Require its length to equal exactly two. From that array,
  collect `advanceEntries` where
  `entry.requestBody?.expectedRevision === 1` and require exactly one; collect
  `savedEntries` where `entry.requestBody?.expectedRevision === 2` and require
  exactly one. Continue to derive `savedBody` only from `savedEntries[0]`.
  The prior unpartitioned `savedEntries` filter and its incorrect length-one
  assertion are removed.
- **Oracle:** the complete selection witness is exactly revision `1 -> 2` by
  the deliberate harness advance, one stale UI request returning 409, then
  revision `2 -> 3` by one successful UI final CAS. Before finalization there
  are exactly two successful selection PUTs total, exactly one request in each
  expected-revision partition, the final partition carries exactly 100 items,
  and durable revision is exactly three. Any missing, duplicate, additional,
  mis-revisioned or wrongly selected successful request fails.
- **Preserved behavior and evidence:** retain C107's page-aware two-checkbox
  swap, C111's `Array.isArray(research.selection)` consumer, the accumulated
  navigation-persistent netlog, the exact stale-409 assertion, final 100-item
  payload assertion, durable revision-three assertion, handoff, post-handoff
  mutation, 26 browser cases, 13 browser controls, every case/control digest,
  provider-substitute counts, cleanup and substitute-fidelity limits. This is
  an accepted-test oracle correction only; no product source, API, database,
  provider, cost, queue, artifact, schema, build input or public behavior
  changes.
- **Invalidation:** failed I109/CV39 remains diagnostic. C112–C117 and I109
  CV36–CV38 remain accepted/reusable by exact dependency proof because C118
  changes only the browser test. The earlier C111 whole-file digest is
  superseded by C118, but its one-expression behavior must remain present and
  is rechecked. CV39 and every later pending final gate require a fresh
  assessment after C118; no prior failed browser attempt is acceptance.
- **Enforcement:** existing `W6-FLOW-07` is the sole case registration and
  existing `W6-NC-06` remains its falsification control; neither membership nor
  digest changes. The already-observed unpartitioned filter is the decisive
  counterexample: with the required advance and final saves it selects two and
  fails. Local source inspection must prove the exact total and revision
  partitions; the fresh causal browser gate must execute the production route,
  UI save, durable CAS and complete unchanged certificate.
- **Alternatives rejected:** deleting the deliberate advance; expecting only
  one successful selection PUT in the accumulated log; clearing or truncating
  the netlog; selecting the last entry by position alone; weakening the count
  to `>=1`; ignoring extra successes; changing the API/UI/repository CAS;
  changing revisions, item count, cases, controls, digests or the browser
  command.
- **Tasks/scenarios:** `KI-W6-CT14` / `KI-W6-C118`; existing
  `SCN-KI-018`, `W6-FLOW-07`, `W6-FLOW-13`, `W6-NC-06`; assessment
  `KI-W6-I110`.

### `DEC-KI-047` — Protected run-workspace proof uses the installed middleware with an opaque local session token

- **Requirements:** `REQ-KI-002`, `REQ-KI-015`, `REQ-KI-016`,
  `REQ-KI-017`; `INV-KI-010`, `INV-KI-011`; evidence `SRC-KI-049` and
  `EV-KI-W6-R54`.
- **Locked boundary:** production `frontend/proxy.ts`, `getAuth()`, the
  `/runs/:path*` matcher, `/sign-in`, application auth routes, and Neon Auth
  package code are read-only. The local W6 substitute uses the installed
  `@neondatabase/auth@0.4.2-beta` middleware exactly as shipped. It supplies
  only the two inputs that the prior harness omitted: one opaque browser
  `__Secure-neon-auth.session_token` cookie and one complete deterministic
  `/get-session` session+user envelope. The SDK, not test code, performs any
  session-data cache signing and the protected-route decision.
- **Harness session contract:** in
  `email_scraper/test/helpers/keyword-intelligence-e2e-harness.js`, define the
  exact constants
  `NEON_AUTH_SESSION_COOKIE_NAME="__Secure-neon-auth.session_token"`,
  `NEON_AUTH_SESSION_COOKIE_VALUE="kiw6-local-session-token"`,
  `AUTH_SESSION_CREATED_AT="2026-08-21T00:00:00.000Z"`, and
  `AUTH_SESSION_EXPIRES_AT="2099-01-01T00:00:00.000Z"`. For authenticated
  `authMode`, `/get-session` returns exactly
  `{session:{id:"kiw6-session-"+authMode,userId,token:NEON_AUTH_SESSION_COOKIE_VALUE,expiresAt:AUTH_SESSION_EXPIRES_AT,createdAt:AUTH_SESSION_CREATED_AT,updatedAt:AUTH_SESSION_CREATED_AT},user:{id:userId,name:authMode==="owner-a"?"KIW6 Owner A":"KIW6 Owner B",email:authMode+"@kiw6.invalid",emailVerified:true,createdAt:AUTH_SESSION_CREATED_AT,updatedAt:AUTH_SESSION_CREATED_AT}}`;
  `userId` is the existing owner selected by `authMode`. Mode `none` still
  returns JSON `null`. The response status/content type, auth trace event,
  `setAuthOwner` semantics and all other helper behavior stay unchanged.
  Export one frozen test seam named `browserSessionCookie` with exactly
  `{name:NEON_AUTH_SESSION_COOKIE_NAME,value:NEON_AUTH_SESSION_COOKIE_VALUE}`
  in the existing frozen harness result.
- **Browser installation:** in
  `frontend/test/browser/keyword-intelligence-e2e.mjs`, immediately after the
  existing `W6-FLOW-07` activation and before
  `const abortDone = armRunsResponseAbort()`, capture
  `sessionAuthFloor = harness.trace().length` and call `Network.setCookie` once with
  `{name:harness.browserSessionCookie.name,value:harness.browserSessionCookie.value,url:baseUrl,path:"/",secure:true,httpOnly:true,sameSite:"Lax"}`.
  Require its returned `success` to equal `true`; call `Network.getCookies`
  once for `[baseUrl]` and require exactly one cookie whose name equals the
  seam name and whose `secure` and `httpOnly` fields are both `true`. Never
  compare, emit or record the token value. Keep the cookie installed through
  the last owner-A `/runs/<id>` reload and immutable-snapshot witness. Before
  the existing `harness.setAuthOwner(harness.otherOwnerId)` call, call
  `Network.getCookies` for `[baseUrl]`, select cookies whose names start with
  `"__Secure-neon-auth."`, require their sorted names to equal exactly
  `["__Secure-neon-auth.local.session_data","__Secure-neon-auth.session_token"]`,
  delete each selected cookie with one `Network.deleteCookies` call using only
  `{name:cookie.name,url:baseUrl}`, then call `Network.getCookies` once more
  and require zero cookie name with that prefix. This prevents the SDK's
  owner-A session-data cache from masking the later owner-B/null partitions.
  Mode `none` must still yield the existing 401/API denial and protected-route
  denial.
- **Substitute ledger:** replace only the authentication entry with:
  `actual: "installed Neon Auth server client and /runs middleware against deterministic loopback /get-session, with one CDP-seeded opaque local session token"`;
  `mayProve: "actual auth-client and middleware calls, protected-workspace routing, cookie transport, and owner propagation/denial branches"`;
  `mustNotClaim: "live Neon Auth availability, external token issuance or validation, credential verification, cookie-cryptography assurance, or external session security"`.
  No other substitute claim changes.
- **Oracle:** after the same successful handoff retry, the client-generated
  navigation reaches exactly `/runs/<encoded runId>` through the real Next
  proxy, the document never visits `/sign-in`, the existing workspace loads
  exactly 100 query inputs, and the existing owner/restart/snapshot checks
  pass. At least one `auth` trace at or after `sessionAuthFloor` with
  `op:"get-session"`, mode `owner-a`, and status 200 exists before workspace
  readiness. The trace and
  browser diagnostics contain neither cookie value nor Cookie/Set-Cookie
  header. The SDK-created session-data cookie and seeded token both exist
  through the last owner-A protected reload, then both are absent before the
  owner-B/null partitions. Removing the browser token, returning the old
  user-only envelope, leaving either Neon cookie across the owner switch,
  returning `null`, or changing the expected route must make the existing
  navigation/auth assertions fail.
- **Coverage and invalidation:** existing `W6-NAV-01`, `W6-FLOW-01`,
  `W6-RES-01`, `W6-NC-02`, and `W6-NC-12` own this strengthened witness. No
  case/control/manifest/digest changes. C118 and I110 CV44 plus the CV45
  backend reuse proof remain accepted. The failed fresh CV45 run remains
  diagnostic. A new assessment must run the causal browser gate and every
  still-pending final gate; prior browser output is not acceptance.
- **Alternatives rejected:** weakening/removing the `/runs` proxy; bypassing
  middleware for tests; navigating to the JSON `statusUrl`; manually minting
  the SDK's private signed session-data JWT; implementing a fake email sign-in
  protocol; changing application auth routes; treating `/sign-in` as success;
  logging the token; or claiming live/external authentication.
- **Tasks/scenarios:** `KI-W6-CT15` / `KI-W6-C119`, then `KI-W6-CT16` /
  `KI-W6-C120`; existing `SCN-KI-018`, `W6-NAV-01`, `W6-FLOW-01`,
  `W6-RES-01`, `W6-NC-02`, `W6-NC-12`; assessment `KI-W6-I111`.

### `DEC-KI-048` — Workspace lineage preserves identity while edit provenance changes exactly

- **Requirements:** `REQ-KI-010`–`REQ-KI-015`; `INV-KI-010/015`; evidence
  `SRC-KI-050` and `EV-KI-W6-R57`.
- **Locked interpretation:** selection-item/RunQuery identity, query source and
  query text are distinct fields. `INV-KI-015` requires the same 100 durable
  RunQuery identities to survive text edits; it does not require the mutable
  `source` provenance label to remain `generated`. The accepted handoff creates
  all 100 rows with `source="generated"`. Editing every row through the real
  `QueryEditor` must change every displayed badge to `user edited`; the first
  two badges must follow the same persisted first-row swap as their query rows.
- **Exact C121 oracle:** in
  `frontend/test/browser/keyword-intelligence-e2e.mjs`, after loading
  `beforeBadges`, require exactly 100 members and require every member to equal
  `"generated"`. After the existing edit/save/reload, construct
  `expectedEditedBadges = beforeBadges.map((badge) => badge === "generated" ?
  "user edited" : badge)` and
  `swappedExpectedBadges = [expectedEditedBadges[1],
  expectedEditedBadges[0], ...expectedEditedBadges.slice(2)]`. Require
  `arrayEqual(afterBadges, swappedExpectedBadges)`. Retain the existing exact
  100-row count, all-text-edited, swapped-order, persistence and zero-add/delete
  assertions. Replace only `captured.workspace.badgesPreserved:true` with
  `captured.workspace.provenanceTransitionVerified:true`; retain its other
  members and the existing `W6-FLOW-09` activation literal.
- **Enforcement:** the pre-edit all-generated assertion makes the transition
  non-vacuous. The order-sensitive equality fails for an unchanged generated
  label, a missing or extra badge, a wrong label, a label detached from the
  swapped row, or a product regression that no longer persists edit provenance.
  A file-local negative control must feed an unchanged generated badge into the
  frozen projection and prove the equality throws before the fresh causal gate.
  Existing `W6-FLOW-09` remains the sole case registration and `W6-NC-06`
  remains its row-identity/add-delete falsification control; no manifest,
  registry, case/control membership or digest changes.
- **Invalidation and reuse:** failed I111 CV53 remains diagnostic. C119 and its
  CV50 proof are unchanged. C120's auth behavior is retained, but its prior
  whole-file ending digest and CV51 source review are superseded by C121; the
  new review must prove every C120 cookie/auth marker remains byte-present
  outside the one C121 hunk. I111 CV52 backend reuse remains valid only after
  the same five backend files are rehashed byte-equal. CV54–CV57 were never run.
- **Alternatives rejected:** preserving the pre-edit badge multiset; removing
  badge coverage; checking only sorted counts; accepting either generated or
  user edited; changing QueryEditor, QuerySource, RunQuery creation, product
  persistence, case/control membership, or the browser command.
- **Tasks/scenarios:** `KI-W6-CT17` / `KI-W6-C121`; existing
  `SCN-KI-018`, `W6-FLOW-09`, `W6-FLOW-13`, `W6-NC-06`; assessment
  `KI-W6-I112`.

### `DEC-KI-049` — Flush exactly the parked run-start callback before confirmation accounting

- **Requirements:** `REQ-KI-010`–`REQ-KI-015`; `INV-KI-010/015`; evidence
  `SRC-KI-051` and `EV-KI-W6-R59`.
- **Locked correction boundary:** this is a local causal-harness orchestration
  defect, not a product scheduler, validation, queue, database or provider
  defect. Preserve `src/server.js`, its injected `schedule` contract, the
  manual scheduler, the inert interval substitute, `drainDownstream`, every
  discovery/domain fault-injection location and the existing 26-case/13-control
  browser registry. Correct it with two sequential single-file leaves only:
  `KI-W6-C122` owns the backend harness export and `KI-W6-C123` owns the browser
  invocation.
- **Exact C122 interface and behavior:** in
  `email_scraper/test/helpers/keyword-intelligence-e2e-harness.js`, add the
  synchronous private callable
  `flushRunStartSchedule(): Readonly<{pendingBefore:number,
  flushedCallbacks:1,pendingAfter:number}>` immediately after the unchanged
  `flushSchedule`. It reads `scheduledCallbacks.length` and throws
  `HarnessPreflightError("expected exactly one parked run-start callback, saw
  <n>")` unless it equals one; removes that sole callback with `shift()`;
  invokes it exactly once; rereads the length and throws
  `HarnessPreflightError("run-start flush left <n> parked callbacks")` unless
  it equals zero; freezes the exact witness
  `{pendingBefore,flushedCallbacks:1,pendingAfter}`; records exactly one safe
  event `{kind:"harness",op:"flush-run-start-schedule",at:nowMs(),...witness}`;
  and returns the witness. Export that callable in the existing frozen harness
  object immediately between `restartBackend` and `drainDownstream`. Do not
  change `flushSchedule`, `schedule`, timers, queue processing or production
  source.
- **Exact C123 caller/order:** in
  `frontend/test/browser/keyword-intelligence-e2e.mjs`, preserve the existing
  click and observed POST `/api/runs/${runId}/start`. Immediately after
  `const googlePairsFloor = harness.trace().length;` and before constructing
  `confirmDeadline`, invoke `const runStartSchedule =
  harness.flushRunStartSchedule();`; require, in order, `pendingBefore===1`,
  `flushedCallbacks===1`, and `pendingAfter===0` with message `run start must
  flush exactly one parked queue-drain callback`; then store
  `captured.confirmationDrain = structuredClone(runStartSchedule)`. Preserve
  the following waits and exact W6-FLOW-10/11/12 assertions. The Google floor
  is deliberately captured before the flush so no validator event can escape
  accounting.
- **Failure/enforcement semantics:** zero or multiple parked callbacks fail
  before the browser may claim confirmation; a callback that is not invoked,
  invokes twice, remains queued, is invoked before the start witness, or is
  invoked after the Google floor/deadline boundary fails the local structural
  oracle or the causal browser gate. The existing W6-FLOW-10 activation proves
  100 actual validator/parser calls and `W6-NC-07` falsifies a missing member;
  W6-FLOW-11/12 and W6-NC-08 continue proving downstream dispatch and Neon
  completion. No new case/control ID or digest is introduced.
- **Invalidation and reuse:** accepted C121 remains the browser baseline at
  SHA-256 `8d89bb198390c3f7baf431ccd3405693c5003eb8a9ee4f0e7ccd75c254d507d0`.
  C119's helper behavior remains accepted, but its helper whole-file digest is
  superseded by C122 and every auth/cookie/session marker must be revalidated.
  I112 CV58 and its C121/C120 source-preservation proof remain reusable only
  after the exact baseline checks; failed CV59 remains diagnostic. CV60-CV63
  never ran and must execute after the fresh causal pass.
- **Alternatives rejected:** real timers; changing production `queueDrain` or
  `schedule`; broadening `flushSchedule`; invoking `drainDownstream` before
  confirmation; relocating discovery/domain fault injections; sleeping longer;
  accepting zero calls; bypassing the real validator/parser; or changing the
  browser command, registries, cases, controls, manifests or digests.
- **Tasks/scenarios:** `KI-W6-CT18` / `KI-W6-C122`, then `KI-W6-CT19` /
  `KI-W6-C123`; existing `SCN-KI-018`, `W6-FLOW-10`–`12`, `W6-NC-07/08`;
  assessment `KI-W6-I113`.

### `DEC-KI-050` — Discard the closed-server callback and invoke only the live-server callback

- **Requirements:** `REQ-KI-010`–`REQ-KI-015`; `INV-KI-010/015`; evidence
  `SRC-KI-052` and `EV-KI-W6-R60`–`R63`. This supersedes only DEC-KI-049's
  one-callback cardinality and witness; the accepted seam, caller boundary and
  every product/downstream constraint remain unchanged.
- **Exact scheduler state:** at the confirmation boundary the shared FIFO
  `scheduledCallbacks` array must contain exactly two members. Index zero is
  the construction callback captured by closed server A before W6-RES-01;
  index one is the construction callback captured by current live server B.
  Server B's start request sets its existing `drainRequested` flag but cannot
  append a third callback while `drainScheduled` is true.
- **Exact parent-direct correction:** the requester authorizes the parent to
  modify only the accepted C122/C123 files. In `flushRunStartSchedule`, require
  `pendingBefore===2`; remove the live callback with `pop()`; set
  `discardedStaleCallbacks` to the remaining length; clear the array; invoke
  the live callback exactly once; require `pendingAfter===0`; and freeze/record
  exactly `{pendingBefore,discardedStaleCallbacks,flushedCallbacks:1,
  pendingAfter}`. In the browser require the exact witness `2/1/1/0` and retain
  the existing captured member and ordering.
- **Failure semantics:** zero, one, three or more pending callbacks fail before
  invocation. A FIFO `shift()` invocation, two invocations, failure to discard
  exactly one stale member, any remaining member, an early/late invocation or
  a moved downstream fault point fails the structural or causal gate. The
  discarded callback is never invoked against its closed server/disconnected
  repository. The live callback remains the only invoked run-start callback.
- **Preservation:** no production scheduler/timer/repository/database/provider,
  `flushSchedule`, `drainDownstream`, queue order, fault injection, registry,
  case/control, manifest, digest, browser command or product behavior changes.
  C122/C123 behavior outside the two replaced assertion blocks remains
  accepted. The parent runs only syntax, exact-source, negative-control, hash
  and diff-scope checks; the window agent owns the fresh causal/stateful gate
  and all remaining I114 gates.
- **Alternatives rejected:** invoking both callbacks and relying on the stale
  callback's swallowed failure; retaining the stale callback for a later broad
  flush; real timers; instance plumbing in production; starting downstream
  drain early; moving fault injections; or weakening the exact two-member
  precondition.
- **Tasks/scenarios:** parent-direct `KI-W6-C124`; existing `SCN-KI-018`,
  `W6-FLOW-10`–`12`, `W6-NC-07/08`; window-agent assessment `KI-W6-I114`.

## 2. Lifecycle transition tables

### Research and stage transitions

| Transition | Actor/precondition | Atomic predicate and writes | Emitted action | Replay result | Forbidden |
|---|---|---|---|---|---|
| create | owner API; valid seeds | insert research queued/g1/config/progress | initialize v1 after commit | idempotent only through caller request policy; otherwise a new research | provider call; result visibility |
| initialize | worker; queued/g1 | queued→running; create immutable expansion stage/tasks/expected count | one task message per row, then check | existing matching stage reconstructs dispatch only | changed task set/config |
| claim task | worker; pending or expired | conditional processing+new lease token/attempt | none | live other token loses | call before claim |
| renew task lease | worker; processing + exact token + expiry>now | conditional expiry=now+60s only | none | count zero is lost | revive expired/terminal/wrong-token row; change owner/token/attempt |
| provider retry | claimed; known retryable result | terminal attempt row; task pending+nextAttemptAt; clear lease | delayed same task message | stale message rechecks DB | increment attempt on throttle wait |
| task success | claimed; strict normalized result | after immutable artifact: first-terminal succeeded+counters | aggregation check then SQS ack | matching artifact reconstructs; terminal row no-op | DB terminal before artifact |
| task skip/fail | claimed; known endpoint outcome | first-terminal skip/fail+counters/safe error | aggregation check then ack | no-op | raw error storage |
| expansion aggregate | all 2–10 expansion tasks terminal; one owner | validate exact US task set/artifacts; put candidate manifest; atomically complete expansion and create one anchor-screen task | one `US:0` task message then check | existing manifest/task set must match | derive from S3 listing; cap before screen |
| anchor aggregate | anchor task terminal; one owner | validate anchor artifact; run exact screening/rank; put 1–200 shortlist manifest; atomically complete anchor and create exact eight non-US tasks | eight ordered market task messages then check | existing shortlist/task set must match | ranking without anchor metrics; second US call |
| renew aggregation lease | aggregator; aggregating + exact token + expiry>now | conditional expiry=now+120s only | none | count zero is lost | revive expired/terminal/wrong-token stage; change owner/token/attempt/counters |
| market aggregate | all eight market tasks terminal; one owner | validate exact artifacts plus the durable shortlist; project expansion and reused US metrics to that shortlist; rerun the at-most-200-row nine-market calculation; put market manifest/result; final fenced transaction publishes result/default selection and completes research | none | completed result is immutable no-op | changed/bypassed shortlist; 300-row leakage; partial result visibility |
| recovery | recovery Lambda; overdue durable row | conditional reclaim/dispatch bookkeeping only | identity task/check messages | duplicates commute | provider call; mutation of terminal row |

### Selection, handoff, and query transitions

| Transition | Actor/precondition | Atomic predicate and writes | Emitted action | Replay result | Forbidden |
|---|---|---|---|---|---|
| save selection | owner; completed; expected revision | replace strict ordered draft; revision +1 | none | stale revision 409 | silent dedup; market-specific list |
| create run | owner; completed; expected revision; no conflicts; 1–100 | one tx creates/reuses handoff, run, snapshot, queries | existing run queue path after commit | same client key/fingerprint returns same run | partial run/queries; new planner |
| edit query review | run owner; awaiting review; expected query revision | branch validator; replace/reorder texts, preserve item-ID set; revision +1 | none | stale 409 | add/delete research-backed row |
| confirm/probe | run owner; expected revision | existing confirm transaction then existing saved probe flow | existing confirmed-query dispatch on pass | immutable attempt/result rules | replace weak keyword/query |

## 3. D1–D13 cross-cutting ledgers

### D1 — Interfaces

Exact public interfaces are `DEC-KI-019`; message/artifact interfaces are
`PAY-KI-006` and `DEC-KI-020`; pure Node exports mirror the named Python
functions in `SRC-KI-008`; the accepted repository plus corrective worker
interfaces are enumerated literally in `DEC-KI-026`, including context reads,
attempt settlement/ambiguity, retry scheduling, aggregate publication, and
recovery reconstruction. `DEC-KI-030` enumerates the backwards-compatible SQS
delay parameter and the complete private W3 helper set. All return explicit
`{outcome:...}` unions; no boolean
conflates not-found, not-ready, conflict, delay, or lease loss.

### D2 — Persistence and atomicity

The complete schema is `DEC-KI-021`. Research creation, stage task-set creation,
counter first-terminalization, retry scheduling, expansion/anchor next-stage
creation, final result plus default-selection publication, selection CAS, and
run handoff are `SAME_ATOMIC_BOUNDARY` Prisma transactions, with exact methods
and predicates in `DEC-KI-026`. S3-before-Neon and
Neon-before-SQS are `RECOVERED_BOUNDARY`: immutable artifact plus fingerprint
reconstructs the first; durable pending/terminal state plus recovery dispatch
reconstructs the second. Provider call is recovered only when the outcome is
known; otherwise `ambiguous` terminalizes (`DEC-KI-007`, `DEC-KI-030`). The
monitor checks and final repository fences in `DEC-KI-030` are the exact
in-process/external-boundary protocol. Migrations are forward
only; no existing row/backfill is required because new nullable/default fields
preserve legacy runs.

### D2A — Storage transport and isolation

Runtime uses existing `DATABASE_URL`; migration uses existing direct migration
transport. Integration tests must use `test/helpers/isolated-postgres.js`, a
disposable collision-free schema, direct non-pooled migrate connection,
verified `current_schema()` and schema-local `_prisma_migrations`, never
`public`, and exact finally cleanup of only the generated schema. Missing,
production-equal, pooled-only, wrong-schema, or cleanup mismatch fails closed.
No test may delete shared rows.

### D3 — Identities and authority

User identity is authenticated owner ID; research ID identifies one owner's
record; generation identifies immutable execution; stage/task identify work;
selection item identifies lineage using only the six-byte `DEC-KI-002` digest;
cache/request fingerprint identifies equal
provider input globally; handoff request identifies one create-run retry; Run,
RunQuery, shop, and RunStore retain existing identities. Cardinalities:
owner 1:N research, research 1:N runs, research 1:3 stages, stage 1:N tasks,
selection 1:1 RunQuery per run, one request fingerprint N tasks/cache 0:1.
No identity substitutes for owner authorization or stable shop identity.

### D4 — Ownership and concurrency

Mutable resource pairs are: API/API selection saves (revision CAS); worker/
worker task (lease token plus attempt-number increment); worker/recovery
(conditional claim and the exact `scheduleRetry` transition); aggregator/
aggregator (aggregation lease); task/aggregator (terminal counters plus all-
terminal predicate); handoff/handoff (unique key plus fingerprint); legacy/
research query writer (queryPlanSource branch and run-level revision). Each pair
has CAS, uniqueness, fencing, or disjoint state. Lease durations/seams and
one-full-duration tests are `DEC-KI-022`, `DEC-KI-026`, `SCN-KI-012`, and
`SCN-KI-020`; `DEC-KI-028/030` and `SCN-KI-022`–`026` close the
exact-expiry, task-monitor, and aggregation-monitor schedules.

### D5 — Payloads and artifacts

Payload certificates are `PAY-KI-001`–`007`; keys, fingerprints, timestamps,
and missing/corrupt/conflict/replay behavior are `DEC-KI-002`, `009`, `020`,
`026`, and `027`.
All Zod objects are strict. Supported provider contract is the single observed
shape only.

### D6 — External operations

DataForSEO caller/adapter, request cardinality, timeout 120 seconds, rate,
five-attempt ceiling, durable pre/post evidence, parsing, crash semantics,
retry scheduling, delayed delivery, known-response fence loss, and ambiguity
are `DEC-KI-005`–`009`, `DEC-KI-026`, and `DEC-KI-030`.
Google remains the existing one-call-per-query
attempt-marker flow (`SRC-KI-013`) with ≤100 calls and ten occurrences each.
S3 put/get and SQS send use existing adapters and retry ownership; SQS/S3 are
not business completion authorities. Each provider attempt must reserve and
settle the literal USD exposure in `DEC-KI-009`; no cost choice remains open.
No subprocess exists in production.

### D7 — Configuration

Replay-affecting config is the immutable v1 snapshot and fingerprint
(`DEC-KI-004`). Secrets are read only by existing secret adapter in Lambda and
never snapshotted. Clock/random seams are injected in repositories/worker;
randomness is used only for IDs/lease tokens, while retry jitter is deterministic.
Provider endpoint base and credentials changing during a generation cause
startup/config mismatch rather than result reinterpretation. The approved
`$3.00000000` budget and reservation formulas are immutable snapshot fields
from research creation. The single keyword queue property/environment mapping
is `DEC-KI-027`; it is infrastructure address, not snapshotted behavior.

### D8 — Control plane and presentation

All create/load/update/handoff/export routes and status mappings are
`DEC-KI-019`; frontend route/component ownership is `DEC-KI-023`; durable
status and stale process behavior are `DEC-KI-018`, `022`. There is no cancel
or delete path in scope. Completed result becomes public to its owner only after
the final transaction.

### D9 — Build/runtime/deployment

Backend deployable is Node ESM Lambda with current Prisma generated client,
AWS SDK externals/build convention, Zod, and exact new `@noble/hashes@2.2.0`.
Frontend is existing Next 16.2.12 build plus exact Chart.js dependencies.
Infrastructure is existing SAM plus one function/queue/DLQ/event mapping and
least-privilege S3/secret/Neon access. The function is Node.js on the same
runtime/architecture as existing handlers, timeout 180 seconds, memory 1024
MiB, ephemeral storage 512 MiB, and reserved concurrency one. Its event mapping
uses batch size one, `ReportBatchItemFailures`, and no `MaximumConcurrency`.
Source queue visibility is 360 seconds with four-day retention; DLQ retention is
14 days; redrive count is five; recovery runs once per minute. Representative emitted artifact inventory,
startup, size, and frontend build are the mandatory `GATE-KI-002`; production
delivery is `KI-W7/W8`. W7 adds the exact one-queue config/environment wiring
from `DEC-KI-027`; no second aggregation queue exists. Until that evidence
exists, D9 is decided but not proven. The local keyword-package cleanup,
reproducibility, sibling-preservation, inventory, size, and startup proof is
fixed by `DEC-KI-030`/`SCN-KI-027`; it does not alter W7/W8 deployment scope.

### D10 — Environment capability

Local Node/Prisma/Next versions are observed in package files. Applied AWS and
provider capabilities are `SRC-KI-025` and must be read-only preflighted in
`KI-W8` before mutation. Required branches are: capability satisfies locked
bound → continue after approval; does not satisfy → stop and revise A7; unknown
permission → stop with exact prerequisite. Published defaults never pass.

### D11 — Scale and complexity

All hard dimensions and operation counts are `DEC-KI-024`. Database writes are
O(tasks + attempts + selections); messages/artifacts O(tasks); successful-run
provider calls are `2×seeds + 1 anchor + 8 remaining markets`; a terminal
anchor failure creates no remaining-market task. Dedup/clustering is O(k²) at
k≤300 during screening and k≤200 during final calculation. No transaction
contains provider/network work. Result publication is
one bounded ≤32 MiB JSONB write and related state updates.

### D12 — Compatibility and lifecycle

`REQ-KI-019`–`021` and `DEC-KI-016` preserve legacy runs through an explicit
default discriminator and no backfill. Standalone cache/output files are not
imported. Mixed/unknown research contract versions are rejected, not migrated
or deleted. Retention is indefinite within scope; deletion is parked.

### D13 — Observability and privacy

Safe logs include research ID, generation, stage, task ID, attempt number,
state transition, counts, durations, fingerprints, cache hit, and safe code.
Metrics distinguish queued, rate-delayed, retry-delayed, leased, stale,
ambiguous, terminal, aggregation, and published. Logs exclude owner ID unless
hashed by existing policy, seeds/keywords, request/response bodies, URLs,
credentials, raw errors, and result content. S3/Neon retention follows A1;
provider normalized cache expires seven days.

### `DEC-KI-051` — Set-based maximum query-validation persistence

`PrismaRunRepository.saveQueryValidation()` keeps its existing live Run lease
fence and all-or-none transaction, but normalizes at most 100 unique query IDs
and persists them with one schema-scoped `UPDATE ... FROM
jsonb_to_recordset(...) RETURNING id`. The returned IDs must equal the complete
input ID set exactly; a missing, duplicate, foreign-run or otherwise
unreconciled row raises `PIPELINE_INPUT_CONFLICT` and rolls back the Run stage
and every query mutation. Null `probeSummary`/`probeResults` inputs retain the
existing stored JSON exactly as the former Prisma `undefined` writes did; all
other scalar/null semantics remain unchanged, and raw SQL sets `updatedAt` to
the supplied clock. This one maximum-scale transaction uses
`{maxWait: 5_000, timeout: 30_000}`. No other repository transaction receives
a broader timeout. The correction changes no provider batching, provider call
count, reservation, public API, schema, queue, artifact or AWS behavior.

### `DEC-KI-052` — Downstream diagnosis precedes any coordinator timeout change

- **Requirements/evidence:** `REQ-KI-010`–`015`,
  `INV-KI-004/005/010/015`, `SRC-KI-054`, `EV-KI-W6-R68`.
- **Locked choice:** CV78 is a harness observability/cleanup defect with an
  unclassified underlying stall. Do not edit the coordinator repository, add a
  retry, or set a database timeout from the teardown error.
- **Helper lifecycle:** permit one active `drainDownstream`. Around every
  dequeued discovery/domain message, record sanitized `message-start`,
  `message-complete`, or `message-failed` with queue class, discriminator,
  monotonic delivery ID, safe error name/code and repository-relative frame.
  Immediately convert the drain promise to the fulfilled outcome union
  `{outcome:"fulfilled",value}` or `{outcome:"rejected",error}`; no rejection
  may escape after teardown.
- **Diagnostic seam:** export `readDownstreamDiagnostics()`, returning active
  lifecycle/message, the last twenty downstream/backend-log/SQS trace entries,
  schema-qualified durable task/stage counts through the administration
  connection, and only `state`, `wait_event_type`, `wait_event` classifications
  for active test-database sessions. Never return PID, query text, SQL,
  connection metadata or payload values. A failed member is the fixed safe
  marker `unavailable`, without suppressing other members.
- **Browser wait:** replace only the first-domain-emission wait with a loop that
  observes a domain SQS event, a rejected outcome, or `message-failed`. At the
  unchanged 120-second deadline capture the diagnostic seam once and fail with
  its safe projection. A domain event continues through the unchanged
  partial-terminal fault point and ultimately requires the fulfilled report.
- **Cleanup:** retain the outcome outside the main try. Before schema drop, wait
  at most 5 seconds for it; if pending, capture diagnostics and keep its
  rejection observed. After the exact-schema drop, wait at most 5 seconds and
  record exactly `settled-before-drop`, `settled-after-drop`, or
  `still-pending`. Cleanup cannot pass merely because the drop aborted work.
- **Falsification:** source enforcement rejects removal of the immediate
  rejection observer and rejects schema drop ordered before the pre-drop
  settlement/diagnostic step. Existing cases, controls and digests are
  unchanged.
- **Assessment:** after sequential one-file `C127` and `C128`, run the unchanged
  causal browser command once. Pass resumes preserved closure gates. Failure is
  usable only with phase, outcome, counts, safe trace/activity classification,
  cleanup settlement and schema-absence evidence; only then may a parent choose
  a production correction.
- **Rejected:** inferred row-lock diagnosis; global/coordinator timeouts;
  unchanged blind retry; raw SQL/query/connection logging.
- **Tasks/scenarios:** `KI-W6-C127`, `KI-W6-C128`, `KI-W6-I116`; existing
  `SCN-KI-018`, `W6-FLOW-11/12`, `W6-RES-02/04`, `W6-NC-08`.

### `DEC-KI-053` — Complete W6 clock, transaction-profile, and coordinator-read closure

- **Requirements/evidence:** `REQ-KI-010`–`015`, `REQ-KI-024`,
  `INV-KI-004`–`006`, `INV-KI-010/011/015`, `SRC-KI-055`, and the accepted
  causal prefix through 100/100 discovery tasks.
- **Clock interface:** add one private `requireAwsPipelineNow(now)` in
  `PrismaRunRepository`; it returns `now` only when `now instanceof Date` and
  `Number.isFinite(now.getTime())`, otherwise throws
  `PipelineInvariantError("PIPELINE_INPUT_CONFLICT")`. The following five
  methods take required argument order `(input, now)`, have no default, invoke
  that validator before their transaction, and pass the validated value to
  `assertCompleteAggregatorInTransaction`: `readAwsReuseInputs`,
  `readAwsReusableProfiles`, `readAwsFinalReuseRows`,
  `readAwsAmbiguousDataForSeoTargets`, and
  `readAwsTerminalCruxBigQueryWork`. No repository aggregation-ownership check
  may create its own current time.
- **Clock callers:** the sole production callers pass `new Date()` as the
  second argument: one call in `domain-aggregator.js`, one in
  `lead-aggregator.js`, and three in `final-aggregator.js`. This is intentional:
  production receives the current instant while the existing harness `pinDates`
  seam deterministically substitutes its controlled clock. Together with the
  four already-correct assertion sites, the reachable inventory is exactly
  nine `assertCompleteAggregatorInTransaction` calls supplied with an explicit
  clock and zero calls containing an internal zero-argument `new Date()`.
- **Transaction profile:** define private frozen constants in the two
  repositories, each byte-equivalent to
  `Object.freeze({ maxWait: 5_000, timeout: 30_000 })`. Every W6-reachable
  interactive transaction passes its repository constant as the second
  `$transaction` argument. The exact coordinator set is eleven:
  `registerStage`, `recordDispatch`, `claimTask`, `renewTask`,
  `recordTerminal`, `claimAggregator`, `renewAggregator`, `getCompleteStage`,
  `completeAggregator`, `listRecoverable`, `cancelRunGeneration`. The exact
  run-repository set is twenty-one: `publishAwsDiscoveryStage`,
  `readAwsReuseInputs`, `readAwsReusableProfiles`,
  `publishAwsDomainCheckpoint`, `publishAwsLeadCheckpoint`, `claimAwsLeadWork`,
  `claimAwsRunLease`, `releaseAwsRunLease`, `loadAwsTrafficStage`,
  `claimAwsTrafficWorkBatch`, `recordAwsDataForSeoOutcome`,
  `readAwsFinalReuseRows`, `readAwsAmbiguousDataForSeoTargets`,
  `readAwsTerminalCruxBigQueryWork`, `publishAwsFinalResults`,
  `readReusableTrafficCache`, `readReusableLatestCruxBigQueryCache`,
  `planDataForSeoRequest`, `claimDataForSeoRequest`,
  `getDataForSeoRunCostUsd`, and `markStaleDataForSeoRequestsAmbiguous`.
  Final membership is exactly 32/32; no global Prisma default or transaction
  outside this literal set changes. `renewAwsRunLease` remains one atomic
  `updateMany` and is not misclassified as an interactive transaction.
- **Coordinator read consolidation:** `lockedTask`, `lockedStage`, and
  `lockedRun` each issue one schema-scoped `SELECT * ... FOR UPDATE`, require
  exactly one returned row, and return that row directly; their follow-up
  Prisma `findUnique` calls are removed. `recordDispatch` locks all stage tasks
  with one ordered `SELECT * ... FOR UPDATE`, uses those returned rows to prove
  exact stage cardinality and requested-item existence, then performs its
  existing `updateMany`; it performs no independent task reload. Lock order,
  state predicates, fencing, returned public shapes, and write cardinalities
  remain unchanged.
- **Parallel decomposition:** the parent freezes nine distinct files and two
  dependency waves. Wave 1 contains the five production files and may execute
  concurrently because every interface above is already frozen and the files,
  commands, runtime resources and write sets are disjoint. Wave 2 contains four
  test files and may execute concurrently only after all wave-1 leaves are
  independently accepted. The integration assessment is always window-agent
  owned and sequential. This is the explicit parallel authority required by
  the sub-window standard; it creates no implied authority for other windows.
- **Enforcement:** add cases `W6-DB-08`–`W6-DB-11` for the exact 11/21
  transaction memberships, nine-clock inventory, lock/read operation ceilings,
  required-now rejection, and controlled-time integration behavior. Controls
  `W6-NC-18`–`W6-NC-20` must respectively make acceptance fail when one
  transaction profile is omitted, one repository assertion recreates its own
  time or loses the caller argument, or one redundant reload is restored. The
  final W6 combined sets become exactly 39 cases with digest
  `f8137d25f5994cc83e4ec1deaa672656d50f19692a5907b10e47399a78c6dd80`
  and 20 controls with digest
  `0cbaad071c1bc474102394ddc0082d61f0c366d67768dcab0eafa7b5f6a3fc88`.
- **Preserved behavior:** no schema, migration, public payload, provider call,
  DataForSEO batch/cost formula, S3/SQS operation, lease duration, heartbeat,
  retry, ambiguity, API, frontend product, deployment, AWS or production
  behavior changes. The explicit profile bounds genuine interactive database
  work; it does not permit network/provider work inside a transaction.
- **Rejected:** fixing only `readAwsReuseInputs`; changing global Prisma
  defaults; extending lease durations; adding transaction retries; changing
  provider batching; retaining redundant reads behind longer timeouts; or
  treating a passing unit suite as causal closure.
- **Tasks/scenarios:** fifteenth KI-W6 corrective sequence, nine single-file
  leaves `KI-W6-C136`–`KI-W6-C144`, window-agent assessment `KI-W6-I119`,
  existing `SCN-KI-018`, and supplemental `SCN-KI-044`.

### `DEC-KI-054` — Stop task heartbeat ownership before terminalization

- **Requirements/evidence:** `REQ-KI-010`–`REQ-KI-015`, `REQ-KI-024`;
  `INV-KI-004`–`006`, `INV-KI-010/011/015`; `SRC-KI-056` and
  `EV-KI-W6-TC06`.
- **Locked lifecycle:** add one internal exported helper
  `preparePipelineTerminalLease(monitor)` in
  `src/aws-pipeline/core/lease-monitor.js`. Its complete algorithm is exactly
  `await monitor.renewNow(); await monitor.stop(); monitor.assertActive();` in
  that order. It adds no catch, suppression, retry, default, timer, clock, or
  return value. A queued/in-flight renewal must settle before `stop` returns;
  any renewal failure prevents terminalization. After successful return the
  interval is cleared and no later timer callback may renew.
- **Worker callers:** the only callers added are `processDiscoveryMessage` and
  `processLeadMessage`. Each replaces its success-path direct `renewNow()` with
  `preparePipelineTerminalLease(monitor)` immediately before its existing
  `recordTerminal(...)`; each removes only the success-path `monitor.stop()`
  that currently follows `recordTerminal`. Existing catch cleanup remains.
  The order becomes artifact validated/written -> renew -> stop/drain ->
  assert active -> fenced terminal transaction -> aggregation-check send ->
  acknowledge. No provider or artifact operation moves inside a transaction.
- **Failure/replay semantics:** renewal or prior monitor failure aborts before
  the terminal transaction. `recordTerminal` retains its token, fingerprint,
  live-expiry, state and transaction fence. A terminal-transaction failure is
  propagated through the unchanged catch cleanup. Dispatcher failure remains
  governed by the existing durable-ready-stage recovery protocol. Busy,
  cancelled and already-terminal claims remain byte-equivalent and perform no
  provider/artifact work. No lease duration, heartbeat interval, recovery age,
  retry count, queue contract, counter, or outcome union changes.
- **Exact ownership/DAG:** four one-file corrections: `C145` owns
  `lease-monitor.js`; after C145 acceptance, `C146` owns
  `discovery-worker.js` and `C147` owns `lead-worker.js` and may run in one
  explicitly authorized parallel wave; after both are accepted, `C148` owns
  `aws-pipeline-transaction-clock-enforcement.test.js`; `I120` is sequential
  and window-agent-only.
- **Enforcement:** add `W6-DB-12`, which must dynamically prove an already
  queued renewal drains, one explicit renewal completes, the timer clears
  exactly once, and a post-stop stale timer callback cannot renew; it must also
  statically prove both workers import and invoke the helper exactly once
  before `recordTerminal`, contain zero direct success-path `renewNow`, and
  contain no stop between terminalization and check dispatch. `W6-NC-21`
  moves discovery back to renew -> terminal -> stop and must falsify the
  unchanged oracle before a fresh positive passes.
- **Coverage arithmetic:** the enforcement group becomes cases
  `W6-DB-08`–`12`, digest
  `1aba569c8f08f9ca3ee240a10c4ddb4fbb0e6ec0bb00608b74aa414faefaaf39`,
  and controls `W6-NC-18`–`21`, digest
  `3068f94cf9c935bfdec5f0374182c5261fc0acaf7e5d8bf80d6b278cfa5b981c`.
  Final W6 closure is exactly 40 cases, digest
  `334999de9923c0af40fa46b1c99eb92b03efce978585a71ff6b031092d105b71`,
  and 21 controls, digest
  `66921e9aae67f455bc35678da9b6ba659165dd037856d437b91c11b3c07fde80`.
- **Rejected:** an identical CV87 timing gamble; treating the durable terminal
  plus failed acknowledgement as success; changing `renewTask`; extending
  leases/timeouts; swallowing `PIPELINE_LEASE_LOST`; changing aggregators,
  traffic settlement, dispatcher recovery, the harness timer, or global timer
  behavior; and source-order checks without a dynamic stopped-timer witness.
- **Tasks/scenarios:** sixteenth KI-W6 corrective sequence `KI-W6-CT24`–`CT27`,
  leaves `KI-W6-C145`–`C148`, assessment `KI-W6-I120`, existing
  `SCN-KI-018`, and supplemental `SCN-KI-045`.

### `DEC-KI-055` — Node test isolation mode for nested enforcement evidence

- **Trigger:** C148 review on Node `v24.14.1` proved that `node --test
  test/aws-pipeline-transaction-clock-enforcement.test.js` runs the file in a
  child process and exposes only one file-level result, suppressing its required
  ten test records and certificate. The identical file with
  `--test-isolation=none` exposes 10 pass/0 fail/0 skip and the exact five-case,
  four-control, `11/21/9/5/2/2/1` certificate.
- **Locked correction:** C148 LOCAL_NOW and I120 CV92 must use exactly `node
  --test --test-isolation=none
  test/aws-pipeline-transaction-clock-enforcement.test.js`. I120 CV93 must use
  exactly `node --test --test-isolation=none
  test/aws-pipeline-contracts.test.js test/aws-pipeline-discovery.test.js
  test/aws-pipeline-transaction-clock-enforcement.test.js`. Expected totals and
  all assertions remain unchanged.
- **Boundary:** this changes only the local evidence transport. It changes no
  source/test bytes, test registration, product behavior, runtime isolation,
  database/browser/build gate, retry/recovery rule, provider/AWS action or cost.
  The already-produced C148 candidate remains reviewable; after the window
  agent records this command supersession it must accept or reject C148 from
  its actual bytes, then continue I120 without another decomposition review.

### `DEC-KI-056` — Observe the real domain-aggregation message discriminator

- **Evidence:** `SRC-KI-057`; I120 CV94. Production and the strict message
  schema emit `type:"aggregation.check"`; no W6 producer emits a type beginning
  `domain`.
- **Exact correction:** in
  `frontend/test/browser/keyword-intelligence-e2e.mjs`, replace only
  `(event.messageTypes || []).some((type) => String(type).startsWith("domain"))`
  with `(event.messageTypes || []).includes("aggregation.check")`. Preserve the
  surrounding `event.kind === "sqs"` guard, trace floor, progress watchdog,
  timeout, diagnostics, cases, controls and every other byte.
- **Semantics:** this observes the first real domain-aggregation trigger after
  discovery completion. It changes no producer, payload, queue, domain count,
  task count, pipeline behavior or timeout. Existing `W6-FLOW-11/12` and their
  controls remain the sole coverage registrations; no new case/control exists.
- **Execution:** requester directly authorizes the one-file C149 bytes. The
  window agent independently reconciles/reviews C149, then personally runs a
  fresh I121 causal gate and, on success, the pending CV95-CV97/CH16 closure.
  A new observable failure outside this exact file/decision returns to parent.

### `DEC-KI-057` — Durable handoff identity is the sole commit signal

- **Evidence:** `SRC-KI-058`; I121 CV99; `DEC-KI-035/038` atomic same-key
  handoff contract.
- **Authoritative waiter:** `waitForDurableHandoffCommit` accepts exactly
  `{clientRequestId,expectedSelectionRevision}` and polls
  `harness.readDurableState()` unconditionally. It returns only when the latest
  durable handoff has both exact values and its associated Run has exactly 100
  RunQueries. HTTP trace presence/absence and response status never gate the
  database read or acceptance.
- **Interception:** the response-stage handler stores the sanitized numeric
  `responseStatusCode`, parses the intercepted POST body, validates the string
  client key and safe-integer revision, stores that identity, and stores the
  returned durable snapshot before calling `Fetch.failRequest`. Parse/identity/
  durability failure remains `durable-handoff-commit` failure.
- **Post-abort proof:** require the browser-netlog request identity to equal the
  intercepted identity; require the stored durable handoff ID/revision and
  100-query Run. The response-finish trace becomes diagnostic-only boolean and
  the intercepted numeric status is diagnostic-only. Same-key retry, UI state,
  30-second durability ceiling, response abort, cases/controls and all later
  behavior remain unchanged.
- **Ownership/execution:** requester authorizes parent-direct one-file C150 in
  the existing browser test, layered on accepted C149. The window agent reviews
  it independently and runs fresh I122; no production or harness-helper edit.

## 4. KI-R5 D1–D13 delta ledger

- **D1 interfaces/payloads:** `DEC-KI-034` and `PAY-KI-008` supersede only the
  W4 selection PUT item input and W5 numeric version/header mirror. All durable
  `SelectionItem`, response, run, worker and legacy interfaces remain unchanged.
- **D2 persistence/atomicity:** no schema or stored shape changes. Selection CAS
  stays one transaction. Equal-key handoff recovery in `DEC-KI-035` is a
  read-only transaction after the failed writer transaction has rolled back.
- **D2A isolation:** only `R5-FIN-07/08` write a generated non-public test
  schema through `test/helpers/isolated-postgres.js`; they verify identity,
  `current_schema()`, schema-local migration history and exact finally cleanup
  before/after writes. No other R5 case is database parity.
- **D3 identity/authority:** owner, research, selection, handoff and Run
  identities are unchanged. A client-only unsaved list key is presentation
  state and is neither sent nor persisted. W4 alone derives canonical item IDs.
- **D4 concurrency:** selection/save uses the accepted revision CAS. Handoff
  request/request competition uses the unique row plus the exact post-rollback
  reconciliation in `DEC-KI-035`; equal requests commute to one Run, unequal
  requests conflict.
- **D5 artifacts:** no S3/message artifact changes. API payload `PAY-KI-008`
  has one strict union, 262144-byte transport ceiling, canonical output and
  rejection rules; no variant probing or legacy dual parser exists.
- **D6 external operations:** no provider/AWS call. Browser→Next and Next→W4
  remain the existing HTTP operations; the three mutation bodies are explicit
  JSON. Retry applies only to same-key run handoff after an ambiguous HTTP
  outcome, never research creation or selection save.
- **D7 configuration:** no new environment, secret, clock or random source.
  Existing `crypto.randomUUID` supplies handoff IDs; no new package is added.
- **D8 control/presentation:** finalization is enabled only for the exact saved
  projection. Ambiguous handoff locks selection mutation and exposes retry of
  the same attempt. Filters/CSV share `DEC-KI-036` semantics.
- **D9 build/runtime:** backend Node and frontend Next dependency closures are
  unchanged. One final existing Next build proves emitted parser/client changes;
  no worker or Lambda artifact is affected.
- **D10 environment:** no new live capability is required. The absence of a
  local Neon-auth session narrows R5's browser claim as `DEC-KI-037`; W6 owns
  full authenticated local E2E after correction.
- **D11 scale:** strict 0–200 mutation input is O(n), maximum measured 143,641
  bytes and capped at 262,144; materialization performs one existing result
  read plus at most 200 in-memory row lookups/canonicalizations, one conflict
  analysis O(n²) at n≤200, and one CAS write. No network/database N+1 is added.
- **D12 compatibility:** durable v1 data and legacy runs are unchanged. The
  defective full-snapshot browser PUT shape is rejected rather than supported
  as a second version. A future external-client compatibility requirement would
  require an A1/A7 change.
- **D13 observability/privacy:** no request body or keyword is logged. Safe UI
  distinguishes definitive failure from retry-required ambiguity. CSV textual
  cells are neutralized without changing stored data or numeric cells.

## `DEC-KI-058` — close W6 by composing the real discovery bridge with accepted scale proofs

**Source:** `SRC-KI-059`; `EV-KI-W6-TC25`; requester direction to avoid an
unbounded browser simulation of the already-proven downstream pipeline.

**Decision:** W6 closure shall replace only the unproved browser assertion from
100 strict discovery artifacts to 1,000 durable domains with a deterministic,
isolated-database bridge. It shall not replace the accepted browser evidence
through durable handoff, workspace, run start, 100 validation calls and 100
discovery dispatches, and it shall not replace the established 1,000-domain
traffic and 1,000-domain/12,000-outcome final-publication corpora.

The implementation and proof are fixed as follows:

1. `processDiscoveryMessage` accepts a third, optional dependency object whose
   only permitted member is `resolveStoreIdentityFn`. The object must be a plain
   object; unknown members and a defined non-function resolver fail before the
   manifest read with `PIPELINE_INPUT_CONFLICT`. The selected resolver is
   `dependencies.resolveStoreIdentityFn ?? resolveStoreIdentity`. Production
   callers remain two-argument callers and therefore retain the real resolver.
2. The focused discovery proof passes the real `resolveStoreIdentity` through
   that seam with only its existing `fetch` dependency replaced by a
   deterministic no-network function. One strict query with ten unique
   `*.myshopify.com/products/result-*` probe results must yield ten strict,
   distinct stores, one immutable artifact, one terminal transition and one
   aggregation check, with exactly ten injected fetches and zero live network,
   provider or AWS operations. The default expression and invalid-dependency
   behavior are source/runtime enforced.
3. The bridge proof uses the real `processDomainAggregation`, coordinator,
   `PrismaRunRepository`, strict artifact parsers and one disposable migrated
   schema. It supplies one confirmed manifest with 100 ordered queries and 100
   succeeded strict query-discovery artifacts, ten unique stable identities per
   artifact. It must publish exactly 1,000 Shops, 1,000 RunStores, one completed
   discovery stage, one lead stage with expected count 1,000, 1,000 lead tasks
   and 1,000 `lead.domain` dispatch messages. Results remain unavailable.
4. The same maximum fixture proves transaction rollback after a deliberately
   conflicting diagnostic and proves stale aggregation-token rejection: zero
   run-specific RunStores, lead stage/tasks or rollback-only Shops may become
   visible; discovery remains aggregating and the Run remains at
   `aws_discovery` with `resultsAvailable:false`.
5. The browser's 1,000-domain/lead assertion is superseded, not weakened, by
   the bridge's exact 1,000-domain database/dispatch witness. No fresh causal
   browser run is required. Previously accepted browser witnesses are reusable
   only after exact input-hash checks; prior downstream scale evidence is
   reusable only where the changed discovery-worker branch is not in its
   dependency closure.
6. No frontend, browser harness, resolver implementation, payload/schema,
   migration, package, queue, retry, lease, provider, AWS or production behavior
   change is authorized. The deterministic fetch exists only in tests and may
   never be selected by the production runtime.

**Coverage:** add `W6-DB-13` (default/injected resolver boundary), `W6-DB-14`
(100 strict query artifacts → 1,000 durable domains/tasks/messages),
`W6-DB-15` (maximum rollback and stale-fence invisibility), and falsification
controls `W6-NC-22`–`24`. Their respective sorted-member-LF digests are
`5342728a461b927afe37050b5f4e8df6df30f42698e3b75144f5872334e19600`
and `97b186a9948a3fbb4077f1d6f4d39b2d635ad1325e37fb82cdb095661bfbe4ee`.
The final W6 unions are exactly 43 cases/digest
`5ef52fb9ed7a7cc182302cd2c2441712f5745f52948c4fb1f10b6e759c4dbe71`
and 24 controls/digest
`3bd895f41f3689c1c1d421d1ea0056c095e1d4cd57d3f90e3987f79104719707`.

**Execution:** parent-authored single-file leaves C152 → parallel C153/C154 →
window-agent-only I124. The requester explicitly directs the parent to perform
the decomposition now; the window agent independently preflights, dispatches
and reviews the frozen leaves without another decomposition phase. It stops
only on PASS or a genuinely new failure outside this decision.

### `DEC-KI-059` — deployment closure, safe activation, and bounded live proof

- **Requirements:** `REQ-KI-002`, `005`, `015`–`017`, `022`–`024`;
  `INV-KI-001`–`009`, `012`–`014`; `AUTH-KI-005`; `EXC-KI-008`.
- **Finding:** `SRC-KI-060` supersedes the stale W7 source inventory and the
  incomplete deployment mechanics in `DEC-KI-025/027`. The keyword ZIP already
  exists, but the production handler would receive the established run
  repository, keyword recovery is not invoked, the required runtime config is
  absent, the former visibility timeout violates the current Lambda/SQS rule,
  and the current deployed-pipeline template/scripts know only the established
  seven functions.
- **Runtime configuration:** `src/config.js` adds exactly
  `awsPipelineKeywordResearchEnabled` from
  `AWS_PIPELINE_KEYWORD_RESEARCH_ENABLED`, strict boolean default `false`, and
  `awsPipelineKeywordResearchQueueUrl` from
  `AWS_PIPELINE_KEYWORD_RESEARCH_QUEUE_URL`, default empty string.
  `loadAwsPipelineConfig` preserves every accepted established-pipeline branch:
  when the keyword flag is false the keyword URL may be empty and the returned
  object includes `awsPipelineKeywordResearchActive:false`; when true it
  requires an HTTPS keyword URL and returns
  `awsPipelineKeywordResearchActive:true`. Invalid active configuration throws
  `Object.assign(new Error("KEYWORD_RUNTIME_CONFIG_INVALID"),
  {code:"KEYWORD_RUNTIME_CONFIG_INVALID"})`; the uninjected keyword handler
  uses the same error object when the active flag is not true. It never guesses
  or aliases a URL. Existing
  six queue requirements and `awsPipelineActive` behavior are unchanged.
- **Production keyword repository:** when `handler(event, runtime)` receives an
  injected runtime, its injected `repository` remains authoritative for tests.
  When `runtime` is absent, it awaits `createPipelineRuntime()`, requires
  `base.prisma`, constructs exactly
  `new PrismaKeywordResearchRepository(base.prisma)`, and replaces only the
  keyword runtime's `repository`. It continues to create the 32 MiB
  keyword-only artifact store from `base.s3Client` and the shared bucket. It
  fails before record processing when keyword activation is false, repository,
  dispatcher, S3 client, artifact store or HTTPS queue configuration is absent.
- **Recovery integration:** the existing scheduled Recovery Lambda and existing
  `rate(5 minutes)` rule are reused; no second recovery function, rule, queue or
  message discriminator is added. Export a testable recovery composition that
  runs `recoverPipelineWork({now,limit},base)` first. If keyword activation is
  false it returns `{pipeline,keyword:{outcome:"disabled"}}` and performs no
  keyword repository read/send. If true it constructs
  `PrismaKeywordResearchRepository(base.prisma)`, calls
  `recoverKeywordWork({now,limit},{...base,repository:keywordRepository})`, and
  returns `{pipeline,keyword}`. `now` is one captured valid `Date`; `limit` is
  the existing integer `1..100`. An established recovery failure prevents the
  keyword pass; a keyword failure does not relabel the established result.
- **Infrastructure:** add exactly these logical resources to the current JSON
  SAM template: `KeywordResearchDlq`, `KeywordResearchQueue`,
  `KeywordWorkerLogGroup`, `KeywordWorkerRole`, `KeywordWorker`,
  `KeywordResearchMapping`, `KeywordResearchDlqDepthAlarm`,
  `KeywordResearchOldestMessageAlarm`, `KeywordWorkerErrorsAlarm`, and
  `KeywordWorkerThrottlesAlarm`. Add parameters
  `KeywordWorkerCodeKey`, `KeywordWorkerCodeVersion`, and
  `KeywordResearchEnabled` (`"false"|"true"`, default `"false"`), condition
  `KeywordResearchEnabledCondition`, and outputs
  `KeywordResearchQueueUrl`, `KeywordResearchQueueArn`,
  `KeywordResearchDlqArn`, `KeywordWorkerFunctionArn`. No existing resource is
  renamed, removed, disabled, recreated, or given broader data-plane access.
- **Queue/function/mapping literals:** standard encrypted queue, name
  `${AWS::StackName}-keyword-research`, retention `345600`, visibility `1080`,
  maximum message bytes `262144`, long poll `20`, redrive receive count `5` to
  encrypted 14-day DLQ. Worker name/log convention is `keyword-worker`, runtime
  `nodejs24.x`, `x86_64`, handler `index.handler`, memory `1024`, reserved
  concurrency `1`, timeout `180`, ephemeral storage `512`, tracing disabled,
  log retention `30`. Mapping uses batch `1`, window `0`,
  `ReportBatchItemFailures`, `Enabled` from the condition, and has no
  `ScalingConfig` or provisioned poller configuration. The 1080-second
  visibility is exactly six times the function timeout.
- **IAM/artifacts/environment:** KeywordWorker may read the existing secret,
  consume and send only `KeywordResearchQueue`, list/get/put only
  `runs/keyword-research/*`, and write only its log group. RecoveryRole gains
  only `sqs:SendMessage` to the keyword queue. ControlPlanePolicy gains only
  `sqs:SendMessage` to the keyword queue. No wildcard S3/SQS data-plane action
  or resource is permitted. KeywordWorker and Recovery receive the keyword URL
  and activation flag; existing environment members remain byte-equivalent.
  No credential value, database URL or provider credential is a template
  parameter, output, Lambda environment value, queue body or evidence member.
- **Build and deployment packet:** keep `scripts/build-lambda.js` and
  `scripts/build-keyword-worker.js` as separate accepted builders. A new
  keyword measurement script imports `KEYWORD_LAMBDA_HANDLERS`, validates only
  `keyword-worker.zip`, uses the established forbidden-inventory/one-engine/
  45-MiB ZIP/200-MiB expanded/cold-import rules, and does not delete siblings.
  New keyword deployment scripts create a content-addressed packet containing
  exactly the accepted template, `keyword-worker.zip`, and the newly built
  `recovery.zip`; refuse source/hash drift; upload encrypted versioned objects;
  create but do not execute a change set by default; require the exact A5
  approval token and `--execute` to apply a previously recorded change-set ID;
  and refuse remove/replacement/broad/unlisted changes. They target only profile
  `storesignal-dev`, region `ap-south-2`, stack
  `storesignal-production-pipeline`, environment `production`, and the STS
  account discovered during W8 preflight. No direct `sam deploy` path exists.
- **Change-set allowlists:** the disabled change set may add only the ten named
  keyword resources and may directly modify only `ControlPlanePolicy`,
  `RecoveryRole`, and `Recovery`, all with replacement `False`. It may also
  contain only the established dynamic `RecoveryInvokePermission`
  (`Conditional`, caused by `RecoverySchedule.Arn`, target `SourceArn`) and
  `RecoverySchedule` (`False`, caused by `Recovery.Arn`) dependency
  reevaluations; either may be absent, but no other member is permitted. The
  activation change set may directly modify only `KeywordResearchMapping`,
  `KeywordWorker`, and `Recovery`, replacement `False`, plus the same zero-or-one
  occurrences of those two exact Recovery dependencies. Its static direct
  targets are respectively `Enabled` and the two `Environment` members. Any
  Remove, replacement `True`, unlisted member or different detail fails before
  execution.
- **Two-step deployment:** the first W8 stack update uses
  `KeywordResearchEnabled=false`, adds the ten resources/outputs/parameters,
  installs the Recovery and keyword code plus narrow IAM/environment changes,
  and proves the mapping disabled and keyword recovery inactive. Backend
  hosting then receives the exact queue URL and flag under a separately
  approved host mutation. One normal owner request queues one one-seed research
  while disabled and proves durable `queued` plus one visible source message
  and zero keyword Lambda processing. A second separately reviewed stack update
  sets `KeywordResearchEnabled=true`; it may modify only the keyword mapping,
  KeywordWorker/Recovery environment and CloudFormation-declared dependent
  resources identified by the reviewed change set. The already-queued research
  is the sole paid canary; no second research is created.
- **Canary boundary:** the canary uses the real authenticated API, SQS event
  source, Lambda, Neon, S3 and dashboard. For one seed and a nonempty shortlist
  its planned first pass is exactly 11 logical calls (2 US expansion, 1 US
  anchor overview, 8 market overviews), at most 55 attempts, and never more than
  the durable `$3.00000000` research cap. Record actual attempts/cost/duration,
  artifact sizes, Lambda peak memory, queue/DLQ/alarm state, result and default
  selection counts. Create the run handoff through the normal dashboard/API and
  verify its 100-or-fewer immutable RunQueries, but do not confirm/start that
  downstream Run; Google, lead, Browserless, traffic and CrUX work are outside
  this canary and receive zero authorization.
- **Approval/rollback:** read-only STS/quota/stack/config/secret-metadata/provider
  capability checks may precede approvals. Disabled stack update, any secret
  version mutation, backend-host configuration, activation update, the one paid
  canary, and any rollback/disable action are distinct approvals; none implies
  another. Failure stops without queue purge, DLQ redrive, data deletion, a
  second canary or manual resource edits. A preapproved rollback changes the
  backend flag and stack parameter back to false; retained rows/artifacts remain
  evidence and are not deleted.
- **Coverage:** W7 requires exactly 12 cases, digest
  `6bacf5d9291362ee0d01f5d0d8e3e53f8f9e214a6ebbf5711497c80f3d74aa2e`,
  and 12 controls, digest
  `6950a20f91b666c03cf59c495576e72ad1501fcd58aa5f4378900bd473edafd7`.
  W8 requires exactly 10 live cases, digest
  `b716a609b2269f69d4e042503ad47dabb1eb397e17726af850f38ab09940431a`,
  and six controls, digest
  `1a2fd2fb71c94f297b27c5c6ad580c67d94ae807525b420996bd4382d46b7c6e`.
- **Supersession:** this decision supersedes only the W7/W8 mechanics in
  `DEC-KI-025` and the W7 configuration timing in `DEC-KI-027`. Their approval
  separation, one-queue architecture and all accepted local behavior remain.
- **Tasks/scenarios:** `KI-W7-T1`–`T6`, `KI-W8-T1`–`T3`,
  `SCN-KI-047`, `SCN-KI-048`.

### `DEC-KI-060` — AWS-first disabled deployment; local activation/canary postponed

- **Requirements:** `REQ-KI-002`, `005`, `015`–`017`, `022`–`024`;
  `INV-KI-001`–`015`; `AUTH-KI-005/007`; `EXC-KI-008`.
- **Requester decision:** deploy and verify the AWS keyword infrastructure first.
  The backend and frontend remain local. Do not configure a hosted control
  plane, activate keyword processing, create a research, call a provider, or
  perform the live handoff in KI-W8.
- **Current-window split:** KI-W8 consumes the accepted W7 template,
  `keyword-worker.zip` and `recovery.zip`; performs read-only AWS target/quota/
  stack preflight; uploads the three content-addressed versioned objects;
  creates and reviews the exact disabled change set; after a separate approval,
  executes that reviewed ID; inspects the applied disabled stack; and stops.
  `KeywordResearchEnabled` is exactly `false`; KeywordResearchMapping is
  disabled; KeywordWorker and Recovery keyword flags are false; the source
  queue and DLQ are empty; established mappings and the recovery schedule
  remain in their accepted active state.
- **W8 action universe:** `W8-ACT-01` uploads the accepted objects and creates/
  reviews the disabled change set only. `W8-ACT-02` executes only its recorded
  reviewed ID and waits for/inspects the disabled result. Each requires its own
  requester approval. No other mutation is permitted. CloudFormation's normal
  automatic update rollback is observed; W8 never purges, redrives, deletes,
  manually repairs, activates, or creates a second change set after an
  observable failure.
- **W8 preflight:** requires exact W7 source/package hashes; fixed profile
  `storesignal-dev`, region `ap-south-2`, stack
  `storesignal-production-pipeline`; STS account; complete/stable starting
  stack; sufficient Lambda/SQS/CloudFormation quotas; expected artifact bucket;
  applied bucket versioning enabled, AES256 default encryption, all four public-
  access blocks true, `BucketOwnerEnforced`, and only the accepted seven-day
  incomplete-multipart lifecycle rule;
  no pending stack operation/change set; and the exact disabled change allowlist
  from `DEC-KI-059`. It does not read secret values, contact DataForSEO, access
  Neon, start a browser, or require frontend/backend sessions.
- **W8 identity privacy:** the exact 12-digit account, account-bearing bucket/
  ARN/URL, object-version IDs and change-set ID remain only in process memory
  and mode-0600 ignored deployment records. Tracked A5/A6/S3 records contain
  only SHA-256 digests, presence/cardinality and account-last-four projections;
  every consumer recomputes equality before the external operation. The packet
  approval token remains the exact source/account-bound authorization fence.
- **W8 coverage:** cases are exactly `W8-CONF-01`, `W8-LIVE-01`,
  `W8-LIVE-02`, `W8-LIVE-03`, digest
  `3bd44b2c2c244b1dd29881dcfa249d9cdad5f9b1aecc981c56612d587283ca7e`.
  Controls are exactly `W8-NC-01`–`W8-NC-08`, digest
  `9bd004917f960abb4842ea2f2da48ed60821fdedd55fcbc54dc7bdd271037ea6`.
  They prove preflight identity/capability, object/change-set identity, applied
  disabled topology, exact approval ledger, hash-drift rejection and unlisted-
  change rejection plus required/registered/executed/activated equality,
  zero skips/duplicates, oracle integrity and live-inspector fidelity. Zero
  Lambda keyword invocation, provider call, database operation, API research,
  browser action or paid cost is required or allowed.
- **Deferred local-control-plane window:** KI-W9 owns later local backend/
  frontend configuration from exact W8 outputs, local profile permission proof,
  strict secret/provider capability proof, two local authenticated owners, the
  single research while mapping remains disabled, reviewed activation, the
  same bounded paid canary, rendered dashboard selection, immutable run handoff
  and failure-only disable rollback. KI-W9 is `DRAFT / NOT ASSIGNABLE`; it must
  be reauthored after W8 supplies applied outputs and the requester is ready to
  provide local sessions and approve paid execution. It may not infer standing
  authority from W8.
- **Supersession:** this decision preserves every accepted W7 source/runtime/
  template/package interface in `DEC-KI-059` but supersedes its W8 hosted-
  control-plane, activation, canary, rollback and seven-action sequencing. The
  parent-approved old W8 decomposition revision `7f2bc819…` is retired without
  deletion as unexecuted historical authoring evidence.
- **Tasks/scenarios:** current `KI-W8-T1/T2`, `SCN-KI-049`; deferred
  `KI-W9-AUTHORING`.

### `DEC-KI-061` — W8 terminates with active keyword AWS infrastructure

- **Requester decision:** KI-W8 remains the final deployment window. There is
  no KI-W9. The backend and frontend continue to run locally, no research or
  paid canary is created by W8, and ACT-01 remains byte-for-byte the disabled
  create/review operation from `DEC-KI-060`.
- **ACT-02 replacement:** one requester approval authorizes one bounded
  sequence: apply the exact ACT-01 full change-set ID; require the complete
  expected-disabled inspection; create and strictly review the deterministic
  `phase=activate` change set; require its direct set to be exactly
  `KeywordResearchMapping.Enabled`, `KeywordWorker.Environment`, and
  `Recovery.Environment`, replacement `False`, plus only the zero-or-one exact
  Recovery dependency members already defined by `DEC-KI-059`; apply that
  exact reviewed activation ID; then require the complete expected-active
  inspection. The production deployment guard maps both `full` apply and both
  `activate` operations to the single authority label `W8-ACT-02`.
- **Final active oracle:** `KeywordResearchEnabled` is `"true"`;
  `KeywordResearchMapping` is `Enabled`; KeywordWorker and Recovery expose
  `AWS_PIPELINE_KEYWORD_RESEARCH_ENABLED="true"`; the established six mappings
  and Recovery schedule remain enabled; inventory/IAM/queue/DLQ/function/alarm
  properties still equal the template; the newly created keyword source queue
  and DLQ remain empty at inspection; and no direct Lambda invocation, queue
  data-plane operation, secret-value read, API research, browser, provider call
  or paid call is performed by W8.
- **Atomicity and failure:** the full apply and activation apply are two
  separate CloudFormation transactions inside one approved ACT-02 sequence.
  Activation begins only after the disabled transaction and inspector pass.
  Any failed or ambiguous full apply stops before activation. Any failed or
  ambiguous activation stops after read-only status/event reconciliation; the
  accepted disabled stack is the safe rollback state. W8 never manually
  repairs, deletes, purges, redrives, directly invokes, or creates a research.
- **Operational consequence:** once activation succeeds, the mapping and
  scheduled Recovery integration are live. A later local backend request may
  enqueue work without another AWS enablement action. The ACT-02 approval must
  therefore explicitly cover this active state; it does not authorize W8 to
  submit work itself.
- **Supersession:** this decision supersedes only the disabled terminal state,
  ACT-02 algorithm/output, KI-W9 reservation, and activation prohibition in
  `DEC-KI-060`. Preflight P1-P6, ACT-01, packet/object identity, privacy,
  allowlists, provider/cost exclusions, and all accepted W7 behavior remain.
- **Tasks/scenarios:** `KI-W8-T2`, `SCN-KI-049`; `KI-W9` is retired and is not
  a successor window.

### `DEC-KI-062` — v2 retailer phrase match and shortlist demotion

- **Requirements:** `REQ-KI-004`, `REQ-KI-024`.
- **Locked choice:** v2 retailer classification keeps the frozen 22-token list.
  Matching uses ordered normalized tokens, consecutive two-token compact folds
  (`wal mart` / `home depot` / `best buy`), compact-signature substring only
  for retailer forms of length ≥ 7, frozen aliases `wallmart` and `amazom`,
  and Levenshtein distance ≤ 1 only when both strings have length ≥ 6. The
  v2 200-shortlist ranks `leadFindingShortlistGroup` 0 then 1 then 2 before
  the existing `DEC-KI-006` comparator. Group 0 has none of
  `brand_competitor`, `local_intent`, `junk_quality`, or
  `informational_dropped`. Group 1 has a penalty flag and is not
  informational. Group 2 is `informational_dropped`. Rows are demoted, not
  excluded. v1 snapshots and the v2 config schema/version are unchanged.
- **Rejected:** expanding the retailer list; unbounded dictionaries; edit
  distance on short names; dropping penalty rows from the 200; ranking v1 by
  these groups; a new research/Google step.
- **Consequences:** misspelled or hyphenated retailer phrases stop occupying
  default-query and overview budget ahead of independent-store phrases.
- **Tasks/scenarios:** `CASE-KR-L-011`, `CASE-KR-L-012`, `CASE-KR-L-013`.

### `DEC-KI-063` — v2 Jaccard bars, informational rescue, invariant-s stem

- **Requirements:** `REQ-KI-004`, `REQ-KI-006`.
- **Locked choice:** v2 pair merge uses content-token Jaccard against
  `leadFindingJaccardThreshold(min(|A|,|B|))`: ≤ 3 tokens → 0.5; ≥ 4 tokens →
  0.6. Same-lane only. The v2 config `clustering.similarityThreshold` literal
  `0.8` remains for snapshot parse and is not the v2 merge bar. Naive `-s`
  stemming skips the frozen `INVARIANT_S_TOKENS` list and still folds
  `stores` / `paddles`. v2 `informational_dropped` is true for `how to` /
  `what is` / `wiki` regardless of DataForSEO intent; a DataForSEO
  `informational` label is ignored for that flag when the phrase contains
  `best`, `review`, `reviews`, `vs`, or `comparison`. v1 flag, stem, and
  cluster paths are unchanged. No seed-overlap default gate.
- **Rejected:** seed-token default gate; lowering 1–2-token pairs with a 50%
  bar as a substitute for identity (share-one on two 2-token sets is 33%);
  config version bump; CSE in research.
- **Consequences:** `organic cotton baby clothes` / `onesies` share a cluster;
  `best ceramic mugs` can default; `tennis` does not become `tenni`.
- **Tasks/scenarios:** `CASE-KR-L-016`, `CASE-KR-L-017`, `CASE-KR-L-018`.
