# Freightos Baltic Index (FBX)

The leading IOSCO-compliant daily container freight rate index, issued with the Baltic Exchange, measuring 40' container spot rates across major global tradelanes.

**Tier:** Freemium
**Auth:** API Key
**Last researched:** 2026-06-11

## Use cases

- Benchmarking global ocean container freight rates (40' FEU) across 13 major lanes for shipping-cost context in reports.
- Tracking daily spot-rate movements as a shipping-market bellwether and disruption indicator.
- Index-linking freight contracts or analyzing rate-change clauses (FBX is used for index-linked contracts and derivatives on CME and SGX).
- Pulling specific lane data (e.g. FBX01 China–US West Coast, FBX11 China–North Europe, FBX13 China–Mediterranean).

## Pricing

- **Free tier:** Headline index values are publicly visible; interactive display and chart exports available.
- **Paid tiers:** Personal package — CSV download. Freightos Data subscription adds historical data + live event feeds (congestion, strikes, weather).
- **Enterprise:** API access included in the enterprise package; also distributed via Barchart cmdty.
- **Notes:** Updated daily at 12:00 UTC. IOSCO- and UK BMR-compliant; Baltic Exchange (BEISL) is Benchmark Administrator, Freightos is Calculating Agent.

## Authentication

API key (enterprise package). CSV download for personal package. Confirm header scheme at onboarding.

## Endpoints

- **Base URL:** Provided with enterprise data package (also via Barchart cmdty API).
- **Key data:**
  - FBX global composite + 13 lane sub-indices (e.g. FBX01, FBX03, FBX11, FBX13), 40' FAK spot rates.
  - Historical series (subscription).

## Example call

```bash
# API access is enterprise-gated; personal package is CSV download.
# Via Barchart cmdty (example pattern — confirm exact endpoint/symbol):
curl "https://ondemand.websol.barchart.com/getQuote.json?apikey=$BARCHART_KEY&symbols=FBX.CM"
```

## Rate limits

Not publicly published; depends on package (CSV vs. enterprise API vs. Barchart).

## SDKs / Libraries

- **Official:** None language-specific; CSV + API + Barchart cmdtyView.
- **Community:** Index values mirrored by third-party data sites (e.g. MacroMicro) for charting.

## Documentation

- Main docs: https://www.freightos.com/freightos-baltic-index/
- API reference: https://resources.freightos.com/ (API access via enterprise package); Barchart: https://www.barchart.com/cmdty/data/pricing-network/freightos

## Notes

- Rates derive from real, anonymized transactions on the WebCargo by Freightos platform — not polls — across 1,000+ consenting companies (1.85B+ data points).
- The standard **container** freight benchmark; pair with Baltic Exchange for dry-bulk/tanker, and Xeneta for granular lane-level contract rates.
- **Cross-reference:** the broader Freightos Terminal also offers air + ocean rate data and event feeds beyond the index itself.
