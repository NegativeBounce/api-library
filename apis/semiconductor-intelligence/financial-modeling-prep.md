# Financial Modeling Prep

Commercial financial-data API providing real-time and historical stock prices, standardized financial statements, ratios, valuation models, analyst estimates, and institutional holdings for global public companies.

**Tier:** Freemium
**Auth:** API Key (query parameter)
**Last researched:** 2026-05-14

## Use cases

- Build a standardized financial-statement comparison for chipmakers — pull income statements, balance sheets, and cash-flow statements for NVDA, AMD, INTC, and TSM in a consistent schema, avoiding the per-company XBRL-tag wrangling that SEC EDGAR requires
- Run valuation screens on the semiconductor sector using the DCF/valuation, key-metrics, and financial-ratios endpoints plus the stock screener (filter by industry "Semiconductors") to rank chip stocks by P/E, EV/EBITDA, and gross margin
- Track ownership and analyst sentiment — pull Form 13F institutional holdings to see which funds are accumulating/reducing semiconductor positions, combined with analyst price targets and earnings-call transcripts

## Pricing

*Prices below are the annual-billed monthly rate; month-to-month billing runs ~34% higher. A separate "Commercial Use" track exists at higher prices for public display/redistribution.*

- **Free tier:** "Basic" — free; 250 API calls/day; end-of-day data only; 5 years history; 500 MB/30-day bandwidth
- **Paid tiers:**
  - Starter — $22/mo; 300 calls/min; real-time US coverage; annual fundamentals & ratios; 20 GB bandwidth
  - Premium — $59/mo; 750 calls/min; 30+ years history; UK & Canada coverage; full fundamentals & ratios; intraday charts; custom DCF; 50 GB bandwidth
  - Ultimate — $149/mo; 3,000 calls/min; global coverage; earnings-call transcripts; ETF/mutual-fund and 13F institutional holdings; 1-minute intraday; 150 GB bandwidth
- **Enterprise:** Custom-priced; 1 TB+/30-day bandwidth, higher limits, redistribution/display licensing — contact FMP
- **Notes:** Bandwidth is a trailing-30-day cap per plan. Publicly displaying or redistributing FMP data requires a separate Data Display and Licensing Agreement (the "Commercial Use" pricing track).

## Authentication

Sign up at https://site.financialmodelingprep.com/ — the developer dashboard issues an API key. Pass the key as a query parameter on every request: `?apikey=YOUR_KEY`. FMP does not use header-based auth for the standard REST API.

## Endpoints

Two API generations are in use: the newer `stable` base (`https://financialmodelingprep.com/stable/`) and the legacy versioned base (`https://financialmodelingprep.com/api/v3/`).

- **Base URL:** `https://financialmodelingprep.com/api/v3/` (legacy form shown below)
- **Key endpoints:**
  - `GET /profile/{ticker}` — company profile: sector, industry, market cap, description
  - `GET /income-statement/{ticker}` — annual/quarterly income statements (also `balance-sheet-statement`, `cash-flow-statement`)
  - `GET /ratios/{ticker}` / `GET /key-metrics/{ticker}` — financial ratios and per-share/valuation metrics
  - `GET /discounted-cash-flow/{ticker}` — DCF intrinsic-value estimate
  - `GET /stock-screener?industry=Semiconductors` — screen/list semiconductor companies by fundamentals
  - `GET /analyst-estimates/{ticker}` — analyst estimates and price targets
  - 13F institutional holdings and earnings-call transcript endpoints — Ultimate plan only

## Example call

```bash
# NVIDIA annual income statements
curl -s "https://financialmodelingprep.com/api/v3/income-statement/NVDA?period=annual&limit=5&apikey=$FMP_API_KEY"

# Screen the semiconductor industry
curl -s "https://financialmodelingprep.com/api/v3/stock-screener?sector=Technology&industry=Semiconductors&limit=100&apikey=$FMP_API_KEY"
```

```python
import requests

tickers = ["NVDA", "AMD", "INTC", "TSM"]
for t in tickers:
    r = requests.get(
        f"https://financialmodelingprep.com/api/v3/ratios/{t}",
        params={"period": "annual", "limit": 1, "apikey": FMP_API_KEY},
        timeout=30,
    ).json()
    if r:
        print(t, "gross margin:", r[0].get("grossProfitMargin"))
```

## Rate limits

- Basic (free): 250 API calls/day
- Starter: 300 calls/minute
- Premium: 750 calls/minute
- Ultimate: 3,000 calls/minute

Plus a separate trailing-30-day bandwidth cap per plan (Free 500 MB → Ultimate 150 GB → Enterprise 1 TB+).

## SDKs / Libraries

- **Official:** FMP publishes multi-language code examples and an official Excel/Google Sheets add-on; the REST API is plain HTTP/JSON
- **Community:** `fmpsdk` (Python, widely referenced and linked by FMP); various wrappers on PyPI/npm; also available via the RapidAPI marketplace (separate billing)

## Documentation

- Main docs: https://site.financialmodelingprep.com/developer/docs
- Pricing: https://site.financialmodelingprep.com/pricing-plans

## Notes

- Two API generations — the newer `stable` endpoints and legacy `api/v3` / `api/v4`. Older tutorials use v3; FMP is steering new users to `stable`. Check which your code targets.
- Feature gating by plan is significant: 13F holdings, earnings-call transcripts, full international coverage, and 1-minute intraday are Ultimate-only; full 30-year history is Premium+. The free tier is end-of-day only and 250 calls/day — fine for prototyping, not production.
- Redistribution/display requires a separate Commercial Use license — the Personal Use pricing above does not permit publicly displaying FMP data.
- Financials are normalized by FMP's own extraction process, which can occasionally diverge from as-filed SEC numbers — for audit-grade work, cross-check against SEC EDGAR.
- The API key travels in the URL query string — keep it out of logs/repos and proxy server-side.
