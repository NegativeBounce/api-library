# IPGeolocation.io Astronomy API

REST API returning sunrise, sunset, moonrise, moonset, solar noon, day length, twilight phases (civil/nautical/astronomical), golden/blue hour, sun and moon altitude/azimuth/distance, and moon parallactic angle for any latitude/longitude or IP address on a given date.

**Tier:** Freemium
**Auth:** API key (query parameter)
**Last researched:** 2026-05-15

## Use cases

- Daily sunrise/sunset/moonrise lookups for global locations with ~1-minute accuracy
- Photography apps needing golden hour and blue hour times
- Solar panel installations needing sun altitude/azimuth
- Smart home lighting automation triggered by sun and moon events
- IP-based astronomy lookups (auto-locate user via IP)

## Pricing

- **Free tier:** 30,000 requests/month with a 1,000/day cap, no credit card required
- **Paid tiers:** Starter ~$15–$19/month (150,000 req/month), Plus ~$49/month (500,000 req/month), higher tiers with increased volume, priority support, and SLA
- **Enterprise:** Custom pricing, 99.99% uptime SLA
- **Notes:** Overage above monthly quota is billed at the plan's surcharge rate (varies by plan). Annual billing gives 2 months free (pay 10, get 12). Pricing sourced from ipgeolocation.io/pricing.html and may shift.

## Authentication

Sign up at ipgeolocation.io for a free account to obtain an API key. Pass the key as a query parameter: `?apiKey=YOUR_API_KEY`.

## Endpoints

- **Base URL:** `https://api.ipgeolocation.io`
- **Key endpoints:**
  - `GET /astronomy` — Returns sun and moon data for a location (lat/lon, address, or IP) on a given date
  - `GET /timezone` — Bundled timezone metadata; useful alongside astronomy lookups

## Example call

```bash
curl "https://api.ipgeolocation.io/astronomy?apiKey=$API_KEY&lat=40.7128&long=-74.0060&date=2026-05-15"
```

```python
import requests

resp = requests.get(
    "https://api.ipgeolocation.io/astronomy",
    params={"apiKey": API_KEY, "lat": 40.7128, "long": -74.0060, "date": "2026-05-15"},
)
data = resp.json()
print(data["astronomy"]["sunrise"], data["astronomy"]["sunset"], data["astronomy"]["moonrise"])
```

## Rate limits

Free plan: 30,000 requests/month with a 1,000/day cap. Paid plans scale with monthly quota; overage handling depends on plan-specific surcharge rate.

## SDKs / Libraries

- **Official:** Java, Python, Go, Ruby, Rust, Kotlin, Swift, C++, C#/.NET, PHP, TypeScript, JavaScript, jQuery SDKs (with a dedicated Astronomy JavaScript SDK)
- **Community:** Multiple community wrappers on GitHub

## Documentation

- Main docs: https://ipgeolocation.io/astronomy-api.html
- API reference: https://ipgeolocation.io/documentation/astronomy-api.html

## Notes

- When `time_zone` is provided, server-side conversion may push event timestamps to the previous or next calendar day relative to the queried date — design clients accordingly.
- IP-based queries accept IPv4 or IPv6 addresses for auto-location.
- Returns detailed twilight categories (civil/nautical/astronomical) plus blue and golden hour windows useful for photography.
