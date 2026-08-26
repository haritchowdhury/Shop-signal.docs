# My Runs Research Resume — Specification Changelog (A7)

Companions: A1 `MY_RUNS_RESEARCH_RESUME_PRODUCT_CONTRACT.md`; A2
`MY_RUNS_RESEARCH_RESUME_DISCOVERY_DOSSIER.md`; A3
`MY_RUNS_RESEARCH_RESUME_DECISION_LEDGER.md`; A4
`MY_RUNS_RESEARCH_RESUME_EXECUTION_CHECKLIST.md`; A5
`MY_RUNS_RESEARCH_RESUME_ACTIVE_STATE.md`; A6
`MY_RUNS_RESEARCH_RESUME_EVIDENCE.md`; A8
`MY_RUNS_RESEARCH_RESUME_TRACEABILITY.md`.

```yaml
- change_id: MRR-CHG-001
  timestamp: 2026-08-26T00:00:00+05:30
  trigger_evidence: [MRR-SRC-001, MRR-SRC-004, MRR-SRC-005, MRR-SRC-007]
  reason: User requested one My Runs resume surface for research and discovery runs.
  old_revision: NONE
  new_revision: INITIAL
  changed_requirements: [MRR-REQ-001, MRR-REQ-002, MRR-REQ-004]
  changed_decisions: [MRR-DEC-001, MRR-DEC-002, MRR-DEC-006]
  affected_windows: [MRR-W1, MRR-W2]
  invalidated_evidence: []
  compatibility_or_migration_effect: No schema migration; existing run contract preserved.
  authorization_effect: Plan authoring only; no execution assignment created.
  resumption_state: READY but UNASSIGNED after authoring certificate.
```

Future changes append rows. Never rewrite an assigned contract, reuse an ID, or
edit historical execution evidence.

