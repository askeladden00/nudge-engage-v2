# Experiment Design — Full-Powered Weekly Summary Test

Pressure-tests the week-5 pilot result and designs the properly powered follow-up test, ahead of finalizing the recommendation to Marcus (`docs/recommendation-memo.md`).

## 1. Pilot Significance Check

**What significance means for a go/no-go call:** it tells you whether an observed difference is unlikely to be random chance — the test for real signal vs. noise from a small sample.

| | Control | Treatment |
|---|---|---|
| n | 50 | 50 |
| Day-30 retained | 11 (22%) | 18 (36%) |

**z = 1.543, two-tailed p = 0.1229 — NOT statistically significant at 95% confidence.**

**Plain-English read:** the 14-point gap is real and points the right direction, but at n=50/arm a gap this size could happen by chance roughly 1 in 8 times even if the feature does nothing. Not rare enough to bet a rollout on. **This is the answer that changes the recommendation memo** — the day-30 lift should be described as promising but unproven, not confirmed, anywhere it's referenced.

## 2. Minimum Detectable Effect (MDE)

**What it means, and why it's set before the test, not after:** MDE is the smallest effect worth caring about. Set after seeing results, it gets unconsciously tuned to justify whatever number you already have — set before, it keeps the test honest.

**MDE for this test: 5 percentage points** (baseline 22% → detecting a lift to 27%), deliberately more conservative than the pilot's observed 14-point gap.

## 3. Required Sample Size

**What power means, and the risk if it's too low:** power is the probability of correctly detecting a real effect if one exists. Too little power risks running the whole test and still walking away with an inconclusive result even when the feature genuinely works — a false negative, the expensive kind of mistake here.

**Inputs:** baseline 22%, MDE 5pts (target 27%), 95% confidence, 80% power.

**Result: n = 1,158 users per arm (2,316 total).**

This replaces the "~161/arm" figure previously noted in `data/metric-diagnosis.md` — that number was reverse-engineered from the pilot's own observed 14-point effect, which isn't the disciplined way to size a test. 1,158/arm is sized against the pre-committed 5pt MDE instead, and is the number that should be used going forward.

## 4. Test Duration

Total sample needed (2,316) is 2.7% of the 85,000 WAU pool — enrollment isn't the constraint, the 30-day maturation window per user is.

**Duration = enrollment time + 30 days.** The actual weekly rate of *new, test-eligible* signups (as opposed to total WAU, which includes existing active users) isn't specified anywhere in the workspace — presenting a range rather than inventing a precise figure:

| Assumed weekly eligible enrollment | Enrollment time | + 30-day observation | Total |
|---|---|---|---|
| 1% of WAU/week (850/wk) — conservative | ~2.7 weeks | +4.3 weeks | **~7.0 weeks** |
| 5% of WAU/week (4,250/wk) — generous | ~0.5 weeks | +4.3 weeks | **~4.8 weeks** |

**Fits within the 8-week max either way**, but margin ranges from ~1 week (conservative) to ~3 weeks (generous) — **confirm the real new-signup rate with data/eng before locking a date**, consistent with the same open item already flagged in `docs/recommendation-memo.md`.

## 5. The Decision

**Run the full powered test. Do not recommend scaling now.** The pilot isn't statistically significant yet (Section 1), and a properly powered test comfortably fits the 8-week window (Sections 3–4) — there's no reason to commit on an unproven number when proving it is both fast and cheap relative to a full rollout.

- **Risk of waiting:** ~5–7 more weeks of the documented retention decline continuing unaddressed while the team waits for a confirmed answer.
- **Risk of scaling now:** committing engineering/product effort and changing the live experience for the full base on a result with a real (~1-in-8) chance of being noise — wasted investment and credibility if it doesn't replicate.

## 6. Leading Indicators to Monitor Weekly

So the team isn't blind for the full 8 weeks:

1. **Day-7 retention, by weekly cohort** — the one metric already confirmed significant in the pilot (p=0.002); the earliest real signal of replication.
   **Get nervous if:** the treatment-control gap shrinks well below the pilot's +30pts, or flips negative, in any cohort.
2. **Weekly summary open rate, by cohort** — available same-day, the most immediately observable input.
   **Get nervous if:** open rate trends downward across cohorts instead of holding the pilot's 28%→56% pattern — would suggest the pilot's early, hand-picked population doesn't represent the broader base.
3. **Action rate vs. retention relationship (the H2 diagnostic)** — watches whether "acted-worse-than-opened" (31.0% vs. 42.1% in the pilot) replicates or was noise.
   **Get nervous if:** the inverse pattern persists or strengthens at scale — would mean the nudge's recommended action may be miscalibrated for a real subgroup, not an n=50 artifact.

## Summary Table

| Question | Answer |
|---|---|
| Is the pilot significant at 95%? | **No** (p=0.123) |
| MDE | 5 percentage points |
| Required sample size | **1,158 per arm (2,316 total)** |
| Estimated duration | **~5–7 weeks** (enrollment-rate dependent) |
| Fits 8-week max? | **Yes**, with 1–3 weeks of buffer |
| Recommendation | **Run the full test before scaling** |
