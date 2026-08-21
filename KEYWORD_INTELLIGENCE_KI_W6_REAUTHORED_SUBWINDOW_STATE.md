# KI-W6 Reauthored Sub-Window State (`S2`)

Mechanical state file. Only `KI-W6-WINDOW-AGENT` writes it, only inside the
`ASG-KI-W6-WA-02` coordination scope (the three `REAUTHORED` artifacts).
Parent artifacts (`A1`–`A8`) are never modified here. This file records no
evidence and no history; see `S3`
(`KEYWORD_INTELLIGENCE_KI_W6_REAUTHORED_SUBWINDOW_EVIDENCE.md`). Decomposition
authority lives in `S1`
(`KEYWORD_INTELLIGENCE_KI_W6_REAUTHORED_SUBWINDOW_CHECKLIST.md`).

```yaml
state_version: 19
parent_window_id: KI-W6
parent_assignment_id: ASG-KI-W6-WA-02
window_agent_identity: KI-W6-WINDOW-AGENT
parent_standard_path: PROJECT_AGNOSTIC_DECISION_COMPLETE_CHECKLIST_AUTHORING_STANDARD.md
parent_standard_revision: cda352017e75c0d11f6797d9fbe108b4365508cd38b0e92365cfb523ede32848
subwindow_standard_path: PROJECT_AGNOSTIC_WINDOW_AGENT_SUBWINDOW_AUTHORING_STANDARD.md
subwindow_standard_revision: 84e7590e74589f308c70dc9b0b67f7e9da395fafb1e5786202ecd1ca15be56e9
parent_contract_revision: 8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c
parent_decision_revision: 4bb1201594bc4a33bf868f19dd73c6777d046cdbb8ae70ef2cc8972dd6c342ad
parent_checklist_revision: a499afe117ee9b9dba07ab1a420d8a9bae824d6d5d7419374427f9cc0687fa63
parent_state_path: ACTIVE_EXECUTION_STATE.md
parent_state_revision: 7b4f43dd62b3262303921878d525908a09689a842cfcf5150d13c3427d772cd8
decomposition_path: KEYWORD_INTELLIGENCE_KI_W6_REAUTHORED_SUBWINDOW_CHECKLIST.md
decomposition_revision: b99633447c17163f6e883d71388b0200a345d2c0ced51252b8d03a8fba3b6b38
evidence_path: KEYWORD_INTELLIGENCE_KI_W6_REAUTHORED_SUBWINDOW_EVIDENCE.md
decomposition_status: READY
integration: 'I101 = CORRECTION_REQUIRED: V3 reached publication and proved the 300-row durable-result defect. State 153 resolves C104 commit 9eff81490d15f6c001bf30121133f538addb81bf as requester-owned provenance; R26 source/local evidence accepts C104, and C105 alone is now assigned.'
current_subwindow: KI-W6-C105
current_assignment_id: ASG-KI-W6-C105
assigned_agent: KI-W6-C105-LEAF-AGENT
subwindow_type: CORRECTION
authorized_write_file: email_scraper/test/keyword-intelligence-worker-flow.test.js
authorized_read_scope: [KEYWORD_INTELLIGENCE_PRODUCT_CONTRACT.md, KEYWORD_INTELLIGENCE_DECISION_LEDGER.md §DEC-KI-039, KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md §KI-W6 in-flight corrective amendment — final result shortlist projection, ACTIVE_EXECUTION_STATE.md, email_scraper/src/aws-pipeline/keyword-intelligence/service.js::aggregateMarket post-C104, email_scraper/src/aws-pipeline/keyword-intelligence/contracts.js, email_scraper/src/aws-pipeline/keyword-intelligence/keys.js]
authorized_actions: [modify aggregationScaffold support symbols and add SCN-KI-041 only, run C105-C1 and C105-C2 only, return one FILE-SUBWINDOW-EXECUTED certificate to the window agent, stop at AWAITING_WINDOW_REVIEW]
prohibited_actions: [window-agent implementation-file edits, any file other than email_scraper/test/keyword-intelligence-worker-flow.test.js, R3/R4 registration or assertion changes, production edits, existing case-ID membership/digest changes, database fixture timeout/retry change, frontend manifest package provider AWS production destructive action, C104 re-execution, I102 execution before independent C105 acceptance, any repository history repair reset revert amend or commit, parallel or out-of-order leaves, multi-file leaves, direct parent-leaf communication, leaf subdelegation, edits to A1-A8 or any parent artifact, reuse or citation of the invalidated state-108 KI-W6 decomposition, new or changed W6 coverage IDs or manifest membership, edits outside the seven-path KI-CL-21 parent scope, KI-W7 work, production database writes, commits/pushes, gate repetition outside approved invalidation and sandbox-recovery rules]
execution_environment_policy:
  sandbox_escalation_for_authorized_local_actions: true
  automatic_identical_recovery_after_proven_environment_invalidation: true
  recovery_limit_per_invalidated_execution: 1
  external_authority_expansion: false
may_start_successor: false
current_status: READY
accepted_subwindows: [KI-W6-S101, KI-W6-S102, KI-W6-S103, KI-W6-S104, KI-W6-S105, KI-W6-C104]
next_subwindow: KI-W6-C105  # only this assigned leaf may begin; I102 requires independent C105 acceptance
blocker: null
last_updated: 2026-08-21T13:52:46+05:30
```

