# Bab el Mandeb & Southern Red Sea — Regional Security Feeds

Curated feeds focused specifically on the Bab el Mandeb strait and Southern Red Sea chokepoint: Houthi anti-ship missile/UAV/USV attacks, naval coalition operations, and the BAM transit decision.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-06-11

## Use cases

- Tracking Houthi anti-ship ballistic/cruise missile, UAV, and USV (drone-boat) attacks at the strait and approaches (Hodeidah/Mokha vicinity, Gulf of Aden ingress).
- Monitoring coalition naval activity (Operation Prosperity Guardian / US, Operation Aspides / EU) shaping convoy and escort options.
- Supporting the "transit Bab el Mandeb vs. divert via Cape of Good Hope" decision for routing, schedule, and cost.
- Watching UKMTO/JMIC alerts and standing-alert windows specific to the chokepoint.

## Pricing

- **Free tier:** All listed feeds/advisories are free.
- **Paid tiers:** None.
- **Enterprise:** N/A.
- **Notes:** This is a focused sub-corridor of the broader Red Sea entry; kept separate because the BAM chokepoint drives discrete transit decisions.

## Authentication

No authentication required for any listed source.

## Endpoints

**Authoritative reporting:**
- UKMTO (incident reports & advisories; see `maritime-security/ukmto.md`): `https://www.ukmto.org/`
- Joint Maritime Information Center (JMIC) threat updates (via CMF): `https://www.combinedmaritimeforces.com/`
- IMB Piracy Reporting Centre: `https://icc-ccs.org/piracy-reporting-centre`

**Maritime news:**
- gCaptain: `https://feeds.feedburner.com/gcaptain` — fastest English-language Red Sea/BAM incident reporting
- Splash247: `https://splash247.com/feed/` — verify before use

**Security & crisis analysis:**
- International Crisis Group (MENA / Yemen): `https://www.crisisgroup.org/rss/81`
- ACLED (Yemen conflict events; see `conflict-events/acled.md`): `https://acleddata.com/`

**Government travel advisories:**
- U.S. State Dept Travel Advisories: `https://travel.state.gov/_res/rss/TAsTWs.xml` — monitor Yemen (L4), Djibouti, Eritrea

## Example call

```python
import feedparser

feeds = {
    "gCaptain": "https://feeds.feedburner.com/gcaptain",
    "ICG MENA": "https://www.crisisgroup.org/rss/81",
    "State Dept": "https://travel.state.gov/_res/rss/TAsTWs.xml",
}
for name, url in feeds.items():
    feed = feedparser.parse(url)
    print(f"{name}: {len(feed.entries)} entries")
```

## Rate limits

Not published. Poll feeds no more than once every 15–30 minutes.

## SDKs / Libraries

- **Official:** None — standard RSS/Atom.
- **Community:** `feedparser` (Python), `rss-parser` (Node.js).

## Documentation

- UKMTO: https://www.ukmto.org/
- Combined Maritime Forces / JMIC: https://www.combinedmaritimeforces.com/
- International Crisis Group Yemen: https://www.crisisgroup.org/middle-east-north-africa/gulf-and-arabian-peninsula/yemen

## Notes

- **Why separate from Red Sea & Suez:** the Bab el Mandeb strait is the specific chokepoint where the transit/divert decision is made and where the densest Houthi attack activity concentrates (Southern Red Sea, BAM, Gulf of Aden approaches). The broader corridor entry (`regional-security-feeds/red-sea-suez-canal.md`) covers Suez/SCA and the wider route.
- The Southern Red Sea and Bab el Mandeb fall within **JWC Listed Areas** — cross-reference `war-risk-zones/jwc-listed-areas.md` for AP pricing context (these areas drive substantial additional war-risk premium).
- UKMTO standing alerts (sometimes 72-hour windows) are a strong leading indicator of elevated attack risk in the alert area.
- Cross-reference: `regional-security-feeds/red-sea-suez-canal.md`, `regional-security-feeds/horn-of-africa-gulf-of-aden.md`, and `maritime-security/ukmto.md`.
