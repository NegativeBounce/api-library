# X (Twitter) API v2

The official X (formerly Twitter) developer API. As of February 2026, X moved to pay-per-use as the default model for new developers — replacing the old Free/Basic/Pro tiers. Useful for keyword and geofenced surveillance of Strait-relevant chatter.

**Tier:** Paid (pay-per-use); Enterprise above 2M reads/month
**Auth:** OAuth 2.0 (Bearer token) or OAuth 1.0a
**Last researched:** 2026-05-09

## Use cases

- Keyword tracking on "Strait of Malacca," "Selat Malaka," vessel names, port hashtags, in English and Bahasa Indonesia / Melayu.
- Geofenced search around Strait coordinates and port cities to surface in-region eyewitness posts.
- Filtered Stream for real-time OSINT alerting.
- Full-archive search (Enterprise tier) for historical incident reconstruction.
- Cross-validation against Dataminr / Factal alerts — confirm whether an event is showing up in raw social signal.

## Pricing

- **Free tier:** None for new developers as of Feb 2026.
- **Pay-per-use (default):** $0.005 per post read (capped at 2M reads/month); $0.015 per standard text/media write; $0.20 per write containing a URL.
- **Legacy Basic ($200/month) and Pro ($5,000/month):** Closed to new signups; existing subscribers retained.
- **Enterprise:** Required above 2M reads/month. Entry-level publicly cited at ~$42,000–$50,000+/month with custom terms.
- **Notes:** Pricing has been volatile since Musk acquisition; verify current rates before procurement.

## Authentication

OAuth 2.0 Bearer token (app-only) for read-only endpoints; OAuth 1.0a or OAuth 2.0 user-context for writes and protected resources.

## Endpoints

- **Base URL:** `https://api.x.com/2/`
- **Key endpoints:**
  - `GET /tweets/search/recent` — last 7 days (pay-per-use / legacy Basic+)
  - `GET /tweets/search/all` — full archive (Pro / Enterprise)
  - `GET /tweets/counts/recent` — query result counts
  - `POST /tweets/search/stream/rules` + `GET /tweets/search/stream` — Filtered Stream
  - `GET /users/by` — user lookups

## Example call

```bash
curl "https://api.x.com/2/tweets/search/recent?query=%22strait%20of%20malacca%22%20OR%20%22selat%20malaka%22&max_results=100&tweet.fields=geo,created_at,lang" \
  -H "Authorization: Bearer $X_BEARER"
```

## Rate limits

15-minute rolling windows on most endpoints. Per-app and per-user limits separate. HTTP 429 + `x-rate-limit-reset` header on breach. Pay-per-use users still face per-second concurrency caps.

## SDKs / Libraries

- **Official:** `twitter-api-python-sdk`, `twitter-api-typescript-sdk`.
- **Community:** `tweepy` (Python, widely used), `twit` (Node), many others.

## Documentation

- Developer hub: https://developer.x.com/
- Pricing: https://docs.x.com/x-api/getting-started/pricing
- API docs: https://docs.x.com/

## Notes

- **Pricing is unstable.** February 2026 changes broke many low-volume use cases; reverify before each procurement decision.
- For Strait-region chatter, geofenced filters are useful but Indonesia/Malaysia geo-tagged posts are a small fraction of total — keyword search is primary.
- Many third-party "Twitter alternative" data providers exist (TwitterAPI.io, BrightData, Apify) at lower cost but with platform-policy / ToS risk; not cataloged here.
