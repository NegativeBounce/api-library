# Spirent GNSS

GNSS receiver testing, simulation, and interference detection hardware/software portfolio. Includes the GSS200D Interference Detector for airport RF monitoring and the GSS7765/GSS9000 simulators for generating jamming/spoofing test signals.

**Tier:** Enterprise
**Auth:** N/A (hardware/software products, not a data API)
**Last researched:** 2026-05-07

## Use cases

- Receiver developers and integrators testing GNSS equipment against jamming and spoofing scenarios in lab/anechoic chambers (GSS9000, GSS7000, GSS7765, SimGEN).
- Airport authorities and ANSPs deploying the GSS200D Interference Detector to continuously monitor the RF environment near runways for GNSS-band interference.
- Defense and aerospace integrators validating CRPA (Controlled Reception Pattern Antenna) systems and adaptive antennas against high-power jamming.
- Civil aviation operators using Spirent's GNSS Spoofing Detection & Alerting Service to receive notifications of likely spoofing events affecting their fleet.

## Pricing

- **Free tier:** None.
- **Paid tiers:** None publicly listed. Spirent products are sold on enterprise quotations.
- **Enterprise:** Contact Spirent sales for hardware quotes (GSS200D, GSS7000, GSS9000, GSS7765 etc.) and service agreements.
- **Notes:** This is a capital-equipment vendor; expect six-figure-and-up quotes for full simulator setups, and bespoke contracts for the spoofing detection & alerting service.

## Authentication

Not applicable — Spirent's products are hardware simulators, RF interference detectors, and managed services. The Spoofing Detection & Alerting Service is a managed offering rather than a self-service developer API.

## Endpoints

- **Base URL:** N/A — Spirent does not publish a public REST API for GPS jamming map / coverage zone data.
- **Key products (not endpoints):**
  - **GSS200D Interference Detector** — fixed-site RF monitoring at airports; quantitative interference assessment.
  - **GSS7000 / GSS9000** — multi-frequency, multi-GNSS simulators with jamming and spoofing generation capabilities (for receiver testing, not field detection).
  - **GSS7765** — dedicated GNSS interference generator for use with GSS7000/9000.
  - **SimGEN / SimIQ** — simulator control software; LabVIEW integration available.
  - **GNSS Spoofing Detection & Alerting Service** — managed service for civil aviation; alerts via Spirent-hosted infrastructure rather than a public REST API.

## Example call

```bash
# No public API. Spirent products are integrated via SimGEN, LabVIEW, and proprietary control interfaces.
# For the Spoofing Detection & Alerting Service, contact: https://www.spirent.com/contact
```

## Rate limits

Not applicable.

## SDKs / Libraries

- **Official:** SimGEN (GUI + scripting interface), SimIQ Capture/Replay, LabVIEW integration libraries.
- **Community:** None — Spirent's ecosystem is closed and integrator-focused.

## Documentation

- Main site: https://www.spirent.com/products/pnt-simulation-systems
- GSS200D Interference Detector announcement: https://www.spirent.com/newsroom/press-releases/2017/May/05-23_GNSS-interference-threats-for-civil-aviation
- GNSS Spoofing Detection & Alerting Service brief: https://www.spirent.com/assets/u/brief-gnss-spoofing-detection-and-alerting-service
- GSS9000 simulator: https://www.spirent.com/products/gnss-simulator-gss9000

## Notes

- **Not a data API for GPS jamming coverage maps.** Spirent is a testing-hardware and managed-service vendor. They do **not** publish a global GPS jamming/spoofing map dataset for developer consumption. If you need jamming coverage zones as a developer-consumable feed, Spirent is the wrong tool — see GPSwise, Aireon, or the underlying ADS-B sources (ADS-B Exchange, OpenSky Network).
- Useful in this catalog as a reference for GNSS resilience programs that need:
  1. Hardware to test their own receivers against simulated jamming/spoofing.
  2. Fixed-site monitoring at airports (GSS200D).
  3. A managed alerting service for fleet GPS spoofing detection (no self-service API access).
- The Spirent vs. **Spire Global** distinction matters: Spire Global (spire.com) is a separate company offering satellite-based RF/GNSS interference detection as data products, which is closer to what a developer might want from a "GPS jamming API." Consider Spire as a separate candidate if commercial GNSS interference geolocation data is needed.
- Listed here per explicit user request, with caveat above.
