# Finance — P&L Projection & 3-Month Cash Flow

Cycle date: 2026-05-14 (mid-sprint revision 2026-05-16)
Owner: Finance agent
Stage: Pre-revenue MVP build — Sprint 0 day 3 of 15
Horizon: 2026-05 → 2026-07 (Months M1–M3)

> **All figures are projections / working assumptions, not actuals.** Currency: USD unless tagged NGN. FX rate used: 1 USD ≈ 1,650 NGN (assumption, May 2026).

---

## 0. What changed since 2026-05-14

| Change | Source | Effect |
|--------|--------|--------|
| TD-006 (flat tiered pricing) accepted by CEO/Finance | dev_backlog decision log; company_state closed decisions | Tier *model* moved from "open" → "closed". Tier *amounts* (NGN 25k/75k/250k) remain placeholders pending Marketing discovery 2026-06-04. |
| TD-009 (Neon Postgres) — free tier covers two pilot deploys + branched staging | dev_backlog TD-009 | Per-pilot DB cost drops to ~$0 inside the 3-mo horizon. Risk shifts to "what if invoice volume exceeds free-tier compute hours". |
| Sprint plan firmed: pilot #1 onboards in Sprint 2 (mid-M2), pilot #2 in Sprint 3 (early M3) | dev_backlog Sprint 2+ preview | Pilot-live counts tightened from "0–2 / 1–2" to "0 / 1 / 2" across M1/M2/M3. Per-pilot Fly.io spend ramps linearly with cohort under TD-005. |
| Sprint 2 ships Next.js UI mid-M2 | dev_backlog Sprint 2+ preview | Contractor design polish moves from M3 → M2 to land *before* pilot #1 sees the upload flow. |
| Legal M2 line flagged as light by CEO open decision #4 | company_state open decisions | M2 legal envelope widened from $750 → $1,150 pending Legal's DPCO retainer quote. Still a point estimate; range disclosed in §5. |
| Outbound shipping is gated on Legal NDPR sign-off (deadline 2026-05-21) | marketing strategy_memo mid-sprint update | New risk: if Legal slips past 2026-05-21, GTM cost ramp (on-sites, pilot incentives) shifts right by ~1 month. Tools spend (Instantly, LinkedIn Sales Nav) continues as committed. |

The 3-month horizon, FX rate, opening-cash placeholder, founder-comp = $0 assumption, and 6-months-free pilot offer all carry unchanged.

---

## 1. Revenue assumptions

### 1.1 Pricing model (now committed; tier amounts still placeholder)
TD-006 closed this cycle: flat monthly fee tiered by invoice volume. Tier amounts remain placeholders until Marketing's discovery-call data lands (2026-06-04).

| Tier | Invoice volume / mo | Monthly price (NGN) | Monthly price (USD-equiv) |
|------|---------------------|---------------------|---------------------------|
| Starter | ≤ 500 | 25,000 | ~$15 |
| Growth | ≤ 2,000 | 75,000 | ~$45 |
| Scale | ≤ 10,000 | 250,000 | ~$150 |

### 1.2 Pilot revenue posture
Marketing's outbound offer is **"6 months free + grandfathered pricing"** (strategy_memo). Every pilot signed in this cycle generates **zero revenue until ~2026-12 at earliest**. M4–M12 revenue ramp will be modeled in the next cycle, once discovery-call willingness-to-pay data exists and Sprint 4 (first paying customer cutover, 2026-07-11 → 2026-07-24) is in flight.

