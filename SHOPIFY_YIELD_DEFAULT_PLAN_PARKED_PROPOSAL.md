# Shopify Yield Default-Plan Ranking — Parked Proposal

**Status:** `PARKED`  
**Date:** 2026-09-01  
**Role of this file:** product note only. It is not A1–A8, not assignment
authority, and not a contract revision. Do not start a window, edit the keyword
intelligence package, or add a research Google stage from this file.

Revisit only after real users exist and market testing shows that DataForSEO-only
default selection still wastes runs on phrases that do not retrieve independent
Shopify merchants. Until then, leave the current v2 research path unchanged.

Related shipped work (not this proposal): retailer phrase/misspelling match and
v2 200-shortlist demotion in `REQ-KI-004` / `REQ-KI-024` / `DEC-KI-062`. Related
context, not authority: `grokplan.md`.

---

## 1. Problem

Keyword research never sees Shopify. It scores DataForSEO volume, CPC, intent,
and seed overlap, then default-selects one phrase per cluster.

Shopify yield is measured later: after the owner retains 1–100 keywords, each
maps to one `site:myshopify.com` query, and query review already probes Custom
Search. That probe already stores `uniqueHosts`, `relevantRatio`,
`relevantResults`, and `baseScore`.

Research-backed confirm currently treats almost every probe as fine (1 host is
enough; 0 relevant results is enough). A high-volume empty phrase can still
become a default query and a confirmed run.

The product job is merchant retrieval, not SEO opportunity. Yield ranking would
exist to put phrases that actually return independent `.myshopify.com` hosts
into the default plan.

---

## 2. What “Shopify yield” means here

Of at most ten Custom Search hits for the mapped query: how many distinct
independent `.myshopify.com` hosts appeared, and how many of those hits match
the query.

It is not “a store exists.” It is not retailer detection. Classification already
owns Walmart-style leakage. Yield owns emptiness and overlap.

---

## 3. The version that would be worth building

Probe **during research**, after nine-market overviews and **before**
`createDefaultSelection`. Map candidate default rows the same way query review
already does (`site:myshopify.com/products …` vs `site:myshopify.com …`), run
the existing CSE probe, and fold `uniqueHosts` / `relevantRatio` into default
selection. Empty or near-empty phrases lose the default slot; the next clean
phrase in the cluster takes it. Rows stay in the table; they are not deleted,
and they are not auto-replaced after the owner retains them.

Confirm-time probes already key on query fingerprint and freshness, so retained
phrases should not be charged again. Net new Google cost is probing phrases the
owner never keeps.

Do not probe the full 1–300 expansion set. The useful set is either the cluster
representatives that would become the default 1–100, or the 200 shortlist if
the table itself should be labeled.

A later privacy-safe prior (`compact signature → {hostCount, relevantRatio,
sampleSize, asOf}`) is optional follow-on after live numbers exist. First-time
niches would still need a probe. It does not replace the research-time CSE
step for a new seed.

---

## 4. Rejected half-measure

Confirm-time labels only (`low_shopify_yield`, require explicit keep) do **not**
rank the default plan. By then recommendations, the 1–100 snapshot, and a run
already exist. That path only saves downstream identity/traffic/lead spend. It
was discussed and parked with the rest: without a research-time probe there is
no point.

Also rejected:

- Auto-replacing a weak retained keyword with another phrase (`REQ-KI-010`,
  `DEC-KI-016`).
- Ranking on “a `.myshopify.com` host exists” alone.
- CSE during research to rewrite the table after the user has retained rows.
- Treating Google hostnames as shops.

---

## 5. Cost and worker boundaries

**Google cost increases.** Research would start calling Custom Search. Today CSE
runs only after retain-and-confirm. Extra spend is on the order of tens to ~200
queries per research, not thousands. Exact dollars depend on Programmable Search
quota.

**Lead worker input does not change.** One lead task remains one stable domain
that needs lead work.

**Discovery worker is not skipped.** CSE answers “does this keyword find Shopify
URLs in Google?” Discovery still fetches the storefront, resolves custom domain
vs `.myshopify.com`, runs `stableShopIdentity()`, persists `Shop` / `RunStore`,
and creates lead tasks. The only Google skip already intended is: do not search
again when `probeResults` are already persisted.

The change would live in **keyword research**, which today is DataForSEO-only
(`expansion` → `anchor_screen` → `market_overview`). Yield needs a Google step
after overviews and before default selection: new research stage and/or message
type, S3 probe artifacts, yield fields on the research result, and Google
credentials on the research worker.

That is a contract change: extra CSE quota, a locked numeric floor (hosts /
ratio / relevant count), and an explicit exception to `EXC-KI-003` (no second
research step). It is larger than the retailer matcher.

---

## 6. Revisit trigger

Unpark only when all of the following are true:

1. Real users are running research-backed discovery, not only internal Clothing
   fixtures.
2. Market testing shows default queries still retrieve empty or overlapping CSE
   pages often enough to justify extra Google spend in research.
3. A parent writes a decision-complete package (floor, probed set, reuse at
   confirm, no lead/discovery message rewrite) and assigns a new window ID.
   Never implement from this note.

The numeric floor is still unwritten. Do not guess it here.
