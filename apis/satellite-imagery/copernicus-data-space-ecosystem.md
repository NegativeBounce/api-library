# Copernicus Data Space Ecosystem

ESA's official gateway to Sentinel mission data and Copernicus services, providing free programmatic access to Sentinel-1 (SAR), Sentinel-2 (10m optical), Sentinel-3, and Sentinel-5P imagery via STAC, OData, OpenSearch, openEO, and Sentinel Hub APIs.

**Tier:** Free (with optional paid Sentinel Hub tiers)
**Auth:** OAuth 2.0 access token (Keycloak)
**Last researched:** 2026-05-07

## Use cases

- Building near-real-time Sentinel-2 (10m optical) and Sentinel-1 (SAR, all-weather) monitoring pipelines for agriculture, forestry, flood mapping, or change detection.
- Free academic / research workflows that need reliable, well-documented Sentinel data with a 5-day revisit globally.
- Cloud-based processing of EO data via openEO without downloading scenes — submit a Python/R/JS workflow against the cloud-resident archive.
- STAC-based catalog search and tile streaming integrated into web maps.

## Pricing

- **Free tier:** All Sentinel mission data is free and open. Each general user account gets a rolling 30-day download quota of 12 TB; 10,000 free openEO credits per month; access to STAC, OData, OpenSearch, and a (rate-limited) Sentinel Hub free tier.
- **Paid tiers:** Sentinel Hub subscriptions on top of CDSE for higher throughput / commercial use — see the Sentinel Hub entry.
- **Enterprise:** Larger quotas available to Copernicus Services / Collaborative Ground Segment / International accounts (institutional, by application).
- **Notes:** Exceeding the 12 TB transfer quota throttles bandwidth to ~1 MB/s with a single concurrent connection until the rolling 30-day total drops back below quota.

## Authentication

OAuth 2.0 via Keycloak. Register a free account at `https://dataspace.copernicus.eu`, then exchange username/password for an access token (10 min expiry, refreshable). Token is sent as `Authorization: Bearer <token>`. For S3 byte-range access to the EO data buckets, generate S3 credentials (free, 12 TB/month quota with 20 MBps bandwidth).

## Endpoints

- **Base URL:** `https://catalogue.dataspace.copernicus.eu` (catalog) and `https://download.dataspace.copernicus.eu` (downloads).
- **Key endpoints:**
  - `GET /odata/v1/Products` — OData catalog query (filter by collection, geometry, sensing date, cloud cover).
  - `GET /resto/api/collections/Sentinel2/search.json` — OpenSearch / resto-style queries.
  - `GET /odata/v1/Products({id})/$value` — direct product download.
  - STAC API base: `https://stac.dataspace.copernicus.eu/v1/`.
  - openEO API base: `https://openeo.dataspace.copernicus.eu/openeo/1.2/`.
  - Sentinel Hub APIs (Process / Catalog / Statistical / Batch): `https://sh.dataspace.copernicus.eu/`.
  - Token endpoint: `https://identity.dataspace.copernicus.eu/auth/realms/CDSE/protocol/openid-connect/token`.

## Example call

```bash
# 1. Get an access token (replace USER/PASS)
TOKEN=$(curl -s -X POST "https://identity.dataspace.copernicus.eu/auth/realms/CDSE/protocol/openid-connect/token" \
  -d "client_id=cdse-public" \
  -d "username=$CDSE_USER" \
  -d "password=$CDSE_PASS" \
  -d "grant_type=password" | jq -r .access_token)

# 2. Search Sentinel-2 L2A scenes over a point in the last 7 days
curl -H "Authorization: Bearer $TOKEN" \
  "https://catalogue.dataspace.copernicus.eu/odata/v1/Products?\$filter=Collection/Name%20eq%20'SENTINEL-2'%20and%20OData.CSC.Intersects(area=geography'SRID=4326;POINT(2.349014%2048.864716)')%20and%20ContentDate/Start%20gt%202026-04-30T00:00:00.000Z&\$top=5"
```

```python
# Python via sentinelhub-py against CDSE
from sentinelhub import SHConfig, SentinelHubRequest, DataCollection, MimeType, BBox, CRS

config = SHConfig()
config.sh_client_id = "<oauth-client-id>"
config.sh_client_secret = "<oauth-client-secret>"
config.sh_token_url = "https://identity.dataspace.copernicus.eu/auth/realms/CDSE/protocol/openid-connect/token"
config.sh_base_url = "https://sh.dataspace.copernicus.eu"

req = SentinelHubRequest(
    evalscript='//VERSION=3\nfunction setup(){return {input:["B04","B03","B02"],output:{bands:3}}}\nfunction evaluatePixel(s){return [s.B04, s.B03, s.B02]}',
    input_data=[SentinelHubRequest.input_data(
        data_collection=DataCollection.SENTINEL2_L2A.define_from("s2l2a", service_url="https://sh.dataspace.copernicus.eu"),
        time_interval=("2026-04-15", "2026-05-06"),
    )],
    responses=[SentinelHubRequest.output_response("default", MimeType.PNG)],
    bbox=BBox((2.25, 48.80, 2.45, 48.92), CRS.WGS84),
    size=(1024, 1024),
    config=config,
)
img = req.get_data()[0]
```

## Rate limits

- **Catalog (OData / OpenSearch / STAC):** ~6,000 requests/hour per user.
- **Downloads (OData $value or S3):** subject to the rolling 30-day 12 TB transfer quota; throttled to ~1 MB/s if exceeded.
- **OpenSearch:** maximum 1,000 results per page, max offset 10,000.
- **openEO:** 10,000 free credits/month, max 2 concurrent batch jobs for general users.
- **Sentinel Hub on CDSE (free tier):** 30,000 processing units/month, ~300 PU/min.

## SDKs / Libraries

- **Official:** [`sentinelhub-py`](https://github.com/sentinel-hub/sentinelhub-py), [openEO Python client](https://open-eo.github.io/openeo-python-client/), [openEO R client](https://open-eo.github.io/openeo-r-client/).
- **Community:** `pystac-client` (STAC), `sentinelsat` (legacy, partial CDSE support), `eodag`, QGIS Sentinel Hub plugin.

## Documentation

- Main docs: https://documentation.dataspace.copernicus.eu/
- API reference: https://documentation.dataspace.copernicus.eu/APIs.html
- Quotas: https://documentation.dataspace.copernicus.eu/Quotas.html

## Notes

- Replaced the legacy Copernicus Open Access Hub (SciHub), which was retired end of October 2023.
- Sentinel-2 has a 5-day combined revisit at the equator, finer at higher latitudes; Sentinel-1 has 6 days with both A+B (Sentinel-1B is non-operational; current cadence varies). Latency to NRT product availability is typically ~3 hours for S1 NRT-3h products and ~4 hours for S2 L1C NRT.
- For commercial use beyond the free tier (especially high-volume Sentinel Hub processing), look at the Sentinel Hub paid plans entry.
- Collections include Sentinel-1/-2/-3/-5P/-6, Copernicus DEM, Copernicus Contributing Missions, Landsat (5/7/8/9), and SMOS.
