# Netlas

Modern internet-wide scanning platform with CVE tagging, TOR/VPN detection, domain intelligence, and a private scanner — providing structured search and bulk download APIs for attack surface discovery and exposure research.

**Tier:** Freemium
**Auth:** Bearer Token (API Key)
**Last researched:** 2026-05-13

## Use cases

- Searching internet scan data with CVE filter support to identify hosts running services with known vulnerabilities by region or ASN
- Bulk-downloading large datasets of scan results without pagination limits for offline analysis and maritime network exposure mapping
- Running private scans against specified IP ranges using Netlas's on-platform scanner to retrieve fresh data beyond the continuous scan index

## Pricing

- **Free tier:** Community — 50 requests/day; 2,500 results/month; internet scan data + DNS/IP WHOIS; Attack Surface Discovery (20 nodes/group, 100 nodes/surface)
- **Paid tiers:**
  - Freelancer — $49/month ($40.83/mo annually): 1,000 req/day; 1M results/month; domain WHOIS, SSL certificates, private scanner (512 targets/scan)
  - Business — $249/month ($207.50/mo annually): 10,000 req/day; 25M results/month; CVE search + advanced filters; TOR/VPN detection; threat intelligence; 1K node groups; 4,096 target scans
  - Corporate — $830/month (annual billing; 5 API keys): unlimited requests; 100M results/month; 10K node groups; 32,768 target scans; priority support
  - Enterprise — custom pricing: unlimited requests and results; 100K node groups; 65,536 target scans; custom rate limits
- **Notes:** CVE filter requires Business plan or above. Free tier daily limit resets at midnight UTC.

## Authentication

Register at https://app.netlas.io and retrieve your API key from the profile page at https://app.netlas.io/profile/. Pass as Bearer token: `Authorization: Bearer <API_KEY>`. The legacy `X-API-Key` header is still supported but deprecated.

## Endpoints

- **Base URL:** `https://app.netlas.io/api/`
- **Key endpoints:**
  - `GET /host/{host}/` — aggregated data for an IP address or domain; combines all Netlas data collections in one response
  - `GET /responses/` — search internet scan responses; params: `q` (query string), `fields`, `source_type`, `start`, `indices`
  - `POST /responses/download/` — bulk download scan results without pagination limit (returns NDJSON stream)
  - `GET /domains/` — domain search; params: `q`, `fields`, `start`
  - `GET /whois_ip/` — IP WHOIS lookup
  - `GET /certs/` — TLS certificate search; params: `q`, `fields`, `start`
  - `GET /scanner/` — list private scans
  - `POST /scanner/` — create a new private scan; body: `target` (IP/CIDR), `ports`, `protocols`
  - `PATCH /scanner/{id}/` — update scan; `DELETE /scanner/{id}/` — cancel scan

**Netlas query syntax examples:** `protocol:http AND port:8080 AND geo.country:JP`, `cve.name:CVE-2021-44228 AND tag:iot`, `certificate.subject.organization:KVH*`

## Example call

```bash
curl -H "Authorization: Bearer $NETLAS_API_KEY" \
  "https://app.netlas.io/api/responses/?q=protocol%3Artsp+AND+geo.country%3ASG&fields=ip%2Cport%2Cprotocol%2Cbanner"
```

```python
import requests

headers = {"Authorization": f"Bearer {NETLAS_API_KEY}"}

# Search for exposed RTSP cameras in Singapore
resp = requests.get(
    "https://app.netlas.io/api/responses/",
    headers=headers,
    params={"q": "protocol:rtsp AND geo.country:SG", "fields": "ip,port,protocol,banner"},
)
for hit in resp.json().get("items", []):
    print(hit["data"]["ip"], hit["data"]["port"], hit["data"].get("banner", "")[:80])

# Host summary
host = requests.get(
    "https://app.netlas.io/api/host/192.0.2.1/",
    headers=headers,
).json()
```

## Rate limits

| Tier | Requests/Minute | Requests/Day |
|---|---|---|
| Free | 60 | 50 |
| Freelancer | 60 | 1,000 |
| Business | 60 | 10,000 |
| Corporate | 60 | Unlimited |

Certificate search: 3 requests/minute across all tiers. HTTP 429 returned on breach with `Retry-After` header. Search results capped at 10,000 via paginated endpoints; use `/responses/download/` for unlimited bulk retrieval.

## SDKs / Libraries

- **Official:** None — REST API only
- **Community:** Netlas Cookbook (Python examples repo, GitHub); integration examples in project documentation

## Documentation

- API reference: https://docs.netlas.io/api-reference/
- Query syntax: https://docs.netlas.io/
- Pricing: https://netlas.io/pricing/
- Cookbook: https://netlas.io/resources/cookbook/

## Notes

- Netlas indexes HTTP/HTTPS, FTP, SSH, Telnet, RTSP, MQTT, Modbus, and other protocols — protocol diversity makes it well-suited for OT/IoT and maritime device discovery.
- CVE tagging (Business plan+) maps observed service versions to known vulnerabilities — find all internet-exposed hosts running a specific vulnerable version without post-processing.
- TOR/VPN detection (Business plan+) flags whether an IP is a TOR exit node or known VPN endpoint — useful for contextualizing suspicious scan sources observed on vessel networks.
- The private scanner lets you run fresh scans against specific CIDR ranges — useful when the continuous scan index may not have recent data for a target range.
- For maritime research: `certificate.subject.organization:KVH* OR certificate.subject.organization:Cobham*` finds exposed satellite terminal web interfaces by their TLS certificate organization field.
- Netlas data freshness: continuous scanning with most protocols re-scanned within days; certificate data may lag by 1–2 weeks.
