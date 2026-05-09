# HawkEye 360

Commercial RF (radio-frequency) signal collection and geolocation provider operating a satellite constellation that detects emissions from vessels — including ships that have switched off AIS. Maritime analytics products (RFGeo, Mission Space, Custody ID) fuse RF detections with AIS to identify "dark ships."

**Tier:** Enterprise
**Auth:** OAuth 2.0 / API Key (issued via Mission Space)
**Last researched:** 2026-05-09

## Use cases

- Detect vessels with AIS switched off in the Strait of Malacca and approaches — RF emissions from radar, satcom, and other onboard systems give them away.
- Custody ID — maintain identity tracking on a target vessel even when it goes AIS-dark.
- Maritime Association analytics — co-occurrence pattern analysis (rendezvous, ship-to-ship transfers, loiter near coastline) tied to suspicious activity.
- GNSS interference detection from space — overlap with the GNSS Interference category (Aireon, GPSJAM, etc.) but uniquely sourced from RF survey constellation.
- Defense-grade pattern-of-life analysis on warships, fishing fleets, and unidentified emitters.

## Pricing

- **Free tier:** None.
- **Paid tiers:** None publicly listed.
- **Enterprise:** RFGeo subscription is the base; Maritime Association and Custody ID are add-ons. Mission Space is the analytics platform layered on top. Pricing is bespoke and tailored to AOI count, revisit cadence, and analytic depth.
- **Notes:** Procurement is sales-led with security-clearance and end-use review. Filed for IPO in April 2026; pricing posture may shift.

## Authentication

OAuth 2.0 / API Key issued via the Mission Space platform after Enterprise contract execution. Access is gated by export-control review.

## Endpoints

- **Mission Space portal:** `https://www.he360.com/missionspace/` (customer-issued login).
- **Public website:** `https://www.he360.com/maritime/`
- **Public API base URL:** Not published. Customers receive a dedicated tenant URL.
- **Surface areas:**
  - RFGeo — geolocated RF detections
  - Maritime Association analytics — vessel co-occurrence and behaviour
  - Custody ID — vessel identity persistence through AIS gaps
  - GNSS Interference Detection (overlap with the GNSS Interference category)

## Example call

```bash
# Illustrative — actual endpoints provisioned per Mission Space tenant.
curl -H "Authorization: Bearer $H360_TOKEN" \
  "https://api.he360.com/v1/rfgeo/detections?bbox=-2.0,99.0,6.0,105.5&start=2026-05-01"
```

## Rate limits

Not publicly documented; defined per contract.

## SDKs / Libraries

- **Official:** Mission Space supports REST integration; specific SDKs are customer-issued.
- **Community:** None.

## Documentation

- Maritime product page: https://www.he360.com/maritime/
- Mission Space platform: https://www.he360.com/missionspace/
- Company overview: https://www.he360.com/

## Notes

- Strongest fit when the user has high-confidence-required dark-vessel detection needs and is willing to pay enterprise-grade pricing.
- Often paired with **Windward** (analytics) or **Spire Maritime** (AIS) to form a fusion picture.
- HawkEye 360 acquired Innovative Signal Analysis (ISA) in 2024 to expand defense capabilities — relevant if Strait monitoring extends to military / patrol vessel tracking.
