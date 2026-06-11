# Data Docked (Maritime Insurance API)

Satellite-AIS maritime data API aimed at marine insurers, P&I clubs and underwriters, with high-risk-area / war-zone / sanctioned-region entry alerts and voyage reconstruction.

**Tier:** Freemium
**Auth:** API Key
**Last researched:** 2026-06-11

> **A true self-serve API** (unlike most of this category). Cataloged here for the war-risk exposure-monitoring use case; it is a general maritime-data API positioned for insurance.

## Use cases

- Tracking vessel entries into high-risk areas, war zones, or sanctioned regions and setting exposure-monitoring alerts.
- Verifying vessel positions for claims investigation and risk monitoring.
- Reconstructing voyages from port-call and position history for underwriting and dispute support.
- Pre-bind checks: vessel particulars, flag state, classification by IMO/MMSI/name.

## Pricing

- **Free tier:** Free trial advertised ("Start Free Trial").
- **Paid tiers:** Subscription/usage-based; specific price points not publicly listed.
- **Enterprise:** 99.9% uptime SLA; contact for higher-volume terms.
- **Notes:** Tracks 200,000+ vessels globally (per provider). Pricing details not public — confirm at signup.

## Authentication

API key. Obtain via account signup; passed per Data Docked's documented header scheme.

## Endpoints

- **Base URL:** `https://www.datadocked.com/` (API; see product docs)
- **Key endpoints (as described):**
  - Vessel position / real-time tracking by IMO, MMSI, or name.
  - High-risk-area / war-zone / sanctioned-region entry detection + alerts.
  - Port-calls by port (arrival/departure times, dwell).
  - Vessel particulars / flag / classification for pre-bind checks.

## Example call

```bash
# Illustrative; confirm exact path/headers from Data Docked API docs
curl -H "Authorization: Bearer $DATADOCKED_API_KEY" \
  "https://api.datadocked.com/v1/vessels/9811000/risk-exposure"
```

## Rate limits

Not publicly published; 99.9% uptime SLA advertised. Confirm limits at signup.

## SDKs / Libraries

- **Official:** None language-specific listed; REST/JSON.
- **Community:** None notable.

## Documentation

- Main docs: https://datadocked.com/maritime-insurance-api
- API reference: https://www.datadocked.com/api-library/ (endpoint pages, e.g. port-calls-by-port)

## Notes

- The most developer-accessible option in this category — self-serve key + free trial, vs. enterprise platforms (Concirrus, Russell) and non-API sources (JWC, Vessel Protect).
- War-zone detection depends on the zone polygons used; pair with JWC Listed Areas (`jwc-listed-areas.md`) if you need pricing-grade boundaries, since the AP economics hinge on the JWC definitions.
- Cross-reference: overlaps `maritime-ais` (positions) and `port-congestion` (port calls); kept here for the insurance/war-risk exposure framing. Avoid double-cataloging — this is its primary home for the exposure use case.
