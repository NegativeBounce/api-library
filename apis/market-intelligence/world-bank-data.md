# World Bank Data

Free official World Bank API for global development and economic indicators, including the monthly "Pink Sheet" commodity price data and ~16,000 time-series indicators across 45+ databases.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-06-11

## Use cases

- Monthly global commodity prices ("Pink Sheet": energy, metals, agriculture) to baseline commodity-market context against security events.
- Country macro/development indicators (GDP, inflation, trade, governance, poverty) for economy-impact framing in intelligence reports.
- Long historical series for trend baselines across 170+ countries.

## Pricing

- **Free tier:** Fully free; no API key required.
- **Paid tiers:** None.
- **Enterprise:** N/A (international organization).
- **Notes:** Indicators API (WDI) is plain REST/JSON — easy to consume. Commodity "Pink Sheet" is a monthly dataset (Excel/CSV) with API access for many series.

## Authentication

None. Public REST endpoints.

## Endpoints

- **Base URL:** `https://api.worldbank.org/v2`
- **Key endpoints:**
  - `GET /country/{iso}/indicator/{code}?format=json` — indicator series by country
  - `GET /indicator/{code}?format=json` — indicator metadata/values
  - `GET /country?format=json` — country list/metadata
  - Commodity "Pink Sheet": monthly dataset (CSV/Excel) via the Commodity Markets pages

## Example call

```bash
# GDP (current US$) for a country, JSON:
curl "https://api.worldbank.org/v2/country/SG/indicator/NY.GDP.MKTP.CD?format=json&per_page=5"
```

```python
import requests
r = requests.get("https://api.worldbank.org/v2/country/SG/indicator/NY.GDP.MKTP.CD",
                 params={"format": "json", "per_page": 5})
print(r.json()[1][:3])
```

## Rate limits

No hard public cap for normal use; be reasonable and cache.

## SDKs / Libraries

- **Official:** Documented Indicators API (v2).
- **Community:** `wbgapi`/`world_bank_data` (Python), `wbstats`/`WDI` (R), JS clients.

## Notes

- The authoritative **free** source for global commodity price indices (Pink Sheet) and broad macro indicators — pairs with `market-intelligence/eia.md` (energy detail) and `market-intelligence/imf-data.md` (financial statistics/WEO).
- Indicators API is trivially easy (plain JSON, no key); the Pink Sheet commodity data is monthly cadence (not intraday) — use commercial feeds (`market-intelligence/commodities-api.md`) for real-time.
- Cross-reference: UN Comtrade (`semiconductor-intelligence/un-comtrade.md`) for bilateral trade, OECD (`semiconductor-intelligence/oecd-data-api.md`) and FRED (`semiconductor-intelligence/fred.md`) for additional macro.
