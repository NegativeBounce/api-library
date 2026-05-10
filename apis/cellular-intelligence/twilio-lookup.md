# Twilio Lookup

Real-time phone number intelligence API by Twilio. Validates numbers, returns line type (mobile / landline / fixed-VoIP / non-fixed-VoIP / toll-free), carrier (with MCC/MNC), and optional advanced data packages: SIM Swap, Call Forwarding, Identity Match, Caller Name, SMS Pumping Risk, Reassigned Number.

**Tier:** Paid (free Basic Lookup + per-request paid packages)
**Auth:** Account SID + Auth Token (HTTP Basic Auth) or API Key/Secret
**Last researched:** 2026-05-09

## Use cases

- Verifying user-supplied phone numbers at signup with carrier + line-type info
- Fraud detection: SIM-swap detection, call-forwarding checks, identity match
- Filtering out non-fixed VoIP for high-risk SMS workflows
- Pre-validating numbers before sending OTP/marketing SMS to reduce undelivered cost
- Reverse-lookup CNAM (caller name) for inbound call routing

## Pricing

- **Free tier:** Basic Lookup (formatting + validity) is free.
- **Paid tiers:** Per-request charges by data package. Line Type Intelligence ~$0.008/lookup; Carrier ~$0.005 (legacy v1); Caller Name and other packages priced separately. Pricing varies by region and is on the Twilio Lookup product page.
- **Enterprise:** Volume discounts via Twilio sales; SIM Swap and Identity Match require carrier approvals via private beta enrollment.
- **Notes:** Some packages (SIM Swap, Reassigned Number) are private beta; Canada Line Type Intelligence requires special approval.

## Authentication

Create a Twilio account at twilio.com to get an Account SID and Auth Token. Use HTTP Basic Auth (`-u SID:TOKEN` in curl) or generate scoped API Key + Secret in the Twilio Console for production.

## Endpoints

- **Base URL:** `https://lookups.twilio.com/v2`
- **Key endpoints:**
  - `GET /PhoneNumbers/{E164Number}` — Basic Lookup (free)
  - `GET /PhoneNumbers/{E164Number}?Fields=line_type_intelligence` — line-type + carrier
  - `GET /PhoneNumbers/{E164Number}?Fields=sim_swap,call_forwarding,identity_match,caller_name,sms_pumping_risk,reassigned_number` — premium fields (separately priced; require enrollment)

## Example call

```bash
curl -X GET "https://lookups.twilio.com/v2/PhoneNumbers/+14159929960?Fields=line_type_intelligence" \
  -u "$TWILIO_ACCOUNT_SID:$TWILIO_AUTH_TOKEN"
```

```python
from twilio.rest import Client
client = Client(account_sid, auth_token)
phone = client.lookups.v2.phone_numbers("+14159929960").fetch(
    fields="line_type_intelligence")
print(phone.line_type_intelligence)
```

## Rate limits

Per-account default of 100 RPS for Lookup v2; can be raised by request. No published per-day fixed cap — billing-controlled.

## SDKs / Libraries

- **Official:** Twilio SDKs for Node, Python, Java, C#, PHP, Ruby, Go.
- **Community:** `twlu` Rust CLI, many third-party CRM/anti-fraud integrations.

## Documentation

- Main docs: https://www.twilio.com/docs/lookup/v2-api
- Quickstart: https://www.twilio.com/docs/lookup/quickstart
- Product page (with current pricing): https://www.twilio.com/en-us/user-authentication-identity/lookup
- Migration v1 → v2: https://www.twilio.com/docs/lookup/v1-api

## Notes

- v1 is legacy but still supported; new development should target v2 for Twilio Regions support and the advanced data packages.
- Carrier coverage for advanced packages (SIM Swap, Identity Match, Call Forwarding) is concentrated in North America, Europe, and Latin America.
- Twilio also offers Verify (OTP) and Voice — Lookup pairs with these for end-to-end auth flows.
