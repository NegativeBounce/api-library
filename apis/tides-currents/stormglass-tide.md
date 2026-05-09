# Stormglass Tide

The tide-prediction surface of the Stormglass.io API, providing global sea-level forecasts and high/low tide times via REST. Cross-listed with the Marine Weather category for the broader Stormglass product.

**Tier:** Freemium
**Auth:** API Key (Authorization header)
**Last researched:** 2026-05-09

## Use cases

- Global tide-height forecasts at any lat/lon for the Strait of Malacca, including offshore points without dedicated tide stations.
- High/low tide times for pilotage windows in Strait ports.
- Combined ops: tide + waves + currents + weather in one Stormglass call (vs. stitching multiple APIs).
- Tide-station discovery via `/tide/stations/area` for nearest-station lookups.
- Cost-effective alternative to UK Admiralty when global (not UK-only) coverage is needed.

## Pricing

- **Free tier:** €0/month, 10 requests/day, non-commercial only (shared with the Stormglass Marine Weather API).
- **Paid tiers:**
  - **Small:** €19/month, 500 req/day.
  - **Medium:** €49/month, 5,000 req/day, commercial use.
  - **Large:** €129/month, 25,000 req/day.
- **Enterprise:** Custom contracts.
- **Notes:** Tide endpoints share the same quota as Marine Weather endpoints — no separate Tide-only plan.

## Authentication

API key in `Authorization: $API_KEY` header.

## Endpoints

- **Base URL:** `https://api.stormglass.io/v2/`
- **Key endpoints:**
  - `GET /tide/sea-level/point` — sea-level forecast at lat/lng
  - `GET /tide/extremes/point` — high/low tide times
  - `GET /tide/stations/area` — tide stations within a bounding box

## Example call

```bash
curl "https://api.stormglass.io/v2/tide/extremes/point?lat=1.290&lng=103.851&start=2026-05-09&end=2026-05-16" \
  -H "Authorization: $STORMGLASS_KEY"
```

## Rate limits

Per-day quota inherited from the parent Stormglass plan (10 → 25,000 requests/day).

## SDKs / Libraries

- **Official:** None.
- **Community:** Same Stormglass community wrappers as the Marine Weather entry.

## Documentation

- Tide docs: https://docs.stormglass.io/#/tide
- Global tide product page: https://stormglass.io/global-tide-api/

## Notes

- Cross-listed with the Marine Weather category — a single Stormglass subscription gives you weather, marine, and tide.
- For Strait-area ports, station-based predictions (`/tide/extremes/point`) are typically reasonable; the algorithm interpolates from nearest known stations + harmonic constants.
- Doesn't expose tidal-current data — for that pair with Open-Meteo Marine or Meteomatics.
