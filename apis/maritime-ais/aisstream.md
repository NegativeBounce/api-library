# AISStream.io

Free WebSocket service streaming live AIS messages from a community-supported global receiver network. JSON output, simple API key auth, and bounding-box / MMSI / message-type filters.

**Tier:** Free
**Auth:** API Key
**Last researched:** 2026-05-09

## Use cases

- Real-time AIS feed for the Strait of Malacca via a tight bounding box (e.g., `[[-2.0, 99.0], [6.0, 105.5]]`).
- Continuous fleet monitoring filtered to a known list of MMSIs (max 50 per subscription).
- Lightweight prototyping or research projects that don't need an SLA or commercial license.
- Subscribing only to message types of interest (`PositionReport`, `ShipStaticData`, `SafetyBroadcastMessage`) to reduce bandwidth.
- Backup feed alongside paid providers (Datalastic, MarineTraffic) for cross-validation.

## Pricing

- **Free tier:** Free, no payment required. Sign up to provision an API key.
- **Paid tiers:** None.
- **Enterprise:** None — community service, no SLA, no support guarantee.
- **Notes:** Coverage and reliability depend on volunteer terrestrial receivers; the Strait of Malacca has reasonable coverage near major ports but expect gaps.

## Authentication

API key issued at signup. Provided in the WebSocket subscription message as the `APIKey` field. Subscription must be sent within 3 seconds of opening the connection.

## Endpoints

- **WebSocket URL:** `wss://stream.aisstream.io/v0/stream`
- **Subscription message** (JSON, one-shot per connection):
  - `APIKey` (required)
  - `BoundingBoxes` (required) — array of `[[lat1,lon1],[lat2,lon2]]` pairs
  - `FiltersShipMMSI` (optional, max 50)
  - `FilterMessageTypes` (optional)

## Example call

```javascript
const WebSocket = require('ws');
const socket = new WebSocket("wss://stream.aisstream.io/v0/stream");

socket.onopen = () => {
  socket.send(JSON.stringify({
    APIKey: process.env.AISSTREAM_KEY,
    BoundingBoxes: [[[-2.0, 99.0], [6.0, 105.5]]],  // Strait of Malacca
    FilterMessageTypes: ["PositionReport", "ShipStaticData"]
  }));
};

socket.onmessage = (event) => {
  const msg = JSON.parse(event.data);
  console.log(msg);
};
```

## Rate limits

Not publicly published. Connection drops if no subscription is sent within 3 seconds. Excessive reconnects or oversized subscriptions may be throttled.

## SDKs / Libraries

- **Official:** Pre-built example clients in Go, Python, JavaScript, Java; OpenAPI 3.0 model definitions available.
- **Community:** Various GitHub forks of the example clients.

## Documentation

- Main site: https://aisstream.io/
- Docs: https://aisstream.io/documentation

## Notes

- No SLA — community-supported and best-effort. Don't use as the *only* feed for safety-critical operations.
- AIS message types include accident/danger reports, SAR aircraft positions, and ship-to-ship binary messages — useful for incident-style filtering.
- Excellent fit as a "free baseline" feeding a fusion engine alongside paid providers.
