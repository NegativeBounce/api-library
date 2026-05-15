# USNO Astronomical Applications API

US Naval Observatory's free public API delivering authoritative rise, set, and transit times for the Sun and Moon, civil twilight beginning/end, moon phases, eclipse data, and celestial navigation almanac data for any location and any date between 1700 and 2100.

**Tier:** Free
**Auth:** None (optional 8-character identifier parameter)
**Last researched:** 2026-05-15

## Use cases

- Litigation and legal use cases requiring authoritative US government astronomical data
- Historical research over centuries-wide date ranges (1700–2100)
- Celestial navigation training and operations
- Educational tools and planetarium software
- Reference baseline against which other astronomical APIs are validated

## Pricing

- **Free tier:** Unlimited under fair use
- **Paid tiers:** None
- **Enterprise:** N/A
- **Notes:** Free public service operated by the US Navy. Institutional users are asked to register an 8-character identifier by emailing usno-ops-center@us.navy.mil.

## Authentication

None required. An optional 8-character alphanumeric `ID` parameter may be set to identify your application; the identifier `AA` is reserved for internal use. Institutional users should register their ID with the USNO Operations Center.

## Endpoints

- **Base URL:** `https://aa.usno.navy.mil/api` (also reachable at `https://api.usno.navy.mil`)
- **Key endpoints:**
  - `GET /rstt/oneday` — Sun and Moon rise, set, transit, civil twilight, and moon phase for a single day at a location
  - `GET /rstt/year` — Full-year rise/set/transit/twilight table
  - `GET /moon/phases/year` — Primary lunar phase dates for a year
  - `GET /moon/phases/date` — Primary phases following a given date (count specified by `nump`)
  - `GET /siderealtime` — Sidereal time and equation of the equinoxes
  - `GET /celnav` — Celestial navigation almanac data
  - `GET /imagery/earth.png` — Day/night Earth map
  - `GET /imagery/moon.png` — Apparent disk of the Moon

## Example call

```bash
curl "https://aa.usno.navy.mil/api/rstt/oneday?date=2026-05-15&coords=40.7128N,74.0060W&tz=-5&ID=MyApp"
```

```python
import requests

resp = requests.get(
    "https://aa.usno.navy.mil/api/rstt/oneday",
    params={"date": "2026-05-15", "coords": "40.7128N,74.0060W", "tz": -5, "ID": "MyApp"},
)
data = resp.json()
sun = data["properties"]["data"]["sundata"]
moon = data["properties"]["data"]["moondata"]
```

## Rate limits

Not publicly documented. Service is intended for legitimate research, educational, and operational use; abusive volume may risk IP blocks. No formal SLA — provided as-is by the US government.

## SDKs / Libraries

- **Official:** None
- **Community:** Various unofficial wrappers on GitHub (e.g., `cbk/API-USNavalObservatory` Perl 6 wrapper); Python and Node wrappers on PyPI/npm

## Documentation

- Main docs: https://aa.usno.navy.mil/data/api
- API reference: https://aa.usno.navy.mil/data/docs/api.php

## Notes

- Date range supported: any date between 1700 and 2100 (inclusive) — by far the widest range of any provider in this category.
- Returns symbols indicating "continuously above horizon" or "continuously below horizon" at polar latitudes.
- No SLA and occasional downtime; not appropriate for hard real-time consumer applications without a fallback.
- See "Astronomical Data Used for Litigation" guidance at aa.usno.navy.mil before relying on data for legal proceedings.
- The underlying algorithms are the same that underpin TimeAndDate's commercial astronomy products.
