# JSONCargo

Developer-first maritime REST API that resolves a Bill of Lading number into its associated container numbers and live tracking, plus vessel and port data, across 95%+ of shipping lines.

**Tier:** Paid
**Auth:** API key
**Last researched:** 2026-06-17

## Use cases

- Given a B/L number, fetch every container associated with it, then track each container's journey (ATD, ETA, port events, vessel).
- Resolve which vessel is carrying a given shipment via the BoL → container → vessel chain.
- Multi-carrier container visibility (Maersk, MSC, CMA CGM, ZIM, Hapag-Lloyd, ONE, COSCO, Evergreen, etc.) through one unified API.

## Pricing

- **Free tier:** None permanent; paid plans start with a reduced first-period trial (e.g., €9 first week on Mariner) then convert to full monthly price.
- **Paid tiers (individual):**
  - Mariner — €9 trial then €99/mo, 1,000 API calls/mo (~€0.099/request).
  - Navigator — €22 trial then €199/mo, 2,500 API calls/mo (~€0.080/request).
  - Admiral — €39 trial then €349/mo, 5,000 API calls/mo (~€0.070/request).
- **Enterprise:** Higher-volume/Pro plans and overage purchasing available; contact sales.
- **Notes:** Every request counts as one API call regardless of repeat tracking. No contract; cancel anytime; 2-week money-back guarantee. Overage billed at plan rate.

## Authentication

API key issued on signup/checkout, sent in the request header. Keys are delivered by email after payment along with documentation.

## Endpoints

- **Base URL:** `https://api.jsoncargo.com` (see documentation for exact versioned paths)
- **Key endpoints:**
  - `GET` Bill of Lading — fetch all container numbers tied to a B/L number (requires the carrier/shipping-line name).
  - `GET` Container tracking — real-time milestones, port/terminal events, ETA for a container.
  - `GET` Vessel — vessel details by UUID, MMSI, or IMO (single, bulk up to 100, and static ship data).
  - `GET` Port / Terminal finder — port and terminal details.

## Example call

```bash
# Resolve containers for a Bill of Lading (carrier/shipping-line name required).
# Confirm exact path and param names in the JSONCargo documentation.
curl -H "X-Api-Key: $JSONCARGO_API_KEY" \
  "https://api.jsoncargo.com/v1/bill-of-lading?bol=ABCD1234567&shipping_line=MAERSK"
```

## Rate limits

Bounded by plan monthly call quotas (1,000 / 2,500 / 5,000). Overage either errors or is billed per the plan rate; upgrade for higher limits. No separate published per-second limit.

## SDKs / Libraries

- **Official:** None published (language-agnostic REST; examples in multiple languages in the docs). GitHub: github.com/jsoncargo.
- **Community:** None notable.

## Documentation

- Main docs: https://jsoncargo.com/documentation-api/
- API reference: https://jsoncargo.com/bill-of-lading-api/ and https://jsoncargo.com/pricing-plans/

## Notes

This is the cleanest answer to "what's on / which vessel carries this BoL" via a self-serve public API. It does NOT return the underlying customs cargo description (HS code, shipper/consignee) — for that use the customs/BoL trade-data vendors in this category. The BoL endpoint requires you to supply the correct shipping-line name. Overlaps the catalog's `maritime-ais` (it also exposes IMO/MMSI vessel lookups) but is distinct in its BoL→container resolution.
