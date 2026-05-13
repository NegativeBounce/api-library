# CORE API

Aggregated open-access research paper API providing real-time access to metadata and full text from 15,000+ data providers across 150+ countries, with 449 million searchable papers and 57 million full texts.

**Tier:** Freemium
**Auth:** API Key
**Last researched:** 2026-05-13

## Use cases

- Retrieving full-text PDFs and metadata for open-access papers across all disciplines
- Building large-scale text mining pipelines on open-access scientific literature
- Searching across aggregated content from institutional repositories, journals, and preprint servers

## Pricing

- **Free tier:** Unregistered access — lower rate limits, no API key required
- **Paid tiers:**
  - Registered (free): API key issued; 1 batch or 5 single requests per 10 seconds
  - Supporting/Sustaining Member: faster rates included as member benefit
  - VIP Rate: premium throughput available on request
- **Enterprise:** Custom 30-day free trial for institutions; contact CORE for eligibility
- **Notes:** Commercial use is permitted under CORE's Terms & Conditions. Rate tiers are request-count based, not subscription priced.

## Authentication

Register at https://core.ac.uk/services/api to obtain a free API key. Pass as `Authorization: Bearer <API_KEY>` header or `?api_key=<API_KEY>` query parameter.

## Endpoints

- **Base URL:** `https://api.core.ac.uk/v3/`
- **Key endpoints:**
  - `GET /search/works` — full-text search across all CORE works; params: `q`, `limit`, `offset`, `scroll`
  - `GET /works/{id}` — retrieve a specific work by CORE ID
  - `POST /search/works` — batch search with complex query body
  - `GET /outputs/{id}` — retrieve output metadata and full-text link
  - `GET /data-providers` — list indexed data providers

## Example call

```bash
curl -H "Authorization: Bearer $CORE_API_KEY" \
  "https://api.core.ac.uk/v3/search/works?q=transformer+architecture&limit=10"
```

```python
import requests

resp = requests.get(
    "https://api.core.ac.uk/v3/search/works",
    headers={"Authorization": f"Bearer {CORE_API_KEY}"},
    params={"q": "transformer architecture", "limit": 10},
)
for work in resp.json()["results"]:
    print(work["title"], work.get("downloadUrl"))
```

## Rate limits

Unregistered: throttled below 5 single requests per 10 seconds. Registered (free API key): 1 batch request or 5 single requests per 10 seconds. VIP tier: higher throughput available on request.

## SDKs / Libraries

- **Official:** None — REST API only; R client via rOpenSci
- **Community:** SDKs on GitHub under the `oacore` organization

## Documentation

- Main docs: https://core.ac.uk/services/api
- API reference: https://api.core.ac.uk/docs/v3

## Notes

- CORE aggregates content from institutional repositories (via OAI-PMH) and direct publisher partnerships — coverage is strongest for open-access content and weakest for subscription-only journals.
- The `downloadUrl` field in search results provides direct links to full-text PDFs where available; not all records include full text.
- For large-scale harvesting, CORE offers dataset snapshots — preferred over iterative API calls for corpus-scale ingestion.
- CORE is a not-for-profit operated by the Open University (UK); data is free for non-commercial and research use.
