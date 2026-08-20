# KI-W6 Sub-Window Evidence (`S3`)

Append-only evidence for `KI-W6` under assignment `ASG-KI-W6-WA-01`. Entries
never amend a task, decision, or authority boundary. Actor identities:
`KI-W6-WINDOW-AGENT` (this window's coordinator), `KI-W6-S001-AGENT` /
`KI-W6-S002-AGENT` (leaf implementation agents), `KI-W6-WINDOW-AGENT`
(integration assessments).

---

## `EV-KI-W6-S01` — Decomposition authoring and entry-gate verification

- **Timestamp:** 2026-08-20T09:42:00+05:30
- **Parent window / assignment:** `KI-W6` / `ASG-KI-W6-WA-01` (A5 state 108;
  `EV-KI-A-047`, `CHG-KI-024`)
- **Actor/role:** `KI-W6-WINDOW-AGENT` (decomposition author)
- **Entry-gate verification (sub-window standard §3; KI-W6-P1/P3 basis):**
  1. Assignment current and names this window agent (A5 state 108 verified
     on disk this session; requester direction recorded in `EV-KI-A-047`).
  2. Delegation authorized (`authorized_actions` includes per-leaf
     delegation; one leaf at a time).
  3. All five revision pins recomputed and byte-equal (parent standard
     `3b7a4fd2…`, sub-window standard `1766f910…`, contract `8b17f85c…`,
     decision ledger `c2dc635e…`, checklist `324667cb…`).
  4. Parent window `READY` for decomposition (A5 `current_status: READY`,
     window `KI-W6`).
  5. Exact scopes known and copied unexpanded (S1 §1).
  6. Every implementation-affecting decision exists: `SCN-KI-018`, T1
     items 1–15, `DEC-KI-024` counters, D2/D2A/D3/D9–D13 all read and
     allocated; the seven S1 §0.1 interpretations are mechanical readings,
     each citing its governing decision, recorded for parent review.
  7. Expected changed files derived from the A4 header (exactly two test
     files) and current source (both verified `ABSENT`).
  8. Dirty tree inventoried without modification: both nested repositories
     clean (`email_scraper` `fac5bb0`, `frontend` `c85f93b`); root porcelain
     is exactly the 36-line owner-controlled relocation set (authoritative
     `LC_ALL=C` digest `d1a974b3…` recomputed and byte-equal this session)
     plus the three KI-W5 subordinate artifacts (tracked, modified by the
     closed W5 window's accepted evidence flow) plus this window's three new
     untracked subordinate artifacts — and nothing else.
  9. No unrelated owner-controlled change will be overwritten.
  10. No required action exceeds parent authority (local-only; mocked
      external boundaries; no provider/AWS/production/commit action).
- **Prerequisite existence proof (KI-W6-P3):** verified on disk this session
  — `test/helpers/isolated-postgres.js` (schema create/migrate deploy/stay-
  in-schema asserts); the accepted in-memory fake shapes
  (`memoryS3` worker-flow.test.js:160–182; `memoryDispatcher` :183–199; the
  `drain` pump worker.test.js:181–203); the G-R9 provider snapshot recipe
  (aws-pipeline-end-to-end.integration.test.js:42–54); the ambiguity trigger
  (adapter.test.js:359–369, HTTP-200 JSON-decode failure → terminal
  ambiguous); `PrismaRunRepository(prisma, { runExecutionBackend: "aws",
  ... })` creating AWS-backend runs (prisma-run-repository.js:942–975) with
  `confirmQueryRevision` equality fencing (:1440–1497); the server AWS
  branch wiring (`pipelineRuntimeFactory` override, `researchQueryValidationPipeline`
  default with `awsProbeSearchPage`, server.js:1077–1131, 1461–1530); the W5
  browser harness (all five phases); local Chrome and production Next build
  (proven by the accepted KI-W5 V1 gate).
- **Negative-search pre-verification (KI-W6-P2 basis):** executed this
  session — backend `src/`: 0 matches (both patterns); frontend trees: one
  comment-only provenance match (`keyword-dashboard.module.css:2`) and zero
  non-comment matches; CDN pattern 0; standalone repository clean. Frozen as
  the §0.1 item-7 comment-exclusion rule.
- **Digest computations (§4 method, `LC_ALL=C`):** two-path planned set
  `bb9f6381cc3b65d08b696fa1f62a2d75759289b4d4f0f44554ca44a2ebf56edc`;
  20-case required union
  `8d6d002cdf86a30459c2d140977fec3b72c30a8d1c4d612f512bd7c37ed4c523`.
- **Artifacts authored:** S1 (833 lines + two amendment edits; revision
  `a0e3e28b7d9e272cfa6b1eec79f224d2b156725d7ebc86b729bfe3067dd42d87`),
  S2 (this state, `AWAITING_PARENT_DECOMPOSITION_REVIEW`), this S3.
- **External mutations/cost:** three coordination files created at the
  workspace root; nothing else; `$0.00`.
- **Disposition:** decomposition authored; readiness pass follows
  (`EV-KI-W6-S02`).

---

## `EV-KI-W6-S02` — Readiness completion and self-falsification

- **Timestamp:** 2026-08-20T09:43:00+05:30
- **Actor/role:** `KI-W6-WINDOW-AGENT` (readiness audit)
- **Checklist completion:** all 44 `SW-*` items in S1 §9 carry resolvable
  references to S1 sections or to this evidence file; zero unchecked, zero
  `N/A`.
- **Self-falsification pass (standard §14, applicable counterexamples):**
  two-writable-files/directory-wildcard naming — rejected by the S1 block
  schema (single literal `writable_file` each; `node --check`/C1 write-set
  proof); unplanned second workspace file — C1 attributable-delta proof in
  both blocks plus build outputs being gitignored; source+test assigned
  together — both sub-windows ARE test files, no production file is
  writable; required parent file absent — §3 equality proof (required set =
  planned set = owned set); duplicate owner — one owner per path; dependent
  before interface freeze — S002 depends only on S1-frozen literals, not on
  S001 execution; unexplained intermediate failure — §8 of S1 §5 blocks
  defines the only permitted pending states (deferred official gate runs);
  subagent successor/parent communication — common prohibited list; window
  agent repairing during review — §7 correction rules; correction rewriting
  history — append-only C-IDs; omitted/skipped cases — certificates assert
  set equality with §4 digests; oracle weakening — NC controls falsify the
  bypass paths; substitute over-claim — §0.1 item 1 bounds the UI-leg claim
  to aggregate `pathWitness` parity; costly gate repetition — frozen once at
  I001 with documented invalidation; correction without invalidation — §7;
  assembled set divergence — I001 write-set proof vs
  `bb9f6381…`; premature successor — `KI-W7` prohibited everywhere,
  `STOP_LOCAL` successor reserved for the parent.
- **Predictable requester gates:** the DB opt-in run requires the
  requester-provided isolated `TEST_DATABASE_URL` (distinct from
  production); sandbox `listen EPERM` failures are rerun under approval;
  commits remain requester-only.
- **External mutations/cost:** none beyond the three coordination files;
  `$0.00`.
- **Disposition:** readiness complete; certificate appended below.

---

## Decomposition readiness certificate (§12.1)

```yaml
certificate: SUBWINDOW-DECOMPOSITION-READY
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-01
window_agent_identity: KI-W6-WINDOW-AGENT
revisions:
  parent_standard: 3b7a4fd25156e1adfbc92abb835c5f82a0d18c686b1c1150feb202f2d944d2ac
  subwindow_standard: 1766f9107ce7d315877b75d4b0ea2b5521dff1c321e12f890b03787d66196ded
  contract: 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c
  decision: c2dc635e5aa58f88c1ec465154663d314af68570fd4cbfdfca7b51c393c6f70f
  parent_checklist: 324667cbe0d467ecf4f913c93e91087e75192bd463e0c05b033ee418754a362e
  decomposition: a0e3e28b7d9e272cfa6b1eec79f224d2b156725d7ebc86b729bfe3067dd42d87
initial_subwindow_ids: [KI-W6-S001, KI-W6-S002]
initial_subwindow_count: 2
planned_file_set: [email_scraper/test/keyword-intelligence-e2e.integration.test.js, frontend/test/browser/keyword-intelligence-e2e.mjs]
planned_file_set_digest: bb9f6381cc3b65d08b696fa1f62a2d75759289b4d4f0f44554ca44a2ebf56edc
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
first_subwindow: KI-W6-S001
integration_assessment_id: KI-W6-I001
parent_review_required: true
```

The window agent stops here. No leaf begins before the parent's
decomposition review and the window agent's resulting `S2.decomposition_status:
READY` transition.
