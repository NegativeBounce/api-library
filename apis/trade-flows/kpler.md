# Kpler

Real-time commodity trade-flow intelligence tracking cargo and vessels across 40+ markets, with volumes, grades, freight, inventories, origins/destinations and buyer/seller detail.

**Tier:** Enterprise
**Auth:** API Key / OAuth
**Last researched:** 2026-06-11

## Use cases

- Tracking global commodity flows (crude, refined products, LPG, LNG, chemicals, dry bulk, metals, agri) by origin, destination, grade and volume for regional intelligence reports.
- Identifying buyers, sellers and forecasted destinations across 40+ markets to anticipate supply-demand shifts.
- Combining cargo flows with freight, floating storage and inventories for chokepoint/disruption impact analysis (e.g. Strait of Hormuz, Suez diversions).
- Embedding flow data into a maritime intelligence app via API, Snowflake, LiveDB, or Excel add-in.

## Pricing

- **Free tier:** None.
- **Paid tiers:** Subscription/contract; pricing not public.
- **Enterprise:** Contact partnerships team; sandbox + API docs provided on engagement. Also resold via ICE (ICE Connect / ICE API & bulk files).
- **Notes:** Kpler is now the parent of Spire Maritime, MarineTraffic and FleetMon (post-acquisitions) — many maritime datasets consolidate here.

## Authentication

API key / OAuth per contract. Multiple delivery channels: REST API, Snowflake Data Share, Kpler LiveDB, Excel Add-In; also via ICE's API/bulk services.

## Endpoints

- **Base URL:** Provided on contract (see kpler.com developer/partnerships; ICE developer portal for ICE-delivered access).
- **Key capabilities:**
  - Cargo/trade flows by commodity, grade, origin/destination, player.
  - Freight, fixtures, floating storage, inventories, refinery data.
  - Vessel tracking + ownership (Kpler AIS) integrated with flows.

## Example call

```bash
# Illustrative; endpoints/auth provided on partnership onboarding
curl -H "Authorization: Bearer $KPLER_TOKEN" \
  "https://api.kpler.com/v1/flows?product=crude&fromZone=Russia&toZone=India"
```

## Rate limits

Per contract; not publicly published.

## SDKs / Libraries

- **Official:** REST API, Snowflake share, LiveDB, Excel Add-In; docs + sandbox on engagement.
- **Community:** None notable (enterprise-gated).

## Documentation

- Main docs: https://www.kpler.com/ (product/commodities; industries/software-technology for API)
- API reference: https://developer.ice.com/ (Kpler via ICE) and Kpler partnerships onboarding.

## Notes

- Tracks 650+ oil grades, 36,000+ vessels; flows validated against customs figures and in-house analysts; data from terrestrial + satellite AIS, satellite imagery, customs records, port intelligence.
- **Cross-reference:** Kpler now underlies several existing entries — Spire Maritime (`maritime-ais`, `port-congestion`), MarineTraffic (`maritime-ais`, `port-congestion`, `vessel-registry`), FleetMon (`maritime-ais`). This entry is the **commodity trade-flow** product specifically.
- For official customs trade stats (vs. Kpler's real-time physical-flow estimates), cross-reference UN Comtrade (`semiconductor-intelligence/un-comtrade.md`) and IMF PortWatch trade estimates (`port-congestion/imf-portwatch.md`).
- The single most comprehensive option for your shipping/mining-platform personas, but enterprise-priced and gated.
