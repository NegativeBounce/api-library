# Onyphe

French cyber defense search engine providing deep internet scan data with up to 48 months of historical records, vulnerability scanning, CTI enrichment, and the OQLv2 query language — positioned for enterprise attack surface management and threat hunting.

**Tier:** Paid
**Auth:** API Key (Bearer)
**Last researched:** 2026-05-13

## Use cases

- Querying up to 48 months of historical scan data to track how an organization's internet exposure has evolved over time
- Using OQLv2 to perform complex multi-field queries across Onyphe's datascan, vulnscan, and riskscan categories for attack surface discovery
- Bulk-exporting internet scan results for offline analysis of maritime or industrial network exposure across large IP ranges

## Pricing

- **Free tier:** None confirmed — plans start at €599/month
- **Paid tiers:**
  - Starter (Lion View) — €599/month: up to 10M results/month; 1-month data history; enterprise categories and filters; internal use only; no Export/Discovery APIs
  - Pro (Eagle View) — €1,099/month: up to 100M results/month; 7-month history; Vulnscan category; no Export/Discovery APIs
  - Best Seller (Griffin View) — €1,699/month: unlimited results/month; up to 48-month history; Riskscan and Ctiscan categories; Export & Discovery APIs; OQLv2 full access
  - Enterprise (Griffin View ASM Edition) — €2,999/month: all of Best Seller plus customizable dashboards and on-demand scan APIs
- **Enterprise:** Unrated API option (no request-per-second cap) available by contacting Onyphe directly
- **Notes:** Attack surface discovery APIs are in BETA as of 2026-05-13 and expected to reach full production readiness in 2026.

## Authentication

Contact Onyphe at https://www.onyphe.io to purchase a plan and obtain an API key. Pass as `Authorization: apikey <KEY>` header on all requests.

## Endpoints

- **Base URL:** `https://www.onyphe.io/api/v2/`
- **Unrated base URL:** `https://www.onyphe.io/unrated/api/v2/`
- **Key endpoints:**
  - `GET /simple/datascan/{ip}` — datascan results for a specific IP address
  - `GET /summary/ip/{ip}` — comprehensive IP summary across all Onyphe data categories
  - `GET /summary/domain/{domain}` — domain summary
  - `GET /summary/hostname/{hostname}` — hostname summary
  - `POST /search/{query}` — search with OQLv2 query string; params: `page`
  - `POST /export/{query}` — bulk export matching OQLv2 query; streams results (Best Seller+ only)
  - `GET /user/me` — account info and plan details

**OQLv2 query examples:** `category:datascan port:554 protocol:rtsp country:SG`, `category:vulnscan cve.name:CVE-2024-1234 country:JP`, `category:datascan app.http.title:"DVR" os:Linux`

## Example call

```bash
curl -H "Authorization: apikey $ONYPHE_API_KEY" \
  "https://www.onyphe.io/api/v2/summary/ip/8.8.8.8"
```

```python
import requests

headers = {"Authorization": f"apikey {ONYPHE_API_KEY}"}

# Search for exposed maritime VSAT terminals
resp = requests.post(
    "https://www.onyphe.io/api/v2/search/category:datascan port:443 app.http.title:KVH",
    headers=headers,
    params={"page": 1},
)
for result in resp.json().get("results", []):
    print(result.get("ip"), result.get("port"), result.get("app", {}).get("http", {}).get("title"))

# IP summary
summary = requests.get(
    "https://www.onyphe.io/api/v2/summary/ip/192.0.2.1",
    headers=headers,
).json()
```

## Rate limits

Average 1 request/second across all standard plans. Exceeding the limit returns HTTP 429. The Unrated API option removes the per-second cap — contact Onyphe for access. No monthly result caps on Best Seller and Enterprise tiers.

## SDKs / Libraries

- **Official:** `onyphe-cli` (Go, official — GitHub: onyphe/cli)
- **Community:** `pyonyphe` (Python, third-party — GitHub: onyphe/pyonyphe); PowerShell module (`Use-Onyphe`)

## Documentation

- Main docs: https://www.onyphe.io/docs
- API search endpoint: https://www.onyphe.io/docs/apis/simple_best
- Pricing: https://www.onyphe.io/pricing
- CLI: https://github.com/onyphe/cli
- 2026 roadmap: https://blog.onyphe.io/en/retrospective-2025-and-roadmap-2026/

## Notes

- Onyphe's 48-month historical data depth is a key differentiator — no other major scanning platform offers this retention at API level, making it particularly valuable for forensic and trend analysis.
- OQLv2 (production-ready as of 2026) introduces search groups, advanced field logic, and improved performance over the v1 query language.
- Data categories: `datascan` (port/banner scan), `vulnscan` (CVE-correlated vulnerability data), `riskscan` (risk-scored exposure), `ctiscan` (CTI-enriched); higher categories require higher plan tiers.
- The on-demand scan API (Enterprise only) lets you request fresh scans of specific IP ranges rather than relying solely on the continuous scan index.
- Attack surface discovery APIs (BETA 2026): dedicated endpoints for ASM workflows — planned for full production release in 2026; contact Onyphe for early access.
- Pricing is in EUR; invoicing is available for organizations; academic/research discount inquiries can be directed to Onyphe directly.
