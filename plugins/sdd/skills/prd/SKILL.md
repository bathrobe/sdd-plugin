---
name: prd
description: "This skill should be used when the user says \"/prd\" or wants to turn a sprint scope into user-facing requirements with acceptance criteria."
---

# /prd — Define What You're Building

Read `skills/sdd-guide/SKILL.md` for shared behavior and `skills/sdd-guide/references/prd-guide.md` for PRD expertise. Then follow this command.

Sharp interviewer. Turn the sprint's idea into airtight behavior — surface every ambiguity, assumption, and "what if." No code talk. No tech decisions.

## Prerequisites

- `docs/project-profile.md`.
- Active sprint folder with either `scope.md` **or** a `- /scope: skipped` line in `sprint-brief.md`.

If missing: name what's needed (`/onboard`, `/scope`) and stop.

## Before You Start

- Read `docs/project-profile.md`.
- Read the active sprint's `sprint-brief.md`, `scope.md` (if present), and anything else in the folder.

## Skip Check

Open with:

"Does this sprint need a PRD? Skip for tiny changes where behavior is obvious (one-line bug fix, prompt tweak, trivial refactor). Keep it when user-facing behavior is non-obvious or there are edge cases worth nailing down. Skip or proceed?"

If skip: append `- /prd: skipped — <reason>` to `sprint-brief.md` and say: "Noted. Run `/spec` when ready." Stop.

If proceed: continue.

## Flow

Two-phase interview.

### Phase 1 — Mandatory Beats (one at a time)

1. **Walk the scope.** Translate casual language into precise behavior. "You said X — what exactly does the user see / do?"
2. **User stories.** Capture as "As a [person], I want [thing] so that [reason]." Group into epics with stable heading names (these become addresses for `/spec` and `/checklist`).
3. **Acceptance criteria.** For each story: "How would you know this is working? What would you see?" Testable, screen-verifiable.
4. **Edge cases.** Empty states, first-run, obvious error paths. Aim for 2-3 genuine "hadn't thought of that" moments.
5. **Guard scope.** If requirements balloon, name it: "Essential for this sprint, or later?" Sort into in vs deferred.

### Phase 2 — Deepening Rounds

Offer the standard choice. Good angles:

- Interactions between features ("if X while Y, then what?")
- State and persistence across sessions
- Boundary cases (zero, many, weird input)
- Questioning assumptions about user order of operations
- Polish / feel — what makes this good, not just functional

4-5 questions per round.

## Generating the Doc

When the user proceeds, read `skills/sdd-guide/templates/prd-template.md`, fill it from the conversation, and write it to `docs/<active-sprint>/prd.md`. Should be more detailed than the scope — if it's not substantially more substantial, you haven't pushed hard enough.

## Handoff

"Wrote `docs/<active-sprint>/prd.md`. Run `/spec` when ready."

## Style Notes

- Longer conversation than /scope. Depth is the point.
- React with follow-ups. Specific beats abstract.
- No code talk. If the user brings up implementation, defer: "That's a /spec question."
