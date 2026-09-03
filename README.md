# Nudge — Engage v2

PM working repository for the Engage v2 initiative at Nudge, a consumer personal finance app. Tracks the research, strategy, decisions, and a working prototype behind an effort to recover a 30-day retention decline.

## What This Is

Nudge's 30-day retention (the share of users still active 30 days after connecting their first bank account) dropped from 44% to 37% over two quarters, concentrated in users who go passive after their first week. This repo is the working record for **Engage v2** — the squad's effort to diagnose why, and to test a candidate fix: a personalized weekly summary (top spending insight, one contextual nudge, savings goal progress).

Owned by the Engage squad: Raj (Senior Engineer), Lena (Product Designer), and me (PM) — reporting to Marcus, Head of Product.

## New Here? Start With

This repo has 30+ files. Most of it is reference material you'll come back to as needed — you don't need to read it all on day one. To get oriented in about 10 minutes:

1. **This section, plus Current Status below** — the whole story in two minutes.
2. **[CLAUDE.md](CLAUDE.md)** — full background: product, squad, current state, a glossary for recurring shorthand, and open questions.
3. **[project.md](project.md)** — the PRD skeleton: problem statement, goals, current success metrics.
4. **[docs/open-items.md](docs/open-items.md)** — everything still pending a real person's sign-off, and every open product/technical question.
5. If you're picking up engineering or design work: **[docs/prd.md](docs/prd.md)**, the actual spec.

Everything else — research, data analysis, the prototype, presentations — is indexed and described in `CLAUDE.md`'s Related Files, grouped by category.

## Current Status

**Phase: Post-pilot, pre-scale.** A real controlled pilot ran in week 5 (`data/metric-findings.md`) and showed a statistically significant day-7 retention lift (76% vs. 46% control, p=0.002); day-30 is promising (36% vs. 22%) but not yet significant (p=0.123). A PRD (`docs/prd.md`) and a quarterly-review deck (`docs/presentation.md`) now exist.

The current ask, pending real sign-off from Marcus: expand the pilot to a properly powered sample (1,158 users/arm, ~5-7 weeks) before any full-rollout decision.

Two things remain explicitly open:
- **The causal link between week-1 goal-setting and reduced churn is unconfirmed** — multiple independent data points (a churned user who did the "right" onboarding steps anyway, and an NPS respondent whose goal was never reinforced) complicate reading it as causal rather than a proxy for a more engaged user segment.
- **H2 and H3** (priority-aware nudging; notification delivery reach) are both still low-confidence and unvalidated.

See `CLAUDE.md`'s Open Questions and `docs/open-items.md` for the full, current list — this section will drift, that file is the one to trust.

## Live Links

All private by default — share from each artifact's own menu.

- **[Weekly Summary Prototype](https://claude.ai/code/artifact/d22034e8-634f-4012-a375-4270786bd1e2)** — the interactive prototype itself
- **[Four Points to Marcus](https://claude.ai/code/artifact/e77f53b2-cf74-4d7d-a98d-e5532c87b85a)** — the quarterly-review deck, clean/minimal style (matches the Keynote-compatible export), same cited data as `docs/presentation.md`
- **[Four Rounds](https://claude.ai/code/artifact/d35aa31e-030c-499f-985c-20e2f54ada62)** — a slide deck covering the full feedback loop the prototype went through
- **[The Habit Gap](https://claude.ai/code/artifact/81972a96-b878-499b-a2cb-7eb66fc2dac3)** — a visual version of the competitive research

## How This Repo Is Organized

| Path | What it is |
|---|---|
| `CLAUDE.md` | Background context — product, my role, the triad, reporting line, current state, glossary, open questions, and a categorized index of every file below |
| `README.md` | This file |
| `project.md` | PRD skeleton — problem statement, goals, non-goals, success metrics, current phase, stakeholders |
| `strategy.md` | The Engage v2 hypothesis, supporting evidence, tensions/complications, and competitive validation |
| `change_log.md` | Full decision audit trail — every significant change made in this repo, dated, with rationale |
| `research/` | 5 files — real interview synthesis, real NPS analysis, real competitive research, real prototype feedback, plus one simulated persona playtest (clearly labeled) |
| `docs/` | 13 files — strategy & specs (decision brief, hypothesis, PRD, spec readiness), data-backed recommendations, prototype QA and design review, the quarterly-review deck, and `open-items.md` (everything pending real sign-off) — see `CLAUDE.md`'s Related Files for the full per-file index |
| `data/` | 4 files — real SQL analysis of the week-5 pilot, the retention diagnosis built on it, engineering-facing instrumentation asks, and the properly-powered follow-up design |
| `prototype/` | The interactive HTML prototype, its README, and `screenshots/` — full-flow screenshots across 4 rounds of feedback |
| `stakeholders/` | Profiles for Raj, Lena, and Marcus. **Local-only, gitignored — not in this repo.** They hold candid characterizations of real coworkers; see `CLAUDE.md` if you need to rebuild your own. |
| `.claude/skills/session-save/` | An end-of-session hygiene skill that proposes updates to the tracking files above before writing anything |
| `.claude/skills/prd/` | Writes audience-calibrated PRDs (`/prd`) — grounded entirely in workspace files, every claim cited, in the same format as `docs/prd.md` |

## A Note on Evidence

This repo mixes real research (interviews, NPS, real prototype feedback) with simulated work: persona playtesting, and two-agent simulated negotiations standing in for conversations that haven't happened yet with Raj, Lena, or Marcus. Every file involved is explicit about which is which — see `CLAUDE.md`'s Glossary for the specific ambiguities to watch for, and `docs/open-items.md` for which simulated outcomes are still awaiting the real conversation. Treat simulated work as hypothesis-generation and a drafted starting point, not as proof of user behavior or actual sign-off.
