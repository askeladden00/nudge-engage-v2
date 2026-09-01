# Metric Diagnosis — 30-Day Retention

Built on `data/metric-findings.md`, with additional SQL run directly against the same SQLite database (loaded from the public "Nudge Dataset" Google Sheet). One data-quality note surfaced while building this: the `opened`/`acted_on`/`day_30` columns import as **TEXT**, not integers — comparing them against a bare integer literal (`=1`) silently matches nothing in SQLite rather than erroring. Every query below either compares against a text literal (`='1'`) or explicitly `CAST(... AS INTEGER)` first; flagging this because it's an easy, silent way to get a confidently wrong answer from this dataset.

## 1. Metric Tree — What Actually Moves 30-Day Retention

```
30-Day Retention
│
├── Day-7 Retention (strongest single leading indicator)
│     D7=0 → 19.7% D30   |   D7=1 → 32.7% D30   (all users, n=500)
│     Whatever happens in the first week roughly doubles or halves the eventual D30 rate.
│
├── Weekly Summary Program (the lever under test, week-5 only)
│     ├── Delivery/Open Rate — NOT the bottleneck
│     │     28–56% (treatment) vs 4–6% (control) across all 4 sends, holds up rather than collapsing.
│     ├── Action Rate (acted_on) — NOT a clean positive lever
│     │     Counterintuitively, users who acted at least once retain WORSE (31.0%) than
│     │     users who opened but never acted (42.1%). See Part 4, H2.
│     └── Goal-Linkage (has a goal set vs. not) — NOT currently a differentiator
│           36.4% (has goal) vs 35.7% (no goal) within week-5 treatment — essentially flat.
│
├── Acquisition Channel — a real, consistent driver, independent of the summary
│     organic 30.9% > referral 26.5% > paid 20.2% (all users)
│     Same ordering holds inside week-5 treatment: organic 43.3% > paid 28.6% > referral 16.7%
│
├── Platform — a smaller but consistent driver
│     iOS 29.8% > Android 25.3% > Web 23.2% (all users)
│
└── General App Engagement (session frequency)
      Matters ACROSS cohorts (drives the week 1→4 decline, see Part 2) but does NOT
      discriminate churn WITHIN week-5 treatment (churned avg 5.22 sessions vs.
      retained avg 5.39 — essentially flat). Engagement gets you into the game;
      it doesn't explain who wins once everyone's already engaged enough to be here.
```

**The practical read:** the weekly summary's job is to move the *day-7* number (where it clearly works — see Part 3) more than to directly cause day-30 retention on its own. Acquisition channel and platform sit as real, independent drivers that any rollout decision needs to account for separately from whether the feature "works."

## 2. What Caused the Decline in Weeks 1–4 — Specifically

Retention: 32.0% → 25.0% → 25.0% → 22.0%. Three specific, data-grounded factors, not a general "engagement declined" story:

**a) Raw session volume drops steadily and tracks the decline closely.**
Avg sessions/user by cohort: **5.74 → 5.08 → 4.48 → 3.69** — a real, monotonic ~36% drop from week 1 to week 4. This lines up with the retention curve far more tightly than any single other variable checked.

**b) Week 4 specifically has a sharp, isolated drop in nudge engagement.**
Nudge open rate: 12.1% → 11.7% → 14.3% → **9.4%**. Acted-on rate: 4.2% → 4.5% → 6.6% → **3.2%**. Week 3 actually *improves* on open/act rate over weeks 1–2, but week 4 drops sharply on both — coinciding with week 4 posting the lowest retention (22%) of the four.

**c) A shifting acquisition mix partly explains the week 1→2 drop specifically.**
Paid-channel share rises from 31% (week 1) to 42% (week 2), and paid users retain ~10 points worse than organic across the whole dataset (20.2% vs. 30.9%). A heavier paid mix in week 2 is a real, quantifiable partial explanation for that specific week's drop — not just "more people churned."

**One thing that does *not* explain the pattern:** goal-setting rate. It moves 32% → 29% → **44%** → 27% — week 3 has the *highest* goal-setting rate of any cohort in 1–4, yet week 3's retention is flat with week 2 (both 25%), not improved. Whatever capped week 3 (most likely the still-declining session volume, 4.48 vs. week 1's 5.74) outweighed the benefit of more goal-setting that week.

