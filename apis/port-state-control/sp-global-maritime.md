# S&P Global Market Intelligence — Maritime (formerly IHS Markit)

Commercial vessel-database and maritime-data product (heritage Lloyd's Register / IHS Fairplay / IHS Markit, consolidated under S&P Global since 2022). Comprehensive vessel particulars, ownership, history, casualties, port calls, and PSC history.

**Tier:** Enterprise
**Auth:** API Key / OAuth (per contract)
**Last researched:** 2026-05-09

## Use cases

- Productised vessel database — IMO, ownership, beneficial owner, manager, technical manager, classification, history.
- Aggregated PSC inspection history across all MoU regions in a single query.
- Casualty and incident database (collisions, grounding, sinking) for risk modelling.
- Ownership-graph traversal — beneficial ownership, related entities.
- Marine credit-risk and operator-due-diligence workflows for banks, P&I clubs, and underwriters.
- Trade-flow / commodity-flow data layered on vessel movements.

## Pricing

- **Free tier:** None.
- **Paid tiers:** None publicly listed.
- **Enterprise:** Custom-quoted by S&P Global Maritime sales. Pricing scales with seats, dataset breadth, and API volume.
- **Notes:** Often bundled with related S&P Global products (Platts commodity prices, Maritime & Trade Atlas).

## Authentication

API key / OAuth 2.0 token issued post-contract. Customer-tenanted environment.

## Endpoints

- **Public site:** `https://www.spglobal.com/market-intelligence/en/solutions/maritime-trade`
- **API base URL:** Customer-issued.
- **Surface areas:**
  - Sea-web Vessels — vessel particulars + ownership
  - PSC history aggregated across MoUs
  - Casualty database
  - Movements / port-call history
  - Ownership graph
  - Maritime & Trade Atlas geospatial layer

## Example call

```bash
# Illustrative — actual endpoints provisioned per S&P Global contract.
curl -H "Authorization: Bearer $SPG_TOKEN" \
  "https://api.spglobal.com/maritime/v1/vessels/9525338?include=psc,casualty,ownership"
```

## Rate limits

Plan-dependent; not publicly documented.

## SDKs / Libraries

- **Official:** Customer-issued integration packages.
- **Community:** None (closed customer base).

## Documentation

- Main product page: https://www.spglobal.com/market-intelligence/en/solutions/maritime-trade
- Sea-web (vessel database): https://maritime.ihs.com/

## Notes

- Heritage matters: this is the lineal product of Lloyd's Register / IHS Fairplay / Janes Fighting Ships — the canonical vessel-data source going back to the 19th century.
- For Strait-of-Malacca counterparty due diligence, S&P Global gives a productised view that Equasis + MoU sites can't match — at enterprise pricing.
- Often paired with Lloyd's List Intelligence (separate product, owned by Maritime Intelligence) — adjacent feeds with overlapping but distinct strengths.
- Procurement is sales-led; expect a multi-week cycle.
