# USNI News (U.S. Naval Institute)

News and analysis from the U.S. Naval Institute covering naval operations, maritime security, and defense policy, alongside Proceedings and Naval History magazines.

**Tier:** Freemium
**Auth:** None (news) / Membership
**Last researched:** 2026-06-11

## Use cases

- Authoritative coverage of U.S. and allied naval operations, fleet movements, and maritime-security policy.
- Document drops (official reports, force structure, budget) and fleet/marine trackers useful for atmospherics.
- Proceedings/Naval History long-form analysis (membership) for deeper strategic context.

## Pricing

- **Free tier:** USNI News articles and RSS are free.
- **Paid tiers:** USNI membership for Proceedings/Naval History and archives.
- **Enterprise:** N/A (membership organization).
- **Notes:** Non-profit professional institute.

## Authentication

None for USNI News/RSS; membership login for magazine archives.

## Endpoints

- **Base URL:** `https://news.usni.org`
- **Key surfaces:**
  - Site: `https://news.usni.org/`
  - RSS: `https://news.usni.org/feed`

## Example call

```python
import feedparser
feed = feedparser.parse("https://news.usni.org/feed")
print(len(feed.entries), "entries")
```

## Rate limits

Not published. Poll RSS no more than once every 30 minutes.

## SDKs / Libraries

- **Official:** None — standard RSS/Atom.
- **Community:** `feedparser` (Python), `rss-parser` (Node.js).

## Documentation

- Main site: https://news.usni.org

## Notes

- The strongest free source for **naval/defense** atmospherics (USN/allied operations, deployments) — directly relevant to naval-coalition activity in Red Sea, Hormuz, Indo-Pacific.
- USNI's weekly Fleet/Marine Tracker is a useful open-source order-of-battle snapshot.
- Cross-reference: `maritime-media/naval-news.md`, `maritime-media/cimsec.md`; for navigational closures see `navigational-warnings/`.
