# Drewry

Independent maritime research consultancy publishing the World Container Index and other freight-rate and port indices used as benchmarks across global shipping.

**Tier:** Freemium
**Auth:** Registration (free indices) / Subscription
**Last researched:** 2026-06-11

## Use cases

- Quantifying the freight-cost impact of maritime-security events: the World Container Index (WCI) and Intra-Asia Container Index (IACI) track spot rates that spike on rerouting/disruption (IACI noted as ~75% above pre-Iran-conflict levels in 2026 due to Hormuz disruption and bunker costs).
- Monitoring cancelled-sailings, port-throughput, and capacity trackers for disruption signals.
- Benchmarking index-linked contract rates and building security→cost narratives for reports.

## Pricing

- **Free tier:** Free indices/trackers (WCI, IACI, Cancelled Sailings, Port Throughput) with site registration/login.
- **Paid tiers:** Container Freight Rate Insight (CFRI) — spot rates across 6,700 port pairs (annual subscription); benchmarking and forecast products.
- **Enterprise:** Advisory/procurement support, Benchmarking Club (shippers/BCOs only).
- **Notes:** WCI is widely referenced; free indices require registration and are published as web pages/PDFs rather than a documented public REST API.

## Authentication

Free registration/login for free indices; subscription credentials for CFRI and premium products. No documented public self-serve API.

## Endpoints

- **Base URL:** No public API. Indices hub + subscription services.
- **Key surfaces:**
  - World Container Index (weekly, 8 East-West lanes + composite).
  - Intra-Asia Container Index (weekly, 18 routes).
  - Cancelled Sailings / Port Throughput trackers.
  - CFRI online service (subscription).

## Example call

```bash
# No public self-serve API. Free indices via registration at drewry.co.uk;
# CFRI spot-rate data is a paid online service / PDF, integration arranged per contract.
```

## Rate limits

N/A (web/portal). Per contract for subscription data services.

## SDKs / Libraries

- **Official:** None.
- **Community:** Some third parties republish WCI values (e.g. macro data aggregators) — verify licensing before redistribution.

## Documentation

- Trackers & indices: https://www.drewry.co.uk/trackers-and-indices/latest-trackers-and-indices
- WCI methodology: https://www.drewry.co.uk/logistics-executive-briefing/logistics-executive-briefing-articles/world-container-index-methodology

## Notes

- The **single most useful freight-rate benchmark** for security→cost correlation; the IACI's explicit "pre-conflict vs now" framing is ideal for intelligence reporting.
- No clean API: free indices need registration and parsing; the paid CFRI is the route to structured spot-rate data. Plan ingestion accordingly.
- Cross-reference: `trade-flows/freightos-baltic-index.md` (FBX, has an API), `trade-flows/xeneta.md` (rate analytics API), and `trade-flows/baltic-exchange.md` (dry-bulk/tanker indices) already in the catalog.
