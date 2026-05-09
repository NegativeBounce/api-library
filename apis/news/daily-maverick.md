# Daily Maverick

Independent South African investigative-journalism publication (Cape Town–based, founded 2009) providing free RSS feeds across politics, business, world, opinion, and investigative ("Scorpio") sections.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-09

## Use cases

- Tracking South African politics, governance, and corruption investigations
- Following continental long-form analysis from a non-paywalled SA outlet
- Building feeds for civic-tech, OSINT, or accountability-journalism tools
- Augmenting News24 or Mail & Guardian feeds with deep-dive investigative content

## Pricing

- **Free tier:** All RSS feeds free; site itself is free-to-read (membership "Maverick Insider" funds the journalism but isn't required for access)
- **Paid tiers:** None for RSS
- **Enterprise:** No documented commercial API; content licensing inquiries via the website
- **Notes:** Daily Maverick relies on reader donations rather than paywalls, so RSS access remains open

## Authentication

None.

## Endpoints

- **Base URL:** `https://www.dailymaverick.co.za/`
- **Key endpoints:**
  - `GET /dmrss/` — main RSS feed
  - Section-specific feeds available by appending category paths (e.g. `/section/politics/feed/`)

## Example call

```bash
curl "https://www.dailymaverick.co.za/dmrss/"
```

## Rate limits

Not publicly documented.

## SDKs / Libraries

- **Official:** None
- **Community:** Standard RSS parsers

## Documentation

- Site: https://www.dailymaverick.co.za/
- RSS: https://www.dailymaverick.co.za/dmrss/

## Notes

Recognized as one of South Africa's leading investigative outlets; "Scorpio" is its dedicated investigative team. No JSON/REST API documented — RSS only. Content covers SA national politics heavily, with regular pan-African and world desks. Site uses standard WordPress-style feed semantics on top of a custom CMS.
