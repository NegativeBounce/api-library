# Dronetag Cloud Platform

A commercial Remote ID platform with a fully documented Cloud API (REST + Socket.io/WebSocket) that serves real-time and historical drone telemetry, aircraft/operation data, and airspace queries. Data originates from Dronetag's own receiver network (Scout stationary, RIDER portable) and transmitter/app users, deduplicated and fused server-side — so you can pull a drone picture for a region over the network, within the network's coverage footprint.

**Tier:** Freemium
**Auth:** API token (Bearer); see Authenticating API Requests
**Last researched:** 2026-06-17

## Use cases

- Pull current + historical Remote ID telemetry for a geographic region (bbox + time range) via REST without operating your own sensors, where Dronetag coverage exists.
- Stream real-time detections via Socket.io for live dashboards, C-UAS/UTM integration, or TAK.
- Manage aircraft, devices, operations, and flights in a Dronetag account programmatically.
- Integrate via InterUSS / network Remote ID, or push detections to your own API (webhooks/HTTP/MQTT distribution).

## Pricing

- **Free tier:** Free Drone Scanner app and developer documentation; basic account access. Receiver hardware (Scout/RIDER) and cloud features (e.g., RIDER Connect, Scout Cloud Mode) are paid.
- **Paid tiers:** Hardware purchase + cloud subscription tiers (RIDER Connect, Scout Cloud); pricing not publicly listed.
- **Enterprise:** City-wide / critical-infrastructure deployments; contact sales.
- **Notes:** REST is for current/historical pulls (manual); for real-time use Socket.io. Airspace telemetry endpoints require both a time range (from/to) and a region (bbox).

## Authentication

Obtain API credentials from your Dronetag account, then pass a Bearer token. Remote ID payloads use Dronetag's Unified Message Protocol (DUMP) format. See `https://help.dronetag.com/developers/data-pull/authenticating`. A 202 on stats endpoints means "refreshing — repeat request until 200."

## Endpoints

- **Base URL:** Per OpenAPI spec at `https://api-docs.dronetag.com/` (e.g., `/v2/airspace/*` for region telemetry).
- **Key endpoints:**
  - `GET /v2/airspace/...` — telemetry for a region (requires `bbox` + `from`/`to`).
  - Aircrafts API — `GET/POST/PATCH/DELETE` aircraft in the account.
  - Flights API — historical flight list + telemetry.
  - Devices / SIM management; Operations + annotations.
  - Socket.io endpoints — real-time telemetry streaming.

## Example call

```bash
# Pull telemetry for a bounding box over a time window
curl -H "Authorization: Bearer $DRONETAG_TOKEN" \
  "https://api.dronetag.com/v2/airspace/telemetry?bbox=14.3,50.0,14.6,50.2&from=2026-06-17T10:00:00Z&to=2026-06-17T11:00:00Z"
```

## Rate limits

Not publicly documented.

## SDKs / Libraries

- **Official:** OpenAPI specification (downloadable); REST + Socket.io documented. Open-source `dronetag/drone-scanner` receiver app.
- **Community:** OpenDroneID ecosystem (interoperable RID).

## Documentation

- Main docs: https://help.dronetag.com/developers
- API reference: https://api-docs.dronetag.com/

## Notes

- **Closest commercial answer to "ADS-B for drones" with a real API**, but coverage is bounded by where Dronetag receivers/app users are — not a universal passive feed. Sees only RID-compliant, broadcasting drones.
- Interoperates with TAK, SafeSky, Aloft; supports InterUSS network RID.
- Straddles detection/tracking: cataloged in `drone-tracking` because you can consume the network feed without owning hardware. (Owning a Scout/RIDER adds your own sensor coverage.)
