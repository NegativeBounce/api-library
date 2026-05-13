# IUMI Statistics (International Union of Marine Insurance)

Annual statistical reports and data publications from the International Union of Marine Insurance covering global marine insurance premiums, major claims, hull and cargo loss trends, and the Hull Inflation Index — the authoritative industry dataset for marine underwriting performance.

**Tier:** Free (public reports)
**Auth:** None
**Last researched:** 2026-05-13

## Use cases

- Analyzing global marine insurance premium volumes by line of business (hull, cargo, offshore, liability)
- Researching major claims frequency and severity trends for hull and cargo insurance classes
- Using the IUMI Hull Inflation Index to adjust historical hull values for inflation in actuarial models

## Pricing

- **Free tier:** Annual Stats Report PDF freely downloadable; selected datasets published publicly
- **Paid tiers:** None for public publications
- **Enterprise:** N/A — IUMI is a trade association; full underlying data is member-only
- **Notes:** Underlying granular data is available only to IUMI member associations; the public Stats Report contains aggregated global totals.

## Authentication

No authentication required for public PDF downloads and published statistics.

## Endpoints

- **Statistics page:** `https://iumi.com/statistics/` — hub for all published statistical datasets and reports
- **Stats Report 2025 PDF:** `https://iumi.com/wp-content/uploads/2025/11/IUMI-Stats-Report-2025.pdf`
- **Access method:** PDF download; no REST API

**No public REST API exists.** Data is published as annual PDF reports and selected Excel datasets.

## Example call

```bash
# Download the 2025 Stats Report
curl -L -o iumi-stats-report-2025.pdf \
  "https://iumi.com/wp-content/uploads/2025/11/IUMI-Stats-Report-2025.pdf"
```

```python
import requests

resp = requests.get(
    "https://iumi.com/wp-content/uploads/2025/11/IUMI-Stats-Report-2025.pdf",
    headers={"User-Agent": "Mozilla/5.0"},
)
with open("iumi-stats-report-2025.pdf", "wb") as f:
    f.write(resp.content)

# Extract tables with pdfplumber
import pdfplumber
with pdfplumber.open("iumi-stats-report-2025.pdf") as pdf:
    for page in pdf.pages:
        tables = page.extract_tables()
        for table in tables:
            print(table)
```

## Rate limits

No API — PDF download only. No rate limits.

## SDKs / Libraries

- **Official:** None
- **Community:** pdfplumber or tabula-py (Python) for PDF table extraction

## Documentation

- IUMI statistics hub: https://iumi.com/statistics/
- Stats Report 2025: https://iumi.com/wp-content/uploads/2025/11/IUMI-Stats-Report-2025.pdf
- About IUMI: https://iumi.com/about/

## Notes

- The 2025 Stats Report (published November 2025) covers 2024 data: global marine insurance premiums of USD 39.92 billion.
- Key datasets published: total premiums by line (ocean hull, cargo, offshore, liability), Major Claims Database, Hull Inflation Index, geographic premium distribution.
- The IUMI Major Claims Database tracks individual losses above USD 500,000 (threshold varies by edition); it is the most comprehensive public dataset of large marine losses.
- The Hull Inflation Index adjusts hull values for inflation using vessel newbuild price indices — essential for accurate long-term loss ratio analysis.
- Premium data is collected from IUMI member associations covering 40+ countries; emerging markets may be underrepresented.
- For loss frequency and severity by vessel type, pair with Allianz Safety and Shipping Review (`allianz-safety-shipping-review.md`) and EMSA EMCIP (`emsa-emcip.md`).
- IUMI annual conference presentations (September each year) release preliminary statistics before the full report; slides are also published on the statistics page.
