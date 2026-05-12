# Nexar API (Octopart)

GraphQL API for electronic component supply chain, design, and manufacturing data sourced from Octopart's database of millions of parts across hundreds of distributors.

**Tier:** Freemium
**Auth:** OAuth 2.0 (client credentials)
**Last researched:** 2026-05-12

## Use cases

- Look up real-time pricing, stock levels, and lifecycle status for semiconductor parts across distributors
- Pull datasheets, technical specs, and CAD models for components used in BOM analysis
- Find similar/alternative parts when sourcing semiconductor components facing supply constraints
- Aggregate distributor pricing for procurement optimization workflows

## Pricing

- **Free tier:** "Evaluation" plan — up to 100 matched parts returned per month; full supply data fields (price, availability, lifecycle, datasheets, specs, ECAD, similar parts)
- **Paid tiers:**
  - Standard — up to 2,000 matched parts; supply data only (price, availability, images, advanced search). Lead time, lifecycle, datasheets, tech specs **not** included
  - Pro — up to 15,000 matched parts; supply data plus add-on access to lead time, lifecycle, datasheets, tech specs
  - Public pricing for Standard/Pro not listed — contact sales via the Nexar portal
- **Enterprise:** Custom plans; full data access including ECAD modules and similar parts
- **Notes:** Billing unit is "matched parts returned," not API calls. Successor to the legacy Octopart APIv4 (deprecated). Powers Altium's Octopart, Altium 365, and Altimade ecosystems.

## Authentication

OAuth 2.0 client credentials flow. Sign up at https://portal.nexar.com, create an organization, then create an application to receive `client_id` and `client_secret`. Exchange those for a bearer token at `https://identity.nexar.com/connect/token`, then send `Authorization: Bearer <token>` on every GraphQL request.

## Endpoints

- **Base URL:** `https://api.nexar.com/graphql`
- **Token URL:** `https://identity.nexar.com/connect/token`
- **Key operations (GraphQL):**
  - `supSearch` — search parts by keyword across the supply database
  - `supSearchMpn` — search by manufacturer part number
  - `supMultiMatch` — batch match a list of MPNs
  - `supParts` — fetch parts by unique part ID with full detail
  - `desCreatePcbDesignJob` — design/Altium 365 integration (separate scope)

## Example call

```bash
# 1. Get access token
curl -X POST "https://identity.nexar.com/connect/token" \
  -d "grant_type=client_credentials" \
  -d "client_id=$NEXAR_CLIENT_ID" \
  -d "client_secret=$NEXAR_CLIENT_SECRET" \
  -d "scope=supply.domain"

# 2. Search for a part
curl -X POST "https://api.nexar.com/graphql" \
  -H "Authorization: Bearer $NEXAR_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"query":"query { supSearchMpn(q: \"STM32F407VGT6\", limit: 5) { results { part { mpn manufacturer { name } medianPrice1000 { price currency } } } } }"}'
```

```python
import requests
token = requests.post(
    "https://identity.nexar.com/connect/token",
    data={"grant_type": "client_credentials",
          "client_id": NEXAR_CLIENT_ID,
          "client_secret": NEXAR_CLIENT_SECRET,
          "scope": "supply.domain"},
).json()["access_token"]

resp = requests.post(
    "https://api.nexar.com/graphql",
    headers={"Authorization": f"Bearer {token}"},
    json={"query": 'query { supSearchMpn(q: "STM32F407VGT6") { results { part { mpn medianPrice1000 { price currency } } } } }'},
)
```

## Rate limits

Not published as request/minute caps. Billing is by "matched parts returned" per month against your plan's quota (100 / 2,000 / 15,000 / custom). Plans documented at https://nexar.com/compare-plans.

## SDKs / Libraries

- **Official:** No officially-maintained SDK. GraphQL queries via any HTTP client. Code samples and Postman collections in docs.nexar.com.
- **Community:** Various community wrappers on GitHub (search "nexar-api" or "octopart-api").

## Documentation

- Main docs: https://docs.nexar.com/
- Plan comparison: https://nexar.com/compare-plans
- Support / how-to: https://support.nexar.com/support/home

## Notes

- The Octopart REST API v4 was deprecated; all integrations must use the Nexar GraphQL API.
- 9,000+ organizations registered; 500,000+ daily API calls serviced (per Nexar's site).
- Free Evaluation plan is most generous on **data fields** (everything included) but caps at only 100 matched parts — useful for PoC, not production.
- Owned by Altium Ltd. (acquired by Renesas Electronics in 2024).
