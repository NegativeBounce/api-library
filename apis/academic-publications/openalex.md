# OpenAlex API

Fully open catalog of the global research system providing structured data on 250+ million scholarly works, authors, institutions, journals, and funding sources via a unified REST API.

**Tier:** Freemium
**Auth:** API Key
**Last researched:** 2026-05-13

## Use cases

- Building literature discovery and recommendation systems across all academic disciplines
- Analyzing citation networks, author collaborations, and institutional research output
- Replacing or supplementing Scopus/Web of Science for bibliometric analysis at no cost

## Pricing

- **Free tier:** $1/day in free API usage per key; 100,000 calls/day; 10 req/sec
- **Paid tiers:** Usage-based plans for higher daily limits, monthly database snapshots, and daily change files — contact sales@openalex.org
- **Enterprise:** N/A (usage-based pricing scales to any volume)
- **Notes:** API keys became required in February 2026. Free tier covers most research and prototyping use cases. Quarterly database snapshots are available at no cost.

## Authentication

Create a free account at https://openalex.org/settings/api to obtain an API key. Pass as `?api_key=<KEY>` query parameter or `Authorization: Bearer <KEY>` header. The previously supported `mailto=` polite pool parameter is being phased out in favor of API keys.

## Endpoints

- **Base URL:** `https://api.openalex.org/`
- **Key endpoints:**
  - `GET /works` — search and filter scholarly works; supports full-text search, field filters, grouping, and sorting
  - `GET /works/{id}` — single work by OpenAlex ID, DOI, arXiv ID, or PubMed ID
  - `GET /authors` — search authors by name, ORCID, or affiliation
  - `GET /authors/{id}` — single author record with works count and citation metrics
  - `GET /sources` — journals, repositories, and conference series
  - `GET /institutions` — universities, labs, and research organizations (ROR-linked)
  - `GET /topics` — subject topic taxonomy derived from paper clusters
  - `GET /funders` — funding organizations (Crossref Funder Registry linked)

**Common filter/sort patterns:** `filter=publication_year:2024,type:article,open_access.is_oa:true`, `sort=cited_by_count:desc`, `group_by=publication_year`

## Example call

```bash
curl "https://api.openalex.org/works?search=large+language+model&filter=publication_year:2024,open_access.is_oa:true&sort=cited_by_count:desc&per-page=25&api_key=$OPENALEX_API_KEY"
```

```python
import requests

resp = requests.get(
    "https://api.openalex.org/works",
    params={
        "search": "large language model",
        "filter": "publication_year:2024,open_access.is_oa:true",
        "sort": "cited_by_count:desc",
        "per-page": 25,
        "api_key": OPENALEX_API_KEY,
    },
)
for work in resp.json()["results"]:
    print(work["title"], work["doi"], work["cited_by_count"])
```

## Rate limits

100,000 calls/day; 10 requests/second. Free tier: $1/day equivalent usage. Use cursor-based pagination (`cursor=*`) for efficient deep traversal of large result sets.

## SDKs / Libraries

- **Official:** None — REST API only
- **Community:** `pyalex` (Python); `openalexR` (R); `openalex-js` (JavaScript)

## Documentation

- Main docs: https://docs.openalex.org
- Developer portal: https://developers.openalex.org
- Pricing: https://help.openalex.org/hc/en-us/articles/24397762024087-Pricing

## Notes

- OpenAlex is the open-source successor to Microsoft Academic Graph (MAG), discontinued in 2021. It is operated by OurResearch (non-profit), the same organization behind Unpaywall.
- Coverage is approximately twice that of Scopus and Web of Science by record count, with significantly better coverage of non-English and Global South publications.
- Monthly snapshots and daily change files require a paid plan; quarterly snapshots are free.
- Works include preprints (arXiv, bioRxiv, etc.) alongside peer-reviewed publications — use `type:preprint` filter to distinguish.
- OpenAlex IDs are stable and persistent (e.g., `https://openalex.org/W2741809807`); DOI, PMID, and arXiv ID are also accepted as lookup identifiers.
