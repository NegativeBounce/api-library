# Dragos Platform

OT-native threat detection and ICS-specific threat intelligence platform — providing asset visibility, detection of ICS-targeted attack techniques, and weekly Knowledge Pack updates with threat group tracking relevant to port and maritime critical infrastructure.

**Tier:** Enterprise
**Auth:** API Key / OAuth 2.0 Bearer JWT
**Last researched:** 2026-05-13

## Use cases

- Retrieving OT asset inventory, active detections, and vulnerability data from Dragos deployments via API for integration with port SOC workflows and ticketing systems
- Accessing the Dragos WorldView threat intelligence API to pull ICS-specific threat group profiles, IOCs, and TTPs relevant to maritime and port infrastructure
- Automating alert triage by querying detection data with least-privilege API credentials scoped to only the required data types

## Pricing

- **Free tier:** None — enterprise licensing only
- **Paid tiers:** Enterprise licensing; contact Dragos for pricing based on site count and asset scale
- **Enterprise:** Custom pricing; contact https://www.dragos.com
- **Notes:** Dragos Platform is purpose-built for OT environments and is delivered as an appliance or virtual machine deployed in the OT network. WorldView threat intelligence is a separate subscription.

## Authentication

Two authentication methods are supported; OAuth 2.0 Bearer JWT is recommended:

**API Key (static):** Generate an API ID and API Secret in the Dragos console (Admin → Users → Add New API Key). Pass both in request headers or as Basic auth credentials. API keys do not expire.

**OAuth 2.0 Bearer JWT (recommended):** Dynamic tokens with expiration and refresh capability. Preferred for production integrations due to reduced credential exposure risk.

Minimum required permissions for common integrations:
- Asset data: `asset:read`
- Detection/alert data: `detection:read`
- Vulnerability data: `vulnerability:read`
- Notification data: `asset:read`, `notification:read`

Generate credentials via: Dragos console → Admin → Users → select user → Add New API Key.

## Endpoints

- **Platform API versions:** v3 and v4 (select based on your Dragos Platform version)
- **Platform base URL:** `https://<dragos-appliance>/api/v{3|4}/`
- **WorldView threat intelligence base URL:** `https://portal.dragos.com/api/v1/`
- **Key platform endpoints:**
  - `GET /assets` — OT asset inventory; params: `page`, `pageSize`, `filter`
  - `GET /detections` — active and historical detections/alerts
  - `GET /vulnerabilities` — CVE-mapped vulnerability data for detected assets
  - `GET /notifications` — platform notifications and events
- **Key WorldView endpoints:**
  - `GET /threatgroups` — ICS-targeting threat group profiles (Dragos Activity Groups)
  - `GET /indicators` — threat indicators (IOCs) for ICS environments
  - `GET /products` — affected product advisories

## Example call

```bash
# Platform: get detections (API Key auth)
curl -u "$DRAGOS_API_ID:$DRAGOS_API_SECRET" \
  "https://dragos-appliance.port.example.com/api/v4/detections?pageSize=50"
```

```python
import requests

base = "https://dragos-appliance.port.example.com/api/v4"
auth = (DRAGOS_API_ID, DRAGOS_API_SECRET)

# Get OT asset inventory
assets = requests.get(f"{base}/assets", auth=auth, params={"pageSize": 100}).json()
for asset in assets.get("assets", []):
    print(asset.get("id"), asset.get("label"), asset.get("type"), asset.get("ips"))

# Get active detections
detections = requests.get(f"{base}/detections", auth=auth).json()
for d in detections.get("detections", []):
    print(d.get("title"), d.get("severity"), d.get("status"))

# WorldView: get ICS threat groups
wv = requests.get(
    "https://portal.dragos.com/api/v1/threatgroups",
    auth=auth,
).json()
```

## Rate limits

Not publicly documented. Contact Dragos for rate limit details applicable to your deployment and license. The platform API runs locally on the Dragos appliance; practical rate limits are governed by appliance hardware.

## SDKs / Libraries

- **Official:** None — REST API only
- **Community:** runZero integration (for asset import); Axonius connector; Cyware CTIX integration for WorldView; Secureworks Taegis integration

## Documentation

- Platform developer guide: available via Dragos customer portal (login required)
- WorldView API reference: https://portal.dragos.com/api/v1/doc/index.html (customer login required)
- Integration guides: https://docs.taegis.secureworks.com/integration/connectNetwork/dragos/ (third-party)
- OT threat landscape 2026: https://www.dragos.com/blog/ot-threat-landscape-2026

## Notes

- Dragos tracks ICS-specific threat groups as "Activity Groups" (e.g., CHERNOVITE, KAMACITE, KOSTOVITE) — these are distinct from general cybercrime groups and specifically target industrial environments including ports and maritime infrastructure.
- The 2026 Dragos OT Year in Review identifies a shift from pre-positioning to active mapping of control loops — relevant for port SOC teams assessing adversary intent.
- Knowledge Packs (weekly updates) push new IOCs, detection logic, and vulnerability context directly to the platform appliance without requiring manual updates — the API reflects this updated data in real time.
- Dragos Platform v4 introduced AI-assisted OT asset lifecycle management and industrial network visibility improvements — check your deployed version before using v4 endpoints.
- For maritime-specific context: Dragos has published whitepapers on ICS/OT cybersecurity in maritime transportation; relevant for understanding the threat landscape specific to port infrastructure.
- Least-privilege API credential scoping is enforced at the role level in the Dragos console — create dedicated API user accounts with only the permissions required for each integration.
