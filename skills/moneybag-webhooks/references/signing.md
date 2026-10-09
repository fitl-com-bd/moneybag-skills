# Signing contract

Headers:

- `X-Webhook-Signature`: `sha256=<hex digest>`
- `X-Webhook-Timestamp`: Unix timestamp as text
- `X-Webhook-Event-Type`: event name
- `X-Webhook-Event-Id`: stable event identifier

Signed message: `<timestamp>.<raw JSON request body>`

Algorithm: HMAC-SHA256 using the webhook configuration secret. Compare the
complete expected signature with constant-time equality. Choose and enforce a
timestamp tolerance for your receiver's replay protection; Moneybag does not
publish a required receiver-side tolerance.
