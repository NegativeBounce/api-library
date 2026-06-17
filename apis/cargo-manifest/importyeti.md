# ImportYeti

Freemium U.S. customs bill-of-lading search tool built from CBP manifest data obtained via FOIA, with shipment records covering products, shippers/consignees, and vessel.

**Tier:** Freemium
**Auth:** Account (free); paid tiers for advanced features
**Last researched:** 2026-06-17

## Use cases

- Free lookup of U.S. ocean import bill-of-lading records to see what a company imported and on which vessel.
- Quick supplier/competitor sourcing checks without a paid trade-data subscription.
- Starting point before committing to a heavier paid platform (Datamyne, ImportGenius, Trademo).

## Pricing

- **Free tier:** Yes — free access to U.S. import/export BoL search (the core differentiator).
- **Paid tiers:** Paid plans add deeper research, decision-maker contacts, and AI outreach features. Exact prices not fixed publicly — see site.
- **Enterprise:** Not publicly documented.
- **Notes:** Data sourced via FOIA requests to U.S. CBP; the company has stated it requested all ~70,000,000 BoLs. Mexican data relies on third-party port authorities.

## Authentication

Free account sign-up for the web tool. No documented self-serve public API — access is the website UI. Treat any programmatic use as scraping unless ImportYeti confirms an API.

## Endpoints

- **Base URL:** Not publicly documented (no published API).
- **Key endpoints:** None published. Access is the web application.

## Example call

```bash
# No public API documented. Access is via the ImportYeti website search UI.
```

## Rate limits

Not publicly documented.

## SDKs / Libraries

- **Official:** None.
- **Community:** None notable.

## Documentation

- Main docs: https://www.importyeti.com/
- API reference: None published.

## Notes

Included as the free/entry-level option in this category — strongest value when you need occasional U.S. ocean BoL lookups (vessel name included) without a subscription. Limitations: U.S.-centric, no air/land, some shipments redacted for confidentiality, and consignee/supplier names can be incomplete. Not an API product — if you need programmatic access, use Trademo, JSONCargo, or a contracted feed from Datamyne/ImportGenius/Volza.
