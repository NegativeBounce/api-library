# N2YO.com

Free real-time satellite tracking website with a public REST API for TLEs, predicted positions, visual passes, radio passes, and "what's overhead" queries. Popular among ham radio operators and amateur space enthusiasts.

**Tier:** Free
**Auth:** API license key (free, generated in account profile)
**Last researched:** 2026-05-09

## Use cases

- Predicting visible satellite passes for any location/time (ham, photography, observation)
- Predicting radio passes for amateur satellite QSOs
- Live position queries for any satellite by NORAD ID (incl. ISS, Starlink, weather sats)
- "What's above me right now within X degrees?" overhead queries
- Building dashboards / Home Assistant integrations / Discord bots tracking specific satellites

## Pricing

- **Free tier:** Free with mandatory account + API key. Hard rate limit of 1,000 transactions per hour (combined across endpoints).
- **Paid tiers:** None published.
- **Enterprise:** Contact n2yo.com directly for higher quotas.
- **Notes:** Same key cannot be used for both legacy SOAP and current REST APIs — REST has its own.

## Authentication

Register at n2yo.com → profile page → "Generate API key". The new key is permanent (not changeable). Append it to every request as `&apiKey=YOUR_KEY`.

## Endpoints

- **Base URL:** `https://api.n2yo.com/rest/v1/satellite`
- **Key endpoints:**
  - `GET /tle/{NORAD_ID}` — TLE for a satellite
  - `GET /positions/{NORAD_ID}/{lat}/{lon}/{alt}/{seconds}` — future positions (lat/lon footprints + az/el for observer), 1 sec resolution
  - `GET /visualpasses/{NORAD_ID}/{lat}/{lon}/{alt}/{days}/{min_visibility}` — visual pass predictions
  - `GET /radiopasses/{NORAD_ID}/{lat}/{lon}/{alt}/{days}/{min_elevation}` — radio pass predictions
  - `GET /above/{lat}/{lon}/{alt}/{search_radius}/{category_id}` — all satellites above observer within search radius

## Example call

```bash
# Get current TLE for the ISS (NORAD 25544)
curl "https://api.n2yo.com/rest/v1/satellite/tle/25544&apiKey=$N2YO_KEY"

# Get next 3 days of visual passes from observer at 40.71/-74.00, ≥300 sec visibility
curl "https://api.n2yo.com/rest/v1/satellite/visualpasses/25544/40.71/-74.00/0/3/300&apiKey=$N2YO_KEY"
```

```python
import requests
URL = "https://api.n2yo.com/rest/v1/satellite/positions/25544/40.71/-74.00/0/60"
r = requests.get(URL, params={"apiKey": API_KEY})
print(r.json()["positions"][0])  # First second of calc — current position
```

## Rate limits

1,000 transactions/hour per API key (combined across all endpoints). Exceed and requests return error responses; hammering can lead to key suspension.

## SDKs / Libraries

- **Official:** None.
- **Community:** `facorazza/n2yo-api` (Python), `djtimca/n2yo-api` (Python fork), `dms-codes/n2yo` (Python script), `djtimca/hasatellitetracker` (Home Assistant integration), N2YO MCP server for Claude/AI agents (`MaxwellCalkin/N2YO-MCP`).

## Documentation

- Main site: https://www.n2yo.com/
- API reference: https://www.n2yo.com/api/
- dlt context: https://dlthub.com/context/source/n2yo

## Notes

- Quote-by-NORAD-ID only — there's no name search endpoint; use CelesTrak or Space-Track for resolving names → NORAD IDs.
- Categories supported on `above` endpoint: amateur, GPS, Galileo, GLONASS, BeiDou, weather, military, science, geostationary, Iridium, Starlink, etc.
- The `positions` endpoint returns one element per second — choose `seconds` carefully for large queries (a 3600-sec query is one transaction).
- Cross-listing: complementary to `gnss-interference` (GPS/Galileo/GLONASS/BeiDou orbits), `rf-monitoring` (radio pass scheduling for HF/UHF SDR observation).
