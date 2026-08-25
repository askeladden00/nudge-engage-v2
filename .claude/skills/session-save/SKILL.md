---
name: session-save
description: End-of-session hygiene pass for Nudge Engage v2. Reviews what was discussed/decided in the current conversation and proposes updates to project.md, strategy.md, change_log.md, and CLAUDE.md — asking for approval before writing anything. Use when the user types /session-save or asks to wrap up / save session progress.
---

# Session Save

Project-scoped skill for the Nudge Engage v2 workspace.

## What this project's files are for

- `CLAUDE.md` — orientation only: product/role/triad/reporting-line background, open questions, the project files index, and working norms. Never duplicate content that lives in another file — if a fact belongs in project.md or strategy.md, link to it instead of restating it.
- `project.md` — current phase, key stakeholders, and the PRD skeleton (Problem Statement, Goals, Non-Goals, Success Metrics)
- `strategy.md` — the retention-recovery hypothesis, supporting evidence, and candidate direction(s)
- `change_log.md` — audit trail of decisions. Each entry is a `## YYYY-MM-DD` header followed by **Decision:**, **Made by:**, **Why:** lines, appended in chronological order (oldest first).

## Steps

1. Review the session for anything that changes the project's understanding: new facts, hypothesis changes, stakeholder/context updates, or decisions made (including documentation/process decisions — those get logged too, per established precedent).
2. Sort findings by destination (facts → project.md, hypothesis/direction → strategy.md, decisions → change_log.md). Anything that doesn't fit — ask before creating a new file.
3. Check CLAUDE.md hygiene — don't duplicate content that now lives elsewhere; only update it if the background, open questions, file index, or working norms actually changed.
4. Present a proposed diff, file by file, before writing anything. Wait for approval.
5. On approval, write the changes, matching each file's existing structure and tone.
6. If nothing warrants an update, say so — don't invent changes to justify the save.
