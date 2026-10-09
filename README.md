# Moneybag Agent Skills

Install Moneybag integration guidance for Codex, Claude Code, Cursor, and other clients supported by the [skills CLI](https://github.com/vercel-labs/skills).

```sh
npx skills add fitl-com-bd/moneybag-skills
```

Run in your project directory. The installer lets you choose skills and clients. Requires Node.js and npm; installation needs no Moneybag account or API key.

For a specific client:

```sh
npx skills add fitl-com-bd/moneybag-skills --agent codex
npx skills add fitl-com-bd/moneybag-skills --agent claude-code
```

Start a new agent session after installing. In Codex, ask:

```text
$moneybag-checkout Add Moneybag sandbox checkout with server-side verification and idempotent fulfillment.
```

In Claude Code, use `/moneybag-checkout` with the same request. Other clients can use: “Use the moneybag-webhooks skill to build a signed webhook receiver with event deduplication.”

| Skill | Purpose |
| --- | --- |
| [moneybag-checkout](skills/moneybag-checkout/SKILL.md) | Hosted checkout, payment verification, and fulfillment |
| [moneybag-webhooks](skills/moneybag-webhooks/SKILL.md) | Raw-body signature verification and event deduplication |
| [moneybag-subscriptions](skills/moneybag-subscriptions/SKILL.md) | Plans and subscription lifecycle integration |
| [moneybag-emi](skills/moneybag-emi/SKILL.md) | EMI discovery and charge calculation |
| [moneybag-integration-review](skills/moneybag-integration-review/SKILL.md) | Security and payment correctness review |

Each package contains instructions, supporting references, and the reviewed public sandbox OpenAPI contract. Contract version: `2.0.0`; SHA-256: `34dbfe060318e05a382654a81a660e816a3402d568091a0f9fba28e9bbe15a9e`. The packages contain no credentials or account permissions. Configure sandbox keys only in trusted server code, and never use redirects as payment proof.

Add `--skill moneybag-checkout` to install one package, or `--global` for installation across projects. Run the install command again to fetch updates.

Read the [agent skills guide](https://developers.moneybag.com.bd/ai), [API reference](https://developers.moneybag.com.bd/api-reference), or [create a sandbox workspace](https://developers.moneybag.com.bd/sandbox).
