# Tehran Times

The first English-language daily newspaper printed after Iran's 1979 Islamic Revolution, founded by Mohammad Beheshti as the self-styled "voice of the Islamic Revolution". State-controlled (not state-owned), tied to the Mehr News Agency (MNA) and hardline factions within the Iranian government. Free RSS access.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-09

## Use cases

- Iranian state-controlled English-language perspective on regional and global affairs
- Tracking official Iranian positions on US-Iran relations, Israel, sanctions, Strait of Hormuz, nuclear program
- Building Middle East source-comparison dashboards (alongside Al Jazeera, Al Arabiya, Times of Israel)
- Persian-bloc geopolitical analysis from Tehran's editorial lens

## Pricing

- **Free tier:** Full RSS feed and site access free with no paywall
- **Paid tiers:** None
- **Enterprise:** Content licensing via direct contact with the publisher
- **Notes:** Funded as part of the MNA umbrella; not reliant on subscription revenue

## Authentication

None.

## Endpoints

- **Base URL:** `https://www.tehrantimes.com/`
- **Key endpoints:**
  - `GET /rss` — main all-news RSS feed
  - RSS help/index page: `/rss-help`
  - Section pages (HTML): `/service/politics`, `/service/international`, `/service/economy`, `/service/society`, `/service/culture`, `/service/multimedia`, `/service/sports`

## Example call

```bash
# Main RSS feed
curl "https://www.tehrantimes.com/rss"

# Politics section (HTML)
curl "https://www.tehrantimes.com/service/politics"
```

## Rate limits

Not publicly documented.

## SDKs / Libraries

- **Official:** None for the public RSS surface
- **Community:** Standard RSS parsers

## Documentation

- Main site: https://www.tehrantimes.com/
- RSS index: https://www.tehrantimes.com/rss-help

## Notes

Founded 1979 by Ayatollah Mohammad Hossein Beheshti as the self-described "voice of the oppressed people in the world." **Not state-owned but considered state-controlled**, closely tied to the **Mehr News Agency (MNA)** and **hardline factions within the Iranian government**. Mohammad Shojaeian became managing director in September 2019; Ali A. Jenabzadeh has been editor-in-chief since April 2020. Editorial line is supportive of the Islamic Republic's ideology and routinely refers to Israel as "the Israeli regime" or "the Zionist regime." Notable 2023 publication of a leaked U.S. State Department memo on the security clearance suspension of U.S. Special Envoy for Iran Rob Malley prompted U.S. House of Representatives investigations. For source-trust analysis: this is the most explicitly state-aligned outlet in this Middle East batch and should be flagged accordingly when used as a primary source. Useful as a primary-source channel for understanding official Iranian framing of regional events, **not as a balanced wire**. Sister English-language Iranian outlets (Press TV, IRNA English, Mehr News English) offer additional state perspectives but Tehran Times is the longest-running and best-known. No public REST/JSON developer API documented.
