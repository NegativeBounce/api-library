# Overhaul

Supply-chain risk management and visibility platform with real-time cargo-theft intelligence, in-transit monitoring, and theft response/recovery.

**Tier:** Enterprise
**Auth:** API key / platform (per contract)
**Last researched:** 2026-06-11

> **Commercial SaaS platform with API integration arranged per contract.** Offers programmatic visibility/risk data to subscribers; not a free public API.

## Use cases

- Real-time in-transit cargo monitoring with risk scoring and theft alerting along routes and at ports/hubs.
- Cargo-theft intelligence and trend reporting (publishes US/Canada cargo theft reports, e.g. Q1 2026, with hotspot analysis such as rising thefts in Memphis).
- Theft response and recovery coordination.
- Supply-chain risk integration into TMS/visibility stacks via API.

## Pricing

- **Free tier:** None (public quarterly theft reports are free; the platform is subscription).
- **Paid tiers:** Subscription to the Overhaul platform — not publicly priced.
- **Enterprise:** Bespoke integration, managed risk/recovery services — contact Overhaul.
- **Notes:** Pricing not public.

## Authentication

API key / platform credentials provisioned per contract. Integration (TMS, visibility) arranged with Overhaul.

## Endpoints

- **Base URL:** Not publicly documented (partner/enterprise API).
- **Key surfaces:**
  - Real-time shipment risk & monitoring.
  - Cargo-theft alerts and incident intelligence.
  - Reporting/analytics.

## Example call

```bash
# API access is provisioned per contract; base URL and auth are partner-specific.
# Public quarterly cargo theft reports: https://over-haul.com/us-cargo-theft-report/
```

## Rate limits

Not publicly documented (per contract).

## SDKs / Libraries

- **Official:** Not publicly documented.
- **Community:** None.

## Documentation

- Main site: https://over-haul.com/
- US cargo theft report: https://over-haul.com/us-cargo-theft-report/

## Notes

- Unlike the database/insurer sources, Overhaul leans **operational**: live in-transit monitoring + risk scoring + recovery, with an API designed to plug into logistics stacks — the most "integration-ready" of the cargo-crime entries.
- Free quarterly US/Canada cargo theft reports are a useful open input alongside Verisk CargoNet and BSI/TT Club.
- Cross-reference: `cargo-crime/verisk-cargonet.md`, `cargo-crime/bsi-connect-screen.md`; for vessel-side tracking see `maritime-ais/` and `dark-vessel-detection/`.
- Confirm endpoint/SDK details and data scope directly during sales scoping.
