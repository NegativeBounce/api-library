# Slingshot Beacon (Slingshot Aerospace Platform)

Slingshot Aerospace's unified space domain awareness platform. Beacon is the conjunction-coordination product; the broader platform also includes Seradata (satellite/launch database with 50,000+ records), Agatha AI (anomaly detection), TALOS AI (maneuver planning), Digital Space Twin, PNT-SA (GNSS interference), and a developer API hub.

**Tier:** Enterprise (operator + government subscriptions)
**Auth:** API key + RBAC permissions
**Last researched:** 2026-05-09

## Use cases

- Conjunction coordination — ingest CDMs (incl. from Space-Track) + user ephemerides, set risk thresholds, alert + coordinate with secondaries
- Operator-to-operator messaging during close-approach events (real-time chat in Beacon)
- Sovereign Space Object Tracking (SSOT) — nations can deploy independent SDA capability via Slingshot sensors + software
- Pattern-of-life analytics — detect maneuvers, station-keeping changes, mission-phase transitions
- Maneuver planning + decision support (TALOS AI)
- Anomaly detection across constellations (Agatha AI)
- Historical mission/launch context + reliability data (Seradata)

## Pricing

- **Free tier:** None published. Slingshot Laboratory (educational orbital sandbox) has free access for learning.
- **Paid tiers:** Subscription-based across product lines; quoted per deployment.
- **Enterprise:** Standard model. Government and defense plans support classified/secure environments.
- **Notes:** Acquired Numerica Space and Seradata in 2022, consolidating into one platform. Sensor network: 220+ sensors across 22 sites (Varda gimbaled EO, Horus LEO array, Argus GEO array).

## Authentication

API keys + RBAC permissions issued per account in the Developer Docs portal. Tiered data environments (sandbox vs. production). MCP Insights Server in development for AI-agent integration.

## Endpoints

- **Base URL:** `https://api.slingshot.space` (per-product subdomains may apply)
- **Key product APIs:**
  - **Beacon API** — CDM ingest/filter, ephemeris upload, maneuver-plan sharing, secondary-operator messaging
  - **SGSN Data API** — Slingshot Global Sensor Network observations + state vectors
  - **SSOT API** — Sovereign Space Object Tracking data layer
  - **MCP Insights Server** (coming soon) — AI-agent connector for orbital analytics
  - **Seradata API** — 50,000+ spacecraft records, mission/operator/financial metadata
  - **Agatha AI / TALOS AI** — anomaly detection + maneuver recommendation pipelines

## Example call

No public sample documented outside customer portals. After provisioning, the developer docs at `slingshot.space/product-developer-docs` provide sandbox endpoints + endpoint reference. Pattern is REST + JSON with API-key header auth.

```bash
# Illustrative pattern (customer-specific endpoints)
curl "https://api.slingshot.space/v1/cdm/recent?since=2026-05-09T00:00:00Z" \
  -H "Authorization: Bearer $SLINGSHOT_API_KEY"
```

## Rate limits

Per-subscription tier; sandbox vs. production tiers have different caps. Specific numbers in customer portal.

## SDKs / Libraries

- **Official:** Developer Docs hub, sandbox environment, embeddable Beacon UI components.
- **Community:** Limited public ecosystem (mostly customer integrations).

## Documentation

- Platform overview: https://www.slingshot.space/platform
- Beacon product page: https://www.slingshot.space/product-beacon
- Developer Docs: https://www.slingshot.space/product-developer-docs
- Data & insights: https://www.slingshot.space/solutions/data-insights
- Government/defense: https://www.slingshot.space/solutions-government-and-defense
- Seradata: https://www.slingshot.space/product-seradata

## Notes

- Sensor network is electro-optical (vs. LeoLabs' radar) — strengths in GEO + xGEO daytime + nighttime tracking; complementary to LeoLabs in LEO.
- Beacon is one of the few neutral conjunction-coordination platforms operators of competing constellations actively share data on.
- PNT-SA (positioning, navigation, timing — situational awareness) detects GPS jamming/spoofing using GNSS receivers on satellites and ground; cross-listing applies to `gnss-interference`.
- Cross-listing: significant overlap with `gnss-interference` (PNT-SA), `satellite-imagery` (electro-optical sensors), and `rf-monitoring` (radio frequency signal insights are an advertised data product).
- Seradata is itself a useful standalone reference; cross-listing applies to `geopolitical-risk` (operator/country attribution for any satellite).
