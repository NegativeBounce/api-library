# SkyTruth

Conservation-technology nonprofit (501(c)(3)) building open-source satellite-based environmental monitoring tools. Free APIs and datasets for ocean pollution, mining, gas flaring, and conservation progress tracking. Founded 2001.

**Tier:** Free
**Auth:** None for most products; API tokens for some integrations
**Last researched:** 2026-05-09

## Use cases

- Ocean pollution monitoring relevant to the Strait of Malacca — chronic oil discharges from vessels, ship-to-ship transfer slicks, illegal dumping.
- Cerulean (cataloged separately) — AI oil-spill detection on Sentinel-1 SAR globally.
- Flaring map — natural gas flaring globally; relevant for offshore E&P near the Strait approaches.
- Mining monitor — mountaintop and other surface mining environmental impacts.
- Co-development with Global Fishing Watch (separate org) for IUU fishing — relevant to dark-vessel work in Strait approaches.

## Pricing

- **Free tier:** All tools and APIs are free for public use.
- **Paid tiers:** None.
- **Enterprise:** Not applicable; sponsorships and grants fund development.
- **Notes:** Some endpoints require an API token for rate-limit control; tokens are free.

## Authentication

Most data products are anonymously accessible. Some specific APIs (e.g., bulk Cerulean exports, mining elevation data) issue free API tokens via signup.

## Endpoints

- **Public site:** `https://skytruth.org/`
- **Cerulean (oil spills):** `https://cerulean.skytruth.org/`
- **Monitor (satellite imagery):** `https://monitor.skytruth.org/`
- **30x30 Progress Tracker:** `https://30x30.skytruth.org/`
- **Flaring map:** `https://skytruth.org/projects/flaring`
- **APIs:** Project-specific; see each product page for documentation.

## Example call

```bash
# Cerulean detections — see the cerulean.md entry for the dedicated API.
# SkyTruth-wide datasets are typically downloaded as GeoTIFF / GeoJSON files from project pages.
```

## Rate limits

Reasonable use; specific limits per project. Not strictly published.

## SDKs / Libraries

- **Official:** Project-specific Jupyter notebooks and Python tooling published on GitHub (https://github.com/SkyTruth).
- **Community:** Active research community using SkyTruth data.

## Documentation

- Main site: https://skytruth.org/
- GitHub: https://github.com/SkyTruth
- Contact: hello@skytruth.org

## Notes

- Strong fit when the use case is environmental + accountability — SkyTruth's mission is to "make environmental harm visible."
- Cerulean is the most directly relevant product for Strait-of-Malacca oil-spill detection — see the dedicated entry.
- Excellent partner for fusion alongside Skylight (IUU fishing), Copernicus (Sentinel imagery), and Global Fishing Watch.
