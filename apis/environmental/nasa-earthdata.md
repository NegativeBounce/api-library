# NASA EOSDIS Earthdata

Central gateway to NASA's 178+ petabytes of Earth observation data. Provides multiple APIs (CMR for metadata search, GIBS for tiles already in `satellite-imagery`, Giovanni for analysis, FIRMS for fires). Free; Earthdata Login required for some downloads.

**Tier:** Free
**Auth:** Earthdata Login (free) for downloads; some APIs anonymous
**Last researched:** 2026-05-09

## Use cases

- Ocean color, sea-surface temperature, chlorophyll-a, suspended-sediment data over the Strait of Malacca for environmental baseline.
- Active-fire data (FIRMS) for monitoring vegetation fires on Sumatra / Borneo — relevant for haze impact on Strait visibility (a recurring operational issue).
- Atmospheric data (aerosols, NO₂) for air-quality / emissions analysis.
- Cryosphere, hydrology, biosphere data layers for broader environmental context.
- Free baseline for Earth-observation programmes that don't justify Maxar / Planet pricing.

## Pricing

- **Free tier:** Fully free.
- **Paid tiers:** None.
- **Enterprise:** Not applicable.
- **Notes:** Earthdata Login is free; authorisation is a one-time signup. Use is unrestricted for non-commercial and many commercial purposes.

## Authentication

- **Earthdata Login** (https://urs.earthdata.nasa.gov/) — required for many DAAC downloads.
- Token-based access for newer cloud-native services.
- Some browsing endpoints (CMR search) are anonymous.

## Endpoints

- **Earthdata home:** `https://earthdata.nasa.gov/`
- **CMR (metadata search):** `https://cmr.earthdata.nasa.gov/search/`
- **FIRMS (fires):** `https://firms.modaps.eosdis.nasa.gov/`
- **GIBS (tiles):** `https://gibs.earthdata.nasa.gov/` (cataloged separately under `satellite-imagery`)
- **Giovanni (analysis):** `https://giovanni.gsfc.nasa.gov/`
- **Worldview (browse):** `https://worldview.earthdata.nasa.gov/`

## Example call

```bash
# CMR search for MODIS Aqua ocean color granules over the Strait of Malacca, last 7 days
curl "https://cmr.earthdata.nasa.gov/search/granules.json?short_name=MODISA_L2_OC&bounding_box=99,-2,105.5,6&temporal=2026-05-02T00:00:00Z,2026-05-09T00:00:00Z" \
  | jq '.feed.entry | length'
```

## Rate limits

CMR endpoints handle ~10–100 req/sec for typical use. DAAC downloads are gated by Earthdata Login throttling. Bulk users should use the Cumulus / cloud-native pipelines (ASF, PO.DAAC).

## SDKs / Libraries

- **Official:** `earthaccess` (Python, https://github.com/nsidc/earthaccess), `harmony-py`, OPeNDAP clients.
- **Community:** `pystac-client` for STAC catalogs; many domain-specific clients per DAAC.

## Documentation

- Main site: https://earthdata.nasa.gov/
- CMR API: https://cmr.earthdata.nasa.gov/search/site/docs/search/api.html
- FIRMS API: https://firms.modaps.eosdis.nasa.gov/api/
- Earthdata Forum: https://forum.earthdata.nasa.gov/

## Notes

- For Strait-of-Malacca environmental monitoring, the most relevant DAACs are PO.DAAC (ocean), OB.DAAC (ocean color / chlorophyll), and LAADS (atmosphere / aerosols / fires).
- FIRMS active-fire data is **highly relevant** for SE Asia haze monitoring — the trans-boundary haze episodes from Sumatran fires routinely affect Strait visibility and shipping safety.
- Use the `earthaccess` Python library for any non-trivial workflows — it handles Earthdata Login token refresh automatically.
- NASA GIBS (tile imagery) is cataloged separately in the Satellite Imagery category — same provider, different surface.
