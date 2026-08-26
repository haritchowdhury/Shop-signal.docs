# My Runs Research Resume — Append-Only Evidence Log (A6)

Evidence records facts and results; they do not grant authority. Mutable status
and assignment live only in A5.

Companions: A1 `MY_RUNS_RESEARCH_RESUME_PRODUCT_CONTRACT.md`; A2
`MY_RUNS_RESEARCH_RESUME_DISCOVERY_DOSSIER.md`; A3
`MY_RUNS_RESEARCH_RESUME_DECISION_LEDGER.md`; A4
`MY_RUNS_RESEARCH_RESUME_EXECUTION_CHECKLIST.md`; A5
`MY_RUNS_RESEARCH_RESUME_ACTIVE_STATE.md`; A7
`MY_RUNS_RESEARCH_RESUME_CHANGELOG.md`; A8
`MY_RUNS_RESEARCH_RESUME_TRACEABILITY.md`.

## Authoring evidence

```yaml
- evidence_id: MRR-AUTH-001
  kind: authority_artifact_audit
  result: PASS
  detail: Workspace AGENTS instructions, frontend AGENTS instructions, the canonical authoring standard, all eight distinct paths, product/exclusion/authorization boundaries, repository status and local-only escalation policy were inspected and recorded. A5 alone owns mutable status.

- evidence_id: MRR-AUTH-002
  kind: payload_no_guessing_audit
  result: PASS
  detail: Three internal payloads have exact provenance/contracts; all new consumed fields are product-owned durable fields; strict query/response parsing and malformed/boundary/unknown-key partitions are specified; result/config/selection/provider/artifact/private material is forbidden. Unknown payload count is zero.

- evidence_id: MRR-AUTH-003
  kind: discovery_lifecycle_audit
  result: PASS
  detail: Schema, repositories, backend routes, BFF routes, RunHistory, dashboard resume/polling, atomic handoff, no-list absence and current stale-test paths were inspected. Read-only listing adds no durable transition; queued/running/completed/failed, owner, handed-off, pagination, failure, abort and concurrent-handoff partitions are closed.

- evidence_id: MRR-AUTH-004
  kind: decision_closure_audit
  result: PASS
  detail: A3 fixes endpoint/schema/parser/query/projection/ordering/transaction/auth/cache/UI/history/test-invalidation choices, operation ceilings and compatibility. No schema/write/key/fingerprint/provider/retry/deployment choice remains.

- evidence_id: MRR-AUTH-005
  kind: scenario_enforcement_audit
  result: PASS
  detail: Reachable-path x state/identity x input/outcome x schedule dimensions reduce to 23 exact cases. Equivalent scalar/query mutations are table-driven; external/write/retry partitions are unreachable by the read-only design. Every case has action, witness, oracle, operation/forbidden set, parity, registration and control/fidelity disposition.

- evidence_id: MRR-AUTH-006
  kind: window_boundary_audit
  result: PASS
  detail: Acyclic W1-W3 sequence, explicit multi-window requester assignment, symbol-specific scopes, all F1-F5 fields, fifteen-field task traces, successor conditions and diff/handoff boxes are present. W3 is test-only and cannot conceal production defects.

- evidence_id: MRR-AUTH-007
  kind: trace_change_audit
  result: PASS
  detail: A8 maps all 15 requirements to evidence/decisions/tasks/cases/assertions; A7 records initial and user-requested test-correction revisions; IDs are unique; A6 append-only; A5 pins revisions and transition concurrency.

- evidence_id: MRR-AUTH-008
  kind: falsification_readiness_audit
  result: PASS
  detail: Forward/backward simulations, reachable-set, no-guessing, anti-vacuity, environment, scale/owner, mistake-derived, mechanical-link, implementation-choice, enforcement, substitute, accepted-test and sandbox-recovery audits passed. NC-01 through NC-10 cover every critical invariant.

- evidence_id: MRR-AUTH-009
  kind: diagnostic_baseline
  result: OBSERVED_NONZERO_BEFORE_IMPLEMENTATION
  commands:
    - frontend: npm test
    - backend: npm test
    - backend focused: node test/keyword-intelligence-api.test.js (localhost escalated)
    - four focused stale-test files
  outcomes:
    frontend: 21 of 22 test files pass; W5-A06 is the only failure
    backend_api_escalated: 35 of 46 tests pass; 11 failures collapse to five source failures plus dependent certificate failures
    backend_query_mapper: 5 of 9 pass; four obsolete contract assertions fail
    backend_worker_flow: 34 of 37 pass; three flows reject null trendSlope caused by obsolete fixture field placement
  classification: Diagnostic only; MRR-SRC-016 through MRR-SRC-018 mechanically explain the stale surfaces. Localhost EPERM from restricted non-escalated attempts is environment-only and disappears under identical escalation.
```

