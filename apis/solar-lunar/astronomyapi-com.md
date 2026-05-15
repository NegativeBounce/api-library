# AstronomyAPI.com

REST API for celestial body positions, sun and moon rise/set events, moon phases, and star/constellation chart imagery, queried by observer coordinates and date.

**Tier:** Freemium
**Auth:** HTTP Basic Auth (Application ID + Application Secret, base64-encoded)
**Last researched:** 2026-05-15

## Use cases

- Compute sun and moon rise/set times for any latitude/longitude up to 366 days per query
- Get planetary positions (RA/Dec and Alt/Az) for stargazing apps
- Generate embeddable moon phase and constellation star chart images
- Power astronomy widgets in web/mobile apps

## Pricing

- **Free tier:** Available after signup (create an Application in the dashboard); rate-limited by IP and overall consumption — exact request quota Not publicly documented
- **Paid tiers:** Not publicly documented; higher-volume access requires emailing contact@astronomyapi.com
- **Enterprise:** Contact sales
- **Notes:** Pricing details are not on the public site; users sign up to a free account and request higher limits as needed

## Authentication

Create an account at astronomyapi.com, then create an Application in the dashboard to receive an `Application ID` and `Application Secret` (the secret is shown only once at creation). Base64-encode the string `applicationId:applicationSecret` and pass it in the `Authorization: Basic <encoded>` header. Set an `Origin` value matching your domain if calling from a browser (CORS).

## Endpoints

- **Base URL:** `https://api.astronomyapi.com/api/v2`
- **Key endpoints:**
  - `GET /bodies` — List supported celestial bodies (Sun, Moon, planets)
  - `GET /bodies/positions` — Iterable list of body positions for a date range
  - `GET /bodies/positions/{body}` — Position of a specific body across a date range (Alt/Az + RA/Dec)
  - `GET /bodies/events/{body}` — Rise/set/transit events for a body over a date range (up to 366 days per query)
  - `POST /studio/moon-phase` — Generate moon phase image
  - `POST /studio/star-chart` — Generate constellation/area star chart image

## Example call

```bash
AUTH=$(echo -n "$APP_ID:$APP_SECRET" | base64)
curl -H "Authorization: Basic $AUTH" \
  "https://api.astronomyapi.com/api/v2/bodies/events/moon?latitude=40.7128&longitude=-74.0060&elevation=10&from_date=2026-05-15&to_date=2026-05-22&time=12:00:00"
```

```python
import base64, requests

auth = base64.b64encode(f"{APP_ID}:{APP_SECRET}".encode()).decode()
resp = requests.get(
    "https://api.astronomyapi.com/api/v2/bodies/events/moon",
    headers={"Authorization": f"Basic {auth}"},
    params={
        "latitude": 40.7128, "longitude": -74.0060, "elevation": 10,
        "from_date": "2026-05-15", "to_date": "2026-05-22", "time": "12:00:00",
    },
)
print(resp.json())
```

## Rate limits

Enforced per IP and based on overall API consumption — exact per-minute or per-month numbers are Not publicly documented. Heavy use returns HTTP 429; users requiring high volume should email contact@astronomyapi.com.

## SDKs / Libraries

- **Official:** JavaScript widgets library at `https://widgets.astronomyapi.com/cdn/astronomy-api-widgets.js`; sample code on GitHub at `AstronomyAPI/Documentation`
- **Community:** Multiple unofficial Node and Python wrappers on GitHub and npm

## Documentation

- Main docs: https://docs.astronomyapi.com/
- API reference: https://docs.astronomyapi.com/endpoints/bodies

## Notes

- Moon phase orientation depends on hemisphere; use the `orientation` parameter to override.
- Rate-limit specifics are not on the public site — plan for some trial-and-error or contact the vendor for production volume.
- Sample code and live demos at https://demo.astronomyapi.com/.
