# NOAA / National Weather Service API

Free U.S. government weather API providing forecasts, alerts, and observations. Native marine forecast products (Coastal Waters Forecast, Offshore Waters Forecast, High Seas Forecast) cover the western Pacific including the South China Sea — adjacent to but not centered on the Strait of Malacca.

**Tier:** Free
**Auth:** None (User-Agent header required)
**Last researched:** 2026-05-09

## Use cases

- High Seas Forecasts and offshore-waters bulletins covering portions of the western Pacific approaches to the Strait.
- General weather context for U.S.-flagged vessels operating in the region.
- No-cost backup feed alongside paid commercial APIs (Stormglass, Tomorrow.io, Meteomatics).
- Tropical cyclone advisories from the National Hurricane Center / Joint Typhoon Warning Center (JTWC) — relevant for vessels in seasonal storm tracks.
- Free tile and GeoJSON layers for analyst dashboards.

## Pricing

- **Free tier:** Fully free; no API key required.
- **Paid tiers:** None.
- **Enterprise:** Not applicable.
- **Notes:** Use is unrestricted within reasonable rate limits. Caching encouraged.

## Authentication

No API key required. The API enforces a `User-Agent` header that should identify the requesting application and (ideally) a contact email — e.g., `User-Agent: malacca-monitor/1.0 (ops@example.com)`.

## Endpoints

- **Base URL:** `https://api.weather.gov`
- **Key endpoints:**
  - `GET /points/{lat},{lon}` — forecast office and grid coordinates lookup
  - `GET /gridpoints/{office}/{x},{y}/forecast` — 12-hour forecast
  - `GET /gridpoints/{office}/{x},{y}/forecast/hourly` — hourly forecast
  - `GET /alerts/active?area={state}` — active alerts
  - `GET /products/types/HSF` — High Seas Forecast text products

## Example call

```bash
curl -H "User-Agent: malacca-monitor (ops@example.com)" \
  "https://api.weather.gov/products/types/HSF"
```

## Rate limits

"Generous" — exact numbers not published. Excessive requests trigger temporary throttling that resolves in ~5 seconds.

## SDKs / Libraries

- **Official:** None.
- **Community:** `noaa-sdk` (Node.js), `pynws`, others on GitHub.

## Documentation

- API documentation: https://www.weather.gov/documentation/services-web-api
- Specification (GitHub): https://weather-gov.github.io/api/
- Operational contact: nco.ops@noaa.gov

## Notes

- NWS coverage is **U.S.-centric**. The Strait of Malacca is **outside** NWS coastal/offshore zones — only the High Seas Forecast (HSF) products and tropical advisories are relevant.
- For genuine Strait-area coverage, pair with a global model API (Stormglass, Tomorrow.io, Open-Meteo, Meteomatics).
- All response formats supported: GeoJSON, JSON-LD, DWML (NWS-specific), CAP, ATOM XML.
