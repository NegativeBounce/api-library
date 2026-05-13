# U.S. State Department Travel Advisories RSS

The U.S. State Department's official RSS feed publishing country-level travel advisory changes, including security level updates (Levels 1–4) and emergency alerts for U.S. citizens abroad.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-13

## Use cases

- Real-time alerting when the U.S. government upgrades a country's security level (e.g., Level 3 "Reconsider Travel" or Level 4 "Do Not Travel")
- Monitoring advisory changes for countries along key maritime shipping routes and chokepoints
- Providing contextual security status for port regions covered by the dashboard

## Pricing

- **Free tier:** Unlimited; no registration required
- **Paid tiers:** None
- **Enterprise:** N/A
- **Notes:** Public U.S. government data feed; no SLA or uptime guarantee.

## Authentication

No authentication required. All RSS feeds are publicly accessible.

## Endpoints

- **Key feeds:**
  - `https://travel.state.gov/_res/rss/TAsTWs.xml` — all Travel Advisories and Travel Warnings (primary feed; confirmed live 2026-05-13)
  - `https://travel.state.gov/_res/rss/TAs.xml` — Travel Alerts only
  - `https://travel.state.gov/_res/rss/RSS_4787.xml` — Worldwide Caution advisory updates

**Advisory levels in feed items:**
  - Format: `{Country} - Level {N}: {Description}`
  - Level 1: Exercise Normal Precautions
  - Level 2: Exercise Increased Caution
  - Level 3: Reconsider Travel
  - Level 4: Do Not Travel

## Example call

```bash
curl "https://travel.state.gov/_res/rss/TAsTWs.xml"
```

```python
import feedparser

feed = feedparser.parse("https://travel.state.gov/_res/rss/TAsTWs.xml")
for entry in feed.entries:
    print(entry.title, entry.published, entry.link)
    # entry.title format: "Somalia - Level 4: Do Not Travel"
```

## Rate limits

Not published. As a public RSS feed, poll no more than once every 15–30 minutes. Advisory updates are irregular — typically multiple times per week, not multiple times per day.

## SDKs / Libraries

- **Official:** None — standard RSS/Atom feed
- **Community:** `feedparser` (Python), `rss-parser` (Node.js); `github.com/Aureum01/StateGovTravelAdvisory` (Python wrapper for advisory data)

## Documentation

- Travel advisories portal: https://travel.state.gov/content/travel/en/traveladvisories/traveladvisories.html/
- RSS feed info: https://travel.state.gov/content/travel/en/traveladvisories/traveladvisories.html/

## Notes

- Advisory level changes for maritime-critical countries are high-signal events: Somalia (L4), Yemen (L4), Libya (L4), Nigeria (L3), Iraq (L4) are typical high-risk designations.
- The feed includes `pubDate` in standard RFC 822 format, enabling easy timestamp parsing and change detection.
- For country-level detail behind each advisory, OSAC Country Security Reports (`osac.md`) provide deeper threat environment context.
- MARAD (U.S. Maritime Administration) advisories are email-list-only with no RSS feed — subscribe separately at https://www.maritime.dot.gov/msci for maritime-specific security communications.
- The Worldwide Caution feed (`RSS_4787.xml`) updates infrequently but covers global terrorism and organized crime trends relevant to all maritime regions.
