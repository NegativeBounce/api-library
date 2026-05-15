# WeatherAPI.com

Comprehensive weather REST API including a dedicated `/astronomy.json` endpoint returning sunrise, sunset, moonrise, moonset, moon phase, and moon illumination for any city, zip code, or lat/lon. Historical data goes back to January 1, 2010; forecasts extend up to 14 days (plan-dependent).

**Tier:** Freemium
**Auth:** API key (query parameter)
**Last researched:** 2026-05-15

## Use cases

- Combined weather + astronomy lookups in a single provider
- Photography apps needing forecast weather alongside sun/moon data
- Historical analysis going back to 2010 (insurance, daylight context for events)
- Hyperlocal scheduling apps (events, deliveries, outdoor work)

## Pricing

- **Free tier:** 100,000 calls/month, 3-day forecast, no credit card required (attribution required)
- **Paid tiers:** Pro $7/month (3M calls), Pro+ $25/month (5M calls), Business $35/month (10M calls) — based on the most recent public pricing
- **Enterprise:** Custom pricing; includes historical solar irradiance, evapotranspiration, pollen, and air quality
- **Notes:** Overage stops service for the remainder of the month rather than billing. 10% discount on annual payment. Free plan requires attribution back to weatherapi.com.

## Authentication

Sign up at weatherapi.com to receive an API key. Pass as a query parameter: `?key=YOUR_API_KEY`.

## Endpoints

- **Base URL:** `https://api.weatherapi.com/v1`
- **Key endpoints:**
  - `GET /astronomy.json` — Sunrise, sunset, moonrise, moonset, moon phase, illumination for a date and location
  - `GET /forecast.json` — Forecast including astronomy data for each day
  - `GET /history.json` — Historical weather + astronomy back to 2010-01-01
  - `GET /timezone.json` — Local time and zone info
  - `GET /marine.json` — Marine forecast including astronomy and tides

## Example call

```bash
curl "https://api.weatherapi.com/v1/astronomy.json?key=$API_KEY&q=40.7128,-74.0060&dt=2026-05-15"
```

```python
import requests

resp = requests.get(
    "https://api.weatherapi.com/v1/astronomy.json",
    params={"key": API_KEY, "q": "40.7128,-74.0060", "dt": "2026-05-15"},
)
astro = resp.json()["astronomy"]["astro"]
print(astro["sunrise"], astro["sunset"], astro["moonrise"], astro["moonset"], astro["moon_phase"])
```

## Rate limits

Per-month call quota by plan (100K free / 3M Pro / 5M Pro+ / 10M Business). Hitting the cap stops service until UTC midnight on the 1st of the next month — no surcharge model. Per-minute rate limits not publicly documented.

## SDKs / Libraries

- **Official:** REST API only; supports JSON and XML responses
- **Community:** Multiple wrappers on PyPI/npm; RapidAPI listing also available

## Documentation

- Main docs: https://www.weatherapi.com/docs/
- API reference: https://www.weatherapi.com/docs/

## Notes

- Historical data is forecast-derived rather than from actuals — fine for astronomy (deterministic), but a caveat for weather variables.
- Astronomy data is also embedded in `/forecast.json` and `/marine.json` for combined queries.
- A bulk endpoint is available on higher-tier plans for batch location queries.
- The Marine endpoint adds tide data alongside astronomy.
