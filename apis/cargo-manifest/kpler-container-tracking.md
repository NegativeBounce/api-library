# Kpler Container Tracking (MarineTraffic)

REST container-tracking API (the former MarineTraffic container product, now Kpler) that tracks shipments by container or Bill of Lading and returns milestones, locations, and the vessels involved.

**Tier:** Enterprise
**Auth:** API key (`X-Container-API-Key` header)
**Last researched:** 2026-06-17

## Use cases

- Create a tracking request for a container or B/L and retrieve all milestones, locations, and vessels for that shipment.
- Pull shipping calls with vessel-call data (waiting time, arrival/departure) filtered by vessel name, port UNLOCODE, or status.
- Embed container + vessel visibility into logistics/supply-chain software.

## Pricing

- **Free tier:** None.
- **Paid tiers:** Not publicly documented (quote-based; part of Kpler/MarineTraffic commercial plans).
- **Enterprise:** Contact sales / partnerships team for API and sandbox access.
- **Notes:** Delivered via Kpler's broader maritime data offering (also available through ICE’s API/bulk file services for some datasets).

## Authentication

API key passed in the `X-Container-API-Key` request header; responses use the JSON:API media type (`Accept: application/vnd.api+json`). Keys provisioned by Kpler/MarineTraffic on a commercial plan.

## Endpoints

- **Base URL:** `https://api.kpler.com/v1`
- **Key endpoints:**
  - `POST` containers/shipments tracking requests — start tracking a container or B/L.
  - `GET /logistics/containers/shipping/calls` — shipping calls with vessel-call metrics (filter by vessel name, port, status).
  - `GET /logistics/containers/shipments/{shipmentId}/transportation-timeline` — milestones, locations, and vessels for a shipment.

## Example call

```bash
curl -H "X-Container-API-Key: $KPLER_CONTAINER_API_KEY" \
  -H "Accept: application/vnd.api+json" \
  "https://api.kpler.com/v1/logistics/containers/shipping/calls?filter[vessel.name][contains]=EMPIRE&include=vessels,ports,terminals"
```

## Rate limits

Not publicly documented (governed by commercial plan).

## SDKs / Libraries

- **Official:** None published (language-agnostic REST; docs show Node/request examples).
- **Community:** None notable.

## Documentation

- Main docs: https://container-tracking.marinetraffic.com/
- API reference: https://container-tracking.marinetraffic.com/ (Kpler container API reference)

## Notes

This is the container/logistics arm of Kpler (post-MarineTraffic acquisition) and is distinct from Kpler's commodity Cargo/Flows product (separate entry). Like JSONCargo it resolves BoL/container → vessel and milestones, but it's enterprise/quote-based rather than self-serve. For commodity-by-vessel ("what grade of crude is this tanker carrying"), use the Kpler Cargo entry. Overlaps `maritime-ais` (Kpler also runs the largest AIS network) — this entry is specifically the container/BoL tracking API.
