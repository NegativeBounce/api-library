# The Times of Israel

A Jerusalem-based independent online newspaper founded in 2012 by veteran Israeli journalist David Horovitz and US-based capital partner Seth Klarman, providing free RSS-accessible news on Israel, the Middle East, and the Jewish world.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-09

## Use cases

- Israel breaking news monitoring (politics, security, IDF, Knesset, settlements, Gaza, Lebanon)
- Independent English-language Israeli editorial perspective for source-comparison alongside Haaretz, Jerusalem Post, Ynetnews
- Tracking Jewish diaspora news, antisemitism, and Israel-related global affairs
- Building Israel/Mideast news readers free of paywall constraints

## Pricing

- **Free tier:** Full RSS feed and site access free with no paywall
- **Paid tiers:** Optional "Times of Israel Community" membership ($6/month or higher) for ad-light experience and member benefits — supports the newsroom but is not required for content access
- **Enterprise:** Content syndication via direct contact with editorial leadership
- **Notes:** Funded by capital partner Seth Klarman plus reader contributions; explicitly states no partisan political affiliation per masthead

## Authentication

None.

## Endpoints

- **Base URL:** `https://www.timesofisrael.com/`
- **Key endpoints:**
  - `GET /feed/` — main all-news RSS feed
  - Topic feeds available via `/topic/{slug}/feed/` pattern (e.g. tech, AI)
  - Section pages (HTML): `/israel-and-the-region/`, `/jewish-times/`, `/world-of-jewish-news/`, `/start-up-israel/`, `/spotlight/`

## Example call

```bash
curl "https://www.timesofisrael.com/feed/"
```

## Rate limits

Not publicly documented.

## SDKs / Libraries

- **Official:** Times of Israel iOS and Android apps (consumer-facing, not developer SDKs)
- **Community:** Standard RSS parsers; community RSS-bridge configurations exist for fuller article fetching

## Documentation

- Main site: https://www.timesofisrael.com/
- About: https://www.timesofisrael.com/about/

## Notes

The Times of Israel is **independent and has no partisan political affiliation per its masthead**, which is unusual among major Israeli English-language outlets. Founded in 2012 by David Horovitz (UK-born Israeli journalist, founding editor) and Seth Klarman (US capital partner). Coverage is strongest on Israeli domestic politics, security/IDF, Israel-Palestinian conflict, Jewish diaspora, and Iran-Israel dynamics. For source-trust analysis: independent ownership distinguishes ToI from state-funded outlets like Al Arabiya, Tehran Times, or partially state-funded outlets like Al Jazeera. RSS feed is free and reliable; no paywall on most articles. No public REST/JSON developer API documented. Some users report the iOS app has display glitches but the underlying RSS surface is solid.
