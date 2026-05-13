# IEEE Xplore API

IEEE's scholarly database API providing metadata search and full-text access across 6+ million engineering, electronics, computer science, and technology documents including journals, conference proceedings, books, and standards.

**Tier:** Freemium
**Auth:** API Key
**Last researched:** 2026-05-13

## Use cases

- Searching IEEE conference and journal papers on specific engineering, CS, or AI topics
- Retrieving metadata and abstracts for papers across IEEE Transactions journals
- Accessing open-access full-text articles programmatically via the Open Access API

## Pricing

- **Free tier:** Metadata Search API — free with registered API key; metadata and abstracts only
- **Paid tiers:**
  - Open Access API — free for IEEE Open Access designated articles; no additional cost beyond API key registration
  - Full-Text Access API — requires IEEE subscription or institutional license; contact IEEE sales
- **Enterprise:** Full-text access bundled into institutional IEEE Xplore subscriptions; contact sales
- **Notes:** API keys are issued during business hours (8am–5pm ET, Mon–Fri). Max 200 results per query across all tiers.

## Authentication

Register an application at https://developer.ieee.org to obtain an API key. Pass as `&apikey=<API_KEY>` query parameter on all requests.

## Endpoints

- **Base URL:** `https://ieeexploreapi.ieee.org/api/v1/`
- **Key endpoints:**
  - `GET /search/articles` — search metadata across all IEEE content; supports keyword, boolean, and field-specific queries
  - `GET /search/articles` with `open_access=True` — filter to open-access full-text articles
  - `GET /search/articles?doi={doi}` — DOI lookup; accepts up to 25 DOIs per request

**Common query parameters:** `querytext`, `newsearch`, `start_record`, `max_records` (max 200), `open_access`, `content_type`, `start_year`, `end_year`, `sort_field`, `sort_order`

## Example call

```bash
curl "https://ieeexploreapi.ieee.org/api/v1/search/articles?querytext=neural+network&max_records=25&start_year=2024&apikey=$IEEE_API_KEY"
```

```python
import requests

resp = requests.get(
    "https://ieeexploreapi.ieee.org/api/v1/search/articles",
    params={
        "querytext": "neural network",
        "max_records": 25,
        "start_year": 2024,
        "apikey": IEEE_API_KEY,
    },
)
for article in resp.json()["articles"]:
    print(article["title"], article["doi"])
```

## Rate limits

Not publicly documented as fixed values. Maximum 200 results per query. Contact IEEE for throughput requirements beyond standard usage.

## SDKs / Libraries

- **Official:** None — REST API only
- **Community:** `ieee-xplore` (Python, third-party); `arcas` (Python multi-source academic search library)

## Documentation

- Developer portal: https://developer.ieee.org
- Getting started: https://developer.ieee.org/getting_started
- API docs: https://developer.ieee.org/docs

## Notes

- The Metadata Search API returns abstracts and bibliographic data only — not full text. Full text requires the Open Access API (for OA papers) or Full-Text Access API (subscription required).
- Boolean search is supported via `querytext` with `AND`, `OR`, `NOT` operators and field qualifiers (e.g., `"neural network" AND Article_Title:transformer`).
- IEEE standards documents (IEEE Std) are included in the index — useful for regulatory and compliance research.
- The DOI lookup accepts up to 25 DOIs in a single request for efficient batch metadata retrieval.
