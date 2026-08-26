# Landing Keyword Research Authentication — Decision-Complete Execution Plan

## 0. Status and authority

**Specification status:** `DECISION-COMPLETE SUCCESSOR SPECIFICATION / NOT THE
CURRENT ACTIVE ASSIGNMENT`

**Prepared:** 26 August 2026, Asia/Kolkata.

This document fixes the complete implementation contract for replacing the
public landing page's legacy direct-run submission with keyword research while
preserving the landing design and the existing sign-up/sign-in continuation
experience.

It is intentionally not a second live execution state. At authoring time,
`ACTIVE_EXECUTION_STATE.md` assigns only `KI-W8-C201`, stops after that
subwindow, and explicitly prohibits frontend, schema, package, and unrelated
source edits. Before this successor work is assigned, the parent must adopt
this specification into the existing eight-artifact keyword-intelligence
package, append the corresponding changelog/evidence/traceability entries,
rehash the package, and create a new assignment after the current stop point.
That adoption gate is an authority/scheduling gate; no implementation choice is
left open by this document.

The applicable standard is
`PROJECT_AGNOSTIC_DECISION_COMPLETE_CHECKLIST_AUTHORING_STANDARD.md`, SHA-256
`cda352017e75c0d11f6797d9fbe108b4365508cd38b0e92365cfb523ede32848`.

The current package revisions verified during authoring are:

| Artifact | Revision |
|---|---|
| `KEYWORD_INTELLIGENCE_PRODUCT_CONTRACT.md` | `8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c` |
| `KEYWORD_INTELLIGENCE_DISCOVERY_DOSSIER.md` | `3a6b294cc561556d0e3d92572121bc8cc529470866fba5bad8f78cf816310470` |
| `KEYWORD_INTELLIGENCE_DECISION_LEDGER.md` | `32ae437a3c755d370e6d78ff4ba33badec0fec504f2045339303c3c9e9ee044e` |
| `KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md` | `25c33528a7a2059aedb0ed850de8e83b49ca5a08b02ee8d2f64621090780e1a6` |
| `KEYWORD_INTELLIGENCE_TRACEABILITY_INDEX.md` | `e89fe868823ba97a3c8877d79055bbc85d2593353add13c32b8a6c35a51e7d4b` |

The current product contract's `REQ-KI-001` covers signed-in creation only. The
successor package must add the anonymous-intent/authenticated-claim requirements
below without weakening owner-scoped research access or changing the keyword
worker contract.

## 1. Locked product outcome

### 1.1 Required behavior

- `LKAI-REQ-001` The public `/` page retains its existing hero, globe, lower
  marketing sections, responsive layout, form card structure, CSS class names,
  local CTA target `#start-discovery`, and suggestion-chip presentation.
- `LKAI-REQ-002` The landing form interprets its entered phrases as keyword
  research seeds, applying the existing keyword contract: one through five
  distinct NFKC-normalized phrases, whitespace collapsed, each 1–100 Unicode
  code points, compared case-insensitively with locale `en-US`.
- `LKAI-REQ-003` A signed-in landing submission calls the existing same-origin
  `POST /api/keyword-research`, creates one owner-scoped `KeywordResearch`,
  dispatches `keyword.initialize.v1`, and navigates to `/keywords/{researchId}`.
- `LKAI-REQ-004` A signed-out landing submission creates only one expiring,
  unowned `KeywordResearchIntent` and one opaque HTTP-only cookie. It creates no
  `KeywordResearch`, sends no SQS message, calls no keyword worker/provider, and
  incurs no provider cost.
- `LKAI-REQ-005` After successful sign-up or sign-in, the unchanged auth form
  continues to `/runs/continue`. That route atomically claims the pending
  keyword intent for the authenticated session owner, creates exactly one owned
  `KeywordResearch`, then and only then dispatches `keyword.initialize.v1` and
  navigates to `/keywords/{researchId}`.
- `LKAI-REQ-006` Same-owner claim retries return the identical research.
  Different-owner, missing, and expired claims are indistinguishable `404`
  outcomes and never create or expose research.
- `LKAI-REQ-007` The intent claim and research creation are one PostgreSQL
  transaction. Queue dispatch is a recovered boundary after commit; existing
  queued-research recovery remains the sole retry authority after dispatch
  failure or process death.
- `LKAI-REQ-008` Only the opaque intent ID is stored in the browser cookie.
  Seeds remain server-side, are never placed in a URL, client storage, logs,
  SQS, or auth-provider payload, and are scrubbed from the claimed intent in the
  successful claim transaction.
- `LKAI-REQ-009` At most one pending search-intent cookie is active. Creating a
  new keyword intent deletes the legacy run-intent cookie; creating a legacy
  run intent deletes the keyword-intent cookie. A successful continuation
  deletes both.
- `LKAI-REQ-010` Already-issued legacy run-intent cookies remain claimable via
  `/runs/continue` and navigate to `/runs/{runId}`. This compatibility path
  never authorizes keyword dispatch. The homepage stops producing legacy run
  intents when this change ships.
- `LKAI-REQ-011` Research retention, keyword selection, handoff into the Run
  pipeline, owner-scoped reads, worker contracts, queue configuration, provider
  behavior, and final lead pipeline remain unchanged.
- `LKAI-REQ-012` Unclaimed keyword intents expire exactly one hour after the
  backend acceptance timestamp and may be deleted only when
  `claimedResearchId IS NULL AND expiresAt <= now`. Claimed mappings persist for
  idempotent claim replay; their `seeds` value is the empty JSON array.
- `LKAI-REQ-013` Input and continuation payloads remain strict. Unknown keys,
  malformed IDs, invalid seed boundaries, unknown continuation discriminators,
  and extra response fields fail closed with existing safe JSON error handling.
- `LKAI-REQ-014` No production database migration, deployment, AWS mutation,
  queue operation, secret installation, new research submission, provider call,
  commit, or push is authorized by this planning document.

### 1.2 Explicit non-goals

- No redesign of `frontend/app/page.tsx`, `landing-sections.tsx`,
  `traffic-globe.tsx`, `globals.css`, or the lower marketing copy/layout.
- No auth-provider API, credential flow, middleware matcher, sign-up form, or
  sign-in form change. `AuthForm` continues to route successful auth to
  `/runs/continue`.
- No browser `localStorage`, `sessionStorage`, query-string, or readable cookie
  persistence for seeds.
- No modification of `keyword.initialize.v1`, SQS schemas, worker handlers,
  recovery messages, DataForSEO calls, Lambda infrastructure, or concurrency.
- No removal of `POST /api/runs`, backend `RunIntent`, legacy run history,
  query review, or run status/result APIs. “Retire the old landing flow” means
  the homepage no longer calls it; it does not mean deleting still-supported
  API/run machinery.
- No automatic worker dispatch merely because an anonymous intent exists.

## 2. Source-grounded evidence inventory

