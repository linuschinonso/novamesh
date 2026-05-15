# Architecture v1 — Day 1 (2026-05-13)

## Agent Topology
Dev ──────────────────┐
Marketing ───────────► CEO → ceo_weekly_report.md
Finance  ────────────►
Legal ───────────────►
All agents read memory/company_state.md

## Role / Skill / Memory per agent

| Agent     | Role                        | Memory file              |
|-----------|----------------------------|--------------------------|
| CEO       | Synthesize all outputs      | memory/ceo_memory.md     |
| Dev       | Product backlog & specs     | memory/dev_memory.md     |
| Marketing | Content & GTM strategy      | memory/marketing_memory.md|
| Finance   | P&L & cash flow             | memory/finance_memory.md |
| Legal     | Risk & compliance           | memory/legal_memory.md   |

## Inter-agent Communication
File-based handoffs only. No direct agent-to-agent calls.
Each agent writes its output file. CEO reads all output files last.

## Memory Design
- Shared: memory/company_state.md (all agents read this)
- Private: each agent has its own memory file
- Outputs: agent_outputs/ folder

## Closed-loop Description
1. Dev runs → writes dev_backlog.md → updates dev_memory.md
2. Marketing runs → writes marketing/ → updates marketing_memory.md
3. Finance runs → writes finance_pnl.md → updates finance_memory.md
4. Legal runs → writes legal_risk.md → updates legal_memory.md
5. CEO runs last → reads all outputs → writes ceo_weekly_report.md