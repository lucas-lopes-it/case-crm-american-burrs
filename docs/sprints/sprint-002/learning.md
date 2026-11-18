# Sprint 002: learning

## The repository is a product too, and the first screen is the README

### What happened

At the end of sprint 001 the repository had tested rules, fallback and evals. The first screen said
"architecture: under construction". Whoever opened the link read the notice and left before reaching
the code.

Sprint 002 didn't change a single line of behavior. It changed what a visitor understands in the
first thirty seconds.

### Why this matters for product people

A technical case is usually written in the order it was built: structure, rule, integration,
outcome. Evaluators read it in the opposite order: they want to know first what changed for the
business, then for whom, then why this solution and not another, and only then how it was done.

Three moves made the difference:

1. **Outcome before architecture.** The number measured in production opens the README.
2. **Decision with cost.** Each choice carries the discarded alternative and what was lost by
   choosing.
3. **Honest status.** What was measured, what is implemented and what is still to be instrumented
   appear separately.

The third one builds the most trust. A reader who finds "to be instrumented" next to a metric
believes the ones marked as measured a lot more.

### How to apply it

For any project you want to show:

1. Write the outcome in one line, with a number and a unit.
2. List the people who use it and what each one needs, without tool names.
3. State the riskiest hypothesis and how it was tested before building.
4. For each decision, write the alternative you discarded and the cost you accepted.
5. Write what was left out on purpose.
6. Mark each metric as measured, implemented or to be instrumented.

### Exercise

Open the README of a project of yours and read only the first thirty seconds. Answer without
scrolling: what problem does it solve, for whom, and what was the outcome? Whatever is missing from
the answer is what is missing from the top of the document.
