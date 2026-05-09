# OpenSanctions

Open-data project consolidating 200+ global sanctions lists, PEP records, debarment, criminal watchlists, and other risk data into a single normalized, freely-licensed dataset. Pay-as-you-go API for commercial use; free for non-commercial.

**Tier:** Freemium (PAYG)
**Auth:** API Key
**Last researched:** 2026-05-09

## Use cases

- Vessel-owner / charterer screening against consolidated global sanctions for Strait-of-Malacca counterparties.
- PEP and adverse-media screening on key personnel (port operators, shipping company directors).
- Free fallback / cross-check against commercial vendors (LSEG World-Check, Dow Jones, ComplyAdvantage).
- On-prem deployment via the open-source matching engine (`yente`) for organisations with data-residency requirements.
- Bulk dataset downloads (CC-BY-NC) for research and academic projects.

## Pricing

- **Free tier:** Free for non-commercial users (CC-BY-NC license). 30-day trial API key on signup with a work email.
- **Paid tiers:** Pay-as-you-go at **€0.10 per API call**, billed monthly.
- **Enterprise:** Bulk data license for on-prem / commercial use; custom pricing.
- **Notes:** Open-source software (`yente`) lets you self-host; you only pay for the data license.

## Authentication

API key issued at signup. Sent in the `Authorization: ApiKey <key>` header.

## Endpoints

- **Base URL:** `https://api.opensanctions.org/`
- **Key endpoints:**
  - `GET /search/{dataset}` — full-text search across entities
  - `POST /match/{dataset}` — bulk match a list of names against the dataset
  - `GET /entities/{id}` — fetch a specific entity
  - `GET /catalog` — dataset metadata
- **Datasets:** `default` (everything), `sanctions`, `peps`, `debarment`, `crime`, etc.

## Example call

```bash
# Match a vessel-owner name against the sanctions dataset
curl -X POST "https://api.opensanctions.org/match/sanctions" \
  -H "Authorization: ApiKey $OPENSANCTIONS_KEY" \
  -H "Content-Type: application/json" \
  -d '{"queries": {"q1": {"schema": "Company", "properties": {"name": ["PT Pelayaran Tempuran Emas"], "country": ["id"]}}}}'
```

## Rate limits

Per-tier; defined in the account dashboard. PAYG callers should expect reasonable concurrency (no aggressive throttling for normal use).

## SDKs / Libraries

- **Official:** `opensanctions` (Python).
- **Community:** Various wrappers; the `nomenklatura`/`yente` ecosystem provides matching primitives.

## Documentation

- API site: https://www.opensanctions.org/api/
- API docs: https://api.opensanctions.org/
- Source code (yente): https://github.com/opensanctions/yente
- Datasets: https://www.opensanctions.org/datasets/

## Notes

- Best free / cheapest option for sanctions screening — €0.10/call is roughly an order of magnitude cheaper than commercial peers for low-to-mid volumes.
- Data sources are transparent — every record links back to the underlying authoritative list (OFAC, EU, UK OFSI, UN, etc.).
- For Strait of Malacca: strong fit for screening Indonesian / Malaysian / Singaporean entities against global sanctions in a single call.
- Cross-reference with Pole Star PurpleTRAC (cataloged in `dark-vessel-detection`) for vessel-specific screening workflows.
