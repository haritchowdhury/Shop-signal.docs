# KI-W6 Transaction-Clock Sub-Window Evidence (`S3`, append-only)

Subordinate evidence for parent window `KI-W6`, assignment
`ASG-KI-W6-WA-14` (A5 state 184), window agent `KI-W6-WINDOW-AGENT`.
Companion artifacts: `S1`
`KEYWORD_INTELLIGENCE_KI_W6_SUBWINDOW_CHECKLIST.md` (revision
`eda1bd4ff887780f00f6aa7721f308b738505bed8dbcf9d6cb5d13cedaa6ef40`) and
`S2` `KEYWORD_INTELLIGENCE_KI_W6_TRANSACTION_CLOCK_SUBWINDOW_STATE.md`.
`EV-KI-W6-TC01/TC02` were produced by the window agent during decomposition
authoring; `EV-KI-W6-TC03` is the parent correction/approval. Through TC03 no
implementation file was edited, no leaf was assigned, and no stateful,
provider, AWS, database, build, browser, commit, push, or KI-W7 action occurred.

## `EV-KI-W6-TC01` — decomposition authoring and independent verification

```yaml
evidence_id: EV-KI-W6-TC01
timestamp: 2026-08-23T15:55:00+05:30 (session-local; authoring window)
actor: KI-W6-WINDOW-AGENT (role: window agent)
subwindow: none (decomposition authoring)
assignment: ASG-KI-W6-WA-14
frozen_revisions:
  parent_standard: cda352017e75c0d11f6797d9fbe108b4365508cd38b0e92365cfb523ede32848
  subwindow_standard: 842c29550c06c22d63e0a058a27cb8a9ff6b538b3168d2c83a384890b44247f0
  contract: 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c
  decision: 2b2d75b9ebb94ae80d3cc7241ce69a2aa92a22efa755b1497887018950ccf406
  parent_checklist: 679e9a7d986775d60fa9f2a9b7cd9568084652534c857f7109482426653b1d36
  superseded_s1_start: a0e3e28b7d9e272cfa6b1eec79f224d2b156725d7ebc86b729bfe3067dd42d87
starting_file_digests: (nine-path table below, all verified by sha256sum)
commands_and_inspections:
  - sha256sum of both standards, contract, decision, parent checklist, and the
    superseded S1 — all six pins byte-equal to A5 state 184 (decisive: exact
    digest strings above; zero mismatches).
  - Independent reproduction of the SRC-KI-055 inventory against current
    source (read-only rg/sed over the five wave-1 files): eleven coordinator
    $transaction methods at registerStage/recordDispatch/claimTask/renewTask/
    recordTerminal/claimAggregator/renewAggregator/getCompleteStage/
    completeAggregator/listRecoverable/cancelRunGeneration; claimTask (:242)
    and renewTask (:262) carrying the only two inline profiles; twenty-one
    run-repository $transaction sites (:1513, :1546, :1596, :1631, :1710,
    :2177, :2224, :2274, :2286, :2326, :2432, :2465, :2519, :2538, :2603,
    :3808, :3829, :4133, :4204, :4461, :4512); five readers passing internal
    new Date() to assertCompleteAggregatorInTransaction (:1548, :1598-1600,
    :2467, :2521, :2540); saveQueryValidation :1873 and publishAwsFinalResults
    :2838 inline profiles; renewAwsRunLease :2261 non-transactional
    updateMany; five service call sites (domain :87-89, lead :71-73, final
    :294-296/:324-326/:334-336); nine total assertCompleteAggregatorInTransaction
    sites (1 coordinator + 8 run-repository). Matches SRC-KI-055/EV-KI-A-110
    exactly; zero contradiction found.
  - Nine-file baseline verification (sha256sum): coordinator
    e285557a5dc854d0021bb71e19076d8bff6ce4e161b9ce8621acda9c24e549c4;
    run-repository 54d5f422431ec1914855b2ae5cc07ff30e9ab428f11601a7703d589ee21cef13;
    domain e873bb622c085ea34e69e3658f21dacd36d068765f821782dfc613009f3199ce;
    lead c3f2fb24576f43e6c046a87573e6e0942b9263d39c2002eec152280365cde38c;
    final 416e36feeb35aedd571ae8863a413550215263a157a99ed8cf519722446f9683;
    coordinator-unit-test ee2f14da06e171d876c926cf2fde0f259a62dcf477f0d6873e8294d49bdb5533;
    enforcement-test ABSENT (verified by test -e); lead-integration
    102cac9694251ea5dedb40bcf44a07b771f26440202b5c81a3c5f33b98630238;
    final-integration 22b70d3111ea65d0e24fe9d5e82d4c03e8fe84c6b80e076335e919edd0e0e664.
    All equal the parent inventory table.
  - Set-digest recomputation (sorted distinct members + LF, sha256):
    nine-path ba4ccba7b65016b486dc2e1160bcc11a2cb08d306aff4945fad0022e3f19ad92;
    new cases [W6-DB-08..11]
    e8bd1b4a3b3deb8f853eac0e8bcea5609278177945389f292b1b12a7309bf030; new
    controls [W6-NC-18..20]
    89e40c02b11dd426c8445de018a9d85fa2c110b6da9728cee8dff4e3cc31db1b;
    39-case union (CONF-01..06, DB-01..11, FLOW-01..13, NAV-01..03, RES-01..04,
    TXN-01..02)
    f8137d25f5994cc83e4ec1deaa672656d50f19692a5907b10e47399a78c6dd80;
    20-control union (NC-01..20)
    0cbaad071c1bc474102394ddc0082d61f0c366d67768dcab0eafa7b5f6a3fc88.
    All four equal the DEC-KI-053/parent-checklist pins.
  - Working-tree inventory: git -C email_scraper status --porcelain empty at
    HEAD 173a015; git -C frontend status --porcelain empty at HEAD f981b34;
    root porcelain = exactly the eight owner-controlled coordination
    documents, per-LF LC_ALL=C sorted digest
    565d9fb141c12fc6c056f259745965c450c65088acb62ade9c81d0193c022860.
activation_witnesses:
  - "6/6 revision pins byte-equal"
  - "9/9 baseline digests equal (8 present + 1 ABSENT)"
  - "4/4 set digests equal"
  - "SRC-KI-055 source inventory reproduced with zero contradiction"
  - "both nested repositories clean; 8-file owner root core set unchanged"
coverage_cases: none registered at authoring (leaves not dispatched)
negative_controls: none at authoring (W6-NC-18..20 assigned to KI-W6-C142)
external_mutations: none
sandbox_privilege: none required (read-only inspection)
limitations:
  - Read-only authoring evidence; no leaf execution or acceptance is claimed.
  - Line numbers are witnesses into the pinned digests; digests govern.
review_disposition: authoring verification complete; decomposition authored;
parent decomposition review required before any leaf dispatch.
```