| Evidence ID | Classification | Observed fact and source |
|---|---|---|
| `LKAI-SRC-001` | OBSERVED | `frontend/app/page.tsx::Home` composes `LandingHeroCopy`, `RunForm`, and `LandingProcess`; the page shell is independent of form submit logic. |
| `LKAI-SRC-002` | OBSERVED | `frontend/components/run-form.tsx::RunForm` is the only frontend `RunForm` caller and currently posts `{shopTypes}` to `/api/runs`, then pushes `/runs/{runId}`. |
| `LKAI-SRC-003` | OBSERVED | `frontend/components/keyword-intelligence/research-form.tsx::ResearchForm` already creates keyword research and pushes `/keywords/{id}`; its private `parseKeywordLines` implements NFKC/collapse/dedup parsing. |
| `LKAI-SRC-004` | OBSERVED | `frontend/lib/client-api.ts::createKeywordResearch` strictly parses the existing research envelope from `POST /api/keyword-research`. |
| `LKAI-SRC-005` | OBSERVED | `frontend/app/api/keyword-research/route.ts::POST` validates the 32 KiB JSON body and 1–5 seeds, then currently requires authentication before proxying. |
| `LKAI-SRC-006` | OBSERVED | `frontend/app/api/runs/route.ts::POST` implements the current anonymous one-hour intent cookie pattern and safe `AUTHENTICATION_REQUIRED` continuation detail. |
| `LKAI-SRC-007` | OBSERVED | `frontend/app/api/run-intents/claim/route.ts::POST` reads the opaque legacy cookie, requires auth, proxies claim, and deletes on success/404. |
| `LKAI-SRC-008` | OBSERVED | `frontend/components/auth-form.tsx::AuthForm.submit` always routes successful sign-up/sign-in to `/runs/continue`; no change is necessary. |
| `LKAI-SRC-009` | OBSERVED | `frontend/components/run-continuation.tsx::RunContinuation` currently assumes every claim returns `StartRunResponse` and hardcodes `/runs/{runId}`. |
| `LKAI-SRC-010` | OBSERVED | `email_scraper/src/server.js` exposes authenticated keyword creation and legacy anonymous run-intent create/claim routes. |
| `LKAI-SRC-011` | OBSERVED | `email_scraper/src/keyword-intelligence/api.js::createResearch` durably creates research before calling `dispatchInitialize`; dispatch failure is swallowed because queued recovery owns retry. |
| `LKAI-SRC-012` | OBSERVED | `email_scraper/src/keyword-intelligence/repository.js::PrismaKeywordResearchRepository.create` writes an owner-scoped queued research; `_transaction` selects the isolated Prisma schema. |
| `LKAI-SRC-013` | OBSERVED | `email_scraper/src/aws-pipeline/keyword-intelligence/recovery.js::recoverKeywordWork` and repository `recover` reconstruct `keyword.initialize.v1` for queued research with no expansion stage. |
| `LKAI-SRC-014` | OBSERVED | `email_scraper/prisma/schema.prisma::RunIntent` stores anonymous legacy input and claim identity; no keyword-intent model exists. |
| `LKAI-SRC-015` | OBSERVED | Installed Next 16.2.12 docs require asynchronous `cookies()` and permit set/delete only in Route Handlers/Server Functions; the planned BFF cookie writes are Route Handler operations. |
| `LKAI-SRC-016` | OBSERVED | Repository searches find no other `RunForm` caller and no other direct frontend `POST /api/runs` creator. Run history/status/query routes remain reachable and required. |
| `LKAI-SRC-017` | OBSERVED | Both nested worktrees were clean during authoring; root owner-controlled coordination state was not staged, committed, repaired, moved, or reversed. |

No external payload or provider fact is required. All new payloads are internal
contracts selected below and must be frozen as sanitized fixtures before the
first implementation edit.

## 3. Locked decisions

| Decision ID | Locked choice | Evidence | Consequence |
|---|---|---|---|
| `LKAI-DEC-001` | Add a dedicated `KeywordResearchIntent` model; do not overload `RunIntent.normalizedShopTypes` or infer type from ID prefixes. | `LKAI-SRC-014` | Legacy and keyword intent semantics remain explicit and independently testable. |
| `LKAI-DEC-002` | Anonymous creation stores normalized seeds only; research config/markets are snapshotted at authenticated claim time. | `LKAI-SRC-006`, `011` | Anonymous users cannot reserve provider behavior or create worker work; claim matches current signed-in creation semantics. |
| `LKAI-DEC-003` | Claim CAS plus `KeywordResearch` insert is `SAME_ATOMIC_BOUNDARY` in `PrismaKeywordResearchRepository._transaction`. | `LKAI-SRC-012` | A failed research insert leaves the intent unclaimed; concurrent claim produces one owner/research. |
| `LKAI-DEC-004` | Post-commit initialize dispatch is `RECOVERED_BOUNDARY`; only `outcome:"created"` makes the immediate send, and existing queued recovery handles every missed send. | `LKAI-SRC-011`, `013` | Same-owner claim replay never amplifies immediate SQS sends and still converges after process death. |
| `LKAI-DEC-005` | Use a separate cookie `storesignal_pending_keyword_research_intent`; keep the current `storesignal_pending_run_intent` as legacy fallback. | `LKAI-SRC-006`, `007` | Cookie value remains opaque; no ambiguous database lookup is required. |
| `LKAI-DEC-006` | `POST /api/run-intents/claim` becomes an internal discriminated continuation BFF returning `legacy_run` or `keyword_research`; it never accepts a destination URL from a backend. | `LKAI-SRC-007`, `009` | Navigation targets derive only from validated IDs and fixed local route templates. |
| `LKAI-DEC-007` | Keyword cookie has priority, and every new intent creation deletes the other kind. Success deletes both cookies. | `LKAI-SRC-006`, `007` | At most one user-selected pending action can be claimed. |
| `LKAI-DEC-008` | Move the existing keyword line parser unchanged into `keyword-intelligence-validation.ts` as `parseKeywordSeedText`; both forms import it. | `LKAI-SRC-003` | Landing and `/keywords` use identical normalization/dedup behavior. |
| `LKAI-DEC-009` | Preserve landing DOM/CSS structure and change only field semantics, copy, validation, submit call, errors, and navigation. | `LKAI-SRC-001`, `002` | Landing design and CTA anchors remain stable. |
| `LKAI-DEC-010` | Preserve legacy run-intent API and claim fallback indefinitely in this change; do not schedule time-based deletion. | `LKAI-SRC-010`, `016` | In-flight sign-ups and non-landing clients remain safe; no keyword work occurs on that branch. |
| `LKAI-DEC-011` | Use a forward-only migration named `20260826120000_keyword_research_intent`; never edit `20260817000000_keyword_intelligence`. | Workspace migration policy | Existing migration history and live keyword rows remain intact. |
| `LKAI-DEC-012` | Prove the user-visible flow with emitted Next, actual Route Handlers, actual backend/API/repository, migrated isolated PostgreSQL, installed Neon-auth substitute, in-memory queue/provider substitutes, and local Chrome. | Existing KI-W6 harness capability | The test proves local emitted/auth/database causality but makes no live provider/auth/deployment claim. |
| `LKAI-DEC-013` | Supersede the whole-file `repository.js` SHA-256 and transaction-site inventory in `keyword-intelligence-repository.test.js` after W1 freezes the required repository change; preserve every historical case and mutation control. The exact new inventory is 19 total sites, nine short sites including `claimIntent`, ten unchanged scale sites, and the W6-NC-15 mutated copy still has 19 call sites because it removes an options argument rather than a call. | Execution discovery: the accepted C112 enforcement test pins the complete production file and exactly 18 transaction sites, so the required new short `claimIntent` transaction necessarily invalidates both literals. | The full backend suite accepts and continues policing the expanded repository without weakening or bypassing its transaction-profile mutation control. |
| `LKAI-DEC-014` | Add only `parseKeywordSeedText` to the sorted `VALIDATION_SURFACE` literal in `keyword-intelligence-inventory.test.ts`; preserve every other export, owned-path inventory, historical case ID/digest, and control. | Execution discovery: W5-I02 pins the complete export surface of the mandated shared validation module, so the required named parser export necessarily invalidates the prior literal. | `npm run check` continues enforcing an exact validation surface while accepting the one planned additive export. |
| `LKAI-DEC-015` | Supersede only the continuation-navigation source assertions in `design-system-shell.test.ts`: require encoded `continuation.run.runId` for the legacy union branch and encoded `continuation.research.id` for the keyword branch; preserve every auth, shell, history, CSS, and not-found assertion. | Execution discovery: the G3 source contract pins the former unwrapped `run.runId` expression, which necessarily changes under the mandated strict continuation union. | The existing design-system regression continues policing both fixed local destinations without weakening the unchanged auth-flow contract. |
| `LKAI-DEC-016` | In backend legacy `POST /api/run-intents`, compute `timestamp=currentDate(now)` once, set `expiresAt=new Date(timestamp.getTime()+3_600_000)`, and pass the same `timestamp` to cleanup. Add a regression using an injected clock that returns a `Date`. | Emitted-browser discovery: the server's default clock returns milliseconds, but the accepted harness returns `Date`; direct `now() + 3_600_000` string-concatenates for the latter and creates an immediately expired legacy intent. | Production semantics stay one hour; injected clocks obey the same formula, allowing the required already-issued legacy continuation to remain testable and correct. |
| `LKAI-DEC-017` | In the accepted e2e harness `pinDates` proxy, exempt only `PrismaRunRepository.createRunIntent` from `withClock`; forward its arguments unchanged because the final `Date` is an expiry, not an operation timestamp. Preserve every other clock pin, substitute, trace, fixture, and public harness interface. | Emitted-browser/direct-harness evidence: after `LKAI-DEC-016`, the harness still rewrites the correctly derived `expiresAt` argument back to `nowBox.current`, producing an exact zero-second lifetime. | The legacy-intent substitute regains production parity (`expiresAt=now+3_600_000`) without changing production code or any other harness clock behavior. |
| `LKAI-DEC-018` | Add fixture-only nonempty `googleApiKey`, `googleSearchEngineId`, and `openaiApiKey` members to the accepted e2e harness `BACKEND_CONFIG`; use deterministic non-production values and change no production configuration path. | The emitted legacy-continuation case reaches the production `assertRunConfig` gate before claiming an already-issued run intent. The accepted harness previously omitted these keys because its prior cases never activated that route, causing a harness-only 503. | The browser registry can exercise the real legacy claim branch. The values authorize no provider call; the registry retains its zero-provider and loopback-only oracles. |
| `LKAI-DEC-019` | Extend the accepted harness's existing `injectCapturedDefect` test interface with exactly `expire-latest-unclaimed-keyword-intent`: update exactly one latest unclaimed `KeywordResearchIntent` to `expiresAt=nowBox.current-1ms`, fail preflight unless exactly one row changes, return only the fault ID and count, and expose no intent, seed, owner, or database identifier. | `LKAI-FE-08` requires a real emitted-browser expired-intent 404 witness, while the production TTL is one hour and the harness intentionally exposes neither its Prisma client nor a general clock setter. | The browser test activates the real backend expiry predicate and BFF cookie-deletion/home-redirect branch without waiting an hour, weakening clock controls, or creating a general database mutation seam. |

