# JWLA.ai

Interactive web platform operationalizing the JWC Listed Areas: real-time vessel tracking against war-risk zones, entry/exit alerts, route-risk scoring, and additional-premium/crew-bonus estimation.

**Tier:** Freemium
**Auth:** Account (local-storage based fleet data)
**Last researched:** 2026-06-11

## Use cases

- Tracking vessels against the current JWC Listed Areas (JWLA-033) with zone entry/exit and approach alerts.
- Calculating composite route risk for a multi-waypoint voyage based on JWC zone intersections.
- Estimating additional premium (AP), crew bonus (incl. IBF Des 11 Level 2 ports for Israel/Lebanon calls), and total per-zone transit cost.
- Generating on-demand fleet exposure reports for war-risk brokers and operators.

## Pricing

- **Free tier:** Map, vessel scanning and basic zone display appear usable without payment; fleet/route features require creating a fleet.
- **Paid tiers:** Not publicly published; advanced fleet/reporting likely gated.
- **Enterprise:** Contact provider.
- **Notes:** Stores fleet data and preferences in browser local storage; logs usage for service improvement.

## Authentication

Account/fleet creation within the app; fleet data persisted via local storage. No documented public API.

## Endpoints

- **Base URL:** `https://jwla.ai/` (web application; no documented public REST API)
- **Key features (UI, not API):**
  - Vessel scanning by map area; zone entry/exit and approach alerts.
  - Sea Routing: multi-waypoint route risk scoring vs. JWC zones.
  - Assessment generation: AP, crew bonus, transit cost; AI-enriched assessment reports.
  - War-risk clause Q&A (CL281, Blocking & Trapping, Strike & Delay, IWL warranties, IBF/ITF obligations).

## Example call

```bash
# No documented public API. Access is via the web app at https://jwla.ai/
# Fleet creation and report generation are performed in-app.
```

## Rate limits

Not published (web application).

## SDKs / Libraries

- **Official:** None documented.
- **Community:** None.

## Documentation

- Main docs: https://jwla.ai/
- API reference: None published.

## Notes

- Tightly aligned to the JWC source (tracks the current JWLA circular — JWLA-033, 3 March 2026) and adds the operational/pricing layer the raw circular lacks.
- Useful as a reference implementation for what a war-risk reporting product looks like end-to-end (zone geofencing + AP/crew-bonus economics + clause guidance).
- Confirm commercial terms and whether any data/API access is available before depending on it programmatically — current evidence is a web UI only.
- Cross-reference: `jwc-listed-areas.md` is the upstream source; pair with AIS providers in `maritime-ais` for the vessel-position layer.
