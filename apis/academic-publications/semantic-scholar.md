# Semantic Scholar Academic Graph API

AI-powered academic paper search and recommendation API from the Allen Institute for AI, covering 200+ million papers across all disciplines with citation graphs, author profiles, and influence metrics.

**Tier:** Freemium
**Auth:** API Key
**Last researched:** 2026-05-13

## Use cases

- Searching papers by relevance using Semantic Scholar's AI-enhanced ranking (beyond simple keyword matching)
- Retrieving citation and reference graphs for research genealogy and influence analysis
- Bulk harvesting paper metadata, abstracts, and open-access PDF links via the bulk search endpoint

## Pricing

- **Free tier:** 5,000 requests/5 minutes (shared unauthenticated pool); dedicated 1 RPS with free API key
- **Paid tiers:** None — higher rate limits negotiable by contacting the S2 team for qualifying research use cases
- **Enterprise:** N/A
- **Notes:** API keys are free. Unauthenticated pool rate is shared across all anonymous users and can be throttled under heavy load — always use an API key.

## Authentication

Request a free API key at https://www.semanticscholar.org/product/api (key delivered by email). Pass as `x-api-key: <KEY>` header or `&api_key=<KEY>` query parameter.

## Endpoints

- **Base URL:** `https://api.semanticscholar.org/graph/v1/`
- **Key endpoints:**
  - `GET /paper/search` — relevance-ranked paper search; params: `query`, `fields`, `limit`, `offset`
  - `GET /paper/search/bulk` — bulk paper search (preferred for large queries); params: `query`, `fields`, `sort`, `limit`, `token` (cursor)
  - `GET /paper/{id}` — single paper by S2 ID, DOI (`DOI:`), arXiv ID (`ARXIV:`), or PMID (`PMID:`)
  - `GET /paper/{id}/citations` — papers that cite this paper
  - `GET /paper/{id}/references` — papers cited by this paper
  - `GET /author/{id}` — author profile with citation counts and h-index
  - `GET /author/search` — author name search
  - `GET /recommendations/v1/papers` — paper recommendations seeded from a list of paper IDs

**Useful `fields` values:** `title`, `abstract`, `year`, `authors`, `externalIds`, `openAccessPdf`, `citationCount`, `influentialCitationCount`, `publicationTypes`, `publicationDate`, `journal`

## Example call

```bash
curl -H "x-api-key: $S2_API_KEY" \
  "https://api.semanticscholar.org/graph/v1/paper/search/bulk?query=mixture+of+experts&fields=title,year,citationCount,openAccessPdf&sort=citationCount:desc"
```

```python
import semanticscholar

sch = semanticscholar.SemanticScholar(api_key=S2_API_KEY)
results = sch.search_paper(
    "mixture of experts",
    fields=["title", "year", "citationCount", "openAccessPdf"],
)
for paper in results:
    print(paper.title, paper.year, paper.citationCount)
```

## Rate limits

Without API key: 5,000 requests per 5 minutes (shared pool — subject to throttling under load). With free API key: 1 request per second (dedicated). Higher limits negotiable for qualifying research use cases.

## SDKs / Libraries

- **Official:** None — REST API only
- **Community:** `semanticscholar` (Python, PyPI; widely used third-party client); `s2-folks` GitHub org for official usage examples and release notes

## Documentation

- Product page: https://www.semanticscholar.org/product/api
- API reference: https://api.semanticscholar.org/api-docs/
- Tutorial: https://www.semanticscholar.org/product/api/tutorial

## Notes

- The `paper/search/bulk` endpoint is preferred over `paper/search` for any query returning more than a few hundred results — it is significantly less resource-intensive on the server.
- `influentialCitationCount` (highly-cited papers that explicitly build on this work) is a unique Semantic Scholar metric not available in other academic APIs — useful for identifying foundational papers.
- The Datasets API provides bulk snapshots of the full S2 corpus — contact Semantic Scholar for access; preferred for training data or corpus-scale research.
- Paper IDs accept multiple formats with prefixes: `ARXIV:2310.06825`, `DOI:10.1145/3514221`, `PMID:37468389`.
