# Sentinel Hub

A commercial RESTful API platform (now owned by Planet, originally Sinergise) that provides on-the-fly processing, mosaicking, and tile streaming over a wide range of Earth observation collections — Sentinel-1/2/3/5P, Landsat, MODIS, PlanetScope, DEM, and bring-your-own COGs.

**Tier:** Freemium
**Auth:** OAuth 2.0 (client credentials)
**Last researched:** 2026-05-07

## Use cases

- Building responsive web maps that stream cloud-free Sentinel-2 mosaics, NDVI, or custom band combinations on the fly via WMS/WMTS.
- Server-side scripted processing (evalscripts in JavaScript) to extract specific bands, indices, or visualizations without downloading full scenes.
- Time-series statistics over an AOI (Statistical API) without pulling rasters — useful for agriculture, monitoring dashboards.
- Batch processing of country / continent-scale jobs against a unified catalog with delivery to S3.

## Pricing

- **Free tier:** 30-day trial — 30,000 requests/month, 300 PU/min, no commercial use, no commercial data (TPDI), no batch API.
- **Paid tiers (via Sinergise / Planet billing):**
  - **Exploration** (non-commercial/research): €30/mo or €300/yr — 30,000 PU/mo, 100,000 requests/mo.
  - **Basic:** €100/mo or €999/yr — 70,000 PU/mo, 700,000 requests/mo, commercial use allowed.
  - **Enterprise S:** €500/mo or €5,000/yr — 400,000 PU/mo, 800,000 requests/mo, batch API enabled.
  - **Enterprise L:** €1,000/mo or €10,000/yr — 1,000,000 PU/mo, 10,000,000 requests/mo.
  - **Top-up packages:** 50,000 PU + 100,000 requests per package (rollover up to 12 months).
- **Enterprise:** Custom plans available on request via info@sentinel-hub.com.
- **Notes:** VAT not included. Annual subscriptions get a discount over monthly. PU cost depends on output pixels, number of input scenes/bands, format (16-bit costs 2x 8-bit), and processing complexity.

## Authentication

OAuth 2.0 client credentials flow. Create an OAuth client in the Sentinel Hub Dashboard (or CDSE dashboard for the CDSE-hosted endpoints), then exchange `client_id` + `client_secret` for a bearer token at `/oauth/token`. Token sent as `Authorization: Bearer <token>` on all subsequent requests.

## Endpoints

- **Base URL (Sinergise/Planet hosted):** `https://services.sentinel-hub.com`
- **Base URL (CDSE hosted, free Sentinel data):** `https://sh.dataspace.copernicus.eu`
- **Key endpoints:**
  - `POST /api/v1/process` — Processing API: synchronous on-the-fly imagery generation from an evalscript, AOI, time range, and collection.
  - `POST /api/v1/catalog/1.0.0/search` — Catalog API (STAC-compliant): search available scenes by collection/bbox/datetime/cloud-cover.
  - `POST /api/v1/statistics` — Statistical API: compute per-AOI per-time-bucket aggregates without rendering rasters.
  - `POST /api/v1/batch/process` — Batch Processing API: large-area asynchronous jobs delivered to S3 (Enterprise only).
  - `GET /ogc/wms/{instance-id}` and `/ogc/wmts/{instance-id}` — OGC tile endpoints configured per-instance via the dashboard.

## Example call

```bash
# 1. Get token
TOKEN=$(curl -s -X POST "https://services.sentinel-hub.com/oauth/token" \
  -d "grant_type=client_credentials" \
  -d "client_id=$SH_CLIENT_ID" \
  -d "client_secret=$SH_CLIENT_SECRET" | jq -r .access_token)

# 2. Process API: get a true-color Sentinel-2 image as PNG
curl -X POST "https://services.sentinel-hub.com/api/v1/process" \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -o image.png \
  -d '{
    "input": {
      "bounds": {"bbox": [13.4, 45.5, 13.5, 45.6]},
      "data": [{"type": "sentinel-2-l2a",
                "dataFilter": {"timeRange": {"from": "2026-04-01T00:00:00Z","to": "2026-05-06T00:00:00Z"},
                               "maxCloudCoverage": 20}}]
    },
    "output": {"width": 512, "height": 512,
               "responses": [{"identifier": "default","format": {"type": "image/png"}}]},
    "evalscript": "//VERSION=3\nfunction setup(){return{input:[\"B04\",\"B03\",\"B02\"],output:{bands:3}}}\nfunction evaluatePixel(s){return [2.5*s.B04, 2.5*s.B03, 2.5*s.B02]}"
  }'
```

## Rate limits

- Per-minute and per-month PU + request limits are tier-dependent (see Pricing).
- Trial: 300 PU/min, 30,000 requests/month.
- Exploration / Basic: 300–500 PU/min.
- Enterprise S/L: 1,000–2,000 PU/min, 300–1,200 requests/min.
- HTTP 403 with detailed message returned when a quota is exceeded.

## SDKs / Libraries

- **Official:**
  - [`sentinelhub-py`](https://github.com/sentinel-hub/sentinelhub-py) (Python).
  - QGIS Sentinel Hub plugin.
  - Requests Builder GUI for prototyping.
- **Community:** Various wrappers in JS/Node, R; Sentinel Hub also integrates with `eo-learn` and openEO.

## Documentation

- Main docs: https://docs.sentinel-hub.com/
- API reference: https://docs.sentinel-hub.com/api/latest/
- Pricing: https://www.sentinel-hub.com/pricing/ (now redirects to https://www.planet.com/pricing/)
- CDSE-hosted variant: https://documentation.dataspace.copernicus.eu/APIs/SentinelHub.html

## Notes

- Sinergise (the original Sentinel Hub company) was acquired by Planet in 2023; Sentinel Hub plans now flow through Planet billing for new customers, while existing direct Sentinel Hub customers remain supported.
- The same Sentinel Hub APIs are also available *for free* (with reduced quotas) via the Copernicus Data Space Ecosystem at `https://sh.dataspace.copernicus.eu` — covering Sentinel-1/2/3/5P, Landsat, and Copernicus DEM. Use that endpoint for free Sentinel data and the Sinergise/Planet endpoint for commercial collections (PlanetScope via TPDI, etc.).
- "Live" here means the latency of the underlying collection (e.g., Sentinel-2 NRT ~4 hours after overpass); Sentinel Hub itself adds minimal latency on top.
- Category overlap with Copernicus Data Space Ecosystem and (for PlanetScope/SkySat) Planet — kept separate because Sentinel Hub is the API platform whereas CDSE is the data ecosystem and Planet is the constellation operator.
