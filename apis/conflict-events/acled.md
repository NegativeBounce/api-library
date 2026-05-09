# ACLED (Armed Conflict Location & Event Data)

The most widely-cited open dataset of political violence and protest events worldwide. Provides incident-level data on battles, violence against civilians, protests, riots, and strategic developments via a free public REST API. Strong coverage of Indonesia, Malaysia, Thailand, and the rest of Southeast Asia relevant to the Strait of Malacca.

**Tier:** Freemium
**Auth:** API Key (registered email)
**Last researched:** 2026-05-09

## Use cases

- Daily / weekly tracking of protests, riots, and political violence in Indonesia (Sumatra, Riau, Aceh), Malaysia, Singapore, and Thailand — relevant for civil-unrest risk to vessels in port and crew shore leave.
- Dataset for trend analysis (e.g., escalation in Aceh, communal violence near Belawan).
- Pattern-of-life modelling: which port cities have surges in event frequency before unrest.
- Cross-validation against commercial conflict-event feeds (Dataminr, Factal, RANE).
- Free academic / NGO use; tiered enterprise commercial use.

## Pricing

- **Free tier:** Academic, journalist, and non-commercial users get free API access after registration. ACLED requests "respectful and measured" usage.
- **Paid tiers:**
  - **myACLED Research / Partner / Enterprise:** Tiered paid access with disaggregated and near-real-time data. Pricing not publicly published.
- **Enterprise:** Government and large-corporate contracts; contact `access@acleddata.com`.
- **Notes:** Free tier carries citation requirements. Commercial use requires a paid tier.

## Authentication

Email-based API key. Pass `email` + `key` query parameters on every call. Register at acleddata.com.

## Endpoints

- **Base URL:** `https://api.acleddata.com/`
- **Key endpoints:**
  - `GET /acled/read` — main event data endpoint (filtering by country, region, event_type, date range, fatalities)
  - `GET /actor/read` — actor metadata
  - `GET /actortype/read` — actor type lookup
  - `GET /country/read` — country list
  - `GET /region/read` — region list

## Example call

```bash
# Recent political violence and protests in Indonesia and Malaysia
curl "https://api.acleddata.com/acled/read?email=$ACLED_EMAIL&key=$ACLED_KEY&country=Indonesia|Malaysia&event_date=2026-04-01|2026-05-09&event_date_where=BETWEEN"
```

## Rate limits

Not strictly published; ACLED relies on responsible-use norms and may throttle abusive callers. Datasets refreshed weekly (free tier) or near-real-time (paid tiers).

## SDKs / Libraries

- **Official:** None.
- **Community:** `acled` (PyPI Python package), R / Stata wrappers used in academic work.

## Documentation

- Main API docs: https://acleddata.com/acled-api-documentation
- Getting started: https://acleddata.com/api-documentation/getting-started
- myACLED FAQ: https://acleddata.com/myacled-faqs

## Notes

- ACLED is the de-facto baseline for protest / conflict event monitoring globally — every commercial intelligence shop benchmarks against ACLED.
- For the Strait of Malacca specifically: ACLED's Indonesia file is rich; track "Riots" and "Protests" near port cities (Belawan, Dumai, Tanjung Balai) as leading indicators.
- Citation: "ACLED — Raleigh, et al. (2010)." Required when publishing analysis.
