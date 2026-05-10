# adsb.fi

Community-driven, open ADS-B aggregator launched after the JETNET acquisition of ADS-B Exchange. ~5,400+ feeders worldwide; provides free, unfiltered access for personal/non-commercial use. API is intentionally compatible with ADSBExchange v2 to ease migration.

**Tier:** Free (personal/non-commercial)
**Auth:** None for public endpoints; feeder IP whitelisted for feeder-only endpoints
**Last researched:** 2026-05-10

## Use cases

- Free real-time aircraft tracking with no API key required
- ADSBExchange v2 API replacement (drop-in for personal projects)
- Community ADS-B data without corporate ownership or filtering
- Hobbyist OSINT, plane spotting, route research, photography planning

## Pricing

- **Free tier:** Fully free for personal/non-commercial use. 1 request/second rate limit on public endpoints; 1 request/30 seconds on feeder-only endpoints.
- **Paid tiers:** None publicly listed. Higher rate limits and commercial use available via direct contact.
- **Enterprise:** Contact site maintainers for commercial agreements.
- **Notes:** Cannot license, sell, rent, or lease the data per ToS. Must cite adsb.fi and link to the home page when using data.

## Authentication

No authentication for public endpoints. Feeder-IP is automatically given access to additional endpoints if you contribute data via a Raspberry-Pi-based ADS-B receiver feeding adsb.fi.

## Endpoints

- **Base URL:** `https://opendata.adsb.fi/api/`
- **Key endpoints:**
  - `GET /v2/hex/{icao24}` — single aircraft by ICAO24 hex
  - `GET /v2/icao/{hex_list}` — multiple aircraft (comma-separated hex)
  - `GET /v2/callsign/{callsign}` — by callsign
  - `GET /v2/reg/{registration}` — by tail number
  - `GET /v2/sqk/{squawk}` — by squawk
  - `GET /v2/mil` — currently airborne military
  - `GET /v3/lat/{lat}/lon/{lon}/dist/{nm}` — within distance of point (preferred over deprecated v2)
  - Feeder-only endpoints (whitelisted by IP, available to contributors)

## Example call

```bash
# Aircraft by hex
curl https://opendata.adsb.fi/api/v2/hex/461E1A

# Multiple by ICAO24
curl https://opendata.adsb.fi/api/v2/icao/461E1A,4ACA0B

# Within 25 NM of Helsinki (v3)
curl https://opendata.adsb.fi/api/v3/lat/60.3179/lon/24.9496/dist/25
```

```python
import requests
r = requests.get("https://opendata.adsb.fi/api/v3/lat/40.7/lon/-74.0/dist/25")
aircraft = r.json().get("ac", [])
print(f"{len(aircraft)} aircraft within 25 NM of NYC")
```

## Rate limits

- Public endpoints: **1 request/second**
- Feeder endpoints: **1 request/30 seconds**

Exceeding these may result in suspension. No published per-day cap.

## SDKs / Libraries

- **Official:** None — REST endpoints are simple enough that wrappers are usually unnecessary.
- **Community:** Compatible with any ADSBExchange v2 client (drop-in base URL change). Listed in `rickstaa/awesome-adsb`. ADSB Feeder Image (`adsb.im`) supports adsb.fi as a target aggregator.

## Documentation

- Project home: https://adsb.fi/
- API specification: https://github.com/adsbfi/opendata/blob/main/README.md
- Live globe view: https://globe.adsb.fi/
- Community lists (awesome-adsb): https://github.com/rickstaa/awesome-adsb

## Notes

- Founded as a direct response to ADS-B Exchange's acquisition by JETNET — emphasis on community ownership and open data.
- API surface is intentionally compatible with ADSBExchange v2 to make migration trivial.
- Data is unfiltered — does not honor FAA tail-number blocking, similar to ADS-B Exchange's original ethos.
- Feeder hardware: Raspberry Pi + RTL-SDR + 1090 MHz antenna; install via the adsb.fi feeder script or the ADSB Feeder Image.
- Cross-listing: alternatives in same ecosystem are airplanes.live, adsb.lol, ADS-B One. All forked or stood up around the 2023 JETNET acquisition.
