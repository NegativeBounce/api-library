# Premium Times Nigeria

Abuja-based investigative newspaper (founded 2011, partner in the Panama Papers consortium) providing a free RSS feed across politics, business, foreign affairs, sports, opinion, and investigations.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-09

## Use cases

- Monitoring Nigerian politics, corruption investigations, and federal-level news
- Building Nigeria-focused news readers or alerting tools
- Augmenting continental aggregators (AllAfrica, Africanews) with primary-source Nigerian reporting
- OSINT/civic-tech tooling around Nigerian governance and accountability

## Pricing

- **Free tier:** RSS feed free
- **Paid tiers:** None for RSS
- **Enterprise:** No documented commercial API; reprint and syndication inquiries via the website
- **Notes:** Site is reader-supported with membership/donation appeals

## Authentication

None.

## Endpoints

- **Base URL:** `https://www.premiumtimesng.com/`
- **Key endpoints:**
  - `GET /feed` — main RSS feed
  - `GET /category/<slug>/feed` — section-specific feeds (e.g. `/category/news/headlines/feed`, `/category/business/feed`)

## Example call

```bash
curl "https://www.premiumtimesng.com/feed"
```

## Rate limits

Not publicly documented.

## SDKs / Libraries

- **Official:** None
- **Community:** Standard RSS parsers; the site is on WordPress so feed semantics follow WP conventions

## Documentation

- Site: https://www.premiumtimesng.com/
- Feed: https://www.premiumtimesng.com/feed

## Notes

Awarded the Pulitzer Prize as part of the international Panama Papers consortium (2017) and the Global Shining Light Award (2017). Sister fact-check arm DUBAWA covers West Africa via the Centre for Journalism Innovation and Development (CJID). No JSON/REST API. WordPress-based feed delivers headline + excerpt + full HTML in `<content:encoded>` for most posts.
