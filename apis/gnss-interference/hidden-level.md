# Hidden Level

Passive RF sensing and airspace monitoring company offering Airspace Monitoring Service (AMS) and RF Data-as-a-Service for drone detection and counter-UAS missions. Operates a sensor network across the full RF spectrum.

**Tier:** Enterprise
**Auth:** Customer-provisioned (RF Data-as-a-Service)
**Last researched:** 2026-05-07

## Use cases

- Critical-infrastructure operators (airports, government facilities, military bases, stadiums) needing real-time detection and geolocation of drones in their airspace.
- Federal/state/local agencies deploying counter-UAS capability with Title 18-compliant passive RF sensing (no signal demodulation).
- Defense customers requiring multi-domain RF situational awareness in high-interference environments.
- Air National Guard bases and similar facilities using Hidden Level's "as-a-service" model for rapid airspace security overhauls.

## Pricing

- **Free tier:** None.
- **Paid tiers:** None publicly listed.
- **Enterprise:** All sales are enterprise — sensors as hardware purchase, or AMS / RF Data-as-a-Service as managed offerings. Contact Hidden Level sales.
- **Notes:** Series C-funded ($120M+ raised by 2025). Customer base is heavy on DoD, federal agencies, and critical-infrastructure operators.

## Authentication

Customer-provisioned API access (for the RF Data-as-a-Service offering); no public developer signup. Hidden Level's systems are designed for closed deployments at customer sites with managed cloud connectivity.

## Endpoints

- **Base URL:** Not publicly documented; provisioned per deployment.
- **Key products (not endpoints):**
  - **Airspace Monitoring Service (AMS)** — managed service deploying Hidden Level sensors at customer sites, returning real-time drone tracks and RF activity.
  - **RF Data-as-a-Service (DaaS)** — programmatic access to RF/airspace data feeds for integrators.
  - **Multiband Passive Radar** — sensor capability for tracking aerial objects across an extended RF spectrum.
  - **DroneOps (with About Objects)** — 3D airspace awareness on Apple Vision Pro (announced Oct 2025).

## Example call

```bash
# No public API documentation. Engagement is via direct sales:
# https://www.hiddenlevel.com/contact
```

## Rate limits

Not publicly documented.

## SDKs / Libraries

- **Official:** None published publicly.
- **Community:** None — Hidden Level operates in classified/sensitive use cases and does not release SDKs to the general developer market.

## Documentation

- Main site: https://www.hiddenlevel.com/
- FAQ: https://www.hiddenlevel.com/faq
- Stewart ANGB case study: https://www.hiddenlevel.com/thought-leadership/stewart-angb-secured--hidden-levels-24-hour-airspace-security-overhaul

## Notes

- **Tangential fit for GNSS jamming maps.** Hidden Level's primary mission is drone detection and counter-UAS via passive RF sensing — not generating global GPS jamming coverage maps. Their sensors do detect signals across the RF spectrum (which includes GNSS bands), and their broader RF DaaS could include GNSS interference observations near customer sites, but this is not their advertised product or a published global feed.
- If your goal is a "GPS jamming coverage map" as in a global polygon dataset, Hidden Level is **not** the right tool. They are a localized RF awareness vendor.
- Useful in this catalog if your underlying need is broader: detecting *any* RF interference (including GNSS) at specific high-value sites you control or operate.
- Founded 2018 in Syracuse, NY by Jeff Cole and Gary Dominicos. Vertically integrated US manufacturing.
- Compliance posture: Title 18 of the U.S. Code (no demodulation of intercepted signals — only presence/location/pattern matching).
- Listed here per explicit user request, with caveat above.
