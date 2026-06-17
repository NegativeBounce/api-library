# SafeSky

A low-altitude traffic-awareness platform that aggregates 30+ cooperative traffic sources (ADS-B, ADS-L, Mode S, FLARM, FANET, OGN, PilotAware, and others) plus 16,000+ ground stations and 100,000+ app users — and exposes a public REST API to publish UAV telemetry and retrieve surrounding live traffic. The closest thing to an "ADS-B for the low-altitude/drone world": you query the network feed without owning sensors.

**Tier:** Freemium (30-day free trial; Enterprise from €49/month)
**Auth:** API key + HMAC request signing
**Last researched:** 2026-06-17

## Use cases

- Retrieve live low-altitude traffic (UAVs, helicopters, gliders, paramotors, GA) around a point or map viewport — no hardware required.
- Publish your drone's live telemetry so it's visible to crewed aviation across the SafeSky network (SORA M2 air-risk mitigation).
- Submit advisory operations (polygon/circle + max altitude) when live telemetry isn't available, so the activity still shows on the network.
- Power BVLOS / drone-in-a-box situational awareness (native integrations with DJI FlightHub 2, RigiTech, FlytBase).

## Pricing

- **Free tier:** 30-day free trial (enableable from the dashboard). Sandbox environment for development/testing.
- **Paid tiers:** SafeSky Enterprise from €49/month (includes API key `sk_live_...` / `ssk_live_...`).
- **Enterprise:** Higher tiers for ANSPs, USSPs, and airspace-management orgs; contact sales.
- **Notes:** API key determines environment (sandbox vs. production). Rate limiting/throttling is published in the docs.

## Authentication

Obtain an API key from the SafeSky dashboard (sandbox and production keys are separate). Requests are authenticated with the API key plus HMAC request signing; official HMAC SDKs exist for Node.js, Java, Dart, C, C#, Kotlin, Python, and Go. All traffic routes through one gateway; the key selects the environment.

## Endpoints

- **Base URL (gateway):** `https://uav-api.safesky.app`
- **Key endpoints:**
  - `POST /v1/uav` — publish live UAV telemetry (batch PUSH); response returns traffic in the vicinity of all submitted UAVs.
  - `GET /v1/uav?viewport=lat_min,lng_min,lat_max,lng_max` — retrieve traffic in a bounding box (map rendering).
  - `GET /v1/uav?radius=...` — retrieve traffic within a circle around a point (proximity alerts).
  - `POST /v1/advisory` — submit advisory operations (polygon/circle + max altitude) for sources lacking live telemetry.
  - Stats API — network-wide statistics; Platform Status API — service health.

## Example call

```bash
# Retrieve live traffic in a map viewport (HMAC signature headers omitted for brevity)
curl -H "x-api-key: $SAFESKY_KEY" \
  "https://uav-api.safesky.app/v1/uav?viewport=50.0,4.3,50.2,4.6"
```

## Rate limits

Published in the docs (Rate Limiting & Throttling section); throttled requests return a documented throttled response. Honor the recommended back-off handling.

## SDKs / Libraries

- **Official:** HMAC auth SDKs for Node.js, Java, Dart, C, C#, Kotlin, Python, Go. Postman collection provided.
- **Community:** Interoperates with SkeyDrone, DJI FlightHub 2, RigiTech, FlytBase.

## Documentation

- Main docs: https://docs.safesky.app/books/safesky-api-for-uav
- API reference: https://docs.safesky.app/books/safesky-api-for-uav/chapter/api-definition

## Notes

- **Strongest "no-sensor" answer in this category for low-altitude air picture**, but its drone visibility is *cooperative* — it sees UAVs that publish telemetry (directly or via partners like SkeyDrone) plus crewed cooperative traffic. Non-cooperative/hostile drones that don't broadcast won't appear unless fed in by a detection partner.
- Belgian/EU-origin but network spans many countries; coverage densest in Europe.
- Two-way value: consume traffic *and* contribute your drone's position.
