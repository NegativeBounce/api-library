# Vortexa

Real-time energy cargo-tracking data covering what every tanker >5,000 dwt is carrying — crude, refined products, LPG, and LNG down to grade level — via a RESTful API and Python SDK. Main commodity-by-vessel competitor to Kpler.

**Tier:** Enterprise
**Auth:** API key (provisioned) / Python SDK
**Last researched:** 2026-06-17

## Use cases

- Retrieve the cargo (commodity, grade, quantity in tonnes), route, and load/discharge for a specific tanker, including the full cargo history of any tanker >5,000 dwt back to 2016.
- Per-vessel and voyage-level enriched cargo + waypoint events (canal usage, ship-to-ship) via the VoyagesSearchEnriched endpoint.
- Build freight-revenue and arbitrage models combining cargo movements with freight pricing across 90,000+ active routes.

## Pricing

- **Free tier:** None (book-a-demo only).
- **Paid tiers:** Not publicly documented (quote-based; tiered by commodity/freight modules and API access).
- **Enterprise:** Contact sales. Delivery via RESTful Data API, Python SDK, or Excel Add-in.
- **Notes:** Coverage cited at 99% of global waterborne oil & gas movements; 500+ crude/condensate grades, 250+ CPP classifications, 25+ DPP grades, 1,500+ gas carriers; 12,800+ tankers / 320,000+ voyages per year. History from 2016.

## Authentication

API key provisioned under a Vortexa license; full API/SDK documentation (Vortexa Docs) is available to licensed users. The Python SDK wraps the same REST endpoints. No self-serve public key.

## Endpoints

- **Base URL:** Not publicly documented (REST API provisioned to licensed users; see Vortexa Docs).
- **Key endpoints:**
  - `CargoMovements` — specific cargo movements (product, grade, quantity) for vessels/flows.
  - `VoyagesSearchEnriched` — voyage waypoint + cargo events with full routing (incl. canal usage).
  - Freight pricing endpoints — benchmark $/ton spot prices on a cargo's actual route (Anywhere Freight Pricing).

## Example call

```bash
# Provisioned REST API. After licensing, Vortexa supplies the base URL and key;
# the Python SDK is the most common access path:
#   pip install vortexasdk
#   from vortexasdk import CargoMovements
# Contact Vortexa / see Vortexa Docs for endpoint specifications.
```

## Rate limits

Not publicly documented (governed by license / API plan).

## SDKs / Libraries

- **Official:** Vortexa Python SDK (`vortexasdk`); Excel Add-in. Vortexa Docs for API + SDK reference.
- **Community:** None notable.

## Documentation

- Main docs: https://www.vortexa.com/product/integrations/energy-data-api-integration
- API reference: https://www.vortexa.com/product/integrations (Vortexa Docs; licensed access)

## Notes

**Cross-listed:** Vortexa also appears in the catalog's `trade-flows` category (aggregate flow/market-intelligence angle). This entry is scoped to its per-vessel cargo capability — "what grade and quantity is this tanker carrying" — which is the direct analogue to the Kpler Cargo / Flows entry in this category. The two are the leading commodity-by-vessel providers for oil/gas; Vortexa is energy-focused (no dry bulk/containers), Kpler spans more commodity classes. Not a customs/BoL product and not a live AIS feed — it's modeled cargo intelligence built on AIS + analytics. See `apis/trade-flows/vortexa.md` for the flows-oriented entry.
