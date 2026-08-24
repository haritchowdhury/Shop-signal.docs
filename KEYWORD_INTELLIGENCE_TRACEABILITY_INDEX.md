# Keyword Intelligence Traceability Index (`A8`)

**Revision:** `KI-TR-25`

This is the sole authority for mechanical requirement/source/decision/task/test
closure. The other artifacts are `A1`
`KEYWORD_INTELLIGENCE_PRODUCT_CONTRACT.md`, `A2`
`KEYWORD_INTELLIGENCE_DISCOVERY_DOSSIER.md`, `A3`
`KEYWORD_INTELLIGENCE_DECISION_LEDGER.md`, `A4`
`KEYWORD_INTELLIGENCE_IMPLEMENTATION_CHECKLIST.md`, `A5`
`ACTIVE_EXECUTION_STATE.md`, `A6`
`KEYWORD_INTELLIGENCE_EXECUTION_EVIDENCE.md`, and `A7`
`KEYWORD_INTELLIGENCE_SPECIFICATION_CHANGELOG.md`.

An execution-evidence slot below is the stable verification checkbox that must
receive a concrete A6 evidence ID when executed. It is not a claim that the
unchecked scenario has run.

For compact tables, `/` repeats the full prefix immediately to its left
(`REQ-KI-003/004` means `REQ-KI-003` and `REQ-KI-004`), and an en-dash range is
inclusive. These two expansions are the mechanical normalization applied before
set comparison.

## 1. Requirement and invariant closure

