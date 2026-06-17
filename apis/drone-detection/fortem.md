# Fortem Technologies (SkyDome System)

A US counter-UAS vendor built from the ground up for C-UAS, combining AESA radar (TrueView), AI at the edge, and an autonomous net-capture interceptor (DroneHunter). SkyDome Manager is the C2 software: an end-to-end sensor-correlation platform that fuses radar, long-range cameras, RF sensors, and mitigation, and exposes a rich bi-directional API to add Fortem sensors/effectors to third-party C2 systems such as Northrop Grumman's FAAD C2.

**Tier:** Enterprise (quote-based; hardware + software)
**Auth:** Customer-provisioned (API credentials on deployment)
**Last researched:** 2026-06-17

## Use cases

- Detect, track, and classify non-cooperative drones with 3D AESA radar (TrueView) and AI-driven threat assessment (ThreatAware).
- Bi-directional integration of Fortem detection/mitigation into a third-party or military C2 (e.g., FAAD C2, FS-LIDS) via the SkyDome Manager API.
- Cue long-range PTZ cameras from radar tracks for visual validation and optical classification; correlate video evidence with track history.
- Coordinate autonomous DroneHunter interceptors (net-capture mitigation) against single or multiple threats from C2.

## Pricing

- **Free tier:** None.
- **Paid tiers:** N/A (not self-serve).
- **Enterprise:** Quote-based. TrueView radars (e.g., R20/R30-class), SkyDome Manager C2, DroneHunter F700 interceptor, DroneHangar. Fixed or mobile. Contact sales.
- **Notes:** Proven within US Army FS-LIDS; integrates with FAAD C2. Mitigation (kinetic net capture) is jurisdiction-restricted.

## Authentication

API credentials are provisioned with a SkyDome deployment; the API is bi-directional with third-party C2. Not a public self-serve API — engage Fortem for the API specification and credentials.

## Endpoints

- **Base URL:** Deployment-specific.
- **Key endpoints / interfaces:**
  - SkyDome Manager API — bi-directional integration of Fortem sensors/effectors with external C2 (detections, tracks, classification, mitigation tasking).
  - Sensor-correlation feeds — radar (TrueView), cameras, RF sensors fused into one air picture.

## Example call

```bash
# Illustrative — base URL and auth are deployment-specific (provided on integration).
curl -H "Authorization: Bearer $SKYDOME_TOKEN" \
  "https://<your-skydome-host>/api/v1/tracks"
```

## Rate limits

Not publicly documented (enterprise deployment).

## SDKs / Libraries

- **Official:** SkyDome Manager API (documentation provided to integrators). No public SDK.
- **Community:** Integrations with FAAD C2 (Northrop Grumman), FS-LIDS, and other leading C-UAS equipment.

## Documentation

- Main docs: https://fortemtech.com/products/skydome-manager/
- API reference: Not public — request via Fortem Technologies.

## Notes

- **Detection scope:** non-cooperative drones via AESA radar + AI — wide-area, day/night/adverse-weather, independent of RF emissions; handles quadcopters and fast fixed-wing. Complement to RF/protocol detectors and cooperative tracking feeds in `drone-tracking`.
- Requires deploying Fortem sensors — surfaces *your* installation's detections; uniquely pairs detection C2 with an autonomous capture-drone effector.
