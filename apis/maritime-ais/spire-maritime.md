# Spire Maritime

Satellite-based AIS data provider offering global coverage (including blue-water and equatorial regions where terrestrial AIS is sparse), now distributed by Kpler. Includes Vessels, Predict (ETA forecasting), and Historical APIs.

**Tier:** Enterprise
**Auth:** API Key / OAuth 2.0 (Bearer token)
**Last researched:** 2026-05-09

## Use cases

- Open-ocean vessel tracking outside terrestrial AIS range — useful for vessels approaching the Strait from the Indian Ocean (Sumatra coast, Bay of Bengal).
- Predicted-ETA service (Spire Predict) for proactive transit planning.
- Historical AIS replays going back 10+ years for incident reconstruction or pattern-of-life analysis.
- Cross-validation of terrestrial AIS feeds (MarineTraffic, VesselFinder) with satellite-sourced data — important when suspect vessels go dark in the Strait.
- Bulk historical extracts via Snowflake (Kpler LiveDB) for analytics workloads.

## Pricing

- **Free tier:** None. Trial / demo available on request.
- **Paid tiers:** None published; enterprise subscription only.
- **Enterprise:** Custom-quoted by Kpler. Pricing typically scales with vessel count, message volume, latency tier, and historical depth.
- **Notes:** No public price list since the Kpler acquisition consolidated Spire Maritime into Kpler's enterprise sales motion.

## Authentication

OAuth 2.0 access tokens or API keys via the Kpler developer portal. GraphQL endpoints typically use Bearer tokens.

## Endpoints

- **Base URL (legacy Spire):** `https://api.spire.com/` (REST and GraphQL)
- **Kpler-hosted endpoints:** vary by product family — see https://developers.kpler.com/
- **Key surfaces:**
  - **Vessels API** — current and recent positions, including satellite-only coverage zones.
  - **Predict API** — forecasted ETAs and destinations.
  - **Historical AIS API** — bulk and query-based access to >10 years of AIS.
  - **NMEA 0183 streams** — raw AIS feed for direct ingestion.
  - **LiveDB / Snowflake share** — analytics-grade continuous database.

## Example call

```bash
curl -X POST "https://api.spire.com/graphql" \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"query":"{ vessels(mmsi: 566093000) { staticData { name imo } lastPositionUpdate { latitude longitude timestamp } } }"}'
```

## Rate limits

Not publicly documented; defined per contract.

## SDKs / Libraries

- **Official:** None published broadly; integration is via REST/GraphQL/NMEA.
- **Community:** None notable.

## Documentation

- Kpler developer portal: https://developers.kpler.com/
- Product page: https://www.kpler.com/spireMT/product
- AIS service docs: https://servicedocs-sm.kpler.com/

## Notes

- Spire's satellite AIS constellation is the differentiator vs. MarineTraffic/VesselFinder, which lean more on terrestrial receivers. For dark-vessel detection workflows in open ocean adjacent to the Strait, Spire is the stronger feed.
- Sometimes called "Spire Sea" or "Spire Maritime" interchangeably.
- Satellite revisit cadence is faster near the equator (favorable for the Strait of Malacca region) than at high latitudes.
- Same Kpler enterprise-sales gate as MarineTraffic — expect a multi-week procurement cycle.
