# WiGLE

Crowd-sourced global database of wireless networks (Wi-Fi, cellular, Bluetooth) collected via wardriving since 2001 — currently 350M+ networks. Queryable by BSSID, SSID, geographic area, vendor OUI prefix, encryption, and more.

**Tier:** Freemium (commercial use requires paid license)
**Auth:** Encoded API Token (HTTP Basic Auth)
**Last researched:** 2026-05-09

## Use cases

- Wireless threat-actor / rogue-AP tracking by BSSID prefix or vendor OUI
- Site survey and security assessment of Wi-Fi networks in a target area
- Geolocating a known SSID/BSSID across the global wardriving dataset
- OSINT / forensic enrichment of captured wireless observations

## Pricing

- **Free tier:** Free account; daily query budget grows with proven contributions and "human" usage signals. New accounts start with very tight quotas (often only a handful of detail/network calls/day) until the user uploads real data and demonstrates non-bot behavior.
- **Paid tiers:** None published; commercial access is by negotiated commercial license only.
- **Enterprise:** Commercial license issues "special unthrottled access tokens" — pricing by use case (contact `WiGLE-admin@wigle.net`).
- **Notes:** Quotas reset daily at 00:00 US/Pacific. Multi-account quota-circumvention is grounds for ban. Non-commercial use is bound by the WiGLE EULA.

## Authentication

Register a free account at wigle.net, then visit the account page to retrieve an Encoded API Token. Use it as HTTP Basic Auth: `Authorization: Basic <encoded_token>`.

## Endpoints

- **Base URL:** `https://api.wigle.net`
- **Key endpoints:**
  - `GET /api/v2/network/search` — search the network DB by SSID, BSSID/netid, geographic box, channel, last-update timestamp, encryption, etc.
  - `GET /api/v2/network/detail` — detail on a specific BSSID (most rate-limited endpoint)
  - `GET /api/v2/network/geocode` — text address → bounding box for use with search
  - `GET /api/v2/profile/user` — current user / quota info
  - `POST /api/v2/file/upload` — upload wardriving data (CSV)

## Example call

```bash
curl -G "https://api.wigle.net/api/v2/network/search" \
  -H "Authorization: Basic $WIGLE_ENCODED_TOKEN" \
  --data-urlencode "ssid=corp-guest" \
  --data-urlencode "latrange1=37.70" --data-urlencode "latrange2=37.80" \
  --data-urlencode "longrange1=-122.50" --data-urlencode "longrange2=-122.40"
```

## Rate limits

Sliding daily limits per account. New accounts: typically only ~5–10 detail calls/day and modestly more search calls/day. Limits scale up automatically as the user uploads valid data and shows organic browsing patterns. 429 returned on overrun. No public hard number; commercial license removes throttling.

## SDKs / Libraries

- **Official:** None.
- **Community:** `wiglr` (R), `wigle_api` (Ruby), assorted Python scripts (e.g., `jbjulia/wigle`, `wytshadow/wigleQuery`), Synapse `synapse-wigle` Power-Up by Vertex Project.

## Documentation

- Main docs: https://api.wigle.net/
- Interactive Swagger: https://api.wigle.net/swagger
- CSV upload format: https://api.wigle.net/csvFormat.html
- FAQ / quota policy: https://wigle.net/faq

## Notes

- Database includes Wi-Fi, cellular cell IDs, **and** Bluetooth observations — cross-listings apply to `cellular-intelligence` and `bluetooth-intelligence`.
- WiGLE explicitly does not allow data harvesting; aggressive scraping leads to account disablement.
- Mobile collection client (WiGLE WiFi Wardriving) is Android-only — Apple disallows wardriving apps in the App Store.
