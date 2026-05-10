# Umbra

US-based commercial Synthetic Aperture Radar (SAR) constellation operator (Santa Barbara, CA). Primarily a SAR data provider — 25 cm spotlight imagery as the headline product — but the X-band SAR payload is also capable of passive RF/SIGINT scanning, and Umbra was one of the original six NRO Strategic Commercial Enhancements BAA RF awardees in 2022. Cataloged under RF Intelligence Feeds for the SIGINT-adjacent capability; primary SAR usage may also warrant a future `satellite-imagery` cross-listing.

**Tier:** Paid (commercial SAR + RF) / Free Open Data Program for select locations
**Auth:** Bearer token (OAuth-style) via Canopy
**Last researched:** 2026-05-10

## Use cases

- All-weather, day/night SAR imagery (25 cm Spotlight, Extended Dwell modes)
- Passive RF/SIGINT scanning from X-band payload (per NRO BAA Phase 3 evaluation)
- Self-service tasking via Canopy API/UI — no human in the loop required
- STAC-compliant archive search by AOI, time, resolution, polarization
- Direct delivery of SAR products to customer cloud (S3 etc.)
- Free Open Data for change detection and time-series experimentation across 20+ locations

## Pricing

- **Free tier:** Open Data Program — multi-looked Spotlight collects (GEC, SICD, SIDD, CPHD) over 20+ recurring global locations, weekly cadence, freely usable under Creative Commons (resell/release/remix without royalty).
- **Paid tiers:** Public per-task pricing in the Canopy UI — Umbra explicitly markets "Our pricing information is public" as a value prop. Tasking a Spotlight collect typically priced by mode, resolution, area, and turnaround.
- **Enterprise:** Custom mission-tailored solutions for government and defense ("the world's most urgent missions"). NRO commercial SAR/RF awardee.
- **Notes:** Data licensed under Creative Commons — customers can resell/redistribute without revenue share, unusual in commercial SAR.

## Authentication

Bearer token issued from Canopy account. Used as `Authorization: Bearer <token>` header on all API calls.

## Endpoints

- **Base URL (Canopy API):** `https://api.canopy.umbra.space/`
- **Base URL (docs):** `https://docs.canopy.umbra.space/`
- **Key endpoints:**
  - `GET /v2/stac/collections/umbra-sar/items/{id}` — single STAC item lookup
  - `POST /archive/search` — STAC-API-compliant search of the archive (CQL2 filters supported)
  - Tasking endpoints — feasibility, task creation, schedule check, real-time updates
  - Get Collect — fetch a `umbra:collect_id` and its assets
  - Get Schema — STAC schema introspection

## Example call

```bash
# Search the archive by datetime range
curl -X POST 'https://api.canopy.umbra.space/archive/search' \
  -H "Authorization: Bearer $UMBRA_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"limit": 10, "datetime": "2026-05-01T00:00:00Z/2026-05-10T00:00:00Z"}'

# Search by 1-meter range resolution using CQL2
curl -X POST 'https://api.canopy.umbra.space/archive/search' \
  -H "Authorization: Bearer $UMBRA_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "limit": 10,
    "filter-lang": "cql2-json",
    "filter": {"op": "=", "args": [{"property": "sar:resolution_range"}, 1]}
  }'

# Fetch a specific STAC item
curl 'https://api.canopy.umbra.space/v2/stac/collections/umbra-sar/items/d395379e-5184-4aaa-9300-2a9725c593f3' \
  -H "Authorization: Bearer $UMBRA_TOKEN"
```

```python
import requests
HEADERS = {"Authorization": f"Bearer {UMBRA_TOKEN}", "Content-Type": "application/json"}
r = requests.post(
    "https://api.canopy.umbra.space/archive/search",
    headers=HEADERS,
    json={
        "limit": 5,
        "datetime": "2026-05-01T00:00:00Z/2026-05-10T00:00:00Z",
        "intersects": {"type": "Point", "coordinates": [-74.0, 40.7]},  # NYC
    },
)
for item in r.json().get("features", []):
    print(item["id"], item["properties"]["umbra:collect_id"], item["properties"]["sar:instrument_mode"])
```

## Rate limits

Tasking subject to satellite schedule and customer subscription. STAC archive search has no published per-account rate limit but expects reasonable use. Open Data Program is rate-limit-light by virtue of being pre-rendered downloads.

## SDKs / Libraries

- **Official:** Canopy web UI; OpenAPI / STAC-API standard endpoints (any STAC client works).
- **Community:**
  - `pystac-client` (Python — works against any STAC API including Umbra)
  - `stac-fastapi` reference impls
  - SAR-specific tooling: SNAP, ISCE, OpenSARToolkit (post-processing)

## Documentation

- Project home: https://umbra.space/
- Open Data Program: https://umbra.space/open-data/
- Canopy docs (intro): https://docs.canopy.umbra.space/docs/introduction
- STAC API v2 migration guide: https://docs.canopy.umbra.space/docs/migrate-to-stac-api-v2
- Archive search via STAC API: https://docs.canopy.umbra.space/docs/archive-catalog-searching-via-stac-api
- API reference (Get Collect): https://docs.canopy.umbra.space/reference/get_collect
- eoPortal mission profile: https://www.eoportal.org/satellite-missions/umbra-sar
- NASA CSDA program (US Government access): https://science.nasa.gov/?p=884532

## Notes

- Constellation goal: 32 SAR sensors in LEO. First satellite Umbra-SAR 2001 launched June 2021. Multiple satellites operational by 2026.
- Imaging modes: **Spotlight** (high-res, multi-look) and **Extended Dwell** (long observation of fixed targets — particularly relevant to RF/SIGINT use).
- Polarizations: VV (single-polar) typical for Spotlight.
- Frequency band: X-band.
- Product types: GEC (Geocoded Ellipsoid Corrected), SICD (Sensor Independent Complex Data — CPHD-derived), SIDD (Sensor Independent Derived Data), CPHD (Compensated Phase History Data — useful for advanced research and InSAR).
- **RF/SIGINT capability:** the same X-band payload "can also be utilized to passively scan for RF activity" (per Gunter's Space Page mission notes). NRO awarded Umbra a 2022 Commercial RF BAA contract option alongside HawkEye 360, Kleos, Aurora Insight, Spire, and PredaSAR — so this is a real (if secondary) commercial offering.
- Open Data Program is the most permissive licensing among major commercial SAR providers — output usable in derivative products without royalty/revenue-share constraints. Useful for prototyping pipelines before paid tasking.
- US Government / federally-funded researcher access is also available via NASA's Commercial Satellite Data Acquisition (CSDA) program.
- Cross-listing: primary SAR capability overlaps `satellite-imagery` (BlackSky, Capella, Planet, Maxar/Vantor); RF capability overlaps the rest of `rf-intelligence-feeds`.
