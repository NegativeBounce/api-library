# Kontakt.io (Kio Cloud)

BLE beacon + AI-powered RTLS platform marketed for healthcare, smart buildings, manufacturing, and retail. Provides Kio Cloud REST API, iOS/Android SDKs, BLE gateways (Portal Light), and a portfolio of beacons and tags.

**Tier:** Paid (hardware + tiered cloud plans)
**Auth:** API Key (Bearer token) for Kio Cloud REST; OAuth/SSO supported for SDKs
**Last researched:** 2026-05-09

## Use cases

- Healthcare RTLS — patient flow, asset tracking (infusion pumps, defibrillators), staff safety, hand-hygiene compliance
- Indoor journey analytics — heatmaps, dwell times, capacity planning
- Smart-building occupancy / wayfinding
- Bulk beacon fleet management (config, OTA firmware, UUID rotation)
- Anti-piggybacking via secure shuffling of iBeacon UUID + MAC at scheduled intervals

## Pricing

- **Free tier:** Free Kio Cloud signup for evaluation; hardware purchase required for live deployment.
- **Paid tiers:** Bundled per-site / per-device subscription packages; pricing through partner network. Beacons / tags / Portal Light gateways sold per-unit.
- **Enterprise:** Healthcare-focused enterprise contracts via Kontakt.io's 1,200+ partner network; deployment-as-a-service options.
- **Notes:** 32,000+ end users, 3M+ devices deployed (vendor-stated). Pricing is opaque on public site — sales-led.

## Authentication

Generate an API Key in the Kio Cloud admin panel. Pass as `Api-Key: $KEY` header (or Bearer token via the iOS/Android SDK's `setAuthHeadersProvider`). SSO / OAuth supported for enterprise tenants.

## Endpoints

- **Base URL:** `https://api.kontakt.io`
- **Key endpoints:**
  - `GET /device` — list devices in the account
  - `GET /device/{uniqueId}` — single device details
  - `PUT /device/{uniqueId}` — update device configuration (UUID, major/minor, Tx power, interval)
  - `GET /venue` — list venues
  - `POST /telemetry` (and gateway endpoints) — receive forwarded scan data
  - `GET /firmware` — list available firmware for OTA

## Example call

```bash
curl -X GET "https://api.kontakt.io/device" \
  -H "Api-Key: $KONTAKT_API_KEY" \
  -H "Accept: application/vnd.com.kontakt+json;version=10"
```

```objective-c
// iOS — using KTKCloudClient (CocoaPods: kontakt-ios-sdk)
[Kontakt setApiKey:@"YOUR_API_KEY"];
KTKCloudClient *client = [[KTKCloudClient alloc] init];
[client getObjects:[KTKDevice class] withParams:nil
  completion:^(NSArray *result, KTKPagination *p, NSError *err){
    NSLog(@"%@", result);
  }];
```

## Rate limits

Vendor doesn't publish hard QPS numbers. Limits scale with subscription tier; large fleets typically warrant talking to support to raise caps.

## SDKs / Libraries

- **Official:** iOS SDK (`kontakt-ios-sdk`, CocoaPods), Android SDK, gateway firmware on Portal Light, Wirepas-compatible mesh integrations.
- **Community:** Various third-party EHR/EMR connectors (Epic, Cerner) via Kontakt.io's healthcare partner program.

## Documentation

- Main docs / Knowledge Base: https://knowledgebase.kontakt.io/
- API reference (versioned): https://developer.kontakt.io/cloud-api/quickstart/
- iOS SDK source: https://github.com/kontaktio/kontakt-ios-sdk
- Cloud Beacon overview: https://kontakt.io/blog/introducing-the-new-cloud-beacon/

## Notes

- "Kio Cloud" is the cloud middleware; Portal Light is the BLE gateway that aggregates scans and forwards to cloud.
- Beacons are iBeacon + Eddystone compatible.
- Healthcare is the primary vertical — many features (patient safety, hand hygiene, nurse call integration) are healthcare-specific.
- Cloud Beacon (USB-powered AC unit) doubles as a 50m fleet manager for remote OTA + UUID rotation, even where standalone beacons can't reach the internet.
- Cross-listing applies to `wifi-intelligence` (Wi-Fi gateway agents on third-party APs).
