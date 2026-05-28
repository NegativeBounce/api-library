# ICEYE

Programmatic tasking and archive purchase of synthetic aperture radar (SAR) imagery from the world's largest SAR satellite constellation, including automated object-detection derivatives.

**Tier:** Enterprise
**Auth:** OAuth 2.0
**Last researched:** 2026-05-28

## Use cases

- Tasking all-weather, day/night SAR captures of an AOI for crisis/flood/maritime monitoring
- Searching and purchasing from the 60,000+ image SAR archive catalog (STAC items)
- Requesting automated derivative products (object detection/classification) on captures

## Pricing

- **Free tier:** None (sponsored/open SAR data available for research, science, and app development by request)
- **Paid tiers:** Per-task and per-frame pricing exposed via the API (integrated tasking prices); requires a commercial contract
- **Enterprise:** Government/defense ISR, Tactical Access (last-minute tasking, direct downlink), and derivatives via contract
- **Notes:** Pricing is contract-specific; the API returns task/frame prices programmatically.

## Authentication

OAuth 2.0. Obtain credentials with an ICEYE contract, request an access token from the Authentication API, and pass it as a bearer token on Tasking, Catalog, Delivery, and Notifications API calls. Access tokens are managed/rotated per the token guide.

## Endpoints

- **Base URL:** `https://api.iceye.com` (ICEYE API Platform; see auth guide for token endpoint)
- **Key endpoints:**
  - `POST` Tasking API (v2) — check feasibility, get price, create/cancel task, request derivatives
  - `GET` Catalog API (v2) — list/search archive (STAC), get frame price, purchase frame
  - Delivery API (v1) — configure delivery destinations
  - Notifications API (v1) — register webhooks for order status

## Example call

```bash
# After obtaining an OAuth 2.0 access token, search the SAR archive catalog:
curl -H "Authorization: Bearer $ACCESS_TOKEN" \
  "https://api.iceye.com/<catalog-v2-search-path>"
```

## Rate limits

Not publicly documented; pagination is supported on list endpoints.

## SDKs / Libraries

- **Official:** ICEYE GitHub org (https://github.com/iceye-ltd); product documentation site
- **Community:** Not notable

## Documentation

- Main docs: https://docs.iceye.com/constellation/api/
- API reference: https://docs.iceye.com/constellation/api/specification/catalog/v2/

## Notes

SAR (radar) sees through cloud and darkness, unlike optical. Highest fidelity ~25cm. Imaging mode controls swath/resolution; incidence angles supported 10–45°. v1.0 of the API is deprecated in favor of v2.0 (migration guide available). "Tactical Access" allows re-tasking up to ~2 hours before overpass.
