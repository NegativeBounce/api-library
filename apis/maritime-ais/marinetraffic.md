# MarineTraffic

Global AIS vessel tracking platform (now part of Kpler) offering real-time vessel positions, port calls, voyage forecasts, and historical AIS data via REST APIs from 13,000+ AIS receivers across 190 countries.

**Tier:** Enterprise
**Auth:** API Key (query parameter)
**Last researched:** 2026-06-11

## Use cases

- Real-time tracking of vessels via Vessel Position services (PS01/PS02) across global shipping lanes and chokepoints.
- Port-call alerts (e.g. Singapore, Port Klang, Tanjung Pelepas, Rotterdam, Fujairah) to confirm transit and dwell times.
- Voyage forecasts (predicted ETA/destination) for vessels approaching a region, useful for handover planning.
- Historical AIS replay for incident investigation (e.g. reconstructing a piracy or collision event timeline).
- Density-map services for hot-spot analysis of fishing/military/commercial activity.

## Pricing

- **Free tier:** None for the API. The marinetraffic.com web map is free for casual use only.
- **Paid tiers:** None — credit-based/self-service pricing was discontinued (enterprise-only since the Kpler consolidation).
- **Enterprise:** Subscription-only, custom-quoted by Kpler sales. Pricing depends on services selected (PS01, PS02, VI01, EV01, VD01, etc.) and request volume.
- **Notes:** Acquired by Kpler in March 2023; pricing and roadmap have shifted toward enterprise contracts only. Users must now contact sales.

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

- ⚠️ **Kpler consolidation:** MarineTraffic is one of three maritime data providers Kpler brought under one umbrella — alongside **FleetMon** (coordinated deal) and **Spire Maritime** (satellite AIS constellation). Credit-based pricing was discontinued; access is now enterprise-subscription only via Kpler sales. The product is still marketed as "MarineTraffic" and existing service codes (PS01, etc.) remain unchanged.
- The free public web at marinetraffic.com is a marketing surface — not a substitute for the API.
- For blue-water / lower-latency satellite data, Kpler also sells Spire Maritime (`maritime-ais/spire-maritime.md`) as a complementary feed; vessel ownership/particulars at enterprise grade are in `vessel-registry/marinetraffic-vessel-particulars.md`.
- Strong AIS receiver density and port-call coverage make it one of the strongest commercial terrestrial feeds in busy regions; the parent commodity-flows product is `trade-flows/kpler.md`.
