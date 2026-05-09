# Middle East Eye

A UK-based independently funded digital news organisation founded in April 2014, focusing on the Middle East, North Africa, and the broader Muslim world. London-headquartered (M.E.E. Limited), free RSS-accessible. ISSN 2634-2456.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-09

## Use cases

- Middle East and North Africa coverage with on-the-ground reporting and "read between the lines" editorial stance
- Tracking Israel-Palestine, Gulf affairs, Egypt, Turkey, Iran with English-language non-Western perspective
- Augmenting Western and Arab state media with a UK-based independent ME-focused source
- Long-form analysis, opinion, and investigative reporting on regional politics, military affairs, and culture

## Pricing

- **Free tier:** Full RSS feed and site access free with no paywall
- **Paid tiers:** None
- **Enterprise:** Content syndication and licensing via direct contact with editorial leadership
- **Notes:** Self-described as "independently funded"; see Notes section for source-trust caveats

## Authentication

None.

## Endpoints

- **Base URL:** `https://www.middleeasteye.net/`
- **Key endpoints:**
  - `GET /rss` — main all-news RSS feed
  - Topic pages (HTML): `/topics/sport`, `/topics/books`, `/news` (main news landing), `/opinion`
  - Sections: news, opinion, culture, video, investigations

## Example call

```bash
curl "https://www.middleeasteye.net/rss"
```

## Rate limits

Not publicly documented.

## SDKs / Libraries

- **Official:** None for the public RSS surface
- **Community:** Standard RSS parsers

## Documentation

- Main site: https://www.middleeasteye.net/
- About: https://www.middleeasteye.net/about-middle-east-eye

## Notes

Editorial independence claim is **disputed for source-trust purposes**: Middle East Eye is formally owned by M.E.E. Limited (sole director Jamal Bessasso) and editor-in-chief is David Hearst, a former foreign lead writer for The Guardian. The organisation **denies and will not disclose its funding sources**, but it is **widely alleged (per Wikipedia, Arab News, and others) to be funded by the government of Qatar**. Several Al Jazeera journalists joined the project around its 2013-2014 formation, and Jonathan Powell, a senior Al Jazeera executive, was a consultant ahead of launch and registered the website's domain names. For users comparing source-trust across Middle East outlets: weight this alongside Al Jazeera's openly partial Qatari government funding when sourcing analysis. Coverage is strongest on Israel-Palestine, Egypt, Turkey, and Gulf affairs from a perspective generally critical of Western, Saudi, UAE, and Egyptian government policies. Employs ~20 full-time staff in London (as of 2017 figures; current staffing not disclosed). Note ISSN 2634-2456 for citation purposes.
