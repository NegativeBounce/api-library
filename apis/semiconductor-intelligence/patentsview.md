# USPTO PatentsView API

Free REST API from the USPTO providing programmatic search and retrieval of U.S. granted patents and pre-grant publications, including bibliographic, classification, assignee, inventor, and citation data.

**Tier:** Free
**Auth:** API Key (`X-Api-Key` header)
**Last researched:** 2026-05-14

## Use cases

- Pull all U.S. granted patents under CPC class H01L (semiconductor devices) filed in the last 10 years to map filing-volume trends across the sector
- Identify and rank the top assignees (e.g., TSMC, Samsung, Intel, ASML) within CPC subclasses like H01L 21/ (semiconductor manufacturing processes) for competitive landscape analysis
- Build inventor and citation networks for a specific semiconductor technology (e.g., EUV lithography, gate-all-around transistors) by combining the patents endpoint with U.S. patent citation data

## Pricing

- **Free tier:** Entirely free; no data-volume charges. The only constraint is the rate limit.
- **Paid tiers:** None
- **Enterprise:** N/A
- **Notes:** Free, public-domain U.S. government data; no licensing restrictions on use.

## Authentication

API key passed in the `X-Api-Key` HTTP header. Keys are requested via a form on the PatentsView site (https://patentsview.org/apis/keyrequest) and delivered by email. **Note:** new API key grants have been temporarily suspended pending migration to the USPTO Open Data Portal — check the docs for current status.

## Endpoints

- **Base URL:** `https://search.patentsview.org/api/v1`
- **Key endpoints:**
  - `GET|POST /patent/` — search granted patents (bibliographic data, dates, titles, abstracts)
  - `GET|POST /publication/` — search pre-grant publications
  - `GET|POST /cpc_class/`, `/cpc_subclass/`, `/cpc_group/` — look up CPC classification entities (e.g., enumerate the H01L hierarchy)
  - `GET|POST /assignee/`, `/inventor/`, `/location/` — disambiguated entity endpoints
  - `GET|POST /us_patent_citations/`, `/us_application_citations/` — citation data
  - `GET|POST /g_claims/`, `/g_brf_sum_texts/` — granted-patent full-text constituents
- **Request params:** `q` (query JSON), `f` (fields array), `s` (sort), `o` (options, e.g. pagination/size)

## Example call

```bash
curl -G 'https://search.patentsview.org/api/v1/patent/' \
  -H 'X-Api-Key: YOUR_API_KEY' \
  --data-urlencode 'q={"_and":[{"_eq":{"cpc_current.cpc_class_id":"H01L"}},{"_gte":{"patent_date":"2020-01-01"}}]}' \
  --data-urlencode 'f=["patent_id","patent_title","patent_date","assignees.assignee_organization"]' \
  --data-urlencode 'o={"size":100}'
```

```python
import requests

url = "https://search.patentsview.org/api/v1/patent/"
headers = {"X-Api-Key": "YOUR_API_KEY"}
payload = {
    "q": {"_and": [
        {"_eq": {"cpc_current.cpc_class_id": "H01L"}},
        {"_gte": {"patent_date": "2020-01-01"}},
    ]},
    "f": ["patent_id", "patent_title", "patent_date", "assignees.assignee_organization"],
    "o": {"size": 100},
}
r = requests.post(url, json=payload, headers=headers)
print(r.json())
```

## Rate limits

45 requests per minute per application — exceeding it returns HTTP 429. Default page size is 1,000 results per request; paginate via the `o` parameter (cursor/`after`-based pagination in the current API).

## SDKs / Libraries

- **Official:** None — USPTO provides REST docs and code snippets only
- **Community:** `patentsview` (R, rOpenSci, with a maintained fork updated for the PatentSearch API); `patentsview2` (Python); the PatentsView Code Snippets repo on GitHub; dltHub has a PatentsView source

## Documentation

- Main docs: https://search.patentsview.org/docs/
- API reference: https://search.patentsview.org/docs/docs/Search%20API/SearchAPIReference/
- Endpoint Dictionary: https://search.patentsview.org/docs/docs/Search%20API/EndpointDictionary/

## Notes

- Major transition: the Legacy API was discontinued May 1, 2025. On March 20, 2026, PatentsView migrates to the USPTO Open Data Portal (`data.uspto.gov`), with expected temporary service interruptions — plan for endpoint/URL changes.
- New API key issuance is currently suspended — a real blocker for new projects; check the docs page for status.
- U.S. patents only — no European/PCT coverage. For semiconductor IP that is globally filed, pair with EPO OPS or Lens.org.
- Assignees and inventors are disambiguated via PatentsView's algorithms — good for entity analysis, but introduces some normalization assumptions.
- Verify the exact CPC field name (`cpc_current.cpc_class_id`) against the live Endpoint Dictionary, as field names changed between API versions.
