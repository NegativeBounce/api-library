# Windward

Maritime AI platform offering vessel risk and compliance scoring, deceptive-shipping-practice detection, and behavioural analytics. Provides a GraphQL API ("API Insights Lab") and a generative AI assistant ("MAI Expert") for analyst workflows.

**Tier:** Enterprise
**Auth:** Bearer token (issued via developer portal)
**Last researched:** 2026-05-09

## Use cases

- Risk and compliance screening for vessels transiting or anchoring in the Strait — dark activity, AIS gaps, identity tampering, ID switching, port-of-call manipulation.
- Behavioural analysis flagging unusual journeys (e.g., loitering off Belawan, abnormal speed/course in TSS lanes).
- Sanctions-related risk scoring layered on top of vessel particulars.
- Multi-source intelligence fusion — Windward ingests AIS, RF (HawkEye 360 partner), satellite imagery, and proprietary signals.
- MAI Expert generative-AI Q&A over Windward's data — useful for analyst productivity in ops centres.

## Pricing

- **Free tier:** None.
- **Paid tiers:** None publicly listed.
- **Enterprise:** Custom-quoted seat-and-API pricing. Distinct SKUs for compliance/screening, ops, and government use cases.
- **Notes:** Windward serves banks, P&I clubs, government agencies, and large operators — pricing is enterprise-grade.

## Authentication

Bearer token issued via the Windward developer portal. GraphQL API uses HTTP `Authorization: Bearer <token>` header.

## Endpoints

- **Developer portal:** `https://developer.windward.ai/`
- **GraphQL endpoint:** Issued per customer (typically `https://api.windward.ai/graphql`).
- **Surface areas (GraphQL resolvers):**
  - `vessels` — particulars + risk score
  - `journeys` — historical voyage history
  - `risk_assessments` — composite risk
  - `deceptive_activities` — flagged events (AIS gaps, identity tampering, etc.)
  - `companies` — beneficial ownership graph

## Example call

```bash
# Illustrative — actual endpoint and token come from the Windward developer portal.
curl -X POST "https://api.windward.ai/graphql" \
  -H "Authorization: Bearer $WW_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"query":"{ vessels(imo: \"9525338\") { name riskScore deceptiveActivities { type startTime } } }"}'
```

## Rate limits

Not publicly documented.

## SDKs / Libraries

- **Official:** None published; GraphQL is consumed via standard HTTP clients.
- **Community:** None notable.

## Documentation

- Developer portal: https://developer.windward.ai/
- GraphQL intro: https://developer.windward.ai/reference/what-is-graphql
- Main site: https://windward.ai/

## Notes

- Windward is the de-facto maritime AI/risk leader for compliance use cases — banks and KYC functions are the primary customer base.
- For Strait of Malacca monitoring specifically, Windward is best paired with a real-time AIS feed (Spire / MarineTraffic) and an RF feed (HawkEye 360) to maximise dark-activity detection.
- MAI Expert generative AI is built on top of Windward's curated graph — useful for natural-language analyst queries but not a substitute for the underlying data.
