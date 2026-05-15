# Xweather Sun Moon

Xweather's (formerly AerisWeather, now part of Vaisala) `sunmoon` REST endpoint provides sunrise, sunset, civil/nautical/astronomical twilight, moon rise/set, moon phase, and moon illumination for any location worldwide, up to one month of data per request.

**Tier:** Paid
**Auth:** Client ID + Client Secret (query parameters)
**Last researched:** 2026-05-15

## Use cases

- Enterprise applications requiring guaranteed uptime and SLA for astronomy + weather
- Media and broadcast applications needing combined sun/moon + lightning + weather imagery
- Aviation, maritime, and transportation operations
- Solar/renewable energy planning at high request volumes
- Combined astronomy + weather mapping with raster overlays (MapsGL)

## Pricing

- **Free tier:** 30-day free trial. PWSWeather Contributor Plan offers free API access (1,000 requests/day, 100/minute) to personal weather station owners.
- **Paid tiers:** Subscription plans roughly $23/month to $1,180/month depending on volume and feature set. Indicative published tiers include ~€300/mo (1M calls), €600/mo (3M), €700/mo (5M), €950/mo (10M).
- **Enterprise:** Custom plans for high-volume and specialized use cases; major airlines must enroll in custom Enterprise plans through the parent Weather Company / IBM portfolio
- **Notes:** Pricing is now branded under Vaisala/Xweather; exact current tiers are quoted via signup.xweather.com rather than a static pricing page. AerisWeather and Xweather URLs both serve documentation.

## Authentication

Sign up at xweather.com to receive a `client_id` and `client_secret`. Pass both as query parameters on each request.

## Endpoints

- **Base URL:** `https://data.api.xweather.com`
- **Key endpoints:**
  - `GET /sunmoon/{action}` — Sun and moon rise/set, twilights, moon rise/set/phase/illumination (up to 1 month per request). `action` accepts location queries by place name, `lat,lon`, postal code, etc.
  - `GET /sunmoon/moonphases/{action}` — Exact times of primary moon phases (new, first quarter, full, last quarter)

## Example call

```bash
curl "https://data.api.xweather.com/sunmoon/40.7128,-74.0060?\
client_id=$CLIENT_ID&client_secret=$CLIENT_SECRET&from=2026-05-15&to=2026-05-22"
```

## Rate limits

Per-minute and per-day caps vary by plan; the PWSWeather Contributor Plan caps at 1,000 requests/day with 100 requests/minute. Paid plans publish monthly call quotas (1M / 3M / 5M / 10M / custom).

## SDKs / Libraries

- **Official:** JavaScript, Python, iOS, Android developer toolkits; MapsGL SDK for visualization
- **Community:** Various third-party clients on GitHub

## Documentation

- Main docs: https://www.xweather.com/docs/weather-api
- API reference: https://www.xweather.com/docs/weather-api/endpoints/sunmoon (legacy docs also at aerisweather.com/support/docs/api/reference/endpoints/sunmoon/)

## Notes

- Moon details in `sunmoon` are an approximation based on calculated illumination; for exact primary phase times use `/sunmoon/moonphases`.
- Sunmoon is one endpoint of a much larger weather API — overlapping use case with WeatherAPI.com and Visual Crossing, but Xweather is heavier on enterprise features (lightning, road weather, hail, MapsGL).
- Rebranding history: AerisWeather → Xweather (under Vaisala). Some legacy docs still live at aerisweather.com.
- The free Contributor Plan is a genuine path to no-cost access for personal weather station contributors.
