# Deutsche Welle (DW)

Germany's international public broadcaster, founded in 1953 in Bonn. Free RSS feeds across all sections in English (plus 30+ other languages). Public-broadcaster funded by the German federal tax budget under the Deutsche Welle Act, which guarantees editorial independence from government influence (BBC-style firewall).

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-09

## Use cases

- Germany domestic and EU policy news in English (Bundestag, Bundesbank, Berlin coalition politics, Energiewende, Bundesliga sports)
- European affairs coverage (Brussels, NATO, EU institutions, Western Europe)
- German-perspective international affairs (Russia-Ukraine war, transatlantic relations, China-EU)
- Multilingual news pipelines — DW publishes in 30+ languages, useful for cross-language ingestion
- Public-broadcaster reference comparison alongside BBC, France 24, NHK World, RFI, Yle News for editorial-independence benchmarks

## Pricing

- **Free tier:** All RSS feeds, full website, mobile apps (iOS, Android, Windows, Symbian), 24/7 TV stream, podcasts, newsletters
- **Paid tiers:** None — fully publicly funded
- **Enterprise:** Content licensing and republication via DW Distribution / DW Transtel; contact via main site
- **Notes:** Funded by the **German federal tax budget**; no advertising on DW news content; editorial independence regulated by the **Deutsche Welle Act**

## Authentication

None.

## Endpoints

- **Base URL:** `https://rss.dw.com/`
- **Key endpoints (English RSS feeds):**
  - All English content: `https://rss.dw.com/rdf/rss-en-all`
  - Top stories: `https://rss.dw.com/rdf/rss-en-top`
  - Germany: `https://rss.dw.com/rdf/rss-en-ger`
  - Europe: `https://rss.dw.com/rdf/rss-en-eu`
  - Asia: `https://rss.dw.com/rdf/rss-en-asia`
  - Business: `https://rss.dw.com/rdf/rss-en-bus`
  - Culture: `https://rss.dw.com/rdf/rss-en-cul`
  - Sports: `https://rss.dw.com/rdf/rss-en-sports`
  - Environment: `https://rss.dw.com/xml/rss_en_enviro`
  - Science: `https://rss.dw.com/xml/rss_en_science`
  - Atom variant: `https://rss.dw.com/atom/rss-en-all`
- **Other languages:** swap `en` for `de` (German), `es` (Spanish), `ar` (Arabic), `ru` (Russian), `fa` (Persian), `tr` (Turkish), `uk` (Ukrainian), etc. — pattern is `rss-{lang}-{section}`
- **Main site:** `https://www.dw.com/en`

## Example call

```bash
# All English content
curl "https://rss.dw.com/rdf/rss-en-all"

# Europe section
curl "https://rss.dw.com/rdf/rss-en-eu"

# Atom variant for top stories
curl "https://rss.dw.com/atom/rss-en-all"
```

## Rate limits

Not publicly documented; standard RSS polling assumed.

## SDKs / Libraries

- **Official:** DW mobile apps for iOS, Android, Windows; DW newsletter service (4 newsletter types: morning compact, evening compact, daily, weekly)
- **Community:** Standard RSS/Atom parsers

## Documentation

- Main English site: https://www.dw.com/en
- RSS feed index: https://www.dw.com/en/more-dw/rss/s-31500
- About DW: https://www.dw.com/en/about-dw/profile/s-30688
- DW Akademie (international media development arm): https://akademie.dw.com/

## Notes

DW is **Germany's international public broadcaster**, founded in May 1953 in Bonn. Approximately 3,000 employees and freelancers from 60+ countries; headquarters in Bonn with a main studio in Berlin. **Broadcasts in 30+ languages**, with satellite TV channels in English, Spanish, and Arabic. The first DW broadcast was a speech by then-Federal President Theodor Heuss on May 3, 1953.

**Editorial independence governance:** DW is funded by the German federal tax budget (Bundesetat), but the **Deutsche Welle Act** (Deutsche-Welle-Gesetz) explicitly mandates that DW content be **independent of government influence**. This is the same BBC-style firewall model as France 24, RFI, NHK World, and Yle News. **For source-trust analysis:** DW is generally considered a credible mainstream public broadcaster, with editorial line consistent with German foreign policy positioning (pro-EU, pro-NATO, pro-Ukraine in current war coverage). Worth flagging that DW's primary mission is Germany's "soft-power" international communications — not domestic German news (the latter is provided by ARD/ZDF). DW has been particularly notable for its **31-language coverage of Russia-Ukraine war** since February 2022, and for maintaining independent Russian-language coverage that has been blocked inside Russia. **DW Akademie** is Germany's media-development organization, training journalists in conflict zones and developing democracies. No public REST/JSON developer API documented; the RDF/Atom RSS endpoints are the primary programmatic surface.
