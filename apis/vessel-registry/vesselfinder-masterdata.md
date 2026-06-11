# VesselFinder Vessel Particulars (MasterData) API

Credit-based API returning comprehensive vessel master data — particulars, flag, builder and ownership — for one or more vessels specified by IMO number.

**Tier:** Paid
**Auth:** API Key
**Last researched:** 2026-06-11

## Use cases

- Bulk-retrieving vessel particulars (name, type, dimensions, flag state, builder, ownership) by IMO for fleet enrichment.
- Pay-as-you-go particulars lookups without an enterprise contract.
- Combining MasterData with VesselFinder's other credit-based services (PortCalls, Distance) in a single credit pool.

## Pricing

- **Free tier:** None.
- **Paid tiers:** Credit-based. MasterData costs ~3 credits per vessel; you are charged only for data delivered. Credits valid 12 months; prices exclude VAT.
- **Enterprise:** Higher-volume credit packs / contact sales.
- **Notes:** Example: master data for 10 vessels = 30 credits. Credits shared across Vessels, PortCalls, MasterData, Distance services.

## Authentication

API key (purchase credits to activate). Key passed per VesselFinder's documented scheme.

## Endpoints

- **Base URL:** VesselFinder API (see vesselfinder.com/api documentation)
- **Key endpoints:**
  - MasterData (Vessel Particulars) — input IMO(s); returns particulars, flag, builder, ownership fields.
  - Related credit-based endpoints: Vessels (positions), PortCalls, Distance.

## Example call

```bash
# Illustrative; confirm exact path/params from VesselFinder API docs
curl "https://api.vesselfinder.com/masterdata?userkey=$VF_API_KEY&imo=9811000"
```

## Rate limits

Governed by credit balance rather than strict rate caps; confirm per-second/connection limits in the API docs.

## SDKs / Libraries

- **Official:** None language-specific; REST/JSON.
- **Community:** None notable.

## Documentation

- Main docs: https://www.vesselfinder.com/vessel-particulars-api
- API reference: https://www.vesselfinder.com/api (full technical docs + sample requests)

## Notes

- **Cross-reference:** VesselFinder is also cataloged in `maritime-ais` for AIS positions. This entry is the distinct **MasterData / particulars** product; credits are shared across both.
- Ownership depth is lighter than MarineTraffic/Lloyd's/S&P — good for particulars and basic ownership, less so for full beneficial-ownership chains.
- Credit model makes it cost-predictable for targeted lookups vs. always-on enterprise feeds.
