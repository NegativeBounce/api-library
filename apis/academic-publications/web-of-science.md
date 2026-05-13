# Web of Science API (Clarivate)

Clarivate's Web of Science citation database API providing bibliographic metadata, citation counts, journal metrics, and researcher profiles from the Web of Science Core Collection.

**Tier:** Freemium
**Auth:** API Key
**Last researched:** 2026-05-13

## Use cases

- Retrieving cited-by counts and times-cited data for bibliometric analysis
- Searching the Web of Science Core Collection for peer-reviewed literature with citation impact metrics
- Building article-level citation links and widgets that display authoritative WoS citation counts

## Pricing

- **Free tier (Starter API):**
  - Free Trial: no WoS subscription required; 50 requests/day; no times-cited data
  - Institutional Member: requires active WoS subscription; 5,000 requests/day; includes times-cited
  - Institutional Integration: high-volume institutional use; 20,000 requests/day
- **Paid tiers:**
  - Web of Science API Expanded: full metadata retrieval, cited references, related records; requires paid license — contact institutional library
  - Journals API: journal-level metrics including Journal Impact Factor (JIF); separate license required
- **Enterprise:** Contact Clarivate for committed-use pricing and SLA
- **Notes:** All tiers beyond the Free Trial require an active Web of Science subscription. The Starter API replaces the legacy Web of Science API Lite.

## Authentication

Register an application at https://developer.clarivate.com to obtain an API key. Pass as `X-ApiKey: <KEY>` header on all requests.

## Endpoints

- **Base URL:** `https://api.clarivate.com/apis/wos-starter/v1/` (Starter API)
- **Key endpoints (Starter API):**
  - `GET /documents` — search documents; params: `q` (WoS query string), `db`, `limit`, `page`, `sortField`
  - `GET /documents/{uid}` — single document by WoS UID
  - `GET /journals` — journal metadata search

**Expanded API** (separate license): additional endpoints for cited references, related records, citing articles, and full author/affiliation metadata.

**WoS query syntax examples:** `TS=(large language model) AND PY=2024 AND DT=Article`

## Example call

```bash
curl -H "X-ApiKey: $WOS_API_KEY" \
  "https://api.clarivate.com/apis/wos-starter/v1/documents?q=TS%3D(transformer+attention)+AND+PY%3D2024&limit=25"
```

```python
import requests

resp = requests.get(
    "https://api.clarivate.com/apis/wos-starter/v1/documents",
    headers={"X-ApiKey": WOS_API_KEY},
    params={"q": "TS=(transformer attention) AND PY=2024", "limit": 25},
)
for doc in resp.json().get("hits", []):
    print(doc["title"], doc.get("citations", {}).get("count"))
```

## Rate limits

| Plan | Requests/Second | Requests/Day |
|---|---|---|
| Free Trial | 1 | 50 |
| Institutional Member | 5 | 5,000 |
| Institutional Integration | 5 | 20,000 |

Expanded API rate limits are governed by institutional license terms.

## SDKs / Libraries

- **Official:** None — REST API only; Swagger/OpenAPI spec available via developer portal
- **Community:** `wos` (Python, third-party); `wosr` (R)

## Documentation

- Developer portal: https://developer.clarivate.com/apis
- Starter API: https://developer.clarivate.com/apis/wos-starter
- Expanded API: https://developer.clarivate.com/apis/wos
- API descriptions guide: https://clarivate.libguides.com/librarianresources/APIs_descriptions

## Notes

- Times-cited counts are the primary differentiator from free alternatives; these are only available with an active WoS institutional subscription.
- Web of Science coverage is selective and curated (~21,000 peer-reviewed journals) — smaller than Scopus or OpenAlex by record count but considered authoritative for citation impact analysis.
- For researchers without institutional WoS access, OpenAlex (`openalex.md`) and Semantic Scholar (`semantic-scholar.md`) provide open citation data at no cost.
- The Journals API (separate license) provides Journal Impact Factor (JIF) and other JCR metrics — contact Clarivate for pricing.
- WoS UID format: `WOS:000123456789012` — stable identifier usable across API calls and exports.
