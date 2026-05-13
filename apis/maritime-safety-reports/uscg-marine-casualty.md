# USCG Marine Casualty Data (MISLE)

US Coast Guard public release of marine casualty and pollution incident data extracted from the Marine Information for Safety and Law Enforcement (MISLE) system — covering all USCG-investigated accidents in US waters from 1982 to present, available as downloadable CSV/Excel datasets.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-13

## Use cases

- Analyzing US marine casualty trends by vessel type, accident cause, geographic area, and outcome (deaths, injuries, property damage)
- Building long-term historical analysis datasets from 40+ years of US Coast Guard incident records
- Researching pollution incidents and casualty patterns in specific US ports, waterways, or coastal zones

## Pricing

- **Free tier:** Full dataset download free with no registration required
- **Paid tiers:** None
- **Enterprise:** N/A — US government public data release
- **Notes:** Published under the US government open data policy; no license restrictions on use.

## Authentication

No authentication required. Download directly from Homeport or Data.gov.

## Endpoints

- **Primary download (Homeport):** `https://homeport.uscg.mil/missions/investigations/marine-casualty-pollution-investigations` — MISLE_DATA.zip containing all casualty records
- **Data.gov listing:** Search `https://catalog.data.gov/` for "USCG Marine Casualty" to find current dataset links and metadata
- **ArcGIS dashboard (2012–2022):** Interactive visualization at USCG ArcGIS portal — provides geographic mapping and basic filtering without download
- **Access method:** CSV/Excel bulk download; no REST API

**No REST API exists.** Data is released as a bulk ZIP archive containing CSV or Excel files. Updates are periodic (annually or as new data is processed).

## Example call

```bash
# Download the MISLE data ZIP
curl -L -o MISLE_DATA.zip \
  "https://homeport.uscg.mil/missions/investigations/marine-casualty-pollution-investigations"
# Extract and inspect
unzip MISLE_DATA.zip -d misle_data/
head -5 misle_data/*.csv
```

```python
import pandas as pd
import zipfile, io, requests

resp = requests.get(
    "https://homeport.uscg.mil/missions/investigations/marine-casualty-pollution-investigations",
    headers={"User-Agent": "Mozilla/5.0"},
)
# Download may redirect — follow to ZIP file URL and extract
with zipfile.ZipFile(io.BytesIO(resp.content)) as z:
    for name in z.namelist():
        print(name)
    df = pd.read_csv(z.open("casualty.csv"))
    print(df.head())
```

## Rate limits

No API — bulk file download only. No rate limits; the file is a static dataset release.

## SDKs / Libraries

- **Official:** None
- **Community:** None — use pandas for CSV/Excel processing after download

## Documentation

- Homeport download page: https://homeport.uscg.mil/missions/investigations/marine-casualty-pollution-investigations
- Data.gov USCG datasets: https://catalog.data.gov/organization/dot-gov (search "marine casualty")
- USCG investigation program: https://www.dco.uscg.mil/Our-Organization/Deputy-for-Operations-Policy-and-Capabilities/Inspections-and-Compliance/Investigations/

## Notes

- Dataset covers all USCG-investigated marine casualties in US waters from 1982 to present — over 100,000 incident records in recent releases.
- Key fields include: vessel name, vessel type, official number, flag, date, location (lat/lon), number of deaths/injuries/missing, property damage estimate, accident type, contributing factors, and case classification.
- Pollution incidents (oil spills, hazmat releases) are included in the same dataset alongside casualty records.
- The ArcGIS dashboard (2012–2022 data) provides geographic visualization but is limited to that date range; the full historical dataset requires downloading the ZIP.
- USCG data covers recreational vessels and commercial vessels; this is a key differentiator from NTSB CAROL (`ntsb-carol.md`), which covers only significant commercial accidents.
- USCG classifies accidents by vessel type including: commercial fishing vessels, passenger vessels, cargo vessels, towing vessels, recreational boats, and uninspected vessels.
- For investigation narrative reports (not just statistics), use NTSB CAROL for major accidents or the USCG investigation portal for USCG-authored reports.
