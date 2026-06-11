# gCaptain

Leading independent maritime news site providing real-time shipping, offshore, and maritime-security reporting via web and RSS.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-06-11

## Use cases

- Fastest reliable English-language reporting on vessel attacks and maritime-security incidents (Red Sea, Hormuz, Black Sea) — often within hours.
- Daily situational "atmospherics" on shipping, offshore energy, sanctions enforcement, and naval activity.
- Monitoring regulatory and industry developments affecting global shipping.

## Pricing

- **Free tier:** Free web access and RSS; free newsletter and account tiers.
- **Paid tiers:** None required for news (membership/club options exist).
- **Enterprise:** N/A.
- **Notes:** Independent; one of the most-read maritime news outlets.

## Authentication

None for public articles/RSS.

## Endpoints

- **Base URL:** `https://gcaptain.com`
- **Key surfaces:**
  - RSS: `https://feeds.feedburner.com/gcaptain`
  - News category: `https://gcaptain.com/category/news/`

## Example call

```python
import feedparser
feed = feedparser.parse("https://feeds.feedburner.com/gcaptain")
print(len(feed.entries), "entries")
for e in feed.entries[:5]:
    print(e.title)
```

## Rate limits

Not published. Poll RSS no more than once every 15–30 minutes.

## SDKs / Libraries

- **Official:** None — standard RSS/Atom.
- **Community:** `feedparser` (Python), `rss-parser` (Node.js).

## Documentation

- Main site: https://gcaptain.com
- RSS: https://feeds.feedburner.com/gcaptain

## Notes

- The single most useful free real-time source for breaking maritime-security incidents; already referenced across the `regional-security-feeds/` entries.
- Pair with official reporting centres (`maritime-security/ukmto.md`) and analysis outlets (`maritime-media/the-maritime-executive.md`, `maritime-media/cimsec.md`) for a full atmospherics picture.
