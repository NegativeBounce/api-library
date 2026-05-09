# Breaking Belize News (BBN)

Belize's leading online news outlet, founded in 2013 by Larry Waight. Reaches approximately 10 million readers per year and 20+ million page views annually, covering Belize alongside Caribbean and Central American developments. Belize-native English (Belize is anglophone).

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-09

## Use cases

- Belize breaking news monitoring (politics, crime, society, business, weather, basketball/sports)
- Tracking Belize-Guatemala territorial dispute, BSI/Tate & Lyle sugar industry, tourism, oil/gas
- Building Caribbean and Central American regional news readers with Belize-specific depth
- Augmenting BBC/Reuters Caribbean coverage with on-the-ground English reporting from Belmopan, Belize City, and the districts

## Pricing

- **Free tier:** Full website access free; mobile app for live notifications
- **Paid tiers:** None
- **Enterprise:** Advertising on `breakingbelizenews.com`; contact via the site's commercial team
- **Notes:** Funded primarily through advertising; mobile app distributed via Google Play (developed by Tana Technologies)

## Authentication

None.

## Endpoints

- **Base URL:** `https://www.breakingbelizenews.com/`
- **Key endpoints:**
  - Main site: `https://www.breakingbelizenews.com/`
  - RSS feed: `https://www.breakingbelizenews.com/feed/` (typical WordPress pattern; verify on integration)
  - Section pages (HTML): national news, international news, sports, entertainment, business, opinion
  - Telegram channel: distribution channel referenced in Twitter bio for platform-resilient updates

## Example call

```bash
# Main site
curl "https://www.breakingbelizenews.com/"

# RSS feed (verify exact path on first integration)
curl "https://www.breakingbelizenews.com/feed/"
```

## Rate limits

Not publicly documented.

## SDKs / Libraries

- **Official:** Breaking Belize News mobile app on Google Play (`com.tana.breakingbelizenews`) for live news notifications, lottery results (Boledo, Fantasy 5, Pick 3), and weather forecasts; YouTube channel
- **Community:** Standard RSS parsers

## Documentation

- Main site: https://www.breakingbelizenews.com/
- Wikipedia: https://en.wikipedia.org/wiki/Breaking_Belize_News

## Notes

Breaking Belize News (BBN) is **independent** and was **founded in 2013 by Larry Waight**. According to the publication's own metrics, BBN serves an average of two million readers per year and gets 20+ million page views annually, making it among the fastest-growing media outlets in Belize. **Belize is anglophone** (English is the official language), so BBN is publishing in the country's primary language — not a "translated edition" in the way El Faro English or Confidencial English are. Coverage spans national news (politics, crime, courts, education, agriculture), international headlines, sports (especially basketball — National Elite Basketball League), entertainment, and business. Has correspondents reporting from Belmopan, Belize City, Toledo, Corozal, Orange Walk, and Cayo districts. Sister/competing English Belize outlets include `channel5belize.com` (5 News Belize, TV-affiliated), `lovefm.com` (radio + news), `sanpedrosun.com` (Ambergris Caye / San Pedro local), and `reporter.bz` (The Reporter Belize, weekly print). For source-trust analysis: independent ownership, no government affiliation, no major editorial bias documented in international press-freedom reports. No public REST/JSON developer API documented; the WordPress-style `/feed/` RSS plus mobile app push are the programmatic surfaces.
