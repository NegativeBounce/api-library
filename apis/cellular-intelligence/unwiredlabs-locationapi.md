# Unwired Labs LocationAPI

Commercial geolocation API by Unwired Labs (the company behind OpenCelliD). Locates devices via cell towers, Wi-Fi, and IP — globally, indoors and outdoors. Marketed as "Location-as-a-Service".

**Tier:** Freemium / Paid
**Auth:** API Token (in JSON body)
**Last researched:** 2026-05-09

## Use cases

- IoT / asset tracking without GPS (battery-saver positioning)
- Drop-in replacement for Google Play Geolocation Services on Android
- Server-side geolocation from a passive cell+Wi-Fi scan submitted by edge devices
- Forensic / OSINT cell-tower lookups with deeper-than-CC-BY-SA dataset

## Pricing

- **Free tier:** Developer plan — limited daily/monthly requests, non-commercial use only, email support.
- **Paid tiers:** Business plan — "as low as $0.10 per device" (volume-based). Scale to millions of requests; custom SLA & contract terms.
- **Enterprise:** Custom contracts including dedicated regional endpoints (us1, eu1, ap1), data partnership credits for fleets that contribute back data.
- **Notes:** Data partnership program — large fleets / popular apps can earn API credits in exchange for sharing anonymous data.

## Authentication

Sign up at my.unwiredlabs.com/trial to receive a developer token. Pass as `"token": "..."` in the JSON request body (NOT a header).

## Endpoints

- **Base URL:** `https://us1.unwiredlabs.com/v2` (also `eu1`, `ap1` regional)
- **Key endpoints:**
  - `POST /process` — submit `cells[]` (1–7), `wifi[]` (≥2 if included), optional `gps[]`, `radio`, `mcc`, `mnc`, `address` flag; returns `{status, lat, lon, accuracy, address}`
  - `POST /process` with `geolocation: 0` — contribute observations to grow the database (not charged)

## Example call

```bash
curl -X POST "https://us1.unwiredlabs.com/v2/process" \
  -H "Content-Type: application/json" \
  -d '{
    "token": "'"$UNWIRED_TOKEN"'",
    "radio": "gsm",
    "mcc": 310,
    "mnc": 410,
    "cells": [{"lac": 7033, "cid": 17811}],
    "wifi": [
      {"bssid": "00:17:c5:cd:ca:aa", "channel": 11, "frequency": 2412},
      {"bssid": "d8:97:ba:c2:f0:5a"}
    ],
    "address": 1
  }'
```

```python
import requests
r = requests.post("https://us1.unwiredlabs.com/v2/process", json={
    "token": "YOUR_TOKEN", "radio": "lte", "mcc": 310, "mnc": 410,
    "cells": [{"lac": 7033, "cid": 17811}],
    "wifi": [{"bssid": "00:17:c5:cd:ca:aa"}, {"bssid": "d8:97:ba:c2:f0:5a"}]
})
print(r.json())
```

## Rate limits

Developer plan: daily and monthly request caps (specific values not published). Business plan: contractually defined. First cell in `cells[]` must be the serving cell. Wi-Fi requires ≥2 BSSIDs to satisfy industry privacy standards.

## SDKs / Libraries

- **Official:** Android library (`location-library-docs`) — drop-in alternative to Google Play Geolocation; OpenAPI v3 spec + auto-generated clients (`locationapi-client-libraries`) for major languages.
- **Community:** RapidAPI listing; many third-party wrappers.

## Documentation

- Main docs: https://docs.unwiredlabs.com/
- API reference: https://unwiredlabs.com/api
- Pricing: https://unwiredlabs.com/pricing
- GitHub org: https://github.com/unwiredlabs

## Notes

- Same company runs OpenCelliD — LocationAPI is the commercial path with no CC-BY-SA attribution requirement and access to older / fuller data.
- Hybrid Wi-Fi+cellular service — cross-listing applies to `wifi-intelligence`.
- LocationIQ (geocoding) is a sister product, separate API.
- Coverage map: https://unwiredlabs.com/coverage
