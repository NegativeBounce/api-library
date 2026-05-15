# SunriseSunset.io

Free unauthenticated REST API returning sunrise, sunset, first/last light, dawn, dusk, solar noon, golden hour, day length, sun position (altitude/azimuth), moonrise, moonset, moon phase, and moon illumination — with optional date ranges of up to one year per request.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-15

## Use cases

- Photography apps needing golden hour and sun position
- Outdoor activity planners (hiking, fishing, astrophotography)
- Real estate listings showing daylight hours
- Calendar/scheduling apps that need daylight context
- Bulk daily lookups across up to 365 days in a single request

## Pricing

- **Free tier:** Unlimited under fair use; no rate limit published, no signup required
- **Paid tiers:** None
- **Enterprise:** N/A
- **Notes:** Tips/donations accepted via Buy Me a Coffee. Sunrise/sunset times are automatically adjusted for elevation using terrain data.

## Authentication

None. No API key required.

## Endpoints

- **Base URL:** `https://api.sunrisesunset.io`
- **Key endpoints:**
  - `GET /json` — Returns sun, moon, golden hour, and elevation data for a lat/lng on a given date; supports `date_start`/`date_end` for ranges up to 365 days

## Example call

```bash
curl "https://api.sunrisesunset.io/json?lat=40.7128&lng=-74.0060&date=2026-05-15&time_format=24"
```

```python
import requests

resp = requests.get(
    "https://api.sunrisesunset.io/json",
    params={
        "lat": 40.7128, "lng": -74.0060,
        "date_start": "2026-05-15", "date_end": "2026-05-22",
    },
)
for day in resp.json()["results"]:
    print(day["date"], day["sunrise"], day["sunset"], day["moonrise"], day["moonset"])
```

## Rate limits

Not publicly documented. Fair use expected. A status page is available.

## SDKs / Libraries

- **Official:** None
- **Community:** Multiple community wrappers in Python and Node — most are thin HTTP wrappers given the API's simplicity

## Documentation

- Main docs: https://sunrisesunset.io/api/
- API reference: https://sunrisesunset.io/api/

## Notes

- Date supports relative formats: "today", "tomorrow".
- `formatted=0` returns ISO 8601; `time_format=unix` returns UNIX timestamps (UTC).
- Up to 365 days of data per request via `date_start` and `date_end`.
- Automatic terrain-based elevation adjustment for sunrise/sunset accuracy.
- Moon data (moonrise, moonset, phase, illumination) and sun position (altitude/azimuth) were added April 2026 — bringing feature parity with paid alternatives for free.
