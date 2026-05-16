# Legal — Risk Assessment & Compliance Checklist

Cycle date: 2026-05-14 (mid-sprint revision 2026-05-16)
Owner: Legal agent
Stage: Pre-revenue MVP build — Sprint 0 day 3 of 15 (Nigeria-first SaaS, B2B invoice reconciliation)

---

## 0. What changed since 2026-05-14

| Change | Source | Legal effect |
|--------|--------|--------------|
| TD-007 — single `StatementParser` protocol across all bank/MoMo formats | dev_backlog | Sub-processor / data-flow story stays one shape regardless of source format. Reduces DPA appendix churn. |
| TD-008 — single append-only `audit_events` table with `before`/`after` JSONB on every entity transition | dev_backlog | **New PII surface.** Audit rows can mirror customer names + narrations indefinitely. Retention/minimisation must be specified, not just "keep 6 years." See new risk **R-11**. |
| TD-009 — Neon Postgres chosen as managed DB | dev_backlog | Specific provisioning instruction now possible: deploy in Neon **EU region** (Frankfurt) for pilot DBs. Replaces the generic "Neon/Supabase EU" item. |
| Finance widened M2 legal envelope $750 → $1,150 (DPCO retainer quote still pending) | finance_pnl §0, §2.3 | One open ask to CEO partially answered. R-06 narrows from "budget is light" to "envelope widened but DPCO retainer not yet quoted." |
| Marketing drafted three execution-layer pieces: discovery call script, objection-handling playbook, segment outreach variants (incl. healthcare) | marketing/strategy_memo mid-sprint update; marketing/{discovery_call_script,objection_handling_playbook,segment_outreach_variants}.md | New verbal/written content goes live the moment NDPR clears. Surfaces three new risks: founder talking points before the pack lands (**R-12**), healthcare segment scope (**R-13**), forwardable pilot summary (**R-14**). |
| T-5 days to the 2026-05-21 counsel-instruction deadline | company_state Active blockers; marketing strategy_memo critical-path note | Cascade is now concrete: Marketing's 2026-05-28 send slips, Dev B4/0.9 stays blocked, pilot #1 onboarding slides into Sprint 3. See new risk **R-15**. |

R-01 through R-10 from cycle 2026-05-14 carry unchanged unless noted below.

---

## Top risk

**NovaMesh will ingest third-party financial PII (SME customer names, account details, transaction narrations from bank/mobile-money statements) before a legal entity exists, before the Nigeria Data Protection Commission (NDPC) is notified, and before any signed Data Processing Agreement (DPA) is in place with pilot customers.** Dev's B4 blocker and Marketing's pilot data-sharing clause both depend on this gap being closed. Under the Nigeria Data Protection Act 2023 (NDPA), a controller-of-major-importance designation kicks in once processing exceeds ~2,000 data subjects in a rolling 12-month window — easily crossed by two pilots whose invoice books contain hundreds of customers each. Worst case before M2 pilot data lands: regulator-imposed remedial order or fine (up to ₦10m or 2% of annual gross revenue, whichever is higher), personal liability for the founder on any pilot contract signed pre-incorporation, and a pilot customer indemnity claim if a leak occurs on a single-tenant deploy without contractual liability caps. Practical fix: incorporate, register, and paper the pilot relationships **before** the first byte of real customer data is uploaded — not in parallel with it.

**Acuity ratchet for this revision (2026-05-16):** with only 5 calendar days to the 2026-05-21 counsel-instruction deadline and Marketing already drafting outbound content that assumes NDPR clearance, the legal pack has graduated from "critical path" to "single-point-of-failure for the cycle." Any slip past 2026-05-19 (a 2-day cushion before the formal deadline) should trigger CEO-level escalation, not silent absorption (see R-15).

---

## Compliance checklist (Nigerian / African SaaS, MVP stage)

### A. Corporate & contracts (blocks pilot onboarding)

