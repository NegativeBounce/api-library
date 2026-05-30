# HubSpot

CRM plus marketing, sales, and service platform with a unified REST CRM API (v3) for contacts, companies, deals, and tickets.

**Tier:** Freemium
**Auth:** OAuth 2.0 or private app access token (Bearer); legacy API keys deprecated
**Last researched:** 2026-05-30

## Use cases

- Sync contacts/companies/deals between HubSpot and external systems
- Build custom internal integrations with private app tokens
- Bulk upserts via batch endpoints to stay under rate limits

## Pricing

- **Free tier:** Free CRM tools (with HubSpot branding, tighter limits)
- **Paid tiers (Sales Hub):** Starter $15/seat, Professional $100/seat, Enterprise $150/seat (per month, billed annually)
- **Enterprise:** $150/seat/month + mandatory $3,500 onboarding
- **Notes:** Professional adds a mandatory $1,500 onboarding; seat-based pricing; API is free within rate limits

## Authentication

Use OAuth 2.0 for public/multi-account apps; private app static tokens for single-account integrations. Pass as `Authorization: Bearer <token>`. Tokens expire (`expires_in`) and must be refreshed.

## Endpoints

- **Base URL:** `https://api.hubapi.com`
- **Key endpoints:**
  - `GET /crm/v3/objects/contacts` — list contacts
  - `POST /crm/v3/objects/contacts` — create a contact
  - `POST /crm/v3/objects/contacts/search` — search (separate, stricter limit)
  - `POST /crm/v3/objects/contacts/batch/create` — batch create

## Example call

```bash
curl -H "Authorization: Bearer $TOKEN" \
  "https://api.hubapi.com/crm/v3/objects/contacts?limit=10"
```

## Rate limits

Private apps: ~190 requests/10s (Professional/Enterprise), ~100/10s on lower tiers; daily caps of 250k (Free/Starter), 650k (Professional), 1M (Enterprise). CRM Search API is capped much lower (~4-5 req/s shared across all search endpoints). Batch endpoints count as one request. 429 responses include Retry-After.

## SDKs / Libraries

- **Official:** Node (@hubspot/api-client), Python (hubspot-api-client), PHP, Ruby
- **Community:** numerous wrappers across languages

## Documentation

- Main docs: https://developers.hubspot.com/docs/api/overview
- API reference: https://developers.hubspot.com/docs/reference/api

## Notes

v3 is current; some endpoints still use v1/v2. 10,000-object cap on bulk CRM operations catches many integrations off guard.
