# Retention Decline — PRD Skeleton

## Overview

_(Product, squad, and team background live in [CLAUDE.md](CLAUDE.md).)_

**Current phase**
Post-pilot, pre-scale. The team moved past problem-alignment: a prototype was built and iterated across 4 feedback rounds, a real controlled pilot ran in week 5 (`data/metric-findings.md`), and a PRD (`docs/prd.md`) and quarterly-review deck (`docs/presentation.md`) now exist. Current ask, pending real sign-off from Marcus: expand the pilot to a properly powered sample before any full-rollout decision (`docs/recommendation-memo.md`). See `docs/open-items.md` for everything still pending a real person's sign-off.

**Key stakeholders**
- Marcus — Head of Product (I report to him; he requested this write-up)
- Raj — Senior Engineer
- Lena — Product Designer

## Problem Statement
30-day retention dropped from 44% to 37% quarter-over-quarter. Users who don't set a savings goal in week 1 churn at roughly 2x the rate of those who do. User research indicates people hit a wall after the initial spending breakdown, with no clear next step. The home feed is static regardless of how recently a user last opened the app. The weekly summary email has a 22% open rate, but the in-app experience doesn't continue what the email started.

## Goals
- Ship H1 (transaction-level drill-down behind the top insight), in-app only, reusing existing goal-progress data — locked v1 scope, pending real triad sign-off (`docs/spec-readiness.md`).
- Reach a properly powered sample (1,158 users/arm, ~5-7 weeks) before any full-rollout decision (`data/experiment-design.md`).

## Non-Goals
- Full rollout before the properly powered test concludes — day-30 lift is promising but not yet statistically significant (`data/experiment-design.md`).
- H2 (priority-aware nudging: debt vs. goal) — explicitly out of scope, 25% confidence, needs cheap validation before any build (`docs/hypothesis.md`).
- Push notification infrastructure — not required for v1, reuses the existing channel (`docs/spec-readiness.md`).

## Success Metrics
- **Proposed, pending Marcus's real sign-off:** day-7 retention as primary (76% vs. 46% in the pilot, p=0.002, significant); day-30 retention becomes primary once the full test is properly powered. Action rate demoted to a diagnostic-only metric — users who act on the nudge currently retain *worse* (31.0%) than users who open but don't act (42.1%), so it isn't safe to optimize toward yet (`docs/recommendation-memo.md`, `data/metric-diagnosis.md`).
- Underlying business metric: 30-day retention rate (currently 37%, down from 44%).
