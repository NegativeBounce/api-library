# Claroty Platform (xDome)

OT/XIoT security platform providing asset management, vulnerability prioritization, and threat detection across industrial and connected environments — with a Swagger-based API Explorer and regional REST API endpoints for programmatic access to alerts, events, vulnerabilities, and asset inventory.

**Tier:** Enterprise
**Auth:** JWT (Bearer Token)
**Last researched:** 2026-05-13

## Use cases

- Pulling the full OT asset inventory from a port or terminal deployment into SIEM, CMDB, or custom dashboards via the REST API
- Retrieving active OT alerts and vulnerability data for automated triage and ticketing workflows in port security operations centers
- Integrating Claroty threat detection events with SOAR platforms (Cortex XSOAR, Splunk SOAR) to automate OT incident response playbooks

## Pricing

- **Free tier:** None — enterprise licensing only
- **Paid tiers:** Enterprise licensing; contact Claroty for pricing based on asset count and deployment model (on-premise or cloud-managed xDome)
- **Enterprise:** Custom pricing; contact https://claroty.com
- **Notes:** Claroty xDome is the cloud-managed variant of the Claroty platform; on-premise CTD (Continuous Threat Detection) deployments also support the same REST API.

## Authentication

Claroty uses JWT (JSON Web Token) authentication. Most API routes require a Bearer token. Obtain a token by authenticating against your Claroty instance:

```bash
POST https://api.claroty.com/api/v1/auth/token
Content-Type: application/json

{"username": "<user>", "password": "<password>"}
```

Include the returned token as `Authorization: Bearer <token>` header on all subsequent requests. Tokens have a fixed expiry; implement refresh logic in long-running integrations.

## Endpoints

- **US base URL:** `https://api.claroty.com`
- **EU base URL:** `https://eu.api.claroty.com`
- **Key endpoints:**
  - `GET /api/v1/alerts` — OT alerts and their affected device records
  - `GET /api/v1/events` — OT activity events related to industrial protocol operations
  - `GET /api/v1/vulnerabilities` — CVE-mapped vulnerabilities and their affected devices
  - `GET /api/v1/assets` — full OT/XIoT asset inventory
  - `POST /api/v1/auth/token` — obtain authentication JWT
- **API Explorer:** Swagger UI accessible within each Claroty deployment instance — auto-generates documentation from the live API, supports in-browser test calls and code generation

## Example call

```bash
# Authenticate
TOKEN=$(curl -s -X POST https://api.claroty.com/api/v1/auth/token \
  -H "Content-Type: application/json" \
  -d '{"username":"'$CLAROTY_USER'","password":"'$CLAROTY_PASS'"}' \
  | python3 -c "import sys,json; print(json.load(sys.stdin)['token'])")

# Fetch active alerts
curl -H "Authorization: Bearer $TOKEN" \
  "https://api.claroty.com/api/v1/alerts?status=active"
```

```python
import requests

# Authenticate
resp = requests.post(
    "https://api.claroty.com/api/v1/auth/token",
    json={"username": CLAROTY_USER, "password": CLAROTY_PASS},
)
token = resp.json()["token"]
headers = {"Authorization": f"Bearer {token}"}

# Get asset inventory
assets = requests.get("https://api.claroty.com/api/v1/assets", headers=headers).json()
for asset in assets.get("objects", []):
    print(asset.get("name"), asset.get("type"), asset.get("ip"))

# Get vulnerabilities
vulns = requests.get("https://api.claroty.com/api/v1/vulnerabilities", headers=headers).json()
for v in vulns.get("objects", []):
    print(v.get("cve_id"), v.get("cvss_score"), v.get("affected_assets_count"))
```

## Rate limits

Not publicly documented. Rate limits are configured per deployment and tier. The API Explorer within each instance may display current limit headers. Contact Claroty for specifics applicable to your license.

## SDKs / Libraries

- **Official:** None — REST API only; Swagger/OpenAPI spec available via built-in API Explorer
- **Community:** Elastic integration (`claroty_xdome` in Elastic integrations catalog); Rapid7 InsightIDR connector; Hunters.ai integration; Cortex XSOAR integration (Palo Alto Marketplace)

## Documentation

- API Explorer: accessible within your Claroty instance (Swagger UI)
- xDome Elastic integration: https://www.elastic.co/docs/reference/integrations/claroty_xdome
- Rapid7 InsightIDR integration: https://docs.rapid7.com/insightidr/claroty-xdome/
- Integrations overview: https://claroty.com/platform/integrations
- API Explorer blog: https://claroty.com/blog/product-feature-spotlight-api-explorer

## Notes

- Claroty xDome supports both OT (industrial protocols: Modbus, DNP3, EtherNet/IP, PROFINET, S7) and XIoT (extended IoT including building management, physical security) asset types — relevant for the converged IT/OT/IoT environment of a modern smart port.
- The API Explorer (Swagger) is particularly useful for initial integration development — it allows testing queries directly against the live deployment without writing code first.
- Claroty's vulnerability data correlates detected software versions against the NVD CVE database and ICS-specific advisory sources including CISA ICS advisories (`cisa-ics-advisories.md`).
- For US and EU deployments, use the correct regional base URL — cross-region requests may return 403 errors.
- Claroty integrates natively with ServiceNow (for ticketing), CrowdStrike (for IT/OT correlated response), and Microsoft Sentinel (for SIEM) — the API complements these for custom integrations.
- The on-premise CTD variant uses a local instance URL (e.g., `https://<claroty-appliance>/`) rather than the cloud regional URLs above.