## 4. Exact contracts

### 4.1 Identifier, time, and cookie formulas

```text
KeywordResearchIntent.id = "intent_" + randomBytes(24).toString("base64url")
accepted pattern          = /^intent_[A-Za-z0-9_-]{32}$/u
createdAt                 = injected backend now
expiresAt                 = new Date(createdAt.getTime() + 3_600_000)
cookie maxAge             = clamp(floor((expiresAtMs - Date.now()) / 1000), 1, 3600)
cookie options            = httpOnly:true, secure:NODE_ENV==="production",
                            sameSite:"lax", path:"/", maxAge
researchId                = existing newResearchId()
initialize message        = {contractVersion:1,type:"keyword.initialize.v1",
                             researchId,generation:1}
```

The intent ID has no authorization meaning. Authorization is the claim
transaction's authenticated `ownerId` predicate plus the durable
`claimedByUserId` mapping.

### 4.2 Database schema

Add exactly this Prisma model and the reverse relation shown below:

```prisma
model KeywordResearchIntent {
  id                  String           @id
  seeds               Json
  createdAt           DateTime         @default(now())
  expiresAt           DateTime
  claimedAt           DateTime?
  claimedByUserId     String?
  claimedResearchId   String?          @unique
  claimedResearch     KeywordResearch? @relation(fields: [claimedResearchId], references: [id], onDelete: Restrict)

  @@index([expiresAt])
}

model KeywordResearch {
  // existing fields unchanged
  intent KeywordResearchIntent?
}
```

The migration creates the seven columns, primary key, unique index
`KeywordResearchIntent_claimedResearchId_key`, index
`KeywordResearchIntent_expiresAt_idx`, and foreign key
`KeywordResearchIntent_claimedResearchId_fkey` with `ON DELETE RESTRICT ON
UPDATE CASCADE`. It changes no existing column, enum, default, row, or index.

Unclaimed rows require `seeds` to parse as the existing normalized 1–5 seed
contract at the repository boundary. Claimed rows have `seeds=[]`, non-null
`claimedAt`, `claimedByUserId`, and `claimedResearchId`.

### 4.3 Backend service and repository signatures

Add these exact exports/methods:

```js
export function newKeywordResearchIntentId(): string

PrismaKeywordResearchRepository.createIntent(
  { intentId, seeds, expiresAt }, now
) -> Promise<{ outcome:"created", intent } | { outcome:"conflict" }>

PrismaKeywordResearchRepository.claimIntent(
  { intentId, ownerId, researchId, configSnapshot, configFingerprint, markets }, now
) -> Promise<
  { outcome:"created", research } |
  { outcome:"found", research } |
  { outcome:"not_found" } |
  { outcome:"conflict" }
>

PrismaKeywordResearchRepository.deleteExpiredIntents(now)
  -> Promise<{count:number}>

createKeywordResearchApi(...).createIntent({seeds})
  -> Promise<{intentId:string,expiresAt:string}>

createKeywordResearchApi(...).claimIntent({ownerId,intentId})
  -> Promise<{created:boolean,research:ResearchView}>
```

Extend `createKeywordResearchApi` dependencies with
`intentIdFactory=newKeywordResearchIntentId`; retain existing defaults and
callers.

`createIntent` strictly parses exactly `{seeds}`, calls existing
`normalizeSeeds`, writes one intent, asynchronously invokes
`deleteExpiredIntents(now)` only after successful creation while swallowing
cleanup failure, and returns the ISO expiry. It has no dispatcher call site.

`claimIntent` strictly parses exactly `{ownerId,intentId}`. It passes the
factory research ID and current `configSnapshot`, fingerprint, and markets to
the repository. `not_found` maps to `ApiError(404,
"KEYWORD_RESEARCH_INTENT_NOT_FOUND", "Pending keyword research was not found or
has expired")`; `conflict` maps to the existing contract mismatch. On
`created`, it performs the same post-commit initialize send as direct
`createResearch`; on `found`, it sends nothing. Dispatch failure is swallowed
only after the durable created result.

### 4.4 Claim transaction algorithm

Inside `_transaction`, in this exact order. The research insert precedes the
intent foreign-key write because the PostgreSQL foreign key is immediate, not
deferred:

