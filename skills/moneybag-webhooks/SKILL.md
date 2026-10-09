---
name: moneybag-webhooks
description: Implement, review, or debug secure Moneybag webhook receivers. Use for HMAC verification, raw-body handling, replay prevention, idempotent event processing, retry behavior, payment reconciliation, or subscription event handling.
---

# Moneybag Webhooks

Read [references/signing.md](references/signing.md) for the exact signature
contract and [references/events.md](references/events.md) for event categories.
For payment or subscription reconciliation, look up the exact API operation in
[references/moneybag-public.json](references/moneybag-public.json), bundled with
this skill. Signing details are in the signing reference, not the OpenAPI schema.

## Workflow

1. Capture the unmodified request bytes before JSON parsing.
2. Read signature, timestamp, event type, and event ID headers.
3. Reject missing, malformed, stale, or invalid signatures.
4. Compute HMAC over `<timestamp>.<raw-body>` and compare in constant time.
5. Record event identity before side effects.
6. Return success for an already-processed valid event.
7. Queue expensive work and reconcile authoritative API state when needed.

## Non-negotiable rules

- Never log the webhook secret or full sensitive payload.
- Never parse/re-serialize JSON before signature verification.
- Never assume delivery order or exactly-once delivery.
- Separate signature acceptance from business-state transitions.
- Make fulfillment and subscription transitions atomic and idempotent.

Do not invent events or expose portal-only webhook configuration endpoints as a
merchant-key public API.
