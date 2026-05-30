# Pipedrive

Sales-focused CRM with a REST API (v1 and v2) for deals, persons, organizations, and pipelines.

**Tier:** Paid
**Auth:** API token (header) or OAuth 2.0 (Bearer, for marketplace apps)
**Last researched:** 2026-05-30

## Use cases

- Pipeline/deal sync between Pipedrive and external tools
- Bulk lead and person imports
- Marketplace apps acting on behalf of customers via OAuth

## Pricing

- **Free tier:** None (14-day free trial)
- **Paid tiers:** Essential $14, Advanced $29, Professional $59, Power $69, Enterprise $99 (per user/month, billed annually)
- **Enterprise:** $99/user/month; volume discounts negotiable
- **Notes:** Monthly billing ~21% higher; add-ons (LeadBooster, Smart Docs, etc.) priced separately

## Authentication

Personal API token via `x-api-token: <token>` header (v2) — note v1 accepted `?api_token=` query param, removed in v2. OAuth 2.0 tokens use `Authorization: Bearer <token>` and are required for Marketplace apps; OAuth tokens are issued from the `oauth.pipedrive.com` domain.

## Endpoints

- **Base URL:** `https://{company}.pipedrive.com/api/v2` (the `/api/` segment is required for v2)
- **Key endpoints:**
  - `GET /deals` — list deals
  - `POST /persons` — create a person
  - `GET /organizations` — list organizations
  - `POST /leads` — create a lead (v1 only)

## Example call

```bash
curl -H "x-api-token: $API_TOKEN" \
  "https://yourcompany.pipedrive.com/api/v2/deals"
```

## Rate limits

Token-Based Rate Limit (TBRL): daily budget = 30,000 base tokens × plan multiplier × number of seats (+ purchased top-ups); each endpoint costs a set number of tokens. Burst limit ~80 requests/2s (higher on upper tiers). 429 responses include X-RateLimit-* and X-Daily-Requests-Left headers.

## SDKs / Libraries

- **Official:** Node (pipedrive), Python (pipedrive)
- **Community:** wrappers in PHP, Ruby, Go

## Documentation

- Main docs: https://developers.pipedrive.com/docs/api/v1
- API reference: https://developers.pipedrive.com/docs/api/v1

## Notes

V1 endpoints sunset after July 2026 — migrate to v2. Not every resource has a v2 endpoint yet (Leads, Notes remain v1). Custom fields are represented by 40-character hash keys.
