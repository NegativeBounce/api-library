# GoComet Port Congestion API

Port congestion tracker delivering a median congestion index across 400+ major seaports, derived from analysis of containerized shipment movements and on-ground delays.

**Tier:** Paid
**Auth:** API Key
**Last researched:** 2026-06-11

## Use cases

- Integrating a port congestion index into an ERP or internal dashboard for shipping/logistics clients.
- Reporting real on-ground delays (proximity/anchorage time plus container gate-out time) rather than AIS-position-only estimates.
- Monitoring congestion across US, EU, EMEA and SEA port coverage for regional intelligence summaries.

## Pricing

- **Free tier:** None published.
- **Paid tiers:** Subscription/quote-based; not publicly listed.
- **Enterprise:** Contact sales.
- **Notes:** Positioned as part of GoComet's logistics-intelligence suite; congestion API integrates with client ERP systems and supports building a custom interface from the pulled data.

## Authentication

API key. Obtain via GoComet account/sales onboarding; passed per documented header scheme.

## Endpoints

- **Base URL:** Not publicly documented (provided on access grant).
- **Key endpoints:**
  - Port congestion query — returns median congestion index per port; integrable with client ERP for custom interfaces.

## Example call

```bash
# Illustrative; confirm exact base URL and header on access grant
curl -H "Authorization: Bearer $GOCOMET_API_KEY" \
  "https://api.gocomet.com/port-congestion?port=USLAX"
```

## Rate limits

Not publicly published. Confirm with GoComet at onboarding.

## SDKs / Libraries

- **Official:** None publicly listed; REST/JSON with ERP integration support.
- **Community:** None notable.

## Documentation

- Main docs: https://www.gocomet.com/real-time-port-congestion
- API reference: Provided on access grant (not public).

## Notes

- Delay logic accounts for vessel time in proximity/anchorage/queue plus container gate-out time, aiming to reflect real delays over modeled estimates.
- Coverage ~400+ ports, analyzing 45,000+ containerized shipments/month; congestion index reported as a median (outliers excluded).
- Base URL/auth header not in public docs — marked accordingly rather than guessed.
