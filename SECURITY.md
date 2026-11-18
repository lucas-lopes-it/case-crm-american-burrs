# Security Policy

## What this repository contains

A reconstruction with fictional data. There is no code, data, credential or customer information
from the original production environment. Customers, products, orders, phone numbers and emails
were generated for the demo.

## Secrets

- The only key used is `ANTHROPIC_API_KEY`, read from a local `.env` file that is not committed.
- The tests and the evals in mock mode run without any key.
- Never include keys, tokens, internal documents or personal data in issues, pull requests or
  fixtures.

## How to report a vulnerability

Use GitHub's private reporting: the **Security** tab, **Report a vulnerability**. Don't open a
public issue for this kind of matter.

If you find anything in this repository that looks like real data, report it the same way. That is
the most serious kind of failure this project can have.

## Versions

Only `main` receives fixes.
