# Close

Inside-sales CRM with built-in calling and SMS, exposing a REST API (v1) for leads, contacts, opportunities, and activities.

**Tier:** Paid
**Auth:** API key (HTTP Basic) or OAuth 2.0 (Bearer)
**Last researched:** 2026-05-30

## Use cases

- Push leads/contacts/activities into Close from a website or external system
- Two-way CRM sync with other platforms
- Custom sales reporting and pipeline analytics

## Pricing

- **Free tier:** None (14-day free trial, includes free data migration)
- **Paid tiers (per user/month, annual / monthly):** Starter $25/$29, Basic $59/$69, Professional $89/$99, Business $129/$149
- **Enterprise:** Business tier $129/user/month annual; custom plans available
- **Notes:** API & Zapier access included on all plans; calls/SMS usage billed separately

## Authentication

API keys (created under Settings → Developer → API Keys) use HTTP Basic auth and are best for internal scripts. OAuth 2.0 (register an app for a client ID/secret) is recommended for public/user-facing apps; pass `Authorization: Bearer <access_token>`.

## Endpoints

- **Base URL:** `https://api.close.com/api/v1`
- **Key endpoints:**
  - `GET /lead/` — list leads
  - `POST /contact/` — create a contact
  - `GET /opportunity/` — list opportunities
  - `POST /activity/call/` — log a call

## Example call

```bash
curl -u "$API_KEY:" \
  "https://api.close.com/api/v1/lead/"
```

## Rate limits

Enforced per endpoint group, at both per-API-key and per-organization levels (org limit = 3× a single key's limit). 429 responses include a ratelimit header with limit/remaining/reset; sleep for the reset value before retrying. Bulk endpoints have their own limits.

## SDKs / Libraries

- **Official:** an MCP server is provided for AI agents
- **Community:** Python (closeio), Node.js, Ruby, PHP, Go

## Documentation

- Main docs: https://developer.close.com/
- API reference: https://developer.close.com/api

## Notes

Docs expose AI-friendly `/llms.txt` and `.md` views per page. Phone numbers and per-minute calling costs are charged on top of seat pricing.
