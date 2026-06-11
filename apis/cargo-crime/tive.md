# Tive

Real-time shipment visibility platform using IoT trackers and a cloud API to deliver location, condition, and tamper/theft alerting for in-transit cargo.

**Tier:** Enterprise
**Auth:** API key / platform (per contract)
**Last researched:** 2026-06-11

> **Commercial IoT + SaaS platform with API integration.** Hardware trackers plus a cloud platform and API; not a free public data feed.

## Use cases

- Real-time, contextual theft alerting tied to a specific load — smart route-deviation, prolonged-stop, door-open, light-exposure, and seal-tamper events surfaced live.
- In-transit recovery: monitoring stolen shipments live to direct law enforcement (documented full-load recoveries).
- Condition monitoring (temperature, humidity, shock, light) for sensitive/perishable cargo through ports and over the road.
- API/TMS/ERP integration so alerts appear inside existing logistics workflows; layered security (Tive Seal + Solo trackers + monitoring team).

## Pricing

- **Free tier:** None.
- **Paid tiers:** Per-shipment / device + subscription — not publicly priced (noted as higher cost per shipment for the security-focused tier).
- **Enterprise:** Volume/managed-monitoring and integration — contact Tive.
- **Notes:** Hardware (trackers/seals) plus platform; pricing not public.

## Authentication

API key / platform credentials provisioned per contract. Documented API for integration into TMS/ERP/visibility stacks.

## Endpoints

- **Base URL:** Partner/enterprise API (not publicly enumerated here).
- **Key surfaces:**
  - Shipment tracking (location + condition).
  - Alerts/events (route deviation, stop, door, light, tamper).
  - Webhooks/integration into TMS/visibility platforms.

## Example call

```bash
# API access is provisioned per contract; base URL and auth are account-specific.
# Platform overview: https://www.tive.com/
```

## Rate limits

Not publicly documented (per contract).

## SDKs / Libraries

- **Official:** API + integrations (TMS/ERP/visibility); details under account.
- **Community:** None notable.

## Documentation

- Main site: https://www.tive.com/
- Security/cargo-theft content: https://www.tive.com/blog/cargo-security-basics-how-to-protect-shipments-from-theft-and-tampering

## Notes

- The most **sensor/IoT-centric** cargo-crime entry: detection comes from physical trackers/seals rather than an incident database — pairs naturally with database/intelligence sources (Verisk CargoNet, BSI SCREEN, TAPA TIS) and the operational platform Overhaul.
- API-first design makes it the easiest to integrate for live alerting in a custom intelligence app, but it covers your own monitored shipments, not industry-wide incident data.
- Cross-reference: `cargo-crime/overhaul.md` (operational peer), `cargo-crime/verisk-cargonet.md` and `cargo-crime/bsi-connect-screen.md` (incident intelligence).
- Confirm endpoint/SDK specifics and data-retention terms during sales scoping.
