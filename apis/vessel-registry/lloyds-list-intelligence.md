# Lloyd's List Intelligence API

Modular maritime intelligence APIs from the 1734-founded authority, combining vessel ownership, characteristics, risk, sanctions, cargo, emissions and geospatial data.

**Tier:** Enterprise
**Auth:** API Key / OAuth
**Last researched:** 2026-06-11

## Use cases

- Revealing hidden/beneficial ownership and company structures for sanctions and compliance investigations.
- Screening vessels, owners, cargo and behaviour with integrated risk indicators (a core insurance/war-risk workflow).
- Enriching reports with vessel characteristics, ports/terminals, inspections, casualties and emissions in one data partner.
- Building a scalable maritime platform on validated AIS (SeaOrbis) plus ownership and risk modules.

## Pricing

- **Free tier:** None.
- **Paid tiers:** Subscription/contract; modular by endpoint set.
- **Enterprise:** Contact sales; dedicated technical onboarding, field mapping, migration support.
- **Notes:** Pricing not public. Owned by Montagu Private Equity (acquired from Informa, 2022). Products include Seasearcher and AIS SeaOrbis.

## Authentication

API key / OAuth per contract. Modular endpoints; credentials and schema provided during technical onboarding.

## Endpoints

- **Base URL:** Provided on contract (see lloydslistintelligence.com/solutions/api).
- **Key endpoints (modular):**
  - Vessel & Ownership — characteristics, ownership structures, company links.
  - Risk & Compliance — sanctions screening, behavioural risk, casualties, inspections.
  - Movements — AIS positions, port calls, ETAs, voyage intelligence (SeaOrbis).
  - Cargo & Trade — cargo risk, trade flows, bill-of-lading validation.
  - Geospatial — ports, terminals, berths, routing context.
  - News — real-time Lloyd's List news via API.

## Example call

```bash
# Illustrative; endpoints/auth provided during onboarding
curl -H "Authorization: Bearer $LLI_TOKEN" \
  "https://api.lloydslistintelligence.com/vessels/9811000/ownership"
```

## Rate limits

Per contract; not publicly published.

## SDKs / Libraries

- **Official:** Documentation, sample responses, schema guidance provided; no public language SDK.
- **Community:** None notable.

## Documentation

- Main docs: https://www.lloydslistintelligence.com/solutions/api
- API reference: Provided on contract (with sample data for pre-production validation).

## Notes

- Among the most authoritative ownership/risk sources; data validated by 80+ analysts and the Lloyd's Agents network.
- SmartMatch resolves duplicate/erroneous identities from registry changes and flags AIS spoofing — valuable for deception detection in war-risk reporting.
- Best-fit for the compliance/sanctions and insurance personas where defensibility of ownership data matters; enterprise cost and onboarding required.
