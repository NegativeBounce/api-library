# Stormglass

Marine weather API aggregating wind, wave, current, tide, and astronomical data from major global models (NOAA, ECMWF, Météo France, Met Office, DWD) — explicitly built for sailing, shipping, and offshore operations.

**Tier:** Freemium
**Auth:** API Key (Authorization header)
**Last researched:** 2026-05-09

## Use cases

- Marine forecasts (wave height/period, swell, wind, currents) for vessels in the Strait of Malacca and approaches.
- Pre-voyage routing decisions — Stormglass exposes 10+ source models with a "best of" `sg` ensemble option.
- Tide predictions at any global coastal point (also see Tides & Currents category).
- Astronomy data (sunrise/sunset, moon phase) for crew operations and visibility planning.
- Lightweight commercial integration without enterprise procurement (€19–€129/month covers most ops cases).

## Pricing

- **Free tier:** €0/month, 10 requests/day, **non-commercial use only**.
- **Paid tiers:**
  - **Small:** €19/month, 500 req/day.
  - **Medium:** €49/month, 5,000 req/day, commercial use.
  - **Large:** €129/month, 25,000 req/day.
- **Enterprise:** Custom invoicing and SLAs.
- **Notes:** 10% annual discount available. All tiers include all parameters.

## Authentication

API key issued at signup. Sent in the `Authorization` header (without `Bearer` prefix): `Authorization: $API_KEY`.

## Endpoints

- **Base URL:** `https://api.stormglass.io/v2/`
- **Key endpoints:**
  - `GET /weather/point` — point forecast (wind, wave, current, etc.)
  - `GET /tide/sea-level/point` — tide / sea level
  - `GET /tide/extremes/point` — tide highs/lows
  - `GET /astronomy/point` — sunrise/sunset/moonphase
  - `GET /elevation/point`, `/bio/point`, `/solar/point` — auxiliary

## Example call

```bash
curl "https://api.stormglass.io/v2/weather/point?lat=1.290&lng=103.851&params=waveHeight,windSpeed,currentSpeed,seaLevel" \
  -H "Authorization: $STORMGLASS_KEY"
```

## Rate limits

Per-tier daily quota (10/day → 25,000/day). No published per-second limit; quotas reset at UTC midnight.

## SDKs / Libraries

- **Official:** None.
- **Community:** Python, Node, Ruby wrappers on GitHub (low traffic).

## Documentation

- Main site: https://stormglass.io/
- Marine weather: https://stormglass.io/marine-weather-api/
- Docs: https://docs.stormglass.io/

## Notes

- Data sources include NOAA, Météo France, Met Office, ECMWF, DWD, plus an AI ensemble (`sg`) — useful for cross-validation.
- For Strait of Malacca, ECMWF + DWD tend to be best-performing source models; Stormglass exposes per-source values so you can pick.
- Sister product `Tide` API also belongs in the Tides & Currents category — cross-referenced.
