# Aurora Insight

> ⚠️ **Discontinued as of 2023-12-18.** Aurora Insight was acquired by Maxar Technologies in January 2023, rebranded as "Maxar Intelligence RF Solutions," then acquired by HawkEye 360 on December 18, 2023. Original Aurora Insight commercial products are no longer offered under that brand. The two satellites (Charlie and Delta) and the multi-year RF database (1.4–40 GHz) now operate under HawkEye 360. New customers should contact HawkEye 360 directly. Entry retained for historical reference.

Denver-based RF spectrum mapping company that captured radio frequency spectrum and wireless network data via ground, aircraft, and satellite-based sensors from 2016 through 2023. Served wireless carriers, regulators, investors, and defense/intelligence customers.

**Tier:** Discontinued (formerly Enterprise)
**Auth:** N/A
**Last researched:** 2026-05-10

## Use cases

- (Historical) Wideband (1.4–40 GHz) RF spectrum scanning at regional scale
- (Historical) Wireless infrastructure mapping for carriers and regulators
- (Historical) Spectrum-use intelligence for defense and intelligence agencies
- (Historical) Multi-source GEOINT fusion when paired with Maxar imagery (2023 only)

## Pricing

- **Free tier:** None.
- **Paid tiers:** Originally subscription-based, never publicly listed.
- **Enterprise:** Closed. Successor: HawkEye 360 (see `apis/dark-vessel-detection/hawkeye-360.md`).
- **Notes:** Total funding ~$18M before acquisition. Investors included Maxar, ValueStream, Alsop Louie, Promus Ventures.

## Authentication

N/A — service no longer offered under the Aurora Insight brand. The HawkEye 360 product portfolio now includes the integrated wideband-scan capability.

## Endpoints

- **Base URL:** N/A (decommissioned)
- **Key endpoints (historical):**
  - REST API for spectrum measurement queries (terrestrial + airborne + satellite sources)
  - Frequency-by-location heatmaps
  - Wireless network coverage and signal-strength layers

## Example call

N/A. For continuing access to the underlying capability, query HawkEye 360's RFGeo or wideband-scan products under their successor offering.

## Rate limits

N/A.

## SDKs / Libraries

- **Official:** N/A.
- **Community:** None publicly available.

## Documentation

- Acquisition announcement (HawkEye 360): https://www.prnewswire.com/news-releases/hawkeye-360-expands-spectrum-scanning-through-the-acquisition-of-rf-solutions-from-maxar-intelligence-302017009.html
- SpaceNews coverage: https://spacenews.com/hawkeye-360-acquires-maxars-rf-solutions-business-unit/
- CB Insights company page (historical): https://www.cbinsights.com/company/aurora-insight

## Notes

- Charlie and Delta satellites continue to operate under HawkEye 360, contributing to a 36+ satellite constellation as of 2025.
- HawkEye 360 inherited the multi-year 1.4–40 GHz database, including 26–40 GHz coverage that was new to its constellation.
- Aurora Insight was one of the original six commercial RF providers awarded NRO Strategic Commercial Enhancements BAA contracts in 2022 (alongside HawkEye 360, Kleos Space, PredaSAR, Spire, Umbra).
- Cross-listing: capability now consolidated under `dark-vessel-detection` (HawkEye 360 entry).
