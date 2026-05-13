# OSAC Country Security Reports

The Overseas Security Advisory Council (OSAC), operated by the U.S. State Department's Bureau of Diplomatic Security, publishes country-level security reports covering crime, civil unrest, terrorism, and travel risk for over 200 countries and territories.

**Tier:** Free (registration required)
**Auth:** Account (free)
**Last researched:** 2026-05-13

## Use cases

- Obtaining detailed country-level crime and security assessments for port regions and maritime chokepoints
- Supplementing RSS-based incident feeds with structured threat environment context per country
- Researching historical crime trends in specific port cities covered in OSAC country reports

## Pricing

- **Free tier:** Full access to all country reports and regional briefs; registration with a U.S.-affiliated organization is required
- **Paid tiers:** None
- **Enterprise:** N/A
- **Notes:** OSAC membership is intended for U.S. private-sector organizations operating overseas. International organizations may access public-facing reports without membership at a reduced data level.

## Authentication

Registration required at https://www.osac.gov. OSAC is designed for U.S. private-sector organizations with overseas operations. Some country reports are publicly accessible without login; full report access requires a free registered account.

## Endpoints

- **Base URL:** `https://www.osac.gov`
- **Key endpoints:** Web-based only — no public REST API
  - Country reports: `https://www.osac.gov/Country/` — browse or search by country
  - Regional briefs: Published periodically under specific country and regional pages

**No machine-readable API is available.** Access is via the web portal only.

## Example call

```python
# No official API — example using requests to scrape public report pages
import requests
from bs4 import BeautifulSoup

resp = requests.get("https://www.osac.gov/Country/Somalia/Content/Detail/Report/")
soup = BeautifulSoup(resp.text, "html.parser")
# Parse report content from HTML
```

## Rate limits

No published limits. The site is not designed for automated scraping; use sparingly and respect `robots.txt`.

## SDKs / Libraries

- **Official:** None
- **Community:** `github.com/Aureum01/StateGovTravelAdvisory` — community wrapper for related U.S. State Dept travel advisory data

## Documentation

- OSAC main site: https://www.osac.gov
- Country reports index: https://www.osac.gov/Country

## Notes

- OSAC country reports are written by Diplomatic Security officers in-country and updated annually or after significant security events — they provide depth and local context that RSS feeds lack.
- For real-time incident alerting, pair OSAC reports with the U.S. State Department Travel Advisories RSS feed (`us-state-dept-travel-advisories.md`).
- OSAC also publishes regional security briefs, crime-and-safety reports, and annual crime statistics for major cities — useful for building baseline threat profiles for specific port cities.
- Countries of high maritime security relevance with active OSAC coverage include: Somalia, Nigeria, Yemen, Libya, Indonesia, Malaysia, Philippines, Colombia, Venezuela, Panama.
