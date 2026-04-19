---
name: onboard
description: "Run at the start of every new sprint. Interviews the user about what they're working on, names the sprint, proposes a doc path, and writes sprint-brief.md."
---

# /onboard — Start a New Sprint

Read `skills/sdd-guide/SKILL.md` for shared behavior, then follow this command.

Per-sprint entry point. A sprint is one feature, bug, refactor, polish pass, spike, prompt tweak — anything with a clear start and end. Run this at the beginning of each one.

## Prerequisites

`docs/project-profile.md` must exist. If missing: "Run `/init-sdd` first — I need the project profile before starting a sprint." Then stop.

## Before You Start

- Read `docs/project-profile.md` in full.
- List `docs/history/` and read just the folder names so you have a sense of recent sprints. Don't open their contents unless the user references one.
- Check `docs/` for an existing active sprint — any folder that isn't `history/` and isn't the profile file.

## Resume Check

If an active sprint folder already exists: "Looks like there's an in-progress sprint at `docs/<name>/`. Resume it or start a new one?"

- Resume: stop and point them at the right next command based on what's already in the folder (`sprint-brief.md` → `/scope`, `scope.md` → `/prd`, etc.).
- New one: confirm you can archive or discard the existing folder, then proceed.

If no active sprint folder: proceed.

## Phase 1 — Mandatory Interview

One question at a time, open-ended. Adapt freely — if an answer covers a later beat, skip it.

1. **What's this sprint?** Feature, bug, refactor, polish, spike, prompt tuning, something else?
2. **Why now?** What triggered it — a bug report, a new idea, something you noticed while using the thing?
3. **Size sense.** One-sitting job or multi-day? Rough gut read is fine.
4. **Anything already decided?** Constraints, fixed choices, libraries you know you're using, approaches you've ruled out.
5. **What does done look like?** How will you know it's shipped?

## Phase 2 — Deepening Rounds

See `sdd-guide/SKILL.md > Deepening Rounds`. Offer:

"I've got enough to name this sprint and propose a doc path. Want another round of sharper questions, or ready to proceed?"

Good deepening questions here: ambiguities in the "done" definition, assumptions buried in the trigger, scope creep risks, dependencies on other code, anything the user seemed unsure about.

## Name the Sprint

Propose a short kebab-case name. Confirm with the user. Adjust if they push back.

## Propose a Doc Path

Based on size and nature, propose which planning docs this sprint needs. Menu:

- `/scope` — brainstorm, shape the idea
- `/prd` — user-facing behavior, requirements
- `/spec` — technical approach
- `/checklist` — build steps

Rough heuristics:

- Tiny prompt tweak or one-line bug: maybe just `/checklist`, or skip straight to building.
- Small bug fix: `/spec` + `/checklist`.
- Normal feature: all four.
- Refactor: `/spec` + `/checklist`, sometimes `/scope` if exploratory.
- Spike: `/scope` alone might be enough.

Present your proposal as a list. Let the user adjust. Remind them each command has its own skip check, so this isn't binding.

## Write `sprint-brief.md`

Create `docs/<sprint-name>/` and write `sprint-brief.md` with:

- Sprint name
- One-line description
- Sprint type (feature / bug / refactor / polish / spike / other)
- Size read
- Proposed doc path (which commands will run)
- Trigger / why now
- Constraints or fixed choices surfaced in the interview
- Definition of done

Keep it short. This is a header for the sprint, not a plan.

## Handoff

"Brief written at `docs/<sprint-name>/sprint-brief.md`. Proposed path: [list]. Run `/<first-command>` when ready."

Replace `<first-command>` with whatever the user chose to start with — usually `/scope`, sometimes `/spec` or `/checklist`.
