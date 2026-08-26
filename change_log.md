# Change Log — Engage v2

Audit trail of decisions made as Engage v2 progresses. Each entry: date, decision, who made it, why.

## 2026-08-17
**Decision:** Stood up project.md, strategy.md, and change_log.md to track Engage v2.
**Made by:** Me
**Why:** Establish shared documentation before Thursday's problem-alignment meeting.

## 2026-08-17
**Decision:** Trimmed CLAUDE.md to remove content duplicated in project.md and strategy.md (Situation, Engage v2, Decisions sections), replacing it with a single Related Files index. project.md's Overview now points to CLAUDE.md for product/squad/team info instead of restating it.
**Made by:** Me
**Why:** CLAUDE.md and project.md held the same facts in two places, risking drift as one got updated without the other. Each fact now has one owning file.

## 2026-08-17
**Decision:** Created a session-save skill (.claude/skills/session-save/SKILL.md) to standardize end-of-session hygiene passes across project.md, strategy.md, change_log.md, and CLAUDE.md.
**Made by:** Me
**Why:** Make the "propose updates, wait for approval" workflow repeatable via /session-save instead of relying on ad hoc reminders each session.

## 2026-08-19
**Decision:** Added a Tensions/Complications section to strategy.md and an open question to CLAUDE.md noting that the week-1 goal-setting/churn correlation may not be causal.
**Made by:** Me
**Why:** research/interview-synthesis.md surfaced a churned user (Tom R.) who completed comparable week-1 onboarding actions and still churned, complicating the existing hypothesis's supporting evidence.

## 2026-08-19
**Decision:** Added research/nps-analysis.md (theme analysis of 10 NPS responses) and cross-referenced it in CLAUDE.md's Open Questions and the Related Files index.
**Made by:** Me
**Why:** The NPS analysis independently reinforces the goal-setting causal-vs-correlation open question — a respondent set a savings goal and reported the app never referenced it again, a third data point alongside Tom R.'s interview.

## 2026-08-19
**Decision:** Added research/competitive-matrix.md (5-competitor analysis: YNAB, Monarch Money, Rocket Money, Copilot Money, Chime) and linked its two white-space findings under strategy.md's Early Direction section.
**Made by:** Me
**Why:** The competitive gaps identified (no one turns a goal into a recurring personal touchpoint; no one serves the casual low-effort user) independently support Lena's weekly-summary concept, giving it external validation alongside the internal interview/NPS evidence. Note: Chime was included per explicit request despite being a banking-primary product outside the stated category filter — flagged in the doc rather than treated as a like-for-like competitor.

## 2026-08-19
**Decision:** Created docs/decision-brief.md, synthesizing product data, interview-synthesis.md, nps-analysis.md, and competitive-matrix.md into a 1-page brief (Situation, Key Findings, Options Considered, Recommended Action, Why Now) for Marcus.
**Made by:** Me
**Why:** Consolidate four independently converging research streams into a single decision-ready document ahead of Thursday's problem-alignment meeting.

## 2026-08-19
**Decision:** Revised docs/decision-brief.md after a roleplayed review pass (not real feedback from Marcus): reframed Recommended Action as a proposal for Thursday rather than a settled decision, added a small-N/qualitative caveat to Key Findings, trimmed Chime out of the Key Findings bullet, rewrote "Why Now" to drop rhetorical framing, and added an explicit "Open Items Before This Can Be Greenlit" section (resourcing ask, success metric) rather than inventing answers to either.
**Made by:** Me
**Why:** The review surfaced real document-quality gaps (scope creep past the problem-alignment mandate, unlabeled small sample size, an unresourced ask, an undefined success metric) that were fixable with existing information, without treating simulated feedback as if a real stakeholder had given it.

## 2026-08-19
**Decision:** Added research/competitive-matrix.md and docs/decision-brief.md to CLAUDE.md's Related Files index.
**Made by:** Me
**Why:** Both files were created and cross-linked elsewhere earlier this session but never indexed in CLAUDE.md — caught during a /session-save hygiene pass.

## 2026-08-19
**Decision:** Built an interactive weekly-summary prototype (docs/pm-brief.md, prototype/index.html, prototype/README.md) — a phone-frame mockup of the notification-to-app flow: notification tap → weekly summary (top insight, goal progress, contextual nudge) → nudge action → confirmation state.
**Made by:** Me
**Why:** First testable artifact against the Engage v2 direction, built on the specific PM brief (28-day-old Chase-connected, inactive user; job-to-be-done: understand spending and take one action) and grounded directly in the interview synthesis, NPS analysis, competitive matrix, and decision brief. Verified working end-to-end in-browser; one spacing bug (insight headline overlapping the bar chart) found and fixed during verification.

## 2026-08-19
**Decision:** Changed the hardcoded goal name in prototype/index.html from "Emergency Fund" to "Europe Trip" (goal card, nudge copy, and CTA button).
**Made by:** Me, approved based on findings from an agentic persona playtest (see research/agentic-playtest.md — simulated, not real user research)
**Why:** Playing Priya's persona against the prototype surfaced that a goal name mismatched to what the user actually set breaks trust right at the moment the nudge asks for action — the highest-priority fix identified in round 1 of the playtest.

## 2026-08-19
**Decision:** Rewrote the notification body and Top Insight headline in prototype/index.html to lead with neutral/forward-looking framing instead of a spending callout ("Dining spending jumped" / "3× what you spent" → "one easy move to stay on pace" framing).
**Made by:** Me, approved based on findings from an agentic persona playtest (see research/agentic-playtest.md — simulated, not real user research)
**Why:** Playing Tom's persona surfaced that deficit-first framing at the entry point reads as judgment before the user reaches the well-received action — the highest-priority fix identified in round 2 of the playtest.

