# Alpha Vantage

Developer-friendly financial market data API covering equities, FX, commodities, economic indicators, and technical indicators through a single REST interface.

**Tier:** Freemium
**Auth:** API Key
**Last researched:** 2026-06-11

## Use cases

- Correlating maritime-security events with equity, FX, and commodity price moves (e.g. tanker-equity or energy reactions to a Hormuz disruption).
- Pulling commodity series (Brent, WTI, natural gas) and economic indicators alongside security timelines for intelligence reports.
- Sentiment/news analysis on companies and topics for market-impact context.
- AI/LLM integration via the official MCP server.

## Pricing

- **Free tier:** Free API key; limited to ~25 requests/day (premium-gated beyond that).
- **Paid tiers:** Premium plans roughly $49.99–$249.99/month with higher rate limits.
- **Enterprise:** Higher-volume/commercial licensing — contact Alpha Vantage.
- **Notes:** Officially licensed NASDAQ US market-data provider; backed by Y Combinator. Free-tier limit is low — plan around it.

## Authentication

API key passed as a query parameter (`apikey`). Free key from the Alpha Vantage site.

## Endpoints

- **Base URL:** `https://www.alphavantage.co/query`
- **Key endpoints (via `function` param):**
  - `TIME_SERIES_DAILY` — equity price history
  - `FX_DAILY` / `CURRENCY_EXCHANGE_RATE` — foreign exchange
  - `WTI`, `BRENT`, `NATURAL_GAS` — energy commodity series
  - `REAL_GDP`, `INFLATION`, `FEDERAL_FUNDS_RATE` — economic indicators
  - `NEWS_SENTIMENT` — market news + sentiment

## Example call

```bash
curl "https://www.alphavantage.co/query?function=BRENT&interval=daily&apikey=$ALPHAVANTAGE_KEY"
```

```python
import requests
r = requests.get("https://www.alphavantage.co/query",
                 params={"function": "BRENT", "interval": "daily",
                         "apikey": "YOUR_KEY"})
print(r.json().get("data", [])[:3])
```

## Rate limits

Free tier ~25 requests/day. Premium tiers raise per-minute/day limits (see pricing).

## SDKs / Libraries

- **Official:** Alpha Vantage MCP server (for AI agents); spreadsheet add-ins.
- **Community:** `alpha_vantage` (Python), numerous wrappers in JS/Go/R.

## Notes

- The broadest single free-tier API spanning equities + FX + commodities + macro — convenient for prototyping the market layer, but the 25/day cap means production use needs a premium tier or a mix with the free official sources below.
- For authoritative energy data prefer `market-intelligence/eia.md`; for official macro prefer `market-intelligence/world-bank-data.md` and `market-intelligence/imf-data.md`.
- Cross-reference: FRED (`semiconductor-intelligence/fred.md`) and Financial Modeling Prep (`semiconductor-intelligence/financial-modeling-prep.md`) are already cataloged and complement this for US macro and company fundamentals.