1. `findUnique({where:{id:intentId}})`.
2. Return `not_found` if absent.
3. If `claimedResearchId` is non-null, return `not_found` unless
   `claimedByUserId===ownerId`; for the same owner load the research by exact ID
   and return `found` regardless of `expiresAt`, or return `conflict` if the
   mapping is broken. Persistence of claimed mappings is the replay authority;
   expiry applies only before the first successful claim.
4. Return `not_found` if the still-unclaimed intent has `expiresAt <= now`;
   otherwise strictly parse its stored seeds before any write.
5. Insert a provisional `KeywordResearch` with the exact same field mapping
   used by repository `create`: queued, generation/contract version 1, current
   config snapshot/fingerprint/markets, stored normalized seeds, progress
   `{stages:{}}`, selection revision zero, and `createdAt:now`. Any insert
   failure rolls back the whole transaction before the intent is changed.
6. Execute `updateMany` with predicate `{id:intentId, claimedResearchId:null,
   claimedByUserId:null, claimedAt:null, expiresAt:{gt:now}}`; write
   `{claimedAt:now,claimedByUserId:ownerId,claimedResearchId:researchId,seeds:[]}`.
7. If the CAS count is zero, delete the exact provisional research by its
   generated `researchId` inside this transaction, then reread the intent.
   Return same-owner `found` after loading its exact mapped research, foreign/
   expired `not_found`, or otherwise `conflict`. The losing transaction must
   commit no provisional research row.
8. If the CAS count is one, commit the provisional research and intent mapping
   together and return `created` only after commit. Any unexpected count is
   `conflict` and rolls back both writes.

The transaction uses the repository's short transaction options and existing
schema selection. No SQS/network call occurs inside it.

### 4.5 Backend HTTP routes

Add:

```text
POST /api/keyword-research-intents
body: {"seeds": string[1..5]}
auth: service-token boundary only; no X-User-Id required
created: 201 {"intentId":"intent_<32>","expiresAt":"<ISO>"}

POST /api/keyword-research-intents/{intentId}/claim
body: absent/empty
auth: trusted X-User-Id required
created: 201 {"research":ResearchView}
replay: 200 {"research":ResearchView}
missing/expired/foreign: 404 KEYWORD_RESEARCH_INTENT_NOT_FOUND
malformed ID: 400 KEYWORD_RESEARCH_INPUT_INVALID
```

The existing authenticated `POST /api/keyword-research` stays byte/field
compatible and the backend still rejects it without trusted user context. Add
`requestedKeywordResearchIntentId(pathname)` using the exact claim grammar and
existing intent-ID pattern; do not probe alternate paths.

### 4.6 Frontend/BFF payloads

Anonymous `POST /api/keyword-research` returns after durable intent creation:

```json
{
  "error": {
    "code": "AUTHENTICATION_REQUIRED",
    "message": "Create an account or sign in to continue this keyword research.",
    "details": { "continueUrl": "/sign-up" }
  }
}
```

Status is `401`. The response also sets only
`storesignal_pending_keyword_research_intent=<opaque-id>` with the fixed cookie
options and deletes `storesignal_pending_run_intent`. Signed-in behavior remains
the existing `202 {research}` proxy response.

The internal continuation response becomes the strict union:

```ts
export type SearchContinuationResponse =
  | { kind: "legacy_run"; run: StartRunResponse }
  | { kind: "keyword_research"; research: ResearchView };
```

`parseSearchContinuationResponse` requires exact top-level and nested keys by
delegating to existing `parseStartRunResponse` or `parseResearchView`. Unknown
kind, URL/destination, extra key, missing field, or malformed nested response
throws `ApiPayloadError` and the BFF maps an unreadable backend success to safe
`502 BACKEND_INVALID_RESPONSE`.

### 4.7 Cookie selection and deletion

Create `frontend/lib/pending-search-intent.ts` exporting exactly:

```ts
PENDING_RUN_INTENT_COOKIE = "storesignal_pending_run_intent"
PENDING_KEYWORD_RESEARCH_INTENT_COOKIE = "storesignal_pending_keyword_research_intent"
PENDING_INTENT_ID_PATTERN = /^intent_[A-Za-z0-9_-]{32}$/u
pendingIntentMaxAge(expiresAt:string, nowMs:number=Date.now()): number | null
pendingIntentCookieOptions(maxAge:number): {
  httpOnly:true; secure:boolean; sameSite:"lax"; path:"/"; maxAge:number
}
```

`pendingIntentMaxAge` returns null unless the timestamp is finite and strictly
future; otherwise it returns `max(1,min(3600,floor(delta/1000)))`.

Claim BFF order:

1. Require auth using `authenticatedRoute`.
2. Read both cookies.
3. Delete malformed cookie values locally.
4. If a valid keyword cookie exists, proxy the keyword claim. Otherwise, if a
   valid legacy cookie exists, proxy legacy claim. Otherwise return existing
   `404 RUN_INTENT_NOT_FOUND`.
5. Non-success backend responses pass through. Delete the selected cookie on
   `404`; retain it on every other error for retry.
6. Strictly parse success, wrap with the local discriminator, and return the
   backend `200`/`201` status with `Cache-Control:no-store`.
7. On success delete both pending cookies.

### 4.8 Landing form behavior

`RunForm` retains `<form id="start-discovery" className="run-form-card
run-start-form ds-card">` and every structural class. Replace only its data and
submit behavior:

- derive `seeds=parseKeywordSeedText(input)` and
  `validation=validateSeedsInput({seeds})`;
- suggestions append one normalized unique seed, refuse a sixth with `You can
  add up to five seed phrases.`, and retain the nine existing chips;
- label secondary text becomes `One seed phrase per line`;
- count renders `N seed phrase(s)`;
- textarea `maxLength` becomes `2004`, accommodating five 100-code-point
  all-astral phrases in UTF-16 plus four newlines; normalization and the strict
  1–5-by-100-code-point validator remain authoritative;
- footer copy becomes `Review keyword opportunities before store discovery
  begins.`;
- button copy becomes `Explore my keywords` and pending copy remains `Building
  your research…`;
- submit calls `createKeywordResearch(validation.seeds)` and pushes
  `/keywords/${encodeURIComponent(view.id)}`;
- the exact auth-required details branch pushes `/sign-up`;
- `BACKEND_TIMEOUT` displays `The research request timed out, so its outcome is
  unknown. Wait a moment before trying again.`;
- every other error uses `errorMessage`.

`ResearchForm` deletes its private parser and imports
`parseKeywordSeedText`; no other behavior or CSS changes.

## 5. State and failure lifecycle

| Transition | Preconditions | Atomic/durable action | Emitted action | Replay/result | Forbidden outcome |
|---|---|---|---|---|---|
| Anonymous submit | strict seeds, no session | insert unowned intent, one-hour expiry | set opaque cookie; return 401 | a repeated user submit creates a new intent and replaces the cookie; old unclaimed row expires | research/SQS/provider action |
| Signed-in submit | strict seeds, valid session | existing research insert | initialize send after commit | existing create semantics | anonymous owner/body identity |
| Auth claim | valid session + live unclaimed intent | claim CAS + research insert in one transaction; scrub intent seeds | initialize send after commit | same owner gets same research | pre-commit send, partial claim, foreign claim |
| Dispatch loss | committed research, send throws/response lost | research remains queued | none from failed call | queued recovery sends initialize | second research or fabricated success |
| Claim response loss | claim committed, BFF/client lacks success | cookie retained | retry claim | found response, no immediate resend; recovery covers missing send | new research ID |
| Same-owner concurrent claim | two calls, same intent/owner | one CAS wins | at most one immediate initialize send | both return same research | two rows/sends |
| Different-owner concurrent claim | two owners | one CAS wins | winner only may send | loser gets 404 | owner/mapping disclosure |
| Expired/missing claim | absent or unclaimed with `expiresAt<=now` | no write | no send | 404; BFF deletes selected cookie | recreation from cookie |
| New keyword intent with legacy cookie | anonymous valid seeds | insert keyword intent | delete legacy cookie, set keyword cookie | keyword wins | both cookies active |
| Legacy continuation | valid legacy cookie + session | unchanged legacy claim transaction | unchanged run queue action | `/runs/{runId}` | keyword initialize send |

