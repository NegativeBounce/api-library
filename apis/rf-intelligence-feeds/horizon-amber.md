# Horizon Technologies Amber

UK-based maritime SIGINT provider operating the Amber™ CubeSat constellation. Detects and demodulates RF emissions from vessels — sat phones (L-band), commercial satcom datalinks, X/S-band maritime radars, and AIS — providing not just geolocation but actual signal content for "dark vessel" intelligence.

**Tier:** Enterprise (Data-as-a-Service)
**Auth:** Customer-provisioned (via Amber Data Centre)
**Last researched:** 2026-05-10

## Use cases

- Tracking dark vessels (AIS-off ships) through their non-cooperative RF emissions
- Sat phone metadata interception from maritime emitters (calls, GPS positions in metadata)
- Maritime radar fingerprinting (X/S-band) for vessel identification at scale
- Sanctions enforcement, counter-piracy, illegal fishing detection
- L-band datalink monitoring for road/rail logistics tracking (planned expansion beyond maritime)

## Pricing

- **Free tier:** None.
- **Paid tiers:** Subscription-based via the Amber Data Centre. Pricing not public.
- **Enterprise:** Standard route. Anchor customer is the UK National Maritime Information Centre (NMIC); broader UK Government, Royal Navy, and allied government customers. Commercial users (insurance, shipping) accessed via partner network.
- **Notes:** Service is non-ITAR (UK origin) — important for non-US allied customers who can't easily license US RF SIGINT products.

## Authentication

Customer credentials provisioned through Horizon Technologies after contract signing. Data delivered through the Amber Data Centre infrastructure (LN Systems partnership).

## Endpoints

- **Base URL:** Customer-specific Amber Data Centre access (no public API endpoint)
- **Key interfaces:**
  - Amber Processing Centre (APC) — primary government data delivery (Portsmouth, UK)
  - Amber Data Centre (ADC) — commercial customer delivery
  - Geolocations + demodulated signal metadata (sat phone GPS positions, radar emission characteristics) in customer-specified formats
  - Pre-launch terrestrial AmberPersistent stations covered strategic chokepoints; satellite delivery began with IOD-3 (lost at launch Jan 2023) and Amber-Phoenix replacement; Amber-2 launched 2025

## Example call

No public REST example — Amber is delivered through bilateral data-sharing agreements. Vendor contact: via horizontechnologies.eu enquiry forms.

## Rate limits

Bound by satellite revisit times and customer service tier. Each Amber satellite covers ~2.6% of Earth's surface per pass. Constellation cadence is regional/EEZ/global depending on subscription scope.

## SDKs / Libraries

- **Official:** None public.
- **Community:** None — closed enterprise stack.

## Documentation

- Product overview: https://horizontechnologies.eu/sigint-solutions/space-based-maritime-sigint-solutions
- Use-case page: https://horizontechnologies.eu/sigint-applications/sigint-for-non-cooperative-maritime-asset-tracking
- Amber Data Centre commissioning: https://horizontechnologies.eu/news/horizon-commisions-amber-data-center
- Amber-2 launch update (May 2025): https://horizontechnologies.eu/news/uk-satellite-to-combat-illegal-migration-launch-in-2025
- eoPortal mission page: https://space.skyrocket.de/doc_sdat/iod-amber.htm

## Notes

- Differentiator from peers (HawkEye 360, Unseenlabs): Amber **demodulates** signals rather than just geolocating them. Output includes sat phone metadata (numbers, GPS positions encoded in protocol headers) and radar fingerprints, not just RF emitter coordinates.
- Targets specifically: L-band sat phones, Iridium devices, X-band maritime radar, S-band maritime radar (SOLAS Reg 19 mandates S-band for ships >3000 GT).
- Mono-satellite design (no triangulation cluster needed) — simpler than Kleos's 4-sat clusters or HawkEye's 3-sat clusters.
- Sister product: airborne FlyingFish™ SIGINT pod (separate hardware product, used by ISR aircraft globally) — relevant if you want both space and airborne data from the same vendor.
- Cross-listing: maritime focus overlaps `dark-vessel-detection` and `maritime-security`.
