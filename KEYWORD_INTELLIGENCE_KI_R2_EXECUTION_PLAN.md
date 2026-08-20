# KI-R2 Execution Plan — Conditional Keyword Lease Renewal and Terminal Fences

> **Historical only — do not execute this file.** Its first- and second-attempt
> overlays predate `CHG-KI-012`. The requester-reopened proof gate is specified
> completely and exclusively by the `KI-R2-RT2`/`SCN-KI-023` subsection of A4
> `KI-CL-8` and the current hash-pinned A5 assignment.

**Authoring disposition:** `DECISION-COMPLETE`. This plan never grants or
records mutable assignment status; only A5 does. At this plan's authoring
snapshot, A5 state 87 assigns only KI-R2. It does not authorize W3 remediation
or acceptance.

**Window:** `KI-R2` (A4 `KI-CL-7`)  
**Stop:** after KI-R2 handoff at `AWAITING_REVIEW`; do not reopen W3.

## 0. Parent-review reopening — second attempt

The first KI-R2 handoff (`EV-KI-R2-01..02`, A5 state 88) is rejected by
`EV-KI-R2-03`. A5 state 89 reopens this same unaccepted window as `READY`.
This section is the mechanical second-attempt overlay; it does not change
`DEC-KI-028`, the seven-symbol source boundary, or any product/runtime decision.

For the second attempt, §3 `P1`, `P2`, and `P4` are replaced as follows; `P3`
is unchanged:

1. `P1-R`: A5 is state 89, assigns only KI-R2 as `READY`, remains
   `accepted_through:KI-R1`, names `KI-W3` only as the blocked next candidate,
   and stops after KI-R2.
2. `P2-R`: preserve the first attempt's three-file working tree at backend
   HEAD `f9457deaee19fdfa1f9c1e33152a143d69753c3c`. Its starting hashes are:
   repository `e2cad9ea0d47adca3baeb28261da7a09ad775e5fc15c1ecde33f132d7387ee39`,
   unit test `1a2168af81e97f9b0cd239d594362e8a0856754f6b0783efa8c2f134843a77a2`,
   integration test
   `0534ec48abdc54dae719bd403fd583b588d2c68016774aefb2fec1ea527199b1`.
   `scripts/build-keyword-worker.js` is byte-identical to HEAD at
   `8d9e71b0227828ac54bbe437f6dc1e76eb37d06241287db036e17cb8ec51ce65`;
   frontend remains clean at `0dfa1acac50fac3a86d02ec674c6d2bab645832d`.
3. `P4-R`: reproduce the four review gaps by inspecting the current tests and
   evidence; do not restore rejected production source. The gaps are the
   missing task exact-boundary/reclaim/stale-terminalize schedule, missing full
   row-equality witnesses after aggregation stale calls, non-Proxy/inverted V5
   controls, and contradictory build/W3 action evidence.

Complete all of the following inside the original §2 boundary:

1. Replace the task portion of `SCN-KI-022` with deterministic isolated
   schedules covering `T0+59,999ms`, exact `T0+60,000ms`, and
   `T0+60,001ms`. A live A heartbeat at `T0+59,999ms` must extend expiry to
   exactly `T0+119,999ms`; B loses at renewed-expiry minus 1ms and wins at
   exact renewed expiry (with a separate +1ms repetition). After B wins, A's
   heartbeat and `terminalize` both return `lost`; reload and deep-compare the
   complete task and owning-stage rows after each stale call. B terminalizes
   once, exact replay is `found`, and the owning-stage terminal/succeeded
   counters remain exactly one.
2. Run the aggregation heartbeat at exactly `T0+40,000ms`, yielding expiry
   `T0+160,000ms`. Preserve the minus-1ms/exact/+1ms competing-owner cases.
   Use separate research fixtures for candidate, shortlist, final-result, and
   fail-stage stale-owner schedules. Before and after every A call, reload and
   deep-compare the source stage, research row (including selection/result),
   all counters and manifest fields, next-stage row, and sorted next-stage task
   set. Then let B perform the corresponding valid operation exactly once;
   candidate/shortlist/final exact completed replay must be `found`, while a
   second `failStage` must not create a second terminal transition.
