# Sign In Enterprise (Traction Guest)

Enterprise visitor, contractor, and employee sign-in management platform with a REST API for automating access workflows, watchlist checking, IoT-triggered credential provisioning, and compliance reporting at port facilities.

**Tier:** Enterprise
**Auth:** OAuth Token
**Last researched:** 2026-05-14

## Use cases

- Managing port contractor and visitor pre-registration (invites) with automatic watchlist screening and host notification via the REST API integrated into a contractor onboarding workflow
- Provisioning Wi-Fi, turnstile, and PACS credentials automatically when a contractor's invite is accepted and they arrive at the port gatehouse
- Exporting sign-in audit logs and access violation records via the API for port compliance reporting and regulatory inspection preparation

## Pricing

- **Free tier:** None — enterprise licensing
- **Paid tiers:** Quote-based per location; pricing not publicly listed; contact https://www.signinenterprise.com
- **Enterprise:** Custom pricing for multi-terminal port deployments; contact Sign In Solutions / Traction Guest sales
- **Notes:** Formerly branded Traction Guest; now operating under the Sign In Enterprise / Sign In Solutions umbrella; legacy `tractionguest.com` portal and APIs remain active.

## Authentication

OAuth token generated from the developer portal. Log in at the regional dev portal using your web portal credentials:

- US: `https://us.tractionguest.com/dev_portal/login`
- Canada: `https://ca.tractionguest.com/dev_portal/login`
- Europe: `https://uk.tractionguest.com/dev_portal/login`

Click **CREATE TOKEN**, select OAuth scopes (`openid` and `all` are pre-selected), and save. Copy the token immediately — it is shown only once. Include as `Authorization: Bearer <token>` on all API calls. An ADMIN permission bundle is recommended for full API access.

## Endpoints

- **Base URL:** Available from the developer portal documentation at `https://developers.signinenterprise.com`
- **Key resources (standard REST; GET/POST/PUT/PATCH/DELETE):**
  - `Invites` — pre-registered visitor and contractor invitations; create, update, cancel
  - `Hosts` — port employees designated as visitor sponsors/hosts
  - `Locations` — port site and zone definitions
  - `Sign-ins` — active and historical sign-in records
  - `Watchlists` — allow/deny lists for visitor and contractor screening
  - `Groups` — host groups and visitor categories
  - `Audit logs` — change and access event audit trail

## Example call

```python
import requests

headers = {
    "Authorization": f"Bearer {SIGN_IN_TOKEN}",
    "Content-Type": "application/json",
}

# Base URL confirmed from the Sign In Enterprise developer portal
base = "https://us.tractionguest.com/api/v3"

# Create a contractor invite
resp = requests.post(
    f"{base}/invites",
    headers=headers,
    json={
        "invite": {
            "first_name": "Maria",
            "last_name": "Cardoso",
            "email": "m.cardoso@portservices.com",
            "company_name": "Port Services Ltd",
            "start_date": "2026-05-15T08:00:00Z",
            "end_date": "2026-05-15T18:00:00Z",
            "location_id": PORT_LOCATION_ID,
            "host_id": HOST_ID,
        }
    },
)
print(resp.json())

# Get current sign-ins
sign_ins = requests.get(f"{base}/sign_ins", headers=headers).json()
for s in sign_ins.get("data", []):
    print(s.get("guest_name"), s.get("signed_in_at"))
```

## Rate limits

Not publicly documented. Contact Sign In Solutions / Traction Guest support for rate limit policies.

## SDKs / Libraries

- **Official:** SDKs for Dart/Flutter, Swift, Android, TypeScript/Angular, and Objective-C — `https://github.com/tractionguest/guest-api`
- **Community:** Avigilon Alta (Openpath) integration; Salesforce AppExchange connector; Microsoft Power Automate connector (`learn.microsoft.com/en-us/connectors/tractionguest`)

## Documentation

- Developer portal: https://developers.signinenterprise.com/
- API token generation: https://help.signinsolutions.com/en/articles/10578260-how-do-i-generate-an-api-token-for-a-3rd-party-integration
- SDK repository: https://github.com/tractionguest/guest-api
- Microsoft Power Automate connector: https://learn.microsoft.com/en-us/connectors/tractionguest/

## Notes

- Sign In Enterprise supports watchlist checking against custom internal lists — port operators can load sanctioned contractor lists, vessel crew deny lists, or personnel suspended from site access and have them automatically flagged at sign-in without gatehouse staff intervention.
- IoT integration capabilities include automatic Wi-Fi provisioning (SSID access token issued on sign-in), turnstile release, and PACS credential activation — making it one of the more capable visitor management platforms for automated port access workflows.
- The platform integrates natively with Avigilon Alta (Openpath) for credential provisioning on invite acceptance, and with Genetec Security Center via the Genetec partner integration hub.
- The `lenel-sdk` on GitHub (`github.com/tractionguest/lenel-sdk`) was authored by Traction Guest as a reference implementation for syncing Sign In Enterprise sign-in data into LenelS2 OnGuard cardholder records.
- Regional API portals are separate deployments — US, Canada, and Europe data are isolated; use the correct regional portal and base URL matching your deployment.
