# El Faro English

The English-language service of El Faro, Latin America's first internet-native digital newspaper, founded in 1998 in San Salvador. Currently operates from exile in San José, Costa Rica (since 2023) under non-profit Fundación Periódica. Free RSS-accessible; multi-award-winning investigative journalism.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-09

## Use cases

- El Salvador and Central America investigative journalism (Bukele administration, gang dynamics, Mara Salvatrucha-13, migration, US-Central America policy)
- Tracking Salvadoran human rights, press freedom, and authoritarian-era developments under Bukele's "state of emergency"
- Cross-regional Central American politics with English-language coverage of Guatemala, Honduras, Nicaragua, Costa Rica
- US-El Salvador relations, especially CECOT prison, Trump administration deportation programs, and Salvadoran diaspora affairs
- Source-comparison alongside other Central American outlets (Tico Times, Confidencial, BBN) for cross-checking regional coverage

## Pricing

- **Free tier:** All RSS-style content and full website free; no paywall
- **Paid tiers:** Optional reader membership ("crowdfunders" community of 1,200+ in El Salvador, US, and globally); members receive exclusive newsroom events and ForoCAP access
- **Enterprise:** Content licensing and republication via direct contact; co-productions with NYT, El País, Univision, Radio Ambulante, ICIJ, and Forbidden Stories
- **Notes:** Funding mix per most recent disclosures: **75% international foundations, 8% royalties (books/films/syndication), 7% advertising, 6% reader contributions, 4% workshops/events**

## Authentication

None.

## Endpoints

- **Base URL:** `https://elfaro.net/en` (canonical) and `https://beta.elfaro.net/en` (beta/current site)
- **Key endpoints:**
  - English homepage: `https://beta.elfaro.net/en`
  - Section pages (HTML): `/en/central-america`, `/en/el-salvador`, `/en/opinion-en`
  - Spanish parent site: `https://elfaro.net/`
  - About / mission: `https://elfaro.net/en/info/about/`

## Example call

```bash
# English homepage
curl "https://beta.elfaro.net/en"

# Spanish parent site (for cross-language ingestion)
curl "https://elfaro.net/"
```

## Rate limits

Not publicly documented.

## SDKs / Libraries

- **Official:** None for the public RSS surface
- **Community:** Standard RSS parsers; X/Twitter `@elfaroenglish` for new-content notifications

## Documentation

- English site: https://beta.elfaro.net/en
- Spanish site: https://elfaro.net/
- About: https://elfaro.net/en/info/about/
- Devex profile: https://www.devex.com/organizations/el-faro-136970

## Notes

El Faro is **independent** and was the **first internet-native, digital-only news outlet in Latin America**, publishing its first article on May 14, 1998. Founded by journalist Carlos Dada and businessman Jorge Simán; Dada has served as editorial director throughout most of the outlet's history. **Currently operates in exile from San José, Costa Rica**, having moved its administrative and legal operations to Costa Rica in April 2023 under the non-profit Fundación Periódica. The bulk of the newsroom remains in San Salvador, with reporters in Guatemala City and Washington, D.C. **El Faro English** was launched in October 2019, beginning as a weekly newsletter and now serving as a full English-language edition.

**Active state-led retaliation alert (May 2026):** On May 7, 2026, El Faro announced that **two of its members' assets, including a bank account and property, were frozen** by the Salvadoran government in retaliation for reporting on Bukele's administration. El Faro has been under sustained legal harassment since 2020 (alleged $200K tax evasion claim), Pegasus spyware was detected on more than 20 of its journalists' iPhones in 2022 (NSO Group lawsuit filed in US federal court), and most of its team operates in exile. Recent investigations include the **Bukele-MS-13 gang negotiations** (May 2020 — broke open the story; later expanded into a 2024 PBS Frontline documentary), the **2010 Monseñor Romero assassination interview** (Captain Álvaro Saravia confession), and contributions to **Panama Papers, Paradise Papers, and Mining Secrets** (Forbidden Stories) projects.

For source-trust analysis: **independent, foundation-funded, multi-award-winning, currently under direct state harassment for its journalism**. Editorial line is investigative and government-critical regardless of left/right alignment (has criticized FMLN and ARENA governments historically; current focus is Bukele's authoritarian consolidation). The 75% international-foundations funding share is worth noting — common among investigative outlets in repressive media environments, but a factor for source-trust analysis. No public REST/JSON developer API documented; X/Twitter `@elfaroenglish` is a reliable signal for new English content.
