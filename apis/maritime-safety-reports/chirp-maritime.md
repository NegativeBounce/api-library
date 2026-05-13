# CHIRP Maritime

Confidential Human Factors Incident Reporting Programme — a UK-based independent safety reporting scheme that collects, analyzes, and publishes anonymized maritime incident reports submitted voluntarily by seafarers, covering near-misses, procedural failures, and safety concerns.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-13

## Use cases

- Researching human factors and near-miss incident patterns from anonymized seafarer reports
- Accessing curated incident narratives for safety training case studies and maritime education
- Monitoring quarterly newsletters and annual digests for emerging safety themes across vessel types

## Pricing

- **Free tier:** All publications freely available for download; no registration required
- **Paid tiers:** None
- **Enterprise:** N/A
- **Notes:** CHIRP is a non-profit charitable organization; all content is published as a public safety resource.

## Authentication

No authentication required. All publications are freely downloadable from the CHIRP Maritime website.

## Endpoints

- **Newsletters:** `https://www.chirpmaritime.org/newsletters/` — quarterly Maritime FEEDBACK newsletters (PDF)
- **Annual digests:** `https://www.chirpmaritime.org/digest/` — yearly digest compilations
- **All publications:** `https://www.chirpmaritime.org/publications/` — full publication archive
- **Access method:** PDF download; no REST API or structured data export

**No programmatic API exists.** Content is published as PDF newsletters and digests; use a PDF extraction library to parse incident narratives.

## Example call

```bash
# List available newsletters page
curl -s "https://www.chirpmaritime.org/newsletters/" | grep -oP 'href="[^"]+\.pdf"'
```

```python
import requests
from bs4 import BeautifulSoup

resp = requests.get("https://www.chirpmaritime.org/newsletters/")
soup = BeautifulSoup(resp.text, "html.parser")
pdf_links = [a["href"] for a in soup.find_all("a", href=True) if a["href"].endswith(".pdf")]
for link in pdf_links:
    print(link)
```

## Rate limits

No API — PDF download only. No published rate limits; standard web server throttling applies.

## SDKs / Libraries

- **Official:** None
- **Community:** None — use pdfplumber or PyMuPDF to extract incident narratives from newsletter PDFs

## Documentation

- Newsletters archive: https://www.chirpmaritime.org/newsletters/
- Annual digests: https://www.chirpmaritime.org/digest/
- All publications: https://www.chirpmaritime.org/publications/
- About CHIRP Maritime: https://www.chirpmaritime.org/about/

## Notes

- CHIRP Maritime FEEDBACK is published quarterly; each issue contains 8–15 anonymized incident reports with human factors analysis.
- Reports are submitted voluntarily by seafarers — bias toward deck and engine room incidents; near-misses are particularly well represented.
- The annual digest aggregates all quarterly reports and adds thematic analysis; useful for year-over-year trend comparison.
- CHIRP also operates separate aviation and offshore oil & gas reporting programmes under the same organization.
- Incident categories include: navigation, cargo, engineering, enclosed spaces, lifting operations, mooring, communication failures.
- For machine-readable incident data, pair with IMO GISIS (`imo-gisis.md`) and MAIB reports (`maib.md`), which provide more structured datasets.
- All publications are available in English; selected materials are published in additional languages.
