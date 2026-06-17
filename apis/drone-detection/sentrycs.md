# Sentrycs

A counter-UAS vendor built around "Cyber over RF" (CoRF) / Protocol Manipulation: it passively decodes drone communication protocols to detect, track, and identify drones (and the operator's last-known location) with low false alarms, and can take control of a rogue drone to land it safely. Open architecture exposes a two-way REST API plus TAK and SAPIENT interoperability for integrating into C2 and other systems.

**Tier:** Enterprise (quote-based; hardware + software)
**Auth:** Customer-provisioned (API credentials on deployment)
**Last researched:** 2026-06-17

## Use cases

- Detect/track/identify non-cooperative drones by decoding their RF protocol (no active radar emissions — passive, emissions-discreet).
- Extract rich identification data (drone + operator last-known location, flight parameters, serial/tail number) and allow-list friendly drones.
- Two-way integration of detections + mitigation into a military/security C2 via REST API, TAK, or SAPIENT.
- Pair detection with protocol-based mitigation (take over controls and land a rogue drone in a predefined spot) where lawful.

## Pricing

- **Free tier:** None.
- **Paid tiers:** N/A (not self-serve).
- **Enterprise:** Quote-based; stationary, portable, and vehicle-mounted systems. Contact sales.
- **Notes:** SAPIENT-compliant (NATO C-UAS standard) and TAK-compatible. Integrated into third-party platforms (e.g., Rafael Drone Dome).

## Authentication

API credentials are provisioned with a Sentrycs deployment; integration is modular and two-way. Not a public self-serve API — engage Sentrycs for the API specification and credentials.

## Endpoints

- **Base URL:** Deployment-specific.
- **Key endpoints / interfaces:**
  - REST API — two-way data exchange (detections, identification, mitigation commands) with external C2/systems.
  - TAK integration — geospatial/situational-awareness feed.
  - SAPIENT interface — open C-UAS sensor/effector integration (NATO standard).

## Example call

```bash
# Illustrative — base URL and auth are deployment-specific (provided on integration).
curl -H "Authorization: Bearer $SENTRYCS_TOKEN" \
  "https://<your-sentrycs-host>/api/v1/tracks"
```

## Rate limits

Not publicly documented (enterprise deployment).

## SDKs / Libraries

- **Official:** REST API + TAK + SAPIENT interfaces (documentation provided to integrators). No public SDK.
- **Community:** Integrations with Xtend, High Lander, Airwayz, Rafael Drone Dome.

## Documentation

- Main docs: https://sentrycs.com/partnerships/
- API reference: Not public — request via Sentrycs.

## Notes

- **Detection scope:** non-cooperative drones via protocol analytics (CoRF) — distinct from radar/optical/acoustic approaches; passive and low-false-alarm, with friend/foe differentiation. Complement to cooperative tracking feeds in `drone-tracking`.
- Coverage depends on the drone's protocol being known/decodable; the system continuously learns RF environments to handle previously unknown links.
- Requires deploying Sentrycs hardware — surfaces *your* installation's detections.
