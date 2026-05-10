# CRFS RFeye

UK (Cambridge)-based enterprise RF spectrum monitoring and geolocation ecosystem. RFeye Nodes / Arrays / SenS Portable hardware paired with RFeye Site SRM software for distributed real-time monitoring, AOA + TDOA + POA geolocation, multi-target signal location, and signal classification.

**Tier:** Enterprise (defense / regulatory / aerospace / security agencies)
**Auth:** Customer-provisioned (deployment-specific)
**Last researched:** 2026-05-09

## Use cases

- Military test range RF monitoring + interference geolocation (24/7 networks of Nodes/Arrays)
- Spectrum regulator interference investigation and enforcement
- Counter-UAS / counter-drone RF detection and direction-finding
- Critical infrastructure protection (airports, embassies, data centers)
- Frequency-hopping, broadband, and low-power signal detection in congested environments
- Long-duration high-fidelity IQ recording (RFeye SenS Portable)

## Pricing

- **Free tier:** None.
- **Paid tiers:** Project-based, sold direct or through defense/security integrators. Hardware (Nodes 100-8 / 100-18 / 100-40 / Arrays / SenS Portable) + software (RFeye Site, Signal Discovery) bundled. Typical deployments are six-figure USD and up.
- **Enterprise:** Standard model. Multi-mission systems for fixed/vehicle/transportable platforms; full integration services.
- **Notes:** Used at major US Army test sites and European MOD ranges (per CRFS public references).

## Authentication

Customer-issued credentials per deployment. RFeye Site connects to networked Nodes/Arrays over secure customer infrastructure. No public API — integration paths are part of contracted scope.

## Endpoints

- **Base URL:** Customer's RFeye Site / Node management infrastructure
- **Key interfaces:**
  - RFeye Site (Windows desktop) — sensor resource management, real-time mission control, 2D/3D mapping with AOA/TDOA/POA overlays
  - RFeye Node ↔ Site network protocol — proprietary, configured per deployment
  - Mission scripting — autonomous embedded missions on Nodes triggered by mask breaks or async events
  - I/Q export — WAV-E format support for downstream analysis (RFeye Site 1.49+)
  - Signal Discovery — automated detection + geolocation that reduces operator cognitive load

## Example call

No public REST/HTTP example — RFeye is a closed enterprise stack. Integration with external systems happens through delivered SDK/connectors or via the Site UI's mission export features. Vendor contact: `enquiries@crfs.com`.

## Rate limits

Bound by deployed hardware capacity (Node count, antenna count, network bandwidth). Site updates AOA/TDOA results at up to 10 Hz on maps.

## SDKs / Libraries

- **Official:** RFeye Site (desktop SRM), Node firmware, Array firmware, integration SDKs delivered to customers.
- **Community:** None — closed ecosystem.

## Documentation

- Product overview: https://www.crfs.com/rfeye-ecosystem
- RFeye Site product page: https://www.everythingrf.com/products/rf-software/crfs/679-901-rfeye-site
- Recent feature update (Pulse-in-Pulse, WAV-E): https://everythingrf.com/news/details/13212-crfs-introduces-pulse-detection-and-wav-e-features-in-the-latest-rfeye-site-software-update
- Multi-target location announcement: https://www.microwavejournal.com/articles/25614-rfeye-site-software-from-crfs-supports-multi-target-location

## Notes

- Customer base skews defense / regulator / aerospace; commercial OEM access requires contracting through CRFS or a partner integrator.
- TDOA accuracy is the most-asked technical question per vendor — depends heavily on Node geometry, time sync (GPS-disciplined), and signal characteristics.
- Acquired by Cohort plc in 2024 (UK defense group).
- Cross-listing applies to `gnss-interference` (related — Hidden Level + GPSwise occupy similar terrain there).
