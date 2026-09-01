# Decision Brief — Engage v2 Retention Recovery

**To:** Marcus (Head of Product) · **From:** Me (PM, Engage) · **Re:** 30-day retention decline

## Situation
30-day retention has dropped from 44% to 37% over the last two quarters, concentrated in users who go passive after their first week. Four independent sources — team/product data, user interviews, NPS feedback, and a competitive scan — now triangulate on the same root cause: users get an initial "aha" from the spending breakdown, then the app gives them nothing further to act on.

## Key Findings
_Caveat: the findings below are qualitative and small-N (3 interviews, 10 NPS responses) — directionally consistent with each other, but not yet validated against usage data at scale._

- **The goal-setting/churn correlation is weaker than it first looked.** Users who skip a week-1 savings goal churn ~2x more (product data) — but Tom R. completed comparable week-1 actions and still churned (interview), and an NPS respondent set a goal the app "never once mentioned again" (NPS #6). Three independent signals now suggest the product isn't reinforcing goals, regardless of their effect on churn.
- **The app goes static immediately after setup.** Described independently by a churned user, a brand-new user, and three separate NPS respondents ("same dashboard every time," "nothing has changed since day one," "nothing new to discover").
- **Users want to be told what to do next, not just shown data.** A recurring theme in both interviews (Tom, Amara) and NPS ("I want Nudge to feel like a financial coach, not a spending tracker").
- **Time-to-value is dangerously slow relative to user patience.** The one retained user's payoff took ~3 months, and she believes most people quit before then; the churned user left at 5 weeks; the new user is already stalling at day 10.
- **No competitor owns this gap either.** Across the 4 category peers scanned (YNAB, Monarch Money, Rocket Money, Copilot Money), none deliver a recurring, low-effort, goal-linked "here's your progress, here's what's next" touchpoint — Monarch's weekly recap is the closest analog but reads as a report, not a directive next step.

## Options Considered
1. **Ship Lena's personalized in-app weekly summary** — one insight, one actionable nudge, and goal progress, surfaced weekly. Directly targets the most-cited finding (staleness/no next step) and matches both competitive white-space gaps. Raj has confirmed it's feasible with existing data; it requires new ranking logic to decide which insight to surface.
2. **Resolve the goal-setting causal question first, before building anything.** Lower upfront cost, but delays shipping any fix this quarter while the team already has three independent, converging data points.
3. **Narrower first step: reconnect goal progress to the existing home feed/email**, without the full weekly-summary redesign — addresses the single most concrete, low-effort win identified (NPS #6) while deferring the larger ranking-logic investment.

## Recommended Action (proposed for Thursday's discussion — not yet a decision)
Recommend the team align on Option 1 — Lena's personalized weekly summary concept, starting with the smallest testable slice (surfacing goal progress) — as the direction to pursue, while validating the causal-vs-correlation question in parallel rather than treating it as a blocker. This is a recommendation to align on at Thursday's meeting, consistent with the problem-alignment-before-solutioning scope Marcus set — not a build decision already made.

## Open Items Before This Can Be Greenlit
- **Resourcing ask:** No estimate yet for the "new ranking logic" work Raj flagged as required — needs sizing from Raj before this can be scoped into a quarter.
- **Success metric:** `project.md` still lists Success Metrics as undefined by the team. Before shipping even the smallest slice, we need agreement on what number moves (and by how much) to call it working. **Update:** real week-5 experiment data now exists (`data/metric-findings.md`) — day-30 retention lift vs. control (+14pts, 22%→36%) is a measurable candidate, though not yet statistically significant at the current sample size (~161/arm needed for 80% power).

## Why Now
This is the first time interviews, NPS feedback, and competitive research have independently converged on the same specific gap — goal-setting isn't being reinforced, and nothing in the app gives users a reason to return in the days after their first insight — rather than each pointing at something different. That convergence is what's changed since last quarter, and it's why Thursday is a reasonable point to align on a direction, even with the open items above still unresolved.
