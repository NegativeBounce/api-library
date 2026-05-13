# East Africa & Indian Ocean — Regional Security Feeds

Curated RSS and news feeds covering security incidents, piracy, and maritime threat reporting for the East African coast, Mozambique Channel, Seychelles, and the western Indian Ocean shipping lanes.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-13

## Use cases

- Monitoring piracy resurgence and armed robbery incidents in the western Indian Ocean
- Tracking security developments in Tanzania, Mozambique, Madagascar, and island port states
- Aggregating East African coastal crime and political instability news affecting shipping

## Pricing

- **Free tier:** All feeds are freely accessible RSS endpoints
- **Paid tiers:** None
- **Enterprise:** N/A
- **Notes:** Feed availability and update frequency vary by source; verify URLs before production deployment.

## Authentication

No authentication required for any listed feed.

## Endpoints

**East African news:**
- Nation Africa (Kenya): `https://nation.africa/feed/` — verify before use (inferred WordPress pattern; Kenya's leading English-language daily)
- Citizen Digital (Kenya): `https://www.citizen.digital/feed/` — verify before use (inferred WordPress pattern; Nairobi-based English news)
- The Citizen Tanzania: `https://www.thecitizen.co.tz/tanzania/feed/` — verify before use (Tanzania English-language daily)

**Pan-African coverage:**
- AllAfrica: `https://allafrica.com/tools/headlines/rdf.php?category=latest` — aggregates stories from 130+ African news outlets; broad East Africa coverage
- Africa Defense Forum: `https://adf-magazine.com/feed/` — verify before use (U.S. AFRICOM-funded; covers regional security and military operations)

**Maritime-specific:**
- gCaptain: `https://feeds.feedburner.com/gcaptain` — confirmed live; covers Indian Ocean piracy and shipping incidents

**Security & crisis analysis:**
- International Crisis Group Africa: `https://www.crisisgroup.org/rss/1` — confirmed live; covers Somalia, Ethiopia, Mozambique, and Great Lakes conflicts

**Government advisories:**
- U.S. State Dept Travel Advisories: `https://travel.state.gov/_res/rss/TAsTWs.xml` — confirmed live; monitor for Somalia (L4), Ethiopia (L3), Mozambique (L2/L3) changes

## Example call

```python
import feedparser

feeds = {
    "AllAfrica": "https://allafrica.com/tools/headlines/rdf.php?category=latest",
    "gCaptain": "https://feeds.feedburner.com/gcaptain",
    "ICG Africa": "https://www.crisisgroup.org/rss/1",
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

- Nation Africa: https://nation.africa
- AllAfrica: https://allafrica.com
- International Crisis Group Africa: https://www.crisisgroup.org/africa
- gCaptain: https://gcaptain.com

## Notes

- East Africa Indian Ocean piracy declined sharply after 2012 but has shown periodic resurgence; the region warrants continuous monitoring.
- The Mozambique Channel is increasingly significant due to LNG developments and insurgent activity in Cabo Delgado province — relevant to tanker and LNG carrier routing.
- Somalia remains a Level 4 (Do Not Travel) designation; any advisory changes from the State Dept feed for Somalia are high-priority alerts.
- Nation Africa and Citizen Digital WordPress patterns are inferred — verify live URLs before integrating into production pipelines.
- INTERPOL's East Africa Regional Bureau in Nairobi coordinates cross-border crime response; Europol news feed (`europol-newsroom.md`) may carry relevant joint operation announcements.
