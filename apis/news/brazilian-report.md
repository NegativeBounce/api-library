# The Brazilian Report

A São Paulo-based, English-language, subscription-funded news publication founded in 2017 by editor-in-chief Gustavo Ribeiro, providing daily and weekly newsletters with insider analysis on Brazilian politics, business, and society plus a Latin America Weekly briefing.

**Tier:** Paid
**Auth:** Subscription account
**Last researched:** 2026-05-09

## Use cases

- In-depth Brazilian political and economic analysis (election cycles, Bolsonaro/Lula post-government dynamics, Mercosur-EU deal, Pix, Petrobras)
- Tracking Brazilian markets, regulation, and corporate developments with English-language insider context
- Latin America weekly briefing for foreign professionals, diplomats, investors, and academics
- Augmenting Rio Times' high-volume news flow with curated, longer-form analysis

## Pricing

- **Free tier:** Limited preview content; sample newsletters
- **Paid tiers:** Premium subscription under ~$200/year (varies by promotion); includes Brazil Daily (Tue–Fri), Brazil Weekly (Mon), and Latin America Weekly (Wed) newsletters plus full website access
- **Enterprise:** Group/corporate subscriptions and custom briefing packages — contact via the publication's about page
- **Notes:** Deliberately ad-free to avoid clickbait incentives; revenue model is entirely subscription-based

## Authentication

Premium content and full newsletter archive require an active subscription account. No public developer REST API.

## Endpoints

- **Base URL:** `https://brazilian.report/`
- **Newsletter platform:** `https://newsletters.brazilian.report/`
- **Key endpoints:**
  - Main site: `https://brazilian.report/`
  - Subscription/upgrade: `https://brazilian.report/subscribe` and `https://newsletters.brazilian.report/upgrade`
  - About: `https://newsletters.brazilian.report/c/about-us`
- No documented public REST/JSON API; programmatic consumers typically use email-newsletter ingestion or contract for syndication

## Example call

```bash
# Public landing pages (free)
curl "https://brazilian.report/"
curl "https://newsletters.brazilian.report/"
```

## Rate limits

Not publicly documented.

## SDKs / Libraries

- **Official:** None for developers; iOS/Android consumer apps and YouTube channel
- **Community:** None notable

## Documentation

- Main site: https://brazilian.report/
- Newsletters: https://newsletters.brazilian.report/
- About: https://newsletters.brazilian.report/c/about-us
- Subscribe: https://brazilian.report/subscribe

## Notes

The Brazilian Report is **independent and subscription-funded** with **no advertising** model — explicitly chosen to avoid clickbait pressure. Founded 2017 in São Paulo by editor-in-chief Gustavo Ribeiro. Has won multiple international awards including: 🥇 Best Website from a small/local company at the **2024 WAN-IFRA Digital Media Awards Americas**, Best Story at the **2024 Digiday Media Awards**, Best online-only news website at the **2023 EPPY Awards**, and Best English Language Media Outlet 2023 at the Global Business Awards. Editorial team produces three flagship newsletters: Brazil Daily (Tue–Fri), Brazil Weekly (Mon), and Latin America Weekly (Wed, launched February 2021). For source-trust analysis: independent, no government affiliation, ad-free model. Cataloged here despite the absence of a true developer API because the value of insider Brazilian analysis is high enough to be worth knowing about. Programmatic consumers without a subscription will find this entry less actionable than free-RSS sources like Rio Times or MercoPress, but for institutional subscribers, the newsletter ingest is reliable and well-curated. Latin America Weekly is the cross-regional product most relevant for users wanting LatAm-wide context.
