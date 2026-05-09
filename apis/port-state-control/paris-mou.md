# Paris MoU

European / North Atlantic regional port-state-control organisation. Coverage is **outside the Strait of Malacca** but Paris MoU PSC history travels with the vessel — relevant for vessels that have called in Europe before transiting the Strait. Authoritative for European port performance data.

**Tier:** Free
**Auth:** None (public database)
**Last researched:** 2026-05-09

## Use cases

- Historical PSC inspection lookup for any vessel inspected in Paris MoU member ports (most of Europe + Russia + Canada).
- Black/Grey/White List flag-state performance — global reference even for vessels not currently in Paris MoU waters.
- Detention / refusal-of-access lists ("banned vessels") — global blacklist that follows vessels.
- Ship Risk Profile calculator and Company Performance calculator — useful for pre-port-call risk modelling.
- Cross-check against Tokyo MoU history for vessels with global trading patterns.

## Pricing

- **Free tier:** Free public database access.
- **Paid tiers:** None.
- **Enterprise:** Not applicable.
- **Notes:** Funded by member-state contributions and EMSA.

## Authentication

None. Public web portal at parismou.org.

## Endpoints

- **Public site:** `https://www.parismou.org/`
- **Inspection search:** `https://www.parismou.org/inspection-search/inspection-search`
- **Detentions / bans:** `https://www.parismou.org/inspections-risk/library-faq/detentions`
- **Performance lists:** `https://www.parismou.org/inspections-risk/library-faq/performance-lists`
- **No documented REST API.** Data available via web forms, monthly detention list PDFs, and annual report.

## Example call

```bash
# Paris MoU does not publish a REST API. Workflow:
# 1. Use the inspection search form at https://www.parismou.org/inspection-search/inspection-search by IMO.
# 2. Download monthly detention list PDFs from the publications page.
# 3. Aggregate via Equasis (which ingests Paris MoU data) for programmatic-friendly access.
```

## Rate limits

Not published. Don't hammer the search form.

## SDKs / Libraries

- **Official:** None.
- **Community:** Limited.

## Documentation

- Main site: https://www.parismou.org/
- Annual reports: https://www.parismou.org/publications-pages/annual-reports

## Notes

- For the Strait of Malacca specifically, Paris MoU data is **secondary** to Tokyo MoU — but vessel-history lookups should always check both, since high-risk vessels often try to avoid PSC scrutiny by switching trading regions.
- The Paris-Tokyo MoU performance-list correlation is high but not perfect; comparing both surfaces gaming behaviour.
- Paris MoU's risk-profile calculator is a publicly documented model — useful baseline if you're building your own internal risk-scoring.
