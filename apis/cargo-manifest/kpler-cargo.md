# Kpler Cargo / Flows

Commodity cargo-tracking data that reports what a specific tanker, gas carrier, or bulker is physically carrying — product, grade, volume, load/discharge — across 36,000+ vessels and hundreds of commodities.

**Tier:** Enterprise
**Auth:** API key / OAuth (provisioned)
**Last researched:** 2026-06-17

## Use cases

- Determine the commodity, grade, and volume aboard a named tanker/gas carrier, plus its load and (forecast) discharge ports.
- Track floating storage and ship-to-ship transfers to see what's on the water vs. onshore.
- Feed crude/LNG/LPG/refined-product flow data into trading, risk, or supply-chain models.

## Pricing

- **Free tier:** None.
- **Paid tiers:** Not publicly documented (quote-based; tiered by commodity packages — e.g., clean products, dirty products, LNG, LPG).
- **Enterprise:** Contact sales. Delivery via Kpler API, Excel Add-In, Snowflake Data Share, or Kpler LiveDB; some packages also available through ICE’s API/bulk file services.
- **Notes:** Coverage cited at 36,000+ vessels (16,000+ liquids tankers carrying chemical/clean/fuel cargoes), with full flow history including STS transfers. Uses AIS + port intelligence + ML destination forecasting.

## Authentication

Customer-provisioned credentials (API key / token, or OAuth depending on delivery channel). Issued by Kpler during onboarding; developers receive API documentation and sandbox access. No self-serve public key.

## Endpoints

- **Base URL:** Not publicly documented (Kpler API / LiveDB; partner-provisioned). Legacy AIS Vessels REST endpoints have been migrated to a Maritime 2.0 GraphQL API.
- **Key endpoints:** Not publicly documented in full — cargo/flows, vessel, port, and storage datasets exposed via the provisioned API, Snowflake share, or LiveDB tables.

## Example call

```bash
# Customer-provisioned. After onboarding, Kpler supplies the base URL,
# auth scheme, and dataset endpoints (REST/GraphQL, Snowflake, or LiveDB).
# Contact Kpler for cargo/flows API specifications.
```

## Rate limits

Not publicly documented (governed by contract / delivery channel).

## SDKs / Libraries

- **Official:** Kpler Excel Add-In; Snowflake Data Share / Kpler LiveDB access. No published public code SDK.
- **Community:** None notable.

## Documentation

- Main docs: https://www.kpler.com/product/commodities/cargo-analytics
- API reference: https://www.kpler.com/industries/software-technology (partner/sandbox docs on request)

## Notes

This is the "what is this vessel actually carrying" layer for bulk/liquid commodities — the closest thing to a real-time cargo manifest for tankers and gas/bulk carriers, where no public customs BoL exists. Distinct from the customs/BoL trade-data vendors (containerized goods by HS code) and from Kpler's Container Tracking entry (BoL→container). Overlaps the catalog's `trade-flows` (Kpler/Vortexa) and `maritime-ais`; this entry is specifically per-vessel commodity cargo. Vortexa (already in `trade-flows`) is the main competitor for oil/gas/products cargo intelligence.
