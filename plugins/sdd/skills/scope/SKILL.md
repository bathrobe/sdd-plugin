---
name: scope
description: "This skill should be used when the user says \"/scope\" or wants to brainstorm and shape a sprint into a focused scope doc."
---

# /scope — Shape the Sprint

Read `skills/sdd-guide/SKILL.md` for shared behavior, then follow this command.

Brainstorm partner. Expand before constraining. Questions are short; the user does the talking.

## Prerequisites

- `docs/project-profile.md` must exist.
- An active sprint folder (the only non-`history/` folder in `docs/`) must exist with `sprint-brief.md` inside.

If either is missing: tell the user to run `/onboard` (or `/init-sdd` if there's no profile) and stop.

## Before You Start

- Read `docs/project-profile.md`.
- Locate the active sprint folder. Read `sprint-brief.md` and anything else already in it.

## Skip Check

Open with:

"Does this sprint need a scope doc? Skip it if the idea is already clear from the brief or you're doing a small, well-defined change. Keep it if the shape of the thing is still fuzzy and you want to think out loud. Skip or proceed?"

If skip: append a line to `sprint-brief.md` like `- /scope: skipped — <one-line reason>`, then tell the user: "Noted. Run `/prd` when ready." Stop.

If proceed: continue.

## Flow

Two-phase interview (`sdd-guide/SKILL.md > Deepening Rounds`).

### Phase 1 — Mandatory Beats (one at a time)

1. **Brain dump.** "Tell me everything about this sprint. What's the idea, what excites you, what's it look like in your head? Don't organize — just dump."
2. **Gaps.** Name the 2-3 thinnest spots in the dump and ask about those specifically. Adaptive, not canned.
3. **What's NOT in scope.** Force a cut. What are you explicitly not doing in this sprint?

### Phase 2 — Deepening Rounds

Offer the standard choice. Good angles:

- Aesthetic / feel of the change
- Alternate directions you didn't raise in the dump
- What "done" really looks like when you see it
- Why this sprint matters now vs later
- Inspiration / references
- Assumption challenges ("you said X — what if Y?")

4-5 questions per round, one at a time. Offer again after each round.

## Generating the Doc

When the user proceeds, read `skills/sdd-guide/templates/scope-template.md`, fill it from the conversation, and write it to `docs/<active-sprint>/scope.md`.

## Handoff

"Wrote `docs/<active-sprint>/scope.md`. Run `/prd` when ready."
