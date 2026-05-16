# Marketing Memory

Last updated: 2026-05-16

---

## Locked ICP (cycle 2026-05-14)

**Primary:** Finance lead / accountant / finance-leaning owner-operator at a Nigerian SME with 10–200 employees, processing 50–2,000 invoices/month, currently reconciling manually in Excel or Google Sheets.

**Geographic concentration:** Lagos (60%), Abuja (25%), Port Harcourt (15%). All within travel range so we can debug pilot data on-site if needed.

**Out of ICP this cycle:** sole traders / under-10-staff micros (low willingness to pay), 200+ enterprises (no security story yet), all non-Nigerian SMEs (FX + bank-format work not ready).

---

## Audience insights (working hypotheses — validate via pilot calls)

- **Pain quantum:** 6–14 hours/week of someone earning ₦400k–₦900k/month spent on reconciliation. Translates to ~₦180k/month of salary cost on a single boring workload. This is the wedge.
- **Why international SaaS fails them:** QuickBooks/Xero assume clean payment references. MoMo (`P2P TRF FROM 080xxxxxxxx`), GTBank, Access, Zenith narrations are unstandardised. The international tools don't import this data cleanly, so they bounce.
- **What they're NOT searching for:** "QuickBooks alternative." They're not in comparison-shopping mode — they've given up on SaaS and are living in Excel. We have to reach them outbound, not via SEO this cycle.
- **What they trust:** Specificity. "GTBank CSV exports" and "MoMo narrations" earn instant credibility. Generic "African fintech" / "AI-powered reconciliation" copy reads as just another foreign vendor that doesn't get it.
- **Partial payments are normal**, not edge cases. A ₦1.2M invoice arriving as 3× ₦400k over three weeks is the rule, not the exception. Matcher and copy both need to acknowledge this.
- **Auditability matters.** Accountants need to defend reconciliations to auditors. Black-box AI matching is a *negative* selling point with this audience. Transparent rules-based matching is a feature, not a limitation to apologise for.

---

## Content produced this cycle

| File | Format | Channel | Status | CTA |
|------|--------|---------|--------|-----|
| `blog_post_reconciliation_drag.md` | Long-form (~900 words) | NovaMesh blog + LinkedIn syndication | Drafted, ready to publish 2026-05-18 | Pilot recruitment |
| `linkedin_post_finance_lead.md` | Short-form social | LinkedIn (founder + company page) | Drafted, ready to post 2026-05-19 08:00 WAT | Comment "pilot" / DM |
| `cold_outreach_pilot_email.md` | 1:1 email + A/B subject lines + follow-up cadence | Direct email | Template ready, blocked on Legal NDPR sign-off before send | 20-min discovery call |
| `discovery_call_script.md` | 20-min interview guide + post-call protocol | Founder-led video calls | Drafted 2026-05-16, ready when first call lands | Pilot ask + data request + referrals |
| `objection_handling_playbook.md` | Internal FAQ (top 8 objections) | Internal — founder reference during outbound | Drafted 2026-05-16, live for use | n/a (internal) |
| `segment_outreach_variants.md` | 5 segment-tailored email body variants | Direct email (replaces body of base template) | Drafted 2026-05-16, ready when Legal clears | 20-min discovery call |
| `strategy_memo.md` | Internal strategy doc + mid-sprint update | Cross-agent | Final + updated 2026-05-16 | n/a |

All six prospect-facing pieces share one CTA: pilot recruitment. No parallel newsletter / waitlist funnels this cycle.

**Identified content gap** (deferred to next cycle, do not start before 2026-05-29): forwardable one-page pilot summary for prospects to send internally to a CEO/MD/accountant. Surfaced by objection #6 in the playbook ("we need to ask our [decision-maker] first").

---

## Brand voice (working rules)

- Specific over aspirational ("GTBank CSV" beats "African financial infrastructure").
- Practitioner-to-practitioner tone, not SaaS marketing tone.
- Honest about what we haven't built ("CSV only, PDF coming later"). This earns trust with accountants faster than polished claims do.
- No AI hype. Sell the transparent rules engine as a feature.

---

## Cross-agent dependencies tracked

- **Dev B2 (pilot data needed):** Marketing's outbound campaign is the source. Target: ≥2 anonymised datasets to Dev by 2026-06-07. Status 2026-05-16: 0/2, downstream of calls which are downstream of emails which are blocked on Legal.
- **Legal (NDPR / NDA):** Outbound email cannot send until Legal signs off on data-handling language. Legal deadline 2026-05-21 (per `legal_risk.md`). **This is now the critical path for the whole marketing cycle.** If it slips, the 2026-05-28 send target and 2026-06-07 dataset target both slip. Escalation rec'd to CEO in mid-sprint strategy memo update.
- **Finance (pricing):** All current copy says "6 months free + grandfathered pricing." If Finance/CEO commit to a model mid-cycle, all CTAs need refresh. Asked Finance to commit by 2026-05-25. Discovery call script Q P1+P2 (2026-05-16) explicitly designed to feed Finance the willingness-to-pay data they need to move tier prices off placeholder by 2026-06-04.
- **CEO (MVP scope):** MVP scope locked 2026-05-14/15 (Dev task 0.1 done per `dev_backlog.md`). No further dependency unless CEO reverses scope.

---

## Goal for this cycle (carry forward into next cycle's check-in)

- [ ] 50 personalised cold emails sent by 2026-05-28 (status 2026-05-16: blocked on Legal NDPR sign-off)
- [ ] 10 discovery calls booked by 2026-06-04
- [ ] ≥2 anonymised pilot datasets delivered to Dev by 2026-06-07
- [ ] Blog post published, LinkedIn post live, outreach template in active use
- [x] Execution-layer pieces drafted (discovery script, objection playbook, segment variants) — completed 2026-05-16

---

## To revisit next cycle

- Validate audience insights against actual discovery-call transcripts. Update or kill hypotheses that didn't hold.
- Decide whether to invest in SEO for "invoice reconciliation Nigeria" next cycle — strong defensible position if Nigeria-first holds.
- Begin building a public "pilot results" content piece once we have 2+ pilots with measurable hours-saved data.
- Pricing language refresh once Finance/CEO commit.
- Build the forwardable one-page pilot summary (gap surfaced by objection #6).
- Pan-Africa expansion is *not* a marketing concern until Sprint 4+ — explicitly hold the line if asked earlier.

---

## Working rules learned this cycle (mid-sprint, 2026-05-16)

- **When the campaign blocks on another agent, build the next downstream piece, don't rebrief the same one.** Outbound blocked on Legal → build the call script + objection playbook so we're ready when the gate opens. Avoids polishing copy past the point of diminishing returns and avoids idle time.
- **Pricing-discovery questions belong on the discovery call, not in outbound copy.** Outbound says "six months free + grandfathered" (commits us to nothing); the discovery call asks willingness-to-pay anchors (gives Finance real data). Splitting it keeps outbound short and turns each call into a Finance research artifact.
- **Segment-specific pain references > generic "your team reconciles invoices."** Five segment variants exist precisely because memory says specificity earns instant credibility. Hypothesis: reply rate on segment variants will beat base template by ≥1.5×. Validate at 25 sends and 50 sends.