| Contract ID | Observed evidence | Locked decision | Implementing task | Verification/oracle | Execution-evidence slot | Final review |
|---|---|---|---|---|---|---|
| `REQ-KI-001` | `SRC-KI-005/006` | `DEC-KI-003/019/033` | `KI-W2-T2`, `KI-W4-T1/T3/T4`, `KI-W5-T1` | `SCN-KI-003`; `W4-A01`, `W4-S01/S02` | `KI-W4-V2/V6` | `KI-FR-2/4` |
| `REQ-KI-002` | `SRC-KI-005/016`; `EV-KI-A-031`; `EV-KI-W3-04/05/07`; `EV-KI-R2-05`; `EV-KI-R3-02` | `DEC-KI-001/018/022/026`–`033` | `KI-W1-T2`, `KI-R1-T1`, `KI-R2-T1`, `KI-R2-RT2`, `KI-W3-T2`, `KI-W3-RT1`–`RT4`, `KI-R3-T1`–`T4`, `KI-R4-T1/T3/T4`, `KI-W4-T1/T3/T4`, `KI-W5-T1` | `SCN-KI-001/012/017/020/022`–`035`; `W4-A01`–`A03`, `W4-S02/S03` | `KI-R1-V1/V3`, `KI-R2-V1`, `KI-R2-RV1`, `KI-R4-V1`–`V6`, `KI-W4-V2/V6`, `KI-W5-V1` | `KI-FR-2/4` |
| `REQ-KI-003` | `SRC-KI-006`; `EV-KI-W3-05/07` | `DEC-KI-004/006/030/031` | `KI-W2-T1`, `KI-W3-T2`, `KI-W3-RT3`, `KI-R3-T4` | `SCN-KI-005/026/031` | `KI-R3-V1` | `KI-FR-2/4` |
| `REQ-KI-004` | `SRC-KI-006/008/009`; `EV-KI-W3-05/07` | `DEC-KI-005/006/010/011/012/030/031` | `KI-W2-T1`, `KI-W3-T2`, `KI-W3-RT1`–`RT3`, `KI-R3-T4` | `SCN-KI-004/005/010/024`–`026`, `031` | `KI-W2-V1`, `KI-R3-V1` | `KI-FR-2/5` |
| `REQ-KI-005` | `SRC-KI-007/012`; `EV-KI-A-031`; `EV-KI-W3-05/07`; `EV-KI-R3-02` | `DEC-KI-012/018/021/026/027/030`–`033` | `KI-W1-T1/T2`, `KI-R1-T1`, `KI-W3-T2`, `KI-W3-RT2/RT3`, `KI-R3-T2`–`T4`, `KI-R4-T1/T3/T4`, `KI-W4-T1/T4` | `SCN-KI-001/009/020/025/026/029`–`035`; `W4-A03`, `W4-S03` | `KI-W1-V1`, `KI-R1-V1`, `KI-R4-V1`–`V3/V6`, `KI-W4-V2/V6` | `KI-FR-1/4` |
| `REQ-KI-006` | `SRC-KI-005/010` | `DEC-KI-013` | `KI-W2-T2`, `KI-W5-T2` | `SCN-KI-011/016` | `KI-W2-V1`, `KI-W5-V1` | `KI-FR-2/4` |
| `REQ-KI-007` | `SRC-KI-010/013` | `DEC-KI-014/019/033` | `KI-W2-T2`, `KI-W4-T1/T3/T4`, `KI-W5-T2` | `SCN-KI-008/011/017`; `W4-A04`, `W4-S04` | `KI-W4-V2/V6`, `KI-W5-V1` | `KI-FR-2/4` |
| `REQ-KI-008` | `SRC-KI-005` | `DEC-KI-013/015/024/033` | `KI-W2-T2`, `KI-W4-T1/T3/T4`, `KI-W5-T2` | `SCN-KI-011/018`; `W4-A04`, `W4-S04` | `KI-W2-V3`, `KI-W4-V2/V6`, `KI-W6-V3` | `KI-FR-2/4` |
| `REQ-KI-009` | `SRC-KI-008/010` | `DEC-KI-015/033` | `KI-W2-T2`, `KI-W4-T1/T3/T4`, `KI-W5-T2` | `SCN-KI-011`; `W4-A04`, `W4-S04` | `KI-W2-V1`, `KI-W4-V2/V6` | `KI-FR-2/4` |
| `REQ-KI-010` | `SRC-KI-005/013` | `DEC-KI-016/017/033` | `KI-W2-T2`, `KI-W4-T2/T3/T4` | `SCN-KI-014/015`; `W4-Q01`–`Q04`, `W4-D01` | `KI-W4-V2/V3/V6` | `KI-FR-2/4` |
| `REQ-KI-011` | `SRC-KI-005/008` | `DEC-KI-016/033` | `KI-W2-T2`, `KI-W4-T2/T3/T4` | `SCN-KI-014`; `W4-Q01`, `W4-D01` | `KI-W4-V2/V3/V6` | `KI-FR-2/4` |
| `REQ-KI-012` | `SRC-KI-013/014/039` | `DEC-KI-016/033/038` | `KI-W4-T3/T4`, `KI-W6-T3/T5` | `SCN-KI-014/018`; `W4-Q05/Q06`; `W6-FLOW-09`–`12` | `KI-W4-V2/V5/V6`, `KI-W6-V3/V5` | `KI-FR-2/4` |
| `REQ-KI-013` | `SRC-KI-013` | `DEC-KI-016/017/033` | `KI-W4-T3/T4` | `SCN-KI-014`; `W4-Q02`–`Q08` | `KI-W4-V2/V5/V6` | `KI-FR-2/4` |
| `REQ-KI-014` | `SRC-KI-010/018` | `DEC-KI-023` | `KI-W5-T1/T2/T3` | `SCN-KI-016/017` | `KI-W5-V1/V2` | `KI-FR-2/4` |
| `REQ-KI-015` | `SRC-KI-012/013`; `EV-KI-A-031` | `DEC-KI-017/021/026/033` | `KI-W1-T1/T2`, `KI-R1-T1`, `KI-W4-T1`–`T4` | `SCN-KI-008/015/020`; `W4-A05`, `W4-S05`, `W4-D01`–`D04` | `KI-R1-V1`, `KI-W4-V2/V3/V6` | `KI-FR-2/4` |
| `REQ-KI-016` | `SRC-KI-005/012`; `EV-KI-A-031` | `DEC-KI-014/017/026/033` | `KI-W1-T1/T2`, `KI-R1-T1`, `KI-W4-T1`–`T4` | `SCN-KI-015/020`; `W4-A05`, `W4-S05`, `W4-D01/D05` | `KI-R1-V1`, `KI-W4-V2/V3/V6` | `KI-FR-2/4` |
| `REQ-KI-017` | `SRC-KI-007/012`; `EV-KI-A-031` | `DEC-KI-009/017/021/026/033` | `KI-W1-T1/T2`, `KI-R1-T1`, `KI-W4-T1/T2/T4` | `SCN-KI-009/015/020`; `W4-A03`, `W4-D05` | `KI-W1-V1`, `KI-R1-V1`, `KI-W4-V2/V3/V6` | `KI-FR-1/4` |
| `REQ-KI-018` | `SRC-KI-008/010` | `DEC-KI-012/019/023/033` | `KI-W2-T1`, `KI-W4-T1/T3/T4`, `KI-W5-T2` | `SCN-KI-010/016`; `W4-A06/A07`, `W4-S06` | `KI-W4-V2/V5/V6`, `KI-W5-V1` | `KI-FR-2/4` |
| `REQ-KI-019` | `SRC-KI-012/013/040` | `DEC-KI-016/021/033/038` | `KI-W1-T1`, `KI-W4-T1`–`T4`, `KI-W6-T3/T5` | `SCN-KI-002/014/018`; `W4-S01/S06`, `W4-Q07`, `W4-D06`, `W4-C06`; `W6-FLOW-13`, `W6-CONF-06` | `KI-W4-V2`–`V6`, `KI-W6-V3/V5/V6` | `KI-FR-1/5` |
| `REQ-KI-020` | `SRC-KI-007/011/040` | `DEC-KI-009/012/038` | `KI-W2-T1`, `KI-W6-T3/T5` | `SCN-KI-010/018`; `W6-CONF-06` | `KI-W2-V4`, `KI-W6-V3/V5/V6` | `KI-FR-1/5` |
| `REQ-KI-021` | `SRC-KI-019/020/021/022`; `EV-KI-W3-05/07`; `EV-KI-R3-02` | `DEC-KI-004/007/012/030`–`033` | `KI-W2-T1`, `KI-W3-T1/T2`, `KI-W3-RT1/RT2`, `KI-R3-T1/T2`, `KI-R4-T2/T3`, `KI-W4-T1/T4` | `SCN-KI-004/005/009/024/025/028/029/033`–`035`; `W4-A08` | `KI-R4-V2/V5/V6`, `KI-W4-V2/V6` | `KI-FR-3/5` |
| `REQ-KI-022` | `SRC-KI-028`–`032`; `EV-KI-A-031`; `EV-KI-W3-05/07`; `EV-KI-R3-02` | `DEC-KI-004/009/025/026/030`–`032`; closed `GATE-KI-003` | `KI-W1-T1/T2`, `KI-R1-T1`, `KI-W3-T1`, `KI-W3-RT1/RT2`, `KI-R3-T1`–`T3`, `KI-R4-T1`–`T4` | `SCN-KI-006/013/020/024/025/028`–`035` | `KI-W1-V1`, `KI-R1-V1`, `KI-R4-V1`–`V6` | `KI-FR-1/3/5` |
| `REQ-KI-023` | `SRC-KI-006/008/030`; `EV-KI-A-031`; `EV-KI-W3-05/07`; `EV-KI-R3-02` | `DEC-KI-004/005/024/026/027/030`–`032` | `KI-W2-T1`, `KI-R1-T1`, `KI-W3-T2`, `KI-W3-RT1`–`RT4`, `KI-R3-T1`–`T4`, `KI-R4-T1`–`T4` | `SCN-KI-001/004/013/020/024`–`035` | `KI-W2-V1/V3`, `KI-R1-V1`, `KI-R4-V1`–`V6` | `KI-FR-2/4/5` |
| `REQ-KI-024` | `SRC-KI-006/008/030/032`; `EV-KI-A-031`; `EV-KI-W3-05/07`; `EV-KI-R3-02` | `DEC-KI-004/006/010/024/026/027/030`–`032` | `KI-W2-T1`, `KI-R1-T1`, `KI-W3-T2`, `KI-W3-RT1`–`RT4`, `KI-R3-T4`, `KI-R4-T3/T4`, `KI-W5-T2/T3` | `SCN-KI-001/005/013/018/020/024`–`035` | `KI-W2-V1/V3`, `KI-R1-V1`, `KI-R4-V1`–`V6`, `KI-W5-V3`, `KI-W6-V3` | `KI-FR-2/4/5` |
| `INV-KI-001` | `SRC-KI-001/007/012` | `DEC-KI-001/021` | `KI-W1-T1/T2` | `SCN-KI-002` | `KI-W1-V1/V4` | `KI-FR-1/5` |
| `INV-KI-002` | `SRC-KI-001/016`; `EV-KI-A-031`; `EV-KI-W3-05/07`; `EV-KI-R3-02` | `DEC-KI-020/026/027/030`–`032` | `KI-R1-T1`, `KI-W3-T2`, `KI-W3-RT1/RT4`, `KI-R3-T1/T4`, `KI-R4-T2/T3`, `KI-W7-T1` | `SCN-KI-006/019/020/024/027/028/032`–`035` | `KI-R1-V3/V4`, `KI-R4-V1/V2/V4`–`V6`, `KI-W8-V4` | `KI-FR-2/3` |
| `INV-KI-003` | `SRC-KI-015/016/039` | `DEC-KI-001/019/033/038` | `KI-W4-T1/T3/T4`, `KI-W6-T3/T5` | `SCN-KI-003/018`; `W4-A01/A02`, `W4-S02`; `W6-FLOW-01` | `KI-W4-V2/V6`, `KI-W6-V3/V5` | `KI-FR-2/4` |
| `INV-KI-004` | `SRC-KI-006/016`; `EV-KI-A-031`; `EV-KI-W3-05/07`; `EV-KI-R3-02` | `DEC-KI-005/006/018/026/030`–`032` | `KI-R1-T1`, `KI-W3-T2`, `KI-W3-RT2/RT3`, `KI-R3-T2`–`T4`, `KI-R4-T1/T3/T4` | `SCN-KI-001/013/020/025/026/029`–`035` | `KI-R1-V1`, `KI-R4-V1`–`V6` | `KI-FR-2/4` |
| `INV-KI-005` | `SRC-KI-001/016`; `EV-KI-A-031`; `EV-KI-W3-04/05/07`; `EV-KI-R2-05`; `EV-KI-R3-02` | `DEC-KI-018/020/026`–`032` | `KI-W1-T2`, `KI-R1-T1`, `KI-R2-T1`, `KI-R2-RT2`, `KI-W3-T2`, `KI-W3-RT2/RT3`, `KI-R3-T2`–`T4`, `KI-R4-T1/T3/T4` | `SCN-KI-001/012/020/022`–`035` | `KI-R1-V1`, `KI-R2-V1`, `KI-R2-RV1`, `KI-R4-V1`–`V6` | `KI-FR-2/4` |
| `INV-KI-006` | `SRC-KI-016`; `EV-KI-A-031`; `EV-KI-W3-04/05/07`; `EV-KI-R2-05`; `EV-KI-R3-02` | `DEC-KI-018/022/026/028`–`032` | `KI-W1-T2`, `KI-R1-T1`, `KI-R2-T1`, `KI-R2-RT2`, `KI-W3-T2`, `KI-W3-RT2/RT3`, `KI-R3-T2`–`T4`, `KI-R4-T1/T3/T4` | `SCN-KI-012/020/022`–`035` | `KI-W1-V1`, `KI-R1-V1`, `KI-R2-V1`, `KI-R2-RV1`, `KI-R4-V1`–`V6` | `KI-FR-2/4` |
| `INV-KI-007` | `SRC-KI-016`; `EV-KI-A-031`; `EV-KI-W3-04/05/07`; `EV-KI-R2-05`; `EV-KI-R3-02` | `DEC-KI-020/022/026`–`032` | `KI-R1-T1`, `KI-R2-T1`, `KI-R2-RT2`, `KI-W3-T2`, `KI-W3-RT1`–`RT3`, `KI-R3-T1`–`T4`, `KI-R4-T1/T3/T4` | `SCN-KI-006/012/020/022`–`035` | `KI-R1-V1/V3`, `KI-R2-V1`, `KI-R2-RV1`, `KI-R4-V1`–`V6` | `KI-FR-2/4` |
| `INV-KI-008` | `SRC-KI-012/016`; `EV-KI-A-031`; `EV-KI-W3-05/07`; `EV-KI-R3-02` | `DEC-KI-007/009/018/026/030`–`032` | `KI-W1-T2`, `KI-R1-T1`, `KI-W3-T1/T2`, `KI-W3-RT1/RT2`, `KI-R3-T1`–`T3`, `KI-R4-T1`–`T4` | `SCN-KI-006/020/024/025/028`–`035` | `KI-R1-V1`, `KI-R4-V1`–`V6` | `KI-FR-2/5` |
| `INV-KI-009` | `SRC-KI-019/022`; `EV-KI-W3-05/07`; `EV-KI-R3-02` | `DEC-KI-009/012/020/030`–`032` | `KI-W2-T1`, `KI-W3-T1/T2`, `KI-W3-RT1/RT2`, `KI-R3-T1`–`T3`, `KI-R4-T1`–`T3` | `SCN-KI-004/006/009/024/025/028`–`035` | `KI-R4-V1/V2/V5/V6` | `KI-FR-1/5` |
| `INV-KI-010` | `SRC-KI-014/039` | `DEC-KI-016/024/033/038` | `KI-W2-T2`, `KI-W4-T2/T3/T4`, `KI-W6-T3/T5` | `SCN-KI-013/018`; `W4-Q05`, `W4-D01`; `W6-FLOW-10`–`12` | `KI-W4-V3/V5/V6`, `KI-W6-V3/V5` | `KI-FR-2/4` |
| `INV-KI-011` | `SRC-KI-001/014/039` | `DEC-KI-016/017/033/038` | `KI-W4-T2/T3/T4`, `KI-W6-T3/T5` | `SCN-KI-018`; `W4-D01/D05`; `W6-FLOW-08`–`13` | `KI-W4-V3/V6`, `KI-W6-V3/V5` | `KI-FR-2/5` |
| `INV-KI-012` | `SRC-KI-001/006`; `EV-KI-W3-05/07` | `DEC-KI-008/025/030/031` | `KI-W3-T1/T2`, `KI-W3-RT1`, `KI-R3-T1/T2`, `KI-W7-T1` | `SCN-KI-007/019/025/028/029` | `KI-R3-V1/V4`, `KI-W7-V3` | `KI-FR-2/3` |
| `INV-KI-013` | `SRC-KI-012/015` | `DEC-KI-002/009/019/033` | `KI-W1-T2`, `KI-W4-T1/T3/T4` | `SCN-KI-008/009`; `W4-A03`, `W4-S01/S03/S04`, `W4-D03` | `KI-W4-V2/V3/V5/V6` | `KI-FR-2/4` |
| `INV-KI-014` | `SRC-KI-016`; `EV-KI-A-031` | `DEC-KI-012/018/020/026/033` | `KI-R1-T1`, `KI-W3-T2`, `KI-W4-T1/T4` | `SCN-KI-001/009/020`; `W4-A03` | `KI-R1-V1`, `KI-W3-V1`, `KI-W4-V2/V6` | `KI-FR-2/4` |
| `INV-KI-015` | `SRC-KI-012/013` | `DEC-KI-002/016/017/033` | `KI-W2-T2`, `KI-W4-T2/T3/T4` | `SCN-KI-014/015`; `W4-Q02/Q04`, `W4-D01/D05` | `KI-W4-V2/V3/V6` | `KI-FR-2/4` |

