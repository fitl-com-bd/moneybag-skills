# EMI security review

- Keep API credentials and EMI requests on a trusted backend.
- Use only Moneybag-hosted checkout for payment authentication.
- Do not store PAN, CVV, OTP, processor credentials, or unredacted payloads.
- Verify transactions server-side and validate webhook raw-body signatures.
- Handle duplicates, delayed events, timeouts, and unknown outcomes idempotently.
- Never infer payment success from redirects or locally calculated installments.
