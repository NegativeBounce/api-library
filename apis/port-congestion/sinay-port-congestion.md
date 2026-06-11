# Sinay Port Congestion API

Real-time worldwide port congestion status with a meaningful free tier, filterable by vessel type and comparable against each port's average congestion.

**Tier:** Freemium
**Auth:** API Key
**Last researched:** 2026-06-11

## Use cases

- Prototyping congestion features against a free tier before committing to a paid plan.
- Retrieving real-time port congestion status worldwide and filtering by vessel type/characteristics for persona-specific reports.
- Comparing a port's current congestion against its own historical average to contextualize severity.
- Feeding congestion signals into port-call optimization and ETA-adjustment logic.

## Pricing

- **Free tier:** 100 API calls/month, no credit card required (trial on the developer platform).
- **Paid tiers:** Subscription-based, usage-priced ("pay for what you use"); specific price points not publicly listed.
- **Enterprise:** Contact sales.
- **Notes:** Part of Sinay's broader maritime API hub (also offers vessel tracking, emissions, ETA, weather APIs). Stated implementation time under half a day.

## Authentication

API key generated on the Sinay developer platform. Passed per Sinay's documented header scheme. Sign up for a free account to obtain the key.

## Endpoints

- **Base URL:** `https://api.sinay.ai` (Port Congestion API under the Sinay hub)
- **Key endpoints:**
  - Port congestion status query — real-time congestion by port, filterable by vessel type; comparison to port average congestion.

## Example call

```bash
# Illustrative; confirm exact path from Swagger/Postman on the developer platform
curl -H "API-Key: $SINAY_API_KEY" \
  "https://api.sinay.ai/port-congestion/v1/status?port=SGSIN&vesselType=container"
```

## Rate limits

10 calls per minute (published). Free tier capped at 100 calls/month.

## SDKs / Libraries

- **Official:** Swagger collection and Postman collection provided; no language-specific SDK required.
- **Community:** None notable.

## Documentation

- Main docs: https://sinay.ai/en/sinay-hub/port-congestion-api/
- API reference: Swagger at https://api.sinay.ai/doc/ and Postman collection (https://www.postman.com/sinayapi)

## Notes

- Metrics are AIS-derived; some indicators are averages/snapshots and methodology can vary by port based on data quality.
- Good developer experience (Swagger + Postman, free trial) makes this a low-friction option for early integration.
- Sinay's sister products (Safecube schedule/container APIs) overlap on schedules but are a distinct product line.
