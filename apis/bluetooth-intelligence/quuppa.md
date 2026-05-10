# Quuppa Intelligent Locating System

Direction-finding (Angle-of-Arrival) BLE RTLS platform delivering centimeter / sub-meter real-time location indoors. Centered on the Quuppa Positioning Engine (QPE) with a unified JSON/REST API.

**Tier:** Enterprise (deployed via Quuppa partner ecosystem)
**Auth:** Customer-provisioned API key / token (deployment-specific)
**Last researched:** 2026-05-09

## Use cases

- High-accuracy real-time tracking of BLE tags + smartphones (centimeter-level under good conditions, sub-meter routinely)
- Industrial / manufacturing asset and worker tracking
- Healthcare RTLS — staff badges, patient flow, equipment location
- Sports analytics — player and ball tracking on broadcast pitches
- Security / access control via location-based zone rules

## Pricing

- **Free tier:** None — sold strictly via Quuppa partner ecosystem.
- **Paid tiers:** Project-based pricing including QPE software, Locator hardware, tags, integration, and support. Quoted per site by partner.
- **Enterprise:** Standard model. ~200 commercial partners worldwide; Quuppa rarely sells direct.
- **Notes:** Hardware + software bundle. QPE handles the RTLS math; tags can be off-the-shelf BLE devices that meet the Quuppa Direction-Finding format.

## Authentication

Quuppa Positioning Engine (QPE) is deployed on-premises or in customer cloud; partners provision API keys on the QPE instance. Tokens are passed in API headers per QPE config.

## Endpoints

- **Base URL:** Customer's QPE deployment URL (`https://qpe.example.com:8080` etc.)
- **Key endpoints:**
  - `GET /qpe-rest/v0/tags` — list and locate active tags
  - `GET /qpe-rest/v0/tags/{tagId}` — current position of a single tag
  - WebSocket / streaming endpoints for real-time location push
  - Zones API — define geographic/indoor zones, enter/exit triggers
  - Rules Engine API — configure conditional triggers (commands sent to tags on zone entry, etc.)

## Example call

```bash
# Customer-specific QPE base URL
curl -X GET "https://qpe.example.com:8080/qpe-rest/v0/tags" \
  -H "Authorization: Bearer $QPE_TOKEN"
```

## Rate limits

Self-hosted/edge model — limits depend on QPE hardware sizing rather than vendor-imposed caps. Typical deployments handle hundreds–thousands of tags concurrently.

## SDKs / Libraries

- **Official:** QPE includes a software suite (planning, simulation, configuration) for partners. SDKs for tag firmware integration with Bluetooth chip vendors (Renesas DA14531 reference design, Nordic, etc.).
- **Community:** Bluetooth SIG Direction Finding format means generic BLE chips can broadcast Quuppa-compatible packets.

## Documentation

- Main product page: https://www.quuppa.com/offering/quuppa-intelligent-locating-system/
- Technology overview: https://www.quuppa.com/technology/overview/
- Products: https://www.quuppa.com/technology/products/
- Webinar with Renesas DA14531 reference: https://info.renesas.com/en-extend-battery-life-ble-quuppa-rt-position-da14531-webinar
- Customer login portal (deeper docs): partners-only

## Notes

- Quuppa was founded in 2012 in Espoo, Finland; technology pre-dates the Bluetooth 5.1 Direction Finding spec and influenced it.
- Positioning method = AoA (Angle of Arrival) using multi-antenna Locators — different from RSSI-based BLE positioning.
- Dot-on-the-map accuracy: centimeters at peak, sub-meter routine, scales to fast-moving objects.
- Tag battery life is best-in-class for sub-meter BLE because tags only transmit (no AoA receive complexity on the tag side).
- Cross-listing: not really overlapping — Quuppa is purely BLE/RTLS, no Wi-Fi or cellular.