- [ ] **CAC incorporation as Limited Liability Company** (Nigeria). Founder cannot sign DPAs personally without unlimited liability exposure. Owns Finance line "Incorporation / CAC fees" ($250 placeholder, M1).
- [ ] **Statutory filings post-incorporation:** TIN with FIRS, employer registration deferred until first hire.
- [ ] **Corporate bank account opened in the company's name** before any pilot invoice or pilot incentive (Finance's $60/mo voucher line) flows out.
- [ ] **Pilot Master Services Agreement (MSA)** with: scope, "AS-IS, no SLA" for MVP, mutual liability cap (recommend cap at fees paid in last 12 months OR ₦5m for free pilots), termination-for-convenience by either party, and an **express written grandfathered-pricing clause** for the post-pilot conversion (Marketing's offer is currently verbal — unenforceable as-is).
- [ ] **Mutual NDA** signed before any pilot shares invoice/statement samples (covers Dev's B2 fixture-data ask).
- [ ] **Data Processing Agreement (DPA)** as a schedule to the MSA, mirroring NDPA 2023 controller/processor split: NovaMesh is the **processor**, the pilot SME is the **controller**.
- [ ] **Contractor IP assignment + confidentiality** clause for the M3 design contractor (Finance §2.4). Without it, design output is not owned by NovaMesh. *Contractor now lands in M2, not M3 — Finance pulled forward (finance_pnl §2.4). IP assignment must be in place before contractor's first deliverable in M2, not M3.*

### B. Data protection — NDPA 2023 / NDPC

- [ ] **Engage a licensed DPCO** for the registration filing and the first data-audit (Finance's M2 line widened from $400 → $700; expect ₦600k–₦1.2m in practice for SaaS handling financial data depending on scope). DPCO retainer quote remains the unanchored variable.
- [ ] **Appoint a Data Protection Officer (DPO) — documented designation, not informal.** Founder is the named DPO for pre-revenue stage; designation letter + contact email must be on file and included in the NDPC notification packet (controller-of-major-importance treatment elevates DPO from a "soft" item to a filing requirement).
- [ ] **File NDPC notification** before crossing the controller-of-major-importance threshold (~2,000 data subjects). Two pilots × an SME invoice book of 200–500 customers each crosses this in the first ingestion batch — treat as triggered from day one.
- [ ] **Publish a Privacy Notice** on the marketing site covering: categories of data processed (incl. third parties named in narrations), lawful basis (contract / legitimate interest for B2B), retention, data subject rights, cross-border transfer.
- [ ] **Acceptable Use Policy** that contractually pushes responsibility onto the pilot for ensuring its own end-customers were notified about reconciliation processing — closes the third-party-in-narration data subject gap (NovaMesh cannot get individual consent from a name appearing in a bank statement).
- [ ] **Cross-border transfer cover — Neon specifically (TD-009 update).** Provision the pilot Neon Postgres in **EU region (Frankfurt)**; Neon's branched staging branch inherits the parent region. For other vendors:
  - Vercel (US) — accept their DPA with SCCs.
  - Sentry (US, deferred to M3 per finance §2.1) — accept SCC-bearing DPA before turning the service on.
  - Fly.io — provision in **`fra` (Frankfurt) or `lhr` (London)** region for pilot services, not the US default.
  - Document each transfer mechanism in the internal data map.
- [ ] **Sub-processor list** maintained and disclosed to pilots in the DPA appendix. Seed list as of this cycle: Neon (DB, EU), Vercel (frontend hosting, US w/ SCC), Fly.io (backend hosting, EU after provisioning fix), Google Workspace (email, US w/ SCC), Sentry (error monitoring, deferred to M3), Instantly (outbound email tool, US — call-note PII risk, see R-12), LinkedIn Sales Navigator (prospect data, US — first-party ICP research only).
- [ ] **Breach notification SOP** drafted: NDPA requires notice to NDPC within 72 hours of awareness of a personal data breach with risk to data subjects.
- [ ] **Data-subject-rights workflow** (access / correction / erasure / objection). For MVP this can be a documented inbox SOP, not a UI feature, but the inbox must exist before pilot data lands.
- [ ] **Audit log retention & minimisation policy (new, ties to TD-008).** The new `audit_events` table writes `before`/`after` JSONB on every state transition on `invoices`, `statement_lines`, and `matches` — i.e. potentially names, narrations, and amounts. Policy must specify: (i) retention aligns with the underlying record's CAMA 6-yr obligation for *transaction-linked* rows (invoice/statement/match data) only; (ii) audit rows that reference records erased under a valid NDPA erasure request must themselves be PII-minimised (hash/tombstone the `before`/`after` payloads, retain the immutable action/timestamp/actor) so audit immutability does not undermine the erasure right; (iii) DPCO sign-off on this policy before pilot #1 onboarding. See R-11.

### C. Security baseline (Dev task 0.9, coordinate with engineering)

- [ ] **Encryption at rest** on Postgres (Neon default) and on object storage if added later.
- [ ] **Encryption in transit** (TLS) end-to-end including admin tools.
- [ ] **Access control:** named admin accounts only — no shared credentials. 2FA mandatory (Finance already budgets a password manager).
- [ ] **Audit log retention policy** defined per item B above. Minimum 6 years for transaction-linked records (CAMA accounting records rule applied conservatively to reconciliation outputs); align with NDPA erasure-right exceptions for legal/accounting obligation; PII-minimise audit rows whose underlying record was erased.
- [ ] **Backups** with documented restore test before pilot cohort 1 onboards (M2). Backups also fall under NDPA — encrypted + access-controlled.
- [ ] **TD-005 single-tenant posture is a compliance asset** — keep it. Smaller blast radius materially reduces breach-notification exposure. Document the migration plan to row-level tenancy as a future change-control item.
- [ ] **Penetration / vulnerability assessment** before paid revenue starts. Not required at MVP, but DPCO audit will ask for the plan.

### D. Sectoral & financial-services boundary

- [ ] **CBN licensing — not currently required.** NovaMesh reads bank statement exports and matches them; it does not initiate, hold, or settle funds. **Do not market as a "payments" product.** Pitch deck and website copy must say "reconciliation," not "payments" or "settlement."
- [ ] **If v2 adds Paystack / Flutterwave integration** (Dev task 0.8), it remains processor-only (read-only access to transaction data via PSP-issued API keys) — still no CBN licensing needed, but each integration has its own data-handling terms that must be reviewed and incorporated into the sub-processor list.
- [ ] **Mobile-money data (MTN MoMo, OPay)** is regulated as payment service data by CBN. Read-only ingestion via customer-supplied statement export is fine; do **not** screen-scrape from operator portals.
- [ ] **Healthcare segment variant — explicit scope guardrail (new).** Marketing's segment outreach variant for healthcare must scope the offer to **invoice/payment-statement reconciliation only**; it must NOT imply NovaMesh handles patient records, HMO claims, clinical data, or anything covered by NHIA / Nigeria Health Act 2014. Legal review the healthcare body copy before its first send. See R-13.

### E. Marketing & outbound (coordinate with Marketing agent)

- [ ] **Cold B2B email under NDPA:** permitted on a legitimate-interest basis but requires (i) a clear unsubscribe mechanism in every message, (ii) sender identification, (iii) no purchased/scraped consumer lists. LinkedIn Sales Navigator-sourced ICP contacts at named companies are acceptable. **Add an opt-out footer to Marketing's outreach template before the first send.**
- [ ] **"6 months free + grandfathered pricing"** must be reduced to writing in the pilot MSA (see Section A). A verbal offer that the company later cannot honor is a misrepresentation risk.
- [ ] **Founder talking-points one-pager — gap-filler, ships this week (new).** Marketing's objection-handling playbook lists "NDPR/data" as objection #3, which the founder will field verbally in discovery calls *before* the legal pack is signed. Produce a short Legal-approved one-pager covering exactly what the founder may and may not claim verbally about NovaMesh's data posture, NDPC status, sub-processors, and incident response, so verbal answers do not constitute misrepresentation. See R-12.
- [ ] **Discovery-call notes — light-touch processing record (new).** The discovery call script collects prospect name, role, company, willingness-to-pay band, and quoted pain points. Store call notes in a documented system (not a personal note-taking app), retain ≤24 months, and include a one-liner in the email/calendar invite consistent with the published Privacy Notice ("calls may be note-taken for product-discovery purposes"). No recording without explicit consent.
- [ ] **Forwardable pilot summary — next cycle, Legal review gated (new).** Marketing flagged a forwardable one-page pilot summary as a next-cycle deliverable. Because it will be evaluated by external decision-makers (CEO/MD/accountant) who will ask compliance questions, Legal must review before any external circulation. Pre-commit to that review in the next cycle so it doesn't become a last-minute gate. See R-14.

### F. Pricing-model legal lens (input to CEO)

- [x] **Flat tiered (TD-006) confirmed by CEO/Finance this cycle.** Lower-risk posture confirmed; tier amounts (NGN 25k / 75k / 250k) still placeholder pending Marketing's discovery-call data (2026-06-04). No further legal action on the *model*; the MSA must lock the *contractual mechanic* (flat monthly recurring, tier-by-volume) without committing specific tier amounts in the pilot agreement.

### G. Market-scope decision (input to CEO)

- [x] **Nigeria-first confirmed by CEO this cycle through Sprint 4 / first 3 paying customers.** POPIA / Kenya DPA 2019 / Ghana DPA 2012 scoping shelved until then. Standing position carried.

---

## Risks flagged this cycle (delta)

- **R-01 — R-10:** carried unchanged from cycle 2026-05-14 except R-06 narrows (Finance widened M2 envelope to $1,150; remaining unknown is the DPCO retainer quote, not the envelope).
- **R-11 — Audit log retention conflict (new).** TD-008's `audit_events` writes `before`/`after` JSONB on every state transition. Without an explicit minimisation rule, audit rows preserve PII (customer names, narrations) past any erasure request and past the underlying record's lifecycle. Fix: PII-minimise audit payloads referencing erased records (retain action + actor + timestamp; tombstone the data). Get DPCO sign-off before pilot #1 onboarding.
- **R-12 — Verbal misrepresentation window (new).** Marketing's discovery-call script + objection playbook will land NDPR-adjacent claims in founder-led calls before the legal pack is signed. Fix: a one-page "what the founder may say" memo, Legal-approved, before the first discovery call books (target: end of this week, 2026-05-22).
- **R-13 — Healthcare segment scope creep (new).** Healthcare variant in segment outreach risks implying NovaMesh handles patient/clinical data. Fix: Legal-review the healthcare body copy and explicitly bound the offer to invoice/payment-statement reconciliation. Block send until cleared.
- **R-14 — Forwardable pilot summary (deferred, flagged now).** Marketing's next-cycle one-pager will circulate to external decision-makers and trigger compliance questions. Fix: Legal review pre-committed for next cycle, not retrofitted under deadline pressure.
- **R-15 — Counsel-instruction deadline cascade (new, time-sensitive).** T-5 days to 2026-05-21. If counsel is not instructed by **2026-05-19 (2-day cushion)**, escalate to CEO weekly report immediately. Cascade: Marketing 2026-05-28 send slips → Dev B2 dataset deadline 2026-06-07 slips → Sprint 2 pilot #1 onboarding (mid-M2) slides into Sprint 3 → Finance M2 GTM cost shape shifts right by ~1 month (per finance_pnl §5 risk #3). No silent absorption: name it in the weekly report.

---

## Recommended next action

**Before Sprint 1 ends (2026-06-12), complete a "pilot-ready legal pack" gating Marketing's first pilot signature and Dev's task 0.9 sign-off. The 2026-05-21 deadline is now a 5-day clock and is the single point of failure for this cycle.**

1. **By end-of-day 2026-05-19 (2-day cushion before deadline):** instruct counsel to (a) file CAC incorporation, (b) draft the pilot MSA + DPA + mutual NDA from a single template set, (c) draft the Privacy Notice and Acceptable Use Policy, (d) draft contractor IP assignment + confidentiality clause (M2 contractor moved forward — was M3). Confirm the legal budget envelope with Finance ($1,150 M2 line now reflects the widened range; DPCO retainer quote still needed to firm it up).
2. **This week (by 2026-05-22):** publish the Legal-approved founder talking-points one-pager (R-12) so the discovery-call calendar can open without verbal-misrepresentation exposure. Coordinate with Marketing on the healthcare segment body-copy review (R-13).
3. **By 2026-05-23 (Dev coordination):** instruct Dev to provision the Neon Postgres pilot DB in **EU `fra` (Frankfurt)** region, and the Fly.io backend services likewise in `fra`/`lhr`. Capture in the cross-border data map (R-05).
4. **M2 (June):** engage DPCO, file NDPC notification (with named-DPO designation letter on file), publish Privacy Notice on the marketing site **before** the first pilot upload. Accept and file SCC-bearing vendor DPAs (Vercel, GitHub, Sentry, Fly.io). Finalise audit-log retention & minimisation policy (R-11) with DPCO sign-off ahead of pilot #1 onboarding (mid-M2).
5. **Gate:** Dev's B4 (data-handling baseline / task 0.9) and Marketing's first pilot signature both block on items 1–4 above. **Escalate to CEO weekly report this cycle if counsel is not instructed by 2026-05-19** so the M2 pilot ramp does not slip silently on legal readiness that could have been de-risked in M1 (R-15).
