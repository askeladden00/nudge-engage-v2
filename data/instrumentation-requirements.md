# Instrumentation Requirements — Weekly Summary Analytics

For Raj/engineering. Derived directly from gaps hit while analyzing the week-5 experiment (`data/metric-findings.md`, `data/metric-diagnosis.md`) — each item ties back to a specific hypothesis or question it would unblock, not a generic "track more stuff" ask.

**Format note:** split into what's actually new instrumentation (engineering's to build) vs. related asks that look similar but aren't (experiment design, content variants, qualitative research) — bundling those together would misrepresent scope.

## Priority 1 — Foundational Gap (blocks the most analyses)

### 1. Transactions / account-connection table
**Fields needed:** `user_id`, `account_id`, `transaction_date`, `amount`, `category`, `account_connected_date`.
**Why it matters:** this doesn't exist anywhere in the current dataset. Every "did this user have spending data" question so far has been answered with a proxy (session screens visited) instead of ground truth — see the confound check in `data/metric-findings.md`. Unblocks: precise zero-transaction/quiet-week detection (already a defined product behavior in `docs/spec-readiness.md` with no way to trigger it correctly today), and testing H4 (no-goal users) against what they actually had to look at, not just whether they visited a screen.
**Priority:** highest — this is the single gap most other items on this list are working around.

### 2. Notification permission status over time
**Fields needed:** `user_id`, `permission_status`, `changed_at`.
**Why it matters:** a silent permission revocation mid-experiment currently looks identical to "received it and ignored it." Unblocks H3 (general disengagement), and closes a permission-state edge case already flagged in `docs/qa-checklist.md`.
**Priority:** high.

## Priority 2 — Sharper Acquisition Data

### 3. Campaign/ad-source granularity on `acquisition_channel`
**Fields needed:** replace or supplement the single `paid`/`organic`/`referral` bucket with campaign ID or ad-source detail.
**Why it matters:** H1 (acquisition channel) is the highest-confidence hypothesis so far (7/10), but "paid" is currently one undifferentiated bucket — can't tell if all paid channels underperform equally or one specific source is dragging the average down.
**Priority:** medium.

## Priority 3 — Financial Context

### 4. Account balance trend / overdraft event tracking
**Fields needed:** periodic balance snapshots or overdraft-event log per user.
**Why it matters:** directly tests H2's "financially strained users are more likely to act on the nudge" explanation — currently inferred, not measured. This hypothesis is the one flagged as most urgent to resolve (it threatens the pending success-metric decision in `docs/decision-brief.md`).
**Priority:** high, tied to H2.

## Priority 4 — Behavioral Granularity

### 5. Session timestamps at time-of-day granularity + per-screen dwell time
**Fields needed:** `session_start_time` (not just date), and duration broken out per screen within a session, not just total `session_duration_seconds`.
**Why it matters:** unblocks H3 — raw session counts don't discriminate churned-vs-retained treatment users at all (5.22 vs. 5.39 sessions); finer-grained behavior might.
**Priority:** medium.

### 6. Days-since-last-session as a queryable field (or the ability to compute recency at any date, not just aggregate counts)
**Why it matters:** also H3 — recency right before the day-30 cutoff may matter more than total volume across the whole window.
**Priority:** medium.

## Already Available — No New Instrumentation Needed

- **Repeat vs. one-time action behavior.** Whether a user acts once vs. across multiple weeks is already sitting in `nudge_weekly_summary_sends` via `week_number` — worth querying before requesting anything new for H2.
- **Multivariate control on channel + variant + platform.** A modeling task, not a data gap — current fields already support this.

## Not Instrumentation — Flagging So Scope Doesn't Get Confused

- **Randomized action-assignment test (H2 causal test).** This is an experiment-design change (deciding to push some openers toward acting and others not), not a new field to log. Needs PM/Raj to scope as its own test, not a ticket for "add a column."
- **No-goal content variant (H4).** A product/content build — designing what a no-goal user should see instead of the current generic experience — not a data pipeline change.
- **Churned-user exit interviews (H3).** Research work, the same methodology behind `research/interview-synthesis.md` — not an engineering or instrumentation task at all.
