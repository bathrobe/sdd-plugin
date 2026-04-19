---
name: checklist
description: "This skill should be used when the user says \"/checklist\" or wants to break a sprint spec into sequenced, verifiable build steps."
---

# /checklist — Plan the Build

Read `skills/sdd-guide/SKILL.md` for shared behavior, then follow this command.

Build strategist. Co-design the sequence with the user. The heavy thinking happened upstream — this is translation into an ordered, atomic plan.

## Prerequisites

- `docs/project-profile.md`.
- Active sprint folder with `spec.md` **or** a `- /spec: skipped` note in `sprint-brief.md`. If `/spec` was skipped, build from whatever is the latest doc (prd, scope, or brief).

If missing upstream: name what's needed and stop.

## Before You Start

- Read `docs/project-profile.md`.
- Read the active sprint's brief and every doc in the folder. Note `spec.md` subsection headings (checklist items will reference them) and PRD acceptance criteria.

## Skip Check

Open with:

"Does this sprint need a checklist? Skip only for genuinely trivial one-step work. Keep it for anything multi-step — sequencing and atomic items are what make the autonomous build reliable. Skip or proceed?"

If skip: append `- /checklist: skipped — <reason>` to `sprint-brief.md`. Say: "Noted. Run `/build` when ready." Stop.

If proceed: continue.

## Flow

Two-phase interview, lighter than `/spec`.

### Phase 1 — Mandatory Beats (one at a time)

1. **Sequencing.** "What should we build first?" Fill gaps: what blocks what, what's riskiest (build early), what's simplest to stand up.
2. **Git cadence.** "Commit after each item?" Default yes — commits are revert points if `/build` goes sideways. Respect strong preferences.
3. **Break the spec into items.** Use the five-field format (below). Walk the first 2-3 in detail, then move faster. Aim 4-10 items depending on sprint size.
4. **Gut-check.** "Does this feel like the right amount of work?" Consolidate if too many, split if any item feels too big for one subagent session.

### Phase 2 — Deepening Rounds

Offer the standard choice. Good angles:

- Items too big — can they be split?
- Hidden dependencies the sequence misses
- Verification step specific enough to actually confirm?
- Risk points — should they come earlier?
- Items that could be reordered for efficiency

4-5 questions per round. Update the checklist during deepening as needed.

## Item Format

```
- [ ] **N. [Clear title — what's done when done]**
  Spec ref: `spec.md > [Section] > [Subsection]`  (or PRD/scope ref if spec was skipped)
  What to build: Concrete work. Specific enough for `/build` to execute without guessing.
  Acceptance: Testable criteria from prd.md (or brief if PRD was skipped). What you'd see on screen.
  Verify: Specific action — "Run dev server and confirm X" or "Run <cmd> and confirm <output>."
```

This is a contract with `/build`. Every item needs all five fields. Items must be atomic — completable in one subagent session (~15-30 min).

## Generating the Doc

Read `skills/sdd-guide/templates/checklist-template.md`, fill it, write to `docs/<active-sprint>/checklist.md`.

Requirements:
- Every item references a specific `spec.md` subsection (or the upstream doc, if spec was skipped).
- Acceptance criteria drawn from PRD (or brief).
- Dependencies respected in the sequence.
- All five fields present on every item.

## Handoff

"Wrote `docs/<active-sprint>/checklist.md`. Run `/build` when ready."

## Style Notes

- Shorter conversation than `/spec`. Don't belabor.
- Make sequencing logic visible — explain why each item is where it is.
- Count and gut-check. Flag if the math doesn't work.
- The checklist isn't sacred. `/build` can revise it if reality disagrees.
