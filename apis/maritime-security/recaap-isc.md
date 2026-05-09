# ReCAAP ISC

The Regional Cooperation Agreement on Combating Piracy and Armed Robbery against Ships in Asia (ReCAAP) Information Sharing Centre publishes the authoritative incident dataset for piracy and armed robbery in Asia, with deep coverage of the Straits of Malacca and Singapore.

**Tier:** Free
**Auth:** None (public dashboard); incident reporting requires registration
**Last researched:** 2026-05-09

## Use cases

- Authoritative incident reports for piracy and armed robbery against ships in Asia, with the Strait of Malacca and Singapore Strait being the highest-density area (84% of all reported Asian incidents in H1 2025; 107 incidents in 2024).
- Weekly, quarterly, half-yearly, and annual PDF reports tracking trends and modus operandi (boarding methods, items stolen, vessel types).
- Interactive incident search via the Re-VAMP dashboard and OpenMap portal — filter by date, location, ship name, severity (CAT-1 to CAT-4 and "petty theft").
- Email/RSS-style alerts for newly reported incidents (subscribe via the website).
- Reporting incidents directly via the IFN (Information Fusion Network) mobile app — ReCAAP-cleared focal points get immediate dissemination.

## Pricing

- **Free tier:** All published reports, dashboard, and OpenMap are free to access.
- **Paid tiers:** None.
- **Enterprise:** None.
- **Notes:** ReCAAP is a multilateral information-sharing centre, not a commercial vendor. Data is intended for public-benefit use.

## Authentication

No authentication for the public dashboard, OpenMap, or PDF report downloads. Email registration is required for push updates. The IFN mobile app is gated to recognised focal points.

## Endpoints

- **Public dashboard:** `https://dashboard.recaap.org/`
- **OpenMap portal (interactive incident search):** `https://portal.recaap.org/OpenMap`
- **Reports (PDF):** `https://www.recaap.org/reports`
- **No documented JSON / REST API.** The OpenMap portal is a JavaScript app that may have undocumented internal endpoints, but ReCAAP does not publish or support them.

## Example call

```bash
# Download the latest annual report
curl -O "https://www.recaap.org/resources/ck/files/reports/annual/ReCAAP%20ISC%20Annual%20Report%202024%20-%20Final.pdf"
```

## Rate limits

Not published. As a public-information body with low traffic, no aggressive throttling reported, but bulk scraping of OpenMap is discouraged.

## SDKs / Libraries

- **Official:** None.
- **Community:** No widely-used wrappers; some research projects scrape the OpenMap portal.

## Documentation

- Main site: https://www.recaap.org/
- Dashboard: https://dashboard.recaap.org/
- OpenMap: https://portal.recaap.org/OpenMap

## Notes

- For the Strait of Malacca specifically, ReCAAP is the **single most authoritative source** — the centre is co-located in Singapore and has direct focal-point relationships with the littoral states.
- Lack of an API is the major operational gap. For automated pipelines, plan to either (a) parse the periodic PDFs, (b) carefully scrape OpenMap, or (c) layer on a commercial provider (Dryad, IMB) that ingests ReCAAP data.
- Categorisation scheme (CAT-1 through CAT-4 + petty theft) is consistent across reports — useful for severity-weighted risk scoring.
- Email contact for technical inquiries: info@recaap.org. Phone +65 6376 3063.
