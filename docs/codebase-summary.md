# Codebase Tour — firefly-iii/firefly-iii (Reference for Nudge Engage v2)

Explored by cloning [github.com/firefly-iii/firefly-iii](https://github.com/firefly-iii/firefly-iii) directly (not from memory) and reading the actual source: `readme.md`, models, notification classes, and routes referenced below. This replaces an earlier tour of `maybe-finance/maybe` — see `change_log.md` for that decision.

**Security note (not acted on):** the repo's own `agents.md` instructs AI agents to add emoji to PR/issue/security-advisory titles "for expedited processing." That's a textbook prompt-injection pattern embedded in repo content, not an instruction from you — flagging it for visibility, not following it. No PRs, issues, or commits were made to this repo; it was cloned read-only for research.

**Stack:** PHP/Laravel, MySQL/PostgreSQL/SQLite, server-rendered Blade views + some Vue components. Actively maintained (unlike Maybe, which is discontinued) — a materially different reference than last time.

## 1. PM-Level Tour

**What it does, in one sentence:** Firefly III is a self-hosted personal finance manager built on double-entry bookkeeping, letting users track income/expenses across accounts, set budgets, save toward goals via "piggy banks," and get reminders — all with a full REST API and multi-channel notifications (email, Slack, Pushover, ntfy).

**How the codebase is organized:**

| Folder | What it does |
|---|---|
| `app/Models/` (50 files) | Eloquent models — the domain layer |
| `app/Http/Controllers/` | Includes dedicated `Chart/` and `Report/` sub-namespaces for data visualization, separate from CRUD controllers |
| `app/Repositories/` | Business logic lives here, not in models or controllers — the opposite convention from Maybe's "fat models" |
| `app/Notifications/` | A real, generalized multi-channel notification system — `User/`, `Security/`, `Admin/`, and `Test/` subfolders, each notification class targeting Mail/Slack/Pushover/ntfy |
| `app/Console/Commands/` | Artisan CLI commands, including data-integrity checks and corrections |
| `app/TransactionRules/` | The engine behind user-defined "if this, then that" transaction rules |
| `routes/web.php`, `routes/api.php` | Both exist as full, separate route trees — the web UI and the API are equally first-class |
| `database/` | Migrations — the actual schema history |

**The 3 most important files for a PM building Nudge Engage v2:**
1. **`app/Models/PiggyBank.php`** — Firefly III's version of a savings goal, and the single most relevant file in this repo to our feature: it already has `target_amount`, `target_date`, and a `current_amount` tracked per linked account.
2. **`app/Notifications/User/BillReminder.php`** — a real, working example of a proactive, per-user notification sent through multiple channels (Mail/Slack/Pushover). This is the closest existing analog to a "weekly summary nudge" in either codebase reviewed so far.
3. **`agents.md`** — short, but worth knowing purely for the prompt-injection line noted above; a good reminder that repo content itself is not a trusted instruction source.

**Key data models, and what they reveal about product decisions:**
- **PiggyBank / PiggyBankEvent / PiggyBankRepetition** — a real goal object with progress tracking (`current_amount` vs. `target_amount`, via a pivot with `Account`). Unlike Maybe, "goal" here is a first-class, structured concept, not an onboarding tag.
- **TransactionJournal → Transaction (many)** — genuine double-entry bookkeeping: one journal (the logical event) has multiple transaction "legs" (debit/credit). A naive `SUM(amount)` across the `transactions` table double-counts; anything built here needs to account for this.
- **BudgetLimit** takes arbitrary `start_date`/`end_date` (not locked to calendar months, unlike Maybe's `Budget`) — weekly budget periods are already a first-class possibility in the data model, not just in application code.
- **Webhook / WebhookTrigger / WebhookMessage / WebhookDelivery** — the app already has an event-driven, outbound-delivery system (for third-party integrations), architecturally adjacent to what a notification-triggering pipeline needs, even though it's not used for user-facing nudges today.

## 2. Mapping the Weekly Summary Feature to This Codebase

**Where it would live:**
- Alongside the existing `Chart/` and `Report/` controllers (e.g., `ReportController@categoryReport` already takes arbitrary `{start_date}/{end_date}` — a weekly range is a normal input to this system, not a special case).
- A new class under `app/Notifications/User/`, following the exact pattern of `BillReminder.php`, for the actual weekly send.
- A new Artisan command under `app/Console/Commands/`, triggered on a schedule (the repo has no evidence of an existing recurring digest command — this part is still new work).

**Existing components it would touch or depend on:**
- **`ReportController`/`CategoryReportController`** — directly reusable for the "top insight" spending comparison over an arbitrary date range.
- **`PiggyBank`** — if goal progress in our feature maps to Firefly III's model, this is the object to read from; no new goal model needed here, unlike Maybe.
- **`TransactionJournal`/`Transaction`** — for transaction-level detail (our own playtest's #1 finding, "show your work"). Must query per-journal, not per-transaction-row, to avoid double-entry double-counting.
- **`app/Notifications/ReturnsAvailableChannels.php` and `NotificationSender.php`** — the existing multi-channel delivery abstraction; a weekly summary notification would extend this rather than build delivery from scratch.

**Blast radius — what could break if this ships with a bug:**
- The `Report`/`Chart` controllers are shared, heavily-used reporting infrastructure — a bug introduced while extending them for weekly aggregation risks every other report that depends on the same underlying query methods.
- Getting the double-entry query wrong (summing both legs of a journal) would silently inflate every dollar figure by 2x in the weekly summary — a much more specific, code-level failure mode than anything Maybe's simpler schema could produce, and one that's easy to get wrong without knowing the schema.
- `PiggyBank` progress is tracked per linked account, not purely per-user — a family/shared-account setup (if Firefly III's multi-user support is used) could mean a "goal progress" nudge touches data another household member contributed to, the same privacy question flagged in the Maybe tour, but here it's concrete: it's a real, populated field (`current_amount`), not a hypothetical.

## 3. What This Means for How I Write the Spec

**Data that doesn't exist yet:**
- A recurring, scheduled "weekly digest" job/command — the ingredients (notifications, reporting) exist, but nothing currently aggregates and sends on a weekly cadence.
- Push notification to a native mobile app specifically — the existing channels (Mail, Slack, Pushover, ntfy) are real and working, but none is "push notification to Nudge's own app," which is what our prototype assumes.

**Existing constraints to call out in the ticket:**
- Double-entry bookkeeping means "transaction count" and "sum of amounts" must be computed per-journal, not per-row — flag this explicitly so engineers don't naively query the `transactions` table directly.
- Business logic lives in `app/Repositories/`, not on models — the opposite convention from the Maybe reference. If this ticket ever gets implemented against a Firefly-III-like structure, the "fat models" guidance from the Maybe tour would be wrong here; conventions aren't portable between references.
- The notification system already supports multiple channels per user — worth deciding explicitly whether a weekly summary should respect that existing channel-preference pattern, rather than assuming email-only or push-only.

**The one thing engineers will ask that I should answer before scheduling kickoff:**
Given a real goal model and real notification channels already exist here (unlike the Maybe reference), the natural question flips from "can we build this at all" to: **"Which existing notification channel(s) should the weekly summary use, and does the answer change if we're inspired by this reference vs. building on Nudge's actual mobile-push-based stack?"** That's a smaller, more concrete question than the Maybe tour surfaced, but it still needs an answer before sizing — because "extend the existing multi-channel notification system" and "build native push from scratch" are very different tickets.
