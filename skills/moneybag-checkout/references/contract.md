# Reviewed checkout contract

- Server: `https://sandbox.api.moneybag.com.bd`
- Authentication: `X-Merchant-API-Key`
- Create: `POST /api/v2/payments/checkout`
- Verify: `GET /api/v2/payments/verify/{transaction_id}`

Use [moneybag-public.json](moneybag-public.json), the bundled Moneybag Public
OpenAPI document, for exact fields and schemas. Checkout returns
`data.checkout_url`, `data.session_id`, and `data.expires_at`. Verification
requires the resulting `transaction_id`, not the checkout `session_id`.
Do not use unreviewed full-backend operations or portal JWT endpoints.

For Collection Dashboard attribution, the optional top-level `checkout_source`
accepts only `WEBSITE_CHECKOUT` or `API_INTEGRATION` (case-sensitive); any other
value causes a request validation error. Omit the field if the origin is unclear.
Choose the payment's origin: website payments use `WEBSITE_CHECKOUT` even though
the backend calls this API; application or automated integration workflows use
`API_INTEGRATION`. Native in-app checkout uses `API_INTEGRATION`; checkout started
on your merchant website inside a WebView uses `WEBSITE_CHECKOUT`. Opening
Moneybag's hosted page in a WebView does not change the original source.
Do not put this hint inside `metadata`. Omission or `null` retains
Unclassified Checkout. Attribution applies when a session is created; historical
transactions and reused sessions retain their original channel.
