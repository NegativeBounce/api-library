# LSEG World-Check One (Refinitiv)

Industry-standard PEP, sanctions, adverse-media, and enforcement-action screening dataset and API platform. Now part of LSEG (formerly Refinitiv). 4M+ structured records, 60+ risk topics, daily updates from global research centres.

**Tier:** Enterprise
**Auth:** API Key / OAuth (per contract)
**Last researched:** 2026-05-09

## Use cases

- Tier-1 KYC / sanctions / PEP screening on Strait-of-Malacca shipping operators, charterers, and beneficial owners.
- Adverse-media monitoring on key entities and individuals.
- Enforcement-action lookups (FCA, OFAC, EU, MAS).
- Zero Footprint Screening API for one-off transaction or payment screening — useful for marine-finance / trade-finance flows.
- Batch screening for periodic sweeps of large counterparty lists.

## Pricing

- **Free tier:** None.
- **Paid tiers:** None publicly listed.
- **Enterprise:** Custom-quoted by LSEG sales. Pricing scales with seat count, data scope, and API call volume. Generally Tier-1 enterprise pricing.
- **Notes:** Often bundled with other LSEG Risk Intelligence products (Due Diligence Reports, Vessel Sanctions screening, etc.).

## Authentication

API key / OAuth 2.0 token issued post-contract. Customer-tenanted environment.

## Endpoints

- **Login portal:** `https://worldcheck.refinitiv.com/`
- **Public product page:** `https://www.lseg.com/en/risk-intelligence/screening-solutions/world-check-kyc-screening`
- **API base URL:** Customer-issued.
- **Surface areas:**
  - World-Check One screening API
  - Zero Footprint Screening API (transaction-level)
  - Batch Screening (file-based)
  - Adverse Media + Enforcement Action endpoints

## Example call

```bash
# Illustrative — actual endpoints provisioned per LSEG World-Check One contract.
curl -H "Authorization: Bearer $WORLDCHECK_TOKEN" \
  "https://api.lseg.com/world-check-one/v2/cases/screeningRequest" \
  -X POST -H "Content-Type: application/json" \
  -d '{"name":"PT Pelayaran Tempuran Emas","entityType":"ORGANISATION","providerTypes":["WATCHLIST","ADVERSE_MEDIA"]}'
```

## Rate limits

Plan-dependent; not publicly documented.

## SDKs / Libraries

- **Official:** Customer-issued integration packages.
- **Community:** None notable (closed customer base).

## Documentation

- Main product page: https://www.lseg.com/en/risk-intelligence/screening-solutions/world-check-kyc-screening
- LSEG developer portal: https://developers.lseg.com/

## Notes

- Branding transition: still commonly referred to as "Refinitiv World-Check" by industry; LSEG completed the Refinitiv acquisition in 2021.
- Most widely-deployed sanctions/PEP feed in the world — tier-1 banks, top-10 freight forwarders, and major marine insurers all use World-Check.
- For maritime-specific sanctions screening, pair with Pole Star PurpleTRAC or Windward to enrich with vessel-tracking context.
