# Tenable OT Security

OT vulnerability management and asset inventory platform (formerly Indegy) using a GraphQL API for flexible data queries — providing CVE-mapped vulnerability data, OT asset discovery, and event monitoring for industrial control system environments including ports and terminals.

**Tier:** Enterprise
**Auth:** API Key
**Last researched:** 2026-05-13

## Use cases

- Querying OT asset inventory and CVE-mapped vulnerability data for all industrial devices detected across port network segments using flexible GraphQL queries
- Exporting vulnerability and asset data for integration with vulnerability management workflows, patch prioritization systems, and CMDB platforms
- Monitoring OT security events and alerts for port control systems via the GraphQL events API

## Pricing

- **Free tier:** None — enterprise licensing only; part of the Tenable One platform or standalone Tenable OT Security license
- **Paid tiers:** Quote-based pricing; typically licensed per asset count; contact Tenable for pricing
- **Enterprise:** Tenable One unified exposure management platform bundles OT Security with Tenable.io and other products; contact https://www.tenable.com
- **Notes:** Pricing is not publicly listed; contact Tenable sales or an authorized reseller for quotes. Academic and government pricing may be available.

## Authentication

Generate an API key within the Tenable OT Security console. Navigate to: Settings → User Management → select user → API Key → Generate Key. Pass as `Authorization: <API_KEY>` header on all GraphQL requests.

## Endpoints

- **API type:** GraphQL (not REST) — single endpoint for all data queries
- **GraphQL endpoint:** `https://<tenable-ot-server>/graphql`
- **No separate REST endpoints** — all data is retrieved via GraphQL queries against the single `/graphql` endpoint
- **Interactive tool:** GraphiQL Playground accessible within the Tenable OT Security web interface for building and testing queries
- **Key GraphQL object types:**
  - `assets` — OT device inventory (IP, MAC, vendor, model, firmware, protocols)
  - `events` — security events and detections
  - `exports` — bulk data export operations
  - `plugins` — vulnerability plugin definitions and CVE mappings

**Note:** Official support for the GraphQL API is described as "still evolving" — the `pyTenable` library (`TenableOT` class) is the recommended integration path as it abstracts API changes.

## Example call

```bash
# GraphQL query for OT assets
curl -X POST \
  -H "Authorization: $TENABLE_OT_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"query": "{ assets { nodes { id name ipAddresses vendor model firmware riskScore } } }"}' \
  "https://tenable-ot.port.example.com/graphql"
```

```python
from tenable.ot import TenableOT

# Connect using pyTenable
ot = TenableOT(
    url="https://tenable-ot.port.example.com",
    api_key=TENABLE_OT_API_KEY,
)

# Get all OT assets
for asset in ot.assets.list():
    print(asset["name"], asset.get("ipAddresses"), asset.get("riskScore"))

# Get vulnerability data
for vuln in ot.vulns.list():
    print(vuln.get("cveId"), vuln.get("cvssScore"), vuln.get("assetCount"))

# Direct GraphQL query (low-level)
result = ot.graphql(
    query="""
    {
      assets(filter: {riskScore: {gt: 7}}) {
        nodes {
          id
          name
          ipAddresses
          vendor
          riskScore
        }
      }
    }
    """
)
```

## Rate limits

Not publicly documented. GraphQL queries against the on-premise appliance are bounded by hardware capacity. Use the `pyTenable` client library for automatic retry and backoff handling.

## SDKs / Libraries

- **Official:** `pyTenable` (Python, PyPI — `pip install pytenable`; `TenableOT` class); official GitHub: tenable/pyTenable
- **Community:** GraphiQL Playground (built into Tenable OT Security web UI for interactive queries); example queries in pyTenable GitHub repository

## Documentation

- OT Security API integration: https://developer.tenable.com/docs/ot-integrations
- pyTenable TenableOT reference: https://pytenable.readthedocs.io/en/stable/api/ot/index.html
- OT Security documentation: https://docs.tenable.com/OT-security.htm
- 2026 release notes: https://docs.tenable.com/release-notes/Content/OT-security/2026.htm
- Developer portal: https://developer.tenable.com/reference/navigate

## Notes

- Tenable OT Security uses GraphQL rather than REST — all data retrieval goes through the single `/graphql` endpoint using typed queries; this is unusual among OT security platforms and requires familiarity with GraphQL syntax.
- The GraphiQL Playground (built into the web UI) is the recommended starting point for integration development — use it to explore the schema, build queries interactively, and validate responses before writing code.
- `pyTenable` is the recommended integration path because it abstracts the GraphQL layer and handles API evolution transparently — the underlying GraphQL schema may change between releases without breaking pyTenable integrations.
- Tenable OT Security was formerly known as Indegy Industrial Cybersecurity Platform (acquired by Tenable in 2019) — legacy documentation and integrations may reference the Indegy name.
- The 2026 release notes indicate active development; check the Tenable release notes page before upgrading to validate API compatibility with existing integrations.
- For port use: Tenable OT Security's risk scoring per asset (combining CVE severity, network exposure, and asset criticality) provides actionable triage for port operators with large asset inventories spanning multiple terminal zones.
- Combine Tenable OT vulnerability data with CISA ICS advisories (`cisa-ics-advisories.md`) and cross-reference against asset inventory from Nozomi Guardian (`nozomi-guardian.md`) or Forescout eyeInspect (`forescout-eyeinspect.md`) for a comprehensive OT vulnerability management picture.
