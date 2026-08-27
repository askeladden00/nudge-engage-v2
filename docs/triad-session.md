# Triad Working Session — Weekly Summary Prototype

## Session Agenda (30 min)

**Attendees:** Raj (Eng), Lena (Design), Me (PM)

**Objective:** Walk Raj and Lena through what four rounds of prototype testing surfaced, align on the updated hypothesis, and leave with a sized next step — not just a status update.

**Pre-read (send before the session, not during):**
- [Four Rounds](https://claude.ai/code/artifact/d35aa31e-030c-499f-985c-20e2f54ada62) — the full feedback loop in slide form
- [docs/hypothesis.md](hypothesis.md) — the updated, confidence-scored hypothesis

### Time-boxed Flow

**0–5 min — Recap**
Quick reminder of the problem (30-day retention 44%→37%) and why this prototype exists: an exploratory pressure-test of Lena's weekly-summary concept, run ahead of full problem-alignment, not a committed build.

**5–15 min — Walk the loop**
Click through the live [prototype](https://claude.ai/code/artifact/d22034e8-634f-4012-a375-4270786bd1e2) (or the deck if time is tight), then the headline result: the hypothesis changed. It's not just "not personal enough" — three of four rounds independently converged on a **trust/verifiability** gap, and one round surfaced a nudge that was actively wrong, not just generic.

**15–25 min — Discussion**

Questions for Raj:
- How big is a transaction-level drill-down behind the top insight (H1 — the highest-confidence, lowest-cost item)? Spike-sized or bigger?
- Rough order-of-magnitude on priority-aware nudge logic (H2 — debt vs. goal awareness), even though it's lower-confidence — so we know the cost if we ever want to test it.
- Does either change the "new ranking logic" estimate flagged as an open item in `docs/decision-brief.md`?

Questions for Lena:
- What would "show your work" (a transaction breakdown) look like — modal, expandable card, separate screen?
- Does the debt-vs-goal finding (H2) touch any other nudge designs beyond this one?
- Does the verifiability finding (H1) suggest other places in the app need the same treatment?

**25–30 min — Decisions to walk out with**
1. Do we agree H1 (verifiability) is the right thing to test first, given it's both highest-confidence and cheapest?
2. A rough sizing from Raj for that specific scope — even directional, to unblock the resourcing-ask open item.
3. Do H2/H3 need dedicated validation, or do they stay in the backlog for now?
4. Who owns the next concrete step, and by when?

---

## Post-Session Alignment Doc (template)

Fill in immediately after the session, while it's fresh — this becomes the record of what the triad actually decided.

```markdown
# Triad Alignment — Weekly Summary Prototype

**Date:** [ ]
**Attendees:** [ ]

## Decisions Made
- [ ]

## Sizing / Estimates
- Transaction-level drill-down (H1): [ ]
- Priority-aware nudge logic (H2): [ ]

## Hypothesis Status
- H1 (Verifiability): [ pursue / hold / needs more validation ]
- H2 (Priority-Aware Nudging): [ pursue / hold / needs more validation ]
- H3 (Notification Delivery Reach): [ pursue / hold / needs more validation ]

## Open Questions Remaining
- [ ]

## Next Step
- Owner: [ ]
- By when: [ ]
- What "done" looks like: [ ]
```
