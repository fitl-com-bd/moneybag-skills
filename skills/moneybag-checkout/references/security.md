# Checkout security review

- Key is read from a server-side secret store.
- Checkout creation and verification run only on the merchant backend.
- Order identity exists before network execution and cannot double-fulfill.
- Redirect URLs are allowlisted HTTPS destinations.
- Redirect state is not trusted as payment proof.
- Verification retries cannot create a second order or fulfillment.
- Logs exclude keys, PII, full request bodies, and payment data.
