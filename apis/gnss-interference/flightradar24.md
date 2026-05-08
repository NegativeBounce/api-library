# Flightradar24

Flight tracking platform with a public GPS jamming/interference web map and a paid REST API exposing live and historical flight positions including ADS-B NIC values that can be used to derive interference zones.

**Tier:** Freemium
**Auth:** API token (Bearer)
**Last researched:** 2026-05-07

## Use cases

- Embed Flightradar24's public GPS jamming map (as iframe or screenshot) for end-user-facing situational awareness.
- Pull live or historical flight position data via the FR24 API and derive your own GPS interference heatmap from NIC values (FR24 itself does not expose jamming polygons via the API).
- Cross-reference specific flights with their navigation integrity over a route, e.g., for incident analysis.
- Build dashboards combining FR24 flight tracks with other datasets (weather, NOTAMs, GPSwise, etc.).

## Pricing

- **Free tier:** The public GPS jamming map at flightradar24.com/data/gps-jamming is free to view. The FR24 API has a sandbox environment for testing with no live credit consumption.
- **Paid tiers:** Three FR24 API plans (separate from the consumer Silver/Gold/Business subscriptions):
  - Explorer — $9/month, 30,000 credits
  - Essential — $99/month, 450,000 credits
  - Advanced — $900/month, 4,050,000 credits
- **Enterprise:** Custom plans available; contact FR24 sales.
- **Notes:** Each endpoint costs a different number of credits per call (a "credit" is the API's billing unit). Top-up credit packs are available if a plan's monthly allotment is exhausted. The Silver/Gold/Business consumer subscriptions do **not** include API access.

## Authentication

Generate an API token in the FR24 API portal at https://fr24api.flightradar24.com after subscribing to a plan. Pass the token in the `Authorization: Bearer <token>` header on each request. A separate sandbox token can be obtained for free for testing endpoints without spending credits.

## Endpoints

- **Base URL:** `https://fr24api.flightradar24.com/api/`
- **Key endpoints (selected, jamming-relevant):**
  - `GET /live/flight-positions/full` — live flight positions in a bounding box, including `nic` (Navigation Integrity Category) per flight when available
  - `GET /live/flight-positions/light` — slimmer live positions payload
  - `GET /historic/flight-positions/full` — historical positions for a time window with NIC values
  - `GET /flight-tracks` — full track for a specific flight ID (includes per-point NIC)
  - `GET /static/airports`, `GET /static/airlines` — metadata
- **GPS jamming map:** The map at https://www.flightradar24.com/data/gps-jamming is **not exposed as a documented public API endpoint**. Aggregated jamming polygon data is rendered client-side from FR24-internal tiles. To compute interference zones programmatically, query NIC values per flight and aggregate.

## Example call

```bash
# Live flight positions in a bounding box (north,west,south,east), including NIC
curl -H "Accept: application/json" \
     -H "Accept-Version: v1" \
     -H "Authorization: Bearer $FR24_API_TOKEN" \
  "https://fr24api.flightradar24.com/api/live/flight-positions/full?bounds=44,30,40,40"
```

```python
# Python (with the official fr24sdk)
from fr24sdk.client import Client

client = Client(api_token="...")
positions = client.live.flight_positions.full(bounds="44,30,40,40")
for p in positions:
    if p.nic is not None and p.nic < 7:  # poor navigation integrity
        print(p.callsign, p.lat, p.lon, p.nic)
```

## Rate limits

Per-plan monthly credit allotments (see Pricing). Per-second/per-minute throttle limits exist but are not specifically published; check the live FR24 API portal for current values.

## SDKs / Libraries

- **Official:** JavaScript SDK and Python SDK (both linked from the FR24 API portal docs).
- **Community:** Multiple unofficial Python wrappers exist on PyPI/GitHub; quality varies and they often scrape the consumer flightradar24.com endpoints rather than using the official fr24api. Prefer the official SDKs.

## Documentation

- Main docs: https://fr24api.flightradar24.com/docs
- API portal: https://fr24api.flightradar24.com/
- Public GPS jamming map (no API): https://www.flightradar24.com/data/gps-jamming
- Blog explainer on the jamming map: https://www.flightradar24.com/blog/inside-flightradar24/gps-jamming-map/

## Notes

- **The web GPS jamming map is not a documented API endpoint.** If you need ready-made jamming polygons, GPSwise (SkAI Data Services) is the better fit. Use FR24 if you want raw flight data with NIC values to build your own analysis.
- FR24 derives jamming/interference from ADS-B NIC values (similar methodology to GPSJAM and GPSwise). Their map is updated every 6 hours, with selectable 6-hour or 24-hour aggregation windows.
- FR24 uses MLAT (multilateration) to recover positions of aircraft that are GPS-jammed/spoofed — useful if you want to compare reported ADS-B positions against MLAT-derived "true" positions to detect spoofing.
- API access is **separate** from the consumer Flightradar24 subscription — you cannot use a Silver/Gold/Business subscription to access the API.
- "Doubled credits" promo seen for new sign-ups before 2025-11-30; verify on the live pricing page whether any current promo is in effect.
