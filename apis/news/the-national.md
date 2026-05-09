# The National (UAE)

Abu Dhabi government-owned English-language daily founded in 2008, providing UAE, Gulf, MENA, and global news with a UAE editorial perspective. Maintains an RSS feed index for programmatic consumption.

**Tier:** Free
**Auth:** None (RSS); registration required for some article features
**Last researched:** 2026-05-09

## Use cases

- UAE breaking news monitoring (Abu Dhabi, Dubai, federal government, expatriate affairs)
- Gulf and MENA coverage with English-language Emirati editorial perspective
- Tracking UAE business (DP World, Etihad, Emirates, ADNOC, Mubadala) in English
- Augmenting Saudi (Al Arabiya/Arab News) and Qatari (Al Jazeera) Gulf coverage with UAE perspective

## Pricing

- **Free tier:** RSS feeds free; full website free to read (some features require free registration)
- **Paid tiers:** None for general news
- **Enterprise:** Content syndication and licensing handled via The National's commercial team
- **Notes:** Owned by International Media Investments (IMI), a private holding company linked to senior Abu Dhabi government figures

## Authentication

None for RSS. Some on-site features (saved articles, newsletters) require a free user account.

## Endpoints

- **Base URL:** `https://www.thenationalnews.com/`
- **Key endpoints:**
  - RSS feed index: `/uae/rss-feeds-1.536712` — landing page with section-by-section feed links
  - Section pages (HTML, free to consume): `/news/uae`, `/news/gulf`, `/news/mena`, `/news/us`, `/news/uk`, `/news/europe`, `/news/asia`, `/business`, `/opinion`, `/future`, `/lifestyle`, `/sport`
- Specific section RSS feed URLs are listed on the RSS index page above and follow the publisher's CMS pattern (article IDs in `1.NNNNNN` format). Verify exact URLs from the index page before integration.

## Example call

```bash
# RSS index landing page (lists all section feeds)
curl "https://www.thenationalnews.com/uae/rss-feeds-1.536712"

# Example section page (HTML)
curl "https://www.thenationalnews.com/news/uae/"
```

## Rate limits

Not publicly documented.

## SDKs / Libraries

- **Official:** The National News iOS app (App Store ID 1281497691) and Android app (`com.the.national`); no developer SDKs
- **Community:** Standard RSS parsers

## Documentation

- Main site: https://www.thenationalnews.com/
- RSS feed index: https://www.thenationalnews.com/uae/rss-feeds-1.536712
- Follow us / channels: https://www.thenationalnews.com/follow-us/

## Notes

The National is **owned by International Media Investments (IMI)**, a private holding company widely understood to be linked to senior Abu Dhabi government figures — so for source-trust analysis, flag this as effectively Abu Dhabi government-aligned. Founded in 2008, it has positioned itself as the UAE's flagship English daily. Editorial coverage is strongest on UAE federal affairs, Gulf business, and MENA geopolitics from an Emirati lens. RSS feed surface is published via the index page above; exact URLs follow the publisher's CMS dot-numbered article format. The print edition is also available via PressReader's `thenational.pressreader.com`. No public REST/JSON developer API documented.
