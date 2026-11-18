# Glossary

The domain terms as they appear in the documentation. Code identifiers are in Portuguese, because
the product serves a Brazilian sales team; the code term is shown in parentheses.

## Business

**Dental schools.** Universities and dentistry courses. The market served by the sales operation in
this case.

**Professor.** The decision maker. Builds the bur kit for the class every academic term.

**Academic term.** The interval between one kit and the next. It is what gives meaning to the
traffic light bands. In Brazil, many courses run quarterly terms (`trimestre`).

**Kit.** The set of burs each student in a class receives. It has composition rules: minimum units
per student, at least one diamond bur and one carbide bur, stock for the whole class and a cost
ceiling per student.

**Account** (`conta`). The customer in the CRM. It can be registered under the school's name or the
professor's own.

**CODPARC.** The partner code in the ERP. It is the key that links the CRM account to the ERP record.

**CNPJ.** The Brazilian company tax ID.

## Traffic light

**Traffic light** (`farol`). Each account's classification by color, based on days since the last
purchase.

| Color (code) | Days without purchase | Reading |
|---|---|---|
| Green (`VERDE`) | 1 to 30 | Current term in progress |
| Yellow (`AMARELO`) | 31 to 60 | Current term in progress |
| Red (`VERMELHO`) | 61 to 90 | Window before the next kit |
| Black (`PRETO`) | 91 to 120 | The professor skipped a cycle |
| Purple (`ROXO`) | no purchase, 0 or more than 120 | Inactive or lead |

**Anticipation.** The contact made when the account turns red, before the professor closes the next
kit.

**Win-back.** The contact made when the account turns black, after a skipped cycle.

**Day 0 edge.** Whoever bought today has zero days without purchase and falls into purple under the
original rule. The reconstruction keeps the behavior and documents the case in a test.

## Briefing

**Briefing.** What the AI delivers to the rep when the account triggers: account situation, next
action, WhatsApp message and email. The text itself is in Portuguese.

**Draft** (`rascunho`). The state every briefing starts in. It only becomes a sent message after
the rep's review.

**Template.** The deterministic briefing, built only from the account data, that takes over when the
AI fails.

**Fallback.** The switch from the AI to the template, after the attempts run out or on an error that
doesn't change on retry.

**Guardrail.** A rule the text cannot break: only numbers that exist in the input and no promise of
discount, promotion, gift or special terms.

## Evaluation

**Evals.** Running the briefing over 20 fictional accounts, with an automated score per criterion.

**Rubric** (`rubrica`). The set of eval criteria: format, numbers present in the input, mention of
days without purchase and last order, word limits, a single question in WhatsApp and no discounts.

**Good mock and bad mock** (`--mock`, `--mock=ruim`). Two fake AI clients. The first follows every
rule and should pass everything. The second has deliberate defects, to prove that the rubric fails
them.

**History** (`historico.csv`). The record of each eval run, with prompt version and hash, to compare
versions.

## Reconstruction

**Reconstruction.** This repository: the product logic rebuilt in code, with fictional data.

**Phase 2.** What is decided and has no code here yet: ERP simulated in Postgres, orchestration in
n8n, CRM and kit app, WhatsApp mock.

**P and A decisions.** P is a product decision, made in the original system. A is an architecture
decision for the reconstruction.
