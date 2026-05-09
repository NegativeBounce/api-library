# Tomorrow.io

Weather intelligence platform offering 60+ data layers (core weather, marine, lightning, fire, flood, air quality, and more) via REST APIs, with a free tier suited to development and an Enterprise tier for production maritime ops.

**Tier:** Freemium
**Auth:** API Key
**Last researched:** 2026-05-09

## Use cases

- Marine forecasts for the Strait of Malacca (wave height, sea-state, surface winds) on the Enterprise plan.
- Weather on Routes — score a planned voyage along its waypoints, useful for fleet ops.
- Custom monitoring (polygon/polyline alerting) — get notified when conditions exceed a threshold inside a defined Strait sub-zone.
- Lightning, severe-weather, and tropical-cyclone alerting for Strait-adjacent areas.
- Historical replays for incident reconstruction (up to 20 years of hourly).

## Pricing

- **Free tier:** 5-day forecast, core layers, 24h history, 1 monitored location, 1 alert. Useful for prototyping.
- **Paid tiers:** Multiple usage-based tiers (request count + features); pricing not publicly listed.
- **Enterprise:** 14-day forecast, premium layers (incl. marine), custom SLAs, route APIs.
- **Notes:** Marine fields are gated to higher tiers; free tier is not suitable for ops use.

## Authentication

API key issued in the developer console. Sent as `apikey` query parameter or via `Authorization: apikey <key>` header.

## Endpoints

- **Base URL:** `https://api.tomorrow.io/v4/`
- **Key endpoints:**
  - `GET /weather/realtime` — current conditions
  - `GET /weather/forecast` — 1h/1d forecast
  - `GET /weather/history/recent` — recent history
  - `GET /weather/history/archive` — historical archive
  - `POST /route` — Weather on Routes
  - `POST /events` — On-Demand Events query (threshold across 5 days)
  - Maps API and Monitor API surfaces

## Example call

```bash
curl "https://api.tomorrow.io/v4/weather/forecast?location=1.290,103.851&fields=waveSignificantHeight,windSpeed&apikey=$TOMORROW_KEY"
```

## Rate limits

Per-plan limits on requests/hour and requests/day; specifics published in the developer dashboard. Claims 99.9% uptime.

## SDKs / Libraries

- **Official:** None broadly distributed; OpenAPI spec available.
- **Community:** Python, Node libraries on GitHub.

## Documentation

- Main docs: https://docs.tomorrow.io/reference/welcome
- Marketing site: https://www.tomorrow.io/weather-api/

## Notes

- Marine variables (wave, sea-state, currents) are part of "premium" tiers. Confirm during signup.
- "Weather on Routes" is genuinely useful for Strait transit risk scoring — accepts a polyline of waypoints and returns conditions per leg.
