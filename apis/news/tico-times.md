# The Tico Times

Costa Rica's English-language daily online newspaper, founded as a print weekly in 1956 by Richard Dyer and now operating as a digital-first publication based in San José. Free RSS access and a Sunday weekly newsletter; independent ownership.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-09

## Use cases

- Costa Rica breaking news monitoring (politics, presidential transitions, business, environment, expat affairs)
- Tracking Costa Rican government, Central Bank policy, tourism and real estate sectors in English
- Building Latin America news readers oriented toward English-speaking residents and travelers in Central America
- Augmenting MercoPress regional Mercosur coverage with deeper Costa Rica-domestic detail and Central American context

## Pricing

- **Free tier:** All RSS feeds, full website, and weekly Sunday newsletter (`weekly.ticotimes.net`) free
- **Paid tiers:** Optional reader donations via the "Donate" link in the site footer
- **Enterprise:** Costa Rica advertising program; classifieds; "Write For Us" contributor program — contact via main site
- **Notes:** Funded primarily through advertising, classifieds, and reader donations

## Authentication

None.

## Endpoints

- **Base URL:** `https://ticotimes.net/`
- **Key endpoints:**
  - RSS feed (linked in site footer): `https://ticotimes.net/feed/` (typical WordPress pattern; verify on integration)
  - Section pages (HTML): `/categories/news`, `/categories/news/costa-rica-news`, `/categories/business`, `/categories/travel`, `/categories/lifestyle`, `/categories/sports`, `/categories/environment-and-wildlife`
  - Newsletter platform: `https://weekly.ticotimes.net/`
  - Classifieds: `https://ticotimes.net/classifieds`

## Example call

```bash
# Main RSS feed (verify exact path on first integration)
curl "https://ticotimes.net/feed/"

# Costa Rica news section (HTML)
curl "https://ticotimes.net/categories/news/costa-rica-news"
```

## Rate limits

Not publicly documented.

## SDKs / Libraries

- **Official:** None for the public RSS surface
- **Community:** Standard RSS parsers; WordPress-style endpoints

## Documentation

- Main site: https://ticotimes.net/
- Weekly newsletter: https://weekly.ticotimes.net/
- About: https://ticotimes.net/about (linked from site footer)

## Notes

The Tico Times is **independent** and is widely regarded as the English-language newspaper of record for Costa Rica. Founded in 1956 as a printed weekly catering to the English-speaking community, it transitioned to a digital-first model in the 2010s. Coverage is strongest on Costa Rican domestic politics, environmental affairs (one of its most distinctive desks given Costa Rica's biodiversity and conservation focus), tourism, real estate, and expat affairs. Notable for early adoption of online news in Latin America. **For source-trust analysis:** independent, no government affiliation, US-Costa Rica audience-oriented editorial style. **Important domain caveat:** `ticotimes.com` is a separate "Tico Times Directory" travel/business directory site (frozen at 2012) — the news outlet is at `ticotimes.net`. Friendly competitor outlets in the Costa Rica English space include `qcostarica.com` and `news.co.cr`. No public REST/JSON developer API documented.
