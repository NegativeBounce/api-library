# FRED API

RESTful web service from the St. Louis Fed providing programmatic access to 800,000+ U.S. and international economic time series, including semiconductor manufacturing output, capacity, and price indices.

**Tier:** Free
**Auth:** API Key (query parameter)
**Last researched:** 2026-05-14

## Use cases

- Track U.S. semiconductor manufacturing health by pulling `IPG3344S` (Industrial Production: Semiconductor and Other Electronic Components, NAICS 3344) and `CAPG3344S` (Industrial Capacity for the same sector) to monitor output and capacity-utilization cycles
- Build a leading-indicator dashboard correlating broader electronics output (`IPG334S`) against manufacturers' new orders, semiconductor PPI, and business inventories to time industry up/down cycles
- Discover and bulk-download all semiconductor-related series via `series/search?search_text=semiconductor`, then pull historical vintages with the ALFRED real-time endpoints to study data revisions for forecasting models

## Pricing

- **Free tier:** Entirely free; 120 requests/minute; up to 100,000 observations per request (paginate with `offset`)
- **Paid tiers:** None
- **Enterprise:** N/A — single free tier for all users
- **Notes:** API key is free but rate-limited; abuse can lead to key suspension. No SLA/uptime guarantee — it is a free public service.

## Authentication

Register a free account at https://fredaccount.stlouisfed.org, then request an API key at https://fredaccount.stlouisfed.org/apikeys. Pass the key as a **query parameter**: `?api_key=YOUR_KEY`. There is no header-based auth. Add `&file_type=json` to get JSON — the default response format is XML.

## Endpoints

- **Base URL:** `https://api.stlouisfed.org/fred/`
- **Key endpoints:**
  - `GET /series` — metadata for an economic data series (e.g., `IPG3344S`)
  - `GET /series/observations` — the actual data values for a series (the core data-pull endpoint)
  - `GET /series/search` — find series matching keywords (e.g., "semiconductor")
  - `GET /series/vintagedates` — historical revision dates for a series (real-time/ALFRED data)
  - `GET /category/series` — all series within a FRED category
  - `GET /release/series` — all series in a given data release
  - `GET /tags` / `GET /related_tags` — tag-based series discovery

## Example call

```bash
curl "https://api.stlouisfed.org/fred/series/observations?series_id=IPG3344S&api_key=$FRED_API_KEY&file_type=json&observation_start=2015-01-01"
```

```python
from fredapi import Fred

fred = Fred(api_key=FRED_API_KEY)
data = fred.get_series("IPG3344S")  # Semiconductor industrial production index
print(data.tail())
```

## Rate limits

120 requests per minute — exceeding it returns HTTP 429. Maximum 100,000 observations per request; use the `offset` parameter to paginate.

## SDKs / Libraries

- **Official:** None — REST API only (the St. Louis Fed lists community toolkits)
- **Community:** `fredapi` (Python, widely used); `fredr` (R, CRAN); `pyfredapi` / `fedfred` (Python); FRED data is also accessible via `pandas-datareader`

## Documentation

- Main docs: https://fred.stlouisfed.org/docs/api/fred/
- API key info: https://fred.stlouisfed.org/docs/api/api_key.html
- Terms of use: https://fred.stlouisfed.org/docs/api/terms_of_use.html

## Notes

- Default response format is XML — you must explicitly pass `file_type=json`.
- Use ALFRED (`alfred.stlouisfed.org`) and the `vintagedates` / real-time-period parameters to access point-in-time (unrevised) data — important for backtesting, since series like `IPG3344S` are revised.
- Note the seasonal vs. non-seasonal variants: `IPG3344S` (seasonally adjusted) vs. `IPG3344N` (not adjusted).
- Some underlying source data carries third-party copyright restrictions; FRED's terms require compliance with source-specific licensing and prohibit misrepresenting the data as official Fed output.
