# GDELT Project

The Global Database of Events, Language, and Tone — a free open dataset and API platform tracking events, themes, and emotions in global news media in 65+ languages. Updates every 15 minutes. The largest open event-database in existence.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-09

## Use cases

- Real-time event detection in Indonesia, Malaysia, Singapore, and Thailand via the GDELT 2.0 Event Database (15-minute resolution).
- Sentiment / tone tracking in news coverage of Strait-of-Malacca-related topics (piracy, labour unrest at ports, environmental incidents).
- DOC 2.0 (full-text article search) for OSINT investigations.
- BigQuery integration for analyst SQL workflows over the full GDELT archive.
- Free fallback / cross-check when paid feeds (Dataminr, Factal) flag an event — does GDELT see the same coverage?
- Long-horizon historical research (archives 215+ years of news).

## Pricing

- **Free tier:** Fully free; no registration required. Open data under liberal licensing.
- **Paid tiers:** None.
- **Enterprise:** Not applicable.
- **Notes:** Hosting BigQuery queries incurs your own GCP costs; the data itself is free.

## Authentication

None for the public APIs and CSV downloads. BigQuery requires a Google Cloud account (your own).

## Endpoints

- **Event Database 2.0:** raw CSV files at `http://data.gdeltproject.org/gdeltv2/` (15-minute drops)
- **Global Knowledge Graph (GKG):** `http://data.gdeltproject.org/gdeltv2/`
- **DOC 2.0 API:** `https://api.gdeltproject.org/api/v2/doc/doc` — full-text article search
- **TV News API:** `https://api.gdeltproject.org/api/v2/tv/tv`
- **BigQuery datasets:** `gdelt-bq:gdeltv2.events`, `gdelt-bq:gdeltv2.gkg`, etc.

## Example call

```bash
# DOC 2.0 — last 24h of articles mentioning "Strait of Malacca"
curl 'https://api.gdeltproject.org/api/v2/doc/doc?query=%22strait+of+malacca%22&mode=ArtList&format=json&maxrecords=100&timespan=24h'
```

## Rate limits

Not formally published. The DOC API throttles overly long or short queries (returns "Your query was too short or too long"). BigQuery scaling is governed by your GCP account.

## SDKs / Libraries

- **Official:** None.
- **Community:** `gdelt` (Python), `gdeltr2` (R), various BigQuery dashboards.

## Documentation

- Project home: https://www.gdeltproject.org/
- Data access: https://www.gdeltproject.org/data.html
- DOC 2.0 docs: https://blog.gdeltproject.org/gdelt-doc-2-0-api-debuts/
- BigQuery overview: https://blog.gdeltproject.org/announcing-gdelt-2-0/

## Notes

- GDELT's CAMEO event taxonomy is widely used in conflict-event research — same actor/event coding conventions as ACLED in many cases.
- For the Strait specifically, DOC 2.0 search is invaluable: query for "Strait of Malacca" + tone < -3 to find negative-sentiment coverage spikes.
- High false-positive rate on raw event data — recommend pairing with ACLED for ground-truth, GDELT for breadth.
- Update cadence (15 min) is faster than ACLED (weekly free tier).