No cancellation state is added. Deleting/replacing a browser cookie does not
delete an intent row; unclaimed expiry cleanup owns eventual deletion. Claimed
research follows the existing keyword cancellation/terminal policy.

## 6. Exact implementation file map

### 6.1 Files that must change or be added

| Path | Symbols and exact change |
|---|---|
| `email_scraper/prisma/schema.prisma` | Add `KeywordResearchIntent`; add `KeywordResearch.intent` reverse relation only. |
| `email_scraper/prisma/migrations/20260826120000_keyword_research_intent/migration.sql` | New forward-only table/index/FK migration from §4.2. |
| `email_scraper/src/keyword-intelligence/repository.js` | Export `newKeywordResearchIntentId`; add `createIntent`, `claimIntent`, `deleteExpiredIntents`; no existing worker method changes. |
| `email_scraper/src/keyword-intelligence/api.js` | Add strict intent schemas/error, factory dependency, `createIntent`, `claimIntent`, and one shared post-commit initialize helper used by direct create and claim. |
| `email_scraper/src/server.js` | Add exact intent create/claim route parser and handlers; preserve authenticated keyword create and all legacy routes. Normalize the legacy run-intent injected clock per `LKAI-DEC-016`. |
| `email_scraper/test/fixtures/keyword-intelligence/landing-keyword-auth-intent-v1.json` | Add strict valid/boundary/invalid request, create response, claim response, and error fixtures; no private/live values. |
| `email_scraper/test/keyword-research-intent.test.js` | New service/server registry for `LKAI-BE-*` and related controls; include the exact Date-returning legacy clock regression from `LKAI-DEC-016`. |
| `email_scraper/test/keyword-research-intent.integration.test.js` | New isolated-PostgreSQL registry for `LKAI-DB-*` and atomic/concurrency controls. |
| `email_scraper/test/keyword-intelligence-repository.test.js` | After `repository.js` is frozen: replace `SCN_KI_043_SOURCE_SHA256`; append `claimIntent` to `SCN_KI_043_SHORT_PARTITION`; change exact total/short counts from 18/8 to 19/9; change the W6-NC-15 mutated-copy call count from 18 to 19; and update the two source-baseline labels from C112 to LKAI-W1. Preserve the ten-member scale partition, option-profile/timeout oracles, all historical case IDs/digests, and the mutation-control procedure. |
| `email_scraper/test/helpers/keyword-intelligence-e2e-harness.js` | In `pinDates`, forward `createRunIntent` arguments unchanged; add only the three deterministic fixture config values in `LKAI-DEC-018`; add only the bounded expired-intent defect in `LKAI-DEC-019`; retain every other clock, interface, fixture, and trace behavior. |
| `email_scraper/README.md` | Document both keyword-intent backend routes and the post-auth-only dispatch invariant. |
| `frontend/lib/pending-search-intent.ts` | New cookie constants, ID pattern, max-age and options helpers from §4.7. |
| `frontend/lib/keyword-intelligence-validation.ts` | Export `parseKeywordSeedText` with the exact moved parser behavior. |
| `frontend/components/keyword-intelligence/research-form.tsx` | Remove private `parseKeywordLines`; import/use shared parser only. |
| `frontend/components/run-form.tsx` | Preserve card markup/classes; replace category parsing/direct-run POST with §4.8 keyword behavior. |
| `frontend/app/api/keyword-research/route.ts` | Branch on `sessionUserId`; signed-in proxy unchanged, signed-out create intent/cookie/401 flow. |
| `frontend/app/api/runs/route.ts` | Import shared cookie helpers; legacy anonymous creation deletes keyword cookie before setting legacy cookie. |
| `frontend/app/api/run-intents/claim/route.ts` | Implement strict two-cookie claim selection/wrapping algorithm from §4.7. |
| `frontend/lib/api-types.ts` | Add `SearchContinuationResponse` strict union. |
| `frontend/lib/api-validation.ts` | Add `parseSearchContinuationResponse`; preserve existing parser exports. |
| `frontend/components/run-continuation.tsx` | Parse union; fixed navigation to keyword or legacy run; recognize both not-found codes. |
| `frontend/test/landing-keyword-auth-flow.test.ts` | New helper/parser/component/source-contract cases and frontend negative controls. |
| `frontend/test/browser/landing-keyword-auth-flow.mjs` | New emitted Next + local Chrome + actual backend/Prisma/auth-substitute flow registry; imports existing e2e harness read-only. |
| `frontend/test/design-system-hero.test.ts` | Replace legacy landing payload/navigation assertions with keyword validation/payload/navigation and unchanged class/suggestion assertions. |
| `frontend/test/keyword-intelligence-inventory.test.ts` | Add only `parseKeywordSeedText` to the sorted `VALIDATION_SURFACE` expected export list; preserve every other inventory/case/control byte except formatter-required adjacency. |
| `frontend/test/design-system-shell.test.ts` | In the continuation test only, replace the old encoded `run.runId` source assertion with exact encoded assertions for `continuation.run.runId` and `continuation.research.id`; preserve all other assertions. |
| `frontend/scripts/g4-browser-regression.mjs` | Replace obsolete 101-category maximum input with six keyword seeds; retain viewport/form/layout captures. |
| `frontend/README.md` | Describe landing keyword submission, both continuation outcomes, keyword BFF routes, and post-auth dispatch. |

### 6.2 Files that must remain byte-unchanged

`frontend/app/page.tsx`, `frontend/components/landing-sections.tsx`,
`frontend/components/traffic-globe.tsx`, `frontend/app/globals.css`,
`frontend/components/auth-form.tsx`, `frontend/app/sign-up/page.tsx`,
`frontend/app/sign-in/page.tsx`, `frontend/app/runs/continue/page.tsx`,
`frontend/lib/client-api.ts`, `frontend/proxy.ts`,
`email_scraper/src/aws-pipeline/keyword-intelligence/contracts.js`,
`recovery.js`, `handler.js`, every provider adapter, infrastructure template,
package/lock file, historical migration, and existing accepted enforcement
fixture.

Generated Prisma client/build output may be regenerated by prescribed commands
but must not be committed.

## 7. Execution windows

### 7.1 Window `LKAI-W1` — Durable anonymous intent and authenticated atomic claim

```yaml
window_id: LKAI-W1
objective: establish the strict server-side intent and post-auth-only dispatch contract
depends_on: []
consumes: this specification adopted into A1-A8 after current active stop
produces: migration, repository/service/HTTP contract, backend enforcement evidence
assigned_agent_policy: one_window
authorized_write_scope: the ten backend paths in §6.1, exact named symbols only
read_only_scope: current keyword config/serializer/recovery, isolated-postgres helper, accepted tests
authorized_actions: local edits, Prisma generate/validate, focused tests, isolated test DB, secret scan
prohibited_actions: frontend edit, AWS/provider/production DB/deploy/secret/commit/push, worker contract edit
successor: LKAI-W2
successor_reserved_for: parent
may_start_successor: false
```

