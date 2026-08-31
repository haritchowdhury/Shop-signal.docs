# Keyword Intelligence Locked Product Contract (`A1`)

**Contract revision:** `KI-PC-2`  
**Status:** locked product behavior; implementation and deployment remain unauthorized

This artifact is the sole authority for required behavior, invariants,
exclusions, compatibility, and authorization for the KeywordSearchVolume
integration. It contains no execution status or accumulated evidence.

The other package artifacts are:

- `A2` — `KEYWORD_INTELLIGENCE_DISCOVERY_DOSSIER.md`
- `A3` — `KEYWORD_INTELLIGENCE_DECISION_LEDGER.md`
- `A4` — `KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md`
- `A5` — `ACTIVE_EXECUTION_STATE.md`
- `A6` — `KEYWORD_INTELLIGENCE_EXECUTION_EVIDENCE.md`
- `A7` — `KEYWORD_INTELLIGENCE_SPECIFICATION_CHANGELOG.md`
- `A8` — `KEYWORD_INTELLIGENCE_TRACEABILITY_INDEX.md`

`KEYWORD_SEARCH_VOLUME_INTEGRATION_PLAN.md` is the product-level source that
this package compiles. It is not an execution authority after this package is
activated.

## 1. Defined terms

| Term | Locked operational meaning |
|---|---|
| research | One owner-scoped, generation-fenced execution over 1–5 seed phrases and all nine supported markets. |
| recommended | An active calculated keyword whose preserved result has `recommended=true`. For v1 snapshots that is the Python-parity score threshold. For v2 researches it is the default query plan: one non-blocked representative per concept cluster, capped at 100. It is not an arbitrary top-N label. |
| selected | A keyword present in the research record's current durable selection draft. |
| retained | A selected keyword in a conflict-free finalized selection containing 1–100 items. |
| active keyword | A calculated or manually added keyword not removed from the current research revision. |
| screened candidate | One globally unique phrase from US expansion that has passed strict US overview normalization. |
| shortlist | The first at most 200 screened candidates under the deterministic anchor ranking in `DEC-KI-006`; only this set receives the remaining eight markets. |
| duplicate conflict | Two selected items with equal compact signatures or Jaccard token similarity at least `0.88`. |
| research-backed run | An Email Scraper `Run` created atomically from a finalized keyword selection revision. |
| query | Exactly one Shopify-scoped Google query mapped from exactly one retained keyword. |
| result occurrence | One accepted Google Custom Search result row for one query before stable-shop/domain merging. |
| complete dashboard | All behavior listed in `REQ-KI-014`; not merely a keyword table or selection dialog. |

## 2. Required user-visible behavior

- `REQ-KI-001` A signed-in owner can create research from 1–5 distinct seed
  phrases. A seed is Unicode NFKC-normalized, trimmed, internal whitespace is
  collapsed, contains 1–100 characters, and is compared case-insensitively for
  duplicate rejection.
- `REQ-KI-002` Research runs asynchronously and durably. Closing a tab,
  navigating away, signing out, or restarting the API does not cancel or erase
  it. Reopening its URL shows its persisted current state.
- `REQ-KI-003` Every shortlisted keyword uses exactly the supported market set: US, GB,
  CA, AU, NZ, DE, FR, IN, and AE with the locked location/language mapping in
  `DEC-KI-004`.
- `REQ-KI-004` Except for the explicitly changed collection topology in
  `REQ-KI-023`–`024` and the lead-finding recommendation contract for
  `keyword-research-config-v2` researches, v1 snapshots preserve the ported
  Python behavior. v2 researches classify with closed-class local/store/retailer
  operators, cluster by dynamic concept key, score with a stable lead-finding
  formula, and default-select one non-blocked representative per cluster.
- `REQ-KI-005` A completed research persists its complete normalized dashboard
  result, default selection, configuration snapshot, and provenance in
  Neon/Postgres. Output files and browser storage are not sources of truth.
- `REQ-KI-006` For v1 snapshots, all active recommended keywords are selected
  by default when their count is at most 100. For v2 researches, default
  selection is exactly one non-blocked representative per concept cluster,
  capped at 100. When more than 100 exist, exactly the first 100 under the
  locked sort are selected and the UI truthfully reports the cap and
  unselected count. There is no top-10 reduction.
- `REQ-KI-007` The owner may select recommended or non-recommended calculated
  keywords, add manual keywords, edit keyword text, remove items, and restore
  calculated items, subject to the durable revision protocol.
- `REQ-KI-008` The selection draft may contain at most 200 items so duplicate
  review remains possible after an over-selection. Finalization requires 1–100
  retained items.
- `REQ-KI-009` Exact and near-similar selected items are shown as conflicts.
  The system supplies one deterministic canonical suggestion but never silently
  deletes or replaces a user's selection. Finalization fails while any conflict
  remains.
