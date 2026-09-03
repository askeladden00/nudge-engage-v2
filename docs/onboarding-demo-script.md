# 15-Minute Live Onboarding Demo — Presenter Script

For running with a teammate who has never used Claude Code, inside this Nudge workspace. Companion to `docs/onboarding-guide.md` (give them that first, or right after — it's a 5-minute read).

**One rule for the whole demo: nothing gets actually saved to this repo's real tracking files.** You'll show Claude proposing changes more than once — every time, the answer is "don't save that," because this is someone else's real project, and the point of the demo is watching the mechanics, not adding demo content to Nudge's actual history. Say that to your teammate up front, out loud, before you start — it's also the first live example of Habit 3 (save on purpose, not by default).

Have `docs/onboarding-scenario.md` and this repo open before you start. Know where a second, empty folder is for minutes 12–15 (anywhere outside this repo — a new folder on Desktop is fine).

---

## Minutes 0–2 — Open the folder, see what Claude already knows

1. In a terminal: `cd` into this repo, then run `claude`.
2. While it loads, tell your teammate: *"The first thing it does is read one file — CLAUDE.md — automatically, every time. That file is its entire memory of this project between sessions."*
3. Once it's up, type: **"What's the current state of this project, and who's on the team?"**
4. Point at the answer, not at Claude — it should correctly name the Current State, the triad (Raj, Lena, PM), and Marcus as the manager, without you having told it anything this session. That's the whole point of minute 0–2: *this came from a file, not from Claude remembering you.*
5. Optionally scroll `CLAUDE.md` open in an editor side-by-side so they see the actual file producing those answers — especially the Glossary section and `docs/open-items.md` pointer, since those come back in the mistake-avoidance habit later.

---

## Minutes 2–7 — The AI interview, and Plan Mode

1. Say: *"Now watch what happens when I hand it a real, messy problem instead of a tidy one."*
2. Type: **"Read docs/onboarding-scenario.md. This is the situation I'm walking into. Before you build or write anything, interview me — ask whatever you need to understand the problem, the team, and what 'done' would look like."**
3. Let it ask 2–4 clarifying questions before you answer anything. Narrate as it happens: *"Notice it didn't start writing a document — it's asking about the exact gaps Marcus's messages left open: no confirmed cause, no success metric."* This is Habit 2 from the guide, live.
4. Answer a couple of its questions with whatever's natural (you can improvise — this is a demo, the answers don't need to be real).
5. Once it starts proposing next steps (drafting a background file or a plan), switch modes — `Shift+Tab` cycles Claude Code's modes; land on **Plan Mode**. Say: *"This makes it show me the plan before touching any files — nothing gets written until I approve it."*
6. Let it present a plan. Read one line of it out loud, then say clearly: **"That looks right, but let's not actually save this — it's a demo scenario, not real Nudge work."** Exit without executing.

---

## Minutes 7–12 — Run a skill, then hand over the keyboard

1. Say: *"Now the other habit — saving on purpose. There's a skill for it."*
2. Type: **"/session-save"** (or "run session save" if slash commands aren't set up yet).
3. Walk through what it does out loud as it runs: it reviews the session for anything real that changed, sorts findings by which file they'd belong in, and — this is the part to point at — **it will very likely come back and say there's nothing worth saving**, since minutes 2–7 were just an interview with no real decisions made. Say: *"That's not it being lazy — the skill is explicitly told not to invent changes just to justify running. That restraint is the save-on-purpose habit."*
4. **Hand over the keyboard.**
5. Have your teammate jot one or two sentences of something real about *themselves* — not Nudge facts, e.g. "I'm a PM on [their team], main problem right now is [whatever's true]."
6. Have them type **"/session-save"** themselves and watch what happens: since their notes aren't Nudge facts, the skill should recognize they don't belong in this project's files and say so, rather than forcing them in somewhere. That's a second live example of the same restraint — and a natural segue to "so where *would* your own notes go?"
7. Whatever it proposes: **they decline the save.** Still a guest in this repo.

---

## Minutes 12–15 — Their turn, their product, their folder

1. Move to the second, empty folder — outside this repo entirely.
2. Run `claude` there fresh. Point out: *"Empty folder, no CLAUDE.md — it knows nothing about anything right now."*
3. **They** paste the reusable workspace prompt (the one from your earlier session — have it ready to hand them, e.g. in a text file or your clipboard history) into the prompt, filling in their own product, team, and problem where the brackets are.
4. They send it. The prompt's own last line asks Claude to interview them before drafting anything — so the demo ends with **them** answering **their own** AI interview, live, in their own new workspace.
5. That's the handoff: they finish the session running it, not watching you.

---

## If You're Short on Time

Minutes 0–2 and 12–15 are the two that must not get cut — everything else is in service of those. If something runs long, compress the Plan Mode explanation in minutes 2–7 to one sentence rather than skipping minute 12–15's handoff.