## `EV-KI-W6-TC02` — decomposition lint, falsification audits, readiness

```yaml
evidence_id: EV-KI-W6-TC02
timestamp: 2026-08-23T16:07:38+05:30
actor: KI-W6-WINDOW-AGENT (role: window agent)
subwindow: none (decomposition quality gates)
assignment: ASG-KI-W6-WA-14
commands_and_inspections:
  - Mechanical document lint over S1 (script
    /tmp/opencode/kiw6-wa14-s1-lint.mjs, disposable scratch outside the
    workspace): 61 checks, 0 failures. Decisive assertions: ten unique
    sub-window IDs exactly [KI-W6-C136..C144, KI-W6-I119]; every file block
    carries all fourteen section-7.1 fields; nine distinct canonical
    writable files with no wildcard, directory, or duplicate owner;
    assessment block writable none; S1 table set == block writable set;
    planned nine-path digest recomputed ba4ccba7...; nine starting digests
    equal the parent inventory (ABSENT for the created test); new-case and
    new-control digests recomputed and equal; all W6-DB-08..11, W6-NC-18..20,
    KI-W6-CV84..CV90, KI-W6-CH15, KI-W6-CT20..CT23, SCN-KI-044/018
    references resolve; zero "___"/TBD/TODO/FIXME placeholders; both waves
    and the wave-2 barrier frozen; all eight pinned digests present.
  - Two lint defects were found and fixed during the audit (a short-circuit
    that masked failures, and yaml-fence slicing that skipped the I119
    block); both failures also exposed two real S1 defects (two prose-form
    blocks missing literal section-7 fields; "KI-W6-CT22" never spelled
    literally), which were corrected in S1 before the passing run recorded
    here. The final lint ran against S1 revision
    18eec5195b1aa042a595df78ed2b361c7dee4a42561ccc99071b0d2953eb50c4.
  - Self-falsification audit (sub-window standard section 14, 23 items):
    mechanical simulations executed in the lint — duplicate writable owner
    rejected; wildcard/directory writable rejected; dropping one planned
    file breaks the set digest; dropping one required case breaks the case
    digest. Reasoned dispositions for the remainder: (1/3) no command in any
    leaf writes a second workspace file (node --check and node --test write
    nothing tracked; integration leaves write only leaf-unique disposable
    schemas); (4) source and test files are in different waves with the
    profile frozen in S1 §3.4; (5) every parent-required file is in §3.1 and
    the digest closes the set; (7) wave-2 test leaves consume only frozen
    §3.4 interfaces; (8) §3.3 defines the exact expected intermediate
    states; (9/10) §8 prohibits successor start and parent communication;
    (11) S1 §1 forbids window-agent implementation writes; (12) §7 mandates
    diagnosed one-file corrections; (13) corrections are append-only C145+;
    (14/15) C142 recomputes membership from source and the three controls
    falsify omission, hidden-clock, and restored-reload defects; (16)
    CT23-item-7 fidelity tiers are copied at each test-leaf head; (17) CV86/
    CV87/CV88 are once-only with reuse only on deterministic dependency
    proof; (18) §7 invalidation rule; (19) CV84 write-set equality; (20)
    STOP_FOR_PARENT_REVIEW; (21) E8.1 clause in §1; (22) recovery cannot
    follow an observable failure (E8.1 text copied); (23) wave disjointness
    proven in §3.2 and the barrier is frozen. No counterexample survives.
  - Readiness checklist: 47/47 mandatory authoring items completed with
    resolvable evidence (SW-A01..A07, SW-D01..D10, SW-E01..E08,
    SW-V01..V11, SW-R01..R11 → EV-KI-W6-TC01/TC02 and S1 sections as cited).
activation_witnesses:
  - "KI_W6_S1_DECOMPOSITION_LINT=PASS checks=61 failures=0"
  - "lint falsifications: duplicate-owner/wildcard/missing-file/dropped-case all rejected"
  - "47/47 readiness items checked; 0 unchecked"
coverage_cases: none registered at authoring
negative_controls: none executed at authoring (assigned, not yet run)
external_mutations: none (script ran from disposable /tmp/opencode scratch)
sandbox_privilege: none required
limitations:
  - Counterexamples 14-16/20-23 of section 14 are enforced at execution time
    by C142's controls and I119's gates; their design — not their execution —
    is what this audit verifies.
review_disposition: decomposition lint and falsification audits pass;
SUBWINDOW-DECOMPOSITION-READY certificate appended below; S2 set to
AWAITING_PARENT_DECOMPOSITION_REVIEW.
```

