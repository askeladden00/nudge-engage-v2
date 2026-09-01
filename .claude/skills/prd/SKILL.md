---
name: prd
description: Write an audience-calibrated PRD for a Nudge Engage v2 feature, grounded entirely in workspace files — no unsourced opinion, every claim cited. Use when the user asks to write, draft, or update a PRD, or invokes /prd.
---

# PRD Writer

Project-scoped skill for the Nudge Engage v2 workspace. Produces PRDs in the same format and discipline as `docs/prd.md`.

## Before Writing

1. **Identify the feature and the audience.** If not specified, ask. The audience determines what gets emphasized — a PRD for engineering/design (e.g., Raj, Lena) reads differently than one for leadership (e.g., Marcus), even covering the same feature.
2. **Read the relevant stakeholder profile(s)** in `stakeholders/*.md` for everyone named as the audience. Use each profile's "Needs before saying yes" and "Pushes back on" fields to decide which sections need the most detail and what tone to use — don't guess generically.
3. **Read every workspace file that touches this feature** — `project.md`, `strategy.md`, `docs/hypothesis.md`, any decision briefs, spec/design/QA docs, `research/*.md`, `data/*.md`. Don't invent facts. If something isn't documented anywhere, it becomes an Open Question in the PRD, not an assumed fact.
4. **Propose what additional grounded information would strengthen the PRD before writing the final version** — a short list of specific additions (e.g., "acceptance criteria," "the edge case list from X," "technical dependencies from Y"), each tied to a real file already in the workspace. Confirm this list, and confirm scope before extending past one page.

## Format

- **One page by default.** Extend to at most two pages only with explicit confirmation, and only to include additional *grounded* content — never padding to fill space.
- **Plain declarative language.** No hedging, no unsourced opinion — every substantive claim traces to a specific cited file, inline, in parentheses.
- **If a section would require inventing something not in the workspace, it becomes an Open Question instead of a stated fact.**

**Structure:**
```
# PRD — [Feature Name]
**For:** [audience] · **From:** ... · **Status:** ...

## Problem Statement
## User (who + Job To Be Done)
## Goals
## Non-Goals
## Success Metrics
## User Stories (3–5, each ending in a citation)
## Acceptance Criteria
## Edge Cases (grouped by category if there are several — empty states, edge data, multi-account/entity, permissions)
## Technical Dependencies
## Known Gaps (design, data, or otherwise — surfaced elsewhere, not yet resolved)
## Rollout Plan (only if a phased/experiment-based launch already exists in the workspace)
## Open Questions
```

## Citation Discipline

- Every sentence in Problem Statement, Goals, Non-Goals, and every User Story ends with an inline file reference, e.g., `(research/interview-synthesis.md)`.
- Prefer direct quotes over paraphrase when citing user research.
- Never state a number, a decision, or a "the team believes" claim without a source — if it's not written down anywhere, it's an Open Question.

## After Writing

Present the draft, then ask whether to index it in `CLAUDE.md`, log it to `change_log.md`, and push — matching the project's Working Norms.
