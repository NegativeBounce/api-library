# Interpol Notices API

Interpol's public REST API for querying Red Notices (international arrest requests), Yellow Notices (missing persons), and Blue Notices (information requests) issued to member countries' law enforcement agencies.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-13

## Use cases

- Screening crew members or passengers against active Interpol Red Notices for serious crimes
- Monitoring new Red Notices linked to maritime crime, drug trafficking, or organized crime networks
- Cross-referencing vessel-of-interest individuals against Interpol wanted persons data

## Pricing

- **Free tier:** Unlimited; no registration required
- **Paid tiers:** None
- **Enterprise:** N/A
- **Notes:** Public API operated by Interpol. No SLA or guaranteed uptime. OpenSanctions offers a daily-refreshed bulk download as an alternative.

## Authentication

No authentication required. The API is publicly accessible.

## Endpoints

- **Base URL:** `https://ws-public.interpol.int/notices/v1/`
- **Key endpoints:**
  - `GET /red` — paginated list of Red Notices (international arrest warrants); 6,440+ active notices as of 2026-05-13
  - `GET /yellow` — Yellow Notices (missing persons)
  - `GET /blue` — Blue Notices (information requests on criminal methods)

**Query parameters (all notice types):**
  - `nationality` — ISO 3166-1 alpha-2 country code (e.g., `US`, `CN`, `NG`)
  - `ageMin` / `ageMax` — integer age range
  - `sexId` — `M` or `F`
  - `page` — page number (results are paginated, ~20 per page)

**Response fields:**
  - `entity_id` — unique notice identifier
  - `forename`, `name` — subject name
  - `date_of_birth` — in `YYYY/MM/DD` format
  - `nationalities` — array of ISO country codes
  - `_links.self.href` — URL to full notice detail record

## Example call

```bash
curl "https://ws-public.interpol.int/notices/v1/red?nationality=NG&page=1"
```

```python
import requests

resp = requests.get(
    "https://ws-public.interpol.int/notices/v1/red",
    params={"nationality": "NG", "page": 1}
)
data = resp.json()
print(f"Total: {data['total']}")
for notice in data["_embedded"]["notices"]:
    print(notice["name"], notice["forename"], notice["nationalities"])
```

## Rate limits

Not published. API is unmetered but apply standard throttling: add 1–2 second delays between paginated requests to avoid server-side blocking.

## SDKs / Libraries

- **Official:** None — REST API only
- **Community:** OpenSanctions (https://opensanctions.org) publishes a daily bulk Interpol Red Notice dataset in structured JSON/CSV format; suitable for offline watchlist matching

## Documentation

- Interpol Wanted Persons: https://www.interpol.int/en/How-we-work/Notices/Red-Notices/View-Red-Notices
- OpenSanctions bulk data: https://www.opensanctions.org/datasets/interpol_red_notices/

## Notes

- The public API returns a subset of notice data; sensitive fields (exact charges, arrest details) may be redacted in the public record. Full notice detail is accessible via `_links.self.href` per record.
- OpenSanctions aggregates Interpol Red Notices alongside OFAC SDN, EU, UN, and FBI watchlists into a unified dataset — preferred for production watchlist screening pipelines.
- Interpol does not provide a real-time push/webhook mechanism; poll the `/red` endpoint daily or use OpenSanctions daily snapshots for freshness.
- Yellow and Blue Notices are less commonly used for maritime security but `/yellow` can support missing crew investigations.
