# beaconDB

Open-source, community-run wireless geolocation service launched in 2024 as a successor to Mozilla Location Services (MLS). Aggregates crowdsourced Wi-Fi access point, cell tower, and Bluetooth observations into a public-domain dataset.

**Tier:** Free
**Auth:** None (clients self-identify via User-Agent)
**Last researched:** 2026-05-09

## Use cases

- Drop-in MLS replacement for geoclue/Linux distros, microG (Android), Firefox
- Free Wi-Fi BSSID → coordinates lookups for hobbyist or research workloads
- Privacy-preserving alternative to Google Geolocation for IoT/off-grid devices
- Contributing wardrived data (via NeoStumbler / Tower Collector) to a public-domain pool

## Pricing

- **Free tier:** Fully free, no API key, no published quotas. Donation/sponsorship is encouraged.
- **Paid tiers:** None.
- **Enterprise:** N/A.
- **Notes:** Project is community-run and self-described as experimental. Coverage is starting from scratch + the final MLS data dump, so density is uneven. Cell fallback comes from MLS' final dump; IP fallback is last resort.

## Authentication

No API key. Clients are expected to set a meaningful `User-Agent` header identifying the software (and ideally OS version) to help operators triage bad-actor traffic. A legacy `?key=<client_id>` query parameter is accepted in place of UA for compatibility with Ichnaea/MLS clients.

## Endpoints

- **Base URL:** `https://api.beacondb.net`
- **Key endpoints:**
  - `POST /v1/geolocate` — Mozilla Ichnaea-compatible geolocate endpoint; submit Wi-Fi APs + cell towers, get `{location: {lat, lng}, accuracy}`
  - `POST /v2/geosubmit` — submit observations (Wi-Fi/cell/GPS) to grow the database

## Example call

```bash
curl -X POST "https://api.beacondb.net/v1/geolocate" \
  -H "Content-Type: application/json" \
  -H "User-Agent: my-app/1.0 (linux; debian-12)" \
  -d '{
    "wifiAccessPoints": [
      {"macAddress":"01:23:45:67:89:AB","signalStrength":-65},
      {"macAddress":"01:23:45:67:89:AC","signalStrength":-72}
    ]
  }'
```

## Rate limits

Not publicly documented. Project relies on responsible UAs rather than hard quotas.

## SDKs / Libraries

- **Official:** None (request format mirrors Mozilla Ichnaea, so most MLS clients work unmodified).
- **Community:** NeoStumbler (Android collector), Tower Collector (Android), beacondb-unifiednlp (microG backend), geoclue 2.7.2+ (Linux).

## Documentation

- Main docs: https://beacondb.net/
- Source: https://github.com/beacondb/beacondb (also on Codeberg)
- Setup guide (Linux/geoclue): https://konstantintutsch.com/blog/beacondb-geolocation-on-linux-gnome/

## Notes

- Public-domain data dumps are planned but not yet shipped at last research; only the live API is fully operational.
- Obfuscation (to prevent reidentifying single devices) is partially in place; some data is still un-obfuscated.
- Compatible with the Mozilla Ichnaea wire format, so existing MLS-era code largely "just works".
- Cross-listed concerns: `cellular-intelligence`, `bluetooth-intelligence`.
