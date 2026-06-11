# TT Club

Specialist mutual insurer for the international transport and logistics industry, publishing cargo-crime loss-prevention intelligence, annual cargo theft reports, and port-authority bulletins.

**Tier:** Free
**Auth:** None (public reports) / Member (insurance)
**Last researched:** 2026-06-11

> **Insurer + publisher, not a data API.** TT Club's value here is freely published loss-prevention intelligence and co-authored cargo theft reports; there is no programmatic feed.

## Use cases

- Loss-prevention intelligence on cargo theft, fraud (fictitious pickups, credit fraud), and port/terminal risk.
- Free annual cargo theft reports (co-authored with BSI Consulting and TAPA EMEA) and regional deep-dives (e.g. Benelux/Rotterdam-Antwerp, Italy, Middle East).
- Port-authority bulletins and StopLoss guidance for terminal and warehouse operators.
- Underwriting/claims context for transport-and-logistics risk near ports.

## Pricing

- **Free tier:** Free — reports, bulletins, and loss-prevention guidance are publicly available.
- **Paid tiers:** N/A for content (TT Club's core business is mutual insurance for members).
- **Enterprise:** Mutual insurance membership / risk-management services.
- **Notes:** Reports are free to download; some require a simple form.

## Authentication

None for public publications. No API.

## Endpoints

- **Base URL:** No API. Publications hub: ttclub.com.
- **Key surfaces:**
  - Annual cargo theft reports (with BSI/TAPA).
  - Regional freight-crime reports.
  - Loss-prevention / StopLoss articles and port-authority bulletins.

## Example call

```bash
# No API. Download reports and bulletins from
#   https://www.ttclub.com/news-and-resources/publications/
```

## Rate limits

N/A (publications).

## SDKs / Libraries

- **Official:** None.
- **Community:** None.

## Documentation

- Main site: https://www.ttclub.com/
- Cargo theft report: https://www.ttclub.com/news-and-resources/publications/article/bsi-consulting-and-tt-club-2025-cargo-theft-report

## Notes

- Best treated as a **free open-source intelligence input** rather than a feed: the annual reports and regional studies are analyst-grade and widely cited.
- TT Club's claims-data perspective complements incident-database providers (Verisk CargoNet, BSI SCREEN, TAPA TIS) by adding the insurer/loss-prevention angle.
- Cross-reference: `cargo-crime/bsi-connect-screen.md` and `cargo-crime/tapa-tis.md` (report co-authors), and `maritime-media/` for ongoing news-feed coverage of cargo crime.