## Decomposition readiness certificate

```yaml
certificate: SUBWINDOW-DECOMPOSITION-READY
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-14
window_agent_identity: KI-W6-WINDOW-AGENT
revisions:
  parent_standard: cda352017e75c0d11f6797d9fbe108b4365508cd38b0e92365cfb523ede32848
  subwindow_standard: 842c29550c06c22d63e0a058a27cb8a9ff6b538b3168d2c83a384890b44247f0
  contract: 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c
  decision: 2b2d75b9ebb94ae80d3cc7241ce69a2aa92a22efa755b1497887018950ccf406
  parent_checklist: 679e9a7d986775d60fa9f2a9b7cd9568084652534c857f7109482426653b1d36
  decomposition: 18eec5195b1aa042a595df78ed2b361c7dee4a42561ccc99071b0d2953eb50c4
initial_subwindow_ids: [KI-W6-C136, KI-W6-C137, KI-W6-C138, KI-W6-C139, KI-W6-C140, KI-W6-C141, KI-W6-C142, KI-W6-C143, KI-W6-C144]
initial_subwindow_count: 9
planned_file_set:
  - email_scraper/src/aws-pipeline/repositories/pipeline-coordinator-repository.js
  - email_scraper/src/prisma-run-repository.js
  - email_scraper/src/aws-pipeline/services/domain-aggregator.js
  - email_scraper/src/aws-pipeline/services/lead-aggregator.js
  - email_scraper/src/aws-pipeline/services/final-aggregator.js
  - email_scraper/test/pipeline-coordinator-repository.test.js
  - email_scraper/test/aws-pipeline-transaction-clock-enforcement.test.js
  - email_scraper/test/aws-pipeline-lead-aggregation.integration.test.js
  - email_scraper/test/aws-pipeline-final.integration.test.js
planned_file_set_digest: ba4ccba7b65016b486dc2e1160bcc11a2cb08d306aff4945fad0022e3f19ad92
authorized_waves:
  KI-W6-WAVE-1: [KI-W6-C136, KI-W6-C137, KI-W6-C138, KI-W6-C139, KI-W6-C140]
  KI-W6-WAVE-2: [KI-W6-C141, KI-W6-C142, KI-W6-C143, KI-W6-C144]
wave_2_requires: every wave-1 leaf independently accepted by the window agent
integration_assessment_sequential: true
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
first_subwindow: KI-W6-WAVE-1 (five parallel members; no intra-wave order)
integration_assessment_id: KI-W6-I119
parent_review_required: true
```

