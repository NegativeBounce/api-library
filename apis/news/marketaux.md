# MarketAux

Financial-news API focused on stock-market, forex, and crypto news with built-in entity tagging and sentiment scoring. Useful for surfacing news around shipping companies, charterers, and insurers exposed to Strait-of-Malacca risk.

**Tier:** Freemium
**Auth:** API Key (query or header)
**Last researched:** 2026-05-09

## Use cases

- Stock-market news on listed shipping operators (e.g., Pacific International Lines parent, MISC Berhad, Yang Ming, Evergreen).
- Sentiment-tagged news on entities affected by Strait-of-Malacca disruptions (oil, container shipping, insurance).
- Free tier suitable for prototyping financial-news monitors.
- Country-filtered news for Indonesia, Malaysia, Singapore.
- Crypto / forex news adjacent to maritime trade-finance flows.

## Pricing

- **Free tier:** 100 requests/day, no credit card required, limited sentiment-tagging features.
- **Paid tiers:** Multiple tiers; "very reasonably priced" per public reviews. Exact prices on the pricing page.
- **Enterprise:** Custom.
- **Notes:** Pricing is an order of magnitude lower than NewsAPI for comparable volumes — good fit when financial-news angle is primary.

## Authentication

API token issued in account dashboard. Pass as `?api_token=...` query parameter.

## Endpoints

- **Base URL:** `https://api.marketaux.com/v1/`
- **Key endpoints:**
  - `GET /news/all` — all news with filters (symbols, countries, language, must_have_entities)
  - `GET /news/by-symbol` — news for a specific equity / crypto symbol
  - `GET /entity/search` — find tagged entities

## Example call

```bash
# News mentioning MISC Berhad (Malaysian shipping) tagged with sentiment
curl "https://api.marketaux.com/v1/news/all?symbols=MISC.KL&filter_entities=true&language=en&api_token=$MARKETAUX_TOKEN"
```

## Rate limits

100 req/day on free tier; higher tiers scale up. Specific per-second limits not strictly published.

## SDKs / Libraries

- **Official:** None broadly distributed.
- **Community:** Python and Node wrappers exist.

## Documentation

- API docs: https://www.marketaux.com/documentation
- Pricing: https://www.marketaux.com/pricing

## Notes

- More focused than NewsAPI / Mediastack — shines when the use case is "what is the market saying about my exposed counterparty?"
- Sentiment-tagging quality is workmanlike; cross-validate with manual review for high-stakes decisions.
