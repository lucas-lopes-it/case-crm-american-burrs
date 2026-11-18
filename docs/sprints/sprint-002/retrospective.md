# Sprint 002: retrospective

> What isn't on `main` doesn't exist for visitors.

## What worked

### Separating product decisions from architecture decisions

The first version of the decisions file had ten decisions, all technical. Readers came away knowing
how the system was built and not knowing why it existed. Putting P1 to P6 first changed how the
whole repository reads.

### Status on every decision and every metric

Marking "implemented", "phase 2" and "to be instrumented" removed the ambiguity between what ran in
production, what is in this code and what is intention.

### The story separate from the README

The README answers quickly for whoever is evaluating. CASE.md tells the story for whoever wants to
read. A single document wouldn't do both well.

## What could improve

### The finished version sat outside `main` for five days

The content was complete on Nov 13 and only reached `main` on Nov 18. In between, the repository's
first screen still showed sections under construction.

### A branch was left behind

The branch `docs/narrativa-original-x-reconstrucao`, from Oct 22, has a commit that was never
merged. The Nov 13 rewrite covered the same ground another way, and the old branch is still open
with no recorded decision about it.

### Heavy images

The four images add up to about 2.4 MB. For a README, they can be reduced with no visible loss.

## What changes

- A documentation pull request is merged the same day it is ready.
- A branch that won't be merged is closed with one line explaining why.
- Every sprint ends with the README checked on `main`, the way a visitor sees it.
