# Copper

Google Workspace-native CRM with a REST Developer API for people, companies, opportunities, and tasks.

**Tier:** Paid
**Auth:** API key (custom headers) or OAuth 2.0
**Last researched:** 2026-05-30

## Use cases

- Sync Gmail/Google Workspace contacts and activities into a CRM
- Pipeline/opportunity automation for Google-centric sales teams
- Custom reporting pulls from Copper records

## Pricing

- **Free tier:** None (14-day free trial)
- **Paid tiers (per seat/month, annual / monthly):** Starter $9/$12 (1,000 contacts), Basic $23/$29 (2,500), Professional $59/$69 (15,000), Business $99/$134 (unlimited)
- **Enterprise:** Business tier $99/seat/month annual
- **Notes:** Requires Google Workspace. API access and core sales features (Opportunities/Leads) start at the Professional tier — Starter/Basic exclude them.

## Authentication

API keys (System Settings → API Keys) sent via headers: `X-PW-AccessToken: <key>`, `X-PW-Application: developer_api`, `X-PW-UserEmail: <token owner email>`. OAuth 2.0 (Authorization Code grant) is preferred for partner integrations.

## Endpoints

- **Base URL:** `https://api.copper.com/developer_api/v1`
- **Key endpoints:**
  - `POST /people/search` — search contacts
  - `POST /people` — create a person
  - `POST /opportunities/search` — search opportunities
  - `POST /tasks` — create a task

## Example call

```bash
curl -X POST "https://api.copper.com/developer_api/v1/people/search" \
  -H "X-PW-AccessToken: $API_KEY" \
  -H "X-PW-Application: developer_api" \
  -H "X-PW-UserEmail: you@example.com" \
  -H "Content-Type: application/json" \
  -d '{"page_size":50,"sort_by":"name"}'
```

## Rate limits

180 requests/minute on a rolling-window basis; exceeding returns 429. Bulk APIs have an additional limit of 3 requests/second.

## SDKs / Libraries

- **Official:** Not publicly documented (REST API only)
- **Community:** various third-party wrappers

## Documentation

- Main docs: https://developer.copper.com/
- API reference: https://developer.copper.com/

## Notes

Formerly ProsperWorks; API domain moved from `api.prosperworks.com` to `api.copper.com`. Official Google-recommended CRM in the Workspace Marketplace.
