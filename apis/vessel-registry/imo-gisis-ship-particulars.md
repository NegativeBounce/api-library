# IMO GISIS Ship & Company Particulars

The IMO's official Global Integrated Shipping Information System, providing authoritative ship identification (IMO numbers), company/registered-owner identification, and related particulars.

**Tier:** Free
**Auth:** IMO Web Account (free)
**Last researched:** 2026-06-11

## Use cases

- Verifying an IMO ship identification number and IMO company/registered-owner identification number against the authoritative source.
- Confirming registered owner / company identity for sanctions and KYC workflows where a primary-source citation is needed.
- Resolving flag, ship type and basic particulars from the body that manages the IMO numbering scheme.
- Backstopping commercial registry data with the official IMO record in intelligence reports.

## Pricing

- **Free tier:** Free with a registered IMO Web Account.
- **Paid tiers:** None.
- **Enterprise:** N/A.
- **Notes:** Operated by the International Maritime Organization. Some modules are public; others require the free account and specific access rights.

## Authentication

Free IMO Web Account (register at the IMO public site). Access is primarily via the GISIS web portal; certain modules expose downloadable datasets. No general-purpose public REST API.

## Endpoints

- **Base URL:** `https://gisis.imo.org/Public/`
- **Key endpoints:**
  - Ship and Company particulars modules (web query by IMO number / name / company).
  - Module-specific reports (varies by access rights).

## Example call

```bash
# Access is via the GISIS web portal with a free IMO Web Account:
#   https://gisis.imo.org/Public/
# No documented public REST API; queries are run through the web modules.
```

## Rate limits

Not published; web-portal access governed by IMO terms.

## SDKs / Libraries

- **Official:** None.
- **Community:** None notable.

## Documentation

- Main docs: https://gisis.imo.org/Public/
- API reference: None (web modules only).

## Notes

- **Cross-reference:** IMO GISIS is also cataloged in `maritime-safety-reports` for its casualty/incident modules. This entry covers the **ship & company particulars / IMO-number authority** angle. Same system, different module set — not a duplicate file in the same folder.
- The IMO number scheme is administered on IMO's behalf by S&P Global (formerly IHS Markit), which is why commercial S&P/Lloyd's data closely tracks GISIS.
- Best used as the authoritative cross-check, not as a bulk programmatic feed — there is no official API for high-volume automated pulls.
