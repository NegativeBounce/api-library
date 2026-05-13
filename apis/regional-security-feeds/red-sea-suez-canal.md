# Red Sea & Suez Canal — Regional Security Feeds

Curated RSS and news feeds covering security incidents, Houthi attacks, and maritime threat reporting for the Red Sea corridor, Suez Canal, and Gulf of Suez.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-13

## Use cases

- Real-time monitoring of Houthi missile, drone, and naval attacks on commercial vessels transiting the Red Sea
- Tracking Suez Canal Authority (SCA) transit developments and Egyptian security posture
- Aggregating security and conflict news from Yemen, Egypt, Sudan, Eritrea, and Djibouti affecting corridor routing

## Pricing

- **Free tier:** All feeds are freely accessible RSS endpoints
- **Paid tiers:** None
- **Enterprise:** N/A
- **Notes:** Feed availability and update frequency vary by source; verify URLs before production deployment.

## Authentication

No authentication required for any listed feed.

## Endpoints

**Maritime-specific:**
- gCaptain maritime news: `https://feeds.feedburner.com/gcaptain` — confirmed live; primary English-language source for Red Sea attack reporting on commercial vessels
- Splash247 maritime: `https://splash247.com/feed/` — verify before use (shipping industry news; inferred WordPress pattern)
- Seatrade Maritime: `https://www.seatrade-maritime.com/rss/xml` — verify before use (industry publication covering Red Sea routing and Canal transits)

**Regional news:**
- Al-Ahram Online (Egypt): `https://english.ahram.org.eg/rss.aspx` — verify before use (Egypt's leading English-language state daily; covers Canal and regional security)

**Security & crisis analysis:**
- International Crisis Group MENA: `https://www.crisisgroup.org/rss/81` — confirmed live; covers Yemen Houthi conflict and Red Sea security environment

**Government advisories:**
- U.S. State Dept Travel Advisories: `https://travel.state.gov/_res/rss/TAsTWs.xml` — confirmed live; monitor for Yemen (L4), Sudan (L4), Eritrea (L3) advisory changes

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

Not published for any source. Poll individual feeds no more than once every 15–30 minutes.

## SDKs / Libraries

- **Official:** None — standard RSS/Atom
- **Community:** `feedparser` (Python), `rss-parser` (Node.js)

## Documentation

- gCaptain: https://gcaptain.com
- International Crisis Group Yemen: https://www.crisisgroup.org/middle-east-north-africa/gulf-and-arabian-peninsula/yemen
- Al-Ahram Online: https://english.ahram.org.eg
- Splash247: https://splash247.com

## Notes

- The Suez Canal handles ~12% of global trade (30% of global container traffic). Since late 2023, Houthi attacks from Yemen have diverted >70% of container traffic to the Cape of Good Hope route — this region is the highest-priority maritime security monitoring corridor globally.
- gCaptain typically reports confirmed vessel attacks within hours; it is the fastest reliable English-language source for Red Sea incidents.
- UKMTO (United Kingdom Maritime Trade Operations) issues incident reports for the Red Sea/Indian Ocean — subscribe to their voluntary reporting scheme at https://www.ukmto.org for direct alerts (email-based, no RSS).
- Operation Prosperity Guardian (US-led) and Operation Aspides (EU-led) press releases covering Red Sea naval operations are published by respective defense ministries — no unified RSS; monitor manually.
- Al-Ahram, Splash247, and Seatrade RSS URLs use inferred patterns — verify before production integration.
