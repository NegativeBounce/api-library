# The Shipping Podcast

Long-running independent maritime podcast featuring interviews with shipping, ports, technology, and maritime-security leaders.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-06-11

## Use cases

- Long-form interviews with maritime industry, technology, and security figures — strong qualitative atmospherics and trend-tracking.
- Tracking emerging themes (decarbonisation, autonomy, crewing, security tech) through practitioner voices.
- Complementary podcast coverage alongside The Maritime Executive's "In the Know," Lloyd's List Shipping Podcast, and CIMSEC's Sea Control.

## Pricing

- **Free tier:** Free via standard podcast platforms and RSS.
- **Paid tiers:** None.
- **Enterprise:** N/A.
- **Notes:** Independent, host-led; episode cadence varies.

## Authentication

None.

## Endpoints

- **Base URL:** `https://shippingpodcast.com`
- **Key surfaces:**
  - Site: `https://shippingpodcast.com/`
  - Podcast RSS: available via Apple/Spotify and the site (verify feed URL before use)

## Example call

```bash
# Standard podcast RSS. Find the feed URL via the site or a podcast directory,
# then parse with feedparser / any podcast client.
```

## Rate limits

N/A (podcast RSS).

## SDKs / Libraries

- **Official:** None — standard podcast RSS.
- **Community:** `feedparser` (Python), `rss-parser` (Node.js).

## Documentation

- Main site: https://shippingpodcast.com

## Notes

- Included to round out **podcast** coverage in this category; best treated as qualitative/atmospheric rather than incident reporting.
- Cross-reference the other podcast-bearing entries: `maritime-media/the-maritime-executive.md`, `maritime-media/lloyds-list.md`, `maritime-media/cimsec.md`.
- Verify the current podcast feed URL before wiring into an automated pipeline.
