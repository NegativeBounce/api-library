# Freshsales

Freshworks' sales CRM with a REST API for contacts, accounts, deals, leads, and sales activities.

**Tier:** Freemium
**Auth:** API key (token-based) + bundle alias
**Last researched:** 2026-05-30

## Use cases

- Sync contacts/deals between Freshsales and external systems
- Automate lead creation and sales-activity logging
- Pull pipeline and deal data for custom reporting

## Pricing

- **Free tier:** Free plan, up to 3 users (limited features, no custom fields)
- **Paid tiers (per user/month, annual / monthly):** Growth $9/$11, Pro $39/$47, Enterprise $59/$71
- **Enterprise:** $59/user/month annual (custom modules, audit logs)
- **Notes:** 21-day free trial of Enterprise features; CPQ add-on ~$19/user beyond the 1 included license; Freshsales Suite adds marketing

## Authentication

API key authentication via `Authorization: Token token=<API_KEY>`. You also need the bundle alias to specify which CRM account in your Freshworks org to target. The key is found under Profile Settings → API Settings.

## Endpoints

- **Base URL:** `https://<bundle-alias>.myfreshworks.com/crm/sales/api`
- **Key endpoints:**
  - `GET /contacts` — list contacts
  - `POST /deals` — create a deal
  - `GET /leads` — list leads
  - `POST /sales_activities` — log an activity

## Example call

```bash
curl -H "Authorization: Token token=$API_KEY" \
  "https://yourbundle.myfreshworks.com/crm/sales/api/contacts"
```

## Rate limits

Tiered by plan, calculated per minute and per hour at the account level (per agent for most modules). Default is roughly 1,000 requests/hour; exceeding returns 429. Limit increases available as a paid add-on.

## SDKs / Libraries

- **Official:** Freshworks Developer Platform / app SDK
- **Community:** various wrappers

## Documentation

- Main docs: https://developers.freshworks.com/crm/api/
- API reference: https://developers.freshworks.com/crm/api/

## Notes

Bundle alias is required for every request. Standalone Freshsales vs Freshsales Suite (Suite bundles marketing automation). Freddy AI lead scoring is available from the Growth plan.
