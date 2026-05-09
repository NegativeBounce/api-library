# DraftKings

DraftKings is a US-licensed sportsbook and daily fantasy sports operator; no general-purpose public API is offered, so developers typically rely on the limited public Marketplace API and reverse-engineered internal endpoints.

**Tier:** Free
**Auth:** None (Marketplace API and unofficial endpoints are unauthenticated)
**Last researched:** 2026-05-09

## Use cases

- Pulling DFS contest, slate, and draftable-player data for lineup optimizers and DFS tools
- Reading DraftKings sportsbook event lists, markets, and live odds for personal odds-comparison projects
- Reading public Marketplace transaction data for NFT/collectibles analytics

## Pricing

- **Free tier:** Marketplace API and unofficial endpoints are publicly reachable at no cost.
- **Paid tiers:** None publicly documented.
- **Enterprise:** No public developer portal. Commercial data partnerships are negotiated directly with DraftKings.
- **Notes:** Pricing claims on third-party "DraftKings API" pages typically refer to aggregator services (OpticOdds, SportsDataIO, etc.) reselling DraftKings odds, not direct DraftKings access.

## Authentication

The public Marketplace Activity API and the unofficial sportsbook/DFS endpoints accept anonymous HTTP GET requests — no API key, OAuth, or session token is required. The DraftKings Terms of Use prohibit using bots, scrapers, or any automation against DraftKings endpoints, so any production use should be cleared with DraftKings legal first.

## Endpoints

- **Base URLs:**
  - Marketplace (officially public): `https://marketplace.draftkings.com/api/activity/{version}`
  - Sportsbook (unofficial): `https://sportsbook.draftkings.com/sites/US-DK/api/`
  - DFS / contests (unofficial): `https://api.draftkings.com/`
- **Key endpoints:**
  - `GET /sites/US-DK/sports/v1/sports` — list sports
  - `GET /lobby/getcontests?sport={code}` — list DFS contests for a sport
  - `GET /draftgroups/v1/draftgroups/{id}/draftables` — players, salaries, positions for a slate
  - `GET /contests/v1/contests/{id}` — full detail on a single contest
  - `GET https://marketplace.draftkings.com/api/activity/v1/transactions` — Marketplace transaction feed (NFTs/collectibles)

## Example call

```bash
# DFS slate / draftable players (unofficial)
curl "https://api.draftkings.com/draftgroups/v1/draftgroups/46589/draftables"

# Marketplace transactions (officially public)
curl "https://marketplace.draftkings.com/api/activity/v1/transactions"
```

## Rate limits

Not publicly documented. The unofficial endpoints have no published quota, and aggressive polling has historically resulted in IP-level rate limiting or blocking.

## SDKs / Libraries

- **Official:** None.
- **Community:**
  - [`jaebradley/draftkings_client`](https://github.com/jaebradley/draftkings_client) — Python client for DFS endpoints (Python 3.7+)
  - [`SeanDrum/Draft-Kings-API-Documentation`](https://github.com/SeanDrum/Draft-Kings-API-Documentation) — community-maintained reverse-engineered docs

## Documentation

- Marketplace Activity API (PDF): https://reignmakers.draftkings.com/_assets/web-assets/Marketplace%20Activity%20API.pdf
- Marketplace API announcement: https://dknetwork.draftkings.com/2022/11/11/draftkings-marketplace-public-api-is-live-now/
- Community DFS docs: https://github.com/SeanDrum/Draft-Kings-API-Documentation

## Notes

- DraftKings does not publish an official public sportsbook or DFS developer API. The Marketplace Activity API (launched November 2022) is the only officially-public interface and is limited to NFT/collectibles transaction data; it does not include sportsbook odds or DFS contests.
- The "unofficial" sportsbook and DFS endpoints (`api.draftkings.com`, `sportsbook.draftkings.com/sites/US-DK/api/`) are internal endpoints that DraftKings can change or lock down without notice. Using them in production carries schedule and ToS risk.
- DraftKings' Terms of Use explicitly prohibit bots, scraping, and automated data extraction against any DraftKings endpoint, including the Marketplace API. Read the ToS before building.
- For production sportsbook odds at DraftKings, use a licensed aggregator (OpticOdds, SportsDataIO, The Odds API, OddsJam, etc.) rather than hitting DraftKings directly.
- Geographic restriction: Marketplace is US/Canada only.
