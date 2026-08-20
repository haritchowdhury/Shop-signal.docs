# KI-R5 Sub-Window Evidence (`S3`)

Append-only evidence for parent window `KI-R5` (assignment `ASG-KI-R5-WA-01`,
window agent `KI-R5-WINDOW-AGENT`). Entries are never edited or deleted;
corrections append new entries. Implementation-leaf evidence is appended here
only by the window agent after independent review; subagent summaries are not
evidence. Sibling artifacts: `KEYWORD_INTELLIGENCE_KI_R5_SUBWINDOW_CHECKLIST.md`
(`S1`, current revision
`cc603020b65343f71d48457b275afbff526a179592805bf6a7c337a9b48d3b83`; see
the append-only S1 revision records) and
`KEYWORD_INTELLIGENCE_KI_R5_SUBWINDOW_STATE.md` (`S2`).

---

## EV-KI-R5-S01 — Decomposition entry gate and starting-state inventory

- **Evidence ID / timestamp:** `EV-KI-R5-S01` / 2026-08-20T10:45:00+05:30.
- **Parent window / assignment:** `KI-R5` / `ASG-KI-R5-WA-01`.
- **Actor / role:** `KI-R5-WINDOW-AGENT` / window agent (decomposition author).
- **Frozen revisions at inspection:** parent standard
  `3b7a4fd25156e1adfbc92abb835c5f82a0d18c686b1c1150feb202f2d944d2ac`;
  sub-window standard
  `1766f9107ce7d315877b75d4b0ea2b5521dff1c321e12f890b03787d66196ded`;
  contract `8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c`;
  decision ledger
  `e8ed580dd08b77540158340c47fae84c5d56b18cc7aba3149ccc2ab568493f5d`;
  checklist
  `4f52bf764525927fd7b68c0795aec5cbbd15f1a8b9b73778d446cfd87e2b94b8`;
  `ACTIVE_EXECUTION_STATE.md` state_version 112 (A5 file digest
  `15b5e62e82afd39be1b5dd6e9043fb254f8341f62e6d298be199a45fb00ddc2e` at
  inspection).
- **Exact inspections performed:** `sha256sum` of the five pinned artifacts —
  all five equal the A5 state-112 pins (entry-gate items 1–3 pass);
  `git -C email_scraper rev-parse HEAD` →
  `fac5bb0f0a4e9c04873c9d338794762d44e35f7f` with empty `status --porcelain`
  (clean; equals A4 `KI-R5-P2`); `git -C frontend rev-parse HEAD` →
  `c85f93b4bc66e1c130401227e46b488c6fe13c94` clean (equals A4 `KI-R5-P2`);
  root `git status --porcelain` → 42 owner-controlled relocation entries,
  `LC_ALL=C` sorted per-line-LF digest
  `3631850a6b226e11205baaafc05fa4fdd22372d1ed7f9f3d1763330d801eefbd`,
  inventoried unmodified.
- **Starting file digests:** the 16 existing paths and 2 `ABSENT` states
  recorded verbatim in `S1` §2; per-member-LF `LC_ALL=C` sorted digest of the
  18 paths recomputed =
  `efc82a884d09561ed27be3513ca6898f0ab311dbe56cf46e9c2c241492560077`, equal to
  the A4 `delegable_file_set_digest`.
- **Decisive assertions:** A5 state 112 names this window agent and only
  `KI-R5` with `accepted_through:KI-W5`, `next_window:KI-W6`,
  `stop_after:KI-R5`, `may_start_successor:false`; delegation to sequential
  single-file leaves under the sub-window standard is authorized by the A4
  `KI-R5` `delegation_policy`; parent window is `READY` for decomposition;
  write/read/action/prohibition scopes are exact in A4/A5; no unrelated
  owner-controlled change exists inside the 18 paths; no required action
  exceeds parent authority.
- **Changed path set of this entry:** none (read-only inspection).
- **Coverage cases:** none applicable (decomposition entry).
- **Negative control:** none required.
- **Limitations / deferred checks:** all behavioral gates deferred to leaves
  and `S1` §6.
- **External mutations / costs:** none / `$0.00`.
- **Review disposition:** accepted by the window agent as the decomposition
  baseline (`SW-A01`–`A04`, `SW-D03`).

## EV-KI-R5-S02 — Parent-scope verification (P3 equivalent, read-only)

- **Evidence ID / timestamp:** `EV-KI-R5-S02` / 2026-08-20T10:50:00+05:30.
- **Actor / role:** `KI-R5-WINDOW-AGENT` / window agent.
- **Frozen revisions:** as `EV-KI-R5-S01`.
- **Exact inspections performed (read-only source reproduction of
  `KI-PR-F01`–`F09` at the cited anchors):**
  - **F01:** `api-serializer.js:1060–1072` serializes persisted
    `research.contractVersion`; `schemas.js:139–148` result schema requires
    `z.literal(1)`; `types.ts:175/210` declare `contractVersion: string`;
    `validation.ts:518/731` use `nonEmptyText`; fixtures
    `api.test.ts:184–190/242–249` use `"ki-research-v1"` — reproduced.
  - **F02:** `client-api.ts:20–32` sets only `Accept`; the three mutation
    methods (`:56–60`, `:72–80`, `:84–95`) send string bodies without
    Content-Type; the Next selection route (`route.ts:10–24`) returns 415
    before auth; browser harness (`:647–697`) replaces `globalThis.fetch` —
    reproduced.
  - **F03:** `selection-review.tsx:57–79` salted FNV-like `ksi_` derivation vs
    `selection.js:12–20` + `dedup.js:48–51` BLAKE2s six-byte `selectionItemId`
    (W4 `api.js:236–247`) — algorithms differ — reproduced.
  - **F04:** backend `server.js:1786` default `readJsonBody` (32 KiB per
    `request-json.js:3–5`) vs Next route `MAX_BODY_BYTES = 262144` —
    reproduced.
  - **F05:** `research-dashboard.tsx:205–238` local draft save vs
    `handleFinalize:240–255` sending only `view.selectionRevision`;
    `view-model.ts:646–654` has no unsaved reason — reproduced.
  - **F06:** `handleFinalize` catch clears `clientRequestIdRef.current = null`
    for every error; `repository.js:1232–1275` has no unique-race
    reconciliation after the in-transaction handoff read;
    `handoff.integration.test.js:439–447` asserts only `fulfilled.length >= 1`
    — reproduced.
  - **F07:** `view-model.ts:185–216` haystack includes `mainIntent` and
    synthetic `recommended`, flags use `.some`; `api.js:350–390` uses `.every`
    and omits those corpus fields — reproduced.
  - **F08:** `api.js:445–465` `saveSelection` never calls
    `validateSelectionDraft`; `selection.js:190–200` conflict analysis silently
    deduplicates; `query-mapper.js:32–46` rejects duplicate IDs at handoff —
    reproduced.
  - **F09:** `export.js:3–10` `csvEscape` quotes only comma/quote/newline;
    `serializeKeywordsCsv:188–208` applies no apostrophe neutralization —
    reproduced.
  - **PAY-KI-008:** present and complete in `DEC-KI-034` (decision ledger
    lines 1614–1620) — verified.
  - **KI-W6 status:** `KEYWORD_INTELLIGENCE_KI_W6_SUBWINDOW_STATE.md` shows
    `current_subwindow: NONE`, S001/S002/I001 `NOT_STARTED`, accepted 0/2, and
    pinned revisions `decision c2dc635e…` / `parent_checklist 324667cb…` that
    differ from the current A5 pins (`e8ed580d…` / `4f52bf76…`) — the prior W6
    decomposition is revision-invalidated, not edited, and no KI-W6 leaf was
    assigned or executed; A7 changelog records the R5 authoring corrections.
    Verified against `SRC-KI-037`.
- **Decisive assertions:** every parent finding is real against current
  source; the consumed decisions are complete; the 18-path change set is
  derivable from the findings and decisions (entry-gate items 6–7).
- **Changed path set:** none (read-only).
- **Coverage cases:** none (verification of parent trace).
- **Limitations:** dynamic reproductions were already performed and recorded
  by parent review `KI-PR-W4-W5-01`; this entry is the read-only
  reproduction-against-current-source required before authoring.
- **External mutations / costs:** none / `$0.00`.
- **Review disposition:** accepted (`SW-D01`, `SW-D02` inputs).

## EV-KI-R5-S03 — Decomposition authored; readiness certificate

- **Evidence ID / timestamp:** `EV-KI-R5-S03` / 2026-08-20T11:05:00+05:30.
- **Actor / role:** `KI-R5-WINDOW-AGENT` / window agent.
- **Frozen revisions:** as `EV-KI-R5-S01`; `S1` revision
  `6c08cb090f7b3e293c39eb4ecb9085a746e51df22a0433f29ead370317a92a0b`.
- **Actions performed:** authored `S1` (§0 authority + six recorded
  interpretations; §1 verbatim parent scope; §2 18-file inventory with
  digests; §3 DAG + interface freeze + intermediate-state contracts; §4
  allocation maps incl. supersession sets; §5 eighteen complete Section-7
  sub-window blocks S001–S018; §6 frozen gates V1–V7 + final merge; §7
  correction rules; §8 all 44 `SW-*` items checked; §9 handoff templates;
  §10 fully authored `KI-R5-I001`; §11 append-only amendments; §12 twenty
  counterexamples); authored `S2` (status
  `AWAITING_PARENT_DECOMPOSITION_REVIEW`, no leaf assigned, next
  `KI-R5-S001`); appended this evidence file and the certificate below.
- **Mechanical lint results:** sub-window IDs unique (S001–S018); file blocks
  ↔ planned files bijective (18/18); every block lists exactly one canonical
  writable file path (no glob/directory/second path); every A4 `KI-R5` task,
  scenario (`SCN-KI-036`–`040`), and coverage case (34 IDs + 12 controls +
  supersession/rerun sets) allocated with zero unmapped; no unresolved
  placeholder in any assignable block; DAG acyclic with named interface edges;
  global digest `507186e7…` and group digests embedded as literals for S017.
- **Decisive assertions:** the decomposition satisfies decision-complete,
  execution-complete, and enforcement-complete definitions for every
  sub-window; the self-falsification of `S1` §12 shows each of the standard's
  twenty counterexamples is rejected by these rules.
- **Changed path set of the window agent (authorized coordination writes
  only):** `KEYWORD_INTELLIGENCE_KI_R5_SUBWINDOW_CHECKLIST.md` (CREATE),
  `KEYWORD_INTELLIGENCE_KI_R5_SUBWINDOW_STATE.md` (CREATE),
  `KEYWORD_INTELLIGENCE_KI_R5_SUBWINDOW_EVIDENCE.md` (CREATE).
- **Coverage cases:** none executed (no leaf ran).
- **Limitations / deferred checks:** every V-gate and the final merge are
  deferred to `KI-R5-I001`; no implementation file was read-modified-written
  by the window agent.
- **External mutations / costs:** none / `$0.00`.
- **Review disposition:** decomposition complete; parent decomposition review
  required before any leaf assignment.

### Certificate

```yaml
certificate: SUBWINDOW-DECOMPOSITION-READY
parent_window_id: KI-R5
parent_assignment_id: ASG-KI-R5-WA-01
window_agent_identity: KI-R5-WINDOW-AGENT
revisions:
  parent_standard: 3b7a4fd25156e1adfbc92abb835c5f82a0d18c686b1c1150feb202f2d944d2ac
  subwindow_standard: 1766f9107ce7d315877b75d4b0ea2b5521dff1c321e12f890b03787d66196ded
  contract: 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c
  decision: e8ed580dd08b77540158340c47fae84c5d56b18cc7aba3149ccc2ab568493f5d
  parent_checklist: 4f52bf764525927fd7b68c0795aec5cbbd15f1a8b9b73778d446cfd87e2b94b8
  decomposition: 6c08cb090f7b3e293c39eb4ecb9085a746e51df22a0433f29ead370317a92a0b
initial_subwindow_ids: [KI-R5-S001, KI-R5-S002, KI-R5-S003, KI-R5-S004, KI-R5-S005, KI-R5-S006, KI-R5-S007, KI-R5-S008, KI-R5-S009, KI-R5-S010, KI-R5-S011, KI-R5-S012, KI-R5-S013, KI-R5-S014, KI-R5-S015, KI-R5-S016, KI-R5-S017, KI-R5-S018]
initial_subwindow_count: 18
planned_file_set: [email_scraper/src/keyword-intelligence/api.js, email_scraper/src/keyword-intelligence/repository.js, email_scraper/src/keyword-intelligence/export.js, email_scraper/src/server.js, email_scraper/test/keyword-intelligence-api.test.js, email_scraper/test/keyword-intelligence-handoff.integration.test.js, email_scraper/test/fixtures/keyword-intelligence/ki-r5-enforcement-manifest-v1.json, email_scraper/test/keyword-intelligence-r5-enforcement.test.js, frontend/lib/keyword-intelligence-types.ts, frontend/lib/keyword-intelligence-validation.ts, frontend/lib/client-api.ts, frontend/lib/keyword-intelligence-view-model.ts, frontend/components/keyword-intelligence/research-dashboard.tsx, frontend/components/keyword-intelligence/selection-review.tsx, frontend/test/keyword-intelligence-api.test.ts, frontend/test/keyword-intelligence-components.test.ts, frontend/test/keyword-intelligence-inventory.test.ts, frontend/test/browser/keyword-intelligence-dashboard.mjs]
planned_file_set_digest: efc82a884d09561ed27be3513ca6898f0ab311dbe56cf46e9c2c241492560077
unmapped_parent_requirements: []
unmapped_parent_decisions: []
unmapped_parent_tasks: []
unmapped_coverage_cases: []
duplicate_initial_file_owners: []
multi_file_subwindows: []
unresolved_interfaces: []
unresolved_intermediate_states: []
unresolved_execution_choices: []
unresolved_evidence_references: []
mandatory_authoring_items_checked: 44
mandatory_authoring_items_unchecked: 0
first_subwindow: KI-R5-S001
integration_assessment_id: KI-R5-I001
parent_review_required: true
```

## EV-KI-R5-C006-02 — corrected one-path planned-set digest

- **Correction:** the readiness certificate in `EV-KI-R5-C006-01` transcribed
  an incorrect `planned_file_set_digest`. The literal one-path set has now been
  mechanically recomputed as the UTF-8 bytes of
  `email_scraper/test/keyword-intelligence-r5-enforcement.test.js` plus LF:
  SHA-256 `2b272324c43a1f4120f0ece14c4579fac819c8702fc0feb94b4f1db61661b5de`.
  No C006/I003 requirement, file, baseline, control, gate, status, or authority
  changes; this entry supersedes only that erroneous certificate field.

```yaml
certificate: SUBWINDOW-DECOMPOSITION-READY-CORRECTION
parent_window_id: KI-R5
parent_assignment_id: ASG-KI-R5-WA-01
window_agent_identity: KI-R5-WINDOW-AGENT
decomposition: a8d888915d2db01bd44e8537627b89995b23632198737df0e45e8a0b4b78f810
corrected_field: planned_file_set_digest
planned_file_set: [email_scraper/test/keyword-intelligence-r5-enforcement.test.js]
planned_file_set_digest: 2b272324c43a1f4120f0ece14c4579fac819c8702fc0feb94b4f1db61661b5de
supersedes: EV-KI-R5-C006-01 planned_file_set_digest only
parent_review_required: true
```

**Stop point:** `S2.decomposition_status = AWAITING_PARENT_DECOMPOSITION_REVIEW`.
No leaf is assigned or dispatched. Only the parent may approve this
decomposition; upon approval, only the window agent sets `S2` to `READY` and
assigns `ASG-KI-R5-S001`.

---

## EV-KI-R5-S04 — Parent decomposition findings applied; revised decomposition

- **Evidence ID / timestamp:** `EV-KI-R5-S04` / 2026-08-20T11:55:00+05:30.
- **Parent window / assignment:** `KI-R5` / `ASG-KI-R5-WA-01`.
- **Actor / role:** `KI-R5-WINDOW-AGENT` / window agent (revision author).
- **Frozen revisions:** unchanged from `EV-KI-R5-S01` (parent standard,
  sub-window standard, contract, decision, checklist; A5 state 112 — the
  parent directed that A5 requires no change and was not touched).
- **Trigger:** parent decomposition review returned "not approved for leaf
  execution" with seven executable defects and interpretation adjudications
  (items 2/4/5 accepted; item 1 rejected as written; items 3 and 6 corrected).
  Recorded verbatim-by-reference in `S1` §11.3.
- **Verification performed before revision (read-only):** current root
  `git status --porcelain` = 45 entries, digest
  `c660d09a800e8a5fd446bd65039f55241d5d7bb4e4c7ef656fe4fc7dcc88417c`
  (finding 1 confirmed — the S001 literal `3631850a…` was the stale
  pre-authoring 42-entry value; my three subordinate artifacts added three
  entries); `api.js:61` uses `z.number().int().nonnegative()` (finding 3
  confirmed); `SelectionItem.sourceKeywordId: string | null`
  (`types.ts:247`, finding 4 confirmed); from `frontend/test/`, the serializer
  import requires `../../email_scraper/...` (finding 2 confirmed);
  `SelectionReviewProps` at `selection-review.tsx:26` with the narrow
  `finalizeState` today (finding 5 confirmed).
- **Exact revisions applied to `S1` (old rev `6c08cb09…` → new rev
  `841e235fd74e65a4d3ab1ca40fe6ac96717e3ef753a1cce2b34d573e76a4f3ae`):**
  1. §2 and §5 S001 now pin the current 45-entry digest `c660d09a…` with an
     authoritative dispatch-time recompute note; §8 `SW-A04` citation updated.
  2. §0.1 item 6 and §5 S013 `read_only_scope` corrected to
     `../../email_scraper/src/api-serializer.js`.
  3. §5 S001 step 1 prescribes the explicit change of line 61 from
     `z.number().int().nonnegative()` to `z.number().int().min(1)`.
  4. §0.1 item 3, §3.1, §5 S009 step 2, and §5 S010 step 1 freeze the exact
     calculated-item guard (validated non-empty string or throw
     `"calculated selection item requires a source id"`) before
     `SelectionMutationItem` construction.
  5. §3.1 freezes the expanded prop/state contract (literals `"idle" |
     "handing-off" | "succeeded" | "definitive_failure" | "retry_required"`,
     `onRetryHandoff` prop, inert/disabled rules, retry notice, exact
     succeeded/definitive_failure transitions); §5 S011 owns the
     type/rendering side and §5 S012 owns the state machine, retry handler,
     and wiring.
  6. §5 S016 lint corrected: every discovered R5 reference must belong to the
     exact owning registry; no undeclared ID.
  7. §0.1 item 1, §3.2 (S018 row), §4.2, §5 S018, §6 (V1–V7 plus single E1
     row), and §10 (I001 inputs/gates) revised to: six execution registries;
     five non-conformance certificates captured at V1/V2/V3/V4; S018
     leaf-time checks limited to syntax/static plus synthetic NC-12; the
     enforcement test executes exactly once during `KI-R5-I001` with all five
     certificates, merges all 34 IDs, and emits the final merged certificate.
- **Decisive assertions:** all seven defects are eliminated in the revised
  `S1`; no parent decision, scope, boundary, case set, digest literal, or
  supersession rule changed; the 18-file plan, sub-window IDs, DAG order,
  interface freeze coverage, and 44/44 `SW-*` closure remain intact; the
  earlier `SUBWINDOW-DECOMPOSITION-READY` certificate in `EV-KI-R5-S03` is
  superseded (not erased) by the certificate below.
- **Changed path set of this entry (authorized coordination writes only):**
  `KEYWORD_INTELLIGENCE_KI_R5_SUBWINDOW_CHECKLIST.md` (revised),
  `KEYWORD_INTELLIGENCE_KI_R5_SUBWINDOW_STATE.md` (state 2),
  `KEYWORD_INTELLIGENCE_KI_R5_SUBWINDOW_EVIDENCE.md` (this entry).
- **Coverage cases:** none executed (no leaf ran).
- **Limitations / deferred checks:** all behavioral gates deferred to leaves
  and `S1` §6/E1 as revised.
- **External mutations / costs:** none / `$0.00`.
- **Review disposition:** revision complete; returned to
  `AWAITING_PARENT_DECOMPOSITION_REVIEW`; no leaf dispatched.

### Certificate (supersedes the certificate in `EV-KI-R5-S03`)

```yaml
certificate: SUBWINDOW-DECOMPOSITION-READY
parent_window_id: KI-R5
parent_assignment_id: ASG-KI-R5-WA-01
window_agent_identity: KI-R5-WINDOW-AGENT
revisions:
  parent_standard: 3b7a4fd25156e1adfbc92abb835c5f82a0d18c686b1c1150feb202f2d944d2ac
  subwindow_standard: 1766f9107ce7d315877b75d4b0ea2b5521dff1c321e12f890b03787d66196ded
  contract: 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c
  decision: e8ed580dd08b77540158340c47fae84c5d56b18cc7aba3149ccc2ab568493f5d
  parent_checklist: 4f52bf764525927fd7b68c0795aec5cbbd15f1a8b9b73778d446cfd87e2b94b8
  decomposition: 841e235fd74e65a4d3ab1ca40fe6ac96717e3ef753a1cce2b34d573e76a4f3ae
initial_subwindow_ids: [KI-R5-S001, KI-R5-S002, KI-R5-S003, KI-R5-S004, KI-R5-S005, KI-R5-S006, KI-R5-S007, KI-R5-S008, KI-R5-S009, KI-R5-S010, KI-R5-S011, KI-R5-S012, KI-R5-S013, KI-R5-S014, KI-R5-S015, KI-R5-S016, KI-R5-S017, KI-R5-S018]
initial_subwindow_count: 18
planned_file_set: [email_scraper/src/keyword-intelligence/api.js, email_scraper/src/keyword-intelligence/repository.js, email_scraper/src/keyword-intelligence/export.js, email_scraper/src/server.js, email_scraper/test/keyword-intelligence-api.test.js, email_scraper/test/keyword-intelligence-handoff.integration.test.js, email_scraper/test/fixtures/keyword-intelligence/ki-r5-enforcement-manifest-v1.json, email_scraper/test/keyword-intelligence-r5-enforcement.test.js, frontend/lib/keyword-intelligence-types.ts, frontend/lib/keyword-intelligence-validation.ts, frontend/lib/client-api.ts, frontend/lib/keyword-intelligence-view-model.ts, frontend/components/keyword-intelligence/research-dashboard.tsx, frontend/components/keyword-intelligence/selection-review.tsx, frontend/test/keyword-intelligence-api.test.ts, frontend/test/keyword-intelligence-components.test.ts, frontend/test/keyword-intelligence-inventory.test.ts, frontend/test/browser/keyword-intelligence-dashboard.mjs]
planned_file_set_digest: efc82a884d09561ed27be3513ca6898f0ab311dbe56cf46e9c2c241492560077
unmapped_parent_requirements: []
unmapped_parent_decisions: []
unmapped_parent_tasks: []
unmapped_coverage_cases: []
duplicate_initial_file_owners: []
multi_file_subwindows: []
unresolved_interfaces: []
unresolved_intermediate_states: []
unresolved_execution_choices: []
unresolved_evidence_references: []
mandatory_authoring_items_checked: 44
mandatory_authoring_items_unchecked: 0
first_subwindow: KI-R5-S001
integration_assessment_id: KI-R5-I001
parent_review_required: true
```

