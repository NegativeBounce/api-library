# JHOD NAVAREA XI (Japan Coast Guard)

Japan Hydrographic and Oceanographic Department (JHOD) coordinates NAVAREA XI under the IMO/IHO Worldwide Navigational Warning Service. Coverage includes the western Pacific and **the Strait of Malacca region** — making this the authoritative coordinator for Strait-relevant broadcast warnings.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-09

## Use cases

- **Authoritative NAVAREA XI warnings for the Strait of Malacca**: seismic survey activity, military exercises, dredging, channel closures, drifting hazards.
- Cross-reference with NAVTEX warnings broadcast on coastal frequencies in the Strait.
- Local Navigational Warnings issued by JHOD.
- Weekly summary of Notices to Mariners.
- Historical archive of NAVAREA XI warnings (2017–present).

## Pricing

- **Free tier:** Fully free public web access.
- **Paid tiers:** None.
- **Enterprise:** Not applicable.
- **Notes:** Operated by the Japan Coast Guard as a public maritime-safety service.

## Authentication

None.

## Endpoints

- **NAVAREA XI portal:** `https://www1.kaiho.mlit.go.jp/TUHO/keiho/navarea11_en.html`
- **JHOD home:** `https://www1.kaiho.mlit.go.jp/jhd-E.html`
- **No documented REST API.** Warnings are published as HTML pages and archived by year.

## Example call

```bash
# JHOD does not publish a REST API. Workflow:
# 1. Browse the NAVAREA XI page at https://www1.kaiho.mlit.go.jp/TUHO/keiho/navarea11_en.html
# 2. For programmatic ingestion, use SeaLagom (aggregates JHOD NAVAREA XI) — recommended.
# 3. Or scrape the HTML archive — JHOD does not formally object but no API support is offered.
```

## Rate limits

Not published. Standard web-access etiquette applies.

## SDKs / Libraries

- **Official:** None.
- **Community:** SeaLagom and similar aggregators ingest this data.

## Documentation

- NAVAREA XI page: https://www1.kaiho.mlit.go.jp/TUHO/keiho/navarea11_en.html
- JHOD international activities: https://www1.kaiho.mlit.go.jp/eng/kokusai_e.html
- 24-hour contact: +81-3-3595-3647

## Notes

- **The single most authoritative free source for NAVAREA XI warnings affecting the Strait of Malacca.** No API, but content is freely viewable.
- Indonesia and Malaysia operate their own coastal-warning services for the Strait under SeaLagom-aggregated coastal NAVTEX — confirm scope when designing pipelines.
- For ops automation, ingest via SeaLagom rather than scraping JHOD directly — saves engineering effort and adds coordinate extraction.
