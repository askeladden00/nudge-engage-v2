# Agentic Persona Playtest — Weekly Summary Prototype

**What this is:** Simulated persona interviews (Claude playing Priya / Tom / Amara from the persona profiles below), reacting to [prototype/index.html](../prototype/index.html). This is **not real user research** — treat findings as hypotheses to validate with actual users, not as evidence on par with `research/interview-synthesis.md` or `research/nps-analysis.md`.

## Persona Profiles Used
- **Priya**, 28, software engineer, SF. Earns well but spends without tracking. Connected Nudge after a big month of eating out. Has a Europe trip savings goal. Checks bank app weekly, usually via alert. Motivated by progress, anxious about unexpected spending totals.
- **Tom**, 34, marketing manager, Chicago. Abandoned three budgeting apps in two years. Feels guilty about money, doesn't want to be lectured. Connected via friend's recommendation. Hasn't opened it since day one. Skeptical any app changes his behavior.
- **Amara**, 41, operations lead, Atlanta. Paying down credit card debt while saving for her kids' activities. Checks accounts regularly, already has a spreadsheet system. High bar for trust — a wrong-looking number ends the relationship.

---

## Round 1 — Priya

**In-character answers:**

1. *What do you think this does?* — Reads it as a weekly recap notification that leads with something she'd actually be anxious about (the dining spike) instead of making her dig for it.
2. *How would you arrive at this experience?* — Notification → tap → straight into the summary, no login friction. Approved of the low-friction entry.
3. *Would you change your spending based on this?* — The "3x your first week" line triggered real anxious-attention. But the goal card said "Emergency Fund" when her actual goal is a Europe trip — broke her trust right at the moment she was being asked to act. Said she'd still double-check her real accounts afterward rather than trust the confirmation.
4. *Magic wand?* — Tie the goal name to what she actually set up, and connect the spending spike to a concrete consequence for her real goal ("pushes your trip back ~4 days") rather than a generic percentage. Also wanted merchant-level detail behind the $186, not just a category total.

**Synthesis:**
- **Struggled with:** The goal-name mismatch broke trust exactly when the nudge asked her to act.
- **Surprised me:** The break happened at step two (goal card), not step three (the ask) — the flow's emotional arc (concern → understanding → action) was interrupted before the action itself even loaded.
- **Most worrying answer:** #3 — she completed the full flow and still said she'd verify manually afterward. That means the flow added a screen in front of the old checking habit instead of replacing it.

**Highest-priority change:** Make the goal name reflect what the user actually set, instead of a fixed default.

**Action taken (approved):** Replaced all instances of the hardcoded "Emergency Fund" goal name with "Europe Trip" across the goal card, nudge copy, and CTA button in `prototype/index.html`. Verified in-browser — renders and functions correctly through the full flow.

---

## Round 2 — Tom

**In-character answers:**

1. *What do you think this does?* — Immediately read it as "another app telling me I spent too much," reacting defensively to "Dining spending jumped this week" as the lead.
2. *How would you arrive at this experience?* — Skeptical he'd open the notification at all — flagged that he connected the app because a friend pushed him to, then forgot it existed. Said he'd only see this screen if someone put it in front of him.
3. *Would you change your spending based on this?* — Credited the nudge for giving him one specific, low-effort action instead of a guilt trip, and said tapping it "did something" — more than his bank app ever has. But was clear that one notification wouldn't change behavior given he's abandoned three similar apps already; wanted to be asked again in a month.
4. *Magic wand?* — Don't lead with what he did wrong; soften or reorder the "bad news" so it doesn't land before the fix. Bigger ask: solve for getting him to open it again next week without having to remember it exists.

**Synthesis:**
- **Struggled with:** Entry tone read as judgment first, which is exactly what his profile says he doesn't want, even though the underlying action mechanic worked for him once he engaged.
- **Surprised me:** He completed the flow and reacted well to the action itself — the mechanic isn't what's failing him, only the entry emotion. A narrower, more fixable problem than "Tom won't engage."
- **Most worrying answer:** #2 — "I probably wouldn't have [arrived here]." That's not a copy critique, it's Tom saying a notification-driven loop may not work on him at all regardless of what the screen says, since he doesn't act on notifications from apps he's mentally checked out of (echoes NPS #5, "I just forget it exists").

