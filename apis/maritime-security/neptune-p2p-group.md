# Neptune P2P Group

International private security company (est. 2009) providing intelligence-led maritime security, vessel protection, and a security-intelligence portal with interactive risk maps and incident dashboards.

**Tier:** Freemium
**Auth:** Account (portal / newsletter)
**Last researched:** 2026-06-11

> **Advisory + portal service, not a self-serve data API.** Free reports and a subscription intelligence portal; bespoke products per contract.

## Use cases

- Monitoring maritime security incidents worldwide via free monthly Maritime Intelligence Reports and incident-report subscriptions.
- Interactive global risk maps and tracker dashboards (Security Intelligence portal) for situational awareness across maritime and land domains.
- Bespoke geographic/thematic intelligence reports (region, country, crime, terrorism, migration, narcotics) on request.
- Vessel protection / SEV planning support in high-risk EEZs (e.g. recent Gabonese EEZ armed-support operation via Gabon Maritime Security).

## Pricing

- **Free tier:** Free newsletter, incident reports, and routine maritime/land/spotlight intelligence reports.
- **Paid tiers:** Security Intelligence portal subscription (real-time intel, risk maps, dashboards) — not publicly priced.
- **Enterprise:** Bespoke reporting, vessel protection, consultancy, training — contact provider.
- **Notes:** Founded/led by former British special-unit personnel; ~97 staff (2026).

## Authentication

Account/portal login for the Security Intelligence portal; newsletter signup for free reports. No documented public self-serve API.

## Endpoints

- **Base URL:** No public API. Web portal + reports (see neptunep2pgroup.com).
- **Key surfaces:**
  - Security Intelligence portal — risk maps, tracker dashboards, conflict/global-threat reporting.
  - Free intelligence reports (maritime, land, spotlight).
  - Bespoke analyst reporting on request.

## Example call

```bash
# No public self-serve API. Free reports via newsletter; portal access by subscription.
#   https://neptunep2pgroup.com/news-and-intelligence-reports/
```

## Rate limits

N/A (portal/reports). Per contract if a feed is provisioned.

## SDKs / Libraries

- **Official:** None.
- **Community:** None.

## Documentation

- Main docs: https://neptunep2pgroup.com/
- Reports: https://neptunep2pgroup.com/news-and-intelligence-reports/

## Notes

- The **free monthly maritime incident reports** are a low-cost data input for situational context; the paid portal adds interactive maps/dashboards.
- Like EOS Risk and MAST, value is analyst-led intelligence + protective services, not a programmatic feed.
- Cross-reference: complements official reporting (`maritime-security/ukmto.md`, `maritime-security/recaap-isc.md`) and the IMB Piracy Reporting Centre (`maritime-security/imb-piracy-reporting-centre.md`).
- Confirm whether portal data is exportable/integrable before relying on it programmatically.
