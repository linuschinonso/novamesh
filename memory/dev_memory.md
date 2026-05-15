# Dev Memory

## 2026-05-14 — Sprint 0 kickoff

**What was decided this cycle:**
- MVP product framing: invoice + bank/mobile-money statement reconciliation for African SMEs, single-tenant, NGN-only, CSV upload only.
- Stack (TD-001): Python 3.12 + FastAPI, Postgres (managed), Next.js + TS + Tailwind. No job queue yet.
- Matching algorithm v1 (TD-002): rules-based — exact amount + date window (issue_date → due_date+14d) + narration token/invoice-number match. No ML in MVP.
- Tenancy (TD-005): per-deploy single-tenant Postgres schemas for first 2 pilots, then move to row-level `tenant_id` after pilot #3.
- Ingestion (TD-004): CSV only. Templates we will provide: invoices, GTBank/Access/Zenith statements, MTN MoMo/OPay statements (statement formats specced in sprint 0, only GTBank parser built in sprint 1).
- Pricing recommendation to CEO/Finance (TD-006): flat monthly fee tiered by invoice volume. Final call not ours.

**Data model committed to:** `invoices`, `statement_lines`, `matches` tables — schemas in agent_outputs/dev_backlog.md.

**Blockers carried forward:**
- B1: CEO sign-off on MVP scope before Sprint 1 starts (2026-05-29).
- B2: No pilot customer data yet — need ≥1 anonymized invoice+statement pair from Marketing.
- B3: Pricing decision pending Finance + CEO.
- B4: NDPR data-handling baseline pending Legal.

**Things to remember next cycle:**
- Track precision/recall on the rules-based matcher against real pilot data; that metric gates the ML question.
- Open company decision "Nigeria first vs. pan-Africa" — Dev's bet is Nigeria-first; TD-003 (NGN-only) already assumes this.
- Don't let Sprint 1 start until 0.1 (scope sign-off) and at least a partial answer to B2 land — otherwise we'll build parsers against assumed schemas.

**Next-cycle entry point:**
1. Re-read company_state.md for any decisions resolved by CEO/Finance/Legal.
2. Promote completed Sprint 0 tasks to "done" and update Sprint 1 task list with concrete sub-tasks.
3. If B2 still open, escalate to CEO weekly report.
