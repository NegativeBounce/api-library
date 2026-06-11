# Global Fishing Watch

Nonprofit open-data platform exposing AIS-derived vessel presence, fishing-effort, and identity data via the 4Wings API, with EEZ/MPA overlays — strong for IUU and dark-fishing analysis.

**Tier:** Free
**Auth:** API Token
**Last researched:** 2026-06-11

## Use cases

- Mapping apparent fishing effort and AIS vessel presence by area, time, and gear type for maritime-domain-awareness reports.
- Overlaying activity against EEZs and Marine Protected Areas to flag potential illegal/unregulated fishing.
- Identity and registry lookups (GFW vessel identity dataset) for cross-referencing suspect vessels.
- Detecting AIS gaps / "dark" periods as an indicator of disabling/spoofing in sensitive zones.

## Pricing

- **Free tier:** Free, open access under GFW data terms (registration for an API token). Nonprofit (501(c)(3); founded by Oceana, SkyTruth, Google).
- **Paid tiers:** None.
- **Enterprise:** N/A.
- **Notes:** Attribution/usage terms apply; intended for research, transparency, and enforcement support. Not a commercial real-time tracking SLA.

## Authentication

API token (Bearer) obtained from a free Global Fishing Watch account / API portal.

## Endpoints

- **Base URL:** `https://gateway.api.globalfishingwatch.org/` (4Wings + vessels/events APIs)
- **Key APIs:**
  - **4Wings API** — gridded activity (apparent fishing effort, AIS vessel presence) by bbox/time.
  - **Vessels API** — vessel identity search and details.
  - **Events API** — encounters, loitering, port visits, AIS gaps.
  - **Datasets / reference** — EEZ, MPA, RFMO regions for overlays.

## Example call

```bash
# Illustrative; confirm dataset IDs/params from GFW API docs
curl -H "Authorization: Bearer $GFW_TOKEN" \
  "https://gateway.api.globalfishingwatch.org/v3/vessels/search?query=EVER%20GIVEN&datasets[0]=public-global-vessel-identity:latest"
```

## Rate limits

Defined by GFW API terms; reasonable-use limits for the free token. See API portal.

## SDKs / Libraries

- **Official:** `gfwr` (R package); documented REST endpoints. Python access via standard HTTP clients.
- **Community:** Various notebooks/wrappers in the GFW GitHub org.

## Documentation

- Main docs: https://globalfishingwatch.org/our-apis/
- API reference: https://globalfishingwatch.org/our-apis/documentation
- Platform update (AIS vessel presence via 4Wings): https://globalfishingwatch.org/platform-update/global-ais-vessel-presence-dataset/

## Notes

- Unique value is the **analytics layer** (fishing effort, encounters, AIS gaps, EEZ/MPA context) rather than raw real-time positions — complementary to commercial AIS feeds.
- Best-in-class for IUU-fishing and transparency use cases; not a substitute for low-latency commercial tracking.
- Cross-reference: pairs with dark-vessel-detection providers (e.g. Skylight, `dark-vessel-detection/skylight.md`) and environmental feeds for a fuller MDA picture.
