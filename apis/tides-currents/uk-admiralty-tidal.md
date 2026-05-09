# UK Admiralty (UKHO) Tidal API

UK Hydrographic Office API platform delivering authoritative tidal-height and tidal-stream predictions for British Isles and Irish waters. Built on the UK's largest network of tidal stations. Tiered access: free Discovery, paid Foundation, paid Premium.

**Tier:** Freemium (Discovery free); Paid (Foundation, Premium)
**Auth:** Subscription Key (Azure API Management)
**Last researched:** 2026-05-09

## Use cases

- Authoritative UK / Irish tidal data — **not directly applicable to the Strait of Malacca** but cataloged as a reference and for any UK-flagged vessel ops in home waters.
- Tidal-stream predictions at named stream locations — useful for high-current pilotage analogues to similar work in the Strait.
- Premium tier provides 1 year of forward and historical tidal data at high resolution — best-in-class quality for UKHO-coverage area.
- Reference standard for tidal-prediction quality (UKHO is widely used by classification societies).

## Pricing

- **Free tier (Discovery):** 1-year subscription giving access to "current + 6 days" of tidal data. Free.
- **Paid tiers:**
  - **Foundation:** £144 (inc. VAT) per year.
  - **Premium:** Higher tier providing historical + current + 1 year of tidal events and interval predictions across UK + Irish stations. Pricing on request.
- **Enterprise:** Custom volume / on-prem contracts via UKHO Products team.
- **Notes:** Renewals managed via the Customer Portal; subscription keys rotate per period.

## Authentication

Azure API Management subscription key in `Ocp-Apim-Subscription-Key` header. Obtained via the ADMIRALTY Maritime Data Solutions developer portal.

## Endpoints

- **Developer portal:** `https://admiraltyapi.portal.azure-api.net/`
- **Tidal API (Discovery / Foundation):** `https://admiralty.azure-api.net/uktidalapi/api/V1/`
- **Tidal API (Premium):** `https://admiralty.azure-api.net/uktidalapi-premium/api/V2/`
- **Key endpoints:**
  - `GET /Stations` — list of tidal stations
  - `GET /Stations/{stationId}/TidalEvents` — high/low events
  - `GET /Stations/{stationId}/TidalHeights` — heights at intervals

## Example call

```bash
curl -H "Ocp-Apim-Subscription-Key: $UKHO_KEY" \
  "https://admiralty.azure-api.net/uktidalapi/api/V1/Stations/0001/TidalEvents?duration=7"
```

## Rate limits

Defined per subscription tier in the API Management portal; not publicly listed in detail.

## SDKs / Libraries

- **Official:** None published; the API is consumed via standard HTTP clients.
- **Community:** Some open-source examples on GitHub.

## Documentation

- API home: https://www.admiralty.co.uk/access-data/apis
- API catalogue (gov.uk): https://www.api.gov.uk/ukho/
- Foundation tier KB: https://customerportal.admiralty.co.uk/knowledgebase/article/KBA-02839-N3V1/en-us

## Notes

- **Coverage is UK + Ireland only.** This entry is cataloged because the user asked for it and because UKHO methodology is the gold standard for tide-prediction quality.
- For Strait of Malacca tidal data, the right tools are WorldTides, Stormglass Tide, or local hydrographic offices (Singapore MPA, Indonesia BIG, Malaysia Department of Survey and Mapping).
- UKHO does sell ADMIRALTY Total Tide as a product covering global tides, but that is a desktop / file product, not an API.
