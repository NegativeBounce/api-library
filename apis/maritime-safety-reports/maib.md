# MAIB (Marine Accident Investigation Branch)

UK government agency responsible for investigating marine accidents involving UK ships worldwide and ships in UK waters — publishing detailed investigation reports, safety bulletins, and an anonymized biannual statistics dataset.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-13

## Use cases

- Accessing full-text MAIB investigation reports for serious marine accidents involving UK vessels or UK waters
- Monitoring new report publications via the GOV.UK Atom feed for automated ingestion workflows
- Downloading the anonymized biannual statistics dataset (Power BI .pbix or CSV) for trend analysis

## Pricing

- **Free tier:** All investigation reports, safety bulletins, and datasets freely available; no registration required
- **Paid tiers:** None
- **Enterprise:** N/A — UK government publication
- **Notes:** All MAIB outputs are published under the Open Government Licence (OGL v3.0).

## Authentication

No authentication required. All content is publicly accessible.

## Endpoints

- **Reports listing:** `https://www.gov.uk/maib-reports` — full archive of MAIB investigation reports, searchable by vessel type, accident type, and date
- **Atom feed (new reports):** `https://www.gov.uk/government/organisations/marine-accident-investigation-branch.atom` — GOV.UK Atom feed; fires on each new MAIB publication
- **Statistics data portal:** `https://maps.dft.gov.uk/maib-data-portal/` — interactive Power BI dashboard; anonymized incident data 2021–2024; biannual updates
- **Access method:** HTML scraping (reports listing), Atom feed (new report notifications), Power BI .pbix download (statistics)

**No REST API exists.** Programmatic access is via the Atom feed (new reports) and the downloadable .pbix / CSV dataset (statistics).

## Example call

```bash
# Poll the Atom feed for new MAIB reports
curl -s "https://www.gov.uk/government/organisations/marine-accident-investigation-branch.atom" \
  | python3 -c "import sys; import xml.etree.ElementTree as ET; \
    root = ET.parse(sys.stdin).getroot(); \
    ns = '{http://www.w3.org/2005/Atom}'; \
    [print(e.find(f'{ns}title').text, e.find(f'{ns}updated').text) for e in root.findall(f'{ns}entry')]"
```

```python
import feedparser

feed = feedparser.parse(
    "https://www.gov.uk/government/organisations/marine-accident-investigation-branch.atom"
)
for entry in feed.entries:
    print(entry.title, entry.updated, entry.link)
```

## Rate limits

No API — Atom feed polling and web download only. GOV.UK imposes standard rate limiting; poll the Atom feed no more frequently than once per hour.

## SDKs / Libraries

- **Official:** None
- **Community:** `feedparser` (Python) for Atom feed parsing; Power BI Desktop or `semantic-link` (Python) for .pbix file access

## Documentation

- Reports archive: https://www.gov.uk/maib-reports
- MAIB organisation page: https://www.gov.uk/government/organisations/marine-accident-investigation-branch
- Statistics data portal: https://maps.dft.gov.uk/maib-data-portal/
- Safety bulletins: https://www.gov.uk/government/collections/maib-safety-bulletins

## Notes

- MAIB investigates accidents in the public interest to improve safety — reports are not for the purpose of determining liability or blame.
- The statistics dataset (2021–2024, biannual) covers accident type, vessel type, location, and outcome with personal identifiers removed; download as .pbix (Power BI) or extract underlying data as CSV.
- Investigation reports typically include: vessel particulars, sequence of events, analysis, conclusions, and safety recommendations.
- MAIB covers UK-registered vessels worldwide and all vessels in UK territorial waters; Scotland, England, Wales, and Northern Ireland are all included (unlike the UK Police API which excludes Scotland).
- For European-wide casualty data, pair with EMSA EMCIP (`emsa-emcip.md`); for global investigation reports, use IMO GISIS (`imo-gisis.md`).
- The Atom feed is the most reliable programmatic notification path for new MAIB publications — typically 20–40 reports per year.
- Safety bulletins (distinct from full investigation reports) are issued for urgent safety issues and appear in the same Atom feed.
