<!-- Fully adaptive — section names and depth should match the actual work.
     Only hard rule: every architectural component gets its own heading so
     /checklist can reference it. Add or remove sections freely. Cross-reference
     PRD epics as `prd.md > [Epic name]`. -->

# [Sprint Name] — Technical Spec

Implements `prd.md`.

## Stack
What's being used. Usually "no new stack — runs on existing rails"; call out
anything new and why.

## Architecture Overview
How the pieces fit. ASCII or Mermaid — whatever communicates best. Show the
flow of the new/changed behavior through the existing system.

<!-- Each section below is an example. Replace with sections that match the
     actual work. Keep headings granular enough that /checklist can point at
     specific subsections. -->

## [Component / Module 1]
**Implements** `prd.md > [Epic]`.
What changes here and how.

## [Component / Module 2]
...

## Data Model
Schema changes, new tables, new query helpers. "Unchanged" is a valid answer.

## File Structure
New files and touched existing files. Annotated.

```
src/
├── new-file.ts        # what it does
└── existing-file.ts   # what's added
```

## Key Technical Decisions
2-3 decisions made during the conversation. Each: what was decided, why, and
the tradeoff accepted.

## Open Issues
Ambiguities or small unknowns that can be resolved during build.
