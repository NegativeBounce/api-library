# EPO Open Patent Services (OPS)

The European Patent Office's RESTful web service giving programmatic access to worldwide patent data — bibliographic records, full text, patent families, legal status, classification, citations, and document images.

**Tier:** Freemium
**Auth:** OAuth 2.0 (Bearer token)
**Last researched:** 2026-05-14

## Use cases

- Retrieve worldwide patent families for a U.S. semiconductor patent to see where a competitor (a foundry or fabless designer) has filed equivalents across the EPO, JPO, KIPO, and CNIPA
- Run CQL searches on `/published-data/search` for CPC H01L combined with applicant names to track European and PCT semiconductor filing activity
- Monitor legal status of key semiconductor patents (lapses, oppositions, grants) across jurisdictions to support freedom-to-operate and licensing decisions

## Pricing

- **Free tier:** "Non-paying" — ~4 GB of data traffic per week (sufficient for most single-researcher workloads)
- **Paid tiers:** "Paying" — €2,800 per year for effectively unlimited traffic volume
- **Enterprise:** Handled via the paid commercial agreement; no separate published enterprise tier. Contact EPO for bulk needs.
- **Notes:** The free quota is measured in data volume (GB), not request count — large full-text or image pulls consume it fast, while bibliographic searches are cheap. EPO also offers bulk data products (DOCDB, EP full-text) separately from OPS.

## Authentication

OAuth 2.0 client-credentials grant. Register at https://developers.epo.org/ and create an app to receive a Consumer Key and Consumer Secret. POST the base64-encoded `key:secret` to the access-token endpoint (`/3.2/auth/accesstoken`) to get a Bearer token (short-lived, ~20 min), then send `Authorization: Bearer <token>` on all service calls.

## Endpoints

- **Base URL:** `https://ops.epo.org/3.2/rest-services`
- **Key endpoints:**
  - `GET /published-data/search` — CQL search across published patent data (returns result lists)
  - `GET /published-data/search/biblio` — search returning bibliographic data inline
  - `GET /published-data/{ref-type}/{format}/{number}/biblio` — bibliographic data for a specific publication
  - `GET /published-data/.../fulltext`, `/claims`, `/description` — full-text constituents (coverage varies by jurisdiction)
  - `GET /family/{ref-type}/{format}/{number}` — INPADOC patent family data
  - `GET /legal/...` — INPADOC legal status events
  - `GET /classification/cpc/...` — CPC classification data and search

## Example call

```bash
# 1. Get an access token
curl -X POST 'https://ops.epo.org/3.2/auth/accesstoken' \
  -H 'Authorization: Basic <BASE64(consumer_key:consumer_secret)>' \
  -H 'Content-Type: application/x-www-form-urlencoded' \
  -d 'grant_type=client_credentials'

# 2. Search published data by CPC class H01L
curl -G 'https://ops.epo.org/3.2/rest-services/published-data/search/biblio' \
  --data-urlencode 'q=cpc="H01L"' \
  -H 'Authorization: Bearer YOUR_ACCESS_TOKEN' \
  -H 'Accept: application/json'
```

```python
import requests, base64

key, secret = "CONSUMER_KEY", "CONSUMER_SECRET"
tok = requests.post(
    "https://ops.epo.org/3.2/auth/accesstoken",
    headers={"Authorization": "Basic " + base64.b64encode(f"{key}:{secret}".encode()).decode()},
    data={"grant_type": "client_credentials"},
).json()["access_token"]

r = requests.get(
    "https://ops.epo.org/3.2/rest-services/published-data/search/biblio",
    params={"q": 'cpc="H01L"'},
    headers={"Authorization": f"Bearer {tok}", "Accept": "application/json"},
)
print(r.json())
```

## Rate limits

Governed by a fair-use quota system, not a fixed requests-per-minute cap. Quota status is reported as green (<50%), yellow (50–75%), red (>75%), black (blocked). Two dimensions are enforced: a per-hour individual quota and a per-week registered quota (~4 GB/week on the free tier). A "Data Usage" API provides historical quota stats.

## SDKs / Libraries

- **Official:** EPO provides documentation, an OPS Swagger/Developer Console, and a user reference guide; no official multi-language SDK
- **Community:** `python-epo-ops-client` (ip-tools, PyPI — the most widely used; handles OAuth + throttling); `epo-ops` Go client; `Rops` R client; `epo-cli` Go CLI; PatZilla uses OPS as a data source

## Documentation

- Main docs: https://www.epo.org/en/searching-for-patents/data/web-services/ops
- Developer portal / API reference & console: https://developers.epo.org/

## Notes

- Default response format is XML; JSON is available on many endpoints via `Accept: application/json`, but XML is the most complete/reliable.
- Access tokens are short-lived (~20 min) — implement refresh logic.
- The free weekly quota is measured in data volume — large full-text or image pulls consume it fast; keep searches bibliographic where possible.
- Full-text coverage is uneven across jurisdictions (strong for EP, US, WO; partial for others).
- Terms of use restrict redistribution of bulk OPS data — review the EPO OPS usage terms before building a commercial product.
- v3.2 is the current version; watch for version bumps that change the base path.
