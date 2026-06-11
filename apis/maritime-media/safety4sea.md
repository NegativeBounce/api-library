# Safety4Sea

Maritime news and resources outlet focused on safety, security, environment, and regulation, with strong incident and advisory aggregation.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-06-11

## Use cases

- Aggregated reporting on maritime-security incidents and advisories (e.g. UKMTO/JMIC updates, Hormuz, Gulf of Aden) — a useful secondary feed for cross-checking.
- Safety, environmental, and regulatory news plus loss-prevention and best-practice resources.
- Topic/tag pages (e.g. UKMTO) that consolidate incident threads for situational awareness.

## Pricing

- **Free tier:** Free web access and RSS.
- **Paid tiers:** None required.
- **Enterprise:** N/A.
- **Notes:** Publisher also runs industry forums/awards.

## Authentication

None for public articles/RSS.

## Endpoints

- **Base URL:** `https://safety4sea.com`
- **Key surfaces:**
  - Site: `https://safety4sea.com/`
  - RSS: `https://safety4sea.com/feed/` (verify before use)
  - Topic example (UKMTO): `https://safety4sea.com/tag/ukmto/`

## Example call

```python
import feedparser
feed = feedparser.parse("https://safety4sea.com/feed/")  # verify URL
print(len(feed.entries), "entries")
```

## Rate limits

Not published. Poll RSS no more than once every 30 minutes.

## SDKs / Libraries

- **Official:** None — standard RSS/Atom.
- **Community:** `feedparser` (Python), `rss-parser` (Node.js).

## Documentation

- Main site: https://safety4sea.com

## Notes

- Good **aggregation/secondary** source: consolidates official advisories and incident reporting into readable threads — handy for situational awareness, but verify primary sources (UKMTO, NSC) for authoritative detail.
- Cross-reference: `maritime-security/ukmto.md`, `maritime-media/gcaptain.md`, and the relevant `regional-security-feeds/` entries.
