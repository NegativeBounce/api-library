# Estimote

BLE beacon platform with proprietary hardware (Proximity, Location, LTE, UWB beacons), iOS/Android SDKs, and a REST Cloud API for device fleet management, telemetry, and event handling.

**Tier:** Paid (hardware purchase + tiered cloud plans)
**Auth:** App Token + App ID (Estimote Cloud REST) / OAuth in SDKs
**Last researched:** 2026-05-09

## Use cases

- Proximity-triggered mobile experiences (retail, museums, sports venues)
- Indoor location / wayfinding via Location Beacons + Indoor Location SDK
- Asset tracking with LTE Beacons (cellular-backhauled BLE/UWB tags) for cloud-side cloud-code event handling
- Beacon fleet management — bulk OTA firmware updates, UUID rotation, telemetry health checks

## Pricing

- **Free tier:** Free Estimote Cloud account for managing devices; no hardware free tier — beacons must be purchased.
- **Paid tiers:** Beacon hardware sold per-unit (Proximity Beacon, Location Beacon, Sticker, LTE Beacon, UWB Beacon — prices vary). Cloud features bundled with hardware; advanced features (LTE data plans, Indoor Location, Cloud Code execution) on subscription.
- **Enterprise:** Custom volume hardware orders + dedicated SLAs, on-prem options for regulated deployments.
- **Notes:** LTE Beacon ships with global cellular subscription bundled into the device price; refresh required for ongoing service.

## Authentication

Sign up at cloud.estimote.com to create an App; you receive an App Token + App ID. Pass these to the iOS/Android SDK constructors. REST API uses Basic Auth with App ID + App Token.

## Endpoints

- **Base URL:** `https://cloud.estimote.com/v1` and `/v2` (for newer endpoints)
- **Key endpoints:**
  - `GET /devices` — list beacons in the account
  - `GET /devices/{identifier}` — device details, telemetry (battery, last-seen, settings)
  - `PUT /devices/{identifier}/pending-settings` — queue settings for next sync
  - `GET /attachments` — Cloud Attachments (key/value content tied to beacons)
  - `GET /lte/devices/{id}/events` — LTE Beacon event history
  - LTE Beacon Cloud Code — Node.js sandbox for handling events server-side

## Example call

```bash
curl -X GET "https://cloud.estimote.com/v2/devices" \
  -u "$ESTIMOTE_APP_ID:$ESTIMOTE_APP_TOKEN"
```

```python
import requests
r = requests.get(
    "https://cloud.estimote.com/v2/devices",
    auth=(APP_ID, APP_TOKEN))
print(r.json())
```

## Rate limits

Not publicly documented as fixed numbers. LTE Beacon Cloud Code functions: must finish within 30 seconds, sandboxed Node.js 10.x, restricted module set.

## SDKs / Libraries

- **Official:** iOS SDK (Proximity SDK, Indoor Location SDK, EstimoteSDK 4.x via CocoaPods), Android SDK (Proximity, Indoor Location), React Native wrapper, Unity 3D example.
- **Community:** Cordova/PhoneGap iBeacon plugins; assorted GitHub samples.

## Documentation

- Main docs: https://developer.estimote.com/
- Cloud API reference: https://cloud.estimote.com/docs/
- LTE Beacon docs: https://developer.estimote.com/lte-beacon/cloud-code-and-apis/
- Forums (deprecated but still useful for old questions): https://forums.estimote.com/

## Notes

- All Estimote beacons are iBeacon and Eddystone compatible — usable with non-Estimote stacks too.
- Estimote scaled down public dev relations after ~2020; some docs and forums are dated, but core APIs remain operational.
- Cross-listing applies to `wifi-intelligence` (some hybrid scenarios) and `cellular-intelligence` (LTE Beacon).
- Eddystone protocol is officially deprecated by Google but still broadcast by Estimote hardware.
