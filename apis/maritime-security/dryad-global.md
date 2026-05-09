# Dryad Global

Maritime risk intelligence platform offering real-time incident reporting, vessel tracking, geofence alerting, and historical analysis through the Secure Voyager Hub portal — and an actual REST API (Stream Voyager) for organisations that need to embed Dryad's curated intelligence into their own pipelines.

**Tier:** Enterprise (Stream Voyager API); Freemium-style for Channel 16 blog content
**Auth:** API Key / OAuth (Stream Voyager); login (Secure Voyager Hub)
**Last researched:** 2026-05-09

## Use cases

- Real-time piracy / armed-robbery / hijacking incident feed for the Strait of Malacca and Singapore Strait, layered with contextual analysis.
- Geofence alerting around high-risk anchorages (e.g., off Belawan, Bintan, Outer Port Limit anchorages in the Singapore Strait).
- AIS-fused vessel tracking with risk overlays — a one-stop dashboard for ops centres.
- Stream Voyager API integration for piping incidents into enterprise monitoring tools, SIEMs, or custom dashboards.
- Historical analysis (15+ years of incident data) for pattern-of-life, route-risk scoring, and underwriter modelling.
- Maritime cyber security advisories.

## Pricing

- **Free tier:** Channel 16 blog (free analysis articles) and a Secure Voyager Hub free trial.
- **Paid tiers:** Secure Voyager Hub portal subscriptions (Basic / Standard / Enterprise) — exact prices listed publicly only as placeholders; contact for quote.
- **Enterprise:** Stream Voyager API access bundled into Enterprise contracts. Volume-based pricing.
- **Notes:** Pricing model is sales-led; expect a procurement cycle similar to Kpler/MarineTraffic.

## Authentication

Secure Voyager Hub: username/password via secure.dryadglobal.com.
Stream Voyager API: API key / OAuth credentials issued by Dryad after Enterprise subscription.

## Endpoints

- **Portal login:** `https://secure.dryadglobal.com/`
- **Account management:** `https://account.dryadglobal.com/`
- **Stream Voyager API base URL:** Issued per customer (not public).
- **Surface areas:**
  - Incident feed (real-time + historical)
  - Geofence alert endpoints (vessel enters/exits high-risk zone)
  - Vessel tracking (SAT-AIS fused)
  - NAVTEX/EGC visualisations
  - Maritime regulation lookup (MPAs, ECAs, restricted areas)

## Example call

```bash
# Illustrative — exact endpoint paths require Stream Voyager onboarding.
curl -H "Authorization: Bearer $DRYAD_TOKEN" \
  "https://api.dryadglobal.com/v1/incidents?bbox=-2.0,99.0,6.0,105.5&since=2026-04-01"
```

## Rate limits

Not publicly documented; defined per Enterprise contract.

## SDKs / Libraries

- **Official:** None publicly distributed (Stream Voyager is a REST API; client integration is bespoke).
- **Community:** None.

## Documentation

- Main site: https://www.dryadglobal.com/
- Risk Intelligence System: https://www.dryadglobal.com/risk-intelligence-system
- Pricing page: https://www.dryadglobal.com/pricing-and-packages
- Channel 16 (free analysis): https://channel16.dryadglobal.com/

## Notes

- Dryad is one of the few maritime security shops that explicitly markets an API (Stream Voyager) — most competitors deliver via PDF and portal only.
- Strong analyst bench; their geopolitical context layered on top of incident data is a differentiator vs. raw feeds.
- For Strait of Malacca specifically, Dryad ingests ReCAAP and IMB sources plus their own analyst input — useful as a "fusion" layer.
- Sometimes branded "Dryad Maritime" historically; rebrand to Dryad Global is current.
