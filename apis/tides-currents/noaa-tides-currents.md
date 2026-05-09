# NOAA CO-OPS Tides & Currents

Free U.S. government API providing water-level observations and predictions, current observations and predictions, met data, and operational forecast guidance. Coverage is U.S.-centric (CONUS, Alaska, Hawaii, Pacific territories, Caribbean), so it has **limited Strait-of-Malacca relevance** but is the gold-standard reference for tidal-prediction methodology.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-09

## Use cases

- Reference implementation and methodology (harmonic constants, tidal predictions) — useful when validating tide algorithms used elsewhere.
- Coverage of U.S. Pacific territories adjacent to long-distance Strait routes (Hawaii, Guam) for trans-Pacific voyage planning.
- Free reference dataset for tidal-current methodology learning and oceanographic R&D.
- Met-ocean data (wind, water temperature, atmospheric pressure) at U.S. tide stations.
- Operational Forecast System (OFS) water-level guidance for U.S. ports.

## Pricing

- **Free tier:** Fully free. No API key required.
- **Paid tiers:** None.
- **Enterprise:** Not applicable.
- **Notes:** Caching strongly encouraged — the free service throttles aggressive use.

## Authentication

None. Self-throttling via "sleep statements" between successive calls is the documented best practice.

## Endpoints

- **Base URL:** `https://api.tidesandcurrents.noaa.gov/api/prod/`
- **Key endpoints:**
  - `GET /datagetter` — primary data endpoint (water level, currents, met)
  - `GET /metadata` (mdapi) — station metadata, bin numbers
  - **Products:** water_level, predictions, hourly_height, high_low, currents, currents_predictions, wind, air_pressure, water_temperature, etc.
  - **Output formats:** JSON, XML, CSV.

## Example call

```bash
# Honolulu Harbor (1612340) — predicted tides for next 7 days, hourly
curl "https://api.tidesandcurrents.noaa.gov/api/prod/datagetter?product=predictions&application=malacca-monitor&begin_date=20260509&range=168&datum=MLLW&station=1612340&time_zone=GMT&units=metric&format=json"
```

## Rate limits

Throttled during heavy load. NOAA recommends pacing requests with sleep statements; bulk pulls should be cached.

## SDKs / Libraries

- **Official:** None.
- **Community:** `noaa-coops` (Python), various R packages.

## Documentation

- API docs: https://api.tidesandcurrents.noaa.gov/api/prod/
- CO-OPS home: https://tidesandcurrents.noaa.gov/
- Contact: co-ops.userservices@noaa.gov

## Notes

- **Limited coverage of the Strait of Malacca itself.** This entry is in the catalog as a reference standard and for U.S. Pacific operations adjacent to Strait-relevant routes — not as a primary feed for the Strait.
- For Strait-area tide data, prefer WorldTides, Stormglass Tide, or scrape-from-official sources (Indonesia BIG/BMKG, Malaysia Marine Department, Singapore MPA).
- The harmonic-constants methodology used by CO-OPS is the basis for most other tidal-prediction APIs — if you're building your own model, this is the reference.
