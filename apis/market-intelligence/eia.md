# EIA (U.S. Energy Information Administration)

Free official U.S. government API for energy data — crude oil, petroleum products, natural gas, electricity, and prices/inventories — with global coverage on many series.

**Tier:** Free
**Auth:** API Key (free)
**Last researched:** 2026-06-11

## Use cases

- Authoritative energy-price and inventory data (Brent/WTI spot, gasoline, distillate, natural gas) to anchor security→energy-market analysis.
- Weekly petroleum status (stocks, imports, refinery utilization) for supply-disruption context after chokepoint events.
- Long historical series for trend baselines in intelligence reports.

## Pricing

- **Free tier:** Fully free with a registered API key. Generous limits.
- **Paid tiers:** None.
- **Enterprise:** N/A (US government).
- **Notes:** Data is public domain; the v2 API is well documented and stable.

## Authentication

Free API key (register on the EIA Open Data site); passed as the `api_key` query parameter.

## Endpoints

- **Base URL:** `https://api.eia.gov/v2`
- **Key endpoints:**
  - `GET /petroleum/pri/spt/data/` — spot prices (Brent, WTI, products)
  - `GET /petroleum/stoc/wstk/data/` — weekly stocks/inventories
  - `GET /natural-gas/pri/fut/data/` — natural gas prices/futures
  - `GET /seriesid/{series}` — direct series lookup (legacy-style)

## Example call

```bash
curl "https://api.eia.gov/v2/petroleum/pri/spt/data/?api_key=$EIA_KEY&frequency=daily&data[0]=value&facets[product][]=EPCBRENT&sort[0][column]=period&sort[0][direction]=desc&length=5"
```

```python
import requests
r = requests.get("https://api.eia.gov/v2/petroleum/pri/spt/data/",
                 params={"api_key": "YOUR_KEY", "frequency": "daily",
                         "data[0]": "value", "length": 5})
print(r.json()["response"]["data"][:3])
```

## Rate limits

Not a hard public cap for normal use; reasonable throttling applies. Suitable for production with caching.

## SDKs / Libraries

- **Official:** Documented v2 REST API + browser/Excel add-in.
- **Community:** `myeia`, `eia-python`, and other wrappers (Python); various JS clients.

## Documentation

- API docs: https://www.eia.gov/opendata/
- Browser: https://www.eia.gov/opendata/browser/

## Notes

- The **best free, authoritative energy source** for this layer — ideal for quantifying oil/gas reaction to Hormuz/Red Sea/Bab el Mandeb events. Public-domain data, no usage cost.
- Pair with `market-intelligence/world-bank-data.md` (monthly global commodity "Pink Sheet" index) and `market-intelligence/imf-data.md` (macro/commodity prices) for a free official-source stack.
- Cross-reference: FRED (`semiconductor-intelligence/fred.md`) also carries many EIA-derived energy series with a single key.
