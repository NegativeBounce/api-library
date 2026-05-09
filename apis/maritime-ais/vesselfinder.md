# VesselFinder

AIS data API offering real-time and historical vessel positions, voyage data, port calls, and master particulars. Credit-based purchase model with subscription options for predefined vessel lists or geofenced areas.

**Tier:** Paid
**Auth:** API Key
**Last researched:** 2026-05-09

## Use cases

- Tracking a known fleet of vessels through the Strait via the **VesselsList** subscription (predefined MMSI list, flat fee).
- Continuous monitoring of vessels inside a Strait of Malacca bounding box via **LiveData** subscription.
- Ad-hoc, credit-based queries for individual vessels, port arrivals, or shortest-route calculations.
- Historical track replay and port-call investigation.
- Containerized cargo tracking via the separate `container.vesselfinder.com` API.

## Pricing

- **Free tier:** None on the AIS API. Free public web app exists for casual use only.
- **Paid tiers:** Credit packages from €330 (10,000 credits) up to €1,470 (50,000 credits). Credits are valid 12 months. Per-call cost varies by endpoint (e.g., MasterData ~3 credits/vessel; Vessels 1 or 10 credits depending on freshness).
- **Subscription methods (`VesselsList`, `LiveData`):** Flat fee, scoped to a customer-defined fleet or area; not credit-deducting.
- **Enterprise:** Custom contracts available for large feeds.
- **Notes:** Prices exclude VAT. Container Tracking API caches each lookup for 12 hours.

## Authentication

API key issued after account purchase, passed as `?userkey=...` query parameter (and `apikey` on the container API).

## Endpoints

- **Base URL:** `https://api.vesselfinder.com/`
- **Key endpoints:**
  - `GET /vessels` — Vessels (real-time data per MMSI/IMO)
  - `GET /masterdata` — MasterData (vessel particulars)
  - `GET /portcalls` — PortCalls (arrivals/departures)
  - `GET /expectedarrivals` — Vessels expected at a port
  - `GET /distance` — Shortest sea route between waypoints
  - **Subscription:** `vesselslist`, `livedata`
- **Container API:** `https://container.vesselfinder.com/api/1.0/`

## Example call

```bash
curl "https://api.vesselfinder.com/vessels?userkey=$API_KEY&mmsi=566093000&format=json"
```

## Rate limits

Not published as global limits; throttling tied to credit balance and subscription scope. Container API enforces a 12-hour cache per shipment to discourage polling.

## SDKs / Libraries

- **Official:** None.
- **Community:** Several JS/Python wrappers on GitHub (none widely adopted).

## Documentation

- Main docs: https://api.vesselfinder.com/docs/
- Container API: https://container.vesselfinder.com/api/1.0/docs
- FAQ: https://api.vesselfinder.com/docs/faq.html

## Notes

- Independent of MarineTraffic/Kpler and Spire — distinct ownership and AIS receiver network.
- The credit model rewards bursty patterns (snapshot of fleet positions on demand) over continuous high-frequency tracking. For continuous Strait monitoring, the `LiveData` subscription is more cost-effective.
- Useful as a second-source feed alongside MarineTraffic for cross-validation of vessel positions and master data.
