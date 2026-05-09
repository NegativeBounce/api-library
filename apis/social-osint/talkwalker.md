# Talkwalker (Hootsuite)

Enterprise social-listening and media-intelligence platform with 30+ social platforms and 150M+ websites covered. Strong image-recognition / visual-listening differentiator. Owned by Hootsuite since 2024.

**Tier:** Enterprise
**Auth:** API Key (Bearer)
**Last researched:** 2026-05-09

## Use cases

- Real-time mentions tracking via the Streaming API for Strait-related keywords and entities.
- Historical search for incident reconstruction via the Search API.
- Image-recognition / visual-listening for surfacing photos of vessels, ports, or incidents (logo/scene detection).
- Multi-language coverage including Indonesian, Malay, Chinese, Thai.
- Combined social + news + broadcast + print monitoring (150M+ sources).

## Pricing

- **Free tier:** None.
- **Paid tiers:** None publicly listed.
- **Enterprise:** Custom-quoted; entry tier ~$9,000–$12,000/year publicly cited; large contracts substantially higher.
- **Notes:** Pricing is sales-led; complex integrations require dedicated engineering resources.

## Authentication

API key (Bearer token) issued post-contract via the Talkwalker developer portal.

## Endpoints

- **Pricing page:** `https://www.talkwalker.com/pricing`
- **Developer portal:** Customer-issued.
- **Surface areas:**
  - Streaming API — real-time collectors
  - Search API — historical query
  - Image-recognition API — logo / scene detection
  - Analytics endpoints

## Example call

```bash
# Illustrative — actual endpoints provisioned per Talkwalker contract.
curl -H "Authorization: Bearer $TALKWALKER_TOKEN" \
  "https://api.talkwalker.com/v1/search?query=%22strait+of+malacca%22&from=2026-05-02"
```

## Rate limits

Plan-dependent; not publicly documented.

## SDKs / Libraries

- **Official:** None broadly distributed.
- **Community:** Limited.

## Documentation

- Pricing / product: https://www.talkwalker.com/pricing
- Main site: https://www.talkwalker.com/

## Notes

- Image-recognition is a meaningful differentiator vs. Brandwatch/Meltwater for visual OSINT.
- Best fit when image / video evidence matters (e.g., users posting photos of vessel incidents).
- Coverage of Asian-language social platforms (Weibo, KakaoTalk public posts) is decent but not exhaustive.
