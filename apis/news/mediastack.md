# Mediastack

REST news API (apilayer / mediastack) covering 7,500+ global news sources in 13 languages, with both live and historical feeds. Affordable mid-tier alternative to NewsAPI.

**Tier:** Freemium
**Auth:** API Key (query parameter)
**Last researched:** 2026-05-09

## Use cases

- Multi-language news monitoring covering English, Bahasa Indonesia, Bahasa Melayu, Mandarin Chinese — useful for Strait-region coverage.
- Live news feed at a per-call cost lower than NewsAPI.
- Historical archive search (paid tiers) for incident reconstruction.
- Source filtering and country filtering (`country=id,my,sg,th`).
- Lightweight commercial use — Mediastack's Professional tier explicitly permits commercial deployment at $99/month.

## Pricing

- **Free:** $0/month, 100 calls/month, **delayed news**, all 13 languages, no commercial.
- **Standard:** $24.99/month ($22.99/mo annual), 10,000 calls, live news, historical, standard support.
- **Professional:** $99.99/month ($87.99/mo annual), 50,000 calls, **commercial use permitted**.
- **Business:** $249.99/month ($212.99/mo annual), 250,000 calls.
- **Enterprise:** Custom.
- **Notes:** Up to 15% off annual; overage charged at decreasing per-call rates. HTTPS only on paid tiers.

## Authentication

API key in `?access_key=...` query parameter.

## Endpoints

- **Base URL:** `http://api.mediastack.com/v1/` (HTTP) / `https://api.mediastack.com/v1/` (HTTPS, paid tiers).
- **Key endpoints:**
  - `GET /news` — live and historical news (filters: keywords, sources, categories, countries, languages, date)
  - `GET /sources` — source metadata

## Example call

```bash
# Articles mentioning Strait of Malacca in English and Indonesian, last 24h
curl "https://api.mediastack.com/v1/news?access_key=$MEDIASTACK_KEY&keywords=strait+of+malacca&languages=en,id&countries=id,my,sg&sort=published_desc&limit=100"
```

## Rate limits

Per-month call cap (100 → 250,000 by tier). Concurrency limits and rate per-second not strictly published.

## SDKs / Libraries

- **Official:** None.
- **Community:** Python, Node wrappers on GitHub.

## Documentation

- API docs: https://mediastack.com/documentation
- Pricing: https://mediastack.com/product

## Notes

- Owned/operated by apilayer — same provider as currencylayer, weatherstack, etc. Reliable infrastructure but support is best-effort below Business tier.
- Coverage of Bahasa Indonesia and Bahasa Melayu is decent but not exhaustive — supplement with local Indonesian/Malaysian sources scraped directly for high-stakes work.
- HTTPS on Free tier requires Standard plan or higher.
