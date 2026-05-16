# Marketing Strategy Memo — Cycle 2026-05-14 (mid-sprint update 2026-05-16)

**From:** Marketing agent
**To:** CEO, Dev, Finance, Legal
**Date:** 2026-05-14 (original), 2026-05-16 (mid-sprint update)
**Re:** Go-to-market posture for pre-revenue MVP cycle

---

## Mid-sprint update — 2026-05-16

Two days into the cycle. No outbound has shipped yet — still gated on Legal's NDPR sign-off (deadline 2026-05-21, see `legal_risk.md`). Rather than wait idle, this update adds three execution-layer pieces (discovery call script, objection-handling playbook, segment-tailored email variants) so that the moment Legal clears the data clause, the founder can move from "send the email" to "run the campaign" without further drafting.

**Status vs. DoD:**
- Cold emails sent: **0 / 50** — blocked on Legal, not on marketing.
- Discovery calls booked: **0 / 10** — downstream of emails.
- Pilot datasets to Dev: **0 / 2** — downstream of calls.
- Content live: **0 / 3** initial pieces published; **3 / 3** additional execution pieces drafted.

**Critical path now runs through Legal.** If Legal slips past 2026-05-21, marketing's 2026-05-28 send deadline is at risk and the 2026-06-07 dataset deadline (Dev B2) almost certainly slips. Recommend CEO escalate Legal status at the next sync. Marketing has no further drafting work that meaningfully accelerates the cycle — the next bottleneck-relieving action is not ours.

---

## TL;DR

This cycle, marketing exists to do exactly one thing: **deliver 10 qualified Nigerian SME pilot prospects into the funnel by 2026-06-04**, so that Dev unblocks B2 (pilot data) and the company hits priority #2 (first 10 target customers). Everything else — brand, content cadence, PR, paid acquisition — is deferred. We are not building an audience this cycle; we are building a pilot cohort.

---

## How this maps to company_state.md priorities

