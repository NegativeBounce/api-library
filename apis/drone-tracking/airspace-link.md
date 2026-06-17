# Airspace Link (AirHub API)

A US "digital infrastructure for drones" platform (FAA-approved LAANC, B4UFLY, and UTM NTAP provider; used in 700+ ATC towers) whose AirHub API delivers airspace data, LAANC authorization, community advisories, FAA TFRs, risk/hazard analytics, and routing — built on Esri GIS and 50+ authoritative data sources. AirHub Portal also integrates third-party UAS detection sensors (RF, radar, Remote ID, acoustic, ADS-B) for a counter-UAS picture.

**Tier:** Freemium (sandbox available; production via account)
**Auth:** API key (sandbox vs. production by base URL)
**Last researched:** 2026-06-17

## Use cases

- Pull controlled/uncontrolled airspace, GIS, and LAANC grid data into a third-party app.
- Broker commercial + recreational (LAANC) authorizations via deep-linking workflows.
- Retrieve FAA TFRs and local community advisories (updated ~every 30 min) for compliance.
- Quantify ground/population risk and hazard within a geographic boundary; routing for BVLOS planning.
- Surface integrated UAS-detection data (cooperative + non-cooperative) tied to FAA registration via an FAA-approved provider.

## Pricing

- **Free tier:** Sandbox mode (does not affect live data). B4UFLY safety info is free to end users.
- **Paid tiers:** Production API access via account; pricing not publicly listed.
- **Enterprise:** Government/municipal UTM, C-UAS programs, consulting; contact sales.
- **Notes:** Base URL determines live vs. sandbox mode.

## Authentication

Create an account to obtain API keys; the request base URL selects sandbox vs. production. AirHub API is REST with resource-oriented URLs, accepting form-encoded or JSON bodies and returning JSON.

## Endpoints

- **Base URL:** Per developer docs at `https://developers.airspacelink.com/` (separate sandbox vs. production hosts).
- **Key endpoints (capabilities):**
  - Airspace data (controlled/uncontrolled, GIS, LAANC grids).
  - Operations creation for LAANC deep-linking (pilot info, start/duration, altitude, boundary shape).
  - Advisories (FAA TFRs + local community advisories).
  - Risk & hazard analytics within a boundary; routing.

## Example call

```bash
# Illustrative — see developers.airspacelink.com for exact paths and sandbox/prod hosts
curl -H "Authorization: Bearer $AIRHUB_KEY" \
  "https://api.airspacelink.com/v1/airspace?lat=42.33&lng=-83.05"
```

## Rate limits

Not publicly documented.

## SDKs / Libraries

- **Official:** REST API documented at developers.airspacelink.com; no public language SDK noted.
- **Community:** None notable.

## Documentation

- Main docs: https://airspacelink.com/developers
- API reference: https://developers.airspacelink.com/

## Notes

- **Coverage is US-centric.** Like Aloft/Wing, the core is airspace + authorization, not a universal passive drone feed — but AirHub additionally ingests detection-sensor data (RF/radar/RID/acoustic) for a fuller airspace picture where those sensors exist.
- Strong choice if you want US airspace data + LAANC + risk analytics + an upgrade path to detection-sensor fusion.