3. Reimplement `clientWithRemovedTaskHeartbeatPredicate(client,key)` as a
   non-mutating nested `Proxy`. It may intercept only
   `keywordResearchTask.updateMany`, must `structuredClone` its argument,
   delete exactly the selected `where` key, and delegate every other property,
   method, and argument unchanged. For each key, run the unchanged assertion
   that expects `lost` and capture its `AssertionError` with `assert.rejects`;
   record one falsified oracle per control. Re-run the same assertion through
   the unwrapped client and require it to pass. Do not assert the broken
   `claimed` result as the control's success criterion.
4. Extend additive cleanup support so every run queries its exact schema name
   after `DROP SCHEMA ... CASCADE` and asserts absence before disconnecting the
   admin client. Never query, clean, or migrate `public`.
5. Append superseding evidence rather than rewriting `EV-KI-R2-01/02`. State
   that attempt one temporarily edited and restored a W3 file and regenerated
   ignored build output; those actions make its no-action wording false. The
   second attempt must perform neither action. Do not run `measure:lambda`, a
   keyword build, or an optional non-isolated whole-suite command. Run only
   §5's required commands, using sandbox approval for documented network or
   localhost restrictions, and record both restricted and approved outcomes.

The source implementation may remain byte-identical to the `P2-R` repository
hash if the completed tests expose no defect. If a defect is exposed, only the
same seven named methods may change. Before handoff, the diff must still contain
exactly the same three authorized files. CAS A5 from state 89 to
`AWAITING_REVIEW`, keep `accepted_through:KI-R1`, and stop; do not reopen W3.

## 1. Assignment and immutable baseline

| Item | Exact value |
|---|---|
| A5 state | `87` |
| Current window | `KI-R2` |
| Accepted through | `KI-R1` |
| A1 hash | `8b17f85c533e8f37f963e5c2bef2b59784714d6ef1ef5ef8964b81abdad0522c` |
| A4 hash | `236a41cdad93883b6494d84beb2d859a6739f32dab0ec58a147bcebff76c8883` |
| Backend baseline | clean `f9457deaee19fdfa1f9c1e33152a143d69753c3c` |
| Frontend baseline | clean `0dfa1acac50fac3a86d02ec674c6d2bab645832d` |
| Repository hash | `c4d0a07713d24418fa49d89582da683449f87c188a13bdedfef3416063baec0b` |
| Unit-test hash | `0c2b28b9d77f0c85db296d4fb8149ad63365739998cb259b991d3d16733dd6ad` |
| Integration-test hash | `7eafb0eb3700da59a29a761ea2a4ddbf1bd8d3fea7f2b87fef6ee6ddd40ba7bc` |
| Successor | `KI-W3`, reserved for parent, `may_start_successor:false` |

Before editing, recompute both document hashes and the three file hashes. Stop
on mismatch. Record root/backend/frontend status without staging, committing,
resetting, moving, or repairing the owner-controlled root relocation state.

## 2. Exact boundary

The only production file is
`email_scraper/src/keyword-intelligence/repository.js`, and only these symbols
may change:

1. `PrismaKeywordResearchRepository.heartbeat`
2. `PrismaKeywordResearchRepository.heartbeatAggregator` (new)
3. `PrismaKeywordResearchRepository.terminalize`
4. `PrismaKeywordResearchRepository.claimAggregator`
5. `PrismaKeywordResearchRepository._completeStageAndCreateNext`
6. `PrismaKeywordResearchRepository.publishResearchResult`
7. `PrismaKeywordResearchRepository.failStage`

The only test files are:

- `email_scraper/test/keyword-intelligence-repository.test.js`, additive KI-R2
  fail-closed/public-surface cases only;
- `email_scraper/test/keyword-intelligence-repository.integration.test.js`,
  additive `SCN-KI-022` helpers/cases only.

