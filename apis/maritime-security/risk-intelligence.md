# Risk Intelligence (RIS)

Danish maritime / security intelligence firm operating the Risk Intelligence System (RIS), a 24/7 portal for incident updates, threat assessments, AIS tracking, and customisable alerts. Subject-matter experts cover piracy, armed conflict, civil unrest, terrorism, and organized crime affecting maritime operations.

**Tier:** Enterprise
**Auth:** Login (subscriber portal); webhooks/API for Enterprise customers
**Last researched:** 2026-05-09

## Use cases

- 24/7 maritime threat intelligence covering the Strait of Malacca, Singapore Strait, and broader Southeast Asia.
- Geofenced incident alerting (e.g., notification when an incident occurs within X nm of your vessel/anchorage).
- AIS-fused vessel tracking with overlays for piracy hotspots, smuggling routes, and political risk zones.
- Pre-voyage and live-voyage risk assessments via the Duty Watch team.
- Historical incident archive for pattern-of-life and underwriter modelling.
- Adjacent coverage: Black Sea, Middle East, West Africa, Latin America — useful for fleets with global routes.

## Pricing

- **Free tier:** None.
- **Paid tiers:** Subscription-based access to the RIS portal; pricing not published.
- **Enterprise:** Custom contracts including alerting webhooks and bulk data exports.
- **Notes:** Pricing scales with seats, geographic scope, and whether webhook/API integration is included.

## Authentication

Subscriber portal login at riskintelligence.eu / RIS portal. Enterprise webhook/API integration uses customer-provisioned credentials (token or API key).

## Endpoints

- **Portal login:** `https://www.riskintelligence.eu/` → subscriber-only access.
- **Public API:** **Not publicly documented.** Enterprise customers receive integration documentation as part of onboarding.
- **Surface areas:**
  - Incident feed (maritime + land-based security relevant to maritime ops)
  - Threat assessments and intel reports
  - Geofence alerting
  - AIS tracking
  - Duty Watch query channel (human analyst access)

## Example call

```bash
# Illustrative — actual endpoint and auth provisioned per customer.
curl -H "Authorization: Bearer $RIS_TOKEN" \
  "https://api.riskintelligence.eu/v1/incidents?region=southeast-asia&since=2026-05-01"
```

## Rate limits

Not publicly documented.

## SDKs / Libraries

- **Official:** None.
- **Community:** None.

## Documentation

- Main site: https://www.riskintelligence.eu/
- Contact: +45 70 26 62 30, https://www.riskintelligence.eu/contact

## Notes

- Strong analyst depth; Risk Intelligence's regional desks (especially Black Sea and Middle East) are well-regarded.
- The Strait of Malacca is covered as part of their Asia-Pacific desk. Confirm coverage scope (incidents, threats, advisories) during sales discussion — some packages exclude lower-tier petty crime.
- 24/7 Duty Watch is differentiating vs. portal-only competitors.
- Often confused with **Verisk Maplecroft** (different company) and **Dragonfly Eye** (different company) — same industry, distinct vendors.
