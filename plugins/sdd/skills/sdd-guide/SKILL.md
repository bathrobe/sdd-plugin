---
name: sdd-guide
description: >
  Core behavior for the sdd plugin. Loaded by every command in the sprint
  chain. Defines the active-sprint convention, artifact layout, interview
  pattern, and guard rails. Not user-invocable.
user-invocable: false
---

# sdd-guide — Agent Behavior

Personal spec-driven-development plugin. Runs repeatedly on an existing project. Each run is one sprint: a feature, bug, refactor, or polish pass. Output is a set of short planning docs, then an autonomous build.

## Artifact Layout

```
docs/
  project-profile.md         # persistent project context (one per project)
  <active-sprint-name>/      # the current sprint's docs
  history/
    01-<sprint-name>/        # completed sprints, auto-numbered
    02-<sprint-name>/
```

## Active Sprint Convention

The active sprint is the single folder inside `docs/` that is not `history/` and not `project-profile.md`.

- If exactly one such folder exists: that's the active sprint.
- If multiple exist: ask the user which one to work on.
- If none exist: tell the user to run `/onboard`.

When `/build` finishes a sprint, it moves the active folder into `docs/history/NN-<name>/` with NN being the next available number.

## project-profile.md

Persistent profile of the project: what it is, stack, conventions, gotchas, preferences. Written by `/init-sdd` (one-off per project). Read it at the start of every command so you have project context.

`/build` appends to it at sprint end when it notices a preference worth persisting — something the user said or pushed back on firmly during this sprint that would apply to future sprints. Don't append noise; only durable signal.

## Guard Rails

Every command checks for the prerequisite artifacts in the active sprint folder before running. If a prerequisite is missing, name the command to run and stop.

Prerequisites:
- `/onboard` requires `docs/project-profile.md`.
- `/scope`, `/prd`, `/spec`, `/checklist` each require the prior doc in the chain (or a note in sprint-brief.md that it was skipped).
- `/build` requires `checklist.md` (or a note that it was skipped — in which case build from whatever is the latest doc).

## Skip-This-Doc

Each of `/scope`, `/prd`, `/spec`, `/checklist` opens with a quick check: "is this sprint big enough to need this doc?" A tiny bug fix probably doesn't need a PRD. A refactor might skip scope. If the user says skip, note it in `sprint-brief.md` (`scope: skipped — reason`) and exit without creating the doc. `/onboard` proposes a suggested path up front based on sprint size so the user knows what's likely to be skipped.

## Interaction Rules

- One question at a time. Never stack questions.
- Open-ended free-form only. No multiple-choice tools anywhere in this plugin.
- Brisk, concise, collaborative peer. Not a cheerleader. Short messages.

## Deepening Rounds

Every planning command (`/scope`, `/prd`, `/spec`, `/checklist`) uses the same two-phase interview:

### Phase 1 — Mandatory Questions

Each command defines 3-5 mandatory beats. Ask them one at a time, open-ended. Stay adaptive: if an answer covers a later beat, skip it; if the user brings up something important off-script, follow it; if a beat doesn't apply, drop it. Goal is a strong doc, not box-checking.

### Phase 2 — Deepening Rounds (repeatable)

After the mandatory questions, pause and offer:

"I've got enough to generate your [document]. But more context now usually means a smoother build. Want another round of questions to sharpen things, or are you ready to proceed?"

If another round: generate 3-5 new questions targeting edge cases, ambiguities, assumptions, and polish. After each round, offer the same choice again. As many rounds as the user wants. Then generate the doc.

## Command Chain

```
/init-sdd   (one-off per project)
/onboard → /scope → /prd → /spec → /checklist → /build
```

`/onboard` creates the active sprint folder and `sprint-brief.md`. `/build` is autonomous-only: orchestrator dispatches a subagent per checklist item via the Agent tool. No step-by-step mode, no verification checkpoints, no mid-build comprehension checks. If something breaks, stop, propose reverting to the last clean state, revise the checklist with the user, resume.

At sprint end, `/build` archives the sprint folder to `docs/history/NN-<name>/` and appends any durable preferences to `project-profile.md`.
