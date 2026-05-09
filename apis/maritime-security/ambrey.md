# Ambrey

UK-based maritime security firm offering risk analytics (Guardian platform), 24/7 Global Operations Centre overwatch, voyage and port risk assessments, and embarked maritime security personnel. Strong delivery in armed transits, but cataloged here for the data/analytics side.

**Tier:** Enterprise
**Auth:** Login (Guardian platform); not a public API
**Last researched:** 2026-05-09

## Use cases

- Pre-voyage risk assessments for Strait of Malacca transits — Ambrey's Voyage Risk Assessment, Port Risk Assessment, and Regional Risk Assessment products.
- Live monitoring via Guardian Watchkeeper (web + mobile) and Sentinel & ECDIS overlays.
- 24/7 escalation channel via Ambrey's Global Operations Centre — human eyes on watch.
- Advanced Screening Assessments — vetting cargoes, charters, or ports against sanctions/PEP/risk lists.
- Embarked security teams (PMSC) for armed transits in adjacent regions (Indian Ocean HRA, Gulf of Guinea) — operationally relevant if your route extends beyond the Strait.

## Pricing

- **Free tier:** None.
- **Paid tiers:** None publicly listed.
- **Enterprise:** Custom-quoted by Ambrey sales. Bundles vary widely (intel-only seat, GOC overwatch, full-service PMSC).
- **Notes:** Ambrey operates as a high-touch service provider — expect longer onboarding than self-service tools.

## Authentication

Customer login to the Guardian platform after subscription. No public API documented.

## Endpoints

- **Guardian platform:** Customer-issued login portal.
- **Public website:** `https://www.ambrey.com/`
- **No documented REST API.** Integrations (e.g., feeding Guardian alerts into a customer SIEM) are bespoke.

## Example call

```bash
# Not applicable — Ambrey delivers via portal, PDF reports, and 24/7 GOC voice/email channel.
# Contact enquiries@ambrey.com or +44 (0)20 3503 0320 to arrange a demo.
```

## Rate limits

Not applicable / not published.

## SDKs / Libraries

- **Official:** None.
- **Community:** None.

## Documentation

- Main site: https://www.ambrey.com/

## Notes

- Best in class for **operational** maritime security (embarked teams, GOC watchkeeping). Less suited as a data feed than Dryad or Risk Intelligence.
- Catalog Ambrey when the use case is "we need analyst-vetted advice and 24/7 escalation," not "we need a webhook of incidents."
- Often appears alongside Solace Global, Diaplous, and EOS Risk in PMSC RFPs.