- `REQ-KI-010` Every retained keyword maps to exactly one query. No retained
  keyword is discarded because it is informational, non-product, weakly
  probed, or outside a top-N ranking.
- `REQ-KI-011` Query mapping is lane-aware: `category_discovery` becomes
  `site:myshopify.com/products <keyword>`; `store_discovery`,
  `local_discovery`, and `brand_competitor` become
  `site:myshopify.com <keyword>`.
- `REQ-KI-012` Google Custom Search probes every mapped query for at most ten
  results. Weak or failed probes remain visible in the existing editable query
  review and do not trigger replacement keyword generation.
- `REQ-KI-013` Research-backed query review preserves revision conflicts,
  explicit confirmation, saved probe evidence, and downstream AWS dispatch.
  The user may edit and reorder mapped queries but may not add or remove rows;
  this preserves one retained keyword to one query.
- `REQ-KI-014` The Next.js application contains the complete current dashboard:
  research hero and phrase chips; manual add/edit/remove; cumulative and
  country views; seed, cluster, intent, lane, facet, volume, opportunity,
  recommendation, flag, and text filters; summary cards; seed chart; interactive
  3D cluster landscape with controls, legend, tooltip, and inspector; funnel;
  discovery mix; intent, recommendation, opportunity, and flag charts; volume
  overlap; monthly history; recommended volume/trend; volume/difficulty bubble;
  competition/opportunity scatter; sortable/selectable/editable/paginated
  table; theme; loading/empty/error states; tooltips; and filtered CSV export.
- `REQ-KI-015` A research-backed run is created only from the exact owner and
  expected selection revision. One database transaction links the run, copies
  an immutable snapshot, and creates one `RunQuery` per retained keyword.
- `REQ-KI-016` A run-specific keyword snapshot survives later research edits
  and completion of the Email Scraper run. It includes original and final
  keyword text, source seeds, market metrics, lane, facets, cluster, score,
  flags, recommendation, and initial query.
- `REQ-KI-017` Owner-scoped research and run snapshots remain durable until a
  separately authorized retention/deletion policy is introduced. Cache rows
  expire after seven days and may be replaced only by a successfully parsed
  normalized response.
- `REQ-KI-018` CSV and JSON-equivalent exports are derived on demand from the
  persisted normalized result and current filters; they never expose raw
  provider bodies or credentials.

## 3. Invariants and limits

- `INV-KI-001` Neon/Postgres is the sole durable application database and
  coordinator. SQLite is absent from the integrated runtime.
- `INV-KI-002` S3 stores only private, encrypted, versioned, immutable worker
  artifacts. SQS messages carry identities and fingerprints, not seeds,
  results, provider bodies, credentials, or business documents.
- `INV-KI-003` The research API creates/reads durable state and dispatches only
  an initial identity message. It performs no DataForSEO research.
- `INV-KI-004` No Lambda invocation performs an entire research. Expansion and
  overview calls are bounded task units and final calculation is a separately
  fenced aggregation transition.
- `INV-KI-005` Stage completion derives only from terminal Neon evidence for an
  immutable expected task set. Queue emptiness, S3 counts, and S3 events are
  never completion signals.
- `INV-KI-006` Every worker uses idempotent first-terminal transitions, bounded
  leases, generation/token fencing, deterministic fingerprints, explicit
  zero-count advancement, and one conditional aggregator owner.
- `INV-KI-007` A worker validates and writes its immutable artifact before its
  terminal Neon result, sends an aggregation check, then acknowledges its SQS
  record.
- `INV-KI-008` Provider-call ambiguity is terminal for that request identity;
  an in-flight call whose outcome cannot be proven is never automatically
  repeated.
- `INV-KI-009` Raw DataForSEO bodies, raw unrestricted HTML, credentials,
  tokens, authorization headers, credential-bearing URLs, and customer contact
  data never enter Postgres, S3, SQS, logs, fixtures, frontend responses, or
  exports.
- `INV-KI-010` Final retained keywords and resulting queries are each bounded
  at 100. Google probe output is bounded at 10 accepted/rejected occurrences
  per query and therefore 1,000 pre-merge occurrences for the run.
- `INV-KI-011` Stable shop identity and downstream domain merging remain the
  existing `stableShopIdentity()`, `Shop.stableKey`, `shopIdForStableKey()`, and
  `runStoreId()` behavior.
- `INV-KI-012` Research worker reserved concurrency is one. The SQS event-source
  mapping does not set `MaximumConcurrency=1`.
- `INV-KI-013` Research visibility and mutation require authenticated
  `ownerId` equality. Cache rows are global internal optimization data and
  confer no access to any research or run.
- `INV-KI-014` Only a final generation-fenced Neon transaction publishes a
  complete research result. Partial checkpoints are not dashboard results.
