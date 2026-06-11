# Sulu-Celebes Sea — Regional Security Feeds

Curated feeds covering the Sulu-Celebes Sea / Eastern Sabah tri-border area (Philippines–Malaysia–Indonesia): kidnap-for-ransom by Abu Sayyaf Group elements, armed robbery, and trafficking.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-06-11

## Use cases

- Monitoring kidnap-for-ransom (KFR) and armed-robbery threats to vessels and crew in the Sulu-Celebes Seas and waters off Eastern Sabah (notably around Sibutu Island and Tawi-Tawi).
- Tracking ReCAAP ISC advisories and threat-level changes (the authoritative regional source) and Philippine Coast Guard / ESSCOM posture.
- Following the Trilateral Cooperative Arrangement (TCA) patrols and designated transit corridors (24-hour advance notification to Maritime Command Centres).
- Watching trafficking (humans, arms, drugs) flows through the porous tri-border archipelago.

## Pricing

- **Free tier:** All listed feeds/advisories are free.
- **Paid tiers:** None.
- **Enterprise:** N/A.
- **Notes:** ReCAAP ISC is the primary authoritative reporting body for Asia; lean on it plus regional news.

## Authentication

No authentication required for any listed source.

## Endpoints

**Authoritative regional reporting:**
- ReCAAP ISC (incident reports & advisories; see `maritime-security/recaap-isc.md`): `https://www.recaap.org/`
- IMB Piracy Reporting Centre (live piracy map / reports; see `maritime-security/imb-piracy-reporting-centre.md`): `https://icc-ccs.org/piracy-reporting-centre`
- IFC Singapore (regional MDA hub; see `maritime-security/ifc-singapore.md`): `https://www.ifc.org.sg/`

**Regional news:**
- Philippine Daily Inquirer: `https://www.inquirer.net/fullfeed` — verify before use
- Rappler (Philippines): `https://www.rappler.com/feed/` — verify before use
- Benar News (Southeast Asia security/terrorism focus): `https://www.benarnews.org/english/rss2.xml` — verify before use

**Maritime news:**
- gCaptain: `https://feeds.feedburner.com/gcaptain`

**Government travel advisories:**
- U.S. State Dept Travel Advisories: `https://travel.state.gov/_res/rss/TAsTWs.xml` — monitor Philippines (Sulu Archipelago / Sulu Sea sub-regions), Malaysia (Eastern Sabah)

## Example call

```python
import feedparser

feeds = {
    "gCaptain": "https://feeds.feedburner.com/gcaptain",
    "Benar News": "https://www.benarnews.org/english/rss2.xml",
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

- ReCAAP ISC: https://www.recaap.org/
- IFC Singapore: https://www.ifc.org.sg/
- ESSCOM (Eastern Sabah Security Command): https://www.esscom.gov.my/

## Notes

- **Threat trend:** KFR abductions have sharply declined — no crew abductions for ransom reported since January 2020, and in Feb 2025 the Philippine Coast Guard downgraded the threat from "Moderate Low" to "Low." ReCAAP still advises vigilance; re-check the current ReCAAP advisory (last major update cycle 2025) before relying on a threat level.
- The residual risk is from **Abu Sayyaf Group (ASG) KFR elements** based around the Sulu islands; transit corridors and advance notification to Command Centres remain the recommended mitigations.
- Distinct from the Singapore/Malacca Strait armed-robbery problem (which is theft-focused and persistent) — keep this entry separate from `regional-security-feeds/southeast-asia-strait-of-malacca.md`.
- Cross-reference: `maritime-security/recaap-isc.md` (authoritative incidents), `maritime-security/ifc-singapore.md` (regional MDA), and `regional-security-feeds/south-china-sea.md` for the adjacent strategic picture.