## Sub-window registry

| ID | Type | File | Status | Assigned agent | Assignment ID |
|---|---|---|---|---|---|
| `KI-W6-S101` | FILE | `frontend/components/keyword-intelligence/research-dashboard.tsx` | ACCEPTED | `KI-W6-S101-LEAF-AGENT` | `ASG-KI-W6-S101` (executed; certificate + `EV-KI-W6-R15` in S3) |
| `KI-W6-S102` | FILE | `frontend/test/browser/keyword-intelligence-dashboard.mjs` | ACCEPTED | `KI-W6-S102-LEAF-AGENT` | `ASG-KI-W6-S102` (executed; certificate + `EV-KI-W6-R16` in S3) |
| `KI-W6-S103` | FILE | `email_scraper/test/helpers/keyword-intelligence-e2e-harness.js` | ACCEPTED | `KI-W6-S103-LEAF-AGENT` | `ASG-KI-W6-S103` (executed; certificate + `EV-KI-W6-R17` in S3) |
| `KI-W6-S104` | FILE | `email_scraper/test/fixtures/keyword-intelligence/ki-w6-enforcement-manifest-v1.json` | ACCEPTED | `KI-W6-S104-LEAF-AGENT` | `ASG-KI-W6-S104` (executed; certificate + `EV-KI-W6-R18` in S3) |
| `KI-W6-S105` | FILE | `frontend/test/browser/keyword-intelligence-e2e.mjs` | ACCEPTED | `KI-W6-S105-LEAF-AGENT` | `ASG-KI-W6-S105` (executed; certificate + `EV-KI-W6-R19` in S3) |
| `KI-W6-I101` | INTEGRATION_ASSESSMENT | (none; gates V1–V6) | CORRECTION_REQUIRED | `KI-W6-WINDOW-AGENT` | `ASG-KI-W6-WA-02` (V3 publication witness; superseded by I102) |
| `KI-W6-C104` | CORRECTION | `email_scraper/src/aws-pipeline/keyword-intelligence/service.js` | ACCEPTED_FOR_INTEGRATION | `KI-W6-C104-LEAF-AGENT` | `ASG-KI-W6-C104` (accepted via EV-KI-W6-R26 and state-153 requester-owned provenance disposition) |
| `KI-W6-C105` | CORRECTION | `email_scraper/test/keyword-intelligence-worker-flow.test.js` | READY | `KI-W6-C105-LEAF-AGENT` | `ASG-KI-W6-C105` |
| `KI-W6-I102` | INTEGRATION_ASSESSMENT | (none; CV1–CV6) | AWAITING_PARENT_DECOMPOSITION_REVIEW | RESERVED (`KI-W6-WINDOW-AGENT`) | NONE |

Counters: accepted initial file leaves 5/5; accepted corrective leaves 0/2;
integration assessments passed 0/2; corrective leaves accepted 1/2; only C105 is assigned. The accepted
five-path history remains `d28ae17864073639580d7650bb03c03474d5370a5034b632cf412e1e3cf3d0bb`.
The current authorized corrective plan is strictly sequential:
`C104 → window review → C105 → window review → I102`; parallel leaves are
prohibited.

Boundary: state 153 classifies backend `HEAD` commit
`9eff81490d15f6c001bf30121133f538addb81bf` as requester-owned provenance,
so the passing C104 review is accepted without rerun or history change. Only
C105 is assigned now; I102 remains unstarted until independent C105 acceptance.
KI-W7 remains prohibited.