## 2026-08-19
**Decision:** Saved prototype/screenshots/round2-01-lock.png, round2-02-summary.png, round2-03-confirmed.png — full-flow screenshots of the current prototype state (after Priya's and Tom's fixes), for future slide-deck use.
**Made by:** Me
**Why:** User asked for screenshots preserved in the workspace, not just viewed inline. Found a working technique (html2canvas rendered in-page, triggered as a browser download, which lands directly in the project root) after the browser tool's native screenshot action proved to have no file-export path. Will reuse this technique for subsequent rounds so a full before/after set exists for deck-building.

## 2026-08-19
**Decision:** Corrected the screenshot round numbering and captured the full before/after set: renamed the existing set to round3-* (state Amara actually evaluated, with both Priya's and Tom's fixes applied), then temporarily reverted prototype/index.html twice to reconstruct and capture round1-* (original state, what Priya saw) and round2-* (Priya's fix only, what Tom saw), restoring the file to its current state afterward and verifying it still works end-to-end.
**Made by:** Me
**Why:** The originally-saved set only reflected the current (post-both-fixes) state; rounds are more useful for the eventual deck if they show what each persona actually reacted to, not just the latest state. All 9 screenshots (3 rounds × 3 states) now live in prototype/screenshots/.

## 2026-08-19
**Decision:** Completed the agentic persona playtest (round 3, Amara) and closed it out with a stack-ranked list of unaddressed findings — see research/agentic-playtest.md. No prototype change made for round 3.
**Made by:** Me, based on the playtest (simulated, not real user research)
**Why:** Amara's finding (nudge assumes savings is the priority over debt payoff) requires real nudge-logic changes, not a copy fix — patching it shallowly risked papering over the finding rather than addressing it, so it was carried into the final backlog instead. The backlog ranks it #2 by severity despite higher build cost, and ranks "show transaction-level detail" #1 since it was raised independently by both Priya and Amara and is purely additive.

## 2026-08-19
**Decision:** Published the prototype as a shareable Artifact ("Weekly Summary Prototype") for peer review, adapted from prototype/index.html to fit the Artifact HTML skeleton (same CSS/JS, wrapper tags stripped).
**Made by:** Me
**Why:** User asked to host the prototype at a public URL for peer review, ahead of building the slide deck. Private by default — sharing is the user's call from the artifact's own menu.

## 2026-08-19
**Decision:** Saved real user feedback on the published prototype to research/prototype-feedback.md, and implemented two quick fixes: added breathing room between the Top Insight headline and its bar chart (margin-bottom 1.5rem → 2.1rem), and added a fund-source line to the nudge card ("From your Chase checking account"). Applied to both prototype/index.html and the published Artifact (same URL, republished).
**Made by:** Me
**Why:** Real feedback flagged the Top Insight box as visually cramped and the $25 nudge's fund source as unclear — both low-risk, additive fixes. The feedback also raised a transaction-breakdown request that independently confirms backlog item #1 in research/agentic-playtest.md (previously only simulated-persona evidence); logged as a cross-reference rather than a new item.

## 2026-08-19
**Decision:** Added the published Artifact link to CLAUDE.md's Related Files and prototype/README.md; also indexed research/agentic-playtest.md and research/prototype-feedback.md in CLAUDE.md (both were missing from the index). Corrected stale "Emergency Fund" references in prototype/README.md to "Europe Trip," and added a "Feedback on This Prototype" section linking the playtest, real feedback, and screenshots.
**Made by:** Me
**Why:** The README had drifted out of sync with the prototype after the goal-name fix, and several files created this session were never indexed in CLAUDE.md — a hygiene catch-up consistent with the file-index discipline established earlier in the session.

## 2026-08-19
**Decision:** Captured round4-01-lock.png, round4-02-summary.png, round4-03-confirmed.png — full-flow screenshots of the current prototype state (after the two real-feedback fixes: Top Insight spacing, $25 fund-source line).
**Made by:** Me
**Why:** Needed for a full before/after slide deck covering all four rounds (Priya, Tom, Amara, real feedback). All 12 screenshots (4 rounds × 3 states) now live in prototype/screenshots/.

## 2026-08-19
**Decision:** Built and published a 10-slide deck ("Four Rounds") as a self-contained Claude Artifact, covering the full feedback loop: title with an upfront simulated-vs-real caveat, a grounding slide tying each round to its source research, one slide per round (Priya, Tom, Amara, real feedback) with real embedded screenshots, a cumulative before/after, the stack-ranked backlog, the live prototype link, and a closing "what this is not" slide. Added to CLAUDE.md's Related Files.
**Made by:** Me
**Why:** Requested as a shareable summary of the iteration loop. Built with image placeholders substituted via a Python script (base64-encoding screenshots directly into the HTML) rather than routing large binary data through the conversation. Structural checks passed (balanced tags, all 9 images embedded, no leftover placeholders) but I could not render a local preview (file exceeded what the preview pane would open) or verify the hosted version myself (preview browser isn't authenticated to claude.ai) — flagged to the user as needing a manual check.

## 2026-08-19
**Decision:** Wrote root README.md (project overview, status, live links, repo structure), added .gitignore excluding .claude/settings.local.json, initialized git, and pushed the repo to a new private GitHub repo (https://github.com/askeladden00/nudge-engage-v2).
**Made by:** Me, with explicit user sign-off at each gate (README content, secrets review, staged-file list, commit message, repo visibility/name/new-vs-existing) before anything was committed or pushed.
**Why:** User requested the workspace be published to GitHub as a durable, shareable record. Scanned all files for secrets/credentials/PII first (none found) — settings.local.json excluded as local dev config, not project content, not a security concern.
