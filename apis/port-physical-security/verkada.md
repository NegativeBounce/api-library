# Verkada

Cloud-managed physical security platform combining access control and video surveillance with a REST API for managing doors, access levels, users, cameras, and events across port facilities from a single system.

**Tier:** Enterprise
**Auth:** API Key + Bearer Token (30-minute TTL)
**Last researched:** 2026-05-14

## Use cases

- Managing port gate access levels and user permissions programmatically via the API, removing and provisioning door access for contractor groups without requiring manual dashboard changes
- Querying door access events and camera alert events from Verkada-managed port checkpoints for integration with a SOC platform or compliance audit system
- Triggering lockdown scenarios across all Verkada-managed port gates via API when a security incident is declared by an operations centre

## Pricing

- **Free tier:** None — Verkada hardware (readers, controllers, cameras) required with cloud subscription
- **Paid tiers:** Hardware purchase + per-camera/per-door cloud subscription; pricing not publicly listed; contact https://www.verkada.com for quotes
- **Enterprise:** Multi-site port deployments supported; volume pricing available
- **Notes:** Unlike most PACS vendors, Verkada bundles hardware, cloud management, and support in a single subscription; no on-premise server is required.

## Authentication

Two-step authentication:

1. **Generate an API key** — in the Verkada Command portal, navigate to Admin → API Keys to create a key with specific product and endpoint permissions.
2. **Exchange for a Bearer token** — POST the API key to the token endpoint; receive a Bearer token valid for 30 minutes. Tokens cannot be refreshed; re-authenticate after expiry.

```bash
POST https://api.verkada.com/token
Content-Type: application/json

{"api_key": "<YOUR_API_KEY>"}
```

Use the returned token as `Authorization: Bearer <token>` on all API calls.

**Note:** API keys have granular permission scopes per product (Access Control, Cameras, Alarms) and per endpoint category — configure the minimum required permissions when generating keys.

## Endpoints

- **Base URL:** `https://api.verkada.com`
- **Key endpoints:**
  - **Access Control**
    - `GET /access/v1/doors` — list all Verkada-managed doors and gates
    - `GET /access/v1/access_levels` — list access levels
    - `POST /access/v1/access_levels` — create a new access level
    - `GET /access/v1/users` — list users with access credentials
    - `POST /access/v1/users` — add a new user
    - `GET /access/v1/events` — access event log (grants, denials, lockdowns)
    - `POST /access/v1/doors/{door_id}/unlock` — remotely unlock a specific door
    - `POST /access/v1/doors/{door_id}/lock` — remotely lock a specific door
  - **Cameras**
    - `GET /cameras/v1/devices` — list all cameras
    - `GET /cameras/v1/footage` — query recorded footage metadata
  - **System**
    - `POST /token` — obtain a 30-minute Bearer token from an API key

**Door Management via API prerequisite:** Enable "Door Management via API" in Command (Admin → Access Settings) at the organization, site, and individual door level before remote lock/unlock calls will be accepted.

## Example call

```bash
# Get a 30-minute Bearer token
TOKEN=$(curl -s -X POST \
  -H "Content-Type: application/json" \
  -d '{"api_key": "'"$VERKADA_API_KEY"'"}' \
  "https://api.verkada.com/token" | jq -r '.token')

# List all access control doors
curl -H "Authorization: Bearer $TOKEN" \
  "https://api.verkada.com/access/v1/doors"

# Remotely unlock a gate
curl -X POST \
  -H "Authorization: Bearer $TOKEN" \
  "https://api.verkada.com/access/v1/doors/$DOOR_ID/unlock"
```

```python
import requests

# Get a fresh token (expires in 30 min — re-authenticate before expiry)
token_resp = requests.post(
    "https://api.verkada.com/token",
    json={"api_key": VERKADA_API_KEY},
)
token = token_resp.json()["token"]
headers = {"Authorization": f"Bearer {token}"}

# Get access events
events = requests.get(
    "https://api.verkada.com/access/v1/events",
    headers=headers,
).json()
for event in events.get("data", []):
    print(event.get("event_type"), event.get("door_name"), event.get("accessed_at"))
```

## Rate limits

300 requests per minute per organization across all endpoints. Verkada may apply different limits to specific endpoints on a case-by-case basis.

## SDKs / Libraries

- **Official:** None — REST API only; Postman collection available at the Verkada API public workspace
- **Community:** Stellar Cyber integration connector; dltHub Verkada source connector; Axonius connector

## Documentation

- API reference: https://apidocs.verkada.com/reference/introduction
- Access API overview: https://apidocs.verkada.com/reference/access-api-101
- Manage doors via API: https://help.verkada.com/access-control/integrations-and-alerts/manage-doors-via-api
- Rate limiting: https://apidocs.verkada.com/reference/ratelimiting
- Postman workspace: https://www.postman.com/verkada-api/verkada-api-public-workspace/documentation/udz2ppu/verkada-command-api

## Notes

- Verkada's 30-minute token design means API integrations must handle token refresh proactively — cache the token, track its issue time, and re-authenticate before the 30-minute window closes rather than waiting for a 401.
- Door Management via API must be explicitly enabled per door in the Command dashboard before the lock/unlock endpoints will accept requests — this is a deliberate safety gate, not an API error.
- Verkada API permissions are scoped per API key at the product and endpoint level — create separate API keys for read-only SIEM integrations vs. write-access operations management integrations to enforce least privilege.
- The Verkada platform combines access control and cameras in one system — the same API key (with appropriate permissions) can query both access events and camera footage metadata, simplifying port SOC integrations that need to correlate access logs with video evidence.
- For port multi-site deployments: Verkada's cloud architecture means all port sites are managed from a single Command organization; the `site_id` filter on event and device endpoints allows per-terminal scoping.