#### Preconditions

- [ ] `LKAI-W1-P1` Verify a new active assignment pins adopted A1/A3/A4 hashes and authorizes only `LKAI-W1`.
- [ ] `LKAI-W1-P2` Verify `KI-W8-C201` has reached its planned stop and no current assignment prohibits schema/backend edits.
- [ ] `LKAI-W1-P3` Record backend/root dirty state and preserve unrelated changes.
- [ ] `LKAI-W1-P4` Verify isolated `TEST_DATABASE_URL` and direct test transport differ from production before migration-backed writes.
- [ ] `LKAI-W1-P5` Validate the literal payload fixture and 11 backend/database case IDs against this document.

#### Tasks

- [ ] `LKAI-W1-T1` Implement the exact schema and forward migration in §4.2/§6.1. Do not edit prior migrations. Add catalog assertions in the new integration file for all seven columns, the primary/unique/expiry indexes, FK actions, reverse relation, and unchanged legacy tables.
- [ ] `LKAI-W1-T2` Implement repository ID/create/claim/cleanup signatures and the eight-step transaction in §§4.1–4.4. Use `_transaction`; preserve schema selection; scrub seeds only in the successful claim CAS; classify every expected result with the locked union.
- [ ] `LKAI-W1-T3` Implement API create/claim strict schemas, safe errors, current-config-at-claim mapping, and shared post-commit dispatch helper. Prove `createIntent` cannot reach the dispatcher and `claimIntent(found)` sends zero immediate messages.
- [ ] `LKAI-W1-T4` Add the two backend routes from §4.5 with exact authentication and status/body behavior. Preserve direct authenticated creation and reject direct unauthenticated creation as before.
- [ ] `LKAI-W1-T5` Add literal fixtures and executable registries for `LKAI-BE-01`–`07`, `LKAI-DB-01`–`04`, and `LKAI-NC-01`–`03`. Registration and execution are recorded only after activation witness and oracle pass.
- [ ] `LKAI-W1-T6` Update backend README only after code/tests establish the exact route and dispatch boundary.

#### Verification

- [ ] `LKAI-W1-V1` Run focused non-DB tests; require all seven backend IDs executed, zero skips/duplicates/unexpected IDs, and no dispatch before authenticated claim.
- [ ] `LKAI-W1-V2` Run the new integration file through the isolated migration helper; require all four DB IDs, rollback proof, both concurrency schedules, exact schema selection, and cleanup postcondition.
- [ ] `LKAI-W1-V3` Run `npm run db:generate`, `npm run db:validate`, `npm run check:secrets`, and `npm test` from `email_scraper/` against frozen final inputs.
- [ ] `LKAI-W1-V4` If the full suite fails only on restricted localhost listeners, prove no matching process/mutation remains and rerun the identical command once with authorized sandbox escalation.
- [ ] `LKAI-W1-V5` Recompute required/registered/executed set equality and the global digest for the W1 subset; falsify `LKAI-NC-01`–`03`.

#### Handoff

- [ ] `LKAI-W1-H1` Record exact changed paths/symbols and migration hash.
- [ ] `LKAI-W1-H2` Record commands, exits, case sets/digests, controls, skips, DB schema identity/cleanup, and no external actions.
- [ ] `LKAI-W1-H3` Prove diff equals W1 scope and all §6.2 protected files remain unchanged.
- [ ] `LKAI-W1-H4` Set only W1 to `AWAITING_REVIEW`; do not begin frontend work.

### 7.2 Window `LKAI-W2` — Landing/BFF continuation and emitted-browser proof

```yaml
window_id: LKAI-W2
objective: make the existing landing form enter keyword research while preserving auth continuation and design
depends_on: [LKAI-W1 accepted]
consumes: W1 routes, payloads, migration, post-auth dispatch guarantee
produces: landing keyword flow, dual continuation, emitted-browser evidence
assigned_agent_policy: one_window
authorized_write_scope: the seventeen frontend paths in §6.1, exact named symbols only
read_only_scope: backend W1 code/tests, existing KI e2e harness, installed Next docs, landing layout/CSS/auth files
authorized_actions: local edits, frontend lint/test/build, focused emitted browser with isolated DB and local substitutes
prohibited_actions: backend/schema/package/lock/auth-provider/middleware/CSS/landing-layout edit, AWS/provider/production/deploy/commit/push
successor: STOP
successor_reserved_for: parent final review
may_start_successor: false
```

#### Preconditions

- [ ] `LKAI-W2-P1` Verify new assignment/hash/state and independent parent acceptance of W1.
- [ ] `LKAI-W2-P2` Verify W1 exact response fixtures and migration-backed behavior remain unchanged.
- [ ] `LKAI-W2-P3` Record frontend/root dirty state and protected-file hashes.
- [ ] `LKAI-W2-P4` Read installed Next route-handler, client-component, cookies, and navigation docs.
- [ ] `LKAI-W2-P5` Verify the browser harness can create/drop an isolated schema and uses only local provider/queue/auth substitutes.

#### Tasks

- [ ] `LKAI-W2-T1` Add the cookie helper and strict continuation type/parser from §§4.6–4.7; add boundary tests for valid unions, every missing/extra/unknown-kind shape, max-age edges, and fixed local navigation derivation.
- [ ] `LKAI-W2-T2` Change keyword BFF `POST` to the exact signed-in/anonymous branches; normalize before proxy; validate intent response before cookie; on invalid backend success return 502 and set no cookie; add the one-cookie invariant to legacy `/api/runs` POST.
- [ ] `LKAI-W2-T3` Change claim BFF and `RunContinuation` to the exact priority/error/deletion/discriminated navigation algorithm. Do not change `AuthForm` or accept a backend destination URL.
- [ ] `LKAI-W2-T4` Move the parser and rewire `RunForm` exactly as §4.8 while preserving the structural DOM/classes/CTA anchor and nine suggestions. Update `ResearchForm` only to import the moved parser.
- [ ] `LKAI-W2-T5` Update the existing static hero test and G4 browser maximum case; add the new frontend registry for `LKAI-FE-01`–`10` and controls `LKAI-NC-04`–`07`.
- [ ] `LKAI-W2-T6` Add the emitted-browser script using `createKeywordIntelligenceE2eHarness` read-only. Exercise signed-out landing submission, zero pre-auth research/send, sign-up navigation, authenticated claim, keyword navigation, response-loss retry, legacy fallback, cookie exclusivity, and responsive form geometry without calling `drainKeywordWork` or any live provider.
- [ ] `LKAI-W2-T7` Update frontend README with exact route/continuation diagrams and the no-pre-auth-dispatch statement.

#### Verification

