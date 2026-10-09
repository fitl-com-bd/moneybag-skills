# EMI contract boundary

The bundled reviewed public artifact is [moneybag-public.json](moneybag-public.json). Treat it as
the only callable partner contract. As of the 2026-09-16 review, `GET
/api/v2/payments/emi-options` (discovery) and `POST /api/v2/payments/emi-amounts`
(calculation of Moneybag-side charges and customer payable amounts) are both reviewed public operations,
runnable in API Lab with `X-Merchant-API-Key`.

Use returned public identifiers unchanged for payment-service and EMI
configuration selection, including any documented identifier prefix. Do not
substitute database integers. Derive exact request and response fields
from the reviewed artifact at implementation time.
