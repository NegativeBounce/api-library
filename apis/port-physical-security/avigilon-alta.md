# Avigilon Alta (Openpath)

Cloud-native mobile-first access control platform (formerly Openpath, acquired by Motorola Solutions 2021) with a REST + MQTT API for managing entries, users, credentials, and real-time access events across port facilities.

**Tier:** Enterprise
**Auth:** OAuth 2.0 (API Key → Bearer JWT)
**Last researched:** 2026-05-14

## Use cases

- Provisioning and revoking mobile credentials for port contractors and staff accessing controlled zones programmatically without manual card issuance
- Querying door/entry unlock events and access logs for all port gate readers via the REST API to feed into a SOC or SIEM
- Triggering lockdown plans and reverting them via API when a port security incident is declared

## Pricing

- **Free tier:** None
- **Paid tiers:** Per-reader hardware + cloud subscription; contact Motorola Solutions / Avigilon for pricing based on reader count and site scale
- **Enterprise:** Custom pricing; contact https://www.avigilon.com
- **Notes:** Hardware (Avigilon Alta readers and ACUs) is required; cloud subscription is bundled; pricing is not publicly listed.

## Authentication

Generate an API key in the Avigilon Alta web portal. Exchange it for a short-lived Bearer JWT:

```bash
POST https://api.openpath.com/auth/api-key
Authorization: Bearer <API_KEY>
```

Include the returned JWT as `Authorization: Bearer <JWT>` on all subsequent calls. JWTs expire; re-authenticate when a 401 is received.

## Endpoints

- **Base URL:** `https://api.openpath.com`
- **Key endpoints:**
  - `GET /orgs/{orgId}/users` — list all organization users
  - `POST /orgs/{orgId}/users` — create a new user (port employee or contractor)
  - `GET /orgs/{orgId}/users/{userId}/credentials` — list credentials for a user
  - `POST /orgs/{orgId}/users/{userId}/credentials` — issue a new credential (mobile or card)
  - `GET /orgs/{orgId}/entries` — list all door/entry points
  - `GET /orgs/{orgId}/acuModels` — list access control unit models
  - `GET /orgs/{orgId}/activityLogs` — access event log
  - `POST /orgs/{orgId}/users/{userId}/credentials/{credentialId}/cloudKeyTriggerLockdownPlan` — trigger lockdown for a credential
  - `POST /orgs/{orgId}/users/{userId}/credentials/{credentialId}/cloudKeyRevertLockdownPlan` — revert lockdown

**MQTT:** Subscribe to real-time access events via the Alta MQTT broker — documented in the API portal with sample code in Python and C#.

## Example call

```bash
# List all entries (doors/gates)
curl -H "Authorization: Bearer $ALTA_JWT" \
  "https://api.openpath.com/orgs/$ORG_ID/entries"

# Issue a mobile credential to a contractor
curl -X POST \
  -H "Authorization: Bearer $ALTA_JWT" \
  -H "Content-Type: application/json" \
  -d '{"credentialType":"mobile", "mobileType":"apple_wallet"}' \
  "https://api.openpath.com/orgs/$ORG_ID/users/$USER_ID/credentials"
```

```python
import requests

base = "https://api.openpath.com"
headers = {"Authorization": f"Bearer {ALTA_JWT}"}

# Get access logs for last 24 hours
logs = requests.get(
    f"{base}/orgs/{ORG_ID}/activityLogs",
    headers=headers,
    params={"from": "2026-05-13T00:00:00Z", "to": "2026-05-14T00:00:00Z"},
).json()
for event in logs.get("data", []):
    print(event.get("event"), event.get("entryName"), event.get("actorName"))
```

## Rate limits

Not publicly documented. Contact Avigilon/Motorola Solutions for rate limit policies applicable to your license tier.

## SDKs / Libraries

- **Official:** iOS Mobile SDK and Android Mobile SDK (for embedding mobile credential UX in custom apps); REST API only for server-side integrations
- **Community:** `openpath.readme.io` Postman collection; sample MQTT code in Python and C# available in the API portal

## Documentation

- API reference: https://openpath.readme.io/
- Motorola Solutions video security & access control docs: https://www.motorolasolutions.com/en_xu/products/training/video-security-access-control-documentation-resources.html
- Avigilon Alta product page: https://www.avigilon.com/access-control

## Notes

- Avigilon Alta (Openpath) was acquired by Motorola Solutions in 2021 and is now sold as part of the Avigilon brand; legacy documentation and integrations reference the "Openpath" name and `openpath.com` domain — both remain active.
- The platform is cloud-first and requires Avigilon Alta hardware readers; it does not support third-party reader integration in the standard configuration.
- Real-time event streaming via MQTT is the recommended pattern for high-frequency access event ingestion (SOC/SIEM integration) rather than polling the REST event log endpoint.
- Mobile credentials via Apple Wallet and Google Wallet are supported for touchless port gate access — relevant for ports implementing contractor touchless entry programs.
- Lockdown plan APIs allow programmatic port security escalation from a central system; combine with perimeter alarm triggers for automated incident response.
