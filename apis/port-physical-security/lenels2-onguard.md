# LenelS2 OnGuard (OpenAccess)

Enterprise on-premise physical access control system (PACS) with the OpenAccess REST API for querying cardholders, controlling access hardware, retrieving events, and integrating with third-party port security and contractor management systems.

**Tier:** Enterprise
**Auth:** Session Token + Application-ID Header
**Last researched:** 2026-05-14

## Use cases

- Querying cardholder records from OnGuard (port employees and contractors) and syncing them with a contractor management or HR system via the OpenAccess API
- Subscribing to real-time access events (access granted, access denied, door forced open, door held open) from OnGuard-managed port gate readers for SIEM or SOC ingestion
- Controlling access panel hardware programmatically (grant access, lock/unlock doors) via the execute_method endpoint in response to security alerts

## Pricing

- **Free tier:** None — requires OnGuard server license and OpenAccess Alliance Program (OAAP) membership
- **Paid tiers:** OnGuard licensing is quote-based per access point/reader; contact LenelS2 (a Carrier company) for pricing at https://www.lenels2.com
- **Enterprise:** Enterprise licensing available; OAAP membership required for API access — apply at https://www.lenels2.com/en/security-solutions/third-party-integration/oaap
- **Notes:** The OpenAccess API is only available to OAAP members; OAAP membership involves a fee and NDA. LenelS2 documentation is available via the MyBuildings portal (portal.mybuildings.com) for licensed customers.

## Authentication

Two headers required on every authenticated request:
- `Application-Id` — your OAAP-issued application identifier
- `Session-Token` — obtained by calling `POST /authentication`

Session tokens expire after 15 minutes of inactivity (configurable). Call `GET /keepalive` to reset the inactivity timer. The `GET /version` endpoint is unauthenticated and can be used to confirm API availability.

```bash
# Obtain a session token
POST /api/access/onguard/openaccess/authentication
Application-Id: <your-app-id>
Content-Type: application/json

{"username": "apiuser", "password": "secret", "directory": {"id": 1}}
```

## Endpoints

- **Base URL:** `https://<OnGuard-server>/api/access/onguard/openaccess`
- **Key endpoints:**
  - `POST /authentication` — authenticate and obtain a session token
  - `DELETE /authentication` — log out and invalidate the session token
  - `GET /keepalive` — reset session inactivity timer
  - `GET /version` — get the OnGuard API version (unauthenticated)
  - `GET /feature_availability` — retrieve OnGuard license feature information
  - `GET /instances?type_name=Lnl_Cardholder` — query cardholder records (port employees/contractors)
  - `GET /instances?type_name=Lnl_Panel` — query access control panel hardware
  - `GET /instances?type_name=Lnl_AccessLevel` — query access levels
  - `POST /execute_method` — execute a hardware method (grant access, lock/unlock door, trigger alarm)
  - `GET /queue/{id}` — retrieve the result of an async queued task
  - `GET /queue` — list all pending queued tasks
  - `DELETE /queue/{id}` — cancel a queued task
  - `POST /partner_values` — store integration-specific custom metadata
  - `PUT /partner_values` — update integration-specific custom metadata

**Cardholder pagination:** Use `page_size`, `queue`, and `filter` parameters on `/instances` queries. Async mode (`queue=true`) is recommended for large cardholder datasets.

## Example call

```bash
# Authenticate and get a session token
curl -X POST \
  -H "Application-Id: $OAAP_APP_ID" \
  -H "Content-Type: application/json" \
  -d '{"username":"apiuser","password":"secret","directory":{"id":1}}' \
  "https://onguard.port.example.com/api/access/onguard/openaccess/authentication"

# Query cardholders (paginated)
curl -H "Application-Id: $OAAP_APP_ID" \
     -H "Session-Token: $SESSION_TOKEN" \
  "https://onguard.port.example.com/api/access/onguard/openaccess/instances?type_name=Lnl_Cardholder&page_size=100"
```

```python
import requests

base = "https://onguard.port.example.com/api/access/onguard/openaccess"
app_id = OAAP_APP_ID

def authenticate():
    resp = requests.post(
        f"{base}/authentication",
        headers={"Application-Id": app_id},
        json={"username": API_USER, "password": API_PASS, "directory": {"id": 1}},
    )
    return resp.json()["session_token"]

session_token = authenticate()
auth_headers = {"Application-Id": app_id, "Session-Token": session_token}

# Get all cardholders
cardholders = requests.get(
    f"{base}/instances",
    headers=auth_headers,
    params={"type_name": "Lnl_Cardholder", "page_size": 100},
).json()
for ch in cardholders.get("Items", []):
    print(ch.get("LASTNAME"), ch.get("FIRSTNAME"), ch.get("BADGEID"))

# Keep session alive during long-running operations
requests.get(f"{base}/keepalive", headers=auth_headers)
```

## Rate limits

Not publicly documented. Practical limits are governed by OnGuard server hardware. Use async queue mode (`queue=true`) for bulk queries to avoid server-side timeouts.

## SDKs / Libraries

- **Official:** None — REST API only; OpenAPI spec and full SDK documentation available to OAAP members via the LenelS2 developer portal
- **Community:** `tractionguest/lenel-sdk` (GitHub — Ruby SDK for OnGuard OpenAccess); SailPoint IdentityNow connector; Axonius connector; Google Chronicle SIEM parser

## Documentation

- OpenAccess knowledge base: https://kb.lenels2.com/home/openaccess
- OAAP program: https://www.lenels2.com/en/security-solutions/third-party-integration/oaap
- Community SDK (Ruby): https://github.com/tractionguest/lenel-sdk

## Notes

- LenelS2 OnGuard is one of the most widely deployed enterprise PACS systems globally and is common in large port authorities, container terminals, and critical infrastructure facilities.
- The OpenAccess API is on-premise only — it connects to the OnGuard Application Server on the local network; there is no cloud-hosted API endpoint.
- OAAP membership grants access to the full OpenAPI specification and test environment; without membership, API documentation is behind the MyBuildings portal login wall.
- The `Lnl_Cardholder` type is the primary entity for port personnel; other useful types include `Lnl_BadgeType`, `Lnl_AccessLevel`, `Lnl_Panel`, `Lnl_Reader`, and `Lnl_Alarm` — query available types via `GET /instances/type_names`.
- Session token inactivity timeout (default 15 minutes) requires the integration to call `/keepalive` regularly in long-running processes; alternatively, re-authenticate on 401 responses.
- Event subscriptions for real-time access events are handled via a separate subscription mechanism within the OnAccess module — consult OAAP documentation for the event subscription API details.
