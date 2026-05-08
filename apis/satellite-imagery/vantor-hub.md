# Vantor Hub (formerly Maxar Geospatial Platform / MGP)

The cloud-based developer platform for the Vantor (formerly Maxar) commercial Earth observation constellation, providing programmatic tasking, streaming, ordering, and analytics over the WorldView and Legion fleet — 30cm native resolution, ~3.8 million km² collected daily, 20+ year archive (~125 PB).

**Tier:** Enterprise (subscription, premium plans starting around $10,000/year)
**Auth:** OAuth 2.0 bearer token (or API key for non-administrative endpoints, 180-day default expiry)
**Last researched:** 2026-05-07

## Use cases

- Defense, intelligence, and government use cases requiring 30cm resolution, 4m CE90 absolute accuracy, and rapid (hours-after-collection) availability.
- Persistent monitoring of high-value sites with FlexView (flexible window) or FastView (priority) tasking tiers.
- Streaming Vivid Mosaic basemaps (15 cm HD over high-interest areas, 30 cm HD covering ~99% of land) into GIS clients via WMTS/WMS.
- Change Monitoring (CM) vector analytics over registered AOIs using Vantor's pre-computed change products.

## Pricing

- **Free tier:** None (limited free trial / sandbox available to qualified developers via the developer portal).
- **Paid tiers:** Subscription-based, formerly branded "MGP Pro" / "SecureWatch":
  - **MGP Pro / Vantor Hub Pro subscriptions:** Premium plans start at ~$10,000/year for streaming + analytics access; pricing scales with concurrent users, AOI / km² included, and tier (basic stream, premium stream + download, change monitoring, etc.).
  - **Tasking:** Charged per km² with two tiers — FlexView (lower cost, broader window, weather-dependent) and FastView (priority, narrower window). Stereo and private tasking available in some tiers.
- **Enterprise:** Custom contracts for defense, intelligence, and large commercial customers; sales-driven for production deployments.
- **Notes:** All commercial pricing is quoted via Vantor sales / authorized resellers (Cansel, PacGeo, etc.). Public dashboard pricing is rare for this tier of provider.

## Authentication

OAuth 2.0 against the Vantor Hub Auth API — POST username/password to receive a bearer token (limited duration, refreshable). For application-to-application use, generate API keys in the console (default 180-day expiration) and pass as `MAXAR-API-KEY` header. Admin endpoints require the bearer token; non-admin endpoints accept either.

## Endpoints

- **Base URL:** `https://api.maxar.com` (endpoints are migrating to `vantor.com` domains alongside the rebrand)
- **Key endpoints:**
  - `POST /auth/v1/oauth2/token` — OAuth2 token endpoint.
  - `GET /discovery/v1/catalog/search` — STAC-compliant catalog search.
  - `POST /tasking/v1/order` — submit a tasking request (FlexView or FastView).
  - `GET /tasking/v1/feasibility` — feasibility check before ordering.
  - `POST /ordering/v1/orders` — order specific catalog items via a named "pipeline" (download, stream, etc.).
  - `GET /streaming/v1/ogc/wmts` and `/streaming/v1/ogc/wms` — Vantor stream tile endpoints.
  - `POST /raster-analytics/v1/...` — synchronous analytics (NDVI, NDWI, classification).
  - `GET /vector-analytics/v1/...` — Change Monitoring vector access via OGC.
  - `POST /monitoring/v1/aois` — register AOIs for new-data alerts.

## Example call

```bash
# 1. Token (or use long-lived API key)
TOKEN=$(curl -s -X POST "https://api.maxar.com/auth/v1/oauth2/token" \
  -d "grant_type=password" \
  -d "client_id=hub-client" \
  -d "username=$MAXAR_USER" \
  -d "password=$MAXAR_PASS" | jq -r .access_token)

# 2. Catalog search via STAC
curl "https://api.maxar.com/discovery/v1/catalog/search" \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "intersects": {"type": "Point", "coordinates": [-77.0369, 38.9072]},
    "datetime": "2026-04-01T00:00:00Z/2026-05-06T00:00:00Z",
    "collections": ["wv02", "wv03-vnir", "lg01"],
    "limit": 10,
    "query": {"eo:cloud_cover": {"lte": 20}}
  }'
```

## Rate limits

Tier-dependent and contract-specific. Standard subscription accounts are limited on concurrent streaming users, daily AOI allocation, and tasking km²/month. Detailed quotas are surfaced in the Hub admin console.

## SDKs / Libraries

- **Official:** Hub web UI, plugins for ArcGIS Pro, ArcGIS Online, and QGIS. Python sample code and reference notebooks via the developer portal.
- **Community:** Limited public SDK ecosystem, given the gated commercial nature of the platform.

## Documentation

- Developer portal: https://developers.maxar.com/
- API docs: https://developers.maxar.com/docs
- Hub documentation: https://pro-docs.maxar.com/en-us/
- Status page: https://hub-status.vantor.com/
- Product page: https://maxar.com/maxar-intelligence/products/mgp-pro

## Notes

- Maxar Intelligence rebranded its commercial product line as **Vantor** in 2025; the platform is now called the **Vantor Hub** (formerly the Maxar Geospatial Platform / MGP / MGP Pro / SecureWatch). API hostnames are in transition between `maxar.com` and `vantor.com` — check the developer portal for current endpoints when integrating.
- "Live" here means imagery available for download or streaming within hours of collection — among the fastest commercial latencies for 30cm optical.
- The constellation revisits any location up to ~15x/day (combined WorldView + Legion), with daily collection capacity of ~7M km².
- For SWIR or stereo pairs, ensure the subscription tier and tasking endpoint support those products — some require the FlexView tier or specific add-on entitlements.
- Most stringent compliance posture among commercial providers (FedRAMP, ITAR, etc.) — relevant for U.S. government and cleared work.
