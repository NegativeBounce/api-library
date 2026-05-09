# OFAC Sanctions List Service (SLS)

Free U.S. Treasury OFAC service providing the Specially Designated Nationals (SDN) List, Consolidated Sanctions List, and other official sanctions lists in machine-readable formats. Authoritative source for U.S. sanctions; replicated by every commercial sanctions vendor.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-09

## Use cases

- Authoritative SDN and Consolidated list ingestion for vessel / company / individual screening.
- Sanctions-related Maritime Advisories from OFAC — directly relevant to Strait-of-Malacca counterparty screening.
- Daily / on-update polling to keep an internal screening dataset fresh.
- Reference standard when cross-validating commercial sanctions feeds.
- Direct ingestion into KYC / AML / sanctions-screening pipelines.

## Pricing

- **Free tier:** Fully free; public-domain data.
- **Paid tiers:** None.
- **Enterprise:** Not applicable.
- **Notes:** Use is unrestricted. For higher-confidence change-detection across multiple jurisdictions, consider OpenSanctions or commercial vendors that consolidate OFAC + EU + UK + UN.

## Authentication

None. Files are public.

## Endpoints

- **SLS portal:** `https://sanctionslist.ofac.treas.gov/`
- **OFAC SLS info:** `https://ofac.treasury.gov/sanctions-list-service`
- **SDN List XML:** `https://sanctionslist.ofac.treas.gov/Home/SdnList` and direct file paths under `https://www.treasury.gov/ofac/downloads/`
- **Formats:** XML, CSV, fixed-field, delimited; advanced XML standard files available alongside legacy SDN.xml / consolidated.xml.
- **Search UI (web):** `https://sanctionssearch.ofac.treas.gov/`

## Example call

```bash
# Download the SDN List XML
curl -o sdn.xml "https://www.treasury.gov/ofac/downloads/sdn.xml"

# Download the Consolidated (non-SDN) Sanctions List XML
curl -o consolidated.xml "https://www.treasury.gov/ofac/downloads/consolidated/consolidated.xml"
```

## Rate limits

Not formally published. As a public file-server use, implement reasonable polling cadence (daily is typical) and respect HTTP cache headers.

## SDKs / Libraries

- **Official:** None — straight file downloads.
- **Community:** Many parsers across languages; `python-ofac` and similar.

## Documentation

- SLS overview: https://ofac.treasury.gov/sanctions-list-service
- File formats / FAQ: https://ofac.treasury.gov/faqs/topic/1641
- Advanced XML standard: https://ofac.treasury.gov/sdn-list-data-formats-data-schemas/

## Notes

- For Strait-of-Malacca specifically, the relevant OFAC content includes designations of Iranian shadow-fleet vessels and entities — increasingly common after 2024 enforcement actions.
- This is a list, not an "API" in the strict sense — but is the canonical input for everyone else's API.
- For an aggregated multi-jurisdiction view (US + EU + UK + UN + others), pair with OpenSanctions.
