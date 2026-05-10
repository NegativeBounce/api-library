# Unseenlabs

French commercial space-based RF detection company operating the BRO (Breizh Reconnaissance Orbiter) constellation. Detects, characterizes, and geolocates RF emitters from vessels at sea — primarily X/S-band maritime radar — to identify dark ships and supplement AIS/SAR data. Mono-satellite (single-satellite Direction-of-Arrival) approach distinguishes it from cluster-based competitors.

**Tier:** Enterprise (RF data products)
**Auth:** Customer-provisioned
**Last researched:** 2026-05-10

## Use cases

- Dark vessel detection (AIS-off, AIS-spoofed, AIS-jammed ships) via passive RF emissions
- EEZ surveillance, illegal fishing detection, sanctions monitoring
- Vessel RF fingerprinting for repeat-emitter tracking across passes
- Tip-and-cue with optical/SAR providers — RF detection narrows the search box for high-cost imagery
- Persistent monitoring of strategic regions (Natuna Sea, South China Sea, Persian Gulf, Arctic)
- Maritime insurance and shipowner fleet visibility

## Pricing

- **Free tier:** None. Sample data sheets available on request.
- **Paid tiers:** Project-based / area-of-interest subscriptions. Pricing not public.
- **Enterprise:** Standard route. Customers include governments, marine underwriters, shipowners, NGOs. Strategic partnerships with S&P Global (analytics fusion).
- **Notes:** EU/French origin can be a procurement advantage for non-US allied customers vs. US ITAR-controlled alternatives.

## Authentication

Customer credentials issued after commercial agreement. Data delivered as files in standard geospatial formats — no public REST API at this time.

## Endpoints

- **Base URL:** Customer-specific data delivery (no public API)
- **Key interfaces / outputs:**
  - RF detection product files: lists of detected emitters with geolocation, accuracy, RF technical parameters (carrier frequency in MHz, pulse duration in nanoseconds, pulse repetition frequency in Hz)
  - Modern geospatial formats: GeoJSON, KML, shapefiles
  - Per-pass coverage: ~300,000 km² (550 × 550 km / 300 × 300 nautical miles) per satellite
  - Geolocation accuracy: ~1 km (better than nautical mile)
  - Tip-and-cue handoff to optical/SAR partners
  - Intelligence reports (analyst-prepared) for situational context

## Example call

No public REST example — data is delivered through customer agreements. Vendor contact: unseenlabs.com → contact form. Product sheet downloadable at https://contents.unseenlabs.space/en/product-sheet-download.

## Rate limits

Constellation-driven. As of late 2024: 15 operational BRO satellites with ~3-hour revisit globally. Target: 25 satellites end of 2025, sub-1-hour revisit. Each satellite supports ~50,000 passes/month with KSAT ground network.

## SDKs / Libraries

- **Official:** None public — outputs are standard geospatial files.
- **Community:** ESA Earth Online quality assessment notes (TN on BRO products): https://earth.esa.int/eogateway/documents/20142/37627/Technical-Note-on-Quality-Assessment-for-BRO.pdf

## Documentation

- Main site: https://unseenlabs.com/
- Technology page: https://unseenlabs.com/en/technology/
- Solutions page: https://unseenlabs.com/en/solutions/
- ESA Earth Online mission profile: https://earth.esa.int/eogateway/missions/unseenlabs/description
- eoPortal BRO mission page: https://www.eoportal.org/satellite-missions/unseenlabs

## Notes

- **Mono-satellite Direction-of-Arrival (DOA)** is the technical differentiator: each satellite individually geolocates, no cluster formation flight required. Compare to HawkEye 360 (3-sat clusters), late-stage Kleos (4-sat clusters).
- Primary signal targets: S-band (SOLAS Reg 19 mandates for >3000 GT vessels) and X-band maritime radar. Spectrum monitoring also captures other shipborne emitters.
- Strategic partnership with S&P Global — Unseenlabs RF feeds are correlated with S&P Maritime data products for sanctions and dark-fleet analytics.
- Strong EU footprint, expanding US presence.
- Cross-listing: significant overlap with `dark-vessel-detection`. Distinct from cataloged HawkEye 360 (different geolocation method, different signal mix, different national origin).
