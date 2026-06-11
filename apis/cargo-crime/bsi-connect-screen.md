# BSI Connect SCREEN

Global supply-chain risk intelligence platform providing cargo-theft incident data, country/commodity risk ratings, and threat analysis across transport modes.

**Tier:** Enterprise
**Auth:** Login / account (platform)
**Last researched:** 2026-06-11

> **Subscription intelligence platform, not a public self-serve API.** Delivered via the BSI Connect SCREEN platform and reports; programmatic access arranged per contract.

## Use cases

- Global cargo-crime intelligence and route/port risk assessment (BSI co-authors the annual cargo theft report with TT Club and TAPA EMEA).
- Country, commodity, and modal risk ratings to support secure routing and facility-siting decisions near ports and inland hubs.
- Trend and threat analysis (organized crime, insider theft, cyber-enabled/strategic theft, fictitious-pickup fraud).
- Supply-chain mapping, security auditing (C-TPAT/AEO/PIP), and compliance program support.

## Pricing

- **Free tier:** None (annual cargo theft reports are published free; the SCREEN platform is subscription).
- **Paid tiers:** Subscription to BSI Connect SCREEN — not publicly priced.
- **Enterprise:** Bespoke intelligence, auditing, advisory — contact BSI.
- **Notes:** Part of BSI Supply Chain Services & Solutions / BSI Consulting. Pricing not public.

## Authentication

Platform login / subscriber credentials provisioned per contract. No documented public self-serve API; integration arranged with BSI.

## Endpoints

- **Base URL:** No public API. BSI Connect SCREEN platform + reports.
- **Key surfaces:**
  - Incident intelligence database (global supply-chain crime).
  - Country/commodity risk ratings.
  - Analyst reports and dashboards.

## Example call

```bash
# No public self-serve API. Intelligence delivered via the BSI Connect SCREEN platform;
# integration arranged per contract with BSI.
```

## Rate limits

N/A (platform/reports). Per contract if a feed is provisioned.

## SDKs / Libraries

- **Official:** None publicly documented.
- **Community:** None.

## Documentation

- Main site: https://www.bsigroup.com/en-US/products-and-services/supply-chain/
- Cargo theft report: https://www.ttclub.com/news-and-resources/publications/article/bsi-and-tt-club-cargo-theft-report/

## Notes

- Strongest **global** (vs. US/Canada-only) cargo-crime intelligence source; complements Verisk CargoNet's North America focus.
- The free annual BSI Consulting / TT Club cargo theft report (latest 2025 edition, published Apr 2026) is a high-value open input even without a SCREEN subscription.
- Cross-reference: `cargo-crime/tt-club.md` and `cargo-crime/tapa-tis.md` (co-authors/partners), `cargo-crime/verisk-cargonet.md` (North America), and `geopolitical-risk/` for the broader country-risk layer.
- Confirm whether programmatic access is available for your build during sales scoping.
