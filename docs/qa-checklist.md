# QA Checklist — Weekly Summary Prototype

Grounded in `docs/spec-readiness.md`, `prototype/README.md`, and a fresh read of `prototype/index.html`.

## 1. Edge Case List

### Empty States
- **No transactions in the past week.** Addressed in intent by `docs/spec-readiness.md` (a distinct "quiet week" variant — not silence, not the spike template with empty data) — **not yet implemented anywhere in `prototype/index.html`**, which only renders the spike scenario.
- **No savings goal set.** Not addressed anywhere. The prototype hardcodes a goal ("Europe Trip") — there's no defined state for a user who never set one. Does the Goal Progress card disappear, prompt goal-setting, or show something else?
- **No app sessions in the past week** (user hasn't opened Nudge at all recently, independent of transaction activity). Not addressed — the prototype always fires the notification regardless of recent engagement. Should a already-disengaged user get a different message than someone who checks weekly?

### Edge Data Conditions
- **Single transaction only.** The Top Insight's two-bar comparison (Week 1 vs. this week) could look dramatically misleading off a sample size of one.
- **Duplicate/overlapping categories** (e.g., "Dining" vs. "Dining & Delivery" both matching due to a categorization glitch) — which one wins for the Top Insight figure?
- **Zero-dollar amounts** (a pending or fully-reversed transaction) — would render as "$0 this week," which could read as broken rather than genuinely uneventful.
- **Negative amounts** (a refund exceeding the period's spend). The bar chart's CSS (`.bar-fill { height: ...% }`) assumes a positive 0–100% range — nothing handles a negative value.
- **Very large amounts** relative to the comparison bar — no capping/scaling logic is visible; unclear how the chart would represent a spend far outside the two bars' current proportions.

### Multi-Account Scenarios
- **Multiple banks connected** — does "Dining & Delivery" aggregate across every linked account, or just one? Not specified anywhere.
- **Conflicting or duplicate data across accounts** (e.g., an internal transfer between the user's own accounts double-counted as spend).
- **One account disconnected or needs re-auth mid-week** — does the summary silently compute off partial data, or flag that it's incomplete?

### Permission States
- **Notifications turned off.** The entire flow in `prototype/index.html` depends on the push notification as the entry point — there's no fallback (in-app banner, email) defined anywhere if permission is denied.
- **Background app refresh off** (iOS) — if the summary is meant to be pre-computed before the notification fires, this could mean stale or unready data at open time. Not addressed.

## 2. PM QA Pass — `prototype/index.html`, Screen by Screen

| # | Screen | Check | Result |
|---|---|---|---|
| 1 | Lock screen | Tapping the notification opens the summary screen | **Pass** — verified via `openApp()` and click/keydown handlers |
| 2 | Lock screen | User can dismiss the notification without opening the app | **Cannot be determined** — real notification dismissal is an OS-level interaction; nothing to test in a phone-frame mockup |
| 3 | Summary screen | Goal name reflects the actual user's goal, not fixed sample data | **Cannot be determined** — this is explicitly illustrative sample data per the prototype's own note; no backend exists yet to verify against |
| 4 | Summary screen | Copy matches the confirmed non-judgmental tone (post Tom's playtest finding) | **Pass** — notification and insight headline both lead with forward-looking framing, not a deficit callout |
| 5 | Summary screen | Fund-source disclosure appears on the nudge card | **Pass** — "From your Chase checking account" is present |
| 6 | Summary screen | Any check that the $25 recommendation won't overdraft the account | **Fail** — no balance logic exists anywhere in the prototype or in `docs/spec-readiness.md` |
| 7 | Nudge interaction | Button shows a loading state before confirming | **Pass** — spinner + "Moving…" text via `completeNudge()` |
| 8 | Nudge interaction | Confirmation state updates goal amount and progress bar correctly | **Pass** — verified `$340→$365`, `34%→36.5%` |
| 9 | Nudge interaction | "Replay demo" fully resets all state | **Pass** — verified in-browser earlier this session |
| 10 | Cross-cutting | Basic keyboard operability and ARIA labeling on interactive elements | **Pass** (partial) — `:focus-visible` states and `aria-label` present on the notification button; a full assistive-tech audit (contrast, reading order across absolutely-positioned views) is out of scope for what this file can verify |

**Blocking before a real launch (not blocking for this prototype artifact, which is explicitly a concept mockup):**
- #6 — no overdraft/balance-safety check before recommending a transfer. This is a financial-trust issue, not cosmetic, and directly undercuts the reason this feature exists (see H1 in `docs/hypothesis.md`).
- The three empty states in Part 1 (no transactions, no goal set, no recent sessions) — users will hit all three in production; only one has even a defined intent (`docs/spec-readiness.md`), and none are implemented.

**Fine to ship as a known issue (for this prototype, at this stage):**
- #3 — hardcoded sample data is expected and disclosed for a concept mockup.
- #2 — no in-mockup dismiss affordance; real OS behavior handles this natively.
- #10 — partial accessibility coverage is acceptable for a concept prototype; track a full audit separately before production.

## 3. Draft PR Comment for Raj

> Not blocking this PR, but want to flag it before we're further down the road: I don't see anywhere — not in the prototype, not in `docs/spec-readiness.md` — that checks whether the $25 we're recommending would actually overdraft the user's checking account. Given how much of this feature's whole premise rests on trust (H1 in `docs/hypothesis.md`), a nudge that bounces feels like exactly the kind of thing that undoes it. Is this handled somewhere I'm missing, or should we get it explicitly onto the ticket before it goes further?
