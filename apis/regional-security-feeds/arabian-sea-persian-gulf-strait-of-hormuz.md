# Arabian Sea, Persian Gulf & Strait of Hormuz — Regional Security Feeds

Curated RSS and news feeds covering security incidents, geopolitical developments, and maritime threat reporting for the Arabian Sea, Persian Gulf, Gulf of Oman, and Strait of Hormuz region.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-13

## Use cases

- Monitoring Iranian naval activity, IRGC seizures, and Strait of Hormuz transit disruptions
- Tracking Houthi and proxy threat developments affecting Gulf shipping lanes
- Aggregating regional crime and unrest news from Oman, UAE, Saudi Arabia, Iran, and Pakistan

## Pricing

- **Free tier:** All feeds are freely accessible RSS endpoints
- **Paid tiers:** None
- **Enterprise:** N/A
- **Notes:** Feed availability and update frequency vary by source; verify URLs before production deployment.

## Authentication

No authentication required for any listed feed.

## Endpoints

**Maritime-specific:**
- gCaptain maritime news: `https://feeds.feedburner.com/gcaptain` — confirmed live; covers Gulf tanker incidents, Hormuz transits, IRGC seizures
- Splash247 maritime: `https://splash247.com/feed/` — verify before use (inferred WordPress pattern)

**Regional news:**
- Arab News Middle East: `https://www.arabnews.com/cat/2/rss.xml` — confirmed live; Saudi-based English-language regional coverage
- Gulf News world: `https://gulfnews.com/rss/world` — verify before use (UAE-based English regional news)
- Times of Oman: `https://timesofoman.com/rss` — verify before use (Oman English-language news)

**Security & crisis analysis:**
- International Crisis Group MENA: `https://www.crisisgroup.org/rss/81` — confirmed live; expert analysis on Gulf and Arabian Peninsula conflicts

**Government advisories:**
- U.S. State Dept Travel Advisories: `https://travel.state.gov/_res/rss/TAsTWs.xml` — confirmed live; monitor for Yemen (L4), Iran (L4), Iraq (L4) level changes

## Example call

```python
import feedparser

feeds = {
    "gCaptain": "https://feeds.feedburner.com/gcaptain",
    "Arab News": "https://www.arabnews.com/cat/2/rss.xml",
    "ICG MENA": "https://www.crisisgroup.org/rss/81",
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

- gCaptain: https://gcaptain.com
- Arab News: https://www.arabnews.com
- International Crisis Group MENA: https://www.crisisgroup.org/middle-east-north-africa
- Gulf News: https://gulfnews.com

## Notes

- The Strait of Hormuz is the world's most critical oil chokepoint (~20% of global petroleum supply). Incidents here generate immediate commodity market impact — high-priority feed for maritime security dashboards.
- IRGC tanker seizures (Iran's Islamic Revolutionary Guard Corps) are frequently first reported via gCaptain before mainstream media.
- Splash247 and Gulf News use inferred WordPress RSS patterns — verify these URLs are live before integrating.
- Seatrade Maritime (`https://www.seatrade-maritime.com/rss/xml`) may also carry Gulf shipping coverage — verify before use.
- MARAD advisories for the Persian Gulf/Gulf of Oman are email-only; subscribe at https://www.maritime.dot.gov/msci.
