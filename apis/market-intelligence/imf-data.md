# IMF Data

Free official International Monetary Fund data API (SDMX) covering macroeconomic and financial statistics — GDP, inflation, trade, balance of payments, exchange rates, and commodity prices — for ~190 countries.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-06-11

## Use cases

- Country-level macro context (GDP growth, inflation, fiscal/debt, balance of payments) to frame how unrest or conflict affects national economies in intelligence reports.
- World Economic Outlook (WEO) series with 5-year projections for forward-looking risk narratives.
- International Financial Statistics (IFS), Direction of Trade Statistics (DOTS), exchange rates, and IMF-reported commodity prices.

## Pricing

- **Free tier:** Fully free; no API key required.
- **Paid tiers:** None.
- **Enterprise:** N/A (international organization).
- **Notes:** Data served via SDMX (3.0) — JSON/XML; may need an SDMX parsing library. Update cadence varies by dataset.

## Authentication

None. Public SDMX endpoints.

## Endpoints

- **Base URL:** `https://api.imf.org/external/sdmx/2.1` (SDMX 2.1) / `https://data.imf.org` portal; newer SDMX 3.0 API documented on the IMF data site.
- **Key datasets:**
  - `IFS` — International Financial Statistics
  - `WEO` — World Economic Outlook
  - `DOT` — Direction of Trade Statistics
  - `BOP` — Balance of Payments

## Example call

```bash
# SDMX 2.1 CompactData example (IFS, quarterly GDP for a country):
curl "https://api.imf.org/external/sdmx/2.1/data/IFS/Q.US.NGDP_R_SA_XDC"
```

```python
# Easiest via a client library that handles SDMX, e.g. sdmx1 / pandasdmx
import sdmx
imf = sdmx.Client("IMF")
# explore dataflows, then request a series
```

## Rate limits

Not a hard public cap for normal use; throttling applies. Cache results.

## SDKs / Libraries

- **Official:** SDMX REST API (documented on data.imf.org).
- **Community:** `sdmx1`/`pandasdmx` (Python), `imfapi`/`imfr` (R), various SDMX clients.

## Documentation

- Data portal: https://data.imf.org/en
- API resource: https://data.imf.org/en/Resource-Pages/IMF-API

## Notes

- The authoritative **free macro** source for country-economy context — pairs with `market-intelligence/world-bank-data.md` for development/commodity indicators.
- SDMX adds a parsing step vs. plain REST; a client library is recommended. Verify the current SDMX version/base path before integrating (IMF has been migrating to SDMX 3.0).
- Cross-reference: OECD (`semiconductor-intelligence/oecd-data-api.md`), FRED (`semiconductor-intelligence/fred.md`), and UN Comtrade (`semiconductor-intelligence/un-comtrade.md`) are already cataloged and complement IMF for OECD-country, US, and bilateral-trade detail.
