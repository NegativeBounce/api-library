# Datalastic Vessels Ownership API

REST endpoint returning vessel ownership information — beneficial owners, operators, and managers — with self-service API access.

**Tier:** Paid
**Auth:** API Key
**Last researched:** 2026-06-11

## Use cases

- Looking up beneficial owner, operator, and manager for a vessel as part of broker/owner due diligence.
- Reverse-searching by beneficial owner name to enumerate associated vessels.
- Adding lightweight ownership enrichment to an existing Datalastic AIS integration without a new vendor.

## Pricing

- **Free tier:** None (14-day trial on subscription plans).
- **Paid tiers:** Subscription with monthly credit/request package (Starter, Experimenter, Developer, Pro+). Ownership calls draw from the same monthly request pool; 10% annual discount.
- **Enterprise:** Pro+ / contact sales.
- **Notes:** One API key grants access to all endpoints. Overuse protection: failed/empty queries don't deduct credits.

## Authentication

API key delivered by email on subscription. Passed as `api-key` query parameter.

## Endpoints

- **Base URL:** `https://api.datalastic.com/api`
- **Key endpoints:**
  - `GET /maritime_reports/ownership` — vessel ownership (beneficial owner, operator, manager); filter by `beneficial_owner` or vessel identifier.

## Example call

```bash
curl "https://api.datalastic.com/api/maritime_reports/ownership?api-key=$DATALASTIC_API_KEY&beneficial_owner=Steamship"
```

```python
import requests

r = requests.get(
    "https://api.datalastic.com/api/maritime_reports/ownership",
    params={"api-key": "$DATALASTIC_API_KEY", "imo": "9811000"},
)
ownership = r.json()
```

## Rate limits

Defined by the monthly request package of the chosen plan (credit-based). 1 request typically = 1 credit; failed queries are not charged.

## SDKs / Libraries

- **Official:** None language-specific; REST/JSON, documented for any language.
- **Community:** None notable.

## Documentation

- Main docs: https://datalastic.com/vessels-ownership-api/
- API reference: https://datalastic.com/api-reference/

## Notes

- **Cross-reference:** Datalastic's primary entry is in `maritime-ais` (AIS positions, ports, historical). This entry covers the distinct **ownership** report endpoint; the same API key and credit pool apply.
- Ownership depth is moderate (owner/operator/manager) — lighter than MarineTraffic/Lloyd's/S&P full ownership trees, but self-service and developer-friendly with fast key issuance.
- Good mid-tier option: more programmatic than Equasis, cheaper/faster to onboard than enterprise providers.