- [ ] `LKAI-W2-V1` Run focused frontend Node tests; require all helper/parser/source-contract cases and controls to execute.
- [ ] `LKAI-W2-V2` Run `npm run check` from `frontend/`; lint, full tests, and one production Next build must pass against frozen final inputs.
- [ ] `LKAI-W2-V3` Run the emitted-browser registry once with the authorized isolated DB and sandbox escalation when required. Require a nonempty actual Route Handler/backend/Prisma path, exact cookie/auth/navigation witnesses, and zero live external operations.
- [ ] `LKAI-W2-V4` At 390×844, 768×1024, and 1280×800, assert the unchanged form/card/hero class inventory, nine suggestions, local CTA target, no horizontal overflow, and usable submit/error states.
- [ ] `LKAI-W2-V5` Recompute the complete 21-case required/registered/executed equality, zero required skips, and digest `60f8ab75a1bae9e047263d8776e375308c14f41e689bffaac8cd9d20b7eb5ece`; falsify all seven controls.
- [ ] `LKAI-W2-V6` Prove all §6.2 protected files and backend W1 inputs remain unchanged; run frontend diff check and root secret scan as applicable.

#### Handoff

- [ ] `LKAI-W2-H1` Record exact changed paths/symbols and frozen source/test hashes.
- [ ] `LKAI-W2-H2` Record commands, exits, viewports, case/control sets and digests, isolated schema cleanup, and external-action count zero.
- [ ] `LKAI-W2-H3` Prove diff equals W2 scope and no successor or parked cleanup began.
- [ ] `LKAI-W2-H4` Set W2 to `AWAITING_REVIEW` and stop for independent parent review.

## 8. Enforcement matrix

### 8.1 Required case set

The required set has 21 literal IDs. Sort by unsigned UTF-8 bytes, append LF to
each, concatenate, and SHA-256. Required digest:
`60f8ab75a1bae9e047263d8776e375308c14f41e689bffaac8cd9d20b7eb5ece`.

| Case | Production path and partition | Activation witness | Exact oracle / forbidden operations | Registration |
|---|---|---|---|---|
| `LKAI-BE-01` | anonymous intent service, 1 and 5 normalized seeds | repository `createIntent` called | one intent, +3600000 ms expiry, zero research/dispatch | backend unit registry |
| `LKAI-BE-02` | 0/6, >100cp, duplicate, control, unknown key | strict parser reached | 400, zero write/dispatch | backend unit registry |
| `LKAI-BE-03` | authenticated direct research create | existing create branch and dispatcher | 202/created research, one initialize; byte-compatible envelope | backend unit/server registry |
| `LKAI-BE-04` | authenticated first intent claim | committed transaction then dispatcher | 201, owned research, scrubbed intent, one post-commit initialize | backend unit/server registry |
| `LKAI-BE-05` | same-owner claim replay | found mapping branch | 200 same research ID, zero new research/immediate send | backend unit registry |
| `LKAI-BE-06` | missing/unclaimed-expired/foreign claim, plus claimed same-owner replay after expiry | not-found/replay predicates | first three are identical 404 with zero research/send and no owner detail; same owner receives the mapped research with no immediate send | backend unit/server registry |
| `LKAI-BE-07` | dispatch throws after commit | dispatch failure caught after created outcome | queued research survives; recovery reconstructs exactly one initialize | backend unit + existing recovery fake |
| `LKAI-DB-01` | migrated schema and expiry cleanup | isolated schema catalog and delete query | exact model/index/FK; only expired unclaimed row deleted | new integration registry |
| `LKAI-DB-02` | injected research insert failure and lost-CAS provisional cleanup | transaction reached provisional insert/CAS schedule | failure or lost race leaves no provisional research; live intent is unchanged unless another claimant won | new integration registry |
| `LKAI-DB-03` | two concurrent same-owner claims | both transactions activated | one research/mapping, both same ID, one created result | new integration registry |
| `LKAI-DB-04` | two concurrent different-owner claims | both owner predicates activated | one winner, one not-found, one research, no cross-owner read | new integration registry |
| `LKAI-FE-01` | signed-in landing, 1 and 5 seeds | real form submit and keyword BFF | POST normalized seeds; `/keywords/{id}`; no `/api/runs` POST | frontend/browser registry |
| `LKAI-FE-02` | landing 0 and 6 seeds | submit handler activated | visible exact error, zero fetch/navigation | frontend/browser registry |
| `LKAI-FE-03` | signed-out landing submit | keyword BFF anonymous branch | sign-up navigation, keyword cookie only, zero research/SQS/provider | emitted-browser registry |
| `LKAI-FE-04` | successful auth after pending keyword intent | `/runs/continue` keyword branch | actual claimed research, one initialize after auth, `/keywords/{id}` | emitted-browser registry |
| `LKAI-FE-05` | claim commit with response loss then retry | retained cookie and same-owner found branch | same research, no second immediate send, eventual recovery possible | component/backend fault registry |
| `LKAI-FE-06` | valid already-issued legacy cookie | legacy claim branch | `/runs/{runId}`, zero keyword initialize | emitted-browser registry |
| `LKAI-FE-07` | opposing pending cookie exists | new-intent cookie write branch | other cookie deleted; success deletes both | Route Handler/browser registry |
| `LKAI-FE-08` | malformed/expired/missing selected cookie | local validation/404 branch | safe home redirect after not-found; no claim/create/send | component/browser registry |
| `LKAI-FE-09` | landing at three required viewports and UI states | emitted DOM/layout capture | unchanged structural classes, nine chips, CTA target, no overflow | emitted-browser registry |
| `LKAI-FE-10` | valid/invalid continuation union payloads | strict parser discriminator | exact union accepted; unknown/extra/URL rejected | frontend Node registry |

### 8.2 Negative controls

The control set has seven IDs and sorted-LF digest
`47694f5643902ea973680404a1022db24c67dcebab471dca20f9d8970da4bb91`.

| Control | Deliberate defect | Required falsification |
|---|---|---|
| `LKAI-NC-01` | fake anonymous create calls dispatcher | `LKAI-BE-01/FE-03` zero-send oracle fails |
| `LKAI-NC-02` | split claim update and research insert across transactions | injected insert failure leaves partial claim; DB-02 fails |
| `LKAI-NC-03` | omit owner equality on claimed replay | foreign claimant sees research; BE-06/DB-04 fail |
| `LKAI-NC-04` | restore landing `POST /api/runs` | FE-01 endpoint/lineage assertion fails |
| `LKAI-NC-05` | parser accepts unknown kind or destination URL | FE-10 strict-union oracle fails |
| `LKAI-NC-06` | do not clear the opposite pending cookie | FE-07 exact cookie-set assertion fails |
| `LKAI-NC-07` | remove/rename a protected landing structural class or CTA | FE-09 inventory/geometry oracle fails |

Required, registered, and executed case sets must be enumerated by executable
registries, not inferred from test names. A case enters the executed set only
after its activation witness and full oracle pass. Missing, duplicate,
unexpected, skipped, selected-but-filtered, or unactivated cases fail the gate.

## 9. Test substitute fidelity

| Production boundary | Substitute/parity | May prove | Must not claim |
|---|---|---|---|
| Next/browser | production `next build` + `next start` + local Chrome CDP | emitted components, Route Handlers, cookies, navigation, responsive DOM | deployed CDN or browser population |
| Authentication | installed Neon Auth client/middleware against existing deterministic loopback session harness | session consumption, owner propagation/denial, cookie transport, protected continuation | external credential verification, live Neon Auth availability, cryptographic assurance |
| Database | actual Prisma repositories and full migrations in one disposable non-public PostgreSQL schema | schema, transactions, CAS, owner isolation, replay, rollback | production latency/permissions |
| SQS | existing in-memory dispatcher reproducing strict `keyword.initialize.v1` validation and send log | message count/order and post-auth reachability | live SQS IAM/delivery |
| Providers | existing local deterministic HTTP fixtures, with worker drain forbidden for pre-auth cases | no-call assertions and causal local processing when explicitly drained in existing regressions | live pricing/quota/availability |

