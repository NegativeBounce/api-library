# The Loadstar

Independent supply-chain, freight, and logistics news outlet covering container shipping, ports, air cargo, and the landside supply chain.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-06-11

## Use cases

- Container-shipping and port news (congestion, carrier moves, freight rates) for commercial/logistics atmospherics.
- Landside supply-chain coverage that intersects cargo-crime and port-disruption intelligence.
- Cross-checking the logistics/economic context behind maritime-security and congestion events.

## Pricing

- **Free tier:** Free web access and RSS.
- **Paid tiers:** Premium/membership options exist but most news is free.
- **Enterprise:** N/A.
- **Notes:** Independent; strong on container/logistics analysis.

## Authentication

None for public articles/RSS.

## Endpoints

- **Base URL:** `https://theloadstar.com`
- **Key surfaces:**
  - Site: `https://theloadstar.com/`
  - RSS: `https://theloadstar.com/feed/` (verify before use)

## Example call

```python
import feedparser
feed = feedparser.parse("https://theloadstar.com/feed/")  # verify URL
print(len(feed.entries), "entries")
```

## Rate limits

Not published. Poll RSS no more than once every 30 minutes.

## SDKs / Libraries

- **Official:** None — standard RSS/Atom.
- **Community:** `feedparser` (Python), `rss-parser` (Node.js).

## Documentation

- Main site: https://theloadstar.com

## Notes

- Bridges **maritime and landside logistics** — useful for the supply-chain/port-congestion and cargo-crime context that pure marsec outlets don't cover.
- Cross-reference: `maritime-media/tradewinds.md`, `port-congestion/`, and the `cargo-crime/` category.
