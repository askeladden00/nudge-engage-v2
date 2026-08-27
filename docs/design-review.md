# Design Review — Weekly Summary Prototype (with Lena)

Produced from a simulated design-review negotiation: Claude played Lena (grounded in `stakeholders/lena.md`), a separate spawned agent played the PM, both grounded in `prototype/index.html`, `research/interview-synthesis.md`, and `docs/spec-readiness.md`. Not a real conversation with Lena — a rehearsal for one.

**Citation discipline:** every user-need claim below cites `research/interview-synthesis.md` — the real interviews — not the separate simulated persona playtest (`research/agentic-playtest.md`), which reuses the same three names for a different, simulated exercise.

## Part 1 — Prototype vs. Real User Needs

**Addressed well:**
- **"Give me something to act on."** Tom: *"I kept waiting for it to give me something to act on and it never really did."* Amara: *"I have been waiting for Nudge to tell me the next step."* → The nudge card is a direct, concrete action, not passive data.
- **"Don't just show me a static dashboard."** Tom: *"The app just showed me the same dashboard every time."* Amara: *"Nothing has changed since the first day."* → The weekly summary is designed to change week to week by definition.
- **"Ask something of me."** Tom: *"I switched to YNAB because at least that feels like it is asking something of me."* → The nudge's explicit request (move $25) does exactly this.

**Not yet addressed:**
- **The insight isn't the kind that created the real aha.** Priya's turning point was *"surfacing patterns I had not consciously registered — like that I always overspend in the last week of the month"* — a recurring pattern across time. The prototype's Top Insight is a two-point week-over-week delta, not pattern detection.
- **Amara's actual unresolved question isn't followed up on.** Her real stuck point was subscription spend: *"I do not really know what to do with that information."* The prototype uses a different, invented scenario (dining) rather than resolving her specific case.
- **The multi-month trust Priya described isn't demonstrated.** *"I feel like Nudge actually knows my financial habits now"* took her *"about three months"* — a single static screen can't prove it builds toward that.

## Part 2 — Design Review Findings (from the negotiation)

Three real gaps surfaced, none of which were visible before this review:

1. **Overclaimed "personalized" label.** The Top Insight is delta math (week 1 vs. this week), not pattern detection. Agreed fix: relabel honestly as "spending changed" for v1; treat true pattern-detection as an explicit v2 requirement once there's enough transaction history to support it.
2. **No evidence the mechanism generalizes beyond dining.** The prototype extrapolates from a dining-spike scenario to claim it would also resolve Amara's subscription-spend stuck point — that's an untested assumption. Agreed action: mock the subscription scenario specifically and test it against her actual complaint, rather than treating the extrapolation as proven.
3. **No defined behavior for a normal, unremarkable week — the likely majority case.** The prototype only has two templates: a spending spike, and (per `docs/spec-readiness.md`) a zero-transaction "quiet week." Nothing exists for "some spending, nothing notable" — probably the most common real state. Agreed action: add as a high-priority backlog item, needing both design input (what "nothing to say" looks like without feeling broken) and product input (what job the summary does in that state).

## Highest-Impact Single Change for Week-1 Retention

**Building the "unremarkable week" template.** Unlike the spike and zero-transaction scenarios (both edge cases by definition), this is the state most users will actually see most weeks. Leaving it undefined means the feature has no behavior for its own modal case — which directly undermines the "don't go static" need both Tom and Amara raised, since it's the scenario most likely to make the app feel static again regardless of how good the spike-case design is.

## Product Decision vs. Lena's Decision

- **Product (PM/Marcus) owns:** whether to invest in pattern-detection now vs. shipping "spending changed" honestly first; whether the subscription-scenario mock and the unremarkable-week template get prioritized this sprint; the eventual success metric.
- **Lena owns:** what "nothing to say" looks like without feeling broken (the unremarkable-week design); the copy/tone correction from "personalized" to an honest v1 label; the visual treatment of a real pattern-based insight once the engine supports one.

## Caveat

This entire exchange was two AI agents reasoning against the actual workspace docs — it surfaced real, citable gaps and produced honest, well-reasoned answers, but no actual sign-off from Lena happened. Treat the three findings and the two backlog items as a strong starting point for the real review, not as decisions already made.
