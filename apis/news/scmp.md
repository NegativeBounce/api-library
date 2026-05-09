# South China Morning Post (SCMP)

Hong Kong's premier English-language newspaper (founded 1903, ~120 years on the China beat) providing free RSS feeds across Hong Kong, China, world, business, tech, and lifestyle sections.

**Tier:** Freemium
**Auth:** None (RSS); subscription login for some premium articles
**Last researched:** 2026-05-09

## Use cases

- Hong Kong and Greater China news monitoring with English-language editorial
- Tracking China political developments, US-China relations, and Asian markets
- Following Chinese tech sector (Alibaba, Tencent, Huawei, BYD, semiconductor supply chain)
- Building dashboards for China-watchers, OSINT, and policy analysts outside the mainland

## Pricing

- **Free tier:** RSS feeds free; many articles available without subscription
- **Paid tiers:** SCMP digital subscription (monthly/annual; pricing varies by region) for premium investigations and full archive access
- **Enterprise:** Content licensing and B2B feeds — contact SCMP via digitalsupport@scmp.com
- **Notes:** Owned by Alibaba Group since 2016; editorial independence is publicly stated but worth noting for source-trust analysis

## Authentication

None for RSS feeds.

## Endpoints

- **Base URL:** `https://www.scmp.com/`
- **Key endpoints (RSS):**
  - `GET /rss/2/feed` — Hong Kong
  - `GET /rss/3/feed` — This Week in Asia (Singapore/Malaysia/Philippines/India/Australasia)
  - `GET /rss/4/feed` — China
  - `GET /rss/5/feed` — World
  - `GET /rss/36/feed` — Tech
  - `GET /rss/91/feed` — Comment
  - `GET /rss/92/feed` — Business
  - `GET /rss/94/feed` — Lifestyle
  - `GET /rss/95/feed` — Sport
  - `GET /rss/96/feed` — Property
  - RSS index: `https://www.scmp.com/rss`

## Example call

```bash
# China desk
curl "https://www.scmp.com/rss/4/feed"

# Hong Kong desk
curl "https://www.scmp.com/rss/2/feed"
```

## Rate limits

Not publicly documented.

## SDKs / Libraries

- **Official:** None
- **Community:** Standard RSS parsers; calibre and similar tools have community recipes for article fetching

## Documentation

- RSS index: https://www.scmp.com/rss
- Site: https://www.scmp.com/

## Notes

Founded 1903; widely considered Hong Kong's newspaper of record. RSS feeds give summaries with links; full article body comes from the page (some paywalled). Sections are numbered (e.g. `/rss/4/feed` = China) — IDs are stable. This Week in Asia covers SE Asia/India/Australasia, useful for scope beyond strict East Asia. No public REST/JSON API documented for general developers.
