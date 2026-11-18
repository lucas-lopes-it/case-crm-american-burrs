# Vision

## Mission

Give attention back to the sales rep. The product reads the portfolio for them and delivers, on the
right day of the customer's cycle, the account already interpreted, the next action and the message
ready to review.

## The problem

Most sales tools hand more information to people who already lack the time to read what exists. At
American Burrs the ERP classified every customer by color, based on days since the last purchase.
The traffic light was right and nobody checked it.

The usual answers to this don't solve it:

- a better dashboard: still asks the rep to open, interpret and decide alone;
- training and usage enforcement: treats an attention problem as an adoption problem;
- a report for leadership: gives visibility to leadership and doesn't change the rep's day;
- a sales chatbot: requires the rep to go to the AI and know what to ask.

## The vision

Sales operations where the system absorbs more information than it produces. The rep doesn't check
dashboards, doesn't fill in the CRM and doesn't build kits in a spreadsheet. They receive the work
already read and decide.

For that, the product needs to:

- understand the customer's buying cycle, not just the order history;
- reach the rep in the place where they already work;
- treat business rules as the boundary of what the AI can write;
- keep a person between the AI and the customer;
- keep working when the AI fails.

## What this repository is

The public reconstruction of this product's logic, with fictional data. The rules that lived in a
low-code application in production are tested code here, and the AI text is scored by an automated
rubric for every prompt version.

It serves two readers:

- whoever is evaluating my product work and wants to see problem, decision, accepted cost and
  outcome;
- whoever builds AI for operations and wants a small example of business rules, fallback and
  evals.

## What this repository is not

- It is not the production system. There is no real code, data, credential or customer here.
- It is not a ready-to-install CRM. Phase 2 (database, orchestration, app and channels) is decided
  and has no code yet.
- It is not a framework. It is a case with its rules exposed.

## Where it is going

The path is in [roadmap.md](../product/roadmap.md). The direction is always the same: every new
capability has to reduce what the rep reads before acting, and has to arrive with a way to measure
whether it did.
