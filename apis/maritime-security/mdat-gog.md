# MDAT-GoG (Maritime Domain Awareness for Trade – Gulf of Guinea)

Joint UK/French regional reporting and advisory centre for the Gulf of Guinea, providing voluntary reporting, incident alerts, and merchant-shipping advisories.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-06-11

> **Government reporting/advisory service, not a programmatic API.** Operated by UKMTO in partnership with the French Marine Nationale MICA Centre. Output is via website, alerts, and direct ship contact — no public REST/JSON feed.

## Use cases

- Verified maritime security alerts and advisories for the Gulf of Guinea (a long-standing piracy/armed-robbery and kidnap-for-ransom hot spot).
- Voluntary reporting and a regional point of contact for merchant vessels transiting the GoG Voluntary Reporting Area.
- Situational awareness for West Africa transit planning, complementing the West Africa & Gulf of Guinea regional feed entry.

## Pricing

- **Free tier:** Free. Public alerts/advisories; voluntary reporting free to participating vessels.
- **Paid tiers:** None.
- **Enterprise:** N/A (government/partnership service).
- **Notes:** Co-run by UKMTO and the French MICA Centre; part of the same regional architecture as UKMTO's Indian Ocean operation.

## Authentication

None for public alerts. Vessels participate by submitting reports per the GoG VRA scheme; emergency contact via the centre's published channels.

## Endpoints

- **Base URL:** No API. Primary source: `https://gog-mdat.org/home`
- **Key surfaces:**
  - Security alerts / warnings for the GoG.
  - Advisories and weekly reporting.
  - Voluntary reporting area guidance.

## Example call

```bash
# No API. Monitor alerts at https://gog-mdat.org/home ; vessels report via the GoG VRA.
```

## Rate limits

N/A (website / direct contact).

## SDKs / Libraries

- **Official:** None.
- **Community:** None.

## Documentation

- Main site: https://gog-mdat.org/home
- Partner: UKMTO (`maritime-security/ukmto.md`) and the French MICA Centre.

## Notes

- The GoG counterpart to UKMTO's Indian Ocean service — the authoritative free source for West Africa maritime security alerts.
- No machine feed: monitor the site or consume via a commercial provider that structures the output.
- Cross-reference: pairs with the `regional-security-feeds/west-africa-gulf-of-guinea.md` region doc and the IMB Piracy Reporting Centre (`maritime-security/imb-piracy-reporting-centre.md`), which is also strong on GoG incidents.
