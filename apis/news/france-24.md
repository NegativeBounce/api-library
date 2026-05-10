# France 24

France's international public broadcaster, headquartered in Paris with 430 journalists from 35 nationalities and a network of 160 correspondent bureaus worldwide. Free RSS feeds across all English sections plus per-tag and per-section variants. Publicly funded but editorially independent (BBC-style).

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-09

## Use cases

- France domestic and EU policy news in English (Élysée, French government, EU summits, French elections)
- French-perspective international affairs (Africa, Middle East, transatlantic relations)
- Pan-European coverage with French editorial framing (NATO, Russia-Ukraine war, EU enlargement)
- Multi-language news pipelines — France 24 broadcasts in French, English, Arabic, and Spanish
- Public-broadcaster reference comparison alongside BBC, DW, NHK World, RFI, Yle News

## Pricing

- **Free tier:** All RSS feeds, full website, mobile app, 24/7 livestream, podcasts, newsletters
- **Paid tiers:** None — fully publicly funded
- **Enterprise:** Content licensing via France Médias Monde Distribution; contact via main site
- **Notes:** France 24 is part of **France Médias Monde** (parent company), which also operates **RFI** (Radio France Internationale) and **MCD** (Monte Carlo Doualiya). Funded by French state via parliamentary appropriation; carries advertising on some platforms

## Authentication

None.

## Endpoints

- **Base URL:** `https://www.france24.com/en/`
- **Key endpoints (English RSS feeds):**
  - All English content: `https://www.france24.com/en/rss`
  - France: `https://www.france24.com/en/france/rss`
  - Europe: `https://www.france24.com/en/europe/rss`
  - Africa: `https://www.france24.com/en/africa/rss`
  - Middle East: `https://www.france24.com/en/middle-east/rss`
  - Americas: `https://www.france24.com/en/americas/rss`
  - Asia/Pacific: `https://www.france24.com/en/asia-pacific/rss`
  - Business & Tech: `https://www.france24.com/en/business-tech/rss`
  - Environment: `https://www.france24.com/en/environment/rss`
  - Sports: `https://www.france24.com/en/sport/rss`
  - Culture: `https://www.france24.com/en/culture/rss`
  - Tag pattern: `https://www.france24.com/en/tag/{tag}/rss` (e.g. `/en/tag/health/rss`, `/en/tag/ukraine/rss`)
- **RSS index page (canonical list):** `https://www.france24.com/en/rss-feeds`
- **Other languages:** swap `/en/` for `/fr/`, `/es/`, `/ar/` for French, Spanish, Arabic editions

## Example call

```bash
# All English content
curl "https://www.france24.com/en/rss"

# Europe section
curl "https://www.france24.com/en/europe/rss"

# Tag-based feed (e.g. Ukraine)
curl "https://www.france24.com/en/tag/ukraine/rss"
```

## Rate limits

Not publicly documented; standard RSS polling assumed.

## SDKs / Libraries

- **Official:** France 24 mobile apps for iOS, Android; podcast feeds; newsletter service
- **Community:** Standard RSS parsers; TelemetryTV digital signage integration

## Documentation

- Main English site: https://www.france24.com/en
- RSS feed index (canonical): https://www.france24.com/en/rss-feeds
- About France 24: https://www.france24.com/en/about-us
- France Médias Monde (parent): https://www.francemediasmonde.com/en

## Notes

France 24 is **France's international public broadcaster**, launched in December 2006 as part of a French government strategy to provide a French-perspective alternative to BBC World News and CNN International. Headquartered in **Issy-les-Moulineaux** (Paris suburb) with 430 journalists representing 35 nationalities and a network of **160 correspondent bureaus** in nearly every country.

**Parent company:** **France Médias Monde** (FMM), which also operates **RFI** (Radio France Internationale, French international radio with strong Africa coverage) and **Monte Carlo Doualiya** (Arabic-language radio). FMM is owned by the French state and funded via parliamentary appropriation through the French audiovisual public funding system. **Editorial independence governance:** France 24 operates under French public-broadcaster editorial-independence norms, similar to BBC and DW. While the editorial line is consistent with French diplomatic positioning (pro-EU, pro-NATO, sympathetic to French foreign policy in Africa and the Middle East), it has not been credibly accused of state propaganda. **For source-trust analysis:** generally considered credible mainstream public broadcasting, with strongest coverage of **Africa (especially Francophone Africa)**, **Middle East**, **Europe/EU institutions**, and **France domestic politics**.

**Coverage strengths worth noting:** France 24's **Francophone Africa** desk is among the strongest in international English-language broadcasting (alongside RFI), making it a useful complement to Africanews, AllAfrica, and Daily Maverick for African affairs coverage. The tag-based RSS pattern (`/en/tag/{tag}/rss`) is particularly useful for topic-specific monitoring (e.g. country-specific feeds like `/en/tag/ukraine/rss`, `/en/tag/syria/rss`). No public REST/JSON developer API documented; RSS is the primary programmatic surface.
