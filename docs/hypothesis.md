# Learning Synthesis — Engage v2 Hypothesis Update

Sources reviewed: `change_log.md`, `docs/decision-brief.md`, `strategy.md`, `project.md`, `CLAUDE.md`, `research/interview-synthesis.md`, `research/nps-analysis.md`, `research/competitive-matrix.md`, `research/agentic-playtest.md` (simulated), `research/prototype-feedback.md` (real).

## What We Know

High confidence — each point below is confirmed by more than one independent source, and at least one is real (not simulated) evidence.

- **30-day retention dropped from 44% to 37%** over two quarters (product data).
- **The app goes static immediately after setup.** Confirmed by Tom R. and Amara L. (real interviews) and three separate NPS respondents (#2, #7, #8).
- **Users want to be told what to do next, not just shown data.** Confirmed by Tom and Amara (interviews) and NPS #3/#6.
- **Goal-setting isn't being reinforced after onboarding.** Three independent signals: Tom R. did the "right" week-1 actions and still churned; an NPS respondent said their goal was "never once mentioned again"; simulated-Priya's playtest reaction to a mismatched goal name.
- **Generic or unverified content erodes trust and drives disengagement.** NPS #4 (a random nudge led a real respondent to disable notifications entirely), NPS #9 (generic tips), simulated-Tom's reaction to deficit-first tone.
- **Users want to verify the number behind an insight, not just trust it.** This is the single most-repeated finding across the whole loop: simulated-Priya ("I'd double check my accounts anyway"), simulated-Amara ("show your work — let me see the actual charges"), and the **real** prototype reviewer (asked for a Dining & Delivery breakdown and where the $25 came from) all converged on the same specific gap, independently.
- **No competitor owns a low-effort, goal-linked, directive weekly touchpoint.** Confirmed across 4 real category peers (YNAB, Monarch Money, Rocket Money, Copilot Money).
- **Time-to-value is slow relative to patience.** Priya's real payoff took ~3 months by her own account; Tom churned at 5 weeks; Amara stalled at 10 days.
- **A "personalized" nudge can be actively wrong, not just generic.** Simulated-Amara's finding: recommending a goal-transfer without knowing the user is carrying debt isn't a missing nice-to-have, it's incorrect advice — a sharper failure mode than "not personal enough."

## What We Assume

Embedded in the current design direction, but not directly tested by anything in this loop.

- That a **weekly** cadence (not daily, not real-time) is the right frequency for re-engagement.
- That surfacing **one** insight and **one** nudge is the right scope, versus a richer feed or multiple options.
- That **personalization itself drives retention** — directionally supported (see above) but never isolated or measured against a control.
- That the fixes made this loop (accurate goal name, softer tone, fund-source clarity) will actually change real behavior, not just read better in a mockup.

## What We Don't Know

Explicit gaps — nothing in this loop resolved these.

- **Causal vs. correlational:** does goal-setting reduce churn, or is it a proxy for an already more-engaged segment? Still open in `CLAUDE.md` — this loop added supporting anecdotes but no causal test.
- **No success metric is defined.** `project.md` still lists this as TBD; we don't yet know what number would tell us this worked.
- **No resourcing or timeline estimate** for the nudge-ranking-logic work `docs/decision-brief.md` flags as required.
- **Whether push notifications reach the target segment at all.** Simulated-Tom raised this directly ("I probably wouldn't have arrived here... I don't act on notifications from apps I've checked out of") — this challenges the delivery mechanism itself, independent of content quality, and was never resolved.
- **Whether the small-N qualitative sample generalizes.** `docs/decision-brief.md`'s own caveat: 3 interviews and 10 NPS responses, directionally consistent but not validated against usage data at scale.
- **Whether the debt-vs-goal nudge failure is common** among Nudge's real user base, or an edge case surfaced by one simulated persona.

## How the Hypothesis Changes

The original hypothesis (`strategy.md`) was that users go passive because the app **isn't personal, timely, or actionable enough** after the first week. Four rounds of testing a design built specifically to fix that (a personalized weekly insight, nudge, and goal progress) did not falsify this — but it surfaced a sharper problem underneath it. Personalization alone isn't the fix, for two reasons that showed up repeatedly and independently:

1. **Trust, not just relevance, is the binding constraint.** Users don't just want content that's about them — they want to be able to verify it. A personalized insight that can't be checked against real transactions gets the same "I'll just check my own accounts" response as no insight at all (Priya, Amara, and the real reviewer all said versions of this).
2. **A personalized nudge can be wrong, which is worse than generic.** Recommending the wrong action — moving money to a goal when the user is carrying debt — doesn't just fail to help, it teaches the user the product doesn't understand their situation (Amara's finding).

A third finding sits outside the content question entirely: the **delivery mechanism itself may be unproven** for the exact segment this is meant to win back (Tom's challenge to push notifications).

## New Hypothesis Statement

The four rounds surfaced three distinct, testable claims — not equally supported. Each is written below as hypothesis / prediction / null hypothesis, so it can actually be run as an experiment rather than treated as already-confirmed.

**Confidence scoring method:** each score reflects (1) number of independent corroborating sources, (2) whether those sources are real vs. simulated, and (3) how directly the evidence maps to the claim (a direct quote vs. an inference). None are scored above 80% — all evidence so far is qualitative reaction to a static mockup, not usage data or an A/B test.

| Hypothesis | Confidence | Cost to Validate |
|---|---|---|
| H1 — Verifiability | **70%** | Low — a UI drill-down, no new logic |
| H3 — Notification Delivery Reach | **30%** | High — needs real notification open-rate data segmented by activity status |
| H2 — Priority-Aware Nudging | **25%** | Low — a small qualitative check with debt-carrying users |

**For prioritization:** H1 is the clear first candidate on both dimensions — highest confidence and cheapest to test. H2 and H3 sit at similar confidence but aren't equally cheap to de-risk: H2 can be checked quickly and informally, while H3 needs real behavioral data before it says anything conclusive.

### Primary Hypothesis (H1 — Verifiability)
*Support: strong (70%) — corroborated by 3 independent sources (2 simulated, 1 real), all converging on the same specific ask.*

- **Hypothesis:** If users can verify a personalized insight or nudge against their own underlying transactions, then they will trust and act on it more than an equivalent insight they cannot verify — because the current drop-off is driven by distrust of unverifiable claims, not by a lack of personalization itself.
- **Prediction:** Adding a transaction-level drill-down behind the top insight increases nudge completion rate (or reduces self-reported "I'll just check my own account instead" behavior) versus the current non-verifiable version.
- **Null hypothesis:** Adding verifiability produces no measurable change in trust or action rate — the drop-off is driven by something else.

### Secondary Hypothesis (H2 — Priority-Aware Nudging)
*Support: weak (25%) — single simulated persona (Amara), not yet corroborated.*

- **Hypothesis:** If a nudge accounts for a user's competing financial priorities (e.g., debt vs. a savings goal) before recommending an action, then users will rate it as more trustworthy than a priority-blind nudge — because a priority-blind nudge is perceived as actively wrong, not merely generic.
- **Prediction:** Users carrying debt who are shown a debt-aware nudge report higher trust/satisfaction than those shown the current priority-blind, goal-transfer nudge.
- **Null hypothesis:** Priority-awareness produces no measurable difference — users don't distinguish between priority-aware and priority-blind nudges in practice.

### Secondary Hypothesis (H3 — Notification Delivery Reach)
*Support: weak (30%) — single simulated persona (Tom), with a weak, indirect echo in NPS #5 ("I just forget it exists") that speaks to low salience but isn't a direct match to the delivery-reach claim.*

- **Hypothesis:** If the weekly summary is delivered via push notification, then users who have already gone passive will not reliably open it, because they've mentally disengaged from the app and don't act on its notifications — meaning content quality alone cannot fix re-engagement.
- **Prediction:** Push notification open rates among already-passive users (e.g., 7+ days inactive) are significantly lower than among currently-active users, even when the underlying content tests well.
- **Null hypothesis:** Passive users open push notifications at a similar rate to active users — delivery channel is not the bottleneck.
