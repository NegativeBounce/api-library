# DroneShield (DroneSentry-C2)

An ASX-listed (ASX:DRO) pure-play counter-UAS vendor that is both a sensor maker and a C2 software developer. Its DroneSentry-C2 command-and-control platform fuses RF, radar, optical/thermal, and ADS-B data via the SensorFusionAI engine and exposes a RESTful API plus a WebSocket streaming API so integrators can pull real-time sensor-fused drone detections into existing security systems.

**Tier:** Enterprise (quote-based; hardware + C2 software)
**Auth:** Customer-provisioned (API credentials on deployment)
**Last researched:** 2026-06-17

## Use cases

- Stream real-time sensor-fused drone "objects" (position, classification, threat level) into a third-party C2, SIEM, or security platform via WebSocket.
- Integrate DroneSentry-C2 detections into existing security systems over REST (status, configuration, threat monitoring, response).
- Network fixed-site, on-the-move, and body-worn (RfPatrol) sensors into one operating picture.
- Build counter-UAS dashboards/automation around the SensorFusionAI detection feed (RF + radar + optical + ADS-B).

## Pricing

- **Free tier:** None.
- **Paid tiers:** N/A (not self-serve).
- **Enterprise:** Quote-based; sold as hardware (DroneSentry-X Mk2 RF, RfOne, SentryCiv, optical) plus DroneSentry-C2 software. Cloud-hosted or on-premises.
- **Notes:** Defeat/effector activation is jurisdiction-restricted (where lawful). C2 receives quarterly software updates.

## Authentication

API access is provisioned with a DroneSentry-C2 deployment (cloud or on-prem); credentials are customer-specific. Not a public, self-serve API — engage DroneShield/their reseller for integration credentials and the API specification.

## Endpoints

- **Base URL:** Deployment-specific (cloud-hosted or on-prem server).
- **Key endpoints / interfaces:**
  - RESTful API — system status, configuration, threat monitoring, response actions.
  - WebSocket API — real-time stream of SensorFusionAI sensor-fused objects to integrators/third-party systems.

## Example call

```bash
# Illustrative — base URL and auth are deployment-specific (provided on integration).
# REST status example:
curl -H "Authorization: Bearer $C2_TOKEN" \
  "https://<your-dronesentry-c2-host>/api/v1/status"
# Real-time detections are delivered over a WebSocket channel (sensor-fused objects).
```

## Rate limits

Not publicly documented (enterprise deployment).

## SDKs / Libraries

- **Official:** REST + WebSocket APIs (documentation provided to integrators). No public SDK.
- **Community:** None notable.

## Documentation

- Main docs: https://www.droneshield.com/products-software (product); API spec provided on engagement.
- API reference: Not public — request via DroneShield.

## Notes

- **Detection scope:** sees *non-cooperative* drones (RF/radar/optical), the complement to cooperative Remote-ID tracking feeds in `drone-tracking`. Now also ingests ADS-B for crewed-air correlation.
- Requires deploying DroneShield sensors — this is not a "no-sensor" feed; the API surfaces *your* installation's detections.
- Strong fit when you want a single vendor for both detection hardware and C2 software, with open integration into third-party systems.
