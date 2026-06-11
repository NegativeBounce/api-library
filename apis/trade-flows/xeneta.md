# Xeneta

Ocean and air freight rate benchmarking platform exposing 600M+ real-time and contract freight rates via API for procurement, pricing and market-intelligence integration.

**Tier:** Enterprise
**Auth:** API Key
**Last researched:** 2026-06-11

## Use cases

- Benchmarking ocean (and air) freight rates on specific lanes for shipping cost analysis in intelligence reports.
- Feeding real-time spot and contract rates into analytics, tender, finance, quoting or pricing systems.
- Tracking rate movements as a leading indicator of supply-chain cost pressure and disruption (e.g. chokepoint diversions raising rates).
- Supporting freight-procurement decisions for shipping-company and logistics personas.

## Pricing

- **Free tier:** None.
- **Paid tiers:** Subscription/contract; API is an add-on to platform subscriptions.
- **Enterprise:** Contact sales.
- **Notes:** Pricing not public. Data sourced from crowdsourced/contributed rate data across shippers and forwarders (600M+ rates).

## Authentication

API key. REST/JSON; credentials provisioned per subscription. No platform training required to consume via API.

## Endpoints

- **Base URL:** Provided on subscription (see xeneta.com/products/api).
- **Key capabilities:**
  - Ocean freight rate benchmarks by corridor/lane (spot + long-term contract).
  - Air freight rate benchmarks (separate Air API).
  - Market data for integration into tender/finance/quoting systems.

## Example call

```bash
# Illustrative; confirm endpoints/auth from Xeneta API docs
curl -H "Authorization: Bearer $XENETA_API_KEY" \
  "https://api.xeneta.com/v2/ocean/rates?origin=CNSHA&destination=NLRTM"
```

## Rate limits

Per contract; not publicly published.

## SDKs / Libraries

- **Official:** REST/JSON API; no language-specific SDK advertised.
- **Community:** None notable.

## Documentation

- Main docs: https://www.xeneta.com/products/api
- API reference: Provided with subscription.

## Notes

- Unlike Kpler/Vortexa (commodity/energy physical flows), Xeneta is **freight-rate-centric** — the price layer rather than the cargo-movement layer. Complementary to flow data.
- Container/ocean focus makes it the natural rate benchmark for shipping-company and forwarder personas; pair with FBX for index-grade container rates.
- **Cross-reference:** for the IOSCO-compliant container index see Freightos Baltic Index (`trade-flows/freightos-baltic-index.md`); for dry-bulk/tanker indices see Baltic Exchange (`trade-flows/baltic-exchange.md`).
