# EMSA CleanSeaNet

European Maritime Safety Agency satellite-based oil-spill and vessel-detection service. Sentinel-1 SAR imagery + alert pipeline delivered to participating coastal states for European waters.

**Tier:** Restricted (free for eligible authorities)
**Auth:** Authority login (national contact points)
**Last researched:** 2026-05-09

## Use cases

- **Coverage is European waters only — not the Strait of Malacca.** Catalogued as a methodology and policy reference, plus for vessels routing Strait → Europe.
- Near-real-time alerts on detected oil spills in Member State EEZs.
- Oil-drift modelling (forecast and backtrack) — same models can be reused conceptually for Strait simulations.
- Vessel detection and meteorological / oceanographic data layered on alerts.
- Reference standard for state-level satellite oil-spill response programs.

## Pricing

- **Free tier:** Free for eligible authorities (EU Member States, overseas territories, candidate countries, EFTA).
- **Paid tiers:** Not applicable; service is grant-funded by the EU.
- **Enterprise:** Not applicable.
- **Notes:** Industry / non-EU users cannot directly access — eligibility is gated to national contact authorities.

## Authentication

Authority-level login via dedicated user interface. Each member state has nominated National Contact Authorities.

## Endpoints

- **Public site:** `https://www.emsa.europa.eu/csn-menu.html`
- **No public REST API.** Service delivered via the CleanSeaNet portal to eligible users; alerts are pushed via email and authority-specific channels.

## Example call

```bash
# Not applicable — CleanSeaNet is gated to EU coastal authorities.
# For non-EU equivalents in Strait of Malacca:
#  - Cerulean (SkyTruth) for oil-spill detection.
#  - Copernicus Data Space (cataloged in satellite-imagery) for raw Sentinel-1 SAR access.
```

## Rate limits

Not applicable.

## SDKs / Libraries

- **Official:** None.
- **Community:** None.

## Documentation

- Main page: https://www.emsa.europa.eu/csn-menu.html
- Service catalogue and detection feedback (2015–2024): linked from the EMSA site.

## Notes

- Cataloged as a **policy and methodology reference** for Strait users — the underlying SAR-based detection is the same approach used by Cerulean.
- Indonesia, Malaysia, and Singapore each operate their own oil-spill response services; Tokyo MoU coordinates aspects of regional response. None match CleanSeaNet's productisation.
- Useful background reading for organisations designing a Strait-of-Malacca oil-spill monitoring programme.
