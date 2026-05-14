# OCEANS-X (MPA Singapore)

Singapore Maritime and Port Authority's new maritime data and API exchange platform — launched April 2026 at Singapore Maritime Week with 100+ APIs and datasets covering port clearance, ship compliance certificates, green shipping corridor data exchange, and public maritime datasets for research.

**Tier:** Freemium
**Auth:** Registration (free)
**Last researched:** 2026-05-13

## Use cases

- Integrating shipping company or agent systems directly with MPA's digitalPORT@SG platform to submit port clearance applications programmatically via API
- Exchanging ISM, ISPS, and MLC compliance certificate data between ship managers, classification societies, and flag state administrations through a standardized interface
- Accessing public maritime datasets from the Port of Singapore for research, analytics, and innovation projects

## Pricing

- **Free tier:** Public maritime datasets accessible with free registration; no cost for qualifying research and innovation use cases
- **Paid tiers:** Operational API access (port clearance, compliance data) may require active commercial relationship with MPA or partner status — contact MPA for terms
- **Enterprise:** G2B (Government-to-Business) and G2G (Government-to-Government) integration agreements available; contact MPA for enterprise onboarding
- **Notes:** OCEANS-X is opt-in infrastructure — MPA is building incentives for adoption rather than mandating compliance timelines. The platform launched April 21, 2026 and is actively expanding its API catalog.

## Authentication

Register at `https://go.gov.sg/OCEANS-X` for platform access. Authentication credentials and API documentation are provided post-registration. Contact MPA at https://www.mpa.gov.sg for registration queries.

## Endpoints

- **Platform access:** `https://go.gov.sg/OCEANS-X`
- **MPA main page:** `https://www.mpa.gov.sg/finance-e-services/oceans-x`
- **Available API categories (100+ total):**
  - **Port Clearance as a Service** — integrate with digitalPORT@SG™ to submit arrival/departure clearance applications; direct system-to-system connectivity replacing manual port agent processes
  - **Ship Certificate Exchange** — ISM, ISPS, and MLC 2006 compliance data exchange between ship managers, class societies, and flag state administrations
  - **Green and Digital Shipping Corridor** — data exchange APIs supporting green shipping corridor initiatives (Singapore–Rotterdam, Singapore–Los Angeles corridors)
  - **Public Maritime Datasets** — vessel traffic statistics, port call data, and maritime operational data for research and innovation
- **API documentation:** Available post-registration via the OCEANS-X portal

## Example call

```python
# Registration required before API access — example flow post-registration
import requests

# Port clearance submission (example structure — exact endpoints post-registration)
resp = requests.post(
    "https://api.oceansxplatform.gov.sg/port-clearance/v1/arrivals",  # indicative URL
    headers={
        "Authorization": f"Bearer {OCEANS_X_TOKEN}",
        "Content-Type": "application/json",
    },
    json={
        "vesselIMO": "9876543",
        "vesselName": "MV EXAMPLE",
        "ETA": "2026-05-15T08:00:00Z",
        "portOfCall": "SGSIN",
        "agentCode": "AGENT001",
    },
)
print(resp.json())
```

## Rate limits

Not publicly documented pre-registration. Contact MPA or check the OCEANS-X developer documentation post-registration for applicable rate limits per API category.

## SDKs / Libraries

- **Official:** None confirmed — REST API; documentation available via portal post-registration
- **Community:** None yet — platform launched April 2026; community tooling expected to develop over time

## Documentation

- OCEANS-X platform access: https://go.gov.sg/OCEANS-X
- MPA OCEANS-X page: https://www.mpa.gov.sg/finance-e-services/oceans-x
- Launch announcement: https://www.mpa.gov.sg/media-centre/details/singapore-launches-oceans-x-to-advance-maritime-digital-connectivity-and-support-global-trade-flows
- Maritime Gateway coverage: https://www.maritimegateway.com/singapore-launches-oceans-x-to-digitise-maritime-connectivity/

## Notes

- OCEANS-X stands for Open/Common Exchange And Network Standardisation-eXchange — the name signals its role as a standardized interoperability layer for the maritime ecosystem.
- The Port of Singapore is the world's second-busiest container port by TEU; OCEANS-X's port clearance APIs directly digitize one of the most operationally significant maritime administrative workflows.
- Ship managers connecting via OCEANS-X can eliminate manual port clearance submissions for Singapore port calls — replacing agent-mediated paper or email processes with direct system-to-system API calls.
- Green and Digital Shipping Corridor APIs support Singapore's bilateral agreements with Rotterdam, Los Angeles, and other major ports to streamline documentation for vessels on green shipping routes.
- Public dataset access is specifically intended for academia, startups, and researchers — making Singapore port traffic data available for analysis without commercial agreements.
- For port OT security specifically: OCEANS-X is more relevant as a port operations data source than a cybersecurity telemetry API; combine with OT monitoring platforms (Nozomi, Claroty, Dragos) for a complete port digital security picture.
- As of 2026-05-13 the platform was newly launched (April 2026) — API catalog and documentation are expanding; check the portal regularly for new API additions.
