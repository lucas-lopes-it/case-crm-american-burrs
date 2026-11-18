# Sprint 002: review

> The code showed how the product works. What was missing was why it exists.

## Goal

Rewrite the documentation through a product lens: outcome first, then user, problem, hypothesis,
decisions, what was left out and how it is measured.

## Stories shipped

### 1. README as a case

- Opens with the outcome: over 60% reduction in commercial tool costs.
- User table (rep, professor, sales leadership) with what each one needs from the product.
- Riskiest hypothesis and how it was validated before building.
- Product evolution table: discovery, MVP, own product and reconstruction.
- "What was left out, on purpose" section.
- Metrics with status: measured in production, implemented, measured in evals or to be instrumented.

### 2. Product decisions before architecture decisions

- Six product decisions (P1 to P6), made in the original system.
- The ten architecture decisions renumbered A1 to A10, each with a status: implemented or phase 2.
- References in the code updated to the new numbering.

### 3. The story in first person

- [CASE.md](../../CASE.md): the traffic light nobody checked, with Herbert Simon's reading of
  attention as the backbone of the argument.

### 4. PRD

- [PRD.md](../../PRD.md): problem, users, goals, out of scope, twelve requirements, metrics, phases,
  risks and open questions.

### 5. Clickable demo

- `docs/demo/funil.html`: architecture, 5-stage pipeline, kit validation and traffic light with
  briefing, in a single file with fictional data.
- Four product images in the README.

## Numbers

- 5 new or rewritten documents and 1 clickable demo.
- All 72 tests still pass. The only code change was the decision numbering in comments.
- Pull request 1 merged into `main` on Nov 18, 2026.

## Left for later

- Vision, principles and glossary as standalone documents.
- Sprint records.
- License, contributing guide and continuous integration.