## 2. Exclusion and authorization closure

| Contract ID | Evidence/decision | Enforced by | Falsification/oracle | Final review |
|---|---|---|---|---|
| `EXC-KI-001` | `SRC-KI-001/005/040`; `DEC-KI-001/038` | all scopes; `KI-W6-T5` | `SCN-KI-018`, `W6-CONF-06`, `W6-NC-13` | `KI-FR-1/5` |
| `EXC-KI-002` | `SRC-KI-006/008`; `DEC-KI-010/011` | `KI-W2-T1` | `SCN-KI-010` golden perturbation | `KI-FR-2/5` |
| `EXC-KI-003` | `SRC-KI-005/013`; `DEC-KI-016/033` | `KI-W2-T2`, `KI-W4-T2/T3/T4` | `SCN-KI-014`; `W4-Q01/Q02/Q07` mixed lanes/non-product branch | `KI-FR-2/5` |
| `EXC-KI-004` | `SRC-KI-005/010`; `DEC-KI-013/015` | `KI-W2-T2`, `KI-W5-T2` | `SCN-KI-011` | `KI-FR-2/5` |
| `EXC-KI-005` | `SRC-KI-001/013/015`; `DEC-KI-016/023/033` | `KI-W4-T2/T3/T4`, `KI-W5-T1` | `W4-Q07`, `W4-S06`, `W4-D06`; `SCN-KI-018` | `KI-FR-1/5` |
| `EXC-KI-006` | `SRC-KI-019`–`022`; `DEC-KI-009/012/030/031` | `KI-W2-T1`, `KI-W3-T1/T2`, `KI-W3-RT1`–`RT3`, `KI-R3-T1`–`T4` | `SCN-KI-024`–`032`; privacy/secret scans | `KI-FR-1/5` |
| `EXC-KI-007` | `SRC-KI-005`; `DEC-KI-018/019/030/031/033` | `KI-W3-T2`, `KI-W3-RT2/RT3`, `KI-R3-T2`–`T4`, `KI-W4-T1/T3/T4` | `SCN-KI-025/026/029`–`032`; `W4-S01`–`S06` route/state set equality | `KI-FR-1/5` |
| `EXC-KI-008` | `SRC-KI-001/002/025`; `DEC-KI-025` | A5, W7/W8 scopes | `SCN-KI-019` approval/preflight | `KI-FR-3/5` |
| `AUTH-KI-001` | `SRC-KI-002/004`; `DEC-KI-025` | current DRAFT status | no implementation checkbox checked | `KI-FR-1` |
| `AUTH-KI-002` | `SRC-KI-002`; `DEC-KI-025` | `ACTIVE_EXECUTION_STATE.md` | hash/status lint | `KI-FR-1/4` |
| `AUTH-KI-003` | `SRC-KI-004`; `DEC-KI-025` | every W-P1 | mismatched assignment stops | `KI-FR-1/4` |
| `AUTH-KI-004` | `SRC-KI-001`; A3 D2A | `KI-W1-P3`, `KI-W6-P3` | wrong/public DB fails closed | `KI-FR-1/2` |
| `AUTH-KI-005` | `SRC-KI-001/025`; `DEC-KI-025` | W7/W8 gates/scopes | `SCN-KI-019` | `KI-FR-3/5` |
| `AUTH-KI-006` | `SRC-KI-003`; `DEC-KI-023/025` | every dirty-scope precondition/handoff | diff set equality | `KI-FR-1/4` |
| `AUTH-KI-007` | `SRC-KI-028`–`032`; `DEC-KI-009/025` | closed `GATE-KI-003`, W1/W3 preconditions | exact `$0.492`/`$2.46` and over-budget zero-call oracles in `SCN-KI-006/013` | `KI-FR-1/3/5` |

## 3. Source-to-target ownership closure

