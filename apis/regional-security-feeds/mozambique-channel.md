# Mozambique Channel — Regional Security Feeds

Curated feeds covering the maritime security environment of the Mozambique Channel and northern Mozambique (Cabo Delgado): insurgency spillover near LNG infrastructure, piracy spillover from the wider Indian Ocean, and offshore energy security.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-06-11

## Use cases

- Monitoring the ISIS-Mozambique (Ansar al-Sunna) insurgency in Cabo Delgado and its maritime/coastal spillover near major offshore LNG developments (e.g. Afungi/Palma).
- Tracking offshore energy-installation security and the EEZ around northern Mozambique (a JWC Listed Area — Cabo Delgado waters).
- Watching for piracy spillover into the Channel from the Somali basin / wider Indian Ocean High Risk Area.
- Following naval patrol postures (SAMIM-successor arrangements, Rwandan and regional forces) affecting transit security.

## Pricing

- **Free tier:** All listed feeds/advisories are free.
- **Paid tiers:** None.
- **Enterprise:** N/A.
- **Notes:** Region has fewer dedicated maritime feeds than the Red Sea/Gulf of Aden; lean on regional news + conflict trackers + government advisories.

## Authentication

No authentication required for any listed source.

## Endpoints

**Security & conflict analysis:**
- ACLED (Africa conflict event data; has an API — see `conflict-events/acled.md`): `https://acleddata.com/`
- International Crisis Group (Africa): `https://www.crisisgroup.org/rss/` — covers Cabo Delgado/Mozambique
- ReliefWeb Mozambique updates: `https://reliefweb.int/updates/rss.xml?primary_country=156`

**Regional news:**
- AllAfrica – Mozambique: `https://allafrica.com/tools/headlines/rdf/mozambique/headlines.rdf` — verify before use
- Daily Maverick (South Africa, strong Mozambique/Cabo Delgado coverage): `https://www.dailymaverick.co.za/dmrss/` — verify before use
- Club of Mozambique (English): `https://clubofmozambique.com/feed/` — verify before use

**Maritime news:**
- gCaptain: `https://feeds.feedburner.com/gcaptain`

**Government travel advisories:**
- U.S. State Dept Travel Advisories: `https://travel.state.gov/_res/rss/TAsTWs.xml` — monitor Mozambique (Cabo Delgado at higher level)

## Example call

```python
import feedparser

feeds = {
    "gCaptain": "https://feeds.feedburner.com/gcaptain",
    "ReliefWeb Mozambique": "https://reliefweb.int/updates/rss.xml?primary_country=156",
    "State Dept": "https://travel.state.gov/_res/rss/TAsTWs.xml",
}
for name, url in feeds.items():
    feed = feedparser.parse(url)
    print(f"{name}: {len(feed.entries)} entries")
```

## Rate limits

Not published. Poll feeds no more than once every 15–30 minutes.

## SDKs / Libraries

- **Official:** None — standard RSS/Atom (ACLED has a documented API).
- **Community:** `feedparser` (Python), `rss-parser` (Node.js).

## Documentation

- ACLED: https://acleddata.com/
- ReliefWeb: https://reliefweb.int/country/moz
- International Crisis Group Mozambique: https://www.crisisgroup.org/africa/southern-africa/mozambique

## Notes

- The strategic driver here is **offshore LNG**: multi-billion-dollar developments off Cabo Delgado sit adjacent to an active insurgency; security of the Afungi peninsula and the surrounding EEZ is the key concern, more than open-ocean piracy.
- Cabo Delgado waters are a **JWC Listed Area** — cross-reference `war-risk-zones/jwc-listed-areas.md` for the war-risk pricing layer.
- The Channel is a major tanker route (Cape of Good Hope diversions from the Red Sea increase traffic here) — relevant to congestion and transit-risk analysis.
- For incident-grade piracy reporting use IMB (`maritime-security/imb-piracy-reporting-centre.md`); for conflict-event granularity ACLED is the strongest structured source.
- Cross-reference: `regional-security-feeds/east-africa-indian-ocean.md` and `regional-security-feeds/horn-of-africa-gulf-of-aden.md` for the wider Indian Ocean picture.
