# AVEVA PI Web API

RESTful interface to the AVEVA PI System industrial data historian — providing real-time and historical access to process telemetry, sensor values, asset hierarchies, and operational data from the PI infrastructure that underpins many of the world's major port and terminal facilities.

**Tier:** Enterprise
**Auth:** Basic / Kerberos
**Last researched:** 2026-05-13

## Use cases

- Retrieving real-time and historical operational telemetry from port equipment — crane load sensors, berth occupancy sensors, power consumption meters, fuel flow sensors — for cybersecurity baselining and anomaly detection
- Querying the PI Asset Framework (AF) hierarchy to map the full asset structure of a port facility, from terminal level down to individual equipment tags
- Streaming process data into SIEM or OT security platforms to correlate physical process anomalies with cybersecurity events

## Pricing

- **Free tier:** None — requires an active AVEVA PI Server license
- **Paid tiers:** PI Web API is included with the AVEVA PI Server (formerly OSIsoft PI Server) license; pricing is per-server and contact-based
- **Enterprise:** AVEVA enterprise licensing; contact https://www.aveva.com or your AVEVA channel partner
- **Notes:** PI Web API is a free add-on component installed on top of a licensed PI Server. The PI Server license itself is the cost gate. AVEVA PI System has an enormous install base at industrial facilities worldwide including major container terminals and bulk ports.

## Authentication

Three authentication modes are supported; configure in the PI Web API administration page:

- **Anonymous** — no credentials required (development and testing only; never use in production)
- **Basic** — pass `Authorization: Basic base64(username:password)` header; requires HTTPS
- **Kerberos** — Windows Active Directory single sign-on; recommended for corporate/OT networks; requires proper SPN configuration and delegation setup

CORS headers can include Authorization headers for cross-origin requests using Basic or Kerberos auth.

## Endpoints

- **Base URL:** `https://<server>/piwebapi/`
- **Key endpoints:**
  - `GET /piwebapi/` — root; returns links to all top-level controllers
  - `GET /piwebapi/system/userinfo` — returns the authenticated user identity (useful for testing auth)
  - `GET /piwebapi/assetservers` — list PI AF Asset Servers
  - `GET /piwebapi/assetdatabases/{webId}/elements` — AF element hierarchy (asset model)
  - `GET /piwebapi/assetdatabases/{webId}/elements/{webId}/attributes` — attributes for an element
  - `GET /piwebapi/points` — PI Data Archive point (tag) listing and search
  - `GET /piwebapi/streams/{webId}/value` — current (snapshot) value for a stream/tag
  - `GET /piwebapi/streams/{webId}/recorded` — recorded (archived) historical values; params: `startTime`, `endTime`, `maxCount`, `boundaryType`
  - `GET /piwebapi/streams/{webId}/interpolated` — interpolated values at regular intervals; params: `startTime`, `endTime`, `interval`
  - `GET /piwebapi/streams/{webId}/summary` — statistical summaries (min, max, average, count)
  - `POST /piwebapi/batch` — execute multiple API requests in a single HTTP call (bulk efficiency)
  - `GET /piwebapi/streamsets/{webId}/value` — current values for multiple streams simultaneously

**WebId** is the PI Web API identifier for any object (point, element, attribute); retrieve it from the listing endpoints.

## Example call

```bash
# Get current value for a PI tag (stream)
curl -u "$PI_USER:$PI_PASS" \
  "https://piserver.port.example.com/piwebapi/streams/{webId}/value"

# Get historical data for the last 24 hours
curl -u "$PI_USER:$PI_PASS" \
  "https://piserver.port.example.com/piwebapi/streams/{webId}/recorded?startTime=*-24h&endTime=*&maxCount=1000"
```

```python
import requests
from requests.auth import HTTPBasicAuth

base = "https://piserver.port.example.com/piwebapi"
auth = HTTPBasicAuth(PI_USER, PI_PASS)

# Get root and navigate to asset servers
root = requests.get(f"{base}/", auth=auth, verify=True).json()
asset_servers = requests.get(root["Links"]["AssetServers"], auth=auth).json()

# Search for a PI tag by name
points = requests.get(
    f"{base}/points",
    auth=auth,
    params={"nameFilter": "CRANE1_LOAD*", "dataServerWebId": DS_WEB_ID},
).json()

# Get current value
for point in points["Items"]:
    val = requests.get(f"{base}/streams/{point['WebId']}/value", auth=auth).json()
    print(point["Name"], val["Value"], val["Timestamp"])
```

## Rate limits

Not publicly documented — determined by PI Server hardware and configuration. The batch endpoint (`/piwebapi/batch`) is the recommended approach for reducing request count in high-frequency polling scenarios. Contact AVEVA or your PI administrator for server-side rate limit configuration.

## SDKs / Libraries

- **Official:** `pi-web-sdk` (Python, PyPI); official client libraries for Python, .NET, Java, Go, Angular, and jQuery via AVEVA GitHub (`AVEVA/AVEVA-Samples-PI-System`)
- **Community:** `osipy` and other community PI clients; numerous examples in AVEVA's learning portal

## Documentation

- PI Web API reference: https://docs.aveva.com/bundle/pi-web-api-reference/page/help.html
- Getting started: https://docs.aveva.com/bundle/pi-web-api-reference/page/help/getting-started.html
- Authentication methods: https://docs.aveva.com/bundle/pi-web-api/page/1023024.html
- AVEVA samples (GitHub): https://github.com/AVEVA/AVEVA-Samples-PI-System
- Learning portal: https://learning.osisoft.com/using-pi-web-api-from-beginner-to-advanced

## Notes

- AVEVA PI System (formerly OSIsoft PI) is the dominant industrial data historian globally — the vast majority of large container terminals, bulk ports, and LNG terminals run PI infrastructure for process data collection.
- PI tags store individual sensor readings; a large port may have tens of thousands of tags covering cranes, conveyors, berth sensors, power systems, HVAC, fuel systems, and environmental monitors.
- The PI Asset Framework (AF) provides a structured asset hierarchy above the raw tag layer — critical for mapping physical assets to their telemetry streams in security workflows.
- For OT cybersecurity use: baseline normal process value ranges per tag using `recorded` historical data, then monitor `value` endpoint in real time for statistical deviations indicating potential manipulation or equipment compromise.
- Always use HTTPS and Kerberos or Basic auth with strong credentials; Anonymous mode is never acceptable in production OT environments.
- PI Web API version compatibility: check the version installed on your PI Server before using newer endpoint features; the reference documentation is versioned by PI Web API release.
