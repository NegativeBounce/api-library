# UK Police Data API

The UK Police open data API providing street-level crime records, stop-and-search data, and force information for England, Wales, and Northern Ireland — searchable by geographic coordinates and month.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-13

## Use cases

- Querying crime incident data near UK ports and coastal areas (Dover, Southampton, Liverpool, Hull)
- Monitoring crime trends at specific port coordinates over rolling monthly windows
- Cross-referencing port-adjacent crime categories (drug offences, theft, violent crime) with vessel schedules

## Pricing

- **Free tier:** Unlimited; no registration required
- **Paid tiers:** None
- **Enterprise:** N/A
- **Notes:** Public government open data. No SLA or real-time guarantee — data is typically 2–3 months behind the current date.

## Authentication

No authentication required. All endpoints are publicly accessible.

## Endpoints

- **Base URL:** `https://data.police.uk/api/`
- **Key endpoints:**
  - `GET /crimes-street/all-crime` — street-level crimes near a coordinate; params: `lat`, `lng`, `date` (YYYY-MM)
  - `GET /crimes-street/{crime-category}` — crimes of a specific category; replace `{crime-category}` with slug (e.g., `drugs`, `theft-from-the-person`, `violent-crime`)
  - `GET /crime-categories` — list all available crime category slugs for a given month
  - `GET /forces` — list all police forces with their slugs
  - `GET /stops-street` — stop-and-search records near a coordinate

**Coastal/port-relevant police forces:**
  - `kent` — covers Dover Strait, Port of Dover, Folkestone
  - `hampshire` — covers Port of Southampton, Portsmouth Naval Base
  - `humberside` — covers Port of Immingham, Port of Hull
  - `merseyside` — covers Port of Liverpool, Birkenhead

## Example call

```bash
# Crimes within 1 mile of Port of Dover in March 2025
curl "https://data.police.uk/api/crimes-street/all-crime?lat=51.1279&lng=1.3134&date=2025-03"
```

```python
import requests

resp = requests.get(
    "https://data.police.uk/api/crimes-street/all-crime",
    params={"lat": 51.1279, "lng": 1.3134, "date": "2025-03"}
)
crimes = resp.json()
for crime in crimes:
    print(crime["category"], crime["location"]["street"]["name"])
```

## Rate limits

Not published. The API is unmetered but add delays between requests for bulk coordinate queries to avoid server-side throttling.

## SDKs / Libraries

- **Official:** None — REST API only
- **Community:** `ukpolice` (Python PyPI package); `ukcrime` (R package); various GitHub wrappers

## Documentation

- API documentation: https://data.police.uk/docs/
- Data methodology: https://data.police.uk/about/

## Notes

- **Coverage:** England, Wales, and Northern Ireland only. Scotland is NOT covered — Police Scotland does not participate in this data sharing initiative.
- **Latency:** Data is typically published 2–3 months behind the current date. This API is not suitable for real-time incident monitoring; use it for trend analysis and baseline threat profiling.
- **Polygon queries:** The API supports custom geographic polygon queries via POST to `/crimes-street/all-crime` with a `poly` parameter (list of lat/lng pairs) — useful for querying irregular port perimeters.
- Maximum polygon area is approximately 1 square mile (larger areas return a 503 error).
- Drug offences, theft, and violent crime categories are most relevant for port security threat monitoring.
