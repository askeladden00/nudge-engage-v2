# Nudge — Background Context

## Current State
Post-pilot, pre-scale. A real controlled pilot ran in week 5 (`data/metric-findings.md`) and showed a statistically significant day-7 retention lift; day-30 is promising but not yet significant. A PRD (`docs/prd.md`) and quarterly-review deck (`docs/presentation.md`) now exist. The active ask is Marcus's sign-off to expand the pilot to a properly powered sample before any full-rollout decision. See `docs/open-items.md` for everything still pending a real person's sign-off, and `project.md` for the current Goals/Success Metrics. If you're new to this repo, README.md's "New Here?" section has a short reading order.

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

## Glossary
- **H1 / H2 / H3** — the three ranked hypotheses in `docs/hypothesis.md` for what's driving the retention decline. H1 (transaction-level drill-down behind the top insight) is the one being built and piloted. H2 (priority-aware nudging: debt vs. goal) and H3 (notification delivery reach) are lower-confidence and not yet validated — see `docs/open-items.md`.
- **Priya / Tom / Amara** — this name set appears in two unrelated places, easy to conflate. `research/interview-synthesis.md`'s Tom R. is a **real** interview subject. `research/agentic-playtest.md`'s Priya, Tom, and Amara are **invented personas** Claude roleplayed to pressure-test the prototype — not real people, not a real usability session, and not the same Tom.
- **Real vs. simulated.** Several docs (`docs/spec-readiness.md`, `docs/design-review.md`, `docs/recommendation-memo.md`, `research/agentic-playtest.md`) contain two-agent simulated negotiations, debates, or playtests — clearly labeled inside each file — standing in for conversations that haven't happened yet with the real people. Treat these as hypothesis-generation and a draft starting point, not as actual sign-off or actual user research. `docs/open-items.md` tracks which of these are still awaiting the real conversation.

