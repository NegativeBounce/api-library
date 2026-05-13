# Europol Newsroom RSS

Europol's official RSS feed delivering press releases on EU-wide law enforcement operations, organized crime takedowns, drug busts, human trafficking, and cross-border criminal investigations.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-13

## Use cases

- Monitoring major European organized crime operations relevant to port security and smuggling
- Tracking cross-border drug trafficking and human smuggling operations affecting maritime chokepoints
- Alerting on Europol joint investigation team (JIT) outcomes involving maritime crime

## Pricing

- **Free tier:** Unlimited; public RSS feed with no registration required
- **Paid tiers:** None
- **Enterprise:** N/A
- **Notes:** Feed is updated whenever Europol publishes a press release; no credit or quota system.

## Authentication

No authentication required. The RSS feed is publicly accessible.

## Endpoints

- **Base URL:** `https://www.europol.europa.eu/`
- **Key endpoints:**
  - `GET /cms/api/rss/news` — full Europol newsroom RSS feed (press releases, operations, publications)

Companion feed:
  - Eurojust newsroom RSS: `https://www.eurojust.europa.eu/rss-feeds` (EU judicial cooperation agency; covers joint trial teams and cross-border prosecution outcomes)

## Example call

```bash
curl "https://www.europol.europa.eu/cms/api/rss/news"
```

```python
import feedparser

feed = feedparser.parse("https://www.europol.europa.eu/cms/api/rss/news")
for entry in feed.entries:
    print(entry.title, entry.published, entry.link)
```

## Rate limits

Not published. As a public RSS feed, apply standard crawl etiquette: poll no more than once every 15–30 minutes.

## SDKs / Libraries

- **Official:** None — standard RSS/Atom; parse with any feed library
- **Community:** `feedparser` (Python), `rss-parser` (Node.js)

## Documentation

- Europol newsroom: https://www.europol.europa.eu/newsroom
- Eurojust RSS: https://www.eurojust.europa.eu/rss-feeds

## Notes

- Feed covers EU member state joint operations; most items involve drug trafficking, migrant smuggling, cybercrime, and financial crime — all relevant to port and maritime threat monitoring.
- Europol's EMPACT (European Multidisciplinary Platform Against Criminal Threats) operations are regularly announced through this feed.
- For bulk historical data, Europol publishes annual "Serious and Organised Crime Threat Assessment" (SOCTA) reports as PDFs on their website.
- Eurojust feed covers judicial coordination and extradition news, complementing Europol's operational coverage.
