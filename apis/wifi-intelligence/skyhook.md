# Skyhook Precision Location

Hybrid Wi-Fi + cellular + GPS positioning service backed by Skyhook's first-party network of 5+ billion Wi-Fi APs and 200+ million cell towers. A wholly-owned Qualcomm subsidiary.

**Tier:** Enterprise (custom commercial pricing; no public free tier)
**Auth:** API Key (XML-over-HTTPS for the cloud API; SDKs use a Skyhook key)
**Last researched:** 2026-05-09

## Use cases

- Wi-Fi-only or hybrid IoT device location (asset trackers, wearables) with no GPS
- Indoor positioning where GNSS is unavailable
- Server-to-server resolution from a passive Wi-Fi/cellular scan
- Network-side geolocation for fleets of LTE-M / NB-IoT devices

## Pricing

- **Free tier:** None publicly listed (developer trials may be granted on request).
- **Paid tiers:** Custom — quoted per integration, signal mix, and call volume.
- **Enterprise:** Standard route. Contact `support@skyhook.com` or skyhook.com sales.
- **Notes:** Skyhook was acquired by Qualcomm Technologies in 2022 (previously a Liberty Broadband subsidiary). No public price list as of last research.

## Authentication

Customer is issued a Skyhook Precision Location Key after contracting. Supplied as an HTTP/XML field by the Cloud API or as an SDK constructor argument.

## Endpoints

- **Base URL:** `https://global.skyhookwireless.com` (use DNS, never hardcoded IPs)
- **Key endpoints:**
  - `POST /wps2/location` — submit observed Wi-Fi APs + cell IDs + optional GPS, returns latitude/longitude/accuracy and (optionally) street address + time zone
  - `POST /wps2/submit` — contribute observations back to Skyhook
  - SDK / Embedded Client interfaces for on-device scan + submit

## Example call

```bash
curl -X POST "https://global.skyhookwireless.com/wps2/location" \
  -H "Content-Type: text/xml" \
  --data-binary @location_request.xml
```

```python
# Pseudo-Python — Skyhook ships customer-specific SDKs
import requests
xml_body = open('request.xml','rb').read()
r = requests.post(
    'https://global.skyhookwireless.com/wps2/location',
    data=xml_body,
    headers={'Content-Type': 'text/xml'})
print(r.text)
```

## Rate limits

Not publicly documented. Defined in customer contract / commercial terms.

## SDKs / Libraries

- **Official:** Embedded Client (C, for constrained devices), Lite Client, native SDKs (Android/iOS/Linux). Distribution is through customer engagements.
- **Community:** `skyhook` Electric Imp library; older third-party wrappers (mostly stale).

## Documentation

- Product page: https://www.skyhook.com/precision-location
- Developer overview (legacy IBM Cloud doc, still current at last research): https://github.com/ibm-cloud-docs/ghbsvc/blob/master/services/Skyhook-Location/index.md
- IoT integration overview: https://www.skyhook.com/blog/skyhooks-precision-location-integration-options-use-cases

## Notes

- Hybrid by design — same call accepts Wi-Fi, cellular, and IP. Cross-listing applies to `cellular-intelligence`.
- Older "Skyhook Wireless" branding still appears in documentation and DNS — same service.
- Detailed API docs and quotas are gated behind NDA/contract; public references are summary-level.
