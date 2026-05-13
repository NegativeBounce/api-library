# NTSB CAROL (Crash Cause and Occurrence Reporting On-Line)

US National Transportation Safety Board's public accident database covering aviation, railroad, highway, pipeline, and marine accidents investigated by the NTSB — searchable via the CAROL web interface and a developing REST API.

**Tier:** Free
**Auth:** None (web); API Key (partner/developer access)
**Last researched:** 2026-05-13

## Use cases

- Searching NTSB marine accident investigation reports and probable cause determinations
- Retrieving accident narratives, factual reports, and docket documents for specific marine incidents
- Building automated pipelines to monitor new NTSB marine investigations and safety recommendations

## Pricing

- **Free tier:** Full CAROL search interface and docket access are free with no registration
- **Paid tiers:** None
- **Enterprise:** N/A
- **Notes:** The NTSB developer API program (aviation and safety recommendations currently available) is expanding to marine; contact NTSB for partner access.

## Authentication

No authentication required for the CAROL web interface and docket search. The developer REST API (aviation-first, marine migration in progress) requires an API key from the NTSB developer portal.

## Endpoints

- **CAROL search:** `https://data.ntsb.gov/carol-main-public/basic-search` — web search interface for all NTSB-investigated accidents
- **Docket search:** `https://data.ntsb.gov/Docket/forms/Searchdocket` — access to investigation docket documents (factual reports, exhibits, transcripts)
- **Developer portal:** `https://developer.ntsb.gov/` — REST API access (aviation endpoint confirmed; marine migration in progress as of 2026-05-13)

**Marine REST API:** Migration from legacy system in progress as of 2026-05-13. Aviation accident API is available; marine accident API endpoints were not yet confirmed at time of research. Check `https://developer.ntsb.gov/` for current status.

## Example call

```bash
# CAROL marine search — web form submission (no direct API endpoint confirmed for marine)
# Check developer portal for current marine API endpoint availability
curl -s "https://developer.ntsb.gov/" -H "User-Agent: Mozilla/5.0"
```

```python
import requests

# Aviation endpoint example (pattern expected for marine when available)
# Replace 'aviation' with marine endpoint slug when released
resp = requests.get(
    "https://developer.ntsb.gov/api/aviation/accidents",
    headers={"api-key": NTSB_API_KEY},
    params={"startDate": "2024-01-01", "endDate": "2024-12-31", "category": "marine"},
)
print(resp.json())
```

## Rate limits

Developer API rate limits not publicly documented; check the developer portal for current terms. The CAROL web interface has no published rate limit but is not designed for high-frequency automated access.

## SDKs / Libraries

- **Official:** None
- **Community:** None confirmed for marine; community wrappers exist for the aviation data (check PyPI for `ntsb`)

## Documentation

- CAROL search: https://data.ntsb.gov/carol-main-public/basic-search
- Docket search: https://data.ntsb.gov/Docket/forms/Searchdocket
- Developer portal: https://developer.ntsb.gov/
- NTSB marine investigations: https://www.ntsb.gov/investigations/Pages/marine.aspx

## Notes

- NTSB investigates significant marine accidents in US waters and involving US-flag vessels abroad; coverage is selective (major accidents only), unlike USCG which has broader incident reporting.
- As of 2026-05-13, the marine REST API migration was in progress — the aviation API was confirmed operational; marine endpoints were not yet available at the developer portal.
- CAROL full-text search covers investigation reports back to the 1960s; the docket system provides supporting documents for investigations from approximately 2000 onward.
- Each NTSB marine investigation produces: preliminary report, factual report, probable cause report, and safety recommendations — all available via CAROL docket.
- For broader US marine incident data (including minor accidents), use USCG MISLE data (`uscg-marine-casualty.md`) which covers all Coast Guard-reported incidents.
- NTSB safety recommendations are tracked in a separate database also accessible via the developer portal (aviation API confirmed; marine in progress).
