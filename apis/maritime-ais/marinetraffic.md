# MarineTraffic

Global AIS vessel tracking platform (now part of Kpler) offering real-time vessel positions, port calls, voyage forecasts, and historical AIS data via REST APIs from 13,000+ AIS receivers across 190 countries.

**Tier:** Enterprise
**Auth:** API Key (query parameter)
**Last researched:** 2026-05-09

## Use cases

- Real-time tracking of vessels transiting the Strait of Malacca via Vessel Position services (PS01/PS02).
- Port-call alerts for Singapore, Port Klang, Tanjung Pelepas, and Belawan to confirm transit and dwell times.
- Voyage forecasts (predicted ETA/destination) for vessels approaching the Strait, useful for handover planning.
- Historical AIS replay for incident investigation (e.g., reconstructing a piracy event timeline).
- Density-map services for hot-spot analysis of fishing/military activity around the Strait.

## Pricing

- **Free tier:** None for the API. The marinetraffic.com web map is free for casual use only.
- **Paid tiers:** None — credit-based pricing was discontinued in January 2025.
- **Enterprise:** Subscription-only, custom-quoted by Kpler sales. Pricing depends on services selected (PS01, PS02, VI01, VI03, EV01, etc.) and request volume.
- **Notes:** Acquired by Kpler in March 2023; product roadmap and pricing have shifted toward enterprise contracts only.

## Authentication

API key issued by Kpler/MarineTraffic after subscription. Key is passed as the `?api_key=...` query parameter on every request. Some services use service codes (e.g., `/api/exportvessel/v:8/`) embedded in the path.

## Endpoints

- **Base URL:** `https://services.marinetraffic.com/api/`
- **Key endpoints (by service code):**
  - `GET /exportvessel/v:8/{api_key}/...` — **PS01:** Single vessel position
  - `GET /exportvessels/...` — **PS02:** Vessel positions in area
  - `GET /voyageforecast/...` — **VI01:** Voyage forecasts (destination/ETA prediction)
  - `GET /portcalls/...` — **EV01:** Port arrivals/departures
  - `GET /vesselmasterdata/...` — **VD01:** Vessel particulars (IMO, dimensions, owner)

## Example call

```bash
curl "https://services.marinetraffic.com/api/exportvessel/v:8/$API_KEY/timespan:10/protocol:jsono"
```

## Rate limits

Per-service throttling defined in the customer's contract (typically expressed as requests per minute and per day per service code). No public rate-limit table — limits scale with the subscribed plan.

## SDKs / Libraries

- **Official:** None published; Kpler/MarineTraffic does not maintain language-specific SDKs.
- **Community:** `amphinicy/marine-traffic-client-api` (Python), `sandrock/MarineTraffic.NET` (.NET) — generally lightly maintained.

## Documentation

- Service docs: https://servicedocs.marinetraffic.com/
- Kpler developer portal: https://developers.kpler.com/
- Product overview: https://www.kpler.com/product/maritime/data-services

## Notes

- Brand: now operates under Kpler, but the product is still marketed as "MarineTraffic." Existing API service codes (PS01, etc.) remain unchanged.
- The free public web at marinetraffic.com is a marketing surface — not a substitute for the API.
- For higher-resolution / lower-latency data, Kpler also sells Spire Maritime (cataloged separately) as a complementary feed.
- For the Strait of Malacca specifically: heavy AIS receiver density and good port-call coverage make this one of the strongest commercial feeds in the region.
