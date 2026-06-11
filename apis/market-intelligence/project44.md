# Project44

Supply-chain visibility platform (Movement) providing real-time multimodal tracking, predictive ETAs, ocean/port intelligence, and disruption alerting via API.

**Tier:** Enterprise
**Auth:** API Key / OAuth (per contract)
**Last researched:** 2026-06-11

## Use cases

- High-fidelity ocean and multimodal shipment tracking with predictive ETAs to measure delay impact from security events and port disruption.
- Port/terminal dwell, congestion, and transit-time analytics for disruption monitoring.
- Webhook-driven exception alerting to feed an intelligence app's logistics-impact layer.

## Pricing

- **Free tier:** None.
- **Paid tiers:** Subscription by volume/modules — not publicly priced.
- **Enterprise:** Bespoke integration (TMS/ERP), managed visibility — contact Project44.
- **Notes:** Strong ocean/carrier network coverage; pricing per contract.

## Authentication

API key / OAuth credentials provisioned per contract; documented REST API and webhooks for partners.

## Endpoints

- **Base URL:** Partner/enterprise API (not publicly enumerated here).
- **Key surfaces:**
  - Shipment tracking (ocean, rail, road, parcel) + predictive ETA.
  - Ocean/port visibility and milestones.
  - Webhooks for status/exception events.

## Example call

```bash
# API access is provisioned per contract; base URL and auth are account-specific.
# Platform overview: https://www.project44.com/
```

## Rate limits

Not publicly documented (per contract).

## SDKs / Libraries

- **Official:** REST API + integrations (TMS/ERP); developer docs under account.
- **Community:** None notable.

## Documentation

- Main site: https://www.project44.com/
- Developer/API: https://developers.project44.com/ (access via account)

## Notes

- The other leading real-time visibility platform alongside FourKites; pick based on carrier coverage, ocean depth, and integration fit.
- Best for the **operational delay/disruption** signal that index data doesn't show — what's moving and how late after a disruption.
- Cross-reference: `market-intelligence/fourkites.md` (direct peer), `port-congestion/`, and `maritime-ais/` for vessel-level position context.
- Confirm endpoint/SDK specifics and data scope during sales scoping.
