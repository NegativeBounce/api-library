# Papers with Code API

Community-maintained API linking machine learning research papers to their open-source implementations, evaluation benchmarks, and state-of-the-art leaderboard results.

**Tier:** Free
**Auth:** None (read); API token (write)
**Last researched:** 2026-05-13

## Use cases

- Finding reproducible code implementations for specific ML papers or methods
- Querying benchmark leaderboards to compare model performance across tasks and datasets
- Monitoring new state-of-the-art results on specific tasks (image classification, NLP, RL)

## Pricing

- **Free tier:** Full read access; no registration required
- **Paid tiers:** None
- **Enterprise:** N/A
- **Notes:** Write access (submitting papers, results, competitions) requires a free API token from your Papers with Code account settings.

## Authentication

No authentication required for read operations. For write operations, obtain a token from your account at https://paperswithcode.com and pass as `Authorization: Token <TOKEN>` header.

## Endpoints

- **Base URL:** `https://paperswithcode.com/api/v1/`
- **Key endpoints:**
  - `GET /papers/` — paginated paper list; params: `q` (search), `arxiv_id`, `title`, `abstract`, `page`, `items_per_page`
  - `GET /papers/{id}/` — single paper by Papers with Code ID
  - `GET /papers/{id}/repositories/` — code repositories linked to a paper
  - `GET /methods/` — ML methods (architectures, techniques) with linked papers
  - `GET /tasks/` — benchmark tasks (e.g., image classification, question answering)
  - `GET /datasets/` — datasets used in benchmarks
  - `GET /evaluations/` — benchmark evaluation tables by task and dataset
  - `GET /results/` — individual model result entries on leaderboards

## Example call

```bash
curl "https://paperswithcode.com/api/v1/papers/?q=diffusion+model&items_per_page=20"
```

```python
from paperswithcode import PapersWithCodeClient

client = PapersWithCodeClient()
papers = client.paper_list(q="diffusion model", items_per_page=20)
for paper in papers.results:
    print(paper.title, paper.arxiv_id, paper.paper_url)
```

## Rate limits

Not publicly documented. No known hard limits for read access; apply standard crawl etiquette.

## SDKs / Libraries

- **Official:** `paperswithcode-client` (Python, PyPI); maintained by the Papers with Code team
- **Community:** Various MCP server implementations for LLM integration

## Documentation

- API docs: https://paperswithcode.com/api/v1/docs/
- Client docs: https://paperswithcode-client.readthedocs.io/
- GitHub: https://github.com/paperswithcode/paperswithcode-client

## Notes

- Papers with Code was acquired by Meta AI Research in 2021 and continues to operate as a free community resource.
- The API does not include full-text paper content — it links to arXiv PDFs and GitHub repositories. Combine with the arXiv API (`arxiv.md`) for paper content.
- State-of-the-art tracking via `/evaluations/` and `/results/` is the unique value of this API — not replicated by other academic APIs.
- The `tasks` taxonomy is a useful controlled vocabulary for ML research areas with 1,000+ tasks defined, each with descriptions and benchmark history.
- Use the `has_code` filter on paper searches to narrow results to papers with linked reproducible implementations.