### 1.3 Pilot cohort sizing (tightened from Sprint 2/3 plan)
- **Cohort 1: 2 pilots**, onboarded in Sprint 2 (pilot #1) and Sprint 3 (pilot #2). TD-005 caps at 2 under single-tenant-per-deploy.
- **Cohort 2: up to 8 waitlisted pilots**, gated on row-level tenancy migration (provisional Sprint 5, post-horizon).
- All 10 pilots free through ~2026-12.

### 1.4 Projected revenue, M1–M3

| Month | Pilots live | Paying pilots | Revenue (USD) |
|-------|-------------|---------------|---------------|
| M1 (May) | 0 | 0 | $0 |
| M2 (Jun) | 1 (pilot #1, mid-month) | 0 | $0 |
| M3 (Jul) | 2 (pilot #2 added early month) | 0 | $0 |

**Total projected revenue, M1–M3: $0.**

---

## 2. Cost breakdown (monthly run-rate, assumed)

### 2.1 Fixed infrastructure & tooling

| Line item | M1 | M2 | M3 | Notes |
|-----------|----|----|----|-------|
| Vercel (Next.js frontend hosting) | $0 | $0 | $20 | Free tier until Sprint 2 UI ships mid-M2; Pro from M3 for one custom domain + analytics. |
| Neon (managed Postgres) | $0 | $0 | $0 | TD-009: free tier covers two pilot deploys + branched staging. Revisit if any pilot exceeds free-tier compute hours. |
| Fly.io (FastAPI backend) | $7 | $32 | $57 | M1: Hobby for dev/staging only. M2: +$25 for pilot #1 single-tenant service. M3: +$25 for pilot #2 (per TD-005). |
| Domain + email (Google Workspace × 2 seats) | $14 | $14 | $14 | Founder + ops alias. |
| GitHub (Team) | $4 | $4 | $4 | One seat; second when first hire lands (post-horizon). |
| Error monitoring (Sentry free → team) | $0 | $0 | $26 | Free tier until both pilots are live. |
| Password manager / 2FA tooling | $5 | $5 | $5 | 1Password or equivalent. |
| **Subtotal: infra & tools** | **$30** | **$55** | **$126** | |

### 2.2 Go-to-market

| Line item | M1 | M2 | M3 | Notes |
|-----------|----|----|----|-------|
| Outbound sending tool (Instantly / Apollo basic) | $35 | $35 | $35 | Tool live as of M1 even though first send is gated on Legal — Marketing DoD still targets 50 emails by 2026-05-28. |
| LinkedIn Sales Navigator (founder) | $80 | $80 | $80 | ICP targeting for Lagos/Abuja/PH finance leads. |
| Travel — Lagos/Abuja/PH pilot visits | $0 | $300 | $400 | M2: 1 on-site (pilot #1 onboarding). M3: 1–2 on-sites (pilot #2 onboarding + pilot #1 debug). Shifts right by ~1 month if Legal slips. |
| Pilot incentive (₦ vouchers / data bundles) | $0 | $30 | $30 | ~$30/pilot soft incentive at onboarding. Slips with on-sites if Legal slips. |
| **Subtotal: GTM** | **$115** | **$445** | **$545** | |

### 2.3 Legal, compliance & corporate (coordinate with Legal agent)

| Line item | M1 | M2 | M3 | Notes |
|-----------|----|----|----|-------|
| Incorporation / CAC fees (Nigeria) — one-time | $250 | $0 | $0 | Placeholder; Legal owns the final figure. |
| NDPR DPCO registration & initial data audit (one-time) | $0 | $700 | $0 | Widened from $400 per CEO open decision #4. Includes registration + initial audit; DPCO ongoing retainer not yet quoted. |
| NDA / DPA / Privacy Notice / AUP legal review | $0 | $400 | $0 | Widened from $300 to reflect Nigerian counsel rates for full Legal pack. |
| Accounting (bookkeeping retainer) | $0 | $50 | $50 | Starts when first invoice/receipt flow exists. |
| **Subtotal: legal & corp** | **$250** | **$1,150** | **$50** | |

### 2.4 People

| Line item | M1 | M2 | M3 | Notes |
|-----------|----|----|----|-------|
| Founder salary | $0 | $0 | $0 | Assumption: founder unpaid pre-revenue. Single biggest swing factor — see §5 risk #2. |
| Contractor (design polish, ~10h) | $0 | $300 | $0 | Moved from M3 → M2 to land before pilot #1 sees the Sprint 2 upload flow. |
| **Subtotal: people** | **$0** | **$300** | **$0** | |

### 2.5 Total monthly cost

| Month | Infra & tools | GTM | Legal & corp | People | **Total** |
|-------|---------------|-----|--------------|--------|-----------|
| M1 (May) | $30 | $115 | $250 | $0 | **$395** |
| M2 (Jun) | $55 | $445 | $1,150 | $300 | **$1,950** |
| M3 (Jul) | $126 | $545 | $50 | $0 | **$721** |
| **3-mo total** | **$211** | **$1,105** | **$1,450** | **$300** | **$3,066** |

3-mo total moved from $2,737 → $3,066 (+$329 / +12%). Drivers: widened Legal M2 envelope (+$400), Fly.io per-pilot ramp (+$39 net), partially offset by Neon free tier (-$50) and lower pilot incentive (-$60).

---

## 3. P&L (3-month summary)

| Line | M1 | M2 | M3 | 3-mo total |
|------|----|----|----|------------|
| Revenue | $0 | $0 | $0 | $0 |
| COGS (infra attributable to pilots) | $0 | $25 | $50 | $75 |
| **Gross profit** | $0 | ($25) | ($50) | ($75) |
| Operating expenses (incl. one-time legal & contractor) | $395 | $1,925 | $671 | $2,991 |
| **Operating loss** | **($395)** | **($1,950)** | **($721)** | **($3,066)** |
| **Net loss (pre-tax)** | **($395)** | **($1,950)** | **($721)** | **($3,066)** |

COGS = the incremental Fly.io services attributable to pilots #1 and #2 (M2: 1 × $25; M3: 2 × $25). Neon free tier means $0 DB COGS this horizon.

---

## 4. 3-month cash flow projection

**Opening cash balance:** *unknown — input still required from CEO (open decision #3 in company_state).* Model below uses the same **$10,000 placeholder** as cycle 2026-05-14 so runway comparisons are like-for-like.

| | M1 (May) | M2 (Jun) | M3 (Jul) |
|--|----------|----------|----------|
| Opening cash | $10,000 | $9,605 | $7,655 |
| Cash in (revenue collected) | $0 | $0 | $0 |
| Cash out — infra & tools | ($30) | ($55) | ($126) |
| Cash out — GTM | ($115) | ($445) | ($545) |
| Cash out — legal & corp | ($250) | ($1,150) | ($50) |
| Cash out — people | $0 | ($300) | $0 |
| **Net cash flow** | **($395)** | **($1,950)** | **($721)** |
| **Closing cash** | **$9,605** | **$7,655** | **$6,934** |

**Implied burn rate (M2–M3 average, excluding one-time legal & contractor):** ~$835/mo.
**Implied runway from M3 closing balance at steady-state burn:** ~8.3 months (before any founder salary, hire, or paid-marketing spend).

Steady-state burn is essentially flat versus the prior cycle ($870 → $835) — the M2 increase is concentrated in one-time legal and a contractor pull-forward, neither of which recurs.

---

## 5. Key risks to the model

1. **Opening cash unknown.** Entire runway calculation rests on a placeholder seed. CEO input needed before this projection is decision-grade. *(Carried — same as prior cycle.)*
2. **Founder salary = $0 assumption.** If the founder requires a $2k/mo draw (Marketing risk #4: 8 hrs/week of sales work), monthly burn ~triples and M3-closing runway drops from ~8 mo to ~3 mo. *(Carried.)*
3. **Legal-slip cascade (new this cycle).** Legal must clear NDPR posture by 2026-05-21 to unblock Marketing's outbound. If Legal slips:
   - Outbound starts late, discovery calls slip past 2026-06-04 → pricing-tier commit slips.
   - On-site visits and pilot incentives shift M2 → M3 (cost-shape change, not 3-mo total change).
   - Pilot #1 onboarding may slip past Sprint 2 → Fly.io M2 +$25 line slides into M3.
   - Net effect: 3-mo total stays similar; M2 burn falls, M3 burn rises, first revenue still ~2026-12.
4. **Legal M2 envelope is widened but not quoted (open decision #4).** Current $1,150 M2 line is a Finance-side widening of the prior $750; the firm number depends on Legal's DPCO retainer quote. Range: **$900 (low) – $1,800 (high)**. If high, M2 burn rises ~$650 and runway drops by ~1 month.
5. **Six-month free pilot offer compresses revenue into 2026-Q4 at earliest.** No paying customer exists in the 3-month window. If pilots churn before conversion, the revenue ramp slides another quarter. *(Carried.)*
6. **Pricing tier amounts not yet committed.** Tier prices are placeholders. Real willingness-to-pay only known after Marketing's discovery calls (target 2026-06-04). Could be ±50% on each tier. *(Carried; pricing *model* now committed, see §0.)*
7. **Pilot capacity ceiling.** TD-005 caps cohort 1 at 2 pilots regardless of marketing performance. Any revenue model that assumes ≥3 paying pilots before Sprint 5 is wrong by construction. *(Carried.)*
8. **Single-tenant per-deploy COGS scales linearly.** Each cohort-1 pilot adds ~$25/mo Fly.io. Two pilots = $50/mo by M3, three pilots (hypothetical Sprint 5+) = $75/mo. Neon free tier insulates DB cost for now but breaks once invoice volume exceeds free-tier compute hours.
9. **FX exposure.** Pricing is NGN-denominated (TD-003); most costs are USD-denominated. A 10% NGN devaluation against USD compresses gross margin once revenue starts. Track from M4. *(Carried.)*
10. **No paid-acquisition / no PR line.** Consistent with Marketing's deferral, but the model has no demand-gen lever if outbound underperforms. A reactive paid-ads budget would need ~$1–2k/mo and is not in this projection. *(Carried.)*

---

## 6. Open asks to CEO this cycle

- Confirm **opening cash balance** (open decision #3) so runway math becomes real. *Highest priority — same ask as 2026-05-14.*
- Confirm **founder compensation assumption** ($0 vs draw) — still the single biggest swing factor.
- Acknowledge the widened **M2 legal envelope ($1,150)** vs. prior $750, pending Legal's firm DPCO retainer quote (open decision #4).
- Note the **Legal-slip cascade in §5 risk #3** — if 2026-05-21 NDPR deadline slips, no immediate cost surprise, but pricing-tier commit (2026-05-25 → 2026-06-04 timeline) and first-paying-customer cutover (Sprint 4) both slide right. Escalation rests with CEO weekly report per Marketing memo.
