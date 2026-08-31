# KI-W10 Lead-Finding Recommendation — Decomposition Draft

**Status:** `DRAFT / NOT ASSIGNABLE`  
**Date:** 2026-08-31  
**Role of this file:** working decomposition from parent/window-agent review. It is **not** A1–A8, **not** an assignment, and **not** authority to edit source.

Current `KEYWORD_INTELLIGENCE_PRODUCT_CONTRACT.md` (`KI-PC-2`) still forbids this work (`EXC-KI-002`, `REQ-KI-004` Python parity). The eight new/revised artifacts do not exist. Literals in the lock table are proposed decisions, not an assigned `A3`.

A window agent that started `cluster.js` from this file would be inventing the retailer list, junk rules, score formula, and `contractVersion` bump.

Related context (not execution authority): `grokplan.md`, `KEYWORD_INTELLIGENCE_LOGIC_AUDIT_2026-08-26.md`.

Standards that govern a future assignable package:

- `PROJECT_AGNOSTIC_DECISION_COMPLETE_CHECKLIST_AUTHORING_STANDARD.md`
- `PROJECT_AGNOSTIC_WINDOW_AGENT_SUBWINDOW_AUTHORING_STANDARD.md`

---

## 1. What this is

One new **parent implementation window** (`KI-W10`, never reuse `KI-W1`–`KI-W9`) after a **contract revision** (`KI-PC-3`). The five product changes are one capability: **lead-finding default query plan**. They share `cluster.js` / `pipeline.js` / `config.js`, so five parallel parent windows would fight over the same files. Parallelism belongs in **single-file sub-window waves**.

```text
parent: revise A1/A3/A4 (KI-PC-3)     ← not implementation
     → KI-W10 lead-finding recommendation v2
          window agent → one-file leaves in waves
               → KI-W10-I001 integration
                    → parent acceptance
                    → STOP (no G14, no AWS, no Luna, no probe/storefront)
```

The five product changes (impact order; build order is classify → cluster → rank → retain/flag → default-select):

1. Default-select one query per concept (`recommended` = default query plan).
2. Delete clothing ontology; classify intent, retailers, junk.
3. Replace clustering with dynamic concept keys (lane + leftover content tokens).
4. Rank for Shopify-lead yield, not SEO opportunity.
5. Flag junk/informational; do not delete informational at the US shortlist; never default-select them; fix canonical sort.

Parked (not this window): US expansion/shortlist topology, nine-market overviews as dashboard columns, nine-way Google CSE `gl`, Luna `/products` vs root durability, probe vs storefront acceptance.

---

## 2. Proposed locks (requester must ratify)

These are the choices an implementer must not make. If any row is rejected, the DAG stays draft.

