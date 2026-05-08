# Aireon AireonVECTOR

Enterprise-grade GPS interference detection and visualization suite from Aireon, leveraging space-based ADS-B and Iridium-derived TDOA "truth positions" to identify jamming and spoofing globally — including over oceans and polar regions.

**Tier:** Enterprise
**Auth:** OAuth 2.0 / API key (provisioned to contracted customers)
**Last researched:** 2026-05-07

## Use cases

- Air Navigation Service Providers (ANSPs) monitoring GPS integrity across their flight information regions, including oceanic and remote airspace.
- Airlines monitoring real-time GPS health of their fleets and receiving alerts when aircraft enter interference zones.
- Defense and intelligence agencies analyzing GPS interference patterns globally with continuous coverage that doesn't depend on terrestrial ADS-B receiver density.
- Airports and authorities investigating localized GPS jamming/spoofing incidents using "truth position" data independent of GPS.
- Safety analytics platforms (Aireon's Safety Dashboard) trending PIC (Position Integrity Category) and IPC (Individual Position Check) values over time.

## Pricing

- **Free tier:** None.
- **Paid tiers:** None publicly listed; Aireon products are sold on enterprise contracts.
- **Enterprise:** Contact sales — typical buyers are ANSPs, airlines, defense/intelligence agencies, and major aviation safety organizations. Pricing is custom and tied to coverage area, data cadence, and API integration scope.
- **Notes:** AireonVECTOR is a suite of multiple products (VECTOR Flight, AireonSTREAM powered by VECTOR, VECTOR Monitor, plus a planned real-time alerting framework and map visualization layer with API integration). Modules can be licensed separately.

## Authentication

Provisioned to contracted customers through AireonPORTAL (single sign-on) or via dedicated API credentials issued by Aireon. OAuth 2.0 is used for portal authentication; streaming/REST API access for AireonSTREAM and VECTOR products is gated by customer-specific keys.

## Endpoints

- **Base URL:** Customer-specific; Aireon does not publish a public REST endpoint base URL.
- **Key data products / endpoints (conceptual):**
  - **AireonVECTOR Flight** — independent "truth position" track for any ADS-B-equipped flight, computed from satellite TDOA, independent of onboard GPS.
  - **AireonSTREAM powered by VECTOR** — gate-to-gate ATS-quality surveillance stream that fills GPS-interference gaps with VECTOR-calculated positions.
  - **AireonVECTOR Monitor** — visualization layer (COTS-based) for ANSPs to investigate interference sources and impacts.
  - **Real-time alerting** — push alerts on GPS integrity degradation (announced; rolling out in 2025–2026).
  - **Map visualization API** — global GPS Interference layer accessible via API integration (announced; rolling out in 2025–2026).
  - **Safety Dashboard GPS Interference metric** — heat maps of PIC and IPC values, trending; part of Aireon's Safety Dashboard product for ANSPs.

## Example call

```bash
# No public example available — Aireon API access is provisioned per contract.
# Reach out via https://aireon.com/contact-us/ to discuss integration.
```

## Rate limits

Determined per customer contract; not publicly documented.

## SDKs / Libraries

- **Official:** None published. Integration is via direct REST/streaming API consumption per Aireon's customer documentation.
- **Community:** None — Aireon is enterprise-only and not on public SDK ecosystems.

## Documentation

- Main docs: https://aireon.com/products/aireonvector/
- AireonINSIGHTS overview: https://aireon.com/products/aireoninsights/
- GPS interference page: https://aireon.com/gps-interference/
- AireonVECTOR launch announcement: https://aireon.com/introducing-aireonvector/

## Notes

- Aireon is the only operator of a global space-based ADS-B network (hosted on Iridium NEXT). This gives them coverage that terrestrial sources (ADS-B Exchange, OpenSky Network) cannot match — particularly oceanic, polar, and remote airspace.
- AireonVECTOR's distinctive capability is generating an aircraft "truth position" from satellite TDOA and kinematic modeling that is **GPS-independent**, which is what enables it to detect spoofing rather than just jamming. Most ADS-B-derived maps (GPSJAM, GPSwise free, FR24) infer interference from NIC/NACp values reported by the aircraft itself, which spoofers can suppress.
- Customer base is exclusively ANSPs, airlines, defense, and large aviation safety organizations. Not a fit for individual developers or hobbyist projects.
- Sale process is high-touch — expect multi-month evaluation cycles and sizable annual contracts.
- Some VECTOR features (real-time alerting framework, map visualization API) were still in roll-out phase as of late 2025; verify current availability with Aireon sales.
