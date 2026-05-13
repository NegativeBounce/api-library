# Criminal IP

Korean cybersecurity intelligence search engine covering internet-exposed IP addresses, open ports, vulnerabilities, and domain infrastructure — with strong coverage of OT/IoT devices including maritime vessel systems, and STIX 2.1 export for threat intelligence integration.

**Tier:** Freemium
**Auth:** API Key
**Last researched:** 2026-05-13

## Use cases

- Querying exposed IP addresses for open ports, running services, detected CVEs, and connected domains in a single API call
- Identifying maritime vessel satellite terminal exposure by searching VSAT/maritime device banners and associated ASNs
- Integrating structured threat intelligence into SIEM/SOAR platforms via STIX 2.1 formatted asset exports

## Pricing

- **Free tier:** Limited credits on signup; no daily cap — credits consumed per query; sufficient for light research use
- **Paid tiers:**
  - Starter — individual monthly or annual subscription; significantly more credits; access to advanced filters
  - Enterprise — organizations; custom pricing, volume credits, SLA support
- **Enterprise:** Contact Criminal IP for custom pricing and academic/government rates
- **Notes:** Rate limiting is credit-based rather than time-based — no daily request cap; queries consume credits from your plan balance. Academic and government discounts available.

## Authentication

Register at https://www.criminalip.io and retrieve your API key from the My Information page. Pass as `x-api-key: <KEY>` header on all requests.

## Endpoints

- **Base URL:** `https://api.criminalip.io`
- **Key endpoints:**
  - `GET /v1/ip/data` — full IP report: open ports, detected services, connected domains, CVEs, VPN/proxy/scanner flags
  - `GET /v1/ip/summary` — condensed IP summary with risk score
  - `POST /v1/domain/scan` — initiate a domain scan; returns scan ID
  - `GET /v1/domain/status/{id}` — poll scan status and retrieve results
  - `GET /v1/banner/search` — search across all banners/service fingerprints
  - `GET /v1/asset/search` — broader asset search with advanced filters

**Common parameters:** `ip` (for IP endpoints), `query` (for search endpoints), `offset`, `limit`

## Example call

```bash
curl -H "x-api-key: $CIP_API_KEY" \
  "https://api.criminalip.io/v1/ip/data?ip=8.8.8.8"
```

```python
import requests

resp = requests.get(
    "https://api.criminalip.io/v1/ip/data",
    headers={"x-api-key": CIP_API_KEY},
    params={"ip": "8.8.8.8"},
)
data = resp.json()
print(data.get("ip"), data.get("score"), data.get("port"))

# Banner search for maritime VSAT terminals
resp = requests.get(
    "https://api.criminalip.io/v1/banner/search",
    headers={"x-api-key": CIP_API_KEY},
    params={"query": "KVH TracPhone", "offset": 0},
)
for result in resp.json().get("data", {}).get("result", []):
    print(result["ip_address"], result["open_port_no"], result["banner"])
```

## Rate limits

Credit-based — no fixed requests-per-minute cap. Each query deducts from your plan credit balance. Check remaining credits via the account dashboard. HTTP 402 is returned when credits are exhausted.

## SDKs / Libraries

- **Official:** None — REST API only
- **Community:** `criminalip-python` (Python, third-party CLI); CIP-NSE-Script (Nmap integration); STIX 2.1 data exports via `CriminalIP-data-STIX` (GitHub)

## Documentation

- Developer portal: https://www.criminalip.io/developer/api/get-ip-data
- API integrations: https://search.criminalip.io/developer/api-integrations
- STIX 2.1 data repo: https://github.com/criminalip/CriminalIP-data-STIX
- Pricing: https://www.criminalip.io/pricing

## Notes

- Criminal IP is developed by AI Spera (South Korea); the platform scans the global internet continuously and indexes results by IP, port, service, CVE, and geolocation.
- Strong coverage of OT/ICS and maritime systems — useful for finding exposed vessel management systems, VSAT terminals (KVH, Cobham, Intellian), and ship AIS/GMDSS equipment.
- Risk scoring (Critical/High/Medium/Low) is applied per IP based on CVE severity, scanning activity, and honeypot interactions — actionable for triage without custom scoring logic.
- STIX 2.1 export enables direct integration with threat intelligence platforms (TIPs) and ISACs.
- Integrates with Wazuh, Splunk, and other SIEM platforms via documented connectors.
- For comparison: Criminal IP has strong CVE correlation; Shodan has broader raw banner data; Censys has stronger certificate coverage.
