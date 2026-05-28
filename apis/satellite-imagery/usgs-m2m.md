# USGS M2M API (EarthExplorer)

The USGS/EROS Machine-to-Machine RESTful JSON API for searching, ordering, and downloading the full Landsat record and 300+ free EROS datasets (the programmatic equivalent of EarthExplorer).

**Tier:** Free
**Auth:** ERS account login-token
**Last researched:** 2026-05-28

## Use cases

- Bulk searching and downloading Landsat (and historical/declassified) scenes by AOI, date, and cloud cover
- Building automated ingest pipelines for free public Earth-observation archives
- Programmatic metadata access mirroring everything available in EarthExplorer

## Pricing

- **Free tier:** Fully free — data is public domain; an account with the M2M MACHINE role is required
- **Paid tiers:** None
- **Enterprise:** N/A
- **Notes:** Access to the MACHINE role requires approval (submit a data-use survey; allow a couple of days).

## Authentication

Create an EROS Registration System (ERS) account and request MACHINE access at https://ers.cr.usgs.gov/profile/access. Authenticate via the `login-token` endpoint using your ERS username + a 64-character application token (the older password `login` endpoint was deprecated Feb 2025). The response returns an API key sent as `X-Auth-Token` on subsequent calls.

## Endpoints

- **Base URL:** `https://m2m.cr.usgs.gov/api/api/json/stable/`
- **Key endpoints:**
  - `POST /login-token` — authenticate, get session API key
  - `POST /dataset-search` — discover datasets
  - `POST /scene-search` — search scenes with spatial/temporal/metadata filters
  - `POST /download-options`, `/download-request`, `/download-retrieve` — get download URLs
  - `POST /logout` — end the session

## Example call

```bash
curl -X POST "https://m2m.cr.usgs.gov/api/api/json/stable/login-token" \
  -H "Content-Type: application/json" \
  -d '{"username":"<ERS_USERNAME>","token":"<APPLICATION_TOKEN>"}'
# Use the returned apiKey value as the X-Auth-Token header on subsequent requests
```

## Rate limits

Not formally published; clients should reuse session tokens and paginate. Excessive requests can trigger rate-limiting errors.

## SDKs / Libraries

- **Official:** USGS EROS code repos (code.usgs.gov/eros-user-services/machine_to_machine)
- **Community:** `landsatxplore`, `callusgs`, `m2m-api` (Python), and others

## Documentation

- Main docs: https://m2m.cr.usgs.gov/
- API reference: https://m2m.cr.usgs.gov/api/docs/json/

## Notes

Covers the entire Landsat record (Collection 2), NLCD, declassified satellite and historical aerial imagery. As of Aug 30, 2024, NASA LP DAAC products (e.g., MODIS) left M2M — use NASA Earthdata / CMR / AppEEARS for those instead.
