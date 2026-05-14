# Genetec ClearID

Cloud-based physical identity and access management (PIAM) REST API from Genetec — providing identity synchronization, visitor management, access request workflows, and host permission management for Security Center deployments at port facilities.

**Tier:** Enterprise
**Auth:** OAuth 2.0 (JWT Assertion)
**Last researched:** 2026-05-14

## Use cases

- Synchronizing port employee and contractor identity records from an HR or CMDB system into Genetec Security Center via the ClearID identity sync API, eliminating manual badge issuance workflows
- Retrieving upcoming and historical visitor events (ship agents, auditors, customs officials) at all port sites from the ClearID API for compliance reporting
- Querying host permissions and access level assignments to audit which contractors have access to which restricted port zones

## Pricing

- **Free tier:** None — requires Genetec Security Center license and ClearID module
- **Paid tiers:** Part of the Genetec Security Center SaaS platform; pricing is quote-based per site and user count; contact https://www.genetec.com
- **Enterprise:** Genetec One unified security platform bundles ClearID with video, access control, and license plate recognition; contact Genetec sales or an authorized reseller
- **Notes:** API access requires DAP (Developer Access Program) membership at developer.genetec.com; apply at https://github.com/Genetec/DAP

## Authentication

OAuth 2.0 with JWT assertion tokens. In the ClearID admin portal (Administration → API integrations), create an API integration and generate a key pair — the system produces a downloadable JSON config file containing the STS URL, Identity Service URL, account ID, and cryptographic credentials. Do not hardcode these values; load from the downloaded config at runtime.

Token endpoint: provided in the downloaded config JSON as `stsUrl` (typically `https://sts.clearid.io/connect/token`). Include the Bearer token as `Authorization: Bearer <token>` on all API calls.

## Endpoints

- **Base URL:** Provided in the downloaded API integration config JSON as `identityServiceUrl`; typically `https://<region>.api.clearid.io`
- **Key endpoints (all standard REST; GET/POST/PUT/PATCH/DELETE):**
  - Identities — create, update, deactivate port employee and contractor identity records
  - Visits — retrieve upcoming and past visitor event records
  - Hosts — list approved visitor hosts with their access permissions
  - Requesters — query access request data
  - Roles — manage access level roles and assignments
  - Sites — list monitored port sites and their configurations

## Example call

```python
import json
import requests

# Load config from the downloaded JSON file
with open("clearid-api-key.json") as f:
    config = json.load(f)

# Get an access token
token_resp = requests.post(
    config["stsUrl"] + "/connect/token",
    data={
        "grant_type": "client_credentials",
        "client_id": config["clientId"],
        "client_secret": config["clientSecret"],
        "scope": "clearid.api",
    },
)
token = token_resp.json()["access_token"]

headers = {"Authorization": f"Bearer {token}"}
identity_url = config["identityServiceUrl"]

# Sync a contractor identity
resp = requests.post(
    f"{identity_url}/identities",
    headers=headers,
    json={
        "firstName": "John",
        "lastName": "Doe",
        "email": "j.doe@contractor.com",
        "externalId": "CONTRACTOR-12345",
    },
)

# Get upcoming visitor events
visits = requests.get(f"{identity_url}/visits", headers=headers).json()
for visit in visits.get("value", []):
    print(visit.get("visitorName"), visit.get("scheduledArrival"), visit.get("siteName"))
```

## Rate limits

Not publicly documented. Contact Genetec or your authorized reseller for rate limit policies applicable to your license tier.

## SDKs / Libraries

- **Official:** Security Center .NET SDK via DAP (Development Acceleration Program); not available for the ClearID REST API specifically
- **Community:** SCIM integration for identity sync from Azure AD/Entra ID, Okta, and other IdPs; One Identity Synchronization Tool connector; LDAP Synchronization Agent

## Documentation

- ClearID developer guide: https://developer.genetec.com/r/en-us/clearid-developer-guide
- Authentication guide: https://help.clearid.io/EN/EN/CID/AuthenticatingConnection.html
- ClearID API overview: https://help.clearid.io/EN/EN/CID/C_CID_AboutTheAPI.html
- DAP (Developer Access Program): https://github.com/Genetec/DAP
- SDK samples: https://github.com/Genetec/Security-Center-SDK-Samples

## Notes

- Genetec ClearID is an API-first service — the entire ClearID web interface is built on top of the same REST API that integrators use, so anything visible in the UI is achievable via API.
- The primary integration pattern is identity synchronization: push employee and contractor records from an HR system or directory into ClearID, which then manages access levels and badge provisioning automatically within Security Center.
- The API config JSON (downloaded from Administration → Automation) contains all base URLs — never hardcode them; they can change between regions and upgrades.
- SCIM is the preferred protocol for automated identity lifecycle management (provisioning/deprovisioning) if your IdP supports it; use the direct REST API for custom workflows or one-off queries.
- For port use: ClearID's access request workflow APIs enable contractors to self-request access to specific berth zones with automatic approval routing to port security managers — reducing manual badge desk workload.
- Genetec Security Center is one of the most widely deployed enterprise PACS globally in port and critical infrastructure environments; the ClearID module adds the identity and visitor management layer on top.
