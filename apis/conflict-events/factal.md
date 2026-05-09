# Factal

Real-time, AI-enhanced verified breaking-news and risk-intelligence platform. Combines AI event detection with experienced journalists for verification. Strong appeal for organisations that need verified events (not raw signals) for decision making.

**Tier:** Paid (with free trial; free for humanitarian organisations)
**Auth:** API Key / OAuth (Factal Edge integration)
**Last researched:** 2026-05-09

## Use cases

- Verified incident alerts for Strait of Malacca and surrounding regions — Factal verifies before alerting, reducing false-positive noise vs. raw social media feeds.
- Proximity notifications for vessels, port facilities, and personnel.
- Brand and executive monitoring (social-media and breaking-news surveillance).
- Incident chat network linking security professionals during crises.
- True Impact™ AI predicting event impact on company assets.
- Integrations with International SOS, ESRI, Everbridge.

## Pricing

- **Free tier:** 30-day free trial for qualified companies; complimentary full access for humanitarian organisations.
- **Paid tiers:** Subscription pricing scaled by seats / monitored locations / API access. Not publicly listed.
- **Enterprise:** Custom contracts for high-volume / multi-region operations.
- **Notes:** Pricing model emphasises seats over per-API-call fees.

## Authentication

API key / OAuth issued via the Factal Edge integration program. Web app uses standard SSO.

## Endpoints

- **Web app:** `https://www.factal.com/`
- **Factal Edge (integration / API):** Customer-issued endpoints; SDK distributed by Factal.
- **Surface areas:**
  - Verified event feed
  - Proximity / geofence alerts
  - Incident chat / collaboration channel
  - Mobile apps (iOS / Android)

## Example call

```bash
# Illustrative — actual endpoint provisioned per Factal Edge tenant.
curl -H "Authorization: Bearer $FACTAL_TOKEN" \
  "https://api.factal.com/v1/events?bbox=-2.0,99.0,6.0,105.5&since=2026-05-08T00:00:00Z"
```

## Rate limits

Not publicly documented.

## SDKs / Libraries

- **Official:** Mobile SDKs (iOS / Android) via Factal Edge.
- **Community:** None.

## Documentation

- Main site: https://www.factal.com/
- Solutions: https://www.factal.com/solutions/

## Notes

- Differentiator vs. Dataminr is **journalist verification** — Factal trades a few minutes of latency for substantially fewer false positives.
- Excellent fit for ops centres that experienced alert fatigue with social-media-first feeds.
- Free for humanitarian NGOs is a meaningful policy — relevant if your Strait-of-Malacca work has an NGO collaboration angle.
