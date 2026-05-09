# News24

South Africa's largest digital news platform (Naspers/Media24, ~6M+ monthly uniques) providing free RSS feeds across national, African, world, business, sport, entertainment, tech, and lifestyle categories.

**Tier:** Free
**Auth:** None (RSS); subscription paywall for premium articles
**Last researched:** 2026-05-09

## Use cases

- South African breaking news monitoring (national, provincial, and city coverage)
- Africa-region desk coverage from a Johannesburg/Cape Town editorial perspective
- Building dashboards or alert tools for SA business, sport, or politics
- Tracking SA investigative reporting and opinion content (full text behind paywall)

## Pricing

- **Free tier:** All RSS feeds free; standard headlines and previews
- **Paid tiers:** News24 Premium subscription (R75/month at last published rate) for full investigative articles — does not provide an additional API
- **Enterprise:** Content syndication via Media24 — contact 24.com partnerships
- **Notes:** RSS provides excerpts and links to news24.com; full premium articles require login on the website

## Authentication

None for RSS feeds. Premium paywall is web-based (cookie/login session) and not exposed as a public API.

## Endpoints

- **Base URL:** `https://feeds.news24.com/articles/` (RSS feed service, fronted by capi24.com infrastructure) and `https://www.news24.com/`
- **Key endpoints:**
  - `GET https://feeds.news24.com/articles/news24/TopStories/rss` — top stories
  - `GET https://feeds.news24.com/articles/news24/SouthAfrica/rss` — South Africa
  - `GET https://feeds.news24.com/articles/news24/Africa/rss` — Africa desk
  - `GET https://feeds.news24.com/articles/Fin24/Tech/rss` — tech (Fin24)
  - Full feed list: https://www.news24.com/news24-rss-feeds-20111202

## Example call

```bash
# News24 Top Stories
curl "https://feeds.news24.com/articles/news24/TopStories/rss"

# Africa desk
curl "https://feeds.news24.com/articles/news24/Africa/rss"
```

## Rate limits

Not publicly documented.

## SDKs / Libraries

- **Official:** None
- **Community:** Standard RSS parsers

## Documentation

- Main RSS index: https://www.news24.com/news24-rss-feeds-20111202
- City Press RSS: https://www.news24.com/citypress/siteelements/services/rss-20090828
- Channel24 (entertainment) RSS: https://www.news24.com/channel/rss-feeds-20100921

## Notes

News24 surpassed 100,000 paid subscribers in early 2024, becoming the largest subscription-led news website in Africa. Sister brands include Fin24 (business), Sport24, Channel24 (entertainment), Health24, and Business Insider SA — each has its own RSS section. RSS items contain headline + short summary; full text and premium investigations require a News24 Premium subscription. No public JSON/REST API documented for general developers.
