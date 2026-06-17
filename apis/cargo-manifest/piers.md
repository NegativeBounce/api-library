# PIERS (S&P Global)

The canonical U.S. waterborne bill-of-lading dataset — 40+ years of import/export shipment records (commodity, shipper, consignee, carrier, vessel, TEUs, value) covering 100% of U.S. port locations, plus selected international markets.

**Tier:** Enterprise
**Auth:** S&P Capital IQ Pro login / Data Lake / bulk feed (provisioned)
**Last researched:** 2026-06-17

## Use cases

- Pull the full set of U.S. ocean bill-of-lading records for a vessel, port, commodity, or company — including HS/SIC code, tonnage, TEUs, and estimated value.
- Market-share and trade-trend analysis, lead generation, fraud detection, and contract-compliance monitoring from transactional trade data.
- Feed enriched U.S. import/export shipment data into freight, pricing, or supply-chain models (as DAT, energy, chemical, and finance firms do).

## Pricing

- **Free tier:** None for production. Free data samples, dictionaries, and documentation available via the S&P Global Data Lake catalogue (registration required).
- **Paid tiers:** Not publicly documented (annual subscription; quote-based, tiered by module and coverage).
- **Enterprise:** Contact S&P Global Market Intelligence. Delivery via the Capital IQ Pro / Connect platform, the S&P Global Data Lake, or bulk file feed.
- **Notes:** ~60,000 U.S. BoLs processed daily within hours of CBP receipt; ~16M+ BoLs and 30M+ company records per year. Verified, standardized, and enriched (refrigerated-cargo flags, company data, D&B linkage).

## Authentication

Access through S&P Capital IQ Pro / Connect with a licensed account, or via the S&P Global Data Lake (catalogue registration is free; data access is contracted). Bulk/feed delivery credentials are provisioned per contract. No self-serve public REST key.

## Endpoints

- **Base URL:** Not publicly documented (platform + Data Lake / bulk feed delivery).
- **Key endpoints:** Not publicly documented. Primary access is the PIERS web product (Bill of Lading Search) and the S&P Global Data Lake dataset; programmatic delivery arranged with S&P.

## Example call

```bash
# No self-serve public API. Access is via S&P Capital IQ Pro / Connect,
# the S&P Global Data Lake (USA Import & Export Maritime Bills of Lading),
# or a contracted bulk feed. Contact S&P Global for delivery specs.
```

## Rate limits

Not publicly documented (governed by subscription / feed terms).

## SDKs / Libraries

- **Official:** None published (platform / Data Lake delivery; S&P Xpressfeed for some datasets).
- **Community:** None notable.

## Documentation

- Main docs: https://www.spglobal.com/market-intelligence/en/solutions/products/piers
- API reference: Not publicly documented. Dataset listing: https://www.marketplace.spglobal.com/en/datasets/bill-of-lading-piers-(277)

## Notes

The 40-year heritage U.S. BoL source (originated at IHS Markit, now S&P Global Maritime Intelligence) — widely regarded as the most authoritative U.S. waterborne trade dataset and the upstream source many resellers (e.g., DAT) license. Strongest on U.S.; international coverage spans ~13–18 markets (Central/South America, India, Vietnam, Turkey, etc.). Vessel name is on each U.S. maritime BoL. Trade-intelligence data, not a live manifest feed. Overlaps the catalog's `port-state-control` and `vessel-registry` S&P Global Maritime entries (those are PSC/registry products, not BoL shipment data) — this entry is specifically the PIERS bill-of-lading dataset. Sits alongside Panjiva, S&P's machine-learning supply-chain platform built on overlapping data.
