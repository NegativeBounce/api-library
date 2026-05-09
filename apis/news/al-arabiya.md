# Al Arabiya English

The English-language service of Saudi state-owned Al Arabiya News Channel, launched in 2007 and headquartered in Riyadh, with correspondents across the region. Provides a Flipboard RSS feed and full free website access; positions itself as Al Jazeera's main pan-Arab competitor.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-09

## Use cases

- Saudi-perspective Middle East news monitoring (politics, business, Gulf affairs)
- Tracking Saudi Vision 2030, NEOM, Aramco, and Saudi-led regional initiatives in English
- Pan-Arab news with explicit Riyadh editorial lens — useful as a counterweight to Al Jazeera's Doha lens
- Building MENA news readers, alerting tools, and source-comparison dashboards

## Pricing

- **Free tier:** Flipboard RSS free; full website free to read with no paywall
- **Paid tiers:** None
- **Enterprise:** Content licensing handled via MBC Group / Middle East News FZ-LLC; contact `contactus@alarabiya.net`
- **Notes:** Funded entirely through Saudi state ownership and broadcast/advertising revenue

## Authentication

None.

## Endpoints

- **Base URL:** `https://english.alarabiya.net/`
- **Key endpoints:**
  - `GET /feed/flipboard/en.xml` — main all-news Flipboard RSS feed
  - Section sites consumable via HTML: `/News/middle-east`, `/News/gulf`, `/News/world`, `/business`, `/views`, `/lifestyle`, `/sports`
  - Live stream: `/live-stream`

## Example call

```bash
curl "https://english.alarabiya.net/feed/flipboard/en.xml"
```

## Rate limits

Not publicly documented.

## SDKs / Libraries

- **Official:** Al Arabiya English iOS and Android apps with live streaming of Al Arabiya and Al Hadath channels (no developer SDKs)
- **Community:** Standard RSS parsers; community RSS-bridge configurations exist for the main domain

## Documentation

- Main site: https://english.alarabiya.net/
- About: https://english.alarabiya.net/about
- Contact: `contactus@alarabiya.net`

## Notes

Al Arabiya English is the English language service of the **Saudi state-owned** Al Arabiya News Channel, owned by MBC Group and operated through Middle East News FZ-LLC, headquartered in Riyadh. Launched in 2007. Editorial line is widely understood as aligned with Saudi government interests and is explicitly state-owned (in contrast to Al Jazeera, which is partially state-funded but formally operates as an independent broadcaster). Notable editorial events include 2012 stories on leaked emails of Syrian UN envoy's daughter and a March 2015 op-ed urging Obama to "listen to Netanyahu" on the Iran nuclear deal. For source-trust analysis: prominently flag Saudi state ownership when comparing against Al Jazeera, Tehran Times, Times of Israel, etc. The Flipboard RSS is the most reliable structured feed; no public REST/JSON developer API is documented.
