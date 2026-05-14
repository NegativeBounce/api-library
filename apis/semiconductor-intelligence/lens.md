# Lens.org API

REST API from The Lens (Cambia) providing unified programmatic search across a global patent corpus (~150M+ records) and scholarly works (~270M+), with rich linkage between patents, scholarship, applicants, and classifications.

**Tier:** Freemium
**Auth:** Bearer Token
**Last researched:** 2026-05-14

## Use cases

- Build a semiconductor IP landscape by searching the patent corpus on `class_cpc.symbol:H01L*` and aggregating by applicant, jurisdiction, and year — across US, EP, WO, CN, JP, and KR in one query
- Link semiconductor patents to the underlying scholarly literature (e.g., papers cited as non-patent literature in EUV or 2D-materials patents) to trace science-to-technology flow
- Track a competitor's global semiconductor portfolio, its patent families, and legal status, and export structured datasets for periodic landscape monitoring

## Pricing

- **Free tier:** "Trial" — free, valid 14 days from approval, for non-commercial or limited academic use; 5,000 API requests/month, up to 5,000,000 records/month, 10 requests/minute, 1,000 records/request, ~45 search fields
- **Paid tiers:** "Member / Custom Access" — negotiated subscription for institutions/companies; higher quotas, continued access, automated downloads, commercial use, 120+ search fields. Pricing is quote-based / not publicly listed
- **Enterprise:** Handled under the same Custom Access process; Lens also offers a fee-waived Academic Workspace and a fee-bearing Professional Workspace (platform, not API)
- **Notes:** PatSeq bulk downloads are a separate product.

## Authentication

Bearer token. Request access via your Lens account profile ("API and Data" tab) and complete the service request form; access is granted after manual review. On approval, generate access tokens (max 5 per user, each valid ~1 year). Send as `Authorization: Bearer <token>` for POST requests, or `?token=<token>` for GET requests.

## Endpoints

- **Base URL:** `https://api.lens.org`
- **Key endpoints:**
  - `POST|GET /patent/search` — search the patent corpus (POST with JSON query body, or GET with query params)
  - `POST|GET /scholarly/search` — search scholarly works
  - `GET /collections/...` — manage and query saved Lens collections
- **Request body supports:** `query`, `sort`, `include` (field selection), `size`, `from`, and `scroll`/`scroll_id` for cursor pagination

## Example call

```bash
curl -X POST 'https://api.lens.org/patent/search' \
  -H 'Authorization: Bearer YOUR_TOKEN' \
  -H 'Content-Type: application/json' \
  -d '{
        "query": "class_cpc.symbol:H01L*",
        "size": 50,
        "include": ["lens_id","biblio.invention_title","biblio.parties.applicants","date_published"]
      }'
```

```python
import requests

url = "https://api.lens.org/patent/search"
headers = {"Authorization": "Bearer YOUR_TOKEN", "Content-Type": "application/json"}
body = {
    "query": {"bool": {"must": [
        {"match": {"class_cpc.symbol": "H01L"}},
        {"range": {"date_published": {"gte": "2020-01-01"}}},
    ]}},
    "size": 100,
    "scroll": "1m",
    "include": ["lens_id", "biblio.invention_title", "biblio.parties.applicants"],
}
r = requests.post(url, json=body, headers=headers)
print(r.json())
```

## Rate limits

Enforced and reported via response headers (`x-rate-limit-remaining-request-per-minute`, `-per-month`, `x-rate-limit-remaining-record-per-month`); exceeding returns HTTP 429. Trial plan: 10 requests/minute, 5,000 requests/month, 5,000,000 records/month, 1,000 records per request. Offset pagination (`from`/`size`) is capped at 10,000 records; use cursor-based `scroll` for larger result sets. Paid-plan limits are higher and negotiated per subscription.

## SDKs / Libraries

- **Official:** None — Lens provides REST docs and a Swagger UI (https://api.lens.org/swagger-ui.html)
- **Community:** Various community wrappers exist on GitHub/PyPI, but none is an officially endorsed, well-maintained standard — verify maintenance status before adopting. Most users call the REST API directly.

## Documentation

- Main docs: https://docs.api.lens.org/
- Getting started: https://docs.api.lens.org/getting-started.html
- Knowledge base / access plans: https://support.lens.org/knowledge-base/lens-patent-and-scholar-api/

## Notes

- Access is gated by manual approval — there is a review/turnaround delay, and trial access is explicitly time-boxed to 14 days, so it is not suitable for a long-running free integration.
- The query language is a modified Elasticsearch Query DSL — powerful but with a learning curve; supports both structured JSON queries and a compact `query_string` syntax. CPC reserved characters like `/` must be backslash-escaped in query-string syntax.
- The trial exposes only ~45 of the 120+ search fields, which can limit landscape-depth analysis until you move to a paid plan.
- Paid pricing is opaque (quote-based) — budget uncertainty for procurement.
- Strong selling point for semiconductor IP work: patent–scholarly linkage and broad global jurisdiction coverage in a single API, which PatentsView (US-only) and EPO OPS (patents-only) don't combine.
