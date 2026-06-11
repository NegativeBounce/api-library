# Vessel Protect

Specialist Lloyd's-backed War-risks Managing General Agent (MGA) underwriting Marine War Risk, Kidnap & Ransom, and Increased Value Disbursement insurance.

**Tier:** Enterprise
**Auth:** N/A (underwriter / MGA, not a data feed)
**Last researched:** 2026-06-11

> **Not a data API.** Vessel Protect is an underwriting source (MGA), not a data provider. Cataloged for completeness so the war-risk-zones picture includes where cover is actually written, not just where risk is measured.

## Use cases

- Identifying a market source for placing Marine War Risk, K&R, and Increased Value Disbursement cover (relevant to the war-risk-broker and shipping-company personas).
- Understanding available war-risk capacity when modelling whether a transit is insurable/at what level.
- Mapping the insurance supply side alongside the zone-definition (JWC) and analytics (Concirrus) layers.

## Pricing

- **Free tier:** N/A.
- **Paid tiers:** N/A (insurance premiums, negotiated per risk).
- **Enterprise:** Broker/market engagement.
- **Notes:** Founded 2020; backed 100% by Lloyd's syndicates. Automatic capacity up to USD 250m, additional capacity for War P&I up to hull values.

## Authentication

N/A. Engagement is via brokers/the insurance market, not API credentials.

## Endpoints

- **Base URL:** No API. Company site: `https://www.vesselprotect.com/`
- **Key "endpoints":** None (insurance products, not data endpoints).

## Example call

```bash
# No API. Vessel Protect is an MGA; engage via a marine war-risk broker.
#   https://www.vesselprotect.com/home
```

## Rate limits

N/A.

## SDKs / Libraries

- **Official:** None.
- **Community:** None.

## Documentation

- Main docs: https://www.vesselprotect.com/home
- API reference: None (not a data provider).

## Notes

- Included per the "catalog both APIs and non-API sources, clearly tier-labeled" decision. This is firmly a **non-API** market source.
- Useful context for an intelligence product: knowing who writes war-risk cover (and at what capacity) helps frame the "is this insurable / at what cost" question your reports may need to answer.
- For programmatic war-risk data, use Concirrus, jwla.ai, Data Docked, or the JWC circular; Vessel Protect is the underwriting endpoint of that chain.
