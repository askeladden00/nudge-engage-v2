# Getting Started with Claude Code — A PM's Guide

*5-minute read. For anyone about to use this for the first time.*

## What Claude Code Actually Is

Claude Code is Claude, running in a folder on your computer instead of a chat window — it can read your files, write new ones, and keep working across many steps instead of one reply at a time. Think of it less like a chatbot and more like a very fast, very literal collaborator who remembers everything in the folder but nothing outside it.

## What You'll Build in Your First Session

You'll paste one prompt (ask whoever onboarded you for it, or see `docs/prd.md`'s workspace for a full working example) that sets Claude up to run the same kind of investigation this Nudge workspace ran: a background file that captures your product and team, a PRD skeleton, and a decision log — before any research or building starts. By the end of session one, you'll have a working folder Claude can pick back up correctly next time, even though it remembers nothing between sessions on its own.

## The 3 Habits That Matter Most

**1. Update the background file every session.** This project keeps one (`CLAUDE.md`) that Claude reads automatically every time you open the folder — product, team, current state, open questions. Claude has no memory between sessions; this file *is* its memory. If something real changed and the file doesn't say so, next session starts from a wrong picture.

**2. Interview before you build.** Don't hand Claude a problem and ask for a deliverable in the same breath. Ask it to interview you first — what's known, what's assumed, what "done" looks like. A five-minute interview catches the gaps that a half-built document hides until much later.

**3. Save everything, on purpose.** Every real decision gets a dated entry in a running log (`change_log.md`), with what was decided, who decided it, and why. Not because you'll read it back often — because six weeks from now, "wait, why did we do it this way" has an actual answer instead of a guess.

## The Single Most Common Mistake

**Treating something Claude generated *about* a real person or a real conversation as if it actually happened.**

It's genuinely useful to have Claude roleplay a stakeholder or a user to pressure-test an idea before the real conversation — this workspace does it repeatedly, and it produces real, useful drafts. The mistake is forgetting, an hour or a week later, that it was a rehearsal — and citing a simulated negotiation, a simulated interview, or a simulated debate as though it were the real person's actual answer.

**How to avoid it:** every simulated document in this workspace says so, loudly, at the top — look for it, and never take a decision "made" in one of those files as final until the real person has actually weighed in. When in doubt, check `docs/open-items.md`: if something's listed there as pending real sign-off, it doesn't matter how confident or well-reasoned the draft sounds — it isn't decided yet.
