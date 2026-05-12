# Digi-Key API (Product Information V4)

REST API suite covering product search, pricing, ordering, and supply chain operations against Digi-Key Electronics' catalog of millions of components.

**Tier:** Free
**Auth:** OAuth 2.0 (2-legged or 3-legged)
**Last researched:** 2026-05-12

## Use cases

- Search semiconductor parts by keyword, part number, manufacturer, or category for BOM tooling
- Pull real-time pricing, inventory, lifecycle status, and product change notifications
- Find substitutions and alternate packages when primary parts are out of stock
- Automate ordering and order status tracking against a Digi-Key business account

## Pricing

- **Free tier:** Free with registration. Sandbox (`sandbox-api.digikey.com`) and Production (`api.digikey.com`) environments. Default ~1,000 requests/day; community libraries report ~120 req/min ceiling.
- **Paid tiers:** None
- **Enterprise:** Higher-volume access negotiated directly with Digi-Key for suppliers/partners — contact your Digi-Key account rep
- **Notes:** Sandbox returns valid-shape data but may not match production data exactly. Customer-specific pricing requires the `X-DIGIKEY-Customer-Id` header matching the authenticated account.

## Authentication

OAuth 2.0 framework. TLS 1.2 required. Register an application at https://developer.digikey.com to obtain `client_id` and `client_secret`.
- **2-legged (client credentials)** — for public data (product search, pricing). Easier setup.
- **3-legged (authorization code)** — required for customer-specific pricing, orders, and account-level operations. OAuth callback can be `https://localhost` during development.

## Endpoints

- **Base URL:** `https://api.digikey.com` (Production) / `https://sandbox-api.digikey.com` (Sandbox)
- **Token URL:** `https://api.digikey.com/v1/oauth2/token`
- **Key endpoints (Product Information V4):**
  - `POST /products/v4/search/keyword` — keyword search with filters
  - `GET /products/v4/search/{productNumber}/productdetails` — full part details
  - `GET /products/v4/search/manufacturers` — list manufacturers
  - `GET /products/v4/search/categories` — category tree
  - `POST /products/v4/search/{productNumber}/recommendedproducts` — recommended/related parts
  - `POST /products/v4/search/{productNumber}/substitutions` — drop-in alternatives
  - `GET /products/v4/search/{productNumber}/media` — datasheets, images, CAD
  - `POST /products/v4/search/productpricing` — bulk pricing queries
  - Order API and Order Status API available as separate product subscriptions

## Example call

```bash
# 1. Get OAuth token (2-legged)
curl -X POST "https://api.digikey.com/v1/oauth2/token" \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -d "client_id=$DIGIKEY_CLIENT_ID&client_secret=$DIGIKEY_CLIENT_SECRET&grant_type=client_credentials"

# 2. Search for a part
curl -X POST "https://api.digikey.com/products/v4/search/keyword" \
  -H "Authorization: Bearer $DIGIKEY_TOKEN" \
  -H "X-DIGIKEY-Client-Id: $DIGIKEY_CLIENT_ID" \
  -H "X-DIGIKEY-Locale-Site: US" \
  -H "X-DIGIKEY-Locale-Language: en" \
  -H "X-DIGIKEY-Locale-Currency: USD" \
  -H "Content-Type: application/json" \
  -d '{"Keywords": "STM32F407VGT6", "Limit": 10}'
```

```python
# Python via community wrapper:  pip install digikey-api
import os, digikey
from digikey.v3.productinformation import KeywordSearchRequest
os.environ["DIGIKEY_CLIENT_ID"] = "..."
os.environ["DIGIKEY_CLIENT_SECRET"] = "..."
result = digikey.keyword_search(body=KeywordSearchRequest(keywords="STM32F407", record_count=10))
```

## Rate limits

- ~1,000 requests per day per application (default)
- ~120 requests per minute (per community Go client implementations)
- Response headers (`X-RateLimit-Limit`, `X-RateLimit-Remaining`) communicate current consumption
- HTTP 429 when exceeded

## SDKs / Libraries

- **Official:** Java and C# client libraries on Digi-Key's GitHub, Postman OAuth2 collections for Sandbox and Production (linked from developer.digikey.com/resources)
- **Community:** `digikey-api` Python package (https://github.com/peeter123/digikey-api), Go client `PatrickWalther/go-digikey`, many others

## Documentation

- Developer portal: https://developer.digikey.com
- Documentation: https://developer.digikey.com/documentation
- API reference (V4): https://developer.digikey.com/products/product-information-v4
- FAQ: https://developer.digikey.com/faq

## Notes

- V3 of the API is being phased out; V4 (Product Information V4) is current. New integrations should target V4.
- Required headers include `X-DIGIKEY-Client-Id` and locale headers (Site, Language, Currency, ShipToCountry) for accurate pricing.
- Sandbox has the same shape as production but data may be incomplete or stale.
- Customer-specific contract pricing requires 3-legged OAuth plus a `X-DIGIKEY-Customer-Id` header matching the authenticated Digi-Key account.
