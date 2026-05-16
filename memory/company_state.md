# NovaMesh — Company State

Last updated: 2026-05-16

## Mission
Automate invoice reconciliation for African SMEs via B2B SaaS.

## Stage
Pre-revenue. Building MVP. Sprint 0 (foundations) runs 2026-05-14 → 2026-05-28; currently day 3 of 15. Sprint 1 (ingestion + matching core) targeted 2026-05-29 → 2026-06-12.

## Current priorities
1. Close the Legal pack (incorporation, NDPC registration, MSA/DPA/NDA templates, Privacy Notice, AUP) before pilot data can land — critical path. Counsel must be instructed by 2026-05-21; **CEO tripwire is 2026-05-19 EOD** (slip past this triggers formal cascade naming in the next weekly report).
2. Recruit first 10 target customers (Marketing DoD: 50 emails by 2026-05-28, 10 calls by 2026-06-04, ≥2 anonymised datasets to Dev by 2026-06-07).
3. Execute Sprint 0 specs and stack scaffolding (Dev tasks 0.2–0.8 close by 2026-05-26; task 0.9 stays blocked on Legal); kick off Sprint 1 on 2026-05-29.
4. Convert Finance model from illustrative to decision-grade by providing opening cash balance and founder compensation posture.
5. Bridge the verbal-misrep window before discovery calendar opens: Legal-drafted founder talking-points one-pager by 2026-05-22 (R-12).

## Closed decisions (this cycle)
- **Pricing model: flat monthly fee tiered by invoice volume.** Tier price points (NGN 25k / 75k / 250k) remain placeholders pending Marketing discovery-call data by 2026-06-04.
- **Target market: Nigeria-first through Sprint 4 / first 3 paying customers.** Pan-Africa deferred.
- **MVP scope (Dev Sprint 0 tasks 0.1–0.9): approved.**
- **Multi-tenancy posture: single-tenant per deploy for first 2 pilots (Dev TD-005); migrate to row-level tenancy after ≥3 customers.**
- **2026-05-19 EOD tripwire for Legal counsel instruction (new this revision).** If counsel is not instructed by EOD 2026-05-19, the cascade (Marketing send → Dev B2 → Sprint 2 pilot #1 → Sprint 4 first-paying-customer cutover) is named in the next CEO weekly report rather than silently absorbed.
- **Healthcare segment scope bounded (new this revision).** Marketing segment variant #5 restricted to invoice/payment reconciliation; no clinical/HMO-claim/NHIA surface. Legal review gates first send (R-13).
- **Cross-border provisioning rule (new this revision).** Neon pilot DB in EU `fra` (Frankfurt); Fly.io pilot services in `fra` or `lhr`. Captured in Sprint 1 tasks S1.1 and S1.10.

## Open decisions
- **Tier price points** — placeholders only until Marketing's discovery calls land willingness-to-pay data (by 2026-06-04).
- **Founder compensation** — modelled at $0 draw; not yet confirmed by CEO. Highest single-input swing factor in the Finance model.
- **Opening cash balance** — needed to make runway math decision-grade.
- **Legal budget envelope** — M2 line widened from $750 → $1,150; firms up when Legal returns DPCO retainer quote. Range: $900–$1,800.
- **Pilot capacity vs. funnel performance** — revisit after first 5 discovery calls land.
- **Forwardable pilot one-pager (R-14)** — Legal review pre-committed for next cycle so it isn't retrofitted under deadline pressure.

## Agent outputs this cycle
- Dev: complete, mid-sprint revision (`agent_outputs/dev_backlog.md`) — adds TD-007/008/009.
- Marketing: complete, mid-sprint additions (`agent_outputs/marketing/strategy_memo.md`, `cold_outreach_pilot_email.md`, `linkedin_post_finance_lead.md`, `blog_post_reconciliation_drag.md`, `discovery_call_script.md`, `objection_handling_playbook.md`, `segment_outreach_variants.md`).
- Finance: complete, mid-sprint revision (`agent_outputs/finance_pnl.md`) — burn widened $2,737 → $3,066, Legal-slip cascade modelled.
- Legal: complete, mid-sprint revision (`agent_outputs/legal_risk.md`) — adds R-11 through R-15.
- CEO: complete (`agent_outputs/ceo_weekly_report.md`) — adds 2026-05-19 tripwire decision.

## Active blockers
- **B4 (Dev) / Legal pack** — counsel-instruction deadline 2026-05-21; **CEO tripwire 2026-05-19 EOD**. Gates Dev Sprint 1 sign-off and Marketing's first cold-email send.
- **R-12 / founder verbal misrep window** — talking-points one-pager required by 2026-05-22.
- **R-13 / healthcare segment scope** — Legal review of segment variant #5 before first send.
- **R-11 / audit-log retention** — Dev+Legal coordination on PII-minimisation of `audit_events` rows referencing erased records; DPCO sign-off required before pilot #1.
- **B4-A / cross-border provisioning** — Dev to provision Neon `fra` and Fly.io `fra`/`lhr` per Legal §B; not counsel-gated, actionable now.
- **B2 (Dev) / pilot data** — depends on Marketing DoD (≥2 datasets to Dev by 2026-06-07); falls back to synthetic fixture (S1.5) if B4 slips.
- **Finance opening cash / founder comp / DPCO quote** — depends on CEO-side input and Legal's DPCO retainer quote return.
