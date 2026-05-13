# LeakIX

Internet scanning platform focused on exposed services and data leaks — indexes misconfigured databases, open file shares, exposed admin panels, and RCE-vulnerable services, surfacing results that other scanners may classify but not highlight as severe.

**Tier:** Freemium
**Auth:** API Key
**Last researched:** 2026-05-13

## Use cases

- Finding exposed databases (Elasticsearch, MongoDB, Redis) and open file shares (SMB, FTP) on internet-facing hosts with no authentication
- Identifying hosts running services with known RCE vulnerabilities using LeakIX's plugin-based severity classification
- Monitoring specific IP ranges or domains for newly exposed services via alert channels with webhook delivery

## Pricing

- **Free tier:** €0/month — 3,000 API requests/month; 15-day delay on results (new exposures not visible immediately); community support only
- **Paid tiers:**
  - Bounty Hunter — €25/month: 100,000 API requests/month; 0-day results (immediate access); RCE and Critical vulnerability plugins; 1 alert channel across 25 monitored resources; result download (1,000 max)
  - Enterprise — €350/month: 100,000 API requests/month; 0-day results; 5 alert channels across 100 resources; result download (50,000 max); direct chat support; commercial use rights
- **Enterprise:** Custom data-sharing arrangements available for research or platform integration upon request
- **Notes:** Free tier is suitable for ad-hoc research; the 15-day delay makes it unsuitable for real-time monitoring. RCE and critical plugins only unlock at Bounty Hunter tier and above.

## Authentication

Register at https://leakix.net to obtain a free API key. Pass as `api-key: <KEY>` header. Include `Accept: application/json` header to receive JSON responses (default is HTML).

## Endpoints

- **Base URL:** `https://leakix.net`
- **Key endpoints:**
  - `GET /search` — search the LeakIX index; params: `q` (query string), `page`, `scope` (`leak` for data leaks, `service` for service exposures)
  - `GET /host/{ip}` — all LeakIX data for a specific IP address
  - `GET /domain/{domain}` — domain-level exposure data
  - `GET /api/subdomains/{domain}` — subdomain enumeration from LeakIX scan data
  - `GET /bulk/search` — multiple searches in one request
  - `GET /api/plugins` — list available LeakIX plugins and their severity classifications
  - `GET /api/plugins/{name}` — details for a specific plugin

**Query syntax examples:** `leak.type:ElasticSearch country:DE`, `service.software.name:Apache port:8080`, `leak.severity:critical`

## Example call

```bash
curl -H "api-key: $LEAKIX_API_KEY" \
     -H "Accept: application/json" \
     "https://leakix.net/search?q=leak.type%3AElasticSearch+country%3ASG&scope=leak"
```

```python
import requests

resp = requests.get(
    "https://leakix.net/search",
    headers={"api-key": LEAKIX_API_KEY, "Accept": "application/json"},
    params={"q": "service.software.name:nginx port:443 country:NG", "scope": "service"},
)
for result in resp.json():
    print(result.get("ip"), result.get("port"), result.get("summary"))

# Host lookup
host = requests.get(
    "https://leakix.net/host/192.168.1.1",
    headers={"api-key": LEAKIX_API_KEY, "Accept": "application/json"},
).json()
```

## Rate limits

1 request/second across all plans. Exceeding the limit returns HTTP 429 with an `x-limited-for` header specifying the wait duration in seconds. Free tier: 3,000 requests/month hard cap.

## SDKs / Libraries

- **Official:** None — REST API only
- **Community:** `LeakPy` (Python, PyPI — unofficial client by Chocapikk); `synapse-leakix` (Synapse threat intelligence integration)

## Documentation

- API reference: https://docs.leakix.net/docs/api/
- Search query fields: https://docs.leakix.net/docs/query/fields/
- Pricing: https://leakix.net/plans
- Blog (scan coverage reports): https://blog.leakix.net/

## Notes

- LeakIX is distinct from Shodan and Censys in that it emphasizes severity — results include a `severity` field (critical, high, medium, low, info) based on what the exposed service reveals or allows.
- RCE-tagged results (Bounty Hunter+ tier) identify services actively exploitable for remote code execution — the most operationally significant exposure type.
- Useful for maritime security research: query for exposed vessel management system panels, maritime-specific software (ECDIS, VDR admin interfaces), or VSAT terminal admin panels by banner or title.
- The 15-day delay on the free tier means results reflect the state of the internet from two weeks ago — not suitable for active incident response.
- LeakIX publishes regular blog posts on their scan coverage and newly discovered exposure categories, updated into 2026.
- Plugin architecture means new exposure types are added regularly — check `/api/plugins` for the current list before building automated monitoring.
