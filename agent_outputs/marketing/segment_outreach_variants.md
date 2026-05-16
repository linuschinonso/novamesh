# Segment-tailored outreach variants — Pilot recruitment

**Audience:** Five Nigerian SME segments from the target list in `cold_outreach_pilot_email.md`.
**Format:** Drop-in body replacements for the base cold email. Subject lines, sign-off, and follow-up cadence are unchanged from the base template.
**Cycle:** 2026-05-14 → 2026-05-28 (50 emails sent), 2026-06-04 (10 calls booked).
**Why these exist:** The base email is generic. With 10 sends per segment, segment-specific pain references (3PL drivers, school termly billing, distributor part-pays) outperform a generic "your team reconciles invoices" line because they signal we know the segment. Memory: *"specificity earns instant credibility. Generic copy reads as just another foreign vendor."*

---

## Shared elements (do not change per segment)

- **Subject line A/B test:** same three from base template.
- **Sign-off:** same as base.
- **Personalisation slots:** `[First name]`, `[Company]`, `[specific reason]`, `[Founder name]` — fill all four before sending.
- **Follow-up cadence:** Day 0 → Day 4 → Day 11 → stop.
- **Send window:** Tue/Wed, 09:30–11:00 WAT.
- **NDPR:** outbound is blocked on Legal sign-off. Do not send any variant until Legal clears the data-handling clause.

Each variant replaces only the **body** of the base email — keep the email under 180 words.

---

## 1. Logistics / haulage (2 of 10 first cohort)

**Why this segment:** High invoice volume, large fleet of repeat customers, complex partial payments for staged deliveries. Stresses the matcher on repeat-customer detection.

**Body:**

> Hi [First name],
>
> I'm [Founder name] — building NovaMesh, a tool that automates invoice-to-payment matching for Nigerian logistics and haulage businesses. Reaching out because [specific reason].
>
> Quick one: when a customer like [example shipper] pays half an invoice on dispatch and the other half on delivery, how long does it take your team to figure out the second payment is for the same job? We've seen logistics SMEs spend a full day a week just chasing this for partial settlements.
>
> We're piloting with 10 Nigerian SMEs. The deal:
>
> - You share one month of anonymised invoices + bank/MoMo statements (NDA first).
> - We run the matcher and walk you through where it lands.
> - If useful, six months free. If not, you've spent 30 minutes and we've learned where it breaks on staged-payment data.
>
> Worth 20 minutes next week? Tuesday 10:00 or Thursday 14:00 WAT.
>
> Thanks for reading.

---

## 2. B2B services / agencies (2 of 10)

**Why this segment:** Lower invoice count, larger ticket sizes, recurring monthly retainers. Stresses the matcher on retainer vs. project-fee disambiguation for the same client.

**Body:**

> Hi [First name],
>
> I'm [Founder name] — building NovaMesh, a tool that automates invoice-to-payment matching for Nigerian B2B agencies and services firms. Reaching out because [specific reason].
>
> Question: when a retainer client pays you in the same month as a one-off project invoice — same bank, same narration pattern — how does your team tell the two payments apart? We've heard finance leads at services firms say this is the single most time-consuming part of their month-end.
>
> We're piloting with 10 Nigerian SMEs. The deal:
>
> - You share one month of anonymised invoices + bank statements (NDA first).
> - We match them and walk you through the result.
> - If useful, six months free. If not, you've spent 30 minutes and we've learned where it breaks on retainer-heavy data.
>
> Worth 20 minutes next week? Tuesday 10:00 or Thursday 14:00 WAT.
>
> Thanks for reading.

---

## 3. Wholesale / distribution (2 of 10)

**Why this segment:** Many customers, lots of small partial payments, MoMo-heavy. Stresses the matcher on partial-payment aggregation and MoMo narrations.

**Body:**

> Hi [First name],
>
> I'm [Founder name] — building NovaMesh, a tool that automates invoice-to-payment matching for Nigerian wholesale and distribution businesses. Reaching out because [specific reason].
>
> One question: when a customer pays a ₦1.2M invoice as three MoMo transfers across two weeks — none of them tagged with an invoice number — how long does it take your team to confirm the invoice is fully settled? Most distributors we've spoken with say this single workflow eats 8–10 hours a week.
>
> We're piloting with 10 Nigerian SMEs. The deal:
>
> - You share one month of anonymised invoices + bank/MoMo statements (NDA first).
> - We run the matcher and walk you through where it lands on partial payments.
> - If useful, six months free. If not, you've spent 30 minutes and we've learned where it breaks.
>
> Worth 20 minutes next week? Tuesday 10:00 or Thursday 14:00 WAT.
>
> Thanks for reading.

---

## 4. Schools / training providers (2 of 10)

**Why this segment:** Termly billing cycles, parent-payer vs. student-account mismatch, mixed cash deposit + transfer. Stresses matcher on payer-vs-payee identity resolution.

**Body:**

> Hi [First name],
>
> I'm [Founder name] — building NovaMesh, a tool that automates invoice-to-payment matching for Nigerian schools and training providers. Reaching out because [specific reason].
>
> Question: at the start of term, when 200 parents pay school fees via transfer — and the bank narration shows the parent's account, not the child's — how does your bursar tie each payment to the right student account? We've heard this is the single most stressful week of the term for finance teams in education.
>
> We're piloting with 10 Nigerian SMEs. The deal:
>
> - You share one term of anonymised invoices + bank statements (NDA first).
> - We run the matcher and walk you through the result.
> - If useful, six months free + grandfathered pricing. If not, 30 minutes lost and we've learned where it breaks on fee-payment data.
>
> Worth 20 minutes next week? Tuesday 10:00 or Thursday 14:00 WAT.
>
> Thanks for reading.

---

## 5. Healthcare / clinics (2 of 10)

**Why this segment:** Mixed payer base (HMO/insurance B2B + walk-in B2C), HMO claim cycles, retroactive payments. Stresses matcher on long-tail reconciliation (90+ days) and mixed payer-class detection.

**Body:**

> Hi [First name],
>
> I'm [Founder name] — building NovaMesh, a tool that automates invoice-to-payment matching for Nigerian clinics and healthcare providers. Reaching out because [specific reason].
>
> Quick one: when an HMO settles 60 days of patient claims in a single lump transfer to your bank — no breakdown attached — how does your team allocate that payment across the right patient invoices? Most clinics we've spoken with say HMO reconciliation alone eats 10+ hours a week of a finance officer's time.
>
> We're piloting with 10 Nigerian SMEs. The deal:
>
> - You share one month of anonymised invoices + bank statements (NDA first).
> - We run the matcher and walk you through where it lands on HMO + walk-in data.
> - If useful, six months free. If not, 30 minutes lost and we've learned where it breaks.
>
> Worth 20 minutes next week? Tuesday 10:00 or Thursday 14:00 WAT.
>
> Thanks for reading.

---

## Routing rules (founder)

- Always pick the variant by the prospect's primary segment, not their secondary. A 3PL that also operates a small wholesale arm = logistics variant.
- If the prospect is genuinely cross-segment (logistics + warehouse + retail), default to the variant for the segment with the higher invoice volume.
- If unsure, send the base template (`cold_outreach_pilot_email.md`). A generic-but-personalised email beats a wrong-segment-but-specific one.

## What to track (per send)

In the outreach tracker, log:
- Variant used (1–5 or base).
- Reply rate by variant.
- Call-booked rate by variant.

Cycle review at 25 sends and 50 sends. If one variant doubles another's reply rate, drop the underperformer and reallocate sends.
