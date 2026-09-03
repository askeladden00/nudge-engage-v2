# Open Items

A single consolidated list of everything in this workspace still waiting on a real decision — either a real person's sign-off, or an unanswered product/technical question. Update this by hand as items resolve or new ones surface; it's a snapshot, not a live system.

## Pending Real Sign-Off

1. **Raj** — `docs/spec-readiness.md`. A simulated two-agent negotiation resolved the H1 scope conflict, proposed a success metric, and defined zero-transaction behavior. No actual sign-off from Raj has happened yet.
2. **Lena** — `docs/design-review.md`. A simulated design review surfaced 3 gaps. One is resolved (see Backlog below); two are still open. No actual sign-off from Lena has happened yet.
3. **Marcus** — two separate asks:
   - `docs/recommendation-memo.md`: swap the primary success metric from action rate to day-7 retention. Note this supersedes `docs/spec-readiness.md`'s earlier metric proposal (24hr post-nudge action rate vs. control) — the day-7 retention proposal is the current ask.
   - `docs/presentation.md` (Slide 6): sign-off to extend the pilot to a properly powered sample (1,158 users/arm, ~5–7 weeks) before any full-rollout decision.

**Caveat on all three:** every negotiation above was two AI agents reasoning against the real workspace docs, not an actual conversation with Raj, Lena, or Marcus. Treat the outcomes as a strong starting point for the real conversation, not as decisions already made — see each file's own caveat section for detail.

## Open Product/Technical Questions

- **Overdraft/balance-safety check.** No logic is implemented anywhere — not in the prototype. A proposed behavior (check balance before showing the nudge; reduce or suppress it if unsafe) now exists in `docs/spec-readiness.md` §3, added 2026-09-02, but it's a draft pending Raj's real input on feasibility, not a locked spec. Flagged in `docs/qa-checklist.md` as blocking before a real launch (not blocking the current prototype artifact).
- **No savings goal set.** No defined state for a user who never set one. The prototype hardcodes "Europe Trip." Does the Goal Progress card disappear, prompt goal-setting, or show something else? (`docs/qa-checklist.md`)
- **Zero-transaction "quiet week."** Intent is defined (`docs/spec-readiness.md`: a distinct low-key variant, not silence, not the spike template with empty data) but not implemented in `prototype/index.html`.
- **No app sessions in the past week**, independent of transaction activity. Not addressed — the prototype always fires the notification regardless of recent engagement. (`docs/qa-checklist.md`)
- **Causal vs. correlational goal-setting link.** Is the week-1 goal-setting/retention correlation causal, or a proxy for a more engaged user segment? Complicated by Tom R., a churned user who did the "right" week-1 actions anyway (`research/interview-synthesis.md`), and by an NPS respondent whose goal went unreinforced (`research/nps-analysis.md`, #6). (`CLAUDE.md` Open Questions)
- **Weekly enrollment pace** for the properly-powered follow-up isn't yet confirmed with data/eng — needed to turn "~5–7 weeks" into an actual rollout date. (`data/experiment-design.md`, `docs/presentation.md` Slide 6)
- **H2 (priority-aware nudging: debt vs. goal)** — 25% confidence, not yet validated. Needs a small qualitative check with debt-carrying users before any build. (`docs/hypothesis.md`)
- **H3 (notification delivery reach)** — scored 30% confidence going in. Real week-5 open-rate data (28–56% vs. 4–6% control, holding across all 4 sends) argues against the original delivery-reach concern, so the score should be revisited upward — but hasn't formally been rescored. (`docs/hypothesis.md`, `data/metric-findings.md`)

## Backlog — Not Yet Built

From `research/agentic-playtest.md`'s stack-ranked list (#1, the transaction drill-down, is built; #2 is H2, tracked above):
- **#3 — Concrete goal-consequence framing.** Tie the spending comparison to a real consequence (e.g. "pushes your trip back ~4 days") instead of a generic percentage. Low effort relative to impact.
- **#4 — Re-engagement beyond a single notification.** Tom: "I'd need someone to put it in front of me... ask me again in a month." Not a prototype fix — a broader notification/re-engagement strategy question.

From `docs/design-review.md` (2 of Lena's 3 gaps still open — the third, an unremarkable-week template, is resolved: built into the prototype as the "Ordinary Week" scenario for PRD user story 5):
- **Relabel "personalized."** The Top Insight is a two-point delta, not pattern detection. `docs/prd.md` already specifies v1 copy should say "spending changed," not "personalized" — not yet confirmed as implemented.
- **Mock and test the subscription-spend scenario** before claiming the mechanism generalizes beyond the dining-spike case it was built and tested against.
