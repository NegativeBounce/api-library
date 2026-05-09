# Windy API

The same data and rendering engine that powers windy.com, exposed as developer APIs: Point Forecast (raw weather data), Map Forecast (tile-based visualisation), and Webcams. Strong wind, wave, and weather-model coverage popular among sailors.

**Tier:** Freemium
**Auth:** API Key
**Last researched:** 2026-05-09

## Use cases

- Embedding Windy's familiar map UI (with wind, waves, currents, pressure layers) into a Strait of Malacca ops dashboard.
- Point Forecast API for backend integration — wind, waves, currents, temperature, precipitation, plus 20+ parameters.
- Webcams API to surface coastal/port webcams (Strait has decent coverage near Singapore, Penang, Phuket).
- Multiple weather models exposable side-by-side: ECMWF, GFS, NEMS, ICON, GFS-Wave, etc.

## Pricing

- **Free tier:** Free key with limited daily requests (typically 500/day for Map Forecast; lower for Point Forecast). Sign up at api.windy.com.
- **Paid tiers:** Multi-tier pricing scaling with daily requests; published on the per-product pricing pages.
- **Enterprise:** Custom contracts including white-label and high-volume tile serving.
- **Notes:** Webcams API is unrestricted (no rate limit) on the free key.

## Authentication

API key passed as `key` query parameter for Map Forecast and as a body field for Point Forecast.

## Endpoints

- **Base URL:** `https://api.windy.com/api/`
- **Key endpoints:**
  - `POST /point-forecast/v2` — raw forecast at a coordinate (model + parameters in body)
  - **Map Forecast** — JS map embed via `https://api.windy.com/map-forecast/libBoot.js`
  - `GET /webcams/v3/webcams` — webcams discovery + still images

## Example call

```bash
# Point Forecast — significant wave height for a Strait coordinate
curl -X POST "https://api.windy.com/api/point-forecast/v2" \
  -H "Content-Type: application/json" \
  -d '{
    "lat": 1.290,
    "lon": 103.851,
    "model": "gfsWave",
    "parameters": ["waves", "windWaves", "swell1"],
    "key": "'"$WINDY_KEY"'"
  }'
```

## Rate limits

Per-product daily quota; free tier ranges from a few hundred to ~500 requests/day depending on product. Paid tiers scale up.

## SDKs / Libraries

- **Official:** None for Point Forecast; Map Forecast uses a JS bootloader.
- **Community:** Several Node/Python wrappers.

## Documentation

- API site: https://api.windy.com/
- Point Forecast: https://api.windy.com/point-forecast
- Map Forecast: https://api.windy.com/map-forecast
- Webcams: https://api.windy.com/webcams

## Notes

- Models include `gfsWave` (NCEP GFS-Wave) and ECMWF wave — both reasonable for the Strait.
- Map Forecast is the easiest way to get a "Windy-style" UI into your ops dashboard with minimal frontend work.
- Webcams API is a hidden gem for visual confirmation of port conditions (e.g., Singapore, Port Klang area webcams).
