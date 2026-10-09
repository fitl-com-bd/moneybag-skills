# Event categories

Implemented categories include payment lifecycle, settlement lifecycle, refund
lifecycle, recurring invoice, and subscription lifecycle events. Read the
event type from `X-Webhook-Event-Type`, but use the event ID for deduplication.
Treat unknown event types as validly signed but unsupported: record and ignore
them without returning a retry-inducing server error.
