# NewsAPI.org

Aggregator REST API providing access to articles from 80,000+ news sources globally with filtering by source, language, country, keyword, and date. Popular freemium choice for general news ingestion.

**Tier:** Freemium
**Auth:** API Key (header or query)
**Last researched:** 2026-05-09

## Use cases

- Pull recent articles mentioning "Strait of Malacca," "Selat Malaka," "Belawan," "Port Klang," or named vessels for OSINT investigations.
- Top-headlines feed for Indonesia, Malaysia, Singapore, and Thailand for regional context.
- Source filtering — Reuters, Channel News Asia, Bloomberg, The Star, Jakarta Post, Bernama.
- Lightweight prototyping (free tier covers dev workflows; paid plans cover prod).
- Backup feed alongside GDELT and local-language news APIs.

## Pricing

- **Free tier (Developer):** $0, 100 requests/day, **dev/test only**, 24-hour article delay, 1-month archive search, CORS for localhost.
- **Paid tiers:**
  - **Business:** $449/month, 250,000 requests/month, real-time, 5-year archive, 99.95% SLA. Overage $0.0018/req.
  - **Advanced:** $1,749/month, 2,000,000 requests/month. Overage $0.0009/req.
- **Enterprise:** Custom pricing; on-prem available.
- **Notes:** 20% annual discount. Free tier is **not licensed for production** — prod use requires Business+.

## Authentication

API key issued at signup. Sent in the `X-Api-Key` header or `?apiKey=...` query parameter.

## Endpoints

- **Base URL:** `https://newsapi.org/v2/`
- **Key endpoints:**
  - `GET /everything` — full-text article search across all sources
  - `GET /top-headlines` — top headlines per country/category
  - `GET /sources` — list of available sources

## Example call

```bash
# Articles mentioning Strait of Malacca over the last 7 days, in English
curl "https://newsapi.org/v2/everything?q=%22strait+of+malacca%22&language=en&sortBy=publishedAt&from=2026-05-02" \
  -H "X-Api-Key: $NEWSAPI_KEY"
```

## Rate limits

- Developer: 100 req/day, max 1 request/second.
- Business: 250K/month rolling.
- Advanced: 2M/month rolling.

## SDKs / Libraries

- **Official:** Node, Python, Ruby (lightly maintained).
- **Community:** Many wrappers across languages.

## Documentation

- Main docs: https://newsapi.org/docs
- Pricing: https://newsapi.org/pricing
- Source list: https://newsapi.org/sources

## Notes

- Coverage of Indonesian and Malaysian-language sources is thinner than English — for local-language work pair with Mediastack or Newscatcher.
- The 24-hour delay on the free tier is a hard blocker for any real-time use.
- The `/everything` endpoint is the workhorse; `/top-headlines` is curated and biased toward major outlets.
