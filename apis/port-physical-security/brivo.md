# Brivo

Cloud-based physical access control platform with an open REST API for managing access points, users, credentials, and access events — enabling port and terminal operators to integrate badge/door management with HR, contractor, and security systems.

**Tier:** Enterprise
**Auth:** OAuth 2.0
**Last researched:** 2026-05-14

## Use cases

- Automating user provisioning and credential issuance for port staff and contractors by integrating Brivo with an HR or contractor management system via the API
- Querying access event logs from Brivo-connected gate readers at port terminals for SIEM ingestion or compliance audit trails
- Remotely locking and unlocking port access points from an operations centre in response to security alerts

## Pricing

- **Free tier:** None — hardware and cloud subscription required
- **Paid tiers:** Approximately $13.50–$20 per door per month depending on edition; advanced capabilities (license plate recognition, anomaly detection, API integrations) add $15–$50 per door per month
- **Enterprise:** Custom pricing for large multi-site port deployments; contact https://www.brivo.com
- **Notes:** API licensing may be a separate line item for enterprise deployments; contact Brivo sales for details. Hardware (Brivo-compatible readers and panels) is required separately.

## Authentication

OAuth 2.0 three-legged authorization code flow. Register your application at `https://developer.brivo.com`, obtain a client ID and secret, then implement the authorization code flow to obtain a Bearer access token. Pass the token as `Authorization: Bearer <token>` on all API calls.

API base hostname is `api.brivo.com`. Developer sandbox access: register at `developer.brivo.com` and email `BrivoAPI@brivo.com` for sandbox credentials.

## Endpoints

- **Base URL:** `https://api.brivo.com`
- **Key endpoints (all prefixed `/v1/api`):**
  - `GET /access-points` — list all door/gate access points
  - `GET /users` — list all users (port employees and contractors)
  - `POST /users` — create a new user record
  - `GET /users/{userId}/passes` — list credentials for a user
  - `POST /users/{userId}/passes` — issue a new credential
  - `DELETE /users/{userId}/passes/{passId}` — revoke a credential
  - `GET /events` — access event log (entry, denial, alert events)
  - `POST /access-points/{accessPointId}/unlock` — remote unlock a door/gate
  - `GET /groups` — list access level groups

## Example call

```bash
# List all access points (gates, doors)
curl -H "Authorization: Bearer $BRIVO_TOKEN" \
  "https://api.brivo.com/v1/api/access-points"

# Remote unlock a gate
curl -X POST \
  -H "Authorization: Bearer $BRIVO_TOKEN" \
  "https://api.brivo.com/v1/api/access-points/$ACCESS_POINT_ID/unlock"
```

```python
import requests

headers = {"Authorization": f"Bearer {BRIVO_TOKEN}"}
base = "https://api.brivo.com/v1/api"

# Get access events for audit
events = requests.get(f"{base}/events", headers=headers).json()
for event in events.get("data", []):
    print(event.get("occurred"), event.get("eventType"), event.get("accessPointName"))

# Revoke a contractor credential
requests.delete(
    f"{base}/users/{USER_ID}/passes/{PASS_ID}",
    headers=headers,
)
```

## Rate limits

- Developer API keys: 25,000 calls/month; 25 calls/second
- Standard production API: 100,000 calls/month
- Higher limits available for enterprise; contact Brivo

## SDKs / Libraries

- **Official:** None — REST API only; OpenAPI specification available via `apidocs.brivo.com`
- **Community:** Axonius connector (asset management); Envoy integration (visitor management → Brivo credential provisioning); MRI OnLocation integration

## Documentation

- API documentation: https://apidocs.brivo.com/
- Developer portal (register + sandbox): https://developer.brivo.com/
- Open API platform overview: https://www.brivo.com/products/open-api-platform/

## Notes

- Brivo also integrates with Eagle Eye Networks for video surveillance; the video API is separate at `developer.eagleeyenetworks.com` — not the same API key or base URL.
- The Technology Partner Program at `developer.brivo.com` provides access to the production API key and a dedicated partner portal with integration support.
- Brivo supports integrations with visitor management systems (Envoy, Proxyclick/Eptura) to automatically issue and revoke access credentials when a visitor is checked in/out — useful for port contractor workflows where access is time-bounded to a single site visit.
- Multi-site port deployments (multiple terminals or berth zones) are supported; access point groups can be scoped per site for event filtering.
