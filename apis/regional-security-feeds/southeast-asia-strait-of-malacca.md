# Southeast Asia & Strait of Malacca — Regional Security Feeds

Curated RSS and news feeds covering piracy, armed robbery, smuggling, and maritime security incidents in the Strait of Malacca, Singapore Strait, Sunda Strait, and surrounding Southeast Asian waters.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-13

## Use cases

- Monitoring piracy and armed robbery against vessels in the Strait of Malacca and Singapore Strait
- Tracking terrorist threats and maritime security developments involving Abu Sayyaf and other regional groups
- Aggregating security news from Malaysia, Indonesia, Singapore, Thailand, and Philippines affecting Malacca transit

## Pricing

- **Free tier:** All feeds are freely accessible RSS endpoints
- **Paid tiers:** None
- **Enterprise:** N/A
- **Notes:** Feed availability and update frequency vary by source; verify URLs before production deployment.

## Authentication

No authentication required for any listed feed.

## Endpoints

**Regional news (English-language):**
- Channel NewsAsia (Singapore): `https://www.channelnewsasia.com/rssfeeds/8395744` — verify before use (CNA Singapore; authoritative Southeast Asia English-language source)
- New Straits Times (Malaysia): `https://www.nst.com.my/feed` — verify before use (Malaysia leading English-language daily)
- The Jakarta Post (Indonesia): `https://www.thejakartapost.com/feed` — verify before use (Indonesia's leading English daily)
- Philippine News Agency: `https://www.pna.gov.ph/feed` — verify before use (Philippines government news wire)
- PhilStar (Philippines): `https://www.philstar.com/rss` — verify before use (Manila-based English broadsheet)

**Security & crisis analysis:**
- International Crisis Group Asia-Pacific: `https://www.crisisgroup.org/rss/30` — confirmed live; covers Myanmar, Indonesia, Philippines, and regional maritime conflicts

**Government advisories:**
- U.S. State Dept Travel Advisories: `https://travel.state.gov/_res/rss/TAsTWs.xml` — confirmed live; monitor advisory changes for Philippines (L2/L3 by region), Indonesia (L2), Myanmar (L4)

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

- Channel NewsAsia: https://www.channelnewsasia.com
- New Straits Times: https://www.nst.com.my
- The Jakarta Post: https://www.thejakartapost.com
- International Crisis Group Asia: https://www.crisisgroup.org/asia

## Notes

- The Strait of Malacca (~1.7 miles at Phillips Channel, narrowest point) handles ~25% of global trade; it is the world's busiest shipping lane for volume. Piracy and armed robbery incidents are tracked by ReCAAP ISC (Regional Cooperation Agreement on Combating Piracy).
- ReCAAP ISC (https://www.recaap.org) publishes incident reports for the Asia-Pacific region; they offer email alerts and PDF reports but no RSS feed as of 2026-05-13.
- BenarNews, which previously covered Southeast Asian security with an RSS feed, suspended/paused operations in 2025 — do not include this source.
- CNA, NST, Jakarta Post, PNA, and PhilStar all use inferred URL patterns — verify each before production integration.
- Abu Sayyaf Group (Philippines/Malaysia border) and piracy in the Sulu-Celebes Sea are distinct threats from Malacca Strait piracy; ICG Asia-Pacific covers both.
- Myanmar's military conflict has displaced maritime trade patterns through the Andaman Sea — monitor ICG Asia-Pacific feed for routing impact assessments.
