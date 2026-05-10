# Meduza

A Russian-language and English-language independent news outlet headquartered in Riga, Latvia, founded in October 2014 by Galina Timchenko and the journalists who had quit Lenta.ru en masse in protest after Timchenko's politically-motivated firing. Independent, exile-based, declared "undesirable" by Russia in January 2023 and blocked inside Russia.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-09

## Use cases

- Russia domestic affairs from independent perspective (Putin regime, war economy, sanctions impact, mobilization, conscription, war losses)
- Russian opposition and exile community coverage; Russian dissident affairs
- Russia-Ukraine war analysis from Russian-speaking but anti-Kremlin perspective
- Belarus, Central Asia, Caucasus, post-Soviet space coverage
- Source-comparison alongside Kyiv Independent (Ukrainian perspective), TASS (Russian state perspective), DW Russian-language service, BBC Russian, and Novaya Gazeta Europe for cross-checking war and Russian-domestic coverage

## Pricing

- **Free tier:** All website content and RSS feeds in both Russian and English; no paywall
- **Paid tiers:** Optional reader donations and crowdfunding support
- **Enterprise:** Content syndication and republication via direct contact
- **Notes:** **No advertising on Meduza** (Russia banned all advertising on Meduza after labeling it a "foreign agent" in 2021); **funded primarily through reader donations and crowdfunding**, plus international foundation support. Russian "foreign agent" designation (2021) and "undesirable organization" designation (January 2023) made advertising and Russian-side reader payments effectively impossible

## Authentication

None.

## Endpoints

- **Base URL:** `https://meduza.io/`
- **Key endpoints:**
  - English homepage: `https://meduza.io/en`
  - Russian homepage: `https://meduza.io/`
  - English RSS (verify exact path on first integration): try `https://meduza.io/en/rss/all` or `https://meduza.io/rss/en/all`
  - Russian RSS (verify): try `https://meduza.io/rss/all`
  - Section feeds (per FeedSpot): `meduza.io/articles`, `meduza.io/razbor` (analysis), `meduza.io/podcasts`
- **Mirror sites:** Meduza maintains backup mirror domains for use inside Russia where the primary domain is blocked; mirror availability rotates due to ongoing DDoS attacks

## Example call

```bash
# English homepage
curl "https://meduza.io/en"

# RSS feed (verify exact path on first integration)
curl "https://meduza.io/rss/en/all"

# Russian site (for cross-language ingestion)
curl "https://meduza.io/"
```

## Rate limits

Not publicly documented. **Caveat:** Meduza has been the target of sustained, sophisticated DDoS attacks since at least February 2024 (peaking at 2 billion requests over 48 hours from a known attack infrastructure including RapidSeedBox and MIN Proxy). Cloudflare protection is in place. Aggressive scraping or unusual request patterns may be rate-limited or challenged.

## SDKs / Libraries

- **Official:** Meduza mobile app (iOS, Android) with VPN-friendly distribution; podcast feeds; Telegram channel for distribution to Russian-domestic audiences
- **Community:** Standard RSS parsers; X/Twitter `@meduza_en` (English) and `@meduzaproject` (Russian)

## Documentation

- Main site (Russian): https://meduza.io/
- English edition: https://meduza.io/en
- About: https://meduza.io/en/about

## Notes

Meduza was **founded in October 2014** by **Galina Timchenko** and the team that had quit Lenta.ru en masse following Timchenko's politically-motivated firing in March 2014 (the Lenta.ru ouster came after Russian state censors issued an official warning over a story containing a hyperlink to "extremist" materials — an interview with a Ukrainian Right Sector member). More than 80 editors and reporters resigned in protest, calling Timchenko's firing "an act of censorship." Timchenko told Forbes the team chose to register Meduza in Latvia, outside the `.ru` domain zone, because **"establishing an independent Russian-language publishing house in Latvia is possible, while in Russia it is not."**

The English edition launched in 2015, initially aimed at international-affairs specialists. Editor-in-chief of the English service: Konstantin Benyumov originally; current leadership has rotated. **English readership grew several-fold after the February 2022 invasion.** Pre-war monthly readership was approximately 20 million unique visitors with Russia as the #1 country and Ukraine #2. Most popular **independent Russian-language news source** prior to the war.

**Russian government actions against Meduza:**
- **2021:** Designated a "foreign agent" by the Russian Ministry of Justice — required prominent disclaimer on all content; Russian advertisers banned from working with Meduza
- **January 2023:** Russia's General Prosecutor's Office designated Meduza an **"undesirable organization,"** stating the outlet "poses a threat to the foundations of Russia's constitutional order and security" — this criminalized any cooperation with Meduza inside Russia
- **Pre-2023:** Sites blocked by Roskomnadzor (Russian internet regulator)
- **February 2024 onwards:** Sustained DDoS attacks against meduza.io, mirror sites, crowdfunding infrastructure, and staff email/social accounts. The April 2024 attack alone generated 2 billion requests over 48 hours

**For source-trust analysis — important nuances:**
- **Independent and exile-based**, with strong track record on Lenta.ru-era investigative journalism
- Editorial line is **anti-Putin, anti-war, sympathetic to Russian opposition**, but maintains journalistic standards (does not engage in pure-advocacy framing)
- **Latvian intelligence has publicly warned that Russian-exile media outlets operating in Latvia could be infiltrated by Russian intelligence agents** — Meduza editor Ivan Kolpakov (interviewed in 2022) stated full trust in his ~50-person team based on long-tenure and pre-existing personal relationships, but the structural risk is worth flagging
- Russia's "undesirable organization" designation (Jan 2023) means **any Russian citizen sharing or quoting Meduza inside Russia faces criminal prosecution** — affects how Russian sources interact with the outlet

**Editorial partnerships:** Meduza has co-produced with BuzzFeed, has sister-outlet relationships with Riga-based Russian-language exile media including Novaya Gazeta Europe (which moved to Riga from Moscow after the invasion). No public REST/JSON developer API documented; RSS and the standard website are the primary programmatic surfaces.
