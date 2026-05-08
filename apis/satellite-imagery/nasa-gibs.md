# NASA GIBS

NASA's Global Imagery Browse Services delivers full-resolution, near-real-time satellite imagery as standards-based map tiles, with no API key or registration required.

**Tier:** Free
**Auth:** None (public, no key)
**Last researched:** 2026-05-07

## Use cases

- Embedding global daily MODIS/VIIRS true-color tiles into a web map for "where is the smoke/fire/storm right now" displays.
- Near-real-time natural hazard monitoring (wildfires, hurricanes, dust, floods) using LANCE-processed layers available within ~3 hours of overpass.
- Time-lapse / change visualization across decades of NASA Earth observation missions in client apps using Leaflet, OpenLayers, Cesium, MapLibre, or QGIS.

## Pricing

- **Free tier:** Fully free, no registration.
- **Paid tiers:** None.
- **Enterprise:** N/A.
- **Notes:** Bulk download (>1,000,000 tiles per 24 hours) requires coordination with the GIBS team.

## Authentication

No authentication. Endpoints are publicly accessible. NASA requests an attribution acknowledging GIBS / NASA EOSDIS in published work or applications using the imagery.

## Endpoints

- **Base URL:** `https://gibs.earthdata.nasa.gov`
- **Key endpoints:**
  - `GET /wmts/{projection}/best/{layer}/default/{time}/{TileMatrixSet}/{z}/{y}/{x}.{format}` — WMTS RESTful tile endpoint, also usable as a generic XYZ tile source.
  - `GET /wms/{projection}/best/wms.cgi` — OGC WMS endpoint (GetMap, GetCapabilities).
  - `GET /twms/{projection}/best/twms.cgi` — Tiled WMS variant.
  - Projections supported: `epsg4326` (geographic), `epsg3857` (Web Mercator), `epsg3413` (Arctic), `epsg3031` (Antarctic).

## Example call

```bash
# Fetch a single MODIS Terra true-color tile (Web Mercator, zoom 6)
curl -o tile.jpeg \
  "https://gibs.earthdata.nasa.gov/wmts/epsg3857/best/MODIS_Terra_CorrectedReflectance_TrueColor/default/2026-05-06/GoogleMapsCompatible_Level9/6/24/40.jpeg"
```

```python
# Python via OWSLib (WMS)
from owslib.wms import WebMapService
wms = WebMapService("https://gibs.earthdata.nasa.gov/wms/epsg4326/best/wms.cgi?", version="1.1.1")
img = wms.getmap(
    layers=["MODIS_Terra_CorrectedReflectance_TrueColor"],
    srs="epsg:4326",
    bbox=(-180, -90, 180, 90),
    size=(1200, 600),
    time="2026-05-06",
    format="image/png",
    transparent=True,
)
open("modis.png", "wb").write(img.read())
```

## Rate limits

Not formally published. Anything over 1,000,000 tile requests in 24 hours is classified as a "bulk download" and should be coordinated with the GIBS team via earthdata-support@nasa.gov.

## SDKs / Libraries

- **Official:** No client SDK — uses OGC standards. Reference clients and example integrations live in the [`nasa-gibs/gibs-web-examples`](https://github.com/nasa-gibs/gibs-web-examples) repo (Leaflet, OpenLayers, Cesium, MapLibre GL, Mapbox GL, Bing, Google Maps).
- **Community:** Any WMTS/WMS-compatible library (OWSLib, Leaflet, OpenLayers, MapLibre, QGIS, ArcGIS Pro).

## Documentation

- Main docs: https://nasa-gibs.github.io/gibs-api-docs/
- API reference: https://nasa-gibs.github.io/gibs-api-docs/access-basics/
- Available layers: https://nasa-gibs.github.io/gibs-api-docs/available-visualizations/

## Notes

- "Live" imagery here means near-real-time (NRT) layers processed by EOSDIS LANCE, typically available ~3–3.5 hours after satellite overpass. This is not commercial high-revisit tasking — for that, see Planet, BlackSky, Capella, or Vantor.
- 1,000+ visualization layers spanning MODIS (Terra/Aqua), VIIRS (Suomi NPP, NOAA-20/21), AIRS, MISR, OMPS, and many more.
- Imagery is pre-rendered as visualizations (tiles), not raw scientific products. For raw L1/L2 data, use NASA Earthdata / CMR.
- Geostationary layers (GOES, Himawari) are available at 10-minute intervals for some products.
- Time dimension is part of the URL/query — use `time=YYYY-MM-DD` (or sub-daily `YYYY-MM-DDTHH:MM:SSZ` for 10-min layers).
