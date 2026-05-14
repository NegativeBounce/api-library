# OECD Data API

RESTful, SDMX-standard web service giving programmatic access to OECD statistical datasets — R&D, trade-in-value-added, and short-term production indicators relevant to the semiconductor and electronics sectors.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-14

## Use cases

- Pull R&D and innovation context for the semiconductor sector from the MSTI dataflow (`OECD.STI.STP,DSD_MSTI@DF_MSTI`) — R&D expenditure, researcher counts, patent counts — to benchmark national semiconductor competitiveness across OECD countries
- Analyze semiconductor/electronics global value chains using the TiVA dataflows (`OECD.STI.PIE,DSD_TIVA_MAINLV@DF_MAINLV`), isolating the "Computer, electronic and optical equipment" industry to study foreign value-added content and supply-chain dependency
- Track short-term electronics production and trade momentum via STES short-term indicators and bilateral merchandise-trade dataflows, filtering on electronics/semiconductor product codes to monitor export/import trends by partner country

## Pricing

- **Free tier:** Fully free, open public data; 60 data requests per hour per client
- **Paid tiers:** None
- **Enterprise:** N/A
- **Notes:** Requests using the `lastNObservations` or `firstNObservations` parameters are blocked by OECD. The strict 60/hour limit makes the API unsuitable for high-frequency polling — cache results.

## Authentication

No authentication of any kind — fully anonymous public access. No API key to obtain, no auth headers or query parameters.

## Endpoints

- **Base URL (SDMX v1):** `https://sdmx.oecd.org/public/rest/`
- **Base URL (SDMX v2):** `https://sdmx.oecd.org/public/rest/v2/` (supports `*` wildcards and more dynamic filtering)
- **Key endpoints:**
  - `GET /data/{agencyId},{dataflowId},{version}/{filter-key}` — retrieve observations for a dataflow; the filter-key is dot-separated dimension values (empty = all)
  - `GET /dataflow/{agencyId}/{dataflowId}/{version}?references=all` — list/describe available dataflows and their structure
  - `GET /datastructure/...` — the Data Structure Definition (dimensions, attributes, allowed codes) for a dataflow
  - `GET /codelist/...` — code lists (country codes, indicator codes)
  - `GET /availableconstraint/...` — which dimension combinations actually contain data
- **Query parameters:** `startPeriod`, `endPeriod`, `dimensionAtObservation=AllDimensions`, `format=jsondata` | `csvfilewithlabels`

## Example call

```bash
curl "https://sdmx.oecd.org/public/rest/data/OECD.STI.STP,DSD_MSTI@DF_MSTI,1.3/?dimensionAtObservation=AllDimensions&format=jsondata&startPeriod=2015"
```

```python
import requests, pandas as pd
from io import StringIO

url = ("https://sdmx.oecd.org/public/rest/data/"
       "OECD.STI.STP,DSD_MSTI@DF_MSTI,1.3/"
       "?format=csvfilewithlabels&startPeriod=2015")
df = pd.read_csv(StringIO(requests.get(url).text))
```

## Rate limits

60 requests per hour per client; over-limit requests are temporarily blocked. The `lastNObservations` / `firstNObservations` parameters are not allowed. Large unfiltered queries may time out — filter by dimensions.

## SDKs / Libraries

- **Official:** None — OECD points users to the generic SDMX ecosystem and publishes an "SDMX RESTful web service cheat sheet"
- **Community:** `pandasdmx` / `sdmx1` (Python); `rsdmx` and the `OECD` package (R)

## Documentation

- API explainer / how-to: https://www.oecd.org/en/data/insights/data-explainers/2024/09/api.html
- SDMX-JSON documentation: https://data.oecd.org/api/sdmx-json-documentation/
- Live dataflow list: https://sdmx.oecd.org/public/rest/dataflow

## Notes

- Major 2024 migration: the legacy OECD.Stat platform/API was retired and replaced by the OECD Data Explorer + this SDMX API — old `stats.oecd.org` endpoints and dataset codes no longer work. Dataflow IDs are now triplet form (`agency,dataflowId,version`).
- There is no FRED-style keyword search — you must discover the correct agency/dataflow/version triplet and dimension order via the `/dataflow` and `/datastructure` endpoints first.
- Two SDMX API versions coexist (v1 vs. v2) with different filtering syntax.
- Default output is verbose SDMX-ML; pass `format=jsondata` or `format=csvfilewithlabels` for easier parsing.
- Usage is subject to OECD Terms and Conditions — data is generally reusable with attribution, though some datasets have restrictions.
