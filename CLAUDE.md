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
- [stakeholders/raj.md](stakeholders/raj.md), [stakeholders/lena.md](stakeholders/lena.md), [stakeholders/marcus.md](stakeholders/marcus.md) — stakeholder profiles (workspace-confirmed facts + flagged defaults), each ending in the one thing that would most change prep for the next conversation
- [docs/spec-readiness.md](docs/spec-readiness.md) — simulated Raj-vs-PM spec negotiation (two agents), resolving the H1 scope conflict, proposing a success metric, and defining zero-transaction behavior — all pending real sign-off from Raj/Lena/Marcus
- [data/metric-findings.md](data/metric-findings.md) — real SQL analysis of the week-5 summary_v1 A/B experiment (first real quantitative data in this project): retention by cohort, goal-setting correlation, treatment-vs-control significance testing, and a data-availability confound check
- [data/metric-diagnosis.md](data/metric-diagnosis.md) — full diagnosis on top of metric-findings.md: a retention metric tree, specific causes of the week 1-4 decline, what the summary actually fixed (day-7, not yet proven day-30), and 4 confidence-scored, ranked hypotheses for remaining treatment churn
- [data/instrumentation-requirements.md](data/instrumentation-requirements.md) — engineering-facing instrumentation asks derived from the diagnosis, split into new instrumentation vs. already-available vs. not-instrumentation (experiment design, content, research)
- [docs/recommendation-memo.md](docs/recommendation-memo.md) — 1-page results memo for Marcus plus a simulated Marcus-vs-PM debate (two agents) that produced a real decision: swap the primary success metric from action rate to day-7 retention — pending real sign-off from Marcus
- [data/experiment-design.md](data/experiment-design.md) — guided statistical walkthrough pressure-testing the pilot (not significant, p=0.123) and designing the properly powered follow-up (1,158 users/arm, ~5-7 weeks, fits an 8-week max), with 3 leading indicators to monitor weekly
- [docs/prd.md](docs/prd.md) — 2-page PRD for Raj/Lena, every line cited to a workspace file, no unsourced opinion; drove two prototype additions (transaction drill-down, ordinary-week scenario)
- [docs/design-review.md](docs/design-review.md) — simulated Lena-vs-PM design review (two agents), citing research/interview-synthesis.md for every user-need claim; surfaced 3 real gaps (overclaimed "personalized" label, untested subscription-scenario extrapolation, no unremarkable-week template) — pending real sign-off from Lena
- [docs/qa-checklist.md](docs/qa-checklist.md) — edge case list, a 10-point PM QA pass on prototype/index.html (pass/fail/cannot-determine), and a draft PR comment for Raj flagging a missing overdraft/balance-safety check
- [prototype/](prototype/) — interactive weekly-summary prototype (notification → summary → nudge action → confirmation), see prototype/README.md
- [Weekly Summary Prototype](https://claude.ai/code/artifact/d22034e8-634f-4012-a375-4270786bd1e2) — shareable Artifact version of the prototype, for peer review (private by default)
- [research/agentic-playtest.md](research/agentic-playtest.md) — simulated persona playtest (Priya, Tom, Amara) of the prototype, with a stack-ranked backlog
- [research/prototype-feedback.md](research/prototype-feedback.md) — real user feedback on the published prototype
- [Four Rounds](https://claude.ai/code/artifact/d35aa31e-030c-499f-985c-20e2f54ada62) — slide deck covering the full feedback loop (4 rounds, before/after, backlog), private by default

## Repo
Pushed to a private GitHub repo: https://github.com/askeladden00/nudge-engage-v2

## Working Norms
- Proactively prompt before saving/updating project.md, strategy.md, change_log.md, or any new file we create together — don't save silently.
