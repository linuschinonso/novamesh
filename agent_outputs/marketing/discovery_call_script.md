# Discovery call script — Pilot recruitment

**Audience:** Finance lead, accountant, or owner-operator at a Nigerian SME (10–200 employees) who responded to outbound and booked a 20-minute call.
**Format:** Founder-led video call, 20 minutes hard stop, one founder + one prospect.
**Cycle:** 2026-05-14 → 2026-06-04. Target: 10 calls booked by 2026-06-04, ≥2 anonymised datasets delivered to Dev by 2026-06-07.
**Goal — in priority order:**
1. Confirm or break our audience hypotheses (see `marketing_memory.md` working hypotheses).
2. Collect willingness-to-pay anchors so Finance can move tier prices off placeholders by 2026-06-04.
3. Get permission to receive one month of anonymised invoices + bank statements (resolves Dev B2).
4. Decide — on the call — whether this prospect is a pilot cohort 1 (2 slots) or cohort 2 waitlist (8 slots).

We do not pitch on this call. We listen, take notes, and ask for data. If we end the call with the prospect feeling heard but not sold to, we ran it correctly.

---

## Pre-call checklist (5 min before, founder)

- [ ] Prospect's LinkedIn open in a tab. Confirm role, tenure, team size.
- [ ] Company website open. Confirm headcount band, sector, locations.
- [ ] Note their bank(s) if visible anywhere (footer, invoices, press). If not, ask in Q2.
- [ ] Recording consent line ready (see below). Do not record without explicit verbal yes.
- [ ] Notes doc open with the question structure below pre-populated.

---

## Opening (2 min)

> "Thanks for making time, [First name]. Quick framing before we start — this is a 20-minute call, you're not on a sales pitch, I'm not going to demo anything. I'm trying to understand how your team reconciles invoices today so we build the right thing. Is it okay if I record this for my own notes? I won't share the recording externally."

If they say no to recording, proceed without. Take written notes.

> "I've got maybe six questions. If at any point you want to flip it and ask me something, just jump in."

---

## Core questions (12 min)

Ask in order. Do not skip Q1 — every other answer is anchored to the volume number.

**Q1. Volume & cadence.** "Roughly how many customer invoices does [Company] send out in a month? And how many incoming payments hit your bank/MoMo accounts against those?"
- Listen for: total invoice count, number of distinct customers, ratio of repeat to one-off customers, whether MoMo is a meaningful channel for them.
- Disqualifier check: if <50 invoices/month, they're below ICP — politely complete the call, do not push them into pilot.

**Q2. Bank stack.** "Which banks and mobile-money platforms do payments come into? GTBank, Access, Zenith, UBA, Wema, MoMo, OPay, PalmPay — which ones?"
- Listen for: count of distinct sources (matters for Dev parser priority — `dev_backlog.md` task 0.3), whether MoMo is in the mix, whether they have USD accounts (out of ICP if yes-and-material).

**Q3. The current reconciliation flow — without leading them.** "Walk me through what your team actually does at month-end to figure out which invoices got paid. Just talk me through it step by step."
- Listen for, do not prompt: who does it (junior accountant vs. finance lead vs. owner), what tool (Excel, Google Sheets, paper, QuickBooks), how long it takes, what part of it they hate.
- Silence is fine. Let them keep talking.

**Q4. The cost — in their words.** "Roughly how many hours per week does [name of person from Q3] spend on this?" Then: "And what does that role earn, roughly — just a band is fine?"
- Listen for: hours × hourly cost. This is the wedge number. If they say "oh it's nothing, an hour or two," they're below ICP — complete politely, do not push pilot.

**Q5. The break.** "What's the worst thing that's happened because of a reconciliation error? Have you ever chased a customer who already paid, or missed that a customer hadn't?"
- Listen for: emotional moment, named incident, specific ₦ amount. This is the story we will quote (anonymised) in cycle 2 content.
- If they pause and say "oh yes, there was this one time…" — let them tell the whole story. This is the highest-signal moment of the call.

**Q6. Existing solutions tried.** "Have you tried any software for this? QuickBooks, Xero, Zoho, anything else?"
- Listen for: specific tool names, why they bounced, what they wished it did, whether they're currently paying for something that isn't working.
- Hypothesis validation: marketing memory says they're NOT comparison-shopping. Test that. If they say "yeah we've been evaluating Xero," update memory.

