# FOFA

Chinese cyberspace mapping search engine by Baimaohui (FOFA Team) providing internet asset discovery, fingerprinting, and aggregation — with particularly strong coverage of Asian infrastructure, industrial systems, maritime equipment, and OT/SCADA devices.

**Tier:** Freemium
**Auth:** Email + API Key (query parameters)
**Last researched:** 2026-05-13

## Use cases

- Searching internet-exposed assets by service banner, certificate, icon hash, or body content to find open cameras, wireless access points, and VSAT terminals
- Discovering maritime vessel WiFi and management systems exposed on the open internet using FOFA-specific fingerprints for vessel equipment manufacturers
- Bulk harvesting of asset data using the Search After API for large-scale internet mapping and OT/IoT exposure analysis

## Pricing

- **Free tier:** Registered account with very limited API access; most fields and commercial use restricted
- **Paid tiers:** F-points based — purchase F-points at approximately $6 per 10,000 F-points; many API fields and higher result limits require subscription
- **Enterprise:** Commercial subscription required for API commercial use; contact FOFA for enterprise pricing
- **Notes:** The free tier is heavily restricted — banner, cert, body, and header fields require paid F-points or subscription. Registration requires a Chinese phone number or invitation in some configurations; international users may use the English portal at `en.fofa.info`.

## Authentication

Register at https://en.fofa.info and retrieve your API key from your profile page. Pass as query parameters: `email=<your@email.com>&key=<API_KEY>`. Alternatively accepted as `Authorization: Basic base64(email:key)` header in some implementations.

## Endpoints

- **Base URL:** `https://fofa.info/api/v1/`
- **Key endpoints:**
  - `GET /search/all` — search assets; params: `qbase64` (Base64-encoded query), `fields` (comma-separated), `page`, `size` (max 2000/page for banner/cert; max 500/page for body), `full` (include expired data)
  - `GET /info/my` — account info and remaining F-points balance
  - `POST /api/batches_pages` — batch search across multiple queries
  - `GET /api/v1/host/{host}` — HOST aggregation: ports, protocols, services for a specific IP/domain
  - Statistics aggregation endpoint for field-level counts

**FOFA query syntax examples:** `app="Apache" && country="JP"`, `banner="220" && port="21" && protocol="ftp"`, `icon_hash="-247388890"` (icon fingerprint), `cert="*.example.com"`

## Example call

```bash
import base64
QUERY = 'app="Hikvision-Cameras" && country="SG"'
Q_B64 = base64.b64encode(QUERY.encode()).decode()

curl "https://fofa.info/api/v1/search/all?email=$FOFA_EMAIL&key=$FOFA_KEY&qbase64=$Q_B64&fields=ip,port,host,title&size=100"
```

```python
import requests, base64

query = 'app="KVH" && protocol="http"'
resp = requests.get(
    "https://fofa.info/api/v1/search/all",
    params={
        "email": FOFA_EMAIL,
        "key": FOFA_KEY,
        "qbase64": base64.b64encode(query.encode()).decode(),
        "fields": "ip,port,host,title,country",
        "size": 100,
    },
)
data = resp.json()
for result in data.get("results", []):
    print(result)
```

## Rate limits

Default query rate: 2 requests/second. Maximum results per page: 2,000 (banner/cert/header queries), 500 (body queries). The Search After API (`search_next`) supports continuous pagination for up to 10 million records per request.

## SDKs / Libraries

- **Official:** `GoFOFA` (Go, by FofaInfo on GitHub); community Python SDK `fofa-py` (by fofapro)
- **Community:** `fofa_viewer` (Java GUI); integrations in ProjectDiscovery's `subfinder` and `nuclei` tools

## Documentation

- API overview: https://en.fofa.info/api
- API tools: https://en.fofa.info/api_tools
- Python SDK: https://github.com/fofapro/fofa-py
- GoFOFA CLI: https://github.com/FofaInfo/GoFOFA

## Notes

- FOFA's `app=` filter searches by application/framework fingerprint — FOFA maintains a large fingerprint library covering thousands of software products including maritime and industrial systems.
- Icon hash search (`icon_hash=`) is powerful for finding all instances of a specific web interface (e.g., a VSAT terminal management panel) even when banners vary.
- Useful maritime queries: `app="Sailor Cobham" && port="80"`, `title="Fleet One" && protocol="http"`, `banner="Intellian" && country="CN"`.
- FOFA has better coverage of Chinese and APAC infrastructure than Shodan or Censys — important for South China Sea and Southeast Asian maritime exposure research.
- Commercial use of the API or scraped data without a paid subscription violates FOFA's terms of service.
- The English portal (`en.fofa.info`) mirrors the Chinese platform; query syntax is identical; F-point balance applies across both.
