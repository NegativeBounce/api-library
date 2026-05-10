# OpenCelliD

Largest open community database of cell tower locations (~50M+ contributors, ~10M+ unique cells, 2B+ measurements). CC-BY-SA 4.0 licensed. Run by Unwired Labs as a community project.

**Tier:** Freemium
**Auth:** API Access Token
**Last researched:** 2026-05-09

## Use cases

- Geolocate IoT/mobile devices by reported cell tower (no GPS)
- Mobile-operator coverage analysis from crowdsourced measurements
- Forensic cell-tower lookup by MCC/MNC/LAC/CID
- Building or augmenting an internal cell-tower DB from CC-BY-SA dumps

## Pricing

- **Free tier:** Free API key on registration. API access limited but generous for non-commercial / contributing users; bulk CSV download up to 2× per day per token, last 18 months of data.
- **Paid tiers:** None directly — OpenCelliD is community-funded. Higher-throughput / commercial / older-data needs are served by sister product Unwired Labs LocationAPI.
- **Enterprise:** Bulk CSV available via AWS Data Exchange (free); commercial use requires CC-BY-SA attribution unless a written exception is granted by Unwired Labs.
- **Notes:** Each `getInAreaSize` call counts as 2 API credits and is free of charge for contributing apps. Non-contributing commercial use is steered to LocationAPI.

## Authentication

Register at opencellid.org (email required) and retrieve an Access Token from the dashboard. Pass it as `?key=YOUR_TOKEN` on every API call.

## Endpoints

- **Base URL:** `https://opencellid.org`
- **Key endpoints:**
  - `GET /cell/get?key=...&mcc=...&mnc=...&lac=...&cellid=...&format=json` — single cell lookup
  - `GET /cell/getMeasures?key=...&mcc=...&mnc=...&lac=...&cellid=...` — measurements for a cell
  - `GET /cell/getInArea?key=...&BBOX=lat1,lon1,lat2,lon2&mcc=...&mnc=...` — cells in a bounding box
  - `GET /cell/getInAreaSize?key=...&BBOX=...&mcc=...&mnc=...` — count of cells in area (2 credits)
  - `POST /measure/uploadCsv` / `POST /measure/uploadJson` — contribute measurements

## Example call

```bash
curl "https://opencellid.org/cell/get?key=$OCID_TOKEN&mcc=262&mnc=2&lac=434&cellid=9200&format=json"
```

```python
import requests
r = requests.get("https://opencellid.org/cell/get", params={
    "key": "YOUR_TOKEN", "mcc": 262, "mnc": 2,
    "lac": 434, "cellid": 9200, "format": "json"})
print(r.json())
```

## Rate limits

API quotas are per-token and not publicly enumerated by exact number; geared for contributors. CSV dump downloads: 2× per token per day. Older / heavy commercial workloads: redirect to Unwired Labs LocationAPI.

## SDKs / Libraries

- **Official:** None.
- **Community:** `opencellid` (Python wrapper, PyPI); Tower Collector (Android collector); various OSINT/forensics scripts.

## Documentation

- Main docs / wiki: https://wiki.opencellid.org/wiki/API
- Database format: https://wiki.opencellid.org/wiki/Database_format
- Downloads page: https://opencellid.org/downloads.php
- Community forum: https://community.opencellid.org/
- AWS Data Exchange listing: https://aws.amazon.com/marketplace/pp/prodview-ljzfb55am2rla

## Notes

- License is CC-BY-SA 4.0 — commercial products must visibly credit OpenCelliD with a link, or negotiate an exception with Unwired Labs.
- CSV dumps cover only the last 18 months. The API itself returns older cells.
- "Changeable" flag distinguishes carrier-provided GPS positions (precise) from crowdsourced estimates (averaged).
- Sister project / commercial path: see `Unwired Labs LocationAPI` in this category.
