# Dragonfly Intelligence

Geopolitical and security intelligence platform (now part of Dow Jones Risk & Compliance after 2025 acquisition). Provides Security Intelligence and Analysis Service (SIAS) — country/city risk reports, travel-risk advisories, threat alerts, and an integrable API ("SIAS API").

**Tier:** Enterprise
**Auth:** API Key (per contract)
**Last researched:** 2026-05-09

## Use cases

- Country and city-level risk reports for Indonesia, Malaysia, Singapore, Thailand — used by corporate security and travel-risk-management teams.
- Travel-risk advisories for crew rotations, port calls, and analyst travel.
- SIAS threat alerts integrated into ops dashboards via the SIAS API.
- Integration with Oxford Analytica (also a Dow Jones property) — complementary geopolitical analyst content.
- Geospatial overlay of asset locations against Dragonfly's risk surfaces.

## Pricing

- **Free tier:** Trial requestable via app.dragonflyintelligence.com.
- **Paid tiers:** None publicly listed.
- **Enterprise:** Custom-quoted via Dow Jones Risk & Compliance. Dow Jones platform fees historically range $10K–$100K+ annually plus per-search/record fees.
- **Notes:** Acquired by Dow Jones for $40M in 2025; pricing/distribution may continue to evolve under Dow Jones.

## Authentication

API key (or OAuth) issued by Dragonfly / Dow Jones during onboarding.

## Endpoints

- **Public site:** `https://dragonflyintelligence.com/`
- **App login:** `https://app.dragonflyintelligence.com/login`
- **SIAS API page:** `https://dragonflyintelligence.com/intelligence/application-programming-interface/`
- **Surface areas:**
  - Country / city risk reports
  - Travel risk
  - Threat alerts
  - Geospatial / asset-overlay APIs

## Example call

```bash
# Illustrative — actual endpoints provisioned per Dragonfly / Dow Jones contract.
curl -H "Authorization: Bearer $DRAGONFLY_TOKEN" \
  "https://api.dragonflyintelligence.com/v1/sias/alerts?country=ID,MY,SG&since=2026-05-01"
```

## Rate limits

Not publicly documented.

## SDKs / Libraries

- **Official:** None broadly distributed; integrations are bespoke.
- **Community:** None notable.

## Documentation

- Main site: https://dragonflyintelligence.com/
- Dow Jones product page: https://www.dowjones.com/djdragonflyintelligence/

## Notes

- Stronger on **narrative geopolitical analysis** than structured event data — pair with ACLED/GDELT for incident granularity.
- Integration into Dow Jones Risk & Compliance unlocks adjacencies: Factiva news, Dow Jones sanctions/PEP data, Oxford Analytica.
- Often listed alongside RANE, Verisk Maplecroft, and Control Risks in enterprise risk-intelligence RFPs.
