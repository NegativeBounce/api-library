# ComplyAdvantage Mesh

Cloud-based AML risk intelligence and compliance platform combining sanctions, PEP, and adverse-media screening with case management, transaction monitoring, and AI-powered auto-remediation. Strong fit for fintech and modern compliance teams.

**Tier:** Paid (Enterprise pricing model)
**Auth:** API Key / OAuth
**Last researched:** 2026-05-09

## Use cases

- Counterparty screening — sanctions, PEPs, adverse media — on Strait-of-Malacca shipping companies, charterers, and trade-finance counterparties.
- Customer onboarding screening with AI-powered auto-remediation (claims 65–85% of profiles can be processed automatically).
- Ongoing monitoring with near-real-time alert generation as risk profiles change.
- Transaction screening for marine trade-finance and bunker-payment flows.
- Integration via API, batch, or SFTP — flexible delivery for varied IT estates.

## Pricing

- **Free tier:** None.
- **Paid tiers:** None publicly listed.
- **Enterprise:** Custom-quoted; pricing scales with screening volume, modules selected, and seats.
- **Notes:** Targeted at fintechs and modern compliance teams — onboarding is faster than legacy enterprise vendors.

## Authentication

API key issued post-contract; OAuth 2.0 supported on newer endpoints.

## Endpoints

- **Public site:** `https://complyadvantage.com/`
- **Developer docs:** `https://docs.complyadvantage.com/`
- **API base URL:** `https://api.complyadvantage.com/`
- **Surface areas:**
  - Searches (sanctions, PEP, adverse media)
  - Cases / case management
  - Transaction monitoring
  - Companies / Customers (KYB / KYC)
  - Webhooks for alert delivery

## Example call

```bash
# Search for an entity across sanctions / PEP / adverse media
curl -H "Authorization: Token $COMPLYADVANTAGE_KEY" \
  "https://api.complyadvantage.com/searches?api_key=$COMPLYADVANTAGE_KEY" \
  -X POST -H "Content-Type: application/json" \
  -d '{"search_term":"PT Pelayaran Tempuran Emas","client_ref":"strait-001","fuzziness":0.6,"types":["sanction","pep","adverse-media"]}'
```

## Rate limits

Plan-dependent; published in the developer dashboard.

## SDKs / Libraries

- **Official:** Python and Node SDKs.
- **Community:** Various integrations (LangChain, Zapier, etc.).

## Documentation

- Main site: https://complyadvantage.com/our-data/
- API docs: https://docs.complyadvantage.com/

## Notes

- Strong fit when speed-to-onboarding matters more than market-cap brand prestige (vs. World-Check / Dow Jones).
- Auto-remediation AI is genuinely useful for high-volume screening workloads — review false-positive rates carefully during pilot.
- SOC 2 Type II + ISO 27001 — strong security posture.
