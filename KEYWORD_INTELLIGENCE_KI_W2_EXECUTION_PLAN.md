# KI-W2 Execution Plan — Exact Node Calculation and Selection Engine

**Status:** ASSIGNED — A5 `state_version 72` records one-window `KI-W2`
(`current_window: KI-W2`, `current_status: IN_PROGRESS`, `authorized_sequence:
[KI-W1, KI-W2]`, `accepted_through: KI-W1`)
**Package:** `KEYWORD_INTELLIGENCE`
**Window:** `KI-W2` (A4 `KI-CL-4`, lines 185–293)
**Prepared:** 2026-08-17
**Assigned:** 2026-08-17 (parent approval; Python oracle deps installed and
verified — `pytest 35/35 pass`)

This document is a requirements-gathering and plan-of-action artifact for the
`KI-W2` window of `KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md` (A4). It
does not authorize work. Nothing here may be executed until the parent accepts
`KI-W1` and records a one-window `KI-W2` assignment in A5 (`AUTH-KI-003`,
`DEC-KI-025`).

Authoritative references: A1 `KEYWORD_INTELLIGENCE_PRODUCT_CONTRACT.md`, A3
`KEYWORD_INTELLIGENCE_DECISION_LEDGER.md`, A4 `KEYWORD_INTELLIGENCE_
IMPLEMENTATION_CHECKLIST.md`, A2 `KEYWORD_INTELLIGENCE_DISCOVERY_DOSSIER.md`,
A6 `KEYWORD_INTELLIGENCE_EXECUTION_EVIDENCE.md`, A7
`KEYWORD_INTELLIGENCE_SPECIFICATION_CHANGELOG.md`, A8
`KEYWORD_INTELLIGENCE_TRACEABILITY_INDEX.md`.

---

## 1. Current execution state and gates

| Fact | Value |
|---|---|
| A5 state version | `71` |
| Current window | `KI-W1` |
| Current status | `AWAITING_REVIEW` |
| `KI-W2` assignment | not granted; `authorized_sequence: [KI-W1]` |
| A1 hash | `8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c` |
| A4 hash | `f8a71a5a73e4381475c7719f2bd3c8ca3fd83318d239f324e0ec3289b271b7ed` |
| `@noble/hashes` | `2.2.0` installed in `email_scraper/`; `blake2s` six-byte digest verified |
| Backend worktree | clean at `c7c9412 K1-W1` |
| Standalone oracle revision | `KeywordSearchVolume@6ce7010` (multi-country support) |

`KI-W2` depends on `KI-W1` (accepted) and `GATE-KI-002` representative-build
proof (`@noble/hashes@2.2.0`). `KI-W1` is complete and awaiting review; `KI-W2`
must not begin until the parent accepts `KI-W1`, hashes A1/A4, and CAS-switches
A5 to `KI-W2`.

---

## 2. Window contract (verbatim from A4 lines 185–202)

- **objective:** Produce Python-parity normalized research results, exports,
  default selections, and conflict analysis in pure Node.
- **depends_on:** `[KI-W1]`
- **consumes:** generated Prisma types only; `SRC-KI-006`…`SRC-KI-011`;
  `DEC-KI-003`…`DEC-KI-016`
- **produces:** pure Node modules, strict domain schemas, golden parity
  fixtures/tests
- **assigned_agent_policy:** one_window
- **authorized_write_scope:**
  - `email_scraper/src/keyword-intelligence/config.js`
  - `email_scraper/src/keyword-intelligence/schemas.js`
  - `email_scraper/src/keyword-intelligence/normalize.js`
  - `email_scraper/src/keyword-intelligence/intent.js`
  - `email_scraper/src/keyword-intelligence/dedup.js`
  - `email_scraper/src/keyword-intelligence/cluster.js`
  - `email_scraper/src/keyword-intelligence/score.js`
  - `email_scraper/src/keyword-intelligence/pipeline.js`
  - `email_scraper/src/keyword-intelligence/selection.js`
  - `email_scraper/src/keyword-intelligence/query-mapper.js`
  - `email_scraper/src/keyword-intelligence/export.js`
  - `email_scraper/test/fixtures/keyword-intelligence/parity-input-v1.json`
  - `email_scraper/test/fixtures/keyword-intelligence/parity-output-v1.json`
  - `email_scraper/test/fixtures/keyword-intelligence/selection-cases-v1.json`
  - `email_scraper/test/keyword-intelligence-parity.test.js`
  - `email_scraper/test/keyword-intelligence-selection.test.js`
  - `email_scraper/test/keyword-intelligence-query-mapper.test.js`