| Company priority | Marketing contribution this cycle |
|------------------|-----------------------------------|
| **1. Define core product features** | Field-validate the working product definition by interviewing pilot prospects (1 question: "how do you reconcile today?"). Feedback flows to Dev within 48h of each call. |
| **2. Identify first 10 target customers** | **This is the cycle's primary deliverable.** Source via the cold outreach template + LinkedIn post + targeted segment list (see outreach doc). Target: 50 outbound emails → 10 calls → 10 pilots signed by 2026-06-04. |
| **3. Establish legal structure** | Out of scope for marketing this cycle, but: any pilot-facing copy mentioning data handling must wait until Legal confirms NDPR posture (Legal's blocker, tied to Dev task 0.9). |

## How this maps to company_state.md open decisions

- **Pricing model (flat fee vs % of invoices):** Marketing recommends we **do not commit publicly to either model until after pilot.** All outbound copy in this cycle offers "six months free + grandfathered pricing." This buys Finance/CEO room to decide without locking us in. Dev's TD-006 recommendation (flat tiered) aligns with what's easier to explain in sales conversations — flag for Finance.
- **Nigeria first vs. pan-Africa:** Marketing fully endorses **Nigeria first**, consistent with Dev's TD-003. Reasons specific to GTM: (a) the ICP pain ("MoMo narrations + GTBank exports") is concretely Nigerian and differentiates us from QuickBooks/Xero copy; (b) pilot customers in Lagos/Abuja/PH are within travel range for on-site debugging; (c) we can dominate "invoice reconciliation Nigeria" SEO inside one quarter, vs. fighting pan-African ambiguity. Pan-Africa is a Sprint 4+ marketing concern.

---

## ICP definition (locked for this cycle)

**Who we sell to:** The finance lead, accountant, or finance-leaning owner-operator at a Nigerian SME with 10–200 employees, processing 50–2,000 invoices/month, currently reconciling in Excel.

**Who we do NOT sell to this cycle:**
- Sole traders and micro-businesses under 10 staff (volume too low, willingness-to-pay too low).
- Enterprises >200 staff (sales cycle too long; we have no security/compliance answers yet).
- Non-Nigerian SMEs, even if they ask (FX, regulatory, and bank-format work isn't ready — politely waitlist them).

**Where they are:** Lagos (60%), Abuja (25%), Port Harcourt (15%) for pilot cohort.

**What they're already doing:** Manual matching in Google Sheets / Excel; a junior accountant or finance assistant burning 6–14 hours/week.

**What they're NOT doing:** Looking at QuickBooks comparison reviews. They've already bounced off international SaaS because the bank/MoMo data doesn't import cleanly.

---

## Channel plan (this cycle only)

| Channel | Effort | Expected pilot leads | Notes |
|---------|--------|---------------------|-------|
| Direct outbound email | High | 6–8 of 10 | Primary channel. See `cold_outreach_pilot_email.md`. |
| LinkedIn (founder profile) | Medium | 1–2 of 10 | See `linkedin_post_finance_lead.md`. |
| Long-form blog post | Low (one-time) | 0–1 of 10 | See `blog_post_reconciliation_drag.md`. Plays a longer-term role in SEO + credibility for cold prospects who Google us after an email lands. |
| Paid ads, SEO, PR, partnerships, events | **None** | 0 | Deliberately deferred. Pre-revenue, no creative testing budget, no story to pitch press yet. |

---

## Content produced this cycle (6 pieces)

**Initial draft set (2026-05-14):**

1. **`blog_post_reconciliation_drag.md`** — long-form awareness piece. Cites concrete pain (hours/week, ₦ cost, unattributed receivables %), names the Nigerian-specific reasons international SaaS fails, ends with pilot CTA.
2. **`linkedin_post_finance_lead.md`** — short-form social post hitting the same pain, optimised for Lagos finance professional engagement window.
3. **`cold_outreach_pilot_email.md`** — 1:1 outbound template with subject-line A/B tests, personalisation slots, follow-up cadence, and a target-segment breakdown for the first 10 customers.

**Mid-sprint additions (2026-05-16) — the execution layer:**

4. **`discovery_call_script.md`** — 20-min structured interview guide for the 10 calls. Six core questions, two pricing-anchor questions (these are the inputs Finance needs to move tier prices off placeholder by 2026-06-04), pilot ask, referral capture. Plus post-call protocol so call notes accumulate into a structured dataset over the cycle.
5. **`objection_handling_playbook.md`** — internal-facing FAQ. Top 8 objections (QuickBooks comparison, pricing, NDPR/data, "we already use X," time, decision-maker delegation, accuracy fears, longevity), recommended responses, and the reasoning so the founder can adapt rather than parrot.
6. **`segment_outreach_variants.md`** — five segment-tailored email body variants for logistics, B2B services, wholesale, schools, healthcare. Replaces the body of the base cold email; subject lines and cadence unchanged.

All six end with the same call to action: **pilot recruitment**. We are not running parallel "newsletter signup" or "early access waitlist" CTAs this cycle — one funnel, one ask.

**Identified gap:** a forwardable one-page pilot summary the prospect can send to their CEO/MD/accountant (per objection #6 in the playbook). Deferred to next cycle so we don't fragment focus before the first call lands — but flagged here so it doesn't disappear.

---

## Brand voice (working definition)

- **Specific over aspirational.** "GTBank CSV exports" and "MoMo P2P TRF narrations" do more work than "African financial infrastructure."
- **Practitioner-to-practitioner.** We write like a finance lead talking to another finance lead, not like a SaaS marketing team.
- **Honest about what we haven't built.** We say "CSV only, PDF coming later" instead of pretending we do everything. This earns trust faster than polished claims do, especially with accountants.
- **No AI hype.** Accountants need explainable matches they can defend in an audit. Our matcher is a transparent rules engine — we sell that as a feature, not apologise for it.

---

## Risks & open questions for CEO

1. **Pricing language risk.** If Finance/CEO commit to a pricing model mid-cycle, we'll need to re-pull all outbound copy. Recommend Finance commit by 2026-05-25 so we can refresh the LinkedIn/blog CTAs before the second outreach wave.
2. **Legal/NDPR risk.** We're asking pilot prospects to share invoice + statement data. We need Legal to clear our NDA + data-handling language before any pilot data lands. Marketing will not send the outreach email until Legal signs off on the data clause. This is on the Legal agent's plate (their item, ties to Dev's 0.9 and B4).
3. **Pilot capacity risk.** If outbound performs and we get 15+ qualified pilots, Dev cannot onboard them all (TD-005: single-tenant per deploy for first 2 pilots only). Marketing recommends a clear "pilot cohort 1 (2 slots)" + "pilot cohort 2 waitlist (8 slots)" structure, sequenced behind Dev's sprint plan.
4. **Founder bandwidth.** All outbound this cycle assumes founder-led sales. If founder cannot commit ~8 hrs/week to outreach calls, this plan does not work and we need to revisit.

---

## Definition of done for marketing, this cycle

- [ ] 50 personalised cold emails sent to Nigerian SME finance leads by 2026-05-28.
- [ ] 10 discovery calls booked by 2026-06-04.
- [ ] At least 2 anonymised invoice+statement datasets handed to Dev by 2026-06-07 (resolves B2).
- [ ] All three initial content pieces live (blog published, LinkedIn post posted, outreach template in active use).
- [x] Execution-layer pieces drafted (discovery script, objection playbook, segment variants) — added 2026-05-16.
- [ ] Marketing memory updated with: what worked, what didn't, learnings from discovery calls.

Anything beyond this list is out of scope for cycle 2026-05-14.

---

## Next-cycle pre-commitments (do not start before 2026-05-29)

These are noted now so they're not forgotten, *not* to be worked this cycle:

- Forwardable one-page pilot summary for prospects to send to their CEO/MD/accountant.
- Refresh pricing language across all live copy once Finance/CEO commit tier prices.
- Begin a public "pilot results" piece once Dev has run the matcher on ≥2 real datasets and we have hours-saved numbers.
- Decide whether to invest in SEO for "invoice reconciliation Nigeria" — only if Nigeria-first holds at CEO sign-off.
