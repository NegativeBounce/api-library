# Cerulean (SkyTruth)

AI-driven oil-spill detection platform processing Sentinel-1 SAR imagery globally. Identifies potential oil spills, attributes them to nearby vessels, and exposes chronic ocean pollution. Free, open API.

**Tier:** Free
**Auth:** API Token (free)
**Last researched:** 2026-05-09

## Use cases

- Continuous oil-spill detection in the Strait of Malacca and approaches (a high-traffic zone with chronic small-spill activity).
- Vessel attribution — Cerulean correlates detected slicks with nearby AIS-tracked vessels to identify likely sources.
- Historical archive of detections going back several years for pattern-of-life analysis.
- Free alternative to commercial services for organisations without EMSA CleanSeaNet eligibility.
- Research / NGO / academic use cases — open data licensing.

## Pricing

- **Free tier:** Free, fully open. API token issued at signup.
- **Paid tiers:** None.
- **Enterprise:** Not applicable.
- **Notes:** Cerulean is funded as a SkyTruth project — sustainable but dependent on grant funding.

## Authentication

API token via SkyTruth account; sent in standard header. Specifics in API docs.

## Endpoints

- **Public site:** `https://cerulean.skytruth.org/`
- **API base URL:** Documented at the Cerulean site under the Developers section.
- **Surface areas:**
  - Slick detections (geospatial polygons + confidence scores)
  - Vessel attribution (linked AIS trajectories)
  - Time-filter and bbox-filter queries

## Example call

```bash
# Illustrative — actual endpoints documented at cerulean.skytruth.org.
curl "https://api.cerulean.skytruth.org/slick/detection/?bbox=-2.0,99.0,6.0,105.5&since=2026-04-01" \
  -H "Authorization: Token $CERULEAN_TOKEN"
```

## Rate limits

Reasonable use; specific numbers not strictly published. Bulk research consumers should email skytruth.

## SDKs / Libraries

- **Official:** Python tooling on GitHub: https://github.com/SkyTruth/cerulean-cloud
- **Community:** Various analysis notebooks.

## Documentation

- Main app: https://cerulean.skytruth.org/
- GitHub: https://github.com/SkyTruth/cerulean-cloud
- Methodology / paper: linked from the SkyTruth site.

## Notes

- For Strait-of-Malacca oil-spill monitoring, Cerulean is uniquely valuable — free, AI-powered, vessel-attribution-aware.
- Pair with Sentinel-1 imagery directly (via Copernicus Data Space — already in `satellite-imagery`) for raw SAR access.
- Chronic-spill detection rate is high in busy lanes; expect many low-confidence detections that need analyst review.
