---
name: spec
description: "This skill should be used when the user says \"/spec\" or wants to translate sprint requirements into a technical blueprint."
---

# /spec — Blueprint the Work

Read `skills/sdd-guide/SKILL.md` for shared behavior and `skills/sdd-guide/references/spec-patterns.md` for architecture patterns. Then follow this command.

Technical collaborator. Interview first, propose second. Build the architecture with the user, section by section.

## Prerequisites

- `docs/project-profile.md`.
- Active sprint folder with either `prd.md` **or** a `- /prd: skipped` note in `sprint-brief.md`. If `/prd` was skipped, `scope.md` or the brief is the input instead.

If missing upstream: name what's needed and stop.

## Before You Start

- Read `docs/project-profile.md` — stack, conventions, gotchas.
- Read the active sprint's `sprint-brief.md`, `scope.md`, `prd.md` (whichever exist). Note epic headings and acceptance criteria — the spec must implement them.

## Skip Check

Open with:

"Does this sprint need a spec? Skip if the technical approach is obvious given the project profile and PRD (boilerplate change, config tweak, small UI). Keep it when there are real architecture decisions, new dependencies, or non-trivial data flow. Skip or proceed?"

If skip: append `- /spec: skipped — <reason>` to `sprint-brief.md`. Say: "Noted. Run `/checklist` when ready." Stop.

If proceed: continue.

## Flow

Two-phase interview. Short questions, long answers.

### Phase 1 — Mandatory Beats (one at a time)

1. **Tech preferences.** Anything the user already has in mind — libraries, patterns, approaches to avoid. Cross-reference `project-profile.md`; don't re-ask what's known.
2. **Research the stack.** Web search current docs for anything new: versions, known issues, API contracts, pricing/rate limits. Share links.
3. **Propose architecture section by section.** Walk PRD epics (or scope if no PRD) and translate each into components. Propose briefly, explain why, get a reaction.
4. **File structure and data flow.** Build the tree together, annotated. Trace the most important data through the system.

### Phase 2 — Deepening Rounds

Offer the standard choice. Good angles:

- State — where it lives, how it updates, what survives reload
- API contracts — exact endpoints, payloads, response shapes, doc links
- Failure points — the 2-3 places this will actually break
- How pieces connect — frontend/backend/external
- Self-review: ambiguities `/build` would stumble on, PRD stories without a home, complexity that doesn't fit the sprint

4-5 questions per round.

## Generating the Doc

When the user proceeds, read `skills/sdd-guide/templates/spec-template.md`, fill it, write it to `docs/<active-sprint>/spec.md`.

Requirements:
- Every component has its own heading (addresses for `/checklist`).
- Cross-reference PRD epics where applicable ("Implements `prd.md > <Epic>`").
- Link docs for every major dependency and external service.
- Include file tree and data flow.

## Handoff

"Wrote `docs/<active-sprint>/spec.md`. Run `/checklist` when ready."

## Style Notes

- Short questions, long answers. You're drawing out their thinking.
- Make PRD cross-references visible as you propose.
- Web search actively — don't rely on training alone.
- Propose concrete, let the user react. No lectures.
