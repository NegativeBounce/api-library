# EOS Risk Group

UK-headquartered global security risk and crisis-management practice providing maritime intelligence, situational security alerts, voyage/port risk assessments, and analyst-led investigations.

**Tier:** Enterprise
**Auth:** Login (portal / subscription)
**Last researched:** 2026-06-11

> **Advisory + intelligence service, not a self-serve data API.** Outputs are alerts, reports, and analyst products delivered via subscription/portal; integration is arranged per contract.

## Use cases

- Real-time situational security alerts for high-risk waters (Red Sea, Bab el Mandeb, Gulf of Aden, Strait of Hormuz) — EOS is an active marsec alerting voice.
- Voyage and port risk assessments for transit planning and underwriting support.
- Bespoke risk reporting by region/theme and analyst-led investigations (ownership networks, deceptive shipping, sanctions exposure).
- Crisis management and response support for incidents at sea.

## Pricing

- **Free tier:** Some public social/alert content; substantive intelligence is subscription/contract.
- **Paid tiers:** Subscription to intelligence/advisory products (not publicly priced).
- **Enterprise:** Bespoke advisory, embedded analysts, investigations — contact sales.
- **Notes:** Pricing not public. Mix of recurring intelligence subscriptions and project-based consultancy.

## Authentication

Portal login / subscription credentials provisioned per contract. No documented public self-serve API.

## Endpoints

- **Base URL:** No public API. Service portal + reporting (see eosrisk.com).
- **Key surfaces:**
  - Situational security alerts (push/feed to subscribers).
  - Voyage & port risk assessments (analyst products).
  - Bespoke risk reports; investigations.

## Example call

```bash
# No public self-serve API. Alerts/reports delivered via subscription/portal;
# any data integration is arranged per contract.
```

## Rate limits

N/A (analyst/advisory delivery). Per contract if a feed is provisioned.

## SDKs / Libraries

- **Official:** None.
- **Community:** None.

## Documentation

- Main docs: https://eosrisk.com/marine/intelligence-advisory/
- Advisory overview: https://eosrisk.com/advisory/

## Notes

- Strong operational reporting cadence in the Red Sea / Gulf of Aden theatre; useful as an expert-analysis layer over raw AIS and incident feeds.
- Differentiator vs. data providers is **analyst-led** intelligence and investigations rather than programmatic data.
- Cross-reference: pairs with the official reporting centres (`maritime-security/ukmto.md`, `maritime-security/recaap-isc.md`) and with dark-vessel/risk data (e.g. `dark-vessel-detection/windward.md`) for a fuller picture.
- Confirm whether an alert feed/API integration is available for your build during sales scoping.
