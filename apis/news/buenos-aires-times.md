# Buenos Aires Times

Argentina's only English-language newspaper, published as a weekly print supplement to the Perfil daily and as a daily-updated digital edition. Run by the Perfil Group (Editorial Perfil S.A., founded by Jorge Fontevecchia), with free RSS access.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-09

## Use cases

- Argentina breaking news monitoring (politics, economy, finance, Milei administration coverage, AMIA case, Falklands/Malvinas)
- Tracking Argentine markets, peso/dollar dynamics, inflation, and IMF program developments in English
- Building Latin America news readers with credible Buenos Aires editorial perspective
- Augmenting MercoPress regional coverage with deeper Argentina-domestic detail

## Pricing

- **Free tier:** All RSS feeds and full website free
- **Paid tiers:** Optional digital subscriptions for member content (paywall on some long-form features)
- **Enterprise:** Editorial sales handled directly via Perfil Group commercial team
- **Notes:** Print weekly distributed inside Perfil newspaper every Saturday; digital is updated daily

## Authentication

None.

## Endpoints

- **Base URL:** `https://www.batimes.com.ar/`
- **Key endpoints:**
  - `GET /feed` — main all-news RSS feed
  - Section pages (HTML): `/section/argentina`, `/section/world`, `/section/economy`, `/section/society`, `/section/sports`, `/section/culture`, `/section/perfil` (Perfil syndicated content), `/last-news`

## Example call

```bash
curl "https://www.batimes.com.ar/feed"
```

## Rate limits

Not publicly documented.

## SDKs / Libraries

- **Official:** None for the public RSS surface
- **Community:** Standard RSS parsers

## Documentation

- Main site: https://www.batimes.com.ar/
- Latest news: https://www.batimes.com.ar/last-news

## Notes

Buenos Aires Times is operated by the **Perfil Group (Editorial Perfil S.A.)**, a privately-held Argentine media group founded by journalist Jorge Fontevecchia in 1976. The print English edition is distributed as a weekly insert inside the daily Perfil newspaper every Saturday; the digital edition (`batimes.com.ar`) is updated continuously. For source-trust analysis: privately owned, no government affiliation, and Perfil Group has a track record of investigative journalism and access-to-public-information advocacy (Argentine government-disclosure lawsuits). Editorial style is broadsheet-formal, with English translations and original Argentine staff reporting. Coverage strongest on Argentine domestic politics, economy/finance, AMIA bombing case, Falklands/Malvinas, and regional Latin American affairs. No public REST/JSON developer API documented; programmatic access via `/feed` RSS only.
