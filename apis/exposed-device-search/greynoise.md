# GreyNoise

Internet background noise intelligence platform that continuously scans the internet and classifies IPs as benign scanners, malicious actors, or unknown — helping analysts distinguish real threats from automated noise in logs and alert feeds.

**Tier:** Freemium
**Auth:** API Key
**Last researched:** 2026-05-13

## Use cases

- Enriching firewall and IDS logs by checking whether an IP is a known internet scanner (benign research, CDN, search engine) vs. a malicious actor
- Searching the NOISE dataset with GNQL (GreyNoise Query Language) to find all IPs scanning for a specific port or vulnerability across the internet
- Bulk-classifying large IP lists (up to 10,000 IPs per request) to triage alerts and reduce false positives in security operations

## Pricing

- **Free tier:** Community API — basic IP lookup with limited metadata; free with account registration
- **Paid tiers:** Enterprise — full IP context, GNQL search, IP Similarity, IP Timeline, batch multi-lookup; contact GreyNoise for pricing
- **Enterprise:** On-Premise API available for air-gapped environments; contact GreyNoise
- **Notes:** The Community API provides a subset of metadata sufficient for basic triage; GNQL and advanced context require Enterprise subscription.

## Authentication

Register at https://www.greynoise.io to obtain a free Community API key. Pass as `key: <KEY>` header on all requests. Enterprise keys use the same header but unlock additional endpoints.

## Endpoints

- **Base URL:** `https://api.greynoise.io`
- **Key endpoints:**
  - `GET /v3/community/{ip}` — Community tier: basic IP classification (noise/riot/unknown) with limited metadata
  - `GET /v3/noise/context/{ip}` — Enterprise: full IP context (tags, CVEs, geo, ASN, scan behavior, classification)
  - `POST /v3/noise/multi/context` — Enterprise: batch context lookup; JSON body with `ips` array (up to 10,000)
  - `GET /v3/noise/quick/{ip}` — quick noise/riot check (is this IP known to GreyNoise?)
  - `POST /v3/noise/multi/quick` — batch quick check for up to 10,000 IPs
  - `GET /v3/experimental/gnql` — Enterprise: GNQL query search across the NOISE dataset; params: `query`, `size` (up to 10,000/page), `scroll` (pagination token)
  - `GET /v3/meta/metadata` — tag and classification metadata

**GNQL query examples:** `tags:CVE-2024-1234`, `classification:malicious AND destination_port:23`, `metadata.country_code:CN AND last_seen:1d`

## Example call

```bash
# Community: check single IP
curl -H "key: $GN_API_KEY" \
  "https://api.greynoise.io/v3/community/198.20.69.74"

# Enterprise: batch check 10,000 IPs
curl -X POST -H "key: $GN_API_KEY" -H "Content-Type: application/json" \
  -d '{"ips": ["1.2.3.4", "5.6.7.8"]}' \
  "https://api.greynoise.io/v3/noise/multi/quick"
```

```python
import greynoise

client = greynoise.GreyNoise(api_key=GN_API_KEY)

# Single IP context (Enterprise)
result = client.ip("198.20.69.74")
print(result["classification"], result.get("tags"))

# GNQL search (Enterprise)
for ip in client.query("tags:MIRAI AND destination_port:23"):
    print(ip["ip"], ip["classification"])
```

## Rate limits

Community API: limited; specific limits not publicly documented. Enterprise: higher limits with "more API requests per minute" — contact GreyNoise for exact values. Batch endpoints accept up to 10,000 IPs per POST; GNQL returns up to 10,000 results per page with scroll-based pagination.

## SDKs / Libraries

- **Official:** `greynoise` (Python, PyPI); `greynoise-cli` (command-line tool)
- **Community:** Splunk app; Cortex XSOAR integration; Palo Alto Cortex Marketplace package

## Documentation

- API docs: https://docs.greynoise.io/docs/using-the-greynoise-api
- GNQL reference: https://docs.greynoise.io/docs/gnql
- Community vs Enterprise features: https://www.greynoise.io/features/product-feature-api
- GitHub: https://github.com/GreyNoise-Intelligence/api.greynoise.io

## Notes

- GreyNoise's primary value is noise reduction: roughly 10–25% of IPs hitting internet-facing services are known benign scanners (Shodan, Censys, security researchers) — GreyNoise filters these out so analysts focus on real threats.
- The `riot` classification identifies IPs belonging to known benign services (Google, Cloudflare, AWS) that would otherwise trigger alerts.
- Tags identify specific behavior: `MIRAI`, `MASSCAN`, `CVE-XXXX-XXXX` exploitation attempts, `RDPSCAN`, etc. — useful for quickly assessing whether observed scanning is targeted or opportunistic.
- For maritime WiFi exposure research, combine GreyNoise with Shodan: use Shodan to find exposed vessel networks, then run those IPs through GreyNoise to see if they're already being actively scanned by threat actors.
- GreyNoise data freshness: IPs are marked as seen within the last 90 days by default; `last_seen` filters allow restricting to recent activity.
