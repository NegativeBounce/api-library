# UKHO Admiralty MSI

UK Hydrographic Office Maritime Safety Information portal providing NAVAREA I and UK coastal navigation warnings, plus weekly Notices to Mariners (NMs). Authoritative for UK / North Sea / North Atlantic but not the Strait of Malacca.

**Tier:** Freemium
**Auth:** None for free downloads; sign-in for restricted content
**Last researched:** 2026-05-09

## Use cases

- Weekly UK Notices to Mariners (free PDF/digital download) — chart corrections, navigational changes, regulatory updates.
- NAVAREA I navigation warnings (UK + adjacent waters).
- UK Coastal warnings — relevant for vessels routing UK→Strait via Cape of Good Hope or Suez approaches.
- Reference standard for NM format and structure (other hydrographic offices model their NMs on UKHO).
- Free baseline alongside paid Admiralty Tidal API and ENC products.

## Pricing

- **Free tier:** Free public download of NMs and RNWs.
- **Paid tiers:** None for MSI portal directly. Adjacent products (Admiralty Tidal API, ENCs, AVCS) are paid.
- **Enterprise:** Not applicable to MSI.
- **Notes:** Sign-in required for some restricted content distributed to Admiralty Distributors.

## Authentication

None for the public portal. Optional sign-in for distributor-level content.

## Endpoints

- **MSI portal:** `https://msi.admiralty.co.uk/`
- **Notices to Mariners:** weekly PDF / NMWeb download.
- **Radio Navigational Warnings (RNW):** NAVAREA I + UK Coastal text feeds.
- **No documented REST API** for MSI; data is delivered as PDFs and HTML.

## Example call

```bash
# UKHO MSI does not publish a REST API. Workflow:
# 1. Browse weekly NMs at https://msi.admiralty.co.uk/
# 2. For programmatic NAVAREA / UK Coastal warnings, use SeaLagom (which aggregates UKHO MSI).
```

## Rate limits

Not formally published.

## SDKs / Libraries

- **Official:** None for MSI; commercial Admiralty digital products have separate SDKs.
- **Community:** Limited.

## Documentation

- MSI portal: https://msi.admiralty.co.uk/
- Maritime Safety Information overview: https://www.admiralty.co.uk/maritime-safety-information

## Notes

- For Strait-of-Malacca-specific data, UKHO MSI is **secondary** — covers NAVAREA I (UK / North Atlantic), not NAVAREA XI.
- Useful for UK-flagged vessels in transit and as a reference standard for NM format.
- For machine-readable global navigational-warning data, prefer NGA MSI or SeaLagom over scraping UKHO PDFs.
