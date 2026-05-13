# EMSA EMCIP (European Marine Casualty Information Platform)

European Maritime Safety Agency's centralized database of marine casualties and incidents reported by EU and EEA member states, providing statistical reports, annual overviews, and a public portal for exploring aggregated casualty data.

**Tier:** Free
**Auth:** None (public portal); Member State credentials (full database access)
**Last researched:** 2026-05-13

## Use cases

- Analyzing European maritime casualty trends by vessel type, accident category, and flag state
- Downloading annual EMSA maritime casualty overview PDFs for benchmarking and research
- Exploring aggregated casualty statistics through the public EMCIP portal with filtering by year, vessel type, and accident class

## Pricing

- **Free tier:** Public portal and annual PDF reports available without registration
- **Paid tiers:** None
- **Enterprise:** Full EMCIP database access is restricted to competent authorities and designated national bodies of EU/EEA member states
- **Notes:** Detailed individual casualty records are available only to member state authorities; public data is partially anonymized and aggregated.

## Authentication

No authentication required for the public portal and downloadable reports. Member state authority access requires designated credentials issued by EMSA.

## Endpoints

- **Public portal:** `https://portal.emsa.europa.eu/web/emcip/` — interactive statistics browser; filterable by year, vessel type, casualty class, flag state, and location
- **Annual reports (PDF):** Published each year at the EMSA publications page; 2022–2025 editions available
- **Access method:** Web portal + PDF download; no REST API

**No public REST API exists.** Data is available via the interactive portal and annual PDF publications.

## Example call

```bash
# Download the most recent annual overview PDF (URL varies by edition)
curl -L -o emsa-maritime-casualty-overview-2024.pdf \
  "https://www.emsa.europa.eu/publications/download/..."
# Check https://www.emsa.europa.eu/accident-investigation-ops/casualty-data.html for current PDF links
```

```python
import requests
from bs4 import BeautifulSoup

# Fetch EMSA casualty data page to locate current annual report PDF
resp = requests.get("https://www.emsa.europa.eu/accident-investigation-ops/casualty-data.html")
soup = BeautifulSoup(resp.text, "html.parser")
pdf_links = [a["href"] for a in soup.find_all("a", href=True) if ".pdf" in a["href"]]
for link in pdf_links:
    print(link)
```

## Rate limits

No API — web portal and PDF download only. No published rate limits.

## SDKs / Libraries

- **Official:** None
- **Community:** None — use pdfplumber or tabula-py to extract tables from annual report PDFs

## Documentation

- EMCIP public portal: https://portal.emsa.europa.eu/web/emcip/
- EMSA casualty data page: https://www.emsa.europa.eu/accident-investigation-ops/casualty-data.html
- Annual overview reports: https://www.emsa.europa.eu/publications/

## Notes

- EMCIP collects data submitted by EU and EEA member states under Directive 2009/18/EC on marine accident investigation.
- Public area data is partially anonymized; individual vessel and crew identifiers are removed for privacy.
- Annual overviews cover very serious casualties (VSC), serious casualties, and less serious casualties as defined by IMO resolution MSC.255(84).
- Coverage extends to accidents in European waters and to EU-flagged vessels worldwide.
- Data from non-EU member states (e.g., Norway, Iceland as EEA members) is included; Turkey, UK post-Brexit data is separate.
- For global casualty data, pair with IMO GISIS (`imo-gisis.md`); for UK-specific investigations, use MAIB (`maib.md`).
- The portal's geographic visualization shows accident locations on an interactive map — useful for spatial analysis without API access.
