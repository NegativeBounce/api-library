# Janes

Defense and security intelligence publisher (Jane's Information Group, est. 1898) offering structured datasets on military capabilities, country risk, terrorism, equipment, sensors, weapons, defense budgets, and geoeconomic threats. Data-as-a-Service available via API and bulk delivery.

**Tier:** Enterprise
**Auth:** API Key / OAuth (issued per contract)
**Last researched:** 2026-05-09

## Use cases

- Country risk intelligence on Indonesia, Malaysia, Singapore, Thailand — politics, military, economics, society, information, infrastructure (PMESII-style).
- Stability indicators and flashpoint identification — useful for predicting unrest near key Strait ports and chokepoints.
- Military / naval capability tracking — especially relevant for the Strait given proximity to Indonesian, Malaysian, and Singaporean naval forces, plus regular U.S. and Chinese naval transits.
- Equipment / sensors / weapons reference data for analyst workflows (Janes is the standard reference for naval and defense equipment).
- Geoeconomic threat data — sanctions, trade choke points, supply-chain risk — relevant for Strait-traffic stakeholders.
- Knowledge graph delivery for AI-driven defense/security workflows.

## Pricing

- **Free tier:** None (some marketing-page articles are free to read).
- **Paid tiers:** None publicly listed.
- **Enterprise:** Custom-quoted; data delivery via API, File GeoDB, Parquet, RDBMS, XML, or Label/Property Graph.
- **Notes:** Pricing typically scoped to specific datasets (Country Profiles, Terrorism, Military Capabilities) and seats. Government and defense-prime contracts dominate.

## Authentication

API key / OAuth 2.0 token issued via Janes' onboarding. Sometimes integrated through customer SSO.

## Endpoints

- **Public website:** `https://www.janes.com/`
- **API base URL:** Customer-issued.
- **Datasets (delivered via API or bulk):**
  - Knowledge graph (interconnected entities)
  - Country profiles & CBRN profiles
  - Terrorism intelligence
  - Military capabilities, equipment, sensors, weapons
  - Defense budgets, programmes, forecasts
  - Geoeconomic threat & influence
  - News, events, analysis

## Example call

```bash
# Illustrative — actual endpoint provisioned per Janes contract.
curl -H "Authorization: Bearer $JANES_TOKEN" \
  "https://api.janes.com/v1/country/intelligence?country=Indonesia"
```

## Rate limits

Not publicly documented.

## SDKs / Libraries

- **Official:** Customer-issued integration packages.
- **Community:** None (closed customer base).

## Documentation

- Main site: https://www.janes.com/
- Datasets overview: https://www.janes.com/defence-intelligence-datasets
- Integration: https://www.janes.com/intara-interconnected-intelligence/existing-system-integration

## Notes

- Janes is the gold standard for **defense-grade** intelligence — most western military and intelligence agencies, plus prime contractors, are customers.
- For Strait of Malacca specifically: Janes' country files on Indonesia and Malaysia plus its naval-capability data are the most authoritative references for state-actor risk.
- Long procurement cycle (months); often requires security clearance for sensitive datasets.
