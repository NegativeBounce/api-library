# Africanews

Pan-African 24/7 news network (Euronews family) providing free RSS feeds, embeddable widgets, and HTML-embed video/timeline content in English, French, Portuguese, and Swahili.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-09

## Use cases

- Continental African breaking news monitoring with multilingual coverage (en/fr/pt/sw)
- Embedding live African news timelines into websites via free widgets
- Building African-news Slack bots, dashboards, or aggregator apps
- Topic-filtered feeds (Business, Sport, Culture, Science & Technology)

## Pricing

- **Free tier:** All RSS feeds and widgets free; no API key required
- **Paid tiers:** None publicly listed for RSS or widget use
- **Enterprise:** Content licensing handled via Euronews syndication partnerships — contact via africanews.com
- **Notes:** Free use of widgets and RSS appears unrestricted; embed code is provided directly on the widgets page

## Authentication

None. Public RSS feeds and copy-paste widget HTML.

## Endpoints

- **Base URL:** `https://www.africanews.com/`
- **Key endpoints:**
  - `GET /feed/rss` — main aggregated feed
  - `GET /feed/rss?theme=<theme>` — section-specific feed (themes include `news`, `business`, `sport`, `culture`, `science-technology`)
  - `GET /page/widgets/` — page with embeddable Just-In timeline and video widgets

## Example call

```bash
# Main Africanews feed
curl "https://www.africanews.com/feed/rss"

# Business-only feed
curl "https://www.africanews.com/feed/rss?theme=business"
```

## Rate limits

Not publicly documented. Reasonable polling cadence is implied by the free RSS access model.

## SDKs / Libraries

- **Official:** None — standard RSS 2.0
- **Community:** Any RSS parser

## Documentation

- Main widgets/RSS page: https://www.africanews.com/page/widgets/

## Notes

Owned by Euronews; launched 2016 as a pan-African counterpart with HQ in Pointe-Noire, Republic of Congo, plus Lyon. Multilingual content (English, French, Portuguese, Swahili — switch via subdomain or theme). RSS gives summaries with links to full articles on africanews.com. The "Just In" widget renders inside an iframe so it stays current automatically. No public REST/JSON API — RSS is the only programmatic surface.
