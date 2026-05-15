# Dev Backlog — NovaMesh

Cycle date: 2026-05-14
Owner: Dev agent
Stage: Pre-revenue MVP build

---

## Product framing (working definition)

NovaMesh is a B2B SaaS tool that ingests an SME's invoices and bank/mobile-money statements, matches them automatically, and flags exceptions for human review. Target user: an accountant or finance lead at an African SME (10–200 employees) currently doing reconciliation manually in Excel.

The MVP must answer one question end-to-end: **"Given this batch of invoices and this bank statement, which invoices are paid, which are unpaid, and which payments are unattributed?"**

---

## Current sprint (Sprint 0 — Foundations, 2026-05-14 → 2026-05-28)

| # | Task | Status | Notes |
|---|------|--------|-------|
| 0.1 | Lock MVP scope to single-tenant, single-currency (NGN) reconciliation | todo | Blocks every other spec. Needs CEO sign-off before sprint 1. |
| 0.2 | Spec the invoice data model (fields, formats, validation rules) | todo | See "Specs" → invoice schema below. |
| 0.3 | Spec the statement data model (bank CSV + mobile money formats) | todo | Cover at minimum: GTBank, Access, Zenith CSV exports; MTN MoMo, OPay statement formats. |
| 0.4 | Decide ingestion path for MVP: CSV upload vs. email forward vs. API | todo | Recommend CSV upload only for MVP. Email/API in v2. |
| 0.5 | Pick reconciliation matching algorithm v1 | todo | Recommend rules-based: exact amount + date window + reference token match. ML later. |
| 0.6 | Choose stack and scaffold repo | todo | See "Technical decisions" → TD-001. |
| 0.7 | Define exception-handling UX (reviewer queue) | todo | Pseudocode in "Specs" section below. |
| 0.8 | Research v2 integrations (Paystack, Flutterwave, Quickbooks Africa) | todo | Research only this sprint, not build. |
| 0.9 | Draft a security/data-handling baseline (encryption at rest, PII boundary, audit log) | todo | Coordinate with Legal agent before any pilot data lands. |

---

## Technical decisions made this cycle

### TD-001 — Stack
- **Backend:** Python 3.12 + FastAPI. Reason: fast iteration, strong CSV/Excel tooling (pandas), team familiarity, deploys cheaply on Render/Fly.
- **DB:** PostgreSQL (managed, e.g. Neon or Supabase). Reason: relational data fits invoices/statements; JSONB columns cover the messy parts of statement rows.
- **Frontend:** Next.js + TypeScript + Tailwind. Reason: one framework covers marketing site and app; cheap to host on Vercel pre-revenue.
- **Queue/jobs:** Defer. Use synchronous request handling for MVP. Add RQ or Celery only when a customer batch exceeds ~30s of processing.

### TD-002 — Reconciliation algorithm v1 (rules-based)
For each invoice `I` and each statement line `S`:
1. Hard match if `S.amount == I.total` AND `S.date ∈ [I.issue_date, I.due_date + 14d]` AND (`I.invoice_number` substring of `S.narration` OR `I.customer_name` token overlap with `S.narration` ≥ 1 token).
2. Soft match (flag for review) if amount matches and date is in window but no narration overlap.
3. Unmatched if no amount match.
4. Statement lines unattributed = any `S` not bound to an `I` after passes 1–2.

No ML in MVP. Track precision/recall on pilot data; revisit once we have ≥3 pilot customers' reconciled history.

### TD-003 — Single-currency MVP
NGN only. Multi-currency forces FX conversion logic, statement-level currency detection, and a settings UI we don't have time to build. Pan-Africa target is a sprint-3+ concern, and ties to the open "Nigeria first vs. pan-Africa" decision in company_state.md — Dev recommends Nigeria first.

### TD-004 — File ingestion
CSV upload only. Reject anything else with a clear error. We will provide downloadable templates for invoices and for the three target bank statement formats. Reason: parsing arbitrary bank PDFs is a 3-sprint problem on its own.

### TD-005 — Multi-tenancy posture
Build single-tenant per deployment for the first 2 pilots (separate Postgres schema per customer). Migrate to row-level tenancy with `tenant_id` once we have ≥3 customers. Reason: faster pilot setup, lower blast radius for a data leak, buys time to design RLS properly.

### TD-006 — Pricing model (input to CEO/Finance)
Dev recommendation: **flat monthly fee tiered by invoice volume** (e.g. ≤500/mo, ≤2k/mo, ≤10k/mo). Reason: % of invoices punishes the customers who benefit most and is harder to forecast for us. Final call sits with CEO + Finance.

---

## Specs (pseudocode)

