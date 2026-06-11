# TAPA Incident Information Service (TIS)

Member-reported cargo-crime incident database run by the Transported Asset Protection Association, covering facility and in-transit theft across EMEA, the Americas, and APAC.

**Tier:** Enterprise
**Auth:** Member login (portal)
**Last researched:** 2026-06-11

> **Member-access incident database, not a public self-serve API.** TIS (the TAPA EMEA Intelligence System / Incident Information Service) is available to TAPA members; data is member-reported and portal-delivered.

## Use cases

- Historic and current cargo-theft incident intelligence for secure route and parking planning (when/where/how criminals target supply chains, and the products most stolen).
- Facility, trucking, and secure-parking risk assessment aligned to TAPA's certifiable security Standards (FSR, TSR, PSR).
- Country/hotspot monitoring — TIS regularly ranks incident counts by country (e.g. Germany, Spain, Italy, South Africa, France, UK, Netherlands, Poland in EMEA reporting).
- Contributing and consuming member-reported incidents to improve regional coverage.

## Pricing

- **Free tier:** None (TIS is a member benefit; some aggregate stats appear in free co-authored reports).
- **Paid tiers:** TAPA membership (association dues) grants TIS access — not publicly priced.
- **Enterprise:** Corporate/LSP membership tiers — contact TAPA.
- **Notes:** Three regional bodies (TAPA EMEA, Americas, APAC); TIS / TAPA EMEA Intelligence System is the EMEA platform.

## Authentication

Member portal login provisioned with TAPA membership. No documented public self-serve API.

## Endpoints

- **Base URL:** No public API. Member portal (TIS / IIS).
- **Key surfaces:**
  - Incident database (member-reported cargo crimes).
  - Route/parking planning intelligence.
  - Standards and audit resources.

## Example call

```bash
# No public self-serve API. TIS incident data is accessed via the TAPA member portal.
# Members submit incidents to (EMEA) tisteam@tapaemea.org.
```

## Rate limits

N/A (member portal).

## SDKs / Libraries

- **Official:** None.
- **Community:** None.

## Documentation

- TAPA EMEA: https://www.tapaemea.org/
- Global: https://www.tapa-global.org/

## Notes

- TIS is **member-reported**, so coverage tracks membership density — strongest in EMEA, growing in Americas/APAC. Quality depends on members reporting, which TAPA actively advocates.
- Complements claims-based (TT Club) and platform datasets (Verisk CargoNet, BSI SCREEN); TAPA co-authors the annual cargo theft report with BSI and TT Club.
- Cross-reference: `cargo-crime/bsi-connect-screen.md`, `cargo-crime/tt-club.md`, `cargo-crime/verisk-cargonet.md`.
- Membership is the gate to programmatic-grade access; confirm data-export/integration terms with TAPA for your build.
