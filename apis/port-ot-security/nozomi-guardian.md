# Nozomi Networks Guardian

OT/IoT asset visibility and threat detection platform with a powerful OpenAPI using Nozomi Query Language (NQL) for flexible data retrieval — actively used in maritime port environments with N2OS v26.2.0 (April 2026) as the current release.

**Tier:** Enterprise
**Auth:** HTTP Basic Auth
**Last researched:** 2026-05-13

## Use cases

- Querying the full OT/IoT asset inventory, active alerts, and vulnerability data from Guardian sensors deployed across port industrial networks using flexible NQL queries
- Forwarding Guardian alerts, audit logs, and health data to SIEM platforms (Splunk, QRadar, Chronicle) and SOAR tools via native integrations or the OpenAPI
- Importing external asset data (from CMDBs, procurement systems, or other sensors) into Guardian via the node import endpoints to enrich the asset inventory

## Pricing

- **Free tier:** Guardian Community Edition — available as a free virtual sensor with limited scale; suitable for lab and evaluation use; see https://community.nozominetworks.com
- **Paid tiers:** Enterprise licensing; contact Nozomi Networks for pricing based on asset count and site scale
- **Enterprise:** Custom pricing; contact https://www.nozominetworks.com
- **Notes:** The Community Edition provides a subset of Guardian functionality at no cost. Enterprise deployments support hardware appliances, virtual machines, and cloud sensors.

## Authentication

HTTP Basic Authentication on every API call. Encode `Username:Password` as Base64 and pass as:

```
Authorization: Basic <base64(Username:Password)>
```

Create a dedicated API user account in Guardian's administration interface — avoid using shared operational credentials. Admin group privileges are required for import endpoints; Viewer role is sufficient for read queries.

## Endpoints

- **Base URL:** `https://<GuardianHost>/api/open/`
- **Key endpoints:**
  - `GET /query/do` — execute an NQL query against Guardian data; param: `query` (NQL string)
  - `POST /nodes/import` — import OT asset records from CSV file upload
  - `POST /nodes/import_from_json` — import OT asset records as JSON payload
  - `GET /alerts/<AlertID>/trace` — download packet trace associated with a specific alert

**NQL query examples:**
- `nodes` — all detected OT/IoT nodes
- `nodes | count` — total node count
- `nodes | where type = "PLC"` — filter for PLCs only
- `alerts` — all alerts
- `alerts | where severity = "high" | head 50` — top 50 high-severity alerts
- `vulnerabilities | head 100` — first 100 vulnerability records
- `sessions` — network sessions
- `links` — communication links between assets
- `nodes | select ip, mac, vendor, firmware, type | sort ip` — custom field selection

**Full NQL reference:** Available in the Guardian User Guide at `technicaldocs.nozominetworks.com`.

## Example call

```bash
# Query all PLC nodes (URL-encode the query string)
curl -u "$GDN_USER:$GDN_PASS" \
  "https://guardian.port.example.com/api/open/query/do?query=nodes%20%7C%20where%20type%20%3D%20%22PLC%22"

# Get high-severity alerts
curl -u "$GDN_USER:$GDN_PASS" \
  'https://guardian.port.example.com/api/open/query/do?query=alerts | where severity = "high"'
```

```python
import requests
from requests.auth import HTTPBasicAuth
from urllib.parse import quote

base = "https://guardian.port.example.com/api/open"
auth = HTTPBasicAuth(GDN_USER, GDN_PASS)

def nql(query):
    resp = requests.get(
        f"{base}/query/do",
        auth=auth,
        params={"query": query},
        verify=True,
    )
    return resp.json()

# Get all OT assets
assets = nql("nodes | select ip, mac, vendor, firmware, type, os")
for node in assets.get("result", []):
    print(node)

# Get active alerts
alerts = nql('alerts | where status = "open" | sort severity | head 100')
for alert in alerts.get("result", []):
    print(alert.get("name"), alert.get("severity"), alert.get("time"))

# Get vulnerability data
vulns = nql("vulnerabilities | head 500")
```

## Rate limits

Not publicly documented. The OpenAPI imposes no explicit published rate limit; practical limits are governed by Guardian appliance hardware. Implement appropriate delays in high-frequency polling loops. The query endpoint handles complex NQL with aggregation and filtering server-side — offload processing to NQL rather than fetching large datasets and filtering client-side.

## SDKs / Libraries

- **Official:** None — REST/OpenAPI only; OpenAPI specification available via the Guardian technical documentation portal
- **Community:** Elastic integration (`nozomi_networks` in Elastic integrations catalog); Secureworks Taegis integration; Axonius connector; runZero asset import

## Documentation

- Administrator Guide (N2OS v26.2.0): https://technicaldocs.nozominetworks.com/out/pdf-output/Guardian-Administrator%20Guide.pdf
- OpenAPI reference: https://technicaldocs.nozominetworks.com/products/n2os/topics/sdk/data-integ-bp/r_n2os-sdk_dibp_openapi.html
- Data integration overview: https://technicaldocs.nozominetworks.com/products/n2os/topics/administration/settings/data-integration/c_n2os_admin_settings_data-integration_overview_guardian.html
- Community Edition: https://community.nozominetworks.com/support.html

## Notes

- Nozomi Networks Guardian is one of the most widely deployed OT security sensors in maritime and port environments globally — the platform has specific use cases documented for port terminal operators and maritime critical infrastructure.
- N2OS v26.2.0 (released April 2026) is the current production release; the OpenAPI is versioned with the OS — check the technical docs portal for the API specification matching your deployed version.
- Guardian's NQL (Nozomi Query Language) is significantly more powerful than a simple filter API — it supports piping, aggregation, grouping, and field selection, enabling complex queries without client-side post-processing.
- Native integrations (20+) include: Splunk (CIM JSON), IBM QRadar (LEEF), Google Chronicle, ServiceNow, Kafka, Cisco ISE, Microsoft Endpoint Configuration Manager, Aruba ClearPass, CarbonBlack, Active Directory — configure via the Guardian admin UI rather than the API for these standard integrations.
- The Central Management Console (CMC) provides a unified view across multiple Guardian sensors (e.g., one per berth zone or terminal) and exposes the same OpenAPI at the CMC level for multi-site queries.
- For port security workflows: combine Guardian asset data with CISA ICS advisories (`cisa-ics-advisories.md`) to identify which specific PLCs and HMIs at a port are affected by newly published CVEs.
