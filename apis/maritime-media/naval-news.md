# Naval News

Defense-media outlet focused on naval and maritime-defense technology, programs, and procurement worldwide.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-06-11

## Use cases

- Tracking naval and maritime-security technology: warships, USVs/UUVs, sensors, missiles, counter-drone, and shipyard programs.
- Procurement and capability developments across navies and coast guards — strong marsec-tech atmospherics.
- Coverage of exercises and deployments (e.g. Black Sea, Indo-Pacific) relevant to regional risk.

## Pricing

- **Free tier:** Free web access and RSS.
- **Paid tiers:** None required.
- **Enterprise:** N/A.
- **Notes:** Independent defense-media publisher.

## Authentication

None for public articles/RSS.

## Endpoints

- **Base URL:** `https://www.navalnews.com`
- **Key surfaces:**
  - Site: `https://www.navalnews.com/`
  - RSS: `https://www.navalnews.com/feed/` (verify before use)

## Example call

```python
import feedparser
feed = feedparser.parse("https://www.navalnews.com/feed/")  # verify URL
print(len(feed.entries), "entries")
```

## Rate limits

Not published. Poll RSS no more than once every 30 minutes.

## SDKs / Libraries

- **Official:** None — standard RSS/Atom.
- **Community:** `feedparser` (Python), `rss-parser` (Node.js).

## Documentation

- Main site: https://www.navalnews.com

## Notes

- Best free source specifically for **naval/maritime-defense technology** tracking (USVs, counter-UAS, sensors) — complements MarineLink's commercial-marine-tech focus.
- Cross-reference: `maritime-media/usni-news.md`, `maritime-media/marinelink.md`, `maritime-media/cimsec.md`.