## Coverage-set certificate

```yaml
coverage_schema: mrr-required-case-set-v1
required_count: 23
required_digest_sha256: 8f367c356ee531534825fb1e56f51656e4d45231ae2cd64ef7fe40a9286d116e
digest_formula: distinct IDs sorted by unsigned UTF-8 bytes, each followed by one LF, SHA-256 lowercase hex
duplicate_ids: 0
unmapped_ids: 0
negative_controls: 10
critical_invariants_without_control: 0
```

## Authoring readiness certificate

```yaml
certificate: AUTHORING-READY
artifact_paths:
  A1: MY_RUNS_RESEARCH_RESUME_PRODUCT_CONTRACT.md
  A2: MY_RUNS_RESEARCH_RESUME_DISCOVERY_DOSSIER.md
  A3: MY_RUNS_RESEARCH_RESUME_DECISION_LEDGER.md
  A4: MY_RUNS_RESEARCH_RESUME_EXECUTION_CHECKLIST.md
  A5: MY_RUNS_RESEARCH_RESUME_ACTIVE_STATE.md
  A6: MY_RUNS_RESEARCH_RESUME_EVIDENCE.md
  A7: MY_RUNS_RESEARCH_RESUME_CHANGELOG.md
  A8: MY_RUNS_RESEARCH_RESUME_TRACEABILITY.md
revisions:
  standard: cda352017e75c0d11f6797d9fbe108b4365508cd38b0e92365cfb523ede32848
  contract: 02386e891133bffc3ad3e7134535873a5567c75c50418701e2f45182f96215fc
  decision: cf4a7a680bfb0c8b6d55e9a0dd9970169ba9fe38205bb9cc736b3ffe03d4e0e9
  checklist: 91d659e2d367b59b128abc74a547f6ba67fec3a93acf66cd0df9c49e83dd5a83
checked_authoring_items: 93
unchecked_required_items: 0
unresolved_evidence_references: 0
unresolved_payload_contracts: 0
delegated_implementation_decisions: 0
unowned_source_members: 0
unowned_plan_members: 0
unproven_competing_owner_pairs: 0
anti_vacuity_failures: 0
mistake_conformance_failures: 0
planned_coverage_cases: 23
unmapped_coverage_cases: 0
duplicate_coverage_case_ids: 0
critical_invariants_without_negative_control: 0
test_substitutes_without_fidelity_disposition: 0
unresolved_accepted_evidence_invalidations: 0
frozen_gate_ambiguities: 0
predictable_gates: []
requester_actions_before_start: []
authorized_first_window: MRR-W1
planned_stop: after MRR-W3 acceptance for independent review
audit_evidence: [MRR-AUTH-001, MRR-AUTH-002, MRR-AUTH-003, MRR-AUTH-004, MRR-AUTH-005, MRR-AUTH-006, MRR-AUTH-007, MRR-AUTH-008, MRR-AUTH-009]
```

## Execution evidence

Append W1, W2 and W3 records below this line; never rewrite authoring or prior
window evidence.

