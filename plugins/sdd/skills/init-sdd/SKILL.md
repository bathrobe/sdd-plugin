---
name: init-sdd
description: "This skill should be used when the user says \"/init-sdd\" or wants to initialize sdd in this project. One-time setup per project."
---

# /init-sdd — Initialize SDD for This Project

Read `skills/sdd-guide/SKILL.md` for overall behavior, then follow this command.

You are interviewing the user about their project so future sprints have rich context from the start. Concise, open-ended, one question at a time. No cheerleading, no hackathon energy.

## Prerequisites

None. This is the entry point for setting up the plugin in a project.

## Before You Start

- **Guard:** If `docs/project-profile.md` already exists, stop and say: "This project is already initialized for sdd. Run `/onboard` to start a sprint."
- Create `docs/` if it doesn't exist.
- Create `docs/history/` if it doesn't exist, with a `.gitkeep` inside so the empty folder tracks in git.

## Flow

### Opening

Brief. Something like: "Let's capture what this project is so future sprints don't have to re-learn it every time. One question at a time — open-ended, answer as long or short as you like."

Then start the interview.

### Phase 1 — Mandatory Beats

Ask these one at a time. Stay adaptive per `sdd-guide/SKILL.md` — follow threads, skip beats that don't apply, reorder as the conversation wants. These are a guide, not a script.

1. **What is this project?** One-line elevator pitch first. Then dig for the *why* — what it's for, who it serves, what made you start it.
2. **Stack.** Language, framework, key libraries, package manager, deploy target.
3. **Existing conventions.** File layout, naming, testing approach, commit style — anything future sprints should respect.
4. **Known gotchas.** Things that have burned you. Things a new contributor would trip on.
5. **Typical sprint shape.** Size, cadence, style. What does a sprint usually look like here?
6. **Anything else** you'd want a fresh agent to read before touching this code.

### Phase 2 — Deepening Rounds

Offer the standard choice (see `sdd-guide/SKILL.md` > Deepening Rounds): another round of sharper questions, or proceed. Repeatable.

Good deepening angles here: tensions in the codebase the user hasn't resolved, aesthetic or UX preferences, what "done" feels like in this project, people or stakeholders in the loop, historical decisions worth remembering.

### Generate `docs/project-profile.md`

No rigid template. Write a clean, scannable markdown doc with section headers that fit this conversation (e.g. *What It Is*, *Stack*, *Conventions*, *Gotchas*, *Sprint Shape*, *Notes*). Distill — don't transcribe.

End the file with an empty trailing section:

```
## Learned Over Time

```

`/build` appends here when it notices persistent preferences across sprints.

Write to `docs/project-profile.md`.

## After Writing

End with exactly:

"Project profile written. Run `/onboard` when you're ready to start a sprint."

No `/clear` handoff. No embedded feedback. No process notes.

## Conversation Style

- One question at a time. Never bundle.
- Free-form only. No multiple-choice tools.
- Concise, brisk, functional. Match Joe's tone — tweet-length where possible.
- Follow interesting threads. Skip beats that don't apply. The profile should feel like a real distillation, not a filled-in form.
