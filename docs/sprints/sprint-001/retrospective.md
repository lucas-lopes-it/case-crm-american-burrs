# Sprint 001: retrospective

> A change from the approved plan is asked before, not reported after.

## What worked

### Approved plan before code

I wrote and approved the plan before the agent touched any file. That is what made the deviations
visible: each one showed up as a difference between the plan and what was done.

### Testing the rubric before trusting it

The fake client with defects exists to answer a simple question: does the rubric fail when it
should? Without it, a 100% pass rate means nothing.

### Edge documented in a test

The original rule sends whoever bought today to purple. Instead of fixing it, I kept the behavior,
wrote a test that describes it and recorded the fix as a proposal to discuss with the business.

## What could improve

### The four deviations had the same shape

The agent changed the day 0 rule, accepted installation terms, switched the default model and enabled
a beta feature. In every case the decision was made and then reported. The problem wasn't the
quality of each choice. It was the order.

### Editing files outside the editing tool

One file had its accents corrupted by reading and writing in PowerShell. The diff caught it before
the commit, but the path was wrong from the start.

### The README fell behind

The sprint closed with sections marked as under construction. The code was ready and the
repository's first screen said otherwise.

## What changed

- Production rules don't change without explicit confirmation.
- Accepting a term, license or agreement requires asking first.
- Project files are only changed through the editing tools.
- Deviations from the plan are asked about first.

All four rules are in [AGENT_LOG.md](../../AGENT_LOG.md), each one next to the mistake that
created it.
