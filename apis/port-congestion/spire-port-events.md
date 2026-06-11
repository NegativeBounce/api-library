# Spire Port Events

AIS-derived smart-data feed that detects vessel arrival, departure, anchorage and canal events across ports, terminals and chokepoints, with a derived Port Congestion Index.

**Tier:** Enterprise
**Auth:** OAuth 2.0 / API Key
**Last researched:** 2026-06-11

> ⚠️ **Acquisition notice (2026):** Spire Maritime was acquired by Kpler. As of early 2026 the standalone Spire Maritime APIs (including Port Events) are being discontinued and migrated to Kpler's maritime data platform. New integrations should target `developers.kpler.com`; existing customers should contact Kpler for migration. Entry retained because the underlying Port Events capability persists under Kpler.

## Use cases

- Computing port congestion from vessel time-in-port plus voyage data, with anchorage vs. berth distinction.
- Tracking granular arrival/departure/anchorage/canal events for individual vessels or whole areas to feed custom congestion and ETA models.
- Detecting probable loading/unloading via draught changes at terminal departure for cargo-flow intelligence.
- Monitoring chokepoint/canal transits (e.g. Suez) as part of regional disruption reporting.

## Pricing

- **Free tier:** None.
- **Paid tiers:** Packaged tiers; pricing not publicly listed.
- **Enterprise:** Contact sales (now via Kpler).
- **Notes:** Historically quote-based by data volume/coverage. Post-acquisition pricing flows through Kpler commercial terms.

## Authentication

OAuth 2.0 / API key (token-based) against Spire's GraphQL endpoint historically; Kpler-migrated access uses Kpler-issued credentials. Confirm current scheme with Kpler at onboarding.

## Endpoints

- **Base URL:** `https://api.spire.com/graphql` (legacy Spire Maritime 2.0 GraphQL; single endpoint)
- **Key endpoints:**
  - GraphQL `port events` query — arrival/departure/anchorage/terminal/canal events filterable by location, ship type, individual vessel (IMO/MMSI), arrival/departure dates.
  - GraphQL `vessels` query — static + voyage data including `matchedPort`, destination, draught, ETA.

## Example call

```bash
curl -X POST "https://api.spire.com/graphql" \
  -H "Authorization: Bearer $SPIRE_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"query":"{ vessels(imo:[9282742]){ nodes { staticData { imo mmsi } currentVoyage { destination draught eta matchedPort { matchScore port { unlocode name } } } } } }"}'
```

## Rate limits

Not publicly published; governed by contract tier. GraphQL subscriptions available historically for streaming events.

## SDKs / Libraries

- **Official:** GraphQL schema serves as live documentation; any GraphQL client works. Kpler provides its own SDKs/clients post-migration.
- **Community:** Standard GraphQL libraries (Apollo, gql, graphql-request).

## Documentation

- Main docs: https://developers.kpler.com (current); legacy at https://documentation.spire.com/maritime-2-0/
- API reference: https://documentation.spire.com/maritime-2-0/#port-events (legacy reference)

## Notes

- Spire is also cataloged in `maritime-ais` (raw AIS positions). This entry covers the distinct **Port Events / congestion** derived product.
- Combines Satellite AIS, Terrestrial AIS, and Enhanced Vessel AIS for coverage; anchorage events use speed/heading/destination heuristics rather than geofence-only detection.
- Because of the Kpler migration, verify endpoint, auth, and product availability directly before building — the legacy Spire endpoints may sunset.
