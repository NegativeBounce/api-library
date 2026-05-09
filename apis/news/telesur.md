# TeleSUR English

The English-language service of teleSUR, a pan-Latin American multistate news network launched in 2005. Primarily funded by Venezuela with additional ALBA-bloc support (Cuba, Nicaragua, Bolivia historically); operated from Quito, Ecuador. Provides free RSS-accessible news with an explicit Bolivarian / leftist editorial line.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-09

## Use cases

- Pan-Latin American news with explicit leftist/Bolivarian editorial perspective
- Tracking Venezuelan government, Cuban affairs, Nicaragua, Bolivia, and broader ALBA-bloc positions in English
- Source-comparison alongside Western and centrist regional outlets (MercoPress, BA Times, Rio Times)
- US foreign policy coverage from a non-Western, anti-imperialist editorial angle
- Building OSINT pipelines that include heterodox Latin American state-funded perspectives

## Pricing

- **Free tier:** All RSS feeds and full website access free
- **Paid tiers:** None
- **Enterprise:** Content licensing handled directly via teleSUR
- **Notes:** Funded primarily through Venezuelan state contributions plus historical contributions from Cuba, Nicaragua, Bolivia, and other ALBA member governments; not a subscription or advertising-driven outlet

## Authentication

None.

## Endpoints

- **Base URL:** `https://www.telesurenglish.net/`
- **Key endpoints:**
  - Home: `/`
  - News index: `/section/news/index.html`
  - Latin America desk: `/news/latin-america/`
  - World desk: `/section/news/world/`
  - Analysis: `/section/news/analysis/`
  - Opinion / sport / culture sections also available
  - RSS index page: `/pages/rss.html`
- Parent network domain (Spanish): `https://www.telesurtv.net/` with English subsection at `/SubSecciones/en/`

## Example call

```bash
# Main English homepage
curl "https://www.telesurenglish.net/"

# Latin America desk
curl "https://www.telesurenglish.net/news/latin-america/"

# RSS index
curl "https://www.telesurenglish.net/pages/rss.html"
```

## Rate limits

Not publicly documented.

## SDKs / Libraries

- **Official:** Live HD broadcast streaming on website and apps; YouTube channel; Telegram and X channels; no developer SDKs
- **Community:** Standard RSS parsers

## Documentation

- Main English site: https://www.telesurenglish.net/
- RSS index: https://www.telesurenglish.net/pages/rss.html
- Parent network: https://www.telesurtv.net/

## Notes

TeleSUR was launched in 2005 as a multistate Latin American news network with the stated mission of providing **"an alternative perspective on global events"** to counter Western corporate media. **Primary funding is from the Venezuelan government** (Maduro / formerly Chávez administrations) with supplementary support over the years from **Cuba, Nicaragua, Bolivia, Ecuador, Uruguay, and Argentina** — though several ALBA-aligned governments have withdrawn or reduced funding amid political shifts (notably Argentina and Ecuador). **For source-trust analysis: this is openly state-funded with an explicit Bolivarian / leftist editorial line.** Editorial line is consistently supportive of Venezuelan, Cuban, and Nicaraguan governments and consistently critical of US foreign policy, NATO, and Western governments. Useful as a primary-source channel for **understanding ALBA-bloc framing** of Latin American and global events including sanctions, US military deployments, anti-imperialist movements, and indigenous/anti-extractivist coverage — **not as a balanced wire**. Strongest desks are Venezuela, Cuba, US foreign policy in Latin America, indigenous/social movements, and Palestine/Middle East coverage from a Global South perspective. Sister Spanish network teleSURtv operates from Caracas; the English service operates primarily from Quito, Ecuador. No public REST/JSON developer API documented; RSS surface plus HTML section pages are the programmatic interface.
