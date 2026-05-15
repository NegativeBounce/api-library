# Sunrise-Sunset.org

Free unauthenticated REST API returning sunrise, sunset, solar noon, day length, and the three twilight phases (civil, nautical, astronomical) for any latitude/longitude on a given date.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-15

## Use cases

- Quick sunrise/sunset lookups in personal projects, prototypes, and hobby sites
- Photography planning using the twilight values
- Educational/teaching examples for HTTP GET + JSON
- Lightweight server-side calculations where moon data isn't needed

## Pricing

- **Free tier:** Unlimited under "reasonable" usage — no rate limit published
- **Paid tiers:** None
- **Enterprise:** N/A
- **Notes:** Attribution back to sunrise-sunset.org is required. Excessive or abusive volume is prohibited per the published terms.

## Authentication

None. No API key, no registration. Just send a GET request.

## Endpoints

- **Base URL:** `https://api.sunrise-sunset.org`
- **Key endpoints:**
  - `GET /json` — Returns sunrise, sunset, solar noon, day length, and three twilight phases for a lat/lon and date

## Example call

```bash
curl "https://api.sunrise-sunset.org/json?lat=36.7202&lng=-4.4203&date=2026-05-15&formatted=0"
```

```python
import requests

resp = requests.get(
    "https://api.sunrise-sunset.org/json",
    params={"lat": 36.7202, "lng": -4.4203, "date": "2026-05-15", "formatted": 0},
)
data = resp.json()["results"]
print(data["sunrise"], data["sunset"])
```

## Rate limits

Not publicly documented. Terms ask for "reasonable request volume" — heavy or abusive usage is prohibited. A status page is available for uptime monitoring.

## SDKs / Libraries

- **Official:** None
- **Community:** Many community libraries exist for solar calculations (Python `suntime`, Node `suncalc`) — though most use local computation rather than this API

## Documentation

- Main docs: https://sunrise-sunset.org/api
- API reference: https://sunrise-sunset.org/api

## Notes

- **No moon data** — this API only covers sun events. For moonrise/moonset use SunriseSunset.io, IPGeolocation, USNO, AstronomyAPI.com, WeatherAPI.com, TimeAndDate, or Xweather.
- Date parameter accepts ISO format and relative formats like "today" and "tomorrow".
- Times default to UTC unless the `tzid` parameter is provided.
- JSONP supported via the `callback` query parameter.
- Set `formatted=0` to receive ISO 8601 timestamps and day length in seconds — recommended for production.