Prisma schema/migrations, every W3 file at `f9457de`, API/frontend/package files,
build output, and all other accepted source are read-only. No provider call,
AWS operation, production/public database write, raw payload restoration, or
commit is permitted.

## 3. Preconditions P1–P4

1. `P1`: A5 names only KI-R2, is state 87, pins the §1 hashes, keeps
   `accepted_through:KI-R1`, and has `stop_after:KI-R2`.
2. `P2`: the backend/frontend and three owned-file hashes equal §1; record the
   complete dirty/status baseline.
3. `P3`: `TEST_DATABASE_URL` exists, differs from production, and the existing
   `test/helpers/isolated-postgres.js` proves an explicit disposable
   non-public `current_schema()` and schema-local `_prisma_migrations`. Never
   print connection values.
4. `P4`: reproduce all four pre-edit contradictions with read-only inspection:
   no `heartbeatAggregator`; task heartbeat has no live-expiry predicate;
   aggregator reclaim uses `lt`; ordinary terminal/publication/failure updates
   omit live-expiry predicates.

If any prerequisite differs, append one concise blocker and stop. Do not choose
a substitute interface or modify a fourth file.

## 4. T1 mechanical implementation

### 4.1 Task heartbeat

Keep the existing validation. Replace its conditional write with exactly:

```js
const leaseExpiresAt = plusMilliseconds(now, TASK_LEASE_MS);
const updated = await this.client.keywordResearchTask.updateMany({
  where: {
    id: taskId,
    state: "processing",
    leaseToken: token,
    leaseExpiresAt: { gt: now }
  },
  data: { leaseExpiresAt, updatedAt: now }
});
return updated.count === 1
  ? { outcome: "claimed", leaseExpiresAt }
  : { outcome: "lost" };
```

It is exactly one database update and zero reads. Do not add `not_found` or
`conflict` outcomes.

### 4.2 Aggregation heartbeat

Add the public method immediately after `claimAggregator` unless local method
ordering makes placing it immediately before claim clearer; no other export is
needed. It must:

1. call `requireNow(now)`;
2. validate `researchId`, `stage`, `generation` (exact default `1` when the
   field is absent), and token with the existing helpers;
3. derive `stageId=keywordStageId(researchId,stage,generation)`;
4. compute `leaseExpiresAt=now+AGGREGATION_LEASE_MS`;
5. perform one `keywordResearchStage.updateMany` with exact predicates:
   `id`, `researchId`, `stage`, `generation`, `state:"aggregating"`, exact
   `aggregationLeaseToken`, and `aggregationLeaseExpiresAt:{gt:now}`;
6. write only `aggregationLeaseExpiresAt` and `updatedAt`;
7. return `{outcome:"claimed",leaseExpiresAt}` for count one, otherwise
   `{outcome:"lost"}`.

There is no lookup, transaction wrapper, owner input, configurable duration,
new token, attempt increment, or projection change.

### 4.3 Exact expiry and terminal fences

- In `claimAggregator`, change only the expired-aggregation conditional CAS
  from `aggregationLeaseExpiresAt:{lt:now}` to `{lte:now}`. A lease is live iff
  expiry `>now`; equality is reclaimable.
- In `terminalize`, after state/token validation return `lost` when expiry is
  absent or `<=now`; its terminal `updateMany.where` must repeat
  `leaseExpiresAt:{gt:now}`.
- In `_completeStageAndCreateNext`, after aggregation state/token validation
  return `lost` when aggregation expiry is absent or `<=now`; its completing
  update must repeat `aggregationLeaseExpiresAt:{gt:now}`. Both candidate and
  shortlist publication inherit this one correction.
- In `publishResearchResult`, after state/token validation return `lost` when
  expiry is absent or `<=now`; the market-stage conditional update must repeat
  `aggregationLeaseExpiresAt:{gt:now}`. Its existing abort must still roll back
  the final transaction when count is zero.
- In `failStage`, its conditional update must add
  `aggregationLeaseExpiresAt:{gt:now}`. Count zero remains `lost`; therefore an
  expired token cannot fail the research.

