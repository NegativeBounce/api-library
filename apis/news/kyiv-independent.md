# The Kyiv Independent

Ukraine's fastest-growing English-language news outlet, founded in November 2021 by former staff of the Kyiv Post who were fired by their owner three months before Russia's full-scale invasion. Independent, ad-free, no paywall, partly journalist-owned, with majority of revenue from reader memberships and donations.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-09

## Use cases

- Ukraine war front-line reporting (Russia-Ukraine war coverage, drone strikes, peace negotiations, Western military aid)
- Ukraine domestic politics, corruption investigations, and Zelensky administration analysis
- Russia analysis from Ukrainian perspective (sanctions, war economy, Putin regime, Russian war crimes)
- Belarus and broader Eastern European affairs
- War Crimes documentation — Kyiv Independent's War Crimes Investigations Unit produces investigative documentaries
- Source-comparison alongside Meduza (Russian-exile perspective), TASS (Russian state perspective), and DW/France 24 (Western public broadcaster) for cross-checking war coverage

## Pricing

- **Free tier:** Full website access, all newsletters, all video reports — no paywall
- **Paid tiers:** Membership program with multiple tiers (Patron, Sponsor, Insider, Partner) starting at ~$5/month; tiered access to Discord community, one-on-one calls with leadership for higher tiers
- **Enterprise:** Content syndication and partnership inquiries via direct contact
- **Notes:** **70% of 2024 revenue came from reader memberships and donations**; remaining mix from grants and commercial activities. **No single owner or external controlling financier**; partly owned by its journalists by design

## Authentication

None.

## Endpoints

- **Base URL:** `https://kyivindependent.com/`
- **Key endpoints:**
  - Main site: `https://kyivindependent.com/`
  - News feed (HTML archive): `https://kyivindependent.com/news-archive/`
  - About / mission: `https://kyivindependent.com/about/`
  - RSS feed: likely `https://kyivindependent.com/feed/` (Ghost CMS pattern; verify on integration). Aggregators reference `kyivindependent.com/news-arc..` (truncated) suggesting `/news-archive/feed/` may also be valid
  - 7 active newsletters: Ukraine Daily, Ukraine Weekly, War Notes, WTF is Wrong With Russia?, Belarus Weekly, Ukraine Business Roundup, Explaining Ukraine — subscribe via main site
- **Membership / Discord:** community access via membership tiers

## Example call

```bash
# Main site
curl "https://kyivindependent.com/"

# News archive (HTML)
curl "https://kyivindependent.com/news-archive/"

# RSS feed (verify exact path on first integration — try /feed/ first)
curl "https://kyivindependent.com/feed/"
```

## Rate limits

Not publicly documented.

## SDKs / Libraries

- **Official:** YouTube channel for video reports and "Ukraine This Week" weekly series; Discord community for members; presence on Bluesky, Twitter (X), Telegram, Threads, TikTok, Facebook, Instagram, LinkedIn, Reddit
- **Community:** Standard RSS parsers (assuming Ghost CMS pattern)

## Documentation

- Main site: https://kyivindependent.com/
- About: https://kyivindependent.com/about/
- Wikipedia: https://en.wikipedia.org/wiki/The_Kyiv_Independent
- Every.org charity profile: https://www.every.org/ki-media

## Notes

The Kyiv Independent was **founded in November 2021** — three months before Russia's full-scale invasion of Ukraine on February 24, 2022 — by a group of journalists who had just been fired from the **Kyiv Post**. The dispute that triggered the firings: in October 2021, Kyiv Post owner **Adnan Kivan** (Syrian-born investor, owner of the KADORR Group and Kanal Odesa 7) attempted to take editorial control of the newsroom, ending its critical coverage of Ukrainian authorities. Journalists believed Kivan had received "signals of discontent" from Zelensky's presidential administration. When the owner shut down the paper on November 8, 2021, the fired team — together with **Jnomics Media** consultancy (Daryna Shevchenko and Jakub Parusinski) — co-founded the Kyiv Independent.

**Awards:** 20+ international journalism awards. **War Crimes Investigations Unit** (formed March 2023) has produced 9-10 investigative documentaries and won 7+ international awards. Reporter **Asami Terajima** shortlisted for 2026 One World Media Awards (Print Award category).

**Coverage strengths:** **Front-line war reporting** (sea drone embeds with Ukrainian Navy, drone strikes, Russian war crimes documentation), **corruption investigations within Ukraine** (including misconduct within Ukrainian military — important for credibility, since they don't only criticize Russia), **Belarus** (dedicated weekly newsletter), and **explanatory journalism** ("Explaining Ukraine" newsletter and podcast).

**For source-trust analysis:** **Independent, reader-funded, no oligarch ownership, partly journalist-owned by design**, no paywall. **Currently the most-cited English-language Ukrainian news source** for international Ukraine coverage. Editorial line is pro-Ukrainian and anti-Kremlin (consistent with the country's existential war), but the outlet has demonstrated willingness to cover Ukrainian government corruption and military misconduct, which strengthens its credibility relative to pure-advocacy outlets. In 2025, when other Ukrainian media outlets were hit by the **USAID freeze**, Kyiv Independent ran a crowdfunding campaign that raised $66,200+ for three local Ukrainian outlets (Tsukr in Sumy, Gwara Media in Kharkiv, MykVisti in Mykolaiv). No public REST/JSON developer API documented.
