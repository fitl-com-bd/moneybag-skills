---
name: moneybag-subscriptions
description: Implement, review, or debug Moneybag recurring-payment integrations using subscription plans, ad-hoc subscriptions, hosted checkout, billing history, pause/resume/cancel lifecycle operations, and webhooks. Use for server-side code generation, integration architecture, lifecycle handling, security review, or troubleshooting against Moneybag Public OpenAPI 2.0.0.
---

# Moneybag Subscriptions

Build subscription integrations from the reviewed public contract. Treat the
bundled references as authoritative; do not invent fields, states,
retry schedules, or webhook guarantees.
Use [references/moneybag-public.json](references/moneybag-public.json) for exact
request fields, response schemas, bounds, and enums. It installs with this skill.

## Workflow

1. Read [references/contract.md](references/contract.md) for endpoints and
   identifiers.
2. Read [references/lifecycle.md](references/lifecycle.md) before implementing
   state transitions or billing behavior.
3. Read [references/security.md](references/security.md) before generating or
   reviewing code.
4. Choose a reusable plan or validate every required ad-hoc billing field.
5. Create the subscription from a trusted server.
6. For prepaid subscriptions, create hosted checkout and verify the resulting
   transaction before activating service.
7. Reconcile API reads and signed webhooks idempotently.
8. Validate the implementation with the checklist below.

## Non-negotiable rules

- Send `X-Merchant-API-Key` only from trusted server code.
- Never place keys in browser/mobile code, URLs, logs, analytics, screenshots,
  source control, or AI prompts.
- Scope every stored subscription to the authenticated merchant and retain the
  returned subscription UUID.
- Do not treat a customer redirect as payment proof; verify server-side.
- Make webhook and order updates idempotent.
- Require explicit operator confirmation before manual invoice generation,
  cancellation, archival, or restoration.
- Do not call production when validating examples; use the sandbox server.

## Validation checklist

- Contract paths, methods, fields, and enums match the bundled contract
  reference.
- Prepaid and postpaid initial states are handled separately.
- Trial, past-due, pause, resume, immediate-cancel, and period-end-cancel states
  have explicit behavior.
- Cross-merchant identifiers cannot be read or mutated.
- Duplicate redirect, verification, and webhook delivery cannot double-fulfill
  or double-activate service.
- Manual invoice generation is not blindly retried.
- Errors are correlated and sanitized without recording credentials or customer
  payment data.

State uncertainty explicitly and cite the contract or lifecycle reference used.