- **shared_file_scope:** none
- **read_only_scope:** the `KeywordSearchVolume/` pipeline, config, tests, and
  dashboard files named in A4 (see §6)
- **authorized_actions:** `[local_source_edits, local_node_tests,
  development_only_python_parity_oracle, evidence_updates]`
- **prohibited_actions:** `[runtime_python_integration, provider_calls,
  database_writes, AWS_operations, frontend_edits, package_changes, commits]`

---

## 3. Preconditions (P1–P4)

| ID | Requirement | Current status / evidence needed |
|---|---|---|
| `KI-W2-P1` | Assignment/hashes/version match | NOT met — parent must CAS A5 to `KI-W2`; A1/A4 hashes pinned above |
| `KI-W2-P2` | `KI-W1` accepted and exact hash dependency exists | `@noble/hashes@2.2.0` in `email_scraper/package.json` + `node_modules`; KI-W1 accepted not yet recorded |
| `KI-W2-P3` | `@noble/hashes@2.2.0` representative build proof present | GATE-KI-002 proof exists (`EV-KI-A-029`); W2 re-asserts import of `@noble/hashes/blake2.js` |
| `KI-W2-P4` | Dirty state/scope and standalone source revision recorded | Backend clean; coordination root dirty (uncommitted A5/A4 docs); oracle pinned `6ce7010` — record in evidence |

---

## 4. Task T1 — Pure function port (A4 lines 209–246)

**Task:** direct-port configuration, models, normalization, intent, dedup,
clustering, scoring, pipeline aggregation, and export functions.

**Requirements/decisions:** `REQ-KI-003`–`005`, `018`, `023`, `024`;
`DEC-KI-004`, `010`–`012`, `024`.

### 4.1 Source → target module map (from `SRC-KI-006/008`)

| Python source (read-only) | Node target (owned) | Ported surface |
|---|---|---|
| `KeywordSearchVolume/config.yaml`, `pipeline/config.py` | `src/keyword-intelligence/config.js` | immutable `keyword-research-config-v1` snapshot per `DEC-KI-004` (nine markets, US anchor, `expansionPerSeedLimit=60`, `screenCandidateLimit=300`, `shortlistLimit=200`, `overviewBatchLimit=700`, `maxCostPerResearchUsd="3.00000000"`); no credentials, no paths/offline/raw modes |
| `pipeline/models.py` | `schemas.js` | Zod 4.4.3 strict schemas: `keyword-research-config-v1`, `keyword-research-result-v1` (fields exactly `DEC-KI-012`), market/metric/keyword/cluster/summary rows; all objects reject unknown keys |
| `pipeline/normalize.py` | `normalize.js` | `computeTrendSlope`, `normalizeItem`, `hasMetrics`, `trendToZeroOne`, `normalizeVolume`, `leastSquaresSlope` |
| `pipeline/intent.py` | `intent.js` | `INTENT_BASE`, `commercialIntentScore`, `isInformational` |
| `pipeline/dedup.py` | `dedup.js` | `tokenize`, `signature`, `compactSignature`, `stableId` (BLAKE2s six-byte via `@noble/hashes`), `jaccard`, `dedupVariants`, `TOKEN_ALIASES` |
| `pipeline/cluster.py` | `cluster.js` | lane/facets vocabularies, `facets`, `lane`, `topicTokens`, representative+complete-link clustering, `clusterLabel`, `clusterKeywords`, `attachVariants`, `aggregateMetadata` |
| `pipeline/score.py` | `score.js` | `BLOCKING_FLAGS`, `flagRecord`, `populationStats`, `scoreRecord`, `scoreAndFlagAll`, `scoreCluster`, `scoreAllClusters` |
| `pipeline/pipeline.py` post-collection | `pipeline.js` | cumulative metrics, weighted averages, dedup→cluster→attach→score→score-clusters→market scoring order; **collection loops intentionally replaced by `DEC-KI-005/006`** |
| `pipeline/output.py` | `export.js` | exact keyword/cluster CSV columns+order and JSON serializers; **delete `raw_ref`; CSV returns string/bytes, no file writes** |

### 4.2 Parity constraints (`DEC-KI-010/011`, SCN-KI-010)

- Statement-for-statement formulas, constants, input order, tie-breaks,
  rounding sites, field names, and comparisons identical to Python.
- Exact equality for strings/booleans/nulls/arrays/membership/IDs/order/
  integer scores/rounded public numbers/flags/recommendations.
