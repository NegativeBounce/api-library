# HID Origo

HID Global's cloud platform for managing mobile access credentials — providing REST APIs for issuing, revoking, and managing digital credentials (Apple Wallet, Google Wallet, Seos) for port employee and contractor access without physical card issuance.

**Tier:** Enterprise
**Auth:** OAuth 2.0 (Bearer Token)
**Last researched:** 2026-05-14

## Use cases

- Issuing mobile access credentials to new port contractors via API immediately upon contractor onboarding, eliminating physical card production delays and card desk visits
- Revoking mobile credentials remotely when a contractor's site access is terminated or a badge is reported lost, without requiring the physical card to be returned
- Querying credential transaction logs for all HID-credential-based access events across port reader infrastructure for audit and compliance reporting

## Pricing

- **Free tier:** None — Technology Partner Program membership and HID reader infrastructure required
- **Paid tiers:** Per-credential and per-reader pricing; contact HID Global for pricing at https://www.hidglobal.com
- **Enterprise:** Enterprise licensing for large-scale port deployments; contact HID Global or an authorized distributor
- **Notes:** Production applications must complete HID certification through the Technology Partner Service program. API access is granted to enrolled Technology Partners only.

## Authentication

OAuth 2.0 Bearer token. Two methods are supported:

1. **Password-based:** `grant_type=client_credentials` with client ID and secret from a System Account in the HID Origo Management Portal
2. **Certificate-based (PKI):** JSON Web Token signed with an RSA private key — recommended for production

Token endpoint: `https://api.origo.hidglobal.com/authentication/customer/{organization_id}/token`

Token lifetime: 1 hour; expires after 5 minutes of inactivity. Re-authenticate on 401 responses.

All requests require three headers:
```
Authorization: Bearer <access_token>
Application-ID: <your-application-id>
Application-Version: <your-application-version>
```

## Endpoints

- **Base URL:** `https://api.origo.hidglobal.com`
- **Key API modules:**
  - **Mobile Identities v2.2** — manage end-user mobile identities linked to physical persons
    - `POST /identities` — create a new mobile identity
    - `GET /identities/{id}` — retrieve an identity record
    - `DELETE /identities/{id}` — delete an identity
  - **Credential Management** — issue and revoke digital credentials (Passes)
    - `POST /passes` — issue a new digital credential (Seos, Apple Wallet, Google Wallet)
    - `GET /passes/{id}` — retrieve credential status
    - `DELETE /passes/{id}` — revoke a credential
    - `PATCH /passes/{id}` — update credential (e.g., add user photo)
  - **User Management** — manage users and their associated identities
  - **Transaction Management** — query credential transaction records
  - **Events and Callbacks** — subscribe to credential lifecycle events (issued, revoked, used)

## Example call

```bash
# Get an access token (password-based)
curl -X POST \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -d "grant_type=client_credentials&client_id=$HID_CLIENT_ID&client_secret=$HID_CLIENT_SECRET" \
  "https://api.origo.hidglobal.com/authentication/customer/$ORG_ID/token"

# Issue a mobile credential to a contractor
curl -X POST \
  -H "Authorization: Bearer $HID_TOKEN" \
  -H "Application-ID: $APP_ID" \
  -H "Application-Version: $APP_VERSION" \
  -H "Content-Type: application/json" \
  -d '{
    "identityId": "identity-uuid",
    "credentialType": "seos",
    "deliveryMethod": "apple_wallet"
  }' \
  "https://api.origo.hidglobal.com/passes"
```

```python
import requests

headers = {
    "Authorization": f"Bearer {HID_TOKEN}",
    "Application-ID": APP_ID,
    "Application-Version": APP_VERSION,
}

# Revoke a credential when a contractor leaves
resp = requests.delete(
    f"https://api.origo.hidglobal.com/passes/{PASS_ID}",
    headers=headers,
)
print(resp.status_code)  # 204 on success
```

## Rate limits

Documented under "Usage Limits" in the HID Origo API portal (`doc.origo.hidglobal.com/api/`) — specific values require login to the Technology Partner documentation.

## SDKs / Libraries

- **Official:** None — REST API only; PDF specification: https://doc.origo.hidglobal.com/api/assets/pdf/ma-api-2.2.pdf
- **Community:** Feenics cloud PACS HID Origo model integration (`apidocs.feenics.com/hid-origo/`); various PACS vendor integrations via the Technology Partner Program

## Documentation

- HID Origo API documentation: https://doc.origo.hidglobal.com/api/
- Authentication guide: https://doc.origo.hidglobal.com/api/authentication/
- Mobile Identities API: https://doc.origo.hidglobal.com/api/mobile-identities/
- Credential Management API: https://doc.origo.hidglobal.com/api/credential-management/
- HID Origo Management Portal: https://portal.origo.hidglobal.com/mobile-identities/

## Notes

- HID Origo operates independently of any specific PACS vendor — it manages credential issuance and revocation, while the underlying access control decisions are made by HID-compatible readers (HID Signo, iCLASS SE, multiCLASS SE) connected to any major PACS (Genetec, Lenel, Brivo, etc.).
- Apple Wallet and Google Wallet credentials issued via HID Origo function as digital copies of Seos-encoded physical badges — port operators can mix physical HID cards and mobile credentials in the same infrastructure without reader replacement.
- User photo uploads for wallet passes must be exactly 1242×1242 px PNG format (updated in the 2026 credential management API revision).
- Google Wallet now supports multiple HID credentials stored in a single pass — relevant for contractors who need access to multiple port facilities under different operators.
- For port use: the ability to issue mobile credentials via API immediately on contractor onboarding removes the physical card desk bottleneck, which is particularly valuable for frequent short-duration port visitors (ship crew members, surveyors, customs inspectors).
