# Mouser Electronics API

REST API for searching Mouser's electronic component catalog and managing carts/orders programmatically.

**Tier:** Free
**Auth:** API Key (query parameter)
**Last researched:** 2026-05-12

## Use cases

- Look up semiconductor parts by keyword, part number, or manufacturer for procurement automation
- Pull real-time stock, pricing, and lead-time data from Mouser's inventory
- Build cart and place orders programmatically against a Mouser business account
- Track order history and status for ERP/MRP integrations

## Pricing

- **Free tier:** Free for all registered Mouser account holders. 30 requests/minute, 1,000 requests/day per key.
- **Paid tiers:** None
- **Enterprise:** Not applicable; same API for all users
- **Notes:** Separate API keys are issued for the Search API vs. the Cart/Order APIs. Cart/Order keys require a billing and shipping address on your Mouser account.

## Authentication

Register at https://www.mouser.com/api-hub/ with a My Mouser account. Generate separate API keys for the Search API and Cart/Order APIs. The key is passed as a query parameter `apiKey=<key>` on every request.

## Endpoints

- **Base URL:** `https://api.mouser.com/api/v1/`
- **Key endpoints:**
  - `POST /search/keyword` — keyword search across the catalog
  - `POST /search/partnumber` — exact / fuzzy part-number search
  - `POST /search/keywordandmanufacturer` — keyword + manufacturer filter
  - `POST /search/manufacturerlist` — list of supported manufacturers
  - `POST /cart/{cartKey}` — manage Mouser shopping carts
  - `POST /order/{orderNumber}` — submit and check orders

## Example call

```bash
curl -X POST "https://api.mouser.com/api/v1/search/partnumber?apiKey=$MOUSER_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "SearchByPartRequest": {
      "mouserPartNumber": "STM32F407VGT6",
      "partSearchOptions": "Exact"
    }
  }'
```

```python
import requests
resp = requests.post(
    f"https://api.mouser.com/api/v1/search/keyword?apiKey={MOUSER_API_KEY}",
    json={"SearchByKeywordRequest": {
        "keyword": "STM32F407",
        "records": 10,
        "startingRecord": 0,
    }},
)
print(resp.json())
```

## Rate limits

- 30 requests per minute per API key
- 1,000 requests per day per API key
- HTTP 429 returned on overage

## SDKs / Libraries

- **Official:** None
- **Community:** `mouser-api` Python package (https://github.com/sparkmicro/mouser-api), Go client `PatrickWalther/go-mouser`, various others on GitHub.

## Documentation

- API hub / sign-up: https://www.mouser.com/api-hub/
- API guide PDF: https://www.mouser.com/pdfDocs/api-guide.pdf
- Interactive explorer: https://api.mouser.com/api/docs/ui/index (may require JS-enabled browser)

## Notes

- Mouser uses Akamai bot protection on its main site; direct scraping is blocked, but the API is the supported programmatic path.
- The API Explorer page is **not** a sandbox — any orders created go against your real account.
- Pricing returned varies by user/account location (geo-based pricing).
- Search API is the typical entry point for research/intelligence work; Cart/Order APIs are for active procurement workflows only.
