# IMO GISIS (Global Integrated Shipping Information System)

International Maritime Organization's official database of shipping information, including marine safety investigation reports, casualty statistics, ship particulars, certificates, port and flag state data, and IMO instruments ratification status.

**Tier:** Free
**Auth:** IMO Web Account (free registration)
**Last researched:** 2026-05-13

## Use cases

- Accessing official IMO marine safety investigation reports submitted by member states after serious casualties
- Querying flag state, port state, and recognized organization data for vessel research
- Downloading casualty and incident statistics for global maritime safety trend analysis

## Pricing

- **Free tier:** Full public access with a free IMO Web Account; no cost
- **Paid tiers:** None
- **Enterprise:** N/A
- **Notes:** Registration is free and open to anyone; some modules have public read access without login.

## Authentication

Create a free IMO Web Account at `https://www.imo.org/en/About/Pages/IMO-Accounts.aspx`. Log in to access full GISIS modules including Casualty module and investigation report downloads.

## Endpoints

- **GISIS portal:** `https://gisis.imo.org/public/default.aspx` — public entry point for all GISIS modules
- **Marine safety investigations:** `https://www.imo.org/en/ourwork/iiis/pages/marine-safety-investigation-reports.aspx` — index of submitted investigation reports
- **Access method:** Web portal with Excel/CSV export; no REST API

**No public REST API exists.** Data is accessible via the GISIS web interface; authenticated users can export query results as Excel or CSV files.

## Example call

```python
# GISIS has no REST API — use Selenium or Playwright for browser automation if scraping is needed
from selenium import webdriver
from selenium.webdriver.common.by import By

driver = webdriver.Chrome()
driver.get("https://gisis.imo.org/public/default.aspx")
# Navigate to Casualty module, apply filters, then export to Excel/CSV
# Parse downloaded file with pandas
import pandas as pd
df = pd.read_excel("gisis_casualty_export.xlsx")
print(df.head())
```

## Rate limits

No API — web portal and file download only. No published rate limits; GISIS is not designed for high-frequency automated access.

## SDKs / Libraries

- **Official:** None
- **Community:** None — browser automation (Selenium, Playwright) required for programmatic data extraction

## Documentation

- GISIS portal: https://gisis.imo.org/public/default.aspx
- IMO Web Account registration: https://www.imo.org/en/About/Pages/IMO-Accounts.aspx
- Marine safety investigations index: https://www.imo.org/en/ourwork/iiis/pages/marine-safety-investigation-reports.aspx
- GISIS user guide: https://www.imo.org/en/OurWork/IIIS/Pages/GISIS.aspx

## Notes

- GISIS is the authoritative source for marine casualty investigation reports submitted by IMO member states under resolution MSC.255(84) (Casualty Investigation Code).
- Investigation reports are submitted voluntarily; coverage varies by flag state — major maritime nations (Bahamas, Panama, Marshall Islands, Liberia) generally submit regularly.
- Casualty module data is updated quarterly; individual report uploads may lag the investigation completion date by 6–24 months.
- GISIS modules include: Ship Particulars, Casualties, Flag State Implementation, Port State Control, Recognized Organizations, Certificates, Piracy/Armed Robbery.
- For EU-specific casualty data with more consistent reporting, use EMSA EMCIP (`emsa-emcip.md`).
- For US maritime accidents with a REST API (in progress), see NTSB CAROL (`ntsb-carol.md`).
- IMO investigation reports follow a standardized format (MAIIF guidelines) making them suitable for structured extraction once downloaded.
