# Dev Backlog — NovaMesh

Cycle date: 2026-05-16
Owner: Dev agent
Stage: Pre-revenue MVP build — Sprint 0 day 3 of 15

---

## Product framing (working definition)

NovaMesh is a B2B SaaS tool that ingests an SME's invoices and bank/mobile-money statements, matches them automatically, and flags exceptions for human review. Target user: an accountant or finance lead at an African SME (10–200 employees) currently doing reconciliation manually in Excel.

The MVP must answer one question end-to-end: **"Given this batch of invoices and this bank statement, which invoices are paid, which are unpaid, and which payments are unattributed?"**

---

## Current sprint (Sprint 0 — Foundations, 2026-05-14 → 2026-05-28)

| #   | Task                                                                          | Status      | Notes                                                                                  |
|-----|-------------------------------------------------------------------------------|-------------|----------------------------------------------------------------------------------------|
| 0.1 | Lock MVP scope to single-tenant, single-currency (NGN) reconciliation         | done        | CEO signed off this cycle. Unblocks Sprint 1 kick-off on 2026-05-29.                   |
| 0.2 | Spec the invoice data model                                                   | done        | Schema below; `invoices` table committed.                                              |
| 0.3 | Spec the statement data model (bank CSV + mobile money formats)               | in progress | Generic `statement_lines` schema done. Per-bank column maps: GTBank done; Access, Zenith, MTN MoMo, OPay due by 2026-05-26. |
| 0.4 | Decide ingestion path for MVP: CSV upload vs. email forward vs. API           | done        | TD-004: CSV only for MVP.                                                              |
| 0.5 | Pick reconciliation matching algorithm v1                                     | done        | TD-002: rules-based hard/soft match.                                                   |
| 0.6 | Choose stack and scaffold repo                                                | in progress | Stack chosen (TD-001). Repo scaffold = Sprint 1 task S1.1.                             |
| 0.7 | Define exception-handling UX (reviewer queue)                                 | done        | Pseudocode below.                                                                      |
| 0.8 | Research v2 integrations (Paystack, Flutterwave, Quickbooks Africa)           | in progress | API docs surveyed; write-up due 2026-05-26.                                            |
| 0.9 | Draft a security/data-handling baseline (encryption at rest, PII, audit log)  | blocked     | Blocked on B4 (Legal pack). Cannot finalise PII boundary until NDPR posture lands.     |

**Sprint 0 exit criteria (must hold by 2026-05-28):** every row above is `done`, except 0.9 which may remain `blocked` only if Legal slips its 2026-05-21 deadline — in which case Sprint 1 work proceeds but no pilot data is permitted to land.

---

## Technical decisions made this cycle

### TD-007 — Statement parser interface (new this cycle)
All bank/mobile-money parsers implement a single Python protocol so Sprint 1 only needs one matching engine:

```
class StatementParser(Protocol):
    source_name: str                # e.g. "gtbank", "mtn_momo"
    def detect(self, header_row: list[str]) -> bool: ...
    def parse(self, file: IO[bytes], account_label: str) -> Iterator[StatementLine]: ...
```

`StatementLine` is a dataclass mirroring the `statement_lines` columns. The ingestion endpoint runs `detect` across registered parsers and dispatches to the first match; unknown formats return a 422 with the offending header.

Reason: keeps Sprint 1 scope to one parser (GTBank) without painting us into a corner when Access/Zenith land in Sprint 3.

### TD-008 — Audit logging shape (new this cycle)
One append-only `audit_events` table, written from every state transition on `invoices`, `statement_lines`, and `matches`:

```
audit_events(
  id           uuid pk,
  tenant_id    uuid,
  actor_id     uuid null,       -- null = system/automated
  entity_type  text not null,   -- invoice|statement_line|match
  entity_id    uuid not null,
  action       text not null,   -- created|updated|matched|review_accepted|review_rejected|split
  before       jsonb,
  after        jsonb,
  occurred_at  timestamptz default now()
)
```

Reason: NDPR + accountant trust both demand "who changed what when". One table is cheap; bolting it on later is not.

