# IMF PortWatch

Free, satellite-derived daily port-call and chokepoint-transit activity with preliminary trade-volume estimates for 2,065 ports and 28 major maritime chokepoints worldwide.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-06-11

## Use cases

- Establishing an authoritative, free baseline of daily port-call counts for "by location and region" intelligence reports.
- Monitoring transit volumes through the 28 tracked chokepoints (Hormuz, Bab-el-Mandeb, Suez, Malacca, Panama, Gibraltar, etc.) for war-risk and disruption reporting.
- Detecting anomalies in port/chokepoint throughput (e.g. dark activity, conflict-driven diversions, GPS jamming impacts) for security and insurance analysis.
- Backfilling historical port and trade-volume baselines to contextualize current congestion against trend.

## Pricing

- **Free tier:** Fully free and public. No account, no key.
- **Paid tiers:** None.
- **Enterprise:** N/A.
- **Notes:** Data produced by the IMF in collaboration with the UN Global Platform. No usage charge; standard ArcGIS service rate limits apply.

## Authentication

None. The datasets are exposed as public ArcGIS Feature Services (Esri GeoServices REST), plus downloadable CSV/KML/GeoJSON/GeoTIFF/PNG/Zip from the dataset pages. WMS and WFS endpoints are also published. No API key or login required.

## Endpoints

- **Base URL:** `https://services9.arcgis.com/weJ1QsnbMYJlCHdG/arcgis/rest/services`
- **Key endpoints:**
  - `GET /Daily_Trade_Data/FeatureServer/0/query` — daily port activity: port-call counts and import/export volume estimates per port.
  - `GET /Daily_Chokepoints_Data/FeatureServer/0/query` — daily chokepoint transit calls and transit trade-volume estimates for the 28 chokepoints.
  - Ports and Chokepoints reference layers expose `portid` / chokepoint IDs used to filter the daily queries.

## Example call

```bash
# Daily port activity for a single port (portid = PORT0), as JSON
curl "https://services9.arcgis.com/weJ1QsnbMYJlCHdG/arcgis/rest/services/Daily_Trade_Data/FeatureServer/0/query?where=portid%20%3D%20%27PORT0%27&outFields=*&maxRecordCountFactor=5&outSR=4326&f=json"
```

```python
import requests

base = "https://services9.arcgis.com/weJ1QsnbMYJlCHdG/arcgis/rest/services"
r = requests.get(
    f"{base}/Daily_Chokepoints_Data/FeatureServer/0/query",
    params={"where": "portid = 'chokepoint1'", "outFields": "*", "f": "json"},
)
features = r.json()["features"]
```

## Rate limits

Not separately published; governed by standard Esri ArcGIS Online hosted-feature-service limits. Use `where` filters and paginate (`resultOffset` / `resultRecordCount`) for large pulls. Data refreshes weekly (Tuesdays ~09:00 ET).

## SDKs / Libraries

- **Official:** None specific. Any ArcGIS REST or GeoServices-compatible client works (ArcGIS API for Python, Esri Leaflet, GDAL/OGR for WFS).
- **Community:** Standard HTTP clients; `arcgis` Python package.

## Documentation

- Main docs: https://portwatch.imf.org/pages/data-and-methodology
- API reference: https://portwatch.imf.org/ (dataset "About" pages expose the GeoService/WMS/WFS API links per layer)

## Notes

- Definition: a "port call" is a defined vessel arrival to berth; bunkering-only stops without trade are excluded to the best of their ability.
- Known data caveats published by IMF: GPS jamming/spoofing and vessels going dark around the Strait of Hormuz and conflict zones; periodic "blackout" days (e.g. Oct 12 2022, Feb 14 2023, Jan 9 2024); transponder shutdowns in sanctioned regions (Red Sea, Iran, Russia, Ukraine, Venezuela); and receiver-coverage changes over time affecting recorded calls (e.g. Gwangyang, Malacca Strait). Flag these in any report built on the data.
- Estimates derive from satellite AIS signals on ~90,000 ships via the UN Global Platform; treat trade volumes as preliminary estimates, not customs-grade figures.
- Best paired with a commercial AIS or congestion feed for real-time granularity; PortWatch is daily and trend-oriented, not minute-level.
