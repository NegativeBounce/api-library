# FCC Universal Licensing System (ULS)

Free public US Federal Communications Commission database of every active and archived wireless license (amateur, commercial mobile, broadcast auxiliary, public safety, etc.). Daily-updated bulk data dumps and a web/CSV/XML query interface.

**Tier:** Free (US government public data)
**Auth:** None for public read; FRN + CORES password required for filing
**Last researched:** 2026-05-09

## Use cases

- Look up call sign, licensee, frequency assignment, location, and status of any US wireless license
- OSINT / due-diligence research on commercial spectrum holders
- Bulk download of license records (e.g., GMRS, Amateur, Maritime Mobile, Aviation) for analysis
- Cross-referencing detected RF emissions against legitimate license assignments
- Mapping wireless license geographic coverage areas

## Pricing

- **Free tier:** Fully free. No request quotas published; courteous use expected (avoid hammering the public servers).
- **Paid tiers:** None.
- **Enterprise:** N/A — public US government data.
- **Notes:** Filing fees apply when submitting/modifying licenses (separate from query/download access).

## Authentication

No auth for public license search or bulk downloads. To file or modify licenses, register at FCC CORES (Commission Registration System) for an FRN (FCC Registration Number) + password.

## Endpoints

- **Base URL:** `https://wireless2.fcc.gov/UlsApp/UlsSearch/`
- **Key endpoints / interfaces:**
  - `searchLicense.jsp` — license search (basic + advanced)
  - `searchAdvanced.jsp` — fielded queries by call sign, FRN, frequency, geographic region, radio service code
  - Bulk data dumps (pipe-delimited `.dat` files) — `https://data.fcc.gov/download/pub/uls/complete/` (e.g., `l_amat.zip` for amateur)
  - Daily incremental updates published alongside weekly full dumps
  - opendata.fcc.gov — FCC's open data portal mirrors selected ULS datasets via Socrata APIs

## Example call

```bash
# Bulk-download the entire amateur radio license dataset (pipe-delimited .dat files)
curl -O https://data.fcc.gov/download/pub/uls/complete/l_amat.zip
unzip l_amat.zip
head -1 HD.dat | tr '|' '\n'   # field layout
```

```bash
# Programmatic license search (returns HTML — parse with BeautifulSoup or similar)
curl "https://wireless2.fcc.gov/UlsApp/UlsSearch/searchLicense.jsp?searchValue=W1AW"
```

```python
# Pull recent ULS data via Socrata (opendata.fcc.gov)
import requests
r = requests.get("https://opendata.fcc.gov/resource/x28i-i4z4.json", params={"$limit": 100})
print(r.json())
```

## Rate limits

No published hard limit. The public web search throttles aggressive scrapers; bulk downloads are the recommended path for high-volume use. Socrata endpoints have their own per-app-token limits.

## SDKs / Libraries

- **Official:** None — bulk `.dat` files documented in the ULS Public Access Database Specification PDF (search "ULS Public Access Database Specification").
- **Community:** Numerous parsers in Python/R/Go, including `pyhamtools` (amateur callsign lookups), `uls-database` mirrors on GitHub.

## Documentation

- ULS landing page: https://www.fcc.gov/wireless/universal-licensing-system
- License search: https://wireless2.fcc.gov/UlsApp/UlsSearch/searchLicense.jsp
- All FCC databases: https://www.fcc.gov/licensing-databases/search-fcc-databases
- Data.gov catalog entry: https://catalog.data.gov/dataset/fcc-universal-licensing-system-uls
- Open data portal: https://opendata.fcc.gov/Wireless/FCC-Universal-Licensing-System-ULS-/x28i-i4z4

## Notes

- Coverage is US-only. International equivalents: ITU MARS (commercial maritime), Ofcom (UK), BNetzA (Germany), JPN MIC (Japan), etc.
- ULS does NOT include broadcast (radio/TV stations) — those live in CDBS / LMS (FCC Licensing & Management System).
- Some sensitive categories (federal users, classified spectrum) are not in ULS by design.
- Bulk file format is pipe-delimited (`|`); the spec defines record types (HD, EN, HS, FR, LO, AN, LA, etc.).
- Cross-listing: useful supplement to `cellular-intelligence` (commercial mobile licensees) and `bluetooth-intelligence` (low-power Part 15 — though Part 15 is unlicensed, not in ULS).
