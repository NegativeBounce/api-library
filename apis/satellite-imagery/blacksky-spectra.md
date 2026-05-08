# BlackSky Spectra

BlackSky's AI-powered geospatial intelligence platform that pairs a high-revisit small-satellite constellation (Gen-2 ~1m, Gen-3 ~35cm) with on-demand tasking, archive, and analytics — built around dawn-to-dusk monitoring with up to ~15 captures per day over priority sites.

**Tier:** Enterprise (subscription, sales-quoted)
**Auth:** OAuth 2.0 / API key (depending on integration path)
**Last researched:** 2026-05-07

## Use cases

- Hourly monitoring of high-value sites (ports, airfields, infrastructure, conflict zones) leveraging BlackSky's mid-inclination orbits for sub-daily revisit.
- Real-time geospatial intelligence (GEOINT) workflows with Spectra's AI-driven object detection, classification, and tracking (vehicles, vessels, aircraft).
- Maritime domain awareness — vessel detection and tracking with very rapid latency.
- "Assured" tasking — guaranteed satellite capacity over reserved AOIs for mission-critical defense use cases.

## Pricing

- **Free tier:** None.
- **Paid tiers:** Sales-quoted subscriptions; representative public contract values:
  - Recent commercial deals reported in the $20M–$50M range over multi-year terms for defense customers.
  - "On-Demand" tasking and "Assured" priority subscriptions priced based on AOI count, revisit cadence, and analytics modules.
- **Enterprise:** Standard delivery channel — defense, intelligence, civil government, and large commercial accounts via direct sales. Some self-service tasking is available through partners (Esri ArcGIS Marketplace, UP42).
- **Notes:** Per-image / per-km² public pricing is not advertised; treat this as quote-only.

## Authentication

OAuth 2.0 / API key via the Spectra platform; specific flow depends on whether the customer uses the BlackSky console directly, the Spectra API, or an integration partner (UP42 credentials, ArcGIS Online add-in token, etc.).

## Endpoints

- **Base URL:** `https://api.spectra.earth` (Spectra platform API; gated to subscribers)
- **Key endpoints (general shape — refer to the customer-specific developer portal for current paths):**
  - `POST /v1/tasking/orders` — submit a tasking order with AOI, time window, and priority tier.
  - `GET /v1/tasking/orders/{id}` — order status and delivered captures.
  - `POST /v1/catalog/search` — search archive imagery.
  - `GET /v1/analytics/{type}` — Spectra AI products (vehicle detection, vessel detection, change, etc.).
- Also exposed via the open-source [STAPI (Satellite Tasking API) spec](https://github.com/stapi-spec) — see `stapi-fastapi-blacksky` for an example integration.

## Example call

```bash
# Conceptual — real auth and endpoint paths require an active Spectra account
curl -X POST "https://api.spectra.earth/v1/tasking/orders" \
  -H "Authorization: Bearer $BLACKSKY_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Port monitoring 2026-05",
    "geometry": {"type": "Point", "coordinates": [-118.2437, 33.7395]},
    "window": {"start": "2026-05-08T00:00:00Z", "end": "2026-05-15T00:00:00Z"},
    "priority": "high",
    "product": "BSG3-50CM",
    "delivery": {"format": "geotiff", "destination": "s3://my-bucket/blacksky/"}
  }'
```

For developers without direct Spectra access, BlackSky tasking is also available through:
- **UP42** marketplace (`https://api.up42.com/...`) — pay-per-task using UP42 credits.
- **Esri ArcGIS Online** — BlackSky Tasking app delivers imagery directly into your ArcGIS organization.

## Rate limits

Contract-specific. Tasking is throttled by available capacity over the requested AOI and chosen priority tier (Standard, Priority, Assured).

## SDKs / Libraries

- **Official:** Spectra web platform, ArcGIS Online integration, partnership-based access via UP42.
- **Community:** [`stapi-spec/stapi-fastapi-blacksky`](https://github.com/stapi-spec/stapi-fastapi-blacksky) — reference implementation of the Satellite Tasking API spec proxying to the BlackSky tasking API.

## Documentation

- Product / offerings: https://blacksky.com/offerings/
- Technology overview: https://blacksky.com/technology/
- ArcGIS marketplace listing: https://www.esri.com/en-us/arcgis-marketplace/listing/products/blacksky-tasking
- UP42 marketplace listing: https://up42.com/marketplace

## Notes

- BlackSky's Gen-3 fleet is ramping up in 2025–2026 with ~35 cm resolution; Gen-2 satellites operate at ~1 m. Revisit and resolution will continue to improve as the constellation expands.
- Mid-inclination orbits give better sub-daily revisit at low/mid latitudes than sun-synchronous-only constellations — relevant when "live / most recent" matters at low latitudes.
- "Spectra" refers to both the AI analytics layer and the customer-facing platform. Tasking uses Spectra to schedule and Spectra AI to derive analytics on returned imagery.
- For developers without an enterprise contract, UP42 is the most accessible path to BlackSky tasking.
- Dusk-to-dawn imaging is a notable BlackSky capability — they image earlier and later in the day than typical SSO constellations.
