# PRD — Personalized Weekly Summary

**For:** Raj, Lena · **From:** Me (PM, Engage) · **Status:** v1 scope locked pending real triad sign-off (`docs/spec-readiness.md`)

## Problem Statement
30-day retention dropped from 44% to 37% over two quarters (`project.md`). Users who don't set a savings goal in week 1 churn ~2x more than those who do (`strategy.md`), though this correlation may not be causal — a churned user completed the same week-1 actions and still left (`research/interview-synthesis.md`). The app is static after initial setup: "the same dashboard every time" (Tom R.), "nothing has changed since the first day" (Amara L.) — `research/interview-synthesis.md`. Users want a directive next step, not just data: "I kept waiting for it to give me something to act on and it never really did" (Tom R.) — `research/interview-synthesis.md`.

## User
28-year-old who connected their Chase account 2 weeks ago and has not opened the app since (`docs/pm-brief.md`). **Job to be done:** understand where their money went this week and take one action (`docs/pm-brief.md`).

## Goals
- Ship H1: a transaction-level drill-down behind the top weekly insight, in-app only (`docs/spec-readiness.md`).
- Reads from existing goal-progress data — no new Goal model required (`docs/spec-readiness.md`).
- Reinforce a user's stated savings goal weekly — currently unaddressed after it's set (NPS #6, `research/nps-analysis.md`).

## Non-Goals
- Push notification infrastructure — not being built for v1 (`docs/spec-readiness.md`).
- H2 (priority-aware nudging: debt vs. goal) — explicitly out of scope, 25% confidence per `docs/hypothesis.md`, needs validation before any build.
- Full rollout — pending a properly powered test (1,158 users/arm; current pilot n=50/arm is not statistically significant at day-30, p=0.123) — `data/experiment-design.md`.

## Success Metrics
Primary: **day-7 retention** — the one metric already confirmed significant in the week-5 pilot (76% vs. 46%, p=0.002). Day-30 retention becomes primary once the full test reaches 1,158 users/arm (`data/experiment-design.md`).
Diagnostic only, not a success bar: action rate (% who act on the nudge within 24hrs). Pilot data shows users who acted retained *worse* (31.0%) than users who opened but didn't act (42.1%) — unconfirmed, possibly a selection effect, but not yet safe to optimize toward (`data/metric-diagnosis.md`).
Pending real sign-off from Marcus (`docs/recommendation-memo.md`).

## User Stories

1. As a user who hasn't opened the app in over a week, I want a weekly summary showing what changed, so I have a reason to return. *(Tom R., Amara L. — `research/interview-synthesis.md`)*
2. As a user viewing a spending insight, I want to see the actual transactions behind it, so I can verify it rather than take it on faith. *(H1, corroborated by 2 simulated personas + 1 real reviewer — `research/agentic-playtest.md`, `research/prototype-feedback.md`)*
3. As a user with a savings goal, I want to see my progress toward it in the summary, so it isn't forgotten after I set it. *(NPS #6 — `research/nps-analysis.md`)*
4. As a user acting on a nudge, I want to know which account the recommended transfer comes from, so I trust it won't overdraft me. *(No overdraft check exists anywhere in the current design — flagged as launch-blocking, `docs/qa-checklist.md`)*
5. As a user in an ordinary week — no spike, no zero-transaction week — I want the summary to still show something sensible, so the feature doesn't feel broken most weeks. *(No template exists for this case today; flagged as the highest-impact single change for retention — `docs/design-review.md`)*

## Acceptance Criteria
- Top insight renders with a transaction-level drill-down (merchant, date, amount) behind the headline figure.
- Goal progress reads from existing goal-progress data; no new data model introduced.
- Zero-transaction week sends a distinct low-key "quiet week" variant with a passive prompt — never silence, never the spike template with empty data (`docs/spec-readiness.md`).
- Nudge copy states the source account for any recommended transfer.
- H2 (debt-vs-goal logic) is absent from this build entirely — no partial implementation.

## Edge Cases to Handle
*(Full list: `docs/qa-checklist.md`)*
- **Empty states:** no transactions this week (defined above); no savings goal set (undefined — see Open Questions); no app sessions in the past week.
- **Edge data:** single transaction only; duplicate/overlapping categories; zero or negative amounts; amounts far outside the comparison bar's scale.
- **Multi-account:** multiple linked banks; conflicting/duplicate data across accounts; one account disconnected mid-week.
- **Permissions:** notifications off (no defined fallback channel today); background refresh off.

## Technical Dependencies
*(Full detail: `docs/codebase-summary.md`)* Reuses existing goal-progress and transaction-category data — no new Goal model or transactions table required for v1. Rough sizing from `docs/hypothesis.md`: comparable prior work (H2) estimated at 3.5–4.5 engineering days solo; this is a smaller scope (no new priority logic), sized similarly or less.

## Known Design Gaps
*(Full detail: `docs/design-review.md`)*
- Current copy implies "personalized" when the insight is a two-point delta, not pattern detection — v1 copy should say "spending changed," not "personalized."
- The feature's applicability beyond the dining-spike scenario (e.g., to a subscription-spend case like Amara's) is an untested assumption, not validated.

## Rollout Plan
Pilot (n=50/arm, week 5) → full powered test (1,158/arm, ~5–7 weeks, fits an 8-week max) → scale decision, pending Marcus (`data/experiment-design.md`, `docs/recommendation-memo.md`). No full rollout before the powered test concludes.

## Open Questions
- **Is the day-30 lift real?** Pilot is underpowered; full test needed (`data/experiment-design.md`).
- **Is action rate safe to use as a metric at all?** Currently correlates with worse retention, not better (`data/metric-diagnosis.md`).
- **What does the "ordinary week" template show?** Needs Lena's design input and a product decision (`docs/design-review.md`).
- **What happens when no savings goal is set?** No defined state today (`docs/qa-checklist.md`).
- **How does the app prevent recommending a transfer that overdrafts the user?** No answer exists yet (`docs/qa-checklist.md`).
- **Is the goal-setting/retention correlation causal?** Still unresolved (`CLAUDE.md`).