### TD-001 — Stack (carried)
- Backend: Python 3.12 + FastAPI.
- DB: PostgreSQL (managed; Neon picked as default for Sprint 1 — free tier covers two pilot deploys).
- Frontend: Next.js + TypeScript + Tailwind.
- Queue/jobs: none in MVP.

### TD-002 — Reconciliation algorithm v1 (carried)
Rules-based hard/soft match. See pseudocode below.

### TD-003 — Single-currency MVP (carried)
NGN only. Reaffirmed: CEO confirmed Nigeria-first through Sprint 4 / first 3 paying customers.

### TD-004 — File ingestion (carried)
CSV upload only.

### TD-005 — Multi-tenancy posture (carried)
Single-tenant per deploy for first 2 pilots. Row-level `tenant_id` migration scheduled for after pilot #3 (provisional Sprint 5).

### TD-006 — Pricing model (resolved)
CEO/Finance accepted Dev's recommendation: flat monthly fee tiered by invoice volume (NGN 25k / 75k / 250k placeholders). Final tier amounts depend on Marketing's discovery-call data by 2026-06-04. Billing wiring stays out of MVP scope until tier amounts firm up.

---

## Specs (pseudocode)

### Invoice schema (Postgres) — unchanged
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

### Statement line schema — unchanged
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

### Match record — unchanged
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

### Reconciliation pass (pseudocode) — unchanged
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

### GTBank parser column map (new this cycle, for S1.2)
GTBank CSV export header (verified against three sample exports collected in research):
```
Trans. Date | Value Date | Reference | Narration | Debits | Credits | Balance
```
Mapping into `StatementLine`:
- `posted_at`   ← `Value Date` (DD/MM/YYYY; fall back to `Trans. Date` if blank).
- `amount`      ← `Credits` as positive; if blank, `Debits` as negative.
- `narration`   ← `Narration`.
- `reference`   ← `Reference`.
- `raw_row`     ← the full row as a JSON object.

Skip rows where both `Debits` and `Credits` are blank (carry-forward balance rows).

### Exception queue UX — unchanged
- Reviewer sees a table: Invoice | Candidate statement line(s) | Confidence | Accept / Reject / Split.
- "Split" supports one invoice paid by multiple lines (deposits, partial payments).
- Every accept/reject writes a row into `audit_events` (TD-008).

---

## Blockers

- **B1** — ~~CEO sign-off on MVP scope~~ **resolved 2026-05-15** (per company_state.md).
- **B2** — No pilot customer data. Marketing committed to ≥2 anonymised datasets by 2026-06-07. Sprint 1 task S1.5 hard-depends on this. If still open by 2026-06-03, escalate to CEO weekly report and ship S1.5 against a synthetic fixture instead.
- **B3** — ~~Pricing decision~~ **resolved 2026-05-15** (flat tiered accepted; tier amounts pending Marketing discovery by 2026-06-04, but that does not block MVP build).
- **B4** — Data-handling baseline (task 0.9). Blocked on Legal pack (incorporation + MSA/DPA/NDA + Privacy Notice + AUP). Legal must instruct counsel by 2026-05-21. **If B4 is still open by 2026-05-28, Sprint 1 proceeds but no pilot data may be loaded into any environment until 0.9 closes.** Synthetic data only.

---

## Next sprint (Sprint 1 — Ingestion + matching core, 2026-05-29 → 2026-06-12)

Goal: a developer-only CLI/API that ingests one invoices CSV + one GTBank statement CSV and emits a reconciliation report. No customer-facing UI.

**Definition of done for the sprint:** running `nm reconcile --invoices a.csv --statement gt.csv --tenant pilot01` returns a JSON report and a human-readable summary, with passing integration tests against at least one anonymised real-customer pair (B2) or, failing that, the synthetic fallback fixture.

