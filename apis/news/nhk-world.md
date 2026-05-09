# NHK World-Japan

Japan's public broadcaster (Nippon Hōsō Kyōkai) international service, providing free English news (text, audio, video) on Japan and Asia-Pacific via RSS feeds, podcast feeds, and embeddable widgets.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-09

## Use cases

- Japan domestic news monitoring from a public-broadcaster source (analogue to BBC for the UK)
- Asia-Pacific breaking news and policy coverage from a Japanese editorial perspective
- Audio/podcast integration for English-language Japan briefings
- Building Japan-focused news readers, alerting tools, or accessibility/learning apps

## Pricing

- **Free tier:** All RSS feeds, podcast feeds, and embeds free
- **Paid tiers:** None
- **Enterprise:** Content licensing handled via NHK; contact NHK World directly
- **Notes:** As a public broadcaster funded by license fees in Japan, NHK World is deliberately free for international audiences

## Authentication

None.

## Endpoints

- **Base URL:** `https://www3.nhk.or.jp/nhkworld/`
- **Key endpoints:**
  - `GET /en/news/feed/v1/en/all/rss.xml` — main English news RSS
  - `GET /en/radionews/podcast/rss/english.xml` — Radio Japan English news podcast feed
  - Embed widgets and live-stream players linked from the NHK World homepage

## Example call

```bash
# English news RSS
curl "https://www3.nhk.or.jp/nhkworld/en/news/feed/v1/en/all/rss.xml"

# English radio news podcast
curl "https://www3.nhk.or.jp/nhkworld/en/radionews/podcast/rss/english.xml"
```

## Rate limits

Not publicly documented.

## SDKs / Libraries

- **Official:** None — standard RSS / podcast (RSS 2.0 with iTunes namespace)
- **Community:** Any RSS parser

## Documentation

- Main site: https://www3.nhk.or.jp/nhkworld/

## Notes

NHK World-Japan publishes in 19 languages including English; this entry covers the English service. Coverage is strong on Japan, the Korean peninsula, and Asia-Pacific affairs. Audio podcast feed is useful for hands-free briefings. Some article URLs in the RSS rotate to a "latest" page after a few weeks (older items may 404), so archive ingestion needs to fetch promptly. No REST/JSON API documented; RSS plus standard embed widgets are the programmatic surface.
