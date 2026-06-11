# IUA Joint War Committee Risk List

The International Underwriting Association's publication of the Joint War Committee's list of areas of perceived enhanced risk for hull war, strikes, terrorism and related perils.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-06-11

> **Not a programmatic API.** The IUA hosts/references the same JWC Listed Areas as the LMA; distribution is via web pages and PDF circulars, not a feed.

## Use cases

- Accessing the JWC Listed Areas from the IUA (company-market) side, complementing the LMA (Lloyd's) publication.
- Confirming the current risk list and its independent-consultant risk-benchmark framing for underwriting context.
- Citing a second authoritative London-market source for the same war-risk zone definitions in reports.

## Pricing

- **Free tier:** Free public access to the risk list.
- **Paid tiers:** None.
- **Enterprise:** N/A.
- **Notes:** The IUA and LMA jointly constitute the Joint War Committee; this is the IUA-side reference to the same product cataloged in `jwc-listed-areas.md`.

## Authentication

None for the public list.

## Endpoints

- **Base URL:** No API.
  - IUA Joint War Committee Risk List page: `https://www.iua.co.uk/` (Underwriting → Committees → Joint War Committee Risk List)
- **Key "endpoints":** Current Listed Areas reference (mirrors the latest JWLA circular).

## Example call

```bash
# No API. Reference page (navigate to the Joint War Committee Risk List):
#   https://www.iua.co.uk/IUA_Member/IUANew/UnderwritingItems/Committees/Joint_War_Committee_Risk_List.aspx
```

## Rate limits

N/A (web pages / PDFs).

## SDKs / Libraries

- **Official:** None.
- **Community:** None.

## Documentation

- Main docs: https://www.iua.co.uk/ (Joint War Committee Risk List)
- Reference: https://lmalloyds.com/committee/joint-war-committee/

## Notes

- **Cross-reference:** This is the IUA companion to `jwc-listed-areas.md` (LMA). Same underlying Listed Areas (currently JWLA-033, 3 March 2026). Kept as a separate entry because the IUA is a distinct publishing body/source, but the area definitions are identical — use the LMA circular PDF for authoritative boundary coordinates.
- Areas note that listed ports/places/coasts have been assessed by an independent consultant to exceed an enhanced-risk benchmark.
- Rating/premium is negotiated between underwriters and brokers; the committee plays no role in pricing.
