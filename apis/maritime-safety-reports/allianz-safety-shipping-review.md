# Allianz Safety and Shipping Review

Annual flagship report from Allianz Global Corporate & Specialty (AGCS) analyzing global shipping losses, incidents, and emerging maritime safety trends across vessel types, accident categories, and geographic regions.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-13

## Use cases

- Benchmarking annual shipping loss totals and incident counts against historical trend data
- Researching accident cause distributions (foundering, fire, machinery failure, collision) by vessel type
- Supporting maritime risk models with authoritative annual loss statistics from a major insurer

## Pricing

- **Free tier:** Full report available as a free PDF download; no registration required
- **Paid tiers:** None
- **Enterprise:** N/A
- **Notes:** Report is a public loss-prevention resource; AGCS makes it freely available as part of its thought-leadership and risk-awareness activities.

## Authentication

No authentication required. Download the PDF directly from the AGCS publications page.

## Endpoints

- **Report landing page:** `https://commercial.allianz.com/news-and-insights/reports/shipping-safety.html`
- **Access method:** PDF download (annual); no REST API
- **Supplementary data:** Selected statistics sometimes released as press-release tables alongside the PDF

**No programmatic API exists.** Data must be extracted from the published PDF or from press-release text accompanying the annual release.

## Example call

```bash
# Download the current year's report PDF (URL varies by edition — check landing page)
curl -L -o allianz-shipping-review-2025.pdf \
  "https://commercial.allianz.com/content/dam/onemarketing/agcs/commercial-allianz/reports/Allianz-Safety-Shipping-Review-2025.pdf"
```

```python
import requests

# Fetch landing page to locate current PDF link
resp = requests.get(
    "https://commercial.allianz.com/news-and-insights/reports/shipping-safety.html",
    headers={"User-Agent": "Mozilla/5.0"},
)
# Parse HTML to extract PDF download URL — link text typically "Download report"
```

## Rate limits

No API — PDF download only. No rate limits; standard web server throttling applies.

## SDKs / Libraries

- **Official:** None
- **Community:** None — use a PDF extraction library (pdfplumber, PyMuPDF) to parse tabular data from the report

## Documentation

- Report landing page: https://commercial.allianz.com/news-and-insights/reports/shipping-safety.html
- AGCS media contacts for data enquiries: https://commercial.allianz.com/news-and-insights/press-releases.html

## Notes

- The 2025 report (covering 2024 data) recorded 27 total losses — the lowest in the dataset's history — and 3,310 incidents; published approximately May 2025.
- Report covers losses of vessels over 100 GT; total loss definition follows standard marine insurance conventions.
- Historical trend data extends back to 2014 in the current series; prior-year PDFs remain available at the landing page.
- Key accident categories tracked: foundering/sinking, fire/explosion, machinery damage, collision, contact, wrecked/stranded, missing.
- Geographic hotspots, vessel type breakdowns, and emerging risk sections (cyber, autonomous vessels, alternative fuels) are updated annually.
- For programmatic access to historical statistics, pair with IUMI (`iumi-statistics.md`) and EMSA EMCIP (`emsa-emcip.md`) data sources.