- Intermediate unrounded IEEE-754 values compare at absolute error ≤`1e-12`.
- Exported CSV exact UTF-8 bytes with LF line endings.
- `raw_ref`, `items[].key` aliases, fallback field paths, and file/disk writes
  are removed; production never invokes Python (`EXC-KI-001/002/006`).
- BLAKE2s six-byte stable IDs: `blake2s(data, { dkLen: 6 })` hex via
  `@noble/hashes/blake2.js` (`DEC-KI-002`).

### 4.3 Bounds and instrumentability (`DEC-KI-024`)

- anchor screening `k ≤ 300`; final calculation `k ≤ 200`.
- Every `O(k²)` loop is explicit and counts operations (Jaccard pairs,
  clustering comparisons); exposed via counters so `SCN-KI-010/013` measure
  them.
- Result object ≤32 MiB.
- Dependencies: Node ESM, Zod 4.4.3, `@noble/hashes@2.2.0` only. No new package
  (`package_changes` is prohibited).

### 4.4 Deliverable tests (owned)

- `test/fixtures/keyword-intelligence/parity-input-v1.json` — sanitized
  normalized overview fixture covering every intent, alias, tie, cluster,
  market, missing metric, history, and seasonality partition.
- `test/fixtures/keyword-intelligence/parity-output-v1.json` — golden Node
  output derived from Python oracle; byte-exact CSV columns included.
- `test/keyword-intelligence-parity.test.js` — one fixture per function
  boundary; exact golden Node/Python equality (`DEC-KI-011`); shuffled/tie/
  boundary cases; deterministic-seed generated 300-candidate anchor and
  200-keyword final tests with operation counters.
- **Negative control:** perturb one weight/alias/tie-break; golden test must
  fail.

---

## 5. Task T2 — Seed/selection/conflict/query engine (A4 lines 248–282)

**Task:** seed/selection parsers, default order, edits, full-list conflict
components/canonical suggestions, and lane query mapper.

**Requirements/decisions:** `REQ-KI-001`, `006`–`011`; `DEC-KI-003`, `013`–`016`.

### 5.1 Functions and behavior

| Function | Contract (from `DEC-KI-003/013/014/015/016`, A4 T2 item 5) |
|---|---|
| `normalizeSeeds(input)` | strict array 1–5; NFKC, trim, collapse Unicode whitespace; 1–100 code points; reject control chars and case-insensitive duplicates; preserve order (`DEC-KI-003`) |
| `createDefaultSelection(result)` | candidate order = recommended desc → opportunity desc (null last) → volume desc (null last) → normalized keyword asc → item ID asc; default = all recommended, truncated to first 100 if needed (`DEC-KI-013`) |
| `validateSelectionDraft(items)` | strict `SelectionItem` (`DEC-KI-014`); 0–200 items; keyword ≤160 code points; rejects malformed |
| `analyzeSelectionConflicts(items)` | all `n(n-1)/2` pairs; Python-equivalent `compact_signature`, token aliases, singularization, stop-stripping, Jaccard ≥0.88; connected components in input order; canonical rank (source canonical → opportunity → volume → shortest → lowercase → item ID); strict `{conflictId,itemIds,pairs,canonicalItemId}` (`DEC-KI-015`); 19,900 comparisons at 200 |
| `mapSelectionToQueries(items)` | lane-aware: `category_discovery` → `site:myshopify.com/products <keyword>`; `store_discovery`/`local_discovery`/`brand_competitor` → `site:myshopify.com <keyword>` (`REQ-KI-011`) |
| `validateResearchBackedQueries(items, queries)` | 1–100 rows; unique sequences; exact persisted item-ID set; NFKC/trim/collapse phrase ≤160 code points, 1–12 alphanumeric-token words, no control/quote/newline/operator punctuation; full query ≤200 code points; one leading lowercase `site:` prefix, no other operator tokens; relevance = ≥1 normalized non-stop token shared with keyword or any seed (`DEC-KI-016`) |

All functions are pure, accept/return plain immutable data, and return strict
success/error unions. `selectionItemId` is imported from the W1
`repository.js` (`ksi_` + 12 lowercase hex BLAKE2s, `DEC-KI-002`).

### 5.2 Bounds

max seeds `5`, seed `100`, keyword `160`, draft `200`, retained/query `100`,
19,900 comparisons, query `200` code points / `12` words.

### 5.3 Deliverable tests (owned)

- `test/fixtures/keyword-intelligence/selection-cases-v1.json` — 0/1/5/6 seeds;
  Unicode/control/duplicates; recommended 0/1/100/101; drafts 0/1/100/101/200/
  201; exact/near/transitive/unique conflicts; all four lanes; product/non-
  product grammar and malicious operators.
