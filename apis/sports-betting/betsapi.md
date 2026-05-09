# BetsAPI

A Bet365-centric data API offering pre-match and in-play feeds for Bet365, BWin, Betfair, Betway, and SboBet, sold as cheap modular packages with low entry cost.

**Tier:** Paid
**Auth:** API Token (query parameter)
**Last researched:** 2026-05-09

## Use cases

- Bet365-specific applications where Bet365 odds are the primary requirement
- Cheap entry into in-play odds streaming (3–5 second updates) for live-betting apps
- Multi-book products that need Betfair, BWin, Betway, or SboBet alongside Bet365
- Quick-and-dirty access to a popular European sportsbook without enterprise contracts

## Pricing

- **Free tier:** None.
- **Paid tiers:** Trial packages from $1 (one-day, max 3 trial purchases per package). Monthly plans gated **per bookmaker** — a Bet365 plan does not include access to BWin, Betfair, Betway, SboBet, or the generic Events API. Volume add-ons raise the hourly request cap from the default 3,600 toward 199,999 (and up to 799,999 with Volume Packages).
- **Enterprise:** "All APIs" combined plan exists; contact for pricing.
- **Notes:** Pricing is published on the BetsAPI site (`/mm/pricing_table`) and on RapidAPI. Default rate limit of 3,600 req/hr is generous for most apps without buying volume add-ons.

## Authentication

Pass `token={YOUR_TOKEN}` as a query parameter on every request.

## Endpoints

- **Base URL:** `https://api.b365api.com/` (load-balanced fallback: `https://api.betsapi.com/`)
- **Key endpoints:**
  - `GET /v1/bet365/upcoming` — upcoming Bet365 events
  - `GET /v1/bet365/inplay` — current in-play events
  - `GET /v1/bet365/event?FI={event_id}` — full odds/markets for an event
  - `GET /v1/bet365/result?event_id={id1,id2,...}` — settled results (up to 10 IDs per call)
  - `GET /v1/events/inplay` — generic in-play events feed (separate package)
  - Equivalent endpoints for `/bwin/`, `/betfair/`, `/betway/`, `/sbobet/`

## Example call

```bash
# Bet365 event detail
curl "https://api.b365api.com/v1/bet365/result?\
token=$BETSAPI_TOKEN&event_id=63543522"
```

## Rate limits

- Default: 3,600 requests per hour, per token, returned in `X-RateLimit-Limit`, `X-RateLimit-Remaining`, `X-RateLimit-Reset` headers.
- Volume Packages raise the cap to 199,999 req/hr, with higher Volume tiers up to 799,999 req/hr.
- In-play data refreshes every 3–5 seconds.

## SDKs / Libraries

- **Official:** None.
- **Community:** Various unofficial Python and Node clients exist on GitHub; none are widely endorsed.

## Documentation

- Main docs: https://betsapi.com/docs/
- Bet365 endpoints: https://betsapi.com/docs/bet365/
- Pricing tables: https://betsapi.com/docs/pricing.html and https://betsapi.com/mm/pricing_table

## Notes

- **Package-gated access** is the most important integration constraint: each bookmaker (Bet365, BWin, Betfair, Betway, SboBet) and the generic Events API are sold as separate packages. Plan accordingly when modeling costs across multiple books.
- All responses are JSON with a `success` key indicating success/failure.
- Bet365's own APIs are not officially public; BetsAPI is the de-facto path for Bet365-specific data, and is widely used in arbitrage and matched-betting tools that target the European market.
- Trial packages limited to 3 purchases per type prevent indefinite trial cycling.
- The load-balanced `api.betsapi.com` fallback is useful when `api.b365api.com` is rate-limited or unavailable; behavior is otherwise identical.
