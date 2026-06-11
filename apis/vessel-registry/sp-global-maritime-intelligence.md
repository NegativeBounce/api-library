# S&P Global Maritime Intelligence

Enterprise maritime data from the manager of the IMO number schemes, unifying vessel ownership, particulars, financial data and risk profiles with Capital IQ corporate intelligence.

**Tier:** Enterprise
**Auth:** API Key / OAuth
**Last researched:** 2026-06-11

## Use cases

- Authoritative vessel particulars and ownership tied to the IMO number scheme S&P administers.
- Bridging maritime assets to corporate/financial intelligence via Capital IQ identifiers for investment and compliance due diligence.
- Validating ownership, ports/berths and ship particulars against S&P's proprietary datasets for defensible decisions.
- Feeding unified ownership + risk profiles into a maritime intelligence platform via API.

## Pricing

- **Free tier:** None.
- **Paid tiers:** Subscription/contract.
- **Enterprise:** Contact sales; API integration plus web dashboards.
- **Notes:** Pricing not public. Built on 300+ years of maritime data heritage (ex-IHS Markit / Lloyd's Register heritage datasets) and S&P's role managing the IMO numbering schemes.

## Authentication

API key / OAuth per contract. Credentials and endpoint schema provided at onboarding; data ingestible into customer or third-party platforms.

## Endpoints

- **Base URL:** Provided on contract (see spglobal.com/market-intelligence maritime solutions).
- **Key endpoints:**
  - Vessel particulars & ownership (IMO-scheme-aligned).
  - Risk profiles and validation datasets (AIS, ports & berths, ship particulars).
  - Capital IQ identifier linkage for corporate/financial intelligence.

## Example call

```bash
# Illustrative; endpoints/auth provided during onboarding
curl -H "Authorization: Bearer $SPG_TOKEN" \
  "https://api.spglobal.com/maritime/v1/vessels/9811000/ownership"
```

## Rate limits

Per contract; not publicly published.

## SDKs / Libraries

- **Official:** API integration documented at onboarding; web dashboards provided alongside.
- **Community:** None notable.

## Documentation

- Main docs: https://www.spglobal.com/market-intelligence/en/solutions/maritime-intelligence
- API reference: Provided on contract.

## Notes

- **Cross-reference:** S&P Global Maritime is also cataloged in `port-state-control`. This entry covers the distinct **vessel particulars / ownership / financial-linkage** angle. Same vendor, different use case — not a duplicate file in the same folder.
- As administrator of the IMO number schemes, S&P is a primary-source-adjacent authority; strong for defensible ownership in regulated workflows.
- The Capital IQ linkage is a differentiator for investment/finance personas (e.g. maritime mining-platform companies assessing counterparties).
- Underpins much third-party data (Equasis ship data is IHS/S&P-sourced); choosing S&P direct gives redistribution terms Equasis can't.
