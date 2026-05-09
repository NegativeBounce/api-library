# AllAfrica

Pan-African news aggregator distributing 600+ daily reports from 90+ African news organizations across 54 countries via free RSS/RDF feeds and commercial syndication.

**Tier:** Free
**Auth:** None (attribution required)
**Last researched:** 2026-05-09

## Use cases

- Continent-wide African news monitoring across 54 countries with country-level filtering
- Topic-specific news aggregation (85+ topics including conflict, governance, mining, health)
- Bilingual coverage in English (allafrica.com) and French (fr.allafrica.com)
- Building African-focused news readers, alerting tools, or dashboards

## Pricing

- **Free tier:** All RSS/RDF feeds free for personal and website use; attribution and link to AllAfrica home page or feed page required
- **Paid tiers:** None for RSS access
- **Enterprise:** Commercial content syndication and licensing available — contact partners.allafrica.com
- **Notes:** Headline modules provided "as-is" with no warranties; full article text typically requires visiting source publishers, since AllAfrica may not have legal rights to republish

## Authentication

None. RSS feeds are public. Attribution requirement: any site displaying headlines must link to AllAfrica home page or the relevant feed's main page.

## Endpoints

- **Base URL:** `https://allafrica.com/tools/headlines/rdf/` (English) and `https://fr.allafrica.com/tools/headlines/rdf/` (French)
- **Key endpoints:**
  - `GET /<category>/headlines.rdf` — RSS/RDF feed for the given category. Categories include: `latest`, `africa`, regions (`westafrica`, `eastafrica`, `northafrica`, `southernafrica`, `centralafrica`), country slugs (`nigeria`, `kenya`, `southafrica`, etc.), and 80+ topics (`business`, `mining`, `health`, `conflict`, `governance`)
  - Full category list: `https://allafrica.com/misc/tools/categories.html`

## Example call

```bash
# Latest pan-African headlines (English)
curl "https://allafrica.com/tools/headlines/rdf/latest/headlines.rdf"

# Nigeria-only feed
curl "https://allafrica.com/tools/headlines/rdf/nigeria/headlines.rdf"

# West Africa in French
curl "https://fr.allafrica.com/tools/headlines/rdf/westafrica/headlines.rdf"
```

## Rate limits

Not publicly documented. Standard HTTP polling etiquette applies; service published as `as-is`.

## SDKs / Libraries

- **Official:** None — standard RSS/RDF (RSS 1.0)
- **Community:** Any RSS parser (feedparser for Python, rss-parser for Node)

## Documentation

- Main docs: https://allafrica.com/misc/tools/rss.html
- Categories list: https://allafrica.com/misc/tools/categories.html

## Notes

Largest African news aggregator (founded 2000, registered in Mauritius), with offices in Cape Town, Dakar, Abuja, Johannesburg, Nairobi, and Washington DC. Aggregates from 90+ partner publishers and 500+ institutions; does not hold republishing rights to all content — RSS items typically link out to the original publisher. For full article text or commercial use, contact AllAfrica partnerships. RDF/RSS 1.0 format; consumers must support RDF or use a parser tolerant of both.
