# Splash 247

Independent global maritime, shipping, and offshore news outlet with exclusive reporting and in-depth analysis.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-06-11

## Use cases

- Daily shipping, offshore, and maritime-business news with frequent exclusives and opinion/analysis.
- Atmospherics on markets, owners/operators, decarbonisation, and regional security developments.
- Complementary coverage to gCaptain and Maritime Executive for cross-checking incident reporting.

## Pricing

- **Free tier:** Free web access and RSS.
- **Paid tiers:** None required.
- **Enterprise:** N/A.
- **Notes:** Independent; founded by veteran maritime journalists.

## Authentication

None for public articles/RSS.

## Endpoints

- **Base URL:** `https://splash247.com`
- **Key surfaces:**
  - RSS: `https://splash247.com/feed/`
  - Site: `https://splash247.com/`

## Example call

```python
import feedparser
feed = feedparser.parse("https://splash247.com/feed/")
print(len(feed.entries), "entries")
```

## Rate limits

Not published. Poll RSS no more than once every 15–30 minutes.

## SDKs / Libraries

- **Official:** None — standard RSS/Atom (WordPress feed).
- **Community:** `feedparser` (Python), `rss-parser` (Node.js).

## Documentation

- Main site: https://splash247.com

## Notes

- Useful third independent voice alongside gCaptain and The Maritime Executive; strong on analysis and commentary.
- Cross-reference: `maritime-media/gcaptain.md`, `maritime-media/the-maritime-executive.md`; referenced as a feed in several `regional-security-feeds/` entries.