- `test/keyword-intelligence-selection.test.js` — boundaries above;
  deterministic default; conflict components; 200 unique pass.
- `test/keyword-intelligence-query-mapper.test.js` — lane mapping, grammar,
  relevance, set-equality, malicious operators.
- **Negative control:** skip one pair in `analyzeSelectionConflicts`; the
  maximum-conflict fixture must fail.

---

## 6. Read-only sources consulted (for the implementer)

- `KeywordSearchVolume/config.yaml`
- `KeywordSearchVolume/pipeline/{config,models,normalize,intent,dedup,cluster,
  score,pipeline,output,client}.py`
- `KeywordSearchVolume/tests/{fixtures.py,test_normalize.py,test_intent.py,
  test_dedup.py,test_cluster.py,test_score.py,test_markets.py,
  test_seed_research.py}`
- `KeywordSearchVolume/dashboard/index.html` (selection/sort behavior)

No file in `KeywordSearchVolume/` may be modified, imported by runtime, or
copied into `email_scraper/` except the sanitized golden fixtures named in A4.

---

## 7. Verification (V1–V4)

| ID | Action |
|---|---|
| `KI-W2-V1` | Execute `SCN-KI-003` (seed/API partitions), `SCN-KI-010` (Python/Node parity), `SCN-KI-011` (selection/conflict boundaries), `SCN-KI-014` (product/non-product query review) with negative controls |
| `KI-W2-V2` | Run focused Node tests (`node --test test/keyword-intelligence-parity.test.js test/keyword-intelligence-selection.test.js test/keyword-intelligence-query-mapper.test.js`) and the development-only Python golden oracle; prove no production script imports/invokes Python (`rg` negative search) |
| `KI-W2-V3` | Measure the 300-candidate anchor path, 200-keyword nine-market path, 200-item duplicate path, result bytes, and exact operation counters against `DEC-KI-024`; record runtime/memory without resource inflation |
| `KI-W2-V4` | Assert fixtures/exports contain no raw reference/body/credential/private field (`npm run check:secrets`), and unknown payload fields fail strict parsing |

---

## 8. Handoff (H1–H6)

1. `H1` Record changed files/symbols (must equal the A4 write scope).
2. `H2` Record commands, outcomes, scenarios, skipped checks.
3. `H3` `git diff` matches authorized scope exactly.
4. `H4` No successor (`KI-W3`) or prohibited action started.
5. `H5` Append evidence to A6; CAS A5 to `AWAITING_REVIEW`.
6. `H6` Stop; do not begin `KI-W3`.

---

## 9. Environment prerequisites / gaps to resolve before execution

1. **A5 assignment:** parent must accept `KI-W1`, rehash A1/A4, and record a
   one-window `KI-W2` assignment before any edit.
2. **Python golden oracle deps:** the development-only oracle needs
   `python-dotenv` (+ optionally `pytest`) to import `pipeline.config`; they are
   not currently installed in the standalone venv (verified: `dotenv` and
   `pytest` missing). Installing them is a **development-environment change**,
   not a package change to `email_scraper/`; the parent must approve any venv
   install before the oracle runs. Alternative: the oracle harness loads
   `config.yaml` directly via `yaml` and calls the pure functions with a
   hand-built config object, avoiding `dotenv` import — this is the preferred
   zero-install path and must be decided before execution.
3. **Fixture materialization:** `parity-input-v1.json`, `parity-output-v1.json`,
   `selection-cases-v1.json` do not yet exist; they are authored from the Python
   oracle + `SRC-KI-008/010` and must not contain provider bodies or seeds beyond
   the sanitized golden set.
4. **Dirty state:** coordination root has uncommitted A4/A5/docs and untracked
   package artifacts; backend is clean. `KI-W2-P4` records this; the implementer
   never stages/commits/repairs the coordination root (`AUTH-KI-006`).

---

## 10. Execution sequence (once assigned)

1. Record `KI-W2-P1…P4` evidence.
2. Implement `schemas.js` (strict Zod config/result/selection schemas) — consumed
   by every other module.
3. Implement `config.js` (immutable v1 snapshot) — consumed by all pure modules.
4. Implement pure modules in dependency order: `intent.js` → `normalize.js` →
   `dedup.js` → `cluster.js` → `score.js` → `pipeline.js` → `export.js`.
5. Implement `selection.js` and `query-mapper.js` (T2).
6. Materialize golden fixtures via the development-only Python oracle.
7. Write the three owned test files; run parity + selection + query tests.
8. Run V1–V4 verification incl. negative controls and `check:secrets`.
9. Hand off (H1–H6), stop.