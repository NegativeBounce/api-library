# SkyFi

Self-service Earth-observation marketplace API that aggregates 40+ providers / 150+ satellites for archive search, multi-sensor tasking, analytics, and delivery — with transparent, upfront pricing and no contracts.

**Tier:** Freemium
**Auth:** API Key
**Last researched:** 2026-05-28

## Use cases

- One API to search/order optical, SAR, multispectral, thermal, and aerial imagery across many providers
- Automated AOI monitoring with webhook notifications and recurring orders
- Running built-in analytics (object detection, vessel detection, stockpile measurement) on imagery

## Pricing

- **Free tier:** Open data (e.g., Sentinel-2) available at no charge; no subscription/commitment required
- **Paid tiers:** Pay-per-order with prices shown upfront — e.g., PlanetScope archive from ~$3.75/km²; optical tasking from ~$300 (25 km² @ 50cm) or ~$812 (25 km² @ 30cm); SAR tasking from ~$675 per 5×5 km scene
- **Enterprise:** Volume/defense workflows via sales
- **Notes:** No quotes or hidden fees; price is calculated instantly from AOI, resolution, and sensor.

## Authentication

Create a SkyFi account and generate an API key from the dashboard. Pass the API key in a request header (see the ReDoc reference for the exact header name). The same key powers search, ordering, tasking, and analytics.

## Endpoints

- **Base URL:** `https://app.skyfi.com/platform-api`
- **Key endpoints:**
  - Archive search — find existing imagery for an AOI
  - Pricing/feasibility — cost estimate before ordering
  - Order placement & tasking — purchase archive or task new captures
  - Analytics execution, webhook notifications, and AOI monitoring

## Example call

```bash
# Search the archive (see ReDoc for exact header name + request schema)
curl -H "X-Skyfi-Api-Key: $SKYFI_API_KEY" \
  "https://app.skyfi.com/platform-api/..."
```

## Rate limits

Not publicly documented.

## SDKs / Libraries

- **Official:** Interactive ReDoc docs with Python & JavaScript examples (app.skyfi.com/platform-api/redoc)
- **Community:** SkyFi MCP server (github.com/mfuechec/SkyFiMCP) for AI-agent access

## Documentation

- Main docs: https://skyfi.com/en/api
- API reference: https://app.skyfi.com/platform-api/redoc

## Notes

SkyFi is an aggregator/"virtual constellation," not a satellite operator — useful when you want one integration across providers instead of separate contracts. Deliverables (GeoTIFF/PNG + metadata) ship to AWS S3 or Google Cloud Storage. Resolutions from ~10m down to 30cm; dual-use (civil + defense).
