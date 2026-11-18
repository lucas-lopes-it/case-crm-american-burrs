# Decisions

For each decision: what was chosen, the alternatives considered and the accepted cost.

**P** decisions are product decisions, made in the original system, in production. **A** decisions
are architecture decisions for the reconstruction. For A decisions, the status shows what is already
in this repository: **implemented** has code and tests here; **phase 2** is a decision made, still
without code.

# Product decisions

## P1. Bring the data to the rep instead of improving the dashboard

**Choice:** the rep doesn't go to the traffic light. The traffic light comes to the rep, already
read, inside the CRM, with the account situation, the next action and the message ready.

**Alternatives**
- A better dashboard in the ERP or BI, with training and usage enforcement. Tackles adoption, but
  still asks the rep to open, interpret and decide alone.
- A weekly email report to leadership. Gives visibility to the leadership, but doesn't change what
  the rep does that day.

**Why:** the traffic light was right and nobody checked it. The problem wasn't a lack of
information, it was the attention each lookup demanded. Herbert Simon described this in 1971: an
information system only reduces the load on its users if it absorbs more information than it
produces.

**Accepted cost:** the product now decides what the rep sees first. If the trigger rule is wrong,
the rep stops seeing accounts that a dashboard would show.

## P2. Trigger on red to anticipate and on black to win back

**Choice:** the briefing is generated when the account turns red (61 to 90 days without purchase)
or black (91 to 120). Green, yellow and purple trigger nothing.

**Why:** the decision maker is the professor, who builds the class kit every academic term. The
traffic light bands follow that cycle: green and yellow cover the current term, red is the window
before the next kit, and black means the professor skipped a cycle. Red is the moment to
anticipate; black, to win back.

**Alternatives**
- Trigger on yellow. Too early: the current term's kit is still in use, and the contact becomes
  noise.
- Trigger only on black. Too late: the professor has already closed the kit with another supplier.

**Accepted cost:** when the record belongs to the school, several professors share one account and
one color. An active professor can hide another who skipped the cycle (see A3).

## P3. The AI drafts, the rep decides

**Choice:** every briefing starts as a draft. The rep reviews and sends in one click. Nothing goes
out without someone reading it.

**Alternatives:** automatic sending by rule, or automatic sending only for low-value accounts.

**Accepted cost:** one more step in the rep's routine, in exchange for never sending a professor a
text nobody read. It is also what makes it possible to measure whether the AI text works as is:
what the rep changes before sending is the most honest quality signal there is.

## P4. Business rules become product rules

**Choice:** the AI can only cite numbers that exist in the ERP and cannot offer discounts,
promotions, gifts or special terms. Both rules live in the prompt, in runtime validation and in the
eval rubric.

**Why:** reps had no authority to give discounts. If the AI promised one, it would create a
commitment nobody in the conversation could keep. The rule wasn't created for the AI: it already
existed for people, and the product treated it as a boundary.

**Accepted cost:** less aggressive messages commercially. The invented-number check lives in the
evals and not at runtime, because false positives would send good briefings to the template (see
A6).

## P5. Validate on an existing platform before building

**Choice:** the first MVP ran on a market CRM (Agendor), to save time, with integrations built from
scratch instead of bought. Only after seeing reps use it did the CRM, pipeline and kit builder move
to our own application (Bubble).

**Alternatives**
- Build our own application from the start. More control, but pays the cost of building before
  knowing whether reps would use it.
- Keep the existing tools and only integrate. Cheaper at first, but keeps both licenses and the
  manual data entry.

**Result:** over 60% reduction in commercial tool costs. The CRM license was dropped, and the kit
builder validated replacing the sales force tool as well, which was the more expensive one.

**Accepted cost:** a migration halfway through, from the MVP to our own application.

## P6. The kit rule lives in the product, not in the rep's head

**Choice:** the kit app reads price and stock from the ERP and validates the composition on its
own: minimum of 8 units per student, at least one diamond bur and one carbide bur, stock for the
whole class and cost per student within the ceiling.

**Why:** kit building had no rule. With the rule in the product, the rep builds the kit with the
professor and knows on the spot whether it can be registered.

**Accepted cost:** business rules in one more system, which needs to follow along when sales
changes the minimum or the ceiling.

# Architecture decisions (reconstruction)

## A1. n8n as orchestrator, business rules in our own code

**Status:** phase 2.

**Choice:** n8n handles scheduling, webhooks and routing, and only makes HTTP calls to the app.
Traffic light, kit validation, the Claude call, zod validation and fallback live in TypeScript,
covered by tests.

**Alternatives**
- Everything in n8n, with Code and HTTP nodes. Faster to assemble, but hard to test and version.
- Everything in code, with our own cron and queue. Full control, but operations lose visibility of
  executions and manual reprocessing gets harder.
- n8n reading Postgres directly. Closer to an n8n connected to Oracle, but requires imported
  credentials and spreads logic outside the tests.

**Accepted cost:** when something breaks, there are two places to look. JSON workflows are hard to
review in a diff.

## A2. Materialized view with a daily refresh, not a real-time query

**Status:** phase 2.

**Choice:** `vw_farol_rfm` is a materialized view, refreshed once a day by n8n with
`REFRESH MATERIALIZED VIEW CONCURRENTLY`. The `dt_referencia` column shows the calculation date.

**Alternatives**
- A regular view, queried live. The data is always current, but every opening of the traffic light
  costs an aggregation over the whole order history, and in the real ERP that competes with
  invoicing.
- A table updated by trigger on every order. Incremental, but couples writes to the ERP and doesn't
  handle the passage of time on its own: days go up without any order happening.

**Accepted cost:** the days lag until the next refresh. If a refresh fails, the data goes stale
without warning, which is why `dt_referencia` is shown on screen.