---

## Pricing anchor questions (3 min)

These exist to give Finance willingness-to-pay data. Ask both. Do not present our prices.

**P1.** "If a tool reliably saved [hours from Q4] per week of [role from Q3]'s time, what would you expect to pay for it monthly? No wrong answer — I'm trying to calibrate."
- If they go silent: "ballpark, ₦20k? ₦100k? ₦500k? — just an order of magnitude."

**P2.** "Would you prefer to pay a flat monthly fee, or a small percentage of invoices processed?"
- Listen for: preference and reasoning. Memory says SMEs prefer predictable flat fees, but we have not confirmed. This question confirms or breaks that.

Capture both answers verbatim in the notes doc. These are the inputs that move tier prices off placeholder by 2026-06-04 (`company_state.md` open decision).

---

## The pilot ask (2 min)

Only if Q1 + Q4 cleared the ICP bar.

> "Two things to wrap up. First — we're putting together a pilot cohort of 10 Nigerian SMEs. The deal: you share one month of anonymised invoices and bank statements with us, we run them through our matcher, and we walk you through the results together. If it works for you, six months free + grandfathered pricing after that. If it doesn't, you've spent maybe an hour total and we've learned where it breaks.
>
> "Before any data moves, we send a one-page NDA — your data stays yours, we use it only to test the matcher. Is this something you'd be open to?"

If yes:
> "Great. I'll send the NDA and a short data-prep guide today. Are you the right person to receive it, or should I copy your [accountant / finance lead / IT]?"

If hesitant:
> "Totally fair — what's the concern? Data sensitivity, time, something else?"
> Capture the objection verbatim. This goes into the objection-handling playbook.

If they're enthusiastic and the call cleared ICP but they're not Lagos/Abuja/PH:
> "Honestly, we're staying Nigeria-focused for the first cohort because we can be on-site if something breaks. Can I add you to cohort 2? We'll be back in touch within 60 days."

---

## Close (1 min)

> "Last thing — is there anyone else in Lagos / Abuja / PH I should be talking to? I'm trying to reach 10 finance leads at SMEs like yours over the next month."

Capture every name they give. These become next week's outbound list.

> "Thanks for the time. I'll have the NDA + data guide in your inbox within 24 hours."

---

## Post-call protocol (within 30 min of hang-up, founder)

- [ ] Write a 5-line summary into `agent_outputs/marketing/call_notes/[YYYY-MM-DD]_[company].md`. Format:
  - Volume / banks / hours-per-week / current tool
  - Quote of the day (their exact words for the wedge moment from Q5)
  - Pricing anchor: P1 answer + P2 answer
  - Pilot decision: cohort 1 / cohort 2 waitlist / disqualified
  - Referrals captured
- [ ] If pilot-yes: send NDA + data-prep guide same day. Block calendar slot for follow-up in 7 days.
- [ ] If new referral names: add to outreach tracker, tag source = `[Company] referral`.
- [ ] Every 5 calls: re-read all notes together and update `marketing_memory.md` working hypotheses. Kill hypotheses that don't hold across ≥3 of 5.

---

## Hard rules for the founder on these calls

- **Do not demo.** We have nothing polished to show, and demoing on a discovery call collapses the conversation into a pitch. The product question is "is the pain real" — not "do you like our UI."
- **Do not commit pricing.** All copy says "six months free + grandfathered pricing." Stick to that line until Finance lands on tier prices (`company_state.md` open decision, target 2026-06-04).
- **Do not promise features.** If they ask "does it do X?" the answer is either "yes, here's what it does" or "not yet — would that block you from piloting?" Never "we can build that for you."
- **Do not skip the NDA line.** Marketing cannot send the NDA until Legal signs off on the data clause (current blocker — see `legal_risk.md`). On the call, the founder must say "before any data moves, we send a one-page NDA." If the prospect tries to send data before the NDA lands, say "let me get our NDA over first — I'll have it to you in 48 hours" and do not accept the data.
- **20 minutes is a hard stop.** If they want to keep talking, schedule a second call. Going long signals we have too much time and undervalues the prospect's calendar.