Do not alter exact completed replays: already-published equal data remains
`found` without requiring a live token. Do not change `settleAttempt` or
`markAttemptAmbiguous`; their post-provider behavior is intentionally different
under `DEC-KI-026`.

## 5. Verification oracles

### V1 — `SCN-KI-022`

Use the existing isolated schema harness and deterministic dates/tokens. Cases
must collectively prove:

- task heartbeat at a live instant performs one update/zero reads and extends
  to exactly `now+60000ms`; expired, wrong-token, terminal, and missing cases
  are `lost` with zero changes;
- aggregation heartbeat performs one update/zero reads and extends to exactly
  `now+120000ms`; owner/token/acquired-at/attempt/counters/manifests are
  unchanged;
- competing aggregator loses at renewed-expiry minus 1ms; at exact expiry one
  claimant can reclaim; a repeated isolated case at plus 1ms also reclaims;
- after B reclaims, A gets `lost` for heartbeat, candidate publication,
  shortlist publication, final publication, and fail-stage paths, with complete
  row equality and zero next-stage/result/selection visibility;
- B can perform each isolated valid publication exactly once, and an exact
  completed replay returns `found`;
- one task terminal counter and one aggregation publication occur—never two.

Do not fake S3/SQS/provider operations; repository integration uses no such
client. Keep original `SCN-KI-020/021` cases byte-identical unless a shared test
helper must be extended additively.

### V2–V4 — required commands and scope

Run from `email_scraper/`:

```bash
node --test --test-isolation=none test/keyword-intelligence-repository.test.js
ALLOW_DATABASE_TESTS=true node --test --test-isolation=none test/keyword-intelligence-repository.integration.test.js
npm run db:generate
npm run db:validate
npm run check:secrets
npm test
```

The database command must use only the isolated URL/harness. If the documented
localhost suites fail with sandbox `listen EPERM`, rerun the identical suites
with sandbox approval and record both outcomes. No other failure may be waived.

Before handoff, `git diff --name-only` must be exactly the three §2 files.
Recompute the read-only schema/migration/package/W3/frontend hashes or exact Git
diff/status proof and record byte identity.

### V5 — negative controls

Add `clientWithRemovedTaskHeartbeatPredicate(client,key)` to the integration
test, following its existing Proxy-wrapper style. It intercepts only
`keywordResearchTask.updateMany`, clones the call argument, deletes the exact
`key` from `where`, and delegates every other path and argument unchanged. Run
three independent controls without modifying production source:

1. remove the token predicate: wrong-token assertion must fail;
2. remove the state predicate: terminal-row assertion must fail;
3. remove the strict-live-expiry predicate: expired-owner assertion must fail.

After each, use the unwrapped client and rerun the matching positive assertion.
Record exact failing test names/counts. Merely asserting a mock was called is
not sufficient; each control must falsify a durable oracle.

## 6. Handoff H1–H6

1. Record exact changed methods/files, commands, test counts, row/query counts,
   negative-control failures, skips, and residual risks in new A6 KI-R2 entries.
2. Drop only this run's disposable schema in `finally` and query its exact name
   for absence. Do not clean `public` or unrelated `kir*` schemas.
3. Prove the final diff contains only the three authorized files; record their
   final hashes and read-only-path equality.
4. Record zero W3/provider/AWS/production/schema/migration/package/frontend/
   build/commit actions.
5. CAS A5 from state 87 to the next state with `current_window:KI-R2`,
   `current_status:AWAITING_REVIEW`, `accepted_through:KI-R1`,
   `next_on_pass:KI-W3`, `stop_after:KI-R2`, and current A1/A4 hashes.
6. Stop. Do not edit, assign, reopen, test as remediation, or accept KI-W3.

KI-R2 acceptance means only that the predecessor lease surface is ready for
W3 consumption. The parent must separately review KI-R2 and explicitly reopen
W3, whose original P/T/V/H boxes remain unchecked.
