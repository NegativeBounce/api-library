# Panjiva (S&P Global)

S&P Global's supply-chain intelligence platform over 2 billion+ shipment records from 20+ governments, exposing bill-of-lading detail (commodity description, consignee, shipper) with ML-cleaned company profiles — available via API, Xpressfeed, and Snowflake.

**Tier:** Enterprise
**Auth:** Platform login; API / Xpressfeed / Snowflake (provisioned)
**Last researched:** 2026-06-17

## Use cases

- Resolve buyer–supplier relationships and a company's full shipment history from bill-of-lading records (commodity, consignee, shipper), including the carrying vessel on U.S. maritime records.
- Push shipment/company data into a CRM or quant model via API, Xpressfeed, or Snowflake.
- Sanctions/forced-labor and tariff-evasion network analysis across 2B+ records using Panjiva's ML entity resolution.

## Pricing

- **Free tier:** None (academic access exists via institutional partnerships, e.g., Redivis).
- **Paid tiers:** Not publicly documented (custom per business; quote-based).
- **Enterprise:** Contact S&P Global Market Intelligence. Delivery via the Panjiva web platform, REST API, Xpressfeed™, or Snowflake.
- **Notes:** Coverage cited at 2B+ shipment records, 8–9M+ company profiles, 190+ countries; granular bill-of-lading data from ~20+ contributing governments (U.S. + Brazil, China, India, Indonesia, Pakistan, Philippines, Sri Lanka, Turkey, Vietnam, Central/South America). U.S. is maritime-only; some countries include all transport modes.

## Authentication

Web platform via licensed account (registerable under an existing S&P Capital IQ Pro subscription). Programmatic delivery — REST API, Xpressfeed, or Snowflake share — is provisioned per contract. No self-serve public REST key.

## Endpoints

- **Base URL:** Not publicly documented (API provisioned to licensed customers).
- **Key endpoints:** Not publicly documented. Core access is the Panjiva web app (shipment/company search, alerts, exports); bulk/programmatic via API/Xpressfeed/Snowflake.

## Example call

```bash
# No self-serve public API. API / Xpressfeed / Snowflake access is provisioned
# under an S&P Global license. Contact S&P Global for endpoint specifications.
```

## Rate limits

Not publicly documented (governed by license / delivery channel).

## SDKs / Libraries

- **Official:** S&P Xpressfeed; Snowflake Data Share. No published public code SDK.
- **Community:** None notable.

## Documentation

- Main docs: https://www.spglobal.com/market-intelligence/en/solutions/products/panjiva-supply-chain-intelligence
- API reference: Not publicly documented (provided to licensed customers). Dataset listing: https://www.marketplace.spglobal.com/en/datasets/panjiva-supply-chain-intelligence-(22)

## Notes

The machine-learning-driven sibling to PIERS within S&P Global — Panjiva leans on entity resolution, HS-code imputation, and network analysis, while PIERS is the raw/enriched U.S. BoL dataset. They overlap heavily on underlying data; choose Panjiva for cleaned multi-country company-level supply-chain analysis and API/Snowflake delivery, PIERS for authoritative raw U.S. BoL. Vessel name present on U.S. maritime BoL records. Trade-intelligence data, not a live manifest feed. Confirmed to offer an API (per vendor/third-party listings), though endpoint specifics are behind licensing.