| Discovered source family | Evidence | Exactly one target owner | Required assertion |
|---|---|---|---|
| config/market constants | `SRC-KI-006` | `KI-W2-T1` | exact v1 snapshot/parity |
| SQLite cache semantics | `SRC-KI-007` | `KI-W1-T2`, then `KI-W3-T1` at distinct symbols | same key/TTL; normalized Postgres only |
| Python normalize/intent/dedup/cluster/score | `SRC-KI-008` | `KI-W2-T1` | `DEC-KI-011` parity |
| Python orchestration/provider slicing | `SRC-KI-006/008/030/032` | `KI-W3-T1/T2` | intentional US expansion/anchor-screen/top-200 topology; bounded durable manifests/calls |
| Python output writers | `SRC-KI-008` | `KI-W2-T1` | exact JSON/CSV minus raw_ref/filesystem |
| standalone dashboard DOM/CSS/functions | `SRC-KI-010` | `KI-W5-T2/T3` at distinct surface/visual symbols | UI inventory set equality |
| historical provider payloads | `SRC-KI-019`–`022` | `KI-W3-T1` | one strict observed shape; no alias/raw body |
| provider cost evidence and approved policy | `SRC-KI-028`–`032` | `KI-W1-T2`/`KI-W3-T1` under closed `GATE-KI-003` | exact per-attempt reservation, `$0.492` first pass, `$2.46` five-attempt exposure, `$3` zero-call denial proof |
| Prisma Run/RunQuery | `SRC-KI-012` | `KI-W1-T1` schema; `KI-W4-T2` behavior | nullable legacy-safe lineage/atomic handoff |
| accepted W2 cluster/selection/API-export domain surface | `SRC-KI-005/008/010` | `KI-W4-T1` at the exact additive symbols in its task block | canonical manual/edit reclassification, owner projection, filtered export, and unchanged W2 behavior |
| existing product-only query path | `SRC-KI-013` | `KI-W4-T3` additive research discriminator branch | legacy byte/behavior regression |
| existing Google probe | `SRC-KI-013/014` | `KI-W4-T3` caller branch only | one probe/query; saved evidence unchanged |
| backend auth/routes/serializer | `SRC-KI-015` | `KI-W4-T1` serializers/service and `KI-W4-T3` exact route/query-review symbols | owner/API status contracts and unchanged legacy serialized key sets |
| W4 enforcement and transaction-test surface | `DEC-KI-033`; current Node and isolated-Postgres harnesses | `KI-W4-T4` exact three fixture/test files only | literal 34-ID required=registered=executed equality, 18 falsified controls, one disposable schema/run |
| AWS adapters/contracts/recovery | `SRC-KI-016` | `KI-W3-T2` new keyword modules | no change to existing handlers |
| unaccepted W3 adapter/service/dispatcher/build sources | `EV-KI-W3-04/05/06/07`, the KI-R3-P2 hashes, and backend `37a0e020...` | `KI-W3-RT1`–`RT4` historical source; `KI-R3-T1`–`T4` exact corrective symbols/tests | `DEC-KI-030/031`; literal 101-ID manifest; `SCN-KI-024`–`032`; no repository/schema/handler/recovery/config/package/build-script edit |
| rejected KI-R3 source and enforcement surface | `EV-KI-R3-01/02`, backend `077213cc...`, exact eight-file KI-R4 set/digest | `KI-R4-T1`–`T4` through parent-reviewed sequential single-file leaves; window agent owns only S1/S2/S3 | `DEC-KI-032`; corrected `SCN-KI-028`–`032`; new `SCN-KI-033`–`035`; cumulative 116-ID equality; no adapter-source/repository/schema/API/frontend/package/AWS edit |
| accepted W1 repository gaps at the W3 boundary | `EV-KI-A-031` | `KI-R1-T1` exact repository symbols only | `DEC-KI-026` interface/set/transaction equality and `SCN-KI-020`; no schema or W3 write |
| frontend proxy/types/client | `SRC-KI-015` | `KI-W5-T1` additive symbols | strict same-origin boundary |
| frontend browser harness | `SRC-KI-018/038/039` | `KI-W5-T3`; `KI-W6-T2/T5` at distinct accepted-oracle/new-causal-harness paths | W5 presentation evidence remains; R5-FIN-01 destination alone is superseded; W6 uses real Next/Chrome with no application-API interception |
| backend status URL and frontend run-workspace routing | `SRC-KI-038` | `KI-W6-T1/T2` at the two dashboard expressions and one R5-FIN-01 oracle only | API `statusUrl` remains `/api/runs/<id>`; both browser success paths use encoded `handoff.run.runId` and reject status-URL navigation |
| local causal auth/provider/cloud seams | `SRC-KI-039` | `KI-W6-T3/T5` | one connected emitted browser→Next→auth→proxy→backend→Prisma/worker→probe→downstream trace under the exact substitute limits |
| invalidated W6 decomposition and revised authoring standards | `SRC-KI-040` | no implementation owner; fresh W6 S1/S2/S3 owned only by a future assigned W6 window agent | old artifacts/IDs/certificates are never reused; parent-reviewed one-file decomposition precedes execution |
| SAM/build entry list | `SRC-KI-016` | `KI-W7-T1` additive symbols | exact topology/artifact inventory |
| unrelated dirty root/frontend members | `SRC-KI-003` | no implementation owner (`PARKED`) | byte-identical/diff exclusion |

## 4. Corrective-finding closure

| Finding from `EV-KI-A-031` | Locked resolution | Implementation owner | Acceptance oracle | W3 consumption rule |
|---|---|---|---|---|
| no durable retry scheduling primitive | `DEC-KI-026` `scheduleRetry` plus corrected attempt lifecycle | `KI-R1-T1` | `SCN-KI-020` known-retry crash/early/due schedule | W3 calls the method; it does not edit repository or invent task mutation |
| no attempt-free throttle lease release | `DEC-KI-026` `deferTask` | `KI-R1-T1` | `SCN-KI-020` throttle delay/count schedule | W3 calls the method before `recordAttempt` and makes zero HTTP calls |
| final result and default selection are split/owner-coupled | `DEC-KI-026` fenced `publishResearchResult` transaction | `KI-R1-T1` | `SCN-KI-020` rollback/stale-token/replay schedules | W3 supplies calculated result/selection to one method |
| runtime queue injection was unnamed | `DEC-KI-027` one URL/property/environment mapping | `KI-W3-T2` consumer; `KI-W7-T1` config/deployment owner | W3 mocked dispatch tests; W7 strict config/topology tests | W3 reads only `runtime.config.awsPipelineKeywordResearchQueueUrl` |
| W1/W2 item identities differ | `DEC-KI-002`/`026` six-byte BLAKE2s formula | `KI-R1-T1` | `SCN-KI-020` calculated/manual equality | W3 and W4 consume one canonical ID |
| worker context/recovery data is incomplete and lost initialize is invisible | `DEC-KI-026` exact context plus initialize/task/check recovery unions | `KI-R1-T1` | `KI-R1-V3`, `SCN-KI-020` message reconstruction without lookup | W3 uses returned projections only |
| aggregator can claim before terminal readiness | `DEC-KI-026` `not_ready` and ready/expired predicates | `KI-R1-T1` | `SCN-KI-020` early/race/expiry schedule | W3 treats `not_ready` as zero-work acknowledgement/recovery state |
| manifest publication is split and artifact time is unstable | `DEC-KI-026` atomic publications; `DEC-KI-027` createdAt mapping | `KI-R1-T1` repository; `KI-W3-T2` artifact writer | `SCN-KI-020` rollback and byte-stable replay | W3 writes S3 first, then calls the one matching publication transaction |
| logical cache version label conflicts with accepted integer column | `DEC-KI-009` maps label to persisted integer `1`; `DEC-KI-026` atomic settle+cache | `KI-R1-T1` | `SCN-KI-020` settle/cache equality and rollback | W3 supplies `cacheEntry.contractVersion:1` only on strict success |
| parent review found attempt-five replay, later-clock retry replay, and zero-row final-publication schedules absent from the first KI-R1 suite | already-locked `DEC-KI-007`/`026`; reopen unaccepted KI-R1 without a new window | `KI-R1-RT1` | `SCN-KI-021` exact replay clocks, row counts, rollback, and partial-state negative control | reopened checks passed; `EV-KI-R1-13` accepts KI-R1 and A5 state 85 assigns W3 |
| parent review of initial W3 found no aggregation heartbeat plus expired-renewal and non-live terminal predicates in the accepted repository | `DEC-KI-028` exact one-update heartbeat unions, exact-expiry reclaim, and live terminal predicates | `KI-R2-T1` in seven named repository methods only | `SCN-KI-022` two-owner clocks, row equality, completed replay, and three independent negative controls | W3 stays read-only during KI-R2; after parent acceptance, reopened W3 calls both heartbeats and proves the full `SCN-KI-012` monitor schedule |
| parent review of KI-R2 second-attempt evidence found the original exact task-expiry renewal and stale aggregation heartbeat after B reclaim were described but not executed | `DEC-KI-028` behavior unchanged; `DEC-KI-029` narrows verification to one frozen pre-handoff focused gate | `KI-R2-RT2` integration-test symbols only; repository source is read-only | `SCN-KI-023` exact equality schedules plus unchanged `SCN-KI-022 V5` representative negative control | satisfied by `EV-KI-R2-06/07`; W3 consumes the accepted hashes without repeating that database suite |
| accepted KI-R2 leaves eight W3-owned gaps: stale settlement continuation, undecodable known-status retry, wrong succeeded-recovery cost, inactive task/aggregation monitoring, discarded failStage fence, immediate retry dispatch, overview string cap 100, and shared/stale build cleanup | `DEC-KI-030` exact result matrix, durable recovery reconstruction, monitor lifecycles, delayed dispatcher, 160-code-point bound, and isolated reproducible build | `KI-W3-RT1`–`RT4` at the exact F1 symbols | `SCN-KI-024`–`027`, one final focused DB gate, one frozen build/regression/secret gate | W3 implements all eight in this one reopened window; success hands directly to W4, while any failed oracle remains a W3 failure rather than an accepted corrective branch |
| second W3 handoff passed broad named scenarios while active settlement lost cost, terminal checks escaped nonterminal fences, recovery bypassed monitor/terminal ordering, known terminal failures could be retried, null dispatcher options were accepted, and helper inventory was false | `DEC-KI-031` literal result/operation/recovery/dispatcher/helper rules and 101-ID executable manifest | unique `KI-R3-T1`–`T4` at four production symbols plus additive manifest/tests | `SCN-KI-028`–`032`, exact group/global set equality, four injected mutation controls, one focused DB gate, unchanged `SCN-KI-027` build proof | `EV-KI-W3-06` remains historical and unaccepted; KI-R3 success establishes cumulative W3 acceptance and only the parent may then assign W4 |
| KI-R3 handoff retained unequal failed-attempt identity, incomplete own-key validation, live-worktree conformance, regex-only hashes, unnamed five-schema DB cases, and vacuous mutation controls | `DEC-KI-032` locks pre-classification identity, `Reflect.ownKeys`, fixed-revision conformance, exact full digests, captured-evidence mutations, one shared schema, and recursive window-agent authority | unique `KI-R4-T1`–`T4`; its window agent decomposes the exact eight-file set into sequential single-file leaves and personally assesses integration | `SCN-KI-033`–`035`, corrected `SCN-KI-028`–`032`, 116-case cumulative equality, four exact falsification controls, one focused DB gate, keyword package and frozen regression gates | `EV-KI-R3-01` remains historical and unaccepted; only parent acceptance of the window-agent KI-R4 handoff may establish cumulative W3 acceptance and assign W4 |