| ID | Lock |
|---|---|
| Version | New researches: config `schemaVersion: "keyword-research-config-v2"`, result `contractVersion: 2`, summary `schemaVersion: 4`. Persisted v1 researches stay readable as v1. No silent upgrade. |
| Facets wire shape | Keep `{audience, category, channel, fit, modifier}`. Fill **only** `channel` (`online` / `store` / `local`). Others always `[]`. |
| Lanes | Same four enums. Membership is closed-class, not clothing. |
| Local | Phrase operators only: `near me`, `close to me`, `closest to me`, `closest`, `nearest`, `nearby`. **Remove** `nyc` / `new york` / `\bin [a-z]+\b`. |
| Store tokens | `shop`, `shops`, `store`, `stores`, `boutique`, `boutiques`, `outlet`, `outlets`, `retailer`, `retailers` |
| Retailer → `brand_competitor` | Frozen lowercase token set: `amazon`, `walmart`, `target`, `ebay`, `etsy`, `aliexpress`, `alibaba`, `shein`, `temu`, `costco`, `ikea`, `bestbuy`, `macys`, `kohls`, `nordstrom`, `wayfair`, `wish`, `overstock`, `rakuten`, `flipkart`, `homedepot`, `lowes` |
| Cluster key | `lane + sorted content tokens`. Content = tokens after folding local/store operators, stripping existing `dedup.stripTokens`, stripping commercial modifiers from the **key only**. Exact key match = cluster. Remainder: complete-link Jaccard **≥ 0.80** on that signature, same lane only. Keys are **dynamic** (computed from the phrase in that research). They are not gathered from Google, DataForSEO, or a niche glossary. |
| Cluster label | Representative keyword (highest lead score, then volume, then shortest, then lexical). No generated “women's clothing stores”. |
| `recommended` | `true` only for the **one default representative per cluster**. Not `score ≥ 55`. |
| Default selection | Active, non-merged rows, no blocking flag, **exactly one row per `clusterId`**, sort representatives by lead score desc, cap **100**. No second member. |
| Lead score (0–100) | Stable, not vs max-in-run. Weights: volume `0.30`, commercialIntent `0.25`, cpc `0.20`, trend `0.15`, seedOverlap `0.10`. **Zero** inverse difficulty / inverse competition. `volNorm = log10(1+vol) / log10(1+1_000_000)`. `cpcNorm = min(cpc, 20) / 20`. `seedOverlap` = Jaccard(content(keyword), union content(seeds)). |
| Blocking flags (not recommended, still visible) | existing: `too_little_traffic`, `too_broad`, `declining_traffic`, `brand_competitor`; plus `local_intent`, `junk_quality`, `informational`. |
| Junk | `junk_quality` if: keyword starts with a digit, **or** consecutive duplicate tokens, **or** more than two non-letter/number/space/`'`/`-` characters. |
| Shortlist | **Do not** drop informational before the 200. Sort: non-informational first, then lead score, volume, keyword. Informational still cannot be default-selected. |
| Canonical conflict | Calculated before manual; **higher** opportunity; **higher** volume; shorter; lexical; itemId. |
| US shortlist / 9 markets / CSE / Luna / storefront | Unchanged. Out of `KI-W10`. |
| Python parity | v1 golden remains a **v1 snapshot test** of the old function behind an explicit v1 helper, or is retired as oracle for `computeResearchResult`. v2 has a new fixture. Parity-green is not acceptance. |
| Frontend | Duplicate the frozen operator/retailer lists in `view-model.ts` (frontend cannot import backend config). Same literals as `config.js`. |
| `score.js` vs `recommended` | `score.js` sets score and flags only. `pipeline.js` sets `recommended` after default-plan construction. |
| Junk knobs | Junk rules are code in `score.js`, not config. Retailer/local lists **are** config. |
| Flag name | Keep `informational_dropped` as the flag string so dashboard filters still match; it no longer means “deleted from the result”. |

Closed-class cluster-key commercial modifiers (strip from key only, not from the stored keyword): `buy`, `buying`, `bought`, `order`, `ordering`, `purchase`, `cheap`, `cheapest`, `affordable`, `sale`, `sales`, `discount`, `discounts`, `deal`, `deals`, `clearance`, `best`, `top`, `new`, `arrivals`, `arrival`, `online`, `price`, `prices`, `cost`, `under`, `review`, `reviews`, `vs`, `comparison`.

---

## 3. Parent window `KI-W10`

```yaml
window_id: KI-W10
objective: New researches emit a niche-agnostic, one-representative-per-concept default query plan; v1 snapshots remain readable.
depends_on: [KI-PC-3 authoring READY]
assigned_agent_policy: one_window
may_start_successor: false
successor: STOP
authorized_actions: [local_source_edits, local_unit_tests]
prohibited_actions:
  [provider_calls, AWS_operations, production_database_writes, commits,
   frontend_edits_outside_listed_paths]
```

### 3.1 Planned write set (no globs)

