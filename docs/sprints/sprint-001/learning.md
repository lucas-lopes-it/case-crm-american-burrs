# Sprint 001: learning

## Fidelity comes before improvement

### What happened

The production traffic light rule classifies as green anyone between 1 and 30 days without
purchase. Whoever bought today has 0 days and, under the rule, falls into purple, the same color as
an inactive customer. It looks like a bug. The coding agent treated it as a bug and fixed it.

I reverted it.

### Why this matters for product people

A rule in production is an agreement the operation has already absorbed. Someone may depend on the
odd behavior without knowing it. When the reconstruction fixes it on its own, it stops describing the
product that existed and starts describing the product someone thought should exist.

The same goes for the AI. The no-discount rule wasn't created for the model. It already applied to
the rep. The product work was recognizing the rule and putting it in three places: in the prompt, in
validation and in the rubric.

### How to apply it

Before changing an inherited rule:

1. Write a test that describes the current behavior, odd part included.
2. Record the change as a proposal, with the practical effect and who needs to agree.
3. Only change it after confirmation from whoever owns the rule.

Before trusting an automated evaluation:

1. Run it against an output you know is wrong.
2. Check that each criterion fails the defect it should fail.
3. Only then read the result of the real output.

### Exercise

Run both commands and compare the reports generated in `evals/runs/`:

```bash
npm run eval -- --mock
npm run eval -- --mock=ruim
```

Then answer: which rubric criterion would you remove without losing protection, and which defect of
the bad client does no criterion catch?
