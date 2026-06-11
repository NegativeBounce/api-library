# MarineTraffic Vessel Particulars & Ownership API

GraphQL API (now part of Kpler) returning comprehensive vessel particulars and the full ownership/management structure for IMO-registered vessels.

**Tier:** Enterprise
**Auth:** API Key
**Last researched:** 2026-06-11

> **Ownership note (2026):** MarineTraffic is now part of Kpler; the Vessels API is documented under kpler.com. The Vessel Ownership feature is available on the Enterprise plan and only for vessels with an IMO number.

## Use cases

- Conducting due diligence with the full ownership tree: beneficial owner, registered owner, commercial manager/disponent owner, operator/charterer, technical manager, ISM manager.
- Retrieving associated companies — ship builder, engine builder, classification society, P&I club — for risk and compliance.
- Partial-match search on vessel name or ownership strings to identify vessels from incomplete data.
- Enriching insurance/war-risk reports with granular particulars across 220k+ IMO vessels (updated daily).

## Pricing

- **Free tier:** None.
- **Paid tiers:** Vessel Ownership is exclusive to the Enterprise plan; pricing via plan comparison/sales.
- **Enterprise:** Contact sales (via Kpler).
- **Notes:** Credit/seat structure varies by plan. Ownership data requires Enterprise tier.

## Authentication

API key per Kpler/MarineTraffic contract. GraphQL endpoint; key passed per documented header scheme.

## Endpoints

- **Base URL:** Kpler/MarineTraffic GraphQL endpoint (provided on contract; see kpler.com vessels API docs).
- **Key endpoints:**
  - GraphQL `vessels` query — particulars + ownership + associated companies, filterable with multiple logical operators; supports partial-data searches.
  - Legacy REST "Vessel Particulars" endpoint exists but is deprecated in favor of the GraphQL Vessel Particulars & Ownership product.

## Example call

```bash
# Illustrative GraphQL shape; confirm endpoint/headers from Kpler docs
curl -X POST "$KPLER_MT_GRAPHQL_URL" \
  -H "Authorization: Bearer $MT_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"query":"{ vessels(imo:\"9811000\"){ name imo flag registeredOwner beneficialOwner ismManager classSociety piClub } }"}'
```

## Rate limits

Per contract (calls/time-period defined in the API key's contract). Not publicly fixed.

## SDKs / Libraries

- **Official:** GraphQL; any GraphQL client. Kpler provides docs/sample responses.
- **Community:** Standard GraphQL libraries.

## Documentation

- Main docs: https://www.kpler.com/product/maritime/vessels-api
- API reference: Kpler maritime API docs; legacy at servicedocs.marinetraffic.com

## Notes

- **Cross-reference:** MarineTraffic AIS positions are in `maritime-ais`, and a MarineTraffic congestion product is in `port-congestion`. This entry is the distinct **particulars & ownership** product.
- Ownership only returned for IMO-registered vessels; non-IMO vessels excluded.
- Strong fit for the ownership-tree + class + P&I needs of insurance/war-risk and sanctions screening.
- Verify current Kpler endpoint and licensing terms before building — branding/endpoints are migrating post-acquisition.