```yaml
- evidence_id: MRR-EXEC-W1
  window: MRR-W1
  result: ACCEPTED
  changed_files:
    - email_scraper/src/api-serializer.js
    - email_scraper/src/keyword-intelligence/api.js
    - email_scraper/src/keyword-intelligence/repository.js
    - email_scraper/src/server.js
    - email_scraper/test/fixtures/keyword-research-history-v1.json
    - email_scraper/test/keyword-research-history.test.js
    - email_scraper/test/keyword-intelligence-repository.test.js
  migrations: []
  focused_gate:
    command: node test/keyword-research-history.test.js (localhost escalated)
    outcome: 9 pass, 0 fail
    required_registered_executed: 7/7/7
    skips_duplicates_unexpected_unactivated: 0/0/0/0
    case_digest: fa497b08109ad34bfa8281e0b284d8304103dc7770051ca4c91e781cb317d6e8
  repository_gate:
    command: node test/keyword-intelligence-repository.test.js
    outcome: 12 pass, 0 fail
    inventory: 20 total, 10 short, 10 scale
    source_sha256: 58c2602f71f17cc2f567e87b0031195c40afb318229df359a6c7ba1609fce52a
  other_gates:
    db_generate: PASS
    db_validate: PASS
    api_serializer: PASS
    full_backend_suite: NONZERO only at the four W3-owned stale surfaces plus their dependent certificates; no W1 case or touched existing test failed
    check_secrets: PREEXISTING_OUT_OF_SCOPE finding at KEYWORD_INTELLIGENCE_KI_W8_SUBWINDOW_CHECKLIST.md:373; no W1 file named
  invariants:
    - exact ownerId and runs.none predicates in count and rows
    - one short transaction and two bounded reads, no writes/external calls
    - summary omits result/config/selection/provider/artifact material
    - existing full serializer stage result remains compatible
    - GET collection auth/query/no-store behavior proven
  diff_scope: PASS
  residuals: W3 owns pre-existing stale keyword assertions; root secret-scan finding is outside this feature and unchanged

- evidence_id: MRR-EXEC-W2
  window: MRR-W2
  result: ACCEPTED
  changed_files:
    - frontend/app/api/keyword-research/route.ts
    - frontend/app/globals.css
    - frontend/app/runs/page.tsx
    - frontend/components/run-history.tsx
    - frontend/lib/keyword-research-history.ts
    - frontend/test/design-system-shell.test.ts
    - frontend/test/my-runs-research-resume.test.ts
    - frontend/test/browser/my-runs-research-resume.mjs
  migrations: []
  unit_gate:
    command: node --experimental-strip-types test/my-runs-research-resume.test.ts
    outcome: 7 pass, 0 fail
    required_registered_executed: 6/6/6
    case_digest: 00d8ddc04ba5d46c5f0949eb3005b0a6f424bbe383f590f4b2f1de624672a4ff
  shell_regression_gate:
    command: node --experimental-strip-types test/design-system-shell.test.ts
    outcome: 5 pass, 0 fail
  frontend_gate:
    command: npm run check (local sandbox escalation for Turbopack process binding)
    outcome: PASS; lint 0 errors and 2 pre-existing unrelated warnings; tests 147 pass/0 fail/0 skip; production build exit 0
    build_routes: [/api/keyword-research, /keywords/[researchId], /runs]
    build_diagnostics: expected dynamic-cookie notices were emitted during static-page probing and did not fail the build
  browser_gate:
    command: node test/browser/my-runs-research-resume.mjs (loopback-only escalation)
    outcome: PASS
    required_registered_executed: 3/3/3
    skips_duplicates_unexpected_unactivated: 0/0/0/0
    case_digest: 6efa137b5959d58571244171d471c99fdb32d92441a1c7940f4caf0dfc149d59
    controls_falsified: [MRR-NC-04, MRR-NC-05]
  invariants:
    - authenticated My searches renders independent Keyword research and Discovery runs sections
    - exactly two initial read-only list requests use page=1 and pageSize=20
    - research links are fixed /keywords/{researchId}; existing run links remain /runs/{runId}
    - linked research is absent by the W1 contract while its resulting run remains listed
    - anonymous keyword-list BFF returns 401 without a backend call; authenticated proxy sends the trusted owner header
    - desktop and mobile emitted surfaces have no horizontal overflow and do not render internal IDs as visible copy
    - landing keyword auth tests remain green in the full frontend suite
  frozen_production_hashes:
    frontend/app/api/keyword-research/route.ts: d8c5494b81eefc249078fc9ba92bc25eb7ec3b9169c488b325eb4898cae6265f
    frontend/app/globals.css: 7df1646d8b4d834ebd6d5cf95f1f0bcf77f351e1b84d2ebfcb9e4314bc79f407
    frontend/app/runs/page.tsx: 24c146e8feefc30408c7932a57195a87cf6bc38ef4cc810cff26778d059ed181
    frontend/components/run-history.tsx: de99ecac6cb4935c445fc1b669e3174bb64b37be0e8b6565888d877776d6ce19
    frontend/lib/keyword-research-history.ts: dc2a48cc70fc2570050bdefe47484c04b7b79c250602baf5af801ea91460bf52
  diff_scope: PASS
  residuals: two pre-existing lint warnings remain in traffic-globe.tsx and keyword-intelligence-dashboard.mjs; neither is in this feature scope

- evidence_id: MRR-EXEC-W3
  window: MRR-W3
  result: ACCEPTED
  changed_files:
    - frontend/test/keyword-intelligence-api.test.ts
    - email_scraper/test/keyword-intelligence-api.test.js
    - email_scraper/test/keyword-intelligence-query-mapper.test.js
    - email_scraper/test/keyword-intelligence-worker-flow.test.js
  production_files: []
  migrations: []
  focused_gates:
    - command: node --experimental-strip-types test/keyword-intelligence-api.test.ts
      outcome: 18 pass, 0 fail
    - command: node test/keyword-intelligence-api.test.js (localhost escalation)
      outcome: 46 pass, 0 fail; W4 required/registered/executed 28/28/28 and R5 10/10/10
    - command: node test/keyword-intelligence-query-mapper.test.js
      outcome: 9 pass, 0 fail
    - command: node test/keyword-intelligence-worker-flow.test.js
      outcome: 37 pass, 0 fail
  full_gates:
    frontend_npm_test: 23 test files pass, 0 fail, 0 skip
    backend_npm_test: exit 0; every unguarded test passed and seven established database-opt-in integrations skipped
    diff_check: PASS in both nested repositories
  corrected_assertions:
    - monthly history accepts variable valid cardinality while malformed points still fail closed
    - deterministic test classifier supplies ordered product booleans and makes no OpenAI call
    - query prefixes depend on explicit product classification, not lane
    - free-text edits allow quotes/operators/no-prefix/unrelated text while empty/control/duplicate/oversize/set mismatch remain invalid
    - synthetic provider history uses keyword_info.monthly_searches, the current adapter-consumed path
  frozen_production_hash_comparison: PASS; W2 production hashes above and all W1 production files are unchanged by W3
  operations: zero OpenAI, DataForSEO, external-network, AWS, database, migration or production calls
  required_registered_executed: 4/4/4
  skips_duplicates_unexpected_unactivated: 0/0/0/0
  global_case_set:
    required_registered_executed: 23/23/23
    digest: 8f367c356ee531534825fb1e56f51656e4d45231ae2cd64ef7fe40a9286d116e
  test_file_hashes:
    frontend/test/keyword-intelligence-api.test.ts: 317f43586ab5f187c0ab9c23094de2a8b62b0b483bb51975db05ec445f04cb54
    email_scraper/test/keyword-intelligence-api.test.js: 1b1665431b18f015bbec72b080d998981c306e04e4254678b835aca722037854
    email_scraper/test/keyword-intelligence-query-mapper.test.js: ed0950aadd0ecc244bd162325dcc0f3bb93734097ad687d48146d735cdf6e80f
    email_scraper/test/keyword-intelligence-worker-flow.test.js: 4fe932d885336f7cf374b838f0273cc42d687b18aae97e10e5a4d5a4c1cf3c2f
  diff_scope: PASS
  residuals: root check:secrets retains the pre-existing out-of-scope finding at KEYWORD_INTELLIGENCE_KI_W8_SUBWINDOW_CHECKLIST.md:373; no feature file is named
```
