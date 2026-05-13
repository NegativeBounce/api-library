# Gard Loss Prevention

Loss prevention publications and safety alerts from Gard, one of the world's largest marine insurers (P&I and H&M), covering incident case studies, claims analysis, operational guidance, and circulars for shipowners, operators, and seafarers.

**Tier:** Free (public content); Member portal (policyholder access)
**Auth:** None (public articles and circulars)
**Last researched:** 2026-05-13

## Use cases

- Accessing incident case studies and loss prevention alerts for maritime safety research and training
- Reviewing Gard circulars on regulatory changes, emerging risks, and claims trends
- Building a feed of maritime loss prevention content for risk intelligence workflows

## Pricing

- **Free tier:** All public articles, loss prevention alerts, and circulars available without registration
- **Paid tiers:** None for public content
- **Enterprise:** Gard member portal (SCOL) provides policyholders with additional claims and certificate services; requires Gard membership
- **Notes:** Gard is a mutual insurer — membership is required to access policy-specific services, but all loss prevention publications are public.

## Authentication

No authentication required for public articles and circulars. The SCOL member portal requires Gard policyholder credentials.

## Endpoints

- **Articles hub:** `https://www.gard.no/articles/` — searchable and filterable library of loss prevention articles and incident case studies
- **Loss prevention updates:** `https://www.gard.no/web/updates/lossprevention` — loss prevention alert archive (legacy path; may redirect)
- **Circulars:** `https://www.gard.no/circulars/` — regulatory and operational circulars
- **Access method:** Web browsing and HTML scraping; no REST API or RSS feed confirmed

**No programmatic API exists.** Content is delivered as HTML articles and PDF attachments.

## Example call

```bash
# Fetch articles listing page
curl -s "https://www.gard.no/articles/" -H "User-Agent: Mozilla/5.0"
```

```python
import requests
from bs4 import BeautifulSoup

resp = requests.get("https://www.gard.no/articles/", headers={"User-Agent": "Mozilla/5.0"})
soup = BeautifulSoup(resp.text, "html.parser")
articles = soup.find_all("article")
for article in articles:
    title = article.find("h2") or article.find("h3")
    link = article.find("a", href=True)
    if title and link:
        print(title.get_text(strip=True), link["href"])
```

## Rate limits

No API — web scraping only. No published rate limits; apply respectful crawl delays (1–2 seconds between requests).

## SDKs / Libraries

- **Official:** None
- **Community:** None

## Documentation

- Articles hub: https://www.gard.no/articles/
- Circulars: https://www.gard.no/circulars/
- About Gard loss prevention: https://www.gard.no/loss-prevention/

## Notes

- Gard publishes loss prevention content in multiple formats: short alerts, long-form case studies, annual reports, and regulatory circulars.
- Key recurring topics: enclosed space entry, mooring safety, fire prevention, cargo claims, collision and grounding causes, crew fatigue.
- Gard's annual H&M and P&I claims statistics provide insurer-side loss data complementary to investigation-authority reports (MAIB, NTSB).
- No confirmed RSS feed — monitor the articles page by scraping or check Gard's LinkedIn/social media for new publication announcements.
- For anonymized incident narrative data, pair with CHIRP Maritime (`chirp-maritime.md`); for investigation authority reports, use MAIB (`maib.md`) or NTSB CAROL (`ntsb-carol.md`).
- The Swedish Club (`swedish-club.md`) publishes similar insurer-perspective loss prevention data and is often cited alongside Gard in comparative analyses.
