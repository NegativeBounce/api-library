# SkyWatch EarthCache

A satellite imagery aggregator API that consolidates 700+ sensors from leading commercial and public providers (Airbus, Planet, KOMPSAT, Sentinel, Landsat, Capella, etc.) behind a single REST API and pay-as-you-go pricing — no per-provider contracts required.

**Tier:** Paid (pay-as-you-use, no subscription required) with free/open data access at no extra charge
**Auth:** API key (Bearer token)
**Last researched:** 2026-05-07

## Use cases

- Adding satellite imagery as a feature inside a SaaS product without negotiating commercial terms with each provider.
- Aggregated tasking across multiple providers — let SkyWatch pick the best-fit sensor by resolution / availability / price for a given AOI.
- Prototyping with free Sentinel/Landsat (10m, 15m, 30m) data, then upgrading to commercial providers without rewriting integration code.
- Monitoring pipelines that need both archive search and future tasking against many constellations.

## Pricing

- **Free tier:** Open data access at no charge — Sentinel, Landsat, NAIP, etc., subject to fair-use rate limits.
- **Paid tiers:** Transparent pay-as-you-use, normalized across providers by resolution and AOI:
  - Low-resolution (5–30m): from a few dollars per task / km².
  - Mid-resolution (1.5–5m): typically $5–$20 per km².
  - High-resolution (30cm–1m): typically $20–$45+ per km², varies by provider.
  - Full per-provider pricing visible inside the EarthCache console / via API price endpoints — pricing is normalized so users see one unified quote per task.
- **Enterprise:** Custom volume contracts and the `HUB` product for multi-user organizations; defense/government quotes via sales.
- **Notes:** No subscriptions, no credit prepayment required for self-service users. Pricing is dynamic and surfaced per-request via the API; always check the live quote before submitting.

## Authentication

API key issued from the EarthCache console. Sent as `x-api-key: <YOUR_KEY>` header on all requests. Dedicated key per environment recommended.

## Endpoints

- **Base URL:** `https://api.skywatch.co/earthcache`
- **Key endpoints:**
  - `POST /archive/search` — start an archive search (returns search ID).
  - `GET /archive/search/{id}/search_results` — paginated results.
  - `POST /archive/orders` — order specific archive results.
  - `POST /tasking/orders` — submit a future tasking request.
  - `GET /tasking/orders/{id}/results` — poll for delivered captures.
  - `POST /pipelines` — set up a recurring delivery pipeline.

## Example call

```bash
# Start an archive search for high-res imagery over an AOI in the last 30 days
curl -X POST "https://api.skywatch.co/earthcache/archive/search" \
  -H "x-api-key: $SKYWATCH_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "location": {"type": "Polygon",
                 "coordinates": [[[-122.45,37.75],[-122.45,37.78],[-122.42,37.78],[-122.42,37.75],[-122.45,37.75]]]},
    "start_date": "2026-04-07",
    "end_date": "2026-05-07",
    "resolution": ["high"],
    "coverage": 80,
    "interval_length": 1,
    "order_by": ["resolution"]
  }'
```

```python
# Python (using requests)
import requests
r = requests.post(
    "https://api.skywatch.co/earthcache/archive/search",
    headers={"x-api-key": SKYWATCH_KEY, "Content-Type": "application/json"},
    json={
        "location": {"type": "Polygon", "coordinates": [...]},
        "start_date": "2026-04-07",
        "end_date": "2026-05-07",
        "resolution": ["medium", "high"],
        "coverage": 80,
    },
)
search_id = r.json()["data"]["id"]
results = requests.get(
    f"https://api.skywatch.co/earthcache/archive/search/{search_id}/search_results",
    headers={"x-api-key": SKYWATCH_KEY},
).json()
```

## Rate limits

Not publicly published. Search and order endpoints are throttled per account; commercial accounts can request elevated limits. 429 responses honored with backoff.

## SDKs / Libraries

- **Official:** EarthCache for ArcGIS Pro Add-In (via Esri Marketplace), EarthCache web console, SkyWatch BUILD developer platform.
- **Community:** [`chris010970/earthcache`](https://github.com/chris010970/earthcache) — Python demo client showing query/download patterns.

## Documentation

- Main docs: https://docs.earthcache.com/
- API reference: https://api-docs.earthcache.com/
- Pricing: https://skywatch.com/earthcache/pricing/

## Notes

- Strongest value for teams that need a single contract across many providers. Per-image pricing may be higher than going directly to each provider, in exchange for not maintaining N commercial relationships.
- "Live" depends on the underlying provider — SkyWatch passes through tasking latencies and archive holds from each constellation.
- Includes both optical and SAR data; aerial imagery (Nearmap) added via partnership announced in 2025.
