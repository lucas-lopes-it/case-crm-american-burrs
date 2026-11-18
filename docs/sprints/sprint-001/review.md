# Sprint 001: review

> The production rule is the requirement. The reconstruction starts there.

## Goal

Take the product rules out of a low-code application and put them into tested code, with fictional
data, so anyone can run and verify them.

## Stories shipped

### 1. Reconstruction structure

- TypeScript project with Vitest, with no database or API key needed to run the tests.
- Separation between domain (`src/domain`), infrastructure (`src/infra`) and evaluation
  (`src/eval`).
- Notice at the top of the README: no code, data, credential or customer from the real environment.

### 2. Traffic light rule

- `classificarFarol(dias)` with the five bands, faithful to the production SQL.
- Edge tests for each band limit, for null and for day 0.
- The day 0 edge (whoever bought today falls into purple) was kept and documented in decision A5.

### 3. Kit validation

- Validation per class: minimum of 8 units per student, at least one diamond bur and one carbide
  bur, stock for the whole class and cost per student within the ceiling.
- Money in integer cents (decision A8).

### 4. Briefing generation

- Structured output with a shape schema, and text rules validated in the domain: word limits, a
  single question in WhatsApp and no discounts.
- One call plus up to two retries, with a per-attempt timeout.
- Errors that don't change on retry go straight to the template.
- Deterministic template with the account data, and an event logged on every fallback (decision A6).

### 5. Briefing evals

- 20 fictional accounts in `evals/fixtures/contas.json`.
- Automated rubric with six criteria.
- Two fake clients: one that follows the rules and one with defects, to prove the rubric fails them.
- History per run, with prompt version and hash, and comparison between the last two runs.

## Numbers

- 72 tests in 5 files, all passing.
- Evals with the good mock: 100% pass rate. With the bad mock: the rubric fails half.
- 4 coding agent deviations recorded in [AGENT_LOG.md](../../AGENT_LOG.md).

## Left for later

- Database, orchestration, app and delivery channels (phase 2).
- The architecture and demo script sections of the README, still marked as under construction at
  the end of the sprint.
