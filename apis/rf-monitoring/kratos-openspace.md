# Kratos OpenSpace Platform

Commercially available, fully software-defined, container-orchestrated satellite ground system from Kratos Defense & Security (NASDAQ: KTOS). Replaces traditional purpose-built RF + modem hardware with virtualized network functions running on x86 / Arm + Kubernetes.

**Tier:** Enterprise (defense / national security / commercial sat operators)
**Auth:** Customer-provisioned, deployment-specific (Kubernetes/SUSE-based)
**Last researched:** 2026-05-09

## Use cases

- Software-defined SATCOM gateways for GEO, MEO, LEO satellites — multi-orbit, multi-mission
- US DoD MILSATCOM modernization (Wideband Global SATCOM, AEHF, ESS, DSCS, Milstar via CCS-C)
- Commercial sat ops — Kratos powers ~80% of commercial sat operations and 90% of US DoD
- Edge SATCOM for tactical units (OpenEdge digitizers + software modems at the edge)
- Earth Observation / Remote Sensing data delivery (e.g., SSC Space Go for LEO smallsats)
- Telemetry, Tracking & Command (TT&C) and Command & Control (C2) of spacecraft

## Pricing

- **Free tier:** None.
- **Paid tiers:** Project-based; covers software licenses, Kratos OpenEdge digitizers, professional services. Multi-million USD typical for full ground-station deployments.
- **Enterprise:** Standard route. Recent contract examples: $25M task order with US Space Force for ESS support (June 2025); deployments at SES, Telesat, SSC Space.
- **Notes:** Built on SUSE (SLE Micro, RKE2, Rancher Multi-Cluster Manager) — cloud-native stack runs on customer cloud, on-premises, or in tactical edge boxes.

## Authentication

Customer-issued credentials provisioned through Kubernetes RBAC + customer's IdP. Network functions communicate over standards-based interfaces (DIFI for digitized RF, etc.). No public API — integration is contracted scope.

## Endpoints

- **Base URL:** Customer's OpenSpace cluster ingress / Kubernetes API (customer-specific)
- **Key interfaces:**
  - Containerized virtual modems, virtual receivers, virtual hubs (vStar) — orchestrated as Kubernetes services
  - DIFI (Digital IF Interoperability) standard — moves digitized RF between OpenEdge digitizers and virtual modems
  - OpenSpace SpectralNet / digitizers — RF-to-digital conversion at the antenna
  - OpenSpace quantum products — virtualized replacements for traditional ground hardware
  - OpenEdge 2500 — edge digitizer that integrates with antenna controllers (e.g., Cobham Tracker 1300TT)
  - Make-before-break handover orchestration for MEO/LEO constellation handoffs

## Example call

No public REST example. Customers integrate via:
- Kubernetes manifests (Rancher Fleet) for service deployment
- DIFI streams between digitizers and virtual modems
- C2 / TT&C command/telemetry via Kratos quantumCMD, quantumDB, etc. (legacy Kratos products that integrate with OpenSpace)

```yaml
# Illustrative Helm/Rancher Fleet pattern (customer-specific)
apiVersion: v1
kind: ConfigMap
metadata:
  name: openspace-vmodem-config
data:
  modem.profile: "DVB-S2X"
  difi.input: "udp://0.0.0.0:50000"
```

## Rate limits

Bound by deployed compute and the satellite link itself. Container orchestration scales horizontally on customer infrastructure.

## SDKs / Libraries

- **Official:** Kratos delivers OpenSpace components, OpenEdge firmware, integration SDKs to customers as part of engagements.
- **Community:** None — closed enterprise stack. DIFI is an open standard that lets third-party RF hardware interoperate.

## Documentation

- Product page: https://www.kratosdefense.com/products/space/satcom/openspace
- Updated product home: https://www.kratosspace.com/virtual-ground/platform
- SUSE case study: https://www.suse.com/success/kratos_success_story/
- US Army demo (Apr 2024): https://www.kratosdefense.com/newsroom/kratos-demonstrates-fully-virtualized-satcom-ground-system-for-u-s-army-futures-command-over-sess-o3b-meo-constellation
- SSC Space Go (Mar 2026): https://www.kratosdefense.com/newsroom/ssc-space-deploys-kratos-openspace-platform-in-its-new-service-for-leo-missions-ssc-space-go
- DIFI standard: https://dificonsortium.org/

## Notes

- "OpenSpace" refers to a family: OpenSpace Platform (orchestration), OpenSpace digitizers (was SpectralNet — RF-to-digital), OpenSpace quantum (virtual hardware replacements like vStar, vSatcom hubs).
- Kratos handles ~90% of US DoD and ~80% of commercial sat ops in some form (vendor-stated).
- Sister/related products: quantumCMD (mission control), Compass (spacecraft simulation), EpochIPS (TT&C) — these often deploy alongside OpenSpace.
- Cross-listing applies to `satellite-tracking` (TT&C overlap) — but OpenSpace is fundamentally a ground-system platform, not a tracking/orbital data API.
