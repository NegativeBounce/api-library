# South China Sea — Regional Security Feeds

Curated RSS and news feeds covering territorial disputes, naval confrontations, and maritime security incidents in the South China Sea, including the Spratly Islands, Paracel Islands, and key chokepoints.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-13

## Use cases

- Monitoring Chinese Coast Guard and PLAN (People's Liberation Army Navy) confrontations with Philippine, Vietnamese, and Malaysian vessels
- Tracking territorial dispute escalations at disputed reefs, shoals, and island features
- Aggregating regional security and political news from Philippines, Vietnam, Malaysia, Brunei, and Taiwan affecting SCS transit safety

## Pricing

- **Free tier:** All feeds are freely accessible RSS endpoints
- **Paid tiers:** None
- **Enterprise:** N/A
- **Notes:** Feed availability and update frequency vary by source; verify URLs before production deployment.

## Authentication

No authentication required for any listed feed.

## Endpoints

**SCS-specific analysis:**
- AMTI / CSIS Asia Maritime Transparency Initiative: `https://amti.csis.org/feed/` — verify before use (definitive source for SCS island-building, confrontations, and satellite analysis)
- Radio Free Asia South China Sea: `https://www.rfa.org/english/news/southchinasea/feed` — verify before use (RFA SCS-specific news feed)

**Regional news:**
- Philippine News Agency: `https://www.pna.gov.ph/feed` — verify before use (Philippines government news wire; covers SCS incidents from Philippine perspective)
- South China Morning Post SCS: `https://www.scmp.com/rss/5/feed` — verify before use (SCMP regional feed; covers SCS and China-ASEAN relations)

**Security & crisis analysis:**
- International Crisis Group Asia-Pacific: `https://www.crisisgroup.org/rss/30` — confirmed live; covers Southeast Asia and broader Indo-Pacific security

**Government advisories:**
- U.S. State Dept Travel Advisories: `https://travel.state.gov/_res/rss/TAsTWs.xml` — confirmed live; monitor advisory changes for Philippines, Vietnam, Malaysia, Taiwan

## Example call

```python
import feedparser

feeds = {
    "ICG Asia-Pacific": "https://www.crisisgroup.org/rss/30",
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

- AMTI/CSIS: https://amti.csis.org
- Radio Free Asia: https://www.rfa.org/english/news/southchinasea
- Philippine News Agency: https://www.pna.gov.ph
- SCMP: https://www.scmp.com

## Notes

- AMTI (Asia Maritime Transparency Initiative) is the most authoritative open-source monitoring resource for SCS developments — satellite imagery analysis, incident mapping, and policy tracking. Their RSS feed is inferred; verify before use.
- The South China Sea carries ~$3.4 trillion in annual trade; the Taiwan Strait and Luzon Strait are critical commercial shipping lanes within this region.
- Philippine News Agency (PNA) is a primary source for incidents at Second Thomas Shoal, Scarborough Shoal, and other Philippines-administered features — URL pattern is inferred.
- SCMP's SCS feed (category 5) is inferred from their RSS structure — verify the correct category ID before production use.
- The U.S. 7th Fleet and Indo-Pacific Command (INDOPACOM) publish Freedom of Navigation Operation (FONOP) statements at https://www.pacom.mil/Media/News/ — no RSS available; monitor manually.
