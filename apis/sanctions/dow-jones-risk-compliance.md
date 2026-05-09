# Dow Jones Risk & Compliance

Editorially-curated PEP, sanctions, adverse-media, state-owned enterprise, and watchlist data, sourced via Dow Jones research bench and Factiva publications. Major rival to LSEG World-Check at the Tier-1 enterprise compliance level. API delivery available.

**Tier:** Enterprise
**Auth:** API Key (Bearer)
**Last researched:** 2026-05-09

## Use cases

- Tier-1 enterprise sanctions / PEP / adverse-media screening on Strait-of-Malacca counterparties.
- Editorially-verified PEP and Relatives & Close Associates (RCA) data — useful for ownership-traversal investigations.
- Adverse-media research drawing from Factiva's licensed publications (high-quality sources).
- Sanctioned-instruments screening for marine-finance flows.
- Taxonomy API to extract codes for searching specific countries, regions, PEP categories, sanctions lists.
- Integration with adjacent Dow Jones products (Dragonfly Intelligence, Oxford Analytica, Factiva).

## Pricing

- **Free tier:** None.
- **Paid tiers:** None publicly listed.
- **Enterprise:** Custom-quoted by Dow Jones sales. Platform fees historically range $10K–$100K+/year plus per-search/record fees.
- **Notes:** Tier-1 pricing comparable to LSEG World-Check; expect months-long procurement.

## Authentication

API key (Bearer token) issued via Dow Jones Developer Platform after contract.

## Endpoints

- **Developer platform:** `https://developer.dowjones.com/`
- **Risk & Compliance API docs:** `https://dowjones.developerprogram.org/site/docs/risk_and_compliance_apis/`
- **Surface areas:**
  - Search API — multi-list screening
  - Taxonomy API — code lookups for filters
  - Watchlists / Sanctions / PEP / Adverse Media endpoints
  - Optimised feeds for payment screening and sanctioned-instruments screening

## Example call

```bash
# Illustrative — actual endpoints provisioned per Dow Jones contract.
curl -H "Authorization: Bearer $DOWJONES_TOKEN" \
  "https://api.dowjones.com/risk-and-compliance/v3/screening/search" \
  -X POST -H "Content-Type: application/json" \
  -d '{"name":"PT Pelayaran Tempuran Emas","contentSet":["SANCTIONS","PEPS","ADVERSE_MEDIA"]}'
```

## Rate limits

Plan-dependent; not publicly documented.

## SDKs / Libraries

- **Official:** None broadly distributed; integration partner ecosystem (AEB, KYC360, RiskScreen, DAIS).
- **Community:** None notable.

## Documentation

- Main site: https://www.dowjones.com/professional/risk/
- Developer platform: https://developer.dowjones.com/
- Legacy R&C API docs: https://dowjones.developerprogram.org/site/docs/risk_and_compliance_apis/

## Notes

- Now sits alongside Dragonfly Intelligence (acquired 2025) under Dow Jones Risk & Compliance — combined entity / risk / geopolitical bundle is a meaningful differentiator.
- Editorial bench is a quality differentiator vs. open data; fewer false positives but higher cost.
- Often selected when an organisation already uses Factiva — leverages the same Dow Jones publication relationships.
