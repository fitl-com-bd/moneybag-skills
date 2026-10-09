# Security and integration review

- Keep `X-Merchant-API-Key` in server-side secret storage.
- Use sandbox during development and automated tests.
- Reject or ignore merchant/resource combinations outside the authenticated
  tenant even if an identifier is syntactically valid.
- Validate Moneybag webhook signatures using the current verified webhook
  contract before processing payloads.
- Store event identity and transaction identity under unique constraints for
  idempotency.
- Verify payment state server-side before granting prepaid service.
- Redact keys, tokens, customer PII, webhook secrets, and full payment payloads
  from prompts, logs, traces, and analytics.
- Treat manual invoice generation as a customer-visible side effect. Require
  explicit confirmation and a stable operator idempotency boundary.
- Do not claim fixed retry schedules, delivery guarantees, or production
  approval unless a separately approved policy defines them.
