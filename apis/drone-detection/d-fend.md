# D-Fend Solutions (EnforceAir)

The leading RF-cyber-takeover counter-drone provider. EnforceAir passively detects, identifies, and tracks rogue drones by analyzing their RF protocol (non-kinetic, non-jamming, zero false alarms), and can take cyber control to land them safely. Its API and Multi-Sensor C2 (MSC2) share rich drone-information elements with external, multi-layered C2 systems, including via the SAPIENT standard.

**Tier:** Enterprise (quote-based; hardware + software)
**Auth:** Customer-provisioned (API credentials on deployment)
**Last researched:** 2026-06-17

## Use cases

- Detect/identify/track non-cooperative drones via RF-cyber analysis (passive, no jamming, no collateral RF disruption).
- Share real-time drone information with an external/organizational C2 via the EnforceAir API or SAPIENT.
- Network multiple EnforceAir systems into one situational picture (MSC2) to cover large areas, and activate mitigation from a third-party C2.
- Cyber-takeover mitigation: assume control of a rogue drone and guide it to a safe landing (where lawful).

## Pricing

- **Free tier:** None.
- **Paid tiers:** N/A (not self-serve).
- **Enterprise:** Quote-based. EnforceAir2 (RF-cyber), EnforceAir PLUS (adds solid-state radar + optional smart RF-effector jamming). Fixed, vehicle, tactical, and man-portable configs. Contact sales.
- **Notes:** Tag/allow-list large numbers of authorized drones in controlled airspace; "disrupted" GNSS-environment mode; naval/maritime deployment options.

## Authentication

API credentials are provisioned with an EnforceAir deployment; integration is two-way with external C2. APIs are periodically updated to expand shared drone-information elements. Not a public self-serve API — engage D-Fend for the API specification and credentials.

## Endpoints

- **Base URL:** Deployment-specific.
- **Key endpoints / interfaces:**
  - EnforceAir API — share drone detection/identification/track data with connected C2 systems; receive feeds (e.g., authorized-drone tagging).
  - SAPIENT interface — standardized C2 information sharing (UK MoD standard).
  - MSC2 — multi-sensor fusion + mitigation activation through third-party C2 platforms.

## Example call

```bash
# Illustrative — base URL and auth are deployment-specific (provided on integration).
curl -H "Authorization: Bearer $ENFORCEAIR_TOKEN" \
  "https://<your-enforceair-host>/api/v1/detections"
```

## Rate limits

Not publicly documented (enterprise deployment).

## SDKs / Libraries

- **Official:** EnforceAir API + SAPIENT (documentation provided to integrators). No public SDK.
- **Community:** Integrates with multi-layered C2 / SOC platforms and complementary sensors.

## Documentation

- Main docs: https://d-fendsolutions.com/enforceair/
- API reference: Not public — request via D-Fend Solutions.

## Notes

- **Detection scope:** non-cooperative drones via RF-cyber/protocol analysis — same family as Sentrycs (CoRF). Passive, zero false alarms, precise ID; coverage depends on the drone's protocol being supported. PLUS variant adds radar for non-protocol targets.
- Requires deploying EnforceAir hardware — surfaces *your* installation's detections.
- Strong fit where safe, controlled mitigation (land-don't-jam) matters in sensitive/urban environments.
