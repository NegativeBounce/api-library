# Censys Search API

Internet-wide scanning platform covering IPv4/IPv6 hosts and TLS certificates, with strong query language support for finding exposed services, open cameras, and misconfigured devices across global infrastructure.

**Tier:** Freemium
**Auth:** HTTP Basic Auth (API ID + Secret)
**Last researched:** 2026-05-13

## Use cases

- Searching internet-wide scan data to identify exposed services, open ports, and misconfigured devices by IP range, ASN, or geographic region
- Querying TLS certificate data to discover hosts presenting specific certificates, expired certs, or self-signed certificates on maritime vessel networks
- Tracking historical host configuration changes to detect when exposed services appear or disappear on monitored IP ranges

## Pricing

- **Free tier:** Starter plan for individuals — limited query credits; 5 credits per 100-result page
- **Paid tiers:**
  - Enterprise — higher credit allocation, 1 credit per 100-result page; contact Censys for pricing
  - Government — tailored for government use cases; contact Censys for pricing
- **Enterprise:** Custom pricing; contact Censys
- **Notes:** Credits are consumed per search page; view-only endpoints (single host lookup by IP) consume fewer credits. The Platform API (v3) provides enterprise attack surface management features under a separate tier.

## Authentication

Register at https://search.censys.io and retrieve your API ID and secret from your account page at https://search.censys.io/account/api. Pass as HTTP Basic Auth: `Authorization: Basic base64(API_ID:SECRET)`.

## Endpoints

- **Search API base URL:** `https://search.censys.io/api/`
- **Platform API base URL:** `https://api.platform.censys.io/v3/`
- **Key endpoints (Search API v2):**
  - `GET /v2/hosts/search` — search hosts using Censys Search Language; params: `q`, `per_page` (max 100), `cursor`, `fields`
  - `GET /v2/hosts/{ip}` — full host record for a single IP
  - `GET /v2/hosts/{ip}/diff` — compare host configurations between two points in time
  - `GET /v2/hosts/{ip}/events` — host change history
  - `GET /v2/hosts/{ip}/names` — DNS names associated with a host
  - `GET /v2/hosts/aggregate` — field-value frequency aggregation across the dataset
  - `GET /v2/certificates/search` — certificate search by query
  - `GET /v2/certificates/{fingerprint}` — single certificate by SHA-256 fingerprint
  - `GET /v2/certificates/{fingerprint}/hosts` — hosts presenting this certificate

**Censys Search Language examples:** `services.port=22 and location.country_code=JP`, `services.http.response.headers.server="Apache" and not labels=CDN`

## Example call

```bash
curl -u "$CENSYS_API_ID:$CENSYS_API_SECRET" \
  "https://search.censys.io/api/v2/hosts/search?q=services.port%3D554+and+services.service_name%3DRTSP&per_page=25"
```

```python
import requests
from requests.auth import HTTPBasicAuth

resp = requests.get(
    "https://search.censys.io/api/v2/hosts/search",
    auth=HTTPBasicAuth(CENSYS_API_ID, CENSYS_API_SECRET),
    params={"q": "services.port=554 and services.service_name=RTSP", "per_page": 25},
)
for host in resp.json().get("result", {}).get("hits", []):
    print(host["ip"], host.get("services"))
```

## Rate limits

Determined by account tier. Credits are consumed per search page (Starter: 5 credits/page; Enterprise: 1 credit/page). Rate limits are displayed on the account API page alongside credentials. Exceed limits and requests return HTTP 429.

## SDKs / Libraries

- **Official:** `censys` (Python, PyPI); `censys-cli` (command-line tool)
- **Community:** Go client (`censys-go`); various community wrappers

## Documentation

- Search API docs: https://docs.censys.com/docs/ls-api
- Platform API docs: https://docs.censys.com/docs/platform-api-transition-guide
- Censys Search Language reference: https://search.censys.io/search/language
- Credit system: https://docs.censys.com/docs/censys-credits

## Notes

- Censys scans the entire IPv4 address space and significant IPv6 ranges; data refreshed continuously with full re-scans on a regular cycle.
- Useful Censys dorks for exposed devices: `services.port=554` (RTSP cameras), `services.port=37777` (Dahua cameras), `services.http.response.html_title="DVR Web Client"`.
- For maritime WiFi/VSAT exposure: search for KVH, Intellian, or Cobham VSAT terminal banners: `services.http.response.body="KVH" and services.port=80`.
- The Platform API (v3) adds adversary investigation, threat hunting, and attack surface management endpoints — separate from the Search API and targeted at enterprise security teams.
- The legacy Search API (v2) and Platform API (v3) coexist; Censys recommends migrating to Platform API for new integrations.
- Certificates endpoint is particularly useful for identifying all hosts sharing a certificate — common in corporate VPN infrastructure and maritime satellite terminals.
