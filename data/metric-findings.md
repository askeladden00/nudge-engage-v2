# Metric Findings — Nudge Weekly Summary Experiment

Source: [Nudge Dataset](https://docs.google.com/spreadsheets/d/1jMZXItXhbYxdBkzM74z2BXbCHHbnvqh4Eyclmmhdiww) (public Google Sheet, 5 tables). Downloaded via CSV export and queried with real SQL against a local SQLite database — every number below is computed, not estimated. This is the **first real quantitative data** this project has had; everything before this was qualitative (interviews, NPS) or simulated (agentic playtest).

**Data shape:** 500 users, cohort weeks 1–4 (100 users each, no experiment, `variant` empty) and cohort week 5 (100 users, split 50 `control` / 50 `summary_v1`).

---

## Q1 — 30-Day Retention by Cohort Week

**SQL:**
```sql
SELECT
  cohort_week,
  COUNT(*) AS n_users,
  SUM(day_30) AS retained_day30,
  ROUND(100.0 * SUM(day_30) / COUNT(*), 1) AS retention_pct
FROM nudge_retention
GROUP BY cohort_week
ORDER BY cohort_week;
```

**Plain English:** For each cohort week, count how many users are in it and how many were still active on day 30, then turn that into a percentage.

**Result:**
| Cohort Week | Users | Retained (D30) | Retention % |
|---|---|---|---|
| 1 | 100 | 32 | 32.0% |
| 2 | 100 | 25 | 25.0% |
| 3 | 100 | 25 | 25.0% |
| 4 | 100 | 22 | 22.0% |
| 5 | 100 | 29 | 29.0% |

**What it means for the scale decision:** Weeks 1→4 show a real, steady decline (32%→22%, a 10-point drop) — consistent with the retention problem this whole project exists to fix. Week 5 ticks back up to 29%, but **that's not a reversal of the trend — it's the treatment effect showing through.** Week 5 is a blend of 50 control users (22.0% D30, matching the week-4 trendline exactly) and 50 `summary_v1` users (36.0% D30). The blended average of those two is exactly 29.0%. Without the experiment, week 5 would almost certainly have continued the decline to ~21-22%.

---

## Q2 — Does Setting a Savings Goal in Week 1 Predict Better Retention?

**SQL:**
```sql
SELECT
  CASE
    WHEN u.goal_set_date IS NOT NULL AND u.goal_set_date != ''
         AND julianday(u.goal_set_date) - julianday(u.signup_date) <= 7
    THEN 'set_goal_week1'
    ELSE 'no_goal_week1'
  END AS goal_group,
  COUNT(*) AS n_users,
  SUM(r.day_30) AS retained_day30,
  ROUND(100.0 * SUM(r.day_30) / COUNT(*), 1) AS retention_pct
FROM nudge_users u
JOIN nudge_retention r ON u.user_id = r.user_id
WHERE u.cohort_week != '5'  -- excludes the active experiment cohort
GROUP BY goal_group;
```

**Plain English:** Join users to their retention outcome, label each user as having set a goal within 7 days of signup or not, and compare day-30 retention between the two groups. Run restricted to cohorts 1–4 so the active week-5 experiment doesn't confound a general behavioral question.

**Result (cohorts 1–4 only):**
| Group | Users | Retained (D30) | Retention % |
|---|---|---|---|
| No goal set in week 1 | 268 | 58 | 21.6% |
| Goal set in week 1 | 132 | 46 | 34.8% |

(All 5 cohorts pooled: 21.8% vs. 36.4% — nearly identical, confirms the experiment cohort isn't distorting this.)

**What it means for the scale decision:** This is real data support for the original "goal-setters churn less" finding referenced throughout this project (`research/interview-synthesis.md`, `strategy.md`) — goal-setters retain at roughly **1.6x** the rate of non-goal-setters, close to the "~2x" figure originally cited. **This is still correlational, not causal** — it doesn't resolve the open question already flagged in `CLAUDE.md` (is this a proxy for a more engaged user segment, or does goal-setting itself cause retention?). What it does do: it's the first real-data confirmation that the correlation the whole hypothesis was built on actually holds at this scale, not just in 3 interviews and 10 NPS responses.

---

## Q3 — Week 5 Only: Day-7 and Day-30 Retention, Treatment vs. Control

**SQL:**
```sql
SELECT
  u.variant,
  COUNT(*) AS n_users,
  SUM(r.day_7) AS d7_retained,
  ROUND(100.0 * SUM(r.day_7) / COUNT(*), 1) AS d7_pct,
  SUM(r.day_30) AS d30_retained,
  ROUND(100.0 * SUM(r.day_30) / COUNT(*), 1) AS d30_pct
FROM nudge_users u
JOIN nudge_retention r ON u.user_id = r.user_id
WHERE u.cohort_week = '5'
GROUP BY u.variant;
```

**Plain English:** Restrict to the week-5 experiment cohort, join to retention outcomes, and compare day-7 and day-30 retention rates between the `control` and `summary_v1` groups.

**Result:**
| Variant | Users | D7 Retained | D7 % | D30 Retained | D30 % |
|---|---|---|---|---|---|
| control | 50 | 23 | 46.0% | 11 | 22.0% |
| summary_v1 | 50 | 38 | 76.0% | 18 | 36.0% |

**Statistical significance** (two-proportion z-test):
- **Day-7: +30 points (46%→76%), z=3.08, p=0.002 — statistically significant.**
- **Day-30: +14 points (22%→36%), z=1.54, p=0.123 — not statistically significant at conventional (p<0.05) threshold**, despite being a large raw effect (a 64% relative lift).

**What it means for the scale decision:** This is genuinely good news, with one real caveat. The day-7 effect is large and statistically solid — the weekly summary clearly changes short-term behavior. The day-30 effect — the metric this entire project is actually about — points the same direction and is a big number, but **at n=50 per arm, it's not yet statistically distinguishable from noise.** A quick power calculation: detecting this exact effect size reliably (80% power, p<0.05) would need **~161 users per arm**, roughly 3.2x the current sample. **Recommendation: this is strong enough to justify continuing and expanding the experiment, not yet strong enough on its own to declare victory on the metric that matters most.** Scale the test, not (yet) the full rollout.

---

## Q4 — Did the Weekly Summary Open Rate Improve Across the 4 Sends vs. Control?

**SQL:**
```sql
SELECT
  variant,
  week_number,
  COUNT(*) AS n_sends,
  SUM(opened) AS n_opened,
  ROUND(100.0 * SUM(opened) / COUNT(*), 1) AS open_rate_pct
FROM nudge_weekly_summary_sends
GROUP BY variant, week_number
ORDER BY variant, week_number;
```

**Plain English:** For each combination of variant and send number (1st through 4th weekly send), count how many were opened out of how many were sent.

**Result:**
| Variant | Send # | Sent | Opened | Open Rate |
|---|---|---|---|---|
| control | 1 | 50 | 2 | 4.0% |
| control | 2 | 50 | 2 | 4.0% |
| control | 3 | 50 | 2 | 4.0% |
| control | 4 | 50 | 3 | 6.0% |
| summary_v1 | 1 | 50 | 14 | 28.0% |
| summary_v1 | 2 | 50 | 26 | 52.0% |
| summary_v1 | 3 | 50 | 26 | 52.0% |
| summary_v1 | 4 | 50 | 28 | 56.0% |

Every treatment-vs-control comparison is statistically significant (e.g., send 4: z=5.67, p<0.0001; all sends pooled: z=9.72, p<0.0001).

**What it means for the scale decision:** Two findings here, one expected and one worth calling out specifically:
1. **Open rate holds up over repeated sends rather than collapsing** — 28% → 52% → 52% → 56%. This is real, direct evidence *against* H3 in `docs/hypothesis.md` (the concern, raised by simulated-Tom, that push notifications might not reliably reach an already-disengaged segment). H3 was scored at only 30% confidence with a single simulated source behind it — this real data should meaningfully raise that confidence.
2. **The improvement isn't a steady climb — it jumps from send 1 to send 2 (28%→52%) and then plateaus** (52%→52%→56%). That's a different pattern than "trust builds gradually each week." Worth investigating what changed between send 1 and send 2 specifically, rather than assuming the whole 4-send arc is one smooth trend.

---

## Follow-Up — Does the Effect Hold Once You Account for Who Actually Had Data?

A real question worth asking before trusting Q3's lift: were treatment and control actually comparable, or did `summary_v1` just happen to land more users who had real spending activity to look at? **This dataset has no transactions or account-connection table**, so there's no exact way to answer "did this user have transactions this week." The closest available proxy: whether a user ever visited `spending_breakdown` or `transaction_detail` in `nudge_sessions`.

**SQL — balance check (is the proxy evenly split between arms?):**
```sql
WITH engaged AS (
  SELECT DISTINCT user_id FROM nudge_sessions
  WHERE screen IN ('spending_breakdown','transaction_detail')
)
SELECT u.variant, COUNT(*) AS n_users,
  SUM(CASE WHEN e.user_id IS NOT NULL THEN 1 ELSE 0 END) AS n_with_data,
  ROUND(100.0*SUM(CASE WHEN e.user_id IS NOT NULL THEN 1 ELSE 0 END)/COUNT(*),1) AS pct_with_data
FROM nudge_users u
LEFT JOIN engaged e ON u.user_id = e.user_id
WHERE u.cohort_week = '5'
GROUP BY u.variant;
```
**Result:** control 58.0% had spending data, `summary_v1` 56.0% — essentially balanced.

**SQL — does the treatment effect hold within each subgroup?**
```sql
WITH engaged AS (
  SELECT DISTINCT user_id FROM nudge_sessions
  WHERE screen IN ('spending_breakdown','transaction_detail')
)
SELECT
  CASE WHEN e.user_id IS NOT NULL THEN 'had_spending_data' ELSE 'no_spending_data_seen' END AS data_group,
  u.variant, COUNT(*) AS n_users, SUM(r.day_30) AS d30_retained,
  ROUND(100.0*SUM(r.day_30)/COUNT(*),1) AS d30_pct
FROM nudge_users u
JOIN nudge_retention r ON u.user_id = r.user_id
LEFT JOIN engaged e ON u.user_id = e.user_id
WHERE u.cohort_week = '5'
GROUP BY data_group, u.variant
ORDER BY data_group, u.variant;
```

| Group | Control D30 | Treatment D30 | Lift |
|---|---|---|---|
| Had spending data | 17.2% (5/29) | 32.1% (9/28) | +14.9pts |
| No spending data seen | 28.6% (6/21) | 40.9% (9/22) | +12.3pts |

**What it means:** The lift holds up at a similar magnitude in both subgroups — the retention effect looks like a real effect of the feature, not an artifact of treatment happening to land more data-rich, naturally-engaged users. **Two honest caveats:** these subgroups are small (21–29 people each, too small to trust a significance test on), and the proxy is imprecise — a whole-period "did they ever look" signal, not "did they have transactions in the specific week the summary covered." **The concrete fix:** add a per-week transaction count or account-connection flag to the data model so this split can be measured exactly instead of approximated — the same underlying gap already flagged in `docs/qa-checklist.md`'s empty-state edge cases, now showing up on the analytics side too.

## Overall Read for the Scale Decision

This is the first real quantitative evidence this project has had, and it's directionally consistent with everything the qualitative and simulated work pointed toward — but with one honest gap:
- **Ship-it signals:** goal-setting correlation replicates at real scale (Q2); day-7 retention lift is large and significant (Q3); open rate is strong, durable, and significantly beats control (Q4) — directly undercutting the H3 delivery-reach concern.
- **Not yet proven:** day-30 retention — the actual north-star metric — moved a lot (+14 points) but isn't statistically significant at the current sample size (Q3). This is an underpowered result, not a null one.
- **Recommended next step:** extend the week-5-style experiment to reach roughly 160 users per arm before treating day-30 lift as confirmed. This is a data point for `docs/decision-brief.md`'s still-open "Success Metric" item — day-30 action/retention lift vs. control is now a measurable candidate, not just a proposal.
