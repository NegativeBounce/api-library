# SEC EDGAR API

Free, public RESTful APIs from the U.S. Securities and Exchange Commission delivering JSON-formatted EDGAR filing histories and XBRL-extracted financial statement data for all SEC-registered companies.

**Tier:** Free
**Auth:** None (descriptive User-Agent header required)
**Last researched:** 2026-05-14

## Use cases

- Pull full filing histories for chipmakers — every 10-K, 10-Q, and 8-K filed by NVIDIA (CIK 0001045810), Intel (CIK 0000050863), and AMD (CIK 0000002488), including accession numbers and document URLs — to build a filings monitor for the U.S. semiconductor sector
- Extract comparable financials across competitors using the Company Facts / Company Concept APIs to pull standardized US-GAAP XBRL tags (Revenues, ResearchAndDevelopmentExpense, GrossProfit) and compare R&D intensity quarter-over-quarter
- Benchmark one metric across the whole industry at a point in time with the Frames API — grab a concept for a calendar quarter across all filers, then filter to SIC code 3674 (Semiconductors) to rank chip companies

## Pricing

- **Free tier:** No usage cost; all EDGAR data is U.S. Government public domain — no licensing fees, no redistribution restrictions
- **Paid tiers:** None
- **Enterprise:** N/A — for heavy use, the SEC recommends the nightly bulk ZIP files (`companyfacts.zip`, `submissions.zip`, recompiled ~3:00 a.m. ET) instead of high-volume API calls
- **Notes:** The only constraint is the fair-access rate limit (see below).

## Authentication

No credentials, API key, or account required. You must send a descriptive `User-Agent` HTTP header containing a contact email address, e.g. `User-Agent: Negative Bounce Research contact@example.com`. Requests without a proper User-Agent may be throttled or blocked.

## Endpoints

- **Base URL:** `https://data.sec.gov`
- **Key endpoints:**
  - `GET /submissions/CIK##########.json` — full filing history and metadata (name, former names, tickers, exchanges, SIC code) for one entity; CIK is 10 digits, zero-padded
  - `GET /api/xbrl/companyfacts/CIK##########.json` — all XBRL facts (every concept, every period) for one company
  - `GET /api/xbrl/companyconcept/CIK##########/us-gaap/{Tag}.json` — all disclosed values for one XBRL concept (e.g., `Revenues`, `ResearchAndDevelopmentExpense`) for one company
  - `GET /api/xbrl/frames/us-gaap/{Tag}/{Unit}/CY####Q#.json` — one fact per reporting entity for a concept across all filers for a calendar period
- **Supporting (on `www.sec.gov`):** ticker→CIK map at `https://www.sec.gov/files/company_tickers.json`

## Example call

```bash
# NVIDIA filing history
curl -s 'https://data.sec.gov/submissions/CIK0001045810.json' \
  -H 'User-Agent: Negative Bounce Research contact@example.com'

# NVIDIA quarterly/annual Revenues (single XBRL concept)
curl -s 'https://data.sec.gov/api/xbrl/companyconcept/CIK0001045810/us-gaap/Revenues.json' \
  -H 'User-Agent: Negative Bounce Research contact@example.com'
```

```python
import requests

HEADERS = {"User-Agent": "Negative Bounce Research contact@example.com"}
# NVIDIA = CIK 1045810
facts = requests.get(
    "https://data.sec.gov/api/xbrl/companyfacts/CIK0001045810.json",
    headers=HEADERS, timeout=30,
).json()
rnd = facts["facts"]["us-gaap"]["ResearchAndDevelopmentExpense"]["units"]["USD"]
for f in rnd[-4:]:
    print(f["end"], f["val"], f.get("form"))
```

## Rate limits

Published fair-access limit: 10 requests per second. The SEC asks users to script efficiently and use the bulk ZIP files for large pulls. Exceeding the limit — or omitting the User-Agent header — can result in temporary IP blocking.

## SDKs / Libraries

- **Official:** None — the SEC publishes only the raw REST endpoints and bulk files
- **Community:** `sec-edgar-api` (Python — handles rate-limiting/User-Agent), `sec-cik-mapper`, `edgartools`, `python-edgar`, `sec-edgar-downloader`. (`sec-api` / sec-api.io is a separate commercial third-party product, not the SEC's own API.)

## Documentation

- Main docs: https://www.sec.gov/search-filings/edgar-application-programming-interfaces
- Developer resources: https://www.sec.gov/about/developer-resources

## Notes

- The required `User-Agent` header containing a contact email is the single most common reason scripts get 403/blocked.
- CIK must be 10 digits, zero-padded in URL paths (`CIK0001045810`, not `CIK1045810`).
- No CORS support — cannot be called directly from browser JavaScript; needs a server-side proxy.
- Foreign private issuers (e.g., TSMC, ASML, which file 20-F/6-K) have thinner and less consistent XBRL tagging than domestic 10-K/10-Q filers; TSMC's primary financials are IFRS. The Frames API works best for US-GAAP domestic filers.
- XBRL data only goes back to ~2009 (when XBRL was first required); older filings exist in `submissions` but not in the XBRL APIs.
- Frame periods are calendar-aligned approximations — companies with non-calendar fiscal years (NVIDIA's ends in late January) get bucketed into the nearest calendar quarter, so cross-company comparisons need care.