| Path | Op | Why |
|---|---|---|
| `email_scraper/src/keyword-intelligence/config.js` | MODIFY | v2 snapshot, lists, weights, flags |
| `email_scraper/src/keyword-intelligence/cluster.js` | MODIFY | kill clothing; concept keys |
| `email_scraper/src/keyword-intelligence/intent.js` | MODIFY | stop boosting `near me` as commercial |
| `email_scraper/src/keyword-intelligence/score.js` | MODIFY | lead score + new flags; do not set `recommended` |
| `email_scraper/src/keyword-intelligence/selection.js` | MODIFY | one per cluster; canonical sort |
| `email_scraper/src/keyword-intelligence/pipeline.js` | MODIFY | wire order; summary counts; contractVersion 2 |
| `email_scraper/src/keyword-intelligence/schemas.js` | MODIFY | contractVersion 2, summary v4 |
| `email_scraper/src/aws-pipeline/keyword-intelligence/service.js` | MODIFY | shortlist comparator; no informational delete |
| `frontend/lib/keyword-intelligence-types.ts` | MODIFY | `contractVersion: 1 \| 2` |
| `frontend/lib/keyword-intelligence-validation.ts` | MODIFY | accept v1 and v2 |
| `frontend/lib/keyword-intelligence-view-model.ts` | MODIFY | replace duplicated clothing classifier |
| `email_scraper/test/keyword-intelligence-parity.test.js` | MODIFY | v1 oracle isolation |
| `email_scraper/test/keyword-intelligence-selection.test.js` | MODIFY | default plan + canonical |
| `email_scraper/test/keyword-intelligence-worker-flow.test.js` | MODIFY | shortlist retains informational |
| `email_scraper/test/keyword-intelligence-lead-finding.test.js` | CREATE | classify/cluster/score cases |
| `email_scraper/test/fixtures/keyword-intelligence/lead-finding-cases-v2.json` | CREATE | literal expected members |
| `frontend/test/keyword-intelligence-components.test.ts` | MODIFY | classifier + contract 2 |
| `frontend/test/keyword-intelligence-api.test.ts` | MODIFY | contract 2 parse |

**Do not touch:** `dedup.js` (0.88 stays), `query-mapper.js`, `query-intent-classifier.js`, AWS worker durability, `storefront-validator.js`.

**Shared-file note:** `cluster.js` owns classification **and** clustering. That is one leaf, not two parallel leaves.

Frontend **is** in scope for this window (the dashboard duplicates the clothing classifier in `view-model.ts`). This is not a G14/G15 AWS window.

---

## 4. Leaf DAG (window-agent `S1`)

Each box is **one writable file**. Parallel only inside a wave. File disjointness alone is not parallel authority; members of a wave must not share outputs, fixtures they write, or other mutable resources.

```text
WAVE-1 (serial)
  KI-W10-S001  config.js

WAVE-2 (parallel — all read frozen config only)
  KI-W10-S002  cluster.js
  KI-W10-S003  intent.js
  KI-W10-S004  score.js
  KI-W10-S005  schemas.js
  KI-W10-S006  frontend/lib/keyword-intelligence-types.ts
  KI-W10-S007  lead-finding-cases-v2.json   (CREATE fixture)

WAVE-3 (parallel; consume WAVE-2 interfaces)
  KI-W10-S008  selection.js
  KI-W10-S009  frontend/lib/keyword-intelligence-validation.ts
  KI-W10-S010  frontend/lib/keyword-intelligence-view-model.ts

WAVE-4
  KI-W10-S011  pipeline.js

WAVE-5
  KI-W10-S012  service.js

WAVE-6 (parallel tests; no shared writable fixture)
  KI-W10-S013  keyword-intelligence-lead-finding.test.js   (CREATE)
  KI-W10-S014  keyword-intelligence-parity.test.js
  KI-W10-S015  keyword-intelligence-selection.test.js
  KI-W10-S016  keyword-intelligence-worker-flow.test.js
  KI-W10-S017  frontend/test/keyword-intelligence-components.test.ts
  KI-W10-S018  frontend/test/keyword-intelligence-api.test.ts

WAVE-7
  KI-W10-I001  integration assessment (window agent, write NONE)
```

S007 (fixture) is in WAVE-2 so S013 can register cases without waiting for pipeline.

**Expected intermediate failure:** production files in WAVE-2 may fail old parity until S014. That failure is owned by S014. Do not treat `npm test` as acceptance before I001.

Why WAVE-2 is actually parallel: `cluster.js` does not import `score.js`; `score.js` does not import `cluster.js`; `intent.js` is standalone; `schemas.js` is Zod only; frontend `types.ts` does not import backend.

Why `pipeline.js` is alone: it is the only assembler (`clusterKeywords` → `scoreAndFlagAll` → `createDefaultSelection` → stamp `recommended`).

