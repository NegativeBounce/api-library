# Sea of Japan & East China Sea — Regional Security Feeds

Curated feeds covering the East China Sea / Sea of Japan strategic environment: Senkaku/Diaoyu tensions, Taiwan-adjacent activity, North Korean missile/sanctions-evasion at sea, and grey-zone coast-guard friction.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-06-11

## Use cases

- Monitoring state-level grey-zone activity (China Coast Guard incursions around the Senkaku/Diaoyu Islands, ADIZ and PLA-Navy movements) affecting commercial routing and risk.
- Tracking North Korean ballistic-missile launches over/into the Sea of Japan and UN sanctions-evasion ship-to-ship transfers.
- Following Taiwan-Strait-adjacent tension that can spill into East China Sea shipping lanes.
- Watching Japan Coast Guard / JMSDF and Korea Coast Guard advisories and NAVAREA XI navigational warnings.

## Pricing

- **Free tier:** All listed feeds/advisories are free.
- **Paid tiers:** None.
- **Enterprise:** N/A.
- **Notes:** Threats here are predominantly state/grey-zone and navigational rather than piracy; sourcing skews to government and quality regional news.

## Authentication

No authentication required for any listed source.

## Endpoints

**Government & navigational:**
- JHOD NAVAREA XI navigational warnings (Japan; see `navigational-warnings/jhod-navarea-xi.md`): `https://www1.kaiho.mlit.go.jp/`
- Japan Coast Guard: `https://www.kaiho.mlit.go.jp/e/` — verify before use
- NGA Maritime Safety Information (broadcast warnings): `https://msi.nga.mil/`

**Regional news:**
- NHK World-Japan (English): `https://www3.nhk.or.jp/nhkworld/en/news/rss/` — verify before use
- The Japan Times: `https://www.japantimes.co.jp/feed/` — verify before use
- Yonhap News (Korea, English): `https://en.yna.co.kr/RSS/news.xml` — verify before use
- Focus Taiwan (CNA): `https://focustaiwan.tw/rss` — verify before use

**Maritime news:**
- gCaptain: `https://feeds.feedburner.com/gcaptain`

**Government travel advisories:**
- U.S. State Dept Travel Advisories: `https://travel.state.gov/_res/rss/TAsTWs.xml` — monitor North Korea (L4), regional changes

## Example call

```python
import feedparser

feeds = {
    "gCaptain": "https://feeds.feedburner.com/gcaptain",
    "NHK World": "https://www3.nhk.or.jp/nhkworld/en/news/rss/",
    "Yonhap": "https://en.yna.co.kr/RSS/news.xml",
}
for name, url in feeds.items():
    feed = feedparser.parse(url)
    print(f"{name}: {len(feed.entries)} entries")
```

## Rate limits

Not published. Poll feeds no more than once every 15–30 minutes.

## SDKs / Libraries

- **Official:** None — standard RSS/Atom; NGA/JHOD provide structured MSI products.
- **Community:** `feedparser` (Python), `rss-parser` (Node.js).

## Documentation

- JHOD NAVAREA XI: https://www1.kaiho.mlit.go.jp/
- NGA MSI: https://msi.nga.mil/
- Japan Coast Guard (English): https://www.kaiho.mlit.go.jp/e/

## Notes

- The dominant risks are **state/grey-zone**: Senkaku/Diaoyu coast-guard standoffs, PLA-Navy and ADIZ activity, North Korean missile tests over the Sea of Japan, and DPRK sanctions-evasion STS transfers — not classical piracy.
- For DPRK sanctions-evasion vessel work, cross-reference `dark-vessel-detection/` and `sanctions/` (e.g. OpenSanctions, OFAC).
- Navigational warnings (NAVAREA XI via JHOD, plus NGA MSI) are the most operationally actionable feed for missile-launch closure areas and exercise zones.
- Cross-reference: `regional-security-feeds/south-china-sea.md` (adjacent strategic theatre), `navigational-warnings/jhod-navarea-xi.md`, and `navigational-warnings/nga-msi.md`.
