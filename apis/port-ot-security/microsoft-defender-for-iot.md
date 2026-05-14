# Microsoft Defender for IoT

Microsoft's OT/IoT network monitoring platform — providing REST API access to detected OT assets, alerts, and vulnerabilities from on-premise OT sensors, plus Azure Resource Manager APIs for cloud-managed deployments; used in critical infrastructure including ports and terminals.

**Tier:** Freemium
**Auth:** Bearer Token
**Last researched:** 2026-05-13

## Use cases

- Querying OT device inventory, active alerts, and CVE-mapped vulnerabilities from Defender for IoT sensors deployed across port OT network segments via the on-premise sensor REST API
- Integrating Defender for IoT detections with Microsoft Sentinel SIEM for unified IT/OT threat visibility across port infrastructure
- Managing multi-site Defender for IoT sensor deployments at large port authorities via the Azure Resource Manager API

## Pricing

- **Free tier:** Free trial available; 1,000 devices committed free per Azure subscription for the first 30 days
- **Paid tiers:** Per-device monthly pricing in Azure; pricing varies by device count tier — contact Microsoft or check Azure pricing calculator
- **Enterprise:** Volume licensing and Microsoft MSSP/partner programs available
- **Notes:** On-premise OT sensor deployment is the primary model for port environments; cloud-managed (Azure portal) management layer is available alongside on-premise sensors.

## Authentication

**On-premise sensor REST API:** Tokens are generated within the OT sensor web interface or via the authentication API. Pass as `Authorization: <token>` header (no "Bearer" prefix for some sensor endpoints — check the specific endpoint documentation).

**Azure Resource Manager API:** Azure AD OAuth 2.0 access token; obtain via `POST https://login.microsoftonline.com/{tenant}/oauth2/v2.0/token` with scope `https://management.azure.com/.default`.

Generate sensor API tokens: Sensor web UI → System Settings → Access Control → API Access Tokens.

## Endpoints

- **On-premise sensor base URL:** `https://<sensor-ip>`
- **Azure RM base URL:** `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.IoTSecurity/`
- **Key on-premise sensor endpoints:**
  - `GET /external/v1/devices` — all OT devices detected by this sensor; includes IP, MAC, vendor, firmware, protocols, risk score
  - `GET /external/v1/alerts` — active and historical alert data with severity and detection type
  - `GET /external/v1/vulnerabilities` — CVE-mapped vulnerability data for detected assets
  - `GET /external/v1/devicecves/{deviceId}` — CVEs for a specific device
  - `POST /external/authentication/validation` — validate API credentials
  - `POST /external/authentication/set_password` — change API user password
- **Key Azure RM endpoints:**
  - `GET /sites` — list all monitored sites
  - `GET /sites/{siteName}/sensors` — list sensors for a site
  - `GET /sensors/{sensorName}/alerts` — alerts from a cloud-managed sensor

## Example call

```bash
# On-premise sensor: get all detected OT devices
curl -H "Authorization: $SENSOR_TOKEN" \
  "https://192.168.1.100/external/v1/devices"

# Get active alerts from sensor
curl -H "Authorization: $SENSOR_TOKEN" \
  "https://192.168.1.100/external/v1/alerts"
```

```python
import requests

sensor_base = "https://192.168.1.100"
headers = {"Authorization": SENSOR_TOKEN}

# Get all OT devices
devices = requests.get(
    f"{sensor_base}/external/v1/devices",
    headers=headers,
    verify=False,  # replace with proper cert validation in production
).json()
for device in devices:
    print(device.get("id"), device.get("ipAddresses"), device.get("vendor"), device.get("riskScore"))

# Get CVE vulnerabilities for a specific device
cves = requests.get(
    f"{sensor_base}/external/v1/devicecves/{device['id']}",
    headers=headers,
    verify=False,
).json()
for cve in cves:
    print(cve.get("cveId"), cve.get("score"))
```

## Rate limits

Not publicly documented for on-premise sensor API. Azure RM API follows standard Azure API rate limits (typically 12,000 read requests per hour per subscription). On-premise sensor API limits are governed by sensor hardware capacity.

## SDKs / Libraries

- **Official:** Azure SDK for Python (`azure-mgmt-iot` for Azure RM); no dedicated Defender for IoT SDK
- **Community:** Microsoft Sentinel data connectors (native integration); Elastic integration; Splunk add-on for Microsoft Security

## Documentation

- On-premise API reference: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/references-work-with-defender-for-iot-apis
- Sensor auth API reference: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/api/sensor-auth-apis
- Azure RM API reference: https://learn.microsoft.com/en-us/rest/api/defenderforcloud/iot-security-solution/get
- Product overview: https://learn.microsoft.com/en-us/azure/defender-for-iot/

## Notes

- Microsoft Defender for IoT was formerly known as Azure Defender for IoT and CyberX (acquired 2020) — documentation and integrations may reference older product names.
- The on-premise OT sensor performs passive network monitoring (like Forescout eyeInspect and Nozomi Guardian) — no active scanning; safe for OT environments with PLCs and safety systems.
- Defender for IoT integrates natively with Microsoft Sentinel, making it the natural choice for port operators already in the Microsoft ecosystem — IT and OT security events appear in a single Sentinel workspace.
- The sensor supports industrial protocols: Modbus, DNP3, EtherNet/IP, PROFINET, BACnet, OPC UA, IEC 61850, Siemens S7, and many others.
- Risk scoring per device is computed from CVE severity, network exposure, and observed protocol behavior — useful for asset triage without custom scoring logic.
- Multi-sensor deployments (e.g., separate sensors per berth or terminal zone) are managed centrally via the Azure portal and the Azure RM API — relevant for large port authorities with multiple facilities.
- The `verify=False` in the example above is for illustration only — always validate TLS certificates in production OT environments.
