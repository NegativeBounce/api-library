# HERE Network Positioning

HERE Technologies' REST positioning service that resolves Wi-Fi APs and/or cell IDs (GSM/WCDMA/TD-SCDMA/CDMA/LTE/LTE-M/NB-IoT/5G) to coordinates from a global crowdsourced DB.

**Tier:** Freemium (free developer tier; pay-as-you-go beyond)
**Auth:** API Key or OAuth 2.0 bearer token
**Last researched:** 2026-05-09

## Use cases

- IoT/asset-tracker positioning when GNSS is unavailable
- Indoor + outdoor positioning with HERE Radio Mapper for HD Wi-Fi accuracy
- AWS IoT Core Device Location backend (HERE is a default partner)
- Hybrid fallback for fleet management and field service

## Pricing

- **Free tier:** Free developer plan via developer.here.com — monthly transaction allowance scales by service; sufficient for prototyping.
- **Paid tiers:** Pay-as-you-grow per transaction with tiered volume discounts. Specific Positioning unit pricing is on the HERE Pricing page after free-tier exhaustion.
- **Enterprise:** Custom contracts with on-prem and multi-cloud (AWS/Azure) deployment options; SLAs.
- **Notes:** HERE has a Gold Partner ecosystem — resellers can bundle deployments with professional services.

## Authentication

Sign up at developer.here.com and create an app to get an API Key (`apiKey=...` query param) or OAuth 2.0 client credentials (Bearer token).

## Endpoints

- **Base URL:** `https://positioning.hereapi.com/v2`
- **Key endpoints:**
  - `POST /locate?apiKey=...` — submit JSON with `wlan[]` (Wi-Fi APs by MAC + RSSI) and/or `cellTowers[]`. Returns `{location: {lat, lng, accuracy}}`.

## Example call

```bash
curl -X POST "https://positioning.hereapi.com/v2/locate?apiKey=$HERE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "wlan": [
      {"mac":"01-23-45-67-89-AB","rss":-65},
      {"mac":"01-23-45-67-89-AC","rss":-72}
    ]
  }'
```

## Rate limits

Per-key limits set by chosen plan (free vs paid). No single hard public number; limits and overage policy live on the HERE Platform pricing page.

## SDKs / Libraries

- **Official:** HERE SDK for Android (full: cellular + Wi-Fi + Bluetooth), HERE SDK for iOS (Bluetooth only due to iOS API restrictions), HERE SDK for Flutter.
- **Community:** AWS IoT Core Device Location integrates HERE Positioning natively.

## Documentation

- Main docs: https://developer.here.com/documentation/positioning/
- Product page: https://www.here.com/platform/positioning
- AWS partnership: https://www.here.com/about/press-releases/here-works-with-aws-to-provide-indooroutdoor-device-positioning-services-to

## Notes

- Vendor-stated DB scale: 200M+ cell IDs, 5.6B+ Wi-Fi APs.
- HD Wi-Fi mode (Radio Mapper or customer SDK) reaches 10–20 m horizontal / 2–5 m vertical accuracy.
- iOS does not expose Wi-Fi/cell scan APIs to apps — iOS positioning is Bluetooth-beacon-only via SDK.
- Hybrid service — cross-listing applies to `cellular-intelligence` and `bluetooth-intelligence`.
