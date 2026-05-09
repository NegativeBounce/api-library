# IMB Piracy Reporting Centre

The International Maritime Bureau (ICC-CCS) Piracy Reporting Centre runs a 24/7 global watch on shipping lanes, publishes a live world map of incidents, and issues quarterly and annual piracy reports. Authoritative complement to ReCAAP for the Strait of Malacca and globally.

**Tier:** Paid (full reports); Free (live map + summaries)
**Auth:** None for public map; subscription for full reports
**Last researched:** 2026-05-09

## Use cases

- Global piracy incident map covering Strait of Malacca and adjacent waters (Sumatra east coast, Singapore Strait, South China Sea).
- Quarterly and annual IMB Piracy & Armed Robbery Against Ships reports — most-cited industry numbers alongside ReCAAP.
- Direct 24/7 reporting hotline for masters whose vessels have been attacked.
- Industry warnings on emerging hotspots and modus operandi.
- Cross-validation of ReCAAP figures (IMB and ReCAAP sometimes differ in classification — important for analysts).

## Pricing

- **Free tier:** Live piracy map (https://icc-ccs.org/map/) and PDF summaries.
- **Paid tiers:** Full piracy reports and bespoke piracy reports (request via the IMB site). Pricing not publicly listed.
- **Enterprise:** Industry membership of the ICC Commercial Crime Services unlocks access to full incident details, watchlists, and analysis.
- **Notes:** Reports are predominantly distributed as PDFs; structured data feeds are not part of the standard offering.

## Authentication

No authentication for the live map. Report requests are individually fulfilled via email after a `Request Piracy Report` form submission.

## Endpoints

- **Live map:** `https://icc-ccs.org/map/`
- **Reports:** `https://www.icc-ccs.org/wp-content/uploads/<year>/<...>.pdf` (quarterly / annual)
- **Request piracy report:** https://icc-ccs.org/request-piracy-report/
- **No documented JSON / REST API.** Live map pulls incidents from an internal endpoint that is not officially supported for third-party use.

## Example call

```bash
# Latest quarterly report (PDF)
curl -O "https://www.icc-ccs.org/wp-content/uploads/2026/04/2026-Jan-Mar-IMB-Piracy-and-Armed-Robbery-Report.pdf"
```

## Rate limits

Not published.

## SDKs / Libraries

- **Official:** None.
- **Community:** None notable.

## Documentation

- IMB-PRC overview: https://icc-ccs.org/imb-piracy-reporting-centre-2/
- Live map: https://icc-ccs.org/map/
- ICC-CCS landing: https://icc-ccs.org/

## Notes

- IMB and ReCAAP definitions of piracy vs. armed robbery sometimes diverge — IMB tends to record more CAT-3/CAT-4 type incidents that ReCAAP categorizes as petty theft. Use both for a fuller picture.
- For machine consumption, plan to parse the quarterly PDF or carefully scrape the live map. No officially supported feed.
- Useful contact: ccs@icc-ccs.org / +44 (0)20 7423 6960. Reporting hotline: +60 3 2078 5763 (Kuala Lumpur).
