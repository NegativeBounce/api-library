# CelesTrak

Free 501(c)(3) public-good service maintained by Dr. T.S. Kelso providing GP (General Perturbations) orbital element sets, supplemental owner-operator GPEs, the SATCAT (Satellite Catalog), and SOCRATES conjunction reports for the global SSA community since the 1980s.

**Tier:** Free
**Auth:** None (responsible-use rate limits enforced via firewall)
**Last researched:** 2026-05-09

## Use cases

- Pulling fresh TLE / OMM data for SGP4 orbit propagation in any tracking app
- Daily satellite catalog (SATCAT) snapshots for analysis
- Higher-accuracy supplemental GPEs for GPS, Iridium, Starlink, OneWeb, etc.
- SOCRATES (Satellite Orbital Conjunction Reports Assessing Threatening Encounters in Space) — collision-risk monitoring
- Group-based queries (active payloads, GEO Protected Zone, Stations, Starlink, 100 brightest, etc.)

## Pricing

- **Free tier:** Fully free under 501(c)(3) public-good model. No paid tier.
- **Paid tiers:** None.
- **Enterprise:** N/A.
- **Notes:** Donations welcome via the website. Sustained heavy use (more than 2-3 downloads/day per file) triggers a temporary ~24h IP firewall block — CelesTrak data only updates every ~2 hours, so polling more often wastes shared resources.

## Authentication

No authentication. Identify your client via a meaningful `User-Agent` header.

## Endpoints

- **Base URL:** `https://celestrak.org`
- **Key endpoints:**
  - `GET /NORAD/elements/gp.php?GROUP=<group>&FORMAT=<tle|2le|3le|csv|xml|json|json-pretty|kvn>` — current GP data for a group (e.g., `stations`, `starlink`, `gps-ops`, `weather`, `active`)
  - `GET /NORAD/elements/gp.php?CATNR=<NORAD_ID>&FORMAT=...` — single-object query
  - `GET /NORAD/elements/gp.php?INTDES=<COSPAR_ID>&FORMAT=...` — by international designator
  - `GET /NORAD/elements/gp.php?NAME=<query>&FORMAT=...` — name search
  - `GET /satcat/records.php?GROUP=...&FORMAT=CSV&ACTIVE=1&ONORBIT=1&MAX=N` — SATCAT records
  - `GET /NORAD/elements/supplemental/sup-gp.php?...` — supplemental owner-operator GPEs
  - `GET /SOCRATES/sort_minRange.php` — current conjunction reports

## Example call

```bash
# All ISS / Tiangong / etc. station TLEs in CSV
curl "https://celestrak.org/NORAD/elements/gp.php?GROUP=stations&FORMAT=csv" -o stations.csv

# Single-object OMM in JSON for the ISS (NORAD 25544)
curl "https://celestrak.org/NORAD/elements/gp.php?CATNR=25544&FORMAT=json" | jq

# Active payloads in the GEO Protected Zone, CSV
curl "https://celestrak.org/satcat/records.php?SPECIAL=gpz&FORMAT=CSV&ACTIVE=1"
```

```python
# Python with Skyfield (handles caching + parsing)
from skyfield.api import load
url = 'https://celestrak.org/NORAD/elements/gp.php?GROUP=stations&FORMAT=csv'
load.download(url, filename='stations.csv', max_age_days=1)
```

## Rate limits

No published per-minute rate; firewall-enforced behavioral limits. CelesTrak fetches new data from upstream every ~2 hours, so clients should not poll more often. Aggressive automation (e.g., once-per-minute polling) gets temp-blocked for up to 24h. Each request can include up to 100 satellites.

## SDKs / Libraries

- **Official:** None — open URL formats designed to work with any HTTP client.
- **Community:** Skyfield (Python), `pyorbital`, `sgp4` (Python/JS/C++), KeepTrack.space front-end, dozens more in C#/Go/Rust/Swift/Dart per the OMM-format ecosystem.

## Documentation

- Project home: https://celestrak.org/
- GP data formats: https://celestrak.org/NORAD/documentation/gp-data-formats.php
- SATCAT format: https://celestrak.org/satcat/satcat-format.php
- Supplemental GPEs: https://celestrak.org/NORAD/elements/supplemental/
- SOCRATES: https://celestrak.org/SOCRATES/
- T.S. Kelso on Bluesky: @TSKelso (transition notices, e.g., 6-digit catalog numbers)

## Notes

- Domain change: `celestrak.com` 301-redirects to `celestrak.org`. Most modern HTTP clients follow this transparently; legacy software (e.g., WxToImg) may break.
- 5-digit TLE catalog numbers run out at **69999**, projected **2026-07-20** — beyond that, new objects use 6-digit IDs and the legacy TLE format won't represent them. CelesTrak has supported OMM (Orbit Mean-Element Message) in JSON/XML/CSV/KVN since May 2020 — migrate now if your code only handles TLE.
- Supplemental GPEs (from owner/operators like the 2nd Space Operations Squadron for GPS) reduce uncertainty by an order of magnitude vs. SSN-derived GPEs.
- CelesTrak depends on Space-Track.org as the upstream source for SSN-derived data; outages there cascade here.
- Cross-listing: complementary to `gnss-interference` (GPS almanacs/GPEs).
