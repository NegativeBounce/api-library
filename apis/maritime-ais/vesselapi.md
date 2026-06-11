# VesselAPI

Unified REST (and WebSocket) maritime data API delivering clean, normalized AIS positions, voyages, port events and vessel particulars for ~695K vessels and 117K ports, with a no-card free tier.

**Tier:** Freemium
**Auth:** API Key (Bearer)
**Last researched:** 2026-06-11

## Use cases

- Querying real-time vessel positions (lat/lon, SOG, COG, heading, nav status) by IMO, MMSI, or name without decoding raw NMEA.
- Sub-minute real-time tracking via WebSocket for monitoring dashboards; REST for periodic polling.
- Resolving vessel identity (MMSI/IMO/name/callsign) and static particulars for enrichment.
- Pulling port events, ETA data, NAVTEX messages, and emissions for voyage and exposure analysis.
- Low-friction prototyping on a free tier before scaling.

## Pricing

- **Free tier:** Free tier with no credit card required.
- **Paid tiers:** Usage-based subscriptions (specific price points not publicly fixed; see site).
- **Enterprise:** Higher-volume / SLA tiers on request.
- **Notes:** Positioned as a single integration replacing multiple scrapers/sources; handles AIS parsing, dedup, position validation, identity resolution server-side.

## Authentication

API key as Bearer token (`Authorization: Bearer YOUR_API_KEY`).

## Endpoints

- **Base URL:** `https://api.vesselapi.com/v1`
- **Key endpoints:**
  - `GET /search/vessels` — search by name/callsign/MMSI/IMO.
  - `GET /vessel/{id}` — particulars; `id` accepts MMSI or IMO (auto-resolves type).
  - `GET /vessel/{id}/position` — latest AIS position.
  - `GET /vessel/{id}/eta` — reported destination + ETA.
  - `GET /vessels/positions` — bulk positions for fleet monitoring.
  - WebSocket feed for sub-minute streaming.

## Example call

```bash
curl -X GET "https://api.vesselapi.com/v1/search/vessels?filter.name=EVERGREEN" \
  -H "Authorization: Bearer $VESSELAPI_KEY"
```

```python
from vessel_api_python import VesselClient
client = VesselClient(api_key="$VESSELAPI_KEY")
result = client.search.vessels(filter_name="Ever Given")
for v in result.vessels or []:
    print(f"{v.name} (IMO {v.imo})")
```

## Rate limits

Tier-dependent; sub-minute update capability advertised. Confirm per-plan limits at signup.

## SDKs / Libraries

- **Official:** Python (`vessel_api_python`), Node/TypeScript (`vesselapi`), Go (`vesselapi`) — with automatic retries/backoff, pagination iterators, typed errors.
- **Community:** Public docs + issue tracker at github.com/vessel-api/VesselApi.

## Documentation

- Main docs: https://vesselapi.com/
- API reference: https://vesselapi.com/ais-data-api (REST + WebSocket); GitHub: https://github.com/vessel-api/VesselApi

## Notes

- Strong developer experience (free tier, official SDKs, WebSocket) makes it a good independent alternative amid Kpler's consolidation of MarineTraffic/FleetMon/Spire.
- Best for coastal/terrestrial-grade coverage and supply-chain visibility; for guaranteed blue-water satellite AIS, pair with a satellite provider (Kpler/Spire, Searoutes).
- Cross-reference: VesselFinder (`maritime-ais/vesselfinder.md`) and Datalastic (`maritime-ais/datalastic.md`) occupy a similar self-service niche.
