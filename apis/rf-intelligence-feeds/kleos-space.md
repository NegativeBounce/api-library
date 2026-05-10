# Kleos Space

> ⚠️ **Discontinued as of 2023-07-26.** Kleos Space announced bankruptcy on July 26, 2023, after its principal creditor (Pure Asset Management) declined to extend credit. ASX trading was suspended in May 2023 and the company was delisted on August 28, 2023. As of June 2024, no successor had publicly emerged. The 16-satellite constellation (4 clusters, 2 of which had partial failures pre-bankruptcy) is no longer commercially operated. Entry retained for historical reference and for any researchers working with archived Kleos LOCATE datasets.

Luxembourg-based commercial RF reconnaissance company (2017–2023) that operated 4-satellite clusters in formation flight to provide multilateration-based RF geolocation. Sold subscription access via single-user, team, and enterprise licenses to government, defense, and analytics customers.

**Tier:** Discontinued (formerly Paid / Enterprise)
**Auth:** N/A
**Last researched:** 2026-05-10

## Use cases

- (Historical) Maritime dark-vessel detection in chokepoints (Strait of Hormuz, South China Sea)
- (Historical) Land-vehicle RF geolocation in remote areas
- (Historical) National Reconnaissance Office (NRO) Strategic Commercial Enhancements BAA RF data delivery
- (Historical) Japanese coastline territorial monitoring (via JSI partnership, 2021)

## Pricing

- **Free tier:** None.
- **Paid tiers:** Single-user, team, and enterprise license subscriptions (closed). Customers licensed access; Kleos retained IP and historical datasets.
- **Enterprise:** Closed. ~60% of 2022 revenue came from US defense customers. Carahsoft was the US Government distribution partner.
- **Notes:** Total raised ~€20M+ across multiple rounds before failure.

## Authentication

N/A — service no longer offered.

## Endpoints

- **Base URL:** N/A (decommissioned)
- **Key endpoints (historical):**
  - LOCATE data products — RF emitter geolocations across covered AOIs
  - Subscription-area-of-interest data downloads
  - VHF and X-band payload data (KSF3 cluster onward, 2023)

## Example call

N/A.

## Rate limits

N/A.

## SDKs / Libraries

- **Official:** N/A.
- **Community:** None publicly maintained.

## Documentation

- Bankruptcy announcement (SpaceNews): https://spacenews.com/geospatial-intelligence-startup-kleos-space-files-for-bankruptcy/
- Wikipedia entry (most current historical record): https://en.wikipedia.org/wiki/Kleos_Space
- Payload Space coverage: https://payloadspace.com/kleos-space-declares-bankruptcy/

## Notes

- Constellation: 4 clusters of 4 satellites each = 16 satellites total. Two satellites (one from cluster 2, one from cluster 3) had technical issues pre-bankruptcy and were written off.
- Clusters: KSM1 (Scouting Mission, Nov 2020, 37° inclination) → KSF1 (Polar Vigilance, Jun 2021, SSO) → KSF2 (Polar Patrol, Apr 2022) → KSF3 (Polar Observer, Jan 2023, VHF + X-band).
- Multi-satellite-cluster geolocation method — distinct from Unseenlabs (mono-satellite) and HawkEye 360 (3-sat clusters).
- Kleos was one of the original 6 NRO Strategic Commercial Enhancements BAA RF awardees (2022, alongside Aurora Insight, HawkEye 360, PredaSAR, Spire, Umbra).
- Customers with archived LOCATE datasets retained licensed access through their license terms; those datasets are static (no new collections post-bankruptcy).
- For continuing maritime RF capability, see `unseenlabs.md`, `horizon-amber.md`, or HawkEye 360 (`apis/dark-vessel-detection/hawkeye-360.md`).
