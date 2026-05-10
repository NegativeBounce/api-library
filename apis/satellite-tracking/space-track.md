# Space-Track.org

Authoritative US Space Force / 18th Space Defense Squadron public catalog of orbital data. Source-of-truth for SSN-derived TLEs, OMMs, SATCAT, decay/reentry, and Conjunction Data Messages (CDMs). Free with US-government registration and acceptable-use compliance.

**Tier:** Free (registered users only)
**Auth:** Username + password (form-based session login → cookie)
**Last researched:** 2026-05-09

## Use cases

- Authoritative TLE / OMM data for any unclassified catalogued object (including 6-digit / Alpha-5 / 9-digit IDs)
- Pulling personalized CDM feeds for your fleet (when registered as an operator)
- Decay / reentry predictions (TIP messages)
- Satellite catalog (SATCAT) bulk pulls + change history
- Launch site catalog, boxscore by country, organization registry

## Pricing

- **Free tier:** Free for registered users. US-government public service; users must agree to USSPACECOM acceptable use policy.
- **Paid tiers:** None.
- **Enterprise:** N/A — same free service applies. Operators get Owner-Operator data access on request (CDMs for their assets).
- **Notes:** Account suspension is enforced for repeat AUP violations. Multiple accounts to circumvent rate limits is explicitly prohibited.

## Authentication

Register at `www.space-track.org`. Authentication is session-based: POST username + password to `/ajaxauth/login`, receive a session cookie, include it on subsequent requests. The cookie expires; re-auth as needed. There is no API token / OAuth flow.

## Endpoints

- **Base URL:** `https://www.space-track.org`
- **Key endpoints:**
  - `POST /ajaxauth/login` — login (form fields: `identity`, `password`)
  - `GET /basicspacedata/query/class/gp/format/json` — current GP data (TLE/OMM)
  - `GET /basicspacedata/query/class/gp_history/...` — historical GP data
  - `GET /basicspacedata/query/class/satcat/...` — satellite catalog
  - `GET /basicspacedata/query/class/decay/...` — decay records
  - `GET /basicspacedata/query/class/tip/...` — Tracking & Impact Predictions (reentry)
  - `GET /basicspacedata/query/class/launch_site/...` — launch sites
  - `GET /basicspacedata/query/class/boxscore/...` — country/org payload counts
  - `GET /expandedspacedata/query/class/cdm_public/...` — public CDM feed
  - `GET /expandedspacedata/query/class/cdm/...` — owner/operator CDMs (auth-gated)
  - REST predicates support comma-delimited lists, comparison operators (`>now-3`), `orderby`, `limit`, `format` (json/xml/csv/tle/3le/kvn/stream)

## Example call

```bash
# 1. Login (cookie jar required)
curl -c st.cookies -b st.cookies \
  -X POST "https://www.space-track.org/ajaxauth/login" \
  -d "identity=$ST_USER&password=$ST_PASS"

# 2. Get the latest TLE for the ISS (NORAD 25544) in 3LE format
curl -b st.cookies \
  "https://www.space-track.org/basicspacedata/query/class/gp/NORAD_CAT_ID/25544/format/3le"
```

```python
# Python — official library is unofficial: `spacetrack` on PyPI
from spacetrack import SpaceTrackClient
st = SpaceTrackClient(identity=ST_USER, password=ST_PASS)
recent = st.gp(norad_cat_id=[25544, 25541],
               epoch='>now-3', orderby='epoch desc',
               format='json')
```

## Rate limits

**Hard limits, strictly enforced:**
- ≤ 30 requests per minute
- ≤ 300 requests per hour

Plus a "data retrieval rate" guideline that prohibits repeatedly issuing one-satellite-per-request loops over hundreds of objects — combine with comma-delimited lists.

## SDKs / Libraries

- **Official:** None.
- **Community:** `spacetrack` (Python, Read-the-Docs hosted, sync + async via aiohttp), `spacetrack-client` (Java, Maven Central), `benelsen/spacetrack` (Node.js), `nkoshell/space-track-api` (Python helper), many internal in-house wrappers.

## Documentation

- Main site: https://www.space-track.org/
- API documentation (login required for full): https://www.space-track.org/documentation
- Python `spacetrack` library: https://spacetrack.readthedocs.io/
- Java client: https://github.com/stevenpaligo/spacetrack-client

## Notes

- Catalog formats now include Alpha-5 (240,000 more IDs in fixed-width TLE) and 9-digit modern OMM — current code should handle both gracefully.
- USSPACECOM provides "express blanket approval" for redistribution of basic SSA data with appropriate citations; analytical publications must cite USSPACECOM as source.
- Outages of Space-Track cascade to CelesTrak (which depends on it) — Aug 2025 outage caused major catalog gaps for ~3 days.
- Owner/operator features (private CDMs, etc.) require additional vetting via your organization's Space-Track account admin.
- Cross-listing: complementary to `satellite-imagery` (collection planning), `gnss-interference` (GNSS satellite orbits + decay/maneuver context).