## 5. Planned-member reverse closure

Every new model is owned by `KI-W1`; every pure domain module by `KI-W2`;
the accepted repository corrections named in `DEC-KI-026` are owned only by
`KI-R1`; the seven repository lease symbols named in `DEC-KI-028` are owned
only by `KI-R2-T1`, while reopened `KI-R2-RT2` owns only additive
`SCN-KI-023` integration-test symbols. Original W3 modules remain historically
owned by `KI-W3-T1/T2`; reopened W3 owns the exact adapter, contract, service,
dispatcher, build, and additive test symbols enumerated through
`KI-W3-RT1`–`RT4`. The unique KI-R3 correction owns only
`settlementFence`, `processTask`, `recoverClaimedTask`, `runProviderAttempt`,
`SqsDispatcher.sendOne`, and the literal additive manifest/test symbols, with
`SCN-KI-028`–`032` supplying the enforcement trace and unchanged
`SCN-KI-027` supplying emitted-package parity. KI-R4 owns only the
`recoverClaimedTask` identity guard, `SqsDispatcher.sendOne` own-key
enumeration, the new R4 manifest, and the six named test-file correction
anchors; its window agent owns only S1/S2/S3 and delegates one file per leaf.
The ten literal W4 paths are partitioned without overlap: four production
files by `KI-W4-T1`, one production file by `KI-W4-T2`, two production files
by `KI-W4-T3`, and three fixture/test files by `KI-W4-T4`; their sorted-LF set
digest is `fe48d14ebec1dffa058cf91cfa9ec10982d4ceaa4c63e0cb9280cabf39a4a59b`.
Every backend route/handoff/query branch by `KI-W4`; every frontend route/proxy/dashboard
surface by `KI-W5`, except the two successful dashboard navigation expressions
and the one accepted R5-FIN-01 destination oracle now uniquely owned by
`KI-W6-T1/T2`. KI-W6 initially owned its new helper, literal manifest and
causal browser harness; `SRC-KI-041`/`DEC-KI-039` add only
`service.js::aggregateMarket` and the aggregation scaffold/additive
`SCN-KI-041` symbols; `SRC-KI-043`/`DEC-KI-041` supersede only
`frontend/test/browser/keyword-intelligence-e2e.mjs::swapOneSelectionItemViaUi`
inside the already-owned causal harness. The complete seven-path digest is
`c3bfe436aba49d52de26298ac74eb30e061d392144dfffbb6954ee792c908bdc`.
Only additive SAM/build/config/runtime-config symbols named in the
W7 header by `KI-W7`; and only approved
external resources plus A5/A6 updates by `KI-W8`. Each owner traces to the
requirements and source anchors in its 15-field task block. No predecessor
write scope contains a successor target.

## 6. KI-W4 executable coverage closure

| W4 task | Exact owned file count | Required case groups | Final gate |
|---|---:|---|---|
| `KI-W4-T1` | 4 | `api_component`, applicable `server_routes` | `KI-W4-V2/V5/V6` |
| `KI-W4-T2` | 1 | `handoff_database` | `KI-W4-V3/V5/V6` |
| `KI-W4-T3` | 2 | `query_review`, applicable `server_routes` | `KI-W4-V2/V5/V6` |
| `KI-W4-T4` | 3 | all five groups plus `conformance` | `KI-W4-V2`–`V6` |

The authoritative W4 required set is the literal 34-ID manifest in A4:
8 `api_component`, 6 `server_routes`, 8 `query_review`, 6
`handoff_database`, and 6 `conformance`. Its normative sorted-member-plus-LF
digest is `86810ce87a79426bb972be2e2827abc3806835190135d17769b52c33e7bb2203`.
Acceptance requires required=registered=executed equality, zero required skips,
unique activation witnesses, the exact forbidden-operation assertions, and
all `W4-NC01`–`W4-NC18` controls to falsify the unchanged oracle before a fresh
positive witness passes. The substitute-fidelity table in A4 limits component
claims; only `W4-D01`–`D06` may certify SQL ownership, CAS, rollback, and durable
row behavior. Final verification is one non-database run, one isolated-schema
database run, one `npm test`, and one secret scan; Prisma generation/validation,
full database integration, builds, live provider calls, AWS actions, and
repeated successful stateful gates are outside W4.

## 7. KI-R5 corrective trace and executable closure

| Review finding / contract IDs | Observed evidence | Locked decision | Implementing task | Scenario / cases | Execution slot | Final review |
|---|---|---|---|---|---|---|
| `KI-PR-F01`; `REQ-KI-005/021` | `SRC-KI-034/036` | `DEC-KI-034` numeric v1 | `KI-R5-T4/T5` | `SCN-KI-036`; `R5-WIRE-01`–`03` | `KI-R5-V1/V2/V6` | parent parses actual W4 serialization with W5 parser |
| `KI-PR-F02`; `REQ-KI-014` | `SRC-KI-034/036` | `DEC-KI-034` explicit JSON headers | `KI-R5-T4/T5` | `SCN-KI-036/038`; `R5-WIRE-04`–`06` | `KI-R5-V2/V4/V6` | parent confirms emitted pass-through 401-not-415 and no intercept claim |
| `KI-PR-F03/F04`; `REQ-KI-007/008`; `INV-KI-010` | `SRC-KI-034/035` | `DEC-KI-034`, `PAY-KI-008` | `KI-R5-T1/T4/T5` | `SCN-KI-036`; `R5-SEL-01`–`03/06`–`08` | `KI-R5-V1/V2/V6/V7` | parent confirms 0/200 accepted, 201/262145 rejected, backend-derived manual ID |
| `KI-PR-F05`; `REQ-KI-007`–`009/015` | `SRC-KI-034` | `DEC-KI-035` saved projection | `KI-R5-T4/T5` | `SCN-KI-038`; `R5-FIN-01`–`04` | `KI-R5-V2/V4/V6` | parent observes zero POST for every dirty partition and saved revision handoff |
| `KI-PR-F06`; `REQ-KI-015/016`; `INV-KI-015` | `SRC-KI-034` | `DEC-KI-035` retry lifecycle/race reconciliation | `KI-R5-T2/T4/T5` | `SCN-KI-037/038`; `R5-FIN-05`–`08` | `KI-R5-V2/V3/V6/V7` | parent verifies same ID/revision retry and one durable Run under concurrency |
| `KI-PR-F07`; `REQ-KI-014/018` | `SRC-KI-034` | `DEC-KI-036` W4 predicate authority | `KI-R5-T3/T4/T5` | `SCN-KI-039`; `R5-EXP-01`–`04` | `KI-R5-V1/V2/V6` | parent compares independent literal ID/CSV sets |
| `KI-PR-F08`; `REQ-KI-008/009` | `SRC-KI-034` | `DEC-KI-036` draft validation before CAS | `KI-R5-T1/T5` | `SCN-KI-036`; `R5-SEL-04/05` | `KI-R5-V1/V6` | parent observes 400 and zero CAS |
| `KI-PR-F09`; `REQ-KI-018`; `INV-KI-009` | `SRC-KI-034` | `DEC-KI-036` textual-cell neutralization | `KI-R5-T3/T5` | `SCN-KI-039`; `R5-EXP-05/06` | `KI-R5-V1/V5/V6/V7` | parent parses dangerous text/numeric cells and scans forbidden fields |
| enforcement/invalidation | `SRC-KI-034/037` | `DEC-KI-037` | `KI-R5-T5` | `SCN-KI-040`; `R5-CONF-01`–`06` | `KI-R5-V1`–`V7`, `H1`–`H6` | parent recomputes 34-ID equality/digests, controls, scope and supersession |