## 3. What Week 5 Treatment vs. Control Tells Us About What the Summary Actually Fixed

It fixed **reach and early return**, not (yet, provably) **long-term retention on its own**:
- **Open rate**: the summary gets seen, repeatedly, at rates control never approaches (28–56% vs. 4–6%) — this is the clearest, most unambiguous win, and it directly answers H3's open question in `docs/hypothesis.md` about whether push notifications reach an already-disengaged segment. They do, in this cohort.
- **Day-7 retention**: +30 points (46%→76%), statistically significant (p=0.002). The summary clearly changes near-term behavior — users who get it come back within the week at a much higher rate.
- **Day-30 retention**: +14 points (22%→36%) — large, but not statistically significant at n=50/arm (p=0.123, see `data/metric-findings.md`).

**What this means specifically:** the summary is proven to solve the *first* problem this whole project set out to fix — "nothing brings users back after the first week" (`strategy.md`'s original hypothesis). It has not yet been proven to solve the deeper problem — whether that early return compounds into lasting retention. Those are different claims, and the data currently only fully supports the first one.

## 4. Four Ranked Hypotheses for Why Some Treatment Users Still Churned

18 of 50 treatment users retained to day 30; 32 churned despite being in the group that got the summary. Ranked by confidence, highest first.

### H1 — Acquisition channel explains more of the remaining churn than anything about the feature
**Prediction:** Users acquired via paid or referral channels churn at meaningfully higher rates than organic users, even within the treatment group — meaning some of this churn reflects who the user is at signup, not anything the summary did or didn't do.
**Confidence: 7/10** — the pattern is consistent at two different scales (whole dataset: organic 30.9% > referral 26.5% > paid 20.2%; within week-5 treatment: organic 43.3% > paid 28.6% > referral 16.7%), which is real signal — but the within-treatment referral cell is only 6 users, too small to fully trust its exact position.
**Would confirm it:** the same organic > paid ordering holding up with a larger, properly-powered treatment sample.
**Would rule it out:** the channel gap disappearing or reversing at scale, or a model controlling for channel still showing the full treatment effect independent of channel mix.

### H2 — Acting on the nudge doesn't cause retention, and may even be a warning sign
**Prediction:** Users who acted on the nudge (moved money) churn at a *higher* rate than users who opened but chose not to act — either because the population that needs prompting into a transfer already skews more financially strained (a selection effect, not a summary effect), or because completing one requested action satisfies curiosity without building a repeatable habit.
**Confidence: 5/10** — the reversal is real and clean in this data (31.0% retained among "acted," 42.1% among "opened but never acted," n=29 vs. 19), but the *why* is speculative — this is an observed pattern without a confirmed mechanism yet. **This matters beyond the number:** `docs/decision-brief.md`'s proposed success metric is literally "% of users who take an action within 24hrs" — if this pattern holds up, that metric may be measuring the wrong thing.
**Would confirm it:** users who act show measurably higher financial-strain indicators (e.g., lower balances, more overdraft activity) than users who merely open.
**Would rule it out:** a follow-up test that nudges some openers toward acting (rather than just observing who chooses to) shows acting *improves* retention when assigned rather than self-selected — proving the current read is confounded, not causal.

### H3 — General app disengagement doesn't explain who churns within treatment
**Prediction:** Among users who already received the summary, neither how often they use the app overall nor how long they spend reading the summary predicts who churns — meaning the answer for this specific group lies outside what's currently measured.
**Confidence: 4/10** — well-supported as a *negative* finding (churned avg. 5.22 sessions vs. retained 5.39; churned avg. summary read-time 107.6s vs. retained 96.4s — both essentially flat, if anything backwards), but as a positive hypothesis about what the real driver *is*, it's underspecified. This is closer to "ruling things out" than "finding the answer."
**Would confirm it:** a more granular engagement signal (time-of-day patterns, specific in-app dwell time, notification-permission changes over time) that still shows no separation between churned and retained.
**Would rule it out:** any such granular signal that *does* cleanly separate the two groups — meaning the driver was measurable, just not with the metrics checked here.

### H4 — Users without a savings goal get less value from the summary
*(Stated per the example format given — the literal hypothesis: "users who churned despite opening the summary did not have a savings goal set, so the summary had nothing to make progress on.")*
**Confidence: 2/10** — the data actively argues against this as currently measured. Within week-5 treatment, retention is essentially identical whether a user has a goal set or not (36.4% vs. 35.7%). This is the weakest-supported of the four, not the strongest, despite being the most intuitive-sounding.
**Would confirm it:** a version of the summary with no goal-progress content at all, tested specifically against no-goal users, shows meaningfully lower engagement/retention than a goal-having cohort gets from the current version.
**Would rule it out:** the existing finding (36.4% ≈ 35.7%) replicating at a larger sample — which would close this line of investigation rather than open it further.

## 5. Which Hypothesis to Test First

**H2 (acting doesn't cause retention) — not H1, despite H1 scoring higher on confidence.** The reasoning: H1 is the most *likely* to be true, but it's not actionable in a way that changes a decision — knowing acquisition channel matters doesn't tell the team to build or ship anything differently next sprint. H2 is different: it directly threatens a decision already in motion. `docs/decision-brief.md` has a success metric — "% of users who take an action within 24hrs of a nudge" — sitting pending Marcus's sign-off *right now*. If H2 holds up, that metric would be actively misleading: optimizing for "acted_on" could mean optimizing for the exact users who are least likely to stick around. That's a small-probability, high-consequence risk sitting directly in the critical path of a decision about to be locked in — worth resolving before, not after, Marcus signs off.

## 6. What Additional Data Would Raise Confidence on Each Hypothesis

Not all four need the same kind of fix — some just need a bigger sample, others need a genuinely different experiment, and one needs to leave this dataset entirely. See `data/instrumentation-requirements.md` for the engineering-facing version of the instrumentation asks below.

**H1 — Acquisition Channel (7/10)**
- Bigger sample on the same instrumentation: the within-treatment referral cell is only 6 users — too small to trust the ordering at that granularity.
- New instrumentation: `acquisition_channel` is a single bucket; campaign/ad-source-level granularity would show whether "paid" broadly is weaker, or one specific channel is dragging the average down.
- No new data needed: run channel + variant + platform as a proper multivariate model instead of separate univariate cuts, using data already collected.

**H2 — Acting Doesn't Cause Retention (5/10 — the one worth resolving first)**
- A different experiment, not more of the same one: "acting" is currently self-selected, so this can't distinguish selection from causation. Randomly assigning a push toward acting (a follow-up prompt or pre-filled default) to a subset of openers, then comparing, is the only clean causal test.
- New instrumentation: no financial context (balance trend, overdraft events) exists anywhere in this dataset — needed to test the "financially strained users are more likely to act" explanation directly instead of inferring it.
- Already queryable, not yet run: whether a user acts once vs. repeatedly across the 4 sends is sitting in `nudge_weekly_summary_sends` via `week_number` right now — worth checking before requesting anything new.

**H3 — General Disengagement Doesn't Explain It (4/10)**
- More granular behavioral data: only session *counts* exist today. Time-of-day patterns, days-since-last-session before churn, and per-screen dwell time could reveal a signal raw counts wash out.
- New instrumentation: notification-permission status over time isn't tracked — a silent revocation mid-experiment looks identical to "ignored it" today but means something different.
- Outside this dataset entirely: this hypothesis is really "we don't know yet." The honest fix may not be more transactional data at all, but a real round of exit interviews with churned week-5 treatment users, the same way `research/interview-synthesis.md` was built.

**H4 — No Goal = Less Value (2/10 — already well-argued against)**
- A different thing to test, not more sample: the flat result may be real, or it may be because no-goal users currently get the *same generic experience* as everyone else (`docs/qa-checklist.md` already flags that "no goal set" isn't a defined state). This can't be cleanly tested until no-goal users get something genuinely different to compare against.
- More N would tighten the confidence interval around "no difference," but is unlikely to overturn a result already this close to flat.

**The pattern across all four:** H1 and H2 need better analysis or experiment design more than raw volume; H3 needs to leave the dataset; H4 needs a different thing to test, not more of the current thing.
