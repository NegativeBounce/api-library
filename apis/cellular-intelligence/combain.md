# Combain Location API

Hybrid positioning service using AI-enhanced cell-ID, Wi-Fi, Bluetooth, LoRaWAN, and indoor radio fingerprinting. Outdoor service is now primarily cell-ID; indoor uses Wi-Fi and BLE beacons. ~185M+ cell IDs across 195 countries.

**Tier:** Freemium / Paid (prepaid credits + custom commercial)
**Auth:** API Key (query parameter)
**Last researched:** 2026-05-09

## Use cases

- Cell-ID outdoor positioning for IoT/asset trackers (low-power alternative to GNSS)
- Indoor positioning using Wi-Fi + BLE radio fingerprinting (Combain Indoor / AI Indoor)
- LoRaWAN gateway-based location for low-power IoT
- Cross-validation against Google/MLS for forensic / law-enforcement workflows

## Pricing

- **Free tier:** Free trial credits on signup; credits valid 12 months. Backward-compatible with Google Geolocation/MLS request format for easy switching.
- **Paid tiers:** Prepaid credit packs paid per successful API call (Mastercard/Visa). Caching of up to ~7 days per result is permitted under standard license.
- **Enterprise:** Custom contracts including on-premise Combain Location DB deployment, AI Indoor radio modeling, and Combain Site Manager Portal.
- **Notes:** All prices exclude VAT. **Outdoor Wi-Fi positioning was discontinued in 2020** for new prepaid customers — global outdoor Wi-Fi is offered only via partner referral.

## Authentication

Sign up at combain.com to receive an API key. Pass as `?key=YOUR_API_KEY` on every request. Indoor service requires a separate Combain Site Manager onboarding for radio model creation.

## Endpoints

- **Base URL:** `https://apiv2.combain.com`
- **Key endpoints:**
  - `POST /` (with `?key=API_KEY`) — submit `cellTowers[]`, `wifiAccessPoints[]`, `bluetoothBeacons[]`, optional GPS; returns `{location: {lat, lng, accuracy}}` and (indoors) building/floor/room
  - Legacy `GET /` HTTP endpoint (v1 CPS) for minimal-bandwidth devices

## Example call

```bash
curl "https://apiv2.combain.com?key=$API_KEY" \
  -X POST \
  -H "Content-Type: application/json" \
  -d '{
    "radioType": "lte",
    "cellTowers": [{
      "mobileCountryCode": 240,
      "mobileNetworkCode": 1,
      "locationAreaCode": 3012,
      "cellId": 11950,
      "signalStrength": -64
    }]
  }'
```

## Rate limits

Pay-per-success model rather than hard QPS caps; abuse protections apply. 404 "notFound" responses on missing cells are not charged but caller should wait 24h before retrying the same query.

## SDKs / Libraries

- **Official:** Combain has an AWS Marketplace SaaS subscription; SDKs distributed per customer engagement.
- **Community:** Compatible with Google Geolocation / Mozilla Ichnaea client code drop-in.

## Documentation

- Main docs: https://combain.com/api/
- API reference: https://portal.combain.com/api/
- Pricing: https://combain.com/products/combain-pricing/
- Cell-ID positioning detail: https://combain.com/positioning-solutions/combain-cell-id-positioning/

## Notes

- Outdoor Wi-Fi positioning discontinued for new customers in 2020; Combain partners with another vendor for that workload.
- Cross-listing applies to `wifi-intelligence` (indoor only) and `bluetooth-intelligence` (BLE beacons indoor).
- Database growth: ~3M new observations/day claimed.
- Subdomain redirection recommended in production (`apiv2.yourcompany.com → apiv2.combain.com`) to avoid hardcoded IPs in shipped devices.
