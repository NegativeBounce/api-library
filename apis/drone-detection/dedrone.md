# Dedrone by Axon (DedroneTracker.AI)

The market-leading smart-airspace-security platform (acquired by Axon in 2024; deployed at 900+ sites across 30+ countries with 800M+ drone detections). DedroneTracker.AI fuses RF sensors, radar, and PTZ cameras with AI/ML to detect, classify, track, and identify drones and their pilots, and exposes extended API access for integrating third-party sensors, cameras, and effectors into its single-pane C2.

**Tier:** Enterprise (quote-based; software + sensors)
**Auth:** Customer-provisioned (API access on deployment)
**Last researched:** 2026-06-17

## Use cases

- Detect, classify, and track non-cooperative drones (and locate the pilot) across distributed multi-site deployments via RF/radar/camera sensor fusion.
- Pull detection-event data into a unified operator interface or push it to an external security/C2 platform via API.
- Integrate third-party devices through the API — PTZ cameras, radar, jammers, automated blinds, fog systems, or other countermeasures (mitigation where legally permitted).
- Support FAA/EU Remote ID and BVLOS-aware workflows; feed Axon public-safety / drone-as-first-responder (DFR) programs.

## Pricing

- **Free tier:** None.
- **Paid tiers:** N/A (not self-serve).
- **Enterprise:** Quote-based; DedroneTracker.AI software plus DedroneSensor RF sensors and optional radar/cameras. On-premise/air-gapped or cloud.
- **Notes:** SAFETY Act-designated. Dedrone itself doesn't sell broadband jamming/kinetic defeat — mitigation is provisioned via integration partners.

## Authentication

API access is provisioned with a DedroneTracker deployment; credentials are customer-specific. Configuration is via a browser-based UI; the extended API connects existing sensors and external security products. Not a public self-serve API — engage Dedrone/Axon (or a regional reseller) for integration details.

## Endpoints

- **Base URL:** Deployment-specific (on-prem/air-gapped or cloud).
- **Key endpoints / interfaces:**
  - Detection-event data access (drone + pilot, classification, track) for a unified operator interface or export.
  - Extended API for integrating third-party sensors (cameras, radar) and effectors (jammers, countermeasures).

## Example call

```bash
# Illustrative — base URL and auth are deployment-specific (provided on integration).
curl -H "Authorization: Bearer $DEDRONE_TOKEN" \
  "https://<your-dedronetracker-host>/api/v1/detections"
```

## Rate limits

Not publicly documented (enterprise deployment).

## SDKs / Libraries

- **Official:** Extended API (documentation provided to customers/integrators). No public SDK.
- **Community:** Integrates with Axon's public-safety platform and many third-party C-UAS components.

## Documentation

- Main docs: https://www.dedrone.com/products/drone-detection-software
- API reference: Not public — request via Dedrone/Axon.

## Notes

- **Detection scope:** non-cooperative drones via RF/radar/camera fusion; software-centric (defeat via partners). Complement to cooperative tracking feeds in `drone-tracking`.
- Requires deploying Dedrone sensors — surfaces *your* installation's detections, not a global passive feed.
- Best fit for distributed multi-site airspace monitoring with unified analytics; strong US municipal reach post-Axon.
