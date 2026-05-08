# GPSJAM

Free public daily map of likely GPS interference worldwide, built by John Wiseman (@lemonodor) from ADS-B Exchange aircraft NACp data.

**Tier:** Free
**Auth:** None (no public API)
**Last researched:** 2026-05-07

## Use cases

- Visual reference for known and suspected GPS jamming/spoofing hotspots (Black Sea, Baltics, Eastern Med, Persian Gulf, parts of South Asia).
- Day-to-day situational awareness for hobbyists, journalists, OSINT analysts, and pilots.
- Historical lookup of interference patterns by date back to 2022-02-14 (earliest available data).
- Pre-flight briefing supplement when you don't need machine-readable data.

## Pricing

- **Free tier:** Entire site is free. Donation-supported.
- **Paid tiers:** None.
- **Enterprise:** None.
- **Notes:** John Wiseman runs GPSJAM as a side project funded by ADS-B Exchange API access and donations.

## Authentication

None — the site is fully public. There is no documented public API, key system, or authentication layer.

## Endpoints

- **Base URL:** `https://gpsjam.org/`
- **Key endpoints:**
  - `GET /` — interactive Mapbox GL map for the current date
  - `GET /?date=YYYY-MM-DD` — interactive map for a specific historical date
  - `GET /faq/`, `GET /about/` — static info pages

GPSJAM does not publish or document any data API. The web map is built on Mapbox GL and consumes private tile/data URLs that are not part of any documented contract — scraping these is brittle and not endorsed by the operator.

## Example call

```bash
# View the current day's map (HTML)
curl "https://gpsjam.org/"

# View a specific historical date
curl "https://gpsjam.org/?date=2024-09-01"
```

## Rate limits

Not published. As a small donation-funded site, treat any access as best-effort and avoid heavy automated scraping.

## SDKs / Libraries

- **Official:** None.
- **Community:** None notable. John Wiseman maintains many GitHub repos at https://github.com/wiseman, but the GPSJAM data pipeline itself is not open-sourced.

## Documentation

- Main docs: https://gpsjam.org/
- FAQ: https://gpsjam.org/faq/
- About: https://gpsjam.org/about/

## Notes

- **No public API.** This entry is cataloged as a reference because GPSJAM is the canonical free GNSS interference map and is referenced by aviation media, OSINT analysts, and OPSGROUP. For programmatic access, use ADS-B Exchange (the underlying source) or GPSwise (the commercial successor with similar methodology).
- Hex resolution: hexagons are roughly the size of Sado Island, Japan (~855 km² / 330 mi²). Three colors: green (<2% bad NACp), yellow (2–10%), red (>10%).
- Updated every 24 hours, soon after midnight UTC. Data is aggregated over a rolling 24-hour window, so transient short-duration interference may not appear.
- Inferred from ADS-B `NACp` (Navigation Accuracy Category for Position) values; cannot distinguish jamming from spoofing, INS-only operation, or aircraft-side equipment problems.
- Known false-positive zones: southwestern US (military trainer aircraft performing aerobatics that temporarily occlude their own GPS antennas).
- No coverage in active war zones (Ukraine) where airlines avoid flying — gaps in the map ≠ "no interference."
- Globe view was discontinued for cost reasons; map is currently flat-projected only.
