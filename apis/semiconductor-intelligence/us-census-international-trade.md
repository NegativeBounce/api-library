# U.S. Census Bureau International Trade API

Delivers detailed monthly U.S. import and export statistics (2010–present) by commodity classification (HS, NAICS, SITC, End-use, Advanced Technology), country, U.S. state, and port.

**Tier:** Free
**Auth:** None / API Key (optional)
**Last researched:** 2026-05-14

## Use cases

- Pull monthly U.S. imports of integrated circuits (HS 8542) by country code to track sourcing-country dependence (e.g., Taiwan, Malaysia, China) and quantify reshoring / friend-shoring trends over time
- Combine HS-code import data with the Advanced Technology Products dataset to isolate semiconductor-specific high-tech trade balances for U.S. supply-chain and policy analysis
- Use state- and port-level HS endpoints to see where semiconductor imports/exports physically enter and leave the U.S. — useful for logistics and fab-location supply-chain mapping

## Pricing

- **Free tier:** Entirely free open U.S. government data; up to 500 API calls/day without a key
- **Paid tiers:** None
- **Enterprise:** N/A — same free service for all users
- **Notes:** Above 500 calls/day a free API key is required (registration only, no cost). Data is U.S. Government public domain — free to use and redistribute; cite the Census Bureau.

## Authentication

No key needed under 500 calls/day. For heavier use, get a free API key at https://api.census.gov/data/key_signup.html (email registration; key arrives by email) and append it as a `&key=YOUR_KEY` query parameter. There is no header-based auth.

## Endpoints

- **Base URL:** `https://api.census.gov/data/timeseries/intltrade/`
- **Key endpoints:**
  - `GET /imports/hs` — monthly U.S. imports by Harmonized System code
  - `GET /exports/hs` — monthly U.S. exports by Harmonized System code
  - `GET /imports/naics` / `GET /exports/naics` — by NAICS industry code
  - `GET /imports/statehs` / `GET /imports/porths` — state- and port-level HS data (2-, 4-, 6-digit HS only)
  - Advanced Technology Products dataset — high-tech (including semiconductor) trade
- **Key variables:** `I_COMMODITY` / `E_COMMODITY` (HS code), `GEN_VAL_MO` (general imports monthly value), `CON_VAL_MO` (imports for consumption), `ALL_VAL_MO` (exports monthly value), `CTY_CODE` / `CTY_NAME` (partner country), `time` (YYYY-MM), `COMM_LVL` (HS digit level)

## Example call

```bash
# U.S. imports of integrated circuits (HS 8542) by country, January 2024
curl "https://api.census.gov/data/timeseries/intltrade/imports/hs?get=CTY_CODE,CTY_NAME,I_COMMODITY,I_COMMODITY_LDESC,GEN_VAL_MO&I_COMMODITY=8542&time=2024-01"
```

```python
import requests

params = {
    "get": "CTY_CODE,CTY_NAME,I_COMMODITY,GEN_VAL_MO",
    "I_COMMODITY": "8542",
    "time": "2024-01",
    "key": CENSUS_API_KEY,  # optional
}
r = requests.get(
    "https://api.census.gov/data/timeseries/intltrade/imports/hs",
    params=params)
data = r.json()  # first row = header, rest = records
```

## Rate limits

500 calls/day per IP without an API key. With a free API key there is no hard published daily cap, but Census advises breaking up large queries — a single call requesting all countries and/or all commodities will error.

## SDKs / Libraries

- **Official:** No official SDK; Census provides an interactive International Trade API Query Builder (https://www.census.gov/foreign-trade/api_tool.html)
- **Community:** `census` and `cenpy` (Python); `censusapi` and `tidycensus` (R) — primarily demographic-focused but can hit any Census API endpoint. For trade specifically, most users call the REST endpoints directly.

## Documentation

- Main docs: https://www.census.gov/data/developers/data-sets/international-trade.html
- API reference (machine-readable variable lists): https://api.census.gov/data/timeseries/intltrade/imports/hs.html
- Census Data API User Guide: https://www.census.gov/data/developers/guidance/api-user-guide.html

## Notes

- Coverage starts January 2010; updated monthly with the trade press release (~5–6 week lag).
- U.S.-centric only — for non-U.S. flows use UN Comtrade. The two complement each other: Census for U.S. dependency mapping with port/state detail, Comtrade for global concentration and mirror-flow analysis.
- Queries that are too broad (all countries × all commodities) return errors — paginate by commodity, country, or time. `COMM_LVL` controls HS digit granularity; state and port data are limited to 2/4/6-digit HS.
- Two import value concepts: `GEN_VAL_MO` (general imports) vs. `CON_VAL_MO` (imports for consumption) — pick deliberately.
- Data is sourced from Customs ACE and Electronic Export Information and is subject to revision in later monthly releases.
