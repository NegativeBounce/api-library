# Yonhap News (English)

South Korea's official wire service (founded 1980) providing English-language RSS feeds, photos, video, and a paid B2B newswire covering Korean Peninsula politics, economy, K-pop/K-content, sports, and social affairs.

**Tier:** Freemium
**Auth:** None (RSS); contract for full wire service
**Last researched:** 2026-05-09

## Use cases

- South Korea breaking news monitoring (politics, economy, defense, North Korea relations)
- Tracking K-pop, K-drama, and Korean Wave (Hallyu) content for entertainment industry use cases
- Korean Peninsula geopolitics from Seoul's perspective (complementary to NK News for DPRK)
- Building Korea-focused news readers, alerting tools, or financial data products

## Pricing

- **Free tier:** RSS feed (`/RSS/news.xml`) free; English website free to read
- **Paid tiers:** B2B wire subscriptions for media outlets, government agencies, corporations, and internet portals — pricing on request
- **Enterprise:** Direct wire feed (3,000+ news items/day in articles, photos, graphics, video) via contract; multi-language services in EN/CN/JP/ES/AR/FR
- **Notes:** Yonhap is the only Korean wire service that works with non-Korean news agencies and has a content-exchange agreement with North Korea's KCNA

## Authentication

None for RSS. Wire service uses customer-provisioned credentials (FTP/API per contract).

## Endpoints

- **Base URL:** `https://en.yna.co.kr/`
- **Key endpoints:**
  - `GET /RSS/news.xml` — main English news RSS
  - Section sites: `/national`, `/business`, `/sports`, `/culture`, `/world` etc. on the same domain

## Example call

```bash
curl "https://en.yna.co.kr/RSS/news.xml"
```

## Rate limits

Not publicly documented for RSS.

## SDKs / Libraries

- **Official:** None for the public RSS surface
- **Community:** Standard RSS parsers

## Documentation

- English site: https://en.yna.co.kr/
- Mobile site: https://m-en.yna.co.kr/
- Korean main site: https://www.yna.co.kr/

## Notes

Established 1980 through merger of three existing news agencies. Operates in Korean, English, Chinese, Japanese, Spanish, Arabic, and French. RSS provides headlines + summaries with links to full articles on en.yna.co.kr (free to read). B2B wire customers receive faster, deeper feeds with photos, graphics, and video — that's a separate contractual product. No public REST/JSON API for the wire content; contract-only.