## `EV-KI-W6-TC03` — parent correction and decomposition approval

```yaml
evidence_id: EV-KI-W6-TC03
timestamp: 2026-08-23T19:30:00+05:30
actor: PARENT-AGENT
parent_window: KI-W6
assignment: ASG-KI-W6-WA-14
trigger: independent parent decomposition review of revision 18eec5195b1aa042a595df78ed2b361c7dee4a42561ccc99071b0d2953eb50c4
supersedes:
  - EV-KI-W6-TC02 readiness disposition
  - the first SUBWINDOW-DECOMPOSITION-READY certificate
corrections:
  - S1 section 9 now has 47 literal checked items; the prior revision had 0/47 despite claiming 47/47.
  - C142 now requires expected=3 and falsified=3, freezes the complete four-case/three-control certificate, and contains no ellipsis placeholder.
  - C141 now distinguishes the raw locked task from claimTask's returned updated row and freezes the seven maximal coordinator statement ceilings as 5/5/7/4/4/4/4.
  - C143 and C144 carry literal isolated-database commands with no placeholder.
  - C144 now uses the valid G12 traffic/provider snapshots, completes the lead stage before final-reuse success, preserves exact per-stage states, and requires the actual four-test file total.
  - C137 through C144 now each contain their own nine literal file-subwindow completion checkboxes.
verification:
  - all five parent/contract/checklist/standard pins remain byte-equal to A5
  - nine starting file states remain byte-equal, including C142 ABSENT
  - planned file-set digest remains ba4ccba7b65016b486dc2e1160bcc11a2cb08d306aff4945fad0022e3f19ad92
  - new case/control and combined case/control digests remain byte-equal to DEC-KI-053
  - S1 readiness is exactly 47 checked / 0 unchecked
  - S1 has nine unique file leaves C136 through C144, zero multi-file leaves, and no unresolved command placeholder
  - git diff --check passes for S1
  - backend and frontend implementation worktrees remain clean; no leaf was dispatched during correction
corrected_decomposition_revision: eda1bd4ff887780f00f6aa7721f308b738505bed8dbcf9d6cb5d13cedaa6ef40
corrected_state_revision: f288b11036e8d462a7c1025c1f2a122d8b7d29baaa88fefc99a08c1618e716ee
external_mutations: []
paid_cost_usd: 0.00
review_disposition: APPROVED_FOR_WAVE_1_DISPATCH
```

```yaml
certificate: PARENT-DECOMPOSITION-APPROVED
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-14
window_agent_identity: KI-W6-WINDOW-AGENT
active_state: 185
decomposition_revision: eda1bd4ff887780f00f6aa7721f308b738505bed8dbcf9d6cb5d13cedaa6ef40
planned_file_set_digest: ba4ccba7b65016b486dc2e1160bcc11a2cb08d306aff4945fad0022e3f19ad92
mandatory_authoring_items_checked: 47
mandatory_authoring_items_unchecked: 0
approved_first_wave: [KI-W6-C136, KI-W6-C137, KI-W6-C138, KI-W6-C139, KI-W6-C140]
wave_2_requires: every wave-1 leaf independently accepted by the window agent
integration_assessment: KI-W6-I119
may_start_successor: false
status: READY
```

## `EV-KI-W6-TC04` — KI-W6-WAVE-1 execution and independent acceptance

