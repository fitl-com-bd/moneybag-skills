# Integration review checklist

## Contract

- Use only the reviewed public OpenAPI routes and public UUID identifiers.
- Validate request/response assumptions, environment URLs, and error handling.

## Security and tenancy

- Keep credentials server-side, redacted, scoped, rotated, and environment-specific.
- Verify every read and mutation is constrained to the authenticated merchant.
- Reject arbitrary destinations, redirects, stale webhook timestamps, and invalid HMAC.

## Payment correctness

- Persist unique order IDs before requests and make fulfillment atomic/idempotent.
- Verify server-side; redirects are never evidence of payment.
- Reconcile timeouts and unknown outcomes instead of assuming failure.
- Tolerate duplicate, delayed, and out-of-order events.

## Operations

- Preserve sanitized correlation IDs and avoid PII/secret logging.
- Cover success, decline, cancel, timeout, duplicate, retry, and rollback paths.
- Define monitoring, escalation, credential revocation, and controlled cutover.
