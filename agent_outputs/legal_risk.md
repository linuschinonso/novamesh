# Legal — Risk Assessment & Compliance Checklist

Cycle date: 2026-05-14
Owner: Legal agent
Stage: Pre-revenue MVP build (Nigeria-first SaaS, B2B invoice reconciliation)

---

## Top risk

**NovaMesh will ingest third-party financial PII (SME customer names, account details, transaction narrations from bank/mobile-money statements) before a legal entity exists, before the Nigeria Data Protection Commission (NDPC) is notified, and before any signed Data Processing Agreement (DPA) is in place with pilot customers.** Dev's B4 blocker and Marketing's pilot data-sharing clause both depend on this gap being closed. Under the Nigeria Data Protection Act 2023 (NDPA), a controller-of-major-importance designation kicks in once processing exceeds ~2,000 data subjects in a rolling 12-month window — easily crossed by two pilots whose invoice books contain hundreds of customers each. Worst case before M2 pilot data lands: regulator-imposed remedial order or fine (up to ₦10m or 2% of annual gross revenue, whichever is higher), personal liability for the founder on any pilot contract signed pre-incorporation, and a pilot customer indemnity claim if a leak occurs on a single-tenant deploy without contractual liability caps. Practical fix: incorporate, register, and paper the pilot relationships **before** the first byte of real customer data is uploaded — not in parallel with it.

---

## Compliance checklist (Nigerian / African SaaS, MVP stage)

### A. Corporate & contracts (blocks pilot onboarding)

