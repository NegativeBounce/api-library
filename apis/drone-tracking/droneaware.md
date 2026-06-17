# DroneAware Network

A free, community-powered crowd-sourced Remote ID detection network — the closest current analogue to an "ADS-B Exchange for drones." Volunteers run low-cost Raspberry Pi nodes that listen for FAA-mandated Remote ID broadcasts (Wi-Fi/Bluetooth) and contribute detections to a shared live map, with email alerts and flight-history replay.

**Tier:** Free
**Auth:** Account (free); public API availability not documented
**Last researched:** 2026-06-17

## Use cases

- See live drone activity on a shared community map without buying a commercial detection system.
- Get email alerts when a drone is detected near your node or your friend-network's coverage.
- Replay historical drone flight paths over an area by date (flight-history calendar).
- Identify make/model of detected drones via cross-reference against the FAA Declaration of Compliance database (150+ manufacturers).

## Pricing

- **Free tier:** Entire platform is free. Run a node (hardware ~$150–175: Raspberry Pi 4/5 + two USB adapters + power) or join free with no node and share a friend's coverage.
- **Paid tiers:** None.
- **Enterprise:** N/A.
- **Notes:** Coverage is only as good as the density of community nodes in a given area — sparse outside populated/enthusiast regions.

## Authentication

Create a free account at `https://droneaware.io/login.html`. Node operators flash DroneAware software onto a Raspberry Pi (~10-min setup). A documented public/developer API for programmatic detection retrieval is **not publicly advertised** as of this research — integration today is via the web map, account alerts, and node software.

## Endpoints

- **Base URL:** Not publicly documented (web platform; no advertised REST API).
- **Key endpoints:** N/A — interaction is via live map (`/live.html`), account email alerts, and history calendar. Node software ingests local RID broadcasts and POSTs detections to the shared network backend.

## Example call

```bash
# No public developer API documented. Interaction is via the web app:
#   Live map:        https://droneaware.io/live.html
#   Build a node:    https://droneaware.io/enroll.html
#   Aircraft DB:     https://droneaware.io/database.html
```

## Rate limits

N/A — no public API documented.

## SDKs / Libraries

- **Official:** Node software image (Raspberry Pi). No developer SDK.
- **Community:** Related open-source RID receivers exist independently (OpenDroneID receiver-android, dronetag/drone-scanner, cyber-defence-campus/RemoteIDReceiver).

## Documentation

- Main docs: https://droneaware.io/
- API reference: Not published — contact the project for integration/API access.

## Notes

- **Directly answers the "AIS/ADS-B for drones" question:** this is the crowd-sourced-network model applied to Remote ID, but it is **early-stage** and coverage is patchy. It only sees *broadcasting, RID-compliant* drones within ~1 mile of a node; non-compliant, spoofed, or RID-disabled drones are invisible.
- No SLA; proof-of-concept-grade reliability. Good for community/situational awareness, not guaranteed detection.
- If a public API is required, confirm availability with the project before depending on it.
