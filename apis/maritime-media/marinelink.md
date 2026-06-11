# MarineLink / Maritime Reporter (New Wave Media)

Maritime news portal and home of Maritime Reporter & Engineering News, covering shipbuilding, marine technology, offshore, and naval developments.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-06-11

## Use cases

- Marine technology and equipment tracking (shipbuilding, propulsion, sensors, autonomy) — strong for marsec-tech atmospherics.
- Naval, offshore, and workboat news plus product/technology announcements.
- Access to Maritime Reporter & Engineering News and related trade magazines (digital editions/whitepapers).

## Pricing

- **Free tier:** Free web access, RSS, newsletters, and digital magazine editions.
- **Paid tiers:** None required.
- **Enterprise:** N/A.
- **Notes:** Publisher New Wave Media (also MarineTechnologyNews, Marine News).

## Authentication

None for public articles/RSS.

## Endpoints

- **Base URL:** `https://www.marinelink.com`
- **Key surfaces:**
  - Site: `https://www.marinelink.com/`
  - RSS: `https://www.marinelink.com/rss` (verify before use)
  - Maritime Reporter: `https://www.marinelink.com/magazines`

## Example call

```python
import feedparser
feed = feedparser.parse("https://www.marinelink.com/rss")  # verify URL
print(len(feed.entries), "entries")
```

## Rate limits

Not published. Poll RSS no more than once every 15–30 minutes.

## SDKs / Libraries

- **Official:** None — standard RSS/Atom.
- **Community:** `feedparser` (Python), `rss-parser` (Node.js).

## Documentation

- Main site: https://www.marinelink.com
- Magazines: https://www.marinelink.com/magazines

## Notes

- Best free source for **marine-technology and shipbuilding** coverage and vendor announcements — useful for tracking maritime-security tech.
- RSS URL should be verified before production integration.
- Cross-reference: `maritime-media/naval-news.md` (defense tech), `maritime-media/riviera.md` (tech webinars/whitepapers).
