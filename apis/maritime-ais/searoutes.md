# Searoutes

Combined terrestrial + satellite AIS API with intelligent route optimization (canal/strait-aware), vessel tracking, and historical traces — powered in part by a LuxSpace satellite AIS partnership.

**Tier:** Freemium
**Auth:** API Key
**Last researched:** 2026-06-11

## Use cases

- Vessel tracking using both terrestrial and satellite AIS (better blue-water coverage than terrestrial-only feeds).
- Route optimization that accounts for canal/strait speeds and vessel-specific routing — useful for ETA and transit-cost modelling.
- Pulling a vessel's historical trace between two dates with average speed and route characteristics, for analytics and risk scoring.
- CO2/emissions and distance calculations along realistic sea routes.

## Pricing

- **Free tier:** Free tier / trial available (API keys self-service).
- **Paid tiers:** Usage-based plans by request volume (specific price points not publicly fixed).
- **Enterprise:** Higher-volume / SLA plans on request.
- **Notes:** 99.9% uptime advertised; AIS updates every ~5 minutes; historical data spans 5+ years with gap-filling and noise reduction.

## Authentication

API key via the `x-api-key` header (per Searoutes docs). Self-service key provisioning.

## Endpoints

- **Base URL:** `https://api.searoutes.com/`
- **Key endpoints:**
  - Route API — optimized sea routes between points/ports (canal- and strait-aware).
  - Vessel API — current position and metadata by IMO/MMSI.
  - Historical trace — vessel track between two dates with speed/route characteristics.
  - Distance / CO2 calculation along routes.

## Example call

```bash
# Illustrative; confirm exact path/params from Searoutes docs
curl -H "x-api-key: $SEAROUTES_KEY" \
  "https://api.searoutes.com/vessel/v2/567894/trace?fromDate=2026-05-01&toDate=2026-05-10"
```

## Rate limits

Plan-dependent; not publicly tabulated. Status page: https://status.searoutes.com/

## SDKs / Libraries

- **Official:** REST/JSON; no language-specific SDK widely advertised.
- **Community:** None notable.

## Documentation

- Main docs: https://searoutes.com/vessel-api/
- API reference: https://developer.searoutes.com/

## Notes

- The **route-optimization** layer (canal/strait/vessel-specific) differentiates Searoutes from pure position feeds — strong for ETA and voyage-cost estimation across chokepoints.
- Satellite + terrestrial blend (LuxSpace) gives broader coverage than terrestrial-only providers without full enterprise satellite pricing.
- Cross-reference: for pure satellite constellation depth see Kpler/Spire (`maritime-ais/spire-maritime.md`); for route/ETA in container shipping see Portcast (`port-congestion/portcast-port-congestion.md`).
