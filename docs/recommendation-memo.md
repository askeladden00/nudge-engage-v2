# Weekly Summary — Results Memo

**To:** Marcus · **From:** Me (PM, Engage) · **Re:** Week-5 weekly summary experiment results

## Recommendation
**Expand the experiment to a properly powered sample (1,158 users/arm — see `data/experiment-design.md`) before committing to a full rollout — not scale now, not wait a full quarter for more data.**

## Situation
We ran a controlled experiment in week 5's signup cohort: 50 users got the personalized weekly summary (`summary_v1`), 50 got nothing (`control`). We were testing whether it moves retention, not shipping it broadly.

## Evidence
- **Day-7 retention: 76% vs. 46% (+30pts) — statistically significant** (p=0.002).
- **Day-30 retention: 36% vs. 22% (+14pts) — large, but not yet statistically significant** at this sample size (p=0.123). A properly powered follow-up (95% confidence, 80% power, 5pt MDE) needs 1,158 users/arm — see `data/experiment-design.md`.
- **Open rate: 28–56% vs. 4–6%, every send** — holds up over 4 weeks rather than collapsing, all highly significant (p<0.0001).

## Ask
Sign-off to extend the experiment for the additional weeks needed to reach 1,158 users/arm (~5–7 weeks, fits the 8-week max — see `data/experiment-design.md`), and your input on the proposed success metric — a new finding complicates it (see below).

## Risk If We Wait
Every week we don't expand the experiment, retention keeps declining on the pattern already documented (32%→22% across cohorts 1–4), and we sit on a positive-but-unconfirmed signal instead of confirming it.

---

## Open Complication (surfaced after this memo was drafted)
Our diagnosis (`data/metric-diagnosis.md`) found that users who acted on the nudge retained *worse* (31.0%) than users who opened but didn't act (42.1%) — directly complicating the proposed success metric ("% who act within 24hrs").

---

## Debate Outcome (simulated — Claude played Marcus using `stakeholders/marcus.md`, a spawned agent played the PM)

Not a real conversation with Marcus — a rehearsal for one. Three questions, in order:

1. **"Is n=50/arm enough to trust this?"** Resolved honestly: day-7 (p=0.002) is real, not noise. Day-30 (p=0.123) is genuinely underpowered, not null — 1,158/arm needed for a properly powered test (see `data/experiment-design.md`), not a vague "trust it."
2. **"What's the cost of waiting?"** Reasoned through the actual math (50 new users/arm/week from week 5's enrollment) rather than inventing a date — flagged that the real enrollment pace needs confirming with data/eng before promising a timeline. Mid-debate, the PM briefly argued for shipping now (cheap H1 build cost + solid day-7 signal) — a real inconsistency with the memo's own recommendation.
3. **"Why trust a metric your own data casts doubt on?"** — combined with catching the inconsistency above. Resolution: the memo's "extend, don't scale" stands, because the H2 finding (unconfirmed, possibly a selection effect) adds a *second* open question on top of the unproven day-30 lift — two stacked uncertainties is a worse position to ship from than one. **New decision: swap the primary success metric from action rate to day-7 retention now, day-30 once properly powered — action rate demoted to a diagnostic metric, not the bar for success.**

**Aligned outcome:** Extend the experiment to reach 1,158 users/arm (up from an earlier, less rigorous ~161/arm estimate — see the correction note in `data/experiment-design.md`). Confirm actual weekly enrollment pace with data/eng before committing to a date. Success metric is now day-7 retention (day-30 once powered), not action rate. Revisit once H2 (acted-worse-than-opened) is confirmed or ruled out.

**Caveat:** this entire exchange was two AI agents reasoning against the actual data — it produced a genuinely useful reconciliation and a concrete metric change, but no real sign-off from Marcus happened. Treat the aligned outcome as a strong draft for the real conversation, not a decision already made.
