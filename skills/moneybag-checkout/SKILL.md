---
name: moneybag-checkout
description: Implement, review, or debug a Moneybag hosted checkout and server-side payment verification integration. Use for backend checkout code, redirect handling, order idempotency, transaction verification, credential safety, or sandbox testing against the reviewed public contract.
---

# Moneybag Checkout

Read [references/contract.md](references/contract.md) before generating code and
[references/security.md](references/security.md) before reviewing an integration.
Use [references/moneybag-public.json](references/moneybag-public.json) for exact
request fields, response schemas, authentication, and sandbox operations. This
file is bundled during installation; no platform repository or MCP server is required.

## Workflow

1. Create checkout from a trusted backend with `X-Merchant-API-Key`.
2. Generate and persist a unique merchant `order_id` before the request.
3. Redirect the customer only to the returned hosted checkout URL.
4. Treat success/cancel redirects as navigation, never payment evidence.
5. Verify the returned transaction ID from the trusted backend.
6. Reconcile verification and signed webhooks idempotently.

## Non-negotiable rules

- Never put merchant keys in browser/mobile code, logs, URLs, source control, or prompts.
- Use sandbox while developing and never silently switch to production.
- Never fulfill solely from redirect query parameters.
- Make fulfillment atomic and idempotent by merchant order ID or transaction ID.
- Preserve Moneybag error correlation IDs but sanitize customer and credential data.

State uncertainty explicitly; do not invent request fields or terminal states.
