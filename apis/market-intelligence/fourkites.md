# FourKites

Real-time supply-chain visibility platform providing multimodal shipment tracking, predictive ETAs, and disruption/risk alerting via API.

**Tier:** Enterprise
**Auth:** API Key / OAuth (per contract)
**Last researched:** 2026-06-11

## Use cases

- Real-time, multimodal (ocean, rail, road, air) shipment visibility and predictive ETAs to measure how security events and port disruption translate into delays.
- Port and network dwell/congestion signals and exception alerting for disruption monitoring.
- Feeding live in-transit status into an intelligence app's logistics layer for security→delivery-impact correlation.

## Pricing

- **Free tier:** None.
- **Paid tiers:** Subscription by volume/modules — not publicly priced.
- **Enterprise:** Bespoke integration (TMS/ERP), managed visibility — contact FourKites.
- **Notes:** Network-effect platform (carrier/ocean coverage); pricing per contract.

## Authentication

API key / OAuth credentials provisioned per contract; documented partner/enterprise API and webhooks.

## Endpoints

- **Base URL:** Partner/enterprise API (not publicly enumerated here).
- **Key surfaces:**
  - Shipment/load tracking (multimodal) and predictive ETA.
  - Ocean visibility (container/vessel milestones).
  - Exceptions/alerts and webhooks for disruption events.

## Example call

```bash
# API access is provisioned per contract; base URL and auth are account-specific.
# Platform overview: https://www.fourkites.com/
```

## Rate limits

Not publicly documented (per contract).

## SDKs / Libraries

- **Official:** API + integrations (TMS/ERP); details under account.
- **Community:** None notable.

## Documentation

- Main site: https://www.fourkites.com/
- Developer/API: https://www.fourkites.com/ (request access)

## Notes

- One of the two leading real-time visibility platforms (with Project44); choose based on existing carrier coverage and integration fit.
- Best for the **operational delay/disruption** dimension that index data (Drewry/FBX) doesn't capture — what's actually moving and how late.
- Cross-reference: `market-intelligence/project44.md` (direct peer), `port-congestion/` (congestion metrics), and `trade-flows/` (rate/flow context).
- Confirm endpoint/SDK specifics and data scope during sales scoping.
