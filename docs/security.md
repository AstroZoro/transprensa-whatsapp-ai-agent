# Security and Public-Portfolio Policy

This repository is intentionally a **sanitized portfolio representation** of a larger automation system.

The production workflow export contains operational metadata that should not be committed to a public repository without review. This document defines what must remain private.

## Never publish

Do not commit any of the following:

- API keys or access tokens
- OpenAI credentials
- PostgreSQL usernames, passwords, or connection strings
- Meta / WhatsApp access tokens or webhook secrets
- real webhook signatures
- production hostnames or private infrastructure endpoints
- customer phone numbers, names, addresses, emails, or document numbers
- WhatsApp message IDs or account identifiers tied to real users
- browser cookies, session storage, authentication state, or Playwright `storageState`
- internal credential IDs when they reveal production configuration
- raw production `pinData`
- private workflow identifiers when they are not necessary for the portfolio
- screenshots containing customer or account data

## Why the raw workflow is not published directly

An n8n export may appear to contain only workflow logic, but it can also include:

- credential references;
- webhook IDs;
- linked workflow IDs;
- pinned production payloads;
- customer data used during debugging;
- internal URLs and infrastructure information.

For that reason, the current production workflow must be treated as sensitive source material.

## Sanitization checklist

Before publishing any n8n workflow example:

1. Remove `pinData` completely.
2. Replace credential objects with placeholder credential names or remove them.
3. Replace workflow IDs with neutral placeholders.
4. Replace webhook IDs and URLs.
5. Remove real customer data from sample payloads.
6. Remove phone-number IDs, business-account IDs, message IDs, and signatures.
7. Search the exported file for domains, IP addresses, emails, phone numbers, secrets, and tokens.
8. Verify browser automation files do not include session or authentication state.
9. Use synthetic example data only.
10. Review the final diff before pushing.

## Recommended public examples

A portfolio repository does not need a full production export to demonstrate technical ability.

Prefer publishing:

- architecture documentation;
- synthetic conversation examples;
- sanitized excerpts of workflow logic;
- generic state schemas;
- anonymized QA scenarios;
- diagrams showing integrations;
- `.env.example` files containing variable names only.

## Environment variables

When code examples require configuration, use environment variables such as:

```text
OPENAI_API_KEY=
POSTGRES_HOST=
POSTGRES_PORT=
POSTGRES_DB=
POSTGRES_USER=
POSTGRES_PASSWORD=
WHATSAPP_ACCESS_TOKEN=
WHATSAPP_PHONE_NUMBER_ID=
```

Never commit the populated `.env` file.

## Incident response

If a secret is accidentally committed to Git history:

1. revoke or rotate the credential immediately;
2. remove the secret from the repository and history where appropriate;
3. review access logs for unexpected use;
4. replace the compromised credential in the production environment.

Removing a secret from the latest commit alone does **not** make a leaked credential safe; rotation is the first priority.
