# Inpixon RTLS

Enterprise indoor positioning + RTLS platform supporting BLE, UWB, Chirp, Wi-Fi, RFID, NFC, QR, LiDAR, and GPS. Provides RESTful APIs, MQTT, CoAP, and the omlox open standard for cross-vendor RTLS integration. Berlin-headquartered.

**Tier:** Enterprise (subscription / Location-as-a-Service)
**Auth:** API Key (per user/developer) + OAuth where supported
**Last researched:** 2026-05-09

## Use cases

- Industrial RTLS for manufacturing (Industry 4.0): worker safety, collision avoidance, asset tracking
- Indoor positioning + wayfinding for smart buildings, healthcare, retail
- ERP/WMS/MES integration via REST, MQTT, omlox bridges (SAP, etc.)
- Wireless device detection for situational awareness / security ops
- BLE-based blue-dot indoor location with sensor fusion (accelerometer, gyro, compass)

## Pricing

- **Free tier:** None.
- **Paid tiers:** Subscription-based, scaled by site / number of tags / anchors. Public list pricing not published; quotes via sales.
- **Enterprise:** "Location-as-a-Service" (LaaS) all-inclusive packages bundling hardware, software, deployment, and managed service.
- **Notes:** Inpixon won 2025 IoT Breakthrough "RTLS Solution of the Year." Heavy presence in EMEA manufacturing; askPixi AI integration adds NL analytics on top of location data.

## Authentication

Customer-provisioned API keys per user/developer through the Inpixon admin console; OAuth supported for some endpoints. Authentication details delivered with deployment package after contracting.

## Endpoints

- **Base URL:** Customer-specific (cloud or on-prem). Vendor docs live on docs.inpixon.com behind login.
- **Key endpoints:**
  - REST endpoints for tag, anchor, zone, and event management
  - MQTT topics for streaming real-time location blinks
  - CoAP for low-power device interactions
  - omlox-compliant interfaces for cross-vendor RTLS interop
  - Webhook configuration for event triggers (zone enter/exit, alarms)

## Example call

```bash
# Pseudo-example — exact endpoints are customer-specific
curl -X GET "https://your-tenant.inpixon.com/api/v1/tags" \
  -H "X-API-Key: $INPIXON_API_KEY"
```

```text
# MQTT topic pattern (illustrative)
inpixon/<site_id>/<zone>/<tag_id>/location
```

## Rate limits

Not publicly documented. Defined per deployment SLA.

## SDKs / Libraries

- **Official:** REST/MQTT/CoAP integration documented; SDKs delivered to customers as part of the engagement.
- **Community:** omlox open-standard integrations enable interop with non-Inpixon RTLS stacks.

## Documentation

- Product overview: https://www.inpixon.com/rtls-platform
- Indoor positioning: https://www.inpixon.com/solutions/indoor-positioning
- Integrations: https://www.inpixon.com/rtls-platform/integrations
- BLE technology page: https://www.inpixon.com/technology/standards/bluetooth-low-energy
- omlox: https://omlox.com/

## Notes

- Some third-party listings (GetApp 2025) state "no API" — this is outdated; Inpixon's own product pages and integrations docs confirm REST/MQTT/CoAP availability.
- Acquired several RTLS-adjacent companies (Nanotron, INTRANAV); platform consolidates those technologies.
- Tech-agnostic: same platform can ingest UWB, BLE, Chirp, GPS, RFID — handy when an environment mixes legacy and new tags.
- ChatGPT integration ("askPixi") for natural-language analytics on location data.
- Cross-listing applies to `wifi-intelligence` (Wi-Fi positioning support) and `rf-monitoring` (passive wireless device detection).
