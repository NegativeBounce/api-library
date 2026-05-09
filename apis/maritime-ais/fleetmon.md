# FleetMon

Hamburg-based AIS provider offering vessel tracking, ETA forecasts, fleet management, and vessel database access. Mix of self-service (Explorer) and API products targeted at logistics, port operations, and freight forwarders.

**Tier:** Paid
**Auth:** API Key (HTTP basic / username + key)
**Last researched:** 2026-05-09

## Use cases

- ETA forecasting for vessels approaching the Strait — FleetMon's "five next ports" AI model is differentiated.
- Tracking a fleet via "MyFleet" — push notifications for state changes (port-call, area enter/exit).
- Vessel database lookups via Vessel ID with extended particulars (dimensions, ownership, callsign).
- Last position queries within a customizable radius around an asset (rig, port, anchorage).
- Fleet-management dashboards in maritime ops shops where the Explorer UI is the primary interface and APIs back custom integrations.

## Pricing

- **Free tier:** None for APIs. Free demo of FleetMon Explorer interactive map.
- **Paid tiers:** FleetMon Explorer subscription starts at €54/month. API pricing is **not publicly listed** — request a quote.
- **Enterprise:** Custom contracts for high-volume ETA / fleet APIs.
- **Notes:** Pricing model historically credit/quota-based per API method, but tiers are negotiated rather than self-service.

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

- FleetMon's strength is the **ETA-forecast AI** (next-five-ports) — useful for predictive risk analysis on vessels approaching the Strait.
- Coverage is solid in European/Asian shipping lanes; the Strait sits in their busy-traffic core.
- Procurement cycle is shorter than MarineTraffic/Kpler but longer than Datalastic's self-service flow.
