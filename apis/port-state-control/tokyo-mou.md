# Tokyo MoU

Regional port-state-control organisation for the Asia-Pacific (22 member authorities including Indonesia, Malaysia, Singapore, Thailand). Authoritative source for PSC inspections of vessels calling at ports in or near the Strait of Malacca.

**Tier:** Free
**Auth:** None (public PSC database)
**Last researched:** 2026-05-09

## Use cases

- **Most-relevant PSC data for Strait of Malacca**: Tokyo MoU member authorities include Singapore, Malaysia, Indonesia, and Thailand — the littoral states.
- Vessel-history lookup by IMO or name in the Tokyo MoU PSC Database.
- Flag-state and recognized organisation (RO) performance rating (Black/Grey/White lists).
- Concentrated Inspection Campaign (CIC) results — periodic deep-dive themes (e.g., crew working hours, ECDIS proficiency).
- Detention / banning lists for vessels barred from member ports.
- Annual statistics on inspection rates and deficiency types.

## Pricing

- **Free tier:** Free public database access.
- **Paid tiers:** None.
- **Enterprise:** Not applicable.
- **Notes:** Member-only portal exists for additional resources, but core PSC data is public.

## Authentication

None for the public PSC database. Members-only portal requires authority credentials.

## Endpoints

- **Public site:** `https://www.tokyo-mou.org/`
- **PSC database:** `https://apcis.tmou.org/public/` (Asia-Pacific Computerized Information System)
- **Performance lists:** `https://www.tokyo-mou.org/inspections_detentions/PSC_database.php`
- **No documented REST API.** Data available via web search forms and downloadable annual reports.

## Example call

```bash
# Tokyo MoU does not publish a REST API. Workflow:
# 1. Use APCIS public search at https://apcis.tmou.org/public/ to look up vessel inspection history.
# 2. Download annual / monthly statistics PDFs from the main site.
# 3. For automated ingestion, careful scraping of APCIS or Equasis (which aggregates Tokyo MoU) is the typical pattern.
```

## Rate limits

Not published. Don't hammer the public form — use Equasis or commercial vendors for bulk programmatic queries.

## SDKs / Libraries

- **Official:** None.
- **Community:** Limited; some academic scrapers.

## Documentation

- Main site: https://www.tokyo-mou.org/
- APCIS public search: https://apcis.tmou.org/public/
- Reports / publications: https://www.tokyo-mou.org/publications/
- Contact: secretariat@tokyo-mou.org / +81-3-3433-0621

## Notes

- For the Strait of Malacca, Tokyo MoU is **the single most authoritative PSC dataset** because Singapore (high-throughput), Malaysia, Indonesia, and Thailand are all member authorities.
- Pair with Equasis for an aggregated cross-MoU view, or with S&P Global / Lloyd's List Intelligence for a productised feed.
- Performance-list classifications (Black/Grey/White) are heavily used by underwriters and charterers — useful flags in your risk model.
