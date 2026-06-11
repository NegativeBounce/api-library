# The Maritime Executive

Maritime news, analysis, and the "In the Know" podcast covering shipping, ports, offshore energy, security, and technology.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-06-11

## Use cases

- Industry news and analysis on ports, carriers, sanctions, naval/security developments, and maritime technology.
- The "In the Know" podcast — editor interviews with port executives, security leaders, and marine-tech principals (useful for atmospherics and tech-tracking).
- Tracking commercial and policy developments (e.g. USTR fees, terminal investments, LNG/sanctions evasion).

## Pricing

- **Free tier:** Free web access, RSS, podcast, and newsletter.
- **Paid tiers:** None required.
- **Enterprise:** N/A.
- **Notes:** Long-running maritime trade publication.

## Authentication

None for public articles, RSS, or podcast.

## Endpoints

- **Base URL:** `https://www.maritime-executive.com`
- **Key surfaces:**
  - News: `https://www.maritime-executive.com/`
  - Podcast: `https://maritime-executive.com/podcast`
  - RSS: `https://www.maritime-executive.com/rss` (verify before use)

## Example call

```python
import feedparser
feed = feedparser.parse("https://www.maritime-executive.com/rss")  # verify URL
print(len(feed.entries), "entries")
```

## Rate limits

Not published. Poll RSS no more than once every 15–30 minutes.

## SDKs / Libraries

- **Official:** None — standard RSS/Atom; podcast via standard podcast RSS.
- **Community:** `feedparser` (Python), `rss-parser` (Node.js).

## Documentation

- Main site: https://www.maritime-executive.com
- Podcast: https://maritime-executive.com/podcast

## Notes

- Strong for **analysis + interviews** rather than raw breaking speed (where gCaptain leads); the podcast is a good marsec-tech and executive-atmospherics input.
- RSS URL pattern should be verified before production integration.
- Cross-reference: `maritime-media/gcaptain.md`, `maritime-media/splash247.md`, `maritime-media/cimsec.md`.
