# MyShipTracking

Terrestrial-AIS vessel tracking API delivering real-time and historical vessel positions, port data, historical tracks and fleet-management functions in a standardized response envelope.

**Tier:** Freemium
**Auth:** API Key
**Last researched:** 2026-06-11

## Use cases

- Real-time tracking of individual vessels (position, speed, course, voyage info) in coastal/terrestrial AIS range.
- Building maritime dashboards and custom fleet solutions on a consistent, documented REST API.
- Pulling historical vessel tracks for route reconstruction and pattern analysis.
- Port-level lookups (vessels in port, expected arrivals) for terminal/operations workflows.

## Pricing

- **Free tier:** Limited free access / trial tier (interactive live map is free on the website).
- **Paid tiers:** Subscription plans by request volume / feature set (specific price points not publicly fixed).
- **Enterprise:** Higher-volume plans on request.
- **Notes:** Exclusively terrestrial AIS — significantly cheaper than satellite providers but limited to ~coastal coverage (within roughly 50 nm of shore).

## Authentication

API key, passed per the documented header/parameter scheme. Provisioned via account signup.

## Endpoints

- **Base URL:** `https://api.myshiptracking.com/`
- **Key endpoints (per docs):**
  - Single vessel position (current position, speed, course, voyage).
  - Vessels in area / bounding box.
  - Port calls / expected arrivals.
  - Historical track for a vessel between dates.
  - Fleet management (saved vessel lists, events).
- Responses use a standardized envelope; docs include multi-language code snippets per endpoint.

## Example call

```bash
# Illustrative; confirm exact path/auth header from MyShipTracking API docs
curl -H "Authorization: Bearer $MST_API_KEY" \
  "https://api.myshiptracking.com/api/v2/vessel?mmsi=566093000"
```

## Rate limits

Not publicly published; plan-dependent. Confirm at signup.

## SDKs / Libraries

- **Official:** None language-specific; REST/JSON with per-endpoint code snippets in docs.
- **Community:** None notable.

## Documentation

- Main docs: https://api.myshiptracking.com/
- Live map / coverage: https://www.myshiptracking.com/

## Notes

- Good budget terrestrial option; for transoceanic legs supplement with satellite AIS (Kpler/Spire, Searoutes).
- Cross-reference: similar terrestrial niche to VesselFinder (`maritime-ais/vesselfinder.md`), Datalastic (`maritime-ais/datalastic.md`), VesselAPI (`maritime-ais/vesselapi.md`).
- Confirm historical-depth and update-cadence limits against your use case before committing.