### 4.1 What cannot be parallel

- Two leaves on `cluster.js`
- `pipeline.js` before cluster/score/selection
- `service.js` before pipeline (shortlist uses `computeResearchResult`)
- Tests that import `computeResearchResult` before S011
- Integration assessment in parallel with any leaf

---

## 5. Exact code changes per leaf

### S001 `email_scraper/src/keyword-intelligence/config.js`

Add v2 snapshot. Keep v1 export for reading old snapshots. Strict fields:

- `classification.localPhrases`, `.storeTokens`, `.retailerTokens`, `.clusterKeyStripTokens`
- `scoring.weights` as locked; **omit** `recommendThreshold` from v2 schema so it cannot be used
- `scoring.volumeLogCap: 1000000`, `scoring.cpcCap: 20`
- `clustering.method: "concept_key"`, `similarityThreshold: 0.80`
- set `minClusterSize: 1`, `clusterLabelStrategy: "representative_keyword"` to match real behavior

### S002 `email_scraper/src/keyword-intelligence/cluster.js`

Delete `AUDIENCE`, `CATEGORY_TERMS`, `FIT_TERMS`, `MODIFIER_TERMS`, `GENERIC` clothing set, apparel `clusterLabel`.

`lane()` order:

1. local phrase in keyword → `local_discovery`
2. any retailer token → `brand_competitor`
3. `mainIntent === navigational` **and** no store token **and** no local → `brand_competitor`
4. store token → `store_discovery`
5. else → `category_discovery`

`facets()`: channel only.

`conceptKey(record)`: tokenize, replace local/store with markers, drop strip + clusterKeyStrip, sort, join `lane + "\u0000" + tokens.join(" ")`.

`clusterKeywords`: partition by lane; union-find exact `conceptKey`; then within lane, complete-link Jaccard ≥ 0.80 on those token sets for leftovers; `clusterId = stableId("c", key)` using representative key; label = representative keyword.

`classifyKeywordForSelection`: same `lane`/`facets` (API/manual edits).

### S003 `email_scraper/src/keyword-intelligence/intent.js`

Remove `near me` from commercial-modifier boost (it stays a local operator in config). Informational detection unchanged.

### S004 `email_scraper/src/keyword-intelligence/score.js`

`flagRecord`: add `local_intent` if `lane === local_discovery`; `junk_quality` per locked rules; keep `informational_dropped` as the flag name.

`scoreRecord`: stable norms; **do not set `recommended`**.

`BLOCKING_FLAGS` used by pipeline when stamping recommended.

`populationStats` unused for recommend; remove from v2 path. Cluster opportunity uses `adjustedClusterVolume` and the same stable volume transform. `recommendedForStoreDiscovery` stamped later from members.

### S005 `email_scraper/src/keyword-intelligence/schemas.js`

Discriminated: parse `contractVersion` 1 or 2. v2 summary `schemaVersion: 4`. Do not require new facet keys.

### S006 `frontend/lib/keyword-intelligence-types.ts`

`contractVersion: 1 | 2`.

### S007 `email_scraper/test/fixtures/keyword-intelligence/lead-finding-cases-v2.json`

CREATE. Literal expected members for every coverage case in Section 6. No “similar” placeholders.

### S008 `email_scraper/src/keyword-intelligence/selection.js`

`createDefaultSelection(rows)`:

1. `mergedInto` null
2. drop blocking flags
3. group by `clusterId` (if missing, `selectionItemId("calculated", keyword)` as synthetic id — should not happen after pipeline)
4. one winner per group
5. sort winners by score, volume, length; slice 0..100

`canonicalItem`: compare so **larger** score/volume wins (fix current ascending sort).

### S009 `frontend/lib/keyword-intelligence-validation.ts`

Accept `contractVersion` 1 and 2.

### S010 `frontend/lib/keyword-intelligence-view-model.ts`

Delete clothing maps (`AUDIENCE`, `CATEGORY_TERMS`, `FIT_TERMS`, `MODIFIER_TERMS`, `KNOWN_RETAIL`). Copy locked lists from S001/A3. Same `lane`/`facets` rules as backend. Empty audience filters stay; no UI redesign.

