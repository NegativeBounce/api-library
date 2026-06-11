# Verisk CargoNet

Cargo theft and supply-chain crime intelligence platform for the U.S. and Canada, providing incident reporting, theft alerts, and recovery support.

**Tier:** Enterprise
**Auth:** Login / account (platform)
**Last researched:** 2026-06-11

> **Subscription intelligence platform, not a public self-serve API.** Data is delivered via the CargoNet platform, alerts, and reports; programmatic integration is arranged per contract.

## Use cases

- Tracking cargo theft and supply-chain crime events across the U.S. and Canada (the dominant dataset for the region — 767 supply-chain crime events in Q1 2026).
- Theft alerts and pattern analysis by geography, commodity, and method (e.g. the 2025–26 shift toward impersonation/identity-based fraud and strategic theft).
- Theft recovery support and law-enforcement coordination.
- Underwriting and loss-prevention analytics for insurers, carriers, brokers, and shippers near ports and logistics hubs.

## Pricing

- **Free tier:** None (public quarterly trend summaries are published free, but the dataset/platform is subscription).
- **Paid tiers:** Subscription to the CargoNet platform — not publicly priced.
- **Enterprise:** Bespoke data/integration, recovery services — contact Verisk.
- **Notes:** A Verisk (Nasdaq: VRSK) business. Pricing not public.

## Authentication

Platform login / subscriber credentials provisioned per contract. No documented public self-serve API; integration arranged with Verisk.

## Endpoints

- **Base URL:** No public API. CargoNet platform + alert feeds.
- **Key surfaces:**
  - Incident database (supply-chain crime events).
  - Theft alerts (push to subscribers).
  - Analytics/reporting (quarterly and annual trend reports).

## Example call

```bash
# No public self-serve API. Data and alerts delivered via the CargoNet platform;
# programmatic integration is arranged per contract with Verisk.
```

## Rate limits

N/A (platform/alerts). Per contract if a feed is provisioned.

## SDKs / Libraries

- **Official:** None publicly documented.
- **Community:** None.

## Documentation

- Main site: https://www.cargonet.com/
- Cargo theft data / reports: https://www.cargonet.com/cargo-theft-data/

## Notes

- The **authoritative cargo-theft dataset for the U.S./Canada**; widely cited in industry trend reporting. Quarterly and annual summaries are free and useful even without a subscription.
- 2026 trend signal: incident volume down slightly but losses steady (~$131.6M in Q1 2026), with organized/transnational crime and impersonation fraud rising — relevant to landside port and logistics-hub risk scoring.
- Complements waterside sources: pair with `maritime-security/imb-piracy-reporting-centre.md` (sea robbery/theft) and the global cargo-crime sources `cargo-crime/bsi-connect-screen.md` and `cargo-crime/tt-club.md`.
- Confirm whether a data feed/API integration is available for your build during sales scoping.
