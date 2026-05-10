# TASS English

The English-language service of TASS (Russian News Agency), the official Russian state news agency dating back to 1904 (founded as the Saint Petersburg Telegraph Agency, later TASS in Soviet era). Free, RSS-accessible, and explicitly serves as the official voice of the Russian government — flag prominently as state media in any source-trust analysis.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-09

## Use cases

- **Russian government official positions and announcements** (Kremlin statements, Ministry of Foreign Affairs press conferences, Putin speeches, official military bulletins from Russian Ministry of Defence)
- Tracking how the Russian state frames international affairs, sanctions, war operations, and diplomatic events
- Sentiment analysis and propaganda monitoring (counter-intelligence and OSINT use cases)
- Cross-source verification — TASS is often the original source for Russian government statements that other outlets quote second-hand
- **Source-trust counterweight** — pairing TASS with Meduza, Kyiv Independent, and DW Russian-language coverage for triangulating Russian-domestic events

## Pricing

- **Free tier:** Full website access and RSS feeds; no paywall on public news
- **Paid tiers:** Wire service subscriptions for media organizations and government clients (legacy news-agency model)
- **Enterprise:** TASS news agency wire service — direct subscriptions for newsrooms, contact via main site
- **Notes:** **State-funded** by the Russian government; TASS is a **federal state unitary enterprise** (FGUP) under the Russian Ministry of Digital Development, Communications and Mass Media

## Authentication

None for the public website / RSS surface. Wire service requires subscription contract.

## Endpoints

- **Base URL:** `https://tass.com/` (English) and `https://tass.ru/` (Russian)
- **Key endpoints (English):**
  - English homepage: `https://tass.com/`
  - Section pages (HTML): `/world`, `/politics`, `/defense`, `/economy`, `/society`, `/sports`, `/science`, `/emergencies`, `/press-review`
  - RSS feeds (verify on integration): typical pattern `https://tass.com/rss/v2.xml` for main feed; section RSS may be available at `/rss/{section}.xml`
- **Other languages:** Russian primary at `tass.ru`; also serves Spanish, Arabic, Chinese, French through separate language editions

## Example call

```bash
# English homepage
curl "https://tass.com/"

# RSS feed (verify exact path on first integration)
curl "https://tass.com/rss/v2.xml"
```

## Rate limits

Not publicly documented. **Sanctions caveat:** TASS is subject to **EU sanctions** (broadcasting restrictions in EU member states), **UK sanctions** (May 2022 onward), and **various national-level restrictions**. Some western jurisdictions may block or rate-limit access from local IPs. **US sanctions:** TASS itself is not on the OFAC SDN List, but related entities and individuals are. Compliance teams should verify current sanctions posture before integration.

## SDKs / Libraries

- **Official:** TASS mobile apps; legacy wire-service feeds for newsroom subscribers
- **Community:** Standard RSS parsers

## Documentation

- English site: https://tass.com/
- Russian site: https://tass.ru/
- About TASS: https://tass.com/info/about-us

## Notes

TASS (Russian News Agency, formerly **Telegraph Agency of the Soviet Union**) is **the official state news agency of the Russian Federation**. The agency traces its origins to **1904** (founded as the Saint Petersburg Telegraph Agency under Tsar Nicholas II), was renamed ROSTA after the 1917 revolution, became **TASS in 1925** as the Soviet Union's primary news service, and continued as the principal Russian state news agency after the Soviet Union's dissolution in 1991. Today TASS operates as a **federal state unitary enterprise (FGUP)** — meaning it is wholly owned and funded by the Russian Federation government.

**For source-trust analysis — flag prominently:**
- **TASS is openly Russian state media.** It does not have any BBC-style editorial-independence firewall analogous to DW or France 24. Editorial line is consistent with Russian government foreign and domestic policy positioning.
- Coverage of **Russia-Ukraine war**, **sanctions**, **Russian domestic dissent**, and **international affairs involving Russia** should be treated as official government framing — useful for understanding Russian state positions, **not** as independently verified information.
- TASS is frequently the primary source for Russian Ministry of Defence battlefield reports, Russian Foreign Ministry statements, and Kremlin announcements. Independent verification via Western, Ukrainian, and Russian-exile sources (Kyiv Independent, Meduza, Novaya Gazeta Europe, BBC Russian, DW Russian, RFE/RL) is essential for editorial use.

**Use cases where TASS is appropriate:**
- Pulling official Russian government statements verbatim for analysis
- Tracking how the Russian state frames events for both domestic and international audiences
- Counter-intelligence, OSINT, sentiment analysis, propaganda monitoring
- Cross-checking quoted Russian official statements that may have been paraphrased elsewhere

**Use cases where TASS should NOT be the primary source:**
- Verified casualty figures, battlefield outcomes, or war-crimes documentation
- Russian domestic dissent, opposition movements, or human-rights conditions
- Independent fact-finding on any topic where the Russian government has a stake in the narrative

**Sister Russian state media** to be aware of: **Sputnik** (formerly Russia Today's wire service, similarly state-controlled), **RIA Novosti** (state news agency, sister to TASS but with different structural lineage), and **RT** (television/digital, EU-banned and US-sanctioned). All three should carry the same source-trust flags as TASS. No public REST/JSON developer API documented for the consumer-facing TASS English service; the RSS endpoints and HTML site are the primary programmatic surfaces.
