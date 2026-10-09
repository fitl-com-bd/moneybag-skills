---
name: moneybag-emi
description: Implement, review, or debug Moneybag installment-payment flows. Use for EMI option discovery, eligibility, tenure selection, payment-service UUID handling, hosted checkout, transaction verification, settlement assumptions, or deciding whether an EMI backend route is approved for public integration.
---

# Moneybag EMI

Read [references/contract.md](references/contract.md) before generating code and
[references/security.md](references/security.md) before reviewing an integration.
Use the bundled [references/moneybag-public.json](references/moneybag-public.json)
for exact discovery, calculation, and checkout request/response schemas.

## Workflow

1. Call the reviewed `GET /api/v2/payments/emi-options` operation to discover available EMI options for the merchant.
2. Call the reviewed `POST /api/v2/payments/emi-amounts` operation to retrieve eligible configurations, Moneybag-side charges, and customer payable amounts for the exact order amount.
3. Present only returned providers, tenures, and public UUID identifiers.
4. Submit the selected configuration unchanged from a trusted backend.
5. Use hosted checkout and treat redirects as navigation only.
6. Verify the transaction and reconcile signed webhooks before fulfillment.

## Non-negotiable rules

- Never invent eligibility, rates, fees, tenures, request fields, or terminal states.
- Never calculate authoritative EMI charges or settlement amounts locally — use the reviewed discovery and calculation operations.
- Never expose keys or collect card credentials in merchant code.
- Never call a backend-only EMI route merely because it exists in source or internal OpenAPI.
- Make order creation and fulfillment idempotent and preserve sanitized request IDs.

State the availability boundary explicitly if a future EMI route is not yet present in the reviewed public contract.
