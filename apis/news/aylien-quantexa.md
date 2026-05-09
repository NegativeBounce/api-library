# Aylien News API (Quantexa)

Enterprise news API with advanced NLP enrichment (entity recognition, sentiment, categorization, summarization, related stories). Now branded as part of Quantexa News API following the Quantexa acquisition. Premium tier for analyst-grade workflows.

**Tier:** Paid (with 14-day trial)
**Auth:** OAuth 2.0 (Bearer token)
**Last researched:** 2026-05-09

## Use cases

- Entity-enriched news search for OSINT investigations on Strait-of-Malacca actors (vessels, ports, companies, named individuals).
- Sentiment and emotion analysis on coverage trends — useful for monitoring narrative shifts on regional security topics.
- Story clustering / "related stories" for analyst workflows that need deduplication and topic grouping.
- Trends API for surfacing topic-level coverage volume changes (e.g., spike in coverage of "Belawan piracy").
- Custom feature bundles licensed per use case.

## Pricing

- **Free tier:** 14-day free trial of News API Pro (full features for evaluation).
- **Paid tiers:** Use-case-licensed; bundles tailored per customer. Not publicly listed — request via sales.
- **Enterprise:** Custom contracts, on-prem available.
- **Notes:** Acquired by Quantexa; current branding mixes Aylien and Quantexa references.

## Authentication

OAuth 2.0 — POST username + password + Application ID to `https://api.aylien.com/v1/oauth/token` to receive a Bearer token (1-hour validity). Pass as `Authorization: Bearer <token>` on subsequent requests.

## Endpoints

- **Token endpoint:** `https://api.aylien.com/v1/oauth/token`
- **Base URL (v6):** `https://api.aylien.com/news/v6/` (some routes via Quantexa hostnames)
- **Key endpoints:**
  - `GET /stories` — search news stories with filters
  - `GET /related_stories` — find similar stories
  - `GET /trends` — topic / entity trend volumes
  - `GET /coverages` — story-coverage analytics
  - `GET /clusters` — clustered story groups

## Example call

```bash
# Stories mentioning Strait of Malacca with sentiment & entity enrichment
curl "https://api.aylien.com/news/v6/stories?aql=text%3A%22strait+of+malacca%22&language=en&published_at.start=NOW-7DAYS" \
  -H "Authorization: Bearer $AYLIEN_TOKEN"
```

## Rate limits

Plan-dependent; not publicly listed.

## SDKs / Libraries

- **Official:** Python, Node, Go SDKs (Aylien-branded).
- **Community:** Various LangChain / Relevance AI integrations.

## Documentation

- News API v6 docs: https://docs.aylien.com/newsapi/v6/getting-started/
- Quantexa News docs: https://docs.aylien.com/
- Plans: https://aylien.com/product/plans

## Notes

- Most analyst-grade NLP among the news APIs in this category — best when downstream consumers are NLP-driven (entity graphs, sentiment dashboards).
- Higher cost than NewsAPI / Mediastack — justified when enrichment quality matters.
- Quantexa branding is in transition; some pages still use Aylien identifiers.
