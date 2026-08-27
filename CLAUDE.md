# Nudge — Background Context

## Product
Nudge is a consumer personal finance app that helps people build better money habits. Users connect their bank accounts, see where their money is going, set savings goals, and get nudges to stay on track. Launched about 4 years ago; well-funded and growing.

## My Role
I'm a PM at Nudge. I own the Engage squad — everything related to keeping users active after they connect their first account: the home feed, weekly money summaries, savings nudges, and push notifications.

## Triad
- Raj — Senior Engineer
- Lena — Product Designer
- Me — PM

## Reporting Line
I report to Marcus, Head of Product.

## Open Questions
- Is the week-1 goal-setting correlation causal, or a proxy for a more engaged user segment? Tom R. (churned user, see research/interview-synthesis.md) completed comparable week-1 actions — connected three accounts, set up a budget — and still churned at 5 weeks, which complicates reading the correlation as causal. A third data point reinforces this: an NPS respondent (research/nps-analysis.md, #6) set a savings goal and says the app "never once mentioned it since" — independent evidence that goal-setting alone isn't being reinforced by the product, regardless of its effect on churn.

## Related Files
- [README.md](README.md) — root repo overview: what this project is, current status, live links, file organization
- [project.md](project.md) — current situation, PRD skeleton (Problem Statement, Goals, Non-Goals, Success Metrics), phase, stakeholders
- [strategy.md](strategy.md) — Engage v2 hypothesis and supporting evidence
- [change_log.md](change_log.md) — decision audit trail
- [research/interview-synthesis.md](research/interview-synthesis.md) — synthesis of 3 user interviews (retained, churned, new)
- [research/nps-analysis.md](research/nps-analysis.md) — theme analysis of 10 NPS responses
- [research/competitive-matrix.md](research/competitive-matrix.md) — structured competitor research (5 apps) underlying The Habit Gap artifact
- [The Habit Gap](https://claude.ai/code/artifact/81972a96-b878-499b-a2cb-7eb66fc2dac3) — visual artifact version of the competitive matrix (private by default)
- [docs/decision-brief.md](docs/decision-brief.md) — 1-page decision brief for Marcus synthesizing all four research streams
- [docs/pm-brief.md](docs/pm-brief.md) — PM brief for the weekly-summary prototype (user, job-to-be-done, feature, constraint)
- [docs/hypothesis.md](docs/hypothesis.md) — learning synthesis (know/assume/don't know) and the updated hypothesis (H1/H2/H3, confidence-scored) superseding strategy.md's original hypothesis
- [docs/triad-session.md](docs/triad-session.md) — agenda, alignment template, and a labeled simulated outcome for the Raj/Lena working session on the prototype
- [docs/codebase-summary.md](docs/codebase-summary.md) — PM-level tour of firefly-iii/firefly-iii (reference codebase), feature mapping, and spec-relevant gaps for the weekly summary feature
- [prototype/](prototype/) — interactive weekly-summary prototype (notification → summary → nudge action → confirmation), see prototype/README.md
- [Weekly Summary Prototype](https://claude.ai/code/artifact/d22034e8-634f-4012-a375-4270786bd1e2) — shareable Artifact version of the prototype, for peer review (private by default)
- [research/agentic-playtest.md](research/agentic-playtest.md) — simulated persona playtest (Priya, Tom, Amara) of the prototype, with a stack-ranked backlog
- [research/prototype-feedback.md](research/prototype-feedback.md) — real user feedback on the published prototype
- [Four Rounds](https://claude.ai/code/artifact/d35aa31e-030c-499f-985c-20e2f54ada62) — slide deck covering the full feedback loop (4 rounds, before/after, backlog), private by default

## Repo
Pushed to a private GitHub repo: https://github.com/askeladden00/nudge-engage-v2

## Working Norms
- Proactively prompt before saving/updating project.md, strategy.md, change_log.md, or any new file we create together — don't save silently.
