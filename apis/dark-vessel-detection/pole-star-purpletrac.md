# Pole Star PurpleTRAC

Automated, API-enabled vessel sanctions and risk screening platform from Pole Star Global, screening ships, ownership, management, and associated entities against 1,800+ sanctions and enforcement watchlists across 90+ jurisdictions. Combines screening with vessel tracking and event alerting.

**Tier:** Paid
**Auth:** API Key (REST)
**Last researched:** 2026-05-09

## Use cases

- Pre-port-call sanctions screening for vessels approaching Singapore, Port Klang, and Belawan.
- Vessel watchlist screening for fleet managers — ownership, management, beneficial-owner chains.
- Bills of lading and container screening (PurpleTRAC also covers cargo-side compliance).
- Continuous tracking — receive alerts when a screened vessel changes flag, ownership, or enters a high-risk area.
- Bulk batch screening directly from MS Excel files (no integration required).

## Pricing

- **Free tier:** None.
- **Paid tiers:** Subscription tiers (SaaS or API-integration), priced per screened entity / per seat. Exact prices not publicly listed.
- **Enterprise:** Full database can be downloaded on-premise with multiple daily updates.
- **Notes:** Customers include large shipping operators, banks, freight forwarders, and government agencies.

## Authentication

API key authentication on the REST API. Credentials issued via the Pole Star developer portal.

## Endpoints

- **Developer portal:** `https://developers.polestarglobal.com/`
- **PurpleTRAC API docs:** `https://developers.polestarglobal.com/docs/purpletrac-v1/`
- **Surface areas:**
  - Ship & flag watchlist check
  - Vessel screening (with ownership graph)
  - BL / container screening
  - Position update / event subscriptions

## Example call

```bash
# Screen a vessel and retrieve screening results
curl -X POST "https://api.polestarglobal.com/purpletrac/v1/screenings" \
  -H "Authorization: ApiKey $POLESTAR_KEY" \
  -H "Content-Type: application/json" \
  -d '{"imo":"9525338","mode":"vessel"}'
```

## Rate limits

Not publicly documented; defined per subscription.

## SDKs / Libraries

- **Official:** None broadly distributed; REST API designed for direct integration.
- **Community:** None notable.

## Documentation

- PurpleTRAC product page: https://www.polestarglobal.com/purpletrac/
- API documentation: https://developers.polestarglobal.com/docs/purpletrac-v1/
- Sanctions screening use case: https://www.polestarglobal.com/use-cases/sanctions-screening/

## Notes

- PurpleTRAC overlaps with the Sanctions category — also catalogued there for cross-reference.
- For Strait of Malacca specifically, PurpleTRAC is the strongest "compliance gate" tool — automated checks before a vessel is allowed alongside.
- Pole Star is widely used by P&I clubs, banks, and the U.S. Department of the Treasury (OFAC has cited Pole Star in advisories).
