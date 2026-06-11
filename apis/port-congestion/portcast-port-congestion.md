# Portcast Port Congestion API

On-demand congestion data for over 1,000 ports worldwide, returning daily and weekly vessel waiting/dwell metrics with categorized congestion severity labels.

**Tier:** Paid
**Auth:** API Key
**Last researched:** 2026-06-11

## Use cases

- Pulling structured daily congestion metrics (vessels berthed, vessels waiting, total waiting time) per port by UN/LOCODE for automated report generation.
- Using weekly percentile analytics (median/mean/upper-range of waiting and dwell) to quantify delay risk for a shipping or insurance client.
- Driving automation off the LOW / MEDIUM / HIGH / LONG-TAIL congestion category labels.
- Comparing live congestion against a 365-day rolling average to flag abnormal conditions.

## Pricing

- **Free tier:** None published.
- **Paid tiers:** Subscription/quote-based; not publicly listed.
- **Enterprise:** Contact sales.
- **Notes:** Pricing obtained via sales. API is positioned as an add-on to Portcast's congestion dashboard and predictive ETA platform.

## Authentication

API key. Obtain credentials by registering with Portcast and requesting API access. Key passed per Portcast's documented header scheme at onboarding.

## Endpoints

- **Base URL:** Not publicly documented (provided on API access grant).
- **Key endpoints:**
  - Port congestion query — input: port UN/LOCODE + optional date range; output: JSON with daily metrics, weekly analytics, congestion category, and port metadata (coordinates).

## Example call

```bash
# Illustrative; confirm exact base URL and header on access grant
curl -H "Authorization: Bearer $PORTCAST_API_KEY" \
  "https://api.portcast.io/port-congestion?unlocode=SGSIN&from=2026-06-01&to=2026-06-10"
```

## Rate limits

Not publicly published. Designed for on-demand retrieval into TMS/planning tools; confirm limits with Portcast.

## SDKs / Libraries

- **Official:** None publicly listed; REST/JSON, integrates with TMS and internal dashboards.
- **Community:** None notable.

## Documentation

- Main docs: https://www.portcast.io/ (Port Congestion API product page and blog)
- API reference: Provided on API access grant (not public).

## Notes

- Coverage stated at 1,000+ ports; metrics computed from AIS signals + live port calls + historical trends, with waiting measured from anchorage arrival to berth.
- Strong fit where you want clean, labeled congestion data without building your own AIS-derivation layer.
- Base URL and exact auth header are not in public docs — marked accordingly rather than guessed.
