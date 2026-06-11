# MarineTraffic Port Congestion API

Terminal- and port-level congestion data with a live congestion index, vessels-waiting counts, and rolling waiting/stay performance metrics, refreshed every 30 minutes.

**Tier:** Enterprise
**Auth:** API Key
**Last researched:** 2026-06-11

## Use cases

- Retrieving terminal-level congestion (congestion index, vessels waiting, avg waiting/stay times) for granular port reports.
- Listing port calls with vessel-level waiting, arrival and departure details for operational and dwell analysis.
- Surfacing carrier/service information operating at a terminal alongside congestion for shipping-line-specific intelligence.
- Filtering terminals by performance insights (performance index, avg waiting/stay) for benchmarking.

## Pricing

- **Free tier:** None for this product (broad MarineTraffic API is credit/subscription-based).
- **Paid tiers:** Quote-based; specific congestion-API price points not publicly listed.
- **Enterprise:** Contact sales.
- **Notes:** Part of MarineTraffic's container-tracking/port API suite. Cross-reference: MarineTraffic AIS positions are cataloged separately in `maritime-ais`; this entry is the distinct congestion/terminal product.

## Authentication

API key. Obtained via MarineTraffic account/sales; passed per documented scheme.

## Endpoints

- **Base URL:** `https://container-tracking.marinetraffic.com/`
- **Key endpoints:**
  - `GET` shipping calls — list of port calls with vessel call data including waiting times, arrival and departure details.
  - `GET` terminal congestion — list of terminals with live metrics (`congestionIndex`, `vesselsWaiting`, `vesselsWaitingAvgTime`, `vesselsStay`, `vesselsStayAvgTime`) and performance insights (`performanceIndex`, `avgWaitingTime`, `avgStayTime`); paginated 50/page.

## Example call

```bash
# Illustrative; confirm exact path/params from MarineTraffic docs on access grant
curl -H "Authorization: Bearer $MARINETRAFFIC_API_KEY" \
  "https://container-tracking.marinetraffic.com/terminal-congestions?congestionIndex=high&page=1"
```

## Rate limits

Not separately published for this product; results paginated 50 entries/page, data updated every 30 minutes. Confirm account limits with MarineTraffic.

## SDKs / Libraries

- **Official:** None language-specific; REST/JSON.
- **Community:** None notable.

## Documentation

- Main docs: https://container-tracking.marinetraffic.com/
- API reference: Same (container-tracking API docs); broader API at https://www.marinetraffic.com/en/online-services/

## Notes

- Filter groups: Performance Insights, Live Metrics, Carrier/Services Information, Related Data (port/terminal details on request).
- 30-minute refresh makes this near-real-time at terminal granularity — stronger for operational detail than daily/trend feeds like PortWatch.
- MarineTraffic is Enterprise-tier in your existing maritime-ais entry; pricing/access realities there apply here too.
