# Squarehead Technology (Discovair G2+)

A Norwegian acoustic-array vendor. The Discovair G2+ is a passive 128-microphone directional array (with an integrated optical camera) that detects and tracks Class I/II drones by sound using machine-learning beamforming — passive, silent, jamming-immune, and effective without line-of-sight. It processes on-edge and integrates into C2 via the Discovair API, ATAK/TAK, and M2M, and is embedded inside larger systems such as DroneShield's DroneSentry-C2.

**Tier:** Enterprise (quote-based; hardware + software)
**Auth:** Customer-provisioned (API credentials on deployment)
**Last researched:** 2026-06-17

## Use cases

- Passive near-field drone detection where RF/radar are unavailable, jammed, or undesirable (silent, emits nothing, no line-of-sight needed).
- Provide directional/360° acoustic early warning to dismounted units via a device running ATAK or Glipe (man-portable "Sentry Post" use case).
- Feed acoustic detections/tracks into a third-party C2 via the Discovair API or M2M; form an inner detection threshold within a multi-sensor matrix.
- Distinguish commercial/standard drones from self-built or modified drones (a tell-tale of nefarious operators) by acoustic signature.

## Pricing

- **Free tier:** None.
- **Paid tiers:** N/A (not self-serve).
- **Enterprise:** Quote-based. Discovair G2+ (128-mic array, IP65, 105° directional or 360° hemispheric mode). Contact sales.
- **Notes:** Used by large defense integrators within their solutions; integrated into DroneShield DroneSentry-C2. Also extensible to RAM/sniper/vehicle acoustic detection.

## Authentication

API/M2M credentials are provisioned with a Discovair deployment. Not a public self-serve API — engage Squarehead for the API specification and credentials.

## Endpoints

- **Base URL:** Deployment-specific.
- **Key endpoints / interfaces:**
  - Discovair API / M2M — share acoustic detections/tracks with external C2 and integrated systems.
  - ATAK/TAK integration — push directional drone alerts to handheld situational-awareness apps.

## Example call

```bash
# Illustrative — base URL and auth are deployment-specific (provided on integration).
curl -H "Authorization: Bearer $DISCOVAIR_TOKEN" \
  "https://<your-discovair-host>/api/v1/detections"
```

## Rate limits

Not publicly documented (enterprise deployment).

## SDKs / Libraries

- **Official:** Discovair API + M2M + ATAK/TAK (documentation provided to integrators). No public SDK.
- **Community:** Integrated into DroneShield DroneSentry-C2; deployed within large defense integrators' stacks.

## Documentation

- Main docs: https://www.sqhead.com/drone-detection
- API reference: Not public — request via Squarehead Technology.

## Notes

- **Detection scope:** non-cooperative drones via passive acoustics — near-field, jamming-immune, no emissions; ideal as an inner-layer/early-warning complement to radar and RF detectors. Range is shorter than radar, so it's typically one layer in a multi-sensor matrix. Complement to cooperative tracking feeds in `drone-tracking`.
- Requires deploying the array — surfaces *your* installation's detections; "no drone can be hacked to silence."
