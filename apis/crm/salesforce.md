# Salesforce

Enterprise CRM platform exposing sales, service, and data via a portfolio of APIs (REST, Bulk 2.0, GraphQL, SOAP, Pub/Sub).

**Tier:** Freemium
**Auth:** OAuth 2.0 (connected app / external client app), Bearer token
**Last researched:** 2026-05-30

## Use cases

- CRUD on standard/custom objects (Accounts, Contacts, Opportunities) from external systems
- Large async data loads via Bulk API 2.0
- Event-driven integrations via Pub/Sub API (change data capture, platform events)

## Pricing

- **Free tier:** Free Suite, limited, up to 5 users
- **Paid tiers:** Starter Suite $25, Pro Suite $100, Enterprise $175, Unlimited $350 (per user/month, billed annually)
- **Enterprise:** Agentforce 1 Sales $550/user/month; volume & multi-year discounts via sales
- **Notes:** ~6% price increase applied Aug 2025 to Enterprise/Unlimited; implementation fees ($5K-$500K+) are separate

## Authentication

OAuth 2.0 via a connected app (migrating to External Client Apps in Spring '26). Client credentials flow for server-to-server. Token endpoint: `https://<mydomain>.my.salesforce.com/services/oauth2/token`. Pass the access token as `Authorization: Bearer <token>`.

## Endpoints

- **Base URL:** `https://<instance>.my.salesforce.com/services/data/v66.0`
- **Key endpoints:**
  - `GET /sobjects/Account/{id}` — retrieve a record
  - `POST /sobjects/Contact` — create a record
  - `GET /query?q=<SOQL>` — run a SOQL query
  - `POST /jobs/ingest` — Bulk API 2.0 load

## Example call

```bash
curl -H "Authorization: Bearer $ACCESS_TOKEN" \
  "https://mydomain.my.salesforce.com/services/data/v66.0/query?q=SELECT+Id,Name+FROM+Account+LIMIT+10"
```

## Rate limits

Per-org rolling 24-hour API request limits set by edition plus purchased licenses (e.g., Enterprise base allotment plus an allotment per license), with separate concurrent long-running request limits. Exact allotment varies by edition; check the org's company information page.

## SDKs / Libraries

- **Official:** Salesforce CLI, Mobile SDK (iOS/Android)
- **Community:** simple-salesforce (Python), jsforce (Node)

## Documentation

- Main docs: https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/
- API reference: https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_list.htm

## Notes

Current API version is v66.0 (Spring '26). API versions 21.0-30.0 were retired Summer '25 (return HTTP 410/400). Not one API but a portfolio — pick the right surface (REST for CRUD, Bulk for volume, Pub/Sub for events).
