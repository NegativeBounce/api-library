# Horn of Africa & Gulf of Aden — Regional Security Feeds

Curated RSS and news feeds covering piracy, armed robbery, Houthi missile and drone attacks, and security incidents along the Gulf of Aden, Bab-el-Mandeb Strait, and the Horn of Africa coast.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-13

## Use cases

- Real-time monitoring of Houthi attacks on commercial shipping transiting the Red Sea and Gulf of Aden
- Tracking Somali piracy resurgence and armed robbery incidents in Somali Basin and Gulf of Aden
- Aggregating security developments in Somalia, Djibouti, Eritrea, and Ethiopia affecting transit routing

## Pricing

- **Free tier:** All feeds are freely accessible RSS endpoints
- **Paid tiers:** None
- **Enterprise:** N/A
- **Notes:** Feed availability and update frequency vary by source; verify URLs before production deployment.

## Authentication

No authentication required for any listed feed.

## Endpoints

**Somali regional news:**
- Garowe Online (Somalia): `https://www.garoweonline.com/en/feed` — verify before use (leading Somali English-language news; standard WordPress pattern)
- Hiiraan Online (Somalia): `https://www.hiiraan.com/feed` — verify before use (Somali diaspora news; 403 returned on direct fetch — URL pattern inferred)

**Security & crisis analysis:**
- International Crisis Group Africa: `https://www.crisisgroup.org/rss/1` — confirmed live; covers Somalia, Ethiopia, and Horn of Africa conflicts
- International Crisis Group MENA: `https://www.crisisgroup.org/rss/81` — confirmed live; covers Yemen and Houthi conflict

**Pan-African & defence:**
- Africa Defense Forum: `https://adf-magazine.com/feed/` — verify before use (U.S. AFRICOM-funded security coverage; covers Horn of Africa military operations)

**Maritime-specific:**
- gCaptain: `https://feeds.feedburner.com/gcaptain` — confirmed live; frontline maritime shipping attack reporting

**Government advisories:**
- U.S. State Dept Travel Advisories: `https://travel.state.gov/_res/rss/TAsTWs.xml` — confirmed live; monitor for Somalia (L4), Yemen (L4), Ethiopia (L3) advisory changes

## Example call

```python
import feedparser

feeds = {
    "ICG Africa": "https://www.crisisgroup.org/rss/1",
    "ICG MENA": "https://www.crisisgroup.org/rss/81",
    "gCaptain": "https://feeds.feedburner.com/gcaptain",
    "State Dept": "https://travel.state.gov/_res/rss/TAsTWs.xml",
}
for name, url in feeds.items():
    feed = feedparser.parse(url)
    print(f"{name}: {len(feed.entries)} entries")
```

## Rate limits

Not published for any source. Poll individual feeds no more than once every 15–30 minutes.

## SDKs / Libraries

- **Official:** None — standard RSS/Atom
- **Community:** `feedparser` (Python), `rss-parser` (Node.js)

## Documentation

- International Crisis Group Horn of Africa: https://www.crisisgroup.org/africa/horn-africa
- International Crisis Group Yemen: https://www.crisisgroup.org/middle-east-north-africa/gulf-and-arabian-peninsula/yemen
- gCaptain: https://gcaptain.com
- Garowe Online: https://www.garoweonline.com

## Notes

- The Bab-el-Mandeb Strait (14 miles at narrowest) handles ~10% of global trade; Houthi attacks since late 2023 have caused widespread shipping rerouting around Cape of Good Hope.
- gCaptain is typically the fastest English-language source for confirmed attack reports on commercial vessels in this corridor.
- Garowe Online and Hiiraan Online are the two most authoritative Somali English-language news sources; their RSS URLs use inferred WordPress patterns and should be verified before production use.
- EUNAVFOR Operation Atalanta publishes press releases at https://eunavfor.eu/news — no RSS feed available, but the site is worth monitoring manually.
- EU NAVFOR and Combined Maritime Forces (CMF) incident reports are the authoritative source for piracy data; these are currently press-release-only without RSS.
