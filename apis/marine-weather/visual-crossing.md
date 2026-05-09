# Visual Crossing Weather

Weather API platform with a generous free tier (1,000 records/day, commercial use allowed) and pay-as-you-go pricing. Marine fields (wave height, swell) are first-class.

**Tier:** Freemium
**Auth:** API Key
**Last researched:** 2026-05-09

## Use cases

- Cost-effective weather + marine forecasts for the Strait of Malacca with commercially-permissive pricing.
- Historical weather at scale — Visual Crossing exposes long historical archives.
- Weather Maps for analyst dashboards.
- Excel / Power BI / Google Sheets integration via published add-ins — useful for non-engineer analysts in maritime ops.
- Migration path from legacy Dark Sky / OpenWeather integrations.

## Pricing

- **Free tier:** 1,000 records/day, commercial and non-commercial use — meaningful for prototyping and small-scale ops.
- **Paid tiers:**
  - **Metered:** Pay-as-you-go at $0.0001/record (~$1 per 10K records).
  - **Professional:** Per-user monthly/annual subscription.
  - **Corporate:** Unlimited access plans.
- **Enterprise:** Custom contracts for high volume / concurrency / on-prem.
- **Notes:** Records ≈ rows of forecast data; one query for 24 hours = 24 records.

## Authentication

API key in `key` query parameter or `X-Api-Key` header.

## Endpoints

- **Base URL:** `https://weather.visualcrossing.com/VisualCrossingWebServices/rest/services/timeline/`
- **Key endpoints:**
  - `GET /timeline/{location}/{date1}/{date2}` — Timeline Weather (forecast + historical)
  - `GET /timeline/{location}` — current + 15-day forecast
  - **Timeline LLX API** — ultra-low latency variant
  - **Weather Maps API** — visualization tiles
  - **Historical Forecast API**

## Example call

```bash
curl "https://weather.visualcrossing.com/VisualCrossingWebServices/rest/services/timeline/1.290,103.851/next7days?include=hours&elements=waveheight,swell,windspeed,temp&key=$VC_KEY&unitGroup=metric&contentType=json"
```

## Rate limits

Per-day record cap (1,000 free tier → unlimited Corporate). No specific per-second limit published.

## SDKs / Libraries

- **Official:** Python, JavaScript, Java, R, Power BI, Excel add-ins.
- **Community:** Multiple wrappers; popular in the data analyst community.

## Documentation

- Weather API: https://www.visualcrossing.com/weather-api
- Timeline API docs: https://www.visualcrossing.com/resources/documentation/weather-api/timeline-weather-api/
- Marine fields: https://www.visualcrossing.com/resources/documentation/weather-data/weather-data-documentation/

## Notes

- Free tier permits commercial use — rare among weather APIs and a real differentiator.
- For Strait-of-Malacca volume (e.g., hourly forecast for 10 anchorages × 7 days = 1,680 records/day) you'll exceed the free tier and tip into metered ($0.17/day) — still very cheap.
- Quality on marine fields is workmanlike rather than best-in-class; for high-stakes routing decisions pair with Stormglass or Meteomatics.
