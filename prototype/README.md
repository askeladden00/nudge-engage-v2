# Nudge — Weekly Summary Prototype

An interactive prototype of the Engage v2 personalized weekly summary, demonstrating the full flow from notification to a completed action.

**Published for peer review:** [Weekly Summary Prototype](https://claude.ai/code/artifact/d22034e8-634f-4012-a375-4270786bd1e2) (private by default — share from the artifact's own menu)

## PM Brief

**User:** 28-year-old who connected their Chase account 2 weeks ago and has not opened the app since.

**Job to be done:** Understand where their money went this week and take one action.

**Feature:** Personalized weekly money summary — top spending insight, one contextual nudge, savings goal progress.

**Constraint:** Use data Nudge already has — no new integrations.

Grounded in [research/interview-synthesis.md](../research/interview-synthesis.md), [research/nps-analysis.md](../research/nps-analysis.md), [research/competitive-matrix.md](../research/competitive-matrix.md), and [docs/decision-brief.md](../docs/decision-brief.md).

## Key Decisions Made During the Interview

- **Purpose:** An interactive flow, not a static mockup — shown as a phone-frame demo from the push notification through to opening the app.
- **Flow depth:** The prototype continues past the summary screen into actually completing the nudge's action and showing a confirmation state, to demonstrate the full "take one action" job-to-be-done — not just "understand where money went."
- **Format:** Mobile phone-frame mockup only (this is a push-notification-driven flow, so a desktop/responsive frame wouldn't represent it accurately).
- **Sample data:** No real user data exists for this scenario, so a specific, illustrative transaction and goal scenario was invented rather than left generic — directly reflecting the research finding that specific insights outperform generic ones (see interview-synthesis.md, Theme 3).
- **Nudge design:** The nudge is explicitly tied to the top insight (a dining spend spike) rather than an independent/generic alert — a deliberate choice to avoid the "random nudge" complaint surfaced in NPS feedback (nps-analysis.md, #4).
- **Goal reinforcement:** The scenario assumes the user set a savings goal during onboarding that has gone unmentioned since — directly targeting the goal-neglect complaint independently raised in both the interview synthesis (Tom R.) and NPS feedback (#6).
- **Scope boundaries:** No backend, no real Plaid/Chase integration, and no other app screens (home feed, other nudge types) — this prototype covers exactly one flow: notification → weekly summary → nudge action → confirmation.

## What's in the Prototype

1. **Lock screen notification** — "Your week in review is ready," tappable to open the app.
2. **Weekly summary screen** — Top Insight (dining spend vs. week 1, shown as a simple bar comparison), Goal Progress (Europe Trip, $340 of $1,000), and a nudge card ("Move $25 to Europe Trip to offset this week's dining spike").
3. **Completed action state** — tapping the nudge shows a brief loading state, then updates the goal progress bar and amount in place, with a confirmation message.

A "Replay demo" control resets the flow — this is a prototype-only affordance, not part of the real app design.

## Running It

Open [index.html](index.html) directly in a browser. No build step or server required.

## Feedback on This Prototype

- [research/agentic-playtest.md](../research/agentic-playtest.md) — simulated persona playtest (Priya, Tom, Amara), with two implemented fixes (goal name, entry tone) and a stack-ranked backlog for what's left
- [research/prototype-feedback.md](../research/prototype-feedback.md) — real user feedback on the published version, with two more implemented fixes (Top Insight spacing, $25 fund-source clarity)
- [screenshots/](screenshots/) — full-flow screenshots across three rounds, tracking what each persona actually saw
