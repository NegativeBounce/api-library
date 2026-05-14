# UN Comtrade API

Programmatic access to the United Nations' database of official international merchandise trade statistics, covering import/export flows by commodity, reporter, partner, and period for ~200 countries.

**Tier:** Freemium
**Auth:** Subscription Key
**Last researched:** 2026-05-14

## Use cases

- Track global trade flows of integrated circuits (HS 8542) and semiconductor devices (HS 8541) to map which countries are net exporters vs. importers and detect supply-chain concentration risk (e.g., Taiwan/Korea export dominance)
- Build bilateral mirror-flow comparisons (`getBilateralData`) to quantify discrepancies in reported semiconductor trade between partners — useful for spotting transshipment or re-export routing through hubs like Hong Kong or Malaysia
- Monitor time-series for subheadings like 854231 (processors/controllers) and 854232 (memories) to correlate trade-volume shifts with export-control events, fab capacity changes, or demand shocks

## Pricing

- **Free tier:** Public (no registration) — preview endpoints, unlimited calls/day, max 500 records per call. Free registered (subscription key) — 500 calls/day, up to 100,000 records per call
- **Paid tiers:** Premium subscriptions add bulk file download, async/batch download, and priority access to the Comtrade Data Lake; specific price points are not publicly documented — arranged directly with UN Comtrade
- **Enterprise:** Institutional/bulk licensing handled directly by UN Comtrade; Data Lake access is the premium differentiator
- **Notes:** Billing/quota distinguishes "final data" (standardized/cleaned) from "tariff-line data" (most granular, as-reported).

## Authentication

Register free at https://comtradedeveloper.un.org/, subscribe to a product, and obtain a subscription key from your profile. Public preview endpoints (`/public/v1/...`) require no key. Authenticated endpoints (`/data/v1/...`, `/tools/v1/...`) require the key, passed either as a `subscription-key` query parameter or via the `Ocp-Apim-Subscription-Key` header (Azure API Management standard).

## Endpoints

- **Base URL:** `https://comtradeapi.un.org`
- **Key endpoints:**
  - `GET /public/v1/preview/{typeCode}/{freqCode}/{clCode}` — free preview of final trade data (max 500 records)
  - `GET /data/v1/get/{typeCode}/{freqCode}/{clCode}` — full final trade data (requires key)
  - `GET /data/v1/getTariffline/{typeCode}/{freqCode}/{clCode}` — full tariff-line (most granular) data
  - `GET /tools/v1/getBilateralData/...` — reported data vs. partner mirror data
  - `GET /tools/v1/getTradeBalance/...` — trade balance indicator
- **Key query params:** `reporterCode`, `partnerCode` (0 = World), `cmdCode` (HS code), `flowCode` (M = imports, X = exports), `period` (e.g., `202205` or `2023`), `maxRecords`

## Example call

```bash
# Free preview — IC (HS 8542) imports reported by the USA (842), monthly, May 2022
curl "https://comtradeapi.un.org/public/v1/preview/C/M/HS?reporterCode=842&period=202205&cmdCode=8542&flowCode=M&partnerCode=0&maxRecords=500"

# Authenticated full data
curl "https://comtradeapi.un.org/data/v1/get/C/A/HS?reporterCode=842&period=2023&cmdCode=8542&flowCode=M&subscription-key=$COMTRADE_KEY"
```

```python
import comtradeapicall

df = comtradeapicall.previewFinalData(
    typeCode="C", freqCode="A", clCode="HS", period="2023",
    reporterCode="842", cmdCode="8542", flowCode="M",
    partnerCode=None, partner2Code=None, customsCode=None, motCode=None,
    maxRecords=500, format_output="JSON", breakdownMode="classic",
    aggregateBy=None, countOnly=None, includeDesc=True)
```

## Rate limits

- Public (no key): unlimited calls/day, 500 records/call
- Free registered: 500 calls/day, 100,000 records/call (async jobs up to 2.5M records)
- Premium: higher quotas and bulk access — exact published numbers vary by subscription product

## SDKs / Libraries

- **Official:** `comtradeapicall` (Python, PyPI — maintained by the `uncomtrade` GitHub org; wraps preview/get/async/bulk/metadata)
- **Community:** `comtradr` (R, rOpenSci — check version for modern-API support, as it was originally built for the legacy API)

## Documentation

- Main docs: https://uncomtrade.org/docs
- Developer portal / API reference: https://comtradedeveloper.un.org/

## Notes

- This is the modern API (`comtradeapi.un.org`). The legacy API (`comtrade.un.org/api/...`) is being retired — use the new one.
- HS code coverage: 8541 (diodes/transistors/semiconductor devices), 8542 (electronic integrated circuits), and 6-digit subheadings like 854231/854232/854233/854239. Tariff-line endpoints expose national codes beyond 6 digits.
- Data is reported by national statistical agencies — expect reporting lags (months to a year+) and gaps for some reporters; use mirror data to fill gaps.
- Bulk/premium data and redistribution are governed by UN Comtrade terms — review before redistributing.
