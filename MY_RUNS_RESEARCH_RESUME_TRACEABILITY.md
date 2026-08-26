# My Runs Research Resume — Traceability Index (A8)

Companions: A1 `MY_RUNS_RESEARCH_RESUME_PRODUCT_CONTRACT.md`; A2
`MY_RUNS_RESEARCH_RESUME_DISCOVERY_DOSSIER.md`; A3
`MY_RUNS_RESEARCH_RESUME_DECISION_LEDGER.md`; A4
`MY_RUNS_RESEARCH_RESUME_EXECUTION_CHECKLIST.md`; A5
`MY_RUNS_RESEARCH_RESUME_ACTIVE_STATE.md`; A6
`MY_RUNS_RESEARCH_RESUME_EVIDENCE.md`; A7
`MY_RUNS_RESEARCH_RESUME_CHANGELOG.md`.

| Requirement | Evidence | Decision | Tasks | Cases | Final assertion |
|---|---|---|---|---|---|
| `MRR-REQ-001` | SRC-001,004,005 | DEC-001,002 | W1-T1–T4, W2-T1–T3 | BE-01, FE-01, E2E-01 | Every unhanded owner research is visible. |
| `MRR-REQ-002` | SRC-005,007 | DEC-007 | W2-T3 | FE-02, E2E-02 | Click reaches exact dashboard route. |
| `MRR-REQ-003` | SRC-008,009 | DEC-003 | W1-T2 | BE-02, NC-03 | No result/config/selection payload. |
| `MRR-REQ-004` | SRC-001,010 | DEC-002,010 | W1-T1, W2-T3 | DB-02, FE-03, NC-02 | Handoff replaces research row with run row. |
| `MRR-REQ-005` | SRC-001-003 | DEC-005 | W1-T1,T4 | DB-01, BE-03, NC-01 | Foreign items and totals are absent. |
| `MRR-REQ-006` | SRC-007,013 | DEC-006,010 | W2-T2,T3 | FE-04, FE-05, NC-05 | Lists fail/page independently. |
| `MRR-REQ-007` | SRC-002,003,007 | DEC-001,011 | W2-T3 | FE-03, REG-01 | Run API and rows remain compatible. |
| `MRR-REQ-008` | SRC-002,008,010 | DEC-008 | all | BE-04, E2E-01 | Zero writes/SQS/provider/S3. |
| `MRR-REQ-009` | SRC-003,006 | DEC-004 | W1-T3,T4,W2-T1 | BE-05, FE-06 | Exact pagination rejection. |
| `MRR-REQ-010` | SRC-003,006 | DEC-005 | W1-T4,W2-T1 | BE-03, E2E-03 | Existing auth and owner propagation. |
| `MRR-REQ-011` | SRC-012,014 | DEC-009 | W1-T4,W2-T1 | BE-01, FE-01 | `no-store` personalized response. |
| `MRR-REQ-012` | SRC-007,013 | DEC-006,011 | W2-T3,T4 | FE-01–05,E2E-01 | Accessible responsive two-section UI. |
| `MRR-REQ-013` | SRC-001 | DEC-008 | all | REG-02 | Schema/migration hashes unchanged. |
| `MRR-REQ-014` | SRC-005,010,015 | DEC-008 | all | REG-01–03 | Dashboard/auth/worker behavior unchanged. |
| `MRR-REQ-015` | SRC-016-019 | DEC-012-015 | W3-T1–T4 | TEST-01–04 | Four stale test surfaces match current contracts with production unchanged. |

## Authoritative required coverage set

```text
MRR-BE-01
MRR-BE-02
MRR-BE-03
MRR-BE-04
MRR-BE-05
MRR-DB-01
MRR-DB-02
MRR-FE-01
MRR-FE-02
MRR-FE-03
MRR-FE-04
MRR-FE-05
MRR-FE-06
MRR-E2E-01
MRR-E2E-02
MRR-E2E-03
MRR-REG-01
MRR-REG-02
MRR-REG-03
MRR-TEST-01
MRR-TEST-02
MRR-TEST-03
MRR-TEST-04
```

The sorted unsigned-UTF-8 LF digest is mechanically recorded in A6 and A4.

## Negative-control mapping

| Control | Deliberate defect | Must fail |
|---|---|---|
| `MRR-NC-01` | Remove owner predicate from item/count query. | DB-01 owner/totals oracle |
| `MRR-NC-02` | Remove `runs.none` filter. | DB-02/FE-03 duplicate oracle |
| `MRR-NC-03` | Select or serialize completed `result`. | BE-02 payload/query projection oracle |
| `MRR-NC-04` | Use backend destination or `/runs/{researchId}`. | FE-02/E2E-02 fixed-link oracle |
| `MRR-NC-05` | Couple both fetches with one failing `Promise.all`. | FE-04 partial-success oracle |
| `MRR-NC-06` | Accept unknown response/query keys. | BE-05/FE-06 strictness oracle |
| `MRR-NC-07` | Remove one required case registration/activation. | coverage-set equality gate |
| `MRR-NC-08` | Restore the obsolete 15–102 monthly-history length rejection. | TEST-01 variable-length-history oracle |
| `MRR-NC-09` | Make mapping depend on legacy lane or let the classifier fake omit/reorder an item. | TEST-02 product/classifier oracle |
| `MRR-NC-10` | Put `monthly_searches` back at item top level. | TEST-04 worker-flow publication oracle |
