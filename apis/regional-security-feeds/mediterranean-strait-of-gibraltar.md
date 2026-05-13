# Mediterranean & Strait of Gibraltar — Regional Security Feeds

Curated RSS and news feeds covering security incidents, migrant smuggling, arms trafficking, and maritime threat reporting for the Western Mediterranean, Strait of Gibraltar, Central Mediterranean, and adjacent North African coast.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-13

## Use cases

- Monitoring migrant smuggling operations and interdictions in the Central Mediterranean and Gibraltar Strait
- Tracking Libyan conflict developments affecting port and coastal security along North Africa
- Aggregating security news from Morocco, Algeria, Tunisia, Libya, and southern European ports

## Pricing

- **Free tier:** All feeds are freely accessible RSS endpoints
- **Paid tiers:** None
- **Enterprise:** N/A
- **Notes:** Feed availability and update frequency vary by source; verify URLs before production deployment.

## Authentication

No authentication required for any listed feed.

## Endpoints

**North African news:**
- Libya Observer (English): `https://www.libyaobserver.ly/feed` — verify before use (English-language Libyan news; inferred WordPress pattern)
- Libya Herald (English): `https://www.libyaherald.com/feed/` — verify before use (established English-language Libyan news outlet)
- Morocco World News: `https://www.moroccoworldnews.com/feed/` — verify before use (Morocco English-language news)

**Pan-African aggregation:**
- AllAfrica: `https://allafrica.com/tools/headlines/rdf.php?category=latest` — covers North African and sub-Saharan stories in English

**Law enforcement:**
- Europol newsroom: `https://www.europol.europa.eu/cms/api/rss/news` — confirmed live; covers migrant smuggling networks, Mediterranean drug trafficking operations

**Security & crisis analysis:**
- International Crisis Group MENA: `https://www.crisisgroup.org/rss/81` — confirmed live; covers Libya, Tunisia, Algeria, and Sahel conflicts

**Government advisories:**
- U.S. State Dept Travel Advisories: `https://travel.state.gov/_res/rss/TAsTWs.xml` — confirmed live; monitor for Libya (L4), Algeria (L2), Tunisia (L2) level changes

## Example call

```python
import feedparser

feeds = {
    "Europol": "https://www.europol.europa.eu/cms/api/rss/news",
    "ICG MENA": "https://www.crisisgroup.org/rss/81",
    "AllAfrica": "https://allafrica.com/tools/headlines/rdf.php?category=latest",
    "State Dept": "https://travel.state.gov/_res/rss/TAsTWs.xml",
}
for name, url in feeds.items():
    feed = feedparser.parse(url)
    print(f"{name}: {len(feed.entries)} entries")
```

## Rate limits

Not published for any source. Poll individual feeds no more than once every 15–30 minutes.

## SDKs / Libraries

- **Official:** None — standard RSS/Atom
- **Community:** `feedparser` (Python), `rss-parser` (Node.js)

## Documentation

- Libya Observer: https://www.libyaobserver.ly
- Libya Herald: https://www.libyaherald.com
- Morocco World News: https://www.moroccoworldnews.com
- International Crisis Group MENA: https://www.crisisgroup.org/middle-east-north-africa
- Europol newsroom: https://www.europol.europa.eu/newsroom

## Notes

- The Central Mediterranean route (Libya/Tunisia to Italy/Malta) is Europe's primary irregular migration corridor; Europol's EMPACT migrant smuggling operations generate frequent newsroom updates.
- Libya has no functioning central government; security developments in Tripoli, Misrata, and Benghazi ports are highly volatile and directly impact shipping in the Central Mediterranean.
- Libya Observer and Libya Herald WordPress patterns are inferred — both outlets are active English-language sources and likely support RSS, but verify URLs before production use.
- Frontex (EU border agency) publishes situational reports and risk analyses at https://frontex.europa.eu/media-centre/news/ — no RSS feed available; monitor manually or scrape.
- The Strait of Gibraltar (8.9 miles at narrowest) is also a primary drug trafficking corridor; Europol and Spanish Guardia Civil operations are frequently announced via the Europol newsroom.
