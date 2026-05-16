# Dev Memory

## 2026-05-16 — Sprint 0 mid-flight, Sprint 1 plan firmed up

**What changed this cycle:**
- CEO signed off MVP scope (Sprint 0 tasks 0.1–0.9). B1 closed.
- CEO + Finance accepted Dev's pricing recommendation (TD-006: flat tiered). B3 closed. Tier amounts (NGN 25k / 75k / 250k) are placeholders pending Marketing discovery-call data by 2026-06-04.
- Multi-tenancy posture confirmed: single-tenant per deploy for first 2 pilots, then row-level (provisional Sprint 5).
- Nigeria-first locked through Sprint 4 / first 3 paying customers — TD-003 (NGN-only) now load-bearing rather than provisional.

**New technical decisions this cycle:**
- **TD-007 — `StatementParser` protocol.** Every bank/MoMo parser implements the same `detect`/`parse` interface; ingestion dispatches by header match. Keeps Sprint 1 to one parser (GTBank) without locking out Access/Zenith/MoMo later.
- **TD-008 — `audit_events` table.** Append-only, written from every state transition on invoices/statement_lines/matches. Cheaper to build now than retrofit; NDPR + accountant trust both need it.
- **TD-009 — Neon Postgres** picked for first pilot deploys (free tier covers two single-tenant DBs + staging branches).

**Sprint 0 status (day 3 of 15):**
- done: 0.1, 0.2, 0.4, 0.5, 0.7
- in progress: 0.3 (Access/Zenith/MoMo/OPay column maps due 2026-05-26), 0.6 (scaffold = S1.1), 0.8 (v2 integrations write-up due 2026-05-26)
- blocked: 0.9 (security baseline — blocked on Legal pack landing, B4)

**Sprint 1 (2026-05-29 → 2026-06-12) now broken into S1.1–S1.10 with day estimates.** Total ~8.5d in a 10-day sprint to absorb B2/B4 slippage. If both slip past 2026-06-05, drop S1.10 (staging deploy) first.

**Blockers carried forward:**
- B2 — pilot data from Marketing (≥2 anonymised datasets by 2026-06-07). Mitigation: S1.5 has a synthetic 50-invoice / 80-line fallback fixture so the sprint doesn't stall. Escalate to CEO weekly report if still open by 2026-06-03.
- B4 — Legal pack. Legal must instruct counsel by 2026-05-21. If still open by 2026-05-28, Sprint 1 runs against synthetic data only; no pilot data lands until 0.9 closes.

**Things to remember next cycle:**
- The GTBank parser column map (in dev_backlog.md spec section) was verified against three sample exports; if a customer comes in with a different export format, that's a parser variant, not a bug in the spec.
- Precision/recall metric on TD-002 still gates the ML question. Cannot measure it until pilot data lands (B2).
- Tier price points are still placeholders; do not wire billing until Marketing's 2026-06-04 discovery data lands.
- TD-008 audit writes are non-negotiable from S1.6 onward — every transition writes a row. If a future cycle proposes skipping audit for speed, push back: NDPR posture depends on it.

**Next-cycle entry point:**
1. Re-read company_state.md for Legal pack status (B4) — if instructed by counsel, unblock 0.9.
2. Check Marketing's progress on B2 (≥2 datasets by 2026-06-07).
3. If 2026-05-28 has passed: close Sprint 0 (mark remaining tasks done or carry blocked items forward), open Sprint 1, promote S1.1 to in-progress.
4. If Marketing slips B2 past 2026-06-03, escalate via CEO weekly report.
