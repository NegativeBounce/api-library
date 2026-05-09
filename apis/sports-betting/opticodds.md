# OpticOdds

A B2B sports-betting data provider with real-time odds from 200+ sportsbooks, real-time SSE streaming, automated bet grading, and a v3 unified API used by sportsbooks, trading desks, and media operators.

**Tier:** Enterprise
**Auth:** API Key (header or query parameter)
**Last researched:** 2026-05-09

## Use cases

- Building or scaling a sportsbook with real-time odds from 200+ books behind one API
- Trading desks running quant models that need low-latency normalized data
- Automated bet grading and settlement (Won, Lost, Refunded, Half Won, Half Lost)
- Sharp-line monitoring, line-movement alerts, and full historical odds replay
- Media platforms embedding live odds with deep links into sportsbook apps

## Pricing

- **Free tier:** None. Trial access via sales contact only.
- **Paid tiers:** Not publicly listed. Pricing scales with book coverage, market depth, streaming entitlement, and SLA tier.
- **Enterprise:** Standard model. Custom contracts; integration in days, not months per vendor marketing.
- **Notes:** Trusted by 200+ companies including BetMGM as a partner / customer reference. Sales contact and demo required to obtain pricing.

## Authentication

API license key, passed either as a header or `key=` query parameter on every request.

## Endpoints

- **Base URL:** `https://api.opticodds.com/api/v3/`
- **Key endpoints:**
  - `GET /sports` — list supported sports and main markets (auth check works here)
  - `GET /leagues`, `GET /sportsbooks`, `GET /markets` — discovery
  - `GET /fixtures` — all fixtures (regardless of odds availability)
  - `GET /fixtures/active` — fixtures with current or historical odds
  - `GET /odds` — odds snapshot for fixtures × sportsbooks
  - SSE streaming endpoints — live odds and live results
  - `GET /injuries` — injury reports filtered by sport / league / team
  - `GET /players`, `GET /lineups` — player metadata, starting lineups
  - Bet grader endpoint — automatic settlement
  - Historical odds — every price change, lock, unlock, settlement

## Example call

```bash
# Check auth and pull supported sports
curl -H "X-Api-Key: $OPTIC_KEY" \
  "https://api.opticodds.com/api/v3/sports"

# Pull current odds for a fixture from 2 sportsbooks
curl -H "X-Api-Key: $OPTIC_KEY" \
  "https://api.opticodds.com/api/v3/odds?fixture_id=$FIX&sportsbook=draftkings,fanduel"
```

## Rate limits

Per 15-second window, resetting at the end of each window:

- Historical odds: 10 requests / 15s
- Streaming endpoints (new connection establishment): 250 requests / 15s
- All other endpoints: 2,500 requests / 15s

OpticOdds does **not** offer webhooks or WebSockets — live data is delivered via SSE (Server-Sent Events).

## SDKs / Libraries

- **Official:** None publicly listed. Vendor offers integration support directly.
- **Community:** None notable.

## Documentation

- Main site: https://opticodds.com/
- Developer docs: https://developer.opticodds.com/docs/odds-api-getting-started-guide
- API reference: https://developer.opticodds.com/reference/getting-started
- API FAQ: https://developer.opticodds.com/docs/api-faq

## Notes

- **Real-time player props and alternate markets across 200+ sportsbooks** is the headline differentiator vs. lighter aggregators that stop at moneyline/spread/total on a smaller book set.
- Six odds formats supported via the `odds_format` query parameter.
- Status / outage info: live status page linked at the bottom of opticodds.com.
- SSE preferred over polling for live odds — designed around event-driven consumption.
- Copilot is a separate OpticOdds product on top of the same data feed: it adds automated pricing, position management, and settlement. The Sports Betting API entry covers the raw feed only.
- Golf fixtures use a non-standard schema for round-prop fixtures (away_team_display = "Round 1/2/3/4", home_team_display = tournament name, no competitors). Worth handling explicitly if you cover golf.
- Auto-grader settlements: Won, Lost, Refunded, Half Won, Half Lost — useful for products that want to skip building a bet-settlement engine.
