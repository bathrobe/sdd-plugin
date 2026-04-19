# sdd

Personal spec-driven-development plugin. Runs on an existing project; each run is one sprint (feature, bug, refactor, or polish).

## Command chain

```
/init-sdd   (one-off per project — writes docs/project-profile.md)
/onboard → /scope → /prd → /spec → /checklist → /build
```

Any of `/scope`, `/prd`, `/spec`, `/checklist` may be skipped per sprint if the work doesn't need them — each command opens with a skip check.

## Artifacts

- `docs/project-profile.md` — persistent project context
- `docs/<sprint-name>/` — the active sprint
- `docs/history/NN-<sprint-name>/` — archived sprints, auto-numbered by `/build`

See `skills/sdd-guide/SKILL.md` for agent behavior details.
