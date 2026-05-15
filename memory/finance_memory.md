# Finance Memory

Last updated: 2026-05-14 (cycle 1)

## Assumptions used in finance_pnl.md (cycle 2026-05-14)

### Reporting basis
- Reporting currency: **USD**, with NGN tagged where relevant.
- FX rate: **1 USD ≈ 1,650 NGN** (May 2026 placeholder).
- Horizon modeled: **M1–M3 = May, June, July 2026**.

### Revenue
- Pricing tiers (placeholder, pending CEO/Finance commit by 2026-05-25):
  - Starter ≤500 invoices/mo → NGN 25,000 (~$15)
  - Growth ≤2,000 invoices/mo → NGN 75,000 (~$45)
  - Scale ≤10,000 invoices/mo → NGN 250,000 (~$150)
- Pricing model assumed: **flat tiered** (per Dev TD-006 and Marketing endorsement). NOT yet committed publicly.
- Pilot offer: **6 months free + grandfathered pricing** → first cash from a pilot signed in May 2026 lands no earlier than ~2026-12.
- M1–M3 revenue = $0 across all months.

### Pilot cohort
- Cohort 1 = 2 pilots (capped by Dev TD-005 single-tenant-per-deploy).
- Cohort 2 = up to 8 waitlisted pilots, unlocked only after Sprint 4+ row-level tenancy migration (out of this 3-mo horizon).
- Onboarding cadence: M2 = 0–2 live, M3 = 1–2 live.

### Costs
- Founder salary modeled at **$0** (single biggest swing factor — flagged to CEO).
- Infra stack costs based on Dev TD-001: Vercel + Neon/Supabase + Render/Fly + Postgres.
- Per-pilot infra cost assumption: **~$25/pilot/month** under single-tenant-per-deploy. Revisit when real ingestion volume exists.
- GTM costs scoped to Marketing's committed channels: outbound email tool, LinkedIn Sales Navigator, travel for Lagos/Abuja/PH on-sites, small pilot incentives. **No paid ads, no PR, no events** — consistent with Marketing channel plan.
- Legal/corp costs include placeholder for Nigeria CAC incorporation ($250 one-time, M1), NDPR DPCO registration ($400 one-time, M2), NDA/DPA legal review ($300 one-time, M2), bookkeeping retainer ($50/mo from M2). **All legal lines pending confirmation by Legal agent.**

### Cash flow
- **Opening cash balance = $10,000 placeholder.** CEO input required before this is decision-grade.
- 3-mo total burn: **$2,737**.
- Steady-state burn (M2–M3 avg, ex one-time legal): **~$870/mo**.
- Implied runway from M3 closing balance: **~8 months** at steady state, assuming $0 founder salary.

## Decisions / recommendations carried into this model
- Endorsed Dev TD-006 (flat tiered pricing) as the working assumption for forecasting.
- Endorsed TD-003 (NGN-only MVP) and Marketing's Nigeria-first posture — model does not include FX or multi-currency complexity.
- Treated B2 (pilot data) as a Marketing-owned deliverable, not a Finance line item.

## Open items for next cycle
- Replace placeholder opening cash with actual figure from CEO.
- Re-pull pricing assumptions after Marketing discovery calls (target: by 2026-06-04).
- Confirm founder compensation policy with CEO; rebuild burn + runway if non-zero.
- Get firm NDPR / incorporation cost quotes from Legal agent and lock M2 legal spend.
- Begin M4–M12 revenue ramp model once pilot conversion intent is known (next cycle).
- Track actual infra spend vs. projection from M2 onward — first reality check on per-pilot COGS assumption.

## Standing reference
- Reporting cadence: one cycle = one P&L + cash flow snapshot, 3-month horizon, written to `agent_outputs/finance_pnl.md`.
- Inputs always read at cycle start: `memory/company_state.md`, `memory/finance_memory.md`, latest `agent_outputs/dev_backlog.md`, latest `agent_outputs/marketing/strategy_memo.md`.
- All numbers labeled as projections/assumptions per CLAUDE.md constraint.
