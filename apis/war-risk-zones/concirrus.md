# Concirrus

AI-driven marine insurtech platform (Quest / Marine One) providing behavioural risk benchmarking, vessel timelines, sanctions compliance and war-zone exposure analytics for underwriters.

**Tier:** Enterprise
**Auth:** API Key / platform (integration available)
**Last researched:** 2026-06-11

> **Platform-first.** Concirrus is primarily a SaaS underwriting platform; data/integration into customer or London Market systems is available but commercial-contract gated, not a self-serve public API.

## Use cases

- Quantifying vessel and voyage war-risk exposure using behavioural analytics (route deviation, port visits, AIS patterns) rather than demographics alone.
- Integrated sanctions compliance and AI news/vessel-timeline feeds for war-risk and compliance workflows.
- Risk aggregation across hull, cargo and liability portfolios for war/peril exposure modelling.
- Automating underwriting submissions with London Market platform integration.

## Pricing

- **Free tier:** None.
- **Paid tiers:** Subscription/contract.
- **Enterprise:** Contact sales.
- **Notes:** Pricing not public. Products: Quest platform and "Marine One" (97% submission accuracy across hull/cargo/liability). Algorithms tap 20+ industry-specific datasets blended with AIS.

## Authentication

Platform login; API/integration credentials provisioned per contract for data flow into customer or London Market systems.

## Endpoints

- **Base URL:** Provided on contract (see concirrus.ai/marine).
- **Key capabilities:**
  - Vessel timeline + behavioural risk scoring.
  - Sanctions/compliance checks.
  - Risk aggregation/exposure for hull/cargo/liability.
  - London Market platform integration for submission/data flow.

## Example call

```bash
# No public self-serve API. Integration/credentials provided per contract.
# Capabilities accessed via the Quest / Marine One platform and contracted data feeds.
```

## Rate limits

Per contract; not publicly published.

## SDKs / Libraries

- **Official:** Integration support provided during onboarding; no public SDK.
- **Community:** None.

## Documentation

- Main docs: https://concirrus.ai/marine/
- API reference: Provided on contract.

## Notes

- Strong fit for the insurance/war-risk-broker personas: this is what underwriters actually use to price marine/war risk.
- Differentiator is behavioural risk modelling ("behaviour is a better indicator of risk than demographics") on the largest commercial marine policy/claims dataset.
- For raw zone definitions use JWC; Concirrus is the analytics/pricing layer on top of vessel behaviour and exposure.
- Confirm whether a data API (vs. platform-only) is offered for your use case during sales scoping.
