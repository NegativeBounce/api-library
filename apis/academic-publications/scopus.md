# Scopus API (Elsevier)

Elsevier's Scopus abstract and citation database API providing search, retrieval, and citation analytics across 78+ million records from peer-reviewed journals, books, and conference proceedings.

**Tier:** Freemium
**Auth:** API Key + Institutional IP or Token
**Last researched:** 2026-05-13

## Use cases

- Searching abstracts and citation data across all scientific disciplines
- Retrieving author profiles, affiliation records, and citation counts for bibliometric analysis
- Building literature review pipelines with rich metadata including funding, keywords, and subject classifications

## Pricing

- **Free tier:** Free for non-commercial use by researchers at academic, public sector, and charitable institutions (requires active institutional Scopus subscription)
- **Paid tiers:** Commercial use requires a separate API license — contact Elsevier sales
- **Enterprise:** Institutional API licenses bundled with Scopus subscriptions
- **Notes:** API access alone does not grant Scopus database access — an active Scopus subscription is required. Rate quota resets every 7 days.

## Authentication

Obtain an API key from https://dev.elsevier.com. Requests must originate from an institutional IP address, or use an Institutional Token for remote access. Pass API key as `?apiKey=<KEY>` query parameter or `X-ELS-APIKey` header. Remote access uses the `X-ELS-Insttoken` header with the Institutional Token.

## Endpoints

- **Base URL:** `https://api.elsevier.com/content/`
- **Key endpoints:**
  - `GET /search/scopus` — full-text search; params: `query` (Scopus query syntax), `start`, `count`, `sort`, `field`, `date`
  - `GET /abstract/scopus_id/{id}` — abstract retrieval by Scopus EID
  - `GET /abstract/doi/{doi}` — abstract retrieval by DOI
  - `GET /abstract/pubmed_id/{pmid}` — abstract retrieval by PubMed ID
  - `GET /author/author_id/{id}` — author profile with metrics and publication list
  - `GET /affiliation/affiliation_id/{id}` — institutional affiliation record

**Scopus query syntax examples:** `TITLE-ABS-KEY(large language model) AND PUBYEAR > 2023 AND DOCTYPE(ar)`

## Example call

```bash
curl -H "X-ELS-APIKey: $SCOPUS_API_KEY" \
  "https://api.elsevier.com/content/search/scopus?query=TITLE-ABS-KEY(transformer+attention)&count=25&sort=citedby-count"
```

```python
from pybliometrics.scopus import ScopusSearch

results = ScopusSearch("TITLE-ABS-KEY(transformer attention) AND PUBYEAR > 2022")
for r in results.results:
    print(r.title, r.coverDate, r.citedby_count)
```

## Rate limits

20,000 requests per 7-day rolling window per API key. Requests are also subject to institutional-level quotas.

## SDKs / Libraries

- **Official:** None — REST API only
- **Community:** `pybliometrics` (Python; covers Scopus, ScienceDirect, and related Elsevier APIs); `rscopus` (R)

## Documentation

- Developer portal: https://dev.elsevier.com
- Scopus API overview: https://dev.elsevier.com/sc_apis.html
- Getting started guide (PDF): https://dev.elsevier.com/guides/Scopus%20API%20Guide_V1_20230907.pdf

## Notes

- An active Scopus institutional subscription is required — the API key alone does not unlock data access. Contact your institution's library to verify eligibility.
- The Scopus query language uses field codes: `TITLE-ABS-KEY`, `AUTH`, `AFFIL`, `SRCTITLE`, `PUBYEAR`, `DOCTYPE`. Consult the Scopus field guide before building complex queries.
- `pybliometrics` is the de facto standard Python library and handles authentication, caching, and response parsing — strongly recommended over raw REST calls.
- Scopus citation counts are updated daily and may differ from Web of Science due to differing source coverage.
- For researchers without institutional Scopus access, OpenAlex (`openalex.md`) provides comparable coverage at no cost.
