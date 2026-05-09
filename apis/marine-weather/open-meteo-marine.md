# Open-Meteo Marine

Free open-source marine weather API exposing wave, swell, ocean current, and sea-surface fields from multiple global models (ECMWF, NCEP GFS, MeteoFrance, DWD). Free for non-commercial use; commercial tier available via separate `customer-` host.

**Tier:** Freemium (Free non-commercial; Paid commercial)
**Auth:** None for non-commercial; API Key for commercial
**Last researched:** 2026-05-09

## Use cases

- Lightweight, free wave/swell/current forecasts for the Strait of Malacca for research, prototyping, and non-commercial ops.
- Backup feed for cross-validation against Stormglass / Tomorrow.io / Meteomatics — same source models, different aggregation.
- Self-hosted option (Docker images) for organisations that want air-gapped weather data.
- Multiple format outputs: JSON, CSV, XLSX (useful for analyst spreadsheets).

## Pricing

- **Free tier:** Free for non-commercial use, no API key, no signup.
- **Paid tiers:** Commercial plans starting around €29/month (varies by request volume); use the `customer-marine-api.open-meteo.com` host.
- **Enterprise:** Self-hosting and custom contracts available.
- **Notes:** Open-source under AGPL — strong choice if licensing transparency matters.

## Authentication

- **Non-commercial:** None.
- **Commercial:** `apikey` query parameter against the `customer-` host.

## Endpoints

- **Base URL (free):** `https://marine-api.open-meteo.com/v1/marine`
- **Base URL (commercial):** `https://customer-marine-api.open-meteo.com/v1/marine`
- **Parameters:**
  - `latitude`, `longitude` (required)
  - `hourly` / `daily` / `current` — variables list
  - `forecast_days` (0–8), `past_days` (0–92)
  - `timezone`, `length_unit`
- **Variables:** `wave_height`, `wave_direction`, `wave_period`, `wave_peak_period`, `wind_wave_height`, `swell_wave_height`, `ocean_current_velocity`, `ocean_current_direction`, `sea_surface_temperature`, `sea_level_height_msl`.

## Example call

```bash
curl "https://marine-api.open-meteo.com/v1/marine?latitude=1.290&longitude=103.851&hourly=wave_height,swell_wave_height,ocean_current_velocity&timezone=Asia%2FSingapore"
```

## Rate limits

Not explicitly published for free tier; reasonable use enforced. Commercial tier scales with subscription.

## SDKs / Libraries

- **Official:** Python (`openmeteo-requests`), Node, R clients on GitHub.
- **Community:** Multiple wrappers across languages.

## Documentation

- Marine API docs: https://open-meteo.com/en/docs/marine-weather-api
- Pricing: https://open-meteo.com/en/pricing
- Source code: https://github.com/open-meteo/open-meteo

## Notes

- Best free option if your organisation qualifies as non-commercial.
- 15-minute resolution available in select regions; check coverage map for the Strait.
- Updates run every 6–12 hours depending on the underlying model.
