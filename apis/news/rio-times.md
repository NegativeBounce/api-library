# The Rio Times

An English-language daily online newspaper covering Rio de Janeiro, Brazil, and Latin America, with a regional newsdesk producing approximately 24 posts per day. Free RSS feed; some premium content gated behind a "Read Without Subscription" / member-login mechanic.

**Tier:** Freemium
**Auth:** None (RSS); subscription/login for some premium content
**Last researched:** 2026-05-09

## Use cases

- Brazil and Rio de Janeiro breaking news (politics, business, real estate, Carnival, nightlife) for English-speaking foreign community and global readers
- Pan-Latin American coverage with country-by-country pages (Argentina through Venezuela)
- Tracking Brazilian markets (Ibovespa, B3, Petrobras, Embraer, Vale) in English
- Defense Monitor / Defense Updates section for South American military and security affairs
- High-frequency news ingestion (~24 posts/day) for monitoring and OSINT

## Pricing

- **Free tier:** RSS feed and most articles free
- **Paid tiers:** Premium membership (login required) for some long-form analysis and "Read Without Subscription" archive
- **Enterprise:** Direct contact via the publication's about/contact page
- **Notes:** Branded as "Latin America's Voice From Brazil"

## Authentication

None for RSS or main content. Premium articles require member login.

## Endpoints

- **Base URL:** `https://www.riotimesonline.com/`
- **Key endpoints:**
  - `GET /feed` — main all-news RSS feed
  - Section pages (HTML, free): `/brazil-news/category/brazil/`, `/rio-de-janeiro/`, `/category/sao-paulo/`, `/category/politics/`, `/category/business/`, `/category/markets/`, `/category/world/`
  - Per-country LatAm pages: `/category/argentina/`, `/category/chile/`, `/category/colombia/`, `/category/peru/`, `/category/venezuela/`, etc.
  - Defense Monitor: `/category/defense-monitor/`

## Example call

```bash
curl "https://www.riotimesonline.com/feed"
```

## Rate limits

Not publicly documented.

## SDKs / Libraries

- **Official:** None for the public RSS surface; Telegram channel `t.me/theriotimes` for distribution
- **Community:** Standard RSS parsers

## Documentation

- Main site: https://www.riotimesonline.com/
- Read without subscription: https://www.riotimesonline.com/read-without-subscription1/
- Telegram: https://t.me/s/theriotimes

## Notes

The Rio Times is **independent** and was founded as an English-language daily oriented toward the foreign community in Rio de Janeiro and Brazil. Coverage has expanded to all of Latin America with country-specific pages (including French Guyana, Suriname, and Caribbean affairs alongside South American countries). High publishing volume (~24 posts/day per Feedspot rankings) makes it a strong source for high-frequency monitoring. Maintains a dedicated **Defense Monitor / Defense Updates** section useful for South American military and security OSINT. For source-trust analysis: independent ownership, no state affiliation, but commercial subscription model means some long-form analysis is paywalled. Brand line: "Latin America's Voice From Brazil." No public REST/JSON developer API documented; the `/feed` RSS plus per-section HTML pages are the programmatic surface.
