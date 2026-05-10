# OpenSky Network

Non-profit, research-oriented ADS-B / Mode S aggregator hosted in Switzerland. Operates a global network of feeders, providing free live API access to states/positions/flights and free historical access to academic researchers via a Trino SQL interface. The most-cited public ADS-B dataset in academic aviation research.

**Tier:** Free (research-oriented; institutional researchers get unlimited access)
**Auth:** OAuth2 client credentials → Bearer token
**Last researched:** 2026-05-10

## Use cases

- Live state-vector queries for academic, hobbyist, or non-commercial use
- Historical ADS-B research via Trino SQL (multi-year archive, state_vectors_data4 has unlimited retention)
- Flight detection / arrival / departure events by airport ICAO code
- Aircraft trajectory reconstruction (waypoint extraction with smart filtering)
- Reproducible aviation research — OpenSky publishes citable datasets (COVID-19 dataset, etc.)
- Emergency / squawk-code monitoring (7700, 7600, 7500)

## Pricing

- **Free tier:** Free for non-commercial / research use. Public REST API has rate limits; institutional researchers can request unlimited access via account application demonstrating research need.
- **Paid tiers:** None.
- **Enterprise:** Commercial use requires `contact@opensky-network.org` for licensing terms.
- **Notes:** AWS and other hyperscaler IPs are routinely blocked due to abuse — host your scripts on a residential or institutional IP.

## Authentication

OAuth2 client credentials grant. Register at opensky-network.org, generate a client_id (ends in `-api-client`) and client_secret in your account profile. Exchange these for a Bearer token via Keycloak; tokens expire after 30 minutes.

```bash
export TOKEN=$(curl -X POST "https://auth.opensky-network.org/auth/realms/opensky-network/protocol/openid-connect/token" \
  -d "grant_type=client_credentials" \
  -d "client_id=$CLIENT_ID" -d "client_secret=$CLIENT_SECRET" | jq -r .access_token)
```

## Endpoints

- **Base URL:** `https://opensky-network.org/api`
- **Key endpoints:**
  - `GET /states/all` — all current state vectors (rate-limited; supports `time`, `icao24`, bounding-box `lamin/lomin/lamax/lomax`)
  - `GET /states/own` — own-receiver state vectors (no rate limit, requires shared receiver)
  - `GET /flights/all?begin={epoch}&end={epoch}` — flights in a time interval
  - `GET /flights/aircraft?icao24={hex}&begin={epoch}&end={epoch}` — flights by aircraft
  - `GET /flights/arrival?airport={ICAO}&begin={epoch}&end={epoch}` — arrivals at an airport
  - `GET /flights/departure?airport={ICAO}&begin={epoch}&end={epoch}` — departures from an airport
  - `GET /tracks?icao24={hex}&time={epoch}` — experimental trajectory waypoints
  - **Trino historical interface** (separate access, granted by admin) — direct SQL on `state_vectors_data4`, `flights_data4`, ADS-B raw tables (`identification_data4`, `position_data4`, `velocity_data4`, etc.)

## Example call

```bash
# Current state vectors over Switzerland (bounding box)
curl -H "Authorization: Bearer $TOKEN" \
  "https://opensky-network.org/api/states/all?lamin=45.83&lomin=5.99&lamax=47.82&lomax=10.52" \
  | jq .

# Departures from Frankfurt (EDDF) in a 1-hour window
curl -H "Authorization: Bearer $TOKEN" \
  "https://opensky-network.org/api/flights/departure?airport=EDDF&begin=1517227200&end=1517230800"
```

```python
# Python via pyopensky / traffic library (recommended)
from pyopensky.rest import REST
rest = REST(username=USER, password=PASS)
arrivals = rest.arrival("LFBO", "2026-05-09 20:00", "2026-05-10 06:00")
```

## Rate limits

- **Anonymous / unauthenticated:** Severe rate limits (functional but small request budget).
- **Authenticated (default):** Higher limits but still capped per minute for `/states/all`.
- **Institutional researcher:** Unlimited access on request, including Trino historical access.
- **Trino:** Max query duration 30 minutes (queue + execution). Always filter on the partition column (`hour` for state_vectors_data4, `day` for flights_data4) — unpartitioned scans get accounts suspended.

## SDKs / Libraries

- **Official:** Python (`opensky-api` and successor `pyopensky`), Java bindings.
- **Community:** `traffic` (Python, recommended for trajectory analysis), R packages, MATLAB toolboxes, and many Jupyter notebooks demonstrating Trino queries.

## Documentation

- Main API docs: https://openskynetwork.github.io/opensky-api/
- REST API reference: https://openskynetwork.github.io/opensky-api/rest.html
- Trino historical: https://openskynetwork.github.io/opensky-api/trino.html
- Project home: https://opensky-network.org/
- Data page: https://opensky-network.org/data
- FAQ: https://opensky-network.org/about/faq

## Notes

- **Citation required.** Any publication using OpenSky data must cite the original Schäfer et al. paper ("Bringing Up OpenSky", 2014). Per ToS.
- Trino access is **separate** from REST API access — granted on application basis by administrators, evaluated for research merit.
- `state_vectors_data4` is the most commonly used table; has **unlimited retention** (years of data). Other tables retain ~1 year only.
- Some historical periods have data gaps due to outages — exclude them from research samples per the Trino docs.
- Live API does NOT include commercial flight metadata (schedules, delays, passenger counts) — only what's directly derivable from ADS-B/Mode S.
- AWS / hyperscaler IP blocking is real — host scripts on institutional or residential IPs.
- Cross-listing: complementary to ADS-B Exchange (different ethos — research vs. unfiltered tracking) and adsb.fi (community-driven). Most-cited dataset for academic aviation research.
