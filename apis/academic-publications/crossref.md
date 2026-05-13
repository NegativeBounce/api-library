# Crossref REST API

Metadata API for 140+ million scholarly works registered with Crossref DOIs, including bibliographic data, funding information, license terms, ORCID author identifiers, and citation counts.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-13

## Use cases

- Resolving DOIs to full bibliographic metadata (authors, journal, volume, issue, pages, license)
- Bulk harvesting of publication metadata by date range for literature monitoring pipelines
- Enriching internal datasets with open citation data via the `/works/{doi}` endpoint

## Pricing

- **Free tier:** Unlimited; no registration required
- **Paid tiers:** None
- **Enterprise:** N/A
- **Notes:** Almost all metadata is not subject to copyright and may be used for any purpose. Some abstracts deposited by publishers are copyrighted — check the `license` field in the response. Crossref Metadata Plus (paid) offers enhanced SLA and richer fields for publishers and data vendors.

## Authentication

No authentication required. Include `mailto=your@email.com` as a query parameter or in the `User-Agent` header to join the "polite pool" for more consistent performance.

## Endpoints

- **Base URL:** `https://api.crossref.org/`
- **Key endpoints:**
  - `GET /works` — paginated list of all works; supports filtering, sorting, and field projection
  - `GET /works/{doi}` — single metadata record for a specific DOI
  - `GET /works/{doi}/agency` — registration agency for a DOI
  - `GET /journals` — journals with Crossref-registered content
  - `GET /journals/{issn}/works` — works from a specific journal
  - `GET /members` — member organizations that registered metadata
  - `GET /funders` — funders in the Open Funder Registry
  - `GET /types` — work type taxonomy

**Common filter parameters for `/works`:** `from-pub-date`, `until-pub-date`, `type`, `has-full-text`, `has-orcid`, `member`

## Example call

```bash
curl "https://api.crossref.org/works?query=large+language+model&filter=from-pub-date:2025-01-01&rows=20&mailto=you@example.com"
```

```python
import requests

resp = requests.get(
    "https://api.crossref.org/works",
    params={
        "query": "large language model",
        "filter": "from-pub-date:2025-01-01",
        "rows": 20,
        "mailto": "you@example.com",
    },
)
for item in resp.json()["message"]["items"]:
    print(item.get("title", [None])[0], item.get("DOI"))
```

## Rate limits

Polite pool (with `mailto`): 50 requests per second per IP. Requests exceeding this are blocked for 10 seconds. Rate limit values are returned in response headers `x-rate-limit-limit` and `x-rate-limit-interval`. Revised limits took effect December 1, 2025.

## SDKs / Libraries

- **Official:** None — REST API only
- **Community:** `habanero` (Python); `rcrossref` (R); `serrano` (Ruby); `crossref-commons` (Python, maintained by Crossref)

## Documentation

- Main docs: https://www.crossref.org/documentation/retrieve-metadata/rest-api/
- API reference: https://github.com/CrossRef/rest-api-doc
- Access and auth: https://www.crossref.org/documentation/retrieve-metadata/rest-api/access-and-authentication/

## Notes

- Crossref does not hold full-text content — it stores metadata and DOI resolution links only. For full text, combine with Unpaywall (`unpaywall.md`) to find open-access versions.
- The `cursor` parameter enables efficient deep pagination through large result sets — prefer it over `offset` for traversing more than 10,000 records.
- OpenCitations (https://opencitations.net) provides an open citation graph derived in part from Crossref deposits, useful for citation network analysis.
- Crossref Metadata Plus (paid) offers enhanced SLA, richer metadata fields, and higher throughput — aimed at publishers and data vendors rather than researchers.
