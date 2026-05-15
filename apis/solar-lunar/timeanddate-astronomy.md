# TimeAndDate Astronomy API

Paid subscription REST API delivering authoritative sunrise, sunset, moonrise, moonset, twilight start/end, day length, exact moon phase moments, body altitude/distance/azimuth, and tide data — based on US Naval Observatory and NASA JPL ephemeris data.

**Tier:** Paid
**Auth:** Access Key + Secret Key (signed requests)
**Last researched:** 2026-05-15

## Use cases

- Maritime/marine applications needing tide + astronomy from a single provider
- Insurance and litigation use cases requiring USNO-grade source data
- Aviation operations planning
- Smart home and smart city automation triggered by precise solar events
- Agriculture and farming applications driven by day length and twilight

## Pricing

- **Free tier:** 3-month free trial of the full API
- **Paid tiers:** Access starts at $99/year per recent pricing pages; legacy tiers (Astronomy 5 at $50/year for 5 cities and 50K requests; Astronomy Full at $300/year for 10 cities and 100K requests) have been published historically — confirm current pricing at signup
- **Enterprise:** Custom packages on request
- **Notes:** Reselling, sublicensing, or compiling data into third-party databases requires a separate agreement. Norwegian customers add 25% MVA. Pricing has evolved over time.

## Authentication

Sign up at dev.timeanddate.com for an account; receive an Access Key and a Secret Key. Requests are signed (HMAC-style) — refer to the developer docs for the exact signing format. Locations can be queried by `placeid`, geographic coordinates, or IATA airport codes.

## Endpoints

- **Base URL:** `https://api.xmltime.com` (legacy endpoint; current docs published at dev.timeanddate.com)
- **Key endpoints:**
  - `astrodata` — Astro Position service: precise sun/moon altitude, distance, azimuth at a point in time
  - `astronomy` — Astro Event service: sunrise, sunset, moonrise, moonset, twilight, moon phases
  - `tides` — Tide service: high/low tide points and hourly sea levels for chosen coordinates

## Example call

```bash
curl "https://api.xmltime.com/astronomy?accesskey=$ACCESS_KEY&secretkey=$SECRET_KEY\
&placeid=usa/new-york&object=sun,moon&startdt=2026-05-15&enddt=2026-05-22\
&types=rise,set,twilight&out=json"
```

## Rate limits

Per-plan request caps (50,000–100,000/year on legacy plans; current plans vary). Query limits restrict number of cities and date range per request (e.g., 31-day windows on certain tiers).

## SDKs / Libraries

- **Official:** XML/JSON endpoints with sample code in PHP, Java, Python, and .NET on the developer site
- **Community:** Limited — most users build thin clients due to the signed-request auth model

## Documentation

- Main docs: https://dev.timeanddate.com/astro/
- API reference: https://dev.timeanddate.com/docs/

## Notes

- Algorithms are derived from US Naval Observatory and NASA JPL ephemeris data — among the most authoritative sources commercially available.
- API access is paid-only; the free trial is the only no-cost path.
- CSV and XML download formats are available alongside the API for non-developer users.
- Pricing tiers have changed over the years; numbers above reflect the most recent public pricing snapshot and may shift — confirm at signup.
