# LSports OddService

LSports is a B2B sports data provider whose OddService feed delivers pre-match and in-play bookmaker odds across 100 sports and 100+ bookmakers, plus a derived consensus product (TRADE360).

**Tier:** Enterprise
**Auth:** API Key / OAuth (per commercial agreement)
**Last researched:** 2026-05-09

## Use cases

- B2B sportsbooks needing wide bookmaker coverage with modular feed selection
- Pre-match and in-play data for ~175,000 pre-match and ~95,000 in-play events per month
- eSports market coverage (2,500+ markets across all sports including eSports)
- Consolidated trading via TRADE360, where LSports computes a customized average from underlying books
- High-volume sites needing low-latency live odds in JSON, XML, or binary formats

## Pricing

- **Free tier:** None.
- **Paid tiers:** Not publicly listed. Modular packaging — customers pick which bookmakers, sports, regions, and feed types (odds, fixtures, livescore, statistics, settlement, results) they need.
- **Enterprise:** Standard model. Custom contract pricing scoped to feed selection and request volume.
- **Notes:** OddService = raw bookmaker lines. TRADE360 = customized average across configured books. The two are distinct products and priced separately.

## Authentication

API key or OAuth 2.0, depending on contract. Credentials provisioned during onboarding.

## Endpoints

- **Base URL:** Documented to API customers; not public.
- **Key endpoints (typical):**
  - Pre-match odds feeds across 100 sports and 100+ books
  - In-play odds feeds with low-latency updates
  - Fixtures, livescore, team and player statistics
  - Market settlement (resulting) and final results
  - eSports markets

## Example call

```bash
# Pseudocode — actual base URL, auth header style, and parameter shape
# are provided in the customer-only documentation
curl -H "X-Api-Key: $LSPORTS_KEY" \
  -H "Accept: application/json" \
  "https://api.lsports.eu/oddservice/v1/odds?sportId=6046&format=json"
```

## Rate limits

Not publicly documented. Per-customer SLA defined in contract; LSports markets the OddService feed as having "the lowest latency in the market" but does not publish hard numbers publicly.

## SDKs / Libraries

- **Official:** None publicly published; LSports provides integration support directly.
- **Community:** None notable.

## Documentation

- OddService product: https://www.lsports.eu/oddservice/
- Main site: https://www.lsports.eu/

## Notes

- **Modular feed selection** is the main commercial differentiator. Unlike enterprise providers that bundle "the firehose," LSports lets customers buy only the bookmakers, sports, and feed types they need — useful for vertical sportsbooks (e.g., eSports-only, Latin American books only).
- Format options of XML, JSON, and binary make LSports a good fit for legacy back-ends and high-throughput trading systems where binary parsers reduce overhead vs. JSON.
- TRADE360 differs from OddService: OddService surfaces the raw bookmaker lines, TRADE360 produces a single derived/averaged price tuned to operator settings. Choose based on whether your trading desk consumes raw lines or a pre-computed market view.
- Strong eSports coverage relative to most enterprise providers, where eSports is often a paid add-on or under-served.
- Often considered alongside Sportradar and Genius Sports for enterprise procurement; LSports tends to compete on price and modularity rather than league-rights exclusivity.
