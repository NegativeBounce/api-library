# Robin Radar Systems (IRIS)

A Dutch radar vendor specializing in purpose-built drone-detection radar. IRIS provides 360° azimuth / 60° elevation 3D coverage with micro-Doppler classification and deep-neural-network (DNN) processing to distinguish drones from birds (including hovering and fixed-wing targets), and is built to integrate: a simple XML broadcast interface ships as standard, plus an API made to integrate with C2 and other sensors/effectors.

**Tier:** Enterprise (quote-based; hardware + software)
**Auth:** Customer-provisioned (interface credentials on deployment)
**Last researched:** 2026-06-17

## Use cases

- Early-warning radar detection of non-cooperative drones (does not rely on the drone broadcasting or being actively controlled).
- Feed IRIS tracks and alarms as a layer into your own security / C2 system via the standard XML broadcast interface or API.
- Cue cameras, jammers, lasers, spoofers, or protocol-manipulators with accurate 3D position (incl. height) for confirmation and mitigation.
- On-the-move detection mounted on a vehicle or maritime vessel (up to ~100 km/h).

## Pricing

- **Free tier:** None.
- **Paid tiers:** N/A (not self-serve).
- **Enterprise:** Quote-based. IRIS (current 3D product, ~29 kg, ~5 km instrumented range / ~78 km² coverage). Contact sales.
- **Notes:** ELVIRA (the original 2D drone-detection radar) was officially retired in 2025 after ~a decade; IRIS is the current product. Radar detects targets regardless of RF behavior — complements RF/protocol systems.

## Authentication

Interface/API credentials are provisioned with an IRIS deployment. The standard XML broadcast interface and integration API are documented for integrators. Not a public self-serve API — engage Robin Radar.

## Endpoints

- **Base URL:** Deployment-specific.
- **Key endpoints / interfaces:**
  - XML broadcast interface (standard) — streams tracks/alarms to external security/C2 systems.
  - Integration API — bi-directional integration with C2 and cueing of other sensors/effectors (3D tracks incl. height).

## Example call

```bash
# Illustrative — IRIS ships a standard XML broadcast interface; an integration API is
# provided on deployment. Exact host/format are deployment-specific.
curl -H "Authorization: Bearer $IRIS_TOKEN" \
  "https://<your-iris-host>/api/v1/tracks"
```

## Rate limits

Not publicly documented (enterprise deployment).

## SDKs / Libraries

- **Official:** Standard XML broadcast interface + integration API (docs provided to integrators). No public SDK.
- **Community:** Integrations with C2/VMS partners (e.g., Genetec) and broader C-UAS stacks; partnership with AirMatrix.

## Documentation

- Main docs: https://www.robinradar.com/products/iris-radar
- API reference: Not public — request via Robin Radar.

## Notes

- **Detection scope:** non-cooperative drones via radar + micro-Doppler/DNN — wide-area early warning independent of RF emissions; sees autonomous/pre-programmed drones and swarms. Complement to RF/protocol detectors and cooperative tracking feeds in `drone-tracking`.
- Requires deploying the radar — surfaces *your* installation's detections; designed to sit at the center of a multi-sensor network.
