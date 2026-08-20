• The defensible count is:

  - 9 major derailment episodes
  - 27 executed corrective windows: G‑R1 through G‑R21, then G‑R24
    through G‑R29

  - G‑R22/G‑R23 were drafted but never executed, so I did not count
    them.

   Episode                    Windows        What went wrong
  ━━━━━━━━━━━━━━━━━━━━━━━━━  ━━━━━━━━━━━━━  ━━━━━━━━━━━━━━━━━━━━━━━━━
   1. Decision-incomplete     G‑R1–G‑R6      The parent
   checklist                                 specification looked
                                             detailed but omitted
                                             exact artifact
                                             outcomes, fingerprints,
                                             timestamps, transaction
                                             composition, packaging
                                             behavior, and database
                                             isolation. G7 therefore
                                             stopped repeatedly.
  ─────────────────────────  ─────────────  ─────────────────────────
   2. False local             G‑R7–G‑R10     G11–G13 were accepted
   acceptance                                using incomplete tests.
                                             The supposed E2E
                                             harness largely
                                             exercised a zero-domain
                                             path and bypassed real
                                             provider/recovery
                                             behavior. The real
                                             matrix exposed missing
                                             protocols and
                                             transaction limits.
  ─────────────────────────  ─────────────  ─────────────────────────
   3. Late AWS deployment     Inside G14     Lambda’s applied quota
   discovery                                 was 10, reserved
                                             concurrency required at
                                             least 111, and the
                                             template exceeded
                                             CloudFormation’s inline
                                             size limit. These
                                             should have been
                                             discovered before
                                             deployment design was
                                             declared complete.
  ─────────────────────────  ─────────────  ─────────────────────────
   4. Untested control-       G‑R11–G‑R12    Run creation omitted
   plane integration                         executionBackend=aws;
                                             coordinator
                                             reconciliation depended
                                             on JavaScript and
                                             PostgreSQL producing
                                             the same sort order. A
                                             stale backend process
                                             also reclaimed a
                                             repaired run using old
                                             code.
  ─────────────────────────  ─────────────  ─────────────────────────
   5. Local tests did not     G‑R13–G‑R14    Packages contained the
   represent Lambda/IAM                      wrong Prisma native
                                             engine for Amazon
                                             Linux. Optional S3
                                             reads assumed absent
                                             objects would produce a
                                             distinguishable 404,
                                             while restricted IAM
                                             returned 403.
  ─────────────────────────  ─────────────  ─────────────────────────
   6. Lead path was only      G‑R15–G‑R19    Missing canonical URLs,
   happy-path tested                         same-task recovery
                                             self-blocking, absent
                                             frontend AWS-stage
                                             mappings, and malformed
                                             mailto: handling were
                                             missed. We worsened
                                             this by raising memory
                                             to 1024 MB before
                                             isolating the actual
                                             infinite loop.
  ─────────────────────────  ─────────────  ─────────────────────────
   7. Scale was treated       G‑R20–G‑R21    Database, S3, SQS,
   too late                                  aggregation, and
                                             DataForSEO operations
                                             contained sequential/
                                             N+1 behavior. Earlier,
                                             the final transaction
                                             timeout had been raised
                                             instead of removing the
                                             work. Mixed-version run
                                             repair also consumed
                                             effort despite this
                                             being a new project.
  ─────────────────────────  ─────────────  ─────────────────────────
   8. Traffic/provider        G‑R24–G‑R27    Provider release
   cardinality was modeled                   metadata was over-
   incorrectly                               strict, cache-only
                                             DataForSEO results were
                                             omitted, resolved CrUX
                                             months conflicted with
                                             latest, multiple shops
                                             sharing one provider
                                             identity were
                                             mishandled, and package
                                             closure was
                                             misunderstood.
   overengineered                            cross-run execution
                                             authority. After
                                             correcting that,
                                             Traffic Worker and
                                             Final Aggregator still
                                             had a lease race
                                             because their claims
                                             were not atomically
                                             mutually exclusive.

  The central cause was not that these were inherently unknowable. It
  was that we repeatedly equated green component tests with a proven
  pipeline. We generalized recovery, compatibility, and ownership
  before proving one fresh, current-format, nonempty production run
  from confirmation through traffic publication.

  The parent-level planning and acceptance process was principally
  responsible. Subagents often stopped correctly because the
  checklist was incomplete; the larger failures occurred when the
  parent declared specifications or implementations complete without
  a representative end-to-end proof.

  The final successful architecture emerged only after enforcing:

  - current-run execution authority instead of global ShopWork;
  - production-shaped, nonempty recovery tests;
  - maximum-cardinality database tests;
  - real provider identity fan-out;
  - Lambda/IAM production parity;
  - and atomic Traffic Worker/Final Aggregator lease exclusion.

  The records supporting this timeline are in
  FINAL_LAMBDA_SQS_S3_MIGRATION_EXECUTION_PLAN.md:3129 and
  AWS_PIPELINE_EXECUTION_EVIDENCE.md:1.
