# Information Fusion Centre (IFC), Singapore

Regional maritime security information-sharing hub hosted by the Republic of Singapore Navy, providing maritime domain awareness, incident alerts, and a partner-facing information portal (IRIS) for the Asia/Indo-Pacific region.

**Tier:** Free
**Auth:** None (public) / Partner access (portal)
**Last researched:** 2026-06-11

> **Government information-sharing centre, not a public self-serve API.** Public products are advisories/reports; deeper real-time sharing (IRIS portal) is for linked agencies/International Liaison Officers.

## Use cases

- Regional maritime situational awareness and incident alerts for Southeast Asia, the Strait of Malacca/Singapore Strait, and the wider Indo-Pacific.
- Cross-referencing piracy/armed-robbery, sea robbery, smuggling and other maritime-crime incidents across the region.
- Accessing fused information shared by partner navies/agencies and International Liaison Officers (ILOs) hosted at the centre.

## Pricing

- **Free tier:** Free public advisories/reports. Voluntary information sharing for partners.
- **Paid tiers:** None.
- **Enterprise:** N/A (government/military-hosted).
- **Notes:** Hosts International Liaison Officers from many navies; operates the IRIS (Information sharing) portal for linked centres.

## Authentication

None for public advisories. The IRIS portal and deeper data sharing require partner/agency access (not commercially provisioned).

## Endpoints

- **Base URL:** No public API. Primary source: `https://www.ifc.org.sg/`
- **Key surfaces:**
  - Public maritime security advisories/reports.
  - IRIS portal (partner/ILO access) for real-time information sharing.
  - Incident categorization across the region's maritime-crime threat types.

## Example call

```bash
# No public self-serve API. Monitor advisories at https://www.ifc.org.sg/
# IRIS portal access is for linked agencies / International Liaison Officers.
```

## Rate limits

N/A (website / partner portal).

## SDKs / Libraries

- **Official:** None.
- **Community:** None.

## Documentation

- Main site: https://www.ifc.org.sg/
- Regional partner of ReCAAP ISC (`maritime-security/recaap-isc.md`).

## Notes

- Strong **Southeast Asia / Malacca-Singapore Strait** coverage; complements ReCAAP ISC (Asia-wide piracy reporting) and IMB.
- Like UKMTO/MDAT-GoG, it is an information-sharing centre rather than a programmatic feed — operationalize by monitoring advisories or via a commercial aggregator.
- Cross-reference: `regional-security-feeds/southeast-asia-strait-of-malacca.md` (region doc), `maritime-security/recaap-isc.md`, and `maritime-security/imb-piracy-reporting-centre.md`.
