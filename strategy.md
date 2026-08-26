# Strategy — Engage v2

## Hypothesis
Users go passive because the app stops feeling relevant after the first week. The initial spending breakdown is a compelling "aha moment," but after that Nudge hasn't given users a reason to come back that feels personal, timely, or actionable.

**Update:** After four rounds of prototype testing, this hypothesis has been superseded by a sharper, confidence-scored version — see [docs/hypothesis.md](docs/hypothesis.md). Summary: personalization alone wasn't sufficient; the binding constraint looks more like *trust/verifiability* (H1, 70% confidence) than relevance per se, with two lower-confidence secondary hypotheses (priority-aware nudging, notification delivery reach) also surfaced but not yet corroborated.

## Supporting Evidence
- Users who don't set a savings goal in week 1 churn at roughly 2x the rate of those who do.
- The home feed looks the same whether a user last opened the app yesterday or three weeks ago.
- The weekly summary email has a 22% open rate, but the in-app experience doesn't continue what the email started.

## Tensions / Complications
- The week-1 goal-setting correlation (users who don't set a savings goal in week 1 churn ~2x more) may not be causal. Tom R., a churned user, completed comparable week-1 onboarding actions — connected three accounts, set up a budget — and still churned at 5 weeks, because nothing followed after setup. See [research/interview-synthesis.md](research/interview-synthesis.md) for the full interview synthesis.

## Early Direction (unconfirmed)
Lena has sketched a personalized in-app weekly summary screen — surfacing a top insight for the week, one actionable nudge based on the user's own patterns, and progress toward their savings goal. Raj has confirmed this is technically feasible with existing data sources, though it would require building new ranking logic to decide which insight to surface.

This direction has not been validated against the problem yet — it's pending alignment on the problem itself at Thursday's meeting.

**Competitive validation:** [research/competitive-matrix.md](research/competitive-matrix.md) independently identifies two gaps across 5 competitors (YNAB, Monarch Money, Rocket Money, Copilot Money, Chime) that align with this direction: (1) none of them turn a stated goal into a recurring, personal touchpoint with a directive next step, and (2) none of them serve the casual, low-effort user without pushing them toward either heavy manual discipline (YNAB) or a comprehensive dashboard (Monarch, Copilot). Both gaps match what Lena's weekly-summary concept is aimed at.

A shareable visual version of the matrix is published at [The Habit Gap](https://claude.ai/code/artifact/81972a96-b878-499b-a2cb-7eb66fc2dac3) (private by default — share from the artifact's own menu).
