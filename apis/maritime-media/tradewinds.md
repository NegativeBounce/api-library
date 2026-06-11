# TradeWinds

Global shipping business news publication covering owners, markets, finance, and regulation, with maritime-security and sanctions reporting.

**Tier:** Freemium
**Auth:** None (some) / Subscription
**Last researched:** 2026-06-11

## Use cases

- Shipping-business and markets news (owners, S&P, finance, newbuildings) for commercial atmospherics.
- Sanctions, shadow-fleet, and regulatory coverage relevant to maritime risk.
- Cross-checking commercial context behind security/incident events.

## Pricing

- **Free tier:** Limited free articles / headlines.
- **Paid tiers:** TradeWinds subscription for full access — contact for pricing.
- **Enterprise:** Corporate/team subscriptions.
- **Notes:** Part of NHST Media Group; business-focused vs. incident-focused.

## Authentication

None for free headlines; subscription login for full articles.

## Endpoints

- **Base URL:** `https://www.tradewindsnews.com`
- **Key surfaces:**
  - Site: `https://www.tradewindsnews.com/`
  - RSS: `https://www.tradewindsnews.com/?service=rss` (verify before use)

## Example call

```bash
# Largely subscription. Verify RSS availability before integration:
#   https://www.tradewindsnews.com/
```

## Rate limits

N/A (editorial site).

## SDKs / Libraries

- **Official:** None.
- **Community:** None.

## Documentation

- Main site: https://www.tradewindsnews.com

## Notes

- Best for the **commercial/financial** dimension of maritime intelligence (who owns/charters/finances vessels) that complements security feeds.
- Mostly paywalled — useful as a subscription source rather than a free programmatic feed; verify RSS scope before relying on it.
- Cross-reference: `maritime-media/lloyds-list.md`, `vessel-registry/` for structured ownership data.