### Invoice schema (Postgres)
```
invoices(
  id              uuid pk,
  tenant_id       uuid,
  invoice_number  text not null,
  customer_name   text not null,
  customer_id     uuid null,
  issue_date      date not null,
  due_date        date not null,
  currency        char(3) not null default 'NGN',
  subtotal        numeric(14,2) not null,
  tax             numeric(14,2) not null default 0,
  total           numeric(14,2) not null,
  status          text not null,          -- draft|sent|paid|partially_paid|void
  source          text not null,          -- csv_upload|manual|api
  raw_row         jsonb,                  -- original CSV row, for audit
  created_at      timestamptz default now(),
  unique (tenant_id, invoice_number)
)
```

### Statement line schema
```
statement_lines(
  id              uuid pk,
  tenant_id       uuid,
  source_account  text not null,          -- e.g. "GTBank-1234"
  posted_at       timestamptz not null,
  amount          numeric(14,2) not null, -- positive = credit, negative = debit
  narration       text,
  reference       text,
  raw_row         jsonb,
  created_at      timestamptz default now()
)
```

### Match record
```
matches(
  id                  uuid pk,
  tenant_id           uuid,
  invoice_id          uuid references invoices(id),
  statement_line_id   uuid references statement_lines(id),
  match_type          text,               -- hard|soft|manual
  confidence          numeric(3,2),       -- 0.00 .. 1.00
  reviewed_by         uuid null,
  reviewed_at         timestamptz null,
  decision            text,               -- accepted|rejected|pending
  created_at          timestamptz default now()
)
```

### Reconciliation pass (pseudocode)
```
def reconcile(tenant_id, batch_id):
    invoices = load_open_invoices(tenant_id)
    lines    = load_unmatched_credit_lines(tenant_id, batch_id)

    for inv in invoices:
        candidates = [s for s in lines
                      if s.amount == inv.total
                      and inv.issue_date <= s.posted_at.date() <= inv.due_date + 14d]
        if not candidates:
            continue

        hard = [s for s in candidates if narration_matches(inv, s)]
        if len(hard) == 1:
            write_match(inv, hard[0], type='hard', confidence=0.95)
            lines.remove(hard[0])
            continue

        # amount+date match, narration ambiguous or missing
        for s in candidates:
            write_match(inv, s, type='soft', confidence=0.6, decision='pending')

    return summary(tenant_id, batch_id)
```

### Exception queue UX
- Reviewer sees a table: Invoice | Candidate statement line(s) | Confidence | Accept / Reject / Split.
- "Split" supports one invoice paid by multiple lines (deposits, partial payments).
- Every accept/reject writes an audit row with user id + timestamp + prior state.

---

## Blockers

- **B1** — MVP scope not yet signed off by CEO. Sprint 1 cannot start until task 0.1 lands.
- **B2** — No pilot customer data. We need at least one anonymized invoice + statement pair to validate TD-002 before building the UI. Marketing agent should source this from the "first 10 target customers" effort.
- **B3** — Pricing model (TD-006) needs Finance + CEO decision. Doesn't block build, but blocks billing wiring in sprint 2.
- **B4** — Data-handling baseline (0.9) blocked on Legal agent's view on NDPR (Nigeria Data Protection Regulation) requirements for financial data.

---

## Next sprint preview (Sprint 1 — Ingestion + matching core, 2026-05-29 → 2026-06-12)

Goal: a developer-only CLI/API that ingests one CSV pair and emits a reconciliation report. No UI yet.

- S1.1 Scaffold FastAPI service + Postgres + migrations (Alembic).
- S1.2 Implement CSV parsers for invoices template + GTBank statement format.
- S1.3 Implement reconciliation pass per TD-002.
- S1.4 Output a JSON + human-readable summary (matched, soft-matched, unattributed).
- S1.5 Seed test fixtures from one anonymized pilot dataset (depends on B2).
- S1.6 Wire basic auth (single admin user, no multi-tenant UI yet).
- S1.7 Integration tests against real CSVs, not mocks.

Sprint 2 (provisional): minimal Next.js UI for upload + exception queue + accept/reject.
Sprint 3 (provisional): second bank format + first pilot onboarding.

---

## Decision log (running)

| ID | Decision | Reason | Date |
|----|----------|--------|------|
| TD-001 | Python/FastAPI + Postgres + Next.js | Iteration speed, team fit, cheap hosting | 2026-05-14 |
| TD-002 | Rules-based matcher v1 (no ML) | Need explainable results for accountants; no training data yet | 2026-05-14 |
| TD-003 | NGN-only MVP | Removes FX, currency detection, settings UI from critical path | 2026-05-14 |
| TD-004 | CSV upload only | PDF parsing is a multi-sprint distraction | 2026-05-14 |
| TD-005 | Single-tenant per deploy for first 2 pilots | Faster, safer; row-level tenancy after 3 customers | 2026-05-14 |
| TD-006 | Recommend flat tiered pricing (pending CEO/Finance) | Aligns incentives; easier to forecast | 2026-05-14 |
