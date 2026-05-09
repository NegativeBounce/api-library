# LifeRaft Navigator

OSINT and threat-intelligence platform spanning surface web, social media, deep web, and dark web. Real-time alerting with AI classification. Acquired by Securitas in February 2026.

**Tier:** Enterprise
**Auth:** API Key / OAuth (via Navigator portal)
**Last researched:** 2026-05-09

## Use cases

- Comprehensive OSINT across surface + social + deep + dark web for Strait-of-Malacca-relevant entities (port operators, charterers, key personnel).
- Real-time alerting on threats to people, assets, brands, and data.
- AI classification for high-volume signal triage.
- Investigation tooling for security analysts (entity pivot, link analysis).
- Cross-platform monitoring including fringe networks and messaging apps.

## Pricing

- **Free tier:** None.
- **Paid tiers:** None publicly listed.
- **Enterprise:** Custom-quoted; multi-thousand-USD-per-month tier typical.
- **Notes:** Securitas acquisition (Feb 2026) may shift packaging and pricing; verify with sales.

## Authentication

API key / OAuth issued via Navigator onboarding. REST API included in all plans.

## Endpoints

- **Public site:** `https://liferaftlabs.com/` (formerly liferaftinc.com)
- **API base URL:** Customer-issued.
- **Surface areas:**
  - OSINT search (surface, social, deep, dark)
  - AI classification / threat-tagging
  - Real-time alerts
  - Analyst workflow / case management

## Example call

```bash
# Illustrative — actual endpoints provisioned per Liferaft contract.
curl -H "Authorization: Bearer $LIFERAFT_TOKEN" \
  "https://api.liferaft.io/v1/search?query=%22strait+of+malacca%22&sources=social,deep,dark&since=2026-05-01"
```

## Rate limits

Not publicly documented.

## SDKs / Libraries

- **Official:** Customer-issued packages.
- **Community:** None notable.

## Documentation

- Main site: https://liferaftlabs.com/
- Securitas integration: https://www.securitas.com/

## Notes

- Strong fit when dark-web coverage matters — relevant if you're concerned about brokered access to vessel-tracking data, leaked crew lists, or insider-threat chatter.
- AI classification reduces analyst workload but vet outputs for false positives.
- Securitas integration may unify Liferaft with broader physical-security workflows.
