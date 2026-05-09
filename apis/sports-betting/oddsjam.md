# OddsJam

A premium real-time odds aggregator pulling main, alternate, and player-prop markets from 100+ sportsbooks at sub-second latency, marketed to professional traders, syndicates, and proprietary sportsbook operations.

**Tier:** Paid
**Auth:** API Key
**Last researched:** 2026-05-09

## Use cases

- Real-time arbitrage and +EV detection across US and global sportsbooks
- High-frequency sports trading and market-making operations
- Player-prop and alternate-market models that require fast, complete data
- Powering proprietary sportsbook pricing engines and trading desks

## Pricing

- **Free tier:** None publicly available.
- **Paid tiers:** Not publicly listed. Industry estimates put entry pricing in the $500–$1,000+/month range, scaling significantly higher for full data feeds with player-prop and push-stream access.
- **Enterprise:** Custom plans with dedicated support, custom endpoints, and high request limits available on request.
- **Notes:** OddsJam also sells consumer betting tools (web app) at separate consumer-tier prices; this entry covers the developer Odds API only. Pricing requires a sales conversation.

## Authentication

API key issued after a sales conversation. Passed via header or query parameter; details depend on contract terms.

## Endpoints

- **Base URL:** Documented to API customers; not public.
- **Key endpoints (typical):**
  - Games / fixtures by league and sport
  - Real-time odds across moneyline, spread, total, alternate, and player-prop markets
  - Historical odds with line-movement timestamps
  - Injury reports, schedules, scores, rankings
  - Push stream of odds updates

## Example call

```python
# Community Python wrapper (oddsjam-api on PyPI)
from OddsJamClient import OddsJamClient
client = OddsJamClient(api_key="YOUR_API_KEY")
client.UseV2()
games = client.GetGames(league="ncaa", sport="football")
odds = client.GetOdds(sportsbook="DraftKings")
```

## Rate limits

Not publicly documented. The platform advertises infrastructure capable of processing 1M+ odds per second; per-customer limits are set by contract.

## SDKs / Libraries

- **Official:** None.
- **Community:**
  - [`oddsjam-api`](https://pypi.org/project/oddsjam-api/) — Python wrapper (V1 + V2 endpoints)
  - [`cooperbrandon1/oddsjam-api`](https://github.com/cooperbrandon1/oddsjam-api) — same package, source repo

## Documentation

- Odds API page: https://oddsjam.com/odds-api
- Consumer tools FAQ: https://oddsjam.com/faq

## Notes

- Differentiator vs. budget aggregators: real-time odds on **player props and alternate markets** across 100+ books, where most cheap APIs stop at moneyline/spread/total on a smaller bookmaker set.
- JSON or XML response formats. Push-stream available alongside REST polling for sub-second updates.
- Consumer-facing OddsJam tools (Arbitrage Finder, +EV Tool, Middle Bets) sit on top of the same data feed; the API is the underlying product.
- Suited for serious operators, not weekend projects — the price floor and the contact-sales sales motion both reflect that.
