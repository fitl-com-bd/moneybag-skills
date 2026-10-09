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
