# Codebase Tour — maybe-finance/maybe (Reference for Nudge Engage v2)

Explored by cloning [github.com/maybe-finance/maybe](https://github.com/maybe-finance/maybe) directly (not from memory) and reading the actual source: `README.md`, the repo's own `CLAUDE.md`, `db/schema.rb`, and the models/controllers/jobs referenced below.

**Important framing note:** this repo is explicitly no longer maintained (its `README.md` links a "final release," v0.6.0). Treat it as a frozen architecture reference — a real, production-grade example of how a personal-finance app models this domain — not a live codebase whose patterns are still evolving.

**Stack:** Ruby on Rails, PostgreSQL, Hotwire (Turbo + Stimulus), Sidekiq for background jobs, ViewComponents + Tailwind for UI.

## 1. PM-Level Tour

**What it does, in one sentence:** Maybe is a self-hostable personal finance app that aggregates a household's bank, investment, crypto, and property accounts (via Plaid sync or CSV import) into a single net worth and cash-flow view, with monthly budgeting and an AI chat assistant layered on top.

**How the codebase is organized:**

| Folder | What it does |
|---|---|
| `app/models/` (93 files) | Where the real business logic lives, by explicit team convention ("skinny controllers, fat models" — logic belongs on models, not in a services layer) |
| `app/controllers/` | Thin — mostly orchestrates models and renders views |
| `app/views/` + `app/components/` | ERB templates and reusable ViewComponents (their preferred unit for anything with variants, state, or interactivity) |
| `app/javascript/` | Stimulus controllers — deliberately minimal JS, native HTML preferred (`<dialog>`, `<details>`) over JS components |
| `app/jobs/` | Sidekiq background jobs — account syncing, imports, AI chat responses |
| `app/mailers/` | Only transactional emails exist today: password reset, invitation, email confirmation. **No digest or recurring summary email exists.** |
| `config/` | Routes, `schedule.yml` (cron jobs), initializers |
| `db/` | `schema.rb` (59 tables) — ground truth for what data actually exists |
| `test/` | Minitest + fixtures only — explicitly **not** RSpec or FactoryBot, by team convention |

**The 3 most important files for a PM building Nudge Engage v2:**
1. **`CLAUDE.md`** (repo root) — the maintainers' own architecture-and-conventions doc, written for AI coding agents. The single best "how this app is actually built, and why" document in the repo.
2. **`app/models/income_statement.rb`** — the reusable engine behind every spending insight (period-scoped category totals). This is functionally the class a weekly top-insight feature would call.
3. **`db/schema.rb`** — ground truth for what data exists, versus what a feature spec might assume exists.

**Key data models, and what they reveal about product decisions:**
- **User → Family → Account → Entry → Category.** Family, not User, is the tenancy boundary — multiple people can share a Family and its accounts. This is a "household" data model, a materially different assumption than a single-user product.
- **Entry is a `delegated_type`** covering Transaction, Valuation, Trade, and Transfer — "transactions" aren't a flat table; they're one of several record types layered under a shared base.
- **Budget/BudgetCategory are strictly monthly** (a unique DB index enforces one budget per family per calendar month). There is no weekly budget concept as a shipped feature.
- **There is no structured "savings goal" object.** The only `goals` field in the schema is a plain text array on `users`, populated during onboarding (e.g., "pay off debt") — a light onboarding signal, not a trackable object with a target amount or progress.
- **`Period` already has a built-in `"current_week"` definition** in code, even though nothing user-facing renders it today — the team clearly anticipated weekly views as a category of feature without ever shipping one.

## 2. Mapping the Weekly Summary Feature to This Codebase

**Where it would live:**
- A new controller alongside `budgets_controller.rb` / `pages_controller.rb` (e.g., `weekly_summaries_controller.rb`), or a new section on the existing dashboard.
- A new Sidekiq job (pattern-matched to `app/jobs/`) plus a new mailer (pattern-matched to `app/mailers/`) for the actual send — **neither exists today** for any recurring, personalized message.
- A new entry in `config/schedule.yml`, alongside the 3 that exist today — all of which are system-maintenance jobs (market data import, sync cleanup, security checks), none user-facing.

**Existing components it would touch or depend on:**
- **`IncomeStatement#expense_totals(period:)`** with **`Period.current_week`** — directly reusable for the "top insight" spending comparison; this math already exists.
- **`Category`** (for a "Dining & Delivery" grouping) and possibly **`Budget`/`BudgetCategory`** if goal progress becomes budget-progress rather than a new object.
- **`Entry`/`Transaction`** for transaction-level detail — the #1 finding from our own playtest ("show your work"). Because `Entry` is a `delegated_type`, "show me the transactions behind this number" is a join, not a flat-table query.
- **`Family`**, since every aggregation above is scoped to `Current.family`, not `Current.user`.
- **Nothing to extend for a savings goal** — there's no `Goal` model in this codebase to build on; it would be new.

**Blast radius — what could break if this ships with a bug:**
- `IncomeStatement` already powers the live dashboard's cash-flow sankey chart. A bug introduced while extending it for a weekly view risks the *existing* dashboard, not just the new feature — this needs to be additive, not a rewrite of shared logic.
- Category totals depend on sync accuracy (Plaid). A bug that ships a wrong weekly number isn't cosmetic — it's the exact trust failure our own playtest already identified as the top finding (H1 in `docs/hypothesis.md`).
- Because `Family` (not `User`) is the sharing boundary, a weekly summary built around one person's goal, sent through a shared household channel, could expose one family member's goal progress to another — a real privacy question this data model forces, that a single-user mental model would miss.

## 3. What This Means for How I Write the Spec

**Data that doesn't exist yet:**
- A structured savings-goal object (target amount, current progress, linked account/category) — today's `goals` field is just onboarding tags.
- A shipped weekly period/budget concept — `Period` supports it in code, but no controller, view, or job uses it.
- Push notification delivery infrastructure — `MobileDevice` only manages OAuth tokens for the mobile app's API access; there's no APNs/FCM sending code anywhere in the repo.
- Any digest-style recurring email — all 4 mailers that exist are one-off transactional emails.

**Existing constraints to call out in the ticket:**
- Monetary values must go through the `Money` object (base-currency conversion) — a raw sum will be wrong for any multi-currency family.
- "Skinny controllers, fat models" is an explicit convention — point engineers to extend `IncomeStatement` or add a model, not a services layer, to match house style.
- Testing is Minitest + fixtures only — worth stating up front so the ticket doesn't generate a testing-approach debate.

**The one thing engineers will ask that I should answer before scheduling kickoff:**
Since neither notification infrastructure nor a Goal model exists, the real fork in the road is: **is this scoped as (a) an in-app screen only, reusing existing data, or (b) the full notification-driven loop — which requires building push infrastructure and a new Goal model from scratch?** These are entirely different sizes of work, and estimation can't start until this is answered. This is the same question sitting in `docs/decision-brief.md`'s open "resourcing ask" — this codebase reference makes concrete just how large that ask actually is.