- [ ] **CAC incorporation as Limited Liability Company** (Nigeria). Founder cannot sign DPAs personally without unlimited liability exposure. Owns Finance line "Incorporation / CAC fees" ($250 placeholder, M1).
- [ ] **Statutory filings post-incorporation:** TIN with FIRS, employer registration deferred until first hire.
- [ ] **Corporate bank account opened in the company's name** before any pilot invoice or pilot incentive (Finance's $60/mo voucher line) flows out.
- [ ] **Pilot Master Services Agreement (MSA)** with: scope, "AS-IS, no SLA" for MVP, mutual liability cap (recommend cap at fees paid in last 12 months OR ₦5m for free pilots), termination-for-convenience by either party, and an **express written grandfathered-pricing clause** for the post-pilot conversion (Marketing's offer is currently verbal — unenforceable as-is).
- [ ] **Mutual NDA** signed before any pilot shares invoice/statement samples (covers Dev's B2 fixture-data ask).
- [ ] **Data Processing Agreement (DPA)** as a schedule to the MSA, mirroring NDPA 2023 controller/processor split: NovaMesh is the **processor**, the pilot SME is the **controller**.
- [ ] **Contractor IP assignment + confidentiality** clause for the M3 design contractor (Finance §2.4). Without it, design output is not owned by NovaMesh.

### B. Data protection — NDPA 2023 / NDPC

- [ ] **Engage a licensed DPCO** for the registration filing and the first data-audit (the $400 Finance M2 line is a floor, not a ceiling — expect ₦600k–₦1.2m in practice for SaaS handling financial data, depending on scope).
- [ ] **Appoint a Data Protection Officer (DPO).** Can be the founder for pre-revenue stage; must be a named individual with documented contact.
- [ ] **File NDPC notification** before crossing the controller-of-major-importance threshold (~2,000 data subjects). Two pilots × an SME invoice book of 200–500 customers each crosses this in the first ingestion batch — treat as triggered from day one.
- [ ] **Publish a Privacy Notice** on the marketing site covering: categories of data processed (incl. third parties named in narrations), lawful basis (contract / legitimate interest for B2B), retention, data subject rights, cross-border transfer.
- [ ] **Acceptable Use Policy** that contractually pushes responsibility onto the pilot for ensuring its own end-customers were notified about reconciliation processing — closes the third-party-in-narration data subject gap (NovaMesh cannot get individual consent from a name appearing in a bank statement).
- [ ] **Cross-border transfer cover.** Vercel (US), Neon/Supabase (US default), Sentry (US), Render/Fly (US/EU) all transfer data outside Nigeria. NDPA s.41 requires adequacy or appropriate safeguards. Pick one path per vendor:
  - Standard Contractual Clauses (SCCs) in the vendor DPA (Vercel, Sentry, GitHub publish DPAs with SCCs — accept them).
  - Provision Neon/Supabase in **EU region** (closest adequacy posture; better than US-East default).
  - Document the transfer mechanism in the internal data map.
- [ ] **Sub-processor list** maintained and disclosed to pilots in the DPA appendix.
- [ ] **Breach notification SOP** drafted: NDPA requires notice to NDPC within 72 hours of awareness of a personal data breach with risk to data subjects.
- [ ] **Data-subject-rights workflow** (access / correction / erasure / objection). For MVP this can be a documented inbox SOP, not a UI feature, but the inbox must exist before pilot data lands.

### C. Security baseline (Dev task 0.9, coordinate with engineering)

- [ ] **Encryption at rest** on Postgres (Neon/Supabase default) and on object storage if added later.
- [ ] **Encryption in transit** (TLS) end-to-end including admin tools.
- [ ] **Access control:** named admin accounts only — no shared credentials. 2FA mandatory (Finance already budgets a password manager).
- [ ] **Audit log retention policy** defined: minimum 6 years for transaction-linked records (CAMA accounting records rule applied conservatively to reconciliation outputs); align with NDPA erasure-right exceptions for legal/accounting obligation.
- [ ] **Backups** with documented restore test before pilot cohort 1 onboards (M2). Backups also fall under NDPA — encrypted + access-controlled.
- [ ] **TD-005 single-tenant posture is a compliance asset** — keep it. Smaller blast radius materially reduces breach-notification exposure. Document the migration plan to row-level tenancy as a future change-control item.
- [ ] **Penetration / vulnerability assessment** before paid revenue starts. Not required at MVP, but DPCO audit will ask for the plan.

### D. Sectoral & financial-services boundary

- [ ] **CBN licensing — not currently required.** NovaMesh reads bank statement exports and matches them; it does not initiate, hold, or settle funds. **Do not market as a "payments" product.** Pitch deck and website copy must say "reconciliation," not "payments" or "settlement."
- [ ] **If v2 adds Paystack / Flutterwave integration** (Dev task 0.8), it remains processor-only (read-only access to transaction data via PSP-issued API keys) — still no CBN licensing needed, but each integration has its own data-handling terms that must be reviewed and incorporated into the sub-processor list.
- [ ] **Mobile-money data (MTN MoMo, OPay)** is regulated as payment service data by CBN. Read-only ingestion via customer-supplied statement export is fine; do **not** screen-scrape from operator portals.

### E. Marketing & outbound (coordinate with Marketing agent)

- [ ] **Cold B2B email under NDPA:** permitted on a legitimate-interest basis but requires (i) a clear unsubscribe mechanism in every message, (ii) sender identification, (iii) no purchased/scraped consumer lists. LinkedIn Sales Navigator-sourced ICP contacts at named companies are acceptable. **Add an opt-out footer to Marketing's outreach template before the first send.**
- [ ] **"6 months free + grandfathered pricing"** must be reduced to writing in the pilot MSA (see Section A). A verbal offer that the company later cannot honor is a misrepresentation risk.

### F. Pricing-model legal lens (input to CEO)

- [ ] **Flat tiered (Dev TD-006 / Finance §1.1) is the lower-risk model.** A "% of invoices processed" model can be read as transaction-linked pricing and creates needless ambiguity with CBN-regulated activities even though the product itself is not payment processing. Recommend confirming the flat-tiered model on legal grounds in addition to the commercial grounds Dev and Finance already raised.

### G. Market-scope decision (input to CEO)

- [ ] **Nigeria-first is the right legal posture.** Pan-Africa expansion adds, per jurisdiction: South Africa (POPIA + Information Regulator registration), Kenya (Data Protection Act 2019 + ODPC registration), Ghana (DPA 2012 + DPC registration), each with separate cross-border-transfer rules. Defer until at least 3 paying customers in Nigeria.

---

## Recommended next action

**Before Sprint 1 ends (2026-06-12), complete a "pilot-ready legal pack" gating Marketing's first pilot signature and Dev's task 0.9 sign-off:**

1. **This week (M1, by 2026-05-21):** instruct counsel to (a) file CAC incorporation, (b) draft the pilot MSA + DPA + mutual NDA from a single template set, (c) draft the Privacy Notice and Acceptable Use Policy. Lock the legal budget envelope with Finance (the current $750 M2 line is light — expect $1,500–$2,500 across M1–M2 once DPCO retainer is real).
2. **M2 (June):** engage DPCO, file NDPC notification, appoint founder as DPO, publish Privacy Notice on the marketing site **before** the first pilot upload. Reconfigure Neon/Supabase to EU region if not already. Accept and file SCC-bearing vendor DPAs (Vercel, GitHub, Sentry, Render).
3. **Gate:** Dev's B4 (data-handling baseline) and Marketing's first pilot signature both block on items 1 and 2 above. Surface this gate to the CEO this cycle so the M2 pilot ramp does not slip on legal readiness it could have de-risked in M1.
