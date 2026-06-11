# Baltic Sea & Gulf of Finland — Regional Security Feeds

Curated feeds covering the Baltic's hybrid-threat environment: undersea cable/pipeline damage, GNSS jamming, "shadow fleet" tanker activity, and NATO/Russia maritime tension.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-06-11

## Use cases

- Monitoring critical-undersea-infrastructure incidents (subsea cables and pipelines) attributed to anchor-dragging and suspected sabotage, especially in the Gulf of Finland.
- Tracking widespread GNSS jamming/spoofing affecting navigation across the eastern Baltic.
- Following "shadow fleet" / sanctioned-tanker activity, flag-state and P&I scrutiny, and port-state-control actions.
- Watching NATO posture (Baltic Sentry and successor activities) and Russia–NATO maritime friction after Finnish/Swedish accession.

## Pricing

- **Free tier:** All listed feeds/advisories are free.
- **Paid tiers:** None.
- **Enterprise:** N/A.
- **Notes:** Strong national-authority and NATO sourcing; news RSS varies — verify URLs.

## Endpoints

**Government & alliance sources:**
- NATO Shipping Centre: `https://shipping.nato.int/nsc` — advisories relevant to the Baltic
- NATO MARCOM news: `https://mc.nato.int/` — Baltic maritime activity
- Finnish Border Guard / Traficom GNSS-interference notices: `https://www.traficom.fi/en` — verify before use
- NAVAREA I (UK) warnings (covers parts of the Baltic via national NAVTEX): national hydrographic offices (UKHO/relevant)

**Regional news:**
- Yle News (Finland, English): `https://feeds.yle.fi/uutiset/v1/recent.rss?publisherIds=YLE_NEWS` — verify before use
- The Barents Observer: `https://thebarentsobserver.com/en/rss` — verify before use
- LRT (Lithuania, English): `https://www.lrt.lt/en/rss` — verify before use

**Maritime news:**
- gCaptain: `https://feeds.feedburner.com/gcaptain`
- Splash247: `https://splash247.com/feed/` — verify before use

**Security analysis:**
- International Crisis Group / RUSI commentary (no single Baltic RSS; monitor manually)

## Example call

```python
import feedparser

feeds = {
    "gCaptain": "https://feeds.feedburner.com/gcaptain",
    "Barents Observer": "https://thebarentsobserver.com/en/rss",
}
for name, url in feeds.items():
    feed = feedparser.parse(url)
    print(f"{name}: {len(feed.entries)} entries")
```

## Rate limits

Not published. Poll feeds no more than once every 15–30 minutes.

## SDKs / Libraries

- **Official:** None — standard RSS/Atom and HTML advisory pages.
- **Community:** `feedparser` (Python), `rss-parser` (Node.js).

## Documentation

- NATO Shipping Centre: https://shipping.nato.int/nsc
- NATO MARCOM: https://mc.nato.int/
- Traficom (Finland): https://www.traficom.fi/en

## Notes

- The defining risk here is **hybrid/grey-zone**, not classical piracy: subsea cable and pipeline damage (multiple incidents since 2023, several in the Gulf of Finland) and persistent GNSS jamming affecting commercial navigation.
- **Shadow fleet** tankers transiting to/from Russian Baltic ports drive sanctions, insurance and PSC exposure — pair with `sanctions/` and `dark-vessel-detection/` sources.
- GNSS interference is severe in the eastern Baltic — cross-reference `gnss-interference/` (e.g. GPSJAM, Zephr) for the navigation-integrity layer.
- Reporting/awareness runs through NATO Shipping Centre and national authorities rather than a UKMTO-style single centre.
- Cross-reference: `regional-security-feeds/english-channel-north-sea.md` (adjacent critical-infrastructure concerns) and `war-risk-zones/jwc-listed-areas.md` (Russia is a JWC Listed Area).
