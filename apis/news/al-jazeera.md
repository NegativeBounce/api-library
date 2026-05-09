# Al Jazeera English

The English-language service of Qatar-based Al Jazeera Media Network, a 24-hour news channel founded in 2006 and headquartered in Doha — the first global English-language news channel headquartered in the Middle East. Free RSS feeds across all news, Middle East, economy, and other sections.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-09

## Use cases

- Middle East and North Africa breaking news from the leading pan-Arab broadcaster
- Tracking Israel/Palestine, Syria, Iran, Gulf states, and regional conflicts with on-the-ground reporting
- Building Arab-world news monitors with English-language editorial
- Augmenting Western news APIs with non-Western perspective on global affairs

## Pricing

- **Free tier:** All RSS feeds free; full website free to read with no paywall
- **Paid tiers:** None
- **Enterprise:** Content licensing and broadcast partnerships handled directly via Al Jazeera Media Network
- **Notes:** Operates as a public-interest broadcaster; not a metered or paywalled service

## Authentication

None.

## Endpoints

- **Base URL:** `https://www.aljazeera.com/`
- **Key endpoints (RSS):**
  - `GET /xml/rss/all.xml` — main all-news feed
  - `GET /xml/rss/middleeast.xml` — Middle East desk
  - `GET /xml/rss/economy.xml` — economy/business
  - Section feeds for Africa, Asia-Pacific, Americas, Europe, sports, science/tech, opinion, and program-specific feeds (Inside Story, etc.) follow the same `/xml/rss/{section}.xml` pattern

## Example call

```bash
# Main all-news feed
curl "https://www.aljazeera.com/xml/rss/all.xml"

# Middle East desk
curl "https://www.aljazeera.com/xml/rss/middleeast.xml"

# Economy/business
curl "https://www.aljazeera.com/xml/rss/economy.xml"
```

## Rate limits

Not publicly documented for RSS feeds.

## SDKs / Libraries

- **Official:** Free Al Jazeera English iOS and Android apps; live HD stream embeddable from website (no developer SDKs)
- **Community:** Standard RSS parsers; community RSS-bridge implementations exist for fuller article fetching

## Documentation

- Main site: https://www.aljazeera.com/
- About AJE: https://www.aljazeera.com/about-us
- Live stream: https://www.aljazeera.com/video/live

## Notes

Al Jazeera Media Network is **partially funded by the government of Qatar**; the broadcaster denies that this funding influences its editorial line. Al Jazeera English launched in 2006 as the network's first English service. Coverage is strongest on the Middle East, North Africa, and conflict zones; the network has won numerous awards for Arab Spring and Gaza coverage. Note for source-trust analysis: ownership and Qatari state funding should be flagged when comparing against other ME outlets. The network is also widely available on Pluto TV, Haystack News, and other OTT services. No public REST/JSON developer API documented; programmatic access is via RSS feeds and the embeddable live-stream player.
