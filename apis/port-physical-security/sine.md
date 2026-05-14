# Sine by Honeywell

Industrial contractor and visitor management platform (part of Honeywell Forge) with an OAuth 2.0 REST API for managing site access invitations, contractor sign-ins, safety inductions, and compliance workflows at port facilities and industrial sites.

**Tier:** Paid
**Auth:** OAuth 2.0
**Last researched:** 2026-05-14

## Use cases

- Pre-registering contractors and service vendors for port site visits via API, triggering automatic safety induction reminders and document collection before arrival
- Querying real-time check-in and check-out data for all contractors currently on site at a port terminal for live mustering, headcount, and emergency evacuation support
- Receiving webhook events when a contractor checks in or out of a port gate to trigger downstream workflows (PACS credential activation, toolbox talk notifications, CMMS work order updates)

## Pricing

- **Free tier:** None — per-site subscription
- **Paid tiers:** Per-site monthly subscription; pricing not publicly listed; contact https://www.sine.co for pricing
- **Enterprise:** Volume pricing for multi-terminal port deployments; contact Honeywell Forge / Sine sales
- **Notes:** Sine is part of the Honeywell Forge Visitor Management product line following Honeywell's acquisition. Enterprise contracts may be via Honeywell directly.

## Authentication

OAuth 2.0 client credentials. Generate API credentials in the Sine admin dashboard (Settings → API Keys) to get a client ID and client secret. Exchange for a Bearer token:

```bash
POST https://openapi.sine.co/oauth/token
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&client_id=CLIENT_ID&client_secret=CLIENT_SECRET
```

Include the token as `Authorization: Bearer <token>` on all requests. **From May 1, 2026**, all requests also require the `X-Sine-Team-ID` header — find your Team ID in Sine Admin → Settings → Team Details.

**Note:** The legacy base URL `api.forge.connected.honeywell.com` was decommissioned on January 31, 2026. All integrations must use `openapi.sine.co`.

## Endpoints

- **Base URL:** `https://openapi.sine.co`
- **Key endpoints:**
  - `GET /sites` — list all port site locations
  - `GET /sites/{siteId}/invitations` — list invitations for a site
  - `POST /sites/{siteId}/invitations` — create a new contractor/visitor invitation
  - `GET /sites/{siteId}/invitations/{invitationId}` — get invitation details
  - `DELETE /sites/{siteId}/invitations/{invitationId}` — cancel an invitation
  - `GET /host-groups` — list host groups (port supervisors and gatekeepers)
  - `GET /companies` — list contractor companies registered in the system
  - `GET /workflow-responses` — retrieve sign-in workflow form responses (safety questions, induction answers)
- **Webhooks** (configured via Sine admin dashboard, authenticated with `x-sine-auth` header):
  - `check_in_request` — fires before a pass is created (allows pre-validation)
  - `check_in_success` — fires after a contractor pass is issued
  - `check_out_success` — fires when a contractor pass is checked out or expires

## Example call

```bash
# List all invitations at a port site
curl -H "Authorization: Bearer $SINE_TOKEN" \
     -H "X-Sine-Team-ID: $SINE_TEAM_ID" \
  "https://openapi.sine.co/sites/$SITE_ID/invitations"

# Create a contractor invitation
curl -X POST \
  -H "Authorization: Bearer $SINE_TOKEN" \
  -H "X-Sine-Team-ID: $SINE_TEAM_ID" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Bob Technician",
    "email": "bob@contractor.com",
    "company": "Port Services Ltd",
    "start_time": "2026-05-15T07:00:00Z",
    "end_time": "2026-05-15T17:00:00Z"
  }' \
  "https://openapi.sine.co/sites/$SITE_ID/invitations"
```

```python
import requests

headers = {
    "Authorization": f"Bearer {SINE_TOKEN}",
    "X-Sine-Team-ID": SINE_TEAM_ID,
}

# Get all contractors currently checked in
invitations = requests.get(
    f"https://openapi.sine.co/sites/{SITE_ID}/invitations",
    headers=headers,
    params={"status": "checked_in"},
).json()
for inv in invitations.get("data", []):
    print(inv.get("name"), inv.get("company"), inv.get("check_in_time"))
```

## Rate limits

Not publicly documented. Contact Sine/Honeywell Forge support for rate limit policies.

## SDKs / Libraries

- **Official:** None — REST API only; OpenAPI specification downloadable from `developer.sine.co`
- **Community:** Webhook-based integrations with PACS systems (Lenel, Genetec); Slack notification integrations

## Documentation

- Developer portal: https://developer.sine.co/
- Getting started: https://developer.sine.co/api/getting-started
- 2026 API upgrade guide: https://developer.sine.co/api/api-upgrade
- Webhook setup: https://sine.support/en/articles/2103371-webhook-integrations-setup

## Notes

- Sine is specifically designed for industrial and construction sites where contractor compliance (safety inductions, insurance certificates, training qualifications) must be validated before site access is granted — this makes it more port/industrial appropriate than general-purpose visitor management tools.
- The Sine sign-in kiosk (iPad or mobile app) supports photo capture, document scanning (SWMS, induction certificates, trade licenses), and NFC/QR code badge scanning at port gatehouses.
- The webhook `check_in_request` event fires before the pass is created — use this hook to query an external contractor database or sanctions list and return a block/allow decision without the contractor being marked as on-site.
- The 2026 API migration (`api.forge.connected.honeywell.com` → `openapi.sine.co`) is complete; any existing integrations using the legacy URL must be updated. The `X-Sine-Team-ID` header is mandatory from May 1, 2026.
- For port mustering: Sine's real-time check-in data combined with `check_out_success` webhooks can drive a live headcount board — combine with muster station assignment logic for emergency evacuation management.
