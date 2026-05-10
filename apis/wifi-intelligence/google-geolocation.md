# Google Maps Geolocation API

Google Maps Platform service that accepts an array of Wi-Fi access points and/or cell towers and returns latitude/longitude with an accuracy radius.

**Tier:** Paid (per-SKU monthly free usage cap)
**Auth:** API Key (or OAuth 2.0 bearer token)
**Last researched:** 2026-05-09

## Use cases

- Fallback location for devices without GPS (IoT, browsers, embedded)
- Resolving Wi-Fi BSSIDs scanned in the field to coordinates
- Cell tower (MCC/MNC/LAC/CID, including 5G NR) → coordinates lookup
- Cross-validating an internal positioning DB against Google's

## Pricing

- **Free tier:** Per-SKU monthly free usage cap (replaced the legacy $200/month credit on March 1, 2025). Geolocation has its own SKU under the Essentials category.
- **Paid tiers:** Pay-as-you-go beyond the free cap, billed under the Geolocation Essentials SKU; automatic volume discounts. Optional subscription plans (Starter $100/mo, Essentials $275/mo, Pro) bundle calls across Maps Platform SKUs.
- **Enterprise:** Negotiated through Google Maps Platform sales; supports SLAs and committed-use discounts.
- **Notes:** Billing must be enabled on the Google Cloud project. India has a separate price list. Daily quota caps configurable in Cloud Console.

## Authentication

Generate an API key in Google Cloud Console and enable the Geolocation API for the project. Pass the key as `?key=YOUR_API_KEY` on the request URL. OAuth 2.0 bearer tokens are also supported for service-account use.

## Endpoints

- **Base URL:** `https://www.googleapis.com/geolocation/v1`
- **Key endpoints:**
  - `POST /geolocate?key=API_KEY` — submit JSON with `wifiAccessPoints[]`, `cellTowers[]` (or `nrCellTowers[]` for 5G), optional `homeMobileCountryCode`, `homeMobileNetworkCode`, `carrier`, `radioType`, `considerIp`. Returns `{location: {lat, lng}, accuracy}`.

## Example call

```bash
curl -X POST "https://www.googleapis.com/geolocation/v1/geolocate?key=$API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "considerIp": false,
    "wifiAccessPoints": [
      {"macAddress":"01:23:45:67:89:AB","signalStrength":-65,"signalToNoiseRatio":40},
      {"macAddress":"01:23:45:67:89:AC","signalStrength":-72}
    ],
    "cellTowers": [
      {"cellId":42,"locationAreaCode":415,"mobileCountryCode":310,"mobileNetworkCode":410,"signalStrength":-60}
    ]
  }'
```

## Rate limits

Default per-project QPS quota; configurable in Cloud Console. No published per-key per-day fixed limit — controlled by quota and billing. Single-Wi-Fi-AP requests are rejected (need ≥2 APs or ≥1 cell tower).

## SDKs / Libraries

- **Official:** Google Maps Platform client libraries — Java, Python, Go, Node.js (`@googlemaps/google-maps-services-js`).
- **Community:** Many third-party Maps wrappers in every major language.

## Documentation

- Main docs: https://developers.google.com/maps/documentation/geolocation/overview
- Request/response reference: https://developers.google.com/maps/documentation/geolocation/requests-geolocation
- Pricing/SKU details: https://developers.google.com/maps/documentation/geolocation/usage-and-billing

## Notes

- Returns only the resolved device position, never the underlying AP/cell coordinates (protects Google's training data).
- 5G NR cells supported via `nrCellTowers[]` block.
- Hybrid Wi-Fi + cellular service — cross-listing applies to `cellular-intelligence`.
- Google's policies forbid using the API to track devices without user consent — review TOS before deploying.
