# Public subscription contract

Moneybag Public OpenAPI 2.0.0. The review date and artifact digest are recorded
in `../contract-version.json`.

Server: `https://sandbox.api.moneybag.com.bd`

Authentication: `X-Merchant-API-Key` on every operation. The key identifies the
merchant; resources are tenant-scoped by that identity.

## Plans

- `POST /api/v2/payments/subscription-plans`
- `GET /api/v2/payments/subscription-plans`
- `GET /api/v2/payments/subscription-plans/{plan_id}`
- `PATCH /api/v2/payments/subscription-plans/{plan_id}`
- `DELETE /api/v2/payments/subscription-plans/{plan_id}`
- `POST /api/v2/payments/subscription-plans/{plan_id}/restore`

Plan paths use the numeric `plan_id`. Archive prevents new use without deleting
historical subscription relationships; restore is a deliberate mutation.

## Subscriptions

- `POST /api/v2/payments/subscriptions`
- `GET /api/v2/payments/subscriptions`
- `GET /api/v2/payments/subscriptions/{subscription_id}`
- `PATCH /api/v2/payments/subscriptions/{subscription_id}`
- `POST /api/v2/payments/subscriptions/{subscription_id}/pause`
- `POST /api/v2/payments/subscriptions/{subscription_id}/resume`
- `POST /api/v2/payments/subscriptions/{subscription_id}/cancel`
- `GET /api/v2/payments/subscriptions/{subscription_id}/billing-history`
- `POST /api/v2/payments/subscriptions/{subscription_id}/generate-invoice`
- `POST /api/v2/payments/subscriptions/{subscription_id}/checkout`

Subscription paths use the returned UUID. Creation accepts either `customer_id`
or `customer`, never both. Consult [moneybag-public.json](moneybag-public.json) for exact schemas
and bounds instead of restating them in generated code.
