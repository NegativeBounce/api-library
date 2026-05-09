# Genius Sports

Genius Sports is a major B2B sports technology provider supplying official-data odds feeds, end-to-end trading services, and risk management to 300+ sportsbooks under partnerships with leagues like the NFL, EPL, FIBA, and Serie A.

**Tier:** Enterprise
**Auth:** OAuth 2.0 / Client ID + secret (per commercial agreement)
**Last researched:** 2026-05-09

## Use cases

- Operating a regulated sportsbook that requires official league data and odds
- In-play and pre-match betting on major leagues with sub-second latency
- Outsourced trading and risk management via Genius Trading Services (GTS)
- Bet-builder, same-game-parlay, and BetVision interactive streaming integrations
- Ingesting third-party odds via the OddsFeed Ingestion API for consolidation

## Pricing

- **Free tier:** None.
- **Paid tiers:** Not publicly listed. Pricing is contract-based, scoped to specific feeds, leagues, and entitlement tiers.
- **Enterprise:** Standard model. Commercial agreement defines access rights, game feeds, sports leagues, and real-time entitlements.
- **Notes:** Total cost typically includes data licensing, integration / certification fees, and (optionally) GTS managed-trading fees. Expect a 6–12+ week onboarding involving certification.

## Authentication

OAuth 2.0 with client credentials (client ID + client secret) issued per commercial contract. Tokens returned in `access_token` and refreshed regularly. Treat credentials as production-grade secrets; rotate per Genius Sports policy.

## Endpoints

- **Base URL:** `https://explorer.api.geniussports.com/`
- **Key endpoints:**
  - OddsFeed Ingestion API — `/OddsFeed-Ingestion/v1/Production/...` (third-party odds ingestion for consolidation)
    - `POST /SourceFixtures` — create / update a fixture from your source
    - `POST /SourceMarkets` — create / update markets and prices (supports suspended state)
    - `DELETE /SourceMarkets` — invalidate a market
    - `POST /SourceHeartbeat` — optional heartbeat to keep BetVision in sync
  - Sportsbook Data & Odds APIs — full odds, fixtures, betbuilder, in-play markets (endpoints documented in customer Confluence portal)
  - Wallet integration endpoints — atomic, idempotent debit/credit/refund flows for bet placement

## Example call

```bash
# Authenticate
curl -X POST "https://api.geniussports.com/oauth/token" \
  -d "grant_type=client_credentials" \
  -d "client_id=$GS_CLIENT_ID" \
  -d "client_secret=$GS_CLIENT_SECRET"

# Use the returned access_token with subsequent requests
curl -H "Authorization: Bearer $GS_TOKEN" \
  "https://explorer.api.geniussports.com/OddsFeed-Ingestion/v1/Production/SourceFixtures"
```

## Rate limits

Per-customer SLA. Genius Sports advertises 99%+ market uptime on flagship feeds (e.g., 99%+ in-play uptime in 2024 EPL season). Real-time messages stream in the 240,000+ events/year range across 80 sport-specific apps; specific per-customer rate limits are negotiated.

## SDKs / Libraries

- **Official:** None publicly listed; integration is REST + Swagger contracts. Vendor provides sandbox credentials and integration support.
- **Community:** None notable.

## Documentation

- Main site: https://www.geniussports.com/
- Sportsbook (Bet) products: https://www.geniussports.com/bet/
- Data & Odds API overview: https://www.geniussports.com/bet/odds-feeds-api/
- OddsFeed Ingestion API (Swagger): https://swaggerui.api.geniussports.com/?url=https://explorer.api.geniussports.com/OddsFeed-Ingestion/v1/Production/swagger-latest.yaml
- Integration documentation portal: https://geniussports.atlassian.net/wiki/spaces/BID/

## Notes

- **Official-data partner status** is the commercial differentiator: Genius Sports holds exclusive or preferred official-data rights for several major leagues (NFL, Premier League, FIBA, Serie A), which means licensed competitors are required to source from Genius for those events.
- The OddsFeed Ingestion API runs in the opposite direction from typical odds APIs — it accepts odds **from** customers (e.g., other sportsbooks, content providers) for consolidation into Genius pipelines, rather than serving odds outward. Don't confuse it with the Sportsbook Data & Odds APIs.
- Suspended vs. invalidated markets: a suspended market temporarily blocks betting; an invalidated market is permanently closed (DELETE on `SourceMarkets`).
- Heartbeats (`SourceHeartbeat`) are optional but recommended to keep BetVision streaming overlays accurate.
- Wallet integration must be atomic, idempotent, and fully audited; certification involves simulating odds changes, latency events, and transaction spikes.
- Regulatory: production use requires a sportsbook license in each jurisdiction. Genius supports compliance but does not provide it.
- Major competitor in this space: Sportradar. The two routinely split league rights; the right partner depends on which leagues your sportsbook needs to cover.
