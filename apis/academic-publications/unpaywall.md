# Unpaywall API

DOI-lookup API that finds legal open-access versions of academic papers, returning direct links to free full-text PDFs hosted on publisher sites, institutional repositories, and preprint servers.

**Tier:** Free
**Auth:** Email (required as query parameter)
**Last researched:** 2026-05-13

## Use cases

- Resolving paywalled DOIs to free legal full-text PDF links for any paper
- Enriching bibliographic datasets with open-access availability status and OA type
- Building literature pipelines that automatically retrieve full text without subscription costs

## Pricing

- **Free tier:** 100,000 requests/day; no registration required beyond providing an email address
- **Paid tiers:** None
- **Enterprise:** N/A
- **Notes:** For datasets larger than the daily API limit, Unpaywall provides free quarterly database snapshots (~100 GB compressed) covering all records.

## Authentication

No account required. Pass your email address as `?email=<your@email.com>` on every request. This parameter is mandatory — requests without it are rejected.

## Endpoints

- **Base URL:** `https://api.unpaywall.org/v2/`
- **Key endpoints:**
  - `GET /{doi}` — retrieve open-access status and PDF links for a single DOI; param: `email`

**Key response fields:**
  - `is_oa` — boolean; whether any legal OA version exists
  - `oa_status` — `gold`, `hybrid`, `bronze`, `green`, or `closed`
  - `best_oa_location.url_for_pdf` — direct link to the best available free PDF
  - `oa_locations` — array of all known OA locations with source, host type, and URL
  - `doi_url`, `title`, `genre`, `year`, `journal_name`, `publisher`

## Example call

```bash
curl "https://api.unpaywall.org/v2/10.1038/nature12373?email=you@example.com"
```

```python
import requests

doi = "10.1038/nature12373"
resp = requests.get(
    f"https://api.unpaywall.org/v2/{doi}",
    params={"email": "you@example.com"},
)
data = resp.json()
print(data["is_oa"], data.get("best_oa_location", {}).get("url_for_pdf"))
```

## Rate limits

100,000 requests per day. For bulk access beyond this, download the full Unpaywall database snapshot (free quarterly release).

## SDKs / Libraries

- **Official:** None — REST API only
- **Community:** `unpywall` (Python, PyPI); `unpaywall-mcp` (MCP server for LLM integration)

## Documentation

- API docs: https://unpaywall.org/products/api
- Data field reference: https://support.unpaywall.org/support/solutions/articles/44002142311
- Snapshot downloads: https://unpaywall.org/products/snapshot

## Notes

- Unpaywall only finds legal open-access copies — it does not link to Sci-Hub or other unauthorized repositories.
- OA status types: `gold` = published OA in a fully OA journal; `hybrid` = OA in a subscription journal (APC paid); `bronze` = free on publisher site without explicit license; `green` = OA copy in a repository (preprint or accepted manuscript).
- Best used as an enrichment step after DOI resolution via Crossref (`crossref.md`) — look up metadata first, then check Unpaywall for free PDF availability.
- The `best_oa_location` is chosen by Unpaywall's algorithm prioritizing publisher-hosted PDFs over repositories; check `oa_locations` for all available sources.
- Unpaywall is operated by OurResearch (non-profit), the same organization behind OpenAlex (`openalex.md`).
