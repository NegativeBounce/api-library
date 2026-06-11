# Vortexa

Real-time waterborne energy trade-flow and freight analytics, tracking crude, clean/dirty products and LNG cargo movements with port-to-port freight pricing and inventories.

**Tier:** Enterprise
**Auth:** API Key
**Last researched:** 2026-06-11

## Use cases

- Tracking global energy flows (crude, refined products, LNG) down to grade level, with full cargo history of every tanker over 5,000 dwt from 2016.
- Monitoring vessel positions, diversions and voyages for early signals of disruption (e.g. Strait of Hormuz, Middle East crisis impacts).
- Pricing freight across 90,000+ port-to-port routes via "Anywhere Freight Pricing" for shipping-cost and tanker-revenue analysis.
- Building custom models with raw flow/freight/inventory data via REST API, Python SDK or Excel add-in.

## Pricing

- **Free tier:** None.
- **Paid tiers:** Subscription/contract; pricing not public.
- **Enterprise:** Contact sales; API, Python SDK, Excel integration included per plan.
- **Notes:** Tracks $3.4T+ in annual waterborne energy trades; 700M+ data points processed daily. Claims view into >99% of global energy flows.

## Authentication

API key. RESTful API using HTTP/REST/JSON; also Python SDK and Excel add-in. Credentials provisioned per contract.

## Endpoints

- **Base URL:** Provided on contract (see vortexa.com/product/integrations).
- **Key capabilities:**
  - Cargo movements / voyages (aggregated and vessel-specific).
  - Freight pricing (Anywhere Freight Pricing) across active + possible routes.
  - Onshore/floating inventories; refinery flows; net imports/exports.

## Example call

```bash
# Illustrative; confirm endpoints/auth from Vortexa API docs
curl -H "Authorization: Bearer $VORTEXA_API_KEY" \
  "https://api.vortexa.com/v6/cargo-movements?filter_products=crude&filter_origins=..."
```

```python
# Vortexa provides an official Python SDK
from vortexasdk import CargoMovements
df = CargoMovements().search(filter_time_min="2026-06-01", filter_time_max="2026-06-10").to_df()
```

## Rate limits

Per contract; not publicly published.

## SDKs / Libraries

- **Official:** Vortexa Python SDK (`vortexasdk`); REST API; Excel add-in.
- **Community:** None notable.

## Documentation

- Main docs: https://www.vortexa.com/product/integrations/energy-data-api-integration
- API reference: Vortexa developer docs (provided with subscription).

## Notes

- Strongest for **energy/oil & gas** flows + freight specifically; pairs well with Baltic Exchange tanker indices for rate context.
- Anywhere Freight Pricing (50,000+ active, 70M possible CPP routes) is a differentiator for tanker-revenue and freight-cost modelling.
- **Cross-reference:** for official customs trade stats see UN Comtrade (`semiconductor-intelligence/un-comtrade.md`); for daily port/chokepoint trade-volume estimates see IMF PortWatch (`port-congestion/imf-portwatch.md`).
- Competes most directly with Kpler on energy; Kpler is broader across commodity classes, Vortexa is energy-deep with strong freight pricing.
