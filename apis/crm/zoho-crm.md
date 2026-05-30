# Zoho CRM

CRM with a REST API (v8) covering leads, contacts, deals, and accounts; part of the broader Zoho ecosystem with shared OAuth.

**Tier:** Freemium
**Auth:** OAuth 2.0 only (`Authorization: Zoho-oauthtoken <token>`)
**Last researched:** 2026-05-30

## Use cases

- Sync large lead/contact volumes from marketing tools into Zoho CRM
- Multi-data-center deployments routing EU/IN/AU data correctly
- COQL queries for analytics and reporting pulls

## Pricing

- **Free tier:** Free edition, up to 3 users
- **Paid tiers:** Standard $14, Professional $23, Enterprise $40, Ultimate $52 (per user/month, billed annually)
- **Enterprise:** Enterprise $40/user/month adds Zia AI; Ultimate $52 adds advanced analytics
- **Notes:** Monthly billing ~20-34% higher; add-on API credit packs available

## Authentication

OAuth 2.0 is the only supported method (legacy auth-token model removed). Obtain a grant token, exchange for access/refresh tokens at `https://accounts.zoho.com/oauth/v2/token` (DC-specific). Send `Authorization: Zoho-oauthtoken <access_token>`. Always use the same data-center domain the credentials were issued in.

## Endpoints

- **Base URL:** `https://www.zohoapis.com/crm/v8` (DC-specific: `.eu`, `.in`, `.com.au`, `.jp`, etc.)
- **Key endpoints:**
  - `GET /crm/v8/Leads` — list leads
  - `POST /crm/v8/Contacts` — create contacts
  - `GET /crm/v8/Deals` — list deals
  - `POST /crm/v8/coql` — run a COQL query

## Example call

```bash
curl -H "Authorization: Zoho-oauthtoken $ACCESS_TOKEN" \
  "https://www.zohoapis.com/crm/v8/Leads"
```

## Rate limits

Credit-based, calculated per 24-hour rolling window. Standard edition = 50,000 + (250 × users), capped at 100,000; higher base for higher editions. Most calls cost 1 credit; some cost more (e.g., Convert Lead = 5). Remaining credits surfaced in the X-API-CREDITS-REMAINING header once 50%+ is consumed. Concurrency limits also apply.

## SDKs / Libraries

- **Official:** Python, Java, Node.js, PHP, Ruby, C#, mobile SDKs
- **Community:** various wrappers

## Documentation

- Main docs: https://www.zoho.com/crm/developer/docs/api/v8/
- API reference: https://www.zoho.com/crm/developer/docs/api/v8/modules-api.html

## Notes

v8 is current (replaced v7 as default). Getting the data-center base URL wrong is the most common integration failure. All Zoho product APIs share the same OAuth system.
