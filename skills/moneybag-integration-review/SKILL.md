---
name: moneybag-integration-review
description: Audit a Moneybag payment integration for contract correctness, credential safety, tenant isolation, idempotency, webhook verification, unknown outcomes, logging, testing, and production readiness. Use for code review, architecture review, launch assessment, incident follow-up, or migration checks across checkout, subscriptions, webhooks, and EMI.
---

# Moneybag Integration Review

Read [references/checklist.md](references/checklist.md) and the bundled
[references/moneybag-public.json](references/moneybag-public.json) before asserting
endpoint fields or states. For signing guidance, consult the public
[webhook guide](https://developers.moneybag.com.bd/docs/webhooks); install
`moneybag-webhooks` if detailed receiver implementation is needed.

## Review workflow

1. Establish environment, reviewed contract version, integration surfaces, and trust boundaries.
2. Trace credentials, customer input, order identity, payment state, and webhook data end to end.
3. Verify deny-by-default route exposure and tenant-scoped access at every mutation.
4. Test retries, duplicate requests/events, stale signatures, cancellation, decline, timeout, and reconciliation.
5. Report findings by severity with evidence, impact, and the smallest safe remediation.
6. Separate sandbox readiness from production approval and deployment authorization.

Do not modify production, rotate live credentials, replay live events, or move
money during a review. Do not report unsupported assumptions as facts.