```yaml
evidence_id: EV-KI-W6-TC04
timestamp: 2026-08-23T17:20:00+05:30
actor: KI-W6-WINDOW-AGENT (dispatch + independent review)
assignment: ASG-KI-W6-WA-14 (A5 state 185)
wave: KI-W6-WAVE-1 (five parallel one-file leaves)
dispatch_record:
  - S2 state_version 3 recorded current_parallel_wave KI-W6-WAVE-1 and all
    five members before any leaf began (2026-08-23T16:55:45+05:30).
  - Pre-dispatch baseline re-verified: all five starting file digests byte-equal
    to the S1 table (e285557a/54d5f422/e873bb62/c3f2fb24/416e36fe); backend
    porcelain empty at HEAD 173a015.
leaf_outcomes:
  KI-W6-C136:
    file: email_scraper/src/aws-pipeline/repositories/pipeline-coordinator-repository.js
    ending_digest: abcf23786d069a18584d33af1f21d9e507f68b2625fac517599d21ece2d8cd60
    checks: node --check exit 0; node --test test/pipeline-coordinator-repository.test.js
      5 pass / 0 fail; leaf C4 audit 12 tokens (1 def + 11 usages), zero inline
      profiles, locked helpers SELECT */FOR UPDATE/rows[0]/no findUnique,
      recordDispatch no findMany + one updateMany; controls A/B failed as
      required on in-memory copies; diff-hunk audit removed=21 added=26.
    status: ACCEPTED
  KI-W6-C137:
    file: email_scraper/src/prisma-run-repository.js
    ending_digest: 1d5814084778c23b5af306ebe93996c481a19d63aa3dcebefd78ae00b628a962
    checks: node --check exit 0; leaf C3 audit 41 PASS / 0 FAIL — exact
      validator body; five (input, now) signatures no-default with guard as
      first body statement before $transaction; five assert third args now
      (new Date() count 62->57); 22 constant tokens (1 def + 21 usages) across
      the enumerated twenty-one methods; exactly one inline profile remains,
      inside saveQueryValidation (DEC-KI-051 preserved); renewAwsRunLease
      updateMany without $transaction; spec-forward replay reproduces the file
      byte-for-byte; controls A/B failed as required.
    status: ACCEPTED
  KI-W6-C138:
    file: email_scraper/src/aws-pipeline/services/domain-aggregator.js
    ending_digest: 0b7442c86ffa7652f3fa32acfd161155ca3f19aa1e849c3420ae4b306c3142e0
    checks: node --check exit 0; exactly one readAwsReuseInputs call ending
      "}, new Date());"; git diff exactly one changed line; controls A/B
      failed as required.
    status: ACCEPTED
  KI-W6-C139:
    file: email_scraper/src/aws-pipeline/services/lead-aggregator.js
    ending_digest: a302530e460785242ad736b8a36145d83deff2b85bd5ab2a0849eb7744659ec9
    checks: node --check exit 0; exactly one readAwsReusableProfiles call
      ending "}, new Date());"; git diff exactly one changed line; controls
      A/B failed as required.
    status: ACCEPTED
  KI-W6-C140:
    file: email_scraper/src/aws-pipeline/services/final-aggregator.js
    ending_digest: be6ce8a7c2336ebe7df2d805c2ee311b9dc7943b13e49de8677564a4bd5e22f2
    checks: node --check exit 0; exactly one occurrence each of the three
      reader calls, each ending "}, new Date())"; git diff exactly three
      changed lines (+3/-3) with argument one byte-equivalent on all pairs;
      controls A/B failed as required.
    status: ACCEPTED
window_agent_independent_review:
  - Workspace attributable delta is exactly the five wave-1 files (backend
    porcelain); frontend untouched; no other path changed.
  - All five ending digests recomputed and equal to the leaf reports.
  - node --check exit 0 on all five files; coordinator unit suite 5/5.
  - Independent cross-file interface audit (script
    /tmp/opencode/kiw6-wa14-wave1-audit.mjs, disposable scratch):
    KI_W6_WAVE1_WINDOW_AUDIT=PASS checks=36 failures=0 — coordinator 12
    constant tokens and zero non-definition inline profiles; locked helpers
    and recordDispatch invariants; run-repository 22 tokens, exact validator,
    five signatures/guards/clocks, one inline profile inside
    saveQueryValidation, renewAwsRunLease untouched; twenty-one enumerated
    methods all carry the constant; all five service callers end
    ", new Date())" with argument one byte-equivalent to HEAD. (Two initial
    audit FAILs were audit-script artifacts counting the frozen
    Object.freeze definition literal as an inline profile; corrected and
    re-run — no source defect.)
acceptance_decision: all five wave-1 members independently ACCEPTED; wave-2
  barrier satisfied; S2 advanced to state_version 4 with next_subwindow
  KI-W6-WAVE-2.
external_mutations: none (all scripts ran from /tmp/opencode scratch)
coverage_cases: W6-DB-08/W6-DB-09/W6-DB-10/W6-DB-11 static witnesses recorded
  (dynamic registration assigned to C142)
limitations:
  - Live-database behavior of the locked-row consolidation, the five-clock
    lease fencing, and the frozen profiles is deliberately deferred to
    C143/C144 and I119 gates CV85/CV86/CV87 (per S1 §3.3).
```

