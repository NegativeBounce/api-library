# SyndiGate

Global content licensing and distribution agency with primary focus on Africa, MENA, and Asia, providing licensed news from 13,000+ publications via REST Content API, RSS, FTP, Amazon Kinesis, or its DISCO search platform.

**Tier:** Paid
**Auth:** API Key / customer-provisioned credentials
**Last researched:** 2026-05-09

## Use cases

- Commercial-grade African content licensing for media platforms, databases, and corporate intelligence
- Backend feed ingestion for African news in 200+ languages with metadata enrichment
- Compliance- and rights-cleared syndication for paid B2B news products
- Aggregating Africa-specialist publications (e.g. Angolan mining trade press, ANA wire content) under a single contract

## Pricing

- **Free tier:** None
- **Paid tiers:** From **$500/month** for full-publication or subject-specific multi-publication feeds, plus one-time setup fee and minimum monthly guarantee. Video feeds from $750/month + setup
- **Enterprise:** Custom contracts; royalty-based reuse fees ($225/article print, $1/article print-out royalty, $1/article per email recipient as published in 2017 rate card)
- **Notes:** Pricing depends on premium-vs-non-premium source, format, and volume; setup fee varies by delivery method (FTP, RSS, API, Kinesis, DISCO). Public rate card is dated 2017 and indicative — contact sales for current rates.

## Authentication

API key issued by SyndiGate after contract execution. Specific auth scheme depends on delivery method (Content API uses key/token; FTP uses standard credentials; Amazon Kinesis uses AWS-style auth).

## Endpoints

- **Base URL:** Customer-specific (provisioned per contract); not a public self-serve URL
- **Key endpoints:** Documented under https://www.syndigate.info/docs/syndigate-api/ (access typically gated)
- **Delivery methods:** RSS feeds, FTP drops, Content API (REST), Amazon Kinesis stream, DISCO search platform

## Example call

```bash
# Generic shape — actual endpoint and parameters provisioned per contract
curl -H "Authorization: Bearer $SYNDIGATE_KEY" \
  "https://api.syndigate.info/v1/articles?source=allafrica&since=2026-05-01"
```

## Rate limits

Per-contract; not publicly documented.

## SDKs / Libraries

- **Official:** None published; integration handled by SyndiGate's Content Operations team during onboarding
- **Community:** None notable

## Documentation

- Main site: https://www.syndigate.info/
- API doc landing: https://www.syndigate.info/docs/syndigate-api/
- Pricing/rate card (2017, indicative): https://www.syndigate.info/pricing-rate-card-for-content-buyers/
- Licensed offering overview: https://www.syndigate.info/licensed-content-offering/

## Notes

Founded 2007 by Jordan-based Al Bawaba Group; offices in Amman, Dubai, London, Mumbai, Sydney, Tokyo. Master catalogue: 13,000+ licensed products across 195 countries / 200+ languages, with Africa as one of the four primary geographic focuses (alongside MENA, Asia, and Latin America). Useful when you need rights-cleared content (vs. RSS scraping) or coverage of niche African trade press. Example call URL above is illustrative; the real endpoint shape is provisioned per customer.
