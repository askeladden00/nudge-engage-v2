# Onboarding Scenario — Sample Input for the AI Interview Demo

Not part of this project's real research or decision trail — a standalone teaching artifact for `docs/onboarding-demo-script.md`. It's a realistic, deliberately messy Slack-thread-style excerpt, written to be pasted into a fresh Claude Code session as the raw input for "the AI interview": ambiguous and underspecified on purpose, the way a real kickoff message actually is, so Claude has something genuine to ask clarifying questions about instead of a tidy pre-solved brief.

Grounded in this workspace's real facts (the retention numbers, the goal-setting correlation, the weekly summary email) — written in a rawer, first-contact voice, before any of the synthesis this repo now contains existed.

---

**#product-engage** · 3 participants

**Marcus** (9:14 AM)
hey — pulled the quarterly numbers and 30-day retention is down again. 44% -> 37% over the last two quarters. that's not noise anymore, three quarters running in the wrong direction

**Marcus** (9:15 AM)
can someone on Engage own digging into this? not asking for a fix yet, just want to understand what's actually happening before we commit to anything

**Me** (9:41 AM)
on it. anything specific already flagged, or fully open?

**Marcus** (9:52 AM)
support's been getting "I forgot this app existed" type tickets. and I know the weekly summary email open rate is like 22%, so people aren't even seeing whatever we do send them. beyond that, genuinely don't know — that's why I want real digging, not a guess

**Raj** (10:03 AM)
fwiw from the eng side nothing broke. no incident, no perf regression around when this started. if it's behavioral it's not from something we shipped

**Me** (10:07 AM)
ok. give me some time to actually talk to users and look at what we've got before I bring back anything that looks like a plan

**Marcus** (10:09 AM)
👍 no rush on the fix. rush on the understanding

---

## Using This in the Demo

Paste the thread above (or just this file's path) into a fresh Claude Code session with something like:

> Read `docs/onboarding-scenario.md`. This is the situation I'm walking into. Before you build or write anything, interview me — ask whatever you need to understand the problem, the team, and what "done" would look like.

The point of the exercise is watching Claude ask questions instead of jumping straight to a deliverable — Marcus's messages are intentionally short on specifics (no confirmed root cause, no success metric, no team roster beyond the three names above), so a good interview should surface exactly those gaps.
