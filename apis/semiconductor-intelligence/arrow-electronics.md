# Arrow Electronics API

REST API providing pricing, availability, and order placement against Arrow Electronics and Verical inventory pools.

**Tier:** Free
**Auth:** API Key + Login (query parameters)
**Last researched:** 2026-05-12

## Use cases

- Search Arrow's distributor inventory for semiconductor part availability and tier pricing
- Pull real-time stock across Arrow's geographic inventory pools (NAC, Asia, Europe, Verical)
- Place orders programmatically against an Arrow account (separate Order API key)
- Cross-reference distributor sourcing for components carried by Arrow vs. Mouser/Digi-Key

## Pricing

- **Free tier:** Free with registration via the API key request form. No published per-minute or per-day rate limits; Arrow's stated policy is that default limits are sufficient for nearly all use cases.
- **Paid tiers:** None
- **Enterprise:** Negotiated separately for high-volume / partner integrations — contact api@arrow.com
- **Notes:** Response caching is explicitly forbidden by the Terms of Use and will result in credential revocation. The Pricing & Availability API and Order API require separate API keys. A Quote API is "coming soon" per Arrow's portal.

## Authentication

Request keys at https://developers.arrow.com/api/index.php/site/page?view=requestAPIKey. Authentication is by passing `login=<login>` and `apikey=<key>` as URL query parameters on every request.

## Endpoints

- **Base URL:** `https://api.arrow.com/itemservice/v4/`
- **Key endpoints (Pricing & Availability):**
  - `GET /en/search/token` — search parts by keyword/token, returns pricing + inventory across configured pools
  - `GET /en/detail` — part detail by manufacturer code + part number, or by `pkey`
- **Inventory pools:** NAC, Asia, Europe, Verical, AE Petsche, Power & Signal. Your API key is configured for a specific subset of pools.

## Example call

```bash
curl "https://api.arrow.com/itemservice/v4/en/search/token?\
login=$ARROW_LOGIN&\
apikey=$ARROW_API_KEY&\
search_token=BAV99&\
rows=10"
```

```python
import requests, urllib.parse
part = urllib.parse.quote("STM32F407VGT6", safe="")
resp = requests.get(
    "https://api.arrow.com/itemservice/v4/en/search/token",
    params={
        "login": ARROW_LOGIN,
        "apikey": ARROW_API_KEY,
        "search_token": part,
        "rows": 10,
    },
)
print(resp.json()["itemserviceresult"]["data"][0]["PartList"])
```

## Rate limits

Not publicly published. Arrow's stated policy: no fixed per-hour/per-minute/per-IP rate limits, but abusive usage results in credential revocation. Caching responses is forbidden.

## SDKs / Libraries

- **Official:** None
- **Community:** Limited; most integrations roll their own HTTP clients

## Documentation

- Developer portal: https://developers.arrow.com/api/
- Getting started: https://developers.arrow.com/api/index.php/site/page?view=gettingStarted
- Pricing & Availability docs: https://developers.arrow.com/api/index.php/site/page?view=Itemservice
- Best practices: https://developers.arrow.com/api/index.php/site/page?view=bestPractices
- Request a key: https://developers.arrow.com/api/index.php/site/page?view=requestAPIKey

## Notes

- All part numbers must be URL-encoded, even those containing already-escaped characters (e.g., `RMC-1/8-1K-1%`).
- Wildcard searches are not allowed by default — contact Arrow for special cases.
- Tier pricing is exposed via `resaleList` arrays under each source in the response.
- Customer-specific contract pricing surfaces under `customerSpecificPricing` if your Arrow account has it.
- Arrow's API is less documented and less mature than Nexar, Mouser, or Digi-Key — expect more friction for first-time integration.
