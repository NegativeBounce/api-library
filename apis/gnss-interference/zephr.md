# Zephr.xyz

Networked GNSS positioning company providing an SDK and cloud APIs that improve GPS accuracy on consumer mobile devices via cooperative satellite-measurement corrections. Has a research-stage GNSS jamming/spoofing detection capability funded by an AFRL SBIR contract.

**Tier:** Freemium (SDK)
**Auth:** API key (provisioned to SDK integrators)
**Last researched:** 2026-05-07

## Use cases

- **Primary product:** AdTech, AR, mobility, logistics, insurance, gaming, and mapping apps that need sub-meter GNSS accuracy on commodity Android (and select iOS) devices.
- Apps that want a "spoof-proof" positioning engine that consumes raw satellite measurements rather than the OS-reported lat/lon (resistant to GPS spoofing apps).
- Pedestrian-to-vehicle collision avoidance and search-and-rescue use cases requiring relative-distance precision between devices.
- **Research stage:** GNSS jamming/spoofing detection and emitter geolocation via crowd-sourced mobile devices, slated for integration with DoD's Tactical Assault Kit (TAK) and DHS's Team Awareness Kit (TAK). Not yet a commercial public API.

## Pricing

- **Free tier:** Developer trial / demo access to the Zephr Positioning SDK is available for evaluation.
- **Paid tiers:** Commercial SDK licensing — pricing not publicly listed; contact Zephr for quotes.
- **Enterprise:** Custom partnerships, especially around the AugPNT military/government use cases.
- **Notes:** Zephr is venture-backed (~$4M+ raised as of 2025) and pricing is in flux as the company scales the cooperative-positioning network.

## Authentication

API key issued by Zephr to SDK integrators. Cloud APIs are accessed via SDK from mobile clients with bundled credentials.

## Endpoints

- **Base URL:** Not publicly documented; SDK integrators receive endpoint and credential details after sign-up.
- **Key product surfaces:**
  - **Zephr Positioning SDK** (Android-first, iOS in progress) — cooperative GNSS positioning achieving <50 cm accuracy in open-sky.
  - **Zephr Cloud APIs** — backend correction services running on Google Cloud.
  - **Zephr Local AI Platform** — local-context APIs and MCP integration for AI applications needing spatial context.
  - **GNSS Jamming/Spoofing Detection SDK (research stage)** — to be available as an SDK; integration with TAK platforms expected as the AFRL Phase II program completes.

## Example call

```bash
# Zephr's product is primarily an Android/iOS SDK rather than a server-side REST API.
# Public REST examples are not published; sign up at https://www.zephr.xyz/ for SDK access.
```

```kotlin
// Pseudo-Kotlin (Android) usage of the Zephr Positioning SDK
val zephr = ZephrClient.initialize(apiKey = "...")
zephr.startPositioning { fix ->
    println("lat=${fix.latitude} lon=${fix.longitude} σ=${fix.uncertaintyMeters}m")
    if (fix.isSpoofingSuspected) {
        // Research-stage: warn the user / fall back to backup nav
    }
}
```

## Rate limits

Not publicly documented.

## SDKs / Libraries

- **Official:** Zephr Positioning SDK (Android; iOS roadmapped). Distributed via Zephr's developer portal.
- **Community:** None — Zephr is a small, recently-founded company with closed SDK distribution.

## Documentation

- Main site: https://www.zephr.xyz/
- Google Cloud customer story (good architectural overview): https://cloud.google.com/blog/products/networking/reimagining-gps-zephr-powers-real-time-gnss-precision-on-the-cloud
- AFRL contract press release: https://insidegnss.com/zephr-xyz-awarded-1-7m-air-force-research-laboratory-contract-for-gnss-jamming-detection-technology/

## Notes

- **Tangential fit for GPS jamming coverage maps.** Zephr's primary product is *receiver-side accuracy improvement* and *spoof-resistant positioning*, not generating global jamming-zone polygons. Their networked-detection R&D could in the future contribute to a crowd-sourced jamming map, but as of the last research date, that capability is in AFRL Phase II testing in Ukraine and U.S. military exercises — not a commercial map API.
- If your use case is "I want to know whether **this user's** mobile device is being jammed/spoofed right now" — Zephr's research-stage SDK is interesting, since it can flag interference at the device level. If your use case is "show me a global map of where interference is happening" — Zephr is **not** the right tool.
- Founded 2022 in Boulder/Louisville, Colorado. Co-founded by Sean Gorman (CEO) and others with PNT and geospatial backgrounds.
- Backed by Space Capital, Kickstart, NSIN Propel Hawaii, First Spark Ventures, and Space Angels.
- Listed here per explicit user request, with caveat above. Reconsider in 6–12 months if/when the jamming detection SDK ships commercially.