### S011 `email_scraper/src/keyword-intelligence/pipeline.js`

Order: cumulative metrics → dedup → `clusterKeywords` → `scoreAndFlagAll` → `createDefaultSelection` on keyword rows → set `row.recommended` from the returned itemIds → cluster `recommendedForStoreDiscovery` if any member recommended → `informationalDropped` = unique active keywords with that flag (not market occurrences) → emit contractVersion 2.

### S012 `email_scraper/src/aws-pipeline/keyword-intelligence/service.js`

`aggregateAnchor`: delete `usable = active.filter(!isInformational)`. Sort with `shortlistComparator` extended: informational last, then recommended, then score, volume, keyword. Truncate 200. Informational can occupy remaining slots only if fewer than 200 non-informational exist.

US screen already calls `computeResearchResult`; after v2 that path clusters/scores and stamps `recommended`.

### S013–S018 tests

- S013 CREATE `keyword-intelligence-lead-finding.test.js` registering Section 6 cases against cluster/score/selection/pipeline as applicable.
- S014 isolate v1 golden; stop using it as oracle for v2 `computeResearchResult`.
- S015 default plan + canonical order.
- S016 shortlist retains informational.
- S017–S018 frontend classifier + contract 2 parse.

---

## 6. Coverage (minimum; full E6 matrix is part of A4 authoring)

Literal cases in `lead-finding-cases-v2.json`:

| Case | Input | Oracle |
|---|---|---|
| `CASE-KR-L-001` | `pickleball store` | lane `store_discovery`, not brand |
| `CASE-KR-L-002` | `best ceramic mugs online` | lane `category_discovery` |
| `CASE-KR-L-003` | `walmart women's clothes clearance` | `brand_competitor` + blocking |
| `CASE-KR-L-004` | five Clothing near-me variants | one `clusterId`, one `recommended` |
| `CASE-KR-L-005` | `pickleball paddles` vs `buy pickleball paddles online` | same cluster, one recommended |
| `CASE-KR-L-006` | `4.12 4 clothing store` | `junk_quality`, not recommended |
| `CASE-KR-L-007` | informational `how to …` | in result + shortlist-eligible, not default |
| `CASE-KR-L-008` | canonical two calculated rows scores 10 vs 90 | suggestion is 90 |
| `CASE-KR-L-009` | same metrics, weak vs strong peer | **same** lead score |
| `CASE-KR-L-010` | v1 stored result | still parses; not rewritten |

Negative controls: reintroduce clothing `unknown+store → brand` and `CASE-KR-L-001` must fail; sort canonical ascending and `CASE-KR-L-008` must fail.

---

## 7. Parent-standard closure (as of this draft)

1. **`DRAFT / NOT ASSIGNABLE`**
2. Eight artifacts: **not created** (would revise existing `KEYWORD_INTELLIGENCE_*` + `ACTIVE_EXECUTION_STATE.md`)
3. Authorized assignment: **none**
4. Authoring checkboxes: **unchecked** (package absent)
5. Payload unknowns: **0 blocking provider payloads** (this window is local algorithms). Historical v1 result payload is **observed**. v2 result shape is **DECIDED** only after A3.
6. Coverage: 10 named cases above; **unmapped until A4 E6 matrix**
7. Falsification: not run (no A4 lint yet)
8. Predictable gates: requester ratify locks; no AWS/paid; frontend **is** in scope
9. Blockers:
   - `KI-PC-2` `EXC-KI-002` still forbids the work
   - closed lists/weights/version bump not in `A3`
   - Python-parity oracle vs v2 not decided in the ledger
   - no `A5` assignment / standard pin

---

## 8. Next parent action

If the lock table in Section 2 is ratified (especially retailer list, junk rules, weights, and `contractVersion: 2`):

1. Author `KI-PC-3` (A1) + A3/A4/A8; changelog A7; evidence A6.
2. Pin hashes in `A5`.
3. Window agent emits `S1`/`S2`/`S3` with starting file digests.
4. Assign **S001 `config.js` only**.

Do not begin implementation from this draft.
