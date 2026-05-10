# ADS-B Exchange

The world's largest independent unfiltered ADS-B receiver network — known for not honoring the FAA's Aircraft Tail Number Blocking list. Provides live and historical aircraft tracking data including military, state, VIP, and FAA-blocklisted flights that other commercial trackers filter out.

**Tier:** Paid (Freemium via RapidAPI personal-use; Enterprise direct)
**Auth:** RapidAPI key (header) for low-cost tier; bilateral API key for Enterprise
**Last researched:** 2026-05-10

## Use cases

- Tracking military, state, VIP, and FAA-blocklisted flights filtered out by mainstream providers
- OSINT investigations on private/government aircraft movement
- Real-time flight tracking by ICAO24 hex, registration, callsign, or geographic bounding box
- Historical ADS-B data for aviation incident research
- Verification cross-checks against filtered providers (e.g., FlightRadar24)

## Pricing

- **Free tier:** None directly. Trial limits via RapidAPI may apply.
- **Paid tiers:** RapidAPI personal-use plan from $10/month for 10,000 requests at the basic tier; multiple higher tiers available. Enthusiast use only — no bulk resale or redistribution permitted.
- **Enterprise:** Custom pricing for full-feature access (live feeds + historical files). Trusted by Fortune 500 + 70+ companies. Direct contact required for commercial license — written authorization mandatory.
- **Notes:** Acquired by JETNET (aviation data provider) in 2023. The community then forked off and started adsb.fi and airplanes.live in protest of the acquisition.

## Authentication

- **RapidAPI tier:** Sign up at rapidapi.com → subscribe to ADSBExchange.com API → use the issued `X-RapidAPI-Key` and `X-RapidAPI-Host` headers.
- **Enterprise:** Bilateral API key issued under commercial license agreement.

## Endpoints

- **Base URL (RapidAPI):** `https://adsbexchange-com1.p.rapidapi.com`
- **Base URL (Enterprise):** Customer-specific
- **Key endpoints:**
  - `GET /v2/hex/{icao24_hex}/` — single aircraft by ICAO24 hex
  - `GET /v2/icao/{hex_list}/` — multiple aircraft by ICAO24 hex (comma-separated)
  - `GET /v2/registration/{reg}/` — by tail number / registration
  - `GET /v2/callsign/{callsign}/` — by callsign
  - `GET /v2/sqk/{squawk}/` — by squawk code (e.g., 7700 emergency)
  - `GET /v2/mil/` — currently airborne military aircraft
  - `GET /v2/lat/{lat}/lon/{lon}/dist/{nm}/` — within distance (NM) of a point
  - Historical files via Enterprise (per-day archive downloads)

## Example call

```bash
curl -X GET "https://adsbexchange-com1.p.rapidapi.com/v2/lat/40.7/lon/-74.0/dist/25/" \
  -H "X-RapidAPI-Key: $RAPIDAPI_KEY" \
  -H "X-RapidAPI-Host: adsbexchange-com1.p.rapidapi.com"
```

```python
import requests
HEADERS = {
    "X-RapidAPI-Key": RAPIDAPI_KEY,
    "X-RapidAPI-Host": "adsbexchange-com1.p.rapidapi.com",
}
r = requests.get(
    "https://adsbexchange-com1.p.rapidapi.com/v2/mil/",
    headers=HEADERS)
print(r.json()["ac"])  # list of currently airborne military aircraft
```

## Rate limits

RapidAPI tier: ~10,000 requests/month at $10/month tier; higher tiers scale up. Enterprise: per-contract.

## SDKs / Libraries

- **Official:** None. RapidAPI provides auto-generated client snippets in many languages.
- **Community:** `pyadsbexchange` and various wrappers; X-Plane LiveTraffic plugin.

## Documentation

- Main data page: https://www.adsbexchange.com/data/
- API lite (personal use): https://www.adsbexchange.com/api-lite/
- Enterprise API: https://www.adsbexchange.com/products/enterprise-api/
- Sample API calls: https://www.adsbexchange.com/data/rest-api-samples/
- RapidAPI listing: https://rapidapi.com/adsbx/api/adsbexchange-com1/

## Notes

- "Unfiltered" is the value proposition: ADSBx does not honor FAA tail-number blocking lists, so military/government/VIP aircraft visible on its receiver network are visible in its data. This is the core reason it exists and the reason adsb.fi/airplanes.live forked.
- Acquisition by JETNET (a commercial aviation data company) in 2023 was controversial — many feeders left the network. Community alternatives (adsb.fi, airplanes.live, adsb.lol) absorbed much of that volume.
- v2 API endpoints are the current standard; v3 endpoints (lat/lon/dist) are the recommended new format.
- Cross-listing: complementary to OpenSky Network (research-focused) and adsb.fi (community-focused, no JETNET).
