# Volza

Global import/export trade-data platform (InfodriveIndia) with 3 billion+ bill-of-lading shipment records across 203 countries, sold on a pay-per-shipment credit model.

**Tier:** Paid
**Auth:** Login (platform); API on enterprise/contract
**Last researched:** 2026-06-17

## Use cases

- Search shipment-level BoL records by product, HS code, supplier, or buyer across 203 countries — including the vessel on covered maritime records.
- Buyer/supplier discovery and competitor sourcing analysis with verified company contacts.
- Price- and volume-trend analysis from actual shipment invoices.

## Pricing

- **Free tier:** None (3-day / 200-usage-point refund window advertised instead).
- **Paid tiers:** Credit-based ("points"). Points are deducted per shipment downloaded, and the deduction varies by country (e.g., 1 point per U.S. or India shipment; 10 points per Guatemala shipment). Subscriptions sold via PayPal/Paddle with instant activation. Exact point-package prices not fixed publicly.
- **Enterprise:** Custom/contract; API access negotiated here.
- **Notes:** Downloaded records are retained for re-download at no extra fee ("buy once").

## Authentication

Primary access is the Volza web platform via account login. API delivery exists for enterprise/contract customers — not a self-serve public key. Confirm API scope and auth with Volza sales.

## Endpoints

- **Base URL:** Not publicly documented (enterprise API).
- **Key endpoints:** Not publicly documented. Core product is the web platform (Global Partner Finder, Company Profiler, dashboards).

## Example call

```bash
# No self-serve public API. Enterprise API delivery is arranged with Volza;
# endpoint specs and credentials provided on contract.
```

## Rate limits

Not publicly documented (governed by points/credits and contract).

## SDKs / Libraries

- **Official:** None published.
- **Community:** None notable.

## Documentation

- Main docs: https://www.volza.com/bill-of-lading-database/
- API reference: Not publicly documented (enterprise).

## Notes

Largest advertised country breadth (203) among the customs/BoL vendors here, via a distinctive pay-per-shipment credit model rather than seat licensing — useful when you need a bounded number of records cheaply. Coverage depth per country varies, and consignee detail is subject to the same redaction limits as other CBP-derived datasets. Vessel name present on covered maritime BoL records. Trade-intelligence data, not a live manifest feed.
