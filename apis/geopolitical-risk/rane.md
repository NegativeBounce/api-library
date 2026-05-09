# RANE (Risk Assistance Network + Exchange)

Enterprise risk-intelligence platform combining geopolitical, cyber, and compliance threat coverage. Inherits Stratfor's geopolitical analysis bench (acquired in 2020). Worldview platform plus dedicated intelligence services. API integration available.

**Tier:** Enterprise
**Auth:** API Key / OAuth (per contract)
**Last researched:** 2026-05-09

## Use cases

- Geopolitical analysis on Indonesia, Malaysia, Singapore, and broader Southeast Asia — particularly strong on regional power-balance, U.S.-China dynamics affecting the Strait, and ASEAN politics.
- Worldview — Stratfor-style strategic forecasts and country-specific deep dives.
- Threat intelligence (cyber + physical) integrated with geopolitical context.
- Due diligence and risk screening for counterparties and portfolio companies.
- Dedicated analyst engagements for bespoke Strait-related questions (state-actor moves, naval positioning, choke-point disruption scenarios).

## Pricing

- **Free tier:** None.
- **Paid tiers:** None publicly listed.
- **Enterprise:** Custom-quoted; serves 400+ organizations including corporates, government agencies, and academic institutions.
- **Notes:** Stratfor / Worldview content historically had low-cost individual subscriptions; under RANE the offering is enterprise-focused.

## Authentication

API key / OAuth 2.0 token issued post-contract. Worldview platform also uses standard SSO.

## Endpoints

- **Public sites:** `https://www.ranenetwork.com/`, `https://worldview.stratfor.com/`
- **API base URL:** Customer-issued.
- **Surface areas:**
  - Risk Intelligence — multi-domain integrated platform
  - Geopolitical Intelligence (incorporating Stratfor)
  - Cyber Intelligence
  - Threat Intelligence
  - Intelligence Briefs

## Example call

```bash
# Illustrative — actual endpoints provisioned per RANE contract.
curl -H "Authorization: Bearer $RANE_TOKEN" \
  "https://api.ranenetwork.com/v1/intelligence/search?q=Strait%20of%20Malacca&since=2026-04-01"
```

## Rate limits

Not publicly documented.

## SDKs / Libraries

- **Official:** None broadly published.
- **Community:** None.

## Documentation

- Main site: https://www.ranenetwork.com/
- Worldview: https://worldview.stratfor.com/

## Notes

- Stratfor heritage is the differentiator for geopolitical content — long-form analyst writing on Strait-relevant topics is uncommon among API-first competitors.
- Best fit when narrative analysis matters as much as structured data feeds.
- Often paired with Verisk Maplecroft (indices), ACLED (events), and Sayari/Kharon (entities) in mature risk-intelligence stacks.
