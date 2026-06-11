# Riviera Maritime Media

Maritime B2B publisher producing news, technical magazines, webinars, and whitepapers across shipping sectors and maritime technology.

**Tier:** Free
**Auth:** None (content) / Registration (webinars)
**Last researched:** 2026-06-11

## Use cases

- Technical and sector news (tankers, gas, offshore, ship operations, decarbonisation, maritime cyber/security).
- Webinars and whitepapers — a strong source of vendor/technical deep-dives for marsec-tech and operational-technology atmospherics.
- Tracking emerging maritime technology and regulatory/technical guidance.

## Pricing

- **Free tier:** Free articles, newsletters; free webinars/whitepapers (registration).
- **Paid tiers:** None required for most content.
- **Enterprise:** N/A.
- **Notes:** B2B publisher; whitepapers are often vendor-sponsored (read with that lens).

## Authentication

None for articles/RSS; free registration for webinars/whitepaper downloads.

## Endpoints

- **Base URL:** `https://www.rivieramm.com`
- **Key surfaces:**
  - Site: `https://www.rivieramm.com/`
  - RSS: `https://www.rivieramm.com/rss` (verify before use)
  - Webinars/whitepapers: `https://www.rivieramm.com/webinars`

## Example call

```python
import feedparser
feed = feedparser.parse("https://www.rivieramm.com/rss")  # verify URL
print(len(feed.entries), "entries")
```

## Rate limits

Not published. Poll RSS no more than once every 30–60 minutes.

## SDKs / Libraries

- **Official:** None — standard RSS/Atom.
- **Community:** `feedparser` (Python), `rss-parser` (Node.js).

## Documentation

- Main site: https://www.rivieramm.com

## Notes

- The strongest entry for **whitepapers and webinars** as intelligence inputs — useful for tracking maritime cyber/OT-security and emerging tech, with the caveat that sponsored content reflects vendor positioning.
- Cross-reference: `maritime-media/marinelink.md`, `maritime-media/safety4sea.md`; for OT-security products see `port-ot-security/`.
