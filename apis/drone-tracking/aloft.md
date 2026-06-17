# Aloft (Air Control / Geo Portal)

A US-focused drone airspace and fleet-management platform (formerly Kittyhawk; powers the FAA's B4UFLY app) whose developer APIs expose FAA airspace map layers, LAANC authorization, Geo Portal local-rule data, and real-time UTM traffic activity (active flight volumes and authorizations) sourced from flights registered in its network.

**Tier:** Freemium
**Auth:** API key / token (developer program; access requested)
**Last researched:** 2026-06-17

## Use cases

- Pull FAA airspace map tiles and advisories (the same data behind B4UFLY) into your own app.
- Submit and manage LAANC airspace authorizations programmatically for at-scale operations.
- Consume real-time "Active Flight Volumes" and "Active Flight Authorizations" layers to see where drones in Aloft's USS network are operating/authorized.
- Track and report Remote ID compliance across an enterprise fleet.

## Pricing

- **Free tier:** Aloft Air Control is free for individual pilots (LAANC, airspace checks, mission planning). Free B4UFLY access.
- **Paid tiers:** Enterprise Air Control adds user management, reporting, integrations/APIs, SOC2/ISO27001 — pricing not public.
- **Enterprise:** Contact sales; developer/API and tile-server access is request-gated.
- **Notes:** No federal funding — commercial USS. API + map-tile access requires requesting access through the developer program.

## Authentication

Request API access through the Aloft developer program (`https://www.aloft.ai/developer/`). Integrations use issued API credentials/tokens; review the API documentation provided on approval. As an FAA-approved USS, onboarding/QA applies to LAANC integrations.

## Endpoints

- **Base URL:** Not publicly published (provided on developer onboarding).
- **Key endpoints (capabilities):**
  - FAA airspace map-tile / map-layer endpoints.
  - LAANC authorization request/management.
  - Geo Portal data (federal/state/county/city drone rules, takeoff/landing restrictions).
  - Real-time UTM activity layer (active flight volumes + authorizations, updates as flights register).

## Example call

```bash
# Illustrative — exact base URL and paths provided on developer onboarding
curl -H "Authorization: Bearer $ALOFT_TOKEN" \
  "https://api.aloft.ai/v1/airspace/advisories?lat=38.95&lng=-77.45"
```

## Rate limits

Not publicly documented.

## SDKs / Libraries

- **Official:** Documented REST API + map tile services (access on request). No public language SDK.
- **Community:** None notable.

## Documentation

- Main docs: https://www.aloft.ai/developer/
- API reference: https://www.aloft.ai/support/dev-portal-faq/ (request full docs via developer program)

## Notes

- **Coverage is US-centric** (FAA LAANC/B4UFLY). Real-time traffic reflects flights registered/authorized *through Aloft's USS*, not a universal passive feed of all airborne drones — so it is not an ADS-B-style catch-all.
- Best-in-class for US LAANC + authoritative local-rule (Geo Portal) data.
- Overlaps with airspace-data sources; cataloged here for the real-time UTM activity / Remote ID compliance angle.
