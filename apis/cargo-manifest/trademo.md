# Trademo

Global trade-intelligence platform with a documented REST API (Trademo Intel) over 3 billion+ bill-of-lading / customs shipment records, returning products, parties, ports, and vessel fields.

**Tier:** Paid
**Auth:** API key (developer API); platform login for Intel UI
**Last researched:** 2026-06-17

## Use cases

- Programmatically pull shipment records for an HS code, shipper, consignee, or country — including the vessel name on each U.S. maritime BoL.
- Embed supplier/buyer discovery and supply-chain mapping into an internal app via API.
- Combine shipment data with Trademo's sanctions/controls APIs for compliance screening.

## Pricing

- **Free tier:** Free trial / free API exploration advertised; no permanent free production tier.
- **Paid tiers:** Self-serve subscriptions using Download Credits (shipment data, company profiles, analytics) and Value-Add Credits (contact info, due-diligence). Exact credit prices not publicly fixed — quote/self-serve via pricing page.
- **Enterprise:** Custom data feeds and higher API volumes on contract.
- **Notes:** U.S. trade data updated daily; some international datasets lag. Coverage cited as 65%+ of global trade at transaction level across 190+ countries (raw granular BoL coverage is narrower, ~15+ countries / ~45% per their materials).

## Authentication

REST APIs authenticate with an API key issued from the Trademo account. The Global Trade Shipments API accepts query parameters (HS code, shipper/consignee name, shipper/consignee country, ports). Obtain keys via the Trademo Intel account / API console.

## Endpoints

- **Base URL:** Not publicly documented in full (per-API base paths under trademo.com/apis).
- **Key endpoints:**
  - Global Trade Shipments API — find shipments by HS code, company, country, port (returns shipment-level records incl. vessel where present).
  - Global Commodity API — trade volumes/value/duty between two countries for an HS code.
  - Controls API / Sanctions screening APIs — compliance content (separate products).

## Example call

```bash
# Illustrative — confirm exact base URL, path, and param names in Trademo's
# API console after obtaining a key.
curl -H "Authorization: Bearer $TRADEMO_API_KEY" \
  "https://api.trademo.com/intel/shipments?hs_code=2709&consignee_country=US"
```

## Rate limits

Not publicly documented (governed by plan credits / API contract).

## SDKs / Libraries

- **Official:** None published (language-agnostic REST).
- **Community:** None notable.

## Documentation

- Main docs: https://www.trademo.com/apis
- API reference: https://www.trademo.com/apis/global-trade-shipments-api (per-API pages; full reference behind account)

## Notes

The most clearly API-first of the customs/BoL trade-data vendors, which is why it's included alongside the heavier platform products (Datamyne, ImportGenius). Vessel name is a field on U.S. maritime BoL records. Coverage percentages vary across Trademo's own pages (65% of global trade vs. ~45% from 15+ countries of granular BoL) — treat the higher number as marketing-level and the lower as raw shipment coverage. Trade-intelligence data, not a live manifest feed.
