# CIMSEC (Center for International Maritime Security)

Non-profit publishing reader-submitted analysis on international maritime security and naval affairs, with the Sea Control podcast.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-06-11

## Use cases

- In-depth analysis of maritime-security strategy, grey-zone competition, naval affairs, and emerging maritime threats — strong analyst-grade atmospherics.
- The Sea Control podcast — interviews and discussion on maritime security topics.
- Tracking think-tank-level debate that often precedes mainstream coverage of marsec issues.

## Pricing

- **Free tier:** Free — all articles and podcast.
- **Paid tiers:** None.
- **Enterprise:** N/A (non-profit).
- **Notes:** Reader-submitted/curated content; volunteer-run.

## Authentication

None.

## Endpoints

- **Base URL:** `https://cimsec.org`
- **Key surfaces:**
  - Site: `https://cimsec.org/`
  - Podcast: `https://cimsec.org/podcast-2/`
  - RSS: `https://cimsec.org/feed/` (verify before use)

## Example call

```python
import feedparser
feed = feedparser.parse("https://cimsec.org/feed/")  # verify URL
print(len(feed.entries), "entries")
```

## Rate limits

Not published. Poll RSS no more than once every 30–60 minutes (lower-frequency publisher).

## SDKs / Libraries

- **Official:** None — standard RSS/Atom; podcast via standard podcast RSS.
- **Community:** `feedparser` (Python), `rss-parser` (Node.js).

## Documentation

- Main site: https://cimsec.org
- Podcast: https://cimsec.org/podcast-2/

## Notes

- One of the best **free analysis** sources for maritime-security strategy and naval affairs — complements the breaking-news outlets with depth.
- Cross-reference: `maritime-media/usni-news.md`, `maritime-media/naval-news.md` for the naval/defense angle.
