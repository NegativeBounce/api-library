# Panama Canal & Caribbean — Regional Security Feeds

Curated RSS and news feeds covering security incidents, drug trafficking, organized crime, and maritime threat reporting for the Panama Canal, Caribbean Sea, and adjacent Central American and island port regions.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-13

## Use cases

- Monitoring drug trafficking interdictions and cartel activity affecting Canal Zone and Caribbean shipping lanes
- Tracking political instability and port security developments in Panama, Colombia, Venezuela, and Caribbean island states
- Aggregating organized crime and gang violence news affecting major Caribbean transit ports (Kingston, Port of Spain, Cartagena)

## Pricing

- **Free tier:** All feeds are freely accessible RSS endpoints
- **Paid tiers:** None
- **Enterprise:** N/A
- **Notes:** Feed availability and update frequency vary by source; verify URLs before production deployment.

## Authentication

No authentication required for any listed feed.

## Endpoints

**Organized crime & security analysis:**
- InSight Crime: `https://insightcrime.org/rss/` — confirmed (429 returned during research; URL confirmed via documentation); leading English-language Latin American organized crime outlet

**Panama & Central America:**
- Newsroom Panama: `https://www.newsroompanama.com/feed/` — verify before use (English-language Panama news; inferred WordPress pattern)

**Caribbean news:**
- Jamaica Gleaner: `https://jamaica-gleaner.com/feed/` — verify before use (Jamaica's leading English daily)
- Trinidad Express: `https://trinidadexpress.com/feed/` — verify before use (Trinidad & Tobago English-language daily)
- Caribbean Journal: `https://caribjournal.com/feed/` — verify before use (English-language Caribbean news aggregator)

**Security & crisis analysis:**
- International Crisis Group Latin America: `https://www.crisisgroup.org/rss/73` — confirmed live; covers Venezuela, Colombia, and Central American conflicts

**Government advisories:**
- U.S. State Dept Travel Advisories: `https://travel.state.gov/_res/rss/TAsTWs.xml` — confirmed live; monitor for Venezuela (L4), Haiti (L4), Colombia (L3), Jamaica (L3) level changes

## Example call

```python
import feedparser

feeds = {
    "InSight Crime": "https://insightcrime.org/rss/",
    "ICG LatAm": "https://www.crisisgroup.org/rss/73",
    "State Dept": "https://travel.state.gov/_res/rss/TAsTWs.xml",
}
for name, url in feeds.items():
    feed = feedparser.parse(url)
    print(f"{name}: {len(feed.entries)} entries")
```

## Rate limits

Not published for any source. InSight Crime rate-limited during research (429 response) — poll no more than once every 30 minutes. All other feeds: poll no more than once every 15–30 minutes.

## SDKs / Libraries

- **Official:** None — standard RSS/Atom
- **Community:** `feedparser` (Python), `rss-parser` (Node.js)

## Documentation

- InSight Crime: https://insightcrime.org
- International Crisis Group Latin America: https://www.crisisgroup.org/latin-america-caribbean
- Newsroom Panama: https://www.newsroompanama.com
- Jamaica Gleaner: https://jamaica-gleaner.com

## Notes

- InSight Crime is the authoritative English-language source for Latin American organized crime reporting; their Panama, Venezuela, and Colombia coverage is essential for Canal Zone threat monitoring.
- The Panama Canal handles ~5% of global trade; drought-related capacity restrictions (2023–2024) and cartel activity near Colón make it a persistent monitoring priority.
- Venezuela (L4) and Haiti (L4) State Dept advisories are persistent high-risk designations; any change is a high-priority signal.
- The USS Coast Guard (USCG) issues maritime security communications for Caribbean waters — email-subscription-only, no RSS. Subscribe at https://www.navcen.uscg.gov/ for NAVTEX and NOTMAR alerts.
- Newsroom Panama, Jamaica Gleaner, Trinidad Express, and Caribbean Journal use inferred WordPress patterns — verify before production integration.
