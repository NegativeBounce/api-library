# ImportGenius

Trade-intelligence platform serving U.S. and international customs bill-of-lading records at the shipment level, including product descriptions, shipper/consignee, and vessel.

**Tier:** Paid
**Auth:** Login (platform); API on higher-tier/custom plans
**Last researched:** 2026-06-17

## Use cases

- Look up the bill-of-lading records for shipments carried on a specific vessel into the U.S. and see the goods, shipper, and consignee.
- Supplier/competitor discovery — trace who a company buys from and the products and volumes moving.
- Automated monitoring with alerts when a watched company has new shipments.

## Pricing

- **Free tier:** None (free trial only).
- **Paid tiers:** Subscription plans billed monthly/annually (annual saves ~17%+). Public pricing page lists tiered monthly download caps; exact figures change — verify on the pricing page. International BoL (Asia, Europe, Latin America) is an add-on.
- **Enterprise:** Custom plans with 21+ country coverage and a dedicated research/data-science team; API access negotiated here.
- **Notes:** U.S. data updated daily. Plans differentiate primarily on download volume and country add-ons.

## Authentication

Web platform via account login. API access is offered on higher-tier/custom (Business/Enterprise) plans — credentials issued by ImportGenius; not a self-serve public key. Confirm API availability and auth scheme with their sales team.

## Endpoints

- **Base URL:** Not publicly documented (API provisioned on Business/Enterprise plans).
- **Key endpoints:** Not publicly documented. Core product is the web app with search, visualizations, and alerts.

## Example call

```bash
# No self-serve public API. API access is arranged on Business/Enterprise plans;
# endpoint specs and keys are provided by ImportGenius.
```

## Rate limits

Not publicly documented (tied to plan download caps and API contract).

## SDKs / Libraries

- **Official:** None published.
- **Community:** None notable.

## Documentation

- Main docs: https://www.importgenius.com/
- API reference: Not publicly documented (provided on qualifying plans).

## Notes

Nearly two decades in the U.S. BoL space; coverage spans U.S. CBP plus 12+ Latin American countries and others (Russia, Turkey, India, Sri Lanka, Ukraine, Vietnam, etc.). Vessel name appears on U.S. ocean BoL records, supporting "what did this ship carry" queries for covered lanes. This is historical/near-real-time trade intelligence, not a live manifest feed. Same shipment layer as Datamyne/Trademo/Volza — included for breadth of coverage and pricing comparison.
