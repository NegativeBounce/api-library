# Sportradar Odds Comparison

Sportradar's Odds Comparison API suite (Prematch, Live, Player Props, Futures, and Regular/Consensus) delivers normalized odds from leading global bookmakers in JSON or XML, paired with a 30-day developer trial.

**Tier:** Enterprise
**Auth:** API Key (developer portal) / contract-based for production
**Last researched:** 2026-05-09

## Use cases

- Media properties embedding live odds in matchup pages and live scoreboards
- Sportsbook operators benchmarking against consensus and competitor lines
- Player-prop content for fantasy and betting media (NFL, NBA, MLB, NHL, etc.)
- Futures / outright markets for season-long and tournament content
- Cross-checking odds against Sportradar's broader Sports API ecosystem (stats, schedules, play-by-play)

## Pricing

- **Free tier:** 30-day free trial covering the developer portal APIs, no purchase required.
- **Paid tiers:** Not publicly listed. Pricing scales by API surface (which Odds Comparison products), data refresh frequency, and contract volume.
- **Enterprise:** Standard model. Sportradar offers tiered packages and custom contracts; pricing is sales-led.
- **Notes:** Trial is intended for evaluation, not production. Pricing varies by sport package and coverage tier — refer to the Coverage Matrix to size what's needed.

## Authentication

Trial access uses an API key issued via the Sportradar developer portal. Production access uses contract-defined credentials (typically API key, sometimes OAuth 2.0 for partner integrations).

## Endpoints

- **Base URL:** `https://api.sportradar.com/`
- **Key endpoints (Odds Comparison product family):**
  - **Odds Comparison Regular API** — aggregated odds, pre-match outrights, consensus lines
  - **Odds Comparison Prematch API** — broad pre-match betting markets
  - **Odds Comparison Futures API** — futures (outright) markets for top US bookmakers
  - **Odds Comparison Live Odds API** — live odds with 15–30s refresh, optimized for media in-game integration
  - **Odds Comparison Player Props API** — player-prop markets across major leagues
  - Each product has its own endpoint family under the `/odds-comparison/...` path

## Example call

```bash
# Trial / production both use the same shape; access level set by the API key
curl "https://api.sportradar.com/odds-comparison-prematch/trial/v2/en/sports/sr:sport:2/sport_event_categories.json?api_key=$SR_KEY"
```

## Rate limits

Trial keys have lower rate limits than production keys; both are documented per-product in the developer portal. Live Odds API is updated every 15–30 seconds rather than via push, so rate limits favor scheduled polling.

## SDKs / Libraries

- **Official:** None universal; some product lines have language-specific samples in the developer portal.
- **Community:** Multiple unofficial Python and Node clients exist; verify version compatibility before depending on one.

## Documentation

- Developer portal: https://developer.sportradar.com/
- Odds APIs reference: https://developer.sportradar.com/odds/reference/intro
- Live Odds API changelog: https://developer.sportradar.com/sportradar-updates/changelog/odds-comparison-live-odds-api
- Coverage Matrix (interactive): linked from `developer.sportradar.com/getting-started/docs/get-started`
- Sports Data API portal: https://docs.sportradar.com/sports-data-api

## Notes

- **Five distinct Odds Comparison products** rather than a single odds API — choose by use case (Live for in-game, Player Props for prop content, Futures for outrights, Prematch for broad pre-match coverage, Regular for consensus). Pricing reflects the breakdown.
- Sportradar holds **official-data partnerships** with several major leagues (NBA, NHL, MLB historically), which gives it preferential or exclusive feeds in some cases. Confirm league rights for your target markets — the right enterprise data partner depends on which leagues you cover.
- US bookmaker coverage explicitly includes DraftKings, FanDuel, BetMGM, BetRivers, Caesars, Circa, and others.
- Live Odds API is **polling-based** (15–30s refresh) rather than push/streaming — explicitly designed for media in-game embedding rather than high-frequency trading.
- JSON and XML response formats. Decimal, American, and fractional odds formats supported.
- Sportradar's broader Sports API ecosystem (stats, schedules, play-by-play) integrates directly via shared IDs — useful when odds and stats need to be reconciled.
- Major competitor in this space: Genius Sports. Routine procurement decision involves comparing league-rights coverage, not just feature lists.
