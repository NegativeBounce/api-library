# SeaLagom

Aggregator API delivering NAVAREA, coastal navigational, and maritime safety warnings from official sources globally, refreshed every 15 minutes. Single normalized REST endpoint with coordinate extraction and webhooks.

**Tier:** Freemium
**Auth:** API Token (header)
**Last researched:** 2026-05-09

## Use cases

- Single-API access to all 21 NAVAREAs including NAVAREA XI (covers Strait of Malacca region — coordinated by Japan).
- Real-time monitoring of Coastal Navigational Warnings issued by Indonesia, Malaysia, Singapore, Thailand.
- Coordinate extraction from natural-language warning text — feeds directly into geofence ops.
- Webhook delivery (Full plan) for push alerts on new warnings.
- Filtering by date, keyword, country, or polygon — useful for narrowing to Strait-relevant content.

## Pricing

- **Basic (Free):** 100 free requests for new users; 1,000 tokens thereafter (1 token per 50 records).
- **More Requests:** 3,000 tokens.
- **Pro:** Adds coordinate extraction and keyword filtering (paid tier).
- **Full API:** Unlimited requests, webhooks, archived messages access.
- **Notes:** Token consumption (1 per 50 records) is generous for low-volume use; archived messages gated to Full plan.

## Authentication

API token issued at signup. Sent in `X-API-Token: <token>` header.

## Endpoints

- **Base URL:** `https://sealagom.com/api/v1/`
- **Key endpoints:**
  - `GET /navarea/` — list NAVAREAs
  - `GET /navarea/{id}/messages/` — active messages for a NAVAREA (e.g., XI)
  - `GET /navarea/{id}/archived_messages/` — historical messages (Full only)
  - `GET /coastal/` — list coastal warnings
  - `GET /coastal/{id}/messages/` — active coastal messages
- **Coordinate formats:** decimal, Google Maps, GeoJSON, DMS.

## Example call

```bash
# Active NAVAREA XI messages (Strait-of-Malacca region)
curl "https://sealagom.com/api/v1/navarea/11/messages/" \
  -H "X-API-Token: $SEALAGOM_TOKEN"
```

## Rate limits

Per-token-pool throttling; Basic and More Requests = 1 token per 50 records, Full = unlimited.

## SDKs / Libraries

- **Official:** None broadly distributed.
- **Community:** Some Python wrappers.

## Documentation

- Main site: https://www.sealagom.com/
- API docs: https://www.sealagom.com/api/docs/
- NAVAREA browsing: https://www.sealagom.com/navarea/

## Notes

- Differentiator vs. NGA MSI is global aggregation — SeaLagom unifies NAVAREA XI (Japan), NAVAREA VIII (India), and coastal warnings from Asian states into one schema.
- Coordinate extraction is the killer feature — broadcast warnings are notoriously free-text; SeaLagom's parsing into structured lat/lon makes them machine-actionable.
- Cross-check against official sources (JHOD for NAVAREA XI; NGA MSI for ASAM) for safety-critical decisions.
