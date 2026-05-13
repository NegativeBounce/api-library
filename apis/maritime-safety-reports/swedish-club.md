# Swedish Club Loss Prevention

Loss prevention publications, claims statistics, and safety insights from The Swedish Club, a mutual marine insurer providing P&I and H&M (Hull and Machinery) coverage — publishing annual H&M and P&I claims analyses by vessel type, accident cause, and trade area.

**Tier:** Free (public content); Member portal (SCOL) for policyholders
**Auth:** None (public publications)
**Last researched:** 2026-05-13

## Use cases

- Analyzing H&M and P&I claims distributions by vessel type and accident cause from an insurer perspective
- Accessing loss prevention guidance and case studies for shipowners, managers, and seafarers
- Researching annual claims trends across machinery damage, grounding, collision, and cargo categories

## Pricing

- **Free tier:** Annual report and loss prevention publications freely available; no registration required
- **Paid tiers:** None for public content
- **Enterprise:** SCOL member portal (policyholder access) provides certificates, claims, and policy management services; requires Swedish Club membership
- **Notes:** The Swedish Club is a mutual insurer — membership is required for policy services, but all public loss prevention content is freely accessible.

## Authentication

No authentication required for public publications and annual reports. The SCOL member portal requires Swedish Club policyholder credentials.

## Endpoints

- **Annual report:** `https://www.swedishclub.com/annual-report/` — current and prior-year annual reports with H&M and P&I claims statistics
- **Loss prevention:** `https://www.swedishclub.com/loss-prevention/` — guidance documents, safety circulars, and case studies
- **Access method:** Web browsing and PDF download; no REST API or RSS feed

**No programmatic API exists.** Content is delivered as HTML pages and downloadable PDF reports.

## Example call

```bash
# Fetch annual report landing page to locate PDF download links
curl -s "https://www.swedishclub.com/annual-report/" -H "User-Agent: Mozilla/5.0"
```

```python
import requests
from bs4 import BeautifulSoup

resp = requests.get(
    "https://www.swedishclub.com/annual-report/",
    headers={"User-Agent": "Mozilla/5.0"},
)
soup = BeautifulSoup(resp.text, "html.parser")
pdf_links = [a["href"] for a in soup.find_all("a", href=True) if ".pdf" in a["href"]]
for link in pdf_links:
    print(link)
```

## Rate limits

No API — web scraping only. No published rate limits; apply respectful crawl delays.

## SDKs / Libraries

- **Official:** None
- **Community:** None — use pdfplumber or PyMuPDF for PDF table extraction from annual reports

## Documentation

- Annual report: https://www.swedishclub.com/annual-report/
- Loss prevention: https://www.swedishclub.com/loss-prevention/
- About The Swedish Club: https://www.swedishclub.com/about-us/

## Notes

- The Swedish Club annual report includes detailed H&M claims data broken down by: vessel type (tanker, bulker, container, ro-ro, general cargo, etc.), accident cause (machinery damage, grounding, fire, collision, contact), and claim size distribution.
- P&I section covers: personal injury, collision liability, cargo, pollution, and wreck removal claims.
- Claims data is presented as frequency and severity metrics — useful for actuarial benchmarking and risk modeling.
- The Swedish Club is one of the 13 members of the International Group of P&I Clubs; their claims data reflects a significant sample of the world fleet.
- For complementary insurer-perspective data, pair with Gard Loss Prevention (`gard-loss-prevention.md`) and IUMI Statistics (`iumi-statistics.md`).
- Loss prevention publications focus on practical operational guidance: machinery maintenance, watchkeeping, cargo securing, enclosed space entry, and crew welfare.
- The SCOL member portal provides real-time certificate and claims access — not relevant for public data extraction.
