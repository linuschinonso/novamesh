# Legal Memory

Last updated: 2026-05-14

## Risks flagged this cycle (2026-05-14)

### R-01 — Pre-incorporation data ingestion (CRITICAL, blocks M2)
Marketing's M2 pilot onboarding will land before CAC incorporation and NDPC notification complete. Founder would otherwise sign DPAs in a personal capacity → unlimited personal liability + regulatory exposure. **Gate:** no real pilot data uploaded until incorporation + DPCO retainer + signed pilot MSA/DPA are in place.

### R-02 — Verbal "6 months free + grandfathered pricing" offer
Marketing's outbound offer is unenforceable as a verbal promise. Must be written into the pilot MSA before any cold-email recipient acts on it. Misrepresentation risk if company later cannot honor.

### R-03 — NDPA controller-of-major-importance threshold
~2,000 data subjects / 12 months. Two pilots' invoice books cross this on first ingestion. Treat NDPC notification as triggered from day-one of pilot data landing, not as a "later" item.

### R-04 — Third-party data subjects in statement narrations
Bank/mobile-money narrations contain names of parties NovaMesh has no relationship with. Cannot get individual consent. Mitigation = contractually push notice obligation onto pilot SME via Acceptable Use Policy.

### R-05 — Cross-border data transfer (Vercel / Neon / Supabase / Sentry / Render)
All default-US-hosted. NDPA s.41 requires SCCs or EU-region provisioning. Action: provision DB in EU region; accept vendor DPAs with SCCs.

### R-06 — Finance legal budget is light
Finance line "NDPR DPCO registration & data audit" = $400 in M2. Realistic floor is ₦600k–₦1.2m (~$360–$730 at 1,650 NGN/USD) for DPCO retainer + audit on financial-data SaaS. Add MSA/DPA/Privacy Notice drafting cost on top. Surfaced to Finance for M2 envelope reset.

### R-07 — % invoice pricing model carries CBN-adjacency optics risk
Transaction-linked pricing on a product that reads payment data can be misread as payment processing. Flat tiered is the cleaner legal posture; aligns with Dev TD-006 and Finance §1.1.

### R-08 — Pan-Africa expansion multiplies compliance regimes
POPIA (SA), DPA 2019 (Kenya), DPA 2012 (Ghana), etc. Each needs separate registration + transfer mechanism. Nigeria-first is the right legal posture for at least the first 3 paying customers.

### R-09 — Contractor IP gap (M3 designer)
Finance's M3 contractor line ($300) needs IP assignment + confidentiality clauses, otherwise designer owns the output.

### R-10 — No SLA / liability cap in pilot contract = open-ended exposure
Single-tenant deploy reduces blast radius (good), but a breach on one pilot without contractual cap could exceed pre-revenue cash on hand. Hard cap required in MSA.

## Standing positions (carry forward)

- **NovaMesh is a data processor, not a controller** for pilot data. Pilot SME is the controller.
- **NovaMesh is not a payment service.** Do not let marketing/website copy drift toward "payments" or "settlement" language. CBN licensing not required as long as we stay read-only on financial data.
- **DPO** designated as the founder for pre-revenue stage. Revisit when first compliance hire happens.
- **Single-tenant per pilot (Dev TD-005) is a compliance asset.** Don't migrate to row-level tenancy purely for cost reasons — keep until the legal pack supports the wider blast radius.
- **CAMA accounting-record retention** (6 years) applies to reconciliation outputs; this beats NDPA erasure for transaction records (legal-obligation exception).

## Open asks to CEO this cycle

1. Confirm pre-Sprint-1 legal budget envelope ($1,500–$2,500 across M1–M2 for incorporation + DPCO + contract drafting), to reset Finance's M2 legal line.
2. Confirm Nigeria-first market scope so we can stop scoping POPIA/Kenya/Ghana regimes speculatively.
3. Confirm flat-tiered pricing (vs % of invoices) so Legal can lock the commercial terms in the pilot MSA template.

## Next-cycle agenda

- DPCO shortlist + retainer signed.
- Pilot MSA + DPA + NDA + Privacy Notice + AUP drafted and circulated to Dev (B4) and Marketing.
- Cross-border data map filled in once Dev confirms vendor regions.
- Sub-processor list seeded from Dev TD-001 + Finance §2.1 + §2.2.
