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

---

## Post-Session Alignment — SIMULATED OUTCOME

**This session has not actually happened.** The user asked to assume it did, so the fill-in below is a plausible, hypothetical projection — grounded in the agenda above, `docs/hypothesis.md`'s confidence scores, and the real architecture findings in `docs/codebase-summary.md` — not a real record of what Raj and Lena said. Treat it as a planning input to react to, not a decision that's actually been made. Replace this section with the real outcome once the session happens.

```markdown
# Triad Alignment — Weekly Summary Prototype

**Date:** [simulated — not a real session]
**Attendees:** Raj, Lena, Me

## Decisions Made
- Descope to an in-app-only MVP that tests H1 (verifiability) first — a transaction-level drill-down behind the top insight — rather than committing to the full notification-driven loop.
- Treat push notifications + a structured Goal model as a separate, larger initiative requiring its own scoping, not a sub-task of this feature. `docs/codebase-summary.md` confirmed neither exists in the reference codebase today.
- H2 and H3 stay in the backlog pending lighter-weight validation before any engineering commitment.

## Sizing / Estimates
- Transaction-level drill-down (H1): Small — reuses existing `IncomeStatement`/`Period` aggregation logic; mainly new UI plus a query through `Entry`/`Transaction`. Raj's rough take: sprint-sized, not a quarter-sized effort.
- Priority-aware nudge logic (H2): Not yet sized — Raj flagged it needs its own discovery (what "competing priority" data even exists per user) before it can be estimated at all.
- Full notification-driven loop (push infra + Goal model): Flagged as multi-sprint and out of scope for this round — bigger than the team had been assuming going in.

## Hypothesis Status
- H1 (Verifiability): pursue — build the in-app-only version first
- H2 (Priority-Aware Nudging): needs more validation — check with a few debt-carrying users before any build commitment
- H3 (Notification Delivery Reach): needs more validation — shouldn't assume push notifications work for this segment; worth checking open-rate data before it's load-bearing in any design

## Open Questions Remaining
- Do we invest in push notification infrastructure at all, or lean on a channel that already exists (e.g., email, in-app) while H3 stays unvalidated?
- Should "goal" become a first-class object now, or can goal progress be approximated near-term via the existing Budget/BudgetCategory model?
- Who validates H2 and H3 before engineering time is committed to either?

## Next Step
- Owner: Me (PM) to write the H1 ticket; Raj to confirm final sizing once scoped
- By when: before next sprint planning
- What "done" looks like: a scoped, estimated ticket for the in-app-only transaction drill-down, ready to bring to sprint planning
```
