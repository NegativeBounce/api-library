# Focus Taiwan (CNA English)

The English-language service of Taiwan's official news agency (Central News Agency, CNA), founded in 1924, publishing 1,000+ daily news items covering Taiwan politics, cross-strait relations, economy, technology (TSMC, MediaTek, Hon Hai), and society.

**Tier:** Freemium
**Auth:** None (current news); subscription for archive >6 months
**Last researched:** 2026-05-09

## Use cases

- Taiwan news monitoring with official-agency reliability (politics, defense, semiconductor industry)
- Cross-strait relations coverage from a Taipei editorial perspective
- Tracking TSMC, MediaTek, and broader Taiwanese tech supply chain
- Augmenting SCMP/Nikkei coverage with primary-source Taiwanese government statements

## Pricing

- **Free tier:** All current news (within last 6 months) free on focustaiwan.tw
- **Paid tiers:** Personal archive access NT$10,000/year or NT$6,000/6 months for articles older than 6 months
- **Enterprise:** B2B wire subscriptions, advertising, content licensing — contact `mia@mail.cna.com.tw` (sales) or `cnanews@mail.cna.com.tw` (newsroom)
- **Notes:** CNA is a state-run non-profit organization (since 1996); receives partial funding from Taiwan's Executive Yuan

## Authentication

None for current English news. Archive subscription requires a personal account login.

## Endpoints

- **Base URL:** `https://focustaiwan.tw/`
- **Key endpoints:**
  - Section pages (HTML): `/politics`, `/cross-strait`, `/business`, `/society`, `/sci-tech`, `/sports`, `/culture`
  - Main news landing: `/news`
  - RSS feeds are not prominently documented; site primarily supports direct page consumption and three official news apps (Chinese, English, Japanese)

## Example call

```bash
# Latest news landing page (HTML)
curl "https://focustaiwan.tw/news"

# Politics section
curl "https://focustaiwan.tw/politics"
```

## Rate limits

Not publicly documented.

## SDKs / Libraries

- **Official:** Three CNA mobile apps (Chinese / English / Japanese) — consumer-facing, not developer SDKs
- **Community:** None notable

## Documentation

- Site: https://focustaiwan.tw/
- About CNA: https://focustaiwan.tw/aboutus
- Subscription/archive: https://focustaiwan.tw/subscription
- CNA Chinese site: https://www.cna.com.tw/

## Notes

CNA is the only multilingual news platform in Taiwan, publishing in Chinese, English, and Japanese with 30+ overseas correspondent locations. Editorial focus is government statements, official announcements, and major social events; not a tabloid. No public REST/JSON API or prominent RSS surface — programmatic consumption typically requires HTML scraping or contracting for the wire service. For a paywall-free, RSS-rich Taiwan source, Taipei Times is an alternative (not yet cataloged).