## Open Questions
- Is the week-1 goal-setting correlation causal, or a proxy for a more engaged user segment? Tom R. (churned user, see research/interview-synthesis.md) completed comparable week-1 actions — connected three accounts, set up a budget — and still churned at 5 weeks, which complicates reading the correlation as causal. A third data point reinforces this: an NPS respondent (research/nps-analysis.md, #6) set a savings goal and says the app "never once mentioned it since" — independent evidence that goal-setting alone isn't being reinforced by the product, regardless of its effect on churn.

## Related Files

**Core tracking**
- [README.md](README.md) — root repo overview: what this project is, current status, live links, file organization
- [project.md](project.md) — current situation, PRD skeleton (Problem Statement, Goals, Non-Goals, Success Metrics), phase, stakeholders
- [strategy.md](strategy.md) — Engage v2 hypothesis and supporting evidence
- [change_log.md](change_log.md) — decision audit trail
- [docs/open-items.md](docs/open-items.md) — consolidated list of everything pending real sign-off or still an open question

**Research — real**
- [research/interview-synthesis.md](research/interview-synthesis.md) — synthesis of 3 user interviews (retained, churned, new)
- [research/nps-analysis.md](research/nps-analysis.md) — theme analysis of 10 NPS responses
- [research/competitive-matrix.md](research/competitive-matrix.md) — structured competitor research (5 apps), always the latest snapshot; underlies The Habit Gap artifact
- [research/competitive-trends.md](research/competitive-trends.md) — month-over-month log of what changed in the competitive landscape between scans
- [research/competitive-history/](research/competitive-history/) — one dated, immutable snapshot per scan (e.g. `2026-08.md`), for comparing any two points in time directly
- [The Habit Gap](https://claude.ai/code/artifact/81972a96-b878-499b-a2cb-7eb66fc2dac3) — visual artifact version of the competitive matrix (private by default) — refreshed manually when the matrix changes materially, not on every scan
- [research/prototype-feedback.md](research/prototype-feedback.md) — real user feedback on the published prototype

**Research — simulated**
- [research/agentic-playtest.md](research/agentic-playtest.md) — simulated persona playtest (Priya, Tom, Amara — see Glossary) of the prototype, with a stack-ranked backlog

**Strategy, specs & decisions**
- [docs/decision-brief.md](docs/decision-brief.md) — 1-page decision brief for Marcus synthesizing all four research streams
- [docs/pm-brief.md](docs/pm-brief.md) — PM brief for the weekly-summary prototype (user, job-to-be-done, feature, constraint)
- [docs/hypothesis.md](docs/hypothesis.md) — learning synthesis (know/assume/don't know) and the updated hypothesis (H1/H2/H3, confidence-scored) superseding strategy.md's original hypothesis
- [docs/triad-session.md](docs/triad-session.md) — agenda, alignment template, and a labeled simulated outcome for the Raj/Lena working session on the prototype
- [docs/codebase-summary.md](docs/codebase-summary.md) — PM-level tour of firefly-iii/firefly-iii (reference codebase), feature mapping, and spec-relevant gaps for the weekly summary feature
- [docs/spec-readiness.md](docs/spec-readiness.md) — simulated Raj-vs-PM spec negotiation (two agents), resolving the H1 scope conflict, proposing a success metric, and defining zero-transaction behavior — pending real sign-off, see `docs/open-items.md`
- [docs/prd.md](docs/prd.md) — 2-page PRD for Raj/Lena, every line cited to a workspace file, no unsourced opinion; drove two prototype additions (transaction drill-down, ordinary-week scenario)

**Data & experiment design**
- [data/metric-findings.md](data/metric-findings.md) — real SQL analysis of the week-5 summary_v1 A/B experiment (first real quantitative data in this project): retention by cohort, goal-setting correlation, treatment-vs-control significance testing, and a data-availability confound check
- [data/metric-diagnosis.md](data/metric-diagnosis.md) — full diagnosis on top of metric-findings.md: a retention metric tree, specific causes of the week 1-4 decline, what the summary actually fixed (day-7, not yet proven day-30), and 4 confidence-scored, ranked hypotheses for remaining treatment churn
- [data/instrumentation-requirements.md](data/instrumentation-requirements.md) — engineering-facing instrumentation asks derived from the diagnosis, split into new instrumentation vs. already-available vs. not-instrumentation (experiment design, content, research)
- [docs/recommendation-memo.md](docs/recommendation-memo.md) — 1-page results memo for Marcus plus a simulated Marcus-vs-PM debate (two agents) that produced a real decision: swap the primary success metric from action rate to day-7 retention — pending real sign-off, see `docs/open-items.md`
- [data/experiment-design.md](data/experiment-design.md) — guided statistical walkthrough pressure-testing the pilot (not significant, p=0.123) and designing the properly powered follow-up (1,158 users/arm, ~5-7 weeks, fits an 8-week max), with 3 leading indicators to monitor weekly

**Prototype & QA**
- [prototype/](prototype/) — interactive weekly-summary prototype (notification → summary → nudge action → confirmation), see prototype/README.md
- [Weekly Summary Prototype](https://claude.ai/code/artifact/d22034e8-634f-4012-a375-4270786bd1e2) — shareable Artifact version of the prototype, for peer review (private by default)
- [docs/qa-checklist.md](docs/qa-checklist.md) — edge case list, a 10-point PM QA pass on prototype/index.html (pass/fail/cannot-determine), and a draft PR comment for Raj flagging a missing overdraft/balance-safety check
- [docs/design-review.md](docs/design-review.md) — simulated Lena-vs-PM design review (two agents), citing research/interview-synthesis.md for every user-need claim; surfaced 3 real gaps, 1 resolved, 2 pending real sign-off, see `docs/open-items.md`

**Presentations**
- [docs/presentation.md](docs/presentation.md) — 7-slide quarterly review narrative for Marcus, backboned by the recommendation memo and metric findings, calibrated to stakeholders/marcus.md
- [docs/presentation-notes.md](docs/presentation-notes.md) — full speaker notes for the deck, one sentence per line
- [Four Points to Marcus](https://claude.ai/code/artifact/e77f53b2-cf74-4d7d-a98d-e5532c87b85a) — the deck as an interactive artifact, pixel-art game styling, same cited data (private by default)
- [Four Rounds](https://claude.ai/code/artifact/d35aa31e-030c-499f-985c-20e2f54ada62) — slide deck covering the full feedback loop (4 rounds, before/after, backlog), private by default

**Stakeholders (local-only)**
- `stakeholders/raj.md`, `stakeholders/lena.md`, `stakeholders/marcus.md` — stakeholder profiles (workspace-confirmed facts + flagged defaults), each ending in the one thing that would most change prep for the next conversation. **Local-only, not in this repo** — they hold candid characterizations of real coworkers, so they're gitignored. If you're a teammate cloning this repo, these won't exist for you; ask the repo owner directly, or write your own from `docs/decision-brief.md`, `docs/triad-session.md`, `research/interview-synthesis.md`, and `docs/hypothesis.md` the way these were built.

**Skills**
- `.claude/skills/prd/` — reusable skill (`/prd`) that writes future PRDs in the same audience-calibrated, fully-cited format
- `.claude/skills/session-save/` — end-of-session hygiene skill that proposes updates to the tracking files above before writing anything
- `.claude/skills/competitive-scan/` — reusable skill (`/competitive-scan`) that re-runs the competitive analysis, archives a dated snapshot, and logs what changed since the last run. Manually triggered — intended roughly monthly, no automation configured.

## Repo
Pushed to a private GitHub repo: https://github.com/askeladden00/nudge-engage-v2

## Working Norms
- Proactively prompt before saving/updating project.md, strategy.md, change_log.md, or any new file we create together — don't save silently.
