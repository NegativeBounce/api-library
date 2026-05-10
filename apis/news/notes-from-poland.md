# Notes from Poland

An independent English-language publication covering Polish news, politics, and society. Founded in 2019 by historian and journalist Daniel Tilles, who serves as editor-in-chief. Free, RSS-accessible, no paywall — among the leading English-language sources on Poland alongside Polish state broadcaster TVP World.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-09

## Use cases

- Poland domestic politics in English (PiS-PO coalition dynamics, presidential affairs, Sejm/Senate, judicial reform, EU-Poland relations)
- Tracking Polish positioning on Russia-Ukraine war, NATO eastern flank, and EU policy
- Poland-Belarus border situation, migration policy, and security affairs
- Polish economic affairs, energy policy (nuclear program, coal transition), and EU funds
- Source-comparison alongside DW, France 24, and Balkan Insight for Central/Eastern European coverage with English-language Polish-specialist depth

## Pricing

- **Free tier:** Full website access, RSS feeds, and newsletter — no paywall
- **Paid tiers:** Optional reader memberships ("Friends of Notes from Poland") and donations via Patreon-style support
- **Enterprise:** Content syndication via direct contact
- **Notes:** Funded primarily through reader memberships, donations, advertising, and grants; small-team independent operation

## Authentication

None.

## Endpoints

- **Base URL:** `https://notesfrompoland.com/`
- **Key endpoints:**
  - Main site: `https://notesfrompoland.com/`
  - RSS feed (verify on integration; typical WordPress pattern): `https://notesfrompoland.com/feed/`
  - Section pages (HTML): `/category/news`, `/category/society`, `/category/politics-and-international`, `/category/business`
  - Newsletter: subscribe via main site
  - About: `https://notesfrompoland.com/about/`

## Example call

```bash
# Main site
curl "https://notesfrompoland.com/"

# RSS feed (verify exact path on first integration)
curl "https://notesfrompoland.com/feed/"
```

## Rate limits

Not publicly documented.

## SDKs / Libraries

- **Official:** None for the public RSS surface; presence on X/Twitter (`@notesfrompoland`), Facebook, LinkedIn, Bluesky, YouTube
- **Community:** Standard RSS parsers (WordPress pattern)

## Documentation

- Main site: https://notesfrompoland.com/
- About: https://notesfrompoland.com/about/

## Notes

Notes from Poland was **founded in 2019 by Daniel Tilles**, a British-born historian (PhD in Polish history) and journalist who serves as the publication's editor-in-chief. The outlet positions itself as an **independent, balanced source on Polish affairs** for international readers — filling a gap between the Polish state broadcaster's English service (TVP World, pro-government editorial line) and the very limited English-language coverage offered by Poland's commercial press (Gazeta Wyborcza, Rzeczpospolita are Polish-only; Onet has minimal English).

**Editorial style:** Notes from Poland generally aims for analytical neutrality, covering both PiS (Law and Justice) and KO (Civic Coalition) governments without strong partisan framing. The publication grew significantly in profile during the 2020s as Poland became increasingly central to European affairs (Ukraine war, refugee crisis, judicial-reform standoff with the EU, presidential elections). **Daniel Tilles** is a frequent commentator for international media on Polish politics, and his historical background gives the publication strong analytical depth on Polish-Russian, Polish-German, and Polish-Jewish historical relations.

**Coverage strengths:**
- **Polish domestic politics** — including the 2023 election that ended PiS rule and the 2025 presidential election and aftermath
- **Poland-Ukraine relations** (one of the most important bilateral relationships in current European security)
- **Polish-Belarus border situation** (migration crisis, hybrid warfare from Belarus/Russia)
- **EU-Poland relations** — judicial reform, rule-of-law disputes, EU funds suspension and release
- **Polish historical affairs** — given Tilles' historian background

**For source-trust analysis:** **Independent**, no government affiliation, balanced editorial line. Generally regarded as one of the most credible English-language sources on Poland, used as a reference by Politico Europe, the Financial Times, BBC, and other major international outlets for Polish-specialist context. **Important caveat:** the publication is small-team (Tilles plus a handful of contributors), so coverage breadth is limited compared to a national daily. For breaking Polish news at scale, Polish-language `Onet`, `Wirtualna Polska`, `TVN24`, and `Polish Press Agency (PAP)` remain the primary national sources. Sister English-language Poland outlets to be aware of: **TVP World** (Polish state broadcaster, government editorial line — flag accordingly), **Polish News in English** (smaller aggregator), and **Visegrad Insight** (regional Central European think tank with English coverage). No public REST/JSON developer API documented; RSS is the primary programmatic surface.
