# LeoLabs

Commercial space domain awareness platform built on a global network of phased-array radars (UHF + S-band, including the Costa Rica Space Radar near-equatorial site, Kiwi Space Radar in NZ, plus mobile Scout S-band DRA radars). Largest commercial LEO catalog with operational ephemerides, CDMs, and AI-driven analytics (Delta — replaces LeoGuard).

**Tier:** Enterprise (operator subscriptions, government contracts)
**Auth:** API key (per account, RBAC-controlled)
**Last researched:** 2026-05-09

## Use cases

- Operational LEO conjunction screening with low-latency CDMs (separate from JSpOC)
- High-accuracy ephemerides + state vectors for satellite operators (~17 m RMS uncertainty)
- Real-time alerts: conjunctions, maneuvers, tumbling, orbit changes
- Proximity monitoring with animated 3D visualization for coplanar objects
- Launch and early-orbit (LEOP) tracking
- Sovereign / government SDA — LeoLabs supplies NASA conjunction assessment data via Space Act Agreement
- Pattern-of-life analytics, threat assessment, characterization (Delta AI platform)

## Pricing

- **Free tier:** Public dashboards (LEO Catalog, Today's Conjunctions, Catalog Search, Instrument Sites) viewable without account. Limited system metrics endpoint public.
- **Paid tiers:** Subscription-based — dashboard seat licenses and API access by plan. No published price list; quoted per-deployment.
- **Enterprise:** Standard model. Operators, governments, allied partners subscribe to feeds tailored to their fleets.
- **Notes:** Acquired by IronNet in late 2025 (per public news cycles); Delta AI launched as the next-gen replacement for LeoGuard.

## Authentication

Sign up at the LeoLabs platform. Customer admins issue API keys via the platform with RBAC permissions. Pass keys per the API quickstart at `platform.leolabs.space/documentation/api_quickstart`.

## Endpoints

- **Base URL:** `https://api.leolabs.space`
- **Key endpoints (per public quickstart):**
  - `GET /catalog/objects` — LEO catalog browse / search (~23k+ objects)
  - `GET /catalog/objects/{id}/states` — state vectors for an object
  - `GET /catalog/objects/{id}/measurements` — radar measurements / passes
  - `GET /catalog/objects/{id}/orbits` — orbit determinations
  - `GET /system_metrics` — public system performance metrics
  - Conjunction Data Messages (CDMs) — subscriber feed
  - Operational ephemeris screening — POST your ephemerides, receive CDMs
  - Embeddable maps + 3D visualizations

## Example call

```bash
# Public system metrics (no auth)
curl "https://api.leolabs.space/system_metrics"

# Authenticated example pattern
curl "https://api.leolabs.space/catalog/objects?text=ISS" \
  -H "Authorization: Bearer $LEOLABS_API_KEY"
```

## Rate limits

Per-subscription tiers — published in account admin once provisioned. State-vector latency: radar pass to state vector ≈ 2 minutes (vendor-stated).

## SDKs / Libraries

- **Official:** LeoHelp CLI, API docs + embeddable maps documentation, ephemerides file format docs.
- **Community:** Various Python/JS wrappers in operator pipelines.

## Documentation

- API quickstart: https://platform.leolabs.space/documentation/api_quickstart
- API docs: https://platform.leolabs.space/documentation/
- System metrics: https://api.leolabs.space/system_metrics
- Public catalog UI: https://platform.leolabs.space/
- Space Domain Awareness page: https://leolabs.space/space-domain-awareness/

## Notes

- Coverage: LEO ~300–2000 km altitude, inclinations 30°–150° (expanding); KSR can detect smaller objects (down to 2 cm class) — subscriber product.
- Radars: Tracker (legacy phased arrays in Alaska, Texas, Costa Rica, Azores, Australia, NZ), Seeker (S-band), Scout (containerized, mobile S-band DRA, 2025+).
- Independence: LeoLabs runs a fully automated TCPED (Tasking, Collection, Processing, Exploitation, Dissemination) pipeline — independent of US Space Force data.
- Cross-listing: complementary to `satellite-imagery` (correlate radar tracks with optical imagery providers) and `gnss-interference` (orbital context for GPS-disrupting satellites).
