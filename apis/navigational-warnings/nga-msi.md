# NGA Maritime Safety Information (MSI)

U.S. National Geospatial-Intelligence Agency portal for global Maritime Safety Information — Anti-Shipping Activity Messages (ASAM), HYDROLANT/HYDROPAC/HYDROARC broadcast warnings, U.S. NAVAREA IV/XII messages, MODU positions, U.S. Coast Guard Local Notices to Mariners. Free public REST API.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-09

## Use cases

- ASAM (Anti-Shipping Activity Messages) — official U.S. government dataset of piracy / armed-robbery / suspicious approaches reports. Strait-of-Malacca incidents appear here.
- HYDROPAC broadcast warnings — covers western/central Pacific including waters approaching the Strait.
- Maritime Operational Threat Response (MOTR) advisories.
- MODU (Mobile Offshore Drilling Unit) position reports for offshore exploration risk.
- World Port Index, Distance Tables, Chart Catalog — useful reference data for maritime ops.

## Pricing

- **Free tier:** Fully free; no registration required.
- **Paid tiers:** None.
- **Enterprise:** Not applicable.
- **Notes:** Public-domain U.S. government data.

## Authentication

None.

## Endpoints

- **Public site:** `https://msi.nga.mil/`
- **REST API base:** `https://msi.nga.mil/api/`
- **Postman collection:** https://www.postman.com/api-evangelist/national-geospatial-intelligence-agency-nga/collection/ak1v6h5/
- **Key endpoints:**
  - `GET /api/publications/asam` — ASAM (Anti-Shipping Activity Messages)
  - `GET /api/publications/broadcast-warn` — broadcast warnings (HYDROPAC, etc.)
  - `GET /api/publications/modu` — MODU positions
  - `GET /api/publications/world-port-index` — port reference data
  - **Output formats:** JSON, GeoJSON; many endpoints accept `?status=active` / time filters.

## Example call

```bash
# ASAM incidents in/near the Strait of Malacca over the last 90 days
curl "https://msi.nga.mil/api/publications/asam?output=json&minOccurDate=2026-02-09" \
  | jq '.asam[] | select(.subreg | tostring | test("31|32|33"))'
```

## Rate limits

Not formally published. Reasonable use; the REST API handles modest traffic without aggressive throttling.

## SDKs / Libraries

- **Official:** None.
- **Community:** Various Python and Node scrapers; Postman collection serves as de-facto reference.

## Documentation

- Portal: https://msi.nga.mil/
- API surface (Postman docs): https://www.postman.com/api-evangelist/national-geospatial-intelligence-agency-nga/documentation/ak1v6h5/maritime-safety-information-rest-api
- About MSI: https://www.nga.mil/resources/Maritime_Safety_Products_and_Services.html

## Notes

- **ASAM is uniquely valuable** — U.S. government-curated dataset of shipping-incident reports with historical depth, not directly available elsewhere as JSON.
- For Strait of Malacca specifically, ASAM subregion codes around 30–33 (Indian Ocean / SE Asia approaches) are the relevant filters.
- Pair with ReCAAP and IMB-PRC for triangulation; ASAM tends to lag slightly but is structured and free.
- Endpoint paths have shifted historically — the Postman collection is the most reliable up-to-date reference.
