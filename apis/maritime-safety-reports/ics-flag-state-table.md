# ICS Flag State Performance Table

Annual ranking of maritime flag states published by the International Chamber of Shipping (ICS), scoring each flag against 19 criteria including ratification of international conventions, Port State Control detention rates, and casualty statistics.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-13

## Use cases

- Evaluating flag state compliance and safety performance for vessel vetting and due diligence workflows
- Comparing flag states on Port State Control detention rates, IMO convention ratification, and audit status
- Tracking year-over-year changes in flag state ranking for maritime risk assessment

## Pricing

- **Free tier:** Full table available as a free PDF download; no registration required
- **Paid tiers:** None
- **Enterprise:** N/A
- **Notes:** Published as a public advocacy and transparency resource by ICS.

## Authentication

No authentication required. Download the PDF directly from the ICS resource page.

## Endpoints

- **2025/2026 edition:** `https://www.ics-shipping.org/resource/shipping-industry-flag-state-performance-table-2025-2026/`
- **ICS resources hub:** `https://www.ics-shipping.org/resources/` — archive of prior editions
- **Access method:** PDF download (annual); no REST API

**No programmatic API exists.** Data is published as a PDF table; extract with tabula-py or pdfplumber for analysis.

## Example call

```bash
# Download the current edition PDF
curl -L -o ics-flag-state-table-2025-2026.pdf \
  "https://www.ics-shipping.org/resource/shipping-industry-flag-state-performance-table-2025-2026/"
```

```python
import tabula
import pandas as pd

# Extract tables from the PDF
dfs = tabula.read_pdf("ics-flag-state-table-2025-2026.pdf", pages="all", multiple_tables=True)
for df in dfs:
    print(df.head())
```

## Rate limits

No API — PDF download only. No rate limits.

## SDKs / Libraries

- **Official:** None
- **Community:** tabula-py or pdfplumber (Python) for PDF table extraction

## Documentation

- 2025/2026 edition: https://www.ics-shipping.org/resource/shipping-industry-flag-state-performance-table-2025-2026/
- ICS resources: https://www.ics-shipping.org/resources/
- About ICS: https://www.ics-shipping.org/about-ics/

## Notes

- The 2025/2026 edition was published January 2026; covers performance data through 2024.
- 19 criteria scored per flag state include: ratification of SOLAS, MARPOL, MLC 2006, STCW, and other IMO conventions; IMO Member Audit Scheme status; Paris MoU, Tokyo MoU, US Coast Guard, and other PSC detention rates.
- Flag states are color-coded (green/amber/red) based on aggregate score — useful for quick vetting decisions.
- The table covers ~100 flag states representing the world fleet by GT.
- For vessel-level Port State Control inspection records, pair with Paris MoU and Tokyo MoU inspection databases (separate sources).
- For flag state casualty investigation standards, cross-reference with IMO GISIS (`imo-gisis.md`) investigation reports.
- ICS represents national shipowner associations from 40+ countries — the table reflects industry-consensus performance benchmarks, not a regulatory authority assessment.
