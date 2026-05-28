# Airbus OneAtlas

Programmatic search, streaming, tasking, and ordering of Airbus optical satellite imagery (Pléiades Neo, Pléiades, SPOT) plus basemaps and elevation data.

**Tier:** Paid
**Auth:** API key exchanged for a bearer access token
**Last researched:** 2026-05-28

## Use cases

- Ordering 30cm Pléiades Neo, 50cm Pléiades, or 1.5m SPOT archive imagery over an AOI
- Tasking new acquisitions for time-sensitive monitoring (construction, agriculture, defense)
- Streaming a continuously updated "Living Library" optical archive into a GIS

## Pricing

- **Free tier:** 1-month free trial (sign-up on the OneAtlas portal); no full-resolution download
- **Paid tiers:** Subscription or pay-per-order; price depends on AOI, resolution, and tasking priority. Pléiades Neo requires a quotation step.
- **Enterprise:** Contract via Airbus Intelligence Customer Care (intelligence-customer-care@airbus.com)
- **Notes:** An active contract is required before generating an API key for pay-per-order tasking.

## Authentication

Obtain an API key from the OneAtlas portal (active contract required), then exchange it for a short-lived bearer access token via the OpenID Connect token endpoint. The token expires regularly and must be renewed. Pass the token as `Authorization: Bearer <access_token>` on every request.

## Endpoints

- **Base URL:** `https://search.foundation.api.oneatlas.airbus.com` (search/access); `https://authenticate.foundation.api.oneatlas.airbus.com` (auth)
- **Key endpoints:**
  - `GET /api/v2/opensearch` — search the archive (OpenSearch; filter by cloud cover, incidence angle, processing level)
  - `POST /api/v1/items` — order/stream items into the private MyData workspace
  - Pay-per-order tasking endpoints for Pléiades Neo, Pléiades & SPOT (price, quotation, order, track)

## Example call

```bash
curl -H "Authorization: Bearer $ACCESS_TOKEN" \
  -H "Cache-Control: no-cache" \
  "https://search.foundation.api.oneatlas.airbus.com/api/v2/opensearch?sortBy=incidenceAngle"
```

## Rate limits

Not publicly documented; governed by contract/subscription terms.

## SDKs / Libraries

- **Official:** OneAtlas Developer Portal guides; ArcGIS/QGIS plugins for archive search
- **Community:** Used by resellers (e.g., Geocento) via the OneAtlas API

## Documentation

- Main docs: https://www.geoapi-airbusds.com/
- API reference: https://www.geoapi-airbusds.com/api-catalog-v2/

## Notes

Pléiades Neo and Pléiades/SPOT ordering share access routes but differ in flow (Pléiades Neo needs a quotation). AOIs must be GeoJSON Polygons. "Living Library" filtering applies cloud cover <30% and incidence angle <40° criteria. Also offers Radar tasking/archive, WorldDEM, and basemap services under the same portal.
