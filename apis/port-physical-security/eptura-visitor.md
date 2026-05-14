# Eptura Visitor (Proxyclick)

Enterprise visitor management REST API (formerly Proxyclick, now part of Eptura) for pre-registering visitors, managing meetings, tracking on-site presence, and integrating visitor records with access control systems at port facilities.

**Tier:** Paid
**Auth:** OAuth 2.0 (Bearer Token)
**Last researched:** 2026-05-14

## Use cases

- Managing pre-registered meetings and visitor invitations for port authority offices and terminal control rooms via the REST API, synced with access control credential issuance
- Tracking which contractors and visitors are currently on-site at a port facility in real time by querying active visit records
- Exporting visitor log data for compliance audits and port facility access investigations

## Pricing

- **Free tier:** None
- **Paid tiers:** Per-location monthly subscription; pricing not publicly listed — contact https://eptura.com for current rates
- **Enterprise:** Volume pricing for multi-site port deployments; contact Eptura sales
- **Notes:** Formerly Proxyclick; now sold as part of the Eptura integrated workplace platform. Pricing for standalone visitor management vs. bundled Eptura platform may differ.

## Authentication

OAuth 2.0 password grant (client credentials + user credentials). Obtain client ID and secret from Eptura/Proxyclick support. Exchange for a Bearer token:

```bash
POST https://api.proxyclick.com/oauth/token
Content-Type: application/x-www-form-urlencoded

grant_type=password&client_id=CLIENT_ID&client_secret=CLIENT_SECRET&username=EMAIL&password=PASSWORD
```

Use the returned `access_token` as `Authorization: Bearer <token>` on all API calls.

## Endpoints

- **Base URL:** `https://api.proxyclick.com/v1`
- **Key endpoints:**
  - `GET /companies` — list companies (multi-tenant deployments)
  - `GET /companies/{id}/users` — list users (employees/hosts) for a company
  - `GET /companies/{id}/vm/meetings` — list scheduled meetings/visits
  - `POST /companies/{id}/vm/meetings` — create a new meeting (visitor pre-registration)
  - `PUT /companies/{id}/vm/meetings/{meetingId}` — update a meeting
  - `DELETE /companies/{id}/vm/meetings/{meetingId}` — cancel a meeting
  - `GET /companies/{id}/vm/visits` — list visit records (sign-in/sign-out events)
  - `POST /companies/{id}/vm/visits` — create a visit record
  - `PATCH /companies/{id}/vm/visits/{visitId}` — update visit status (check in/out)
  - `GET /companies/{id}/vm/visitors` — list visitor profiles
  - `GET /companies/{id}/vm/custom-fields` — retrieve custom form fields

**Data formats:** JSON (UTF-8); dates in ISO 8601 format; phone numbers in E.164 format.

## Example call

```bash
# List all scheduled meetings at a port company
curl -H "Authorization: Bearer $EPTURA_TOKEN" \
  "https://api.proxyclick.com/v1/companies/$COMPANY_ID/vm/meetings"

# Mark a contractor as on-site (check in)
curl -X PATCH \
  -H "Authorization: Bearer $EPTURA_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"status": "on_site"}' \
  "https://api.proxyclick.com/v1/companies/$COMPANY_ID/vm/visits/$VISIT_ID"
```

```python
import requests

base = "https://api.proxyclick.com/v1"
headers = {"Authorization": f"Bearer {EPTURA_TOKEN}"}

# Get all contractors currently on-site
visits = requests.get(
    f"{base}/companies/{COMPANY_ID}/vm/visits",
    headers=headers,
    params={"status": "on_site"},
).json()
for visit in visits:
    print(visit.get("visitor", {}).get("name"), visit.get("checkIn"))
```

## Rate limits

Not publicly documented. Contact Eptura for rate limit information.

## SDKs / Libraries

- **Official:** None — REST API only; cURL examples in documentation
- **Community:** Genetec ClearID integration (native visitor management connector); Palo Alto Cortex XSOAR playbooks; ServiceNow integration

## Documentation

- API reference: https://api.proxyclick.com/v1/docs/
- Eptura Visitor product page: https://eptura.com/proxyclick/
- Genetec integration: https://www.genetec.com/partners/partner-integration-hub/proxyclick/proxyclick-visitor-management

## Notes

- Proxyclick rebranded to Eptura Visitor following acquisition by Eptura (integrated workplace management platform); the API domain `api.proxyclick.com` and all existing integrations remain active.
- The platform integrates natively with Genetec Security Center for visitor-triggered credential provisioning — one of the more commonly used visitor-to-PACS bridges in enterprise port environments.
- Custom fields (`/vm/custom-fields`) support port-specific data collection on sign-in (vessel name, berth number, contractor company, safety induction status) without platform customization.
- The `status` field on visit records supports: `expected`, `on_site`, `checked_out` — use `PATCH` to update as visitors move through port checkpoints.
