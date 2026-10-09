# Subscription lifecycle

## Initial state

- Trial configured: `TRIALING`.
- No trial, `PREPAID`: `PENDING`; the first payment must activate service.
- No trial, `POSTPAID`: `ACTIVE`; the first invoice is issued after the consumed
  period.

## Operating states

- `ACTIVE` may be paused and becomes `PAUSED`.
- Only `PAUSED` may be resumed; it returns to `ACTIVE`.
- A failed billing attempt may move service to `PAST_DUE`; successful recovery
  returns it to `ACTIVE`.
- Immediate cancellation enters `CANCELLED`.
- Period-end cancellation records cancellation intent while service continues;
  the completed terminal state is `EXPIRED`.
- `CANCELLED` and `EXPIRED` must not be cancelled again.

Treat status reads, verified payments, and webhooks as potentially concurrent.
Apply transitions idempotently and re-fetch current state on conflict.
