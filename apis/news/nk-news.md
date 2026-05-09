# NK News

Independent specialist publication (Korea Risk Group / NK Consulting Inc., founded 2010) focused entirely on North Korea (DPRK), providing subscription-based news, analysis, podcasts, and the NK Pro research platform with leadership/ship/aviation trackers.

**Tier:** Paid
**Auth:** Subscription account (no public developer REST API)
**Last researched:** 2026-05-09

## Use cases

- North Korea-specific intelligence, analysis, and primary-source reporting (no real alternatives)
- DPRK leadership tracking, ship and aviation movements, and KCNA media monitoring (via NK Pro)
- Korean Peninsula sanctions and security analysis for governments, think tanks, and academics
- Augmenting global news APIs with the only dedicated DPRK English-language outlet

## Pricing

- **Free tier:** Limited free articles per month before paywall; KCNA Watch (sister site) is free
- **Paid tiers:** NK News membership ~$3.84/week (annual) or higher monthly rates; mobile app reports ~$29.99/month or ~$299.99/year
- **Enterprise:** NK Pro for professionals — research tools, databases, leadership tracker, ship tracker, aviation tracker, leading indicators; institutional pricing on request
- **Notes:** Funded almost entirely through user subscriptions. Content syndication agreement with The Guardian since 2014.

## Authentication

NK News and NK Pro both require an active subscription account. Web/app login; no public developer REST API. RSS feeds exist but are primarily subscriber-facing.

## Endpoints

- **Base URL:** `https://www.nknews.org/`
- **Key endpoints:**
  - Main site: `https://www.nknews.org/`
  - NK Pro platform: `https://www.nknews.org/pro/`
  - KCNA Watch (free sister site): `https://kcnawatch.org/`
- No public, documented developer API. Programmatic consumers typically use subscriber RSS feeds or content syndication via The Guardian.

## Example call

```bash
# Marketing/landing pages are public
curl "https://www.nknews.org/"

# KCNA Watch is freely accessible (no subscription)
curl "https://kcnawatch.org/"
```

## Rate limits

Not publicly documented.

## SDKs / Libraries

- **Official:** iOS and Android apps for subscribers; no developer SDKs
- **Community:** None notable

## Documentation

- Main site: https://www.nknews.org/
- Subscription info: https://signup.nknews.org/
- FAQ: https://www.nknews.org/frequently-asked-questions-about-nk-news/
- KCNA Watch (free): https://kcnawatch.org/

## Notes

The only English-language specialist publication focused entirely on the DPRK. Sister site KCNA Watch provides free archive and live-stream access to Korean Central Television. NK Pro's research databases (leadership tracker, ship tracker, aviation tracker, leading indicators) are unique — no real competitor exists. Important caveat: this is a subscription product, not a true developer API. Cataloged here because the value of DPRK-specialist content is high enough that it's worth knowing about even without a public dev API. The publication's editorial stance is widely regarded as evidence-based and critical of the DPRK regime.
