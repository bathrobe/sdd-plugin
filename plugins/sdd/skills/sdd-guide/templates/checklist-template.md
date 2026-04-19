<!-- Every item uses the four-field format below. /build is autonomous-only
     and reads each item; all four fields must be present. -->

# Build Checklist — [Sprint Name]

## Checklist

- [ ] **1. [Clear title — what's done when this step is complete]**
  Spec ref: `spec.md > [Section] > [Subsection]`
  What to build: Concrete description of the work. Specific enough that `/build` can execute without guessing.
  Acceptance: `prd.md > [Epic]` — what behavior this unlocks.

- [ ] **2. [Title]**
  Spec ref: `spec.md > [Section]`
  What to build: [...]
  Acceptance: `prd.md > [Epic]` — [...]

<!-- Continue for all items. Sequence respects dependencies — earlier items
     unblock later ones. Final item usually runs typecheck/tests and archives
     the sprint docs to docs/history/NN-<sprint>/. -->

## Out of scope

Brief list of items deferred from `prd.md > What We'd Add With More Time` that
are explicitly not built in this pass.