The new emitted-browser test reuses the existing harness. The parent-reviewed
`LKAI-DEC-017` through `LKAI-DEC-019` corrections are the only permitted
harness changes; any other need to change that accepted harness is a new
specification contradiction, not an implementation-agent choice.

## 10. Verification commands and frozen gates

Diagnostics during editing may run focused files repeatedly. Handoff evidence
must run against frozen final inputs:

From `email_scraper/`:

```text
node --test test/keyword-research-intent.test.js
npm run db:generate
npm run db:validate
ALLOW_DATABASE_TESTS=true node -r dotenv/config --test --test-concurrency=1 test/keyword-research-intent.integration.test.js
npm run check:secrets
npm test
git diff --check
```

The integration command requires the existing isolated-test rules and a
`TEST_DATABASE_URL`/direct transport proven non-production. It never migrates
production or cleans `public`.

From `frontend/`:

```text
node --experimental-strip-types --test test/landing-keyword-auth-flow.test.ts test/design-system-hero.test.ts
npm run check
ALLOW_DATABASE_TESTS=true node test/browser/landing-keyword-auth-flow.mjs
git diff --check
```

The emitted-browser command performs one Next build only if `npm run check`'s
frozen build cannot be reused by exact hash. It creates/drops one disposable
schema in `finally`, uses local auth/queue/provider substitutes, and performs no
AWS/provider/paid action.

Any source/test/fixture/migration edit after a frozen gate invalidates the
applicable gate and requires rerun. Environment-only listener denial permits
one identical escalated recovery under the authoring standard after read-only
postconditions prove no surviving process, schema, mutation, or usable result.

## 11. Rollout, compatibility, and recovery

1. Apply the forward migration before deploying backend code that references
   `KeywordResearchIntent`. Production migration/deployment requires its own
   existing approval process and is not authorized here.
2. Deploy backend service support before frontend. Until frontend ships, current
   landing behavior remains unchanged; the new backend endpoints are dormant.
3. Deploy frontend. New landing submissions then use keyword research; existing
   legacy pending cookies still claim through the fallback.
4. Do not enable/alter any keyword queue or worker mapping for this change. The
   already-deployed queued-research recovery covers post-claim send loss.
5. Rollback frontend alone restores legacy landing creation while backend/model
   additions remain harmless. Rollback backend while new frontend is active is
   forbidden; restore frontend first.
6. The migration is additive and is not rolled back destructively. No intent,
   research, Run, or historical row is deleted during rollback.
7. A future removal of legacy landing APIs/cookies is parked and requires a new
   usage/compatibility decision. It is not part of this execution sequence.

## 12. Mechanical traces and decision audit

| Trace | Source -> change -> target -> caller -> assertion |
|---|---|
| `LKAI-TRACE-001` | `RunForm.submit` direct `/api/runs` -> existing `createKeywordResearch` -> keyword BFF -> signed-in backend create -> FE-01/BE-03 |
| `LKAI-TRACE-002` | private `parseKeywordLines` -> `parseKeywordSeedText` -> both forms -> boundary tests -> FE-01/02 |
| `LKAI-TRACE-003` | keyword BFF auth-only branch -> session branch + intent proxy -> backend createIntent -> cookie/401 -> FE-03/BE-01 |
| `LKAI-TRACE-004` | `AuthForm` unchanged `/runs/continue` -> dual claim BFF -> backend claimIntent transaction -> research -> post-commit send -> FE-04/BE-04/DB-02 |
| `LKAI-TRACE-005` | legacy claim BFF -> discriminated wrapper -> RunContinuation fixed `/runs` navigation -> FE-06 |
| `LKAI-TRACE-006` | claim response loss -> durable mapping -> same-owner found -> strict wrapper -> same `/keywords` navigation -> FE-05/BE-05 |
| `LKAI-TRACE-007` | intent expiry/foreign owner -> repository not_found -> backend safe 404 -> BFF cookie deletion -> continuation home -> BE-06/FE-08 |
| `LKAI-TRACE-008` | created research send failure -> queued row -> existing repository recover -> existing recovery message -> BE-07 |
| `LKAI-TRACE-009` | landing DOM source -> submit-only rewiring -> same structural classes/CTA -> emitted three-viewport inspection -> FE-09 |

| Decision category | Locked choice | Implementing task | Verification |
|---|---|---|---|
| Files and symbols | Exact §6 path/symbol map; protected set byte-unchanged | W1-T1–T6, W2-T1–T7 | diff/set-equality gates |
| Interfaces/dependencies | Exact §4 signatures/unions; no new package | W1-T2–T4, W2-T1–T4 | BE/FE strict contract cases |
| Data/transactions | Dedicated model; claim+research same transaction; dispatch recovered | W1-T1–T3 | DB-01–04, BE-07 |
| Failure/retry/limits | one-hour TTL, 1–5×100cp, same-owner replay, foreign 404, queued recovery | W1-T2–T5, W2-T1–T6 | BE-02/05–07, FE-02/05/08 |
| Cross-window output | W1 response/migration contract consumed unchanged by W2 | W1 handoff, W2 preconditions | fixture hash + emitted causal flow |

## 13. Authoring closure and adoption gate

Resolved implementation unknowns: **0**.

External payload unknowns: **0**.

Planned required coverage cases: **21**; unmapped: **0**; duplicates: **0**.

Critical invariants: **7**; negative controls: **7**; unresolved controls: **0**.

Test substitutes: **5**; unresolved fidelity dispositions: **0**.

Predictable requester actions before local implementation: **none after formal
successor assignment**. Production migration/deployment remains a separate
future approval boundary.

The only current blocker to assignment is coordination authority: the live
state still assigns `KI-W8-C201` and the conforming A1–A8 successor package has
not yet adopted this requirement. A parent adoption pass must:

- append new stable requirements to A1;
- append the observed evidence rows to A2;
- append decisions `LKAI-DEC-001`–`017` to A3;
- append these two windows/checklists/case matrices to A4;
- append authoring evidence and the readiness certificate to A6;
- append one specification-change record to A7;
- append traces `LKAI-TRACE-001`–`009` to A8;
- hash A1/A3/A4 and create a new A5 assignment for `LKAI-W1`; and
- preserve all prior accepted evidence unless a named changed test is explicitly
  invalidated and superseded.

Until that pass occurs, status is `DECISION-COMPLETE / NOT ASSIGNABLE`. After
the pass reports zero unresolved references and the live state authorizes
`LKAI-W1`, the first implementation agent has no remaining design choice.

## 14. Independent final review

After W1 and W2 are accepted, a parent reviewer who did not rely on the
implementation handoff must:

- inspect the complete current diff and exact protected-file set;
- rerun the risk-proportionate frozen cases and all seven controls;
- independently recompute required/registered/executed case IDs and digest;
- trace anonymous submit to intent with zero research/send/provider action;
- trace authenticated claim through one transaction to one post-commit send;
- schedule same-owner and different-owner concurrency against real isolated
  PostgreSQL;
- verify signed-in direct creation and legacy continuation still work;
- verify emitted landing structure at all three viewports;
- verify the migration is additive and historical data unchanged;
- verify no raw seeds appear in cookies, URLs, logs, SQS, fixtures, or auth
  payloads; and
- limit all deployment/live claims to separately approved evidence.

Overall completion requires all 21 cases, all seven controls, W1/W2 handoffs,
and independent review to pass with no unaccepted corrective window.
