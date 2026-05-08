# GPSwise

Real-time GPS jamming and spoofing detection map and API operated by SkAI Data Services, derived from ADS-B data via the OpenSky Network and Wingbits.

**Tier:** Freemium
**Auth:** API key (Pro tier; details on request)
**Last researched:** 2026-05-07

## Use cases

- Display global GPS jamming and spoofing zones on operational dashboards for airlines, dispatchers, and flight ops teams.
- Pull near-real-time interference polygons (H3 hex grid) into electronic flight bag (EFB) software, route-planning tools, or risk dashboards.
- Cross-check aircraft routes against active jamming/spoofing hotspots for go/no-go and alternates planning.
- Academic and humanitarian research into GNSS interference patterns (free Pro access for academics and NGOs on request).

## Pricing

- **Free tier:** Free public web map at gpswise.aero. Data is delayed by at least 24 hours. No API access.
- **Paid tiers:** GPSwise Pro — near-real-time data, full historical archive, Lufthansa Lido aero charts overlay, detailed flight info, and custom API endpoints. Pricing is not publicly listed; quoted on request via contact@skai-data-services.com.
- **Enterprise:** Custom API integrations and partnerships (e.g., integrations with Lufthansa Lido, Aviobook EFB, SkyPath GPS Interference Layer). Contact sales.
- **Notes:** GPSwise Pro is offered free to academic researchers and NGOs by application. Pricing tiers and rate limits for the API are not publicly published as of the last research date.

## Authentication

The free public map at gpswise.aero requires no authentication. API access is gated behind GPSwise Pro; SkAI provisions API keys to subscribers on request. Contact contact@skai-data-services.com or +41 76 814 05 91 to request API credentials and pricing.

## Endpoints

- **Base URL:** `https://gpswise.aero/` (web app); API base URL is provisioned per customer and not publicly documented.
- **Key endpoints:** Not publicly documented. GPS World reports that SkAI offers "custom API endpoints to integrate jamming and spoofing data into third-party products," with separate feeds for jamming hex polygons (H3 grid) and discrete spoofing events (real-time, per-aircraft).

## Example call

```bash
# No public example available. Pro API access is provisioned per customer.
# After receiving API credentials from SkAI, a typical request would resemble:
curl -H "Authorization: Bearer $GPSWISE_API_KEY" \
  "https://api.gpswise.aero/v1/interference?bbox=33,30,38,35&since=2026-05-07T00:00:00Z"
```

## Rate limits

Not publicly documented. Determined per customer contract.

## SDKs / Libraries

- **Official:** None published. Integration is via direct REST API consumption.
- **Community:** None known.

## Documentation

- Main docs: https://gpswise.aero/
- Pro tier and integration info: https://www.skai-data-services.com/blog/introducing-gpswise-pro
- API reference: Not publicly available; provided to Pro subscribers.

## Notes

- GPSwise is generally considered the leading public/commercial source for real-time GPS jamming and spoofing data, used by 30+ airlines and 20,000+ users.
- Underlying data comes from ADS-B (OpenSky Network + Wingbits since 2026), so coverage is determined by ADS-B receiver density. War zones with no flights or sparse receivers will appear as gaps.
- Spoofing detection has detection latency of seconds; jamming map updates every ~10 minutes (improved in 2026 from the prior 1-hour cadence).
- Operates on an H3 hex grid; spatial resolution was increased in 2026.
- The free tier is intentionally lagged by 24 hours to push commercial users to Pro.
- Spinoff of Zurich University of Applied Sciences (ZHAW), Switzerland.
- Strong fit for aviation use cases; less battle-tested for maritime, ground, or critical-infrastructure use cases (though those are within Dimetor/SkAI's NAVSentry partnership scope).
