# UKMTO (United Kingdom Maritime Trade Operations)

The primary emergency point of contact and voluntary reporting authority for merchant shipping in the Middle East / Indian Ocean region, issuing verified maritime security alerts and advisories.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-06-11

> **Government reporting/advisory service, not a programmatic API.** Alerts, advisories, and a weekly report are published via the UKMTO website and direct ship contact; there is no public REST/JSON feed.

## Use cases

- Authoritative, verified security alerts and advisories for the Voluntary Reporting Area (VRA) — Red Sea, Gulf of Aden, Indian Ocean, Arabian Sea, Strait of Hormuz.
- Primary 24/7 emergency point of contact for vessels encountering incidents in the region.
- Weekly summary reports of regional maritime security activity for situational awareness.
- Reference geography via UKHO Maritime Security Chart Q6099 (defines the VRA).
- Gulf of Guinea coverage via partnership with the French MICA Centre (see MDAT-GoG).

## Pricing

- **Free tier:** Free. Public alerts/advisories and weekly reports; voluntary reporting is free to participating vessels.
- **Paid tiers:** None.
- **Enterprise:** N/A (government service).
- **Notes:** Operates the Voluntary Reporting Scheme (VRS); ~30,000 ship transits reported per year. Part of the Single Information Framework (SIF) with regional partners.

## Authentication

None for public alerts. Vessels participate in the VRS by submitting position reports (initial/daily/final) directly to UKMTO; emergency contact by phone/email.

## Endpoints

- **Base URL:** No API. Primary sources:
  - Website + alerts: `https://www.ukmto.org/`
  - Emergency contact: +44 (0) 2392 222060 / watchkeepers@ukmto.org
- **Key surfaces:**
  - Security alerts / warnings (incident-driven).
  - Advisories (regional sightings/reports).
  - Weekly summary report.
  - Maritime Security Chart Q6099 (VRA geography).

## Example call

```bash
# No API. Monitor alerts at https://www.ukmto.org/ ; vessels report via the VRS.
# Incident reporting is by phone/email, not a programmatic endpoint.
```

## Rate limits

N/A (website / direct contact).

## SDKs / Libraries

- **Official:** None.
- **Community:** None (some third parties scrape/republish alerts — verify against the source).

## Documentation

- Main site: https://www.ukmto.org/
- About / VRS: https://www.ukmto.org/about-us
- BMP Maritime Security guidance referenced via UKMTO.

## Notes

- The **authoritative regional source** for the Middle East/Indian Ocean theatre — the alerts EOS, Ambrey, Dryad and others routinely cite originate here.
- No machine feed: to operationalize, monitor the site/alerts or consume via a commercial provider that ingests and structures UKMTO output.
- Cross-reference: companion regional centres — MDAT-GoG (`maritime-security/mdat-gog.md`, Gulf of Guinea), ReCAAP ISC (`maritime-security/recaap-isc.md`, Asia), and the Singapore IFC (`maritime-security/ifc-singapore.md`). For navigational (vs. security) warnings see `navigational-warnings/`.
