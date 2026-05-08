# Planet Labs

Operates the largest commercial Earth observation constellation, providing daily 3m global PlanetScope imagery (the SuperDove fleet) plus high-resolution 50cm SkySat tasking with up to 10x daily revisit, accessible via REST APIs, a Python client, STAC catalog, and platform integrations.

**Tier:** Paid (with self-service plans starting in the low thousands USD/year and a 30-day free trial)
**Auth:** API key (Bearer or HTTP Basic) or OAuth 2.0 for Insights Platform
**Last researched:** 2026-05-07

## Use cases

- Daily-revisit broad-area monitoring with PlanetScope (3m, 8-band) for agriculture, deforestation, infrastructure, defense, and emergency response.
- High-resolution targeted tasking with SkySat (50cm, sub-daily revisit) for site monitoring, event response, and verification.
- Programmatic delivery of Analysis-Ready PlanetScope (ARPS) and Planet Basemaps into cloud workflows via STAC + Subscriptions API.
- "Single Order Tasking" workflows where the user pays per km² for a one-off SkySat capture without an annual contract.

## Pricing

- **Free tier:** 30-day Planet Insights Platform trial — sandbox PlanetScope data over hundreds of locations; Planet Education & Research Program (free for qualifying academic users, country-dependent).
- **Paid tiers:**
  - **Single Order Tasking (SkySat):**
    - SkySat Archive: $6 per km² (≥30-day-old imagery).
    - Flexible Tasking: $12 per km² (Planet picks best window).
    - Assured Tasking: $40 per km² (priority window, weather-tolerant).
  - **PlanetScope Monitoring (subscription):** Self-service plans available; pricing scales with area-under-management (AUM) and contract term — typically quoted by sales for production use. Tropical Forest Observation Program (TFOP) and similar programs offer reduced pricing for specific use cases.
  - **SkySat Tasking subscriptions:** Requires sales-quoted contract; minimum AOI 0.01 km² (1 hectare), tasking credit packages in 50 / 150 / 300 km² bundles.
- **Enterprise:** Annual contracts with custom data volumes, defense / intelligence pricing via sales.
- **Notes:** Planet Insights Platform is the unified portal; Sentinel Hub is now part of Planet, so PlanetScope can also be consumed through Sentinel Hub API plans.

## Authentication

Two patterns:

1. **Classic Planet API key** — `Authorization: api-key <PL_API_KEY>` or HTTP Basic with the API key as username and empty password. Get the key from `https://www.planet.com/account/`.
2. **OAuth 2.0** — for Planet Insights Platform applications and Sentinel Hub-style processing endpoints; client credentials flow against the Planet identity service.

## Endpoints

- **Base URL:** `https://api.planet.com`
- **Key endpoints:**
  - `POST /data/v1/quick-search` — Catalog search across item types (PSScene, SkySatScene, SkySatCollect, etc.).
  - `GET /data/v1/item-types/{type}/items/{id}/assets/` — list and activate downloadable assets.
  - `POST /compute/ops/orders/v2/orders` — Orders API: bundle multiple scenes, apply tools (clip, harmonize, COG), deliver to cloud bucket.
  - `POST /subscriptions/v1/subscriptions` — Subscriptions API: standing orders that auto-deliver new acquisitions.
  - `POST /tasking/v2/orders/` — Tasking API: SkySat / Pelican high-resolution tasking.
  - `https://api.planet.com/basemaps/v1/mosaics` — Planet Basemaps.
  - STAC catalog: `https://api.planet.com/stac` (Insights Platform).

## Example call

```bash
# Search for recent PlanetScope scenes over a point
curl -X POST "https://api.planet.com/data/v1/quick-search" \
  -u "$PL_API_KEY:" \
  -H "Content-Type: application/json" \
  -d '{
    "item_types": ["PSScene"],
    "filter": {
      "type": "AndFilter",
      "config": [
        {"type": "GeometryFilter","field_name": "geometry",
         "config": {"type": "Point","coordinates": [-122.4194, 37.7749]}},
        {"type": "DateRangeFilter","field_name": "acquired",
         "config": {"gte": "2026-04-25T00:00:00Z","lte": "2026-05-06T00:00:00Z"}},
        {"type": "RangeFilter","field_name": "cloud_cover",
         "config": {"lte": 0.2}}
      ]
    }
  }'
```

```python
# Python via the official planet client
from planet import Auth, Session, DataClient, data_filter
import asyncio

async def search():
    async with Session(auth=Auth.from_key("PL_API_KEY")) as sess:
        client = DataClient(sess)
        flt = data_filter.and_filter([
            data_filter.geometry_filter({"type": "Point", "coordinates": [-122.42, 37.77]}),
            data_filter.date_range_filter("acquired", gte="2026-04-25T00:00:00Z"),
            data_filter.range_filter("cloud_cover", lte=0.2),
        ])
        async for item in client.search(["PSScene"], search_filter=flt, limit=10):
            print(item["id"], item["properties"]["acquired"])

asyncio.run(search())
```

## Rate limits

Not publicly itemized for every endpoint. Generally:
- Data API search: ~10 requests/sec sustained, with burst allowance.
- Activation requests for assets: throttled per account.
- Tasking, Orders, and Subscriptions APIs use job-level concurrency caps based on subscription tier.
- 429 responses include `Retry-After` headers; clients are expected to back off.

## SDKs / Libraries

- **Official:**
  - [`planet`](https://github.com/planetlabs/planet-client-python) — Python SDK (CLI + async client).
  - [`@planet/client`](https://www.npmjs.com/package/@planet/client) — JavaScript/Node client.
  - QGIS plugin, ArcGIS Pro Add-In.
- **Community:** Various wrappers; Stanford / Brown / NASA CSDA integrations are well-documented examples.

## Documentation

- Main docs: https://docs.planet.com/
- Develop / APIs: https://docs.planet.com/develop/apis/
- Tasking API: https://docs.planet.com/develop/apis/tasking/
- Pricing: https://www.planet.com/pricing/

## Notes

- "Daily" PlanetScope coverage is land-only and weather-dependent; cloud cover and high latitudes affect actual revisit.
- SkySat fleet is 15 satellites with up to 10x daily revisit, 50cm orthorectified, 4-band + panchromatic, plus full-motion video for some captures.
- New "Planet SuperRes" generative AI product enhances 3m PlanetScope to 2m visual.
- For users who only need free/open data, prefer Copernicus Data Space Ecosystem (Sentinel-2, 10m, 5-day revisit).
- Pelican is Planet's next-generation high-resolution constellation, currently being phased into tasking workflows alongside SkySat.
- Archive holds: SkySat archive imagery is published 30 days after collection by default (configurable 0–30 day "Archive Hold").
