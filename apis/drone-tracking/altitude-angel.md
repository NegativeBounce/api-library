# Altitude Angel GuardianUTM

A global UTM (Unmanned Traffic Management) cloud platform whose APIs provide real-time airspace, ground-hazard, and fused air-traffic ("surveillance") data — letting you consume a correlated picture of drone and crewed traffic without owning sensors, and optionally feed your own sensor data in.

**Tier:** Freemium
**Auth:** OAuth 2.0 (Bearer token; client credentials / device flow)
**Last researched:** 2026-06-17

## Use cases

- Pull authoritative airspace, no-fly-zone, and ground-hazard data for 155+ countries through one canonical API instead of stitching together national sources.
- Consume Altitude Angel's fused, real-time air-picture (Surveillance API "out" endpoints) to see correlated drone/crewed traffic and receive conflict alerts in a monitored area.
- Feed your own drone-detection sensor or aggregated RID feed *into* GuardianUTM ("Surveillance In") so detections are fused with the wider network.
- Automate flight planning and digital airspace approvals within "UTM Ready" zones.

## Pricing

- **Free tier:** Free 30-day API trial; free developer account at developers.altitudeangel.com. Some flight-planning/approval tools are free to end users.
- **Paid tiers:** GuardianUTM Cloud sold as three API packages (data-ingest/fusion vs. strategic feed access); pricing not publicly listed — quoted per package.
- **Enterprise:** National-scale U-space/UTM deployments for ANSPs and regulators; contact sales.
- **Notes:** Surveillance and Approval-Services integrations require an onboarding/registration process before go-live.

## Authentication

Register a developer account at `https://developers.altitudeangel.com`. APIs use OAuth 2.0 Bearer tokens. For the Surveillance API, sensors/systems are pre-registered (support ticket) and obtain a device token either via an OAuth2 `client_credentials` request (scope `surveillance_api`, `token_format=jwt`, `device_id=<sensor id>`) or, for headless devices, via a pairing flow that returns a JWT `accessToken` + `refreshToken`. Minimum TLS 1.2. Always resolve service hosts via fresh DNS (IPs rotate).

## Endpoints

- **Base URL:** `https://surveillance.altitudeangel.com/v1` (Surveillance); broader services under the GuardianUTM Cloud base (resolve via DNS per docs).
- **Key endpoints:**
  - `POST /devices/{deviceId}/relay` — relay position reports for a known device (Surveillance In).
  - `POST /pairing/{sensorId}` — consume a pairing token for a headless sensor (no auth).
  - Surveillance "Out" endpoints — retrieve device and position-report data for a known user.
  - GuardianUTM Cloud — airspace/navigation data (100+ categories), ground hazards (80+ categories), flight-plan creation, approvals, conflict alerts, area hazard reports.

## Example call

```bash
# Submit a position report (Surveillance In) for a registered device
curl -X POST "https://surveillance.altitudeangel.com/v1/devices/$DEVICE_ID/relay" \
  -H "Authorization: Bearer $ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
        "reports": [
          { "lat": 51.5074, "lng": -0.1278, "altitude": 120,
            "timestamp": "2026-06-17T12:00:00Z" }
        ]
      }'
```

## Rate limits

Not publicly documented.

## SDKs / Libraries

- **Official:** REST APIs documented at docs.altitudeangel.com; no broadly published language SDK — integrate over HTTPS/OAuth2.
- **Community:** None notable.

## Documentation

- Main docs: https://docs.altitudeangel.com/
- API reference: https://docs.altitudeangel.com/docs/surveillance-api ; developer portal at https://www.altitudeangel.com/developer-portal

## Notes

- **Reality check on "ADS-B for drones":** GuardianUTM gives a *fused* air picture, but its live drone-traffic richness depends on what sensors/feeds are connected in a given area plus network Remote ID coverage — it is not yet a globally complete passive drone feed the way ADS-B Exchange is for crewed aircraft.
- Strongest, most mature global option in this category for authoritative airspace + UTM data and for fusing your own detections.
- Overlaps with airspace/geofencing data categories; cataloged here because its differentiator for drone *tracking* is the Surveillance fusion + UTM traffic feed.
