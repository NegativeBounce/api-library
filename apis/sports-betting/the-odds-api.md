# The Odds API

A widely-used freemium odds aggregator providing pre-match and in-play odds in JSON from 40+ global bookmakers via a simple credit-based REST API.

**Tier:** Freemium
**Auth:** API Key (query parameter)
**Last researched:** 2026-05-09

## Use cases

- Side projects, prototypes, and demos that need free real bookmaker odds
- Odds-comparison tools and affiliate sites covering US, UK, EU, and AU markets
- Backtesting models against historical odds snapshots back to 2020
- Spreadsheet-driven analysis via the Excel and Google Sheets add-ons

## Pricing

- **Free tier:** 500 credits/month, no credit card required.
- **Paid tiers:** Public on the website. Tiers shown previously include Rookie ($20/mo, 20K req), Champion ($49/mo, 90K req), Superstar ($99/mo), and higher. Verify current pricing at the-odds-api.com — listings have shifted occasionally.
- **Enterprise:** No formal SLA tier; high-volume users contact the team directly.
- **Notes:** Each request to `/odds` costs `markets × regions` credits, not 1 — a single NBA call across US + UK regions is 2 credits. Historical odds calls cost 10× the standard rate. Plan capacity is consumed faster than the raw "requests per month" number suggests.

## Authentication

Pass `apiKey={YOUR_KEY}` as a query parameter on every request. Keys are issued instantly via email after signup.

## Endpoints

- **Base URL:** `https://api.the-odds-api.com/v4/`
- **Key endpoints:**
  - `GET /sports` — list in-season sports (free, no quota cost)
  - `GET /sports/{sport}/odds` — pre-match and in-play odds for a sport
  - `GET /sports/{sport}/events` — upcoming and live events
  - `GET /sports/{sport}/events/{eventId}/odds` — odds for a specific event (supports player props)
  - `GET /sports/{sport}/scores` — live and recent scores/results
  - `GET /historical/sports/{sport}/odds` — historical odds snapshot (10× credits)

## Example call

```bash
# NFL moneyline odds from US bookmakers, American odds format
curl "https://api.the-odds-api.com/v4/sports/americanfootball_nfl/odds?\
regions=us&markets=h2h&oddsFormat=american&apiKey=$ODDS_API_KEY"
```

## Rate limits

Quota is enforced via the credit system rather than a per-second rate limit. Remaining quota is returned in `x-requests-remaining` and `x-requests-used` response headers. Empty responses (no events for a sport) do not consume credits.

## SDKs / Libraries

- **Official:** None.
- **Community:** Multiple Python and Node wrappers exist on GitHub; none are officially endorsed. Excel and Google Sheets add-ons are published by the vendor.

## Documentation

- Main site: https://the-odds-api.com/
- API guide (v4): https://the-odds-api.com/liveapi/guides/v4/
- List of bookmakers: https://the-odds-api.com/sports-odds-data/bookmaker-apis.html

## Notes

- Bookmaker coverage skews to **soft books** — DraftKings, FanDuel, BetMGM, Caesars, William Hill, Unibet, Bovada, etc. Sharp books (Pinnacle, Singbet, SBOBet) are not in the standard catalog, so this is not the right API for sharp benchmarking.
- Player props and alternate markets are available for selected US sports and bookmakers; coverage is expanding but uneven across leagues.
- Lay odds (exchange) for relevant Betfair/Matchbook markets are returned with the `h2h_lay` market key.
- Polling-only — no WebSocket or SSE streaming. Live odds latency is bounded by your polling cadence.
