# Nudge — Engage v2

PM working repository for the Engage v2 initiative at Nudge, a consumer personal finance app. Tracks the research, strategy, decisions, and a working prototype behind an effort to recover a 30-day retention decline.

## What This Is

Nudge's 30-day retention (the share of users still active 30 days after connecting their first bank account) dropped from 44% to 37% over two quarters, concentrated in users who go passive after their first week. This repo is the working record for **Engage v2** — the squad's effort to diagnose why, and to test a candidate fix: a personalized weekly summary (top spending insight, one contextual nudge, savings goal progress).

Owned by the Engage squad: Raj (Senior Engineer), Lena (Product Designer), and me (PM) — reporting to Marcus, Head of Product.

## Current Status

**Phase: Problem-alignment.** The team is still working to agree on the root cause of the retention drop before formally committing to a solution — a working meeting is scheduled to align on the problem before designing solutions. Building and testing the prototype in this repo was an exploratory pressure-test of Lena's weekly-summary concept, run ahead of that alignment — not a committed build.

Two things remain explicitly open:
- **Success metrics are not yet defined** by the team.
- **The causal link between week-1 goal-setting and reduced churn is unconfirmed** — multiple independent data points (a churned user who did the "right" onboarding steps anyway, and an NPS respondent whose goal was never reinforced) complicate reading it as causal rather than a proxy for a more engaged user segment.

See `CLAUDE.md`'s Open Questions and `project.md`'s Goals/Success Metrics sections for the full detail.

## Live Links

All private by default — share from each artifact's own menu.

- **[Weekly Summary Prototype](https://claude.ai/code/artifact/d22034e8-634f-4012-a375-4270786bd1e2)** — the interactive prototype itself
- **[Four Rounds](https://claude.ai/code/artifact/d35aa31e-030c-499f-985c-20e2f54ada62)** — a slide deck covering the full feedback loop the prototype went through
- **[The Habit Gap](https://claude.ai/code/artifact/81972a96-b878-499b-a2cb-7eb66fc2dac3)** — a visual version of the competitive research

## How This Repo Is Organized

| Path | What it is |
|---|---|
| `CLAUDE.md` | Background context — product, my role, the triad, reporting line, open questions, and an index of every file below |
| `project.md` | PRD skeleton — problem statement, goals, non-goals, success metrics, current phase, stakeholders |
| `strategy.md` | The Engage v2 hypothesis, supporting evidence, tensions/complications, and competitive validation |
| `change_log.md` | Full decision audit trail — every significant change made in this repo, dated, with rationale |
| `research/` | `interview-synthesis.md` (3 user interviews), `nps-analysis.md` (10 NPS responses), `competitive-matrix.md` (5 competitor apps), `agentic-playtest.md` (simulated persona playtest of the prototype), `prototype-feedback.md` (real feedback on the published prototype) |
| `docs/` | `decision-brief.md` (1-page brief synthesizing all research for Marcus), `pm-brief.md` (the brief the prototype was built against) |
| `prototype/` | The interactive HTML prototype, its README, and `screenshots/` — full-flow screenshots across 4 rounds of feedback |
| `.claude/skills/session-save/` | An end-of-session hygiene skill that proposes updates to the tracking files above before writing anything |
| `.claude/skills/prd/` | Writes audience-calibrated PRDs (`/prd`) — grounded entirely in workspace files, every claim cited, in the same format as `docs/prd.md` |

## A Note on Evidence

This repo mixes real research (interviews, NPS, real prototype feedback) with simulated persona playtesting (Claude roleplaying personas grounded in the real interviews, not real usability sessions). Files and the "Four Rounds" deck are explicit about which is which — treat simulated rounds as hypothesis-generation, not proof of user behavior.
