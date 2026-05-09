# Sayari

Commercial intelligence and entity-resolution platform mapping global commerce across 250+ jurisdictions and 1.5B+ entities. Strong fit for ownership-graph traversal, supply-chain risk, sanctions screening, and forced-labor due diligence — useful for identifying state-actor and beneficial-owner risk on Strait-transiting vessels and connected companies.

**Tier:** Enterprise
**Auth:** API Key / OAuth (issued via Sayari onboarding)
**Last researched:** 2026-05-09

## Use cases

- Beneficial-ownership graph traversal on shipping companies, charterers, and managers operating in the Strait of Malacca.
- Supply-chain risk on cargoes (forced labor, sanctioned parties, end-use control) — increasingly required by Western customs regimes.
- Hidden-risk discovery — Sayari claims 72% of risk it discovers is not on global sanctions watchlists.
- Trade-flow analytics (Sayari Trade) — origin/destination patterns of cargoes and counterparts.
- AI agentic workflows over the commercial graph — explainable outputs with calibrated uncertainty.

## Pricing

- **Free tier:** None.
- **Paid tiers:** None publicly listed.
- **Enterprise:** Custom-quoted by Sayari sales. Pricing scales with seats, query volume, and dataset breadth.
- **Notes:** Customers include Fortune 500 (HSBC, BP, Tesla, Microsoft) and U.S. government agencies. Procurement is sales-led; expect a multi-week cycle.

## Authentication

API key / OAuth 2.0 token issued during Sayari onboarding. Tenant-scoped.

## Endpoints

- **Public site:** `https://sayari.com/`
- **API base URL:** Customer-issued.
- **Surface areas:**
  - Sayari Graph — entity resolution + ownership traversal
  - Sayari Trade — trade-flow analytics
  - Risk endpoints — sanctions, PEP, forced labor, export-control
  - Superconductor — quality-evaluation infrastructure for AI deployments

## Example call

```bash
# Illustrative — actual endpoints are tenant-scoped.
curl -H "Authorization: Bearer $SAYARI_TOKEN" \
  "https://api.sayari.com/v1/entity/search?q=PT%20Pelayaran%20Tempuran&country=IDN"
```

## Rate limits

Not publicly documented; defined per contract.

## SDKs / Libraries

- **Official:** Customer-issued packages.
- **Community:** None notable (closed customer base).

## Documentation

- Main site: https://sayari.com/
- Developer login: https://sayari.com/login

## Notes

- Backed by TPG, Centana Growth Partners, and In-Q-Tel — In-Q-Tel ties signal U.S. intelligence-community alignment.
- Strongest fit when the use case requires explainability — Sayari's outputs link back to underlying source documents (registry filings, customs records, news).
- For Strait of Malacca: useful for screening Indonesian/Malaysian/Singaporean charterers and beneficial-owner chains; particularly strong on Indonesian corporate registry data.
