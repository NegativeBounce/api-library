# Datalastic

Maritime tracking REST API providing real-time vessel positions, ETA, port data, and historical track for 750,000+ vessels. Lower-cost commodity AIS feed with published pricing tiers and quick self-service onboarding.

**Tier:** Paid
**Auth:** API Key (query parameter)
**Last researched:** 2026-05-09

## Use cases

- Cost-effective continuous tracking of vessels in/near the Strait via `/vessel_inradius` or area queries.
- Bulk vessel state lookups (up to 100 MMSI per request) via `/vessel_bulk`.
- Port arrival monitoring for Singapore, Port Klang, Belawan, and Tanjung Pelepas via `/port_find` + tracking endpoints.
- Historical track replay for incident investigation.
- Quick prototyping — published pricing and an inexpensive €9 trial make it easy to start without a sales cycle.

## Pricing

- **Free tier:** None outright, but a 14-day trial at €9 lets you evaluate the API.
- **Paid tiers (monthly):**
  - **Starter:** €199/month, 20,000 credits.
  - **Experimenter:** €569/month, 80,000 credits.
  - **Developer Pro+:** €679/month, unlimited credits.
  - "+ Add-Ons" variants exist at higher prices for richer datasets.
- **Annual billing:** ~10% discount (Starter €179/mo, Experimenter €512/mo, Developer Pro+ €611/mo equivalent).
- **Enterprise:** Custom contracts available.
- **Notes:** 1 credit = 1 vessel returned per request. Credit allowance resets each billing cycle. 14-day money-back guarantee on all tiers.

## Authentication

API key issued at signup, passed as `?api-key=...` query parameter on every call.

## Endpoints

- **Base URL:** `https://api.datalastic.com/api/v0/`
- **Key endpoints:**
  - `GET /vessel` — basic real-time tracking by MMSI/IMO/UUID
  - `GET /vessel_pro` — extended (ETA, draft, destination)
  - `GET /vessel_bulk` — up to 100 vessels in one call
  - `GET /vessel_inradius` — vessels within radius of a point or another vessel
  - `GET /vessel_find` — search by type, country, specs
  - `GET /port_find` — port lookup
  - `GET /vessel_info` — detailed vessel particulars
  - `POST /report` — async report generation

## Example call

```bash
curl "https://api.datalastic.com/api/v0/vessel?api-key=$API_KEY&mmsi=566093000"
```

```bash
# Vessels within 50 nm of the Port of Singapore
curl "https://api.datalastic.com/api/v0/vessel_inradius?api-key=$API_KEY&lat=1.290&lon=103.851&radius=50"
```

## Rate limits

- 600 API calls per minute, account-wide.
- Monthly credit allowance varies by plan (20,000 → unlimited).

## SDKs / Libraries

- **Official:** None.
- **Community:** Various third-party wrappers; none with significant adoption.

## Documentation

- Pricing: https://datalastic.com/pricing/
- API reference: https://datalastic.com/api-reference/
- Onboarding guide: https://datalastic.com/blog/how-to-use-datalastic-maritime-api/

## Notes

- Best fit when budget matters and you don't need MarineTraffic-grade coverage or guarantees. Coverage is generally good in busy traffic lanes (including the Strait of Malacca) but thinner in remote ocean.
- Servers in Munich, Germany; the company reports 99.8% uptime in 2024.
- Email + Telegram support — fast response time but not enterprise-grade SLA.