### KI-R5 source/target and substitute closure

- The exact 18 delegable paths and sorted-per-LF digest
  `efc82a884d09561ed27be3513ca6898f0ab311dbe56cf46e9c2c241492560077`
  are owned only by `KI-R5-T1`–`T5`; S1/S2/S3 are owned only by the window
  agent. All Prisma/schema, package/lock, route/auth/proxy, worker/provider/
  artifact/queue/build/infrastructure and KI-W6 files are unowned/read-only.
- `PAY-KI-008` producer→consumer closure is W5 minimal mapper → emitted Next
  size/media parser → W4 strict union/materializer → existing full canonical
  selection response. No browser field supplies owner, canonical item ID,
  metrics, lane, facets, seed or durable version.
- Test substitute claims are bounded: backend fakes cover service call order;
  the one real-Prisma registry covers handoff uniqueness/rollback; fetch capture
  covers client init; the emitted Next unauthenticated pass-through covers the
  real media-type branch; actual W4 serializer→W5 parser covers response shape;
  intercepted dashboard data covers presentation only. `R5-CONF-05` rejects
  any broader claim.
- The authoritative R5 set has group counts `6/8/8/6/6` and global 34-ID
  digest `507186e7489a3f9eec18eb5de78692dbc55a8d1d2d106544aa4295a98ac9be60`.
  Every ID has exactly one registry in A4; `R5-CONF-02/06` enforce exact
  required=registered=executed equality and falsify missing, skip, duplicate,
  unexpected, unactivated, weakened-oracle and divergent-substitute states.
- `KI-W6` now depends on accepted KI-R5. The state-108 W6 decomposition has no
  assigned/executed leaf and is invalidated by `CHG-KI-025`; it supplies no
  implementation or acceptance evidence and must be regenerated after R5.

## 8. KI-W6 reauthored causal-proof closure

| Contract / finding | Observed evidence | Locked decision | Exact owner | Executable cases | Frozen gate / parent oracle |
|---|---|---|---|---|---|
| successful handoff opens API JSON instead of workspace | `SRC-KI-038` | `DEC-KI-038` workspace route from encoded `run.runId`; API `statusUrl` unchanged | `KI-W6-T1/T2` | `W6-NAV-01`–`03`; `NC-01` | V1 source/oracle inventory; V3 causal Chrome route; only R5-FIN-01 destination superseded |
| real authenticated frontend/backend causality absent from R5 | `SRC-KI-036/039` | one emitted Next/auth-client/proxy/backend/Prisma chain; no application-API interception | `KI-W6-T3/T5` | `W6-FLOW-01/02/06`; `W6-RES-01`; `NC-02/09/12` | V2 sole build; V3 one causal stateful run; substitute ledger caps claims |
| maximum keyword research and durable UI visibility | accepted W2/W3/R4/R5 evidence; `SRC-KI-039/041` | `DEC-KI-038/039`: exact 19-call, 300-screen→200-durable-shortlist→200-final/default-100, `$0.492` topology and fenced result | `KI-W6-T3/T5`, `KI-W6-CT1/CT2` | `SCN-KI-018/041`; `W6-FLOW-03`–`07`; `W6-RES-02/03`; `NC-03`–`05` | CV1 component projection; CV3 causal exact call/artifact/attempt/visibility counts; CV5 emitted worker; CV6 independent trace recompute |
| saved selection to immutable run/query lineage | accepted W4/R5 evidence | numeric-v1 minimal mutation, saved-only handoff, same-key retry, immutable snapshot | `KI-W6-T1/T3/T5` | `W6-NAV-02`; `W6-FLOW-07`–`09/13`; `NC-06` | V3 real SQL/browser proof; V5 exact Run/RunQuery/snapshot sets |
| query confirmation to downstream stable-domain boundary | existing query-review/Google-parser/discovery/domain source | exactly 100 validator/searchPage calls, 1,000 parsed occurrences, 100 per-query tasks, 1,000 stable hosts/run stores/lead tasks; stop before lead fetch; do not claim the bypassed Google transport/artifact wrapper | `KI-W6-T3/T5` | `W6-FLOW-10`–`12`; `W6-RES-02/04`; `NC-07/08` | V3 actual validator/parser/services with deterministic boundaries; V5 exact identity/count and substitute-limit recompute |
| coverage, anti-vacuity, scope and obsolete runtime | `SRC-KI-040/041`; parent standard E6–E8 | literal 26-case/13-control manifest, unique registration/activation, exact seven-file/integrated-entry inventory; SCN-KI-041 is supplemental and never a second case registration | `KI-W6-T4/T5`, `KI-W6-CT1/CT2` | `W6-CONF-01`–`06`; `NC-10`–`13` | corrected V1/CV1 source; CV3 certificate; CV5/CV6 package/scope/evidence proof |

The authoritative W6 groups contain `3/13/4/6` members with digests
`103df262…`, `14aa36ae…`, `fc83e2c6…`, `b8180b2f…`; the 26-member global digest
is `d81bab26bc5aadd19c162156c13890611b2fc5a6d0dcb917234453d568ffb4d4`.
Every case registers exactly once in the new browser harness. Acceptance requires
required=registered=executed=activated equality, zero exceptional members,
thirteen pass→mutated-fail→fresh-pass controls, one isolated schema absent after
cleanup, and exact operation/identity counts. V2–V4 are single-run frozen gates;
only their named file dependencies invalidate them. A proven sandbox/channel
failure permits the standards-defined identical escalated recovery, never a
changed command or a behavioral-failure relabel.

The following W6 overlay is additive to every corresponding Section 1 row and
is the mechanical expansion used for completeness checks:

| Exact contract set | W6 owner | W6 oracle/cases | Evidence slot |
|---|---|---|---|
| `REQ-KI-001`–`005`, `021`–`024`; `INV-KI-001`–`009`, `012`–`014` | `KI-W6-T3/T5` | `SCN-KI-018`; `W6-FLOW-01`–`06`, `W6-RES-02`–`04` | `KI-W6-V3/V5/V6` |
| `REQ-KI-006`–`009`, `014`, `018` | `KI-W6-T3/T5` | `W6-FLOW-06/07`; actual dashboard surfaces, saved selection and causal reload | `KI-W6-V2/V3/V5` |
| `REQ-KI-010`–`013`; `INV-KI-010/011/015` | `KI-W6-T3/T5` | `W6-FLOW-09`–`12`; 100 query identities, validation/parser calls and 1,000 stable domains | `KI-W6-V3/V5` |
| `REQ-KI-015`–`017` | `KI-W6-T1/T2/T3/T5` | `W6-NAV-01`–`03`, `W6-FLOW-07`–`09/13`, `W6-RES-01`; saved-only/same-key/immutable owner-scoped handoff | `KI-W6-V1/V3/V5` |
| `REQ-KI-019/020`; all `EXC-KI-001`–`008` and `AUTH-KI-001`–`004/006/007` applicable locally | W6 header, `KI-W6-T3/T5`, A5 | `W6-CONF-01`–`06`, `W6-NC-09`–`13`; exact scope, obsolete-runtime, substitute and authority closure | `KI-W6-P1`–`P6`, `V1/V3/V5/V6`, `H1`–`H6` |
| `REQ-KI-002/003/023/024`; `INV-KI-004/005/014` corrective overlay | `KI-W6-CT1/CT2` under `DEC-KI-039` | `SCN-KI-041`; existing sole `W6-FLOW-05` registration and `W6-NC-05` control; 300 anchor keys project through the durable 200-keyword manifest to exactly 200 final keys/default 100 | `KI-W6-CV1/CV3/CV5/CV6`, `KI-W6-CH1/CH2` |
| `REQ-KI-001`, `REQ-KI-002`, `REQ-KI-003`, `REQ-KI-023`, `REQ-KI-024`; `INV-KI-004`, `INV-KI-005`, `INV-KI-014` fixture-correction overlay | `KI-W6-CT3` under `DEC-KI-040` | corrected supplemental `SCN-KI-041`; five seeds × 60 unique ordered candidates; anchor-stage manifest fingerprint; unchanged `W6-FLOW-04`, `W6-FLOW-05`, `W6-FLOW-06` and `W6-NC-05` | `KI-W6-CV7`, `KI-W6-CV9`, `KI-W6-CV10`, `KI-W6-CV11`, `KI-W6-CV12`, `KI-W6-CH3`, `KI-W6-CH4` |
| `REQ-KI-007`, `REQ-KI-008`, `REQ-KI-009`, `REQ-KI-014`, `REQ-KI-015`; `INV-KI-010` paginated-selection correction overlay | `KI-W6-CT4` under `DEC-KI-041` | existing `W6-FLOW-07` and `W6-FLOW-13` traverse the real 25-row pages, remove one selected row, add one different unselected row and preserve exactly 100; unchanged `W6-NC-06`; zero new registration | `KI-W6-CV13`–`CV18`, `KI-W6-CH5`, `KI-W6-CH6` |
| `REQ-KI-002`, `REQ-KI-005`, `REQ-KI-024`; `INV-KI-004`, `INV-KI-005`, `INV-KI-006`, `INV-KI-014` bounded-publication correction overlay | `SRC-KI-044`; `KI-W6-CT5/CT6` under `DEC-KI-042` | `SCN-KI-042`; separate exact `W6-TXN-01/02` registry proves deterministic P2028 rollback and delayed maximum 30-second success; `W6-NC-14`; existing browser 26/13 manifest unchanged; combined 28/14 sets and digests frozen | `KI-W6-CV19`–`CV24`, `KI-W6-CH7`, `KI-W6-CH8` |
| `REQ-KI-002`, `REQ-KI-005`, `REQ-KI-024`; `INV-KI-004`, `INV-KI-005`, `INV-KI-006`, `INV-KI-014` supported-delay-probe overlay | `SRC-KI-045`; `KI-W6-CT7` under `DEC-KI-043` | unchanged `SCN-KI-042`, `W6-TXN-01/02`, `W6-NC-14`; same 21-second injection with a supported text result; unchanged combined 28/14 sets and digests | `KI-W6-CV25`–`CV30` |
| `REQ-KI-007`, `REQ-KI-008`, `REQ-KI-009`, `REQ-KI-014`, `REQ-KI-015`; `INV-KI-010` causal selection-array overlay | `SRC-KI-046`; `KI-W6-CT8` under `DEC-KI-044` | existing `W6-FLOW-07/13`, `W6-NC-06`; serialized selection array drives 100-item revision advance, stale 409, page-aware swap and final 100-item CAS; unchanged browser 26/13 and combined 28/14 sets | `KI-W6-CV31`–`CV35` |
| `REQ-KI-002`, `REQ-KI-005`, `REQ-KI-022`, `REQ-KI-024`; `INV-KI-004`, `INV-KI-005`, `INV-KI-006`, `INV-KI-014` KI repository transaction/recovery overlay | `SRC-KI-047`; `KI-W6-CT9`–`CT13` under `DEC-KI-045` | `SCN-KI-043`; `W6-DB-01`–`07` and `W6-NC-15`–`17`; exact 18-path 8-short/10-scale profiles, set-based operation ceilings, three-read recovery merge and hard 100-dispatch bound | `KI-W6-CV36`–`CV43`, `KI-W6-CH9` |
| `REQ-KI-007`, `REQ-KI-008`, `REQ-KI-009`, `REQ-KI-014`, `REQ-KI-015`; `INV-KI-010` successful-selection witness overlay | `SRC-KI-048`; `KI-W6-CT14` under `DEC-KI-046` | existing `SCN-KI-018`, `W6-FLOW-07/13`, `W6-NC-06`; exactly two successful selection PUTs partition into one expected-revision-1 advance and one expected-revision-2 final CAS, with one stale 409, 100 final items and durable revision three; browser 26/13 and final combined 35/17 memberships/digests unchanged | `KI-W6-CV44`–`CV49`, `KI-W6-CH10` |
| `REQ-KI-002`, `REQ-KI-015`, `REQ-KI-016`, `REQ-KI-017`; `INV-KI-010/011` protected-workspace auth-substitute overlay | `SRC-KI-049`; `KI-W6-CT15/CT16` under `DEC-KI-047` | existing `SCN-KI-018`, `W6-NAV-01`, `W6-FLOW-01`, `W6-RES-01`, `W6-NC-02/12`; opaque local session token plus complete deterministic session envelope drives the installed Neon middleware to the real `/runs/<id>` workspace while owner-B/null denial remains; no product auth edit and browser 26/13 plus final 35/17 memberships/digests unchanged | `KI-W6-CV50`–`CV57`, `KI-W6-CH11` |
| `REQ-KI-010`–`REQ-KI-015`; `INV-KI-010/015` workspace edit-provenance overlay | `SRC-KI-050`; `KI-W6-CT17` under `DEC-KI-048` | existing `SCN-KI-018`, `W6-FLOW-09/13`, `W6-NC-06`; exactly 100 generated pre-edit badges become 100 user-edited badges in the persisted first-row-swap order while the same 100 rows/text lineage and zero add/delete persist; browser 26/13 plus final 35/17 memberships/digests unchanged | `KI-W6-CV58`–`CV63`, `KI-W6-CH12` |
| `REQ-KI-010`–`REQ-KI-015`; `INV-KI-010/015` run-start scheduler overlay | `SRC-KI-051`; `KI-W6-CT18/CT19` under `DEC-KI-049` | existing `SCN-KI-018`, `W6-FLOW-10`–`12`, `W6-NC-07/08`; exactly one parked run-start callback is flushed after the observed start POST and Google trace floor but before confirmation waiting, producing witness 1/1/0, 100 actual validator/parser calls, 100 discovery tasks and the unchanged later fault-partitioned 1,000-domain proof; browser 26/13 plus final 35/17 memberships/digests unchanged | `KI-W6-CV64`–`CV69`, `KI-W6-CH13` |
| `REQ-KI-010`–`REQ-KI-015`; `INV-KI-010/015` restart-aware run-start scheduler overlay | `SRC-KI-052`; parent-direct `KI-W6-C124` under `DEC-KI-050` | existing `SCN-KI-018`, `W6-FLOW-10`–`12`, `W6-NC-07/08`; after the required server-A→server-B restart, exactly two FIFO callbacks exist, exactly one closed-server callback is discarded, exactly one live-server callback is invoked and zero remain, producing witness 2/1/1/0 before the unchanged 100-validator/100-discovery/1,000-domain proof; no case/control/digest change | `KI-W6-CV70`–`CV75`, `KI-W6-CH14` |
| `REQ-KI-010`–`REQ-KI-015`; `INV-KI-006/010/015` maximum query-validation persistence overlay | `SRC-KI-053`; parent-direct `KI-W6-C125/C126` under `DEC-KI-051` | one lease-fenced set-based 100-row update, exact returned-ID reconciliation, rollback on mismatch/lost lease, explicit 30-second scale budget; existing browser cases/controls unchanged | `KI-W6-CV76`–`CV79`, then preserved `CV72`–`CV75/CH14` |
| `REQ-KI-010`–`REQ-KI-015`; `INV-KI-004/005/010/015` downstream diagnostic/cleanup overlay | `SRC-KI-054`; `KI-W6-C127/C128` under `DEC-KI-052` | one observed downstream promise, per-message safe lifecycle, bounded pre-drop settlement, safe durable/activity snapshot and no teardown-masked rejection; existing `W6-FLOW-11/12`, `W6-RES-02/04`, `W6-NC-08`, browser 26/13 and final 35/17 sets unchanged | `KI-W6-CV80`–`CV83`; causal CV81 then preserved closure gates |
| `REQ-KI-010`–`REQ-KI-015`, `REQ-KI-024`; `INV-KI-004`–`006`, `INV-KI-010/011/015` complete clock/transaction/round-trip overlay | `SRC-KI-055`; `KI-W6-CT20`–`CT23`, leaves `KI-W6-C136`–`C144` under `DEC-KI-053` | exact 11 coordinator + 21 run-repository interactive transaction profiles; five required-now repository readers and five service callers; nine explicit aggregation clocks; single-query locked-row helpers and no recordDispatch reload; `SCN-KI-044`, `W6-DB-08`–`11`, `W6-NC-18`–`20`; combined 39/20 set equality and digests | `KI-W6-CV84`–`CV90`, `KI-W6-CH15`; one focused isolated-database gate, one durable causal browser gate, final regression/build/privacy/scope closure |
| `REQ-KI-010`–`REQ-KI-015`, `REQ-KI-024`; `INV-KI-004`–`006`, `INV-KI-010/011/015` task-terminal lease-lifecycle overlay | `SRC-KI-056`; `KI-W6-CT24`–`CT27`, leaves `KI-W6-C145`–`C148` under `DEC-KI-054` | shared renew→stop/drain→assert helper; discovery and lead invoke it before terminalization; dynamic queued-renewal/timer-clear/no-post-stop-renew witness; `SCN-KI-045`, `W6-DB-12`, `W6-NC-21`; combined 40/21 set equality and digests | `KI-W6-CV91`–`CV97`, `KI-W6-CH16`; focused enforcement/regression, dependency reuse of CV86, one durable causal browser gate, final regression/build/privacy/scope closure |
| same terminal-lifecycle overlay; local nested-test evidence transport only | C148/I120 under `DEC-KI-055` | Node 24 default isolation exposes one file wrapper; exact `--test-isolation=none` commands expose the unchanged 10-test enforcement and 26-test focused certificates | `EV-KI-W6-TC15`; C148 review; `KI-W6-CV92/CV93`; no case/control/source/product change |
| `REQ-KI-010`–`015`; `INV-KI-010/015` domain-aggregation observation overlay | `SRC-KI-057`; parent-direct `KI-W6-C149` under `DEC-KI-056` | browser observes exact produced discriminator `aggregation.check` instead of impossible `domain*`; existing `W6-FLOW-11/12` and `W6-NC-08`, no new registration | `KI-W6-CV98`–`CV101`, `KI-W6-CH17`; fresh 1,000-domain causal run then unchanged closure |
| `REQ-KI-015`–`017`; `INV-KI-010/011/015` durable handoff observation overlay | `SRC-KI-058`; parent-direct `KI-W6-C150` under `DEC-KI-057` | exact intercepted client key/revision matched to durable handoff and associated 100-query Run; response status/finish trace diagnostic only; existing `W6-NAV-02`, `W6-FLOW-08`, `W6-NC-06` | `KI-W6-CV102`–`CV105`, `KI-W6-CH18`; fresh causal run then unchanged closure |
| `REQ-KI-010`–`015`, `REQ-KI-024`; `INV-KI-004`–`006`, `INV-KI-010/015` discovery-resolution bridge overlay | `SRC-KI-059`; `KI-W6-CT30`–`CT32`, leaves `KI-W6-C152`–`C154` under `DEC-KI-058` | `SCN-KI-046`; real resolver with injected no-network fetch proves ten stores for one query; 100 strict artifacts drive the real domain aggregator/repositories to exactly 1,000 Shops/RunStores/lead tasks/messages; maximum rollback/stale fence remain invisible; `W6-DB-13`–`15`, `W6-NC-22`–`24`; final 43/24 unions | `KI-W6-CV110`–`CV115`, `KI-W6-CH20`; retain browser causality only through 100 discovery dispatches, bridge the missing middle in isolated Neon, and reuse unchanged post-resolution scale corpora |

