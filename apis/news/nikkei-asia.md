# Nikkei Asia

English-language Asia-Pacific business and political news from Nikkei Inc. (Japan's leading financial media group), with free RSS feeds and a subscription-based platform covering markets, tech, and policy across Asia.

**Tier:** Freemium
**Auth:** None (RSS); subscription login for full articles
**Last researched:** 2026-05-09

## Use cases

- Asia-Pacific business and economic news monitoring (Japan + greater Asia)
- Tracking Asian tech companies, semiconductor industry, and capital markets
- Building dashboards or alerting tools focused on Japan/Asia business
- Augmenting global financial APIs with Asia-region editorial perspective

## Pricing

- **Free tier:** RSS headlines free for personal/non-commercial use; site has metered articles for non-subscribers
- **Paid tiers:** Individual subscription (Nikkei Asia digital), with discounted student/group plans; pricing varies by region
- **Enterprise:** Group and corporate subscriptions; content syndication partnerships available — contact Nikkei
- **Notes:** RSS terms explicitly limit republication, copying, or redistribution. Subscriber rights are governed by the Nikkei Asia subscription agreement.

## Authentication

None for RSS. Full article access requires a Nikkei Asia subscription (web/app login).

## Endpoints

- **Base URL:** `https://asia.nikkei.com/`
- **Key endpoints:**
  - `GET /rss/feed/nar` — main Nikkei Asia review feed
  - Section feeds available via the regist subdomain (Trending, Business, Markets, Tech, Politics, Features) — see the official RSS index
  - RSS index: `https://info.asia.nikkei.com/rss`

## Example call

```bash
curl "https://asia.nikkei.com/rss/feed/nar"
```

## Rate limits

Not publicly documented for RSS.

## SDKs / Libraries

- **Official:** None
- **Community:** Standard RSS parsers; community RSS-bridge implementations exist for fuller article fetching

## Documentation

- RSS index: https://info.asia.nikkei.com/rss
- Site: https://asia.nikkei.com/

## Notes

Nikkei Inc. has been publishing financial news for 145+ years; Nikkei Asia is its English-language regional flagship (relaunched from "Nikkei Asian Review" in 2020). Strong on Asia-Pacific business and tech, including primary-source reporting on Japanese conglomerates, Taiwanese chipmakers, and ASEAN markets. RSS access is intentionally restrictive — non-commercial only without a subscriber agreement. No public REST/JSON API documented. Nikkei Inc. also owns the Financial Times.
