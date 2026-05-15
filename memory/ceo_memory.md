# CEO Memory

Last updated: 2026-05-14

## Decisions made

### 2026-05-14 — Cycle 1
- **Pricing model: flat monthly fee tiered by invoice volume.** Adopted Dev TD-006. Reasoning: three independent agents (Dev, Finance, Legal) converged on this from commercial, financial-modelling, and regulatory angles respectively. Tier *prices* remain placeholders (NGN 25k / 75k / 250k per Finance §1.1) pending Marketing discovery-call data by 2026-06-04. Tier *model* is committed.
- **Target market: Nigeria-first through Sprint 4 / first 3 paying customers.** Pan-Africa deferred. Reasoning: Dev TD-003 (no FX), Marketing (ICP pain is concretely Nigerian, prospects within travel range), Legal §G (avoids POPIA/Kenya/Ghana registration overhead). Revisit once 3 paying Nigerian customers exist.
- **Sprint 0 scope (Dev tasks 0.1–0.9): approved as written.** Dev cleared to start Sprint 1 on 2026-05-29 contingent on Legal closing B4 (NDPR data-handling baseline).
- **Single-tenant per deploy for first 2 pilots (Dev TD-005): endorsed.** Legal §C flags it as a compliance asset (smaller blast radius for a breach). Migration to row-level tenancy gated on ≥3 customers.

## Open CEO-side items (carry forward to next cycle)

These cannot be resolved by reading agent outputs — they require external input from the human principal.

- **Opening cash balance** (Finance §4, §6 ask #1). Finance is using a placeholder $10,000 seed; runway math is illustrative until this is provided.
- **Founder compensation posture** (Finance §5 risk #2, ask #3). Modelled at $0 draw. A $2k/mo draw triples monthly burn and cuts runway from ~8 months to ~3 months. Highest single-input swing factor in the financial model.
- **Legal budget envelope** (Finance §2.3, Legal §"Recommended next action"). Current M2 line ($750) is light. Expected real envelope $1,500–$2,500 across M1–M2 once DPCO retainer is real. Wait for Legal to return DPCO quote, then revise Finance envelope.

## Standing principles for this stage

- **When multiple agents converge from independent angles, close the decision fast.** Pricing model + Nigeria-first this cycle were textbook examples. The cost of leaving such decisions open is downstream rework (Marketing hedges copy, Finance models placeholders, Dev defers schema). Close, then iterate on parameters.
- **Legal is on the critical path, not parallel to it.** Pilot data cannot land until incorporation + NDPC notification + DPA/MSA/NDA templates exist. Sequence Sprint 1 around this gate, not through it.
- **Pilot capacity is the binding constraint, not lead volume.** Dev TD-005 caps cohort 1 at 2 pilots regardless of how well Marketing's outbound performs. Marketing's 10-pilot funnel must be sequenced as cohort 1 (2 slots) + cohort 2 waitlist (8 slots), not as 10 simultaneous onboardings.
- **No public pricing commitment until pilot.** Outbound copy across all channels uses "6 months free + grandfathered pricing." Tier price points are internal until validated by discovery calls.

## Active blockers I am tracking across agents

- **B4 / Legal pack** — gates Dev Sprint 1 sign-off and Marketing's first cold-email send. Legal must instruct counsel by 2026-05-21.
- **B2 / pilot data** — Marketing DoD says ≥2 anonymised datasets to Dev by 2026-06-07. On track but a critical handoff.
- **Finance model decision-grade only after CEO inputs above** — accept current numbers as illustrative.
