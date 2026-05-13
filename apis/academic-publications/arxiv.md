# arXiv API

Open-access preprint repository API for searching and retrieving papers in physics, mathematics, computer science, AI/ML, quantitative biology, economics, and related fields.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-13

## Use cases

- Fetching the latest AI/ML preprints by subject category (cs.AI, cs.LG, stat.ML)
- Building literature monitoring pipelines for new research in specific topic areas
- Retrieving full paper metadata (abstract, authors, categories, PDF link) by arXiv ID

## Pricing

- **Free tier:** Unlimited; no registration required
- **Paid tiers:** None
- **Enterprise:** N/A
- **Notes:** Bulk data access (full-text corpus) is available via S3 requester-pays at a per-GB rate — see https://info.arxiv.org/help/bulk_data_s3.html

## Authentication

No authentication required. The API is publicly accessible.

## Endpoints

- **Base URL:** `https://export.arxiv.org/api/`
- **Key endpoints:**
  - `GET /query` — search and retrieve paper metadata

**Query parameters:**
  - `search_query` — field-prefixed query string (e.g., `ti:transformer`, `cat:cs.LG`, `all:diffusion model`)
  - `id_list` — comma-delimited arXiv IDs for direct lookup
  - `start` — result offset (default 0)
  - `max_results` — results per response (default 10; max 2,000 per call; total max 30,000 per query)
  - `sortBy` — `relevance`, `lastUpdatedDate`, or `submittedDate`
  - `sortOrder` — `ascending` or `descending`

**Search field prefixes:** `ti` (title), `au` (author), `abs` (abstract), `cat` (subject category), `all` (all fields)

## Example call

```bash
curl "https://export.arxiv.org/api/query?search_query=cat:cs.LG&sortBy=submittedDate&sortOrder=descending&max_results=10"
```

```python
import arxiv

client = arxiv.Client()
search = arxiv.Search(
    query="cat:cs.LG",
    max_results=10,
    sort_by=arxiv.SortCriterion.SubmittedDate,
)
for result in client.results(search):
    print(result.title, result.published, result.pdf_url)
```

## Rate limits

Maximum 1 request every 3 seconds; use a single connection only. Responses are cached — no need to re-query the same search more than once per day. Requests returning more than 30,000 results are rejected with HTTP 400.

## SDKs / Libraries

- **Official:** None — REST API only (Atom 1.0 XML response)
- **Community:** `arxiv` (Python, PyPI); `aioarxiv` (async Python); various Node.js wrappers

## Documentation

- Main docs: https://info.arxiv.org/help/api/index
- User manual: https://info.arxiv.org/help/api/user-manual.html
- Terms of use: https://info.arxiv.org/help/api/tou.html

## Notes

- Response format is Atom 1.0 XML. Parse with `feedparser` or the `arxiv` Python library rather than raw XML parsing.
- arXiv also exposes an OAI-PMH interface (`https://export.arxiv.org/oai2`) for bulk harvesting of metadata by date range — preferred over repeated API queries for large ingestion jobs.
- Subject categories relevant to AI/ML: `cs.AI` (Artificial Intelligence), `cs.LG` (Machine Learning), `cs.CV` (Computer Vision), `cs.CL` (Computation and Language), `stat.ML` (Machine Learning in Statistics).
- Papers are preprints and have not necessarily undergone peer review; check the `journal_ref` field for publication status.
