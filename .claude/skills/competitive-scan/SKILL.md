---
name: competitive-scan
description: Re-run the Nudge Engage v2 competitive analysis, archive a dated snapshot, and log what changed since the last run. Use when the user asks to update, refresh, or re-run the competitive research, or invokes /competitive-scan. Intended to run roughly monthly.
---

# Competitive Scan

Project-scoped skill for the Nudge Engage v2 workspace. Repeats `research/competitive-matrix.md`'s original research on a recurring cadence, preserving every past run so industry changes can be tracked over time — not just the current state.

**This skill is manually triggered** (run `/competitive-scan`, or ask in a session) — there is no unattended scheduling in this workspace. If a monthly cadence matters, the recurring job is on the human, not the tool.

## Files This Skill Owns

- `research/competitive-matrix.md` — always the **latest** snapshot. Overwritten each run.
- `research/competitive-history/YYYY-MM.md` — one dated, immutable archive per run, in the same format as the matrix. Never edit a past month's file — each is a record of what was true at that time.
- `research/competitive-trends.md` — a running log, one `## YYYY-MM` entry per run, of what changed since the previous run. This is the file that answers "how has the industry moved," without re-reading every full snapshot.

## Steps

1. **Check the last run.** Read `research/competitive-trends.md`'s most recent entry and the newest file in `research/competitive-history/` to know what was true last time and how long it's been.
2. **Re-research the same competitor set** — YNAB, Monarch Money, Rocket Money, Copilot Money, Chime — using the same categories as the existing matrix (Core features, Pricing, Target customer, Post-connection engagement mechanism, Notable recent changes), sourced the same way (current pricing pages, "what's new"/changelog pages, recent reviews). Cite every source, same as the original.
3. **Do one light pass for new entrants** in the spending-insights/habit-building category. If something genuinely new and relevant turns up, flag it as a candidate addition and ask before folding it into the ongoing competitor set — don't silently expand scope.
4. **Diff against the last snapshot**, competitor by competitor: pricing changes, feature additions/removals, positioning shifts, notable rating or review-sentiment changes. "No material change" is a valid, expected finding for any given competitor in any given month — don't manufacture a change to justify the run.
5. **Re-check the White Space section** (`research/competitive-matrix.md`'s "gaps none of them own well") against this month's findings — note explicitly whether each gap still holds or has started to close.
6. **Present the diff before writing anything**: the new snapshot's content, and the drafted `research/competitive-trends.md` entry. Wait for approval, matching the project's Working Norms.
7. **On approval:**
   - Write `research/competitive-history/YYYY-MM.md` (the full new snapshot, dated to this run).
   - Overwrite `research/competitive-matrix.md` with the same content (it stays the "latest" pointer everything else in the workspace already links to).
   - Append the new entry to `research/competitive-trends.md`.
   - Log the run to `change_log.md` (Decision/Made by/Why, per the established format).
   - If "The Habit Gap" artifact is still linked from `CLAUDE.md`, flag that it's now stale relative to the new matrix and ask whether to republish it — don't republish without asking.
8. **If nothing changed at all** across every competitor, say so plainly in the trends entry rather than padding it — a real "no material change this month" is useful signal, not a failure to find something.
