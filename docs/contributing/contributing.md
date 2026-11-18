# How to contribute

Contributions from product, sales operations and technology people are welcome. You don't need to
write code. An edge case the rule doesn't cover, a new fictional account for the evals or a fix in
the documentation also improve the project.

## Setup

1. Fork the repository and create a small branch.
2. Install Node 22 or later.
3. Run `npm install`.
4. Run `npm test` and `npm run typecheck` before and after your change.
5. If you touch the briefing, run `npm run eval -- --mock` and `npm run eval -- --mock=ruim`.

No API key is needed for these commands.

## Good contributions

- Explain which problem of the rep, the professor or sales leadership is being solved.
- Are small and come with tests.
- Keep business rules in `src/domain`, with no infrastructure dependencies.
- Respect the [principles](../vision/principles.md), especially number 9: production rules don't
  change without confirmation. A rule change proposal comes in as an issue before it becomes code.
- Record relevant decisions in [DECISIONS.md](../DECISIONS.md), with alternatives and accepted cost.
- Use fictional data only.

## Pull request

Describe the problem, the solution, how to test it and what changes for the rep. By taking part,
you agree to the [Code of Conduct](../../CODE_OF_CONDUCT.md).
