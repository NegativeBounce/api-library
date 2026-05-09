# Meteomatics

Enterprise-grade weather API with 1,800+ parameters covering meteorology, ocean, marine, and environmental fields. Aggregates global, regional, oceanic, and AI-based models. Strong choice for high-precision marine forecasting.

**Tier:** Paid (with free trial)
**Auth:** Basic auth (username + password) or OAuth token
**Last researched:** 2026-05-09

## Use cases

- High-precision marine forecasting — significant wave height, peak wave period, swell, surface currents — for Strait of Malacca operations.
- Routing decisions where multiple model agreement and uncertainty estimates matter.
- Vertical profiles (atmospheric and oceanic) for specialised ops (e.g., ECMWF ocean reanalysis, ROMS-style outputs).
- Long historical archives going back decades for risk/insurance modelling.
- Tailored marine bundles where wave + current + tide are merged into a single API surface.

## Pricing

- **Free tier:** 14-day free trial with up to 1,000 queries.
- **Paid tiers:** Monthly and yearly licenses; pricing tailored by parameter selection, request volume, and access patterns. Not publicly listed.
- **Enterprise:** Custom contracts including on-premise data delivery and source-model licensing.
- **Notes:** Pricing is genuinely sales-led — no self-service signup beyond the trial.

## Authentication

- **Basic auth:** `https://username:password@api.meteomatics.com/...` (works but transmits password in URL — not recommended).
- **OAuth token:** Obtain a 2-hour token via `https://login.meteomatics.com/api/v1/token` using basic auth, then send `Authorization: Bearer <token>` on subsequent calls.

## Endpoints

- **Base URL:** `https://api.meteomatics.com/`
- **URL pattern:** `https://api.meteomatics.com/{validdatetime}/{parameters}/{location}/{format}`
- **Marine parameters:** `significant_wave_height:m`, `wave_period:s`, `mean_wave_direction:d`, `wind_wave_height:m`, `swell_wave_height:m`, `ocean_current_speed:ms`, `sea_surface_temperature:C`, etc.

## Example call

```bash
# Significant wave height for a Strait coordinate, JSON
curl -u "$METEOMATICS_USER:$METEOMATICS_PW" \
  "https://api.meteomatics.com/2026-05-09T00:00:00ZP1D:PT1H/significant_wave_height:m,wind_speed_10m:ms/1.290,103.851/json"
```

## Rate limits

Plan-dependent; enforced as parallel-request and total-query limits per billing period.

## SDKs / Libraries

- **Official:** Python (`meteomatics-python`), MATLAB connector, R wrapper.
- **Community:** Several Node and Java integrations.

## Documentation

- API home: https://www.meteomatics.com/en/api/
- Getting started: https://www.meteomatics.com/en/api/getting-started/
- Marine parameters: https://www.meteomatics.com/en/api/available-parameters/marine-parameters/
- OAuth: https://www.meteomatics.com/en/api/request/api-requests-oauth-authentification/

## Notes

- Of the marine APIs in this category, Meteomatics is the most "model-engineering" friendly — exposes raw parameter codes, multiple models, and physical units in URL.
- Strong fit if you have meteorologists / physical oceanographers in-house.
- For the Strait of Malacca, ECMWF + ECMWF ocean and ROMS-style regional models give the best fidelity.