**Stop point (unchanged):** `S2.decomposition_status =
AWAITING_PARENT_DECOMPOSITION_REVIEW`. No leaf is assigned or dispatched.
Supersedes the certificate appended in `EV-KI-R5-S03`, which remains as
history. Only the parent may approve; upon approval, only the window agent
sets `S2` to `READY` and assigns `ASG-KI-R5-S001`.

---

## EV-KI-R5-S05 — Second parent review: two residual defects applied

- **Evidence ID / timestamp:** `EV-KI-R5-S05` / 2026-08-20T12:20:00+05:30.
- **Parent window / assignment:** `KI-R5` / `ASG-KI-R5-WA-01`.
- **Actor / role:** `KI-R5-WINDOW-AGENT` / window agent (revision author).
- **Frozen revisions:** unchanged from `EV-KI-R5-S01` (parent standard,
  sub-window standard, contract, decision, checklist; A5 state 112 — parent
  directed no A5 change and none was made).
- **Trigger:** second parent decomposition review confirmed the seven
  first-round findings resolved and returned two residual defects; recorded
  in `S1` §11.3 second-review block.
- **Verification performed before revision (read-only):** recomputed the
  non-conformance subtotals from the A4 manifest groups — wire 6 + selection
  8 + finalization 8 + export 6 = **28** (defect 1 confirmed: `S1` said 29);
  inspected the S011 LOCAL_NOW oracle text (defect 2 confirmed: it keyed
  disabled logic off `"handing-off"` and `"retry_required"` only, omitting
  `"succeeded"`, while the S011 transformation itself disables everything in
  `"succeeded"`).
- **Exact revisions applied to `S1` (rev `841e235f…` → rev
  `6ff7830adc72874a3c30a2000ec96f32a668fba230fe652260d83ad2cab9500f`):**
  1. §5 S018: "merge the 29 executed non-conformance IDs" → "merge the 28
     executed non-conformance IDs (wire 6 + selection 8 + finalization 8 +
     export 6) with the six executed conformance IDs" = 34.
  2. §5 S011 LOCAL_NOW: disabled logic now verified for all three disabling
     states (`"handing-off"`, `"retry_required"`, `"succeeded"`, with
     `"succeeded"` disabling everything); §3.1 frozen contract and S011
     transformation step 2 clarify that `"definitive_failure"` adds no
     state-based control lock while the existing accepted-W5 409
     `staleConflict` lock continues to apply unchanged.
  3. §11.3 second-review record appended.
- **Decisive assertions:** both defects eliminated; no other `S1` content,
  parent decision, scope, boundary, case set, digest literal, or
  supersession rule changed; the 18-file plan, sub-window IDs, DAG order,
  interface freeze, six-registry/E1 enforcement flow, and 44/44 `SW-*`
  closure remain intact; the `EV-KI-R5-S04` certificate is superseded (not
  erased) by the certificate below.
- **Changed path set of this entry (authorized coordination writes only):**
  `KEYWORD_INTELLIGENCE_KI_R5_SUBWINDOW_CHECKLIST.md` (revised),
  `KEYWORD_INTELLIGENCE_KI_R5_SUBWINDOW_STATE.md` (state 3),
  `KEYWORD_INTELLIGENCE_KI_R5_SUBWINDOW_EVIDENCE.md` (this entry).
- **Coverage cases:** none executed (no leaf ran).
- **Limitations / deferred checks:** all behavioral gates deferred to leaves
  and `S1` §6/E1.
- **External mutations / costs:** none / `$0.00`.
- **Review disposition:** revision complete; returned once more to
  `AWAITING_PARENT_DECOMPOSITION_REVIEW`; no leaf dispatched; no A5 change.

### Certificate (supersedes the certificates in `EV-KI-R5-S03`/`EV-KI-R5-S04`)

```yaml
certificate: SUBWINDOW-DECOMPOSITION-READY
parent_window_id: KI-R5
parent_assignment_id: ASG-KI-R5-WA-01
window_agent_identity: KI-R5-WINDOW-AGENT
revisions:
  parent_standard: 3b7a4fd25156e1adfbc92abb835c5f82a0d18c686b1c1150feb202f2d944d2ac
  subwindow_standard: 1766f9107ce7d315877b75d4b0ea2b5521dff1c321e12f890b03787d66196ded
  contract: 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c
  decision: e8ed580dd08b77540158340c47fae84c5d56b18cc7aba3149ccc2ab568493f5d
  parent_checklist: 4f52bf764525927fd7b68c0795aec5cbbd15f1a8b9b73778d446cfd87e2b94b8
  decomposition: 6ff7830adc72874a3c30a2000ec96f32a668fba230fe652260d83ad2cab9500f
initial_subwindow_ids: [KI-R5-S001, KI-R5-S002, KI-R5-S003, KI-R5-S004, KI-R5-S005, KI-R5-S006, KI-R5-S007, KI-R5-S008, KI-R5-S009, KI-R5-S010, KI-R5-S011, KI-R5-S012, KI-R5-S013, KI-R5-S014, KI-R5-S015, KI-R5-S016, KI-R5-S017, KI-R5-S018]
initial_subwindow_count: 18
planned_file_set: [email_scraper/src/keyword-intelligence/api.js, email_scraper/src/keyword-intelligence/repository.js, email_scraper/src/keyword-intelligence/export.js, email_scraper/src/server.js, email_scraper/test/keyword-intelligence-api.test.js, email_scraper/test/keyword-intelligence-handoff.integration.test.js, email_scraper/test/fixtures/keyword-intelligence/ki-r5-enforcement-manifest-v1.json, email_scraper/test/keyword-intelligence-r5-enforcement.test.js, frontend/lib/keyword-intelligence-types.ts, frontend/lib/keyword-intelligence-validation.ts, frontend/lib/client-api.ts, frontend/lib/keyword-intelligence-view-model.ts, frontend/components/keyword-intelligence/research-dashboard.tsx, frontend/components/keyword-intelligence/selection-review.tsx, frontend/test/keyword-intelligence-api.test.ts, frontend/test/keyword-intelligence-components.test.ts, frontend/test/keyword-intelligence-inventory.test.ts, frontend/test/browser/keyword-intelligence-dashboard.mjs]
planned_file_set_digest: efc82a884d09561ed27be3513ca6898f0ab311dbe56cf46e9c2c241492560077
unmapped_parent_requirements: []
unmapped_parent_decisions: []
unmapped_parent_tasks: []
unmapped_coverage_cases: []
duplicate_initial_file_owners: []
multi_file_subwindows: []
unresolved_interfaces: []
unresolved_intermediate_states: []
unresolved_execution_choices: []
unresolved_evidence_references: []
mandatory_authoring_items_checked: 44
mandatory_authoring_items_unchecked: 0
first_subwindow: KI-R5-S001
integration_assessment_id: KI-R5-I001
parent_review_required: true
```

**Stop point (unchanged):** `S2.decomposition_status =
AWAITING_PARENT_DECOMPOSITION_REVIEW`. No leaf is assigned or dispatched.
Supersedes the certificates in `EV-KI-R5-S03`/`EV-KI-R5-S04`, which remain as
history. Only the parent may approve; upon approval, only the window agent
sets `S2` to `READY` and assigns `ASG-KI-R5-S001`.

---

## EV-KI-R5-S06 — Parent decomposition approval; S2 READY; S001 staged

- **Evidence ID / timestamp:** `EV-KI-R5-S06` / 2026-08-20T12:40:00+05:30.
- **Parent window / assignment:** `KI-R5` / `ASG-KI-R5-WA-01`.
- **Actor / role:** `KI-R5-WINDOW-AGENT` / window agent (approval converter
  and dispatch coordinator).
- **Frozen revisions:** unchanged from `EV-KI-R5-S01`; approved `S1`
  revision
  `6ff7830adc72874a3c30a2000ec96f32a668fba230fe652260d83ad2cab9500f`.
- **Activation witness:** the requester relayed the parent's approval of the
  revised decomposition ("parent agent approved the window plan"). This entry
  converts that approval per the sub-window standard §12.1: only the window
  agent may set `S2.decomposition_status: READY`.
- **Actions performed:** `S2` advanced to state 4 — `decomposition_status:
  READY`; `current_subwindow: KI-R5-S001`; `current_assignment_id:
  ASG-KI-R5-S001`; per-leaf scope staged from `S1` §5 S001; `next_subwindow:
  KI-R5-S001` (dispatch in progress). `S1` §11.3 approval record appended.
- **Dispatch-time verification (read-only):** root `git status --porcelain`
  = 45 entries, `LC_ALL=C` per-line-LF digest
  `c660d09a800e8a5fd446bd65039f55241d5d7bb4e4c7ef656fe4fc7dcc88417c`
  (unchanged — S1/S2/S3 content revisions do not alter the path set; this is
  the authoritative value for the S001 preflight per `S1` §2 dispatch note);
  nested repositories clean at `fac5bb0f` / `c85f93b`.
- **Decisive assertions:** parent approval received for `S1` rev
  `6ff7830a…`; the approved plan is the 18-leaf sequential DAG plus
  `KI-R5-I001` (window agent); no parent decision was invented or broadened;
  A5/A4/A3 remain untouched by this window (A5 state 112, digest
  `15b5e62e…`).
- **Changed path set of this entry (authorized coordination writes only):**
  `KEYWORD_INTELLIGENCE_KI_R5_SUBWINDOW_STATE.md` (state 4),
  `KEYWORD_INTELLIGENCE_KI_R5_SUBWINDOW_EVIDENCE.md` (this entry),
  `KEYWORD_INTELLIGENCE_KI_R5_SUBWINDOW_CHECKLIST.md` (§11.3 approval record
  only).
- **Coverage cases:** none executed yet; leaf execution begins with
  `ASG-KI-R5-S001`.
- **External mutations / costs:** none / `$0.00`.
- **Review disposition:** accepted; `S2` is `READY`; dispatch of
  `ASG-KI-R5-S001` may begin immediately, strictly one leaf at a time in the
  `S1` §3 order, each stopping at `AWAITING_WINDOW_REVIEW` for independent
  window-agent review before the next dispatch.

---

## EV-KI-R5-S07 — S001 leaf executed; window-agent review: ACCEPTED

