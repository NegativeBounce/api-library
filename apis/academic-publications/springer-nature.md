# Springer Nature API

Springer Nature's developer API providing metadata search, abstract retrieval, and full-text access to 3+ million articles across scientific journals and books in life sciences, materials science, engineering, mathematics, and physics.

**Tier:** Freemium
**Auth:** API Key
**Last researched:** 2026-05-13

## Use cases

- Searching Springer and Nature journal metadata and abstracts for scientific literature pipelines
- Retrieving full-text content from open-access Springer Nature publications for text mining
- Building institution-scale literature discovery tools with access to subscriber content via the TDM API

## Pricing

- **Free tier:** Open Access API and Meta API — free with registered API key; 100 hits/minute
- **Paid tiers:**
  - Premium API — higher rate limits and multiple key support; pricing not publicly listed (contact sales)
  - Full Text API (TDM) — requires active Springer Nature subscription or institutional license
- **Enterprise:** Institutional licensing via Springer Nature Data Solutions; contact datasolutions.springernature.com
- **Notes:** Free tier covers open-access content only. Subscription-only full text requires the TDM API under an institutional agreement. Downloading at scale without a TDM agreement violates Springer Nature's terms.

## Authentication

Register at https://dev.springernature.com to obtain a free API key. Pass as `?api_key=<KEY>` query parameter on all requests.

## Endpoints

- **Base URL:** `https://api.springernature.com/`
- **Key endpoints:**
  - `GET /openaccess/json` — open-access article metadata and full text in JSON
  - `GET /openaccess/jats` — open-access full text in JATS XML format
  - `GET /meta/v2/json` — metadata and abstracts for all Springer Nature content (subscription + OA); JSON
  - `GET /meta/v2/pam` — metadata in PRISM/PAM XML format

**Common query parameters:** `q` (query string), `p` (page size, default 10, max 100), `s` (start index), `subject`, `journal`, `year`, `country`, `type`

## Example call

```bash
curl "https://api.springernature.com/openaccess/json?q=large+language+model&p=25&api_key=$SN_API_KEY"
```

```python
import requests

resp = requests.get(
    "https://api.springernature.com/openaccess/json",
    params={"q": "large language model", "p": 25, "api_key": SN_API_KEY},
)
for record in resp.json().get("records", []):
    print(record["title"], record["publicationName"], record.get("openAccess"))
```

## Rate limits

Free tier: 100 requests per minute per API key. Premium tier: higher limits (not publicly documented). Rate limit details: https://dev.springernature.com/docs/rate-limit-details/rate-limits/

## SDKs / Libraries

- **Official:** None — REST API only
- **Community:** Third-party Python wrappers; R packages available via CRAN

## Documentation

- Developer portal: https://dev.springernature.com
- Open Access API docs: https://dev.springernature.com/docs/api-endpoints/open-access/
- Introduction: https://dev.springernature.com/docs/introduction/

## Notes

- The Open Access API (free) returns full-text content only for articles published as open access — not all Springer Nature content.
- The Meta API (free) returns metadata and abstracts for all Springer Nature content but requires a subscription to view full text on the publisher's site.
- Springer Nature journals include Nature, Scientific Reports, Nature Communications, and 2,900+ specialist titles — coverage is strongest in life sciences and physical sciences.
- The API supports 20+ filtering dimensions including subject area, journal, country, publication type, and date range.
- The TDM (Text and Data Mining) API is intended for large-scale text mining under institutional agreements; contact Springer Nature Data Solutions for access and terms.
