# Newscatcher

News and Web Search APIs with a credit-based pricing model and explicit support for "monitor slots" (saved searches that run on a schedule). Useful for ongoing surveillance of a small set of search terms.

**Tier:** Freemium
**Auth:** API Key (header)
**Last researched:** 2026-05-09

## Use cases

- Continuous monitoring of "Strait of Malacca," named vessels, and key entities via monitor slots that re-run searches every 6h or daily.
- News and web search across global sources, including local-language coverage.
- Historical archive search on Enterprise tier (full archive, deep search, exclusive datasets).
- Lite-mode searches when broad query coverage is needed (different credit cost).
- Pay-as-you-go individual tier for occasional ad-hoc queries.

## Pricing

- **Individual (Free):** Pay-as-you-go, 100 max results per search, 1 monitor slot.
- **Starter:** $50/month, 6,000 credits/month, up to 300 results, 5 monitor slots, daily monitoring.
- **Scale:** $500/month, 60,000 credits, 1,000 results, 10 monitor slots, monitoring every 6h.
- **Enterprise:** Custom credits, full archive, unlimited monitors, 6h frequency.
- **Notes:** "Base" mode = 10 credits/record; "Lite" = 100 credits/search. Unused credits roll over to next billing period.

## Authentication

API key issued at signup; sent in the `x-api-key` header.

## Endpoints

- **Base URL:** `https://v3-api.newscatcherapi.com/api/v3/` (Newscatcher v3)
- **Key endpoints:**
  - `GET /search` — query news articles
  - `GET /latest_headlines` — recent headlines per country/source
  - `GET /sources` — source metadata
  - **Monitors** — saved searches with scheduled execution

## Example call

```bash
curl "https://v3-api.newscatcherapi.com/api/v3/search?q=%22strait+of+malacca%22&lang=en,id,ms&from=2026-05-02&page_size=100" \
  -H "x-api-key: $NEWSCATCHER_KEY"
```

## Rate limits

Tied to credits and concurrent connection count. Individual tier = 1 connection; Enterprise = 4+.

## SDKs / Libraries

- **Official:** Python (`newscatcher`), Node, Go wrappers.
- **Community:** Various integrations.

## Documentation

- Main site: https://www.newscatcherapi.com/
- API docs: https://docs.newscatcherapi.com/
- Pricing: https://www.newscatcherapi.com/pricing

## Notes

- Strong differentiator is the "monitors" feature — purpose-built for ongoing surveillance use cases.
- Web Search API (separate product) extends beyond news to general web pages — useful for OSINT.
- Coverage of Asian languages (Indonesian, Malay, Chinese) is reasonable.