- `INV-KI-015` One selection item maps to one query row by a stable selection
  item identity; editing query text does not break that lineage.

## 4. Compatibility and migration policy

- `REQ-KI-019` Existing runs without keyword-research lineage retain their
  product-only generator, validation rules, row-add/remove behavior, API
  representation, and historical readability. They are not backfilled.
- `REQ-KI-020` Existing KeywordSearchVolume SQLite cache and output files are
  not imported into production. Sanitized historical fixtures may be used only
  for parity and payload proof.
- `REQ-KI-021` Existing completed research records use their snapshotted
  contract/configuration version. Unsupported future or malformed versions are
  rejected with a safe `CONTRACT_MISMATCH`; they are never guessed or silently
  upgraded.
- `REQ-KI-022` Every DataForSEO network attempt requires a successful atomic USD
  cost reservation against immutable `maxCostPerResearchUsd=3.00000000`.
  Suggestions and related each reserve `0.01560000` per call. Overview with
  requested keyword count `n` reserves
  `0.01200000 + 0.00012000*n`. Known provider cost settles the reservation;
  ambiguous exposure remains counted at its reservation. A call is forbidden
  when settled cost plus active/ambiguous reservations plus its proposed
  reservation would exceed `3.00000000`; budget exhaustion makes zero provider
  calls and terminally fails with the safe truthful budget error.
- `REQ-KI-023` Expansion is intentionally changed from every market to the US
  anchor only: location code `2840`, language code `en`, language name
  `English`. Each of at most five seeds receives one suggestions and one
  related request, for 2–10 expansion calls. Per-seed endpoint merge retains at
  most 60 phrases including the seed; global first-occurrence merge retains at
  most 300 unique candidates.
- `REQ-KI-024` One US anchor overview request screens all 1–300 candidates.
  Strict usable non-informational normalized rows are processed through the
  preserved variant, cluster, flag, recommendation, and scoring algorithms,
  ranked by `DEC-KI-006`, and truncated to 200. The other eight market requests
  contain only that shortlist; the final calculation reuses the US metrics and
  recalculates the complete nine-market result. No candidate is capped before
  the metric-backed US screen.

## 5. Explicit exclusions

- `EXC-KI-001` No Python runtime, Python subprocess, SQLite database, iframe,
  separate API/application, second dashboard, Fargate, Step Functions,
  DynamoDB coordination, or S3-event/queue-emptiness completion.
- `EXC-KI-002` No nine-market expansion, Google `gl` fan-out, AWS/Luna/storefront
  redesign, or clothing-specific scoring ontology. New researches use
  lead-finding classification, concept-key clustering, and one-representative
  default selection (`keyword-research-config-v2`). Persisted v1 snapshots keep
  Python-parity scoring and are not rewritten.
- `EXC-KI-003` No product-only query policy and no storefront-verification or
  second research step between query mapping and Google probing.
- `EXC-KI-004` No automatic duplicate reduction, arbitrary top-N reduction, or
  per-market final selection list.
- `EXC-KI-005` No replacement of auth, frontend/API control-plane patterns,
  stable shop identity, query probing, or downstream pipeline architecture.
- `EXC-KI-006` No import or retention of raw historical provider response files.
- `EXC-KI-007` No cancellation/deletion endpoint in this scope. Research may
  terminally fail but is not user-cancelled.
- `EXC-KI-008` No deployment, secret installation, event-source enablement,
  paid/provider call, production database write, queue operation, or AWS
  mutation without its named later approval gate.

## 6. Authorization and deployment boundary

- `AUTH-KI-001` This contract authorizes documentation and read-only discovery
  only. It does not authorize implementation.
- `AUTH-KI-002` `ACTIVE_EXECUTION_STATE.md` remains the sole assignment
  authority. It names the keyword package for documentation but keeps `KI-W1`
  unassigned while its recorded gates/readiness conditions remain open.
- `AUTH-KI-003` Local implementation may begin only after a parent records a
  matching contract/checklist hash and one exact assignment in `A5`.
- `AUTH-KI-004` Isolated database tests require the existing disposable-schema
  harness and a non-production `TEST_DATABASE_URL`.
- `AUTH-KI-005` Infrastructure source edits, AWS creation, secret changes,
  event-source enablement, provider calls, and production canaries are separate
  gates exactly as specified by their checklist windows.
- `AUTH-KI-006` No implementation window may stage, commit, repair, move, or
  reverse the coordination-root relocation or overwrite unrelated frontend
  changes.
- `AUTH-KI-007` The requester approved the exact `$3.00000000` research budget
  and formulas in `REQ-KI-022`; this closes the former `GATE-KI-003` authoring
  decision but authorizes no paid call. Paid calls remain separately gated by
  `AUTH-KI-005` and the active execution state.
