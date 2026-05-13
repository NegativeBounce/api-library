# ZoomEye

Chinese internet asset discovery search engine by Knownsec 404 Team — providing device and web component search across global internet infrastructure with strong coverage of Asian networks, IoT devices, industrial systems, and maritime equipment.

**Tier:** Freemium
**Auth:** API Key
**Last researched:** 2026-05-13

## Use cases

- Searching internet-exposed devices and services across Chinese, APAC, and global infrastructure using ZoomEye dork queries for IoT devices, cameras, and vessel systems
- Discovering web components (frameworks, CMS, exposed admin panels) by technology fingerprint to map attack surfaces across maritime operator infrastructure
- Querying device/service exposure data for specific IP ranges, ASNs, or geographic regions to supplement Shodan/Censys with better APAC coverage

## Pricing

- **Free tier:** Registered account with limited monthly search quota; results cached locally for 5 days to conserve quota; sufficient for light research
- **Paid tiers:** Multiple subscription tiers with higher result quotas; pricing not publicly listed — check https://www.zoomeye.ai/pricing for current plans
- **Enterprise:** Contact ZoomEye/Knownsec for high-volume and commercial licensing
- **Notes:** ZoomEye recently upgraded to API-2024V2 with support for custom fields, Base64-encoded queries, and improved pagination. The platform migrated its primary domain from `zoomeye.org` to `zoomeye.ai` — both remain active.

## Authentication

Register at https://www.zoomeye.ai and retrieve your API key from your profile page. Pass as `API-KEY: <KEY>` header on all requests. Username/password authentication is also supported via `POST /user/login` which returns a JWT token.

## Endpoints

- **Base URL:** `https://api.zoomeye.org`
- **Key endpoints:**
  - `GET /host/search` — search internet-connected devices and services; params: `query` (ZoomEye dork), `page`, `pagesize` (max 20/page default), `facets`, `fields` (custom field selection, API-2024V2)
  - `GET /web/search` — search web components and frameworks; params: `query`, `page`
  - `GET /user/info` — account info including remaining search quota
  - `POST /user/login` — authenticate with email/password; returns JWT access token (alternative to API-KEY header)

**ZoomEye dork examples:** `app:"Hikvision IP Camera" country:"JP"`, `app:"D-Link Router" port:80`, `app:"OpenSSH" os:"RouterOS"`, `"KVH" port:443 country:"SG"`, `title:"DVR Login" country:"CN"`

## Example call

```bash
curl -H "API-KEY: $ZOOMEYE_API_KEY" \
  "https://api.zoomeye.org/host/search?query=app%3A%22Hikvision+IP+Camera%22+country%3A%22SG%22&page=1"
```

```python
import requests, base64

headers = {"API-KEY": ZOOMEYE_API_KEY}

# Device/host search
resp = requests.get(
    "https://api.zoomeye.org/host/search",
    headers=headers,
    params={"query": 'app:"KVH" port:80', "page": 1, "pagesize": 20},
)
data = resp.json()
print(f"Total: {data.get('total')}")
for match in data.get("matches", []):
    print(match.get("ip"), match.get("portinfo", {}).get("port"), match.get("geoinfo", {}).get("country", {}).get("names", {}).get("en"))

# Check remaining quota
info = requests.get("https://api.zoomeye.org/user/info", headers=headers).json()
print(f"Quota remaining: {info.get('resources', {}).get('search-free', 'N/A')}")
```

## Rate limits

Quota-based per account plan — quota tracked against the monthly search allocation. Results queried are cached locally (by the official SDK) for 5 days to reduce quota consumption. Specific per-minute rate limits are not publicly documented. HTTP 403 or quota-related error returned when monthly allocation is exhausted.

## SDKs / Libraries

- **Official:** `zoomeye` (Python, PyPI — by Knownsec 404 Team); `zoomeye-sdk` (updated SDK on PyPI); MCP server (`mcp_zoomeye` on GitHub for LLM integration)
- **Community:** Various Go and Ruby implementations; integration in ProjectDiscovery tools

## Documentation

- API v2 reference: https://www.zoomeye.ai/doc
- Python SDK: https://github.com/knownsec/ZoomEye-python
- MCP server: https://github.com/zoomeye-ai/mcp_zoomeye
- API-2024V2 upgrade guide: available via the ZoomEye developer portal

## Notes

- ZoomEye has significantly better coverage of Chinese domestic IP space than Shodan or Censys — essential for research involving Chinese-flagged vessels, port infrastructure, or Chinese-manufactured maritime equipment.
- The `app=` filter searches by application fingerprint from ZoomEye's fingerprint library — covering routers, cameras, SCADA systems, and maritime equipment by vendor and model.
- Useful for identifying Dahua/Hikvision cameras and maritime navigation systems exposed in Chinese and APAC waters that may not appear in Western scanning platforms.
- ZoomEye data freshness: continuous scanning; freshness varies by target region and port — APAC coverage is generally more current than on competing platforms.
- The API-2024V2 upgrade added custom field selection (`fields` parameter), reducing response payload size for bulk queries — important for high-volume searches within quota limits.
- For broader global coverage, use ZoomEye alongside Shodan (global coverage) and FOFA (Chinese/industrial fingerprint depth); the three platforms have complementary but overlapping datasets.
