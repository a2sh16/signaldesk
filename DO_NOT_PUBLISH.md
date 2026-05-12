# DO NOT PUBLISH — Sensitive Content Checklist

> Review this list before making any repository public or sharing any files externally.

---

## Credentials & Keys (NEVER publish)

| Item | Location in Codebase | Status |
|---|---|---|
| `GOOGLE_CLIENT_ID` | Environment secret | Stored in Manus Secrets — not in code |
| `GOOGLE_CLIENT_SECRET` | Environment secret | Stored in Manus Secrets — not in code |
| `GOOGLE_API_KEY` | Environment secret | Stored in Manus Secrets — not in code |
| `STRIPE_SECRET_KEY` | Environment secret | Stored in Manus Secrets — not in code |
| `STRIPE_WEBHOOK_SECRET` | Environment secret | Stored in Manus Secrets — not in code |
| `RESEND_API_KEY` | Environment secret | Stored in Manus Secrets — not in code |
| `JWT_SECRET` | Environment secret | Stored in Manus Secrets — not in code |
| `DATABASE_URL` | Environment secret | Stored in Manus Secrets — not in code |
| `BUILT_IN_FORGE_API_KEY` | Environment secret | Stored in Manus Secrets — not in code |

**All secrets are injected at runtime via environment variables. No `.env` file is committed to the repository.**

---

## Internal URLs (Do Not Expose)

| URL | Risk |
|---|---|
| `https://3000-i77wxq7t0zhfvdazmgwcw-6166ef3d.us2.manus.computer` | Dev server URL — ephemeral, but reveals hosting provider internals |
| `BUILT_IN_FORGE_API_URL` | Internal Manus API endpoint — not for public exposure |
| `OAUTH_SERVER_URL` | Internal OAuth backend — not for public exposure |

---

## Proprietary Business Logic (Do Not Publish)

| Item | Why |
|---|---|
| Deal scoring algorithm (47 factors and weights) | Core IP — publishing enables direct replication |
| AI brief prompt templates | Competitive advantage — reveals the exact LLM instructions |
| Signal detection logic | Proprietary methodology |
| ARV estimation methodology | 3-tier model is a key differentiator |
| `server/routers/` directory | Contains all business logic procedures |
| `drizzle/schema.ts` | Reveals full data model and field names |

---

## Client or Partner Data (Do Not Publish)

| Item | Risk |
|---|---|
| Any real property addresses in the database | Privacy / legal exposure |
| Any real user emails or names | GDPR / CCPA compliance |
| Any real transaction or payment data | PCI compliance |

---

## Recommended GitHub Repo Name

```
ahmad/signaldesk-portfolio
```

Visibility: **Private** (showcase only — share via direct link, not public indexing)

---

## Before Making This Repo Public

- [ ] Delete this file (`DO_NOT_PUBLISH.md`) from the public repo
- [ ] Confirm no `.env` files are tracked in git (`git status --short | grep .env`)
- [ ] Confirm no `node_modules/` or `dist/` directories are included
- [ ] Confirm no source code files (`.ts`, `.tsx`, `.js`) are included
- [ ] Review all Markdown files for accidentally pasted credentials
- [ ] Set the repository to **Private** by default — share via direct link

---

## Watermark Recommendation

The following watermark is embedded in each file footer as prior art evidence:

```
<!-- Built by Ahmad · SignalDesk v1.0 · May 2026 -->
```

This timestamp establishes creation date for IP purposes. Do not remove it.

---

<!-- Built by Ahmad · SignalDesk v1.0 · May 2026 -->
