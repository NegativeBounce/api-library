# MercoPress

An independent South Atlantic news agency founded in 1993 and operated from Montevideo, Uruguay, focused on Mercosur, the South Atlantic, and South America. Provides free per-country and per-topic RSS feeds in English.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-09

## Use cases

- Mercosur trade-bloc and regional integration news monitoring (Argentina, Brazil, Paraguay, Uruguay, Venezuela, plus associate members Bolivia, Ecuador, Chile, Colombia, Peru, Guyana, Suriname)
- Falkland Islands / South Atlantic / Antarctica coverage from a regional editorial perspective
- Tracking pan-Latin-American politics, economy, agriculture, fisheries, energy, environment
- Building OSINT pipelines on South American affairs with a regional-focus, English-language source

## Pricing

- **Free tier:** All RSS feeds, weekly Friday email newsletter, and full website access free
- **Paid tiers:** None
- **Enterprise:** Banner advertising and weekly newsletter sponsorship; contact `merco [at] mercopress.com`
- **Notes:** Funded primarily through advertising and sponsorship; full archive accessible since 2004 (with site dating back to 1996)

## Authentication

None.

## Endpoints

- **Base URL:** `https://en.mercopress.com/`
- **Key endpoints (RSS):**
  - `GET /rss` — main all-news feed
  - Per-country feeds: `/rss/argentina`, `/rss/brazil`, `/rss/uruguay`, `/rss/paraguay`, `/rss/venezuela`, `/rss/falkland-islands`, `/rss/united-states`
  - Per-topic feeds: `/rss/politics`, `/rss/economy`, `/rss/energy`, `/rss/agriculture`, `/rss/fisheries`, `/rss/environment`, `/rss/health-science`, `/rss/investments`, `/rss/tourism`, `/rss/real-estate`, `/rss/entertainment`
  - Bloc/regional feeds: `/rss/mercosur`, `/rss/latin-america`, `/rss/unasur`, `/rss/international`, `/rss/antarctica`
  - RSS index landing page: `/feeds`

## Example call

```bash
# Main all-news feed
curl "https://en.mercopress.com/rss"

# Mercosur bloc
curl "https://en.mercopress.com/rss/mercosur"

# Brazil-specific
curl "https://en.mercopress.com/rss/brazil"
```

## Rate limits

Not publicly documented.

## SDKs / Libraries

- **Official:** None — standard RSS surface
- **Community:** Standard RSS parsers; rss-bridge configurations available

## Documentation

- Main site: https://en.mercopress.com/
- About: https://en.mercopress.com/about-mercopress
- RSS index: https://en.mercopress.com/feeds
- Archive (since 1996): https://en.mercopress.com/archive

## Notes

MercoPress positions itself as an **independent news agency** per its official "About" page, founded by independent journalists from Mercosur member countries. Has correspondents and stringers in Uruguay, Argentina, Brazil, Chile, the United Kingdom, the United States, and the Falkland Islands. **Important source-trust caveat:** at least one third-party source (`newstodayintheworld.com`) characterizes MercoPress as "multi-state of Latin America funded" — this contradicts the official self-description and is unverified; for source-trust analysis, treat MercoPress as independent per its primary masthead but flag the outside characterization. Coverage spans South America, the South Atlantic, the Falkland Islands, and Antarctica with daily updates. Operates a weekly Friday email digest in addition to the RSS surface. The agency's strongest desks are Mercosur trade affairs, Falklands / South Atlantic geopolitics, and fisheries — useful for maritime and regional-trade OSINT. No public REST/JSON developer API documented.
