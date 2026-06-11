# Commodities-API

Real-time and historical commodity price API covering 130+ commodities (energy, metals, agriculture) plus currency conversion.

**Tier:** Freemium
**Auth:** API Key
**Last researched:** 2026-06-11

## Use cases

- Real-time Brent/WTI crude, natural gas, and refined-product prices to quantify energy-market reaction to maritime-security events (e.g. Hormuz/Bab el Mandeb disruptions).
- Tracking metals and agricultural commodities for broader supply-chain and inflation context.
- Currency-and-commodity conversion across 170+ currencies for normalized reporting.

## Pricing

- **Free tier:** Limited free access / trial; low request volume.
- **Paid tiers:** Tiered monthly plans by request volume and update frequency (7-day Pro trial advertised).
- **Enterprise:** Higher volume / SLA — contact provider.
- **Notes:** Data sourced from multiple banks/financial providers (incl. World Bank), updated frequently (per-minute on higher tiers). Midpoint (bid/ask average) data.

## Authentication

API key passed as a query parameter (`access_key`).

## Endpoints

- **Base URL:** `https://commodities-api.com/api`
- **Key endpoints:**
  - `GET /latest` — latest prices for requested symbols
  - `GET /{date}` — historical prices for a date
  - `GET /timeseries` — series over a date range
  - `GET /fluctuation` — change between two dates

## Example call

```bash
curl "https://commodities-api.com/api/latest?access_key=$COMMODITIES_KEY&base=USD&symbols=BRENTOIL,WTIOIL,NG"
```

## Rate limits

By plan (per-month request caps; per-minute on higher tiers). Free/trial is limited — see pricing.

## SDKs / Libraries

- **Official:** REST only; documented endpoints.
- **Community:** Generic HTTP clients; some third-party wrappers.

## Notes

- A convenient commercial real-time feed when sub-daily commodity updates matter; for authoritative/free energy data prefer `market-intelligence/eia.md` and for monthly official commodity indices `market-intelligence/world-bank-data.md`.
- Similar commercial alternatives exist (OilPriceAPI, CommodityPriceAPI, API Ninjas commodity endpoints) — this entry stands in for that class; verify current pricing/limits before committing.
- Cross-reference: `trade-flows/` for freight-rate indices and `market-intelligence/alpha-vantage.md` for a multi-asset free-tier option.
