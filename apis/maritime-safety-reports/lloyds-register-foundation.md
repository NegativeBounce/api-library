# Lloyd's Register Foundation

Independent global safety charity (formerly Lloyd's Register's charitable arm) funding research, education, and data initiatives on engineering and technology safety — including the Global Safety Evidence Center (GSEC) and maritime heritage archive.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-13

## Use cases

- Accessing the Global Safety Evidence Center (GSEC) for curated safety research and evidence syntheses across transport and engineering sectors
- Downloading maritime heritage archive materials including historical classification records and safety-at-sea publications
- Sourcing academic and industry safety research reports funded by the foundation for literature reviews

## Pricing

- **Free tier:** All public reports, GSEC content, and heritage archive materials freely available; no registration required
- **Paid tiers:** None for public content
- **Enterprise:** N/A — charitable organization; all funded research is published openly
- **Notes:** Some heritage archive materials may require contacting the archive team for high-resolution access.

## Authentication

No authentication required for public reports and GSEC content.

## Endpoints

- **Foundation home:** `https://www.lrfoundation.org.uk/`
- **Publications:** `https://www.lrfoundation.org.uk/news/publications` — all foundation-funded research reports
- **GSEC (Global Safety Evidence Center):** `https://www.lrfoundation.org.uk/gsec` — curated safety evidence portal
- **Heritage archive (safety at sea):** `https://heritage.lrfoundation.org.uk/safety-at-sea` — historical maritime safety records
- **Access method:** Web portal and PDF download; no REST API

**No programmatic API exists.** Content is delivered via web pages and downloadable PDF reports.

## Example call

```bash
# Fetch publications listing page
curl -s "https://www.lrfoundation.org.uk/news/publications" -H "User-Agent: Mozilla/5.0"
```

```python
import requests
from bs4 import BeautifulSoup

resp = requests.get(
    "https://www.lrfoundation.org.uk/news/publications",
    headers={"User-Agent": "Mozilla/5.0"},
)
soup = BeautifulSoup(resp.text, "html.parser")
links = [a["href"] for a in soup.find_all("a", href=True) if "publication" in a["href"].lower()]
for link in links:
    print(link)
```

## Rate limits

No API — web scraping only. No published rate limits; apply respectful crawl delays.

## SDKs / Libraries

- **Official:** None
- **Community:** None

## Documentation

- Foundation website: https://www.lrfoundation.org.uk/
- GSEC portal: https://www.lrfoundation.org.uk/gsec
- Heritage archive: https://heritage.lrfoundation.org.uk/safety-at-sea
- Research grants and partners: https://www.lrfoundation.org.uk/research

## Notes

- The Lloyd's Register Foundation is independent of Lloyd's Register Group (the classification society) — it is a charity focused on safety research, not a commercial entity.
- GSEC synthesizes evidence across multiple safety domains: maritime, rail, road, workplace, and emerging technologies (autonomous systems, hydrogen, digitalization).
- The heritage archive contains Lloyd's Register survey records dating back to 1764 — the longest-running continuous dataset of merchant vessel classification and condition records in existence.
- Foundation research areas include: human factors, safety culture, risk perception, accident investigation methodology, and safety of autonomous and digital systems.
- Annual impact reports and research summaries are published each year and available in the publications section.
- For investigation-authority accident reports, pair with MAIB (`maib.md`) and IMO GISIS (`imo-gisis.md`); the foundation's research provides complementary academic context.
