# Competitive Trends — Month-over-Month Log

Tracks what actually *changed* in the competitive landscape between runs of the competitive scan, so the industry's movement can be read without re-diffing full snapshots by hand. Each entry pairs with a dated archive in `research/competitive-history/`. The current state always lives in `research/competitive-matrix.md`.

Run this monthly via the `.claude/skills/competitive-scan/` skill (`/competitive-scan`) — manually triggered, no automation configured.

## 2026-08 — Baseline

First run. No prior month to diff against — see `research/competitive-history/2026-08.md` for the full snapshot. Findings as of this date:

- **YNAB:** $14.99/mo or $109/yr, single tier. Recent additions: Spending Breakdown, expanded Targets, Focused Views, Apple Card/Cash/Savings import, Together-plan collaboration, Public API upgrades.
- **Monarch Money:** New two-tier pricing (Core $8.33–14.99/mo, Plus $199/yr) introduced with the 2026 "Winter Release," which also added an AI Assistant, AI-powered insights, a weekly recap, receipt scanning, and equity tracking.
- **Rocket Money:** Free tier + pay-what-you-want Premium ($6–14/mo). Strong app-store ratings (4.5–4.6★) but a much weaker 3.3/5 on Trustpilot, with recurring complaints about surprise bill-negotiation charges and difficult cancellation.
- **Copilot Money:** $13/mo or $95/yr. Apple-only historically; a limited web app was added Dec 2025. Named an Apple Editor's Choice app and a "top budgeting app" in 2026; recurring complaint that auto-categorization rules aren't user-editable.
- **Chime *(banking-primary, not a like-for-like peer):*** No monthly fee. June 2026 update (v5.331.0) added "smart tools" and accessibility features, lifting its App Store rating from 3.04 to 3.77.

**White Space at baseline** (from `research/competitive-matrix.md`): (1) no competitor turns a stated goal into a recurring, personal touchpoint; (2) no competitor serves the casual, low-effort user without pushing them toward full budgeting discipline or a full dashboard. Both gaps open as of this baseline.

## 2026-09

Diffed against the 2026-08 baseline. Full snapshot: `research/competitive-history/2026-09.md`.

- **Rocket Money — material change.** Launched a new Premium Plus tier ($15/mo, limited release, broader rollout planned later in 2026) built around "Rowan," an AI agent that monitors accounts and proactively texts the user about savings opportunities (price increases, unexpected fees, trials about to convert), and can act on instruction via text (cancel, chase a refund). Shifts the engagement mechanism from purely alert/negotiation-based to a proactive, conversational, SMS-native one — the lowest-effort mechanism among all five as of this scan, though still savings-hunting rather than insight/habit-building.
- **Copilot Money — moderate change.** The beta "Money Assistant" expanded (Aug 12, 2026): can now create/update/delete categories, budgets, transactions, recurring transactions, and rules; surfaces proactive suggestions; shows charts in-chat; a beta MCP integration exposes budget/account data to third-party AI tools. Growing from passive categorization into an active conversational layer.
- **Monarch Money — minor, not structural.** A `MONARCHVIP` promo code (50% off first year) is circulating. Core/Plus pricing and features unchanged.
- **YNAB — no material change.** Pricing and feature set match baseline.
- **Chime — unconfirmed, not "no change."** Source quality was poor this cycle (name collisions with Amazon Chime and an unrelated calendar app; Chime's own changelog page returned stale cached content). App Store shows a general update dated 2026-08-27 with no available detail. Treat as an open gap in this scan, not a confirmed absence of change — worth a more targeted look next cycle.

**White Space re-check:**
- Gap 1 (goal-linked recurring touchpoint) — still fully open. Neither change above is goal-linked.
- Gap 2 (casual, low-effort user) — still open, but worth watching: Rowan is the first competitor move toward the *low-effort, notification-native* half of this gap, even though it's aimed at savings-hunting rather than insight delivery.
