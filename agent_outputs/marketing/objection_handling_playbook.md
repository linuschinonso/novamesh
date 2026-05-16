# Objection handling playbook — Pilot recruitment

**Audience:** Founder running outbound + discovery calls. Internal-facing.
**Format:** Objection → recommended response → underlying reasoning (so founder can adapt, not parrot).
**Cycle:** 2026-05-14 → 2026-06-04.
**How to use:** Skim before each call. Update the **what we've learned** section after every 5 calls — these are working answers, not gospel.

---

## Hard rules (do not violate, even under pressure)

1. **Never quote tier prices.** Tier price points (NGN 25k / 75k / 250k in `company_state.md`) are placeholders. All outbound says "six months free + grandfathered pricing." Holding this line buys Finance room to decide by 2026-06-04 without us locking the company in.
2. **Never accept pilot data before the NDA lands.** Even if the prospect emails a statement at 9pm. Reply: "let me get our NDA over first — I'll have it to you within 48 hours" and delete the attachment unread. NDA is gated on Legal's NDPR sign-off (current blocker, see `legal_risk.md`).
3. **Never promise a feature on the call.** If the prospect needs something we don't have, the only allowed answers are: "yes, here's how it works today," "not yet — would that block you from piloting?," or "let me check and come back to you in writing." No "we can build that for you."
4. **Never disparage QuickBooks/Xero by name.** If asked, the answer is "they're great tools, they were just built for a different reconciliation pattern than what most Naira books look like." Punching down at incumbents reads insecure.

---

## Top 8 objections, ranked by expected frequency

### 1. "How is this different from QuickBooks / Xero / Zoho?"

**Recommended response:**
> "Honest answer — QuickBooks and Xero are general accounting platforms. They assume payments come in with clean references. The reconciliation problem we're solving is specific to Naira bank narrations and MoMo transfers, where the reference is `P2P TRF FROM 080xxxxxxxx` and there's no invoice number anywhere. We don't replace your accounting system; we sit upstream of it and tell it which invoice each payment matches to. If you're already exporting from QuickBooks to Excel to match payments manually, that's the workflow we replace."

**Why this works:** We don't position as a competitor. We position as the layer that makes their existing accounting tool finally work on Naira data. Memory says this audience has already bounced off international SaaS — they're not in comparison-shopping mode, they're in "Excel-and-suffering" mode.

---

### 2. "What does it cost?"

**Recommended response:**
> "Pilot cohort is six months free, and pilot customers get grandfathered pricing after that. We haven't finalised the tiers yet — we're using the pilot to calibrate what's fair given how much time it actually saves your team. Can I ask a related question — if a tool reliably gave [name from earlier in call] back [hours from Q4 in discovery script] per week, what would you expect to pay monthly?"

**Why this works:** Pivots a pricing pressure-question into a pricing discovery question. The answer is genuinely the input Finance needs by 2026-06-04. Do not state a tier price even if pushed twice. On third push: "honestly, I'd rather get the matcher right on your books than quote you a number I might walk back."

---

### 3. "Is our data safe? Are you NDPR-compliant?"

**Recommended response:**
> "Good question, and short answer: we're being deliberate about it. Before any data moves, we send a one-page NDA. Once the pilot starts, the agreement we use covers data processing under the NDPR — you remain the data controller, we're a processor, we don't share with third parties, and we delete the data at the end of the engagement or whenever you ask. For the pilot itself we ask for anonymised data, so customer names and account numbers can be masked before you send anything. Happy to send our data-handling note to you and your team to review before we go further."

**Why this works:** Names NDPR explicitly. Concedes the right-to-delete and the data-processor framing without overpromising. Offers to put it in writing — which the prospect will probably want to forward to their CEO/MD anyway.

**Caveat:** This is the highest-stakes objection. Do not freelance. If the prospect pushes past this script, the founder's only escalation is "let me have our legal counsel send you a one-pager — what's the best email?" Then loop Legal in same day.

---

### 4. "We already use QuickBooks / Sage / our accountant uses [system]."