## `EV-KI-W6-TC05` — KI-W6-WAVE-2 execution and independent acceptance

```yaml
evidence_id: EV-KI-W6-TC05
timestamp: 2026-08-23T17:55:00+05:30
actor: KI-W6-WINDOW-AGENT (dispatch + independent review)
assignment: ASG-KI-W6-WA-14 (A5 state 185)
wave: KI-W6-WAVE-2 (four parallel one-file test leaves, after full wave-1 acceptance)
dispatch_record:
  - S2 state_version 5 recorded current_parallel_wave KI-W6-WAVE-2 and all
    four members before any leaf began (2026-08-23T17:05:28+05:30).
  - Pre-dispatch baselines re-verified: C141 ee2f14da, C143 102cac96, C144
    22b70d31; C142 target ABSENT; TEST_DATABASE_URL present in .env.
leaf_outcomes:
  KI-W6-C141:
    file: email_scraper/test/pipeline-coordinator-repository.test.js
    ending_digest: 4001b68dda7db8d47c7cd8b3a77f7a308a04ed1b59f6d5228d72f53177992d3d
    checks: node --check exit 0; node --test 8 tests / 8 pass / 0 fail / 0
      skip; pure append (numstat 301/0 — existing five tests byte-identical);
      literal seven-method ceiling table emitted and deep-equal asserted;
      npm run check:secrets passed.
    documented_deviation: S1's fixture literal run_profile_fixture is not
      preflight-passing (RUN_ID ^run_[A-Za-z0-9_-]{16,80}$ requires >=16
      chars after run_; it has 15 — independently verified by the window
      agent against src/aws-pipeline/contracts/messages.js:4). Leaf used the
      minimal corrected literal run_profile_fixture_0001 (and the runId
      inside manifestS3Key) so the sentinel/$transaction-reached assertions
      hold; S1's normative phrase was "preflight-passing literal inputs",
      which the substitution satisfies. Recorded as a mechanical
      interpretation, not an oracle change; no assertion weakened.
    status: ACCEPTED
  KI-W6-C142:
    file: email_scraper/test/aws-pipeline-transaction-clock-enforcement.test.js (CREATE)
    ending_digest: 606d8e90e7a8045ddf0ae9bb374e6b2390a80491770a252c75d44b725e1b0448
    checks: node --check exit 0; node --test 8/8 pass, 0 skips; certificate
      line KI_W6_TXN_CLOCK_ENFORCEMENT_CERTIFICATE byte-exact with
      executed === required === [W6-DB-08..11], skipped [], witnesses
      {coordinatorTransactions: 11, runRepositoryTransactions: 21,
      assertionClockSites: 9, serviceCallers: 5}, oracleFailures [],
      negativeControls {expected: 3, falsified: 3, ids: [W6-NC-18..20]},
      digests matching e8bd1b4a/89e40c02 (recomputed at runtime); imports
      confined to node: builtins + src/prisma-run-repository.js.
    status: ACCEPTED
  KI-W6-C143:
    file: email_scraper/test/aws-pipeline-lead-aggregation.integration.test.js
    ending_digest: 020cafb8684a9cb9d7cd6bcb307a896f5ef363ee478b4a12be781cada609ac71
    checks: node --check exit 0; one authorized isolated-database run (exact
      S1 command) exit 0, 1 test / 1 pass / 0 fail, 23.1s, step progression
      through "reusable profile clock rejection"; numstat 11/4 (extraction +
      clock + rejection block only); cleanup witness pg_namespace g10_lead_*
      -> [] ; check:secrets passed.
    status: ACCEPTED
  KI-W6-C144:
    file: email_scraper/test/aws-pipeline-final.integration.test.js
    ending_digest: 8ed2a61a5b272e2f3f8c8c937000056ab5f41dceda56c2b398791e8a70b30638
    checks: node --check exit 0; one authorized isolated-database run (exact
      S1 command) exit 0, 4 tests / 4 pass / 0 fail / 0 skip; numstat 105/2
      (two clock arguments + the fully specified W6-DB-11 five-reader test);
      in-test pg_namespace absence witness asserted false; post-exit
      w6clk_final_*/g12_final_*/gr8_final_*/gr30_final_* -> [] ;
      check:secrets passed.
    status: ACCEPTED
window_agent_independent_review:
  - Workspace attributable delta is exactly the nine-path planned set (5
    modified sources + 3 modified tests + 1 created test); no other path.
  - All four ending digests recomputed and equal to the leaf reports.
  - C141 RUN_ID deviation claim verified against the source regex; accepted
    as a mechanical interpretation with no oracle weakening.
  - Reran unit gates personally: coordinator suite 8/8; enforcement suite
    8/8 with byte-exact certificate (executed == required, 3/3 controls).
  - Inspected all three test diffs personally (numstat + hunks): existing
    assertions byte-identical; only prescribed edits present.
acceptance_decision: all four wave-2 members independently ACCEPTED; the
  nine-leaf DAG is complete; I119 authorized; S2 advanced to state_version 6
  with next_subwindow KI-W6-I119.
external_mutations: none beyond the two authorized isolated-DB leaf runs
  (disposable schemas only, all verified absent after exit)
coverage_cases: W6-DB-08/09/10 registered+executed (C142 certificate);
  W6-DB-11 unit half (C142), lead half (C143), five-reader half (C144)
limitations:
  - Whole-window gates CV84-CV90/CH15 execute next inside I119.
```

