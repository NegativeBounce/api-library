# Wing OpenSky

Alphabet/Wing's drone airspace-access platform (US + Australia). An FAA-approved LAANC USS and CASA-approved provider, OpenSky offers a free flyer app plus a partner API that lets companies embed OpenSky's airspace rules and near-real-time authorization workflows into their own apps.

**Tier:** Freemium (free app; API via partnership)
**Auth:** API credentials (partner integration)
**Last researched:** 2026-06-17

## Use cases

- Embed tailored airspace rules/flight-brief logic into your own drone app (per-operation, per-drone).
- Request near-real-time LAANC authorizations (US) or Australian automated access authorizations from within a third-party app.
- Manage and log flights/permissions to a pilot profile.
- White-label OpenSky airspace access for an enterprise/government fleet platform (e.g., Measure Ground Control integration).

## Pricing

- **Free tier:** OpenSky flyer app is free (US + Australia), iOS/Android.
- **Paid tiers:** API/partner integration terms not publicly listed.
- **Enterprise:** Partner/contract basis — contact Wing.
- **Notes:** This is an airspace-access + authorization API, not a live third-party drone-traffic feed.

## Authentication

API access is via partnership with Wing; integrators receive credentials to surface OpenSky inside their own applications. Specific auth scheme not publicly documented (partner onboarding).

## Endpoints

- **Base URL:** Not publicly published (partner integration).
- **Key endpoints (capabilities):**
  - Airspace rules / flight-brief retrieval tailored to a specific operation and drone.
  - LAANC (US) / automated access (Australia) authorization request + management.
  - Flight and permission logging to a pilot profile.

## Example call

```bash
# Not publicly documented — OpenSky API is provided to integration partners.
# Public entry points are the OpenSky flyer apps (iOS/Android) and wing.com/opensky.
```

## Rate limits

Not publicly documented.

## SDKs / Libraries

- **Official:** Partner API (no public SDK published).
- **Community:** None notable.

## Documentation

- Main docs: https://wing.com/opensky
- API reference: Not public — request via Wing partnership.

## Notes

- **Coverage:** US + Australia only. Provides *airspace access and authorization*, not a passive feed of where other drones currently are — so it does not answer the "ADS-B for drones" need directly. Cataloged here as a major no-your-own-sensor airspace/authorization source operators integrate with.
- Backed by Alphabet; one of the most established LAANC USS apps alongside Aloft and Airspace Link.