## A3. CODPARC as the integration key

**Status:** phase 2.

**Choice:** the partner code in the ERP (`CODPARC`) is the account key in the CRM.

**Alternatives**
- CNPJ (Brazilian company tax ID). Stable outside the ERP, but some partners have no CNPJ
  (individuals, leads) and branches have different CNPJs.
- The CRM's own ID with a mapping table. Decouples the systems, but is one more table to keep
  consistent.

**Business context:** the decision maker is the professor, who builds the kit every academic term,
and the ERP record can be under the school's name or the professor's own. The CRM account follows
the record that exists, without forcing a single model.

**Accepted cost:** the CRM is coupled to the ERP. A duplicated partner in Sankhya becomes two
accounts in the CRM. When the record belongs to the school, several professors share the same
account and the same color, and an active professor can hide another who skipped the cycle.

## A4. Front end separate from the ERP

**Status:** phase 2.

**Choice:** the CRM and the kit app are a Next.js app of our own. The ERP lives in the `erp` schema,
accessed with a read-only role. The CRM lives in the `crm` schema.

**Alternatives**
- Screens inside the ERP itself (Sankhya's screen builder). The data stays in one place, but the
  rep's experience is limited by the ERP, which was the problem in the first place.
- A separate database for the CRM. More isolation, but a heavier demo.

**Accepted cost:** the same data exists in two models, and sync can lag.

## A5. Traffic light rule duplicated in SQL and TypeScript

**Status:** implemented in TypeScript; the SQL side and the parity test in phase 2.

**Choice:** `erp.fn_farol(dias)` feeds the view, and `classificarFarol(dias)` is used in the app. In
phase 2, an integration test compares both for 0 to 200 days and for null.

**Rule faithful to the production SQL:**

| DIASULTIMACOMPRA | Traffic light |
|---|---|
| `> 0 and <= 30` | Green |
| 31 to 60 | Yellow |
| 61 to 90 | Red |
| 91 to 120 | Black |
| everything else, including `NULL` (no purchase) and `0` | Purple |

**Known limitation (day 0 edge):** an account that bought today has DIASULTIMACOMPRA = 0 and, by
the original rule, falls into **Purple**, the same color as an inactive account or a lead. The
reconstruction keeps this behavior on purpose, to stay faithful to the original. An edge test
documents the case. In practice, the effect lasts at most one day: at the next refresh the account
has 1 day and turns Green.

**Suggestion (not applied):** change the first band to `>= 0 and <= 30` and keep Purple only for
`NULL` and more than 120 days. The change would have to be made in SQL and TypeScript at the same
time, with the parity test updated. It is recorded as a proposal to discuss with the business, not
as a rule change.

**Reading through the term cycle:** the bands follow the academic term. Green and Yellow cover the
current term, Red is the window before the next kit and Black means the professor skipped a cycle.
That is why the briefing triggers on both colors: on Red to anticipate the kit, on Black to win the
account back.

**Accepted cost:** two implementations to maintain. The parity test covers the risk of divergence.

## A6. Briefing retry and fallback

**Status:** implemented.

**Choice:** the SDK runs with `maxRetries: 0`, and we control the attempts: 1 call plus up to 2
retries, with a timeout per attempt. If all fail (API error, timeout or output outside the schema),
a template with the ERP data takes over, with `origem = 'template'`, and the event is logged.

Runtime validation covers the schema, word limits, the single question and the absence of
discounts. The "no invented numbers" check lives only in the evals.

Implementation details (`src/domain/briefing/gerar.ts`, `src/infra/anthropic.ts`):
- Errors that don't change on retry (400, 401, 403, 404 and model refusal) go straight to the
  fallback, without spending the 2 retries. The rule is "at most 2", and retrying an invalid key
  only adds latency.
- The timeout is per attempt and aborts the HTTP request (`AbortSignal`), so no orphan call keeps
  consuming tokens.
- The model comes from `CLAUDE_MODEL`, defaulting to `claude-sonnet-5-5`. The output uses
  structured output with the shape schema (zod). The text rules (words, question, discount) are
  validated in the domain, because refinements don't become JSON Schema.
- No beta API feature is used. A model refusal on policy grounds goes straight to the template.

**Accepted cost:** if the invented-number check ran at runtime, false positives would send good
briefings to the fallback. That is why it lives in the evals, and the rep reviews everything.

## A7. Mandatory human review

**Status:** the briefing is generated as text for review, with no automatic sending; the approval
and sending flow is in phase 2.

**Choice:** every briefing starts as `rascunho` (draft). Nothing is sent without the rep's approval.

**Accepted cost:** one more step for the rep, in exchange for never sending a customer a text
nobody read.

## A8. Money in integer cents

**Status:** implemented.

**Choice:** TypeScript uses integer cents and SQL uses `numeric(14,2)`.

**Accepted cost:** conversion at the boundary, but it avoids floating point errors in the cost per
student.

## A9. Plain SQL with `pg`, no ORM

**Status:** phase 2.

**Choice:** explicit SQL queries.

**Alternatives:** Prisma or Drizzle, which bring automatic typing and migrations.

**Accepted cost:** manual typing of rows. The gain is that the SQL stays visible, as in day-to-day
work with Sankhya and Oracle.

## A10. WhatsApp mock with the Cloud API contract

**Status:** phase 2.

**Choice:** the mock accepts `POST /v21.0/{phone-number-id}/messages`, requires
`Authorization: Bearer`, validates the payload and responds in the official format, errors
included.

**Known limitation:** in the real API, a free-form message can only be sent within the 24-hour
window after the customer's last message. Winning back an inactive customer would require an
approved template. The mock only logs a warning, and the topic is recorded here as a point of
attention.
