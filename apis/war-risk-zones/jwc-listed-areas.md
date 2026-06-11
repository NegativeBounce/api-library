# JWC Listed Areas (Lloyd's Market Association / IUA)

The canonical London-market list of geographical "Areas of Perceived Enhanced Risk" for Hull War, Piracy, Terrorism and related perils, published by the Joint War Committee.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-06-11

> **Not a programmatic API.** The JWC publishes its Listed Areas as dated PDF circulars (e.g. JWLA-033). There is no official REST/JSON feed. Consume by fetching the latest circular PDF and parsing, or by licensing a downstream vendor (see Notes).

## Use cases

- Defining the authoritative war-risk zone boundaries that drive additional war-risk premium (AP) for any maritime intelligence report.
- Determining whether a voyage/port call falls inside a Listed Area for underwriting, charterparty "safe port" analysis, and transit-cost estimation.
- Anchoring a war-risk product to the same source insurers and war-risk brokers actually price against.
- Tracking quarterly changes to the risk map (additions/removals) as a leading indicator of shifting geopolitical risk.

## Pricing

- **Free tier:** The Listed Areas circulars are published free by LMA/IUA. Full LMA members additionally access Herminius' JWC Quarterly Briefings.
- **Paid tiers:** None for the list itself.
- **Enterprise:** N/A.
- **Notes:** The JWC sets the areas, not the rating — premium is negotiated between underwriters and brokers. The JWC is advised by independent security advisers (Herminius).

## Authentication

None for the public circulars. Member briefings require LMA membership login.

## Endpoints

- **Base URL:** No API. Primary sources:
  - LMA committee page: `https://lmalloyds.com/committee/joint-war-committee/`
  - IUA risk list: `https://www.iua.co.uk/` (Joint War Committee Risk List)
  - Latest circular PDFs are mirrored by P&I clubs and brokers (e.g. Skuld, Alandia, Filhet-Allard).
- **Key "endpoints":** Latest circular PDF (currently JWLA-033, dated 3 March 2026).

## Example call

```bash
# No API. Fetch the latest circular PDF and parse the Listed Areas, e.g.:
curl -L -o jwla-033.pdf \
  "https://lmalloyds.com/wp-content/uploads/2026/03/JWLA-033_Iran.pdf"
```

## Rate limits

N/A (static PDF documents).

## SDKs / Libraries

- **Official:** None.
- **Community:** None official; downstream platforms (e.g. jwla.ai) operationalize the list.

## Documentation

- Main docs: https://lmalloyds.com/committee/joint-war-committee/
- Reference: https://www.iua.co.uk/ (Joint War Committee Risk List)

## Notes

### Current Listed Areas — JWLA-033 (dated 3 March 2026)

> These areas change roughly quarterly. Always re-fetch the latest circular before relying on this list.

- **Africa:** Benin; Cabo Delgado (waters as defined); Djibouti; Eritrea (south of 18°N only); Gulf of Guinea (waters as defined); Libya; Nigeria; Somalia; Sudan; Togo.
- **Europe:** Sea of Azov and Black Sea waters plus inland waters (as defined).
- **Persian/Arabian Gulf, Gulf of Oman, Indian Ocean, Gulf of Aden and Southern Red Sea** (waters as defined).
- **Asia:** Pakistan.
- **Middle East:** Bahrain; Iran; Iraq (incl. all Iraqi offshore oil terminals); Israel; Kuwait; Lebanon; Oman; Qatar; Saudi Arabia (Gulf coast); Saudi Arabia (Red Sea coast, excluding transits); Syria; UAE; Yemen.
- **Russia.**
- **South America:** Guyana (only calls to offshore installations in the Guyanese EEZ beyond territorial waters).

JWLA-033 changes vs. prior list: added Bahrain, Djibouti, Kuwait, Oman, Qatar; amended the Persian/Arabian Gulf–Gulf of Oman–Indian Ocean–Gulf of Aden–Southern Red Sea boundary definition.

- The precise lat/long boundary definitions ("as defined overleaf") are in the circular PDF — essential for accurate geofencing; do not approximate from the country names alone.
- Cross-reference: pairs naturally with `regional-security-feeds` (operational security) and `geopolitical-risk` (forward-looking risk). JWC is the insurance-pricing layer specifically.
