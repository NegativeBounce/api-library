# Brandwatch (Cision)

Enterprise digital consumer-research and social listening platform analyzing 1.4T+ posts across 100M+ online sources back to 2008. Owned by Cision since 2021. Strong fit for narrative tracking and brand/asset monitoring around Strait of Malacca topics.

**Tier:** Enterprise
**Auth:** API Key (Bearer token via Brandwatch developer portal)
**Last researched:** 2026-05-09

## Use cases

- Long-horizon narrative tracking on "Strait of Malacca," port labour disputes, environmental incidents, piracy events.
- Sentiment-and-theme analysis using Iris (Brandwatch's AI assistant).
- Visual-listening (image classification) for brand/logo and scene detection — useful for surfacing photos of incidents from social posts.
- Custom classifiers for organization-specific topics (e.g., "loitering vessel near Belawan").
- Historical archive (back to 2008) for trend modeling.

## Pricing

- **Free tier:** None.
- **Paid tiers:** Enterprise only; not publicly listed. Generally Tier-1 pricing comparable to Talkwalker / Meltwater.
- **Enterprise:** Custom-quoted per data volume, sources, seats, and modules.
- **Notes:** "Reviews" product was sunsetted into Consumer Research; clarify scope during procurement.

## Authentication

Bearer token issued via Brandwatch developer portal after Enterprise contract.

## Endpoints

- **Public site:** `https://www.brandwatch.com/`
- **Developer portal:** `https://developers.brandwatch.com/`
- **Surface areas:**
  - Mentions / Queries — historical and ongoing search
  - Custom classifiers + image recognition
  - Iris AI summaries
  - Channels — owned-channel data unification

## Example call

```bash
# Illustrative — actual endpoints provisioned per Brandwatch contract.
curl -H "Authorization: Bearer $BRANDWATCH_TOKEN" \
  "https://api.brandwatch.com/projects/{projectId}/data/mentions?queryId=...&pageSize=500"
```

## Rate limits

Plan-dependent; not publicly documented.

## SDKs / Libraries

- **Official:** None broadly distributed; integration partners abound.
- **Community:** Various Python/Node wrappers.

## Documentation

- Main site: https://www.brandwatch.com/products/consumer-research/
- Developer portal: https://developers.brandwatch.com/

## Notes

- Strongest brand-research and consumer-insight platform among the social listening tools.
- For Strait-of-Malacca security ops specifically, Brandwatch is heavier-weight than needed; Talkwalker and Meltwater have stronger ops-focused workflows.
- Iris generative AI is helpful for analyst summarisation but not a replacement for raw-data export.