**Highest-priority change:** Reframe the top-of-flow tone from deficit-first to context-first — lead with neutral/forward-looking framing instead of a spending callout, so the entry point doesn't read as a scolding before reaching the well-received action.

**Action taken (approved):** Rewrote the notification body ("Dining spending jumped this week — see what changed and one thing to try" → "This week's spending shifted a bit — here's one easy move to stay on pace for your Europe Trip") and the Top Insight headline (removed the "3× what you spent" comparison from the bold copy, replaced with a forward-looking bridge to the goal: "Dining & delivery came in at $186 this week — here's one easy way to stay on track for your Europe Trip"). The $62-vs-$186 comparison remains visible in the bar chart itself — the fix removes the verbal "you did 3x worse" framing, not the underlying data. Verified in-browser, no layout regressions.

---

## Round 3 — Amara

**In-character answers:**

1. *What do you think this does?* — Recognized it as a weekly digest she already does manually in a spreadsheet; approached it skeptically, ready to check its work rather than take it at face value.
2. *How would you arrive at this experience?* — No complaints about the notification-to-app mechanic, but immediately wanted to know if the $186 figure would match her bank app to the dollar — said a mismatch would end her use of the product entirely.
3. *Would you change your spending based on this?* — Rejected the specific nudge: she's carrying credit-card debt, and $25 of slack should go to the card (higher interest cost) before a savings goal. The nudge assumed savings was her top priority and picked wrong. Generalized from this single bad recommendation to distrust of the whole product ("what else does it not know about my situation?").
4. *Magic wand?* — Wanted to see the actual transaction list behind the $186 (merchant names, dates, amounts), not just a category total. Wanted the nudge logic to account for her actual priority (debt vs. goal) before recommending where money should go.

**Synthesis:**
- **Struggled with:** Two distinct trust problems — an unverifiable top-line number, and a nudge that confidently gave the wrong advice for her situation.
- **Surprised me:** She engaged with the concept exactly like her spreadsheet — checking its work rather than rejecting the format. The failure wasn't the format, it was that "personalized" wasn't actually personalized to her financial priorities, a sharper version of the "nudges feel generic" complaint already in NPS #4/#9.
- **Most worrying answer:** #3 — one wrong recommendation was enough for her to question the product's entire understanding of her situation. For a persona with an explicitly high trust bar, one bad nudge can be product-ending, not feature-ending.

**Decision:** Held rather than quick-patched — the fix (nudge logic reflecting actual financial priority) is a real engineering change, not a copy edit, so a shallow fix risked papering over the finding. Carried into the final stack-ranked list instead.

---

## Final Stack-Ranked List — Unaddressed Findings

| Rank | Finding | Usability Impact | Trust/Behavior Impact | Notes |
|---|---|---|---|---|
| 1 | Show transaction-level detail behind the top insight (tap to see actual charges — merchant, date, amount) | High — makes the number verifiable, not asserted | High — raised independently by **both** Priya and Amara, the only finding two personas converged on | Additive (a drill-down), not a logic change — likely best return for effort |
| 2 | Make the nudge reflect actual financial priority (don't default to "move to a goal" if the user is carrying debt) | Medium (surfaces only for debt-carrying users) | Highest severity — Amara: "if it doesn't know I have debt, what else does it not know" — a wrong recommendation, not a missing feature | Real engineering lift (nudge engine needs to know about competing priorities) — flagged for Raj |
| 3 | Tie the spending comparison to a concrete goal consequence (e.g., "pushes your trip back ~4 days") instead of a generic percentage | Medium — deepens the emotional connection to progress | Medium | Low effort relative to impact — mostly a copy/calculation formula |
| 4 | Solve for re-engagement beyond a single notification (Tom: "I'd need someone to put it in front of me... ask me again in a month") | N/A within this prototype's scope | High long-term — questions whether the entry mechanism works at all for a checked-out segment | Not a prototype fix — a broader notification/re-engagement strategy question |

**If only one gets built next:** #1 — the only finding two independent personas raised on their own, purely additive, and directly answers the sharpest quote in the whole exercise (Priya saying she'd verify manually even after completing the flow).

**Most urgent to flag to Raj regardless of build order:** #2 — not a missing nice-to-have, but the prototype actively giving wrong advice to an entire user segment.
