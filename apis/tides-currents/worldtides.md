# WorldTides

Global tide prediction API providing tidal heights, extremes (highs/lows), tide stations, and vertical datums via a credit-based REST API. Covers the entire world ocean including the Strait of Malacca and adjacent ports.

**Tier:** Freemium
**Auth:** API Key (query parameter)
**Last researched:** 2026-05-09

## Use cases

- Tide-height forecasts at any lat/lon for vessel anchoring decisions in Singapore Strait, Port Klang, Belawan, Phuket, etc.
- High/low tide times for pilotage and channel-transit planning.
- Tide-station discovery within a radius (e.g., 50 km around a target anchorage).
- Vertical datums (chart datum, MSL, MLLW) for surveying and dredge ops.
- Tide-aware ETD/ETA refinement for tide-restricted ports.

## Pricing

- **Free tier:** 100 free credits on signup (no time limit).
- **Paid tiers:**
  - **Pay-as-you-go:** ~$1.99 per 1,000 credits (pre-paid).
  - **Subscriptions:** Starting from ~$0.99/month for low-volume use.
- **Enterprise:** Custom contracts available.
- **Notes:** Credits scale with data type — Heights = 1 credit per 7 days of half-hourly data; Extremes = 1 credit per 7 days; Stations = 1–3 credits depending on radius.

## Authentication

API key issued at registration. Passed as `?key=...` query parameter.

## Endpoints

- **Base URL:** `https://www.worldtides.info/api/v3`
- **Key endpoints (selected via boolean flags):**
  - `?heights` — tidal heights
  - `?extremes` — high/low tide times
  - `?stations` — nearby station list
  - `?datums` — vertical reference levels
  - `?plot` — visual graph

## Example call

```bash
# 7 days of half-hourly tide heights for the Port of Singapore
curl "https://www.worldtides.info/api/v3?heights&date=2026-05-09&days=7&lat=1.290&lon=103.851&step=1800&key=$WORLDTIDES_KEY"
```

## Rate limits

Not explicitly published. Throttling is enforced via the credit balance — you can't exceed your purchased capacity.

## SDKs / Libraries

- **Official:** None.
- **Community:** Home Assistant integration, several Python and JS wrappers.

## Documentation

- API docs: https://www.worldtides.info/apidocs
- Developer site: https://www.worldtides.info/developer

## Notes

- One of the most cost-effective global tide APIs — ~$2 buys 1,000 days of tide data at default resolution.
- For the Strait of Malacca specifically, station density is good (Singapore TG, Tanjung Pagar, Penang, Lumut, Belawan).
- For tidal *currents* (not just heights), prefer NOAA CO-OPS, Stormglass, or commercial oceanographic providers — WorldTides focuses on vertical tide.
