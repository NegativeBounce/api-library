# FleetMon

Hamburg-based AIS provider (now part of Kpler) offering vessel tracking, ETA forecasts, fleet management, and vessel database access. Mix of self-service (Explorer) and API products targeted at logistics, port operations, and freight forwarders.

**Tier:** Paid
**Auth:** API Key (HTTP basic / username + key)
**Last researched:** 2026-06-11

## Use cases

- ETA forecasting for vessels approaching a port/region — FleetMon's "next five ports" AI model is differentiated.
- Tracking a fleet via "MyFleet" — push notifications for state changes (port-call, area enter/exit).
- Vessel database lookups via Vessel ID with extended particulars (dimensions, ownership, callsign).
- Last position queries within a customizable radius around an asset (rig, port, anchorage).
- Fleet-management dashboards in maritime ops shops where the Explorer UI is the primary interface and APIs back custom integrations.

## Pricing

- **Free tier:** None for APIs. Free demo of FleetMon Explorer interactive map.
- **Paid tiers:** FleetMon Explorer subscription starts at €54/month. API pricing is **not publicly listed** — request a quote.
- **Enterprise:** Custom contracts for high-volume ETA / fleet APIs.
- **Notes:** Pricing model historically credit/quota-based per API method, but tiers are negotiated rather than self-service. Now under Kpler's commercial umbrella (see Kpler consolidation note below).

## Authentication

Username + API key (HTTP Basic Auth or query-param credentials), provisioned through the FleetMon Developer portal after subscription.

## Endpoints

- **Base URL:** `https://api.fleetmon.com/` (production)
- **Key endpoints / API products:**
  - **Vessel Search** — by Vessel ID, returning particulars.
  - **Last Position** — current position for a vessel or list.
  - **Vessels in Radius** — last positions within a radius of an asset.
  - **MyFleet** — positions and events for a customer-defined fleet.
  - **ETA Forecast** — AI-predicted next-five-ports list.
  - **Port Calls** — arrival/departure events for a port or vessel.

## Example call

```bash
# Illustrative — exact endpoint paths require developer-portal access.
curl -u "$USERNAME:$API_KEY" \
  "https://api.fleetmon.com/vessel/v1/last_position?mmsi=566093000"
```

## Rate limits

Not publicly documented. Defined per contract / per API method.

## SDKs / Libraries

- **Official:** None broadly published.
- **Community:** `fitnr/fleetmonger` (Python wrapper for legacy FleetMon API; lightly maintained).

## Documentation

- Developer portal: https://developer.fleetmon.com/
- API suite overview: https://developer.fleetmon.com/api-suite/
- Pricing: https://www.fleetmon.com/pricing-plans/

## Notes

- ⚠️ **Kpler consolidation:** FleetMon was acquired by Kpler in a coordinated deal alongside **MarineTraffic** (March 2023) and **Spire Maritime** — combining three maritime data providers under one umbrella. FleetMon currently retains its own brand, Explorer product, developer portal, and the €54/mo entry tier, but commercial terms and roadmap now sit within Kpler. Re-verify current pricing/portal status before committing.
- FleetMon's standout is the **ETA-forecast AI** (next-five-ports) — useful for predictive risk analysis on vessels approaching a chokepoint.
- Coverage is solid in European/Asian shipping lanes.
- Procurement cycle is shorter than MarineTraffic/Kpler enterprise but longer than Datalastic's self-service flow.
- Cross-reference: sibling Kpler-owned feeds MarineTraffic (`maritime-ais/marinetraffic.md`) and Spire Maritime (`maritime-ais/spire-maritime.md`); parent commodity-flows product `trade-flows/kpler.md`.
