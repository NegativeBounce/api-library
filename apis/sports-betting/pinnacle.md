# Pinnacle

Pinnacle Sports is a sharp, low-margin offshore sportsbook whose REST API exposes odds, fixtures, line checks, and bet placement; access is restricted to high-value bettors and commercial partners since July 23, 2025.

**Tier:** Enterprise
**Auth:** HTTP Basic (funded Pinnacle account credentials)
**Last researched:** 2026-05-09

## Use cases

- Pulling sharp benchmark closing lines for CLV (closing line value) analysis
- Programmatic bet placement against a sharp book for syndicate or quant use
- Reference pricing for arbitrage and +EV detection against soft US books
- Pre-game handicapping and academic sports-betting research projects

## Pricing

- **Free tier:** None. The API requires a funded Pinnacle account; access is no longer self-service.
- **Paid tiers:** Not publicly published. Access is now bespoke and negotiated.
- **Enterprise:** Commercial partnerships and high-volume access are negotiated by emailing `api@pinnacle.com` with a written use-case description.
- **Notes:** Affiliates historically maintained access by referring 5+ funded signups in a rolling 3-month window; that pathway may still apply for affiliate partners but is not advertised as the general route.

## Authentication

The API uses HTTP Basic authentication with the username and password of a funded Pinnacle account. All requests must use HTTPS (TLS 1.2 preferred, TLS 1.1 minimum). Access is locked to a maximum of 2 distinct IP addresses per client. Esports endpoints require additional authorization via `b2b@pinnacle.com`.

## Endpoints

- **Base URL:** `https://api.pinnacle.com/`
- **Key endpoints:**
  - `GET /v3/sports` — list sports (call once per 60 minutes max)
  - `GET /v1/leagues?sportId={id}` — leagues for a sport
  - `GET /v1/fixtures?sportId={id}` — non-settled events
  - `GET /v1/odds?sportId={id}` — odds snapshot or delta
  - `GET /v1/line` — price check before bet placement
  - `POST /v2/bets/place` — place a single bet
  - `POST /v2/bets/parlay` — place a parlay
  - `GET /v3/bets` — settled bet history
  - `GET /v1/inrunning` — live in-running events
  - `GET /v1/client/balance` — account balance

## Example call

```bash
# Get NBA fixtures (sportId 4)
curl -u "$PINNACLE_USER:$PINNACLE_PASS" \
  -H "Accept: application/json" \
  -H "Accept-Encoding: gzip" \
  -H "User-Agent: my-app/1.0" \
  "https://api.pinnacle.com/v1/fixtures?sportId=4"
```

## Rate limits

Strict and per-endpoint:

- `/v1/odds` and `/v1/fixtures`: 1 request per 2 minutes per endpoint per `sportId`. Use the `since` parameter for delta polling.
- `/v1/sports`: 1 request per 60 minutes.
- `/v1/line`: pre-bet price check only; do not loop.
- `/v1/odds` and `/v1/fixtures` snapshot calls are cached for 60 seconds; delta calls are not cached.
- Exceeding limits returns `429 Too Many Requests`.

## SDKs / Libraries

- **Official:** None.
- **Community:**
  - [`pinnacle.API`](https://rdrr.io/cran/pinnacle.API/) — R package on CRAN
  - [`pinnacleapi/pinnacleapi-documentation`](https://github.com/pinnacleapi/pinnacleapi-documentation) — official-style reference docs maintained on GitHub

## Documentation

- Lines API reference: https://pinnacleapi.github.io/linesapi
- Bets API reference: https://pinnacleapi.github.io/betsapi
- GitHub docs hub: https://github.com/pinnacleapi/pinnacleapi-documentation
- Pinnacle API access (overview / contact): https://www.pinnacle.com/en/api

## Notes

- **Public access closed since 2025-07-23.** General self-service access has been discontinued. Apply via `api@pinnacle.com` with a written use-case (commercial partnership, high-volume bettor, academic research, pregame handicapping). Decisions are case-by-case.
- The API includes real bet placement (`/v2/bets/place` and `/v2/bets/parlay`), not just odds reading. A funded account is mandatory and balance is required to wager.
- HTTP compression (`Accept-Encoding: gzip`) is strongly recommended; without a proper `User-Agent` header, compression may not work and performance suffers.
- Pinnacle is offshore — restricted or unavailable in the US, France, and several other jurisdictions. Treat the API as a reference data source if you operate in a restricted market.
- Pinnacle's lines are the de-facto sharp benchmark; many +EV and CLV tools are built around comparing soft US-book lines (DraftKings, FanDuel) to Pinnacle's no-vig consensus.