**Recommended response:**
> "Great — and you'll keep using it. We're not replacing your books. We sit upstream: ingest your invoices (CSV from QuickBooks works) and your bank statements, do the matching, and hand you back a reconciled report you can post into QuickBooks in a single click. The question for the pilot isn't 'switch to us' — it's 'does the matcher actually save your team 8 hours a week.' Worth 20 minutes to find out?"

**Why this works:** Reframes from "rip and replace" (which they hear as risk) to "lightweight add-on" (which they hear as low-commitment). Names a specific integration (QuickBooks CSV export) even though direct integration is roadmap not MVP — the CSV path works today.

---

### 5. "We don't have time / we're slammed right now."

**Recommended response:**
> "Totally hear that — and I think you've just told me you're a fit, because 'we're slammed' usually means somebody on your team is spending half their week on stuff like this. Pilot ask is light: 20-min call, you send one month of anonymised invoices + statements (your accountant probably already has these in a folder), we run them and send you the result. Total of maybe two hours of your team's time over a month. If it's the wrong moment, fair — can I check back in six weeks?"

**Why this works:** Reframes the objection as confirmation of fit. Quantifies the actual ask (two hours over a month) so they're not imagining a multi-week implementation project. Offers a soft re-engage door so we keep the relationship warm.

---

### 6. "We need to ask our CEO / MD / accountant first."

**Recommended response:**
> "Of course — and that's normal. Can I send you a one-page summary you can forward? It explains the pilot deal, the data we'd need, and the NDPR side of things in plain language. If your [CEO/MD/accountant] has questions after that, I'm happy to do a 15-minute call with them directly."

**Why this works:** Two moves: (a) gives them a forwardable artifact so they're not retelling the pitch from memory, (b) volunteers a second call to the decision-maker so the prospect doesn't have to defend the pilot internally. *Action item: build this one-pager — currently a gap. Tracked in strategy memo as a next-cycle deliverable.*

---

### 7. "What if your matcher gets it wrong? What if it tells us a customer paid who didn't?"

**Recommended response:**
> "This is the right question to ask. Two answers. First, the matcher returns three lists, not one — confidently matched, ambiguous, and unattributed. Anything where the match isn't unambiguous goes into a review queue for a human to confirm. We're not asking your team to trust a black box. Second, every match shows you exactly which rules fired and on what data — there's no 'AI says so' anywhere. Your accountant can defend every reconciliation in an audit. That's a deliberate design choice; we know accountants need explainability."

**Why this works:** Validates the concern (don't minimise it). Then names two specific design choices — the review queue and the transparent rules — that address the concern. Memory says auditability is a *positive* selling point with this audience; lean into it. Never describe NovaMesh as "AI-powered."

---

### 8. "How do I know you'll still be around in 12 months?"

**Recommended response:**
> "Fair, and I won't bullshit you — we're pre-revenue, building the first version, looking for our first 10 customers. That's exactly what the pilot is. You get six months free, you keep your data, the matcher runs on CSVs you control, and there's no integration to undo if it doesn't work out. The lowest-stakes way to test it is to pilot now while it costs you nothing, and decide at month six whether to stay. If we're still building the right thing at that point, you've gotten value for free. If we're not, you walk away with no switching cost."

**Why this works:** Honest about stage (memory: practitioners-to-practitioners, honest about what we haven't built earns trust). Names the asymmetry — they have nothing locked in. Removes the existential risk of "if you go under, I'm stranded."

---

## What we've learned from calls (update this section after every 5 calls)

*Empty as of 2026-05-16. First update due after call #5 — expected week of 2026-05-25.*

Track here:
- Which objections actually came up vs. predicted.
- Any objection we didn't anticipate (these go to the top of the next update).
- Which responses landed and which felt forced.
- Quotes from prospects that we should fold into next cycle's content.

---

## When in doubt

Three escape valves the founder can always use:
1. **"That's a fair question — let me come back to you on it in writing today."** (For anything where a wrong answer is worse than a delayed answer.)
2. **"Honestly, I don't know yet — that's part of why we're piloting."** (For product questions about edge cases.)
3. **"Let me loop in our [legal counsel / accountant / Dev lead] — what's the best email to copy them on?"** (For specialist questions.)

None of these lose the deal. Pretending to know something we don't will.
