# Dataminr Pulse

Enterprise real-time intelligence platform processing 1M+ public data sources (social media, blogs, broadcast, sensor) with multi-modal fusion AI to detect events as they emerge — often before mainstream media coverage. Subscription-only, sales-led.

**Tier:** Enterprise
**Auth:** API Key / OAuth 2.0 (issued via account team)
**Last researched:** 2026-05-09

## Use cases

- Real-time alerting on events affecting vessels, ports, and personnel near the Strait of Malacca — earthquakes, civil unrest flare-ups, port labour actions, terror incidents.
- Hyperlocal incident detection (e.g., tweets and local-language news from Belawan, Tanjung Pinang, Dumai indicating an emerging issue).
- Multi-modal fusion across text, audio, image, video, and sensor data — broader signal than text-only OSINT feeds.
- Geofence alerting on facility / vessel locations.
- Integration with security-ops platforms (Genetec, Esri, Everbridge) via Dataminr's partner ecosystem.

## Pricing

- **Free tier:** None.
- **Paid tiers:** None publicly listed.
- **Enterprise:** Custom-quoted by Dataminr account team. Pricing scales with seats, alert categories, and integrations.
- **Notes:** Procurement is sales-led; expect a 4–8 week onboarding cycle including security review.

## Authentication

API key / OAuth 2.0 token issued via the Dataminr customer success team. Scoped to a tenant.

## Endpoints

- **Public website:** `https://www.dataminr.com/`
- **API base URL:** Tenant-specific; not publicly documented.
- **Surface areas:**
  - Pulse (Corporate Security) — real-time alerts
  - Dataminr First Alert — public-sector tier
  - Webhook/integration endpoints for SIEM and physical-security platforms

## Example call

```bash
# Illustrative — actual endpoint is provisioned per tenant.
curl -H "Authorization: Bearer $DATAMINR_TOKEN" \
  "https://gateway.dataminr.com/api/v3/alerts?bbox=-2.0,99.0,6.0,105.5&since=2026-05-08T00:00:00Z"
```

## Rate limits

Not publicly documented; defined per contract.

## SDKs / Libraries

- **Official:** Customer-issued SDKs for major platforms (Java, Python, etc.).
- **Community:** None notable (closed ecosystem).

## Documentation

- Pulse product page: https://www.dataminr.com/products/pulse
- Corporate Security overview: https://www.dataminr.com/solutions/corporate-security/

## Notes

- Strongest fit when low-latency event detection is mission-critical (e.g., crew safety, executive protection, real-time port-ops oversight).
- Integration partners (Genetec, Esri, Everbridge) reduce integration burden if you already use those platforms.
- Cited by major banks, governments, and Fortune 500 corporate security teams.
- Often paired with Factal as a "two-source" verification stack.