## 9. KI-W7/W8 deployment and live-proof closure

This section supersedes the older W7/W8 references in Sections 1–5 wherever
they name `SCN-KI-019`, the nonexistent `build-aws-handlers.js`, a second
recovery schedule, 360-second visibility, or one broad deployment/canary action.

| Contract set | Observed evidence | Locked decision | Exact owner | Executable oracle | Evidence slot |
|---|---|---|---|---|---|
| `REQ-KI-002/005/022`–`024`; `INV-KI-001`–`009/012`–`014` | `SRC-KI-060`; accepted W6 build/worker evidence | `DEC-KI-059` runtime/config/recovery closure | `KI-W7-T1/T2/T6` | `SCN-KI-047`; `W7-RUNTIME-01/02`; `W7-NC-01`–`04` | `KI-W7-V2/V4/V5` |
| `INV-KI-001/002/012`; `AUTH-KI-005`; `EXC-KI-008` | current template/build/deployment scripts in `SRC-KI-060`; official AWS bounds | `DEC-KI-059` ten resources, 1080 visibility, disabled condition, narrow IAM, two ZIP packet | `KI-W7-T3`–`T6` | `SCN-KI-047`; `W7-INFRA-01`–`06`, `W7-BUILD-01`, `W7-DEPLOY-01/02`, `W7-CONF-01`; `W7-NC-05`–`12` | `KI-W7-V1`–`V6` |
| `REQ-KI-002/005/022`–`024`; `AUTH-KI-005/007`; `EXC-KI-008` | accepted W7 packet plus W8 applied preflight | `DEC-KI-059` seven separately approved actions | `KI-W8-T1/T2` | `SCN-KI-048`; `W8-LIVE-01`–`05`; `W8-NC-01`–`04` | `KI-W8-V1`–`V4` |
| `REQ-KI-015`–`017/022`–`024`; `INV-KI-005`–`011/013`–`015` | same one queued research; real SQS/Lambda/Neon/S3/UI path | `DEC-KI-059` bounded keyword-only canary and stop-before-confirmation boundary | `KI-W8-T3` | `SCN-KI-048`; `W8-LIVE-06`–`09`, `W8-CONF-01`; `W8-NC-05/06` | `KI-W8-V4`–`V7` |

### W7 exact ownership and enforcement

- The only W7 implementation/test paths are the literal 13-path table in A4;
  its sorted-member-plus-LF digest is
  `04ce71235fe61103c071f859d6050d4f8fee2b56dc0e088b9d97f5111be57a9f`.
- W7 required cases are exactly 12/digest
  `6bacf5d9291362ee0d01f5d0d8e3e53f8f9e214a6ebbf5711497c80f3d74aa2e`;
  controls are exactly 12/digest
  `6950a20f91b666c03cf59c495576e72ad1501fcd58aa5f4378900bd473edafd7`.
- Config, handler/recovery, template, measurement and deployment scripts have
  one authoritative interface in `DEC-KI-059`; the window-agent decomposition
  allocates one file per leaf and may not invent a second schedule, merge the
  two builders, or select deployment semantics.

### W8 exact authority and enforcement

- W8 has zero source/test write paths and therefore zero implementation leaves.
  The window agent personally owns the one sequential assessment; it cannot
  delegate an AWS/host/provider approval to a leaf.
- W8 required cases are exactly 10/digest
  `b716a609b2269f69d4e042503ad47dabb1eb397e17726af850f38ab09940431a`;
  controls are exactly six/digest
  `1a2fd2fb71c94f297b27c5c6ad580c67d94ae807525b420996bd4382d46b7c6e`.
- `W8-ACT-01`–`07` are the complete mutation/paid-action universe. Separate
  approval is mandatory for each applicable action. ACT-04 creates the sole
  research while disabled; ACT-05 activates it; ACT-06 is the only paid
  execution. The handoff Run is never confirmed, so downstream provider work
  is exactly outside W8.
