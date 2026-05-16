# Legal Memory

Last updated: 2026-05-16 (mid-sprint revision)

## Risks flagged this cycle (carried + new)

### Carried unchanged from 2026-05-14

- **R-01 — Pre-incorporation data ingestion (CRITICAL, blocks M2).** No real pilot data uploaded until incorporation + DPCO retainer + signed pilot MSA/DPA are in place.
- **R-02 — Verbal "6 months free + grandfathered pricing" offer.** Must be written into the pilot MSA before any cold-email recipient acts on it.
- **R-03 — NDPA controller-of-major-importance threshold (~2,000 data subjects).** Treat NDPC notification as triggered from day one of pilot data landing.
- **R-04 — Third-party data subjects in statement narrations.** Push notice obligation onto pilot SME via AUP — cannot get individual consent from a name in a narration.
- **R-05 — Cross-border data transfer.** NDPA s.41 requires SCCs or EU provisioning. **Update 2026-05-16:** with TD-009 (Neon picked), instruction to Dev is now specific — Neon `fra` (Frankfurt), Fly.io `fra`/`lhr`. Vercel/Sentry/GitHub via SCC-bearing vendor DPAs.
- **R-06 — Finance legal budget.** **Update 2026-05-16:** narrowed — Finance widened M2 envelope $750 → $1,150. Remaining unknown is the DPCO retainer quote itself, not the envelope.
- **R-07 — % invoice pricing model CBN-adjacency optics.** **Resolved 2026-05-15:** CEO/Finance accepted flat tiered (TD-006). MSA must lock the contractual mechanic (flat monthly, tier-by-volume) without baking in placeholder tier amounts.
- **R-08 — Pan-Africa expansion multiplies compliance regimes.** **Confirmed 2026-05-15:** Nigeria-first through Sprint 4 / first 3 paying customers — POPIA/Kenya/Ghana scoping shelved until then.
- **R-09 — Contractor IP gap (M3 designer).** **Update 2026-05-16:** contractor pulled forward M3 → M2 in finance_pnl §2.4. IP assignment clause must land in M2 (was M3) before first deliverable.
- **R-10 — No SLA / liability cap in pilot contract.** Hard cap required in MSA — recommend fees-paid-in-12-months OR ₦5m for free pilots.

### New this cycle (2026-05-16)

- **R-11 — Audit log retention conflict (TD-008).** New `audit_events` table with `before`/`after` JSONB writes PII (customer names, narrations) on every state transition. Need PII-minimisation rule for audit rows whose underlying record is erased under NDPA (tombstone the payload, retain action+actor+timestamp). DPCO sign-off required before pilot #1 onboarding.
- **R-12 — Verbal misrepresentation window.** Marketing's discovery call script + objection playbook lands NDPR-adjacent claims in founder-led calls before the legal pack is signed. Need a one-page founder talking-points memo, Legal-approved, before the first discovery call books. Target: 2026-05-22.
- **R-13 — Healthcare segment scope creep.** Segment outreach variant for healthcare risks implying NovaMesh handles patient/clinical data (NHIA / Nigeria Health Act 2014 territory). Legal-review body copy and explicitly bound the offer to invoice/payment-statement reconciliation only. Block healthcare-segment send until cleared.
- **R-14 — Forwardable pilot summary (deferred to next cycle, flagged now).** Marketing's planned next-cycle one-pager will circulate to external decision-makers (CEO/MD/accountant) and trigger compliance questions. Pre-commit Legal review for next cycle.
- **R-15 — Counsel-instruction deadline cascade (time-sensitive).** T-5 days to 2026-05-21. If counsel is not instructed by 2026-05-19 (2-day cushion), escalate to CEO weekly report immediately. Cascade: Marketing 2026-05-28 send slips → Dev B2 dataset 2026-06-07 slips → Sprint 2 pilot #1 (mid-M2) slides into Sprint 3 → Finance M2 GTM costs shift right ~1 month.

## Standing positions (carry forward)

- **NovaMesh is a data processor, not a controller** for pilot data. Pilot SME is the controller.
- **NovaMesh is not a payment service.** Do not let marketing/website copy drift toward "payments" or "settlement" language. CBN licensing not required as long as we stay read-only on financial data.
- **DPO** designated as the founder for pre-revenue stage — but, under controller-of-major-importance treatment (R-03), the designation must be **documented** (designation letter, named contact email) and included in the NDPC notification packet, not informal.
- **Single-tenant per pilot (Dev TD-005) is a compliance asset.** Don't migrate to row-level tenancy purely for cost reasons — keep until the legal pack supports the wider blast radius.
- **CAMA accounting-record retention** (6 years) applies to reconciliation outputs; this beats NDPA erasure for transaction records (legal-obligation exception). Audit rows referencing erased records must still be PII-minimised (R-11).
- **Healthcare-segment outreach** must stay scoped to invoice/payment-statement reconciliation — never imply patient/clinical data handling (R-13).
- **Cross-border default for new infra** = EU region (Frankfurt). Document each vendor's transfer mechanism in the internal data map.

## Sub-processor list (seed, as of 2026-05-16)

| Vendor | Purpose | Region | Mechanism |
|--------|---------|--------|-----------|
| Neon | Managed Postgres (pilot DBs, branched staging) | EU `fra` (Frankfurt) — to provision | Adequacy via EU; accept Neon DPA |
| Vercel | Next.js frontend hosting | US | SCC-bearing Vercel DPA |
| Fly.io | FastAPI backend, single-tenant per pilot | EU `fra`/`lhr` — to provision | Adequacy via EU; accept Fly.io DPA |
| Google Workspace | Founder + ops email | US | SCC-bearing Google DPA |
| GitHub | Source repo, CI | US | SCC-bearing GitHub DPA |
| Sentry | Error monitoring (deferred to M3 per Finance §2.1) | US | SCC-bearing Sentry DPA — file before turn-on |
| Instantly | Outbound email tool (Finance §2.2, $35/mo) | US | SCC-bearing Instantly DPA; call-note PII risk (R-12) |
| LinkedIn Sales Navigator | ICP prospect research | US | First-party only; no scraping |

## Open asks to CEO this cycle

1. **Counsel instruction by 2026-05-19** (2-day cushion before 2026-05-21 deadline) — escalation trigger if missed (R-15).
2. Acknowledge Finance's **widened M2 legal envelope ($1,150)** — DPCO retainer quote still pending.
3. ~~Confirm Nigeria-first market scope~~ — **closed this cycle.**
4. ~~Confirm flat-tiered pricing~~ — **closed this cycle (TD-006).**

## Next-cycle agenda

- DPCO shortlist + retainer signed; quote firms up the M2 envelope.
- Pilot MSA + DPA + NDA + Privacy Notice + AUP drafted and circulated to Dev (B4) and Marketing.
- Audit-log retention & minimisation policy drafted with DPCO sign-off (R-11) before pilot #1.
- Founder talking-points one-pager published (R-12).
- Healthcare-segment body copy review delivered to Marketing (R-13).
- Pre-commit Legal review of Marketing's forwardable pilot summary (R-14).
- Cross-border data map populated once Dev confirms Neon/Fly.io EU provisioning.
- Sub-processor list above hardened into DPA appendix template.
