# West Africa & Gulf of Guinea — Regional Security Feeds

Curated RSS and news feeds covering piracy, kidnap-for-ransom, oil theft, and maritime security incidents in the Gulf of Guinea, Niger Delta, and West African coastal shipping lanes.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-13

## Use cases

- Monitoring piracy and kidnap-for-ransom incidents targeting commercial vessels in the Gulf of Guinea
- Tracking oil theft, bunkering crime, and illegal fishing in the Niger Delta and Gulf of Guinea EEZs
- Aggregating security news from Nigeria, Ghana, Cameroon, Benin, Togo, Côte d'Ivoire, and Gabon

## Pricing

- **Free tier:** All feeds are freely accessible RSS endpoints
- **Paid tiers:** None
- **Enterprise:** N/A
- **Notes:** Feed availability and update frequency vary by source; verify URLs before production deployment.

## Authentication

No authentication required for any listed feed.

## Endpoints

**Nigerian news (English-language):**
- Vanguard Nigeria: `https://www.vanguardngr.com/feed/` — verify before use (Nigeria's major English-language daily; covers Niger Delta and maritime crime)
- The Punch Nigeria: `https://punchng.com/feed/` — verify before use (Nigeria's highest-circulation English daily)

**Pan-African coverage:**
- AllAfrica: `https://allafrica.com/tools/headlines/rdf.php?category=latest` — aggregates West African English-language news from 130+ outlets
- Africa Defense Forum: `https://adf-magazine.com/feed/` — verify before use (U.S. AFRICOM-funded; covers Gulf of Guinea security operations and capacity building)

**Security & crisis analysis:**
- International Crisis Group Africa: `https://www.crisisgroup.org/rss/1` — confirmed live; covers Nigeria, Cameroon, Sahel, and West African conflicts

**Government advisories:**
- U.S. State Dept Travel Advisories: `https://travel.state.gov/_res/rss/TAsTWs.xml` — confirmed live; monitor advisory changes for Nigeria (L3), Cameroon (L3), Mali (L4), Burkina Faso (L4)

## Example call

```python
import feedparser

feeds = {
    "AllAfrica": "https://allafrica.com/tools/headlines/rdf.php?category=latest",
    "ICG Africa": "https://www.crisisgroup.org/rss/1",
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

- Vanguard Nigeria: https://www.vanguardngr.com
- The Punch Nigeria: https://punchng.com
- AllAfrica: https://allafrica.com
- International Crisis Group West Africa: https://www.crisisgroup.org/africa/west-africa
- Africa Defense Forum: https://adf-magazine.com

## Notes

- The Gulf of Guinea has been the world's most piracy-affected region since approximately 2019, surpassing the Gulf of Aden; crew kidnap-for-ransom is the dominant attack type rather than cargo theft.
- IMB (International Maritime Bureau) Piracy Reporting Centre publishes quarterly reports covering Gulf of Guinea incidents — reports available at https://www.icc-ccs.org/icc/imb; no RSS feed.
- Nigeria's maritime zone (Niger Delta, Lagos, Bonny) accounts for the majority of Gulf of Guinea incidents; Vanguard and The Punch are the most reliable English-language sources for domestic incident coverage.
- ECOWAS (Economic Community of West African States) and the Yaoundé Architecture (Zone F, G, H) coordinate Gulf of Guinea maritime security; no RSS feeds available from these bodies.
- Vanguard, The Punch, and Africa Defense Forum use inferred WordPress patterns — verify before production integration.
- Sahel conflict spillover into coastal Benin, Togo, and northern Ghana is an emerging threat to port hinterland security; ICG Africa covers this trend.
