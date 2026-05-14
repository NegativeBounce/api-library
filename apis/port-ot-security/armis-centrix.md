# Armis Centrix

Agentless asset intelligence platform covering IT, OT, IoT, and IoMT devices — providing real-time visibility, risk scoring, and threat detection across all connected assets without requiring agents or network changes, with a developer portal launched February 2026.

**Tier:** Enterprise
**Auth:** API Key (v1) / OAuth 2.0 Client Credentials (v3)
**Last researched:** 2026-05-13

## Use cases

- Discovering and inventorying all OT/IoT devices across port infrastructure — including PLCs, HMIs, sensors, cranes, and gate systems — without deploying agents
- Enriching SIEM and SOAR platforms with real-time OT asset context, risk scores, and vulnerability data via the REST API
- Integrating Armis asset intelligence into custom dashboards and operational workflows for port security operations centers

## Pricing

- **Free tier:** None — enterprise licensing only
- **Paid tiers:** Enterprise licensing; contact Armis for pricing based on asset count and deployment scale
- **Enterprise:** Custom pricing; contact https://www.armis.com
- **Notes:** Armis launched a dedicated developer portal in February 2026, positioning the API as a primary integration path for security teams and technology partners.

## Authentication

**API v1:** Obtain an API key from your Armis account. Pass as `x-api-key: <KEY>` header on all v1 requests.

**API v3 (recommended — new developer portal):** OAuth 2.0 client credentials flow. Obtain Client ID, Client Secret, and Vendor ID from the developer portal at https://dev.armis.com. Exchange for an access token:

```bash
POST https://api.armis.com/v3/oauth/token
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&client_id=<CLIENT_ID>&client_secret=<CLIENT_SECRET>&vendor_id=<VENDOR_ID>&scope=<SCOPES>
```

Include the returned access token as `Authorization: Bearer <token>` on subsequent requests.

## Endpoints

- **Base URL v1:** `https://ic.armis.com/api/v1/`
- **Base URL v3:** `https://api.armis.com/v3/`
- **Token endpoint:** `https://api.armis.com/v3/oauth/token`
- **Key endpoints:**
  - `GET /device/_search` — search and filter the full device/asset inventory (v1)
  - `GET /alerts/` — active and historical alert data
  - `GET /vulnerabilities/` — CVE-mapped vulnerability data per asset
  - `GET /networks/` — network segment and traffic data
  - `POST /v3/oauth/token` — obtain OAuth 2.0 access token (v3)
- Full endpoint reference: available at https://dev.armis.com/reference

## Example call

```bash
# v1: search for OT assets
curl -H "x-api-key: $ARMIS_API_KEY" \
  "https://ic.armis.com/api/v1/device/_search?assetType=OT"
```

```python
import requests

# v3: obtain token
token_resp = requests.post(
    "https://api.armis.com/v3/oauth/token",
    data={
        "grant_type": "client_credentials",
        "client_id": ARMIS_CLIENT_ID,
        "client_secret": ARMIS_CLIENT_SECRET,
        "vendor_id": ARMIS_VENDOR_ID,
        "scope": "devices:read alerts:read",
    },
)
token = token_resp.json()["access_token"]

# use token on v3 endpoints
devices = requests.get(
    "https://api.armis.com/v3/devices/",
    headers={"Authorization": f"Bearer {token}"},
).json()
for device in devices.get("data", {}).get("devices", []):
    print(device.get("name"), device.get("type"), device.get("riskLevel"))
```

## Rate limits

Not publicly documented. Contact Armis for rate limit details applicable to your license tier. The developer portal (https://dev.armis.com) includes best practices guidance for high-volume integrations.

## SDKs / Libraries

- **Official:** `armis-sdk-python` (Python, GitHub: ArmisSecurity/armis-sdk-python)
- **Community:** Elastic integration (`armis` integration in Elastic integrations catalog); Sumo Logic cloud-to-cloud integration; Axonius connector

## Documentation

- Developer portal: https://dev.armis.com/
- Authentication docs: https://docs.ic.armis.com/docs/documentation_authentication
- API FAQ (v3 upgrade): https://dev.armis.com/docs/faq
- Python SDK: https://github.com/ArmisSecurity/armis-sdk-python
- Integrations: https://www.armis.com/platform/integrations/

## Notes

- Armis uses passive network traffic analysis (no agents, no active scanning) — critical for OT environments where active scanning can disrupt PLCs, RTUs, and safety systems.
- Coverage extends to all asset types: IT (servers, workstations), OT (PLCs, HMIs, SCADA), IoT (cameras, badge readers, HVAC), and IoMT (medical devices) — relevant for ports with converged IT/OT security programs.
- The v3 API (developer portal, February 2026) is the recommended integration path; v1 API key authentication remains supported but is the legacy path.
- Armis Centrix integrates with SIEM platforms (Splunk, QRadar, Microsoft Sentinel), SOAR platforms, and CMDBs (ServiceNow) out of the box — API complements these for custom integrations.
- For port OT specifically: Armis can fingerprint industrial Ethernet devices, maritime communication equipment, and cargo handling systems without requiring OT-side configuration changes.
