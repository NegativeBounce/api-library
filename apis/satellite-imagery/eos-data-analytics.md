# EOS Data Analytics

Cloud-based satellite imagery search, rendering, and analytics (vegetation indices, statistics) across Sentinel, Landsat, MODIS, CBERS, and commercial high-res sources, via the EOSDA API Connect REST API and LandViewer platform.

**Tier:** Freemium
**Auth:** API Key
**Last researched:** 2026-05-28

## Use cases

- Computing vegetation/spectral indices (NDVI, NDRE, NDWI, etc.) over a field or AOI
- Pulling rendered raster tiles (JPEG/PNG/GeoTIFF) of a chosen band combination
- Ordering high-resolution commercial imagery (up to 0.3–0.4m) without an enterprise contract

## Pricing

- **Free tier:** LandViewer web platform offers ~10 free medium-resolution images/day; Academic Outreach program grants free access to qualifying students/researchers/NGOs
- **Paid tiers:** Subscriptions unlock full platform/analytics; high-resolution imagery ordered separately starting ~$1.7/km²
- **Enterprise:** Custom analytics and high-load API plans via sales
- **Notes:** API Connect trial activated by contacting api.support@eosda.com (≈1 business day).

## Authentication

Register on the EOSDA API Connect developer dashboard to obtain a personal API key. Send the key with every request, either as the `api_key` query parameter or in request headers.

## Endpoints

- **Base URL:** `https://api-connect.eos.com/api/`
- **Key endpoints:**
  - `GET /render/...` — rendered raster image for a scene + index/band combo
  - Search API — find scenes across Sentinel, Landsat, CBERS-4, and others
  - Statistics API — zonal stats (avg, std dev, etc.) for indices over an AOI
  - Field Management — store/reuse AOI (field) IDs

## Example call

```bash
curl --location --request GET \
  "https://api-connect.eos.com/api/render/S2/36/U/XU/2016/5/2/0/NDVI/10/611/354?api_key=$EOSDA_API_KEY"
```

## Rate limits

Default 10 requests per minute per API key; higher limits negotiable for high-load applications. One request can cover an AOI up to 200 km² (20,000 ha).

## SDKs / Libraries

- **Official:** EOSDA API Connect docs + Postman collection; WMS integration for QGIS/ArcGIS
- **Community:** Not notable

## Documentation

- Main docs: https://doc.eos.com/
- API reference: https://doc.eos.com/docs/quickstart/

## Notes

EOSDA API Connect is the developer REST API; LandViewer is the web app over the same data. 17+ built-in indices plus custom band math. High-resolution commercial imagery (Beijing-3B, SuperView NEO, KOMPSAT, etc.) is ordered separately and not included in subscriptions.
