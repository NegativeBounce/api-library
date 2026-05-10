# ESA DISCOSweb

ESA Space Debris Office's "Database and Information System Characterising Objects in Space" — physical characteristics (mass, shape, dimensions, cross-section, RCS) for ~70k+ trackable objects in Earth orbit. The complement to TLEs: TLEs say *where*, DISCOS says *what*.

**Tier:** Free (operational-need account required)
**Auth:** Bearer token (per-account API key) + version header
**Last researched:** 2026-05-09

## Use cases

- Looking up physical properties (mass, dimensions, cross-section, RCS) of any cataloged object
- Conjunction-risk modeling — pairing DISCOS object size with TLE state vectors
- Re-entry prediction inputs (mass + ballistic coefficient context)
- Liability and ownership analysis (country, operator, launch info)
- Mission design — comparing mass / shape / cross-section across analog spacecraft

## Pricing

- **Free tier:** Free of charge for operational and research use. Account application via email demonstrating operational need.
- **Paid tiers:** None.
- **Enterprise:** N/A — ESA public-good service.
- **Notes:** Account application reviewed by ESA Space Debris Office staff; expect a few business days. The legacy "DISCOSweb Operations API" (Basic Auth) is being phased out in favor of the public DISCOSweb API (Bearer token).

## Authentication

Register a Space Debris User Account at `account.sdo.esoc.esa.int`, then apply for DISCOSweb access via email to `space.debris.support@esa.int` with operational need justification. Once approved, generate an API token in the user portal. Pass:
- `Authorization: Bearer <YOUR_TOKEN>`
- `DiscosWeb-Api-Version: 2`

## Endpoints

- **Base URL:** `https://discosweb.esoc.esa.int`
- **Key endpoints:**
  - `GET /api/objects` — paginated list of all objects (filterable by `satno`, `cosparId`, `country`, `objectClass`, etc.)
  - `GET /api/objects/{discosId}` — single object by DISCOS internal ID
  - `GET /api/objects?filter[satno]=25544` — query by NORAD ID
  - `GET /api/launches` — launch records
  - `GET /api/launch-systems` — launch vehicle data
  - `GET /api/initial-orbits` — initial orbit info per object
  - `GET /api/fragmentation-events` — known on-orbit breakups

## Example call

```bash
curl "https://discosweb.esoc.esa.int/api/objects/39634" \
  -H "Authorization: Bearer $DISCOSWEB_TOKEN" \
  -H "DiscosWeb-Api-Version: 2"
# → JSON with satno, cosparId, name, objectClass, mass, shape, dimensions, xSect*, country, etc.
```

```python
import requests
HEADERS = {
    "Authorization": f"Bearer {api_token}",
    "DiscosWeb-Api-Version": "2",
}
r = requests.get("https://discosweb.esoc.esa.int/api/objects",
                 params={"page[number]": 1, "page[size]": 60},
                 headers=HEADERS)
data = r.json()  # JSON:API format with data[].attributes
```

## Rate limits

Recommended cap is ~20 requests/minute per token. Default page size is 30 (max 100). Polite paginated reads + caching are expected. Account suspension is possible for abuse.

## SDKs / Libraries

- **Official:** None (REST + JSON:API spec is well-documented).
- **Community:** `DiscosWebSdk` (C#, NuGet), Python helper scripts (`omerfkeles/space-debris-liability`, etc.), various Jupyter notebooks demonstrating bulk pulls.

## Documentation

- DISCOSweb portal: https://discosweb.esoc.esa.int/
- Space Debris User Account: https://account.sdo.esoc.esa.int/
- API specification: available after login under DISCOSweb → API
- ESA Space Debris page: https://www.esa.int/Space_Safety/Space_Debris
- Status of services paper (SDC7): https://conference.sdo.esoc.esa.int/proceedings/sdc7/paper/712/SDC7-paper712.pdf

## Notes

- Output uses JSON:API conventions — every object has `data.id`, `data.type`, `data.attributes`. Pagination via `links.next`.
- "Old" Operations API at `discosweb-api.sdo.esoc.esa.int` is deprecated but still up; new code should target the v2 public API.
- Coverage includes payloads, rocket bodies, and debris from every catalogued launch since Sputnik.
- Cross-listing: complementary to `satellite-imagery` (mass + dimensions + ID), `gnss-interference` (jam-source attribution research).
