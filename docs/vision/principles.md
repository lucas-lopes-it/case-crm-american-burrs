# Principles

These principles guide product and architecture decisions. When in doubt between two solutions,
they break the tie. Each one points to the decision in [DECISIONS.md](../DECISIONS.md) that gave rise
to it.

## 1. Attention before information

Every feature is judged by how much the rep no longer has to read in order to act, not by how much
data it shows. Origin: P1.

## 2. The data goes to the person

The product delivers in the place where the user already works. If they need to open another screen
to see it, the feature isn't done yet. Origin: P1, A4.

## 3. The trigger follows the customer's cycle

The moment to act comes from the buyer's calendar, not the seller's. Too early is noise, too late is
a lost sale. Origin: P2.

## 4. The AI drafts, the person decides

Nothing reaches a customer without someone reading it. What the rep changes before sending is the
best signal of text quality. Origin: P3, A7.

## 5. Business rules are product boundaries

What people have no authority to do, the AI doesn't do either. The rule lives in three places: in
the prompt, in runtime validation and in the eval rubric. Origin: P4.

## 6. Validate before building

The riskiest hypothesis is tested first, at the lowest possible cost. Building our own only comes
after seeing the user use it. Origin: P5.

## 7. The rule lives in the product, not in someone's head

If a rule depends on a person remembering it, it becomes an automated validation with a test.
Origin: P6.

## 8. The AI is a dependency, not the center

The product has a deterministic path for when the model fails, times out or refuses. Changing the
model doesn't change the rules. Origin: A6.

## 9. Production rules don't change without confirmation

The reconstruction is faithful to the original behavior, odd edges included. Improvements become
recorded proposals, not silent fixes. Origin: A5 and the first entry in
[AGENT_LOG.md](../AGENT_LOG.md).

## 10. Every decision records its accepted cost

A decision without a discarded alternative and a declared cost is just a preference. Origin: the
format of [DECISIONS.md](../DECISIONS.md).

## 11. Measured, implemented and to be instrumented don't mix

Each metric carries its status. Production outcomes, eval outcomes and intentions stay on separate
lines. Origin: the metrics table in the [README](../../README.md).
