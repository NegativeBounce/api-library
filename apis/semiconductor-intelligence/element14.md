# Element14 / Farnell / Newark Product Search API

REST (and SOAP) API for searching the Farnell/Newark/element14 catalog of 1.3M+ parts across regions (EMEA + Japan, Americas, APAC).

**Tier:** Free
**Auth:** API Key (Search) / JWT Bearer (Order)
**Last researched:** 2026-05-12

## Use cases

- Search the unified Farnell/Newark/element14 catalog by keyword, order code, or manufacturer part number
- Pull regional pricing and inventory across EMEA, Americas, and APAC stores
- Retrieve datasheets, images, packaging options, RoHS/compliance flags, and lead times
- Programmatically place and manage orders via the separate Order API

## Pricing

- **Free tier:** Free with registration. No published per-minute rate limits for Product Search; Order API has rate limits "designed to support normal transaction volumes."
- **Paid tiers:** None
- **Enterprise:** Trade-account / iBuy users contact the eProcurement team for elevated Order API access
- **Notes:** Search API and Order API require separate API keys. Three regional brands (Farnell/Newark/element14) share a unified catalog but have distinct order endpoints.

## Authentication

Register at https://partner.element14.com/member/register and link to your Farnell/Newark/element14 trade account. You receive a 24-character alphanumeric API key.
- **Product Search API:** API key passed as query parameter `callInfo.apiKey=<key>`
- **Order API:** JWT Bearer authentication; obtain a token via the Generate JWT endpoint (30-minute validity)
- **Contract pricing:** Requires additional `customerId`, `signature`, and `dateTimeStamp` URL parameters computed from a Secret Key

## Endpoints

- **Base URL (Product Search):** `https://api.element14.com/`
- **Order endpoints:** `https://api.farnell.com` (EMEA + Japan), `https://api.newark.com` (Americas), `https://api.element14.com` (APAC)
- **Key endpoints (Product Search):**
  - `GET /catalog/products?term=any:<keyword>&storeInfo.id=<store>` — keyword search
  - `GET /catalog/products?term=manuPartNum:<mpn>&storeInfo.id=<store>` — search by manufacturer part number
  - `GET /catalog/products?term=id:<order_code>&storeInfo.id=<store>` — search by Farnell/Newark/element14 order code
- **Response groups:** `small` (default), `medium`, `large`, `prices`, `inventory`

## Example call

```bash
curl "https://api.element14.com/catalog/products?\
term=manuPartNum:STM32F407VGT6\
&storeInfo.id=uk.farnell.com\
&resultsSettings.offset=0\
&resultsSettings.numberOfResults=10\
&resultsSettings.responseGroup=large\
&callInfo.responseDataFormat=JSON\
&callInfo.apiKey=$ELEMENT14_API_KEY"
```

```python
import requests
resp = requests.get(
    "https://api.element14.com/catalog/products",
    params={
        "term": "any:STM32F407",
        "storeInfo.id": "uk.farnell.com",
        "resultsSettings.numberOfResults": 10,
        "resultsSettings.responseGroup": "large",
        "callInfo.responseDataFormat": "JSON",
        "callInfo.apiKey": ELEMENT14_API_KEY,
    },
)
print(resp.json())
```

## Rate limits

Not publicly published for the Product Search API. Order API rate limits exist but specific numbers are not disclosed — Farnell states they are "designed to support normal transaction volumes." JWT tokens for the Order API expire after 30 minutes.

## SDKs / Libraries

- **Official:** Interactive Swagger / Playground at https://partner.element14.com/io-docs
- **Community:** `pyFarnell` (https://pyfarnell.readthedocs.io/) — unofficial Python wrapper

## Documentation

- Partner portal: https://partner.element14.com/
- Product Search REST docs: https://partner.element14.com/docs/read/Product_Search_API_REST__Description
- Order API: https://partner.element14.com/order
- Order API FAQ: https://partner.element14.com/order/FAQs
- Interactive playground: https://partner.element14.com/io-docs

## Notes

- Three regional brands: Farnell (EMEA + Japan), Newark (Americas), element14 (APAC). Same API surface, different `storeInfo.id` and order endpoints.
- Contract Pricing requires a Secret Key plus a signature calculation that references the legacy SOAP function name — not a clean REST flow.
- API supports both REST (production) and SOAP (BETA) for Product Search.
- Reliable for European and APAC sourcing where Mouser/Digi-Key have less inventory.
