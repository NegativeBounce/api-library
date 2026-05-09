# Meltwater

Media intelligence platform combining news monitoring, social listening, and analytics. API access typically bundled with Enterprise contracts. Strong global coverage including Asia-Pacific.

**Tier:** Enterprise
**Auth:** API Key / OAuth (via Meltwater Developer Portal)
**Last researched:** 2026-05-09

## Use cases

- Combined news + social listening for Strait-related coverage and consumer chatter.
- Real-time streaming console for ops dashboards.
- Modular product selection (media monitoring + social listening + analytics + influencer + sales intelligence).
- Asia-Pacific language coverage including Indonesian, Malay, Mandarin, Thai.
- Integration into existing customer platforms (CRM, BI tools, custom apps) via Meltwater APIs.

## Pricing

- **Free tier:** None.
- **Paid tiers:** Custom-quoted.
- **Enterprise:** Standard contracting model; pricing varies with seats, regions, modules, contract length.
- **Notes:** API access is typically included in Enterprise contracts but can require additional fees on smaller deployments.

## Authentication

API key / OAuth issued via Meltwater Developer Portal post-contract. Bearer token typical.

## Endpoints

- **Developer portal:** `https://developer.meltwater.com/`
- **Base URL (illustrative):** `https://api.meltwater.com/v1/`
- **Surface areas:**
  - Listening (search + streaming)
  - Media monitoring (news)
  - Analytics
  - Streaming Console (real-time delivery)

## Example call

```bash
# Illustrative — actual endpoints provisioned via Meltwater Developer Portal.
curl -H "Authorization: Bearer $MELTWATER_TOKEN" \
  "https://api.meltwater.com/v1/listening/search?query=%22strait+of+malacca%22"
```

## Rate limits

Per-plan; documented in the developer portal.

## SDKs / Libraries

- **Official:** None broadly distributed.
- **Community:** Limited.

## Documentation

- Main site: https://www.meltwater.com/en/products/api-and-integrations
- Developer portal: https://developer.meltwater.com/
- Listening overview: https://developer.meltwater.com/docs/meltwater-api/listening/overview/

## Notes

- Best fit when news + social must be unified — Meltwater is one of the few enterprise platforms that does both genuinely well.
- Pairs naturally with Brandwatch (insight) or Talkwalker (visual) depending on emphasis.
- Long sales cycle; expect a 4–8 week procurement.
