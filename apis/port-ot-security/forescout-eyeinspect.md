# Forescout eyeInspect

Passive OT network monitoring platform (formerly SecurityMatters SilentDefense) providing REST API access to industrial asset inventory, alert data, and CVE-mapped vulnerability records — without active scanning that could disrupt port control systems.

**Tier:** Enterprise
**Auth:** Username / Password (role-based)
**Last researched:** 2026-05-13

## Use cases

- Querying the full OT device inventory discovered through passive network traffic analysis across port industrial Ethernet networks
- Pulling CVE-mapped vulnerability records per OT asset for integration with vulnerability management and patch prioritization workflows
- Retrieving alert data from eyeInspect for forwarding into SIEM platforms or automated port SOC ticketing workflows

## Pricing

- **Free tier:** None — enterprise licensing only
- **Paid tiers:** Enterprise licensing; contact Forescout for pricing based on asset count and deployment model
- **Enterprise:** Custom pricing; contact https://www.forescout.com
- **Notes:** eyeInspect is deployable as a hardware appliance or virtual machine in the OT network. Can operate standalone or integrated with Forescout eyeSight for combined IT/OT network visibility.

## Authentication

Username and password authentication against the eyeInspect appliance. The API user account must be assigned at minimum the **Viewer** role (read-only access to assets, alerts, and vulnerabilities). Creating a dedicated API-only user account is recommended over using a shared operational account.

Pass credentials as HTTP Basic Auth: `Authorization: Basic base64(username:password)`. All API communication should occur over HTTPS.

## Endpoints

- **Base URL:** `https://<eyeInspect-server>` (your deployed appliance IP or FQDN)
- **API version:** v1 (current as of eyeInspect v5.5.0)
- **Key endpoints:**
  - `GET /api/v1/hosts` — full OT asset inventory; each host record includes detected OS, firmware, protocol support, open ports, and CVE vulnerability records; page size max 100 records per request
  - `GET /api/v1/alerts` — alert data including detection type, severity, affected assets, and timestamp
  - `GET /api/v1/links` — network links (communication relationships between assets)
  - `GET /api/v1/changes` — asset configuration change events
  - `GET /api/v1/system/status` — appliance health and status

**Vulnerability data:** CVE records are embedded within host records returned by `/api/v1/hosts` — there is no separate vulnerability endpoint; vulnerability definitions are derived from the per-host CVE fields.

## Example call

```bash
# Get OT asset inventory (first 100 hosts)
curl -u "$EI_USER:$EI_PASS" \
  "https://eyeinspect.port.example.com/api/v1/hosts?limit=100&offset=0"

# Get active alerts
curl -u "$EI_USER:$EI_PASS" \
  "https://eyeinspect.port.example.com/api/v1/alerts?limit=100"
```

```python
import requests
from requests.auth import HTTPBasicAuth

base = "https://eyeinspect.port.example.com"
auth = HTTPBasicAuth(EI_USER, EI_PASS)

# Paginate through all OT assets
offset, page_size = 0, 100
while True:
    resp = requests.get(
        f"{base}/api/v1/hosts",
        auth=auth,
        params={"limit": page_size, "offset": offset},
        verify=True,
    ).json()
    hosts = resp.get("data", [])
    if not hosts:
        break
    for host in hosts:
        print(host.get("ip_addresses"), host.get("vendor"), host.get("model"))
        for cve in host.get("cves", []):
            print(f"  CVE: {cve['cve_id']} CVSS: {cve.get('cvss_score')}")
    offset += page_size

# Get recent alerts
alerts = requests.get(f"{base}/api/v1/alerts", auth=auth).json()
for alert in alerts.get("data", []):
    print(alert.get("title"), alert.get("severity"), alert.get("timestamp"))
```

## Rate limits

Not publicly documented. The recommended page size of 100 records per request should be respected; larger page sizes may cause timeouts on appliances with large asset inventories. Implement appropriate delays between paginated requests.

## SDKs / Libraries

- **Official:** None — REST API only
- **Community:** Cortex XSOAR integration (Palo Alto Marketplace: `Forescout EyeInspect`); ServiceNow Vulnerability Response integration; Brinqa connector; Axonius connector

## Documentation

- API guide (v5.5.0): https://docs.forescout.com/bundle/eyeinspect_api_guide_v5_5_0/page/gitdoc-eyeinspect/eyeInspect/eyeinspect_api_guide/about_eyeinspect_api.html
- Forescout documentation portal: https://docs.forescout.com
- eyeInspect product page: https://www.forescout.com/products/eyeinspect/
- Cortex XSOAR integration: https://xsoar.pan.dev/docs/reference/integrations/forescout-eye-inspect

## Notes

- eyeInspect uses passive deep packet inspection (DPI) of industrial protocols — it detects assets and their communications without sending any packets into the OT network, making it safe for environments where active scanning could disrupt safety systems or PLCs.
- Supported industrial protocols include: Modbus, DNP3, EtherNet/IP, PROFINET, IEC 61850, IEC 60870-5-104, BACnet, Siemens S7, OPC DA/UA, and many others — relevant for the full range of port automation systems.
- The `/api/v1/links` endpoint is particularly useful for port security: it maps which OT devices communicate with which others, enabling detection of unexpected lateral movement or new communication relationships.
- For maritime/port use: eyeInspect can fingerprint PLC models (Siemens S7-300/400/1200/1500, Rockwell ControlLogix, Schneider Modicon), vessel management terminal interfaces, and crane automation controllers from their network traffic signatures.
- eyeInspect can integrate with Forescout eyeSight for combined IT/OT policy enforcement — use the API to export OT asset data to your enterprise asset management system.
- Vulnerability data embedded in host records is correlated against NVD CVE database and vendor-specific security advisories; combine with CISA ICS advisories (`cisa-ics-advisories.md`) for a complete OT vulnerability picture.
