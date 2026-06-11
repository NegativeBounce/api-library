# Black Sea & Sea of Azov — Regional Security Feeds

Curated RSS, advisory, and news feeds covering the Russia–Ukraine war's maritime dimension: projectile/drone strikes, sea mines, GNSS jamming, and grain-corridor developments in the Black Sea and Sea of Azov.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-06-11

## Use cases

- Monitoring kinetic threats to commercial shipping (projectiles, explosions, USV/drone attacks, moored and drifting naval mines) across the Black Sea and Sea of Azov.
- Tracking GNSS jamming/spoofing and AIS disruption that degrade vessel tracking and the evidentiary value of electronic records throughout the region.
- Following NATO Shipping Centre recommendations, NAVAREA III warnings, and IMO circular guidance (CL 4524 series) for routing and ISPS security-level decisions.
- Watching grain-corridor / port-status developments (Ukrainian ports often at ISPS Level 3; Russian ports at Level 2).

## Pricing

- **Free tier:** All listed feeds and advisories are freely accessible.
- **Paid tiers:** None.
- **Enterprise:** N/A.
- **Notes:** Government advisories are authoritative; news RSS varies in cadence — verify URLs before production use.

## Authentication

No authentication required for any listed source.

## Endpoints

**Government advisories & warnings (authoritative):**
- NATO Shipping Centre (Black Sea recommends / advisories): `https://shipping.nato.int/nsc` — primary military advisory channel; contact info@shipping.nato.int / +44 (0) 1923-956-574
- NAVAREA III warnings in force (Spain, covers Black Sea): `https://armada.defensa.gob.es/ihm/Aplicaciones/Navareas/Index_Navareas_xml_en.html`
- U.S. MARAD Maritime Security Advisories (e.g. 2026-003, Black Sea & Sea of Azov): `https://www.maritime.dot.gov/msci`
- IMO Black Sea / Sea of Azov hot topic (CL 4524 series, mine-threat circulars): `https://www.imo.org/en/MediaCentre/HotTopics/Pages/MaritimeSecurityandSafetyintheBlackSeaandSeaofAzov.aspx`

**Maritime news:**
- gCaptain: `https://feeds.feedburner.com/gcaptain` — fast English-language incident reporting
- Splash247: `https://splash247.com/feed/` — verify before use

**Security & crisis analysis:**
- International Crisis Group (Europe & Central Asia): `https://www.crisisgroup.org/rss/` — covers the Russia–Ukraine war

**Government travel advisories:**
- U.S. State Dept Travel Advisories: `https://travel.state.gov/_res/rss/TAsTWs.xml` — monitor Ukraine (L4), Russia (L4)

## Example call

```python
import feedparser

feeds = {
    "gCaptain": "https://feeds.feedburner.com/gcaptain",
    "State Dept": "https://travel.state.gov/_res/rss/TAsTWs.xml",
}
for name, url in feeds.items():
    feed = feedparser.parse(url)
    print(f"{name}: {len(feed.entries)} entries")
```

## Rate limits

Not published. Poll individual feeds no more than once every 15–30 minutes; advisory pages change infrequently.

## SDKs / Libraries

- **Official:** None — standard RSS/Atom and HTML advisory pages.
- **Community:** `feedparser` (Python), `rss-parser` (Node.js).

## Documentation

- NATO Shipping Centre: https://shipping.nato.int/nsc
- MARAD MSCI: https://www.maritime.dot.gov/msci
- IMO hot topic: https://www.imo.org/en/MediaCentre/HotTopics/Pages/MaritimeSecurityandSafetyintheBlackSeaandSeaofAzov.aspx

## Notes

- As of early 2026, U.S. MARAD Advisory 2026-003 remains the standing reference: commercial vessels struck by projectiles, drones/USVs and explosions since Feb 2022, with incidents as recent as Jan 2026, plus moored and drifting naval mines (primarily north-western Black Sea). Re-check for the current advisory number before relying on this.
- **GNSS jamming/spoofing is pervasive** — pair this feed with `gnss-interference/` sources (e.g. GPSJAM) for the navigation-integrity picture.
- The July 2025 mine strike on the dredger INHULSKYI (Bystrom River channel, 3 crew killed) underlines the persistent mine threat.
- Reporting channels: NATO Shipping Centre and the Mediterranean Voluntary Reporting Scheme; NSC is the de-facto primary advisory authority here (unlike UKMTO's role further south/east).
- Cross-reference: `regional-security-feeds/mediterranean-strait-of-gibraltar.md` (NATO MARLANT/Med VRS), `maritime-security/ukmto.md` (different theatre), and the war-risk pricing layer at `war-risk-zones/jwc-listed-areas.md` (Black Sea/Azov are JWC Listed Areas).