- **Evidence ID / timestamp:** `EV-KI-R5-S07` / 2026-08-20T13:05:00+05:30.
- **Subwindow / assignment:** `KI-R5-S001` / `ASG-KI-R5-S001` (api.js).
- **Leaf stop state:** `AWAITING_WINDOW_REVIEW` (relay: "S001 awaiting
  review").
- **Change representation:** requester-authored commit `94aeaf95` ("S001",
  author Harit) on parent `fac5bb0f0a4e9c04873c9d338794762d44e35f7f`
  (baseline HEAD) — the requester exercised the requester-only committer
  privilege ("i committed anyways"); the leaf itself made no commit. Commit
  touches exactly `src/keyword-intelligence/api.js` (24 insertions, 31
  deletions); both nested working trees clean after it.
- **Independent window-agent verification (read-only):**
  - P1 ✓ — pre-edit blob digest `git show 94aeaf9^:src/…/api.js` =
    `8c6e9845c0847e49f5eaa30f815e2fd4287db899a62c8aeb815adcdd730971fb`
    (spec `starting_file_digest` match); ending digest
    `60751cca94a0c80010eb182907789f98f72d377d60fa24f613076b4b6cc05a10`.
  - T1 ✓ — all four ordered transformations and no other edit:
    (1) `saveSelectionInputSchema` items element is the strict
    discriminated union (`calculated` with `/^ksi_[a-f0-9]{12}$/u`
    sourceKeywordId; `manual`) and `expectedRevision` is
    `z.number().int().min(1)` (no `.nonnegative()` remains anywhere);
    (2) `canonicalizeSelectionItem` is the DEC-KI-034 materializer —
    calculated: row lookup with 400 on absence, `itemId=row.itemId`,
    row-retained `originalKeyword`/`sourceSeeds`/`metricsSnapshot`,
    classification with `row.mainIntent`; manual: `selectionItemId("manual",
    keyword)`, 400 on absent/empty first seed, `sourceSeeds=[firstSeed]`,
    null id/metrics, classification with `mainIntent: null`; every old
    client-supplied-field comparison (`item.itemId`, `item.originalKeyword`,
    `item.sourceSeeds`, `item.metricsSnapshot`, `item.lane`, `item.facets`,
    `item.sourceKeywordId` on input) deleted;
    (3) `validateSelectionDraft(draft)` inserted exactly once, textually
    before `analyzeSelectionConflicts(` (lines 449/451), import extended on
    the existing `./selection.js` line; `parseStrict` and the
    `MAX_SELECTION_ITEMS` (200) guard retained (line 438);
    (4) `createResearch`/`getResearch`/`createRun`/`exportCsv`, error codes,
    serializer output, and the one-read+one-CAS repository sequence are
    outside the diff (untouched).
  - V1 ✓ — `node --check src/keyword-intelligence/api.js` exit 0;
    `discriminatedUnion("sourceKind"` present exactly once; anchor (c) holds
    (zero `item.itemId` matches; `metricsSnapshot` matches are the retained
    row materialization, not input comparisons).
  - V2 ✓ — attributable change set is exactly the writable file (commit
    stat: 1 file; nested trees clean; root path set unchanged at 45 entries,
    digest `c660d09a800e8a5fd446bd65039f55241d5d7bb4e4c7ef656fe4fc7dcc88417c`).
  - V3 ✓ — S001 registers no leaf-time coverage IDs (behavioral proof
    deferred by spec to S005); registered = executed = ∅.
  - H2 ✓ — no second-file edit, successor work, external mutation, or parent
    communication; $0.00.
- **Residual integration obligations (per spec):** `R5-SEL-01`–`08`
  behavioral proof in S005; V1; V5. Note (non-blocking): `sameStringArray`/
  `deepEqual` helpers are now unused inside api.js — spec ordered no other
  edit, so their retention is correct; V1/V5 own any later disposition.
- **Review disposition:** **ACCEPTED.** `S2` advanced to state 5: S001 in
  `accepted_subwindows`; `KI-R5-S002` / `ASG-KI-R5-S002` staged with the
  dispatch-time change-set digest `c660d09a…` (post-S001 root path set;
  backend clean at `94aeaf9`). Next dispatch: `ASG-KI-R5-S002` (server.js).

---

## EV-KI-R5-S08 — S002 leaf executed; window-agent review: ACCEPTED

- **Evidence ID / timestamp:** `EV-KI-R5-S08` / 2026-08-20T13:25:00+05:30.
- **Subwindow / assignment:** `KI-R5-S002` / `ASG-KI-R5-S002` (server.js).
- **Leaf stop state:** `AWAITING_WINDOW_REVIEW` (relay: "S002 awaiting
  review").
- **Change representation:** requester-authored commit `125730b3` ("S002")
  on parent `94aeaf95` (S001) — requester-only committer privilege; commit
  touches exactly `src/server.js` (1 insertion, 1 deletion); working tree
  clean after it.
- **Independent window-agent verification (read-only):**
  - P1 ✓ — pre-edit blob digest `git show 125730b^:src/server.js` =
    `f9947000fe3edcd2d582979ad155fb732e0abd40726baa241e75d9ca9eb2e428`
    (spec `starting_file_digest` match); ending digest
    `2611f04068a26e04c5c1ec9a12ccf3fb8d54ca3bf55766d400a8a923fcaaa07a`.
  - T1 ✓ — exactly the single-argument edit: inside the
    `requestedKeywordResearchId(requestUrl.pathname, "selection")` +
    `request.method === "PUT"` block, `const payload = await
    readJsonBody(request);` → `readJsonBody(request, 262144)` (line 1785);
    diff is 1+/1− with no other change.
  - V1 ✓ — `node --check src/server.js` exit 0; anchor inspection: literal
    `262144` appears at exactly the selection route; all other
    `readJsonBody` call sites keep the default (lines 1686, 1732, 1756,
    1797, 1887); the `128 * 1024` site (line 1823) is pre-existing and
    untouched (outside the 1+/1− diff).
  - V2 ✓ — attributable change set is exactly the writable file (commit
    stat: 1 file; nested trees clean; root path set unchanged at 45 entries,
    digest `c660d09a…`).
  - V3 ✓ — no leaf-time coverage IDs (`R5-SEL-06`/`R5-SEL-08` deferred by
    spec to S005); registered = executed = ∅.
  - H2 ✓ — no second-file edit, other route/branch change, successor work,
    external mutation, or parent communication; $0.00.
- **Residual integration obligations (per spec):** `R5-SEL-06`/`R5-SEL-08`
  behavioral proof in S005; V1; V5.
- **Review disposition:** **ACCEPTED.** `S2` advanced to state 6: S002 in
  `accepted_subwindows`; `KI-R5-S003` / `ASG-KI-R5-S003` staged (export.js;
  live starting digest verified `03284102ee94ae11…` = spec value; backend
  clean at `125730b`). Next dispatch: `ASG-KI-R5-S003` (export.js).

---

## EV-KI-R5-S09 — S003 leaf executed; window-agent review: ACCEPTED

- **Evidence ID / timestamp:** `EV-KI-R5-S09` / 2026-08-20T13:45:00+05:30.
- **Subwindow / assignment:** `KI-R5-S003` / `ASG-KI-R5-S003` (export.js).
- **Leaf stop state:** `AWAITING_WINDOW_REVIEW` (relay: "S003 is awaiting
  review").
- **Change representation:** requester-authored commit `a8b86017` ("S003")
  on parent `125730b3` (S002) — requester-only committer privilege; commit
  touches exactly `src/keyword-intelligence/export.js` (18 insertions,
  9 deletions); working tree clean after it.
- **Independent window-agent verification (read-only):**
  - P1 ✓ — pre-edit blob digest `git show a8b8601^:…/export.js` =
    `03284102ee94ae11073e81d4dd331faa64dd4ee99ed1adadee1cd34366300d19`
    (spec `starting_file_digest` match); ending digest
    `4313dd63d23f21a8be595338e2e55492c2218d929a639f17bb48e755519e3adf`.
  - T1 ✓ — both ordered transformations and no other edit:
    (1) `neutralizeTextCell` is module-local and byte-identical to the
    DEC-KI-036 spec (single apostrophe, `startsWith("'")` idempotence guard,
    tab/CR-leading or `^\s*[=+\-@]`-leading strings only, applied once
    before existing quote/escape);
    (2) in `serializeKeywordsCsv` exactly the spec-enumerated textual cells
    are wrapped — `d.keyword`, `d.seed`, `d.source_seeds.join("|")`,
    `d.competition_level || ""`, `d.main_intent || ""`, `d.cluster || ""`,
    `d.cluster_id || ""`, `d.lane`, `pyDumps(d.facets, true)`,
    `d.variant_group_id || ""`, `d.variant_canonical || ""`,
    `(d.flags || []).join(";")`, `d.merged_into || ""`,
    `pyDumps(d.monthly_history, true)`, `d.available_markets.join("|")`;
    all numeric cells (`intStr`/`pyFloatStr`/`pyBoolStr` outputs including
    nullable `trend_slope`) remain unwrapped; header row, column order, and
    `csvEscape` are outside the diff (unchanged).
  - V1 ✓ — `node --check src/keyword-intelligence/export.js` exit 0;
    `node --test --test-isolation=none test/keyword-intelligence-parity.test.js`
    **11/11 PASS, 0 fail, 0 skip** (safe values byte-identical; no fixture
    edit); anchor inspection: `neutralizeTextCell` defined exactly once and
    applied to the named cells only.
  - V2 ✓ — attributable change set is exactly the writable file (commit
    stat: 1 file; nested trees clean; root path set unchanged at 45 entries,
    digest `c660d09a…`).
  - V3 ✓ — no leaf-time coverage IDs (`R5-EXP-05`/`R5-EXP-06` deferred by
    spec to S005); registered = executed = ∅.
  - H2 ✓ — no second-file edit, column/header/formatting change, successor
    work, external mutation, or parent communication; $0.00.
- **Residual integration obligations (per spec):** `R5-EXP-05`/`R5-EXP-06`
  behavioral proof in S005; V1; V5.
- **Review disposition:** **ACCEPTED.** `S2` advanced to state 7: S003 in
  `accepted_subwindows`; `KI-R5-S004` / `ASG-KI-R5-S004` staged
  (repository.js read-only P2002 reconciliation; live starting digest
  verified `fa249de2…` = spec; DB runs prohibited before V3). Next dispatch:
  `ASG-KI-R5-S004` (repository.js).

---

## EV-KI-R5-S10 — S004 leaf executed; window-agent review: ACCEPTED

- **Evidence ID / timestamp:** `EV-KI-R5-S10` / 2026-08-20T14:05:00+05:30.
- **Subwindow / assignment:** `KI-R5-S004` / `ASG-KI-R5-S004`
  (repository.js).
- **Leaf stop state:** `AWAITING_WINDOW_REVIEW` (relay: "S004 is awaiting
  review").
- **Change representation:** requester-authored commit `b06360c5` ("S004")
  on parent `a8b86017` (S003) — requester-only committer privilege; commit
  touches exactly `src/keyword-intelligence/repository.js` (15 insertions,
  0 deletions — insert-only into the `createRun` catch); working tree clean
  after it.
- **Independent window-agent verification (read-only):**
  - P1 ✓ — pre-edit blob digest `git show b06360c^:…/repository.js` =
    `fa249de27bc6d47c2480c342c5bf5760868328445e83dca9bb31be97fa2387c7`
    (spec `starting_file_digest` match); ending digest
    `be134a3fe039008a9509e940184337e14b276d6bd0e68b6c0830b03e2a68bf48`.
  - T1 ✓ — exactly the ordered transformation and no other edit: the P2002
    branch is inserted in the catch after the `RunHandoffAbort` mapping and
    before `throw error`; the reconciliation is a new `this._transaction`
    performing exactly `findUnique`×2
    (`keywordResearchHandoff.findUnique` by `researchId_clientRequestId`
    with `researchId` and `input.clientRequestId`, then
    `run.findUnique({ where: { id: handoff.runId } })`) and zero
    creates/updates; `throw originalError` when the handoff row is absent;
    durable-only comparison (`selectionFingerprint` vs
    `input.selectionFingerprint`, `selectionRevision` vs
    `input.expectedSelectionRevision`); outcomes limited to the existing
    union (`"conflict"`/`KEYWORD_RUN_HANDOFF_CONFLICT` or `"found"` with
    the run); the first transaction, its `RunHandoffAbort` mapping, and the
    winning write path (lines 1236/1263) are outside the diff (untouched);
    public signature and outcome unions unchanged; no retry loop/sleep or
    distributed lock introduced.
  - V1 ✓ — `node --check src/keyword-intelligence/repository.js` exit 0;
    anchor inspection: exactly one `P2002` branch in the file (line 1275);
    the `keywordResearchHandoff.create` at line 1263 is the pre-existing
    winner path, not part of the reconciliation.
  - V2 ✓ — attributable change set is exactly the writable file (commit
    stat: 1 file; nested trees clean; root path set unchanged at 45 entries,
    digest `c660d09a…`).
  - V3 ✓ — no leaf-time coverage IDs (`R5-FIN-07`/`R5-FIN-08` + `NC-07`
    deferred by spec to V3; `W4-D04` supersession to S006); registered =
    executed = ∅.
  - H2 ✓ — no second-file edit, schema/migration edit, DB run, successor
    work, external mutation, or parent communication; $0.00.
- **Residual integration obligations (per spec):** `R5-FIN-07`/`R5-FIN-08`
  + `NC-07` behavioral proof at V3 (single isolated-DB run);
  `W4-D04` supersession in S006; V5. DB runs remain prohibited before V3.
- **Review disposition:** **ACCEPTED.** `S2` advanced to state 8: S004 in
  `accepted_subwindows`; `KI-R5-S005` / `ASG-KI-R5-S005` staged
  (test/keyword-intelligence-api.test.js — BAPI registry, NC-03/04/10,
  supersession of exactly {W4-A04, A06, A07, S04, S06}, single focused
  file run with certificate; live starting digest verified
  `09e92358…` = spec; backend clean at `b06360c`). Next dispatch:
  `ASG-KI-R5-S005` (api.test.js).

---

## EV-KI-R5-S11 — S005 leaf executed; window-agent review: ACCEPTED

- **Evidence ID / timestamp:** `EV-KI-R5-S11` / 2026-08-20T14:40:00+05:30.
- **Subwindow / assignment:** `KI-R5-S005` / `ASG-KI-R5-S005`
  (api.test.js).
- **Leaf stop state:** `AWAITING_WINDOW_REVIEW` (relay: "S005 is awaiting
  review").
- **Change representation:** requester-authored commit `13effc7` ("S005")
  on parent `b06360c5` (S004) — requester-only committer privilege; commit
  touches exactly `test/keyword-intelligence-api.test.js` (184 insertions,
  11 deletions); working tree clean after it.
- **Independent window-agent verification (read-only):**
  - P1 ✓ — pre-edit blob digest `git show 13effc7^:…/api.test.js` =
    `09e9235810a767bb4173a41a139b66f5cfe81c7a70ebddaf21773a78abc2aea0`
    (spec `starting_file_digest` match); ending digest
    `64e30a7034b4191bd7c952450940aca56b6b8bdcee4105afebacbfa85da30063`.
  - T1 ✓ — all four ordered transformations: (1) literal `R5_API_CASES`
    registry with exactly the ten spec IDs (line 37) and executable
    case-map implementations of the A4 rows (SEL-01..08, EXP-05/06, each
    pushing its ID after activation witness + oracle); (2) negative
    controls implemented with the A4 control-table labels
    (`R5_SELECTION_WIRE_OR_LIMIT_DIVERGED`,
    `R5_DUPLICATE_WRITE_FORBIDDEN`, `R5_CSV_TEXT_UNSAFE`) in the
    pass–mutate–fail–restore pattern (assertion/expected-message dual
    checks, lines 2125–2134); (3) supersession of exactly
    {W4-A04, W4-A06, W4-A07, W4-S04, W4-S06} — the W4 ID set in the file is
    unchanged (`diff` of sorted old/new W4 IDs: empty), so no unlisted W4
    case was removed; the five oracles are modified in place with R5
    citations; the pre-existing `KI_W4_EXECUTION_CERTIFICATE` emission
    (line 1975) is structurally unchanged; (4) exactly one
    `KI_R5_EXECUTION_CERTIFICATE=` line for registry `"api"` with sorted
    arrays and per-member-LF digests (line 2145).
  - V1 ✓ — window-agent rerun of
    `node --test --test-isolation=none test/keyword-intelligence-api.test.js`:
    **46/46 pass, 0 fail, 0 skipped, 0 todo**; certificate captured
    verbatim for E1: registry `"api"`, required=registered=executed =
    [R5-EXP-05, R5-EXP-06, R5-SEL-01..08], skipped `[]`, digests all
    `3db029274e44b2a25ce1e551a10ef9c689ef71e6b4dedcac4e258175fc092a84`.
  - V2 ✓ — attributable change set is exactly the writable file (commit
    stat: 1 file; nested trees clean; root path set unchanged at 45 entries,
    digest `c660d09a…`).
  - V3 ✓ — registered = executed = 10/10 case IDs, zero skips (certificate
    arrays + run output agree).
  - H2 ✓ — no production-file edit, DB run, provider/AWS call, successor
    work, or parent communication; $0.00.
- **Residual integration obligations (per spec):** V1 frozen rerun; V5.
- **Review disposition:** **ACCEPTED.** `S2` advanced to state 9: S005 in
  `accepted_subwindows`; `KI-R5-S006` / `ASG-KI-R5-S006` staged
  (handoff.integration.test.js — DB registry {R5-FIN-07, R5-FIN-08},
  NC-07, W4-D04 supersession; node --check + no-database registration run
  only — DB execution deferred to V3; live starting digest verified
  `2a17aa56…` = spec; backend clean at `13effc7`). Next dispatch:
  `ASG-KI-R5-S006`.

---

## EV-KI-R5-S12 — S006 leaf executed; window-agent review: ACCEPTED

- **Evidence ID / timestamp:** `EV-KI-R5-S12` / 2026-08-20T15:05:00+05:30.
- **Subwindow / assignment:** `KI-R5-S006` / `ASG-KI-R5-S006`
  (handoff.integration.test.js).
- **Leaf stop state:** `AWAITING_WINDOW_REVIEW` (relay: "S006 is awaiting
  review").
- **Change representation:** requester-authored commit `7c6134c` ("S006")
  on parent `13effc7` (S005) — requester-only committer privilege; commit
  touches exactly `test/keyword-intelligence-handoff.integration.test.js`
  (150 insertions, 1 deletion); working tree clean after it.
- **Independent window-agent verification (read-only):**
  - P1 ✓ — pre-edit blob digest `git show 7c6134c^:…/handoff…test.js` =
    `2a17aa562893c294a5f027ce074df17695cc4e6c156addcdc1af3522b6ada75c`
    (spec `starting_file_digest` match); ending digest
    `5ab13d446229fc4c6840a0c321feb3e09371c4d09ffb9fe988be59fcd8108813`.
  - T1 ✓ — all four ordered transformations:
    (1) literal `R5_DB_CASES = ["R5-FIN-07", "R5-FIN-08"]` (line 25) with
    the two cases as named subtests inside the existing single-harness
    disposable-schema lifecycle;
    (2) `W4-D04` superseded in place — the **only** deleted line in the
    entire diff is the old `assert.ok(fulfilled.length >= 1, …)`; the new
    oracle asserts exactly two fulfilled with sorted deep-equal
    `["created","found"]`, exactly one Run, one RunQuery set, one handoff
    row, citing `R5-FIN-07`; the W4-D ID set in the file is unchanged, so
    D01–D03/D05/D06 are byte-identical;
    (3) `NC-07` via `clientWithMissingReconciliation` non-mutating proxy for
    the losing call — the unchanged two-fulfilled oracle throws
    `R5_EQUAL_RACE_NOT_RECONCILED` when the proxy hides reconciliation, and
    the unwrapped client passes in the fresh fixture above (finally-block
    disconnect restore; zero production-source edits);
    (4) exactly one registry `"database"` `KI_R5_EXECUTION_CERTIFICATE=`
    line (line 810) with sorted arrays and per-member-LF digests.
  - V1 ✓ — `node --check` exit 0; window-agent no-database registration
    run: **2 pass / 1 designed skip / 0 fail**, exactly one certificate
    line, captured verbatim: registry `"database"`,
    required=[R5-FIN-07, R5-FIN-08], registered=[]/executed=[]/
    skipped=[both] — the designed deferral shape (DB execution belongs to
    V3 only); required digest `0cc6cab7b86d187e8db4edcd44d68a6752a2375e6bdc7eaeba7d051e470a09b5`.
  - V2 ✓ — attributable change set is exactly the writable file (commit
    stat: 1 file; nested trees clean; root path set unchanged at 45 entries,
    digest `c660d09a…`).
  - V3 ✓ — registered leaf-time coverage = ∅ by spec (execution deferred to
    V3); the registration run proves structure with zero failures.
  - H2 ✓ — no database execution (`ALLOW_DATABASE_TESTS` not set; run
    skipped as designed), no production edit, provider/AWS call, successor
    work, or parent communication; $0.00.
- **Residual integration obligations (per spec):** V3 single frozen
  isolated-DB run (`R5-FIN-07`/`R5-FIN-08` + executed-certificate capture);
  V5.
- **Review disposition:** **ACCEPTED.** `S2` advanced to state 10: S006 in
  `accepted_subwindows` — backend file set (S001–S006) complete;
  `KI-R5-S007` / `ASG-KI-R5-S007` staged — **first frontend leaf**
  (`frontend/lib/keyword-intelligence-types.ts` type-only edits;
  `contractVersion: 1` ×2 + three mutation type exports; strip-types
  import smoke; live starting digest verified `1619572d…` = spec; frontend
  clean at `c85f93b`). Next dispatch:   `ASG-KI-R5-S007`.

---

## EV-KI-R5-S13 — S007 leaf executed; window-agent review: ACCEPTED

- **Evidence ID / timestamp:** `EV-KI-R5-S13` / 2026-08-20T15:30:00+05:30.
- **Subwindow / assignment:** `KI-R5-S007` / `ASG-KI-R5-S007`
  (frontend/lib/keyword-intelligence-types.ts).
- **Leaf stop state:** `AWAITING_WINDOW_REVIEW` (relay: "S007 awaiting
  review").
- **Change representation:** requester-authored commit `077af2d` ("KI-R5
  S007") on parent `c85f93b` (frontend baseline) — requester-only committer
  privilege; commit touches exactly `lib/keyword-intelligence-types.ts`
  (6 insertions, 2 deletions); frontend tree clean after it.
- **Independent window-agent verification (read-only):**
  - P1 ✓ — pre-edit blob digest `git show 077af2d^:…types.ts` =
    `1619572d606af3b43a7bbf9945ef3f208e01f99c01ced29e2666a84c244b1f19`
    (spec `starting_file_digest` match); ending digest
    `fafd471b9df9bf4fb25706adda0e091bb2188d9baf2bd195bb7ead9e9b093d39`.
  - T1 ✓ — exactly the three ordered type-only transformations: the file's
    only two `contractVersion: string;` occurrences (pre-edit grep count 2)
    are converted to `contractVersion: 1;` at `ResearchResult` (line 176)
    and `ResearchView` (line 215); the three appended exports
    `CalculatedSelectionMutation` / `ManualSelectionMutation` /
    `SelectionMutationItem` are byte-identical to the spec (lines 272–274);
    the diff contains nothing else.
  - V1 ✓ — anchor inspection: exactly two `contractVersion: 1;` literals;
    three type exports present; zero `export const`/`export function`
    (runtime export surface unchanged — W5-I01 remains byte-read-only);
    strip-types load smoke
    `node --experimental-strip-types --input-type=module -e "await
    import('./lib/keyword-intelligence-types.ts')"` from `frontend/` —
    exit 0.
  - V2 ✓ — attributable change set is exactly the writable file (commit
    stat: 1 file; frontend and backend trees clean; root path set unchanged
    at 45 entries, digest `c660d09a…`).
  - V3 ✓ — no leaf-time coverage IDs (`R5-WIRE-01`–`03` deferred by spec to
    S013); registered = executed = ∅.
  - H2 ✓ — no runtime export change, second-file edit, successor work,
    external mutation, or parent communication; $0.00.
- **Residual integration obligations (per spec):** S008/S009 consumers;
  V2/V4.
- **Review disposition:** **ACCEPTED.** `S2` advanced to state 11: S007 in
  `accepted_subwindows`; `KI-R5-S008` / `ASG-KI-R5-S008` staged
  (validation.ts `=== 1` guards at `result()`/`parseResearchView()`;
  live starting digest verified `8275def2a60c2cac443f1ca6e0a6f2d64cf31df9d467513be6cf0eaba34a6464`
  = spec; frontend clean at `077af2d`). Next dispatch:   `ASG-KI-R5-S008`.

---

## EV-KI-R5-S14 — S008 leaf executed; window-agent review: ACCEPTED

- **Evidence ID / timestamp:** `EV-KI-R5-S14` / 2026-08-20T15:50:00+05:30.
- **Subwindow / assignment:** `KI-R5-S008` / `ASG-KI-R5-S008`
  (frontend/lib/keyword-intelligence-validation.ts).
- **Leaf stop state:** `AWAITING_WINDOW_REVIEW` (relay: "S008 awaiting
  review").
- **Change representation:** requester-authored commit `289de4c` ("S008")
  on parent `077af2d` (S007) — requester-only committer privilege; commit
  touches exactly `lib/keyword-intelligence-validation.ts` (2 insertions,
  2 deletions); frontend tree clean after it.
- **Independent window-agent verification (read-only):**
  - P1 ✓ — pre-edit blob digest `git show 289de4c^:…validation.ts` =
    `8275def2a60c2cac443f1ca6e0a6f2d64cf31df9d467513be6cf0eaba34a6464`
    (spec `starting_file_digest` match); ending digest
    `81f7c0648fe9f91e77a0b8cd814747fc23bae1b489fee9c51c05adf22e761689`.
  - T1 ✓ — exactly the two ordered edits and nothing else: in `result()`
    (the wire `research` result parser) and in `parseResearchView()`, the
    `contractVersion: nonEmptyText(source.contractVersion, …)` forms are
    replaced with the byte-identical spec guard
    `source.contractVersion === 1 ? 1 : (() => { throw new
    ApiPayloadError(…); })()` — an exact `=== 1` guard rejecting any string,
    other number, null, undefined, or non-integer; no dual-version parser
    introduced.
  - V1 ✓ — anchor inspection: exactly two `contractVersion === 1` guards;
    zero remaining `nonEmptyText(source.contractVersion` occurrences;
    `nonEmptyText` remains used by unrelated fields; strip-types load smoke
    exit 0; export surface diff old→new is empty (8 exports unchanged —
    W5-I02 oracle remains byte-read-only).
  - V2 ✓ — attributable change set is exactly the writable file (commit
    stat: 1 file; both nested trees clean; root path set unchanged at 45
    entries, digest `c660d09a…`).
  - V3 ✓ — no leaf-time coverage IDs (`R5-WIRE-01`–`03` deferred by spec to
    S013); registered = executed = ∅.
  - H2 ✓ — no shared-parser change beyond the two sites, second-file edit,
    successor work, external mutation, or parent communication; $0.00.
- **Residual integration obligations (per spec):** `R5-WIRE-01`–`03` proof
  in S013; V2/V4.
- **Review disposition:** **ACCEPTED.** `S2` advanced to state 12: S008 in
  `accepted_subwindows`; `KI-R5-S009` / `ASG-KI-R5-S009` staged
  (client-api.ts — three JSON headers + module-local guarded
  `toSelectionMutation`; live starting digest verified
  `b57d7b8609387243b8413a084303acf89c2fc4943ec170077321a01a3608c936` =
  spec; frontend clean at `289de4c`). Next dispatch:   `ASG-KI-R5-S009`.

---

## EV-KI-R5-S15 — S009 leaf executed; window-agent review: ACCEPTED

- **Evidence ID / timestamp:** `EV-KI-R5-S15` / 2026-08-20T16:15:00+05:30.
- **Subwindow / assignment:** `KI-R5-S009` / `ASG-KI-R5-S009`
  (frontend/lib/client-api.ts).
- **Leaf stop state:** `AWAITING_WINDOW_REVIEW` (relay: "S009 awaiting
  review").
- **Change representation:** requester-authored commit `c6642ae` ("S009")
  on parent `289de4c` (S008) — requester-only committer privilege; commit
  touches exactly `lib/client-api.ts` (19 insertions, 3 deletions); frontend
  tree clean after it.
- **Independent window-agent verification (read-only):**
  - P1 ✓ — pre-edit blob digest `git show c6642ae^:…client-api.ts` =
    `b57d7b8609387243b8413a084303acf89c2fc4943ec170077321a01a3608c936`
    (spec `starting_file_digest` match); ending digest
    `288654c7881fc3df6f02b0b62d3641b8d153becb29af3fe6e3ca3db704519bd6`.
  - T1 ✓ — all four ordered transformations: (1)–(3) exactly three
    `headers: { "Content-Type": "application/json" }` additions
    (`createKeywordResearch`, `saveKeywordSelection`,
    `startKeywordResearchRun`; pre-edit count 0 → 3); (2) module-local
    `toSelectionMutation` (line 56, not exported; zero occurrences pre-edit)
    is byte-identical in behavior to the frozen §3.1 guard — calculated
    requires a non-empty string `sourceKeywordId`, else throws
    `new Error("calculated selection item requires a source id")` before
    constructing the member; manual returns `{ sourceKind: "manual",
    keyword }`; PUT body is exactly
    `JSON.stringify({ expectedRevision, items: toSelectionMutation(items) })`
    — no snapshot/derived field, no client identity authority; public
    signature unchanged (`items: SelectionItem[]`); (4) `apiRequest`, every
    GET, and `startKeywordResearchRun`'s body
    (`{ expectedSelectionRevision, clientRequestId }` exactly) unchanged.
  - V1 ✓ (with one environmental finding) — anchors hold; the literal
    strip-types import smoke fails with
    `ERR_MODULE_NOT_FOUND: Cannot find package '@/lib'` — the window agent
    reproduced the **identical failure on the pre-edit blob**, so it is a
    pre-existing module-resolution limitation of the `@/lib` path alias
    outside Next's bundler, not a leaf defect; compensating parse proof
    `node --experimental-strip-types --check lib/client-api.ts` exit 0.
    Real load behavior remains owned by V2/V4 under Next resolution.
  - V2 ✓ — attributable change set is exactly the writable file (commit
    stat: 1 file; both nested trees clean; root path set unchanged at 45
    entries, digest `c660d09a…`).
  - V3 ✓ — no leaf-time coverage IDs (`R5-WIRE-05/06` deferred by spec to
    S013; `R5-WIRE-04` to S015/V4); registered = executed = ∅.
  - H2 ✓ — no `apiRequest` behavior change, legacy-caller change,
    second-file edit, successor work, external mutation, or parent
    communication; $0.00.
- **Residual integration obligations (per spec):** `R5-WIRE-05/06` init
  capture in S013; `R5-WIRE-04` route boundary in S015/V4; V2/V4.
- **Review disposition:** **ACCEPTED.** `S2` advanced to state 13: S009 in
  `accepted_subwindows`; `KI-R5-S010` / `ASG-KI-R5-S010` staged
  (view-model.ts — `selectionSaveProjection` + `"unsaved"` gate reason +
  haystack/flags predicate corrections; live starting digest verified
  `b91f0f5e7fd9f692e5f9086f1be0f511af1f0b6b755d117924497a52f89ce9d5` =
  spec; frontend clean at `c6642ae`). Next dispatch: `ASG-KI-R5-S010`.

---

## EV-KI-R5-S16 — S010 leaf executed; window-agent review: ACCEPTED

- Evidence ID / timestamp: EV-KI-R5-S16 / 2026-08-20T12:59:17+05:30.
- Subwindow / assignment: KI-R5-S010 / ASG-KI-R5-S010
  (frontend/lib/keyword-intelligence-view-model.ts).
- Leaf stop state: AWAITING_WINDOW_REVIEW (implementation was already present
  as requester-authored commit 664f515, S010).
- Frozen revisions verified: parent standard
  3b7a4fd25156e1adfbc92abb835c5f82a0d18c686b1c1150feb202f2d944d2ac;
  sub-window standard
  1766f9107ce7d315877b75d4b0ea2b5521dff1c321e12f890b03787d66196ded;
  contract 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c;
  decision e8ed580dd08b77540158340c47fae84c5d56b18cc7aba3149ccc2ab568493f5d;
  parent checklist 4f52bf764525927fd7b68c0795aec5cbbd15f1a8b9b73778d446cfd87e2b94b8;
  decomposition 6ff7830adc72874a3c30a2000ec96f32a668fba230fe652260d83ad2cab9500f.
- Independent window-agent verification (read-only):
  - P1 PASS — frontend HEAD = 664f51522d06b04aa0a01ddb4cc9c55c9a4e3a25,
    parent = accepted S009 c6642aeb6f35d5fe88ba31e0417bb5f7e3c7c2e5;
    the pre-edit blob digest matches the assigned starting digest
    b91f0f5e7fd9f692e5f9086f1be0f511af1f0b6b755d117924497a52f89ce9d5.
  - T1 PASS — the one-file diff contains exactly the prescribed ordered
    changes: module-local selectionSaveProjection with the frozen calculated
    source guard and exact error literal; the unsaved reason and projection
    comparison between over_limit and conflicts; removal of mainIntent and
    synthetic recommended from haystack; and filter.flags.every. Persisted
    ordering is untouched and no runtime export was added.
  - V1 PASS — strip-types syntax check and exact module import smoke exited 0.
    The deterministic literal spot-check exited 0, proving flags [a,b] retain
    only the row with both flags and a mainIntent-only search returns zero rows.
  - V2 PASS — commit stat reports exactly one changed file (25 insertions,
    4 deletions); frontend and backend nested trees are clean; the current
    owner-controlled root set has 45 entries and dispatch-time digest
    02530e7cc6bba4e59291f1eba4cf5464b784bbabac4dfb2384c33fae90f54a74.
  - V3 PASS — no S010 local coverage IDs are registered or executed; listed
    integration cases R5-EXP-01 through R5-EXP-04 and R5-FIN-02 through
    R5-FIN-04 remain deferred to S013/S014 as specified; skipped, duplicate,
    and unexpected cases are empty.
  - H2 PASS — no second-file edit, successor work, parent communication,
    provider/AWS/database operation, destructive action, or external cost
    occurred; cost $0.00.
- Ending file digest:
  5a193f82981d865b44e082a39a374cdf77d7ec3300bbfc3659246709a8ed3df5.
- Review disposition: ACCEPTED_FOR_INTEGRATION. S010 is closed and S011 /
  ASG-KI-R5-S011 is staged for
  frontend/components/keyword-intelligence/selection-review.tsx, with live
  starting digest
  5d127c195a2553cc077b4b1a3f592add08a184b9761cfce658fbb810b248f992.

---

## EV-KI-R5-S17 — S1 revision delta audit; S011 dispatch blocked

- Evidence ID / timestamp: EV-KI-R5-S17 / 2026-08-20T13:00:00+05:30.
- Parent window / assignment: KI-R5 / ASG-KI-R5-WA-01.
- Actor / role: KI-R5-WINDOW-AGENT / window agent.
- Trigger: before executing staged S011, the live S1 digest was independently
  recomputed as f38d0bfd40dea50a11fb7473c0013d224f5b3e519c54d964553fc227c79b7319,
  while S2 decomposition_revision and S3 inherited pin remain
  6ff7830adc72874a3c30a2000ec96f32a668fba230fe652260d83ad2cab9500f.
- Exact inspections performed (read-only):
  - sha256sum of KEYWORD_INTELLIGENCE_KI_R5_SUBWINDOW_CHECKLIST.md produced
    the live f38d0bfd… digest; S2 and S3 still pin 6ff7830a….
  - rg located no second on-disk copy of the R5 S1 checklist and no Git
    history entry for that path. Unreachable Git objects inspected were
    unrelated AWS documents, not an approved S1 copy.
  - Live S1 §0 retains the pinned parent/contract/decision/checklist revisions;
    §3 retains the sequential S010 → S011 dependency; §5 S010 retains the
    projection/saved-gate/filter instructions; §5 S011 retains the exact
    prop, inertness, retry-notice, draft-key, and stale-conflict instructions;
    §11.3 records the EV-KI-R5-S06 approval claim for S1 6ff7830a….
  - The semantic anchors therefore appear present, but those inspections do
    not prove byte-equivalence to the approved 6ff7830a… artifact.
- Decisive result: the standard revision-mismatch rule requires a delta audit
  and blocks new sub-window assignment until the approved revision content is
  verified or a parent-authorized correction/reapproval supplies a new pin.
  S011 was not executed, and no implementation file was modified.
- Changed path set: none in the implementation repositories; only this
  append-only evidence entry is a coordination write.
- Coverage: none registered, executed, skipped, duplicated, or unexpected;
  no local or whole-window gate was run.
- External mutations / costs: none / $0.00.
- Review disposition: PARENT_BLOCKED for S011 dispatch pending authoritative
  S1 revision reconciliation.

---

## EV-KI-R5-S18 — Parent-authorized S1 pin reconciliation; S011 resumed

- Evidence ID / timestamp: EV-KI-R5-S18 / 2026-08-20T13:10:00+05:30.
- Parent window / assignment: KI-R5 / ASG-KI-R5-WA-01.
- Actor / role: KI-R5-WINDOW-AGENT / window agent.
- Authority: A5 state 114 is IN_PROGRESS and explicitly authorizes this
  S2/S3-only reconciliation; EV-KI-A-053 records the mechanical delta proof;
  CHG-KI-028 records the reapproval, unchanged requirements/decisions, and
  no-rerun rule.
- Exact reconciliation performed:
  - live S1 remains
    f38d0bfd40dea50a11fb7473c0013d224f5b3e519c54d964553fc227c79b7319;
  - S2 decomposition_revision changed from 6ff7830a… to f38d0bfd…;
  - S2 state advanced 14 → 15, current_status changed BLOCKED → READY,
    blocker cleared, current leaf remains KI-R5-S011 / ASG-KI-R5-S011;
  - accepted_subwindows remains exactly S001 through S010;
  - S001–S010 were not rerun and S1 was not modified.
- S011 preflight: selection-review.tsx digest remains the assigned starting
  digest 5d127c195a2553cc077b4b1a3f592add08a184b9761cfce658fbb810b248f992;
  frontend and backend worktrees are clean.
- Coverage: no new cases registered or executed; no prior evidence invalidated;
  hash-only drift is explicitly non-normative under EV-KI-A-053.
- External mutations / costs: none / $0.00.
- Review disposition: **RESUMED_FOR_S011**. S011 is ready for dispatch under
  the unchanged S1 task block.

---

## EV-KI-R5-S19 — S011 leaf executed; window-agent review: ACCEPTED

- Evidence ID / timestamp: EV-KI-R5-S19 / 2026-08-20T13:20:00+05:30.
- Subwindow / assignment: KI-R5-S011 / ASG-KI-R5-S011
  (frontend/components/keyword-intelligence/selection-review.tsx).
- Leaf stop state: AWAITING_WINDOW_REVIEW; requester-authored commit fba0775
  on accepted S010 commit 664f515.
- Independent window-agent verification:
  - P1 PASS — pre-edit blob digest from git show fba0775^ matches the assigned
    5d127c195a2553cc077b4b1a3f592add08a184b9761cfce658fbb810b248f992;
    ending digest is
    763c7d4921257ab698b448ddff4846dbc1d9571a306409a233137cd89be11921.
  - T1 PASS — the one-file diff expands the exact finalizeState union and
    onRetryHandoff prop; removes MANUAL_ID_LANES, manualItemDigest, and
    stableManualItemId; creates monotonic collision-checked draft_ keys;
    disables manual add/edit/remove/save/finalize controls for handing-off,
    retry_required, and succeeded; adds the exact retry notice/button; and
    preserves definitive_failure idle-equivalent behavior plus staleConflict
    locking. No ksi_ literal or second-file edit exists.
  - V1 PASS — anchor inspection proves all required symbols, literals, three
    inert states, retry control, and unchanged staleConflict path. The generic
    Node strip-types loader is not applicable to TSX and returns
    ERR_UNKNOWN_FILE_EXTENSION before loading; this was not a required S011
    check, and no product failure is inferred from it.
  - V2 PASS — commit stat and diff contain exactly the authorized file; root
    changed-file set remains 45 entries with digest
    02530e7cc6bba4e59291f1eba4cf5464b784bbabac4dfb2384c33fae90f54a74;
    backend and frontend worktrees are clean.
  - V3 PASS — S011 local coverage registration/execution is empty as required;
    R5-SEL-02 and R5-WIRE-05 remain deferred to the prescribed integration
    owners; skipped, duplicate, and unexpected local cases are empty.
  - H2 PASS — no successor work, parent communication, external mutation,
    provider/AWS/database operation, destructive action, commit by the
    window agent, or cost occurred.
- Review disposition: ACCEPTED_FOR_INTEGRATION. S011 is closed and S012 /
  ASG-KI-R5-S012 is staged for
  frontend/components/keyword-intelligence/research-dashboard.tsx, with live
  starting digest
  94ba68eec79302352bdd6ac387bd8f27586ba0bb078d80b7b1390c56518ef023.

---

## EV-KI-R5-S20 — S012 leaf executed; window-agent review: ACCEPTED

- Evidence ID / timestamp: EV-KI-R5-S20 / 2026-08-20T13:30:00+05:30.
- Subwindow / assignment: KI-R5-S012 / ASG-KI-R5-S012
  (frontend/components/keyword-intelligence/research-dashboard.tsx).
- Leaf stop state: AWAITING_WINDOW_REVIEW; requester-authored commit 5e2083c
  on accepted S011 commit fba0775.
- Independent window-agent verification:
  - P1 PASS — pre-edit blob digest matches the assigned
    94ba68eec79302352bdd6ac387bd8f27586ba0bb078d80b7b1390c56518ef023;
    ending digest is
    19494a99a2be28683167908289176bf44ebb8d0bb1eb40f63cc6d1cd770c6337.
  - T1 PASS — the one-file diff adds the exact five-state finalize union,
    preserves canonical save response replacement and revision-driven draft
    reset, allocates the request ID only when entering from idle, sets
    succeeded before navigation, classifies <500 responses as definitive,
    retains ID/revision for ambiguous outcomes, and adds same-ID/revision
    retry handling. The S011 onRetryHandoff prop is wired.
  - V1 PASS — anchor inspection proves retry_required, definitive_failure,
    succeeded, retained clientRequestIdRef usage, no ambiguous-path nulling,
    canonical save response update, and router navigation. The generic Node
    strip-types loader is not applicable to TSX and returns
    ERR_UNKNOWN_FILE_EXTENSION before loading; S012 requires anchor
    inspection, not a TSX loader smoke.
  - V2 PASS — commit stat and diff contain exactly the authorized file; root
    changed-file set remains 45 entries with digest
    02530e7cc6bba4e59291f1eba4cf5464b784bbabac4dfb2384c33fae90f54a74;
    backend and frontend worktrees are clean.
  - V3 PASS — no S012 local coverage IDs are registered or executed;
    R5-FIN-01 through R5-FIN-06 and R5-WIRE-06 remain deferred to S014/V4;
    skipped, duplicate, and unexpected local cases are empty.
  - H2 PASS — no successor work, parent communication, external mutation,
    provider/AWS/database operation, destructive action, or window-agent
    implementation edit occurred; cost $0.00.
- Review disposition: ACCEPTED_FOR_INTEGRATION. S012 is closed and S013 /
  ASG-KI-R5-S013 is staged for frontend/test/keyword-intelligence-api.test.ts,
  with live starting digest
  a2f40c62bdf6d34136c2d6a318c8aef24e426581182a2d5edf0ef6fc950cd5c5.

---

## EV-KI-R5-S21 — S013 leaf blocked by accepted S010 defect

- Evidence ID / timestamp: EV-KI-R5-S21 / 2026-08-20T13:40:00+05:30.
- Subwindow / assignment: KI-R5-S013 / ASG-KI-R5-S013
  (frontend/test/keyword-intelligence-api.test.ts).
- Leaf stop state: AWAITING_WINDOW_REVIEW; no file changed. Preflight digest
  remains a2f40c62bdf6d34136c2d6a318c8aef24e426581182a2d5edf0ef6fc950cd5c5;
  frontend HEAD is 5e2083c and backend HEAD is 7c6134c; both worktrees are
  clean.
- Independent diagnosis: accepted S010 ending digest
  5a193f82981d865b44e082a39a374cdf77d7ec3300bbfc3659246709a8ed3df5 has
  canFinalizeSelection calling selectionSaveProjection(view.selection.items)
  at view-model.ts:663. The frozen ResearchView type declares selection as
  SelectionItem[] at keyword-intelligence-types.ts:220, so the call reaches
  selectionSaveProjection(undefined) and throws while evaluating items.map.
  The same production function is called by the dashboard and selection
  review, so this is not test-only.
- Exact reproduction: node --experimental-strip-types --test
  test/keyword-intelligence-api.test.ts exits 1 on the current tree. The
  reported W5-A05/W5-A06 string-version failures are expected S013
  supersession inputs; W5-A10 independently activates the TypeError path.
- Frozen remedy: change only view-model.ts:663 from
  selectionSaveProjection(view.selection.items) to
  selectionSaveProjection(view.selection). This is the existing S010 file,
  inside the fixed 18-path set, and is required before a faithful S013
  W5-A09/W5-A10 supersession can execute.
- Authority result: a one-file corrective sub-window KI-R5-C001 is required,
  but authoring it requires an append to S1 §11.1. A5 state 114 expressly
  prohibits further S1 mutation without parent reapproval. No C001 was
  authored or assigned, and no implementation file was modified.
- Coverage: S013 required cases were not registered or executed; no case was
  skipped, duplicated, or made unexpected by the leaf. No prior accepted
  evidence is silently invalidated.
- External mutations / costs: none / $0.00.
- Review disposition: **PARENT_BLOCKED** pending parent reapproval for the S1
  corrective-subwindow amendment and C001 assignment.

---

## EV-KI-R5-S22 — C001 corrective sub-window authored and staged

- Evidence ID / timestamp: EV-KI-R5-S22 / 2026-08-20T13:45:00+05:30.
- Parent window / assignment: KI-R5 / ASG-KI-R5-WA-01.
- Actor / role: KI-R5-WINDOW-AGENT / window agent.
- Authority: A5 state 115, EV-KI-A-054, and CHG-KI-029 authorize exactly one
  append-only C001 block to S1 §11.1 and one corrective leaf owning only
  frontend/lib/keyword-intelligence-view-model.ts.
- S1 amendment: appended complete KI-R5-C001 Section-7 correction block and
  CORRECTIVE-SUBWINDOW-READY certificate. New S1 digest is
  0f3ef85771392d164ad1e44f044c1b71659b84d44176b47aed58c4afaca35657.
- Corrective assignment: ASG-KI-R5-C001; writable file
  frontend/lib/keyword-intelligence-view-model.ts; live starting digest
  5a193f82981d865b44e082a39a374cdf77d7ec3300bbfc3659246709a8ed3df5.
- Frozen transformation: one expression only,
  selectionSaveProjection(view.selection.items) to
  selectionSaveProjection(view.selection). Direct equal-saved and
  unsaved-different canFinalizeSelection oracles plus strip-types module load
  are required before acceptance.
- Invalidation: only EV-KI-R5-S16's erroneous canFinalizeSelection proof and
  resulting-file digest are superseded by C001. S16's unrelated filter and
  projection evidence remains valid. S012 remains unchanged and must be
  dependency-revalidated after C001 acceptance; S013 remains unexecuted.
- State transition: S2 state 19, current_subwindow KI-R5-C001,
  current_status READY, blocker null; S013 remains blocked from resumption
  until C001 is accepted.
- Coverage: no C001 local coverage IDs; no final gate run.
- External mutations / costs: none / $0.00.
- Review disposition: **CORRECTIVE-SUBWINDOW-READY**; stop at C001 leaf
  execution/review boundary.

---

## EV-KI-R5-S23 — C001 predecessor cycle corrected; readiness superseded

- Evidence ID / timestamp: EV-KI-R5-S23 / 2026-08-20T13:52:00+05:30.
- Parent window / assignment: KI-R5 / ASG-KI-R5-WA-01.
- Actor / role: KI-R5-WINDOW-AGENT / window agent.
- Authority: A5 state 116, EV-KI-A-055, and CHG-KI-030 authorize exactly two
  S1 edits: the C001 task-block and certificate predecessors become
  KI-R5-S010.
- Mechanical delta proof: live S1 contains exactly two C001 predecessor fields,
  both [KI-R5-S010], at lines 1550 and 1633; zero [KI-R5-S013] predecessor
  fields remain. Replacing only those two literals back to KI-R5-S013 with the
  deterministic two-line sed command reproduces prior S1 digest
  0f3ef85771392d164ad1e44f044c1b71659b84d44176b47aed58c4afaca35657.
  Live corrected S1 digest is
  0743b17406ecc1643510a1f36a19c9c0a4ba20acc868ff12788896cc4b5782da.
- Readiness proof: S010 is accepted; S013 remains unexecuted/blocked; C001
  has zero unresolved certificate choices and remains limited to the frozen
  one-expression change in view-model.ts. The S013 trigger is no longer a
  predecessor, so the cycle is removed.
- Supersession: EV-KI-R5-S22's readiness/pin claim is superseded only by this
  corrected readiness evidence. Its diagnosis, scope, transformation, starting
  digest, and zero-implementation statement remain valid.
- State effect: S2 may replace its decomposition pin with 0743b174…, preserve
  C001 as the sole READY leaf, and dispatch it without another parent review.
- External mutations / costs: none / $0.00.
- Review disposition: **CORRECTIVE-SUBWINDOW-READY**; C001 may execute under
  the unchanged EV-KI-A-054 local-oracle requirements.

---

## EV-KI-R5-S24 — C001 executed; window-agent review: ACCEPTED

- Evidence ID / timestamp: EV-KI-R5-S24 / 2026-08-20T14:05:00+05:30.
- Corrective subwindow / assignment: KI-R5-C001 / ASG-KI-R5-C001
  (frontend/lib/keyword-intelligence-view-model.ts).
- Leaf stop state: AWAITING_WINDOW_REVIEW; requester-authored commit 4db1d89
  on accepted S012 commit 5e2083c.
- Independent window-agent verification:
  - P1 PASS — pre-edit blob digest matches C001's pinned
    5a193f82981d865b44e082a39a374cdf77d7ec3300bbfc3659246709a8ed3df5;
    ending digest is
    fe068056e1484a5c4b1e82bfe21fdc8123dc72115354dbe188eb925d3f286f6d.
  - T1 PASS — the exact one-file diff has one deletion and one insertion:
    selectionSaveProjection(view.selection.items) became
    selectionSaveProjection(view.selection). No other expression, export,
    filter, projection, ordering, or error path changed.
  - V1 PASS — strip-types module load plus direct completed-view oracles pass:
    an equal SelectionItem[] draft returns {ok:true,reason:""} and a
    keyword-different draft returns {ok:false,reason:"unsaved"}; neither
    call throws TypeError.
  - V2 PASS — commit scope and diff name only the authorized file; root
    changed-file set remains 45 entries with digest
    02530e7cc6bba4e59291f1eba4cf5464b784bbabac4dfb2384c33fae90f54a74;
    frontend and backend worktrees are clean.
  - V3 PASS — no C001 local coverage is owned or executed; all integration
    cases remain assigned to their existing frozen owners.
  - H2 PASS — no second-file edit, successor implementation, external
    mutation, provider/AWS/database operation, destructive action, or
    window-agent implementation edit occurred; cost $0.00.
- Supersession and dependency revalidation:
  - EV-KI-R5-S16's resulting-file digest and canFinalizeSelection proof are
    superseded by this entry only. Its unrelated filter/parity and projection
    evidence remains valid.
  - S012 implementation remains byte-identical at
    19494a99a2be28683167908289176bf44ebb8d0bb1eb40f63cc6d1cd770c6337
    before and after C001. Its only affected dependency is
    canFinalizeSelection, whose repaired direct saved/unsaved proof above now
    satisfies the dashboard call contract; no S012 implementation rerun is
    required.
- Review disposition: **ACCEPTED_FOR_INTEGRATION.** C001 is accepted; S012
  dependency revalidation passed; S013 may resume as the next unexecuted
  initial leaf.

---

## EV-KI-R5-S25 — S013 leaf executed; window-agent review: ACCEPTED

- Evidence ID / timestamp: EV-KI-R5-S25 / 2026-08-20T14:20:00+05:30.
- Subwindow / assignment: KI-R5-S013 / ASG-KI-R5-S013
  (frontend/test/keyword-intelligence-api.test.ts).
- Leaf stop state: AWAITING_WINDOW_REVIEW; requester-authored commit 94ab4b2
  on accepted C001 commit 4db1d89.
- Independent window-agent verification:
  - P1 PASS — pre-edit blob digest matches
    a2f40c62bdf6d34136c2d6a318c8aef24e426581182a2d5edf0ef6fc950cd5c5;
    ending digest is
    d012c960d8d7d90a405d0de26c8884fbd56e11be5495987d4cea856376851c0a.
  - T1 PASS — every contractVersion fixture is numeric 1; only W5-A05,
    W5-A06, W5-A09, and W5-A10 are superseded; manual fixtures use draft
    keys; the actual W4 serializer/W5 parser, client mutation init captures,
    UI/backend filter parity cases, and four prescribed controls are present.
  - V1 PASS — the exact focused command
    node --experimental-strip-types --test test/keyword-intelligence-api.test.ts
    exits 0 with zero skips. The source emits one frontend_api certificate
    with the exact nine required/registered/executed IDs and digest
    dcf2126c268a44b559c150840317ca0f7d33b0f97c144c1e0e26eb47dc30f3f5.
  - V2 PASS — commit scope and diff name only the authorized test file; root
    changed-file set remains 45 entries with digest
    02530e7cc6bba4e59291f1eba4cf5464b784bbabac4dfb2384c33fae90f54a74;
    frontend and backend worktrees are clean.
  - V3 PASS — required = registered = executed frontend API set:
    R5-WIRE-01/02/03/05/06 and R5-EXP-01/02/03/04; skipped, duplicate,
    unexpected, and missing-witness sets are empty. Controls NC-01, NC-02,
    NC-08, and NC-09 use pass–mutate–fail–restore assertions.
  - H2 PASS — no production-file edit, unrelated W5 weakening, database,
    browser, enforcement, provider/AWS, destructive, or successor action
    occurred; cost $0.00.
- Residual obligations: V2 capture of the frontend_api certificate and the
  frozen merge gates remain owned by KI-R5-I001.
- Review disposition: **ACCEPTED_FOR_INTEGRATION.** S013 is accepted and S014
  / ASG-KI-R5-S014 is staged for
  frontend/test/keyword-intelligence-components.test.ts, with live starting
  digest 6e14ecc8eed297a6ca608ec365799b6cb2da2914d231944cb6be3047e24fe168.

---

## EV-KI-R5-S26 — S014 review rejected: component-lifecycle substitute lacks fidelity

- Evidence ID / timestamp: EV-KI-R5-S26 / 2026-08-20T14:30:00+05:30.
- Subwindow / assignment: KI-R5-S014 / ASG-KI-R5-S014
  (frontend/test/keyword-intelligence-components.test.ts).
- Leaf stop state: AWAITING_WINDOW_REVIEW; requester-authored commit f74c045
  changed only the authorized test file. Its starting digest matches
  6e14ecc8eed297a6ca608ec365799b6cb2da2914d231944cb6be3047e24fe168;
  ending digest is
  2fcb1c88df97f2471ed78a94d7e8aa70a91d89f206632213a75a4c4ebc3d6ba4.
- Local command result: the required focused command
  node --experimental-strip-types --test test/keyword-intelligence-components.test.ts
  exits 0 with zero skips. Scope/diff checks also pass.
- Review failure: R5-FIN-01 through R5-FIN-06 are activated through a newly
  invented local handoff()/retryHandoff() model and ComponentRequest trace.
  The file does not import ResearchDashboard, SelectionReview,
  startKeywordResearchRun, saveKeywordSelection, or a production request
  boundary. Thus its synthetic state/request trace can pass while the actual
  dashboard/review control locking, state transitions, and fetch handoff
  behavior are defective.
- Governing authority: A4 SCN-KI-038 requires actual component state/request
  capture. DEC-KI-037 limits substitute claims to the named serializer/parser,
  fetch-capture, emitted-Next, and DB classes; it does not authorize a local
  replacement handoff state machine as proof of FIN-01 through FIN-06.
- Required remedy: revise this one test file under a new corrective sub-window
  so its FIN cases activate the actual component/dashboard production path or
  another parent-authorized fidelity-preserving substitute. The current
  evidence cannot be accepted and must not be reclassified by a passing local
  model test.
- Authority result: A5 state 116 authorizes only the completed C001
  predecessor correction and C001 execution; it does not authorize an S1 C002
  amendment. No corrective leaf is authored or assigned.
- Coverage disposition: the literal R5_COMPONENT_CASES registry exists but its
  executed FIN witnesses are invalid for acceptance; no valid component
  certificate is available. No external mutation, provider/AWS/database call,
  destructive action, or cost occurred.
- Review disposition: **PARENT_BLOCKED** pending parent authorization of a
  decision- and execution-complete one-file S014 corrective sub-window.

---

## EV-KI-R5-S27 — C002/browser realignment authored; parent review required

- Evidence ID / timestamp: EV-KI-R5-S27 / 2026-08-20T14:45:00+05:30.
- Authority verified: A5 state 117 (`CORRECTIVE_AUTHORING_AUTHORIZED`),
  `EV-KI-A-056`, and `CHG-KI-031` authorize only S1/S2/S3 reauthoring for
  the S014 substitute-fidelity defect. Their pinned A1/A3/A4 revisions match
  S2; implementation/test edits, C002/S015 dispatch, browser/build/enforcement
  execution, and KI-W6 remain prohibited.
- Exact S1 amendment: prior S1 digest
  `0743b17406ecc1643510a1f36a19c9c0a4ba20acc868ff12788896cc4b5782da` became
  `80c81cf2e71e3bff61a88dafdd71d8d579bb93e13e56b759ac663de60387d2e5`.
  It appends decision- and execution-complete `KI-R5-C002`, frozen to remove
  only S014's invented component handoff/retry model, FIN-01..06, NC-05/06,
  and components certificate while preserving W5-C05/C08/C12.
- Allocation realignment: revised S015 is blocked on accepted C002 and owns
  literal `R5_BROWSER_CASES = [R5-WIRE-04, R5-FIN-01..06]`; FIN activation is
  CDP operation of the emitted hydrated dashboard with production request
  capture. The specification identifies actual remove-and-readd as the UI's
  reorder path. S016 forbids a components registry/certificate; S018/I001
  consume exactly `api`, `database`, `frontend_api`, and `browser` certificates.
  V2 captures only `frontend_api`; V4 captures the seven-ID browser certificate;
  V6/E1 merge the four certificates plus conformance.
- Preservation proof: S017 remains byte-for-byte unchanged by authorization;
  the manifest groups, all 34 case IDs, the five manifest per-group digests,
  and global digest `507186e7489a3f9eec18eb5de78692dbc55a8d1d2d106544aa4295a98ac9be60`
  are unchanged. No case other than FIN-01..06 and no control other than
  NC-05/06 moved.
- Mechanical review: S1 has one C002 writable file, C002→S015 and S015→S016/
  S018 dependency edges, and no C002/S015 assignment. Registry/certificate
  references were reconciled to five registries (four non-conformance plus
  conformance); historical S014 instructions are explicitly superseded.
- State disposition: S2 state 24 pins the new S1 revision and records
  `AWAITING_PARENT_DECOMPOSITION_REVIEW`; `KI-R5-C002` and revised S015 are
  unassigned. No implementation/test file changed, no focused/browser/build/
  database/enforcement command ran, no provider/AWS/production/destructive
  action or commit occurred.
- Review request: parent must independently approve or return the amended S1.
  On approval only, the window agent may set S2 READY and dispatch C002;
  without it, no leaf may start.

---

## EV-KI-R5-S28 — C002 realignment precision revision authored; parent review required

- Evidence ID / timestamp: EV-KI-R5-S28 / 2026-08-20T15:00:00+05:30.
- Authority verified: A5 state 118 (`CORRECTIVE_REVISION_REQUIRED`),
  `EV-KI-A-057`, and `CHG-KI-032` authorize only the five stated S1/S2/S3
  corrections. C002/S015 execution and all implementation/test edits remain
  prohibited.
- Supersession: this entry supersedes only `EV-KI-R5-S27`'s readiness claim;
  its root-cause, no-execution, seven-ID reallocation, four-certificate
  arithmetic, and S017-preservation observations remain valid.
- Exact S1 revision: `80c81cf2e71e3bff61a88dafdd71d8d579bb93e13e56b759ac663de60387d2e5`
  became `4cf412ce19daeb3c043d4d872223c8ad74a73587eb35f84d56a63413f7f53b00`.
- Five correction proof: C002 now removes the rejected-model-only
  `editSelectedItemText` import in its authorized action, ordered edit, diff
  oracle, and absence check. S015 authorizes exactly the five mutable W5
  browser oracles `W5-B02`, `W5-B03`, `W5-B04`, `W5-B05`, and `W5-R03`.
  S1 states that the S015 browser registry alone executes A4 `FCOMP`
  lifecycle evidence and NC-05/06; S016 is lint-only. S018 has explicit
  canonical read paths for all four case registries, components/inventory
  tests, the changelog, manifest, decision ledger, and nested git metadata.
- C002 certificate correction: `status: READY`; `invalidated_evidence: []`;
  `invalidated_gates: []`. `EV-KI-R5-S26` remains trigger evidence. S1 prose
  records planned V2/V4/E1/V6 specification replacement without claiming an
  executed-gate invalidation.
- Preservation proof: S017 instructions/fixture bytes remain untouched; the
  manifest still contains exactly the unchanged 34 IDs, five group digests,
  and global digest
  `507186e7489a3f9eec18eb5de78692dbc55a8d1d2d106544aa4295a98ac9be60`.
  No case other than FIN-01..06 and no control other than NC-05/06 moved.
- State disposition: S2 state 25 pins S1 revision `4cf412ce…` and remains
  `AWAITING_PARENT_DECOMPOSITION_REVIEW`. No leaf is assigned or executed;
  no focused/browser/build/database/enforcement command, external action,
  destructive action, or commit occurred.
- Review request: parent must approve or return this corrected decomposition.
  Only a future approval can make C002 dispatchable.

---

## EV-KI-R5-S29 — S017 literal preservation mechanical proof

- Evidence ID / timestamp: EV-KI-R5-S29 / 2026-08-20T15:00:00+05:30.
- Read-only command: a Node assertion extracted only the S017 block from S1
  and required all five literal groups (`wire` 6, `selection` 8,
  `finalization` 8, `export` 6, `conformance` 6) plus the five per-group
  digests and global digest. Outcome:
  `S017_LITERAL_PRESERVATION=PASS groups=5 ids=34 digests=6`.
- Scope checks: `git -C frontend status --short`, `git -C email_scraper
  status --short`, and `git diff --check` produced no output. No test,
  browser/build, database, enforcement, provider, AWS, production, destructive,
  or commit action occurred.

---

## EV-KI-R5-S30 — C002 live-dispatch P1 correction and inverse proof

- Evidence ID / timestamp: EV-KI-R5-S30 / 2026-08-20T15:08:00+05:30.
- Authority verified: A5 state 119, `EV-KI-A-058`, and `CHG-KI-033` authorize
  exactly one S1 line change: C002 completion checklist P1.
- Exact replacement: the obsolete fixed `parent state 117` P1 became the live
  dispatch oracle requiring A5 assignment `ASG-KI-R5-WA-01`, the parent-approved
  decomposition revision recorded at dispatch, predecessor evidence, writable
  file, and both starting digests; A5 state 117 remains historical authoring
  authority only.
- Forward digest: S1 `4cf412ce19daeb3c043d4d872223c8ad74a73587eb35f84d56a63413f7f53b00`
  became `65b91920edd84720f469d1bbbd57b0837fc0b1bfb11621f4a0f13f9f4ba4ef61`.
  Inverse proof: streaming the one exact old P1 line back into the current S1
  reproduces `4cf412ce19daeb3c043d4d872223c8ad74a73587eb35f84d56a63413f7f53b00`.
- Scope: no other S1 normative change; registry/certificate/gate allocations,
  S017 instructions, all 34 IDs and group/global digest literals, and all
  implementation/test files remain unchanged. S2 state 26 pins the new S1
  digest and remains `AWAITING_PARENT_DECOMPOSITION_REVIEW`.
- No leaf assignment/execution, test/browser/build/database/enforcement command,
  external mutation, destructive action, or commit occurred. Parent approval is
  still required before C002 can dispatch.

---

## EV-KI-R5-S31 — C002 P1 dispatch preflight blocked by frozen root digest

- Evidence ID / timestamp: EV-KI-R5-S31 / 2026-08-20T15:12:00+05:30.
- Parent approval recorded: A5 state 120 / `EV-KI-A-059` / `CHG-KI-034`
  approves S1 revision
  `65b91920edd84720f469d1bbbd57b0837fc0b1bfb11621f4a0f13f9f4ba4ef61`.
  S2 is therefore converted to `decomposition_status: READY`.
- C002 P1 results: S1 and on-disk component-test digests match exactly
  (`65b91920…`; `2fcb1c88df97f2471ed78a94d7e8aa70a91d89f206632213a75a4c4ebc3d6ba4`),
  and both nested repositories are clean. The required root digest fails:
  frozen C002 value
  `02530e7cc6bba4e59291f1eba4cf5464b784bbabac4dfb2384c33fae90f54a74`
  versus live 45-entry `git status --porcelain | LC_ALL=C sort` digest
  `c660d09a800e8a5fd446bd65039f55241d5d7bb4e4c7ef656fe4fc7dcc88417c`.
- Causal authority: C002 P1 requires both starting digests to match; S1 is
  frozen by A5 state 120 and no action authorizes an S1 root-digest amendment.
  A valid unique assignment cannot be issued with failed P1. C002 and S015
  remain unassigned; no leaf received write authority.
- Disposition: **PARENT_BLOCKED**. Parent reapproval is required for a
  decision-complete S1 correction to C002's frozen root digest, followed by a
  fresh preflight and dispatch. No implementation/test edit, focused test,
  browser/build/database/enforcement command, external action, destructive
  action, commit, successor, KI-W6, or KI-W7 work occurred.

---

## EV-KI-R5-S32 — C002 corrected digest, P1 pass, and dispatch

- Evidence ID / timestamp: EV-KI-R5-S32 / 2026-08-20T15:14:43+05:30.
- Authority: A5 state 121 / `EV-KI-A-060` / `CHG-KI-035` authorize exactly one
  C002 YAML literal replacement and immediate dispatch after P1 passes.
- Exact S1 delta: only C002
  `starting_repository_change_set_digest` changed
  `02530e7cc6bba4e59291f1eba4cf5464b784bbabac4dfb2384c33fae90f54a74` →
  `c660d09a800e8a5fd446bd65039f55241d5d7bb4e4c7ef656fe4fc7dcc88417c`.
  Corrected S1 digest: `cdb235dc0b6a3e2ca2027296e083ccb5f60e63a068e2a0a5f61d7d7ae6360856`.
  Streaming the old literal back reproduces prior approved S1
  `65b91920edd84720f469d1bbbd57b0837fc0b1bfb11621f4a0f13f9f4ba4ef61`.
- C002 P1 PASS: S1 pin matches; writable-file digest is
  `2fcb1c88df97f2471ed78a94d7e8aa70a91d89f206632213a75a4c4ebc3d6ba4`;
  live root status is 45 entries with sorted-LF digest `c660d09a…`; frontend
  and backend nested worktrees are clean; the parent assignment remains
  `ASG-KI-R5-WA-01` and A5 state 121 is `DECOMPOSITION_APPROVED`.
- Dispatch: `KI-R5-C002` is assigned to `KI-R5-C002-LEAF` under unique
  `ASG-KI-R5-C002`, with exactly one writable file
  `frontend/test/keyword-intelligence-components.test.ts`. The leaf must apply
  the approved C002 ordered removal only, run its one focused component
  regression, return its certificate at `AWAITING_WINDOW_REVIEW`, and not start
  S015. S015 remains reserved pending independent C002 acceptance.
- No implementation edit, test, external mutation, destructive action, or
  commit has occurred during this window-agent correction/dispatch step.

---

## Leaf execution evidence (appended by the window agent after each review)

*(leaf review evidence is recorded in the `EV-KI-R5-S07`+ entries above; this
placeholder section is superseded and reserved)*

---

## EV-KI-R5-S33 — C002 accepted; S015 predecessor revalidated and dispatched

- Evidence ID / timestamp: EV-KI-R5-S33 / 2026-08-20T15:30:00+05:30.
- Authority: A5 state 121 remains `DECOMPOSITION_APPROVED`; its authorized
  sequential action is independent C002 review followed by S015 dispatch only
  after C002 acceptance. S1 is pinned at
  `cdb235dc0b6a3e2ca2027296e083ccb5f60e63a068e2a0a5f61d7d7ae6360856`.
- C002 input/ending proof: assigned starting digest
  `2fcb1c88df97f2471ed78a94d7e8aa70a91d89f206632213a75a4c4ebc3d6ba4`;
  ending digest
  `cb980ba0d75cf60306f3e9622f3472b7cf05a64d01eadf60c0e216c4cfe4b38e`.
  Requester-authored commit `3a28c6987625f1701ce7bf3ce10c31e5fe5339c3`
  has parent `f74c045` and names exactly
  `frontend/test/keyword-intelligence-components.test.ts` (211 deletions,
  one formatting-only line addition). Frontend and backend worktrees are clean;
  the owner-controlled root status remains 45 paths with sorted-LF digest
  `c660d09a800e8a5fd446bd65039f55241d5d7bb4e4c7ef656fe4fc7dcc88417c`.
- T1/T2 PASS: independent diff inspection confirms removal of only the named
  `editSelectedItemText` import, contiguous invented component
  handoff/retry model, FIN-01..06 and NC-05/06 registry subtests, and its
  components certificate. The necessary W5-C12 title deletion removes its
  obsolete R5-FIN reference without changing test behavior or its oracle.
  `REGISTERED_CASE_IDS`, the W5 certificate construction, W5-C05, W5-C08,
  W5-C12 assertions, and every other retained W5 assertion remain intact.
- V1 PASS: from `frontend/`, exact command
  `node --experimental-strip-types --test test/keyword-intelligence-components.test.ts`
  exited 0: 1 file test passed, 0 failed, 0 skipped, 0 todo. The retained W5
  certificate construction is unchanged.
- V2/V3 PASS: static absence search finds no `editSelectedItemText`,
  `R5_COMPONENT_CASES`, `registry: "components"`, `handoff(`,
  `retryHandoff(`, `R5-FIN-`, `R5-NC-05`, `R5-NC-06`, or
  `KI_R5_EXECUTION_CERTIFICATE` in the components test. No browser, build,
  enforcement, database, provider, AWS, production, destructive, successor,
  or KI-W6 action was run. `git show --check` reports only the end-of-file
  blank line caused by removal of the final former registry block; it introduces
  no executable/test/oracle content.
- Disposition: `ACCEPTED_FOR_INTEGRATION`. `KI-R5-C002` is accepted and S014
  remains superseded. Revised S015 predecessors are independently satisfied by
  accepted S012 (`EV-KI-R5-S20`) and this C002 disposition. Its live browser
  harness starting digest is
  `d28cc1b5411d412edeba139f715da69ab5c09a8d67c543be4cc69719ef5e68a7`;
  it is dispatched uniquely as `ASG-KI-R5-S015` to `KI-R5-S015-LEAF` with
  only `frontend/test/browser/keyword-intelligence-dashboard.mjs` writable.
  S015 may run only its structural local checks; V4 retains the sole browser/
  build execution authority.

---

## EV-KI-R5-S34 — S015 review blocked: FIN-04 omits the required rendered save action

- Evidence ID / timestamp: EV-KI-R5-S34 / 2026-08-20T16:00:00+05:30.
- Scope/preflight: S015 requester-authored commit
  `d4763a771734dfe043d59e2a4ae5b0dc6e0371c9` has parent `3a28c69` and changes
  exactly `frontend/test/browser/keyword-intelligence-dashboard.mjs` from
  assigned digest
  `d28cc1b5411d412edeba139f715da69ab5c09a8d67c543be4cc69719ef5e68a7` to
  `ea7ab5ff8ac6368ff278520fa79876dcd30c8764fb3e8f6fb7a066cf3d95805d`.
  `node --check test/browser/keyword-intelligence-dashboard.mjs` exits 0.
  The frontend and backend worktrees are clean; root status remains 45 paths
  with sorted-LF digest `c660d09a800e8a5fd446bd65039f55241d5d7bb4e4c7ef656fe4fc7dcc88417c`.
- Independent review failure: in `R5-FIN-04`, after the actual manual-input/Add
  action makes a dirty three-item draft, the next operation is
  `waitForInPage(... PUT ... , "save PUT captured")`. No preceding `click` of
  the rendered `Save selection` button exists in that scenario. Its fixture
  produces a PUT only when that control is clicked. The wait therefore times
  out and the required canonical-save, incremented-revision, and subsequent
  finalize POST witnesses cannot execute. This is a deterministic omitted
  behavior, not an environmental/browser prerequisite.
- Required correction: insert exactly the existing rendered-control operation
  `await click(cdp, "[...document.querySelectorAll('[data-surface=\\\"surface:selection-review\\\"] button')].find(n => n.textContent.includes('Save selection'))");`
  between the manual-add readiness wait and `waitForInPage` in R5-FIN-04.
  No parent-level behavior decision is needed, but the standard requires a new
  single-file corrective sub-window with a fresh baseline and assignment;
  reopening S015 is prohibited.
- Authority disposition: A5 state 121 authorizes no S1 change beyond the
  already-completed C002 digest replacement. It therefore does not authorize
  authoring/dispatching KI-R5-C003. `CORRECTION_REQUIRED` is mechanically known
  but cannot be assigned; disposition is `PARENT_BLOCKED`. S015, S016, S017,
  S018, and I001 remain unassigned. No browser/build/enforcement/database,
  provider/AWS/production/destructive action, successor, or KI-W6 work ran.

---

## EV-KI-R5-S35 — review-only C003 accepted; S016 dispatched

- Evidence ID / timestamp: EV-KI-R5-S35 / 2026-08-20T16:15:00+05:30.
- Authority and documentation: A5 state 122 / `EV-KI-A-061` / `CHG-KI-036`
  authorize only the requester exception: S1 review-only C003 authoring plus
  independent window-agent review of existing commit `4dd9b4f`, with no
  implementation write or C003 leaf. S1 now hashes
  `5b4d9e846560c1ee81b2b42c2589485049c3c9a4cb3c3acddff9b9725d30ef05` and
  contains the C003 review target, exact ancestry, digests, placement oracle,
  structural checks, and prohibitions.
- P1/T1 PASS: `4dd9b4f0357b7c118d6c8ea92af212c7ff0693ba` has exactly parent
  `d4763a771734dfe043d59e2a4ae5b0dc6e0371c9`, names only
  `frontend/test/browser/keyword-intelligence-dashboard.mjs`, and is exactly
  four insertions/zero deletions. The additions are the three prescribed
  explanatory comment lines and one rendered Save selection `click`, placed
  after FIN-04's dirty-three-item readiness witness and before its
  `waitForInPage` PUT witness. Pre-fix/candidate digests are respectively
  `ea7ab5ff8ac6368ff278520fa79876dcd30c8764fb3e8f6fb7a066cf3d95805d` and
  `1c4cc5ae801f586398cf2e7a30c785f84868001d215fd85bd3d1bc0a920deb01`.
- V1 PASS: exact command from `frontend/`,
  `node --check test/browser/keyword-intelligence-dashboard.mjs`, exits 0.
  No browser/build/V4, enforcement, database, full regression, provider, AWS,
  production, destructive, or KI-W6 action ran.
- V2 PASS: complete S015 structural inspection reports
  `S015_C003_STRUCTURAL=PASS ids=7 numeric_versions=4`: the exact seven-ID
  `R5_BROWSER_CASES` registry remains; no `ki-research-v1` string remains;
  all four fixture contract versions are numeric literals; all seven R5 cases
  remain rendered-control/request-capture scenarios; the seed-dresses export
  remains `LITERAL_EXPORT_CSV_SEED_DRESSES`, pass-through/NC-11 remains, and
  the browser certificate exists only for deferred V4 execution. No direct
  `startKeywordResearchRun` or `saveKeywordSelection` call is present.
- Scope/preconditions: frontend and backend worktrees are clean. The live root
  status remains 45 paths with sorted-LF digest
  `c660d09a800e8a5fd446bd65039f55241d5d7bb4e4c7ef656fe4fc7dcc88417c`.
  `frontend/test/keyword-intelligence-inventory.test.ts` matches S016's
  starting digest
  `67828152b71f9b05ec847d5fc0d3be238452d526aeffee8255e17b39a644f480`.
- Disposition: `ACCEPTED_FOR_INTEGRATION`. C003 accepts the requester-supplied
  repair and supersedes the blocked S015 disposition; S015 remains superseded
  rather than accepted in its defective original form. `KI-R5-S016` is
  immediately dispatched as `ASG-KI-R5-S016` to `KI-R5-S016-LEAF`, with only
  `frontend/test/keyword-intelligence-inventory.test.ts` writable. S017–I001
  remain unassigned; KI-W6 remains prohibited.

---

## EV-KI-R5-S36 — S016 blocked by frozen W5-I02 legacy version fixture

- Evidence ID / timestamp: EV-KI-R5-S36 / 2026-08-20T16:30:00+05:30.
- Preflight: no S016 file edit occurred. The assigned inventory-test digest
  remains `67828152b71f9b05ec847d5fc0d3be238452d526aeffee8255e17b39a644f480`;
  frontend and backend worktrees are clean and root status remains 45 paths
  with sorted-LF digest
  `c660d09a800e8a5fd446bd65039f55241d5d7bb4e4c7ef656fe4fc7dcc88417c`.
- Independent reproduction: the exact required command from `frontend/`,
  `node --experimental-strip-types --test test/keyword-intelligence-inventory.test.ts`,
  exits 1 (0 pass, 1 fail, 0 skip). TAP attributes the file failure to the
  inventory test; the source-level oracle below identifies its deterministic
  cause without changing the file.
- Root cause: `minimalView()` and its nested `result()` retain
  `contractVersion: "ki-research-v1"`, while accepted S008's
  `parseResearchView` accepts only `source.contractVersion === 1` and otherwise
  throws `new ApiPayloadError("research.contractVersion")`. W5-I02 passes the
  minimal view to `parseResearchEnvelope` inside `assert.doesNotThrow`, making
  the required full pass impossible on the pre-S016 baseline.
- Boundary proof: S016 authorizes only an additive static registry-lint block
  and explicitly prohibits changing any W5-I oracle; its exact transformation
  says no existing W5-I0x oracle changes. DEC-KI-037's exhaustive mutable set
  excludes W5-I02, leaving it byte/semantic read-only. S013's authorized
  numeric-fixture updates did not include the inventory test. The locked
  specification therefore supplies no authorized owner for this necessary
  fixture correction at S016 execution time.
- Required next action: a parent-authorized one-file `KI-R5-C004` must own only
  `frontend/test/keyword-intelligence-inventory.test.ts`, update the two
  fixture version literals to numeric `1` while preserving the W5-I02 oracle,
  then re-run the focused inventory test and resume S016's additive registry
  work under a fresh baseline. A5 state 122 permits no C004 authoring or
  assignment. Disposition: `PARENT_BLOCKED`; S016 and every successor remain
  unassigned. No browser/build/enforcement/database/provider/AWS/production,
  destructive, successor, or KI-W6 action ran.

## Corrective sub-window evidence

### EV-KI-R5-S37 — C004 reviewed and accepted; fresh S016 baseline issued

- Evidence ID / timestamp: EV-KI-R5-S37 / 2026-08-20T16:43:55+05:30.
- Authority: A5 state 123, `EV-KI-A-062`, and `CHG-KI-037`. The exact C004
  block is appended to S1 §11.1; its live revision is
  `e73d80946af502c2e5d7225f0eeccdd5603535fdefbb05e19ccd2a13afb1a6b4`.
- Change provenance and P1/P2: requester-preserved commit
  `acf02e3bda9c4a037cc41a7fc9af8a2173ef8723` has parent `4dd9b4f`; its only
  changed path is `frontend/test/keyword-intelligence-inventory.test.ts`.
  The parent blob hashes to the authorized C004 baseline
  `67828152b71f9b05ec847d5fc0d3be238452d526aeffee8255e17b39a644f480`;
  the candidate ending blob hashes to
  `0fb64ea35701be7f5788aced0c5bc3989c9180c57bfd516c525ea0c4cc3cae04`.
  Both nested worktrees are clean and the protected root 45-path set remains
  `c660d09a800e8a5fd446bd65039f55241d5d7bb4e4c7ef656fe4fc7dcc88417c`.
- T1/V2: the commit is exactly one file, two replacements, zero additions
  outside those replacements: `result()` and `minimalView()` each change only
  `contractVersion: "ki-research-v1"` to `contractVersion: 1`. The resulting
  file has zero legacy string occurrences and exactly two numeric fixture
  occurrences. `W5-I02`, every other W5-I oracle, the W5 execution-certificate
  emission, negative controls, registry content, and S016 block are not part
  of C004's diff.
- V1: from `frontend/`, `node --experimental-strip-types --test
  test/keyword-intelligence-inventory.test.ts` exits 0 (`pass 1`, `fail 0`,
  `skipped 0`). No V2/V4/build/browser/database/full-regression/enforcement,
  provider, AWS, production, destructive, or KI-W6 operation ran.
- Disposition: `ACCEPTED_FOR_INTEGRATION`. `0fb64ea3…` is the C004 ending
  digest and the fresh, verified S016 baseline. `ASG-KI-R5-S016-R1` is the
  replacement assignment; it may only append S016's frozen registry lint.

### EV-KI-R5-S38 — S016 reviewed and accepted; S017 dispatched

- Evidence ID / timestamp: EV-KI-R5-S38 / 2026-08-20T16:43:55+05:30.
- Preconditions: C004 is accepted above. Requester-preserved commit
  `c80db6ab9d899ce8936db29ce1f49a59b4f95bfd` directly follows `acf02e3`;
  its parent inventory blob is the fresh C004 ending digest `0fb64ea3…` and
  its current ending digest is
  `5ec4ef0ae24859200975b37e53bc55c7c81baaf917628ac213ef3b0df4fc5bd8`.
  It changes exactly the S016 writable file (128 insertions, no deletion);
  frontend/backend worktrees are clean and the root 45-path digest is
  unchanged at `c660d09a…`.
- Exact transformation: the one appended block reads only the three frozen
  sibling frontend test files, rejects `R5_COMPONENT_CASES` and a
  `registry: "components"` certificate, deep-compares the required nine-ID
  `R5_FRONTEND_CASES` and seven-ID `R5_BROWSER_CASES` owner sets, and checks
  each discovered R5 case citation is both declared in the local manifest set
  and located in its exact owner registry (with comments/supersession citations
  exempted as specified). Its literal sets equal S1 §4.2 exactly: frontend API
  owns WIRE 01/02/03/05/06 plus EXP 01–04; browser owns WIRE 04 plus FIN 01–06.
- Preservation: the pre-existing W5-I01–W5-I06 bodies, W5-I02's export-surface
  and strict-parser assertions, `KI_W5_EXECUTION_CERTIFICATE` emission, all
  registration content, and the two C004 numeric fixtures are byte-identical
  outside the append. No manifest file, certificate line, case ID allocation,
  or other path changed.
- LOCAL_NOW: the focused inventory command recorded above exits 0 with zero
  skip and executes the final appended static lint. No V2/V4/build/browser/
  database/full-regression/enforcement, provider, AWS, production, destructive,
  successor implementation, or KI-W6 action ran during review.
- Disposition: `ACCEPTED_FOR_INTEGRATION`. S016's accepted ending digest is
  `5ec4ef0a…`. `KI-R5-S017` / `ASG-KI-R5-S017` is now the only assigned leaf,
  owning only the absent literal enforcement-manifest fixture; S018 and I001
  remain unassigned.

## EV-KI-R5-S39 — S017 reviewed and accepted; S018 dispatched

- Evidence ID / timestamp: EV-KI-R5-S39 / 2026-08-20T16:53:52+05:30.
- Authority and preconditions: A5 state 123 authorizes sequential S017 then
  S018 after independent review. S2 state 33 was `READY` for S017; its assigned
  file was absent at dispatch. The frozen S1 revision remains
  `e73d80946af502c2e5d7225f0eeccdd5603535fdefbb05e19ccd2a13afb1a6b4`.
- Change provenance and scope: requester commit
  `ed3878446e7f11686004ccf705f5ed7476c6cdbb` adds exactly
  `email_scraper/test/fixtures/keyword-intelligence/ki-r5-enforcement-manifest-v1.json`
  (49 additions, zero deletions), with no whitespace errors. Its ending file
  digest is `e9f11c915d20e368aa7b9eb8e7f497b1837d7970b14ff68bf340d1326d85c180`.
  Both nested worktrees are clean; the owner-controlled root remains 45 paths
  with sorted-LF digest
  `c660d09a800e8a5fd446bd65039f55241d5d7bb4e4c7ef656fe4fc7dcc88417c`.
- Literal-manifest review: strict JSON parse confirms exactly root keys
  `contractVersion`, `groups`, version `ki-r5-enforcement-manifest-v1`, and
  groups `wire`, `selection`, `finalization`, `export`, `conformance` in A4
  order. Their ordered members are exactly R5-WIRE-01..06, R5-SEL-01..08,
  R5-FIN-01..08, R5-EXP-01..06, and R5-CONF-01..06: 34 unique IDs and no
  metadata or extra IDs.
- LOCAL_NOW PASS: recomputation using UTF-8/LF/SHA-256 produces the frozen
  per-member group digests: wire `64e53c38…`, selection `a7fe88a1…`,
  finalization `14330e67…`, export `6d4ca77b…`, conformance `5960be17…`.
  The frozen UTF-8-sorted 34-ID digest also passes exactly:
  `507186e7489a3f9eec18eb5de78692dbc55a8d1d2d106544aa4295a98ac9be60`.
  No browser/build/database/full-regression/enforcement execution, provider,
  AWS, production, destructive, or KI-W6 work ran.
- Disposition: `ACCEPTED_FOR_INTEGRATION`. S018 is dispatched as
  `ASG-KI-R5-S018` to `KI-R5-S018-LEAF`, with only
  `email_scraper/test/keyword-intelligence-r5-enforcement.test.js` writable.
  It may run only its frozen syntax/static leaf checks and must stop at
  `AWAITING_WINDOW_REVIEW`; the CONF execution and 34-ID merge remain I001-only.

## EV-KI-R5-S40 — S018 reviewed and accepted; I001 dispatched

- Evidence ID / timestamp: EV-KI-R5-S40 / 2026-08-20T17:15:00+05:30.
- Authority and preconditions: A5 state 123 authorizes S018 after S017 and
  reserves personal I001 execution for the window agent once all leaves are
  accepted. S2 state 34 assigned S018 with an absent writable file; S001–S017
  (with accepted C001–C004 corrections) are accepted. The frozen S1 revision
  remains `e73d80946af502c2e5d7225f0eeccdd5603535fdefbb05e19ccd2a13afb1a6b4`.
- Change provenance and scope: requester commit
  `fe224741ea51a741d0ee7615ff4dbfd927a1599a` follows `ed3878446e7f11686004ccf705f5ed7476c6cdbb`
  and adds exactly `email_scraper/test/keyword-intelligence-r5-enforcement.test.js`
  (677 additions, zero deletions). `git diff --check` passes. The ending file
  digest is `465b3d9fd5b43d2b5f34573a0ab392c58205ff4fce2b7f5b2b86abbdfed17bf4`.
  Both nested worktrees are clean; the protected root has 45 normal-status
  entries and its sorted-LF digest remains
  `c660d09a800e8a5fd446bd65039f55241d5d7bb4e4c7ef656fe4fc7dcc88417c`.
- Frozen transformation review: the new file owns the exact six-member
  `R5_CONFORMANCE_CASES` literal, requires exactly the four `api`,
  `database`, `frontend_api`, and `browser` certificates before registering
  CONF-01–06, parses the literal S017 manifest with duplicate rejection before
  set creation, statically enumerates all five registries, validates their
  required/registered/executed digests, and constructs the exact sorted
  34-ID merged certificate. CONF-03 through CONF-05 contain the prescribed
  DEC-KI-037 supersession, scope, and substitute-fidelity lints. The seven
  synthetic NC-12 variants emit exactly `R5_REQUIRED_SET_MISMATCH`,
  `R5_REQUIRED_CASE_SKIPPED`, `R5_CASE_ID_INVALID` (duplicate and unexpected),
  `R5_ACTIVATION_WITNESS_MISSING`, `R5_ORACLE_WEAKENED`, and
  `R5_SUBSTITUTE_FIDELITY_DIVERGED`.
- LOCAL_NOW PASS: `node --check test/keyword-intelligence-r5-enforcement.test.js`
  exits 0. With no certificate input, the pure helpers parse the S017 manifest,
  resolve each of the five registered sets equal to its frozen required set and
  exact digest, and prove untouched synthetic evidence passes before and after
  every NC-12 falsification. No CONF test registration/execution, 34-ID merge,
  browser/build/database/full-regression/enforcement execution, provider,
  AWS, production, destructive, or KI-W6 work ran.
- Disposition: `ACCEPTED_FOR_INTEGRATION`. S018's ending digest above is
  accepted. All leaves are now accepted; `KI-R5-I001` /
  `ASG-KI-R5-I001` is dispatched to the window agent. Its frozen V1–V7 gates
  and the one E1 enforcement run remain unexecuted and must be performed only
  in I001.

## Integration assessment evidence

## EV-KI-R5-I001-01 — V1 pass; V2 certificate-capture blocker

- Evidence ID / timestamp: EV-KI-R5-I001-01 / 2026-08-20T17:24:00+05:30.
- Authority and inputs: A5 state 123 authorizes exactly one final-input run of
  V1–V7 and E1 in order for I001. S2 state 35 was READY, all leaves were
  accepted, S1 remained pinned at
  `e73d80946af502c2e5d7225f0eeccdd5603535fdefbb05e19ccd2a13afb1a6b4`, and
  both nested worktrees were clean before gate execution.
- V1 observed / expected / activation: the exact command from `email_scraper/`,
  `node --test --test-isolation=none test/keyword-intelligence-api.test.js`,
  first failed only at localhost binding with `listen EPERM: operation not
  permitted 127.0.0.1`. This is the documented restricted-sandbox condition,
  so the identical command was rerun with the required localhost permission.
  It passed **46/46**, zero fail/cancel/skip/todo, and emitted exactly one R5
  certificate: `registry: "api"`; required = registered = executed = the ten
  allocated IDs; skipped and oracleFailures empty; all three digests
  `3db029274e44b2a25ce1e551a10ef9c689ef71e6b4dedcac4e258175fc092a84`.
- V2 observed / expected / activation: the exact frozen command from
  `frontend/`, `node --experimental-strip-types --test
  test/keyword-intelligence-api.test.ts test/keyword-intelligence-components.test.ts
  test/keyword-intelligence-inventory.test.ts`, exited 0: 3 tests passed,
  zero fail/cancel/skip/todo. Its complete emitted output contains only those
  three file-level TAP lines and summary; it contains no
  `KI_R5_EXECUTION_CERTIFICATE=` line. The API test source at lines 913–922
  defines the required `frontend_api` certificate only through nested
  `t.diagnostic()`. Under this command's required default per-file isolation,
  that diagnostic is not surfaced in observable output, so it cannot be
  captured for I001.
- Causal path / governing rule: S1 §6 V2 requires capture of that certificate;
  S1 §6 E1 requires all four *captured* certificates and expressly forbids a
  partial-certificate enforcement run. S1 permits no V2 rerun after a passing
  command without an invalidation, and I001 has no implementation-file write
  authority. Reconstructing the JSON from source would not satisfy the required
  execution witness.
- Disposition: `PARENT_BLOCKED`. V3, V4, V5, E1, V6, and V7 were not run. No
  implementation or S1 file changed; no provider, AWS, production, database,
  commit, push, KI-W6, or external mutation occurred. Parent correction is
  required to make the one allowed V2 execution emit a capturable certificate
  (or otherwise revise the frozen evidence protocol) before I001 can resume.

## EV-KI-R5-I001-02 — V2 evidence-protocol correction accepted for rerun

- Evidence ID / timestamp: EV-KI-R5-I001-02 / 2026-08-20T17:26:00+05:30.
- Parent authority: A5 state 124, `EV-KI-A-063`, and `CHG-KI-038` classify the
  prior V2 result as evidence-protocol-only and authorize no implementation
  work. They permit exactly one S1 change: V2 inserts
  `--test-isolation=none` after `--test`, plus the parent-adjudication record.
- Mechanical amendment: S1 now hashes
  `c5411cb28ab806522ac28977b447ab91816f691a4bd4fe9209773f06b596571e`.
  The three selected files, cwd, three-file outcome, `frontend_api` registry,
  cases, controls, digests, certificate payload, and every other V1–V7/E1
  instruction are unchanged. S2 state 37 pins that revision and returns I001
  to READY.
- Invalidation/resumption: only V2 acceptance evidence is invalidated. V1's
  successful `api` certificate remains accepted and must not be repeated. The
  corrected V2 command may execute once; on its exact certificate capture and
  pass result, I001 resumes at V3. No implementation file changed.

## EV-KI-R5-I001-03 — corrected V2 pass; isolated V3 prerequisite absent

- Evidence ID / timestamp: EV-KI-R5-I001-03 / 2026-08-20T17:28:00+05:30.
- Corrected V2 (single authorized execution): `node --experimental-strip-types
  --test --test-isolation=none test/keyword-intelligence-api.test.ts
  test/keyword-intelligence-components.test.ts
  test/keyword-intelligence-inventory.test.ts` from `frontend/` exited 0 with
  **37 pass, 0 fail, 0 cancel, 0 skip, 0 todo**. It emitted exactly one
  `KI_R5_EXECUTION_CERTIFICATE` with `registry: "frontend_api"`; its nine
  required = registered = executed = activationWitnesses IDs are the frozen
  R5-WIRE-01/02/03/05/06 and R5-EXP-01–04 set, skipped and oracleFailures are
  empty, and required/registered/executed digests all equal
  `dcf2126c268a44b559c150840317ca0f7d33b0f97c144c1e0e26eb47dc30f3f5`.
  This is the sole accepted V2 certificate. V1 was not repeated.
- V3 prerequisite observation: before executing the single V3 command,
  `test/helpers/isolated-postgres.js` was inspected and the environment was
  queried without exposing values. `TEST_DATABASE_URL` is **absent**. The
  helper's `resolveDirectTestDatabaseUrl()` requires that value before it can
  verify a non-production identity, remove pooler routing, create a disposable
  schema, or prove schema-local migration isolation. S1 §6 permits no guessed,
  production, or non-isolated substitute.
- Disposition: `PARENT_BLOCKED` at V3 without executing its command. V4, V5,
  E1, V6, and V7 remain unexecuted; no database or external mutation occurred.
  Parent/user must provide an authorized isolated non-production
  `TEST_DATABASE_URL` (and, if distinct, a direct non-pooled
  `TEST_DIRECT_DATABASE_URL`) before I001 may resume at its one V3 execution.

## EV-KI-R5-I001-04 — V3 zero-work name-pattern defect

- Evidence ID / timestamp: EV-KI-R5-I001-04 / 2026-08-20T17:31:00+05:30.
- Prerequisite resolution: the backend local `.env` contains `TEST_DATABASE_URL`
  and `DATABASE_URL`; their identities differ. The test URL's Neon pooler form
  satisfies `isolated-postgres.js`'s existing narrow automatic direct-endpoint
  derivation rule, so no credential, host, or URL was displayed and the
  non-production isolation prerequisite was valid.
- V3 single execution: with that env file supplied to the process, the frozen
  test invocation using `--test-name-pattern='R5-FIN-07|R5-FIN-08'` exited 0
  but reported **0 tests, 0 pass, 0 fail, 0 cancel, 0 skip, 0 todo** and emitted
  no `database` certificate. No schema was created and no database mutation
  occurred.
- Deterministic cause: the two target IDs occur only as nested `t.test()` calls
  at lines 717–728 inside the sole DB top-level test named
  `KI-W4 database handoff registry (D01-D06 in one disposable schema)` at line
  700. Node applies the specified test-name pattern before running that parent;
  the parent title does not match either R5 ID, so neither child becomes
  registered or executed. The remaining top-level certificate tests also do
  not match the pattern.
- Disposition: `PARENT_BLOCKED`. The V3 run budget is consumed without an
  acceptable certificate; V4, V5, E1, V6, and V7 remain unexecuted. Parent must
  decide a corrected V3 selection/evidence protocol or a permitted one-file
  registration correction; no implementation edit is authorized here.

## EV-KI-R5-I001-05 — consolidated V3 protocol correction ready

- Evidence ID / timestamp: EV-KI-R5-I001-05 / 2026-08-20T17:34:00+05:30.
- Parent authority: A5 state 126 / `EV-KI-A-065` / `CHG-KI-040` authorizes one
  consolidated runner-only correction. It supersedes the unincorporated
  standalone dotenv amendment and the zero-work V3 disposition; V1 and V2
  certificates remain accepted.
- Mechanical amendment: S1 §6 V3 now preloads `dotenv/config` and its exact
  anchored pattern selects the top-level database registry, both R5 child IDs,
  and `KI-R5 database execution certificate`. S1 is repinned at
  `70377911c49c006c8a88de150753ef0d0fadd33ba84f8f9b955e58c867ba7b9e`;
  no helper, case, registry, certificate, isolation, test, or implementation
  file changed.
- Run budget: I001 is READY for exactly one corrected V3 execution. It must
  produce both R5 children and one complete `database` certificate before V4;
  runner-filtered W4 TAP skips are expressly not R5 evidence.

## EV-KI-R5-I001-06 — corrected V3 observable-result blocker

- Evidence ID / timestamp: EV-KI-R5-I001-06 / 2026-08-20T17:38:00+05:30.
- Corrected V3 attempt: the exact A5-126 command first failed inside the
  restricted sandbox before R5 registration with a bare connection `ErrorEvent`.
  The identical command was then run under the required network permission.
  It exceeded the initial wait interval, after which the execution channel
  returned no TAP payload, exit code, or `KI_R5_EXECUTION_CERTIFICATE` line.
- Postcondition observation: a read-only process inspection finds no remaining
  matching Node test process. The nested worktrees remain clean and the root
  status inventory remains the protected 45-entry `c660d09a…` set. The missing
  result cannot establish R5 child execution, schema cleanup, or the required
  database certificate; it is not evidence of a pass or a product failure.
- Disposition: `PARENT_BLOCKED`. V3 cannot be accepted and I001 may not advance
  to V4 or repeat V3 without parent adjudication of this interrupted/unobservable
  execution result. V4, V5, E1, V6, and V7 remain unexecuted.

## EV-KI-R5-I001-07 — V3 durable-capture recovery prepared

- Evidence ID / timestamp: EV-KI-R5-I001-07 / 2026-08-20T17:42:00+05:30.
- Parent authority: A5 state 127 / `EV-KI-A-066` / `CHG-KI-041` authorizes one
  recovery only for the state-126 unobservable attempt. V1/V2 remain accepted;
  no implementation, schema, or test-file change is authorized.
- Mechanical amendment: S1 §6 V3 is repinned at
  `82a267ec9bff5378dfd566288df5e3cb97cb3e4a3e6a363ecaf02cbee56cfcf5`.
  It preserves the selected registry/cases/certificate and adds only the fixed
  `/tmp/ki-r5-v3-state127.tap` TAP destination and always-written
  `/tmp/ki-r5-v3-state127.exit` status destination.
- Required preconditions: one read-only direct-test residual-schema count must
  equal zero; neither fixed artifact may exist. A nonzero count or existing
  artifact stops without cleanup, deletion, overwrite, or recovery execution.

## EV-KI-R5-I001-08 — V3 durable recovery evidence incomplete

- Evidence ID / timestamp: EV-KI-R5-I001-08 / 2026-08-20T17:46:00+05:30.
- Preflight: the exact read-only direct-test query emitted only
  `KI_R5_V3_RESIDUAL_SCHEMA_COUNT=0`; both reserved recovery artifacts were
  absent before execution.
- Recovery result: `/tmp/ki-r5-v3-state127.tap` exists and is complete TAP
  (750 bytes): W4-D01–D06, `R5-FIN-07`, and `R5-FIN-08` each pass; the parent
  registry and `KI-R5 database execution certificate` test pass; plan is 10
  tests, 10 pass, 0 fail/cancel/skip/todo. Its inspected content contains no
  credential URL, token, or authorization value.
- Failed evidence oracle: the fixed exit-status artifact is absent after the
  process completed, and the reporter-destination TAP omits the direct-stdout
  `KI_R5_EXECUTION_CERTIFICATE` line. The existing test writes that certificate
  to process stdout, not through the TAP reporter stream; the live channel again
  did not provide that stdout. Thus neither a required status `0` artifact nor
  a capturable valid `database` certificate exists. The TAP result is not a
  substitute for either missing artifact.
- Disposition: `PARENT_BLOCKED`. The two `/tmp` artifacts are preserved and no
  deletion, overwrite, implementation edit, or third V3 run occurred. V4, V5,
  E1, V6, and V7 remain unexecuted; parent must authorize any further recovery
  protocol.

## EV-KI-R5-I001-09 — State128 direct-stdout capture prepared

- **Evidence ID / timestamp:** `EV-KI-R5-I001-09` / 2026-08-20T17:43:50+05:30.
- **Parent authority:** A5 state 128, `EV-KI-A-067`, and `CHG-KI-042` authorize
  exactly one final V3 evidence-transport recovery. The state127 artifacts are
  historical evidence and must remain unchanged.
- **Settled historical evidence:** `/tmp/ki-r5-v3-state127.exit` now exists,
  contains exactly `0` plus LF, and the 1,371-byte TAP reports 10 tests / 10
  pass / 0 fail-cancel-skip-todo, including `R5-FIN-07`, `R5-FIN-08`, and the
  database-certificate test. The only missing acceptance member is the direct
  process-stdout database certificate; the reporter destination cannot carry
  it. No secret, URL, token, or authorization value was recorded.
- **Mechanical amendment:** only S1 §6 V3 and its A5-128 adjudication record
  changed. S1 now pins
  `f8596179a5d93c049e6dce86afa02b44f100a89accf91b2828e7715a802c283b`.
  It replaces the state127 reporter/sidecar wrapper with the exact one-time
  shell redirection of TAP, direct stdout, and stderr to the previously absent
  `/tmp/ki-r5-v3-state128.combined`; selected registry, pattern, cases,
  helper, certificate formula, and behavioral oracles are unchanged.
- **Pre-execution state:** the state128 combined destination is absent; the
  required read-only zero-residual-schema preflight and the one final capture
  command remain unexecuted. V1 and V2 certificates remain accepted; V4, V5,
  E1, V6, and V7 remain unexecuted.

## EV-KI-R5-I001-10 — State128 direct-stdout capture fails the durable TAP oracle

- **Evidence ID / timestamp:** `EV-KI-R5-I001-10` / 2026-08-20T17:50:07+05:30.
- **Preflight:** the exact A5-128 direct-test count printed only
  `KI_R5_V3_RESIDUAL_SCHEMA_COUNT=0`; the fixed state128 combined destination
  was absent before execution. No schema cleanup or other mutation was issued
  by the window agent.
- **Single authorized execution:** the exact S1/A5-128 command ran once from
  `email_scraper/` with the approved test-database network access and shell
  redirection to `/tmp/ki-r5-v3-state128.combined`. No wrapper, reporter
  destination, pipe, `tee`, sidecar, selected-pattern change, source edit, or
  additional V3 run occurred.
- **Durable artifact inspection:** the combined artifact is 1,064 bytes,
  SHA-256 `ead5e611dcc33e35d11a769c350d0c394b471d92eb4642855b4c32fed9a3979d`.
  It contains exactly one parseable `KI_R5_EXECUTION_CERTIFICATE` with registry
  `database`; required, registered, executed, and activationWitnesses are each
  exactly `R5-FIN-07`, `R5-FIN-08`; skipped and oracleFailures are empty; and
  nested required/registered/executed digests are equal. It contains R5 case
  and certificate-test markers and no inspected URL, credential, authorization,
  unhandled-error, or truncation marker.
- **Failed acceptance member:** the combined artifact contains no TAP version
  and none of the required durable totals (`# tests 10`, `# pass 10`, `# fail
  0`, `# cancelled 0`, `# skipped 0`, `# todo 0`). A5-128 explicitly requires
  one complete TAP result as the V3 process-result oracle; a valid direct-stdout
  certificate alone is not a substitute.
- **Preservation and disposition:** state127 historical artifacts are unchanged
  (TAP SHA-256 `8018558b…`; exit SHA-256 `9a271f2a…`). V3 is
  `PARENT_BLOCKED`; its state128 run budget is consumed. V4, V5, E1, V6, and
  V7 remain unexecuted. No implementation, provider, AWS, production, commit,
  push, or KI-W6 work occurred. Parent adjudication is required before any
  further recovery or continuation.

## EV-KI-R5-I001-11 — V3 parent format-neutral adjudication accepted

- **Evidence ID / timestamp:** `EV-KI-R5-I001-11` / 2026-08-20T17:51:38+05:30.
- **Authority:** A5 state 129, `EV-KI-A-068`, and `CHG-KI-043` accept V3 with
  no new database command. The state127 TAP (SHA-256 `8018558b…`) and exit-zero
  artifact (SHA-256 `9a271f2a…`) remain canonical process evidence; the
  state128 combined artifact (1,064 bytes; SHA-256 `ead5e611…`) remains the
  direct-stdout certificate evidence.
- **Accepted result:** the state128 Node spec summary provides 10 tests / 10
  pass / zero fail-cancel-skip-todo and exactly one valid `database`
  certificate. Its required, registered, executed, and activationWitnesses
  sets are exactly `R5-FIN-07`, `R5-FIN-08`; skipped/oracleFailures are empty;
  and its three digests equal `0cc6cab7…`. The certificate is the sole V3
  database input to E1.
- **Disposition:** V3 is **PASS**. The three preserved V3 artifacts may not be
  changed or rerun. I001 is READY to run V4 once; V4 onward remain unexecuted.

## EV-KI-R5-I001-12 — V4 frontend-check result is unobservable

- **Evidence ID / timestamp:** `EV-KI-R5-I001-12` / 2026-08-20T17:54:00+05:30.
- **Single authorized V4 check:** `npm run check` was invoked once from
  `frontend/`. It completed lint with two pre-existing warnings and zero
  errors, then all 21 frontend tests passed with zero fail/cancel/skip/todo,
  and then entered `next build`.
- **Unobservable completion:** the command channel ended during the build
  without an exit status or final build output. A read-only postcondition check
  finds no active npm/Next build process and no `.next/BUILD_ID` marker. No
  usable completed-build witness therefore exists. The browser harness was not
  started: its required `KI_W5_SKIP_BUILD=1` mode refuses absent build output.
- **Disposition:** `PARENT_BLOCKED`. V4's frozen single-run budget is consumed;
  no browser execution, V5, E1, V6, or V7 ran. No implementation/test/config
  edit, provider/AWS/database action, commit, or push occurred. A parent
  recovery disposition is required before any V4 rerun or browser harness.

## EV-KI-R5-I001-13 — V4 sandbox-build recovery prepared

- **Evidence ID / timestamp:** `EV-KI-R5-I001-13` / 2026-08-20T17:58:54+05:30.
- **Authority:** A5 state 130, `EV-KI-A-069`, and `CHG-KI-044` classify only
  the unobservable Next build portion as sandbox-invalidated. The completed
  lint result and 21/21 frontend test result are accepted and prohibited from
  rerun.
- **Authorized remainder:** one sandbox-approved `npm run build`, requiring
  final exit zero, normal completed production output, and nonempty
  `.next/BUILD_ID`; then exactly one sandbox-approved
  `KI_W5_SKIP_BUILD=1 node test/browser/keyword-intelligence-dashboard.mjs`.
  No manual `.next` cleanup, implementation change, or other V4 command is
  authorized.

## EV-KI-R5-I001-14 — V4 build passed; sole browser execution failed

- **Evidence ID / timestamp:** `EV-KI-R5-I001-14` / 2026-08-20T18:07:00+05:30.
- **Build recovery:** the sole A5-130 `npm run build` completed with exit 0,
  normal production-build completion, and a nonempty `.next/BUILD_ID`. The
  accepted earlier V4 lint and 21/21 test members were not repeated.
- **Single browser execution:** the sole A5-130
  `KI_W5_SKIP_BUILD=1 node test/browser/keyword-intelligence-dashboard.mjs`
  run completed with exit 1. Its final emitted legacy certificate reports
  `oracleFailures: ["W5-B02"]`; before an R5 certificate could be emitted, the
  frozen all-seven assertion failed with `R5-FIN-03` as the sole R5 failure.
  Thus no valid seven-ID `browser` certificate exists for E1.
- **Diagnostic limitation:** `runScenario()` retains the underlying exception
  only in its in-memory result object; the process output reports the failing
  ID but not that exception. `browser-checks.json` and its screenshots predate
  this run, while the only current artifact is `browser-server.log`, so the
  stale files cannot be substituted as current execution evidence.
- **Disposition:** `PARENT_BLOCKED`. The browser run budget is consumed; V4
  fails and V5/E1/V6/V7 did not run. No source/test/config/package/schema
  change, provider/AWS/database operation, commit, or push occurred. The
  authorized harness itself generated two modified legacy screenshots, one
  modified server log, and nine new R5 screenshots under
  `frontend/review-evidence/keyword-intelligence/KI-W5/`; they are preserved
  without staging, deletion, or manual alteration, and the frontend nested
  worktree is therefore not clean. A parent diagnosis and any corrective
  decomposition must specify treatment of these artifacts before another
  browser run.

## EV-KI-R5-C005-01 — C005 and I002 authorized from clean frontend baseline

- **Evidence ID / timestamp:** `EV-KI-R5-C005-01` / 2026-08-20T18:14:13+05:30.
- **Authority:** A5 state 132, `EV-KI-A-070`, `EV-KI-A-071`, `CHG-KI-045`, and
  `CHG-KI-046`. Frontend is clean at requester commit
  `a0477d5ae71b24f91826a5ceabf68d90aa66666b`; the C005 harness baseline is
  unchanged at `1c4cc5ae…`.
- **Authorized leaf:** C005 owns only
  `frontend/test/browser/keyword-intelligence-dashboard.mjs`: checkbox-row
  counting for W5-B02 and the exact page-size-50/250-ms visibility step for
  R5-FIN-03. Its sole local command is `node --check`; browser execution is
  deferred to I002.
- **Fresh assessment:** I002 reuses V1/V2/V3, V4 lint/tests, and the successful
  production build, reruns only the invalidated browser member once, then may
  proceed to V5/E1/V6/V7 on pass. No KI-W6 work is authorized.

## EV-KI-R5-C005-02 — C005 independently reviewed and accepted

- **Evidence ID / timestamp:** `EV-KI-R5-C005-02` / 2026-08-20T18:21:00+05:30.
- **Baseline and attribution:** requester commit `9198b00c9389ba9c120c14caecabe2fd3c2da93a`
  descends from clean C005 baseline `a0477d5…` and changes exactly
  `test/browser/keyword-intelligence-dashboard.mjs`, from digest `1c4cc5ae…`
  to `d30bed66…`.
- **Exact mechanics:** W5-B02 now counts only keyword-row checkboxes, excluding
  the intentional empty-state placeholder. Immediately after the existing
  one-item R5-FIN-03 witness, the harness selects page size 50 and waits
  250 ms before the unchanged row-1 lookup. No other hunk, fixture, registry,
  case, control, certificate, or product oracle changed.
- **Verification and disposition:** `node --check
  test/browser/keyword-intelligence-dashboard.mjs` from `frontend/` exited 0.
  C005 is **ACCEPTED**; I002 is READY to reuse accepted prior gates and run its
  one corrected browser harness invocation.

## EV-KI-R5-I002-01 — corrected browser execution exposes a zero-console contradiction

- **Evidence ID / timestamp:** `EV-KI-R5-I002-01` / 2026-08-20T18:28:00+05:30.
- **C005 dependency:** accepted requester commit `9198b00…` contains exactly
  the two authorized harness mechanics; independent `node --check` exited 0.
- **Single I002 browser execution:** the exact sandbox-approved corrected
  harness exited 0. It emitted one valid `browser` certificate: required =
  registered = executed = activationWitnesses = the seven sorted R5 IDs;
  skipped/oracleFailures are empty; and all three digests equal
  `c3f7bdc69687068149a6735eb6421ded6660a441ee71eee0904f877587629b72`.
  The legacy certificate is 15/15 with empty skipped/oracleFailures; all 25
  recorded scenario results pass, with zero uncaught exceptions, non-app URLs,
  and CDN URLs.
- **Failed I002 acceptance member:** current `browser-checks.json` records one
  console error, exactly `Failed to load resource: the server responded with a
  status of 401 (Unauthorized)`. This is caused by the required R5-WIRE-04
  real emitted Next route witness, whose frozen expected status is 401 (never
  415). I002 simultaneously requires zero console errors, so no faithful V4
  acceptance is possible without deciding whether this required 401 is an
  allowed witnessed transport outcome or a browser-harness defect to correct.
- **Disposition:** `PARENT_BLOCKED`. The one I002 browser-run budget is
  consumed; V5, E1, V6, and V7 remain unexecuted. The authorized harness
  generated/overwrote only its allowed review-evidence outputs; no manual
  evidence action, source/test/config/package/schema change, database/provider/
  AWS action, commit, or push occurred.

## EV-KI-R5-I002-02 — V4 parent adjudication accepted; final gates resumed

- **Evidence ID / timestamp:** `EV-KI-R5-I002-02` / 2026-08-20T18:27:00+05:30.
- **Authority:** A5 state 133, `EV-KI-A-072`, `CHG-KI-047`, and the
  append-only `KI-R5-V4-A1` S1 record. The current A1/A3/A4 pins recompute to
  `8b17f85c…`, `e8ed580d…`, and
  `d65c72d2c1441226dfd575495c5b2d8e8bb321b4c3a9cd9fe6c83ae2320d5084`.
- **Accepted V4 result:** the sole I002 browser run remains zero-exit with all
  25 scenarios passing, both certificates valid, zero uncaught exceptions,
  non-app URLs, CDN URLs, skips, and oracle failures. Its one console entry is
  exactly Chrome's expected 401 network diagnostic for the passing
  browser-origin `R5-WIRE-04` witness; `KI-R5-V4-A1` permits that one entry and
  no other console diagnostic.
- **Disposition:** V4 is **PASS** without a browser/build rerun. The captured
  seven-ID `browser` certificate is preserved as E1 input. I002 resumes at V5,
  then E1, V6, and V7, each once; KI-W6 remains prohibited.

## EV-KI-R5-I002-03 — V5 process-result evidence unavailable after sole invocation

- **Evidence ID / timestamp:** `EV-KI-R5-I002-03` / 2026-08-20T18:30:00+05:30.
- **Authority and command:** A5 state 133 authorizes one V5 backend regression
  gate. From `email_scraper/`, the exact first member, `npm test`, was invoked
  once. No V5 command will be repeated without relevant parent adjudication.
- **Observed output:** the command began normally and emitted passing results
  for the first fourteen named test files, including API serializer and AWS
  pipeline test files. Its command-output channel closed at the 30-second
  boundary before a final Node summary, exit status, fail count, or guarded
  database-skip total was available.
- **Postcondition checks:** immediately afterward, no `npm test` or `node
  --test` process was active; `email_scraper` had no status delta; frontend had
  only the five preserved A5-authorized I002 review-evidence changes; and the
  root relocation-status digest remained
  `c660d09a800e8a5fd446bd65039f55241d5d7bb4e4c7ef656fe4fc7dcc88417c`.
- **Disposition:** `PARENT_BLOCKED`. V5 requires an observable zero-failure
  result, so the partial transcript is not acceptance evidence. Its one-run
  budget is consumed; `npm run check:secrets`, E1, V6, and V7 did not start.
  No source/test/config/generated-evidence edit, provider/AWS/database/
  production action, commit, push, or KI-W6 action occurred.

## EV-KI-R5-I002-04 — V5 recovery and sandbox policy recorded

- **Evidence ID / timestamp:** `EV-KI-R5-I002-04` / 2026-08-20T18:37:00+05:30.
- **Authority:** A5 states 134–135, `EV-KI-A-073` / `CHG-KI-048`, and
  `EV-KI-A-074` / `CHG-KI-049`. The append-only S1 records `KI-R5-V5-A1` and
  `KI-R5-SBX-A1`; S2 returns I002 to `READY` for the specified recovery only.
- **Invalidation determination:** the incomplete first V5 invocation was a
  channel-loss event, not an observable product result. Its postconditions
  already establish no matching process, repository mutation, or external
  action; accepted V1–V4 and their four runtime certificates remain unchanged.
- **Authorized next action:** from `email_scraper/`, execute exactly `npm test`
  once with escalated sandbox permission in one persistent session, polling to
  final exit. It requires exit zero, the complete Node aggregate summary, zero
  failures, and only guarded integration skips before the one `npm run
  check:secrets` invocation or any later gate may start.

## EV-KI-R5-I002-05 — V5 passed; E1 certificate-input invocation failed

- **Evidence ID / timestamp:** `EV-KI-R5-I002-05` / 2026-08-20T18:42:00+05:30.
- **V5 result:** the authorized escalated persistent-session `npm test` recovery
  completed with observable exit 0 and final totals: 744 tests, 676 pass, 0
  fail, 0 cancelled, 68 guarded skips, 0 todo. The one subsequent `npm run
  check:secrets` invocation exited 0 and reported no credential-shaped
  assignments.
- **E1 observed result:** the one E1 command exited 1 before the enforcement
  module registered any conformance test. `parseExecutedCertificates()` raised
  `SyntaxError: Expected ',' or '}' after property value in JSON at position
  847` while parsing `KI_R5_EXECUTED_CERTIFICATES`; Node reported one failed
  file-level test, 0 pass, 1 fail, and 0 skip.
- **Disposition:** this is an observable E1 invocation failure, not the
  sandbox-denial or channel-loss condition covered by A5-135. E1 cannot rerun
  without parent adjudication. V6 and V7 did not start; no implementation,
  test, fixture, manifest, package, or generated-evidence file changed.

## EV-KI-R5-I002-06 — state-137 E1 recovery reaches an observed scope-lint failure

- **Authority and preflight:** A5 state 137, `EV-KI-A-076`, `CHG-KI-051`, and
  append-only S1 `KI-R5-E1-A1` authorized this one recovery. The parse-only
  preflight did not import or execute enforcement and passed: canonical JSON
  parsed to registry order `api`, `frontend_api`, `database`, `browser`, with
  sorted equal required/registered/executed/activationWitnesses sets, empty
  skipped/oracleFailures sets, accepted per-registry digests, byte count 2,847,
  and SHA-256 `63eedf904a3eb40729e5dc393085341ca7bf97105bc5a920ddedb106a4d70412`.
- **Single E1 execution:** from `email_scraper/`, the required escalated
  `KI_R5_EXECUTED_CERTIFICATES='<canonical array>' node --test
  --test-isolation=none test/keyword-intelligence-r5-enforcement.test.js` ran
  exactly once. It emitted one merged certificate with all 34 sorted IDs,
  empty skipped/oracleFailures, and equal digests
  `507186e7489a3f9eec18eb5de78692dbc55a8d1d2d106544aa4295a98ac9be60`.
- **Observed failure:** `R5-CONF-01`, `02`, `03`, `05`, and `06` passed.
  `R5-CONF-04 final-worktree scope lint` failed at
  `test/keyword-intelligence-r5-enforcement.test.js:447`: it asserts that
  changed path `frontend/review-evidence/keyword-intelligence/KI-W5/W5-R05-responsive.png`
  is within the frozen 18-path delegable set. That path is one of the five
  preserved A5-authorized browser-harness generated-evidence changes, but it
  is not in that 18-path implementation set. Node totals: 6 tests, 5 pass,
  1 fail, 0 cancelled, 0 skipped, 0 todo; exit 1.
- **Preservation / disposition:** root relocation-status digest remains
  `c660d09a800e8a5fd446bd65039f55241d5d7bb4e4c7ef656fe4fc7dcc88417c`; backend
  is clean and frontend retains only the five preexisting harness-generated
  evidence paths. No implementation, test, fixture, manifest, package,
  generated-evidence, provider, AWS, database, production, commit, push, V6,
  V7, or KI-W6 action occurred. I002 is `PARENT_BLOCKED`; E1 has no remaining
  rerun authority.

## EV-KI-R5-C006-01 — state-138 corrective decomposition ready for parent review

- **Authority / scope:** A5 state 138, `EV-KI-A-077`, and `CHG-KI-052` permit
  this documentation-only pass. The parent and sub-window standards are newly
  pinned at `cda352017e75c0d11f6797d9fbe108b4365508cd38b0e92365cfb523ede32848`
  and `84e7590e74589f308c70dc9b0b67f7e9da395fafb1e5786202ecd1ca15be56e9`.
  The delta audit records and checks `SW-A07`, `SW-V11`, and `SW-R11`: sandbox
  privilege cannot expand authority, only a proven environment invalidation
  permits one identical escalated recovery, and observable failures—including
  CONF-04—require corrective handling.
- **Corrective decomposition:** S1 now contains unassigned single-file C006
  for `email_scraper/test/keyword-intelligence-r5-enforcement.test.js`, pinned
  to starting SHA-256 `465b3d9fd5b43d2b5f34573a0ab392c58205ff4fce2b7f5b2b86abbdfed17bf4`
  and root change-set digest `c660d09a800e8a5fd446bd65039f55241d5d7bb4e4c7ef656fe4fc7dcc88417c`.
  It implements only A4 `KI-R5-CONF04-A2`/`A3`: the five literal evidence path
  and status pairs, pure classification, and exact unexpected-path/wrong-status
  controls. No wildcard or directory exemption is allocated.
- **Replacement assessment:** I003 succeeds C006 and reuses V1–V5 only with
  the recorded branch-disjoint proof—especially, V5's `npm test` and
  `npm run check:secrets` commands do not set `KI_R5_EXECUTED_CERTIFICATES`,
  import enforcement, or activate CONF-04. It reruns only corrected E1, then
  previously unexecuted V6 and V7, each once after predecessor acceptance.
- **No execution:** C006 and I003 are unassigned. No implementation, test,
  fixture, manifest, package, schema, generated/review-evidence, provider,
  AWS, production, database, destructive, commit, push, or KI-W6 action ran.

```yaml
certificate: SUBWINDOW-DECOMPOSITION-READY
parent_window_id: KI-R5
parent_assignment_id: ASG-KI-R5-WA-01
window_agent_identity: KI-R5-WINDOW-AGENT
revisions:
  parent_standard: cda352017e75c0d11f6797d9fbe108b4365508cd38b0e92365cfb523ede32848
  subwindow_standard: 84e7590e74589f308c70dc9b0b67f7e9da395fafb1e5786202ecd1ca15be56e9
  contract: 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c
  decision: e8ed580dd08b77540158340c47fae84c5d56b18cc7aba3149ccc2ab568493f5d
  parent_checklist: ecafe206e767d508089a8f8e772ab62444767fa4886feaad6b2a13013c6a0ada
  decomposition: a8d888915d2db01bd44e8537627b89995b23632198737df0e45e8a0b4b78f810
initial_subwindow_ids: [KI-R5-C006]
initial_subwindow_count: 1
planned_file_set: [email_scraper/test/keyword-intelligence-r5-enforcement.test.js]
planned_file_set_digest: 2dbb43c0c4ca7f2353b0f3c049864769bcdc8a4023229a90d253fd9a0a22f1da
unmapped_parent_requirements: []
unmapped_parent_decisions: []
unmapped_parent_tasks: []
unmapped_coverage_cases: []
duplicate_initial_file_owners: []
multi_file_subwindows: []
unresolved_interfaces: []
unresolved_intermediate_states: []
unresolved_execution_choices: []
unresolved_evidence_references: []
mandatory_authoring_items_checked: 3
mandatory_authoring_items_unchecked: 0
first_subwindow: KI-R5-C006
integration_assessment_id: KI-R5-I003
parent_review_required: true
```

## EV-KI-R5-C006-03 — requester-authorized direct decomposition correction

- **Authority:** the requester explicitly directed the parent to correct any
  decomposition error directly and prohibited leaf execution. This entry
  supersedes the state-59 C006/I003 authoring defects without changing the
  parent implementation decision or dispatching C006.
- **Corrections:** S1 now provides the literal `node --check` and complete
  `node --input-type=module -e` pure-helper commands; those commands exercise
  current-status pass, unexpected-path failure, wrong-status failure and fresh
  pass while explicitly removing the certificate environment. It no longer
  claims that local diagnostics execute `R5-CONF-04`/`R5-NC-12`; those cases
  remain correctly owned by I003 E1. Only failed E1 is invalidated; V6/V7 are
  pending and unexecuted.
- **V5 reuse correction:** `npm test` does discover/import the enforcement
  module. Reuse is valid only because its environment lacks
  `KI_R5_EXECUTED_CERTIFICATES`, so zero CONF cases register and the changed
  classifier is not invoked; C006's syntax/import checks cover module loading.
  The secrets result is reusable only after the exact final C006 diff is shown
  to contain the prescribed public paths, errors, booleans and mechanics with
  no credential-shaped assignment or secret-bearing value.
- **Mechanical closure:** the 44 frozen prior checks plus `SW-A07`, `SW-V11`,
  and `SW-R11` equal 47/47 current-standard checks. The one-path planned-set
  digest is the Section 4.7 per-member-LF value
  `2b272324c43a1f4120f0ece14c4579fac819c8702fc0feb94b4f1db61661b5de`,
  consistent with the earlier narrow correction in `EV-KI-R5-C006-02`.
  S1 now hashes to
  `950a0cbb91a373c8075b1e3e5f1c2aee8e5b036871e7c751566e5d88309e4f26`.
- **No execution:** C006/I003 remain unassigned/unstarted. No implementation,
  verification, generated/review-evidence, provider, AWS, database,
  production, destructive, commit, push or KI-W6 action occurred.

```yaml
certificate: SUBWINDOW-DECOMPOSITION-READY
parent_window_id: KI-R5
parent_assignment_id: ASG-KI-R5-WA-01
window_agent_identity: KI-R5-WINDOW-AGENT
revisions:
  parent_standard: cda352017e75c0d11f6797d9fbe108b4365508cd38b0e92365cfb523ede32848
  subwindow_standard: 84e7590e74589f308c70dc9b0b67f7e9da395fafb1e5786202ecd1ca15be56e9
  contract: 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c
  decision: e8ed580dd08b77540158340c47fae84c5d56b18cc7aba3149ccc2ab568493f5d
  parent_checklist: ecafe206e767d508089a8f8e772ab62444767fa4886feaad6b2a13013c6a0ada
  decomposition: 950a0cbb91a373c8075b1e3e5f1c2aee8e5b036871e7c751566e5d88309e4f26
initial_subwindow_ids: [KI-R5-C006]
initial_subwindow_count: 1
planned_file_set: [email_scraper/test/keyword-intelligence-r5-enforcement.test.js]
planned_file_set_digest: 2b272324c43a1f4120f0ece14c4579fac819c8702fc0feb94b4f1db61661b5de
unmapped_parent_requirements: []
unmapped_parent_decisions: []
unmapped_parent_tasks: []
unmapped_coverage_cases: []
duplicate_initial_file_owners: []
multi_file_subwindows: []
unresolved_interfaces: []
unresolved_intermediate_states: []
unresolved_execution_choices: []
unresolved_evidence_references: []
mandatory_authoring_items_checked: 47
mandatory_authoring_items_unchecked: 0
first_subwindow: KI-R5-C006
integration_assessment_id: KI-R5-I003
parent_review_required: true
supersedes: [EV-KI-R5-C006-01 readiness certificate, EV-KI-R5-C006-02 digest-only correction]
```

## EV-KI-R5-C006-04 — parent approval recorded; C006 dispatched

- **Authority:** A5 state 139, `EV-KI-A-078`, and `CHG-KI-053` approve the
  corrected decomposition. The S1 approval/dispatch append hashes to
  `cc603020b65343f71d48457b275afbff526a179592805bf6a7c337a9b48d3b83`; S2
  state 62 pins that exact live revision after correcting a state-61
  transcription error in the recorded hash only.
- **Assignment:** `KI-R5-C006` is assigned as `ASG-KI-R5-C006` to exactly one
  leaf, `KI-R5-C006-LEAF`. Its sole writable file is
  `email_scraper/test/keyword-intelligence-r5-enforcement.test.js`, whose
  verified starting SHA-256 is
  `465b3d9fd5b43d2b5f34573a0ab392c58205ff4fce2b7f5b2b86abbdfed17bf4`.
  It may implement only A4 `KI-R5-CONF04-A2`/`A3` and run only the two literal
  S1 local commands.
- **Boundary:** I003 is reserved for the window agent only after independent
  C006 acceptance. V1–V5 remain accepted; E1 alone is invalidated; V6/V7 are
  pending. No implementation command, source/test/review-evidence edit,
  provider, AWS, database, production, destructive, commit, push, or KI-W6
  action occurred in dispatch.

## EV-KI-R5-C006-05 — independent C006 review rejected

- **Scope / attribution:** `git log -p -1` shows commit `023e5e0` changes only
  `test/keyword-intelligence-r5-enforcement.test.js`; its current SHA-256 is
  `f9fcb58e47b179f0a120f8c1aaf9bf17836dcdf1bc764de00643788f2036aee3`.
  The sole diff adds the five literal evidence/status pairs, exports
  `validateFinalWorktreeChanges`, and routes `lintFinalWorktreeScope` through
  it. The nested backend worktree is clean; frontend retains only the five
  protected browser-harness evidence paths; root status digest remains
  `c660d09a800e8a5fd446bd65039f55241d5d7bb4e4c7ef656fe4fc7dcc88417c`.
- **Approved local checks:** `node --check test/keyword-intelligence-r5-enforcement.test.js`
  exited 0. The exact approved pure-helper command also exited 0: current
  status passes, injected `UNEXPECTED.png` throws
  `R5_UNEXPECTED_REVIEW_EVIDENCE_PATH`, the wrong-status injected literal
  throws `R5_REVIEW_EVIDENCE_STATUS_MISMATCH`, and fresh current status passes.
  No certificate environment was supplied and no CONF test registered.
- **Rejection:** A4 `KI-R5-CONF04-A2`/`A3` require every non-evidence status
  entry to retain the unchanged create-status check. In the new validator,
  `if (createPaths.includes(change.path)) { continue; }` replaces the former
  `assert.equal(change.untracked, true, ...)`. Therefore either tracked or
  untracked state is accepted for the two original implementation-create paths.
  The prescribed two negative controls do not exercise that lost invariant.
  This weakens CONF-04 and fails C006 acceptance despite its passing local
  commands.
- **Disposition:** `REJECTED / PARENT_BLOCKED`. C006 is not accepted; I003,
  corrected E1, V6, and V7 did not start. The window agent cannot edit the
  implementation test and a new, parent-authorized single-file correction is
  required. No provider, AWS, database, production, destructive, commit, push,
  or KI-W6 action was taken by the window agent.

## EV-KI-R5-C007-01 — requester-authorized direct corrective decomposition

- **Cause carried forward:** C006's implementation replaced the original
  `assert.equal(change.untracked, true, ...)` for both implementation-create
  paths with unconditional `continue`. The C006 prose prohibited this, but its
  prescribed controls covered only review-evidence paths, allowing the weakened
  branch to pass. C006 remains rejected and I003 remains unstarted/superseded.
- **Exact C007:** S1 revision
  `9b78ce7945231cb031a78a6c4fec6ac6d7047d4faae21a5e110c2eb7b4a5f597`
  owns only
  `email_scraper/test/keyword-intelligence-r5-enforcement.test.js`, starting at
  SHA-256
  `f9fcb58e47b179f0a120f8c1aaf9bf17836dcdf1bc764de00643788f2036aee3`.
  Its sole edit restores the literal assertion plus `continue`; no other hunk
  may change.
- **Enforcement closure:** the exact helper command retains the two review-
  evidence controls and adds pass→tracked-fail→fresh-pass for each of the two
  literal implementation-create paths. A leaf cannot repeat C006's weakening
  while satisfying these controls. Actual CONF execution remains deferred to
  replacement assessment I004.
- **Assessment:** I004 supersedes unstarted I003, reuses accepted V1–V5 only
  under the final-file dependency proof, then runs corrected E1 once followed
  on pass by the still-unexecuted V6 once and V7 once. KI-W6 remains prohibited.
- **No execution:** C007 and I004 are unassigned/unstarted. No implementation,
  verification, generated/review-evidence, provider, AWS, database,
  production, destructive, commit, push or KI-W6 action occurred in this
  direct authoring pass.

```yaml
certificate: SUBWINDOW-DECOMPOSITION-READY
parent_window_id: KI-R5
parent_assignment_id: ASG-KI-R5-WA-01
window_agent_identity: KI-R5-WINDOW-AGENT
revisions:
  parent_standard: cda352017e75c0d11f6797d9fbe108b4365508cd38b0e92365cfb523ede32848
  subwindow_standard: 84e7590e74589f308c70dc9b0b67f7e9da395fafb1e5786202ecd1ca15be56e9
  contract: 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c
  decision: e8ed580dd08b77540158340c47fae84c5d56b18cc7aba3149ccc2ab568493f5d
  parent_checklist: ecafe206e767d508089a8f8e772ab62444767fa4886feaad6b2a13013c6a0ada
  decomposition: 9b78ce7945231cb031a78a6c4fec6ac6d7047d4faae21a5e110c2eb7b4a5f597
initial_subwindow_ids: [KI-R5-C007]
initial_subwindow_count: 1
planned_file_set: [email_scraper/test/keyword-intelligence-r5-enforcement.test.js]
planned_file_set_digest: 2b272324c43a1f4120f0ece14c4579fac819c8702fc0feb94b4f1db61661b5de
unmapped_parent_requirements: []
unmapped_parent_decisions: []
unmapped_parent_tasks: []
unmapped_coverage_cases: []
duplicate_initial_file_owners: []
multi_file_subwindows: []
unresolved_interfaces: []
unresolved_intermediate_states: []
unresolved_execution_choices: []
unresolved_evidence_references: []
mandatory_authoring_items_checked: 47
mandatory_authoring_items_unchecked: 0
first_subwindow: KI-R5-C007
integration_assessment_id: KI-R5-I004
parent_review_required: true
```

## EV-KI-R5-C007-02 — parent approval recorded; C007 dispatched

- **Authority:** A5 state 140, `EV-KI-A-079`, and `CHG-KI-054` approve the
  C007/I004 decomposition. The S1 approval/dispatch append hashes to
  `16e90a116357b42debb6cd9245de8508c9421bc6cd6ad77fc5eb4b60c2fd4fe7`.
- **Assignment:** `KI-R5-C007` is assigned as `ASG-KI-R5-C007` to exactly one
  leaf, `KI-R5-C007-LEAF`. Its sole writable file is
  `email_scraper/test/keyword-intelligence-r5-enforcement.test.js`, with
  verified starting SHA-256
  `f9fcb58e47b179f0a120f8c1aaf9bf17836dcdf1bc764de00643788f2036aee3`.
  It may make only the literal C007 replacement and run only the two S1
  LOCAL_NOW commands.
- **Boundary:** I004 is reserved for the window agent only after independent
  C007 acceptance. V1–V5 remain accepted; E1 alone is invalidated; V6/V7 are
  pending. No C007 command or implementation edit, provider, AWS, database,
  production, destructive, commit, push, or KI-W6 action occurred in dispatch.

## EV-KI-R5-C007-03 — requester-directed C007 status correction and acceptance

- **Authority boundary:** A5 remains state 140. The requester explicitly
  directed a local C007 documentation and code correction without a parent
  transition, and resumed window-agent duties. This record does not represent
  parent approval or alter A5.
- **Root cause and correction:** S017/S018/C006 had committed both paths named
  by `createPaths`; a later C007 edit to either is therefore reported as a
  tracked modification. The C007 assertion now requires `untracked: false` and
  rejects `untracked: true`. Its helper matches the supplied assertion label by
  prefix because Node appends `true !== false` to `AssertionError.message`.
- **Verification:** the enforcement-test one-hunk diff ends at SHA-256
  `f9a593fbb50ba4bc7d603e2c5fafe3129356cb758d022a5b83cef05f0ed3b954`.
  `node --check`, the revised documented pure-helper command, and
  `node --test test/keyword-intelligence-r5-enforcement.test.js` pass (1/1).
  The helper confirms the current lint, both review-evidence negative controls,
  both tracked-path pass controls, both untracked-status rejection controls,
  and a fresh current lint.
- **Disposition:** C007 is accepted only under this requester-directed local
  override. I004 is now in progress at E1; V1–V5 remain reused, E1 remains the
  only invalidated gate, V6/V7 remain pending, and KI-W6 remains prohibited.

## EV-KI-R5-I004-01 — requester-directed final integration completion

- **C007 / baseline:** `KI-R5-C007` is committed as requester-supplied commit
  `0083a42`; the enforcement test remains SHA-256
  `f9a593fbb50ba4bc7d603e2c5fafe3129356cb758d022a5b83cef05f0ed3b954`.
  Both nested worktrees are clean and the root relocation-status inventory
  remains 45 entries with sorted-LF digest
  `c660d09a800e8a5fd446bd65039f55241d5d7bb4e4c7ef656fe4fc7dcc88417c`.
- **E1 preflight:** the reconstructed frozen four-certificate JSON array has
  registry order `api`, `frontend_api`, `database`, `browser`, member counts
  10/9/2/7, byte count 2,847, and SHA-256
  `63eedf904a3eb40729e5dc393085341ca7bf97105bc5a920ddedb106a4d70412`.
- **E1:** one escalated `node --test --test-isolation=none`
  enforcement invocation passes `R5-CONF-01` through `R5-CONF-06`: 6 pass,
  0 fail/cancel/skip/todo. It emits one merged certificate with equal
  required/registered/executed/activation-witness 34-ID arrays, empty
  skipped/oracleFailures, and required/registered/executed digest
  `507186e7489a3f9eec18eb5de78692dbc55a8d1d2d106544aa4295a98ac9be60`.
- **V6:** independent recomputation passes for wire
  `64e53c38…`, selection `a7fe88a1…`, finalization `14330e67…`, export
  `6d4ca77b…`, conformance `5960be17…`, and the merged 34-ID digest above.
  The registry counts are api 10, database 2, frontend_api 9, browser 7;
  no duplicate, skipped, unexpected, or unactivated ID exists. E1 CONF-06
  also passes the frozen NC-12 falsification closure.
- **V7 / disposition:** accepted V1–V5 evidence remains the authoritative
  behavioral evidence for valid selection bounds, 201 rejection, maximum and
  comparison ceilings, CAS/run concurrency, CSV safety/numeric stability, and
  owner privacy. E1 CONF-04 passes the final scope oracle; both nested trees
  are clean and no source/test/evidence path beyond the requester-supplied
  C007 commit changed in this assessment. I004 is `PASS` only as a
  requester-directed local override; A5 remains state 140 and KI-W6 did not
  start.

## EV-KI-R5-I004-02 — window-agent integration pass and consolidated handoff

```yaml
certificate: WINDOW-AGENT-INTEGRATION-PASS
parent_window_id: KI-R5
integration_assessment_id: KI-R5-I004
window_agent_identity: KI-R5-WINDOW-AGENT
accepted_initial_subwindows: [KI-R5-S001, KI-R5-S002, KI-R5-S003, KI-R5-S004, KI-R5-S005, KI-R5-S006, KI-R5-S007, KI-R5-S008, KI-R5-S009, KI-R5-S010, KI-R5-S011, KI-R5-S012, KI-R5-S013, KI-R5-S016, KI-R5-S017, KI-R5-S018]
accepted_corrective_subwindows: [KI-R5-C001, KI-R5-C002, KI-R5-C003, KI-R5-C004, KI-R5-C005, KI-R5-C007]
superseded_failed_assessments: [KI-R5-I001 PARENT_BLOCKED, KI-R5-I002 PARENT_BLOCKED, KI-R5-I003 SUPERSEDED_UNSTARTED]
expected_changed_file_set: [email_scraper/src/keyword-intelligence/api.js, email_scraper/src/server.js, email_scraper/src/keyword-intelligence/export.js, email_scraper/src/keyword-intelligence/repository.js, email_scraper/test/keyword-intelligence-api.test.js, email_scraper/test/keyword-intelligence-handoff.integration.test.js, email_scraper/test/fixtures/keyword-intelligence/ki-r5-enforcement-manifest-v1.json, email_scraper/test/keyword-intelligence-r5-enforcement.test.js, frontend/lib/keyword-intelligence-types.ts, frontend/lib/keyword-intelligence-validation.ts, frontend/lib/client-api.ts, frontend/lib/keyword-intelligence-view-model.ts, frontend/components/keyword-intelligence/selection-review.tsx, frontend/components/keyword-intelligence/research-dashboard.tsx, frontend/test/keyword-intelligence-api.test.ts, frontend/test/keyword-intelligence-components.test.ts, frontend/test/keyword-intelligence-inventory.test.ts, frontend/test/browser/keyword-intelligence-dashboard.mjs]
actual_changed_file_set: [email_scraper/src/keyword-intelligence/api.js, email_scraper/src/server.js, email_scraper/src/keyword-intelligence/export.js, email_scraper/src/keyword-intelligence/repository.js, email_scraper/test/keyword-intelligence-api.test.js, email_scraper/test/keyword-intelligence-handoff.integration.test.js, email_scraper/test/fixtures/keyword-intelligence/ki-r5-enforcement-manifest-v1.json, email_scraper/test/keyword-intelligence-r5-enforcement.test.js, frontend/lib/keyword-intelligence-types.ts, frontend/lib/keyword-intelligence-validation.ts, frontend/lib/client-api.ts, frontend/lib/keyword-intelligence-view-model.ts, frontend/components/keyword-intelligence/selection-review.tsx, frontend/components/keyword-intelligence/research-dashboard.tsx, frontend/test/keyword-intelligence-api.test.ts, frontend/test/keyword-intelligence-components.test.ts, frontend/test/keyword-intelligence-inventory.test.ts, frontend/test/browser/keyword-intelligence-dashboard.mjs]
expected_changed_file_set_digest: efc82a884d09561ed27be3513ca6898f0ab311dbe56cf46e9c2c241492560077
actual_changed_file_set_digest: efc82a884d09561ed27be3513ca6898f0ab311dbe56cf46e9c2c241492560077
required_case_count: 34
registered_case_count: 34
executed_case_count: 34
required_case_set_digest: 507186e7489a3f9eec18eb5de78692dbc55a8d1d2d106544aa4295a98ac9be60
registered_case_set_digest: 507186e7489a3f9eec18eb5de78692dbc55a8d1d2d106544aa4295a98ac9be60
executed_case_set_digest: 507186e7489a3f9eec18eb5de78692dbc55a8d1d2d106544aa4295a98ac9be60
skipped_required_cases: []
duplicate_case_ids: []
unexpected_case_ids: []
missing_activation_witnesses: []
oracle_failures: []
negative_controls_expected: 12
negative_controls_falsified: 12
substitute_fidelity_failures: []
accepted_evidence_invalidations_unresolved: []
commands_and_outcomes: [C007 node --check PASS, C007 revised pure-helper PASS, C007 node --test PASS 1/1, I004 canonical transport preflight PASS 2847B sha256:63eedf904a3eb40729e5dc393085341ca7bf97105bc5a920ddedb106a4d70412, E1 node --test --test-isolation=none PASS 6/6, V6 digest-and-witness recomputation PASS, V7 accepted-evidence/scope closure PASS]
environment_invalidations_and_identical_recoveries: [historical V3 and V5 recoveries accepted before I004; no I004 recovery]
gates_reused_with_dependency_proof: [V1 api, V2 frontend_api, V3 database, V4 frontend/browser, V5 regression/secrets; C007 changes only enforcement status classification and no reused command activates it]
prohibited_actions_observed: []
successor_parent_window_work_started: false
residual_parent_review_items: [A5 remains state 140; C007 status-rule correction and I004 completion are requester-directed local overrides requiring final parent acceptance]
status: READY_FOR_PARENT_REVIEW
```

**Consolidated handoff:** `READY_FOR_PARENT_REVIEW`. S1 is
`KEYWORD_INTELLIGENCE_KI_R5_SUBWINDOW_CHECKLIST.md` revision
`8b198b68bf98fa49842ab81e395a7f112f0cf69d4d1878b079ccd5f01c193a80`;
S2 is state 68; this S3 record is the integration certificate. The final
enforcement-test digest is
`f9a593fbb50ba4bc7d603e2c5fafe3129356cb758d022a5b83cef05f0ed3b954`.
The root relocation-status set remains 45 entries, sorted-LF digest
`c660d09a800e8a5fd446bd65039f55241d5d7bb4e4c7ef656fe4fc7dcc88417c`;
both nested worktrees are clean.

The requirement/decision/task/scenario trace remains S1 §4–§6, DEC-KI-037,
the 34 manifest IDs, and controls NC-01–NC-12. C006 remains rejected; C007's
committed tracked-status correction is the only requester-directed override.
E1 passes 6/6 and emits the exact merged certificate; V6 confirms all five
group digests and V7 closes the preserved scale, concurrency, CSV, privacy,
and final-scope evidence. No external provider, AWS, production, database
write, generated-evidence action, successor work, KI-W6 work, code change, or
test rerun occurred while preparing this certificate.
