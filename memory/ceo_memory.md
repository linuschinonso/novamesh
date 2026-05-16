# CEO Memory

Last updated: 2026-05-16

## Decisions made

### 2026-05-14 — Cycle 1
- **Pricing model: flat monthly fee tiered by invoice volume.** Adopted Dev TD-006. Reasoning: three independent agents (Dev, Finance, Legal) converged on this from commercial, financial-modelling, and regulatory angles respectively. Tier *prices* remain placeholders (NGN 25k / 75k / 250k per Finance §1.1) pending Marketing discovery-call data by 2026-06-04. Tier *model* is committed.
- **Target market: Nigeria-first through Sprint 4 / first 3 paying customers.** Pan-Africa deferred. Reasoning: Dev TD-003 (no FX), Marketing (ICP pain is concretely Nigerian, prospects within travel range), Legal §G (avoids POPIA/Kenya/Ghana registration overhead). Revisit once 3 paying Nigerian customers exist.
- **Sprint 0 scope (Dev tasks 0.1–0.9): approved as written.** Dev cleared to start Sprint 1 on 2026-05-29 contingent on Legal closing B4 (NDPR data-handling baseline).
- **Single-tenant per deploy for first 2 pilots (Dev TD-005): endorsed.** Legal §C flags it as a compliance asset (smaller blast radius for a breach). Migration to row-level tenancy gated on ≥3 customers.

### 2026-05-16 — Cycle 1 mid-sprint
- **2026-05-19 EOD adopted as a hard tripwire for Legal counsel instruction.** If counsel is not instructed by EOD 2026-05-19, the cascade (Marketing send → Dev B2 → Sprint 2 pilot #1 → Sprint 4 first-paying-customer cutover) shifts right by the slippage and is named explicitly in the next CEO weekly report — no silent absorption. Reasoning: three agents independently arrived at the same date (Legal §"Recommended next action" item 1 and R-15; Finance §5 risk #3 cascade analysis; Marketing strategy_memo mid-sprint critical-path note). Converging signal from three independent angles = close fast. Cost of formalising the tripwire is zero if Legal hits the date.
- **Healthcare segment scope bounded.** Marketing segment variant #5 must be scoped to invoice/payment-statement reconciliation only — no clinical/HMO-claim/NHIA surface. Legal review gates first send. R-13. Caught pre-send.
- **Founder talking-points one-pager required by 2026-05-22 (R-12).** Bridges the verbal-misrep window between discovery calls opening and the legal pack landing. Legal drafts, CEO approves. Without it, every discovery call carries misrep exposure.
- **Contractor IP/confidentiality clause is now M2, not M3.** Finance pulled the design contractor forward from M3 to M2 to land before pilot #1 sees the upload flow; Legal flagged the IP-assignment deadline must move with it. Coordination win, not a new decision but worth recording.

## Open CEO-side items (carry forward to next cycle)

These cannot be resolved by reading agent outputs — they require external input from the human principal.

- **Opening cash balance** (Finance §6 ask #1). Finance is using a placeholder $10,000 seed; runway math is illustrative until this is provided. Carried from 2026-05-14.
- **Founder compensation posture** (Finance §6 ask #2). Modelled at $0 draw. A $2k/mo draw triples monthly burn and cuts runway from ~8 months to ~3 months. Highest single-input swing factor. Carried from 2026-05-14.
- **Legal budget envelope** (Finance §6 ask #3, Legal §"Recommended next action"). M2 line widened to $1,150; firms up when Legal returns DPCO retainer quote (week of 2026-05-25 plausible). Range disclosed: $900 (low) – $1,800 (high). Acknowledge widened range; final number pending quote.
- **Forwardable pilot one-pager Legal review** (R-14). Pre-commit Legal review for next cycle so it doesn't become a last-minute gate when Marketing drafts the artifact.
- **Pilot-capacity reassessment after first 5 discovery calls.** TD-005 caps cohort 1 at 2; once we see real funnel performance the cohort-1 / cohort-2-waitlist sequencing becomes a live decision.

## Standing principles for this stage

- **When multiple agents converge from independent angles, close the decision fast.** Pricing model + Nigeria-first (cycle 1) and the 2026-05-19 Legal tripwire (mid-sprint) were textbook examples. The cost of leaving such decisions open is downstream rework (Marketing hedges copy, Finance models placeholders, Dev defers schema). Close, then iterate on parameters.
- **Legal is on the critical path, not parallel to it.** Pilot data cannot land until incorporation + NDPC notification + DPA/MSA/NDA templates exist. Sequence Sprint 1 around this gate, not through it. Mid-sprint reinforcement: with T-5 days to the deadline, Legal graduated from "critical path" to "single point of failure" — formalise tripwires so slippage is owned.
- **Pilot capacity is the binding constraint, not lead volume.** Dev TD-005 caps cohort 1 at 2 pilots regardless of how well Marketing's outbound performs. Marketing's 10-pilot funnel must be sequenced as cohort 1 (2 slots) + cohort 2 waitlist (8 slots), not as 10 simultaneous onboardings.
- **No public pricing commitment until pilot.** Outbound copy across all channels uses "6 months free + grandfathered pricing." Tier price points are internal until validated by discovery calls.
- **Catch coupling early, not in post-mortem.** TD-008 created R-11 the same cycle Dev specified it; TD-009 created the EU-region provisioning instruction the same cycle Dev chose Neon; healthcare segment scope (R-13) was bounded before the first send. The agent loop catches these if we let it — don't override with "ship now, fix later" instincts on PII/scope items.
- **Don't silently absorb slippage.** If a deadline slips, the cascade should be named in the weekly report, not absorbed into the schedule and forgotten. The 2026-05-19 tripwire is the first formal application of this principle.

## Active blockers I am tracking across agents

- **B4 / Legal pack** — gates Dev Sprint 1 sign-off and Marketing's first cold-email send. Counsel-instruction deadline 2026-05-21; tripwire 2026-05-19 EOD.
- **R-12 / founder verbal misrep window** — talking-points one-pager required by 2026-05-22 before discovery calendar opens.
- **R-13 / healthcare segment scope** — Legal review of segment variant #5 before first send. Block on send.
- **R-11 / audit-log retention** — Dev+Legal coordination on PII-minimisation of `audit_events` rows referencing erased records. DPCO sign-off required before pilot #1 onboarding (mid-M2).
- **B4-A / cross-border provisioning** — Dev needs explicit instruction to provision Neon pilot DB in `fra` and Fly.io services in `fra`/`lhr`. Not counsel-gated; can move now.
- **B2 / pilot data** — Marketing DoD says ≥2 anonymised datasets to Dev by 2026-06-07. On track if B4 clears; falls back to synthetic fixture in S1.5 if not.
- **Finance model decision-grade only after CEO inputs above** — accept current numbers as illustrative.
