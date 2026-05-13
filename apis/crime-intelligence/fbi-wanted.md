# FBI Wanted API

The FBI's public REST API for querying the official Most Wanted list, including fugitives, missing persons, terrorism suspects, and persons of interest across all FBI field offices.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-13

## Use cases

- Cross-referencing crew manifests or port visitors against active FBI wanted persons
- Monitoring new fugitive postings from coastal or port-adjacent field offices (e.g., Miami, New York, Houston)
- Building watchlist alerts for wanted subjects associated with drug trafficking or organized crime

## Pricing

- **Free tier:** Unlimited; no registration required
- **Paid tiers:** None
- **Enterprise:** N/A
- **Notes:** Public government data; no SLA or uptime guarantee.

## Authentication

No authentication required. The API is publicly accessible with no API key.

## Endpoints

- **Base URL:** `https://api.fbi.gov/`
- **Key endpoints:**
  - `GET /wanted/v1/list` — paginated list of wanted persons; supports filtering by classification, field office, and status

**Query parameters:**
  - `title` — filter by title/name keyword
  - `field_offices` — filter by FBI field office slug (e.g., `miami`, `new-york`, `houston`)
  - `status` — `na` (active), `captured`, `located`, `recovered`, `deceased`
  - `person_classification` — `Main`, `Victim`, `Accomplice`
  - `page` — page number (default 1)
  - `limit` — results per page (default 20, max 50)
  - `sort_on` — field to sort by (e.g., `publication`)
  - `sort_order` — `asc` or `desc`

## Example call

```bash
curl "https://api.fbi.gov/wanted/v1/list?field_offices=miami&status=na&limit=20"
```

```python
import requests

resp = requests.get(
    "https://api.fbi.gov/wanted/v1/list",
    params={"field_offices": "miami", "status": "na", "limit": 20}
)
for item in resp.json()["items"]:
    print(item["title"], item["modified"])
```

## Rate limits

Not publicly documented. The API is unmetered but may enforce server-side throttling. Add delays (1–2 seconds) between successive requests to avoid being blocked.

## SDKs / Libraries

- **Official:** None — REST API only
- **Community:** Various GitHub wrappers; OpenSanctions ingests FBI Wanted data into its bulk dataset

## Documentation

- API landing page: https://www.fbi.gov/wanted/api
- Interactive explorer: https://api.fbi.gov/

## Notes

- Data covers all FBI wanted categories: fugitives, terrorism, cyber, missing persons, unknown bank robbers, and more. Filter by `person_classification` and `title` to narrow to relevant threat types.
- The `field_offices` parameter accepts lowercase slugs matching FBI field office city names. Coastal offices with high maritime relevance: `miami`, `new-york`, `houston`, `los-angeles`, `seattle`, `new-orleans`.
- Results include photos, charges, physical descriptions, and last known locations where available.
- OpenSanctions (https://opensanctions.org) aggregates FBI Wanted data alongside OFAC, Interpol, and UN sanctions lists for unified watchlist screening.
