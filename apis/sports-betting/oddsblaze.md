# OddsBlaze

A speed-focused odds aggregator branded as "world's fastest odds data," with distinctive features including a same-game-parlay calculator, weighted consensus odds, and OLV/CLV tracking.

**Tier:** Paid
**Auth:** API Key (query parameter)
**Last researched:** 2026-05-09

## Use cases

- Same-game-parlay (SGP) pricing via the BlazeBuilder calculator
- Custom-weighted consensus odds for in-house pricing models
- Opening / closing line value (OLV / CLV) analysis and reporting
- Real-time SSE streaming for live-betting applications

## Pricing

- **Free tier:** None publicly listed. A trial may be available on request.
- **Paid tiers:** Real-time access starts at $249/month per public industry comparisons. Tiered plans scale on book coverage and feature access.
- **Enterprise:** Custom contracts for high-volume / SGP-heavy use cases.
- **Notes:** Verify current numbers at oddsblaze.com — pricing comparisons published by competitors may not reflect the latest tiers.

## Authentication

API key passed as a `key=` query parameter on every request.

## Endpoints

- **Base URL:** `https://data.oddsblaze.com/v1/`
- **Key endpoints:**
  - `GET /odds/{sportsbook_id}_{league_id}.json` — odds for a book × league
  - SGP / BlazeBuilder calculator endpoints (covered in customer docs)
  - Consensus odds with custom weighting
  - Historical / OLV / CLV endpoints
  - SSE streaming for live odds and results

## Example call

```bash
curl "https://data.oddsblaze.com/v1/odds/betmgm_ncaaf.json?\
key=$ODDSBLAZE_KEY&market=Point%20Spread,Total%20Points&main=true&price=decimal"
```

## Rate limits

Not publicly documented in detail; tier-dependent. SSE streaming connections are favored over high-frequency polling.

## SDKs / Libraries

- **Official:** None publicly listed; integration is via plain REST + SSE.
- **Community:** None notable.

## Documentation

- API docs: https://docs.oddsblaze.com/api/odds/
- Main site: https://oddsblaze.com/sports-betting-api

## Notes

- **SGP calculator (BlazeBuilder)** is the standout differentiator — most aggregators do not expose structured SGP pricing because each sportsbook calculates SGPs with proprietary correlation engines internally. OddsBlaze approximates SGP pricing on its own.
- Supports seven odds formats: American, decimal, fractional, probability, Malaysian, Indonesian, Hong Kong.
- Real-time SSE streaming on paid tiers eliminates polling overhead for live-odds use cases.
- Game IDs follow a readable convention like `mlb:arizona_diamondbacks:philadelphia_phillies:2024-06-21`, which is useful for de-duplication and cross-source matching.
- Best fit for product teams that specifically need SGP pricing, line-movement analytics, or consensus weighting; less compelling than SportsGameOdds or The Odds API for vanilla moneyline/spread/total use.
