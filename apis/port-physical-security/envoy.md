# Envoy

Workplace and visitor management platform with a REST API and webhooks for automating visitor sign-in, contractor pre-registration, employee scheduling, and access event notifications at port facility reception and gatehouse checkpoints.

**Tier:** Freemium
**Auth:** OAuth 2.0
**Last researched:** 2026-05-14

## Use cases

- Pre-registering port contractors and ship agents as invited visitors so they receive QR codes for gatehouse check-in before arrival
- Triggering badge printing, NDA signing, and access credential issuance (via Brivo or other PACS integration) automatically when a visitor signs in at the port gatehouse kiosk
- Querying visitor log data via the API to build compliance audit reports for regulatory inspections of port facility access records

## Pricing

- **Free tier:** Available for small sites — limited visitor entries and basic features; exact limits vary by plan
- **Paid tiers:** Standard, Premium, and Enterprise tiers; pricing not publicly listed; contact https://envoy.com/pricing for current rates
- **Enterprise:** Custom pricing for multi-site port deployments; volume discounts available
- **Notes:** Pricing is per location; multi-terminal port operators pay per facility location.

## Authentication

OAuth 2.0 token-based. For private (internal) apps, obtain an API token directly from the Envoy web dashboard (Visitors → Settings → Account → API key). For public apps (integrations), implement the full OAuth flow. Pass the token as `Authorization: Bearer <token>` on all API calls.

Developer portal and full OAuth documentation: `https://developers.envoy.com/hub/docs`

## Endpoints

- **Base URL:** `https://app.envoy.com/a/`
- **Key endpoints:**
  - `GET /visitors` — list visitor sign-ins
  - `GET /invites` — list pre-registered invitations
  - `POST /invites` — create a new visitor invite (pre-register a contractor)
  - `DELETE /invites/{inviteId}` — cancel an invite
  - `GET /employees` — list employees (hosts)
  - `GET /locations` — list facility locations
  - `GET /flows` — sign-in flows (visitor types with custom fields and steps)
- **Webhooks:** Subscribe to `visitor_sign_in`, `visitor_sign_out`, `invite_created`, `invite_updated`, `invite_removed` events via the Envoy developer portal

## Example call

```bash
# List all current invites (pre-registered visitors)
curl -H "Authorization: Bearer $ENVOY_TOKEN" \
  "https://app.envoy.com/a/invites"

# Pre-register a ship agent arriving tomorrow
curl -X POST \
  -H "Authorization: Bearer $ENVOY_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "data": {
      "type": "invites",
      "attributes": {
        "full_name": "Jane Smith",
        "email": "jsmith@shippingagent.com",
        "expected_arrival_time": "2026-05-15T08:00:00Z"
      }
    }
  }' \
  "https://app.envoy.com/a/invites"
```

```python
import requests

headers = {"Authorization": f"Bearer {ENVOY_TOKEN}"}

# Get today's sign-ins
sign_ins = requests.get(
    "https://app.envoy.com/a/visitors",
    headers=headers,
).json()
for visitor in sign_ins.get("data", []):
    print(visitor["attributes"].get("full_name"), visitor["attributes"].get("signed_in_at"))
```

## Rate limits

Not publicly documented. Contact Envoy developer support for rate limit policies applicable to your plan tier.

## SDKs / Libraries

- **Official:** Node.js Integrations SDK — https://github.com/envoy/envoy-integrations-sdk-nodejs
- **Community:** Brivo integration (auto-provision access credentials on check-in); Slack integration; Salesforce AppExchange connector

## Documentation

- Developer hub: https://developers.envoy.com/hub/docs/intro
- API reference: https://developers.envoy.com/hub/reference
- Integrations directory: https://envoy.com/product/integrations/

## Notes

- Envoy integrates natively with major PACS platforms (Brivo, Lenel, Genetec, HID) to provision door access credentials automatically when a visitor checks in — this is the primary integration pattern for port gatehouse automation.
- The Envoy kiosk iPad app supports custom sign-in flows including document signing (NDAs, safety briefings), ID scanning, photo capture, and watchlist checking — configure via the dashboard, not the API.
- Envoy's watchlist feature can be configured to flag visitors against internal deny lists; for maritime port use, combine with sanctioned-vessel databases or sanctions checks (`opensanctions.md`) via webhook-triggered lookups.
- Envoy March 2026 product release added new workplace reservation APIs — check the changelog at `envoy.com/workplace-management/whats-new-at-envoy-march-2026-product-releases` for current feature availability.
