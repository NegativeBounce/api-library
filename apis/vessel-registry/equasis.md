# Equasis

Free, EMSA-managed open database consolidating ship safety, ownership, management, classification, P&I and inspection data for the world merchant fleet (vessels over 100 GT).

**Tier:** Free
**Auth:** Account (free registration)
**Last researched:** 2026-06-11

## Use cases

- Resolving a vessel's registered owner, ISM/ship manager, classification society and P&I club by IMO number for due diligence and KYC.
- Cross-referencing flag, gross/deadweight tonnage, year built, type and status when only partial identifiers are known (name, call sign, MMSI).
- Pulling PSC inspection and deficiency history alongside ownership for risk scoring (insurance/war-risk personas).
- Free baseline ownership lookups before escalating to paid commercial providers for deeper beneficial-ownership chains.

## Pricing

- **Free tier:** Fully free. Requires a free account.
- **Paid tiers:** None.
- **Enterprise:** N/A.
- **Notes:** Non-profit, EU Commission + French maritime administration initiative; EMSA hosts the management unit. Ship/ownership data sourced from IHS (now S&P Global) under licence — usage restricted to internal business purposes, not commercial redistribution.

## Authentication

Free account registration at equasis.org. Access is via the web portal (and a mobile site). There is **no official public REST API** — automated access is not officially supported.

## Endpoints

- **Base URL:** `https://www.equasis.org/EquasisWeb/` (web portal; no documented API)
- **Key endpoints:**
  - Web search by IMO / name / call sign / MMSI / tonnage / flag.
  - Ship Info, Inspections, and Ship History tabs per vessel.
  - Company search (registered address, fleet list, aggregate inspection/deficiency synthesis).

## Example call

```bash
# No official API. Access is via authenticated web session at:
#   https://www.equasis.org/EquasisWeb/public/HomePage
# Community tooling (unofficial, HTML-scraping) example: rhinonix/equasis-cli
#   equasis-cli vessel --imo 9811000
```

## Rate limits

Not published. As a web portal there are no documented programmatic limits; unofficial scraping is subject to breakage when the site structure changes and to Equasis terms of use.

## SDKs / Libraries

- **Official:** None (no API).
- **Community:** `rhinonix/equasis-cli` (Python CLI that parses Ship Info, Inspections, Ship History tabs — 50+ data points; unofficial, may break on site changes).

## Documentation

- Main docs: https://www.equasis.org/EquasisWeb/public/About
- API reference: None (no official API).

## Notes

- **Cross-reference:** Equasis is also cataloged in `port-state-control` for its PSC inspection-regime angle. This entry covers the **vessel particulars + ownership** use case. Same source, different lens — not a duplicate file in the same folder.
- Underlying ship/ownership data is IHS/S&P Global; licence prohibits commercial product use — important for an app that resells intelligence. Confirm licensing before building Equasis-derived data into a paid product.
- ~85,000+ vessels; ~70% of data refreshed weekly (class/statutory certs, PSC, P&I, particulars).
- Five+ PSC regimes feed it (Paris MoU, Tokyo MoU, Indian Ocean MoU, USCG, Viña del Mar).
- For commercial-grade, redistributable ownership data, use MarineTraffic/Kpler, Lloyd's List Intelligence, or S&P Global instead.
