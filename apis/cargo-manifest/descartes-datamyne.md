# Descartes Datamyne

Bill-of-lading and customs trade database that exposes shipment-level records — products, shippers/consignees, ports, volumes, and the vessel carrying each shipment — across 190+ countries.

**Tier:** Enterprise
**Auth:** Login (platform); bulk/API delivery on contract
**Last researched:** 2026-06-17

## Use cases

- Identify what a named vessel carried into U.S. ports by drilling from bill-of-lading records to product, shipper, and consignee.
- Map a company's supply chain — suppliers, trade lanes, volumes, and prices paid — from customs manifests.
- Sanctions/forced-labor and trade-compliance investigations using HS-code-classified shipment records.

## Pricing

- **Free tier:** None.
- **Paid tiers:** Not publicly documented (quote-based; tiered by country/market coverage and seat count).
- **Enterprise:** Contact sales. Bulk file and API delivery available under contract.
- **Notes:** U.S. maritime import records are added daily, ~24 hours after receipt from U.S. CBP. Coverage advertised at 190+ countries / 250 markets.

## Authentication

Web platform access via account login. Programmatic/bulk delivery (including API keys and S3/secure-link extracts) is provisioned per contract — credentials issued by Descartes during onboarding. No self-serve public API key.

## Endpoints

- **Base URL:** Not publicly documented (customer-provisioned API/bulk delivery).
- **Key endpoints:** Not publicly documented. Primary access is the Datamyne web application; API/bulk extracts are arranged with Descartes.

## Example call

```bash
# No public API. Access is via the Datamyne web platform or a contracted
# data feed (API key / S3 extract) provisioned during onboarding.
# Contact Descartes for endpoint specifications.
```

## Rate limits

Not publicly documented (governed by contract / data-feed terms).

## SDKs / Libraries

- **Official:** None published.
- **Community:** None notable.

## Documentation

- Main docs: https://www.datamyne.com/our-product/bill-of-lading-database/
- API reference: Not publicly documented (provided to contracted customers).

## Notes

Part of Descartes Systems Group. Strongest on U.S. CBP maritime bill-of-lading data, with broad international customs coverage layered on. Vessel name is a field on each U.S. maritime BoL record, so the database can answer "what did vessel X carry" for covered lanes — but it is a trade-intelligence product, not a live cargo feed. Some consignee/shipper records are redacted at the importer's request, and air/land coverage is narrower than ocean. Overlaps the catalog's `vessel-registry` (ownership/particulars) and `trade-flows` (aggregate flows) — this entry is specifically the shipment/manifest layer.
