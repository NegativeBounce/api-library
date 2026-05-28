# Satellogic

Self-service tasking and archive ordering of sub-meter multispectral optical imagery from the Satellogic NewSat constellation, via the Aleph platform and API.

**Tier:** Paid
**Auth:** OAuth 2.0 (Client Credentials)
**Last researched:** 2026-05-28

## Use cases

- Standard or rush tasking of ~70cm/sub-meter optical imagery over a point or area of interest
- High-frequency change detection (up to 4–7 daily revisits) for economic/infrastructure monitoring
- Searching and ordering archive multispectral (RGB + NIR) imagery via a STAC-compliant catalog

## Pricing

- **Free tier:** None (Analysis API requests are free and don't create orders, but yield no imagery)
- **Paid tiers:** Transparent pricing — standard tasking from ~$8/km² (50 km² min), guaranteeing ≤20% cloud and <25° off-nadir; rush tasking delivered within 12–24h; archive cheaper
- **Enterprise:** Government sharing uplifts (+25%/+50%), public-release uplift (+200%), dedicated/constellation programs via sales
- **Notes:** A Contract defines which products (Archive, Standard, Rush) credentials can order; tasking order cutoff ~6h before collection.

## Authentication

OAuth 2.0 Client Credentials flow. POST `client_id`/`client_secret` (the "M2M Imagery Integrator" role) to the token endpoint to receive a bearer access token valid 24h. Every API request needs both the token (`authorizationToken: Bearer <token>` header) and a contract ID (`X-Satellogic-Contract-Id`).

## Endpoints

- **Base URL:** `https://api.satellogic.com` (token endpoint: `https://auth.platform.satellogic.com/oauth/token`)
- **Key endpoints:**
  - `GET /contracts` — list contracts available to your credentials
  - `GET /v2/orders/` — create/list tasking & archive orders
  - `GET /v2/captures/` — track captures by status/time
  - `GET /v2/deliverables/` — retrieve delivered products; STAC API for archive discovery

## Example call

```bash
# 1. Get a 24h access token
curl -X POST 'https://auth.platform.satellogic.com/oauth/token' \
  -H 'content-type: application/json' \
  -d '{"client_id":"<ID>","client_secret":"<SECRET>","audience":"https://api.satellogic.com/","grant_type":"client_credentials"}'

# 2. List your contracts
curl 'https://api.satellogic.com/contracts' \
  -H 'authorizationToken: Bearer <ACCESS_TOKEN>'
```

## Rate limits

Not publicly documented. SLAs (order cutoff, delivery time) are measured monthly at the 90th percentile, not per-capture.

## SDKs / Libraries

- **Official:** Aleph Documentation Center (REST API v2, Python examples)
- **Community:** Also resold via UP42 (`satellogic-tasking`)

## Documentation

- Main docs: https://developers.satellogic.com/
- API reference: https://developers.satellogic.com/aleph-v2/api/api_v2_specs.html

## Notes

Aleph v2 introduces a unified Orders model (Order → Capture → Deliverable state machine); existing v1 orders are auto-represented in v2. Processing levels L0–L1D_SR. Analysis API gives free, ephemeral (24h) collection-feasibility estimates — add ≥10 min buffer when converting to a task.
