# Verisk Maplecroft

Global risk intelligence and indices provider (Verisk subsidiary) covering 198 countries across 190+ risk indices: political, economic, climate, environmental, ESG, supply-chain, and human rights. API + dashboards + GIS delivery options.

**Tier:** Enterprise
**Auth:** API Key (issued per contract)
**Last researched:** 2026-05-09

## Use cases

- Country risk indices for Indonesia, Malaysia, Singapore, Thailand — quantified, comparable, time-series-able.
- Climate-risk indices for the Strait region (sea-level rise, typhoon exposure, infrastructure resilience).
- Supply-chain and ESG due-diligence layered on vessel ownership / charterer / cargo origin.
- Catastrophe modelling and underwriting (Verisk core capability) — useful for marine insurers.
- GIS overlays on a base map (GRiD platform) for analyst workflows.

## Pricing

- **Free tier:** None.
- **Paid tiers:** None publicly listed.
- **Enterprise:** Custom-quoted. Pricing scales with index selection, geographies, and seats.
- **Notes:** Multinational customer base (Airbus, JPMorgan, Shell, L'Oréal, BlackRock) implies enterprise-grade pricing.

## Authentication

API key issued during Maplecroft onboarding; sometimes integrated via customer SSO.

## Endpoints

- **Public site:** `https://www.maplecroft.com/`
- **API base URL:** Customer-issued.
- **Delivery options:**
  - REST API
  - GRiD interactive dashboards
  - BI-tool connectors (Power BI, Tableau)
  - GIS mapping (Esri integration)
- **Surface areas:**
  - Country risk indices (190+)
  - Industry-specific risk
  - Commodity risk
  - Human rights / ESG datasets

## Example call

```bash
# Illustrative — actual endpoints provisioned per Maplecroft contract.
curl -H "x-api-key: $MAPLECROFT_KEY" \
  "https://api.maplecroft.com/v2/indices?index=political-risk&country=IDN,MYS,SGP,THA"
```

## Rate limits

Not publicly documented.

## SDKs / Libraries

- **Official:** Connectors for Power BI, Tableau, Esri.
- **Community:** None notable.

## Documentation

- Main site: https://www.maplecroft.com/

## Notes

- Indices model is the differentiator — quantified, comparable, time-series scoring of country and sub-national risk.
- For Strait-of-Malacca specifically, country-level indices are insufficient on their own; layer Maplecroft against ACLED / RANE / news for incident-level granularity.
- ESG / human-rights datasets are best-in-class — relevant for charterers and cargo-owners with disclosure obligations.
