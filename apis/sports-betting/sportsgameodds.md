# SportsGameOdds

A developer-friendly odds aggregator with transparent pricing, REST + WebSocket feeds, and 80+ bookmakers including Pinnacle, designed for indie devs and growing platforms.

**Tier:** Freemium
**Auth:** API Key
**Last researched:** 2026-05-09

## Use cases

- Indie betting tools, fantasy apps, and odds-comparison sites that need affordable real-time data
- Player-prop and alternate-line modeling without enterprise pricing
- Backtesting against closing-line data for model validation
- Same-game-parlay-adjacent and futures-heavy products

## Pricing

- **Free tier:** Available for testing. Limited request volume; suitable for development, not production.
- **Paid tiers:** $99–$499/month publicly listed, billed monthly. 7-day free trial on paid plans.
- **Enterprise:** "AllStar" and custom plans for higher volume and streaming access; contact sales.
- **Notes:** Billing unit is "objects" — each item in a response counts (10 events returned = 10 objects), but pulling more bookmakers or more markets within a single event does **not** add cost. This is meaningfully different from credit-based providers that charge per market × region.

## Authentication

API key issued at signup. Passed via header `X-Api-Key: {key}` or as a query parameter (`apiKey=...`).

## Endpoints

- **Base URL:** `https://api.sportsgameodds.com/`
- **Key endpoints:**
  - `GET /v2/events` — events with odds (supports `includeAltLines=true`)
  - `GET /v2/leagues` — supported leagues
  - `GET /v2/sportsbooks` — supported books
  - `GET /v2/players` — player metadata for prop markets
  - Streaming: WebSocket push feed via Pusher (AllStar+ tiers only)

## Example call

```bash
curl -H "X-Api-Key: $SGO_KEY" \
  "https://api.sportsgameodds.com/v2/events?leagueID=NFL&includeAltLines=true"
```

```javascript
// Official Node SDK
import SportsGameOdds from 'sports-odds-api';
const client = new SportsGameOdds({ apiKeyParam: process.env.YOUR_API_KEY });
const page = await client.events.get();
```

## Rate limits

Tier-dependent. Higher tiers raise sync frequency; the free tier is limited to slower polling. Streaming endpoints are gated to AllStar/custom plans.

## SDKs / Libraries

- **Official:**
  - [`sports-odds-api`](https://www.npmjs.com/package/sports-odds-api) — Node/TypeScript SDK
  - [`SportsGameOdds/sports-odds-api-java`](https://github.com/SportsGameOdds/sports-odds-api-java) — Java SDK
- **Community:** Postman collections published by the vendor.

## Documentation

- Main site: https://sportsgameodds.com/
- API reference: https://sportsgameodds.apidocumentation.com/
- Pricing: https://sportsgameodds.com/pricing/

## Notes

- Coverage: 50+ leagues, 80+ sportsbooks, 3,000+ markets including player props, alt lines, futures, team props.
- Includes Pinnacle alongside DraftKings, FanDuel, BetMGM, and major European books — this is the cheap path to sharp + soft benchmarking.
- Live odds refresh in 30–60s on REST; sub-minute on the WebSocket push feed.
- Historical depth is shallower than enterprise providers (LSports, Sportradar). Closing-odds capture is included, which is sufficient for most CLV-style validation but not deep tick-level reconstruction.
- Streaming API is currently in beta; call patterns and response formats may change.