| # | Task | Owner | Dep | Est |
|---|------|-------|-----|-----|
| S1.1 | Scaffold FastAPI service + Postgres (Neon) + Alembic migrations. Repo layout: `app/`, `app/ingest/`, `app/match/`, `app/api/`, `tests/`, `migrations/`. Add Ruff + Pyright + pytest in CI (GitHub Actions). | Dev | — | 1.5d |
| S1.2 | Implement invoice CSV parser against the template in spec 0.2. Reject rows missing required fields with line-numbered errors. | Dev | S1.1 | 1d |
| S1.3 | Implement GTBank statement parser per the column map above; register against the `StatementParser` protocol (TD-007). | Dev | S1.1 | 1d |
| S1.4 | Implement the reconciliation pass per TD-002. Pure-function core in `app/match/engine.py`; DB writes in `app/match/store.py`. | Dev | S1.2, S1.3 | 1.5d |
| S1.5 | Seed test fixtures: (a) anonymised pilot dataset if Marketing delivers by 2026-06-07; (b) synthetic 50-invoice / 80-line fixture as fallback so the sprint is not blocked. | Dev | B2 (soft) | 0.5d |
| S1.6 | Wire `audit_events` writes (TD-008) into every state transition. One pytest per transition type asserting the audit row exists. | Dev | S1.4 | 0.5d |
| S1.7 | Single admin auth: API-key header, one key per deploy, stored hashed in `app_admins`. No multi-tenant login UI yet. | Dev | S1.1 | 0.5d |
| S1.8 | Integration tests against real CSV files (not mocks). Coverage target: parser ≥90%, matcher ≥85%, end-to-end golden test produces the expected JSON report byte-for-byte. | Dev | S1.4, S1.5 | 1d |
| S1.9 | CLI entrypoint `nm reconcile` wrapping the API for developer/pilot operator use. | Dev | S1.4 | 0.5d |
| S1.10 | Deploy one staging environment on Fly.io with the Neon free-tier DB; smoke test ingestion against S1.5 fixture. | Dev | S1.1, S1.7 | 0.5d |

**Total estimate:** ~8.5 dev-days for a 10-working-day sprint — buffer absorbs B2/B4 slippage. If both B2 and B4 slip past sprint mid-point (2026-06-05), drop S1.10 (staging deploy) to keep matcher quality in scope.

**Out of scope for Sprint 1 (explicit):**
- Any UI. Reviewer queue UI ships in Sprint 2.
- Access/Zenith/MTN MoMo/OPay parsers. Sprint 3.
- Multi-tenant login, billing, RLS. Per TD-005.
- ML scoring. Per TD-002.

---

## Sprint 2+ preview (provisional)

- **Sprint 2 (2026-06-13 → 2026-06-26):** Next.js UI for upload, run reconciliation, reviewer queue with accept/reject/split. First end-to-end pilot run with customer #1.
- **Sprint 3 (2026-06-27 → 2026-07-10):** Second + third bank parsers (Access, Zenith); pilot #2 onboarding; precision/recall dashboard against real reconciled history.
- **Sprint 4 (2026-07-11 → 2026-07-24):** Mobile money parsers (MTN MoMo, OPay); first paying customer cutover.
- **Sprint 5 (provisional):** Row-level tenancy migration (per TD-005) once pilot #3 lands.

---

## Decision log (running)

| ID | Decision | Reason | Date |
|----|----------|--------|------|
| TD-001 | Python/FastAPI + Postgres + Next.js | Iteration speed, team fit, cheap hosting | 2026-05-14 |
| TD-002 | Rules-based matcher v1 (no ML) | Need explainable results for accountants; no training data yet | 2026-05-14 |
| TD-003 | NGN-only MVP | Removes FX, currency detection, settings UI from critical path | 2026-05-14 |
| TD-004 | CSV upload only | PDF parsing is a multi-sprint distraction | 2026-05-14 |
| TD-005 | Single-tenant per deploy for first 2 pilots | Faster, safer; row-level tenancy after 3 customers | 2026-05-14 |
| TD-006 | Flat tiered pricing accepted by CEO/Finance | Aligns incentives; easier to forecast — final tier amounts pending Marketing discovery | 2026-05-15 |
| TD-007 | `StatementParser` protocol for all bank/MoMo parsers | One matcher, many parsers; lets us add formats without touching match engine | 2026-05-16 |
| TD-008 | Single `audit_events` table for every entity transition | NDPR + accountant trust demand auditability; bolting on later is expensive | 2026-05-16 |
| TD-009 | Neon Postgres (managed) for first pilot deploys | Free tier covers two single-tenant deploys; easy branching for staging | 2026-05-16 |
