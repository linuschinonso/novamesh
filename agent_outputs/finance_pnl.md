# Finance — P&L Projection & 3-Month Cash Flow

Cycle date: 2026-05-14
Owner: Finance agent
Stage: Pre-revenue MVP build
Horizon: 2026-05 → 2026-07 (Months M1–M3)

> **All figures are projections / working assumptions, not actuals.** Currency: USD unless tagged NGN. FX rate used: 1 USD ≈ 1,650 NGN (assumption, May 2026).

---

## 1. Revenue assumptions

### 1.1 Pricing model (assumed, not committed)
Adopting Dev's TD-006 recommendation as the working model pending CEO/Finance sign-off:

| Tier | Invoice volume / mo | Monthly price (NGN) | Monthly price (USD-equiv) |
|------|---------------------|---------------------|---------------------------|
| Starter | ≤ 500 | 25,000 | ~$15 |
| Growth | ≤ 2,000 | 75,000 | ~$45 |
| Scale | ≤ 10,000 | 250,000 | ~$150 |

These are placeholder price points to make the model runnable. Final pricing depends on discovery-call willingness-to-pay data (Marketing, by 2026-05-25 per their risk #1).

### 1.2 Pilot revenue posture
Marketing's outbound offer is **"6 months free + grandfathered pricing"** (strategy_memo §"open decisions"). Implication: every pilot signed in Cycle 2026-05-14 generates **zero revenue until ~2026-12**, regardless of how many pilots land.

### 1.3 Pilot cohort sizing (from Dev TD-005 + Marketing DoD)
- Cohort 1: **2 paying-eligible pilots** onboarded in M2 (single-tenant per deploy).
- Cohort 2: **up to 8 waitlisted pilots**, onboarded only after Dev migrates to row-level tenancy (≥3 customers, Sprint 4+, post-horizon).
- All 10 pilots free through ~2026-12.

### 1.4 Projected revenue, M1–M3

| Month | Pilots live | Paying pilots | Revenue (USD) |
|-------|-------------|---------------|---------------|
| M1 (May) | 0 | 0 | $0 |
| M2 (Jun) | 0–2 | 0 | $0 |
| M3 (Jul) | 1–2 | 0 | $0 |

**Total projected revenue, M1–M3: $0.** Revenue modeling moves to the M4–M12 horizon in the next cycle.

---

## 2. Cost breakdown (monthly run-rate, assumed)

### 2.1 Fixed infrastructure & tooling

| Line item | M1 | M2 | M3 | Notes |
|-----------|----|----|----|-------|
| Vercel (Next.js frontend hosting) | $0 | $0 | $20 | Free tier until M3 traffic, then Pro for one custom domain + analytics. |
| Neon / Supabase (Postgres) | $0 | $25 | $25 | Free tier covers M1; paid tier from M2 to support pilot data + backups. |
| Render / Fly.io (FastAPI backend) | $7 | $25 | $25 | Hobby in M1 (no real workload), standard from M2 once pilots ingest. |
| Domain + email (Google Workspace × 2 seats) | $14 | $14 | $14 | Founder + ops alias. |
| GitHub (Team) | $4 | $4 | $4 | One seat now; second when first hire lands (post-horizon). |
| Error monitoring (Sentry free → team) | $0 | $0 | $26 | Free tier until pilots are live. |
| Password manager / 2FA tooling | $5 | $5 | $5 | 1Password or equivalent. |
| **Subtotal: infra & tools** | **$30** | **$73** | **$119** | |

### 2.2 Go-to-market

| Line item | M1 | M2 | M3 | Notes |
|-----------|----|----|----|-------|
| Outbound sending tool (Instantly / Apollo basic) | $35 | $35 | $35 | Needed to run 50 cold emails per Marketing DoD. |
| LinkedIn Sales Navigator (founder) | $80 | $80 | $80 | ICP targeting for Lagos/Abuja/PH finance leads. |
| Travel — Lagos/Abuja/PH pilot visits | $0 | $300 | $400 | M2: 1 on-site; M3: 1–2 on-sites for cohort 1 debugging. |
| Pilot incentive (₦ vouchers / data bundles) | $0 | $60 | $60 | ~$30/pilot soft incentive to honor data-sharing time. |
| **Subtotal: GTM** | **$115** | **$475** | **$575** | |

### 2.3 Legal, compliance & corporate (assumed; coordinate with Legal agent)

| Line item | M1 | M2 | M3 | Notes |
|-----------|----|----|----|-------|
| Incorporation / CAC fees (Nigeria) — one-time | $250 | $0 | $0 | Placeholder; Legal owns the final figure (open decision #3 in company_state). |
| NDPR DPCO registration & data audit (one-time) | $0 | $400 | $0 | Required before pilot data lands (Dev B4, Marketing risk #2). |
| Pilot NDA + DPA legal review | $0 | $300 | $0 | Counsel review of Marketing's outreach data clause. |
| Accounting (bookkeeping retainer) | $0 | $50 | $50 | Starts when first invoice/receipt flow exists. |
| **Subtotal: legal & corp** | **$250** | **$750** | **$50** | |

### 2.4 People

| Line item | M1 | M2 | M3 | Notes |
|-----------|----|----|----|-------|
| Founder salary | $0 | $0 | $0 | Assumption: founder unpaid pre-revenue. Flag for CEO — if a salary draw is needed, this line dominates the model. |
| Contractor (design polish, ~10h in M3) | $0 | $0 | $300 | One-off for upload-flow UI before pilot cohort 1. Optional. |
| **Subtotal: people** | **$0** | **$0** | **$300** | |

### 2.5 Total monthly cost

| Month | Infra & tools | GTM | Legal & corp | People | **Total** |
|-------|---------------|-----|--------------|--------|-----------|
| M1 (May) | $30 | $115 | $250 | $0 | **$395** |
| M2 (Jun) | $73 | $475 | $750 | $0 | **$1,298** |
| M3 (Jul) | $119 | $575 | $50 | $300 | **$1,044** |
| **3-mo total** | **$222** | **$1,165** | **$1,050** | **$300** | **$2,737** |

---

## 3. P&L (3-month summary)

| Line | M1 | M2 | M3 | 3-mo total |
|------|----|----|----|------------|
| Revenue | $0 | $0 | $0 | $0 |
| COGS (infra attributable to pilots) | $0 | $50 | $50 | $100 |
| **Gross profit** | $0 | ($50) | ($50) | ($100) |
| Operating expenses (incl. one-time legal) | $395 | $1,248 | $994 | $2,637 |
| **Operating loss** | **($395)** | **($1,298)** | **($1,044)** | **($2,737)** |
| **Net loss (pre-tax)** | **($395)** | **($1,298)** | **($1,044)** | **($2,737)** |

---

## 4. 3-month cash flow projection

**Opening cash balance:** *unknown — input required from CEO.* Model below assumes a placeholder seed of **$10,000** so runway can be reasoned about. Replace with actual once provided.

| | M1 (May) | M2 (Jun) | M3 (Jul) |
|--|----------|----------|----------|
| Opening cash | $10,000 | $9,605 | $8,307 |
| Cash in (revenue collected) | $0 | $0 | $0 |
| Cash out — infra & tools | ($30) | ($73) | ($119) |
| Cash out — GTM | ($115) | ($475) | ($575) |
| Cash out — legal & corp | ($250) | ($750) | ($50) |
| Cash out — people | $0 | $0 | ($300) |
| **Net cash flow** | **($395)** | **($1,298)** | **($1,044)** |
| **Closing cash** | **$9,605** | **$8,307** | **$7,263** |

**Implied burn rate (M2–M3 average, excluding one-time legal): ~$870/mo.**
**Implied runway from M3 closing balance at steady-state burn: ~8 months** (before any founder salary, hire, or paid-marketing spend).

---

## 5. Key risks to the model

1. **Opening cash unknown.** The entire runway calculation rests on a placeholder seed. CEO input needed before this projection is decision-grade.
2. **Founder salary = $0 assumption.** If the founder requires any draw (e.g. $2k/mo to cover personal cash needs during 8 hrs/week of sales work — Marketing risk #4), monthly burn ~triples and runway drops from ~8 mo to ~3 mo.
3. **Six-month free pilot offer compresses revenue into 2026-Q4 at earliest.** No paying customer exists in the 3-month window. If pilots churn before converting, the model's revenue ramp slides another quarter.
4. **Pricing not yet committed.** Tier prices are Finance placeholders. Real willingness-to-pay only known after Marketing's discovery calls (deadline 2026-06-04). Could be ±50%.
5. **Pilot capacity ceiling.** Dev TD-005 caps cohort 1 at 2 pilots regardless of marketing performance. Any revenue model that assumes ≥3 paying pilots before Sprint 4+ is wrong by construction.
6. **NDPR / legal cost is an estimate.** Legal agent has not yet returned NDPR compliance scoping. The $400 DPCO line could be materially higher (registration + ongoing audit retainer).
7. **FX exposure.** Pricing is NGN-denominated (TD-003), most costs are USD-denominated (Vercel, Neon, GitHub, etc.). A 10% NGN devaluation against USD compresses gross margin once revenue starts. Track from M4 onward.
8. **Single-tenant deploy model raises per-pilot COGS.** Each new pilot in cohort 1 adds incremental infra cost (separate DB/schema, possibly separate Render service). Model assumes ~$25/pilot/month at this stage — revisit when ingestion volume is real.
9. **No paid-acquisition / no PR line.** Consistent with Marketing's deferral, but means the model has no demand-gen lever if outbound underperforms. A reactive paid-ads budget would need ~$1–2k/mo and isn't in this projection.
10. **One-time legal costs concentrated in M2.** If incorporation or NDPR slips, the spend slides — affects cash flow shape but not 3-mo total.

---

## 6. Open asks to CEO this cycle

- Confirm **opening cash balance** so runway math becomes real.
- Decide on **pricing model** (flat tiered vs % of invoices) by 2026-05-25 per Marketing risk #1.
- Confirm **founder compensation assumption** ($0 vs draw) — single biggest swing factor in the model.
- Confirm **legal/corp budget envelope** so Finance can lock the M2 legal line with the Legal agent.
