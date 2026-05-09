# Echosec by Flashpoint

Geospatial OSINT platform aggregating mainstream social media, fringe networks, and messaging apps onto an interactive map. Now part of Flashpoint's Physical Threat Intelligence stack. Strong location-first workflow.

**Tier:** Enterprise
**Auth:** API Key (Bearer)
**Last researched:** 2026-05-09

## Use cases

- Geofenced social monitoring around Strait of Malacca coordinates and port anchorages.
- Real-time alerts on posts from within a customer-defined polygon (e.g., a 5km radius around Belawan).
- Coverage of fringe and messaging-app sources beyond mainstream social platforms.
- Integrated AI for surfacing actionable items (Echosec Optimize, launched Dec 2025).
- Combined with Flashpoint's broader threat-intelligence (cyber + physical) feeds.

## Pricing

- **Free tier:** None.
- **Paid tiers:** None publicly listed.
- **Enterprise:** Custom-quoted via Flashpoint sales (pricing portal at go.flashpoint.io/pricing requires contact).
- **Notes:** Pricing typically includes Flashpoint Ignite intelligence access alongside Echosec geo-listening.

## Authentication

API key issued post-contract via Flashpoint customer portal.

## Endpoints

- **Public site:** `https://flashpoint.io/ignite/echosec-by-flashpoint/`
- **API base URL:** Customer-issued.
- **Surface areas:**
  - Geospatial search (lat/lon + radius / polygon)
  - Source-filtered queries (social, fringe, messaging)
  - Real-time alerts on saved AOIs
  - AI-driven optimization (Echosec Optimize)

## Example call

```bash
# Illustrative — actual endpoints provisioned per Flashpoint contract.
curl -H "Authorization: Bearer $ECHOSEC_TOKEN" \
  "https://api.flashpoint.io/echosec/v1/search?lat=1.290&lon=103.851&radius_km=5&since=2026-05-08T00:00:00Z"
```

## Rate limits

Plan-dependent; not publicly documented.

## SDKs / Libraries

- **Official:** Customer-issued.
- **Community:** None notable.

## Documentation

- Echosec product page: https://flashpoint.io/ignite/echosec-by-flashpoint/
- Flashpoint pricing: https://go.flashpoint.io/pricing
- Datasheet: https://flashpoint.io/resources/datasheets/echosec-platform-overview/

## Notes

- The geospatial-first workflow is the differentiator vs. Brandwatch/Talkwalker/Meltwater.
- Useful for ops centres that think in maps, not in keyword feeds.
- For Strait-of-Malacca, geofenced alerts on port anchorages and chokepoints align directly with maritime ops needs.
