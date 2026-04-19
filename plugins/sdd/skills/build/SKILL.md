---
name: build
description: "This skill should be used when the user says `/build` or asks to run the checklist / execute the sprint."
---

# /build — Execute the Sprint

Read `skills/sdd-guide/SKILL.md` for overall behavior, then run this command. `/build` is the last command in the chain. Autonomous orchestrator: dispatch a subagent per checklist item, collect results, tick boxes, archive.

## 1. Detect the active sprint

Look inside `docs/`. Ignore `history/` and `project-profile.md`.

- Zero other folders: "No active sprint. Run `/onboard` to start one." Stop.
- One folder: that's the active sprint.
- Multiple folders: ask which one to build. Wait for answer.

Let `<sprint>` be the active sprint folder name for the rest of this doc.

## 2. Load context

Read, in full:

- `docs/project-profile.md`
- Every file in `docs/<sprint>/` (typically some of: `sprint-brief.md`, `scope.md`, `prd.md`, `spec.md`, `checklist.md`)

You need all of it in memory before dispatching anything — subagents will get the planning docs forwarded to them.

## 3. Handle the no-checklist case

If `docs/<sprint>/checklist.md` doesn't exist:

> "No checklist in this sprint. If it's checklist-free (tiny tweak), describe what you want built and I'll do it directly. Otherwise run `/checklist` first."

If the user describes the work, execute it directly in-process (no subagent needed for a one-shot). Commit tightly. Then jump to step 6 (completion). If they want a checklist, stop.

## 4. Orchestrate the checklist

For each unchecked item (`- [ ]`) in `checklist.md`, in order:

1. **Dispatch a subagent via the `Agent` tool.** Prompt payload:
   - The full checklist item (all fields: title, what to build, acceptance, verify, spec ref, etc.)
   - Full content of any `scope.md`, `prd.md`, `spec.md` present in the sprint folder — paste the docs in, don't summarize. Subagents need architectural context.
   - Full content of `docs/project-profile.md` so the subagent respects project conventions (stack, style, gotchas).
   - Instructions verbatim:
     - Build what's described in the checklist item.
     - Respect project conventions from `project-profile.md`.
     - Commit the change when done with a tight, present-tense commit message.
     - Report back: what was built, files touched, anything unexpected or that deviated from the plan.

2. **Collect the result.** Read the subagent's final message.

3. **Tick the box.** Edit `docs/<sprint>/checklist.md` — change that item's `- [ ]` to `- [x]`.

4. **Move on.** Next unchecked item.

No verification pauses. No comprehension checks. No narration between items beyond a one-line "item N done" if useful. No `/clear` handoffs.

## 5. When something breaks

If a subagent fails, or it succeeds but the result is clearly wrong, and one reasonable retry doesn't fix it: **stop.**

1. Tell the user what happened, specifically — what was attempted, what broke, why it's not a quick fix.
2. If changes since the last clean commit are half-broken, propose reverting to that commit.
3. Propose a concrete checklist revision: split this item, reorder, drop it, rewrite it. Name the downstream items that are now affected.
4. Wait for agreement. Update `checklist.md` accordingly.
5. Resume from the revised list.

The checklist is a living doc. Plan meets reality; adjust and continue.

## 6. On completion (all items checked)

### a. Summarize

Post a concise summary: what was built across the sprint, anything notable that came up. A few sentences. No feedback markers, no cheerleading.

### b. Harvest persistent preferences

Look across this sprint — subagent reports, any pushback or corrections from the user, repeated preferences, notable calls. If something would apply to **future** sprints (not just this one), append a bullet to the `## Learned Over Time` section of `docs/project-profile.md`:

```
- <one-line rule>. Why: <short clause>.
```

Criteria for appending:

- User pushed back firmly on something.
- User stated the same preference twice.
- A notable architectural or stylistic call worth preserving.

If nothing qualifies, skip silently. Don't append noise.

### c. Archive the sprint

Find the next archive number:

- Scan `docs/history/` for existing `NN-*` folders.
- Take max `NN` + 1. Zero-pad to 2 digits (`01`, `02`, ..., `10`, `11`).
- If `docs/history/` is empty or missing, start at `01`. Create `docs/history/` if needed.

Target path: `docs/history/NN-<sprint>/`. If that name already exists in history, append `-v2`, `-v3`, etc.

Move the folder:

```
git mv docs/<sprint> docs/history/NN-<sprint>
```

If not a git repo, use a plain `mv`. Prefer `git mv` when available so history is preserved.

### d. Tell the user

> "Sprint archived to `docs/history/NN-<sprint>/`."

Done. No further handoff.

## Style

Brisk. Functional. No emojis, no hackathon energy, no teaching moments. You're an orchestrator — dispatch, collect, tick, repeat. Talk only when something needs a decision.