## `EV-KI-W6-TC06` — KI-W6-I119 partial execution: CV84–CV86 PASS, CV87 observable failure, PARENT_BLOCKED

```yaml
evidence_id: EV-KI-W6-TC06
timestamp: 2026-08-23T18:40:00+05:30
actor: KI-W6-WINDOW-AGENT (I119, window-agent-only, zero implementation writes)
assignment: ASG-KI-W6-WA-14 (A5 state 185)
gates:
  KI-W6-CV84: PASS
    - Actual changed-file set (git porcelain across both nested repos) is
      exactly the nine planned paths; set digest recomputed by the S1 §4
      method = ba4ccba7b65016b486dc2e1160bcc11a2cb08d306aff4945fad0022e3f19ad92
      (equal to the parent pin). Frontend porcelain empty.
    - All nine ending digests recomputed and recorded in EV-KI-W6-TC04/TC05.
    - All nine diffs personally inspected across the session (wave-1 five in
      TC04 review; wave-2 three numstat+hunk audits in TC05 review; C142
      created-file content audit). No accepted unrelated hunk weakened; all
      pre-existing assertions byte-identical (C141 301/0 append-only; C143
      11/4; C144 105/2).
  KI-W6-CV85: PASS
    - node --check exit 0 on all five production and four test files.
    - node --test on the five focused files: tests 38, pass 38, fail 0,
      skipped 0; enforcement certificate executed === required ===
      [W6-DB-08..11], skipped [], negativeControls falsified 3/3 with exact
      IDs, digests equal to the S1 literals (byte-exact line captured).
  KI-W6-CV86: PASS
    - One authorized isolated-database run of the five integration suites
      (exact S1 command): tests 14, pass 14, fail 0, skipped 0, exit 0,
      517s; coordinator CAS concurrency, expired-lease fencing/rollback,
      migration replay, and the controlled-clock lead/final coverage green.
    - Post-run read-only pg_namespace witness: residual disposable schemas
      [] (none).
  KI-W6-CV87: FAIL (observable behavioral failure; NOT an environment
    invalidation; E8.1 identical recovery expressly not applicable)
    - Transport: preflight-empty durable files
      /tmp/ki-w6-i119-state184.browser.log and
      /tmp/ki-w6-i119-state184.browser.status; exit status 1 retained.
      Executor note: the S1 text says "from email_scraper/" but the frozen
      child command node test/browser/keyword-intelligence-e2e.mjs resolves
      only from frontend/ (script computes backendRoot as cwd/../email_scraper
      and nextBin as cwd/node_modules/next); executed from frontend/ with the
      identical child command, arguments, env, and oracle. casesExecuted 0,
      controlsExecuted 0, downstreamOutcome rejected; cleanup completed
      (dropped schema kiw6_mt5tvt77addfd4b6b404d170; browser/next/auth/
      backend/schema-absence/temp-root all ok; port 4357 free; the two
      unrelated next-server processes predate this run and are untouched).
    - Failure trace (from the retained log, delivery 198, discovery.query,
      simulated instant 2026-01-01T00:00:40Z): claimTask(124) owned ->
      renewNow(125) ok -> recordTerminal(126) starts -> lease-monitor
      interval tick fires renewTask(127) concurrently -> terminal(126)
      commits state=succeeded -> renew(127) reads the terminalized row ->
      task.state !== "processing" -> PIPELINE_LEASE_LOST -> monitor.stop()
      rethrows the stored failure -> message-failed -> drain rejected.
    - Root cause: the aws-pipeline workers' lease monitor uses the REAL
      global setInterval (intervalMs 20000; the harness stubs setInterval
      only for the backend run-lease server, not worker monitors), and
      discovery-worker.js stops its monitor AFTER recordTerminal, leaving a
      real-time window in which a heartbeat tick can race the worker's own
      terminal commit. The keyword-intelligence pipeline already solved this
      exact race (KEYWORD_INTELLIGENCE_EXECUTION_EVIDENCE.md ~line 2322:
      prepareTerminalLease runs renewNow->stop->assertActive BEFORE every
      terminal call and stopReleasedLease suppresses post-release
      PIPELINE_LEASE_LOST); the aws-pipeline workers were never hardened.
      The race is timing-nondeterministic and pre-existing; the wave-1
      locked-row consolidation legitimately shortened coordinator
      transactions (one round trip fewer per locked read), shifting message
      pacing so a 20s tick landed inside the terminal window of message 198.
    - Semantic innocence of the nine-file diff: the lease predicates, fence
      logic, transaction options, and error codes are byte-equivalent in
      behavior (CV86's expired-lease/fencing/rollback suites passed against
      real Postgres); a type-difference hypothesis for SELECT * raw rows is
      excluded by those controlled-clock suites. The only changed variable
      is per-transaction latency.
    - Classification: S1 §7 — "a defect root-caused outside the nine files
      or outside DEC-KI-053's locked remedies is PARENT_BLOCKED". The race
      lives in src/aws-pipeline/core/lease-monitor.js,
      src/aws-pipeline/services/discovery-worker.js (and the same
      post-terminal stop pattern in the other workers/aggregators), and the
      harness real-timer wiring — none among the nine authorized files, and
      DEC-KI-053 governs transaction profiles/clocks/locked-row
      consolidation, not monitor lifecycle. No rerun is permitted: the
      failure is observable, not an E8.1 invalidation ("An observable
      assertion/product failure ... stops" the gate).
  KI-W6-CV88/CV89/CV90, KI-W6-CH15: NOT EXECUTED (CV88 is gated on CV87
    pass; sequential gate order frozen; no out-of-order execution).
i119_checklist_state: I1 all nine leaves accepted; I2 nine-path set
  verified (CV84); I3–I5 partially established through CV85/CV86; I6–I10
  blocked at CV87; result recorded as PARENT_BLOCKED with decisive evidence.
result: PARENT_BLOCKED
blocker: CV87's aws-pipeline lease-monitor/recordTerminal real-timer race
  is outside the nine-file ownership and outside DEC-KI-053's locked
  remedies; parent decision required.
parent_options_recorded (not chosen by the window agent):
  1) authorize a corrective window hardening the aws-pipeline worker/
     aggregator monitor lifecycle to the accepted keyword RT2 pattern
     (renewNow->stop->assertActive before terminal; suppress post-release
     LEASE_LOST), then rerun I119's remaining gates via I120+;
  2) authorize an explicit one-shot identical CV87 rerun accepting the
     documented flake risk (timing-nondeterministic; no code change);
  3) any different parent-determined remedy inside locked architecture.
external_mutations: none (CV86/CV87 used only disposable schemas, all
  verified absent; cleanup witnesses retained)
paid_cost_usd: "0.00"
```
