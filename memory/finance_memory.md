# Finance Memory

Last updated: 2026-05-16 (cycle 1, mid-sprint revision)

## Assumptions used in finance_pnl.md (cycle 2026-05-14, revised 2026-05-16)

### Reporting basis
- Reporting currency: **USD**, with NGN tagged where relevant.
- FX rate: **1 USD ≈ 1,650 NGN** (May 2026 placeholder).
- Horizon modeled: **M1–M3 = May, June, July 2026**.

### Revenue
- Pricing model: **flat tiered, committed** (TD-006 closed by CEO/Finance this cycle). Tier *amounts* still placeholder pending Marketing discovery 2026-06-04:
  - Starter ≤500 invoices/mo → NGN 25,000 (~$15)
  - Growth ≤2,000 invoices/mo → NGN 75,000 (~$45)
  - Scale ≤10,000 invoices/mo → NGN 250,000 (~$150)
- Pilot offer: **6 months free + grandfathered pricing** → first cash from a pilot signed in May 2026 lands no earlier than ~2026-12.
- M1–M3 revenue = $0 across all months.

### Pilot cohort (tightened from Dev Sprint 2/3 plan)
- Cohort 1 = 2 pilots (capped by Dev TD-005 single-tenant-per-deploy).
- Cohort 2 = up to 8 waitlisted pilots, unlocked only after Sprint 5 row-level tenancy migration (out of this 3-mo horizon).
- Onboarding cadence (revised): **M1 = 0 live, M2 = 1 live (pilot #1 mid-month, Sprint 2), M3 = 2 live (pilot #2 early-month, Sprint 3).**

### Costs — what changed this revision
- **Neon Postgres = $0 across M1–M3** (was $25/mo from M2). TD-009 confirms free tier covers two pilot deploys + branched staging. Risk: free-tier compute-hour cap if invoice volume spikes.
- **Fly.io ramps per-pilot under TD-005:** M1 $7 (Hobby, dev only), M2 $32 ($7 + 1 pilot service), M3 $57 ($7 + 2 pilot services). Was flat $25/mo from M2.
- **Legal M2 widened from $750 → $1,150** per CEO open decision #4 ("Finance's $750 M2 line is light"). Breakdown: NDPR DPCO registration + initial audit $700 (was $400), Legal pack review $400 (was $300), bookkeeping $50. Range $900–$1,800; firm number depends on DPCO retainer quote from Legal.
- **Contractor design polish ($300) moved from M3 → M2** to land before pilot #1 sees the Sprint 2 upload flow.
- **Pilot incentive ($30/pilot)** unchanged per pilot, but M2 line is now $30 (1 pilot) not $60 — corrected sizing now that pilot #1 lands mid-M2.
- Per-pilot infra cost assumption ≈ **$25/pilot/month** (Fly.io single-tenant service); DB cost effectively $0 inside Neon free tier until volume breaks it.

### Costs — unchanged
- Founder salary modeled at **$0** (single biggest swing factor — flagged to CEO).
- GTM tooling (Instantly $35, LinkedIn Sales Nav $80) carries from M1 even though outbound is gated on Legal.
- Travel: M2 $300 (1 on-site), M3 $400 (1–2 on-sites). Shifts right by ~1 month if Legal slips past 2026-05-21.
- One-time Nigeria CAC incorporation $250 in M1.
- No paid ads / PR / events — consistent with Marketing's deferred channels.

### Cash flow
- **Opening cash balance = $10,000 placeholder** (carried unchanged from prior cycle for like-for-like comparison). CEO input still required.
- 3-mo total burn: **$3,066** (was $2,737; +$329 / +12%).
- Steady-state burn (M2–M3 avg, ex one-time legal & contractor): **~$835/mo** (was ~$870/mo — slightly down despite higher 3-mo total because the increase is concentrated in one-time lines).
- Implied runway from M3 closing balance: **~8.3 months** at steady state, assuming $0 founder salary.

## Decisions / recommendations carried into this model
- Endorsed Dev TD-006 (flat tiered pricing) — **now CEO-closed**, no longer a Finance recommendation.
- Endorsed TD-003 (NGN-only MVP) and Marketing's Nigeria-first posture — model does not include FX or multi-currency complexity.
- Treated B2 (pilot data) as a Marketing-owned deliverable, not a Finance line item.
- Acknowledged CEO open decision #4 by widening M2 legal envelope rather than holding the prior $750 line.

## Open items for next cycle
- Replace placeholder opening cash with actual figure from CEO.
- Re-pull pricing **tier amounts** after Marketing discovery calls (target 2026-06-04).
- Confirm founder compensation policy with CEO; rebuild burn + runway if non-zero.
- Get firm NDPR / incorporation cost quote from Legal agent and tighten M2 legal range ($900–$1,800 today).
- Begin M4–M12 revenue ramp model once pilot conversion intent is known (next cycle).
- Track actual infra spend vs. projection from M2 onward — first reality check on per-pilot Fly.io COGS + Neon free-tier ceiling.
- Re-run cost-shape sensitivity if Legal slips past 2026-05-21 (M2/M3 burn redistribution per §5 risk #3 of P&L).

## Standing reference
- Reporting cadence: one cycle = one P&L + cash flow snapshot, 3-month horizon, written to `agent_outputs/finance_pnl.md`. Mid-sprint revisions allowed when upstream inputs (Dev decisions, CEO closed decisions, Marketing channel updates) materially change assumptions.
- Inputs always read at cycle start: `memory/company_state.md`, `memory/finance_memory.md`, latest `agent_outputs/dev_backlog.md`, latest `agent_outputs/marketing/strategy_memo.md`.
- All numbers labeled as projections/assumptions per CLAUDE.md constraint.
