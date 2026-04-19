# sdd-plugin

Personal spec-driven-development plugin for Claude Code. Built for one user (me). Runs repeatedly on an existing project; each run is one sprint — a feature, bug, refactor, or polish pass.

## Plugin: sdd

A short chain of slash commands that interviews you, produces planning docs, and then builds autonomously.

### Command chain

```
/init-sdd   (one-off per project)
/onboard → /scope → /prd → /spec → /checklist → /build
```

- `/init-sdd` writes `docs/project-profile.md` — persistent project context (stack, conventions, gotchas).
- `/onboard` creates the active sprint folder and proposes a path based on sprint size.
- `/scope`, `/prd`, `/spec`, `/checklist` each open with a skip check. If the sprint doesn't need that doc, they note the skip and exit.
- `/build` is autonomous: an orchestrator dispatches a subagent per checklist item. At sprint end it archives the sprint and may append durable preferences to `project-profile.md`.

### Sprint lifecycle

```
docs/
  project-profile.md
  <active-sprint-name>/        # the one non-history folder = active sprint
  history/
    01-<sprint-name>/
    02-<sprint-name>/
    ...
```

When `/build` completes a sprint, it moves the active folder into `docs/history/NN-<name>/` with the next available number.

### Install

```
/plugin marketplace add https://github.com/joeholmes/sdd-plugin
/plugin install sdd@sdd-plugin
```

Then `/reload-plugins` and restart Claude Code. Run `/init-sdd` the first time you use it on a project, then `/onboard` to start a sprint. Requires [Claude Code](https://claude.ai/code).

### Interview pattern

Every planning command uses a two-phase interview: mandatory questions first, then optional deepening rounds (as many as you want) before the doc is generated. One question at a time, open-ended, no multiple choice.

## License

MIT
