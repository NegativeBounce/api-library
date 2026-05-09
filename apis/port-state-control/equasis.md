# Equasis

Free maritime safety information database aggregating vessel particulars, ownership, classification, P&I club, and port-state-control inspection data from major flag states, classification societies, and the Paris/Indian Ocean/Mediterranean MoUs. Co-managed by EMSA and France's Maritime Affairs.

**Tier:** Free
**Auth:** Account registration (free)
**Last researched:** 2026-05-09

## Use cases

- Free vessel-history lookup (PSC inspections, deficiencies, detentions) for ships transiting the Strait of Malacca.
- Cross-checking vessel particulars (IMO, flag, gross tonnage, ownership, manager, P&I club, classification society) against AIS-claimed identity.
- Verifying that a vessel matches its claimed certificates / class.
- Identifying high-risk operators by aggregating PSC detentions across MoU regions.
- Free baseline alongside paid commercial vessel-database providers (S&P Global, Lloyd's List Intelligence).

## Pricing

- **Free tier:** All ship and company searches free; account registration required.
- **Paid tiers:** None.
- **Enterprise:** Not applicable.
- **Notes:** Service is funded by EMSA and partners; not a commercial product.

## Authentication

Free account at equasis.org. Login required for ship / company search; HTTP form-based login (no public API).

## Endpoints

- **Public site:** `https://www.equasis.org/`
- **No documented public API.** Web interface only; data is intended for individual lookups, not bulk programmatic ingestion.
- **Surface areas (web UI):**
  - Ship search by IMO / name
  - Company search by IMO / name
  - PSC inspection history
  - Vessel particulars (class, flag, P&I, owner/manager, year built, GT/DWT)

## Example call

```bash
# Equasis does not publish a REST API. Workflow is:
# 1. Register at https://www.equasis.org/ to obtain login credentials.
# 2. Use the web UI for vessel lookup, or carefully scrape post-login.
# 3. Paris/Tokyo/Indian Ocean MoU sites provide more bulk-friendly data exports.
```

## Rate limits

Not formally published. Aggressive scraping is discouraged and likely to result in account suspension.

## SDKs / Libraries

- **Official:** None.
- **Community:** Several research / academic scrapers exist on GitHub; respect ToS.

## Documentation

- Main site: https://www.equasis.org/
- About / governance: https://www.equasis.org/EquasisWeb/public/About

## Notes

- Best free starting point for any ad-hoc vessel-history investigation.
- For programmatic / bulk consumption, prefer the underlying MoU data sources (Paris, Tokyo, Indian Ocean) or commercial vendors.
- For the Strait of Malacca specifically: Equasis aggregates Tokyo MoU PSC data, which covers Singapore, Malaysia, Indonesia, and Thailand — directly relevant to vessel risk-profiling.
