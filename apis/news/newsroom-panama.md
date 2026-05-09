# Newsroom Panama

An independent English-language Panama-specialist news outlet covering politics, business, the Panama Canal, tourism, and society. Founded by veteran journalist Eric Jackson; positions itself as one of the few English-only news destinations focused exclusively on Panama.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-09

## Use cases

- Panama breaking news in English (politics, presidential affairs, Panama Canal Authority, banking)
- Tracking Panama Canal traffic, drought-driven transit restrictions, expansion projects, and global shipping implications
- Following Panama financial sector and offshore-finance developments (especially post-Panama Papers)
- Building Latin America and Caribbean news readers with Panama-specific English depth, complementing MercoPress regional coverage and Tico Times Costa Rica coverage

## Pricing

- **Free tier:** Full website access free
- **Paid tiers:** None publicly documented; potential reader donation channel
- **Enterprise:** Advertising via direct contact with the publication
- **Notes:** Funded primarily through advertising and reader support; small-team independent operation

## Authentication

None.

## Endpoints

- **Base URL:** `https://www.newsroompanama.com/`
- **Key endpoints:**
  - Main site: `https://www.newsroompanama.com/`
  - RSS feed: `https://www.newsroompanama.com/feed/` (typical WordPress pattern; verify on integration)
  - Section pages (HTML): news, politics, business, society, sports, opinion
- **Important caveat:** verify site liveness and current URL pattern at integration time. Smaller English Panama outlets have a history of going dormant, changing platforms, or merging with other regional sources.

## Example call

```bash
# Main site
curl "https://www.newsroompanama.com/"

# RSS feed (verify exact path on first integration)
curl "https://www.newsroompanama.com/feed/"
```

## Rate limits

Not publicly documented.

## SDKs / Libraries

- **Official:** None for the public RSS surface
- **Community:** Standard RSS parsers

## Documentation

- Main site: https://www.newsroompanama.com/
- Operator: founder Eric Jackson, veteran Panama-focused English journalist (also operates `thepanamanews.com` historically)

## Notes

Newsroom Panama is **independent** and operates as one of the few English-only Panama-specialist news outlets. The Panama English-language media landscape is small relative to Spanish (which has heavyweights `La Prensa Panama`, `La Estrella de Panamá`, and `TVN-2`), so Newsroom Panama and similar small operations fill a niche for international readers, expats, retirees, and shipping-industry professionals. Coverage strongest on Panama Canal, banking/finance, presidential politics, and Panamanian-specific economic developments.

**Important verification caveat:** the Panama English news space has historically been volatile — sites have gone dormant or changed platforms with little notice (`panamapost.com`, `panama-guide.com`, `thepanamanews.com` have all had availability issues at various points). At integration time, verify (a) site is live, (b) RSS feed is reachable, (c) recent publishing cadence is healthy. If Newsroom Panama is not reachable, alternative English Panama sources include `newsroompanama.com`'s sister sites historically operated by Eric Jackson, plus aggregator entries via MercoPress (`/rss` includes Panama coverage as part of regional Mercosur-adjacent reporting) and InSight Crime (Panama crime/security coverage from a US-based investigative perspective).

For source-trust analysis: independent, no government affiliation, expat/international-audience-oriented editorial. **Coverage gap to flag:** Newsroom Panama is small relative to El Faro or Confidencial; for primary-source Panama news at scale, Spanish-language `La Prensa Panama` (`prensa.com`) is the dominant national paper. No public REST/JSON developer API documented.
