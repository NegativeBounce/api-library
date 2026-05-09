# Kharon

Sanctions, financial-crimes, and supply-chain risk analytics platform built for compliance teams at major banks and Fortune 100 companies. Combines an investigative research bench (Kharon Core) with platforms (ClearView, GraphCast) for entity screening and risk-graph integration.

**Tier:** Enterprise
**Auth:** API Key / OAuth (issued per contract)
**Last researched:** 2026-05-09

## Use cases

- Sanctions and forced-labor screening on Strait-transiting vessels, charterers, and cargo originators — Kharon is widely cited in OFAC and EU enforcement actions.
- Military end-use compliance — relevant if cargo or vessel ownership has dual-use exposure.
- Investment risk screening for institutional investors with Strait-related supply-chain exposure.
- ClearView visual analytics for KYC and counterparty investigations.
- GraphCast integration to enrich existing screening / AI systems with Kharon's risk graph.

## Pricing

- **Free tier:** None.
- **Paid tiers:** None publicly listed.
- **Enterprise:** Custom-quoted. Pricing scales with seats, dataset breadth, and integration depth.
- **Notes:** Customers include 7 of 10 largest U.S. banks and 6 of 10 largest EU banks — implies Tier-1 enterprise pricing.

## Authentication

API key / OAuth 2.0 token issued during Kharon onboarding. Customer-tenanted.

## Endpoints

- **Public site:** `https://www.kharon.com/`
- **API base URL:** Customer-issued.
- **Surface areas:**
  - ClearView — visual analytics platform for KYC + investigations
  - Kharon Core — research/data infrastructure
  - GraphCast — risk-graph integration into existing systems
  - The Brief — analyst research products

## Example call

```bash
# Illustrative — actual endpoints provisioned per Kharon contract.
curl -H "Authorization: Bearer $KHARON_TOKEN" \
  "https://api.kharon.com/v1/entities/search?name=Pelayaran%20Tempuran&country=ID"
```

## Rate limits

Not publicly documented.

## SDKs / Libraries

- **Official:** Customer-issued integration packages.
- **Community:** None.

## Documentation

- Main site: https://www.kharon.com/
- Contact: info@kharon.com / +1 424-320-2977

## Notes

- Strong fit if your stack already includes a screening engine (e.g., Refinitiv, ComplyAdvantage) and you want to enrich it with Kharon's risk graph rather than replace.
- Customer testimonials cite ~5x productivity gains on screening workloads.
- Less of a "raw API" than a curated risk-intelligence platform — pairs naturally with Sayari (graph), OpenSanctions (free fallback), and Pole Star PurpleTRAC (vessel-specific screening).
