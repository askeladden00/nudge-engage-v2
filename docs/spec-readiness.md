# Spec Readiness — Weekly Summary (H1)

Produced from a simulated spec-review negotiation: Claude played Raj (using `stakeholders/raj.md`), and a separate agent played the PM, both grounded in the actual workspace docs. Not a real conversation with Raj — a rehearsal for one.

## 1. Spec Readiness Summary

**Solid going in — no pushback needed:**
- The core hypothesis (H1, verifiability) and why it's the right first bet to test — well-evidenced across `docs/hypothesis.md`.
- Technical feasibility — reuses existing goal-progress data, no new data model required.

**Needed work — identified and resolved during this negotiation:**

| Gap | Resolution reached |
|---|---|
| Three different, unreconciled definitions of "smallest slice" across `docs/decision-brief.md`, `docs/hypothesis.md`, and `docs/triad-session.md` | Locked: H1 — transaction-level drill-down, in-app only, no push infrastructure, no new Goal model |
| No success metric (`project.md` still says "not yet defined") | Proposed: % of users taking an action within 24hrs of a nudge, vs. a control group — **pending Marcus's sign-off, not yet locked** |
| No defined behavior for a zero-transaction week | New decision: send a distinct low-key "quiet week" variant — not silence, not the normal spike template with empty data |
| Risk of H2 (debt-vs-goal priority nudging) scope-creeping into this ticket mid-sprint | Explicitly fenced out of scope in writing, citing its 25% confidence score in `docs/hypothesis.md` |

**What's left before this is truly kickoff-ready:** two sign-offs, not engineering blockers — Marcus on the proposed success metric, Lena on the locked scope. Raj considered these "get it in writing" problems, not reasons to hold the ticket.

## 2. Rewritten Sections

**Scope** (replaces the three conflicting framings in decision-brief.md / hypothesis.md / triad-session.md):
> **v1 scope:** Transaction-level drill-down behind the top weekly insight, surfaced in-app only. No push notification infrastructure, no new Goal model — reads from existing goal-progress data. H2 (priority-aware nudging) is explicitly out of scope for this ticket.

**Success Metric** (replaces "not yet defined" in project.md):
> **Proposed, pending Marcus's sign-off:** % of users who take an action (open a category, adjust a budget, dismiss with feedback) within 24 hours of receiving a nudge, measured against a control group that doesn't receive it. Not yet a locked decision.

**Empty State** (new section — didn't exist anywhere before this exercise):
> **Zero-transaction weeks:** The notification still fires, using a distinct low-key variant — no spending highlight, a "quiet week" message plus a passive prompt (check a goal, review a budget). It does not go silent, and does not reuse the normal spike template with empty data.

## 3. Async Slack Message (send to Raj before sprint kickoff)

> Hey Raj — recap from our spec pass, want your explicit thumbs-up before I bring this to kickoff:
> - **Scope:** H1 only (transaction drill-down, in-app), no push infra, no new Goal model. H2 explicitly out of scope.
> - **Success metric:** proposing 24hr post-nudge action rate vs. control — taking it to Marcus this week for sign-off, will confirm once locked.
> - **Zero-transaction weeks:** sends a distinct "quiet week" variant instead of going silent or reusing the spike template.
>
> If that all still matches what we landed on, I'll get the ticket written up. Flag anything that's drifted.
